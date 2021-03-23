---
title: Capitolo 3-Descrizione dei servizi client di Azure RTO NetX Duo SNTP
description: Questo capitolo contiene una descrizione di tutti i servizi client NetX Duo SNTP (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 75b2b878cd084ca1c1cdd1eed4333d303fe32ad6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821650"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-sntp-client-services"></a><span data-ttu-id="aed9a-103">Capitolo 3-Descrizione dei servizi client di Azure RTO NetX Duo SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-103">Chapter 3 - Description of Azure RTOS NetX Duo SNTP Client Services</span></span>

<span data-ttu-id="aed9a-104">Questo capitolo contiene una descrizione di tutti i servizi client di Azure RTO NetX Duo SNTP (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="aed9a-104">This chapter contains a description of all Azure RTOS NetX Duo SNTP Client services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="aed9a-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="aed9a-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="aed9a-106">**nx_sntp_client_create**: *creare il client SNTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-106">**nx_sntp_client_create**: *Create the SNTP Client*</span></span>
- <span data-ttu-id="aed9a-107">**nx_sntp_client_delete**: *eliminare il client SNTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-107">**nx_sntp_client_delete**: *Delete the SNTP Client*</span></span>
- <span data-ttu-id="aed9a-108">**nx_sntp_client_get_local_time**: *ottenere l'ora locale del client SNTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-108">**nx_sntp_client_get_local_time**: *Get SNTP Client local time*</span></span>
- <span data-ttu-id="aed9a-109">**nx_sntp_client_get_local_time_extended**: *ottenere l'ora locale del client SNTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-109">**nx_sntp_client_get_local_time_extended**: *Get SNTP Client local time*</span></span>
- <span data-ttu-id="aed9a-110">**nx_sntp_client_initialize_broadcast**: *inizializzare il client per l'operazione di broadcast IPv4*</span><span class="sxs-lookup"><span data-stu-id="aed9a-110">**nx_sntp_client_initialize_broadcast**: *Initialize Client for IPv4 broadcast operation*</span></span>
- <span data-ttu-id="aed9a-111">**nxd_sntp_client_initialize_broadcast**: *inizializzare il client per l'operazione di broadcast IPv6 o IPv4*</span><span class="sxs-lookup"><span data-stu-id="aed9a-111">**nxd_sntp_client_initialize_broadcast**: *Initialize Client for IPv6 or IPv4 broadcast operation*</span></span>
- <span data-ttu-id="aed9a-112">**nx_sntp_client_initialize_unicast**: *inizializzare il client per l'operazione unicast IPv4*</span><span class="sxs-lookup"><span data-stu-id="aed9a-112">**nx_sntp_client_initialize_unicast**: *Initialize Client for IPv4 unicast operation*</span></span>
- <span data-ttu-id="aed9a-113">**nxd_sntp_client_initialize_unicast**: *inizializzare il client per l'operazione unicast IPv4 o IPv6*</span><span class="sxs-lookup"><span data-stu-id="aed9a-113">**nxd_sntp_client_initialize_unicast**: *Initialize Client for IPv4 or IPv6 unicast operation*</span></span>
- <span data-ttu-id="aed9a-114">**nx_sntp_client_receiving_udpates**: il *client sta attualmente ricevendo aggiornamenti SNTP validi*</span><span class="sxs-lookup"><span data-stu-id="aed9a-114">**nx_sntp_client_receiving_udpates**: *Client is currently receiving valid SNTP updates*</span></span>
- <span data-ttu-id="aed9a-115">**nx_sntp_client_request_unicast_time**: *inviare una richiesta unicast direttamente al server NTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-115">**nx_sntp_client_request_unicast_time**: *Send a unicast request directly to the NTP Server*</span></span>
- <span data-ttu-id="aed9a-116">**nx_sntp_client_run_broadcast**: *eseguire il client in modalità broadcast*</span><span class="sxs-lookup"><span data-stu-id="aed9a-116">**nx_sntp_client_run_broadcast**: *Run the Client in broadcast mode*</span></span>
- <span data-ttu-id="aed9a-117">**nx_sntp_client_run_unicast**: *eseguire il client in modalità unicast*</span><span class="sxs-lookup"><span data-stu-id="aed9a-117">**nx_sntp_client_run_unicast**: *Run the Client in unicast mode*</span></span>
- <span data-ttu-id="aed9a-118">**nx_sntp_client_set_local_time**: *impostare l'ora locale iniziale del client SNTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-118">**nx_sntp_client_set_local_time**: *Set SNTP Client initial local time*</span></span>
- <span data-ttu-id="aed9a-119">**nx_sntp_client_set_time_update_notify**: *impostare il callback di aggiornamento SNTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-119">**nx_sntp_client_set_time_update_notify**: *Set the SNTP update callback*</span></span>
- <span data-ttu-id="aed9a-120">**nx_sntp_client_stop**: *arrestare il thread del client SNTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-120">**nx_sntp_client_stop**: *Stop the SNTP Client thread*</span></span>
- <span data-ttu-id="aed9a-121">**nx_sntp_client_utility_display_date_and_time**: *Visualizza tempo NTP in secondi*</span><span class="sxs-lookup"><span data-stu-id="aed9a-121">**nx_sntp_client_utility_display_date_and_time**: *Display NTP time in seconds*</span></span>
- <span data-ttu-id="aed9a-122">**nx_sntp_client_utility_msecs_to_fraction**: *convertire i millisecondi in un componente della frazione NTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-122">**nx_sntp_client_utility_msecs_to_fraction**: *Convert milliseconds to an NTP fraction component*</span></span>
- <span data-ttu-id="aed9a-123">**nx_sntp_client_utility_usecs_to_fraction**: *convertire i microsecondi in un componente della frazione NTP*</span><span class="sxs-lookup"><span data-stu-id="aed9a-123">**nx_sntp_client_utility_usecs_to_fraction**: *Convert microseconds to an NTP fraction component*</span></span>
- <span data-ttu-id="aed9a-124">**nx_sntp_client_utility_fraction_to_usecs**: *conversione di un componente della frazione NTP in microsecondi*</span><span class="sxs-lookup"><span data-stu-id="aed9a-124">**nx_sntp_client_utility_fraction_to_usecs**: *Convert an NTP fraction component to microseconds*</span></span>


## <a name="nx_sntp_client_create"></a><span data-ttu-id="aed9a-125">nx_sntp_client_create</span><span class="sxs-lookup"><span data-stu-id="aed9a-125">nx_sntp_client_create</span></span>

<span data-ttu-id="aed9a-126">Creare un client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-126">Create an SNTP Client</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-127">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-127">Prototype</span></span>

```C
UINT nx_sntp_client_create(NX_SNTP_CLIENT *client_ptr, NX_IP *ip_ptr,  
                                     UINT iface_index, 
                                     NX_PACKET_POOL *packet_pool_ptr, 
UINT (*leap_second_handler)(NX_SNTP_CLIENT *client_ptr, 
                                        UINT indicator), 
UINT (*kiss_of_death_handler)(NX_SNTP_CLIENT *client_ptr, 
                               NX_SNTP_TIME_MESSAGE *server_time_msg),
VOID (random_number_generator)(struct NX_SNTP_CLIENT_STRUCT 
                                *client_ptr, ULONG *rand));

```

### <a name="description"></a><span data-ttu-id="aed9a-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-128">Description</span></span>

<span data-ttu-id="aed9a-129">Questo servizio crea un'istanza del client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-129">This service creates an SNTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-130">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-130">Input Parameters</span></span>

- <span data-ttu-id="aed9a-131">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-131">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-132">**ip_ptr** Puntatore a istanza IP client</span><span class="sxs-lookup"><span data-stu-id="aed9a-132">**ip_ptr** Pointer to Client IP instance</span></span>

- <span data-ttu-id="aed9a-133">**iface_index** Indice per l'interfaccia di rete SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-133">**iface_index** Index to SNTP network interface</span></span>

- <span data-ttu-id="aed9a-134">**packet_pool_ptr** Puntatore al pool di pacchetti client</span><span class="sxs-lookup"><span data-stu-id="aed9a-134">**packet_pool_ptr** Pointer to Client packet pool</span></span>

- <span data-ttu-id="aed9a-135">**leap_second_handler** Callback per la risposta dell'applicazione al secondo intercalare imminente</span><span class="sxs-lookup"><span data-stu-id="aed9a-135">**leap_second_handler** Callback for application response to impending leap second</span></span>

- <span data-ttu-id="aed9a-136">**kiss_of_death_handler** Callback per la risposta dell'applicazione a ricevere il bacio del pacchetto di morte</span><span class="sxs-lookup"><span data-stu-id="aed9a-136">**kiss_of_death_handler** Callback for application response to receiving Kiss of Death packet</span></span>

- <span data-ttu-id="aed9a-137">**random_number_generator** Callback a servizio Generatore di numeri casuali</span><span class="sxs-lookup"><span data-stu-id="aed9a-137">**random_number_generator** Callback to random number generator service</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-138">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-138">Return Values</span></span>

- <span data-ttu-id="aed9a-139">Creazione client riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="aed9a-139">**NX_SUCCESS** (0x00) Successful Client creation</span></span>

- <span data-ttu-id="aed9a-140">**NX_SNTP_INSUFFICIENT_PACKET_PAYLOAD** (0xD2A) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-140">**NX_SNTP_INSUFFICIENT_PACKET_PAYLOAD** (0xD2A) Invalid non pointer input</span></span>

- <span data-ttu-id="aed9a-141">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-141">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-142">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="aed9a-142">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-143">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-143">Allowed From</span></span>

<span data-ttu-id="aed9a-144">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-144">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-145">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-145">Example</span></span>

```C
/* Create the SNTP Client on the primary interface. */
UINT iface_index = 0;
status =  nx_sntp_client_create(&demo_client, 
                     iface_index, &client_ip, 
&client_packet_pool, leap_second_handler, 
                    kiss_of_death_handler, 
NULL /* no random_number_generator callback */);

/* If status is NX_SUCCESS an SNTP Client instance was successfully
   created.  */

```

## <a name="nx_sntp_client_delete"></a><span data-ttu-id="aed9a-146">nx_sntp_client_delete</span><span class="sxs-lookup"><span data-stu-id="aed9a-146">nx_sntp_client_delete</span></span>

<span data-ttu-id="aed9a-147">Eliminare un client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-147">Delete an SNTP Client</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-148">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-148">Prototype</span></span>

```C
UINT nx_sntp_client_delete(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="aed9a-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-149">Description</span></span>

<span data-ttu-id="aed9a-150">Questo servizio Elimina un'istanza del client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-150">This service deletes an SNTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-151">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-151">Input Parameters</span></span>

- <span data-ttu-id="aed9a-152">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-152">**client_ptr** Pointer to SNTP Client control block</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-153">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-153">Return Values</span></span>

- <span data-ttu-id="aed9a-154">Creazione client riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="aed9a-154">**NX_SUCCESS** (0x00) Successful Client creation</span></span>

- <span data-ttu-id="aed9a-155">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-155">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-156">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-156">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-157">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-157">Allowed From</span></span>

<span data-ttu-id="aed9a-158">Thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-158">Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-159">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-159">Example</span></span>

```C
/* Delete the SNTP Client. */
status =  nx_sntp_client_delete(&demo_client);

/* If status is NX_SUCCESS an SNTP Client 
   instance was successfully deleted.  */

```

## <a name="nx_sntp_client_get_local_time"></a><span data-ttu-id="aed9a-160">nx_sntp_client_get_local_time</span><span class="sxs-lookup"><span data-stu-id="aed9a-160">nx_sntp_client_get_local_time</span></span>

<span data-ttu-id="aed9a-161">Ottenere l'ora locale del client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-161">Get the SNTP Client local time</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-162">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-162">Prototype</span></span>

```C
UINT nx_sntp_client_get_local_time(NX_SNTP_CLIENT *client_ptr , 
                                                ULONG *seconds, 
                                                ULONG *fraction, 
                                                CHAR *buffer);

```

### <a name="description"></a><span data-ttu-id="aed9a-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-163">Description</span></span>

<span data-ttu-id="aed9a-164">Questo servizio ottiene l'ora locale del client SNTP con un input del puntatore del buffer dell'opzione per ricevere i dati nel formato del messaggio stringa.</span><span class="sxs-lookup"><span data-stu-id="aed9a-164">This service gets the SNTP Client local time with an option buffer pointer input to receive the data in string message format.</span></span>

<span data-ttu-id="aed9a-165">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="aed9a-165">This service is deprecated.</span></span> <span data-ttu-id="aed9a-166">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_sntp_client_get_local_time_extended*().</span><span class="sxs-lookup"><span data-stu-id="aed9a-166">Developers are encouraged to migrate to *nx_sntp_client_get_local_time_extended*().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-167">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-167">Input Parameters</span></span>

- <span data-ttu-id="aed9a-168">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-168">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-169">**secondi** Puntatore ai secondi dell'ora locale</span><span class="sxs-lookup"><span data-stu-id="aed9a-169">**seconds** Pointer to local time seconds</span></span>

- <span data-ttu-id="aed9a-170">**frazione** di Componente frazione ora locale</span><span class="sxs-lookup"><span data-stu-id="aed9a-170">**fraction** Local time fraction component</span></span>

- <span data-ttu-id="aed9a-171">**buffer** Puntatore al buffer per scrivere i dati relativi all'ora</span><span class="sxs-lookup"><span data-stu-id="aed9a-171">**buffer** Pointer to buffer to write time data</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-172">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-172">Return Values</span></span>

- <span data-ttu-id="aed9a-173">Creazione client riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="aed9a-173">**NX_SUCCESS** (0x00) Successful Client creation</span></span>

- <span data-ttu-id="aed9a-174">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-174">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-175">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-175">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-176">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-176">Allowed From</span></span>

<span data-ttu-id="aed9a-177">Thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-177">Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-178">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-178">Example</span></span>

```C
/* Get the SNTP Client local time without the 
   string message option. */

ULONG base_seconds;
ULONG base_fraction;

status =  nx_sntp_client_get_local_time(&demo_client, 
                                       &base_seconds, 
                                       &base_fraction, 
                                       NX_NULL);
/* If status is NX_SUCCESS an SNTP Client time was successfully
   retrieved.  */

```

## <a name="nx_sntp_client_get_local_time_extended"></a><span data-ttu-id="aed9a-179">nx_sntp_client_get_local_time_extended</span><span class="sxs-lookup"><span data-stu-id="aed9a-179">nx_sntp_client_get_local_time_extended</span></span>

<span data-ttu-id="aed9a-180">Ottenere l'ora locale del client SNTP esteso</span><span class="sxs-lookup"><span data-stu-id="aed9a-180">Get the extended SNTP Client local time</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-181">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-181">Prototype</span></span>

```C
UINT nx_sntp_client_get_local_time_extended(
                 NX_SNTP_CLIENT *client_ptr,
                 ULONG *seconds, 
                 ULONG *fraction, 
                 CHAR *buffer
                 UINT buffer_size);

```

### <a name="description"></a><span data-ttu-id="aed9a-182">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-182">Description</span></span>

<span data-ttu-id="aed9a-183">Questo servizio ottiene l'ora locale del client SNTP esteso con un input del puntatore del buffer dell'opzione per ricevere i dati nel formato del messaggio stringa.</span><span class="sxs-lookup"><span data-stu-id="aed9a-183">This service gets the extended SNTP Client local time with an option buffer pointer input to receive the data in string message format.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-184">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-184">Input Parameters</span></span>

- <span data-ttu-id="aed9a-185">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-185">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-186">**secondi** Puntatore ai secondi dell'ora locale</span><span class="sxs-lookup"><span data-stu-id="aed9a-186">**seconds** Pointer to local time seconds</span></span>

- <span data-ttu-id="aed9a-187">**frazione** di Puntatore a componente frazione</span><span class="sxs-lookup"><span data-stu-id="aed9a-187">**fraction** Pointer to fraction component</span></span>

- <span data-ttu-id="aed9a-188">**buffer** Puntatore al buffer per scrivere i dati relativi all'ora</span><span class="sxs-lookup"><span data-stu-id="aed9a-188">**buffer** Pointer to buffer to write time data</span></span>

- <span data-ttu-id="aed9a-189">**BUFFER_SIZE** Lunghezza del buffer</span><span class="sxs-lookup"><span data-stu-id="aed9a-189">**buffer_size** Length of buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-190">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-190">Return Values</span></span>

- <span data-ttu-id="aed9a-191">Creazione client riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="aed9a-191">**NX_SUCCESS** (0x00) Successful Client creation</span></span>

- <span data-ttu-id="aed9a-192">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-192">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-193">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-193">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

- <span data-ttu-id="aed9a-194">Controllo NX_SIZE_ERROR (0x09) buffer_size esito negativo</span><span class="sxs-lookup"><span data-stu-id="aed9a-194">NX_SIZE_ERROR (0x09) Check buffer_size fail</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-195">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-195">Allowed From</span></span>

<span data-ttu-id="aed9a-196">Thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-196">Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-197">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-197">Example</span></span>

```C
/* Get the SNTP Client local time without the 
   string message option. */

#define BUFSIZE 50

ULONG seconds;
ULONG fraction;
CHAR  buffer[BUFSIZE];

status =  nx_sntp_client_get_local_time_extended(&demo_client, 
                                                &seconds, 
                                                &fraction, 
                                                buffer, 
                                                BUFSIZE);

/* If status is NX_SUCCESS an SNTP Client 
   time was successfully retrieved.  */

```

## <a name="nx_sntp_client_initialize_broadcast"></a><span data-ttu-id="aed9a-198">nx_sntp_client_initialize_broadcast</span><span class="sxs-lookup"><span data-stu-id="aed9a-198">nx_sntp_client_initialize_broadcast</span></span>

<span data-ttu-id="aed9a-199">Inizializzare il client per l'operazione di broadcast</span><span class="sxs-lookup"><span data-stu-id="aed9a-199">Initialize the Client for broadcast operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-200">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-200">Prototype</span></span>

```C
UINT nx_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                                    ULONG multicast_server_address, 
                                    ULONG broadcast_time_servers);


```

### <a name="description"></a><span data-ttu-id="aed9a-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-201">Description</span></span>

<span data-ttu-id="aed9a-202">Questo servizio Inizializza il client per l'operazione di broadcast impostando l'indirizzo IP del server SNTP e inizializzando i parametri di avvio e i timeout di SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-202">This service initializes the Client for broadcast operation by setting the the SNTP Server IP address and initializing SNTP startup parameters and timeouts.</span></span> <span data-ttu-id="aed9a-203">Se gli indirizzi multicast e broadcast sono diversi da null, viene selezionato l'indirizzo multicast.</span><span class="sxs-lookup"><span data-stu-id="aed9a-203">If both multicast and broadcast addresses are non-null, the multicast address is selected.</span></span> <span data-ttu-id="aed9a-204">Se entrambi gli indirizzi sono null, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="aed9a-204">If both addresses are null an error is returned.</span></span> <span data-ttu-id="aed9a-205">Si noti che questo supporta solo indirizzi server IPv4.</span><span class="sxs-lookup"><span data-stu-id="aed9a-205">Note this supports IPv4 server addresses only.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-206">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-206">Input Parameters</span></span>

- <span data-ttu-id="aed9a-207">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-207">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-208">**multicast_server_address** Indirizzo multicast di SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-208">**multicast_server_address** SNTP multicast address</span></span>

- <span data-ttu-id="aed9a-209">**broadcast_time_server** Indirizzo di broadcast del server SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-209">**broadcast_time_server** SNTP server broadcast address</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-210">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-210">Return Values</span></span>

- <span data-ttu-id="aed9a-211">Creazione client riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="aed9a-211">**NX_SUCCESS** (0x00) Successful Client Creation</span></span>

- <span data-ttu-id="aed9a-212">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-212">**NX_INVALID_PARAMETERS** (0x4D) Invalid non pointer input</span></span>

- <span data-ttu-id="aed9a-213">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-213">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-214">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-214">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-215">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-215">Allowed From</span></span>

<span data-ttu-id="aed9a-216">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-216">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-217">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-217">Example</span></span>

```C
/* Initialize the client for broadcast operation.  */
status =  nx_sntp_client_initialize_broadcast(client_ptr,0x0,
                            NX_NULL, IP_ADDRESS(192,2,2,255);

/* If status is NX_SUCCESS the Client 
   was successfully initialized.  */

```

## <a name="nxd_sntp_client_initialize_broadcast"></a><span data-ttu-id="aed9a-218">nxd_sntp_client_initialize_broadcast</span><span class="sxs-lookup"><span data-stu-id="aed9a-218">nxd_sntp_client_initialize_broadcast</span></span>

<span data-ttu-id="aed9a-219">Inizializzare il client per l'operazione di trasmissione IPv4 o IPv6</span><span class="sxs-lookup"><span data-stu-id="aed9a-219">Initialize the Client for IPv4 or IPv6 broadcast operation</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-220">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-220">Prototype</span></span>

```C
UINT nxd_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                            NXD_ADDRESS *multicast_server_address, 
                            NXD_ADDRESS *broadcast_server_address);

```

### <a name="description"></a><span data-ttu-id="aed9a-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-221">Description</span></span>

<span data-ttu-id="aed9a-222">Questo servizio Inizializza il client per l'operazione di broadcast impostando l'indirizzo IP del server SNTP e inizializzando i parametri di avvio e i timeout di SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-222">This service initializes the Client for broadcast operation by setting up the SNTP Server IP address and initializing SNTP startup parameters and timeouts.</span></span> <span data-ttu-id="aed9a-223">Se i puntatori di trasmissione e di indirizzo multicast sono diversi da null, viene selezionato l'indirizzo multicast.</span><span class="sxs-lookup"><span data-stu-id="aed9a-223">If both broadcast and multicast address pointers are non null, the multicast address is selected.</span></span> <span data-ttu-id="aed9a-224">Se entrambi i puntatori di indirizzo sono null, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="aed9a-224">If both address pointers are null, an error is returned.</span></span> <span data-ttu-id="aed9a-225">Sono supportati i tipi di indirizzi sia IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="aed9a-225">This supports both IPv4 and IPv6 address types.</span></span> <span data-ttu-id="aed9a-226">Si noti che IPv6 non supporta la trasmissione, quindi il puntatore all'indirizzo di trasmissione è impostato su IPv6, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="aed9a-226">Note that IPv6 does not support broadcast, so the broadcast address pointer is set to IPv6, an error is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-227">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-227">Input Parameters</span></span>

- <span data-ttu-id="aed9a-228">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-228">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-229">**multicast_server_address** Indirizzo multicast del server SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-229">**multicast_server_address** SNTP server multicast address</span></span>

- <span data-ttu-id="aed9a-230">**broadcast_server_address** Indirizzo di broadcast del server SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-230">**broadcast_server_address** SNTP server broadcast address</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-231">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-231">Return Values</span></span>

- <span data-ttu-id="aed9a-232">Inizializzazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="aed9a-232">**NX_SUCCESS** (0x00) Client successfully initialized</span></span>

- <span data-ttu-id="aed9a-233">NX_SNTP_PARAM_ERROR (0xD0D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-233">NX_SNTP_PARAM_ERROR (0xD0D) Invalid non pointer input</span></span>

- <span data-ttu-id="aed9a-234">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-234">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-235">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-235">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>


### <a name="allowed-from"></a><span data-ttu-id="aed9a-236">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-236">Allowed From</span></span>

<span data-ttu-id="aed9a-237">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-237">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-238">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-238">Example</span></span>

```C
/* Initialize the client for broadcast operation.  */
NXD_ADDRESS broadcast_server;

Broadcast_server.nxd_ip_address = NX_IP_VERSION_V6;
Broadcast_server.nxd_ip_address.v6[0] = 0x20010db1;
Broadcast_server.nxd_ip_address.v6[1] = 0x0f101;
Broadcast_server.nxd_ip_address.v6[2] = 0x0;
Broadcast_server.nxd_ip_address.v6[3] = 0x101;

status =  nxd_sntp_client_initialize_broadcast(client_ptr,0x0,
                                  NX_NULL, &broadcast_server)


/* If status is NX_SUCCESS the Client 
   was successfully initialized.  */

```

## <a name="nx_sntp_client_initialize_unicast"></a><span data-ttu-id="aed9a-239">nx_sntp_client_initialize_unicast</span><span class="sxs-lookup"><span data-stu-id="aed9a-239">nx_sntp_client_initialize_unicast</span></span>

<span data-ttu-id="aed9a-240">Configurare il client di SNTP per l'esecuzione in unicast</span><span class="sxs-lookup"><span data-stu-id="aed9a-240">Set up the SNTP Client to run in unicast</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-241">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-241">Prototype</span></span>

```C
UINT nx_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                        ULONG unicast_time_server);

```
### <a name="description"></a><span data-ttu-id="aed9a-242">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-242">Description</span></span>

<span data-ttu-id="aed9a-243">Questo servizio Inizializza il client per l'operazione unicast impostando l'indirizzo IP del server SNTP e inizializzando i parametri di avvio e i timeout di SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-243">This service initializes the Client for unicast operation by setting the SNTP Server IP address and initializing SNTP startup parameters and timeouts.</span></span> <span data-ttu-id="aed9a-244">Si noti che questo supporta solo indirizzi server IPv4.</span><span class="sxs-lookup"><span data-stu-id="aed9a-244">Note this supports IPv4 server addresses only.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-245">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-245">Input Parameters</span></span>

- <span data-ttu-id="aed9a-246">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-246">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-247">**unicast_time_server** Indirizzo IP del server SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-247">**unicast_time_server** SNTP server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-248">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-248">Return Values</span></span>

- <span data-ttu-id="aed9a-249">Inizializzazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="aed9a-249">**NX_SUCCESS** (0x00) Client successfully initialized</span></span>

- <span data-ttu-id="aed9a-250">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-250">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

- <span data-ttu-id="aed9a-251">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-251">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-252">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-252">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-253">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-253">Allowed From</span></span>

<span data-ttu-id="aed9a-254">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-254">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-255">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-255">Example</span></span>

```C
/* Initialize the Client for unicast operation.  */
status =  nx_sntp_client_initialize_unicast(&client_ptr, 
                                 IP_ADDRESS(192,2,2,1));


/* If status is NX_SUCCESS the Client 
   is initialized for unicast operation.  */

```


## <a name="nxd_sntp_client_initialize_unicast"></a><span data-ttu-id="aed9a-256">nxd_sntp_client_initialize_unicast</span><span class="sxs-lookup"><span data-stu-id="aed9a-256">nxd_sntp_client_initialize_unicast</span></span>

<span data-ttu-id="aed9a-257">Configurare il client di SNTP per l'esecuzione in unicast IPv4 o IPv6</span><span class="sxs-lookup"><span data-stu-id="aed9a-257">Set up the SNTP Client to run in IPv4 or IPv6 unicast</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-258">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-258">Prototype</span></span>

```C
UINT nxd_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                  NXD_ADDRESS *unicast_time_server);

```

### <a name="description"></a><span data-ttu-id="aed9a-259">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-259">Description</span></span>

<span data-ttu-id="aed9a-260">Questo servizio Inizializza il client per l'operazione unicast impostando l'indirizzo IP del server SNTP e inizializzando i parametri di avvio e i timeout di SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-260">This service initializes the Client for unicast operation by setting up the SNTP Server IP address and initializing SNTP startup parameters and timeouts.</span></span> <span data-ttu-id="aed9a-261">Sono supportati i tipi di indirizzi sia IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="aed9a-261">This supports both IPv4 and IPv6 address types.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-262">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-262">Input Parameters</span></span>

- <span data-ttu-id="aed9a-263">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-263">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-264">**unicast_time_server** Indirizzo IP del server SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-264">**unicast_time_server** SNTP server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-265">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-265">Return Values</span></span>

- <span data-ttu-id="aed9a-266">Inizializzazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="aed9a-266">**NX_SUCCESS** (0x00) Client successfully initialized</span></span>

- <span data-ttu-id="aed9a-267">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-267">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

- <span data-ttu-id="aed9a-268">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-268">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-269">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-269">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-270">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-270">Allowed From</span></span>

<span data-ttu-id="aed9a-271">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-271">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-272">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-272">Example</span></span>

```C
/* Initialize the Client for unicast operation.  */
NXD_ADDRESS unicast_server;

unicast _server.nxd_ip_address = NX_IP_VERSION_V6;
unicast _server.nxd_ip_address.v6[0] = 0x20010db1;
unicast _server.nxd_ip_address.v6[1] = 0x0f101;
unicast _server.nxd_ip_address.v6[2] = 0x0;
unicast _server.nxd_ip_address.v6[3] = 0x101;

status =  nxd_sntp_client_initialize_unicast(&client_ptr, 
                                        *unicast_server); 


/* If status is NX_SUCCESS the Client 
   is initialized for unicast operation.  */

```

## <a name="nx_sntp_client_receiving_updates"></a><span data-ttu-id="aed9a-273">nx_sntp_client_receiving_updates</span><span class="sxs-lookup"><span data-stu-id="aed9a-273">nx_sntp_client_receiving_updates</span></span>

<span data-ttu-id="aed9a-274">Indica se il client riceve aggiornamenti validi</span><span class="sxs-lookup"><span data-stu-id="aed9a-274">Indicate if Client is receiving valid updates</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-275">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-275">Prototype</span></span>

```C
UINT nx_sntp_client_receiving_updates(NX_SNTP_CLIENT *client_ptr, 
                                           UINT *receive_status);

```

### <a name="description"></a><span data-ttu-id="aed9a-276">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-276">Description</span></span>

<span data-ttu-id="aed9a-277">Questo servizio indica se il client riceve aggiornamenti SNTP validi.</span><span class="sxs-lookup"><span data-stu-id="aed9a-277">This service indicates if the Client is receiving valid SNTP updates.</span></span> <span data-ttu-id="aed9a-278">Se viene superato il lasso di tempo massimo senza un aggiornamento o un limite valido per gli aggiornamenti consecutivi non validi, lo stato di ricezione viene restituito come false.</span><span class="sxs-lookup"><span data-stu-id="aed9a-278">If the maximum time lapse without a valid update or limit on consecutive invalid updates is exceeded, the receive status is returned as false.</span></span> <span data-ttu-id="aed9a-279">Si noti che il client SNTP è ancora in esecuzione e, se l'applicazione vuole riavviare il client di SNTP con un altro server unicast o broadcast/multicast, deve arrestare il client SNTP usando il servizio *nx_sntp_client_stop* , reinizializzare il client usando uno dei servizi di inizializzazione con un altro server.</span><span class="sxs-lookup"><span data-stu-id="aed9a-279">Note that the SNTP Client is still running and if the application wishes to restart the SNTP Client with another unicast or broadcast/multicast server it must stop the SNTP Client using the *nx_sntp_client_stop* service, reinitialize the Client using one of the initialize services with another server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-280">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-280">Input Parameters</span></span>

- <span data-ttu-id="aed9a-281">**client_ptr** Puntatore al blocco di controllo client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-281">**client_ptr** Pointer to SNTP Client control block.</span></span>

- <span data-ttu-id="aed9a-282">**receive_status** Puntatore a indicatore se il client riceve aggiornamenti validi.</span><span class="sxs-lookup"><span data-stu-id="aed9a-282">**receive_status** Pointer to indicator if Client is receiving valid updates.</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-283">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-283">Return Values</span></span>

- <span data-ttu-id="aed9a-284">Il client **NX_SUCCESS** (0x00) ha ricevuto correttamente lo stato di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="aed9a-284">**NX_SUCCESS** (0x00) Client successfully received update status</span></span>

- <span data-ttu-id="aed9a-285">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-285">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-286">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-286">Allowed From</span></span>

<span data-ttu-id="aed9a-287">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-287">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-288">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-288">Example</span></span>

```C
/* Determine if the SNTP Client is receiving valid udpates.  */
UINT receive_status;

status =  nx_sntp_client_receiving_updates(client_ptr, 
                                     &receive_status);

/* If status is NX_SUCCESS and receive_status is NX_TRUE, 
   the client is currently receiving valid updates.  */

```

## <a name="nx_sntp_client_request_unicast_time"></a><span data-ttu-id="aed9a-289">nx_sntp_client_request_unicast_time</span><span class="sxs-lookup"><span data-stu-id="aed9a-289">nx_sntp_client_request_unicast_time</span></span>

<span data-ttu-id="aed9a-290">Inviare una richiesta unicast direttamente al server NTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-290">Send a unicast request directly to the NTP Server</span></span>


### <a name="prototype"></a><span data-ttu-id="aed9a-291">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-291">Prototype</span></span>

```C
UINT nx_sntp_client_request_unicast_time(NX_SNTP_CLIENT *client_ptr, 
                                                  UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="aed9a-292">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-292">Description</span></span>

<span data-ttu-id="aed9a-293">Questo servizio consente all'applicazione di inviare direttamente una richiesta unicast al server NTP in modo asincrono dall'attività thread del client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-293">This service allows the application to directly send a unicast request to the NTP server asynchronously from the SNTP Client thread task.</span></span> <span data-ttu-id="aed9a-294">L'opzione wait specifica il tempo di attesa di una risposta.</span><span class="sxs-lookup"><span data-stu-id="aed9a-294">The wait option specifies how long to wait for a response.</span></span> <span data-ttu-id="aed9a-295">In caso di esito positivo, l'applicazione può usare altri servizi client di SNTP per ottenere l'ora più recente.</span><span class="sxs-lookup"><span data-stu-id="aed9a-295">If successful, the application can use other SNTP Client services to obtain the latest time.</span></span> <span data-ttu-id="aed9a-296">Per altri dettagli, vedere la sezione relativa alle **richieste unicast asincrone di SNTP** .</span><span class="sxs-lookup"><span data-stu-id="aed9a-296">See section **SNTP Asynchronous Unicast Requests** for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-297">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-297">Input Parameters</span></span>

- <span data-ttu-id="aed9a-298">**client_ptr** Puntatore al blocco di controllo client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-298">**client_ptr** Pointer to SNTP Client control block.</span></span>

- <span data-ttu-id="aed9a-299">**Wait_option** Opzione wait per la risposta NTP nei cicli del timer.</span><span class="sxs-lookup"><span data-stu-id="aed9a-299">**Wait_option** Wait option for NTP response in timer ticks.</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-300">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-300">Return Values</span></span>

- <span data-ttu-id="aed9a-301">Il client **NX_SUCCESS** (0x00) Invia e riceve correttamente l'aggiornamento unicast</span><span class="sxs-lookup"><span data-stu-id="aed9a-301">**NX_SUCCESS** (0x00) Client successfully sends and receives unicast update</span></span>

- <span data-ttu-id="aed9a-302">Thread client di **NX_SNTP_CLIENT_NOT_STARTED** (0xD0B) non avviato</span><span class="sxs-lookup"><span data-stu-id="aed9a-302">**NX_SNTP_CLIENT_NOT_STARTED** (0xD0B) Client thread not started</span></span>

- <span data-ttu-id="aed9a-303">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-303">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-304">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-304">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-305">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-305">Allowed From</span></span>

<span data-ttu-id="aed9a-306">Thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-306">Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-307">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-307">Example</span></span>

```C
/* Determine if the SNTP Client is receiving valid udpates.  */
UINT receive_status;

status =  nx_sntp_client_request_unicast_time(client_ptr, 400);

/* If status is NX_SUCCESS and receive_status is NX_TRUE, 
   the client is received a valid response to the unicast request.  */

```

## <a name="nx_sntp_client_run_broadcast"></a><span data-ttu-id="aed9a-308">nx_sntp_client_run_broadcast</span><span class="sxs-lookup"><span data-stu-id="aed9a-308">nx_sntp_client_run_broadcast</span></span>

<span data-ttu-id="aed9a-309">Eseguire il client in modalità broadcast</span><span class="sxs-lookup"><span data-stu-id="aed9a-309">Run the Client in broadcast mode</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-310">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-310">Prototype</span></span>

```C
UINT nx_sntp_client_run_broadcast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="aed9a-311">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-311">Description</span></span>

<span data-ttu-id="aed9a-312">Questo servizio avvia il client in modalità broadcast in cui attenderà la ricezione delle trasmissioni dal server SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-312">This service starts the Client in broadcast mode where it will wait to receive broadcasts from the SNTP server.</span></span> <span data-ttu-id="aed9a-313">Se viene ricevuto un messaggio SNTP broadcast valido, viene reimpostato il timeout del client SNTP per la scadenza massima senza aggiornamento e il numero di messaggi non validi consecutivi ricevuti.</span><span class="sxs-lookup"><span data-stu-id="aed9a-313">If a valid broadcast SNTP message is received, the SNTP client timeout for maximum lapse without an update and count of consecutive invalid messages received are reset.</span></span> <span data-ttu-id="aed9a-314">Se viene superato uno di questi limiti, il client di SNTP imposta lo stato del server su non valido anche se continuerà ad attendere la ricezione degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="aed9a-314">If the either of these limits are exceeded, the SNTP Client sets the server status to invalid although it will still wait to receive updates.</span></span> <span data-ttu-id="aed9a-315">L'applicazione può eseguire il polling dell'attività client SNTP per lo stato del server e, se non è valido, arrestare il client SNTP e reinizializzarlo con un altro indirizzo di broadcast SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-315">The application can poll the SNTP Client task for server status, and if invalid stop the SNTP Client and reinitialize it with another SNTP broadcast address.</span></span> <span data-ttu-id="aed9a-316">Può anche passare a un server SNTP unicast.</span><span class="sxs-lookup"><span data-stu-id="aed9a-316">It can also switch to a unicast SNTP server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-317">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-317">Input Parameters</span></span>

- <span data-ttu-id="aed9a-318">**client_ptr** Puntatore al blocco di controllo client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-318">**client_ptr** Pointer to SNTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-319">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-319">Return Values</span></span>

- <span data-ttu-id="aed9a-320">**stato** --------stato di completamento effettivo</span><span class="sxs-lookup"><span data-stu-id="aed9a-320">**status** -------- Actual completion status</span></span>

- <span data-ttu-id="aed9a-321">Client **NX_SNTP_CLIENT_ALREADY_STARTED** (0xD0C) già avviato</span><span class="sxs-lookup"><span data-stu-id="aed9a-321">**NX_SNTP_CLIENT_ALREADY_STARTED** (0xD0C) Client already started</span></span>

- <span data-ttu-id="aed9a-322">Client **NX_SNTP_CLIENT_NOT_INITIALIZED** (0xD01) non inizializzato</span><span class="sxs-lookup"><span data-stu-id="aed9a-322">**NX_SNTP_CLIENT_NOT_INITIALIZED** (0xD01) Client not initialized</span></span>

- <span data-ttu-id="aed9a-323">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-323">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-324">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-324">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-325">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-325">Allowed From</span></span>

<span data-ttu-id="aed9a-326">Thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-326">Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-327">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-327">Example</span></span>

```C
/* Start Client running in broadcast mode.  */
status =  nx_sntp_client_run_broadcast(client_ptr);

/* If status is NX_SUCCESS, the client is successfully started.  */

```

## <a name="nx_sntp_client_run_unicast"></a><span data-ttu-id="aed9a-328">nx_sntp_client_run_unicast</span><span class="sxs-lookup"><span data-stu-id="aed9a-328">nx_sntp_client_run_unicast</span></span>

<span data-ttu-id="aed9a-329">Eseguire il client in modalità unicast</span><span class="sxs-lookup"><span data-stu-id="aed9a-329">Run the Client in unicast mode</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-330">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-330">Prototype</span></span>

```C
UINT nx_sntp_client_run_unicast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="aed9a-331">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-331">Description</span></span>

<span data-ttu-id="aed9a-332">Questo servizio avvia il client in modalità unicast, in cui invia periodicamente una richiesta unicast al server SNTP per un aggiornamento del tempo.</span><span class="sxs-lookup"><span data-stu-id="aed9a-332">This service starts the Client in unicast mode where it periodically sends a unicast request to its SNTP Server for a time update.</span></span> <span data-ttu-id="aed9a-333">Se viene ricevuto un messaggio SNTP valido, viene reimpostato il timeout del client SNTP per la scadenza massima senza aggiornamento, l'intervallo di polling iniziale e il numero di messaggi non validi consecutivi ricevuti.</span><span class="sxs-lookup"><span data-stu-id="aed9a-333">If a valid SNTP message is received, the SNTP client timeout for maximum lapse without an update, initial polling interval and count of consecutive invalid messages received are reset.</span></span> <span data-ttu-id="aed9a-334">Se viene superato uno di questi limiti, il client SNTP imposta lo stato del server su non valido anche se eseguirà comunque il polling e attenda la ricezione degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="aed9a-334">If the either of these limits are exceeded, the SNTP Client sets the Server status to invalid although it will still poll and wait to receive updates.</span></span> <span data-ttu-id="aed9a-335">L'applicazione può eseguire il polling dell'attività client SNTP per lo stato del server e, se non è valido, arrestare il client SNTP e reinizializzarlo con un altro indirizzo unicast SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-335">The application can poll the SNTP Client task for server status, and if invalid stop the SNTP Client and reinitialize it with another SNTP unicast address.</span></span> <span data-ttu-id="aed9a-336">Può anche passare a un server SNTP broadcast.</span><span class="sxs-lookup"><span data-stu-id="aed9a-336">It can also switch to a broadcast SNTP server.</span></span>

<span data-ttu-id="aed9a-337">.</span><span class="sxs-lookup"><span data-stu-id="aed9a-337">.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-338">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-338">Input Parameters</span></span>

- <span data-ttu-id="aed9a-339">**client_ptr** Puntatore al blocco di controllo client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-339">**client_ptr** Pointer to SNTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-340">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-340">Return Values</span></span>

- <span data-ttu-id="aed9a-341">**NX_SUCCESS** (0x00) ha avviato correttamente il client in modalità unicast</span><span class="sxs-lookup"><span data-stu-id="aed9a-341">**NX_SUCCESS** (0x00) Successfully started Client in unicast mode</span></span>

- <span data-ttu-id="aed9a-342">Client **NX_SNTP_CLIENT_ALREADY_STARTED** (0xD0C) già avviato</span><span class="sxs-lookup"><span data-stu-id="aed9a-342">**NX_SNTP_CLIENT_ALREADY_STARTED** (0xD0C) Client already started</span></span>

- <span data-ttu-id="aed9a-343">Client **NX_SNTP_CLIENT_NOT_INITIALIZED** (0xD01) non inizializzato</span><span class="sxs-lookup"><span data-stu-id="aed9a-343">**NX_SNTP_CLIENT_NOT_INITIALIZED** (0xD01) Client not initialized</span></span>

- <span data-ttu-id="aed9a-344">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-344">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="aed9a-345">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-345">NX_CALLER_ERROR (0x11) Invalid caller of service</span></span>


### <a name="allowed-from"></a><span data-ttu-id="aed9a-346">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-346">Allowed From</span></span>

<span data-ttu-id="aed9a-347">Thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-347">Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-348">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-348">Example</span></span>

```C
/* Start the Client in unicast mode. */
status =  nx_sntp_client_run_unicast(client_ptr);

/* If status = NX_SUCCESS, the Client was successfully started.  */

```

## <a name="nx_sntp_client_set_local_time"></a><span data-ttu-id="aed9a-349">nx_sntp_client_set_local_time</span><span class="sxs-lookup"><span data-stu-id="aed9a-349">nx_sntp_client_set_local_time</span></span>

<span data-ttu-id="aed9a-350">Imposta l'ora locale del client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-350">Set the SNTP Client local time</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-351">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-351">Prototype</span></span>

```C
UINT nx_sntp_client_set_local_time(NX_SNTP_CLIENT *client_ptr , 
                                ULONG seconds, ULONG fraction);

```

### <a name="description"></a><span data-ttu-id="aed9a-352">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-352">Description</span></span>

<span data-ttu-id="aed9a-353">Questo servizio imposta l'ora locale del client SNTP con l'ora di input, in formato SNTP, ad esempio secondi e "frazione", che rappresenta il formato per l'inserimento di frazioni di secondo in formato esadecimale.</span><span class="sxs-lookup"><span data-stu-id="aed9a-353">This service sets the SNTP Client local time with the input time, in SNTP format e.g. seconds and ‘fraction’ which is the format for putting fractions of a second in hexadecimal format.</span></span> <span data-ttu-id="aed9a-354">È progettato per l'aggiornamento dell'ora locale del client SNTP da un custode del tempo indipendente, ad esempio un clock in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="aed9a-354">It is intended for updating the SNTP Client local time from an independent time keeper, e.g. a real time clock.</span></span> <span data-ttu-id="aed9a-355">Il protocollo SNTP è concepito per gli aggiornamenti del tempo di SNTP per il tempo di clock locale da "Drifting".</span><span class="sxs-lookup"><span data-stu-id="aed9a-355">The SNTP protocol is intended for SNTP time updates to keep local clock time from ‘drifting’.</span></span> <span data-ttu-id="aed9a-356">Gli aggiornamenti temporali del server SNTP possono essere, ma non sono intesi come input esclusivo per l'ora locale del client SNTP se non è presente alcun detentore del tempo indipendente nel dispositivo applicativo.</span><span class="sxs-lookup"><span data-stu-id="aed9a-356">SNTP server time updates can be, but are not intended to be the sole input to the SNTP Client local time if there is no independent time keeper on the application device.</span></span>

<span data-ttu-id="aed9a-357">Questa API può essere usata anche per concedere al client SNTP un'ora di base prima di avviare il thread del client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-357">This API can also be used to give the SNTP Client a base time before starting the SNTP Client thread.</span></span> <span data-ttu-id="aed9a-358">L'ora locale del client SNTP viene confrontata con gli aggiornamenti ricevuti per i dati temporali validi.</span><span class="sxs-lookup"><span data-stu-id="aed9a-358">The SNTP Client local time is compared to received updates for valid time data.</span></span> <span data-ttu-id="aed9a-359">Per il primo aggiornamento ricevuto, potrebbe essere presente una discrepanza molto grande.</span><span class="sxs-lookup"><span data-stu-id="aed9a-359">For the first time update received, there might be a very large discrepancy.</span></span> <span data-ttu-id="aed9a-360">È pertanto possibile che il client SNTP ignori la discrepanza al primo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="aed9a-360">Therefore there is an option for the SNTP Client to ignore the discrepancy on the first update.</span></span> <span data-ttu-id="aed9a-361">In questo modo, il client SNTP può avviarsi senza un'ora di base.</span><span class="sxs-lookup"><span data-stu-id="aed9a-361">In this manner, the SNTP Client can start without a base time.</span></span> <span data-ttu-id="aed9a-362">È possibile ottenere tempo di input da epoche note (in genere disponibili su Internet) e calcolate come numero di secondi a partire dal 1 ° gennaio 1900 (fino a 2036 quando viene avviato un nuovo ' Epoch '.</span><span class="sxs-lookup"><span data-stu-id="aed9a-362">Input time can be obtained from known epoch times (usually available on the Internet) and are computed as the number of seconds since January 1, 1900 (until 2036 when a new ‘epoch’ will be started.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-363">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-363">Input Parameters</span></span>

- <span data-ttu-id="aed9a-364">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-364">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-365">**secondi** Componente relativo ai secondi dell'input temporale</span><span class="sxs-lookup"><span data-stu-id="aed9a-365">**seconds** Seconds component of the time input</span></span>

- <span data-ttu-id="aed9a-366">**frazione** di Componente dei subsecondi nel formato della frazione SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-366">**fraction** Subseconds component in the SNTP fraction format</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-367">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-367">Return Values</span></span>

- <span data-ttu-id="aed9a-368">**NX_SUCCESS** (0x00) ha impostato correttamente l'ora locale</span><span class="sxs-lookup"><span data-stu-id="aed9a-368">**NX_SUCCESS** (0x00) Successfully set local time</span></span>

- <span data-ttu-id="aed9a-369">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-369">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-370">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-370">Allowed From</span></span>

<span data-ttu-id="aed9a-371">Inizializzazione</span><span class="sxs-lookup"><span data-stu-id="aed9a-371">Initialization</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-372">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-372">Example</span></span>

```C
/* Set the SNTP Client local time. */
base_seconds =  0xd2c50b71;
base_fraction = 0xa132db1e;

status =  nx_sntp_client_set_local_time(&demo_client, 
                                        base_seconds, 
                                        base_fraction);

/* If status is NX_SUCCESS an SNTP Client time 
   was successfully set.  */

```

## <a name="nx_sntp_client_set_time_update_notify"></a><span data-ttu-id="aed9a-373">nx_sntp_client_set_time_update_notify</span><span class="sxs-lookup"><span data-stu-id="aed9a-373">nx_sntp_client_set_time_update_notify</span></span>

<span data-ttu-id="aed9a-374">Imposta callback di aggiornamento SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-374">Set the SNTP update callback</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-375">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-375">Prototype</span></span>

```C
UINT nx_sntp_client_set_time_update_notify(NX_SNTP_CLIENT *client_ptr, 
                           VOID (time_update_cb)(NX_SNTP_TIME_MESSAGE 
                        *time_update_ptr, NX_SNTP_TIME *local_time)));

```

### <a name="description"></a><span data-ttu-id="aed9a-376">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-376">Description</span></span>

<span data-ttu-id="aed9a-377">Questo servizio imposta callback per notificare all'applicazione quando il client di SNTP riceve un aggiornamento temporale valido.</span><span class="sxs-lookup"><span data-stu-id="aed9a-377">This service sets callback to notify the application when the SNTP Client receives a valid time update.</span></span> <span data-ttu-id="aed9a-378">Fornisce il messaggio SNTP effettivo e l'ora locale del client SNTP (in genere lo stesso) in formato NTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-378">It supplies the actual SNTP message and the SNTP Client’s local time (usually the same) in NTP format.</span></span> <span data-ttu-id="aed9a-379">L'applicazione può usare direttamente i dati NTP o chiamare il *servizio nx_sntp_client_utility_display_date_time* per convertire l'ora in formato leggibile.</span><span class="sxs-lookup"><span data-stu-id="aed9a-379">The application can use the NTP data directly or call the *nx_sntp_client_utility_display_date_time service* to convert the time to human readable format.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-380">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-380">Input Parameters</span></span>

- <span data-ttu-id="aed9a-381">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-381">**client_ptr** Pointer to SNTP Client control block</span></span>

- <span data-ttu-id="aed9a-382">**time_update_cb** Puntatore alla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="aed9a-382">**time_update_cb** Pointer to callback function</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-383">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-383">Return Values</span></span>

- <span data-ttu-id="aed9a-384">Il callback **NX_SUCCESS** (0x00) è stato impostato correttamente</span><span class="sxs-lookup"><span data-stu-id="aed9a-384">**NX_SUCCESS** (0x00) Successfully set callback</span></span>

- <span data-ttu-id="aed9a-385">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-385">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-386">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-386">Allowed From</span></span>

<span data-ttu-id="aed9a-387">Inizializzazione</span><span class="sxs-lookup"><span data-stu-id="aed9a-387">Initialization</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-388">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-388">Example</span></span>

```C
/* Set the SNTP Client time update callback. */
VOID client_time_update_notify(NX_SNTP_TIME_MESSAGE *time_update_ptr, 
                                           NX_SNTP_TIME *local time);

NX_SNTP_CLIENT demo_client;


status = nx_sntp_client_set_time_update_notify(&demo_client, 
                                            time_update_cb);

/* If status is NX_SUCCESS an SNTP Client 
   time update callback was successfully set.  */

```

## <a name="nx_sntp_client_stop"></a><span data-ttu-id="aed9a-389">nx_sntp_client_stop</span><span class="sxs-lookup"><span data-stu-id="aed9a-389">nx_sntp_client_stop</span></span>

<span data-ttu-id="aed9a-390">Arrestare il thread del client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-390">Stop the SNTP Client thread</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-391">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-391">Prototype</span></span>

```C
UINT nx_sntp_client_stop(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="aed9a-392">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-392">Description</span></span>

<span data-ttu-id="aed9a-393">Questo servizio arresta il thread del client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-393">This service stops the SNTP Client thread.</span></span> <span data-ttu-id="aed9a-394">Le attività dei thread del client SNTP, che vengono eseguite in un ciclo infinito, vengono sospese in ogni iterazione per rilasciare il controllo dello stato del client SNTP e consentono alle applicazioni di effettuare chiamate API sul client SNTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-394">The SNTP Client thread tasks, which runs in an infinite loop, pauses on every iteration to release control of the SNTP Client state and allow applications to make API calls on the SNTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-395">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-395">Input Parameters</span></span>

- <span data-ttu-id="aed9a-396">**client_ptr** Puntatore al blocco di controllo client SNTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-396">**client_ptr** Pointer to SNTP Client control block</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-397">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-397">Return Values</span></span>

- <span data-ttu-id="aed9a-398">Thread client arrestato **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="aed9a-398">**NX_SUCCESS** (0x00) Successful stopped Client thread</span></span>

- <span data-ttu-id="aed9a-399">**NX_SNTP_CLIENT_NOT_STARTED** (0XDB) SNTP thread del client non avviato</span><span class="sxs-lookup"><span data-stu-id="aed9a-399">**NX_SNTP_CLIENT_NOT_STARTED** (0xDB) SNTP Client thread not started</span></span>

- <span data-ttu-id="aed9a-400">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-400">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-401">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-401">Allowed From</span></span>

<span data-ttu-id="aed9a-402">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-402">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-403">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-403">Example</span></span>

```C
/* Stop the SNTP Client. */
status =  nx_sntp_client_stop(&demo_client);

/* If status is NX_SUCCESS an SNTP 
   Client instance was successfully stopped.  */

```

## <a name="nx_sntp_client_utility_display_date_time"></a><span data-ttu-id="aed9a-404">nx_sntp_client_utility_display_date_time</span><span class="sxs-lookup"><span data-stu-id="aed9a-404">nx_sntp_client_utility_display_date_time</span></span>

<span data-ttu-id="aed9a-405">Converte una stringa di data e ora NTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-405">Convert an NTP Time to Date and Time string</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-406">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-406">Prototype</span></span>

```C
UINT nx_sntp_client_utility_display_date_time (NX_SNTP_CLIENT 
                      *client_ptr, CHAR *buffer, UINT length);

```

### <a name="description"></a><span data-ttu-id="aed9a-407">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-407">Description</span></span>

<span data-ttu-id="aed9a-408">Questo servizio converte l'ora locale del client SNTP in un formato di data anno mese e restituisce la data nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="aed9a-408">This service converts the SNTP Client local time to a year month date format and returns the date in the supplied buffer.</span></span> <span data-ttu-id="aed9a-409">Il NX_SNTP_CURRENT_YEAR deve essere diverso da quello dell'ora del client corrente, ma deve essere definito.</span><span class="sxs-lookup"><span data-stu-id="aed9a-409">The NX_SNTP_CURRENT_YEAR need not be the same year as the current Client time but it must be defined.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-410">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-410">Input Parameters</span></span>

- <span data-ttu-id="aed9a-411">**Puntatore client_ptr al client SNTP**</span><span class="sxs-lookup"><span data-stu-id="aed9a-411">**client_ptr Pointer to SNTP Client**</span></span>

- <span data-ttu-id="aed9a-412">**buffer** Puntatore al buffer per archiviare la data</span><span class="sxs-lookup"><span data-stu-id="aed9a-412">**buffer** Pointer to buffer to store date</span></span>

- <span data-ttu-id="aed9a-413">**lunghezza** Dimensioni del buffer di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-413">**length** Size of input buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-414">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-414">Return Values</span></span>

- <span data-ttu-id="aed9a-415">Conversione **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="aed9a-415">**NX_SUCCESS** (0x00) Successful conversion</span></span>

- <span data-ttu-id="aed9a-416">Il **NX_SNTP_ERROR_CONVERTING_DATETIME** (0xD08) non NX_SNTP_CURRENT_YEAR definito o non è stato stabilito alcun tempo client locale</span><span class="sxs-lookup"><span data-stu-id="aed9a-416">**NX_SNTP_ERROR_CONVERTING_DATETIME** (0xD08) NX_SNTP_CURRENT_YEAR not defined or no local client time established</span></span>

- <span data-ttu-id="aed9a-417">Lunghezza del buffer insufficiente **NX_SNTP_INVALID_DATETIME_BUFFER** (0xD07)</span><span class="sxs-lookup"><span data-stu-id="aed9a-417">**NX_SNTP_INVALID_DATETIME_BUFFER** (0xD07) Insufficient buffer length</span></span>


### <a name="allowed-from"></a><span data-ttu-id="aed9a-418">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-418">Allowed From</span></span>

<span data-ttu-id="aed9a-419">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-419">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-420">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-420">Example</span></span>

```C
/* Convert and display the Client’s local time. */

status =  nx_sntp_client_utility_display_date_time(client_ptr , 
                                        buffer, sizeof(buffer));

/* If status is NX_SUCCESS, 
   date was successfully written to buffer.  */

```

## <a name="nx_sntp_client_utility_msecs_to_fraction"></a><span data-ttu-id="aed9a-421">nx_sntp_client_utility_msecs_to_fraction</span><span class="sxs-lookup"><span data-stu-id="aed9a-421">nx_sntp_client_utility_msecs_to_fraction</span></span>

<span data-ttu-id="aed9a-422">Convertire i millisecondi in un componente della frazione NTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-422">Convert milliseconds to an NTP fraction component</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-423">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-423">Prototype</span></span>

```C
UINT nx_sntp_client_utility_msecs_to_fraction (ULONG milliseconds,   
                                                 ULONG *fraction);

```

### <a name="description"></a><span data-ttu-id="aed9a-424">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-424">Description</span></span>

<span data-ttu-id="aed9a-425">Questo servizio converte i millisecondi di input nel componente della frazione NTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-425">This service converts the input milliseconds to the NTP fraction component.</span></span> <span data-ttu-id="aed9a-426">È progettato per l'uso con applicazioni che hanno un'ora di base iniziale per il client SNTP, ma non in formato NTP secondi/frazione.</span><span class="sxs-lookup"><span data-stu-id="aed9a-426">It is intended for use with applications that have a starting base time for the SNTP Client but not in NTP seconds/fraction format.</span></span> <span data-ttu-id="aed9a-427">Il numero di millisecondi deve essere minore di 1000 per creare una frazione valida.</span><span class="sxs-lookup"><span data-stu-id="aed9a-427">The number of milliseconds must be less than 1000 to make a valid fraction.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-428">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-428">Input Parameters</span></span>

- <span data-ttu-id="aed9a-429">**millisecondi per la conversione**</span><span class="sxs-lookup"><span data-stu-id="aed9a-429">**milliseconds Milliseconds to convert**</span></span>

- <span data-ttu-id="aed9a-430">**frazione** di Puntatore a millisecondi convertiti in frazione</span><span class="sxs-lookup"><span data-stu-id="aed9a-430">**fraction** Pointer to milliseconds converted to fraction</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-431">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-431">Return Values</span></span>

- <span data-ttu-id="aed9a-432">Conversione **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="aed9a-432">**NX_SUCCESS** (0x00) Successful conversion</span></span>

- <span data-ttu-id="aed9a-433">Errore di **NX_SNTP_OVERFLOW_ERROR** (0XD32) durante la conversione del tempo in una data</span><span class="sxs-lookup"><span data-stu-id="aed9a-433">**NX_SNTP_OVERFLOW_ERROR** (0xD32) Error converting time to a date</span></span>

- <span data-ttu-id="aed9a-434">Input di dati di SNTP NX_SNTP_INVALID_TIME (0xD30) non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-434">NX_SNTP_INVALID_TIME (0xD30) Invalid SNTP data input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-435">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-435">Allowed From</span></span>

<span data-ttu-id="aed9a-436">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-436">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-437">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-437">Example</span></span>

```C
/* Convert the milliseconds to a fraction. */


status =  nx_sntp_client_utility_msecs_to_fraction(milliseconds, 
                                                     &fraction);

/* If status is NX_SUCCESS, 
   data was successfully converted.  */

```

## <a name="nx_sntp_client_utility_usecs_to_fraction"></a><span data-ttu-id="aed9a-438">nx_sntp_client_utility_usecs_to_fraction</span><span class="sxs-lookup"><span data-stu-id="aed9a-438">nx_sntp_client_utility_usecs_to_fraction</span></span>

<span data-ttu-id="aed9a-439">Converte i microsecondi in un componente della frazione NTP</span><span class="sxs-lookup"><span data-stu-id="aed9a-439">Convert microseconds to an NTP fraction component</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-440">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-440">Prototype</span></span>

```C
UINT nx_sntp_client_utility_usecs_to_fraction (ULONG microseconds,   
                                                 ULONG *fraction);

```
### <a name="description"></a><span data-ttu-id="aed9a-441">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-441">Description</span></span>

<span data-ttu-id="aed9a-442">Questo servizio converte i microsecondi di input nel componente della frazione NTP.</span><span class="sxs-lookup"><span data-stu-id="aed9a-442">This service converts the input microseconds to the NTP fraction component.</span></span> <span data-ttu-id="aed9a-443">È progettato per l'uso con applicazioni che hanno un'ora di base iniziale per il client SNTP, ma non in formato NTP secondi/frazione.</span><span class="sxs-lookup"><span data-stu-id="aed9a-443">It is intended for use with applications that have a starting base time for the SNTP Client but not in NTP seconds/fraction format.</span></span> <span data-ttu-id="aed9a-444">Il numero di microsecondi deve essere inferiore a 1 milione per creare una frazione valida.</span><span class="sxs-lookup"><span data-stu-id="aed9a-444">The number of microseconds must be less than 1000000 to make a valid fraction.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-445">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-445">Input Parameters</span></span>

- <span data-ttu-id="aed9a-446">**microsecondi** Microsecondi da convertire</span><span class="sxs-lookup"><span data-stu-id="aed9a-446">**microseconds** Microseconds to convert</span></span>

- <span data-ttu-id="aed9a-447">**frazione** di Puntatore a microsecondi convertito in frazione</span><span class="sxs-lookup"><span data-stu-id="aed9a-447">**fraction** Pointer to microseconds converted to fraction</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-448">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-448">Return Values</span></span>

- <span data-ttu-id="aed9a-449">Conversione **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="aed9a-449">**NX_SUCCESS** (0x00) Successful conversion</span></span>

- <span data-ttu-id="aed9a-450">Errore di **NX_SNTP_OVERFLOW_ERROR** (0XD32) durante la conversione del tempo in una data</span><span class="sxs-lookup"><span data-stu-id="aed9a-450">**NX_SNTP_OVERFLOW_ERROR** (0xD32) Error converting time to a date</span></span>

- <span data-ttu-id="aed9a-451">Input di dati di SNTP NX_SNTP_INVALID_TIME (0xD30) non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-451">NX_SNTP_INVALID_TIME (0xD30) Invalid SNTP data input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-452">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-452">Allowed From</span></span>

<span data-ttu-id="aed9a-453">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-453">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-454">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-454">Example</span></span>

```C
/* Convert the microseconds to a fraction. */


status =  nx_sntp_client_utility_msecs_to_fraction(microseconds, 
                                                     &fraction);

/* If status is NX_SUCCESS, data was successfully converted.  */

```

## <a name="nx_sntp_client_utility_fraction_to_usecs"></a><span data-ttu-id="aed9a-455">nx_sntp_client_utility_fraction_to_usecs</span><span class="sxs-lookup"><span data-stu-id="aed9a-455">nx_sntp_client_utility_fraction_to_usecs</span></span>

<span data-ttu-id="aed9a-456">Converte un componente della frazione NTP in microsecondi</span><span class="sxs-lookup"><span data-stu-id="aed9a-456">Convert an NTP fraction component to microseconds</span></span>

### <a name="prototype"></a><span data-ttu-id="aed9a-457">Prototipo</span><span class="sxs-lookup"><span data-stu-id="aed9a-457">Prototype</span></span>

```C
UINT nx_sntp_client_utility_fraction_to_usecs (ULONG fraction,   
                                         ULONG *microseconds);

```

### <a name="description"></a><span data-ttu-id="aed9a-458">Descrizione</span><span class="sxs-lookup"><span data-stu-id="aed9a-458">Description</span></span>

<span data-ttu-id="aed9a-459">Questo servizio converte il componente della frazione NTP di input in microsecondi.</span><span class="sxs-lookup"><span data-stu-id="aed9a-459">This service converts the input NTP fraction component to microseconds.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="aed9a-460">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="aed9a-460">Input Parameters</span></span>

- <span data-ttu-id="aed9a-461">**frazione frazione da convertire**</span><span class="sxs-lookup"><span data-stu-id="aed9a-461">**fraction Fraction to convert**</span></span>

- <span data-ttu-id="aed9a-462">**microsecondi** Puntatore alla frazione convertita in microsecondi</span><span class="sxs-lookup"><span data-stu-id="aed9a-462">**microseconds** Pointer to fraction converted to microseconds</span></span>

### <a name="return-values"></a><span data-ttu-id="aed9a-463">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="aed9a-463">Return Values</span></span>

- <span data-ttu-id="aed9a-464">Conversione **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="aed9a-464">**NX_SUCCESS** (0x00) Successful conversion</span></span>

- <span data-ttu-id="aed9a-465">Input di dati di SNTP NX_SNTP_INVALID_TIME (0xD30) non valido</span><span class="sxs-lookup"><span data-stu-id="aed9a-465">NX_SNTP_INVALID_TIME (0xD30) Invalid SNTP data input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="aed9a-466">Consentito da</span><span class="sxs-lookup"><span data-stu-id="aed9a-466">Allowed From</span></span>

<span data-ttu-id="aed9a-467">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="aed9a-467">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="aed9a-468">Esempio</span><span class="sxs-lookup"><span data-stu-id="aed9a-468">Example</span></span>

```C
/* Convert the fraction to microseconds. */


status =  nx_sntp_client_utility_fraction_to_msecs(fraction, 
                                             &microseconds);

/* If status is NX_SUCCESS, data was successfully converted.  */
```