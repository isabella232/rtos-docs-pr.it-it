---
title: Capitolo 3-Descrizione dei servizi AutoIP NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi AutoIP di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 22cc06c32cc9f1857b32d1d2b44a506ea1652cfd
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822751"
---
# <a name="chapter-3---description-of-azure-rtos-netx-autoip-services"></a><span data-ttu-id="da8cf-103">Capitolo 3-Descrizione dei servizi AutoIP NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="da8cf-103">Chapter 3 - Description of Azure RTOS NetX AutoIP services</span></span>

<span data-ttu-id="da8cf-104">Questo capitolo contiene una descrizione di tutti i servizi AutoIP di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="da8cf-104">This chapter contains a description of all Azure RTOS NetX AutoIP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="da8cf-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="da8cf-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="da8cf-106">**nx_auto_ip_create**: *creare un'istanza di AutoIP*</span><span class="sxs-lookup"><span data-stu-id="da8cf-106">**nx_auto_ip_create**: *Create AutoIP instance*</span></span>
- <span data-ttu-id="da8cf-107">**nx_auto_ip_delete**: *eliminare l'istanza di AutoIP*</span><span class="sxs-lookup"><span data-stu-id="da8cf-107">**nx_auto_ip_delete**: *Delete AutoIP instance*</span></span>
- <span data-ttu-id="da8cf-108">**nx_auto_ip_get_address**: *ottenere l'indirizzo AutoIP corrente*</span><span class="sxs-lookup"><span data-stu-id="da8cf-108">**nx_auto_ip_get_address**: *Get current AutoIP address*</span></span>
- <span data-ttu-id="da8cf-109">**nx_auto_ip_set_interface**: *impostare l'interfaccia IP per la necessità di un indirizzo AutoIP*</span><span class="sxs-lookup"><span data-stu-id="da8cf-109">**nx_auto_ip_set_interface**: *Set IP interface needing an AutoIP address*</span></span>
- <span data-ttu-id="da8cf-110">**nx_auto_ip_start**: *Avvia elaborazione AutoIP*</span><span class="sxs-lookup"><span data-stu-id="da8cf-110">**nx_auto_ip_start**: *Start AutoIP processing*</span></span>
- <span data-ttu-id="da8cf-111">**nx_auto_ip_stop**: *Arresta elaborazione AutoIP*</span><span class="sxs-lookup"><span data-stu-id="da8cf-111">**nx_auto_ip_stop**: *Stop AutoIP processing*</span></span>

## <a name="nx_auto_ip_create"></a><span data-ttu-id="da8cf-112">nx_auto_ip_create</span><span class="sxs-lookup"><span data-stu-id="da8cf-112">nx_auto_ip_create</span></span>

<span data-ttu-id="da8cf-113">Creare un'istanza di AutoIP</span><span class="sxs-lookup"><span data-stu-id="da8cf-113">Create AutoIP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="da8cf-114">Prototipo</span><span class="sxs-lookup"><span data-stu-id="da8cf-114">Prototype</span></span>

```c
UINT nx_auto_ip_create(NX_AUTO_IP *auto_ip_ptr, CHAR *name,
            NX_IP *ip_ptr, VOID *stack_ptr, ULONG stack_size,
            UINT priority);
```

### <a name="description"></a><span data-ttu-id="da8cf-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="da8cf-115">Description</span></span>

<span data-ttu-id="da8cf-116">Questo servizio crea un'istanza di AutoIP nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="da8cf-116">This service creates an AutoIP instance on the specified IP instance.</span></span>

- <span data-ttu-id="da8cf-117">**auto_ip_ptr**: puntatore al blocco di controllo AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-117">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="da8cf-118">**nome**: nome dell'istanza di AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-118">**name**: Name of AutoIP instance.</span></span>
- <span data-ttu-id="da8cf-119">**ip_ptr**: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-119">**ip_ptr**: Pointer to IP instance.</span></span>
- <span data-ttu-id="da8cf-120">**stack_ptr**: puntatore all'area dello stack di thread AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-120">**stack_ptr**: Pointer to AutoIP thread stack area.</span></span>
- <span data-ttu-id="da8cf-121">**stack_size**: dimensioni dell'area dello stack di thread AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-121">**stack_size**: Size of the AutoIP thread stack area.</span></span>
- <span data-ttu-id="da8cf-122">**Priority**: priorità del thread AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-122">**priority**: Priority of the AutoIP thread.</span></span>

> [!NOTE]
> <span data-ttu-id="da8cf-123">Se si usa DHCP, il thread DHCP deve avere una priorità più elevata rispetto al thread dell'istanza IP e al thread AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-123">If DHCP is used, the DHCP thread must have a higher priority than the IP instance thread and the AutoIP thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="da8cf-124">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="da8cf-124">Return Values</span></span>

- <span data-ttu-id="da8cf-125">**NX_SUCCESS**: (0x00) creazione AutoIP riuscita.</span><span class="sxs-lookup"><span data-stu-id="da8cf-125">**NX_SUCCESS**: (0x00) Successful AutoIP create.</span></span>
- <span data-ttu-id="da8cf-126">**NX_AUTO_IP_ERROR**: (0XA00) AutoIP crea errore.</span><span class="sxs-lookup"><span data-stu-id="da8cf-126">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP create error.</span></span>
- <span data-ttu-id="da8cf-127">NX_PTR_ERROR: (0x16) non valido AutoIP, ip_ptr o puntatore dello stack.</span><span class="sxs-lookup"><span data-stu-id="da8cf-127">NX_PTR_ERROR: (0x16) Invalid AutoIP, ip_ptr, or stack pointer.</span></span>
- <span data-ttu-id="da8cf-128">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-128">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="da8cf-129">Consentito da</span><span class="sxs-lookup"><span data-stu-id="da8cf-129">Allowed From</span></span>

<span data-ttu-id="da8cf-130">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="da8cf-130">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="da8cf-131">Esempio</span><span class="sxs-lookup"><span data-stu-id="da8cf-131">Example</span></span>

```c
/* Create the AutoIP instance "auto_ip_0" on "ip_0". */
status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);

/* If status is NX_SUCCESS an AutoIP instance was successfully created. */
```

### <a name="see-also"></a><span data-ttu-id="da8cf-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="da8cf-132">See Also</span></span>

<span data-ttu-id="da8cf-133">nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="da8cf-133">nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_delete"></a><span data-ttu-id="da8cf-134">nx_auto_ip_delete</span><span class="sxs-lookup"><span data-stu-id="da8cf-134">nx_auto_ip_delete</span></span>

<span data-ttu-id="da8cf-135">Elimina istanza AutoIP</span><span class="sxs-lookup"><span data-stu-id="da8cf-135">Delete AutoIP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="da8cf-136">Prototipo</span><span class="sxs-lookup"><span data-stu-id="da8cf-136">Prototype</span></span>

```c
UINT nx_auto_ip_delete(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a><span data-ttu-id="da8cf-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="da8cf-137">Description</span></span>

<span data-ttu-id="da8cf-138">Questo servizio Elimina un'istanza di AutoIP creata in precedenza nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="da8cf-138">This service deletes a previously created AutoIP instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="da8cf-139">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="da8cf-139">Input Parameters</span></span>

- <span data-ttu-id="da8cf-140">**auto_ip_ptr**: puntatore al blocco di controllo AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-140">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="da8cf-141">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="da8cf-141">Return Values</span></span>

- <span data-ttu-id="da8cf-142">**NX_SUCCESS**: (0x00) eliminazione AutoIP riuscita.</span><span class="sxs-lookup"><span data-stu-id="da8cf-142">**NX_SUCCESS**: (0x00) Successful AutoIP delete.</span></span>
- <span data-ttu-id="da8cf-143">**NX_AUTO_IP_ERROR**: (0XA00) AutoIP eliminare l'errore.</span><span class="sxs-lookup"><span data-stu-id="da8cf-143">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP delete error.</span></span>
- <span data-ttu-id="da8cf-144">NX_PTR_ERROR (0x16): puntatore AutoIP non valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-144">NX_PTR_ERROR (0x16): Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="da8cf-145">NX_CALLER_ERROR (0x11): chiamante non valido di questo servizio.</span><span class="sxs-lookup"><span data-stu-id="da8cf-145">NX_CALLER_ERROR (0x11): Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="da8cf-146">Consentito da</span><span class="sxs-lookup"><span data-stu-id="da8cf-146">Allowed From</span></span>

<span data-ttu-id="da8cf-147">Thread</span><span class="sxs-lookup"><span data-stu-id="da8cf-147">Threads</span></span>

### <a name="example"></a><span data-ttu-id="da8cf-148">Esempio</span><span class="sxs-lookup"><span data-stu-id="da8cf-148">Example</span></span>

```c
/* Delete the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_delete(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully deleted. */
```

### <a name="see-also"></a><span data-ttu-id="da8cf-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="da8cf-149">See Also</span></span>

<span data-ttu-id="da8cf-150">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="da8cf-150">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_get_address"></a><span data-ttu-id="da8cf-151">nx_auto_ip_get_address</span><span class="sxs-lookup"><span data-stu-id="da8cf-151">nx_auto_ip_get_address</span></span>

<span data-ttu-id="da8cf-152">Ottenere l'indirizzo AutoIP corrente</span><span class="sxs-lookup"><span data-stu-id="da8cf-152">Get current AutoIP address</span></span>

### <a name="prototype"></a><span data-ttu-id="da8cf-153">Prototipo</span><span class="sxs-lookup"><span data-stu-id="da8cf-153">Prototype</span></span>

```c
UINT nx_auto_ip_get_address(NX_AUTO_IP *auto_ip_ptr,
                            ULONG *local_ip_address);
```

### <a name="description"></a><span data-ttu-id="da8cf-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="da8cf-154">Description</span></span>

<span data-ttu-id="da8cf-155">Questo servizio recupera l'indirizzo AutoIP attualmente configurato.</span><span class="sxs-lookup"><span data-stu-id="da8cf-155">This service retrieves the currently setup AutoIP address.</span></span> <span data-ttu-id="da8cf-156">Se non ne esiste uno, viene restituito un indirizzo IP 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="da8cf-156">If there isn't one, an IP address of 0.0.0.0 is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="da8cf-157">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="da8cf-157">Input Parameters</span></span>

- <span data-ttu-id="da8cf-158">**auto_ip_ptr**: puntatore al blocco di controllo AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-158">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="da8cf-159">**local_ip_address**: destinazione per l'indirizzo IP restituito.</span><span class="sxs-lookup"><span data-stu-id="da8cf-159">**local_ip_address**: Destination for return IP address.</span></span>

### <a name="return-values"></a><span data-ttu-id="da8cf-160">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="da8cf-160">Return Values</span></span>

- <span data-ttu-id="da8cf-161">**NX_SUCCESS**: (0x00) operazione AutoIP riuscita Get.</span><span class="sxs-lookup"><span data-stu-id="da8cf-161">**NX_SUCCESS**: (0x00) Successful AutoIP address get.</span></span>
- <span data-ttu-id="da8cf-162">**NX_AUTO_IP_NO_LOCAL**: (0XA01) non sono presenti indirizzi AutoIP validi.</span><span class="sxs-lookup"><span data-stu-id="da8cf-162">**NX_AUTO_IP_NO_LOCAL**: (0xA01) No valid AutoIP address.</span></span>
- <span data-ttu-id="da8cf-163">NX_PTR_ERROR: (0x16) puntatore AutoIP non valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-163">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="da8cf-164">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-164">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="da8cf-165">Consentito da</span><span class="sxs-lookup"><span data-stu-id="da8cf-165">Allowed From</span></span>

<span data-ttu-id="da8cf-166">Inizializzazione, timer, thread, ISRs</span><span class="sxs-lookup"><span data-stu-id="da8cf-166">Initialization, Timers, Threads, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="da8cf-167">Esempio</span><span class="sxs-lookup"><span data-stu-id="da8cf-167">Example</span></span>

```c
ULONG local_address;

/* Get the AutoIP address resolved by the instance "auto_ip_0." */
status = nx_auto_ip_get_address(&auto_ip_0, &local_address);

/* If status is NX_SUCCESS the local IP address is in "local_address." */
```

### <a name="see-also"></a><span data-ttu-id="da8cf-168">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="da8cf-168">See Also</span></span>

<span data-ttu-id="da8cf-169">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="da8cf-169">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_set_interface"></a><span data-ttu-id="da8cf-170">nx_auto_ip_set_interface</span><span class="sxs-lookup"><span data-stu-id="da8cf-170">nx_auto_ip_set_interface</span></span>

<span data-ttu-id="da8cf-171">Impostare l'interfaccia di rete per AutoIP</span><span class="sxs-lookup"><span data-stu-id="da8cf-171">Set network interface for AutoIP</span></span>

### <a name="prototype"></a><span data-ttu-id="da8cf-172">Prototipo</span><span class="sxs-lookup"><span data-stu-id="da8cf-172">Prototype</span></span>

```c
UINT nx_auto_ip_set_interface(NX_AUTO_IP *auto_ip_ptr,
                                UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="da8cf-173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="da8cf-173">Description</span></span>

<span data-ttu-id="da8cf-174">Questo servizio imposta l'indice per l'interfaccia di rete AutoIP esegue il probe per un indirizzo IP di rete.</span><span class="sxs-lookup"><span data-stu-id="da8cf-174">This service sets the index for the network interface AutoIP will probe for a network IP address.</span></span> <span data-ttu-id="da8cf-175">Il valore predefinito è zero (l'interfaccia di rete primaria).</span><span class="sxs-lookup"><span data-stu-id="da8cf-175">The default is zero (the primary network interface).</span></span> <span data-ttu-id="da8cf-176">Applicabile solo per i dispositivi multihomed.</span><span class="sxs-lookup"><span data-stu-id="da8cf-176">Only applicable for multihomed devices.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="da8cf-177">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="da8cf-177">Input Parameters</span></span>

- <span data-ttu-id="da8cf-178">**auto_ip_ptr**: puntatore al blocco di controllo AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-178">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="da8cf-179">**interface_index**: interfaccia per verificare l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="da8cf-179">**interface_index**: Interface to probe IP address for</span></span>

### <a name="return-values"></a><span data-ttu-id="da8cf-180">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="da8cf-180">Return Values</span></span>

- <span data-ttu-id="da8cf-181">**NX_SUCCESS**: (0x00) set di interfacce AutoIP riuscito</span><span class="sxs-lookup"><span data-stu-id="da8cf-181">**NX_SUCCESS**: (0x00) Successful AutoIP interface set</span></span>
- <span data-ttu-id="da8cf-182">**NX_AUTO_IP_BAD_INTERFACE_INDEX**: (0xA02) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="da8cf-182">**NX_AUTO_IP_BAD_INTERFACE_INDEX**: (0xA02) Invalid network interface</span></span> 
- <span data-ttu-id="da8cf-183">NX_PTR_ERROR: (0x16) puntatore AutoIP non valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-183">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="da8cf-184">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-184">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="da8cf-185">Consentito da</span><span class="sxs-lookup"><span data-stu-id="da8cf-185">Allowed From</span></span>

<span data-ttu-id="da8cf-186">Inizializzazione, timer, thread, ISRs</span><span class="sxs-lookup"><span data-stu-id="da8cf-186">Initialization, Timers, Threads, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="da8cf-187">Esempio</span><span class="sxs-lookup"><span data-stu-id="da8cf-187">Example</span></span>

```c
ULONG interface_index;

/* Set the network interface on which AutoIP probes for host address. */
status = nx_auto_ip_set_interface(&auto_ip_0, interface_index);

/* If status is NX_SUCCESS the network interface is valid and set in the AutoIP control block auto_ip_0. */
```

### <a name="see-also"></a><span data-ttu-id="da8cf-188">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="da8cf-188">See Also</span></span>

<span data-ttu-id="da8cf-189">nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="da8cf-189">nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_start"></a><span data-ttu-id="da8cf-190">nx_auto_ip_start</span><span class="sxs-lookup"><span data-stu-id="da8cf-190">nx_auto_ip_start</span></span>

<span data-ttu-id="da8cf-191">Avvia elaborazione AutoIP</span><span class="sxs-lookup"><span data-stu-id="da8cf-191">Start AutoIP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="da8cf-192">Prototipo</span><span class="sxs-lookup"><span data-stu-id="da8cf-192">Prototype</span></span>

```c
UINT nx_auto_ip_start(NX_AUTO_IP *auto_ip_ptr,
                    ULONG starting_local_address);
```

### <a name="description"></a><span data-ttu-id="da8cf-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="da8cf-193">Description</span></span>

<span data-ttu-id="da8cf-194">Questo servizio avvia il protocollo AutoIP in un'istanza di AutoIP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="da8cf-194">This service starts the AutoIP protocol on a previously created AutoIP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="da8cf-195">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="da8cf-195">Input Parameters</span></span>

- <span data-ttu-id="da8cf-196">**auto_ip_ptr**: puntatore al blocco di controllo AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-196">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="da8cf-197">**starting_local_address**: indirizzo iniziale AutoIP facoltativo.</span><span class="sxs-lookup"><span data-stu-id="da8cf-197">**starting_local_address**: Optional AutoIP starting address.</span></span> <span data-ttu-id="da8cf-198">Il valore IP_ADDRESS (0, 0, 0, 0) specifica che deve essere derivato un indirizzo AutoIP casuale.</span><span class="sxs-lookup"><span data-stu-id="da8cf-198">A value of IP_ADDRESS(0,0,0,0) specifies that a random AutoIP address should be derived.</span></span> <span data-ttu-id="da8cf-199">In caso contrario, se viene specificato un indirizzo AutoIP valido, NetX AutoIP tenterà di assegnare tale indirizzo.</span><span class="sxs-lookup"><span data-stu-id="da8cf-199">Otherwise, if a valid AutoIP address is specified, NetX AutoIP attempts to assign that address.</span></span>

### <a name="return-values"></a><span data-ttu-id="da8cf-200">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="da8cf-200">Return Values</span></span>

- <span data-ttu-id="da8cf-201">**NX_SUCCESS**: (0x00) avvio AutoIP riuscito.</span><span class="sxs-lookup"><span data-stu-id="da8cf-201">**NX_SUCCESS**: (0x00) Successful AutoIP start.</span></span>
- <span data-ttu-id="da8cf-202">**NX_AUTO_IP_ERROR**: (0XA00) AutoIP errore di avvio.</span><span class="sxs-lookup"><span data-stu-id="da8cf-202">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP start error.</span></span>
- <span data-ttu-id="da8cf-203">NX_PTR_ERROR: (0x16) puntatore AutoIP non valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-203">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="da8cf-204">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-204">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="da8cf-205">Consentito da</span><span class="sxs-lookup"><span data-stu-id="da8cf-205">Allowed From</span></span>

<span data-ttu-id="da8cf-206">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="da8cf-206">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="da8cf-207">Esempio</span><span class="sxs-lookup"><span data-stu-id="da8cf-207">Example</span></span>

```c
/* Start the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_start(&auto_ip_0, IP_ADDRESS(0,0,0,0));

/* If status is NX_SUCCESS an AutoIP instance was successfully started. */
```

### <a name="see-also"></a><span data-ttu-id="da8cf-208">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="da8cf-208">See Also</span></span>

<span data-ttu-id="da8cf-209">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="da8cf-209">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_stop"></a><span data-ttu-id="da8cf-210">nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="da8cf-210">nx_auto_ip_stop</span></span>

<span data-ttu-id="da8cf-211">Arresta elaborazione AutoIP</span><span class="sxs-lookup"><span data-stu-id="da8cf-211">Stop AutoIP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="da8cf-212">Prototipo</span><span class="sxs-lookup"><span data-stu-id="da8cf-212">Prototype</span></span>

```c
UINT nx_auto_ip_stop(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a><span data-ttu-id="da8cf-213">Descrizione</span><span class="sxs-lookup"><span data-stu-id="da8cf-213">Description</span></span>

<span data-ttu-id="da8cf-214">Questo servizio arresta il protocollo AutoIP in un'istanza di AutoIP creata e avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="da8cf-214">This service stops the AutoIP protocol on a previously created and started AutoIP instance.</span></span> <span data-ttu-id="da8cf-215">Questo servizio viene in genere usato quando l'indirizzo IP viene modificato tramite DHCP o manualmente in un indirizzo non AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-215">This service is typically used when the IP address is changed via DHCP or manually to a non-AutoIP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="da8cf-216">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="da8cf-216">Input Parameters</span></span>

- <span data-ttu-id="da8cf-217">**auto_ip_ptr**: puntatore al blocco di controllo AutoIP.</span><span class="sxs-lookup"><span data-stu-id="da8cf-217">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="da8cf-218">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="da8cf-218">Return Values</span></span>

- <span data-ttu-id="da8cf-219">**NX_SUCCESS**: (0x00) AutoIP arrestati correttamente.</span><span class="sxs-lookup"><span data-stu-id="da8cf-219">**NX_SUCCESS**: (0x00) Successful AutoIP stop.</span></span>
- <span data-ttu-id="da8cf-220">**NX_AUTO_IP_ERROR**: (0XA00) AutoIP errore irreversibile.</span><span class="sxs-lookup"><span data-stu-id="da8cf-220">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP stop error.</span></span>
- <span data-ttu-id="da8cf-221">NX_PTR_ERROR: (0x16) puntatore AutoIP non valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-221">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="da8cf-222">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="da8cf-222">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="da8cf-223">Consentito da</span><span class="sxs-lookup"><span data-stu-id="da8cf-223">Allowed From</span></span>

<span data-ttu-id="da8cf-224">Thread</span><span class="sxs-lookup"><span data-stu-id="da8cf-224">Threads</span></span>

### <a name="example"></a><span data-ttu-id="da8cf-225">Esempio</span><span class="sxs-lookup"><span data-stu-id="da8cf-225">Example</span></span>

```c
/* Stop the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_stop(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully stopped. */
```

### <a name="see-also"></a><span data-ttu-id="da8cf-226">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="da8cf-226">See Also</span></span>

<span data-ttu-id="da8cf-227">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_start</span><span class="sxs-lookup"><span data-stu-id="da8cf-227">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_start</span></span>