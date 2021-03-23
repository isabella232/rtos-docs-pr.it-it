---
title: Capitolo 4-Descrizione dei servizi MDN
description: Questo capitolo contiene una descrizione di tutti i servizi MDN NetX
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 89df0ab5f09be8ad50a27d23bae8b20d71caa0b4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821821"
---
# <a name="chapter-4---description-of-mdns-services"></a><span data-ttu-id="550bb-103">Capitolo 4-Descrizione dei servizi MDN</span><span class="sxs-lookup"><span data-stu-id="550bb-103">Chapter 4 - Description of mDNS services</span></span>

<span data-ttu-id="550bb-104">Questo capitolo contiene una descrizione di tutti i servizi MDN NetX (elencati di seguito).</span><span class="sxs-lookup"><span data-stu-id="550bb-104">This chapter contains a description of all NetX mDNS services (listed below).</span></span>

> [!NOTE]
> <span data-ttu-id="550bb-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="550bb-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_mdns_create"></a><span data-ttu-id="550bb-106">nx_mdns_create</span><span class="sxs-lookup"><span data-stu-id="550bb-106">nx_mdns_create</span></span>

<span data-ttu-id="550bb-107">Creare un'istanza di MDN</span><span class="sxs-lookup"><span data-stu-id="550bb-107">Create an mDNS instance</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-108">Prototype</span></span>

```C
UINT nx_mdns_create(NX_MDNS *mdns_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool,
    UINT priority, VOID *stack_ptr,
    UINT stack_size, UCHAR *host_name,
    VOID *local_service_cache,
    UINT local_service_cache_size,
    VOID *peer_service_cache,
    UINT peer_service_cache_size,
    VOID (*probing_notify)(NX_MDNS *mdns_ptr,
        UCHAR *name, UINT probing_state));
```

### <a name="description"></a><span data-ttu-id="550bb-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-109">Description</span></span>

<span data-ttu-id="550bb-110">Questo servizio crea un'istanza MDN sull'istanza IP specifica e sulle risorse associate.</span><span class="sxs-lookup"><span data-stu-id="550bb-110">This service creates an mDNS instance on the specific IP instance and associated resources.</span></span> <span data-ttu-id="550bb-111">Viene inoltre creato un thread per gestire i messaggi MDN in ingresso, rispondere alle query e trasmettere periodicamente messaggi di query.</span><span class="sxs-lookup"><span data-stu-id="550bb-111">A thread is also created to handle incoming mDNS messages, to respond to queries, and to periodically transmit query messages.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-112">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-112">Input Parameters</span></span>

- <span data-ttu-id="550bb-113">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-113">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-114">**ip_ptr** Puntatore all'istanza IP associata.</span><span class="sxs-lookup"><span data-stu-id="550bb-114">**ip_ptr** Pointer to the associated IP instance.</span></span>
- <span data-ttu-id="550bb-115">**packet_pool** Puntatore a un pool di pacchetti valido.</span><span class="sxs-lookup"><span data-stu-id="550bb-115">**packet_pool** Pointer to a valid packet pool.</span></span>
- <span data-ttu-id="550bb-116">**priorità** di Priorità del thread MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-116">**priority** Priority of the mDNS thread.</span></span>
- <span data-ttu-id="550bb-117">**stack_ptr** Puntatore all'area dello stack per il thread MDN</span><span class="sxs-lookup"><span data-stu-id="550bb-117">**stack_ptr** Pointer to the stack area for the mDNS thread</span></span>
- <span data-ttu-id="550bb-118">**stack_size** Dimensioni dell'area dello stack.</span><span class="sxs-lookup"><span data-stu-id="550bb-118">**stack_size** Size of the stack area.</span></span>
- <span data-ttu-id="550bb-119">**HOST_NAME** Nome host assegnato a questo nodo.</span><span class="sxs-lookup"><span data-stu-id="550bb-119">**host_name** Host name assigned to this node.</span></span>
- <span data-ttu-id="550bb-120">**local_service_cache** Spazio di archiviazione per servizi registrati locali.</span><span class="sxs-lookup"><span data-stu-id="550bb-120">**local_service_cache** Storage space for local registered services.</span></span>
- <span data-ttu-id="550bb-121">**local_service_cache_size** Dimensione della cache del servizio locale.</span><span class="sxs-lookup"><span data-stu-id="550bb-121">**local_service_cache_size** Size of the local service cache.</span></span>
- <span data-ttu-id="550bb-122">**peer_service_cache** Spazio di archiviazione per le informazioni sul servizio ricevute</span><span class="sxs-lookup"><span data-stu-id="550bb-122">**peer_service_cache** Storage space for service information received</span></span>
- <span data-ttu-id="550bb-123">**peer_service_cache_size** Dimensione della cache del servizio peer</span><span class="sxs-lookup"><span data-stu-id="550bb-123">**peer_service_cache_size** Size of the peer service cache</span></span>
- <span data-ttu-id="550bb-124">**probing_notify** Funzione di callback facoltativa richiamata alla fine dell'operazione di sondaggio.</span><span class="sxs-lookup"><span data-stu-id="550bb-124">**probing_notify** Optional callback function invoked at the end of the probing operation.</span></span> <span data-ttu-id="550bb-125">Invia una notifica all'applicazione indipendentemente dal fatto che il nome host (in caso di abilitazione di MDN in un'interfaccia locale) o il nome del servizio (dopo la registrazione di un servizio) sia univoco.</span><span class="sxs-lookup"><span data-stu-id="550bb-125">It notifies the application whether or not the host name (when enabling mDNS on a local interface), or the service name (after registering a service) is unique.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-126">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-126">Return Values</span></span>

- <span data-ttu-id="550bb-127">L'istanza MDN è stata creata **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="550bb-127">**NX_SUCCESS** (0x00) Successfully created mDNS instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-128">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-128">Allowed From</span></span>

<span data-ttu-id="550bb-129">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-129">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-130">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-130">Example</span></span>

```C
UCHAR stack_ptr[2048];
UCHAR local_cache_ptr[2048];
UCHAR peer_cache_ptr[8192];

/* Create a mDNS instance. */
status = nx_mdns_create(&my_mdns, &ip_0, &pool_0,
    3, stack_ptr, 2048,
    “NETX-MDNS-HOST”,
    local_cache_ptr, 2048,
    peer_cache_ptr, 8192,
    probing_notify);

/* If status is NX_SUCCESS, mDNS instance was created. */
```

## <a name="nx_mdns_delete"></a><span data-ttu-id="550bb-131">nx_mdns_delete</span><span class="sxs-lookup"><span data-stu-id="550bb-131">nx_mdns_delete</span></span>

<span data-ttu-id="550bb-132">Eliminare un'istanza MDN</span><span class="sxs-lookup"><span data-stu-id="550bb-132">Delete an mDNS instance</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-133">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-133">Prototype</span></span>

```C
UINT nx_mdns_delete(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="550bb-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-134">Description</span></span>

<span data-ttu-id="550bb-135">Questo servizio Elimina l'istanza MDN e libera le risorse.</span><span class="sxs-lookup"><span data-stu-id="550bb-135">This service deletes the mDNS instance and frees its resources.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-136">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-136">Input Parameters</span></span>

- <span data-ttu-id="550bb-137">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-137">**mdns_ptr** Pointer to the mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-138">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-138">Return Values</span></span>

- <span data-ttu-id="550bb-139">**NX_SUCCESS** (0x00) ha eliminato correttamente l'istanza MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-139">**NX_SUCCESS** (0x00) Successfully deleted the mDNS instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-140">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-140">Allowed From</span></span>

<span data-ttu-id="550bb-141">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-141">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-142">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-142">Example</span></span>

```C
/* Delete a previously created mDNS instance. */

status = nx_mdns_delete(&my_mdns);

/* If status is NX_SUCCESS, the mDNS instance has been deleted. */
```

## <a name="nx_mdns_enable"></a><span data-ttu-id="550bb-143">nx_mdns_enable</span><span class="sxs-lookup"><span data-stu-id="550bb-143">nx_mdns_enable</span></span>

<span data-ttu-id="550bb-144">Avviare il servizio MDN</span><span class="sxs-lookup"><span data-stu-id="550bb-144">Start the mDNS service</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-145">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-145">Prototype</span></span>

```C
UINT nx_mdns_enable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="550bb-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-146">Description</span></span>

<span data-ttu-id="550bb-147">Questa API Abilita il servizio MDN in un'interfaccia fisica specifica.</span><span class="sxs-lookup"><span data-stu-id="550bb-147">This API enables mDNS service on specific physical interface.</span></span> <span data-ttu-id="550bb-148">Quando il servizio è abilitato, il modulo MDN verifica innanzitutto tutti i nomi di servizio univoci sulla rete prima di rispondere alle query ricevute sull'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="550bb-148">Once the service is enabled, the mDNS module first probes all its unique service names on the network before responding to queries received on the interface.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-149">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-149">Input Parameters</span></span>

- <span data-ttu-id="550bb-150">**mdns_ptr** Puntatore al blocco di controllo dell'istanza MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-150">**mdns_ptr** Pointer to the mDNS instance control block.</span></span>
- <span data-ttu-id="550bb-151">**interface_index** Indice dell'interfaccia in cui deve essere abilitato il servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-151">**interface_index** Index to the interface where the service is to be enabled</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-152">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-152">Return Values</span></span>

- <span data-ttu-id="550bb-153">**NX_SUCCESS** (0x00) ha abilitato correttamente il servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-153">**NX_SUCCESS** (0x00) Successfully enabled the service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-154">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-154">Allowed From</span></span>

<span data-ttu-id="550bb-155">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-155">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-156">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-156">Example</span></span>

```C
/* Enable mDNS service on specific interface. */

status = nx_mdns_enable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was enabled. */
```

## <a name="nx_mdns_disable"></a><span data-ttu-id="550bb-157">nx_mdns_disable</span><span class="sxs-lookup"><span data-stu-id="550bb-157">nx_mdns_disable</span></span>

<span data-ttu-id="550bb-158">Disabilitare il servizio MDN</span><span class="sxs-lookup"><span data-stu-id="550bb-158">Disable the mDNS service</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-159">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-159">Prototype</span></span>

```C
UINT nx_mdns_disable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="550bb-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-160">Description</span></span>

<span data-ttu-id="550bb-161">Questa API Disabilita il servizio MDN sull'interfaccia fisica specifica.</span><span class="sxs-lookup"><span data-stu-id="550bb-161">This API disables mDNS service on the specific physical interface.</span></span> <span data-ttu-id="550bb-162">Quando il servizio è disabilitato, MDN invia messaggi "Goodbye" per ogni servizio locale alla rete collegata all'interfaccia, in modo che i nodi adiacenti ricevano una notifica.</span><span class="sxs-lookup"><span data-stu-id="550bb-162">Once the service is disabled, the mDNS sends "goodbye" messages for every local service to the network that is attached to the interface, so the neighboring nodes are notified.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-163">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-163">Input Parameters</span></span>

- <span data-ttu-id="550bb-164">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-164">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-165">**interface_index** Indice dell'interfaccia in cui deve essere disabilitato il servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-165">**interface_index** Index to the interface where the service is to be disabled</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-166">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-166">Return Values</span></span>

- <span data-ttu-id="550bb-167">Il servizio è stato disabilitato **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="550bb-167">**NX_SUCCESS** (0x00) Successfully disabled the service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-168">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-168">Allowed From</span></span>

<span data-ttu-id="550bb-169">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-169">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-170">Example</span></span>

```C
/* Disable mDNS service on specific interface. */

status = nx_mdns_disable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was disabled. */
```

## <a name="nx_mdns_cache_notify_set"></a><span data-ttu-id="550bb-171">nx_mdns_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="550bb-171">nx_mdns_cache_notify_set</span></span>

<span data-ttu-id="550bb-172">Installa la funzione di notifica completa della cache MDN</span><span class="sxs-lookup"><span data-stu-id="550bb-172">Installs the mDNS cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-173">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-173">Prototype</span></span>

```c
UINT nx_mdns_cache_notify_set(NX_MDNS *mdns_ptr,
    VOID (*cache_full_notify_cb)(NX_MDNS *mdns_ptr,
        UINT state, UINT cache_type));
```

### <a name="description"></a><span data-ttu-id="550bb-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-174">Description</span></span>

<span data-ttu-id="550bb-175">Questo servizio installa una funzione di callback fornita dall'utente, che viene richiamata quando la cache del servizio locale o la cache del servizio peer diventa piena.</span><span class="sxs-lookup"><span data-stu-id="550bb-175">This service installs a user-supplied callback function, which is invoked when either the local service cache or peer service cache becomes full.</span></span> <span data-ttu-id="550bb-176">Quando la cache del servizio è completa, non è possibile aggiungere altri record di risorse MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-176">When the service cache is full, no more mDNS Resource Record can be added.</span></span> <span data-ttu-id="550bb-177">Si noti che la cache del servizio può diventare piena a causa della frammentazione interna, quando vengono aggiunti e rimossi servizi con diverse lunghezze di stringa.</span><span class="sxs-lookup"><span data-stu-id="550bb-177">Note that the service cache may become full as a result of internal fragmentation, when services with various string lengths are added and removed.</span></span> <span data-ttu-id="550bb-178">Quando viene ricevuta una notifica completa della cache nella cache del servizio peer, l'applicazione può usare il servizio "*nx_mdns_service_cache_clear"* per cancellare tutte le voci nella cache del servizio peer.</span><span class="sxs-lookup"><span data-stu-id="550bb-178">On receiving a cache full notification on peer service cache, the application may use the service "*nx_mdns_service_cache_clear"* to erase all entries in the peer service cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-179">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-179">Input Parameters</span></span>

- <span data-ttu-id="550bb-180">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-180">**mdns_ptr** Pointer to the mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-181">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-181">Return Values</span></span>

- <span data-ttu-id="550bb-182">**NX_SUCCESS** (0x00) ha installato correttamente la funzione di callback Notify cache MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-182">**NX_SUCCESS** (0x00) Successfully installed the mDNS cache notify callback function.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-183">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-183">Allowed From</span></span>

<span data-ttu-id="550bb-184">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-184">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-185">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-185">Example</span></span>

```C
/* Set mDNS cache notify callback. */

status = nx_mdns_cache_notify_set(&my_mdns, cache_full_nofiy_cb);

/* If status is NX_SUCCESS, mDNS cache notify callback was set. */
```

## <a name="nx_mdns_cache_notify_clear"></a><span data-ttu-id="550bb-186">nx_mdns_cache_notify_clear</span><span class="sxs-lookup"><span data-stu-id="550bb-186">nx_mdns_cache_notify_clear</span></span>

<span data-ttu-id="550bb-187">Cancella la funzione di notifica completa della cache del servizio MDN</span><span class="sxs-lookup"><span data-stu-id="550bb-187">Clear the mDNS service cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-188">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-188">Prototype</span></span>

```C
UINT nx_mdns_cache_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="550bb-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-189">Description</span></span>

<span data-ttu-id="550bb-190">Questo servizio Cancella una funzione di callback di notifica della cache del servizio fornita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="550bb-190">This service clears a user-supplied service cache notify callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-191">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-191">Input Parameters</span></span>

- <span data-ttu-id="550bb-192">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-192">**mdns_ptr** Pointer to the mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-193">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-193">Return Values</span></span>

- <span data-ttu-id="550bb-194">**NX_SUCCESS** (0x00) ha cancellato correttamente la funzione di callback Notify della cache del servizio MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-194">**NX_SUCCESS** (0x00) Successfully cleared the mDNS service cache notify callback function.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-195">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-195">Allowed From</span></span>

<span data-ttu-id="550bb-196">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-196">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-197">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-197">Example</span></span>

```C
/* Clear mDNS cache notify callback. */

status = nx_mdns_cache_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, mDNS cache notify callback clear. */
```

## <a name="nx_mdns_domain_name_set"></a><span data-ttu-id="550bb-198">nx_mdns_domain_name_set</span><span class="sxs-lookup"><span data-stu-id="550bb-198">nx_mdns_domain_name_set</span></span>

<span data-ttu-id="550bb-199">Imposta il nome di dominio</span><span class="sxs-lookup"><span data-stu-id="550bb-199">Sets the domain name</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-200">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-200">Prototype</span></span>

```C
UINT nx_mdns_domain_name_set(NX_MDNS *mdns_ptr, CHAR *domain_name);
```

### <a name="description"></a><span data-ttu-id="550bb-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-201">Description</span></span>

<span data-ttu-id="550bb-202">Questo servizio configura il nome di dominio locale predefinito.</span><span class="sxs-lookup"><span data-stu-id="550bb-202">This service sets up the default local domain name.</span></span> <span data-ttu-id="550bb-203">Quando viene creata l'istanza di MDN, il nome di dominio locale predefinito viene impostato su ". local".</span><span class="sxs-lookup"><span data-stu-id="550bb-203">When the mDNS instance is created, the default local domain name is set to “.local”.</span></span> <span data-ttu-id="550bb-204">Questa API consente a un'applicazione di sovrascrivere il nome di dominio locale predefinito.</span><span class="sxs-lookup"><span data-stu-id="550bb-204">This API allows an application to overwrite the default local domain name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-205">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-205">Input Parameters</span></span>

- <span data-ttu-id="550bb-206">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-206">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-207">**Domain_name** Nome di dominio da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="550bb-207">**domain_name** The domain name to be used.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-208">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-208">Return Values</span></span>

- <span data-ttu-id="550bb-209">Il dominio locale è stato configurato con **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="550bb-209">**NX_SUCCESS** (0x00) Successfully configured local domain.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-210">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-210">Allowed From</span></span>

<span data-ttu-id="550bb-211">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-211">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-212">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-212">Example</span></span>

```C
/* Set the domain name. */

status = nx_mdns_domain_name_set(&my_mdns, “home”);

/* If status is NX_SUCCESS, the “home” domain name was set. */
```

## <a name="nx_mdns_service_announcement_timing_set"></a><span data-ttu-id="550bb-213">nx_mdns_service_announcement_timing_set</span><span class="sxs-lookup"><span data-stu-id="550bb-213">nx_mdns_service_announcement_timing_set</span></span>

<span data-ttu-id="550bb-214">Imposta i parametri di intervallo per i messaggi di annuncio del servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-214">Sets the timing parameters for service announcement messages</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-215">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-215">Prototype</span></span>

```C
UINT nx_mdns_service_announcement_timing_set(NX_MDNS *mdns_ptr,
    UINT t, UINT p, UINT k, UINT retrans_interval,
    UINT period_interval, UINT max_time);
```

### <a name="description"></a><span data-ttu-id="550bb-216">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-216">Description</span></span>

<span data-ttu-id="550bb-217">Questo servizio riconfigura i parametri di intervallo utilizzati da MDN durante l'invio degli annunci di servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-217">This service reconfigures the timing parameters employed by mDNS when sending the service announcements.</span></span> <span data-ttu-id="550bb-218">Il periodo di pubblicazione *inizia da un segno di* graduazione e può essere espanso in modo telescopico con 2 alla potenza di *k* Factor.</span><span class="sxs-lookup"><span data-stu-id="550bb-218">Publish period starts from *t* ticks and can be expanded telescopically with 2 to the power of *k* factor.</span></span> <span data-ttu-id="550bb-219">Il numero di ripetizioni per annuncio è *p*, l'intervallo tra ogni annuncio ripetuto è il ciclo di *intervallo* e il numero di periodi di annuncio max_time.</span><span class="sxs-lookup"><span data-stu-id="550bb-219">The number of repetitions per advertisement is *p*, the interval between each repeated advertisement is *interval* ticks, and the number of announcement period is max_time.</span></span> <span data-ttu-id="550bb-220">Per impostazione predefinita, il periodo iniziale è impostato su 1 secondo, con k = 1 (il periodo raddoppia ogni volta), *p = 1* (nessuna ripetizione), retrans_interval = 0 (nessun intervallo di tempo), Period_interval = 0xFFFFFFFF (intervallo massimo periodo) e max_time = 3 (numero di annunci).</span><span class="sxs-lookup"><span data-stu-id="550bb-220">By default, the initial period is set to 1 second, with k = 1 (the period doubles each time), *p = 1* (no repetition), retrans_interval = 0(no time interval), period_interval = 0xFFFFFFFF(max period interval) and max_time = 3(number of advertisement).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-221">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-221">Input Parameters</span></span>

- <span data-ttu-id="550bb-222">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-222">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-223">**t** numero di cicli per il periodo iniziale.</span><span class="sxs-lookup"><span data-stu-id="550bb-223">**t** Number of ticks for the initial period.</span></span> <span data-ttu-id="550bb-224">Il valore predefinito è 100 cicli per 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="550bb-224">Default is 100 ticks for 1 second.</span></span>
- <span data-ttu-id="550bb-225">numero **p** di ripetizioni.</span><span class="sxs-lookup"><span data-stu-id="550bb-225">**p** Number of repetitions.</span></span> <span data-ttu-id="550bb-226">Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="550bb-226">Default value is 1.</span></span>
- <span data-ttu-id="550bb-227">fattore telescopico **k** .</span><span class="sxs-lookup"><span data-stu-id="550bb-227">**k** Telescopic factor.</span></span> <span data-ttu-id="550bb-228">Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="550bb-228">Default value is 1.</span></span>
- <span data-ttu-id="550bb-229">**retrans_interval** Numero di cicli di attesa prima dell'invio di messaggi di annuncio ripetuti.</span><span class="sxs-lookup"><span data-stu-id="550bb-229">**retrans_interval** Number of ticks to wait before sending out repeated announcement messages.</span></span> <span data-ttu-id="550bb-230">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="550bb-230">Default value is 0.</span></span>
- <span data-ttu-id="550bb-231">**period_interval** Numero di cicli tra due periodi di annuncio.</span><span class="sxs-lookup"><span data-stu-id="550bb-231">**period_interval** Number of ticks between two announcement period.</span></span> <span data-ttu-id="550bb-232">Il valore predefinito è 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="550bb-232">Default value is 0xFFFFFFFF.</span></span>
- <span data-ttu-id="550bb-233">**max_time** Numero di periodi di annuncio da utilizzare per l'annuncio.</span><span class="sxs-lookup"><span data-stu-id="550bb-233">**max_time** Number of announcement period to use for the advertisement.</span></span> <span data-ttu-id="550bb-234">Dopo i periodi di annuncio *max_time* , non vengono inviati altri messaggi di annuncio.</span><span class="sxs-lookup"><span data-stu-id="550bb-234">After the *max_time* announcement periods, no more announcement messages are sent.</span></span> <span data-ttu-id="550bb-235">Il valore predefinito è 3.</span><span class="sxs-lookup"><span data-stu-id="550bb-235">Default value is 3.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-236">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-236">Return Values</span></span>

- <span data-ttu-id="550bb-237">**NX_SUCCESS** (0x00) imposta correttamente i valori di intervallo.</span><span class="sxs-lookup"><span data-stu-id="550bb-237">**NX_SUCCESS** (0x00) Successfully sets the timing values.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-238">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-238">Allowed From</span></span>

<span data-ttu-id="550bb-239">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-239">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-240">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-240">Example</span></span>

```C
/* Set the service announcement timing. */

status = nx_mdns_service_announcement_timing_set(&my_mdns, 100,
    1, 1, 0, 0xFFFFFFFF, 3);

/* If status is NX_SUCCESS, the service announcement timing was set. */
```

## <a name="nx_mdns_service_add"></a><span data-ttu-id="550bb-241">nx_mdns_service_add</span><span class="sxs-lookup"><span data-stu-id="550bb-241">nx_mdns_service_add</span></span>

<span data-ttu-id="550bb-242">Aggiungere un servizio locale</span><span class="sxs-lookup"><span data-stu-id="550bb-242">Add a local service</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-243">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-243">Prototype</span></span>

```C
UINT nx_mdns_service_add(NX_MDNS *mdns_ptr, CHAR *instance,
    CHAR *service, CHAR *subtype, UINT ttl, USHORT priority,
    USHORT weight, USHORT port, UCHAR *text, UCHAR is_unique,
    UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="550bb-244">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-244">Description</span></span>

<span data-ttu-id="550bb-245">Questa API registra un servizio offerto dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="550bb-245">This API registers a service offered by the application.</span></span> <span data-ttu-id="550bb-246">Se viene impostato il flag *is_unique* , MDN verifica il nome del servizio per assicurarsi che sia univoco nella rete locale prima di iniziare ad annunciare il servizio sulla rete.</span><span class="sxs-lookup"><span data-stu-id="550bb-246">If the flag *is_unique* is set, mDNS probes the service name to make sure it is unique on the local network before starting to announce the service on the network.</span></span> <span data-ttu-id="550bb-247">*Instance* è la parte dell'istanza del nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-247">*Instance* is the instance portion of the service name.</span></span> <span data-ttu-id="550bb-248">Il *servizio* è la parte del servizio del nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-248">The *service* is the service portion of the service name.</span></span> <span data-ttu-id="550bb-249">Ad esempio, "_http. _tcp" è un servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-249">For example “_http._tcp” is a service.</span></span> <span data-ttu-id="550bb-250">Per descrivere un servizio con sottotipo, il chiamante deve utilizzare il parametro del *sottotipo* .</span><span class="sxs-lookup"><span data-stu-id="550bb-250">To describe a service with subtype, caller must use the *subtype* parameter.</span></span> <span data-ttu-id="550bb-251">Ad esempio, se il servizio desiderato è "_printer. _sub. _http. _tcp", il campo del servizio è "_http. _tcp: e il campo del sottotipo è" _printer ".</span><span class="sxs-lookup"><span data-stu-id="550bb-251">For example, if the desired service is “_printer._sub._http._tcp”, the service field is “_http._tcp:, and the subtype field is “_printer”.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-252">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-252">Input Parameters</span></span>

- <span data-ttu-id="550bb-253">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-253">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-254">**istanza** di Puntatore al nome dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-254">**instance** Pointer to the instance name of the service.</span></span>
- <span data-ttu-id="550bb-255">**servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo.</span><span class="sxs-lookup"><span data-stu-id="550bb-255">**service** Pointer to the mDNS service type, excluding subtype information.</span></span>
- <span data-ttu-id="550bb-256">**sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-256">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>
- <span data-ttu-id="550bb-257">**priorità** di Priorità del servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-257">**priority** Service priority</span></span>
- <span data-ttu-id="550bb-258">**peso** Peso del servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-258">**weight** Service weight</span></span>
- <span data-ttu-id="550bb-259">**porta** Numero di porta TCP o UDP utilizzato dal servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-259">**port** TCP or UDP port number the service uses</span></span>
- <span data-ttu-id="550bb-260">**testo** Informazioni aggiuntive sul testo</span><span class="sxs-lookup"><span data-stu-id="550bb-260">**text** Additional text information</span></span>
- <span data-ttu-id="550bb-261">**is_unique** Flag booleano che indica se il servizio è condiviso o univoco.</span><span class="sxs-lookup"><span data-stu-id="550bb-261">**is_unique** Boolean flag indicating whether the service is shared or unique.</span></span> <span data-ttu-id="550bb-262">Per i servizi registrati come univoci, gli MDN devono verificare il servizio sulla rete prima di iniziare a offrirlo.</span><span class="sxs-lookup"><span data-stu-id="550bb-262">For services registered as unique, mDNS must probe the service on the network before starting offering it.</span></span>
- <span data-ttu-id="550bb-263">**Interface_index** Interfaccia fisica a cui viene offerto il servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-263">**Interface_index** Physical interface the service is offered through.</span></span> <span data-ttu-id="550bb-264">Per un servizio offerto tramite uno dei servizi collegati, viene usato il valore *NX_MDNS_ALL_INTERFACES* .</span><span class="sxs-lookup"><span data-stu-id="550bb-264">For a service that is offered through any of the attached services, the value *NX_MDNS_ALL_INTERFACES* is used.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-265">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-265">Return Values</span></span>

- <span data-ttu-id="550bb-266">**NX_SUCCESS** (0x00) ha registrato correttamente il servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-266">**NX_SUCCESS** (0x00) Successfully registered the service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-267">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-267">Allowed From</span></span>

<span data-ttu-id="550bb-268">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-268">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-269">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-269">Example</span></span>

```C
/* Add local service. */

status = nx_mdns_service_add(&my_mdns, “NETX-SERVICE”,
    “_http._tcp”, NX_NULL,
    NX_NULL, 0, 0, 0, 80, NX_TRUE, 0);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was added. */
```

## <a name="nx_mdns_service_delete"></a><span data-ttu-id="550bb-270">nx_mdns_service_delete</span><span class="sxs-lookup"><span data-stu-id="550bb-270">nx_mdns_service_delete</span></span>

<span data-ttu-id="550bb-271">Rimuovere un servizio registrato precedente</span><span class="sxs-lookup"><span data-stu-id="550bb-271">Remove a previous registered service</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-272">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-272">Prototype</span></span>

```C
UINT nx_mdns_service_delete(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype);
```

### <a name="description"></a><span data-ttu-id="550bb-273">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-273">Description</span></span>

<span data-ttu-id="550bb-274">Questa API Elimina un servizio registrato precedente.</span><span class="sxs-lookup"><span data-stu-id="550bb-274">This API deletes a previous registered service.</span></span> <span data-ttu-id="550bb-275">Quando il servizio viene eliminato, i messaggi "Goodbye" vengono inviati alla rete locale, in modo che i nodi adiacenti ricevano una notifica.</span><span class="sxs-lookup"><span data-stu-id="550bb-275">As the service is deleted, "goodbye" messages are sent to the local network so the neighboring nodes are notified.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-276">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-276">Input Parameters</span></span>

- <span data-ttu-id="550bb-277">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-277">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-278">**istanza** di Puntatore al nome dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-278">**instance** Pointer to the instance name of the service.</span></span>
- <span data-ttu-id="550bb-279">**servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo.</span><span class="sxs-lookup"><span data-stu-id="550bb-279">**service** Pointer to the mDNS service type, excluding subtype information.</span></span>
- <span data-ttu-id="550bb-280">**sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-280">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-281">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-281">Return Values</span></span>

- <span data-ttu-id="550bb-282">**NX_SUCCESS** (0x00) ha eliminato correttamente il servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-282">**NX_SUCCESS** (0x00) Successfully deleted the service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-283">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-283">Allowed From</span></span>

<span data-ttu-id="550bb-284">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-284">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-285">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-285">Example</span></span>

```C
/* Delete local service. */

status = nx_mdns_service_delete(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was deleted. */
```

## <a name="nx_mdns_service_one_shot_query"></a><span data-ttu-id="550bb-286">nx_mdns_service_one_shot_query</span><span class="sxs-lookup"><span data-stu-id="550bb-286">nx_mdns_service_one_shot_query</span></span>

<span data-ttu-id="550bb-287">Avviare l'individuazione del servizio One-Shot</span><span class="sxs-lookup"><span data-stu-id="550bb-287">Initiate one-shot service discovery</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-288">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-288">Prototype</span></span>

```C
UINT nx_mdns_service_one_shot_query(NX_MDNS *mdns_ptr,
    UCHAR *instance,
    UCHAR *service,
    UCHAR *subtype,
    NX_MDNS_SERVICE *service_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="550bb-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-289">Description</span></span>

<span data-ttu-id="550bb-290">Questo servizio esegue una query MDN monouso.</span><span class="sxs-lookup"><span data-stu-id="550bb-290">This service performs a one-shot mDNS query.</span></span> <span data-ttu-id="550bb-291">Se il servizio specificato viene trovato nella cache del servizio peer, viene restituita la prima istanza.</span><span class="sxs-lookup"><span data-stu-id="550bb-291">If the specified service is found in the peer service cache, the first instance is returned.</span></span> <span data-ttu-id="550bb-292">Se non vengono trovati servizi nella cache del servizio peer locale, il modulo MDN emette un comando di query e attende la risposta.</span><span class="sxs-lookup"><span data-stu-id="550bb-292">If no services are found in the local peer service cache, the mDNS module issues a query command and wait for response.</span></span> <span data-ttu-id="550bb-293">Il servizio è bloccato fino a quando non viene ricevuta la prima risposta o si verifica il timeout della query.</span><span class="sxs-lookup"><span data-stu-id="550bb-293">The service is blocked till either the first answer is received or the query times out.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-294">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-294">Input Parameters</span></span>

- <span data-ttu-id="550bb-295">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-295">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-296">**istanza** di Puntatore al nome dell'istanza del servizio, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-296">**instance** Pointer to the instance name of the service, if applicable.</span></span>
- <span data-ttu-id="550bb-297">**servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo.</span><span class="sxs-lookup"><span data-stu-id="550bb-297">**service** Pointer to the mDNS service type, excluding subtype information.</span></span> <span data-ttu-id="550bb-298">l'applicazione deve specificare il tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-298">the application must specify the service type.</span></span>
- <span data-ttu-id="550bb-299">**sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-299">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>
- <span data-ttu-id="550bb-300">**service_ptr** Puntatore fornito dall'utente alla struttura NX_MDNS_SERVICE che archivia i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="550bb-300">**service_ptr** User provided pointer to NX_MDNS_SERVICE structure that stores the query results.</span></span>
- <span data-ttu-id="550bb-301">**WAIT_OPTION** Quantità di tempo, espressa in cicli, per l'attesa di una risposta.</span><span class="sxs-lookup"><span data-stu-id="550bb-301">**wait_option** The amount of time, in ticks, to wait for a response.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-302">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-302">Return Values</span></span>

- <span data-ttu-id="550bb-303">**NX_SUCCESS** (0x00) ha ottenuto correttamente le informazioni sul servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-303">**NX_SUCCESS** (0x00) Successfully obtained service information.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-304">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-304">Allowed From</span></span>

<span data-ttu-id="550bb-305">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-305">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-306">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-306">Example</span></span>

```C
/* Start service one shot query. */

status = nx_mdns_service_one_shot_query(&my_mdns, “NETX-SERVICE”, “_http._tcp”,
    NX_NULL, service_ptr, 500);

/* If status is NX_SUCCESS, The query with
    name: NetX-SERVICE._http._tcp.local,
     type: ANY (SRV and TXT) was sent.
    And the answer was stored in service_ptr if success. */
```

## <a name="nx_mdns_service_continuous_query"></a><span data-ttu-id="550bb-307">nx_mdns_service_continuous_query</span><span class="sxs-lookup"><span data-stu-id="550bb-307">nx_mdns_service_continuous_query</span></span>

<span data-ttu-id="550bb-308">Avviare l'individuazione continua del servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-308">Initiate continuous service discovery</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-309">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-309">Prototype</span></span>

```C
UINT nx_mdns_service_continous_query(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a><span data-ttu-id="550bb-310">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-310">Description</span></span>

<span data-ttu-id="550bb-311">Questo servizio avvia una query continua.</span><span class="sxs-lookup"><span data-stu-id="550bb-311">This service starts a continuous query.</span></span> <span data-ttu-id="550bb-312">Si noti che il servizio viene restituito immediatamente.</span><span class="sxs-lookup"><span data-stu-id="550bb-312">Note that the service returns immediately.</span></span> <span data-ttu-id="550bb-313">Dopo aver emesso una query continua, l'applicazione può recuperare il record di servizio usando l'API *nx_mdns_service_lookup*.</span><span class="sxs-lookup"><span data-stu-id="550bb-313">After issuing a continuous query, the application may retrieve service record by using the API *nx_mdns_service_lookup*.</span></span> <span data-ttu-id="550bb-314">Per arrestare la query continua, l'applicazione può usare l'API *nx_mdns_service_query_stop*</span><span class="sxs-lookup"><span data-stu-id="550bb-314">To stop the continuous query, the application may use the API *nx_mdns_service_query_stop*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-315">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-315">Input Parameters</span></span>

- <span data-ttu-id="550bb-316">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-316">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-317">**istanza** di Puntatore al nome dell'istanza del servizio, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-317">**instance** Pointer to the instance name of the service, if applicable.</span></span>
- <span data-ttu-id="550bb-318">**servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-318">**service** Pointer to the mDNS service type, excluding subtype information, if applicable.</span></span>
- <span data-ttu-id="550bb-319">**sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-319">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-320">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-320">Return Values</span></span>

- <span data-ttu-id="550bb-321">La query continua è stata avviata **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="550bb-321">**NX_SUCCESS** (0x00) Successfully started continues query.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-322">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-322">Allowed From</span></span>

<span data-ttu-id="550bb-323">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-323">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-324">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-324">Example</span></span>

```C
/* Start service continuous query. */

status = nx_mdns_service_continuous_query(&my_mdns,
    “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The continuous query with
    name: NetX-SERVICE._http._tcp.local,
    type: ANY (SRV and TXT) was added.
    And the query will be periodically sent. */
```

## <a name="nx_mdns_service_query_stop"></a><span data-ttu-id="550bb-325">nx_mdns_service_query_stop</span><span class="sxs-lookup"><span data-stu-id="550bb-325">nx_mdns_service_query_stop</span></span>

<span data-ttu-id="550bb-326">Interrompere l'individuazione di un servizio continuo emesso in precedenza</span><span class="sxs-lookup"><span data-stu-id="550bb-326">Cease a previously issued continuous service discovery</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-327">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-327">Prototype</span></span>

```C
UINT nx_mdns_service_query_stop(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a><span data-ttu-id="550bb-328">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-328">Description</span></span>

<span data-ttu-id="550bb-329">Questa API termina un'individuazione del servizio continua rilasciata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="550bb-329">This API terminates a previous issued continuous service discovery.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-330">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-330">Input Parameters</span></span>

- <span data-ttu-id="550bb-331">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-331">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-332">**istanza** di Puntatore al nome dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-332">**instance** Pointer to the instance name of the service.</span></span>
- <span data-ttu-id="550bb-333">**servizio** di Puntatore al tipo di servizio MDN, informazioni sul sottotipo.</span><span class="sxs-lookup"><span data-stu-id="550bb-333">**service** Pointer to the mDNS service type, subtype information.</span></span>
- <span data-ttu-id="550bb-334">**sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-334">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-335">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-335">Return Values</span></span>

- <span data-ttu-id="550bb-336">**NX_SUCCESS** (0x00) ha arrestato correttamente la query continua.</span><span class="sxs-lookup"><span data-stu-id="550bb-336">**NX_SUCCESS** (0x00) Successfully stopped continues query.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-337">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-337">Allowed From</span></span>

<span data-ttu-id="550bb-338">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-338">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-339">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-339">Example</span></span>

```C
/* Stop service continuous query. */

status = nx_mdns_service_query_stop(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The continuous query with
    name: NetX-SERVICE._http._tcp.local,
    type: ANY (SRV and TXT) was stopped. */
```

## <a name="nx_mdns_service_lookup"></a><span data-ttu-id="550bb-340">nx_mdns_service_lookup</span><span class="sxs-lookup"><span data-stu-id="550bb-340">nx_mdns_service_lookup</span></span>

<span data-ttu-id="550bb-341">Recupera il servizio dalla cache del servizio peer locale</span><span class="sxs-lookup"><span data-stu-id="550bb-341">Retrieves the service from the local peer service cache</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-342">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-342">Prototype</span></span>

```C
UINT nx_mdns_service_lookup(NXD_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype, UINT instance_index,
    NXD_MDNS_SERVICE *service_ptr);
```

### <a name="description"></a><span data-ttu-id="550bb-343">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-343">Description</span></span>

<span data-ttu-id="550bb-344">Questo servizio Cerca i servizi che corrispondono al nome dell'istanza (se specificati) e il tipo di servizio nella cache del servizio peer locale.</span><span class="sxs-lookup"><span data-stu-id="550bb-344">This service looks up services matching the instance name (if provided) and the type of service in the local peer service cache.</span></span> <span data-ttu-id="550bb-345">L'applicazione deve avviare la ricerca del servizio con *instance_index* impostato su zero per il primo servizio nella cache che corrisponde alla descrizione.</span><span class="sxs-lookup"><span data-stu-id="550bb-345">Application shall start the service lookup with *instance_index* set to zero for the first service in the cache that matches the description.</span></span> <span data-ttu-id="550bb-346">L'applicazione continuerà a usare questo servizio aumentando *instance_index* valore per i servizi aggiuntivi presenti nella cache, fino a quando il servizio non restituisce *NX_NO_MORE_ENTRIES*, che indica la fine della cache.</span><span class="sxs-lookup"><span data-stu-id="550bb-346">Application shall keep using this service with increasing *instance_index* value for additional services found in the cache, till the service returns *NX_NO_MORE_ENTRIES*, which indicates the end of the cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-347">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-347">Input Parameters</span></span>

- <span data-ttu-id="550bb-348">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-348">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-349">**istanza** di Puntatore al nome dell'istanza del servizio, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-349">**instance** Pointer to the instance name of the service, if applicable.</span></span>
- <span data-ttu-id="550bb-350">**servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-350">**service** Pointer to the mDNS service type, excluding subtype information, if applicable.</span></span>
- <span data-ttu-id="550bb-351">**sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="550bb-351">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>
- <span data-ttu-id="550bb-352">**Instance_index** Numero di indice dell'istanza da restituire.</span><span class="sxs-lookup"><span data-stu-id="550bb-352">**Instance_index** Index number to the instance to be returned.</span></span>
- <span data-ttu-id="550bb-353">**service_ptr** Puntatore fornito dall'utente alla struttura NX_MDNS_SERVICE che archivia i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="550bb-353">**service_ptr** User provided pointer to NX_MDNS_SERVICE structure that stores the lookup results.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-354">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-354">Return Values</span></span>

- <span data-ttu-id="550bb-355">Il servizio è stato recuperato da **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="550bb-355">**NX_SUCCESS** (0x00) Successfully retrieved the service</span></span>
- <span data-ttu-id="550bb-356">**NX_NO_MORE_ENTRIES** (0x17) non viene trovata alcuna voce di servizio in corrispondenza del numero di indice specificato.</span><span class="sxs-lookup"><span data-stu-id="550bb-356">**NX_NO_MORE_ENTRIES** (0x17) No service entry is found at the specified index number.</span></span> <span data-ttu-id="550bb-357">Questo codice di errore indica la fine della ricerca.</span><span class="sxs-lookup"><span data-stu-id="550bb-357">This error code indicates the end of the search.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-358">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-358">Allowed From</span></span>

<span data-ttu-id="550bb-359">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-359">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-360">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-360">Example</span></span>

```C
/* Lookup the service on specific index. */

status = nx_mdns_service_lookup(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL,
    0, service_ptr);

/* If status is NX_SUCCESS, The service with
    name: NetX-SERVICE._http._tcp.local, was retrieved. */
```

## <a name="nx_mdns_service_ignore_set"></a><span data-ttu-id="550bb-361">nx_mdns_service_ignore_set</span><span class="sxs-lookup"><span data-stu-id="550bb-361">nx_mdns_service_ignore_set</span></span>

<span data-ttu-id="550bb-362">Configura un set di ignoramenti del servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-362">Configures a service ignore set</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-363">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-363">Prototype</span></span>

```C
UINT nx_mdns_service_ignore_set(NX_MDNS *mdns_ptr, ULONG service_mask);
```

### <a name="description"></a><span data-ttu-id="550bb-364">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-364">Description</span></span>

<span data-ttu-id="550bb-365">Questa API configura una maschera per ignorare i servizi specificati dalla maschera di maschera *service_mask* .</span><span class="sxs-lookup"><span data-stu-id="550bb-365">This API configures a mask to ignore services specified by the *service_mask* bitmask.</span></span> <span data-ttu-id="550bb-366">L'utente può facoltativamente utilizzare il service_mask per selezionare i tipi di servizio che non si desidera memorizzare nella cache.</span><span class="sxs-lookup"><span data-stu-id="550bb-366">User may optionally use the service_mask to select service types it does not wish to be cached.</span></span> <span data-ttu-id="550bb-367">Nella tabella *nx_mdns_service_types* in *nxd_mdns. c* viene definito un elenco di servizi.</span><span class="sxs-lookup"><span data-stu-id="550bb-367">A list of services is defined in the table *nx_mdns_service_types* in *nxd_mdns.c.*</span></span> <span data-ttu-id="550bb-368">La maschera corrispondente del primo tipo di servizio in nx_mdns_service_types [] è 0x00000001, la maschera del secondo tipo di servizio è 0x00000002 e così via.</span><span class="sxs-lookup"><span data-stu-id="550bb-368">The corresponding mask of the first service type in nx_mdns_service_types[] is 0x00000001, the mask of the second service type is 0x00000002, and so on.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-369">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-369">Input Parameters</span></span>

- <span data-ttu-id="550bb-370">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-370">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-371">**service_mask** Tipi di servizio definiti dall'utente da ignorare.</span><span class="sxs-lookup"><span data-stu-id="550bb-371">**service_mask** User-defined service types to ignore.</span></span> <span data-ttu-id="550bb-372">La maschera è un tipo ULONG a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="550bb-372">The mask is a 32-bit ULONG type.</span></span> <span data-ttu-id="550bb-373">Ogni bit rappresenta una voce nella matrice *nx_mdns_service_types* definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="550bb-373">Each bit represents an entry in the user-defined *nx_mdns_service_types* array.</span></span> <span data-ttu-id="550bb-374">Se viene impostato un bit, il tipo di servizio corrispondente specificato nella *nx_mdns_service_type* matrice non verrà archiviato nella cache del servizio peer.</span><span class="sxs-lookup"><span data-stu-id="550bb-374">If a bit is set, the corresponding service type specified in the *nx_mdns_service_type* array will not store in the peer service cache.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-375">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-375">Return Values</span></span>

- <span data-ttu-id="550bb-376">**NX_SUCCESS** (0x00) imposta correttamente il servizio ignora maschera.</span><span class="sxs-lookup"><span data-stu-id="550bb-376">**NX_SUCCESS** (0x00) Successfully sets the service ignore mask.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-377">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-377">Allowed From</span></span>

<span data-ttu-id="550bb-378">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-378">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-379">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-379">Example</span></span>

```C
/* Set the service mask to ignore the specified service. */

status = nx_mdns_service_ignore_set(&my_mdns, 0x00000003);

/* If status is NX_SUCCESS, The service with
    type “_device-info” and “_http” will be ignored. */
```

## <a name="nx_mdns_service_notify_set"></a><span data-ttu-id="550bb-380">nx_mdns_service_notify_set</span><span class="sxs-lookup"><span data-stu-id="550bb-380">nx_mdns_service_notify_set</span></span>

<span data-ttu-id="550bb-381">Configura una funzione di callback per la notifica della modifica del servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-381">Configures a service change notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-382">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-382">Prototype</span></span>

```C
UINT nx_mdns_service_notify_set(NX_MDNS *mdns_ptr, ULONG service_mask,
    VOID (*service_change_notify)(NX_MDNS *mdns_ptr,
    NX_MDNS_SERVICE *service_ptr, UINT state));
```

### <a name="description"></a><span data-ttu-id="550bb-383">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-383">Description</span></span>

<span data-ttu-id="550bb-384">Questa API configura una funzione di callback di notifica della modifica del servizio.</span><span class="sxs-lookup"><span data-stu-id="550bb-384">This API configures a service change notify callback function.</span></span> <span data-ttu-id="550bb-385">Questa funzione di callback viene richiamata quando un servizio offerto da altri nodi sulla rete viene aggiunto, modificato o non più disponibile.</span><span class="sxs-lookup"><span data-stu-id="550bb-385">This callback function is invoked when a service offered by other nodes on the network is added, changed or is no longer available.</span></span> <span data-ttu-id="550bb-386">L'utente può facoltativamente utilizzare il service_mask per selezionare i tipi di servizio che si desidera monitorare.</span><span class="sxs-lookup"><span data-stu-id="550bb-386">User may optionally use the service_mask to select service types it wishes to monitor.</span></span> <span data-ttu-id="550bb-387">Un elenco di servizi monitorati è hardcoded nella tabella *nx_mdns_service_types* in *nxd_mdns. c.*</span><span class="sxs-lookup"><span data-stu-id="550bb-387">A list of services being monitored are hard-coded in the table *nx_mdns_service_types* in *nxd_mdns.c.*</span></span>

<span data-ttu-id="550bb-388">La maschera corrispondente del primo tipo di servizio in nx_mdns_service_types [] è 0x00000001, la maschera del secondo tipo di servizio è 0x00000002 e così via.</span><span class="sxs-lookup"><span data-stu-id="550bb-388">The corresponding mask of the first service type in nx_mdns_service_types[] is 0x00000001, the mask of the second service type is 0x00000002, and so on.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-389">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-389">Input Parameters</span></span>

- <span data-ttu-id="550bb-390">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-390">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-391">**service_mask** Tipi di servizio definiti dall'utente da monitorare.</span><span class="sxs-lookup"><span data-stu-id="550bb-391">**service_mask** User-defined service types to monitor.</span></span> <span data-ttu-id="550bb-392">La maschera è un tipo ULONG a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="550bb-392">The mask is a 32-bit ULONG type.</span></span> <span data-ttu-id="550bb-393">Ogni bit rappresenta una voce nella matrice *nx_mdns_service_types* .</span><span class="sxs-lookup"><span data-stu-id="550bb-393">Each bit represents an entry in the *nx_mdns_service_types* array.</span></span>
- <span data-ttu-id="550bb-394">**service_change_notify** Funzione di callback da richiamare quando viene modificato il servizio specificato.</span><span class="sxs-lookup"><span data-stu-id="550bb-394">**service_change_notify** The callback function to be invoked when the specified service is changed.</span></span> <span data-ttu-id="550bb-395">Le informazioni dettagliate sul servizio vengono restituite nella memoria a cui punta *service_ptr.*</span><span class="sxs-lookup"><span data-stu-id="550bb-395">The detailed service information is returned in the memory pointed to by *service_ptr.*</span></span> <span data-ttu-id="550bb-396">Si noti che il contenuto nella memoria non è valido dopo la restituzione dalla funzione Notify callback.</span><span class="sxs-lookup"><span data-stu-id="550bb-396">Note that the content in the memory is invalid after returning from the notify callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-397">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-397">Return Values</span></span>

- <span data-ttu-id="550bb-398">**NX_SUCCESS** (0x00) ha installato correttamente la funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="550bb-398">**NX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-399">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-399">Allowed From</span></span>

<span data-ttu-id="550bb-400">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-400">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-401">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-401">Example</span></span>

```C
/* Set the service mask to notify the specified service. */

status = nx_mdns_service_notify_set(&my_mdns, 0x00000002, service_change_notify);

/* If status is NX_SUCCESS, the callback will be called
    if received the service with type “_http”. */
```

## <a name="nx_mdns_service_notify_clear"></a><span data-ttu-id="550bb-402">nx_mdns_service_notify_clear</span><span class="sxs-lookup"><span data-stu-id="550bb-402">nx_mdns_service_notify_clear</span></span>

<span data-ttu-id="550bb-403">Cancellare la funzione di callback notifica modifica servizio</span><span class="sxs-lookup"><span data-stu-id="550bb-403">Clear the service change notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-404">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-404">Prototype</span></span>

```C
UINT nx_mdns_service_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="550bb-405">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-405">Description</span></span>

<span data-ttu-id="550bb-406">Questa API Cancella la funzione di callback notifica di modifica del servizio e.</span><span class="sxs-lookup"><span data-stu-id="550bb-406">This API clears the service change notify callback function and the .</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-407">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-407">Input Parameters</span></span>

- <span data-ttu-id="550bb-408">**mdns_ptr** Puntatore al blocco di controllo MDN..</span><span class="sxs-lookup"><span data-stu-id="550bb-408">**mdns_ptr** Pointer to mDNS control block..</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-409">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-409">Return Values</span></span>

- <span data-ttu-id="550bb-410">**NX_SUCCESS** (0x00) ha cancellato correttamente la funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="550bb-410">**NX_SUCCESS** (0x00) Successfully cleared the callback function.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-411">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-411">Allowed From</span></span>

<span data-ttu-id="550bb-412">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-412">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-413">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-413">Example</span></span>

```C
/* Clear the service notify. */

status = nx_mdns_service_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, the service notify function clear. */
```

## <a name="nx_mdns_host_address_get"></a><span data-ttu-id="550bb-414">nx_mdns_host_address_get</span><span class="sxs-lookup"><span data-stu-id="550bb-414">nx_mdns_host_address_get</span></span>

<span data-ttu-id="550bb-415">Ottenere l'indirizzo host</span><span class="sxs-lookup"><span data-stu-id="550bb-415">Get the host address</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-416">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-416">Prototype</span></span>

```C
UINT nx_mdns_host_address_get(NX_MDNS *mdns_ptr,
    UCHAR *host_name, ULONG *ipv4_address,
    ULONG *ipv6_address, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="550bb-417">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-417">Description</span></span>

<span data-ttu-id="550bb-418">Questo servizio esegue una query MDN sugli indirizzi IPv4 e IPv6 host.</span><span class="sxs-lookup"><span data-stu-id="550bb-418">This service performs a mDNS query on host IPv4 and IPv6 addresses.</span></span> <span data-ttu-id="550bb-419">Se l'indirizzo del nome host specificato si trova nella cache del servizio peer, viene restituito l'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="550bb-419">If the address of specified host name is found in peer service cache, the address is returned.</span></span> <span data-ttu-id="550bb-420">Se non viene trovato alcun indirizzo nella cache dei servizi peer, il modulo MDN rilascia una query di tipo e AAAA e attende la risposta.</span><span class="sxs-lookup"><span data-stu-id="550bb-420">If no address is found in the peer service cache, the mDNS module issues A and AAAA type queries and wait for response.</span></span> <span data-ttu-id="550bb-421">Questa API si blocca fino a quando non viene ricevuta una risposta o si verifica il timeout della query.</span><span class="sxs-lookup"><span data-stu-id="550bb-421">This API blocks until either an answer is received or the query times out.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-422">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-422">Input Parameters</span></span>

- <span data-ttu-id="550bb-423">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-423">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="550bb-424">**HOST_NAME** Puntatore al nome host.</span><span class="sxs-lookup"><span data-stu-id="550bb-424">**host_name** Pointer to host name.</span></span>
- <span data-ttu-id="550bb-425">**Ipv4_address** Puntatore a un indirizzo allineato a 4 byte per lo spazio di archiviazione degli indirizzi IPv4.</span><span class="sxs-lookup"><span data-stu-id="550bb-425">**ipv4_address** Pointer to a 4-byte aligned address for IPv4 address storage space.</span></span> <span data-ttu-id="550bb-426">L'utente deve allocare 4 byte di spazio per l'indirizzo IPv4.</span><span class="sxs-lookup"><span data-stu-id="550bb-426">User shall allocate 4 bytes of space for the IPv4 - address.</span></span> <span data-ttu-id="550bb-427">NX_NULL indirizzo può essere passato all'API se non è necessario che l'applicazione recuperi l'indirizzo IPv4.</span><span class="sxs-lookup"><span data-stu-id="550bb-427">NX_NULL address can be passed into this API if application does not need to retrieve IPv4 address.</span></span>
- <span data-ttu-id="550bb-428">**Ipv6_address** Puntatore all'indirizzo allineato a 4 byte per lo spazio di archiviazione degli indirizzi IPv6.</span><span class="sxs-lookup"><span data-stu-id="550bb-428">**ipv6_address** Pointer to the 4-byte aligned address for IPv6 address storage space.</span></span> <span data-ttu-id="550bb-429">L'utente deve allocare 16 byte di spazio per l'indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="550bb-429">User shall allocate 16 bytes of space for the - IPv6 address.</span></span> <span data-ttu-id="550bb-430">NX_NULL indirizzo può essere passato all'API se non è necessario che l'applicazione recuperi l'indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="550bb-430">NX_NULL address can be passed into this API if application does not need to retrieve IPv6 address.</span></span>
- <span data-ttu-id="550bb-431">**WAIT_OPTION** Quantità di tempo, espressa in cicli, per l'attesa di una risposta.</span><span class="sxs-lookup"><span data-stu-id="550bb-431">**wait_option** The amount of time, in ticks, to wait for a response.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-432">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-432">Return Values</span></span>

- <span data-ttu-id="550bb-433">**NX_SUCCESS** (0x00) ha ottenuto correttamente l'indirizzo host.</span><span class="sxs-lookup"><span data-stu-id="550bb-433">**NX_SUCCESS** (0x00) Successfully obtained host address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-434">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-434">Allowed From</span></span>

<span data-ttu-id="550bb-435">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-435">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-436">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-436">Example</span></span>

```C
ULONG ipv4_address;
ULONG ipv6_address[4];

/* Get the IP address of specified host. */
status = nx_mdns_host_address_get(&my_mdns, “MDNS-Host”, &ipv4_address, ipv6_address, 500);

/* If status is NX_SUCCESS, the IP address of specified host was retrieved. */
```

## <a name="nx_mdns_local_cache_clear"></a><span data-ttu-id="550bb-437">nx_mdns_local_cache_clear</span><span class="sxs-lookup"><span data-stu-id="550bb-437">nx_mdns_local_cache_clear</span></span>

<span data-ttu-id="550bb-438">Cancella tutti i servizi locali</span><span class="sxs-lookup"><span data-stu-id="550bb-438">Erase all local services</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-439">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-439">Prototype</span></span>

```C
UINT nx_mdns_local_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="550bb-440">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-440">Description</span></span>

<span data-ttu-id="550bb-441">Questo servizio Cancella tutte le voci nella cache del servizio locale dopo aver inviato il messaggio di addio.</span><span class="sxs-lookup"><span data-stu-id="550bb-441">This service clears all entries in the local service cache after send the Goodbye message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-442">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-442">Input Parameters</span></span>

- <span data-ttu-id="550bb-443">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-443">**mdns_ptr** Pointer to mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-444">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-444">Return Values</span></span>

- <span data-ttu-id="550bb-445">**NX_SUCCESS** (0x00) ha cancellato correttamente tutte le voci nella cache.</span><span class="sxs-lookup"><span data-stu-id="550bb-445">**NX_SUCCESS** (0x00) Successfully erased all entries in the cache.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-446">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-446">Allowed From</span></span>

<span data-ttu-id="550bb-447">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-447">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-448">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-448">Example</span></span>

```C
/* Clear the local cache, delete all local service. */

status = nx_mdns_local_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of local cache were deleted. */
```

## <a name="nx_mdns_peer_cache_clear"></a><span data-ttu-id="550bb-449">nx_mdns_peer_cache_clear</span><span class="sxs-lookup"><span data-stu-id="550bb-449">nx_mdns_peer_cache_clear</span></span>

<span data-ttu-id="550bb-450">Cancella tutti i servizi individuati</span><span class="sxs-lookup"><span data-stu-id="550bb-450">Erase all the discovered services</span></span>

### <a name="prototype"></a><span data-ttu-id="550bb-451">Prototipo</span><span class="sxs-lookup"><span data-stu-id="550bb-451">Prototype</span></span>

```C
UINT nx_mdns_peer_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="550bb-452">Descrizione</span><span class="sxs-lookup"><span data-stu-id="550bb-452">Description</span></span>

<span data-ttu-id="550bb-453">Questo servizio Cancella tutte le voci della cache dei servizi peer.</span><span class="sxs-lookup"><span data-stu-id="550bb-453">This service clears all entries in the peer service cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="550bb-454">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="550bb-454">Input Parameters</span></span>

- <span data-ttu-id="550bb-455">**mdns_ptr** Puntatore al blocco di controllo MDN.</span><span class="sxs-lookup"><span data-stu-id="550bb-455">**mdns_ptr** Pointer to mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="550bb-456">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="550bb-456">Return Values</span></span>

- <span data-ttu-id="550bb-457">**NX_SUCCESS** (0x00) ha cancellato correttamente tutte le voci nella cache.</span><span class="sxs-lookup"><span data-stu-id="550bb-457">**NX_SUCCESS** (0x00) Successfully erased all entries in the cache.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="550bb-458">Consentito da</span><span class="sxs-lookup"><span data-stu-id="550bb-458">Allowed From</span></span>

<span data-ttu-id="550bb-459">Thread</span><span class="sxs-lookup"><span data-stu-id="550bb-459">Threads</span></span>

### <a name="example"></a><span data-ttu-id="550bb-460">Esempio</span><span class="sxs-lookup"><span data-stu-id="550bb-460">Example</span></span>

```C
/* Clear the peer cache, delete all peer service. */

status = nx_mdns_peer_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of peer cache were deleted. */
```
