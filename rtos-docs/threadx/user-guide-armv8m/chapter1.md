---
title: Capitolo 1 - Introduzione a Azure RTOS ThreadX per ARMv8-M.
description: Questo capitolo è il punto di partenza per la lettura del Azure RTOS ThreadX Addendum per ARMv8-M.
author: v-condav
ms.author: v-condav
ms.date: 03/04/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1f0d87ec562c7fcfa6af5d2240655ef526f6e0611d509fe60c745436371413d7
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798249"
---
# <a name="chapter-1--overview"></a>Panoramica del capitolo 1

L'architettura ARMv8-M introduce nuove funzionalità di sicurezza, tra cui TrustZone, che consente di contrassegnare la memoria come sicura o non sicura. Seguendo le linee guida di ARM, ThreadX (e l'applicazione utente) è progettato per essere eseguito in modalità non protetta. ThreadX (e l'applicazione utente) possono essere eseguiti anche in modalità protetta. Per interfacciarsi con il software in modalità sicura, sono necessarie alcune nuove API ThreadX. Questo documento descrive questi servizi ThreadX specifici dell'architettura ARMv8-M, tra cui Cortex-M23, Cortex-M33, Cortex-M35P e Cortex-M55.
