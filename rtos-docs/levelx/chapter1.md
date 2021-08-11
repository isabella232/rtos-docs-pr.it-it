---
title: Capitolo 1 - Panoramica di Azure RTOS LevelX
description: Azure RTOS LevelX fornisce funzionalità di livellamento dell'usura flash NAD e NOR alle applicazioni incorporate.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 73c06d48b98081291d83635e049e6cf8641714c87efe815f9399f3fbab3a6211
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790599"
---
# <a name="chapter-1---overview-of-azure-rtos-levelx"></a>Capitolo 1 - Panoramica di Azure RTOS LevelX

Azure RTOS LevelX fornisce funzionalità di livellamento dell'usura flash NAD e NOR alle applicazioni incorporate. Poiché la memoria flash NAD e NOR può essere cancellata solo un numero finito di volte, è fondamentale distribuire uniformemente l'uso della memoria flash. Questo è in genere detto "livello di usura" ed è lo scopo alla base di LevelX.

L'algoritmo che sceglie il blocco flash da riutilizzare si basa principalmente sul conteggio delle cancellazioni, ma non interamente. Il blocco con il conteggio di cancellazione più basso potrebbe non essere scelto se è presente un altro blocco con un conteggio di cancellazione all'interno di un delta accettabile dal conteggio di cancellazione minima e con un numero maggiore di mapping obsoleti. In questi casi, il blocco con il maggior numero di mapping obsoleti verrà cancellato e riutilizzato, risparmiando così un sovraccarico nello spostamento di voci di mapping valide.

LevelX supporta più istanze di parti NAD e/o NOR, ad esempio l'applicazione può utilizzare istanze separate di LevelX all'interno della stessa applicazione. Ogni istanza richiede il proprio blocco di controllo fornito dall'applicazione e il relativo driver flash.

LevelX presenta all'utente una matrice di settori logici mappati alla memoria flash fisica all'interno di LevelX. Per migliorare le prestazioni, LevelX fornisce anche una cache dei mapping dei settori logici più recenti. Le dimensioni di questa cache vengono definite dal programmatore. Le applicazioni possono usare LevelX in combinazione con FileX o possono leggere/scrivere direttamente settori logici. LevelX non ha alcuna dipendenza da FileX e una dipendenza molto piccola da ThreadX (vengono usati solo tipi di dati ThreadX primitivi).

LevelX è progettato per la tolleranza di errore. Gli aggiornamenti flash vengono eseguiti in un processo in più passaggi che può essere interrotto in ogni passaggio. LevelX ripristina automaticamente lo stato ottimale durante l'operazione successiva.

LevelX richiede un driver flash per l'accesso fisico alla memoria flash sottostante. Vengono forniti driver simulati NAD e NOR di esempio che possono essere usati come punto di partenza per l'implementazione di driver LevelX effettivi. Inoltre, i requisiti dei driver sono dettagliati più avanti in questa documentazione.

I capitoli seguenti descrivono l'operazione funzionale per il supporto NAD e NOR LevelX.
