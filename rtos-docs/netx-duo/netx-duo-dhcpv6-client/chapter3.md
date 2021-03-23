---
title: Capitolo 3-opzioni di configurazione DHCPv6 di Azure RTO NetX Duo
description: Sono disponibili diverse opzioni di configurazione per la compilazione di Azure RTO NetX Duo DHCPv6.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e5396b1c04581b5f79d337462368c4718ba9bb16
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821992"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-configuration-options"></a><span data-ttu-id="5e5a9-103">Capitolo 3-opzioni di configurazione DHCPv6 di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="5e5a9-103">Chapter 3 - Azure RTOS NetX Duo DHCPv6 configuration options</span></span>

<span data-ttu-id="5e5a9-104">Sono disponibili diverse opzioni di configurazione per la compilazione di Azure RTO NetX Duo DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-104">There are several configuration options for building Azure RTOS NetX Duo DHCPv6.</span></span> <span data-ttu-id="5e5a9-105">L'elenco seguente descrive tutti i dettagli:</span><span class="sxs-lookup"><span data-stu-id="5e5a9-105">The following list describes each in detail:</span></span>  
  
  
- <span data-ttu-id="5e5a9-106">**NX_DHCPV6_THREAD_PRIORITY** Priorità del thread del client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-106">**NX_DHCPV6_THREAD_PRIORITY** Priority of the Client thread.</span></span> <span data-ttu-id="5e5a9-107">Per impostazione predefinita, questo valore specifica che il thread client viene eseguito con priorità 2.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-107">By   default, this value specifies that   the Client thread runs at priority   2.</span></span>

- <span data-ttu-id="5e5a9-108">**NX_DHCPV6_MUTEX_WAIT** Opzione di timeout per ottenere un blocco esclusivo su un mutex client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-108">**NX_DHCPV6_MUTEX_WAIT** Time out option for obtaining an exclusive lock on a DHCPv6 Client mutex.</span></span> <span data-ttu-id="5e5a9-109">Il valore predefinito è TX_WAIT_FOREVER.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-109">The default value is TX_WAIT_FOREVER.</span></span>

- <span data-ttu-id="5e5a9-110">**NX_DHCPV6_TICKS_PER_SECOND** Rapporto tra i cicli e i secondi.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-110">**NX_DHCPV6_TICKS_PER_SECOND** Ratio of ticks to seconds.</span></span> <span data-ttu-id="5e5a9-111">Si tratta di un dipendente dal processore.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-111">This is processor dependent.</span></span> <span data-ttu-id="5e5a9-112">Il valore predefinito è 100.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-112">The default value is 100.</span></span>

- <span data-ttu-id="5e5a9-113">**NX_DHCPV6_IP_LIFETIME_TIMER_INTERVAL**  Intervallo di tempo in secondi durante il quale il timer di durata IP aggiorna il periodo di tempo in cui l'indirizzo IP corrente è stato assegnato al client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-113">**NX_DHCPV6_IP_LIFETIME_TIMER_INTERVAL**  Time interval in seconds at which the IP lifetime timer updates the length of time the current IP address has been assigned to the Client.</span></span> <span data-ttu-id="5e5a9-114">Per impostazione predefinita, questo valore è 1.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-114">By default, this value is 1.</span></span>

- <span data-ttu-id="5e5a9-115">**NX_DHCPV6_SESSION_TIMER_INTERVAL**  Intervallo di tempo in secondi durante il quale il timer della sessione aggiorna il periodo di tempo in cui il client è stato in una sessione di comunicazione con il server.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-115">**NX_DHCPV6_SESSION_TIMER_INTERVAL**  Time interval in seconds at which the session timer updates the length of time the Client has been in session communicating with the Server.</span></span> <span data-ttu-id="5e5a9-116">Per impostazione predefinita, questo valore è 1.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-116">By default, this value is 1.</span></span>

- <span data-ttu-id="5e5a9-117">**NX_DHCPV6_MAX_IA_ADDRESS** Numero massimo di indirizzi IA che è possibile aggiungere al record client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-117">**NX_DHCPV6_MAX_IA_ADDRESS** The maximum number of IA addresses that can be added to the Client record.</span></span> <span data-ttu-id="5e5a9-118">Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-118">The default value is 1.</span></span> 

- <span data-ttu-id="5e5a9-119">**NX_DHCPV6_NUM_DNS_SERVERS** Numero di server DNS da archiviare nel record client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-119">**NX_DHCPV6_NUM_DNS_SERVERS** Number of DNS servers to store to the client record.</span></span> <span data-ttu-id="5e5a9-120">Il valore predefinito è 2.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-120">The default value is 2.</span></span>

- <span data-ttu-id="5e5a9-121">**NX_DHCPV6_NUM_TIME_SERVERS** Numero di server di tempo da archiviare nel record client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-121">**NX_DHCPV6_NUM_TIME_SERVERS** Number of time servers to store to the client record.</span></span> <span data-ttu-id="5e5a9-122">Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-122">The default value is 1.</span></span>

- <span data-ttu-id="5e5a9-123">**NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE**  Dimensioni del buffer nel record client in cui memorizzare il nome di dominio di rete del client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-123">**NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE**  Size of the buffer in the Client record to hold the client’s network domain name.</span></span> <span data-ttu-id="5e5a9-124">Il valore predefinito è 30.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-124">The default value is 30.</span></span>

- <span data-ttu-id="5e5a9-125">**NX_DHCPV6_TIME_ZONE_BUFFER_SIZE**  Dimensioni del buffer nel record client per il mantenimento del fuso orario del client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-125">**NX_DHCPV6_TIME_ZONE_BUFFER_SIZE**  Size of the buffer in the Client record to hold the Client’s time zone.</span></span> <span data-ttu-id="5e5a9-126">Il valore predefinito è 10.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-126">The default value is 10.</span></span>

- <span data-ttu-id="5e5a9-127">**NX_DHCPV6_MAX_MESSAGE_SIZE** Dimensioni del buffer nel record client per memorizzare il messaggio di stato dell'opzione in una risposta del server.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-127">**NX_DHCPV6_MAX_MESSAGE_SIZE** Size of the buffer in the Client record to hold the option status message in a Server reply.</span></span> <span data-ttu-id="5e5a9-128">Il valore predefinito è 100 byte.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-128">The default value is 100 bytes.</span></span>

- <span data-ttu-id="5e5a9-129">**NX_DHCPV6_PACKET_TIME_OUT** Timeout in secondi per l'allocazione di un pacchetto dal pool di pacchetti client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-129">**NX_DHCPV6_PACKET_TIME_OUT** Time out in seconds for allocating a packet from the Client packet pool.</span></span> <span data-ttu-id="5e5a9-130">Il valore predefinito è 3 secondi.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-130">The default value is 3 seconds.</span></span>

- <span data-ttu-id="5e5a9-131">**NX_DHCPV6_TYPE_OF_SERVICE** Definisce il tipo di servizio per la trasmissione di pacchetti UDP dal socket client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-131">**NX_DHCPV6_TYPE_OF_SERVICE** This defines the type of service for UDP packet transmission from the DHCPv6 Client socket.</span></span> <span data-ttu-id="5e5a9-132">Il valore predefinito è **NX_IP_NORMAL**.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-132">The default value is **NX_IP_NORMAL**.</span></span>

- <span data-ttu-id="5e5a9-133">**NX_DHCPV6_TIME_TO_LIVE** Il numero di volte in cui un pacchetto client viene inviato da un router di rete prima che il pacchetto venga rimosso.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-133">**NX_DHCPV6_TIME_TO_LIVE** The number of times a Client packet is forwarded by a network router before the packet is discarded.</span></span> <span data-ttu-id="5e5a9-134">Il valore predefinito è 0x80.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-134">The default value is 0x80.</span></span>

- <span data-ttu-id="5e5a9-135">**NX_DHCPV6_QUEUE_DEPTH** Specifica il numero di pacchetti da memorizzare nella coda di ricezione del socket UDP client prima che NetX Duo elimini i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-135">**NX_DHCPV6_QUEUE_DEPTH** Specifies the number of packets to keep in the Client UDP socket receive queue before NetX Duo discards packets.</span></span> <span data-ttu-id="5e5a9-136">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-136">The default value is 5.</span></span>

## <a name="dhcpv6-message-transmission"></a><span data-ttu-id="5e5a9-137">Trasmissione messaggi DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5e5a9-137">DHCPv6 Message Transmission</span></span>

<span data-ttu-id="5e5a9-138">È disponibile un set di opzioni client DHCPv6 per l'impostazione dei parametri sulla trasmissione dei messaggi DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-138">There are a set of DHCPv6 Client options for setting parameters on DHCPv6 message transmission.</span></span> <span data-ttu-id="5e5a9-139">Si tratta di:</span><span class="sxs-lookup"><span data-stu-id="5e5a9-139">These are:</span></span> 

  - <span data-ttu-id="5e5a9-140">timeout iniziale</span><span class="sxs-lookup"><span data-stu-id="5e5a9-140">initial timeout</span></span>

  - <span data-ttu-id="5e5a9-141">ritardo massimo alla prima trasmissione</span><span class="sxs-lookup"><span data-stu-id="5e5a9-141">maximum delay on the first transmission</span></span>

  - <span data-ttu-id="5e5a9-142">timeout massimo di ritrasmissione</span><span class="sxs-lookup"><span data-stu-id="5e5a9-142">maximum retransmission timeout</span></span> 

  - <span data-ttu-id="5e5a9-143">numero massimo di ritrasmissioni</span><span class="sxs-lookup"><span data-stu-id="5e5a9-143">maximum number of retransmissions</span></span> 

  - <span data-ttu-id="5e5a9-144">durata massima di attesa per la risposta del server</span><span class="sxs-lookup"><span data-stu-id="5e5a9-144">maximum duration to wait for server response</span></span>

<span data-ttu-id="5e5a9-145">Questi parametri si applicano a ognuno dei messaggi del client DHCPv6:</span><span class="sxs-lookup"><span data-stu-id="5e5a9-145">These parameters apply to each of the DHCPv6 Client messages:</span></span>

- <span data-ttu-id="5e5a9-146">SOLLECITAZIONE</span><span class="sxs-lookup"><span data-stu-id="5e5a9-146">SOLICIT</span></span>

- <span data-ttu-id="5e5a9-147">RICHIESTA</span><span class="sxs-lookup"><span data-stu-id="5e5a9-147">REQUEST</span></span>

- <span data-ttu-id="5e5a9-148">RINNOVARE</span><span class="sxs-lookup"><span data-stu-id="5e5a9-148">RENEW</span></span>

- <span data-ttu-id="5e5a9-149">RIASSOCIARE</span><span class="sxs-lookup"><span data-stu-id="5e5a9-149">REBIND</span></span>

- <span data-ttu-id="5e5a9-150">RELEASE</span><span class="sxs-lookup"><span data-stu-id="5e5a9-150">RELEASE</span></span>

- <span data-ttu-id="5e5a9-151">DECLINO</span><span class="sxs-lookup"><span data-stu-id="5e5a9-151">DECLINE</span></span>

- <span data-ttu-id="5e5a9-152">CONFERMA</span><span class="sxs-lookup"><span data-stu-id="5e5a9-152">CONFIRM</span></span>

- <span data-ttu-id="5e5a9-153">INFORMARE</span><span class="sxs-lookup"><span data-stu-id="5e5a9-153">INFORM</span></span>

<span data-ttu-id="5e5a9-154">Di seguito è riportato un elenco completo delle opzioni configurabili e del relativo valore predefinito</span><span class="sxs-lookup"><span data-stu-id="5e5a9-154">The following is a complete list of these configurable options and their default</span></span> 

<span data-ttu-id="5e5a9-155">values:</span><span class="sxs-lookup"><span data-stu-id="5e5a9-155">values:</span></span>

```C
NX_DHCPV6_FIRST_SOL_MAX_DELAY                   (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_INIT_SOL_TRANSMISSION_TIMEOUT         (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_SOL_RETRANSMISSION_TIMEOUT        (120 *
                                                NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_SOL_RETRANSMISSION_COUNT          0
NX_DHCPV6_MAX_SOL_RETRANSMISSION_DURATION       0

NX_DHCPV6_INIT_REQ_TRANSMISSION_TIMEOUT         (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_REQ_RETRANSMISSION_TIMEOUT        (30 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_REQ_RETRANSMISSION_COUNT          10
NX_DHCPV6_MAX_REQ_RETRANSMISSION_DURATION       0

NX_DHCPV6_INIT_RENEW_TRANSMISSION_TIMEOUT       (10*NX_DHCPV6_TICKS_PER_SECOND)     
NX_DHCPV6_MAX_RENEW_RETRANSMISSION_TIMEOUT      (600*   
                                                NX_DHCPV6_TICKS_PER_SECOND)  
NX_DHCPV6_MAX_RENEW_RETRANSMISSION_COUNT        0

NX_DHCPV6_INIT_REBIND_TRANSMISSION_TIMEOUT      (10*NX_DHCPV6_TICKS_PER_SECOND)     
NX_DHCPV6_MAX_REBIND_RETRANSMISSION_TIMEOUT     (600*  
                                                NX_DHCPV6_TICKS_PER_SECOND)  
NX_DHCPV6_MAX_REBIND_RETRANSMISSION_COUNT       0 

NX_DHCPV6_INIT_RELEASE_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_TIMEOUT    0 
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_COUNT      5  
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_DURATION   0

NX_DHCPV6_INIT_DECLINE_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_TIMEOUT    0
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_COUNT      5  
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_DURATION   0
NX_DHCPV6_FIRST_CONFIRM_MAX_DELAY               (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_INIT_CONFIRM_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_TIMEOUT    (4*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_COUNT      0  
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_DURATION   10

NX_DHCPV6_FIRST_INFORM_MAX_DELAY                (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_INIT_INFORM_TRANSMISSION_TIMEOUT      (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_TIMEOUT     (120*   
                                                NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_COUNT       0 
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_DURATION    0
```

<span data-ttu-id="5e5a9-156">Per nessun limite per un timeout di ritrasmissione, impostare il numero di ritrasmissioni dei messaggi su 0.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-156">For no limit on a retransmission timeout, set the message retransmission count to 0.</span></span> <span data-ttu-id="5e5a9-157">Per nessun limite per il numero di volte che un messaggio client DHCPv6 viene ritrasmesso (nuovi tentativi), impostare il numero di ritrasmissione dei messaggi su 0.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-157">For no limit on the number of times a DHCPv6 Client message is retransmitted (retries), set the message retransmission count to 0.</span></span>

> [!NOTE]
> <span data-ttu-id="5e5a9-158">Indipendentemente dalla durata del timeout o dal numero di tentativi, quando la durata valida di un indirizzo IPv6 scade, viene rimossa dalla tabella degli indirizzi IP e non può più essere utilizzata dal client.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-158">Regardless of length of timeout or number of retries, when an IPv6 address valid lifetime expires, it is removed from the IP address table and can no longer be used by the Client.</span></span> <span data-ttu-id="5e5a9-159">Il client DHCPv6 NetX Duo avvierà automaticamente l'invio di messaggi di SOLLECITAzione che richiedono un nuovo indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="5e5a9-159">The NetX Duo DHCPv6 Client will automatically begin sending SOLICIT messages requesting a new IPv6 address.</span></span>