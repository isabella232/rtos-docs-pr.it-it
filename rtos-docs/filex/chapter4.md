---
title: Capitolo 4-Descrizione dei servizi FileX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi FileX di Azure RTO in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c9e91244856b322d53f85bdd572bd317a055776a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822448"
---
# <a name="chapter-4--description-of-azure-rtos-filex-services"></a><span data-ttu-id="08a18-103">Capitolo 4-Descrizione dei servizi FileX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="08a18-103">Chapter 4- Description of Azure RTOS FileX services</span></span>

<span data-ttu-id="08a18-104">Questo capitolo contiene una descrizione di tutti i servizi FileX di Azure RTO in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="08a18-104">This chapter contains a description of all Azure RTOS FileX services in alphabetic order.</span></span> <span data-ttu-id="08a18-105">I nomi dei servizi sono progettati in modo da raggruppare tutti i servizi simili.</span><span class="sxs-lookup"><span data-stu-id="08a18-105">Service names are designed so all similar services are grouped together.</span></span>

## <a name="fx_directory_attributes_read"></a><span data-ttu-id="08a18-106">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-106">fx_directory_attributes_read</span></span>

<span data-ttu-id="08a18-107">Legge gli attributi di directory</span><span class="sxs-lookup"><span data-stu-id="08a18-107">Reads directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-108">Prototype</span></span>

```c
UINT fx_directory_attributes_read ( 
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes_ptr);
```

### <a name="description"></a><span data-ttu-id="08a18-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-109">Description</span></span>

<span data-ttu-id="08a18-110">Questo servizio legge gli attributi della directory dal supporto specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-110">This service reads the directory's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-111">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-111">Input Parameters</span></span>

- <span data-ttu-id="08a18-112">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-112">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-113">**DIRECTORY_NAME**: puntatore al nome della directory richiesta (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-113">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="08a18-114">**attributes** _Ptr: puntatore alla destinazione per gli attributi della directory da inserire.</span><span class="sxs-lookup"><span data-stu-id="08a18-114">**attributes** _ptr: Pointer to the destination for the directory's attributes to be placed.</span></span> <span data-ttu-id="08a18-115">Gli attributi di directory vengono restituiti in un formato mappa di bit con le seguenti impostazioni possibili:</span><span class="sxs-lookup"><span data-stu-id="08a18-115">The directory attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="08a18-116">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-116">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="08a18-117">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-117">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="08a18-118">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="08a18-118">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="08a18-119">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="08a18-119">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="08a18-120">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="08a18-120">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="08a18-121">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="08a18-121">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-122">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-122">Return Values</span></span>

- <span data-ttu-id="08a18-123">Lettura degli attributi di directory riusciti **FX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-123">**FX_SUCCESS** (0x00) Successful directory attributes read</span></span>
- <span data-ttu-id="08a18-124">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-124">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-125">Impossibile trovare la directory specificata di **FX _NOT** (0x04) nel supporto</span><span class="sxs-lookup"><span data-stu-id="08a18-125">**FX _NOT FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="08a18-126">La voce **FX_NOT_DIRECTORY** (0x0E) non è una directory</span><span class="sxs-lookup"><span data-stu-id="08a18-126">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="08a18-127">Errore di I/O driver **FX_IO_ERROR** (0x90)</span><span class="sxs-lookup"><span data-stu-id="08a18-127">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="08a18-128">Il file **FX_FILE_CORRUPT** 0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-128">**FX_FILE_CORRUPT** 0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-129">Settore **FX_SECTOR_INVALID** (0X89) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-129">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="08a18-130">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="08a18-130">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="08a18-131">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-131">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-132">Supporto di **FX_MEDIA_INVALID** (0x02) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-132">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="08a18-133">**FX_PTR_ERROR** (0x18) puntatore del supporto non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-133">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="08a18-134">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-134">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-135">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-135">Allowed From</span></span>

<span data-ttu-id="08a18-136">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-136">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-137">Example</span></span>

```c
FX_MEDIA     my_media;
UINT     status;
/* Retrieve the attributes of "mydir" from the specified media.*/
status = fx_directory_attributes_read(&my_media, "mydir", &attributes);
/* If status equals FX_SUCCESS, "attributes" contains the directory attributes of "mydir". */
```

### <a name="see-also"></a><span data-ttu-id="08a18-138">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-138">See Also</span></span>

- <span data-ttu-id="08a18-139">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-139">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-140">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-140">fx_directory_create</span></span>
- <span data-ttu-id="08a18-141">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-141">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-142">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-142">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-143">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-143">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-144">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-144">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-145">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-145">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-146">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-146">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-147">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-147">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-148">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-148">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-149">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-149">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-150">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-150">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-151">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-151">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-152">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-152">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-153">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-153">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-154">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-154">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-155">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-155">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-156">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-156">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-157">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-157">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-158">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-158">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_attributes_set"></a><span data-ttu-id="08a18-159">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-159">fx_directory_attributes_set</span></span>

<span data-ttu-id="08a18-160">Imposta gli attributi della directory</span><span class="sxs-lookup"><span data-stu-id="08a18-160">Sets directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-161">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-161">Prototype</span></span>

```c
UINT fx_directory_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes);
```

### <a name="description"></a><span data-ttu-id="08a18-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-162">Description</span></span>

<span data-ttu-id="08a18-163">Questo servizio imposta gli attributi della directory su quelli specificati dal chiamante.</span><span class="sxs-lookup"><span data-stu-id="08a18-163">This service sets the directory's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-164">*Questa applicazione è autorizzata a modificare solo un subset degli attributi della directory con questo servizio. Qualsiasi tentativo di impostare attributi aggiuntivi provocherà un errore.*</span><span class="sxs-lookup"><span data-stu-id="08a18-164">*This application is only allowed to modify a subset of the directory's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-165">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-165">Input Parameters</span></span>

- <span data-ttu-id="08a18-166">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-166">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-167">**DIRECTORY_NAME**: puntatore al nome della directory richiesta (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-167">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="08a18-168">**Attributes**: nuovi attributi a questa directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-168">**attributes**: The new attributes to this directory.</span></span> <span data-ttu-id="08a18-169">Gli attributi di directory validi sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="08a18-169">The valid directory attributes are defined as follows:</span></span>
  - <span data-ttu-id="08a18-170">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-170">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="08a18-171">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-171">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="08a18-172">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="08a18-172">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="08a18-173">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="08a18-173">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-174">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-174">Return Values</span></span>

- <span data-ttu-id="08a18-175">Set di attributi di directory riusciti **FX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-175">**FX_SUCCESS** (0x00) Successful directory attribute set</span></span>
- <span data-ttu-id="08a18-176">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-176">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-177">La directory specificata **FX_NOT_FOUND** (0x04) non è stata trovata nel supporto</span><span class="sxs-lookup"><span data-stu-id="08a18-177">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="08a18-178">La voce **FX_NOT_DIRECTORY** (0x0E) non è una directory</span><span class="sxs-lookup"><span data-stu-id="08a18-178">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="08a18-179">Errore di I/O driver **FX_IO_ERROR** (0x90)</span><span class="sxs-lookup"><span data-stu-id="08a18-179">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="08a18-180">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura</span><span class="sxs-lookup"><span data-stu-id="08a18-180">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="08a18-181">Il file di **FX_FILE_CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-181">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-182">Settore **FX_SECTOR_INVALID** (0X89) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-182">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="08a18-183">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="08a18-183">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="08a18-184">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-184">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-185">Supporto di **FX_MEDIA_INVALID** (0x02) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-185">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="08a18-186">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="08a18-186">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="08a18-187">**FX_PTR_ERROR** (0x18) puntatore del supporto non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-187">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="08a18-188">**FX_INVALID_ATTR** (0x19) attributi non validi selezionati.</span><span class="sxs-lookup"><span data-stu-id="08a18-188">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="08a18-189">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-190">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-190">Allowed From</span></span>

<span data-ttu-id="08a18-191">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-192">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-192">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
status = fx_directory_attributes_set(&my_media, "mydir", FX_READ_ONLY);
/*Set the attributes of "mydir" to read-only. */
/* If status equals FX_SUCCESS, the directory "mydir" is read-only. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-193">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-193">See Also</span></span>

- <span data-ttu-id="08a18-194">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-194">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-195">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-195">fx_directory_create</span></span>
- <span data-ttu-id="08a18-196">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-196">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-197">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-197">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-198">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-198">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-199">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-199">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-200">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-200">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-201">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-201">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-202">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-202">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-203">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-203">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-204">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-204">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-205">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-205">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-206">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-206">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-207">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-207">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-208">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-208">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-209">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-209">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-210">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-210">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-211">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-211">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-212">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-212">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-213">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-213">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_create"></a><span data-ttu-id="08a18-214">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-214">fx_directory_create</span></span>

<span data-ttu-id="08a18-215">Crea una sottodirectory</span><span class="sxs-lookup"><span data-stu-id="08a18-215">Creates subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-216">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-216">Prototype</span></span>

```c
UINT fx_directory_create(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```
### <a name="description"></a><span data-ttu-id="08a18-217">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-217">Description</span></span>

<span data-ttu-id="08a18-218">Questo servizio crea una sottodirectory nella directory predefinita corrente o nel percorso specificato nel nome della directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-218">This service creates a subdirectory in the current default directory or in the path supplied in the directory name.</span></span> <span data-ttu-id="08a18-219">Diversamente dalla directory radice, le sottodirectory non hanno un limite al numero di file che possono contenere.</span><span class="sxs-lookup"><span data-stu-id="08a18-219">Unlike the root directory, subdirectories do not have a limit on the number of files they can hold.</span></span> <span data-ttu-id="08a18-220">La directory radice può solo tenere il numero di voci determinate dal record di avvio.</span><span class="sxs-lookup"><span data-stu-id="08a18-220">The root directory can only hold the number of entries determined by the boot record.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-221">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-221">Input Parameters</span></span>

- <span data-ttu-id="08a18-222">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-222">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-223">**DIRECTORY_NAME**: puntatore al nome della directory da creare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-223">**directory_name**: Pointer to the name of the directory to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-224">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-224">Return Values</span></span>

- <span data-ttu-id="08a18-225">Creazione Directory riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-225">**FX_SUCCESS** (0x00) Successful directory create.</span></span>
- <span data-ttu-id="08a18-226">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-226">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-227">La directory specificata **FX_NOT_FOUND** (0x04) non è stata trovata nel supporto</span><span class="sxs-lookup"><span data-stu-id="08a18-227">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="08a18-228">La voce **FX_NOT_DIRECTORY** (0x0E) non è una directory</span><span class="sxs-lookup"><span data-stu-id="08a18-228">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="08a18-229">Errore di I/O driver **FX_IO_ERROR** (0x90)</span><span class="sxs-lookup"><span data-stu-id="08a18-229">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="08a18-230">Il file di **FX_FILE _CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-230">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-231">Settore **FX_SECTOR_INVALID** (0X89) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-231">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="08a18-232">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="08a18-232">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="08a18-233">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-233">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-234">Supporto di **FX_MEDIA_INVALID** (0x02) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-234">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="08a18-235">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="08a18-235">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="08a18-236">**FX_PTR_ERROR** (0x18) puntatore del supporto non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-236">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="08a18-237">**FX_INVALID_ATTR** (0x19) attributi non validi selezionati.</span><span class="sxs-lookup"><span data-stu-id="08a18-237">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="08a18-238">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-238">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-239">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-239">Allowed From</span></span>

<span data-ttu-id="08a18-240">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-240">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-241">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-241">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Create a subdirectory called "temp" in the current default directory. */

status = fx_directory_create(&my_media, "temp");

/* If status equals FX_SUCCESS, the new subdirectory "temp" has been created. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-242">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-242">See Also</span></span>

- <span data-ttu-id="08a18-243">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-243">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-244">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-244">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-245">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-245">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-246">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-246">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-247">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-247">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-248">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-248">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-249">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-249">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-250">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-250">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-251">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-251">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-252">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-252">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-253">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-253">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-254">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-254">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-255">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-255">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-256">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-256">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-257">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-257">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-258">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-258">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-259">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-259">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-260">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-260">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-261">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-261">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-262">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-262">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_get"></a><span data-ttu-id="08a18-263">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-263">fx_directory_default_get</span></span>

<span data-ttu-id="08a18-264">Ottiene l'ultima directory predefinita</span><span class="sxs-lookup"><span data-stu-id="08a18-264">Gets last default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-265">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-265">Prototype</span></span>

```c
UINT fx_directory_default_get(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="08a18-266">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-266">Description</span></span>

<span data-ttu-id="08a18-267">Questo servizio restituisce il puntatore al percorso impostato per ultimo dal ***fx_directory_default_set***.</span><span class="sxs-lookup"><span data-stu-id="08a18-267">This service returns the pointer to the path last set by ***fx_directory_default_set***.</span></span> <span data-ttu-id="08a18-268">Se la directory predefinita non è stata impostata o se la directory predefinita corrente è la directory radice, viene restituito il valore FX_NULL.</span><span class="sxs-lookup"><span data-stu-id="08a18-268">If the default directory has not been set or if the current default directory is the root directory, a value of FX_NULL is returned.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-269">*Le dimensioni predefinite della stringa di percorso interna sono di 256 caratteri; può essere modificato modificando **FX_MAXIMUM_PATH** in **fx_api. h** e ricompilando l'intera libreria FILEX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene utilizzato internamente da FileX.*</span><span class="sxs-lookup"><span data-stu-id="08a18-269">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-270">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-270">Input Parameters</span></span>

- <span data-ttu-id="08a18-271">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-271">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-272">**return_path_name**: puntatore alla destinazione per l'ultima stringa di directory predefinita.</span><span class="sxs-lookup"><span data-stu-id="08a18-272">**return_path_name**: Pointer to the destination for the last default directory string.</span></span> <span data-ttu-id="08a18-273">Se l'impostazione corrente della directory predefinita è la radice, viene restituito il valore FX_NULL.</span><span class="sxs-lookup"><span data-stu-id="08a18-273">A value of FX_NULL is returned if the current setting of the default directory is the root.</span></span> <span data-ttu-id="08a18-274">Quando il supporto viene aperto, root è il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="08a18-274">When the media is opened, root is the default.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-275">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-275">Return Values</span></span>

- <span data-ttu-id="08a18-276">**FX_SUCCESS** (0x00) operazione predefinita per la directory Get</span><span class="sxs-lookup"><span data-stu-id="08a18-276">**FX_SUCCESS** (0x00) Successful default directory get</span></span>
- <span data-ttu-id="08a18-277">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-278">**FX_PTR_ERROR** (0x18) supporto o puntatore di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-278">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="08a18-279">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-279">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-280">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-280">Allowed From</span></span>

<span data-ttu-id="08a18-281">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-281">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-282">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-282">Example</span></span>

```c
FX_MEDIA my_media;
CHAR *current_default_dir;
UINT status;
/* Retrieve the current default directory. */
status = fx_directory_default_get(&my_media, &current_default_dir);
/* If status equals FX_SUCCESS, "current_default_dir" 
    contains a pointer to the current default directory).*/
```

### <a name="see-also"></a><span data-ttu-id="08a18-283">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-283">See Also</span></span>

- <span data-ttu-id="08a18-284">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-284">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-285">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-285">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-286">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-286">fx_directory_create</span></span>
- <span data-ttu-id="08a18-287">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-287">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-288">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-288">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-289">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-289">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-290">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-290">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-291">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-291">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-292">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-292">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-293">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-293">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-294">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-294">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-295">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-295">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-296">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-296">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-297">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-297">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-298">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-298">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-299">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-299">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-300">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-300">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-301">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-301">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-302">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-302">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-303">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-303">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_set"></a><span data-ttu-id="08a18-304">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-304">fx_directory_default_set</span></span>

<span data-ttu-id="08a18-305">Imposta la directory predefinita</span><span class="sxs-lookup"><span data-stu-id="08a18-305">Sets default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-306">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-306">Prototype</span></span>

```c

UINT fx_directory_default_set(
    FX_MEDIA *media_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="08a18-307">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-307">Description</span></span>

<span data-ttu-id="08a18-308">Questo servizio imposta la directory predefinita del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-308">This service sets the default directory of the media.</span></span> <span data-ttu-id="08a18-309">Se viene specificato un valore di FX_NULL, la directory predefinita viene impostata sulla directory radice del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-309">If a value of FX_NULL is supplied, the default directory is set to the media's root directory.</span></span> <span data-ttu-id="08a18-310">Tutte le operazioni di file successive che non specificano in modo esplicito un percorso utilizzeranno per impostazione predefinita questa directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-310">All subsequent file operations that do not explicitly specify a path will default to this directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-311">*Le dimensioni predefinite della stringa di percorso interna sono di 256 caratteri; può essere modificato modificando **FX_MAXIMUM_PATH** in **fx_api. h** e ricompilando l'intera libreria FILEX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene utilizzato internamente da FileX.*</span><span class="sxs-lookup"><span data-stu-id="08a18-311">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-312">*Per i nomi forniti dall'applicazione, FileX supporta sia la barra rovesciata ( \\ ) che la barra (/) per separare directory, sottodirectory e nomi file. Tuttavia, FileX usa solo il carattere barra rovesciata nei percorsi restituiti all'applicazione.*</span><span class="sxs-lookup"><span data-stu-id="08a18-312">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-313">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-313">Input Parameters</span></span>

- <span data-ttu-id="08a18-314">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-314">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-315">**new_path_name**: puntatore al nuovo nome di directory predefinito.</span><span class="sxs-lookup"><span data-stu-id="08a18-315">**new_path_name**: Pointer to new default directory name.</span></span> <span data-ttu-id="08a18-316">Se viene specificato un valore di FX_NULL, la directory predefinita del supporto viene impostata sulla directory radice del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-316">If a value of FX_NULL is supplied, the default directory of the media is set to the media's root directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-317">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-317">Return Values</span></span>

- <span data-ttu-id="08a18-318">Set di directory predefinito **FX_SUCCESS** (0x00) completato</span><span class="sxs-lookup"><span data-stu-id="08a18-318">**FX_SUCCESS** (0x00)  Successful default directory set</span></span>
- <span data-ttu-id="08a18-319">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-319">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-320">Impossibile trovare la nuova directory **FX_INVALID_PATH** (0x0D)</span><span class="sxs-lookup"><span data-stu-id="08a18-320">**FX_INVALID_PATH** (0x0D) New directory could not be found</span></span>
- <span data-ttu-id="08a18-321">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-321">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-322">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-322">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-323">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-323">Allowed From</span></span>

<span data-ttu-id="08a18-324">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-324">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-325">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-325">Example</span></span>

```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_default_set(&my_media, "\\abc\\def\\ghi");
/* If status equals FX_SUCCESS, the default directory for this media is \abc\def\ghi. All subsequent file operations that do not explicitly specify a path will default to this directory. Note that the character "\" serves as an escape character in a string. To represent the character "\", use the construct "\\". This is done because of the C language- only one "\" is really present in the string. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-326">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-326">See Also</span></span>

- <span data-ttu-id="08a18-327">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-327">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-328">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-328">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-329">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-329">fx_directory_create</span></span>
- <span data-ttu-id="08a18-330">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-330">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-331">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-331">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-332">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-332">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-333">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-333">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-334">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-334">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-335">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-335">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-336">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-336">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-337">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-337">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-338">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-338">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-339">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-339">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-340">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-340">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-341">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-341">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-342">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-342">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-343">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-343">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-344">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-344">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-345">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-345">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-346">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-346">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_delete"></a><span data-ttu-id="08a18-347">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-347">fx_directory_delete</span></span>

<span data-ttu-id="08a18-348">Elimina la sottodirectory</span><span class="sxs-lookup"><span data-stu-id="08a18-348">Deletes subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-349">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-349">Prototype</span></span>

```c
UINT fx_directory_delete(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="08a18-350">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-350">Description</span></span>

<span data-ttu-id="08a18-351">Questo servizio Elimina la directory specificata.</span><span class="sxs-lookup"><span data-stu-id="08a18-351">This service deletes the specified directory.</span></span> <span data-ttu-id="08a18-352">Si noti che la directory deve essere vuota per eliminarla.</span><span class="sxs-lookup"><span data-stu-id="08a18-352">Note that the directory must be empty to delete it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-353">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-353">Input Parameters</span></span>

- <span data-ttu-id="08a18-354">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-354">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-355">**DIRECTORY_NAME**: puntatore al nome della directory da eliminare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-355">**directory_name**: Pointer to name of directory to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-356">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-356">Return Values</span></span>

- <span data-ttu-id="08a18-357">Eliminazione directory riuscita **FX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-357">**FX_SUCCESS** (0x00) Successful directory delete</span></span>
- <span data-ttu-id="08a18-358">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-358">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-359">Impossibile trovare la directory specificata **FX_NOT_FOUND** (0x04)</span><span class="sxs-lookup"><span data-stu-id="08a18-359">**FX_NOT_FOUND** (0x04) Specified directory was not found</span></span>
- <span data-ttu-id="08a18-360">La directory specificata **FX_DIR_NOT_EMPTY** (0x10) non è vuota</span><span class="sxs-lookup"><span data-stu-id="08a18-360">**FX_DIR_NOT_EMPTY** (0x10) Specified directory is not empty</span></span>
- <span data-ttu-id="08a18-361">Errore di I/O driver **FX_IO_ERROR** (0x90)</span><span class="sxs-lookup"><span data-stu-id="08a18-361">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="08a18-362">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura</span><span class="sxs-lookup"><span data-stu-id="08a18-362">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="08a18-363">Il file di **FX_FILE_CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-363">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-364">Settore **FX_SECTOR_INVALID** (0X89) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-364">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="08a18-365">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="08a18-365">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="08a18-366">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-366">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-367">Supporto di **FX_MEDIA_INVALID** (0x02) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-367">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="08a18-368">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="08a18-368">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="08a18-369">**FX_NOT_DIRECTORY** (0X0E) non è una voce di directory</span><span class="sxs-lookup"><span data-stu-id="08a18-369">**FX_NOT_DIRECTORY** (0x0E) Not a directory entry</span></span>
- <span data-ttu-id="08a18-370">**FX_PTR_ERROR** (0x18) puntatore del supporto non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-370">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="08a18-371">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-371">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-372">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-372">Allowed From</span></span>

<span data-ttu-id="08a18-373">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-373">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-374">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-374">Example</span></span>
```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_delete(&my_media, "abc");
/* Delete the subdirectory "abc." */
/* If status equals FX_SUCCESS, the subdirectory "abc" was deleted. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-375">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-375">See Also</span></span>

- <span data-ttu-id="08a18-376">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-376">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-377">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-377">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-378">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-378">fx_directory_create</span></span>
- <span data-ttu-id="08a18-379">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-379">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-380">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-380">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-381">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-381">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-382">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-382">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-383">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-383">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-384">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-384">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-385">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-385">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-386">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-386">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-387">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-387">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-388">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-388">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-389">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-389">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-390">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-390">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-391">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-391">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-392">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-392">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-393">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-393">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-394">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-394">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-395">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-395">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_entry_find"></a><span data-ttu-id="08a18-396">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-396">fx_directory_first_entry_find</span></span>

<span data-ttu-id="08a18-397">Ottiene la prima voce di directory</span><span class="sxs-lookup"><span data-stu-id="08a18-397">Gets first directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-398">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-398">Prototype</span></span>

```c
UINT fx_directory_first_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="08a18-399">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-399">Description</span></span>

<span data-ttu-id="08a18-400">Questo servizio recupera il nome della prima voce nella directory predefinita e lo copia nella destinazione specificata.</span><span class="sxs-lookup"><span data-stu-id="08a18-400">This service retrieves the first entry name in the default directory and copies it to the specified destination.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-401">*La destinazione specificata deve essere sufficientemente grande da contenere il nome FileX di dimensioni massime, come definito da **FX_MAX_LONG_NAME_LEN.***</span><span class="sxs-lookup"><span data-stu-id="08a18-401">*The specified destination must be large enough to hold the maximum sized FileX name, as defined by **FX_MAX_LONG_NAME_LEN.***</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-402">*Se si usa un percorso non locale, è importante prevenire (con un semaforo ThreadX, un mutex o una modifica del livello di priorità) che altri thread dell'applicazione modifichino questa directory durante l'attraversamento di una directory. In caso contrario, è possibile ottenere risultati non validi.*</span><span class="sxs-lookup"><span data-stu-id="08a18-402">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-403">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-403">Input Parameters</span></span>

- <span data-ttu-id="08a18-404">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-404">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-405">**return_entry_name**: puntatore alla destinazione per il primo nome di voce nella directory predefinita.</span><span class="sxs-lookup"><span data-stu-id="08a18-405">**return_entry_name**: Pointer to destination for the first entry name in the default directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-406">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-406">Return Values</span></span>

- <span data-ttu-id="08a18-407">Ricerca nella prima voce di directory riuscita **FX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-407">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="08a18-408">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-408">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-409">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="08a18-409">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="08a18-410">Errore di I/O driver **FX_IO_ERROR** (0x90)</span><span class="sxs-lookup"><span data-stu-id="08a18-410">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="08a18-411">Il file di **FX_FILE_CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-411">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-412">Settore **FX_SECTOR_INVALID** (0X89) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-412">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="08a18-413">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="08a18-413">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="08a18-414">**FX_PTR_ERROR** (0x18) supporto o puntatore di destinazione non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-414">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer</span></span>
- <span data-ttu-id="08a18-415">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread</span><span class="sxs-lookup"><span data-stu-id="08a18-415">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-416">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-416">Allowed From</span></span>

<span data-ttu-id="08a18-417">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-417">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-418">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-418">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;
CHAR             entry[FX_MAX_LONG_NAME_LEN];
/* Retrieve the first directory entry in the current directory. */
status = fx_directory_first_entry_find(&my_media, entry);
/* If status equals FX_SUCCESS, the entry in the directory is the "entry" string. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-419">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-419">See Also</span></span>

- <span data-ttu-id="08a18-420">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-420">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-421">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-421">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-422">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-422">fx_directory_create</span></span>
- <span data-ttu-id="08a18-423">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-423">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-424">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-424">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-425">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-425">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-426">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-426">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-427">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-427">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-428">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-428">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-429">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-429">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-430">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-430">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-431">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-431">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-432">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-432">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-433">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-433">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-434">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-434">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-435">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-435">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-436">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-436">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-437">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-437">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-438">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-438">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-439">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-439">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_full_entry_find"></a><span data-ttu-id="08a18-440">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-440">fx_directory_first_full_entry_find</span></span>

<span data-ttu-id="08a18-441">Ottiene la prima voce di directory con informazioni complete</span><span class="sxs-lookup"><span data-stu-id="08a18-441">Gets first directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-442">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-442">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="08a18-443">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-443">Input Parameters</span></span>

- <span data-ttu-id="08a18-444">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-444">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-445">**DIRECTORY_NAME**: puntatore alla destinazione per il nome di una voce di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-445">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="08a18-446">Deve avere una dimensione minima di FX_MAX_LONG_NAME_LEN.</span><span class="sxs-lookup"><span data-stu-id="08a18-446">Must be at least as big as FX_MAX_LONG_NAME_LEN.</span></span>
- <span data-ttu-id="08a18-447">**attributi**: se non null, puntatore alla destinazione per gli attributi della voce da inserire.</span><span class="sxs-lookup"><span data-stu-id="08a18-447">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.</span></span> <span data-ttu-id="08a18-448">Gli attributi vengono restituiti in un formato mappa di bit con le seguenti impostazioni possibili:</span><span class="sxs-lookup"><span data-stu-id="08a18-448">The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="08a18-449">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-449">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="08a18-450">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-450">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="08a18-451">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="08a18-451">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="08a18-452">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="08a18-452">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="08a18-453">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="08a18-453">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="08a18-454">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="08a18-454">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="08a18-455">**size**: se non null, puntatore alla destinazione per la dimensione della voce in byte.</span><span class="sxs-lookup"><span data-stu-id="08a18-455">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="08a18-456">**year**: se non null, puntatore alla destinazione per l'anno di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-456">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="08a18-457">**Month**: se non null, puntatore alla destinazione per il mese di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-457">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="08a18-458">**Day**: se non null, puntatore alla destinazione per il giorno di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-458">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="08a18-459">**hour**: se non null, puntatore alla destinazione per l'ora di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-459">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="08a18-460">**minute**: se non null, puntatore alla destinazione per il minuto di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-460">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="08a18-461">**secondo**: se non null, puntatore alla destinazione per la seconda modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-461">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-462">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-462">Return Values</span></span>

- <span data-ttu-id="08a18-463">Ricerca nella prima voce di directory riuscita **FX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-463">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="08a18-464">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-464">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-465">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="08a18-465">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="08a18-466">Errore di I/O driver **FX_IO_ERROR** (0x90)</span><span class="sxs-lookup"><span data-stu-id="08a18-466">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="08a18-467">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura</span><span class="sxs-lookup"><span data-stu-id="08a18-467">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="08a18-468">Il file di **FX_FILE _CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-468">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-469">Settore **FX_SECTOR_INVALID** (0X89) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-469">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="08a18-470">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="08a18-470">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="08a18-471">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-471">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-472">Supporto di **FX_MEDIA_INVALID** (0x02) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-472">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="08a18-473">**FX_PTR_ERROR** (0x18) supporto o puntatore di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-473">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="08a18-474">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-474">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-475">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-475">Allowed From</span></span>

<span data-ttu-id="08a18-476">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-476">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-477">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-477">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-478">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-478">See Also</span></span>

- <span data-ttu-id="08a18-479">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-479">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-480">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-480">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-481">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-481">fx_directory_create</span></span>
- <span data-ttu-id="08a18-482">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-482">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-483">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-483">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-484">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-484">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-485">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-485">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-486">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-486">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-487">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-487">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-488">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-488">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-489">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-489">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-490">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-490">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-491">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-491">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-492">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-492">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-493">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-493">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-494">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-494">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-495">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-495">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-496">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-496">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-497">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-497">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-498">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-498">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_information_get"></a><span data-ttu-id="08a18-499">fx_directory_information_get:</span><span class="sxs-lookup"><span data-stu-id="08a18-499">fx_directory_information_get:</span></span>

<span data-ttu-id="08a18-500">Ottiene informazioni sulla voce di directory</span><span class="sxs-lookup"><span data-stu-id="08a18-500">Gets directory entry information</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-501">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-501">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="08a18-502">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-502">Input Parameters</span></span>

- <span data-ttu-id="08a18-503">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-503">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-504">**DIRECTORY_NAME**: puntatore al nome della voce di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-504">**directory_name**: Pointer to name of the directory entry.</span></span>
- <span data-ttu-id="08a18-505">**Attributes**: puntatore alla destinazione per gli attributi.</span><span class="sxs-lookup"><span data-stu-id="08a18-505">**attributes**: Pointer to the destination for the attributes.</span></span>
- <span data-ttu-id="08a18-506">**size**: puntatore alla destinazione per la dimensione.</span><span class="sxs-lookup"><span data-stu-id="08a18-506">**size**: Pointer to the destination for the size.</span></span>
- <span data-ttu-id="08a18-507">**year**: puntatore alla destinazione per l'anno.</span><span class="sxs-lookup"><span data-stu-id="08a18-507">**year**: Pointer to the destination for the year.</span></span>
- <span data-ttu-id="08a18-508">**Month**: puntatore alla destinazione per il mese.</span><span class="sxs-lookup"><span data-stu-id="08a18-508">**month**: Pointer to the destination for the month.</span></span>
- <span data-ttu-id="08a18-509">**Day**: puntatore alla destinazione per la giornata.</span><span class="sxs-lookup"><span data-stu-id="08a18-509">**day**: Pointer to the destination for the day.</span></span>
- <span data-ttu-id="08a18-510">**hour**: puntatore alla destinazione per l'ora.</span><span class="sxs-lookup"><span data-stu-id="08a18-510">**hour**: Pointer to the destination for the hour.</span></span>
- <span data-ttu-id="08a18-511">**minute**: puntatore alla destinazione per i minuti.</span><span class="sxs-lookup"><span data-stu-id="08a18-511">**minute**: Pointer to the destination for the minute.</span></span>
- <span data-ttu-id="08a18-512">**secondo**: puntatore alla destinazione per il secondo.</span><span class="sxs-lookup"><span data-stu-id="08a18-512">**second**: Pointer to the destination for the second.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-513">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-513">Return Values</span></span>

- <span data-ttu-id="08a18-514">Ricerca nella prima voce di directory riuscita **FX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-514">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="08a18-515">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-515">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-516">La directory specificata **FX_NOT_FOUND** (0x04) non è stata trovata nel supporto</span><span class="sxs-lookup"><span data-stu-id="08a18-516">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="08a18-517">Errore di I/O driver **FX_IO_ERROR** (0x90)</span><span class="sxs-lookup"><span data-stu-id="08a18-517">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="08a18-518">Supporto di **FX_MEDIA_INVALID** (0x02) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-518">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="08a18-519">Il file di **FX_FILE _CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-519">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-520">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="08a18-520">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="08a18-521">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-521">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-522">Settore **FX_SECTOR_INVALID** (0X89) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-522">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="08a18-523">**FX_PTR_ERROR** (0x18) supporto o puntatore di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-523">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="08a18-524">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-524">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-525">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-525">Allowed From</span></span>

<span data-ttu-id="08a18-526">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-526">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-527">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-527">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-528">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-528">See Also</span></span>

- <span data-ttu-id="08a18-529">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-529">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-530">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-530">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-531">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-531">fx_directory_create</span></span>
- <span data-ttu-id="08a18-532">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-532">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-533">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-533">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-534">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-534">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-535">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-535">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-536">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-536">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-537">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-537">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-538">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-538">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-539">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-539">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-540">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-540">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-541">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-541">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-542">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-542">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-543">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-543">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-544">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-544">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-545">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-545">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-546">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-546">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-547">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-547">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-548">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-548">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_clear"></a><span data-ttu-id="08a18-549">fx_directory_local_path_clear:</span><span class="sxs-lookup"><span data-stu-id="08a18-549">fx_directory_local_path_clear:</span></span>

<span data-ttu-id="08a18-550">Cancella il percorso locale predefinito</span><span class="sxs-lookup"><span data-stu-id="08a18-550">Clears default local path</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-551">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-551">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="08a18-552">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-552">Description</span></span>

<span data-ttu-id="08a18-553">Questo servizio Cancella il percorso locale precedente impostato per il thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="08a18-553">This service clears the previous local path set up for the calling thread.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-554">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-554">Input Parameters</span></span>

- <span data-ttu-id="08a18-555">**media_ptr**: puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-555">**media_ptr**: Pointer to a previously opened media.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-556">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-556">Return Values</span></span>

- <span data-ttu-id="08a18-557">Il percorso locale riuscito **FX_SUCCESS** (0x00) è stato cancellato.</span><span class="sxs-lookup"><span data-stu-id="08a18-557">**FX_SUCCESS** (0x00) Successful local path clear.</span></span>
- <span data-ttu-id="08a18-558">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è attualmente aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-558">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="08a18-559">È stato definito **FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="08a18-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined</span></span>
- <span data-ttu-id="08a18-560">**FX_PTR_ERROR** (0x18) puntatore del supporto non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-560">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-561">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-561">Allowed From</span></span>

<span data-ttu-id="08a18-562">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-562">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-563">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-563">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Clear the previously setup local path for this media. */
status = fx_directory_local_path_clear(&my_media);
/* If status equals FX_SUCCESS the local path is cleared. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-564">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-564">See Also</span></span>

- <span data-ttu-id="08a18-565">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-565">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-566">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-566">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-567">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-567">fx_directory_create</span></span>
- <span data-ttu-id="08a18-568">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-568">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-569">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-569">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-570">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-570">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-571">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-571">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-572">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-572">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-573">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-573">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-574">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-574">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-575">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-575">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-576">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-576">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-577">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-577">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-578">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-578">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-579">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-579">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-580">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-580">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-581">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-581">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-582">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-582">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-583">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-583">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-584">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-584">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_get"></a><span data-ttu-id="08a18-585">fx_directory_local_path_get:</span><span class="sxs-lookup"><span data-stu-id="08a18-585">fx_directory_local_path_get:</span></span>

<span data-ttu-id="08a18-586">Ottiene la stringa di percorso locale corrente</span><span class="sxs-lookup"><span data-stu-id="08a18-586">Gets the current local path string</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-587">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-587">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="08a18-588">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-588">Description</span></span>

<span data-ttu-id="08a18-589">Questo servizio restituisce il puntatore del percorso locale del supporto specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-589">This service returns the local path pointer of the specified media.</span></span> <span data-ttu-id="08a18-590">Se non è impostato alcun percorso locale, al chiamante viene restituito un valore NULL.</span><span class="sxs-lookup"><span data-stu-id="08a18-590">If there is no local path set, a NULL is returned to the caller.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-591">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-591">Input Parameters</span></span>

- <span data-ttu-id="08a18-592">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-592">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-593">**return_path_name**: puntatore al puntatore della stringa di destinazione per la stringa di percorso locale da archiviare.</span><span class="sxs-lookup"><span data-stu-id="08a18-593">**return_path_name**: Pointer to the destination string pointer for the local path string to be stored.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-594">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-594">Return Values</span></span>

- <span data-ttu-id="08a18-595">**FX_SUCCESS** (0x00) percorso locale riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="08a18-595">**FX_SUCCESS** (0x00) Successful local path get.</span></span>
- <span data-ttu-id="08a18-596">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è attualmente aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-596">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="08a18-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="08a18-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="08a18-598">**FX_PTR_ERROR** (0x18) puntatore del supporto non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-598">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>


### <a name="allowed-from"></a><span data-ttu-id="08a18-599">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-599">Allowed From</span></span>

<span data-ttu-id="08a18-600">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-600">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-601">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-601">Example</span></span>

```c
FX_MEDIA         my_media;
CHAR             *my_path;
UINT             status;
/* Retrieve the current local path string. */
status = fx_directory_local_path_get(&my_media, &my_path);
/* If status equals FX_SUCCESS, "my_path" points to the local path string. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-602">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-602">See Also</span></span>

- <span data-ttu-id="08a18-603">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-603">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-604">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-604">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-605">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-605">fx_directory_create</span></span>
- <span data-ttu-id="08a18-606">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-606">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-607">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-607">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-608">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-608">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-609">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-609">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-610">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-610">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-611">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-611">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-612">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-612">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-613">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-613">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-614">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-614">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-615">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-615">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-616">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-616">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-617">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-617">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-618">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-618">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-619">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-619">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-620">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-620">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-621">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-621">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-622">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-622">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_restore"></a><span data-ttu-id="08a18-623">fx_directory_local_path_restore:</span><span class="sxs-lookup"><span data-stu-id="08a18-623">fx_directory_local_path_restore:</span></span>

<span data-ttu-id="08a18-624">Ripristina il percorso locale precedente</span><span class="sxs-lookup"><span data-stu-id="08a18-624">Restores previous local path</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-625">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-625">Prototype</span></span>

```c
UINT fx_directory_local_path_restore(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr);
```

### <a name="description"></a><span data-ttu-id="08a18-626">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-626">Description</span></span>

<span data-ttu-id="08a18-627">Questo servizio ripristina un percorso locale impostato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-627">This service restores a previously set local path.</span></span> <span data-ttu-id="08a18-628">Viene ripristinata anche la posizione di ricerca della directory eseguita su questo percorso locale, che rende questa routine utile negli attraversamenti ricorsivi delle directory da parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-628">The directory search position made on this local path is also restored, which makes this routine useful in recursive directory traversals by the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-629">*Ogni percorso locale contiene una stringa di percorso locale di dimensioni **FX_MAXIMUM_PATH** , che per impostazione predefinita è di 256 caratteri. Questa stringa di percorso interna non viene utilizzata da FileX e viene fornita solo per l'utilizzo dell'applicazione. Se **FX_LOCAL_PATH** viene dichiarata come variabile locale, gli utenti devono prestare attenzione alla crescita dello stack in base alle dimensioni della struttura. Gli utenti sono invitati a ridurre le dimensioni del **FX_MAXIMUM_PATH** e a ricompilare l'origine della libreria FILEX.*</span><span class="sxs-lookup"><span data-stu-id="08a18-629">*Each local path contains a local path string of **FX_MAXIMUM_PATH** in size, which by default is 256 characters. This internal path string is not used by FileX and is provided only for the application's use. If **FX_LOCAL_PATH** is going to be declared as a local variable, users should beware of the stack growing by the size of this structure. Users are welcome to reduce the size of **FX_MAXIMUM_PATH** and rebuild the FileX library source.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-630">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-630">Input Parameters</span></span>

- <span data-ttu-id="08a18-631">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-631">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-632">**local_path_ptr**: puntatore al percorso locale impostato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-632">**local_path_ptr**: Pointer to the previously set local path.</span></span> <span data-ttu-id="08a18-633">È molto importante assicurarsi che questo puntatore faccia effettivamente riferimento a un oggetto utilizzato in precedenza e che ancora il percorso locale sia intatto.</span><span class="sxs-lookup"><span data-stu-id="08a18-633">It's very important to ensure that this pointer does indeed point to a previously used and still intact local path.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-634">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-634">Return Values</span></span>

- <span data-ttu-id="08a18-635">**FX_SUCCESS** (0x00) il ripristino del percorso locale è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-635">**FX_SUCCESS** (0x00) Successful local path restore.</span></span>
- <span data-ttu-id="08a18-636">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-636">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open.</span></span>
- <span data-ttu-id="08a18-637">È stato definito **FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH.</span><span class="sxs-lookup"><span data-stu-id="08a18-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined.</span></span>
- <span data-ttu-id="08a18-638">Il puntatore del percorso locale o del supporto **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-638">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-639">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-639">Allowed From</span></span>

<span data-ttu-id="08a18-640">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-640">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-641">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-641">Example</span></span>

```c
FX_MEDIA                  my_media;
FX_LOCAL_PATH             my_previous_local_path;
UINT                      status;
/* Restore the previous local path. */
status = fx_directory_local_path_restore(&my_media, &my_previous_local_path);
/* If status equals FX_SUCCESS, the previous local path has been restored. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-642">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-642">See Also</span></span>

- <span data-ttu-id="08a18-643">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-643">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-644">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-644">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-645">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-645">fx_directory_create</span></span>
- <span data-ttu-id="08a18-646">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-646">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-647">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-647">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-648">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-648">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-649">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-649">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-650">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-650">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-651">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-651">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-652">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-652">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-653">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-653">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-654">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-654">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-655">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-655">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-656">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-656">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-657">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-657">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-658">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-658">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-659">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-659">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-660">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-660">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-661">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-661">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-662">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-662">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_set"></a><span data-ttu-id="08a18-663">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-663">fx_directory_local_path_set</span></span>

<span data-ttu-id="08a18-664">Imposta un percorso locale specifico del thread</span><span class="sxs-lookup"><span data-stu-id="08a18-664">Sets up a thread-specific local path</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-665">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-665">Prototype</span></span>

```c
UINT fx_directory_local_path_set(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="08a18-666">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-666">Description</span></span>

<span data-ttu-id="08a18-667">Questo servizio imposta un percorso specifico del thread come specificato dal \***new_path_string** _.</span><span class="sxs-lookup"><span data-stu-id="08a18-667">This service sets up a thread-specific path as specified by the \***new_path_string** _.</span></span> <span data-ttu-id="08a18-668">Al termine di questa routine, le informazioni sul percorso locale archiviate in _ *_local_path_ptr_*\* avranno la precedenza sul percorso multimediale globale per tutte le operazioni di file e directory eseguite dal thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-668">After successful completion of this routine, the local path information stored in _ *_local_path_ptr_*\* will take precedence over the global media path for all file and directory operations made by this thread.</span></span> <span data-ttu-id="08a18-669">Questa operazione non avrà alcun effetto su nessun altro thread del sistema</span><span class="sxs-lookup"><span data-stu-id="08a18-669">This will have no impact on any other thread in the system</span></span> 
> [!IMPORTANT]
> <span data-ttu-id="08a18-670">*Le dimensioni predefinite della stringa di percorso locale sono di 256 caratteri; può essere modificato modificando **FX_MAXIMUM_PATH** in **fx_api. h** e ricompilando l'intera libreria FILEX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene utilizzato internamente da FileX.*</span><span class="sxs-lookup"><span data-stu-id="08a18-670">*The default size of the local path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-671">*Per i nomi forniti dall'applicazione, FileX supporta sia la barra rovesciata ( \\ ) che la barra (/) per separare directory, sottodirectory e nomi file. Tuttavia, FileX usa solo il carattere barra rovesciata nei percorsi restituiti all'applicazione.*</span><span class="sxs-lookup"><span data-stu-id="08a18-671">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-672">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-672">Input Parameters</span></span>

- <span data-ttu-id="08a18-673">**media_ptr**: puntatore al supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-673">**media_ptr**: Pointer to the previously opened media.</span></span>
- <span data-ttu-id="08a18-674">**local_path_ptr**: destinazione per contenere le informazioni sul percorso locale specifiche del thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-674">**local_path_ptr**: Destination for holding the thread-specific local path information.</span></span> <span data-ttu-id="08a18-675">È possibile specificare l'indirizzo di questa struttura per la funzione di ripristino del percorso locale in futuro.</span><span class="sxs-lookup"><span data-stu-id="08a18-675">The address of this structure may be supplied to the local path restore function in the future.</span></span>
- <span data-ttu-id="08a18-676">**new_path_name**: specifica il percorso locale del programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-676">**new_path_name**: Specifies the local path to setup.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-677">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-677">Return Values</span></span>

- <span data-ttu-id="08a18-678">Il set di directory predefinito **FX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-678">**FX_SUCCESS** (0x00) Successful default directory set.</span></span>
- <span data-ttu-id="08a18-679">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-679">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-680">**FX_NOT_IMPLEMENTED** (0x22) \* \* FX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="08a18-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="08a18-681">Impossibile trovare la nuova directory **FX_INVALID_PATH** (0x0D).</span><span class="sxs-lookup"><span data-stu-id="08a18-681">**FX_INVALID_PATH** (0x0D) New directory could not be found.</span></span>
- <span data-ttu-id="08a18-682">**FX_NOT_IMPLEMENTED** (0x22)-\* \* FX_NO_LOCAL_PATH è definito.</span><span class="sxs-lookup"><span data-stu-id="08a18-682">**FX_NOT_IMPLEMENTED** (0x22)- \*\*FX_NO_LOCAL_PATH is defined.</span></span>
- <span data-ttu-id="08a18-683">Il puntatore del percorso locale o del supporto **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-683">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-684">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-684">Allowed From</span></span>

<span data-ttu-id="08a18-685">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-685">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-686">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-686">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-687">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-687">See Also</span></span>

- <span data-ttu-id="08a18-688">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-688">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-689">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-689">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-690">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-690">fx_directory_create</span></span>
- <span data-ttu-id="08a18-691">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-691">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-692">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-692">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-693">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-693">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-694">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-694">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-695">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-695">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-696">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-696">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-697">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-697">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-698">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-698">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-699">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-699">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-700">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-700">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-701">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-701">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-702">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-702">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-703">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-703">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-704">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-704">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-705">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-705">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-706">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-706">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-707">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-707">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get"></a><span data-ttu-id="08a18-708">fx_directory_long_name_get:</span><span class="sxs-lookup"><span data-stu-id="08a18-708">fx_directory_long_name_get:</span></span>

<span data-ttu-id="08a18-709">Ottiene il nome lungo dal nome breve</span><span class="sxs-lookup"><span data-stu-id="08a18-709">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-710">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-710">Prototype</span></span>

```c
UINT fx_directory_long_name_get(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name);
```

### <a name="description"></a><span data-ttu-id="08a18-711">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-711">Description</span></span>

<span data-ttu-id="08a18-712">Questo servizio recupera il nome lungo (se presente) associato al nome breve fornito (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-712">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="08a18-713">Il nome breve può essere un nome file o un nome di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-713">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-714">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-714">Input Parameters</span></span>

- <span data-ttu-id="08a18-715">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-715">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-716">**short_name**: puntatore a nome breve origine (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-716">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="08a18-717">**long_name**: puntatore alla destinazione per il nome lungo.</span><span class="sxs-lookup"><span data-stu-id="08a18-717">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="08a18-718">Se non è presente un nome lungo, viene restituito il nome breve.</span><span class="sxs-lookup"><span data-stu-id="08a18-718">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="08a18-719">Si noti che la destinazione per il nome lungo deve essere sufficientemente grande da contenere FX_MAX_LONG_NAME_LEN caratteri.</span><span class="sxs-lookup"><span data-stu-id="08a18-719">Note that the destination for the long name must be large enough to hold FX_MAX_LONG_NAME_LEN characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-720">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-720">Return Values</span></span>

- <span data-ttu-id="08a18-721">Ottenere il nome lungo di **FX_SUCCESS** (0x00) con esito positivo</span><span class="sxs-lookup"><span data-stu-id="08a18-721">**FX_SUCCESS** (0x00) Successful long name get</span></span>
- <span data-ttu-id="08a18-722">Nome breve **FX_NOT_FOUND** (0x04) non trovato</span><span class="sxs-lookup"><span data-stu-id="08a18-722">**FX_NOT_FOUND** (0x04) Short name was not found</span></span>
- <span data-ttu-id="08a18-723">Errore di I/O driver **FX_IO_ERROR** (0x90)</span><span class="sxs-lookup"><span data-stu-id="08a18-723">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="08a18-724">Supporto di **FX_MEDIA_INVALID** (0x02) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-724">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="08a18-725">Il file di **FX_FILE_CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-725">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-726">Settore **FX_SECTOR_INVALID** (0X89) non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-726">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="08a18-727">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="08a18-727">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="08a18-728">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-728">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-729">**FX_PTR_ERROR** (0x18) supporto o puntatore al nome non valido</span><span class="sxs-lookup"><span data-stu-id="08a18-729">**FX_PTR_ERROR** (0x18) Invalid media or name pointer</span></span>
- <span data-ttu-id="08a18-730">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread</span><span class="sxs-lookup"><span data-stu-id="08a18-730">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-731">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-731">Allowed From</span></span>

<span data-ttu-id="08a18-732">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-732">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-733">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-733">Example</span></span>

```c
FX_MEDIA            my_media;
UCHAR               my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */
status = fx_directory_long_name_get(&my_media, "TEXT~01.TXT", my_long_name);
/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-734">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-734">See Also</span></span>

- <span data-ttu-id="08a18-735">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-735">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-736">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-736">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-737">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-737">fx_directory_create</span></span>
- <span data-ttu-id="08a18-738">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-738">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-739">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-739">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-740">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-740">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-741">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-741">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-742">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-742">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-743">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-743">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-744">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-744">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-745">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-745">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-746">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-746">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-747">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-747">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-748">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-748">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-749">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-749">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-750">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-750">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-751">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-751">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-752">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-752">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-753">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-753">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-754">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-754">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get_extended"></a><span data-ttu-id="08a18-755">fx_directory_long_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="08a18-755">fx_directory_long_name_get_extended</span></span>

<span data-ttu-id="08a18-756">Ottiene il nome lungo dal nome breve</span><span class="sxs-lookup"><span data-stu-id="08a18-756">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-757">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-757">Prototype</span></span>

```c
UINT fx_directory_long_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name,
    UINT long_file_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="08a18-758">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-758">Description</span></span>

<span data-ttu-id="08a18-759">Questo servizio recupera il nome lungo (se presente) associato al nome breve fornito (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-759">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="08a18-760">Il nome breve può essere un nome file o un nome di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-760">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-761">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-761">Input Parameters</span></span>

- <span data-ttu-id="08a18-762">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-762">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-763">**short_name**: puntatore a nome breve origine (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-763">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="08a18-764">**long_name**: puntatore alla destinazione per il nome lungo.</span><span class="sxs-lookup"><span data-stu-id="08a18-764">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="08a18-765">Se non è presente un nome lungo, viene restituito il nome breve.</span><span class="sxs-lookup"><span data-stu-id="08a18-765">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="08a18-766">Nota: la destinazione per il nome lungo deve essere sufficientemente grande da contenere **FX_MAX_LONG_NAME_LEN** caratteri.</span><span class="sxs-lookup"><span data-stu-id="08a18-766">Note: Destination for the long name must be large enough to hold **FX_MAX_LONG_NAME_LEN** characters.</span></span>
- <span data-ttu-id="08a18-767">**long_file_name_buffer_length**: lunghezza del buffer del nome lungo.</span><span class="sxs-lookup"><span data-stu-id="08a18-767">**long_file_name_buffer_length**: Length of the long name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-768">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-768">Return Values</span></span>

- <span data-ttu-id="08a18-769">**FX_SUCCESS** (0x00) nome lungo riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="08a18-769">**FX_SUCCESS** (0x00) Successful long name get.</span></span>
- <span data-ttu-id="08a18-770">Nome breve **FX_NOT_FOUND** (0x04) non trovato.</span><span class="sxs-lookup"><span data-stu-id="08a18-770">**FX_NOT_FOUND** (0x04) Short name was not found.</span></span>
- <span data-ttu-id="08a18-771">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-771">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-772">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-772">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-773">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-773">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-774">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-774">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-775">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-775">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-776">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-776">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="08a18-777">**FX_PTR_ERROR** (0x18) supporto o puntatore al nome non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-777">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="08a18-778">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-778">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-779">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-779">Allowed From</span></span>

<span data-ttu-id="08a18-780">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-780">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-781">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-781">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */

status = fx_directory_long_name_get_extended(&my_media,
    "TEXT~01.TXT", my_long_name), sizeof(my_long_name));

/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-782">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-782">See Also</span></span>

- <span data-ttu-id="08a18-783">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-783">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-784">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-784">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-785">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-785">fx_directory_create</span></span>
- <span data-ttu-id="08a18-786">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-786">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-787">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-787">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-788">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-788">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-789">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-789">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-790">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-790">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-791">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-791">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-792">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-792">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-793">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-793">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-794">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-794">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-795">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-795">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-796">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-796">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-797">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-797">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-798">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-798">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-799">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-799">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-800">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-800">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-801">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-801">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-802">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-802">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_name_test"></a><span data-ttu-id="08a18-803">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-803">fx_directory_name_test</span></span>

<span data-ttu-id="08a18-804">Test per la directory</span><span class="sxs-lookup"><span data-stu-id="08a18-804">Tests for directory</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-805">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-805">Prototype</span></span>

```c
UINT fx_directory_name_test(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="08a18-806">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-806">Description</span></span>

<span data-ttu-id="08a18-807">Questo servizio verifica se il nome fornito è o meno una directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-807">This service tests whether or not the supplied name is a directory.</span></span> <span data-ttu-id="08a18-808">In tal caso, viene restituito un FX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="08a18-808">If so, a FX_SUCCESS is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-809">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-809">Input Parameters</span></span>

- <span data-ttu-id="08a18-810">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-810">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-811">**DIRECTORY_NAME**: puntatore al nome della voce di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-811">**directory_name**: Pointer to name of the directory entry.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-812">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-812">Return Values</span></span>

- <span data-ttu-id="08a18-813">Il nome fornito **FX_SUCCESS** (0x00) è una directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-813">**FX_SUCCESS** (0x00) Supplied name is a directory.</span></span>
- <span data-ttu-id="08a18-814">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto</span><span class="sxs-lookup"><span data-stu-id="08a18-814">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="08a18-815">Impossibile trovare la voce della directory **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-815">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="08a18-816">La voce **FX_NOT_DIRECTORY** (0x0E) non è una directory</span><span class="sxs-lookup"><span data-stu-id="08a18-816">**FX_NOT_DIRECTORY** (0x0E)  Entry is not a directory</span></span>
- <span data-ttu-id="08a18-817">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-817">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-818">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-818">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-819">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-819">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-820">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-820">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-821">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-821">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-822">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-822">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="08a18-823">**FX_PTR_ERROR** (0x18) supporto o puntatore al nome non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-823">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="08a18-824">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-824">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-825">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-825">Allowed From</span></span>

<span data-ttu-id="08a18-826">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-826">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-827">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-827">Example</span></span>

```c
FX_MEDIA        my_media;
UNIT             status;
/* Check to see if the name "abc" is directory */

status = fx_directory_name_test(&my_media, "abc");

/* If status equals FX_SUCCESS "abc" is a directory. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-828">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-828">See Also</span></span>

- <span data-ttu-id="08a18-829">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-829">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-830">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-830">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-831">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-831">fx_directory_create</span></span>
- <span data-ttu-id="08a18-832">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-832">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-833">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-833">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-834">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-834">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-835">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-835">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-836">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-836">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-837">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-837">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-838">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-838">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-839">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-839">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-840">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-840">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-841">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-841">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-842">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-842">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-843">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-843">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-844">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-844">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-845">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-845">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-846">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-846">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-847">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-847">fx_unicode_directory_create</span></span>

## <a name="fx_directory_next_entry_find"></a><span data-ttu-id="08a18-848">fx_directory_next_entry_find:</span><span class="sxs-lookup"><span data-stu-id="08a18-848">fx_directory_next_entry_find:</span></span>

<span data-ttu-id="08a18-849">Preleva la voce della directory successiva</span><span class="sxs-lookup"><span data-stu-id="08a18-849">Picks up next directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-850">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-850">Prototype</span></span>

```c
UINT fx_directory_next_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="08a18-851">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-851">Description</span></span>

<span data-ttu-id="08a18-852">Questo servizio restituisce il nome della voce successiva nella directory predefinita corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-852">This service returns the next entry name in the current default directory.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-853">*Se si usa un percorso non locale, è anche importante prevenire (con un semaforo ThreadX o un livello di priorità dei thread) che altri thread dell'applicazione modifichino questa directory durante l'attraversamento di una directory. In caso contrario, è possibile ottenere risultati non validi.*</span><span class="sxs-lookup"><span data-stu-id="08a18-853">*If using a non-local path, it is also important to prevent (with a ThreadX semaphore or thread priority level) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-854">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-854">Input Parameters</span></span>

- <span data-ttu-id="08a18-855">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-855">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-856">**return_entry_name**: puntatore alla destinazione per il nome della voce successiva nella directory predefinita.</span><span class="sxs-lookup"><span data-stu-id="08a18-856">**return_entry_name**: Pointer to destination for the next entry name in the default directory.</span></span> <span data-ttu-id="08a18-857">Il buffer a cui punta il puntatore deve essere sufficientemente grande da contenere la dimensione massima del nome FileX, definito da **_FX_MAX_LONG_NAME_LEN_**.</span><span class="sxs-lookup"><span data-stu-id="08a18-857">The buffer this pointer points to must be large enough to hold the maximum size of FileX name, defined by **_FX_MAX_LONG_NAME_LEN_**.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-858">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-858">Return Values</span></span>

- <span data-ttu-id="08a18-859">Ricerca voce successiva riuscita **FX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-859">**FX_SUCCESS** (0x00) Successful next entry find</span></span>
- <span data-ttu-id="08a18-860">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-860">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-861">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci in questa directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-861">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="08a18-862">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-862">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-863">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-863">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-864">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-864">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-865">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-865">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-866">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-866">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-867">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-867">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-868">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-868">**FX_CALLER_ERROR** (0x20)     Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-869">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-869">Allowed From</span></span>

<span data-ttu-id="08a18-870">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-871">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-871">Example</span></span>

```c
FX_MEDIA        my_media;
CHAR            next_name[FX_MAX_LONG_NAME_LEN];
UINT            status;

/* Retrieve the next entry in the default directory. */

status = fx_directory_next_entry_find(&my_media, next_name);

/* If status equals TX_SUCCESS, the name of the next directory entry is in "next_name". */
```

### <a name="see-also"></a><span data-ttu-id="08a18-872">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-872">See Also</span></span>

- <span data-ttu-id="08a18-873">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-873">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-874">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-874">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-875">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-875">fx_directory_create</span></span>
- <span data-ttu-id="08a18-876">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-876">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-877">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-877">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-878">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-878">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-879">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-879">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-880">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-880">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-881">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-881">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-882">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-882">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-883">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-883">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-884">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-884">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-885">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-885">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-886">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-886">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-887">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-887">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-888">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-888">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-889">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-889">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-890">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-890">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-891">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-891">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-892">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-892">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_next_full_entry_find"></a><span data-ttu-id="08a18-893">fx_directory_next_full_entry_find:</span><span class="sxs-lookup"><span data-stu-id="08a18-893">fx_directory_next_full_entry_find:</span></span>

<span data-ttu-id="08a18-894">Ottiene la voce della directory successiva con informazioni complete</span><span class="sxs-lookup"><span data-stu-id="08a18-894">Gets next directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-895">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-895">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="08a18-896">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-896">Description</span></span>

<span data-ttu-id="08a18-897">Questo servizio recupera il nome della voce successiva nella directory predefinita e lo copia nella destinazione specificata.</span><span class="sxs-lookup"><span data-stu-id="08a18-897">This service retrieves the next entry name in the default directory and copies it to the specified destination.</span></span> <span data-ttu-id="08a18-898">Restituisce inoltre informazioni complete sulla voce, come specificato dai parametri di input aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="08a18-898">It also returns full information about the entry as specified by the additional input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-899">\* La destinazione specificata deve essere sufficientemente grande da contenere il nome FileX di dimensioni massime, come definito da \* \* \* FX_MAX_LONG_NAME_LEN \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="08a18-899">\*The specified destination must be large enough to hold the maximum sized FileX name, as defined by \*\*\*FX_MAX_LONG_NAME_LEN\*\*\*\*</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-900">*Se si usa un percorso non locale, è importante prevenire (con un semaforo ThreadX, un mutex o una modifica del livello di priorità) che altri thread dell'applicazione modifichino questa directory durante l'attraversamento di una directory. In caso contrario, è possibile ottenere risultati non validi.*</span><span class="sxs-lookup"><span data-stu-id="08a18-900">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-901">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-901">Input Parameters</span></span>

- <span data-ttu-id="08a18-902">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-902">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-903">**DIRECTORY_NAME**: puntatore alla destinazione per il nome di una voce di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-903">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="08a18-904">Deve avere una dimensione minima di **FX_MAX_LONG_NAME_LEN**.</span><span class="sxs-lookup"><span data-stu-id="08a18-904">Must be at least as big as **FX_MAX_LONG_NAME_LEN**.</span></span>
- <span data-ttu-id="08a18-905">**attributi**: se non null, puntatore alla destinazione per gli attributi della voce da inserire. Gli attributi vengono restituiti in un formato mappa di bit con le seguenti impostazioni possibili:</span><span class="sxs-lookup"><span data-stu-id="08a18-905">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="08a18-906">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-906">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="08a18-907">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-907">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="08a18-908">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="08a18-908">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="08a18-909">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="08a18-909">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="08a18-910">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="08a18-910">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="08a18-911">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="08a18-911">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="08a18-912">**size**: se non null, puntatore alla destinazione per la dimensione della voce in byte.</span><span class="sxs-lookup"><span data-stu-id="08a18-912">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="08a18-913">**Month**: se non null, puntatore alla destinazione per il mese di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-913">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="08a18-914">**year**: se non null, puntatore alla destinazione per l'anno di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-914">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="08a18-915">**Day**: se non null, puntatore alla destinazione per il giorno di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-915">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="08a18-916">**hour**: se non null, puntatore alla destinazione per l'ora di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-916">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="08a18-917">**minute**: se non null, puntatore alla destinazione per il minuto di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-917">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="08a18-918">**secondo**: se non null, puntatore alla destinazione per la seconda modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="08a18-918">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-919">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-919">Return Values</span></span>

- <span data-ttu-id="08a18-920">**FX_SUCCESS** (0x00) la voce successiva della directory è stata trovata.</span><span class="sxs-lookup"><span data-stu-id="08a18-920">**FX_SUCCESS** (0x00) Successful directory next entry find.</span></span>
- <span data-ttu-id="08a18-921">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-921">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-922">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci in questa directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-922">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="08a18-923">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-923">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-924">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-924">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-925">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-925">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-926">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-926">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-927">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-927">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="08a18-928">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-928">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-929">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido o tutti i parametri di input sono null.</span><span class="sxs-lookup"><span data-stu-id="08a18-929">**FX_PTR_ERROR** (0x18) Invalid media pointer or all input parameters are NULL.</span></span>
- <span data-ttu-id="08a18-930">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-930">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-931">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-931">Allowed From</span></span>

<span data-ttu-id="08a18-932">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-932">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-933">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-933">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-934">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-934">See Also</span></span>

- <span data-ttu-id="08a18-935">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-935">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-936">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-936">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-937">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-937">fx_directory_create</span></span>
- <span data-ttu-id="08a18-938">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-938">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-939">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-939">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-940">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-940">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-941">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-941">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-942">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-942">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-943">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-943">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-944">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-944">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-945">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-945">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-946">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-946">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-947">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-947">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-948">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-948">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-949">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-949">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-950">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-950">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-951">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-951">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-952">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-952">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-953">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-953">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-954">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-954">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_rename"></a><span data-ttu-id="08a18-955">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-955">fx_directory_rename</span></span>

<span data-ttu-id="08a18-956">Rinomina la directory</span><span class="sxs-lookup"><span data-stu-id="08a18-956">Renames directory</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-957">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-957">Prototype</span></span>

```c
UINT fx_directory_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_directory_name,
    CHAR *new_directory_name);
```

### <a name="description"></a><span data-ttu-id="08a18-958">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-958">Description</span></span>

<span data-ttu-id="08a18-959">Questo servizio modifica il nome della directory con il nome della nuova directory specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-959">This service changes the directory name to the specified new directory name.</span></span> <span data-ttu-id="08a18-960">La ridenominazione viene eseguita anche in relazione al percorso specificato o al percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="08a18-960">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="08a18-961">Se nel nuovo nome della directory viene specificato un percorso, la directory rinominata viene spostata in modo efficace nel percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-961">If a path is specified in the new directory name, the renamed directory is effectively moved to the specified path.</span></span> <span data-ttu-id="08a18-962">Se non viene specificato alcun percorso, la directory rinominata viene inserita nel percorso predefinito corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-962">If no path is specified, the renamed directory is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-963">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-963">Input Parameters</span></span>

- <span data-ttu-id="08a18-964">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-964">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-965">**old_directory_name**: puntatore al nome di directory corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-965">**old_directory_name**: Pointer to current directory name.</span></span>
- <span data-ttu-id="08a18-966">**new_directory_name**: puntatore al nuovo nome della directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-966">**new_directory_name**: Pointer to new directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-967">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-967">Return Values</span></span>

- <span data-ttu-id="08a18-968">**FX_SUCCESS** (0x00) la ridenominazione della directory è riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-968">**FX_SUCCESS** (0x00) Successful directory rename.</span></span>
- <span data-ttu-id="08a18-969">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-969">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-970">Impossibile trovare la voce della directory **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-970">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="08a18-971">La voce **FX_NOT_DIRECTORY** (0x0E) non è una directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-971">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory.</span></span>
- <span data-ttu-id="08a18-972">Il nome della nuova directory **FX_INVALID_NAME** (0x0C) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-972">**FX_INVALID_NAME** (0x0C) New directory name is invalid.</span></span>
- <span data-ttu-id="08a18-973">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-973">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-974">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-974">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-975">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-975">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-976">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-976">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-977">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-977">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-978">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-978">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="08a18-979">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-979">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-980">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci in questa directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-980">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="08a18-981">**FX_INVALID_PATH** (0x0D) percorso non valido fornito con il nome della directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-981">**FX_INVALID_PATH** (0x0D) Invalid path supplied with directory name.</span></span>
- <span data-ttu-id="08a18-982">La directory specificata **FX_ALREADY_CREATED** (0x0B) è già stata creata.</span><span class="sxs-lookup"><span data-stu-id="08a18-982">**FX_ALREADY_CREATED** (0x0B) Specified directory was already created.</span></span>
- <span data-ttu-id="08a18-983">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-983">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-984">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-984">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-985">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-985">Allowed From</span></span>

<span data-ttu-id="08a18-986">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-986">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-987">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-987">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Change the directory "abc" to "def". */
status = fx_directory_rename(&my_media, "abc", "def");

/* If status equals FX_SUCCESS, the directory was changed to "def". */
```

### <a name="see-also"></a><span data-ttu-id="08a18-988">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-988">See Also</span></span>

- <span data-ttu-id="08a18-989">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-989">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-990">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-990">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-991">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-991">fx_directory_create</span></span>
- <span data-ttu-id="08a18-992">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-992">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-993">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-993">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-994">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-994">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-995">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-995">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-996">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-996">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-997">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-997">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-998">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-998">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-999">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-999">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-1000">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-1000">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-1001">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1001">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-1002">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1002">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-1003">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-1003">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-1004">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1004">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-1005">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1005">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-1006">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1006">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-1007">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1007">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-1008">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1008">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get"></a><span data-ttu-id="08a18-1009">fx_directory_short_name_get:</span><span class="sxs-lookup"><span data-stu-id="08a18-1009">fx_directory_short_name_get:</span></span>

<span data-ttu-id="08a18-1010">Ottiene il nome breve da un nome lungo</span><span class="sxs-lookup"><span data-stu-id="08a18-1010">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1011">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1011">Prototype</span></span>

```c
UINT fx_directory_short_name_get(
    FX_MEDIA *media_ptr,
    CHAR *long_name, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="08a18-1012">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1012">Description</span></span>

<span data-ttu-id="08a18-1013">Questo servizio recupera il nome breve (formato 8,3) associato al nome lungo fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-1013">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="08a18-1014">Il nome lungo può essere un nome file o un nome di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-1014">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1015">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1015">Input Parameters</span></span>

- <span data-ttu-id="08a18-1016">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1016">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-1017">**long_name**: puntatore al nome lungo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="08a18-1017">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="08a18-1018">**short_name**: puntatore al nome breve della destinazione (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-1018">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="08a18-1019">Si noti che la destinazione per il nome breve deve essere sufficientemente grande da contenere 14 caratteri.</span><span class="sxs-lookup"><span data-stu-id="08a18-1019">Note that the destination for the short name must be large enough to hold 14 characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1020">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1020">Return Values</span></span>

- <span data-ttu-id="08a18-1021">**FX_SUCCESS** (0x00) nome breve riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="08a18-1021">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="08a18-1022">Impossibile trovare il nome lungo **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-1022">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="08a18-1023">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1023">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1024">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1024">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1025">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1025">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1026">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1026">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1027">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1027">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1028">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1028">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1029">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-1029">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-1030">**FX_PTR_ERROR** (0x18) supporto o puntatore al nome non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1030">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="08a18-1031">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1031">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1032">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1032">Allowed From</span></span>

<span data-ttu-id="08a18-1033">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1033">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1034">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1034">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get(&my_media,
    "my_really_long_name", my_short_name);

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1035">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1035">See Also</span></span>

- <span data-ttu-id="08a18-1036">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1036">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-1037">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1037">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-1038">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1038">fx_directory_create</span></span>
- <span data-ttu-id="08a18-1039">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1039">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-1040">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1040">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-1041">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1041">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-1042">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1042">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-1043">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1043">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-1044">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1044">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-1045">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-1045">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-1046">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1046">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-1047">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-1047">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-1048">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1048">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-1049">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1049">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-1050">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-1050">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-1051">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1051">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-1052">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1052">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-1053">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1053">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-1054">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1054">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-1055">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1055">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get_extended"></a><span data-ttu-id="08a18-1056">fx_directory_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="08a18-1056">fx_directory_short_name_get_extended</span></span>

<span data-ttu-id="08a18-1057">Ottiene il nome breve da un nome lungo</span><span class="sxs-lookup"><span data-stu-id="08a18-1057">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1058">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1058">Prototype</span></span>

```csharp
UINT fx_directory_short_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *long_name,
    CHAR *short_name,
    UINT short_file_name_length);
```

### <a name="description"></a><span data-ttu-id="08a18-1059">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1059">Description</span></span>

<span data-ttu-id="08a18-1060">Questo servizio recupera il nome breve (formato 8,3) associato al nome lungo fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-1060">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="08a18-1061">Il nome lungo può essere un nome file o un nome di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-1061">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1062">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1062">Input Parameters</span></span>

- <span data-ttu-id="08a18-1063">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1063">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-1064">**long_name**: puntatore al nome lungo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="08a18-1064">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="08a18-1065">**short_name**: puntatore al nome breve della destinazione (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-1065">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="08a18-1066">Nota: la destinazione per il nome breve deve essere sufficientemente grande da contenere 14 caratteri.</span><span class="sxs-lookup"><span data-stu-id="08a18-1066">Note: Destination for the short name must be large enough to hold 14 characters.</span></span>
- <span data-ttu-id="08a18-1067">**short_file_name_length**: lunghezza del buffer dei nomi brevi.</span><span class="sxs-lookup"><span data-stu-id="08a18-1067">**short_file_name_length**: Length of short name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1068">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1068">Return Values</span></span>

- <span data-ttu-id="08a18-1069">**FX_SUCCESS** (0x00) nome breve riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="08a18-1069">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="08a18-1070">Impossibile trovare il nome lungo **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-1070">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="08a18-1071">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1071">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1072">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1072">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1073">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1074">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1075">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1075">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1076">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1076">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1077">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-1077">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-1078">**FX_PTR_ERROR** (0x18) supporto o puntatore al nome non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1078">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="08a18-1079">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1079">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1080">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1080">Allowed From</span></span>

<span data-ttu-id="08a18-1081">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1081">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1082">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1082">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get_extended(&my_media,
    "my_really_long_name", my_short_name, sizeof(my_short_name));

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1083">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1083">See Also</span></span>

- <span data-ttu-id="08a18-1084">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1084">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-1085">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1085">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-1086">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1086">fx_directory_create</span></span>
- <span data-ttu-id="08a18-1087">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1087">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-1088">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1088">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-1089">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1089">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-1090">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1090">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-1091">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1091">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-1092">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1092">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-1093">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-1093">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-1094">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1094">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-1095">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-1095">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-1096">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1096">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-1097">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1097">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-1098">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-1098">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-1099">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1099">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-1100">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-1100">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-1101">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1101">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-1102">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1102">fx_unicode_directory_create</span></span>
- <span data-ttu-id="08a18-1103">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1103">fx_unicode_directory_rename</span></span>

## <a name="fx_fault_tolerant_enable"></a><span data-ttu-id="08a18-1104">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-1104">fx_fault_tolerant_enable</span></span>

<span data-ttu-id="08a18-1105">Abilita il servizio a tolleranza di errore</span><span class="sxs-lookup"><span data-stu-id="08a18-1105">Enables the fault tolerant service</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1106">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1106">Prototype</span></span>

```csharp
UINT fx_fault_tolerant_enable(
    FX_MEDIA *media_ptr,
    VOID *memory_buffer,
    UINT memory_size);
```

### <a name="description"></a><span data-ttu-id="08a18-1107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1107">Description</span></span>

<span data-ttu-id="08a18-1108">Questo servizio Abilita il modulo a tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="08a18-1108">This service enables the fault tolerant module.</span></span> <span data-ttu-id="08a18-1109">All'avvio, il modulo a tolleranza di errore rileva se il file system è sotto la protezione a tolleranza di errore FileX.</span><span class="sxs-lookup"><span data-stu-id="08a18-1109">Upon starting, the fault tolerant module detects whether or not the file system is under FileX fault tolerant protection.</span></span> <span data-ttu-id="08a18-1110">In caso contrario, il servizio rileva i settori disponibili nell'file system per archiviare i log in file system transazioni.</span><span class="sxs-lookup"><span data-stu-id="08a18-1110">If it is not, the service finds available sectors on the file system to store logs on file system transactions.</span></span> <span data-ttu-id="08a18-1111">Se il file system si trova sotto la protezione a tolleranza di errore FileX, applica i log al file system per mantenerne l'integrità.</span><span class="sxs-lookup"><span data-stu-id="08a18-1111">If the file system is under FileX fault tolerant protection, it applies the logs to the file system to maintain its integrity.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1112">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1112">Input Parameters</span></span>

- <span data-ttu-id="08a18-1113">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1113">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-1114">**memory_ptr**: puntatore a un blocco di memoria utilizzato dal modulo a tolleranza di errore come memoria Scratch.</span><span class="sxs-lookup"><span data-stu-id="08a18-1114">**memory_ptr**: Pointer to a block of memory used by the fault tolerant module as scratch memory.</span></span>
- <span data-ttu-id="08a18-1115">**memory_size**: dimensione della memoria Scratch.</span><span class="sxs-lookup"><span data-stu-id="08a18-1115">**memory_size**: The size of the scratch memory.</span></span> <span data-ttu-id="08a18-1116">Per il corretto funzionamento della tolleranza di errore, le dimensioni della memoria dei file temporanei devono essere di almeno 3072 byte, e devono essere costituite da più dimensioni del settore.</span><span class="sxs-lookup"><span data-stu-id="08a18-1116">In order for fault tolerant to work properly, the scratch memory size shall be at least 3072 bytes,- and must be multiple of sector size.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1117">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1117">Return Values</span></span>

- <span data-ttu-id="08a18-1118">**FX_SUCCESS** (0x00) ha abilitato correttamente la tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="08a18-1118">**FX_SUCCESS** (0x00) Successfully enabled fault tolerant.</span></span>
- <span data-ttu-id="08a18-1119">Dimensioni della memoria **FX_NOT_ENOUGH_MEMORY** (0x91) troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="08a18-1119">**FX_NOT_ENOUGH_MEMORY** (0x91)    memory size too small.</span></span>
- <span data-ttu-id="08a18-1120">Errore del settore di avvio **FX_BOOT_ERROR** (0x01).</span><span class="sxs-lookup"><span data-stu-id="08a18-1120">**FX_BOOT_ERROR** (0x01) Boot sector error.</span></span>
- <span data-ttu-id="08a18-1121">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1121">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1122">**FX_NO_MORE_ENTRIES** (0X0F) non sono più disponibili cluster gratuiti.</span><span class="sxs-lookup"><span data-stu-id="08a18-1122">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="08a18-1123">Il supporto di **FX_NO_MORE_SPACE** (0x0A) associato a questo file non dispone di un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="08a18-1123">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="08a18-1124">Il settore **FX_SECTOR_INVALID** (0x89) non è valido</span><span class="sxs-lookup"><span data-stu-id="08a18-1124">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="08a18-1125">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1125">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1126">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1126">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-1127">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1127">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1128">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1128">Allowed From</span></span>

<span data-ttu-id="08a18-1129">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1129">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1130">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1130">Example</span></span>

```c

/* Declare memory space used for fault tolerant. */

ULONG fault tolerant_memory[3072 / sizeof(ULONG)];

/* Enable fault tolerant. */

fx_fault_tolerant_enable(media_ptr, fault_tolerant_memory, sizeof(fault_tolerant_memory));

```

### <a name="see-also"></a><span data-ttu-id="08a18-1131">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1131">See Also</span></span>

- <span data-ttu-id="08a18-1132">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-1132">fx_system_initialize</span></span>
- <span data-ttu-id="08a18-1133">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-1133">fx_media_abort</span></span>
- <span data-ttu-id="08a18-1134">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-1134">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-1135">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-1135">fx_media_check</span></span>
- <span data-ttu-id="08a18-1136">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1136">fx_media_close</span></span>
- <span data-ttu-id="08a18-1137">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1137">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-1138">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-1138">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-1139">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-1139">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-1140">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-1140">fx_media_flush</span></span>
- <span data-ttu-id="08a18-1141">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-1141">fx_media_format</span></span>
- <span data-ttu-id="08a18-1142">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1142">fx_media_open</span></span>
- <span data-ttu-id="08a18-1143">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1143">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-1144">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1144">fx_media_read</span></span>
- <span data-ttu-id="08a18-1145">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-1145">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-1146">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1146">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-1147">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1147">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-1148">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1148">fx_media_write</span></span>

## <a name="fx_file_allocate"></a><span data-ttu-id="08a18-1149">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1149">fx_file_allocate</span></span>

<span data-ttu-id="08a18-1150">Alloca spazio per un file</span><span class="sxs-lookup"><span data-stu-id="08a18-1150">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1151">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1151">Prototype</span></span>

```csharp
UINT fx_file_allocate(
    FX_FILE *file_ptr, 
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="08a18-1152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1152">Description</span></span>

<span data-ttu-id="08a18-1153">Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1153">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="08a18-1154">FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster.</span><span class="sxs-lookup"><span data-stu-id="08a18-1154">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="08a18-1155">Il risultato viene quindi arrotondato per eccesso al cluster intero successivo.</span><span class="sxs-lookup"><span data-stu-id="08a18-1155">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="08a18-1156">Per allocare spazio oltre i 4 GB, l'applicazione deve utilizzare il *fx_file_extended_allocate* del servizio.</span><span class="sxs-lookup"><span data-stu-id="08a18-1156">To allocate space beyond 4GB, application shall use the service *fx_file_extended_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1157">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1157">Input Parameters</span></span>

- <span data-ttu-id="08a18-1158">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-1158">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="08a18-1159">**dimensioni**: numero di byte da allocare per il file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1159">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1160">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1160">Return Values</span></span>

- <span data-ttu-id="08a18-1161">**FX_SUCCESS** (0x00) l'allocazione di file riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-1161">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="08a18-1162">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1162">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-1163">**FX_FAT_READ_ERROR** (0X03) non è riuscito a leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1163">**FX_FAT_READ_ERROR** (0x03) Failed to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1164">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1164">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1165">Il file specificato **FX_NOT_OPEN** (0x07) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1165">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="08a18-1166">**FX_NO_MORE_ENTRIES** (0X0F) non sono più disponibili cluster gratuiti.</span><span class="sxs-lookup"><span data-stu-id="08a18-1166">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="08a18-1167">Il supporto di **FX_NO_MORE_SPACE** (0x0A) associato a questo file non dispone di un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="08a18-1167">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="08a18-1168">Il settore **FX_SECTOR_INVALID** (0x89) non è valido</span><span class="sxs-lookup"><span data-stu-id="08a18-1168">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="08a18-1169">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1169">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1170">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1170">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1171">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1171">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-1172">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1172">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1173">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1173">Allowed From</span></span>

<span data-ttu-id="08a18-1174">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1174">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1175">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1175">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;

/* Allocate 1024 bytes to the end of my_file. */

status = fx_file_allocate(&my_file, 1024);

/* If status equals FX_SUCCESS the file now has one or more
    contiguous cluster(s) that can accommodate at least 1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1176">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1176">See Also</span></span>

- <span data-ttu-id="08a18-1177">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1177">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1178">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1178">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1179">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1179">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1180">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1180">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="08a18-1181">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1181">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1182">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1182">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1183">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1183">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1184">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1184">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1185">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1185">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1186">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1186">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1187">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1187">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1188">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1188">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1189">fx_file_open fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1189">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="08a18-1190">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1190">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1191">fx_file_rename fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1191">fx_file_rename- fx_file_seek</span></span>
- <span data-ttu-id="08a18-1192">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1192">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1193">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1193">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1194">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1194">fx_file_write</span></span>
- <span data-ttu-id="08a18-1195">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1195">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1196">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1196">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1197">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1197">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1198">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1198">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1199">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1199">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_read"></a><span data-ttu-id="08a18-1200">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1200">fx_file_attributes_read</span></span>

<span data-ttu-id="08a18-1201">Legge gli attributi del file</span><span class="sxs-lookup"><span data-stu-id="08a18-1201">Reads file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1202">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1202">Prototype</span></span>

```c
    UINT fx_file_attributes_read(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT *attributes_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-1203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1203">Description</span></span>

<span data-ttu-id="08a18-1204">Questo servizio legge gli attributi del file dal supporto specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1204">This service reads the file's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1205">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1205">Input Parameters</span></span>

- <span data-ttu-id="08a18-1206">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1206">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-1207">**file_name**: puntatore al nome del file richiesto (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1207">**file_name**: Pointer to the name of the requested file (directory path is optional).</span></span>
- <span data-ttu-id="08a18-1208">**attributes_ptr**: puntatore alla destinazione per gli attributi del file da inserire.</span><span class="sxs-lookup"><span data-stu-id="08a18-1208">**attributes_ptr**: Pointer to the destination for the file's attributes to be placed.</span></span> <span data-ttu-id="08a18-1209">Gli attributi di file vengono restituiti in un formato mappa di bit con le seguenti impostazioni possibili:</span><span class="sxs-lookup"><span data-stu-id="08a18-1209">The file attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="08a18-1210">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-1210">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="08a18-1211">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-1211">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="08a18-1212">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="08a18-1212">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="08a18-1213">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="08a18-1213">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="08a18-1214">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="08a18-1214">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="08a18-1215">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="08a18-1215">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1216">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1216">Return Values</span></span>

- <span data-ttu-id="08a18-1217">Lettura attributo riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-1217">**FX_SUCCESS** (0x00) Successful attribute read.</span></span>
- <span data-ttu-id="08a18-1218">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1218">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-1219">Il file specificato **FX_NOT_FOUND** (0x04) non è stato trovato nel supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1219">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="08a18-1220">**FX_NOT_A_FILE** file specificato (0x05) è una directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-1220">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="08a18-1221">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1221">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1222">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1222">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1223">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1223">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1224">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1224">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1225">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1225">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1226">**FX_PTR_ERROR** (0x18) il puntatore al supporto o agli attributi non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1226">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="08a18-1227">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1227">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1228">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1228">Allowed From</span></span>

<span data-ttu-id="08a18-1229">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1229">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1230">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1230">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;
UINT             attributes;

/* Retrieve the attributes of "myfile.txt" from the specified media. */

status = fx_file_attributes_read(&my_media, "myfile.txt", &attributes);

/* If status equals FX_SUCCESS, "attributes"
    contains the file attributes for "myfile.txt". */

```

### <a name="see-also"></a><span data-ttu-id="08a18-1231">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1231">See Also</span></span>

- <span data-ttu-id="08a18-1232">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1232">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1233">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1233">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1234">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1234">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1235">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1235">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="08a18-1236">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1236">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1237">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1237">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1238">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1238">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1239">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1239">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1240">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1240">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1241">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1241">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1242">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1242">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1243">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1243">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1244">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1244">fx_file_open</span></span>
- <span data-ttu-id="08a18-1245">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1245">fx_file_read</span></span>
- <span data-ttu-id="08a18-1246">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1246">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1247">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1247">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1248">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1248">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1249">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1249">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1250">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1250">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1251">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1251">fx_file_write</span></span>
- <span data-ttu-id="08a18-1252">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1252">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1253">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1253">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1254">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1254">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1255">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1255">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1256">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1256">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_set"></a><span data-ttu-id="08a18-1257">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1257">fx_file_attributes_set</span></span>

<span data-ttu-id="08a18-1258">Imposta gli attributi del file</span><span class="sxs-lookup"><span data-stu-id="08a18-1258">Sets file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1259">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1259">Prototype</span></span>

```c
UINT fx_file_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT attributes);
```
### <a name="description"></a><span data-ttu-id="08a18-1260">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1260">Description</span></span>

<span data-ttu-id="08a18-1261">Questo servizio imposta gli attributi del file su quelli specificati dal chiamante.</span><span class="sxs-lookup"><span data-stu-id="08a18-1261">This service sets the file's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-1262">*L'applicazione è autorizzata a modificare solo un subset degli attributi del file con questo servizio. Qualsiasi tentativo di impostare attributi aggiuntivi provocherà un errore.*</span><span class="sxs-lookup"><span data-stu-id="08a18-1262">*The application is only allowed to modify a subset of the file's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1263">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1263">Input Parameters</span></span>

- <span data-ttu-id="08a18-1264">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1264">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-1265">**file_name**: puntatore al nome del file richiesto \* \* (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1265">**file_name**: Pointer to the name of the requested file\*\* (directory path is optional).</span></span>
- <span data-ttu-id="08a18-1266">**Attributes**: nuovi attributi per il file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1266">**attributes**: The new attributes for the file.</span></span> <span data-ttu-id="08a18-1267">Gli attributi di file validi sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="08a18-1267">The valid file attributes are defined as follows:</span></span>
  - <span data-ttu-id="08a18-1268">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-1268">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="08a18-1269">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-1269">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="08a18-1270">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="08a18-1270">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="08a18-1271">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="08a18-1271">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1272">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1272">Return Values</span></span>

- <span data-ttu-id="08a18-1273">Set di attributi **FX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-1273">**FX_SUCCESS** (0x00) Successful attribute set.</span></span>
- <span data-ttu-id="08a18-1274">Il file **FX_ACCESS_ERROR** (0x06) è aperto e non è possibile impostarne gli attributi.</span><span class="sxs-lookup"><span data-stu-id="08a18-1274">**FX_ACCESS_ERROR** (0x06) File is open and cannot have its attributes set.</span></span>
- <span data-ttu-id="08a18-1275">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1275">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1276">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1276">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1277">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-1278">**FX_NO_MORE_ENTRIES** (0X0F) non sono presenti altre voci nella tabella FAT o nella mappa del cluster exFAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1278">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in the FAT table or exFAT cluster map.</span></span>
- <span data-ttu-id="08a18-1279">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-1279">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="08a18-1280">Il file specificato **FX_NOT_FOUND** (0x04) non è stato trovato nel supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1280">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="08a18-1281">**FX_NOT_A_FILE** file specificato (0x05) è una directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-1281">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="08a18-1282">Il settore **FX_SECTOR_INVALID** (0x89) non è valido</span><span class="sxs-lookup"><span data-stu-id="08a18-1282">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="08a18-1283">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1283">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1284">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1284">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1285">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-1285">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-1286">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1286">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-1287">**FX_INVALID_ATTR** (0x19) attributi non validi selezionati.</span><span class="sxs-lookup"><span data-stu-id="08a18-1287">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="08a18-1288">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1288">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1289">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1289">Allowed From</span></span>

<span data-ttu-id="08a18-1290">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1290">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1291">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1291">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Set the attributes of "myfile.txt" to read-only. */

status = fx_file_attributes_set(&my_media, "myfile.txt", FX_READ_ONLY);

/* If status equals FX_SUCCESS, the file is now read-only. */

```

### <a name="see-also"></a><span data-ttu-id="08a18-1292">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1292">See Also</span></span>

- <span data-ttu-id="08a18-1293">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1293">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1294">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1294">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1295">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1295">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1296">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1296">fx_file_close</span></span>
- <span data-ttu-id="08a18-1297">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1297">fx_file_create</span></span>
- <span data-ttu-id="08a18-1298">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1298">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1299">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1299">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1300">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1300">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1301">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1301">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1302">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1302">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1303">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1303">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1304">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1304">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1305">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1305">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1306">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1306">fx_file_open</span></span>
- <span data-ttu-id="08a18-1307">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1307">fx_file_read</span></span>
- <span data-ttu-id="08a18-1308">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1308">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1309">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1309">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1310">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1310">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1311">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1311">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1312">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1312">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1313">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1313">fx_file_write</span></span>
- <span data-ttu-id="08a18-1314">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1314">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1315">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1315">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1316">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1316">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1317">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1317">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1318">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1318">fx_unicode_short_name_get</span></span>

## <a name="fx_file_best_effort_allocate"></a><span data-ttu-id="08a18-1319">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1319">fx_file_best_effort_allocate</span></span>

<span data-ttu-id="08a18-1320">Massimo sforzo per allocare spazio per un file</span><span class="sxs-lookup"><span data-stu-id="08a18-1320">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1321">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1321">Prototype</span></span>

```c
UINT fx_file_best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG size,
    ULONG *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="08a18-1322">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1322">Description</span></span>

<span data-ttu-id="08a18-1323">Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1323">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="08a18-1324">FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster.</span><span class="sxs-lookup"><span data-stu-id="08a18-1324">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="08a18-1325">Il risultato viene quindi arrotondato per eccesso al cluster intero successivo.</span><span class="sxs-lookup"><span data-stu-id="08a18-1325">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="08a18-1326">Se nel supporto non sono disponibili cluster consecutivi sufficienti, questo servizio collega il più grande blocco disponibile di cluster consecutivi al file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1326">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="08a18-1327">La quantità di spazio effettivamente allocata al file viene restituita al chiamante.</span><span class="sxs-lookup"><span data-stu-id="08a18-1327">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="08a18-1328">Per allocare spazio oltre i 4 GB, l'applicazione deve utilizzare il *fx_file_extended_best_effort_allocate* del servizio.</span><span class="sxs-lookup"><span data-stu-id="08a18-1328">To allocate space beyond 4GB, application shall use the service *fx_file_extended_best_effort_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1329">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1329">Input Parameters</span></span>

- <span data-ttu-id="08a18-1330">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-1330">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="08a18-1331">**dimensioni**: numero di byte da allocare per il file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1331">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1332">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1332">Return Values</span></span>

- <span data-ttu-id="08a18-1333">**FX_SUCCESS** (0x00) l'allocazione di file con il migliore tentativo riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-1333">**FX_SUCCESS** (0x00) Successful best-effort file allocation.</span></span>
- <span data-ttu-id="08a18-1334">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1334">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-1335">Il file specificato **FX_NOT_OPEN** (0x07) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1335">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="08a18-1336">Il supporto di **FX_NO_MORE_SPACE** (0x0A) associato a questo file non dispone di un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="08a18-1336">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="08a18-1337">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1337">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1338">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1338">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1339">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1339">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1340">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1340">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1341">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1341">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1342">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1342">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1343">**FX_PTR_ERROR** (0x18) puntatore o destinazione del file non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1343">**FX_PTR_ERROR** (0x18) Invalid file pointer or destination.</span></span>
- <span data-ttu-id="08a18-1344">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1344">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1345">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1345">Allowed From</span></span>

<span data-ttu-id="08a18-1346">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1346">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1347">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1347">Example</span></span>

```c

FX_FILE         my_file;
UINT             status;
ULONG             actual_allocation;

/* Attempt to allocate 1024 bytes to the end of my_file. */

status = fx_file_best_effort_allocate(&my_file, 1024, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */

```

### <a name="see-also"></a><span data-ttu-id="08a18-1348">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1348">See Also</span></span>

- <span data-ttu-id="08a18-1349">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1349">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1350">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1350">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1351">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1351">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1352">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1352">fx_file_close</span></span>
- <span data-ttu-id="08a18-1353">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1353">fx_file_create</span></span>
- <span data-ttu-id="08a18-1354">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1354">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1355">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1355">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1356">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1356">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1357">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1357">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1358">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1358">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1359">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1359">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1360">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1360">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1361">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1361">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1362">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1362">fx_file_open</span></span>
- <span data-ttu-id="08a18-1363">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1363">fx_file_read</span></span>
- <span data-ttu-id="08a18-1364">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1364">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1365">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1365">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1366">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1366">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1367">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1367">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1368">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1368">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1369">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1369">fx_file_write</span></span>
- <span data-ttu-id="08a18-1370">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1370">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1371">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1371">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1372">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1372">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1373">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1373">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1374">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1374">fx_unicode_short_name_get</span></span>

## <a name="fx_file_close"></a><span data-ttu-id="08a18-1375">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1375">fx_file_close</span></span>

<span data-ttu-id="08a18-1376">Chiude il file</span><span class="sxs-lookup"><span data-stu-id="08a18-1376">Closes file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1377">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1377">Prototype</span></span>

```c
UINT fx_file_close(FX_FILE *file_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-1378">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1378">Description</span></span>

<span data-ttu-id="08a18-1379">Questo servizio chiude il file specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1379">This service closes the specified file.</span></span> <span data-ttu-id="08a18-1380">Se il file è stato aperto per la scrittura e se è stato modificato, il servizio completa il processo di modifica del file aggiornando la voce della directory con le nuove dimensioni e l'ora e la data di sistema correnti.</span><span class="sxs-lookup"><span data-stu-id="08a18-1380">If the file was open for writing and if it was modified, this service completes the file modification process by updating its directory entry with the new size and the current system time and date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1381">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1381">Input Parameters</span></span>

- <span data-ttu-id="08a18-1382">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-1382">**file_ptr**: Pointer to a previously opened file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1383">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1383">Return Values</span></span>

- <span data-ttu-id="08a18-1384">Chiusura del file **FX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="08a18-1384">**FX_SUCCESS** (0x00) Successful file close.</span></span>
- <span data-ttu-id="08a18-1385">Il file specificato **FX_NOT_OPEN** (0x07) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1385">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="08a18-1386">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1386">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1387">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1387">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1388">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1388">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1389">**FX_PTR_ERROR** (0x18) il puntatore al supporto o agli attributi non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1389">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="08a18-1390">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1390">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1391">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1391">Allowed From</span></span>

<span data-ttu-id="08a18-1392">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1392">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1393">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1393">Example</span></span>

```c

FX_FILE        my_file;
UINT        status;

/* Close the previously opened file "my_file". */
status = fx_file_close(&my_file);

/* If status equals FX_SUCCESS, the file was closed successfully. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1394">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1394">See Also</span></span>

- <span data-ttu-id="08a18-1395">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1395">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1396">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1396">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1397">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1397">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1398">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1398">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1399">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1399">fx_file_create</span></span>
- <span data-ttu-id="08a18-1400">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1400">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1401">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1401">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1402">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1402">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1403">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1403">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1404">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1404">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1405">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1405">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1406">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1406">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1407">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1407">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1408">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1408">fx_file_open</span></span>
- <span data-ttu-id="08a18-1409">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1409">fx_file_read</span></span>
- <span data-ttu-id="08a18-1410">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1410">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1411">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1411">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1412">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1412">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1413">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1413">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1414">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1414">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1415">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1415">fx_file_write</span></span>
- <span data-ttu-id="08a18-1416">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1416">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1417">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1417">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1418">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1418">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1419">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1419">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1420">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1420">fx_unicode_short_name_get</span></span>

## <a name="fx_file_create"></a><span data-ttu-id="08a18-1421">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1421">fx_file_create</span></span>

<span data-ttu-id="08a18-1422">Crea il file</span><span class="sxs-lookup"><span data-stu-id="08a18-1422">Creates file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1423">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1423">Prototype</span></span>

```c
UINT fx_file_create(
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="08a18-1424">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1424">Description</span></span>

<span data-ttu-id="08a18-1425">Questo servizio crea il file specificato nella directory predefinita o nel percorso della directory fornito con il nome del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1425">This service creates the specified file in the default directory or in the directory path supplied with the file name.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-1426">*Questo servizio crea un file di lunghezza zero, ovvero nessun cluster allocato. L'allocazione viene eseguita automaticamente nelle Scritture di file successive oppure può essere eseguita in anticipo con il servizio fx_file_allocate o fx_file_extended_allocate per uno spazio oltre i 4 GB).*</span><span class="sxs-lookup"><span data-stu-id="08a18-1426">*This service creates a file of zero length, i.e., no clusters allocated. Allocation will automatically take place on subsequent file writes or can be done in advance with the fx_file_allocate service or fx_file_extended_allocate for space beyond 4GB) service.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1427">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1427">Input Parameters</span></span>

- <span data-ttu-id="08a18-1428">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1428">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-1429">**file_name**: puntatore al nome del file da creare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1429">**file_name**: Pointer to the name of the file to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1430">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1430">Return Values</span></span>

- <span data-ttu-id="08a18-1431">Creazione file riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-1431">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="08a18-1432">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1432">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-1433">Il file specificato **FX_ALREADY_CREATED** (0x0B) è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1433">**FX_ALREADY_CREATED** (0x0B) Specified file was already created.</span></span>
- <span data-ttu-id="08a18-1434">**FX_NO_MORE_SPACE** (0x0A) non sono presenti altre voci nella directory radice oppure non sono disponibili altri cluster.</span><span class="sxs-lookup"><span data-stu-id="08a18-1434">**FX_NO_MORE_SPACE** (0x0A)    Either there are no more entries in the root directory or there are no more clusters available.</span></span>
- <span data-ttu-id="08a18-1435">**FX_INVALID_PATH** (0x0D) percorso non valido fornito con il nome file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1435">**FX_INVALID_PATH** (0x0D) Invalid path supplied with file name.</span></span>
- <span data-ttu-id="08a18-1436">Il nome del file **FX_INVALID_NAME** (0x0C) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1436">**FX_INVALID_NAME** (0x0C) File name is invalid.</span></span>
- <span data-ttu-id="08a18-1437">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1437">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1438">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1438">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1439">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1439">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1440">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1440">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1441">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1441">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1442">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-1442">**FX_MEDIA_INVALID** (0x02)Invalid media.</span></span>
- <span data-ttu-id="08a18-1443">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1443">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1444">Il supporto di **FX_WRITE_PROTECT** (0X23) sottostante è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1444">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="08a18-1445">**FX_PTR_ERROR** (0x18) non valido o il puntatore al nome file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1445">**FX_PTR_ERROR** (0x18) Invalid media or file name pointer.</span></span>
- <span data-ttu-id="08a18-1446">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1446">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1447">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1447">Allowed From</span></span>

<span data-ttu-id="08a18-1448">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1448">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1449">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1449">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Create a file called "myfile.txt" in the
    root or the default directory of the media. */

status = fx_file_create(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, a zero sized file named "myfile.txt". */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1450">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1450">See Also</span></span>
- <span data-ttu-id="08a18-1451">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1451">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1452">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1452">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1453">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1453">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1454">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1454">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1455">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1455">fx_file_close</span></span>
- <span data-ttu-id="08a18-1456">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1456">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1457">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1457">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1458">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1458">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1459">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1459">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1460">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1460">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1461">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1461">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1462">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1462">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1463">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1463">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1464">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1464">fx_file_open</span></span>
- <span data-ttu-id="08a18-1465">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1465">fx_file_read</span></span>
- <span data-ttu-id="08a18-1466">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1466">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1467">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1467">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1468">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1468">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1469">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1469">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1470">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1470">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1471">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1471">fx_file_write</span></span>
- <span data-ttu-id="08a18-1472">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1472">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1473">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1473">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1474">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1474">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1475">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1475">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1476">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1476">fx_unicode_short_name_get</span></span>

## <a name="fx_file_date_time_set"></a><span data-ttu-id="08a18-1477">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1477">fx_file_date_time_set</span></span>

### <a name="sets-file-date-and-time"></a><span data-ttu-id="08a18-1478">Imposta la data e l'ora del file</span><span class="sxs-lookup"><span data-stu-id="08a18-1478">Sets file date and time</span></span>

<span data-ttu-id="08a18-1479">Impostazione della data e dell'ora del file</span><span class="sxs-lookup"><span data-stu-id="08a18-1479">Setting File Date and Time</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1480">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1480">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="08a18-1481">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1481">Description</span></span>

<span data-ttu-id="08a18-1482">Questo servizio imposta la data e l'ora del file specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1482">This service sets the date and time of the specified file.</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="input-parameters"></a><span data-ttu-id="08a18-1483">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1483">Input Parameters</span></span>

- <span data-ttu-id="08a18-1484">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1484">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-1485">**file_name**: puntatore al nome del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1485">**file_name**: Pointer to name of the file.</span></span>
- <span data-ttu-id="08a18-1486">**anno**: valore dell'anno (1980-2107 inclusi).</span><span class="sxs-lookup"><span data-stu-id="08a18-1486">**year**: Value of year (1980-2107 inclusive).</span></span>
- <span data-ttu-id="08a18-1487">**mese**: valore del mese (1-12 inclusivo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1487">**month**: Value of month (1-12 inclusive).</span></span>
- <span data-ttu-id="08a18-1488">**giorno**: valore del giorno (1-31 inclusivo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1488">**day**: Value of day (1-31 inclusive).</span></span>
- <span data-ttu-id="08a18-1489">**ora**: valore di hour (0-23 inclusivo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1489">**hour**: Value of hour (0-23 inclusive).</span></span>
- <span data-ttu-id="08a18-1490">**minuto**: valore di minuto (0-59 inclusivo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1490">**minute**: Value of minute (0-59 inclusive).</span></span>
- <span data-ttu-id="08a18-1491">**secondo**: valore del secondo (0-59 inclusivo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1491">**second**: Value of second (0-59 inclusive).</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1492">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1492">Return Values</span></span>

- <span data-ttu-id="08a18-1493">Il set di data/ora **FX_SUCCESS** (0x00) ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="08a18-1493">**FX_SUCCESS** (0x00) Successful date/time set.</span></span>
- <span data-ttu-id="08a18-1494">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1494">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-1495">Impossibile trovare il file **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-1495">**FX_NOT_FOUND** (0x04)    File was not found.</span></span>
- <span data-ttu-id="08a18-1496">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1496">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="08a18-1497">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1497">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1498">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1498">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1499">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1499">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1500">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-1500">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="08a18-1501">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1501">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1502">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1502">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1503">**FX_PTR_ERROR** (0x18) supporto o puntatore al nome non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1503">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="08a18-1504">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1504">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="08a18-1505">L'anno **FX_INVALID_YEAR** (0x12) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1505">**FX_INVALID_YEAR** (0x12) Year is invalid.</span></span>
- <span data-ttu-id="08a18-1506">Il mese **FX_INVALID_MONTH** (0x13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1506">**FX_INVALID_MONTH** (0x13) Month is invalid.</span></span>
- <span data-ttu-id="08a18-1507">Il giorno **FX_INVALID_DAY** (0x14) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1507">**FX_INVALID_DAY** (0x14) Day is invalid.</span></span>
- <span data-ttu-id="08a18-1508">L'ora **FX_INVALID_HOUR** (0x15) non è valida.</span><span class="sxs-lookup"><span data-stu-id="08a18-1508">**FX_INVALID_HOUR** (0x15)    Hour is invalid.</span></span>
- <span data-ttu-id="08a18-1509">Il minuto **FX_INVALID_MINUTE** (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1509">**FX_INVALID_MINUTE** (0x16) Minute is invalid.</span></span>
- <span data-ttu-id="08a18-1510">Il secondo **FX_INVALID_SECOND** (0x17) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1510">**FX_INVALID_SECOND** (0x17) Second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1511">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1511">Allowed From</span></span>

<span data-ttu-id="08a18-1512">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1512">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1513">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1513">Example</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="see-also"></a><span data-ttu-id="08a18-1514">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1514">See Also</span></span>

- <span data-ttu-id="08a18-1515">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1515">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1516">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1516">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1517">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1517">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1518">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1518">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1519">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1519">fx_file_close</span></span>
- <span data-ttu-id="08a18-1520">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1520">fx_file_create</span></span>
- <span data-ttu-id="08a18-1521">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1521">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1522">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1522">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1523">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1523">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1524">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1524">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1525">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1525">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1526">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1526">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1527">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1527">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1528">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1528">fx_file_open</span></span>
- <span data-ttu-id="08a18-1529">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1529">fx_file_read</span></span>
- <span data-ttu-id="08a18-1530">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1530">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1531">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1531">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1532">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1532">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1533">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1533">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1534">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1534">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1535">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1535">fx_file_write</span></span>
- <span data-ttu-id="08a18-1536">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1536">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1537">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1537">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1538">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1538">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1539">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1539">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1540">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1540">fx_unicode_short_name_get</span></span>

## <a name="fx_file_delete"></a><span data-ttu-id="08a18-1541">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1541">fx_file_delete</span></span>

### <a name="deletes-file"></a><span data-ttu-id="08a18-1542">Elimina il file</span><span class="sxs-lookup"><span data-stu-id="08a18-1542">Deletes file</span></span>

<span data-ttu-id="08a18-1543">Eliminazione file</span><span class="sxs-lookup"><span data-stu-id="08a18-1543">File Deletion</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1544">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1544">Prototype</span></span>

```c
UINT fx_file_delete(
    FX_MEDIA *media_ptr, 
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="08a18-1545">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1545">Description</span></span>

<span data-ttu-id="08a18-1546">Questo servizio Elimina il file specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1546">This service deletes the specified file.</span></span>


### <a name="input-parameters"></a><span data-ttu-id="08a18-1547">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1547">Input Parameters</span></span>

- <span data-ttu-id="08a18-1548">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1548">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-1549">**file_name**: puntatore al nome del file da eliminare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1549">**file_name**: Pointer to the name of the file to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1550">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1550">Return Values</span></span>

- <span data-ttu-id="08a18-1551">Eliminazione file riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-1551">**FX_SUCCESS** (0x00) Successful file delete.</span></span>
- <span data-ttu-id="08a18-1552">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1552">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-1553">Il file specificato **FX_NOT_FOUND** (0x04) non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1553">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="08a18-1554">Il nome file specificato **FX_NOT_A_FILE** (0x05) è una directory o un volume.</span><span class="sxs-lookup"><span data-stu-id="08a18-1554">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="08a18-1555">Il file specificato **FX_ACCESS_ERROR** (0x06) è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1555">**FX_ACCESS_ERROR** (0x06) Specified file is currently open.</span></span>
- <span data-ttu-id="08a18-1556">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1556">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1557">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1557">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1558">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1558">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1559">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1559">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1560">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1560">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1561">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1561">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1562">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1562">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1563">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-1563">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-1564">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1564">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-1565">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1565">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1566">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1566">Allowed From</span></span>

<span data-ttu-id="08a18-1567">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1567">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1568">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1568">Example</span></span>

```c

FX_MEDIA            my_media;
UINT                 status;
/* Delete the file "myfile.txt". */

status = fx_file_delete(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, "myfile.txt" has been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1569">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1569">See Also</span></span>

- <span data-ttu-id="08a18-1570">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1570">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1571">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1571">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1572">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1572">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1573">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1573">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1574">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1574">fx_file_close</span></span>
- <span data-ttu-id="08a18-1575">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1575">fx_file_create</span></span>
- <span data-ttu-id="08a18-1576">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1576">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1577">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1577">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1578">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1578">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1579">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1579">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1580">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1580">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1581">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1581">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1582">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1582">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1583">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1583">fx_file_open</span></span>
- <span data-ttu-id="08a18-1584">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1584">fx_file_read</span></span>
- <span data-ttu-id="08a18-1585">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1585">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1586">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1586">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1587">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1587">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1588">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1588">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1589">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1589">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1590">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1590">fx_file_write</span></span>
- <span data-ttu-id="08a18-1591">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1591">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1592">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1592">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1593">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1593">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1594">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1594">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1595">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1595">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_allocate"></a><span data-ttu-id="08a18-1596">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1596">fx_file_extended_allocate</span></span>

<span data-ttu-id="08a18-1597">Alloca spazio per un file</span><span class="sxs-lookup"><span data-stu-id="08a18-1597">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1598">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1598">Prototype</span></span>

```c
UINT fx_file_extended_allocate(
    FX_FILE *file_ptr, 
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="08a18-1599">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1599">Description</span></span>

<span data-ttu-id="08a18-1600">Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1600">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="08a18-1601">FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster.</span><span class="sxs-lookup"><span data-stu-id="08a18-1601">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="08a18-1602">Il risultato viene quindi arrotondato per eccesso al cluster intero successivo.</span><span class="sxs-lookup"><span data-stu-id="08a18-1602">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="08a18-1603">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1603">This service is designed for exFAT.</span></span> <span data-ttu-id="08a18-1604">Il parametro *size* accetta un valore integer a 64 bit, che consente al chiamante di pre-allocare spazio oltre i 4 GB.</span><span class="sxs-lookup"><span data-stu-id="08a18-1604">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1605">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1605">Input Parameters</span></span>

- <span data-ttu-id="08a18-1606">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-1606">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="08a18-1607">**dimensioni**: numero di byte da allocare per il file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1607">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1608">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1608">Return Values</span></span>

- <span data-ttu-id="08a18-1609">**FX_SUCCESS** (0x00) l'allocazione di file riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-1609">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="08a18-1610">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1610">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-1611">Il file specificato **FX_NOT_OPEN** (0x07) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1611">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="08a18-1612">Il supporto di **FX_NO_MORE_SPACE** (0x0A) associato a questo file non dispone di un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="08a18-1612">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="08a18-1613">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1613">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1614">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1614">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1615">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1615">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1616">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1616">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1617">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1617">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1618">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1618">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1619">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1619">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-1620">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1620">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1621">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1621">Allowed From</span></span>

<span data-ttu-id="08a18-1622">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1622">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1623">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1623">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;
/* Allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_allocate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS the file now has
    one or more contiguous cluster(s) that can accommodate at least
    1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1624">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1624">See Also</span></span>

- <span data-ttu-id="08a18-1625">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1625">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1626">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1626">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1627">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1627">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1628">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1628">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1629">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1629">fx_file_close</span></span>
- <span data-ttu-id="08a18-1630">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1630">fx_file_create</span></span>
- <span data-ttu-id="08a18-1631">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1631">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1632">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1632">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1633">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1633">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1634">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1634">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1635">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1635">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1636">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1636">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1637">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1637">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1638">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1638">fx_file_open</span></span>
- <span data-ttu-id="08a18-1639">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1639">fx_file_read</span></span>
- <span data-ttu-id="08a18-1640">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1640">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1641">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1641">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1642">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1642">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1643">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1643">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1644">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1644">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1645">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1645">fx_file_write</span></span>
- <span data-ttu-id="08a18-1646">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1646">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1647">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1647">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1648">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1648">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1649">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1649">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1650">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1650">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_best_effort_allocate"></a><span data-ttu-id="08a18-1651">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1651">fx_file_extended_best_effort_allocate</span></span>

<span data-ttu-id="08a18-1652">Massimo sforzo per allocare spazio per un file</span><span class="sxs-lookup"><span data-stu-id="08a18-1652">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1653">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1653">Prototype</span></span>

```c
UINT fx_file_extended best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG64 size,
    ULONG64 *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="08a18-1654">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1654">Description</span></span>

<span data-ttu-id="08a18-1655">Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1655">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="08a18-1656">FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster.</span><span class="sxs-lookup"><span data-stu-id="08a18-1656">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="08a18-1657">Il risultato viene quindi arrotondato per eccesso al cluster intero successivo.</span><span class="sxs-lookup"><span data-stu-id="08a18-1657">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="08a18-1658">Se nel supporto non sono disponibili cluster consecutivi sufficienti, questo servizio collega il più grande blocco disponibile di cluster consecutivi al file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1658">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="08a18-1659">La quantità di spazio effettivamente allocata al file viene restituita al chiamante.</span><span class="sxs-lookup"><span data-stu-id="08a18-1659">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="08a18-1660">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1660">This service is designed for exFAT.</span></span> <span data-ttu-id="08a18-1661">Il parametro *size* accetta un valore integer a 64 bit, che consente al chiamante di pre-allocare spazio oltre i 4 GB.</span><span class="sxs-lookup"><span data-stu-id="08a18-1661">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1662">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1662">Input Parameters</span></span>

- <span data-ttu-id="08a18-1663">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-1663">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="08a18-1664">**dimensioni**: numero di byte da allocare per il file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1664">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1665">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1665">Return Values</span></span>

- <span data-ttu-id="08a18-1666">**FX_SUCCESS** (0x00) l'allocazione di file riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-1666">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="08a18-1667">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1667">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-1668">Il file specificato **FX_NOT_OPEN** (0x07) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1668">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="08a18-1669">Il supporto di **FX_NO_MORE_SPACE** (0x0A) associato a questo file non dispone di un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="08a18-1669">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="08a18-1670">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1670">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1671">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1671">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1672">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1672">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1673">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1673">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1674">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1674">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1675">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1675">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1676">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1676">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-1677">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1677">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1678">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1678">Allowed From</span></span>

<span data-ttu-id="08a18-1679">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1679">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1680">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1680">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-1681">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1681">See Also</span></span>

- <span data-ttu-id="08a18-1682">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1682">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1683">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1683">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1684">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1684">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1685">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1685">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1686">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1686">fx_file_close</span></span>
- <span data-ttu-id="08a18-1687">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1687">fx_file_create</span></span>
- <span data-ttu-id="08a18-1688">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1688">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1689">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1689">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1690">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1690">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1691">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1691">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1692">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1692">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1693">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1693">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1694">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1694">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1695">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1695">fx_file_open</span></span>
- <span data-ttu-id="08a18-1696">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1696">fx_file_read</span></span>
- <span data-ttu-id="08a18-1697">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1697">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1698">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1698">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1699">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1699">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1700">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1700">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1701">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1701">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1702">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1702">fx_file_write</span></span>
- <span data-ttu-id="08a18-1703">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1703">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1704">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1704">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1705">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1705">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1706">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1706">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1707">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1707">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_relative_seek"></a><span data-ttu-id="08a18-1708">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1708">fx_file_extended_relative_seek</span></span>

<span data-ttu-id="08a18-1709">Posizioni in un offset di byte relativo</span><span class="sxs-lookup"><span data-stu-id="08a18-1709">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1710">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1710">Prototype</span></span>

```c
UINT fx_file_extended_relative_seek(
    FX_FILE *file_ptr,
    ULONG64 byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="08a18-1711">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1711">Description</span></span>

<span data-ttu-id="08a18-1712">Questo servizio posiziona il puntatore di lettura/scrittura del file interno nell'offset di byte relativo specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1712">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="08a18-1713">Ogni successiva richiesta di lettura o scrittura verrà avviata in questo percorso del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1713">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="08a18-1714">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1714">This service is designed for exFAT.</span></span> <span data-ttu-id="08a18-1715">Il parametro *byte_offset* accetta un valore integer a 64 bit, che consente al chiamante di riposizionare il puntatore di lettura/scrittura oltre i 4 GB.</span><span class="sxs-lookup"><span data-stu-id="08a18-1715">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-1716">*Se l'operazione Seek tenta di eseguire la ricerca oltre la fine del file, il puntatore di lettura/scrittura del file viene posizionato alla fine del file. Viceversa, se l'operazione di ricerca tenta di posizionarsi oltre l'inizio del file, il puntatore di lettura/scrittura del file viene posizionato all'inizio del file.*</span><span class="sxs-lookup"><span data-stu-id="08a18-1716">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1717">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1717">Input Parameters</span></span>

- <span data-ttu-id="08a18-1718">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-1718">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="08a18-1719">**byte_offset**: offset di byte relativo desiderato nel file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1719">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="08a18-1720">**seek_from**: la direzione e la posizione in cui eseguire la ricerca relativa.</span><span class="sxs-lookup"><span data-stu-id="08a18-1720">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="08a18-1721">Le opzioni di ricerca valide sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="08a18-1721">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="08a18-1722">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-1722">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="08a18-1723">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-1723">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="08a18-1724">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-1724">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="08a18-1725">FX_SEEK_BACK (0x03) se si specifica FX_SEEK_BEGIN, l'operazione di ricerca viene eseguita a partire dall'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1725">FX_SEEK_BACK (0x03) If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="08a18-1726">Se FX_SEEK_END viene specificato, l'operazione di ricerca viene eseguita all'indietro a partire dalla fine del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1726">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="08a18-1727">Se FX_SEEK_FORWARD viene specificato, l'operazione di ricerca viene eseguita in base alla posizione del file corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-1727">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="08a18-1728">Se FX_SEEK_BACK viene specificato, l'operazione di ricerca viene eseguita all'indietro rispetto alla posizione corrente del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1728">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1729">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1729">Return Values</span></span>

- <span data-ttu-id="08a18-1730">**FX_SUCCESS** (0x00) il tentativo relativo al file riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-1730">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="08a18-1731">Il file specificato **FX_NOT_OPEN** (0x07) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1731">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="08a18-1732">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1732">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1733">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1733">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1734">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1734">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1735">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1735">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1736">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1736">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-1737">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1737">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1738">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1738">Allowed From</span></span>

<span data-ttu-id="08a18-1739">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1739">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1740">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1740">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to seek forward 0x100000000 bytes in "my_file". */

status = fx_file_extended_relative_seek(&my_file, 0x100000000, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write
    pointers are positioned 0x100000000 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1741">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1741">See Also</span></span>

- <span data-ttu-id="08a18-1742">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1742">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1743">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1743">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1744">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1744">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1745">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1745">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1746">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1746">fx_file_close</span></span>
- <span data-ttu-id="08a18-1747">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1747">fx_file_create</span></span>
- <span data-ttu-id="08a18-1748">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1748">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1749">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1749">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1750">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1750">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1751">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1751">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1752">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1752">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1753">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1753">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1754">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1754">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1755">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1755">fx_file_open</span></span>
- <span data-ttu-id="08a18-1756">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1756">fx_file_read</span></span>
- <span data-ttu-id="08a18-1757">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1757">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1758">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1758">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1759">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1759">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1760">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1760">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1761">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1761">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1762">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1762">fx_file_write</span></span>
- <span data-ttu-id="08a18-1763">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1763">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1764">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1764">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1765">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1765">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1766">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1766">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1767">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1767">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_seek"></a><span data-ttu-id="08a18-1768">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1768">fx_file_extended_seek</span></span>

<span data-ttu-id="08a18-1769">Offset posizioni in byte</span><span class="sxs-lookup"><span data-stu-id="08a18-1769">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1770">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1770">Prototype</span></span>

```c
UINT fx_file_extended_seek(
    FX_FILE *file_ptr, 
    ULONG64 byte_offset);
```
### <a name="description"></a><span data-ttu-id="08a18-1771">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1771">Description</span></span>

<span data-ttu-id="08a18-1772">Questo servizio posiziona il puntatore di lettura/scrittura del file interno nell'offset di byte specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1772">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="08a18-1773">Ogni successiva richiesta di lettura o scrittura verrà avviata in questo percorso del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1773">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="08a18-1774">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1774">This service is designed for exFAT.</span></span> <span data-ttu-id="08a18-1775">Il parametro *byte_offset* accetta un valore integer a 64 bit, che consente al chiamante di riposizionare il puntatore di lettura/scrittura oltre i 4 GB.</span><span class="sxs-lookup"><span data-stu-id="08a18-1775">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1776">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1776">Input Parameters</span></span>

- <span data-ttu-id="08a18-1777">**file_ptr**: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1777">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="08a18-1778">**byte_offset**: offset di byte desiderato nel file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1778">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="08a18-1779">Se il valore è zero, il puntatore di lettura/scrittura viene posizionato all'inizio del file, mentre un valore maggiore della dimensione del file posiziona il puntatore di lettura/scrittura alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1779">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1780">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1780">Return Values</span></span>

- <span data-ttu-id="08a18-1781">Ricerca file riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-1781">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="08a18-1782">Il file specificato **FX_NOT_OPEN** (0x07) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1782">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="08a18-1783">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1783">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1784">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1784">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1785">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1785">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1786">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1786">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1787">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1787">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-1788">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1788">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1789">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1789">Allowed From</span></span>

<span data-ttu-id="08a18-1790">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1790">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1791">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1791">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;
/* Seek to position 0x100000000 of "my_file." */

status = fx_file_extended_seek(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned 0x100000000 bytes from the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1792">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1792">See Also</span></span>

- <span data-ttu-id="08a18-1793">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1793">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1794">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1794">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1795">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1795">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1796">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1796">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1797">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1797">fx_file_close</span></span>
- <span data-ttu-id="08a18-1798">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1798">fx_file_create</span></span>
- <span data-ttu-id="08a18-1799">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1799">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1800">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1800">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1801">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1801">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1802">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1802">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1803">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1803">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1804">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1804">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1805">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1805">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1806">fx_file_open fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1806">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="08a18-1807">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1807">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1808">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1808">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1809">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1809">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1810">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1810">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1811">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1811">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1812">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1812">fx_file_write</span></span>
- <span data-ttu-id="08a18-1813">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1813">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1814">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1814">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1815">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1815">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1816">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1816">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1817">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1817">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate"></a><span data-ttu-id="08a18-1818">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1818">fx_file_extended_truncate</span></span>

<span data-ttu-id="08a18-1819">Tronca il file</span><span class="sxs-lookup"><span data-stu-id="08a18-1819">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1820">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1820">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="08a18-1821">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1821">Description</span></span>

<span data-ttu-id="08a18-1822">Questo servizio tronca le dimensioni del file fino alla dimensione specificata.</span><span class="sxs-lookup"><span data-stu-id="08a18-1822">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="08a18-1823">Se la dimensione fornita è maggiore delle dimensioni effettive del file, il servizio non esegue alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-1823">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="08a18-1824">Nessuno dei cluster multimediali associati al file viene rilasciato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1824">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-1825">*Usare cautela per troncare i file che possono anche essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="08a18-1825">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="08a18-1826">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1826">This service is designed for exFAT.</span></span> <span data-ttu-id="08a18-1827">Il parametro *size* accetta un valore integer a 64 bit, che consente al chiamante di funzionare oltre i 4 GB.</span><span class="sxs-lookup"><span data-stu-id="08a18-1827">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1828">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1828">Input Parameters</span></span>

- <span data-ttu-id="08a18-1829">**file_ptr**: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1829">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="08a18-1830">**dimensioni**: nuove dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1830">**size**: New file size.</span></span> <span data-ttu-id="08a18-1831">Byte oltre la nuova dimensione del file vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="08a18-1831">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1832">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1832">Return Values</span></span>

- <span data-ttu-id="08a18-1833">**FX_SUCCESS** (0x00) il troncamento del file è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-1833">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="08a18-1834">Il file specificato **FX_NOT_OPEN** (0x07) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1834">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="08a18-1835">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1835">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-1836">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1836">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1837">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1837">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1838">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1838">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1839">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1839">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1840">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1840">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1841">Il supporto di **FX_WRITE_PROTECT** (0X23) sottostante è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1841">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="08a18-1842">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1842">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-1843">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1843">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1844">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1844">Allowed From</span></span>

<span data-ttu-id="08a18-1845">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1845">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1846">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1846">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Truncate "my_file" to 0x100000000 bytes. */

status = fx_file_extended_truncate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, "my_file" contains 0x100000000 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1847">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1847">See Also</span></span>

- <span data-ttu-id="08a18-1848">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1848">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1849">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1849">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1850">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1850">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1851">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1851">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1852">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1852">fx_file_close</span></span>
- <span data-ttu-id="08a18-1853">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1853">fx_file_create</span></span>
- <span data-ttu-id="08a18-1854">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1854">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1855">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1855">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1856">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1856">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1857">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1857">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1858">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1858">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1859">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1859">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1860">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1860">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1861">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1861">fx_file_open</span></span>
- <span data-ttu-id="08a18-1862">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1862">fx_file_read</span></span>
- <span data-ttu-id="08a18-1863">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1863">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1864">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1864">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1865">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1865">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1866">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1866">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1867">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1867">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1868">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1868">fx_file_write</span></span>
- <span data-ttu-id="08a18-1869">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1869">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1870">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1870">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1871">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1871">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1872">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1872">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1873">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1873">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate_release"></a><span data-ttu-id="08a18-1874">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1874">fx_file_extended_truncate_release</span></span>

<span data-ttu-id="08a18-1875">Tronca i cluster di file e versioni</span><span class="sxs-lookup"><span data-stu-id="08a18-1875">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1876">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1876">Prototype</span></span>

```c
UINT fx_file_extended_truncate_release(
    FX_FILE *file_ptr, 
    ULONG64 size);
```

### <a name="description"></a><span data-ttu-id="08a18-1877">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1877">Description</span></span>

<span data-ttu-id="08a18-1878">Questo servizio tronca le dimensioni del file fino alla dimensione specificata.</span><span class="sxs-lookup"><span data-stu-id="08a18-1878">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="08a18-1879">Se la dimensione fornita è maggiore delle dimensioni effettive del file, il servizio non esegue alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-1879">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="08a18-1880">A differenza del servizio ***fx_file_extended_truncate*** , questo servizio rilascia tutti i cluster non utilizzati.</span><span class="sxs-lookup"><span data-stu-id="08a18-1880">Unlike the ***fx_file_extended_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-1881">*Usare cautela per troncare i file che possono anche essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="08a18-1881">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="08a18-1882">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1882">This service is designed for exFAT.</span></span> <span data-ttu-id="08a18-1883">Il parametro *size* accetta un valore integer a 64 bit, che consente al chiamante di funzionare oltre i 4 GB.</span><span class="sxs-lookup"><span data-stu-id="08a18-1883">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1884">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1884">Input Parameters</span></span>

- <span data-ttu-id="08a18-1885">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-1885">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="08a18-1886">**dimensioni**: nuove dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1886">**size**: New file size.</span></span> <span data-ttu-id="08a18-1887">Byte oltre la nuova dimensione del file vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="08a18-1887">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1888">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1888">Return Values</span></span>

- <span data-ttu-id="08a18-1889">**FX_SUCCESS** (0x00) il troncamento del file è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-1889">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="08a18-1890">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1890">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-1891">Il file specificato **FX_NOT_OPEN** (0x07) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1891">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="08a18-1892">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1892">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1893">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1893">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-1894">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1894">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1895">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1895">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-1896">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1896">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1897">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1897">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1898">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1898">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-1899">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1899">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-1900">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1900">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1901">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1901">Allowed From</span></span>

<span data-ttu-id="08a18-1902">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1902">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1903">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1903">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Attempt to truncate everything after the first 0x100000000 bytes of "my_file". */

status = fx_file_extended_truncate_release(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file is now 0x100000000
    bytes or fewer and all unused clusters have been released. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1904">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1904">See Also</span></span>

- <span data-ttu-id="08a18-1905">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1905">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1906">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1906">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1907">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1907">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1908">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1908">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1909">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-1909">fx_file_close</span></span>
- <span data-ttu-id="08a18-1910">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1910">fx_file_create</span></span>
- <span data-ttu-id="08a18-1911">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1911">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1912">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1912">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1913">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1913">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1914">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1914">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1915">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1915">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1916">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1916">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1917">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1917">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1918">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1918">fx_file_open</span></span>
- <span data-ttu-id="08a18-1919">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1919">fx_file_read</span></span>
- <span data-ttu-id="08a18-1920">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1920">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1921">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1921">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1922">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1922">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1923">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1923">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1924">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1924">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1925">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1925">fx_file_write</span></span>
- <span data-ttu-id="08a18-1926">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1926">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1927">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1927">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1928">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1928">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1929">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1929">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1930">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1930">fx_unicode_short_name_get</span></span>

## <a name="fx_file_open"></a><span data-ttu-id="08a18-1931">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-1931">fx_file_open</span></span>

<span data-ttu-id="08a18-1932">Apre il file</span><span class="sxs-lookup"><span data-stu-id="08a18-1932">Opens file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1933">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1933">Prototype</span></span>

```c
UINT fx_file_open(
    FX_MEDIA *media_ptr,
    FX_FILE *file_ptr,
    CHAR *file_name,
    UINT open_type);
```
### <a name="description"></a><span data-ttu-id="08a18-1934">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1934">Description</span></span>

<span data-ttu-id="08a18-1935">Questo servizio apre il file specificato per la lettura o la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1935">This service opens the specified file for either reading or writing.</span></span> <span data-ttu-id="08a18-1936">Un file può essere aperto per la lettura più volte, mentre un file può essere aperto solo per la scrittura una volta finché il writer non chiude il file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1936">A file may be opened for reading multiple times, while a file can only be opened for writing once until the writer closes the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-1937">*È necessario prestare attenzione se un file è aperto simultaneamente per la lettura e la scrittura. La scrittura di file eseguita quando un file viene aperto contemporaneamente per la lettura potrebbe non essere visibile dal lettore, a meno che il lettore non chiuda e riapra il file per la lettura. Analogamente, il writer di file deve prestare attenzione quando si usano i servizi di troncamento del file. Se un file viene troncato dal writer, i lettori dello stesso file potrebbero restituire dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="08a18-1937">*Care must be taken if a file is concurrently open for reading and writing. File writing performed when a file is simultaneously opened for reading may not be seen by the reader, unless the reader closes and reopens the file for reading. Similarly, the file writer should be careful when using file truncate services. If a file is truncated by the writer, readers of the same file could return invalid data.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-1938">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-1938">Input Parameters</span></span>

- <span data-ttu-id="08a18-1939">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-1939">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-1940">**file_ptr**: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1940">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="08a18-1941">**file_name**: puntatore al nome del file da aprire (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-1941">**file_name**: Pointer to the name of the file to open (directory path is optional).</span></span>
- <span data-ttu-id="08a18-1942">**open_type**: tipo di file aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1942">**open_type**: Type of file open.</span></span> <span data-ttu-id="08a18-1943">Le opzioni di tipo aperto valide sono:</span><span class="sxs-lookup"><span data-stu-id="08a18-1943">Valid open type options are:</span></span>
  - <span data-ttu-id="08a18-1944">FX_OPEN_FOR_READ (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-1944">FX_OPEN_FOR_READ (0x00)</span></span>
  - <span data-ttu-id="08a18-1945">FX_OPEN_FOR_WRITE (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-1945">FX_OPEN_FOR_WRITE (0x01)</span></span>
  - <span data-ttu-id="08a18-1946">FX_OPEN_FOR_READ_FAST (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-1946">FX_OPEN_FOR_READ_FAST (0x02)</span></span>

<span data-ttu-id="08a18-1947">L'apertura dei file con FX_OPEN_FOR_READ e FX_OPEN_FOR_READ_FAST è simile:</span><span class="sxs-lookup"><span data-stu-id="08a18-1947">Opening files with FX_OPEN_FOR_READ and FX_OPEN_FOR_READ_FAST is similar:</span></span>

- <span data-ttu-id="08a18-1948">FX_OPEN_FOR_READ include la verifica che l'elenco collegato di cluster che comprende il file sia intatto e FX_OPEN_FOR_READ_FAST non esegue questa verifica, rendendola più veloce.</span><span class="sxs-lookup"><span data-stu-id="08a18-1948">FX_OPEN_FOR_READ includes verification that the linked-list of clusters that comprise the file are intact, and FX_OPEN_FOR_READ_FAST does not perform this verification, which makes it faster.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-1949">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-1949">Return Values</span></span>

- <span data-ttu-id="08a18-1950">Apertura del file **FX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="08a18-1950">**FX_SUCCESS** (0x00) Successful file open.</span></span>
- <span data-ttu-id="08a18-1951">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-1951">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-1952">Il file specificato **FX_NOT_FOUND** (0x04) non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1952">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="08a18-1953">Il nome file specificato **FX_NOT_A_FILE** (0x05) è una directory o un volume.</span><span class="sxs-lookup"><span data-stu-id="08a18-1953">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="08a18-1954">Il file specificato **FX_FILE_CORRUPT** (0x08) è danneggiato e l'apertura non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-1954">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the open failed.</span></span>
- <span data-ttu-id="08a18-1955">Il file specificato **FX_ACCESS_ERROR** (0x06) è già aperto o il tipo aperto non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1955">**FX_ACCESS_ERROR** (0x06) Specified file is already open or open type is invalid.</span></span>
- <span data-ttu-id="08a18-1956">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-1956">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-1957">**FX_MEDIA_INVALID** (0x02) supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-1957">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="08a18-1958">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-1958">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-1959">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-1959">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-1960">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-1960">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-1961">Il supporto di **FX_WRITE_PROTECT** (0X23) sottostante è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-1961">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="08a18-1962">Il puntatore del file o del supporto di **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-1962">**FX_PTR_ERROR** (0x18) Invalid media or file pointer.</span></span>
- <span data-ttu-id="08a18-1963">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-1963">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-1964">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-1964">Allowed From</span></span>

<span data-ttu-id="08a18-1965">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-1965">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-1966">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-1966">Example</span></span>

```c
FX_MEDIA     my_media;
FX_FILE     my_file;
UINT         status;

/* Open the file "myfile.txt" for reading. */

status = fx_file_open(&my_media, &my_file, "myfile.txt", FX_OPEN_FOR_READ);

/* If status equals FX_SUCCESS, file "myfile.txt" is now
    open and may be accessed now with the my_file pointer. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-1967">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-1967">See Also</span></span>

- <span data-ttu-id="08a18-1968">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1968">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-1969">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1969">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-1970">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1970">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-1971">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1971">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1972">fx_file_close fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1972">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="08a18-1973">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1973">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-1974">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-1974">fx_file_delete</span></span>
- <span data-ttu-id="08a18-1975">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1975">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-1976">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-1976">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-1977">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1977">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-1978">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1978">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-1979">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1979">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-1980">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1980">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-1981">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1981">fx_file_read</span></span>
- <span data-ttu-id="08a18-1982">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1982">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-1983">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1983">fx_file_rename</span></span>
- <span data-ttu-id="08a18-1984">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-1984">fx_file_seek</span></span>
- <span data-ttu-id="08a18-1985">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-1985">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-1986">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-1986">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-1987">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-1987">fx_file_write</span></span>
- <span data-ttu-id="08a18-1988">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-1988">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-1989">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-1989">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-1990">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-1990">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-1991">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1991">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-1992">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-1992">fx_unicode_short_name_get</span></span>

## <a name="fx_file_read"></a><span data-ttu-id="08a18-1993">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-1993">fx_file_read</span></span>

<span data-ttu-id="08a18-1994">Legge i byte dal file</span><span class="sxs-lookup"><span data-stu-id="08a18-1994">Reads bytes from file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-1995">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-1995">Prototype</span></span>

```c
UINT fx_file_read(
    FX_FILE *file_ptr, 
    VOID *buffer_ptr,
    ULONG request_size, 
    ULONG *actual_size);
```
### <a name="description"></a><span data-ttu-id="08a18-1996">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-1996">Description</span></span>

<span data-ttu-id="08a18-1997">Questo servizio legge i byte dal file e li archivia nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-1997">This service reads bytes from the file and stores them in the supplied buffer.</span></span> <span data-ttu-id="08a18-1998">Al termine della lettura, il puntatore di lettura interno del file viene regolato in modo da puntare al byte successivo del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-1998">After the read is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span> <span data-ttu-id="08a18-1999">Se nella richiesta sono presenti meno byte rimanenti, solo i byte rimanenti vengono archiviati nel buffer.</span><span class="sxs-lookup"><span data-stu-id="08a18-1999">If there are fewer bytes remaining in the request, only the bytes remaining are stored in the buffer.</span></span> <span data-ttu-id="08a18-2000">In ogni caso, al chiamante viene restituito il numero totale di byte memorizzati nel buffer.</span><span class="sxs-lookup"><span data-stu-id="08a18-2000">In any case, the total number of bytes placed in the buffer is returned to the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2001">*L'applicazione deve garantire che il buffer fornito sia in grado di archiviare il numero specificato di byte richiesti.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2001">*The application must ensure that the buffer supplied is able to store the specified number of requested bytes.*</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2002">*Si ottengono prestazioni più veloci se il buffer di destinazione si trova su un limite di parole lunghe e la dimensione richiesta è equamente divisibile per sizeof (**ULONG**).*</span><span class="sxs-lookup"><span data-stu-id="08a18-2002">*Faster performance is achieved if the destination buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2003">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2003">Input Parameters</span></span>

- <span data-ttu-id="08a18-2004">**file_ptr**: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2004">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="08a18-2005">**buffer_ptr**: puntatore al buffer di destinazione per la lettura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2005">**buffer_ptr**: Pointer to the destination buffer for the read.</span></span>
- <span data-ttu-id="08a18-2006">**request_size**: numero massimo di byte da leggere.</span><span class="sxs-lookup"><span data-stu-id="08a18-2006">**request_size**: Maximum number of bytes to read.</span></span>
- <span data-ttu-id="08a18-2007">**actual_size**: puntatore alla variabile per memorizzare il numero effettivo di byte letti nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2007">**actual_size**: Pointer to the variable to hold the actual number of bytes read into the supplied buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2008">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2008">Return Values</span></span>

- <span data-ttu-id="08a18-2009">Lettura file riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-2009">**FX_SUCCESS** (0x00) Successful file read.</span></span>
- <span data-ttu-id="08a18-2010">Il file specificato **FX_NOT_OPEN** (0x07) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2010">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="08a18-2011">Il file specificato **FX_FILE_CORRUPT** (0x08) è danneggiato e la lettura non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-2011">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the read failed.</span></span>
- <span data-ttu-id="08a18-2012">È stata raggiunta la fine del file **FX_END_OF_FILE** (0x09).</span><span class="sxs-lookup"><span data-stu-id="08a18-2012">**FX_END_OF_FILE** (0x09) End of file has been reached.</span></span>
- <span data-ttu-id="08a18-2013">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2013">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-2014">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-2014">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-2015">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2015">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2016">**FX_PTR_ERROR** (0x18) il puntatore del buffer o del file non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2016">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="08a18-2017">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2017">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2018">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2018">Allowed From</span></span>

<span data-ttu-id="08a18-2019">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2019">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2020">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2020">Example</span></span>

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
### <a name="see-also"></a><span data-ttu-id="08a18-2021">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2021">See Also</span></span>

- <span data-ttu-id="08a18-2022">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2022">fx_file_allocate,</span></span>
- <span data-ttu-id="08a18-2023">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="08a18-2023">fx_file_attributes_read,</span></span>
- <span data-ttu-id="08a18-2024">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="08a18-2024">fx_file_attributes_set,</span></span>
- <span data-ttu-id="08a18-2025">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2025">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="08a18-2026">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="08a18-2026">fx_file_close,</span></span>
- <span data-ttu-id="08a18-2027">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="08a18-2027">fx_file_create,</span></span>
- <span data-ttu-id="08a18-2028">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="08a18-2028">fx_file_date_time_set,</span></span>
- <span data-ttu-id="08a18-2029">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="08a18-2029">fx_file_delete,</span></span>
- <span data-ttu-id="08a18-2030">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2030">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="08a18-2031">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2031">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="08a18-2032">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="08a18-2032">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="08a18-2033">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="08a18-2033">fx_file_extended_seek,</span></span>
- <span data-ttu-id="08a18-2034">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2034">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="08a18-2035">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="08a18-2035">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="08a18-2036">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="08a18-2036">fx_file_open,</span></span>
- <span data-ttu-id="08a18-2037">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="08a18-2037">fx_file_relative_seek,</span></span>
- <span data-ttu-id="08a18-2038">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="08a18-2038">fx_file_rename,</span></span>
- <span data-ttu-id="08a18-2039">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="08a18-2039">fx_file_seek,</span></span>
- <span data-ttu-id="08a18-2040">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2040">fx_file_truncate,</span></span>
- <span data-ttu-id="08a18-2041">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="08a18-2041">fx_file_truncate_release,</span></span>
- <span data-ttu-id="08a18-2042">fx_file_write,</span><span class="sxs-lookup"><span data-stu-id="08a18-2042">fx_file_write,</span></span>
- <span data-ttu-id="08a18-2043">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="08a18-2043">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="08a18-2044">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="08a18-2044">fx_unicode_file_create,</span></span>
- <span data-ttu-id="08a18-2045">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="08a18-2045">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="08a18-2046">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="08a18-2046">fx_unicode_name_get,</span></span>
- <span data-ttu-id="08a18-2047">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2047">fx_unicode_short_name_get</span></span>

## <a name="fx_file_relative_seek"></a><span data-ttu-id="08a18-2048">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2048">fx_file_relative_seek</span></span>

<span data-ttu-id="08a18-2049">Posizioni in un offset di byte relativo</span><span class="sxs-lookup"><span data-stu-id="08a18-2049">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2050">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2050">Prototype</span></span>

```c
UINT fx_file_relative_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="08a18-2051">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2051">Description</span></span>

<span data-ttu-id="08a18-2052">Questo servizio posiziona il puntatore di lettura/scrittura del file interno nell'offset di byte relativo specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2052">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="08a18-2053">Ogni successiva richiesta di lettura o scrittura verrà avviata in questo percorso del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2053">Any subsequent file read or write request will begin at this location in the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-2054">*Se l'operazione Seek tenta di eseguire la ricerca oltre la fine del file, il puntatore di lettura/scrittura del file viene posizionato alla fine del file. Viceversa, se l'operazione di ricerca tenta di posizionarsi oltre l'inizio del file, il puntatore di lettura/scrittura del file viene posizionato all'inizio del file.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2054">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

<span data-ttu-id="08a18-2055">Per eseguire una ricerca con un valore di offset oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_relative_seek*.</span><span class="sxs-lookup"><span data-stu-id="08a18-2055">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_relative_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2056">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2056">Input Parameters</span></span>

- <span data-ttu-id="08a18-2057">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-2057">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="08a18-2058">**byte_offset**: offset di byte relativo desiderato nel file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2058">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="08a18-2059">**seek_from**: la direzione e la posizione in cui eseguire la ricerca relativa.</span><span class="sxs-lookup"><span data-stu-id="08a18-2059">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="08a18-2060">Le opzioni di ricerca valide sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="08a18-2060">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="08a18-2061">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="08a18-2061">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="08a18-2062">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-2062">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="08a18-2063">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-2063">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="08a18-2064">FX_SEEK_BACK (0x03)</span><span class="sxs-lookup"><span data-stu-id="08a18-2064">FX_SEEK_BACK (0x03)</span></span>

<span data-ttu-id="08a18-2065">Se FX_SEEK_BEGIN viene specificato, l'operazione di ricerca viene eseguita a partire dall'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2065">If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="08a18-2066">Se FX_SEEK_END viene specificato, l'operazione di ricerca viene eseguita all'indietro a partire dalla fine del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2066">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="08a18-2067">Se FX_SEEK_FORWARD viene specificato, l'operazione di ricerca viene eseguita in base alla posizione del file corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-2067">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="08a18-2068">Se FX_SEEK_BACK viene specificato, l'operazione di ricerca viene eseguita all'indietro rispetto alla posizione corrente del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2068">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2069">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2069">Return Values</span></span>

- <span data-ttu-id="08a18-2070">**FX_SUCCESS** (0x00) il tentativo relativo al file riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2070">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="08a18-2071">Il file specificato **FX_NOT_OPEN** (0x07) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2071">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="08a18-2072">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2072">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2073">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-2074">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-2075">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2075">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-2076">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2076">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-2077">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2077">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2078">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2078">Allowed From</span></span>

<span data-ttu-id="08a18-2079">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2079">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2080">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2080">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to move 10 bytes forward in "my_file". */

status = fx_file_relative_seek(&my_file, 10, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write pointers
    are positioned 10 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-2081">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2081">See Also</span></span>

- <span data-ttu-id="08a18-2082">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2082">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-2083">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2083">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-2084">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2084">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-2085">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2085">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2086">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2086">fx_file_close</span></span>
- <span data-ttu-id="08a18-2087">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2087">fx_file_create</span></span>
- <span data-ttu-id="08a18-2088">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2088">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-2089">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-2089">fx_file_delete</span></span>
- <span data-ttu-id="08a18-2090">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2090">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-2091">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2091">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2092">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2092">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-2093">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2093">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-2094">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2094">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-2095">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2095">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-2096">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2096">fx_file_open</span></span>
- <span data-ttu-id="08a18-2097">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2097">fx_file_read</span></span>
- <span data-ttu-id="08a18-2098">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2098">fx_file_rename</span></span>
- <span data-ttu-id="08a18-2099">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2099">fx_file_seek</span></span>
- <span data-ttu-id="08a18-2100">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2100">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-2101">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2101">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-2102">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2102">fx_file_write</span></span>
- <span data-ttu-id="08a18-2103">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2103">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-2104">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2104">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-2105">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2105">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-2106">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2106">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-2107">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2107">fx_unicode_short_name_get</span></span>

## <a name="fx_file_rename"></a><span data-ttu-id="08a18-2108">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2108">fx_file_rename</span></span>

<span data-ttu-id="08a18-2109">Rinomina il file</span><span class="sxs-lookup"><span data-stu-id="08a18-2109">Renames  file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2110">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2110">Prototype</span></span>

```c
UINT fx_file_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_file_name,
    CHAR *new_file_name);
```
### <a name="description"></a><span data-ttu-id="08a18-2111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2111">Description</span></span>

<span data-ttu-id="08a18-2112">Questo servizio modifica il nome del file specificato da *old_file_name*.</span><span class="sxs-lookup"><span data-stu-id="08a18-2112">This service changes the name of the file specified by *old_file_name*.</span></span> <span data-ttu-id="08a18-2113">La ridenominazione viene eseguita anche in relazione al percorso specificato o al percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2113">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="08a18-2114">Se viene specificato un percorso nel nuovo nome file, il file rinominato viene spostato in modo efficace nel percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2114">If a path is specified in the new file name, the renamed file is effectively moved to the specified path.</span></span> <span data-ttu-id="08a18-2115">Se non viene specificato alcun percorso, il file rinominato viene inserito nel percorso predefinito corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-2115">If no path is specified, the renamed file is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2116">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2116">Input Parameters</span></span>

- <span data-ttu-id="08a18-2117">**media_ptr**: puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2117">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="08a18-2118">**old_file_name**: puntatore al nome del file da rinominare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="08a18-2118">**old_file_name**: Pointer to the name of the file to rename (directory path is optional).</span></span>
- <span data-ttu-id="08a18-2119">**new_file_name**: puntatore al nuovo nome file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2119">**new_file_name**: Pointer to the new file name.</span></span> <span data-ttu-id="08a18-2120">Il percorso della directory non è consentito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2120">The directory path is not allowed.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2121">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2121">Return Values</span></span>

- <span data-ttu-id="08a18-2122">**FX_SUCCESS** (0x00) ridenominazione del file riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-2122">**FX_SUCCESS** (0x00) Successful file rename.</span></span>
- <span data-ttu-id="08a18-2123">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2123">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2124">Il file specificato **FX_NOT_FOUND** (0x04) non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2124">**FX_NOT_FOUND** (0x04)    Specified file was not found.</span></span>
- <span data-ttu-id="08a18-2125">**FX_NOT_A_FILE** file specificato (0x05) è una directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-2125">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="08a18-2126">Il file specificato **FX_ACCESS_ERROR** (0x06) è già aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2126">**FX_ACCESS_ERROR** (0x06) Specified file is already open.</span></span>
- <span data-ttu-id="08a18-2127">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2127">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2128">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2128">**FX_WRITE_PROTECT** (0x23)    Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-2129">**FX_INVALID_NAME** (0x0C) il nome file specificato non è un nome di file valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2129">**FX_INVALID_NAME** (0x0C) Specified new file name is not a valid file name.</span></span>
- <span data-ttu-id="08a18-2130">Il percorso **FX_INVALID_PATH** (0x0D) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2130">**FX_INVALID_PATH** (0x0D)    Path is invalid.</span></span>
- <span data-ttu-id="08a18-2131">**FX_ALREADY_CREATED** (0x0B) viene utilizzato il nuovo nome file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2131">**FX_ALREADY_CREATED** (0x0B) The new file name is used.</span></span>
- <span data-ttu-id="08a18-2132">Il supporto **FX_MEDIA_INVALID** (0x02) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2132">**FX_MEDIA_INVALID** (0x02)    Media is invalid.</span></span>
- <span data-ttu-id="08a18-2133">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2133">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-2134">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2134">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-2135">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2135">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-2136">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-2136">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-2137">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2137">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="08a18-2138">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2138">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-2139">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2139">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2140">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2140">Allowed From</span></span>

<span data-ttu-id="08a18-2141">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2141">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2142">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2142">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Rename "myfile1.txt" to "myfile2.txt" in the default directory of the media. */

status = fx_file_rename(&my_media, "myfile1.txt", "myfile2.txt");

/* If status equals FX_SUCCESS, the file was successfully renamed. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-2143">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2143">See Also</span></span>

- <span data-ttu-id="08a18-2144">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2144">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-2145">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2145">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-2146">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2146">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-2147">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2147">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2148">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2148">fx_file_close</span></span>
- <span data-ttu-id="08a18-2149">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2149">fx_file_create</span></span>
- <span data-ttu-id="08a18-2150">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2150">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-2151">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-2151">fx_file_delete</span></span>
- <span data-ttu-id="08a18-2152">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2152">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-2153">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2153">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2154">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2154">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-2155">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2155">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-2156">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2156">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-2157">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2157">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-2158">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2158">fx_file_open</span></span>
- <span data-ttu-id="08a18-2159">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2159">fx_file_read</span></span>
- <span data-ttu-id="08a18-2160">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2160">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-2161">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2161">fx_file_seek</span></span>
- <span data-ttu-id="08a18-2162">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2162">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-2163">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2163">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-2164">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2164">fx_file_write</span></span>
- <span data-ttu-id="08a18-2165">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2165">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-2166">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2166">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-2167">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2167">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-2168">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2168">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-2169">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2169">fx_unicode_short_name_get</span></span>

## <a name="fx_file_seek"></a><span data-ttu-id="08a18-2170">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2170">fx_file_seek</span></span>

<span data-ttu-id="08a18-2171">Offset posizioni in byte</span><span class="sxs-lookup"><span data-stu-id="08a18-2171">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2172">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2172">Prototype</span></span>

```c
UINT fx_file_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset);
```
### <a name="description"></a><span data-ttu-id="08a18-2173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2173">Description</span></span>

<span data-ttu-id="08a18-2174">Questo servizio posiziona il puntatore di lettura/scrittura del file interno nell'offset di byte specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2174">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="08a18-2175">Ogni successiva richiesta di lettura o scrittura verrà avviata in questo percorso del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2175">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="08a18-2176">Per eseguire una ricerca con un valore di offset oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_seek*.</span><span class="sxs-lookup"><span data-stu-id="08a18-2176">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2177">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2177">Input Parameters</span></span>

- <span data-ttu-id="08a18-2178">**file_ptr**: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2178">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="08a18-2179">**byte_offset**: offset di byte desiderato nel file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2179">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="08a18-2180">Se il valore è zero, il puntatore di lettura/scrittura viene posizionato all'inizio del file, mentre un valore maggiore della dimensione del file posiziona il puntatore di lettura/scrittura alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2180">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2181">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2181">Return Values</span></span>

- <span data-ttu-id="08a18-2182">Ricerca file riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-2182">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="08a18-2183">Il file specificato **FX_NOT_OPEN** (0x07) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2183">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="08a18-2184">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2184">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2185">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2185">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-2186">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2186">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-2187">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-2187">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-2188">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2188">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-2189">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2190">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2190">Allowed From</span></span>

<span data-ttu-id="08a18-2191">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2192">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2192">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Seek to the beginning of "my_file." */
status = fx_file_seek(&my_file, 0);
/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned to the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-2193">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2193">See Also</span></span>

- <span data-ttu-id="08a18-2194">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2194">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-2195">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2195">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-2196">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2196">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-2197">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2197">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2198">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2198">fx_file_close</span></span>
- <span data-ttu-id="08a18-2199">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2199">fx_file_create</span></span>
- <span data-ttu-id="08a18-2200">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2200">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-2201">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-2201">fx_file_delete</span></span>
- <span data-ttu-id="08a18-2202">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2202">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-2203">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2203">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2204">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2204">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-2205">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2205">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-2206">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2206">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-2207">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2207">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-2208">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2208">fx_file_open</span></span>
- <span data-ttu-id="08a18-2209">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2209">fx_file_read</span></span>
- <span data-ttu-id="08a18-2210">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2210">fx_file_rename</span></span>
- <span data-ttu-id="08a18-2211">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2211">fx_file_seek</span></span>
- <span data-ttu-id="08a18-2212">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2212">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-2213">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2213">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-2214">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2214">fx_file_write</span></span>
- <span data-ttu-id="08a18-2215">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2215">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-2216">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2216">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-2217">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2217">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-2218">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2218">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-2219">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2219">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate"></a><span data-ttu-id="08a18-2220">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2220">fx_file_truncate</span></span>

<span data-ttu-id="08a18-2221">Tronca il file</span><span class="sxs-lookup"><span data-stu-id="08a18-2221">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2222">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2222">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="08a18-2223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2223">Description</span></span>

<span data-ttu-id="08a18-2224">Questo servizio tronca le dimensioni del file fino alla dimensione specificata.</span><span class="sxs-lookup"><span data-stu-id="08a18-2224">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="08a18-2225">Se la dimensione fornita è maggiore delle dimensioni effettive del file, il servizio non esegue alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-2225">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="08a18-2226">Nessuno dei cluster multimediali associati al file viene rilasciato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2226">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2227">*Usare cautela per troncare i file che possono anche essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2227">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="08a18-2228">Per operare oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_truncate*.</span><span class="sxs-lookup"><span data-stu-id="08a18-2228">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2229">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2229">Input Parameters</span></span>

- <span data-ttu-id="08a18-2230">**file_ptr**: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2230">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="08a18-2231">**dimensioni**: nuove dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2231">**size**: New file size.</span></span> <span data-ttu-id="08a18-2232">Byte oltre la nuova dimensione del file vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="08a18-2232">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2233">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2233">Return Values</span></span>

- <span data-ttu-id="08a18-2234">**FX_SUCCESS** (0x00) il troncamento del file è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2234">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="08a18-2235">Il file specificato **FX_NOT_OPEN** (0x07) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2235">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="08a18-2236">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2236">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-2237">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2237">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2238">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2238">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-2239">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2239">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-2240">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2240">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-2241">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2241">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-2242">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="08a18-2242">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="08a18-2243">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2243">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-2244">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2244">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2245">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2245">Allowed From</span></span>

<span data-ttu-id="08a18-2246">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2246">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2247">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2247">Example</span></span>

```c
FX_FILE                my_file;
UINT                status;
/* Truncate "my_file" to 100 bytes. */

status = fx_file_truncate(&my_file, 100);

/* If status equals FX_SUCCESS, "my_file" contains 100 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-2248">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2248">See Also</span></span>

- <span data-ttu-id="08a18-2249">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2249">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-2250">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2250">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-2251">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2251">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-2252">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2252">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2253">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2253">fx_file_close</span></span>
- <span data-ttu-id="08a18-2254">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2254">fx_file_create</span></span>
- <span data-ttu-id="08a18-2255">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2255">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-2256">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-2256">fx_file_delete</span></span>
- <span data-ttu-id="08a18-2257">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2257">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-2258">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2258">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2259">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2259">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-2260">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2260">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-2261">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2261">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-2262">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2262">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-2263">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2263">fx_file_open</span></span>
- <span data-ttu-id="08a18-2264">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2264">fx_file_read</span></span>
- <span data-ttu-id="08a18-2265">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2265">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-2266">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2266">fx_file_rename</span></span>
- <span data-ttu-id="08a18-2267">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2267">fx_file_seek</span></span>
- <span data-ttu-id="08a18-2268">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2268">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-2269">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2269">fx_file_write</span></span>
- <span data-ttu-id="08a18-2270">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2270">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-2271">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2271">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-2272">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2272">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-2273">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2273">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-2274">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2274">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate_release"></a><span data-ttu-id="08a18-2275">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2275">fx_file_truncate_release</span></span>

<span data-ttu-id="08a18-2276">Tronca i cluster di file e versioni</span><span class="sxs-lookup"><span data-stu-id="08a18-2276">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2277">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2277">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="08a18-2278">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2278">Description</span></span>

<span data-ttu-id="08a18-2279">Questo servizio tronca le dimensioni del file fino alla dimensione specificata.</span><span class="sxs-lookup"><span data-stu-id="08a18-2279">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="08a18-2280">Se la dimensione fornita è maggiore delle dimensioni effettive del file, il servizio non esegue alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-2280">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="08a18-2281">A differenza del servizio ***fx_file_truncate*** , questo servizio rilascia tutti i cluster non utilizzati.</span><span class="sxs-lookup"><span data-stu-id="08a18-2281">Unlike the ***fx_file_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2282">*Usare cautela per troncare i file che possono anche essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2282">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="08a18-2283">Per operare oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_truncate_release*.</span><span class="sxs-lookup"><span data-stu-id="08a18-2283">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate_release*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2284">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2284">Input Parameters</span></span>

- <span data-ttu-id="08a18-2285">**file_ptr**: puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-2285">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="08a18-2286">**dimensioni**: nuove dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2286">**size**: New file size.</span></span> <span data-ttu-id="08a18-2287">Byte oltre la nuova dimensione del file vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="08a18-2287">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2288">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2288">Return Values</span></span>

- <span data-ttu-id="08a18-2289">**FX_SUCCESS** (0x00) il troncamento del file è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2289">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="08a18-2290">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2290">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-2291">Il file specificato **FX_NOT_OPEN** (0x07) non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2291">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="08a18-2292">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2292">**FX_IO_ERROR** (0x90)    Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2293">Il supporto di **FX_WRITE_PROTECT** (0X23) sottostante è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2293">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="08a18-2294">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2294">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="08a18-2295">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2295">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-2296">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2296">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-2297">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2297">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-2298">**FX_NO_MORE_SPACE** (0X0A) non più spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-2298">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation.</span></span>
- <span data-ttu-id="08a18-2299">Il puntatore del file **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2299">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="08a18-2300">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2300">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2301">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2301">Allowed From</span></span>

<span data-ttu-id="08a18-2302">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2302">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2303">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2303">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;

/* Attempt to truncate everything after the first 100 bytes of "my_file". */

status = fx_file_truncate_release(&my_file, 100);

/* If status equals FX_SUCCESS, the file is now 100 bytes
    or fewer and all unused clusters have been released. */
```
### <a name="see-also"></a><span data-ttu-id="08a18-2304">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2304">See Also</span></span>

- <span data-ttu-id="08a18-2305">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2305">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-2306">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2306">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-2307">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2307">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-2308">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2308">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2309">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2309">fx_file_close</span></span>
- <span data-ttu-id="08a18-2310">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2310">fx_file_create</span></span>
- <span data-ttu-id="08a18-2311">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2311">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-2312">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-2312">fx_file_delete</span></span>
- <span data-ttu-id="08a18-2313">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2313">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-2314">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2314">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2315">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2315">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-2316">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2316">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-2317">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2317">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-2318">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2318">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-2319">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2319">fx_file_open</span></span>
- <span data-ttu-id="08a18-2320">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2320">fx_file_read</span></span>
- <span data-ttu-id="08a18-2321">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2321">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-2322">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2322">fx_file_rename</span></span>
- <span data-ttu-id="08a18-2323">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2323">fx_file_seek</span></span>
- <span data-ttu-id="08a18-2324">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2324">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-2325">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2325">fx_file_write</span></span>
- <span data-ttu-id="08a18-2326">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2326">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-2327">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2327">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-2328">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2328">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-2329">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2329">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-2330">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2330">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write"></a><span data-ttu-id="08a18-2331">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2331">fx_file_write</span></span>

<span data-ttu-id="08a18-2332">Scrive i byte nel file</span><span class="sxs-lookup"><span data-stu-id="08a18-2332">Writes bytes to file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2333">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2333">Prototype</span></span>

```c
UINT fx_file_write(
    FX_FILE *file_ptr,
    VOID *buffer_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="08a18-2334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2334">Description</span></span>

<span data-ttu-id="08a18-2335">Questo servizio scrive i byte dal buffer specificato a partire dalla posizione corrente del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2335">This service writes bytes from the specified buffer starting at the file's current position.</span></span> <span data-ttu-id="08a18-2336">Al termine della scrittura, il puntatore di lettura interno del file viene regolato in modo da puntare al byte successivo del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2336">After the write is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2337">*Si ottengono prestazioni più veloci se il buffer di origine si trova su un limite di parole lunghe e la dimensione richiesta è equamente divisibile per sizeof (**ULONG**).*</span><span class="sxs-lookup"><span data-stu-id="08a18-2337">*Faster performance is achieved if the source buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2338">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2338">Input Parameters</span></span>

- <span data-ttu-id="08a18-2339">**file_ptr**: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2339">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="08a18-2340">**buffer_ptr**: puntatore al buffer di origine per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2340">**buffer_ptr**: Pointer to the source buffer for the write.</span></span>
- <span data-ttu-id="08a18-2341">**dimensioni**: numero di byte da scrivere.</span><span class="sxs-lookup"><span data-stu-id="08a18-2341">**size**: Number of bytes to write.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2342">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2342">Return Values</span></span>

- <span data-ttu-id="08a18-2343">**FX_SUCCESS** (0x00) scrittura file riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-2343">**FX_SUCCESS** (0x00) Successful file write.</span></span>
- <span data-ttu-id="08a18-2344">Il file specificato **FX_NOT_OPEN** (0x07) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2344">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="08a18-2345">Il file specificato **FX_ACCESS_ERROR** (0x06) non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2345">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="08a18-2346">**FX_NO_MORE_SPACE** (0x0A) non è disponibile più spazio nel supporto per l'esecuzione di questa operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2346">**FX_NO_MORE_SPACE** (0x0A) There is no more room available in the media to perform this write.</span></span>
- <span data-ttu-id="08a18-2347">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2347">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2348">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2348">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-2349">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2349">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-2350">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2350">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-2351">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2351">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="08a18-2352">**FX_NO_MORE_ENTRIES** (0X0F) non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2352">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="08a18-2353">**FX_PTR_ERROR** (0x18) il puntatore del buffer o del file non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2353">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="08a18-2354">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2354">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2355">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2355">Allowed From</span></span>

<span data-ttu-id="08a18-2356">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2356">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2357">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2357">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Write a 10 character buffer to "my_file." */

status = fx_file_write(&my_file, "1234567890", 10);

/* If status equals FX_SUCCESS, the small text string was written out to the file. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-2358">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2358">See Also</span></span>

- <span data-ttu-id="08a18-2359">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2359">fx_file_allocate,</span></span>
- <span data-ttu-id="08a18-2360">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="08a18-2360">fx_file_attributes_read,</span></span>
- <span data-ttu-id="08a18-2361">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="08a18-2361">fx_file_attributes_set,</span></span>
- <span data-ttu-id="08a18-2362">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2362">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="08a18-2363">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="08a18-2363">fx_file_close,</span></span>
- <span data-ttu-id="08a18-2364">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="08a18-2364">fx_file_create,</span></span>
- <span data-ttu-id="08a18-2365">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="08a18-2365">fx_file_date_time_set,</span></span>
- <span data-ttu-id="08a18-2366">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="08a18-2366">fx_file_delete,</span></span>
- <span data-ttu-id="08a18-2367">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2367">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="08a18-2368">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2368">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="08a18-2369">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="08a18-2369">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="08a18-2370">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="08a18-2370">fx_file_extended_seek,</span></span>
- <span data-ttu-id="08a18-2371">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2371">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="08a18-2372">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="08a18-2372">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="08a18-2373">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="08a18-2373">fx_file_open,</span></span>
- <span data-ttu-id="08a18-2374">fx_file_read,</span><span class="sxs-lookup"><span data-stu-id="08a18-2374">fx_file_read,</span></span>
- <span data-ttu-id="08a18-2375">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="08a18-2375">fx_file_relative_seek,</span></span>
- <span data-ttu-id="08a18-2376">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="08a18-2376">fx_file_rename,</span></span>
- <span data-ttu-id="08a18-2377">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="08a18-2377">fx_file_seek,</span></span>
- <span data-ttu-id="08a18-2378">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="08a18-2378">fx_file_truncate,</span></span>
- <span data-ttu-id="08a18-2379">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="08a18-2379">fx_file_truncate_release,</span></span>
- <span data-ttu-id="08a18-2380">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="08a18-2380">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="08a18-2381">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="08a18-2381">fx_unicode_file_create,</span></span>
- <span data-ttu-id="08a18-2382">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="08a18-2382">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="08a18-2383">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="08a18-2383">fx_unicode_name_get,</span></span>
- <span data-ttu-id="08a18-2384">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2384">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write_notify_set"></a><span data-ttu-id="08a18-2385">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2385">fx_file_write_notify_set</span></span>

<span data-ttu-id="08a18-2386">Imposta la funzione di notifica di scrittura del file</span><span class="sxs-lookup"><span data-stu-id="08a18-2386">Sets the file write notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2387">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2387">Prototype</span></span>

```c
UINT fx_file_write_notify_set(
    FX_FILE *file_ptr,
    VOID (*file_write_notify)(FX_FILE*));
```
### <a name="description"></a><span data-ttu-id="08a18-2388">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2388">Description</span></span>

<span data-ttu-id="08a18-2389">Questo servizio installa la funzione di callback che viene richiamata dopo una corretta operazione di scrittura del file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2389">This service installs callback function that is invoked after a successful file write operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2390">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2390">Input Parameters</span></span>

- <span data-ttu-id="08a18-2391">**file_ptr**: puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-2391">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="08a18-2392">**file_write_notify**: funzione di callback di scrittura file da installare.</span><span class="sxs-lookup"><span data-stu-id="08a18-2392">**file_write_notify**: File write callback function to be installed.</span></span> <span data-ttu-id="08a18-2393">Imposta la funzione di callback su NULL disabilita la funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="08a18-2393">Set the callback function to NULL disables the callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2394">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2394">Return Values</span></span>

- <span data-ttu-id="08a18-2395">**FX_SUCCESS** (0x00) ha installato correttamente la funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="08a18-2395">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="08a18-2396">Il file_ptr **FX_PTR_ERROR** (0x18) è null.</span><span class="sxs-lookup"><span data-stu-id="08a18-2396">**FX_PTR_ERROR** (0x18) file_ptr is NULL.</span></span>
- <span data-ttu-id="08a18-2397">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2397">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2398">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2398">Allowed From</span></span>

<span data-ttu-id="08a18-2399">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2400">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2400">Example</span></span>

```c
fx_file_write_notify_set(file_ptr, my_file_close_callback);

```

### <a name="see-also"></a><span data-ttu-id="08a18-2401">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2401">See Also</span></span>

- <span data-ttu-id="08a18-2402">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2402">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-2403">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2403">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-2404">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2404">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-2405">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2405">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2406">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2406">fx_file_close</span></span>
- <span data-ttu-id="08a18-2407">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2407">fx_file_create</span></span>
- <span data-ttu-id="08a18-2408">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2408">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-2409">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-2409">fx_file_delete</span></span>
- <span data-ttu-id="08a18-2410">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2410">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-2411">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-2411">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-2412">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2412">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-2413">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2413">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-2414">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2414">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-2415">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2415">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-2416">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2416">fx_file_open</span></span>
- <span data-ttu-id="08a18-2417">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2417">fx_file_read</span></span>
- <span data-ttu-id="08a18-2418">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2418">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-2419">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2419">fx_file_rename</span></span>
- <span data-ttu-id="08a18-2420">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-2420">fx_file_seek</span></span>
- <span data-ttu-id="08a18-2421">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-2421">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-2422">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-2422">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-2423">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2423">fx_file_write</span></span>
- <span data-ttu-id="08a18-2424">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-2424">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-2425">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-2425">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-2426">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2426">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-2427">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2427">fx_unicode_short_name_get</span></span>

## <a name="fx_media_abort"></a><span data-ttu-id="08a18-2428">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2428">fx_media_abort</span></span>

<span data-ttu-id="08a18-2429">Interrompe le attività multimediali</span><span class="sxs-lookup"><span data-stu-id="08a18-2429">Aborts media activities</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2430">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2430">Prototype</span></span>

```c
UINT fx_media_abort(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-2431">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2431">Description</span></span>

<span data-ttu-id="08a18-2432">Questo servizio interrompe tutte le attività correnti associate al supporto, inclusa la chiusura di tutti i file aperti, l'invio di una richiesta di interruzione al driver associato e l'inserimento del supporto in uno stato interrotto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2432">This service aborts all current activities associated with the media, including closing all open files, sending an abort request to the associated driver, and placing the media in an aborted state.</span></span> <span data-ttu-id="08a18-2433">Questo servizio viene in genere chiamato quando vengono rilevati errori di I/O.</span><span class="sxs-lookup"><span data-stu-id="08a18-2433">This service is typically called when I/O errors are detected.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2434">*È necessario riaprire il supporto per riutilizzarlo dopo l'esecuzione di un'operazione di interruzione.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2434">*The media must be re-opened to use it again after an abort operation is performed.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2435">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2435">Input Parameters</span></span>

- <span data-ttu-id="08a18-2436">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2436">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2437">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2437">Return Values</span></span>

- <span data-ttu-id="08a18-2438">Interruzione del supporto di **FX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-2438">**FX_SUCCESS** (0x00) Successful media abort.</span></span>
- <span data-ttu-id="08a18-2439">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2439">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2440">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2440">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-2441">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2441">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2442">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2442">Allowed From</span></span>

<span data-ttu-id="08a18-2443">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2443">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2444">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2444">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Abort all activity associated with "my_media". */

status = fx_media_abort(&my_media);

/* If status equals FX_SUCCESS, all activity
    associated with the media has been aborted. */

```

### <a name="see-also"></a><span data-ttu-id="08a18-2445">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2445">See Also</span></span>

- <span data-ttu-id="08a18-2446">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2446">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2447">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2447">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2448">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2448">fx_media_check</span></span>
- <span data-ttu-id="08a18-2449">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2449">fx_media_close</span></span>
- <span data-ttu-id="08a18-2450">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2450">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2451">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2451">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2452">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2452">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2453">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2453">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2454">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2454">fx_media_format</span></span>
- <span data-ttu-id="08a18-2455">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2455">fx_media_open</span></span>
- <span data-ttu-id="08a18-2456">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2456">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2457">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2457">fx_media_read</span></span>
- <span data-ttu-id="08a18-2458">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2458">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2459">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2459">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2460">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2460">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2461">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2461">fx_media_write</span></span>
- <span data-ttu-id="08a18-2462">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2462">fx_system_initialize</span></span>

## <a name="fx_media_cache_invalidate"></a><span data-ttu-id="08a18-2463">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2463">fx_media_cache_invalidate</span></span>

<span data-ttu-id="08a18-2464">Invalida la cache del settore logico</span><span class="sxs-lookup"><span data-stu-id="08a18-2464">Invalidates logical sector cache</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2465">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2465">Prototype</span></span>

```c
UINT fx_media_cache_invalidate(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="08a18-2466">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2466">Description</span></span>

<span data-ttu-id="08a18-2467">Questo servizio Scarica tutti i settori dirty nella cache e quindi invalida l'intera cache del settore logico.</span><span class="sxs-lookup"><span data-stu-id="08a18-2467">This service flushes all dirty sectors in the cache and then invalidates the entire logical sector cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2468">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2468">Input Parameters</span></span>

- <span data-ttu-id="08a18-2469">**media_ptr**: puntatore al blocco di controllo multimediale</span><span class="sxs-lookup"><span data-stu-id="08a18-2469">**media_ptr**: Pointer to media control block</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2470">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2470">Return Values</span></span>

- <span data-ttu-id="08a18-2471">**FX_SUCCESS** (0x00) la cache multimediale riuscita è invalidata.</span><span class="sxs-lookup"><span data-stu-id="08a18-2471">**FX_SUCCESS** (0x00) Successful media cache invalidate.</span></span>
- <span data-ttu-id="08a18-2472">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2472">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2473">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2473">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2474">**FX_PTR_ERROR** (0x18) supporto non valido o puntatore a zero.</span><span class="sxs-lookup"><span data-stu-id="08a18-2474">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="08a18-2475">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2475">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2476">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2476">Allowed From</span></span>

<span data-ttu-id="08a18-2477">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2477">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2478">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2478">Example</span></span>

```c
FX_MEDIA     my_media;

/* Invalidate the cache of the media. */
status = fx_media_cache_invalidate(&my_media);

/* If status is FX_SUCCESS the cache in the media
    was successfully flushed and invalidated. */

```

### <a name="see-also"></a><span data-ttu-id="08a18-2479">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2479">See Also</span></span>

- <span data-ttu-id="08a18-2480">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2480">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2481">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2481">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2482">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2482">fx_media_check</span></span>
- <span data-ttu-id="08a18-2483">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2483">fx_media_close</span></span>
- <span data-ttu-id="08a18-2484">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2484">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2485">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2485">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2486">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2486">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2487">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2487">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2488">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2488">fx_media_format</span></span>
- <span data-ttu-id="08a18-2489">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2489">fx_media_open</span></span>
- <span data-ttu-id="08a18-2490">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2490">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2491">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2491">fx_media_read</span></span>
- <span data-ttu-id="08a18-2492">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2492">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2493">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2493">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2494">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2494">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2495">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2495">fx_media_write</span></span>
- <span data-ttu-id="08a18-2496">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2496">fx_system_initialize</span></span>

## <a name="fx_media_check"></a><span data-ttu-id="08a18-2497">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2497">fx_media_check</span></span>

<span data-ttu-id="08a18-2498">Verifica la presenza di errori nei supporti</span><span class="sxs-lookup"><span data-stu-id="08a18-2498">Checks media for errors</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2499">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2499">Prototype</span></span>

```c
UINT fx_media_check(
    FX_MEDIA *media_ptr,
    UCHAR *scratch_memory_ptr,
    ULONG scratch_memory_size,
    ULONG error_correction_option,
    ULONG *errors_detected_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-2500">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2500">Description</span></span>

<span data-ttu-id="08a18-2501">Questo servizio controlla i supporti specificati per gli errori strutturali di base, tra cui il collegamento incrociato tra file e directory, le catene FAT non valide e i cluster persi.</span><span class="sxs-lookup"><span data-stu-id="08a18-2501">This service checks the specified media for basic structural errors, including file/directory cross-linking, invalid FAT chains, and lost clusters.</span></span> <span data-ttu-id="08a18-2502">Questo servizio offre inoltre la possibilità di correggere gli errori rilevati.</span><span class="sxs-lookup"><span data-stu-id="08a18-2502">This service also provides the capability to correct detected errors.</span></span>

<span data-ttu-id="08a18-2503">Il servizio fx_media_check richiede memoria Scratch per l'analisi approfondita delle directory e dei file nel supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2503">The fx_media_check service requires scratch memory for its depth-first analysis of directories and files in the media.</span></span> <span data-ttu-id="08a18-2504">In particolare, la memoria Scratch fornita al servizio di controllo multimediale deve essere sufficientemente grande da contenere diverse voci di directory, una struttura di dati per "stack" la posizione di immissione della directory corrente prima di accedere alle sottodirectory e infine la mappa di bit logica.</span><span class="sxs-lookup"><span data-stu-id="08a18-2504">Specifically, the scratch memory supplied to the media check service must be large enough to hold several directory entries, a data structure to "stack" the current directory entry position before entering into subdirectories, and finally the logical FAT bit map.</span></span> <span data-ttu-id="08a18-2505">La memoria Scratch deve avere una lunghezza compresa tra 512-1024 byte e la memoria per la mappa di bit logica, che richiede un numero di bit quanti sono i cluster nei supporti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2505">The scratch memory should be at least 512-1024 bytes plus memory for the logical FAT bit map, which requires as many bits as there are clusters in the media.</span></span> <span data-ttu-id="08a18-2506">Ad esempio, un dispositivo con cluster 8000 richiede 1000 byte per rappresentare e quindi richiede un'area scratch totale nell'ordine di 2048 byte.</span><span class="sxs-lookup"><span data-stu-id="08a18-2506">For example, a device with 8000 clusters would require 1000 bytes to represent and thus require a total scratch area on the order of 2048 bytes.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2507">*Questo servizio deve essere chiamato solo immediatamente dopo fx_media_open e senza altre attività file system.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2507">*This service should only be called immediately after fx_media_open and without any other file system activity.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2508">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2508">Input Parameters</span></span>

- <span data-ttu-id="08a18-2509">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2509">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-2510">**scratch_memory_ptr**: puntatore all'inizio della memoria Scratch.</span><span class="sxs-lookup"><span data-stu-id="08a18-2510">**scratch_memory_ptr**: Pointer to the start of scratch memory.</span></span>
- <span data-ttu-id="08a18-2511">**scratch_memory_size**: dimensione in byte della memoria Scratch.</span><span class="sxs-lookup"><span data-stu-id="08a18-2511">**scratch_memory_size**: Size of scratch memory in bytes.</span></span>
- <span data-ttu-id="08a18-2512">**error_correction_option**: opzione Correzione errori bit, quando è impostato il bit, viene eseguita la correzione degli errori.</span><span class="sxs-lookup"><span data-stu-id="08a18-2512">**error_correction_option**: Error correction option bits, when the bit is set, error correction is performed.</span></span> <span data-ttu-id="08a18-2513">I bit delle opzioni di correzione dell'errore sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="08a18-2513">The error correction option bits are defined as follows:</span></span>
  - <span data-ttu-id="08a18-2514">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-2514">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="08a18-2515">FX_DIRECTORY_ERROR (0x02)</span><span class="sxs-lookup"><span data-stu-id="08a18-2515">FX_DIRECTORY_ERROR (0x02)</span></span>
  - <span data-ttu-id="08a18-2516">FX_LOST_CLUSTER_ERROR (0x04) semplicemente o insieme le opzioni di correzione degli errori richieste.</span><span class="sxs-lookup"><span data-stu-id="08a18-2516">FX_LOST_CLUSTER_ERROR (0x04) Simply OR together the required error correction options.</span></span> <span data-ttu-id="08a18-2517">Se non è richiesta alcuna correzione di errori, è necessario specificare un valore pari a 0.</span><span class="sxs-lookup"><span data-stu-id="08a18-2517">If no error correction is required, a value of 0 should be supplied.</span></span>
- <span data-ttu-id="08a18-2518">**errors_detected_ptr**: destinazione per i bit di rilevamento degli errori, come definito di seguito:</span><span class="sxs-lookup"><span data-stu-id="08a18-2518">**errors_detected_ptr**: Destination for error detection bits, as defined below:</span></span>
  - <span data-ttu-id="08a18-2519">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="08a18-2519">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="08a18-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span><span class="sxs-lookup"><span data-stu-id="08a18-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span></span>
  - <span data-ttu-id="08a18-2521">FX_FILE_SIZE_ERROR (0x08)</span><span class="sxs-lookup"><span data-stu-id="08a18-2521">FX_FILE_SIZE_ERROR (0x08)</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2522">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2522">Return Values</span></span>

- <span data-ttu-id="08a18-2523">**FX_SUCCESS** (0x00) controllo del supporto riuscito, visualizzare i dettagli relativi alla destinazione degli errori rilevati.</span><span class="sxs-lookup"><span data-stu-id="08a18-2523">**FX_SUCCESS** (0x00) Successful media check, view the errors detected destination for details.</span></span>
- <span data-ttu-id="08a18-2524">**FX_ACCESS_ERROR** (0x06) non è in grado di eseguire la verifica con file aperti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2524">**FX_ACCESS_ERROR** (0x06) Unable to perform check with open files.</span></span>
- <span data-ttu-id="08a18-2525">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2525">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-2526">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2526">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2527">**FX_NO_MORE_SPACE** (0X0A) non più spazio sul supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2527">**FX_NO_MORE_SPACE** (0x0A) No more space on the media.</span></span>
- <span data-ttu-id="08a18-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) non è sufficientemente grande per la memoria disponibile.</span><span class="sxs-lookup"><span data-stu-id="08a18-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) Supplied scratch memory is not large enough.</span></span>
- <span data-ttu-id="08a18-2529">**FX_ERROR_NOT_FIXED** (0x93) il danneggiamento della directory radice FAT32 che non è stato possibile risolvere.</span><span class="sxs-lookup"><span data-stu-id="08a18-2529">**FX_ERROR_NOT_FIXED** (0x93) Corruption of FAT32 root directory that could not be fixed.</span></span>
- <span data-ttu-id="08a18-2530">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2530">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2531">Il settore **FX_SECTOR_INVALID** (0x89) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2531">**FX_SECTOR_INVALID** (0x89) Sector is invalid.</span></span>
- <span data-ttu-id="08a18-2532">**FX_PTR_ERROR** (0x18) supporto non valido o puntatore a zero.</span><span class="sxs-lookup"><span data-stu-id="08a18-2532">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="08a18-2533">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2533">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="08a18-2534">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2534">Allowed From</span></span>

<span data-ttu-id="08a18-2535">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2535">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2536">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2536">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-2537">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2537">See Also</span></span>

- <span data-ttu-id="08a18-2538">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2538">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2539">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2539">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2540">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2540">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2541">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2541">fx_media_close</span></span>
- <span data-ttu-id="08a18-2542">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2542">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2543">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2543">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2544">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2544">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2545">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2545">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2546">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2546">fx_media_format</span></span>
- <span data-ttu-id="08a18-2547">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2547">fx_media_open</span></span>
- <span data-ttu-id="08a18-2548">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2548">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2549">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2549">fx_media_read</span></span>
- <span data-ttu-id="08a18-2550">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2550">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2551">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2551">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2552">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2552">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2553">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2553">fx_media_write</span></span>
- <span data-ttu-id="08a18-2554">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2554">fx_system_initialize</span></span>

## <a name="fx_media_close"></a><span data-ttu-id="08a18-2555">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2555">fx_media_close</span></span>

<span data-ttu-id="08a18-2556">Chiude i supporti</span><span class="sxs-lookup"><span data-stu-id="08a18-2556">Closes media</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2557">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2557">Prototype</span></span>

```c
UINT fx_media_close(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-2558">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2558">Description</span></span>

<span data-ttu-id="08a18-2559">Questo servizio chiude il supporto specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2559">This service closes the specified media.</span></span> <span data-ttu-id="08a18-2560">Nel processo di chiusura del supporto, tutti i file aperti vengono chiusi e tutti i buffer rimanenti vengono scaricati nei supporti fisici.</span><span class="sxs-lookup"><span data-stu-id="08a18-2560">In the process of closing the media, all open files are closed and any remaining buffers are flushed to the physical media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2561">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2561">Input Parameters</span></span>

- <span data-ttu-id="08a18-2562">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2562">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2563">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2563">Return Values</span></span>

- <span data-ttu-id="08a18-2564">Chiusura **FX_SUCCESS** (0x00) riuscita del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2564">**FX_SUCCESS** (0x00) Successful media close.</span></span>
- <span data-ttu-id="08a18-2565">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2565">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2566">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2566">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2567">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2567">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-2568">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2568">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2569">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2569">Allowed From</span></span>

<span data-ttu-id="08a18-2570">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2570">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2571">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2571">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Close "my_media". */

status = fx_media_close(&my_media);

/* If status equals FX_SUCCESS, "my_media" is closed. */

```

### <a name="see-also"></a><span data-ttu-id="08a18-2572">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2572">See Also</span></span>

- <span data-ttu-id="08a18-2573">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2573">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2574">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2574">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2575">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2575">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2576">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2576">fx_media_check</span></span>
- <span data-ttu-id="08a18-2577">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2577">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2578">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2578">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2579">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2579">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2580">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2580">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2581">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2581">fx_media_format</span></span>
- <span data-ttu-id="08a18-2582">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2582">fx_media_open</span></span>
- <span data-ttu-id="08a18-2583">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2583">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2584">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2584">fx_media_read</span></span>
- <span data-ttu-id="08a18-2585">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2585">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2586">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2586">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2587">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2587">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2588">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2588">fx_media_write</span></span>
- <span data-ttu-id="08a18-2589">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2589">fx_system_initialize</span></span>

## <a name="fx_media_close_notify_set"></a><span data-ttu-id="08a18-2590">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2590">fx_media_close_notify_set</span></span>

<span data-ttu-id="08a18-2591">Imposta la funzione media Close Notify</span><span class="sxs-lookup"><span data-stu-id="08a18-2591">Sets the media close notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2592">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2592">Prototype</span></span>

```c
UINT fx_media_close_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_close_notify)(FX_MEDIA*));
```

### <a name="description"></a><span data-ttu-id="08a18-2593">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2593">Description</span></span>

<span data-ttu-id="08a18-2594">Questo servizio imposta una funzione di callback Notify che verrà richiamata dopo che un supporto è stato chiuso correttamente.</span><span class="sxs-lookup"><span data-stu-id="08a18-2594">This service sets a notify callback function which will be invoked after a media is successfully closed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2595">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2595">Input Parameters</span></span>

- <span data-ttu-id="08a18-2596">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2596">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-2597">**media_close_notify**: è possibile installare la funzione di callback per la notifica di chiusura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2597">**media_close_notify**: Media close notify callback function to be installed.</span></span> <span data-ttu-id="08a18-2598">Il passaggio di un valore NULL come funzione di callback Disabilita il callback di chiusura multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2598">Passing NULL as the callback function disables the media close callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2599">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2599">Return Values</span></span>

- <span data-ttu-id="08a18-2600">**FX_SUCCESS** (0x00) ha installato correttamente la funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="08a18-2600">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="08a18-2601">Il media_ptr **FX_PTR_ERROR** (0x18) è null.</span><span class="sxs-lookup"><span data-stu-id="08a18-2601">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="08a18-2602">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2602">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2603">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2603">Allowed From</span></span>

<span data-ttu-id="08a18-2604">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2604">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2605">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2605">Example</span></span>

```c
fx_media_close_notify_set(media_ptr, my_media_close_callback);

```
### <a name="see-also"></a><span data-ttu-id="08a18-2606">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2606">See Also</span></span>

- <span data-ttu-id="08a18-2607">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2607">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2608">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2608">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2609">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2609">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2610">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2610">fx_media_check</span></span>
- <span data-ttu-id="08a18-2611">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2611">fx_media_close</span></span>
- <span data-ttu-id="08a18-2612">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2612">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2613">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2613">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2614">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2614">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2615">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2615">fx_media_format</span></span>
- <span data-ttu-id="08a18-2616">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2616">fx_media_open</span></span>
- <span data-ttu-id="08a18-2617">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2617">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2618">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2618">fx_media_read</span></span>
- <span data-ttu-id="08a18-2619">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2619">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2620">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2620">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2621">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2621">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2622">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2622">fx_media_write</span></span>
- <span data-ttu-id="08a18-2623">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2623">fx_system_initialize</span></span>

## <a name="fx_media_exfat_format"></a><span data-ttu-id="08a18-2624">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2624">fx_media_exFAT_format</span></span>

<span data-ttu-id="08a18-2625">Formatta i supporti</span><span class="sxs-lookup"><span data-stu-id="08a18-2625">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2626">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2626">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="08a18-2627">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2627">Description</span></span>

<span data-ttu-id="08a18-2628">Questo servizio formatta il supporto fornito in modo compatibile con exFAT in base ai parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2628">This service formats the supplied media in an exFAT compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="08a18-2629">Questo servizio deve essere chiamato prima di aprire il supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2629">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2630">*La formattazione di un supporto già formattato Cancella in modo efficace tutti i file e le directory nel supporto.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2630">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2631">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2631">Input Parameters</span></span>

- <span data-ttu-id="08a18-2632">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2632">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="08a18-2633">Viene utilizzato solo per fornire alcune informazioni di base necessarie per il funzionamento del driver.</span><span class="sxs-lookup"><span data-stu-id="08a18-2633">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="08a18-2634">**driver**: puntatore al driver di i/O per questo supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2634">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="08a18-2635">Si tratta in genere dello stesso driver fornito alla chiamata fx_media_open successiva.</span><span class="sxs-lookup"><span data-stu-id="08a18-2635">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="08a18-2636">**driver_info_ptr**: puntatore a informazioni facoltative che possono essere utilizzate dal driver di i/O.</span><span class="sxs-lookup"><span data-stu-id="08a18-2636">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="08a18-2637">**memory_ptr**: puntatore alla memoria di lavoro per il supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2637">**memory_ptr**: Pointer to the working memory for the media.</span></span> <span data-ttu-id="08a18-2638">memory_size specifica le dimensioni della memoria del supporto di lavoro.</span><span class="sxs-lookup"><span data-stu-id="08a18-2638">memory_size Specifies the size of the working media memory.</span></span> <span data-ttu-id="08a18-2639">Il valore delle dimensioni deve essere almeno uguale a quello delle dimensioni del settore del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2639">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="08a18-2640">**volume_name**: puntatore alla stringa del nome del volume, che è un massimo di 11 caratteri.</span><span class="sxs-lookup"><span data-stu-id="08a18-2640">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="08a18-2641">**number_of_fats**: numero di grassi sui supporti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2641">**number_of_fats**: Number of FATs on the media.</span></span> <span data-ttu-id="08a18-2642">L'implementazione corrente supporta un FAT sui supporti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2642">Current implementation supports one FAT on the media.</span></span>
- <span data-ttu-id="08a18-2643">**hidden_sectors**: numero di settori nascosti prima del settore di avvio del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2643">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="08a18-2644">Questo è tipico quando sono presenti più partizioni.</span><span class="sxs-lookup"><span data-stu-id="08a18-2644">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="08a18-2645">**total_sectors**: numero totale di settori nel supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2645">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="08a18-2646">**bytes_per_sector**: numero di byte per settore, che in genere è 512.</span><span class="sxs-lookup"><span data-stu-id="08a18-2646">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="08a18-2647">FileX richiede un multiplo di 32.</span><span class="sxs-lookup"><span data-stu-id="08a18-2647">FileX requires this to be a multiple of 32.</span></span>
- <span data-ttu-id="08a18-2648">**sectors_per_cluster**: numero di settori in ogni cluster.</span><span class="sxs-lookup"><span data-stu-id="08a18-2648">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="08a18-2649">Il cluster è l'unità di allocazione minima in un file system FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2649">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="08a18-2650">**volumne_serial_number**: numero di serie da usare per il volume.</span><span class="sxs-lookup"><span data-stu-id="08a18-2650">**volumne_serial_number**: Serial number to be used for this volume.</span></span>
- <span data-ttu-id="08a18-2651">**boundary_unit**: dimensioni di allineamento dell'area dati fisica, in numero di settori.</span><span class="sxs-lookup"><span data-stu-id="08a18-2651">**boundary_unit**: Physical data area alignment size, in number of sectors.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2652">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2652">Return Values</span></span>

- <span data-ttu-id="08a18-2653">**FX_SUCCESS** (0x00) il formato dei supporti riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2653">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="08a18-2654">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2654">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2655">**FX_PTR_ERROR** (0x18) supporto non valido, driver o puntatore di memoria.</span><span class="sxs-lookup"><span data-stu-id="08a18-2655">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="08a18-2656">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2656">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2657">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2657">Allowed From</span></span>

<span data-ttu-id="08a18-2658">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2658">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2659">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2659">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-2660">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2660">See Also</span></span>

- <span data-ttu-id="08a18-2661">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2661">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2662">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2662">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2663">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2663">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2664">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2664">fx_media_check</span></span>
- <span data-ttu-id="08a18-2665">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2665">fx_media_close</span></span>
- <span data-ttu-id="08a18-2666">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2666">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2667">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2667">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2668">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2668">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2669">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2669">fx_media_format</span></span>
- <span data-ttu-id="08a18-2670">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2670">fx_media_open</span></span>
- <span data-ttu-id="08a18-2671">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2671">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2672">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2672">fx_media_read</span></span>
- <span data-ttu-id="08a18-2673">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2673">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2674">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2674">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2675">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2675">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2676">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2676">fx_media_write</span></span>
- <span data-ttu-id="08a18-2677">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2677">fx_system_initialize</span></span>

## <a name="fx_media_extended_space_available"></a><span data-ttu-id="08a18-2678">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2678">fx_media_extended_space_available</span></span>

<span data-ttu-id="08a18-2679">Restituisce lo spazio multimediale disponibile</span><span class="sxs-lookup"><span data-stu-id="08a18-2679">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2680">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2680">Prototype</span></span>

```c
UINT fx_media_extended_space_available(
    FX_MEDIA *media_ptr,
    ULONG64 *available_bytes_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-2681">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2681">Description</span></span>

<span data-ttu-id="08a18-2682">Questo servizio restituisce il numero di byte disponibili nel supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2682">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="08a18-2683">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2683">This service is designed for exFAT.</span></span> <span data-ttu-id="08a18-2684">Il puntatore al parametro *available_bytes* accetta un valore integer a 64 bit, che consente al chiamante di lavorare con supporti oltre i 4 GB.</span><span class="sxs-lookup"><span data-stu-id="08a18-2684">The pointer to *available_bytes* parameter takes a 64-bit integer value, which allows the caller to work with media beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2685">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2685">Input Parameters</span></span>

- <span data-ttu-id="08a18-2686">**media_ptr**: puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-2686">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="08a18-2687">**available_bytes_ptr**: byte disponibili rimasti nei supporti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2687">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2688">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2688">Return Values</span></span>

- <span data-ttu-id="08a18-2689">**FX_SUCCESS** (0x00) ha recuperato lo spazio disponibile sul supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2689">**FX_SUCCESS** (0x00) Successfully retrieved space available on the media.</span></span>
- <span data-ttu-id="08a18-2690">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2690">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2691">**FX_PTR_ERROR** (0x18) il puntatore multimediale non valido o il puntatore byte disponibili è null.</span><span class="sxs-lookup"><span data-stu-id="08a18-2691">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="08a18-2692">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2692">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2693">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2693">Allowed From</span></span>

<span data-ttu-id="08a18-2694">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2694">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2695">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2695">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG64            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_extended_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="08a18-2696">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2696">See Also</span></span>

- <span data-ttu-id="08a18-2697">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2697">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2698">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2698">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2699">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2699">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2700">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2700">fx_media_check</span></span>
- <span data-ttu-id="08a18-2701">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2701">fx_media_close</span></span>
- <span data-ttu-id="08a18-2702">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2702">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2703">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2703">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2704">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2704">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2705">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2705">fx_media_format</span></span>
- <span data-ttu-id="08a18-2706">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2706">fx_media_open</span></span>
- <span data-ttu-id="08a18-2707">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2707">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2708">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2708">fx_media_read</span></span>
- <span data-ttu-id="08a18-2709">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2709">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2710">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2710">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2711">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2711">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2712">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2712">fx_media_write</span></span>
- <span data-ttu-id="08a18-2713">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2713">fx_system_initialize</span></span>

## <a name="fx_media_flush"></a><span data-ttu-id="08a18-2714">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2714">fx_media_flush</span></span>

<span data-ttu-id="08a18-2715">Scarica i dati in un supporto fisico</span><span class="sxs-lookup"><span data-stu-id="08a18-2715">Flushes data to physical media</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2716">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2716">Prototype</span></span>

```c
UINT fx_media_flush(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-2717">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2717">Description</span></span>

<span data-ttu-id="08a18-2718">Questo servizio Scarica tutti i settori memorizzati nella cache e le voci di directory dei file modificati nei supporti fisici.</span><span class="sxs-lookup"><span data-stu-id="08a18-2718">This service flushes all cached sectors and directory entries of any modified files to the physical media.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2719">*Questa routine può essere chiamata periodicamente dall'applicazione per ridurre il rischio di danneggiamento dei file e/o la perdita di dati in caso di un'improvvisa interruzione dell'alimentazione sulla destinazione.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2719">*This routine may be called periodically by the application to reduce the risk of file corruption and/or data loss in the event of a sudden loss of power on the target.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2720">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2720">Input Parameters</span></span>

- <span data-ttu-id="08a18-2721">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2721">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2722">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2722">Return Values</span></span>

- <span data-ttu-id="08a18-2723">**FX_SUCCESS** (0x00) lo svuotamento multimediale è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2723">**FX_SUCCESS** (0x00) Successful media flush.</span></span>
- <span data-ttu-id="08a18-2724">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2724">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2725">Il file **FX_FILE_CORRUPT** (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="08a18-2725">**FX_FILE_CORRUPT**    (0x08) File is corrupted.</span></span>
- <span data-ttu-id="08a18-2726">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2726">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-2727">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2727">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2728">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-2728">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-2729">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2729">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-2730">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2730">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2731">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2731">Allowed From</span></span>

<span data-ttu-id="08a18-2732">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2732">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2733">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2733">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Flush all cached sectors and modified file entries to the physical media. */

status = fx_media_flush(&my_media);

/* If status equals FX_SUCCESS, the physical media is completely up-to-date. */

```

### <a name="see-also"></a><span data-ttu-id="08a18-2734">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2734">See Also</span></span>

- <span data-ttu-id="08a18-2735">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2735">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2736">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2736">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2737">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2737">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2738">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2738">fx_media_check</span></span>
- <span data-ttu-id="08a18-2739">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2739">fx_media_close</span></span>
- <span data-ttu-id="08a18-2740">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2740">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2741">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2741">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2742">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2742">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2743">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2743">fx_media_format</span></span>
- <span data-ttu-id="08a18-2744">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2744">fx_media_open</span></span>
- <span data-ttu-id="08a18-2745">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2745">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2746">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2746">fx_media_read</span></span>
- <span data-ttu-id="08a18-2747">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2747">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2748">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2748">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2749">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2749">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2750">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2750">fx_media_write</span></span>
- <span data-ttu-id="08a18-2751">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2751">fx_system_initialize</span></span>

## <a name="fx_media_format"></a><span data-ttu-id="08a18-2752">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2752">fx_media_format</span></span>

<span data-ttu-id="08a18-2753">Formatta i supporti</span><span class="sxs-lookup"><span data-stu-id="08a18-2753">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2754">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2754">Prototype</span></span>

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
### <a name="description"></a><span data-ttu-id="08a18-2755">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2755">Description</span></span>

<span data-ttu-id="08a18-2756">Questo servizio formatta il supporto fornito in un modo compatibile con FAT 12/16/32 in base ai parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2756">This service formats the supplied media in a FAT 12/16/32 compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="08a18-2757">Questo servizio deve essere chiamato prima di aprire il supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2757">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2758">*La formattazione di un supporto già formattato Cancella in modo efficace tutti i file e le directory nel supporto.*</span><span class="sxs-lookup"><span data-stu-id="08a18-2758">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2759">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2759">Input Parameters</span></span>

- <span data-ttu-id="08a18-2760">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2760">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="08a18-2761">Viene utilizzato solo per fornire alcune informazioni di base necessarie per il funzionamento del driver.</span><span class="sxs-lookup"><span data-stu-id="08a18-2761">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="08a18-2762">**driver**: puntatore al driver di i/O per questo supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2762">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="08a18-2763">Si tratta in genere dello stesso driver fornito alla chiamata fx_media_open successiva.</span><span class="sxs-lookup"><span data-stu-id="08a18-2763">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="08a18-2764">**driver_info_ptr**: puntatore a informazioni facoltative che possono essere utilizzate dal driver di i/O.</span><span class="sxs-lookup"><span data-stu-id="08a18-2764">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="08a18-2765">**memory_ptr**: puntatore alla memoria di lavoro per il supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2765">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="08a18-2766">**memory_size**: specifica le dimensioni della memoria del supporto di lavoro.</span><span class="sxs-lookup"><span data-stu-id="08a18-2766">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="08a18-2767">Il valore delle dimensioni deve essere almeno uguale a quello delle dimensioni del settore del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2767">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="08a18-2768">**volume_name**: puntatore alla stringa del nome del volume, che è un massimo di 11 caratteri.</span><span class="sxs-lookup"><span data-stu-id="08a18-2768">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="08a18-2769">**number_of_fats**: numero di grassi nei supporti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2769">**number_of_fats**: Number of FATs in the media.</span></span> <span data-ttu-id="08a18-2770">Il valore minimo è 1 per il FAT primario.</span><span class="sxs-lookup"><span data-stu-id="08a18-2770">The minimal value is 1 for the primary FAT.</span></span> <span data-ttu-id="08a18-2771">I valori maggiori di 1 comportano il mantenimento di copie FAT aggiuntive in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="08a18-2771">Values greater than 1 result in additional FAT copies being maintained at run-time.</span></span>
- <span data-ttu-id="08a18-2772">**directory_entries**: numero di voci di directory nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="08a18-2772">**directory_entries**: Number of directory entries in the root directory.</span></span>
- <span data-ttu-id="08a18-2773">**hidden_sectors**: numero di settori nascosti prima del settore di avvio del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2773">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="08a18-2774">Questo è tipico quando sono presenti più partizioni.</span><span class="sxs-lookup"><span data-stu-id="08a18-2774">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="08a18-2775">**total_sectors**: numero totale di settori nel supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2775">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="08a18-2776">**bytes_per_sector**: numero di byte per settore, che in genere è 512.</span><span class="sxs-lookup"><span data-stu-id="08a18-2776">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="08a18-2777">FileX richiede un multiplo di 32.</span><span class="sxs-lookup"><span data-stu-id="08a18-2777">FileX requires this to be a multiple of 32.</span></span>
- <span data-ttu-id="08a18-2778">**sectors_per_cluster**: numero di settori in ogni cluster.</span><span class="sxs-lookup"><span data-stu-id="08a18-2778">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="08a18-2779">Il cluster è l'unità di allocazione minima in un file system FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2779">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="08a18-2780">**Heads**: numero di testine fisiche.</span><span class="sxs-lookup"><span data-stu-id="08a18-2780">**heads**: Number of physical heads.</span></span>
- <span data-ttu-id="08a18-2781">**sectors_per_track**: numero di settori per traccia.</span><span class="sxs-lookup"><span data-stu-id="08a18-2781">**sectors_per_track**: Number of sectors per track.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2782">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2782">Return Values</span></span>

- <span data-ttu-id="08a18-2783">**FX_SUCCESS** (0x00) il formato dei supporti riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2783">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="08a18-2784">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2784">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2785">**FX_PTR_ERROR** (0x18) supporto non valido, driver o puntatore di memoria.</span><span class="sxs-lookup"><span data-stu-id="08a18-2785">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="08a18-2786">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2786">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2787">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2787">Allowed From</span></span>

<span data-ttu-id="08a18-2788">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2788">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2789">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2789">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-2790">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2790">See Also</span></span>

- <span data-ttu-id="08a18-2791">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2791">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2792">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2792">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2793">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2793">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2794">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2794">fx_media_check</span></span>
- <span data-ttu-id="08a18-2795">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2795">fx_media_close</span></span>
- <span data-ttu-id="08a18-2796">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2796">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2797">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2797">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2798">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2798">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2799">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2799">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2800">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2800">fx_media_open</span></span>
- <span data-ttu-id="08a18-2801">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2801">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2802">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2802">fx_media_read</span></span>
- <span data-ttu-id="08a18-2803">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2803">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2804">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2804">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2805">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2805">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2806">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2806">fx_media_write</span></span>
- <span data-ttu-id="08a18-2807">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2807">fx_system_initialize</span></span>

## <a name="fx_media_open"></a><span data-ttu-id="08a18-2808">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2808">fx_media_open</span></span>

<span data-ttu-id="08a18-2809">Apre i supporti per l'accesso ai file</span><span class="sxs-lookup"><span data-stu-id="08a18-2809">Opens media for file access</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2810">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2810">Prototype</span></span>

```c
UINT fx_media_open(
    FX_MEDIA *media_ptr, 
    CHAR *media_name,
    VOID(*media_driver)(FX_MEDIA *),
    VOID *driver_info_ptr,
    VOID *memory_ptr, 
    ULONG memory_size);
```
### <a name="description"></a><span data-ttu-id="08a18-2811">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2811">Description</span></span>

<span data-ttu-id="08a18-2812">Questo servizio apre un supporto per l'accesso ai file tramite il driver I/O fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2812">This service opens a media for file access using the supplied I/O driver.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-2813">*La memoria fornita a questo servizio viene utilizzata per implementare una cache di settore logico interna, di conseguenza, maggiore è la quantità di memoria fornita, il numero maggiore di I/O fisico è ridotto. FileX richiede una cache di almeno un settore logico (byte per settore del supporto).*</span><span class="sxs-lookup"><span data-stu-id="08a18-2813">*The memory supplied to this service is used to implement an internal logical sector cache, hence, the more memory supplied the more physical I/O is reduced. FileX requires a cache of at least one logical sector (bytes per sector of the media).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2814">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2814">Input Parameters</span></span>

- <span data-ttu-id="08a18-2815">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2815">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-2816">**media_name**: puntatore al nome del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2816">**media_name**: Pointer to media's name.</span></span>
- <span data-ttu-id="08a18-2817">**media_driver**: puntatore al driver I/O per questo supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2817">**media_driver**: Pointer to I/O driver for this media.</span></span> <span data-ttu-id="08a18-2818">Il driver I/O deve essere conforme ai requisiti del driver FileX definiti nel capitolo 5.</span><span class="sxs-lookup"><span data-stu-id="08a18-2818">The I/O driver must conform to FileX driver requirements defined in Chapter 5.</span></span>
- <span data-ttu-id="08a18-2819">**driver_info_ptr**: puntatore a informazioni facoltative che il driver di i/O fornito può utilizzare.</span><span class="sxs-lookup"><span data-stu-id="08a18-2819">**driver_info_ptr**: Pointer to optional information that the supplied I/O driver may utilize.</span></span>
- <span data-ttu-id="08a18-2820">**memory_ptr**: puntatore alla memoria di lavoro per il supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2820">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="08a18-2821">**memory_size**: specifica le dimensioni della memoria del supporto di lavoro.</span><span class="sxs-lookup"><span data-stu-id="08a18-2821">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="08a18-2822">Il valore delle dimensioni deve essere pari a quello delle dimensioni del settore del supporto (in genere 512 byte).</span><span class="sxs-lookup"><span data-stu-id="08a18-2822">The size must be as large as the media's sector size (typically 512 bytes).</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2823">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2823">Return Values</span></span>

- <span data-ttu-id="08a18-2824">Apertura del supporto **FX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="08a18-2824">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="08a18-2825">Errore **FX_BOOT_ERROR** (0x01) durante la lettura del settore di avvio del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2825">**FX_BOOT_ERROR** (0x01) Error reading the media's boot sector.</span></span>
- <span data-ttu-id="08a18-2826">**FX_MEDIA_INVALID** (0x02) il settore di avvio del supporto specificato è danneggiato o non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2826">**FX_MEDIA_INVALID** (0x02) Specified media's boot sector is corrupt or invalid.</span></span> <span data-ttu-id="08a18-2827">Inoltre, questo codice restituito viene utilizzato per indicare che la dimensione della cache del settore logico o la dimensione della voce FAT non è una potenza di 2.</span><span class="sxs-lookup"><span data-stu-id="08a18-2827">In addition, this return code is used to indicate that either the logical sector cache size or the FAT entry size is not a power of 2.</span></span>
- <span data-ttu-id="08a18-2828">Errore **FX_FAT_READ_ERROR** (0X03) durante la lettura del file multimediale FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-2828">**FX_FAT_READ_ERROR** (0x03) Error reading the media FAT.</span></span>
- <span data-ttu-id="08a18-2829">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2829">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2830">**FX_PTR_ERROR** (0x18) uno o più puntatori sono null.</span><span class="sxs-lookup"><span data-stu-id="08a18-2830">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="08a18-2831">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2831">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2832">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2832">Allowed From</span></span>

<span data-ttu-id="08a18-2833">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2833">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2834">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2834">Example</span></span>

```c
FX_MEDIA         ram_disk,
UINT             status;
UCHAR             buffer[128];
/* Open a 32KByte RAM disk starting at the fixed address of 0x800000.
    Note that the total 32KByte media size and 128-byte sector size is defined inside of the driver. */

status = fx_media_open(&ram_disk, "RAM DISK", fx_ram_driver, 0, &buffer[0], sizeof(buffer));

/* If status equals FX_SUCCESS, the RAM disk has been successfully setup and is ready for file access! */

```

### <a name="see-also"></a><span data-ttu-id="08a18-2835">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2835">See Also</span></span>

- <span data-ttu-id="08a18-2836">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2836">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2837">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2837">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2838">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2838">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2839">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2839">fx_media_check</span></span>
- <span data-ttu-id="08a18-2840">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2840">fx_media_close</span></span>
- <span data-ttu-id="08a18-2841">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2841">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2842">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2842">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2843">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2843">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2844">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2844">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2845">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2845">fx_media_format</span></span>
- <span data-ttu-id="08a18-2846">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2846">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2847">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2847">fx_media_read</span></span>
- <span data-ttu-id="08a18-2848">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2848">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2849">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2849">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2850">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2850">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2851">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2851">fx_media_write</span></span>
- <span data-ttu-id="08a18-2852">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2852">fx_system_initialize</span></span>

## <a name="fx_media_open_notify_set"></a><span data-ttu-id="08a18-2853">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2853">fx_media_open_notify_set</span></span>

<span data-ttu-id="08a18-2854">Imposta la funzione Media Open Notify</span><span class="sxs-lookup"><span data-stu-id="08a18-2854">Sets the media open notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2855">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2855">Prototype</span></span>

```c
UINT fx_media_open_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_open_notify)(FX_MEDIA*));
```
### <a name="description"></a><span data-ttu-id="08a18-2856">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2856">Description</span></span>

<span data-ttu-id="08a18-2857">Questo servizio imposta una funzione di callback Notify che verrà richiamata dopo l'apertura corretta di un supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2857">This service sets a notify callback function which will be invoked after a media is successfully opened.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2858">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2858">Input Parameters</span></span>

- <span data-ttu-id="08a18-2859">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2859">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-2860">**media_open_notify**: è possibile installare la funzione di callback per la notifica di comunicazione aperta.</span><span class="sxs-lookup"><span data-stu-id="08a18-2860">**media_open_notify**: Media open notify callback function to be installed.</span></span> <span data-ttu-id="08a18-2861">Il passaggio di un valore NULL come funzione di callback Disabilita il callback aperto del supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2861">Passing NULL as the callback function disables the media open callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2862">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2862">Return Values</span></span>


- <span data-ttu-id="08a18-2863">**FX_SUCCESS** (0x00) ha installato correttamente la funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="08a18-2863">**FX_SUCCESS** (0x00) Successfuly installed the callback function.</span></span>
- <span data-ttu-id="08a18-2864">Il media_ptr **FX_PTR_ERROR** (0x18) è null.</span><span class="sxs-lookup"><span data-stu-id="08a18-2864">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="08a18-2865">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2865">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2866">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2866">Allowed From</span></span>

<span data-ttu-id="08a18-2867">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2867">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2868">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2868">Example</span></span>

```c
fx_media_open_notify_set(media_ptr, my_media_open_callback);

```

### <a name="see-also"></a><span data-ttu-id="08a18-2869">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2869">See Also</span></span>

- <span data-ttu-id="08a18-2870">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2870">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2871">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2871">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2872">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2872">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2873">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2873">fx_media_check</span></span>
- <span data-ttu-id="08a18-2874">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2874">fx_media_close</span></span>
- <span data-ttu-id="08a18-2875">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2875">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2876">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2876">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2877">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2877">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2878">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2878">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2879">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2879">fx_media_format</span></span>
- <span data-ttu-id="08a18-2880">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2880">fx_media_open</span></span>
- <span data-ttu-id="08a18-2881">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2881">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2882">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2882">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2883">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2883">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2884">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2884">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2885">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2885">fx_media_write</span></span>
- <span data-ttu-id="08a18-2886">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2886">fx_system_initialize</span></span>

## <a name="fx_media_read"></a><span data-ttu-id="08a18-2887">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2887">fx_media_read</span></span>

<span data-ttu-id="08a18-2888">Legge il settore logico dal supporto</span><span class="sxs-lookup"><span data-stu-id="08a18-2888">Reads logical sector from media</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2889">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2889">Prototype</span></span>

```c
UINT fx_media_read(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector, 
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-2890">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2890">Description</span></span>

<span data-ttu-id="08a18-2891">Questo servizio legge un settore logico dal supporto e lo inserisce nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2891">This service reads a logical sector from the media and places it into the supplied buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2892">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2892">Input Parameters</span></span>

- <span data-ttu-id="08a18-2893">**media_ptr**: puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-2893">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="08a18-2894">**logical_sector**: settore logico da leggere.</span><span class="sxs-lookup"><span data-stu-id="08a18-2894">**logical_sector**: Logical sector to read.</span></span>
- <span data-ttu-id="08a18-2895">**buffer_ptr**: puntatore alla destinazione per la lettura del settore logico.</span><span class="sxs-lookup"><span data-stu-id="08a18-2895">**buffer_ptr**: Pointer to the destination for the logical sector read.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2896">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2896">Return Values</span></span>

- <span data-ttu-id="08a18-2897">**FX_SUCCESS** (0x00) lettura del supporto riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-2897">**FX_SUCCESS** (0x00) Successful media read.</span></span>
- <span data-ttu-id="08a18-2898">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2898">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2899">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2899">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2900">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2900">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-2901">Il puntatore del buffer o del supporto **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2901">**FX_PTR_ERROR** (0x18) Invalid media or buffer pointer.</span></span>
- <span data-ttu-id="08a18-2902">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2902">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2903">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2903">Allowed From</span></span>

<span data-ttu-id="08a18-2904">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2904">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2905">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2905">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_buffer[128];
UINT            STATUS;
/* Read logical sector 22 into "my_buffer" assuming the
    physical media has a sector size of 128. */
status = fx_media_read(&my_media, 22, my_buffer);
/* If status equals FX_SUCCESS, the contents of logical sector 22 are in "my_buffer". */
```

### <a name="see-also"></a><span data-ttu-id="08a18-2906">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2906">See Also</span></span>

- <span data-ttu-id="08a18-2907">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2907">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2908">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2908">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2909">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2909">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2910">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2910">fx_media_check</span></span>
- <span data-ttu-id="08a18-2911">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2911">fx_media_close</span></span>
- <span data-ttu-id="08a18-2912">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2912">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2913">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2913">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2914">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2914">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2915">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2915">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2916">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2916">fx_media_format</span></span>
- <span data-ttu-id="08a18-2917">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2917">fx_media_open</span></span>
- <span data-ttu-id="08a18-2918">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2918">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2919">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2919">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2920">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2920">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2921">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2921">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2922">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2922">fx_media_write</span></span>
- <span data-ttu-id="08a18-2923">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2923">fx_system_initialize</span></span>

## <a name="fx_media_space_available"></a><span data-ttu-id="08a18-2924">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2924">fx_media_space_available</span></span>

<span data-ttu-id="08a18-2925">Restituisce lo spazio multimediale disponibile</span><span class="sxs-lookup"><span data-stu-id="08a18-2925">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2926">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2926">Prototype</span></span>

```c
UINT fx_media_space_available(
    FX_MEDIA *media_ptr,
    ULONG *available_bytes_ptr);
```

### <a name="description"></a><span data-ttu-id="08a18-2927">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2927">Description</span></span>

<span data-ttu-id="08a18-2928">Questo servizio restituisce il numero di byte disponibili nel supporto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2928">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="08a18-2929">Per lavorare con i supporti di dimensioni superiori a 4 GB, l'applicazione deve usare il servizio *fx_media_extended_space_available*.</span><span class="sxs-lookup"><span data-stu-id="08a18-2929">To work with the media larger than 4GB, application shall use the service *fx_media_extended_space_available*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2930">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2930">Input Parameters</span></span>

- <span data-ttu-id="08a18-2931">**media_ptr**: puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-2931">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="08a18-2932">**available_bytes_ptr**: byte disponibili rimasti nei supporti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2932">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2933">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2933">Return Values</span></span>

- <span data-ttu-id="08a18-2934">**FX_SUCCESS** (0x00) ha restituito lo spazio disponibile nei supporti.</span><span class="sxs-lookup"><span data-stu-id="08a18-2934">**FX_SUCCESS** (0x00) Successfully returned available space on media.</span></span>
- <span data-ttu-id="08a18-2935">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2935">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2936">**FX_PTR_ERROR** (0x18) il puntatore multimediale non valido o il puntatore byte disponibili è null.</span><span class="sxs-lookup"><span data-stu-id="08a18-2936">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="08a18-2937">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2937">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2938">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2938">Allowed From</span></span>

<span data-ttu-id="08a18-2939">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2939">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2940">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2940">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="08a18-2941">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2941">See Also</span></span>

- <span data-ttu-id="08a18-2942">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2942">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2943">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2943">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2944">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2944">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2945">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2945">fx_media_check</span></span>
- <span data-ttu-id="08a18-2946">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2946">fx_media_close</span></span>
- <span data-ttu-id="08a18-2947">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2947">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2948">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2948">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2949">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2949">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2950">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2950">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2951">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2951">fx_media_format</span></span>
- <span data-ttu-id="08a18-2952">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2952">fx_media_open</span></span>
- <span data-ttu-id="08a18-2953">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2953">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2954">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2954">fx_media_read</span></span>
- <span data-ttu-id="08a18-2955">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2955">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-2956">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2956">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2957">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2957">fx_media_write</span></span>
- <span data-ttu-id="08a18-2958">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2958">fx_system_initialize</span></span>

## <a name="fx_media_volume_get"></a><span data-ttu-id="08a18-2959">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-2959">fx_media_volume_get</span></span>

<span data-ttu-id="08a18-2960">Ottiene il nome del volume multimediale</span><span class="sxs-lookup"><span data-stu-id="08a18-2960">Gets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-2961">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-2961">Prototype</span></span>

```c
UINT fx_media_volume_get(
    FX_MEDIA *media_ptr,
    CHAR *volume_name,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="08a18-2962">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-2962">Description</span></span>

<span data-ttu-id="08a18-2963">Questo servizio recupera il nome del volume del supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-2963">This service retrieves the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-2964">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-2964">Input Parameters</span></span>

- <span data-ttu-id="08a18-2965">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-2965">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-2966">**volume_name**: puntatore alla destinazione per il nome del volume.</span><span class="sxs-lookup"><span data-stu-id="08a18-2966">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="08a18-2967">Si noti che la destinazione deve essere almeno sufficientemente grande da contenere 12 caratteri.</span><span class="sxs-lookup"><span data-stu-id="08a18-2967">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="08a18-2968">**volume_source**: indica la posizione in cui recuperare il nome, dal settore di avvio o dalla directory radice.</span><span class="sxs-lookup"><span data-stu-id="08a18-2968">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="08a18-2969">I valori validi per questo parametro sono:</span><span class="sxs-lookup"><span data-stu-id="08a18-2969">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="08a18-2970">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="08a18-2970">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="08a18-2971">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="08a18-2971">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-2972">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-2972">Return Values</span></span>

- <span data-ttu-id="08a18-2973">**FX_SUCCESS** (0x00) volume di supporti riusciti Get.</span><span class="sxs-lookup"><span data-stu-id="08a18-2973">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="08a18-2974">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-2974">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-2975">Impossibile trovare il volume **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-2975">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="08a18-2976">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-2976">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-2977">**FX_PTR_ERROR** (0x18) il puntatore di destinazione del volume o del supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-2977">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="08a18-2978">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-2978">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-2979">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-2979">Allowed From</span></span>

<span data-ttu-id="08a18-2980">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-2980">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-2981">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-2981">Example</span></span>

```c
FX_MEDIA        ram_disk;
UCHAR             volume_name[12];
/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name), FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */

```

### <a name="see-also"></a><span data-ttu-id="08a18-2982">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-2982">See Also</span></span>

- <span data-ttu-id="08a18-2983">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-2983">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-2984">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-2984">fx_media_abort</span></span>
- <span data-ttu-id="08a18-2985">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-2985">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-2986">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-2986">fx_media_check</span></span>
- <span data-ttu-id="08a18-2987">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-2987">fx_media_close</span></span>
- <span data-ttu-id="08a18-2988">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2988">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-2989">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2989">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-2990">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2990">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-2991">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-2991">fx_media_flush</span></span>
- <span data-ttu-id="08a18-2992">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-2992">fx_media_format</span></span>
- <span data-ttu-id="08a18-2993">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-2993">fx_media_open</span></span>
- <span data-ttu-id="08a18-2994">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2994">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-2995">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-2995">fx_media_read</span></span>
- <span data-ttu-id="08a18-2996">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-2996">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-2997">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-2997">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-2998">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-2998">fx_media_write</span></span>
- <span data-ttu-id="08a18-2999">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-2999">fx_system_initialize</span></span>

## <a name="fx_media_volume_get_extended"></a><span data-ttu-id="08a18-3000">fx_media_volume_get_extended</span><span class="sxs-lookup"><span data-stu-id="08a18-3000">fx_media_volume_get_extended</span></span>

<span data-ttu-id="08a18-3001">Ottiene il nome del volume multimediale del supporto aperto in precedenza</span><span class="sxs-lookup"><span data-stu-id="08a18-3001">Gets media volume name of previously opened media</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3002">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3002">Prototype</span></span>

```c
UINT fx_media_volume_get_extended(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name,
    UINT volume_name_buffer_length,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="08a18-3003">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3003">Description</span></span>

<span data-ttu-id="08a18-3004">Questo servizio recupera il nome del volume del supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-3004">This service retrieves the volume name of the previously opened media.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3005">Questo servizio è identico a \***fx_media_volume_get ()** _ ad eccezione del fatto che il chiamante passa alla dimensione del buffer _ \*volume_name\*\*.</span><span class="sxs-lookup"><span data-stu-id="08a18-3005">This service is identical to ***fx_media_volume_get()** _ except the caller passes in the size of the _ *volume_name** buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3006">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3006">Input Parameters</span></span>


- <span data-ttu-id="08a18-3007">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3007">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3008">**volume_name**: puntatore alla destinazione per il nome del volume.</span><span class="sxs-lookup"><span data-stu-id="08a18-3008">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="08a18-3009">Si noti che la destinazione deve essere almeno sufficientemente grande da contenere 12 caratteri.</span><span class="sxs-lookup"><span data-stu-id="08a18-3009">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="08a18-3010">**volume_name_buffer_length**: dimensione del buffer di volume_name.</span><span class="sxs-lookup"><span data-stu-id="08a18-3010">**volume_name_buffer_length**: Size of volume_name buffer.</span></span>
- <span data-ttu-id="08a18-3011">**volume_source**: indica la posizione in cui recuperare il nome, dal settore di avvio o dalla directory radice.</span><span class="sxs-lookup"><span data-stu-id="08a18-3011">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="08a18-3012">I valori validi per questo parametro sono:</span><span class="sxs-lookup"><span data-stu-id="08a18-3012">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="08a18-3013">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="08a18-3013">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="08a18-3014">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="08a18-3014">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3015">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3015">Return Values</span></span>

- <span data-ttu-id="08a18-3016">**FX_SUCCESS** (0x00) volume di supporti riusciti Get.</span><span class="sxs-lookup"><span data-stu-id="08a18-3016">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="08a18-3017">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3017">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3018">Impossibile trovare il volume **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-3018">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="08a18-3019">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3019">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3020">**FX_PTR_ERROR** (0x18) il puntatore di destinazione del volume o del supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3020">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="08a18-3021">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3021">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3022">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3022">Allowed From</span></span>

<span data-ttu-id="08a18-3023">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3023">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3024">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3024">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             volume_name[12];

/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name),
                                      FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-3025">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3025">See Also</span></span>

- <span data-ttu-id="08a18-3026">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-3026">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-3027">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-3027">fx_media_abort</span></span>
- <span data-ttu-id="08a18-3028">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-3028">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-3029">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-3029">fx_media_check</span></span>
- <span data-ttu-id="08a18-3030">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3030">fx_media_close</span></span>
- <span data-ttu-id="08a18-3031">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3031">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-3032">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-3032">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-3033">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-3033">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-3034">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-3034">fx_media_flush</span></span>
- <span data-ttu-id="08a18-3035">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-3035">fx_media_format</span></span>
- <span data-ttu-id="08a18-3036">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3036">fx_media_open</span></span>
- <span data-ttu-id="08a18-3037">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3037">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-3038">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3038">fx_media_read</span></span>
- <span data-ttu-id="08a18-3039">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-3039">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-3040">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3040">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-3041">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3041">fx_media_write</span></span>
- <span data-ttu-id="08a18-3042">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-3042">fx_system_initialize</span></span>

## <a name="fx_media_volume_set"></a><span data-ttu-id="08a18-3043">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3043">fx_media_volume_set</span></span>

<span data-ttu-id="08a18-3044">Imposta il nome del volume multimediale</span><span class="sxs-lookup"><span data-stu-id="08a18-3044">Sets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3045">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3045">Prototype</span></span>

```c
UINT fx_media_volume_set(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name);
```
### <a name="description"></a><span data-ttu-id="08a18-3046">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3046">Description</span></span>

<span data-ttu-id="08a18-3047">Questo servizio imposta il nome del volume del supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-3047">This service sets the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3048">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3048">Input Parameters</span></span>

- <span data-ttu-id="08a18-3049">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3049">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3050">**volume_name**: puntatore al nome del volume.</span><span class="sxs-lookup"><span data-stu-id="08a18-3050">**volume_name**: Pointer to the volume name.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3051">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3051">Return Values</span></span>

- <span data-ttu-id="08a18-3052">**FX_SUCCESS** (0x00) set di volumi multimediali riusciti.</span><span class="sxs-lookup"><span data-stu-id="08a18-3052">**FX_SUCCESS** (0x00) Successful media volume set.</span></span>
- <span data-ttu-id="08a18-3053">Il Volume_name **FX_INVALID_NAME** (0x0C) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3053">**FX_INVALID_NAME** (0x0C) Volume_name is invalid.</span></span>
- <span data-ttu-id="08a18-3054">**FX_MEDIA_INVALID** (0x02) non è in grado di impostare il nome del volume.</span><span class="sxs-lookup"><span data-stu-id="08a18-3054">**FX_MEDIA_INVALID** (0x02) Unable to set volume name.</span></span>
- <span data-ttu-id="08a18-3055">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3055">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3056">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3056">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3057">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-3057">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-3058">Il puntatore del nome del volume o del supporto **FX_PTR_ERROR** (0x18) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3058">**FX_PTR_ERROR** (0x18) Invalid media or volume name pointer.</span></span>
- <span data-ttu-id="08a18-3059">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3059">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3060">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3060">Allowed From</span></span>

<span data-ttu-id="08a18-3061">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3061">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3062">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3062">Example</span></span>

```c
FX_MEDIA ram_disk;

/* Set the volume name to "MY_VOLUME". */

status = fx_media_volume_set(&ram_disk, "MY_VOLUME");

/* If status is FX_SUCCESS, the volume name was successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-3063">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3063">See Also</span></span>

- <span data-ttu-id="08a18-3064">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-3064">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-3065">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-3065">fx_media_abort</span></span>
- <span data-ttu-id="08a18-3066">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-3066">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-3067">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-3067">fx_media_check</span></span>
- <span data-ttu-id="08a18-3068">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3068">fx_media_close</span></span>
- <span data-ttu-id="08a18-3069">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3069">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-3070">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-3070">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-3071">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-3071">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-3072">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-3072">fx_media_flush</span></span>
- <span data-ttu-id="08a18-3073">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-3073">fx_media_format</span></span>
- <span data-ttu-id="08a18-3074">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3074">fx_media_open</span></span>
- <span data-ttu-id="08a18-3075">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3075">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-3076">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3076">fx_media_read</span></span>
- <span data-ttu-id="08a18-3077">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-3077">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-3078">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3078">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-3079">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3079">fx_media_write</span></span>
- <span data-ttu-id="08a18-3080">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-3080">fx_system_initialize</span></span>

## <a name="fx_media_write"></a><span data-ttu-id="08a18-3081">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3081">fx_media_write</span></span>

<span data-ttu-id="08a18-3082">Scrive il settore logico</span><span class="sxs-lookup"><span data-stu-id="08a18-3082">Writes logical sector</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3083">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3083">Prototype</span></span>

```c
UINT fx_media_write(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector,
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="08a18-3084">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3084">Description</span></span>

<span data-ttu-id="08a18-3085">Questo servizio scrive il buffer fornito nel settore logico specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-3085">This service writes the supplied buffer to the specified logical sector.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3086">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3086">Input Parameters</span></span>

- <span data-ttu-id="08a18-3087">**media_ptr**: puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="08a18-3087">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="08a18-3088">**logical_sector**: settore logico da scrivere.</span><span class="sxs-lookup"><span data-stu-id="08a18-3088">**logical_sector**: Logical sector to write.</span></span>
- <span data-ttu-id="08a18-3089">**buffer_ptr**: puntatore all'origine per la scrittura nel settore logico.</span><span class="sxs-lookup"><span data-stu-id="08a18-3089">**buffer_ptr**: Pointer to the source for the logical sector write.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3090">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3090">Return Values</span></span>

- <span data-ttu-id="08a18-3091">**FX_SUCCESS** (0x00) scrittura multimediale riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-3091">**FX_SUCCESS** (0x00) Successful media write.</span></span>
- <span data-ttu-id="08a18-3092">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3092">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3093">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3093">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-3094">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3094">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3095">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-3095">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-3096">**FX_PTR_ERROR** (0x18) puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3096">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="08a18-3097">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3097">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3098">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3098">Allowed From</span></span>

<span data-ttu-id="08a18-3099">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3099">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3100">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3100">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3101">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3101">See Also</span></span>

- <span data-ttu-id="08a18-3102">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="08a18-3102">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="08a18-3103">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="08a18-3103">fx_media_abort</span></span>
- <span data-ttu-id="08a18-3104">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="08a18-3104">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="08a18-3105">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="08a18-3105">fx_media_check</span></span>
- <span data-ttu-id="08a18-3106">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3106">fx_media_close</span></span>
- <span data-ttu-id="08a18-3107">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3107">fx_media_close_notify_set</span></span>
- <span data-ttu-id="08a18-3108">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="08a18-3108">fx_media_exFAT_format</span></span>
- <span data-ttu-id="08a18-3109">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-3109">fx_media_extended_space_available</span></span>
- <span data-ttu-id="08a18-3110">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="08a18-3110">fx_media_flush</span></span>
- <span data-ttu-id="08a18-3111">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="08a18-3111">fx_media_format</span></span>
- <span data-ttu-id="08a18-3112">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3112">fx_media_open</span></span>
- <span data-ttu-id="08a18-3113">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3113">fx_media_open_notify_set</span></span>
- <span data-ttu-id="08a18-3114">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3114">fx_media_read</span></span>
- <span data-ttu-id="08a18-3115">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="08a18-3115">fx_media_space_available</span></span>
- <span data-ttu-id="08a18-3116">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3116">fx_media_volume_get</span></span>
- <span data-ttu-id="08a18-3117">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3117">fx_media_volume_set</span></span>
- <span data-ttu-id="08a18-3118">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-3118">fx_system_initialize</span></span>

## <a name="fx_system_date_get"></a><span data-ttu-id="08a18-3119">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3119">fx_system_date_get</span></span>

<span data-ttu-id="08a18-3120">Ottiene file system data</span><span class="sxs-lookup"><span data-stu-id="08a18-3120">Gets file system date</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3121">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3121">Prototype</span></span>

```c
UINT fx_system_date_get(
    UINT *year, 
    UINT *month, 
    UINT *day);
```
### <a name="description"></a><span data-ttu-id="08a18-3122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3122">Description</span></span>

<span data-ttu-id="08a18-3123">Questo servizio restituisce la data di sistema corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-3123">This service returns the current system date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3124">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3124">Input Parameters</span></span>

- <span data-ttu-id="08a18-3125">**year**: puntatore alla destinazione per year.</span><span class="sxs-lookup"><span data-stu-id="08a18-3125">**year**: Pointer to destination for year.</span></span>
- <span data-ttu-id="08a18-3126">**Month**: puntatore alla destinazione per month.</span><span class="sxs-lookup"><span data-stu-id="08a18-3126">**month**: Pointer to destination for month.</span></span>
- <span data-ttu-id="08a18-3127">**Day**: puntatore alla destinazione per il giorno.</span><span class="sxs-lookup"><span data-stu-id="08a18-3127">**day**: Pointer to destination for day.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3128">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3128">Return Values</span></span>

- <span data-ttu-id="08a18-3129">Il recupero della data con esito positivo **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-3129">**FX_SUCCESS** (0x00) Successful date retrieval.</span></span>
- <span data-ttu-id="08a18-3130">**FX_PTR_ERROR** (0x18) uno o più parametri di input sono null.</span><span class="sxs-lookup"><span data-stu-id="08a18-3130">**FX_PTR_ERROR** (0x18) One or more of the input parameters are NULL.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3131">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3131">Allowed From</span></span>

<span data-ttu-id="08a18-3132">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3132">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3133">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3133">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3134">See Also</span></span>

- <span data-ttu-id="08a18-3135">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3135">fx_system_date_set</span></span>
- <span data-ttu-id="08a18-3136">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-3136">fx_system_initialize</span></span>
- <span data-ttu-id="08a18-3137">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3137">fx_system_time_get</span></span>
- <span data-ttu-id="08a18-3138">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3138">fx_system_time_set</span></span>

## <a name="fx_system_date_set"></a><span data-ttu-id="08a18-3139">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3139">fx_system_date_set</span></span>

<span data-ttu-id="08a18-3140">Imposta la data di sistema</span><span class="sxs-lookup"><span data-stu-id="08a18-3140">Sets system date</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3141">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3141">Prototype</span></span>

```c
UINT fx_system_date_set(
    UINT year, 
    UINT month, 
    UINT day);
```

### <a name="description"></a><span data-ttu-id="08a18-3142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3142">Description</span></span>

<span data-ttu-id="08a18-3143">Questo servizio imposta la data di sistema come specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-3143">This service sets the system date as specified.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-3144">*Questo servizio deve essere chiamato poco dopo **fx_system_initialize** per impostare la data di sistema iniziale. Per impostazione predefinita, la data di sistema è quella dell'ultima versione FileX generica.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3144">*This service should be called shortly after **fx_system_initialize** to set the initial system date. By default, the system date is that of the last generic FileX release.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3145">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3145">Input Parameters</span></span>

- <span data-ttu-id="08a18-3146">**anno**: nuovo anno.</span><span class="sxs-lookup"><span data-stu-id="08a18-3146">**year**: New year.</span></span> <span data-ttu-id="08a18-3147">L'intervallo valido è compreso tra 1980 e l'anno 2107.</span><span class="sxs-lookup"><span data-stu-id="08a18-3147">The valid range is from 1980 through the year 2107.</span></span>
- <span data-ttu-id="08a18-3148">**mese**: nuovo mese.</span><span class="sxs-lookup"><span data-stu-id="08a18-3148">**month**: New month.</span></span> <span data-ttu-id="08a18-3149">L'intervallo valido è compreso tra 1 e 12.</span><span class="sxs-lookup"><span data-stu-id="08a18-3149">The valid range is from 1 through 12.</span></span>
- <span data-ttu-id="08a18-3150">**giorno**: nuovo giorno.</span><span class="sxs-lookup"><span data-stu-id="08a18-3150">**day**: New day.</span></span> <span data-ttu-id="08a18-3151">L'intervallo valido è compreso tra 1 e 31, a seconda delle condizioni del mese e dell'anno bisestile.</span><span class="sxs-lookup"><span data-stu-id="08a18-3151">The valid range is from 1 through 31, depending on month and leap year conditions.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3152">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3152">Return Values</span></span>

- <span data-ttu-id="08a18-3153">Impostazione della data riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-3153">**FX_SUCCESS** (0x00) Successful date setting.</span></span>
- <span data-ttu-id="08a18-3154">**FX_INVALID_YEAR** (0x12) anno non valido specificato.</span><span class="sxs-lookup"><span data-stu-id="08a18-3154">**FX_INVALID_YEAR** (0x12) Invalid year specified.</span></span>
- <span data-ttu-id="08a18-3155">Il mese **FX_INVALID_MONTH** (0x13) specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3155">**FX_INVALID_MONTH** (0x13) Invalid month specified.</span></span>
- <span data-ttu-id="08a18-3156">È stato specificato il giorno **FX_INVALID_DAY** (0X14) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3156">**FX_INVALID_DAY** (0x14) Invalid day specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3157">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3157">Allowed From</span></span>

<span data-ttu-id="08a18-3158">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3158">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3159">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3159">Example</span></span>

```c
 UINT             status;

/* Set the system date to December 12, 2005. */

status = fx_system_date_set(2005, 12, 12);

/* If status equals FX_SUCCESS, the file system date is now
    12-12-2005. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-3160">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3160">See Also</span></span>

- <span data-ttu-id="08a18-3161">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3161">fx_system_date_get</span></span>
- <span data-ttu-id="08a18-3162">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-3162">fx_system_initialize</span></span>
- <span data-ttu-id="08a18-3163">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3163">fx_system_time_get</span></span>
- <span data-ttu-id="08a18-3164">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3164">fx_system_time_set</span></span>

## <a name="fx_system_initialize"></a><span data-ttu-id="08a18-3165">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-3165">fx_system_initialize</span></span>

<span data-ttu-id="08a18-3166">Inizializza l'intero sistema</span><span class="sxs-lookup"><span data-stu-id="08a18-3166">Initializes entire system</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3167">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3167">Prototype</span></span>

```c
VOID fx_system_initialize(void);
```

### <a name="description"></a><span data-ttu-id="08a18-3168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3168">Description</span></span>

<span data-ttu-id="08a18-3169">Questo servizio Inizializza tutte le principali strutture di dati FileX.</span><span class="sxs-lookup"><span data-stu-id="08a18-3169">This service initializes all the major FileX data structures.</span></span> <span data-ttu-id="08a18-3170">Deve essere chiamato in ***tx_application_define*** o possibilmente da un thread di inizializzazione e deve essere chiamato prima di usare qualsiasi altro servizio FILEX.</span><span class="sxs-lookup"><span data-stu-id="08a18-3170">It should be called either in ***tx_application_define*** or possibly from an initialization thread and must be called prior to using any other FileX service.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-3171">\* Una volta inizializzata da questa chiamata, l'applicazione deve chiamare ***fx_system_date_set** _ e _ *fx_system_time_set** per iniziare con una data e un'ora di sistema accurate.\*</span><span class="sxs-lookup"><span data-stu-id="08a18-3171">*Once initialized by this call, the application should call ***fx_system_date_set** _ and _ *fx_system_time_set** to start with an accurate system date and time.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3172">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3172">Input Parameters</span></span>

<span data-ttu-id="08a18-3173">nessuno</span><span class="sxs-lookup"><span data-stu-id="08a18-3173">None</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3174">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3174">Return Values</span></span>

<span data-ttu-id="08a18-3175">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="08a18-3175">None.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3176">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3176">Allowed From</span></span>

<span data-ttu-id="08a18-3177">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3177">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3178">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3178">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3179">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3179">See Also</span></span>

- <span data-ttu-id="08a18-3180">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3180">fx_system_date_get</span></span>
- <span data-ttu-id="08a18-3181">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3181">fx_system_date_set</span></span>
- <span data-ttu-id="08a18-3182">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3182">fx_system_time_get</span></span>
- <span data-ttu-id="08a18-3183">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3183">fx_system_time_set</span></span>

## <a name="fx_system_time_get"></a><span data-ttu-id="08a18-3184">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3184">fx_system_time_get</span></span>

<span data-ttu-id="08a18-3185">Ottiene l'ora di sistema corrente</span><span class="sxs-lookup"><span data-stu-id="08a18-3185">Gets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3186">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3186">Prototype</span></span>

```c
UINT fx_system_time_get(
    UINT *hour,
    UINT *minute,
    UINT *second);
```

### <a name="description"></a><span data-ttu-id="08a18-3187">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3187">Description</span></span>

<span data-ttu-id="08a18-3188">Questo servizio recupera l'ora di sistema corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-3188">This service retrieves the current system time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3189">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3189">Input Parameters</span></span>

- <span data-ttu-id="08a18-3190">**ora**: puntatore alla destinazione per l'ora.</span><span class="sxs-lookup"><span data-stu-id="08a18-3190">**hour**: Pointer to destination for hour.</span></span>
- <span data-ttu-id="08a18-3191">**minute**: puntatore alla destinazione per i minuti.</span><span class="sxs-lookup"><span data-stu-id="08a18-3191">**minute**: Pointer to destination for minute.</span></span>
- <span data-ttu-id="08a18-3192">**secondo**: puntatore alla destinazione per il secondo.</span><span class="sxs-lookup"><span data-stu-id="08a18-3192">**second**: Pointer to destination for second.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3193">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3193">Return Values</span></span>

- <span data-ttu-id="08a18-3194">**FX_SUCCESS** (0x00) il recupero dell'ora di sistema è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3194">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="08a18-3195">**FX_PTR_ERROR** (0x18) uno o più parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3195">**FX_PTR_ERROR** (0x18) One or more of the input parameters</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3196">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3196">Allowed From</span></span>

<span data-ttu-id="08a18-3197">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3197">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3198">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3198">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3199">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3199">See Also</span></span>

- <span data-ttu-id="08a18-3200">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3200">fx_system_date_get</span></span>
- <span data-ttu-id="08a18-3201">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3201">fx_system_date_set</span></span>
- <span data-ttu-id="08a18-3202">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-3202">fx_system_initialize</span></span>
- <span data-ttu-id="08a18-3203">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3203">fx_system_time_set</span></span>

## <a name="fx_system_time_set"></a><span data-ttu-id="08a18-3204">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3204">fx_system_time_set</span></span>

<span data-ttu-id="08a18-3205">Imposta l'ora di sistema corrente</span><span class="sxs-lookup"><span data-stu-id="08a18-3205">Sets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3206">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3206">Prototype</span></span>

```c
UINT fx_system_time_set(UINT hour, UINT minute, UINT second);
```

### <a name="description"></a><span data-ttu-id="08a18-3207">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3207">Description</span></span>

<span data-ttu-id="08a18-3208">Questo servizio imposta l'ora di sistema corrente su quella specificata dai parametri di input.</span><span class="sxs-lookup"><span data-stu-id="08a18-3208">This service sets the current system time to that specified by the input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-3209">*Questo servizio deve essere chiamato poco dopo **fx_system_initialize** per impostare l'ora di sistema iniziale. Per impostazione predefinita, l'ora di sistema è 0:0:0.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3209">*This service should be called shortly after **fx_system_initialize** to set the initial system time. By default, the system time is 0:0:0.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3210">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3210">Input Parameters</span></span>

- <span data-ttu-id="08a18-3211">**ora**: nuova ora (0-23).</span><span class="sxs-lookup"><span data-stu-id="08a18-3211">**hour**: New hour (0-23).</span></span>
- <span data-ttu-id="08a18-3212">**minuto**: nuovo minuto (0-59).</span><span class="sxs-lookup"><span data-stu-id="08a18-3212">**minute**: New minute (0-59).</span></span>
- <span data-ttu-id="08a18-3213">**secondo**: nuovo secondo (0-59).</span><span class="sxs-lookup"><span data-stu-id="08a18-3213">**second**: New second (0-59).</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3214">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3214">Return Values</span></span>

- <span data-ttu-id="08a18-3215">**FX_SUCCESS** (0x00) il recupero dell'ora di sistema è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3215">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="08a18-3216">La nuova ora **FX_INVALID_HOUR** (0x15) non è valida.</span><span class="sxs-lookup"><span data-stu-id="08a18-3216">**FX_INVALID_HOUR**    (0x15) New hour is invalid.</span></span>
- <span data-ttu-id="08a18-3217">**FX_INVALID_MINUTE** (0x16) nuovo minuto non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3217">**FX_INVALID_MINUTE** (0x16) New minute is invalid.</span></span>
- <span data-ttu-id="08a18-3218">Il nuovo secondo **FX_INVALID_SECOND** (0x17) non è valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3218">**FX_INVALID_SECOND** (0x17) New second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3219">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3219">Allowed From</span></span>

<span data-ttu-id="08a18-3220">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3220">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3221">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3221">Example</span></span>

```c
 UINT status;

/* Set the current system time to hour 23, minute 21, and second 20. */

status = fx_system_time_set(23, 21, 20);

/* If status is FX_SUCCESS, the current system time has been set. */
```

### <a name="see-also"></a><span data-ttu-id="08a18-3222">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3222">See Also</span></span>

- <span data-ttu-id="08a18-3223">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3223">fx_system_date_get</span></span>
- <span data-ttu-id="08a18-3224">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3224">fx_system_date_set</span></span>
- <span data-ttu-id="08a18-3225">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="08a18-3225">fx_system_initialize</span></span>
- <span data-ttu-id="08a18-3226">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3226">fx_system_time_get</span></span>

## <a name="fx_unicode_directory_create"></a><span data-ttu-id="08a18-3227">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3227">fx_unicode_directory_create</span></span>

<span data-ttu-id="08a18-3228">Crea una directory Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3228">Creates a Unicode directory</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3229">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3229">Prototype</span></span>

```c
UINT fx_unicode_directory_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```
### <a name="description"></a><span data-ttu-id="08a18-3230">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3230">Description</span></span>

<span data-ttu-id="08a18-3231">Questo servizio crea una sottodirectory con nome Unicode nella directory predefinita corrente; non sono consentite informazioni sul percorso nel parametro del nome di origine Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3231">This service creates a Unicode-named subdirectory in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="08a18-3232">In caso di esito positivo, viene restituito dal servizio il nome breve (formato 8,3) della sottodirectory Unicode appena creata.</span><span class="sxs-lookup"><span data-stu-id="08a18-3232">If successful, the short name (8.3 format) of the newly created Unicode subdirectory is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-3233">*Tutte le operazioni nella sottodirectory Unicode, che lo rendono il percorso predefinito, l'eliminazione e così via, devono essere eseguite specificando il nome breve restituito (formato 8,3) per i servizi directory FileX standard.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3233">*All operations on the Unicode subdirectory (making it the default path, deleting, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX directory services.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3234">*Questo servizio non è supportato nei supporti exFAT.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3234">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3235">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3235">Input Parameters</span></span>

- <span data-ttu-id="08a18-3236">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3236">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3237">**source_unicode_name**: puntatore al nome Unicode per la nuova sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="08a18-3237">**source_unicode_name**: Pointer to the Unicode name for the new subdirectory.</span></span>
- <span data-ttu-id="08a18-3238">**source_unicode_length**: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3238">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="08a18-3239">**short_name**: puntatore alla destinazione per nome breve (formato 8,3) per la nuova sottodirectory Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3239">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode subdirectory.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3240">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3240">Return Values</span></span>

- <span data-ttu-id="08a18-3241">**FX_SUCCESS** (0x00) la directory Unicode creata è riuscita.</span><span class="sxs-lookup"><span data-stu-id="08a18-3241">**FX_SUCCESS** (0x00) Successful Unicode directory create.</span></span>
- <span data-ttu-id="08a18-3242">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3242">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3243">La directory specificata **FX_ALREADY_CREATED** (0x0B) esiste già.</span><span class="sxs-lookup"><span data-stu-id="08a18-3243">**FX_ALREADY_CREATED** (0x0B) Specified directory already exists.</span></span>
- <span data-ttu-id="08a18-3244">**FX_NO_MORE_SPACE** (0X0A) non sono più disponibili cluster nel supporto per la nuova voce di directory.</span><span class="sxs-lookup"><span data-stu-id="08a18-3244">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new directory entry.</span></span>
- <span data-ttu-id="08a18-3245">Il servizio **FX_NOT_IMPLEMENTED** (0x22) non è implementato per exFAT file System.</span><span class="sxs-lookup"><span data-stu-id="08a18-3245">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="08a18-3246">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-3246">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-3247">**FX_PTR_ERROR** (0x18) i puntatori ai supporti o ai nomi non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-3247">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="08a18-3248">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3248">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="08a18-3249">**FX_IO_ERROR (0x90)** Errore di I/O del driver.</span><span class="sxs-lookup"><span data-stu-id="08a18-3249">**FX_IO_ERROR    (0x90)** Driver I/O error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3250">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3250">Allowed From</span></span>

<span data-ttu-id="08a18-3251">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3251">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3252">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3252">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3253">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3253">See Also</span></span>

- <span data-ttu-id="08a18-3254">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3254">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-3255">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3255">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-3256">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3256">fx_directory_create</span></span>
- <span data-ttu-id="08a18-3257">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3257">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-3258">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3258">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-3259">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3259">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-3260">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-3260">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-3261">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-3261">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-3262">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3262">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-3263">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-3263">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-3264">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3264">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-3265">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-3265">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-3266">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3266">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-3267">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3267">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-3268">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-3268">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-3269">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-3269">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-3270">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-3270">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-3271">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3271">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-3272">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3272">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-3273">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3273">fx_unicode_directory_rename</span></span>

## <a name="fx_unicode_directory_rename"></a><span data-ttu-id="08a18-3274">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3274">fx_unicode_directory_rename</span></span>

<span data-ttu-id="08a18-3275">Rinomina la directory con la stringa Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3275">Renames directory using Unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3276">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3276">Prototype</span></span>

```c
UINT fx_unicode_directory_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length,
    CHAR *new_short_name);
```
### <a name="description"></a><span data-ttu-id="08a18-3277">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3277">Description</span></span>

<span data-ttu-id="08a18-3278">Questo servizio modifica una sottodirectory con nome Unicode in un nuovo nome Unicode specificato nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-3278">This service changes a Unicode-named subdirectory to specified new Unicode name in current working directory.</span></span> <span data-ttu-id="08a18-3279">I parametri del nome Unicode non devono avere informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="08a18-3279">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3280">*Questo servizio non è supportato nei supporti exFAT.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3280">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3281">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3281">Input Parameters</span></span>

- <span data-ttu-id="08a18-3282">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3282">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3283">**old_unicode_name**: puntatore al nome Unicode per il file corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-3283">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="08a18-3284">**old_unicode_name_length**: lunghezza del nome Unicode corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-3284">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="08a18-3285">**new_unicode_name**: puntatore al nuovo nome file Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3285">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="08a18-3286">**old_unicode_name_length**: lunghezza del nuovo nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3286">**old_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="08a18-3287">**new_short_name**: puntatore alla destinazione per nome breve (formato 8,3) per il file Unicode rinominato.</span><span class="sxs-lookup"><span data-stu-id="08a18-3287">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span> <span data-ttu-id="08a18-3288">Rinomina Directory con Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3288">Rename Directory with Unicode</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3289">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3289">Return Values</span></span>

- <span data-ttu-id="08a18-3290">Apertura del supporto **FX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="08a18-3290">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="08a18-3291">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3291">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3292">Il nome di directory specificato **FX_ALREADY_CREATED** (0x0B) esiste già.</span><span class="sxs-lookup"><span data-stu-id="08a18-3292">**FX_ALREADY_CREATED** (0x0B) Specified directory name already exists.</span></span>
- <span data-ttu-id="08a18-3293">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3293">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3294">**FX_PTR_ERROR** (0x18) uno o più puntatori sono null.</span><span class="sxs-lookup"><span data-stu-id="08a18-3294">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="08a18-3295">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3295">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="08a18-3296">**FX_WRITE_PROTECT** (0x23) i supporti specificati sono protetti da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-3296">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3297">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3297">Allowed From</span></span>

<span data-ttu-id="08a18-3298">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3298">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3299">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3299">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3300">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3300">See Also</span></span>

- <span data-ttu-id="08a18-3301">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3301">fx_directory_attributes_read</span></span>
- <span data-ttu-id="08a18-3302">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3302">fx_directory_attributes_set</span></span>
- <span data-ttu-id="08a18-3303">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3303">fx_directory_create</span></span>
- <span data-ttu-id="08a18-3304">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3304">fx_directory_default_get</span></span>
- <span data-ttu-id="08a18-3305">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3305">fx_directory_default_set</span></span>
- <span data-ttu-id="08a18-3306">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3306">fx_directory_delete</span></span>
- <span data-ttu-id="08a18-3307">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-3307">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="08a18-3308">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-3308">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="08a18-3309">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3309">fx_directory_information_get</span></span>
- <span data-ttu-id="08a18-3310">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="08a18-3310">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="08a18-3311">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3311">fx_directory_local_path_get</span></span>
- <span data-ttu-id="08a18-3312">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="08a18-3312">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="08a18-3313">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3313">fx_directory_local_path_set</span></span>
- <span data-ttu-id="08a18-3314">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3314">fx_directory_long_name_get</span></span>
- <span data-ttu-id="08a18-3315">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="08a18-3315">fx_directory_name_test</span></span>
- <span data-ttu-id="08a18-3316">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-3316">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="08a18-3317">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="08a18-3317">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="08a18-3318">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3318">fx_directory_rename</span></span>
- <span data-ttu-id="08a18-3319">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3319">fx_directory_short_name_get</span></span>
- <span data-ttu-id="08a18-3320">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3320">fx_unicode_directory_create</span></span>

## <a name="fx_unicode_file_create"></a><span data-ttu-id="08a18-3321">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3321">fx_unicode_file_create</span></span>

<span data-ttu-id="08a18-3322">Crea un file Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3322">Creates a Unicode file</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3323">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3323">Prototype</span></span>

```c
UINT fx_unicode_file_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="08a18-3324">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3324">Description</span></span>

<span data-ttu-id="08a18-3325">Questo servizio crea un file con nome Unicode nella directory predefinita corrente. nel parametro del nome di origine Unicode non sono consentite informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="08a18-3325">This service creates a Unicode-named file in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="08a18-3326">In caso di esito positivo, il nome breve (formato 8,3) del file Unicode appena creato viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="08a18-3326">If successful, the short name (8.3 format) of the newly created Unicode file is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="08a18-3327">*Tutte le operazioni sul file Unicode (apertura, scrittura, lettura, chiusura e così via) devono essere eseguite fornendo il nome breve restituito (formato 8,3) ai servizi file FileX standard.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3327">*All operations on the Unicode file (opening, writing, reading, closing, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX file services.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3328">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3328">Input Parameters</span></span>


- <span data-ttu-id="08a18-3329">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3329">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3330">**source_unicode_name**: puntatore al nome Unicode per il nuovo file.</span><span class="sxs-lookup"><span data-stu-id="08a18-3330">**source_unicode_name**: Pointer to the Unicode name for the new file.</span></span>
- <span data-ttu-id="08a18-3331">**source_unicode_length**: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3331">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="08a18-3332">**short_name**: puntatore alla destinazione per nome breve (formato 8,3) per il nuovo file Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3332">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3333">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3333">Return Values</span></span>

- <span data-ttu-id="08a18-3334">Creazione file riuscita **FX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="08a18-3334">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="08a18-3335">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3335">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3336">Il file specificato **FX_ALREADY_CREATED** (0x0B) esiste già.</span><span class="sxs-lookup"><span data-stu-id="08a18-3336">**FX_ALREADY_CREATED** (0x0B) Specified file already exists.</span></span>
- <span data-ttu-id="08a18-3337">**FX_NO_MORE_SPACE** (0X0A) non sono più disponibili cluster nel supporto per la nuova voce di file.</span><span class="sxs-lookup"><span data-stu-id="08a18-3337">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new file entry.</span></span>
- <span data-ttu-id="08a18-3338">Il servizio **FX_NOT_IMPLEMENTED** (0x22) non è implementato per exFAT file System.</span><span class="sxs-lookup"><span data-stu-id="08a18-3338">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="08a18-3339">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3339">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3340">Il supporto di **FX_WRITE_PROTECT** (0X23) specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-3340">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="08a18-3341">**FX_PTR_ERROR** (0x18) i puntatori ai supporti o ai nomi non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-3341">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="08a18-3342">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3342">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3343">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3343">Allowed From</span></span>

<span data-ttu-id="08a18-3344">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3344">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3345">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3345">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3346">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3346">See Also</span></span>

- <span data-ttu-id="08a18-3347">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3347">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-3348">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3348">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-3349">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3349">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-3350">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3350">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3351">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3351">fx_file_close</span></span>
- <span data-ttu-id="08a18-3352">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3352">fx_file_create</span></span>
- <span data-ttu-id="08a18-3353">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3353">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-3354">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3354">fx_file_delete</span></span>
- <span data-ttu-id="08a18-3355">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3355">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-3356">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3356">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3357">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3357">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-3358">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3358">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-3359">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3359">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-3360">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3360">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-3361">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3361">fx_file_open</span></span>
- <span data-ttu-id="08a18-3362">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3362">fx_file_read</span></span>
- <span data-ttu-id="08a18-3363">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3363">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-3364">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3364">fx_file_rename</span></span>
- <span data-ttu-id="08a18-3365">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3365">fx_file_seek</span></span>
- <span data-ttu-id="08a18-3366">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3366">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-3367">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3367">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-3368">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3368">fx_file_write</span></span>
- <span data-ttu-id="08a18-3369">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3369">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-3370">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3370">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-3371">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3371">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-3372">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3372">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_file_rename"></a><span data-ttu-id="08a18-3373">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3373">fx_unicode_file_rename</span></span>

<span data-ttu-id="08a18-3374">Rinomina un file usando la stringa Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3374">Renames a file using unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3375">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3375">Prototype</span></span>

```c
UINT fx_unicode_file_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length, 
    CHAR *new_short_name);
```

### <a name="description"></a><span data-ttu-id="08a18-3376">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3376">Description</span></span>

<span data-ttu-id="08a18-3377">Questo servizio modifica un nome di file con nome Unicode in un nuovo nome Unicode specificato nella directory predefinita corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-3377">This service changes a Unicode-named file name to specified new Unicode name in current default directory.</span></span> <span data-ttu-id="08a18-3378">I parametri del nome Unicode non devono avere informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="08a18-3378">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3379">*Questo servizio non è supportato nei supporti exFAT.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3379">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3380">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3380">Input Parameters</span></span>

- <span data-ttu-id="08a18-3381">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3381">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3382">**old_unicode_name**: puntatore al nome Unicode per il file corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-3382">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="08a18-3383">**old_unicode_name_length**: lunghezza del nome Unicode corrente.</span><span class="sxs-lookup"><span data-stu-id="08a18-3383">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="08a18-3384">**new_unicode_name**: puntatore al nuovo nome file Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3384">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="08a18-3385">**new_unicode_name_length**: lunghezza del nuovo nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3385">**new_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="08a18-3386">**new_short_name**: puntatore alla destinazione per nome breve (formato 8,3) per il file Unicode rinominato.</span><span class="sxs-lookup"><span data-stu-id="08a18-3386">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3387">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3387">Return Values</span></span>


- <span data-ttu-id="08a18-3388">Apertura del supporto **FX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="08a18-3388">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="08a18-3389">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3389">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3390">Il nome file specificato **FX_ALREADY_CREATED** (0x0B) esiste già.</span><span class="sxs-lookup"><span data-stu-id="08a18-3390">**FX_ALREADY_CREATED** (0x0B) Specified file name already exists.</span></span>
- <span data-ttu-id="08a18-3391">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3391">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3392">**FX_PTR_ERROR** (0x18) uno o più puntatori sono null.</span><span class="sxs-lookup"><span data-stu-id="08a18-3392">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="08a18-3393">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3393">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="08a18-3394">**FX_WRITE_PROTECT** (0x23) i supporti specificati sono protetti da scrittura.</span><span class="sxs-lookup"><span data-stu-id="08a18-3394">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3395">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3395">Allowed From</span></span>

<span data-ttu-id="08a18-3396">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3396">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3397">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3397">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3398">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3398">See Also</span></span>

- <span data-ttu-id="08a18-3399">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3399">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-3400">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3400">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-3401">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3401">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-3402">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3402">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3403">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3403">fx_file_close</span></span>
- <span data-ttu-id="08a18-3404">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3404">fx_file_create</span></span>
- <span data-ttu-id="08a18-3405">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3405">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-3406">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3406">fx_file_delete</span></span>
- <span data-ttu-id="08a18-3407">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3407">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-3408">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3408">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3409">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3409">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-3410">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3410">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-3411">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3411">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-3412">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3412">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-3413">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3413">fx_file_open</span></span>
- <span data-ttu-id="08a18-3414">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3414">fx_file_read</span></span>
- <span data-ttu-id="08a18-3415">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3415">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-3416">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3416">fx_file_rename</span></span>
- <span data-ttu-id="08a18-3417">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3417">fx_file_seek</span></span>
- <span data-ttu-id="08a18-3418">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3418">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-3419">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3419">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-3420">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3420">fx_file_write</span></span>
- <span data-ttu-id="08a18-3421">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3421">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-3422">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3422">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-3423">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3423">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-3424">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3424">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get"></a><span data-ttu-id="08a18-3425">fx_unicode_length_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3425">fx_unicode_length_get</span></span>

<span data-ttu-id="08a18-3426">Ottiene la lunghezza del nome Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3426">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3427">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3427">Prototype</span></span>

```c
ULONG fx_unicode_length_get(UCHAR *unicode_name);
```
### <a name="description"></a><span data-ttu-id="08a18-3428">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3428">Description</span></span>

<span data-ttu-id="08a18-3429">Questo servizio determina la lunghezza del nome Unicode fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3429">This service determines the length of the supplied Unicode name.</span></span> <span data-ttu-id="08a18-3430">Un carattere Unicode è rappresentato da due byte.</span><span class="sxs-lookup"><span data-stu-id="08a18-3430">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="08a18-3431">Un nome Unicode è costituito da una serie di caratteri Unicode a due byte terminati da due byte NULL (due byte di valore 0).</span><span class="sxs-lookup"><span data-stu-id="08a18-3431">A Unicode name is a series of two byte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3432">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3432">Input Parameters</span></span>

<span data-ttu-id="08a18-3433">**unicode_name**: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3433">**unicode_name**: Pointer to Unicode name.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3434">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3434">Return Values</span></span>

<span data-ttu-id="08a18-3435">**length**: lunghezza del nome Unicode (numero di caratteri Unicode nel nome).</span><span class="sxs-lookup"><span data-stu-id="08a18-3435">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3436">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3436">Allowed From</span></span>

<span data-ttu-id="08a18-3437">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3437">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3438">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3438">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3439">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3439">See Also</span></span>

- <span data-ttu-id="08a18-3440">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3440">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-3441">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3441">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-3442">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3442">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-3443">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3443">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3444">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3444">fx_file_close</span></span>
- <span data-ttu-id="08a18-3445">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3445">fx_file_create</span></span>
- <span data-ttu-id="08a18-3446">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3446">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-3447">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3447">fx_file_delete</span></span>
- <span data-ttu-id="08a18-3448">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3448">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-3449">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3449">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3450">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3450">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-3451">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3451">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-3452">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3452">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-3453">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3453">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-3454">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3454">fx_file_open</span></span>
- <span data-ttu-id="08a18-3455">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3455">fx_file_read</span></span>
- <span data-ttu-id="08a18-3456">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3456">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-3457">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3457">fx_file_rename</span></span>
- <span data-ttu-id="08a18-3458">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3458">fx_file_seek</span></span>
- <span data-ttu-id="08a18-3459">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3459">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-3460">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3460">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-3461">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3461">fx_file_write</span></span>
- <span data-ttu-id="08a18-3462">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3462">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-3463">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3463">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-3464">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3464">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-3465">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3465">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-3466">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3466">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get_extended"></a><span data-ttu-id="08a18-3467">fx_unicode_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="08a18-3467">fx_unicode_length_get_extended</span></span>

<span data-ttu-id="08a18-3468">Ottiene la lunghezza del nome Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3468">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3469">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3469">Prototype</span></span>

```c
UINT fx_unicode_length_get_extended(
    UCHAR *unicode_name,
    UINT buffer_length);
```
### <a name="description"></a><span data-ttu-id="08a18-3470">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3470">Description</span></span>

<span data-ttu-id="08a18-3471">Questo servizio ottiene la lunghezza del nome Unicode fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3471">This service gets the length of the supplied Unicode name.</span></span> <span data-ttu-id="08a18-3472">Un carattere Unicode è rappresentato da due byte.</span><span class="sxs-lookup"><span data-stu-id="08a18-3472">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="08a18-3473">Un nome Unicode è una serie di caratteri Unicode twobyte terminati da due byte NULL (due byte di valore 0).</span><span class="sxs-lookup"><span data-stu-id="08a18-3473">A Unicode name is a series of twobyte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3474">*Questo servizio è identico a **fx_unicode_length_get ()** ad eccezione del fatto che il chiamante passa alla dimensione del buffer **unicode_name** , inclusi i due caratteri null.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3474">*This service is identical to **fx_unicode_length_get()** except the caller passes in the size of the **unicode_name** buffer, including the two NULL characters.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3475">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3475">Input Parameters</span></span>

- <span data-ttu-id="08a18-3476">**unicode_name**: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3476">**unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="08a18-3477">**BUFFER_LENGTH**: dimensione del buffer dei nomi Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3477">**buffer_length**: Size of Unicode name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3478">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3478">Return Values</span></span>

<span data-ttu-id="08a18-3479">**length**: lunghezza del nome Unicode (numero di caratteri Unicode nel nome).</span><span class="sxs-lookup"><span data-stu-id="08a18-3479">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3480">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3480">Allowed From</span></span>

<span data-ttu-id="08a18-3481">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3481">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3482">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3482">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3483">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3483">See Also</span></span>

- <span data-ttu-id="08a18-3484">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3484">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-3485">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3485">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-3486">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3486">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-3487">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3487">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3488">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3488">fx_file_close</span></span>
- <span data-ttu-id="08a18-3489">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3489">fx_file_create</span></span>
- <span data-ttu-id="08a18-3490">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3490">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-3491">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3491">fx_file_delete</span></span>
- <span data-ttu-id="08a18-3492">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3492">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-3493">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3493">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3494">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3494">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-3495">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3495">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-3496">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3496">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-3497">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3497">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-3498">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3498">fx_file_open</span></span>
- <span data-ttu-id="08a18-3499">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3499">fx_file_read</span></span>
- <span data-ttu-id="08a18-3500">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3500">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-3501">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3501">fx_file_rename</span></span>
- <span data-ttu-id="08a18-3502">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3502">fx_file_seek</span></span>
- <span data-ttu-id="08a18-3503">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3503">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-3504">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3504">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-3505">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3505">fx_file_write</span></span>
- <span data-ttu-id="08a18-3506">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3506">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-3507">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3507">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-3508">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3508">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-3509">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3509">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-3510">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3510">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get"></a><span data-ttu-id="08a18-3511">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3511">fx_unicode_name_get</span></span>

<span data-ttu-id="08a18-3512">Ottiene il nome Unicode dal nome breve</span><span class="sxs-lookup"><span data-stu-id="08a18-3512">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3513">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3513">Prototype</span></span>

```c
UINT fx_unicode_name_get(
    FX_MEDIA *media_ptr, 
    CHAR *source_short_name,
    UCHAR *destination_unicode_name, 
    ULONG *destination_unicode_length);
```

### <a name="description"></a><span data-ttu-id="08a18-3514">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3514">Description</span></span>

<span data-ttu-id="08a18-3515">Questo servizio recupera il nome Unicode associato al nome breve fornito (formato 8,3) nella directory predefinita corrente; nel parametro nome breve non sono consentite informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="08a18-3515">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="08a18-3516">Se l'esito è positivo, il servizio restituisce il nome Unicode associato al nome breve.</span><span class="sxs-lookup"><span data-stu-id="08a18-3516">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3517">*Questo servizio può essere utilizzato per ottenere i nomi Unicode per i file e le sottodirectory.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3517">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3518">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3518">Input Parameters</span></span>

- <span data-ttu-id="08a18-3519">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3519">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3520">**short_name** Puntatore al nome breve (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-3520">**short_name** Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="08a18-3521">**destination_unicode_name**: puntatore alla destinazione per il nome Unicode associato al nome breve fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3521">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="08a18-3522">**destination_unicode_length**: puntatore alla lunghezza del nome Unicode restituita.</span><span class="sxs-lookup"><span data-stu-id="08a18-3522">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3523">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3523">Return Values</span></span>

- <span data-ttu-id="08a18-3524">**FX_SUCCESS** (0x00) il recupero del nome Unicode è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3524">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="08a18-3525">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-3525">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="08a18-3526">Il file di **FX_FILE_CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-3526">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-3527">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3527">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3528">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3528">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3529">Il nome breve **FX_NOT_FOUND** (0x04) non è stato trovato o la dimensione della destinazione Unicode è troppo piccola.</span><span class="sxs-lookup"><span data-stu-id="08a18-3529">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="08a18-3530">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3530">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-3531">**FX_PTR_ERROR** (0x18) i puntatori ai supporti o ai nomi non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-3531">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="08a18-3532">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3532">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3533">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3533">Allowed From</span></span>

<span data-ttu-id="08a18-3534">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3534">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3535">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3535">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3536">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3536">See Also</span></span>

- <span data-ttu-id="08a18-3537">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3537">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-3538">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3538">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-3539">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3539">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-3540">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3540">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3541">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3541">fx_file_close</span></span>
- <span data-ttu-id="08a18-3542">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3542">fx_file_create</span></span>
- <span data-ttu-id="08a18-3543">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3543">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-3544">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3544">fx_file_delete</span></span>
- <span data-ttu-id="08a18-3545">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3545">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-3546">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3546">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3547">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3547">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-3548">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3548">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-3549">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3549">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-3550">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3550">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-3551">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3551">fx_file_open</span></span>
- <span data-ttu-id="08a18-3552">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3552">fx_file_read</span></span>
- <span data-ttu-id="08a18-3553">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3553">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-3554">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3554">fx_file_rename</span></span>
- <span data-ttu-id="08a18-3555">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3555">fx_file_seek</span></span>
- <span data-ttu-id="08a18-3556">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3556">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-3557">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3557">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-3558">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3558">fx_file_write</span></span>
- <span data-ttu-id="08a18-3559">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3559">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-3560">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3560">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-3561">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3561">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-3562">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3562">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get_extended"></a><span data-ttu-id="08a18-3563">fx_unicode_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="08a18-3563">fx_unicode_name_get_extended</span></span>

<span data-ttu-id="08a18-3564">Ottiene il nome Unicode dal nome breve</span><span class="sxs-lookup"><span data-stu-id="08a18-3564">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3565">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3565">Prototype</span></span>

```c
UINT fx_unicode_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *source_short_name,
    UCHAR *destination_unicode_name,
    ULONG *destination_unicode_length,
    ULONG unicode_name_buffer_length);
```
### <a name="description"></a><span data-ttu-id="08a18-3566">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3566">Description</span></span>

<span data-ttu-id="08a18-3567">Questo servizio recupera il nome Unicode associato al nome breve fornito (formato 8,3) nella directory predefinita corrente; nel parametro nome breve non sono consentite informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="08a18-3567">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="08a18-3568">Se l'esito è positivo, il servizio restituisce il nome Unicode associato al nome breve.</span><span class="sxs-lookup"><span data-stu-id="08a18-3568">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3569">\* Questo servizio è identico a \***fx_unicode_name_get**_, ad eccezione del chiamante che fornisce la dimensione del buffer Unicode di destinazione come argomento di input. Ciò consente al servizio di garantire che non sovrascriva il buffer Unicode di destinazione_</span><span class="sxs-lookup"><span data-stu-id="08a18-3569">\*This service is identical to \***fx_unicode_name_get**_, except the caller supplies the size of the destination Unicode buffer as an input argument. This allows the service to guarantee that it will not overwrite the destination Unicode buffer_</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3570">*Questo servizio può essere utilizzato per ottenere i nomi Unicode per i file e le sottodirectory.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3570">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3571">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3571">Input Parameters</span></span>

- <span data-ttu-id="08a18-3572">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3572">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3573">**short_name**: puntatore al nome breve (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-3573">**short_name**: Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="08a18-3574">**destination_unicode_name**: puntatore alla destinazione per il nome Unicode associato al nome breve fornito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3574">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="08a18-3575">**destination_unicode_length**: puntatore alla lunghezza del nome Unicode restituita.</span><span class="sxs-lookup"><span data-stu-id="08a18-3575">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>
- <span data-ttu-id="08a18-3576">**unicode_name_buffer_length**: dimensione del buffer dei nomi Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3576">**unicode_name_buffer_length**: Size of the Unicode name buffer.</span></span> <span data-ttu-id="08a18-3577">Nota: è necessario un carattere di terminazione NULL, che rende un byte aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="08a18-3577">Note: A NULL terminator is required, which makes an extra byte.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3578">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3578">Return Values</span></span>

- <span data-ttu-id="08a18-3579">**FX_SUCCESS** (0x00) il recupero del nome Unicode è riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3579">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="08a18-3580">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-3580">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="08a18-3581">Il file di **FX_FILE_CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-3581">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-3582">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3582">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3583">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3583">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3584">Il nome breve **FX_NOT_FOUND** (0x04) non è stato trovato o la dimensione della destinazione Unicode è troppo piccola.</span><span class="sxs-lookup"><span data-stu-id="08a18-3584">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="08a18-3585">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3585">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-3586">**FX_PTR_ERROR** (0x18) i puntatori ai supporti o ai nomi non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-3586">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="08a18-3587">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3587">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3588">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3588">Allowed From</span></span>

<span data-ttu-id="08a18-3589">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3589">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3590">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3590">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3591">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3591">See Also</span></span>

- <span data-ttu-id="08a18-3592">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3592">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-3593">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3593">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-3594">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3594">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-3595">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3595">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3596">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3596">fx_file_close</span></span>
- <span data-ttu-id="08a18-3597">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3597">fx_file_create</span></span>
- <span data-ttu-id="08a18-3598">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3598">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-3599">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3599">fx_file_delete</span></span>
- <span data-ttu-id="08a18-3600">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3600">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-3601">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3601">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3602">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3602">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-3603">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3603">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-3604">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3604">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-3605">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3605">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-3606">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3606">fx_file_open</span></span>
- <span data-ttu-id="08a18-3607">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3607">fx_file_read</span></span>
- <span data-ttu-id="08a18-3608">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3608">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-3609">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3609">fx_file_rename</span></span>
- <span data-ttu-id="08a18-3610">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3610">fx_file_seek</span></span>
- <span data-ttu-id="08a18-3611">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3611">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-3612">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3612">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-3613">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3613">fx_file_write</span></span>
- <span data-ttu-id="08a18-3614">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3614">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-3615">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3615">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-3616">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3616">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-3617">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3617">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_short_name_get"></a><span data-ttu-id="08a18-3618">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3618">fx_unicode_short_name_get</span></span>

<span data-ttu-id="08a18-3619">Ottiene il nome breve dal nome Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3619">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3620">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3620">Prototype</span></span>

```c
UINT fx_unicode_short_name_get(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length,
    CHAR *destination_short_name);
```

<span data-ttu-id="08a18-3621">Questo servizio recupera il nome breve (formato 8,3) associato al nome Unicode all'interno della directory predefinita corrente. nel parametro del nome Unicode non sono consentite informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="08a18-3621">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="08a18-3622">In caso di esito positivo, il nome breve associato al nome Unicode viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="08a18-3622">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3623">*Questo servizio può essere usato per ottenere nomi brevi per i file e le sottodirectory.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3623">*This service can be used to get short names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3624">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3624">Input Parameters</span></span>

- <span data-ttu-id="08a18-3625">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3625">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3626">**source_unicode_name**: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3626">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="08a18-3627">**source_unicode_length**: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3627">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="08a18-3628">**destination_short_name**: puntatore alla destinazione per il nome breve (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-3628">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="08a18-3629">Deve avere una dimensione di almeno 13 byte.</span><span class="sxs-lookup"><span data-stu-id="08a18-3629">This must be at least 13 bytes in size.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3630">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3630">Return Values</span></span>

- <span data-ttu-id="08a18-3631">**FX_SUCCESS** (0x00) il recupero del nome breve riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3631">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="08a18-3632">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-3632">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="08a18-3633">Il file di **FX_FILE_CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-3633">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="08a18-3634">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3634">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3635">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3635">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3636">Impossibile trovare il nome Unicode **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-3636">**FX_NOT_FOUND** (0x04)    Unicode name was not found.</span></span>
- <span data-ttu-id="08a18-3637">Il servizio **FX_NOT_IMPLEMENTED** (0x22) non è implementato per exFAT file System.</span><span class="sxs-lookup"><span data-stu-id="08a18-3637">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="08a18-3638">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3638">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-3639">**FX_PTR_ERROR** (0x18) i puntatori ai supporti o ai nomi non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-3639">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="08a18-3640">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3640">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3641">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3641">Allowed From</span></span>

<span data-ttu-id="08a18-3642">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3642">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3643">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3643">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3644">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3644">See Also</span></span>

- <span data-ttu-id="08a18-3645">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3645">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-3646">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3646">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-3647">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3647">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-3648">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3648">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3649">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3649">fx_file_close</span></span>
- <span data-ttu-id="08a18-3650">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3650">fx_file_create</span></span>
- <span data-ttu-id="08a18-3651">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3651">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-3652">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3652">fx_file_delete</span></span>
- <span data-ttu-id="08a18-3653">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3653">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-3654">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3654">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3655">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3655">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-3656">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3656">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-3657">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3657">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-3658">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3658">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-3659">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3659">fx_file_open</span></span>
- <span data-ttu-id="08a18-3660">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3660">fx_file_read</span></span>
- <span data-ttu-id="08a18-3661">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3661">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-3662">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3662">fx_file_rename</span></span>
- <span data-ttu-id="08a18-3663">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3663">fx_file_seek</span></span>
- <span data-ttu-id="08a18-3664">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3664">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-3665">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3665">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-3666">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3666">fx_file_write</span></span>
- <span data-ttu-id="08a18-3667">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3667">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-3668">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3668">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-3669">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3669">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-3670">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3670">fx_unicode_name_get</span></span>

## <a name="fx_unicode_short_name_get_extended"></a><span data-ttu-id="08a18-3671">fx_unicode_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="08a18-3671">fx_unicode_short_name_get_extended</span></span>

<span data-ttu-id="08a18-3672">Ottiene il nome breve dal nome Unicode</span><span class="sxs-lookup"><span data-stu-id="08a18-3672">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="08a18-3673">Prototipo</span><span class="sxs-lookup"><span data-stu-id="08a18-3673">Prototype</span></span>

```c
UINT fx_unicode_short_name_get_extended(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *destination_short_name,
    ULONG short_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="08a18-3674">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08a18-3674">Description</span></span>

<span data-ttu-id="08a18-3675">Questo servizio recupera il nome breve (formato 8,3) associato al nome Unicode all'interno della directory predefinita corrente. nel parametro del nome Unicode non sono consentite informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="08a18-3675">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="08a18-3676">In caso di esito positivo, il nome breve associato al nome Unicode viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="08a18-3676">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a18-3677">*Questo servizio è identico a **fx_unicode_short_name_get ()**, ad eccezione del chiamante che fornisce la dimensione del buffer di destinazione come argomento di input. Ciò consente al servizio di garantire che il nome breve non superi il buffer di destinazione.*</span><span class="sxs-lookup"><span data-stu-id="08a18-3677">*This service is identical to **fx_unicode_short_name_get()**, except the caller supplies the size of the destination buffer as an input argument. This allows the service to guarantee the short name does not exceed the destination buffer.*</span></span>

<span data-ttu-id="08a18-3678">*Questo servizio può essere usato per ottenere nomi brevi per i file e le sottodirectory*</span><span class="sxs-lookup"><span data-stu-id="08a18-3678">*This service can be used to get short names for both files and subdirectories*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="08a18-3679">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="08a18-3679">Input Parameters</span></span>

- <span data-ttu-id="08a18-3680">**media_ptr**: puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="08a18-3680">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="08a18-3681">**source_unicode_name**: puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3681">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="08a18-3682">**source_unicode_length**: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="08a18-3682">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="08a18-3683">**destination_short_name**: puntatore alla destinazione per il nome breve (formato 8,3).</span><span class="sxs-lookup"><span data-stu-id="08a18-3683">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="08a18-3684">Deve avere una dimensione di almeno 13 byte.</span><span class="sxs-lookup"><span data-stu-id="08a18-3684">This must be at least 13 bytes in size.</span></span>
- <span data-ttu-id="08a18-3685">**short_name_buffer_length**: dimensione del buffer di destinazione.</span><span class="sxs-lookup"><span data-stu-id="08a18-3685">**short_name_buffer_length**: Size of the destination buffer.</span></span> <span data-ttu-id="08a18-3686">La dimensione del buffer deve essere di almeno 14 byte.</span><span class="sxs-lookup"><span data-stu-id="08a18-3686">The buffer size must be at least 14 bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="08a18-3687">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="08a18-3687">Return Values</span></span>

- <span data-ttu-id="08a18-3688">**FX_SUCCESS** (0x00) il recupero del nome breve riuscito.</span><span class="sxs-lookup"><span data-stu-id="08a18-3688">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="08a18-3689">**FX_FAT_READ_ERROR** (0X03) non è in grado di leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="08a18-3689">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="08a18-3690">Il file di **FX_FILE_CORRUPT** (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="08a18-3690">**FX_FILE_CORRUPT** (0x08)    File is corrupted</span></span>
- <span data-ttu-id="08a18-3691">Errore di I/O del driver **FX_IO_ERROR** (0x90).</span><span class="sxs-lookup"><span data-stu-id="08a18-3691">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="08a18-3692">Il supporto specificato **FX_MEDIA_NOT_OPEN** (0x11) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="08a18-3692">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="08a18-3693">Impossibile trovare il nome Unicode **FX_NOT_FOUND** (0x04).</span><span class="sxs-lookup"><span data-stu-id="08a18-3693">**FX_NOT_FOUND** (0x04) Unicode name was not found.</span></span>
- <span data-ttu-id="08a18-3694">Il servizio **FX_NOT_IMPLEMENTED** (0x22) non è implementato per exFAT file System.</span><span class="sxs-lookup"><span data-stu-id="08a18-3694">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="08a18-3695">Settore **FX_SECTOR_INVALID** (0X89) non valido.</span><span class="sxs-lookup"><span data-stu-id="08a18-3695">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="08a18-3696">**FX_PTR_ERROR** (0x18) i puntatori ai supporti o ai nomi non validi.</span><span class="sxs-lookup"><span data-stu-id="08a18-3696">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="08a18-3697">Il chiamante **FX_CALLER_ERROR** (0x20) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="08a18-3697">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="08a18-3698">Consentito da</span><span class="sxs-lookup"><span data-stu-id="08a18-3698">Allowed From</span></span>

<span data-ttu-id="08a18-3699">Thread</span><span class="sxs-lookup"><span data-stu-id="08a18-3699">Threads</span></span>

### <a name="example"></a><span data-ttu-id="08a18-3700">Esempio</span><span class="sxs-lookup"><span data-stu-id="08a18-3700">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="08a18-3701">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="08a18-3701">See Also</span></span>

- <span data-ttu-id="08a18-3702">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3702">fx_file_allocate</span></span>
- <span data-ttu-id="08a18-3703">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3703">fx_file_attributes_read</span></span>
- <span data-ttu-id="08a18-3704">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3704">fx_file_attributes_set</span></span>
- <span data-ttu-id="08a18-3705">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3705">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3706">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="08a18-3706">fx_file_close</span></span>
- <span data-ttu-id="08a18-3707">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3707">fx_file_create</span></span>
- <span data-ttu-id="08a18-3708">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3708">fx_file_date_time_set</span></span>
- <span data-ttu-id="08a18-3709">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="08a18-3709">fx_file_delete</span></span>
- <span data-ttu-id="08a18-3710">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3710">fx_file_extended_allocate</span></span>
- <span data-ttu-id="08a18-3711">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="08a18-3711">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="08a18-3712">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3712">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="08a18-3713">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3713">fx_file_extended_seek</span></span>
- <span data-ttu-id="08a18-3714">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3714">fx_file_extended_truncate</span></span>
- <span data-ttu-id="08a18-3715">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3715">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="08a18-3716">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="08a18-3716">fx_file_open</span></span>
- <span data-ttu-id="08a18-3717">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="08a18-3717">fx_file_read</span></span>
- <span data-ttu-id="08a18-3718">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3718">fx_file_relative_seek</span></span>
- <span data-ttu-id="08a18-3719">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3719">fx_file_rename</span></span>
- <span data-ttu-id="08a18-3720">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="08a18-3720">fx_file_seek</span></span>
- <span data-ttu-id="08a18-3721">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="08a18-3721">fx_file_truncate</span></span>
- <span data-ttu-id="08a18-3722">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="08a18-3722">fx_file_truncate_release</span></span>
- <span data-ttu-id="08a18-3723">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="08a18-3723">fx_file_write</span></span>
- <span data-ttu-id="08a18-3724">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="08a18-3724">fx_file_write_notify_set</span></span>
- <span data-ttu-id="08a18-3725">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="08a18-3725">fx_unicode_file_create</span></span>
- <span data-ttu-id="08a18-3726">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="08a18-3726">fx_unicode_file_rename</span></span>
- <span data-ttu-id="08a18-3727">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3727">fx_unicode_name_get</span></span>
- <span data-ttu-id="08a18-3728">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="08a18-3728">fx_unicode_short_name_get</span></span>
