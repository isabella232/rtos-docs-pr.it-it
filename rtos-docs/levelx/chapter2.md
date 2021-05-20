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
# <a name="chapter-2---installation-and-use-of-azure-rtos-levelx"></a>Capitolo 2 - Installazione e uso di Azure RTOS LevelX

L'installazione e l Azure RTOS di LevelX sono semplici e descritte nelle sezioni seguenti di questo capitolo.

## <a name="distribution"></a>Distribuzione

LevelX viene distribuito in ANSI C in cui ogni funzione è contenuta in un file C separato. I file nella distribuzione LevelX sono i seguenti.
- lx_api.h
- lx_nand_flash_256byte_ecc_check.c
- lx_nand_flash_256byte_ecc_compute.c
- lx_nand_flash_block_full_update.c
- lx_nand_flash_block_reclaim.c
- lx_nand_flash_close.c
- lx_nand_flash_defragment.c  
- lx_nand_flash_extended_cache_enable.c
- lx_nand_flash_initialize.c
- lx_nand_flash_logical_sector_find.c
- lx_nand_flash_next_block_to_erase_find.c
- lx_nand_flash_open.c
- lx_nand_flash_page_ecc_check.c
- lx_nand_flash_page_ecc_compute.c  
- lx_nand_flash_partial_defragment.c
- lx_nand_flash_physical_page_allocate.c
- lx_nand_flash_sector_mapping_cache_invalidate.c
- lx_nand_flash_sector_read.c
- lx_nand_flash_sector_release.c
- lx_nand_flash_sector_write.c
- lx_nand_flash_system_error.c
- lx_nor_flash_block_reclaim.c
- lx_nor_flash_close.c
- lx_nor_flash_defragment.c  
- lx_nor_flash_extended_cache_enable.c
- lx_nor_flash_initialize.c
- lx_nor_flash_logical_sector_find.c
- lx_nor_flash_next_block_to_erase_find.c
- lx_nor_flash_open.c
- lx_nor_flash_partial_defragment.c
- lx_nor_flash_physical_sector_allocate.c
- lx_nor_flash_sector_mapping_cache_invalidate.c
- lx_nor_flash_sector_read.c
- lx_nor_flash_sector_release.c
- lx_nor_flash_sector_write.c
- lx_nor_flash_system_error.c

Sono disponibili anche esempi di simulatori e driver FileX per le istanze NAD levelx e NOR, come indicato di seguito.

- demo_filex_nand_flash.c  
- fx_nand_flash_simulated_driver.c
- lx_nand_flash_simulator.c
- demo_filex_nor_flash.c  
- fx_nor_flash_simulated_driver.c
- lx_nor_flash_simulator.c

Naturalmente, se è necessaria solo la memoria flash NAD, sono necessari solo i file flash NAD LevelX (***lx_nand_ \* .c***). Analogamente, se è necessaria solo la memoria flash NOR, sono necessari solo i file flash NOR (**_lx_nor_ \_ .c***).

## <a name="configuration-options"></a>Opzioni di configurazione

LevelX può essere configurato in fase di compilazione tramite le definizione condizionali descritte di seguito. È sufficiente aggiungere la definizione desiderata alla compilazione di ogni origine LevelX per usare l'opzione .

- **LX_DIRECT_READ:** definita, questa opzione ignora la routine di lettura del driver flash NOR a favore o legge direttamente la memoria NOR, con un conseguente aumento significativo delle prestazioni.
- **LX_FREE_SECTOR_DATA_VERIFY:** definito, in questo modo la logica aperta dell'istanza di LevelX NOR verifica che i settori NOR liberi siano tutti quelli.
- **LX_NAND_SECTOR_MAPPING_CACHE_SIZE:** per impostazione predefinita questo valore è 16 e definisce le dimensioni della cache per il mapping dei settori logici. Valori di grandi dimensioni migliorano le prestazioni, ma costi di memoria. La dimensione minima è 8 e tutti i valori devono essere una potenza di 2.
- **LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: definito, viene creata una cache di mapping diretto, in modo che non siano presenti mancati riscontri nella cache. Richiede anche che LX_NAND_SECTOR_MAPPING_CACHE_SIZE rappresenta il numero esatto di pagine totali nel dispositivo flash.
- **LX_NOR_DISABLE_EXTENDED_CACHE**: definito, la cache NOR estesa è stata disabilitata.
- **LX_NOR_EXTENDED_CACHE_SIZE:** per impostazione predefinita questo valore è 8, che rappresenta un massimo di 8 settori che possono essere memorizzati nella cache in un'istanza di NOR.
- **LX_NOR_SECTOR_MAPPING_CACHE_SIZE:** per impostazione predefinita, questo valore è 16 e definisce le dimensioni della cache per il mapping dei settori logici. Valori di grandi dimensioni migliorano le prestazioni, ma costi di memoria. La dimensione minima è 8 e tutti i valori devono essere una potenza di 2.
- **LX_THREAD_SAFE_ENABLE:** definito, questo rende LevelX thread-safe usando un oggetto mutex ThreadX in tutta l'API.
- **LX_STANDALONE_ENABLE**: definito, consente l'uso di LevelX in modalità autonoma (senza Azure RTOS). Per impostazione predefinita, questo simbolo non è definito.

> [!IMPORTANT]
> Quando si usa LevelX in modalità autonoma **(LX_STANDALONE_ENABLE** deve essere definito), i file/librerie ThreadX non sono necessari. La funzionalità thread-safe LevelX è disabilitata in questa modalità.

## <a name="using-levelx"></a>Uso di LevelX

Per usare LevelX, da solo o con FileX, includere il file ***lx_api.h** _ nel codice che fa riferimento all'API LevelX. Assicurarsi anche che il codice dell'oggetto LevelX sia disponibile in fase di collegamento. Esaminare i file _*_demo_filex_nand_flash.c_*_ e _ *_demo_filex_nor_flash.c_** per esempi su come usare LevelX.
