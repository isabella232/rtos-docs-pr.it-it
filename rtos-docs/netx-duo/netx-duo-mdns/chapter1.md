---
title: 'Capitolo 1: introduzione ad Azure RTO NetX Duo MDN/DNS-SD'
description: Azure RTO NetX Duo MDN/DNS-SD aumenta il servizio DNS tradizionale.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b46539ee4d502fa4c90fb3392e25cd3bee40dc5b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821830"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mdnsdns-sd"></a><span data-ttu-id="b44d2-103">Capitolo 1: introduzione ad Azure RTO NetX Duo MDN/DNS-SD</span><span class="sxs-lookup"><span data-stu-id="b44d2-103">Chapter 1 - Introduction to Azure RTOS NetX Duo mDNS/DNS-SD</span></span>

<span data-ttu-id="b44d2-104">I messaggi MDN e DNS-SD sono protocolli progettati per potenziare il servizio DNS tradizionale.</span><span class="sxs-lookup"><span data-stu-id="b44d2-104">The mDNS and DNS-SD are protocols designed to augment the traditional DNS service.</span></span> <span data-ttu-id="b44d2-105">MDN fornisce il nome host e il servizio di ricerca ai nodi della rete locale.</span><span class="sxs-lookup"><span data-stu-id="b44d2-105">mDNS provides host name and service lookup to the nodes on the local network.</span></span> <span data-ttu-id="b44d2-106">Ogni nodo utilizza il canale multicast IPv4 o IPv6 per annunciare i servizi che offre ai propri vicini, risponde alle query dagli elementi adiacenti e invia query sul comportamento delle proprie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b44d2-106">Each node uses IPv4 or IPv6 multicast channel to announce services it offers to its neighbors, responds to queries from its neighbors, and sends queries on behave of its applications.</span></span> <span data-ttu-id="b44d2-107">Per impostazione predefinita, i messaggi MDN operano in un ambiente distribuito, eliminando in tal modo una funzione centralizzata.</span><span class="sxs-lookup"><span data-stu-id="b44d2-107">By design, mDNS operates in a distributed environment, thus eliminates a centralized serve.</span></span>

<span data-ttu-id="b44d2-108">DNS-SD si basa su MDN.</span><span class="sxs-lookup"><span data-stu-id="b44d2-108">DNS-SD is built on top of mDNS.</span></span> <span data-ttu-id="b44d2-109">DNS-SD consente ai nodi di annunciare i servizi forniti alla rete locale o di individuare i servizi offerti da altri nodi nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="b44d2-109">DNS-SD allows nodes to announce services they provide to the local network or to discover services offered by other nodes on the local network.</span></span> <span data-ttu-id="b44d2-110">Nel documento il termine *MDN* si riferisce ai servizi che coprono sia la specifica MDN che la specifica DNS-SD.</span><span class="sxs-lookup"><span data-stu-id="b44d2-110">Throughout the document, the term *mDNS* refers to the services that cover both the mDNS specification and the DNS-SD specification.</span></span>

## <a name="mdns-standard"></a><span data-ttu-id="b44d2-111">Standard MDN</span><span class="sxs-lookup"><span data-stu-id="b44d2-111">mDNS Standard</span></span>

<span data-ttu-id="b44d2-112">L'implementazione di NetX Duo MDN/DNS-SD è conforme alle RFC seguenti:</span><span class="sxs-lookup"><span data-stu-id="b44d2-112">NetX Duo mDNS/DNS-SD implementation conforms to the following RFCs:</span></span>

- <span data-ttu-id="b44d2-113">RFC 6762: specifica MDN</span><span class="sxs-lookup"><span data-stu-id="b44d2-113">RFC 6762: mDNS Specification</span></span>
- <span data-ttu-id="b44d2-114">RFC 6763: specifica DNS-SD</span><span class="sxs-lookup"><span data-stu-id="b44d2-114">RFC 6763: DNS-SD Specification</span></span>