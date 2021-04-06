---
title: Capitolo 2-installazione del supporto ThreadX per ARMv8-M
description: Questo capitolo illustra come installare e usare il codice sorgente ThreadX per l'architettura ARMv8-M.
author: v-condav
ms.author: v-condav
ms.date: 03/04/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 303b83bcc92797314b764353b770965c0170fb99
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377592"
---
#  <a name="chapter-2--installing-threadx-support-for-armv8-m"></a><span data-ttu-id="1bcd6-103">Capitolo 2 installazione del supporto ThreadX per ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="1bcd6-103">Chapter 2  Installing ThreadX support for ARMv8-M</span></span>

<span data-ttu-id="1bcd6-104">Sono disponibili file di codice sorgente ThreadX aggiuntivi per supportare l'architettura ARMv8-M.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-104">There are additional ThreadX source code files to support the ARMv8-M architecture.</span></span>

<span data-ttu-id="1bcd6-105">Se ThreadX deve essere eseguito in modalità protetta, questi file e API aggiuntivi non sono necessari.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-105">If ThreadX is to be run in secure mode, these additional files and APIs are not needed.</span></span> <span data-ttu-id="1bcd6-106">Per eseguire ThreadX in modalità protetta, definire il simbolo **TX_SECURE_EXECUTION** nella parte superiore di **_tx_port. h_*_ o nella riga di comando o nelle impostazioni del progetto. Assicurarsi che _\* TX_SECURE_EXECUTION*\* sia definito per tutti i file c e assembly.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-106">To run ThreadX in secure mode, define the symbol **TX_SECURE_EXECUTION** at the top of **_tx_port.h_*_ or on the command line or project settings. Ensure _\* TX_SECURE_EXECUTION*\* is defined for all c and assembly files.</span></span> <span data-ttu-id="1bcd6-107">ThreadX e l'applicazione utente vengono eseguiti in modalità protetta.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-107">ThreadX and the user application will execute in secure mode.</span></span>

<span data-ttu-id="1bcd6-108">Per eseguire ThreadX e l'applicazione utente in modalità non protetta e supportare funzioni sicure richiamabili non sicure, effettuare le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-108">To run ThreadX and the user application in non-secure mode and support non-secure callable secure functions, please do the following.</span></span>

<span data-ttu-id="1bcd6-109">Il file ***tx_thread_secure_stack. c*** deve essere aggiunto all'applicazione protetta.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-109">The file ***tx_thread_secure_stack.c*** must be added to the secure application.</span></span>

<span data-ttu-id="1bcd6-110">I file seguenti devono essere aggiunti alla libreria ThreadX.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-110">The following files must be added to the ThreadX library.</span></span>

- <span data-ttu-id="1bcd6-111">***tx_secure_interface. h***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-111">***tx_secure_interface.h***</span></span>
- <span data-ttu-id="1bcd6-112">***txe_thread_secure_stack_allocate. c***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-112">***txe_thread_secure_stack_allocate.c***</span></span>
- <span data-ttu-id="1bcd6-113">***txe_thread_secure_stack_free. c***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-113">***txe_thread_secure_stack_free.c***</span></span>
- <span data-ttu-id="1bcd6-114">***tx_thread_secure_stack_allocate. s***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-114">***tx_thread_secure_stack_allocate.s***</span></span>
- <span data-ttu-id="1bcd6-115">***tx_thread_secure_stack_free. s***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-115">***tx_thread_secure_stack_free.s***</span></span>

<span data-ttu-id="1bcd6-116">I due file seguenti sostituiscono i file generici nella libreria ThreadX.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-116">The following two files replace the generic files in the ThreadX library.</span></span>

- <span data-ttu-id="1bcd6-117">***tx_thread_stack_error_handler. c***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-117">***tx_thread_stack_error_handler.c***</span></span>
- <span data-ttu-id="1bcd6-118">***tx_thread_stack_error_notify. c***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-118">***tx_thread_stack_error_notify.c***</span></span>

## <a name="additional-threadx-sources-for-armv8-m"></a><span data-ttu-id="1bcd6-119">Origini ThreadX aggiuntive per ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="1bcd6-119">Additional ThreadX Sources for ARMv8-M</span></span>

<span data-ttu-id="1bcd6-120">I file ThreadX aggiuntivi per l'architettura ARMv8-M TrustZone sono descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-120">The additional ThreadX files for the ARMv8-M TrustZone architecture are described below.</span></span>

  | <span data-ttu-id="1bcd6-121">**Nome file**</span><span class="sxs-lookup"><span data-stu-id="1bcd6-121">**File Name**</span></span>                            | <span data-ttu-id="1bcd6-122">**Contents**</span><span class="sxs-lookup"><span data-stu-id="1bcd6-122">**Contents**</span></span>                                                        |
  |------------------------------------------|---------------------------------------------------------------------|
  | <span data-ttu-id="1bcd6-123">***tx_secure_interface. h***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-123">***tx_secure_interface.h***</span></span>              | <span data-ttu-id="1bcd6-124">File di inclusione che definisce le funzioni chiamabili non sicure di ThreadX.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-124">Include file that defines the ThreadX non-secure callable functions.</span></span> |
  | <span data-ttu-id="1bcd6-125">***txe_thread_secure_stack_allocate. c***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-125">***txe_thread_secure_stack_allocate.c***</span></span> |  <span data-ttu-id="1bcd6-126">Errore durante il controllo del file per l'API di allocazione dello stack protetto.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-126">Error-checking file for the secure stack allocate API.</span></span> |
  | <span data-ttu-id="1bcd6-127">***txe_thread_secure_stack_free. c***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-127">***txe_thread_secure_stack_free.c***</span></span>     |  <span data-ttu-id="1bcd6-128">Errore durante il controllo del file per l'API gratuita dello stack protetto.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-128">Error-checking file for the secure stack free API.</span></span> |
  | <span data-ttu-id="1bcd6-129">***tx_thread_secure_stack_allocate. s***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-129">***tx_thread_secure_stack_allocate.s***</span></span>  |  <span data-ttu-id="1bcd6-130">Impiallacciatura non protetta per il servizio Secure stack allocate.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-130">Non-secure veneer for the secure stack allocate service.</span></span> |
  | <span data-ttu-id="1bcd6-131">***tx_thread_secure_stack_free. s***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-131">***tx_thread_secure_stack_free.s***</span></span>      |  <span data-ttu-id="1bcd6-132">Impiallacciatura non sicura per il servizio Secure stack free.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-132">Non-secure veneer for the secure stack free service.</span></span> |
  | <span data-ttu-id="1bcd6-133">***tx_thread_stack_error_handler. c***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-133">***tx_thread_stack_error_handler.c***</span></span>    |  <span data-ttu-id="1bcd6-134">Gestore per gli errori dello stack di thread.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-134">Handler for thread stack errors.</span></span> |
  | <span data-ttu-id="1bcd6-135">***tx_thread_stack_error_notify. c***</span><span class="sxs-lookup"><span data-stu-id="1bcd6-135">***tx_thread_stack_error_notify.c***</span></span>     |  <span data-ttu-id="1bcd6-136">Registra il callback di notifica per la gestione degli errori dello stack dei thread.</span><span class="sxs-lookup"><span data-stu-id="1bcd6-136">Register notification callback for handling thread stack errors.</span></span> |
