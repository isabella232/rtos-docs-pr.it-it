---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo BSD
description: Il wrapper compliancy dell'API socket BSD supporta alcune delle chiamate API socket BSD di base, con alcune limitazioni e usa le primitive di Azure RTO NetX duo sotto.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e89018dffd2f9f9065efab2ecabdf4364c4f89a3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822064"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-bsd"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo BSD

Il wrapper compliancy dell'API socket BSD supporta alcune delle chiamate API socket BSD di base, con alcune limitazioni e usa le primitive di Azure RTO NetX duo sotto.

## <a name="bsd-socket-api-compliancy-wrapper-source"></a>Origine wrapper compliancy dell'API socket BSD

Il codice sorgente wrapper è progettato per semplicità ed è costituito da due file, vale a dire *nxd_bsd. h* e *nxd_bsd. c*. Il file *nxd_bsd. h* definisce tutte le costanti wrapper dell'API socket BSD e i prototipi di subroutine, mentre *nxd_bsd. c* contiene il codice sorgente di compatibilità API socket BSD effettivo. Questi file di origine wrapper sono comuni a tutti i pacchetti di supporto di NetX Duo.

Il pacchetto è costituito da:

- **nxd_bsd. c**: codice sorgente wrapper
- **nxd_bsd. h**: file di intestazione principale

Programmi demo di esempio:

- **bsd_demo_udp. c**: *demo con due peer UDP (solo IPv4)*
- **bsd_demo_tcp. c**: *demo con un singolo server e client TCP*
- **bsd_demo_raw. c**: *demo con due peer non elaborati*