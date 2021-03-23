---
title: Capitolo 4-Descrizione dei servizi per dispositivi USBX
description: Informazioni sui servizi del dispositivo USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d4aea7470ba2d9075296164b9d1fb61db4f88523
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824041"
---
# <a name="description-of-usbx-device-services"></a><span data-ttu-id="2d050-103">Descrizione dei servizi per dispositivi USBX</span><span class="sxs-lookup"><span data-stu-id="2d050-103">Description of USBX Device Services</span></span>

### <a name="ux_device_stack_alternate_setting_get"></a><span data-ttu-id="2d050-104">ux_device_stack_alternate_setting_get</span><span class="sxs-lookup"><span data-stu-id="2d050-104">ux_device_stack_alternate_setting_get</span></span>

<span data-ttu-id="2d050-105">Ottenere l'impostazione alternativa corrente per un valore di interfaccia</span><span class="sxs-lookup"><span data-stu-id="2d050-105">Get current alternate setting for an interface value</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-106">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-106">Prototype</span></span>

```c
UINT ux_device_stack_alternate_setting_get(ULONG interface_value);
```

### <a name="description"></a><span data-ttu-id="2d050-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-107">Description</span></span>

<span data-ttu-id="2d050-108">Questa funzione viene usata dall'host USB per ottenere l'impostazione alternativa corrente per un valore di interfaccia specifico.</span><span class="sxs-lookup"><span data-stu-id="2d050-108">This function is used by the USB host to obtain the current alternate setting for a specific interface value.</span></span> <span data-ttu-id="2d050-109">Viene chiamato dal driver del controller quando viene ricevuta una richiesta **GET_INTERFACE** .</span><span class="sxs-lookup"><span data-stu-id="2d050-109">It is called by the controller driver when a **GET_INTERFACE** request is received.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-110">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-110">Input Parameter</span></span>

- <span data-ttu-id="2d050-111">**Interface_value** Valore dell'interfaccia per cui viene eseguita una query sull'impostazione alternativa corrente</span><span class="sxs-lookup"><span data-stu-id="2d050-111">**Interface_value** Interface value for which the current alternate setting is queried</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-112">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-112">Return Values</span></span>

- <span data-ttu-id="2d050-113">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="2d050-113">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="2d050-114">Valore dell'interfaccia **UX_ERROR** (0Xff) errato.</span><span class="sxs-lookup"><span data-stu-id="2d050-114">**UX_ERROR** (0xFF) Wrong interface value.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-115">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-115">Example</span></span>

```c
ULONG interface_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_alternate_setting_set"></a><span data-ttu-id="2d050-116">ux_device_stack_alternate_setting_set</span><span class="sxs-lookup"><span data-stu-id="2d050-116">ux_device_stack_alternate_setting_set</span></span>

<span data-ttu-id="2d050-117">Imposta l'impostazione alternativa corrente per un valore di interfaccia</span><span class="sxs-lookup"><span data-stu-id="2d050-117">Set current alternate setting for an interface value</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-118">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-118">Prototype</span></span>

```c
UINT ux_device_stack_alternate_setting_set(
    ULONG interface_value, 
    ULONG alternate_setting_value);
```

### <a name="description"></a><span data-ttu-id="2d050-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-119">Description</span></span>

<span data-ttu-id="2d050-120">Questa funzione viene usata dall'host USB per impostare l'impostazione alternativa corrente per un valore di interfaccia specifico.</span><span class="sxs-lookup"><span data-stu-id="2d050-120">This function is used by the USB host to set the current alternate setting for a specific interface value.</span></span> <span data-ttu-id="2d050-121">Viene chiamato dal driver del controller quando viene ricevuta una richiesta **SET_INTERFACE** .</span><span class="sxs-lookup"><span data-stu-id="2d050-121">It is called by the controller driver when a **SET_INTERFACE** request is received.</span></span> <span data-ttu-id="2d050-122">Al termine dell' **SET_INTERFACE** , i valori delle impostazioni alternative vengono applicati alla classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-122">When the **SET_INTERFACE** is completed, the values of the alternate settings are applied to the class.</span></span>

<span data-ttu-id="2d050-123">Lo stack del dispositivo emetterà un **UX_SLAVE_CLASS_COMMAND_CHANGE** alla classe proprietaria di questa interfaccia per riflettere la modifica dell'impostazione alternativa.</span><span class="sxs-lookup"><span data-stu-id="2d050-123">The device stack will issue a **UX_SLAVE_CLASS_COMMAND_CHANGE** to the class that owns this interface to reflect the change of alternate setting.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-124">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-124">Parameters</span></span>

- <span data-ttu-id="2d050-125">**interface_value**: valore dell'interfaccia per cui è impostata l'impostazione alternativa corrente.</span><span class="sxs-lookup"><span data-stu-id="2d050-125">**interface_value**: Interface value for which the current alternate setting is set.</span></span>
- <span data-ttu-id="2d050-126">**alternate_setting_value**: nuovo valore dell'impostazione alternativa.</span><span class="sxs-lookup"><span data-stu-id="2d050-126">**alternate_setting_value**: The new alternate setting value.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-127">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-127">Return Values</span></span>

- <span data-ttu-id="2d050-128">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="2d050-128">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="2d050-129">**UX_INTERFACE_HANDLE_UNKNOWN** (0X52) non è collegata alcuna interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-129">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) No interface attached.</span></span>
- <span data-ttu-id="2d050-130">Il dispositivo **UX_FUNCTION_NOT_SUPPORTED** (0x54) non è configurato.</span><span class="sxs-lookup"><span data-stu-id="2d050-130">**UX_FUNCTION_NOT_SUPPORTED** (0x54) Device is not configured.</span></span>
- <span data-ttu-id="2d050-131">Valore dell'interfaccia **UX_ERROR** (0Xff) errato.</span><span class="sxs-lookup"><span data-stu-id="2d050-131">**UX_ERROR** (0xFF) Wrong interface value.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-132">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-132">Example</span></span>

```c
ULONG interface_value;

ULONG alternate_setting_value;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_set(interface_value, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_class_register"></a><span data-ttu-id="2d050-133">ux_device_stack_class_register</span><span class="sxs-lookup"><span data-stu-id="2d050-133">ux_device_stack_class_register</span></span>

<span data-ttu-id="2d050-134">Registrare una nuova classe dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="2d050-134">Register a new USB device class</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-135">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-135">Prototype</span></span>

```c
UINT ux_device_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT *),
    ULONG configuration_number, 
    ULONG interface_number,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="2d050-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-136">Description</span></span>

<span data-ttu-id="2d050-137">Questa funzione viene usata dall'applicazione per registrare una nuova classe di dispositivo USB.</span><span class="sxs-lookup"><span data-stu-id="2d050-137">This function is used by the application to register a new USB device class.</span></span> <span data-ttu-id="2d050-138">Questa registrazione avvia un contenitore di classi e non un'istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-138">This registration starts a class container and not an instance of the class.</span></span> <span data-ttu-id="2d050-139">Una classe deve avere un thread attivo ed essere collegata a un'interfaccia specifica.</span><span class="sxs-lookup"><span data-stu-id="2d050-139">A class should have an active thread and be attached to a specific interface.</span></span>

<span data-ttu-id="2d050-140">Per alcune classi è previsto un elenco di parametri o parametri.</span><span class="sxs-lookup"><span data-stu-id="2d050-140">Some classes expect a parameter or parameter list.</span></span> <span data-ttu-id="2d050-141">Ad esempio, la classe di archiviazione del dispositivo dovrebbe prevedere la geometria del dispositivo di archiviazione che sta provando a emulare.</span><span class="sxs-lookup"><span data-stu-id="2d050-141">For instance, the device storage class would expect the geometry of the storage device it is trying to emulate.</span></span> <span data-ttu-id="2d050-142">Il campo del parametro dipende pertanto dal requisito della classe e può essere un valore o un puntatore a una struttura compilata con i valori della classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-142">The parameter field is therefore dependent on the class requirement and can be a value or a pointer to a structure filled with the class values.</span></span>

> [!NOTE]
> <span data-ttu-id="2d050-143">La stringa C di class_name deve essere con terminazione NULL e la lunghezza (senza il carattere di terminazione NULL) non deve essere maggiore di **UX_MAX_CLASS_NAME_LENGTH**.</span><span class="sxs-lookup"><span data-stu-id="2d050-143">The C string of class_name must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than **UX_MAX_CLASS_NAME_LENGTH**.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-144">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-144">Parameters</span></span>

- <span data-ttu-id="2d050-145">**class_name** Nome classe</span><span class="sxs-lookup"><span data-stu-id="2d050-145">**class_name** Class Name</span></span>
- <span data-ttu-id="2d050-146">**class_entry_function** Funzione entry della classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-146">**class_entry_function** The entry function of the class.</span></span>
- <span data-ttu-id="2d050-147">**configuration_number** Numero di configurazione a cui è collegata questa classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-147">**configuration_number** The configuration number this class is attached to.</span></span>
- <span data-ttu-id="2d050-148">**interface_number** Numero di interfaccia a cui è collegata questa classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-148">**interface_number** The interface number this class is attached to.</span></span>
- <span data-ttu-id="2d050-149">**parametro** di Puntatore a un elenco di parametri specifici della classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-149">**parameter** A pointer to a class specific parameter list.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-150">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-150">Return Values</span></span>

- <span data-ttu-id="2d050-151">**UX_SUCCESS** (0x00) la classe è stata registrata</span><span class="sxs-lookup"><span data-stu-id="2d050-151">**UX_SUCCESS** (0x00) The class was registered</span></span>
- <span data-ttu-id="2d050-152">**UX_MEMORY_INSUFFICIENT** (0X12) nessuna voce lasciata nella tabella della classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-152">**UX_MEMORY_INSUFFICIENT** (0x12) No entries left in class table.</span></span>
- <span data-ttu-id="2d050-153">**UX_THREAD_ERROR** (0x16) non è in grado di creare un thread di classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-153">**UX_THREAD_ERROR** (0x16) Cannot create a class thread.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-154">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-154">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */

/* Initialize the device storage class. The class is connected with interface 1 */
status = ux_device_stack_class_register(_ux_system_slave_class_storage_name ux_device_class_storage_entry,
    1, 1, (VOID *)&parameter);
```

### <a name="ux_device_stack_class_unregister"></a><span data-ttu-id="2d050-155">ux_device_stack_class_unregister</span><span class="sxs-lookup"><span data-stu-id="2d050-155">ux_device_stack_class_unregister</span></span>

<span data-ttu-id="2d050-156">Annulla la registrazione di una classe dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="2d050-156">Unregister a USB device class</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-157">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-157">Prototype</span></span>

```c
UINT ux_device_stack_class_unregister(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT*));
```

### <a name="description"></a><span data-ttu-id="2d050-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-158">Description</span></span>

<span data-ttu-id="2d050-159">Questa funzione viene usata dall'applicazione per annullare la registrazione di una classe dispositivo USB.</span><span class="sxs-lookup"><span data-stu-id="2d050-159">This function is used by the application to unregister a USB device class.</span></span>

> [!NOTE]
> <span data-ttu-id="2d050-160">La stringa C di class_name deve essere con terminazione NULL e la lunghezza (senza il carattere di terminazione NULL) non deve essere maggiore di **UX_MAX_CLASS_NAME_LENGTH**.</span><span class="sxs-lookup"><span data-stu-id="2d050-160">The C string of class_name must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than **UX_MAX_CLASS_NAME_LENGTH**.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-161">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-161">Parameters</span></span>

- <span data-ttu-id="2d050-162">**class_name**: nome della classe</span><span class="sxs-lookup"><span data-stu-id="2d050-162">**class_name**: Class Name</span></span>
- <span data-ttu-id="2d050-163">**class_entry_function**: la funzione entry della classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-163">**class_entry_function**: The entry function of the class.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-164">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-164">Return Values</span></span>

- <span data-ttu-id="2d050-165">**UX_SUCCESS** (0x00) per cui è stata annullata la registrazione della classe.</span><span class="sxs-lookup"><span data-stu-id="2d050-165">**UX_SUCCESS** (0x00) The class was unregistered.</span></span>
- <span data-ttu-id="2d050-166">**UX_NO_CLASS_MATCH** (0x57) la classe non è registrata.</span><span class="sxs-lookup"><span data-stu-id="2d050-166">**UX_NO_CLASS_MATCH** (0x57) The class isn't registered.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-167">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-167">Example</span></span>

```c
/* The following example illustrates this service. */

/* Unitialize the device storage class. */
status = ux_device_stack_class_unregister(_ux_system_slave_class_storage_name, ux_device_class_storage_entry);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_get"></a><span data-ttu-id="2d050-168">ux_device_stack_configuration_get</span><span class="sxs-lookup"><span data-stu-id="2d050-168">ux_device_stack_configuration_get</span></span>

<span data-ttu-id="2d050-169">Ottenere la configurazione corrente</span><span class="sxs-lookup"><span data-stu-id="2d050-169">Get the current configuration</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-170">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-170">Prototype</span></span>

```c
UINT ux_device_stack_configuration_get(VOID);
```

### <a name="description"></a><span data-ttu-id="2d050-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-171">Description</span></span>

<span data-ttu-id="2d050-172">Questa funzione viene usata dall'host per ottenere la configurazione corrente in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2d050-172">This function is used by the host to obtain the current configuration running in the device.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-173">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-173">Input Parameter</span></span>

<span data-ttu-id="2d050-174">nessuno</span><span class="sxs-lookup"><span data-stu-id="2d050-174">None</span></span>

### <a name="return-value"></a><span data-ttu-id="2d050-175">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2d050-175">Return Value</span></span>

- <span data-ttu-id="2d050-176">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="2d050-176">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-177">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-177">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_get();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_set"></a><span data-ttu-id="2d050-178">ux_device_stack_configuration_set</span><span class="sxs-lookup"><span data-stu-id="2d050-178">ux_device_stack_configuration_set</span></span>

<span data-ttu-id="2d050-179">Imposta la configurazione corrente</span><span class="sxs-lookup"><span data-stu-id="2d050-179">Set the current configuration</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-180">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-180">Prototype</span></span>

```c
UINT ux_device_stack_configuration_set(ULONG configuration_value);
```

### <a name="description"></a><span data-ttu-id="2d050-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-181">Description</span></span>

<span data-ttu-id="2d050-182">Questa funzione viene usata dall'host per impostare la configurazione corrente in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2d050-182">This function is used by the host to set the current configuration running in the device.</span></span> <span data-ttu-id="2d050-183">Al momento della ricezione di questo comando, lo stack di dispositivi USB attiverà l'impostazione alternativa 0 di ogni interfaccia connessa a questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="2d050-183">Upon reception of this command, the USB device stack will activate the alternate setting 0 of each interface connected to this configuration.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-184">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-184">Input Parameter</span></span>

- <span data-ttu-id="2d050-185">**configuration_value** Valore di configurazione selezionato dall'host.</span><span class="sxs-lookup"><span data-stu-id="2d050-185">**configuration_value** The configuration value selected by the host.</span></span>

### <a name="return-value"></a><span data-ttu-id="2d050-186">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2d050-186">Return Value</span></span>

- <span data-ttu-id="2d050-187">**UX_SUCCESS** (0x00) la configurazione è stata impostata correttamente.</span><span class="sxs-lookup"><span data-stu-id="2d050-187">**UX_SUCCESS** (0x00) The configuration was successfully set.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-188">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-188">Example</span></span>

```c
ULONG configuration_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_set(configuration_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_descriptor_send"></a><span data-ttu-id="2d050-189">ux_device_stack_descriptor_send</span><span class="sxs-lookup"><span data-stu-id="2d050-189">ux_device_stack_descriptor_send</span></span>

<span data-ttu-id="2d050-190">Invia un descrittore all'host</span><span class="sxs-lookup"><span data-stu-id="2d050-190">Send a descriptor to the host</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-191">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-191">Prototype</span></span>

```c
UINT ux_device_stack_descriptor_send(
    ULONG descriptor_type, 
    ULONG request_index, 
    ULONG host_length);
```

### <a name="description"></a><span data-ttu-id="2d050-192">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-192">Description</span></span>

<span data-ttu-id="2d050-193">Questa funzione viene utilizzata dal lato dispositivo per restituire un descrittore all'host.</span><span class="sxs-lookup"><span data-stu-id="2d050-193">This function is used by the device side to return a descriptor to the host.</span></span> <span data-ttu-id="2d050-194">Questo descrittore può essere un descrittore di dispositivo, un descrittore di configurazione o una stringa.</span><span class="sxs-lookup"><span data-stu-id="2d050-194">This descriptor can be a device descriptor, a configuration descriptor or a string descriptor.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-195">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-195">Parameters</span></span>

- <span data-ttu-id="2d050-196">**descriptor_type**: tipo del descrittore.</span><span class="sxs-lookup"><span data-stu-id="2d050-196">**descriptor_type**: The type of the descriptor.</span></span> <span data-ttu-id="2d050-197">Deve essere uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="2d050-197">Must be one of the following values.</span></span>
  - <span data-ttu-id="2d050-198">**UX_DEVICE_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="2d050-198">**UX_DEVICE_DESCRIPTOR_ITEM**</span></span>
  - <span data-ttu-id="2d050-199">**UX_CONFIGURATION_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="2d050-199">**UX_CONFIGURATION_DESCRIPTOR_ITEM**</span></span>
  - <span data-ttu-id="2d050-200">**UX_STRING_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="2d050-200">**UX_STRING_DESCRIPTOR_ITEM**</span></span>
  - <span data-ttu-id="2d050-201">**UX_DEVICE_QUALIFIER_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="2d050-201">**UX_DEVICE_QUALIFIER_DESCRIPTOR_ITEM**</span></span>
  - <span data-ttu-id="2d050-202">**UX_OTHER_SPEED_DESCRIPTOR_ITEM**</span><span class="sxs-lookup"><span data-stu-id="2d050-202">**UX_OTHER_SPEED_DESCRIPTOR_ITEM**</span></span>
- <span data-ttu-id="2d050-203">**request_index**: Indice del descrittore.</span><span class="sxs-lookup"><span data-stu-id="2d050-203">**request_index**: The index of the descriptor.</span></span>
- <span data-ttu-id="2d050-204">**host_length**: lunghezza richiesta dall'host.</span><span class="sxs-lookup"><span data-stu-id="2d050-204">**host_length**: The length required by the host.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-205">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-205">Return Values</span></span>

- <span data-ttu-id="2d050-206">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="2d050-206">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="2d050-207">**UX_ERROR** (0Xff) il trasferimento non è stato completato.</span><span class="sxs-lookup"><span data-stu-id="2d050-207">**UX_ERROR** (0xFF) The transfer was not completed.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-208">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-208">Example</span></span>

```c
ULONG descriptor_type;
ULONG request_index;
ULONG host_length;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_descriptor_send(descriptor_type, request_index, host_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_disconnect"></a><span data-ttu-id="2d050-209">ux_device_stack_disconnect</span><span class="sxs-lookup"><span data-stu-id="2d050-209">ux_device_stack_disconnect</span></span>

<span data-ttu-id="2d050-210">Scollega stack di dispositivi</span><span class="sxs-lookup"><span data-stu-id="2d050-210">Disconnect device stack</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-211">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-211">Prototype</span></span>

```c
UINT ux_device_stack_disconnect(VOID);
```

### <a name="description"></a><span data-ttu-id="2d050-212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-212">Description</span></span>

<span data-ttu-id="2d050-213">VBUS Manager chiama questa funzione quando è presente una disconnessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2d050-213">The VBUS manager calls this function when there is a device disconnection.</span></span> <span data-ttu-id="2d050-214">Lo stack del dispositivo informa tutte le classi registrate in questo dispositivo e successivamente rilascerà tutte le risorse del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2d050-214">The device stack will inform all classes registered to this device and will thereafter release all the device resources.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-215">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-215">Input Parameter</span></span>

<span data-ttu-id="2d050-216">nessuno</span><span class="sxs-lookup"><span data-stu-id="2d050-216">None</span></span>

### <a name="return-value"></a><span data-ttu-id="2d050-217">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2d050-217">Return Value</span></span>

- <span data-ttu-id="2d050-218">**UX_SUCCESS** (0x00) il dispositivo è stato disconnesso.</span><span class="sxs-lookup"><span data-stu-id="2d050-218">**UX_SUCCESS** (0x00) The device was disconnected.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-219">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-219">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_disconnect();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_endpoint_stall"></a><span data-ttu-id="2d050-220">ux_device_stack_endpoint_stall</span><span class="sxs-lookup"><span data-stu-id="2d050-220">ux_device_stack_endpoint_stall</span></span>

<span data-ttu-id="2d050-221">Condizione di blocco endpoint richiesta</span><span class="sxs-lookup"><span data-stu-id="2d050-221">Request endpoint Stall condition</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-222">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-222">Prototype</span></span>

```c
UINT ux_device_stack_endpoint_stall(UX_SLAVE_ENDPOINT*endpoint);
```

### <a name="description"></a><span data-ttu-id="2d050-223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-223">Description</span></span>

<span data-ttu-id="2d050-224">Questa funzione viene chiamata dalla classe dispositivo USB quando un endpoint deve restituire una condizione di stallo dell'host.</span><span class="sxs-lookup"><span data-stu-id="2d050-224">This function is called by the USB device class when an endpoint should return a Stall condition to the host.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-225">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-225">Input Parameter</span></span>

- <span data-ttu-id="2d050-226">**endpoint** di Endpoint in cui viene richiesta la condizione di blocco.</span><span class="sxs-lookup"><span data-stu-id="2d050-226">**endpoint** The endpoint on which the Stall condition is requested.</span></span>

### <a name="return-value"></a><span data-ttu-id="2d050-227">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2d050-227">Return Value</span></span>

- <span data-ttu-id="2d050-228">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-228">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="2d050-229">**UX_ERROR** (0Xff) il dispositivo è in uno stato non valido.</span><span class="sxs-lookup"><span data-stu-id="2d050-229">**UX_ERROR** (0xFF) The device is in an invalid state.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-230">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-230">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_endpoint_stall(endpoint);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_host_wakeup"></a><span data-ttu-id="2d050-231">ux_device_stack_host_wakeup</span><span class="sxs-lookup"><span data-stu-id="2d050-231">ux_device_stack_host_wakeup</span></span>

<span data-ttu-id="2d050-232">Riattivare l'host</span><span class="sxs-lookup"><span data-stu-id="2d050-232">Wake up the host</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-233">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-233">Prototype</span></span>

```c
UINT ux_device_stack_host_wakeup(VOID);
```

### <a name="description"></a><span data-ttu-id="2d050-234">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-234">Description</span></span>

<span data-ttu-id="2d050-235">Questa funzione viene chiamata quando il dispositivo desidera riattivare l'host.</span><span class="sxs-lookup"><span data-stu-id="2d050-235">This function is called when the device wants to wake up the host.</span></span> <span data-ttu-id="2d050-236">Questo comando è valido solo quando il dispositivo è in modalità di sospensione.</span><span class="sxs-lookup"><span data-stu-id="2d050-236">This command is only valid when the device is in suspend mode.</span></span> <span data-ttu-id="2d050-237">Spetta all'applicazione del dispositivo decidere quando vuole riattivare l'host USB.</span><span class="sxs-lookup"><span data-stu-id="2d050-237">It is up to the device application to decide when it wants to wake up the USB host.</span></span> <span data-ttu-id="2d050-238">Ad esempio, un modem USB può riattivare un host quando rileva un segnale ANULARe sulla linea telefonica.</span><span class="sxs-lookup"><span data-stu-id="2d050-238">For instance, a USB modem can wake up a host when it detects a RING signal on the telephone line.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-239">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-239">Input Parameter</span></span>

<span data-ttu-id="2d050-240">nessuno</span><span class="sxs-lookup"><span data-stu-id="2d050-240">None</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-241">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-241">Return values</span></span>

- <span data-ttu-id="2d050-242">**UX_SUCCESS** (0x00) la chiamata ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="2d050-242">**UX_SUCCESS** (0x00) The call was successful.</span></span>
- <span data-ttu-id="2d050-243">**UX_FUNCTION_NOT_SUPPORTED** (0X54) la chiamata non è riuscita (il dispositivo probabilmente non è in modalità di sospensione).</span><span class="sxs-lookup"><span data-stu-id="2d050-243">**UX_FUNCTION_NOT_SUPPORTED** (0x54) The call failed (the device was probably not in the suspended mode).</span></span>

### <a name="example"></a><span data-ttu-id="2d050-244">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-244">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_host_wakeup();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_initialize"></a><span data-ttu-id="2d050-245">ux_device_stack_initialize</span><span class="sxs-lookup"><span data-stu-id="2d050-245">ux_device_stack_initialize</span></span>

<span data-ttu-id="2d050-246">Inizializza stack dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="2d050-246">Initialize USB device stack</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-247">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-247">Prototype</span></span>

```c
UINT ux_device_stack_initialize(
    UCHAR *device_framework_high_speed,
    ULONG device_framework_length_high_speed,
    UCHAR *device_framework_full_speed,
    ULONG device_framework_length_full_speed,
    UCHAR *string_framework,
    ULONG string_framework_length,
    UCHAR *language_id_framework,
    ULONG language_id_framework_length),
    UINT (*ux_system_slave_change_function)(ULONG)));
```

### <a name="description"></a><span data-ttu-id="2d050-248">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-248">Description</span></span>

<span data-ttu-id="2d050-249">Questa funzione viene chiamata dall'applicazione per inizializzare lo stack del dispositivo USB.</span><span class="sxs-lookup"><span data-stu-id="2d050-249">This function is called by the application to initialize the USB device stack.</span></span> <span data-ttu-id="2d050-250">Non inizializza alcuna classe né controller.</span><span class="sxs-lookup"><span data-stu-id="2d050-250">It does not initialize any classes or any controllers.</span></span> <span data-ttu-id="2d050-251">Questa operazione deve essere eseguita con chiamate di funzione separate.</span><span class="sxs-lookup"><span data-stu-id="2d050-251">This should be done with separate function calls.</span></span> <span data-ttu-id="2d050-252">Questa chiamata fornisce principalmente lo stack con il Framework del dispositivo per la funzione USB.</span><span class="sxs-lookup"><span data-stu-id="2d050-252">This call mainly provides the stack with the device framework for the USB function.</span></span> <span data-ttu-id="2d050-253">Supporta la velocità elevata e completa, con la possibilità di avere un Framework del dispositivo completamente separato per ogni velocità.</span><span class="sxs-lookup"><span data-stu-id="2d050-253">It supports both high and full speeds with the possibility to have completely separate device framework for each speed.</span></span> <span data-ttu-id="2d050-254">Sono supportati il Framework di stringhe e più lingue.</span><span class="sxs-lookup"><span data-stu-id="2d050-254">String framework and multiple languages are supported.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-255">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-255">Parameters</span></span>

- <span data-ttu-id="2d050-256">**device_framework_high_speed**: puntatore al Framework ad alta velocità.</span><span class="sxs-lookup"><span data-stu-id="2d050-256">**device_framework_high_speed**: Pointer to the high speed framework.</span></span>
- <span data-ttu-id="2d050-257">**device_framework_length_high_speed**: lunghezza del Framework ad alta velocità.</span><span class="sxs-lookup"><span data-stu-id="2d050-257">**device_framework_length_high_speed**: Length of the high speed framework.</span></span>
- <span data-ttu-id="2d050-258">**device_framework_full_speed**: puntatore al Framework a velocità intera.</span><span class="sxs-lookup"><span data-stu-id="2d050-258">**device_framework_full_speed**: Pointer to the full speed framework.</span></span>
- <span data-ttu-id="2d050-259">**device_framework_length_full_speed**: lunghezza del Framework a velocità intera.</span><span class="sxs-lookup"><span data-stu-id="2d050-259">**device_framework_length_full_speed**: Length of the full speed framework.</span></span>
- <span data-ttu-id="2d050-260">**string_framework**: puntatore a Framework di stringa.</span><span class="sxs-lookup"><span data-stu-id="2d050-260">**string_framework**: Pointer to string framework.</span></span>
- <span data-ttu-id="2d050-261">**string_framework_length**: lunghezza del Framework di stringa.</span><span class="sxs-lookup"><span data-stu-id="2d050-261">**string_framework_length**: Length of string framework.</span></span>
- <span data-ttu-id="2d050-262">**language_id_framework**: puntatore al Framework del linguaggio di stringa.</span><span class="sxs-lookup"><span data-stu-id="2d050-262">**language_id_framework**: Pointer to string language framework.</span></span>
- <span data-ttu-id="2d050-263">**language_id_framework_length**: lunghezza del Framework del linguaggio di stringa.</span><span class="sxs-lookup"><span data-stu-id="2d050-263">**language_id_framework_length**: Length of the string language framework.</span></span>
- <span data-ttu-id="2d050-264">**ux_system_slave_change_function**: funzione da chiamare quando lo stato del dispositivo cambia.</span><span class="sxs-lookup"><span data-stu-id="2d050-264">**ux_system_slave_change_function**: Function to be called when the device state changes.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-265">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-265">Return Values</span></span>

- <span data-ttu-id="2d050-266">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-266">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="2d050-267">**UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente per inizializzare lo stack.</span><span class="sxs-lookup"><span data-stu-id="2d050-267">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory to initialize the stack.</span></span>
- <span data-ttu-id="2d050-268">**UX_DESCRIPTOR_CORRUPTED** (0X42) il descrittore non è valido.</span><span class="sxs-lookup"><span data-stu-id="2d050-268">**UX_DESCRIPTOR_CORRUPTED** (0x42) The descriptor is invalid.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-269">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-269">Example</span></span>

```c
/* Example of a device framework */

#define DEVICE_FRAMEWORK_LENGTH_FULL_SPEED 50

UCHAR device_framework_full_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x08,
    0xec, 0x08, 0x10, 0x00, 0x00, 0x00, 0x00, 0x00,
    0x00, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50,
    0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x40, 0x00, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x40, 0x00, 0x00
};

#define DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED 60

UCHAR device_framework_high_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40,
    0x0a, 0x07, 0x25, 0x40, 0x01, 0x00, 0x01, 0x02,
    0x03, 0x01,

    /* Device qualifier descriptor */
    0x0a, 0x06, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40,
    0x01, 0x00,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50,
    0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x00, 0x02, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x00, 0x02, 0x00
};

/* String Device Framework:
    Byte 0 and 1: Word containing the language ID: 0x0904 for US
    Byte 2 : Byte containing the index of the descriptor
    Byte 3 : Byte containing the length of the descriptor string */

#define STRING_FRAMEWORK_LENGTH 38 UCHAR string_framework[] = {
    /* Manufacturer string descriptor: Index 1 */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72,0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,

    /* Product string descriptor: Index 2 */
    0x09, 0x04, 0x02, 0x0c,
    0x4D, 0x4C, 0x36, 0x39, 0x36, 0x35, 0x30, 0x30,
    0x20, 0x53, 0x44, 0x4B,

    /* Serial Number string descriptor: Index 3 */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31
};

/* Multiple languages are supported on the device, to add a language besides English, 
  the Unicode language code must be appended to the language_id_framework array 
  and the length adjusted accordingly. */

#define LANGUAGE_ID_FRAMEWORK_LENGTH 2

UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

<span data-ttu-id="2d050-270">L'applicazione può richiedere una chiamata quando il controller ne modifica lo stato.</span><span class="sxs-lookup"><span data-stu-id="2d050-270">The application can request a call back when the controller changes its state.</span></span> <span data-ttu-id="2d050-271">I due stati principali per il controller sono:</span><span class="sxs-lookup"><span data-stu-id="2d050-271">The two main states for the controller are:</span></span>

- <span data-ttu-id="2d050-272">**UX_DEVICE_SUSPENDED**</span><span class="sxs-lookup"><span data-stu-id="2d050-272">**UX_DEVICE_SUSPENDED**</span></span>
- <span data-ttu-id="2d050-273">**UX_DEVICE_RESUMED**</span><span class="sxs-lookup"><span data-stu-id="2d050-273">**UX_DEVICE_RESUMED**</span></span>

<span data-ttu-id="2d050-274">Se l'applicazione non necessita di segnali Suspend/Resume, fornisce una funzione UX_NULL.</span><span class="sxs-lookup"><span data-stu-id="2d050-274">If the application does not need Suspend/Resume signals, it would supply a UX_NULL function.</span></span>

```c
UINT status;

/* The code below is required for installing the device portion of USBX. 
    There is no call back for device status change in this example. */
status = ux_device_stack_initialize(&device_framework_high_speed,
    DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED, &device_framework_full_speed,
    DEVICE_FRAMEWORK_LENGTH_FULL_SPEED, &string_framework,
    STRING_FRAMEWORK_LENGTH, &language_id_framework,
    LANGUAGE_ID_FRAMEWORK_LENGTH, UX_NULL);

/* If status equals UX_SUCCESS, initialization was successful. */
```

### <a name="ux_device_stack_interface_delete"></a><span data-ttu-id="2d050-275">ux_device_stack_interface_delete</span><span class="sxs-lookup"><span data-stu-id="2d050-275">ux_device_stack_interface_delete</span></span>

<span data-ttu-id="2d050-276">Eliminare un'interfaccia dello stack</span><span class="sxs-lookup"><span data-stu-id="2d050-276">Delete a stack interface</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-277">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-277">Prototype</span></span>

```c
UINT ux_device_stack_interface_delete(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a><span data-ttu-id="2d050-278">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-278">Description</span></span>

<span data-ttu-id="2d050-279">Questa funzione viene chiamata quando è necessario rimuovere un'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-279">This function is called when an interface should be removed.</span></span> <span data-ttu-id="2d050-280">Un'interfaccia viene rimossa quando viene estratto un dispositivo o dopo una reimpostazione del bus o quando è presente una nuova impostazione alternativa.</span><span class="sxs-lookup"><span data-stu-id="2d050-280">An interface is either removed when a device is extracted, or following a bus reset, or when there is a new alternate setting.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-281">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-281">Input Parameter</span></span>

- <span data-ttu-id="2d050-282">**interfaccia**: puntatore all'interfaccia da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="2d050-282">**interface**: Pointer to the interface to remove.</span></span>

### <a name="return-value"></a><span data-ttu-id="2d050-283">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2d050-283">Return Value</span></span>

- <span data-ttu-id="2d050-284">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-284">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-285">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-285">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_delete(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_get"></a><span data-ttu-id="2d050-286">ux_device_stack_interface_get</span><span class="sxs-lookup"><span data-stu-id="2d050-286">ux_device_stack_interface_get</span></span>

<span data-ttu-id="2d050-287">Ottenere il valore dell'interfaccia corrente</span><span class="sxs-lookup"><span data-stu-id="2d050-287">Get the current interface value</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-288">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-288">Prototype</span></span>

```c
UINT ux_device_stack_interface_get(UINT interface_value);
```

### <a name="description"></a><span data-ttu-id="2d050-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-289">Description</span></span>

<span data-ttu-id="2d050-290">Questa funzione viene chiamata quando l'host esegue una query sull'interfaccia corrente.</span><span class="sxs-lookup"><span data-stu-id="2d050-290">This function is called when the host queries the current interface.</span></span> <span data-ttu-id="2d050-291">Il dispositivo restituisce il valore dell'interfaccia corrente.</span><span class="sxs-lookup"><span data-stu-id="2d050-291">The device returns the current interface value.</span></span>

> [!NOTE]
> <span data-ttu-id="2d050-292">Questa funzione è deprecata.</span><span class="sxs-lookup"><span data-stu-id="2d050-292">This function is deprecated.</span></span> <span data-ttu-id="2d050-293">È disponibile per il software legacy, ma il nuovo software deve invece usare la funzione ***ux_device_stack_alternate_setting_get*** .</span><span class="sxs-lookup"><span data-stu-id="2d050-293">It is available for legacy software, but new software should use the ***ux_device_stack_alternate_setting_get*** function instead.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-294">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-294">Input Parameter</span></span>

- <span data-ttu-id="2d050-295">**interface_value** Valore di interfaccia da restituire.</span><span class="sxs-lookup"><span data-stu-id="2d050-295">**interface_value** Interface value to return.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-296">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-296">Return Values</span></span>

- <span data-ttu-id="2d050-297">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-297">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="2d050-298">**UX_ERROR** (0Xff) non esiste alcuna interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-298">**UX_ERROR** (0xFF) No interface exists.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-299">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-299">Example</span></span>

```c
ULONG interface_value;

UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_set"></a><span data-ttu-id="2d050-300">ux_device_stack_interface_set</span><span class="sxs-lookup"><span data-stu-id="2d050-300">ux_device_stack_interface_set</span></span>

<span data-ttu-id="2d050-301">Modificare l'impostazione alternativa dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="2d050-301">Change the alternate setting of the interface</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-302">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-302">Prototype</span></span>

```c
UINT ux_device_stack_interface_set(
    UCHAR *device_framework,
    ULONG device_framework_length, 
    ULONG alternate_setting_value);
```

### <a name="description"></a><span data-ttu-id="2d050-303">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-303">Description</span></span>

<span data-ttu-id="2d050-304">Questa funzione viene chiamata quando l'host richiede una modifica dell'impostazione alternativa per l'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-304">This function is called when the host requests a change of the alternate setting for the interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-305">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-305">Parameters</span></span>

- <span data-ttu-id="2d050-306">**device_framework**: indirizzo del Framework del dispositivo per questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-306">**device_framework**: Address of the device framework for this interface.</span></span>
- <span data-ttu-id="2d050-307">**device_framework_length**: lunghezza del Framework del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2d050-307">**device_framework_length**: Length of the device framework.</span></span>
- <span data-ttu-id="2d050-308">**alternate_setting_value**: valore di impostazione alternativo che verrà utilizzato da questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-308">**alternate_setting_value**: Alternate setting value to be used by this interface.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-309">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-309">Return Values</span></span>

- <span data-ttu-id="2d050-310">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-310">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="2d050-311">**UX_ERROR** (0Xff) non esiste alcuna interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-311">**UX_ERROR** (0xFF) No interface exists.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-312">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-312">Example</span></span>

```c
UCHAR * device_framework
ULONG device_framework_length;
ULONG alternate_setting_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_set(device_framework,
    device_framework_length, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_start"></a><span data-ttu-id="2d050-313">ux_device_stack_interface_start</span><span class="sxs-lookup"><span data-stu-id="2d050-313">ux_device_stack_interface_start</span></span>

<span data-ttu-id="2d050-314">Avvia la ricerca di una classe per il proprietario di un'istanza dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="2d050-314">Start search for a class to own an interface instance</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-315">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-315">Prototype</span></span>

```c
UINT ux_device_stack_interface_start(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a><span data-ttu-id="2d050-316">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-316">Description</span></span>

<span data-ttu-id="2d050-317">Questa funzione viene chiamata quando un'interfaccia è stata selezionata dall'host e lo stack del dispositivo deve cercare una classe dispositivo per il proprietario di questa istanza dell'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-317">This function is called when an interface has been selected by the host and the device stack needs to search for a device class to own this interface instance.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="2d050-318">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="2d050-318">Input Parameter</span></span>

- <span data-ttu-id="2d050-319">**interfaccia**: puntatore all'interfaccia creata.</span><span class="sxs-lookup"><span data-stu-id="2d050-319">**interface**: Pointer to the interface created.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-320">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-320">Return Values</span></span>

- <span data-ttu-id="2d050-321">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-321">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="2d050-322">**UX_NO_CLASS_MATCH** (0x57) non esiste alcuna classe per questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2d050-322">**UX_NO_CLASS_MATCH** (0x57) No class exists for this interface.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-323">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-323">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_start(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_transfer_request"></a><span data-ttu-id="2d050-324">ux_device_stack_transfer_request</span><span class="sxs-lookup"><span data-stu-id="2d050-324">ux_device_stack_transfer_request</span></span>

<span data-ttu-id="2d050-325">Richiesta di trasferimento dei dati all'host</span><span class="sxs-lookup"><span data-stu-id="2d050-325">Request to transfer data to the host</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-326">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-326">Prototype</span></span>

```c
UINT ux_device_stack_transfer_request(
    UX_SLAVE_TRANSFER *transfer_request,
    ULONG slave_length, 
    ULONG host_length);
```

### <a name="description"></a><span data-ttu-id="2d050-327">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-327">Description</span></span>

<span data-ttu-id="2d050-328">Questa funzione viene chiamata quando una classe o lo stack desidera trasferire i dati all'host.</span><span class="sxs-lookup"><span data-stu-id="2d050-328">This function is called when a class or the stack wants to transfer data to the host.</span></span> <span data-ttu-id="2d050-329">L'host esegue sempre il polling del dispositivo, ma il dispositivo può preparare i dati in anticipo.</span><span class="sxs-lookup"><span data-stu-id="2d050-329">The host always polls the device but the device can prepare data in advance.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-330">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-330">Parameters</span></span>

- <span data-ttu-id="2d050-331">**transfer_request**: puntatore alla richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="2d050-331">**transfer_request**: Pointer to the transfer request.</span></span>
- <span data-ttu-id="2d050-332">**slave_length**: lunghezza del dispositivo che vuole restituire.</span><span class="sxs-lookup"><span data-stu-id="2d050-332">**slave_length**: Length the device wants to return.</span></span>
- <span data-ttu-id="2d050-333">**host_length**: lunghezza richiesta dall'host.</span><span class="sxs-lookup"><span data-stu-id="2d050-333">**host_length**: Length the host has requested.</span></span>

### <a name="return-values"></a><span data-ttu-id="2d050-334">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2d050-334">Return Values</span></span>

- <span data-ttu-id="2d050-335">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-335">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="2d050-336">**UX_TRANSFER_NOT_READY** (0x25) il dispositivo è in uno stato non valido; deve essere **collegato**, **configurato** o **risolto**.</span><span class="sxs-lookup"><span data-stu-id="2d050-336">**UX_TRANSFER_NOT_READY** (0x25) The device is in an invalid state; it must be **ATTACHED**, **CONFIGURED**, or **ADDRESSED**.</span></span>
- <span data-ttu-id="2d050-337">Errore di trasporto **UX_ERROR** (0xFF).</span><span class="sxs-lookup"><span data-stu-id="2d050-337">**UX_ERROR** (0xFF) Transport error.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-338">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-338">Example</span></span>

```c
UINT status;

/* The following example illustrates how to transfer more data than an application requests. */
while(total_length) {
    /* How much can we send in this transfer? */
    if (total_length > UX_SLAVE_CLASS_STORAGE_BUFFER_SIZE)
        transfer_length = UX_SLAVE_CLASS_STORAGE_BUFFER_SIZE;
    else
        transfer_length = total_length;

   /* Copy the Storage Buffer into the transfer request memory. */
   ux_utility_memory_copy(transfer_request ->  ux_slave_transfer_request_data_pointer,
       media_memory, transfer_length);

   /* Send the data payload back to the caller. */
   status = ux_device_transfer_request(transfer_request,
       transfer_length, transfer_length);

   /* If status equals UX_SUCCESS, the operation was successful. */

   /* Update the buffer address.  */
    media_memory += transfer_length;

   /* Update the length to remain. */
    total_length -= transfer_length;
}
```

### <a name="ux_device_stack_transfer_abort"></a><span data-ttu-id="2d050-339">ux_device_stack_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="2d050-339">ux_device_stack_transfer_abort</span></span>

<span data-ttu-id="2d050-340">Annullare una richiesta di trasferimento</span><span class="sxs-lookup"><span data-stu-id="2d050-340">Cancel a transfer request</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-341">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-341">Prototype</span></span>

```c
UINT ux_device_stack_transfer_abort(
    UX_SLAVE_TRANSFER *transfer_request, 
    ULONG completion_code);
```

### <a name="description"></a><span data-ttu-id="2d050-342">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-342">Description</span></span>

<span data-ttu-id="2d050-343">Questa funzione viene chiamata quando un'applicazione deve annullare una richiesta di trasferimento o quando lo stack deve interrompere una richiesta di trasferimento associata a un endpoint.</span><span class="sxs-lookup"><span data-stu-id="2d050-343">This function is called when an application needs to cancel a transfer request or when the stack needs to abort a transfer request associated with an endpoint.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-344">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-344">Parameters</span></span>

- <span data-ttu-id="2d050-345">**transfer_request**: puntatore alla richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="2d050-345">**transfer_request**: Pointer to the transfer request.</span></span>
- <span data-ttu-id="2d050-346">**completion_code**: codice di errore da restituire alla classe in attesa del completamento della richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="2d050-346">**completion_code**: Error code to be returned to the class waiting for this transfer request to complete.</span></span>

### <a name="return-value"></a><span data-ttu-id="2d050-347">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2d050-347">Return Value</span></span>

- <span data-ttu-id="2d050-348">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-348">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="2d050-349">Esempio</span><span class="sxs-lookup"><span data-stu-id="2d050-349">Example</span></span>

```c
UINT status;

/* The following example illustrates how to abort a transfer when a
    bus reset has been detected on the bus. */
status = ux_device_stack_transfer_abort(transfer_request, UX_TRANSFER_BUS_RESET);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_uninitialize"></a><span data-ttu-id="2d050-350">ux_device_stack_uninitialize</span><span class="sxs-lookup"><span data-stu-id="2d050-350">ux_device_stack_uninitialize</span></span>

<span data-ttu-id="2d050-351">Stack Unitialize</span><span class="sxs-lookup"><span data-stu-id="2d050-351">Unitialize stack</span></span>

### <a name="prototype"></a><span data-ttu-id="2d050-352">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2d050-352">Prototype</span></span>

```c
UINT ux_device_stack_uninitialize();
```

### <a name="description"></a><span data-ttu-id="2d050-353">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d050-353">Description</span></span>

<span data-ttu-id="2d050-354">Questa funzione viene chiamata quando un'applicazione deve unitialize lo stack di dispositivi USBX. tutte le risorse dello stack del dispositivo vengono liberate.</span><span class="sxs-lookup"><span data-stu-id="2d050-354">This function is called when an application needs to unitialize the USBX device stack – all device stack resources are freed.</span></span> <span data-ttu-id="2d050-355">Questa operazione deve essere chiamata dopo che è stata annullata la registrazione di tutte le classi tramite ux_device_stack_class_unregister.</span><span class="sxs-lookup"><span data-stu-id="2d050-355">This should be called after all classes have been unregistered via ux_device_stack_class_unregister.</span></span>

### <a name="parameters"></a><span data-ttu-id="2d050-356">Parametri</span><span class="sxs-lookup"><span data-stu-id="2d050-356">Parameters</span></span>

<span data-ttu-id="2d050-357">nessuno</span><span class="sxs-lookup"><span data-stu-id="2d050-357">None</span></span>

### <a name="return-value"></a><span data-ttu-id="2d050-358">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2d050-358">Return Value</span></span>

<span data-ttu-id="2d050-359">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="2d050-359">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
