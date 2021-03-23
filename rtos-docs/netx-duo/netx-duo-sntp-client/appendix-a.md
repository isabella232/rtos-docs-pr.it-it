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
# <a name="appendix-a---azure-rtos-netx-duo-sntp-fatal-error-codes"></a><span data-ttu-id="01ede-103">Appendice A-codici di errore irreversibili di Azure RTO NetX Duo SNTP</span><span class="sxs-lookup"><span data-stu-id="01ede-103">Appendix A - Azure RTOS NetX Duo SNTP Fatal Error Codes</span></span>

<span data-ttu-id="01ede-104">I codici di errore seguenti comporteranno l'interruzione degli aggiornamenti temporali del client di Azure RTO NetX Duo SNTP con il server corrente.</span><span class="sxs-lookup"><span data-stu-id="01ede-104">The following error codes will result in the Azure RTOS NetX Duo SNTP Client aborting time updates with the current server.</span></span> <span data-ttu-id="01ede-105">Spetta all'applicazione decidere se il server deve essere rimosso dall'elenco client di SNTP dei server disponibili o semplicemente passare al server successivo disponibile nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="01ede-105">It is up to the application to decide if the server should be removed from the SNTP Client list of available servers, or simply switch to the next available server on the list.</span></span> <span data-ttu-id="01ede-106">La definizione di ogni stato di errore è definita in \* nxd_sntp_client. h.</span><span class="sxs-lookup"><span data-stu-id="01ede-106">The definition of each error status is defined in \*nxd_sntp_client.h.</span></span> *

<span data-ttu-id="01ede-107">Quando il client SNTP restituisce un errore dall'elenco seguente all'applicazione, è probabile che il server venga sostituito con un altro server.</span><span class="sxs-lookup"><span data-stu-id="01ede-107">When the SNTP Client returns an error from the list below to the application, the Server should probably be replaced with another Server.</span></span> <span data-ttu-id="01ede-108">Si noti che lo stato di errore NX_SNTP_KOD_REMOVE_SERVER viene lasciato al SNTP client Kiss of Death handler (funzione di callback) per impostare:</span><span class="sxs-lookup"><span data-stu-id="01ede-108">Note that the NX_SNTP_KOD_REMOVE_SERVER error status is left to the SNTP Client kiss of death handler (callback function) to set:</span></span>

- <span data-ttu-id="01ede-109">NX_SNTP_KOD_REMOVE_SERVER 0xD0C</span><span class="sxs-lookup"><span data-stu-id="01ede-109">NX_SNTP_KOD_REMOVE_SERVER 0xD0C</span></span>  
- <span data-ttu-id="01ede-110">NX_SNTP_SERVER_AUTH_FAIL 0xD0D</span><span class="sxs-lookup"><span data-stu-id="01ede-110">NX_SNTP_SERVER_AUTH_FAIL 0xD0D</span></span>  
- <span data-ttu-id="01ede-111">NX_SNTP_INVALID_NTP_VERSION 0xD11</span><span class="sxs-lookup"><span data-stu-id="01ede-111">NX_SNTP_INVALID_NTP_VERSION 0xD11</span></span>  
- <span data-ttu-id="01ede-112">NX_SNTP_INVALID_SERVER_MODE 0xD12</span><span class="sxs-lookup"><span data-stu-id="01ede-112">NX_SNTP_INVALID_SERVER_MODE 0xD12</span></span>  
- <span data-ttu-id="01ede-113">NX_SNTP_INVALID_SERVER_STRATUM 0xD15</span><span class="sxs-lookup"><span data-stu-id="01ede-113">NX_SNTP_INVALID_SERVER_STRATUM 0xD15</span></span>  

<span data-ttu-id="01ede-114">Quando il client SNTP restituisce un errore dall'elenco seguente all'applicazione, il server può solo temporaneamente non essere in grado di fornire aggiornamenti temporali validi e non deve essere rimosso:</span><span class="sxs-lookup"><span data-stu-id="01ede-114">When the SNTP Client returns an error from the list below to the application, the Server may only temporarily be unable to provide valid time updates and need not be removed:</span></span>

- <span data-ttu-id="01ede-115">HNX_SNTP_NO_UNICAST_FROM_SERVER 0xD09</span><span class="sxs-lookup"><span data-stu-id="01ede-115">HNX_SNTP_NO_UNICAST_FROM_SERVER 0xD09</span></span>  
- <span data-ttu-id="01ede-116">NX_SNTP_SERVER_CLOCK_NOT_SYNC 0xD0A</span><span class="sxs-lookup"><span data-stu-id="01ede-116">NX_SNTP_SERVER_CLOCK_NOT_SYNC 0xD0A</span></span>  
- <span data-ttu-id="01ede-117">NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD0B</span><span class="sxs-lookup"><span data-stu-id="01ede-117">NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD0B</span></span>  
- <span data-ttu-id="01ede-118">NX_SNTP_OVER_BAD_UPDATE_LIMIT 0xD17</span><span class="sxs-lookup"><span data-stu-id="01ede-118">NX_SNTP_OVER_BAD_UPDATE_LIMIT 0xD17</span></span>  
- <span data-ttu-id="01ede-119">NX_SNTP_BAD_SERVER_ROOT_DISPERSION 0xD16</span><span class="sxs-lookup"><span data-stu-id="01ede-119">NX_SNTP_BAD_SERVER_ROOT_DISPERSION 0xD16</span></span>  
- <span data-ttu-id="01ede-120">NX_SNTP_INVALID_RTT_TIME 0xD21</span><span class="sxs-lookup"><span data-stu-id="01ede-120">NX_SNTP_INVALID_RTT_TIME 0xD21</span></span>  
- <span data-ttu-id="01ede-121">NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD24</span><span class="sxs-lookup"><span data-stu-id="01ede-121">NX_SNTP_KOD_SERVER_NOT_AVAILABLE 0xD24</span></span>