---
title: Appendice A-codici di errore irreversibili di Azure RTO NetX Duo SNTP
description: I codici di errore seguenti comporteranno l'interruzione degli aggiornamenti temporali del client di Azure RTO NetX Duo SNTP con il server corrente.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 065e7a3e65b3cf8d7fcfb34bb9568a673791609a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821665"
---
# <a name="appendix-a---azure-rtos-netx-duo-sntp-fatal-error-codes"></a>Appendice A-codici di errore irreversibili di Azure RTO NetX Duo SNTP

I codici di errore seguenti comporteranno l'interruzione degli aggiornamenti temporali del client di Azure RTO NetX Duo SNTP con il server corrente. Spetta all'applicazione decidere se il server deve essere rimosso dall'elenco client di SNTP dei server disponibili o semplicemente passare al server successivo disponibile nell'elenco. La definizione di ogni stato di errore è definita in * nxd_sntp_client. h. *

Quando il client SNTP restituisce un errore dall'elenco seguente all'applicazione, è probabile che il server venga sostituito con un altro server. Si noti che lo stato di errore NX_SNTP_KOD_REMOVE_SERVER viene lasciato al SNTP client Kiss of Death handler (funzione di callback) per impostare:

- NX_SNTP_KOD_REMOVE_SERVER 0xD0C  
- NX_SNTP_SERVER_AUTH_FAIL 0xD0D  
- NX_SNTP_INVALID_NTP_VERSION 0xD11  
- NX_SNTP_INVALID_SERVER_MODE 0xD12  
- NX_SNTP_INVALID_SERVER_STRATUM 0xD15  

Quando il client SNTP restituisce un errore dall'elenco seguente all'applicazione, il server può solo temporaneamente non essere in grado di fornire aggiornamenti temporali validi e non deve essere rimosso:

- HNX_SNTP_NO_UNICAST_FROM_SERVER 0xD09  
- NX_SNTP_SERVER_CLOCK_NOT_SYNC 0xD0A  
- NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD0B  
- NX_SNTP_OVER_BAD_UPDATE_LIMIT 0xD17  
- NX_SNTP_BAD_SERVER_ROOT_DISPERSION 0xD16  
- NX_SNTP_INVALID_RTT_TIME 0xD21  
- NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD24