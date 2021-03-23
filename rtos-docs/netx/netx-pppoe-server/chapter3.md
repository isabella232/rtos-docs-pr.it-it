---
title: Capitolo 3-Descrizione dei servizi server PPPoE di Azure RTO NetX
description: Questo capitolo contiene una descrizione di tutti i servizi del server PPPoE di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d1137fae4dfea428d50e2defed94de6a838b01c6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822505"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-server-services"></a><span data-ttu-id="2a7e5-103">Capitolo 3-Descrizione dei servizi server PPPoE di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="2a7e5-103">Chapter 3 - Description of Azure RTOS NetX PPPoE Server Services</span></span>

<span data-ttu-id="2a7e5-104">Questo capitolo contiene una descrizione di tutti i servizi del server PPPoE di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-104">This chapter contains a description of all Azure RTOS NetX PPPoE Server services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="2a7e5-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="2a7e5-106">**nx_pppoe_server_create**: *creare un'istanza del server PPPoE*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-106">**nx_pppoe_server_create**: *Create a PPPoE Server instance*</span></span>

- <span data-ttu-id="2a7e5-107">**nx_pppoe_server_ac_name_set**: *impostare il nome del concentratore di accesso*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-107">**nx_pppoe_server_ac_name_set**: *Set Access Concentrator name*</span></span>

- <span data-ttu-id="2a7e5-108">**nx_pppoe_server_delete**: *eliminare un'istanza del server PPPoE*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-108">**nx_pppoe_server_delete**: *Delete a PPPoE Server instance*</span></span>

- <span data-ttu-id="2a7e5-109">**nx_pppoe_server_enable**: *Abilita servizi server PPPoE*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-109">**nx_pppoe_server_enable**: *Enable PPPoE Server services*</span></span>

- <span data-ttu-id="2a7e5-110">**nx_pppoe_server_disable**: *disabilitare i servizi server PPPoE*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-110">**nx_pppoe_server_disable**: *Disable PPPoE Server services*</span></span>

- <span data-ttu-id="2a7e5-111">**nx_pppoe_server_callback_notify_set**: *set pppoe server callback Notify Functions*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-111">**nx_pppoe_server_callback_notify_set**: *Set PPPoE Server callback notify functions*</span></span>

- <span data-ttu-id="2a7e5-112">**nx_pppoe_server_service_name_set**: *impostare il nome del servizio server PPPoE*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-112">**nx_pppoe_server_service_name_set**: *Set PPPoE Server service name*</span></span>

- <span data-ttu-id="2a7e5-113">**nx_pppoe_server_session_send**: *inviare i dati del server PPPoE alla sessione specificata*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-113">**nx_pppoe_server_session_send**: *Send PPPoE Server data to specified session*</span></span>

- <span data-ttu-id="2a7e5-114">**nx_pppoe_server_session_packet_send**: *inviare il pacchetto del server PPPoE alla sessione specificata*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-114">**nx_pppoe_server_session_packet_send**: *Send PPPoE Server packet to specified session*</span></span>

- <span data-ttu-id="2a7e5-115">**nx_pppoe_server_session_terminate**: *termina la sessione PPPoE specificata*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-115">**nx_pppoe_server_session_terminate**: *Terminate the specified PPPoE session*</span></span>

- <span data-ttu-id="2a7e5-116">**nx_pppoe_server_session_get**: *ottenere le informazioni di sessione specificate*</span><span class="sxs-lookup"><span data-stu-id="2a7e5-116">**nx_pppoe_server_session_get**: *Get the specified session information*</span></span>

## <a name="nx_pppoe_server_create"></a><span data-ttu-id="2a7e5-117">nx_pppoe_server_create</span><span class="sxs-lookup"><span data-stu-id="2a7e5-117">nx_pppoe_server_create</span></span>

<span data-ttu-id="2a7e5-118">Creare un'istanza del server PPPoE</span><span class="sxs-lookup"><span data-stu-id="2a7e5-118">Create a PPPoE Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-119">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-119">Prototype</span></span>

```c
UINT nx_pppoe_server_create(NX_PPPOE_SERVER *pppoe_server_ptr,
                            CHAR *name, NX_IP *ip_ptr,
                            UINT interface_index,
                            VOID (*pppoe_link_driver)
                            (struct NX_IP_DRIVER_STRUCT *)
                            NX_PACKET_POOL *pool_ptr,
                            VOID *stack_ptr, ULONG stack_size,
                            UINT priority);
```

### <a name="description"></a><span data-ttu-id="2a7e5-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-120">Description</span></span>

<span data-ttu-id="2a7e5-121">Questo servizio crea un'istanza del server PPPoE con il driver di collegamento fornito dall'utente per l'istanza IP NetX specificata.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-121">This service creates a PPPoE Server instance with the user supplied link driver for the specified NetX IP instance.</span></span> <span data-ttu-id="2a7e5-122">Se il driver di collegamento non è stato inizializzato e abilitato, il software PPPoE Sever è responsabile dell'inizializzazione del driver di collegamento.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-122">If link driver has not been initialized, and enabled, PPPoE sever software is responsible initializing the link driver.</span></span>

<span data-ttu-id="2a7e5-123">Inoltre, l'applicazione deve fornire un pool di pacchetti creato in precedenza per l'istanza del server PPPoE da usare per l'allocazione dei pacchetti interna.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-123">In addition, the application must supply a previously created packet pool for the PPPoE Server instance to use for internal packet allocation.</span></span>

<span data-ttu-id="2a7e5-124">Si noti che in genere è consigliabile creare il thread IP NetX con una priorità più alta rispetto alla priorità del thread del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-124">Note that it is generally a good idea to create the NetX IP thread at a higher priority than the PPPoE Server thread priority.</span></span> <span data-ttu-id="2a7e5-125">Per ulteriori informazioni su come specificare la priorità del thread IP, fare riferimento al servizio *nx_ip_create* .</span><span class="sxs-lookup"><span data-stu-id="2a7e5-125">Please refer to the *nx_ip_create* service for more information on specifying the IP thread priority.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-126">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-126">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-127">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-127">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="2a7e5-128">**nome**: nome dell'istanza del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-128">**name**: Name of this PPPoE Server instance.</span></span>
- <span data-ttu-id="2a7e5-129">**ip_ptr**: puntatore al blocco di controllo per l'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-129">**ip_ptr**: Pointer to control block for IP instance.</span></span>
- <span data-ttu-id="2a7e5-130">**interface_index**: Indice dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-130">**interface_index**: Interface index.</span></span>
- <span data-ttu-id="2a7e5-131">**pppoe_link_driver**: driver di collegamento fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-131">**pppoe_link_driver**: User supplied link driver.</span></span>
- <span data-ttu-id="2a7e5-132">**pool_ptr**: puntatore al pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-132">**pool_ptr**: Pointer to packet pool.</span></span>
- <span data-ttu-id="2a7e5-133">**stack_ptr**: puntatore all'inizio dell'area dello stack del thread del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-133">**stack_ptr**: Pointer to start of PPPoE Server thread's stack area.</span></span>
- <span data-ttu-id="2a7e5-134">**stack_size**: dimensioni in byte nello stack del thread.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-134">**stack_size**: Size in bytes in the thread's stack.</span></span>
- <span data-ttu-id="2a7e5-135">**priorità**: priorità dei thread del server PPPoE interni (1-31).</span><span class="sxs-lookup"><span data-stu-id="2a7e5-135">**priority**: Priority of internal PPPoE Server threads (1-31).</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-136">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-136">Return Values</span></span>

- <span data-ttu-id="2a7e5-137">**NX_PPPOE_SERVER_SUCCESS**: (0x00) la creazione del server PPPoE è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-137">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server create.</span></span>
- <span data-ttu-id="2a7e5-138">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) server PPPoE, IP, pool di pacchetti o puntatore dello stack non validi.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-138">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server, IP, packet pool, or stack pointer.</span></span>
- <span data-ttu-id="2a7e5-139">NX_PPPOE_SERVER_INVALID_INTERFACE: (0xC2) interfaccia non valida.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-139">NX_PPPOE_SERVER_INVALID_INTERFACE: (0xC2) Invalid interface.</span></span>
- <span data-ttu-id="2a7e5-140">NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) dimensioni del payload non valide per il pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-140">NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) Invalid payload size of packet pool.</span></span>
- <span data-ttu-id="2a7e5-141">NX_PPPOE_SERVER_MEMORY_SIZE_ERROR: (0xC4) dimensione della memoria non valida.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-141">NX_PPPOE_SERVER_MEMORY_SIZE_ERROR: (0xC4) Invalid memory size.</span></span>
- <span data-ttu-id="2a7e5-142">NX_PPPOE_SERVER_PRIORITY_ERROR: (0xC5) priorità non valida del thread del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-142">NX_PPPOE_SERVER_PRIORITY_ERROR: (0xC5) Invalid priority of PPPoE Server thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-143">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-143">Allowed From</span></span>

<span data-ttu-id="2a7e5-144">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-144">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-145">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-145">Example</span></span>

```c
/* Create "my_pppoe_server" for IP instance "my_ip". */
status = nx_pppoe_server_create(&my_pppoe_server, "my PPPoE Server", &my_ip,
                                &my_pool, stack_start, 1024, 2);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully created. */
```

## <a name="nx_pppoe_server_delete"></a><span data-ttu-id="2a7e5-146">nx_pppoe_server_delete</span><span class="sxs-lookup"><span data-stu-id="2a7e5-146">nx_pppoe_server_delete</span></span>

<span data-ttu-id="2a7e5-147">Eliminare un'istanza del server PPPoE</span><span class="sxs-lookup"><span data-stu-id="2a7e5-147">Delete a PPPoE Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-148">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-148">Prototype</span></span>

```c
UINT nx_pppoe_server_delete(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a><span data-ttu-id="2a7e5-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-149">Description</span></span>

<span data-ttu-id="2a7e5-150">Questo servizio Elimina l'istanza del server PPPoE creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-150">This service deletes the previously created PPPoE Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-151">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-151">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-152">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-152">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-153">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-153">Return Values</span></span>

- <span data-ttu-id="2a7e5-154">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-154">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-155">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-155">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-156">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-156">Allowed From</span></span>

<span data-ttu-id="2a7e5-157">Thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-157">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-158">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-158">Example</span></span>

```c
/* Delete PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_delete(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully deleted. */
```

## <a name="nx_pppoe_server_enable"></a><span data-ttu-id="2a7e5-159">nx_pppoe_server_enable</span><span class="sxs-lookup"><span data-stu-id="2a7e5-159">nx_pppoe_server_enable</span></span>

<span data-ttu-id="2a7e5-160">Abilita servizio server PPPoE</span><span class="sxs-lookup"><span data-stu-id="2a7e5-160">Enable PPPoE Server service</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-161">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-161">Prototype</span></span>

```c
UINT nx_pppoe_server_enable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a><span data-ttu-id="2a7e5-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-162">Description</span></span>

<span data-ttu-id="2a7e5-163">Questo servizio Abilita i servizi del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-163">This service enables the PPPoE Server services.</span></span>

> [!NOTE]
> <span data-ttu-id="2a7e5-164">Questa funzione deve essere chiamata dopo *nx_pppoe_server_create* e *nx_pppoe_server_callback_notify_set*.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-164">This function must be called after *nx_pppoe_server_create* and *nx_pppoe_server_callback_notify_set*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-165">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-165">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-166">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-166">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-167">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-167">Return Values</span></span>

- <span data-ttu-id="2a7e5-168">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-168">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-169">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-169">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-170">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-170">Allowed From</span></span>

<span data-ttu-id="2a7e5-171">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-171">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-172">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-172">Example</span></span>

```c
/* Enable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_enable(&my_pppoe_server);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has enabled. */
```

## <a name="nx_pppoe_server_disable"></a><span data-ttu-id="2a7e5-173">nx_pppoe_server_disable</span><span class="sxs-lookup"><span data-stu-id="2a7e5-173">nx_pppoe_server_disable</span></span>

<span data-ttu-id="2a7e5-174">Disabilitare il servizio server PPPoE</span><span class="sxs-lookup"><span data-stu-id="2a7e5-174">Disable PPPoE Server service</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-175">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-175">Prototype</span></span>

```c
UINT nx_pppoe_server_disable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a><span data-ttu-id="2a7e5-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-176">Description</span></span>

<span data-ttu-id="2a7e5-177">Questo servizio Disabilita i servizi del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-177">This service disables the PPPoE Server services.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-178">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-178">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-179">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-179">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-180">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-180">Return Values</span></span>

- <span data-ttu-id="2a7e5-181">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-181">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-182">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-182">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-183">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-183">Allowed From</span></span>

<span data-ttu-id="2a7e5-184">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-184">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-185">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-185">Example</span></span>

```c
/* Disable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_disable(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has disabled. */
```

## <a name="nx_pppoe_server_callback_notify_set"></a><span data-ttu-id="2a7e5-186">nx_pppoe_server_callback_notify_set</span><span class="sxs-lookup"><span data-stu-id="2a7e5-186">nx_pppoe_server_callback_notify_set</span></span>

<span data-ttu-id="2a7e5-187">Imposta funzioni di notifica di callback del server PPPoE</span><span class="sxs-lookup"><span data-stu-id="2a7e5-187">Set PPPoE Server callback notify functions</span></span> 

### <a name="prototype"></a><span data-ttu-id="2a7e5-188">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-188">Prototype</span></span>

```c
UINT nx_pppoe_server_callback_notify_set(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        VOID (* pppoe_discover_initiation_notify)(UINT session_index,
                ULONG length, UCHAR *data),
        VOID (* pppoe_discover_request_notify)(UINT session_index),
        VOID (* pppoe_discover_terminate_notify)(UINT session_index),
        VOID (* pppoe_discover_terminate_confirm)(UINT session_index),
        VOID (* pppoe_data_receive_notify)(UINT session_index,
                ULONG length, UCHAR *data, UINT packet_id),
        VOID (* pppoe_discover_notify)(UINT session_index, UCHAR *data))
```

### <a name="description"></a><span data-ttu-id="2a7e5-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-189">Description</span></span>

<span data-ttu-id="2a7e5-190">Questo servizio imposta le funzioni di notifica del callback del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-190">This service sets PPPoE Server callback notify functions.</span></span>

> [!NOTE]
> <span data-ttu-id="2a7e5-191">Questa funzione deve essere chiamata prima di *nx_pppoe_server_enabl e* deve essere impostato il puntatore alla funzione pppoe_data_receive_notify, in caso contrario *nx_pppoe_server_enable* sarà un errore.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-191">This function must be called before *nx_pppoe_server_enabl, and* the pppoe_data_receive_notify function pointer must be set, if not, *nx_pppoe_server_enable* will be failure.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-192">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-192">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-193">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-193">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="2a7e5-194">**pppoe_discover_initiation_notify**: funzione dell'applicazione chiamata ogni volta che viene ricevuto il messaggio di avvio dell'individuazione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-194">**pppoe_discover_initiation_notify**: Application function that is called whenever PPPoE discover initiation message is received.</span></span> <span data-ttu-id="2a7e5-195">Se questo valore è NULL, l'individuazione della funzione di callback di avvio è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-195">If this value is NULL, discover initiation callback function is disabled.</span></span>
- <span data-ttu-id="2a7e5-196">**pppoe_discover_request_notify**: funzione dell'applicazione chiamata ogni volta che viene ricevuto un messaggio di richiesta di individuazione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-196">**pppoe_discover_request_notify**: Application function that is called whenever PPPoE discover request message is received.</span></span> <span data-ttu-id="2a7e5-197">Se questo valore è NULL, la funzione di callback Discover request è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-197">If this value is NULL, discover request callback function is disabled.</span></span>
- <span data-ttu-id="2a7e5-198">**pppoe_discover_terminate_notify**: funzione dell'applicazione chiamata ogni volta che viene ricevuto il messaggio PPPoE Discover terminate.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-198">**pppoe_discover_terminate_notify**: Application function that is called whenever PPPoE discover terminate message is received.</span></span> <span data-ttu-id="2a7e5-199">Se questo valore è NULL, la funzione di callback Discover terminate è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-199">If this value is NULL, discover terminate callback function is disabled.</span></span>
- <span data-ttu-id="2a7e5-200">**pppoe_discover_terminate_confirm**: funzione dell'applicazione che viene chiamata ogni volta che viene inviato il messaggio di individuazione della terminazione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-200">**pppoe_discover_terminate_confirm**: Application function that is called whenever PPPoE discover terminate message is sent.</span></span> <span data-ttu-id="2a7e5-201">Se questo valore è NULL, la funzione di callback Discover terminate è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-201">If this value is NULL, discover terminate callback function is disabled.</span></span>
- <span data-ttu-id="2a7e5-202">**pppoe_data_receive_notify**: funzione dell'applicazione chiamata ogni volta che viene ricevuto un messaggio di dati PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-202">**pppoe_data_receive_notify**: Application function that is called whenever PPPoE data message is received.</span></span> <span data-ttu-id="2a7e5-203">Il valore non deve essere zero.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-203">This value must not be zero.</span></span>
- <span data-ttu-id="2a7e5-204">**pppoe_data_send_notify**: funzione dell'applicazione chiamata ogni volta che viene inviato un messaggio di dati PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-204">**pppoe_data_send_notify**: Application function that is called whenever PPPoE data message is sent.</span></span> <span data-ttu-id="2a7e5-205">Se questo valore è NULL, la funzione di callback di invio dati è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-205">If this value is NULL, data send callback function is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-206">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-206">Return Values</span></span>

- <span data-ttu-id="2a7e5-207">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-207">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-208">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore a funzione o puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-208">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer or function pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-209">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-209">Allowed From</span></span>

<span data-ttu-id="2a7e5-210">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-210">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-211">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-211">Example</span></span>

```c
/* Set PPPoE Server callback notify functions, PPPoE Server instance "my_pppoe_server". */

status = nx_pppoe_server_disable(&my_pppoe_server,
                pppoe_discovery_initiation_notify,
                pppoe_discovery_request_notify,
                pppoe_discovery_terminate_notify,
                pppoe_discovery_terminate_confirm,
                pppoe_data_receive_notify,
                pppoe_data_send_notify);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the callback notify functions for "my_pppoe_server" service has set. */
```

## <a name="nx_pppoe_server_ac_name_set"></a><span data-ttu-id="2a7e5-212">nx_pppoe_server_ac_name_set</span><span class="sxs-lookup"><span data-stu-id="2a7e5-212">nx_pppoe_server_ac_name_set</span></span>

<span data-ttu-id="2a7e5-213">Imposta nome concentratore accesso</span><span class="sxs-lookup"><span data-stu-id="2a7e5-213">Set Access Concentrator name</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-214">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-214">Prototype</span></span>

```c
UINT nx_pppoe_server_ac_name_set(
    NX_PPPOE_SERVER *pppoe_server_ptr,
    CHAR *ac_name, UINT ac_name_length,
);
```

### <a name="description"></a><span data-ttu-id="2a7e5-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-215">Description</span></span>

<span data-ttu-id="2a7e5-216">Questo set di funzioni chiama il nome di funzione del concentratore di accesso.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-216">This function set Access Concentrator name function call.</span></span>

> [!NOTE]
> <span data-ttu-id="2a7e5-217">La stringa di ac_name deve essere con terminazione NULL e la lunghezza di ac_name corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-217">The string of ac_name must be NULL-terminated and length of ac_name matches the length specified in the argument list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-218">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-218">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-219">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-219">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="2a7e5-220">**ac_name**: nome del concentratore di accesso.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-220">**ac_name**: Access Concentrator name.</span></span>
- <span data-ttu-id="2a7e5-221">**ac_name_length**: lunghezza del ac_ame.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-221">**ac_name_length**: Length of ac_ame.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-222">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-222">Return Values</span></span>

- <span data-ttu-id="2a7e5-223">**NX_PPPOE_SERVER_SUCCESS**: (0x00) il set di server PPPoE è riuscito.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-223">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server set.</span></span>
- <span data-ttu-id="2a7e5-224">**NX_PPPOE_SERVER_PTR_ERROR**: (0XC1) server PPPoE, IP, pool di pacchetti o puntatore dello stack non validi.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-224">**NX_PPPOE_SERVER_PTR_ERROR**: (0xC1) Invalid PPPoE Server, IP, packet pool, or stack pointer.</span></span>
- <span data-ttu-id="2a7e5-225">**NX_SIZE_ERROR**: il controllo (0x09) name_length esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-225">**NX_SIZE_ERROR**: (0x09) Check name_length fail.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-226">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-226">Allowed From</span></span>

<span data-ttu-id="2a7e5-227">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-227">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-228">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-228">Example</span></span>

```c
/* Set "my PPPoE ac name" for Server instance "my_pppoe_server". */
status = nx_pppoe_server_ac_name_set(&my_pppoe_server, "my PPPoE ac name",16);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my PPPoE ac name" was successfully set. */
```

## <a name="nx_pppoe_server_service_name_set"></a><span data-ttu-id="2a7e5-229">nx_pppoe_server_service_name_set</span><span class="sxs-lookup"><span data-stu-id="2a7e5-229">nx_pppoe_server_service_name_set</span></span>

<span data-ttu-id="2a7e5-230">Imposta il nome del servizio server PPPoE</span><span class="sxs-lookup"><span data-stu-id="2a7e5-230">Set PPPoE Server service name</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-231">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-231">Prototype</span></span>

```c
UINT nx_pppoe_server_service_name_set(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UCHAR **service_name, UINT service_name_count);
```

### <a name="description"></a><span data-ttu-id="2a7e5-232">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-232">Description</span></span>

<span data-ttu-id="2a7e5-233">Questo servizio imposta il nome del servizio server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-233">This service sets PPPoE Server service name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-234">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-234">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-235">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-235">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-236">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-236">Return Values</span></span>

- <span data-ttu-id="2a7e5-237">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-237">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-238">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-238">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-239">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-239">Allowed From</span></span>

<span data-ttu-id="2a7e5-240">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-240">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-241">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-241">Example</span></span>

```c
CHAR *nx_pppoe_service_name[] =
{
    "XBB",
    "PRINTER",
    NX_NULL
};

/* Set service name for PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_service_namet_set(&my_pppoe_server,
                                    nx_pppoe_service_name, 2);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service name has set. */
```

## <a name="nx_pppoe_server_session_send"></a><span data-ttu-id="2a7e5-242">nx_pppoe_server_session_send</span><span class="sxs-lookup"><span data-stu-id="2a7e5-242">nx_pppoe_server_session_send</span></span>

<span data-ttu-id="2a7e5-243">Invia dati server PPPoE alla sessione specificata</span><span class="sxs-lookup"><span data-stu-id="2a7e5-243">Send PPPoE Server data to specified session</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-244">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-244">Prototype</span></span>

```c
UINT nx_pppoe_server_session_send (NX_PPPOE_SERVER *pppoe_server_ptr,
                UINT session_index, UCHAR *data_ptr, UINT data_length);
```

### <a name="description"></a><span data-ttu-id="2a7e5-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-245">Description</span></span>

<span data-ttu-id="2a7e5-246">Questo servizio invia il frame PPPoE usando l'ID sessione specificato.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-246">This service sends PPPoE frame using specified session ID.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-247">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-247">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-248">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-248">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="2a7e5-249">**session_index**: indice della sessione.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-249">**session_index**: The index of session.</span></span>
- <span data-ttu-id="2a7e5-250">**DATA_PTR**: puntatore all'avvio del frame di dati del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-250">**data_ptr**: Pointer to start of PPPoE Server data frame.</span></span>
- <span data-ttu-id="2a7e5-251">**Data_length**: lunghezza del frame di dati del server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-251">**data_length**: Length of PPPoE Server data frame.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-252">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-252">Return Values</span></span>

- <span data-ttu-id="2a7e5-253">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-253">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-254">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-254">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>
- <span data-ttu-id="2a7e5-255">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) il servizio server PPPoE non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-255">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE Server service is not enabled.</span></span>
- <span data-ttu-id="2a7e5-256">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) indice della sessione PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-256">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Invalid PPPoE session index.</span></span>
- <span data-ttu-id="2a7e5-257">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) la sessione PPPoE non è stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-257">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-258">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-258">Allowed From</span></span>

<span data-ttu-id="2a7e5-259">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-259">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-260">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-260">Example</span></span>

```c
/* Send PPPoE Server data to specified session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_send(&my_pppoe_server, 0, my_data_ptr, 1400);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" data has sent. */
```

## <a name="nx_pppoe_server_session_packet_send"></a><span data-ttu-id="2a7e5-261">nx_pppoe_server_session_packet_send</span><span class="sxs-lookup"><span data-stu-id="2a7e5-261">nx_pppoe_server_session_packet_send</span></span>

<span data-ttu-id="2a7e5-262">Invia pacchetto server PPPoE alla sessione specificata</span><span class="sxs-lookup"><span data-stu-id="2a7e5-262">Send PPPoE Server packet to specified session</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-263">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-263">Prototype</span></span>

```c
UINT nx_pppoe_server_session_packet_send (
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UINT session_index, NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="2a7e5-264">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-264">Description</span></span>

<span data-ttu-id="2a7e5-265">Questo servizio invia il pacchetto PPPoE usando l'ID sessione specificato.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-265">This service sends PPPoE packet using specified session ID.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-266">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-266">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-267">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-267">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="2a7e5-268">**session_index**: indice della sessione.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-268">**session_index**: The index of session.</span></span>
- <span data-ttu-id="2a7e5-269">**packet_ptr**: puntatore al pacchetto PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-269">**packet_ptr**: Pointer to PPPoE packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-270">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-270">Return Values</span></span>

- <span data-ttu-id="2a7e5-271">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-271">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-272">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-272">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>
- <span data-ttu-id="2a7e5-273">NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) pacchetto server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-273">NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) Invalid PPPoE Server packet.</span></span>
- <span data-ttu-id="2a7e5-274">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) il servizio server PPPoE non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-274">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE Server service is not enabled.</span></span>
- <span data-ttu-id="2a7e5-275">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) indice della sessione PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-275">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Invalid PPPoE session index.</span></span>
- <span data-ttu-id="2a7e5-276">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) la sessione PPPoE non è stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-276">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-277">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-277">Allowed From</span></span>

<span data-ttu-id="2a7e5-278">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-278">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-279">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-279">Example</span></span>

```c
/* Send PPPoE Server data to specified session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_packet_send(&my_pppoe_server, 0, packet_ptr);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" packet has sent. */
```

## <a name="nx_pppoe_server_session_terminate"></a><span data-ttu-id="2a7e5-280">nx_pppoe_server_session_terminate</span><span class="sxs-lookup"><span data-stu-id="2a7e5-280">nx_pppoe_server_session_terminate</span></span>

<span data-ttu-id="2a7e5-281">Termina la sessione PPPoE specificata</span><span class="sxs-lookup"><span data-stu-id="2a7e5-281">Terminate the specified PPPoE session</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-282">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-282">Prototype</span></span>

```c
UINT nx_pppoe_server_session_terminate(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UINT session_index);
```

### <a name="description"></a><span data-ttu-id="2a7e5-283">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-283">Description</span></span>

<span data-ttu-id="2a7e5-284">Questo servizio termina la sessione PPPoE specificata.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-284">This service terminates the specified PPPoE session.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-285">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-285">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-286">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-286">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="2a7e5-287">**session_index**: indice della sessione.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-287">**session_index**: The index of session.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-288">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-288">Return Values</span></span>

- <span data-ttu-id="2a7e5-289">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-289">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-290">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-290">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>
- <span data-ttu-id="2a7e5-291">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) il servizio server PPPoE non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-291">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE Server service is not enabled.</span></span>
- <span data-ttu-id="2a7e5-292">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) indice della sessione PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-292">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Invalid PPPoE session index.</span></span>
- <span data-ttu-id="2a7e5-293">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) la sessione PPPoE non è stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-293">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-294">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-294">Allowed From</span></span>

<span data-ttu-id="2a7e5-295">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-295">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-296">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-296">Example</span></span>

```c
/* Terminates the specified PPPoE session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_send(&my_pppoe_server, 0);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the session indexed with 0 has terminated. */
```

## <a name="nx_pppoe_server_session_get"></a><span data-ttu-id="2a7e5-297">nx_pppoe_server_session_get</span><span class="sxs-lookup"><span data-stu-id="2a7e5-297">nx_pppoe_server_session_get</span></span>

<span data-ttu-id="2a7e5-298">Ottenere le informazioni sulla sessione PPPoE specificate</span><span class="sxs-lookup"><span data-stu-id="2a7e5-298">Get the specified PPPoE session information</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-299">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-299">Prototype</span></span>

```c
UINT nx_pppoe_server_session_get(NX_PPPOE_SERVER *pppoe_server_ptr,
                                UINT session_index
                                ULONG *client_mac_msw,
                                ULONG *client_mac_lsw,
                                ULONG *session_id);
```

### <a name="description"></a><span data-ttu-id="2a7e5-300">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-300">Description</span></span>

<span data-ttu-id="2a7e5-301">Questo servizio ottiene le informazioni sulla sessione PPPoE specificate, l'indirizzo fisico e l'ID di sessione del client.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-301">This service gets the specified PPPoE session information, client physical address and session id.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-302">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-302">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-303">**pppoe_server_ptr**: puntatore al blocco di controllo server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-303">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="2a7e5-304">**session_index**: indice della sessione.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-304">**session_index**: The index of session.</span></span>
- <span data-ttu-id="2a7e5-305">**client_mac_msw**: puntatore RSU indirizzo fisico client.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-305">**client_mac_msw**: Client Physical address MSW pointer.</span></span>
- <span data-ttu-id="2a7e5-306">**client_mac_lsw**: puntatore RSU indirizzo fisico client.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-306">**client_mac_lsw**: Client Physical address MSW pointer.</span></span>
- <span data-ttu-id="2a7e5-307">**session_id**: puntatore ID sessione.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-307">**session_id**: Session ID pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-308">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-308">Return Values</span></span>

- <span data-ttu-id="2a7e5-309">**NX_PPPOE_SERVER_SUCCESS**: (0x00) eliminazione del server PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-309">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="2a7e5-310">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) puntatore al server PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-310">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>
- <span data-ttu-id="2a7e5-311">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) indice della sessione PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-311">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Invalid PPPoE session index.</span></span>
- <span data-ttu-id="2a7e5-312">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) la sessione PPPoE non è stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-312">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-313">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-313">Allowed From</span></span>

<span data-ttu-id="2a7e5-314">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-314">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-315">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-315">Example</span></span>

```c
/* Gets the specified PPPoE session information, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_get (&my_pppoe_server, 0, &client_mac_msw, &client_mac_lsw, &session_id);

/* If status is NX_PPPOE_SERVER_SUCCESS, the client physical address and session id of the session indexed with 0 has got. */
```

## <a name="pppinitind"></a><span data-ttu-id="2a7e5-316">PppInitInd</span><span class="sxs-lookup"><span data-stu-id="2a7e5-316">PppInitInd</span></span>

<span data-ttu-id="2a7e5-317">Configurare il nome del servizio predefinito</span><span class="sxs-lookup"><span data-stu-id="2a7e5-317">Configure the default Service Name</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-318">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-318">Prototype</span></span>

```c
VOID PppInitnd(UINT length, UCHAR *aData);
```

### <a name="description"></a><span data-ttu-id="2a7e5-319">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-319">Description</span></span>

<span data-ttu-id="2a7e5-320">Il software PPPoE esporrà questa funzione per consentire al software di TTP di configurare il "nome del servizio predefinito" che deve essere usato da PPPoE per filtrare le richieste PADI in arrivo.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-320">The PPPoE software will expose this function to allow TTP's software to configure the 'default Service Name' that the PPPoE should use to filter incoming PADI requests.</span></span> <span data-ttu-id="2a7e5-321">Il software PPPoE deve ricordare queste informazioni e, se viene ricevuto un pacchetto PADI contenente un nome di servizio corrispondente, deve chiamare PppDiscoverReq.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-321">The PPPoE software should remember this information, and if a PADI packet is received containing a service name that matches then it should call PppDiscoverReq.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-322">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-322">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-323">**lunghezza**: lunghezza del nome del servizio predefinito.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-323">**length**: Length of default service name.</span></span>
- <span data-ttu-id="2a7e5-324">**ADATA**: nome del servizio predefinito.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-324">**aData**: Default service name.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-325">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-325">Return Values</span></span>

<span data-ttu-id="2a7e5-326">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="2a7e5-326">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-327">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-327">Allowed From</span></span>

<span data-ttu-id="2a7e5-328">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-328">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-329">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-329">Example</span></span>

```c
/* Configure the default Service Name. */
PppInitInd (3, "XBB");
```

## <a name="pppdiscovercnf"></a><span data-ttu-id="2a7e5-330">PppDiscoverCnf</span><span class="sxs-lookup"><span data-stu-id="2a7e5-330">PppDiscoverCnf</span></span>

<span data-ttu-id="2a7e5-331">Definire il campo del nome del servizio del pacchetto PADO</span><span class="sxs-lookup"><span data-stu-id="2a7e5-331">Define the Service Name field of the PADO packet</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-332">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-332">Prototype</span></span>

```c
VOID PppDiscoverCnf (UINT length, UCHAR *aData, UINT interfaceHandle);
```

### <a name="description"></a><span data-ttu-id="2a7e5-333">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-333">Description</span></span>

<span data-ttu-id="2a7e5-334">Il software PPPoE esporrà questa funzione per consentire al software di TTP di definire il campo del nome del servizio del pacchetto PADO.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-334">The PPPoE software will expose this function to allow TTP's software to define the Service Name field of the PADO packet.</span></span> <span data-ttu-id="2a7e5-335">Il software PPPoE non deve inviare il PADO fino a quando non viene chiamato il PppDiscoverCnf.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-335">The PPPoE software should not send the PADO until the PppDiscoverCnf is called.</span></span>

<span data-ttu-id="2a7e5-336">Il pacchetto PADO conterrà un nome del concentratore di accesso (usando l'ID di tag 0x0102 come definito in RFC2516), definito all'inizializzazione del software PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-336">The PADO packet shall contain an access concentrator name (using the tag id 0x0102 as defined in RFC2516), defined on initialisation of the PPPoE software.</span></span>

<span data-ttu-id="2a7e5-337">È possibile passare più nomi di servizio in aData, con ogni nome con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-337">Multiple service names can be passed in aData, with each name to be null terminated.</span></span>

<span data-ttu-id="2a7e5-338">Il carattere null viene usato come separatore per garantire la massima flessibilità nel caso in cui sia necessario passare altri comandi come parte del nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-338">Null character is used as a separator to provide maximum flexibility in case other commands need to be passed in as part of the service name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-339">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-339">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-340">**lunghezza**: lunghezza del nome del servizio predefinito.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-340">**length**: Length of default service name.</span></span>
- <span data-ttu-id="2a7e5-341">**ADATA**: nome del servizio predefinito.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-341">**aData**: Default service name.</span></span>
- <span data-ttu-id="2a7e5-342">**interfaceHandle**: handle di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-342">**interfaceHandle**: Interface handle.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-343">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-343">Return Values</span></span>

<span data-ttu-id="2a7e5-344">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="2a7e5-344">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-345">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-345">Allowed From</span></span>

<span data-ttu-id="2a7e5-346">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-346">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-347">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-347">Example</span></span>

```c
/* Define the Service Name field of the PADO packet. */
PppDiscoverCnf (3, "XBB", 0);
```

## <a name="pppopencnf"></a><span data-ttu-id="2a7e5-348">PppOpenCnf</span><span class="sxs-lookup"><span data-stu-id="2a7e5-348">PppOpenCnf</span></span>

<span data-ttu-id="2a7e5-349">Accettare o rifiutare la sessione PPPoE</span><span class="sxs-lookup"><span data-stu-id="2a7e5-349">Accept or reject the PPPoE session</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-350">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-350">Prototype</span></span>

```c
VOID PppOpenCnf (UCHAR accept, UINT interfaceHandle);
```

### <a name="description"></a><span data-ttu-id="2a7e5-351">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-351">Description</span></span>

<span data-ttu-id="2a7e5-352">Il software PPPoE esporrà questa funzione per consentire al software di TTP di accettare o rifiutare la sessione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-352">The PPPoE software will expose this function to allow TTP's software to accept or reject the PPPoE session.</span></span>  <span data-ttu-id="2a7e5-353">In risposta a questo lo stack PPPoE deve accettare la connessione e assegnare un numero di Session_ID PPPoE univoco associato a interfaceHandle.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-353">In response to this the PPPoE stack should accept the connection and assign a unique PPPoE Session_ID number associated with the interfaceHandle.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-354">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-354">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-355">**Accept**: NX_TRUE se la connessione deve essere accettata.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-355">**accept**: NX_TRUE if the connection is to be accepted.</span></span>
- <span data-ttu-id="2a7e5-356">**interfaceHandle**: handle di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-356">**interfaceHandle**: Interface handle.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-357">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-357">Return Values</span></span>

<span data-ttu-id="2a7e5-358">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="2a7e5-358">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-359">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-359">Allowed From</span></span>

<span data-ttu-id="2a7e5-360">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-360">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-361">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-361">Example</span></span>

```c
/* Accept the connection. */
PppOpenCnf(NX_TRUE, 0);
```

## <a name="pppcloseind"></a><span data-ttu-id="2a7e5-362">PppCloseInd</span><span class="sxs-lookup"><span data-stu-id="2a7e5-362">PppCloseInd</span></span>

<span data-ttu-id="2a7e5-363">Chiudere una sessione PPPoE</span><span class="sxs-lookup"><span data-stu-id="2a7e5-363">Close a PPPoE session</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-364">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-364">Prototype</span></span>

```c
VOID PppCloseInd (UINT interfaceHandle, UCHAR *causeCode);
```

### <a name="description"></a><span data-ttu-id="2a7e5-365">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-365">Description</span></span>

<span data-ttu-id="2a7e5-366">Il software PPPoE esporrà questa funzione per consentire al software di TTP di chiudere una sessione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-366">The PPPoE software will expose this function to allow TTP's software to close a PPPoE session.</span></span>

<span data-ttu-id="2a7e5-367">Il software PPPoE indicherà la stringa di codice della causare nel tag Generic-Error (0x0203) nel messaggio PADT</span><span class="sxs-lookup"><span data-stu-id="2a7e5-367">The PPPoE software will indicate the cause code string in the Generic-Error tag (0x0203) in the PADT message</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-368">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-368">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-369">**interfaceHandle**: handle di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-369">**interfaceHandle**: Interface handle.</span></span>
- <span data-ttu-id="2a7e5-370">**causeCode**: stringa con terminazione null per l'invio di informazioni sul motivo per la chiusura della connessione dal server PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-370">**causeCode**: Null terminated string for sending information about the reason for closing the connection from the PPPoE Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-371">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-371">Return Values</span></span>

<span data-ttu-id="2a7e5-372">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="2a7e5-372">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-373">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-373">Allowed From</span></span>

<span data-ttu-id="2a7e5-374">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-374">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-375">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-375">Example</span></span>

```c
/* Close a PPPoE session. */
PppCloseInd(0, NX_NULL);
```

## <a name="pppclosecnf"></a><span data-ttu-id="2a7e5-376">PppCloseCnf</span><span class="sxs-lookup"><span data-stu-id="2a7e5-376">PppCloseCnf</span></span>

<span data-ttu-id="2a7e5-377">Verificare che l'handle sia stato liberato</span><span class="sxs-lookup"><span data-stu-id="2a7e5-377">Confirm that the handle has been freed</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-378">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-378">Prototype</span></span>

```c
VOID PppCloseCnf (UINT interfaceHandle);
```

### <a name="description"></a><span data-ttu-id="2a7e5-379">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-379">Description</span></span>

<span data-ttu-id="2a7e5-380">Il software PPPoE esporrà questa funzione per consentire al software di TTP di confermare che l'handle è stato liberato.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-380">The PPPoE software will expose this function to allow TTP's software to confirm that the handle has been freed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-381">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-381">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-382">**interfaceHandle**: handle di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-382">**interfaceHandle**: Interface handle.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-383">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-383">Return Values</span></span>

<span data-ttu-id="2a7e5-384">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="2a7e5-384">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-385">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-385">Allowed From</span></span>

<span data-ttu-id="2a7e5-386">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-386">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-387">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-387">Example</span></span>

```c
/* Confirm that the handle has been freed. */
PppCloseCnf(0);
```

## <a name="ppptransmitdatacnf"></a><span data-ttu-id="2a7e5-388">PppTransmitDataCnf</span><span class="sxs-lookup"><span data-stu-id="2a7e5-388">PppTransmitDataCnf</span></span>

<span data-ttu-id="2a7e5-389">Consenti la conferma di un dato PPP precedente</span><span class="sxs-lookup"><span data-stu-id="2a7e5-389">Allow a preceding PPP data to be acknowledged</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-390">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-390">Prototype</span></span>

```c
VOID PppTransmitDataCnf (UINT interfaceHandle, UCHAR *aData,
                        UINT packet_id);
```

### <a name="description"></a><span data-ttu-id="2a7e5-391">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-391">Description</span></span>

<span data-ttu-id="2a7e5-392">Il software PPPoE esporrà questa funzione per consentire la conferma di un PppTransmitDataReq precedente.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-392">The PPPoE software will expose this function to allow a preceding PppTransmitDataReq to be acknowledged.</span></span>  <span data-ttu-id="2a7e5-393">Questo implica che il software di TTP è pronto per un nuovo frame PPP da PPPoE.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-393">It implies that TTP's software is ready for a new PPP frame from PPPoE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-394">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-394">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-395">**interfaceHandle**: handle di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-395">**interfaceHandle**: Interface handle.</span></span>
- <span data-ttu-id="2a7e5-396">**ADATA**: puntatore al buffer dei dati PPP che è stato accettato.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-396">**aData**: Pointer the PPP data buffer that has been accepted.</span></span>
- <span data-ttu-id="2a7e5-397">**Packet_id**: identificatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-397">**Packet_id**: Packet identifier.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-398">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-398">Return Values</span></span>

<span data-ttu-id="2a7e5-399">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="2a7e5-399">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-400">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-400">Allowed From</span></span>

<span data-ttu-id="2a7e5-401">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-401">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-402">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-402">Example</span></span>

```c
UINT packet_id = 0x20015429

/* Allow a preceding PPP data to be acknowledged, let PPPoE Server release the packet with same packet identifier. */
PppTransmitDataCnf(0, NX_NULL, packet_id);
```

## <a name="pppreceivedataind"></a><span data-ttu-id="2a7e5-403">PppReceiveDataInd</span><span class="sxs-lookup"><span data-stu-id="2a7e5-403">PppReceiveDataInd</span></span>

<span data-ttu-id="2a7e5-404">Ricevere dati dalla trasmissione tramite Ethernet</span><span class="sxs-lookup"><span data-stu-id="2a7e5-404">Receive data from transmission over Ethernet</span></span>

### <a name="prototype"></a><span data-ttu-id="2a7e5-405">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2a7e5-405">Prototype</span></span>

```c
VOID PppReceiveDataInd(UINT interfaceHandle, UINT length, UCHAR *aData);
```

### <a name="description"></a><span data-ttu-id="2a7e5-406">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2a7e5-406">Description</span></span>

<span data-ttu-id="2a7e5-407">Il software PPPoE esporrà questa funzione per ricevere i dati per la trasmissione tramite Ethernet</span><span class="sxs-lookup"><span data-stu-id="2a7e5-407">The PPPoE software will expose this function to receive data for transmission over Ethernet</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a7e5-408">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="2a7e5-408">Input Parameters</span></span>

- <span data-ttu-id="2a7e5-409">**interfaceHandle**: handle di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-409">**interfaceHandle**: Interface handle.</span></span>
- <span data-ttu-id="2a7e5-410">**length**: numero di byte in ADATA.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-410">**length**: The number of bytes in aData.</span></span>
- <span data-ttu-id="2a7e5-411">**ADATA**: buffer dei dati contenente il frame di dati PPP.</span><span class="sxs-lookup"><span data-stu-id="2a7e5-411">**aData**: Data buffer containing the frame of PPP data.</span></span>

### <a name="return-values"></a><span data-ttu-id="2a7e5-412">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2a7e5-412">Return Values</span></span>

<span data-ttu-id="2a7e5-413">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="2a7e5-413">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2a7e5-414">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2a7e5-414">Allowed From</span></span>

<span data-ttu-id="2a7e5-415">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2a7e5-415">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="2a7e5-416">Esempio</span><span class="sxs-lookup"><span data-stu-id="2a7e5-416">Example</span></span>

```c
/* Receive data from transmission over Ethernet, data start pointer is aData.
The number of bytes in aData is 1480. */
PppReceiveDataInd (0, 1480, aData);
```