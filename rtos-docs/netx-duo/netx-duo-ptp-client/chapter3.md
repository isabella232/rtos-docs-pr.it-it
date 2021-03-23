---
title: Capitolo 3-Descrizione dei servizi client PTP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi client PTP NetX Duo in ordine alfabetico.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b4cdeca81c157934e35a219cd5535ec38f2c0746
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821707"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-ptp-client-services"></a><span data-ttu-id="eccc5-103">Capitolo 3-Descrizione dei servizi client PTP di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="eccc5-103">Chapter 3 - Description of Azure RTOS NetX Duo PTP Client Services</span></span>

<span data-ttu-id="eccc5-104">Questo capitolo contiene una descrizione di tutti i servizi client PTP NetX Duo (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="eccc5-104">This chapter contains a description of all NetX Duo PTP client services (listed below) in alphabetical order.</span></span>

[!NOTE]
> <span data-ttu-id="eccc5-105">*Nella sezione **valori restituiti** nelle seguenti descrizioni della funzione API, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.*</span><span class="sxs-lookup"><span data-stu-id="eccc5-105">*In the **Return Values** section in the following API function descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.*</span></span>

## <a name="nx_ptp_client_create"></a><span data-ttu-id="eccc5-106">nx_ptp_client_create</span><span class="sxs-lookup"><span data-stu-id="eccc5-106">nx_ptp_client_create</span></span>

<span data-ttu-id="eccc5-107">Creare un'istanza del client PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-107">Create a PTP client instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-108">Prototype</span></span>

```C
UINT nx_ptp_client_create(
    NX_PTP_CLIENT *client_ptr, NX_IP *ip_ptr, 
    UINT interface_index,
    NX_PACKET_POOL *packet_pool_ptr, 
    UINT thread_priority, 
    UCHAR *thread_stack, 
    UINT stack_size,
    NX_PTP_CLIENT_CLOCK_CALLBACK clock_callback, 
    VOID *clock_callback_data);
```

### <a name="description"></a><span data-ttu-id="eccc5-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-109">Description</span></span>

<span data-ttu-id="eccc5-110">Questo servizio crea un'istanza del client PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-110">This service creates an instance of the PTP client.</span></span>

<span data-ttu-id="eccc5-111">Si noti che l'applicazione deve prima creare un'istanza IP e un pool di pacchetti affinché il client PTP trasmetta i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="eccc5-111">Note that the  application must first create an IP instance and a packet pool for the PTP client to transmit packets.</span></span> <span data-ttu-id="eccc5-112">Per il pool di pacchetti, l'applicazione può usare lo stesso pool di pacchetti nell'istanza IP; in alternativa, è possibile creare un pool di pacchetti dedicato per il client PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-112">For the packet pool, application may use the same packet pool in the IP instance; or it can create a dedicated packet pool for PTP client.</span></span>  <span data-ttu-id="eccc5-113">L'approccio dedicato ai pool di pacchetti ha il vantaggio di usare pacchetti di piccole dimensioni (128 byte pacchetti se viene usato IPv6 o 108 byte solo per IPv4).</span><span class="sxs-lookup"><span data-stu-id="eccc5-113">The dedicated packet pool approach has the advantage of using small packets (128 bytes packets if IPv6 is used, or 108 bytes for IPv4-only).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-114">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-114">Input Parameters</span></span>
* <span data-ttu-id="eccc5-115">**client_ptr** Puntatore al client PTP da creare</span><span class="sxs-lookup"><span data-stu-id="eccc5-115">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="eccc5-116">**ip_ptr** Puntatore a istanza IP</span><span class="sxs-lookup"><span data-stu-id="eccc5-116">**ip_ptr** Pointer to IP instance</span></span>
* <span data-ttu-id="eccc5-117">**interface_index** Indice dell'interfaccia di rete PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-117">**interface_index** Index of PTP network interface</span></span>
* <span data-ttu-id="eccc5-118">**packet_pool_ptr** Puntatore al pool di pacchetti client</span><span class="sxs-lookup"><span data-stu-id="eccc5-118">**packet_pool_ptr** Pointer to client packet pool</span></span>
* <span data-ttu-id="eccc5-119">**THREAD_PRIORITY**  Priorità del thread PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-119">**thread_priority**  Priority of PTP thread</span></span>
* <span data-ttu-id="eccc5-120">**thread_stack** Puntatore a stack di thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-120">**thread_stack** Pointer to thread stack</span></span>
* <span data-ttu-id="eccc5-121">**stack_size** Dimensioni dello stack di thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-121">**stack_size** Size of thread stack</span></span>
* <span data-ttu-id="eccc5-122">**clock_callback** Callback Clock PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-122">**clock_callback** PTP clock callback</span></span>
* <span data-ttu-id="eccc5-123">**clock_callback_data** Dati per il callback di clock</span><span class="sxs-lookup"><span data-stu-id="eccc5-123">**clock_callback_data** Data for the clock callback</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-124">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-124">Return Values</span></span>
* <span data-ttu-id="eccc5-125">Creazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="eccc5-125">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="eccc5-126">Il payload del pacchetto **NX_PTP_CLIENT_INSUFFICIENT_PACKET_PAYLOAD** (0xD04) è troppo piccolo</span><span class="sxs-lookup"><span data-stu-id="eccc5-126">**NX_PTP_CLIENT_INSUFFICIENT_PACKET_PAYLOAD** (0xD04) Packet payload too small</span></span>
* <span data-ttu-id="eccc5-127">Errore **NX_PTP_CLIENT_CLOCK_CALLBACK_FAILURE** (0xD05) al callback Clock</span><span class="sxs-lookup"><span data-stu-id="eccc5-127">**NX_PTP_CLIENT_CLOCK_CALLBACK_FAILURE** (0xD05) Failure on clock callback</span></span>
* <span data-ttu-id="eccc5-128">**stato** di Stato di completamento delle chiamate al servizio NetX Duo e ThreadX</span><span class="sxs-lookup"><span data-stu-id="eccc5-128">**status** Status completion of NetX Duo and ThreadX service calls</span></span>
* <span data-ttu-id="eccc5-129">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-129">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
* <span data-ttu-id="eccc5-130">Interfaccia NX_INVALID_INTERFACE (0x4C) non valida</span><span class="sxs-lookup"><span data-stu-id="eccc5-130">NX_INVALID_INTERFACE (0x4C) Invalid interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-131">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-131">Allowed From</span></span>
<span data-ttu-id="eccc5-132">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-132">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-133">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-133">Example</span></span>
```C
/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_delete"></a><span data-ttu-id="eccc5-134">nx_ptp_client_delete</span><span class="sxs-lookup"><span data-stu-id="eccc5-134">nx_ptp_client_delete</span></span>

<span data-ttu-id="eccc5-135">Elimina un'istanza del client PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-135">Deletes a PTP client instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-136">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-136">Prototype</span></span>

```C
UINT nx_ptp_client_delete(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="eccc5-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-137">Description</span></span>

<span data-ttu-id="eccc5-138">Questo servizio Elimina un'istanza del client PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-138">This service deletes an instance of the PTP client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-139">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-139">Input Parameters</span></span>
* <span data-ttu-id="eccc5-140">**client_ptr** Puntatore al client PTP da eliminare</span><span class="sxs-lookup"><span data-stu-id="eccc5-140">**client_ptr** Pointer to PTP client to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-141">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-141">Return Values</span></span>
* <span data-ttu-id="eccc5-142">Il client **NX_SUCCESS** (0x00) è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="eccc5-142">**NX_SUCCESS** (0x00) Client successfully deleted</span></span>
* <span data-ttu-id="eccc5-143">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-143">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-144">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-144">Allowed From</span></span>
<span data-ttu-id="eccc5-145">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-145">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-146">Example</span></span>
```C
/* Delete the PTP client instance */
status = nx_ptp_client_delete(&ptp_client);

/* If the client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_master_info_get"></a><span data-ttu-id="eccc5-147">nx_ptp_client_master_info_get</span><span class="sxs-lookup"><span data-stu-id="eccc5-147">nx_ptp_client_master_info_get</span></span>

<span data-ttu-id="eccc5-148">Ottenere informazioni sull'orologio Master.</span><span class="sxs-lookup"><span data-stu-id="eccc5-148">Get master clock information.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-149">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-149">Prototype</span></span>

```C
UINT nx_ptp_client_master_info_get(
    NX_PTP_CLIENT_MASTER *master_ptr, 
    NXD_ADDRESS *address, 
    UCHAR **port_identity, 
    UINT *port_identity_length, 
    UCHAR *priority1, 
    UCHAR *priority2, 
    UCHAR *clock_class, UCHAR *clock_accuracy, 
    USHORT *clock_variance, 
    UCHAR **grandmaster_identity,
    UINT *grandmaster_identity_length, 
    USHORT *steps_removed, 
    UCHAR *time_source);
```

### <a name="description"></a><span data-ttu-id="eccc5-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-150">Description</span></span>
<span data-ttu-id="eccc5-151">Questo servizio ottiene informazioni sul clock del master.</span><span class="sxs-lookup"><span data-stu-id="eccc5-151">This service gets information of master clock.</span></span> <span data-ttu-id="eccc5-152">Il blocco di controllo master viene passato all'applicazione utente tramite la funzione di callback evento.</span><span class="sxs-lookup"><span data-stu-id="eccc5-152">The master control block is passed to user application through event callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-153">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-153">Input Parameters</span></span>
* <span data-ttu-id="eccc5-154">**master_ptr** Puntatore al clock master di PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-154">**master_ptr** Pointer to PTP master clock</span></span>
* <span data-ttu-id="eccc5-155">**Indirizzo** Indirizzo del clock master</span><span class="sxs-lookup"><span data-stu-id="eccc5-155">**address** Address of master clock</span></span>
* <span data-ttu-id="eccc5-156">**port_identity** Identità e porta master PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-156">**port_identity** PTP master port and identity</span></span>
* <span data-ttu-id="eccc5-157">**port_identity_length** Lunghezza della porta master e dell'identità PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-157">**port_identity_length** Length of PTP master port and identity</span></span>
* <span data-ttu-id="eccc5-158">**priority1** Priority1 di clock master PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-158">**priority1** Priority1 of PTP master clock</span></span>
* <span data-ttu-id="eccc5-159">**Priority2** Priority2 di clock master PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-159">**priority2** Priority2 of PTP master clock</span></span>
* <span data-ttu-id="eccc5-160">**clock_class** Classe di clock master PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-160">**clock_class** Class of PTP master clock</span></span>
* <span data-ttu-id="eccc5-161">**clock_accuracy** Accuratezza del clock master PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-161">**clock_accuracy** Accuracy of PTP master clock</span></span>
* <span data-ttu-id="eccc5-162">**clock_variance** Varianza del clock master PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-162">**clock_variance** Variance of PTP master clock</span></span>
* <span data-ttu-id="eccc5-163">**grandmaster_identity** Identità del clock Grandmaster</span><span class="sxs-lookup"><span data-stu-id="eccc5-163">**grandmaster_identity** Identity of grandmaster clock</span></span>
* <span data-ttu-id="eccc5-164">**grandmaster_identity_length** Lunghezza dell'identità del Grandmaster</span><span class="sxs-lookup"><span data-stu-id="eccc5-164">**grandmaster_identity_length** Length of grandmaster Identity</span></span>
* <span data-ttu-id="eccc5-165">**steps_removed** Passaggi rimossi dall'intestazione PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-165">**steps_removed** Steps removed from PTP header</span></span>
* <span data-ttu-id="eccc5-166">**Time_Source** Origine del timer usato dall'orologio Grandmaster</span><span class="sxs-lookup"><span data-stu-id="eccc5-166">**time_source** The source of timer used by grandmaster clock</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-167">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-167">Return Values</span></span>
* <span data-ttu-id="eccc5-168">**NX_SUCCESS** (0x00) ottenere correttamente le informazioni sull'orologio Master</span><span class="sxs-lookup"><span data-stu-id="eccc5-168">**NX_SUCCESS** (0x00) Get master clock information successfully</span></span>
* <span data-ttu-id="eccc5-169">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-169">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-170">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-170">Allowed From</span></span>
<span data-ttu-id="eccc5-171">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-171">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-172">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-172">Example</span></span>
```C
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
NXD_ADDRESS address;
UCHAR *port_identity;
UINT port_identity_length;
UCHAR priority1, priority2;
UCHAR clock_class, clock_accuracy;
USHORT clock_variance;
UCHAR *grandmaster_identity;
UINT grandmaster_identity_length;
USHORT steps_removed;
UCHAR time_source;

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_MASTER:
        {
            status = nx_ptp_client_master_info_get((NX_PTP_CLIENT_MASTER *)event_data, 
                                                   &address, &port_identity,
                                                   &port_identity_length, &priority1, 
                                                   &priority2, &clock_class,
                                                   &clock_accuracy, &clock_variance, 
                                                   &grandmaster_identity,
                                                   &grandmaster_identity_length, 
                                                   &steps_removed, &time_source);

            /* If the master clock information was successfully get, status = NX_SUCCESS. */
            break;
        }

        /* Other event process. */
    }
}
```

## <a name="nx_ptp_client_packet_timestamp_notify"></a><span data-ttu-id="eccc5-173">nx_ptp_client_packet_timestamp_notify</span><span class="sxs-lookup"><span data-stu-id="eccc5-173">nx_ptp_client_packet_timestamp_notify</span></span>

<span data-ttu-id="eccc5-174">Notifica al client PTP il timestamp del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="eccc5-174">Notify PTP client the timestamp of the packet.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-175">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-175">Prototype</span></span>

```C
VOID nx_ptp_client_packet_timestamp_notify(
    NX_PTP_CLIENT *client_ptr, 
    NX_PACKET *packet_ptr, 
    NX_PTP_TIME *timestamp_ptr);
```

### <a name="description"></a><span data-ttu-id="eccc5-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-176">Description</span></span>
<span data-ttu-id="eccc5-177">Questo servizio informa il client PTP che il pacchetto viene trasmesso con timestamp.</span><span class="sxs-lookup"><span data-stu-id="eccc5-177">This service notifies the PTP client that packet is transmitted with timestamp.</span></span> <span data-ttu-id="eccc5-178">Questo servizio è progettato per il driver di rete e viene richiamato quando il pacchetto viene trasmesso.</span><span class="sxs-lookup"><span data-stu-id="eccc5-178">This service is designed for network driver and invoked when the packet is transmitted.</span></span> <span data-ttu-id="eccc5-179">Il timestamp viene in genere generato dall'hardware.</span><span class="sxs-lookup"><span data-stu-id="eccc5-179">The timestamp is usually generated by hardware.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-180">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-180">Input Parameters</span></span>
* <span data-ttu-id="eccc5-181">**client_ptr** Puntatore al client PTP da creare</span><span class="sxs-lookup"><span data-stu-id="eccc5-181">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="eccc5-182">**packet_ptr** Puntatore al pacchetto PTP trasmesso</span><span class="sxs-lookup"><span data-stu-id="eccc5-182">**packet_ptr** Pointer to PTP packet that is transmitted</span></span>
* <span data-ttu-id="eccc5-183">**timestamp_ptr** Puntatore al timestamp del pacchetto PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-183">**timestamp_ptr** Pointer to timestamp of PTP packet</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-184">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-184">Return Values</span></span>
<span data-ttu-id="eccc5-185">nessuno</span><span class="sxs-lookup"><span data-stu-id="eccc5-185">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-186">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-186">Allowed From</span></span>
<span data-ttu-id="eccc5-187">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-187">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-188">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-188">Example</span></span>
```C
/* Call notification callback */
nx_ptp_client_packet_timestamp_notify(client_ptr, packet_ptr, &ts);
```

## <a name="nx_ptp_client_soft_clock_callback"></a><span data-ttu-id="eccc5-189">nx_ptp_client_soft_clock_callback</span><span class="sxs-lookup"><span data-stu-id="eccc5-189">nx_ptp_client_soft_clock_callback</span></span>

<span data-ttu-id="eccc5-190">Implementazione del software di un clock di PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-190">Software implementation of a PTP clock.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-191">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-191">Prototype</span></span>

```C
UINT nx_ptp_client_soft_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```

### <a name="description"></a><span data-ttu-id="eccc5-192">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-192">Description</span></span>
<span data-ttu-id="eccc5-193">Questa funzione di callback funge da origine di clock a bassa risoluzione simulata per PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-193">This callback function serves as a simulated low resolution clock source for PTP.</span></span> <span data-ttu-id="eccc5-194">Questa routine viene fornita come riferimento e non può essere usata per la produzione.</span><span class="sxs-lookup"><span data-stu-id="eccc5-194">This routine is provided as a reference and cannot be used for production.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-195">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-195">Input Parameters</span></span>
* <span data-ttu-id="eccc5-196">**client_ptr** Puntatore al client PTP da creare</span><span class="sxs-lookup"><span data-stu-id="eccc5-196">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="eccc5-197">**operazione** di Operazione di callback. i valori validi sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="eccc5-197">**operation** Callback operation, valid values are defined as:</span></span>
  * <span data-ttu-id="eccc5-198">**NX_PTP_CLIENT_CLOCK_INIT** Inizializza Clock.</span><span class="sxs-lookup"><span data-stu-id="eccc5-198">**NX_PTP_CLIENT_CLOCK_INIT** Initialize clock.</span></span>
  * <span data-ttu-id="eccc5-199">**NX_PTP_CLIENT_CLOCK_SET** Imposta il timestamp corrente specificato da `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="eccc5-199">**NX_PTP_CLIENT_CLOCK_SET** Set current timestamp specified by `time_ptr`.</span></span>
  * <span data-ttu-id="eccc5-200">**NX_PTP_CLIENT_CLOCK_GET** Restituisce il timestamp corrente a `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="eccc5-200">**NX_PTP_CLIENT_CLOCK_GET** Return current timestamp to `time_ptr`.</span></span>
  * <span data-ttu-id="eccc5-201">**NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Estrarre il timestamp da `packet_ptr` a `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="eccc5-201">**NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Extract timestamp from `packet_ptr` to `time_ptr`.</span></span>
  * <span data-ttu-id="eccc5-202">**NX_PTP_CLIENT_CLOCK_ADJUST** Imposta il timestamp corrente inferiore a *1* secondo.</span><span class="sxs-lookup"><span data-stu-id="eccc5-202">**NX_PTP_CLIENT_CLOCK_ADJUST** Adjust current timestamp less than *1* second.</span></span>
  * <span data-ttu-id="eccc5-203">**NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Contrassegnare il `packet_ptr` che richiede per notificare al client PTP il timestamp al momento della trasmissione.</span><span class="sxs-lookup"><span data-stu-id="eccc5-203">**NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Mark the `packet_ptr` which requires to notify PTP client the timestamp when it is transmitted.</span></span>
  * <span data-ttu-id="eccc5-204">**NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Aggiornare il timer soft.</span><span class="sxs-lookup"><span data-stu-id="eccc5-204">**NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Update soft timer.</span></span> <span data-ttu-id="eccc5-205">Può essere ignorato dal clock dell'hardware.</span><span class="sxs-lookup"><span data-stu-id="eccc5-205">It can be ignored by hardware clock.</span></span>
* <span data-ttu-id="eccc5-206">**time_ptr** Puntatore al timestamp.</span><span class="sxs-lookup"><span data-stu-id="eccc5-206">**time_ptr** Pointer to timestamp.</span></span>
* <span data-ttu-id="eccc5-207">**packet_ptr** Puntatore al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="eccc5-207">**packet_ptr** Pointer to packet.</span></span>
* <span data-ttu-id="eccc5-208">**callback_data** Puntatore ai dati di callback opachi.</span><span class="sxs-lookup"><span data-stu-id="eccc5-208">**callback_data** Pointer to opaque callback data.</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-209">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-209">Return Values</span></span>
* <span data-ttu-id="eccc5-210">Operazione di **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="eccc5-210">**NX_SUCCESS** (0x00) Operation successfully</span></span>
* <span data-ttu-id="eccc5-211">Parametro **NX_PTP_PARAM_ERROR** (0XD03) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-211">**NX_PTP_PARAM_ERROR** (0xD03) Invalid parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-212">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-212">Allowed From</span></span>
<span data-ttu-id="eccc5-213">PTP interno</span><span class="sxs-lookup"><span data-stu-id="eccc5-213">PTP internal</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-214">Example</span></span>
```C/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              nx_ptp_client_soft_clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_start"></a><span data-ttu-id="eccc5-215">nx_ptp_client_start</span><span class="sxs-lookup"><span data-stu-id="eccc5-215">nx_ptp_client_start</span></span>

<span data-ttu-id="eccc5-216">Avviare il client PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-216">Start PTP client.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-217">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-217">Prototype</span></span>

```C
UINT nx_ptp_client_start(
    NX_PTP_CLIENT *client_ptr, 
    UCHAR *client_port_identity_ptr, 
    UINT client_port_identity_length,
    UINT domain, 
    UINT transport_specific, 
    NX_PTP_CLIENT_EVENT_CALLBACK event_callback,
    VOID *event_callback_data)
```

### <a name="description"></a><span data-ttu-id="eccc5-218">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-218">Description</span></span>
<span data-ttu-id="eccc5-219">Questo servizio avvia un'istanza del client PTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="eccc5-219">This service starts a previously created PTP client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-220">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-220">Input Parameters</span></span>
* <span data-ttu-id="eccc5-221">**client_ptr** Puntatore al client PTP da creare</span><span class="sxs-lookup"><span data-stu-id="eccc5-221">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="eccc5-222">**client_port_identity_ptr** Puntatore alla porta e all'identità client, può essere NULL</span><span class="sxs-lookup"><span data-stu-id="eccc5-222">**client_port_identity_ptr** Pointer to client port and identity, it can be NULL</span></span>
* <span data-ttu-id="eccc5-223">**client_port_identity_length** Lunghezza della porta e dell'identità del client.</span><span class="sxs-lookup"><span data-stu-id="eccc5-223">**client_port_identity_length** Length of client port and identity.</span></span> <span data-ttu-id="eccc5-224">Deve essere 0 se client_port_identity_ptr è NULL o NX_PTP_CLOCK_PORT_IDENTITY_SIZE (10)</span><span class="sxs-lookup"><span data-stu-id="eccc5-224">It must be 0 if client_port_identity_ptr is NULL or NX_PTP_CLOCK_PORT_IDENTITY_SIZE (10)</span></span>
* <span data-ttu-id="eccc5-225">**dominio** Dominio orologio PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-225">**domain** PTP clock domain</span></span>
* <span data-ttu-id="eccc5-226">**transport_specific** 4 bit di trasporto specifico</span><span class="sxs-lookup"><span data-stu-id="eccc5-226">**transport_specific** 4 bits of transport specific</span></span>
* <span data-ttu-id="eccc5-227">**event_callback** Funzione di callback richiamata sull'evento</span><span class="sxs-lookup"><span data-stu-id="eccc5-227">**event_callback** Callback function invoked on event</span></span>
* <span data-ttu-id="eccc5-228">**event_callback_data** Dati per il callback di evento</span><span class="sxs-lookup"><span data-stu-id="eccc5-228">**event_callback_data** Data for the event callback</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-229">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-229">Return Values</span></span>
* <span data-ttu-id="eccc5-230">Il client **NX_SUCCESS** (0x00) è stato avviato</span><span class="sxs-lookup"><span data-stu-id="eccc5-230">**NX_SUCCESS** (0x00) Client successfully started</span></span>
* <span data-ttu-id="eccc5-231">Il client PTP **NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) è già stato avviato</span><span class="sxs-lookup"><span data-stu-id="eccc5-231">**NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) PTP client already started</span></span>
* <span data-ttu-id="eccc5-232">**stato** di Stato di completamento delle chiamate al servizio NetX Duo e ThreadX</span><span class="sxs-lookup"><span data-stu-id="eccc5-232">**status** Status completion of NetX Duo and ThreadX service calls</span></span>
* <span data-ttu-id="eccc5-233">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-233">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-234">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-234">Allowed From</span></span>
<span data-ttu-id="eccc5-235">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-235">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-236">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-236">Example</span></span>
```C
status = nx_ptp_client_start(&ptp_client, NX_NULL, 0, 0, 0, ptp_event_callback, NX_NULL);

/* If the client was successfully started, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_stop"></a><span data-ttu-id="eccc5-237">nx_ptp_client_stop</span><span class="sxs-lookup"><span data-stu-id="eccc5-237">nx_ptp_client_stop</span></span>

<span data-ttu-id="eccc5-238">Arrestare il client PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-238">Stop PTP client.</span></span>  <span data-ttu-id="eccc5-239">Quando il client PTP viene arrestato, non elabora i pacchetti PTP né trasmette i pacchetti PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-239">After the PTP client is stopped, it does not process PTP packets, nor does it transmit PTP packets.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-240">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-240">Prototype</span></span>

```C
UINT nx_ptp_client_stop(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="eccc5-241">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-241">Description</span></span>
<span data-ttu-id="eccc5-242">Questo servizio interrompe un'istanza del client PTP creata e avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="eccc5-242">This service stops a previously created and started PTP client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-243">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-243">Input Parameters</span></span>
* <span data-ttu-id="eccc5-244">**client_ptr** Puntatore al client PTP da arrestare</span><span class="sxs-lookup"><span data-stu-id="eccc5-244">**client_ptr** Pointer to PTP client to stop</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-245">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-245">Return Values</span></span>
* <span data-ttu-id="eccc5-246">Il client **NX_SUCCESS** (0x00) è stato arrestato</span><span class="sxs-lookup"><span data-stu-id="eccc5-246">**NX_SUCCESS** (0x00) Client successfully stopped</span></span>
* <span data-ttu-id="eccc5-247">Client **NX_PTP_CLIENT_NOT_STARTED** (0xD01) non avviato</span><span class="sxs-lookup"><span data-stu-id="eccc5-247">**NX_PTP_CLIENT_NOT_STARTED** (0xD01) Client not started</span></span>
* <span data-ttu-id="eccc5-248">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-248">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-249">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-249">Allowed From</span></span>
<span data-ttu-id="eccc5-250">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-250">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-251">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-251">Example</span></span>
```C
status = nx_ptp_client_stop(&ptp_client);

/* If the client was successfully stopped, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_sync_info_get"></a><span data-ttu-id="eccc5-252">nx_ptp_client_sync_info_get</span><span class="sxs-lookup"><span data-stu-id="eccc5-252">nx_ptp_client_sync_info_get</span></span>

<span data-ttu-id="eccc5-253">Ottenere le informazioni di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="eccc5-253">Get Sync information.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-254">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-254">Prototype</span></span>

```C
UINT nx_ptp_client_sync_info_get(
    NX_PTP_CLIENT_SYNC *sync_ptr, 
    USHORT *flags, 
    SHORT *utc_offset);
```

### <a name="description"></a><span data-ttu-id="eccc5-255">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-255">Description</span></span>
<span data-ttu-id="eccc5-256">Questo servizio ottiene informazioni sul messaggio di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="eccc5-256">This service gets information of Sync message.</span></span> <span data-ttu-id="eccc5-257">Il blocco di controllo di sincronizzazione viene passato all'applicazione utente tramite la funzione di callback evento.</span><span class="sxs-lookup"><span data-stu-id="eccc5-257">The Sync control block is passed to user application through event callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-258">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-258">Input Parameters</span></span>
* <span data-ttu-id="eccc5-259">**client_ptr** Puntatore al client PTP da creare</span><span class="sxs-lookup"><span data-stu-id="eccc5-259">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="eccc5-260">**flag** Flag nel messaggio di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="eccc5-260">**flags** Flags in Sync message</span></span>
* <span data-ttu-id="eccc5-261">**utc_offset** Offset tra TAI e UTC</span><span class="sxs-lookup"><span data-stu-id="eccc5-261">**utc_offset** Offset between TAI and UTC</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-262">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-262">Return Values</span></span>
* <span data-ttu-id="eccc5-263">**NX_SUCCESS** (0x00) ottenere correttamente le informazioni di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="eccc5-263">**NX_SUCCESS** (0x00) Get Sync information successfully</span></span>
* <span data-ttu-id="eccc5-264">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-264">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-265">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-265">Allowed From</span></span>
<span data-ttu-id="eccc5-266">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-266">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-267">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-267">Example</span></span>
```C
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
USHORT utc_offset;

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_SYNC:
        {
            nx_ptp_client_sync_info_get((NX_PTP_CLIENT_SYNC *)event_data, NX_NULL, &utc_offset);

            /* If the Sync information was successfully get, status = NX_SUCCESS. */
            break;
        }

        /* Other event process. */
    }
}
```

## <a name="nx_ptp_client_time_get"></a><span data-ttu-id="eccc5-268">nx_ptp_client_time_get</span><span class="sxs-lookup"><span data-stu-id="eccc5-268">nx_ptp_client_time_get</span></span>

<span data-ttu-id="eccc5-269">Ottiene l'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="eccc5-269">Get current time.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-270">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-270">Prototype</span></span>

```C
UINT nx_ptp_client_time_get(
    NX_PTP_CLIENT *client_ptr, 
    NX_PTP_TIME *time_ptr);
```

### <a name="description"></a><span data-ttu-id="eccc5-271">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-271">Description</span></span>
<span data-ttu-id="eccc5-272">Questo servizio ottiene il valore corrente del clock di PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-272">This service gets the current value of the PTP clock.</span></span> <span data-ttu-id="eccc5-273">È disponibile, indipendentemente dal fatto che il client PTP sia sincronizzato con l'orologio Master.</span><span class="sxs-lookup"><span data-stu-id="eccc5-273">It is available no matter PTP client is synchronized with master clock or not.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-274">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-274">Input Parameters</span></span>
* <span data-ttu-id="eccc5-275">**client_ptr** Puntatore al client PTP da creare</span><span class="sxs-lookup"><span data-stu-id="eccc5-275">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="eccc5-276">**time_ptr** Puntatore all'ora di PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-276">**time_ptr** Pointer to PTP time</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-277">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-277">Return Values</span></span>
* <span data-ttu-id="eccc5-278">Creazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="eccc5-278">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="eccc5-279">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-279">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-280">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-280">Allowed From</span></span>
<span data-ttu-id="eccc5-281">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-281">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-282">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-282">Example</span></span>
```C
/* Get the PTP clock */
nx_ptp_client_time_get(&ptp_client, &tm);
```

## <a name="nx_ptp_client_time_set"></a><span data-ttu-id="eccc5-283">nx_ptp_client_time_set</span><span class="sxs-lookup"><span data-stu-id="eccc5-283">nx_ptp_client_time_set</span></span>

<span data-ttu-id="eccc5-284">Imposta l'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="eccc5-284">Set current time.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-285">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-285">Prototype</span></span>

```C
UINT nx_ptp_client_time_set(
    NX_PTP_CLIENT *client_ptr, 
    NX_PTP_TIME *time_ptr);
```

### <a name="description"></a><span data-ttu-id="eccc5-286">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-286">Description</span></span>
<span data-ttu-id="eccc5-287">Questo servizio imposta il valore corrente del clock di PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-287">This service sets the current value of the PTP clock.</span></span> <span data-ttu-id="eccc5-288">Deve essere richiamato prima dell'avvio del client PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-288">It must be invoked before PTP client starts.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-289">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-289">Input Parameters</span></span>
* <span data-ttu-id="eccc5-290">**client_ptr** Puntatore al client PTP da creare</span><span class="sxs-lookup"><span data-stu-id="eccc5-290">**client_ptr** Pointer to PTP client to create</span></span>
* <span data-ttu-id="eccc5-291">**time_ptr** Puntatore all'ora di PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-291">**time_ptr** Pointer to PTP time</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-292">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-292">Return Values</span></span>
* <span data-ttu-id="eccc5-293">Creazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="eccc5-293">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="eccc5-294">Il client PTP **NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) è già stato avviato</span><span class="sxs-lookup"><span data-stu-id="eccc5-294">**NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) PTP client already started</span></span>
* <span data-ttu-id="eccc5-295">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-295">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-296">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-296">Allowed From</span></span>
<span data-ttu-id="eccc5-297">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-297">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-298">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-298">Example</span></span>
```C
/* Set current time before PTP client started.  */
status = nx_ptp_client_time_set(&ptp_client, &tm);
```

## <a name="nx_ptp_client_utility_convert_time_to_date"></a><span data-ttu-id="eccc5-299">nx_ptp_client_utility_convert_time_to_date</span><span class="sxs-lookup"><span data-stu-id="eccc5-299">nx_ptp_client_utility_convert_time_to_date</span></span>

<span data-ttu-id="eccc5-300">Convertire l'ora del PTP in una data e un'ora UTC.</span><span class="sxs-lookup"><span data-stu-id="eccc5-300">Convert PTP time to a UTC date and time.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-301">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-301">Prototype</span></span>

```C
UINT nx_ptp_client_utility_convert_time_to_date(
    NX_PTP_TIME *time_ptr, 
    LONG offset, 
    NX_PTP_DATE_TIME *date_time_ptr);
```

### <a name="description"></a><span data-ttu-id="eccc5-302">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-302">Description</span></span>
<span data-ttu-id="eccc5-303">Questo servizio converte l'ora PTP in una data e un'ora UTC.</span><span class="sxs-lookup"><span data-stu-id="eccc5-303">This service converts PTP time to a UTC date and time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-304">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-304">Input Parameters</span></span>
* <span data-ttu-id="eccc5-305">**time_ptr** Puntatore all'ora di PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-305">**time_ptr** Pointer to PTP time</span></span>
* <span data-ttu-id="eccc5-306">**offset** Offset del secondo con segno per aggiungere l'ora di PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-306">**offset** Signed second offset to add the PTP time</span></span>
* <span data-ttu-id="eccc5-307">**date_time_ptr** Puntatore alla data risultante</span><span class="sxs-lookup"><span data-stu-id="eccc5-307">**date_time_ptr** Pointer to resulting date</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-308">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-308">Return Values</span></span>
* <span data-ttu-id="eccc5-309">Creazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="eccc5-309">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="eccc5-310">**Puntatore alla data risultante** (0xD03) parametro di input non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-310">**Pointer to resulting date** (0xD03) Invalid input parameter</span></span>
* <span data-ttu-id="eccc5-311">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-311">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-312">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-312">Allowed From</span></span>
<span data-ttu-id="eccc5-313">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-313">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-314">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-314">Example</span></span>
```C
/* convert PTP time to UTC date and time */
status = nx_ptp_client_utility_convert_time_to_date(&tm, -ptp_utc_offset, &date);

/* If the time was successfully converted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_utility_time_diff"></a><span data-ttu-id="eccc5-315">nx_ptp_client_utility_time_diff</span><span class="sxs-lookup"><span data-stu-id="eccc5-315">nx_ptp_client_utility_time_diff</span></span>

<span data-ttu-id="eccc5-316">Diff due volte PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-316">Diff two PTP times.</span></span>

### <a name="prototype"></a><span data-ttu-id="eccc5-317">Prototipo</span><span class="sxs-lookup"><span data-stu-id="eccc5-317">Prototype</span></span>

```C
UINT nx_ptp_client_utility_time_diff(
    NX_PTP_TIME *time1_ptr, 
    NX_PTP_TIME *time2_ptr, 
    NX_PTP_TIME *result_ptr);
```

### <a name="description"></a><span data-ttu-id="eccc5-318">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eccc5-318">Description</span></span>
<span data-ttu-id="eccc5-319">Questo servizio calcola la differenza tra due volte PTP.</span><span class="sxs-lookup"><span data-stu-id="eccc5-319">This service computes the difference between two PTP times.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="eccc5-320">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="eccc5-320">Input Parameters</span></span>
* <span data-ttu-id="eccc5-321">**time1_ptr** Puntatore alla prima ora PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-321">**time1_ptr** Pointer to first PTP time</span></span>
* <span data-ttu-id="eccc5-322">**time2_ptr** Puntatore alla seconda ora PTP</span><span class="sxs-lookup"><span data-stu-id="eccc5-322">**time2_ptr** Pointer to second PTP time</span></span>
* <span data-ttu-id="eccc5-323">**result_ptr** Puntatore al risultato time1-time2</span><span class="sxs-lookup"><span data-stu-id="eccc5-323">**result_ptr** Pointer to result time1-time2</span></span>

### <a name="return-values"></a><span data-ttu-id="eccc5-324">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="eccc5-324">Return Values</span></span>
* <span data-ttu-id="eccc5-325">Creazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="eccc5-325">**NX_SUCCESS** (0x00) Client successfully created</span></span>
* <span data-ttu-id="eccc5-326">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="eccc5-326">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="eccc5-327">Consentito da</span><span class="sxs-lookup"><span data-stu-id="eccc5-327">Allowed From</span></span>
<span data-ttu-id="eccc5-328">Thread</span><span class="sxs-lookup"><span data-stu-id="eccc5-328">Threads</span></span>

### <a name="example"></a><span data-ttu-id="eccc5-329">Esempio</span><span class="sxs-lookup"><span data-stu-id="eccc5-329">Example</span></span>
```C
/* Diff time.  */
status = nx_ptp_client_utility_time_diff(&time1, &time2, &result);

/* If the calculation was successfully, status = NX_SUCCESS. */
```