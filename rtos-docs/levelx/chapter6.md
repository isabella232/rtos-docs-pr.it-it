---
title: Capitolo 6-Azure RTO LevelX o API
description: LevelX o API RTO di Azure disponibili per l'applicazione.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3ab7d3a7e431d7c8f49ef4f5cab9216dc77c8d33
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822955"
---
# <a name="chapter-6---azure-rtos-levelx-nor-apis"></a><span data-ttu-id="94dfd-103">Capitolo 6-Azure RTO LevelX o API</span><span class="sxs-lookup"><span data-stu-id="94dfd-103">Chapter 6 - Azure RTOS LevelX NOR APIs</span></span>

<span data-ttu-id="94dfd-104">Le funzioni API o LevelX di Azure RTO non sono disponibili per l'applicazione, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="94dfd-104">The Azure RTOS LevelX NOR API functions available to the application are as follows.</span></span>

- <span data-ttu-id="94dfd-105">\***lx_nor_flash_close** _: _Close o l'istanza Flash \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-105">***lx_nor_flash_close** _: _Close NOR flash instance*</span></span>
- <span data-ttu-id="94dfd-106">\***lx_nor_flash_defragment** _: _Defragment o l'istanza Flash \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-106">***lx_nor_flash_defragment** _: _Defragment NOR flash instance*</span></span>
- <span data-ttu-id="94dfd-107">\***lx_nor_flash_extended_cache_enable** _: _Enable/Disable esteso o cache \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-107">***lx_nor_flash_extended_cache_enable** _: _Enable/disable extended NOR cache*</span></span>
- <span data-ttu-id="94dfd-108">\***lx_nor_flash_initialize** _: _Initialize o supporto Flash \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-108">***lx_nor_flash_initialize** _: _Initialize NOR flash support*</span></span>
- <span data-ttu-id="94dfd-109">\***lx_nor_flash_open** _: _Open o l'istanza Flash \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-109">***lx_nor_flash_open** _: _Open NOR flash instance*</span></span>
- <span data-ttu-id="94dfd-110">\***lx_nor_flash_partial_defragment** _: _Partial deframmentazione di o di un'istanza Flash \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-110">***lx_nor_flash_partial_defragment** _: _Partial defragment of NOR flash instance*</span></span>
- <span data-ttu-id="94dfd-111">\***lx_nor_flash_sector_read** _: _Read o settore Flash \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-111">***lx_nor_flash_sector_read** _: _Read NOR flash sector*</span></span>
- <span data-ttu-id="94dfd-112">\***lx_nor_flash_sector_release** _: _Release o settore Flash \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-112">***lx_nor_flash_sector_release** _: _Release NOR flash sector*</span></span>
- <span data-ttu-id="94dfd-113">\***lx_nor_flash_sector_write** _: _Write o settore Flash \*</span><span class="sxs-lookup"><span data-stu-id="94dfd-113">***lx_nor_flash_sector_write** _: _Write NOR flash sector*</span></span>

## <a name="lx_nor_flash_close"></a><span data-ttu-id="94dfd-114">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-114">lx_nor_flash_close</span></span>

<span data-ttu-id="94dfd-115">Istanza Close o Flash</span><span class="sxs-lookup"><span data-stu-id="94dfd-115">Close NOR flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-116">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-116">Prototype</span></span>

```c
UINT lx_nor_flash_close(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a><span data-ttu-id="94dfd-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-117">Description</span></span>

<span data-ttu-id="94dfd-118">Questo servizio chiude l'istanza precedentemente aperta o Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-118">This service closes the previously opened NOR flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-119">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-119">Input Parameters</span></span>

- <span data-ttu-id="94dfd-120">*nor_flash*: né puntatore all'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-120">*nor_flash*: NOR flash instance pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-121">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-121">Return Values</span></span>

- <span data-ttu-id="94dfd-122">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-122">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-123">**LX_ERROR**: (0x01) errore durante la chiusura dell'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-123">**LX_ERROR**: (0x01) Error closing flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-124">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-124">Allowed From</span></span>

<span data-ttu-id="94dfd-125">Thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-125">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-126">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-126">Example</span></span>

```c
/* Close NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_close(&my_nor_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-127">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-127">See Also</span></span>

- <span data-ttu-id="94dfd-128">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-128">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="94dfd-129">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-129">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="94dfd-130">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-130">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="94dfd-131">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-131">lx_nor_flash_open</span></span>
- <span data-ttu-id="94dfd-132">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-132">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="94dfd-133">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-133">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="94dfd-134">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-134">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="94dfd-135">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-135">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_defragment"></a><span data-ttu-id="94dfd-136">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-136">lx_nor_flash_defragment</span></span>

<span data-ttu-id="94dfd-137">Deframmenta o istanza Flash</span><span class="sxs-lookup"><span data-stu-id="94dfd-137">Defragment NOR flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-138">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-138">Prototype</span></span>

```c
UINT lx_nor_flash_defragment(LX_NOR_FLASH *nor_flash);
```

### <a name="description"></a><span data-ttu-id="94dfd-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-139">Description</span></span>

<span data-ttu-id="94dfd-140">Questo servizio Deframmenta l'istanza precedentemente aperta o Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-140">This service defragments the previously opened NOR flash instance.</span></span> <span data-ttu-id="94dfd-141">Il processo di deframmentazione ottimizza il numero di settori e blocchi liberi.</span><span class="sxs-lookup"><span data-stu-id="94dfd-141">The defragment process maximizes the number of free sectors and blocks.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-142">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-142">Input Parameters</span></span>

- <span data-ttu-id="94dfd-143">*nor_flash*: né puntatore all'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-143">*nor_flash*: NOR flash instance pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-144">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-144">Return Values</span></span>

- <span data-ttu-id="94dfd-145">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-145">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-146">**LX_ERROR**: (0x01) errore durante la deframmentazione dell'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-146">**LX_ERROR**: (0x01) Error defragmenting flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-147">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-147">Allowed From</span></span>

<span data-ttu-id="94dfd-148">Thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-148">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-149">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-149">Example</span></span>

```c
/* Defragment NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_defragment(&my_nor_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-150">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-150">See Also</span></span>

- <span data-ttu-id="94dfd-151">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-151">lx_nor_flash_close</span></span>
- <span data-ttu-id="94dfd-152">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-152">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="94dfd-153">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-153">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="94dfd-154">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-154">lx_nor_flash_open</span></span>
- <span data-ttu-id="94dfd-155">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-155">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="94dfd-156">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-156">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="94dfd-157">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-157">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="94dfd-158">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-158">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_extended_cache_enable"></a><span data-ttu-id="94dfd-159">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-159">lx_nor_flash_extended_cache_enable</span></span>

<span data-ttu-id="94dfd-160">Abilita/Disabilita esteso o cache</span><span class="sxs-lookup"><span data-stu-id="94dfd-160">Enable/disable extended NOR cache</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-161">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-161">Prototype</span></span>

```c
UINT lx_nor_flash_extended_cache_enable(
    LX_NOR_FLASH *nor_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="94dfd-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-162">Description</span></span>

<span data-ttu-id="94dfd-163">Questo servizio implementa un livello di cache del settore o nella RAM usando la memoria fornita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94dfd-163">This service implements a NOR sector cache layer in RAM using the memory supplied by the application.</span></span> <span data-ttu-id="94dfd-164">Ogni 512 byte di memoria fornita si traduce in uno o più settori che possono essere memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="94dfd-164">Each 512 bytes of memory supplied translates to one NOR sector that can be cached.</span></span> <span data-ttu-id="94dfd-165">I settori memorizzati nella cache sono quelli che contengono le informazioni sul controllo del blocco, ad esempio il conteggio delle cancellazioni, la mappa del settore gratuito e le informazioni sul mapping del settore.</span><span class="sxs-lookup"><span data-stu-id="94dfd-165">The sectors cached are those that contain the block control information, e.g., erase count, free sector map, and sector mapping information.</span></span> <span data-ttu-id="94dfd-166">I settori dati non vengono archiviati in questa cache.</span><span class="sxs-lookup"><span data-stu-id="94dfd-166">Data sectors are not stored in this cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-167">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-167">Input Parameters</span></span>

- <span data-ttu-id="94dfd-168">**nor_flash**: né puntatore all'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-168">**nor_flash**: NOR flash instance pointer.</span></span>  
- <span data-ttu-id="94dfd-169">**Memory**: indirizzo iniziale per la memoria cache, allineato per l'accesso ULONG.</span><span class="sxs-lookup"><span data-stu-id="94dfd-169">**memory**: Starting address for cache memory, aligned for ULONG access.</span></span> <span data-ttu-id="94dfd-170">Il valore LX_NULL Disabilita la cache.</span><span class="sxs-lookup"><span data-stu-id="94dfd-170">A value of LX_NULL disables the cache.</span></span>  
- <span data-ttu-id="94dfd-171">**size**: dimensione in byte della memoria fornita (deve essere un multiplo di 512 byte).</span><span class="sxs-lookup"><span data-stu-id="94dfd-171">**size**: The size in bytes of the memory supplied (should be multiple of 512 bytes).</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-172">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-172">Return Values</span></span>

- <span data-ttu-id="94dfd-173">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-173">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-174">**LX_ERROR**: (0x01) memoria insufficiente per uno o più settori.</span><span class="sxs-lookup"><span data-stu-id="94dfd-174">**LX_ERROR**: (0x01) Not enough memory for one NOR sector.</span></span>
- <span data-ttu-id="94dfd-175">**LX_DISABLED**: (0x09) o la cache estesa disabilitata dall'opzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="94dfd-175">**LX_DISABLED**: (0x09) NOR extended cache disabled by configuration option.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-176">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-176">Allowed From</span></span>

<span data-ttu-id="94dfd-177">Thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-177">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-178">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-178">Example</span></span>

```c
/* Enable the NOR flash cache for the instance "my_nor_flash". */  
status = lx_nor_flash_extended_cache_enable(&my_nor_flash,  
    &my_memory, sizeof(my_memory));  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-179">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-179">See Also</span></span>

- <span data-ttu-id="94dfd-180">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-180">lx_nor_flash_close</span></span>
- <span data-ttu-id="94dfd-181">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-181">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="94dfd-182">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-182">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="94dfd-183">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-183">lx_nor_flash_open</span></span>
- <span data-ttu-id="94dfd-184">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-184">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="94dfd-185">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-185">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="94dfd-186">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-186">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="94dfd-187">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-187">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_initialize"></a><span data-ttu-id="94dfd-188">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-188">lx_nor_flash_initialize</span></span>

<span data-ttu-id="94dfd-189">Inizializzazione o supporto Flash</span><span class="sxs-lookup"><span data-stu-id="94dfd-189">Initialize NOR flash support</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-190">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-190">Prototype</span></span>

```c
UINT lx_nor_flash_initialize(void);
```

### <a name="description"></a><span data-ttu-id="94dfd-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-191">Description</span></span>

<span data-ttu-id="94dfd-192">Questo servizio Inizializza LevelX o il supporto Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-192">This service initializes LevelX NOR flash support.</span></span> <span data-ttu-id="94dfd-193">Deve essere chiamato prima di qualsiasi altro LevelX o API.</span><span class="sxs-lookup"><span data-stu-id="94dfd-193">It must be called before any other LevelX NOR APIs.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-194">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-194">Input Parameters</span></span>

- <span data-ttu-id="94dfd-195">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="94dfd-195">**None**</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-196">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-196">Return Values</span></span>

- <span data-ttu-id="94dfd-197">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-197">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-198">**LX_ERROR**: (0x01) errore durante l'INIZIALIZZAzione o il supporto Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-198">**LX_ERROR**: (0x01) Error initializing NOR flash support.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-199">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-199">Allowed From</span></span>

<span data-ttu-id="94dfd-200">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-200">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-201">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-201">Example</span></span>

```c
/* Initialize NOR flash support. */  
status = lx_nor_flash_initialize();  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-202">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-202">See Also</span></span>

- <span data-ttu-id="94dfd-203">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-203">lx_nor_flash_close</span></span>
- <span data-ttu-id="94dfd-204">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-204">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="94dfd-205">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-205">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="94dfd-206">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-206">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="94dfd-207">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-207">lx_nor_flash_open</span></span>
- <span data-ttu-id="94dfd-208">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-208">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="94dfd-209">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-209">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="94dfd-210">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-210">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_open"></a><span data-ttu-id="94dfd-211">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-211">lx_nor_flash_open</span></span>

<span data-ttu-id="94dfd-212">Apri o istanza Flash</span><span class="sxs-lookup"><span data-stu-id="94dfd-212">Open NOR flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-213">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-213">Prototype</span></span>

```c
UINT lx_nor_flash_open(
    LX_NOR_FLASH *nor_flash, 
    CHAR *name,  
    UINT (*nor_driver_initialize) (LX_NOR_FLASH *));
```

### <a name="description"></a><span data-ttu-id="94dfd-214">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-214">Description</span></span>

<span data-ttu-id="94dfd-215">Questo servizio apre un'istanza di o Flash con la funzione di inizializzazione del driver e del blocco di controllo flash specificata.</span><span class="sxs-lookup"><span data-stu-id="94dfd-215">This service opens a NOR flash instance with the specified NOR flash control block and driver initialization function.</span></span> <span data-ttu-id="94dfd-216">Si noti che la funzione di inizializzazione del driver è responsabile dell'installazione di diversi puntatori a funzione per la lettura, la scrittura e la cancellazione dei blocchi dell'hardware o dell'hardware associato a questa istanza di o Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-216">Note that the driver initialization function is responsible for installing various function pointers for reading, writing, and erasing blocks of the NOR hardware associated with this NOR flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-217">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-217">Input Parameters</span></span>

- <span data-ttu-id="94dfd-218">*nor_flash*: né puntatore all'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-218">*nor_flash*: NOR flash instance pointer.</span></span>
- <span data-ttu-id="94dfd-219">*nome*: nome dell'istanza di o Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-219">*name*: Name of NOR flash instance.</span></span>
- <span data-ttu-id="94dfd-220">*nor_driver_initialize*: puntatore a funzione o funzione di inizializzazione del driver Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-220">*nor_driver_initialize*: Function pointer to NOR flash driver Initialization function.</span></span> <span data-ttu-id="94dfd-221">Vedere il capitolo 5 di questa guida per altre informazioni sulle responsabilità dei driver di o Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-221">Please refer to Chapter 5 of this guide for more details on NOR flash driver responsibilities.</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-222">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-222">Return Values</span></span>

- <span data-ttu-id="94dfd-223">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-223">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-224">**LX_ERROR**: (0x01) errore durante l'apertura o l'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-224">**LX_ERROR**: (0x01) Error opening NOR flash instance.</span></span>
- <span data-ttu-id="94dfd-225">**LX_NO_MEMORY**: il driver (0x08) non ha fornito il buffer per la lettura di nessun settore nella RAM.</span><span class="sxs-lookup"><span data-stu-id="94dfd-225">**LX_NO_MEMORY**:  (0x08) Driver did not provide buffer for reading none sector into RAM.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-226">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-226">Allowed From</span></span>

<span data-ttu-id="94dfd-227">Thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-227">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-228">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-228">Example</span></span>

```c
/* Open NOR flash instance "my_nor_flash" with the driver "my_nor_driver_initialize". */  
status = lx_nor_flash_open(&my_nor_flash,"my NOR flash",  
    my_nor_driver_initialize);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-229">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-229">See Also</span></span>

- <span data-ttu-id="94dfd-230">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-230">lx_nor_flash_close</span></span>
- <span data-ttu-id="94dfd-231">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-231">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="94dfd-232">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-232">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="94dfd-233">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-233">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="94dfd-234">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-234">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="94dfd-235">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-235">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="94dfd-236">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-236">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="94dfd-237">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-237">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_partial_defragment"></a><span data-ttu-id="94dfd-238">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-238">lx_nor_flash_partial_defragment</span></span>

<span data-ttu-id="94dfd-239">Deframmentazione parziale dell'istanza di o di Flash</span><span class="sxs-lookup"><span data-stu-id="94dfd-239">Partial defragment of NOR flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-240">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-240">Prototype</span></span>

```c
UINT lx_nor_flash_partial_defragment(
    LX_NOR_FLASH *nor_flash, 
    UINT max_blocks);
```

### <a name="description"></a><span data-ttu-id="94dfd-241">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-241">Description</span></span>

<span data-ttu-id="94dfd-242">Questo servizio Deframmenta l'istanza precedentemente aperta o flash fino al numero massimo di blocchi specificato.</span><span class="sxs-lookup"><span data-stu-id="94dfd-242">This service defragments the previously opened NOR flash instance up to the maximum number of blocks specified.</span></span> <span data-ttu-id="94dfd-243">Il processo di deframmentazione ottimizza il numero di settori e blocchi liberi.</span><span class="sxs-lookup"><span data-stu-id="94dfd-243">The defragment process maximizes the number of free sectors and blocks.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-244">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-244">Input Parameters</span></span>

- <span data-ttu-id="94dfd-245">*nor_flash*: né puntatore all'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-245">*nor_flash*: NOR flash instance pointer.</span></span>
- <span data-ttu-id="94dfd-246">*max_blocks*: numero massimo di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94dfd-246">*max_blocks*: Maximum number of blocks.</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-247">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-247">Return Values</span></span>

- <span data-ttu-id="94dfd-248">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-248">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-249">**LX_ERROR**: (0x01) errore durante la deframmentazione dell'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-249">**LX_ERROR**: (0x01) Error defragmenting flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-250">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-250">Allowed From</span></span>

<span data-ttu-id="94dfd-251">Thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-251">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-252">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-252">Example</span></span>

```c
/* Defragment of one block in NOR flash instance* *"my_nor_flash". */  
status = lx_nor_flash_partial_defragment(&my_nor_flash, 1);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-253">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-253">See Also</span></span>

- <span data-ttu-id="94dfd-254">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-254">lx_nor_flash_close</span></span>
- <span data-ttu-id="94dfd-255">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-255">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="94dfd-256">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-256">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="94dfd-257">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-257">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="94dfd-258">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-258">lx_nor_flash_open</span></span>
- <span data-ttu-id="94dfd-259">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-259">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="94dfd-260">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-260">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="94dfd-261">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-261">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_sector_read"></a><span data-ttu-id="94dfd-262">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-262">lx_nor_flash_sector_read</span></span>

<span data-ttu-id="94dfd-263">Lettura e settore Flash</span><span class="sxs-lookup"><span data-stu-id="94dfd-263">Read NOR flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-264">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-264">Prototype</span></span>

```c
UINT lx_nor_flash_sector_read(
    LX_NOR_FLASH *nor_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a><span data-ttu-id="94dfd-265">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-265">Description</span></span>

<span data-ttu-id="94dfd-266">Questo servizio legge il settore logico dall'istanza di o Flash e, se ha esito positivo, restituisce il contenuto nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="94dfd-266">This service reads the logical sector from the NOR flash instance and if successful returns the contents in the supplied buffer.</span></span> <span data-ttu-id="94dfd-267">Si noti che la dimensione del settore è sempre di 512 byte.</span><span class="sxs-lookup"><span data-stu-id="94dfd-267">Note that NOR sector size is always 512 bytes.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-268">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-268">Input Parameters</span></span>

- <span data-ttu-id="94dfd-269">*nor_flash* O puntatore all'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-269">*nor_flash* NOR flash instance pointer.</span></span>
- <span data-ttu-id="94dfd-270">*logical_sector*: settore logico da leggere.</span><span class="sxs-lookup"><span data-stu-id="94dfd-270">*logical_sector*: Logical sector to read.</span></span>
- <span data-ttu-id="94dfd-271">*buffer*: puntatore alla destinazione per il contenuto del settore logico.</span><span class="sxs-lookup"><span data-stu-id="94dfd-271">*buffer*: Pointer to destination for contents of the logical sector.</span></span> <span data-ttu-id="94dfd-272">Si presuppone che il buffer sia 512 byte e che sia allineato per l'accesso ULONG.</span><span class="sxs-lookup"><span data-stu-id="94dfd-272">Note that the buffer is assumed to be 512 bytes and aligned for ULONG access.</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-273">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-273">Return Values</span></span>

- <span data-ttu-id="94dfd-274">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-274">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-275">**LX_ERROR**: (0x01) errore durante la lettura o il settore Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-275">**LX_ERROR**: (0x01) Error reading NOR flash sector.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-276">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-276">Allowed From</span></span>

<span data-ttu-id="94dfd-277">Thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-277">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-278">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-278">Example</span></span>

```c
/* Read logical sector 20 of the NOR flash instance "my_nor_flash" and place contents in "buffer". */ 
status = lx_nor_flash_sector_read(&my_nor_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, "buffer" contains the contents of logical sector 20. */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-279">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-279">See Also</span></span>

- <span data-ttu-id="94dfd-280">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-280">lx_nor_flash_close</span></span>
- <span data-ttu-id="94dfd-281">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-281">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="94dfd-282">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-282">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="94dfd-283">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-283">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="94dfd-284">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-284">lx_nor_flash_open</span></span>
- <span data-ttu-id="94dfd-285">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-285">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="94dfd-286">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-286">lx_nor_flash_sector_release</span></span>
- <span data-ttu-id="94dfd-287">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-287">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_sector_release"></a><span data-ttu-id="94dfd-288">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-288">lx_nor_flash_sector_release</span></span>

<span data-ttu-id="94dfd-289">Versione o settore Flash</span><span class="sxs-lookup"><span data-stu-id="94dfd-289">Release NOR flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-290">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-290">Prototype</span></span>

```c
UINT lx_nor_flash_sector_release(
    LX_NOR_FLASH *nor_flash,
    ULONG logical_sector);
```

### <a name="description"></a><span data-ttu-id="94dfd-291">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-291">Description</span></span>

<span data-ttu-id="94dfd-292">Questo servizio rilascia il mapping del settore logico nell'istanza di o di Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-292">This service releases the logical sector mapping in the NOR flash instance.</span></span> <span data-ttu-id="94dfd-293">Il rilascio di un settore logico quando non viene usato rende più efficiente il livellamento del LevelX.</span><span class="sxs-lookup"><span data-stu-id="94dfd-293">Releasing a logical sector when not used makes the LevelX wear leveling more efficient.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-294">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-294">Input Parameters</span></span>

- <span data-ttu-id="94dfd-295">*nor_flash*: né puntatore all'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-295">*nor_flash*: NOR flash instance pointer.</span></span>
- <span data-ttu-id="94dfd-296">*logical_sector*: settore logico da rilasciare.</span><span class="sxs-lookup"><span data-stu-id="94dfd-296">*logical_sector*: Logical sector to release.</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-297">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-297">Return Values</span></span>

- <span data-ttu-id="94dfd-298">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-298">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-299">**LX_ERROR**: (0x01) errore o scrittura nel settore Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-299">**LX_ERROR**: (0x01) Error NOR flash sector write.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-300">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-300">Allowed From</span></span>

<span data-ttu-id="94dfd-301">Thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-301">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-302">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-302">Example</span></span>

```c
/* Release logical sector 20 of the NOR flash instance "my_nor_flash". */  
status = lx_nor_flash_sector_release(&my_nor_flash, 20);  
  
/* If status is LX_SUCCESS, logical sector 20 has been released. */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-303">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-303">See Also</span></span>

- <span data-ttu-id="94dfd-304">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-304">lx_nor_flash_close</span></span>
- <span data-ttu-id="94dfd-305">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-305">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="94dfd-306">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-306">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="94dfd-307">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-307">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="94dfd-308">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-308">lx_nor_flash_open</span></span>
- <span data-ttu-id="94dfd-309">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-309">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="94dfd-310">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-310">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="94dfd-311">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-311">lx_nor_flash_sector_write</span></span>

## <a name="lx_nor_flash_sector_write"></a><span data-ttu-id="94dfd-312">lx_nor_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="94dfd-312">lx_nor_flash_sector_write</span></span>

<span data-ttu-id="94dfd-313">Settore della scrittura e del flash</span><span class="sxs-lookup"><span data-stu-id="94dfd-313">Write NOR flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="94dfd-314">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94dfd-314">Prototype</span></span>

```c
UINT lx_nor_flash_sector_write(
    LX_nor_FLASH *NOR_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a><span data-ttu-id="94dfd-315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94dfd-315">Description</span></span>

<span data-ttu-id="94dfd-316">Questo servizio scrive il settore logico specificato nell'istanza di o Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-316">This service writes the specified logical sector in the NOR flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="94dfd-317">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="94dfd-317">Input Parameters</span></span>

- <span data-ttu-id="94dfd-318">*nor_flash*: né puntatore all'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-318">*nor_flash*: NOR flash instance pointer.</span></span>
- <span data-ttu-id="94dfd-319">*logical_sector*: settore logico da scrivere.</span><span class="sxs-lookup"><span data-stu-id="94dfd-319">*logical_sector*: Logical sector to write.</span></span>
- <span data-ttu-id="94dfd-320">*buffer*: puntatore al contenuto del settore logico.</span><span class="sxs-lookup"><span data-stu-id="94dfd-320">*buffer*: Pointer to the contents of the logical sector.</span></span> <span data-ttu-id="94dfd-321">Si presuppone che il buffer sia allineato a 512 byte per l'accesso ULONG.</span><span class="sxs-lookup"><span data-stu-id="94dfd-321">Note that the buffer is assumed to be 512 bytes aligned for ULONG access.</span></span>

### <a name="return-values"></a><span data-ttu-id="94dfd-322">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94dfd-322">Return Values</span></span>

- <span data-ttu-id="94dfd-323">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94dfd-323">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="94dfd-324">**LX_NO_SECTORS**: (0x02) non sono più disponibili settori gratuiti per eseguire la scrittura.</span><span class="sxs-lookup"><span data-stu-id="94dfd-324">**LX_NO_SECTORS**: (0x02) No more free sectors are available to perform the write.</span></span>
- <span data-ttu-id="94dfd-325">**LX_ERROR**: (0x01) errore durante il rilascio o il settore Flash.</span><span class="sxs-lookup"><span data-stu-id="94dfd-325">**LX_ERROR**: (0x01) Error releasing NOR flash sector.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94dfd-326">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94dfd-326">Allowed From</span></span>

<span data-ttu-id="94dfd-327">Thread</span><span class="sxs-lookup"><span data-stu-id="94dfd-327">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94dfd-328">Esempio</span><span class="sxs-lookup"><span data-stu-id="94dfd-328">Example</span></span>

```c
/* Write logical sector 20 of the NOR flash instance "my_nor_flash" with the contents pointed to by "buffer". */ 
status = lx_nor_flash_sector_write(&my_nor_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, logical sector 20 has been written with the contents of "buffer". */
```

### <a name="see-also"></a><span data-ttu-id="94dfd-329">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94dfd-329">See Also</span></span>

- <span data-ttu-id="94dfd-330">lx_nor_flash_close</span><span class="sxs-lookup"><span data-stu-id="94dfd-330">lx_nor_flash_close</span></span>
- <span data-ttu-id="94dfd-331">lx_nor_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-331">lx_nor_flash_defragment</span></span>
- <span data-ttu-id="94dfd-332">lx_nor_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="94dfd-332">lx_nor_flash_extended_cache_enable</span></span>
- <span data-ttu-id="94dfd-333">lx_nor_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="94dfd-333">lx_nor_flash_initialize</span></span>
- <span data-ttu-id="94dfd-334">lx_nor_flash_open</span><span class="sxs-lookup"><span data-stu-id="94dfd-334">lx_nor_flash_open</span></span>
- <span data-ttu-id="94dfd-335">lx_nor_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="94dfd-335">lx_nor_flash_partial_defragment</span></span>
- <span data-ttu-id="94dfd-336">lx_nor_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="94dfd-336">lx_nor_flash_sector_read</span></span>
- <span data-ttu-id="94dfd-337">lx_nor_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="94dfd-337">lx_nor_flash_sector_release</span></span>
