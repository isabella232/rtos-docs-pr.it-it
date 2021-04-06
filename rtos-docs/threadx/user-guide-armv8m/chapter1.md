---
title: Capitolo 1-Introduzione ad Azure RTO ThreadX per ARMv8-M.
description: Questo capitolo è il punto di partenza per leggere l'addendum di Azure RTO ThreadX per ARMv8-M.
author: v-condav
ms.author: v-condav
ms.date: 03/04/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 486466f41e64adb9e32ebbd21a22629221ffa9c1
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377595"
---
# <a name="chapter-1--overview"></a>Panoramica del capitolo 1

L'architettura ARMv8-M introduce nuove funzionalità di sicurezza, tra cui TrustZone, che consente di contrassegnare la memoria come protetta o non protetta. Le linee guida seguenti per ARM, ThreadX (e l'applicazione utente) sono progettate per essere eseguite in modalità non protetta. ThreadX e l'applicazione utente possono essere eseguiti anche in modalità protetta. Per l'interfaccia con software in modalità protetta, sono necessarie alcune nuove API ThreadX. Questo documento descrive i servizi ThreadX specifici dell'architettura ARMv8-M, tra cui Cortex-M23, Cortex-M33, Cortex-M35P e Cortex-M55.
