---
title: Capitolo 3-Descrizione dei servizi client PPPoE di Azure RTO NetX
description: Questo capitolo contiene una descrizione di tutti i servizi client PPPoE di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 246115fc97d7597246f7fd5b4fb88cb615baab33
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821494"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-client-services"></a><span data-ttu-id="a7b1b-103">Capitolo 3-Descrizione dei servizi client PPPoE di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="a7b1b-103">Chapter 3 - Description of Azure RTOS NetX PPPoE Client Services</span></span>

<span data-ttu-id="a7b1b-104">Questo capitolo contiene una descrizione di tutti i servizi client PPPoE di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-104">This chapter contains a description of all Azure RTOS NetX PPPoE Client services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="a7b1b-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="a7b1b-106">**nx_pppoe_client_create** *creare un'istanza del client PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-106">**nx_pppoe_client_create** *Create a PPPoE Client instance*</span></span>
- <span data-ttu-id="a7b1b-107">**nx_pppoe_client_delete** *eliminare un'istanza del client PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-107">**nx_pppoe_client_delete** *Delete a PPPoE Client instance*</span></span>
- <span data-ttu-id="a7b1b-108">**nx_pppoe_client_host_uniq_set** *impostare l'host univoco per il client PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-108">**nx_pppoe_client_host_uniq_set** *Set the host unique for PPPoE Client*</span></span>
- <span data-ttu-id="a7b1b-109">**nx_pppoe_client_host_uniq_set_extended** *impostare l'host univoco per il client PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-109">**nx_pppoe_client_host_uniq_set_extended** *Set the host unique for PPPoE Client*</span></span>
- <span data-ttu-id="a7b1b-110">**nx_pppoe_client_service_name_set** *impostare il nome del servizio per il client PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-110">**nx_pppoe_client_service_name_set** *Set the service name for PPPoE Client*</span></span>
- <span data-ttu-id="a7b1b-111">**nx_pppoe_client_service_name_set_extended** *impostare il nome del servizio per il client PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-111">**nx_pppoe_client_service_name_set_extended** *Set the service name for PPPoE Client*</span></span>
- <span data-ttu-id="a7b1b-112">**nx_pppoe_client_session_connect** *connettere la sessione client PPPoE al server PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-112">**nx_pppoe_client_session_connect** *Connect PPPoE Client session to PPPoE Server*</span></span>
- <span data-ttu-id="a7b1b-113">**nx_pppoe_client_session_packet_send** *inviare il pacchetto di sessione PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-113">**nx_pppoe_client_session_packet_send** *Send PPPoE session packet*</span></span>
- <span data-ttu-id="a7b1b-114">**nx_pppoe_client_session_terminate** *terminare la sessione PPPoE*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-114">**nx_pppoe_client_session_terminate** *Terminate the PPPoE session*</span></span>
- <span data-ttu-id="a7b1b-115">**nx_pppoe_client_session_get** *ottenere il inf della sessione PPPoE specificato*</span><span class="sxs-lookup"><span data-stu-id="a7b1b-115">**nx_pppoe_client_session_get** *Get the specified PPPoE session inf*</span></span>

## <a name="nx_pppoe_client_create"></a><span data-ttu-id="a7b1b-116">nx_pppoe_client_create</span><span class="sxs-lookup"><span data-stu-id="a7b1b-116">nx_pppoe_client_create</span></span>

<span data-ttu-id="a7b1b-117">Creare un'istanza del client PPPoE</span><span class="sxs-lookup"><span data-stu-id="a7b1b-117">Create a PPPoE Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-118">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-118">Prototype</span></span>

```c
UINT  nx_pppoe_client_create(NX_PPPOE_CLIENT *pppoe_client_ptr,
                            CHAR *name, NX_IP *ip_ptr,
                            UINT interface_index,
                            NX_PACKET_POOL *pool_ptr,
                            VOID *stack_ptr, ULONG stack_size,
                            UINT priority,
                            VOID (*pppoe_link_driver)
                            (struct NX_IP_DRIVER_STRUCT *)
                            VOID (*pppoe_packet_receive)
                            (NX_PACKET *packet_ptr));
```

### <a name="description"></a><span data-ttu-id="a7b1b-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-119">Description</span></span>

<span data-ttu-id="a7b1b-120">Questo servizio crea un'istanza del client PPPoE con il driver di collegamento fornito dall'utente per l'istanza IP NetX specificata.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-120">This service creates a PPPoE Client instance with the user supplied link driver for the specified NetX IP instance.</span></span> <span data-ttu-id="a7b1b-121">Se il driver di collegamento non è stato inizializzato e abilitato, il software client PPPoE è responsabile dell'inizializzazione del driver di collegamento.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-121">If link driver has not been initialized, and enabled, PPPoE Client software is responsible initializing the link driver.</span></span>

<span data-ttu-id="a7b1b-122">Inoltre, l'applicazione deve fornire un pool di pacchetti creato in precedenza per l'istanza del client PPPoE da usare per l'allocazione dei pacchetti interna.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-122">In addition, the application must supply a previously created packet pool for the PPPoE Client instance to use for internal packet allocation.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-123">In genere è consigliabile creare il thread IP NetX con una priorità più alta rispetto alla priorità del thread del client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-123">Generally a good idea to create the NetX IP thread at a higher priority than the PPPoE Client thread priority.</span></span> <span data-ttu-id="a7b1b-124">Per ulteriori informazioni su come specificare la priorità del thread IP, fare riferimento al servizio *nx_ip_create* .</span><span class="sxs-lookup"><span data-stu-id="a7b1b-124">Please refer to the *nx_ip_create* service for more information on specifying the IP thread priority.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-125">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-125">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-126">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-126">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="a7b1b-127">**nome** Nome dell'istanza del client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-127">**name** Name of this PPPoE Client instance.</span></span>
 - <span data-ttu-id="a7b1b-128">**ip_ptr** Puntatore al blocco di controllo per l'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-128">**ip_ptr** Pointer to control block for IP instance.</span></span>
 - <span data-ttu-id="a7b1b-129">**interface_index** Indice dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-129">**interface_index** Interface index.</span></span>
 - <span data-ttu-id="a7b1b-130">**pool_ptr** Puntatore al pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-130">**pool_ptr** Pointer to packet pool.</span></span>
 - <span data-ttu-id="a7b1b-131">**stack_ptr** Puntatore all'inizio dell'area dello stack del thread del client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-131">**stack_ptr** Pointer to start of PPPoE Client thread’s stack area.</span></span>
 - <span data-ttu-id="a7b1b-132">**stack_size** Dimensioni in byte nello stack del thread.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-132">**stack_size** Size in bytes in the thread’s stack.</span></span>
 - <span data-ttu-id="a7b1b-133">**priorità** di Priorità dei thread client PPPoE interni (1-31).</span><span class="sxs-lookup"><span data-stu-id="a7b1b-133">**priority** Priority of internal PPPoE Client threads (1-31).</span></span>
 - <span data-ttu-id="a7b1b-134">**pppoe_link_driver** Driver di collegamento fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-134">**pppoe_link_driver** User supplied link driver.</span></span>
 - <span data-ttu-id="a7b1b-135">**pppoe_packet_receive** Funzione di ricezione pacchetti fornita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-135">**pppoe_packet_receive** User supplied packet receive function.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-136">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-136">Return Values</span></span>

 - <span data-ttu-id="a7b1b-137">Creazione del client PPPoE riuscita **NX_PPPOE_CLIENT_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="a7b1b-137">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client create.</span></span>
 - <span data-ttu-id="a7b1b-138">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) client PPPoE, IP, pool di pacchetti o puntatore dello stack non validi.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-138">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client, IP, packet pool, or stack pointer.</span></span>
 - <span data-ttu-id="a7b1b-139">L'interfaccia NX_PPPOE_CLIENT_INVALID_INTERFACE (0xD2) non è valida.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-139">NX_PPPOE_CLIENT_INVALID_INTERFACE (0xD2) Invalid interface.</span></span>
 - <span data-ttu-id="a7b1b-140">Dimensioni del payload del pool di pacchetti NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) non valide.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-140">NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) Invalid payload size of packet pool.</span></span>
 - <span data-ttu-id="a7b1b-141">Dimensioni della memoria NX_PPPOE_CLIENT_MEMORY_SIZE_ERROR (0xD4) non valide.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-141">NX_PPPOE_CLIENT_MEMORY_SIZE_ERROR (0xD4) Invalid memory size.</span></span>
 - <span data-ttu-id="a7b1b-142">NX_PPPOE_CLIENT_PRIORITY_ERROR (0xD5) priorità non valida del thread del client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-142">NX_PPPOE_CLIENT_PRIORITY_ERROR (0xD5) Invalid priority of PPPoE Client thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-143">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-143">Allowed From</span></span>

<span data-ttu-id="a7b1b-144">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-144">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-145">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-145">Example</span></span>

```c
/* Create “my_pppoe_client” for IP instance “my_ip”. */
status =  nx_pppoe_client_create(&my_pppoe_client, “my PPPoE Client”, &my_ip,
0, &my_pool, stack_start, 1024, 2,
link_driver, packet_receive);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully created. */
```

## <a name="nx_pppoe_client_delete"></a><span data-ttu-id="a7b1b-146">nx_pppoe_client_delete</span><span class="sxs-lookup"><span data-stu-id="a7b1b-146">nx_pppoe_client_delete</span></span>

<span data-ttu-id="a7b1b-147">Eliminare un'istanza del client PPPoE</span><span class="sxs-lookup"><span data-stu-id="a7b1b-147">Delete a PPPoE Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-148">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-148">Prototype</span></span>

```c
UINT nx_pppoe_client_delete(NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a><span data-ttu-id="a7b1b-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-149">Description</span></span>

<span data-ttu-id="a7b1b-150">Questo servizio Elimina l'istanza del client PPPoE creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-150">This service deletes the previously created PPPoE Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-151">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-151">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-152">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE</span><span class="sxs-lookup"><span data-stu-id="a7b1b-152">**pppoe_client_ptr** Pointer to PPPoE Client control block</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-153">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-153">Return Values</span></span>

 - <span data-ttu-id="a7b1b-154">L'eliminazione del client PPPoE riuscita **NX_PPPOE_CLIENT_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="a7b1b-154">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client delete.</span></span>
 - <span data-ttu-id="a7b1b-155">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-155">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-156">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-156">Allowed From</span></span>

<span data-ttu-id="a7b1b-157">Thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-157">Threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-158">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-158">Example</span></span>

```c
/* Delete PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_delete(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully deleted. */
```

## <a name="nx_pppoe_client_host_uniq_set"></a><span data-ttu-id="a7b1b-159">nx_pppoe_client_host_uniq_set</span><span class="sxs-lookup"><span data-stu-id="a7b1b-159">nx_pppoe_client_host_uniq_set</span></span>

<span data-ttu-id="a7b1b-160">Imposta host client PPPoE univoco</span><span class="sxs-lookup"><span data-stu-id="a7b1b-160">Set PPPoE Client host unique</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-161">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-161">Prototype</span></span>

```c
UINT nx_pppoe_client_host_uniq_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq);
```

### <a name="description"></a><span data-ttu-id="a7b1b-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-162">Description</span></span>

<span data-ttu-id="a7b1b-163">Questo servizio imposta l'host client PPPoE come univoco.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-163">This service sets PPPoE Client host unique.</span></span> <span data-ttu-id="a7b1b-164">Host-Uniq viene utilizzato da un host per associare in modo univoco un concentratore di accesso a una determinata richiesta host.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-164">Host-Uniq is used by a host to uniquely associate an Access Concentrator to a particular Host request.</span></span>
<span data-ttu-id="a7b1b-165">Può essere dati binari di qualsiasi valore e lunghezza che l'host sceglie.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-165">It can be binary data of any value and length that the Host chooses.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-166">l'host univoco deve essere una stringa con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-166">host unique must be Null-terminated string.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-167">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-167">This service is deprecated.</span></span> <span data-ttu-id="a7b1b-168">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_pppoe_client_host_uniq_set_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-168">Developers are encouraged to migrate to *nx_pppoe_client_host_uniq_set_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-169">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-169">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-170">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-170">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="a7b1b-171">**host_uniq** Puntatore a un host univoco.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-171">**host_uniq** Pointer to an host unique.</span></span> <span data-ttu-id="a7b1b-172">L'host univoco deve essere una stringa con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-172">Host unique must be Null-terminated string.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-173">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-173">Return Values</span></span>

 - <span data-ttu-id="a7b1b-174">Il set univoco dell'host client PPPoE **NX_PPPOE_CLIENT_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-174">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client host unique set.</span></span>
 - <span data-ttu-id="a7b1b-175">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-175">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-176">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-176">Allowed From</span></span>

<span data-ttu-id="a7b1b-177">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-177">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-178">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-178">Example</span></span>

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set(&my_pppoe_client,
“220000000000000041000000”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_host_uniq_set_extended"></a><span data-ttu-id="a7b1b-179">nx_pppoe_client_host_uniq_set_extended</span><span class="sxs-lookup"><span data-stu-id="a7b1b-179">nx_pppoe_client_host_uniq_set_extended</span></span>

<span data-ttu-id="a7b1b-180">Imposta host client PPPoE univoco</span><span class="sxs-lookup"><span data-stu-id="a7b1b-180">Set PPPoE Client host unique</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-181">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-181">Prototype</span></span>

```c
UINT nx_pppoe_client_host_uniq_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq,UINT host_uniq_length);
```

### <a name="description"></a><span data-ttu-id="a7b1b-182">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-182">Description</span></span>

<span data-ttu-id="a7b1b-183">Questo servizio imposta l'host client PPPoE come univoco.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-183">This service sets PPPoE Client host unique.</span></span> <span data-ttu-id="a7b1b-184">Host-Uniq viene utilizzato da un host per associare in modo univoco un concentratore di accesso a una determinata richiesta host.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-184">Host-Uniq is used by a host to uniquely associate an Access Concentrator to a particular Host request.</span></span>
<span data-ttu-id="a7b1b-185">Può essere dati binari di qualsiasi valore e lunghezza che l'host sceglie.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-185">It can be binary data of any value and length that the Host chooses.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-186">l'host univoco deve essere una stringa con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-186">host unique must be Null-terminated string.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-187">Questo servizio sostituisce *nx_pppoe_client_host_uniq_set ()*.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-187">This service replaces *nx_pppoe_client_host_uniq_set()*.</span></span> <span data-ttu-id="a7b1b-188">Questa versione fornisce informazioni aggiuntive sulla lunghezza per il servizio.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-188">This version supplies additional length information to the service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-189">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-189">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-190">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-190">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="a7b1b-191">**host_uniq** Puntatore a un host univoco.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-191">**host_uniq** Pointer to an host unique.</span></span> <span data-ttu-id="a7b1b-192">L'host univoco deve essere una stringa con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-192">Host unique must be Null-terminated string.</span></span>
 - <span data-ttu-id="a7b1b-193">**host_uniq_length** Lunghezza di host_uniq</span><span class="sxs-lookup"><span data-stu-id="a7b1b-193">**host_uniq_length** Length of host_uniq</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-194">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-194">Return Values</span></span>

 - <span data-ttu-id="a7b1b-195">Il set univoco dell'host client PPPoE **NX_PPPOE_CLIENT_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-195">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client host unique set.</span></span>
 - <span data-ttu-id="a7b1b-196">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-196">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Invalid PPPoE Client pointer.</span></span>
 - <span data-ttu-id="a7b1b-197">Controllo **NX_SIZE_ERROR** (0x09) host_uniq_length esito negativo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-197">**NX_SIZE_ERROR** (0x09) Check host_uniq_length fail</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-198">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-198">Allowed From</span></span>

<span data-ttu-id="a7b1b-199">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-199">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-200">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-200">Example</span></span>

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set_extended(&my_pppoe_client,
“220000000000000041000000”,24);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_service_name_set"></a><span data-ttu-id="a7b1b-201">nx_pppoe_client_service_name_set</span><span class="sxs-lookup"><span data-stu-id="a7b1b-201">nx_pppoe_client_service_name_set</span></span>

<span data-ttu-id="a7b1b-202">Imposta il nome del servizio client PPPoE</span><span class="sxs-lookup"><span data-stu-id="a7b1b-202">Set PPPoE Client service name</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-203">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-203">Prototype</span></span>

```c
UINT nx_pppoe_client_service_name_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *service_name);
```

### <a name="description"></a><span data-ttu-id="a7b1b-204">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-204">Description</span></span>

<span data-ttu-id="a7b1b-205">Questo servizio imposta il nome del servizio client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-205">This service sets PPPoE Client service name.</span></span> <span data-ttu-id="a7b1b-206">Service-Name che indica il servizio richiesto dall'host.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-206">The Service-Name indicating the service the Host is requesting.</span></span> <span data-ttu-id="a7b1b-207">Se Service-Name non è impostato, indica che l'host accetterà un numero qualsiasi di servizi.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-207">If Service-Name is not set, indicating Host will accept any number of services.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-208">il nome del servizio deve essere una stringa con terminazione null</span><span class="sxs-lookup"><span data-stu-id="a7b1b-208">service name must be Null-terminated string</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-209">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-209">This service is deprecated.</span></span> <span data-ttu-id="a7b1b-210">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_pppoe_client_service_name_set_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-210">Developers are encouraged to migrate to *nx_pppoe_client_service_name_set_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-211">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-211">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-212">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-212">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="a7b1b-213">**SERVICE_NAME** Puntatore a un nome di servizio.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-213">**service_name** Pointer to an service name.</span></span> <span data-ttu-id="a7b1b-214">Il nome del servizio deve essere una stringa con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-214">Service name must be Null-terminated string.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-215">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-215">Return Values</span></span>

 - <span data-ttu-id="a7b1b-216">**NX_PPPOE_CLIENT_SUCCESS** (0x00) il nome del servizio client PPPoE è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-216">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client service name set.</span></span>
 - <span data-ttu-id="a7b1b-217">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-217">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-218">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-218">Allowed From</span></span>

<span data-ttu-id="a7b1b-219">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-219">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-220">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-220">Example</span></span>

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_service_name_set(&my_pppoe_client,
“BRAS”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” service name has set. */
```

## <a name="nx_pppoe_client_service_name_set_extended"></a><span data-ttu-id="a7b1b-221">nx_pppoe_client_service_name_set_extended</span><span class="sxs-lookup"><span data-stu-id="a7b1b-221">nx_pppoe_client_service_name_set_extended</span></span>

<span data-ttu-id="a7b1b-222">Imposta il nome del servizio client PPPoE</span><span class="sxs-lookup"><span data-stu-id="a7b1b-222">Set PPPoE Client service name</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-223">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-223">Prototype</span></span>

```c
UINT nx_pppoe_client_service_name_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *service_name,UINT service_name_length);
```

### <a name="description"></a><span data-ttu-id="a7b1b-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-224">Description</span></span>

<span data-ttu-id="a7b1b-225">Questo servizio imposta il nome del servizio client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-225">This service sets PPPoE Client service name.</span></span> <span data-ttu-id="a7b1b-226">Service-Name che indica il servizio richiesto dall'host.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-226">The Service-Name indicating the service the Host is requesting.</span></span> <span data-ttu-id="a7b1b-227">Se Service-Name non è impostato, indica che l'host accetterà un numero qualsiasi di servizi.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-227">If Service-Name is not set, indicating Host will accept any number of services.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-228">il nome del servizio deve essere una stringa con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-228">service name must be Null-terminated string.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-229">Questo servizio sostituisce *nx_pppoe_client_service_name_set ()*.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-229">This service replaces *nx_pppoe_client_service_name_set()*.</span></span> <span data-ttu-id="a7b1b-230">Questa versione fornisce informazioni aggiuntive sulla lunghezza del nome del servizio alla funzione.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-230">This version supplies additional service name length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-231">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-231">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-232">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-232">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="a7b1b-233">**SERVICE_NAME** Puntatore a un nome di servizio.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-233">**service_name** Pointer to an service name.</span></span> <span data-ttu-id="a7b1b-234">Il nome del servizio deve essere una stringa con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-234">Service name must be Null-terminated string.</span></span>
 - <span data-ttu-id="a7b1b-235">**service_name_length** Lunghezza di service_name</span><span class="sxs-lookup"><span data-stu-id="a7b1b-235">**service_name_length** Length of service_name</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-236">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-236">Return Values</span></span>

 - <span data-ttu-id="a7b1b-237">**NX_PPPOE_CLIENT_SUCCESS** (0x00) il nome del servizio client PPPoE è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-237">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client service name set.</span></span>
 - <span data-ttu-id="a7b1b-238">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-238">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Invalid PPPoE Client pointer.</span></span>
 - <span data-ttu-id="a7b1b-239">Controllo **NX_SIZE_ERROR** (0x09) service_name_length esito negativo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-239">**NX_SIZE_ERROR** (0x09) Check service_name_length fail</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-240">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-240">Allowed From</span></span>

<span data-ttu-id="a7b1b-241">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-241">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-242">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-242">Example</span></span>

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_service_name_set_extended(&my_pppoe_client,
“BRAS”,4);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” service name has set. */
```

## <a name="nx_pppoe_client_session_connect"></a><span data-ttu-id="a7b1b-243">nx_pppoe_client_session_connect</span><span class="sxs-lookup"><span data-stu-id="a7b1b-243">nx_pppoe_client_session_connect</span></span>

<span data-ttu-id="a7b1b-244">Connetti sessione client PPPoE</span><span class="sxs-lookup"><span data-stu-id="a7b1b-244">Connect PPPoE Client session</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-245">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-245">Prototype</span></span>

```c
UINT nx_pppoe_client_session_connect(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="a7b1b-246">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-246">Description</span></span>

<span data-ttu-id="a7b1b-247">Questo servizio esegue la connessione di sessione PPPoE utilizzando un client PPPoE creato in precedenza al server PPPoE specificato.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-247">This service makes PPPoE session connection using a previously created PPPoE Client to the specified PPPoE Server.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1b-248">Questa funzione deve essere chiamata dopo *nx_pppoe_client_create*, *nx_pppoe_client_host_uniq_set* e *nx_pppoe_client_service_name_set*.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-248">This function must be called after *nx_pppoe_client_create*, *nx_pppoe_client_host_uniq_set* and *nx_pppoe_client_service_name_set*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-249">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-249">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-250">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-250">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="a7b1b-251">**WAIT_OPTION** Opzione wait mentre viene stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-251">**wait_option** Wait option while the connection is being established.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-252">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-252">Return Values</span></span>

 - <span data-ttu-id="a7b1b-253">**NX_PPPOE_CLIENT_SUCCESS** (0x00) connessione della sessione client PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-253">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client session connect.</span></span>
 - <span data-ttu-id="a7b1b-254">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-254">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-255">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-255">Allowed From</span></span>

<span data-ttu-id="a7b1b-256">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-256">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-257">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-257">Example</span></span>

```c
/* Enable PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_connect(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” session connection has connected. */
```

## <a name="nx_pppoe_client_session_packet_send"></a><span data-ttu-id="a7b1b-258">nx_pppoe_client_session_packet_send</span><span class="sxs-lookup"><span data-stu-id="a7b1b-258">nx_pppoe_client_session_packet_send</span></span>

<span data-ttu-id="a7b1b-259">Invia pacchetto client PPPoE alla sessione specificata</span><span class="sxs-lookup"><span data-stu-id="a7b1b-259">Send PPPoE Client packet to specified session</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-260">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-260">Prototype</span></span>

```c
UINT nx_pppoe_client_session_packet_send(
                                    NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="a7b1b-261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-261">Description</span></span>

<span data-ttu-id="a7b1b-262">Questo servizio invia il pacchetto PPPoE usando l'ID sessione specificato.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-262">This service sends PPPoE packet using specified session ID.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-263">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-263">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-264">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-264">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="a7b1b-265">**packet_ptr** Puntatore al pacchetto PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-265">**packet_ptr** Pointer to PPPoE packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-266">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-266">Return Values</span></span>

 - <span data-ttu-id="a7b1b-267">**NX_PPPOE_CLIENT_SUCCESS** (0x00) ha completato l'invio di pacchetti client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-267">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client packet send.</span></span>
 - <span data-ttu-id="a7b1b-268">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-268">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>
 - <span data-ttu-id="a7b1b-269">NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) pacchetto client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-269">NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) Invalid PPPoE Client packet.</span></span>
 - <span data-ttu-id="a7b1b-270">La sessione PPPoE NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) non è stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-270">NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-271">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-271">Allowed From</span></span>

<span data-ttu-id="a7b1b-272">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-272">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-273">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-273">Example</span></span>

```c
/* Send PPPoE client packet to specified session, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_packet_send(&my_pppoe_client, packet_ptr);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” packet has sent. */
```

## <a name="nx_pppoe_client_session_terminate"></a><span data-ttu-id="a7b1b-274">nx_pppoe_client_session_terminate</span><span class="sxs-lookup"><span data-stu-id="a7b1b-274">nx_pppoe_client_session_terminate</span></span>

<span data-ttu-id="a7b1b-275">Termina sessione client PPPoE</span><span class="sxs-lookup"><span data-stu-id="a7b1b-275">Terminate PPPoE Client session</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-276">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-276">Prototype</span></span>

```c
UINT nx_pppoe_client_session_terminate(
                                    NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a><span data-ttu-id="a7b1b-277">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-277">Description</span></span>

<span data-ttu-id="a7b1b-278">Questo servizio termina la sessione PPPoE specificata.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-278">This service terminates the specified PPPoE session.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-279">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-279">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-280">**pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-280">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-281">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-281">Return Values</span></span>

 - <span data-ttu-id="a7b1b-282">**NX_PPPOE_CLIENT_SUCCESS** (0x00) termina la sessione client PPPoE riuscita.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-282">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client session terminate.</span></span>
 - <span data-ttu-id="a7b1b-283">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-283">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-284">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-284">Allowed From</span></span>

<span data-ttu-id="a7b1b-285">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-285">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-286">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-286">Example</span></span>

```c
/* Terminates the specified PPPoE session, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_terminate(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the session has terminated. */
```

## <a name="nx_pppoe_client_session_get"></a><span data-ttu-id="a7b1b-287">nx_pppoe_client_session_get</span><span class="sxs-lookup"><span data-stu-id="a7b1b-287">nx_pppoe_client_session_get</span></span>

<span data-ttu-id="a7b1b-288">Ottenere le informazioni sulla sessione PPPoE specificate</span><span class="sxs-lookup"><span data-stu-id="a7b1b-288">Get the specified PPPoE session information</span></span>

### <a name="prototype"></a><span data-ttu-id="a7b1b-289">Prototipo</span><span class="sxs-lookup"><span data-stu-id="a7b1b-289">Prototype</span></span>

```c
UINT nx_pppoe_client_session_get(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                ULONG *server_mac_msw,
                                ULONG *server_mac_lsw,
                                ULONG *session_id);
```

### <a name="description"></a><span data-ttu-id="a7b1b-290">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b1b-290">Description</span></span>

<span data-ttu-id="a7b1b-291">Questo servizio ottiene le informazioni sulla sessione PPPoE specificate, l'indirizzo fisico del server e l'ID di sessione.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-291">This service gets the specified PPPoE session information, server physical address and session id.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="a7b1b-292">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="a7b1b-292">Input Parameters</span></span>

 - <span data-ttu-id="a7b1b-293">**pppoe_server_ptr** Puntatore al blocco di controllo client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-293">**pppoe_server_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="a7b1b-294">**server_mac_msw** Puntatore a RSU indirizzo fisico server.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-294">**server_mac_msw** Server Physical address MSW pointer.</span></span>
 - <span data-ttu-id="a7b1b-295">**server_mac_lsw** Puntatore a RSU indirizzo fisico server.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-295">**server_mac_lsw** Server Physical address MSW pointer.</span></span>
 - <span data-ttu-id="a7b1b-296">**session_id** Puntatore ID sessione.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-296">**session_id** Session ID pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="a7b1b-297">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="a7b1b-297">Return Values</span></span>

 - <span data-ttu-id="a7b1b-298">**NX_PPPOE_CLIENT_SUCCESS** (0x00) riuscita sessione client PPPoE Get.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-298">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client session get.</span></span>
 - <span data-ttu-id="a7b1b-299">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) puntatore client PPPoE non valido.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-299">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>
 - <span data-ttu-id="a7b1b-300">La sessione PPPoE NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) non è stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="a7b1b-300">NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="a7b1b-301">Consentito da</span><span class="sxs-lookup"><span data-stu-id="a7b1b-301">Allowed From</span></span>

<span data-ttu-id="a7b1b-302">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="a7b1b-302">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="a7b1b-303">Esempio</span><span class="sxs-lookup"><span data-stu-id="a7b1b-303">Example</span></span>

```c
/* Gets the specified PPPoE session information, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_get (&my_pppoe_client, &server_mac_msw, &server_mac_lsw, &session_id);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the server physical address and session id
   of the session has got. */
```
