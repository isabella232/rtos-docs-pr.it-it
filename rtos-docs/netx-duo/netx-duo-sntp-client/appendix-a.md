---
title: Appendice A - Azure RTOS di errore irreversibile di NetX Duo SNTP
description: I codici di errore seguenti causano l Azure RTOS client NetX Duo SNTP che interrompe gli aggiornamenti dell'ora con il server corrente.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e0152c1342b3edffd42f7442c51e7c5d62b199a5b38085dac06b4c0dbee9e9a8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790106"
---
# <a name="appendix-a---azure-rtos-netx-duo-sntp-fatal-error-codes"></a>Appendice A - Azure RTOS di errore irreversibile di NetX Duo SNTP

I codici di errore seguenti causano l Azure RTOS client NetX Duo SNTP che interrompe gli aggiornamenti dell'ora con il server corrente. È l'applicazione a decidere se il server deve essere rimosso dall'elenco di server disponibili del client SNTP o semplicemente passare al successivo server disponibile nell'elenco. La definizione di ogni stato di errore è definita in *nxd_sntp_client.h. *

Quando il client SNTP restituisce un errore dall'elenco seguente all'applicazione, è probabile che il server debba essere sostituito con un altro server. Si noti che NX_SNTP_KOD_REMOVE_SERVER stato di errore viene lasciato al gestore di decesso del client SNTP (funzione di callback) da impostare:

- NX_SNTP_KOD_REMOVE_SERVER 0xD0C  
- NX_SNTP_SERVER_AUTH_FAIL 0xD0D  
- NX_SNTP_INVALID_NTP_VERSION 0xD11  
- NX_SNTP_INVALID_SERVER_MODE 0xD12  
- NX_SNTP_INVALID_SERVER_STRATUM 0xD15  

Quando il client SNTP restituisce un errore dall'elenco seguente all'applicazione, il server potrebbe non essere temporaneamente in grado di fornire aggiornamenti di ora validi e non deve essere rimosso:

- HNX_SNTP_NO_UNICAST_FROM_SERVER 0xD09  
- NX_SNTP_SERVER_CLOCK_NOT_SYNC 0xD0A  
- NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD0B  
- NX_SNTP_OVER_BAD_UPDATE_LIMIT 0xD17  
- NX_SNTP_BAD_SERVER_ROOT_DISPERSION 0xD16  
- NX_SNTP_INVALID_RTT_TIME 0xD21  
- NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD24