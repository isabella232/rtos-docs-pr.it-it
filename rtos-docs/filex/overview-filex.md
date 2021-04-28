---
title: Informazioni Azure RTOS FileX
description: Azure RTOS FileX è un file system compatibile con FAT (High Performance, Tabella di allocazione file) completamente integrato con Azure RTOS ThreadX e disponibile per tutti i processori supportati. Come Azure RTOS ThreadX, Azure RTOS FileX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni attualmente incorporate che richiedono operazioni di gestione dei file. FileX supporta la maggior parte dei supporti fisici, tra cui RAM, Azure RTOS memoria flash USBX, SD CARD e NAND/NOR tramite Azure RTOS LevelX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0a54f160c96fb3e90c2295ae72020c121d367a12
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171353"
---
# <a name="overview-of-azure-rtos-filex"></a>Panoramica di Azure RTOS FileX

Azure RTOS fileX embedded file system è la soluzione avanzata di livello industriale di Azure RTOS per i formati di file FAT Microsoft, progettata specificamente per applicazioni IoT, in tempo reale e con un'incorporazione approfondita. Azure RTOS FileX supporta tutti i formati di file microsoft, inclusi FAT12, FAT16, FAT32 ed exFAT. FileX offre anche la tolleranza di errore facoltativa e il livellamento dell'usura FLASH tramite un prodotto aggiuntivo denominato [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/). Tutto questo in combinazione con un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rendono Azure RTOS FileX la scelta ideale per le applicazioni IoT incorporate più complesse.

## <a name="api-protocols"></a>Protocolli API

### <a name="media-services"></a>Servizi multimediali

- Supporto di FAT 16/16/32 ed exFAT
- MINIMO FLASH da 6 KB, 2,5 KB di RAM
- Completare i servizi di accesso ai supporti
- Numero illimitato di istanze di supporti
- Interfaccia del driver del settore logico di lettura/scrittura semplice
- Supporto di più partizioni
- Cache del settore logico
- Cache delle voci FAT
- Supporto facoltativo per la tolleranza di errore
- Aggiornamento FAT secondario posticipato
- Traccia a livello di sistema tramite Azure RTOS TraceX
- API intuitive per l'accesso ai supporti, tra cui:
  - fx_media_open
  - fx_media_close
  - fx_media_format
  - fx_media_space_available

### <a name="directory-services"></a>Servizi directory

- Percorsi fino a 256 byte
- Nomi di directory lunghi e 8.3 supportati
- Creazione della directory & eliminazione
- Navigazione e attraversamento delle directory
- Gestione degli attributi della directory
- Traccia a livello di sistema tramite Azure RTOS TraceX
- API intuitive per l'accesso alla directory, tra cui:
  - fx_directory_create
  - fx_directory_delete
  - fx_directory_attributes_set
  - fx_directory_attributes_read
  - fx_directory_first_entry_find
  - fx_directory_next_entry_find

### <a name="file-services"></a>Servizi file

- Flash minimo da 3,3 KB
- File aperti illimitati
- I file di sola lettura possono essere aperti più volte
- Nomi di directory lunghi e 8.3 supportati
- Supporto di file contigui
- Logica di ricerca rapida
- Preallocazione dei cluster
- Creazione, eliminazione e ridenominazione di file
- Lettura, scrittura e lettura di file
- Gestione degli attributi di file
- Traccia a livello di sistema tramite Azure RTOS TraceX
- API di accesso ai file intuitive, tra cui:
  - fx_file_create
  - fx_file_delete
  - fx_file_attributes_set
  - fx_file_attributes_read
  - fx_file_read
  - fx_file_seek
  - fx_file_write

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTOS FileX è una tecnologia avanzata, tra cui:

- Supporto fat 12/16/32 ed exFAT
- Supporto di più partizioni
- Scalabilità automatica
- Neutrale endian
- Nome file lungo e supporto 8.3
- Supporto della tolleranza di errore facoltativo
- Cache dei settori logici
- Cache delle voci FAT
- Preallocazione dei cluster
- Supporto di file contigui
- Metriche facoltative delle prestazioni
- Azure RTOS di analisi del sistema TraceX

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a>NOR/NAND Wear Leveling (Azure RTOS LevelX)

Azure RTOS LevelX è il prodotto Microsoft di livellamento per usura NOR/NAND FLASH. Azure RTOS LevelX può essere usato in combinazione con FileX o come libreria di settore FLASH di lettura/scrittura diretta autonoma per l'applicazione.
