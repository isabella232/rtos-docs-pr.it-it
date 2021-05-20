---
title: Capitolo 2 - Installazione e uso di Azure RTOS LevelX
description: L'installazione e l'uso di LevelX sono semplici e descritti nelle sezioni seguenti di questo capitolo.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 34110e74e8ad0a6acd376c00c1284a3ea715c5f5
ms.sourcegitcommit: 4ebe7c51ba850951c6a9d0f15e22d07bb752bc28
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2021
ms.locfileid: "110223316"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-levelx"></a><span data-ttu-id="8f7b8-103">Capitolo 2 - Installazione e uso di Azure RTOS LevelX</span><span class="sxs-lookup"><span data-stu-id="8f7b8-103">Chapter 2 - Installation and use of Azure RTOS LevelX</span></span>

<span data-ttu-id="8f7b8-104">L'installazione e l Azure RTOS di LevelX sono semplici e descritte nelle sezioni seguenti di questo capitolo.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-104">Installation and use of Azure RTOS LevelX is straightforward and described in the following sections of this chapter.</span></span>

## <a name="distribution"></a><span data-ttu-id="8f7b8-105">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="8f7b8-105">Distribution</span></span>

<span data-ttu-id="8f7b8-106">LevelX viene distribuito in ANSI C in cui ogni funzione è contenuta in un file C separato.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-106">LevelX is distributed in ANSI C where each function is contained in its own separate C file.</span></span> <span data-ttu-id="8f7b8-107">I file nella distribuzione LevelX sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-107">The files in the LevelX distribution are as follows.</span></span>
- <span data-ttu-id="8f7b8-108">lx_api.h</span><span class="sxs-lookup"><span data-stu-id="8f7b8-108">lx_api.h</span></span>
- <span data-ttu-id="8f7b8-109">lx_nand_flash_256byte_ecc_check.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-109">lx_nand_flash_256byte_ecc_check.c</span></span>
- <span data-ttu-id="8f7b8-110">lx_nand_flash_256byte_ecc_compute.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-110">lx_nand_flash_256byte_ecc_compute.c</span></span>
- <span data-ttu-id="8f7b8-111">lx_nand_flash_block_full_update.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-111">lx_nand_flash_block_full_update.c</span></span>
- <span data-ttu-id="8f7b8-112">lx_nand_flash_block_reclaim.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-112">lx_nand_flash_block_reclaim.c</span></span>
- <span data-ttu-id="8f7b8-113">lx_nand_flash_close.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-113">lx_nand_flash_close.c</span></span>
- <span data-ttu-id="8f7b8-114">lx_nand_flash_defragment.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-114">lx_nand_flash_defragment.c</span></span>  
- <span data-ttu-id="8f7b8-115">lx_nand_flash_extended_cache_enable.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-115">lx_nand_flash_extended_cache_enable.c</span></span>
- <span data-ttu-id="8f7b8-116">lx_nand_flash_initialize.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-116">lx_nand_flash_initialize.c</span></span>
- <span data-ttu-id="8f7b8-117">lx_nand_flash_logical_sector_find.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-117">lx_nand_flash_logical_sector_find.c</span></span>
- <span data-ttu-id="8f7b8-118">lx_nand_flash_next_block_to_erase_find.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-118">lx_nand_flash_next_block_to_erase_find.c</span></span>
- <span data-ttu-id="8f7b8-119">lx_nand_flash_open.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-119">lx_nand_flash_open.c</span></span>
- <span data-ttu-id="8f7b8-120">lx_nand_flash_page_ecc_check.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-120">lx_nand_flash_page_ecc_check.c</span></span>
- <span data-ttu-id="8f7b8-121">lx_nand_flash_page_ecc_compute.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-121">lx_nand_flash_page_ecc_compute.c</span></span>  
- <span data-ttu-id="8f7b8-122">lx_nand_flash_partial_defragment.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-122">lx_nand_flash_partial_defragment.c</span></span>
- <span data-ttu-id="8f7b8-123">lx_nand_flash_physical_page_allocate.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-123">lx_nand_flash_physical_page_allocate.c</span></span>
- <span data-ttu-id="8f7b8-124">lx_nand_flash_sector_mapping_cache_invalidate.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-124">lx_nand_flash_sector_mapping_cache_invalidate.c</span></span>
- <span data-ttu-id="8f7b8-125">lx_nand_flash_sector_read.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-125">lx_nand_flash_sector_read.c</span></span>
- <span data-ttu-id="8f7b8-126">lx_nand_flash_sector_release.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-126">lx_nand_flash_sector_release.c</span></span>
- <span data-ttu-id="8f7b8-127">lx_nand_flash_sector_write.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-127">lx_nand_flash_sector_write.c</span></span>
- <span data-ttu-id="8f7b8-128">lx_nand_flash_system_error.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-128">lx_nand_flash_system_error.c</span></span>
- <span data-ttu-id="8f7b8-129">lx_nor_flash_block_reclaim.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-129">lx_nor_flash_block_reclaim.c</span></span>
- <span data-ttu-id="8f7b8-130">lx_nor_flash_close.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-130">lx_nor_flash_close.c</span></span>
- <span data-ttu-id="8f7b8-131">lx_nor_flash_defragment.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-131">lx_nor_flash_defragment.c</span></span>  
- <span data-ttu-id="8f7b8-132">lx_nor_flash_extended_cache_enable.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-132">lx_nor_flash_extended_cache_enable.c</span></span>
- <span data-ttu-id="8f7b8-133">lx_nor_flash_initialize.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-133">lx_nor_flash_initialize.c</span></span>
- <span data-ttu-id="8f7b8-134">lx_nor_flash_logical_sector_find.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-134">lx_nor_flash_logical_sector_find.c</span></span>
- <span data-ttu-id="8f7b8-135">lx_nor_flash_next_block_to_erase_find.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-135">lx_nor_flash_next_block_to_erase_find.c</span></span>
- <span data-ttu-id="8f7b8-136">lx_nor_flash_open.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-136">lx_nor_flash_open.c</span></span>
- <span data-ttu-id="8f7b8-137">lx_nor_flash_partial_defragment.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-137">lx_nor_flash_partial_defragment.c</span></span>
- <span data-ttu-id="8f7b8-138">lx_nor_flash_physical_sector_allocate.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-138">lx_nor_flash_physical_sector_allocate.c</span></span>
- <span data-ttu-id="8f7b8-139">lx_nor_flash_sector_mapping_cache_invalidate.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-139">lx_nor_flash_sector_mapping_cache_invalidate.c</span></span>
- <span data-ttu-id="8f7b8-140">lx_nor_flash_sector_read.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-140">lx_nor_flash_sector_read.c</span></span>
- <span data-ttu-id="8f7b8-141">lx_nor_flash_sector_release.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-141">lx_nor_flash_sector_release.c</span></span>
- <span data-ttu-id="8f7b8-142">lx_nor_flash_sector_write.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-142">lx_nor_flash_sector_write.c</span></span>
- <span data-ttu-id="8f7b8-143">lx_nor_flash_system_error.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-143">lx_nor_flash_system_error.c</span></span>

<span data-ttu-id="8f7b8-144">Sono disponibili anche esempi di simulatori e driver FileX per le istanze NAD levelx e NOR, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-144">There are also simulator and FileX driver samples for both LevelX NAND and NOR instances, as follows.</span></span>

- <span data-ttu-id="8f7b8-145">demo_filex_nand_flash.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-145">demo_filex_nand_flash.c</span></span>  
- <span data-ttu-id="8f7b8-146">fx_nand_flash_simulated_driver.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-146">fx_nand_flash_simulated_driver.c</span></span>
- <span data-ttu-id="8f7b8-147">lx_nand_flash_simulator.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-147">lx_nand_flash_simulator.c</span></span>
- <span data-ttu-id="8f7b8-148">demo_filex_nor_flash.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-148">demo_filex_nor_flash.c</span></span>  
- <span data-ttu-id="8f7b8-149">fx_nor_flash_simulated_driver.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-149">fx_nor_flash_simulated_driver.c</span></span>
- <span data-ttu-id="8f7b8-150">lx_nor_flash_simulator.c</span><span class="sxs-lookup"><span data-stu-id="8f7b8-150">lx_nor_flash_simulator.c</span></span>

<span data-ttu-id="8f7b8-151">Naturalmente, se è necessaria solo la memoria flash NAD, sono necessari solo i file flash NAD LevelX (***lx_nand_ \* .c***).</span><span class="sxs-lookup"><span data-stu-id="8f7b8-151">Of course, if only NAND flash is required, only the LevelX NAND flash files (***lx_nand_\*.c***) are needed.</span></span> <span data-ttu-id="8f7b8-152">Analogamente, se è necessaria solo la memoria flash NOR, sono necessari solo i file flash NOR (\*\*_lx_nor_ \_ .c\*\*\*).</span><span class="sxs-lookup"><span data-stu-id="8f7b8-152">Similarly, if only NOR flash is required, only the NOR flash files (\*\*_lx_nor_\_.c\*\*\*) are needed.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="8f7b8-153">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="8f7b8-153">Configuration Options</span></span>

<span data-ttu-id="8f7b8-154">LevelX può essere configurato in fase di compilazione tramite le definizione condizionali descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-154">LevelX can be configured at compile time via the conditional defines described below.</span></span> <span data-ttu-id="8f7b8-155">È sufficiente aggiungere la definizione desiderata alla compilazione di ogni origine LevelX per usare l'opzione .</span><span class="sxs-lookup"><span data-stu-id="8f7b8-155">Simply add the desired define to the compilation of each LevelX source to use the option.</span></span>

- <span data-ttu-id="8f7b8-156">**LX_DIRECT_READ:** definita, questa opzione ignora la routine di lettura del driver flash NOR a favore o legge direttamente la memoria NOR, con un conseguente aumento significativo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-156">**LX_DIRECT_READ**:  Defined, this option bypasses the NOR flash driver read routine in favor or reading the NOR memory directly, resulting in a significant performance increase.</span></span>
- <span data-ttu-id="8f7b8-157">**LX_FREE_SECTOR_DATA_VERIFY:** definito, in questo modo la logica aperta dell'istanza di LevelX NOR verifica che i settori NOR liberi siano tutti quelli.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-157">**LX_FREE_SECTOR_DATA_VERIFY**: Defined, this causes the LevelX NOR instance open logic to verify free NOR sectors are all ones.</span></span>
- <span data-ttu-id="8f7b8-158">**LX_NAND_SECTOR_MAPPING_CACHE_SIZE:** per impostazione predefinita questo valore è 16 e definisce le dimensioni della cache per il mapping dei settori logici.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-158">**LX_NAND_SECTOR_MAPPING_CACHE_SIZE**:  By default this value is 16 and defines the logical sector mapping cache size.</span></span> <span data-ttu-id="8f7b8-159">Valori di grandi dimensioni migliorano le prestazioni, ma costi di memoria.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-159">Large values improve performance, but cost memory.</span></span> <span data-ttu-id="8f7b8-160">La dimensione minima è 8 e tutti i valori devono essere una potenza di 2.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-160">The minimum size is 8 and all values must be a power of 2.</span></span>
- <span data-ttu-id="8f7b8-161">**LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: definito, viene creata una cache di mapping diretto, in modo che non siano presenti mancati riscontri nella cache.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-161">**LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: Defined, this creates a direct mapping cache, such that there are no cache misses.</span></span> <span data-ttu-id="8f7b8-162">Richiede anche che LX_NAND_SECTOR_MAPPING_CACHE_SIZE rappresenta il numero esatto di pagine totali nel dispositivo flash.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-162">It also requires that LX_NAND_SECTOR_MAPPING_CACHE_SIZE represents the exact number of total pages in your flash device.</span></span>
- <span data-ttu-id="8f7b8-163">**LX_NOR_DISABLE_EXTENDED_CACHE**: definito, la cache NOR estesa è stata disabilitata.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-163">**LX_NOR_DISABLE_EXTENDED_CACHE**: Defined, this disabled the extended NOR cache.</span></span>
- <span data-ttu-id="8f7b8-164">**LX_NOR_EXTENDED_CACHE_SIZE:** per impostazione predefinita questo valore è 8, che rappresenta un massimo di 8 settori che possono essere memorizzati nella cache in un'istanza di NOR.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-164">**LX_NOR_EXTENDED_CACHE_SIZE**: By default this value is 8, which represents a maximum of 8 sectors that can be cached in a NOR instance.</span></span>
- <span data-ttu-id="8f7b8-165">**LX_NOR_SECTOR_MAPPING_CACHE_SIZE:** per impostazione predefinita, questo valore è 16 e definisce le dimensioni della cache per il mapping dei settori logici.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-165">**LX_NOR_SECTOR_MAPPING_CACHE_SIZE**: By default this value is 16 and defines the logical sector mapping cache size.</span></span> <span data-ttu-id="8f7b8-166">Valori di grandi dimensioni migliorano le prestazioni, ma costi di memoria.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-166">Large values improve performance, but cost memory.</span></span> <span data-ttu-id="8f7b8-167">La dimensione minima è 8 e tutti i valori devono essere una potenza di 2.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-167">The minimum size is 8 and all values must be a power of 2.</span></span>
- <span data-ttu-id="8f7b8-168">**LX_THREAD_SAFE_ENABLE:** definito, questo rende LevelX thread-safe usando un oggetto mutex ThreadX in tutta l'API.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-168">**LX_THREAD_SAFE_ENABLE**: Defined, this makes LevelX thread-safe by using a ThreadX mutex object throughout the API.</span></span>
- <span data-ttu-id="8f7b8-169">**LX_STANDALONE_ENABLE**: definito, consente l'uso di LevelX in modalità autonoma (senza Azure RTOS).</span><span class="sxs-lookup"><span data-stu-id="8f7b8-169">**LX_STANDALONE_ENABLE**: Defined, enables LevelX to be used in standalone mode (without Azure RTOS).</span></span> <span data-ttu-id="8f7b8-170">Per impostazione predefinita, questo simbolo non è definito.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-170">By default this symbol is not defined.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f7b8-171">Quando si usa LevelX in modalità autonoma **(LX_STANDALONE_ENABLE** deve essere definito), i file/librerie ThreadX non sono necessari.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-171">When using LevelX in Standalone mode (**LX_STANDALONE_ENABLE** must be defined), ThreadX files/libraries are not required.</span></span> <span data-ttu-id="8f7b8-172">La funzionalità thread-safe LevelX è disabilitata in questa modalità.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-172">LevelX thread-safe feature is disabled in this mode.</span></span>

## <a name="using-levelx"></a><span data-ttu-id="8f7b8-173">Uso di LevelX</span><span class="sxs-lookup"><span data-stu-id="8f7b8-173">Using LevelX</span></span>

<span data-ttu-id="8f7b8-174">Per usare LevelX, da solo o con FileX, includere il file \***lx_api.h** _ nel codice che fa riferimento all'API LevelX.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-174">To use LevelX, either by itself or with FileX, include the file \***lx_api.h** _ in the code that references the LevelX API.</span></span> <span data-ttu-id="8f7b8-175">Assicurarsi anche che il codice dell'oggetto LevelX sia disponibile in fase di collegamento.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-175">Also ensure that the LevelX object code is available at link time.</span></span> <span data-ttu-id="8f7b8-176">Esaminare i file _*_demo_filex_nand_flash.c_*_ e _ *_demo_filex_nor_flash.c_*\* per esempi su come usare LevelX.</span><span class="sxs-lookup"><span data-stu-id="8f7b8-176">Please examine the files _*_demo_filex_nand_flash.c_*_ and _ *_demo_filex_nor_flash.c_*\* for examples of how to use LevelX.</span></span>
