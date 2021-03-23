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
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-bsd"></a><span data-ttu-id="1c68c-103">Capitolo 1-Introduzione ad Azure RTO NetX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="1c68c-103">Chapter 1 - Introduction to Azure RTOS NetX Duo BSD</span></span>

<span data-ttu-id="1c68c-104">Il wrapper compliancy dell'API socket BSD supporta alcune delle chiamate API socket BSD di base, con alcune limitazioni e usa le primitive di Azure RTO NetX duo sotto.</span><span class="sxs-lookup"><span data-stu-id="1c68c-104">The BSD Socket API Compliancy Wrapper supports some of the basic BSD Socket API calls, with some limitations and utilizes Azure RTOS NetX Duo primitives underneath.</span></span>

## <a name="bsd-socket-api-compliancy-wrapper-source"></a><span data-ttu-id="1c68c-105">Origine wrapper compliancy dell'API socket BSD</span><span class="sxs-lookup"><span data-stu-id="1c68c-105">BSD Socket API Compliancy Wrapper Source</span></span>

<span data-ttu-id="1c68c-106">Il codice sorgente wrapper è progettato per semplicità ed è costituito da due file, vale a dire *nxd_bsd. h* e *nxd_bsd. c*.</span><span class="sxs-lookup"><span data-stu-id="1c68c-106">The Wrapper source code is designed for simplicity and is comprised of two files, namely *nxd_bsd.h* and *nxd_bsd.c*.</span></span> <span data-ttu-id="1c68c-107">Il file *nxd_bsd. h* definisce tutte le costanti wrapper dell'API socket BSD e i prototipi di subroutine, mentre *nxd_bsd. c* contiene il codice sorgente di compatibilità API socket BSD effettivo.</span><span class="sxs-lookup"><span data-stu-id="1c68c-107">The *nxd_bsd.h* file defines all the necessary BSD Socket API wrapper constants and subroutine prototypes, while *nxd_bsd.c* contains the actual BSD Socket API compatibility source code.</span></span> <span data-ttu-id="1c68c-108">Questi file di origine wrapper sono comuni a tutti i pacchetti di supporto di NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="1c68c-108">These Wrapper source files are common to all NetX Duo support packages.</span></span>

<span data-ttu-id="1c68c-109">Il pacchetto è costituito da:</span><span class="sxs-lookup"><span data-stu-id="1c68c-109">The package consists of:</span></span>

- <span data-ttu-id="1c68c-110">**nxd_bsd. c**: codice sorgente wrapper</span><span class="sxs-lookup"><span data-stu-id="1c68c-110">**nxd_bsd.c**: Wrapper source code</span></span>
- <span data-ttu-id="1c68c-111">**nxd_bsd. h**: file di intestazione principale</span><span class="sxs-lookup"><span data-stu-id="1c68c-111">**nxd_bsd.h**: Main header file</span></span>

<span data-ttu-id="1c68c-112">Programmi demo di esempio:</span><span class="sxs-lookup"><span data-stu-id="1c68c-112">Sample demo programs:</span></span>

- <span data-ttu-id="1c68c-113">**bsd_demo_udp. c**: *demo con due peer UDP (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="1c68c-113">**bsd_demo_udp.c**: *Demo with two UDP peers (IPv4 only)*</span></span>
- <span data-ttu-id="1c68c-114">**bsd_demo_tcp. c**: *demo con un singolo server e client TCP*</span><span class="sxs-lookup"><span data-stu-id="1c68c-114">**bsd_demo_tcp.c**: *Demo with a single TCP server and client*</span></span>
- <span data-ttu-id="1c68c-115">**bsd_demo_raw. c**: *demo con due peer non elaborati*</span><span class="sxs-lookup"><span data-stu-id="1c68c-115">**bsd_demo_raw.c**: *Demo with two RAW peers*</span></span>