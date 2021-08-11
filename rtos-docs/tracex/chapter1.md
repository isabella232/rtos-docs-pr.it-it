---
title: Capitolo 1 - Introduzione a Azure RTOS TraceX
description: Azure RTOS TraceX è uno strumento di analisi di sistema Microsoft che visualizza le informazioni sugli eventi di sistema raccolte da ThreadX in esecuzione in una destinazione incorporata.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 70eb06341e5d57f59c74888046bda3bbf95dc88cac56332be640d9576551796f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785057"
---
# <a name="chapter-1---introduction-to-azure-rtos-tracex"></a>Capitolo 1 - Introduzione a Azure RTOS TraceX

Azure RTOS TraceX è uno strumento di analisi di sistema Microsoft che visualizza le informazioni sugli eventi di sistema raccolte da ThreadX in esecuzione in una destinazione incorporata. L'utente è responsabile del trasferimento del buffer di traccia archiviato nella RAM nella destinazione incorporata in un file binario nel computer host. L'utente può quindi aprire questo file con TraceX e analizzare graficamente gli eventi di destinazione, diagnosticando i problemi di sistema e ottimizzare un'applicazione funzionante per migliorare le prestazioni e la gestione delle risorse.

## <a name="tracex-requirements"></a>Requisiti di TraceX

TraceX richiede Windows XP (o versione superiore). Il sistema deve avere almeno 192 MB di RAM, 2 GB di spazio disponibile su disco rigido e una visualizzazione minima di 1024x768 con 256 colori. Inoltre, l'applicazione deve essere in esecuzione in ThreadX V5.0 o versione successiva.

TraceX richiede anche l'installazione Microsoft .NET framework di traccia, che viene eseguita automaticamente dal programma di installazione di TraceX.

## <a name="tracex-constraints"></a>Vincoli TraceX

TraceX presenta i vincoli seguenti:

- I file TraceX sono limitati a un massimo di 32.768 eventi (circa 1 MB).
- L'origine timestamp deve avere una risoluzione ragionevole. Se la risoluzione è troppo bassa, gli eventi si sovrapporranno. Se la risoluzione è troppo elevata, potrebbero verificarsi lunghi gap tra gli eventi.
- TraceX non può misurare in modo accurato gli intervalli tra gli eventi superiori al periodo del timer.
