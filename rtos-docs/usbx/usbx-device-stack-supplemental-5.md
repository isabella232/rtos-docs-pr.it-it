---
title: Capitolo 5-USBX OTG
description: Informazioni su come USBX supporta le funzionalità di OTG di USB quando è disponibile un controller USB compatibile con OTG nell'hardware design.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 64a3c44f84b9ffca31d9e616d14d3d5d87c56bd7
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550321"
---
# <a name="chapter-5---usbx-otg"></a><span data-ttu-id="71472-103">Capitolo 5-USBX OTG</span><span class="sxs-lookup"><span data-stu-id="71472-103">Chapter 5 - USBX OTG</span></span>

<span data-ttu-id="71472-104">USBX supporta le funzionalità di OTG di USB quando un controller USB compatibile con OTG è disponibile nella progettazione dell'hardware.</span><span class="sxs-lookup"><span data-stu-id="71472-104">USBX supports the OTG functionalities of USB when an OTG compliant USB controller is available in the hardware design.</span></span>

<span data-ttu-id="71472-105">USBX supporta OTG nello stack USB principale.</span><span class="sxs-lookup"><span data-stu-id="71472-105">USBX supports OTG in the core USB stack.</span></span> <span data-ttu-id="71472-106">Per il funzionamento di OTG, tuttavia, è necessario un controller USB specifico.</span><span class="sxs-lookup"><span data-stu-id="71472-106">But for OTG to function, it requires a specific USB controller.</span></span> <span data-ttu-id="71472-107">Le funzioni del controller USBX OTG si trovano nella directory usbx_otg.</span><span class="sxs-lookup"><span data-stu-id="71472-107">USBX OTG controller functions can be found in the usbx_otg directory.</span></span> <span data-ttu-id="71472-108">La versione corrente di USBX supporta solo il LPC3131 NXP con le funzionalità complete di OTG.</span><span class="sxs-lookup"><span data-stu-id="71472-108">The current USBX version only supports the NXP LPC3131 with full OTG capabilities.</span></span>

<span data-ttu-id="71472-109">Le funzioni regolari del driver del controller (host o dispositivo) sono ancora disponibili nella usbx_device_controllers USBX standard e usbx_host_controllers ma la directory usbx_otg contiene le funzioni OTG specifiche associate al controller USB.</span><span class="sxs-lookup"><span data-stu-id="71472-109">The regular controller driver functions (host or device) can still be found in the standard USBX usbx_device_controllers and usbx_host_controllers but the usbx_otg directory contains the specific OTG functions associated with the USB controller.</span></span>

<span data-ttu-id="71472-110">Sono disponibili quattro categorie di funzioni per un controller OTG oltre alle normali funzioni host/dispositivo.</span><span class="sxs-lookup"><span data-stu-id="71472-110">There are four categories of functions for an OTG controller in addition to the usual host/device functions.</span></span>

- <span data-ttu-id="71472-111">Funzioni specifiche di VBUS</span><span class="sxs-lookup"><span data-stu-id="71472-111">VBUS specific functions</span></span>
- <span data-ttu-id="71472-112">Avvio e arresto del controller</span><span class="sxs-lookup"><span data-stu-id="71472-112">Start and Stop of the controller</span></span>
- <span data-ttu-id="71472-113">Gestione ruoli USB</span><span class="sxs-lookup"><span data-stu-id="71472-113">USB role manager</span></span>
- <span data-ttu-id="71472-114">Gestori di interrupt</span><span class="sxs-lookup"><span data-stu-id="71472-114">Interrupt handlers</span></span>

## <a name="vbus-functions"></a><span data-ttu-id="71472-115">Funzioni VBUS</span><span class="sxs-lookup"><span data-stu-id="71472-115">VBUS functions</span></span>

<span data-ttu-id="71472-116">Ogni controller deve disporre di un VBUS Manager per modificare lo stato di VBUS in base ai requisiti di risparmio energia.</span><span class="sxs-lookup"><span data-stu-id="71472-116">Each controller needs to have a VBUS manager to change the state of VBUS based on power management requirements.</span></span> <span data-ttu-id="71472-117">In genere, questa funzione esegue solo l'attivazione o la disattivazione di VBUS.</span><span class="sxs-lookup"><span data-stu-id="71472-117">Usually, this function only performs turning on or off VBUS.</span></span>

## <a name="start-and-stop-the-controller"></a><span data-ttu-id="71472-118">Avviare e arrestare il controller</span><span class="sxs-lookup"><span data-stu-id="71472-118">Start and Stop the controller</span></span>

<span data-ttu-id="71472-119">Diversamente da quanto avviene con un'implementazione USB normale, il gruppo OTG richiede che l'host e/o lo stack del dispositivo siano attivati e disattivati in caso di modifica del ruolo.</span><span class="sxs-lookup"><span data-stu-id="71472-119">Unlike a regular USB implementation, OTG requires the host and/or the device stack to be activated and deactivated when the role changes.</span></span>

## <a name="usb-role-manager"></a><span data-ttu-id="71472-120">Gestione ruoli USB</span><span class="sxs-lookup"><span data-stu-id="71472-120">USB role Manager</span></span>

<span data-ttu-id="71472-121">Il gestore dei ruoli USB riceve i comandi per modificare lo stato del dispositivo USB.</span><span class="sxs-lookup"><span data-stu-id="71472-121">The USB role manager receives commands to change the state of the USB.</span></span> <span data-ttu-id="71472-122">Ci sono diversi Stati che richiedono transizioni da e verso:</span><span class="sxs-lookup"><span data-stu-id="71472-122">There are several states that need transitions to and from:</span></span>

| <span data-ttu-id="71472-123">State</span><span class="sxs-lookup"><span data-stu-id="71472-123">State</span></span>                    | <span data-ttu-id="71472-124">valore</span><span class="sxs-lookup"><span data-stu-id="71472-124">Value</span></span> | <span data-ttu-id="71472-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="71472-125">Description</span></span>                                           |
| ------------------------ | ----- | ----------------------------------------------------- |
| <span data-ttu-id="71472-126">UX_OTG_IDLE</span><span class="sxs-lookup"><span data-stu-id="71472-126">UX_OTG_IDLE</span></span>            | <span data-ttu-id="71472-127">0</span><span class="sxs-lookup"><span data-stu-id="71472-127">0</span></span>     | <span data-ttu-id="71472-128">Il dispositivo è inattivo.</span><span class="sxs-lookup"><span data-stu-id="71472-128">The device is Idle.</span></span> <span data-ttu-id="71472-129">Non connesso ad alcun elemento</span><span class="sxs-lookup"><span data-stu-id="71472-129">Not connected to anything</span></span> |
| <span data-ttu-id="71472-130">UX_OTG_IDLE_TO_HOST</span><span class="sxs-lookup"><span data-stu-id="71472-130">UX_OTG_IDLE_TO_HOST</span></span>  | <span data-ttu-id="71472-131">1</span><span class="sxs-lookup"><span data-stu-id="71472-131">1</span></span>     | <span data-ttu-id="71472-132">Il dispositivo è connesso a un connettore di tipo</span><span class="sxs-lookup"><span data-stu-id="71472-132">Device is connected with type A connector</span></span>             |
| <span data-ttu-id="71472-133">UX_OTG_IDLE_TO_SLAVE</span><span class="sxs-lookup"><span data-stu-id="71472-133">UX_OTG_IDLE_TO_SLAVE</span></span> | <span data-ttu-id="71472-134">2</span><span class="sxs-lookup"><span data-stu-id="71472-134">2</span></span>     | <span data-ttu-id="71472-135">Il dispositivo è connesso al connettore di tipo B</span><span class="sxs-lookup"><span data-stu-id="71472-135">Device is connected with type B connector</span></span>             |
| <span data-ttu-id="71472-136">UX_OTG_HOST_TO_IDLE</span><span class="sxs-lookup"><span data-stu-id="71472-136">UX_OTG_HOST_TO_IDLE</span></span>  | <span data-ttu-id="71472-137">3</span><span class="sxs-lookup"><span data-stu-id="71472-137">3</span></span>     | <span data-ttu-id="71472-138">Il dispositivo host è stato disconnesso</span><span class="sxs-lookup"><span data-stu-id="71472-138">Host device got disconnected</span></span>                          |
| <span data-ttu-id="71472-139">UX_OTG_HOST_TO_SLAVE</span><span class="sxs-lookup"><span data-stu-id="71472-139">UX_OTG_HOST_TO_SLAVE</span></span> | <span data-ttu-id="71472-140">4</span><span class="sxs-lookup"><span data-stu-id="71472-140">4</span></span>     | <span data-ttu-id="71472-141">Scambio di ruoli da host a slave</span><span class="sxs-lookup"><span data-stu-id="71472-141">Role swap from Host to Slave</span></span>                          |
| <span data-ttu-id="71472-142">UX_OTG_SLAVE_TO_IDLE</span><span class="sxs-lookup"><span data-stu-id="71472-142">UX_OTG_SLAVE_TO_IDLE</span></span> | <span data-ttu-id="71472-143">5</span><span class="sxs-lookup"><span data-stu-id="71472-143">5</span></span>     | <span data-ttu-id="71472-144">Il dispositivo slave è disconnesso</span><span class="sxs-lookup"><span data-stu-id="71472-144">Slave device is disconnected</span></span>                          |
| <span data-ttu-id="71472-145">UX_OTG_SLAVE_TO_HOST</span><span class="sxs-lookup"><span data-stu-id="71472-145">UX_OTG_SLAVE_TO_HOST</span></span> | <span data-ttu-id="71472-146">6</span><span class="sxs-lookup"><span data-stu-id="71472-146">6</span></span>     | <span data-ttu-id="71472-147">Scambio di ruoli da slave a host</span><span class="sxs-lookup"><span data-stu-id="71472-147">Role swap from Slave to Host</span></span>                          |

## <a name="interrupt-handlers"></a><span data-ttu-id="71472-148">Gestori di interrupt</span><span class="sxs-lookup"><span data-stu-id="71472-148">Interrupt handlers</span></span>

<span data-ttu-id="71472-149">Sia i driver di host che i driver del controller del dispositivo per OTG necessitano di gestori di interrupt diversi per monitorare i segnali oltre gli interrupt USB tradizionali, in particolare i segnali dovuti a SRP e VBUS.</span><span class="sxs-lookup"><span data-stu-id="71472-149">Both host and device controller drivers for OTG needs different interrupt handlers to monitor signals beyond traditional USB interrupts, in particular signals due to SRP and VBUS.</span></span>

<span data-ttu-id="71472-150">Come inizializzare un controller USB OTG.</span><span class="sxs-lookup"><span data-stu-id="71472-150">How to initialize a USB OTG controller.</span></span> <span data-ttu-id="71472-151">Per esempio, viene usato NXP LPC3131.</span><span class="sxs-lookup"><span data-stu-id="71472-151">We use the NXP LPC3131 as an example here.</span></span>

```C
/* Initialize the LPC3131 OTG controller. */
status = ux_otg_lpc3131_initialize(0x19000000, lpc3131_vbus_function,
    tx_demo_change_mode_callback);
```

<span data-ttu-id="71472-152">In questo esempio si inizializza il LPC3131 in modalità OTG passando una funzione VBUS e un callback per la modifica della modalità (da host a slave o viceversa).</span><span class="sxs-lookup"><span data-stu-id="71472-152">In this example, we initialize the LPC3131 in OTG mode by passing a VBUS function and a callback for mode change (from host to slave or vice versa).</span></span>

<span data-ttu-id="71472-153">La funzione di callback deve semplicemente registrare la nuova modalità e riattivare un thread in sospeso per agire sul nuovo stato.</span><span class="sxs-lookup"><span data-stu-id="71472-153">The callback function should simply record the new mode and wake up a pending thread to act up the new state.</span></span>

```C
void tx_demo_change_mode_callback(ULONG mode) {
    /* Simply save the otg mode. */
    otg_mode = mode;

    /* Wake up the thread that is waiting. */
    ux_utility_semaphore_put(&mode_change_semaphore);
}
```

<span data-ttu-id="71472-154">Il valore della modalità passato può includere i valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="71472-154">The mode value that is passed can have the following values.</span></span>

- <span data-ttu-id="71472-155">**UX_OTG_MODE_IDLE**</span><span class="sxs-lookup"><span data-stu-id="71472-155">**UX_OTG_MODE_IDLE**</span></span>
- <span data-ttu-id="71472-156">**UX_OTG_MODE_SLAVE**</span><span class="sxs-lookup"><span data-stu-id="71472-156">**UX_OTG_MODE_SLAVE**</span></span>
- <span data-ttu-id="71472-157">**UX_OTG_MODE_HOST**</span><span class="sxs-lookup"><span data-stu-id="71472-157">**UX_OTG_MODE_HOST**</span></span>

<span data-ttu-id="71472-158">L'applicazione può sempre controllare l'aspetto del dispositivo esaminando la variabile:</span><span class="sxs-lookup"><span data-stu-id="71472-158">The application can always check what the device is by looking at the variable:</span></span>

```C
_ux_system_otg -> ux_system_otg_device_type
```

<span data-ttu-id="71472-159">I valori possibili sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="71472-159">Its values can be any of the following.</span></span>

- <span data-ttu-id="71472-160">**UX_OTG_DEVICE_A**</span><span class="sxs-lookup"><span data-stu-id="71472-160">**UX_OTG_DEVICE_A**</span></span>
- <span data-ttu-id="71472-161">**UX_OTG_DEVICE_B**</span><span class="sxs-lookup"><span data-stu-id="71472-161">**UX_OTG_DEVICE_B**</span></span>
- <span data-ttu-id="71472-162">**UX_OTG_DEVICE_IDLE**</span><span class="sxs-lookup"><span data-stu-id="71472-162">**UX_OTG_DEVICE_IDLE**</span></span>

<span data-ttu-id="71472-163">Un dispositivo host USB OTG può sempre richiedere uno scambio di ruolo eseguendo il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="71472-163">A USB OTG host device can always ask for a role swap by issuing the following command.</span></span>

```C
/* Ask the stack to perform a HNP swap with the device. We relinquish the host role to A device. */
ux_host_stack_role_swap(storage -> ux_host_class_storage_device);
```

<span data-ttu-id="71472-164">Per un dispositivo slave, non esiste alcun comando da emettere, ma il dispositivo slave può impostare uno stato per modificare il ruolo, che verrà prelevato dall'host quando emette una **GET_STATUS** e lo scambio verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="71472-164">For a slave device, there is no command to issue but the slave device can set a state to change the role, which will be picked up by the host when it issues a **GET_STATUS** and the swap will then be initiated.</span></span>

```C
/* We are a B device, ask for role swap.
   The next GET_STATUS from the host will get the status change and do the HNP. */
_ux_system_otg -> ux_system_otg_slave_role_swap_flag =
    UX_OTG_HOST_REQUEST_FLAG;
```
