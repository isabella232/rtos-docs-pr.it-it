---
title: Capitolo 4-API NAND LevelX di Azure RTO
description: API di Azure RTO LevelX NAND disponibili per l'applicazione.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 73bb94768396b4b8461791a164a102d1f8ef159f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822967"
---
# <a name="chapter-4---azure-rtos-levelx-nand-apis"></a><span data-ttu-id="c9044-103">Capitolo 4-API NAND LevelX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="c9044-103">Chapter 4 - Azure RTOS LevelX NAND APIs</span></span>

<span data-ttu-id="c9044-104">Le API di Azure RTO LevelX NAND disponibili per l'applicazione sono:</span><span class="sxs-lookup"><span data-stu-id="c9044-104">The Azure RTOS LevelX NAND APIs available to the application are:</span></span>

- <span data-ttu-id="c9044-105">\***lx_nand_flash_close** _: _Close istanza Flash NAND \*</span><span class="sxs-lookup"><span data-stu-id="c9044-105">***lx_nand_flash_close** _: _Close NAND flash instance*</span></span>
- <span data-ttu-id="c9044-106">\***lx_nand_flash_defragment** _: _Defragment istanza Flash NAND \*</span><span class="sxs-lookup"><span data-stu-id="c9044-106">***lx_nand_flash_defragment** _: _Defragment NAND flash instance*</span></span>
- <span data-ttu-id="c9044-107">\***lx_nand_flash_extended_cache_enable** _: _Enable/Disable della cache NAND estesa \*</span><span class="sxs-lookup"><span data-stu-id="c9044-107">***lx_nand_flash_extended_cache_enable** _: _Enable/disable extended NAND cache*</span></span>
- <span data-ttu-id="c9044-108">\***lx_nand_flash_initialize** _: _Initialize supporto Flash NAND \*</span><span class="sxs-lookup"><span data-stu-id="c9044-108">***lx_nand_flash_initialize** _: _Initialize NAND flash support*</span></span>
- <span data-ttu-id="c9044-109">\***lx_nand_flash_open** _: _Open istanza Flash NAND \*</span><span class="sxs-lookup"><span data-stu-id="c9044-109">***lx_nand_flash_open** _: _Open NAND flash instance*</span></span>
- <span data-ttu-id="c9044-110">\***lx_nand_flash_page_ecc_check** _: _Check pagina per gli errori ecc con correzione \*</span><span class="sxs-lookup"><span data-stu-id="c9044-110">***lx_nand_flash_page_ecc_check** _: _Check page for ECC errors with correction*</span></span>
- <span data-ttu-id="c9044-111">\***lx_nand_flash_page_ecc_compute** _: _Computes ecc per la pagina \*</span><span class="sxs-lookup"><span data-stu-id="c9044-111">***lx_nand_flash_page_ecc_compute** _: _Computes ECC for page*</span></span>
- <span data-ttu-id="c9044-112">\***lx_nand_flash_partial_defragment** _: _Partial deframmentazione dell'istanza Flash NAND \*</span><span class="sxs-lookup"><span data-stu-id="c9044-112">***lx_nand_flash_partial_defragment** _: _Partial defragment of NAND flash instance*</span></span>
- <span data-ttu-id="c9044-113">\***lx_nand_flash_sector_read** _: _Read settore Flash NAND \*</span><span class="sxs-lookup"><span data-stu-id="c9044-113">***lx_nand_flash_sector_read** _: _Read NAND flash sector*</span></span>
- <span data-ttu-id="c9044-114">\***lx_nand_flash_sector_release** _: _Release settore Flash NAND \*</span><span class="sxs-lookup"><span data-stu-id="c9044-114">***lx_nand_flash_sector_release** _: _Release NAND flash sector*</span></span>
- <span data-ttu-id="c9044-115">\***lx_nand_flash_sector_write** _: _Write settore Flash NAND \*</span><span class="sxs-lookup"><span data-stu-id="c9044-115">***lx_nand_flash_sector_write** _: _Write NAND flash sector*</span></span>

## <a name="lx_nand_flash_close"></a><span data-ttu-id="c9044-116">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-116">lx_nand_flash_close</span></span>

<span data-ttu-id="c9044-117">Chiudi istanza Flash NAND</span><span class="sxs-lookup"><span data-stu-id="c9044-117">Close NAND flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-118">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-118">Prototype</span></span>

```c
UINT lx_nand_flash_close(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a><span data-ttu-id="c9044-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-119">Description</span></span>

<span data-ttu-id="c9044-120">Questo servizio chiude l'istanza Flash NAND precedentemente aperta.</span><span class="sxs-lookup"><span data-stu-id="c9044-120">This service closes the previously opened NAND flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-121">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-121">Input Parameters</span></span>

- <span data-ttu-id="c9044-122">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-122">**nand_flash**: NAND flash instance pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-123">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-123">Return Values</span></span>

- <span data-ttu-id="c9044-124">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-124">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-125">**LX_ERROR**: (0x01) errore durante la chiusura dell'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="c9044-125">**LX_ERROR**: (0x01) Error closing flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-126">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-126">Allowed From</span></span>

<span data-ttu-id="c9044-127">Thread</span><span class="sxs-lookup"><span data-stu-id="c9044-127">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-128">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-128">Example</span></span>

```c
/* Close NAND flash instance "my_nand_flash". */
status = lx_nand_flash_close(&my_nand_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-129">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-129">See Also</span></span>

- <span data-ttu-id="c9044-130">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-130">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-131">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-131">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-132">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-132">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-133">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-133">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-134">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-134">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-135">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-135">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-136">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-136">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-137">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-137">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-138">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-138">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-139">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-139">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_defragment"></a><span data-ttu-id="c9044-140">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-140">lx_nand_flash_defragment</span></span>

<span data-ttu-id="c9044-141">Deframmenta istanza Flash NAND</span><span class="sxs-lookup"><span data-stu-id="c9044-141">Defragment NAND flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-142">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-142">Prototype</span></span>

```c
UINT lx_nand_flash_defragment(LX_NAND_FLASH *nand_flash);
```

### <a name="description"></a><span data-ttu-id="c9044-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-143">Description</span></span>

<span data-ttu-id="c9044-144">Questo servizio Deframmenta l'istanza Flash NAND precedentemente aperta.</span><span class="sxs-lookup"><span data-stu-id="c9044-144">This service defragments the previously opened NAND flash instance.</span></span> <span data-ttu-id="c9044-145">Il processo di deframmentazione ottimizza il numero di pagine e blocchi liberi.</span><span class="sxs-lookup"><span data-stu-id="c9044-145">The defragment process maximizes the number of free pages and blocks.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-146">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-146">Input Parameters</span></span>

- <span data-ttu-id="c9044-147">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-147">**nand_flash**: NAND flash instance pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-148">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-148">Return Values</span></span>

- <span data-ttu-id="c9044-149">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-149">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-150">**LX_ERROR**: (0x01) errore durante la deframmentazione dell'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="c9044-150">**LX_ERROR**: (0x01) Error defragmenting flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-151">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-151">Allowed From</span></span>

<span data-ttu-id="c9044-152">Thread</span><span class="sxs-lookup"><span data-stu-id="c9044-152">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-153">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-153">Example</span></span>

```c
/* Defragment NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_defragment(&my_nand_flash);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-154">See Also</span></span>

- <span data-ttu-id="c9044-155">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-155">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-156">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-156">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-157">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-157">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-158">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-158">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-159">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-159">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-160">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-160">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-161">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-161">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-162">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-162">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-163">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-163">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-164">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-164">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_extended_cache_enable"></a><span data-ttu-id="c9044-165">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-165">lx_nand_flash_extended_cache_enable</span></span>

<span data-ttu-id="c9044-166">Abilita/Disabilita cache NAND estesa</span><span class="sxs-lookup"><span data-stu-id="c9044-166">Enable/disable extended NAND cache</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-167">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-167">Prototype</span></span>

```c
UINT lx_nand_flash_extended_cache_enable(
    LX_NAND_FLASH
    *nand_flash,  
    VOID *memory, 
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="c9044-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-168">Description</span></span>

<span data-ttu-id="c9044-169">Questo servizio implementa un livello di cache nella RAM usando la memoria fornita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c9044-169">This service implements a cache layer in RAM using the memory supplied by the application.</span></span> <span data-ttu-id="c9044-170">La quantità totale di memoria necessaria per l'operazione Full cache può essere calcolata nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c9044-170">The total amount of memory required for full cache operation can be calculated as follows:</span></span>

```c
size (in_bytes) = number_of_blocks (rounded up to be divisible by 4) +  
    ((number_of_blocks * pages_per_block) * 4)  +  
    ((number_of_blocks * (pages_per_block + 1)) * 4)
```

<span data-ttu-id="c9044-171">Se la memoria fornita non è sufficientemente grande da contenere la cache NAND completa, questa routine consentirà la maggior parte della cache del flash NAND in base alla memoria fornita.</span><span class="sxs-lookup"><span data-stu-id="c9044-171">If the supplied memory is not large enough to accommodate the full NAND cache, this routine will enable as much of the NAND flash cache as possible based on the memory supplied.</span></span>

<span data-ttu-id="c9044-172">La cache NAND è disabilitata se l'indirizzo di memoria specificato è NULL.</span><span class="sxs-lookup"><span data-stu-id="c9044-172">The NAND cache is disabled if the memory address specified is NULL.</span></span> <span data-ttu-id="c9044-173">La cache NAND potrebbe quindi essere utilizzata in modo temporaneo.</span><span class="sxs-lookup"><span data-stu-id="c9044-173">Hence, the NAND cache maybe be used in a temporary fashion.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-174">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-174">Input Parameters</span></span>

- <span data-ttu-id="c9044-175">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-175">**nand_flash**: NAND flash instance pointer.</span></span>  
- <span data-ttu-id="c9044-176">**Memory**: indirizzo iniziale per la memoria cache allineata per l'accesso ULONG.</span><span class="sxs-lookup"><span data-stu-id="c9044-176">**memory**: Starting address for cache memory aligned for ULONG access.</span></span> <span data-ttu-id="c9044-177">Il valore LX_NULL Disabilita la cache.</span><span class="sxs-lookup"><span data-stu-id="c9044-177">A value of LX_NULL disables the cache.</span></span>  
- <span data-ttu-id="c9044-178">**size**: dimensione in byte della memoria fornita.</span><span class="sxs-lookup"><span data-stu-id="c9044-178">**size**: The size in bytes of the memory supplied.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-179">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-179">Return Values</span></span>

- <span data-ttu-id="c9044-180">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-180">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-181">**LX_ERROR**: (0x01) memoria insufficiente per un elemento della cache NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-181">**LX_ERROR**: (0x01) Not enough memory for one element of the NAND cache.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-182">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-182">Allowed From</span></span>

<span data-ttu-id="c9044-183">Thread</span><span class="sxs-lookup"><span data-stu-id="c9044-183">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-184">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-184">Example</span></span>

```c
/* Enable the NAND flash cache for the instance "my_nand_flash". */
status = lx_nand_flash_extended_cache_enable(&my_nand_flash,  
    &my_memory, sizeof(my_memory));  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-185">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-185">See Also</span></span>

- <span data-ttu-id="c9044-186">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-186">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-187">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-187">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-188">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-188">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-189">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-189">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-190">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-190">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-191">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-191">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-192">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-192">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-193">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-193">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-194">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-194">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-195">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-195">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_initialize"></a><span data-ttu-id="c9044-196">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-196">lx_nand_flash_initialize</span></span>

<span data-ttu-id="c9044-197">Inizializza supporto Flash NAND</span><span class="sxs-lookup"><span data-stu-id="c9044-197">Initialize NAND flash support</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-198">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-198">Prototype</span></span>

```c
UINT lx_nand_flash_initialize(void);
```

### <a name="description"></a><span data-ttu-id="c9044-199">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-199">Description</span></span>

<span data-ttu-id="c9044-200">Questo servizio Inizializza il supporto Flash NAND LevelX.</span><span class="sxs-lookup"><span data-stu-id="c9044-200">This service initializes LevelX NAND flash support.</span></span> <span data-ttu-id="c9044-201">Deve essere chiamato prima di qualsiasi altra API LevelX NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-201">It must be called before any other LevelX NAND APIs.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-202">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-202">Input Parameters</span></span>

- <span data-ttu-id="c9044-203">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="c9044-203">**None**</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-204">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-204">Return Values</span></span>

- <span data-ttu-id="c9044-205">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-205">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-206">**LX_ERROR**: (0x01) errore durante l'inizializzazione del supporto Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-206">**LX_ERROR**: (0x01) Error initializing NAND flash support.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-207">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-207">Allowed From</span></span>

<span data-ttu-id="c9044-208">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c9044-208">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-209">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-209">Example</span></span>

```c
/* Initialize NAND flash support. */
status = lx_nand_flash_initialize();  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-210">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-210">See Also</span></span>

- <span data-ttu-id="c9044-211">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-211">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-212">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-212">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-213">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-213">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-214">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-214">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-215">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-215">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-216">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-216">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-217">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-217">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-218">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-218">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-219">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-219">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-220">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-220">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_open"></a><span data-ttu-id="c9044-221">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-221">lx_nand_flash_open</span></span>

<span data-ttu-id="c9044-222">Apri istanza Flash NAND</span><span class="sxs-lookup"><span data-stu-id="c9044-222">Open NAND flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-223">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-223">Prototype</span></span>

```c
UINT lx_nand_flash_open(
    LX_NAND_FLASH *nand_flash, 
    CHAR *name,  
    UINT (*nand_driver_initialize) (LX_NAND_FLASH *));
```

### <a name="description"></a><span data-ttu-id="c9044-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-224">Description</span></span>

<span data-ttu-id="c9044-225">Questo servizio apre un'istanza di Flash NAND con il blocco di controllo flash NAND specificato e la funzione di inizializzazione del driver.</span><span class="sxs-lookup"><span data-stu-id="c9044-225">This service opens a NAND flash instance with the specified NAND flash control block and driver initialization function.</span></span> <span data-ttu-id="c9044-226">Si noti che la funzione di inizializzazione del driver è responsabile dell'installazione di diversi puntatori a funzione per la lettura, la scrittura e la cancellazione di blocchi/pagine dell'hardware NAND associato a questa istanza di Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-226">Note that the driver initialization function is responsible for installing various function pointers for reading, writing, and erasing blocks/pages of the NAND hardware associated with this NAND flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-227">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-227">Input Parameters</span></span>

- <span data-ttu-id="c9044-228">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-228">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="c9044-229">**nome**: nome dell'istanza di Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-229">**name**: Name of NAND flash instance.</span></span>
- <span data-ttu-id="c9044-230">**nand_driver_initialize**: puntatore a funzione per la funzione di inizializzazione del driver Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-230">**nand_driver_initialize**: Function pointer to NAND flash driver initialization function.</span></span> <span data-ttu-id="c9044-231">Per ulteriori informazioni sulle responsabilità dei driver Flash NAND, vedere il capitolo 3 di questa guida.</span><span class="sxs-lookup"><span data-stu-id="c9044-231">Please refer to Chapter 3 of this guide for more details on NAND flash driver responsibilities.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-232">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-232">Return Values</span></span>

- <span data-ttu-id="c9044-233">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-233">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-234">**LX_ERROR**: (0x01) errore durante l'apertura dell'istanza NAND Flash.</span><span class="sxs-lookup"><span data-stu-id="c9044-234">**LX_ERROR**: (0x01) Error opening NAND flash instance.</span></span>
- <span data-ttu-id="c9044-235">**LX_NO_MEMORY**: il driver (0x08) non ha fornito il buffer per la lettura di una pagina nella RAM.</span><span class="sxs-lookup"><span data-stu-id="c9044-235">**LX_NO_MEMORY**: (0x08) Driver did not provide buffer for reading one page into RAM.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-236">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-236">Allowed From</span></span>

<span data-ttu-id="c9044-237">Thread</span><span class="sxs-lookup"><span data-stu-id="c9044-237">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-238">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-238">Example</span></span>

```c
/* Open NAND flash instance "my_nand_flash" with the driver "my_nand_driver_initialize". */ 
status = lx_nand_flash_open(&my_nand_flash,"my nand flash",  
    my_nand_driver_initialize);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-239">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-239">See Also</span></span>

- <span data-ttu-id="c9044-240">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-240">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-241">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-241">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-242">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-242">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-243">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-243">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-244">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-244">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-245">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-245">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-246">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-246">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-247">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-247">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-248">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-248">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-249">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-249">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_page_ecc_check"></a><span data-ttu-id="c9044-250">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-250">lx_nand_flash_page_ecc_check</span></span>

<span data-ttu-id="c9044-251">Pagina di controllo degli errori ECC con correzione</span><span class="sxs-lookup"><span data-stu-id="c9044-251">Check page for ECC errors with correction</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-252">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-252">Prototype</span></span>

```c
UINT lx_nand_flash_page_ecc_check(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a><span data-ttu-id="c9044-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-253">Description</span></span>

<span data-ttu-id="c9044-254">Questo servizio verifica l'integrità del buffer di pagine NAND fornito con l'ECC fornito.</span><span class="sxs-lookup"><span data-stu-id="c9044-254">This service verifies the integrity of the supplied NAND page buffer with the supplied ECC.</span></span> <span data-ttu-id="c9044-255">Si presuppone che le dimensioni della pagina (definite nel puntatore dell'istanza Flash NAND) siano un multiplo di 256 byte e che il codice ECC fornito sia in grado di correggere un errore a 1 bit in ogni porzione di 256 byte della pagina.</span><span class="sxs-lookup"><span data-stu-id="c9044-255">Page size (defined in the NAND flash instance pointer) is assumed to be a multiple of 256-bytes and the ECC code supplied is capable of correcting a 1 bit error in each 256-byte portion of the page.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-256">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-256">Input Parameters</span></span>

- <span data-ttu-id="c9044-257">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-257">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="c9044-258">**page_buffer**: puntatore al buffer della pagina Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-258">**page_buffer**: Pointer to NAND flash page buffer.</span></span>
- <span data-ttu-id="c9044-259">**ecc_buffer**: puntatore ad ecc per la pagina Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-259">**ecc_buffer**: Pointer to ECC for NAND flash page.</span></span> <span data-ttu-id="c9044-260">Si noti che ci sono 3 byte ECC per parte della pagina a 256 byte.</span><span class="sxs-lookup"><span data-stu-id="c9044-260">Note that there are 3 ECC bytes per 256-byte portion of the page.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-261">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-261">Return Values</span></span>

- <span data-ttu-id="c9044-262">**LX_SUCCESS**: (0x00) la pagina NAND non contiene errori.</span><span class="sxs-lookup"><span data-stu-id="c9044-262">**LX_SUCCESS**: (0x00) NAND page has no errors.</span></span>
- <span data-ttu-id="c9044-263">**LX_NAND_ERROR_CORRECTED**: (0x06) uno o più errori a 1 bit sono stati corretti nella pagina NAND: le correzioni si trovano nel buffer di pagina.</span><span class="sxs-lookup"><span data-stu-id="c9044-263">**LX_NAND_ERROR_CORRECTED**: (0x06) One or more 1-bit errors were corrected in the NAND page—correction(s) are in the page buffer.</span></span>
- <span data-ttu-id="c9044-264">**LX_NAND_ERROR_NOT_CORRECTED**: (0x07) troppi errori da correggere nella pagina NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-264">**LX_NAND_ERROR_NOT_CORRECTED**: (0x07) Too many errors to correct on the NAND page.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-265">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-265">Allowed From</span></span>

<span data-ttu-id="c9044-266">Driver LevelX</span><span class="sxs-lookup"><span data-stu-id="c9044-266">LevelX Driver</span></span>

### <a name="example"></a><span data-ttu-id="c9044-267">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-267">Example</span></span>

```c
/* Check the NAND page pointed to by "page_pointer" of the NAND flash instance "my_nand_flash" . */
status = lx_nand_flash_page_ecc_check(&my_nand_flash, page_pointer, ecc_pointer);  
  
/* If status is LX_SUCCESS the page is valid. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-268">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-268">See Also</span></span>

- <span data-ttu-id="c9044-269">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-269">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-270">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-270">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-271">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-271">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-272">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-272">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-273">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-273">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-274">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-274">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-275">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-275">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-276">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-276">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-277">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-277">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-278">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-278">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_page_ecc_compute"></a><span data-ttu-id="c9044-279">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-279">lx_nand_flash_page_ecc_compute</span></span>

<span data-ttu-id="c9044-280">Calcolo ECC per la pagina</span><span class="sxs-lookup"><span data-stu-id="c9044-280">Compute ECC for page</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-281">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-281">Prototype</span></span>

```c
UINT lx_nand_flash_page_ecc_compute(
    LX_NAND_FLASH *nand_flash,  
    UCHAR *page_buffer, 
    UCHAR *ecc_buffer);
```

### <a name="description"></a><span data-ttu-id="c9044-282">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-282">Description</span></span>

<span data-ttu-id="c9044-283">Questo servizio calcola l'ECC del buffer di pagine NAND fornito e restituisce il ECC nel buffer di ECC fornito.</span><span class="sxs-lookup"><span data-stu-id="c9044-283">This service computes the ECC of the supplied NAND page buffer and returns the ECC in the supplied ECC buffer.</span></span> <span data-ttu-id="c9044-284">Si presuppone che le dimensioni della pagina siano un multiplo di 256 byte (definito nel puntatore dell'istanza Flash NAND).</span><span class="sxs-lookup"><span data-stu-id="c9044-284">Page size is assume to be a multiple of 256-bytes (defined in the NAND flash instance pointer).</span></span> <span data-ttu-id="c9044-285">Il codice ECC viene usato per verificare l'integrità della pagina quando viene letta in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c9044-285">The ECC code is used to verify the integrity of the page when it is read at a later time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-286">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-286">Input Parameters</span></span>

- <span data-ttu-id="c9044-287">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-287">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="c9044-288">**page_buffer**: puntatore al buffer della pagina Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-288">**page_buffer**: Pointer to NAND flash page buffer.</span></span>
- <span data-ttu-id="c9044-289">**ecc_buffer**: puntatore alla destinazione per ecc della pagina Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-289">**ecc_buffer**: Pointer to destination for ECC of the NAND flash page.</span></span> <span data-ttu-id="c9044-290">Si noti che deve essere di 3 byte di spazio di archiviazione ECC per parte della pagina a 256 byte.</span><span class="sxs-lookup"><span data-stu-id="c9044-290">Note that must be 3 bytes of ECC storage per 256-byte portion of the page.</span></span> <span data-ttu-id="c9044-291">Ad esempio, una pagina di 2048 byte richiede 24 byte per l'ECC.</span><span class="sxs-lookup"><span data-stu-id="c9044-291">For example, a 2048 byte page would require 24 bytes for the ECC.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-292">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-292">Return Values</span></span>

- <span data-ttu-id="c9044-293">**LX_SUCCESS**: (0x00) ecc calcolato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c9044-293">**LX_SUCCESS**: (0x00) ECC successfully calculated.</span></span>
- <span data-ttu-id="c9044-294">**LX_ERROR**: (0x01) errore durante il calcolo ecc.</span><span class="sxs-lookup"><span data-stu-id="c9044-294">**LX_ERROR**: (0x01) Error calculating ECC.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-295">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-295">Allowed From</span></span>

<span data-ttu-id="c9044-296">Driver LevelX</span><span class="sxs-lookup"><span data-stu-id="c9044-296">LevelX Driver</span></span>

### <a name="example"></a><span data-ttu-id="c9044-297">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-297">Example</span></span>

```c
/* Compute ECC for the NAND page pointed to by "page_pointer" of the NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_page_ecc_compute(&my_nand_flash, page_pointer, ecc_pointer);  
  
/* If status is LX_SUCCESS the ECC was calculated and Can be found in the memory pointed to by "ecc_pointer." */
```

### <a name="see-also"></a><span data-ttu-id="c9044-298">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-298">See Also</span></span>

- <span data-ttu-id="c9044-299">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-299">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-300">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-300">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-301">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-301">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-302">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-302">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-303">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-303">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-304">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-304">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-305">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-305">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-306">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-306">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-307">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-307">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-308">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-308">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_partial_defragment"></a><span data-ttu-id="c9044-309">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-309">lx_nand_flash_partial_defragment</span></span>

<span data-ttu-id="c9044-310">Deframmentazione parziale dell'istanza di Flash NAND</span><span class="sxs-lookup"><span data-stu-id="c9044-310">Partial defragment of NAND flash instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-311">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-311">Prototype</span></span>

```c
UINT lx_nand_flash_partial_defragment(
    LX_NAND_FLASH *nand_flash,  
    UINT max_blocks);
```

### <a name="description"></a><span data-ttu-id="c9044-312">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-312">Description</span></span>

<span data-ttu-id="c9044-313">Questo servizio Deframmenta l'istanza Flash NAND precedentemente aperta fino al numero massimo di blocchi specificato.</span><span class="sxs-lookup"><span data-stu-id="c9044-313">This service defragments the previously opened NAND flash instance up to the maximum number of blocks specified.</span></span> <span data-ttu-id="c9044-314">Il processo di deframmentazione ottimizza il numero di pagine e blocchi liberi.</span><span class="sxs-lookup"><span data-stu-id="c9044-314">The defragment process maximizes the number of free pages and blocks.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-315">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-315">Input Parameters</span></span>

- <span data-ttu-id="c9044-316">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-316">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="c9044-317">**max_blocks**: numero massimo di blocchi.</span><span class="sxs-lookup"><span data-stu-id="c9044-317">**max_blocks**: Maximum number of blocks.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-318">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-318">Return Values</span></span>

- <span data-ttu-id="c9044-319">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-319">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-320">**LX_ERROR**: (0x01) errore durante la deframmentazione dell'istanza Flash.</span><span class="sxs-lookup"><span data-stu-id="c9044-320">**LX_ERROR**: (0x01) Error defragmenting flash instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-321">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-321">Allowed From</span></span>

<span data-ttu-id="c9044-322">Thread</span><span class="sxs-lookup"><span data-stu-id="c9044-322">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-323">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-323">Example</span></span>

```c
/* Defragment 1 block of NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_partial_defragment(&my_nand_flash, 1);  
  
/* If status is LX_SUCCESS the request was successful. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-324">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-324">See Also</span></span>

- <span data-ttu-id="c9044-325">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-325">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-326">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-326">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-327">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-327">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-328">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-328">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-329">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-329">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-330">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-330">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-331">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-331">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-332">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-332">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-333">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-333">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-334">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-334">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_sector_read"></a><span data-ttu-id="c9044-335">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-335">lx_nand_flash_sector_read</span></span>

<span data-ttu-id="c9044-336">Leggi il settore NAND Flash</span><span class="sxs-lookup"><span data-stu-id="c9044-336">Read NAND flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-337">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-337">Prototype</span></span>

```c
UINT lx_nand_flash_sector_read(
    LX_NAND_FLASH *nand_flash,  
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a><span data-ttu-id="c9044-338">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-338">Description</span></span>

<span data-ttu-id="c9044-339">Questo servizio legge il settore logico dall'istanza Flash NAND e, in caso di esito positivo, restituisce il contenuto del buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="c9044-339">This service reads the logical sector from the NAND flash instance and if successful returns the contents in the supplied buffer.</span></span> <span data-ttu-id="c9044-340">Si noti che le dimensioni del settore NAND sono sempre le dimensioni di pagina dell'hardware NAND sottostante.</span><span class="sxs-lookup"><span data-stu-id="c9044-340">Note that NAND sector size is always the page size of the underlying NAND hardware.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-341">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-341">Input Parameters</span></span>

- <span data-ttu-id="c9044-342">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-342">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="c9044-343">**logical_sector**: settore logico da leggere.</span><span class="sxs-lookup"><span data-stu-id="c9044-343">**logical_sector**: Logical sector to read.</span></span>
- <span data-ttu-id="c9044-344">**buffer**: puntatore alla destinazione per il contenuto del settore logico.</span><span class="sxs-lookup"><span data-stu-id="c9044-344">**buffer**: Pointer to destination for contents of the logical sector.</span></span> <span data-ttu-id="c9044-345">Si presuppone che il buffer corrisponda alle dimensioni della pagina Flash NAND e allineato per l'accesso ULONG.</span><span class="sxs-lookup"><span data-stu-id="c9044-345">Note that the buffer is assumed to be the size of the NAND flash page size and aligned for ULONG access.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-346">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-346">Return Values</span></span>

- <span data-ttu-id="c9044-347">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-347">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-348">**LX_ERROR**: (0x01) errore durante la lettura del settore NAND Flash.</span><span class="sxs-lookup"><span data-stu-id="c9044-348">**LX_ERROR**: (0x01) Error reading NAND flash sector.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-349">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-349">Allowed From</span></span>

<span data-ttu-id="c9044-350">Thread</span><span class="sxs-lookup"><span data-stu-id="c9044-350">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-351">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-351">Example</span></span>

```c
/* Read logical sector 20 of the NAND flash instance "my_nand_flash" and place contents in "buffer". */
status = lx_nand_flash_sector_read(&my_nand_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, "buffer" contains the contentsnof logical sector 20. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-352">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-352">See Also</span></span>

- <span data-ttu-id="c9044-353">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-353">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-354">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-354">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-355">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-355">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-356">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-356">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-357">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-357">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-358">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-358">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-359">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-359">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-360">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-360">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-361">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-361">lx_nand_flash_sector_release</span></span>
- <span data-ttu-id="c9044-362">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-362">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_sector_release"></a><span data-ttu-id="c9044-363">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-363">lx_nand_flash_sector_release</span></span>

<span data-ttu-id="c9044-364">Settore Flash NAND versione</span><span class="sxs-lookup"><span data-stu-id="c9044-364">Release NAND flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-365">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-365">Prototype</span></span>

```c
UINT lx_nand_flash_sector_release(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector);
```

### <a name="description"></a><span data-ttu-id="c9044-366">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-366">Description</span></span>

<span data-ttu-id="c9044-367">Questo servizio rilascia il mapping del settore logico nell'istanza del flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-367">This service releases the logical sector mapping in the NAND flash instance.</span></span> <span data-ttu-id="c9044-368">Il rilascio di un settore logico quando non viene usato rende più efficiente il livellamento del LevelX.</span><span class="sxs-lookup"><span data-stu-id="c9044-368">Releasing a logical sector when not used makes the LevelX wear leveling more efficient.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-369">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-369">Input Parameters</span></span>

- <span data-ttu-id="c9044-370">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-370">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="c9044-371">**logical_sector**: settore logico da rilasciare.</span><span class="sxs-lookup"><span data-stu-id="c9044-371">**logical_sector**: Logical sector to release.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-372">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-372">Return Values</span></span>

- <span data-ttu-id="c9044-373">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-373">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-374">**LX_ERROR**: (0x01) errore durante la scrittura del settore Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-374">**LX_ERROR**: (0x01) Error NAND flash sector write.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-375">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-375">Allowed From</span></span>

<span data-ttu-id="c9044-376">Thread</span><span class="sxs-lookup"><span data-stu-id="c9044-376">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-377">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-377">Example</span></span>

```c
/* Release logical sector 20 of the NAND flash instance "my_nand_flash". */  
status = lx_nand_flash_sector_release(&my_nand_flash, 20);  
  
/* If status is LX_SUCCESS, logical sector 20 has been released. */
```

### <a name="see-also"></a><span data-ttu-id="c9044-378">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-378">See Also</span></span>

- <span data-ttu-id="c9044-379">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-379">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-380">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-380">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-381">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-381">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-382">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-382">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-383">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-383">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-384">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-384">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-385">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-385">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-386">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-386">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-387">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-387">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-388">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-388">lx_nand_flash_sector_write</span></span>

## <a name="lx_nand_flash_sector_write"></a><span data-ttu-id="c9044-389">lx_nand_flash_sector_write</span><span class="sxs-lookup"><span data-stu-id="c9044-389">lx_nand_flash_sector_write</span></span>

<span data-ttu-id="c9044-390">Scrivi settore Flash NAND</span><span class="sxs-lookup"><span data-stu-id="c9044-390">Write NAND flash sector</span></span>

### <a name="prototype"></a><span data-ttu-id="c9044-391">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c9044-391">Prototype</span></span>

```c
UINT lx_nand_flash_sector_write(
    LX_NAND_FLASH *nand_flash,
    ULONG logical_sector, 
    VOID *buffer);
```

### <a name="description"></a><span data-ttu-id="c9044-392">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9044-392">Description</span></span>

<span data-ttu-id="c9044-393">Questo servizio scrive il settore logico specificato nell'istanza di Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-393">This service writes the specified logical sector in the NAND flash instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c9044-394">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c9044-394">Input Parameters</span></span>

- <span data-ttu-id="c9044-395">**nand_flash**: puntatore all'istanza Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-395">**nand_flash**: NAND flash instance pointer.</span></span>
- <span data-ttu-id="c9044-396">**logical_sector**: settore logico da scrivere.</span><span class="sxs-lookup"><span data-stu-id="c9044-396">**logical_sector**: Logical sector to write.</span></span>
- <span data-ttu-id="c9044-397">**buffer**: puntatore al contenuto del settore logico.</span><span class="sxs-lookup"><span data-stu-id="c9044-397">**buffer**: Pointer to the contents of the logical sector.</span></span> <span data-ttu-id="c9044-398">Si presuppone che il buffer corrisponda alle dimensioni della pagina Flash NAND e allineato per l'accesso ULONG.</span><span class="sxs-lookup"><span data-stu-id="c9044-398">Note that the buffer is assumed to be the size of the NAND flash page size and aligned for ULONG access.</span></span>

### <a name="return-values"></a><span data-ttu-id="c9044-399">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c9044-399">Return Values</span></span>

- <span data-ttu-id="c9044-400">**LX_SUCCESS**: (0x00) la richiesta è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c9044-400">**LX_SUCCESS**: (0x00) Successful request.</span></span>
- <span data-ttu-id="c9044-401">**LX_NO_SECTORS**: (0x02) non sono più disponibili settori gratuiti per eseguire la scrittura.</span><span class="sxs-lookup"><span data-stu-id="c9044-401">**LX_NO_SECTORS**: (0x02) No more free sectors are available to perform the write.</span></span>
- <span data-ttu-id="c9044-402">**LX_ERROR**: (0x01) errore durante il rilascio del settore Flash NAND.</span><span class="sxs-lookup"><span data-stu-id="c9044-402">**LX_ERROR**: (0x01) Error releasing NAND flash sector.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c9044-403">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c9044-403">Allowed From</span></span>

<span data-ttu-id="c9044-404">Thread</span><span class="sxs-lookup"><span data-stu-id="c9044-404">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c9044-405">Esempio</span><span class="sxs-lookup"><span data-stu-id="c9044-405">Example</span></span>

```c
/* Write logical sector 20 of the NAND flash instance "my_nand_flash" with the contents pointed to by "buffer". */  
status = lx_nand_flash_sector_write(&my_nand_flash, 20, buffer);  
  
/* If status is LX_SUCCESS, logical sector 20 has been written with the contents of "buffer". */
```

### <a name="see-also"></a><span data-ttu-id="c9044-406">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c9044-406">See Also</span></span>

- <span data-ttu-id="c9044-407">lx_nand_flash_close</span><span class="sxs-lookup"><span data-stu-id="c9044-407">lx_nand_flash_close</span></span>
- <span data-ttu-id="c9044-408">lx_nand_flash_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-408">lx_nand_flash_defragment</span></span>
- <span data-ttu-id="c9044-409">lx_nand_flash_extended_cache_enable</span><span class="sxs-lookup"><span data-stu-id="c9044-409">lx_nand_flash_extended_cache_enable</span></span>
- <span data-ttu-id="c9044-410">lx_nand_flash_initialize</span><span class="sxs-lookup"><span data-stu-id="c9044-410">lx_nand_flash_initialize</span></span>
- <span data-ttu-id="c9044-411">lx_nand_flash_open</span><span class="sxs-lookup"><span data-stu-id="c9044-411">lx_nand_flash_open</span></span>
- <span data-ttu-id="c9044-412">lx_nand_flash_page_ecc_check</span><span class="sxs-lookup"><span data-stu-id="c9044-412">lx_nand_flash_page_ecc_check</span></span>
- <span data-ttu-id="c9044-413">lx_nand_flash_page_ecc_compute</span><span class="sxs-lookup"><span data-stu-id="c9044-413">lx_nand_flash_page_ecc_compute</span></span>
- <span data-ttu-id="c9044-414">lx_nand_flash_partial_defragment</span><span class="sxs-lookup"><span data-stu-id="c9044-414">lx_nand_flash_partial_defragment</span></span>
- <span data-ttu-id="c9044-415">lx_nand_flash_sector_read</span><span class="sxs-lookup"><span data-stu-id="c9044-415">lx_nand_flash_sector_read</span></span>
- <span data-ttu-id="c9044-416">lx_nand_flash_sector_release</span><span class="sxs-lookup"><span data-stu-id="c9044-416">lx_nand_flash_sector_release</span></span>
