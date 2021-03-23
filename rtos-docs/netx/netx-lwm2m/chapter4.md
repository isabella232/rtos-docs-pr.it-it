---
title: Capitolo 4-Descrizione dei servizi LWM2M NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi LWM2M di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d5a402790387c2720db304fe93d74252494d7638
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822577"
---
# <a name="chapter-4---description-of-azure-rtos-netx-lwm2m-services"></a><span data-ttu-id="db2f7-103">Capitolo 4-Descrizione dei servizi LWM2M NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="db2f7-103">Chapter 4 - Description of Azure RTOS NetX LWM2M services</span></span>

<span data-ttu-id="db2f7-104">Questo capitolo contiene una descrizione di tutti i servizi LWM2M di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="db2f7-104">This chapter contains a description of all Azure RTOS NetX LWM2M services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="db2f7-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="db2f7-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

### <a name="lwm2m-client-management"></a><span data-ttu-id="db2f7-106">Gestione client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-106">LWM2M Client Management</span></span>

- <span data-ttu-id="db2f7-107">**nx_lwm2m_client_create**: *creare un client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-107">**nx_lwm2m_client_create**: *Create LWM2M Client*</span></span>
- <span data-ttu-id="db2f7-108">**nx_lwm2m_client_delete**: *eliminare il client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-108">**nx_lwm2m_client_delete**: *Delete LWM2M Client*</span></span>
- <span data-ttu-id="db2f7-109">**nx_lwm2m_client_lock**: *bloccare il client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-109">**nx_lwm2m_client_lock**: *Lock LWM2M Client*</span></span>
- <span data-ttu-id="db2f7-110">**nx_lwm2m_client_object_add**: *aggiungere l'implementazione dell'oggetto al client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-110">**nx_lwm2m_client_object_add**: *Add Object implementation to the LWM2M Client*</span></span>
- <span data-ttu-id="db2f7-111">**nx_lwm2m_client_unlock**: *sbloccare il client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-111">**nx_lwm2m_client_unlock**: *Unlock LWM2M Client*</span></span>

### <a name="lwm2m-client-session-management"></a><span data-ttu-id="db2f7-112">Gestione delle sessioni client di LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-112">LWM2M Client Session Management</span></span>

- <span data-ttu-id="db2f7-113">**nx_lwm2m_client_session_bootstrap**: *avviare una sessione con un server bootstrap*</span><span class="sxs-lookup"><span data-stu-id="db2f7-113">**nx_lwm2m_client_session_bootstrap**: *Start a session with a Bootstrap Server*</span></span>
- <span data-ttu-id="db2f7-114">**nx_lwm2m_client_session_bootstrap_dtls**: *avviare una sessione protetta con un server bootstrap*</span><span class="sxs-lookup"><span data-stu-id="db2f7-114">**nx_lwm2m_client_session_bootstrap_dtls**: *Start a secure session with a Bootstrap Server*</span></span>
- <span data-ttu-id="db2f7-115">**nx_lwm2m_client_session_create**: *creare una sessione client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-115">**nx_lwm2m_client_session_create**: *Create LWM2M Client Session*</span></span>
- <span data-ttu-id="db2f7-116">**nx_lwm2m_client_session_delete**: *eliminare la sessione del client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-116">**nx_lwm2m_client_session_delete**: *Delete LWM2M Client Session*</span></span>
- <span data-ttu-id="db2f7-117">**nx_lwm2m_client_session_deregister**: *terminare una sessione con un server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-117">**nx_lwm2m_client_session_deregister**: *Terminate a session with a LWM2M Server*</span></span>
- <span data-ttu-id="db2f7-118">**nx_lwm2m_client_session_error_get**: *ottenere l'ultimo errore di una sessione*</span><span class="sxs-lookup"><span data-stu-id="db2f7-118">**nx_lwm2m_client_session_error_get**: *Get last error of a session*</span></span>
- <span data-ttu-id="db2f7-119">**nx_lwm2m_client_session_register**: *avviare una sessione con un server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-119">**nx_lwm2m_client_session_register**: *Start a session with a LWM2M Server*</span></span>
- <span data-ttu-id="db2f7-120">**nx_lwm2m_client_session_register_dtls**: *avviare una sessione protetta con un server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-120">**nx_lwm2m_client_session_register_dtls**: *Start a secure session with a LWM2M Server*</span></span>
- <span data-ttu-id="db2f7-121">**nx_lwm2m_client_session_update**: *aggiornare una sessione con un server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-121">**nx_lwm2m_client_session_update**: *Update a session with a LWM2M Server*</span></span>

### <a name="security-object-implementation"></a><span data-ttu-id="db2f7-122">Implementazione di oggetti di sicurezza</span><span class="sxs-lookup"><span data-stu-id="db2f7-122">Security Object Implementation</span></span>

- <span data-ttu-id="db2f7-123">**nx_lwm2m_client_security_key_callbacks_set**: *impostare i callback di gestione delle chiavi di sicurezza*</span><span class="sxs-lookup"><span data-stu-id="db2f7-123">**nx_lwm2m_client_security_key_callbacks_set**: *Set security key management callbacks*</span></span>

### <a name="device-object-implementation"></a><span data-ttu-id="db2f7-124">Implementazione di oggetti dispositivo</span><span class="sxs-lookup"><span data-stu-id="db2f7-124">Device Object Implementation</span></span>

- <span data-ttu-id="db2f7-125">**nx_lwm2m_client_device_callbacks_set**: *impostare i callback dell'applicazione oggetto dispositivo*</span><span class="sxs-lookup"><span data-stu-id="db2f7-125">**nx_lwm2m_client_device_callbacks_set**: *Set Device Object application callbacks*</span></span>
- <span data-ttu-id="db2f7-126">**nx_lwm2m_client_device_error_push**: *aggiungere il codice di errore all'oggetto dispositivo*</span><span class="sxs-lookup"><span data-stu-id="db2f7-126">**nx_lwm2m_client_device_error_push**: *Add error code to Device Object*</span></span>
- <span data-ttu-id="db2f7-127">**nx_lwm2m_client_device_error_reset**: *Reimposta i codici di errore dell'oggetto dispositivo*</span><span class="sxs-lookup"><span data-stu-id="db2f7-127">**nx_lwm2m_client_device_error_reset**: *Reset error codes of Device Object*</span></span>
- <span data-ttu-id="db2f7-128">**nx_lwm2m_client_device_resource_changed**: *modifica del segnale della risorsa oggetto dispositivo*</span><span class="sxs-lookup"><span data-stu-id="db2f7-128">**nx_lwm2m_client_device_resource_changed**: *Signal change of Device Object resource*</span></span>

### <a name="custom-objects-implementation"></a><span data-ttu-id="db2f7-129">Implementazione di oggetti personalizzati</span><span class="sxs-lookup"><span data-stu-id="db2f7-129">Custom Objects Implementation</span></span>

- <span data-ttu-id="db2f7-130">**nx_lwm2m_object_resource_changed**: *modifica del segnale di un valore di risorsa di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-130">**nx_lwm2m_object_resource_changed**: *Signal change of a resource value of an Object Instance*</span></span>

### <a name="local-device-management"></a><span data-ttu-id="db2f7-131">Gestione dei dispositivi locali</span><span class="sxs-lookup"><span data-stu-id="db2f7-131">Local Device Management</span></span>

- <span data-ttu-id="db2f7-132">**nx_lwm2m_client_object_create**: *creare una nuova istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-132">**nx_lwm2m_client_object_create**: *Create a new Object Instance*</span></span>
- <span data-ttu-id="db2f7-133">**nx_lwm2m_client_object_delete**: *eliminare un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-133">**nx_lwm2m_client_object_delete**: *Delete an Object Instance*</span></span>
- <span data-ttu-id="db2f7-134">**nx_lwm2m_client_object_discover**: *individuazione delle risorse di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-134">**nx_lwm2m_client_object_discover**: *Discover resources of an Object Instance*</span></span>
- <span data-ttu-id="db2f7-135">**nx_lwm2m_client_object_execute**: *eseguire la risorsa di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-135">**nx_lwm2m_client_object_execute**: *Execute resource of an Object Instance*</span></span>
- <span data-ttu-id="db2f7-136">**nx_lwm2m_client_object_get_next**: *Ottiene l'elenco di oggetti implementati dal client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="db2f7-136">**nx_lwm2m_client_object_get_next**: *Get the list of Objects implemented by the LWM2M Client*</span></span>
- <span data-ttu-id="db2f7-137">**nx_lwm2m_client_object_instance_get_next**: *Ottiene l'elenco di istanze di un oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-137">**nx_lwm2m_client_object_instance_get_next**: *Get the list of Instances of an Object*</span></span>
- <span data-ttu-id="db2f7-138">**nx_lwm2m_client_object_read**: *leggere i valori delle risorse di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-138">**nx_lwm2m_client_object_read**: *Read resources values of an Object Instance*</span></span>
- <span data-ttu-id="db2f7-139">**nx_lwm2m_client_object_write**: *modificare i valori delle risorse di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-139">**nx_lwm2m_client_object_write**: *Change resources values of an Object instance*</span></span>

### <a name="resources-values-decoding"></a><span data-ttu-id="db2f7-140">Decodifica dei valori delle risorse</span><span class="sxs-lookup"><span data-stu-id="db2f7-140">Resources Values Decoding</span></span>

- <span data-ttu-id="db2f7-141">**nx_lwm2m_resource_get_boolean**: *recuperare il valore di una risorsa booleana*</span><span class="sxs-lookup"><span data-stu-id="db2f7-141">**nx_lwm2m_resource_get_boolean**: *Get the value of a Boolean Resource*</span></span>
- <span data-ttu-id="db2f7-142">**nx_lwm2m_resource_get_float32**: *ottiene il valore di una risorsa a virgola mobile a 32 bit*</span><span class="sxs-lookup"><span data-stu-id="db2f7-142">**nx_lwm2m_resource_get_float32**: *Get the value of a 32-bit Floating Point Resource*</span></span>
- <span data-ttu-id="db2f7-143">**nx_lwm2m_resource_get_float64**: *ottiene il valore di una risorsa a virgola mobile a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="db2f7-143">**nx_lwm2m_resource_get_float64**: *Get the value of a 64-bit Floating Point Resource*</span></span>
- <span data-ttu-id="db2f7-144">**nx_lwm2m_resource_get_integer32**: *recuperare il valore di una risorsa Integer a 32 bit*</span><span class="sxs-lookup"><span data-stu-id="db2f7-144">**nx_lwm2m_resource_get_integer32**: *Get the value of a 32-Bit Integer Resource*</span></span>
- <span data-ttu-id="db2f7-145">**nx_lwm2m_resource_get_integer64**: *recuperare il valore di una risorsa Integer a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="db2f7-145">**nx_lwm2m_resource_get_integer64**: *Get the value of a 64-Bit Integer Resource*</span></span>
- <span data-ttu-id="db2f7-146">**nx_lwm2m_resource_get_objlnk**: *recuperare il valore di una risorsa di collegamento a un oggetto*</span><span class="sxs-lookup"><span data-stu-id="db2f7-146">**nx_lwm2m_resource_get_objlnk**: *Get the value of an Object Link Resource*</span></span>
- <span data-ttu-id="db2f7-147">**nx_lwm2m_resource_get_opaque**: *recuperare il valore di una risorsa opaca*</span><span class="sxs-lookup"><span data-stu-id="db2f7-147">**nx_lwm2m_resource_get_opaque**: *Get the value of an Opaque Resource*</span></span>
- <span data-ttu-id="db2f7-148">**nx_lwm2m_resource_get_string**: *recuperare il valore di una risorsa di stringa*</span><span class="sxs-lookup"><span data-stu-id="db2f7-148">**nx_lwm2m_resource_get_string**: *Get the value of a String Resource*</span></span>
- <span data-ttu-id="db2f7-149">**nx_lwm2m_resource_multiple_get_boolean**: *recuperare il valore di una risorsa booleana per più istanze di risorse*</span><span class="sxs-lookup"><span data-stu-id="db2f7-149">**nx_lwm2m_resource_multiple_get_boolean**: *Get the value of a Boolean Resource Multiple Resource Instance*</span></span>
- <span data-ttu-id="db2f7-150">**nx_lwm2m_resource_multiple_get_float32**: *ottiene il valore di un'istanza a virgola mobile a virgola mobile a 32 bit*</span><span class="sxs-lookup"><span data-stu-id="db2f7-150">**nx_lwm2m_resource_multiple_get_float32**: *Get the value of a 32-bit Floating Point Multiple Resource Instance*</span></span>
- <span data-ttu-id="db2f7-151">**nx_lwm2m_resource_multiple_get_float64**: *ottiene il valore di un'istanza a virgola mobile a virgola mobile a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="db2f7-151">**nx_lwm2m_resource_multiple_get_float64**: *Get the value of a 64-bit Floating Point Multiple Resource Instance*</span></span>
- <span data-ttu-id="db2f7-152">**nx_lwm2m_resource_multiple_get_integer32**: *ottiene il valore di un'istanza di risorsa Integer a 32 bit*</span><span class="sxs-lookup"><span data-stu-id="db2f7-152">**nx_lwm2m_resource_multiple_get_integer32**: *Get the value of a 32-Bit Integer Multiple Resource Instance*</span></span>
- <span data-ttu-id="db2f7-153">**nx_lwm2m_resource_multiple_get_integer64**: *ottiene il valore di un'istanza di risorsa Integer a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="db2f7-153">**nx_lwm2m_resource_multiple_get_integer64**: *Get the value of a 64-Bit Integer Multiple Resource Instance*</span></span>
- <span data-ttu-id="db2f7-154">**nx_lwm2m_resource_multiple_get_objlnk**: *recuperare il valore di un oggetto collegamento a più istanze di risorse*</span><span class="sxs-lookup"><span data-stu-id="db2f7-154">**nx_lwm2m_resource_multiple_get_objlnk**: *Get the value of an Object Link Multiple Resource Instance*</span></span>
- <span data-ttu-id="db2f7-155">**nx_lwm2m_resource_multiple_get_opaque**: *ottiene il valore di un'istanza di più risorse opaca*</span><span class="sxs-lookup"><span data-stu-id="db2f7-155">**nx_lwm2m_resource_multiple_get_opaque**: *Get the value of an Opaque Multiple Resource Instance*</span></span>
- <span data-ttu-id="db2f7-156">**nx_lwm2m_resource_multiple_get_string**: *recuperare il valore di una stringa con più istanze di risorse*</span><span class="sxs-lookup"><span data-stu-id="db2f7-156">**nx_lwm2m_resource_multiple_get_string**: *Get the value of a String Multiple Resource Instance*</span></span>

### <a name="firmware-update-object"></a><span data-ttu-id="db2f7-157">Oggetto di aggiornamento del firmware</span><span class="sxs-lookup"><span data-stu-id="db2f7-157">Firmware Update Object</span></span>

- <span data-ttu-id="db2f7-158">**nx_lwm2m_firmware_create**: *creare un oggetto di aggiornamento del firmware*</span><span class="sxs-lookup"><span data-stu-id="db2f7-158">**nx_lwm2m_firmware_create**: *Create Firmware Update Object*</span></span>
- <span data-ttu-id="db2f7-159">**nx_lwm2m_firmware_package_info_set**: *impostare le informazioni sul pacchetto di aggiornamento del firmware*</span><span class="sxs-lookup"><span data-stu-id="db2f7-159">**nx_lwm2m_firmware_package_info_set**: *Set Firmware Update Package Information*</span></span>
- <span data-ttu-id="db2f7-160">**nx_lwm2m_firmware_result_set**: *impostare il risultato dell'aggiornamento del firmware*</span><span class="sxs-lookup"><span data-stu-id="db2f7-160">**nx_lwm2m_firmware_result_set**: *Set Firmware Update Result*</span></span>
- <span data-ttu-id="db2f7-161">**nx_lwm2m_firmware_state_set**: *impostare lo stato di aggiornamento del firmware*</span><span class="sxs-lookup"><span data-stu-id="db2f7-161">**nx_lwm2m_firmware_state_set**: *Set Firmware Update State*</span></span>

## <a name="nx_lwm2m_client_create"></a><span data-ttu-id="db2f7-162">nx_lwm2m_client_create</span><span class="sxs-lookup"><span data-stu-id="db2f7-162">nx_lwm2m_client_create</span></span>

<span data-ttu-id="db2f7-163">Crea client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-163">Create LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-164">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-164">Prototype</span></span>

```c
UINT nx_lwm2m_client_create(NX_LWM2M_CLIENT *client_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr, UINT local_port, const CHAR *name_ptr,
    const CHAR *msisdn_ptr, UCHAR binding_modes, VOID *stack_ptr, ULONG stack_size);
```

### <a name="description"></a><span data-ttu-id="db2f7-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-165">Description</span></span>

<span data-ttu-id="db2f7-166">Questo servizio crea un'istanza del client LWM2M, che viene eseguita nel contesto del proprio thread ThreadX.</span><span class="sxs-lookup"><span data-stu-id="db2f7-166">This service creates a LWM2M Client instance, which runs in the context of its own ThreadX thread.</span></span>

<span data-ttu-id="db2f7-167">Il client LWM2M implementa i seguenti oggetti LWM2M OMA: Security (0), server (1), controllo di accesso (2) e Device (3).</span><span class="sxs-lookup"><span data-stu-id="db2f7-167">The LWM2M Client implements the following OMA LWM2M Objects: Security (0), Server (1), Access Control (2) and Device (3).</span></span> <span data-ttu-id="db2f7-168">Le altre implementazioni di oggetti devono essere aggiunte dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-168">The other objects implementations must be added by the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-169">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-169">Parameters</span></span>

- <span data-ttu-id="db2f7-170">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-170">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-171">**ip_ptr**: puntatore all'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-171">**ip_ptr**: Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="db2f7-172">**packet_pool_ptr**: puntatore al pool di pacchetti predefinito per il client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-172">**packet_pool_ptr**: Pointer to the default packet pool for this LWM2M Client.</span></span>
- <span data-ttu-id="db2f7-173">**local_port**: porta UDP locale utilizzata per la comunicazione non protetta.</span><span class="sxs-lookup"><span data-stu-id="db2f7-173">**local_port**: The local UDP port used for non-secure communication.</span></span>
- <span data-ttu-id="db2f7-174">**name_ptr**: puntatore al nome dell'endpoint del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-174">**name_ptr**: Pointer to LWM2M Client endpoint name.</span></span>
- <span data-ttu-id="db2f7-175">**msisdn_ptr**: puntatore a MSISDN in cui è possibile raggiungere il client LWM2M per l'utilizzo con l'associazione SMS, può essere null se l'associazione SMS non è supportata.</span><span class="sxs-lookup"><span data-stu-id="db2f7-175">**msisdn_ptr**: Pointer to the MSISDN where the LWM2M Client can be reached for use with the SMS binding, can be NULL if SMS binding is not supported.</span></span>
- <span data-ttu-id="db2f7-176">**binding_modes**: l'associazione e le modalità supportate dal client LWM2M devono essere una combinazione di flag NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S e NX_LWM2M_BINDING_SQ.</span><span class="sxs-lookup"><span data-stu-id="db2f7-176">**binding_modes**: The binding and modes supported by the LWM2M Client, must be a combination of NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S and NX_LWM2M_BINDING_SQ flags.</span></span>
- <span data-ttu-id="db2f7-177">**stack_ptr**: puntatore all'area dello stack di thread del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-177">**stack_ptr**: Pointer to LWM2M Client thread stack area.</span></span>
- <span data-ttu-id="db2f7-178">**stack_size**: dimensioni dello stack dei thread del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-178">**stack_size**: The LWM2M Client thread stack size.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-179">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-179">Return Values</span></span>

- <span data-ttu-id="db2f7-180">**NX_SUCCESS**: il client LWM2M è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="db2f7-180">**NX_SUCCESS**: The LWM2M Client has been successfully created.</span></span>
- <span data-ttu-id="db2f7-181">**NX_LWM2M_ERROR**: errore di creazione del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-181">**NX_LWM2M_ERROR**: LWM2M Client create error.</span></span>
- <span data-ttu-id="db2f7-182">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-182">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_delete"></a><span data-ttu-id="db2f7-183">nx_lwm2m_client_delete</span><span class="sxs-lookup"><span data-stu-id="db2f7-183">nx_lwm2m_client_delete</span></span>

<span data-ttu-id="db2f7-184">Elimina client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-184">Delete LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-185">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-185">Prototype</span></span>

```c
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-186">Description</span></span>

<span data-ttu-id="db2f7-187">Questo servizio Elimina un'istanza del client LWM2M creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-187">This service deletes a previously created LWM2M Client instance.</span></span>

<span data-ttu-id="db2f7-188">Tutte le sessioni attualmente associate al client vengono eliminate anche da questa chiamata.</span><span class="sxs-lookup"><span data-stu-id="db2f7-188">All sessions currently attached the client are also deleted by this call.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-189">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-189">Parameters</span></span>

- <span data-ttu-id="db2f7-190">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-190">**client_ptr**: Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-191">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-191">Return Values</span></span>

- <span data-ttu-id="db2f7-192">**NX_SUCCESS**: il client LWM2M è stato eliminato correttamente.</span><span class="sxs-lookup"><span data-stu-id="db2f7-192">**NX_SUCCESS**: The LWM2M Client has been successfully deleted.</span></span>
- <span data-ttu-id="db2f7-193">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-193">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_device_callbacks_set"></a><span data-ttu-id="db2f7-194">nx_lwm2m_client_device_callbacks_set</span><span class="sxs-lookup"><span data-stu-id="db2f7-194">nx_lwm2m_client_device_callbacks_set</span></span>

<span data-ttu-id="db2f7-195">Imposta callback applicazione oggetto dispositivo</span><span class="sxs-lookup"><span data-stu-id="db2f7-195">Set Device Object application callbacks</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-196">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-196">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_READ_CALLBACK read_callback,
    NX_LWM2M_CLIENT_DEVICE_DISCOVER_CALLBACK discover_callback,
    NX_LWM2M_CLIENT_DEVICE_WRITE_CALLBACK write_callback,
    NX_LWM2M_CLIENT_DEVICE_EXECUTE_CALLBACK execute_callback);
```

### <a name="description"></a><span data-ttu-id="db2f7-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-197">Description</span></span>

<span data-ttu-id="db2f7-198">Questo servizio installa i callback dell'applicazione per l'implementazione di operazioni sulle risorse dell'oggetto dispositivo LWM2M che non sono gestite dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-198">This service installs the application callbacks for implementing operations on the LWM2M Device Object resources that are not handled by the LWM2M Client.</span></span>

<span data-ttu-id="db2f7-199">Il client LWM2M implementa le risorse seguenti: codice errore (11), Reimposta codice errore (12), binding supportato e modalità (16), le operazioni per le altre risorse vengono reindirizzate all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-199">The LWM2M Client implements the following resources : Error Code (11), Reset Error Code (12) and Supported Binding and Modes (16), operations to the other resources are redirected to the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-200">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-200">Parameters</span></span>

- <span data-ttu-id="db2f7-201">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-201">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-202">**Read_Callback**: callback del metodo ' Read '.</span><span class="sxs-lookup"><span data-stu-id="db2f7-202">**read_callback**: The 'Read' method callback.</span></span>
- <span data-ttu-id="db2f7-203">**discover_callback**: callback del metodo ' Discover '.</span><span class="sxs-lookup"><span data-stu-id="db2f7-203">**discover_callback**: The 'Discover' method callback.</span></span>
- <span data-ttu-id="db2f7-204">**write_callback**: callback del metodo ' Write '.</span><span class="sxs-lookup"><span data-stu-id="db2f7-204">**write_callback**: The 'Write' method callback.</span></span>
- <span data-ttu-id="db2f7-205">**execute_callback**: callback del metodo ' Execute '.</span><span class="sxs-lookup"><span data-stu-id="db2f7-205">**execute_callback**: The 'Execute' method callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-206">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-206">Return Values</span></span>

- <span data-ttu-id="db2f7-207">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-207">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-208">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-208">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_device_error_push"></a><span data-ttu-id="db2f7-209">nx_lwm2m_client_device_error_push</span><span class="sxs-lookup"><span data-stu-id="db2f7-209">nx_lwm2m_client_device_error_push</span></span>

<span data-ttu-id="db2f7-210">Aggiungere il codice di errore all'oggetto dispositivo</span><span class="sxs-lookup"><span data-stu-id="db2f7-210">Add error code to Device Object</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-211">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-211">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_error_push(NX_LWM2M_CLIENT *client_ptr, UCHAR code);
```

### <a name="description"></a><span data-ttu-id="db2f7-212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-212">Description</span></span>

<span data-ttu-id="db2f7-213">Questo servizio aggiunge una nuova istanza alla risorsa del codice di errore (11) del dispositivo dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-213">This service adds a new instance to the Error Code (11) resource of the Object Device.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-214">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-214">Parameters</span></span>

- <span data-ttu-id="db2f7-215">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-215">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-216">**Code**: nuovo codice di errore.</span><span class="sxs-lookup"><span data-stu-id="db2f7-216">**code**: The new error code.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-217">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-217">Return Values</span></span>

- <span data-ttu-id="db2f7-218">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-218">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-219">**NX_LWM2M_BUFFER_TOO_SMALL**: è stato raggiunto il numero massimo di codici di errore archiviati.</span><span class="sxs-lookup"><span data-stu-id="db2f7-219">**NX_LWM2M_BUFFER_TOO_SMALL**: The maximum number of stored error codes has been reached.</span></span>
- <span data-ttu-id="db2f7-220">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-220">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_device_error_reset"></a><span data-ttu-id="db2f7-221">nx_lwm2m_client_device_error_reset</span><span class="sxs-lookup"><span data-stu-id="db2f7-221">nx_lwm2m_client_device_error_reset</span></span>

<span data-ttu-id="db2f7-222">Reimposta i codici di errore dell'oggetto dispositivo</span><span class="sxs-lookup"><span data-stu-id="db2f7-222">Reset error codes of Device Object</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-223">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-223">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-224">Description</span></span>

<span data-ttu-id="db2f7-225">Questo servizio Elimina tutte le istanze di risorse del codice di errore dall'oggetto dispositivo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-225">This service deletes all error code resource instances from the Device Object.</span></span> <span data-ttu-id="db2f7-226">Equivale a eseguire il codice di errore di reimpostazione della risorsa (12).</span><span class="sxs-lookup"><span data-stu-id="db2f7-226">This is equivalent to executing the resource Reset Error Code (12).</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-227">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-227">Parameters</span></span>

- <span data-ttu-id="db2f7-228">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-228">**client_ptr**: Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-229">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-229">Return Values</span></span>

- <span data-ttu-id="db2f7-230">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-230">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-231">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-231">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_device_resource_changed"></a><span data-ttu-id="db2f7-232">nx_lwm2m_client_device_resource_changed</span><span class="sxs-lookup"><span data-stu-id="db2f7-232">nx_lwm2m_client_device_resource_changed</span></span>

<span data-ttu-id="db2f7-233">Modifica del segnale della risorsa oggetto dispositivo</span><span class="sxs-lookup"><span data-stu-id="db2f7-233">Signal change of Device Object resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-234">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-234">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_resource_changed(NX_LWM2M_CLIENT *client_ptr,
                                    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a><span data-ttu-id="db2f7-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-235">Description</span></span>

<span data-ttu-id="db2f7-236">Il servizio viene usato dall'applicazione per segnalare al client LWM2M che una risorsa del dispositivo oggetto è cambiata.</span><span class="sxs-lookup"><span data-stu-id="db2f7-236">The service is used by the application to signal to the LWM2M Client that a resource of the Object Device has changed.</span></span> <span data-ttu-id="db2f7-237">Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-237">The LWM2M Client will send a notification if the resource is observed by a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-238">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-238">Parameters</span></span>

- <span data-ttu-id="db2f7-239">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-239">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-240">**Resource**: puntatore alla struttura che descrive la risorsa che è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="db2f7-240">**resource**: Pointer to the structure describing the resource that has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-241">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-241">Return Values</span></span>

- <span data-ttu-id="db2f7-242">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-242">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-243">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-243">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_lock"></a><span data-ttu-id="db2f7-244">nx_lwm2m_client_lock</span><span class="sxs-lookup"><span data-stu-id="db2f7-244">nx_lwm2m_client_lock</span></span>

<span data-ttu-id="db2f7-245">Blocca client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-245">Lock LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-246">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-246">Prototype</span></span>

```c
UINT nx_lwm2m_client_lock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-247">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-247">Description</span></span>

<span data-ttu-id="db2f7-248">Questo servizio blocca il client LWM2M per impedire l'accesso concurent agli oggetti LWM2M dai server o da un altro thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-248">This service locks the LWM2M Client to prevent concurent access to the LWM2M objects from the servers or another application thread.</span></span>

<span data-ttu-id="db2f7-249">Se il client LWM2M è attualmente bloccato da un altro thread, la funzione si bloccherà fino a quando non viene sbloccato il client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-249">If the LWM2M Client is currently locked by another thread, the function will block until the LWM2M Client is unlocked.</span></span>

<span data-ttu-id="db2f7-250">È possibile nidificare le chiamate alle coppie nx_lwm2m_client_lock ()/nx_lwm2m_client_unlock ().</span><span class="sxs-lookup"><span data-stu-id="db2f7-250">Calls to nx_lwm2m_client_lock()/nx_lwm2m_client_unlock() pairs can be nested.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-251">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-251">Parameters</span></span>

- <span data-ttu-id="db2f7-252">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-252">**client_ptr**: Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-253">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-253">Return Values</span></span>

- <span data-ttu-id="db2f7-254">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-254">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-255">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-255">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_add"></a><span data-ttu-id="db2f7-256">nx_lwm2m_client_object_add</span><span class="sxs-lookup"><span data-stu-id="db2f7-256">nx_lwm2m_client_object_add</span></span>

<span data-ttu-id="db2f7-257">Aggiungere l'implementazione dell'oggetto al client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-257">Add Object implementation to the LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-258">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-258">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_add(NX_LWM2M_CLIENT *client_ptr,
                                NX_LWM2M_OBJECT *object_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-259">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-259">Description</span></span>

<span data-ttu-id="db2f7-260">Questo servizio aggiunge una nuova implementazione dell'oggetto al client di LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-260">This service adds a new Object implementation to the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-261">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-261">Parameters</span></span>

- <span data-ttu-id="db2f7-262">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-262">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-263">**object_ptr**: puntatore alla struttura che definisce l'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-263">**object_ptr**: Pointer to the structure defining the Object implementation.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-264">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-264">Return Values</span></span>

- <span data-ttu-id="db2f7-265">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-265">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-266">**NX_LWM2M_ALREADY_EXIST**: l'ID oggetto esiste già.</span><span class="sxs-lookup"><span data-stu-id="db2f7-266">**NX_LWM2M_ALREADY_EXIST**: The Object ID already exists.</span></span>
- <span data-ttu-id="db2f7-267">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-267">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_create"></a><span data-ttu-id="db2f7-268">nx_lwm2m_client_object_create</span><span class="sxs-lookup"><span data-stu-id="db2f7-268">nx_lwm2m_client_object_create</span></span>

<span data-ttu-id="db2f7-269">Creare una nuova istanza dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-269">Create a new Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-270">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-270">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_create(NX_LWM2M_CLIENT *client_ptr,
            NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr,
            UINT num_values, const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-271">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-271">Description</span></span>

<span data-ttu-id="db2f7-272">Questo servizio esegue un'operazione di creazione su un oggetto del client LWM2M per creare una nuova istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-272">This service performs a 'Create' operation on an Object of the LWM2M Client to create a new Object Instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-273">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-273">Parameters</span></span>

- <span data-ttu-id="db2f7-274">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-274">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-275">**object_id**: ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-275">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="db2f7-276">**instance_id_ptr**: puntatore all'ID della nuova istanza, può essere null se il client LWM2M deve assegnare un ID istanza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-276">**instance_id_ptr**: Pointer to the ID of the new instance, can be NULL if the LWM2M Client must assign an Instance ID.</span></span> <span data-ttu-id="db2f7-277">Se l'ID è il valore riservato 65535, il client LWM2M assegnerà un ID istanza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-277">If the ID is the reserved value 65535 the LWM2M Client will assign an Instance ID.</span></span> <span data-ttu-id="db2f7-278">Se non è NULL, l'ID assegnato viene restituito dopo la chiamata.</span><span class="sxs-lookup"><span data-stu-id="db2f7-278">If not NULL the assigned ID is returned after the call.</span></span>
- <span data-ttu-id="db2f7-279">**num_values**: numero di valori da impostare.</span><span class="sxs-lookup"><span data-stu-id="db2f7-279">**num_values**: The number of values to set.</span></span>
- <span data-ttu-id="db2f7-280">**values_ptr**: puntatore a una matrice di valori di risorsa per inizializzare la nuova istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-280">**values_ptr**: Pointer to an array of resource values to initialize the new Object Instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-281">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-281">Return Values</span></span>

- <span data-ttu-id="db2f7-282">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-282">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-283">**NX_LWM2M_ALREADY_EXIST**: l'ID dell'istanza dell'oggetto esiste già.</span><span class="sxs-lookup"><span data-stu-id="db2f7-283">**NX_LWM2M_ALREADY_EXIST**: The Object Instance ID already exists.</span></span>
- <span data-ttu-id="db2f7-284">**NX_LWM2M_METHOD_NOT_ALLOWED**: l'oggetto non supporta la creazione di istanze.</span><span class="sxs-lookup"><span data-stu-id="db2f7-284">**NX_LWM2M_METHOD_NOT_ALLOWED**: The Object doesn't support instance creation.</span></span>
- <span data-ttu-id="db2f7-285">**NX_LWM2M_NO_MEMORY**: non è possibile allocare memoria per archiviare la nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-285">**NX_LWM2M_NO_MEMORY**: Cannot allocate memory to store the new instance.</span></span>
- <span data-ttu-id="db2f7-286">**NX_LWM2M_NOT_FOUND**: l'ID oggetto non esiste.</span><span class="sxs-lookup"><span data-stu-id="db2f7-286">**NX_LWM2M_NOT_FOUND**: The Object ID doesn't exist.</span></span>
- <span data-ttu-id="db2f7-287">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-287">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_delete"></a><span data-ttu-id="db2f7-288">nx_lwm2m_client_object_delete</span><span class="sxs-lookup"><span data-stu-id="db2f7-288">nx_lwm2m_client_object_delete</span></span>

<span data-ttu-id="db2f7-289">Eliminare un'istanza di oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-289">Delete an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-290">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-290">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_delete(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id);
```

### <a name="description"></a><span data-ttu-id="db2f7-291">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-291">Description</span></span>

<span data-ttu-id="db2f7-292">Questo servizio esegue un'operazione di eliminazione su un'istanza di oggetto del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-292">This service performs a 'Delete' operation on an Object Instance of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-293">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-293">Parameters</span></span>

- <span data-ttu-id="db2f7-294">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-294">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-295">**object_id**: ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-295">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="db2f7-296">**Instance_Id**: ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-296">**instance_id**: The Object Instance ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-297">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-297">Return Values</span></span>

- <span data-ttu-id="db2f7-298">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-298">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-299">**NX_LWM2M_METHOD_NOT_ALLOWED**: l'oggetto non supporta l'eliminazione dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-299">**NX_LWM2M_METHOD_NOT_ALLOWED**: The Object doesn't support instance deletion.</span></span>
- <span data-ttu-id="db2f7-300">**NX_LWM2M_NOT_FOUND**: l'ID oggetto o l'ID istanza oggetto non esiste.</span><span class="sxs-lookup"><span data-stu-id="db2f7-300">**NX_LWM2M_NOT_FOUND**: The Object ID or Object Instance ID doesn't exist.</span></span>
- <span data-ttu-id="db2f7-301">NX_PTR_ERROR puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-301">NX_PTR_ERROR Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_discover"></a><span data-ttu-id="db2f7-302">nx_lwm2m_client_object_discover</span><span class="sxs-lookup"><span data-stu-id="db2f7-302">nx_lwm2m_client_object_discover</span></span>

<span data-ttu-id="db2f7-303">Individuare le risorse di un'istanza dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-303">Discover resources of an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-304">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-304">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_discover(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT *num_resources_ptr, NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-305">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-305">Description</span></span>

<span data-ttu-id="db2f7-306">Questo servizio esegue un'operazione di individuazione su un'istanza dell'oggetto del client LWM2M, restituisce l'elenco delle risorse implementate dall'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-306">This service performs a 'Discover' operation on an Object Instance of the LWM2M Client, this returns the list of resources implemented by the Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-307">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-307">Parameters</span></span>

- <span data-ttu-id="db2f7-308">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-308">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-309">**object_id**: ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-309">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="db2f7-310">**Instance_Id**: ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-310">**instance_id**: The Object Instance ID.</span></span>
- <span data-ttu-id="db2f7-311">**num_resources_ptr**: in input la dimensione del buffer di destinazione, in output il numero di elementi scritti nel buffer.</span><span class="sxs-lookup"><span data-stu-id="db2f7-311">**num_resources_ptr**: On input the size of the destination buffer, on output the number of elements writen to the buffer.</span></span>
- <span data-ttu-id="db2f7-312">**resources_ptr**: puntatore al buffer di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-312">**resources_ptr**: Pointer to the destination buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-313">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-313">Return Values</span></span>

- <span data-ttu-id="db2f7-314">**NX_SUCCESS**: operazione riuscita..</span><span class="sxs-lookup"><span data-stu-id="db2f7-314">**NX_SUCCESS**: Successful operation..</span></span>
- <span data-ttu-id="db2f7-315">**NX_LWM2M_BUFFER_TOO_SMALL**: il buffer di risorse è troppo piccolo per archiviare l'elenco di risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-315">**NX_LWM2M_BUFFER_TOO_SMALL**: The resources buffer is too small to store the list of resources.</span></span>
- <span data-ttu-id="db2f7-316">**NX_LWM2M_NOT_FOUND**: l'ID oggetto o l'ID istanza oggetto non esiste.</span><span class="sxs-lookup"><span data-stu-id="db2f7-316">**NX_LWM2M_NOT_FOUND**: The Object ID or Object Instance ID doesn't exist.</span></span>
- <span data-ttu-id="db2f7-317">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-317">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_execute"></a><span data-ttu-id="db2f7-318">nx_lwm2m_client_object_execute</span><span class="sxs-lookup"><span data-stu-id="db2f7-318">nx_lwm2m_client_object_execute</span></span>

<span data-ttu-id="db2f7-319">Esegui risorsa di un'istanza dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-319">Execute resource of an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-320">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-320">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_execute(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr, UINT arguments_length);
```

### <a name="description"></a><span data-ttu-id="db2f7-321">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-321">Description</span></span>

<span data-ttu-id="db2f7-322">Questo servizio esegue l'operazione di esecuzione su una risorsa dell'istanza di oggetto del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-322">This service performs the 'Execute' operation on an Object Instance Resource of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-323">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-323">Parameters</span></span>

- <span data-ttu-id="db2f7-324">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-324">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-325">**object_id**: ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-325">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="db2f7-326">**Instance_Id**: ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-326">**instance_id**: The Object Instance ID.</span></span>
- <span data-ttu-id="db2f7-327">**resource_id**: ID risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-327">**resource_id**: The Resource ID.</span></span>
- <span data-ttu-id="db2f7-328">**arguments_ptr**: puntatore agli argomenti dell'operazione di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-328">**arguments_ptr**: Pointer to the arguments of the execute operation.</span></span> <span data-ttu-id="db2f7-329">Può essere NULL se arguments_length è zero.</span><span class="sxs-lookup"><span data-stu-id="db2f7-329">Can be NULL if arguments_length is zero.</span></span>
- <span data-ttu-id="db2f7-330">**arguments_length**: lunghezza degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="db2f7-330">**arguments_length**: The length of the arguments.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-331">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-331">Return Values</span></span>

- <span data-ttu-id="db2f7-332">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-332">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-333">**NX_LWM2M_METHOD_NOT_ALLOWED**: la risorsa non supporta l'operazione di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-333">**NX_LWM2M_METHOD_NOT_ALLOWED**: The resource doesn't support the execute operation.</span></span>
- <span data-ttu-id="db2f7-334">**NX_LWM2M_NOT_FOUND**: ID oggetto, ID istanza oggetto o ID risorsa inesistente.</span><span class="sxs-lookup"><span data-stu-id="db2f7-334">**NX_LWM2M_NOT_FOUND**: The Object ID, Object Instance ID or the resource ID doesn't exist.</span></span>
- <span data-ttu-id="db2f7-335">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-335">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_get_next"></a><span data-ttu-id="db2f7-336">nx_lwm2m_client_object_get_next</span><span class="sxs-lookup"><span data-stu-id="db2f7-336">nx_lwm2m_client_object_get_next</span></span>

<span data-ttu-id="db2f7-337">Ottenere l'elenco di oggetti implementati dal client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-337">Get the list of Objects implemented by the LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-338">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-338">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_get_next(NX_LWM2M_CLIENT *client_ptr,
                                    NX_LWM2M_ID *object_id_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-339">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-339">Description</span></span>

<span data-ttu-id="db2f7-340">Questo servizio restituisce l'ID dell'oggetto successivo implementato dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-340">This service returns the ID of the next Object implemented by the LWM2M Client.</span></span> <span data-ttu-id="db2f7-341">Se l'ID oggetto corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito il primo ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-341">If the current Object ID is set to NX_LWM2M_RESERVED_ID (65535) the first Object ID is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-342">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-342">Parameters</span></span>

- <span data-ttu-id="db2f7-343">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-343">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-344">**object_id_ptr**: puntatore all'ID dell'oggetto corrente.</span><span class="sxs-lookup"><span data-stu-id="db2f7-344">**object_id_ptr**: Pointer to the current Object ID.</span></span> <span data-ttu-id="db2f7-345">Il risultato restituito contiene l'ID oggetto successivo implementato dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-345">On return contains the next Object ID implemented by the LWM2M Client.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-346">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-346">Return Values</span></span>

- <span data-ttu-id="db2f7-347">**NX_SUCCESS**: operazione riuscita..</span><span class="sxs-lookup"><span data-stu-id="db2f7-347">**NX_SUCCESS**: Successful operation..</span></span>
- <span data-ttu-id="db2f7-348">**NX_LWM2M_NOT_FOUND**: l'ID oggetto specificato è l'ultimo del database.</span><span class="sxs-lookup"><span data-stu-id="db2f7-348">**NX_LWM2M_NOT_FOUND**: The given Object ID is the last of the database.</span></span>
- <span data-ttu-id="db2f7-349">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-349">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_instance_get_next"></a><span data-ttu-id="db2f7-350">nx_lwm2m_client_object_instance_get_next</span><span class="sxs-lookup"><span data-stu-id="db2f7-350">nx_lwm2m_client_object_instance_get_next</span></span>

<span data-ttu-id="db2f7-351">Ottiene l'elenco di istanze di un oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-351">Get the list of Instances of an Object</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-352">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-352">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_instance_get_next(NX_LWM2M_CLIENT *client_ptr,
                    NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-353">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-353">Description</span></span>

<span data-ttu-id="db2f7-354">Questo servizio restituisce l'ID dell'istanza di oggetto successiva dell'oggetto specificato.</span><span class="sxs-lookup"><span data-stu-id="db2f7-354">This service returns the ID of the next Object Instance of the given Object.</span></span> <span data-ttu-id="db2f7-355">Se l'ID istanza corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito l'ID della prima istanza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-355">If the current Instance ID is set to NX_LWM2M_RESERVED_ID (65535) the ID of the first instance is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-356">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-356">Parameters</span></span>

- <span data-ttu-id="db2f7-357">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-357">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-358">**object_id**: ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-358">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="db2f7-359">**instance_id_ptr**: puntatore all'ID dell'istanza dell'oggetto corrente.</span><span class="sxs-lookup"><span data-stu-id="db2f7-359">**instance_id_ptr**: Pointer to the current Object Instance ID.</span></span> <span data-ttu-id="db2f7-360">In return contiene l'ID dell'istanza successiva dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-360">On return contains the next Instance ID of the Object.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-361">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-361">Return Values</span></span>

- <span data-ttu-id="db2f7-362">**NX_SUCCESS**: operazione riuscita..</span><span class="sxs-lookup"><span data-stu-id="db2f7-362">**NX_SUCCESS**: Successful operation..</span></span>
- <span data-ttu-id="db2f7-363">**NX_LWM2M_NOT_FOUND**: l'ID istanza specificato è l'ultimo dell'oggetto o l'ID oggetto non è implementato.</span><span class="sxs-lookup"><span data-stu-id="db2f7-363">**NX_LWM2M_NOT_FOUND**: The given Instance ID is the last of the object, or the Object ID is not implemented.</span></span>
- <span data-ttu-id="db2f7-364">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-364">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_read"></a><span data-ttu-id="db2f7-365">nx_lwm2m_client_object_read</span><span class="sxs-lookup"><span data-stu-id="db2f7-365">nx_lwm2m_client_object_read</span></span>

<span data-ttu-id="db2f7-366">Leggere i valori delle risorse di un'istanza dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-366">Read resources values of an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-367">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-367">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_read(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT num_values, NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a><span data-ttu-id="db2f7-368">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-368">Description</span></span>

<span data-ttu-id="db2f7-369">Questo servizio esegue un'operazione di lettura su un'istanza di oggetto del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-369">This service performs a 'Read' operation on an Object Instance of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-370">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-370">Parameters</span></span>

- <span data-ttu-id="db2f7-371">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-371">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-372">**object_id**: ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-372">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="db2f7-373">**Instance_Id**: ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-373">**instance_id**: The Object Instance ID.</span></span>
- <span data-ttu-id="db2f7-374">**num_values**: numero di risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="db2f7-374">**num_values**: The number of resources to read.</span></span>
- <span data-ttu-id="db2f7-375">**values_ptr**: puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="db2f7-375">**values_ptr**: Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources to read.</span></span> <span data-ttu-id="db2f7-376">In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="db2f7-376">On return the array is filled with the corresponding types and values.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-377">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-377">Return Values</span></span>

- <span data-ttu-id="db2f7-378">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-378">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-379">**NX_LWM2M_METHOD_NOT_ALLOWED**: una risorsa non supporta l'operazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="db2f7-379">**NX_LWM2M_METHOD_NOT_ALLOWED**: A resource doesn't support the read operation.</span></span>
- <span data-ttu-id="db2f7-380">**NX_LWM2M_NOT_FOUND**: ID oggetto, ID istanza oggetto o ID risorsa inesistente.</span><span class="sxs-lookup"><span data-stu-id="db2f7-380">**NX_LWM2M_NOT_FOUND**: The Object ID, Object Instance ID or a resource ID doesn't exist.</span></span>
- <span data-ttu-id="db2f7-381">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-381">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_write"></a><span data-ttu-id="db2f7-382">nx_lwm2m_client_object_write</span><span class="sxs-lookup"><span data-stu-id="db2f7-382">nx_lwm2m_client_object_write</span></span>

<span data-ttu-id="db2f7-383">Modificare i valori delle risorse di un'istanza dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-383">Change resources values of an Object instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-384">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-384">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_write(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, UINT num_values,
        const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

### <a name="description"></a><span data-ttu-id="db2f7-385">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-385">Description</span></span>

<span data-ttu-id="db2f7-386">Questo servizio esegue un'operazione di scrittura su un'istanza di oggetto del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-386">This service performs a 'Write' operation on an Object Instance of the LWM2M Client.</span></span>

<span data-ttu-id="db2f7-387">È possibile specificare le operazioni di scrittura seguenti per il parametro *write_op* :</span><span class="sxs-lookup"><span data-stu-id="db2f7-387">The following write operations can be specified to the *write_op* parameter:</span></span>

- <span data-ttu-id="db2f7-388">**0** &mdash; aggiornamento parziale: aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate le altre risorse esistenti,</span><span class="sxs-lookup"><span data-stu-id="db2f7-388">**0** &mdash; Partial Update: adds or updates Resources provided in the new value and leaves other existing Resources unchanged,</span></span>

- <span data-ttu-id="db2f7-389">**NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Sostituisci istanza: sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa specificati.</span><span class="sxs-lookup"><span data-stu-id="db2f7-389">**NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Replace Instance: replaces the Object Instance with the new provided resource values.</span></span>

- <span data-ttu-id="db2f7-390">**NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Sostituisci risorsa: sostituisce le risorse con i nuovi valori di risorsa forniti, usati per sostituire più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-390">**NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Replace Resource: replaces the Resources with the new provided resource values (used to replace Multiple Resources).</span></span>

- <span data-ttu-id="db2f7-391">**NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Write: indica una chiamata da una sequenza di bootstrap.</span><span class="sxs-lookup"><span data-stu-id="db2f7-391">**NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Write: indicates a call from a Bootstrap sequence.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-392">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-392">Parameters</span></span>

- <span data-ttu-id="db2f7-393">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-393">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-394">**object_id**: ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-394">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="db2f7-395">**Instance_Id**: ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-395">**instance_id**: The Object Instance ID.</span></span>
- <span data-ttu-id="db2f7-396">**num_values**: numero di risorse da scrivere.</span><span class="sxs-lookup"><span data-stu-id="db2f7-396">**num_values**: The number of resources to write.</span></span>
- <span data-ttu-id="db2f7-397">**values_ptr**: puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse, i tipi e i valori da scrivere.</span><span class="sxs-lookup"><span data-stu-id="db2f7-397">**values_ptr**: Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources, the types and the values to write.</span></span>
- <span data-ttu-id="db2f7-398">**write_op**: tipo di operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="db2f7-398">**write_op**: The type of write operation.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-399">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-399">Return Values</span></span>

- <span data-ttu-id="db2f7-400">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-400">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-401">**NX_LWM2M_BAD_ENCODING**: il tipo di una risorsa non è valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-401">**NX_LWM2M_BAD_ENCODING**: The type of a resource is not valid.</span></span>
- <span data-ttu-id="db2f7-402">**NX_LWM2M_BUFFER_TOO_SMALL**: la lunghezza di un valore è troppo grande per essere archiviata nell'istanza di.</span><span class="sxs-lookup"><span data-stu-id="db2f7-402">**NX_LWM2M_BUFFER_TOO_SMALL**: The length of a value is too big to be stored in the instance.</span></span>
- <span data-ttu-id="db2f7-403">**NX_LWM2M_METHOD_NOT_ALLOWED**: una risorsa non supporta l'operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="db2f7-403">**NX_LWM2M_METHOD_NOT_ALLOWED**: A resource doesn't support the write operation.</span></span>
- <span data-ttu-id="db2f7-404">**NX_LWM2M_NO_MEMORY**: non è possibile allocare memoria per archiviare un valore di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-404">**NX_LWM2M_NO_MEMORY**: Cannot allocate memory to store a resource value.</span></span>
- <span data-ttu-id="db2f7-405">**NX_LWM2M_NOT_ACCEPTABLE**: il valore di una risorsa non è valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-405">**NX_LWM2M_NOT_ACCEPTABLE**: The value of a resource is not valid.</span></span>
- <span data-ttu-id="db2f7-406">**NX_LWM2M_NOT_FOUND**: ID oggetto, ID istanza oggetto o ID risorsa inesistente.</span><span class="sxs-lookup"><span data-stu-id="db2f7-406">**NX_LWM2M_NOT_FOUND**: The Object ID, Object Instance ID or a resource ID doesn't exist.</span></span>
- <span data-ttu-id="db2f7-407">NX_OPTION_ERROR: tipo di operazione di scrittura non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-407">NX_OPTION_ERROR: Invalid type of write operation.</span></span>
- <span data-ttu-id="db2f7-408">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-408">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_security_key_callbacks_set"></a><span data-ttu-id="db2f7-409">nx_lwm2m_client_security_key_callbacks_set</span><span class="sxs-lookup"><span data-stu-id="db2f7-409">nx_lwm2m_client_security_key_callbacks_set</span></span>

<span data-ttu-id="db2f7-410">Imposta callback di gestione delle chiavi degli oggetti di sicurezza</span><span class="sxs-lookup"><span data-stu-id="db2f7-410">Set Security Object key management callbacks</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-411">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-411">Prototype</span></span>

```c
UINT nx_lwm2m_client_security_key_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_CLIENT_SECURITY_KEY_WRITE_CALLBACK write_callback,
                NX_LWM2M_CLIENT_SECURITY_KEY_DELETE_CALLBACK delete_callback);
```

### <a name="description"></a><span data-ttu-id="db2f7-412">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-412">Description</span></span>

<span data-ttu-id="db2f7-413">Questo servizio installa i callback dell'applicazione per l'implementazione delle operazioni sulle risorse degli oggetti di sicurezza LWM2M correlate alle chiavi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-413">This service installs the application callbacks for implementing operations on the LWM2M Security Object resources related to the security keys.</span></span>

<span data-ttu-id="db2f7-414">Il client LWM2M delega la gestione delle chiavi di sicurezza all'applicazione durante le sessioni di bootstrap. i callback verranno chiamati quando il server di bootstrap scrive o Elimina le risorse seguenti in un'istanza dell'oggetto di sicurezza: chiave pubblica o identità (3), chiave pubblica del server (4), chiave privata (5).</span><span class="sxs-lookup"><span data-stu-id="db2f7-414">The LWM2M Client delegates the security key management to the application during the Bootstrap sessions, the callbacks will be called when the Bootstrap Server writes or deletes the following resources on a Security Object Instance: Public Key or Identity (3), Server Public Key (4), Secret Key (5).</span></span>

<span data-ttu-id="db2f7-415">L'applicazione è responsabile dell'archiviazione dei dati delle chiavi e della configurazione delle sessioni DTLS usate dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-415">The application is responsible for storing the keys data and for configuring the DTLS sessions used by the LWM2M client.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-416">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-416">Parameters</span></span>

- <span data-ttu-id="db2f7-417">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-417">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="db2f7-418">**write_callback**: callback del metodo della chiave ' Write '.</span><span class="sxs-lookup"><span data-stu-id="db2f7-418">**write_callback**: The 'Write' key method callback.</span></span>
- <span data-ttu-id="db2f7-419">**delete_callback**: callback del metodo della chiave ' Delete '.</span><span class="sxs-lookup"><span data-stu-id="db2f7-419">**delete_callback**: The 'Delete' key method callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-420">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-420">Return Values</span></span>

- <span data-ttu-id="db2f7-421">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-421">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-422">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-422">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_bootstrap"></a><span data-ttu-id="db2f7-423">nx_lwm2m_client_session_bootstrap</span><span class="sxs-lookup"><span data-stu-id="db2f7-423">nx_lwm2m_client_session_bootstrap</span></span>

<span data-ttu-id="db2f7-424">Avviare una sessione con un server bootstrap</span><span class="sxs-lookup"><span data-stu-id="db2f7-424">Start a session with a Bootstrap Server</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-425">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-425">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_bootstrap(NX_LWM2M_CLIENT_SESSION
    *session_ptr, NX_LWM2M_ID security_id, ULONG ip_address, UINT port);
```

### <a name="description"></a><span data-ttu-id="db2f7-426">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-426">Description</span></span>

<span data-ttu-id="db2f7-427">Questo servizio avvia una sessione con un server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="db2f7-427">This service start a session with a Bootstrap Server.</span></span> <span data-ttu-id="db2f7-428">Il server deve disporre di un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-428">The server should have a corresponding security instance in the Security Object.</span></span>

<span data-ttu-id="db2f7-429">Se la risorsa ' Mantieni fuori ' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà il bootstrap avviato dal server, se non è stato avviato alcun bootstrap dal server dopo questo periodo di tempo in cui verrà eseguito un bootstrap avviato dal client.</span><span class="sxs-lookup"><span data-stu-id="db2f7-429">If the 'Hold Off' resource is different than zero in the Security Instance associated with this server the session will wait for a Server Initiated Bootstrap, if no bootstrap is initiated by the server after this period of time a Client Initiated Boostrap will be performed.</span></span>

<span data-ttu-id="db2f7-430">Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="db2f7-430">Any current active session is aborted by this call and replaced by the new Bootstrap Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-431">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-431">Parameters</span></span>

- <span data-ttu-id="db2f7-432">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-432">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="db2f7-433">**security_id**: l'ID dell'istanza di sicurezza del server bootstrap deve essere impostato su NX_LWM2M_RESERVED_ID (65535) se nel server bootstrap non è definita alcuna istanza di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-433">**security_id**: The Security Instance ID of the Bootstrap Server, must be set to NX_LWM2M_RESERVED_ID (65535) if the Bootstrap Server has no Security Instance defined.</span></span>
- <span data-ttu-id="db2f7-434">**ip_address**: indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-434">**ip_address**: The IP address of the server.</span></span>
- <span data-ttu-id="db2f7-435">**Port**: porta UDP del server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-435">**port**: The UDP port of the server.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-436">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-436">Return Values</span></span>

- <span data-ttu-id="db2f7-437">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-437">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-438">**NX_LWM2M_NOT_FOUND**: non è presente alcuna istanza di oggetto di sicurezza corrispondente all'ID dell'istanza di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-438">**NX_LWM2M_NOT_FOUND**: There is No Security Object instance corresponding to the Security Instance ID.</span></span>
- <span data-ttu-id="db2f7-439">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-439">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a><span data-ttu-id="db2f7-440">nx_lwm2m_client_session_bootstrap_dtls</span><span class="sxs-lookup"><span data-stu-id="db2f7-440">nx_lwm2m_client_session_bootstrap_dtls</span></span>

<span data-ttu-id="db2f7-441">Avviare una sessione protetta con un server bootstrap</span><span class="sxs-lookup"><span data-stu-id="db2f7-441">Start a secure session with a Bootstrap Server</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-442">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-442">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID security_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a><span data-ttu-id="db2f7-443">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-443">Description</span></span>

<span data-ttu-id="db2f7-444">Questo servizio avvia una sessione con un server bootstrap usando una connessione DTLS sicura.</span><span class="sxs-lookup"><span data-stu-id="db2f7-444">This service start a session with a Bootstrap Server using a secure DTLS connection.</span></span> <span data-ttu-id="db2f7-445">Il server deve disporre di un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-445">The server should have a corresponding security instance in the Security Object.</span></span>

<span data-ttu-id="db2f7-446">Prima di chiamare questa funzione, è necessario che la sessione DTLS sia stata configurata con i pacchetti di crittografia e il materiale della chiave appropriati.</span><span class="sxs-lookup"><span data-stu-id="db2f7-446">The DTLS session must have been configured with the proper cipher suites and key material before calling this function.</span></span> <span data-ttu-id="db2f7-447">È necessario definire NX_SECURE_ENABLE_DTLS.</span><span class="sxs-lookup"><span data-stu-id="db2f7-447">NX_SECURE_ENABLE_DTLS must be defined.</span></span>

<span data-ttu-id="db2f7-448">Se la risorsa ' Mantieni fuori ' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà il bootstrap avviato dal server, se non è stato avviato alcun bootstrap dal server dopo questo periodo di tempo in cui verrà eseguito un bootstrap avviato dal client.</span><span class="sxs-lookup"><span data-stu-id="db2f7-448">If the 'Hold Off' resource is different than zero in the Security Instance associated with this server the session will wait for a Server Initiated Bootstrap, if no bootstrap is initiated by the server after this period of time a Client Initiated Boostrap will be performed.</span></span>

<span data-ttu-id="db2f7-449">Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="db2f7-449">Any current active session is aborted by this call and replaced by the new Bootstrap Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-450">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-450">Parameters</span></span>

- <span data-ttu-id="db2f7-451">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-451">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="db2f7-452">**security_id**: l'ID dell'istanza di sicurezza del server bootstrap deve essere impostato su NX_LWM2M_RESERVED_ID (65535) se nel server bootstrap non è definita alcuna istanza di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-452">**security_id**: The Security Instance ID of the Bootstrap Server, must be set to NX_LWM2M_RESERVED_ID (65535) if the Bootstrap Server has no Security Instance defined.</span></span>
- <span data-ttu-id="db2f7-453">**ip_address**: indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-453">**ip_address**: The IP address of the server.</span></span>
- <span data-ttu-id="db2f7-454">**Port**: porta UDP del server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-454">**port**: The UDP port of the server.</span></span>
- <span data-ttu-id="db2f7-455">**dtls_session_ptr**: la sessione DTLS da usare per la sessione bootstrap.</span><span class="sxs-lookup"><span data-stu-id="db2f7-455">**dtls_session_ptr**: The DTLS session to use for the Bootstrap session.</span></span>
- <span data-ttu-id="db2f7-456">**dtls_local_port**: la porta UDP locale utilizzata per la sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="db2f7-456">**dtls_local_port**: The local UDP port used for the DTLS session.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-457">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-457">Return Values</span></span>

- <span data-ttu-id="db2f7-458">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-458">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-459">**NX_LWM2M_NOT_FOUND**: non è presente alcuna istanza di oggetto di sicurezza corrispondente all'ID dell'istanza di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-459">**NX_LWM2M_NOT_FOUND**: There is No Security Object instance corresponding to the Security Instance ID.</span></span>
- <span data-ttu-id="db2f7-460">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-460">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_create"></a><span data-ttu-id="db2f7-461">nx_lwm2m_client_session_create</span><span class="sxs-lookup"><span data-stu-id="db2f7-461">nx_lwm2m_client_session_create</span></span>

<span data-ttu-id="db2f7-462">Creare una sessione client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-462">Create LWM2M Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-463">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-463">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_create(NX_LWM2M_CLIENT_SESSION *session_ptr,
         NX_LWM2M_CLIENT *client_ptr,
         NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK state_callback);
```

### <a name="description"></a><span data-ttu-id="db2f7-464">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-464">Description</span></span>

<span data-ttu-id="db2f7-465">Questo servizio crea una nuova sessione client di LWM2M collegata a un client LWM2M esistente.</span><span class="sxs-lookup"><span data-stu-id="db2f7-465">This service creates a new LWM2M Client Session attached to an existing LWM2M Client.</span></span> <span data-ttu-id="db2f7-466">La sessione viene usata dal client LWM2M per comunicare con un server bootstrap o un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-466">The session is used by the LWM2M Client to communicate with a Bootstrap Server or a LWM2M Server.</span></span>

<span data-ttu-id="db2f7-467">L'applicazione deve fornire una funzione di callback che verrà chiamata quando viene aggiornato lo stato della sessione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-467">The application must provide a callback function that will be called when the state of the session is updated.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-468">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-468">Parameters</span></span>

- <span data-ttu-id="db2f7-469">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-469">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="db2f7-470">**client_ptr**: puntatore al client LWM2M creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-470">**client_ptr**: Pointer to the previously created LWM2M Client.</span></span>
- <span data-ttu-id="db2f7-471">**state_callback**: callback dell'applicazione che viene chiamato quando lo stato della sessione viene modificato.</span><span class="sxs-lookup"><span data-stu-id="db2f7-471">**state_callback**: Application callback that is called when the state of the session has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-472">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-472">Return Values</span></span>

- <span data-ttu-id="db2f7-473">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-473">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-474">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-474">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_delete"></a><span data-ttu-id="db2f7-475">nx_lwm2m_client_session_delete</span><span class="sxs-lookup"><span data-stu-id="db2f7-475">nx_lwm2m_client_session_delete</span></span>

<span data-ttu-id="db2f7-476">Elimina sessione client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-476">Delete LWM2M Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-477">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-477">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-478">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-478">Description</span></span>

<span data-ttu-id="db2f7-479">Questo servizio Elimina una sessione client di LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-479">This service deletes a LWM2M Client Session.</span></span>

<span data-ttu-id="db2f7-480">Quando un client LWM2M viene eliminato chiamando nx_lwm2m_client_delete vengono eliminate anche tutte le sessioni associate al client.</span><span class="sxs-lookup"><span data-stu-id="db2f7-480">When a LWM2M Client is deleted by calling nx_lwm2m_client_delete all sessions attached to the client are also deleted.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-481">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-481">Parameters</span></span>

- <span data-ttu-id="db2f7-482">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-482">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-483">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-483">Return Values</span></span>

- <span data-ttu-id="db2f7-484">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-484">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-485">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-485">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_deregister"></a><span data-ttu-id="db2f7-486">nx_lwm2m_client_session_deregister</span><span class="sxs-lookup"><span data-stu-id="db2f7-486">nx_lwm2m_client_session_deregister</span></span>

<span data-ttu-id="db2f7-487">Terminare una sessione con un server LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-487">Terminate a session with a LWM2M Server</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-488">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-488">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-489">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-489">Description</span></span>

<span data-ttu-id="db2f7-490">Questo servizio esegue un'operazione di annullamento della registrazione in un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-490">This service performs a 'De-Register' operation to a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-491">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-491">Parameters</span></span>

- <span data-ttu-id="db2f7-492">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-492">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-493">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-493">Return Values</span></span>

- <span data-ttu-id="db2f7-494">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-494">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-495">**NX_LWM2M_NOT_REGISTERED**: il client non è registrato nel server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-495">**NX_LWM2M_NOT_REGISTERED**: The client is not registered to the server.</span></span>
- <span data-ttu-id="db2f7-496">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-496">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_error_get"></a><span data-ttu-id="db2f7-497">nx_lwm2m_client_session_error_get</span><span class="sxs-lookup"><span data-stu-id="db2f7-497">nx_lwm2m_client_session_error_get</span></span>

<span data-ttu-id="db2f7-498">Ottenere l'ultimo errore di una sessione</span><span class="sxs-lookup"><span data-stu-id="db2f7-498">Get last error of a session</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-499">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-499">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-500">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-500">Description</span></span>

<span data-ttu-id="db2f7-501">Questo servizio restituisce il codice di errore della sessione quando la sessione è in stato di errore.</span><span class="sxs-lookup"><span data-stu-id="db2f7-501">This service returns the error code of the session when the session is in an error state.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-502">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-502">Parameters</span></span>

- <span data-ttu-id="db2f7-503">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-503">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-504">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-504">Return Values</span></span>

- <span data-ttu-id="db2f7-505">**NX_SUCCESS**: la sessione non è in stato di errore.</span><span class="sxs-lookup"><span data-stu-id="db2f7-505">**NX_SUCCESS**: The session is not in error state.</span></span>
- <span data-ttu-id="db2f7-506">**NX_LWM2M_ADDRESS_ERROR**: Indirizzo server non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-506">**NX_LWM2M_ADDRESS_ERROR**: Invalid server address.</span></span>
- <span data-ttu-id="db2f7-507">**NX_LWM2M_BUFFER_TOO_SMALL**: il payload della richiesta non rientra nel buffer di rete.</span><span class="sxs-lookup"><span data-stu-id="db2f7-507">**NX_LWM2M_BUFFER_TOO_SMALL**: Payload of request doesn't fit in network buffer.</span></span>
- <span data-ttu-id="db2f7-508">**NX_LWM2M_DTLS_ERROR**: non è stato possibile stabilire una connessione protetta con il server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-508">**NX_LWM2M_DTLS_ERROR**: Failed to establish secured connection with server.</span></span>
- <span data-ttu-id="db2f7-509">**NX_LWM2M_ERROR**: errore non specificato.</span><span class="sxs-lookup"><span data-stu-id="db2f7-509">**NX_LWM2M_ERROR**: Unspecified error.</span></span>
- <span data-ttu-id="db2f7-510">**NX_LWM2M_FORBIDDEN**: la registrazione è stata rifiutata dal server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-510">**NX_LWM2M_FORBIDDEN**: Registration refused by server.</span></span>
- <span data-ttu-id="db2f7-511">**NX_LWM2M_NOT_FOUND**: il client non è stato trovato dal server durante l'aggiornamento/annullamento della registrazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-511">**NX_LWM2M_NOT_FOUND**: Client not found by server when updating/deregistering.</span></span>
- <span data-ttu-id="db2f7-512">**NX_LWM2M_SERVER_INSTANCE_DELETED**: l'istanza dell'oggetto server corrispondente alla sessione è stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="db2f7-512">**NX_LWM2M_SERVER_INSTANCE_DELETED**: The Server Object Instance corresponding to the session has been deleted.</span></span>
- <span data-ttu-id="db2f7-513">**NX_LWM2M_TIMED_OUT**: nessuna risposta dal server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-513">**NX_LWM2M_TIMED_OUT**: No answer from server.</span></span>
- <span data-ttu-id="db2f7-514">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-514">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_register"></a><span data-ttu-id="db2f7-515">nx_lwm2m_client_session_register</span><span class="sxs-lookup"><span data-stu-id="db2f7-515">nx_lwm2m_client_session_register</span></span>

<span data-ttu-id="db2f7-516">Avviare una sessione con un server LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-516">Start a session with a LWM2M Server</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-517">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-517">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register(NX_LWM2M_CLIENT_SESSION *session_ptr,
                    NX_LWM2M_ID server_id, ULONG ip_address, UINT port);
```

### <a name="description"></a><span data-ttu-id="db2f7-518">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-518">Description</span></span>

<span data-ttu-id="db2f7-519">Questo servizio esegue un'operazione di registrazione in un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-519">This service performs a 'Register' operation to a LWM2M Server.</span></span> <span data-ttu-id="db2f7-520">Il server deve disporre di un'istanza del server corrispondente nell'oggetto server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-520">The server must have a corresponding server instance in the Server Object.</span></span>

<span data-ttu-id="db2f7-521">Se la registrazione ha esito positivo, il client LWM2M elaborerà ulteriori operazioni dal server e invierà periodicamente messaggi di aggiornamento finché il client non viene deregistrato.</span><span class="sxs-lookup"><span data-stu-id="db2f7-521">If the registration is successful the LWM2M Client will process further operations from the server and will periodically send 'Update' messages until the client is de-registered.</span></span>

<span data-ttu-id="db2f7-522">Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-522">Any current active session is aborted by this call and replaced by the new LWM2M Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-523">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-523">Parameters</span></span>

- <span data-ttu-id="db2f7-524">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-524">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="db2f7-525">**server_id**: ID server breve del server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-525">**server_id**: The Short Server ID of the LWM2M Server.</span></span>
- <span data-ttu-id="db2f7-526">**ip_address**: indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-526">**ip_address**: The IP address of the server.</span></span>
- <span data-ttu-id="db2f7-527">**Port**: porta UDP del server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-527">**port**: The UDP port of the server.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-528">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-528">Return Values</span></span>

- <span data-ttu-id="db2f7-529">**NX_SUCCESS**: operazione riuscita..</span><span class="sxs-lookup"><span data-stu-id="db2f7-529">**NX_SUCCESS**: Successful operation..</span></span>
- <span data-ttu-id="db2f7-530">**NX_LWM2M_NOT_FOUND**: non esiste alcuna istanza dell'oggetto server corrispondente all'ID server breve.</span><span class="sxs-lookup"><span data-stu-id="db2f7-530">**NX_LWM2M_NOT_FOUND**: There is No Server Object instance corresponding to the Short Server ID.</span></span>
- <span data-ttu-id="db2f7-531">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-531">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_register_dtls"></a><span data-ttu-id="db2f7-532">nx_lwm2m_client_session_register_dtls</span><span class="sxs-lookup"><span data-stu-id="db2f7-532">nx_lwm2m_client_session_register_dtls</span></span>

<span data-ttu-id="db2f7-533">Avviare una sessione protetta con un server LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-533">Start a secure session with a LWM2M Server</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-534">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-534">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID server_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a><span data-ttu-id="db2f7-535">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-535">Description</span></span>

<span data-ttu-id="db2f7-536">Questo servizio esegue un'operazione di registrazione in un server LWM2M usando una connessione DTLS sicura.</span><span class="sxs-lookup"><span data-stu-id="db2f7-536">This service performs a 'Register' operation to a LWM2M Server using a secure DTLS connection.</span></span> <span data-ttu-id="db2f7-537">Il server deve disporre di un'istanza del server corrispondente nell'oggetto server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-537">The server must have a corresponding server instance in the Server Object.</span></span>

<span data-ttu-id="db2f7-538">Prima di chiamare questa funzione, è necessario che la sessione DTLS sia stata configurata con i pacchetti di crittografia e il materiale della chiave appropriati.</span><span class="sxs-lookup"><span data-stu-id="db2f7-538">The DTLS session must have been configured with the proper cipher suites and key material before calling this function.</span></span> <span data-ttu-id="db2f7-539">È necessario definire NX_SECURE_ENABLE_DTLS.</span><span class="sxs-lookup"><span data-stu-id="db2f7-539">NX_SECURE_ENABLE_DTLS must be defined.</span></span>

<span data-ttu-id="db2f7-540">Ogni sessione DTLS usa il proprio socket UDP per la comunicazione, quindi la porta locale dtls_local_port deve essere diversa per ogni sessione se l'applicazione crea diverse sessioni sicure.</span><span class="sxs-lookup"><span data-stu-id="db2f7-540">Each DTLS session uses its own UDP socket for communication, so the local port dtls_local_port must be different for each session if the application creates several secure sessions.</span></span>

<span data-ttu-id="db2f7-541">Se la registrazione ha esito positivo, il client LWM2M elaborerà ulteriori operazioni dal server e invierà periodicamente messaggi di aggiornamento finché il client non viene deregistrato.</span><span class="sxs-lookup"><span data-stu-id="db2f7-541">If the registration is successful the LWM2M Client will process further operations from the server and will periodically send 'Update' messages until the client is de-registered.</span></span>

<span data-ttu-id="db2f7-542">Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-542">Any current active session is aborted by this call and replaced by the new LWM2M Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-543">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-543">Parameters</span></span>

- <span data-ttu-id="db2f7-544">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-544">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="db2f7-545">**server_id**: ID server breve del server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-545">**server_id**: The Short Server ID of the LWM2M Server.</span></span>
- <span data-ttu-id="db2f7-546">**ip_address**: indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-546">**ip_address**: The IP address of the server.</span></span>
- <span data-ttu-id="db2f7-547">**Port**: porta UDP del server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-547">**port**: The UDP port of the server.</span></span>
- <span data-ttu-id="db2f7-548">**dtls_session_ptr**: la sessione DTLS da usare per la sessione LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-548">**dtls_session_ptr**: The DTLS session to use for the LWM2M session.</span></span>
- <span data-ttu-id="db2f7-549">**dtls_local_port**: la porta UDP locale utilizzata per la sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="db2f7-549">**dtls_local_port**: The local UDP port used for the DTLS session.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-550">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-550">Return Values</span></span>

- <span data-ttu-id="db2f7-551">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-551">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-552">**NX_LWM2M_NOT_FOUND**: non esiste alcuna istanza dell'oggetto server corrispondente all'ID server breve.</span><span class="sxs-lookup"><span data-stu-id="db2f7-552">**NX_LWM2M_NOT_FOUND**: There is No Server Object instance corresponding to the Short Server ID.</span></span>
- <span data-ttu-id="db2f7-553">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-553">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_update"></a><span data-ttu-id="db2f7-554">nx_lwm2m_client_session_update</span><span class="sxs-lookup"><span data-stu-id="db2f7-554">nx_lwm2m_client_session_update</span></span>

<span data-ttu-id="db2f7-555">Aggiornare una sessione con un server LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-555">Update a session with a LWM2M Server</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-556">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-556">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-557">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-557">Description</span></span>

<span data-ttu-id="db2f7-558">Questo servizio esegue un'operazione di aggiornamento in un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-558">This service performs an 'Update' operation to a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-559">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-559">Parameters</span></span>

- <span data-ttu-id="db2f7-560">**session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-560">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-561">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-561">Return Values</span></span>

- <span data-ttu-id="db2f7-562">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-562">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-563">**NX_LWM2M_NOT_REGISTERED**: il client non è registrato nel server.</span><span class="sxs-lookup"><span data-stu-id="db2f7-563">**NX_LWM2M_NOT_REGISTERED**: The client is not registered to the server.</span></span>
- <span data-ttu-id="db2f7-564">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-564">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_unlock"></a><span data-ttu-id="db2f7-565">nx_lwm2m_client_unlock</span><span class="sxs-lookup"><span data-stu-id="db2f7-565">nx_lwm2m_client_unlock</span></span>

<span data-ttu-id="db2f7-566">Sbloccare il client LWM2M</span><span class="sxs-lookup"><span data-stu-id="db2f7-566">Unlock LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-567">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-567">Prototype</span></span>

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-568">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-568">Description</span></span>

<span data-ttu-id="db2f7-569">Questo servizio Sblocca il previoulsy client di LWM2M bloccato da una chiamata a nx_lwm2m_client_unlock ().</span><span class="sxs-lookup"><span data-stu-id="db2f7-569">This service unlocks the LWM2M Client previoulsy locked by a call to nx_lwm2m_client_unlock().</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-570">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-570">Parameters</span></span>

- <span data-ttu-id="db2f7-571">**client_ptr**: puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-571">**client_ptr**: Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-572">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-572">Return Values</span></span>

- <span data-ttu-id="db2f7-573">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-573">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-574">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-574">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_firmware_create"></a><span data-ttu-id="db2f7-575">nx_lwm2m_firmware_create</span><span class="sxs-lookup"><span data-stu-id="db2f7-575">nx_lwm2m_firmware_create</span></span>

<span data-ttu-id="db2f7-576">Crea oggetto aggiornamento firmware</span><span class="sxs-lookup"><span data-stu-id="db2f7-576">Create Firmware Update Object</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-577">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-577">Prototype</span></span>

```c
UINT nx_lwm2m_firmware_create(NX_LWM2M_FIRMWARE *firmware_ptr,
    NX_LWM2M_CLIENT *client_ptr, UINT protocols,
    NX_LWM2M_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_FIRMWARE_UPDATE_CALLBACK update_callback);
```

### <a name="description"></a><span data-ttu-id="db2f7-578">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-578">Description</span></span>

<span data-ttu-id="db2f7-579">Questo servizio Inizializza un oggetto di aggiornamento del firmware e aggiunge l'oggetto a un client LWM2M creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-579">This service initializes a Firmware Update Object and adds the Object to a previously created LWM2M Client.</span></span> <span data-ttu-id="db2f7-580">L'oggetto di aggiornamento del firmware implementa le risorse per la comunicazione con un server LWM2M, ma l'applicazione deve fornire callback per implementare le operazioni effettive nel firmware (dowloading, archiviazione e aggiornamento del firmware).</span><span class="sxs-lookup"><span data-stu-id="db2f7-580">The Firmware Update Object implements the resources for communicating with a LWM2M Server but the application must provide callbacks for implementing the actual operations on the firmware (dowloading, storing, and updating the firmware).</span></span>

<span data-ttu-id="db2f7-581">Il parametro Protocols indica i protocolli supportati dall'applicazione per il recupero del firmware con la risorsa ' URI pacchetto '. vengono definiti i flag seguenti:</span><span class="sxs-lookup"><span data-stu-id="db2f7-581">The protocols parameter indicates which protocols are supported by the application for retrieving the firmware with the 'Package URI' resource, the following flags are defined:</span></span>

<span data-ttu-id="db2f7-582">NX_LWM2M_FIRMWARE_PROTOCOL_COAP, NX_LWM2M_FIRMWARE_PROTOCOL_COAPS, NX_LWM2M_FIRMWARE_PROTOCOL_HTTP NX_LWM2M_FIRMWARE_PROTOCOL_HTPPS.</span><span class="sxs-lookup"><span data-stu-id="db2f7-582">NX_LWM2M_FIRMWARE_PROTOCOL_COAP, NX_LWM2M_FIRMWARE_PROTOCOL_COAPS, NX_LWM2M_FIRMWARE_PROTOCOL_HTTP, NX_LWM2M_FIRMWARE_PROTOCOL_HTPPS.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-583">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-583">Parameters</span></span>

- <span data-ttu-id="db2f7-584">**firmware_ptr**: puntatore al blocco di controllo dell'oggetto firmware.</span><span class="sxs-lookup"><span data-stu-id="db2f7-584">**firmware_ptr**: Pointer to the Firmware Object control block.</span></span>
- <span data-ttu-id="db2f7-585">**client_ptr**: puntatore a PREVISOUSLY creato LWM2M client.</span><span class="sxs-lookup"><span data-stu-id="db2f7-585">**client_ptr**: Pointer to previsously created LWM2M Client.</span></span>
- <span data-ttu-id="db2f7-586">**protocolli**: flag che indicano i protocolli supportati dalla risorsa URI del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-586">**protocols**: Flags indicating which protocols are supported by the Package URI resource.</span></span>
- <span data-ttu-id="db2f7-587">**package_callback**: deve essere null [TBD].</span><span class="sxs-lookup"><span data-stu-id="db2f7-587">**package_callback**: Must be NULL [TBD].</span></span>
- <span data-ttu-id="db2f7-588">**package_uri_callback**: callback utilizzato per implementare la risorsa URI del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-588">**package_uri_callback**: Callback used to implement the Package URI resource.</span></span>
- <span data-ttu-id="db2f7-589">**update_callback**: callback utilizzato per implementare la risorsa di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="db2f7-589">**update_callback**: Callback used to implement the Update resource.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-590">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-590">Return Values</span></span>

- <span data-ttu-id="db2f7-591">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-591">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-592">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-592">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_firmware_package_info_set"></a><span data-ttu-id="db2f7-593">nx_lwm2m_firmware_package_info_set</span><span class="sxs-lookup"><span data-stu-id="db2f7-593">nx_lwm2m_firmware_package_info_set</span></span>

<span data-ttu-id="db2f7-594">Impostare le informazioni sul pacchetto di aggiornamento del firmware</span><span class="sxs-lookup"><span data-stu-id="db2f7-594">Set Firmware Update Package Information</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-595">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-595">Prototype</span></span>

```c
UINT nx_lwm2m_firmware_package_info_set(NX_LWM2M_FIRMWARE *firmware_ptr,
                                const CHAR *name, const CHAR *version);
```

### <a name="description"></a><span data-ttu-id="db2f7-596">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-596">Description</span></span>

<span data-ttu-id="db2f7-597">Questo servizio modifica i valori delle risorse ' PkgName ' (6) è PkgVersion ' (7) dell'oggetto di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="db2f7-597">This service changes the values of the 'PkgName' (6) and 'PkgVersion' (7) resources of the Firmware Update Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-598">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-598">Parameters</span></span>

- <span data-ttu-id="db2f7-599">**firmware_ptr**: puntatore all'oggetto di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="db2f7-599">**firmware_ptr**: Pointer to the Firmware Update Object.</span></span>
- <span data-ttu-id="db2f7-600">**nome**: nuovo valore del nome del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-600">**name**: The new value of the Package Name.</span></span>
- <span data-ttu-id="db2f7-601">**Version**: nuovo valore della versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-601">**version**: The new value of the Package Version.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-602">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-602">Return Values</span></span>

- <span data-ttu-id="db2f7-603">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-603">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-604">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-604">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_firmware_result_set"></a><span data-ttu-id="db2f7-605">nx_lwm2m_firmware_result_set</span><span class="sxs-lookup"><span data-stu-id="db2f7-605">nx_lwm2m_firmware_result_set</span></span>

<span data-ttu-id="db2f7-606">Imposta il risultato dell'aggiornamento del firmware</span><span class="sxs-lookup"><span data-stu-id="db2f7-606">Set Firmware Update Result</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-607">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-607">Prototype</span></span>

```c
UINT nx_lwm2m_firmware_result_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR result);
```

### <a name="description"></a><span data-ttu-id="db2f7-608">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-608">Description</span></span>

<span data-ttu-id="db2f7-609">Questo servizio modifica il valore della risorsa ' aggiornamento risultato ' (5) dell'oggetto aggiornamento firmware.</span><span class="sxs-lookup"><span data-stu-id="db2f7-609">This service changes the value of the 'Update Result' (5) resource of the Firmware Update Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-610">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-610">Parameters</span></span>

- <span data-ttu-id="db2f7-611">**firmware_ptr**: puntatore all'oggetto di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="db2f7-611">**firmware_ptr**: Pointer to the Firmware Update Object.</span></span>
- <span data-ttu-id="db2f7-612">**risultato**: nuovo valore della risorsa del risultato dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="db2f7-612">**result**: The new value of the Update Result resource.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-613">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-613">Return Values</span></span>

- <span data-ttu-id="db2f7-614">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-614">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-615">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-615">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_firmware_state_set"></a><span data-ttu-id="db2f7-616">nx_lwm2m_firmware_state_set</span><span class="sxs-lookup"><span data-stu-id="db2f7-616">nx_lwm2m_firmware_state_set</span></span>

<span data-ttu-id="db2f7-617">Imposta lo stato di aggiornamento del firmware</span><span class="sxs-lookup"><span data-stu-id="db2f7-617">Set Firmware Update State</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-618">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-618">Prototype</span></span>

```c
UINT nx_lwm2m_firmware_state_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR state);
```

### <a name="description"></a><span data-ttu-id="db2f7-619">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-619">Description</span></span>

<span data-ttu-id="db2f7-620">Questo servizio modifica il valore della risorsa ' state ' (3) dell'oggetto di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="db2f7-620">This service changes the value of the 'State' (3) resource of the Firmware Update Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-621">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-621">Parameters</span></span>

- <span data-ttu-id="db2f7-622">**firmware_ptr**: puntatore all'oggetto di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="db2f7-622">**firmware_ptr**: Pointer to the Firmware Update Object.</span></span>
- <span data-ttu-id="db2f7-623">**stato**: nuovo valore della risorsa di stato.</span><span class="sxs-lookup"><span data-stu-id="db2f7-623">**state**: The new value of the State resource.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-624">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-624">Return Values</span></span>

- <span data-ttu-id="db2f7-625">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-625">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-626">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-626">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_object_resource_changed"></a><span data-ttu-id="db2f7-627">nx_lwm2m_object_resource_changed</span><span class="sxs-lookup"><span data-stu-id="db2f7-627">nx_lwm2m_object_resource_changed</span></span>

<span data-ttu-id="db2f7-628">Modifica del segnale di un valore di risorsa di un'istanza dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-628">Signal change of a resource value of an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-629">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-629">Prototype</span></span>

```c
UINT nx_lwm2m_object_resource_changed(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a><span data-ttu-id="db2f7-630">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-630">Description</span></span>

<span data-ttu-id="db2f7-631">Questo servizio viene usato da un'implementazione dell'oggetto per segnalare al client LWM2M che uno dei relativi valori di risorsa è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="db2f7-631">This service is used by an Object implementation to signals the LWM2M Client that one of its resource value has changed.</span></span> <span data-ttu-id="db2f7-632">Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="db2f7-632">The LWM2M Client will send a notification if the resource is observed by a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-633">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-633">Parameters</span></span>

- <span data-ttu-id="db2f7-634">**object_ptr**: puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-634">**object_ptr**: Pointer to the Object implementation.</span></span>
- <span data-ttu-id="db2f7-635">**instance_ptr**: puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-635">**instance_ptr**: Pointer to the Object Instance.</span></span>
- <span data-ttu-id="db2f7-636">**Resource**: puntatore alla struttura che descrive la risorsa che è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="db2f7-636">**resource**: Pointer to the structure describing the resource that has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-637">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-637">Return Values</span></span>

- <span data-ttu-id="db2f7-638">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-638">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-639">NX_PTR_ERROR: puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="db2f7-639">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_resource_get_boolean"></a><span data-ttu-id="db2f7-640">nx_lwm2m_resource_get_boolean</span><span class="sxs-lookup"><span data-stu-id="db2f7-640">nx_lwm2m_resource_get_boolean</span></span>

<span data-ttu-id="db2f7-641">Ottenere il valore di una risorsa booleana</span><span class="sxs-lookup"><span data-stu-id="db2f7-641">Get the value of a Boolean Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-642">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-642">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_boolean(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-643">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-643">Description</span></span>

<span data-ttu-id="db2f7-644">Il servizio recupera il valore di una risorsa booleana.</span><span class="sxs-lookup"><span data-stu-id="db2f7-644">The service retrieves the value of a Boolean Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-645">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-645">Parameters</span></span>

- <span data-ttu-id="db2f7-646">**valore**: puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-646">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="db2f7-647">**bool_ptr**: puntatore al valore booleano di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-647">**bool_ptr**: Pointer to the destination Boolean value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-648">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-648">Return Values</span></span>

- <span data-ttu-id="db2f7-649">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-649">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-650">**NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="db2f7-650">**NX_LWM2M_BAD_ENCODING**: The resource value is not a Boolean value.</span></span>

## <a name="nx_lwm2m_resource_get_float32"></a><span data-ttu-id="db2f7-651">nx_lwm2m_resource_get_float32</span><span class="sxs-lookup"><span data-stu-id="db2f7-651">nx_lwm2m_resource_get_float32</span></span>

<span data-ttu-id="db2f7-652">Ottenere il valore di una risorsa a virgola mobile a 32 bit</span><span class="sxs-lookup"><span data-stu-id="db2f7-652">Get the value of a 32-bit Floating Point Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-653">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-653">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_float32(const NX_LWM2M_RESOURCE *value,
                                NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-654">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-654">Description</span></span>

<span data-ttu-id="db2f7-655">Il servizio recupera il valore di una risorsa a virgola mobile a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="db2f7-655">The service retrieves the value of a 32-bit Floating Point Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-656">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-656">Parameters</span></span>

- <span data-ttu-id="db2f7-657">**valore**: puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-657">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="db2f7-658">**float32_ptr**: puntatore al valore a virgola mobile a 32 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-658">**float32_ptr**: Pointer to the destination 32-Bit Floating Point value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-659">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-659">Return Values</span></span>

- <span data-ttu-id="db2f7-660">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-660">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-661">**NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="db2f7-661">**NX_LWM2M_BAD_ENCODING**: The resource value is not a Floating Point value.</span></span>

## <a name="nx_lwm2m_resource_get_float64"></a><span data-ttu-id="db2f7-662">nx_lwm2m_resource_get_float64</span><span class="sxs-lookup"><span data-stu-id="db2f7-662">nx_lwm2m_resource_get_float64</span></span>

<span data-ttu-id="db2f7-663">Ottenere il valore di una risorsa a virgola mobile a 64 bit</span><span class="sxs-lookup"><span data-stu-id="db2f7-663">Get the value of a 64-bit Floating Point Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-664">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-664">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_float64(const NX_LWM2M_RESOURCE *value,
                                NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-665">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-665">Description</span></span>

<span data-ttu-id="db2f7-666">Il servizio recupera il valore di una risorsa a virgola mobile a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="db2f7-666">The service retrieves the value of a 64-bit Floating Point Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-667">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-667">Parameters</span></span>

- <span data-ttu-id="db2f7-668">**valore**: puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-668">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="db2f7-669">**float64_ptr**: puntatore al valore a virgola mobile a 64 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-669">**float64_ptr**: Pointer to the destination 64-Bit Floating Point value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-670">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-670">Return Values</span></span>

- <span data-ttu-id="db2f7-671">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-671">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-672">**NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="db2f7-672">**NX_LWM2M_BAD_ENCODING**: The resource value is not a Floating Point value.</span></span>

## <a name="nx_lwm2m_resource_get_integer32"></a><span data-ttu-id="db2f7-673">nx_lwm2m_resource_get_integer32</span><span class="sxs-lookup"><span data-stu-id="db2f7-673">nx_lwm2m_resource_get_integer32</span></span>

<span data-ttu-id="db2f7-674">Ottenere il valore di una risorsa Integer a 32 bit</span><span class="sxs-lookup"><span data-stu-id="db2f7-674">Get the value of a 32-Bit Integer Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-675">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-675">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_integer32(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-676">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-676">Description</span></span>

<span data-ttu-id="db2f7-677">Il servizio recupera il valore di una risorsa Integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="db2f7-677">The service retrieves the value of a 32-Bit Integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-678">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-678">Parameters</span></span>

- <span data-ttu-id="db2f7-679">**valore**: puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-679">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="db2f7-680">**int32_ptr**: puntatore al valore Integer a 32 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-680">**int32_ptr**: Pointer to the destination 32-Bit Integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-681">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-681">Return Values</span></span>

- <span data-ttu-id="db2f7-682">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-682">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-683">**NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore intero oppure il valore integer non rientra in un numero a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="db2f7-683">**NX_LWM2M_BAD_ENCODING**: The resource value is not an Integer value, or the Integer value doesn't fit in a 32-Bit number.</span></span>

## <a name="nx_lwm2m_resource_get_integer64"></a><span data-ttu-id="db2f7-684">nx_lwm2m_resource_get_integer64</span><span class="sxs-lookup"><span data-stu-id="db2f7-684">nx_lwm2m_resource_get_integer64</span></span>

<span data-ttu-id="db2f7-685">Ottenere il valore di una risorsa Integer a 64 bit</span><span class="sxs-lookup"><span data-stu-id="db2f7-685">Get the value of a 64-Bit Integer Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-686">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-686">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_integer64(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-687">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-687">Description</span></span>

<span data-ttu-id="db2f7-688">Il servizio recupera il valore di una risorsa Integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="db2f7-688">The service retrieves the value of a 64-Bit Integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-689">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-689">Parameters</span></span>

- <span data-ttu-id="db2f7-690">**valore**: puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-690">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="db2f7-691">**int64_ptr**: puntatore al valore Integer a 64 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-691">**int64_ptr**: Pointer to the destination 64-Bit Integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-692">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-692">Return Values</span></span>

- <span data-ttu-id="db2f7-693">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-693">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-694">**NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore integer.</span><span class="sxs-lookup"><span data-stu-id="db2f7-694">**NX_LWM2M_BAD_ENCODING**: The resource value is not an Integer value.</span></span>

## <a name="nx_lwm2m_resource_get_objlnk"></a><span data-ttu-id="db2f7-695">nx_lwm2m_resource_get_objlnk</span><span class="sxs-lookup"><span data-stu-id="db2f7-695">nx_lwm2m_resource_get_objlnk</span></span>

<span data-ttu-id="db2f7-696">Ottenere il valore di una risorsa di collegamento a un oggetto</span><span class="sxs-lookup"><span data-stu-id="db2f7-696">Get the value of an Object Link Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-697">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-697">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_objlnk(const NX_LWM2M_RESOURCE *value,
                                    NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-698">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-698">Description</span></span>

<span data-ttu-id="db2f7-699">Il servizio recupera il valore di una risorsa di collegamento a un oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-699">The service retrieves the value of an Object Link Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-700">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-700">Parameters</span></span>

- <span data-ttu-id="db2f7-701">**valore**: puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-701">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="db2f7-702">**objlnk_ptr**: puntatore al valore del collegamento all'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-702">**objlnk_ptr**: Pointer to the destination Object Link value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-703">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-703">Return Values</span></span>

- <span data-ttu-id="db2f7-704">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-704">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-705">**NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore di collegamento a un oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-705">**NX_LWM2M_BAD_ENCODING**: The resource value is not an Object Link value.</span></span>

## <a name="nx_lwm2m_resource_get_opaque"></a><span data-ttu-id="db2f7-706">nx_lwm2m_resource_get_opaque</span><span class="sxs-lookup"><span data-stu-id="db2f7-706">nx_lwm2m_resource_get_opaque</span></span>

<span data-ttu-id="db2f7-707">Ottenere il valore di una risorsa opaca</span><span class="sxs-lookup"><span data-stu-id="db2f7-707">Get the value of an Opaque Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-708">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-708">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_opaque(const NX_LWM2M_RESOURCE *value,
            const VOID **opaque_ptr_ptr, UINT *opaque_length_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-709">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-709">Description</span></span>

<span data-ttu-id="db2f7-710">Il servizio recupera il valore di una risorsa opaca.</span><span class="sxs-lookup"><span data-stu-id="db2f7-710">The service retrieves the value of an Opaque Resource.</span></span>

<span data-ttu-id="db2f7-711">Un valore di risorsa opaco è costituito da un puntatore a un buffer e una lunghezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-711">An opaque resource value consists of a pointer to a buffer and a length.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-712">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-712">Parameters</span></span>

- <span data-ttu-id="db2f7-713">**valore**: puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-713">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="db2f7-714">**opaque_ptr_ptr**: puntatore al puntatore al buffer opaco di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-714">**opaque_ptr_ptr**: Pointer to the destination opaque buffer pointer.</span></span>
- <span data-ttu-id="db2f7-715">**opaque_length_ptr**: puntatore alla lunghezza del buffer opaco di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-715">**opaque_length_ptr**: Pointer to the destination opaque buffer length.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-716">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-716">Return Values</span></span>

- <span data-ttu-id="db2f7-717">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-717">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-718">**NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore opaco.</span><span class="sxs-lookup"><span data-stu-id="db2f7-718">**NX_LWM2M_BAD_ENCODING**: The resource value is not an Opaque value.</span></span>

## <a name="nx_lwm2m_resource_get_string"></a><span data-ttu-id="db2f7-719">nx_lwm2m_resource_get_string</span><span class="sxs-lookup"><span data-stu-id="db2f7-719">nx_lwm2m_resource_get_string</span></span>

<span data-ttu-id="db2f7-720">Ottenere il valore di una risorsa di stringa</span><span class="sxs-lookup"><span data-stu-id="db2f7-720">Get the value of a String Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-721">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-721">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_string(const NX_LWM2M_RESOURCE *value,
            const CHAR **string_ptr_ptr, UINT *string_length_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-722">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-722">Description</span></span>

<span data-ttu-id="db2f7-723">Il servizio recupera il valore di una risorsa di stringa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-723">The service retrieves the value of a String Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-724">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-724">Parameters</span></span>

- <span data-ttu-id="db2f7-725">**valore**: puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-725">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="db2f7-726">**string_ptr_ptr**: puntatore al puntatore della stringa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-726">**string_ptr_ptr**: Pointer to the destination string pointer.</span></span>
- <span data-ttu-id="db2f7-727">**string_length_ptr**: puntatore alla lunghezza della stringa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-727">**string_length_ptr**: Pointer to the destination string length.</span></span> <span data-ttu-id="db2f7-728">Può essere NULL se la stringa è con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="db2f7-728">Can be NULL if the string is null-terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-729">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-729">Return Values</span></span>

- <span data-ttu-id="db2f7-730">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-730">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-731">**NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-731">**NX_LWM2M_BAD_ENCODING**: The resource value is not a String value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_boolean"></a><span data-ttu-id="db2f7-732">nx_lwm2m_resource_multiple_get_boolean</span><span class="sxs-lookup"><span data-stu-id="db2f7-732">nx_lwm2m_resource_multiple_get_boolean</span></span>

<span data-ttu-id="db2f7-733">Ottenere il valore di una risorsa booleana più istanze di risorse</span><span class="sxs-lookup"><span data-stu-id="db2f7-733">Get the value of a Boolean Resource Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-734">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-734">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_boolean(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-735">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-735">Description</span></span>

<span data-ttu-id="db2f7-736">Il servizio recupera il valore di un'istanza di risorsa booleana da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="db2f7-736">The service retrieves the value of a Boolean Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-737">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-737">Parameters</span></span>

- <span data-ttu-id="db2f7-738">**value**: puntatore alla descrizione del valore di più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-738">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="db2f7-739">**index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-739">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="db2f7-740">**instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-740">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="db2f7-741">**bool_ptr**: puntatore al valore booleano di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-741">**bool_ptr**: Pointer to the destination Boolean value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-742">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-742">Return Values</span></span>

- <span data-ttu-id="db2f7-743">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-743">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-744">**NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-744">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="db2f7-745">**NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="db2f7-745">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not a Boolean value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_float32"></a><span data-ttu-id="db2f7-746">nx_lwm2m_resource_multiple_get_float32</span><span class="sxs-lookup"><span data-stu-id="db2f7-746">nx_lwm2m_resource_multiple_get_float32</span></span>

<span data-ttu-id="db2f7-747">Ottenere il valore di un'istanza a virgola mobile a virgola mobile a 32 bit</span><span class="sxs-lookup"><span data-stu-id="db2f7-747">Get the value of a 32-bit Floating Point Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-748">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-748">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_float32(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-749">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-749">Description</span></span>

<span data-ttu-id="db2f7-750">Il servizio recupera il valore di un'istanza di risorsa a virgola mobile a 32 bit da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="db2f7-750">The service retrieves the value of a 32-bit Floating Point Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-751">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-751">Parameters</span></span>

- <span data-ttu-id="db2f7-752">**value**: puntatore alla descrizione del valore di più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-752">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="db2f7-753">**index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-753">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="db2f7-754">**instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-754">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="db2f7-755">**float32_ptr**: puntatore al valore a virgola mobile a 32 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-755">**float32_ptr**: Pointer to the destination 32-Bit Floating Point value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-756">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-756">Return Values</span></span>

- <span data-ttu-id="db2f7-757">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-757">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-758">**NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-758">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="db2f7-759">**NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="db2f7-759">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not a Floating Point value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_float64"></a><span data-ttu-id="db2f7-760">nx_lwm2m_resource_multiple_get_float64</span><span class="sxs-lookup"><span data-stu-id="db2f7-760">nx_lwm2m_resource_multiple_get_float64</span></span>

<span data-ttu-id="db2f7-761">Ottenere il valore di un'istanza a virgola mobile a virgola mobile a 64 bit</span><span class="sxs-lookup"><span data-stu-id="db2f7-761">Get the value of a 64-bit Floating Point Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-762">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-762">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_float64(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-763">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-763">Description</span></span>

<span data-ttu-id="db2f7-764">Il servizio recupera il valore di un'istanza di risorsa a virgola mobile a 64 bit da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="db2f7-764">The service retrieves the value of a 64-bit Floating Point Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-765">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-765">Parameters</span></span>

- <span data-ttu-id="db2f7-766">**value**: puntatore alla descrizione del valore di più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-766">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="db2f7-767">**index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-767">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="db2f7-768">**instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-768">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="db2f7-769">**float64_ptr**: puntatore al valore a virgola mobile a 64 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-769">**float64_ptr**: Pointer to the destination 64-Bit Floating Point value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-770">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-770">Return Values</span></span>

- <span data-ttu-id="db2f7-771">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-771">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-772">**NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-772">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="db2f7-773">**NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="db2f7-773">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not a Floating Point value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_integer32"></a><span data-ttu-id="db2f7-774">nx_lwm2m_resource_multiple_get_integer32</span><span class="sxs-lookup"><span data-stu-id="db2f7-774">nx_lwm2m_resource_multiple_get_integer32</span></span>

<span data-ttu-id="db2f7-775">Ottenere il valore di un'istanza di più risorse di un Integer a 32 bit</span><span class="sxs-lookup"><span data-stu-id="db2f7-775">Get the value of a 32-Bit Integer Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-776">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-776">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_integer32(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-777">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-777">Description</span></span>

<span data-ttu-id="db2f7-778">Il servizio recupera il valore di un'istanza di risorsa Integer a 32 bit da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="db2f7-778">The service retrieves the value of a 32-Bit Integer Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-779">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-779">Parameters</span></span>

- <span data-ttu-id="db2f7-780">**value**: puntatore alla descrizione del valore di più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-780">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="db2f7-781">**index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-781">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="db2f7-782">**instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-782">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="db2f7-783">**int32_ptr**: puntatore al valore Integer a 32 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-783">**int32_ptr**: Pointer to the destination 32-Bit Integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-784">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-784">Return Values</span></span>

- <span data-ttu-id="db2f7-785">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-785">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-786">**NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-786">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="db2f7-787">**NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore intero oppure il valore integer non rientra in un numero a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="db2f7-787">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not an Integer value, or the Integer value doesn't fit in a 32-Bit number.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_integer64"></a><span data-ttu-id="db2f7-788">nx_lwm2m_resource_multiple_get_integer64</span><span class="sxs-lookup"><span data-stu-id="db2f7-788">nx_lwm2m_resource_multiple_get_integer64</span></span>

<span data-ttu-id="db2f7-789">Ottenere il valore di un'istanza di più risorse di un Integer a 64 bit</span><span class="sxs-lookup"><span data-stu-id="db2f7-789">Get the value of a 64-Bit Integer Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-790">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-790">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_integer64(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-791">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-791">Description</span></span>

<span data-ttu-id="db2f7-792">Il servizio recupera il valore di un'istanza di risorsa Integer a 64 bit da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="db2f7-792">The service retrieves the value of a 64-Bit Integer Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-793">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-793">Parameters</span></span>

- <span data-ttu-id="db2f7-794">**value**: puntatore alla descrizione del valore di più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-794">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="db2f7-795">**index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-795">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="db2f7-796">**instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-796">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="db2f7-797">**int64_ptr**: puntatore al valore Integer a 64 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-797">**int64_ptr**: Pointer to the destination 64-Bit Integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-798">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-798">Return Values</span></span>

- <span data-ttu-id="db2f7-799">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-799">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-800">**NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-800">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="db2f7-801">**NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore integer.</span><span class="sxs-lookup"><span data-stu-id="db2f7-801">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not an Integer value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_objlnk"></a><span data-ttu-id="db2f7-802">nx_lwm2m_resource_multiple_get_objlnk</span><span class="sxs-lookup"><span data-stu-id="db2f7-802">nx_lwm2m_resource_multiple_get_objlnk</span></span>

<span data-ttu-id="db2f7-803">Ottenere il valore di un oggetto collegamento a più istanze di risorse</span><span class="sxs-lookup"><span data-stu-id="db2f7-803">Get the value of an Object Link Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-804">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-804">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_objlnk(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-805">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-805">Description</span></span>

<span data-ttu-id="db2f7-806">Il servizio recupera il valore di un'istanza di risorsa collegamento a un oggetto da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="db2f7-806">The service retrieves the value of an Object Link Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-807">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-807">Parameters</span></span>

- <span data-ttu-id="db2f7-808">**value**: puntatore alla descrizione del valore di più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-808">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="db2f7-809">**index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-809">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="db2f7-810">**instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-810">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="db2f7-811">**objlnk_ptr**: puntatore al valore del collegamento all'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-811">**objlnk_ptr**: Pointer to the destination Object Link value.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-812">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-812">Return Values</span></span>

- <span data-ttu-id="db2f7-813">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-813">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-814">**NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-814">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="db2f7-815">**NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore di collegamento a un oggetto.</span><span class="sxs-lookup"><span data-stu-id="db2f7-815">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not an Object Link value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_opaque"></a><span data-ttu-id="db2f7-816">nx_lwm2m_resource_multiple_get_opaque</span><span class="sxs-lookup"><span data-stu-id="db2f7-816">nx_lwm2m_resource_multiple_get_opaque</span></span>

<span data-ttu-id="db2f7-817">Ottenere il valore di un'istanza di più risorse opaca</span><span class="sxs-lookup"><span data-stu-id="db2f7-817">Get the value of an Opaque Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-818">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-818">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_opaque(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const VOID **opaque_ptr_ptr,
    UINT *opaque_length_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-819">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-819">Description</span></span>

<span data-ttu-id="db2f7-820">Il servizio recupera il valore di un'istanza di risorsa opaca da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="db2f7-820">The service retrieves the value of an Opaque Resource Instance from a Multiple Resource.</span></span>

<span data-ttu-id="db2f7-821">Un valore di risorsa opaco è costituito da un puntatore a un buffer e una lunghezza.</span><span class="sxs-lookup"><span data-stu-id="db2f7-821">An opaque resource value consists of a pointer to a buffer and a length.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-822">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-822">Parameters</span></span>

- <span data-ttu-id="db2f7-823">**value**: puntatore alla descrizione del valore di più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-823">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="db2f7-824">**index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-824">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="db2f7-825">**instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-825">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="db2f7-826">**opaque_ptr_ptr**: puntatore al puntatore al buffer opaco di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-826">**opaque_ptr_ptr**: Pointer to the destination opaque buffer pointer.</span></span>
- <span data-ttu-id="db2f7-827">**opaque_length_ptr**: puntatore alla lunghezza del buffer opaco di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-827">**opaque_length_ptr**: Pointer to the destination opaque buffer length.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-828">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-828">Return Values</span></span>

- <span data-ttu-id="db2f7-829">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-829">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-830">**NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-830">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="db2f7-831">**NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore opaco.</span><span class="sxs-lookup"><span data-stu-id="db2f7-831">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not an Opaque value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_string"></a><span data-ttu-id="db2f7-832">nx_lwm2m_resource_multiple_get_string</span><span class="sxs-lookup"><span data-stu-id="db2f7-832">nx_lwm2m_resource_multiple_get_string</span></span>

<span data-ttu-id="db2f7-833">Ottenere il valore di una stringa con più istanze di risorse</span><span class="sxs-lookup"><span data-stu-id="db2f7-833">Get the value of a String Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="db2f7-834">Prototipo</span><span class="sxs-lookup"><span data-stu-id="db2f7-834">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_string(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const CHAR **string_ptr_ptr,
    UINT *string_length_ptr);
```

### <a name="description"></a><span data-ttu-id="db2f7-835">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db2f7-835">Description</span></span>

<span data-ttu-id="db2f7-836">Il servizio recupera il valore di un'istanza di risorsa stringa da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="db2f7-836">The service retrieves the value of a String Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="db2f7-837">Parametri</span><span class="sxs-lookup"><span data-stu-id="db2f7-837">Parameters</span></span>

- <span data-ttu-id="db2f7-838">**value**: puntatore alla descrizione del valore di più risorse.</span><span class="sxs-lookup"><span data-stu-id="db2f7-838">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="db2f7-839">**index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-839">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="db2f7-840">**instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-840">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="db2f7-841">**string_ptr_ptr**: puntatore al puntatore della stringa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-841">**string_ptr_ptr**: Pointer to the destination string pointer.</span></span>
- <span data-ttu-id="db2f7-842">**string_length_ptr**: puntatore alla lunghezza della stringa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="db2f7-842">**string_length_ptr**: Pointer to the destination string length.</span></span> <span data-ttu-id="db2f7-843">Può essere NULL se la stringa è con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="db2f7-843">Can be NULL if the string is null-terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="db2f7-844">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="db2f7-844">Return Values</span></span>

- <span data-ttu-id="db2f7-845">**NX_SUCCESS**: operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="db2f7-845">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="db2f7-846">**NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="db2f7-846">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="db2f7-847">**NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore dell'istanza non è un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="db2f7-847">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the instance value is not a String value.</span></span>
