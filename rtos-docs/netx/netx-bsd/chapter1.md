---
title: Capitolo 1-Introduzione ad Azure RTO NetX BSD
description: Il wrapper dell'API compliancy di NetX BSD Sockets di Azure RTO supporta alcune delle chiamate API di base per i socket BSD con alcune limitazioni e usa le primitive NetX sotto.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: fce781ac97ae75c4148614453eeb35c3064f8849
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821512"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-bsd"></a>Capitolo 1-Introduzione ad Azure RTO NetX BSD

Il wrapper compliancy dell'API NetX BSD Sockets supporta alcune delle chiamate API di base per i socket BSD con alcune limitazioni e usa le primitive NetX sotto. Questo livello di compatibilità API dei socket BSD dovrebbe essere eseguito come veloce o leggermente più veloce delle implementazioni BSD tipiche, perché questo wrapper usa le primitive NetX interne e ignora il controllo degli errori NetX di base.

## <a name="bsd-sockets-api-compliancy-wrapper-source"></a>Origine wrapper compliancy API socket BSD

Il codice sorgente del wrapper BSD è progettato per semplicità ed è costituito solo da due file, *nx_bsd. h* e *nx_bsd. c*. Il file *nx_bsd. h* definisce tutte le costanti e i prototipi di subroutine del wrapper API per i socket BSD, mentre *nx_bsd. c* contiene il codice sorgente di compatibilità API per i socket BSD effettivi. Questi file di origine del wrapper BSD sono comuni a tutti i pacchetti di supporto NetX.

Il pacchetto è costituito da:

- **nx_bsd. c**: codice sorgente wrapper
- **nx_bsd. h**: file di intestazione principale

Programmi demo di esempio:

- **bsd_demo_tcp. c**: *demo con un singolo server e client TCP*
- **bsd_demo_udp. c**: *demo con due client UDP e un server UDP*
