---
title: Capitolo 1-Panoramica di Azure RTO LevelX
description: Azure RTO LevelX offre funzionalità di livellamento NAND e NOR Flash per le applicazioni incorporate.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 045446fec74164f125bc0ad27e8b7a904be14ab2
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822178"
---
# <a name="chapter-1---overview-of-azure-rtos-levelx"></a>Capitolo 1-Panoramica di Azure RTO LevelX

Azure RTO LevelX offre funzionalità di livellamento NAND e NOR Flash per le applicazioni incorporate. Poiché sia la memoria NAND che quella Flash possono essere cancellate solo un numero finito di volte, è fondamentale distribuire l'uso della memoria flash in modo uniforme. Questa operazione viene in genere definita "livellamento dell'utilizzo" ed è lo scopo dietro LevelX.

L'algoritmo che sceglie il blocco Flash da riutilizzare si basa principalmente sul conteggio delle eliminazioni, ma non interamente. Il blocco con il numero di cancellazioni più basso potrebbe non essere scelto se è presente un altro blocco con un conteggio di cancellazione in un Delta accettabile rispetto al numero minimo di cancellazioni e con un numero maggiore di mapping obsoleti. In questi casi, il blocco con il maggior numero di mapping obsoleti verrà cancellato e riutilizzato, risparmiando in questo modo il sovraccarico nello stato di movimenti di mapping validi.

LevelX supporta più istanze di NAND e/o né parti, ad esempio, l'applicazione può usare istanze separate di LevelX all'interno della stessa applicazione. Ogni istanza richiede il proprio blocco di controllo fornito dall'applicazione, nonché il proprio driver Flash.

LevelX presenta all'utente una matrice di settori logici mappati alla memoria flash fisica all'interno di LevelX. Per migliorare le prestazioni, LevelX fornisce anche una cache dei mapping del settore logico più recenti. Le dimensioni della cache sono definite dal programmatore. Le applicazioni possono usare LevelX insieme a FileX o possono leggere/scrivere direttamente settori logici. LevelX non ha dipendenze da FileX e una dipendenza minima da ThreadX (vengono usati solo i tipi di dati ThreadX primitivi).

LevelX è progettato per la tolleranza di errore. Gli aggiornamenti flash vengono eseguiti in un processo in più passaggi che possono essere interrotti in ogni passaggio. LevelX esegue automaticamente il ripristino dello stato ottimale durante l'operazione successiva.

LevelX richiede un driver Flash per l'accesso fisico alla memoria flash sottostante. I driver NAND e non simulati di esempio vengono forniti e possono essere usati come punto di partenza valido per implementare i driver LevelX effettivi. Inoltre, i requisiti dei driver sono descritti in dettaglio più avanti in questa documentazione.

I capitoli seguenti descrivono l'operazione funzionale per il supporto di NAND e non LevelX.
