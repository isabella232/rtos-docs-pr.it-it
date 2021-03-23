---
title: Capitolo 4-Descrizione dei servizi NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi NetX di Azure RTO in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 720e573b53070a754618830134f63a8421b9fd29
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821545"
---
# <a name="chapter-4---description-of-azure-rtos-netx-services"></a><span data-ttu-id="cec97-103">Capitolo 4-Descrizione dei servizi NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="cec97-103">Chapter 4 - Description of Azure RTOS NetX Services</span></span>

<span data-ttu-id="cec97-104">Questo capitolo contiene una descrizione di tutti i servizi NetX di Azure RTO in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="cec97-104">This chapter contains a description of all Azure RTOS NetX services in alphabetic order.</span></span> <span data-ttu-id="cec97-105">I nomi dei servizi sono progettati in modo da raggruppare tutti i servizi simili.</span><span class="sxs-lookup"><span data-stu-id="cec97-105">Service names are designed so all similar services are grouped together.</span></span> <span data-ttu-id="cec97-106">Ad esempio, tutti i servizi ARP sono disponibili all'inizio di questo capitolo.</span><span class="sxs-lookup"><span data-stu-id="cec97-106">For example, all ARP services are found at the beginning of this chapter.</span></span>

> [!NOTE]
> <span data-ttu-id="cec97-107">*Si noti che un'API socket BSD-Compatible è disponibile per il codice dell'applicazione legacy che non è in grado di sfruttare appieno l'API NetX a prestazioni elevate. Per altre informazioni sull'API socket BSD-Compatible, vedere l'Appendice D.*</span><span class="sxs-lookup"><span data-stu-id="cec97-107">*Note that a BSD-Compatible Socket API is available for legacy application code that cannot take full advantage of the high-performance NetX API. Refer to Appendix D for more information on the BSD-Compatible Socket API.*</span></span>

<span data-ttu-id="cec97-108">Nella sezione "valori restituiti" di ogni descrizione, i valori in **grassetto** non sono interessati dall'opzione NX_DISABLE_ERROR_CHECKING usata per disabilitare il controllo degli errori dell'API, mentre i valori in grassetto non sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="cec97-108">In the "Return Values" section of each description, values in **BOLD** are not affected by the NX_DISABLE_ERROR_CHECKING option used to disable the API error checking, while values in non-bold are completely disabled.</span></span> <span data-ttu-id="cec97-109">Le sezioni "consentito da" indicano che è possibile chiamare ogni servizio NetX.</span><span class="sxs-lookup"><span data-stu-id="cec97-109">The "Allowed From" sections indicate from which each NetX service can be called.</span></span>

## <a name="nx_arp_dynamic_entries_invalidate"></a><span data-ttu-id="cec97-110">nx_arp_dynamic_entries_invalidate</span><span class="sxs-lookup"><span data-stu-id="cec97-110">nx_arp_dynamic_entries_invalidate</span></span>

<span data-ttu-id="cec97-111">Invalida tutte le voci dinamiche nella cache ARP</span><span class="sxs-lookup"><span data-stu-id="cec97-111">Invalidate all dynamic entries in the ARP cache</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-112">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-112">Prototype</span></span>

```C
UINT nx_arp_dynamic_entries_invalidate(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-113">Description</span></span>

<span data-ttu-id="cec97-114">Questo servizio invalida tutte le voci ARP dinamiche attualmente presenti nella cache ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-114">This service invalidates all dynamic ARP entries currently in the ARP cache.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-115">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-115">Parameters</span></span>

- <span data-ttu-id="cec97-116">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-116">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-117">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-117">Return Values</span></span>

- <span data-ttu-id="cec97-118">L'invalidamento della cache ARP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-118">**NX_SUCCESS** (0x00) Successful ARP cache invalidate.</span></span>
- <span data-ttu-id="cec97-119">**NX_NOT_ENABLED** (0X14) ARP non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-119">**NX_NOT_ENABLED** (0x14) ARP is not enabled.</span></span>
- <span data-ttu-id="cec97-120">**NX_PTR_ERROR** (0x07) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-120">**NX_PTR_ERROR** (0x07) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-121">Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="cec97-121">**NX_CALLER_ERROR** (0x11) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-122">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-122">Allowed From</span></span>

<span data-ttu-id="cec97-123">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-123">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-124">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-124">Preemption Possible</span></span>

<span data-ttu-id="cec97-125">No</span><span class="sxs-lookup"><span data-stu-id="cec97-125">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-126">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-126">Example</span></span>

```c
/* Invalidate all dynamic entries in the ARP cache. */
status = nx_arp_dynamic_entries_invalidate(&ip_0);
/* If status is NX_SUCCESS the dynamic ARP entries were successfully invalidated. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-127">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-127">See Also</span></span>

- <span data-ttu-id="cec97-128">nx_arp_dynamic_entry_set, nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-128">nx_arp_dynamic_entry_set, nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="cec97-129">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-129">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="cec97-130">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-130">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="cec97-131">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-131">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_dynamic_entry_set"></a><span data-ttu-id="cec97-132">nx_arp_dynamic_entry_set</span><span class="sxs-lookup"><span data-stu-id="cec97-132">nx_arp_dynamic_entry_set</span></span>

<span data-ttu-id="cec97-133">Imposta voce ARP dinamica</span><span class="sxs-lookup"><span data-stu-id="cec97-133">Set dynamic ARP entry</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-134">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-134">Prototype</span></span>

```C
UINT nx_arp_dynamic_entry_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a><span data-ttu-id="cec97-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-135">Description</span></span>

<span data-ttu-id="cec97-136">Questo servizio alloca una voce dinamica dalla cache ARP e imposta l'indirizzo IP specificato sul mapping degli indirizzi fisici.</span><span class="sxs-lookup"><span data-stu-id="cec97-136">This service allocates a dynamic entry from the ARP cache and sets up the specified IP to physical address mapping.</span></span> <span data-ttu-id="cec97-137">Se viene specificato un indirizzo fisico zero, alla rete viene inviata una richiesta ARP effettiva per poter risolvere l'indirizzo fisico.</span><span class="sxs-lookup"><span data-stu-id="cec97-137">If a zero physical address is specified, an actual ARP request is sent to the network in order to have the physical address resolved.</span></span> <span data-ttu-id="cec97-138">Si noti inoltre che questa voce verrà rimossa se ARP aging è attivo o se la cache ARP è esaurita e si tratta della voce ARP usata meno di recente.</span><span class="sxs-lookup"><span data-stu-id="cec97-138">Also note that this entry will be removed if ARP aging is active or if the ARP cache is exhausted and this is the least recently used ARP entry.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-139">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-139">Parameters</span></span>

- <span data-ttu-id="cec97-140">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-140">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-141">**ip_address** Indirizzo IP da mappare.</span><span class="sxs-lookup"><span data-stu-id="cec97-141">**ip_address** IP address to map.</span></span>
- <span data-ttu-id="cec97-142">**physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico.</span><span class="sxs-lookup"><span data-stu-id="cec97-142">**physical_msw** Top 16 bits (47-32) of the physical address.</span></span>
- <span data-ttu-id="cec97-143">**physical_lsw** Inferiore 32 bit (31-0) dell'indirizzo fisico.</span><span class="sxs-lookup"><span data-stu-id="cec97-143">**physical_lsw** Lower 32 bits (31-0) of the physical address.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-144">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-144">Return Values</span></span>

- <span data-ttu-id="cec97-145">Il set di voci dinamiche ARP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-145">**NX_SUCCESS** (0x00) Successful ARP dynamic entry set.</span></span>
- <span data-ttu-id="cec97-146">**NX_NO_MORE_ENTRIES** (0x17) non sono disponibili altre voci ARP nella cache ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-146">**NX_NO_MORE_ENTRIES** (0x17) No more ARP entries are available in the ARP cache.</span></span>
- <span data-ttu-id="cec97-147">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-147">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-148">**NX_PTR_ERROR** (0x07) puntatore a istanza IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-148">**NX_PTR_ERROR** (0x07) Invalid IP instance pointer.</span></span>
- <span data-ttu-id="cec97-149">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-149">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-150">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-150">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-151">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-151">Allowed From</span></span>

<span data-ttu-id="cec97-152">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-152">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-153">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-153">Preemption Possible</span></span>

<span data-ttu-id="cec97-154">No</span><span class="sxs-lookup"><span data-stu-id="cec97-154">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-155">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-155">Example</span></span>

```C
/* Setup a dynamic ARP entry on the previously created IP Instance 0. */
status = nx_arp_dynamic_entry_set(&ip_0, IP_ADDRESS(1,2,3,4),
    0x1022, 0x1234);
/* If status is NX_SUCCESS, there is now a dynamic mapping between
    the IP address of 1.2.3.4 and the physical hardware address of
    10:22:00:00:12:34. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-156">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-156">See Also</span></span>

- <span data-ttu-id="cec97-157">nx_arp_dynamic_entries_invalidate, nx_arp_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-157">nx_arp_dynamic_entries_invalidate, nx_arp_enable,</span></span>
- <span data-ttu-id="cec97-158">nx_arp_gratuitous_send, nx_arp_hardware_address_find,</span><span class="sxs-lookup"><span data-stu-id="cec97-158">nx_arp_gratuitous_send, nx_arp_hardware_address_find,</span></span>
- <span data-ttu-id="cec97-159">nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-159">nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="cec97-160">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-160">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_enable"></a><span data-ttu-id="cec97-161">nx_arp_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-161">nx_arp_enable</span></span>

<span data-ttu-id="cec97-162">Abilita il protocollo ARP (Address Resolution Protocol).</span><span class="sxs-lookup"><span data-stu-id="cec97-162">Enables Address Resolution Protocol (ARP).</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-163">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-163">Prototype</span></span>

```C
UINT nx_arp_enable(
    NX_IP *ip_ptr, 
    VOID *arp_cache_memory, 
    ULONG arp_cache_size);
```

### <a name="description"></a><span data-ttu-id="cec97-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-164">Description</span></span>

<span data-ttu-id="cec97-165">Questo servizio Inizializza il componente ARP di NetX per l'istanza IP specifica.</span><span class="sxs-lookup"><span data-stu-id="cec97-165">This service initializes the ARP component of NetX for the specific IP instance.</span></span> <span data-ttu-id="cec97-166">L'inizializzazione ARP include la configurazione della cache ARP e delle varie routine di elaborazione ARP necessarie per l'invio e la ricezione di messaggi ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-166">ARP initialization includes setting up the ARP cache and various ARP processing routines necessary for sending and receiving ARP messages.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-167">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-167">Parameters</span></span>

- <span data-ttu-id="cec97-168">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-168">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-169">**arp_cache_memory** Puntatore all'area memoria per inserire la cache ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-169">**arp_cache_memory** Pointer to memory area to place ARP cache.</span></span>
- <span data-ttu-id="cec97-170">**arp_cache_size** Ogni voce ARP è 52 byte, il numero totale di voci ARP è, di conseguenza, la dimensione divisa per 52.</span><span class="sxs-lookup"><span data-stu-id="cec97-170">**arp_cache_size** Each ARP entry is 52 bytes, the total number of ARP entries is, therefore, the size divided by 52.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-171">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-171">Return Values</span></span>

- <span data-ttu-id="cec97-172">Abilitazione ARP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-172">**NX_SUCCESS** (0x00) Successful ARP enable.</span></span>
- <span data-ttu-id="cec97-173">**NX_PTR_ERROR** (0x07) un puntatore di memoria cache o un indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-173">**NX_PTR_ERROR** (0x07) Invalid IP or cache memory pointer.</span></span>
- <span data-ttu-id="cec97-174">La memoria della cache ARP fornita dall'utente **NX_SIZE_ERROR** (0x09) è troppo piccola.</span><span class="sxs-lookup"><span data-stu-id="cec97-174">**NX_SIZE_ERROR** (0x09) User supplied ARP cache memory is too small.</span></span>
- <span data-ttu-id="cec97-175">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-175">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-176">**NX_ALREADY_ENABLED** (0X15) questo componente è già stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-176">**NX_ALREADY_ENABLED** (0x15) This component has already been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-177">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-177">Allowed From</span></span>

<span data-ttu-id="cec97-178">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-178">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-179">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-179">Preemption Possible</span></span>

<span data-ttu-id="cec97-180">No</span><span class="sxs-lookup"><span data-stu-id="cec97-180">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-181">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-181">Example</span></span>

```C
/* Enable ARP and supply 1024 bytes of ARP cache memory for
    previously created IP Instance ip_0. */
status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
/* If status is NX_SUCCESS, ARP was successfully enabled for this IP instance.*/
```

### <a name="see-also"></a><span data-ttu-id="cec97-182">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-182">See Also</span></span>

- <span data-ttu-id="cec97-183">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-183">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="cec97-184">nx_arp_gratuitous_send, nx_arp_hardware_address_find,</span><span class="sxs-lookup"><span data-stu-id="cec97-184">nx_arp_gratuitous_send, nx_arp_hardware_address_find,</span></span>
- <span data-ttu-id="cec97-185">nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-185">nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="cec97-186">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-186">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_gratuitous_send"></a><span data-ttu-id="cec97-187">nx_arp_gratuitous_send</span><span class="sxs-lookup"><span data-stu-id="cec97-187">nx_arp_gratuitous_send</span></span>

<span data-ttu-id="cec97-188">Inviare una richiesta ARP gratuita</span><span class="sxs-lookup"><span data-stu-id="cec97-188">Send gratuitous ARP request</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-189">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-189">Prototype</span></span>

```C
UINT nx_arp_gratuitous_send(
    NX_IP *ip_ptr,
    VOID (*response_handler) (NX_IP *ip_ptr, NX_PACKET *packet_ptr));
```

### <a name="description"></a><span data-ttu-id="cec97-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-190">Description</span></span>

<span data-ttu-id="cec97-191">Questo servizio attraversa tutte le interfacce fisiche per trasmettere richieste ARP gratuite, purché l'indirizzo IP dell'interfaccia sia valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-191">This service goes through all the physical interfaces to transmit gratuitous ARP requests as long as the interface IP address is valid.</span></span> <span data-ttu-id="cec97-192">Se successivamente viene ricevuta una risposta ARP, viene chiamato il gestore di risposta fornito per elaborare la risposta all'ARP gratuito.</span><span class="sxs-lookup"><span data-stu-id="cec97-192">If an ARP response is subsequently received, the supplied response handler is called to process the response to the gratuitous ARP.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-193">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-193">Parameters</span></span>

- <span data-ttu-id="cec97-194">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-194">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-195">**response_handler** Puntatore alla funzione di gestione delle risposte.</span><span class="sxs-lookup"><span data-stu-id="cec97-195">**response_handler** Pointer to response handling function.</span></span> <span data-ttu-id="cec97-196">Se viene specificato NX_NULL, le risposte verranno ignorate.</span><span class="sxs-lookup"><span data-stu-id="cec97-196">If NX_NULL is supplied, responses are ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-197">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-197">Return Values</span></span>

- <span data-ttu-id="cec97-198">**NX_SUCCESS** (0x00) la trasmissione ARP gratuita è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cec97-198">**NX_SUCCESS** (0x00) Successful gratuitous ARP send.</span></span>
- <span data-ttu-id="cec97-199">**NX_NO_PACKET** (0x01) non è disponibile alcun pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-199">**NX_NO_PACKET** (0x01) No packet available.</span></span>
- <span data-ttu-id="cec97-200">**NX_NOT_ENABLED** (0X14) ARP non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-200">**NX_NOT_ENABLED** (0x14) ARP is not enabled.</span></span>
- <span data-ttu-id="cec97-201">L'indirizzo IP corrente **NX_IP_ADDRESS_ERROR** (0x21) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-201">**NX_IP_ADDRESS_ERROR** (0x21) Current IP address is invalid.</span></span>
- <span data-ttu-id="cec97-202">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-202">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-203">Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread.</span><span class="sxs-lookup"><span data-stu-id="cec97-203">**NX_CALLER_ERROR** (0x11) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-204">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-204">Allowed From</span></span>

<span data-ttu-id="cec97-205">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-205">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-206">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-206">Preemption Possible</span></span>

<span data-ttu-id="cec97-207">No</span><span class="sxs-lookup"><span data-stu-id="cec97-207">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-208">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-208">Example</span></span>

```C
/* Send gratuitous ARP without any response handler. */
status = nx_arp_gratuitous_send(&ip_0, NX_NULL);

/* If status is NX_SUCCESS the gratuitous ARP was successfully sent. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-209">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-209">See Also</span></span>

- <span data-ttu-id="cec97-210">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-210">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="cec97-211">nx_arp_enable, nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-211">nx_arp_enable, nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="cec97-212">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-212">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="cec97-213">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-213">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_hardware_address_find"></a><span data-ttu-id="cec97-214">nx_arp_hardware_address_find</span><span class="sxs-lookup"><span data-stu-id="cec97-214">nx_arp_hardware_address_find</span></span>

<span data-ttu-id="cec97-215">Individuare l'indirizzo hardware fisico dato un indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="cec97-215">Locate physical hardware address given an IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-216">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-216">Prototype</span></span>

```C
UINT nx_arp_hardware_address_find(
    NX_IP *ip_ptr,
    ULONG ip_address, 
    ULONG *physical_msw, 
    ULONG *physical_lsw);
```

### <a name="description"></a><span data-ttu-id="cec97-217">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-217">Description</span></span>

<span data-ttu-id="cec97-218">Questo servizio tenta di trovare un indirizzo hardware fisico nella cache ARP che è associato all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-218">This service attempts to find a physical hardware address in the ARP cache that is associated with the supplied IP address.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-219">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-219">Parameters</span></span>

- <span data-ttu-id="cec97-220">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-220">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-221">**ip_address** Indirizzo IP da cercare.</span><span class="sxs-lookup"><span data-stu-id="cec97-221">**ip_address** IP address to search for.</span></span>
- <span data-ttu-id="cec97-222">**physical_msw** Puntatore alla variabile per la restituzione dei primi 16 bit (47-32) dell'indirizzo fisico.</span><span class="sxs-lookup"><span data-stu-id="cec97-222">**physical_msw** Pointer to the variable for returning the top 16 bits (47-32) of the physical address.</span></span>
- <span data-ttu-id="cec97-223">**physical_lsw** Puntatore alla variabile per la restituzione dei 32 bit inferiori (31-0) dell'indirizzo fisico.</span><span class="sxs-lookup"><span data-stu-id="cec97-223">**physical_lsw** Pointer to the variable for returning the lower 32 bits (31-0) of the physical address.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-224">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-224">Return Values</span></span>

- <span data-ttu-id="cec97-225">Ricerca di indirizzi hardware ARP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-225">**NX_SUCCESS** (0x00) Successful ARP hardware address find.</span></span>
- <span data-ttu-id="cec97-226">Il mapping di **NX_ENTRY_NOT_FOUND** (0x16) non è stato trovato nella cache ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-226">**NX_ENTRY_NOT_FOUND** (0x16) Mapping was not found in the ARP cache.</span></span>
- <span data-ttu-id="cec97-227">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-227">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-228">**NX_PTR_ERROR** (0x07) un puntatore di memoria o un indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-228">**NX_PTR_ERROR** (0x07) Invalid IP or memory pointer.</span></span>
- <span data-ttu-id="cec97-229">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-229">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-230">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-230">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-231">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-231">Allowed From</span></span>

<span data-ttu-id="cec97-232">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-232">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-233">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-233">Preemption Possible</span></span>

<span data-ttu-id="cec97-234">No</span><span class="sxs-lookup"><span data-stu-id="cec97-234">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-235">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-235">Example</span></span>

```C
/* Search for the hardware address associated with the IP address of
    1.2.3.4 in the ARP cache of the previously created IP
    Instance 0. */
status = nx_arp_hardware_address_find(
    &ip_0, 
    IP_ADDRESS(1,2,3,4),
    &physical_msw, 
    &physical_lsw);

/* If status is NX_SUCCESS, the variables physical_msw and
    physical_lsw contain the hardware address.*/
```

### <a name="see-also"></a><span data-ttu-id="cec97-236">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-236">See Also</span></span>

- <span data-ttu-id="cec97-237">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-237">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="cec97-238">nx_arp_enable, nx_arp_gratuitous_send, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-238">nx_arp_enable, nx_arp_gratuitous_send, nx_arp_info_get,</span></span>
- <span data-ttu-id="cec97-239">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-239">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="cec97-240">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-240">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_info_get"></a><span data-ttu-id="cec97-241">nx_arp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-241">nx_arp_info_get</span></span>

<span data-ttu-id="cec97-242">Recuperare informazioni sulle attività ARP</span><span class="sxs-lookup"><span data-stu-id="cec97-242">Retrieve information about ARP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-243">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-243">Prototype</span></span>

```C
UINT nx_arp_info_get(
    NX_IP *ip_ptr,
    ULONG *arp_requests_sent,
    ULONG *arp_requests_received,
    ULONG *arp_responses_sent,
    ULONG *arp_responses_received,
    ULONG *arp_dynamic_entries,
    ULONG *arp_static_entries,
    ULONG *arp_aged_entries,
    ULONG *arp_invalid_messages);
```

### <a name="description"></a><span data-ttu-id="cec97-244">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-244">Description</span></span>

<span data-ttu-id="cec97-245">Questo servizio recupera informazioni sulle attività ARP per l'istanza IP associata.</span><span class="sxs-lookup"><span data-stu-id="cec97-245">This service retrieves information about ARP activities for the associated IP instance.</span></span>

<span data-ttu-id="cec97-246">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-246">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-247">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-247">Parameters</span></span>

- <span data-ttu-id="cec97-248">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-248">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-249">**arp_requests_sent** Puntatore alla destinazione per le richieste ARP totali inviate da questa istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-249">**arp_requests_sent** Pointer to destination for the total ARP requests sent from this IP instance.</span></span>
- <span data-ttu-id="cec97-250">**arp_requests_received** Puntatore alla destinazione per le richieste ARP totali ricevute dalla rete.</span><span class="sxs-lookup"><span data-stu-id="cec97-250">**arp_requests_received** Pointer to destination for the total ARP requests received from the network.</span></span>
- <span data-ttu-id="cec97-251">**arp_responses_sent** Puntatore alla destinazione per le risposte ARP totali inviate da questa istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-251">**arp_responses_sent** Pointer to destination for the total ARP responses sent from this IP instance.</span></span>
- <span data-ttu-id="cec97-252">**arp_responses_received** Puntatore alla destinazione per le risposte ARP totali ricevute dalla rete.</span><span class="sxs-lookup"><span data-stu-id="cec97-252">**arp_responses_received** Pointer to the destination for the total ARP responses received from the network.</span></span>
- <span data-ttu-id="cec97-253">**arp_dynamic_entries** Puntatore alla destinazione per il numero corrente di voci ARP dinamiche.</span><span class="sxs-lookup"><span data-stu-id="cec97-253">**arp_dynamic_entries** Pointer to the destination for the current number of dynamic ARP entries.</span></span>
- <span data-ttu-id="cec97-254">**arp_static_entries** Puntatore alla destinazione per il numero corrente di voci ARP statiche.</span><span class="sxs-lookup"><span data-stu-id="cec97-254">**arp_static_entries** Pointer to the destination for the current number of static ARP entries.</span></span>
- <span data-ttu-id="cec97-255">**arp_aged_entries** Puntatore alla destinazione del numero totale di voci ARP obsolete e diventate non valide.</span><span class="sxs-lookup"><span data-stu-id="cec97-255">**arp_aged_entries** Pointer to the destination of the total number of ARP entries that have aged and became invalid.</span></span>
- <span data-ttu-id="cec97-256">**arp_invalid_messages** Puntatore alla destinazione del totale dei messaggi ARP non validi ricevuti.</span><span class="sxs-lookup"><span data-stu-id="cec97-256">**arp_invalid_messages** Pointer to the destination of the total invalid ARP messages received.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-257">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-257">Return Values</span></span>

- <span data-ttu-id="cec97-258">Il recupero delle informazioni ARP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-258">**NX_SUCCESS** (0x00) Successful ARP information retrieval.</span></span>
- <span data-ttu-id="cec97-259">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-259">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-260">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-260">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-261">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-261">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-262">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-262">Allowed From</span></span>

<span data-ttu-id="cec97-263">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-263">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-264">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-264">Preemption Possible</span></span>

<span data-ttu-id="cec97-265">No</span><span class="sxs-lookup"><span data-stu-id="cec97-265">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-266">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-266">Example</span></span>

```C
/* Pickup ARP information for ip_0. */
status = nx_arp_info_get(
    &ip_0, 
    &arp_requests_sent,
    &arp_requests_received,
    &arp_responses_sent,
    &arp_responses_received,
    &arp_dynamic_entries,
    &arp_static_entries,
    &arp_aged_entries,
    &arp_invalid_messages);
/* If status is NX_SUCCESS, the ARP information has been stored in
    the supplied variables. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-267">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-267">See Also</span></span>

- <span data-ttu-id="cec97-268">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-268">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="cec97-269">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-269">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="cec97-270">nx_arp_hardware_address_find, nx_arp_ip_address_find,</span><span class="sxs-lookup"><span data-stu-id="cec97-270">nx_arp_hardware_address_find, nx_arp_ip_address_find,</span></span>
- <span data-ttu-id="cec97-271">nx_arp_static_entries_delete, nx_arp_static_entry_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-271">nx_arp_static_entries_delete, nx_arp_static_entry_create,</span></span>
- <span data-ttu-id="cec97-272">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-272">nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_ip_address_find"></a><span data-ttu-id="cec97-273">nx_arp_ip_address_find</span><span class="sxs-lookup"><span data-stu-id="cec97-273">nx_arp_ip_address_find</span></span>

<span data-ttu-id="cec97-274">Individuare l'indirizzo IP in base a un indirizzo fisico</span><span class="sxs-lookup"><span data-stu-id="cec97-274">Locate IP address given a physical address</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-275">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-275">Prototype</span></span>

```C
UINT nx_arp_ip_address_find(
    NX_IP *ip_ptr, 
    ULONG *ip_address,
    ULONG physical_msw, 
    ULONG physical_lsw);
```

### <a name="description"></a><span data-ttu-id="cec97-276">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-276">Description</span></span>

<span data-ttu-id="cec97-277">Questo servizio tenta di trovare un indirizzo IP nella cache ARP associata all'indirizzo fisico fornito.</span><span class="sxs-lookup"><span data-stu-id="cec97-277">This service attempts to find an IP address in the ARP cache that is associated with the supplied physical address.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-278">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-278">Parameters</span></span>

- <span data-ttu-id="cec97-279">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-279">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-280">**ip_address** Puntatore per restituire l'indirizzo IP, se ne viene trovato uno mappato.</span><span class="sxs-lookup"><span data-stu-id="cec97-280">**ip_address** Pointer to return IP address, if one is found that has been mapped.</span></span>
- <span data-ttu-id="cec97-281">**physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico da cercare.</span><span class="sxs-lookup"><span data-stu-id="cec97-281">**physical_msw** Top 16 bits (47-32) of the physical address to search for.</span></span>
- <span data-ttu-id="cec97-282">**physical_lsw** Inferiore 32 bit (31-0) dell'indirizzo fisico da cercare.</span><span class="sxs-lookup"><span data-stu-id="cec97-282">**physical_lsw** Lower 32 bits (31-0) of the physical address to search for.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-283">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-283">Return Values</span></span>

- <span data-ttu-id="cec97-284">Ricerca di indirizzi IP ARP riusciti **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="cec97-284">**NX_SUCCESS** (0x00) Successful ARP IP address find</span></span>
- <span data-ttu-id="cec97-285">Il mapping di **NX_ENTRY_NOT_FOUND** (0x16) non è stato trovato nella cache ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-285">**NX_ENTRY_NOT_FOUND** (0x16) Mapping was not found in the ARP cache.</span></span>
- <span data-ttu-id="cec97-286">**NX_PTR_ERROR** (0x07) un puntatore di memoria o un indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-286">**NX_PTR_ERROR** (0x07) Invalid IP or memory pointer.</span></span>
- <span data-ttu-id="cec97-287">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-287">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-288">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-288">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-289">**NX_INVALID_PARAMETERS** (irreversibile 0x4d) Physical_msw e physical_lsw sono entrambi 0.</span><span class="sxs-lookup"><span data-stu-id="cec97-289">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw and physical_lsw are both 0.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-290">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-290">Allowed From</span></span>

<span data-ttu-id="cec97-291">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-291">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-292">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-292">Preemption Possible</span></span>

<span data-ttu-id="cec97-293">No</span><span class="sxs-lookup"><span data-stu-id="cec97-293">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-294">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-294">Example</span></span>

```C
/* Search for the IP address associated with the hardware address of
    0x0:0x01234 in the ARP cache of the previously created IP
    Instance ip_0. */
status = nx_arp_ip_address_find(&ip_0, &ip_address, 0x0, 0x1234);

/* If status is NX_SUCCESS, the variables ip_address contains the
    associated IP address.*/
```

### <a name="see-also"></a><span data-ttu-id="cec97-295">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-295">See Also</span></span>

- <span data-ttu-id="cec97-296">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-296">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="cec97-297">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-297">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="cec97-298">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-298">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="cec97-299">nx_arp_static_entries_delete, nx_arp_static_entry_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-299">nx_arp_static_entries_delete,nx_arp_static_entry_create,</span></span>
- <span data-ttu-id="cec97-300">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-300">nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_static_entries_delete"></a><span data-ttu-id="cec97-301">nx_arp_static_entries_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-301">nx_arp_static_entries_delete</span></span>

<span data-ttu-id="cec97-302">Elimina tutte le voci ARP statiche</span><span class="sxs-lookup"><span data-stu-id="cec97-302">Delete all static ARP entries</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-303">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-303">Prototype</span></span>

```C
UINT nx_arp_static_entries_delete(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-304">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-304">Description</span></span>

<span data-ttu-id="cec97-305">Questo servizio Elimina tutte le voci statiche nella cache ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-305">This service deletes all static entries in the ARP cache.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-306">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-306">Parameters</span></span>

- <span data-ttu-id="cec97-307">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-307">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-308">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-308">Return Values</span></span>

- <span data-ttu-id="cec97-309">Vengono eliminate le voci statiche **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-309">**NX_SUCCESS** (0x00) Static entries are deleted.</span></span>
- <span data-ttu-id="cec97-310">**NX_PTR_ERROR** (0x07) Ip_ptr puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-310">**NX_PTR_ERROR** (0x07) Invalid ip_ptr pointer.</span></span>
- <span data-ttu-id="cec97-311">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-311">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-312">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-312">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-313">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-313">Allowed From</span></span>

<span data-ttu-id="cec97-314">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-314">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-315">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-315">Preemption Possible</span></span>

<span data-ttu-id="cec97-316">No</span><span class="sxs-lookup"><span data-stu-id="cec97-316">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-317">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-317">Example</span></span>

```C
/* Delete all the static ARP entries for IP Instance 0, assuming
    "ip_0" is the NX_IP structure for IP Instance 0. */

status = nx_arp_static_entries_delete(&ip_0);

/* If status is NX_SUCCESS all static ARP entries in the ARP cache
have been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-318">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-318">See Also</span></span>

- <span data-ttu-id="cec97-319">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-319">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="cec97-320">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-320">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="cec97-321">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-321">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="cec97-322">nx_arp_ip_address_find, nx_arp_static_entry_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-322">nx_arp_ip_address_find, nx_arp_static_entry_create,</span></span>
- <span data-ttu-id="cec97-323">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-323">nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_static_entry_create"></a><span data-ttu-id="cec97-324">nx_arp_static_entry_create</span><span class="sxs-lookup"><span data-stu-id="cec97-324">nx_arp_static_entry_create</span></span>

<span data-ttu-id="cec97-325">Creare un indirizzo IP statico al mapping hardware nella cache ARP</span><span class="sxs-lookup"><span data-stu-id="cec97-325">Create static IP to hardware mapping in ARP cache</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-326">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-326">Prototype</span></span>

```C
UINT nx_arp_static_entry_create(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a><span data-ttu-id="cec97-327">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-327">Description</span></span>

<span data-ttu-id="cec97-328">Questo servizio crea un mapping statico da indirizzo IP a fisico nella cache ARP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-328">This service creates a static IP-to-physical address mapping in the ARP cache for the specified IP instance.</span></span> <span data-ttu-id="cec97-329">Le voci ARP statiche non sono soggette ad aggiornamenti periodici ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-329">Static ARP entries are not subject to ARP periodic updates.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-330">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-330">Parameters</span></span>

- <span data-ttu-id="cec97-331">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-331">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-332">**ip_address** Indirizzo IP da mappare.</span><span class="sxs-lookup"><span data-stu-id="cec97-332">**ip_address** IP address to map.</span></span>
- <span data-ttu-id="cec97-333">**physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico da mappare.</span><span class="sxs-lookup"><span data-stu-id="cec97-333">**physical_msw** Top 16 bits (47-32) of the physical address to map.</span></span>
- <span data-ttu-id="cec97-334">**physical_lsw** Inferiore 32 bit (31-0) dell'indirizzo fisico da mappare.</span><span class="sxs-lookup"><span data-stu-id="cec97-334">**physical_lsw** Lower 32 bits (31-0) of the physical address to map.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-335">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-335">Return Values</span></span>

- <span data-ttu-id="cec97-336">Creazione di una voce statica ARP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-336">**NX_SUCCESS** (0x00) Successful ARP static entry create.</span></span>
- <span data-ttu-id="cec97-337">**NX_NO_MORE_ENTRIES** (0x17) non sono disponibili altre voci ARP nella cache ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-337">**NX_NO_MORE_ENTRIES** (0x17) No more ARP entries are available in the ARP cache.</span></span>
- <span data-ttu-id="cec97-338">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-338">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-339">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-339">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-340">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-340">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-341">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-341">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-342">**NX_INVALID_PARAMETERS** (irreversibile 0x4d) Physical_msw e physical_lsw sono entrambi 0.</span><span class="sxs-lookup"><span data-stu-id="cec97-342">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw and physical_lsw are both 0.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-343">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-343">Allowed From</span></span>

<span data-ttu-id="cec97-344">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-344">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-345">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-345">Preemption Possible</span></span>

<span data-ttu-id="cec97-346">No</span><span class="sxs-lookup"><span data-stu-id="cec97-346">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-347">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-347">Example</span></span>

```C
/* Create a static ARP entry on the previously created IP
    Instance 0. */

status = nx_arp_static_entry_create(&ip_0, IP_ADDRESS(1,2,3,4),
    0x0, 0x1234);

/* If status is NX_SUCCESS, there is now a static mapping between
    the IP address of 1.2.3.4 and the physical hardware address of
    00:00:00:00:12:34. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-348">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-348">See Also</span></span>

- <span data-ttu-id="cec97-349">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-349">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="cec97-350">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-350">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="cec97-351">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-351">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="cec97-352">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-352">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="cec97-353">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-353">nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_static_entry_delete"></a><span data-ttu-id="cec97-354">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-354">nx_arp_static_entry_delete</span></span>

<span data-ttu-id="cec97-355">Eliminare l'indirizzo IP statico al mapping hardware nella cache ARP</span><span class="sxs-lookup"><span data-stu-id="cec97-355">Delete static IP to hardware mapping in ARP cache</span></span>


### <a name="prototype"></a><span data-ttu-id="cec97-356">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-356">Prototype</span></span>

```C
UINT nx_arp_static_entry_delete(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a><span data-ttu-id="cec97-357">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-357">Description</span></span>

<span data-ttu-id="cec97-358">Questo servizio trova ed elimina un mapping statico da indirizzo IP a fisico creato in precedenza nella cache ARP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-358">This service finds and deletes a previously created static IP-to-physical address mapping in the ARP cache for the specified IP instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-359">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-359">Parameters</span></span>

- <span data-ttu-id="cec97-360">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-360">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-361">**ip_address** Indirizzo IP mappato in modo statico.</span><span class="sxs-lookup"><span data-stu-id="cec97-361">**ip_address** IP address that was mapped statically.</span></span>
- <span data-ttu-id="cec97-362">**physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico mappato in modo statico.</span><span class="sxs-lookup"><span data-stu-id="cec97-362">**physical_msw** Top 16 bits (47 - 32) of the physical address that was mapped statically.</span></span>
- <span data-ttu-id="cec97-363">**physical_lsw** Inferiore 32 bit (31-0) dell'indirizzo fisico mappato in modo statico.</span><span class="sxs-lookup"><span data-stu-id="cec97-363">**physical_lsw** Lower 32 bits (31 - 0) of the physical address that was mapped statically.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-364">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-364">Return Values</span></span>

- <span data-ttu-id="cec97-365">Eliminazione di una voce statica ARP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-365">**NX_SUCCESS** (0x00) Successful ARP static entry delete.</span></span>
- <span data-ttu-id="cec97-366">La voce ARP statica **NX_ENTRY_NOT_FOUND** (0x16) non è stata trovata nella cache ARP.</span><span class="sxs-lookup"><span data-stu-id="cec97-366">**NX_ENTRY_NOT_FOUND** (0x16) Static ARP entry was not found in the ARP cache.</span></span>
- <span data-ttu-id="cec97-367">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-367">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-368">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-368">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-369">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-369">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-370">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-370">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-371">**NX_INVALID_PARAMETERS** (irreversibile 0x4d) Physical_msw e physical_lsw sono entrambi 0.</span><span class="sxs-lookup"><span data-stu-id="cec97-371">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw and physical_lsw are both 0.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-372">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-372">Allowed From</span></span>

<span data-ttu-id="cec97-373">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-373">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-374">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-374">Preemption Possible</span></span>

<span data-ttu-id="cec97-375">No</span><span class="sxs-lookup"><span data-stu-id="cec97-375">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-376">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-376">Example</span></span>

```C
/* Delete a static ARP entry on the previously created IP
    instance ip_0. */
status = nx_arp_static_entry_delete(&ip_0, IP_ADDRESS(1,2,3,4),
    0x0, 0x1234);
/* If status is NX_SUCCESS, the previously created static ARP entry
    was successfully deleted. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-377">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-377">See Also</span></span>

- <span data-ttu-id="cec97-378">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-378">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="cec97-379">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-379">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="cec97-380">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-380">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="cec97-381">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-381">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="cec97-382">nx_arp_static_entry_create</span><span class="sxs-lookup"><span data-stu-id="cec97-382">nx_arp_static_entry_create</span></span>

## <a name="nx_icmp_enable"></a><span data-ttu-id="cec97-383">nx_icmp_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-383">nx_icmp_enable</span></span>

<span data-ttu-id="cec97-384">Abilita Internet Control Message Protocol (ICMP)</span><span class="sxs-lookup"><span data-stu-id="cec97-384">Enable Internet Control Message Protocol (ICMP)</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-385">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-385">Prototype</span></span>

```C
UINT nx_icmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-386">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-386">Description</span></span>

<span data-ttu-id="cec97-387">Questo servizio Abilita il componente ICMP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-387">This service enables the ICMP component for the specified IP instance.</span></span>
<span data-ttu-id="cec97-388">Il componente ICMP è responsabile della gestione dei messaggi di errore Internet e delle richieste di ping e delle risposte.</span><span class="sxs-lookup"><span data-stu-id="cec97-388">The ICMP component is responsible for handling Internet error messages and ping requests and replies.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-389">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-389">Parameters</span></span>

- <span data-ttu-id="cec97-390">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-390">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-391">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-391">Return Values</span></span>

- <span data-ttu-id="cec97-392">Abilitazione ICMP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-392">**NX_SUCCESS** (0x00) Successful ICMP enable.</span></span>
- <span data-ttu-id="cec97-393">Il protocollo ICMP **NX_ALREADY_ENABLED** (0x15) è già abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-393">**NX_ALREADY_ENABLED** (0x15) ICMP is already enabled.</span></span>
- <span data-ttu-id="cec97-394">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-394">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-395">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-395">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-396">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-396">Allowed From</span></span>

<span data-ttu-id="cec97-397">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-397">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-398">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-398">Preemption Possible</span></span>

<span data-ttu-id="cec97-399">No</span><span class="sxs-lookup"><span data-stu-id="cec97-399">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-400">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-400">Example</span></span>

```C
/* Enable ICMP on the previously created IP Instance ip_0. */
status = nx_icmp_enable(&ip_0);

/* If status is NX_SUCCESS, ICMP is enabled. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-401">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-401">See Also</span></span>

- <span data-ttu-id="cec97-402">nx_icmp_info_get, nx_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="cec97-402">nx_icmp_info_get, nx_icmp_ping</span></span>

## <a name="nx_icmp_info_get"></a><span data-ttu-id="cec97-403">nx_icmp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-403">nx_icmp_info_get</span></span>

<span data-ttu-id="cec97-404">Recuperare informazioni sulle attività ICMP</span><span class="sxs-lookup"><span data-stu-id="cec97-404">Retrieve information about ICMP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-405">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-405">Prototype</span></span>

```C
UINT nx_icmp_info_get(
    NX_IP *ip_ptr,
    ULONG *pings_sent,
    ULONG *ping_timeouts,
    ULONG *ping_threads_suspended,
    ULONG *ping_responses_received,
    ULONG *icmp_checksum_errors,
    ULONG *icmp_unhandled_messages);
```

### <a name="description"></a><span data-ttu-id="cec97-406">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-406">Description</span></span>

<span data-ttu-id="cec97-407">Questo servizio recupera informazioni sulle attività ICMP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-407">This service retrieves information about ICMP activities for the specified IP instance.</span></span>

<span data-ttu-id="cec97-408">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-408">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-409">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-409">Parameters</span></span>

- <span data-ttu-id="cec97-410">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-410">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-411">**pings_sent** Puntatore alla destinazione per il numero totale di ping inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-411">**pings_sent** Pointer to destination for the total number of pings sent.</span></span>
- <span data-ttu-id="cec97-412">**ping_timeouts** Puntatore alla destinazione per il numero totale di timeout del ping.</span><span class="sxs-lookup"><span data-stu-id="cec97-412">**ping_timeouts** Pointer to destination for the total number of ping timeouts.</span></span>
- <span data-ttu-id="cec97-413">**ping_threads_suspended** Puntatore alla destinazione del numero totale di thread sospesi nelle richieste di ping.</span><span class="sxs-lookup"><span data-stu-id="cec97-413">**ping_threads_suspended** Pointer to destination of the total number of threads suspended on ping requests.</span></span>
- <span data-ttu-id="cec97-414">**ping_responses_received** Puntatore a ESTINAZIONE del numero totale di risposte ping ricevute.</span><span class="sxs-lookup"><span data-stu-id="cec97-414">**ping_responses_received** Pointer to estination of the total number of ping responses received.</span></span>
- <span data-ttu-id="cec97-415">**icmp_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum ICMP.</span><span class="sxs-lookup"><span data-stu-id="cec97-415">**icmp_checksum_errors** Pointer to destination of the total number of ICMP checksum errors.</span></span>
- <span data-ttu-id="cec97-416">**icmp_unhandled_messages** Puntatore a ESTINAZIONE del numero totale di messaggi ICMP non gestiti.</span><span class="sxs-lookup"><span data-stu-id="cec97-416">**icmp_unhandled_messages** Pointer to estination of the total number of un-handled ICMP messages.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-417">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-417">Return Values</span></span>

- <span data-ttu-id="cec97-418">Il recupero delle informazioni ICMP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-418">**NX_SUCCESS** (0x00) Successful ICMP information retrieval.</span></span>
- <span data-ttu-id="cec97-419">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-419">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-420">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-420">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-421">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-421">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-422">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-422">Allowed From</span></span>

<span data-ttu-id="cec97-423">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-423">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-424">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-424">Preemption Possible</span></span>

<span data-ttu-id="cec97-425">No</span><span class="sxs-lookup"><span data-stu-id="cec97-425">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-426">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-426">Example</span></span>

```C
/* Retrieve ICMP information from previously created IP
    instance ip_0. */
status = nx_icmp_info_get(
    &ip_0, 
    &pings_sent, 
    &ping_timeouts,
    &ping_threads_suspended,
    &ping_responses_received,
    &icmp_checksum_errors,
    &icmp_unhandled_messages);

/* If status is NX_SUCCESS, ICMP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-427">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-427">See Also</span></span>

- <span data-ttu-id="cec97-428">nx_icmp_enable, nx_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="cec97-428">nx_icmp_enable, nx_icmp_ping</span></span>

## <a name="nx_icmp_ping"></a><span data-ttu-id="cec97-429">nx_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="cec97-429">nx_icmp_ping</span></span>

<span data-ttu-id="cec97-430">Invia richiesta ping all'indirizzo IP specificato</span><span class="sxs-lookup"><span data-stu-id="cec97-430">Send ping request to specified IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-431">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-431">Prototype</span></span>

```C
UINT nx_icmp_ping(
    NX_IP *ip_ptr,
    ULONG ip_address,
    CHAR *data, ULONG data_size,
    NX_PACKET **response_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-432">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-432">Description</span></span>

<span data-ttu-id="cec97-433">Questo servizio invia una richiesta ping all'indirizzo IP specificato e attende il periodo di tempo specificato per un messaggio di risposta ping.</span><span class="sxs-lookup"><span data-stu-id="cec97-433">This service sends a ping request to the specified IP address and waits for the specified amount of time for a ping response message.</span></span> <span data-ttu-id="cec97-434">Se non viene ricevuta alcuna risposta, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="cec97-434">If no response is received, an error is returned.</span></span> <span data-ttu-id="cec97-435">In caso contrario, viene restituito l'intero messaggio di risposta nella variabile a cui punta response_ptr.</span><span class="sxs-lookup"><span data-stu-id="cec97-435">Otherwise, the entire response message is returned in the variable pointed to by response_ptr.</span></span>

<span data-ttu-id="cec97-436">*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto dopo che non è più necessario.*</span><span class="sxs-lookup"><span data-stu-id="cec97-436">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet after it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-437">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-437">Parameters</span></span>

- <span data-ttu-id="cec97-438">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-438">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-439">**ip_address** Indirizzo IP, in ordine byte host, per eseguire il ping.</span><span class="sxs-lookup"><span data-stu-id="cec97-439">**ip_address** IP address, in host byte order, to ping.</span></span> <span data-ttu-id="cec97-440">Puntatore dati all'area dati per il messaggio ping.</span><span class="sxs-lookup"><span data-stu-id="cec97-440">data Pointer to data area for ping message.</span></span>
- <span data-ttu-id="cec97-441">**DATA_SIZE** Numero di byte nei dati ping</span><span class="sxs-lookup"><span data-stu-id="cec97-441">**data_size** Number of bytes in the ping data</span></span>
- <span data-ttu-id="cec97-442">**response_ptr** Puntatore al puntatore del pacchetto per restituire il messaggio di risposta ping in.</span><span class="sxs-lookup"><span data-stu-id="cec97-442">**response_ptr** Pointer to packet pointer to return the ping response message in.</span></span>
- <span data-ttu-id="cec97-443">**WAIT_OPTION** Definisce il tempo di attesa per una risposta ping.</span><span class="sxs-lookup"><span data-stu-id="cec97-443">**wait_option** Defines how long to wait for a ping response.</span></span> <span data-ttu-id="cec97-444">le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-444">wait options are defined as follows:</span></span>

  - <span data-ttu-id="cec97-445">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-445">NX_NO_WAIT (0x00000000)</span></span>
  - <span data-ttu-id="cec97-446">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-446">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
  - <span data-ttu-id="cec97-447">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-447">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-448">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-448">Return Values</span></span>

- <span data-ttu-id="cec97-449">**NX_SUCCESS** (0x00) Ping riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-449">**NX_SUCCESS** (0x00) Successful ping.</span></span> <span data-ttu-id="cec97-450">Il puntatore del messaggio di risposta è stato inserito nella variabile a cui punta response_ptr.</span><span class="sxs-lookup"><span data-stu-id="cec97-450">Response message pointer was placed in the variable pointed to by response_ptr.</span></span>
- <span data-ttu-id="cec97-451">**NX_NO_PACKET** (0x01) non è in grado di allocare un pacchetto di richieste ping.</span><span class="sxs-lookup"><span data-stu-id="cec97-451">**NX_NO_PACKET** (0x01) Unable to allocate a ping request packet.</span></span>
- <span data-ttu-id="cec97-452">L'area dati specificata **NX_OVERFLOW** (0x03) supera la dimensione predefinita del pacchetto per questa istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-452">**NX_OVERFLOW** (0x03) Specified data area exceeds the default packet size for this IP instance.</span></span>
- <span data-ttu-id="cec97-453">L'IP richiesto **NX_NO_RESPONSE** (0x29) non ha risposto.</span><span class="sxs-lookup"><span data-stu-id="cec97-453">**NX_NO_RESPONSE** (0x29) Requested IP did not respond.</span></span>
- <span data-ttu-id="cec97-454">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-454">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-455">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-455">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-456">**NX_PTR_ERROR** (0x07) un puntatore IP o risposta non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-456">**NX_PTR_ERROR** (0x07) Invalid IP or response pointer.</span></span>
- <span data-ttu-id="cec97-457">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-457">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-458">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-458">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-459">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-459">Allowed From</span></span>

<span data-ttu-id="cec97-460">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-460">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-461">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-461">Preemption Possible</span></span>

<span data-ttu-id="cec97-462">No</span><span class="sxs-lookup"><span data-stu-id="cec97-462">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-463">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-463">Example</span></span>

```C
/* Issue a ping to IP address 1.2.3.5 from the previously created IP
    Instance ip_0. */
status = nx_icmp_ping(&ip_0, IP_ADDRESS(1,2,3,5), "abcd", 4,
    &response_ptr, 10);

/* If status is NX_SUCCESS, a ping response was received from IP
    address 1.2.3.5 and the response packet is contained in the
    packet pointed to by response_ptr. It should have the same "abcd"
    four bytes of data. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-464">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-464">See Also</span></span>

- <span data-ttu-id="cec97-465">nx_icmp_enable, nx_icmp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-465">nx_icmp_enable, nx_icmp_info_get</span></span>

## <a name="nx_igmp_enable"></a><span data-ttu-id="cec97-466">nx_igmp_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-466">nx_igmp_enable</span></span>

<span data-ttu-id="cec97-467">Abilita IGMP (Internet Group Management Protocol)</span><span class="sxs-lookup"><span data-stu-id="cec97-467">Enable Internet Group Management Protocol (IGMP)</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-468">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-468">Prototype</span></span>

```C
UINT nx_igmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-469">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-469">Description</span></span>

<span data-ttu-id="cec97-470">Questo servizio Abilita il componente IGMP nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-470">This service enables the IGMP component on the specified IP instance.</span></span>
<span data-ttu-id="cec97-471">Il componente IGMP è responsabile della fornitura del supporto per le operazioni di gestione dei gruppi multicast IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-471">The IGMP component is responsible for providing support for IP multicast group management operations.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-472">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-472">Parameters</span></span>

- <span data-ttu-id="cec97-473">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-473">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-474">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-474">Return Values</span></span>

- <span data-ttu-id="cec97-475">L'abilitazione di IGMP è riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-475">**NX_SUCCESS** (0x00) Successful IGMP enable.</span></span>
- <span data-ttu-id="cec97-476">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-476">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-477">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-477">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-478">**NX_ALREADY_ENABLED** (0X15) questo componente è già stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-478">**NX_ALREADY_ENABLED** (0x15) This component has already been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-479">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-479">Allowed From</span></span>

<span data-ttu-id="cec97-480">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-480">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-481">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-481">Preemption Possible</span></span>

<span data-ttu-id="cec97-482">No</span><span class="sxs-lookup"><span data-stu-id="cec97-482">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-483">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-483">Example</span></span>

```C
/* Enable IGMP on the previously created IP Instance ip_0. */
status = nx_igmp_enable(&ip_0);

/* If status is NX_SUCCESS, IGMP is enabled. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-484">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-484">See Also</span></span>

- <span data-ttu-id="cec97-485">nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-485">nx_igmp_info_get,nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="cec97-486">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span><span class="sxs-lookup"><span data-stu-id="cec97-486">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span></span>
- <span data-ttu-id="cec97-487">nx_igmp_multicast_join, nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="cec97-487">nx_igmp_multicast_join, nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_info_get"></a><span data-ttu-id="cec97-488">nx_igmp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-488">nx_igmp_info_get</span></span>

<span data-ttu-id="cec97-489">Recuperare informazioni sulle attività IGMP</span><span class="sxs-lookup"><span data-stu-id="cec97-489">Retrieve information about IGMP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-490">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-490">Prototype</span></span>

```C
UINT nx_igmp_info_get(
    NX_IP *ip_ptr,
    ULONG *igmp_reports_sent,
    ULONG *igmp_queries_received,
    ULONG *igmp_checksum_errors,
    ULONG *current_groups_joined);
```

### <a name="description"></a><span data-ttu-id="cec97-491">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-491">Description</span></span>

<span data-ttu-id="cec97-492">Questo servizio recupera informazioni sulle attività IGMP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-492">This service retrieves information about IGMP activities for the specified IP instance.</span></span>

<span data-ttu-id="cec97-493">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-493">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-494">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-494">Parameters</span></span>

- <span data-ttu-id="cec97-495">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-495">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-496">**igmp_reports_sent** Puntatore alla destinazione per il numero totale di report ICMP inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-496">**igmp_reports_sent** Pointer to destination for the total number of ICMP reports sent.</span></span>
- <span data-ttu-id="cec97-497">**igmp_queries_received** Puntatore alla destinazione per il numero totale di query ricevute dal router multicast.</span><span class="sxs-lookup"><span data-stu-id="cec97-497">**igmp_queries_received** Pointer to destination for the total number of queries received by multicast router.</span></span>
- <span data-ttu-id="cec97-498">**igmp_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum IGMP nei pacchetti di ricezione.</span><span class="sxs-lookup"><span data-stu-id="cec97-498">**igmp_checksum_errors** Pointer to destination of the total number of IGMP checksum errors on receive packets.</span></span>
- <span data-ttu-id="cec97-499">**current_groups_joined** Puntatore alla destinazione del numero corrente di gruppi Uniti tramite questa istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-499">**current_groups_joined** Pointer to destination of the current number of groups joined through this IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-500">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-500">Return Values</span></span>

- <span data-ttu-id="cec97-501">Il recupero delle informazioni IGMP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-501">**NX_SUCCESS** (0x00) Successful IGMP information retrieval.</span></span>
- <span data-ttu-id="cec97-502">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-502">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-503">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-503">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-504">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-504">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-505">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-505">Allowed From</span></span>

<span data-ttu-id="cec97-506">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-506">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-507">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-507">Preemption Possible</span></span>

<span data-ttu-id="cec97-508">No</span><span class="sxs-lookup"><span data-stu-id="cec97-508">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-509">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-509">Example</span></span>

```C
/* Retrieve IGMP information
    from previously created IP Instance ip_0. */
status = nx_igmp_info_get(
    &ip_0, 
    &igmp_reports_sent,
    &igmp_queries_received,
    &igmp_checksum_errors,
    &current_groups_joined);
/* If status is NX_SUCCESS, IGMP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-510">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-510">See Also</span></span>

- <span data-ttu-id="cec97-511">nx_igmp_enable, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-511">nx_igmp_enable, nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="cec97-512">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span><span class="sxs-lookup"><span data-stu-id="cec97-512">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span></span>
- <span data-ttu-id="cec97-513">nx_igmp_multicast_join, nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="cec97-513">nx_igmp_multicast_join, nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_loopback_disable"></a><span data-ttu-id="cec97-514">nx_igmp_loopback_disable</span><span class="sxs-lookup"><span data-stu-id="cec97-514">nx_igmp_loopback_disable</span></span>

<span data-ttu-id="cec97-515">Disabilitare il loopback IGMP</span><span class="sxs-lookup"><span data-stu-id="cec97-515">Disable IGMP loopback</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-516">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-516">Prototype</span></span>

```C
UINT nx_igmp_loopback_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-517">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-517">Description</span></span>

<span data-ttu-id="cec97-518">Questo servizio Disabilita il loopback IGMP per tutti i gruppi multicast successivi Uniti in join.</span><span class="sxs-lookup"><span data-stu-id="cec97-518">This service disables IGMP loopback for all subsequent multicast groups joined.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-519">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-519">Parameters</span></span>

- <span data-ttu-id="cec97-520">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-520">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-521">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-521">Return Values</span></span>
- <span data-ttu-id="cec97-522">**NX_SUCCESS** (0x00) la disabilitazione del loopback IGMP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-522">**NX_SUCCESS** (0x00) Successful IGMP loopback disable.</span></span>
- <span data-ttu-id="cec97-523">Il **NX_NOT_ENABLED** (0X14) IGMP non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-523">**NX_NOT_ENABLED** (0x14) IGMP is not enabled.</span></span>
- <span data-ttu-id="cec97-524">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-524">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-525">Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-525">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-526">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-526">Allowed From</span></span>

<span data-ttu-id="cec97-527">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-527">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-528">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-528">Preemption Possible</span></span>

<span data-ttu-id="cec97-529">No</span><span class="sxs-lookup"><span data-stu-id="cec97-529">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-530">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-530">Example</span></span>

```C
/* Disable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_disable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is disabled. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-531">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-531">See Also</span></span>

- <span data-ttu-id="cec97-532">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-532">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_enable,</span></span>
- <span data-ttu-id="cec97-533">nx_igmp_multicast_interface_join, nx_igmp_multicast_join,</span><span class="sxs-lookup"><span data-stu-id="cec97-533">nx_igmp_multicast_interface_join, nx_igmp_multicast_join,</span></span>
- <span data-ttu-id="cec97-534">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="cec97-534">nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_loopback_enable"></a><span data-ttu-id="cec97-535">nx_igmp_loopback_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-535">nx_igmp_loopback_enable</span></span>

<span data-ttu-id="cec97-536">Abilita loopback loopback</span><span class="sxs-lookup"><span data-stu-id="cec97-536">Enable IGMP loopback</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-537">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-537">Prototype</span></span>

```C
UINT nx_igmp_loopback_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-538">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-538">Description</span></span>

<span data-ttu-id="cec97-539">Questo servizio Abilita il loopback IGMP per tutti i gruppi multicast successivi Uniti in join.</span><span class="sxs-lookup"><span data-stu-id="cec97-539">This service enables IGMP loopback for all subsequent multicast groups joined.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-540">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-540">Parameters</span></span>

- <span data-ttu-id="cec97-541">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-541">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-542">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-542">Return Values</span></span>
- <span data-ttu-id="cec97-543">**NX_SUCCESS** (0x00) la disabilitazione del loopback IGMP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-543">**NX_SUCCESS** (0x00) Successful IGMP loopback disable.</span></span>
- <span data-ttu-id="cec97-544">Il **NX_NOT_ENABLED** (0X14) IGMP non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-544">**NX_NOT_ENABLED** (0x14) IGMP is not enabled.</span></span>
- <span data-ttu-id="cec97-545">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-545">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-546">Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-546">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-547">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-547">Allowed From</span></span>

<span data-ttu-id="cec97-548">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-548">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-549">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-549">Preemption Possible</span></span>

<span data-ttu-id="cec97-550">No</span><span class="sxs-lookup"><span data-stu-id="cec97-550">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-551">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-551">Example</span></span>

```C
/* Enable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_enable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is enabled. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-552">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-552">See Also</span></span>

- <span data-ttu-id="cec97-553">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-553">nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="cec97-554">nx_igmp_multicast_interface_join, nx_igmp_multicast_join,</span><span class="sxs-lookup"><span data-stu-id="cec97-554">nx_igmp_multicast_interface_join, nx_igmp_multicast_join,</span></span>
- <span data-ttu-id="cec97-555">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="cec97-555">nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_multicast_interface_join"></a><span data-ttu-id="cec97-556">nx_igmp_multicast_interface_join</span><span class="sxs-lookup"><span data-stu-id="cec97-556">nx_igmp_multicast_interface_join</span></span>

<span data-ttu-id="cec97-557">Unisci istanza IP al gruppo multicast specificato tramite un'interfaccia</span><span class="sxs-lookup"><span data-stu-id="cec97-557">Join IP instance to specified multicast group via an interface</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-558">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-558">Prototype</span></span>

```C
UINT nx_igmp_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="cec97-559">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-559">Description</span></span>

<span data-ttu-id="cec97-560">Questo servizio unisce un'istanza IP al gruppo multicast specificato tramite un'interfaccia di rete specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-560">This service joins an IP instance to the specified multicast group via a specified network interface.</span></span> <span data-ttu-id="cec97-561">Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="cec97-561">An internal counter is maintained to keep track of the number of times the same group has been joined.</span></span> <span data-ttu-id="cec97-562">Dopo l'aggiunta al gruppo multicast, il componente IGMP consentirà la ricezione di pacchetti IP con questo indirizzo di gruppo tramite l'interfaccia di rete specificata e segnalerà anche ai router che questo IP è membro di questo gruppo multicast.</span><span class="sxs-lookup"><span data-stu-id="cec97-562">After joining the multicast group, the IGMP component will allow reception of IP packets with this group address via the specified network interface and also report to routers that this IP is a member of this multicast group.</span></span> <span data-ttu-id="cec97-563">I messaggi di join di appartenenza IGMP, di report e di uscita vengono inviati anche tramite l'interfaccia di rete specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-563">The IGMP membership join, report, and leave messages are also sent via the specified network interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-564">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-564">Parameters</span></span>

- <span data-ttu-id="cec97-565">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-565">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-566">**group_address** Indirizzo del gruppo multicast IP di classe D da unire in ordine byte host.</span><span class="sxs-lookup"><span data-stu-id="cec97-566">**group_address** Class D IP multicast group address to join in host byte order.</span></span>
- <span data-ttu-id="cec97-567">**interface_index** Indice dell'interfaccia associata all'istanza di NetX.</span><span class="sxs-lookup"><span data-stu-id="cec97-567">**interface_index** Index of the Interface attached to the NetX instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-568">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-568">Return Values</span></span>

- <span data-ttu-id="cec97-569">**NX_SUCCESS** (0x00) il join del gruppo multicast è riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-569">**NX_SUCCESS** (0x00) Successful multicast group join.</span></span>
- <span data-ttu-id="cec97-570">**NX_NO_MORE_ENTRIES** (0x17) non è possibile unire in join più gruppi multicast. è stato superato il limite massimo.</span><span class="sxs-lookup"><span data-stu-id="cec97-570">**NX_NO_MORE_ENTRIES** (0x17) No more multicast groups can be joined, maximum exceeded.</span></span>
- <span data-ttu-id="cec97-571">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-571">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-572">L'indice del dispositivo **NX_INVALID_INTERFACE** (0x4C) punta a un'interfaccia di rete non valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-572">**NX_INVALID_INTERFACE** (0x4C) Device index points to an invalid network interface.</span></span>
- <span data-ttu-id="cec97-573">L'indirizzo del gruppo multicast **NX_IP_ADDRESS_ERROR** (0x21) specificato non è un indirizzo di classe D valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-573">**NX_IP_ADDRESS_ERROR** (0x21) Multicast group address provided is not a valid class D address.</span></span>
- <span data-ttu-id="cec97-574">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-574">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-575">Il supporto multicast IP **NX_NOT_ENABLED** (0x14) non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-575">**NX_NOT_ENABLED** (0x14) IP multicast support is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-576">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-576">Allowed From</span></span>

<span data-ttu-id="cec97-577">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-577">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-578">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-578">Preemption Possible</span></span>

<span data-ttu-id="cec97-579">No</span><span class="sxs-lookup"><span data-stu-id="cec97-579">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-580">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-580">Example</span></span>

```C
/* Previously created IP Instance joins the multicast group
    244.0.0.200, via the interface at index 1 in the IP interface list. */
#define INTERFACE_INDEX 1
status = nx_igmp_multicast_interface_join
    (&ip, IP_ADDRESS(244,0,0,200),
    INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully joined
    the multicast group. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-581">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-581">See Also</span></span>

- <span data-ttu-id="cec97-582">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-582">nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="cec97-583">nx_igmp_loopback_enable, nx_igmp_multicast_join,</span><span class="sxs-lookup"><span data-stu-id="cec97-583">nx_igmp_loopback_enable, nx_igmp_multicast_join,</span></span>
- <span data-ttu-id="cec97-584">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="cec97-584">nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_multicast_join"></a><span data-ttu-id="cec97-585">nx_igmp_multicast_join</span><span class="sxs-lookup"><span data-stu-id="cec97-585">nx_igmp_multicast_join</span></span>

<span data-ttu-id="cec97-586">Unisci istanza IP al gruppo multicast specificato</span><span class="sxs-lookup"><span data-stu-id="cec97-586">Join IP instance to specified multicast group</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-587">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-587">Prototype</span></span>

```C
UINT nx_igmp_multicast_join(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a><span data-ttu-id="cec97-588">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-588">Description</span></span>

<span data-ttu-id="cec97-589">Questo servizio unisce un'istanza IP al gruppo multicast specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-589">This service joins an IP instance to the specified multicast group.</span></span> <span data-ttu-id="cec97-590">Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="cec97-590">An internal counter is maintained to keep track of the number of times the same group has been joined.</span></span> <span data-ttu-id="cec97-591">Il driver viene indirizzato per l'invio di un report IGMP se si tratta della prima richiesta di join in rete che indica l'intenzione dell'host di partecipare al gruppo.</span><span class="sxs-lookup"><span data-stu-id="cec97-591">The driver is commanded to send an IGMP report if this is the first join request out on the network indicating the host's intention to join the group.</span></span> <span data-ttu-id="cec97-592">Dopo l'Unione, il componente IGMP consentirà la ricezione di pacchetti IP con questo indirizzo di gruppo e report ai router che questo IP è membro di questo gruppo multicast.</span><span class="sxs-lookup"><span data-stu-id="cec97-592">After joining, the IGMP component will allow reception of IP packets with this group address and report to routers that this IP is a member of this multicast group.</span></span>

> [!NOTE]
> <span data-ttu-id="cec97-593">*Per aggiungere un gruppo multicast in un dispositivo non primario, usare il nx_igmp_multicast_interface_join di servizio **.***</span><span class="sxs-lookup"><span data-stu-id="cec97-593">*To join a multicast group on a non-primary device, use the service **nx_igmp_multicast_interface_join.***</span></span>

- <span data-ttu-id="cec97-594">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="cec97-594">**Parameters**</span></span>

- <span data-ttu-id="cec97-595">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-595">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-596">**group_address** Indirizzo del gruppo multicast IP di classe D da unire.</span><span class="sxs-lookup"><span data-stu-id="cec97-596">**group_address** Class D IP multicast group address to join.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-597">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-597">Return Values</span></span>

- <span data-ttu-id="cec97-598">**NX_SUCCESS** (0x00) il join del gruppo multicast è riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-598">**NX_SUCCESS** (0x00) Successful multicast group join.</span></span>
- <span data-ttu-id="cec97-599">**NX_NO_MORE_ENTRIES** (0x17) non è possibile unire in join più gruppi multicast. è stato superato il limite massimo.</span><span class="sxs-lookup"><span data-stu-id="cec97-599">**NX_NO_MORE_ENTRIES** (0x17) No more multicast groups can be joined, maximum exceeded.</span></span>
- <span data-ttu-id="cec97-600">L'indice del dispositivo **NX_INVALID_INTERFACE** (0x4C) punta a un'interfaccia di rete non valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-600">**NX_INVALID_INTERFACE** (0x4C) Device index points to an invalid network interface.</span></span>
- <span data-ttu-id="cec97-601">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo del gruppo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-601">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP group address.</span></span>
- <span data-ttu-id="cec97-602">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-602">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-603">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-603">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-604">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-604">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-605">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-605">Allowed From</span></span>

<span data-ttu-id="cec97-606">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-606">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-607">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-607">Preemption Possible</span></span>

<span data-ttu-id="cec97-608">No</span><span class="sxs-lookup"><span data-stu-id="cec97-608">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-609">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-609">Example</span></span>

```C
/* Previously created IP Instance ip_0 joins the multicast group
    224.0.0.200. */
status = nx_igmp_multicast_join(&ip_0, IP_ADDRESS(224,0,0,200));

/* If status is NX_SUCCESS, this IP instance has successfully
    joined the multicast group 224.0.0.200. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-610">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-610">See Also</span></span>

- <span data-ttu-id="cec97-611">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-611">nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="cec97-612">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span><span class="sxs-lookup"><span data-stu-id="cec97-612">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span></span>
- <span data-ttu-id="cec97-613">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="cec97-613">nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_multicast_leave"></a><span data-ttu-id="cec97-614">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="cec97-614">nx_igmp_multicast_leave</span></span>

<span data-ttu-id="cec97-615">Genera l'istanza IP per uscire dal gruppo multicast specificato</span><span class="sxs-lookup"><span data-stu-id="cec97-615">Cause IP instance to leave specified multicast group</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-616">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-616">Prototype</span></span>

```C
UINT nx_igmp_multicast_leave(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a><span data-ttu-id="cec97-617">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-617">Description</span></span>

<span data-ttu-id="cec97-618">Questo servizio fa in modo che un'istanza IP lasci il gruppo multicast specificato, se il numero di richieste Leave corrisponde al numero di richieste di join.</span><span class="sxs-lookup"><span data-stu-id="cec97-618">This service causes an IP instance to leave the specified multicast group, if the number of leave requests matches the number of join requests.</span></span> <span data-ttu-id="cec97-619">In caso contrario, il conteggio interno dei join viene semplicemente decrementato.</span><span class="sxs-lookup"><span data-stu-id="cec97-619">Otherwise, the internal join count is simply decremented.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-620">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-620">Parameters</span></span>

- <span data-ttu-id="cec97-621">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-621">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-622">**group_address** Gruppo multicast da lasciare.</span><span class="sxs-lookup"><span data-stu-id="cec97-622">**group_address** Multicast group to leave.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-623">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-623">Return Values</span></span>

- <span data-ttu-id="cec97-624">**NX_SUCCESS** (0x00) il join del gruppo multicast è riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-624">**NX_SUCCESS** (0x00) Successful multicast group join.</span></span>
- <span data-ttu-id="cec97-625">Impossibile trovare **NX_ENTRY_NOT_FOUND** (0x16) la richiesta di join precedente.</span><span class="sxs-lookup"><span data-stu-id="cec97-625">**NX_ENTRY_NOT_FOUND** (0x16) Previous join request was not found.</span></span>
- <span data-ttu-id="cec97-626">L'indice del dispositivo **NX_INVALID_INTERFACE** (0x4C) punta a un'interfaccia di rete non valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-626">**NX_INVALID_INTERFACE** (0x4C) Device index points to an invalid network interface.</span></span>
- <span data-ttu-id="cec97-627">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo del gruppo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-627">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP group address.</span></span>
- <span data-ttu-id="cec97-628">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-628">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-629">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-629">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-630">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-630">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-631">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-631">Allowed From</span></span>

<span data-ttu-id="cec97-632">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-632">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-633">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-633">Preemption Possible</span></span>

<span data-ttu-id="cec97-634">No</span><span class="sxs-lookup"><span data-stu-id="cec97-634">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-635">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-635">Example</span></span>

```C
/* Cause IP instance to leave the multicast group 224.0.0.200. */
status = nx_igmp_multicast_leave(&ip_0, IP_ADDRESS(224,0,0,200);

/* If status is NX_SUCCESS, this IP instance has successfully left
    the multicast group 224.0.0.200. */
```
### <a name="see-also"></a><span data-ttu-id="cec97-636">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-636">See Also</span></span>

- <span data-ttu-id="cec97-637">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-637">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="cec97-638">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span><span class="sxs-lookup"><span data-stu-id="cec97-638">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span></span>
- <span data-ttu-id="cec97-639">nx_igmp_multicast_join</span><span class="sxs-lookup"><span data-stu-id="cec97-639">nx_igmp_multicast_join</span></span>

## <a name="nx_ip_address_change_notifiy"></a><span data-ttu-id="cec97-640">nx_ip_address_change_notifiy</span><span class="sxs-lookup"><span data-stu-id="cec97-640">nx_ip_address_change_notifiy</span></span>

<span data-ttu-id="cec97-641">Notifica all'applicazione se le modifiche all'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="cec97-641">Notify application if IP address changes</span></span>


### <a name="prototype"></a><span data-ttu-id="cec97-642">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-642">Prototype</span></span>

```C
UINT nx_ip_address_change_notify(
    NX_IP *ip_ptr,
    VOID(*change_notify)(NX_IP *,VOID *),
    VOID *additional_info);
```

### <a name="description"></a><span data-ttu-id="cec97-643">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-643">Description</span></span>

<span data-ttu-id="cec97-644">Questo servizio registra una funzione di notifica dell'applicazione che viene chiamata ogni volta che viene modificato l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-644">This service registers an application notification function that is called whenever the IP address is changed.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-645">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-645">Parameters</span></span>

- <span data-ttu-id="cec97-646">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-646">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-647">**CHANGE_NOTIFY** Puntatore alla funzione di notifica della modifica IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-647">**change_notify** Pointer to IP change notification function.</span></span> <span data-ttu-id="cec97-648">Se questo parametro è NX_NULL, la notifica di modifica degli indirizzi IP è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-648">If this parameter is NX_NULL, IP address change notification is disabled.</span></span>
- <span data-ttu-id="cec97-649">**additional_info** Puntatore a informazioni aggiuntive facoltative fornite anche alla funzione di notifica quando viene modificato l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-649">**additional_info** Pointer to optional additional information that is also supplied to the notification function when the IP address is changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-650">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-650">Return Values</span></span>

- <span data-ttu-id="cec97-651">Notifica di modifica dell'indirizzo IP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-651">**NX_SUCCESS** (0x00) Successful IP address change notification.</span></span>
- <span data-ttu-id="cec97-652">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-652">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-653">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-653">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-654">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-654">Allowed From</span></span>

<span data-ttu-id="cec97-655">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-655">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-656">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-656">Preemption Possible</span></span>

<span data-ttu-id="cec97-657">No</span><span class="sxs-lookup"><span data-stu-id="cec97-657">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-658">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-658">Example</span></span>

```C
/* Register the function "my_ip_changed" to be called whenever
the IP address is changed. */
status = nx_ip_address_change_notify(&ip_0, my_ip_changed, NX_NULL);

/* If status is NX_SUCCESS, the "my_ip_changed" function will be
    called whenever the IP address changes. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-659">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-659">See Also</span></span>

- <span data-ttu-id="cec97-660">nx_ip_address_get, nx_ip_address_set, nx_ip_create, nx_ip_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-660">nx_ip_address_get, nx_ip_address_set, nx_ip_create, nx_ip_delete,</span></span>
- <span data-ttu-id="cec97-661">nx_ip_driver_direct_command, nx_ip_driver_interface_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-661">nx_ip_driver_direct_command, nx_ip_driver_interface_direct_command,</span></span>
- <span data-ttu-id="cec97-662">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-662">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span></span>
- <span data-ttu-id="cec97-663">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-663">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="cec97-664">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-664">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_address_get"></a><span data-ttu-id="cec97-665">nx_ip_address_get</span><span class="sxs-lookup"><span data-stu-id="cec97-665">nx_ip_address_get</span></span>

<span data-ttu-id="cec97-666">Recuperare l'indirizzo IP e la network mask</span><span class="sxs-lookup"><span data-stu-id="cec97-666">Retrieve IP address and network mask</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-667">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-667">Prototype</span></span>

```C
UINT nx_ip_address_get(
    NX_IP *ip_ptr,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a><span data-ttu-id="cec97-668">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-668">Description</span></span>

<span data-ttu-id="cec97-669">Questo servizio recupera l'indirizzo IP e il relativo subnet mask dell'interfaccia di rete primaria.</span><span class="sxs-lookup"><span data-stu-id="cec97-669">This service retrieves IP address and its subnet mask of the primary network interface.</span></span>

<span data-ttu-id="cec97-670">\* Per ottenere informazioni sul dispositivo secondario, usare il servizio</span><span class="sxs-lookup"><span data-stu-id="cec97-670">\*To obtain information of the secondary device, use the service</span></span>
- <span data-ttu-id="cec97-671">**nx_ip_interface_address_get**. \*</span><span class="sxs-lookup"><span data-stu-id="cec97-671">**nx_ip_interface_address_get**.\*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-672">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-672">Parameters</span></span>

- <span data-ttu-id="cec97-673">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-673">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-674">**ip_address** Puntatore alla destinazione per l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-674">**ip_address** Pointer to destination for IP address.</span></span>
- <span data-ttu-id="cec97-675">**network_mask** Puntatore alla destinazione per network mask.</span><span class="sxs-lookup"><span data-stu-id="cec97-675">**network_mask** Pointer to destination for network mask.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-676">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-676">Return Values</span></span>

- <span data-ttu-id="cec97-677">**NX_SUCCESS** (0x00) indirizzo IP riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="cec97-677">**NX_SUCCESS** (0x00) Successful IP address get.</span></span>
- <span data-ttu-id="cec97-678">**NX_PTR_ERROR** (0x07) indirizzo IP non valido o puntatore alla variabile restituita.</span><span class="sxs-lookup"><span data-stu-id="cec97-678">**NX_PTR_ERROR** (0x07) Invalid IP or return variable pointer.</span></span>
- <span data-ttu-id="cec97-679">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-679">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-680">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-680">Allowed From</span></span>

<span data-ttu-id="cec97-681">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-681">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-682">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-682">Preemption Possible</span></span>

<span data-ttu-id="cec97-683">No</span><span class="sxs-lookup"><span data-stu-id="cec97-683">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-684">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-684">Example</span></span>

```C
/* Get the IP address and network mask from the previously created
    IP Instance ip_0. */
status = nx_ip_address_get(&ip_0,
    &ip_address, &network_mask);

/* If status is NX_SUCCESS, the variables ip_address and
    network_mask contain the IP and network mask respectively. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-685">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-685">See Also</span></span>

- <span data-ttu-id="cec97-686">nx_ip_address_change_notify, nx_ip_address_set, nx_ip_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-686">nx_ip_address_change_notify, nx_ip_address_set, nx_ip_create,</span></span>
- <span data-ttu-id="cec97-687">nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-687">nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-688">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-688">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-689">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-689">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="cec97-690">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span><span class="sxs-lookup"><span data-stu-id="cec97-690">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span></span>
- <span data-ttu-id="cec97-691">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-691">nx_system_initialize</span></span>

## <a name="nx_ip_address_set"></a><span data-ttu-id="cec97-692">nx_ip_address_set</span><span class="sxs-lookup"><span data-stu-id="cec97-692">nx_ip_address_set</span></span>

<span data-ttu-id="cec97-693">Imposta indirizzo IP e network mask</span><span class="sxs-lookup"><span data-stu-id="cec97-693">Set IP address and network mask</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-694">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-694">Prototype</span></span>

```C
UINT nx_ip_address_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a><span data-ttu-id="cec97-695">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-695">Description</span></span>

<span data-ttu-id="cec97-696">Questo servizio imposta l'indirizzo IP e il network mask per l'interfaccia di rete primaria.</span><span class="sxs-lookup"><span data-stu-id="cec97-696">This service sets IP address and network mask for the primary network interface.</span></span>

<span data-ttu-id="cec97-697">*Per impostare l'indirizzo IP e il network mask per il dispositivo secondario, usare il **nx_ip_interface_address_set** del servizio.*</span><span class="sxs-lookup"><span data-stu-id="cec97-697">*To set IP address and network mask for the secondary device, use the service **nx_ip_interface_address_set**.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-698">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-698">Parameters</span></span>

- <span data-ttu-id="cec97-699">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-699">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-700">**ip_address** Nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-700">**ip_address** New IP address.</span></span>
- <span data-ttu-id="cec97-701">**network_mask** Nuovo network mask.</span><span class="sxs-lookup"><span data-stu-id="cec97-701">**network_mask** New network mask.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-702">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-702">Return Values</span></span>

- <span data-ttu-id="cec97-703">Set di indirizzi IP riusciti **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-703">**NX_SUCCESS** (0x00) Successful IP address set.</span></span>
- <span data-ttu-id="cec97-704">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-704">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-705">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-705">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-706">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-706">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-707">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-707">Allowed From</span></span>

<span data-ttu-id="cec97-708">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-708">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-709">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-709">Preemption Possible</span></span>

<span data-ttu-id="cec97-710">No</span><span class="sxs-lookup"><span data-stu-id="cec97-710">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-711">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-711">Example</span></span>

```C
/* Set the IP address and network mask to 1.2.3.4 and 0xFFFFFF00
    for the previously created IP Instance ip_0. */
status = nx_ip_address_set(&ip_0, IP_ADDRESS(1,2,3,4), 0xFFFFFF00UL);

/* If status is NX_SUCCESS, the IP instance now has an IP address
    of 1.2.3.4 and a network mask of 0xFFFFFF00. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-712">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-712">See Also</span></span>

- <span data-ttu-id="cec97-713">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-713">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_create,</span></span>
- <span data-ttu-id="cec97-714">nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-714">nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-715">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-715">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-716">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-716">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="cec97-717">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span><span class="sxs-lookup"><span data-stu-id="cec97-717">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span></span>
- <span data-ttu-id="cec97-718">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-718">nx_system_initialize</span></span>

## <a name="nx_ip_create"></a><span data-ttu-id="cec97-719">nx_ip_create</span><span class="sxs-lookup"><span data-stu-id="cec97-719">nx_ip_create</span></span>

<span data-ttu-id="cec97-720">Creare un'istanza IP</span><span class="sxs-lookup"><span data-stu-id="cec97-720">Create an IP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-721">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-721">Prototype</span></span>

```C
UINT nx_ip_create(
    NX_IP *ip_ptr, 
    CHAR *name, 
    ULONG ip_address,
    ULONG network_mask, 
    NX_PACKET_POOL *default_pool,
    VOID (*ip_network_driver)(NX_IP_DRIVER *),
    VOID *memory_ptr, 
    ULONG memory_size,
    UINT priority);
```

### <a name="description"></a><span data-ttu-id="cec97-722">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-722">Description</span></span>

<span data-ttu-id="cec97-723">Questo servizio crea un'istanza IP con l'indirizzo IP e il driver di rete specificati dall'utente.</span><span class="sxs-lookup"><span data-stu-id="cec97-723">This service creates an IP instance with the user supplied IP address and network driver.</span></span> <span data-ttu-id="cec97-724">Inoltre, l'applicazione deve fornire un pool di pacchetti creato in precedenza per l'istanza IP da usare per l'allocazione dei pacchetti interna.</span><span class="sxs-lookup"><span data-stu-id="cec97-724">In addition, the application must supply a previously created packet pool for the IP instance to use for internal packet allocation.</span></span> <span data-ttu-id="cec97-725">Si noti che il driver di rete dell'applicazione fornito non viene chiamato fino a quando non viene eseguito il thread di questo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-725">Note that the supplied application network driver is not called until this IP's thread executes.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-726">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-726">Parameters</span></span>

- <span data-ttu-id="cec97-727">**ip_ptr** Puntatore al blocco di controllo per creare una nuova istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-727">**ip_ptr** Pointer to control block to create a new IP instance.</span></span>
- <span data-ttu-id="cec97-728">**nome** Nome della nuova istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-728">**name** Name of this new IP instance.</span></span>
- <span data-ttu-id="cec97-729">**ip_address** Indirizzo IP per la nuova istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-729">**ip_address** IP address for this new IP instance.</span></span>
- <span data-ttu-id="cec97-730">**network_mask** Maschera per delineare la parte di rete dell'indirizzo IP per la suddivisione in subnet e l'uso di super-reti.</span><span class="sxs-lookup"><span data-stu-id="cec97-730">**network_mask** Mask to delineate the network portion of the IP address for sub-netting and super-netting uses.</span></span>
- <span data-ttu-id="cec97-731">**default_pool** Puntatore al blocco di controllo del pool di pacchetti NetX creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-731">**default_pool** Pointer to control block of previously created NetX packet pool.</span></span>
- <span data-ttu-id="cec97-732">**ip_network_driver** Driver di rete fornito dall'utente utilizzato per inviare e ricevere pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-732">**ip_network_driver** User-supplied network driver used to send and receive IP packets.</span></span>
- <span data-ttu-id="cec97-733">**memory_ptr** Puntatore all'area di memoria per l'area dello stack del thread helper IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-733">**memory_ptr** Pointer to memory area for the IP helper thread’s stack area.</span></span>
- <span data-ttu-id="cec97-734">**memory_size** Numero di byte nell'area di memoria per lo stack del thread helper IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-734">**memory_size** Number of bytes in the memory area for the IP helper thread’s stack.</span></span>
- <span data-ttu-id="cec97-735">**priorità** di Priorità del thread helper IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-735">**priority** Priority of IP helper thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-736">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-736">Return Values</span></span>
- <span data-ttu-id="cec97-737">Creazione dell'istanza IP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-737">**NX_SUCCESS** (0x00) Successful IP instance creation.</span></span>
- <span data-ttu-id="cec97-738">La libreria NetX **NX_NOT_IMPLEMENTED** (0x4A) non è configurata correttamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-738">**NX_NOT_IMPLEMENTED** (0x4A) NetX library is configured incorrectly.</span></span>
- <span data-ttu-id="cec97-739">**NX_PTR_ERROR** (0x07) IP non valido, puntatore alla funzione del driver di rete, pool di pacchetti o puntatore di memoria.</span><span class="sxs-lookup"><span data-stu-id="cec97-739">**NX_PTR_ERROR** (0x07) Invalid IP, network driver function pointer, packet pool, or memory pointer.</span></span>
- <span data-ttu-id="cec97-740">**NX_SIZE_ERROR** (0x09) la dimensione dello stack fornita è troppo piccola.</span><span class="sxs-lookup"><span data-stu-id="cec97-740">**NX_SIZE_ERROR** (0x09) The supplied stack size is too small.</span></span>
- <span data-ttu-id="cec97-741">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-741">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-742">**NX_IP_ADDRESS_ERROR** (0X21) l'indirizzo IP specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-742">**NX_IP_ADDRESS_ERROR** (0x21) The supplied IP address is invalid.</span></span>
- <span data-ttu-id="cec97-743">**NX_OPTION_ERROR** (0X21) la priorità del thread IP specificata non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-743">**NX_OPTION_ERROR** (0x21) The supplied IP thread priority is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-744">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-744">Allowed From</span></span>

<span data-ttu-id="cec97-745">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-745">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-746">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-746">Preemption Possible</span></span>

<span data-ttu-id="cec97-747">No</span><span class="sxs-lookup"><span data-stu-id="cec97-747">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-748">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-748">Example</span></span>

```C
/* Create an IP instance with an IP address of 1.2.3.4 and a network
    mask of 0xFFFFFF00UL. The "ethernet_driver" specifies the entry
    point of the application specific network driver and the
    "stack_memory_ptr" specifies the start of a 1024 byte memory
    area that is used for this IP instance’s helper thread.  */
status = nx_ip_create(
    &ip_0, 
    "NetX IP Instance ip_0",
    IP_ADDRESS(1, 2, 3, 4),
    0xFFFFFF00UL, &pool_0, 
    ethernet_driver,
    stack_memory_ptr, 
    1024, 
    1);

/* If status is NX_SUCCESS, the IP instance has been created. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-749">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-749">See Also</span></span>

- <span data-ttu-id="cec97-750">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-750">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-751">nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-751">nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-752">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-752">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-753">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-753">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="cec97-754">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span><span class="sxs-lookup"><span data-stu-id="cec97-754">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span></span>
- <span data-ttu-id="cec97-755">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-755">nx_system_initialize</span></span>

## <a name="nx_ip_delete"></a><span data-ttu-id="cec97-756">nx_ip_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-756">nx_ip_delete</span></span>

<span data-ttu-id="cec97-757">Elimina istanza IP creata in precedenza</span><span class="sxs-lookup"><span data-stu-id="cec97-757">Delete previously created IP instance</span></span>


### <a name="prototype"></a><span data-ttu-id="cec97-758">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-758">Prototype</span></span>

```C
UINT nx_ip_delete(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-759">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-759">Description</span></span>

<span data-ttu-id="cec97-760">Questo servizio Elimina un'istanza IP creata in precedenza e rilascia tutte le risorse di sistema di proprietà dell'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-760">This service deletes a previously created IP instance and releases all of the system resources owned by the IP instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-761">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-761">Parameters</span></span>
- <span data-ttu-id="cec97-762">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-762">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-763">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-763">Return Values</span></span>

- <span data-ttu-id="cec97-764">Eliminazione IP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-764">**NX_SUCCESS** (0x00) Successful IP deletion.</span></span>
- <span data-ttu-id="cec97-765">**NX_SOCKETS_BOUND** (0x28) a questa istanza IP sono ancora associati socket UDP o TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-765">**NX_SOCKETS_BOUND** (0x28) This IP instance still has UDP or TCP sockets bound to it.</span></span> <span data-ttu-id="cec97-766">Prima di eliminare l'istanza IP, è necessario che tutti i socket siano non associati ed eliminati.</span><span class="sxs-lookup"><span data-stu-id="cec97-766">All sockets must be unbound and deleted prior to deleting the IP instance.</span></span>
- <span data-ttu-id="cec97-767">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-767">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-768">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-768">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-769">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-769">Allowed From</span></span>

<span data-ttu-id="cec97-770">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-770">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-771">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-771">Preemption Possible</span></span>

<span data-ttu-id="cec97-772">Sì</span><span class="sxs-lookup"><span data-stu-id="cec97-772">Yes</span></span>

### <a name="example"></a><span data-ttu-id="cec97-773">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-773">Example</span></span>

```C
/* Delete a previously created IP instance. */
status = nx_ip_delete(&ip_0);

/* If status is NX_SUCCESS, the IP instance has been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-774">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-774">See Also</span></span>

- <span data-ttu-id="cec97-775">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-775">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-776">nx_ip_create, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-776">nx_ip_create, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-777">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-777">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-778">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-778">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="cec97-779">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span><span class="sxs-lookup"><span data-stu-id="cec97-779">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span></span>
- <span data-ttu-id="cec97-780">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-780">nx_system_initialize</span></span>

## <a name="nx_ip_driver_direct_command"></a><span data-ttu-id="cec97-781">nx_ip_driver_direct_command</span><span class="sxs-lookup"><span data-stu-id="cec97-781">nx_ip_driver_direct_command</span></span>

<span data-ttu-id="cec97-782">Invia comando al driver di rete</span><span class="sxs-lookup"><span data-stu-id="cec97-782">Issue command to network driver</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-783">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-783">Prototype</span></span>

```C
UINT nx_ip_driver_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    ULONG *return_value_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-784">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-784">Description</span></span>

<span data-ttu-id="cec97-785">Questo servizio fornisce un'interfaccia diretta al driver dell'interfaccia di rete primaria dell'applicazione specificato durante la chiamata di ***nx_ip_create*** .</span><span class="sxs-lookup"><span data-stu-id="cec97-785">This service provides a direct interface to the application's primary network interface driver specified during the ***nx_ip_create*** call.</span></span>

<span data-ttu-id="cec97-786">I comandi specifici dell'applicazione possono essere utilizzati per fornire un valore numerico maggiore o uguale a NX_LINK_USER_COMMAND.</span><span class="sxs-lookup"><span data-stu-id="cec97-786">Application-specific commands can be used providing their numeric value is greater than or equal to NX_LINK_USER_COMMAND.</span></span>

<span data-ttu-id="cec97-787">*Per eseguire il comando per il dispositivo secondario, usare il servizio **nx_ip_driver_interface_direct_command** .*</span><span class="sxs-lookup"><span data-stu-id="cec97-787">*To issue command for the secondary device, use the **nx_ip_driver_interface_direct_command** service.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-788">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-788">Parameters</span></span>

- <span data-ttu-id="cec97-789">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-789">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-790">**comando** Codice di comando numerico.</span><span class="sxs-lookup"><span data-stu-id="cec97-790">**command** Numeric command code.</span></span> <span data-ttu-id="cec97-791">I comandi standard vengono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-791">Standard commands are defined as follows:</span></span>

- <span data-ttu-id="cec97-792">NX_LINK_GET_STATUS (10)</span><span class="sxs-lookup"><span data-stu-id="cec97-792">NX_LINK_GET_STATUS (10)</span></span>
- <span data-ttu-id="cec97-793">NX_LINK_GET_SPEED (11)</span><span class="sxs-lookup"><span data-stu-id="cec97-793">NX_LINK_GET_SPEED (11)</span></span>
- <span data-ttu-id="cec97-794">NX_LINK_GET_DUPLEX_TYPE (12)</span><span class="sxs-lookup"><span data-stu-id="cec97-794">NX_LINK_GET_DUPLEX_TYPE (12)</span></span>
- <span data-ttu-id="cec97-795">NX_LINK_GET_ERROR_COUNT (13)</span><span class="sxs-lookup"><span data-stu-id="cec97-795">NX_LINK_GET_ERROR_COUNT (13)</span></span>
- <span data-ttu-id="cec97-796">NX_LINK_GET_RX_COUNT (14)</span><span class="sxs-lookup"><span data-stu-id="cec97-796">NX_LINK_GET_RX_COUNT (14)</span></span>
- <span data-ttu-id="cec97-797">NX_LINK_GET_TX_COUNT (15)</span><span class="sxs-lookup"><span data-stu-id="cec97-797">NX_LINK_GET_TX_COUNT (15)</span></span>
- <span data-ttu-id="cec97-798">NX_LINK_GET_ALLOC_ERRORS (16)</span><span class="sxs-lookup"><span data-stu-id="cec97-798">NX_LINK_GET_ALLOC_ERRORS (16)</span></span>
- <span data-ttu-id="cec97-799">NX_LINK_USER_COMMAND (50)</span><span class="sxs-lookup"><span data-stu-id="cec97-799">NX_LINK_USER_COMMAND (50)</span></span>

- <span data-ttu-id="cec97-800">**return_value_ptr** Puntatore alla variabile restituita nel chiamante.</span><span class="sxs-lookup"><span data-stu-id="cec97-800">**return_value_ptr** Pointer to return variable in the caller.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-801">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-801">Return Values</span></span>

- <span data-ttu-id="cec97-802">**NX_SUCCESS** (0x00) il comando diretto del driver di rete è riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-802">**NX_SUCCESS** (0x00) Successful network driver direct command.</span></span>
- <span data-ttu-id="cec97-803">Comando del driver di rete non gestito o non implementato **NX_UNHANDLED_COMMAND** (0x44).</span><span class="sxs-lookup"><span data-stu-id="cec97-803">**NX_UNHANDLED_COMMAND** (0x44) Unhandled or unimplemented network driver command.</span></span>
- <span data-ttu-id="cec97-804">**NX_PTR_ERROR** (0x07) un indirizzo IP o un puntatore al valore restituito non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-804">**NX_PTR_ERROR** (0x07) Invalid IP or return value pointer.</span></span>
- <span data-ttu-id="cec97-805">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-805">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-806">**NX_INVALID_INTERFACE** (0x4C) indice di interfaccia non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-806">**NX_INVALID_INTERFACE** (0x4C) Invalid interface index.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-807">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-807">Allowed From</span></span>

<span data-ttu-id="cec97-808">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-808">Threads</span></span>

- <span data-ttu-id="cec97-809">**Precedenza possibile**</span><span class="sxs-lookup"><span data-stu-id="cec97-809">**Preemption Possible**</span></span>

<span data-ttu-id="cec97-810">No</span><span class="sxs-lookup"><span data-stu-id="cec97-810">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-811">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-811">Example</span></span>

```C
/* Make a direct call to the application-specific network driver
    for the previously created IP instance. For this example, the
    network driver is interrogated for the link status. */
status = nx_ip_driver_direct_command(
    &ip_0, NX_LINK_GET_STATUS,
    &link_status);

/* If status is NX_SUCCESS, the link_status variable contains a
    NX_TRUE or NX_FALSE value representing the status of the
    physical link. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-812">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-812">See Also</span></span>

- <span data-ttu-id="cec97-813">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-813">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-814">nx_ip_create, nx_ip_delete, nx_ip_driver_interface_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-814">nx_ip_create, nx_ip_delete, nx_ip_driver_interface_direct_command,</span></span>
- <span data-ttu-id="cec97-815">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-815">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span></span>
- <span data-ttu-id="cec97-816">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-816">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="cec97-817">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-817">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_driver_interface_direct_command"></a><span data-ttu-id="cec97-818">nx_ip_driver_interface_direct_command</span><span class="sxs-lookup"><span data-stu-id="cec97-818">nx_ip_driver_interface_direct_command</span></span>

<span data-ttu-id="cec97-819">Invia comando al driver di rete</span><span class="sxs-lookup"><span data-stu-id="cec97-819">Issue command to network driver</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-820">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-820">Prototype</span></span>

```C
UINT nx_ip_driver_interface_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    UINT interface_index,
    ULONG *return_value_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-821">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-821">Description</span></span>

<span data-ttu-id="cec97-822">Questo servizio fornisce un comando diretto al driver di dispositivo di rete dell'applicazione nell'istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-822">This service provides a direct command to the application's network device driver in the IP instance.</span></span> <span data-ttu-id="cec97-823">I comandi specifici dell'applicazione possono essere utilizzati per fornire un valore numerico maggiore o uguale a *NX_LINK_USER_COMMAND*.</span><span class="sxs-lookup"><span data-stu-id="cec97-823">Application-specific commands can be used providing their numeric value is greater than or equal to *NX_LINK_USER_COMMAND*.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-824">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-824">Parameters</span></span>

- <span data-ttu-id="cec97-825">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-825">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-826">**comando** Codice di comando numerico.</span><span class="sxs-lookup"><span data-stu-id="cec97-826">**command** Numeric command code.</span></span> <span data-ttu-id="cec97-827">I comandi standard vengono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-827">Standard commands are defined as follows:</span></span>
- <span data-ttu-id="cec97-828">NX_LINK_GET_STATUS (10)</span><span class="sxs-lookup"><span data-stu-id="cec97-828">NX_LINK_GET_STATUS (10)</span></span>
- <span data-ttu-id="cec97-829">NX_LINK_GET_SPEED (11)</span><span class="sxs-lookup"><span data-stu-id="cec97-829">NX_LINK_GET_SPEED (11)</span></span>
- <span data-ttu-id="cec97-830">NX_LINK_GET_DUPLEX_TYPE (12)</span><span class="sxs-lookup"><span data-stu-id="cec97-830">NX_LINK_GET_DUPLEX_TYPE (12)</span></span>
- <span data-ttu-id="cec97-831">NX_LINK_GET_ERROR_COUNT (13)</span><span class="sxs-lookup"><span data-stu-id="cec97-831">NX_LINK_GET_ERROR_COUNT (13)</span></span>
- <span data-ttu-id="cec97-832">NX_LINK_GET_RX_COUNT (14)</span><span class="sxs-lookup"><span data-stu-id="cec97-832">NX_LINK_GET_RX_COUNT (14)</span></span>
- <span data-ttu-id="cec97-833">NX_LINK_GET_TX_COUNT (15)</span><span class="sxs-lookup"><span data-stu-id="cec97-833">NX_LINK_GET_TX_COUNT (15)</span></span>
- <span data-ttu-id="cec97-834">NX_LINK_GET_ALLOC_ERRORS (16)</span><span class="sxs-lookup"><span data-stu-id="cec97-834">NX_LINK_GET_ALLOC_ERRORS (16)</span></span>
- <span data-ttu-id="cec97-835">NX_LINK_USER_COMMAND (50)</span><span class="sxs-lookup"><span data-stu-id="cec97-835">NX_LINK_USER_COMMAND (50)</span></span>
- <span data-ttu-id="cec97-836">**interface_index** Indice dell'interfaccia di rete a cui deve essere inviato il comando.</span><span class="sxs-lookup"><span data-stu-id="cec97-836">**interface_index** Index of the network interface the command should be sent to.</span></span>
- <span data-ttu-id="cec97-837">**return_value_ptr** Puntatore alla variabile restituita nel chiamante.</span><span class="sxs-lookup"><span data-stu-id="cec97-837">**return_value_ptr** Pointer to return variable in the caller.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-838">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-838">Return Values</span></span>
- <span data-ttu-id="cec97-839">**NX_SUCCESS** (0x00) il comando diretto del driver di rete è riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-839">**NX_SUCCESS** (0x00) Successful network driver direct command.</span></span>
- <span data-ttu-id="cec97-840">Comando del driver di rete non gestito o non implementato **NX_UNHANDLED_COMMAND** (0x44).</span><span class="sxs-lookup"><span data-stu-id="cec97-840">**NX_UNHANDLED_COMMAND** (0x44) Unhandled or unimplemented network driver command.</span></span>
- <span data-ttu-id="cec97-841">Indice di interfaccia **NX_INVALID_INTERFACE** (0X4C) non valido</span><span class="sxs-lookup"><span data-stu-id="cec97-841">**NX_INVALID_INTERFACE** (0x4C) Invalid interface index</span></span>
- <span data-ttu-id="cec97-842">**NX_PTR_ERROR** (0x07) un indirizzo IP o un puntatore al valore restituito non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-842">**NX_PTR_ERROR** (0x07) Invalid IP or return value pointer.</span></span>
- <span data-ttu-id="cec97-843">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-843">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-844">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-844">Allowed From</span></span>

<span data-ttu-id="cec97-845">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-845">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-846">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-846">Preemption Possible</span></span>

<span data-ttu-id="cec97-847">No</span><span class="sxs-lookup"><span data-stu-id="cec97-847">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-848">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-848">Example</span></span>

```C
/* Make a direct call to the application-specific network driver
    for the previously created IP instance. For this example, the
    network driver is interrogated for the link status. */

/* Set the interface index to the primary device. */
UINT interface_index = 0;
    status = nx_ip_driver_interface_direct_command(&ip_0,
    NX_LINK_GET_STATUS,
    interface_index,
    &link_status);
/* If status is NX_SUCCESS, the link_status variable contains a
    NX_TRUE or NX_FALSE value representing the status of the
    physical link. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-849">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-849">See Also</span></span>

- <span data-ttu-id="cec97-850">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-850">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-851">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-851">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-852">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-852">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span></span>
- <span data-ttu-id="cec97-853">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-853">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="cec97-854">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-854">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_forwarding_disable"></a><span data-ttu-id="cec97-855">nx_ip_forwarding_disable</span><span class="sxs-lookup"><span data-stu-id="cec97-855">nx_ip_forwarding_disable</span></span>

<span data-ttu-id="cec97-856">Disabilitare l'invio di pacchetti IP</span><span class="sxs-lookup"><span data-stu-id="cec97-856">Disable IP packet forwarding</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-857">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-857">Prototype</span></span>

```C
UINT nx_ip_forwarding_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-858">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-858">Description</span></span>

<span data-ttu-id="cec97-859">Questo servizio Disabilita l'invio di pacchetti IP all'interno del componente NetX IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-859">This service disables forwarding IP packets inside the NetX IP component.</span></span> <span data-ttu-id="cec97-860">Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-860">On creation of the IP task, this service is automatically disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-861">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-861">Parameters</span></span>

- <span data-ttu-id="cec97-862">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-862">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-863">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-863">Return Values</span></span>

- <span data-ttu-id="cec97-864">**NX_SUCCESS** (0x00) la disabilitazione dell'invio IP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-864">**NX_SUCCESS** (0x00) Successful IP forwarding disable.</span></span>
- <span data-ttu-id="cec97-865">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-865">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-866">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-866">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-867">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-867">Allowed From</span></span>

<span data-ttu-id="cec97-868">Inizializzazione, thread, timer</span><span class="sxs-lookup"><span data-stu-id="cec97-868">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-869">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-869">Preemption Possible</span></span>

<span data-ttu-id="cec97-870">No</span><span class="sxs-lookup"><span data-stu-id="cec97-870">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-871">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-871">Example</span></span>

```C
/* Disable IP forwarding on this IP instance. */
status = nx_ip_forwarding_disable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been disabled on the
    previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-872">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-872">See Also</span></span>

- <span data-ttu-id="cec97-873">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-873">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-874">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-874">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-875">nx_ip_driver_interface_direct_command, nx_ip_forwarding_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-875">nx_ip_driver_interface_direct_command, nx_ip_forwarding_enable,</span></span>
- <span data-ttu-id="cec97-876">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-876">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="cec97-877">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-877">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_forwarding_enable"></a><span data-ttu-id="cec97-878">nx_ip_forwarding_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-878">nx_ip_forwarding_enable</span></span>

<span data-ttu-id="cec97-879">Abilita l'invio di pacchetti IP</span><span class="sxs-lookup"><span data-stu-id="cec97-879">Enable IP packet forwarding</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-880">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-880">Prototype</span></span>

```C
UINT nx_ip_forwarding_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-881">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-881">Description</span></span>

<span data-ttu-id="cec97-882">Questo servizio consente l'invio di pacchetti IP all'interno del componente NetX IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-882">This service enables forwarding IP packets inside the NetX IP component.</span></span> <span data-ttu-id="cec97-883">Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-883">On creation of the IP task, this service is automatically disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-884">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-884">Parameters</span></span>

- <span data-ttu-id="cec97-885">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-885">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-886">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-886">Return Values</span></span>
- <span data-ttu-id="cec97-887">**NX_SUCCESS** (0x00) abilitata per l'invio di indirizzi IP riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-887">**NX_SUCCESS** (0x00) Successful IP forwarding enable.</span></span>
- <span data-ttu-id="cec97-888">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-888">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-889">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-889">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-890">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-890">Allowed From</span></span>

<span data-ttu-id="cec97-891">Inizializzazione, thread, timer</span><span class="sxs-lookup"><span data-stu-id="cec97-891">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-892">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-892">Preemption Possible</span></span>

<span data-ttu-id="cec97-893">No</span><span class="sxs-lookup"><span data-stu-id="cec97-893">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-894">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-894">Example</span></span>

```C
/* Enable IP forwarding on this IP instance. */
status = nx_ip_forwarding_enable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been enabled on the
    previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-895">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-895">See Also</span></span>

- <span data-ttu-id="cec97-896">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-896">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-897">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-897">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-898">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-898">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-899">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-899">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="cec97-900">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-900">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_fragment_disable"></a><span data-ttu-id="cec97-901">nx_ip_fragment_disable</span><span class="sxs-lookup"><span data-stu-id="cec97-901">nx_ip_fragment_disable</span></span>

<span data-ttu-id="cec97-902">Disabilitare la frammentazione di pacchetti IP</span><span class="sxs-lookup"><span data-stu-id="cec97-902">Disable IP packet fragmenting</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-903">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-903">Prototype</span></span>

```C
UINT nx_ip_fragment_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-904">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-904">Description</span></span>

<span data-ttu-id="cec97-905">Questo servizio Disabilita la funzionalità di riassemblaggio e frammentazione di pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-905">This service disables IP packet fragmenting and reassembling functionality.</span></span> <span data-ttu-id="cec97-906">Per i pacchetti in attesa di essere riassemblati, questo servizio rilascia questi pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-906">For packets waiting to be reassembled, this service releases these packets.</span></span> <span data-ttu-id="cec97-907">Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-907">On creation of the IP task, this service is automatically disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-908">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-908">Parameters</span></span>

- <span data-ttu-id="cec97-909">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-909">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-910">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-910">Return Values</span></span>
- <span data-ttu-id="cec97-911">**NX_SUCCESS** (0x00) la disabilitazione del FRAMMENTo IP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-911">**NX_SUCCESS** (0x00) Successful IP fragment disable.</span></span>
- <span data-ttu-id="cec97-912">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-912">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-913">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-913">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-914">La frammentazione IP **NX_NOT_ENABLED** (0x14) non è abilitata nell'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-914">**NX_NOT_ENABLED** (0x14) IP Fragmentation is not enabled on the IP instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-915">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-915">Allowed From</span></span>

<span data-ttu-id="cec97-916">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-916">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-917">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-917">Preemption Possible</span></span>

<span data-ttu-id="cec97-918">No</span><span class="sxs-lookup"><span data-stu-id="cec97-918">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-919">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-919">Example</span></span>

```C
/* Disable IP fragmenting on this IP instance. */
status = nx_ip_fragment_disable(&ip_0);

/* If status is NX_SUCCESS, disables IP fragmenting on the
    previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-920">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-920">See Also</span></span>

- <span data-ttu-id="cec97-921">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-921">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-922">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-922">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-923">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-923">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-924">nx_ip_forwarding_enable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-924">nx_ip_forwarding_enable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="cec97-925">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-925">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_fragment_enable"></a><span data-ttu-id="cec97-926">nx_ip_fragment_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-926">nx_ip_fragment_enable</span></span>

<span data-ttu-id="cec97-927">Abilitare la frammentazione di pacchetti IP</span><span class="sxs-lookup"><span data-stu-id="cec97-927">Enable IP packet fragmenting</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-928">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-928">Prototype</span></span>

```C
UINT nx_ip_fragment_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-929">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-929">Description</span></span>

<span data-ttu-id="cec97-930">Questo servizio Abilita la funzionalità di frammentazione e riassemblaggio di pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-930">This service enables IP packet fragmenting and reassembling functionality.</span></span> <span data-ttu-id="cec97-931">Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-931">On creation of the IP task, this service is automatically disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-932">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-932">Parameters</span></span>

- <span data-ttu-id="cec97-933">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-933">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-934">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-934">Return Values</span></span>

- <span data-ttu-id="cec97-935">Abilitazione del frammento IP **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-935">**NX_SUCCESS** (0x00) Successful IP fragment enable.</span></span>
- <span data-ttu-id="cec97-936">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-936">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-937">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-937">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-938">Le funzionalità di frammentazione IP **NX_NOT_ENABLED** (0x14) non vengono compilate in NETX.</span><span class="sxs-lookup"><span data-stu-id="cec97-938">**NX_NOT_ENABLED** (0x14) IP Fragmentation features is not compiled into NetX.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-939">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-939">Allowed From</span></span>

<span data-ttu-id="cec97-940">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-940">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-941">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-941">Preemption Possible</span></span>

<span data-ttu-id="cec97-942">No</span><span class="sxs-lookup"><span data-stu-id="cec97-942">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-943">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-943">Example</span></span>

```C
/* Enable IP fragmenting on this IP instance. */
status = nx_ip_fragment_enable(&ip_0);

/* If status is NX_SUCCESS, IP fragmenting has been enabled on the
    previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-944">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-944">See Also</span></span>

- <span data-ttu-id="cec97-945">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-945">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-946">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-946">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-947">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-947">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-948">nx_ip_forwarding_enable, nx_ip_fragment_disable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-948">nx_ip_forwarding_enable, nx_ip_fragment_disable, nx_ip_info_get,</span></span>
- <span data-ttu-id="cec97-949">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-949">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_gateway_address_set"></a><span data-ttu-id="cec97-950">nx_ip_gateway_address_set</span><span class="sxs-lookup"><span data-stu-id="cec97-950">nx_ip_gateway_address_set</span></span>

<span data-ttu-id="cec97-951">Impostare l'indirizzo IP del gateway</span><span class="sxs-lookup"><span data-stu-id="cec97-951">Set Gateway IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-952">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-952">Prototype</span></span>

```C
UINT nx_ip_gateway_address_set(
    NX_IP *ip_ptr, 
    ULONG ip_address);
```

### <a name="description"></a><span data-ttu-id="cec97-953">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-953">Description</span></span>

<span data-ttu-id="cec97-954">Questo servizio imposta l'indirizzo IP del gateway IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-954">This service sets the IP gateway IP address.</span></span> <span data-ttu-id="cec97-955">Tutto il traffico fuori rete viene indirizzato a questo gateway per la trasmissione.</span><span class="sxs-lookup"><span data-stu-id="cec97-955">All out-of-network traffic are routed to this gateway for transmission.</span></span> <span data-ttu-id="cec97-956">Il gateway deve essere direttamente accessibile tramite una delle interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="cec97-956">The gateway must be directly accessible through one of the network interfaces.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-957">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-957">Parameters</span></span>

- <span data-ttu-id="cec97-958">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-958">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-959">**ip_address** Indirizzo IP del gateway.</span><span class="sxs-lookup"><span data-stu-id="cec97-959">**ip_address** IP address of the gateway.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-960">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-960">Return Values</span></span>

- <span data-ttu-id="cec97-961">**NX_SUCCESS** (0x00) set di indirizzi IP del gateway riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-961">**NX_SUCCESS** (0x00) Successful Gateway IP address set.</span></span>
- <span data-ttu-id="cec97-962">**NX_PTR_ERROR** (0x07) puntatore a istanza IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-962">**NX_PTR_ERROR** (0x07) Invalid IP instance pointer.</span></span>
- <span data-ttu-id="cec97-963">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-963">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-964">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-964">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-965">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-965">Allowed From</span></span>

<span data-ttu-id="cec97-966">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-966">Initialization, thread</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-967">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-967">Preemption Possible</span></span>

<span data-ttu-id="cec97-968">No</span><span class="sxs-lookup"><span data-stu-id="cec97-968">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-969">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-969">Example</span></span>

```C
/* Setup the Gateway address for previously created IP
    Instance ip_0. */
status = nx_ip_gateway_address_set(&ip_0, IP_ADDRESS(1,2,3,99));

/* If status is NX_SUCCESS, all out-of-network send requests are
    routed to 1.2.3.99. */
```
### <a name="see-also"></a><span data-ttu-id="cec97-970">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-970">See Also</span></span>

- <span data-ttu-id="cec97-971">nx_ip_info_get, nx_ip_static_route_add, nx_ip_static_route_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-971">nx_ip_info_get, nx_ip_static_route_add, nx_ip_static_route_delete</span></span>

## <a name="nx_ip_info_get"></a><span data-ttu-id="cec97-972">nx_ip_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-972">nx_ip_info_get</span></span>

<span data-ttu-id="cec97-973">Recuperare informazioni sulle attività IP</span><span class="sxs-lookup"><span data-stu-id="cec97-973">Retrieve information about IP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-974">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-974">Prototype</span></span>

```C
UINT nx_ip_info_get(
    NX_IP *ip_ptr,
    ULONG *ip_total_packets_sent,
    ULONG *ip_total_bytes_sent,
    ULONG *ip_total_packets_received,
    ULONG *ip_total_bytes_received,
    ULONG *ip_invalid_packets,
    ULONG *ip_receive_packets_dropped,
    ULONG *ip_receive_checksum_errors,
    ULONG *ip_send_packets_dropped,
    ULONG *ip_total_fragments_sent,
    ULONG *ip_total_fragments_received);
```

### <a name="description"></a><span data-ttu-id="cec97-975">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-975">Description</span></span>

<span data-ttu-id="cec97-976">Questo servizio recupera informazioni sulle attività IP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-976">This service retrieves information about IP activities for the specified IP instance.</span></span>

<span data-ttu-id="cec97-977">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-977">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-978">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-978">Parameters</span></span>

- <span data-ttu-id="cec97-979">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-979">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-980">**ip_total_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti IP inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-980">**ip_total_packets_sent** Pointer to destination for the total number of IP packets sent.</span></span>
- <span data-ttu-id="cec97-981">**ip_total_bytes_sent** Puntatore alla destinazione per il numero totale di byte inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-981">**ip_total_bytes_sent** Pointer to destination for the total number of bytes sent.</span></span>
- <span data-ttu-id="cec97-982">**ip_total_packets_received** Puntatore alla destinazione del numero totale di pacchetti di ricezione IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-982">**ip_total_packets_received** Pointer to destination of the total number of IP receive packets.</span></span>
- <span data-ttu-id="cec97-983">**ip_total_bytes_received** Puntatore alla destinazione del numero totale di byte IP ricevuti.</span><span class="sxs-lookup"><span data-stu-id="cec97-983">**ip_total_bytes_received** Pointer to destination of the total number of IP bytes received.</span></span>
- <span data-ttu-id="cec97-984">**ip_invalid_packets** Puntatore alla destinazione del numero totale di pacchetti IP non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-984">**ip_invalid_packets** Pointer to destination of the total number of invalid IP packets.</span></span>
- <span data-ttu-id="cec97-985">**ip_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione eliminati.</span><span class="sxs-lookup"><span data-stu-id="cec97-985">**ip_receive_packets_dropped** Pointer to destination of the total number of receive packets dropped.</span></span>
- <span data-ttu-id="cec97-986">**ip_receive_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum nei pacchetti di ricezione.</span><span class="sxs-lookup"><span data-stu-id="cec97-986">**ip_receive_checksum_errors** Pointer to destination of the total number of checksum errors in receive packets.</span></span>
- <span data-ttu-id="cec97-987">**ip_send_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di invio eliminati.</span><span class="sxs-lookup"><span data-stu-id="cec97-987">**ip_send_packets_dropped** Pointer to destination of the total number of send packets dropped.</span></span>
- <span data-ttu-id="cec97-988">**ip_total_fragments_sent** Puntatore alla destinazione del numero totale di frammenti inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-988">**ip_total_fragments_sent** Pointer to destination of the total number of fragments sent.</span></span>
- <span data-ttu-id="cec97-989">**ip_total_fragments_received** Puntatore alla destinazione del numero totale di frammenti ricevuti.</span><span class="sxs-lookup"><span data-stu-id="cec97-989">**ip_total_fragments_received** Pointer to destination of the total number of fragments received.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-990">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-990">Return Values</span></span>

- <span data-ttu-id="cec97-991">Il recupero delle informazioni IP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-991">**NX_SUCCESS** (0x00) Successful IP information retrieval.</span></span>
- <span data-ttu-id="cec97-992">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-992">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-993">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-993">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-994">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-994">Allowed From</span></span>

<span data-ttu-id="cec97-995">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-995">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-996">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-996">Preemption Possible</span></span>

<span data-ttu-id="cec97-997">No</span><span class="sxs-lookup"><span data-stu-id="cec97-997">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-998">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-998">Example</span></span>

```C
/* Retrieve IP information from previously created IP
Instance 0. */
status = nx_ip_info_get(&ip_0,
    &ip_total_packets_sent,
    &ip_total_bytes_sent,
    &ip_total_packets_received,
    &ip_total_bytes_received,
    &ip_invalid_packets,
    &ip_receive_packets_dropped,
    &ip_receive_checksum_errors,
    &ip_send_packets_dropped,
    &ip_total_fragments_sent,
    &ip_total_fragments_received);

/* If status is NX_SUCCESS, IP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-999">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-999">See Also</span></span>

- <span data-ttu-id="cec97-1000">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-1000">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-1001">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-1001">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-1002">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1002">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-1003">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1003">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="cec97-1004">nx_ip_fragment_enable, nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-1004">nx_ip_fragment_enable, nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_interface_address_get"></a><span data-ttu-id="cec97-1005">nx_ip_interface_address_get</span><span class="sxs-lookup"><span data-stu-id="cec97-1005">nx_ip_interface_address_get</span></span>

<span data-ttu-id="cec97-1006">Recuperare l'indirizzo IP dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="cec97-1006">Retrieve interface IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1007">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1007">Prototype</span></span>

```C
UINT nx_ip_interface_address_get (
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a><span data-ttu-id="cec97-1008">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1008">Description</span></span>

<span data-ttu-id="cec97-1009">Questo servizio recupera l'indirizzo IP di un'interfaccia di rete specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1009">This service retrieves the IP address of a specified network interface.</span></span>

<span data-ttu-id="cec97-1010">*Il dispositivo specificato, se non il dispositivo primario, deve essere precedentemente collegato all'istanza IP.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1010">*The specified device, if not the primary device, must be previously attached to the IP instance.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1011">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1011">Parameters</span></span>

- <span data-ttu-id="cec97-1012">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1012">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1013">**interface_index** Indice dell'interfaccia, lo stesso valore dell'indice per l'interfaccia di rete collegata all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1013">**interface_index** Interface index, the same value as the index to the network interface attached to the IP instance.</span></span>
- <span data-ttu-id="cec97-1014">**ip_address** Puntatore alla destinazione per l'indirizzo IP dell'interfaccia del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1014">**ip_address** Pointer to destination for the device interface IP address.</span></span>
- <span data-ttu-id="cec97-1015">**network_mask** Puntatore alla destinazione per l'interfaccia del dispositivo network mask.</span><span class="sxs-lookup"><span data-stu-id="cec97-1015">**network_mask** Pointer to destination for the device interface network mask.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1016">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1016">Return Values</span></span>

- <span data-ttu-id="cec97-1017">**NX_SUCCESS** (0x00) indirizzo IP riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="cec97-1017">**NX_SUCCESS** (0x00) Successful IP address get.</span></span>
- <span data-ttu-id="cec97-1018">L'interfaccia di rete specificata **NX_INVALID_INTERFACE** (0x4C) non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1018">**NX_INVALID_INTERFACE** (0x4C) Specified network interface is invalid.</span></span>
- <span data-ttu-id="cec97-1019">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1019">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1020">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1020">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1021">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1021">Allowed From</span></span>

<span data-ttu-id="cec97-1022">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1022">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1023">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1023">Preemption Possible</span></span>

<span data-ttu-id="cec97-1024">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1024">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1025">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1025">Example</span></span>

```C
#define INTERFACE_INDEX 1
/* Get device IP address and network mask for the specified
    interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_get(ip_ptr,INTERFACE_INDEX,
    &ip_address, &network_mask);

/* If status is NX_SUCCESS the interface address was successfully
    retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1026">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1026">See Also</span></span>

- <span data-ttu-id="cec97-1027">nx_ip_interface_address_set, nx_ip_interface_attach,</span><span class="sxs-lookup"><span data-stu-id="cec97-1027">nx_ip_interface_address_set, nx_ip_interface_attach,</span></span>
- <span data-ttu-id="cec97-1028">nx_ip_interface_info_get, nx_ip_interface_status_check,</span><span class="sxs-lookup"><span data-stu-id="cec97-1028">nx_ip_interface_info_get, nx_ip_interface_status_check,</span></span>
- <span data-ttu-id="cec97-1029">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-1029">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_interface_address_set"></a><span data-ttu-id="cec97-1030">nx_ip_interface_address_set</span><span class="sxs-lookup"><span data-stu-id="cec97-1030">nx_ip_interface_address_set</span></span>

<span data-ttu-id="cec97-1031">Impostare l'indirizzo IP e la network mask dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="cec97-1031">Set interface IP address and network mask</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1032">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1032">Prototype</span></span>

```C
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a><span data-ttu-id="cec97-1033">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1033">Description</span></span>

<span data-ttu-id="cec97-1034">Questo servizio imposta l'indirizzo IP e il network mask per l'interfaccia IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1034">This service sets the IP address and network mask for the specified IP interface.</span></span>

<span data-ttu-id="cec97-1035">*L'interfaccia specificata deve essere precedentemente collegata all'istanza IP.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1035">*The specified interface must be previously attached to the IP instance.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1036">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1036">Parameters</span></span>

- <span data-ttu-id="cec97-1037">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1037">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1038">**interface_index** Indice dell'interfaccia associata all'istanza di NetX.</span><span class="sxs-lookup"><span data-stu-id="cec97-1038">**interface_index** Index of the interface attached to the NetX instance.</span></span>
- <span data-ttu-id="cec97-1039">**ip_address** Nuovo indirizzo IP dell'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="cec97-1039">**ip_address** New network interface IP address.</span></span>
- <span data-ttu-id="cec97-1040">**network_mask** Nuova interfaccia network mask.</span><span class="sxs-lookup"><span data-stu-id="cec97-1040">**network_mask** New interface network mask.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1041">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1041">Return Values</span></span>

- <span data-ttu-id="cec97-1042">Set di indirizzi IP riusciti **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-1042">**NX_SUCCESS** (0x00) Successful IP address set.</span></span>
- <span data-ttu-id="cec97-1043">L'interfaccia di rete specificata **NX_INVALID_INTERFACE** (0x4C) non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1043">**NX_INVALID_INTERFACE** (0x4C) Specified network interface is invalid.</span></span>
- <span data-ttu-id="cec97-1044">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1044">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1045">**NX_PTR_ERROR** (0x07) puntatori non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-1045">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="cec97-1046">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido</span><span class="sxs-lookup"><span data-stu-id="cec97-1046">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1047">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1047">Allowed From</span></span>

<span data-ttu-id="cec97-1048">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1048">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1049">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1049">Preemption Possible</span></span>

<span data-ttu-id="cec97-1050">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1050">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1051">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1051">Example</span></span>

```C
#define INTERFACE_INDEX 1
/* Set device IP address and network mask for the specified
    interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_set(ip_ptr, INTERFACE_INDEX,
    ip_address, network_mask);

/* If status is NX_SUCCESS the interface IP address and mask was
successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1052">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1052">See Also</span></span>

- <span data-ttu-id="cec97-1053">nx_ip_interface_address_get, nx_ip_interface_attach,</span><span class="sxs-lookup"><span data-stu-id="cec97-1053">nx_ip_interface_address_get, nx_ip_interface_attach,</span></span>
- <span data-ttu-id="cec97-1054">nx_ip_interface_info_get, nx_ip_interface_status_check,</span><span class="sxs-lookup"><span data-stu-id="cec97-1054">nx_ip_interface_info_get, nx_ip_interface_status_check,</span></span>
- <span data-ttu-id="cec97-1055">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-1055">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_interface_attach"></a><span data-ttu-id="cec97-1056">nx_ip_interface_attach</span><span class="sxs-lookup"><span data-stu-id="cec97-1056">nx_ip_interface_attach</span></span>

<span data-ttu-id="cec97-1057">Collegare l'interfaccia di rete all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="cec97-1057">Attach network interface to IP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1058">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1058">Prototype</span></span>

```C
UINT nx_ip_interface_attach(
    NX_IP *ip_ptr, 
    CHAR *interface_name,
    ULONG ip_address,
    ULONG network_mask,
    VOID(*ip_link_driver)
    (struct NX_IP_DRIVER_STRUCT *));
```

### <a name="description"></a><span data-ttu-id="cec97-1059">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1059">Description</span></span>

<span data-ttu-id="cec97-1060">Questo servizio aggiunge un'interfaccia di rete fisica all'interfaccia IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1060">This service adds a physical network interface to the IP interface.</span></span> <span data-ttu-id="cec97-1061">Si noti che l'istanza IP viene creata con l'interfaccia primaria, quindi ogni interfaccia aggiuntiva è secondaria all'interfaccia primaria.</span><span class="sxs-lookup"><span data-stu-id="cec97-1061">Note the IP instance is created with the primary interface so each additional interface is secondary to the primary interface.</span></span> <span data-ttu-id="cec97-1062">Il numero totale di interfacce di rete collegate all'istanza IP (inclusa l'interfaccia primaria) non può superare **NX_MAX_PHYSICAL_INTERFACES**.</span><span class="sxs-lookup"><span data-stu-id="cec97-1062">The total number of network interfaces attached to the IP instance (including the primary interface) cannot exceed **NX_MAX_PHYSICAL_INTERFACES**.</span></span>

<span data-ttu-id="cec97-1063">Se il thread IP non è ancora in esecuzione, le interfacce secondarie verranno inizializzate come parte del processo di avvio del thread IP che inizializza tutte le interfacce fisiche.</span><span class="sxs-lookup"><span data-stu-id="cec97-1063">If the IP thread has not been running yet, the secondary interfaces will be initialized as part of the IP thread startup process that initializes all physical interfaces.</span></span>

<span data-ttu-id="cec97-1064">Se il thread IP non è ancora in esecuzione, l'interfaccia secondaria viene inizializzata come parte del servizio ***nx_ip_interface_attach*** .</span><span class="sxs-lookup"><span data-stu-id="cec97-1064">If the IP thread is not running yet, the secondary interface is initialized as part of the ***nx_ip_interface_attach*** service.</span></span>

<span data-ttu-id="cec97-1065">*ip_ptr deve puntare a una struttura IP NetX valida.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1065">*ip_ptr must point to a valid NetX IP structure.*</span></span>

- <span data-ttu-id="cec97-1066">*Per il numero di interfacce di rete per l'istanza IP, è necessario configurare **NX_MAX_PHYSICAL_INTERFACES** . Il valore predefinito è uno.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1066">***NX_MAX_PHYSICAL_INTERFACES** must be configured for the number of network interfaces for the IP instance. The default value is one.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1067">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1067">Parameters</span></span>

- <span data-ttu-id="cec97-1068">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1068">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1069">**INTERFACE_NAME** Puntatore alla stringa del nome di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="cec97-1069">**interface_name** Pointer to interface name string.</span></span>
- <span data-ttu-id="cec97-1070">**ip_address** Indirizzo IP del dispositivo nell'ordine dei byte dell'host.</span><span class="sxs-lookup"><span data-stu-id="cec97-1070">**ip_address** Device IP address in host byte order.</span></span>
- <span data-ttu-id="cec97-1071">**network_mask** Network mask del dispositivo nell'ordine dei byte dell'host.</span><span class="sxs-lookup"><span data-stu-id="cec97-1071">**network_mask** Device network mask in host byte order.</span></span>
- <span data-ttu-id="cec97-1072">**ip_link_driver** Driver Ethernet per l'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="cec97-1072">**ip_link_driver** Ethernet driver for the interface.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1073">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1073">Return Values</span></span>

- <span data-ttu-id="cec97-1074">La voce **NX_SUCCESS** (0x00) viene aggiunta alla tabella di routing statica.</span><span class="sxs-lookup"><span data-stu-id="cec97-1074">**NX_SUCCESS** (0x00) Entry is added to static routing table.</span></span>
- <span data-ttu-id="cec97-1075">Numero massimo di interfacce **NX_NO_MORE_ENTRIES** (0x17).</span><span class="sxs-lookup"><span data-stu-id="cec97-1075">**NX_NO_MORE_ENTRIES** (0x17) Max number of interfaces.</span></span>
- <span data-ttu-id="cec97-1076">Viene superato **NX_MAX_PHYSICAL_INTERFACES** .</span><span class="sxs-lookup"><span data-stu-id="cec97-1076">**NX_MAX_PHYSICAL_INTERFACES** is exceeded.</span></span>
- <span data-ttu-id="cec97-1077">**NX_DUPLICATED_ENTRY** (0X52) l'indirizzo IP specificato è già in uso in questa istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1077">**NX_DUPLICATED_ENTRY** (0x52) The supplied IP address is already used on this IP instance.</span></span>
- <span data-ttu-id="cec97-1078">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1078">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1079">L'input del puntatore **NX_PTR_ERROR** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1079">**NX_PTR_ERROR** (0x07) Invalid pointer input.</span></span>
- <span data-ttu-id="cec97-1080">**NX_IP_ADDRESS_ERROR** (0x21) l'input dell'indirizzo IP non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1080">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1081">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1081">Allowed From</span></span>

<span data-ttu-id="cec97-1082">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1082">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1083">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1083">Preemption Possible</span></span>

<span data-ttu-id="cec97-1084">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1084">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1085">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1085">Example</span></span>

```C
/* Attach secondary device for device IP address 192.168.1.68 with
    the specified Ethernet driver. */
status = nx_ip_interface_attach(ip_ptr, “secondary_port”,
    IP_ADDRESS(192,168,1,68),
    0xFFFFFF00UL,
    nx_etherDriver);
/* If status is NX_SUCCESS the interface was successfully added to
    the IP instance interface table. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1086">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1086">See Also</span></span>

- <span data-ttu-id="cec97-1087">nx_ip_interface_address_get, nx_ip_interface_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-1087">nx_ip_interface_address_get, nx_ip_interface_address_set,</span></span>
- <span data-ttu-id="cec97-1088">nx_ip_interface_info_get, nx_ip_interface_status_check,</span><span class="sxs-lookup"><span data-stu-id="cec97-1088">nx_ip_interface_info_get, nx_ip_interface_status_check,</span></span>
- <span data-ttu-id="cec97-1089">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-1089">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_interface_info_get"></a><span data-ttu-id="cec97-1090">nx_ip_interface_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-1090">nx_ip_interface_info_get</span></span>

<span data-ttu-id="cec97-1091">Recuperare i parametri dell'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="cec97-1091">Retrieve network interface parameters</span></span>


### <a name="prototype"></a><span data-ttu-id="cec97-1092">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1092">Prototype</span></span>

```C
UINT nx_ip_interface_info_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    CHAR **interface_name,
    ULONG *ip_address,
    ULONG *network_mask,
    ULONG *mtu_size,
    ULONG *physical_address_msw,
    ULONG *physical_address_lsw);
```

### <a name="description"></a><span data-ttu-id="cec97-1093">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1093">Description</span></span>

<span data-ttu-id="cec97-1094">Questo servizio recupera informazioni sui parametri di rete per l'interfaccia di rete specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1094">This service retrieves information on network parameters for the specified network interface.</span></span> <span data-ttu-id="cec97-1095">Tutti i dati vengono recuperati nell'ordine dei byte dell'host.</span><span class="sxs-lookup"><span data-stu-id="cec97-1095">All data are retrieved in host byte order.</span></span>

<span data-ttu-id="cec97-1096">*ip_ptr deve puntare a una struttura IP NetX valida. L'interfaccia specificata, se non l'interfaccia primaria, deve essere precedentemente collegata all'istanza IP.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1096">*ip_ptr must point to a valid NetX IP structure. The specified interface, if not the primary interface, must be previously attached to the IP instance.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1097">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1097">Parameters</span></span>

- <span data-ttu-id="cec97-1098">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1098">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1099">**interface_index** Indice che specifica l'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="cec97-1099">**interface_index** Index specifying network interface.</span></span>
- <span data-ttu-id="cec97-1100">**INTERFACE_NAME** Puntatore al buffer che include il nome dell'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="cec97-1100">**interface_name** Pointer to the buffer that holds the name of the network interface.</span></span>
- <span data-ttu-id="cec97-1101">**ip_address** Puntatore alla destinazione per l'indirizzo IP dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="cec97-1101">**ip_address** Pointer to the destination for the IP address of the interface.</span></span>
- <span data-ttu-id="cec97-1102">**network_mask** Puntatore alla destinazione per network mask.</span><span class="sxs-lookup"><span data-stu-id="cec97-1102">**network_mask** Pointer to destination for network mask.</span></span>
- <span data-ttu-id="cec97-1103">**mtu_size** Puntatore alla destinazione per l'unità di trasferimento massima per questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="cec97-1103">**mtu_size** Pointer to destination for maximum transfer unit for this interface.</span></span>
- <span data-ttu-id="cec97-1104">**physical_address_msw** Puntatore alla destinazione per i primi 16 bit dell'indirizzo MAC del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1104">**physical_address_msw** Pointer to destination for top 16 bits of the device MAC address.</span></span>
- <span data-ttu-id="cec97-1105">**physical_address_lsw** Puntatore alla destinazione per i 32 bit inferiori dell'indirizzo MAC del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1105">**physical_address_lsw** Pointer to destination for lower 32 bits of the device MAC address.</span></span>


### <a name="return-values"></a><span data-ttu-id="cec97-1106">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1106">Return Values</span></span>
- <span data-ttu-id="cec97-1107">Sono state ottenute le informazioni sull'interfaccia **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-1107">**NX_SUCCESS** (0x00) Interface information has been obtained.</span></span>
- <span data-ttu-id="cec97-1108">L'input del puntatore **NX_PTR_ERROR** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1108">**NX_PTR_ERROR** (0x07) Invalid pointer input.</span></span>
- <span data-ttu-id="cec97-1109">**NX_INVALID_INTERFACE** (0x4C) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1109">**NX_INVALID_INTERFACE** (0x4C) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-1110">Il servizio **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.</span><span class="sxs-lookup"><span data-stu-id="cec97-1110">**NX_CALLER_ERROR** (0x11) Service is not called from system initialization or thread context.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1111">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1111">Allowed From</span></span>

<span data-ttu-id="cec97-1112">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1112">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1113">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1113">Preemption Possible</span></span>

<span data-ttu-id="cec97-1114">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1114">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1115">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1115">Example</span></span>

```C
/* Retrieve interface parameters for the specified interface (index
    1 in IP instance list of interfaces). */
#define INTERFACE_INDEX 1

status = nx_ip_interface_info_get(ip_ptr, INTERFACE_INDEX,
    &name_ptr, &ip_address,
    &network_mask,
    &mtu_size,
    &physical_address_msw,
    &physical_address_lsw);

/* If status is NX_SUCCESS the interface information is
    successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1116">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1116">See Also</span></span>

- <span data-ttu-id="cec97-1117">nx_ip_interface_address_get, nx_ip_interface_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-1117">nx_ip_interface_address_get, nx_ip_interface_address_set,</span></span>
- <span data-ttu-id="cec97-1118">nx_ip_interface_attach, nx_ip_interface_status_check,</span><span class="sxs-lookup"><span data-stu-id="cec97-1118">nx_ip_interface_attach, nx_ip_interface_status_check,</span></span>
- <span data-ttu-id="cec97-1119">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-1119">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_interface_status_check"></a><span data-ttu-id="cec97-1120">nx_ip_interface_status_check</span><span class="sxs-lookup"><span data-stu-id="cec97-1120">nx_ip_interface_status_check</span></span>

<span data-ttu-id="cec97-1121">Controllare lo stato di un'istanza IP</span><span class="sxs-lookup"><span data-stu-id="cec97-1121">Check status of an IP instance</span></span>


### <a name="prototype"></a><span data-ttu-id="cec97-1122">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1122">Prototype</span></span>

```C
UINT nx_ip_interface_status_check(
    NX_IP *ip_ptr,
    UINT interface_index
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-1123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1123">Description</span></span>

<span data-ttu-id="cec97-1124">Questo servizio controlla ed eventualmente attende lo stato specificato dell'interfaccia di rete di un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1124">This service checks and optionally waits for the specified status of the network interface of a previously created IP instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1125">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1125">Parameters</span></span>

- <span data-ttu-id="cec97-1126">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1126">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1127">**interface_index** Numero di indice dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="cec97-1127">**interface_index** Interface index number</span></span>
- <span data-ttu-id="cec97-1128">**needed_status** Stato IP richiesto, definito in formato mappa di bit, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cec97-1128">**needed_status** IP status requested, defined in bit-map form as follows:</span></span>
    - <span data-ttu-id="cec97-1129">NX_IP_INITIALIZE_DONE (0x0001)</span><span class="sxs-lookup"><span data-stu-id="cec97-1129">NX_IP_INITIALIZE_DONE (0x0001)</span></span>
    - <span data-ttu-id="cec97-1130">NX_IP_ADDRESS_RESOLVED (0x0002)</span><span class="sxs-lookup"><span data-stu-id="cec97-1130">NX_IP_ADDRESS_RESOLVED (0x0002)</span></span>
    - <span data-ttu-id="cec97-1131">NX_IP_LINK_ENABLED (0x0004)</span><span class="sxs-lookup"><span data-stu-id="cec97-1131">NX_IP_LINK_ENABLED (0x0004)</span></span>
    - <span data-ttu-id="cec97-1132">NX_IP_ARP_ENABLED (0x0008)</span><span class="sxs-lookup"><span data-stu-id="cec97-1132">NX_IP_ARP_ENABLED (0x0008)</span></span>
    - <span data-ttu-id="cec97-1133">NX_IP_UDP_ENABLED (0x0010)</span><span class="sxs-lookup"><span data-stu-id="cec97-1133">NX_IP_UDP_ENABLED (0x0010)</span></span>
    - <span data-ttu-id="cec97-1134">NX_IP_TCP_ENABLED (0x0020)</span><span class="sxs-lookup"><span data-stu-id="cec97-1134">NX_IP_TCP_ENABLED (0x0020)</span></span>
    - <span data-ttu-id="cec97-1135">NX_IP_IGMP_ENABLED (0x0040)</span><span class="sxs-lookup"><span data-stu-id="cec97-1135">NX_IP_IGMP_ENABLED (0x0040)</span></span>
    - <span data-ttu-id="cec97-1136">NX_IP_RARP_COMPLETE (0x0080)</span><span class="sxs-lookup"><span data-stu-id="cec97-1136">NX_IP_RARP_COMPLETE (0x0080)</span></span>
    - <span data-ttu-id="cec97-1137">NX_IP_INTERFACE_LINK_ENABLED (0x0100)</span><span class="sxs-lookup"><span data-stu-id="cec97-1137">NX_IP_INTERFACE_LINK_ENABLED (0x0100)</span></span>
- <span data-ttu-id="cec97-1138">**actual_status** Puntatore alla destinazione del set di bit effettivo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1138">**actual_status** Pointer to destination of actual bits set.</span></span>
- <span data-ttu-id="cec97-1139">**WAIT_OPTION** Definisce il comportamento del servizio se i bit di stato richiesti non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="cec97-1139">**wait_option** Defines how the service behaves if the requested status bits are not available.</span></span> <span data-ttu-id="cec97-1140">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-1140">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="cec97-1141">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1141">NX_NO_WAIT (0x00000000)</span></span>
    - <span data-ttu-id="cec97-1142">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-1142">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="cec97-1143">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-1143">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1144">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1144">Return Values</span></span>

- <span data-ttu-id="cec97-1145">**NX_SUCCESS** (0x00) Verifica stato IP riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1145">**NX_SUCCESS** (0x00) Successful IP status check.</span></span>
- <span data-ttu-id="cec97-1146">La richiesta di stato **NX_NOT_SUCCESSFUL** (0x43) non è stata soddisfatta entro il timeout specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1146">**NX_NOT_SUCCESSFUL** (0x43) Status request was not satisfied within the timeout specified.</span></span>
- <span data-ttu-id="cec97-1147">Il puntatore IP **NX_PTR_ERROR** (0x07) è o è diventato non valido oppure il puntatore di stato effettivo non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1147">**NX_PTR_ERROR** (0x07) IP pointer is or has become invalid, or actual status pointer is invalid.</span></span>
- <span data-ttu-id="cec97-1148">**NX_OPTION_ERROR** (0x0A) opzione di stato necessaria non valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1148">**NX_OPTION_ERROR** (0x0a) Invalid needed status option.</span></span>
- <span data-ttu-id="cec97-1149">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1149">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1150">Il Interface_index **NX_INVALID_INTERFACE** (0x4C) non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1150">**NX_INVALID_INTERFACE** (0x4C) Interface_index is out of range.</span></span> <span data-ttu-id="cec97-1151">oppure l'interfaccia non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1151">or the interface is not valid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1152">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1152">Allowed From</span></span>

<span data-ttu-id="cec97-1153">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1153">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1154">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1154">Preemption Possible</span></span>

<span data-ttu-id="cec97-1155">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1155">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1156">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1156">Example</span></span>

```C
/* Wait 10 ticks for the link up status on the previously created IP
    instance. */
status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_LINK_ENABLED,
    &actual_status, 10);

/* If status is NX_SUCCESS, the secondary link for the specified IP
    instance is up. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1157">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1157">See Also</span></span>

- <span data-ttu-id="cec97-1158">nx_ip_interface_address_get, nx_ip_interface_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-1158">nx_ip_interface_address_get, nx_ip_interface_address_set,</span></span>
- <span data-ttu-id="cec97-1159">nx_ip_interface_attach, nx_ip_interface_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-1159">nx_ip_interface_attach, nx_ip_interface_info_get,</span></span>
- <span data-ttu-id="cec97-1160">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-1160">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_link_status_change_notify_set"></a><span data-ttu-id="cec97-1161">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-1161">nx_ip_link_status_change_notify_set</span></span>

<span data-ttu-id="cec97-1162">Impostare la funzione di callback notifica modifica stato collegamento</span><span class="sxs-lookup"><span data-stu-id="cec97-1162">Set the link status change notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1163">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1163">Prototype</span></span>

```C
UINT nx_ip_link_status_change_notify_set(
    NX_IP *ip_ptr,
    VOID (*link_status_change_notify)(NX_IP *ip_ptr, UINT interface_index, UINT link_up));
```

### <a name="description"></a><span data-ttu-id="cec97-1164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1164">Description</span></span>

<span data-ttu-id="cec97-1165">Questo servizio configura la funzione di callback notifica modifica stato collegamento.</span><span class="sxs-lookup"><span data-stu-id="cec97-1165">This service configures the link status change notify callback function.</span></span> <span data-ttu-id="cec97-1166">La routine di *link_status_change_notify* fornita dall'utente viene richiamata quando viene modificato lo stato dell'interfaccia primaria o secondaria, ad esempio se viene modificato l'indirizzo IP. Se *link_status_change_notify* è null, la funzionalità di callback notifica modifica stato collegamento è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1166">The user-supplied *link_status_change_notify* routine is invoked when either the primary or secondary interface status is changed (such as IP address is changed.) If *link_status_change_notify* is NULL, the link status change notify callback feature is disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1167">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1167">Parameters</span></span>

- <span data-ttu-id="cec97-1168">**ip_ptr** Puntatore del blocco di controllo IP</span><span class="sxs-lookup"><span data-stu-id="cec97-1168">**ip_ptr** IP control block pointer</span></span>
- <span data-ttu-id="cec97-1169">**link_status_change_notify** Funzione di callback fornita dall'utente da chiamare su una modifica all'interfaccia fisica.</span><span class="sxs-lookup"><span data-stu-id="cec97-1169">**link_status_change_notify** User-supplied callback function to be called upon a change to the physical interface.</span></span>


### <a name="return-values"></a><span data-ttu-id="cec97-1170">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1170">Return Values</span></span>

- <span data-ttu-id="cec97-1171">Set di **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="cec97-1171">**NX_SUCCESS** (0x00) Successful set</span></span>
- <span data-ttu-id="cec97-1172">**NX_PTR_ERROR** (0x07) puntatore a blocco di controllo IP non valido o nuovo puntatore a indirizzo fisico</span><span class="sxs-lookup"><span data-stu-id="cec97-1172">**NX_PTR_ERROR** (0x07) Invalid IP control block pointer or new physical address pointer</span></span>
- <span data-ttu-id="cec97-1173">Il servizio **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.</span><span class="sxs-lookup"><span data-stu-id="cec97-1173">**NX_CALLER_ERROR** (0x11) Service is not called from system initialization or thread context.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="cec97-1174">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1174">Allowed From</span></span>

<span data-ttu-id="cec97-1175">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1175">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1176">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1176">Preemption Possible</span></span>

<span data-ttu-id="cec97-1177">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1177">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1178">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1178">Example</span></span>

```C
/* Configure a callback function to be used when the physical
    interface status is changed. */
status = nx_ip_link_status_change_notify_set(&ip_0, my_change_cb);

/* If status == NX_SUCCESS, the link status change notify function
    is set. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1179">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1179">See Also</span></span>

- <span data-ttu-id="cec97-1180">nx_ip_interface_address_get, nx_ip_interface_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-1180">nx_ip_interface_address_get, nx_ip_interface_address_set,</span></span>
- <span data-ttu-id="cec97-1181">nx_ip_interface_attach, nx_ip_interface_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-1181">nx_ip_interface_attach, nx_ip_interface_info_get,</span></span>
- <span data-ttu-id="cec97-1182">nx_ip_interface_status_check</span><span class="sxs-lookup"><span data-stu-id="cec97-1182">nx_ip_interface_status_check</span></span>

## <a name="nx_ip_raw_packet_disable"></a><span data-ttu-id="cec97-1183">nx_ip_raw_packet_disable</span><span class="sxs-lookup"><span data-stu-id="cec97-1183">nx_ip_raw_packet_disable</span></span>

<span data-ttu-id="cec97-1184">Disabilitare l'invio/ricezione di pacchetti non elaborati</span><span class="sxs-lookup"><span data-stu-id="cec97-1184">Disable raw packet sending/receiving</span></span>


### <a name="prototype"></a><span data-ttu-id="cec97-1185">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1185">Prototype</span></span>

```C
UINT nx_ip_raw_packet_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1186">Description</span></span>

<span data-ttu-id="cec97-1187">Questo servizio Disabilita la trasmissione e la ricezione di pacchetti IP non elaborati per questa istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1187">This service disables transmission and reception of raw IP packets for this IP instance.</span></span> <span data-ttu-id="cec97-1188">Se il servizio pacchetti non elaborati è stato precedentemente abilitato e sono presenti pacchetti non elaborati nella coda di ricezione, il servizio rilascerà tutti i pacchetti non elaborati ricevuti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1188">If the raw packet service was previously enabled, and there are raw packets in the receive queue, this service will release any received raw packets.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1189">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1189">Parameters</span></span>

- <span data-ttu-id="cec97-1190">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1190">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1191">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1191">Return Values</span></span>

- <span data-ttu-id="cec97-1192">**NX_SUCCESS** (0x00) la disabilitazione del pacchetto non elaborato IP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1192">**NX_SUCCESS** (0x00) Successful IP raw packet disable.</span></span>
- <span data-ttu-id="cec97-1193">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1193">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-1194">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1194">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1195">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1195">Allowed From</span></span>

<span data-ttu-id="cec97-1196">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1196">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1197">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1197">Preemption Possible</span></span>

<span data-ttu-id="cec97-1198">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1198">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1199">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1199">Example</span></span>

```C
/* Disable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_disable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
    been disabled for the previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1200">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1200">See Also</span></span>

- <span data-ttu-id="cec97-1201">nx_ip_raw_packet_enable, nx_ip_raw_packet_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-1201">nx_ip_raw_packet_enable, nx_ip_raw_packet_receive,</span></span>
- <span data-ttu-id="cec97-1202">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="cec97-1202">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span></span>

## <a name="nx_ip_raw_packet_enable"></a><span data-ttu-id="cec97-1203">nx_ip_raw_packet_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-1203">nx_ip_raw_packet_enable</span></span>

<span data-ttu-id="cec97-1204">Abilita elaborazione pacchetti non elaborati</span><span class="sxs-lookup"><span data-stu-id="cec97-1204">Enable raw packet processing</span></span>


### <a name="prototype"></a><span data-ttu-id="cec97-1205">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1205">Prototype</span></span>

```C
UINT nx_ip_raw_packet_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1206">Description</span></span>

<span data-ttu-id="cec97-1207">Questo servizio consente la trasmissione e la ricezione di pacchetti IP non elaborati per questa istanza IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1207">This service enables transmission and reception of raw IP packets for this IP instance.</span></span> <span data-ttu-id="cec97-1208">I pacchetti TCP, UDP, ICMP e IGMP in ingresso vengono ancora elaborati da NetX.</span><span class="sxs-lookup"><span data-stu-id="cec97-1208">Incoming TCP, UDP, ICMP, and IGMP packets are still processed by NetX.</span></span> <span data-ttu-id="cec97-1209">I pacchetti con tipi di protocollo di livello superiore sconosciuti vengono elaborati dalla routine di ricezione dei pacchetti non elaborati.</span><span class="sxs-lookup"><span data-stu-id="cec97-1209">Packets with unknown upper layer protocol types are processed by raw packet reception routine.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1210">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1210">Parameters</span></span>

- <span data-ttu-id="cec97-1211">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1211">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1212">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1212">Return Values</span></span>

- <span data-ttu-id="cec97-1213">**NX_SUCCESS** (0x00) abilitata per i pacchetti non elaborati IP riusciti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1213">**NX_SUCCESS** (0x00) Successful IP raw packet enable.</span></span>
- <span data-ttu-id="cec97-1214">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1214">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-1215">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1215">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1216">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1216">Allowed From</span></span>

<span data-ttu-id="cec97-1217">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1217">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1218">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1218">Preemption Possible</span></span>

<span data-ttu-id="cec97-1219">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1219">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1220">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1220">Example</span></span>

```C
/* Enable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_enable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
    been enabled for the previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1221">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1221">See Also</span></span>

- <span data-ttu-id="cec97-1222">nx_ip_raw_packet_disable, nx_ip_raw_packet_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-1222">nx_ip_raw_packet_disable, nx_ip_raw_packet_receive,</span></span>
- <span data-ttu-id="cec97-1223">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="cec97-1223">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span></span>

## <a name="nx_ip_raw_packet_interface_send"></a><span data-ttu-id="cec97-1224">nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="cec97-1224">nx_ip_raw_packet_interface_send</span></span>

<span data-ttu-id="cec97-1225">Invia pacchetto IP non elaborato tramite l'interfaccia di rete specificata</span><span class="sxs-lookup"><span data-stu-id="cec97-1225">Send raw IP packet through specified network interface</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1226">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1226">Prototype</span></span>

```C
UINT nx_ip_raw_packet_interface_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    UINT address_index,
    ULONG type_of_service);
```

### <a name="description"></a><span data-ttu-id="cec97-1227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1227">Description</span></span>

<span data-ttu-id="cec97-1228">Questo servizio invia un pacchetto IP non elaborato all'indirizzo IP di destinazione utilizzando l'indirizzo IP locale specificato come indirizzo di origine e tramite l'interfaccia di rete associata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1228">This service sends a raw IP packet to the destination IP address using the specified local IP address as the source address, and through the associated network interface.</span></span> <span data-ttu-id="cec97-1229">Si noti che questa routine restituisce immediatamente un risultato e, pertanto, non è noto se il pacchetto IP è effettivamente stato inviato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1229">Note that this routine returns immediately, and it is, therefore, not known if the IP packet has actually been sent.</span></span> <span data-ttu-id="cec97-1230">Il driver di rete sarà responsabile del rilascio del pacchetto al termine della trasmissione.</span><span class="sxs-lookup"><span data-stu-id="cec97-1230">The network driver will be responsible for releasing the packet when the transmission is complete.</span></span> <span data-ttu-id="cec97-1231">Questo servizio differisce da altri servizi in quanto non esiste alcun modo per sapere se il pacchetto è stato effettivamente inviato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1231">This service differs from other services in that there is no way of knowing if the packet was actually sent.</span></span> <span data-ttu-id="cec97-1232">Potrebbe andare persa in Internet.</span><span class="sxs-lookup"><span data-stu-id="cec97-1232">It could get lost on the Internet.</span></span>

<span data-ttu-id="cec97-1233">*Si noti che è necessario abilitare l'elaborazione di indirizzi IP non elaborati.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1233">*Note that raw IP processing must be enabled.*</span></span>

<span data-ttu-id="cec97-1234">*Questo servizio è simile a **nx_ip_raw_packet_send**, ad eccezione del fatto che questo servizio consente a un'applicazione di inviare pacchetti IP non elaborati da un'interfaccia fisica specificata.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1234">*This service is similar to **nx_ip_raw_packet_send**, except that this service allows an application to send raw IP packet from a specified physical interfaces.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1235">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1235">Parameters</span></span>

- <span data-ttu-id="cec97-1236">**ip_ptr** Puntatore all'attività IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1236">**ip_ptr** Pointer to previously created IP task.</span></span>
- <span data-ttu-id="cec97-1237">**packet_ptr** Puntatore al pacchetto da trasmettere.</span><span class="sxs-lookup"><span data-stu-id="cec97-1237">**packet_ptr** Pointer to packet to transmit.</span></span>
- <span data-ttu-id="cec97-1238">**destination_ip** Indirizzo IP per l'invio del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1238">**destination_ip** IP address to send packet.</span></span>
- <span data-ttu-id="cec97-1239">**address_index** Indice dell'indirizzo dell'interfaccia su cui inviare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1239">**address_index** Index of the address of the interface to send packet out on.</span></span>
- <span data-ttu-id="cec97-1240">**Type_of_Service** Tipo di servizio per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1240">**type_of_service** Type of service for packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1241">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1241">Return Values</span></span>

- <span data-ttu-id="cec97-1242">Il pacchetto **NX_SUCCESS** (0x00) è stato trasmesso correttamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-1242">**NX_SUCCESS** (0x00) Packet successfully transmitted.</span></span>
- <span data-ttu-id="cec97-1243">**NX_IP_ADDRESS_ERROR** (0X21) non è disponibile alcuna interfaccia in uscita adatta.</span><span class="sxs-lookup"><span data-stu-id="cec97-1243">**NX_IP_ADDRESS_ERROR** (0x21) No suitable outgoing interface available.</span></span>
- <span data-ttu-id="cec97-1244">L'elaborazione dei pacchetti IP non elaborati **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1244">**NX_NOT_ENABLED** (0x14) Raw IP packet processing not enabled.</span></span>
- <span data-ttu-id="cec97-1245">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1245">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1246">L'input del puntatore **NX_PTR_ERROR** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1246">**NX_PTR_ERROR** (0x07) Invalid pointer input.</span></span>
- <span data-ttu-id="cec97-1247">Il tipo di servizio specificato **NX_OPTION_ERROR** (0X0A) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1247">**NX_OPTION_ERROR** (0x0A) Invalid type of service specified.</span></span>
- <span data-ttu-id="cec97-1248">**NX_OVERFLOW** (0x03) puntatore a anteporre il pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1248">**NX_OVERFLOW** (0x03) Invalid packet prepend pointer.</span></span>
- <span data-ttu-id="cec97-1249">**NX_UNDERFLOW** (0x02) puntatore a anteporre il pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1249">**NX_UNDERFLOW** (0x02) Invalid packet prepend pointer.</span></span>
- <span data-ttu-id="cec97-1250">**NX_INVALID_INTERFACE** (0x4C) è stato specificato un indice di interfaccia non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1250">**NX_INVALID_INTERFACE** (0x4C) Invalid interface index specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1251">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1251">Allowed From</span></span>

<span data-ttu-id="cec97-1252">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1252">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1253">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1253">Preemption Possible</span></span>

<span data-ttu-id="cec97-1254">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1254">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1255">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1255">Example</span></span>

```C
#define ADDRESS_IDNEX 1
/* Send packet out on interface 1 with normal type of service. */
status = nx_ip_raw_packet_interface_send(ip_ptr, packet_ptr,
    destination_ip,
    ADDRESS_INDEX,
    NX_IP_NORMAL);
/* If status is NX_SUCCESS the packet was successfully transmitted. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1256">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1256">See Also</span></span>

- <span data-ttu-id="cec97-1257">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1257">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span></span>
- <span data-ttu-id="cec97-1258">nx_ip_raw_packet_receive, nx_ip_raw_packet_send</span><span class="sxs-lookup"><span data-stu-id="cec97-1258">nx_ip_raw_packet_receive, nx_ip_raw_packet_send</span></span>

## <a name="nx_ip_raw_packet_receive"></a><span data-ttu-id="cec97-1259">nx_ip_raw_packet_receive</span><span class="sxs-lookup"><span data-stu-id="cec97-1259">nx_ip_raw_packet_receive</span></span>

<span data-ttu-id="cec97-1260">Ricevi pacchetto IP non elaborato</span><span class="sxs-lookup"><span data-stu-id="cec97-1260">Receive raw IP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1261">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1261">Prototype</span></span>

```C
UINT nx_ip_raw_packet_receive(
    NX_IP *ip_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-1262">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1262">Description</span></span>

<span data-ttu-id="cec97-1263">Questo servizio riceve un pacchetto IP non elaborato dall'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1263">This service receives a raw IP packet from the specified IP instance.</span></span> <span data-ttu-id="cec97-1264">Se nella coda di ricezione di pacchetti non elaborati sono presenti pacchetti IP, il primo pacchetto (meno recente) viene restituito al chiamante.</span><span class="sxs-lookup"><span data-stu-id="cec97-1264">If there are IP packets on the raw packet receive queue, the first (oldest) packet is returned to the caller.</span></span> <span data-ttu-id="cec97-1265">In caso contrario, se non sono disponibili pacchetti, il chiamante potrebbe sospendere come specificato dall'opzione wait.</span><span class="sxs-lookup"><span data-stu-id="cec97-1265">Otherwise, if no packets are available, the caller may suspend as specified by the wait option.</span></span>

<span data-ttu-id="cec97-1266">*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1266">*If NX_SUCCESS, is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1267">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1267">Parameters</span></span>

- <span data-ttu-id="cec97-1268">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1268">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1269">**packet_ptr** Puntatore al puntatore in cui inserire il pacchetto IP non elaborato ricevuto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1269">**packet_ptr** Pointer to pointer to place the received raw IP packet in.</span></span>
- <span data-ttu-id="cec97-1270">**WAIT_OPTION** Definisce il comportamento del servizio se non sono disponibili pacchetti IP non elaborati.</span><span class="sxs-lookup"><span data-stu-id="cec97-1270">**wait_option** Defines how the service behaves if there are no raw IP packets available.</span></span> <span data-ttu-id="cec97-1271">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-1271">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-1272">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1272">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-1273">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-1273">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-1274">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-1274">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1275">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1275">Return Values</span></span>

- <span data-ttu-id="cec97-1276">**NX_SUCCESS** (0x00) la ricezione di pacchetti non elaborati IP riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1276">**NX_SUCCESS** (0x00) Successful IP raw packet receive.</span></span>
- <span data-ttu-id="cec97-1277">**NX_NO_PACKET** (0x01) non è disponibile alcun pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1277">**NX_NO_PACKET** (0x01) No packet was available.</span></span>
- <span data-ttu-id="cec97-1278">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-1278">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-1279">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1279">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-1280">**NX_PTR_ERROR** (0x07) indirizzo IP non valido o puntatore al pacchetto restituito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1280">**NX_PTR_ERROR** (0x07) Invalid IP or return packet pointer.</span></span>
- <span data-ttu-id="cec97-1281">**NX_CALLER_ERROR** (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="cec97-1281">**NX_CALLER_ERROR** (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1282">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1282">Allowed From</span></span>

<span data-ttu-id="cec97-1283">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1283">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1284">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1284">Preemption Possible</span></span>

<span data-ttu-id="cec97-1285">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1285">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1286">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1286">Example</span></span>

```C
/* Receive a raw IP packet for this IP instance, wait for a maximum
    of 4 timer ticks. */
status = nx_ip_raw_packet_receive(&ip_0, &packet_ptr, 4);

/* If status is NX_SUCCESS, the raw IP packet pointer is in the
    variable packet_ptr. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1287">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1287">See Also</span></span>

- <span data-ttu-id="cec97-1288">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1288">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span></span>
- <span data-ttu-id="cec97-1289">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="cec97-1289">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span></span>

## <a name="nx_ip_raw_packet_send"></a><span data-ttu-id="cec97-1290">nx_ip_raw_packet_send</span><span class="sxs-lookup"><span data-stu-id="cec97-1290">nx_ip_raw_packet_send</span></span>

<span data-ttu-id="cec97-1291">Invia pacchetto IP non elaborato</span><span class="sxs-lookup"><span data-stu-id="cec97-1291">Send raw IP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1292">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1292">Prototype</span></span>

```C
UINT nx_ip_raw_packet_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    ULONG type_of_service);
```

### <a name="description"></a><span data-ttu-id="cec97-1293">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1293">Description</span></span>

<span data-ttu-id="cec97-1294">Questo servizio invia un pacchetto IP non elaborato all'indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-1294">This service sends a raw IP packet to the destination IP address.</span></span> <span data-ttu-id="cec97-1295">Si noti che questa routine viene restituita immediatamente e non è quindi noto se il pacchetto IP è stato effettivamente inviato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1295">Note that this routine returns immediately, and it is therefore not known whether the IP packet has actually been sent.</span></span> <span data-ttu-id="cec97-1296">Il driver di rete sarà responsabile del rilascio del pacchetto al termine della trasmissione.</span><span class="sxs-lookup"><span data-stu-id="cec97-1296">The network driver will be responsible for releasing the packet when the transmission is complete.</span></span>

<span data-ttu-id="cec97-1297">Per un sistema multihome, NetX usa l'indirizzo IP di destinazione per trovare un'interfaccia di rete appropriata e usa l'indirizzo IP dell'interfaccia come indirizzo di origine.</span><span class="sxs-lookup"><span data-stu-id="cec97-1297">For a multihome system, NetX uses the destination IP address to find an appropriate network interface and uses the IP address of the interface as the source address.</span></span> <span data-ttu-id="cec97-1298">Se l'indirizzo IP di destinazione è broadcast o multicast, viene utilizzata la prima interfaccia valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1298">If the destination IP address is broadcast or multicast, the first valid interface is used.</span></span> <span data-ttu-id="cec97-1299">In questo caso, le applicazioni usano la ***nx_ip_raw_packet_interface_send*** .</span><span class="sxs-lookup"><span data-stu-id="cec97-1299">Applications use the ***nx_ip_raw_packet_interface_send*** in this case.</span></span>

<span data-ttu-id="cec97-1300">*A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete rilascerà il pacchetto dopo la trasmissione.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1300">*Unless an error is returned, the application should not release the packet after this call. Doing so will cause unpredictable results because the network driver will release the packet after transmission.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1301">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1301">Parameters</span></span>

- <span data-ttu-id="cec97-1302">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1302">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1303">**packet_ptr** Puntatore al pacchetto IP non elaborato da inviare.</span><span class="sxs-lookup"><span data-stu-id="cec97-1303">**packet_ptr** Pointer to the raw IP packet to send.</span></span>
- <span data-ttu-id="cec97-1304">**destination_ip** Indirizzo IP di destinazione, che può essere un indirizzo IP host specifico, una trasmissione di rete, un ciclo interno o un indirizzo multicast.</span><span class="sxs-lookup"><span data-stu-id="cec97-1304">**destination_ip** Destination IP address, which can be a specific host IP address, a network broadcast, an internal loop-back, or a multicast address.</span></span>
- <span data-ttu-id="cec97-1305">**Type_of_Service** Definisce il tipo di servizio per la trasmissione. i valori validi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="cec97-1305">**type_of_service** Defines the type of service for the transmission, legal values are as follows:</span></span>
- <span data-ttu-id="cec97-1306">NX_IP_NORMAL (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1306">NX_IP_NORMAL (0x00000000)</span></span>
- <span data-ttu-id="cec97-1307">NX_IP_MIN_DELAY (0x00100000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1307">NX_IP_MIN_DELAY (0x00100000)</span></span>
- <span data-ttu-id="cec97-1308">NX_IP_MAX_DATA (0x00080000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1308">NX_IP_MAX_DATA (0x00080000)</span></span>
- <span data-ttu-id="cec97-1309">NX_IP_MAX_RELIABLE (0x00040000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1309">NX_IP_MAX_RELIABLE (0x00040000)</span></span>
- <span data-ttu-id="cec97-1310">NX_IP_MIN_COST (0x00020000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1310">NX_IP_MIN_COST (0x00020000)</span></span>


### <a name="return-values"></a><span data-ttu-id="cec97-1311">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1311">Return Values</span></span>

- <span data-ttu-id="cec97-1312">È stata avviata l'operazione di invio di pacchetti non elaborati non elaborati (0x00) **NX_SUCCESS**</span><span class="sxs-lookup"><span data-stu-id="cec97-1312">**NX_SUCCESS** (0x00) Successful IP raw packet send initiated.</span></span>
- <span data-ttu-id="cec97-1313">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1313">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-1314">La funzionalità IP raw **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1314">**NX_NOT_ENABLED** (0x14) Raw IP feature is not enabled.</span></span>
- <span data-ttu-id="cec97-1315">Il tipo di servizio **NX_OPTION_ERROR** (0X0A) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1315">**NX_OPTION_ERROR** (0x0A) Invalid type of service.</span></span>
- <span data-ttu-id="cec97-1316">**NX_UNDERFLOW** (0x02) spazio insufficiente per anteporre un'intestazione IP al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1316">**NX_UNDERFLOW** (0x02) Not enough room to prepend an IP header on the packet.</span></span>
- <span data-ttu-id="cec97-1317">Il puntatore di aggiunta del pacchetto **NX_OVERFLOW** (0x03) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1317">**NX_OVERFLOW** (0x03) Packet append pointer is invalid.</span></span>
- <span data-ttu-id="cec97-1318">**NX_PTR_ERROR** (0x07) un puntatore IP o di pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1318">**NX_PTR_ERROR** (0x07) Invalid IP or packet pointer.</span></span>
- <span data-ttu-id="cec97-1319">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1319">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1320">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1320">Allowed From</span></span>

<span data-ttu-id="cec97-1321">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1321">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1322">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1322">Preemption Possible</span></span>

<span data-ttu-id="cec97-1323">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1323">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1324">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1324">Example</span></span>

```C
/* Send a raw IP packet to IP address 1.2.3.5. */
status = nx_ip_raw_packet_send(&ip_0, packet_ptr,
    IP_ADDRESS(1,2,3,5),
    NX_IP_NORMAL);

/* If status is NX_SUCCESS, the raw IP packet pointed to by
    packet_ptr has been sent. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1325">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1325">See Also</span></span>

- <span data-ttu-id="cec97-1326">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1326">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span></span>
- <span data-ttu-id="cec97-1327">nx_ip_raw_packet_receive, nx_ip_raw_packet_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-1327">nx_ip_raw_packet_receive, nx_ip_raw_packet_send,</span></span>
- <span data-ttu-id="cec97-1328">nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="cec97-1328">nx_ip_raw_packet_interface_send</span></span>

## <a name="nx_ip_static_route_add"></a><span data-ttu-id="cec97-1329">nx_ip_static_route_add</span><span class="sxs-lookup"><span data-stu-id="cec97-1329">nx_ip_static_route_add</span></span>

<span data-ttu-id="cec97-1330">Aggiungere una route statica alla tabella di routing</span><span class="sxs-lookup"><span data-stu-id="cec97-1330">Add static route to the routing table</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1331">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1331">Prototype</span></span>

```C
UINT nx_ip_static_route_add(
    NX_IP *ip_ptr,
    ULONG network_address,
    ULONG net_mask,
    ULONG next_hop);
```

### <a name="description"></a><span data-ttu-id="cec97-1332">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1332">Description</span></span>

<span data-ttu-id="cec97-1333">Questo servizio aggiunge una voce alla tabella di routing statica.</span><span class="sxs-lookup"><span data-stu-id="cec97-1333">This service adds an entry to the static routing table.</span></span> <span data-ttu-id="cec97-1334">Si noti che l'indirizzo di *next_hop* deve essere direttamente accessibile da uno dei dispositivi di rete locali.</span><span class="sxs-lookup"><span data-stu-id="cec97-1334">Note that the *next_hop* address must be directly accessible from one of the local network devices.</span></span>

<span data-ttu-id="cec97-1335">*Si noti che ip_ptr necessario puntare a una struttura IP NetX valida e che la libreria NetX deve essere compilata con NX_ENABLE_IP_STATIC_ROUTING definito per l'uso di questo servizio. Per impostazione predefinita, NetX viene compilato senza NX_ENABLE_IP_STATIC_ROUTING definito.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1335">*Note that ip_ptr must point to a valid NetX IP structure and the NetX library must be built with NX_ENABLE_IP_STATIC_ROUTING defined to use this service. By default NetX is built without NX_ENABLE_IP_STATIC_ROUTING defined.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1336">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1336">Parameters</span></span>

- <span data-ttu-id="cec97-1337">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1337">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1338">**Network_Address** Indirizzo di rete di destinazione, in ordine byte host</span><span class="sxs-lookup"><span data-stu-id="cec97-1338">**network_address** Target network address, in host byte order</span></span>
- <span data-ttu-id="cec97-1339">**net_mask** Network mask di destinazione, in ordine byte host</span><span class="sxs-lookup"><span data-stu-id="cec97-1339">**net_mask** Target network mask, in host byte order</span></span>
- <span data-ttu-id="cec97-1340">**next_hop** Indirizzo hop successivo per la rete di destinazione, in ordine byte host</span><span class="sxs-lookup"><span data-stu-id="cec97-1340">**next_hop** Next hop address for the target network, in host byte order</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1341">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1341">Return Values</span></span>

- <span data-ttu-id="cec97-1342">La voce **NX_SUCCESS** (0x00) viene aggiunta alla tabella di routing statica.</span><span class="sxs-lookup"><span data-stu-id="cec97-1342">**NX_SUCCESS** (0x00) Entry is added to the static routing table.</span></span>
- <span data-ttu-id="cec97-1343">La tabella di routing statica **NX_OVERFLOW** (0x03) è piena.</span><span class="sxs-lookup"><span data-stu-id="cec97-1343">**NX_OVERFLOW** (0x03) Static routing table is full.</span></span>
- <span data-ttu-id="cec97-1344">**NX_NOT_SUPPORTED** (0X4B) questa funzionalità non è compilata in.</span><span class="sxs-lookup"><span data-stu-id="cec97-1344">**NX_NOT_SUPPORTED** (0x4B) This feature is not compiled in.</span></span>
- <span data-ttu-id="cec97-1345">L'hop successivo **NX_IP_ADDRESS_ERROR** (0x21) non è direttamente accessibile tramite interfacce locali.</span><span class="sxs-lookup"><span data-stu-id="cec97-1345">**NX_IP_ADDRESS_ERROR** (0x21) Next hop is not directly accessible via local interfaces.</span></span>
- <span data-ttu-id="cec97-1346">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1346">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1347">**NX_PTR_ERROR** (0x07) Ip_ptr puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1347">**NX_PTR_ERROR** (0x07) Invalid ip_ptr pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1348">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1348">Allowed From</span></span>

<span data-ttu-id="cec97-1349">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1349">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1350">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1350">Preemption Possible</span></span>

<span data-ttu-id="cec97-1351">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1351">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1352">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1352">Example</span></span>

```C
/* Specify the next hop for the 192.168.10.0 through the gateway
    192.168.1.1. */
status = nx_ip_static_route_add(ip_ptr, IP_ADDRESS(192,168,10,0),
    0xFFFFFF00UL,
    IP_ADDRESS(192,168,1,1));

/* If status is NX_SUCCESS the route was successfully added to the
    static routing table. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1353">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1353">See Also</span></span>

- <span data-ttu-id="cec97-1354">nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-1354">nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_delete</span></span>

## <a name="nx_ip_static_route_delete"></a><span data-ttu-id="cec97-1355">nx_ip_static_route_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-1355">nx_ip_static_route_delete</span></span>

<span data-ttu-id="cec97-1356">Elimina route statica dalla tabella di routing</span><span class="sxs-lookup"><span data-stu-id="cec97-1356">Delete static route from routing table</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1357">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1357">Prototype</span></span>

```C
UINT nx_ip_static_route_delete(
    NX_IP *ip_ptr,
    ULONG network_address, 
    ULONG net_mask);
```

### <a name="description"></a><span data-ttu-id="cec97-1358">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1358">Description</span></span>

<span data-ttu-id="cec97-1359">Questo servizio Elimina una voce dalla tabella di routing statica.</span><span class="sxs-lookup"><span data-stu-id="cec97-1359">This service deletes an entry from the static routing table.</span></span>

<span data-ttu-id="cec97-1360">*Si noti che ip_ptr necessario puntare a una struttura IP NetX valida e che la libreria NetX deve essere compilata con NX_ENABLE_IP_STATIC_ROUTING definito per l'uso di questo servizio. Per impostazione predefinita, NetX viene compilato senza NX_ENABLE_IP_STATIC_ROUTING definito.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1360">*Note that ip_ptr must point to a valid NetX IP structure and the NetX library must be built with NX_ENABLE_IP_STATIC_ROUTING defined to use this service. By default NetX is built without NX_ENABLE_IP_STATIC_ROUTING defined.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1361">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1361">Parameters</span></span>

- <span data-ttu-id="cec97-1362">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1362">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1363">**Network_Address** Indirizzo di rete di destinazione, in ordine byte host.</span><span class="sxs-lookup"><span data-stu-id="cec97-1363">**network_address** Target network address, in host byte order.</span></span>
- <span data-ttu-id="cec97-1364">**net_mask** Network mask di destinazione, in ordine byte host.</span><span class="sxs-lookup"><span data-stu-id="cec97-1364">**net_mask** Target network mask, in host byte order.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1365">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1365">Allowed From</span></span>

<span data-ttu-id="cec97-1366">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1366">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1367">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1367">Preemption Possible</span></span>

<span data-ttu-id="cec97-1368">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1368">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1369">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1369">Example</span></span>

```C
/* Remove the static route for 192.168.10.0 from the routing table.*/
status = nx_ip_static_route_delete(ip_ptr,
    IP_ADDRESS(192,168,10,0), 0xFFFFFF00UL,);

/* If status is NX_SUCCESS the route was successfully removed from
    the static routing table. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1370">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1370">See Also</span></span>

- <span data-ttu-id="cec97-1371">nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_add</span><span class="sxs-lookup"><span data-stu-id="cec97-1371">nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_add</span></span>

## <a name="nx_ip_status_check"></a><span data-ttu-id="cec97-1372">nx_ip_status_check</span><span class="sxs-lookup"><span data-stu-id="cec97-1372">nx_ip_status_check</span></span>

<span data-ttu-id="cec97-1373">Controllare lo stato di un'istanza IP</span><span class="sxs-lookup"><span data-stu-id="cec97-1373">Check status of an IP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1374">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1374">Prototype</span></span>

```C
UINT nx_ip_status_check(
    NX_IP *ip_ptr,
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-1375">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1375">Description</span></span>

<span data-ttu-id="cec97-1376">Questo servizio controlla ed eventualmente attende lo stato specificato dell'interfaccia di rete primaria di un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1376">This service checks and optionally waits for the specified status of the primary network interface of a previously created IP instance.</span></span> <span data-ttu-id="cec97-1377">Per ottenere lo stato sulle interfacce secondarie, le applicazioni devono utilizzare il servizio ***nx_ip_interface_status_check.***</span><span class="sxs-lookup"><span data-stu-id="cec97-1377">To obtain status on secondary interfaces, applications shall use the service ***nx_ip_interface_status_check.***</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1378">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1378">Parameters</span></span>

- <span data-ttu-id="cec97-1379">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1379">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1380">**needed_status** Stato IP richiesto, definito in formato mappa di bit, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cec97-1380">**needed_status** IP status requested, defined in bit-map form as follows:</span></span>
- <span data-ttu-id="cec97-1381">NX_IP_INITIALIZE_DONE (0x0001)</span><span class="sxs-lookup"><span data-stu-id="cec97-1381">NX_IP_INITIALIZE_DONE (0x0001)</span></span>
- <span data-ttu-id="cec97-1382">NX_IP_ADDRESS_RESOLVED (0x0002)</span><span class="sxs-lookup"><span data-stu-id="cec97-1382">NX_IP_ADDRESS_RESOLVED (0x0002)</span></span>
- <span data-ttu-id="cec97-1383">NX_IP_LINK_ENABLED (0x0004)</span><span class="sxs-lookup"><span data-stu-id="cec97-1383">NX_IP_LINK_ENABLED (0x0004)</span></span>
- <span data-ttu-id="cec97-1384">NX_IP_ARP_ENABLED (0x0008)</span><span class="sxs-lookup"><span data-stu-id="cec97-1384">NX_IP_ARP_ENABLED (0x0008)</span></span>
- <span data-ttu-id="cec97-1385">NX_IP_UDP_ENABLED (0x0010)</span><span class="sxs-lookup"><span data-stu-id="cec97-1385">NX_IP_UDP_ENABLED (0x0010)</span></span>
- <span data-ttu-id="cec97-1386">NX_IP_TCP_ENABLED (0x0020)</span><span class="sxs-lookup"><span data-stu-id="cec97-1386">NX_IP_TCP_ENABLED (0x0020)</span></span>
- <span data-ttu-id="cec97-1387">NX_IP_IGMP_ENABLED (0x0040)</span><span class="sxs-lookup"><span data-stu-id="cec97-1387">NX_IP_IGMP_ENABLED (0x0040)</span></span>
- <span data-ttu-id="cec97-1388">NX_IP_RARP_COMPLETE (0x0080)</span><span class="sxs-lookup"><span data-stu-id="cec97-1388">NX_IP_RARP_COMPLETE (0x0080)</span></span>
- <span data-ttu-id="cec97-1389">NX_IP_INTERFACE_LINK_ENABLED (0x0100)</span><span class="sxs-lookup"><span data-stu-id="cec97-1389">NX_IP_INTERFACE_LINK_ENABLED (0x0100)</span></span>
- <span data-ttu-id="cec97-1390">**actual_status** Puntatore alla destinazione del set di bit effettivo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1390">**actual_status** Pointer to destination of actual bits set.</span></span>
- <span data-ttu-id="cec97-1391">**WAIT_OPTION** Definisce il comportamento del servizio se i bit di stato richiesti non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="cec97-1391">**wait_option** Defines how the service behaves if the requested status bits are not available.</span></span> <span data-ttu-id="cec97-1392">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-1392">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-1393">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1393">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-1394">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-1394">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-1395">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-1395">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1396">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1396">Return Values</span></span>

- <span data-ttu-id="cec97-1397">**NX_SUCCESS** (0x00) Verifica stato IP riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1397">**NX_SUCCESS** (0x00) Successful IP status check.</span></span>
- <span data-ttu-id="cec97-1398">La richiesta di stato **NX_NOT_SUCCESSFUL** (0x43) non è stata soddisfatta entro il timeout specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1398">**NX_NOT_SUCCESSFUL** (0x43) Status request was not satisfied within the timeout specified.</span></span>
- <span data-ttu-id="cec97-1399">Il puntatore IP **NX_PTR_ERROR** (0x07) è o è diventato non valido oppure il puntatore di stato effettivo non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1399">**NX_PTR_ERROR** (0x07) IP pointer is or has become invalid, or actual status pointer is invalid.</span></span>
- <span data-ttu-id="cec97-1400">**NX_OPTION_ERROR** (0x0A) opzione di stato necessaria non valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1400">**NX_OPTION_ERROR** (0x0a) Invalid needed status option.</span></span>
- <span data-ttu-id="cec97-1401">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1401">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1402">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1402">Allowed From</span></span>

<span data-ttu-id="cec97-1403">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1403">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1404">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1404">Preemption Possible</span></span>

<span data-ttu-id="cec97-1405">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1405">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1406">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1406">Example</span></span>

```C
/* Wait 10 ticks for the link up status on the previously created IP
    instance. */
status = nx_ip_status_check(&ip_0, NX_IP_LINK_ENABLED,
    &actual_status, 10);

/* If status is NX_SUCCESS, the link for the specified IP instance
    is up. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1407">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1407">See Also</span></span>

- <span data-ttu-id="cec97-1408">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-1408">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-1409">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-1409">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-1410">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1410">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-1411">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1411">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="cec97-1412">nx_ip_fragment_enable, nx_ip_info_get, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-1412">nx_ip_fragment_enable, nx_ip_info_get, nx_system_initialize</span></span>

## <a name="nx_packet_allocate"></a><span data-ttu-id="cec97-1413">nx_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="cec97-1413">nx_packet_allocate</span></span>

<span data-ttu-id="cec97-1414">Alloca pacchetto dal pool specificato</span><span class="sxs-lookup"><span data-stu-id="cec97-1414">Allocate packet from specified pool</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1415">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1415">Prototype</span></span>

```C
UINT nx_packet_allocate(
    NX_PACKET_POOL *pool_ptr,
    NX_PACKET **packet_ptr,
    ULONG packet_type,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-1416">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1416">Description</span></span>

<span data-ttu-id="cec97-1417">Questo servizio alloca un pacchetto dal pool specificato e regola il puntatore anteposto nel pacchetto in base al tipo di pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1417">This service allocates a packet from the specified pool and adjusts the prepend pointer in the packet according to the type of packet specified.</span></span> <span data-ttu-id="cec97-1418">Se non è disponibile alcun pacchetto, il servizio viene sospeso in base all'opzione wait specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1418">If no packet is available, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1419">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1419">Parameters</span></span>

- <span data-ttu-id="cec97-1420">**pool_ptr** Puntatore al pool di pacchetti creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1420">**pool_ptr** Pointer to previously created packet pool.</span></span>
- <span data-ttu-id="cec97-1421">**packet_ptr** Puntatore al puntatore del puntatore del pacchetto allocato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1421">**packet_ptr** Pointer to the pointer of the allocated packet pointer.</span></span>
- <span data-ttu-id="cec97-1422">**packet_type** Definisce il tipo di pacchetto richiesto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1422">**packet_type** Defines the type of packet requested.</span></span> <span data-ttu-id="cec97-1423">Per un elenco dei tipi di pacchetti supportati, vedere "pool di pacchetti" nella pagina 49 del capitolo 3.</span><span class="sxs-lookup"><span data-stu-id="cec97-1423">See “Packet Pools” on page 49 in Chapter 3 for a list of supported packet types.</span></span>
- <span data-ttu-id="cec97-1424">**WAIT_OPTION** Definisce il tempo di attesa in cicli se non sono disponibili pacchetti nel pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1424">**wait_option** Defines the wait time in ticks if there are no packets available in the packet pool.</span></span> <span data-ttu-id="cec97-1425">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-1425">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-1426">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1426">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-1427">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-1427">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-1428">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-1428">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1429">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1429">Return Values</span></span>

- <span data-ttu-id="cec97-1430">**NX_SUCCESS** (0x00) allocare il pacchetto correttamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-1430">**NX_SUCCESS** (0x00) Successful packet allocate.</span></span>
- <span data-ttu-id="cec97-1431">**NX_NO_PACKET** (0x01) non è disponibile alcun pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1431">**NX_NO_PACKET** (0x01) No packet available.</span></span>
- <span data-ttu-id="cec97-1432">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-1432">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-1433">Le dimensioni del pacchetto **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non supportano il protocollo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1433">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="cec97-1434">Il tipo di pacchetto **NX_OPTION_ERROR** (0X0A) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1434">**NX_OPTION_ERROR** (0x0A) Invalid packet type.</span></span>
- <span data-ttu-id="cec97-1435">**NX_PTR_ERROR** (0x07) il pool o il puntatore di ritorno al pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1435">**NX_PTR_ERROR** (0x07) Invalid pool or packet return pointer.</span></span>
- <span data-ttu-id="cec97-1436">**NX_CALLER_ERROR** (0x11) opzione di attesa non valida da un thread non.</span><span class="sxs-lookup"><span data-stu-id="cec97-1436">**NX_CALLER_ERROR** (0x11) Invalid wait option from nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1437">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1437">Allowed From</span></span>

<span data-ttu-id="cec97-1438">Inizializzazione, thread, timer e ISRs (driver di rete dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="cec97-1438">Initialization, threads, timers, and ISRs (application network drivers).</span></span> <span data-ttu-id="cec97-1439">L'opzione wait deve essere NX_NO_WAIT quando viene usata in ISR o nel contesto del timer.</span><span class="sxs-lookup"><span data-stu-id="cec97-1439">Wait option must be NX_NO_WAIT when used in ISR or in timer context.</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1440">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1440">Preemption Possible</span></span>

<span data-ttu-id="cec97-1441">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1441">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1442">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1442">Example</span></span>

```C
/* Allocate a new UDP packet from the previously created packet pool
    and suspend for a maximum of 5 timer ticks if the pool is
    empty. */
status = nx_packet_allocate(&pool_0, &packet_ptr, NX_UDP_PACKET, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is
    found in the variable packet_ptr. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1443">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1443">See Also</span></span>

- <span data-ttu-id="cec97-1444">nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1444">nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1445">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="cec97-1445">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="cec97-1446">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-1446">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="cec97-1447">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="cec97-1447">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="cec97-1448">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1448">nx_packet_transmit_release</span></span>

## <a name="nx_packet_copy"></a><span data-ttu-id="cec97-1449">nx_packet_copy</span><span class="sxs-lookup"><span data-stu-id="cec97-1449">nx_packet_copy</span></span>

<span data-ttu-id="cec97-1450">Copia pacchetto</span><span class="sxs-lookup"><span data-stu-id="cec97-1450">Copy packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1451">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1451">Prototype</span></span>

```C
UINT nx_packet_copy(
    NX_PACKET *packet_ptr,
    NX_PACKET **new_packet_ptr,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-1452">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1452">Description</span></span>

<span data-ttu-id="cec97-1453">Questo servizio Copia le informazioni del pacchetto fornito in uno o più nuovi pacchetti allocati dal pool di pacchetti fornito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1453">This service copies the information in the supplied packet to one or more new packets that are allocated from the supplied packet pool.</span></span> <span data-ttu-id="cec97-1454">In caso di esito positivo, il puntatore al nuovo pacchetto viene restituito nella destinazione a cui punta **new_packet_ptr**.</span><span class="sxs-lookup"><span data-stu-id="cec97-1454">If successful, the pointer to the new packet is returned in destination pointed to by **new_packet_ptr**.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1455">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1455">Parameters</span></span>

- <span data-ttu-id="cec97-1456">**packet_ptr** Puntatore al pacchetto di origine.</span><span class="sxs-lookup"><span data-stu-id="cec97-1456">**packet_ptr** Pointer to the source packet.</span></span>
- <span data-ttu-id="cec97-1457">**new_packet_ptr** Puntatore alla destinazione di dove restituire il puntatore alla nuova copia del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1457">**new_packet_ptr** Pointer to the destination of where to return the pointer to the new copy of the packet.</span></span>
- <span data-ttu-id="cec97-1458">**pool_ptr** Puntatore al pool di pacchetti creato in precedenza usato per allocare uno o più pacchetti per la copia.</span><span class="sxs-lookup"><span data-stu-id="cec97-1458">**pool_ptr** Pointer to the previously created packet pool that is used to allocate one or more packets for the copy.</span></span>
- <span data-ttu-id="cec97-1459">**WAIT_OPTION** Definisce il modo in cui il servizio resta in attesa se non sono disponibili pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1459">**wait_option** Defines how the service waits if there are no packets available.</span></span> <span data-ttu-id="cec97-1460">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-1460">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-1461">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1461">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-1462">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-1462">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-1463">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-1463">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1464">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1464">Return Values</span></span>
- <span data-ttu-id="cec97-1465">**NX_SUCCESS** (0x00) copia di pacchetti riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1465">**NX_SUCCESS** (0x00) Successful packet copy.</span></span>
- <span data-ttu-id="cec97-1466">Il pacchetto **NX_NO_PACKET** (0x01) non è disponibile per la copia.</span><span class="sxs-lookup"><span data-stu-id="cec97-1466">**NX_NO_PACKET** (0x01) Packet not available for copy.</span></span>
- <span data-ttu-id="cec97-1467">Il pacchetto o la copia di origine vuota **NX_INVALID_PACKET** (0x12) non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1467">**NX_INVALID_PACKET** (0x12) Empty source packet or copy failed.</span></span>
- <span data-ttu-id="cec97-1468">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-1468">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-1469">Le dimensioni del pacchetto **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non supportano il protocollo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1469">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="cec97-1470">**NX_PTR_ERROR** (0x07) un pool, un pacchetto o un puntatore di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1470">**NX_PTR_ERROR** (0x07) Invalid pool, packet, or destination pointer.</span></span>
- <span data-ttu-id="cec97-1471">**NX_UNDERFLOW** (0x02) puntatore a anteporre il pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1471">**NX_UNDERFLOW** (0x02) Invalid packet prepend pointer.</span></span>
- <span data-ttu-id="cec97-1472">**NX_OVERFLOW** (0x03) puntatore di Accodamento pacchetti non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1472">**NX_OVERFLOW** (0x03) Invalid packet append pointer.</span></span>
- <span data-ttu-id="cec97-1473">**NX_CALLER_ERROR** (0x11) è stata specificata un'opzione Wait nell'inizializzazione o in un ISR.</span><span class="sxs-lookup"><span data-stu-id="cec97-1473">**NX_CALLER_ERROR** (0x11) A wait option was specified in initialization or in an ISR.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1474">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1474">Allowed From</span></span>

<span data-ttu-id="cec97-1475">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="cec97-1475">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1476">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1476">Preemption Possible</span></span>

<span data-ttu-id="cec97-1477">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1477">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1478">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1478">Example</span></span>

```C
NX_PACKET *new_copy_ptr;

/* Copy packet pointed to by "old_packet_ptr" using packets from
    previously created packet pool_0. */
status = nx_packet_copy(old_packet, &new_copy_ptr, &pool_0, 20);

/* If status is NX_SUCCESS, new_copy_ptr points to the packet copy. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1479">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1479">See Also</span></span>

- <span data-ttu-id="cec97-1480">nx_packet_allocate, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1480">nx_packet_allocate, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1481">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="cec97-1481">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="cec97-1482">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-1482">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="cec97-1483">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="cec97-1483">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="cec97-1484">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1484">nx_packet_transmit_release</span></span>

## <a name="nx_packet_data_append"></a><span data-ttu-id="cec97-1485">nx_packet_data_append</span><span class="sxs-lookup"><span data-stu-id="cec97-1485">nx_packet_data_append</span></span>

<span data-ttu-id="cec97-1486">Accoda dati alla fine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="cec97-1486">Append data to end of packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1487">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1487">Prototype</span></span>

```C
UINT nx_packet_data_append(
    NX_PACKET *packet_ptr,
    VOID *data_start, 
    ULONG data_size,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-1488">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1488">Description</span></span>

<span data-ttu-id="cec97-1489">Questo servizio aggiunge i dati alla fine del pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1489">This service appends data to the end of the specified packet.</span></span> <span data-ttu-id="cec97-1490">L'area dati fornita viene copiata nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1490">The supplied data area is copied into the packet.</span></span> <span data-ttu-id="cec97-1491">Se la memoria disponibile non è sufficiente e la funzionalità per i pacchetti concatenati è abilitata, per soddisfare la richiesta verranno allocati uno o più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1491">If there is not enough memory available, and the chained packet feature is enabled, one or more packets will be allocated to satisfy the request.</span></span> <span data-ttu-id="cec97-1492">Se la funzionalità di pacchetto concatenato non è abilitata, viene restituito *NX_SIZE_ERROR* .</span><span class="sxs-lookup"><span data-stu-id="cec97-1492">If the chained packet feature is not enabled, *NX_SIZE_ERROR* is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1493">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1493">Parameters</span></span>

- <span data-ttu-id="cec97-1494">**packet_ptr** Puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1494">**packet_ptr** Packet pointer.</span></span>
- <span data-ttu-id="cec97-1495">**DATA_START** Puntatore all'inizio dell'area dati dell'utente da accodare al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1495">**data_start** Pointer to the start of the user’s data area to append to the packet.</span></span>
- <span data-ttu-id="cec97-1496">**DATA_SIZE** Dimensioni dell'area dati dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cec97-1496">**data_size** Size of user’s data area.</span></span>
- <span data-ttu-id="cec97-1497">**pool_ptr** Puntatore al pool di pacchetti da cui allocare un altro pacchetto se non c'è spazio sufficiente nel pacchetto corrente.</span><span class="sxs-lookup"><span data-stu-id="cec97-1497">**pool_ptr** Pointer to packet pool from which to allocate another packet if there is not enough room in the current packet.</span></span>
- <span data-ttu-id="cec97-1498">**WAIT_OPTION** Definisce il comportamento del servizio se non sono disponibili pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1498">**wait_option** Defines how the service behaves if there are no packets available.</span></span> <span data-ttu-id="cec97-1499">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-1499">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-1500">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1500">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-1501">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-1501">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-1502">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-1502">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1503">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1503">Return Values</span></span>

- <span data-ttu-id="cec97-1504">**NX_SUCCESS** (0x00) Accodamento pacchetti riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1504">**NX_SUCCESS** (0x00) Successful packet append.</span></span>
- <span data-ttu-id="cec97-1505">**NX_NO_PACKET** (0x01) non è disponibile alcun pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1505">**NX_NO_PACKET** (0x01) No packet available.</span></span>
- <span data-ttu-id="cec97-1506">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al *tx_thread_wait_abort*.</span><span class="sxs-lookup"><span data-stu-id="cec97-1506">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="cec97-1507">Le dimensioni del pacchetto **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non supportano il protocollo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1507">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="cec97-1508">Il puntatore **NX_UNDERFLOW** (0x02) Prepend è inferiore all'avvio del payload.</span><span class="sxs-lookup"><span data-stu-id="cec97-1508">**NX_UNDERFLOW** (0x02) Prepend pointer is less than payload start.</span></span>
- <span data-ttu-id="cec97-1509">Il puntatore di Accodamento **NX_OVERFLOW** (0x03) è maggiore della fine del payload.</span><span class="sxs-lookup"><span data-stu-id="cec97-1509">**NX_OVERFLOW** (0x03) Append pointer is greater than payload end.</span></span>
- <span data-ttu-id="cec97-1510">**NX_PTR_ERROR** (0x07) il pool, il pacchetto o il puntatore ai dati non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1510">**NX_PTR_ERROR** (0x07) Invalid pool, packet, or data Pointer.</span></span>
- <span data-ttu-id="cec97-1511">Dimensioni dei dati **NX_SIZE_ERROR** (0x09) non valide.</span><span class="sxs-lookup"><span data-stu-id="cec97-1511">**NX_SIZE_ERROR** (0x09) Invalid data size.</span></span>
- <span data-ttu-id="cec97-1512">**NX_CALLER_ERROR** (0x11) opzione di attesa non valida da un thread non.</span><span class="sxs-lookup"><span data-stu-id="cec97-1512">**NX_CALLER_ERROR** (0x11) Invalid wait option from nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1513">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1513">Allowed From</span></span>

<span data-ttu-id="cec97-1514">Inizializzazione, thread, timer e ISRs (driver di rete dell'applicazione)</span><span class="sxs-lookup"><span data-stu-id="cec97-1514">Initialization, threads, timers, and ISRs (application network drivers)</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1515">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1515">Preemption Possible</span></span>

<span data-ttu-id="cec97-1516">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1516">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1517">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1517">Example</span></span>

```C
/* Append "abcd" to the specified packet. */
status = nx_packet_data_append(packet_ptr, "abcd", 4, &pool_0, 5);

/* If status is NX_SUCCESS, the additional four bytes "abcd" have
    been appended to the packet. */
```


### <a name="see-also"></a><span data-ttu-id="cec97-1518">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1518">See Also</span></span>

- <span data-ttu-id="cec97-1519">nx_packet_allocate, nx_packet_copy, nx_packet_data_extract_offset,</span><span class="sxs-lookup"><span data-stu-id="cec97-1519">nx_packet_allocate, nx_packet_copy, nx_packet_data_extract_offset,</span></span>
- <span data-ttu-id="cec97-1520">nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-1520">nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,</span></span>
- <span data-ttu-id="cec97-1521">nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="cec97-1521">nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="cec97-1522">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1522">nx_packet_transmit_release</span></span>

## <a name="nx_packet_data_extract_offset"></a><span data-ttu-id="cec97-1523">nx_packet_data_extract_offset</span><span class="sxs-lookup"><span data-stu-id="cec97-1523">nx_packet_data_extract_offset</span></span>

<span data-ttu-id="cec97-1524">Estrai i dati dal pacchetto tramite un offset</span><span class="sxs-lookup"><span data-stu-id="cec97-1524">Extract data from packet via an offset</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1525">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1525">Prototype</span></span>

```C
UINT nx_packet_data_extract_offset(
    NX_PACKET *packet_ptr,
    ULONG offset,
    VOID *buffer_start,
    ULONG buffer_length,
    ULONG *bytes_copied);
```

### <a name="description"></a><span data-ttu-id="cec97-1526">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1526">Description</span></span>

<span data-ttu-id="cec97-1527">Questo servizio copia i dati da un pacchetto NetX (o catena di pacchetti) a partire dall'offset specificato, dal puntatore a prependi del pacchetto della dimensione specificata, in byte, nel buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1527">This service copies data from a NetX packet (or packet chain) starting at the specified offset from the packet prepend pointer of the specified size in bytes into the specified buffer.</span></span> <span data-ttu-id="cec97-1528">Il numero di byte effettivamente copiati viene restituito in *bytes_copied.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1528">The number of bytes actually copied is returned in *bytes_copied.*</span></span> <span data-ttu-id="cec97-1529">Questo servizio non rimuove i dati dal pacchetto, né modifica il puntatore anteposto o altre informazioni sullo stato interno.</span><span class="sxs-lookup"><span data-stu-id="cec97-1529">This service does not remove data from the packet, nor does it adjust the prepend pointer or other internal state information.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1530">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1530">Parameters</span></span>

- <span data-ttu-id="cec97-1531">**packet_ptr** Puntatore al pacchetto da estrarre</span><span class="sxs-lookup"><span data-stu-id="cec97-1531">**packet_ptr** Pointer to packet to extract</span></span>
- <span data-ttu-id="cec97-1532">**offset** Offset dal puntatore a anteporre corrente.</span><span class="sxs-lookup"><span data-stu-id="cec97-1532">**offset** Offset from the current prepend pointer.</span></span>
- <span data-ttu-id="cec97-1533">**buffer_start** Puntatore all'inizio del buffer di salvataggio</span><span class="sxs-lookup"><span data-stu-id="cec97-1533">**buffer_start** Pointer to start of save buffer</span></span>
- <span data-ttu-id="cec97-1534">**BUFFER_LENGTH** Numero di byte da copiare</span><span class="sxs-lookup"><span data-stu-id="cec97-1534">**buffer_length** Number of bytes to copy</span></span>
- <span data-ttu-id="cec97-1535">**bytes_copied** Numero di byte effettivamente copiati</span><span class="sxs-lookup"><span data-stu-id="cec97-1535">**bytes_copied** Number of bytes actually copied</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1536">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1536">Return Values</span></span>

- <span data-ttu-id="cec97-1537">**NX_SUCCESS** (0x00) copia di pacchetti riuscita</span><span class="sxs-lookup"><span data-stu-id="cec97-1537">**NX_SUCCESS** (0x00) Successful packet copy</span></span>
- <span data-ttu-id="cec97-1538">È stato specificato un valore di offset non valido **NX_PACKET_OFFSET_ERROR** (0x53)</span><span class="sxs-lookup"><span data-stu-id="cec97-1538">**NX_PACKET_OFFSET_ERROR** (0x53) Invalid offset value was supplied</span></span>
- <span data-ttu-id="cec97-1539">**NX_PTR_ERROR** (0x07) puntatore a pacchetto o puntatore al buffer non valido</span><span class="sxs-lookup"><span data-stu-id="cec97-1539">**NX_PTR_ERROR** (0x07) Invalid packet pointer or buffer pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1540">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1540">Allowed From</span></span>

<span data-ttu-id="cec97-1541">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="cec97-1541">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1542">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1542">Preemption Possible</span></span>

<span data-ttu-id="cec97-1543">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1543">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1544">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1544">Example</span></span>

```C
/* Extract 10 bytes from the start of the received packet buffer
    into the specified memory area. */
status = nx_packet_data_extract_offset(my_packet, 0, &data[0], 10,
    &bytes_copied);

/* If status is NX_SUCCESS, 10 bytes were successfully copied into
    the data buffer. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1545">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1545">See Also</span></span>

- <span data-ttu-id="cec97-1546">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1546">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1547">nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-1547">nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,</span></span>
- <span data-ttu-id="cec97-1548">nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="cec97-1548">nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="cec97-1549">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1549">nx_packet_transmit_release</span></span>

## <a name="nx_packet_data_retrieve"></a><span data-ttu-id="cec97-1550">nx_packet_data_retrieve</span><span class="sxs-lookup"><span data-stu-id="cec97-1550">nx_packet_data_retrieve</span></span>

<span data-ttu-id="cec97-1551">Recuperare dati dal pacchetto</span><span class="sxs-lookup"><span data-stu-id="cec97-1551">Retrieve data from packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1552">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1552">Prototype</span></span>

```C
UINT nx_packet_data_retrieve(
    NX_PACKET *packet_ptr,
    VOID *buffer_start, 
    ULONG *bytes_copied);
```

### <a name="description"></a><span data-ttu-id="cec97-1553">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1553">Description</span></span>

<span data-ttu-id="cec97-1554">Questo servizio copia i dati dal pacchetto fornito nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1554">This service copies data from the supplied packet into the supplied buffer.</span></span> <span data-ttu-id="cec97-1555">Il numero effettivo di byte copiati viene restituito nella destinazione a cui punta **bytes_copied**.</span><span class="sxs-lookup"><span data-stu-id="cec97-1555">The actual number of bytes copied is returned in the destination pointed to by **bytes_copied**.</span></span>

<span data-ttu-id="cec97-1556">Si noti che questo servizio non modifica lo stato interno del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1556">Note that this service does not change internal state of the packet.</span></span> <span data-ttu-id="cec97-1557">I dati recuperati sono ancora disponibili nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1557">The data being retrieved is still available in the packet.</span></span>

<span data-ttu-id="cec97-1558">*Il buffer di destinazione deve essere sufficientemente grande da contenere il contenuto del pacchetto. In caso contrario, la memoria verrà danneggiata causando risultati imprevedibili.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1558">*The destination buffer must be large enough to hold the packet's contents. If not, memory will be corrupted causing unpredictable results.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1559">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1559">Parameters</span></span>

- <span data-ttu-id="cec97-1560">**packet_ptr** Puntatore al pacchetto di origine.</span><span class="sxs-lookup"><span data-stu-id="cec97-1560">**packet_ptr** Pointer to the source packet.</span></span>
- <span data-ttu-id="cec97-1561">**buffer_start** Puntatore all'inizio dell'area del buffer.</span><span class="sxs-lookup"><span data-stu-id="cec97-1561">**buffer_start** Pointer to the start of the buffer area.</span></span>
- <span data-ttu-id="cec97-1562">**bytes_copied** Puntatore alla destinazione per il numero di byte copiati.</span><span class="sxs-lookup"><span data-stu-id="cec97-1562">**bytes_copied** Pointer to the destination for the number of bytes copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1563">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1563">Return Values</span></span>

- <span data-ttu-id="cec97-1564">Il recupero dei dati del pacchetto **NX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1564">**NX_SUCCESS** (0x00) Successful packet data retrieve.</span></span>
- <span data-ttu-id="cec97-1565">Il pacchetto **NX_INVALID_PACKET** (0X12) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1565">**NX_INVALID_PACKET** (0x12) Invalid packet.</span></span>
- <span data-ttu-id="cec97-1566">**NX_PTR_ERROR** (0x07) pacchetto non valido, avvio del buffer o puntatore di byte copiato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1566">**NX_PTR_ERROR** (0x07) Invalid packet, buffer start, or bytes copied pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1567">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1567">Allowed From</span></span>

<span data-ttu-id="cec97-1568">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="cec97-1568">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1569">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1569">Preemption Possible</span></span>

<span data-ttu-id="cec97-1570">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1570">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1571">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1571">Example</span></span>

```C
UCHAR buffer[512];
ULONG bytes_copied;

/* Retrieve data from packet pointed to by "packet_ptr". */
status = nx_packet_data_retrieve(packet_ptr, buffer, &bytes_copied);

/* If status is NX_SUCCESS, buffer contains the contents of the
    packet, the size of which is contained in "bytes_copied." */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1572">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1572">See Also</span></span>

- <span data-ttu-id="cec97-1573">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1573">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1574">nx_packet_data_extract_offset, nx_packet_length_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-1574">nx_packet_data_extract_offset, nx_packet_length_get,</span></span>
- <span data-ttu-id="cec97-1575">nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-1575">nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="cec97-1576">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="cec97-1576">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="cec97-1577">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1577">nx_packet_transmit_release</span></span>

## <a name="nx_packet_length_get"></a><span data-ttu-id="cec97-1578">nx_packet_length_get</span><span class="sxs-lookup"><span data-stu-id="cec97-1578">nx_packet_length_get</span></span>

<span data-ttu-id="cec97-1579">Ottenere la lunghezza dei dati del pacchetto</span><span class="sxs-lookup"><span data-stu-id="cec97-1579">Get length of packet data</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1580">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1580">Prototype</span></span>

```C
UINT nx_packet_length_get(
    NX_PACKET *packet_ptr, 
    ULONG *length);
```

### <a name="description"></a><span data-ttu-id="cec97-1581">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1581">Description</span></span>

<span data-ttu-id="cec97-1582">Questo servizio ottiene la lunghezza dei dati nel pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1582">This service gets the length of the data in the specified packet.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1583">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1583">Parameters</span></span>

- <span data-ttu-id="cec97-1584">**packet_ptr** Puntatore al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1584">**packet_ptr** Pointer to the packet.</span></span>
- <span data-ttu-id="cec97-1585">**lunghezza** Destinazione per la lunghezza del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1585">**length** Destination for the packet length.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1586">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1586">Allowed From</span></span>

<span data-ttu-id="cec97-1587">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="cec97-1587">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1588">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1588">Preemption Possible</span></span>

<span data-ttu-id="cec97-1589">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1589">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1590">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1590">Example</span></span>

```C
/* Get the length of the data in "my_packet." */
status = nx_packet_length_get(my_packet, &my_length);

/* If status is NX_SUCCESS, data length is in "my_length". */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1591">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1591">See Also</span></span>

- <span data-ttu-id="cec97-1592">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1592">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1593">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="cec97-1593">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="cec97-1594">nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-1594">nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="cec97-1595">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="cec97-1595">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="cec97-1596">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1596">nx_packet_transmit_release</span></span>

## <a name="nx_packet_pool_create"></a><span data-ttu-id="cec97-1597">nx_packet_pool_create</span><span class="sxs-lookup"><span data-stu-id="cec97-1597">nx_packet_pool_create</span></span>

<span data-ttu-id="cec97-1598">Crea pool di pacchetti nell'area di memoria specificata</span><span class="sxs-lookup"><span data-stu-id="cec97-1598">Create packet pool in specified memory area</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1599">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1599">Prototype</span></span>

```C
UINT nx_packet_pool_create(
    NX_PACKET_POOL *pool_ptr,
    CHAR *name,
    ULONG payload_size,
    VOID *memory_ptr,
    ULONG memory_size);
```

### <a name="description"></a><span data-ttu-id="cec97-1600">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1600">Description</span></span>

<span data-ttu-id="cec97-1601">Questo servizio crea un pool di pacchetti con le dimensioni del pacchetto specificate nell'area di memoria fornita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="cec97-1601">This service creates a packet pool of the specified packet size in the memory area supplied by the user.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1602">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1602">Parameters</span></span>

- <span data-ttu-id="cec97-1603">**pool_ptr** Puntatore al blocco di controllo del pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1603">**pool_ptr** Pointer to packet pool control block.</span></span>
- <span data-ttu-id="cec97-1604">**nome** Puntatore al nome dell'applicazione per il pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1604">**name** Pointer to application’s name for the packet pool.</span></span>
- <span data-ttu-id="cec97-1605">**payload_size** Numero di byte in ogni pacchetto nel pool.</span><span class="sxs-lookup"><span data-stu-id="cec97-1605">**payload_size** Number of bytes in each packet in the pool.</span></span> <span data-ttu-id="cec97-1606">Questo valore deve essere almeno di 40 byte e deve essere divisibile anche per 4.</span><span class="sxs-lookup"><span data-stu-id="cec97-1606">This value must be at least 40 bytes and must also be evenly divisible by 4.</span></span>
- <span data-ttu-id="cec97-1607">**memory_ptr** Puntatore all'area di memoria in cui inserire il pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1607">**memory_ptr** Pointer to the memory area to place the packet pool in.</span></span> <span data-ttu-id="cec97-1608">Il puntatore deve essere allineato su un limite ULONG.</span><span class="sxs-lookup"><span data-stu-id="cec97-1608">The pointer should be aligned on an ULONG boundary.</span></span>
- <span data-ttu-id="cec97-1609">**memory_size** Dimensioni dell'area di memoria del pool.</span><span class="sxs-lookup"><span data-stu-id="cec97-1609">**memory_size** Size of the pool memory area.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1610">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1610">Return Values</span></span>

- <span data-ttu-id="cec97-1611">Creazione pool di pacchetti riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-1611">**NX_SUCCESS** (0x00) Successful packet pool create.</span></span>
- <span data-ttu-id="cec97-1612">**NX_PTR_ERROR** (0x07) il pool o il puntatore di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1612">**NX_PTR_ERROR** (0x07) Invalid pool or memory pointer.</span></span>
- <span data-ttu-id="cec97-1613">**NX_SIZE_ERROR** (0x09) dimensione del blocco o della memoria non valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1613">**NX_SIZE_ERROR** (0x09) Invalid block or memory size.</span></span>
- <span data-ttu-id="cec97-1614">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1614">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1615">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1615">Allowed From</span></span>

<span data-ttu-id="cec97-1616">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1616">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1617">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1617">Preemption Possible</span></span>

<span data-ttu-id="cec97-1618">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1618">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1619">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1619">Example</span></span>

```C
/* Create a packet pool of 32000 bytes starting at physical
    address 0x10000000. */
status = nx_packet_pool_create(&pool_0, "Default Pool", 128,
    (void *) 0x10000000, 32000);

/* If status is NX_SUCCESS, the packet pool has been successfully
    created. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1620">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1620">See Also</span></span>

- <span data-ttu-id="cec97-1621">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1621">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1622">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="cec97-1622">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="cec97-1623">nx_packet_length_get, nx_packet_pool_delete, nx_packet_pool_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-1623">nx_packet_length_get, nx_packet_pool_delete, nx_packet_pool_info_get,</span></span>
- <span data-ttu-id="cec97-1624">nx_packet_release, nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1624">nx_packet_release, nx_packet_transmit_release</span></span>

## <a name="nx_packet_pool_delete"></a><span data-ttu-id="cec97-1625">nx_packet_pool_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-1625">nx_packet_pool_delete</span></span>

<span data-ttu-id="cec97-1626">Elimina pool di pacchetti creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="cec97-1626">Delete previously created packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1627">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1627">Prototype</span></span>

```C
UINT nx_packet_pool_delete(NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1628">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1628">Description</span></span>

<span data-ttu-id="cec97-1629">Questo servizio Elimina un pool di pacchetti creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1629">This service deletes a previously-created packet pool.</span></span> <span data-ttu-id="cec97-1630">NetX verifica la presenza di eventuali thread attualmente sospesi nei pacchetti nel pool di pacchetti e cancella la sospensione.</span><span class="sxs-lookup"><span data-stu-id="cec97-1630">NetX checks for any threads currently suspended on packets in the packet pool and clears the suspension.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1631">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1631">Parameters</span></span>

- <span data-ttu-id="cec97-1632">**pool_ptr** Puntatore al blocco di controllo del pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cec97-1632">**pool_ptr** Packet pool control block pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1633">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1633">Return Values</span></span>

- <span data-ttu-id="cec97-1634">Eliminazione del pool di pacchetti riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-1634">**NX_SUCCESS** (0x00) Successful packet pool delete.</span></span>
- <span data-ttu-id="cec97-1635">**NX_PTR_ERROR** (0x07) puntatore al pool non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1635">**NX_PTR_ERROR** (0x07) Invalid pool pointer.</span></span>
- <span data-ttu-id="cec97-1636">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1636">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1637">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1637">Allowed From</span></span>

<span data-ttu-id="cec97-1638">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1638">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1639">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1639">Preemption Possible</span></span>

<span data-ttu-id="cec97-1640">Sì</span><span class="sxs-lookup"><span data-stu-id="cec97-1640">Yes</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1641">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1641">Example</span></span>

```C
/* Delete a previously created packet pool. */
status = nx_packet_pool_delete(&pool_0);

/* If status is NX_SUCCESS, the packet pool has been successfully
    deleted. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1642">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1642">See Also</span></span>

- <span data-ttu-id="cec97-1643">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1643">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1644">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="cec97-1644">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="cec97-1645">nx_packet_length_get, nx_packet_pool_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-1645">nx_packet_length_get, nx_packet_pool_create,</span></span>
- <span data-ttu-id="cec97-1646">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="cec97-1646">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="cec97-1647">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1647">nx_packet_transmit_release</span></span>

## <a name="nx_packet_pool_info_get"></a><span data-ttu-id="cec97-1648">nx_packet_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-1648">nx_packet_pool_info_get</span></span>

<span data-ttu-id="cec97-1649">Recuperare informazioni su un pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cec97-1649">Retrieve information about a packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1650">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1650">Prototype</span></span>

```C
UINT nx_packet_pool_info_get(
    NX_PACKET_POOL *pool_ptr,
    ULONG *total_packets,
    ULONG *free_packets,
    ULONG *empty_pool_requests,
    ULONG *empty_pool_suspensions,
    ULONG *invalid_packet_releases);
```

### <a name="description"></a><span data-ttu-id="cec97-1651">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1651">Description</span></span>

<span data-ttu-id="cec97-1652">Questo servizio recupera le informazioni sul pool di pacchetti specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1652">This service retrieves information about the specified packet pool.</span></span>

<span data-ttu-id="cec97-1653">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1653">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1654">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1654">Parameters</span></span>

- <span data-ttu-id="cec97-1655">**pool_ptr** Puntatore al pool di pacchetti creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1655">**pool_ptr** Pointer to previously created packet pool.</span></span>
- <span data-ttu-id="cec97-1656">**total_packets** Puntatore alla destinazione per il numero totale di pacchetti nel pool.</span><span class="sxs-lookup"><span data-stu-id="cec97-1656">**total_packets** Pointer to destination for the total number of packets in the pool.</span></span>
- <span data-ttu-id="cec97-1657">**free_packets** Puntatore alla destinazione per il numero totale di pacchetti attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="cec97-1657">**free_packets** Pointer to destination for the total number of currently free packets.</span></span>
- <span data-ttu-id="cec97-1658">**empty_pool_requests** Puntatore alla destinazione del numero totale di richieste di allocazione quando il pool è vuoto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1658">**empty_pool_requests** Pointer to destination of the total number of allocation requests when the pool was empty.</span></span>
- <span data-ttu-id="cec97-1659">**empty_pool_suspensions** Puntatore alla destinazione del numero totale di sospensioni del pool vuote.</span><span class="sxs-lookup"><span data-stu-id="cec97-1659">**empty_pool_suspensions** Pointer to destination of the total number of empty pool suspensions.</span></span>
- <span data-ttu-id="cec97-1660">**invalid_packet_releases** Puntatore alla destinazione del numero totale di versioni di pacchetti non valide.</span><span class="sxs-lookup"><span data-stu-id="cec97-1660">**invalid_packet_releases** Pointer to destination of the total number of invalid packet releases.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1661">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1661">Return Values</span></span>

- <span data-ttu-id="cec97-1662">Il recupero delle informazioni sul pool di pacchetti è stato completato **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-1662">**NX_SUCCESS** (0x00) Successful packet pool information retrieval.</span></span>
- <span data-ttu-id="cec97-1663">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1663">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-1664">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1664">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1665">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1665">Allowed From</span></span>

<span data-ttu-id="cec97-1666">Inizializzazione, thread e timer</span><span class="sxs-lookup"><span data-stu-id="cec97-1666">Initialization, threads, and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1667">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1667">Preemption Possible</span></span>

<span data-ttu-id="cec97-1668">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1668">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1669">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1669">Example</span></span>

```C
/* Retrieve packet pool information. */
status = nx_packet_pool_info_get(&pool_0,
    &total_packets,
    &free_packets,
    &empty_pool_requests,
    &empty_pool_suspensions,
    &invalid_packet_releases);

/* If status is NX_SUCCESS, packet pool information was
    retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1670">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1670">See Also</span></span>

- <span data-ttu-id="cec97-1671">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1671">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1672">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="cec97-1672">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="cec97-1673">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-1673">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete</span></span>
- <span data-ttu-id="cec97-1674">nx_packet_release, nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1674">nx_packet_release, nx_packet_transmit_release</span></span>

## <a name="nx_packet_release"></a><span data-ttu-id="cec97-1675">nx_packet_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1675">nx_packet_release</span></span>

<span data-ttu-id="cec97-1676">Versione del pacchetto allocato in precedenza</span><span class="sxs-lookup"><span data-stu-id="cec97-1676">Release previously allocated packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1677">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1677">Prototype</span></span>

```C
UINT nx_packet_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1678">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1678">Description</span></span>

<span data-ttu-id="cec97-1679">Questo servizio rilascia un pacchetto, inclusi eventuali pacchetti aggiuntivi concatenati al pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1679">This service releases a packet, including any additional packets chained to the specified packet.</span></span> <span data-ttu-id="cec97-1680">Se un altro thread è bloccato per l'allocazione dei pacchetti, riceve il pacchetto e lo riprende.</span><span class="sxs-lookup"><span data-stu-id="cec97-1680">If another thread is blocked on packet allocation, it is given the packet and resumed.</span></span>

<span data-ttu-id="cec97-1681">*L'applicazione deve impedire il rilascio di un pacchetto più di una volta, perché questa operazione provocherà risultati imprevedibili.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1681">*The application must prevent releasing a packet more than once, because doing so will cause unpredictable results.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1682">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1682">Parameters</span></span>

- <span data-ttu-id="cec97-1683">**packet_ptr** Puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1683">**packet_ptr** Packet pointer.</span></span>


### <a name="return-values"></a><span data-ttu-id="cec97-1684">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1684">Return Values</span></span>
- <span data-ttu-id="cec97-1685">**NX_SUCCESS** (0x00) versione del pacchetto completata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1685">**NX_SUCCESS** (0x00) Successful packet release.</span></span>
- <span data-ttu-id="cec97-1686">**NX_PTR_ERROR** (0x07) puntatore al pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1686">**NX_PTR_ERROR** (0x07) Invalid packet pointer.</span></span>
- <span data-ttu-id="cec97-1687">Il puntatore **NX_UNDERFLOW** (0x02) Prepend è inferiore all'avvio del payload.</span><span class="sxs-lookup"><span data-stu-id="cec97-1687">**NX_UNDERFLOW** (0x02) Prepend pointer is less than payload start.</span></span>
- <span data-ttu-id="cec97-1688">Il puntatore di Accodamento **NX_OVERFLOW** (0x03) è maggiore della fine del payload.</span><span class="sxs-lookup"><span data-stu-id="cec97-1688">**NX_OVERFLOW** (0x03) Append pointer is greater than payload end.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1689">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1689">Allowed From</span></span>

<span data-ttu-id="cec97-1690">Inizializzazione, thread, timer e ISRs (driver di rete dell'applicazione)</span><span class="sxs-lookup"><span data-stu-id="cec97-1690">Initialization, threads, timers, and ISRs (application network drivers)</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1691">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1691">Preemption Possible</span></span>

<span data-ttu-id="cec97-1692">Sì</span><span class="sxs-lookup"><span data-stu-id="cec97-1692">Yes</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1693">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1693">Example</span></span>

```C
/* Release a previously allocated packet. */
status = nx_packet_release(packet_ptr);

/* If status is NX_SUCCESS, the packet has been returned to the
    packet pool it was allocated from. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1694">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1694">See Also</span></span>

- <span data-ttu-id="cec97-1695">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1695">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1696">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="cec97-1696">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="cec97-1697">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-1697">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="cec97-1698">nx_packet_pool_info_get, nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1698">nx_packet_pool_info_get, nx_packet_transmit_release</span></span>

## <a name="nx_packet_transmit_release"></a><span data-ttu-id="cec97-1699">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1699">nx_packet_transmit_release</span></span>

<span data-ttu-id="cec97-1700">Rilascia un pacchetto trasmesso</span><span class="sxs-lookup"><span data-stu-id="cec97-1700">Release a transmitted packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1701">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1701">Prototype</span></span>

```C
UINT nx_packet_transmit_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1702">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1702">Description</span></span>

<span data-ttu-id="cec97-1703">Per i pacchetti non TCP, questo servizio rilascia un pacchetto trasmesso, inclusi eventuali pacchetti aggiuntivi concatenati al pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1703">For non-TCP packets, this service releases a transmitted packet, including any additional packets chained to the specified packet.</span></span> <span data-ttu-id="cec97-1704">Se un altro thread è bloccato per l'allocazione dei pacchetti, riceve il pacchetto e lo riprende.</span><span class="sxs-lookup"><span data-stu-id="cec97-1704">If another thread is blocked on packet allocation, it is given the packet and resumed.</span></span> <span data-ttu-id="cec97-1705">Per un pacchetto TCP trasmesso, il pacchetto è contrassegnato come trasmesso ma non rilasciato finché il pacchetto non viene riconosciuto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1705">For a transmitted TCP packet, the packet is marked as being transmitted but not released till the packet is acknowledged.</span></span> <span data-ttu-id="cec97-1706">Questo servizio viene in genere chiamato dal driver di rete dell'applicazione dopo la trasmissione di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1706">This service is typically called from the application's network driver after a packet is transmitted.</span></span>

<span data-ttu-id="cec97-1707">*Il driver di rete deve rimuovere l'intestazione supporto fisico e regolare la lunghezza del pacchetto prima di chiamare il servizio.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1707">*The network driver should remove the physical media header and adjust the length of the packet before calling this service.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1708">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1708">Parameters</span></span>

- <span data-ttu-id="cec97-1709">**packet_ptr** Puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1709">**packet_ptr** Packet pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1710">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1710">Return Values</span></span>

- <span data-ttu-id="cec97-1711">**NX_SUCCESS** (0x00) ha completato la trasmissione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-1711">**NX_SUCCESS** (0x00) Successful transmit packet release.</span></span>
- <span data-ttu-id="cec97-1712">**NX_PTR_ERROR** (0x07) puntatore al pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1712">**NX_PTR_ERROR** (0x07) Invalid packet pointer.</span></span>
- <span data-ttu-id="cec97-1713">Il puntatore **NX_UNDERFLOW** (0x02) Prepend è inferiore all'avvio del payload.</span><span class="sxs-lookup"><span data-stu-id="cec97-1713">**NX_UNDERFLOW** (0x02) Prepend pointer is less than payload start.</span></span>
- <span data-ttu-id="cec97-1714">Il puntatore di Accodamento **NX_OVERFLOW** (0x03) è maggiore della fine del payload.</span><span class="sxs-lookup"><span data-stu-id="cec97-1714">**NX_OVERFLOW** (0x03) Append pointer is greater than payload end.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1715">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1715">Allowed From</span></span>

<span data-ttu-id="cec97-1716">Inizializzazione, thread, timer, driver di rete dell'applicazione (incluso ISRs)</span><span class="sxs-lookup"><span data-stu-id="cec97-1716">Initialization, threads, timers, Application network drivers (including ISRs)</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1717">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1717">Preemption Possible</span></span>

<span data-ttu-id="cec97-1718">Sì</span><span class="sxs-lookup"><span data-stu-id="cec97-1718">Yes</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1719">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1719">Example</span></span>

```C
/* Release a previously allocated packet that was just transmitted
    from the application network driver. */
status = nx_packet_transmit_release(packet_ptr);

/* If status is NX_SUCCESS, the transmitted packet has been
    returned to the packet pool it was allocated from. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1720">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1720">See Also</span></span>

- <span data-ttu-id="cec97-1721">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="cec97-1721">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="cec97-1722">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="cec97-1722">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="cec97-1723">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-1723">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="cec97-1724">nx_packet_pool_info_get, nx_packet_release</span><span class="sxs-lookup"><span data-stu-id="cec97-1724">nx_packet_pool_info_get, nx_packet_release</span></span>

## <a name="nx_rarp_disable"></a><span data-ttu-id="cec97-1725">nx_rarp_disable</span><span class="sxs-lookup"><span data-stu-id="cec97-1725">nx_rarp_disable</span></span>

<span data-ttu-id="cec97-1726">Disabilitare il protocollo RARP (inverse Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="cec97-1726">Disable Reverse Address Resolution Protocol (RARP)</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1727">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1727">Prototype</span></span>

```C
UINT nx_rarp_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1728">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1728">Description</span></span>

<span data-ttu-id="cec97-1729">Questo servizio Disabilita il componente RARP di NetX per l'istanza IP specifica.</span><span class="sxs-lookup"><span data-stu-id="cec97-1729">This service disables the RARP component of NetX for the specific IP instance.</span></span> <span data-ttu-id="cec97-1730">Per un sistema multihome, questo servizio Disabilita RARP su tutte le interfacce.</span><span class="sxs-lookup"><span data-stu-id="cec97-1730">For a multihome system, this service disables RARP on all interfaces.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1731">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1731">Parameters</span></span>

- <span data-ttu-id="cec97-1732">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1732">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1733">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1733">Return Values</span></span>

- <span data-ttu-id="cec97-1734">**NX_SUCCESS** (0x00) DISABILITAto RARP con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="cec97-1734">**NX_SUCCESS** (0x00) Successful RARP disable.</span></span>
- <span data-ttu-id="cec97-1735">**NX_NOT_ENABLED** (0X14) RARP non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1735">**NX_NOT_ENABLED** (0x14) RARP was not enabled.</span></span>
- <span data-ttu-id="cec97-1736">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1736">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-1737">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1737">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1738">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1738">Allowed From</span></span>

<span data-ttu-id="cec97-1739">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1739">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1740">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1740">Preemption Possible</span></span>

<span data-ttu-id="cec97-1741">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1741">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1742">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1742">Example</span></span>

```C
/* Disable RARP on the previously created IP instance. */
status = nx_rarp_disable(&ip_0);

/* If status is NX_SUCCESS, RARP is disabled. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1743">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1743">See Also</span></span>

- <span data-ttu-id="cec97-1744">nx_rarp_enable, nx_rarp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-1744">nx_rarp_enable, nx_rarp_info_get</span></span>

## <a name="nx_rarp_enable"></a><span data-ttu-id="cec97-1745">nx_rarp_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-1745">nx_rarp_enable</span></span>

<span data-ttu-id="cec97-1746">Abilita il protocollo RARP (Reverse Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="cec97-1746">Enable Reverse Address Resolution Protocol (RARP)</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1747">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1747">Prototype</span></span>

```C
UINT nx_rarp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1748">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1748">Description</span></span>

<span data-ttu-id="cec97-1749">Questo servizio Abilita il componente RARP di NetX per l'istanza IP specifica.</span><span class="sxs-lookup"><span data-stu-id="cec97-1749">This service enables the RARP component of NetX for the specific IP instance.</span></span> <span data-ttu-id="cec97-1750">Il componente RARP esegue la ricerca in tutte le interfacce di rete collegate per un indirizzo IP zero.</span><span class="sxs-lookup"><span data-stu-id="cec97-1750">The RARP components searches through all attached network interfaces for zero IP address.</span></span> <span data-ttu-id="cec97-1751">Un indirizzo IP zero indica che l'interfaccia non è ancora stata assegnata all'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1751">A zero IP address indicates the interface does not have IP address assignment yet.</span></span> <span data-ttu-id="cec97-1752">RARP tenta di risolvere l'indirizzo IP abilitando il processo RARP su tale interfaccia.</span><span class="sxs-lookup"><span data-stu-id="cec97-1752">RARP attempts to resolve the IP address by enabling RARP process on that interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1753">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1753">Parameters</span></span>

- <span data-ttu-id="cec97-1754">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1754">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1755">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1755">Return Values</span></span>

- <span data-ttu-id="cec97-1756">Abilitazione di **NX_SUCCESS** (0x00) RARP riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1756">**NX_SUCCESS** (0x00) Successful RARP enable.</span></span>
- <span data-ttu-id="cec97-1757">L'indirizzo IP **NX_IP_ADDRESS_ERROR** (0x21) è già valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1757">**NX_IP_ADDRESS_ERROR** (0x21) IP address is already valid.</span></span>
- <span data-ttu-id="cec97-1758">**NX_ALREADY_ENABLED** (0X15) RARP è già abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1758">**NX_ALREADY_ENABLED** (0x15) RARP was already enabled.</span></span>
- <span data-ttu-id="cec97-1759">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1759">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-1760">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1760">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1761">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1761">Allowed From</span></span>

<span data-ttu-id="cec97-1762">Inizializzazione, thread, timer</span><span class="sxs-lookup"><span data-stu-id="cec97-1762">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1763">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1763">Preemption Possible</span></span>

<span data-ttu-id="cec97-1764">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1764">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1765">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1765">Example</span></span>

```C
/* Enable RARP on the previously created IP instance. */
status = nx_rarp_enable(&ip_0);

/* If status is NX_SUCCESS, RARP is enabled and is attempting to
    resolve this IP instance’s address by querying the network. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1766">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1766">See Also</span></span>

- <span data-ttu-id="cec97-1767">nx_rarp_disable, nx_rarp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-1767">nx_rarp_disable, nx_rarp_info_get</span></span>

## <a name="nx_rarp_info_get"></a><span data-ttu-id="cec97-1768">nx_rarp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-1768">nx_rarp_info_get</span></span>

<span data-ttu-id="cec97-1769">Recuperare informazioni sulle attività RARP</span><span class="sxs-lookup"><span data-stu-id="cec97-1769">Retrieve information about RARP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1770">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1770">Prototype</span></span>

```C
UINT nx_rarp_info_get(
    NX_IP *ip_ptr,
    ULONG *rarp_requests_sent,
    ULONG *rarp_responses_received,
    ULONG *rarp_invalid_messages);
```

### <a name="description"></a><span data-ttu-id="cec97-1771">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1771">Description</span></span>

<span data-ttu-id="cec97-1772">Questo servizio recupera informazioni sulle attività RARP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1772">This service retrieves information about RARP activities for the specified IP instance.</span></span>

<span data-ttu-id="cec97-1773">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1773">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1774">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1774">Parameters</span></span>

- <span data-ttu-id="cec97-1775">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1775">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1776">**rarp_requests_sent** Puntatore alla destinazione per il numero totale di richieste RARP inviate.</span><span class="sxs-lookup"><span data-stu-id="cec97-1776">**rarp_requests_sent** Pointer to destination for the total number of RARP requests sent.</span></span>
- <span data-ttu-id="cec97-1777">**rarp_responses_received** Puntatore alla destinazione per il numero totale di risposte RARP ricevute.</span><span class="sxs-lookup"><span data-stu-id="cec97-1777">**rarp_responses_received** Pointer to destination for the total number of RARP responses received.</span></span>
- <span data-ttu-id="cec97-1778">**rarp_invalid_messages** Puntatore alla destinazione del numero totale di messaggi non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-1778">**rarp_invalid_messages** Pointer to destination of the total number of invalid messages.</span></span>


### <a name="return-values"></a><span data-ttu-id="cec97-1779">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1779">Return Values</span></span>
- <span data-ttu-id="cec97-1780">Il recupero delle informazioni RARP riuscito **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-1780">**NX_SUCCESS** (0x00) Successful RARP information retrieval.</span></span>
- <span data-ttu-id="cec97-1781">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1781">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-1782">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1782">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-1783">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1783">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1784">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1784">Allowed From</span></span>

<span data-ttu-id="cec97-1785">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1785">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1786">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1786">Preemption Possible</span></span>

<span data-ttu-id="cec97-1787">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1787">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1788">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1788">Example</span></span>

```C
/* Retrieve RARP information from previously created IP
    Instance 0. */
status = nx_rarp_info_get(&ip_0,
    &rarp_requests_sent,
    &rarp_responses_received,
    &rarp_invalid_messages);

/* If status is NX_SUCCESS, RARP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1789">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1789">See Also</span></span>

- <span data-ttu-id="cec97-1790">nx_rarp_disable, nx_rarp_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-1790">nx_rarp_disable, nx_rarp_enable</span></span>

## <a name="nx_system_initialize"></a><span data-ttu-id="cec97-1791">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="cec97-1791">nx_system_initialize</span></span>

<span data-ttu-id="cec97-1792">Inizializzare il sistema NetX</span><span class="sxs-lookup"><span data-stu-id="cec97-1792">Initialize NetX System</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1793">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1793">Prototype</span></span>

```C
VOID nx_system_initialize(VOID);
```

### <a name="description"></a><span data-ttu-id="cec97-1794">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1794">Description</span></span>

<span data-ttu-id="cec97-1795">Questo servizio Inizializza le risorse di sistema NetX di base in preparazione per l'uso.</span><span class="sxs-lookup"><span data-stu-id="cec97-1795">This service initializes the basic NetX system resources in preparation for use.</span></span> <span data-ttu-id="cec97-1796">Deve essere chiamata dall'applicazione durante l'inizializzazione e prima che venga eseguita qualsiasi altra chiamata a NetX.</span><span class="sxs-lookup"><span data-stu-id="cec97-1796">It should be called by the application during initialization and before any other NetX call are made.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1797">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1797">Parameters</span></span>

<span data-ttu-id="cec97-1798">nessuno</span><span class="sxs-lookup"><span data-stu-id="cec97-1798">None</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1799">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1799">Return Values</span></span>

<span data-ttu-id="cec97-1800">nessuno</span><span class="sxs-lookup"><span data-stu-id="cec97-1800">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1801">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1801">Allowed From</span></span>

<span data-ttu-id="cec97-1802">Inizializzazione, thread, timer, ISRs</span><span class="sxs-lookup"><span data-stu-id="cec97-1802">Initialization, threads, timers, ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1803">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1803">Preemption Possible</span></span>

<span data-ttu-id="cec97-1804">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1804">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1805">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1805">Example</span></span>

```C
/* Initialize NetX for operation. */
nx_system_initialize();

/* At this point, NetX is ready for IP creation and all subsequent
    network operations. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1806">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1806">See Also</span></span>

- <span data-ttu-id="cec97-1807">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-1807">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="cec97-1808">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="cec97-1808">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="cec97-1809">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1809">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="cec97-1810">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-1810">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="cec97-1811">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check</span><span class="sxs-lookup"><span data-stu-id="cec97-1811">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check</span></span>

## <a name="nx_tcp_client_socket_bind"></a><span data-ttu-id="cec97-1812">nx_tcp_client_socket_bind</span><span class="sxs-lookup"><span data-stu-id="cec97-1812">nx_tcp_client_socket_bind</span></span>

<span data-ttu-id="cec97-1813">Associa socket TCP client a porta TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-1813">Bind client TCP socket to TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1814">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1814">Prototype</span></span>

```C
UINT nx_tcp_client_socket_bind(
    NX_TCP_SOCKET *socket_ptr,
    UINT port, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-1815">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1815">Description</span></span>

<span data-ttu-id="cec97-1816">Questo servizio associa il socket client TCP creato in precedenza alla porta TCP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1816">This service binds the previously created TCP client socket to the specified TCP port.</span></span> <span data-ttu-id="cec97-1817">I socket TCP validi sono compresi tra 0 e 0xFFFF.</span><span class="sxs-lookup"><span data-stu-id="cec97-1817">Valid TCP sockets range from 0 through 0xFFFF.</span></span> <span data-ttu-id="cec97-1818">Se la porta TCP specificata non è disponibile, il servizio viene sospeso in base all'opzione di attesa fornita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1818">If the specified TCP port is unavailable, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1819">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1819">Parameters</span></span>

- <span data-ttu-id="cec97-1820">**socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1820">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="cec97-1821">**porta** Numero di porta da associare (da 1 a 0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-1821">**port** Port number to bind (1 through 0xFFFF).</span></span> <span data-ttu-id="cec97-1822">Se il numero di porta è NX_ANY_PORT (0x0000), l'istanza IP cercherà la porta libera successiva e la utilizzerà per l'associazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-1822">If port number is NX_ANY_PORT (0x0000), the IP instance will search for the next free port and use that for the binding.</span></span>
- <span data-ttu-id="cec97-1823">**WAIT_OPTION** Definisce il comportamento del servizio se la porta è già associata a un altro socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-1823">**wait_option** Defines how the service behaves if the port is already bound to another socket.</span></span> <span data-ttu-id="cec97-1824">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-1824">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-1825">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1825">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-1826">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-1826">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-1827">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-1827">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1828">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1828">Return Values</span></span>

- <span data-ttu-id="cec97-1829">**NX_SUCCESS** (0x00) associazione Socket riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1829">**NX_SUCCESS** (0x00) Successful socket bind.</span></span>
- <span data-ttu-id="cec97-1830">**NX_ALREADY_BOUND** (0X22) questo socket è già associato a un'altra porta TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1830">**NX_ALREADY_BOUND** (0x22) This socket is already bound to another TCP port.</span></span>
- <span data-ttu-id="cec97-1831">La porta **NX_PORT_UNAVAILABLE** (0x23) è già associata a un socket diverso.</span><span class="sxs-lookup"><span data-stu-id="cec97-1831">**NX_PORT_UNAVAILABLE** (0x23) Port is already bound to a different socket.</span></span>
- <span data-ttu-id="cec97-1832">**NX_NO_FREE_PORTS** (0X45) non è disponibile alcuna porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-1832">**NX_NO_FREE_PORTS** (0x45) No free port.</span></span>
- <span data-ttu-id="cec97-1833">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al *tx_thread_wait_abort*.</span><span class="sxs-lookup"><span data-stu-id="cec97-1833">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="cec97-1834">La porta **NX_INVALID_PORT** (0x46) non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1834">**NX_INVALID_PORT** (0x46) Invalid port.</span></span>
- <span data-ttu-id="cec97-1835">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1835">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-1836">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1836">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1837">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1837">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1838">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1838">Allowed From</span></span>

<span data-ttu-id="cec97-1839">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1839">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1840">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1840">Preemption Possible</span></span>

<span data-ttu-id="cec97-1841">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1841">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1842">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1842">Example</span></span>

```C
/* Bind a previously created client socket to port 12 and wait for 7
    timer ticks for the bind to complete. */
status = nx_tcp_client_socket_bind(&client_socket, 12, 7);

/* If status is NX_SUCCESS, the previously created client_socket is
    bound to port 12 on the associated IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1843">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1843">See Also</span></span>

- <span data-ttu-id="cec97-1844">nx_tcp_client_socket_connect, nx_tcp_client_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-1844">nx_tcp_client_socket_connect, nx_tcp_client_socket_port_get,</span></span>
- <span data-ttu-id="cec97-1845">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span><span class="sxs-lookup"><span data-stu-id="cec97-1845">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span></span>
- <span data-ttu-id="cec97-1846">nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="cec97-1846">nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="cec97-1847">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1847">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-1848">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1848">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-1849">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-1849">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-1850">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-1850">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-1851">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-1851">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-1852">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-1852">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-1853">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-1853">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_client_socket_connect"></a><span data-ttu-id="cec97-1854">nx_tcp_client_socket_connect</span><span class="sxs-lookup"><span data-stu-id="cec97-1854">nx_tcp_client_socket_connect</span></span>

<span data-ttu-id="cec97-1855">Connetti socket TCP client</span><span class="sxs-lookup"><span data-stu-id="cec97-1855">Connect client TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1856">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1856">Prototype</span></span>

```C
UINT nx_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG server_ip,
    UINT server_port,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-1857">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1857">Description</span></span>

<span data-ttu-id="cec97-1858">Questo servizio connette il socket client TCP creato in precedenza e associato alla porta del server specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1858">This service connects the previously-created and bound TCP client socket to the specified server's port.</span></span> <span data-ttu-id="cec97-1859">Le porte del server TCP valide sono comprese tra 0 e 0xFFFF.</span><span class="sxs-lookup"><span data-stu-id="cec97-1859">Valid TCP server ports range from 0 through 0xFFFF.</span></span> <span data-ttu-id="cec97-1860">Se la connessione non viene completata immediatamente, il servizio viene sospeso in base all'opzione wait specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-1860">If the connection does not complete immediately, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1861">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1861">Parameters</span></span>

- <span data-ttu-id="cec97-1862">**socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1862">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="cec97-1863">**server_ip** Indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="cec97-1863">**server_ip** Server’s IP address.</span></span>
- <span data-ttu-id="cec97-1864">**SERVER_PORT** Numero di porta del server a cui connettersi (da 1 a 0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-1864">**server_port** Server port number to connect to (1 through 0xFFFF).</span></span>
- <span data-ttu-id="cec97-1865">**WAIT_OPTION** Definisce il comportamento del servizio mentre viene stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-1865">**wait_option** Defines how the service behaves while the connection is being established.</span></span> <span data-ttu-id="cec97-1866">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-1866">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-1867">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-1867">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-1868">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-1868">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-1869">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-1869">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1870">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1870">Return Values</span></span>

- <span data-ttu-id="cec97-1871">**NX_SUCCESS** (0x00) connessione socket riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1871">**NX_SUCCESS** (0x00) Successful socket connect.</span></span>
- <span data-ttu-id="cec97-1872">Il socket **NX_NOT_BOUND** (0x24) non è associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1872">**NX_NOT_BOUND** (0x24) Socket is not bound.</span></span>
- <span data-ttu-id="cec97-1873">Il socket **NX_NOT_CLOSED** (0x35) non è in uno stato chiuso.</span><span class="sxs-lookup"><span data-stu-id="cec97-1873">**NX_NOT_CLOSED** (0x35) Socket is not in a closed state.</span></span>
- <span data-ttu-id="cec97-1874">**NX_IN_PROGRESS** (0x37) non è stata specificata alcuna attesa. il tentativo di connessione è in corso.</span><span class="sxs-lookup"><span data-stu-id="cec97-1874">**NX_IN_PROGRESS** (0x37) No wait was specified, the connection attempt is in progress.</span></span>
- <span data-ttu-id="cec97-1875">Non è stata specificata l'interfaccia **NX_INVALID_INTERFACE** (0x4C).</span><span class="sxs-lookup"><span data-stu-id="cec97-1875">**NX_INVALID_INTERFACE** (0x4C) Invalid interface supplied.</span></span>
- <span data-ttu-id="cec97-1876">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-1876">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-1877">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP del server non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1877">**NX_IP_ADDRESS_ERROR** (0x21) Invalid server IP address.</span></span>
- <span data-ttu-id="cec97-1878">La porta **NX_INVALID_PORT** (0x46) non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-1878">**NX_INVALID_PORT** (0x46) Invalid port.</span></span>
- <span data-ttu-id="cec97-1879">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1879">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-1880">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1880">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1881">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1881">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1882">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1882">Allowed From</span></span>

<span data-ttu-id="cec97-1883">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1883">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1884">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1884">Preemption Possible</span></span>

<span data-ttu-id="cec97-1885">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1885">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1886">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1886">Example</span></span>

```C
/* Initiate a TCP connection from a previously created and bound
    client socket. The connection requested in this example is to
    port 12 on the server with the IP address of 1.2.3.5. This
    service will wait 300 timer ticks for the connection to take
    place before giving up. */
status = nx_tcp_client_socket_connect(&client_socket,
    IP_ADDRESS(1,2,3,5), 12, 300);

/* If status is NX_SUCCESS, the previously created and bound
    client_socket is connected to port 12 on IP 1.2.3.5. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1887">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1887">See Also</span></span>

- <span data-ttu-id="cec97-1888">nx_tcp_client_socket_bind, nx_tcp_client_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-1888">nx_tcp_client_socket_bind, nx_tcp_client_socket_port_get,</span></span>
- <span data-ttu-id="cec97-1889">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span><span class="sxs-lookup"><span data-stu-id="cec97-1889">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span></span>
- <span data-ttu-id="cec97-1890">nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="cec97-1890">nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="cec97-1891">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1891">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-1892">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1892">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-1893">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-1893">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-1894">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-1894">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-1895">nx_tcp_socket_info_get, nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="cec97-1895">nx_tcp_socket_info_get, nx_tcp_socket_receive</span></span>
- <span data-ttu-id="cec97-1896">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-1896">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-1897">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-1897">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_client_socket_port_get"></a><span data-ttu-id="cec97-1898">nx_tcp_client_socket_port_get</span><span class="sxs-lookup"><span data-stu-id="cec97-1898">nx_tcp_client_socket_port_get</span></span>

<span data-ttu-id="cec97-1899">Ottenere il numero di porta associato al socket TCP client</span><span class="sxs-lookup"><span data-stu-id="cec97-1899">Get port number bound to client TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1900">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1900">Prototype</span></span>

```C
UINT nx_tcp_client_socket_port_get(
    NX_TCP_SOCKET *socket_ptr,
    UINT *port_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1901">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1901">Description</span></span>

<span data-ttu-id="cec97-1902">Questo servizio recupera il numero di porta associato al socket, che è utile per trovare la porta allocata da NetX nelle situazioni in cui è stato specificato il NX_ANY_PORT nel momento in cui il socket è stato associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1902">This service retrieves the port number associated with the socket, which is useful to find the port allocated by NetX in situations where the NX_ANY_PORT was specified at the time the socket was bound.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1903">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1903">Parameters</span></span>

- <span data-ttu-id="cec97-1904">**socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1904">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="cec97-1905">**port_ptr** Puntatore alla destinazione per il numero di porta restituito.</span><span class="sxs-lookup"><span data-stu-id="cec97-1905">**port_ptr** Pointer to destination for the return port number.</span></span> <span data-ttu-id="cec97-1906">I numeri di porta validi sono compresi tra 1 e 0xFFFF.</span><span class="sxs-lookup"><span data-stu-id="cec97-1906">Valid port numbers are (1 through 0xFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1907">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1907">Return Values</span></span>

- <span data-ttu-id="cec97-1908">**NX_SUCCESS** (0x00) associazione Socket riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1908">**NX_SUCCESS** (0x00) Successful socket bind.</span></span>
- <span data-ttu-id="cec97-1909">**NX_NOT_BOUND** (0X24) questo socket non è associato a una porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-1909">**NX_NOT_BOUND** (0x24) This socket is not bound to a port.</span></span>
- <span data-ttu-id="cec97-1910">**NX_PTR_ERROR** (0x07) puntatore a socket non valido o puntatore a porta restituita.</span><span class="sxs-lookup"><span data-stu-id="cec97-1910">**NX_PTR_ERROR** (0x07) Invalid socket pointer or port return pointer.</span></span>
- <span data-ttu-id="cec97-1911">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1911">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1912">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1912">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1913">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1913">Allowed From</span></span>

<span data-ttu-id="cec97-1914">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1914">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1915">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1915">Preemption Possible</span></span>

<span data-ttu-id="cec97-1916">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1916">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1917">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1917">Example</span></span>

```C
/* Get the port number of previously created and bound client
    socket. */
status = nx_tcp_client_socket_port_get(&client_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
    socket is bound to. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1918">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1918">See Also</span></span>

- <span data-ttu-id="cec97-1919">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-1919">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-1920">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span><span class="sxs-lookup"><span data-stu-id="cec97-1920">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span></span>
- <span data-ttu-id="cec97-1921">nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="cec97-1921">nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="cec97-1922">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1922">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-1923">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1923">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-1924">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-1924">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-1925">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-1925">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-1926">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-1926">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-1927">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-1927">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-1928">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-1928">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_client_socket_unbind"></a><span data-ttu-id="cec97-1929">nx_tcp_client_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="cec97-1929">nx_tcp_client_socket_unbind</span></span>

<span data-ttu-id="cec97-1930">Annulla Binding socket client TCP dalla porta TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-1930">Unbind TCP client socket from TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1931">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1931">Prototype</span></span>

```C
UINT nx_tcp_client_socket_unbind(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1932">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1932">Description</span></span>

<span data-ttu-id="cec97-1933">Questo servizio rilascia l'associazione tra il socket client TCP e una porta TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1933">This service releases the binding between the TCP client socket and a TCP port.</span></span> <span data-ttu-id="cec97-1934">Se sono presenti altri thread in attesa di associare un altro socket allo stesso numero di porta, il primo thread sospeso viene quindi associato a questa porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-1934">If there are other threads waiting to bind another socket to the same port number, the first suspended thread is then bound to this port.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1935">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1935">Parameters</span></span>

- <span data-ttu-id="cec97-1936">**socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1936">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1937">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1937">Return Values</span></span>

- <span data-ttu-id="cec97-1938">La disassociazione del socket è riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-1938">**NX_SUCCESS** (0x00) Successful socket unbind.</span></span>
- <span data-ttu-id="cec97-1939">Il socket **NX_NOT_BOUND** (0x24) non è stato associato ad alcuna porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-1939">**NX_NOT_BOUND** (0x24) Socket was not bound to any port.</span></span>
- <span data-ttu-id="cec97-1940">Il socket **NX_NOT_CLOSED** (0x35) non è stato disconnesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-1940">**NX_NOT_CLOSED** (0x35) Socket has not been disconnected.</span></span>
- <span data-ttu-id="cec97-1941">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1941">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-1942">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1942">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-1943">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1943">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1944">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1944">Allowed From</span></span>

<span data-ttu-id="cec97-1945">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-1945">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1946">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1946">Preemption Possible</span></span>

<span data-ttu-id="cec97-1947">Sì</span><span class="sxs-lookup"><span data-stu-id="cec97-1947">Yes</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1948">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1948">Example</span></span>

```C
/* Unbind a previously created and bound client TCP socket. */
status = nx_tcp_client_socket_unbind(&client_socket);

/* If status is NX_SUCCESS, the client socket is no longer
    bound. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1949">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1949">See Also</span></span>

- <span data-ttu-id="cec97-1950">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-1950">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-1951">nx_tcp_client_socket_port_get, nx_tcp_enable, nx_tcp_free_port_find,</span><span class="sxs-lookup"><span data-stu-id="cec97-1951">nx_tcp_client_socket_port_get, nx_tcp_enable, nx_tcp_free_port_find,</span></span>
- <span data-ttu-id="cec97-1952">nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="cec97-1952">nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="cec97-1953">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1953">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-1954">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1954">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-1955">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-1955">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-1956">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-1956">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-1957">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-1957">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-1958">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-1958">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-1959">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-1959">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_enable"></a><span data-ttu-id="cec97-1960">nx_tcp_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-1960">nx_tcp_enable</span></span>

<span data-ttu-id="cec97-1961">Abilitare il componente TCP di NetX</span><span class="sxs-lookup"><span data-stu-id="cec97-1961">Enable TCP component of NetX</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1962">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1962">Prototype</span></span>

```C
UINT nx_tcp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1963">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1963">Description</span></span>

<span data-ttu-id="cec97-1964">Questo servizio Abilita il componente Transmission Control Protocol (TCP) di NetX.</span><span class="sxs-lookup"><span data-stu-id="cec97-1964">This service enables the Transmission Control Protocol (TCP) component of NetX.</span></span> <span data-ttu-id="cec97-1965">Dopo l'abilitazione, le connessioni TCP possono essere stabilite dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-1965">After enabled, TCP connections may be established by the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1966">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1966">Parameters</span></span>

- <span data-ttu-id="cec97-1967">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1967">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-1968">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-1968">Return Values</span></span>

- <span data-ttu-id="cec97-1969">**NX_SUCCESS** (0x00) abilitato per TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-1969">**NX_SUCCESS** (0x00) Successful TCP enable.</span></span>
- <span data-ttu-id="cec97-1970">**NX_ALREADY_ENABLED** (0X15) TCP è già abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-1970">**NX_ALREADY_ENABLED** (0x15) TCP is already enabled.</span></span>
- <span data-ttu-id="cec97-1971">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-1971">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-1972">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-1972">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-1973">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-1973">Allowed From</span></span>

<span data-ttu-id="cec97-1974">Inizializzazione, thread, timer</span><span class="sxs-lookup"><span data-stu-id="cec97-1974">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-1975">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1975">Preemption Possible</span></span>

<span data-ttu-id="cec97-1976">No</span><span class="sxs-lookup"><span data-stu-id="cec97-1976">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-1977">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-1977">Example</span></span>

```C
/* Enable TCP on a previously created IP instance ip_0. */
status = nx_tcp_enable(&ip_0);

/* If status is NX_SUCCESS, TCP is enabled on the IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-1978">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-1978">See Also</span></span>

- <span data-ttu-id="cec97-1979">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-1979">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-1980">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-1980">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-1981">nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="cec97-1981">nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="cec97-1982">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1982">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-1983">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-1983">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-1984">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-1984">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-1985">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-1985">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-1986">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-1986">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-1987">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-1987">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-1988">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-1988">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_free_port_find"></a><span data-ttu-id="cec97-1989">nx_tcp_free_port_find</span><span class="sxs-lookup"><span data-stu-id="cec97-1989">nx_tcp_free_port_find</span></span>

<span data-ttu-id="cec97-1990">Trova la porta TCP successiva disponibile</span><span class="sxs-lookup"><span data-stu-id="cec97-1990">Find next available TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-1991">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-1991">Prototype</span></span>

```C
UINT nx_tcp_free_port_find(
    NX_IP *ip_ptr,
    UINT port, UINT *free_port_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-1992">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-1992">Description</span></span>

<span data-ttu-id="cec97-1993">Questo servizio tenta di individuare una porta TCP gratuita (senza binding) a partire dalla porta fornita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-1993">This service attempts to locate a free TCP port (unbound) starting from the application supplied port.</span></span> <span data-ttu-id="cec97-1994">La logica di ricerca eseguirà il wrapping se la ricerca viene eseguita per raggiungere il valore di porta massimo di 0xFFFF.</span><span class="sxs-lookup"><span data-stu-id="cec97-1994">The search logic will wrap around if the search happens to reach the maximum port value of 0xFFFF.</span></span> <span data-ttu-id="cec97-1995">Se la ricerca ha esito positivo, la porta libera viene restituita nella variabile a cui punta *free_port_ptr*.</span><span class="sxs-lookup"><span data-stu-id="cec97-1995">If the search is successful, the free port is returned in the variable pointed to by *free_port_ptr*.</span></span>

<span data-ttu-id="cec97-1996">*Questo servizio può essere chiamato da un altro thread e deve essere restituita la stessa porta. Per evitare questo race condition, è possibile che l'applicazione inserisca il servizio e che il socket client effettivo venga associato sotto la protezione di un mutex.*</span><span class="sxs-lookup"><span data-stu-id="cec97-1996">*This service can be called from another thread and have the same port returned. To prevent this race condition, the application may wish to place this service and the actual client socket bind under the protection of a mutex.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-1997">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-1997">Parameters</span></span>

- <span data-ttu-id="cec97-1998">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-1998">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-1999">**porta** Numero di porta da cui iniziare la ricerca (da 1 a 0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-1999">**port** Port number to start search at (1 through 0xFFFF).</span></span>
- <span data-ttu-id="cec97-2000">**free_port_ptr** Puntatore al valore restituito della porta libera di destinazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2000">**free_port_ptr** Pointer to the destination free port return value.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2001">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2001">Return Values</span></span>

- <span data-ttu-id="cec97-2002">**NX_SUCCESS** (0x00) riuscite dalla porta libera.</span><span class="sxs-lookup"><span data-stu-id="cec97-2002">**NX_SUCCESS** (0x00) Successful free port find.</span></span>
- <span data-ttu-id="cec97-2003">**NX_NO_FREE_PORTS** (0X45) non sono state trovate porte gratuite.</span><span class="sxs-lookup"><span data-stu-id="cec97-2003">**NX_NO_FREE_PORTS** (0x45) No free ports found.</span></span>
- <span data-ttu-id="cec97-2004">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2004">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-2005">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2005">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2006">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2006">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-2007">**NX_INVALID_PORT** (0x46) il numero di porta specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2007">**NX_INVALID_PORT** (0x46) The specified port number is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2008">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2008">Allowed From</span></span>

<span data-ttu-id="cec97-2009">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2009">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2010">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2010">Preemption Possible</span></span>

<span data-ttu-id="cec97-2011">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2011">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2012">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2012">Example</span></span>

```C
/* Locate a free TCP port, starting at port 12, on a previously
    created IP instance. */
status = nx_tcp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS, "free_port" contains the next free port
    on the IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2013">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2013">See Also</span></span>

- <span data-ttu-id="cec97-2014">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2014">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2015">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2015">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2016">nx_tcp_enable, nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2016">nx_tcp_enable, nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="cec97-2017">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2017">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-2018">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2018">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-2019">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2019">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2020">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2020">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2021">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2021">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2022">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2022">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2023">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2023">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_info_get"></a><span data-ttu-id="cec97-2024">nx_tcp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-2024">nx_tcp_info_get</span></span>

<span data-ttu-id="cec97-2025">Recuperare informazioni sulle attività TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2025">Retrieve information about TCP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2026">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2026">Prototype</span></span>

```C
UINT nx_tcp_info_get(
    NX_IP *ip_ptr,
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received,
    ULONG *tcp_invalid_packets,
    ULONG *tcp_receive_packets_dropped,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_connections,
    ULONG *tcp_disconnections,
    ULONG *tcp_connections_dropped,
    ULONG *tcp_retransmit_packets);
```

### <a name="description"></a><span data-ttu-id="cec97-2027">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2027">Description</span></span>

<span data-ttu-id="cec97-2028">Questo servizio recupera informazioni sulle attività TCP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2028">This service retrieves information about TCP activities for the specified IP instance.</span></span>

<span data-ttu-id="cec97-2029">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2029">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2030">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2030">Parameters</span></span>

- <span data-ttu-id="cec97-2031">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2031">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-2032">**tcp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti TCP inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-2032">**tcp_packets_sent** Pointer to destination for the total number of TCP packets sent.</span></span>
- <span data-ttu-id="cec97-2033">**tcp_bytes_sent** Puntatore alla destinazione per il numero totale di byte TCP inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-2033">**tcp_bytes_sent** Pointer to destination for the total number of TCP bytes sent.</span></span>
- <span data-ttu-id="cec97-2034">**tcp_packets_received** Puntatore alla destinazione del numero totale di pacchetti TCP ricevuti.</span><span class="sxs-lookup"><span data-stu-id="cec97-2034">**tcp_packets_received** Pointer to destination of the total number of TCP packets received.</span></span>
- <span data-ttu-id="cec97-2035">**tcp_bytes_received** Puntatore alla destinazione del numero totale di byte TCP ricevuti.</span><span class="sxs-lookup"><span data-stu-id="cec97-2035">**tcp_bytes_received** Pointer to destination of the total number of TCP bytes received.</span></span>
- <span data-ttu-id="cec97-2036">**tcp_invalid_packets** Puntatore alla destinazione del numero totale di pacchetti TCP non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-2036">**tcp_invalid_packets** Pointer to destination of the total number of invalid TCP packets.</span></span>
- <span data-ttu-id="cec97-2037">**tcp_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione TCP eliminati.</span><span class="sxs-lookup"><span data-stu-id="cec97-2037">**tcp_receive_packets_dropped** Pointer to destination of the total number of TCP receive packets dropped.</span></span>
- <span data-ttu-id="cec97-2038">**tcp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti TCP con errori di checksum.</span><span class="sxs-lookup"><span data-stu-id="cec97-2038">**tcp_checksum_errors** Pointer to destination of the total number of TCP packets with checksum errors.</span></span>
- <span data-ttu-id="cec97-2039">**tcp_connections** Puntatore alla destinazione del numero totale di connessioni TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2039">**tcp_connections** Pointer to destination of the total number of TCP connections.</span></span>
- <span data-ttu-id="cec97-2040">**tcp_disconnections** Puntatore alla destinazione del numero totale di disconnessioni TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2040">**tcp_disconnections** Pointer to destination of the total number of TCP disconnections.</span></span>
- <span data-ttu-id="cec97-2041">**tcp_connections_dropped** Puntatore alla destinazione del numero totale di connessioni TCP eliminate.</span><span class="sxs-lookup"><span data-stu-id="cec97-2041">**tcp_connections_dropped** Pointer to destination of the total number of TCP connections dropped.</span></span>
- <span data-ttu-id="cec97-2042">**tcp_retransmit_packets** Puntatore alla destinazione del numero totale di pacchetti TCP ritrasmessi.</span><span class="sxs-lookup"><span data-stu-id="cec97-2042">**tcp_retransmit_packets** Pointer to destination of the total number of TCP packets retransmitted.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2043">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2043">Return Values</span></span>

- <span data-ttu-id="cec97-2044">Il recupero delle informazioni TCP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2044">**NX_SUCCESS** (0x00) Successful TCP information retrieval.</span></span>
- <span data-ttu-id="cec97-2045">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2045">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-2046">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2046">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2047">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2047">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2048">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2048">Allowed From</span></span>

<span data-ttu-id="cec97-2049">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2049">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2050">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2050">Preemption Possible</span></span>

<span data-ttu-id="cec97-2051">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2051">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2052">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2052">Example</span></span>

```C
/* Retrieve TCP information from previously created IP Instance ip_0. */
status = nx_tcp_info_get(&ip_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_invalid_packets,
    &tcp_receive_packets_dropped,
    &tcp_checksum_errors,
    &tcp_connections,
    &tcp_disconnections
    &tcp_connections_dropped,
    &tcp_retransmit_packets);

/* If status is NX_SUCCESS, TCP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2053">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2053">See Also</span></span>

- <span data-ttu-id="cec97-2054">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2054">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2055">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2055">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2056">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2056">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="cec97-2057">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2057">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-2058">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2058">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-2059">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2059">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2060">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2060">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2061">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2061">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2062">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2062">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2063">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2063">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_accept"></a><span data-ttu-id="cec97-2064">nx_tcp_server_socket_accept</span><span class="sxs-lookup"><span data-stu-id="cec97-2064">nx_tcp_server_socket_accept</span></span>

<span data-ttu-id="cec97-2065">Accetta connessione TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2065">Accept TCP connection</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2066">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2066">Prototype</span></span>

```C
UINT nx_tcp_server_socket_accept(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-2067">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2067">Description</span></span>

<span data-ttu-id="cec97-2068">Questo servizio accetta o prepara l'accettazione di una richiesta di connessione socket client TCP per una porta precedentemente configurata per l'ascolto.</span><span class="sxs-lookup"><span data-stu-id="cec97-2068">This service accepts (or prepares to accept) a TCP client socket connection request for a port that was previously set up for listening.</span></span> <span data-ttu-id="cec97-2069">Questo servizio può essere chiamato immediatamente dopo che l'applicazione chiama il servizio di ascolto o di riascolto oppure dopo che la routine di callback di ascolto viene chiamata quando la connessione client è effettivamente presente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2069">This service may be called immediately after the application calls the listen or re-listen service, or after the listen callback routine is called when the client connection is actually present.</span></span> <span data-ttu-id="cec97-2070">Se non è possibile stabilire una connessione immediatamente, il servizio viene sospeso in base all'opzione wait specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2070">If a connection cannot not be established right away, the service suspends according to the supplied wait option.</span></span>

<span data-ttu-id="cec97-2071">*L'applicazione deve chiamare **nx_tcp_server_socket_unaccept** dopo che la connessione non è più necessaria per rimuovere l'associazione del socket server alla porta del server.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2071">*The application must call **nx_tcp_server_socket_unaccept** after the connection is no longer needed to remove the server socket's binding to the server port.*</span></span>

<span data-ttu-id="cec97-2072">*Le routine di callback dell'applicazione vengono chiamate dall'interno del thread helper dell'IP.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2072">*Application callback routines are called from within the IP's helper thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2073">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2073">Parameters</span></span>

- <span data-ttu-id="cec97-2074">**socket_ptr** Puntatore al blocco di controllo socket del server TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2074">**socket_ptr** Pointer to the TCP server socket control block.</span></span>
- <span data-ttu-id="cec97-2075">**WAIT_OPTION** Definisce il comportamento del servizio mentre viene stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2075">**wait_option** Defines how the service behaves while the connection is being established.</span></span> <span data-ttu-id="cec97-2076">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-2076">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-2077">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2077">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-2078">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-2078">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-2079">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-2079">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>


### <a name="return-values"></a><span data-ttu-id="cec97-2080">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2080">Return Values</span></span>
- <span data-ttu-id="cec97-2081">**NX_SUCCESS** (0x00) accettazione socket server TCP riuscita (connessione passiva).</span><span class="sxs-lookup"><span data-stu-id="cec97-2081">**NX_SUCCESS** (0x00) Successful TCP server socket accept (passive connect).</span></span>
- <span data-ttu-id="cec97-2082">**NX_NOT_LISTEN_STATE** (0X36) il socket del server specificato non è in uno stato di attesa.</span><span class="sxs-lookup"><span data-stu-id="cec97-2082">**NX_NOT_LISTEN_STATE** (0x36) The server socket supplied is not in a listen state.</span></span>
- <span data-ttu-id="cec97-2083">**NX_IN_PROGRESS** (0x37) non è stata specificata alcuna attesa. il tentativo di connessione è in corso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2083">**NX_IN_PROGRESS** (0x37) No wait was specified, the connection attempt is in progress.</span></span>
- <span data-ttu-id="cec97-2084">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al *tx_thread_wait_abort*.</span><span class="sxs-lookup"><span data-stu-id="cec97-2084">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="cec97-2085">Errore del puntatore del socket **NX_PTR_ERROR** (0x07).</span><span class="sxs-lookup"><span data-stu-id="cec97-2085">**NX_PTR_ERROR** (0x07) Socket pointer error.</span></span>
- <span data-ttu-id="cec97-2086">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2086">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2087">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2087">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2088">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2088">Allowed From</span></span>

<span data-ttu-id="cec97-2089">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2089">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2090">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2090">Preemption Possible</span></span>

<span data-ttu-id="cec97-2091">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2091">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2092">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2092">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;
void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This
    example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;
    /* Assuming that:
        "port_12_semaphore" has already been created with an
        initial count of 0 "my_ip" has already been created and the
        link is enabled "my_pool" packet pool has already been
        created */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to each client and then disconnecting.*/
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
            request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
            complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye"
                message */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is called
            even if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket
            again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }

    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a><span data-ttu-id="cec97-2093">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2093">See Also</span></span>

- <span data-ttu-id="cec97-2094">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2094">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2095">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2095">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2096">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2096">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2097">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2097">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-2098">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2098">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-2099">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2099">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2100">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2100">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2101">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2101">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2102">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2102">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2103">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2103">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_listen"></a><span data-ttu-id="cec97-2104">nx_tcp_server_socket_listen</span><span class="sxs-lookup"><span data-stu-id="cec97-2104">nx_tcp_server_socket_listen</span></span>

<span data-ttu-id="cec97-2105">Abilita l'ascolto della connessione client sulla porta TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2105">Enable listening for client connection on TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2106">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2106">Prototype</span></span>

```C
UINT nx_tcp_server_socket_listen(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr,
    UINT listen_queue_size,
    VOID (*listen_callback)(NX_TCP_SOCKET *socket_ptr, UINT port));
```

### <a name="description"></a><span data-ttu-id="cec97-2107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2107">Description</span></span>

<span data-ttu-id="cec97-2108">Questo servizio consente l'attesa di una richiesta di connessione client sulla porta TCP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2108">This service enables listening for a client connection request on the specified TCP port.</span></span> <span data-ttu-id="cec97-2109">Quando viene ricevuta una richiesta di connessione client, il socket del server fornito viene associato alla porta specificata e viene chiamata la funzione di callback di ascolto fornita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2109">When a client connection request is received, the supplied server socket is bound to the specified port and the supplied listen callback function is called.</span></span>

<span data-ttu-id="cec97-2110">L'elaborazione della routine di callback di ascolto è stata completata fino all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2110">The listen callback routine's processing is completely up to the application.</span></span> <span data-ttu-id="cec97-2111">Può contenere la logica per riattivare un thread dell'applicazione che esegue successivamente un'operazione Accept.</span><span class="sxs-lookup"><span data-stu-id="cec97-2111">It may contain logic to wake up an application thread that subsequently performs an accept operation.</span></span> <span data-ttu-id="cec97-2112">Se l'applicazione dispone già di un thread sospeso durante l'accettazione dell'elaborazione per questo socket, la routine di callback di ascolto potrebbe non essere necessaria.</span><span class="sxs-lookup"><span data-stu-id="cec97-2112">If the application already has a thread suspended on accept processing for this socket, the listen callback routine may not be needed.</span></span>

<span data-ttu-id="cec97-2113">Se l'applicazione desidera gestire connessioni client aggiuntive sulla stessa porta, il ***nx_tcp_server_socket_relisten*** deve essere chiamato con un socket disponibile (un socket nello stato Closed) per la connessione successiva.</span><span class="sxs-lookup"><span data-stu-id="cec97-2113">If the application wishes to handle additional client connections on the same port, the ***nx_tcp_server_socket_relisten*** must be called with an available socket (a socket in the CLOSED state) for the next connection.</span></span> <span data-ttu-id="cec97-2114">Fino a quando non viene chiamato il servizio di riascolto, le connessioni client aggiuntive vengono accodate.</span><span class="sxs-lookup"><span data-stu-id="cec97-2114">Until the re-listen service is called, additional client connections are queued.</span></span> <span data-ttu-id="cec97-2115">Quando viene superata la profondità massima della coda, la richiesta di connessione meno recente viene eliminata a favore dell'accodamento della nuova richiesta di connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2115">When the maximum queue depth is exceeded, the oldest connection request is dropped in favor of queuing the new connection request.</span></span> <span data-ttu-id="cec97-2116">La profondità massima della coda è specificata da questo servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2116">The maximum queue depth is specified by this service.</span></span>

<span data-ttu-id="cec97-2117">*Le routine di callback dell'applicazione vengono chiamate dal thread di supporto IP interno.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2117">*Application callback routines are called from the internal IP helper thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2118">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2118">Parameters</span></span>

- <span data-ttu-id="cec97-2119">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2119">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-2120">**porta** Numero di porta su cui restare in ascolto (da 1 a 0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-2120">**port** Port number to listen on (1 through 0xFFFF).</span></span>
- <span data-ttu-id="cec97-2121">**socket_ptr** Puntatore al socket da utilizzare per la connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2121">**socket_ptr** Pointer to socket to use for the connection.</span></span>
- <span data-ttu-id="cec97-2122">**listen_queue_size** Numero di richieste di connessione client che possono essere accodate.</span><span class="sxs-lookup"><span data-stu-id="cec97-2122">**listen_queue_size** Number of client connection requests that can be queued.</span></span>
- <span data-ttu-id="cec97-2123">**Listen_Callback** Funzione dell'applicazione da chiamare quando viene ricevuta la connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2123">**listen_callback** Application function to call when the connection is received.</span></span> <span data-ttu-id="cec97-2124">Se viene specificato un valore NULL, la funzionalità di callback di ascolto è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2124">If a NULL is specified, the listen callback feature is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2125">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2125">Return Values</span></span>

- <span data-ttu-id="cec97-2126">**NX_SUCCESS** (0x00) la porta TCP abilitata per l'ascolto è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2126">**NX_SUCCESS** (0x00) Successful TCP port listen enable.</span></span>
- <span data-ttu-id="cec97-2127">**NX_MAX_LISTEN** (0X33) non sono disponibili altre strutture di richiesta di ascolto.</span><span class="sxs-lookup"><span data-stu-id="cec97-2127">**NX_MAX_LISTEN** (0x33) No more listen request structures are available.</span></span> <span data-ttu-id="cec97-2128">La costante NX_MAX_LISTEN_REQUESTS in nx_api. h definisce il numero di richieste di ascolto attive possibili.</span><span class="sxs-lookup"><span data-stu-id="cec97-2128">The constant NX_MAX_LISTEN_REQUESTS in nx_api.h defines how many active listen requests are possible.</span></span>
- <span data-ttu-id="cec97-2129">**NX_NOT_CLOSED** (0x35) il socket server specificato non si trova in uno stato chiuso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2129">**NX_NOT_CLOSED** (0x35) The supplied server socket is not in a closed state.</span></span>
- <span data-ttu-id="cec97-2130">**NX_ALREADY_BOUND** (0X22) il socket del server specificato è già associato a una porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-2130">**NX_ALREADY_BOUND** (0x22) The supplied server socket is already bound to a port.</span></span>
- <span data-ttu-id="cec97-2131">**NX_DUPLICATE_LISTEN** (0x34) è già presente una richiesta di ascolto attiva per questa porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-2131">**NX_DUPLICATE_LISTEN** (0x34) There is already an active listen request for this port.</span></span>
- <span data-ttu-id="cec97-2132">La porta **NX_INVALID_PORT** (0x46) specificata non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-2132">**NX_INVALID_PORT** (0x46) Invalid port specified.</span></span>
- <span data-ttu-id="cec97-2133">**NX_PTR_ERROR** (0x07) un puntatore IP o socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2133">**NX_PTR_ERROR** (0x07) Invalid IP or socket pointer.</span></span>
- <span data-ttu-id="cec97-2134">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2134">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2135">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2135">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2136">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2136">Allowed From</span></span>

<span data-ttu-id="cec97-2137">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2137">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2138">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2138">Preemption Possible</span></span>

<span data-ttu-id="cec97-2139">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2139">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2140">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2140">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread.*/
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket.
        This example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an
        initial count of 0 "my_ip" has already been created
        and the link is enabled "my_pool" packet pool has already
        been created.
    */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server
        Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to
        each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
            request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

    /* Wait for 200 ticks for the client socket connection
        to complete. */
    status = nx_tcp_server_socket_accept(&server_socket, 200);

    /* Check for a successful connection. */
    if (status == NX_SUCCESS)
    {
        /* Allocate a packet for the "Hello_and_Goodbye"
            message. */
        nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
            NX_WAIT_FOREVER);

        /* Place "Hello_and_Goodbye" in the packet. */
        nx_packet_data_append(my_packet, "Hello_and_Goodbye",
            sizeof("Hello_and_Goodbye"),
            &my_pool,
            NX_WAIT_FOREVER);

        /* Send "Hello_and_Goodbye" to client. */
        nx_tcp_socket_send(&server_socket, my_packet, 200);

        /* Check for an error. */
        if (status)
        {
            /* Error, release the packet. */
            nx_packet_release(my_packet);
        }
        /* Now disconnect the server socket from the client. */
        nx_tcp_socket_disconnect(&server_socket, 200);
    }

    /* Unaccept the server socket. Note that unaccept is called
        even if disconnect or accept fails. */
    nx_tcp_server_socket_unaccept(&server_socket);

    /* Setup server socket for listening with this socket
    again. */
    nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
}

/* We are now done so unlisten on server port 12. */
nx_tcp_server_socket_unlisten(&my_ip, 12);

/* Delete the server socket. */
nx_tcp_socket_delete(&server_socket);
```

### <a name="see-also"></a><span data-ttu-id="cec97-2141">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2141">See Also</span></span>

- <span data-ttu-id="cec97-2142">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2142">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2143">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2143">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2144">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2144">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2145">nx_tcp_server_socket_accept, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2145">nx_tcp_server_socket_accept, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-2146">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2146">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-2147">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2147">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2148">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2148">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2149">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2149">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2150">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2150">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2151">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2151">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_relisten"></a><span data-ttu-id="cec97-2152">nx_tcp_server_socket_relisten</span><span class="sxs-lookup"><span data-stu-id="cec97-2152">nx_tcp_server_socket_relisten</span></span>

<span data-ttu-id="cec97-2153">Re-ascolto della connessione client sulla porta TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2153">Re-listen for client connection on TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2154">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2154">Prototype</span></span>

```C
UINT nx_tcp_server_socket_relisten(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-2155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2155">Description</span></span>

<span data-ttu-id="cec97-2156">Questo servizio viene chiamato dopo la ricezione di una connessione su una porta che è stata impostata in precedenza per l'ascolto.</span><span class="sxs-lookup"><span data-stu-id="cec97-2156">This service is called after a connection has been received on a port that was setup previously for listening.</span></span> <span data-ttu-id="cec97-2157">Lo scopo principale di questo servizio è fornire un nuovo socket server per la successiva connessione client.</span><span class="sxs-lookup"><span data-stu-id="cec97-2157">The main purpose of this service is to provide a new server socket for the next client connection.</span></span> <span data-ttu-id="cec97-2158">Se una richiesta di connessione viene accodata, la connessione verrà elaborata immediatamente durante la chiamata al servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2158">If a connection request is queued, the connection will be processed immediately during this service call.</span></span>

<span data-ttu-id="cec97-2159">*La stessa routine di callback specificata dalla richiesta di ascolto originale viene chiamata anche quando è presente una connessione per questo nuovo socket del server.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2159">*The same callback routine specified by the original listen request is also called when a connection is present for this new server socket.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2160">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2160">Parameters</span></span>

- <span data-ttu-id="cec97-2161">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2161">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-2162">**porta** Numero di porta su cui eseguire di nuovo l'ascolto (da 1 a 0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-2162">**port** Port number to re-listen on (1 through 0xFFFF).</span></span>
- <span data-ttu-id="cec97-2163">**socket_ptr** Socket da utilizzare per la connessione client successiva.</span><span class="sxs-lookup"><span data-stu-id="cec97-2163">**socket_ptr** Socket to use for the next client connection.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2164">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2164">Return Values</span></span>
- <span data-ttu-id="cec97-2165">**NX_SUCCESS** (0x00) la porta TCP riascoltata è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2165">**NX_SUCCESS** (0x00) Successful TCP port re-listen.</span></span>
- <span data-ttu-id="cec97-2166">**NX_NOT_CLOSED** (0x35) il socket server specificato non si trova in uno stato chiuso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2166">**NX_NOT_CLOSED** (0x35) The supplied server socket is not in a closed state.</span></span>
- <span data-ttu-id="cec97-2167">**NX_ALREADY_BOUND** (0X22) il socket del server specificato è già associato a una porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-2167">**NX_ALREADY_BOUND** (0x22) The supplied server socket is already bound to a port.</span></span>
- <span data-ttu-id="cec97-2168">**NX_INVALID_RELISTEN** (0x47) è già presente un puntatore socket valido per questa porta oppure la porta specificata non ha una richiesta di ascolto attiva.</span><span class="sxs-lookup"><span data-stu-id="cec97-2168">**NX_INVALID_RELISTEN** (0x47) There is already a valid socket pointer for this port or the port specified does not have a listen request active.</span></span>
- <span data-ttu-id="cec97-2169">**NX_CONNECTION_PENDING** (0X48) uguale NX_SUCCESS, ad eccezione del fatto che è stata eseguita una richiesta di connessione in coda ed è stata elaborata durante questa chiamata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2169">**NX_CONNECTION_PENDING** (0x48) Same as NX_SUCCESS, except there was a queued connection request and it was processed during this call.</span></span>
- <span data-ttu-id="cec97-2170">La porta **NX_INVALID_PORT** (0x46) specificata non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-2170">**NX_INVALID_PORT** (0x46) Invalid port specified.</span></span>
- <span data-ttu-id="cec97-2171">**NX_PTR_ERROR** (0x07) un IP non valido o un puntatore di callback di ascolto.</span><span class="sxs-lookup"><span data-stu-id="cec97-2171">**NX_PTR_ERROR** (0x07) Invalid IP or listen callback pointer.</span></span>
- <span data-ttu-id="cec97-2172">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2172">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2173">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2173">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2174">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2174">Allowed From</span></span>

<span data-ttu-id="cec97-2175">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2175">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2176">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2176">Preemption Possible</span></span>

<span data-ttu-id="cec97-2177">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2177">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2178">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2178">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread.*/
    tx_semaphore_put(&port_12_semaphore);
    }

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This
    example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
    "port_12_semaphore" has already been created with an initial
        count of 0.
        "my_ip" has already been created and the link is enabled.
        "my_pool" packet pool has already been created. */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL,
        port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);
    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to each client then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
        request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
        complete. */
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye"
            message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is
        called even if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket
        again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a><span data-ttu-id="cec97-2179">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2179">See Also</span></span>

- <span data-ttu-id="cec97-2180">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2180">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2181">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2181">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2182">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2182">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2183">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2183">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2184">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2184">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="cec97-2185">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2185">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2186">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2186">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2187">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2187">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2188">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2188">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2189">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2189">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_unaccept"></a><span data-ttu-id="cec97-2190">nx_tcp_server_socket_unaccept</span><span class="sxs-lookup"><span data-stu-id="cec97-2190">nx_tcp_server_socket_unaccept</span></span>

<span data-ttu-id="cec97-2191">Rimuovi associazione socket con porta di ascolto</span><span class="sxs-lookup"><span data-stu-id="cec97-2191">Remove socket association with listening port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2192">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2192">Prototype</span></span>

```C
UINT nx_tcp_server_socket_unaccept(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-2193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2193">Description</span></span>

<span data-ttu-id="cec97-2194">Questo servizio rimuove l'associazione tra questo socket server e la porta del server specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2194">This service removes the association between this server socket and the specified server port.</span></span> <span data-ttu-id="cec97-2195">L'applicazione deve chiamare questo servizio dopo una disconnessione o dopo una chiamata Accept non riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2195">The application must call this service after a disconnection or after an unsuccessful accept call.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2196">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2196">Parameters</span></span>

- <span data-ttu-id="cec97-2197">**socket_ptr** Puntatore all'istanza del socket del server di installazione precedente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2197">**socket_ptr** Pointer to previously setup server socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2198">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2198">Return Values</span></span>

- <span data-ttu-id="cec97-2199">Impossibile accettare il socket server riuscito **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2199">**NX_SUCCESS** (0x00) Successful server socket unaccept.</span></span>
- <span data-ttu-id="cec97-2200">Il socket del server **NX_NOT_LISTEN_STATE** (0x36) si trova in uno stato non valido e probabilmente non è disconnesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2200">**NX_NOT_LISTEN_STATE** (0x36) Server socket is in an improper state, and is probably not disconnected.</span></span>
- <span data-ttu-id="cec97-2201">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2201">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2202">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2202">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2203">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2203">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2204">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2204">Allowed From</span></span>

<span data-ttu-id="cec97-2205">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2205">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2206">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2206">Preemption Possible</span></span>

<span data-ttu-id="cec97-2207">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2207">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2208">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2208">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This example
    doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an initial count
        of 0 "my_ip" has already been created and the link is enabled
        "my_pool" packet pool has already been created
        */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,NX_NULL,
        port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye"
        to each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection request
            is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
            complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye" message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet,
                "Hello_and_Goodbye",sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is called even
            if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a><span data-ttu-id="cec97-2209">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2209">See Also</span></span>

- <span data-ttu-id="cec97-2210">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2210">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2211">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind, nx_tcp_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-2211">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind, nx_tcp_enable,</span></span>
- <span data-ttu-id="cec97-2212">nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2212">nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="cec97-2213">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="cec97-2213">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="cec97-2214">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2214">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2215">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2215">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2216">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2216">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2217">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2217">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2218">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2218">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_unlisten"></a><span data-ttu-id="cec97-2219">nx_tcp_server_socket_unlisten</span><span class="sxs-lookup"><span data-stu-id="cec97-2219">nx_tcp_server_socket_unlisten</span></span>

<span data-ttu-id="cec97-2220">Disabilitare l'ascolto della connessione client sulla porta TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2220">Disable listening for client connection on TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2221">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2221">Prototype</span></span>

```C
UINT nx_tcp_server_socket_unlisten(NX_IP *ip_ptr, UINT port);
```

### <a name="description"></a><span data-ttu-id="cec97-2222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2222">Description</span></span>

<span data-ttu-id="cec97-2223">Questo servizio Disabilita l'attesa di una richiesta di connessione client sulla porta TCP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2223">This service disables listening for a client connection request on the specified TCP port.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2224">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2224">Parameters</span></span>

- <span data-ttu-id="cec97-2225">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2225">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-2226">**porta** Numero di porta da disabilitare in ascolto (da 0 a 0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-2226">**port** Number of port to disable listening (0 through 0xFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2227">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2227">Return Values</span></span>

- <span data-ttu-id="cec97-2228">**NX_SUCCESS** (0x00) la disabilitazione dell'ascolto TCP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2228">**NX_SUCCESS** (0x00) Successful TCP listen disable.</span></span>
- <span data-ttu-id="cec97-2229">L'attesa **NX_ENTRY_NOT_FOUND** (0x16) non è stata abilitata per la porta specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2229">**NX_ENTRY_NOT_FOUND** (0x16) Listening was not enabled for the specified port.</span></span>
- <span data-ttu-id="cec97-2230">La porta **NX_INVALID_PORT** (0x46) specificata non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-2230">**NX_INVALID_PORT** (0x46) Invalid port specified.</span></span>
- <span data-ttu-id="cec97-2231">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2231">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-2232">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2232">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2233">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2233">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2234">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2234">Allowed From</span></span>

<span data-ttu-id="cec97-2235">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2235">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2236">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2236">Preemption Possible</span></span>

<span data-ttu-id="cec97-2237">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2237">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2238">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2238">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This example
    doesn't use this callback.*/
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an initial count
        of 0 "my_ip" has already been created and the link is enabled
        "my_pool" packet pool has already been created
    */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye" to
        each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection request is
            present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye" message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"), &my_pool,
                NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }
            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }
        /* Unaccept the server socket. Note that unaccept is called even if
        disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a><span data-ttu-id="cec97-2239">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2239">See Also</span></span>

- <span data-ttu-id="cec97-2240">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2240">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2241">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2241">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2242">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2242">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2243">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2243">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2244">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2244">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2245">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2245">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2246">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2246">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2247">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2247">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2248">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2248">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2249">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2249">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_bytes_available"></a><span data-ttu-id="cec97-2250">nx_tcp_socket_bytes_available</span><span class="sxs-lookup"><span data-stu-id="cec97-2250">nx_tcp_socket_bytes_available</span></span>

<span data-ttu-id="cec97-2251">Recupera il numero di byte disponibili per il recupero</span><span class="sxs-lookup"><span data-stu-id="cec97-2251">Retrieves number of bytes available for retrieval</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2252">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2252">Prototype</span></span>

```C
UINT nx_tcp_socket_bytes_available(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```

### <a name="description"></a><span data-ttu-id="cec97-2253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2253">Description</span></span>

<span data-ttu-id="cec97-2254">Questo servizio ottiene il numero di byte disponibili per il recupero nel socket TCP specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2254">This service obtains the number of bytes available for retrieval in the specified TCP socket.</span></span> <span data-ttu-id="cec97-2255">Si noti che il socket TCP deve essere già connesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2255">Note that the TCP socket must already be connected.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2256">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2256">Parameters</span></span>

- <span data-ttu-id="cec97-2257">**socket_ptr** Puntatore al socket TCP precedentemente creato e connesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2257">**socket_ptr** Pointer to previously created and connected TCP socket.</span></span>
- <span data-ttu-id="cec97-2258">**bytes_available** Puntatore alla destinazione per byte disponibili.</span><span class="sxs-lookup"><span data-stu-id="cec97-2258">**bytes_available** Pointer to destination for bytes available.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2259">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2259">Return Values</span></span>

- <span data-ttu-id="cec97-2260">Il servizio **NX_SUCCESS** (0x00) viene eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2260">**NX_SUCCESS** (0x00) Service executes successfully.</span></span> <span data-ttu-id="cec97-2261">Il numero di byte disponibili per la lettura viene restituito al chiamante.</span><span class="sxs-lookup"><span data-stu-id="cec97-2261">Number of bytes available for read is returned to the caller.</span></span>
- <span data-ttu-id="cec97-2262">Il socket **NX_NOT_CONNECTED** (0x38) non si trova in uno stato connesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2262">**NX_NOT_CONNECTED** (0x38) Socket is not in a connected state.</span></span>
- <span data-ttu-id="cec97-2263">**NX_PTR_ERROR** (0x07) puntatori non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-2263">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="cec97-2264">**NX_NOT_ENABLED** TCP (0x14) non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2264">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="cec97-2265">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2265">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2266">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2266">Allowed From</span></span>

<span data-ttu-id="cec97-2267">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2267">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2268">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2268">Preemption Possible</span></span>

<span data-ttu-id="cec97-2269">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2269">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2270">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2270">Example</span></span>

```C
/* Get the bytes available for retrieval on the specified socket. */
status = nx_tcp_socket_bytes_available(&my_socket,
    &bytes_available);

/* Is status = NX_SUCCESS, the available bytes is returned in
    bytes_available. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2271">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2271">See Also</span></span>

- <span data-ttu-id="cec97-2272">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2272">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2273">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2273">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2274">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2274">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2275">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2275">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2276">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2276">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2277">nx_tcp_server_socket_unlisten, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2277">nx_tcp_server_socket_unlisten, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2278">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2278">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2279">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2279">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2280">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2280">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2281">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2281">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_create"></a><span data-ttu-id="cec97-2282">nx_tcp_socket_create</span><span class="sxs-lookup"><span data-stu-id="cec97-2282">nx_tcp_socket_create</span></span>

<span data-ttu-id="cec97-2283">Creazione di un client TCP o di un server socket</span><span class="sxs-lookup"><span data-stu-id="cec97-2283">Create TCP client or server socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2284">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2284">Prototype</span></span>

```C
UINT nx_tcp_socket_create(
    NX_IP *ip_ptr, 
    NX_TCP_SOCKET *socket_ptr,
    CHAR *name, ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG window_size,
    VOID (*urgent_data_callback)(NX_TCP_SOCKET *socket_ptr),
    VOID (*disconnect_callback)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="cec97-2285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2285">Description</span></span>

<span data-ttu-id="cec97-2286">Questo servizio crea un client TCP o un socket server per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2286">This service creates a TCP client or server socket for the specified IP instance.</span></span>

<span data-ttu-id="cec97-2287">*Le routine di callback dell'applicazione vengono chiamate dal thread associato a questa istanza IP.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2287">*Application callback routines are called from the thread associated with this IP instance.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2288">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2288">Parameters</span></span>

- <span data-ttu-id="cec97-2289">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2289">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-2290">**socket_ptr** Puntatore al nuovo blocco di controllo socket TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2290">**socket_ptr** Pointer to new TCP socket control block.</span></span>
- <span data-ttu-id="cec97-2291">**nome** Nome dell'applicazione per questo socket TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2291">**name** Application name for this TCP socket.</span></span>
- <span data-ttu-id="cec97-2292">**Type_of_Service** Definisce il tipo di servizio per la trasmissione. i valori validi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="cec97-2292">**type_of_service** Defines the type of service for the transmission, legal values are as follows:</span></span>

- <span data-ttu-id="cec97-2293">NX_IP_NORMAL (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2293">NX_IP_NORMAL (0x00000000)</span></span>
- <span data-ttu-id="cec97-2294">NX_IP_MIN_DELAY (0x00100000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2294">NX_IP_MIN_DELAY (0x00100000)</span></span>
- <span data-ttu-id="cec97-2295">NX_IP_MAX_DATA (0x00080000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2295">NX_IP_MAX_DATA (0x00080000)</span></span>
- <span data-ttu-id="cec97-2296">NX_IP_MAX_RELIABLE (0x00040000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2296">NX_IP_MAX_RELIABLE (0x00040000)</span></span>
- <span data-ttu-id="cec97-2297">NX_IP_MIN_COST (0x00020000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2297">NX_IP_MIN_COST (0x00020000)</span></span>

- <span data-ttu-id="cec97-2298">**frammento**  Specifica se la frammentazione IP è consentita o meno.</span><span class="sxs-lookup"><span data-stu-id="cec97-2298">**fragment**  Specifies whether or not IP fragmenting is allowed.</span></span> <span data-ttu-id="cec97-2299">Se viene specificato NX_FRAGMENT_OKAY (0x0), è consentita la frammentazione IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2299">If NX_FRAGMENT_OKAY (0x0) is specified, IP fragmenting is allowed.</span></span> <span data-ttu-id="cec97-2300">Se viene specificato NX_DONT_FRAGMENT (0x4000), la frammentazione IP è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2300">If  NX_DONT_FRAGMENT (0x4000) is specified, IP fragmenting is disabled.</span></span>
- <span data-ttu-id="cec97-2301">**Time_to_live** Specifica il valore a 8 bit che definisce il numero di router che questo pacchetto può superare prima di essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2301">**time_to_live** Specifies the 8-bit value that defines how many routers this packet can pass before being thrown away.</span></span> <span data-ttu-id="cec97-2302">Il valore predefinito è specificato dal NX_IP_TIME_TO_LIVE.</span><span class="sxs-lookup"><span data-stu-id="cec97-2302">The default value is specified by NX_IP_TIME_TO_LIVE.</span></span>
- <span data-ttu-id="cec97-2303">**window_size** Definisce il numero massimo di byte consentiti nella coda di ricezione per questo socket</span><span class="sxs-lookup"><span data-stu-id="cec97-2303">**window_size** Defines the maximum number of bytes allowed in the receive queue for this socket</span></span>
- <span data-ttu-id="cec97-2304">**urgent_data_callback** Funzione dell'applicazione che viene chiamata ogni volta che vengono rilevati dati urgenti nel flusso di ricezione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2304">**urgent_data_callback** Application function that is called whenever urgent data is detected in the receive stream.</span></span> <span data-ttu-id="cec97-2305">Se questo valore è NX_NULL, i dati urgenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="cec97-2305">If this value is NX_NULL, urgent data is ignored.</span></span>
- <span data-ttu-id="cec97-2306">**disconnect_callback** Funzione dell'applicazione che viene chiamata ogni volta che una disconnessione viene emessa dal socket all'altra estremità della connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2306">**disconnect_callback** Application function that is called whenever a disconnect is issued by the socket at the other end of the connection.</span></span> <span data-ttu-id="cec97-2307">Se questo valore è NX_NULL, la funzione di callback di disconnessione è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2307">If this value is NX_NULL, the disconnect callback function is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2308">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2308">Return Values</span></span>
- <span data-ttu-id="cec97-2309">Creazione socket client TCP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2309">**NX_SUCCESS** (0x00) Successful TCP client socket create.</span></span>
- <span data-ttu-id="cec97-2310">**NX_OPTION_ERROR** (0x0A) tipo di servizio non valido, frammento, dimensioni della finestra non valide o opzione Time-tolive.</span><span class="sxs-lookup"><span data-stu-id="cec97-2310">**NX_OPTION_ERROR** (0x0A) Invalid type-of-service, fragment, invalid window size, or time-tolive option.</span></span>
- <span data-ttu-id="cec97-2311">**NX_PTR_ERROR** (0x07) un puntatore IP o socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2311">**NX_PTR_ERROR** (0x07) Invalid IP or socket pointer.</span></span>
- <span data-ttu-id="cec97-2312">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2312">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2313">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2313">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2314">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2314">Allowed From</span></span>

<span data-ttu-id="cec97-2315">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2315">Initialization and Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2316">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2316">Preemption Possible</span></span>

<span data-ttu-id="cec97-2317">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2317">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2318">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2318">Example</span></span>

```C
/* Create a TCP client socket on the previously created IP instance,
    with normal delivery, IP fragmentation enabled, 0x80 time to
    live, a 200-byte receive window, no urgent callback routine, and
    the "client_disconnect" routine to handle disconnection initiated
    from the other end of the connection. */
status = nx_tcp_socket_create(&ip_0, &client_socket,
    "Client Socket",
    NX_IP_NORMAL, NX_FRAGMENT_OKAY,
    0x80, 200, NX_NULL
    client_disconnect);

/* If status is NX_SUCCESS, the client socket is created and ready
    to be bound. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2319">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2319">See Also</span></span>

- <span data-ttu-id="cec97-2320">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2320">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2321">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2321">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2322">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2322">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2323">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2323">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2324">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2324">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2325">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2325">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2326">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2326">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2327">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2327">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2328">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2328">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2329">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2329">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_delete"></a><span data-ttu-id="cec97-2330">nx_tcp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-2330">nx_tcp_socket_delete</span></span>

<span data-ttu-id="cec97-2331">Elimina socket TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2331">Delete TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2332">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2332">Prototype</span></span>

```C
UINT nx_tcp_socket_delete(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-2333">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2333">Description</span></span>

<span data-ttu-id="cec97-2334">Questo servizio Elimina un socket TCP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2334">This service deletes a previously created TCP socket.</span></span> <span data-ttu-id="cec97-2335">Se il socket è ancora associato o connesso, il servizio restituisce un codice di errore.</span><span class="sxs-lookup"><span data-stu-id="cec97-2335">If the socket is still bound or connected, the service returns an error code.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2336">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2336">Parameters</span></span>

- <span data-ttu-id="cec97-2337">**socket_ptr** Socket TCP creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="cec97-2337">**socket_ptr** Previously created TCP socket</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2338">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2338">Return Values</span></span>

- <span data-ttu-id="cec97-2339">Eliminazione del socket riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2339">**NX_SUCCESS** (0x00) Successful socket delete.</span></span>
- <span data-ttu-id="cec97-2340">Il socket **NX_NOT_CREATED** (0x27) non è stato creato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2340">**NX_NOT_CREATED** (0x27) Socket was not created.</span></span>
- <span data-ttu-id="cec97-2341">Il socket **NX_STILL_BOUND** (0x42) è ancora associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2341">**NX_STILL_BOUND** (0x42) Socket is still bound.</span></span>
- <span data-ttu-id="cec97-2342">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2342">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2343">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2343">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2344">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2344">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2345">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2345">Allowed From</span></span>

<span data-ttu-id="cec97-2346">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2346">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2347">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2347">Preemption Possible</span></span>

<span data-ttu-id="cec97-2348">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2348">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2349">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2349">Example</span></span>

```C
/* Delete a previously created TCP client socket. */
status = nx_tcp_socket_delete(&client_socket);

/* If status is NX_SUCCESS, the client socket is deleted. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2350">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2350">See Also</span></span>

- <span data-ttu-id="cec97-2351">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2351">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2352">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2352">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2353">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2353">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2354">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2354">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2355">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2355">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2356">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2356">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2357">nx_tcp_socket_create, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2357">nx_tcp_socket_create, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2358">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2358">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2359">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2359">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="cec97-2360">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2360">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_disconnect"></a><span data-ttu-id="cec97-2361">nx_tcp_socket_disconnect</span><span class="sxs-lookup"><span data-stu-id="cec97-2361">nx_tcp_socket_disconnect</span></span>

<span data-ttu-id="cec97-2362">Disconnettere le connessioni socket client e server</span><span class="sxs-lookup"><span data-stu-id="cec97-2362">Disconnect client and server socket connections</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2363">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2363">Prototype</span></span>

```C
UINT nx_tcp_socket_disconnect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-2364">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2364">Description</span></span>

<span data-ttu-id="cec97-2365">Questo servizio disconnette una connessione client o socket server stabilita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2365">This service disconnects an established client or server socket connection.</span></span> <span data-ttu-id="cec97-2366">Una disconnessione di un socket del server deve essere seguita da una richiesta di non accettazione, mentre un socket client disconnesso viene lasciato in uno stato pronto per un'altra richiesta di connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2366">A disconnect of a server socket should be followed by an unaccept request, while a client socket that is disconnected is left in a state ready for another connection request.</span></span> <span data-ttu-id="cec97-2367">Se non è possibile completare immediatamente il processo di disconnessione, il servizio viene sospeso in base all'opzione wait specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2367">If the disconnect process cannot finish immediately, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2368">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2368">Parameters</span></span>

- <span data-ttu-id="cec97-2369">**socket_ptr** Puntatore a un'istanza del client o del socket del server connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2369">**socket_ptr** Pointer to previously connected client or server socket instance.</span></span>
- <span data-ttu-id="cec97-2370">**WAIT_OPTION** Definisce il comportamento del servizio mentre è in corso la disconnessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2370">**wait_option** Defines how the service behaves while the disconnection is in progress.</span></span> <span data-ttu-id="cec97-2371">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-2371">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-2372">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2372">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-2373">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-2373">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-2374">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-2374">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2375">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2375">Return Values</span></span>

- <span data-ttu-id="cec97-2376">Disconnessione socket riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2376">**NX_SUCCESS** (0x00) Successful socket disconnect.</span></span>
- <span data-ttu-id="cec97-2377">Il socket specificato **NX_NOT_CONNECTED** (0x38) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2377">**NX_NOT_CONNECTED** (0x38) Specified socket is not connected.</span></span>
- <span data-ttu-id="cec97-2378">È in corso la disconnessione **NX_IN_PROGRESS** (0x37). non è stata specificata alcuna attesa.</span><span class="sxs-lookup"><span data-stu-id="cec97-2378">**NX_IN_PROGRESS** (0x37) Disconnect is in progress, no wait was specified.</span></span>
- <span data-ttu-id="cec97-2379">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-2379">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-2380">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2380">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2381">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2381">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2382">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2382">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2383">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2383">Allowed From</span></span>

<span data-ttu-id="cec97-2384">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2384">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2385">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2385">Preemption Possible</span></span>

<span data-ttu-id="cec97-2386">Sì</span><span class="sxs-lookup"><span data-stu-id="cec97-2386">Yes</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2387">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2387">Example</span></span>

```C
/* Disconnect from a previously established connection and wait a
    maximum of 400 timer ticks. */
status = nx_tcp_socket_disconnect(&client_socket, 400);

/* If status is NX_SUCCESS, the previously connected socket (either
    as a result of the client socket connect or the server accept) is
    disconnected. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2388">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2388">See Also</span></span>

- <span data-ttu-id="cec97-2389">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2389">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2390">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2390">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2391">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2391">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2392">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2392">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2393">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2393">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2394">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2394">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2395">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2395">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-2396">nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2396">nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,</span></span>
- <span data-ttu-id="cec97-2397">nx_tcp_socket_send, nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2397">nx_tcp_socket_send, nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_disconnect_complete_notify"></a><span data-ttu-id="cec97-2398">nx_tcp_socket_disconnect_complete_notify</span><span class="sxs-lookup"><span data-stu-id="cec97-2398">nx_tcp_socket_disconnect_complete_notify</span></span>

<span data-ttu-id="cec97-2399">Installazione della funzione di callback di disconnessione TCP completata</span><span class="sxs-lookup"><span data-stu-id="cec97-2399">Install TCP disconnect complete notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2400">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2400">Prototype</span></span>

```C
UINT nx_tcp_socket_disconnect_complete_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_disconnect_complete_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="cec97-2401">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2401">Description</span></span>

<span data-ttu-id="cec97-2402">Questo servizio registra una funzione di callback che viene richiamata dopo il completamento di un'operazione di disconnessione del socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2402">This service registers a callback function which is invoked after a socket disconnect operation is completed.</span></span> <span data-ttu-id="cec97-2403">La funzione di callback di disconnessione socket TCP è disponibile se NetX è compilato con l'opzione</span><span class="sxs-lookup"><span data-stu-id="cec97-2403">The TCP socket disconnect complete callback function is available if NetX is built with the option</span></span>

- <span data-ttu-id="cec97-2404">***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** definito.</span><span class="sxs-lookup"><span data-stu-id="cec97-2404">***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** defined.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2405">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2405">Parameters</span></span>

- <span data-ttu-id="cec97-2406">**socket_ptr** Puntatore a un'istanza del client o del socket del server connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2406">**socket_ptr** Pointer to previously connected client or server socket instance.</span></span>
- <span data-ttu-id="cec97-2407">**tcp_disconnect_complete_notify** Funzione di callback da installare.</span><span class="sxs-lookup"><span data-stu-id="cec97-2407">**tcp_disconnect_complete_notify** The callback function to be installed.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2408">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2408">Return Values</span></span>
- <span data-ttu-id="cec97-2409">**NX_SUCCESS** (0x00) ha registrato correttamente la funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="cec97-2409">**NX_SUCCESS** (0x00) Successfully registered the callback function.</span></span>
- <span data-ttu-id="cec97-2410">**NX_NOT_SUPPORTED** (0X4B) la funzionalità di notifica estesa non è incorporata nella libreria NETX</span><span class="sxs-lookup"><span data-stu-id="cec97-2410">**NX_NOT_SUPPORTED** (0x4B) The extended notify feature is not built into the NetX library</span></span>
- <span data-ttu-id="cec97-2411">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2411">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2412">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2412">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2413">La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2413">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2414">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2414">Allowed From</span></span>

<span data-ttu-id="cec97-2415">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2415">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2416">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2416">Preemption Possible</span></span>

<span data-ttu-id="cec97-2417">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2417">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2418">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2418">Example</span></span>

```C
/* Install the disconnect complete notify callback function. */
status = nx_tcp_socket_disconnect_complete_notify(&client_socket,
    callback);
```

### <a name="see-also"></a><span data-ttu-id="cec97-2419">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2419">See Also</span></span>

- <span data-ttu-id="cec97-2420">nx_tcp_enable, nx_tcp_socket_create, nx_tcp_socket_establish_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2420">nx_tcp_enable, nx_tcp_socket_create, nx_tcp_socket_establish_notify,</span></span>
- <span data-ttu-id="cec97-2421">nx_tcp_socket_mss_get, nx_tcp_socket_mss_peer_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2421">nx_tcp_socket_mss_get, nx_tcp_socket_mss_peer_get,</span></span>
- <span data-ttu-id="cec97-2422">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2422">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span></span>
- <span data-ttu-id="cec97-2423">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="cec97-2423">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="cec97-2424">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="cec97-2424">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="cec97-2425">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2425">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_establish_notify"></a><span data-ttu-id="cec97-2426">nx_tcp_socket_establish_notify</span><span class="sxs-lookup"><span data-stu-id="cec97-2426">nx_tcp_socket_establish_notify</span></span>

<span data-ttu-id="cec97-2427">Impostare la funzione TCP establishe Notify callback</span><span class="sxs-lookup"><span data-stu-id="cec97-2427">Set TCP establish notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2428">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2428">Prototype</span></span>

```C
UINT nx_tcp_socket_establish_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_establish_notify)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="cec97-2429">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2429">Description</span></span>

<span data-ttu-id="cec97-2430">Questo servizio registra una funzione di callback, che viene chiamata dopo che un socket TCP crea una connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2430">This service registers a callback function, which is called after a TCP socket makes a connection.</span></span> <span data-ttu-id="cec97-2431">Il socket TCP stabilisce la funzione di callback è disponibile se NetX viene compilato con l'opzione ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** definita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2431">The TCP socket establish callback function is available if NetX is built with the option ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** defined.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2432">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2432">Parameters</span></span>

- <span data-ttu-id="cec97-2433">**socket_ptr** Puntatore a un'istanza del client o del socket del server connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2433">**socket_ptr** Pointer to previously connected client or server socket instance.</span></span>
- <span data-ttu-id="cec97-2434">**tcp_establish_notify** Funzione di callback richiamata dopo che è stata stabilita una connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2434">**tcp_establish_notify** Callback function invoked after a TCP connection is established.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2435">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2435">Return Values</span></span>

- <span data-ttu-id="cec97-2436">**NX_SUCCESS** (0x00) imposta correttamente la funzione Notify.</span><span class="sxs-lookup"><span data-stu-id="cec97-2436">**NX_SUCCESS** (0x00) Successfully sets the notify function.</span></span>
- <span data-ttu-id="cec97-2437">**NX_NOT_SUPPORTED** (0X4B) la funzionalità di notifica estesa non è incorporata nella libreria NETX</span><span class="sxs-lookup"><span data-stu-id="cec97-2437">**NX_NOT_SUPPORTED** (0x4B) The extended notify feature is not built into the NetX library</span></span>
- <span data-ttu-id="cec97-2438">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2438">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2439">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2439">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2440">**NX_NOT_ENABLED** (0X14) TCP non è stato abilitato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2440">**NX_NOT_ENABLED** (0x14) TCP has not been enabled by the application.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2441">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2441">Allowed From</span></span>

<span data-ttu-id="cec97-2442">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2442">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2443">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2443">Preemption Possible</span></span>

<span data-ttu-id="cec97-2444">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2444">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2445">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2445">Example</span></span>

```C
/* Set the function pointer "callback" as the notify function NetX
will call when the connection is in the established state. */
status = nx_tcp_socket_establish_notify(&client_socket, callback);
```

### <a name="see-also"></a><span data-ttu-id="cec97-2446">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2446">See Also</span></span>

- <span data-ttu-id="cec97-2447">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2447">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2448">nx_tcp_socket_disconnect_complete_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2448">nx_tcp_socket_disconnect_complete_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="cec97-2449">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2449">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="cec97-2450">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2450">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-2451">nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="cec97-2451">nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="cec97-2452">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2452">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_info_get"></a><span data-ttu-id="cec97-2453">nx_tcp_socket_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-2453">nx_tcp_socket_info_get</span></span>

<span data-ttu-id="cec97-2454">Recuperare informazioni sulle attività dei socket TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2454">Retrieve information about TCP socket activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2455">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2455">Prototype</span></span>

```C
UINT nx_tcp_socket_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received,
    ULONG *tcp_retransmit_packets,
    ULONG *tcp_packets_queued,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_socket_state,
    ULONG *tcp_transmit_queue_depth,
    ULONG *tcp_transmit_window,
    ULONG *tcp_receive_window);
```

### <a name="description"></a><span data-ttu-id="cec97-2456">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2456">Description</span></span>

<span data-ttu-id="cec97-2457">Questo servizio recupera informazioni sulle attività socket TCP per l'istanza di socket TCP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2457">This service retrieves information about TCP socket activities for the specified TCP socket instance.</span></span>

<span data-ttu-id="cec97-2458">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2458">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2459">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2459">Parameters</span></span>

- <span data-ttu-id="cec97-2460">**socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2460">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="cec97-2461">**tcp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti TCP inviati al socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2461">**tcp_packets_sent** Pointer to destination for the total number of TCP packets sent on socket.</span></span>
- <span data-ttu-id="cec97-2462">**tcp_bytes_sent** Puntatore alla destinazione per il numero totale di byte TCP inviati al socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2462">**tcp_bytes_sent** Pointer to destination for the total number of TCP bytes sent on socket.</span></span>
- <span data-ttu-id="cec97-2463">**tcp_packets_received** Puntatore alla destinazione del numero totale di pacchetti TCP ricevuti sul socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2463">**tcp_packets_received** Pointer to destination of the total number of TCP packets received on socket.</span></span>
- <span data-ttu-id="cec97-2464">**tcp_bytes_received** Puntatore alla destinazione del numero totale di byte TCP ricevuti sul socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2464">**tcp_bytes_received** Pointer to destination of the total number of TCP bytes received on socket.</span></span>
- <span data-ttu-id="cec97-2465">**tcp_retransmit_packets** Puntatore alla destinazione del numero totale di ritrasmissioni di pacchetti TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2465">**tcp_retransmit_packets** Pointer to destination of the total number of TCP packet retransmissions.</span></span>
- <span data-ttu-id="cec97-2466">**tcp_packets_queued** Puntatore alla destinazione del numero totale di pacchetti TCP in coda nel socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2466">**tcp_packets_queued** Pointer to destination of the total number of queued TCP packets on socket.</span></span>
- <span data-ttu-id="cec97-2467">**tcp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti TCP con errori di checksum nel socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2467">**tcp_checksum_errors** Pointer to destination of the total number of TCP packets with checksum errors on socket.</span></span>
- <span data-ttu-id="cec97-2468">**tcp_socket_state** Puntatore alla destinazione dello stato corrente del socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2468">**tcp_socket_state** Pointer to destination of the socket’s current state.</span></span>
- <span data-ttu-id="cec97-2469">**tcp_transmit_queue_depth** Puntatore alla destinazione del numero totale di pacchetti di trasmissione ancora in coda in attesa di ACK.</span><span class="sxs-lookup"><span data-stu-id="cec97-2469">**tcp_transmit_queue_depth** Pointer to destination of the total number of transmit packets still queued waiting for ACK.</span></span>
- <span data-ttu-id="cec97-2470">**tcp_transmit_window** Puntatore alla destinazione della dimensione della finestra di trasmissione corrente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2470">**tcp_transmit_window** Pointer to destination of the current transmit window size.</span></span>
- <span data-ttu-id="cec97-2471">**tcp_receive_window** Puntatore alla destinazione delle dimensioni correnti della finestra di ricezione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2471">**tcp_receive_window** Pointer to destination of the current receive window size.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2472">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2472">Return Values</span></span>

- <span data-ttu-id="cec97-2473">Il recupero delle informazioni sul socket TCP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2473">**NX_SUCCESS** (0x00) Successful TCP socket information retrieval.</span></span>
- <span data-ttu-id="cec97-2474">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2474">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2475">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2475">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2476">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2476">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2477">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2477">Return Values</span></span>

```C
/* Retrieve TCP socket information from previously created socket_0.*/
status = nx_tcp_socket_info_get(&socket_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_retransmit_packets,
    &tcp_packets_queued,
    &tcp_checksum_errors,
    &tcp_socket_state,
    &tcp_transmit_queue_depth,
    &tcp_transmit_window,
    &tcp_receive_window);

/* If status is NX_SUCCESS, TCP socket information was retrieved. */
```

### <a name="allowed-from"></a><span data-ttu-id="cec97-2478">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2478">Allowed From</span></span>

<span data-ttu-id="cec97-2479">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2479">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2480">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2480">Preemption Possible</span></span>

<span data-ttu-id="cec97-2481">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2481">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2482">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2482">Example</span></span>

```C
/* Retrieve TCP socket information from previously created socket_0.*/
status = nx_tcp_socket_info_get(&socket_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_retransmit_packets,
    &tcp_packets_queued,
    &tcp_checksum_errors,
    &tcp_socket_state,
    &tcp_transmit_queue_depth,
    &tcp_transmit_window,
    &tcp_receive_window);

/* If status is NX_SUCCESS, TCP socket information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2483">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2483">See Also</span></span>

- <span data-ttu-id="cec97-2484">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2484">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2485">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2485">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2486">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2486">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2487">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2487">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2488">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2488">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2489">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2489">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2490">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2490">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2491">nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2491">nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,</span></span>
- <span data-ttu-id="cec97-2492">nx_tcp_socket_send, nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2492">nx_tcp_socket_send, nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_mss_get"></a><span data-ttu-id="cec97-2493">nx_tcp_socket_mss_get</span><span class="sxs-lookup"><span data-stu-id="cec97-2493">nx_tcp_socket_mss_get</span></span>

<span data-ttu-id="cec97-2494">Ottenere la MSS del socket</span><span class="sxs-lookup"><span data-stu-id="cec97-2494">Get MSS of socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2495">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2495">Prototype</span></span>

```C
UINT nx_tcp_socket_mss_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a><span data-ttu-id="cec97-2496">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2496">Description</span></span>

<span data-ttu-id="cec97-2497">Questo servizio recupera la dimensione del segmento massimo locale (MSS) del socket specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2497">This service retrieves the specified socket's local Maximum Segment Size (MSS).</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2498">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2498">Parameters</span></span>

- <span data-ttu-id="cec97-2499">**socket_ptr** Puntatore al socket creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2499">**socket_ptr** Pointer to previously created socket.</span></span>
- <span data-ttu-id="cec97-2500">**MSS** Destinazione per la restituzione di MSS.</span><span class="sxs-lookup"><span data-stu-id="cec97-2500">**mss** Destination for returning MSS.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2501">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2501">Return Values</span></span>

- <span data-ttu-id="cec97-2502">**NX_SUCCESS** (0x00) riuscite MSS Get.</span><span class="sxs-lookup"><span data-stu-id="cec97-2502">**NX_SUCCESS** (0x00) Successful MSS get.</span></span>
- <span data-ttu-id="cec97-2503">**NX_PTR_ERROR** (0x07) o un puntatore di destinazione MSS non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2503">**NX_PTR_ERROR** (0x07) Invalid socket or MSS destination pointer.</span></span>
- <span data-ttu-id="cec97-2504">**NX_NOT_ENABLED** TCP (0x14) non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2504">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="cec97-2505">Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2505">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2506">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2506">Allowed From</span></span>

<span data-ttu-id="cec97-2507">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2507">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2508">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2508">Preemption Possible</span></span>

<span data-ttu-id="cec97-2509">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2509">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2510">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2510">Example</span></span>

```C
/* Get the MSS for the socket "my_socket". */
status = nx_tcp_socket_mss_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
    socket's current MSS value. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2511">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2511">See Also</span></span>

- <span data-ttu-id="cec97-2512">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2512">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2513">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2513">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="cec97-2514">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_peer_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2514">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_peer_get,</span></span>
- <span data-ttu-id="cec97-2515">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2515">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span></span>
- <span data-ttu-id="cec97-2516">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="cec97-2516">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="cec97-2517">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="cec97-2517">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="cec97-2518">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2518">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_mss_peer_get"></a><span data-ttu-id="cec97-2519">nx_tcp_socket_mss_peer_get</span><span class="sxs-lookup"><span data-stu-id="cec97-2519">nx_tcp_socket_mss_peer_get</span></span>

<span data-ttu-id="cec97-2520">Ottenere la MSS del socket TCP peer</span><span class="sxs-lookup"><span data-stu-id="cec97-2520">Get MSS of the peer TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2521">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2521">Prototype</span></span>

```C
UINT nx_tcp_socket_mss_peer_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a><span data-ttu-id="cec97-2522">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2522">Description</span></span>

<span data-ttu-id="cec97-2523">Questo servizio recupera le dimensioni massime del segmento (MSS) annunciate dal socket peer.</span><span class="sxs-lookup"><span data-stu-id="cec97-2523">This service retrieves the Maximum Segment Size (MSS) advertised by the peer socket.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2524">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2524">Parameters</span></span>

- <span data-ttu-id="cec97-2525">**socket_ptr** Puntatore al socket precedentemente creato e connesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2525">**socket_ptr** Pointer to previously created and connected socket.</span></span>
- <span data-ttu-id="cec97-2526">**MSS** Destinazione per la restituzione dell'oggetto MSS.</span><span class="sxs-lookup"><span data-stu-id="cec97-2526">**mss** Destination for returning the MSS.</span></span>


### <a name="return-values"></a><span data-ttu-id="cec97-2527">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2527">Return Values</span></span>

- <span data-ttu-id="cec97-2528">**NX_SUCCESS** (0x00) il peer MSS riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="cec97-2528">**NX_SUCCESS** (0x00) Successful peer MSS get.</span></span>
- <span data-ttu-id="cec97-2529">**NX_PTR_ERROR** (0x07) o un puntatore di destinazione MSS non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2529">**NX_PTR_ERROR** (0x07) Invalid socket or MSS destination pointer.</span></span>
- <span data-ttu-id="cec97-2530">**NX_NOT_ENABLED** TCP (0x14) non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2530">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="cec97-2531">Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2531">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2532">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2532">Allowed From</span></span>

<span data-ttu-id="cec97-2533">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2533">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2534">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2534">Preemption Possible</span></span>

<span data-ttu-id="cec97-2535">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2535">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2536">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2536">Example</span></span>

```C
/* Get the MSS of the connected peer to the socket "my_socket". */
status = nx_tcp_socket_mss_peer_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
    socket peer’s advertised MSS value. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2537">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2537">See Also</span></span>

- <span data-ttu-id="cec97-2538">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2538">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2539">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2539">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="cec97-2540">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2540">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="cec97-2541">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2541">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span></span>
- <span data-ttu-id="cec97-2542">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="cec97-2542">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="cec97-2543">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="cec97-2543">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="cec97-2544">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2544">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_mss_set"></a><span data-ttu-id="cec97-2545">nx_tcp_socket_mss_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2545">nx_tcp_socket_mss_set</span></span>

<span data-ttu-id="cec97-2546">Imposta MSS del socket</span><span class="sxs-lookup"><span data-stu-id="cec97-2546">Set MSS of socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2547">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2547">Prototype</span></span>

```C
UINT nx_tcp_socket_mss_set(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG mss);
```

### <a name="description"></a><span data-ttu-id="cec97-2548">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2548">Description</span></span>

<span data-ttu-id="cec97-2549">Questo servizio imposta la dimensione massima del segmento (MSS) del socket specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2549">This service sets the specified socket's Maximum Segment Size (MSS).</span></span> <span data-ttu-id="cec97-2550">Si noti che il valore MSS deve rientrare nell'IP dell'interfaccia di rete MTU, consentendo spazio per le intestazioni IP e TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2550">Note the MSS value must be within the network interface IP MTU, allowing room for IP and TCP headers.</span></span>

<span data-ttu-id="cec97-2551">Questo servizio deve essere utilizzato prima che un socket TCP avvii il processo di connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2551">This service should be used before a TCP socket starts the connection process.</span></span> <span data-ttu-id="cec97-2552">Se il servizio viene utilizzato dopo che è stata stabilita una connessione TCP, il nuovo valore non ha alcun effetto sulla connessione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2552">If the service is used after a TCP connection is established, the new value has no effect on the connection.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2553">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2553">Parameters</span></span>

- <span data-ttu-id="cec97-2554">**socket_ptr** Puntatore al socket creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2554">**socket_ptr** Pointer to previously created socket.</span></span>
- <span data-ttu-id="cec97-2555">**MSS** Valore di MSS da impostare.</span><span class="sxs-lookup"><span data-stu-id="cec97-2555">**mss** Value of MSS to set.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2556">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2556">Return Values</span></span>

- <span data-ttu-id="cec97-2557">Set di MSS riusciti **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2557">**NX_SUCCESS** (0x00) Successful MSS set.</span></span>
- <span data-ttu-id="cec97-2558">Il valore MSS specificato per **NX_SIZE_ERROR** (0x09) è troppo grande.</span><span class="sxs-lookup"><span data-stu-id="cec97-2558">**NX_SIZE_ERROR** (0x09) Specified MSS value is too large.</span></span>
- <span data-ttu-id="cec97-2559">Non è stata stabilita la connessione TCP **NX_NOT_CONNECTED** (0x38)</span><span class="sxs-lookup"><span data-stu-id="cec97-2559">**NX_NOT_CONNECTED** (0x38) TCP connection has not been established</span></span>
- <span data-ttu-id="cec97-2560">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2560">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2561">**NX_NOT_ENABLED** TCP (0x14) non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2561">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="cec97-2562">Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2562">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2563">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2563">Allowed From</span></span>

<span data-ttu-id="cec97-2564">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2564">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2565">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2565">Preemption Possible</span></span>

<span data-ttu-id="cec97-2566">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2566">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2567">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2567">Example</span></span>

```C
/* Set the MSS of the socket "my_socket" to 1000 bytes. */
status = nx_tcp_socket_mss_set(&my_socket, 1000);

/* If status is NX_SUCCESS, the MSS of "my_socket" is 1000 bytes. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2568">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2568">See Also</span></span>

- <span data-ttu-id="cec97-2569">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2569">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2570">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2570">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="cec97-2571">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2571">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="cec97-2572">nx_tcp_socket_mss_peer_get, nx_tcp_socket_peer_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2572">nx_tcp_socket_mss_peer_get, nx_tcp_socket_peer_info_get,</span></span>
- <span data-ttu-id="cec97-2573">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="cec97-2573">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="cec97-2574">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="cec97-2574">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="cec97-2575">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2575">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_peer_info_get"></a><span data-ttu-id="cec97-2576">nx_tcp_socket_peer_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-2576">nx_tcp_socket_peer_info_get</span></span>

<span data-ttu-id="cec97-2577">Recuperare informazioni sul socket TCP peer</span><span class="sxs-lookup"><span data-stu-id="cec97-2577">Retrieve information about peer TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2578">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2578">Prototype</span></span>

```C
UINT nx_tcp_socket_peer_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *peer_ip_address, 
    ULONG *peer_port);
```

### <a name="description"></a><span data-ttu-id="cec97-2579">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2579">Description</span></span>

<span data-ttu-id="cec97-2580">Questo servizio recupera le informazioni sull'indirizzo IP e sulla porta del peer per il socket TCP connesso sulla rete IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2580">This service retrieves peer IP address and port information for the connected TCP socket over IP network.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2581">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2581">Parameters</span></span>

- <span data-ttu-id="cec97-2582">**socket_ptr** Puntatore al socket TCP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2582">**socket_ptr** Pointer to previously created TCP socket.</span></span>
- <span data-ttu-id="cec97-2583">**peer_ip_address** Puntatore alla destinazione per l'indirizzo IP del peer nell'ordine dei byte dell'host.</span><span class="sxs-lookup"><span data-stu-id="cec97-2583">**peer_ip_address** Pointer to destination for peer IP address, in host byte order.</span></span>
- <span data-ttu-id="cec97-2584">**peer_port** Puntatore alla destinazione per il numero di porta peer nell'ordine dei byte dell'host.</span><span class="sxs-lookup"><span data-stu-id="cec97-2584">**peer_port** Pointer to destination for peer port number, in host byte order.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2585">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2585">Return Values</span></span>

- <span data-ttu-id="cec97-2586">Il servizio **NX_SUCCESS** (0x00) viene eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2586">**NX_SUCCESS** (0x00) Service executes successfully.</span></span> <span data-ttu-id="cec97-2587">Il numero di porta e l'indirizzo IP del peer vengono restituiti al chiamante.</span><span class="sxs-lookup"><span data-stu-id="cec97-2587">Peer IP address and port number are returned to the caller.</span></span>
- <span data-ttu-id="cec97-2588">Il socket **NX_NOT_CONNECTED** (0x38) non si trova in uno stato connesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2588">**NX_NOT_CONNECTED** (0x38) Socket is not in a connected state.</span></span>
- <span data-ttu-id="cec97-2589">**NX_PTR_ERROR** (0x07) puntatori non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-2589">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="cec97-2590">**NX_NOT_ENABLED** TCP (0x14) non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2590">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="cec97-2591">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2591">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2592">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2592">Allowed From</span></span>

<span data-ttu-id="cec97-2593">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2593">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2594">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2594">Preemption Possible</span></span>

<span data-ttu-id="cec97-2595">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2595">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2596">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2596">Example</span></span>

```C
/* Obtain peer IP address and port on the specified TCP socket. */
status = nx_tcp_socket_peer_info_get(&my_socket, &peer_ip_address,
    &peer_port);

/* If status = NX_SUCCESS, the data was successfully obtained. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2597">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2597">See Also</span></span>

- <span data-ttu-id="cec97-2598">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2598">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2599">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2599">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="cec97-2600">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2600">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="cec97-2601">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2601">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="cec97-2602">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="cec97-2602">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="cec97-2603">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="cec97-2603">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="cec97-2604">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2604">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_receive"></a><span data-ttu-id="cec97-2605">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="cec97-2605">nx_tcp_socket_receive</span></span>

<span data-ttu-id="cec97-2606">Ricevere dati dal socket TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2606">Receive data from TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2607">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2607">Prototype</span></span>

```C
UINT nx_tcp_socket_receive(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-2608">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2608">Description</span></span>

<span data-ttu-id="cec97-2609">Questo servizio riceve i dati TCP dal socket specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2609">This service receives TCP data from the specified socket.</span></span> <span data-ttu-id="cec97-2610">Se non viene accodato alcun dato nel socket specificato, il chiamante viene sospeso in base all'opzione wait fornita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2610">If no data are queued on the specified socket, the caller suspends based on the supplied wait option.</span></span>

<span data-ttu-id="cec97-2611">*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2611">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2612">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2612">Parameters</span></span>

- <span data-ttu-id="cec97-2613">**socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2613">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="cec97-2614">**packet_ptr** Puntatore al puntatore del pacchetto TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2614">**packet_ptr** Pointer to TCP packet pointer.</span></span>
- <span data-ttu-id="cec97-2615">**WAIT_OPTION** Definisce il comportamento del servizio se nessun dato è attualmente accodato in questo socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2615">**wait_option** Defines how the service behaves if no data are currently queued on this socket.</span></span> <span data-ttu-id="cec97-2616">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-2616">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-2617">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2617">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-2618">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-2618">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-2619">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-2619">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2620">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2620">Return Values</span></span>
- <span data-ttu-id="cec97-2621">**NX_SUCCESS** (0x00) la ricezione dei dati socket è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2621">**NX_SUCCESS** (0x00) Successful socket data receive.</span></span>
- <span data-ttu-id="cec97-2622">Il socket **NX_NOT_BOUND** (0x24) non è ancora associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2622">**NX_NOT_BOUND** (0x24) Socket is not bound yet.</span></span>
- <span data-ttu-id="cec97-2623">**NX_NO_PACKET** (0x01) non sono stati ricevuti dati.</span><span class="sxs-lookup"><span data-stu-id="cec97-2623">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="cec97-2624">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-2624">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-2625">**NX_NOT_CONNECTED** (0X38) il socket non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2625">**NX_NOT_CONNECTED** (0x38) The socket is no longer connected.</span></span>
- <span data-ttu-id="cec97-2626">**NX_PTR_ERROR** (0x07) socket non valido o puntatore al pacchetto restituito.</span><span class="sxs-lookup"><span data-stu-id="cec97-2626">**NX_PTR_ERROR** (0x07) Invalid socket or return packet pointer.</span></span>
- <span data-ttu-id="cec97-2627">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2627">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2628">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2628">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2629">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2629">Allowed From</span></span>

<span data-ttu-id="cec97-2630">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2630">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2631">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2631">Preemption Possible</span></span>

<span data-ttu-id="cec97-2632">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2632">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2633">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2633">Example</span></span>

<span data-ttu-id="cec97-2634">/\* Ricevere un pacchetto dal socket client TCP creato e connesso in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2634">/\* Receive a packet from the previously created and connected TCP client socket.</span></span> <span data-ttu-id="cec97-2635">Se non è disponibile alcun pacchetto, attendere i cicli di 200 timer prima di rinunciare.</span><span class="sxs-lookup"><span data-stu-id="cec97-2635">If no packet is available, wait for 200 timer ticks before giving up.</span></span> <span data-ttu-id="cec97-2636">\*/status = nx_tcp_socket_receive (&client_socket, &packet_ptr, 200);</span><span class="sxs-lookup"><span data-stu-id="cec97-2636">\*/ status = nx_tcp_socket_receive(&client_socket, &packet_ptr, 200);</span></span>

<span data-ttu-id="cec97-2637">/\* Se lo stato è NX_SUCCESS, il pacchetto ricevuto fa riferimento a "packet_ptr".</span><span class="sxs-lookup"><span data-stu-id="cec97-2637">/\* If status is NX_SUCCESS, the received packet is pointed to by "packet_ptr".</span></span> */

### <a name="see-also"></a><span data-ttu-id="cec97-2638">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2638">See Also</span></span>

- <span data-ttu-id="cec97-2639">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2639">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2640">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2640">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2641">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2641">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2642">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2642">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2643">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2643">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2644">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2644">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2645">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2645">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2646">nx_tcp_socket_info_get, nx_tcp_socket_receive_queue_max_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2646">nx_tcp_socket_info_get, nx_tcp_socket_receive_queue_max_set,</span></span>
- <span data-ttu-id="cec97-2647">nx_tcp_socket_send, nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2647">nx_tcp_socket_send, nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_receive_notify"></a><span data-ttu-id="cec97-2648">nx_tcp_socket_receive_notify</span><span class="sxs-lookup"><span data-stu-id="cec97-2648">nx_tcp_socket_receive_notify</span></span>

<span data-ttu-id="cec97-2649">Notificare all'applicazione i pacchetti ricevuti</span><span class="sxs-lookup"><span data-stu-id="cec97-2649">Notify application of received packets</span></span>


### <a name="prototype"></a><span data-ttu-id="cec97-2650">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2650">Prototype</span></span>

```C
UINT nx_tcp_socket_receive_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_receive_notify) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="cec97-2651">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2651">Description</span></span>

<span data-ttu-id="cec97-2652">Questo servizio configura il puntatore della funzione receive Notify con la funzione di callback specificata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2652">This service configures the receive notify function pointer with the callback function specified by the application.</span></span> <span data-ttu-id="cec97-2653">Questa funzione di callback viene quindi chiamata ogni volta che vengono ricevuti uno o più pacchetti nel socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2653">This callback function is then called whenever one or more packets are received on the socket.</span></span> <span data-ttu-id="cec97-2654">Se viene fornito un puntatore NX_NULL, la funzione Notify è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2654">If a NX_NULL pointer is supplied, the notify function is disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2655">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2655">Parameters</span></span>

- <span data-ttu-id="cec97-2656">**socket_ptr** Puntatore al socket TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2656">**socket_ptr** Pointer to the TCP socket.</span></span>
- <span data-ttu-id="cec97-2657">**tcp_receive_notify** Puntatore alla funzione di callback dell'applicazione che viene chiamato quando uno o più pacchetti vengono ricevuti sul socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2657">**tcp_receive_notify** Application callback function pointer that is called when one or more packets are received on the socket.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2658">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2658">Return Values</span></span>

- <span data-ttu-id="cec97-2659">La notifica di ricezione del socket riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2659">**NX_SUCCESS** (0x00) Successful socket receive notify.</span></span>
- <span data-ttu-id="cec97-2660">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2660">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2661">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2661">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2662">La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2662">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2663">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2663">Allowed From</span></span>

<span data-ttu-id="cec97-2664">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2664">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2665">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2665">Preemption Possible</span></span>

<span data-ttu-id="cec97-2666">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2666">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2667">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2667">Example</span></span>

```C
/* Setup a receive packet callback function for the "client_socket"
socket. */
status = nx_tcp_socket_receive_notify(&client_socket,
    my_receive_notify);

/* If status is NX_SUCCESS, NetX will call the function named
    "my_receive_notify" whenever one or more packets are received for
    "client_socket". */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2668">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2668">See Also</span></span>

- <span data-ttu-id="cec97-2669">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2669">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2670">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2670">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="cec97-2671">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2671">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="cec97-2672">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2672">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="cec97-2673">nx_tcp_socket_peer_info_get, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="cec97-2673">nx_tcp_socket_peer_info_get, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="cec97-2674">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="cec97-2674">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="cec97-2675">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2675">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_send"></a><span data-ttu-id="cec97-2676">nx_tcp_socket_send</span><span class="sxs-lookup"><span data-stu-id="cec97-2676">nx_tcp_socket_send</span></span>

<span data-ttu-id="cec97-2677">Inviare dati tramite un socket TCP</span><span class="sxs-lookup"><span data-stu-id="cec97-2677">Send data through a TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2678">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2678">Prototype</span></span>

```C
UINT nx_tcp_socket_send(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-2679">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2679">Description</span></span>

<span data-ttu-id="cec97-2680">Questo servizio invia dati TCP tramite un socket TCP connesso in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2680">This service sends TCP data through a previously connected TCP socket.</span></span> <span data-ttu-id="cec97-2681">Se le ultime dimensioni della finestra annunciata del ricevitore sono inferiori a questa richiesta, il servizio viene sospeso facoltativamente in base all'opzione wait specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2681">If the receiver's last advertised window size is less than this request, the service optionally suspends based on the wait option specified.</span></span> <span data-ttu-id="cec97-2682">Questo servizio garantisce che non vengano inviati dati di pacchetto di dimensioni superiori a MSS al livello IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2682">This service guarantees that no packet data larger than MSS is sent to the IP layer.</span></span>

<span data-ttu-id="cec97-2683">*A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete tenterà anche di rilasciare il pacchetto dopo la trasmissione.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2683">*Unless an error is returned, the application should not release the packet after this call. Doing so will cause unpredictable results because the network driver will also try to release the packet after transmission.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2684">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2684">Parameters</span></span>

- <span data-ttu-id="cec97-2685">**socket_ptr** Puntatore a un'istanza di socket TCP connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2685">**socket_ptr** Pointer to previously connected TCP socket instance.</span></span>
- <span data-ttu-id="cec97-2686">**packet_ptr** Puntatore al pacchetto di dati TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2686">**packet_ptr** TCP data packet pointer.</span></span>
- <span data-ttu-id="cec97-2687">**WAIT_OPTION** Definisce il comportamento del servizio se la richiesta è maggiore delle dimensioni della finestra del destinatario.</span><span class="sxs-lookup"><span data-stu-id="cec97-2687">**wait_option** Defines how the service behaves if the request is greater than the window size of the receiver.</span></span> <span data-ttu-id="cec97-2688">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-2688">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-2689">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2689">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-2690">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-2690">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-2691">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-2691">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2692">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2692">Return Values</span></span>

- <span data-ttu-id="cec97-2693">**NX_SUCCESS** (0x00) del socket inviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2693">**NX_SUCCESS** (0x00) Successful socket send.</span></span>
- <span data-ttu-id="cec97-2694">Il socket **NX_NOT_BOUND** (0x24) non è stato associato ad alcuna porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-2694">**NX_NOT_BOUND** (0x24) Socket was not bound to any port.</span></span>
- <span data-ttu-id="cec97-2695">**NX_NO_INTERFACE_ADDRESS** (0X50) non è stata trovata alcuna interfaccia in uscita adatta.</span><span class="sxs-lookup"><span data-stu-id="cec97-2695">**NX_NO_INTERFACE_ADDRESS** (0x50) No suitable outgoing interface found.</span></span>
- <span data-ttu-id="cec97-2696">Il socket **NX_NOT_CONNECTED** (0x38) non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2696">**NX_NOT_CONNECTED** (0x38) Socket is no longer connected.</span></span>
- <span data-ttu-id="cec97-2697">La richiesta **NX_WINDOW_OVERFLOW** (0x39) è maggiore della dimensione della finestra annunciata del ricevitore in byte.</span><span class="sxs-lookup"><span data-stu-id="cec97-2697">**NX_WINDOW_OVERFLOW** (0x39) Request is greater than receiver’s advertised window size in bytes.</span></span>
- <span data-ttu-id="cec97-2698">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-2698">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-2699">Il pacchetto **NX_INVALID_PACKET** (0x12) non è allocato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2699">**NX_INVALID_PACKET** (0x12) Packet is not allocated.</span></span>
- <span data-ttu-id="cec97-2700">È stata raggiunta la profondità massima della coda di trasmissione **NX_TX_QUEUE_DEPTH** (0x49).</span><span class="sxs-lookup"><span data-stu-id="cec97-2700">**NX_TX_QUEUE_DEPTH** (0x49) Maximum transmit queue depth has been reached.</span></span>
- <span data-ttu-id="cec97-2701">Il puntatore di aggiunta del pacchetto **NX_OVERFLOW** (0x03) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2701">**NX_OVERFLOW** (0x03) Packet append pointer is invalid.</span></span>
- <span data-ttu-id="cec97-2702">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2702">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2703">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2703">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2704">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2704">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-2705">Il puntatore **NX_UNDERFLOW** (0x02) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2705">**NX_UNDERFLOW** (0x02) Packet prepend pointer is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2706">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2706">Allowed From</span></span>

<span data-ttu-id="cec97-2707">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2707">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2708">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2708">Preemption Possible</span></span>

<span data-ttu-id="cec97-2709">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2709">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2710">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2710">Example</span></span>

```C
/* Send a packet out on the previously created and connected TCP
    socket. If the receive window on the other side of the connection
    is less than the packet size, wait 200 timer ticks before giving up. */
status = nx_tcp_socket_send(&client_socket, packet_ptr, 200);

/* If status is NX_SUCCESS, the packet has been sent! */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2711">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2711">See Also</span></span>

- <span data-ttu-id="cec97-2712">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2712">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2713">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2713">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2714">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2714">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2715">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2715">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2716">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2716">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2717">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2717">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2718">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2718">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2719">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2719">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2720">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2720">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_state_wait</span></span>

### <a name="nx_tcp_socket_state_wait"></a><span data-ttu-id="cec97-2721">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="cec97-2721">nx_tcp_socket_state_wait</span></span>

<span data-ttu-id="cec97-2722">Attendere che il socket TCP entri in uno stato specifico</span><span class="sxs-lookup"><span data-stu-id="cec97-2722">Wait for TCP socket to enter specific state</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2723">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2723">Prototype</span></span>

```C
UINT nx_tcp_socket_state_wait(
    NX_TCP_SOCKET *socket_ptr,
    UINT desired_state, 
    ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="cec97-2724">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2724">Description</span></span>

<span data-ttu-id="cec97-2725">Questo servizio attende che il socket entri nello stato desiderato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2725">This service waits for the socket to enter the desired state.</span></span> <span data-ttu-id="cec97-2726">Se il socket non è nello stato desiderato, il servizio viene sospeso in base all'opzione wait specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2726">If the socket is not in the desired state, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2727">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2727">Parameters</span></span>

- <span data-ttu-id="cec97-2728">**socket_ptr** Puntatore a un'istanza di socket TCP connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2728">**socket_ptr** Pointer to previously connected TCP socket instance.</span></span>
- <span data-ttu-id="cec97-2729">**desired_state** Stato TCP desiderato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2729">**desired_state** Desired TCP state.</span></span> <span data-ttu-id="cec97-2730">Gli Stati di socket TCP validi sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-2730">Valid TCP socket states are defined as follows:</span></span>
- <span data-ttu-id="cec97-2731">NX_TCP_CLOSED (0x01)</span><span class="sxs-lookup"><span data-stu-id="cec97-2731">NX_TCP_CLOSED (0x01)</span></span>
- <span data-ttu-id="cec97-2732">NX_TCP_LISTEN_STATE (0x02)</span><span class="sxs-lookup"><span data-stu-id="cec97-2732">NX_TCP_LISTEN_STATE (0x02)</span></span>
- <span data-ttu-id="cec97-2733">NX_TCP_SYN_SENT (0x03)</span><span class="sxs-lookup"><span data-stu-id="cec97-2733">NX_TCP_SYN_SENT (0x03)</span></span>
- <span data-ttu-id="cec97-2734">NX_TCP_SYN_RECEIVED (0x04)</span><span class="sxs-lookup"><span data-stu-id="cec97-2734">NX_TCP_SYN_RECEIVED (0x04)</span></span>
- <span data-ttu-id="cec97-2735">NX_TCP_ESTABLISHED (0x05)</span><span class="sxs-lookup"><span data-stu-id="cec97-2735">NX_TCP_ESTABLISHED (0x05)</span></span>
- <span data-ttu-id="cec97-2736">NX_TCP_CLOSE_WAIT (0x06)</span><span class="sxs-lookup"><span data-stu-id="cec97-2736">NX_TCP_CLOSE_WAIT (0x06)</span></span>
- <span data-ttu-id="cec97-2737">NX_TCP_FIN_WAIT_1 (0x07)</span><span class="sxs-lookup"><span data-stu-id="cec97-2737">NX_TCP_FIN_WAIT_1 (0x07)</span></span>
- <span data-ttu-id="cec97-2738">NX_TCP_FIN_WAIT_2 (0x08)</span><span class="sxs-lookup"><span data-stu-id="cec97-2738">NX_TCP_FIN_WAIT_2 (0x08)</span></span>
- <span data-ttu-id="cec97-2739">NX_TCP_CLOSING (0x09)</span><span class="sxs-lookup"><span data-stu-id="cec97-2739">NX_TCP_CLOSING (0x09)</span></span>
- <span data-ttu-id="cec97-2740">NX_TCP_TIMED_WAIT (0x0A)</span><span class="sxs-lookup"><span data-stu-id="cec97-2740">NX_TCP_TIMED_WAIT (0x0A)</span></span>
- <span data-ttu-id="cec97-2741">NX_TCP_LAST_ACK (0x0B)</span><span class="sxs-lookup"><span data-stu-id="cec97-2741">NX_TCP_LAST_ACK (0x0B)</span></span>
- <span data-ttu-id="cec97-2742">**WAIT_OPTION** Definisce il comportamento del servizio se lo stato richiesto non è presente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2742">**wait_option** Defines how the service behaves if the requested state is not present.</span></span> <span data-ttu-id="cec97-2743">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-2743">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-2744">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2744">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-2745">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-2745">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-2746">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-2746">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2747">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2747">Return Values</span></span>
- <span data-ttu-id="cec97-2748">Attesa stato riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2748">**NX_SUCCESS** (0x00) Successful state wait.</span></span>
- <span data-ttu-id="cec97-2749">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2749">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2750">Lo stato **NX_NOT_SUCCESSFUL** (0x43) non è presente entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2750">**NX_NOT_SUCCESSFUL** (0x43) State not present within the specified wait time.</span></span>
- <span data-ttu-id="cec97-2751">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-2751">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-2752">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2752">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2753">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2753">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-2754">**NX_OPTION_ERROR** (0X0A) lo stato del socket desiderato non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2754">**NX_OPTION_ERROR** (0x0A) The desired socket state is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2755">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2755">Allowed From</span></span>

<span data-ttu-id="cec97-2756">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2756">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2757">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2757">Preemption Possible</span></span>

<span data-ttu-id="cec97-2758">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2758">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2759">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2759">Example</span></span>

```C
/* Wait 300 timer ticks for the previously created socket to enter
    the established state in the TCP state machine. */
status = nx_tcp_socket_state_wait(&client_socket,
    NX_TCP_ESTABLISHED, 300);

/* If status is NX_SUCCESS, the socket is now in the established
    state! */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2760">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2760">See Also</span></span>

- <span data-ttu-id="cec97-2761">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2761">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="cec97-2762">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2762">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2763">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2763">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="cec97-2764">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="cec97-2764">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="cec97-2765">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="cec97-2765">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="cec97-2766">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2766">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2767">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="cec97-2767">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="cec97-2768">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2768">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2769">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send</span><span class="sxs-lookup"><span data-stu-id="cec97-2769">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send</span></span>

## <a name="nx_tcp_socket_timed_wait_callback"></a><span data-ttu-id="cec97-2770">nx_tcp_socket_timed_wait_callback</span><span class="sxs-lookup"><span data-stu-id="cec97-2770">nx_tcp_socket_timed_wait_callback</span></span>

<span data-ttu-id="cec97-2771">Installa callback per lo stato di attesa programmato</span><span class="sxs-lookup"><span data-stu-id="cec97-2771">Install callback for timed wait state</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2772">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2772">Prototype</span></span>

```C
UINT nx_tcp_socket_timed_wait_callback(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_timed_wait_callback) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="cec97-2773">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2773">Description</span></span>

<span data-ttu-id="cec97-2774">Questo servizio registra una funzione di callback che viene richiamata quando il socket TCP è in stato di attesa programmato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2774">This service registers a callback function which is invoked when the TCP socket is in timed wait state.</span></span> <span data-ttu-id="cec97-2775">Per utilizzare questo servizio, è necessario compilare la libreria NetX con l'opzione ***NX_ENABLE_EXTENDED_NOTIFY*** definita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2775">To use this service, the NetX library must be built with the option ***NX_ENABLE_EXTENDED_NOTIFY*** defined.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2776">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2776">Parameters</span></span>

- <span data-ttu-id="cec97-2777">**socket_ptr** Puntatore a un'istanza del client o del socket del server connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2777">**socket_ptr** Pointer to previously connected client or server socket instance.</span></span>
- <span data-ttu-id="cec97-2778">**tcp_timed_wait_callback** Funzione di callback Wait temporizzata</span><span class="sxs-lookup"><span data-stu-id="cec97-2778">**tcp_timed_wait_callback** The timed wait callback function</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2779">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2779">Return Values</span></span>

- <span data-ttu-id="cec97-2780">**NX_SUCCESS** (0x00) registra correttamente il socket della funzione di callback</span><span class="sxs-lookup"><span data-stu-id="cec97-2780">**NX_SUCCESS** (0x00) Successfully registers the callback function socket</span></span>
- <span data-ttu-id="cec97-2781">La libreria NetX **NX_NOT_SUPPORTED** (0x4B) viene compilata senza la funzionalità di notifica estesa abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2781">**NX_NOT_SUPPORTED** (0x4B) NetX library is built without the extended notify feature enabled.</span></span>
- <span data-ttu-id="cec97-2782">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2782">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2783">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2783">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2784">La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2784">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2785">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2785">Allowed From</span></span>

<span data-ttu-id="cec97-2786">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2786">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2787">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2787">Preemption Possible</span></span>

<span data-ttu-id="cec97-2788">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2788">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2789">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2789">Example</span></span>

```C
/* Install the timed wait callback function */
nx_tcp_socket_timed_wait_callback(&client_socket, callback);
```

### <a name="see-also"></a><span data-ttu-id="cec97-2790">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2790">See Also</span></span>

- <span data-ttu-id="cec97-2791">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2791">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2792">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2792">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="cec97-2793">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2793">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="cec97-2794">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2794">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="cec97-2795">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2795">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-2796">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="cec97-2796">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="cec97-2797">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2797">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_transmit_configure"></a><span data-ttu-id="cec97-2798">nx_tcp_socket_transmit_configure</span><span class="sxs-lookup"><span data-stu-id="cec97-2798">nx_tcp_socket_transmit_configure</span></span>

<span data-ttu-id="cec97-2799">Configurare i parametri di trasmissione del socket</span><span class="sxs-lookup"><span data-stu-id="cec97-2799">Configure socket's transmit parameters</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2800">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2800">Prototype</span></span>

```C
UINT nx_tcp_socket_transmit_configure(
    NX_TCP_SOCKET *socket_ptr,
    ULONG max_queue_depth,
    ULONG timeout,
    ULONG max_retries,
    ULONG timeout_shift);
```

### <a name="description"></a><span data-ttu-id="cec97-2801">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2801">Description</span></span>

<span data-ttu-id="cec97-2802">Questo servizio configura vari parametri di trasmissione del socket TCP specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2802">This service configures various transmit parameters of the specified TCP socket.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2803">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2803">Parameters</span></span>

- <span data-ttu-id="cec97-2804">**socket_ptr** Puntatore al socket TCP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2804">**socket_ptr** Pointer to the TCP socket.</span></span>
- <span data-ttu-id="cec97-2805">**max_queue_depth** Numero massimo di pacchetti che possono essere accodati per la trasmissione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2805">**max_queue_depth** Maximum number of packets allowed to be queued for transmission.</span></span>
- <span data-ttu-id="cec97-2806">**timeout** Numero di cicli del timer ThreadX in attesa di un ACK prima che il pacchetto venga nuovamente inviato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2806">**timeout** Number of ThreadX timer ticks an ACK is waited for before the packet is sent again.</span></span>
- <span data-ttu-id="cec97-2807">**max_retries** Numero massimo di tentativi consentiti.</span><span class="sxs-lookup"><span data-stu-id="cec97-2807">**max_retries** Maximum number of retries allowed.</span></span>
- <span data-ttu-id="cec97-2808">**timeout_shift** Valore per spostare il timeout per ogni nuovo tentativo successivo.</span><span class="sxs-lookup"><span data-stu-id="cec97-2808">**timeout_shift** Value to shift the timeout for each subsequent retry.</span></span> <span data-ttu-id="cec97-2809">Il valore 0 comporta lo stesso timeout tra i tentativi successivi.</span><span class="sxs-lookup"><span data-stu-id="cec97-2809">A value of 0, results in the same timeout between successive retries.</span></span> <span data-ttu-id="cec97-2810">Il valore 1, raddoppia il timeout tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="cec97-2810">A value of 1, doubles the timeout between retries.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2811">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2811">Return Values</span></span>
- <span data-ttu-id="cec97-2812">Configurazione socket di trasmissione riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2812">**NX_SUCCESS** (0x00) Successful transmit socket configure.</span></span>
- <span data-ttu-id="cec97-2813">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2813">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-2814">Opzione profondità coda non valida **NX_OPTION_ERROR** (0x0A).</span><span class="sxs-lookup"><span data-stu-id="cec97-2814">**NX_OPTION_ERROR** (0x0a) Invalid queue depth option.</span></span>
- <span data-ttu-id="cec97-2815">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2815">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2816">La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2816">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2817">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2817">Allowed From</span></span>

<span data-ttu-id="cec97-2818">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2818">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2819">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2819">Preemption Possible</span></span>

<span data-ttu-id="cec97-2820">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2820">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2821">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2821">Example</span></span>

```C
/* Configure the "client_socket" for a maximum transmit queue depth
    of 12, 100 tick timeouts, a maximum of 20 retries, and a timeout
    double on each successive retry. */
status = nx_tcp_socket_transmit_configure(&client_socket,
    12,100,20, 1);

/* If status is NX_SUCCESS, the socket’s transmit retry has been
    configured. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2822">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2822">See Also</span></span>

- <span data-ttu-id="cec97-2823">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2823">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2824">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2824">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="cec97-2825">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2825">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="cec97-2826">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2826">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="cec97-2827">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2827">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-2828">nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="cec97-2828">nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="cec97-2829">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2829">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_window_update_notify_set"></a><span data-ttu-id="cec97-2830">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="cec97-2830">nx_tcp_socket_window_update_notify_set</span></span>

<span data-ttu-id="cec97-2831">Notifica dell'applicazione degli aggiornamenti delle dimensioni della finestra</span><span class="sxs-lookup"><span data-stu-id="cec97-2831">Notify application of window size updates</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2832">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2832">Prototype</span></span>

```C
UINT nx_tcp_socket_window_update_notify_set(
    NX_TCP_SOCKET
    *socket_ptr,
    VOID (*tcp_window_update_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="cec97-2833">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2833">Description</span></span>

<span data-ttu-id="cec97-2834">Questo servizio installa una routine di callback di aggiornamento della finestra del socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2834">This service installs a socket window update callback routine.</span></span> <span data-ttu-id="cec97-2835">Questa routine viene chiamata automaticamente ogni volta che il socket specificato riceve un pacchetto che indica un aumento delle dimensioni della finestra dell'host remoto.</span><span class="sxs-lookup"><span data-stu-id="cec97-2835">This routine is called automatically whenever the specified socket receives a packet indicating an increase in the window size of the remote host.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2836">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2836">Parameters</span></span>

- <span data-ttu-id="cec97-2837">**socket_ptr** Puntatore al socket TCP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2837">**socket_ptr** Pointer to previously created TCP socket.</span></span>
- <span data-ttu-id="cec97-2838">**tcp_window_update_notify** Routine di callback da chiamare quando cambiano le dimensioni della finestra.</span><span class="sxs-lookup"><span data-stu-id="cec97-2838">**tcp_window_update_notify** Callback routine to be called when the window size changes.</span></span> <span data-ttu-id="cec97-2839">Il valore NULL disabilita l'aggiornamento delle modifiche della finestra.</span><span class="sxs-lookup"><span data-stu-id="cec97-2839">A value of NULL disables the window change update.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2840">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2840">Return Values</span></span>
- <span data-ttu-id="cec97-2841">Nel socket è installata la routine di callback **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-2841">**NX_SUCCESS** (0x00) Callback routine is installed on the socket.</span></span>
- <span data-ttu-id="cec97-2842">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2842">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2843">**NX_PTR_ERROR** (0x07) puntatori non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-2843">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="cec97-2844">La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2844">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="cec97-2845">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2845">Allowed From</span></span>

<span data-ttu-id="cec97-2846">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2846">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2847">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2847">Preemption Possible</span></span>

<span data-ttu-id="cec97-2848">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2848">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2849">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2849">Example</span></span>

```C
/* Set the function pointer to the windows update callback after creating the
socket. */
status = nx_tcp_socket_window_update_notify_set(&data_socket,
    my_windows_update_callback);

/* Define the window callback function in the host application. */
void my_windows_update_callback(NX_TCP_SCOCKET *data_socket)
{
    /* Process update on increase TCP transmit socket window size. */
    return;
}
```

### <a name="see-also"></a><span data-ttu-id="cec97-2850">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2850">See Also</span></span>

- <span data-ttu-id="cec97-2851">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-2851">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="cec97-2852">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2852">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="cec97-2853">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2853">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="cec97-2854">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="cec97-2854">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="cec97-2855">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-2855">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-2856">nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure</span><span class="sxs-lookup"><span data-stu-id="cec97-2856">nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure</span></span>

## <a name="nx_udp_enable"></a><span data-ttu-id="cec97-2857">nx_udp_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-2857">nx_udp_enable</span></span>

<span data-ttu-id="cec97-2858">Abilita componente UDP di NetX</span><span class="sxs-lookup"><span data-stu-id="cec97-2858">Enable UDP component of NetX</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2859">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2859">Prototype</span></span>

```C
UINT nx_udp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-2860">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2860">Description</span></span>

<span data-ttu-id="cec97-2861">Questo servizio Abilita il componente UDP (User Datagram Protocol) di NetX.</span><span class="sxs-lookup"><span data-stu-id="cec97-2861">This service enables the User Datagram Protocol (UDP) component of NetX.</span></span> <span data-ttu-id="cec97-2862">Dopo l'abilitazione, i datagrammi UDP possono essere inviati e ricevuti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2862">After enabled, UDP datagrams may be sent and received by the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2863">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2863">Parameters</span></span>

- <span data-ttu-id="cec97-2864">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2864">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2865">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2865">Return Values</span></span>

- <span data-ttu-id="cec97-2866">**NX_SUCCESS** (0x00) Enable UDP riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-2866">**NX_SUCCESS** (0x00) Successful UDP enable.</span></span>
- <span data-ttu-id="cec97-2867">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2867">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-2868">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2868">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2869">**NX_ALREADY_ENABLED** (0X15) questo componente è già stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2869">**NX_ALREADY_ENABLED** (0x15) This component has already been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2870">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2870">Allowed From</span></span>

<span data-ttu-id="cec97-2871">Inizializzazione, thread, timer</span><span class="sxs-lookup"><span data-stu-id="cec97-2871">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2872">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2872">Preemption Possible</span></span>

<span data-ttu-id="cec97-2873">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2873">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2874">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2874">Example</span></span>

```C
/* Enable UDP on the previously created IP instance. */
status = nx_udp_enable(&ip_0);

/* If status is NX_SUCCESS, UDP is now enabled on the specified IP
    instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2875">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2875">See Also</span></span>

- <span data-ttu-id="cec97-2876">nx_udp_free_port_find, nx_udp_info_get, nx_udp_packet_info_extract,</span><span class="sxs-lookup"><span data-stu-id="cec97-2876">nx_udp_free_port_find, nx_udp_info_get, nx_udp_packet_info_extract,</span></span>
- <span data-ttu-id="cec97-2877">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2877">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2878">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-2878">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="cec97-2879">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2879">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-2880">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2880">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2881">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2881">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-2882">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2882">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2883">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-2883">nx_udp_source_extract</span></span>

## <a name="nx_udp_free_port_find"></a><span data-ttu-id="cec97-2884">nx_udp_free_port_find</span><span class="sxs-lookup"><span data-stu-id="cec97-2884">nx_udp_free_port_find</span></span>

<span data-ttu-id="cec97-2885">Trova la porta UDP successiva disponibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2885">Find next available UDP port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2886">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2886">Prototype</span></span>

```C
UINT nx_udp_free_port_find(
    NX_IP *ip_ptr, 
    UINT port,
    UINT *free_port_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-2887">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2887">Description</span></span>

<span data-ttu-id="cec97-2888">Questo servizio cerca una porta UDP gratuita (senza binding) a partire dal numero di porta fornito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2888">This service looks for a free UDP port (unbound) starting from the application supplied port number.</span></span> <span data-ttu-id="cec97-2889">Se la ricerca raggiunge il valore massimo della porta di 0xFFFF, viene eseguito il wrapping della logica di ricerca.</span><span class="sxs-lookup"><span data-stu-id="cec97-2889">The search logic will wrap around if the search reaches the maximum port value of 0xFFFF.</span></span> <span data-ttu-id="cec97-2890">Se la ricerca ha esito positivo, la porta libera viene restituita nella variabile a cui punta *free_port_ptr*.</span><span class="sxs-lookup"><span data-stu-id="cec97-2890">If the search is successful, the free port is returned in the variable pointed to by *free_port_ptr*.</span></span>

<span data-ttu-id="cec97-2891">*Questo servizio può essere chiamato da un altro thread e può avere la stessa porta restituita. Per evitare questo race condition, è possibile che l'applicazione inserisca il servizio e il socket effettivo associato alla protezione di un mutex.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2891">*This service can be called from another thread and can have the same port returned. To prevent this race condition, the application may wish to place this service and the actual socket bind under the protection of a mutex.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2892">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2892">Parameters</span></span>

- <span data-ttu-id="cec97-2893">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2893">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-2894">**porta** Numero di porta da cui iniziare la ricerca (da 1 a 0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-2894">**port** Port number to start search (1 through 0xFFFF).</span></span>
- <span data-ttu-id="cec97-2895">**free_port_ptr** Puntatore alla variabile di restituzione della porta libera di destinazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2895">**free_port_ptr** Pointer to the destination free port return variable.</span></span>


### <a name="return-values"></a><span data-ttu-id="cec97-2896">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2896">Return Values</span></span>

- <span data-ttu-id="cec97-2897">**NX_SUCCESS** (0x00) riuscite dalla porta libera.</span><span class="sxs-lookup"><span data-stu-id="cec97-2897">**NX_SUCCESS** (0x00) Successful free port find.</span></span>
- <span data-ttu-id="cec97-2898">**NX_NO_FREE_PORTS** (0X45) non sono state trovate porte gratuite.</span><span class="sxs-lookup"><span data-stu-id="cec97-2898">**NX_NO_FREE_PORTS** (0x45) No free ports found.</span></span>
- <span data-ttu-id="cec97-2899">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2899">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-2900">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2900">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2901">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2901">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="cec97-2902">Il numero di porta specificato **NX_INVALID_PORT** (0x46) non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2902">**NX_INVALID_PORT** (0x46) Specified port number is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2903">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2903">Allowed From</span></span>

<span data-ttu-id="cec97-2904">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2904">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2905">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2905">Preemption Possible</span></span>

<span data-ttu-id="cec97-2906">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2906">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2907">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2907">Example</span></span>

```C
/* Locate a free UDP port, starting at port 12, on a previously
    created IP instance. */
status = nx_udp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS pointer, "free_port" identifies the next
    free UDP port on the IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2908">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2908">See Also</span></span>

- <span data-ttu-id="cec97-2909">nx_udp_enable, nx_udp_info_get, nx_udp_packet_info_extract,</span><span class="sxs-lookup"><span data-stu-id="cec97-2909">nx_udp_enable, nx_udp_info_get, nx_udp_packet_info_extract,</span></span>
- <span data-ttu-id="cec97-2910">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2910">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2911">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-2911">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="cec97-2912">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2912">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-2913">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2913">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2914">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2914">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-2915">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2915">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2916">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-2916">nx_udp_source_extract</span></span>

## <a name="nx_udp_info_get"></a><span data-ttu-id="cec97-2917">nx_udp_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-2917">nx_udp_info_get</span></span>

<span data-ttu-id="cec97-2918">Recuperare informazioni sulle attività UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-2918">Retrieve information about UDP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2919">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2919">Prototype</span></span>

```C
UINT nx_udp_info_get(
    NX_IP *ip_ptr,
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_invalid_packets,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
```

### <a name="description"></a><span data-ttu-id="cec97-2920">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2920">Description</span></span>

<span data-ttu-id="cec97-2921">Questo servizio recupera informazioni sulle attività UDP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2921">This service retrieves information about UDP activities for the specified IP instance.</span></span>

<span data-ttu-id="cec97-2922">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-2922">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2923">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2923">Parameters</span></span>

- <span data-ttu-id="cec97-2924">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2924">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-2925">**udp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti UDP inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-2925">**udp_packets_sent** Pointer to destination for the total number of UDP packets sent.</span></span>
- <span data-ttu-id="cec97-2926">**udp_bytes_sent** Puntatore alla destinazione per il numero totale di byte UDP inviati.</span><span class="sxs-lookup"><span data-stu-id="cec97-2926">**udp_bytes_sent** Pointer to destination for the total number of UDP bytes sent.</span></span>
- <span data-ttu-id="cec97-2927">**udp_packets_received** Puntatore alla destinazione del numero totale di pacchetti UDP ricevuti.</span><span class="sxs-lookup"><span data-stu-id="cec97-2927">**udp_packets_received** Pointer to destination of the total number of UDP packets received.</span></span>
- <span data-ttu-id="cec97-2928">**udp_bytes_received** Puntatore alla destinazione del numero totale di byte UDP ricevuti.</span><span class="sxs-lookup"><span data-stu-id="cec97-2928">**udp_bytes_received** Pointer to destination of the total number of UDP bytes received.</span></span>
- <span data-ttu-id="cec97-2929">**udp_invalid_packets** Puntatore alla destinazione del numero totale di pacchetti UDP non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-2929">**udp_invalid_packets** Pointer to destination of the total number of invalid UDP packets.</span></span>
- <span data-ttu-id="cec97-2930">**udp_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione UDP eliminati.</span><span class="sxs-lookup"><span data-stu-id="cec97-2930">**udp_receive_packets_dropped** Pointer to destination of the total number of UDP receive packets dropped.</span></span>
- <span data-ttu-id="cec97-2931">**udp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti UDP con errori di checksum.</span><span class="sxs-lookup"><span data-stu-id="cec97-2931">**udp_checksum_errors** Pointer to destination of the total number of UDP packets with checksum errors.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2932">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2932">Return Values</span></span>

- <span data-ttu-id="cec97-2933">**NX_SUCCESS** (0x00) il recupero delle informazioni UDP è riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-2933">**NX_SUCCESS** (0x00) Successful UDP information retrieval.</span></span>
- <span data-ttu-id="cec97-2934">**NX_PTR_ERROR** (0x07) puntatore IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-2934">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="cec97-2935">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2935">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-2936">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-2936">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="cec97-2937">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2937">Allowed From</span></span>

<span data-ttu-id="cec97-2938">Inizializzazione, thread e timer</span><span class="sxs-lookup"><span data-stu-id="cec97-2938">Initialization, threads, and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2939">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2939">Preemption Possible</span></span>

<span data-ttu-id="cec97-2940">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2940">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2941">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2941">Example</span></span>

```C
/* Retrieve UDP information from previously created IP Instance ip_0. */
status = nx_udp_info_get(&ip_0, &udp_packets_sent,
    &udp_bytes_sent,
    &udp_packets_received,
    &udp_bytes_received,
    &udp_invalid_packets,
    &udp_receive_packets_dropped,
    &udp_checksum_errors);

/* If status is NX_SUCCESS, UDP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2942">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2942">See Also</span></span>

- <span data-ttu-id="cec97-2943">nx_udp_enable, nx_udp_free_port_find, nx_udp_packet_info_extract,</span><span class="sxs-lookup"><span data-stu-id="cec97-2943">nx_udp_enable, nx_udp_free_port_find, nx_udp_packet_info_extract,</span></span>
- <span data-ttu-id="cec97-2944">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2944">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2945">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-2945">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="cec97-2946">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2946">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-2947">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2947">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2948">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2948">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-2949">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2949">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2950">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-2950">nx_udp_source_extract</span></span>

## <a name="nx_udp_packet_info_extract"></a><span data-ttu-id="cec97-2951">nx_udp_packet_info_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-2951">nx_udp_packet_info_extract</span></span>

<span data-ttu-id="cec97-2952">Estrai parametri di rete dal pacchetto UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-2952">Extract network parameters from UDP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2953">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2953">Prototype</span></span>

```C
UINT nx_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address,
    UINT *protocol,
    UINT *port,
    UINT *interface_index);
```

### <a name="description"></a><span data-ttu-id="cec97-2954">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2954">Description</span></span>

<span data-ttu-id="cec97-2955">Questo servizio estrae i parametri di rete, ad esempio indirizzo IP, numero di porta peer, tipo di protocollo (questo servizio restituisce sempre il tipo UDP) da un pacchetto ricevuto su un'interfaccia in ingresso.</span><span class="sxs-lookup"><span data-stu-id="cec97-2955">This service extracts network parameters, such as IP address, peer port number, protocol type (this service always returns UDP type) from a packet received on an incoming interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2956">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2956">Parameters</span></span>

- <span data-ttu-id="cec97-2957">**packet_ptr** Puntatore al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-2957">**packet_ptr** Pointer to packet.</span></span>
- <span data-ttu-id="cec97-2958">**ip_address** Puntatore all'indirizzo IP del mittente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2958">**ip_address** Pointer to sender IP address.</span></span>
- <span data-ttu-id="cec97-2959">**protocollo** di Puntatore a protocollo (UDP).</span><span class="sxs-lookup"><span data-stu-id="cec97-2959">**protocol** Pointer to protocol (UDP).</span></span>
- <span data-ttu-id="cec97-2960">**porta** Puntatore al numero di porta del mittente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2960">**port** Pointer to sender’s port number.</span></span>
- <span data-ttu-id="cec97-2961">**interface_index** Puntatore all'indice dell'interfaccia ricevente.</span><span class="sxs-lookup"><span data-stu-id="cec97-2961">**interface_index** Pointer to receiving interface index.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2962">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2962">Return Values</span></span>

- <span data-ttu-id="cec97-2963">Estrazione dei dati dell'interfaccia di pacchetti **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2963">**NX_SUCCESS** (0x00) Packet interface data successfully extracted.</span></span>
- <span data-ttu-id="cec97-2964">Il pacchetto **NX_INVALID_PACKET** (0x12) non contiene un frame IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-2964">**NX_INVALID_PACKET** (0x12) Packet does not contain IP frame.</span></span>
- <span data-ttu-id="cec97-2965">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="cec97-2965">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="cec97-2966">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-2966">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-2967">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-2967">Allowed From</span></span>

<span data-ttu-id="cec97-2968">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-2968">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-2969">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-2969">Preemption Possible</span></span>

<span data-ttu-id="cec97-2970">No</span><span class="sxs-lookup"><span data-stu-id="cec97-2970">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-2971">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-2971">Example</span></span>

```C
/* Extract network data from UDP packet interface.*/
status = nx_udp_packet_info_extract( packet_ptr, &ip_address,
    &protocol, &port,
    &interface_index);

/* If status is NX_SUCCESS packet data was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-2972">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-2972">See Also</span></span>

- <span data-ttu-id="cec97-2973">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2973">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-2974">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-2974">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-2975">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-2975">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="cec97-2976">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-2976">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-2977">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-2977">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-2978">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-2978">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-2979">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-2979">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-2980">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-2980">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_bind"></a><span data-ttu-id="cec97-2981">nx_udp_socket_bind</span><span class="sxs-lookup"><span data-stu-id="cec97-2981">nx_udp_socket_bind</span></span>

<span data-ttu-id="cec97-2982">Associa socket UDP a porta UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-2982">Bind UDP socket to UDP port</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-2983">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-2983">Prototype</span></span>

```C
UINT nx_udp_socket_bind(
    NX_UDP_SOCKET *socket_ptr, 
    UINT port,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-2984">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-2984">Description</span></span>

<span data-ttu-id="cec97-2985">Questo servizio associa il socket UDP creato in precedenza alla porta UDP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-2985">This service binds the previously created UDP socket to the specified UDP port.</span></span> <span data-ttu-id="cec97-2986">I socket UDP validi sono compresi tra 0 e 0xFFFF.</span><span class="sxs-lookup"><span data-stu-id="cec97-2986">Valid UDP sockets range from 0 through 0xFFFF.</span></span> <span data-ttu-id="cec97-2987">Se il numero di porta richiesto è associato a un altro socket, il servizio attende il periodo di tempo specificato affinché il socket venga dissociato dal numero di porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-2987">If the requested port number is bound to another socket, this service waits for specified period of time for the socket to unbind from the port number.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-2988">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-2988">Parameters</span></span>

- <span data-ttu-id="cec97-2989">**socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-2989">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>
- <span data-ttu-id="cec97-2990">**porta** Numero di porta da associare (da 1 a 0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-2990">**port** Port number to bind to (1 through 0xFFFF).</span></span> <span data-ttu-id="cec97-2991">Se il numero di porta è NX_ANY_PORT (0x0000), l'istanza IP cercherà la porta libera successiva e la utilizzerà per l'associazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-2991">If port number is NX_ANY_PORT (0x0000), the IP instance will search for the next free port and use that for the binding.</span></span>
- <span data-ttu-id="cec97-2992">**WAIT_OPTION** Definisce il comportamento del servizio se la porta è già associata a un altro socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-2992">**wait_option** Defines how the service behaves if the port is already bound to another socket.</span></span> <span data-ttu-id="cec97-2993">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-2993">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-2994">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-2994">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-2995">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-2995">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-2996">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-2996">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-2997">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-2997">Return Values</span></span>

- <span data-ttu-id="cec97-2998">**NX_SUCCESS** (0x00) associazione Socket riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-2998">**NX_SUCCESS** (0x00) Successful socket bind.</span></span>
- <span data-ttu-id="cec97-2999">**NX_ALREADY_BOUND** (0X22) questo socket è già associato a un'altra porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-2999">**NX_ALREADY_BOUND** (0x22) This socket is already bound to another port.</span></span>
- <span data-ttu-id="cec97-3000">La porta **NX_PORT_UNAVAILABLE** (0x23) è già associata a un socket diverso.</span><span class="sxs-lookup"><span data-stu-id="cec97-3000">**NX_PORT_UNAVAILABLE** (0x23) Port is already bound to a different socket.</span></span>
- <span data-ttu-id="cec97-3001">**NX_NO_FREE_PORTS** (0X45) non è disponibile alcuna porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-3001">**NX_NO_FREE_PORTS** (0x45) No free port.</span></span>
- <span data-ttu-id="cec97-3002">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="cec97-3002">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="cec97-3003">La porta **NX_INVALID_PORT** (0x46) specificata non è valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-3003">**NX_INVALID_PORT** (0x46) Invalid port specified.</span></span>
- <span data-ttu-id="cec97-3004">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3004">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-3005">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3005">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3006">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3006">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3007">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3007">Allowed From</span></span>

<span data-ttu-id="cec97-3008">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3008">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3009">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3009">Preemption Possible</span></span>

<span data-ttu-id="cec97-3010">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3010">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3011">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3011">Example</span></span>

```C
/* Bind the previously created UDP socket to port 12 on the
    previously created IP instance. If the port is already bound,
    wait for 300 timer ticks before giving up. */
status = nx_udp_socket_bind(&udp_socket, 12, 300);

/* If status is NX_SUCCESS, the UDP socket is now bound to
    port 12.*/
```

### <a name="see-also"></a><span data-ttu-id="cec97-3012">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3012">See Also</span></span>

- <span data-ttu-id="cec97-3013">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3013">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3014">nx_udp_packet_info_extract, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="cec97-3014">nx_udp_packet_info_extract, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="cec97-3015">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3015">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="cec97-3016">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3016">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3017">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-3017">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-3018">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3018">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-3019">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3019">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-3020">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3020">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_bytes_available"></a><span data-ttu-id="cec97-3021">nx_udp_socket_bytes_available</span><span class="sxs-lookup"><span data-stu-id="cec97-3021">nx_udp_socket_bytes_available</span></span>

<span data-ttu-id="cec97-3022">Recupera il numero di byte disponibili per il recupero</span><span class="sxs-lookup"><span data-stu-id="cec97-3022">Retrieves number of bytes available for retrieval</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3023">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3023">Prototype</span></span>

```C
UINT nx_udp_socket_bytes_available(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```

### <a name="description"></a><span data-ttu-id="cec97-3024">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3024">Description</span></span>

<span data-ttu-id="cec97-3025">Questo servizio recupera il numero di byte disponibili per la ricezione nel socket UDP specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3025">This service retrieves number of bytes available for reception in the specified UDP socket.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3026">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3026">Parameters</span></span>

- <span data-ttu-id="cec97-3027">**socket_ptr** Puntatore al socket UDP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3027">**socket_ptr** Pointer to previously created UDP socket.</span></span>
- <span data-ttu-id="cec97-3028">**bytes_available** Puntatore alla destinazione per byte disponibili.</span><span class="sxs-lookup"><span data-stu-id="cec97-3028">**bytes_available** Pointer to destination for bytes available.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3029">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3029">Return Values</span></span>

- <span data-ttu-id="cec97-3030">**NX_SUCCESS** (0x00) byte riusciti di recupero disponibili.</span><span class="sxs-lookup"><span data-stu-id="cec97-3030">**NX_SUCCESS** (0x00) Successful bytes available retrieval.</span></span>
- <span data-ttu-id="cec97-3031">Il socket **NX_NOT_SUCCESSFUL** (0x43) non è associato a una porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-3031">**NX_NOT_SUCCESSFUL** (0x43) Socket not bound to a port.</span></span>
- <span data-ttu-id="cec97-3032">**NX_PTR_ERROR** (0x07) puntatori non validi.</span><span class="sxs-lookup"><span data-stu-id="cec97-3032">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="cec97-3033">La funzionalità UDP **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-3033">**NX_NOT_ENABLED** (0x14) UDP feature is not enabled.</span></span>
- <span data-ttu-id="cec97-3034">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3034">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3035">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3035">Allowed From</span></span>

<span data-ttu-id="cec97-3036">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3036">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3037">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3037">Preemption Possible</span></span>

<span data-ttu-id="cec97-3038">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3038">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3039">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3039">Example</span></span>

```C
/* Get the bytes available for retrieval from the UDP socket. */
status = nx_udp_socket_bytes_available(&my_socket, &bytes_available);

/* If status == NX_SUCCESS, the number of bytes was successfully
    retrieved.*/
```

### <a name="see-also"></a><span data-ttu-id="cec97-3040">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3040">See Also</span></span>

- <span data-ttu-id="cec97-3041">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3041">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3042">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3042">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3043">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3043">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="cec97-3044">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3044">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3045">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-3045">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-3046">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3046">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-3047">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3047">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-3048">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3048">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_checksum_disable"></a><span data-ttu-id="cec97-3049">nx_udp_socket_checksum_disable</span><span class="sxs-lookup"><span data-stu-id="cec97-3049">nx_udp_socket_checksum_disable</span></span>

<span data-ttu-id="cec97-3050">Disabilitare il checksum per il socket UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3050">Disable checksum for UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3051">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3051">Prototype</span></span>

```C
UINT nx_udp_socket_checksum_disable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-3052">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3052">Description</span></span>

<span data-ttu-id="cec97-3053">Questo servizio Disabilita la logica di checksum per l'invio e la ricezione di pacchetti sul socket UDP specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3053">This service disables the checksum logic for sending and receiving packets on the specified UDP socket.</span></span> <span data-ttu-id="cec97-3054">Quando la logica di checksum è disabilitata, il valore zero viene caricato nel campo checksum dell'intestazione UDP per tutti i pacchetti inviati tramite questo socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3054">When the checksum logic is disabled, a value of zero is loaded into the UDP header's checksum field for all packets sent through this socket.</span></span> <span data-ttu-id="cec97-3055">Un valore di checksum con valore zero nell'intestazione UDP segnala al ricevitore che checksum non viene calcolato per questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-3055">A zero-value checksum value in the UDP header signals the receiver that checksum is not computed for this packet.</span></span>

<span data-ttu-id="cec97-3056">Si noti inoltre che questa operazione non ha effetto se vengono definiti ***NX_DISABLE_UDP_RX_CHECKSUM** _ e _ *_NX_DISABLE_UDP_TX_CHECKSUM_** durante la ricezione e l'invio di pacchetti UDP rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-3056">Also note that this has no effect if ***NX_DISABLE_UDP_RX_CHECKSUM** _ and _ *_NX_DISABLE_UDP_TX_CHECKSUM_** are defined when receiving and sending UDP packets respectively.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3057">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3057">Parameters</span></span>

- <span data-ttu-id="cec97-3058">**socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3058">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3059">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3059">Return Values</span></span>

- <span data-ttu-id="cec97-3060">**NX_SUCCESS** (0x00) disabilitato checksum del socket riuscito.</span><span class="sxs-lookup"><span data-stu-id="cec97-3060">**NX_SUCCESS** (0x00) Successful socket checksum disable.</span></span>
- <span data-ttu-id="cec97-3061">Il socket **NX_NOT_BOUND** (0x24) non è associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3061">**NX_NOT_BOUND** (0x24) Socket is not bound.</span></span>
- <span data-ttu-id="cec97-3062">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3062">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-3063">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3063">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3064">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3064">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3065">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3065">Allowed From</span></span>

<span data-ttu-id="cec97-3066">Inizializzazione, thread, timer</span><span class="sxs-lookup"><span data-stu-id="cec97-3066">Initialization, threads, timer</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3067">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3067">Preemption Possible</span></span>

<span data-ttu-id="cec97-3068">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3068">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3069">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3069">Example</span></span>

```C
/* Disable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_disable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will not have a checksum
    calculated. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3070">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3070">See Also</span></span>

- <span data-ttu-id="cec97-3071">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3071">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3072">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3072">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3073">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3073">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3074">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3074">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3075">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-3075">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-3076">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3076">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-3077">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3077">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-3078">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3078">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_checksum_enable"></a><span data-ttu-id="cec97-3079">nx_udp_socket_checksum_enable</span><span class="sxs-lookup"><span data-stu-id="cec97-3079">nx_udp_socket_checksum_enable</span></span>

<span data-ttu-id="cec97-3080">Abilita checksum per socket UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3080">Enable checksum for UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3081">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3081">Prototype</span></span>

```C
UINT nx_udp_socket_checksum_enable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-3082">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3082">Description</span></span>

<span data-ttu-id="cec97-3083">Questo servizio Abilita la logica di checksum per l'invio e la ricezione di pacchetti sul socket UDP specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3083">This service enables the checksum logic for sending and receiving packets on the specified UDP socket.</span></span> <span data-ttu-id="cec97-3084">Il checksum copre l'intera area dati UDP e un'intestazione pseudo-IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3084">The checksum covers the entire UDP data area as well as a pseudo IP header.</span></span>

<span data-ttu-id="cec97-3085">Si noti inoltre che questa operazione non ha effetto se vengono definiti **NX_DISABLE_UDP_RX_CHECKSUM** e **NX_DISABLE_UDP_TX_CHECKSUM** durante la ricezione e l'invio di pacchetti UDP rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-3085">Also note that this has no effect if **NX_DISABLE_UDP_RX_CHECKSUM** and **NX_DISABLE_UDP_TX_CHECKSUM** are defined when receiving and sending UDP packets respectively.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3086">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3086">Parameters</span></span>

- <span data-ttu-id="cec97-3087">**socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3087">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3088">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3088">Return Values</span></span>

- <span data-ttu-id="cec97-3089">Abilitazione del checksum del socket **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-3089">**NX_SUCCESS** (0x00) Successful socket checksum enable.</span></span>
- <span data-ttu-id="cec97-3090">Il socket **NX_NOT_BOUND** (0x24) non è associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3090">**NX_NOT_BOUND** (0x24) Socket is not bound.</span></span>
- <span data-ttu-id="cec97-3091">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3091">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-3092">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3092">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3093">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3093">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3094">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3094">Allowed From</span></span>

<span data-ttu-id="cec97-3095">Inizializzazione, thread, timer</span><span class="sxs-lookup"><span data-stu-id="cec97-3095">Initialization, threads, timer</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3096">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3096">Preemption Possible</span></span>

<span data-ttu-id="cec97-3097">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3097">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3098">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3098">Example</span></span>

```C
/* Enable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_enable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will have a checksum
    calculated. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3099">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3099">See Also</span></span>

- <span data-ttu-id="cec97-3100">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3100">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3101">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3101">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3102">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3102">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3103">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3103">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3104">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-3104">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-3105">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3105">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-3106">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3106">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-3107">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3107">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_create"></a><span data-ttu-id="cec97-3108">nx_udp_socket_create</span><span class="sxs-lookup"><span data-stu-id="cec97-3108">nx_udp_socket_create</span></span>

<span data-ttu-id="cec97-3109">Crea socket UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3109">Create UDP socket.</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3110">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3110">Prototype</span></span>

```C
UINT nx_udp_socket_create(
    NX_IP *ip_ptr,
    NX_UDP_SOCKET *socket_ptr, CHAR *name,
    ULONG type_of_service, ULONG fragment,
    UINT time_to_live, ULONG queue_maximum);
```

### <a name="description"></a><span data-ttu-id="cec97-3111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3111">Description</span></span>

<span data-ttu-id="cec97-3112">Questo servizio crea un socket UDP per l'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-3112">This service creates a UDP socket for the specified IP instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3113">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3113">Parameters</span></span>

- <span data-ttu-id="cec97-3114">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3114">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="cec97-3115">**socket_ptr** Puntatore al nuovo blocco di controllo socket UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3115">**socket_ptr** Pointer to new UDP socket control bloc.</span></span>
- <span data-ttu-id="cec97-3116">**nome** Nome dell'applicazione per questo socket UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3116">**name** Application name for this UDP socket.</span></span>
- <span data-ttu-id="cec97-3117">**Type_of_Service** Definisce il tipo di servizio per la trasmissione. i valori validi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="cec97-3117">**type_of_service** Defines the type of service for the transmission, legal values are as follows:</span></span>
    - <span data-ttu-id="cec97-3118">NX_IP_NORMAL (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-3118">NX_IP_NORMAL (0x00000000)</span></span>
    - <span data-ttu-id="cec97-3119">NX_IP_MIN_DELAY (0x00100000)</span><span class="sxs-lookup"><span data-stu-id="cec97-3119">NX_IP_MIN_DELAY (0x00100000)</span></span>
    - <span data-ttu-id="cec97-3120">NX_IP_MAX_DATA (0x00080000)</span><span class="sxs-lookup"><span data-stu-id="cec97-3120">NX_IP_MAX_DATA (0x00080000)</span></span>
    - <span data-ttu-id="cec97-3121">NX_IP_MAX_RELIABLE (0x00040000)</span><span class="sxs-lookup"><span data-stu-id="cec97-3121">NX_IP_MAX_RELIABLE (0x00040000)</span></span>
    - <span data-ttu-id="cec97-3122">NX_IP_MIN_COST (0x00020000)</span><span class="sxs-lookup"><span data-stu-id="cec97-3122">NX_IP_MIN_COST (0x00020000)</span></span>
- <span data-ttu-id="cec97-3123">**frammento** Specifica se la frammentazione IP è consentita o meno.</span><span class="sxs-lookup"><span data-stu-id="cec97-3123">**fragment** Specifies whether or not IP fragmenting is allowed.</span></span> <span data-ttu-id="cec97-3124">Se viene specificato NX_FRAGMENT_OKAY (0x0), è consentita la frammentazione IP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3124">If NX_FRAGMENT_OKAY (0x0) is specified, IP fragmenting is allowed.</span></span> <span data-ttu-id="cec97-3125">Se viene specificato NX_DONT_FRAGMENT (0x4000), la frammentazione IP è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-3125">If NX_DONT_FRAGMENT (0x4000) is specified, IP fragmenting is disabled.</span></span>
- <span data-ttu-id="cec97-3126">**Time_to_live** Specifica il valore a 8 bit che definisce il numero di router che questo pacchetto può superare prima di essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3126">**time_to_live** Specifies the 8-bit value that defines how many routers this packet can pass before being thrown away.</span></span> <span data-ttu-id="cec97-3127">Il valore predefinito è specificato dal NX_IP_TIME_TO_LIVE.</span><span class="sxs-lookup"><span data-stu-id="cec97-3127">The default value is specified by NX_IP_TIME_TO_LIVE.</span></span>
- <span data-ttu-id="cec97-3128">**queue_maximum** Definisce il numero massimo di datagrammi UDP che possono essere accodati per il socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3128">**queue_maximum** Defines the maximum number of UDP datagrams that can be queued for this socket.</span></span> <span data-ttu-id="cec97-3129">Una volta raggiunto il limite della coda, per ogni nuovo pacchetto ricevuto viene rilasciato il pacchetto UDP meno recente.</span><span class="sxs-lookup"><span data-stu-id="cec97-3129">After the queue limit is reached, for every new packet received the oldest UDP packet is released.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3130">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3130">Return Values</span></span>

- <span data-ttu-id="cec97-3131">Creazione socket UDP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-3131">**NX_SUCCESS** (0x00) Successful UDP socket create.</span></span>
- <span data-ttu-id="cec97-3132">**NX_OPTION_ERROR** (0x0A) tipo di servizio, frammento o opzione di durata (TTL) non valida.</span><span class="sxs-lookup"><span data-stu-id="cec97-3132">**NX_OPTION_ERROR** (0x0A) Invalid type-of-service, fragment, or time-to-live option.</span></span>
- <span data-ttu-id="cec97-3133">**NX_PTR_ERROR** (0x07) un puntatore IP o socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3133">**NX_PTR_ERROR** (0x07) Invalid IP or socket pointer.</span></span>
- <span data-ttu-id="cec97-3134">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3134">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3135">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3135">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3136">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3136">Allowed From</span></span>

<span data-ttu-id="cec97-3137">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3137">Initialization and Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3138">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3138">Preemption Possible</span></span>

<span data-ttu-id="cec97-3139">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3139">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3140">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3140">Example</span></span>

```C
/* Create a UDP socket with a maximum receive queue of 30 packets.*/
status = nx_udp_socket_create(&ip_0, &udp_socket, "Sample UDP Socket",
    NX_IP_NORMAL, NX_FRAGMENT_OKAY, 0x80, 30);

/* If status is NX_SUCCESS, the new UDP socket has been created and
    is ready for binding. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3141">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3141">See Also</span></span>

- <span data-ttu-id="cec97-3142">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3142">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3143">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3143">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3144">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3144">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3145">nx_udp_socket_checksum_enable, nx_udp_socket_delete,</span><span class="sxs-lookup"><span data-stu-id="cec97-3145">nx_udp_socket_checksum_enable, nx_udp_socket_delete,</span></span>
- <span data-ttu-id="cec97-3146">nx_udp_socket_info_get, nx_udp_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3146">nx_udp_socket_info_get, nx_udp_socket_port_get,</span></span>
- <span data-ttu-id="cec97-3147">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-3147">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-3148">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3148">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="cec97-3149">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3149">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_delete"></a><span data-ttu-id="cec97-3150">nx_udp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="cec97-3150">nx_udp_socket_delete</span></span>

<span data-ttu-id="cec97-3151">Elimina socket UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3151">Delete UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3152">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3152">Prototype</span></span>

```C
UINT nx_udp_socket_delete(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-3153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3153">Description</span></span>

<span data-ttu-id="cec97-3154">Questo servizio Elimina un socket UDP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3154">This service deletes a previously created UDP socket.</span></span> <span data-ttu-id="cec97-3155">Se il socket è stato associato a una porta, il socket deve essere prima non associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3155">If the socket was bound to a port, the socket must be unbound first.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3156">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3156">Parameters</span></span>

- <span data-ttu-id="cec97-3157">**socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3157">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3158">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3158">Return Values</span></span>

- <span data-ttu-id="cec97-3159">Eliminazione del socket riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-3159">**NX_SUCCESS** (0x00) Successful socket delete.</span></span>
- <span data-ttu-id="cec97-3160">Il socket **NX_STILL_BOUND** (0x42) è ancora associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3160">**NX_STILL_BOUND** (0x42) Socket is still bound.</span></span>
- <span data-ttu-id="cec97-3161">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3161">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-3162">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3162">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3163">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3163">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3164">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3164">Allowed From</span></span>

<span data-ttu-id="cec97-3165">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3165">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3166">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3166">Preemption Possible</span></span>

<span data-ttu-id="cec97-3167">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3167">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3168">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3168">Example</span></span>

```C
/* Delete a previously created UDP socket. */
status = nx_udp_socket_delete(&udp_socket);

/* If status is NX_SUCCESS, the previously created UDP socket has
    been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3169">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3169">See Also</span></span>

- <span data-ttu-id="cec97-3170">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3170">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3171">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3171">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3172">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3172">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3173">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3173">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3174">nx_udp_socket_info_get, nx_udp_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3174">nx_udp_socket_info_get, nx_udp_socket_port_get,</span></span>
- <span data-ttu-id="cec97-3175">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-3175">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-3176">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3176">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="cec97-3177">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3177">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_info_get"></a><span data-ttu-id="cec97-3178">nx_udp_socket_info_get</span><span class="sxs-lookup"><span data-stu-id="cec97-3178">nx_udp_socket_info_get</span></span>

<span data-ttu-id="cec97-3179">Recuperare informazioni sulle attività del socket UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3179">Retrieve information about UDP socket activities</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3180">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3180">Prototype</span></span>

```C
UINT nx_udp_socket_info_get(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_packets_queued,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
```

### <a name="description"></a><span data-ttu-id="cec97-3181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3181">Description</span></span>

<span data-ttu-id="cec97-3182">Questo servizio recupera informazioni sulle attività socket UDP per l'istanza del socket UDP specificata.</span><span class="sxs-lookup"><span data-stu-id="cec97-3182">This service retrieves information about UDP socket activities for the specified UDP socket instance.</span></span>

<span data-ttu-id="cec97-3183">*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*</span><span class="sxs-lookup"><span data-stu-id="cec97-3183">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3184">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3184">Parameters</span></span>

- <span data-ttu-id="cec97-3185">**socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3185">**socket_ptr** Pointer to previously-created UDP socket instance.</span></span>
- <span data-ttu-id="cec97-3186">**udp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti UDP inviati al socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3186">**udp_packets_sent** Pointer to destination for the total number of UDP packets sent on socket.</span></span>
- <span data-ttu-id="cec97-3187">**udp_bytes_sent** Puntatore alla destinazione per il numero totale di byte UDP inviati al socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3187">**udp_bytes_sent** Pointer to destination for the total number of UDP bytes sent on socket.</span></span>
- <span data-ttu-id="cec97-3188">**udp_packets_received** Puntatore alla destinazione del numero totale di pacchetti UDP ricevuti sul socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3188">**udp_packets_received** Pointer to destination of the total number of UDP packets received on socket.</span></span>
- <span data-ttu-id="cec97-3189">**udp_bytes_received** Puntatore alla destinazione del numero totale di byte UDP ricevuti sul socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3189">**udp_bytes_received** Pointer to destination of the total number of UDP bytes received on socket.</span></span>
- <span data-ttu-id="cec97-3190">**udp_packets_queued** Puntatore alla destinazione del numero totale di pacchetti UDP in coda nel socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3190">**udp_packets_queued** Pointer to destination of the total number of queued UDP packets on socket.</span></span>
- <span data-ttu-id="cec97-3191">**udp_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione UDP eliminati per il socket a causa del superamento della dimensione della coda.</span><span class="sxs-lookup"><span data-stu-id="cec97-3191">**udp_receive_packets_dropped** Pointer to destination of the total number of UDP receive packets dropped for socket due to queue size being exceeded.</span></span>
- <span data-ttu-id="cec97-3192">**udp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti UDP con errori di checksum nel socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3192">**udp_checksum_errors** Pointer to destination of the total number of UDP packets with checksum errors on socket.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3193">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3193">Return Values</span></span>

- <span data-ttu-id="cec97-3194">Il recupero delle informazioni sul socket UDP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-3194">**NX_SUCCESS** (0x00) Successful UDP socket information retrieval.</span></span>
- <span data-ttu-id="cec97-3195">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3195">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-3196">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3196">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3197">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3197">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3198">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3198">Allowed From</span></span>

<span data-ttu-id="cec97-3199">Inizializzazione, thread e timer</span><span class="sxs-lookup"><span data-stu-id="cec97-3199">Initialization, threads, and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3200">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3200">Preemption Possible</span></span>

<span data-ttu-id="cec97-3201">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3201">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3202">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3202">Example</span></span>

```C
/* Retrieve UDP socket information from socket 0.*/
status = nx_udp_socket_info_get(&socket_0,
    &udp_packets_sent,
    &udp_bytes_sent,
    &udp_packets_received,
    &udp_bytes_received,
    &udp_queued_packets,
    &udp_receive_packets_dropped,
    &udp_checksum_errors);

/* If status is NX_SUCCESS, UDP socket information was retrieved.*/
```

### <a name="see-also"></a><span data-ttu-id="cec97-3203">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3203">See Also</span></span>

- <span data-ttu-id="cec97-3204">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3204">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3205">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3205">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3206">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3206">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3207">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3207">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3208">nx_udp_socket_delete, nx_udp_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3208">nx_udp_socket_delete, nx_udp_socket_port_get,</span></span>
- <span data-ttu-id="cec97-3209">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-3209">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-3210">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3210">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="cec97-3211">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3211">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_port_get"></a><span data-ttu-id="cec97-3212">nx_udp_socket_port_get</span><span class="sxs-lookup"><span data-stu-id="cec97-3212">nx_udp_socket_port_get</span></span>

<span data-ttu-id="cec97-3213">Preleva il numero di porta associato al socket UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3213">Pick up port number bound to UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3214">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3214">Prototype</span></span>

```C
UINT nx_udp_socket_port_get(NX_UDP_SOCKET *socket_ptr, UINT *port_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-3215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3215">Description</span></span>

<span data-ttu-id="cec97-3216">Questo servizio recupera il numero di porta associato al socket, che è utile per trovare la porta allocata da NetX nelle situazioni in cui è stato specificato il NX_ANY_PORT nel momento in cui il socket è stato associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3216">This service retrieves the port number associated with the socket, which is useful to find the port allocated by NetX in situations where the NX_ANY_PORT was specified at the time the socket was bound.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3217">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3217">Parameters</span></span>

- <span data-ttu-id="cec97-3218">**socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3218">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>
- <span data-ttu-id="cec97-3219">**port_ptr** Puntatore alla destinazione per il numero di porta restituito.</span><span class="sxs-lookup"><span data-stu-id="cec97-3219">**port_ptr** Pointer to destination for the return port number.</span></span> <span data-ttu-id="cec97-3220">I numeri di porta validi sono (1-0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="cec97-3220">Valid port numbers are (1- 0xFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3221">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3221">Return Values</span></span>

- <span data-ttu-id="cec97-3222">**NX_SUCCESS** (0x00) associazione Socket riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-3222">**NX_SUCCESS** (0x00) Successful socket bind.</span></span>
- <span data-ttu-id="cec97-3223">**NX_NOT_BOUND** (0X24) questo socket non è associato a una porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-3223">**NX_NOT_BOUND** (0x24) This socket is not bound to a port.</span></span>
- <span data-ttu-id="cec97-3224">**NX_PTR_ERROR** (0x07) puntatore a socket non valido o puntatore a porta restituita.</span><span class="sxs-lookup"><span data-stu-id="cec97-3224">**NX_PTR_ERROR** (0x07) Invalid socket pointer or port return pointer.</span></span>
- <span data-ttu-id="cec97-3225">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3225">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3226">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3226">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3227">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3227">Allowed From</span></span>

<span data-ttu-id="cec97-3228">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3228">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3229">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3229">Preemption Possible</span></span>

<span data-ttu-id="cec97-3230">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3230">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3231">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3231">Example</span></span>

```C
/* Get the port number of created and bound UDP socket. */
status = nx_udp_socket_port_get(&udp_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
    socket is bound to. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3232">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3232">See Also</span></span>

- <span data-ttu-id="cec97-3233">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3233">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3234">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3234">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3235">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3235">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3236">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3236">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3237">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3237">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3238">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-3238">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-3239">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3239">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="cec97-3240">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3240">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_receive"></a><span data-ttu-id="cec97-3241">nx_udp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="cec97-3241">nx_udp_socket_receive</span></span>

<span data-ttu-id="cec97-3242">Ricevi datagramma dal socket UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3242">Receive datagram from UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3243">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3243">Prototype</span></span>

```C
UINT nx_udp_socket_receive(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="cec97-3244">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3244">Description</span></span>

<span data-ttu-id="cec97-3245">Questo servizio riceve un datagramma UDP dal socket specificato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3245">This service receives an UDP datagram from the specified socket.</span></span> <span data-ttu-id="cec97-3246">Se non viene accodato alcun datagramma sul socket specificato, il chiamante viene sospeso in base all'opzione wait fornita.</span><span class="sxs-lookup"><span data-stu-id="cec97-3246">If no datagram is queued on the specified socket, the caller suspends based on the supplied wait option.</span></span>

<span data-ttu-id="cec97-3247">*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*</span><span class="sxs-lookup"><span data-stu-id="cec97-3247">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3248">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3248">Parameters</span></span>

- <span data-ttu-id="cec97-3249">**socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3249">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>
- <span data-ttu-id="cec97-3250">**packet_ptr** Puntatore al puntatore del pacchetto del datagramma UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3250">**packet_ptr** Pointer to UDP datagram packet pointer.</span></span>
- <span data-ttu-id="cec97-3251">**WAIT_OPTION** Definisce il comportamento del servizio se un datagramma non è attualmente accodato in questo socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3251">**wait_option** Defines how the service behaves if a datagram is not currently queued on this socket.</span></span> <span data-ttu-id="cec97-3252">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="cec97-3252">The wait options are defined as follows:</span></span>
- <span data-ttu-id="cec97-3253">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="cec97-3253">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="cec97-3254">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="cec97-3254">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="cec97-3255">valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="cec97-3255">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3256">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3256">Allowed From</span></span>

<span data-ttu-id="cec97-3257">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3257">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3258">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3258">Preemption Possible</span></span>

<span data-ttu-id="cec97-3259">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3259">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3260">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3260">Example</span></span>

```C
/* Receive a packet from a previously created and bound UDP socket.
    If no packets are currently available, wait for 500 timer ticks
    before giving up. */
status = nx_udp_socket_receive(&udp_socket, &packet_ptr, 500);

/* If status is NX_SUCCESS, the received UDP packet is pointed to by
    packet_ptr. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3261">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3261">See Also</span></span>

- <span data-ttu-id="cec97-3262">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3262">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3263">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3263">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3264">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3264">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3265">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3265">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3266">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3266">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3267">nx_udp_socket_port_get, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="cec97-3267">nx_udp_socket_port_get, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="cec97-3268">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3268">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="cec97-3269">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3269">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_receive_notify"></a><span data-ttu-id="cec97-3270">nx_udp_socket_receive_notify</span><span class="sxs-lookup"><span data-stu-id="cec97-3270">nx_udp_socket_receive_notify</span></span>

<span data-ttu-id="cec97-3271">Invia una notifica all'applicazione di ogni pacchetto ricevuto</span><span class="sxs-lookup"><span data-stu-id="cec97-3271">Notify application of each received packet</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3272">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3272">Prototype</span></span>

```C
UINT nx_udp_socket_receive_notify(
    NX_UDP_SOCKET *socket_ptr,
    VOID (*udp_receive_notify)
    (NX_UDP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="cec97-3273">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3273">Description</span></span>

<span data-ttu-id="cec97-3274">Questo servizio imposta il puntatore della funzione receive Notify per la funzione di callback specificata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-3274">This service sets the receive notify function pointer to the callback function specified by the application.</span></span> <span data-ttu-id="cec97-3275">Questa funzione di callback viene quindi chiamata ogni volta che viene ricevuto un pacchetto nel socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3275">This callback function is then called whenever a packet is received on the socket.</span></span> <span data-ttu-id="cec97-3276">Se viene fornito un puntatore NX_NULL, la funzione receive Notify è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-3276">If a NX_NULL pointer is supplied, the receive notify function is disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3277">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3277">Parameters</span></span>

- <span data-ttu-id="cec97-3278">**socket_ptr** Puntatore al socket UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3278">**socket_ptr** Pointer to the UDP socket.</span></span>
- <span data-ttu-id="cec97-3279">**udp_receive_notify** Puntatore alla funzione di callback dell'applicazione che viene chiamato quando viene ricevuto un pacchetto nel socket.</span><span class="sxs-lookup"><span data-stu-id="cec97-3279">**udp_receive_notify** Application callback function pointer that is called when a packet is received on the socket.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3280">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3280">Allowed From</span></span>

<span data-ttu-id="cec97-3281">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="cec97-3281">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3282">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3282">Preemption Possible</span></span>

<span data-ttu-id="cec97-3283">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3283">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3284">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3284">Example</span></span>

```C
/* Setup a receive packet callback function for the "udp_socket"
socket. */
status = nx_udp_socket_receive_notify(&udp_socket,
    my_receive_notify);

/* If status is NX_SUCCESS, NetX will call the function named
    "my_receive_notify" whenever a packet is received for
    "udp_socket". */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3285">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3285">See Also</span></span>

- <span data-ttu-id="cec97-3286">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3286">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3287">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3287">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3288">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3288">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3289">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3289">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3290">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3290">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3291">nx_udp_socket_port_get, nx_udp_socket_receive, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3291">nx_udp_socket_port_get, nx_udp_socket_receive, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-3292">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3292">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="cec97-3293">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3293">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_send"></a><span data-ttu-id="cec97-3294">nx_udp_socket_send</span><span class="sxs-lookup"><span data-stu-id="cec97-3294">nx_udp_socket_send</span></span>

<span data-ttu-id="cec97-3295">Inviare un datagramma UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3295">Send a UDP Datagram</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3296">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3296">Prototype</span></span>

```C
UINT nx_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port);
```

### <a name="description"></a><span data-ttu-id="cec97-3297">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3297">Description</span></span>

<span data-ttu-id="cec97-3298">Questo servizio invia un datagramma UDP tramite un socket UDP precedentemente creato e associato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3298">This service sends a UDP datagram through a previously created and bound UDP socket.</span></span> <span data-ttu-id="cec97-3299">NetX trova un indirizzo IP locale appropriato come indirizzo di origine in base all'indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-3299">NetX finds a suitable local IP address as source address based on the destination IP address.</span></span> <span data-ttu-id="cec97-3300">Per specificare un'interfaccia e un indirizzo IP di origine specifici, l'applicazione deve usare il servizio **nx_udp_socket_interface_send** .</span><span class="sxs-lookup"><span data-stu-id="cec97-3300">To specify a specific interface and source IP address, the application should use the **nx_udp_socket_interface_send** service.</span></span>

<span data-ttu-id="cec97-3301">Si noti che questo servizio viene restituito immediatamente, indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-3301">Note that this service returns immediately regardless of whether the UDP datagram was successfully sent.</span></span>

<span data-ttu-id="cec97-3302">Il socket deve essere associato a una porta locale.</span><span class="sxs-lookup"><span data-stu-id="cec97-3302">The socket must be bound to a local port.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3303">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3303">Parameters</span></span>

- <span data-ttu-id="cec97-3304">**socket_ptr** Puntatore all'istanza Socket UDP creata in precedenza</span><span class="sxs-lookup"><span data-stu-id="cec97-3304">**socket_ptr** Pointer to previously created UDP socket instance</span></span>
- <span data-ttu-id="cec97-3305">**packet_ptr** Puntatore al pacchetto del datagramma UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3305">**packet_ptr** UDP datagram packet pointer</span></span>
- <span data-ttu-id="cec97-3306">**ip_address** Indirizzo IP di destinazione</span><span class="sxs-lookup"><span data-stu-id="cec97-3306">**ip_address** Destination IP address</span></span>
- <span data-ttu-id="cec97-3307">**porta** Numero di porta di destinazione valido compreso tra 1 e 0xFFFF), in ordine byte host</span><span class="sxs-lookup"><span data-stu-id="cec97-3307">**port** Valid destination port number between 1 and 0xFFFF), in host byte order</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3308">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3308">Return Values</span></span>

- <span data-ttu-id="cec97-3309">**NX_SUCCESS** (0x00) trasmissione socket UDP riuscita</span><span class="sxs-lookup"><span data-stu-id="cec97-3309">**NX_SUCCESS** (0x00) Successful UDP socket send</span></span>
- <span data-ttu-id="cec97-3310">Socket **NX_NOT_BOUND** (0x24) non associato ad alcuna porta</span><span class="sxs-lookup"><span data-stu-id="cec97-3310">**NX_NOT_BOUND** (0x24) Socket not bound to any port</span></span>
- <span data-ttu-id="cec97-3311">**NX_NO_INTERFACE_ADDRESS** (0X50) non è possibile trovare un'interfaccia in uscita adatta.</span><span class="sxs-lookup"><span data-stu-id="cec97-3311">**NX_NO_INTERFACE_ADDRESS** (0x50) No suitable outgoing interface can be found.</span></span>
- <span data-ttu-id="cec97-3312">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP del server non valido</span><span class="sxs-lookup"><span data-stu-id="cec97-3312">**NX_IP_ADDRESS_ERROR** (0x21) Invalid server IP address</span></span>
- <span data-ttu-id="cec97-3313">Lo spazio di **NX_UNDERFLOW** (0x02) non è sufficiente per l'intestazione UDP nel pacchetto</span><span class="sxs-lookup"><span data-stu-id="cec97-3313">**NX_UNDERFLOW** (0x02) Not enough room for UDP header in the packet</span></span>
- <span data-ttu-id="cec97-3314">Puntatore di aggiunta pacchetto di **NX_OVERFLOW** (0x03) non valido</span><span class="sxs-lookup"><span data-stu-id="cec97-3314">**NX_OVERFLOW** (0x03) Packet append pointer is invalid</span></span>
- <span data-ttu-id="cec97-3315">**NX_PTR_ERROR** (0x07) puntatore al socket non valido</span><span class="sxs-lookup"><span data-stu-id="cec97-3315">**NX_PTR_ERROR** (0x07) Invalid socket pointer</span></span>
- <span data-ttu-id="cec97-3316">**NX_CALLER_ERROR** (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="cec97-3316">**NX_CALLER_ERROR** (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="cec97-3317">Il **NX_NOT_ENABLED** UDP (0x14) non è stato abilitato</span><span class="sxs-lookup"><span data-stu-id="cec97-3317">**NX_NOT_ENABLED** (0x14) UDP has not been enabled</span></span>
- <span data-ttu-id="cec97-3318">Il numero di porta **NX_INVALID_PORT** (0x46) non è compreso in un intervallo valido</span><span class="sxs-lookup"><span data-stu-id="cec97-3318">**NX_INVALID_PORT** (0x46) Port number is not within a valid range</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3319">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3319">Allowed From</span></span>

<span data-ttu-id="cec97-3320">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3320">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3321">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3321">Preemption Possible</span></span>

<span data-ttu-id="cec97-3322">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3322">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3323">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3323">Example</span></span>

```C
ULONG server_address;

/* Set the UDP Client IP address. */
server_address = IP_ADDRESS(1,2,3,5);

/* Send a packet to the UDP server at server_address on port 12. */
status = nx_udp_socket_send(&client_socket, packet_ptr,
    server_address, 12);

/* If status == NX_SUCCESS, the application successfully transmitted
    the packet out the UDP socket to its peer. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3324">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3324">See Also</span></span>

- <span data-ttu-id="cec97-3325">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3325">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3326">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3326">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3327">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3327">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3328">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3328">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3329">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3329">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3330">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-3330">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-3331">nx_udp_socket_receive_notify, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3331">nx_udp_socket_receive_notify, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="cec97-3332">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3332">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_interface_send"></a><span data-ttu-id="cec97-3333">nx_udp_socket_interface_send</span><span class="sxs-lookup"><span data-stu-id="cec97-3333">nx_udp_socket_interface_send</span></span>

<span data-ttu-id="cec97-3334">Invia datagramma tramite socket UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3334">Send datagram through UDP socket.</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3335">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3335">Prototype</span></span>

```C
UINT nx_udp_socket_interface_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port,
    UINT address_index);
```

### <a name="description"></a><span data-ttu-id="cec97-3336">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3336">Description</span></span>

<span data-ttu-id="cec97-3337">Questo servizio invia un datagramma UDP tramite un socket UDP precedentemente creato e associato tramite l'interfaccia di rete con l'indirizzo IP specificato come indirizzo di origine.</span><span class="sxs-lookup"><span data-stu-id="cec97-3337">This service sends a UDP datagram through a previously created and bound UDP socket through the network interface with the specified IP address as the source address.</span></span> <span data-ttu-id="cec97-3338">Si noti che il servizio restituisce immediatamente un risultato, indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente o meno.</span><span class="sxs-lookup"><span data-stu-id="cec97-3338">Note that service returns immediately, regardless of whether or not the UDP datagram was successfully sent.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3339">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3339">Parameters</span></span>

- <span data-ttu-id="cec97-3340">**socket_ptr** Socket per la trasmissione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-3340">**socket_ptr** Socket to transmit the packet out on.</span></span>
- <span data-ttu-id="cec97-3341">**packet_ptr** Puntatore al pacchetto da trasmettere.</span><span class="sxs-lookup"><span data-stu-id="cec97-3341">**packet_ptr** Pointer to packet to transmit.</span></span>
- <span data-ttu-id="cec97-3342">**ip_address** Indirizzo IP di destinazione per l'invio del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-3342">**ip_address** Destination IP address to send packet.</span></span>
- <span data-ttu-id="cec97-3343">**porta** Porta di destinazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-3343">**port** Destination port.</span></span>
- <span data-ttu-id="cec97-3344">**address_index** Indice dell'indirizzo associato all'interfaccia su cui inviare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cec97-3344">**address_index** Index of the address associated with the interface to send packet on.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3345">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3345">Return Values</span></span>

- <span data-ttu-id="cec97-3346">Il pacchetto **NX_SUCCESS** (0x00) è stato inviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="cec97-3346">**NX_SUCCESS** (0x00) Packet successfully sent.</span></span>
- <span data-ttu-id="cec97-3347">Il socket **NX_NOT_BOUND** (0x24) non è associato a una porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-3347">**NX_NOT_BOUND** (0x24) Socket not bound to a port.</span></span>
- <span data-ttu-id="cec97-3348">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3348">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="cec97-3349">L'elaborazione UDP di **NX_NOT_ENABLED** (0x14) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="cec97-3349">**NX_NOT_ENABLED** (0x14) UDP processing not enabled.</span></span>
- <span data-ttu-id="cec97-3350">**NX_PTR_ERROR** (0x07) puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3350">**NX_PTR_ERROR** (0x07) Invalid pointer.</span></span>
- <span data-ttu-id="cec97-3351">**NX_OVERFLOW** (0x03) puntatore di Accodamento pacchetti non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3351">**NX_OVERFLOW** (0x03) Invalid packet append pointer.</span></span>
- <span data-ttu-id="cec97-3352">**NX_UNDERFLOW** (0x02) puntatore a anteporre il pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3352">**NX_UNDERFLOW** (0x02) Invalid packet prepend pointer.</span></span>
- <span data-ttu-id="cec97-3353">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3353">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3354">**NX_INVALID_INTERFACE** (0x4C) indice di indirizzo non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3354">**NX_INVALID_INTERFACE** (0x4C) Invalid address index.</span></span>
- <span data-ttu-id="cec97-3355">Il numero di porta **NX_INVALID_PORT** (0x46) supera il numero di porta massimo.</span><span class="sxs-lookup"><span data-stu-id="cec97-3355">**NX_INVALID_PORT** (0x46) Port number exceeds maximum port number.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3356">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3356">Allowed From</span></span>

<span data-ttu-id="cec97-3357">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3357">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3358">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3358">Preemption Possible</span></span>

<span data-ttu-id="cec97-3359">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3359">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3360">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3360">Example</span></span>

```C
#define ADDRESS_INDEX 1

/* Send packet out on port 80 to the specified destination IP on the
interface at index 1 in the IP task interface list. */
status = nx_udp_packet_interface_send(socket_ptr, packet_ptr,
    destination_ip, 80,
    ADDRESS_INDEX);

/* If status is NX_SUCCESS packet was successfully transmitted. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3361">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3361">See Also</span></span>

- <span data-ttu-id="cec97-3362">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3362">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3363">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3363">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3364">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3364">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3365">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3365">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3366">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3366">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3367">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-3367">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-3368">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3368">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-3369">nx_udp_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="cec97-3369">nx_udp_socket_unbind</span></span>

## <a name="nx_udp_socket_unbind"></a><span data-ttu-id="cec97-3370">nx_udp_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="cec97-3370">nx_udp_socket_unbind</span></span>

<span data-ttu-id="cec97-3371">Separare il socket UDP dalla porta UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3371">Unbind UDP socket from UDP port.</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3372">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3372">Prototype</span></span>

```C
UINT nx_udp_socket_unbind(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="cec97-3373">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3373">Description</span></span>

<span data-ttu-id="cec97-3374">Questo servizio rilascia l'associazione tra il socket UDP e una porta UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3374">This service releases the binding between the UDP socket and a UDP port.</span></span> <span data-ttu-id="cec97-3375">Tutti i pacchetti ricevuti archiviati nella coda di ricezione vengono rilasciati come parte dell'operazione di annullamento dell'associazione.</span><span class="sxs-lookup"><span data-stu-id="cec97-3375">Any received packets stored in the receive queue are released as part of the unbind operation.</span></span>

<span data-ttu-id="cec97-3376">Se sono presenti altri thread in attesa di associare un altro socket alla porta non associata, il primo thread sospeso viene quindi associato alla porta appena non associata.</span><span class="sxs-lookup"><span data-stu-id="cec97-3376">If there are other threads waiting to bind another socket to the unbound port, the first suspended thread is then bound to the newly unbound port.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3377">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3377">Parameters</span></span>

- <span data-ttu-id="cec97-3378">**socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cec97-3378">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3379">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3379">Return Values</span></span>

- <span data-ttu-id="cec97-3380">La disassociazione del socket è riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="cec97-3380">**NX_SUCCESS** (0x00) Successful socket unbind.</span></span>
- <span data-ttu-id="cec97-3381">Il socket **NX_NOT_BOUND** (0x24) non è stato associato ad alcuna porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-3381">**NX_NOT_BOUND** (0x24) Socket was not bound to any port.</span></span>
- <span data-ttu-id="cec97-3382">**NX_PTR_ERROR** (0x07) puntatore al socket non valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3382">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="cec97-3383">Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="cec97-3383">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="cec97-3384">**NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="cec97-3384">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3385">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3385">Allowed From</span></span>

<span data-ttu-id="cec97-3386">Thread</span><span class="sxs-lookup"><span data-stu-id="cec97-3386">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3387">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3387">Preemption Possible</span></span>

<span data-ttu-id="cec97-3388">Sì</span><span class="sxs-lookup"><span data-stu-id="cec97-3388">Yes</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3389">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3389">Example</span></span>

```C
/* Unbind the previously bound UDP socket. */
status = nx_udp_socket_unbind(&udp_socket);

/* If status is NX_SUCCESS, the previously bound socket is now
    unbound. */
```

### <a name="see-also"></a><span data-ttu-id="cec97-3390">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3390">See Also</span></span>

- <span data-ttu-id="cec97-3391">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3391">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3392">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3392">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3393">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3393">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3394">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3394">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3395">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3395">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3396">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-3396">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-3397">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3397">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-3398">nx_udp_socket_interface_send, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3398">nx_udp_socket_interface_send, nx_udp_source_extract</span></span>

## <a name="nx_udp_source_extract"></a><span data-ttu-id="cec97-3399">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="cec97-3399">nx_udp_source_extract</span></span>

<span data-ttu-id="cec97-3400">Estrarre IP e la porta di trasmissione dal datagramma UDP</span><span class="sxs-lookup"><span data-stu-id="cec97-3400">Extract IP and sending port from UDP datagram</span></span>

### <a name="prototype"></a><span data-ttu-id="cec97-3401">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cec97-3401">Prototype</span></span>

```C
UINT nx_udp_source_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, UINT *port);
```

### <a name="description"></a><span data-ttu-id="cec97-3402">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cec97-3402">Description</span></span>

<span data-ttu-id="cec97-3403">Questo servizio estrae l'IP e il numero di porta del mittente dalle intestazioni IP e UDP del datagramma UDP fornito.</span><span class="sxs-lookup"><span data-stu-id="cec97-3403">This service extracts the sender's IP and port number from the IP and UDP headers of the supplied UDP datagram.</span></span>

### <a name="parameters"></a><span data-ttu-id="cec97-3404">Parametri</span><span class="sxs-lookup"><span data-stu-id="cec97-3404">Parameters</span></span>

- <span data-ttu-id="cec97-3405">**packet_ptr** Puntatore al pacchetto del datagramma UDP.</span><span class="sxs-lookup"><span data-stu-id="cec97-3405">**packet_ptr** UDP datagram packet pointer.</span></span>
- <span data-ttu-id="cec97-3406">**ip_address** Puntatore valido alla variabile dell'indirizzo IP restituito.</span><span class="sxs-lookup"><span data-stu-id="cec97-3406">**ip_address** Valid pointer to the return IP address variable.</span></span>
- <span data-ttu-id="cec97-3407">**porta** Puntatore valido alla variabile della porta restituita.</span><span class="sxs-lookup"><span data-stu-id="cec97-3407">**port** Valid pointer to the return port variable.</span></span>

### <a name="return-values"></a><span data-ttu-id="cec97-3408">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cec97-3408">Return Values</span></span>

- <span data-ttu-id="cec97-3409">**NX_SUCCESS** (0x00) l'estrazione IP/porta di origine è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cec97-3409">**NX_SUCCESS** (0x00) Successful source IP/port extraction.</span></span>
- <span data-ttu-id="cec97-3410">**NX_INVALID_PACKET** (0X12) il pacchetto fornito non è valido.</span><span class="sxs-lookup"><span data-stu-id="cec97-3410">**NX_INVALID_PACKET** (0x12) The supplied packet is invalid.</span></span>
- <span data-ttu-id="cec97-3411">**NX_PTR_ERROR** (0x07) pacchetto non valido o destinazione IP o porta.</span><span class="sxs-lookup"><span data-stu-id="cec97-3411">**NX_PTR_ERROR** (0x07) Invalid packet or IP or port destination.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cec97-3412">Consentito da</span><span class="sxs-lookup"><span data-stu-id="cec97-3412">Allowed From</span></span>

<span data-ttu-id="cec97-3413">Inizializzazione, thread, timer, ISR</span><span class="sxs-lookup"><span data-stu-id="cec97-3413">Initialization, threads, timers, ISR</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="cec97-3414">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="cec97-3414">Preemption Possible</span></span>

<span data-ttu-id="cec97-3415">No</span><span class="sxs-lookup"><span data-stu-id="cec97-3415">No</span></span>

### <a name="example"></a><span data-ttu-id="cec97-3416">Esempio</span><span class="sxs-lookup"><span data-stu-id="cec97-3416">Example</span></span>

```C
/* Extract the IP and port information from the sender of the UPD
    packet. */
status = nx_udp_source_extract(packet_ptr, &sender_ip_address,
    &sender_port);

/* If status is NX_SUCCESS, the sender IP and port information has
    been stored in sender_ip_address and sender_port respectively.*/
```

### <a name="see-also"></a><span data-ttu-id="cec97-3417">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cec97-3417">See Also</span></span>

- <span data-ttu-id="cec97-3418">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3418">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="cec97-3419">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="cec97-3419">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="cec97-3420">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="cec97-3420">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="cec97-3421">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="cec97-3421">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="cec97-3422">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="cec97-3422">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="cec97-3423">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="cec97-3423">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="cec97-3424">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="cec97-3424">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="cec97-3425">nx_udp_socket_interface_send, nx_udp_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="cec97-3425">nx_udp_socket_interface_send, nx_udp_socket_unbind</span></span>