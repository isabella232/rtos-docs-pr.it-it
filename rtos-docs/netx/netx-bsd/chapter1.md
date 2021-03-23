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
# <a name="chapter-1---introduction-to-azure-rtos-netx-bsd"></a><span data-ttu-id="61228-103">Capitolo 1-Introduzione ad Azure RTO NetX BSD</span><span class="sxs-lookup"><span data-stu-id="61228-103">Chapter 1 - Introduction to Azure RTOS NetX BSD</span></span>

<span data-ttu-id="61228-104">Il wrapper compliancy dell'API NetX BSD Sockets supporta alcune delle chiamate API di base per i socket BSD con alcune limitazioni e usa le primitive NetX sotto.</span><span class="sxs-lookup"><span data-stu-id="61228-104">The NetX BSD Sockets API Compliancy Wrapper supports some of the basic BSD Sockets API calls with some limitations and utilizes NetX primitives underneath.</span></span> <span data-ttu-id="61228-105">Questo livello di compatibilità API dei socket BSD dovrebbe essere eseguito come veloce o leggermente più veloce delle implementazioni BSD tipiche, perché questo wrapper usa le primitive NetX interne e ignora il controllo degli errori NetX di base.</span><span class="sxs-lookup"><span data-stu-id="61228-105">This BSD Sockets API compatibility layer should perform as fast or slightly faster than typical BSD implementations, since this Wrapper utilizes internal NetX primitives and bypasses basic NetX error checking.</span></span>

## <a name="bsd-sockets-api-compliancy-wrapper-source"></a><span data-ttu-id="61228-106">Origine wrapper compliancy API socket BSD</span><span class="sxs-lookup"><span data-stu-id="61228-106">BSD Sockets API Compliancy Wrapper Source</span></span>

<span data-ttu-id="61228-107">Il codice sorgente del wrapper BSD è progettato per semplicità ed è costituito solo da due file, *nx_bsd. h* e *nx_bsd. c*.</span><span class="sxs-lookup"><span data-stu-id="61228-107">The BSD Wrapper source code is designed for simplicity and is comprised of only two files, *nx_bsd.h* and *nx_bsd.c*.</span></span> <span data-ttu-id="61228-108">Il file *nx_bsd. h* definisce tutte le costanti e i prototipi di subroutine del wrapper API per i socket BSD, mentre *nx_bsd. c* contiene il codice sorgente di compatibilità API per i socket BSD effettivi.</span><span class="sxs-lookup"><span data-stu-id="61228-108">The *nx_bsd.h* file defines all the necessary BSD Sockets API Wrapper constants and subroutine prototypes, while *nx_bsd.c* contains the actual BSD Sockets API compatibility source code.</span></span> <span data-ttu-id="61228-109">Questi file di origine del wrapper BSD sono comuni a tutti i pacchetti di supporto NetX.</span><span class="sxs-lookup"><span data-stu-id="61228-109">These BSD Wrapper source files are common to all NetX support packages.</span></span>

<span data-ttu-id="61228-110">Il pacchetto è costituito da:</span><span class="sxs-lookup"><span data-stu-id="61228-110">The package consists of:</span></span>

- <span data-ttu-id="61228-111">**nx_bsd. c**: codice sorgente wrapper</span><span class="sxs-lookup"><span data-stu-id="61228-111">**nx_bsd.c**: Wrapper source code</span></span>
- <span data-ttu-id="61228-112">**nx_bsd. h**: file di intestazione principale</span><span class="sxs-lookup"><span data-stu-id="61228-112">**nx_bsd.h**: Main header file</span></span>

<span data-ttu-id="61228-113">Programmi demo di esempio:</span><span class="sxs-lookup"><span data-stu-id="61228-113">Sample demo programs:</span></span>

- <span data-ttu-id="61228-114">**bsd_demo_tcp. c**: *demo con un singolo server e client TCP*</span><span class="sxs-lookup"><span data-stu-id="61228-114">**bsd_demo_tcp.c**: *Demo with a single TCP server and client*</span></span>
- <span data-ttu-id="61228-115">**bsd_demo_udp. c**: *demo con due client UDP e un server UDP*</span><span class="sxs-lookup"><span data-stu-id="61228-115">**bsd_demo_udp.c**: *Demo with two UDP clients and a UDP server*</span></span>
