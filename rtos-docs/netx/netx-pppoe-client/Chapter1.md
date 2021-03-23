---
title: Capitolo 1-Introduzione ad Azure RTO NetX client PPPoE
description: Questo capitolo contiene i dettagli del modulo PPPoE di Azure RTO NetX.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bbf1e064bb38754bd67b279a0fd60d46d3d6d557
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822547"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pppoe-client"></a><span data-ttu-id="928c0-103">Capitolo 1-Introduzione ad Azure RTO NetX client PPPoE</span><span class="sxs-lookup"><span data-stu-id="928c0-103">Chapter 1 - Introduction to Azure RTOS NetX PPPoE Client</span></span>

<span data-ttu-id="928c0-104">PPP over Ethernet (PPPoE) consente agli host di connettersi al server PPP tramite Ethernet invece della tradizionale comunicazione della linea seriale basata su caratteri.</span><span class="sxs-lookup"><span data-stu-id="928c0-104">PPP over Ethernet (PPPoE) allows hosts to connect to PPP server via Ethernet instead of the traditional character-based serial line communication.</span></span>  <span data-ttu-id="928c0-105">I dettagli tecnici di PPPoE sono descritti in RFC 2516: un metodo per la trasmissione di PPP over Ethernet (PPPoE).</span><span class="sxs-lookup"><span data-stu-id="928c0-105">The technical details of PPPoE are described in RFC 2516:  A Method for Transmitting PPP over Ethernet (PPPoE).</span></span> <span data-ttu-id="928c0-106">Questo documento è incentrato sui dettagli del modulo PPPoE NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="928c0-106">This document focuses on the details of  Azure RTOS NetX PPPoE module.</span></span>

<span data-ttu-id="928c0-107">Per fornire una connessione Point-to-Point su Ethernet, ogni sessione PPP deve apprendere l'indirizzo Ethernet del peer remoto, nonché stabilire un identificatore di sessione univoco.</span><span class="sxs-lookup"><span data-stu-id="928c0-107">To provide a point-to-point connection over Ethernet, each PPP session must learn the Ethernet address of the remote peer, as well as establish a unique session identifier.</span></span>

<span data-ttu-id="928c0-108">In base allo standard RFC 2516, PPPoE è costituito da due fasi: la fase di individuazione e la fase della sessione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="928c0-108">According to RFC 2516, PPPoE consists of two stages: the Discovery stage, and PPPoE Session stage.</span></span> <span data-ttu-id="928c0-109">Quando un host (client) desidera avviare una sessione PPP, deve prima eseguire l'individuazione per trovare il server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="928c0-109">When a host (client) wishes to start a PPP session, it must first perform Discovery to find PPPoE server.</span></span> <span data-ttu-id="928c0-110">Questo passaggio consente inoltre al server e al client di identificare gli indirizzi MAC Ethernet e SESSION_ID, che verranno usati per il resto della sessione PPP.</span><span class="sxs-lookup"><span data-stu-id="928c0-110">This step also allows the server and the client to identify each other’s Ethernet MAC address and SESSION_ID, which will be used for the rest of the PPP session.</span></span>

<span data-ttu-id="928c0-111">Un frame Ethernet è il seguente:</span><span class="sxs-lookup"><span data-stu-id="928c0-111">An Ethernet frame is as follows:</span></span>

![Frame Ethernet](media/ethernet-frame.png)

<span data-ttu-id="928c0-113">Il payload Ethernet per PPPoE è il seguente:</span><span class="sxs-lookup"><span data-stu-id="928c0-113">The Ethernet payload for PPPoE is as follows:</span></span>

![Payload Ethernet](media/ethernet-payload.png)

## <a name="pppoe-discovery-stage"></a><span data-ttu-id="928c0-115">Fase di individuazione PPPoE</span><span class="sxs-lookup"><span data-stu-id="928c0-115">PPPoE Discovery Stage</span></span>

<span data-ttu-id="928c0-116">La fase di individuazione PPPoE consente ai client di selezionare un server da tutti i server disponibili sulla rete, in modo da creare una sessione prima di scambiare i frame PPP.</span><span class="sxs-lookup"><span data-stu-id="928c0-116">The PPPoE Discovery stage allows clients to select a server from all available servers on the network, effectively to create a session prior to PPP frames being exchanged.</span></span>  <span data-ttu-id="928c0-117">Al termine della fase di individuazione, sia il client che il server devono accettare un ID di sessione univoco ed entrambi i lati devono essere a conoscenza dell'indirizzo MAC del peer.</span><span class="sxs-lookup"><span data-stu-id="928c0-117">At the end of the discovery stage, both the client and the server shall agree on a unique session ID, and both sides need to know peer’s MAC address.</span></span>

| <span data-ttu-id="928c0-118">Messaggio di individuazione</span><span class="sxs-lookup"><span data-stu-id="928c0-118">Discovery Message</span></span> | <span data-ttu-id="928c0-119">Codice</span><span class="sxs-lookup"><span data-stu-id="928c0-119">Code</span></span> | <span data-ttu-id="928c0-120">Direzione</span><span class="sxs-lookup"><span data-stu-id="928c0-120">Direction</span></span> |
| ----------------- | ---- | --------- |
| <span data-ttu-id="928c0-121">Avvio di individuazione attiva PPPoE (PADI)</span><span class="sxs-lookup"><span data-stu-id="928c0-121">PPPoE Active Discovery Initiation (PADI)</span></span> | <span data-ttu-id="928c0-122">0x09</span><span class="sxs-lookup"><span data-stu-id="928c0-122">0x09</span></span> | <span data-ttu-id="928c0-123">Da client a broadcast</span><span class="sxs-lookup"><span data-stu-id="928c0-123">From Client to broadcast</span></span> |
| <span data-ttu-id="928c0-124">Offerta di individuazione attiva PPPoE (PADO)</span><span class="sxs-lookup"><span data-stu-id="928c0-124">PPPoE Active Discovery Offer (PADO)</span></span> | <span data-ttu-id="928c0-125">0x07</span><span class="sxs-lookup"><span data-stu-id="928c0-125">0x07</span></span> | <span data-ttu-id="928c0-126">Da server a client</span><span class="sxs-lookup"><span data-stu-id="928c0-126">From Server to Client</span></span> |
| <span data-ttu-id="928c0-127">Richiesta di individuazione attiva PPPoE (PADR)</span><span class="sxs-lookup"><span data-stu-id="928c0-127">PPPoE Active Discovery Request (PADR)</span></span> | <span data-ttu-id="928c0-128">0x19</span><span class="sxs-lookup"><span data-stu-id="928c0-128">0x19</span></span> | <span data-ttu-id="928c0-129">Da client a server</span><span class="sxs-lookup"><span data-stu-id="928c0-129">From Client to Server</span></span> |
| <span data-ttu-id="928c0-130">Sessione di individuazione attiva PPPOE-conferma (rilievi)</span><span class="sxs-lookup"><span data-stu-id="928c0-130">PPPOE Active Discovery Session-confirmation (PADS)</span></span> | <span data-ttu-id="928c0-131">0x65</span><span class="sxs-lookup"><span data-stu-id="928c0-131">0x65</span></span> | <span data-ttu-id="928c0-132">Da server a client</span><span class="sxs-lookup"><span data-stu-id="928c0-132">From Server to Client</span></span> |
| <span data-ttu-id="928c0-133">Termina individuazione attiva PPPoE (PADT)</span><span class="sxs-lookup"><span data-stu-id="928c0-133">PPPoE Active Discovery Terminate (PADT)</span></span> | <span data-ttu-id="928c0-134">0xa7</span><span class="sxs-lookup"><span data-stu-id="928c0-134">0xa7</span></span> | <span data-ttu-id="928c0-135">Può essere avviato dal server o dal client</span><span class="sxs-lookup"><span data-stu-id="928c0-135">Can be initiated from either server or client</span></span> |

<span data-ttu-id="928c0-136">Tutti i frame Ethernet di individuazione hanno il campo ETHER_TYPE impostato sul valore 0x8863.</span><span class="sxs-lookup"><span data-stu-id="928c0-136">All Discovery Ethernet frames have the ETHER_TYPE field set to the value 0x8863.</span></span>

## <a name="pppoe-session-message"></a><span data-ttu-id="928c0-137">Messaggio di sessione PPPoE</span><span class="sxs-lookup"><span data-stu-id="928c0-137">PPPoE Session Message</span></span>

<span data-ttu-id="928c0-138">Dopo che il client e il server hanno creato una sessione, i frame PPP possono essere trasferiti come messaggi di sessione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="928c0-138">After the client and the server create a session, PPP frames can be transferred as PPPoE Session messages.</span></span>  <span data-ttu-id="928c0-139">Durante una sessione, il SESSION_ID non deve cambiare e deve essere il valore assegnato dal server durante la fase di individuazione.</span><span class="sxs-lookup"><span data-stu-id="928c0-139">During a session, the SESSION_ID must not change and must be the value the server assigned during the Discovery stage.</span></span>

<span data-ttu-id="928c0-140">Tutti i frame Ethernet della sessione PPPoE hanno il campo ETHER_TYPE impostato sul valore 0x8864.</span><span class="sxs-lookup"><span data-stu-id="928c0-140">All PPPoE Session Ethernet frames have the ETHER_TYPE field set to the value 0x8864.</span></span>
