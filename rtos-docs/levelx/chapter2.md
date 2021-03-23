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
# <a name="chapter-2---installation-and-use-of-azure-rtos-levelx"></a>Capitolo 2-installazione e uso di Azure RTO LevelX

L'installazione e l'uso di Azure RTO LevelX sono semplici e descritti nelle sezioni seguenti di questo capitolo.

## <a name="distribution"></a>Distribuzione

LevelX viene distribuito in ANSI C, dove ogni funzione è contenuta nel proprio file C separato. I file nella distribuzione LevelX sono i seguenti.
- lx_api. h
- lx_nand_flash_256byte_ecc_check. c
- lx_nand_flash_256byte_ecc_compute. c
- lx_nand_flash_block_full_update. c
- lx_nand_flash_block_reclaim. c
- lx_nand_flash_close. c
- lx_nand_flash_defragment. c  
- lx_nand_flash_extended_cache_enable. c
- lx_nand_flash_initialize. c
- lx_nand_flash_logical_sector_find. c
- lx_nand_flash_next_block_to_erase_find. c
- lx_nand_flash_open. c
- lx_nand_flash_page_ecc_check. c
- lx_nand_flash_page_ecc_compute. c  
- lx_nand_flash_partial_defragment. c
- lx_nand_flash_physical_page_allocate. c
- lx_nand_flash_sector_mapping_cache_invalidate. c
- lx_nand_flash_sector_read. c
- lx_nand_flash_sector_release. c
- lx_nand_flash_sector_write. c
- lx_nand_flash_system_error. c
- lx_nor_flash_block_reclaim. c
- lx_nor_flash_close. c
- lx_nor_flash_defragment. c  
- lx_nor_flash_extended_cache_enable. c
- lx_nor_flash_initialize. c
- lx_nor_flash_logical_sector_find. c
- lx_nor_flash_next_block_to_erase_find. c
- lx_nor_flash_open. c
- lx_nor_flash_partial_defragment. c
- lx_nor_flash_physical_sector_allocate. c
- lx_nor_flash_sector_mapping_cache_invalidate. c
- lx_nor_flash_sector_read. c
- lx_nor_flash_sector_release. c
- lx_nor_flash_sector_write. c
- lx_nor_flash_system_error. c

Sono disponibili anche esempi di driver simulatore e FileX per le istanze di LevelX NAND e NOR, come indicato di seguito.

- demo_filex_nand_flash. c  
- fx_nand_flash_simulated_driver. c
- lx_nand_flash_simulator. c
- demo_filex_nor_flash. c  
- fx_nor_flash_simulated_driver. c
- lx_nor_flash_simulator. c

Naturalmente, se è necessario solo il flash NAND, sono necessari solo i file Flash NAND LevelX (***lx_nand_ \* . c***). Analogamente, se è necessario solo o Flash, sono necessari solo i file o i file Flash (* *_lx_nor_ \_ . c * * *).

## <a name="configuration-options"></a>Opzioni di configurazione

LevelX può essere configurato in fase di compilazione tramite le definizioni condizionali descritte di seguito. È sufficiente aggiungere la definizione desiderata alla compilazione di ogni origine LevelX per usare l'opzione.

- **LX_DIRECT_READ**: definito, questa opzione consente di ignorare la routine di lettura del driver Flash, o di non leggere né direttamente la memoria, con un conseguente aumento significativo delle prestazioni.
- **LX_FREE_SECTOR_DATA_VERIFY**: definito, in questo modo la logica di apertura della LevelX o dell'istanza per verificare il libero e i settori sono tutti quelli disponibili.
- **LX_NAND_SECTOR_MAPPING_CACHE_SIZE**: per impostazione predefinita, questo valore è 16 e definisce la dimensione della cache del mapping del settore logico. I valori di grandi dimensioni migliorano le prestazioni, ma la memoria di costo. La dimensione minima è 8 e tutti i valori devono essere una potenza di 2.
- **LX_NAND_FLASH_DIRECT_MAPPING_CACHE**: definito, viene creata una cache di mapping diretto, in modo che non vengano rilevati mancati riscontri nella cache. Richiede anche che LX_NAND_SECTOR_MAPPING_CACHE_SIZE rappresenti il numero esatto di pagine totali nel dispositivo flash.
- **LX_NOR_DISABLE_EXTENDED_CACHE**: definito, disabilitato l'estensione o la cache.
- **LX_NOR_EXTENDED_CACHE_SIZE**: per impostazione predefinita, questo valore è 8, che rappresenta un massimo di 8 settori che possono essere memorizzati nella cache in un'istanza di o.
- **LX_NOR_SECTOR_MAPPING_CACHE_SIZE**: per impostazione predefinita, questo valore è 16 e definisce la dimensione della cache del mapping del settore logico. I valori di grandi dimensioni migliorano le prestazioni, ma la memoria di costo. La dimensione minima è 8 e tutti i valori devono essere una potenza di 2.
- **LX_THREAD_SAFE_ENABLE**: definito, rende thread-safe LevelX usando un oggetto mutex THREADX nell'API.

## <a name="using-levelx"></a>Uso di LevelX

Per usare LevelX, da solo o con FileX, includere il file ***lx_api. h** _ nel codice che fa riferimento all'API LevelX. Assicurarsi inoltre che il codice dell'oggetto LevelX sia disponibile in fase di collegamento. Per esempi relativi all'uso di LevelX, esaminare i file _*_demo_filex_nand_flash. c_*_ e _ *_demo_filex_nor_flash. c_**.
