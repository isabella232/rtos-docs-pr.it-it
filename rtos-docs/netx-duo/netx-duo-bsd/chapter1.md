---
title: Capitolo 1 - Introduzione a Azure RTOS NetX Duo BSD
description: BSD Socket API Compliancy Wrapper supporta alcune delle chiamate API socket BSD di base, con alcune limitazioni e usa Azure RTOS primitive NetX Duo sottostanti.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: caf8d5374204bc553ac903f4720d3db402d9a10da5c26caa0fa67c4b5d340049
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790497"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-bsd"></a>Capitolo 1 - Introduzione a Azure RTOS NetX Duo BSD

BSD Socket API Compliancy Wrapper supporta alcune delle chiamate API socket BSD di base, con alcune limitazioni e usa Azure RTOS primitive NetX Duo sottostanti.

## <a name="bsd-socket-api-compliancy-wrapper-source"></a>Origine wrapper di compilare l'API socket BSD

Il codice sorgente wrapper è progettato per semplicità ed è costituito da due file, *nxd_bsd.h* *e nxd_bsd.c*. Il file *nxd_bsd.h* definisce tutte le costanti wrapper dell'API socket BSD necessarie e i prototipi di subroutine, mentre *nxd_bsd.c* contiene il codice sorgente effettivo di compatibilità dell'API socket BSD. Questi file di origine wrapper sono comuni a tutti i pacchetti di supporto di NetX Duo.

Il pacchetto è costituito da:

- **nxd_bsd.c**: Codice sorgente wrapper
- **nxd_bsd.h:** file di intestazione principale

Programmi demo di esempio:

- **bsd_demo_udp.c:** demo *con due peer UDP (solo IPv4)*
- **bsd_demo_tcp.c:** demo *con un singolo server TCP e un client*
- **bsd_demo_raw.c:** demo *con due peer RAW*