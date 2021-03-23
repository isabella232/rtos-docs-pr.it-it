---
title: Capitolo 2-installazione e uso di Azure RTO LevelX
description: L'installazione e l'uso di LevelX sono semplici e descritti nelle sezioni seguenti di questo capitolo.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 575776875452cfc718401556a6440d787cb18893
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822970"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-levelx"></a><span data-ttu-id="d7469-103">Capitolo 2-installazione e uso di Azure RTO LevelX</span><span class="sxs-lookup"><span data-stu-id="d7469-103">Chapter 2 - Installation and use of Azure RTOS LevelX</span></span>

<span data-ttu-id="d7469-104">L'installazione e l'uso di Azure RTO LevelX sono semplici e descritti nelle sezioni seguenti di questo capitolo.</span><span class="sxs-lookup"><span data-stu-id="d7469-104">Installation and use of Azure RTOS LevelX is straightforward and described in the following sections of this chapter.</span></span>

## <a name="distribution"></a><span data-ttu-id="d7469-105">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="d7469-105">Distribution</span></span>

<span data-ttu-id="d7469-106">LevelX viene distribuito in ANSI C, dove ogni funzione è contenuta nel proprio file C separato.</span><span class="sxs-lookup"><span data-stu-id="d7469-106">LevelX is distributed in ANSI C where each function is contained in its own separate C file.</span></span> <span data-ttu-id="d7469-107">I file nella distribuzione LevelX sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="d7469-107">The files in the LevelX distribution are as follows.</span></span>
- <span data-ttu-id="d7469-108">lx_api. h</span><span class="sxs-lookup"><span data-stu-id="d7469-108">lx_api.h</span></span>
- <span data-ttu-id="d7469-109">lx_nand_flash_256byte_ecc_check. c</span><span class="sxs-lookup"><span data-stu-id="d7469-109">lx_nand_flash_256byte_ecc_check.c</span></span>
- <span data-ttu-id="d7469-110">lx_nand_flash_256byte_ecc_compute. c</span><span class="sxs-lookup"><span data-stu-id="d7469-110">lx_nand_flash_256byte_ecc_compute.c</span></span>
- <span data-ttu-id="d7469-111">lx_nand_flash_block_full_update. c</span><span class="sxs-lookup"><span data-stu-id="d7469-111">lx_nand_flash_block_full_update.c</span></span>
- <span data-ttu-id="d7469-112">lx_nand_flash_block_reclaim. c</span><span class="sxs-lookup"><span data-stu-id="d7469-112">lx_nand_flash_block_reclaim.c</span></span>
- <span data-ttu-id="d7469-113">lx_nand_flash_close. c</span><span class="sxs-lookup"><span data-stu-id="d7469-113">lx_nand_flash_close.c</span></span>
- <span data-ttu-id="d7469-114">lx_nand_flash_defragment. c</span><span class="sxs-lookup"><span data-stu-id="d7469-114">lx_nand_flash_defragment.c</span></span>  
- <span data-ttu-id="d7469-115">lx_nand_flash_extended_cache_enable. c</span><span class="sxs-lookup"><span data-stu-id="d7469-115">lx_nand_flash_extended_cache_enable.c</span></span>
- <span data-ttu-id="d7469-116">lx_nand_flash_initialize. c</span><span class="sxs-lookup"><span data-stu-id="d7469-116">lx_nand_flash_initialize.c</span></span>
- <span data-ttu-id="d7469-117">lx_nand_flash_logical_sector_find. c</span><span class="sxs-lookup"><span data-stu-id="d7469-117">lx_nand_flash_logical_sector_find.c</span></span>
- <span data-ttu-id="d7469-118">lx_nand_flash_next_block_to_erase_find. c</span><span class="sxs-lookup"><span data-stu-id="d7469-118">lx_nand_flash_next_block_to_erase_find.c</span></span>
- <span data-ttu-id="d7469-119">lx_nand_flash_open. c</span><span class="sxs-lookup"><span data-stu-id="d7469-119">lx_nand_flash_open.c</span></span>
- <span data-ttu-id="d7469-120">lx_nand_flash_page_ecc_check. c</span><span class="sxs-lookup"><span data-stu-id="d7469-120">lx_nand_flash_page_ecc_check.c</span></span>
- <span data-ttu-id="d7469-121">lx_nand_flash_page_ecc_compute. c</span><span class="sxs-lookup"><span data-stu-id="d7469-121">lx_nand_flash_page_ecc_compute.c</span></span>  
- <span data-ttu-id="d7469-122">lx_nand_flash_partial_defragment. c</span><span class="sxs-lookup"><span data-stu-id="d7469-122">lx_nand_flash_partial_defragment.c</span></span>
- <span data-ttu-id="d7469-123">lx_nand_flash_physical_page_allocate. c</span><span class="sxs-lookup"><span data-stu-id="d7469-123">lx_nand_flash_physical_page_allocate.c</span></span>
- <span data-ttu-id="d7469-124">lx_nand_flash_sector_mapping_cache_invalidate. c</span><span class="sxs-lookup"><span data-stu-id="d7469-124">lx_nand_flash_sector_mapping_cache_invalidate.c</span></span>
- <span data-ttu-id="d7469-125">lx_nand_flash_sector_read. c</span><span class="sxs-lookup"><span data-stu-id="d7469-125">lx_nand_flash_sector_read.c</span></span>
- <span data-ttu-id="d7469-126">lx_nand_flash_sector_release. c</span><span class="sxs-lookup"><span data-stu-id="d7469-126">lx_nand_flash_sector_release.c</span></span>
- <span data-ttu-id="d7469-127">lx_nand_flash_sector_write. c</span><span class="sxs-lookup"><span data-stu-id="d7469-127">lx_nand_flash_sector_write.c</span></span>
- <span data-ttu-id="d7469-128">lx_nand_flash_system_error. c</span><span class="sxs-lookup"><span data-stu-id="d7469-128">lx_nand_flash_system_error.c</span></span>
- <span data-ttu-id="d7469-129">lx_nor_flash_block_reclaim. c</span><span class="sxs-lookup"><span data-stu-id="d7469-129">lx_nor_flash_block_reclaim.c</span></span>
- <span data-ttu-id="d7469-130">lx_nor_flash_close. c</span><span class="sxs-lookup"><span data-stu-id="d7469-130">lx_nor_flash_close.c</span></span>
- <span data-ttu-id="d7469-131">lx_nor_flash_defragment. c</span><span class="sxs-lookup"><span data-stu-id="d7469-131">lx_nor_flash_defragment.c</span></span>  
- <span data-ttu-id="d7469-132">lx_nor_flash_extended_cache_enable. c</span><span class="sxs-lookup"><span data-stu-id="d7469-132">lx_nor_flash_extended_cache_enable.c</span></span>
- <span data-ttu-id="d7469-133">lx_nor_flash_initialize. c</span><span class="sxs-lookup"><span data-stu-id="d7469-133">lx_nor_flash_initialize.c</span></span>
- <span data-ttu-id="d7469-134">lx_nor_flash_logical_sector_find. c</span><span class="sxs-lookup"><span data-stu-id="d7469-134">lx_nor_flash_logical_sector_find.c</span></span>
- <span data-ttu-id="d7469-135">lx_nor_flash_next_block_to_erase_find. c</span><span class="sxs-lookup"><span data-stu-id="d7469-135">lx_nor_flash_next_block_to_erase_find.c</span></span>
- <span data-ttu-id="d7469-136">lx_nor_flash_open. c</span><span class="sxs-lookup"><span data-stu-id="d7469-136">lx_nor_flash_open.c</span></span>
- <span data-ttu-id="d7469-137">lx_nor_flash_partial_defragment. c</span><span class="sxs-lookup"><span data-stu-id="d7469-137">lx_nor_flash_partial_defragment.c</span></span>
- <span data-ttu-id="d7469-138">lx_nor_flash_physical_sector_allocate. c</span><span class="sxs-lookup"><span data-stu-id="d7469-138">lx_nor_flash_physical_sector_allocate.c</span></span>
- <span data-ttu-id="d7469-139">lx_nor_flash_sector_mapping_cache_invalidate. c</span><span class="sxs-lookup"><span data-stu-id="d7469-139">lx_nor_flash_sector_mapping_cache_invalidate.c</span></span>
- <span data-ttu-id="d7469-140">lx_nor_flash_sector_read. c</span><span class="sxs-lookup"><span data-stu-id="d7469-140">lx_nor_flash_sector_read.c</span></span>
- <span data-ttu-id="d7469-141">lx_nor_flash_sector_release. c</span><span class="sxs-lookup"><span data-stu-id="d7469-141">lx_nor_flash_sector_release.c</span></span>
- <span data-ttu-id="d7469-142">lx_nor_flash_sector_write. c</span><span class="sxs-lookup"><span data-stu-id="d7469-142">lx_nor_flash_sector_write.c</span></span>
- <span data-ttu-id="d7469-143">lx_nor_flash_system_error. c</span><span class="sxs-lookup"><span data-stu-id="d7469-143">lx_nor_flash_system_error.c</span></span>

<span data-ttu-id="d7469-144">Sono disponibili anche esempi di driver simulatore e FileX per le istanze di LevelX NAND e NOR, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d7469-144">There are also simulator and FileX driver samples for both LevelX NAND and NOR instances, as follows.</span></span>

- <span data-ttu-id="d7469-145">demo_filex_nand_flash. c</span><span class="sxs-lookup"><span data-stu-id="d7469-145">demo_filex_nand_flash.c</span></span>  
- <span data-ttu-id="d7469-146">fx_nand_flash_simulated_driver. c</span><span class="sxs-lookup"><span data-stu-id="d7469-146">fx_nand_flash_simulated_driver.c</span></span>
- <span data-ttu-id="d7469-147">lx_nand_flash_simulator. c</span><span class="sxs-lookup"><span data-stu-id="d7469-147">lx_nand_flash_simulator.c</span></span>
- <span data-ttu-id="d7469-148">demo_filex_nor_flash. c</span><span class="sxs-lookup"><span data-stu-id="d7469-148">demo_filex_nor_flash.c</span></span>  
- <span data-ttu-id="d7469-149">fx_nor_flash_simulated_driver. c</span><span class="sxs-lookup"><span data-stu-id="d7469-149">fx_nor_flash_simulated_driver.c</span></span>
- <span data-ttu-id="d7469-150">lx_nor_flash_simulator. c</span><span class="sxs-lookup"><span data-stu-id="d7469-150">lx_nor_flash_simulator.c</span></span>

<span data-ttu-id="d7469-151">Naturalmente, se è necessario solo il flash NAND, sono necessari solo i file Flash NAND LevelX (***lx_nand_ \* . c***).</span><span class="sxs-lookup"><span data-stu-id="d7469-151">Of course, if only NAND flash is required, only the LevelX NAND flash files (***lx_nand_\*.c***) are needed.</span></span> <span data-ttu-id="d7469-152">Analogamente, se è necessario solo o Flash, sono necessari solo i file o i file Flash (\* \*_lx_nor_ \_ . c \* \* \*).</span><span class="sxs-lookup"><span data-stu-id="d7469-152">Similarly, if only NOR flash is required, only the NOR flash files (\*\*_lx_nor_\_.c\*\*\*) are needed.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="d7469-153">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="d7469-153">Configuration Options</span></span>

<span data-ttu-id="d7469-154">LevelX può essere configurato in fase di compilazione tramite le definizioni condizionali descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="d7469-154">LevelX can be configured at compile time via the conditional defines described below.</span></span> <span data-ttu-id="d7469-155">È sufficiente aggiungere la definizione desiderata alla compilazione di ogni origine LevelX per usare l'opzione.</span><span class="sxs-lookup"><span data-stu-id="d7469-155">Simply add the desired define to the compilation of each LevelX source to use the option.</span></span>

- <span data-ttu-id="d7469-156">**LX_DIRECT_READ**: definito, questa opzione consente di ignorare la routine di lettura del driver Flash, o di non leggere né direttamente la memoria, con un conseguente aumento significativo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d7469-156">**LX_DIRECT_READ**:  Defined, this option bypasses the NOR flash driver read routine in favor or reading the NOR memory directly, resulting in a significant performance increase.</span></span>
- <span data-ttu-id="d7469-157">**LX_FREE_SECTOR_DATA_VERIFY**: definito, in questo modo la logica di apertura della LevelX o dell'istanza per verificare il libero e i settori sono tutti quelli disponibili.</span><span class="sxs-lookup"><span data-stu-id="d7469-157">**LX_FREE_SECTOR_DATA_VERIFY**: Defined, this causes the LevelX NOR instance open logic to verify free NOR sectors are all ones.</span></span>
- <span data-ttu-id="d7469-158">**LX_NAND_SECTOR_MAPPING_CACHE_SIZE**: per impostazione predefinita, questo valore è 16 e definisce la dimensione della cache del mapping del settore logico.</span><span class="sxs-lookup"><span data-stu-id="d7469-158">**LX_NAND_SECTOR_MAPPING_CACHE_SIZE**:  By default this value is 16 and defines the logical sector mapping cache size.</span></span> <span data-ttu-id="d7469-159">I valori di grandi dimensioni migliorano le prestazioni, ma la memoria di costo.</span><span class="sxs-lookup"><span data-stu-id="d7469-159">Large values improve performance, but cost memory.</span></span> <span data-ttu-id="d7469-160">La dimensione minima è 8 e tutti i valori devono essere una potenza di 2.</span><span class="sxs-lookup"><span data-stu-id="d7469-160">The minimum size is 8 and all values must be a power of 2.</span></span>
- <span data-ttu-id="d7469-161">**LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: definito, viene creata una cache di mapping diretto, in modo che non vengano rilevati mancati riscontri nella cache.</span><span class="sxs-lookup"><span data-stu-id="d7469-161">**LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: Defined, this creates a direct mapping cache, such that there are no cache misses.</span></span> <span data-ttu-id="d7469-162">Richiede anche che LX_NAND_SECTOR_MAPPING_CACHE_SIZE rappresenti il numero esatto di pagine totali nel dispositivo flash.</span><span class="sxs-lookup"><span data-stu-id="d7469-162">It also requires that LX_NAND_SECTOR_MAPPING_CACHE_SIZE represents the exact number of total pages in your flash device.</span></span>
- <span data-ttu-id="d7469-163">**LX_NOR_DISABLE_EXTENDED_CACHE**: definito, disabilitato l'estensione o la cache.</span><span class="sxs-lookup"><span data-stu-id="d7469-163">**LX_NOR_DISABLE_EXTENDED_CACHE**: Defined, this disabled the extended NOR cache.</span></span>
- <span data-ttu-id="d7469-164">**LX_NOR_EXTENDED_CACHE_SIZE**: per impostazione predefinita, questo valore è 8, che rappresenta un massimo di 8 settori che possono essere memorizzati nella cache in un'istanza di o.</span><span class="sxs-lookup"><span data-stu-id="d7469-164">**LX_NOR_EXTENDED_CACHE_SIZE**: By default this value is 8, which represents a maximum of 8 sectors that can be cached in a NOR instance.</span></span>
- <span data-ttu-id="d7469-165">**LX_NOR_SECTOR_MAPPING_CACHE_SIZE**: per impostazione predefinita, questo valore è 16 e definisce la dimensione della cache del mapping del settore logico.</span><span class="sxs-lookup"><span data-stu-id="d7469-165">**LX_NOR_SECTOR_MAPPING_CACHE_SIZE**: By default this value is 16 and defines the logical sector mapping cache size.</span></span> <span data-ttu-id="d7469-166">I valori di grandi dimensioni migliorano le prestazioni, ma la memoria di costo.</span><span class="sxs-lookup"><span data-stu-id="d7469-166">Large values improve performance, but cost memory.</span></span> <span data-ttu-id="d7469-167">La dimensione minima è 8 e tutti i valori devono essere una potenza di 2.</span><span class="sxs-lookup"><span data-stu-id="d7469-167">The minimum size is 8 and all values must be a power of 2.</span></span>
- <span data-ttu-id="d7469-168">**LX_THREAD_SAFE_ENABLE**: definito, rende thread-safe LevelX usando un oggetto mutex THREADX nell'API.</span><span class="sxs-lookup"><span data-stu-id="d7469-168">**LX_THREAD_SAFE_ENABLE**: Defined, this makes LevelX thread-safe by using a ThreadX mutex object throughout the API.</span></span>

## <a name="using-levelx"></a><span data-ttu-id="d7469-169">Uso di LevelX</span><span class="sxs-lookup"><span data-stu-id="d7469-169">Using LevelX</span></span>

<span data-ttu-id="d7469-170">Per usare LevelX, da solo o con FileX, includere il file \***lx_api. h** _ nel codice che fa riferimento all'API LevelX.</span><span class="sxs-lookup"><span data-stu-id="d7469-170">To use LevelX, either by itself or with FileX, include the file \***lx_api.h** _ in the code that references the LevelX API.</span></span> <span data-ttu-id="d7469-171">Assicurarsi inoltre che il codice dell'oggetto LevelX sia disponibile in fase di collegamento.</span><span class="sxs-lookup"><span data-stu-id="d7469-171">Also ensure that the LevelX object code is available at link time.</span></span> <span data-ttu-id="d7469-172">Per esempi relativi all'uso di LevelX, esaminare i file _*_demo_filex_nand_flash. c_*_ e _ \*_demo_filex_nor_flash. c_\*\*.</span><span class="sxs-lookup"><span data-stu-id="d7469-172">Please examine the files _*_demo_filex_nand_flash.c_*_ and _ *_demo_filex_nor_flash.c_*\* for examples of how to use LevelX.</span></span>
