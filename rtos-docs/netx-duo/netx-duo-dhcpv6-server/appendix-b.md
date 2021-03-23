---
title: Appendice B-codici di stato del server DHCPv6 di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i codici di stato del server DHCPv6 di NetX Duo
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7c79a0c0bc9acfcfca69c7333d30cd7cab35ba5f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821962"
---
# <a name="appendix-b---azure-rtos-netx-duo-dhcpv6-server-status-codes"></a><span data-ttu-id="a9062-103">Appendice B-codici di stato del server DHCPv6 di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a9062-103">Appendix B - Azure RTOS NetX Duo DHCPv6 server status codes</span></span>

| <span data-ttu-id="a9062-104">Nome</span><span class="sxs-lookup"><span data-stu-id="a9062-104">Name</span></span>              | <span data-ttu-id="a9062-105">Codice</span><span class="sxs-lookup"><span data-stu-id="a9062-105">Code</span></span>            | <span data-ttu-id="a9062-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a9062-106">Description</span></span> |
| ------------------- | ------------------- | --------------- |
| <span data-ttu-id="a9062-107">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="a9062-107">Success</span></span> | <span data-ttu-id="a9062-108">0</span><span class="sxs-lookup"><span data-stu-id="a9062-108">0</span></span> | <span data-ttu-id="a9062-109">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="a9062-109">Success</span></span> |
| <span data-ttu-id="a9062-110">Errore non specificato</span><span class="sxs-lookup"><span data-stu-id="a9062-110">Unspecified Failure</span></span> | <span data-ttu-id="a9062-111">1</span><span class="sxs-lookup"><span data-stu-id="a9062-111">1</span></span> | <span data-ttu-id="a9062-112">Errore, motivo non specificato; Questo codice di stato viene impostato dal server per indicare un errore generale durante la concessione della richiesta client non corrispondente agli altri codici</span><span class="sxs-lookup"><span data-stu-id="a9062-112">Failure, reason unspecified; this status code is set by the Server to indicate a general failure in granting the Client request not matching the other codes</span></span> |
| <span data-ttu-id="a9062-113">Noaddress disponibile</span><span class="sxs-lookup"><span data-stu-id="a9062-113">NoAddress Available</span></span> | <span data-ttu-id="a9062-114">2</span><span class="sxs-lookup"><span data-stu-id="a9062-114">2</span></span> | <span data-ttu-id="a9062-115">Il server non dispone di indirizzi disponibili da assegnare al client</span><span class="sxs-lookup"><span data-stu-id="a9062-115">Server has no addresses available to assign to the Client</span></span> |
| <span data-ttu-id="a9062-116">NoBinding</span><span class="sxs-lookup"><span data-stu-id="a9062-116">NoBinding</span></span> | <span data-ttu-id="a9062-117">3</span><span class="sxs-lookup"><span data-stu-id="a9062-117">3</span></span> | <span data-ttu-id="a9062-118">L'indirizzo del client IA (Binding) non è disponibile, ad esempio, l'indirizzo IP richiesto non è disponibile per il server per il lease o l'assegnazione a un altro client.</span><span class="sxs-lookup"><span data-stu-id="a9062-118">Client IA address (binding) is not available e.g. the requested IP address is not available for the Server to lease or assigned to another Client.</span></span> |
| <span data-ttu-id="a9062-119">NotOnLink</span><span class="sxs-lookup"><span data-stu-id="a9062-119">NotOnLink</span></span> | <span data-ttu-id="a9062-120">4</span><span class="sxs-lookup"><span data-stu-id="a9062-120">4</span></span> | <span data-ttu-id="a9062-121">Il prefisso per l'indirizzo indica che l'indirizzo IP non è un indirizzo di collegamento</span><span class="sxs-lookup"><span data-stu-id="a9062-121">The prefix for the address indicates the IP address is not an on link address</span></span> |
| <span data-ttu-id="a9062-122">UseMulticast</span><span class="sxs-lookup"><span data-stu-id="a9062-122">UseMulticast</span></span> | <span data-ttu-id="a9062-123">5</span><span class="sxs-lookup"><span data-stu-id="a9062-123">5</span></span> | <span data-ttu-id="a9062-124">Inviato da un server in risposta alla ricezione di un messaggio client utilizzando l'indirizzo unicast del server anziché l'indirizzo multicast *All_DHCP_Relay_Agents_and_Servers*</span><span class="sxs-lookup"><span data-stu-id="a9062-124">Sent by a Server in response to receiving a Client message using the Server’s unicast address instead of the *All_DHCP_Relay_Agents_and_Servers* multicast address</span></span> |