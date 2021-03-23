---
title: Capitolo 4-Descrizione dei servizi CLIENT di LWM2M
description: Questo capitolo contiene una descrizione di tutti i servizi client di LWM2M in ordine alfabetico.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 825a215ba756b39b6d76e6cc773c288e8b8aab01
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821833"
---
# <a name="chapter-4--description-of-lwm2m-client-services"></a><span data-ttu-id="d5390-103">Capitolo 4 Descrizione dei servizi CLIENT di LWM2M</span><span class="sxs-lookup"><span data-stu-id="d5390-103">Chapter 4  Description of LWM2M CLIENT Services</span></span>

<span data-ttu-id="d5390-104">Questo capitolo contiene una descrizione di tutti i servizi client di LWM2M elencati di seguito in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="d5390-104">This chapter contains a description of all LWM2M Client services listed below in alphabetic order.</span></span>

<span data-ttu-id="d5390-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal  **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="d5390-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the  **NX_DISABLE_ERROR_CHECKING** define that is used to disable API  error checking, while non-bold values are completely disabled.</span></span>

<span data-ttu-id="d5390-106">**Gestione client LWM2M:**</span><span class="sxs-lookup"><span data-stu-id="d5390-106">**LWM2M Client Management:**</span></span>

- <span data-ttu-id="d5390-107">nx_lwm2m_client_create: *creare un client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-107">nx_lwm2m_client_create: *Create LWM2M Client*</span></span>

- <span data-ttu-id="d5390-108">nx_lwm2m_client_delete: *eliminare il client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-108">nx_lwm2m_client_delete: *Delete LWM2M Client*</span></span>

- <span data-ttu-id="d5390-109">nx_lwm2m_client_lock: *bloccare il client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-109">nx_lwm2m_client_lock: *Lock LWM2M Client*</span></span>

- <span data-ttu-id="d5390-110">nx_lwm2m_client_unlock: *sbloccare il client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-110">nx_lwm2m_client_unlock: *Unlock LWM2M Client*</span></span>

<span data-ttu-id="d5390-111">**Gestione delle sessioni client di LWM2M:**</span><span class="sxs-lookup"><span data-stu-id="d5390-111">**LWM2M Client Session Management:**</span></span>

- <span data-ttu-id="d5390-112">nx_lwm2m_client_session_create: *creare una sessione client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-112">nx_lwm2m_client_session_create: *Create LWM2M Client Session*</span></span>

- <span data-ttu-id="d5390-113">nx_lwm2m_client_session_delete: *eliminare la sessione del client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-113">nx_lwm2m_client_session_delete: *Delete LWM2M Client Session*</span></span>

- <span data-ttu-id="d5390-114">nx_lwm2m_client_session_bootstrap: *avviare una sessione con un server bootstrap*</span><span class="sxs-lookup"><span data-stu-id="d5390-114">nx_lwm2m_client_session_bootstrap: *Start a session with a Bootstrap Server*</span></span>

- <span data-ttu-id="d5390-115">nx_lwm2m_client_session_bootstrap_dtls: *avviare una sessione protetta con un server bootstrap*</span><span class="sxs-lookup"><span data-stu-id="d5390-115">nx_lwm2m_client_session_bootstrap_dtls: *Start a secure session with a Bootstrap Server*</span></span>

- <span data-ttu-id="d5390-116">nx_lwm2m_client_session_register_info_get: *ottenere informazioni sul registro del server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-116">nx_lwm2m_client_session_register_info_get: *Get LWM2M Server register info*</span></span>

- <span data-ttu-id="d5390-117">nx_lwm2m_client_session_register: *avviare una sessione con un server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-117">nx_lwm2m_client_session_register: *Start a session with a LWM2M Server*</span></span>

- <span data-ttu-id="d5390-118">nx_lwm2m_client_session_register_dtls: *avviare una sessione protetta con un server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-118">nx_lwm2m_client_session_register_dtls: *Start a secure session with a LWM2M Server*</span></span>

- <span data-ttu-id="d5390-119">nx_lwm2m_client_session_update: *aggiornare una sessione con un server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-119">nx_lwm2m_client_session_update: *Update a session with a LWM2M Server*</span></span>

- <span data-ttu-id="d5390-120">nx_lwm2m_client_session_deregister: *terminare una sessione con un server lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-120">nx_lwm2m_client_session_deregister: *Terminate a session with a LWM2M Server*</span></span>

- <span data-ttu-id="d5390-121">nx_lwm2m_client_session_error_get: *ottenere l'ultimo errore di una sessione*</span><span class="sxs-lookup"><span data-stu-id="d5390-121">nx_lwm2m_client_session_error_get: *Get last error of a session*</span></span>

<span data-ttu-id="d5390-122">**Implementazione dell'oggetto dispositivo:**</span><span class="sxs-lookup"><span data-stu-id="d5390-122">**Device Object Implementation:**</span></span>

- <span data-ttu-id="d5390-123">nx_lwm2m_client_device_callbacks_set: *impostare i callback dell'applicazione oggetto dispositivo*</span><span class="sxs-lookup"><span data-stu-id="d5390-123">nx_lwm2m_client_device_callbacks_set: *Set Device Object application callbacks*</span></span>

- <span data-ttu-id="d5390-124">nx_lwm2m_client_device_error_push: *aggiungere il codice di errore all'oggetto dispositivo*</span><span class="sxs-lookup"><span data-stu-id="d5390-124">nx_lwm2m_client_device_error_push: *Add error code to Device Object*</span></span>

- <span data-ttu-id="d5390-125">nx_lwm2m_client_device_error_reset: *Reimposta i codici di errore dell'oggetto dispositivo*</span><span class="sxs-lookup"><span data-stu-id="d5390-125">nx_lwm2m_client_device_error_reset: *Reset error codes of Device Object*</span></span>

- <span data-ttu-id="d5390-126">nx_lwm2m_client_device_resource_changed: *modifica del segnale della risorsa oggetto dispositivo*</span><span class="sxs-lookup"><span data-stu-id="d5390-126">nx_lwm2m_client_device_resource_changed: *Signal change of Device Object resource*</span></span>

<span data-ttu-id="d5390-127">**Implementazione dell'oggetto di aggiornamento del firmware:**</span><span class="sxs-lookup"><span data-stu-id="d5390-127">**Firmware Update Object Implementation:**</span></span>

- <span data-ttu-id="d5390-128">nx_lwm2m_firmware_create: *creare un oggetto di aggiornamento del firmware*</span><span class="sxs-lookup"><span data-stu-id="d5390-128">nx_lwm2m_firmware_create: *Create Firmware Update Object*</span></span>

- <span data-ttu-id="d5390-129">nx_lwm2m_firmware_package_info_set: *impostare le informazioni sul pacchetto di aggiornamento del firmware*</span><span class="sxs-lookup"><span data-stu-id="d5390-129">nx_lwm2m_firmware_package_info_set: *Set Firmware Update Package Information*</span></span>

- <span data-ttu-id="d5390-130">nx_lwm2m_firmware_result_set: *impostare il risultato dell'aggiornamento del firmware*</span><span class="sxs-lookup"><span data-stu-id="d5390-130">nx_lwm2m_firmware_result_set: *Set Firmware Update Result*</span></span>

- <span data-ttu-id="d5390-131">nx_lwm2m_firmware_state_set: *impostare lo stato di aggiornamento del firmware*</span><span class="sxs-lookup"><span data-stu-id="d5390-131">nx_lwm2m_firmware_state_set: *Set Firmware Update State*</span></span>

<span data-ttu-id="d5390-132">**Implementazione di oggetti personalizzati:**</span><span class="sxs-lookup"><span data-stu-id="d5390-132">**Custom Objects Implementation:**</span></span>

- <span data-ttu-id="d5390-133">nx_lwm2m_client_object_add: *aggiungere l'implementazione dell'oggetto al client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-133">nx_lwm2m_client_object_add: *Add Object implementation to LWM2M Client*</span></span>

- <span data-ttu-id="d5390-134">nx_lwm2m_client_object_remove: *rimuovere l'implementazione dell'oggetto dal client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-134">nx_lwm2m_client_object_remove: *Remove Object implementation from LWM2M Client*</span></span>

- <span data-ttu-id="d5390-135">nx_lwm2m_client_object_instance_add: *aggiungere un'istanza dell'oggetto al client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-135">nx_lwm2m_client_object_instance_add: *Add Object Instance to LWM2M Client*</span></span>

- <span data-ttu-id="d5390-136">nx_lwm2m_client_object_instance_remove: *rimuovere l'istanza dell'oggetto dal client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-136">nx_lwm2m_client_object_instance_remove: *Remove Object Instance from LWM2M Client*</span></span>

- <span data-ttu-id="d5390-137">nx_lwm2m_object_resource_changed: *modifica del segnale di un valore di risorsa di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-137">nx_lwm2m_object_resource_changed: *Signal change of a resource value of an Object Instance*</span></span>

<span data-ttu-id="d5390-138">**Gestione dei dispositivi locali**</span><span class="sxs-lookup"><span data-stu-id="d5390-138">**Local Device Management**</span></span>

- <span data-ttu-id="d5390-139">nx_lwm2m_client_object_create: *creare una nuova istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-139">nx_lwm2m_client_object_create: *Create a new Object Instance*</span></span>

- <span data-ttu-id="d5390-140">nx_lwm2m_client_object_delete: *eliminare un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-140">nx_lwm2m_client_object_delete: *Delete an Object Instance*</span></span>

- <span data-ttu-id="d5390-141">nx_lwm2m_client_object_discover: *individuazione delle risorse di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-141">nx_lwm2m_client_object_discover: *Discover resources of an Object Instance*</span></span>

- <span data-ttu-id="d5390-142">nx_lwm2m_client_object_execute: *eseguire la risorsa di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-142">nx_lwm2m_client_object_execute: *Execute resource of an Object Instance*</span></span>

- <span data-ttu-id="d5390-143">nx_lwm2m_client_object_next_get: *Ottiene l'elenco di oggetti implementati dal client lwm2m*</span><span class="sxs-lookup"><span data-stu-id="d5390-143">nx_lwm2m_client_object_next_get: *Get the list of Objects implemented by the LWM2M Client*</span></span>

- <span data-ttu-id="d5390-144">nx_lwm2m_client_object_instance_next_get: *Ottiene l'elenco di istanze di un oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-144">nx_lwm2m_client_object_instance_next_get: *Get the list of Instances of an Object*</span></span>

- <span data-ttu-id="d5390-145">nx_lwm2m_client_object_read: *leggere i valori delle risorse di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-145">nx_lwm2m_client_object_read: *Read resources values of an Object Instance*</span></span>

- <span data-ttu-id="d5390-146">nx_lwm2m_client_object_write: *modificare i valori delle risorse di un'istanza dell'oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-146">nx_lwm2m_client_object_write: *Change resources values of an Object instance*</span></span>

<span data-ttu-id="d5390-147">**Impostazione informazioni risorse e valori:**</span><span class="sxs-lookup"><span data-stu-id="d5390-147">**Resources Info and Values Setting:**</span></span>

- <span data-ttu-id="d5390-148">nx_lwm2m_client_resource_info_set: *impostare le informazioni sulla risorsa*</span><span class="sxs-lookup"><span data-stu-id="d5390-148">nx_lwm2m_client_resource_info_set: *Set the resource info*</span></span>

- <span data-ttu-id="d5390-149">nx_lwm2m_client_resource_string_set: *impostare il valore della risorsa come stringa*</span><span class="sxs-lookup"><span data-stu-id="d5390-149">nx_lwm2m_client_resource_string_set: *Set the resource value as string*</span></span>

- <span data-ttu-id="d5390-150">nx_lwm2m_client_resource_integer32_set: *impostare il valore della risorsa come intero a 32 bit*</span><span class="sxs-lookup"><span data-stu-id="d5390-150">nx_lwm2m_client_resource_integer32_set: *Set the resource value as 32-Bit integer*</span></span>

- <span data-ttu-id="d5390-151">nx_lwm2m_client_resource_integer64_set: *impostare il valore della risorsa come intero a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="d5390-151">nx_lwm2m_client_resource_integer64_set: *Set the resource value as 64-Bit integer*</span></span>

- <span data-ttu-id="d5390-152">nx_lwm2m_client_resource_float32_set: *impostare il valore della risorsa come float a 32 bit*</span><span class="sxs-lookup"><span data-stu-id="d5390-152">nx_lwm2m_client_resource_float32_set: *Set the resource value as 32-Bit float*</span></span>

- <span data-ttu-id="d5390-153">nx_lwm2m_client_resource_float64_set: *impostare il valore della risorsa come float a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="d5390-153">nx_lwm2m_client_resource_float64_set: *Set the resource value as 64-Bit float*</span></span>

- <span data-ttu-id="d5390-154">nx_lwm2m_client_resource_boolean_set: *impostare il valore della risorsa come valore booleano*</span><span class="sxs-lookup"><span data-stu-id="d5390-154">nx_lwm2m_client_resource_boolean_set: *Set the resource value as boolean*</span></span>

- <span data-ttu-id="d5390-155">nx_lwm2m_client_resource_objlnk_set: *impostare il valore della risorsa come collegamento all'oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-155">nx_lwm2m_client_resource_objlnk_set: *Set the resource value as object link*</span></span>

- <span data-ttu-id="d5390-156">nx_lwm2m_client_resource_opaque_set: *impostare il valore della risorsa come opaco*</span><span class="sxs-lookup"><span data-stu-id="d5390-156">nx_lwm2m_client_resource_opaque_set: *Set the resource value as opaque*</span></span>

- <span data-ttu-id="d5390-157">nx_lwm2m_client_resource_instance_set: *impostare il valore della risorsa come istanza di per più risorse*</span><span class="sxs-lookup"><span data-stu-id="d5390-157">nx_lwm2m_client_resource_instance_set: *Set the resource value as instance for multiple resource*</span></span>
-
- <span data-ttu-id="d5390-158">nx_lwm2m_client_resource_dim_set: *impostare la dimensione della risorsa per più risorse.*</span><span class="sxs-lookup"><span data-stu-id="d5390-158">nx_lwm2m_client_resource_dim_set: *Set the resource dimension for multiple resource.*</span></span>

<span data-ttu-id="d5390-159">**Informazioni sulle risorse e valori per ottenere:**</span><span class="sxs-lookup"><span data-stu-id="d5390-159">**Resources Info and Values Getting:**</span></span>

- <span data-ttu-id="d5390-160">nx_lwm2m_client_resource_info_get: *ottenere le informazioni sulle risorse*</span><span class="sxs-lookup"><span data-stu-id="d5390-160">nx_lwm2m_client_resource_info_get: *Get the resource info*</span></span>

- <span data-ttu-id="d5390-161">nx_lwm2m_client_resource_string_get: *recuperare il valore di una risorsa di stringa*</span><span class="sxs-lookup"><span data-stu-id="d5390-161">nx_lwm2m_client_resource_string_get: *Get the value of a string resource*</span></span>

- <span data-ttu-id="d5390-162">nx_lwm2m_client_resource_integer32_get: *recuperare il valore di una risorsa Integer a 32 bit*</span><span class="sxs-lookup"><span data-stu-id="d5390-162">nx_lwm2m_client_resource_integer32_get: *Get the value of a 32-Bit integer resource*</span></span>

- <span data-ttu-id="d5390-163">nx_lwm2m_client_resource_integer64_get: *recuperare il valore di una risorsa Integer a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="d5390-163">nx_lwm2m_client_resource_integer64_get: *Get the value of a 64-Bit integer resource*</span></span>

- <span data-ttu-id="d5390-164">nx_lwm2m_client_resource_float32_get: *recuperare il valore di una risorsa float a 32 bit*</span><span class="sxs-lookup"><span data-stu-id="d5390-164">nx_lwm2m_client_resource_float32_get: *Get the value of a 32-Bit float resource*</span></span>

- <span data-ttu-id="d5390-165">nx_lwm2m_client_resource_float64_get: *recuperare il valore di una risorsa float a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="d5390-165">nx_lwm2m_client_resource_float64_get: *Get the value of a 64-Bit float resource*</span></span>

- <span data-ttu-id="d5390-166">nx_lwm2m_client_resource_boolean_get: *recuperare il valore di una risorsa booleana*</span><span class="sxs-lookup"><span data-stu-id="d5390-166">nx_lwm2m_client_resource_boolean_get: *Get the value of a boolean resource*</span></span>

- <span data-ttu-id="d5390-167">nx_lwm2m_client_resource_objlnk_get: *recuperare il valore di una risorsa di collegamento a un oggetto*</span><span class="sxs-lookup"><span data-stu-id="d5390-167">nx_lwm2m_client_resource_objlnk_get: *Get the value of an object link resource*</span></span>

- <span data-ttu-id="d5390-168">nx_lwm2m_client_resource_opaque_get: *recuperare il valore di una risorsa opaca*</span><span class="sxs-lookup"><span data-stu-id="d5390-168">nx_lwm2m_client_resource_opaque_get: *Get the value of an opaque resource*</span></span>

- <span data-ttu-id="d5390-169">nx_lwm2m_client_resource_instance_get: *ottenere l'istanza della risorsa per più risorse*</span><span class="sxs-lookup"><span data-stu-id="d5390-169">nx_lwm2m_client_resource_instance_get: *Get the resource instance for multiple resource*</span></span>

- <span data-ttu-id="d5390-170">nx_lwm2m_client_resource_dim_get: *ottenere la dimensione della risorsa per più risorse.*</span><span class="sxs-lookup"><span data-stu-id="d5390-170">nx_lwm2m_client_resource_dim_get: *Get the resource dimension for multiple resource.*</span></span>

## <a name="nx_lwm2m_client_create"></a><span data-ttu-id="d5390-171">nx_lwm2m_client_create</span><span class="sxs-lookup"><span data-stu-id="d5390-171">nx_lwm2m_client_create</span></span>

<span data-ttu-id="d5390-172">Crea un client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-172">Creates a LWM2M client.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-173">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-173">Prototype</span></span>

```C
UINT nx_lwm2m_client_create(
    NX_LWM2M_CLIENT client_ptr,
    NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    const CHAR *name_ptr,
    UINT name_length,
    const CHAR *msisdn_ptr,
    UINT msisdn_length,
    UCHAR binding_modes,
    VOID *stack_ptr,
    ULONG stack_size,
    UINT priority);
```

### <a name="description"></a><span data-ttu-id="d5390-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-174">Description</span></span>

<span data-ttu-id="d5390-175">Questo servizio crea un'istanza del client LWM2M, che viene eseguita nel contesto del proprio thread ThreadX.</span><span class="sxs-lookup"><span data-stu-id="d5390-175">This service creates a LWM2M Client instance, which runs in the context of its own ThreadX thread.</span></span>

<span data-ttu-id="d5390-176">Il client LWM2M implementa i seguenti oggetti LWM2M OMA: Security (0), server (1), controllo di accesso (2) e Device (3).</span><span class="sxs-lookup"><span data-stu-id="d5390-176">The LWM2M Client implements the following OMA LWM2M Objects: Security (0), Server (1), Access Control (2) and Device (3).</span></span> <span data-ttu-id="d5390-177">Le altre implementazioni di oggetti devono essere aggiunte dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-177">The other objects implementations must be added by the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-178">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-178">Parameters</span></span>

- <span data-ttu-id="d5390-179">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-179">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-180">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d5390-180">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="d5390-181">**packet_pool_ptr** Puntatore al pool di pacchetti predefinito per il client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-181">**packet_pool_ptr** Pointer to the default packet pool for this LWM2M Client.</span></span>
- <span data-ttu-id="d5390-182">**name_ptr** Puntatore al nome dell'endpoint del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-182">**name_ptr** Pointer to LWM2M Client endpoint name.</span></span>
- <span data-ttu-id="d5390-183">**name_length** Lunghezza del nome dell'endpoint del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-183">**name_length** Length of LWM2M Client endpoint name.</span></span>
- <span data-ttu-id="d5390-184">**msisdn_ptr** Puntatore a MSISDN in cui è possibile raggiungere il client LWM2M per l'utilizzo con l'associazione SMS. può essere NULL se l'associazione SMS non è supportata.</span><span class="sxs-lookup"><span data-stu-id="d5390-184">**msisdn_ptr** Pointer to the MSISDN where the LWM2M Client can be reached for use with the SMS binding, can be NULL if SMS binding is not supported.</span></span>
- <span data-ttu-id="d5390-185">**msisdn_length** Lunghezza del numero MSISDN.</span><span class="sxs-lookup"><span data-stu-id="d5390-185">**msisdn_length** Length of MSISDN number.</span></span>
- <span data-ttu-id="d5390-186">**binding_modes** Il binding e le modalità supportate dal client LWM2M devono essere costituiti da una combinazione di flag di NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S e NX_LWM2M_BINDING_SQ.</span><span class="sxs-lookup"><span data-stu-id="d5390-186">**binding_modes** The binding and modes supported by the LWM2M Client, must be a combination of NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S and NX_LWM2M_BINDING_SQ flags.</span></span>
- <span data-ttu-id="d5390-187">**stack_ptr** Puntatore all'area dello stack di thread del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-187">**stack_ptr** Pointer to LWM2M Client thread stack area.</span></span>
- <span data-ttu-id="d5390-188">**stack_size** Dimensioni dello stack dei thread del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-188">**stack_size** The LWM2M Client thread stack size.</span></span>
- <span data-ttu-id="d5390-189">**priorità** di Priorità del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-189">**priority** Priority of LWM2M Client.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-190">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-190">Return Values</span></span>

- <span data-ttu-id="d5390-191">**NX_SUCCESS** Il client LWM2M è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d5390-191">**NX_SUCCESS** The LWM2M Client has been successfully created.</span></span>
- <span data-ttu-id="d5390-192">**NX_LWM2M_CLIENT_ERROR** Errore di creazione del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-192">**NX_LWM2M_CLIENT_ERROR** LWM2M Client create error.</span></span>
- <span data-ttu-id="d5390-193">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d5390-193">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="d5390-194">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-194">**NX_PTR_ERROR** Invalid pointer.</span></span>
- <span data-ttu-id="d5390-195">**NX_SIZE_ERROR** Dimensioni dello stack non valide.</span><span class="sxs-lookup"><span data-stu-id="d5390-195">**NX_SIZE_ERROR** Invalid stack size.</span></span>
- <span data-ttu-id="d5390-196">**NX_OPTION_ERROR** Priorità non valida.</span><span class="sxs-lookup"><span data-stu-id="d5390-196">**NX_OPTION_ERROR** Invalid priority.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-197">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-197">Allowed From</span></span>

<span data-ttu-id="d5390-198">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-198">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-199">Example</span></span>

```C
/* Create LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client, &ip_0, &pool_0, 
  "netxlwm2mclient", sizeof("netxlwm2mclient") - 1,           
                                NX_NULL, 0, NX_LWM2M_CLIENT_BINDING_U, 
                                stack_ptr, stack_size, priority);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully created.  */
```

## <a name="nx_lwm2m_client_delete"></a><span data-ttu-id="d5390-200">nx_lwm2m_client_delete</span><span class="sxs-lookup"><span data-stu-id="d5390-200">nx_lwm2m_client_delete</span></span>

<span data-ttu-id="d5390-201">Elimina un client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-201">Deletes a LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-202">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-202">Prototype</span></span>

```C
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-203">Description</span></span>

<span data-ttu-id="d5390-204">Questo servizio Elimina un'istanza del client LWM2M creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d5390-204">This service deletes a previously created LWM2M Client instance.</span></span>

<span data-ttu-id="d5390-205">Tutte le sessioni attualmente associate al client vengono eliminate anche da questa chiamata.</span><span class="sxs-lookup"><span data-stu-id="d5390-205">All sessions currently attached the client are also deleted by this call.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-206">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-206">Parameters</span></span>

- <span data-ttu-id="d5390-207">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-207">**client_ptr** Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-208">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-208">Return Values</span></span>

- <span data-ttu-id="d5390-209">**NX_SUCCESS** Il client LWM2M è stato eliminato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d5390-209">**NX_SUCCESS** The LWM2M Client has been successfully deleted.</span></span>
- <span data-ttu-id="d5390-210">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-210">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-211">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-211">Allowed From</span></span>

<span data-ttu-id="d5390-212">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-212">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-213">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-213">Example</span></span>

```c
/* Delete the LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_device_callback_set"></a><span data-ttu-id="d5390-214">nx_lwm2m_client_device_callback_set</span><span class="sxs-lookup"><span data-stu-id="d5390-214">nx_lwm2m_client_device_callback_set</span></span>

<span data-ttu-id="d5390-215">Imposta il callback dell'applicazione di un oggetto dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d5390-215">Sets a device object's application callback.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-216">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-216">Prototype</span></span>

```C
UINT **nx_lwm2m_client_device_callback_set**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_OPERATION_CALLBACK operation_callback);
```

### <a name="description"></a><span data-ttu-id="d5390-217">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-217">Description</span></span>

<span data-ttu-id="d5390-218">Questo servizio installa il callback dell'applicazione per l'implementazione di operazioni sulle risorse dell'oggetto dispositivo LWM2M che non sono gestite dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-218">This service installs the application callback for implementing operations on the LWM2M Device Object resources that are not handled by the LWM2M Client.</span></span>

<span data-ttu-id="d5390-219">Il client LWM2M implementa le risorse seguenti: codice errore (11), Reimposta codice errore (12), binding supportato e modalità (16), le operazioni per le altre risorse vengono reindirizzate all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-219">The LWM2M Client implements the following resources: Error Code (11), Reset Error Code (12) and Supported Binding and Modes (16), operations to the other resources are redirected to the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-220">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-220">Parameters</span></span>

- <span data-ttu-id="d5390-221">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-221">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-222">**operation_callback** Callback dell'operazione per "Read", "Discover", "Write" ed "Execute".</span><span class="sxs-lookup"><span data-stu-id="d5390-222">**operation_callback** The operation callback for “Read”, “Discover”, “Write” and “Execute”.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-223">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-223">Return Values</span></span>

- <span data-ttu-id="d5390-224">**NX_SUCCESS** Il callback dell'operazione è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d5390-224">**NX_SUCCESS** The operation callback has been successfully set.</span></span>
- <span data-ttu-id="d5390-225">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-225">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-226">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-226">Allowed From</span></span>

<span data-ttu-id="d5390-227">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-227">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-228">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-228">Example</span></span>

```c
/* Set device callback.  */
status = nx_lwm2m_client_device_callback_set(&lwm2m_client, device_operation);

/* If status is NX_SUCCESS a device callback was successfully set.  */
```

## <a name="nx_lwm2m_client_device_error_push"></a><span data-ttu-id="d5390-229">nx_lwm2m_client_device_error_push</span><span class="sxs-lookup"><span data-stu-id="d5390-229">nx_lwm2m_client_device_error_push</span></span>
<span data-ttu-id="d5390-230">Aggiunge un codice di errore a un oggetto dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d5390-230">Adds an error code to a device object.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-231">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-231">Prototype</span></span>

```C
UINT **nx_lwm2m_client_device_error_push**(
    NX_LWM2M_CLIENT *client_ptr,
    UCHAR code);
```

### <a name="description"></a><span data-ttu-id="d5390-232">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-232">Description</span></span>

<span data-ttu-id="d5390-233">Questo servizio aggiunge una nuova istanza alla risorsa del codice di errore (11) del dispositivo dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-233">This service adds a new instance to the Error Code (11) resource of the Object Device.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-234">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-234">Parameters</span></span>

- <span data-ttu-id="d5390-235">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-235">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-236">**codice** Nuovo codice di errore.</span><span class="sxs-lookup"><span data-stu-id="d5390-236">**code** The new error code.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-237">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-237">Return Values</span></span>

- <span data-ttu-id="d5390-238">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-238">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-239">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL**</span><span class="sxs-lookup"><span data-stu-id="d5390-239">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL**</span></span>

<span data-ttu-id="d5390-240">Il numero massimo di codici di errore archiviati è</span><span class="sxs-lookup"><span data-stu-id="d5390-240">The maximum number of stored error codes has</span></span>

<span data-ttu-id="d5390-241">è stato raggiunto.</span><span class="sxs-lookup"><span data-stu-id="d5390-241">been reached.</span></span>

<span data-ttu-id="d5390-242">NX_PTR_ERROR puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-242">NX_PTR_ERROR Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-243">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-243">Allowed From</span></span>

<span data-ttu-id="d5390-244">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-244">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-245">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-245">Example</span></span>

```C
/* Push device error 1 (Low battery power) to server.  */
status = nx_lwm2m_client_device_error_push(&lwm2m_client, 1);

/* If status is NX_SUCCESS a device error was successfully pushed.  */
```

## <a name="nx_lwm2m_client_device_error_reset"></a><span data-ttu-id="d5390-246">nx_lwm2m_client_device_error_reset</span><span class="sxs-lookup"><span data-stu-id="d5390-246">nx_lwm2m_client_device_error_reset</span></span>

<span data-ttu-id="d5390-247">Reimposta i codici di errore dell'oggetto dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d5390-247">Resets the error codes of Device Object.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-248">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-248">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-249">Description</span></span>

<span data-ttu-id="d5390-250">Questo servizio Elimina tutte le istanze di risorse del codice di errore dall'oggetto dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d5390-250">This service deletes all error code resource instances from the Device Object.</span></span> <span data-ttu-id="d5390-251">Equivale a eseguire il codice di errore di reimpostazione della risorsa (12).</span><span class="sxs-lookup"><span data-stu-id="d5390-251">This is equivalent to executing the resource Reset Error Code (12).</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-252">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-252">Parameters</span></span>

- <span data-ttu-id="d5390-253">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-253">**client_ptr** Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-254">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-254">Return Values</span></span>

- <span data-ttu-id="d5390-255">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-255">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-256">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-256">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-257">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-257">Allowed From</span></span>

<span data-ttu-id="d5390-258">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-258">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-259">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-259">Example</span></span>

```c
/* Delete all device error code.  */
status = nx_lwm2m_client_device_error_reset(&lwm2m_client);

/* If status is NX_SUCCESS, reset device error successfully.  */
```

## <a name="nx_lwm2m_client_device_resource_changed"></a><span data-ttu-id="d5390-260">nx_lwm2m_client_device_resource_changed</span><span class="sxs-lookup"><span data-stu-id="d5390-260">nx_lwm2m_client_device_resource_changed</span></span>

<span data-ttu-id="d5390-261">Segnala una modifica a una risorsa oggetto dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d5390-261">Signals a change to a Device Object resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-262">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-262">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_resource_changed(
    NX_LWM2M_CLIENT *client_ptr, 
    const NX_LWM2M_RESOURCE *resource);

```

### <a name="description"></a><span data-ttu-id="d5390-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-263">Description</span></span>

<span data-ttu-id="d5390-264">Il servizio viene usato dall'applicazione per segnalare al client LWM2M che una risorsa del dispositivo oggetto è cambiata.</span><span class="sxs-lookup"><span data-stu-id="d5390-264">The service is used by the application to signal to the LWM2M Client that a resource of the Object Device has changed.</span></span> <span data-ttu-id="d5390-265">Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-265">The LWM2M Client will send a notification if the resource is observed by a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-266">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-266">Parameters</span></span>

- <span data-ttu-id="d5390-267">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-267">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-268">**risorsa** di Puntatore alla struttura che descrive la risorsa che è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="d5390-268">**resource** Pointer to the structure describing the resource that has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-269">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-269">Return Values</span></span>

- <span data-ttu-id="d5390-270">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-270">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-271">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-271">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-272">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-272">Allowed From</span></span>

<span data-ttu-id="d5390-273">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-273">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-274">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-274">Example</span></span>

```c
/* Change device resource.  */
status = nx_lwm2m_client_device_resource_changed(&lwm2m_client, &resource);

/* If status is NX_SUCCESS, a device resource was successfully changed.  */
```

##  <a name="nx_lwm2m_client_firmware_create"></a><span data-ttu-id="d5390-275">nx_lwm2m_client_firmware_create</span><span class="sxs-lookup"><span data-stu-id="d5390-275">nx_lwm2m_client_firmware_create</span></span>

<span data-ttu-id="d5390-276">Creare un oggetto firmware del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-276">Create a LWM2M Client Firmware Object.</span></span> 

### <a name="prototype"></a><span data-ttu-id="d5390-277">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-277">Prototype</span></span>

```c
UINT nx_lwm2m_client_firmware_create(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    NX_LWM2M_CLIENT *client_ptr, 
    UINT protocols,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_URI_CALLBACK update_callback);
```

### <a name="description"></a><span data-ttu-id="d5390-278">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-278">Description</span></span>

<span data-ttu-id="d5390-279">Il servizio viene usato dall'applicazione per creare un oggetto firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-279">The service is used by the application to create firmware object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-280">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-280">Parameters</span></span>

- <span data-ttu-id="d5390-281">**firmware_ptr** Puntatore all'oggetto firmware del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-281">**firmware_ptr** Pointer to LWM2M Client Firmware object.</span></span>
- <span data-ttu-id="d5390-282">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-282">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-283">**protocolli** di Protocolli supportati.</span><span class="sxs-lookup"><span data-stu-id="d5390-283">**protocols** The supported protocols.</span></span>
- <span data-ttu-id="d5390-284">**package_callback** Callback del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-284">**package_callback** The package callback.</span></span>
- <span data-ttu-id="d5390-285">**package_uri_callback** Callback dell'URI del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-285">**package_uri_callback** The package URI callback.</span></span>
- <span data-ttu-id="d5390-286">**update_callback** Callback dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d5390-286">**update_callback** The update callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-287">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-287">Return Values</span></span>

<span data-ttu-id="d5390-288">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-288">**NX_SUCCESS** Successful operation.</span></span>
<span data-ttu-id="d5390-289">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-289">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-290">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-290">Allowed From</span></span>

<span data-ttu-id="d5390-291">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-291">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-292">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-292">Example</span></span>

```c
/* Create firmware object.  */
status = nx_lwm2m_client_firmware_create(&firmware, &lwm2m_client,     
                                         NX_LWM2M_CLIENT_FIRMWARE_PROTOCOL_HTTP, 
                                         NX_NULL, firmware_packet_uri,
                                         firmware_update);

/* If status is NX_SUCCESS, firmware object was successfully created.  */
```

##  <a name="nx_lwm2m_client_firmware_package_info_set"></a><span data-ttu-id="d5390-293">nx_lwm2m_client_firmware_package_info_set</span><span class="sxs-lookup"><span data-stu-id="d5390-293">nx_lwm2m_client_firmware_package_info_set</span></span>

<span data-ttu-id="d5390-294">Imposta le informazioni del pacchetto del firmware del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-294">Sets the LWM2M Client Firmware package information.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-295">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-295">Prototype</span></span>

```c
UINT nx_lwm2m_client_firmware_package_info_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    const CHAR *name, 
    UINT name_length, 
    const CHAR *version, 
    UINT version_length);
```

### <a name="description"></a><span data-ttu-id="d5390-296">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-296">Description</span></span>

<span data-ttu-id="d5390-297">Il servizio viene utilizzato dall'applicazione per impostare le risorse di informazioni sul pacchetto dell'oggetto di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-297">The service is used by the application to set the package information resources of the firmware update object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-298">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-298">Parameters</span></span>

- <span data-ttu-id="d5390-299">**firmware_ptr** Puntatore all'oggetto firmware del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-299">**firmware_ptr** Pointer to LWM2M Client Firmware object.</span></span>
- <span data-ttu-id="d5390-300">**nome** Nome del pacchetto del firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-300">**name** The name of firmware package.</span></span>
- <span data-ttu-id="d5390-301">**name_length** Lunghezza del nome.</span><span class="sxs-lookup"><span data-stu-id="d5390-301">**name_length** The length of name.</span></span>
- <span data-ttu-id="d5390-302">**versione** di Versione del pacchetto del firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-302">**version** The version of firmware package.</span></span>
- <span data-ttu-id="d5390-303">**version_length** Lunghezza della versione.</span><span class="sxs-lookup"><span data-stu-id="d5390-303">**version_length** The length of version.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-304">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-304">Return Values</span></span>

- <span data-ttu-id="d5390-305">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-305">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-306">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-306">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-307">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-307">Allowed From</span></span>

<span data-ttu-id="d5390-308">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-308">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-309">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-309">Example</span></span>

```c
/* Set the package information resources of the firmware object.  */
status = nx_lwm2m_client_firmware_package_info_set(&firmware, 2m_client,     
                                    “LWM2M Firmware”, sizeof(“LWM2M Firmware”) -1,
                                    “1.0.0.0”, sizeof(“1.0.0.0”) - 1);

/* If status is NX_SUCCESS, package information resources was successfully set. */
```

##  <a name="nx_lwm2m_client_firmware_result_set"></a><span data-ttu-id="d5390-310">nx_lwm2m_client_firmware_result_set</span><span class="sxs-lookup"><span data-stu-id="d5390-310">nx_lwm2m_client_firmware_result_set</span></span>

<span data-ttu-id="d5390-311">Imposta la risorsa risultato aggiornamento dell'oggetto aggiornamento firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-311">Sets the update result resource of the firmware update object.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-312">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-312">Prototype</span></span>

```c
UINT nx_lwm2m_client_firmware_result_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a><span data-ttu-id="d5390-313">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-313">Description</span></span>

<span data-ttu-id="d5390-314">Il servizio viene usato dall'applicazione per impostare la risorsa del risultato dell'aggiornamento dell'oggetto di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-314">The service is used by the application to set the update result resource of the firmware update object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-315">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-315">Parameters</span></span>

- <span data-ttu-id="d5390-316">**firmware_ptr** Puntatore all'oggetto firmware del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-316">**firmware_ptr** Pointer to LWM2M Client Firmware object.</span></span>
- <span data-ttu-id="d5390-317">**risultato** Risultato dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d5390-317">**result** The update result.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-318">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-318">Return Values</span></span>

- <span data-ttu-id="d5390-319">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-319">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-320">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-320">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-321">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-321">Allowed From</span></span>

<span data-ttu-id="d5390-322">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-322">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-323">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-323">Example</span></span>

```c
/* Set the update result resource of the firmware object.  */
status = nx_lwm2m_client_firmware_result_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_RESULT_SUCCESS);

/* If status is NX_SUCCESS, the update result resource was successfully set.  */
```

##  <a name="nx_lwm2m_client_firmware_state_set"></a><span data-ttu-id="d5390-324">nx_lwm2m_client_firmware_state_set</span><span class="sxs-lookup"><span data-stu-id="d5390-324">nx_lwm2m_client_firmware_state_set</span></span>

<span data-ttu-id="d5390-325">Imposta la risorsa risultato aggiornamento dell'oggetto aggiornamento firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-325">Sets the update result resource of the firmware update object.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-326">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-326">Prototype</span></span>

```c
UINT nx_lwm2m_client_firmware_state_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a><span data-ttu-id="d5390-327">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-327">Description</span></span>

<span data-ttu-id="d5390-328">Il servizio viene usato dall'applicazione per impostare lo stato dell'oggetto di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-328">The service is used by the application to set the state of the firmware update object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-329">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-329">Parameters</span></span>

- <span data-ttu-id="d5390-330">**firmware_ptr** Puntatore all'oggetto firmware del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-330">**firmware_ptr** Pointer to LWM2M Client Firmware object.</span></span>
- <span data-ttu-id="d5390-331">**stato** di Stato dell'oggetto firmware.</span><span class="sxs-lookup"><span data-stu-id="d5390-331">**state** The state of the firmware object.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-332">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-332">Return Values</span></span>

- <span data-ttu-id="d5390-333">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-333">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-334">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-334">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-335">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-335">Allowed From</span></span>

<span data-ttu-id="d5390-336">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-336">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-337">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-337">Example</span></span>

```c
/* Set the state of the firmware object.  */
status = nx_lwm2m_client_firmware_state_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_STATE_IDLE);

/* If status is NX_SUCCESS, the state was successfully set.  */
```

## <a name="nx_lwm2m_client_lock"></a><span data-ttu-id="d5390-338">nx_lwm2m_client_lock</span><span class="sxs-lookup"><span data-stu-id="d5390-338">nx_lwm2m_client_lock</span></span>

<span data-ttu-id="d5390-339">Blocca il client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-339">Locks the LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-340">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-340">Prototype</span></span>

```c
UINT **nx_lwm2m_client_lock**(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-341">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-341">Description</span></span>

<span data-ttu-id="d5390-342">Questo servizio blocca il client LWM2M per impedire l'accesso simultaneo agli oggetti LWM2M dai server o da un altro thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-342">This service locks the LWM2M Client to prevent concurrent access to the LWM2M objects from the servers or another application thread.</span></span>

<span data-ttu-id="d5390-343">Se il client LWM2M è attualmente bloccato da un altro thread, la funzione si bloccherà fino a quando non viene sbloccato il client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-343">If the LWM2M Client is currently locked by another thread, the function will block until the LWM2M Client is unlocked.</span></span>

<span data-ttu-id="d5390-344">Le chiamate alle coppie ***nx_lwm2m_client_lock** _/_ *_nx_lwm2m_client_unlock_** possono essere nidificate.</span><span class="sxs-lookup"><span data-stu-id="d5390-344">Calls to \***nx_lwm2m_client_lock**_/_*_nx_lwm2m_client_unlock_*\* pairs can be nested.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-345">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-345">Parameters</span></span>

- <span data-ttu-id="d5390-346">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-346">**client_ptr** Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-347">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-347">Return Values</span></span>

- <span data-ttu-id="d5390-348">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-348">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-349">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-349">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-350">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-350">Allowed From</span></span>

<span data-ttu-id="d5390-351">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-351">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-352">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-352">Example</span></span>

```c
/* Lock the LWM2M client.  */
status = nx_lwm2m_client_lock(&lwm2m_client);

/* If status is NX_SUCCESS, lwm2m client was successfully locked.  */
```

## <a name="nx_lwm2m_client_object_add"></a><span data-ttu-id="d5390-353">nx_lwm2m_client_object_add</span><span class="sxs-lookup"><span data-stu-id="d5390-353">nx_lwm2m_client_object_add</span></span>

<span data-ttu-id="d5390-354">Aggiunge un'implementazione dell'oggetto al client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-354">Adds an Object implementation to the LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-355">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-355">Prototype</span></span>

```c
UINT **nx_lwm2m_client_object_add**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK object_operation);
```

### <a name="description"></a><span data-ttu-id="d5390-356">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-356">Description</span></span>

<span data-ttu-id="d5390-357">Questo servizio aggiunge una nuova implementazione dell'oggetto al client di LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-357">This service adds a new Object implementation to the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-358">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-358">Parameters</span></span>

- <span data-ttu-id="d5390-359">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-359">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-360">**object_ptr** Puntatore alla struttura che definisce l'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-360">**object_ptr** Pointer to the structure defining the Object implementation.</span></span>
- <span data-ttu-id="d5390-361">**object_id** ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-361">**object_id** The object id.</span></span>
- <span data-ttu-id="d5390-362">**object_operation** Funzione di callback dell'operazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-362">**object_operation** The object operation callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-363">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-363">Return Values</span></span>

- <span data-ttu-id="d5390-364">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-364">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-365">**NX_LWM2M_CLIENT_ALREADY_EXIST** ID oggetto già esistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-365">**NX_LWM2M_CLIENT_ALREADY_EXIST** The Object ID already exists.</span></span>
- <span data-ttu-id="d5390-366">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-366">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-367">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-367">Allowed From</span></span>

<span data-ttu-id="d5390-368">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-368">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-369">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-369">Example</span></span>

```c
/* Add new object to the lwm2m client.  */
status = nx_lwm2m_client_object_add(&lwm2m_client, &object, 
                                    3303, object_operation);

/* If status is NX_SUCCESS, the new object was successfully added.  */
```

## <a name="nx_lwm2m_client_object_create"></a><span data-ttu-id="d5390-370">nx_lwm2m_client_object_create</span><span class="sxs-lookup"><span data-stu-id="d5390-370">nx_lwm2m_client_object_create</span></span>

<span data-ttu-id="d5390-371">Crea una nuova istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-371">Creates a new Object Instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-372">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-372">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_create(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-373">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-373">Description</span></span>

<span data-ttu-id="d5390-374">Questo servizio esegue un'operazione di creazione su un oggetto del client LWM2M per creare una nuova istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-374">This service performs a ‘Create’ operation on an Object of the LWM2M Client to create a new Object Instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-375">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-375">Parameters</span></span>

- <span data-ttu-id="d5390-376">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-376">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-377">**object_id** ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-377">**object_id** The Object ID.</span></span>
- <span data-ttu-id="d5390-378">**instance_id_ptr** Puntatore all'ID della nuova istanza, può essere **null** se il client LWM2M deve assegnare un ID istanza.</span><span class="sxs-lookup"><span data-stu-id="d5390-378">**instance_id_ptr** Pointer to the ID of the new instance, can be **NULL** if the LWM2M Client must assign an Instance ID.</span></span> <span data-ttu-id="d5390-379">Se l'ID è il valore riservato 65535, il client LWM2M assegnerà un ID istanza.</span><span class="sxs-lookup"><span data-stu-id="d5390-379">If the ID is the reserved value 65535 the LWM2M Client will assign an Instance ID.</span></span> <span data-ttu-id="d5390-380">Se non è NULL, l'ID assegnato viene restituito dopo la chiamata.</span><span class="sxs-lookup"><span data-stu-id="d5390-380">If not NULL the assigned ID is returned after the call.</span></span>
- <span data-ttu-id="d5390-381">**num_values** Numero di valori da impostare.</span><span class="sxs-lookup"><span data-stu-id="d5390-381">**num_values** The number of values to set.</span></span>
- <span data-ttu-id="d5390-382">**values_ptr** Puntatore a una matrice di valori di risorsa per inizializzare la nuova istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-382">**values_ptr** Pointer to an array of resource values to initialize the new Object Instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-383">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-383">Return Values</span></span>

- <span data-ttu-id="d5390-384">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-384">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-385">**NX_LWM2M_CLIENT_ALREADY_EXIST** L'ID dell'istanza dell'oggetto esiste già.</span><span class="sxs-lookup"><span data-stu-id="d5390-385">**NX_LWM2M_CLIENT_ALREADY_EXIST** The Object Instance ID already exists.</span></span>
- <span data-ttu-id="d5390-386">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** L'oggetto non supporta la creazione di istanze.</span><span class="sxs-lookup"><span data-stu-id="d5390-386">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** The Object doesn’t support instance creation.</span></span>
- <span data-ttu-id="d5390-387">**NX_LWM2M_CLIENT_NO_MEMORY** Impossibile allocare memoria per archiviare la nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="d5390-387">**NX_LWM2M_CLIENT_NO_MEMORY** Cannot allocate memory to store the new instance.</span></span>
- <span data-ttu-id="d5390-388">**NX_LWM2M_CLIENT_NOT_FOUND** L'ID oggetto non esiste.</span><span class="sxs-lookup"><span data-stu-id="d5390-388">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID doesn’t exist.</span></span>
- <span data-ttu-id="d5390-389">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-389">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-390">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-390">Allowed From</span></span>

<span data-ttu-id="d5390-391">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-391">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-392">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-392">Example</span></span>

```c
/* Create new object instance.  */
status = nx_lwm2m_client_object_create(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, a new object instance was successfully created.  */
```

## <a name="nx_lwm2m_client_object_delete"></a><span data-ttu-id="d5390-393">nx_lwm2m_client_object_delete</span><span class="sxs-lookup"><span data-stu-id="d5390-393">nx_lwm2m_client_object_delete</span></span>

<span data-ttu-id="d5390-394">Elimina un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-394">Deletes an Object Instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-395">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-395">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_delete(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a><span data-ttu-id="d5390-396">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-396">Description</span></span>

<span data-ttu-id="d5390-397">Questo servizio esegue un'operazione di eliminazione su un'istanza di oggetto del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-397">This service performs a ‘Delete’ operation on an Object Instance of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-398">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-398">Parameters</span></span>

- <span data-ttu-id="d5390-399">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-399">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-400">**object_id** ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-400">**object_id** The Object ID.</span></span>
- <span data-ttu-id="d5390-401">**Instance_Id** ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-401">**instance_id** The Object Instance ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-402">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-402">Return Values</span></span>

- <span data-ttu-id="d5390-403">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-403">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-404">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** L'oggetto non supporta l'eliminazione dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="d5390-404">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** The Object doesn’t support instance deletion.</span></span>
- <span data-ttu-id="d5390-405">**NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto o ID istanza oggetto inesistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-405">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID or Object Instance ID doesn’t exist.</span></span>
- <span data-ttu-id="d5390-406">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-406">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-407">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-407">Allowed From</span></span>

<span data-ttu-id="d5390-408">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-408">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-409">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-409">Example</span></span>

```c
/* Delete an object instance.  */
status = nx_lwm2m_client_object_delete(&lwm2m_client, 3303, 0);

/* If status is NX_SUCCESS, an object instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_object_discover"></a><span data-ttu-id="d5390-410">nx_lwm2m_client_object_discover</span><span class="sxs-lookup"><span data-stu-id="d5390-410">nx_lwm2m_client_object_discover</span></span>

<span data-ttu-id="d5390-411">Individua le risorse di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-411">Discovers resources of an Object Instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-412">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-412">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_discover(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT *num_resources,
    NX_LWM2M_CLIENT_RESOURCE *resources);

```

### <a name="description"></a><span data-ttu-id="d5390-413">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-413">Description</span></span>

<span data-ttu-id="d5390-414">Questo servizio esegue un'operazione di individuazione su un'istanza dell'oggetto del client LWM2M, restituisce l'elenco delle risorse implementate dall'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-414">This service performs a ‘Discover’ operation on an Object Instance of the LWM2M Client, this returns the list of resources implemented by the Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-415">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-415">Parameters</span></span>

- <span data-ttu-id="d5390-416">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-416">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-417">**object_id** ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-417">**object_id** The Object ID.</span></span>
- <span data-ttu-id="d5390-418">**Instance_Id** ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-418">**instance_id** The Object Instance ID.</span></span>
- <span data-ttu-id="d5390-419">**num_resources** In input dimensione del buffer di destinazione, in output il numero di elementi scritti nel buffer.</span><span class="sxs-lookup"><span data-stu-id="d5390-419">**num_resources** On input the size of the destination buffer, on output the number of elements written to the buffer.</span></span>
- <span data-ttu-id="d5390-420">**risorse** di Puntatore al buffer di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-420">**resources** Pointer to the destination buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-421">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-421">Return Values</span></span>

- <span data-ttu-id="d5390-422">*NX_SUCCESS*\* operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="d5390-422">*NX_SUCCESS*\* Successful operation.</span></span>
- <span data-ttu-id="d5390-423">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Il buffer di risorse è troppo piccolo per archiviare l'elenco di risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-423">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** The resources buffer is too small to store the list of resources.</span></span>
- <span data-ttu-id="d5390-424">**NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto o ID istanza oggetto inesistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-424">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID or Object Instance ID doesn’t exist.</span></span>
- <span data-ttu-id="d5390-425">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-425">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-426">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-426">Allowed From</span></span>

<span data-ttu-id="d5390-427">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-427">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-428">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-428">Example</span></span>

```c
NX_LWM2M_CLIENT_RESOURCE resources[10]
UINT num_resources = 10;

/* Discover object resources.  */
status = nx_lwm2m_client_object_discover(&lwm2m_client, 3303, 0, 
                                         &num_resources, resource);

/* If status is NX_SUCCESS, discover object resources successfully.  */
```

## <a name="nx_lwm2m_client_object_execute"></a><span data-ttu-id="d5390-429">nx_lwm2m_client_object_execute</span><span class="sxs-lookup"><span data-stu-id="d5390-429">nx_lwm2m_client_object_execute</span></span>

<span data-ttu-id="d5390-430">Esegue un'operazione di esecuzione su una risorsa di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-430">Performs an 'Execute' operation on a resource of an Object Instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-431">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-431">Prototype</span></span>

```C
UINT **nx_lwm2m_client_object_execute**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr,
    UINT arguments_length);
```

### <a name="description"></a><span data-ttu-id="d5390-432">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-432">Description</span></span>

<span data-ttu-id="d5390-433">Questo servizio esegue l'operazione di esecuzione su una risorsa dell'istanza di oggetto del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-433">This service performs the ‘Execute’ operation on an Object Instance Resource of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-434">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-434">Parameters</span></span>

- <span data-ttu-id="d5390-435">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-435">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-436">**object_id** ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-436">**object_id** The Object ID.</span></span>
- <span data-ttu-id="d5390-437">**Instance_Id** ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-437">**instance_id** The Object Instance ID.</span></span>
- <span data-ttu-id="d5390-438">**resource_id** ID della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-438">**resource_id** The Resource ID.</span></span>
- <span data-ttu-id="d5390-439">**arguments_ptr** Puntatore agli argomenti dell'operazione di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d5390-439">**arguments_ptr** Pointer to the arguments of the execute operation.</span></span> <span data-ttu-id="d5390-440">Può essere NULL se arguments_length è zero.</span><span class="sxs-lookup"><span data-stu-id="d5390-440">Can be NULL if arguments_length is zero.</span></span>
- <span data-ttu-id="d5390-441">**arguments_length** Lunghezza degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="d5390-441">**arguments_length** The length of the arguments.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-442">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-442">Return Values</span></span>

- <span data-ttu-id="d5390-443">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-443">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-444">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Il buffer di risorse è troppo piccolo per archiviare l'elenco di risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-444">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** The resources buffer is too small to store the list of resources.</span></span>
- <span data-ttu-id="d5390-445">**NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto o ID istanza oggetto inesistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-445">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID or Object Instance ID doesn’t exist.</span></span>
- <span data-ttu-id="d5390-446">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-446">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-447">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-447">Allowed From</span></span>

<span data-ttu-id="d5390-448">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-448">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-449">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-449">Example</span></span>

```c
/* Execute object resource.  */
status = nx_lwm2m_client_object_execute (&lwm2m_client, 3303, 0, 0,  
                                         “5”, 1);

/* If status is NX_SUCCESS, an object resource was successfully executed.  */
```

## <a name="nx_lwm2m_client_object_instance_add"></a><span data-ttu-id="d5390-450">nx_lwm2m_client_object_instance_add</span><span class="sxs-lookup"><span data-stu-id="d5390-450">nx_lwm2m_client_object_instance_add</span></span>

<span data-ttu-id="d5390-451">Aggiunge un'implementazione dell'istanza di oggetto a un oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-451">Adds an Object instance implementation to an object.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-452">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-452">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_instance_add(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-453">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-453">Description</span></span>

<span data-ttu-id="d5390-454">Questo servizio aggiunge una nuova implementazione dell'istanza di oggetto al client di LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-454">This service adds a new Object instance implementation to the LWM2M Client.</span></span> <span data-ttu-id="d5390-455">Se il valore di instance_id_ptr è **NX_LWM2M_CLIENT_RESERVED_ID**, il client di LWM2M assegna automaticamente un ID istanza non usato. in caso contrario, il client LWM2M utilizzerà il valore impostato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-455">If the value of instance_id_ptr is **NX_LWM2M_CLIENT_RESERVED_ID**, LWM2M Client will automatically assign an unused instance id, otherwise, LWM2M Client will use the value application set.</span></span> <span data-ttu-id="d5390-456">Una volta aggiunta la nuova istanza, l'instance_id verrà compilata instance_id_ptr per tornare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-456">Once new instance was added successfully, the instance_id will be filled in instance_id_ptr to return to application.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-457">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-457">Parameters</span></span>

- <span data-ttu-id="d5390-458">**object_ptr** Puntatore alla struttura che definisce l'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-458">**object_ptr** Pointer to the structure defining the Object implementation.</span></span>
- <span data-ttu-id="d5390-459">**instance_ptr** Puntatore alla struttura che definisce l'implementazione dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-459">**instance_ptr** Pointer to the structure defining the Object instance implementation.</span></span>
- <span data-ttu-id="d5390-460">**instance_id_ptr** Puntatore all'ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-460">**instance_id_ptr** Pointer to the object instance id.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-461">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-461">Return Values</span></span>

- <span data-ttu-id="d5390-462">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-462">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-463">**NX_CLIENT_LWM2M_ALREADY_EXIST** ID oggetto già esistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-463">**NX_CLIENT_LWM2M_ALREADY_EXIST** The Object ID already exists.</span></span>
- <span data-ttu-id="d5390-464">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-464">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-465">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-465">Allowed From</span></span>

<span data-ttu-id="d5390-466">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-466">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-467">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-467">Example</span></span>

```c
/* Add new object instance to the object.  */
status = nx_lwm2m_client_object_instance_add(&object, &object_instance,
                                             &instance_id);

/* If status is NX_SUCCESS, the new object instance was successfully added.  */
```

## <a name="nx_lwm2m_client_object_instance_next_get"></a><span data-ttu-id="d5390-468">nx_lwm2m_client_object_instance_next_get</span><span class="sxs-lookup"><span data-stu-id="d5390-468">nx_lwm2m_client_object_instance_next_get</span></span>

<span data-ttu-id="d5390-469">Ottiene l'istanza successiva di un oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-469">Gets the next instance of an Object.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-470">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-470">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_instance_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-471">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-471">Description</span></span>

<span data-ttu-id="d5390-472">Questo servizio restituisce l'ID dell'istanza di oggetto successiva dell'oggetto specificato.</span><span class="sxs-lookup"><span data-stu-id="d5390-472">This service returns the ID of the next Object Instance of the given Object.</span></span> <span data-ttu-id="d5390-473">Se l'ID istanza corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito l'ID della prima istanza.</span><span class="sxs-lookup"><span data-stu-id="d5390-473">If the current Instance ID is set to NX_LWM2M_RESERVED_ID (65535) the ID of the first instance is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-474">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-474">Parameters</span></span>

- <span data-ttu-id="d5390-475">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-475">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-476">**object_id** ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-476">**object_id** The Object ID.</span></span>
- <span data-ttu-id="d5390-477">**instance_id_ptr** Puntatore all'ID dell'istanza dell'oggetto corrente.</span><span class="sxs-lookup"><span data-stu-id="d5390-477">**instance_id_ptr** Pointer to the current Object Instance ID.</span></span> <span data-ttu-id="d5390-478">In return contiene l'ID dell'istanza successiva dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-478">On return contains the next Instance ID of the Object.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-479">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-479">Return Values</span></span>

- <span data-ttu-id="d5390-480">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-480">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-481">**NX_CLIENT_LWM2M_NOT_FOUND** L'ID istanza specificato è l'ultimo dell'oggetto o l'ID oggetto non è implementato.</span><span class="sxs-lookup"><span data-stu-id="d5390-481">**NX_CLIENT_LWM2M_NOT_FOUND** The given Instance ID is the last of the object, or the Object ID is not implemented.</span></span>
- <span data-ttu-id="d5390-482">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-482">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-483">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-483">Allowed From</span></span>

<span data-ttu-id="d5390-484">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-484">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-485">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-485">Example</span></span>

```c
/* Get the next instance of an object.  */
status = nx_lwm2m_client_object_instance_next_get(&lwm2m_client, 3303, 
                                                  &instance_id);

/* If status is NX_SUCCESS, get the next instance successfully.  */
```

## <a name="nx_lwm2m_client_object_instance_remove"></a><span data-ttu-id="d5390-486">nx_lwm2m_client_object_instance_remove</span><span class="sxs-lookup"><span data-stu-id="d5390-486">nx_lwm2m_client_object_instance_remove</span></span>

<span data-ttu-id="d5390-487">Rimuove un'implementazione dell'istanza di oggetto da un oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-487">Removes an  Object instance implementation from an object.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-488">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-488">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_instance_remove(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-489">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-489">Description</span></span>

<span data-ttu-id="d5390-490">Questo servizio rimuove un'istanza di oggetto da un oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-490">This service removes an Object instance from an object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-491">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-491">Parameters</span></span>

- <span data-ttu-id="d5390-492">***object_ptr*** Puntatore alla struttura che definisce l'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-492">***object_ptr*** Pointer to the structure defining the Object implementation.</span></span>
- <span data-ttu-id="d5390-493">**instance_ptr** Puntatore alla struttura che definisce l'implementazione dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-493">**instance_ptr** Pointer to the structure defining the Object instance implementation.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-494">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-494">Return Values</span></span>

- <span data-ttu-id="d5390-495">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-495">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-496">**NX_LWM2M_CLIENT_ALREADY_EXIST** ID oggetto già esistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-496">**NX_LWM2M_CLIENT_ALREADY_EXIST** The Object ID already exists.</span></span>
- <span data-ttu-id="d5390-497">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-497">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-498">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-498">Allowed From</span></span>

<span data-ttu-id="d5390-499">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-499">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-500">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-500">Example</span></span>

```c
/* Remove object instance from an object.  */
status = nx_lwm2m_client_object_instance_remove(&object, &object_instance);

/* If status is NX_SUCCESS, the object instance was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_next_get"></a><span data-ttu-id="d5390-501">nx_lwm2m_client_object_next_get</span><span class="sxs-lookup"><span data-stu-id="d5390-501">nx_lwm2m_client_object_next_get</span></span>

<span data-ttu-id="d5390-502">Ottiene l'oggetto successivo del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-502">Gets the next object of the LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-503">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-503">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID \*object_id_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-504">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-504">Description</span></span>

<span data-ttu-id="d5390-505">Questo servizio restituisce l'ID dell'oggetto successivo implementato dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-505">This service returns the ID of the next Object implemented by the LWM2M Client.</span></span> <span data-ttu-id="d5390-506">Se l'ID oggetto corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito il primo ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-506">If the current Object ID is set to NX_LWM2M_RESERVED_ID (65535) the first Object ID is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-507">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-507">Parameters</span></span>

- <span data-ttu-id="d5390-508">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-508">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-509">**object_id_ptr** Puntatore all'ID dell'oggetto corrente.</span><span class="sxs-lookup"><span data-stu-id="d5390-509">**object_id_ptr** Pointer to the current Object ID.</span></span> <span data-ttu-id="d5390-510">Il risultato restituito contiene l'ID oggetto successivo implementato dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-510">On return contains the next Object ID implemented by the LWM2M Client.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-511">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-511">Return Values</span></span>

- <span data-ttu-id="d5390-512">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-512">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-513">**NX_LWM2M_CLIENT_NOT_FOUND** L'ID oggetto specificato è l'ultimo del database.</span><span class="sxs-lookup"><span data-stu-id="d5390-513">**NX_LWM2M_CLIENT_NOT_FOUND** The given Object ID is the last of the database.</span></span>
<span data-ttu-id="d5390-514">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-514">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-515">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-515">Allowed From</span></span>

<span data-ttu-id="d5390-516">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-516">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-517">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-517">Example</span></span>

```c
/* Get the next object of lwm2m client.  */
status = nx_lwm2m_client_object_next_get(&lwm2m_client, &object_id);

/* If status is NX_SUCCESS, get the next object successfully.  */
```

## <a name="nx_lwm2m_client_object_read"></a><span data-ttu-id="d5390-518">nx_lwm2m_client_object_read</span><span class="sxs-lookup"><span data-stu-id="d5390-518">nx_lwm2m_client_object_read</span></span>

<span data-ttu-id="d5390-519">Legge i valori resource's di un'istanza di oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-519">Reads an Object Instance's resource's values.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-520">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-520">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_read(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a><span data-ttu-id="d5390-521">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-521">Description</span></span>

<span data-ttu-id="d5390-522">Questo servizio esegue un'operazione di lettura su un'istanza di oggetto del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-522">This service performs a ‘Read’ operation on an Object Instance of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-523">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-523">Parameters</span></span>

- <span data-ttu-id="d5390-524">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-524">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-525">**object_id** ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-525">**object_id** The Object ID.</span></span>
- <span data-ttu-id="d5390-526">**Instance_Id** ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-526">**instance_id** The Object Instance ID.</span></span>
- <span data-ttu-id="d5390-527">**num_values** Numero di risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="d5390-527">**num_values** The number of resources to read.</span></span>
- <span data-ttu-id="d5390-528">**values_ptr** Puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="d5390-528">**values_ptr** Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources to read.</span></span> <span data-ttu-id="d5390-529">In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="d5390-529">On return the array is filled with the corresponding types and values.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-530">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-530">Return Values</span></span>

- <span data-ttu-id="d5390-531">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-531">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-532">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Una risorsa non supporta l'operazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="d5390-532">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** A resource doesn’t support the read operation.</span></span>
- <span data-ttu-id="d5390-533">**NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto, ID istanza oggetto o ID risorsa inesistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-533">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID, Object Instance ID or a resource ID doesn’t exist.</span></span>
- <span data-ttu-id="d5390-534">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-534">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-535">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-535">Allowed From</span></span>

<span data-ttu-id="d5390-536">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-536">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-537">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-537">Example</span></span>

```c
/* Read the object resources.  */
status = nx_lwm2m_client_object_read(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, the resources were successfully read.  */
```

## <a name="nx_lwm2m_client_object_remove"></a><span data-ttu-id="d5390-538">nx_lwm2m_client_object_remove</span><span class="sxs-lookup"><span data-stu-id="d5390-538">nx_lwm2m_client_object_remove</span></span>

<span data-ttu-id="d5390-539">Rimuove un'implementazione dell'istanza di oggetto da un oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-539">Removes an Object instance implementation from an object.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-540">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-540">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_remove(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-541">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-541">Description</span></span>

<span data-ttu-id="d5390-542">Questo servizio rimuove un oggetto dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-542">This service removes an Object from the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-543">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-543">Parameters</span></span>

- <span data-ttu-id="d5390-544">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-544">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-545">**object_ptr** Puntatore alla struttura che definisce l'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-545">**object_ptr** Pointer to the structure defining the Object implementation.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-546">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-546">Return Values</span></span>

- <span data-ttu-id="d5390-547">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-547">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-548">**NX_LWM2M_CLIENT_ALREADY_EXIST** ID oggetto già esistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-548">**NX_LWM2M_CLIENT_ALREADY_EXIST** The Object ID already exists.</span></span>
- <span data-ttu-id="d5390-549">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-549">**NX_PTR_ERROR** Invalid pointer.</span></span>
- <span data-ttu-id="d5390-550">**NX_LWM2M_CLIENT_FORBIDDEN** La rimozione dell'oggetto interno non è consentita.</span><span class="sxs-lookup"><span data-stu-id="d5390-550">**NX_LWM2M_CLIENT_FORBIDDEN** Removing internal object is forbidden.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-551">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-551">Allowed From</span></span>

<span data-ttu-id="d5390-552">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-552">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-553">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-553">Example</span></span>

```c
/* Remove object from lwm2m client.  */
status = nx_lwm2m_client_object_remove(&lwm2m_client, &object);

/* If status is NX_SUCCESS, the object was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_resource_changed"></a><span data-ttu-id="d5390-554">nx_lwm2m_client_object_resource_changed</span><span class="sxs-lookup"><span data-stu-id="d5390-554">nx_lwm2m_client_object_resource_changed</span></span>

<span data-ttu-id="d5390-555">Segnala una modifica di una risorsa dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-555">Signals a change of an Object resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-556">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-556">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_resource_changed(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a><span data-ttu-id="d5390-557">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-557">Description</span></span>

<span data-ttu-id="d5390-558">Il servizio viene usato dall'applicazione per segnalare al client LWM2M che una risorsa dell'oggetto è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="d5390-558">The service is used by the application to signal to the LWM2M Client that a resource of the Object has changed.</span></span> <span data-ttu-id="d5390-559">Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-559">The LWM2M Client will send a notification if the resource is observed by a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-560">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-560">Parameters</span></span>

- <span data-ttu-id="d5390-561">**object_ptr** Puntatore alla struttura che definisce l'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-561">**object_ptr** Pointer to the structure defining the Object implementation.</span></span>
- <span data-ttu-id="d5390-562">***instance_ptr*** Puntatore alla struttura che definisce l'implementazione dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-562">***instance_ptr*** Pointer to the structure defining the Object instance implementation.</span></span>
- <span data-ttu-id="d5390-563">**risorsa** di Puntatore alla struttura che descrive la risorsa che è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="d5390-563">**resource** Pointer to the structure describing the resource that has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-564">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-564">Return Values</span></span>

- <span data-ttu-id="d5390-565">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-565">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-566">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-566">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-567">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-567">Allowed From</span></span>

<span data-ttu-id="d5390-568">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-568">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-569">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-569">Example</span></span>

```c
/* Change object resource.  */
status = nx_lwm2m_client_object_resource_changed(&object, &instance, &resource);

/* If status is NX_SUCCESS, a resource was successfully changed.  */
```

## <a name="nx_lwm2m_client_object_write"></a><span data-ttu-id="d5390-570">nx_lwm2m_client_object_write</span><span class="sxs-lookup"><span data-stu-id="d5390-570">nx_lwm2m_client_object_write</span></span>

<span data-ttu-id="d5390-571">Modifica i valori della risorsa di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-571">Changes resource's values of an Object instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-572">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-572">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_write(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr,
    UINT write_op);
```

### <a name="description"></a><span data-ttu-id="d5390-573">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-573">Description</span></span>

<span data-ttu-id="d5390-574">Questo servizio esegue un'operazione di scrittura su un'istanza di oggetto del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-574">This service performs a ‘Write’ operation on an Object Instance of the LWM2M Client.</span></span>

<span data-ttu-id="d5390-575">È possibile specificare le operazioni di scrittura seguenti per il parametro *write_op* .</span><span class="sxs-lookup"><span data-stu-id="d5390-575">The following write operations can be specified to the *write_op* parameter.</span></span>

| <span data-ttu-id="d5390-576">Valore</span><span class="sxs-lookup"><span data-stu-id="d5390-576">Value</span></span> | <span data-ttu-id="d5390-577">Operazione di scrittura &nbsp;</span><span class="sxs-lookup"><span data-stu-id="d5390-577">Write&nbsp;Operation</span></span> | <span data-ttu-id="d5390-578">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-578">Description</span></span> |
| --- | ---| --- |
| <span data-ttu-id="d5390-579">0</span><span class="sxs-lookup"><span data-stu-id="d5390-579">0</span></span> | <span data-ttu-id="d5390-580">Aggiornamento parziale</span><span class="sxs-lookup"><span data-stu-id="d5390-580">Partial Update</span></span> | <span data-ttu-id="d5390-581">Aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate le altre risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="d5390-581">Adds or updates Resources provided in the new value and leaves other existing Resources unchanged.</span></span> |
| <span data-ttu-id="d5390-582">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE**</span><span class="sxs-lookup"><span data-stu-id="d5390-582">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE**</span></span> | <span data-ttu-id="d5390-583">Sostituisci istanza</span><span class="sxs-lookup"><span data-stu-id="d5390-583">Replace Instance</span></span> | <span data-ttu-id="d5390-584">Sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa specificati.</span><span class="sxs-lookup"><span data-stu-id="d5390-584">Replaces the Object Instance with the new provided resource values.</span></span> |
| <span data-ttu-id="d5390-585">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE**</span><span class="sxs-lookup"><span data-stu-id="d5390-585">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE**</span></span> | <span data-ttu-id="d5390-586">Sostituisci risorsa</span><span class="sxs-lookup"><span data-stu-id="d5390-586">Replace Resource</span></span> | <span data-ttu-id="d5390-587">Sostituisce le risorse con i nuovi valori di risorsa forniti, usati per sostituire più risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-587">Replaces the Resources with the new provided resource values (used to replace Multiple Resources).</span></span> |
| <span data-ttu-id="d5390-588">**NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP**</span><span class="sxs-lookup"><span data-stu-id="d5390-588">**NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP**</span></span> | <span data-ttu-id="d5390-589">Scrittura bootstrap</span><span class="sxs-lookup"><span data-stu-id="d5390-589">Bootstrap Write</span></span> | <span data-ttu-id="d5390-590">Indica una chiamata da una sequenza di bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-590">Indicates a call from a Bootstrap sequence.</span></span> |

### <a name="parameters"></a><span data-ttu-id="d5390-591">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-591">Parameters</span></span>

- <span data-ttu-id="d5390-592">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-592">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="d5390-593">**object_id** ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-593">**object_id** The Object ID.</span></span>
- <span data-ttu-id="d5390-594">**Instance_Id** ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-594">**instance_id** The Object Instance ID.</span></span>
- <span data-ttu-id="d5390-595">**num_values** Numero di risorse da scrivere.</span><span class="sxs-lookup"><span data-stu-id="d5390-595">**num_values** The number of resources to write.</span></span>
- <span data-ttu-id="d5390-596">**values_ptr** Puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse, i tipi e i valori da scrivere.</span><span class="sxs-lookup"><span data-stu-id="d5390-596">**values_ptr** Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources, the types and the values to write.</span></span>
- <span data-ttu-id="d5390-597">**write_op** Tipo di operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="d5390-597">**write_op** The type of write operation.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-598">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-598">Return Values</span></span>

- <span data-ttu-id="d5390-599">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-599">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-600">**NX_LWM2M_CLIENT_BAD_ENCODING** Il tipo di una risorsa non è valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-600">**NX_LWM2M_CLIENT_BAD_ENCODING** The type of a resource is not valid.</span></span>
- <span data-ttu-id="d5390-601">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** La lunghezza di un valore è troppo grande per essere archiviata nell'istanza di.</span><span class="sxs-lookup"><span data-stu-id="d5390-601">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** The length of a value is too big to be stored in the instance.</span></span>
- <span data-ttu-id="d5390-602">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Una risorsa non supporta l'operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="d5390-602">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** A resource doesn’t support the write operation.</span></span>
- <span data-ttu-id="d5390-603">**NX_LWM2M_CLIENT_NO_MEMORY** Impossibile allocare memoria per archiviare un valore di risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-603">**NX_LWM2M_CLIENT_NO_MEMORY** Cannot allocate memory to store a resource value.</span></span>
- <span data-ttu-id="d5390-604">**NX_LWM2M_CLIENT_NOT_ACCEPTABLE** Il valore di una risorsa non è valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-604">**NX_LWM2M_CLIENT_NOT_ACCEPTABLE** The value of a resource is not valid.</span></span>
- <span data-ttu-id="d5390-605">**NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto, ID istanza oggetto o ID risorsa inesistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-605">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID, Object Instance ID or a resource ID doesn’t exist.</span></span>
- <span data-ttu-id="d5390-606">**NX_OPTION_ERROR** Tipo di operazione di scrittura non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-606">**NX_OPTION_ERROR** Invalid type of write operation.</span></span> 
- <span data-ttu-id="d5390-607">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-607">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-608">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-608">Allowed From</span></span>

<span data-ttu-id="d5390-609">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-609">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-610">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-610">Example</span></span>

```c
/* Write object resources.  */
status = nx_lwm2m_client_object_write(&lwm2m_client, 3303, 0, 2, &resource,
                                      NX_LWM2M_CLIENT_OBJECT_WRITE_UPDATE);

/* If status is NX_SUCCESS, write object resources successfully.  */
```

## <a name="nx_lwm2m_client_resource_boolean_get"></a><span data-ttu-id="d5390-611">nx_lwm2m_client_resource_boolean_get</span><span class="sxs-lookup"><span data-stu-id="d5390-611">nx_lwm2m_client_resource_boolean_get</span></span>

<span data-ttu-id="d5390-612">Ottiene il valore di una risorsa booleana.</span><span class="sxs-lookup"><span data-stu-id="d5390-612">Gets the value of a Boolean Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-613">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-613">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_boolean_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-614">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-614">Description</span></span>

<span data-ttu-id="d5390-615">Il servizio recupera il valore di una risorsa booleana.</span><span class="sxs-lookup"><span data-stu-id="d5390-615">The service retrieves the value of a Boolean Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-616">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-616">Parameters</span></span>

- <span data-ttu-id="d5390-617">**risorsa** di Puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-617">**resource** Pointer to Resource value description.</span></span>
- <span data-ttu-id="d5390-618">**bool_ptr** Puntatore al valore booleano di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-618">**bool_ptr** Pointer to the destination Boolean value.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-619">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-619">Return Values</span></span>

- <span data-ttu-id="d5390-620">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-620">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-621">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="d5390-621">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a Boolean value.</span></span>
- <span data-ttu-id="d5390-622">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-622">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-623">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-623">Allowed From</span></span>

<span data-ttu-id="d5390-624">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-624">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-625">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-625">Example</span></span>

```c
/* Get the value of a Boolean resource.  */
status = nx_lwm2m_client_resource_boolean_get(&resource, &bool);

/* If status is NX_SUCCESS, the value of Boolean resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_boolean_set"></a><span data-ttu-id="d5390-626">nx_lwm2m_client_resource_boolean_set</span><span class="sxs-lookup"><span data-stu-id="d5390-626">nx_lwm2m_client_resource_boolean_set</span></span>

<span data-ttu-id="d5390-627">Imposta il valore di una risorsa booleana.</span><span class="sxs-lookup"><span data-stu-id="d5390-627">Sets the value of a Boolean Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-628">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-628">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_boolean_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_BOOL bool_data);
```

### <a name="description"></a><span data-ttu-id="d5390-629">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-629">Description</span></span>

<span data-ttu-id="d5390-630">Il servizio imposta il valore di una risorsa booleana.</span><span class="sxs-lookup"><span data-stu-id="d5390-630">The service sets the value of a Boolean Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-631">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-631">Parameters</span></span>

- <span data-ttu-id="d5390-632">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-632">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-633">**bool_data** Dati booleani.</span><span class="sxs-lookup"><span data-stu-id="d5390-633">**bool_data** Boolean data.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-634">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-634">Return Values</span></span>

- <span data-ttu-id="d5390-635">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-635">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-636">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-636">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-637">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-637">Allowed From</span></span>

<span data-ttu-id="d5390-638">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-638">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-639">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-639">Example</span></span>

```c
/* Set the value of a Boolean resource.  */
status = nx_lwm2m_client_resource_boolean_set(&resource, NX_TRUE);

/* If status is NX_SUCCESS, the value of Boolean resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_dim_get"></a><span data-ttu-id="d5390-640">nx_lwm2m_client_resource_dim_get</span><span class="sxs-lookup"><span data-stu-id="d5390-640">nx_lwm2m_client_resource_dim_get</span></span>

<span data-ttu-id="d5390-641">Ottiene la dimensione della risorsa per più risorse</span><span class="sxs-lookup"><span data-stu-id="d5390-641">Gets the resource dimension for multiple Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-642">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-642">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_dim_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    UCHAR *dim);
```

### <a name="description"></a><span data-ttu-id="d5390-643">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-643">Description</span></span>

<span data-ttu-id="d5390-644">Il servizio recupera la dimensione della risorsa per più risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-644">The service retrieves the resource dimension for multiple resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-645">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-645">Parameters</span></span>

- <span data-ttu-id="d5390-646">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-646">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-647">puntatore **Dim** alla dimensione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-647">**dim** Pointer to the destination dimension.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-648">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-648">Return Values</span></span>

- <span data-ttu-id="d5390-649">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-649">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-650">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="d5390-650">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a Boolean value.</span></span>
- <span data-ttu-id="d5390-651">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-651">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-652">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-652">Allowed From</span></span>

<span data-ttu-id="d5390-653">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-653">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-654">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-654">Example</span></span>

```c
/* Get the resource dimension for multiple resource.  */
status = nx_lwm2m_client_resource_dim_get(&resource, &dim);

/* If status is NX_SUCCESS, the resource dimension was successfully get. */
```

## <a name="nx_lwm2m_client_resource_dim_set"></a><span data-ttu-id="d5390-655">nx_lwm2m_client_resource_dim_set</span><span class="sxs-lookup"><span data-stu-id="d5390-655">nx_lwm2m_client_resource_dim_set</span></span>

<span data-ttu-id="d5390-656">Imposta la dimensione della risorsa per più risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-656">Sets the resource dimension for multiple resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-657">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-657">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_dim_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    CHAR dim);
```

### <a name="description"></a><span data-ttu-id="d5390-658">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-658">Description</span></span>

<span data-ttu-id="d5390-659">Il servizio imposta la dimensione della risorsa per più risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-659">The service sets the resource dimension for multiple resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-660">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-660">Parameters</span></span>

- <span data-ttu-id="d5390-661">**valore** di Puntatore alla descrizione del valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-661">**value** Pointer to Resource value description.</span></span>
- <span data-ttu-id="d5390-662">valore **Dim** della dimensione.</span><span class="sxs-lookup"><span data-stu-id="d5390-662">**dim** Dimension value.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-663">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-663">Return Values</span></span>

- <span data-ttu-id="d5390-664">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-664">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-665">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-665">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-666">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-666">Allowed From</span></span>

<span data-ttu-id="d5390-667">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-667">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-668">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-668">Example</span></span>

```c
/* Set the resource dimension.  */
status = nx_lwm2m_client_resource_dim_set(&resource, 3);

/* If status is NX_SUCCESS, the resource dimension was successfully set. */
```

## <a name="nx_lwm2m_client_resource_float32_get"></a><span data-ttu-id="d5390-669">nx_lwm2m_client_resource_float32_get</span><span class="sxs-lookup"><span data-stu-id="d5390-669">nx_lwm2m_client_resource_float32_get</span></span>

<span data-ttu-id="d5390-670">Ottiene il valore di una risorsa **float** a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-670">Gets the value of a 32-Bit **float** Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-671">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-671">Prototype</span></span>

```C
UINT nx_lwm2m_client_resource_float32_get(
    NX_LWM2M_CLIENT_RESOURCE *resource,
    NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-672">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-672">Description</span></span>

<span data-ttu-id="d5390-673">Il servizio recupera il valore di una risorsa **float** a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-673">The service retrieves the value of a 32-Bit **float** Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-674">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-674">Parameters</span></span>

- <span data-ttu-id="d5390-675">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-675">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-676">**float32_ptr** Puntatore al valore **float** a 32 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-676">**float32_ptr** Pointer to the destination 32-Bit **float** value.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-677">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-677">Return Values</span></span>

- <span data-ttu-id="d5390-678">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-678">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-679">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="d5390-679">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a Boolean value.</span></span>
- <span data-ttu-id="d5390-680">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-680">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-681">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-681">Allowed From</span></span>

<span data-ttu-id="d5390-682">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-682">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-683">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-683">Example</span></span>

```C
/* Get the value of a 32-Bit float resource.  */
status = nx_lwm2m_client_resource_float32_get(&resource, &float32);

/* If status is NX_SUCCESS, the value of 32-Bit float resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_float32_set"></a><span data-ttu-id="d5390-684">nx_lwm2m_client_resource_float32_set</span><span class="sxs-lookup"><span data-stu-id="d5390-684">nx_lwm2m_client_resource_float32_set</span></span>

<span data-ttu-id="d5390-685">Imposta il valore di una risorsa **float** a 32 bit</span><span class="sxs-lookup"><span data-stu-id="d5390-685">Sets the value of a 32-Bit **float** Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-686">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-686">Prototype</span></span>

```C
UINT nx_lwm2m_client_resource_float32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource,
    NX_LWM2M_FLOAT32 float32_data);
```

### <a name="description"></a><span data-ttu-id="d5390-687">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-687">Description</span></span>

<span data-ttu-id="d5390-688">Il servizio imposta il valore di una risorsa **float** a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-688">The service sets the value of a 32-Bit **float** Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-689">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-689">Parameters</span></span>

- <span data-ttu-id="d5390-690">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-690">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-691">**float32_data** dati **float** a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-691">**float32_data** 32-Bit **float** data.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-692">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-692">Return Values</span></span>

- <span data-ttu-id="d5390-693">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-693">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-694">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-694">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-695">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-695">Allowed From</span></span>

<span data-ttu-id="d5390-696">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-696">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-697">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-697">Example</span></span>

```c
/* Set the value of a 32-Bit float resource.  */
status = nx_lwm2m_client_resource_float32_set(&resource, 1.24);

/* If status is NX_SUCCESS, the value of 32-Bit float resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_float64_get"></a><span data-ttu-id="d5390-698">nx_lwm2m_client_resource_float64_get</span><span class="sxs-lookup"><span data-stu-id="d5390-698">nx_lwm2m_client_resource_float64_get</span></span>

<span data-ttu-id="d5390-699">Ottiene il valore di una risorsa float a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-699">Gets the value of a 64-Bit float Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-700">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-700">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_float64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-701">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-701">Description</span></span>

<span data-ttu-id="d5390-702">Il servizio recupera il valore di una risorsa **float** a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-702">The service retrieves the value of a 64-Bit **float** Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-703">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-703">Parameters</span></span>

- <span data-ttu-id="d5390-704">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-704">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-705">**float64_ptr** Puntatore al valore **float** a 64 bit di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-705">**float64_ptr** Pointer to the destination 64-Bit **float** value.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-706">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-706">Return Values</span></span>

- <span data-ttu-id="d5390-707">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-707">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-708">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore float.</span><span class="sxs-lookup"><span data-stu-id="d5390-708">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a float value.</span></span>
- <span data-ttu-id="d5390-709">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-709">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-710">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-710">Allowed From</span></span>

<span data-ttu-id="d5390-711">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-711">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-712">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-712">Example</span></span>

```c
/* Get the value of a 64-Bit float resource.  */
status = nx_lwm2m_client_resource_float64_get(&resource, &float64);

/* If status is NX_SUCCESS, the value of 64-Bit float resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_float64_set"></a><span data-ttu-id="d5390-713">nx_lwm2m_client_resource_float64_set</span><span class="sxs-lookup"><span data-stu-id="d5390-713">nx_lwm2m_client_resource_float64_set</span></span>

<span data-ttu-id="d5390-714">Imposta il valore di una risorsa **float** a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-714">Sets the value of a 64-Bit **float** Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-715">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-715">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_float64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_FLOAT64 float64_data);
```

### <a name="description"></a><span data-ttu-id="d5390-716">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-716">Description</span></span>

<span data-ttu-id="d5390-717">Il servizio imposta il valore di una risorsa **float** a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-717">The service sets the value of a 64-Bit **float** Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-718">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-718">Parameters</span></span>

- <span data-ttu-id="d5390-719">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-719">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-720">**float64_data** dati **float** a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-720">**float64_data** 64-bit **float** data.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-721">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-721">Return Values</span></span>

- <span data-ttu-id="d5390-722">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-722">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-723">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-723">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-724">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-724">Allowed From</span></span>

<span data-ttu-id="d5390-725">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-725">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-726">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-726">Example</span></span>

```c
/* Set the value of a 64-Bit float resource.  */
status = nx_lwm2m_client_resource_float64_set(&resource, 1.24);

/* If status is NX_SUCCESS, the value of 64-Bit float resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_info_get"></a><span data-ttu-id="d5390-727">nx_lwm2m_client_resource_info_get</span><span class="sxs-lookup"><span data-stu-id="d5390-727">nx_lwm2m_client_resource_info_get</span></span>

<span data-ttu-id="d5390-728">Ottiene le informazioni sulla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-728">Gets the resource info.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-729">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-729">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_info_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *resource_id, 
    ULONG *operation);
```

### <a name="description"></a><span data-ttu-id="d5390-730">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-730">Description</span></span>

<span data-ttu-id="d5390-731">Il servizio recupera le informazioni sulla risorsa della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-731">The service retrieves the resource information of Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-732">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-732">Parameters</span></span>

- <span data-ttu-id="d5390-733">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-733">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-734">**resource_id** Puntatore all'ID risorsa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-734">**resource_id** Pointer to the destination resource ID.</span></span>
- <span data-ttu-id="d5390-735">**operazione** di Puntatore all'operazione della risorsa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-735">**operation** Pointer to the destination resource operation.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-736">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-736">Return Values</span></span>

- <span data-ttu-id="d5390-737">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-737">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-738">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-738">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-739">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-739">Allowed From</span></span>

<span data-ttu-id="d5390-740">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-740">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-741">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-741">Example</span></span>

```c
/* Get the resource information.  */
status = nx_lwm2m_client_resource_info_get(&resource, &resource_id, &operation);

/* If status is NX_SUCCESS, the resource information was successfully get. */
```

## <a name="nx_lwm2m_client_resource_info_set"></a><span data-ttu-id="d5390-742">nx_lwm2m_client_resource_info_set</span><span class="sxs-lookup"><span data-stu-id="d5390-742">nx_lwm2m_client_resource_info_set</span></span>

<span data-ttu-id="d5390-743">Imposta le informazioni sulla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-743">Sets the resource information.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-744">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-744">Prototype</span></span>

```C
UINT nx_lwm2m_client_resource_info_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    NX_LWM2M_FLOAT64 float64_data);
```

### <a name="description"></a><span data-ttu-id="d5390-745">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-745">Description</span></span>

<span data-ttu-id="d5390-746">Il servizio imposta le informazioni sulla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-746">The service sets the resource information.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-747">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-747">Parameters</span></span>

- <span data-ttu-id="d5390-748">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-748">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-749">**resource_id** ID della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-749">**resource_id** ID of the resource.</span></span>
- <span data-ttu-id="d5390-750">**operazione** di Operazione della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-750">**operation** Operation of the resource.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-751">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-751">Return Values</span></span>

- <span data-ttu-id="d5390-752">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-752">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-753">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-753">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-754">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-754">Allowed From</span></span>

<span data-ttu-id="d5390-755">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-755">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-756">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-756">Example</span></span>

```c
/* Set the resource information.  */
status = nx_lwm2m_client_resource_info_set(&resource, 0, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);

/* If status is NX_SUCCESS, the resource information was successfully set. */
```

## <a name="nx_lwm2m_client_resource_instances_get"></a><span data-ttu-id="d5390-757">nx_lwm2m_client_resource_instances_get</span><span class="sxs-lookup"><span data-stu-id="d5390-757">nx_lwm2m_client_resource_instances_get</span></span>

<span data-ttu-id="d5390-758">Ottiene l'istanza di più risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-758">Gets the instance of multiple resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-759">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-759">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_instances_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_CLIENT_RESOURCE *resource_instances, 
    UINT *count);
```

### <a name="description"></a><span data-ttu-id="d5390-760">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-760">Description</span></span>

<span data-ttu-id="d5390-761">Il servizio recupera le informazioni sulla risorsa della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-761">The service retrieves the resource information of Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-762">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-762">Parameters</span></span>

- <span data-ttu-id="d5390-763">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-763">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-764">**resource_instances** Puntatore all'ID risorsa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-764">**resource_instances** Pointer to the destination resource ID.</span></span>
- <span data-ttu-id="d5390-765">**numero** di Puntatore al conteggio.</span><span class="sxs-lookup"><span data-stu-id="d5390-765">**count** Pointer to the count.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-766">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-766">Return Values</span></span>

- <span data-ttu-id="d5390-767">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-767">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-768">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="d5390-768">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a Boolean value.</span></span>
- <span data-ttu-id="d5390-769">**NX_LWM2M_CLIENT_NO_MEMORY** Nessuna memoria per compilare le istanze.</span><span class="sxs-lookup"><span data-stu-id="d5390-769">**NX_LWM2M_CLIENT_NO_MEMORY** No memory to fill out instances.</span></span>
- <span data-ttu-id="d5390-770">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-770">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-771">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-771">Allowed From</span></span>

<span data-ttu-id="d5390-772">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-772">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-773">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-773">Example</span></span>

```c
/* Get the resource information.  */
status = nx_lwm2m_client_resource_instances_get(&resource, &resource_instances,
                                                &count);

/* If status is NX_SUCCESS, the instances of multiple resource information were successfully get. */
```

## <a name="nx_lwm2m_client_resource_instances_set"></a><span data-ttu-id="d5390-774">nx_lwm2m_client_resource_instances_set</span><span class="sxs-lookup"><span data-stu-id="d5390-774">nx_lwm2m_client_resource_instances_set</span></span>

<span data-ttu-id="d5390-775">Imposta le istanze della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-775">Sets the resource instances.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-776">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-776">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_instances_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_CLIENT_RESOURCE *resource_instances, 
    UINT count);
```
### <a name="description"></a><span data-ttu-id="d5390-777">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-777">Description</span></span>

<span data-ttu-id="d5390-778">Il servizio imposta le istanze di risorse per più risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-778">The service sets the resource instances for multiple resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-779">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-779">Parameters</span></span>

- <span data-ttu-id="d5390-780">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-780">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-781">**resource_instance** Puntatore a istanze di risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-781">**resource_instance** Pointer to resource instances.</span></span>
- <span data-ttu-id="d5390-782">**numero** di Conteggio delle istanze di risorse.</span><span class="sxs-lookup"><span data-stu-id="d5390-782">**count** Count of resource instances.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-783">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-783">Return Values</span></span>

- <span data-ttu-id="d5390-784">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-784">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-785">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-785">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-786">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-786">Allowed From</span></span>

<span data-ttu-id="d5390-787">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-787">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-788">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-788">Example</span></span>

```c
/* Set the resource information.  */
status = nx_lwm2m_client_resource_instances_set(&resource, &resource_instance, 2);

/* If status is NX_SUCCESS, the resource instances were successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer32_get"></a><span data-ttu-id="d5390-789">nx_lwm2m_client_resource_integer32_get</span><span class="sxs-lookup"><span data-stu-id="d5390-789">nx_lwm2m_client_resource_integer32_get</span></span>

<span data-ttu-id="d5390-790">Ottiene il valore di una risorsa Integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-790">Gets the value of a 32-Bit integer Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-791">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-791">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_integer32_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 *integer32_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-792">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-792">Description</span></span>

<span data-ttu-id="d5390-793">Il servizio recupera il valore di una risorsa Integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-793">The service retrieves the value of a 32-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-794">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-794">Parameters</span></span>

- <span data-ttu-id="d5390-795">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-795">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-796">**integer32_ptr** Puntatore al valore integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-796">**integer32_ptr** Pointer to the 32-Bit integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-797">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-797">Return Values</span></span>

- <span data-ttu-id="d5390-798">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-798">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-799">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore intero.</span><span class="sxs-lookup"><span data-stu-id="d5390-799">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not integer value.</span></span>
- <span data-ttu-id="d5390-800">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-800">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-801">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-801">Allowed From</span></span>

<span data-ttu-id="d5390-802">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-802">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-803">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-803">Example</span></span>

```c
/* Get the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_get(&resource, &integer32);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer32_set"></a><span data-ttu-id="d5390-804">nx_lwm2m_client_resource_integer32_set</span><span class="sxs-lookup"><span data-stu-id="d5390-804">nx_lwm2m_client_resource_integer32_set</span></span>

<span data-ttu-id="d5390-805">Imposta il valore di una risorsa Integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-805">Sets the value of a 32-Bit integer Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-806">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-806">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_integer32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 integer32_data);
```

### <a name="description"></a><span data-ttu-id="d5390-807">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-807">Description</span></span>

<span data-ttu-id="d5390-808">Il servizio imposta il valore di una risorsa Integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-808">The service sets the value of a 32-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-809">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-809">Parameters</span></span>

- <span data-ttu-id="d5390-810">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-810">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-811">**integer32_data** dati integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-811">**integer32_data** 32-Bit integer data.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-812">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-812">Return Values</span></span>

- <span data-ttu-id="d5390-813">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-813">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-814">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-814">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-815">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-815">Allowed From</span></span>

<span data-ttu-id="d5390-816">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-816">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-817">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-817">Example</span></span>

```c
/* Set the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_set(&resource, 8);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer64_get"></a><span data-ttu-id="d5390-818">nx_lwm2m_client_resource_integer64_get</span><span class="sxs-lookup"><span data-stu-id="d5390-818">nx_lwm2m_client_resource_integer64_get</span></span>

<span data-ttu-id="d5390-819">Ottiene il valore di una risorsa Integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-819">Gets the value of a 64-Bit integer Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-820">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-820">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_integer64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 *integer64_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-821">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-821">Description</span></span>

<span data-ttu-id="d5390-822">Il servizio recupera il valore di una risorsa Integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-822">The service retrieves the value of a 64-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-823">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-823">Parameters</span></span>

- <span data-ttu-id="d5390-824">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-824">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-825">**integer64_ptr** Puntatore al valore integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-825">**integer64_ptr** Pointer to the 64-Bit integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-826">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-826">Return Values</span></span>

- <span data-ttu-id="d5390-827">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-827">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-828">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-828">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not 64-Bit integer value.</span></span>
- <span data-ttu-id="d5390-829">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-829">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-830">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-830">Allowed From</span></span>

<span data-ttu-id="d5390-831">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-831">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-832">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-832">Example</span></span>

```c
/* Get the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_get(&resource, &integer64);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer64_set"></a><span data-ttu-id="d5390-833">nx_lwm2m_client_resource_integer64_set</span><span class="sxs-lookup"><span data-stu-id="d5390-833">nx_lwm2m_client_resource_integer64_set</span></span>

## <a name="set-the-value-of-a-64-bit-integer-resource"></a><span data-ttu-id="d5390-834">Impostare il valore di una risorsa Integer a 64 bit</span><span class="sxs-lookup"><span data-stu-id="d5390-834">Set the value of a 64-Bit integer Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-835">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-835">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_integer64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 integer64_data);
```

### <a name="description"></a><span data-ttu-id="d5390-836">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-836">Description</span></span>

<span data-ttu-id="d5390-837">Il servizio imposta il valore di una risorsa Integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-837">The service sets the value of a 64-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-838">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-838">Parameters</span></span>

- <span data-ttu-id="d5390-839">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-839">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-840">**integer64_data** intero a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-840">**integer64_data** 64-bit integer.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-841">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-841">Return Values</span></span>

- <span data-ttu-id="d5390-842">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-842">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-843">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-843">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-844">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-844">Allowed From</span></span>

<span data-ttu-id="d5390-845">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-845">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-846">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-846">Example</span></span>

```c
/* Set the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_set(&resource, 32323);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully set. */
```

##  <a name="nx_lwm2m_client_resource_objlnk_get"></a><span data-ttu-id="d5390-847">nx_lwm2m_client_resource_objlnk_get</span><span class="sxs-lookup"><span data-stu-id="d5390-847">nx_lwm2m_client_resource_objlnk_get</span></span>

<span data-ttu-id="d5390-848">Ottiene il valore di una risorsa di collegamento a un oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-848">Gets the value of an object link resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-849">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-849">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_objlnk_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *object_id, 
    NX_LWM2M_ID *instance_id);
```

### <a name="description"></a><span data-ttu-id="d5390-850">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-850">Description</span></span>

<span data-ttu-id="d5390-851">Il servizio recupera il valore del collegamento all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-851">The service retrieves the value of object link.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-852">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-852">Parameters</span></span>

- <span data-ttu-id="d5390-853">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-853">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-854">**object_id** Puntatore all'ID dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-854">**object_id** Pointer to the object ID.</span></span>
- <span data-ttu-id="d5390-855">**Instance_Id** Puntatore all'ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-855">**instance_id** Pointer to the object instance ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-856">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-856">Return Values</span></span>

- <span data-ttu-id="d5390-857">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-857">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-858">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore di collegamento all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-858">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not an object link value.</span></span>
- <span data-ttu-id="d5390-859">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-859">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-860">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-860">Allowed From</span></span>

<span data-ttu-id="d5390-861">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-861">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-862">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-862">Example</span></span>

```c
/* Get the value of the object link resource.  */
status = nx_lwm2m_client_resource_objlnk_get(&resource, &object_id, &instance_id);

/* If status is NX_SUCCESS, the object link value was successfully get. */
```

## <a name="nx_lwm2m_client_resource_objlnk_set"></a><span data-ttu-id="d5390-863">nx_lwm2m_client_resource_objlnk_set</span><span class="sxs-lookup"><span data-stu-id="d5390-863">nx_lwm2m_client_resource_objlnk_set</span></span>

<span data-ttu-id="d5390-864">Imposta le istanze di risorse</span><span class="sxs-lookup"><span data-stu-id="d5390-864">Sets the resource instances</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-865">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-865">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_objlnk_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    NX_LWM2M_ID object_id, 
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a><span data-ttu-id="d5390-866">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-866">Description</span></span>

<span data-ttu-id="d5390-867">Il servizio imposta il valore della risorsa collegamento a oggetti.</span><span class="sxs-lookup"><span data-stu-id="d5390-867">The service sets the value of the object link resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-868">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-868">Parameters</span></span>

- <span data-ttu-id="d5390-869">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-869">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-870">**object_id** ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-870">**object_id** Object ID.</span></span>
- <span data-ttu-id="d5390-871">**Instance_Id** ID istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5390-871">**instance_id** Object instance ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-872">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-872">Return Values</span></span>

- <span data-ttu-id="d5390-873">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-873">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-874">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-874">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-875">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-875">Allowed From</span></span>

<span data-ttu-id="d5390-876">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-876">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-877">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-877">Example</span></span>

```c
/* Set the value of object link resource.  */
status = nx_lwm2m_client_resource_objlnk_set(&resource, 3303, 2);

/* If status is NX_SUCCESS, the value of object link resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_opaque_get"></a><span data-ttu-id="d5390-878">nx_lwm2m_client_resource_opaque_get</span><span class="sxs-lookup"><span data-stu-id="d5390-878">nx_lwm2m_client_resource_opaque_get</span></span>

<span data-ttu-id="d5390-879">Ottiene il valore di una risorsa opaca.</span><span class="sxs-lookup"><span data-stu-id="d5390-879">Gets the value of an opaque Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-880">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-880">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_opaque_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const VOID **opaque_ptr, 
    UINT \*opaque_length);
```


### <a name="description"></a><span data-ttu-id="d5390-881">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-881">Description</span></span>

<span data-ttu-id="d5390-882">Il servizio recupera il valore di una risorsa opaca.</span><span class="sxs-lookup"><span data-stu-id="d5390-882">The service retrieves the value of an opaque Resource.</span></span> <span data-ttu-id="d5390-883">Un valore di risorsa opaco è costituito da un puntatore a un buffer e una lunghezza.</span><span class="sxs-lookup"><span data-stu-id="d5390-883">An opaque resource value consists of a pointer to a buffer and a length.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-884">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-884">Parameters</span></span>

- <span data-ttu-id="d5390-885">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-885">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-886">**opaque_ptr** Puntatore ai dati opachi.</span><span class="sxs-lookup"><span data-stu-id="d5390-886">**opaque_ptr** Pointer to the opaque data.</span></span>
- <span data-ttu-id="d5390-887">**opaque_length** Puntatore alla lunghezza dei dati opachi.</span><span class="sxs-lookup"><span data-stu-id="d5390-887">**opaque_length** Pointer to the opaque data length.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-888">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-888">Return Values</span></span>

- <span data-ttu-id="d5390-889">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-889">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-890">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è una risorsa opaca.</span><span class="sxs-lookup"><span data-stu-id="d5390-890">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not an opaque resource.</span></span>
- <span data-ttu-id="d5390-891">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-891">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-892">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-892">Allowed From</span></span>

<span data-ttu-id="d5390-893">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-893">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-894">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-894">Example</span></span>

```c
/* Get the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_get(&resource, &opaque_ptr, &opaque_length);

/* If status is NX_SUCCESS, the value of opaque resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_opaque_set"></a><span data-ttu-id="d5390-895">nx_lwm2m_client_resource_opaque_set</span><span class="sxs-lookup"><span data-stu-id="d5390-895">nx_lwm2m_client_resource_opaque_set</span></span>

<span data-ttu-id="d5390-896">Imposta il valore di una risorsa opaca.</span><span class="sxs-lookup"><span data-stu-id="d5390-896">Sets the value of an opaque Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-897">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-897">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_opaque_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    VOID *opaque_ptr, 
    UINT opaque_length);
```

### <a name="description"></a><span data-ttu-id="d5390-898">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-898">Description</span></span>

<span data-ttu-id="d5390-899">Il servizio imposta il valore di una risorsa opaca.</span><span class="sxs-lookup"><span data-stu-id="d5390-899">The service sets the value of an opaque Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-900">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-900">Parameters</span></span>

- <span data-ttu-id="d5390-901">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-901">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-902">**opaque_ptr** Puntatore ai dati opachi.</span><span class="sxs-lookup"><span data-stu-id="d5390-902">**opaque_ptr** Pointer to the opaque data.</span></span>
- <span data-ttu-id="d5390-903">**opaque_length** Lunghezza dei dati opachi.</span><span class="sxs-lookup"><span data-stu-id="d5390-903">**opaque_length** Length of the opaque data.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-904">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-904">Return Values</span></span>

- <span data-ttu-id="d5390-905">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-905">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-906">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-906">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-907">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-907">Allowed From</span></span>

<span data-ttu-id="d5390-908">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-908">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-909">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-909">Example</span></span>

```c
/* Set the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_set(&resource, “AQIDBAU=”, 8);

/* If status is NX_SUCCESS, the value of opaque resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_string_get"></a><span data-ttu-id="d5390-910">nx_lwm2m_client_resource_string_get</span><span class="sxs-lookup"><span data-stu-id="d5390-910">nx_lwm2m_client_resource_string_get</span></span>

<span data-ttu-id="d5390-911">Ottiene il valore di una risorsa di stringa.</span><span class="sxs-lookup"><span data-stu-id="d5390-911">Gets the value of a string Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-912">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-912">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_string_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const CHAR **string_ptr, 
    UINT *string_length);
```

### <a name="description"></a><span data-ttu-id="d5390-913">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-913">Description</span></span>

<span data-ttu-id="d5390-914">Il servizio recupera il valore di una risorsa di stringa.</span><span class="sxs-lookup"><span data-stu-id="d5390-914">The service retrieves the value of a string Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-915">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-915">Parameters</span></span>

- <span data-ttu-id="d5390-916">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-916">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-917">**string_ptr** Puntatore al puntatore della stringa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-917">**string_ptr** Pointer to the destination string pointer.</span></span>
- <span data-ttu-id="d5390-918">**string_length** Puntatore alla lunghezza della stringa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-918">**string_length** Pointer to the destination string length.</span></span> <span data-ttu-id="d5390-919">Può essere **null** se la stringa è con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="d5390-919">Can be **NULL** if the string is null-terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-920">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-920">Return Values</span></span>

- <span data-ttu-id="d5390-921">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-921">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-922">**NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="d5390-922">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a string value.</span></span>
- <span data-ttu-id="d5390-923">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-923">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-924">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-924">Allowed From</span></span>

<span data-ttu-id="d5390-925">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-925">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-926">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-926">Example</span></span>

```c
/* Get the value of a string resource.  */
status = nx_lwm2m_client_resource_string_get(&resource, &string_ptr, &string_length);

/* If status is NX_SUCCESS, the value of string resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_string_set"></a><span data-ttu-id="d5390-927">nx_lwm2m_client_resource_string_set</span><span class="sxs-lookup"><span data-stu-id="d5390-927">nx_lwm2m_client_resource_string_set</span></span>

<span data-ttu-id="d5390-928">Imposta il valore di una risorsa di stringa.</span><span class="sxs-lookup"><span data-stu-id="d5390-928">Sets the value of a string Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-929">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-929">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_string_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    CHAR *string_ptr, 
    UINT string_length);
```

### <a name="description"></a><span data-ttu-id="d5390-930">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-930">Description</span></span>

<span data-ttu-id="d5390-931">Il servizio imposta il valore di una risorsa Integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d5390-931">The service sets the value of a 64-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-932">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-932">Parameters</span></span>

- <span data-ttu-id="d5390-933">**risorsa** di Puntatore alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5390-933">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="d5390-934">**string_ptr** Puntatore alla stringa.</span><span class="sxs-lookup"><span data-stu-id="d5390-934">**string_ptr** Pointer to the string.</span></span>
- <span data-ttu-id="d5390-935">**string_length** Lunghezza della stringa.</span><span class="sxs-lookup"><span data-stu-id="d5390-935">**string_length** Length of the string.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-936">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-936">Return Values</span></span>

- <span data-ttu-id="d5390-937">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-937">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-938">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-938">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-939">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-939">Allowed From</span></span>

<span data-ttu-id="d5390-940">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-940">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-941">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-941">Example</span></span>

```c
/* Set the value of a string resource.  */
status = nx_lwm2m_client_resource_string_set(&resource, “test”, sizeof(“test”) - 1);

/* If status is NX_SUCCESS, the value of string resource was successfully set. */
```

## <a name="nx_lwm2m_client_session_bootstrap"></a><span data-ttu-id="d5390-942">nx_lwm2m_client_session_bootstrap</span><span class="sxs-lookup"><span data-stu-id="d5390-942">nx_lwm2m_client_session_bootstrap</span></span>

<span data-ttu-id="d5390-943">Avvia una sessione con un server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-943">Starts a session with a Bootstrap Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-944">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-944">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_bootstrap(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID security_id, 
    ULONG ip_address, 
    UINT port);
```

### <a name="description"></a><span data-ttu-id="d5390-945">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-945">Description</span></span>

<span data-ttu-id="d5390-946">Questo servizio avvia una sessione con un server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-946">This service starts a session with a Bootstrap Server.</span></span> <span data-ttu-id="d5390-947">Il server deve disporre di un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5390-947">The server should have a corresponding security instance in the Security Object.</span></span>

<span data-ttu-id="d5390-948">Se la risorsa ' Mantieni fuori ' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà il bootstrap avviato dal server, se non è stato avviato alcun bootstrap dal server dopo questo periodo di tempo in cui verrà eseguito un bootstrap avviato dal client.</span><span class="sxs-lookup"><span data-stu-id="d5390-948">If the ‘Hold Off’ resource is different than zero in the Security Instance associated with this server the session will wait for a Server Initiated Bootstrap, If no bootstrap is initiated by the server after this period of time a Client Initiated Boostrap will be performed.</span></span>

<span data-ttu-id="d5390-949">Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-949">Any current active session is aborted by this call and replaced by the new Bootstrap Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-950">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-950">Parameters</span></span>

- <span data-ttu-id="d5390-951">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-951">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="d5390-952">**security_id** L'ID dell'istanza di sicurezza del server bootstrap deve essere impostato su NX_LWM2M_RESERVED_ID (65535) se nel server bootstrap non è definita alcuna istanza di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5390-952">**security_id** The Security Instance ID of the Bootstrap Server, must be set to NX_LWM2M_RESERVED_ID (65535) if the Bootstrap Server has no Security Instance defined.</span></span>
- <span data-ttu-id="d5390-953">**ip_address** Indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="d5390-953">**ip_address** The IP address of the server.</span></span>
- <span data-ttu-id="d5390-954">**porta** Porta UDP del server.</span><span class="sxs-lookup"><span data-stu-id="d5390-954">**port** The UDP port of the server.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-955">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-955">Return Values</span></span>

- <span data-ttu-id="d5390-956">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-956">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-957">**NX_LWM2M_CLIENT_ERROR** Errore bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-957">**NX_LWM2M_CLIENT_ERROR** Bootstrap error.</span></span>
- <span data-ttu-id="d5390-958">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d5390-958">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="d5390-959">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-959">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-960">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-960">Allowed From</span></span>

<span data-ttu-id="d5390-961">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-961">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-962">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-962">Example</span></span>

```c
/* Start bootstrap.  */
status = nx_lwm2m_client_session_bootstrap(&lwm2m_client, 0, &ip_address, 5783);

/* If status is NX_SUCCESS, start bootstrap successfully.  */
```

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a><span data-ttu-id="d5390-963">nx_lwm2m_client_session_bootstrap_dtls</span><span class="sxs-lookup"><span data-stu-id="d5390-963">nx_lwm2m_client_session_bootstrap_dtls</span></span>

<span data-ttu-id="d5390-964">Avvia una sessione protetta con un server bootstrap</span><span class="sxs-lookup"><span data-stu-id="d5390-964">Starts a secure session with a Bootstrap Server</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-965">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-965">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID security_id, 
    ULONG ip_address, 
    UINT port, 
    NX_SECURE_DTLS_SESSION *dtls_session_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-966">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-966">Description</span></span>

<span data-ttu-id="d5390-967">Questo servizio avvia una sessione con un server bootstrap usando una connessione DTLS sicura.</span><span class="sxs-lookup"><span data-stu-id="d5390-967">This service start a session with a Bootstrap Server using a secure DTLS connection.</span></span> <span data-ttu-id="d5390-968">Il server deve disporre di un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5390-968">The server should have a corresponding security instance in the Security Object.</span></span>

<span data-ttu-id="d5390-969">Prima di chiamare questa funzione, è necessario che la sessione DTLS sia stata configurata con i pacchetti di crittografia e il materiale della chiave appropriati.</span><span class="sxs-lookup"><span data-stu-id="d5390-969">The DTLS session must have been configured with the proper cipher suites and key material before calling this function.</span></span> <span data-ttu-id="d5390-970">È necessario definire **NX_SECURE_ENABLE_DTLS** .</span><span class="sxs-lookup"><span data-stu-id="d5390-970">**NX_SECURE_ENABLE_DTLS** must be defined.</span></span>

<span data-ttu-id="d5390-971">Se la risorsa ' Mantieni fuori ' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà il bootstrap avviato dal server, se non è stato avviato alcun bootstrap dal server dopo questo periodo di tempo in cui verrà eseguito un bootstrap avviato dal client.</span><span class="sxs-lookup"><span data-stu-id="d5390-971">If the ‘Hold Off’ resource is different than zero in the Security Instance associated with this server the session will wait for a Server Initiated Bootstrap, if no bootstrap is initiated by the server after this period of time a Client Initiated Boostrap will be performed.</span></span> 

<span data-ttu-id="d5390-972">Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-972">Any current active session is aborted by this call and replaced by the new Bootstrap Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-973">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-973">Parameters</span></span>

- <span data-ttu-id="d5390-974">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-974">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="d5390-975">**security_id** L'ID dell'istanza di sicurezza del server bootstrap deve essere impostato su **NX_LWM2M_RESERVED_ID** (65535) se nel server bootstrap non è definita alcuna istanza di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5390-975">**security_id** The Security Instance ID of the Bootstrap Server, must be set to **NX_LWM2M_RESERVED_ID** (65535) if the Bootstrap Server has no Security Instance defined.</span></span>
- <span data-ttu-id="d5390-976">**ip_address** Indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="d5390-976">**ip_address** The IP address of the server.</span></span>
- <span data-ttu-id="d5390-977">**porta** Porta UDP del server.</span><span class="sxs-lookup"><span data-stu-id="d5390-977">**port** The UDP port of the server.</span></span>
- <span data-ttu-id="d5390-978">**dtls_session_ptr** Sessione DTLS da utilizzare per la sessione bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-978">**dtls_session_ptr** The DTLS session to use for the Bootstrap session.</span></span>
- <span data-ttu-id="d5390-979">**dtls_local_port** Porta UDP locale utilizzata per la sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="d5390-979">**dtls_local_port** The local UDP port used for the DTLS session.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-980">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-980">Return Values</span></span>

- <span data-ttu-id="d5390-981">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-981">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-982">**NX_LWM2M_CLIENT_ERROR** Errore bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-982">**NX_LWM2M_CLIENT_ERROR** Bootstrap error.</span></span>
- <span data-ttu-id="d5390-983">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d5390-983">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="d5390-984">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-984">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-985">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-985">Allowed From</span></span>

<span data-ttu-id="d5390-986">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-986">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-987">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-987">Example</span></span>

```c
/* Start bootstrap with DTLS.  */
status = nx_lwm2m_client_session_bootstrap_dtls(&lwm2m_client, 0, &ip_address, 5784, &dtls_session);

/* If status is NX_SUCCESS, start bootstrap successfully.  */
```

## <a name="nx_lwm2m_client_session_create"></a><span data-ttu-id="d5390-988">nx_lwm2m_client_session_create</span><span class="sxs-lookup"><span data-stu-id="d5390-988">nx_lwm2m_client_session_create</span></span>

<span data-ttu-id="d5390-989">Crea una sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-989">Creates a LWM2M Client Session.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-990">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-990">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_create(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK state_callback);
```

### <a name="description"></a><span data-ttu-id="d5390-991">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-991">Description</span></span>

<span data-ttu-id="d5390-992">Questo servizio crea una nuova sessione client di LWM2M collegata a un client LWM2M esistente.</span><span class="sxs-lookup"><span data-stu-id="d5390-992">This service creates a new LWM2M Client Session attached to an existing LWM2M Client.</span></span> <span data-ttu-id="d5390-993">La sessione viene usata dal client LWM2M per comunicare con un server bootstrap o un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-993">The session is used by the LWM2M Client to communicate with a Bootstrap Server or a LWM2M Server.</span></span> 

<span data-ttu-id="d5390-994">L'applicazione deve fornire una funzione di callback che verrà chiamata quando viene aggiornato lo stato della sessione.</span><span class="sxs-lookup"><span data-stu-id="d5390-994">The application must provide a callback function that will be called when the state of the session is updated.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-995">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-995">Parameters</span></span>

- <span data-ttu-id="d5390-996">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-996">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="d5390-997">**client_ptr** Puntatore al client LWM2M creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d5390-997">**client_ptr** Pointer to the previously created LWM2M Client.</span></span>
- <span data-ttu-id="d5390-998">**state_callback** Callback dell'applicazione che viene chiamato quando lo stato della sessione viene modificato.</span><span class="sxs-lookup"><span data-stu-id="d5390-998">**state_callback** Application callback that is called when the state of the session has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-999">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-999">Return Values</span></span>

- <span data-ttu-id="d5390-1000">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1000">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-1001">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1001">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1002">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1002">Allowed From</span></span>

<span data-ttu-id="d5390-1003">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1003">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1004">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1004">Example</span></span>

```c
/* Create session.  */
status = nx_lwm2m_client_session_create(&session, &lwm2m_client, session_callback);

/* If status is NX_SUCCESS, a session was successfully created.  */
```

## <a name="nx_lwm2m_client_session_delete"></a><span data-ttu-id="d5390-1005">nx_lwm2m_client_session_delete</span><span class="sxs-lookup"><span data-stu-id="d5390-1005">nx_lwm2m_client_session_delete</span></span>

<span data-ttu-id="d5390-1006">Elimina una sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1006">Deletes a LWM2M Client Session.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-1007">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-1007">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-1008">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-1008">Description</span></span>

<span data-ttu-id="d5390-1009">Questo servizio Elimina una sessione client di LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1009">This service deletes a LWM2M Client Session.</span></span>

<span data-ttu-id="d5390-1010">Quando un client LWM2M viene eliminato chiamando nx_lwm2m_client_delete vengono eliminate anche tutte le sessioni associate al client.</span><span class="sxs-lookup"><span data-stu-id="d5390-1010">When a LWM2M Client is deleted by calling nx_lwm2m_client_delete all sessions attached to the client are also deleted.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-1011">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-1011">Parameters</span></span>

- <span data-ttu-id="d5390-1012">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1012">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-1013">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-1013">Return Values</span></span>

- <span data-ttu-id="d5390-1014">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1014">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-1015">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1015">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1016">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1016">Allowed From</span></span>

<span data-ttu-id="d5390-1017">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1017">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1018">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1018">Example</span></span>

```c
/* Delete session.  */
status = nx_lwm2m_client_session_delete(&session);

/* If status is NX_SUCCESS, a session was successfully deleted.  */
```

## <a name="nx_lwm2m_client_session_deregister"></a><span data-ttu-id="d5390-1019">nx_lwm2m_client_session_deregister</span><span class="sxs-lookup"><span data-stu-id="d5390-1019">nx_lwm2m_client_session_deregister</span></span>

<span data-ttu-id="d5390-1020">Termina una sessione con un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1020">Terminates a session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-1021">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-1021">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-1022">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-1022">Description</span></span>

<span data-ttu-id="d5390-1023">Questo servizio esegue un'operazione di annullamento della registrazione in un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1023">This service performs a ‘De-Register’ operation to a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-1024">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-1024">Parameters</span></span>

- <span data-ttu-id="d5390-1025">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1025">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-1026">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-1026">Return Values</span></span>

- <span data-ttu-id="d5390-1027">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1027">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-1028">**NX_LWM2M_CLIENT_NOT_REGISTERED** Il client non è registrato nel server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1028">**NX_LWM2M_CLIENT_NOT_REGISTERED** The client is not registered to the server.</span></span>
- <span data-ttu-id="d5390-1029">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1029">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1030">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1030">Allowed From</span></span>

<span data-ttu-id="d5390-1031">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1031">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1032">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1032">Example</span></span>

```c
/* De-register session.  */
status = nx_lwm2m_client_session_deregister(&session);

/* If status is NX_SUCCESS, session was successfully de-registered.  */
```

## <a name="nx_lwm2m_client_session_error_get"></a><span data-ttu-id="d5390-1033">nx_lwm2m_client_session_error_get</span><span class="sxs-lookup"><span data-stu-id="d5390-1033">nx_lwm2m_client_session_error_get</span></span>

<span data-ttu-id="d5390-1034">Ottiene l'ultimo errore di una sessione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1034">Gets the last error of a session.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-1035">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-1035">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-1036">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-1036">Description</span></span>

<span data-ttu-id="d5390-1037">Questo servizio restituisce il codice di errore della sessione quando la sessione è in stato di errore.</span><span class="sxs-lookup"><span data-stu-id="d5390-1037">This service returns the error code of the session when the session is in an error state.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-1038">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-1038">Parameters</span></span>

- <span data-ttu-id="d5390-1039">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1039">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-1040">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-1040">Return Values</span></span>

- <span data-ttu-id="d5390-1041">**NX_SUCCESS** La sessione non è in stato di errore.</span><span class="sxs-lookup"><span data-stu-id="d5390-1041">**NX_SUCCESS** The session is not in error state.</span></span>
- <span data-ttu-id="d5390-1042">**NX_LWM2M_CLIENT_ADDRESS_ERROR** Indirizzo server non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1042">**NX_LWM2M_CLIENT_ADDRESS_ERROR** Invalid server address.</span></span>
- <span data-ttu-id="d5390-1043">**NX_LWM2M_ CLIENT_BUFFER_TOO_SMALL** Il payload della richiesta non rientra nel buffer di rete.</span><span class="sxs-lookup"><span data-stu-id="d5390-1043">**NX_LWM2M_ CLIENT_BUFFER_TOO_SMALL** Payload of request doesn’t fit in network buffer.</span></span>
- <span data-ttu-id="d5390-1044">**NX_LWM2M_ CLIENT_DTLS_ERROR** Impossibile stabilire una connessione protetta con il server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1044">**NX_LWM2M_ CLIENT_DTLS_ERROR** Failed to establish secured connection with server.</span></span>
- <span data-ttu-id="d5390-1045">**NX_LWM2M_ CLIENT_ERROR** Errore non specificato.</span><span class="sxs-lookup"><span data-stu-id="d5390-1045">**NX_LWM2M_ CLIENT_ERROR** Unspecified error.</span></span>
- <span data-ttu-id="d5390-1046">**NX_LWM2M_ CLIENT_FORBIDDEN** La registrazione è stata rifiutata dal server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1046">**NX_LWM2M_ CLIENT_FORBIDDEN** Registration refused by server.</span></span>
- <span data-ttu-id="d5390-1047">**NX_LWM2M_ CLIENT_NOT_FOUND** Client non trovato dal server durante l'aggiornamento/annullamento della registrazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1047">**NX_LWM2M_ CLIENT_NOT_FOUND** Client not found by server when updating/deregistering.</span></span>
- <span data-ttu-id="d5390-1048">**NX_LWM2M_ CLIENT_SERVER_INSTANCE_DELETED** L'istanza dell'oggetto server corrispondente alla sessione è stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1048">**NX_LWM2M_ CLIENT_SERVER_INSTANCE_DELETED** The Server Object Instance corresponding to the session has been deleted.</span></span>
- <span data-ttu-id="d5390-1049">**NX_LWM2M_ CLIENT_TIMED_OUT** Nessuna risposta dal server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1049">**NX_LWM2M_ CLIENT_TIMED_OUT** No answer from server.</span></span>
- <span data-ttu-id="d5390-1050">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1050">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1051">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1051">Allowed From</span></span>

<span data-ttu-id="d5390-1052">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1052">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1053">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1053">Example</span></span>

```c
/* Get the error.  */
status = nx_lwm2m_client_session_error_get(&session);
```
## <a name="nx_lwm2m_client_session_register"></a><span data-ttu-id="d5390-1054">nx_lwm2m_client_session_register</span><span class="sxs-lookup"><span data-stu-id="d5390-1054">nx_lwm2m_client_session_register</span></span>

<span data-ttu-id="d5390-1055">Avvia una sessione con un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1055">Starts a session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-1056">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-1056">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID server_id, 
    ULONG ip_address, 
    UINT port);
```


### <a name="description"></a><span data-ttu-id="d5390-1057">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-1057">Description</span></span>

<span data-ttu-id="d5390-1058">Questo servizio esegue un'operazione di registrazione in un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1058">This service performs a ‘Register’ operation to a LWM2M Server.</span></span> <span data-ttu-id="d5390-1059">Il server deve disporre di un'istanza del server corrispondente nell'oggetto server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1059">The server must have a corresponding server instance in the Server Object.</span></span>

<span data-ttu-id="d5390-1060">Se la registrazione ha esito positivo, il client LWM2M elaborerà ulteriori operazioni dal server e invierà periodicamente messaggi di aggiornamento finché il client non viene deregistrato.</span><span class="sxs-lookup"><span data-stu-id="d5390-1060">If the registration is successfully the LWM2M Client will process further operations from the server and will periodically send ‘Update’ messages until the client is de-registered.</span></span>

<span data-ttu-id="d5390-1061">Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1061">Any current active session is aborted by this call and replaced by the new LWM2M Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-1062">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-1062">Parameters</span></span>

- <span data-ttu-id="d5390-1063">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1063">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="d5390-1064">**server_id** ID server breve del server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1064">**server_id** The Short Server ID of the LWM2M Server.</span></span>
- <span data-ttu-id="d5390-1065">**ip_address** Indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1065">**ip_address** The IP address of the server.</span></span>
- <span data-ttu-id="d5390-1066">**porta** Porta UDP del server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1066">**port** The UDP port of the server.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-1067">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-1067">Return Values</span></span>

- <span data-ttu-id="d5390-1068">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1068">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-1069">**NX_LWM2M_CLIENT_ERROR** Errore bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-1069">**NX_LWM2M_CLIENT_ERROR** Bootstrap error.</span></span>
- <span data-ttu-id="d5390-1070">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d5390-1070">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="d5390-1071">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1071">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1072">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1072">Allowed From</span></span>

<span data-ttu-id="d5390-1073">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1073">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1074">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1074">Example</span></span>

```c
/* Start register.  */
status = nx_lwm2m_client_session_register (&lwm2m_client, 123, &ip_address, 5683);

/* If status is NX_SUCCESS, start register successfully.  */
```

## <a name="nx_lwm2m_client_session_register_dtls"></a><span data-ttu-id="d5390-1075">nx_lwm2m_client_session_register_dtls</span><span class="sxs-lookup"><span data-stu-id="d5390-1075">nx_lwm2m_client_session_register_dtls</span></span>

<span data-ttu-id="d5390-1076">Avvia una sessione protetta con un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1076">Starts a secure session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-1077">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-1077">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID server_id, 
    ULONG ip_address, 
    UINT port,
    NX_SECURE_DTLS_SESSION *dtls_session_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-1078">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-1078">Description</span></span>

<span data-ttu-id="d5390-1079">Questo servizio esegue un'operazione di registrazione in un server LWM2M usando una connessione DTLS sicura.</span><span class="sxs-lookup"><span data-stu-id="d5390-1079">This service performs a ‘Register’ operation to a LWM2M Server using a secure DTLS connection.</span></span> <span data-ttu-id="d5390-1080">Il server deve disporre di un'istanza del server corrispondente nell'oggetto server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1080">The server must have a corresponding server instance in the Server Object.</span></span>

<span data-ttu-id="d5390-1081">Prima di chiamare questa funzione, è necessario che la sessione DTLS sia stata configurata con i pacchetti di crittografia e il materiale della chiave appropriati.</span><span class="sxs-lookup"><span data-stu-id="d5390-1081">The DTLS session must have been configured with the proper cipher suites and key material before calling this function.</span></span> <span data-ttu-id="d5390-1082">È necessario definire **NX_SECURE_ENABLE_DTLS** .</span><span class="sxs-lookup"><span data-stu-id="d5390-1082">**NX_SECURE_ENABLE_DTLS** must be defined.</span></span>

<span data-ttu-id="d5390-1083">Se la registrazione ha esito positivo, il client LWM2M elaborerà ulteriori operazioni dal server e invierà periodicamente messaggi di aggiornamento finché il client non viene deregistrato.</span><span class="sxs-lookup"><span data-stu-id="d5390-1083">If the registration is successfully the LWM2M Client will process further operations from the server and will periodically send ‘Update’ messages until the client is de-registered.</span></span>

<span data-ttu-id="d5390-1084">Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1084">Any current active session is aborted by this call and replaced by the new LWM2M Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-1085">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-1085">Parameters</span></span>

- <span data-ttu-id="d5390-1086">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1086">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="d5390-1087">**server_id** ID server breve del server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1087">**server_id** The Short Server ID of the LWM2M Server.</span></span>
- <span data-ttu-id="d5390-1088">**ip_address** Indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1088">**ip_address** The IP address of the server.</span></span>
- <span data-ttu-id="d5390-1089">**porta** Porta UDP del server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1089">**port** The UDP port of the server.</span></span>
- <span data-ttu-id="d5390-1090">**dtls_session_ptr** Sessione DTLS da utilizzare per la sessione LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1090">**dtls_session_ptr** The DTLS session to use for the LWM2M session.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-1091">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-1091">Return Values</span></span>

- <span data-ttu-id="d5390-1092">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1092">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-1093">**NX_LWM2M_CLIENT_ERROR** Errore bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-1093">**NX_LWM2M_CLIENT_ERROR** Bootstrap error.</span></span>
- <span data-ttu-id="d5390-1094">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d5390-1094">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="d5390-1095">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1095">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1096">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1096">Allowed From</span></span>

<span data-ttu-id="d5390-1097">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1097">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1098">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1098">Example</span></span>

```c
/* Start register with DTLS.  */
status = nx_lwm2m_client_session_register_dtls(&lwm2m_client, 123, &ip_address, 5683, &dtls_session);

/* If status is NX_SUCCESS, start register with DTLS successfully.  */
```

## <a name="nx_lwm2m_client_session_register_info_get"></a><span data-ttu-id="d5390-1099">nx_lwm2m_client_session_register_info_get</span><span class="sxs-lookup"><span data-stu-id="d5390-1099">nx_lwm2m_client_session_register_info_get</span></span>

<span data-ttu-id="d5390-1100">Avvia una sessione protetta con un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1100">Starts a secure session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-1101">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-1101">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    UINT security_instance_id, 
    NX_LWM2M_ID *server_id,
    CHAR **server_uri, 
    UINT *server_uri_length, 
    UCHAR *security_mode, 
    UCHAR **pub_key_or_id, 
    UINT *pub_key_or_id_len, 
    UCHAR **server_pub_key, 
    UINT *server_pub_key_len, 
    UCHAR **secret_key, 
    UINT *secret_key_len);
```

### <a name="description"></a><span data-ttu-id="d5390-1102">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-1102">Description</span></span>

<span data-ttu-id="d5390-1103">Una volta stabilita una sessione di comunicazione con un server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="d5390-1103">Once a communication session with a Bootstrap server was established.</span></span> <span data-ttu-id="d5390-1104">L'applicazione può chiamare questa API per ottenere le informazioni sul server e sulla sicurezza per il passaggio di registrazione successivo.</span><span class="sxs-lookup"><span data-stu-id="d5390-1104">Application can call this api to get the server and security information for the next registration step.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-1105">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-1105">Parameters</span></span>

- <span data-ttu-id="d5390-1106">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1106">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="d5390-1107">**security_instance_id** ID istanza di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5390-1107">**security_instance_id** Security instance ID.</span></span>
- <span data-ttu-id="d5390-1108">**server_id** Puntatore all'ID del server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1108">**server_id** Pointer to destination server ID.</span></span>
- <span data-ttu-id="d5390-1109">**server_uri** Puntatore all'URI del server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1109">**server_uri** Pointer to destination server uri.</span></span>
- <span data-ttu-id="d5390-1110">**server_uri_len** Puntatore alla lunghezza dell'URI del server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1110">**server_uri_len** Pointer to destination server uri length.</span></span>
- <span data-ttu-id="d5390-1111">**security_mode** Puntatore alla modalità di sicurezza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1111">**security_mode** Pointer to destination security mode.</span></span>
- <span data-ttu-id="d5390-1112">**pub_key_or_id** Puntatore alla chiave pubblica o all'identità di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1112">**pub_key_or_id** Pointer to destination public key or identity.</span></span>
- <span data-ttu-id="d5390-1113">**pub_key_or_id_len** Puntatore alla chiave pubblica della destinazione o alla lunghezza dell'identità.</span><span class="sxs-lookup"><span data-stu-id="d5390-1113">**pub_key_or_id_len** Pointer to destination public key or identity length.</span></span>
- <span data-ttu-id="d5390-1114">**server_pub_key** Puntatore alla chiave pubblica del server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1114">**server_pub_key** Pointer to destination server public key.</span></span>
- <span data-ttu-id="d5390-1115">**server_pub_key_len** Puntatore alla lunghezza della chiave pubblica del server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1115">**server_pub_key_len** Pointer to destination server public key length.</span></span>
- <span data-ttu-id="d5390-1116">**SECRET_KEY** Puntatore alla chiave privata di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1116">**secret_key** Pointer to destination secret key.</span></span>
- <span data-ttu-id="d5390-1117">**secret_key_len** Puntatore alla lunghezza della chiave privata di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d5390-1117">**secret_key_len** Pointer to destination secret key length.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-1118">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-1118">Return Values</span></span>

- <span data-ttu-id="d5390-1119">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1119">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-1120">**NX_LWM2M_CLIENT_NOT_FOUND** Nessuna istanza di oggetto di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5390-1120">**NX_LWM2M_CLIENT_NOT_FOUND** There is no security Object instance.</span></span>
- <span data-ttu-id="d5390-1121">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1121">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1122">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1122">Allowed From</span></span>

<span data-ttu-id="d5390-1123">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1123">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1124">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1124">Example</span></span>

```c
/* Get the register information.  */
status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_length, &security_mode, &pub_key_or_id, &pub_key_or_id_len, NX_NULL, NX_NULL, &secret_key, &secret_key_len);

/* If status is NX_SUCCESS, the register information was successfully gotten.  */
```

## <a name="nx_lwm2m_client_session_update"></a><span data-ttu-id="d5390-1125">nx_lwm2m_client_session_update</span><span class="sxs-lookup"><span data-stu-id="d5390-1125">nx_lwm2m_client_session_update</span></span>

<span data-ttu-id="d5390-1126">Aggiorna una sessione con un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1126">Updates a session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-1127">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-1127">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-1128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-1128">Description</span></span>

<span data-ttu-id="d5390-1129">Questo servizio esegue un'operazione di aggiornamento in un server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1129">This service performs an ‘Update’ operation to a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-1130">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-1130">Parameters</span></span>

- <span data-ttu-id="d5390-1131">**session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1131">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-1132">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-1132">Return Values</span></span>

- <span data-ttu-id="d5390-1133">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1133">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-1134">**NX_LWM2M_CLIENT_NOT_REGISTERED** Il client non è registrato nel server.</span><span class="sxs-lookup"><span data-stu-id="d5390-1134">**NX_LWM2M_CLIENT_NOT_REGISTERED** The client is not registered to the server.</span></span>
- <span data-ttu-id="d5390-1135">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1135">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1136">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1136">Allowed From</span></span>

<span data-ttu-id="d5390-1137">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1137">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1138">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1138">Example</span></span>

```c
/* Update a session.  */
status = nx_lwm2m_client_session_update(&session);

/* If status is NX_SUCCESS, a session was successfully updated.  */
```

## <a name="nx_lwm2m_client_unlock"></a><span data-ttu-id="d5390-1139">nx_lwm2m_client_unlock</span><span class="sxs-lookup"><span data-stu-id="d5390-1139">nx_lwm2m_client_unlock</span></span>

<span data-ttu-id="d5390-1140">Sblocca un client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1140">Unlocks a LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="d5390-1141">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d5390-1141">Prototype</span></span>

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="d5390-1142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5390-1142">Description</span></span>

<span data-ttu-id="d5390-1143">Questo servizio Sblocca il client LWM2M precedentemente bloccato da una chiamata a ***nx_lwm2m_client_unlock***.</span><span class="sxs-lookup"><span data-stu-id="d5390-1143">This service unlocks the LWM2M Client previously locked by a call to ***nx_lwm2m_client_unlock***.</span></span>

### <a name="parameters"></a><span data-ttu-id="d5390-1144">Parametri</span><span class="sxs-lookup"><span data-stu-id="d5390-1144">Parameters</span></span>

- <span data-ttu-id="d5390-1145">**client_ptr** Puntatore al blocco di controllo client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="d5390-1145">**client_ptr** Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d5390-1146">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d5390-1146">Return Values</span></span>

- <span data-ttu-id="d5390-1147">**NX_SUCCESS** Operazione completata.</span><span class="sxs-lookup"><span data-stu-id="d5390-1147">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="d5390-1148">**NX_PTR_ERROR** Puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d5390-1148">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d5390-1149">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d5390-1149">Allowed From</span></span>

<span data-ttu-id="d5390-1150">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="d5390-1150">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="d5390-1151">Esempio</span><span class="sxs-lookup"><span data-stu-id="d5390-1151">Example</span></span>

```c
/* Unlock lwm2m client.  */
status = nx_lwm2m_client_unlock(&lwm2m_client);

/* If status is NX_SUCCESS, unlock lwm2m client successfully.  */
```