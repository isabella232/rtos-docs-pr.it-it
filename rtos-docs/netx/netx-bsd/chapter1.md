---
title: Capitolo 1 - Introduzione a Azure RTOS NetX BSD
description: Il wrapper Azure RTOS'API SocketSD NetX BSD supporta alcune delle chiamate API BSD Sockets di base con alcune limitazioni e usa le primitive NetX sottostanti.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b58283a38a25ffdd438d7853999f3b6e390f280a947aa45101d8df86447bf3dd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796720"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-bsd"></a>Capitolo 1 - Introduzione a Azure RTOS NetX BSD

NetX BSD Sockets API Compliancy Wrapper supporta alcune delle chiamate API BSD Sockets di base con alcune limitazioni e usa le primitive NetX sottostanti. Questo livello di compatibilità dell'API BSD Sockets deve essere veloce o leggermente più veloce delle tipiche implementazioni di BSD, poiché questo wrapper usa primitive NetX interne e ignora il controllo degli errori NetX di base.

## <a name="bsd-sockets-api-compliancy-wrapper-source"></a>Origine wrapper di compilare l'API BSD Sockets

Il codice sorgente del wrapper BSD è progettato per semplicità ed è costituito solo da due file, *nx_bsd.h* e *nx_bsd.c*. Il file *nx_bsd.h* definisce tutte le costanti e i prototipi di subroutine del wrapper API BSD Sockets necessari, mentre *nx_bsd.c* contiene il codice sorgente effettivo di compatibilità dell'API BSD Sockets. Questi file di origine del wrapper BSD sono comuni a tutti i pacchetti di supporto NetX.

Il pacchetto è costituito da:

- **nx_bsd.c:** codice sorgente wrapper
- **nx_bsd.h:** file di intestazione principale

Programmi demo di esempio:

- **bsd_demo_tcp.c:** demo *con un singolo server TCP e un client*
- **bsd_demo_udp.c:** demo *con due client UDP e un server UDP*
