---
title: Capitolo 4-Descrizione dei servizi NAT
description: Questo capitolo contiene una descrizione di tutti i servizi API NAT NetX Duo in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8bdbdfcb2da6425fb99cadc7b2f6815dedc12953
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821755"
---
# <a name="chapter-4---description-of-nat-services"></a><span data-ttu-id="50029-103">Capitolo 4-Descrizione dei servizi NAT</span><span class="sxs-lookup"><span data-stu-id="50029-103">Chapter 4 - Description of NAT services</span></span>

<span data-ttu-id="50029-104">Questo capitolo contiene una descrizione di tutti i servizi API NAT NetX Duo (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="50029-104">This chapter contains a description of all NetX Duo NAT API services (listed below) in alphabetical order.</span></span>

> [!NOTE]
> <span data-ttu-id="50029-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="50029-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_nat_create"></a><span data-ttu-id="50029-106">nx_nat_create</span><span class="sxs-lookup"><span data-stu-id="50029-106">nx_nat_create</span></span>

<span data-ttu-id="50029-107">Creare un server NAT</span><span class="sxs-lookup"><span data-stu-id="50029-107">Create a NAT Server</span></span>

### <a name="prototype"></a><span data-ttu-id="50029-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="50029-108">Prototype</span></span>

```C
UINT nx_nat_create(NX_NAT_DEVICE *nat_ptr, NX_IP *ip_ptr,
    UINT global_interface_index,
    VOID *dynamic_cache_memory,
    UINT dynamic_cache_size);
```

### <a name="description"></a><span data-ttu-id="50029-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="50029-109">Description</span></span>

<span data-ttu-id="50029-110">Questo servizio crea un'istanza del server NAT.</span><span class="sxs-lookup"><span data-stu-id="50029-110">This service creates an instance of the NAT server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50029-111">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="50029-111">Input Parameters</span></span>

- <span data-ttu-id="50029-112">**nat_ptr** Puntatore all'istanza NAT da creare</span><span class="sxs-lookup"><span data-stu-id="50029-112">**nat_ptr** Pointer to NAT instance to create</span></span>
- <span data-ttu-id="50029-113">**puntatore ip_ptr** all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="50029-113">**ip_ptr Pointer** to IP instance</span></span>
- <span data-ttu-id="50029-114">**global_interface_index** Indicizzare l'interfaccia di rete globale</span><span class="sxs-lookup"><span data-stu-id="50029-114">**global_interface_index** Index to the global network interface</span></span>
- <span data-ttu-id="50029-115">**dynamic_cache_memory** Area memoria puntatore alla tabella NAT</span><span class="sxs-lookup"><span data-stu-id="50029-115">**dynamic_cache_memory** Pointer memory area to NAT table</span></span>
- <span data-ttu-id="50029-116">**dynamic_cache_size** Dimensioni dell'area di memoria per la tabella NAT</span><span class="sxs-lookup"><span data-stu-id="50029-116">**dynamic_cache_size** Size of memory area for NAT table</span></span>

### <a name="return-values"></a><span data-ttu-id="50029-117">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="50029-117">Return Values</span></span>

- <span data-ttu-id="50029-118">Server NAT **NX_SUCCESS** (0x00) creato correttamente</span><span class="sxs-lookup"><span data-stu-id="50029-118">**NX_SUCCESS** (0x00) NAT server successfully created</span></span>
- <span data-ttu-id="50029-119">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-119">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="50029-120">NX_NAT_PARAM_ERROR (0xD01) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="50029-120">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>
- <span data-ttu-id="50029-121">Input del puntatore della cache NX_NAT_CACHE_ERROR (0xD02) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-121">NX_NAT_CACHE_ERROR (0xD02) Invalid cache pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50029-122">Consentito da</span><span class="sxs-lookup"><span data-stu-id="50029-122">Allowed From</span></span>

<span data-ttu-id="50029-123">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="50029-123">Application code</span></span>

### <a name="example"></a><span data-ttu-id="50029-124">Esempio</span><span class="sxs-lookup"><span data-stu-id="50029-124">Example</span></span>

```C
#define NX_NAT_ENTRY_CACHE_SIZE 20480

static UCHAR nat_cache[NX_NAT_ENTRY_CACHE_SIZE];
UINT global_interface_index = 0;

/* Create a NAT Server and cache with a global interface index. */
status = nx_nat_create(nat_ptr, ip_ptr, global_interface_index,
    nat_cache, NX_NAT_ENTRY_CACHE_SIZE);

/* If status = NX_SUCCESS, the NAT instance was successfully
    created. */
```

## <a name="nx_nat_delete"></a><span data-ttu-id="50029-125">nx_nat_delete</span><span class="sxs-lookup"><span data-stu-id="50029-125">nx_nat_delete</span></span>

<span data-ttu-id="50029-126">Eliminare un server NAT</span><span class="sxs-lookup"><span data-stu-id="50029-126">Delete a NAT Server</span></span>

### <a name="prototype"></a><span data-ttu-id="50029-127">Prototipo</span><span class="sxs-lookup"><span data-stu-id="50029-127">Prototype</span></span>

```C
UINT nx_nat_delete(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="50029-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="50029-128">Description</span></span>

<span data-ttu-id="50029-129">Questo servizio Elimina un server NAT creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="50029-129">This service deletes a previously created NAT Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50029-130">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="50029-130">Input Parameters</span></span>

- <span data-ttu-id="50029-131">**nat_ptr** Puntatore all'istanza NAT da eliminare</span><span class="sxs-lookup"><span data-stu-id="50029-131">**nat_ptr** Pointer to NAT instance to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="50029-132">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="50029-132">Return Values</span></span>

- <span data-ttu-id="50029-133">**NX_SUCCESS** (0x00) NAT eliminato correttamente</span><span class="sxs-lookup"><span data-stu-id="50029-133">**NX_SUCCESS** (0x00) NAT successfully deleted</span></span>
- <span data-ttu-id="50029-134">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-134">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50029-135">Consentito da</span><span class="sxs-lookup"><span data-stu-id="50029-135">Allowed From</span></span>

<span data-ttu-id="50029-136">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="50029-136">Application code</span></span>

### <a name="example"></a><span data-ttu-id="50029-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="50029-137">Example</span></span>

```C
/* Delete the NAT instance. */
status = nx_nat_delete (nat_ptr);

/* If the NAT instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_nat_enable"></a><span data-ttu-id="50029-138">nx_nat_enable</span><span class="sxs-lookup"><span data-stu-id="50029-138">nx_nat_enable</span></span>

<span data-ttu-id="50029-139">Abilitare l'istanza IP per NAT</span><span class="sxs-lookup"><span data-stu-id="50029-139">Enable the IP instance for NAT</span></span>

### <a name="prototype"></a><span data-ttu-id="50029-140">Prototipo</span><span class="sxs-lookup"><span data-stu-id="50029-140">Prototype</span></span>

```C
UINT nx_nat_enable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="50029-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="50029-141">Description</span></span>

<span data-ttu-id="50029-142">Questo servizio Abilita l'istanza IP per NAT (ad esempio, inoltra i pacchetti ricevuti al server NAT).</span><span class="sxs-lookup"><span data-stu-id="50029-142">This service enables the IP instance for NAT (e.g. forward received packets to the NAT server).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50029-143">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="50029-143">Input Parameters</span></span>

- <span data-ttu-id="50029-144">**nat_ptr** Puntatore all'istanza NAT</span><span class="sxs-lookup"><span data-stu-id="50029-144">**nat_ptr** Pointer to NAT instance</span></span>

### <a name="return-values"></a><span data-ttu-id="50029-145">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="50029-145">Return Values</span></span>

- <span data-ttu-id="50029-146">NAT **NX_SUCCESS** (0x00) correttamente abilitato</span><span class="sxs-lookup"><span data-stu-id="50029-146">**NX_SUCCESS** (0x00) NAT successfully enabled</span></span>
- <span data-ttu-id="50029-147">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-147">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50029-148">Consentito da</span><span class="sxs-lookup"><span data-stu-id="50029-148">Allowed From</span></span>

<span data-ttu-id="50029-149">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="50029-149">Application code</span></span>

### <a name="example"></a><span data-ttu-id="50029-150">Esempio</span><span class="sxs-lookup"><span data-stu-id="50029-150">Example</span></span>

```C
/* Enable the NAT server. */
status = nx_nat_enable (nat_ptr);

/* If status = NX_SUCCESS, the IP instance was successfully enabled for NAT. */
```

## <a name="nx_nat_disable"></a><span data-ttu-id="50029-151">nx_nat_disable</span><span class="sxs-lookup"><span data-stu-id="50029-151">nx_nat_disable</span></span>

<span data-ttu-id="50029-152">Disabilitare l'istanza IP per NAT</span><span class="sxs-lookup"><span data-stu-id="50029-152">Disable the IP instance for NAT</span></span>

### <a name="prototype"></a><span data-ttu-id="50029-153">Prototipo</span><span class="sxs-lookup"><span data-stu-id="50029-153">Prototype</span></span>

```C
UINT nx_nat_disable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="50029-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="50029-154">Description</span></span>

<span data-ttu-id="50029-155">Questo servizio Disabilita NAT nell'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="50029-155">This service disables NAT on the IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50029-156">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="50029-156">Input Parameters</span></span>

- <span data-ttu-id="50029-157">**nat_ptr** Puntatore all'istanza NAT</span><span class="sxs-lookup"><span data-stu-id="50029-157">**nat_ptr** Pointer to NAT instance</span></span>

### <a name="return-values"></a><span data-ttu-id="50029-158">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="50029-158">Return Values</span></span>

- <span data-ttu-id="50029-159">NAT **NX_SUCCESS** (0x00) disabilitato</span><span class="sxs-lookup"><span data-stu-id="50029-159">**NX_SUCCESS** (0x00) NAT successfully disabled</span></span>
- <span data-ttu-id="50029-160">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-160">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50029-161">Consentito da</span><span class="sxs-lookup"><span data-stu-id="50029-161">Allowed From</span></span>

<span data-ttu-id="50029-162">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="50029-162">Application code</span></span>

### <a name="example"></a><span data-ttu-id="50029-163">Esempio</span><span class="sxs-lookup"><span data-stu-id="50029-163">Example</span></span>

```C
/* Disable the NAT server. */
status = nx_nat_disable (nat_ptr);

/* If status = NX_SUCCESS the NAT operation successfully disable. */
```

## <a name="nx_nat_cache_notify_set"></a><span data-ttu-id="50029-164">nx_nat_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="50029-164">nx_nat_cache_notify_set</span></span>

<span data-ttu-id="50029-165">Impostare una funzione di callback notifica completa della cache</span><span class="sxs-lookup"><span data-stu-id="50029-165">Set a cache full notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="50029-166">Prototipo</span><span class="sxs-lookup"><span data-stu-id="50029-166">Prototype</span></span>

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)
    (NX_NAT_DEVICE *nat_ptr)));
```

### <a name="description"></a><span data-ttu-id="50029-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="50029-167">Description</span></span>

<span data-ttu-id="50029-168">Questo servizio registra il callback completo della cache con il puntatore alla funzione di input cache_full_notify_cb che punta a una funzione di notifica completa della cache definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="50029-168">This service registers the cache full callback with the input function pointer cache_full_notify_cb which points to a user defined cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50029-169">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="50029-169">Input Parameters</span></span>

- <span data-ttu-id="50029-170">**nat_ptr** Puntatore all'istanza NAT</span><span class="sxs-lookup"><span data-stu-id="50029-170">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="50029-171">**cache_full_notify_cb** Puntatore alla funzione di notifica completa della cache</span><span class="sxs-lookup"><span data-stu-id="50029-171">**cache_full_notify_cb** Pointer to cache full notify function</span></span>

### <a name="return-values"></a><span data-ttu-id="50029-172">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="50029-172">Return Values</span></span>

- <span data-ttu-id="50029-173">Funzione di notifica completa della cache **NX_SUCCESS** (0x00) impostata correttamente</span><span class="sxs-lookup"><span data-stu-id="50029-173">**NX_SUCCESS** (0x00) Cache full notify function successfully set</span></span>
- <span data-ttu-id="50029-174">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-174">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="50029-175">NX_NAT_PARAM_ERROR (0xD01) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="50029-175">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50029-176">Consentito da</span><span class="sxs-lookup"><span data-stu-id="50029-176">Allowed From</span></span>

<span data-ttu-id="50029-177">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="50029-177">Application code</span></span>

### <a name="example"></a><span data-ttu-id="50029-178">Esempio</span><span class="sxs-lookup"><span data-stu-id="50029-178">Example</span></span>

```C
/* Set the cache full notify callback function to the NAT instance. */
status = nx_nat_cache_notify_set(nat_ptr, cache_full_notify_cb);

/* If status = NX_SUCCESS the callback function was successfully set. */
```

## <a name="nx_nat_inbound_entry_create"></a><span data-ttu-id="50029-179">nx_nat_inbound_entry_create</span><span class="sxs-lookup"><span data-stu-id="50029-179">nx_nat_inbound_entry_create</span></span>

<span data-ttu-id="50029-180">Creare una voce in ingresso nella tabella NAT Translation</span><span class="sxs-lookup"><span data-stu-id="50029-180">Create an inbound entry in the NAT translation table</span></span>

### <a name="prototype"></a><span data-ttu-id="50029-181">Prototipo</span><span class="sxs-lookup"><span data-stu-id="50029-181">Prototype</span></span>

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr
    ULONG local_ip_address,
    USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

### <a name="description"></a><span data-ttu-id="50029-182">Descrizione</span><span class="sxs-lookup"><span data-stu-id="50029-182">Description</span></span>

<span data-ttu-id="50029-183">Questo servizio crea una voce in ingresso come statica (voce permanente senza scadenza) e la aggiunge alla tabella di traduzione NAT.</span><span class="sxs-lookup"><span data-stu-id="50029-183">This service creates an inbound entry as static (permanent entry, never expires) and adds it to the NAT translation table.</span></span> <span data-ttu-id="50029-184">Queste voci vengono in genere create per i server host locali in cui viene avviata una connessione da un host nella rete esterna.</span><span class="sxs-lookup"><span data-stu-id="50029-184">These entries are usually created for local host servers where a connection is initiated from a host on the outside network.</span></span> <span data-ttu-id="50029-185">Il server NAT verifica che la porta esterna non sia già in uso nella tabella di traduzione o che sia associata a un socket NetX duo già esistente dello stesso protocollo.</span><span class="sxs-lookup"><span data-stu-id="50029-185">The NAT server checks that the external port is not already in use in the translation table or bound by a previously existing NetX Duo socket of the same protocol.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50029-186">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="50029-186">Input Parameters</span></span>

- <span data-ttu-id="50029-187">**nat_ptr** Puntatore all'istanza NAT</span><span class="sxs-lookup"><span data-stu-id="50029-187">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="50029-188">**entry_ptr** Puntatore alla voce di traslazione</span><span class="sxs-lookup"><span data-stu-id="50029-188">**entry_ptr** Pointer to translation entry</span></span>
- <span data-ttu-id="50029-189">**local_ip_address** Indirizzo IP host locale</span><span class="sxs-lookup"><span data-stu-id="50029-189">**local_ip_address** Local host IP address</span></span>
- <span data-ttu-id="50029-190">**external_port** Porta di destinazione nella rete esterna</span><span class="sxs-lookup"><span data-stu-id="50029-190">**external_port** Destination port on the external network</span></span>
- <span data-ttu-id="50029-191">**local_port** Porta di origine (host locale)</span><span class="sxs-lookup"><span data-stu-id="50029-191">**local_port** Source (local host) port</span></span>
- <span data-ttu-id="50029-192">**protocollo** di Protocollo Packet (ad esempio, TCP)</span><span class="sxs-lookup"><span data-stu-id="50029-192">**protocol** Packet protocol (e.g TCP)</span></span>

### <a name="return-values"></a><span data-ttu-id="50029-193">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="50029-193">Return Values</span></span>

- <span data-ttu-id="50029-194">Creazione della voce **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="50029-194">**NX_SUCCESS** (0x00) Entry successfully created</span></span>
- <span data-ttu-id="50029-195">**NX_NAT_PORT_UNAVAILABLE** (0xD0D) porta esterna non valida</span><span class="sxs-lookup"><span data-stu-id="50029-195">**NX_NAT_PORT_UNAVAILABLE** (0xD0D) Invalid external port</span></span>
- <span data-ttu-id="50029-196">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-196">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="50029-197">NX_NAT_PARAM_ERROR (0xD01) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="50029-197">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50029-198">Consentito da</span><span class="sxs-lookup"><span data-stu-id="50029-198">Allowed From</span></span>

<span data-ttu-id="50029-199">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="50029-199">Application code</span></span>

### <a name="example"></a><span data-ttu-id="50029-200">Esempio</span><span class="sxs-lookup"><span data-stu-id="50029-200">Example</span></span>

```C
/* Create an entry for an inbound TCP packet. */
status = nx_nat_inbound_entry_create(nat_ptr, entry_ptr,
    IP_ADDRESS(192,168,2,2), 5001, 5001,
    NX_PROTOCOL_TCP);

/* If status = NX_SUCCESS the entry was successfully created. */
```

## <a name="nx_nat_inbound_entry_delete"></a><span data-ttu-id="50029-201">nx_nat_inbound_entry_delete</span><span class="sxs-lookup"><span data-stu-id="50029-201">nx_nat_inbound_entry_delete</span></span>

<span data-ttu-id="50029-202">Eliminare una voce in ingresso nella tabella NAT Translation</span><span class="sxs-lookup"><span data-stu-id="50029-202">Delete an inbound entry in the NAT translation table</span></span>

### <a name="prototype"></a><span data-ttu-id="50029-203">Prototipo</span><span class="sxs-lookup"><span data-stu-id="50029-203">Prototype</span></span>

```C
UINT nx_nat_inbound_entry_delete(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *delete_entry_ptr)
```

### <a name="description"></a><span data-ttu-id="50029-204">Descrizione</span><span class="sxs-lookup"><span data-stu-id="50029-204">Description</span></span>

<span data-ttu-id="50029-205">Questo servizio Elimina la voce in ingresso specificata dalla tabella di conversione.</span><span class="sxs-lookup"><span data-stu-id="50029-205">This service deletes the specified inbound entry from the translation table.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50029-206">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="50029-206">Input Parameters</span></span>

- <span data-ttu-id="50029-207">**nat_ptr** Puntatore all'istanza NAT</span><span class="sxs-lookup"><span data-stu-id="50029-207">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="50029-208">**delete_entry_ptr** Puntatore alla voce di traduzione NAT</span><span class="sxs-lookup"><span data-stu-id="50029-208">**delete_entry_ptr** Pointer to the NAT translation entry</span></span>

### <a name="return-values"></a><span data-ttu-id="50029-209">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="50029-209">Return Values</span></span>

- <span data-ttu-id="50029-210">La voce **NX_SUCCESS** (0x00) è stata eliminata</span><span class="sxs-lookup"><span data-stu-id="50029-210">**NX_SUCCESS** (0x00) Entry successfully deleted</span></span>
- <span data-ttu-id="50029-211">La voce **NX_NAT_ENTRY_NOT_FOUND** (0xD04) non è stata trovata</span><span class="sxs-lookup"><span data-stu-id="50029-211">**NX_NAT_ENTRY_NOT_FOUND** (0xD04) Entry does not found</span></span>
- <span data-ttu-id="50029-212">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-212">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="50029-213">Tipo di traduzione NX_NAT_ENTRY_TYPE_ERROR (0xD0C) non valido</span><span class="sxs-lookup"><span data-stu-id="50029-213">NX_NAT_ENTRY_TYPE_ERROR (0xD0C) Invalid translation type</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50029-214">Consentito da</span><span class="sxs-lookup"><span data-stu-id="50029-214">Allowed From</span></span>

<span data-ttu-id="50029-215">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="50029-215">Application code</span></span>

### <a name="example"></a><span data-ttu-id="50029-216">Esempio</span><span class="sxs-lookup"><span data-stu-id="50029-216">Example</span></span>

```C
/* Delete the specified static entry from the translation table. */
status = nx_nat_inbound_entry_delete(nat_ptr, delete_entry_ptr);

/* If status = NX_SUCCESS the entry was successfully deleted. */
```
