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
# <a name="chapter-1---introduction-to-azure-rtos-tracex"></a><span data-ttu-id="2a61d-103">Capitolo 1-Introduzione ad Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="2a61d-103">Chapter 1 - Introduction to Azure RTOS TraceX</span></span>

<span data-ttu-id="2a61d-104">Azure RTO TraceX è uno strumento di analisi di sistema Microsoft che visualizza le informazioni sugli eventi di sistema raccolte da ThreadX in esecuzione in una destinazione incorporata.</span><span class="sxs-lookup"><span data-stu-id="2a61d-104">Azure RTOS TraceX is a Microsoft system analysis tool that displays system event information gathered by ThreadX running on an embedded target.</span></span> <span data-ttu-id="2a61d-105">L'utente è responsabile del trasferimento del buffer di traccia archiviato in RAM nella destinazione incorporata in un file binario nel computer host.</span><span class="sxs-lookup"><span data-stu-id="2a61d-105">The user is responsible for transferring the trace buffer stored in RAM in the embedded target to a binary file on the host computer.</span></span> <span data-ttu-id="2a61d-106">L'utente può quindi aprire il file con TraceX e analizzare graficamente gli eventi di destinazione, diagnosticare i problemi di sistema e ottimizzare un'applicazione funzionante per migliorare le prestazioni e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="2a61d-106">The user can then open this file with TraceX and graphically analyze the target events, diagnosing system problems and tuning a working application to improve performance and resource management.</span></span>

## <a name="tracex-requirements"></a><span data-ttu-id="2a61d-107">Requisiti di TraceX</span><span class="sxs-lookup"><span data-stu-id="2a61d-107">TraceX Requirements</span></span>

<span data-ttu-id="2a61d-108">TraceX richiede Windows XP (o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="2a61d-108">TraceX requires Windows XP (or above).</span></span> <span data-ttu-id="2a61d-109">Il sistema deve avere un minimo di 192 MB di RAM, 2 GB di spazio disponibile su disco rigido e una visualizzazione minima di 1024x768 con colori 256.</span><span class="sxs-lookup"><span data-stu-id="2a61d-109">The system should have a minimum of 192 MB of RAM, 2 GB of available hard-disk space, and a minimum display of 1024x768 with 256 colors.</span></span> <span data-ttu-id="2a61d-110">Inoltre, l'applicazione deve essere in esecuzione in ThreadX V 5.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2a61d-110">In addition, the application must be running on ThreadX V5.0 or later.</span></span>

<span data-ttu-id="2a61d-111">TraceX richiede anche l'installazione di Microsoft .NET Framework, che il programma di installazione di TraceX esegue automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2a61d-111">TraceX also requires the Microsoft .NET framework be installed, which the TraceX installer does automatically.</span></span>

## <a name="tracex-constraints"></a><span data-ttu-id="2a61d-112">Vincoli TraceX</span><span class="sxs-lookup"><span data-stu-id="2a61d-112">TraceX Constraints</span></span>

<span data-ttu-id="2a61d-113">TraceX presenta i vincoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a61d-113">TraceX has the following constraints:</span></span>

- <span data-ttu-id="2a61d-114">I file TraceX sono limitati a un massimo di 32.768 eventi (circa 1 MB).</span><span class="sxs-lookup"><span data-stu-id="2a61d-114">TraceX files are limited to a maximum of 32,768 events (roughly 1 MB ).</span></span>
- <span data-ttu-id="2a61d-115">L'origine dell'indicatore di data e ora deve avere una risoluzione ragionevole.</span><span class="sxs-lookup"><span data-stu-id="2a61d-115">The time-stamp source must have reasonable resolution.</span></span> <span data-ttu-id="2a61d-116">Se la risoluzione è troppo bassa, gli eventi si sovrappongono.</span><span class="sxs-lookup"><span data-stu-id="2a61d-116">If the resolution is too low, the events will overlap.</span></span> <span data-ttu-id="2a61d-117">Se la risoluzione è troppo elevata, è possibile che si verifichino Gap prolunghe tra gli eventi.</span><span class="sxs-lookup"><span data-stu-id="2a61d-117">If the resolution is too high, there is potential for long gaps between events.</span></span>
- <span data-ttu-id="2a61d-118">TraceX non è in grado di misurare accuratamente gli intervalli tra gli eventi maggiori del periodo del timer.</span><span class="sxs-lookup"><span data-stu-id="2a61d-118">TraceX cannot accurately measure intervals between events greater than the timer period.</span></span>
