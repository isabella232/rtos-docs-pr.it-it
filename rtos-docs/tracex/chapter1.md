---
title: Capitolo 1-Introduzione ad Azure RTO TraceX
description: Azure RTO TraceX è uno strumento di analisi di sistema Microsoft che visualizza le informazioni sugli eventi di sistema raccolte da ThreadX in esecuzione in una destinazione incorporata.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 3009d13388b3b7e8eca041dc6ede569a5caf5e9b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823588"
---
# <a name="chapter-1---introduction-to-azure-rtos-tracex"></a>Capitolo 1-Introduzione ad Azure RTO TraceX

Azure RTO TraceX è uno strumento di analisi di sistema Microsoft che visualizza le informazioni sugli eventi di sistema raccolte da ThreadX in esecuzione in una destinazione incorporata. L'utente è responsabile del trasferimento del buffer di traccia archiviato in RAM nella destinazione incorporata in un file binario nel computer host. L'utente può quindi aprire il file con TraceX e analizzare graficamente gli eventi di destinazione, diagnosticare i problemi di sistema e ottimizzare un'applicazione funzionante per migliorare le prestazioni e la gestione delle risorse.

## <a name="tracex-requirements"></a>Requisiti di TraceX

TraceX richiede Windows XP (o versione successiva). Il sistema deve avere un minimo di 192 MB di RAM, 2 GB di spazio disponibile su disco rigido e una visualizzazione minima di 1024x768 con colori 256. Inoltre, l'applicazione deve essere in esecuzione in ThreadX V 5.0 o versione successiva.

TraceX richiede anche l'installazione di Microsoft .NET Framework, che il programma di installazione di TraceX esegue automaticamente.

## <a name="tracex-constraints"></a>Vincoli TraceX

TraceX presenta i vincoli seguenti:

- I file TraceX sono limitati a un massimo di 32.768 eventi (circa 1 MB).
- L'origine dell'indicatore di data e ora deve avere una risoluzione ragionevole. Se la risoluzione è troppo bassa, gli eventi si sovrappongono. Se la risoluzione è troppo elevata, è possibile che si verifichino Gap prolunghe tra gli eventi.
- TraceX non è in grado di misurare accuratamente gli intervalli tra gli eventi maggiori del periodo del timer.
