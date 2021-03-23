---
title: Capitolo 2-Considerazioni sulle classi di dispositivi USBX
description: La classe RNDIS del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo Ethernet. Questa classe è basata sull'implementazione proprietaria di Microsoft ed è specifica per le piattaforme Windows.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8104f00e192486f57fe9c22b2c83aa9a22954739
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824317"
---
# <a name="chapter-2---usbx-device-class-considerations"></a><span data-ttu-id="ff6cc-104">Capitolo 2-Considerazioni sulle classi di dispositivi USBX</span><span class="sxs-lookup"><span data-stu-id="ff6cc-104">Chapter 2 - USBX Device Class Considerations</span></span>

## <a name="usb-device-rndis-class"></a><span data-ttu-id="ff6cc-105">Classe RNDIS del dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="ff6cc-105">USB Device RNDIS Class</span></span>

<span data-ttu-id="ff6cc-106">La classe RNDIS del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-106">The USB device RNDIS class allows for a USB host system to communicate with the device as a ethernet device.</span></span> <span data-ttu-id="ff6cc-107">Questa classe è basata sull'implementazione proprietaria di Microsoft ed è specifica per le piattaforme Windows.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-107">This class is based on the Microsoft proprietary implementation and is specific to Windows platforms.</span></span>

<span data-ttu-id="ff6cc-108">Un Framework di dispositivi conforme a RNDIS deve essere dichiarato dallo stack del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-108">A RNDIS compliant device framework needs to be declared by the device stack.</span></span> <span data-ttu-id="ff6cc-109">Di seguito è riportato un esempio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-109">An example is found below.</span></span>

```C
unsigned char device_framework_full_speed[] = {
    /* VID: 0x04b4
    PID: 0x1127
    */

    /* Device Descriptor */
    0x12, /* bLength */
    0x01, /* bDescriptorType */
    0x10, 0x01, /* bcdUSB */
    0x02, /* bDeviceClass - CDC */
    0x00, /* bDeviceSubClass */
    0x00, /* bDeviceProtocol */
    0x40, /* bMaxPacketSize0 */
    0xb4, 0x04, /* idVendor */
    0x27, 0x11, /* idProduct */
    0x00, 0x01, /* bcdDevice */
    0x01, /* iManufacturer */
    0x02, /* iProduct */
    0x03, /* iSerialNumber */
    0x01, /* bNumConfigurations */

    /* Configuration Descriptor */
    0x09, /* bLength */
    0x02, /* bDescriptorType */
    0x38, 0x00, /* wTotalLength */
    0x02, /* bNumInterfaces */
    0x01, /* bConfigurationValue */
    0x00, /* iConfiguration */
    0x40, /* bmAttributes - Self-powered */
    0x00, /* bMaxPower */

    /* Interface Association Descriptor */
    0x08, /* bLength */
    0x0b, /* bDescriptorType */
    0x00, /* bFirstInterface */
    0x02, /* bInterfaceCount */
    0x02, /* bFunctionClass - CDC - Communication */
    0xff, /* bFunctionSubClass - Vendor Defined – In this case, RNDIS */
    0x00, /* bFunctionProtocol - No class specific protocol required */
    0x00, /* iFunction */

    /* Interface Descriptor */
    0x09, /* bLength */
    0x04, /* bDescriptorType */
    0x00, /* bInterfaceNumber */
    0x00, /* bAlternateSetting */
    0x01, /* bNumEndpoints */
    0x02, /* bInterfaceClass - CDC - Communication */
    0xff, /* bInterfaceSubClass - Vendor Defined – In this case, RNDIS */
    0x00, /* bInterfaceProtocol - No class specific protocol required */
    0x00, /* iInterface */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x83, /* bEndpointAddress */
    0x03, /* bmAttributes - Interrupt */
    0x08, 0x00, /* wMaxPacketSize */
    0xff, /* bInterval */

    /* Interface Descriptor */
    0x09, /* bLength */
    0x04, /* bDescriptorType */
    0x01, /* bInterfaceNumber */
    0x00, /* bAlternateSetting */
    0x02, /* bNumEndpoints */
    0x0a, /* bInterfaceClass - CDC - Data */
    0x00, /* bInterfaceSubClass - Should be 0x00 */
    0x00, /* bInterfaceProtocol - No class specific protocol required */
    0x00, /* iInterface */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x02, /* bEndpointAddress */
    0x02, /* bmAttributes - Bulk */
    0x40, 0x00, /* wMaxPacketSize */
    0x00, /* bInterval */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x81, /* bEndpointAddress */
    0x02, /* bmAttributes - Bulk */
    0x40, 0x00, /* wMaxPacketSize */
    0x00, /* bInterval */
};
```

<span data-ttu-id="ff6cc-110">La classe RNDIS usa un approccio del descrittore di dispositivo molto simile a CDC-ACM e CDC-ECM e richiede anche un descrittore IAD.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-110">The RNDIS class uses a very similar device descriptor approach to the CDC-ACM and CDC-ECM and also requires a IAD descriptor.</span></span> <span data-ttu-id="ff6cc-111">Vedere la classe CDC-ACM per la definizione e i requisiti per il descrittore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-111">See the CDC-ACM class for definition and requirements for the device descriptor.</span></span>

<span data-ttu-id="ff6cc-112">L'attivazione della classe RNDIS è la seguente.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-112">The activation of the RNDIS class is as follows.</span></span>

```C
/* Set the parameters for callback when insertion/extraction of a CDC device. Set to NULL.*/

parameter.ux_slave_class_rndis_instance_activate = UX_NULL;
parameter.ux_slave_class_rndis_instance_deactivate = UX_NULL;

/* Define a local NODE ID. */

parameter.ux_slave_class_rndis_parameter_local_node_id[0] = 0x00;
parameter.ux_slave_class_rndis_parameter_local_node_id[1] = 0x1e;
parameter.ux_slave_class_rndis_parameter_local_node_id[2] = 0x58;
parameter.ux_slave_class_rndis_parameter_local_node_id[3] = 0x41;
parameter.ux_slave_class_rndis_parameter_local_node_id[4] = 0xb8;
parameter.ux_slave_class_rndis_parameter_local_node_id[5] = 0x78;

/* Define a remote NODE ID. */

parameter.ux_slave_class_rndis_parameter_remote_node_id[0] = 0x00;
parameter.ux_slave_class_rndis_parameter_remote_node_id[1] = 0x1e;
parameter.ux_slave_class_rndis_parameter_remote_node_id[2] = 0x58;
parameter.ux_slave_class_rndis_parameter_remote_node_id[3] = 0x41;
parameter.ux_slave_class_rndis_parameter_remote_node_id[4] = 0xb8;
parameter.ux_slave_class_rndis_parameter_remote_node_id[5] = 0x79;

/* Set extra parameters used by the RNDIS query command with certain OIDs. */

parameter.ux_slave_class_rndis_parameter_vendor_id = 0x04b4 ;
parameter.ux_slave_class_rndis_parameter_driver_version = 0x1127;
ux_utility_memory_copy(parameter.ux_slave_class_rndis_parameter_vendor_description,
    "ELOGIC RNDIS", 12);

/* Initialize the device rndis class. This class owns both interfaces. */
status = ux_device_stack_class_register(_ux_system_slave_class_rndis_name,
    ux_device_class_rndis_entry, 1,0, &parameter);
```

<span data-ttu-id="ff6cc-113">Per quanto riguarda CDC-ECM, la classe RNDIS richiede 2 nodi, uno locale e uno remoto, ma non è necessario disporre di un descrittore di stringa che descrive il nodo remoto.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-113">As for the CDC-ECM, the RNDIS class requires 2 nodes, one local and one remote but there is no requirement to have a string descriptor describing the remote node.</span></span>

<span data-ttu-id="ff6cc-114">Tuttavia, a causa del meccanismo di messaggistica proprietaria di Microsoft, sono necessari alcuni parametri aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-114">However due to Microsoft proprietary messaging mechanism, some extra parameters are required.</span></span> <span data-ttu-id="ff6cc-115">Prima di tutto è necessario passare l'ID fornitore.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-115">First the vendor ID has to be passed.</span></span> <span data-ttu-id="ff6cc-116">Analogamente, la versione del driver di RNDIS.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-116">Likewise, the driver version of the RNDIS.</span></span> <span data-ttu-id="ff6cc-117">È necessario assegnare anche una stringa del fornitore.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-117">A vendor string must also be given.</span></span>

<span data-ttu-id="ff6cc-118">La classe RNDIS dispone di API predefinite per il trasferimento dei dati in entrambe le direzioni, ma sono nascoste all'applicazione perché l'applicazione utente comunicherà con il dispositivo Ethernet USB tramite NetX.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-118">The RNDIS class has built-in APIs for transferring data both ways but they are hidden to the application as the user application will communicate with the USB Ethernet device through NetX.</span></span>

<span data-ttu-id="ff6cc-119">La classe USBX RNDIS è strettamente legata allo stack di rete NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-119">The USBX RNDIS class is closely tied to Azure RTOS NetX Network stack.</span></span> <span data-ttu-id="ff6cc-120">Un'applicazione che usa sia NetX che la classe RNDIS di USBX attiverà lo stack di rete NetX nel modo consueto, ma in aggiunta deve attivare lo stack di rete USB come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-120">An application using both NetX and USBX RNDIS class will activate the NetX network stack in its usual way but in addition needs to activate the USB network stack as follows.</span></span>

```C
/* Initialize the NetX system. */

nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

<span data-ttu-id="ff6cc-121">Lo stack di rete USB deve essere attivato solo una volta e non è specifico di RNDIS, ma è richiesto da qualsiasi classe USB che richiede i servizi di NetX.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-121">The USB network stack needs to be activated only once and is not specific to RNDIS but is required by any USB class that requires NetX services.</span></span>

<span data-ttu-id="ff6cc-122">La classe RNDIS non verrà riconosciuta dagli host MAC OS e Linux perché è specifica dei sistemi operativi Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-122">The RNDIS class will not be recognized by MAC OS and Linux hosts as it is specific to Microsoft operating systems.</span></span> <span data-ttu-id="ff6cc-123">Nelle piattaforme Windows un file con estensione inf deve essere presente nell'host che corrisponde al descrittore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-123">On windows platforms a .inf file needs to be present on the host that matches the device descriptor.</span></span> <span data-ttu-id="ff6cc-124">Microsoft fornisce un modello per la classe RNDIS ed è disponibile nella directory usbx_windows_host_files.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-124">Microsoft supplies a template for the RNDIS class and it can be found in the usbx_windows_host_files directory.</span></span> <span data-ttu-id="ff6cc-125">Per la versione più recente di Windows, è necessario usare il file RNDIS_Template. inf.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-125">For more recent version of Windows the file RNDIS_Template.inf should be used.</span></span> <span data-ttu-id="ff6cc-126">Questo file deve essere modificato in modo da riflettere il PID/VID usato dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-126">This file needs to be modified to reflect the PID/VID used by the device.</span></span> <span data-ttu-id="ff6cc-127">Il PID/VID sarà specifico per il cliente finale quando la società e il prodotto vengono registrati con il dispositivo USB-IF.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-127">The PID/VID will be specific to the final customer when the company and the product are registered with the USB-IF.</span></span> <span data-ttu-id="ff6cc-128">Nel file inf i campi da modificare si trovano qui.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-128">In the inf file, the fields to modify are located here.</span></span>

```Inf
[DeviceList]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00

[DeviceList.NTamd64]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00
```

<span data-ttu-id="ff6cc-129">Nel Framework del dispositivo RNDIS il PID/VID viene archiviato nel descrittore del dispositivo. vedere il descrittore del dispositivo dichiarato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-129">In the device framework of the RNDIS device, the PID/VID are stored in the device descriptor (see the device descriptor declared above)</span></span>

<span data-ttu-id="ff6cc-130">Quando un sistema host USB individua il dispositivo RNDIS USB, viene montata un'interfaccia di rete e il dispositivo può essere usato con lo stack del protocollo di rete.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-130">When a USB host systems discovers the USB RNDIS device, it will mount a network interface and the device can be used with network protocol stack.</span></span> <span data-ttu-id="ff6cc-131">Per informazioni di riferimento, vedere il sistema operativo host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-131">See the host Operating System for reference.</span></span>

## <a name="usb-device-dfu-class"></a><span data-ttu-id="ff6cc-132">Classe dispositivo USB DFU</span><span class="sxs-lookup"><span data-stu-id="ff6cc-132">USB Device DFU Class</span></span>

<span data-ttu-id="ff6cc-133">La classe dispositivo USB DFU consente a un sistema host USB di aggiornare il firmware del dispositivo in base a un'applicazione host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-133">The USB device DFU class allows for a USB host system to update the device firmware based on a host application.</span></span> <span data-ttu-id="ff6cc-134">La classe DFU è una classe standard USB-IF.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-134">The DFU class is a USB-IF standard class.</span></span>

<span data-ttu-id="ff6cc-135">La classe USBX DFU è relativamente semplice.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-135">USBX DFU class is relatively simple.</span></span> <span data-ttu-id="ff6cc-136">Il descrittore del dispositivo it non richiede alcun endpoint di controllo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-136">It device descriptor does not require anything but a control endpoint.</span></span> <span data-ttu-id="ff6cc-137">Nella maggior parte dei casi, questa classe verrà incorporata in un dispositivo composito USB.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-137">Most of the time, this class will be embedded into a USB composite device.</span></span> <span data-ttu-id="ff6cc-138">Il dispositivo può essere qualsiasi, ad esempio un dispositivo di archiviazione o un dispositivo di comunicazione, e l'interfaccia DFU aggiunta può informare l'host che il firmware del dispositivo può essere aggiornato in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-138">The device can be anything such as a storage device or a comm device and the added DFU interface can inform the host that the device can have its firmware updated on the fly.</span></span>

<span data-ttu-id="ff6cc-139">La classe DFU funziona in 3 passaggi.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-139">The DFU class works in 3 steps.</span></span> <span data-ttu-id="ff6cc-140">Prima di tutto il dispositivo viene montato normalmente usando la classe esportata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-140">First the device mounts as normal using the class exported.</span></span> <span data-ttu-id="ff6cc-141">Un'applicazione nell'host (Windows o Linux) eserciterà la classe DFU e invierà una richiesta per ripristinare la modalità DFU del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-141">An application on the host (Windows or Linux) will exercise the DFU class and send a request to reset the device into DFU mode.</span></span> <span data-ttu-id="ff6cc-142">Il dispositivo scomparirà dal bus per un breve periodo di tempo (sufficiente per l'host e il dispositivo per rilevare una sequenza di reimpostazione) e al riavvio, il dispositivo sarà esclusivamente in modalità DFU, in attesa che l'applicazione host invii un aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-142">The device will disappear from the bus for a short time (enough for the host and the device to detect a RESET sequence) and upon restarting, the device will be exclusively in DFU mode, waiting for the host application to send a firmware upgrade.</span></span> <span data-ttu-id="ff6cc-143">Al termine dell'aggiornamento del firmware, l'applicazione host Reimposta il dispositivo e, al momento della rienumerazione, il dispositivo tornerà al normale funzionamento con il nuovo firmware.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-143">When the firmware upgrade has been completed, the host application resets the device and upon re-enumeration the device will revert to its normal operation with the new firmware.</span></span>

<span data-ttu-id="ff6cc-144">Un Framework del dispositivo DFU sarà simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-144">A DFU device framework will look like this.</span></span>

```C
UCHAR device_framework_full_speed[] = {

    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x40,
    0x99, 0x99, 0x00, 0x00, 0x00, 0x00, 0x01, 0x02,
    0x03, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x1b, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor for DFU. */
    0x09, 0x04, 0x00, 0x00, 0x00, 0xFE, 0x01, 0x01, 0x00,

    /* Functional descriptor for DFU. */
    0x09, 0x21, 0x0f, 0xE8, 0x03, 0x40, 0x00, 0x00,
    0x01,

};
```

<span data-ttu-id="ff6cc-145">In questo esempio, il descrittore DFU non è associato ad altre classi.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-145">In this example, the DFU descriptor is not associated with any other classes.</span></span> <span data-ttu-id="ff6cc-146">Dispone di un descrittore di interfaccia semplice e nessun altro endpoint collegato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-146">It has a simple interface descriptor and no other endpoints attached to it.</span></span> <span data-ttu-id="ff6cc-147">È disponibile un descrittore funzionale che descrive le specifiche delle funzionalità di DFU del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-147">There is a Functional descriptor that describes the specifics of the DFU capabilities of the device.</span></span>

<span data-ttu-id="ff6cc-148">La descrizione delle funzionalità di DFU è la seguente:</span><span class="sxs-lookup"><span data-stu-id="ff6cc-148">The description of the DFU capabilities are as follows.</span></span>

| <span data-ttu-id="ff6cc-149">Nome</span><span class="sxs-lookup"><span data-stu-id="ff6cc-149">Name</span></span>             | <span data-ttu-id="ff6cc-150">Offset</span><span class="sxs-lookup"><span data-stu-id="ff6cc-150">Offset</span></span>  | <span data-ttu-id="ff6cc-151">Dimensione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-151">Size</span></span> | <span data-ttu-id="ff6cc-152">tipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-152">type</span></span>      | <span data-ttu-id="ff6cc-153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-153">Description</span></span> |
|------------------|----------|------|-----------|------------|
| <span data-ttu-id="ff6cc-154">bmAttributes</span><span class="sxs-lookup"><span data-stu-id="ff6cc-154">bmAttributes</span></span>  | <span data-ttu-id="ff6cc-155">2</span><span class="sxs-lookup"><span data-stu-id="ff6cc-155">2</span></span>     | <span data-ttu-id="ff6cc-156">1</span><span class="sxs-lookup"><span data-stu-id="ff6cc-156">1</span></span>   | <span data-ttu-id="ff6cc-157">Campo di bit</span><span class="sxs-lookup"><span data-stu-id="ff6cc-157">Bit field</span></span> | <span data-ttu-id="ff6cc-158">Bit 3: il dispositivo eseguirà una sequenza di scollegamento e collegamento del bus quando riceve una richiesta DFU_DETACH.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-158">Bit 3: device will perform a bus detach-attach sequence when it receives a DFU_DETACH request.</span></span> <span data-ttu-id="ff6cc-159">L'host non deve emettere una reimpostazione USB.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-159">The host must not issue a USB Reset.</span></span> <span data-ttu-id="ff6cc-160">(bitWillDetach) 0 = No 1 = sì bit 2: il dispositivo è in grado di comunicare tramite USB dopo la fase di manifesto.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-160">(bitWillDetach) 0 = no 1 = yes Bit 2: device is able to communicate via USB after Manifestation phase.</span></span> <span data-ttu-id="ff6cc-161">(bitManifestationTolerant) 0 = No, deve vedere il ripristino del bus 1 = sì bit 1: upload capable (bitCanUpload) 0 = No 1 = sì bit 0: download capable (bitCanDnload) 0 = No 1 = Yes</span><span class="sxs-lookup"><span data-stu-id="ff6cc-161">(bitManifestationTolerant) 0 = no, must see bus reset 1 = yes Bit 1: upload capable (bitCanUpload) 0 = no 1 = yes Bit 0: download capable (bitCanDnload) 0 = no 1 = yes</span></span>  |
| <span data-ttu-id="ff6cc-162">wDetachTimeOut</span><span class="sxs-lookup"><span data-stu-id="ff6cc-162">wDetachTimeOut</span></span>  | <span data-ttu-id="ff6cc-163">3</span><span class="sxs-lookup"><span data-stu-id="ff6cc-163">3</span></span>      | <span data-ttu-id="ff6cc-164">2</span><span class="sxs-lookup"><span data-stu-id="ff6cc-164">2</span></span>  | <span data-ttu-id="ff6cc-165">d'acquisto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-165">number</span></span>    | <span data-ttu-id="ff6cc-166">Tempo, in millisecondi, durante il quale il dispositivo resterà in attesa dopo la ricezione della richiesta DFU_DETACH.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-166">Time, in milliseconds, that the device will wait after receipt of the DFU_DETACH request.</span></span> <span data-ttu-id="ff6cc-167">Se questo tempo scade senza una reimpostazione USB, il dispositivo interromperà la fase di riconfigurazione e tornerà al normale funzionamento.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-167">If this time elapses without a USB reset, then the device will terminate the Reconfiguration phase and revert back to normal operation.</span></span> <span data-ttu-id="ff6cc-168">Rappresenta il tempo massimo di attesa del dispositivo, a seconda dei timer e così via.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-168">This represents the maximum time that the device can wait (depending on its timers, etc.).</span></span> <span data-ttu-id="ff6cc-169">USBX imposta questo valore su 1000 ms.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-169">USBX sets this value to 1000 ms.</span></span>  |
| <span data-ttu-id="ff6cc-170">wTransferSize</span><span class="sxs-lookup"><span data-stu-id="ff6cc-170">wTransferSize</span></span>  | <span data-ttu-id="ff6cc-171">5</span><span class="sxs-lookup"><span data-stu-id="ff6cc-171">5</span></span>      | <span data-ttu-id="ff6cc-172">2</span><span class="sxs-lookup"><span data-stu-id="ff6cc-172">2</span></span>  | <span data-ttu-id="ff6cc-173">d'acquisto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-173">number</span></span>    | <span data-ttu-id="ff6cc-174">Numero massimo di byte che il dispositivo può accettare per ogni \- operazione di scrittura del controllo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-174">Maximum number of bytes that the device can accept per control\-write operation.</span></span> <span data-ttu-id="ff6cc-175">USBX imposta questo valore su 64 byte.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-175">USBX sets this value to 64 bytes.</span></span> |

<span data-ttu-id="ff6cc-176">La dichiarazione della classe DFU è la seguente:</span><span class="sxs-lookup"><span data-stu-id="ff6cc-176">The declaration of the DFU class is as follows:</span></span>

```C
/* Store the DFU parameters. */

dfu_parameter.ux_slave_class_dfu_parameter_instance_activate =
    tx_demo_thread_dfu_activate;

dfu_parameter.ux_slave_class_dfu_parameter_instance_deactivate =
    tx_demo_thread_dfu_deactivate;

dfu_parameter.ux_slave_class_dfu_parameter_read =
    tx_demo_thread_dfu_read;

dfu_parameter.ux_slave_class_dfu_parameter_write =
    tx_demo_thread_dfu_write;

dfu_parameter.ux_slave_class_dfu_parameter_get_status =
    tx_demo_thread_dfu_get_status;

dfu_parameter.ux_slave_class_dfu_parameter_notify =
    tx_demo_thread_dfu_notify;

dfu_parameter.ux_slave_class_dfu_parameter_framework =
    device_framework_dfu;

dfu_parameter.ux_slave_class_dfu_parameter_framework_length =
    DEVICE_FRAMEWORK_LENGTH_DFU;

/* Initialize the device dfu class. The class is connected with interface
1 on configuration 1. */
status = ux_device_stack_class_register(_ux_system_slave_class_dfu_name,
    ux_device_class_dfu_entry, 1, 0,
    (VOID *)&dfu_parameter);

if (status!=UX_SUCCESS) return;
```

<span data-ttu-id="ff6cc-177">La classe DFU deve funzionare con un'applicazione firmware del dispositivo specifica per la destinazione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-177">The DFU class needs to work with a device firmware application specific to the target.</span></span> <span data-ttu-id="ff6cc-178">Quindi definisce diverse chiamate a blocchi di lettura e scrittura di firmware e per ottenere lo stato dall'applicazione di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-178">Therefore it defines several call back to read and write blocks of firmware and to get status from the firmware update application.</span></span> <span data-ttu-id="ff6cc-179">La classe DFU dispone inoltre di una funzione Notify callback per informare l'applicazione quando si verifica un inizio e una fine del trasferimento del firmware.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-179">The DFU class also has a notify callback function to inform the application when a begin and end of transfer of the firmware occur.</span></span>

<span data-ttu-id="ff6cc-180">Di seguito è riportata la descrizione di un flusso di applicazione DFU tipico.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-180">Following is the description of a typical DFU application flow.</span></span>

![Flusso dell'applicazione DFU](./media/usbx-device-stack-supplemental/dfu-application-flow.png)

<span data-ttu-id="ff6cc-182">Il problema principale della classe DFU è ottenere l'applicazione corretta nell'host per eseguire il download del firmware.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-182">The major challenge of the DFU class is getting the right application on the host to perform the download the firmware.</span></span> <span data-ttu-id="ff6cc-183">Non sono presenti applicazioni fornite da Microsoft o da USB-IF.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-183">There is no application supplied by Microsoft or the USB-IF.</span></span> <span data-ttu-id="ff6cc-184">Alcune Shareware sono disponibili e funzionano ragionevolmente bene in Linux e in una minore quantità di Windows.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-184">Some shareware exist and they work reasonably well on Linux and to a lesser extent on Windows.</span></span>

<span data-ttu-id="ff6cc-185">In Linux è possibile usare dfu-utils qui: sono [https://wiki.openmoko.org/wiki/Dfu-util](https://wiki.openmoko.org/wiki/Dfu-util) disponibili numerose informazioni su dfu utils in questo collegamento: [https://www.libusb.org/wiki/windows_backend](https://www.libusb.org/wiki/windows_backend)</span><span class="sxs-lookup"><span data-stu-id="ff6cc-185">On Linux, one can use dfu-utils to be found here: [https://wiki.openmoko.org/wiki/Dfu-util](https://wiki.openmoko.org/wiki/Dfu-util) A lot of information on dfu utils can also be found on this link: [https://www.libusb.org/wiki/windows_backend](https://www.libusb.org/wiki/windows_backend)</span></span>

<span data-ttu-id="ff6cc-186">L'implementazione Linux di DFU esegue correttamente la sequenza di reimpostazione tra l'host e il dispositivo e pertanto non è necessario che il dispositivo esegua questa operazione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-186">The Linux implementation of DFU performs correctly the reset sequence between the host and the device and therefore the device does not need to do it.</span></span> <span data-ttu-id="ff6cc-187">Linux può accettare affinché il *BitWillDetach* bmAttributes sia 0.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-187">Linux can accept for the bmAttributes *bitWillDetach* to be 0.</span></span> <span data-ttu-id="ff6cc-188">Windows sull'altro lato richiede che il dispositivo esegua la reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-188">Windows on the other side requires the device to perform the reset.</span></span>

<span data-ttu-id="ff6cc-189">In Windows, il registro USB deve essere in grado di associare il dispositivo USB con i relativi PID/VID e la libreria USB, che a sua volta verrà usata dall'applicazione DFU.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-189">On Windows, the USB registry must be able to associate the USB device with its PID/VID and the USB library which will in turn be used by the DFU application.</span></span> <span data-ttu-id="ff6cc-190">Questa operazione può essere eseguita facilmente con l'utilità gratuita Zadig disponibile qui: [https://sourceforge.net/projects/libwdi/files/zadig/](https://sourceforge.net/projects/libwdi/files/zadig/) .</span><span class="sxs-lookup"><span data-stu-id="ff6cc-190">This can be easily done with the free utility Zadig which can be found here: [https://sourceforge.net/projects/libwdi/files/zadig/](https://sourceforge.net/projects/libwdi/files/zadig/).</span></span>

<span data-ttu-id="ff6cc-191">Se si esegue Zadig per la prima volta, verrà visualizzata la schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="ff6cc-191">Running Zadig for the first time will show this screen:</span></span>

![Esecuzione di Zadig per la prima volta](./media/usbx-device-stack-supplemental/zadig.png)

<span data-ttu-id="ff6cc-193">Dall'elenco dei dispositivi, trovare il dispositivo e associarlo al driver libusb Windows.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-193">From the device list, find your device and associate it with the libusb windows driver.</span></span> <span data-ttu-id="ff6cc-194">Questa operazione consente di associare il PID/VID del dispositivo alla libreria USB di Windows usata dalle utilità di DFU.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-194">This will bind the PID/VID of the device with the Windows USB library used by the DFU utilities.</span></span>

<span data-ttu-id="ff6cc-195">Per utilizzare il comando DFU, è sufficiente decomprimere le utilità di dfu compresse in una directory, assicurandosi che la dll libusb sia presente anche nella stessa directory.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-195">To operate the DFU command, simply unpack the zipped dfu utilities into a directory, making sure the libusb dll is also present in the same directory.</span></span> <span data-ttu-id="ff6cc-196">Le utilità di DFU devono essere eseguite da una casella DOS dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-196">The DFU utilities must be run from a DOS box at the command line.</span></span>

<span data-ttu-id="ff6cc-197">Digitare prima di tutto il comando **dfu-util – l** per determinare se il dispositivo è elencato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-197">First, type the command **dfu-util –l** to determine whether the device is listed.</span></span> <span data-ttu-id="ff6cc-198">In caso contrario, eseguire Zadig per verificare che il dispositivo sia elencato e associato alla libreria USB.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-198">If not, run Zadig to make sure the device is listed and associated with the USB library.</span></span> <span data-ttu-id="ff6cc-199">Verrà visualizzata una schermata come segue:</span><span class="sxs-lookup"><span data-stu-id="ff6cc-199">You should see a screen as follows:</span></span>

```Command-line
C:\usb specs\DFU\dfu-util-0.6&gt;dfu-util -l dfu-util 0.6

Copyright 2005-2008 Weston Schmidt, Harald Welte and OpenMoko Inc.
Copyright 2010-2012 Tormod Volden and Stefan Schmidt
This program is Free Software and has ABSOLUTELY NO WARRANTY
Found Runtime: [0a5c:21bc] devnum=0, cfg=1, intf=3, alt=0, name="UNDEFINED"
```

<span data-ttu-id="ff6cc-200">Il passaggio successivo consiste nel preparare il file da scaricare.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-200">The next step will be to prepare the file to be downloaded.</span></span> <span data-ttu-id="ff6cc-201">La classe USBX DFU non esegue alcuna verifica su questo file ed è indipendente dal formato interno.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-201">The USBX DFU class does not perform any verification on this file and is agnostic of its internal format.</span></span> <span data-ttu-id="ff6cc-202">Questo file del firmware è molto specifico per la destinazione ma non per DFU né per USBX.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-202">This firmware file is very specific to the target but not to DFU nor to USBX.</span></span>

<span data-ttu-id="ff6cc-203">A questo punto, è possibile indicare a dfu-util di inviare il file digitando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ff6cc-203">Then the dfu-util can be instructed to send the file by typing the following command:</span></span>

```Command-line
dfu-util –R –t 64 -D file_to_download.hex
```

<span data-ttu-id="ff6cc-204">In dfu-util dovrebbe essere visualizzato il processo di download del file fino a quando il firmware non è stato completamente scaricato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-204">The dfu-util should display the file download process until the firmware has been completely downloaded.</span></span>

## <a name="usb-device-pima-class-ptp-responder"></a><span data-ttu-id="ff6cc-205">Classe PIMA del dispositivo USB (risponditore PTP)</span><span class="sxs-lookup"><span data-stu-id="ff6cc-205">USB Device PIMA Class (PTP Responder)</span></span>

<span data-ttu-id="ff6cc-206">La classe PIMA del dispositivo USB consente a un sistema host USB (initiator) di connettersi a un</span><span class="sxs-lookup"><span data-stu-id="ff6cc-206">The USB device PIMA class allows for a USB host system (Initiator) to connect to a</span></span>

<span data-ttu-id="ff6cc-207">Dispositivo PIMA (resonder) per trasferire i file multimediali.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-207">PIMA device (Resonder) to transfer media files.</span></span> <span data-ttu-id="ff6cc-208">La classe Pima USBX è conforme alla classe USB-IF PIMA 15740, nota anche come classe PTP (per il protocollo di trasferimento immagini).</span><span class="sxs-lookup"><span data-stu-id="ff6cc-208">USBX Pima Class is conforming to the USB-IF PIMA 15740 class also known as PTP class (for Picture Transfer Protocol).</span></span>

<span data-ttu-id="ff6cc-209">La classe PIMA del lato dispositivo USBX supporta le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-209">USBX device side PIMA class supports the following operations.</span></span>

| <span data-ttu-id="ff6cc-210">Codice operativo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-210">Operation code</span></span>                                    | <span data-ttu-id="ff6cc-211">Valore</span><span class="sxs-lookup"><span data-stu-id="ff6cc-211">Value</span></span> | <span data-ttu-id="ff6cc-212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-212">Description</span></span>                       |
|---------------------------------------------------|---------|-----------------------------------------------------|
| <span data-ttu-id="ff6cc-213">UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO</span><span class="sxs-lookup"><span data-stu-id="ff6cc-213">UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO</span></span>    | <span data-ttu-id="ff6cc-214">0x1001</span><span class="sxs-lookup"><span data-stu-id="ff6cc-214">0x1001</span></span>  | <span data-ttu-id="ff6cc-215">Ottenere le operazioni e gli eventi supportati dal dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-215">Obtain the device supported operations and events</span></span>                                                         |
| <span data-ttu-id="ff6cc-216">UX_DEVICE_CLASS_PIMA_OC_OPEN_SESSION</span><span class="sxs-lookup"><span data-stu-id="ff6cc-216">UX_DEVICE_CLASS_PIMA_OC_OPEN_SESSION</span></span>        | <span data-ttu-id="ff6cc-217">0x1002</span><span class="sxs-lookup"><span data-stu-id="ff6cc-217">0x1002</span></span>  | <span data-ttu-id="ff6cc-218">Aprire una sessione tra l'host e il dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-218">Open a session between the host and the device</span></span>                                                            |
| <span data-ttu-id="ff6cc-219">UX_DEVICE_CLASS_PIMA_OC_CLOSE_SESSION</span><span class="sxs-lookup"><span data-stu-id="ff6cc-219">UX_DEVICE_CLASS_PIMA_OC_CLOSE_SESSION</span></span>       | <span data-ttu-id="ff6cc-220">0x1003</span><span class="sxs-lookup"><span data-stu-id="ff6cc-220">0x1003</span></span>  | <span data-ttu-id="ff6cc-221">Chiudere una sessione tra l'host e il dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-221">Close a session between the host and the device</span></span>                                                           |
| <span data-ttu-id="ff6cc-222">UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_IDS</span><span class="sxs-lookup"><span data-stu-id="ff6cc-222">UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_IDS</span></span>    | <span data-ttu-id="ff6cc-223">0x1004</span><span class="sxs-lookup"><span data-stu-id="ff6cc-223">0x1004</span></span>  | <span data-ttu-id="ff6cc-224">Restituisce l'ID di archiviazione per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-224">Returns the storage ID for the device.</span></span> <span data-ttu-id="ff6cc-225">USBX PIMA usa solo un ID archiviazione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-225">USBX PIMA uses one storage ID only</span></span> |
| <span data-ttu-id="ff6cc-226">UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_INFO</span><span class="sxs-lookup"><span data-stu-id="ff6cc-226">UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_INFO</span></span>   | <span data-ttu-id="ff6cc-227">0x1005</span><span class="sxs-lookup"><span data-stu-id="ff6cc-227">0x1005</span></span>  | <span data-ttu-id="ff6cc-228">Restituisce informazioni sull'oggetto di archiviazione, ad esempio la capacità massima e lo spazio libero</span><span class="sxs-lookup"><span data-stu-id="ff6cc-228">Return information about the storage object such as max capacity and free space</span></span>                           |
| <span data-ttu-id="ff6cc-229">UX_DEVICE_CLASS_PIMA_OC_GET_NUM_OBJECTS</span><span class="sxs-lookup"><span data-stu-id="ff6cc-229">UX_DEVICE_CLASS_PIMA_OC_GET_NUM_OBJECTS</span></span>    | <span data-ttu-id="ff6cc-230">0x1006</span><span class="sxs-lookup"><span data-stu-id="ff6cc-230">0x1006</span></span>  | <span data-ttu-id="ff6cc-231">Restituisce il numero di oggetti contenuti nel dispositivo di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-231">Return the number of objects contained in the storage device</span></span>                                              |
| <span data-ttu-id="ff6cc-232">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_HANDLES</span><span class="sxs-lookup"><span data-stu-id="ff6cc-232">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_HANDLES</span></span> | <span data-ttu-id="ff6cc-233">0x1007</span><span class="sxs-lookup"><span data-stu-id="ff6cc-233">0x1007</span></span>  | <span data-ttu-id="ff6cc-234">Restituisce una matrice di handle degli oggetti nel dispositivo di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-234">Return an array of handles of the objects on the storage device</span></span>                                           |
| <span data-ttu-id="ff6cc-235">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_INFO</span><span class="sxs-lookup"><span data-stu-id="ff6cc-235">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_INFO</span></span>    | <span data-ttu-id="ff6cc-236">0x1008</span><span class="sxs-lookup"><span data-stu-id="ff6cc-236">0x1008</span></span>  | <span data-ttu-id="ff6cc-237">Restituisce informazioni su un oggetto, ad esempio il nome dell'oggetto, la data di creazione, la data di modifica</span><span class="sxs-lookup"><span data-stu-id="ff6cc-237">Return information about an object such as the name of the object, its creation date, modification date</span></span> |
| <span data-ttu-id="ff6cc-238">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="ff6cc-238">UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT</span></span>          | <span data-ttu-id="ff6cc-239">0x1009</span><span class="sxs-lookup"><span data-stu-id="ff6cc-239">0x1009</span></span>  | <span data-ttu-id="ff6cc-240">Restituisce i dati relativi a un oggetto specifico</span><span class="sxs-lookup"><span data-stu-id="ff6cc-240">Return the data pertaining to a specific object</span></span>                                                         |
| <span data-ttu-id="ff6cc-241">UX_DEVICE_CLASS_PIMA_OC_GET_THUMB</span><span class="sxs-lookup"><span data-stu-id="ff6cc-241">UX_DEVICE_CLASS_PIMA_OC_GET_THUMB</span></span>           | <span data-ttu-id="ff6cc-242">0x100A</span><span class="sxs-lookup"><span data-stu-id="ff6cc-242">0x100A</span></span>  | <span data-ttu-id="ff6cc-243">Invia l'anteprima se disponibile per un oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-243">Send the thumbnail if available about an object</span></span>                                                           |
| <span data-ttu-id="ff6cc-244">UX_DEVICE_CLASS_PIMA_OC_DELETE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="ff6cc-244">UX_DEVICE_CLASS_PIMA_OC_DELETE_OBJECT</span></span>       | <span data-ttu-id="ff6cc-245">0x100B</span><span class="sxs-lookup"><span data-stu-id="ff6cc-245">0x100B</span></span>  | <span data-ttu-id="ff6cc-246">Eliminare un oggetto nel supporto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-246">Delete an object on the media</span></span>                                                                             |
| <span data-ttu-id="ff6cc-247">UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT_INFO</span><span class="sxs-lookup"><span data-stu-id="ff6cc-247">UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT_INFO</span></span>   | <span data-ttu-id="ff6cc-248">0x100C</span><span class="sxs-lookup"><span data-stu-id="ff6cc-248">0x100C</span></span>  | <span data-ttu-id="ff6cc-249">Invia alle informazioni sul dispositivo relative a un oggetto per la creazione sul supporto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-249">Send to the device information about an object for its creation on the media</span></span>                              |
| <span data-ttu-id="ff6cc-250">UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT</span><span class="sxs-lookup"><span data-stu-id="ff6cc-250">UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT</span></span>         | <span data-ttu-id="ff6cc-251">0x100D</span><span class="sxs-lookup"><span data-stu-id="ff6cc-251">0x100D</span></span>  | <span data-ttu-id="ff6cc-252">Inviare i dati per un oggetto al dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-252">Send data for an object to the device</span></span>                                                                     |
| <span data-ttu-id="ff6cc-253">UX_DEVICE_CLASS_PIMA_OC_FORMAT_STORE</span><span class="sxs-lookup"><span data-stu-id="ff6cc-253">UX_DEVICE_CLASS_PIMA_OC_FORMAT_STORE</span></span>        | <span data-ttu-id="ff6cc-254">0x100F</span><span class="sxs-lookup"><span data-stu-id="ff6cc-254">0x100F</span></span>  | <span data-ttu-id="ff6cc-255">Pulire i supporti del dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-255">Clean the device media</span></span>                                                                                    |
| <span data-ttu-id="ff6cc-256">UX_DEVICE_CLASS_PIMA_OC_RESET_DEVICE</span><span class="sxs-lookup"><span data-stu-id="ff6cc-256">UX_DEVICE_CLASS_PIMA_OC_RESET_DEVICE</span></span>        | <span data-ttu-id="ff6cc-257">0x0110</span><span class="sxs-lookup"><span data-stu-id="ff6cc-257">0x0110</span></span>  | <span data-ttu-id="ff6cc-258">Reimpostare il dispositivo di destinazione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-258">Reset the target device</span></span>                                                                                   |

| <span data-ttu-id="ff6cc-259">Codice operativo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-259">Operation Code</span></span>                                         | <span data-ttu-id="ff6cc-260">Valore</span><span class="sxs-lookup"><span data-stu-id="ff6cc-260">Value</span></span> | <span data-ttu-id="ff6cc-261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-261">Description</span></span> |
|--------------------------------------------------------|-------|-----------------------------------------|
| <span data-ttu-id="ff6cc-262">UX_DEVICE_CLASS_PIMA_EC_CANCEL_TRANSACTION</span><span class="sxs-lookup"><span data-stu-id="ff6cc-262">UX_DEVICE_CLASS_PIMA_EC_CANCEL_TRANSACTION</span></span>       | <span data-ttu-id="ff6cc-263">0x4001</span><span class="sxs-lookup"><span data-stu-id="ff6cc-263">0x4001</span></span>  | <span data-ttu-id="ff6cc-264">Annulla la transazione corrente</span><span class="sxs-lookup"><span data-stu-id="ff6cc-264">Cancels the current transaction</span></span>                                                 |
| <span data-ttu-id="ff6cc-265">UX_DEVICE_CLASS_PIMA_EC_OBJECT_ADDED</span><span class="sxs-lookup"><span data-stu-id="ff6cc-265">UX_DEVICE_CLASS_PIMA_EC_OBJECT_ADDED</span></span>             | <span data-ttu-id="ff6cc-266">0x4002</span><span class="sxs-lookup"><span data-stu-id="ff6cc-266">0x4002</span></span>  | <span data-ttu-id="ff6cc-267">Un oggetto è stato aggiunto al supporto del dispositivo e può essere recuperato da host\.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-267">An object has been added to the device media and can be retrieved by the host\.</span></span> |
| <span data-ttu-id="ff6cc-268">UX_DEVICE_CLASS_PIMA_EC_OBJECT_REMOVED</span><span class="sxs-lookup"><span data-stu-id="ff6cc-268">UX_DEVICE_CLASS_PIMA_EC_OBJECT_REMOVED</span></span>           | <span data-ttu-id="ff6cc-269">0x4003</span><span class="sxs-lookup"><span data-stu-id="ff6cc-269">0x4003</span></span>  | <span data-ttu-id="ff6cc-270">Un oggetto è stato eliminato dal supporto del dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-270">An object has been deleted from the device media</span></span>                                |
| <span data-ttu-id="ff6cc-271">UX_DEVICE_CLASS_PIMA_EC_STORE_ADDED</span><span class="sxs-lookup"><span data-stu-id="ff6cc-271">UX_DEVICE_CLASS_PIMA_EC_STORE_ADDED</span></span>              | <span data-ttu-id="ff6cc-272">0x4004</span><span class="sxs-lookup"><span data-stu-id="ff6cc-272">0x4004</span></span>  | <span data-ttu-id="ff6cc-273">È stato aggiunto un supporto al dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-273">A media has been added to the device</span></span>                                            |
| <span data-ttu-id="ff6cc-274">UX_DEVICE_CLASS_PIMA_EC_STORE_REMOVED</span><span class="sxs-lookup"><span data-stu-id="ff6cc-274">UX_DEVICE_CLASS_PIMA_EC_STORE_REMOVED</span></span>            | <span data-ttu-id="ff6cc-275">0x4005</span><span class="sxs-lookup"><span data-stu-id="ff6cc-275">0x4005</span></span>  | <span data-ttu-id="ff6cc-276">Un supporto è stato eliminato dal dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-276">A media has been deleted from the device</span></span>                                        |
| <span data-ttu-id="ff6cc-277">UX_DEVICE_CLASS_PIMA_EC_DEVICE_PROP_CHANGED</span><span class="sxs-lookup"><span data-stu-id="ff6cc-277">UX_DEVICE_CLASS_PIMA_EC_DEVICE_PROP_CHANGED</span></span>     | <span data-ttu-id="ff6cc-278">0x4006</span><span class="sxs-lookup"><span data-stu-id="ff6cc-278">0x4006</span></span>  | <span data-ttu-id="ff6cc-279">Le proprietà del dispositivo sono state modificate</span><span class="sxs-lookup"><span data-stu-id="ff6cc-279">Device properties have changed</span></span>                                                  |
| <span data-ttu-id="ff6cc-280">UX_DEVICE_CLASS_PIMA_EC_OBJECT_INFO_CHANGED</span><span class="sxs-lookup"><span data-stu-id="ff6cc-280">UX_DEVICE_CLASS_PIMA_EC_OBJECT_INFO_CHANGED</span></span>     | <span data-ttu-id="ff6cc-281">0x4007</span><span class="sxs-lookup"><span data-stu-id="ff6cc-281">0x4007</span></span>  | <span data-ttu-id="ff6cc-282">Sono state modificate informazioni sugli oggetti</span><span class="sxs-lookup"><span data-stu-id="ff6cc-282">An object information has changed</span></span>                                               |
| <span data-ttu-id="ff6cc-283">UX_DEVICE_CLASS_PIMA_EC_DEVICE_INFO_CHANGE</span><span class="sxs-lookup"><span data-stu-id="ff6cc-283">UX_DEVICE_CLASS_PIMA_EC_DEVICE_INFO_CHANGE</span></span>      | <span data-ttu-id="ff6cc-284">0x4008</span><span class="sxs-lookup"><span data-stu-id="ff6cc-284">0x4008</span></span>  | <span data-ttu-id="ff6cc-285">Un dispositivo è stato modificato</span><span class="sxs-lookup"><span data-stu-id="ff6cc-285">A device has changed</span></span>                                                            |
| <span data-ttu-id="ff6cc-286">UX_DEVICE_CLASS_PIMA_EC_REQUEST_OBJECT_TRANSFER</span><span class="sxs-lookup"><span data-stu-id="ff6cc-286">UX_DEVICE_CLASS_PIMA_EC_REQUEST_OBJECT_TRANSFER</span></span> | <span data-ttu-id="ff6cc-287">0x4009</span><span class="sxs-lookup"><span data-stu-id="ff6cc-287">0x4009</span></span>  | <span data-ttu-id="ff6cc-288">Il dispositivo richiede il trasferimento di un oggetto dall'host</span><span class="sxs-lookup"><span data-stu-id="ff6cc-288">The device requests the transfer of an object from the host</span></span>                     |
| <span data-ttu-id="ff6cc-289">UX_DEVICE_CLASS_PIMA_EC_STORE_FULL</span><span class="sxs-lookup"><span data-stu-id="ff6cc-289">UX_DEVICE_CLASS_PIMA_EC_STORE_FULL</span></span>               | <span data-ttu-id="ff6cc-290">0x400A</span><span class="sxs-lookup"><span data-stu-id="ff6cc-290">0x400A</span></span>  | <span data-ttu-id="ff6cc-291">Il dispositivo segnala il supporto completo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-291">Device reports the media is full</span></span>                                                |
| <span data-ttu-id="ff6cc-292">UX_DEVICE_CLASS_PIMA_EC_DEVICE_RESET</span><span class="sxs-lookup"><span data-stu-id="ff6cc-292">UX_DEVICE_CLASS_PIMA_EC_DEVICE_RESET</span></span>             | <span data-ttu-id="ff6cc-293">0x400B</span><span class="sxs-lookup"><span data-stu-id="ff6cc-293">0x400B</span></span>  | <span data-ttu-id="ff6cc-294">Report del dispositivo reimpostato</span><span class="sxs-lookup"><span data-stu-id="ff6cc-294">Device reports it was reset</span></span>                                                     |
| <span data-ttu-id="ff6cc-295">UX_DEVICE_CLASS_PIMA_EC_STORAGE_INFO_CHANGED</span><span class="sxs-lookup"><span data-stu-id="ff6cc-295">UX_DEVICE_CLASS_PIMA_EC_STORAGE_INFO_CHANGED</span></span>    | <span data-ttu-id="ff6cc-296">0x400C</span><span class="sxs-lookup"><span data-stu-id="ff6cc-296">0x400C</span></span>  | <span data-ttu-id="ff6cc-297">Le informazioni di archiviazione sono state modificate nel dispositivo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-297">Storage information has changed on the device</span></span>                                   |
| <span data-ttu-id="ff6cc-298">UX_DEVICE_CLASS_PIMA_EC_CAPTURE_COMPLETE</span><span class="sxs-lookup"><span data-stu-id="ff6cc-298">UX_DEVICE_CLASS_PIMA_EC_CAPTURE_COMPLETE</span></span>         | <span data-ttu-id="ff6cc-299">0x400D</span><span class="sxs-lookup"><span data-stu-id="ff6cc-299">0x400D</span></span>  | <span data-ttu-id="ff6cc-300">Acquisizione completata</span><span class="sxs-lookup"><span data-stu-id="ff6cc-300">Capture is completed</span></span>                                                            |

<span data-ttu-id="ff6cc-301">La classe di dispositivi USBX PIMA usa un thread TX per ascoltare i comandi PIMA dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-301">The USBX PIMA device class uses a TX Thread to listen to PIMA commands from the host.</span></span>

<span data-ttu-id="ff6cc-302">Un comando PIMA è costituito da un blocco di comandi, da un blocco di dati e da una fase di stato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-302">A PIMA command is composed of a command block, a data block and a status phase.</span></span>

<span data-ttu-id="ff6cc-303">La funzione ux_device_class_pima_thread invia una richiesta allo stack per ricevere un comando PIMA dal lato host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-303">The function ux_device_class_pima_thread posts a request to the stack to receive a PIMA command from the host side.</span></span> <span data-ttu-id="ff6cc-304">Il comando PIMA viene decodificato e verificato per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-304">The PIMA command is decoded and verified for content.</span></span> <span data-ttu-id="ff6cc-305">Se il blocco di comandi è valido, viene diramato al gestore del comando appropriato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-305">If the command block is valid, it branches to the appropriate command handler.</span></span>

<span data-ttu-id="ff6cc-306">La maggior parte dei comandi PIMA può essere eseguita solo quando una sessione è stata aperta dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-306">Most PIMA commands can only be executed when a session has been opened by the host.</span></span> <span data-ttu-id="ff6cc-307">L'unica eccezione è rappresentata dal comando **UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO**.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-307">The only exception is the command **UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO**.</span></span> <span data-ttu-id="ff6cc-308">Con l'implementazione di USBX PIMA, è possibile aprire una sola sessione tra un iniziatore e un risponditore in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-308">With USBX PIMA implementation, only one session can be opened between an Initiator and Responder at any time.</span></span> <span data-ttu-id="ff6cc-309">Tutte le transazioni all'interno della singola sessione sono bloccate e non è possibile avviare alcuna nuova transazione prima del completamento di quella precedente.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-309">All transactions within the single session are blocking and no new transaction can begin before the previous one completed.</span></span>

<span data-ttu-id="ff6cc-310">Le transazioni PIMA sono costituite da 3 fasi, una fase di comando, una fase di dati facoltativa e una fase di risposta.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-310">PIMA transactions are composed of 3 phases, a command phase, an optional data phase and a response phase.</span></span> <span data-ttu-id="ff6cc-311">Se è presente una fase di dati, può essere presente solo in una direzione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-311">If a data phase is present, it can only be in one direction.</span></span>

<span data-ttu-id="ff6cc-312">L'iniziatore determina sempre il flusso delle operazioni PIMA, ma il risponditore può avviare gli eventi all'initiator per informare le modifiche di stato che si sono verificate durante una sessione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-312">The Initiator always determines the flow of the PIMA operations but the Responder can initiate events back to the Initiator to inform status changes that happened during a session.</span></span>

<span data-ttu-id="ff6cc-313">Il diagramma seguente illustra il trasferimento di un oggetto dati tra l'host e la classe di dispositivi PIMA.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-313">The following diagram shows the transfer of a data object between the host and the PIMA device class.</span></span>

![Transazioni PIMA](./media/usbx-device-stack-supplemental/pima-transactions.png)

## <a name="initialization-of-the-pima-device-class"></a><span data-ttu-id="ff6cc-315">Inizializzazione della classe di dispositivi PIMA</span><span class="sxs-lookup"><span data-stu-id="ff6cc-315">Initialization of the PIMA device class</span></span>

<span data-ttu-id="ff6cc-316">Per la classe di dispositivi PIMA sono necessari alcuni parametri forniti dall'applicazione durante l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-316">The PIMA device class needs some parameters supplied by the application during the initialization.</span></span>

<span data-ttu-id="ff6cc-317">I parametri seguenti descrivono le informazioni sul dispositivo e sull'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-317">The following parameters describe the device and storage information.</span></span>

- `ux_device_class_pima_manufacturer`
- `ux_device_class_pima_model`
- `ux_device_class_pima_device_version`
- `ux_device_class_pima_serial_number`
- `ux_device_class_pima_storage_id`
- `ux_device_class_pima_storage_type`
- `ux_device_class_pima_storage_file_system_type`
- `ux_device_class_pima_storage_access_capability`
- `ux_device_class_pima_storage_max_capacity_low`
- `ux_device_class_pima_storage_max_capacity_high`
- `ux_device_class_pima_storage_free_space_low`
- `ux_device_class_pima_storage_free_space_high`
- `ux_device_class_pima_storage_free_space_image`
- `ux_device_class_pima_storage_description`
- `ux_device_class_pima_storage_volume_label`

<span data-ttu-id="ff6cc-318">La classe PIMA richiede anche la registrazione del callback nell'applicazione per informare l'applicazione di determinati eventi oppure recuperare/archiviare i dati da e verso i supporti locali.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-318">The PIMA class also requires the registration of callback into the application to inform the application of certain events or retrieve/store data from/to the local media.</span></span> <span data-ttu-id="ff6cc-319">I callback sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-319">The callbacks are as follows.</span></span>

- `ux_device_class_pima_object_number_get`
- `ux_device_class_pima_object_handles_get`
- `ux_device_class_pima_object_info_get`
- `ux_device_class_pima_object_data_get`
- `ux_device_class_pima_object_info_send`
- `ux_device_class_pima_object_data_send`
- `ux_device_class_pima_object_delete`

<span data-ttu-id="ff6cc-320">Nell'esempio seguente viene illustrato come inizializzare il lato client di PIMA.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-320">The following example shows how to initialize the client side of PIMA.</span></span> <span data-ttu-id="ff6cc-321">Questo esempio USA PictBridge come client per PIMA.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-321">This example uses Pictbridge as a client for PIMA.</span></span>

```C
/* Initialize the first XML object valid in the pictbridge instance.

Initialize the handle, type and file name.

The storage handle and the object handle have a fixed value of 1 in our implementation. */

object_info = pictbridge -> ux_pictbridge_object_client;

object_info -> ux_device_class_pima_object_format = UX_DEVICE_CLASS_PIMA_OFC_SCRIPT;
object_info -> ux_device_class_pima_object_storage_id = 1;
object_info -> ux_device_class_pima_object_handle_id = 2;

ux_utility_string_to_unicode(_ux_pictbridge_ddiscovery_name,
    object_info -> ux_device_class_pima_object_filename);

/* Initialize the head and tail of the notification round robin buffers.
   At first, the head and tail are pointing to the beginning of the array.
*/

pictbridge -> ux_pictbridge_event_array_head =
    pictbridge -> ux_pictbridge_event_array;

pictbridge -> ux_pictbridge_event_array_tail =
    pictbridge -> ux_pictbridge_event_array;

pictbridge -> ux_pictbridge_event_array_end =
    pictbridge -> ux_pictbridge_event_array +
    UX_PICTBRIDGE_MAX_EVENT_NUMBER;

/* Initialialize the pima device parameter. */
pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_manufacturer =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_model =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_serial_number =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_id = 1;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_type =
    UX_DEVICE_CLASS_PIMA_STC_FIXED_RAM;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_file_system_type =
    UX_DEVICE_CLASS_PIMA_FSTC_GENERIC_FLAT;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_access_capability =
    UX_DEVICE_CLASS_PIMA_AC_READ_WRITE;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_max_capacity_low =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_storage_size;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_max_capacity_high = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_low =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_storage_size;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_high = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_image = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_description =
    _ux_pictbridge_volume_description;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_volume_label =
    _ux_pictbridge_volume_label;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_number_get =
    ux_pictbridge_dpsclient_object_number_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_handles_get =
    ux_pictbridge_dpsclient_object_handles_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_info_get =
    ux_pictbridge_dpsclient_object_info_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_data_get =
    ux_pictbridge_dpsclient_object_data_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_info_send =
    ux_pictbridge_dpsclient_object_info_send;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_data_send =
    ux_pictbridge_dpsclient_object_data_send;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_delete =
    ux_pictbridge_dpsclient_object_delete;

/* Store the instance owner. */
pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_application =
    (VOID *) pictbridge;

/* Initialize the device pima class. The class is connected with interface 0 */

status = ux_device_stack_class_register(_ux_system_slave_class_pima_name,
    ux_device_class_pima_entry, 1, 0, (VOID *)&pictbridge -> ux_pictbridge_pima_parameter);

/* Check status. */
if (status != UX_SUCCESS)
```

## <a name="ux_device_class_pima_object_add"></a><span data-ttu-id="ff6cc-322">ux_device_class_pima_object_add</span><span class="sxs-lookup"><span data-stu-id="ff6cc-322">ux_device_class_pima_object_add</span></span>

<span data-ttu-id="ff6cc-323">Aggiunta di un oggetto e invio dell'evento all'host</span><span class="sxs-lookup"><span data-stu-id="ff6cc-323">Adding an object and sending the event to the host</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-324">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-324">Prototype</span></span>

```C
UINT ux_device_class_pima_object_add(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG object_handle);
```

### <a name="description"></a><span data-ttu-id="ff6cc-325">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-325">Description</span></span>

<span data-ttu-id="ff6cc-326">Questa funzione viene chiamata quando la classe PIMA deve aggiungere un oggetto e informare l'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-326">This function is called when the PIMA class needs to add an object and inform the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-327">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-327">Parameters</span></span>

- <span data-ttu-id="ff6cc-328">**Pima**: puntatore all'istanza della classe Pima</span><span class="sxs-lookup"><span data-stu-id="ff6cc-328">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="ff6cc-329">**object_handle**: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-329">**object_handle**: Handle of the object.</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-330">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-330">Example</span></span>

```C
/* Send the notification to the host that an object has been added. */

status = ux_device_class_pima_object_add(pima, UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST);
```

## <a name="ux_device_class_pima_object_number_get"></a><span data-ttu-id="ff6cc-331">ux_device_class_pima_object_number_get</span><span class="sxs-lookup"><span data-stu-id="ff6cc-331">ux_device_class_pima_object_number_get</span></span>

<span data-ttu-id="ff6cc-332">Recupero del numero di oggetto dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-332">Getting the object number from the application</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-333">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-333">Prototype</span></span>

```C
UINT ux_device_class_pima_object_number_get(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG *object_number);
```

### <a name="description"></a><span data-ttu-id="ff6cc-334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-334">Description</span></span>

<span data-ttu-id="ff6cc-335">Questa funzione viene chiamata quando la classe PIMA deve recuperare il numero di oggetti nel sistema locale e inviarlo di nuovo all'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-335">This function is called when the PIMA class needs to retrieve the number of objects in the local system and send it back to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-336">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-336">Parameters</span></span>

- <span data-ttu-id="ff6cc-337">**Pima**: puntatore all'istanza della classe Pima</span><span class="sxs-lookup"><span data-stu-id="ff6cc-337">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="ff6cc-338">**object_number**: indirizzo del numero di oggetti da restituire</span><span class="sxs-lookup"><span data-stu-id="ff6cc-338">**object_number**: Address of the number of objects to be returned</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-339">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-339">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_number_get(UX_SLAVE_CLASS_PIMA *pima, ULONG *number_objects)
{
    /* We force the number of objects to be 1 only here. This will be the XML scripts. */
    *number_objects = 1;
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_handles_get"></a><span data-ttu-id="ff6cc-340">ux_device_class_pima_object_handles_get</span><span class="sxs-lookup"><span data-stu-id="ff6cc-340">ux_device_class_pima_object_handles_get</span></span>

<span data-ttu-id="ff6cc-341">Restituisce la matrice dell'handle di oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-341">Return the object handle array</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-342">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-342">Prototype</span></span>

```C
UINT **ux_device_class_pima_object_handles_get**(
    UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number);
```

### <a name="description"></a><span data-ttu-id="ff6cc-343">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-343">Description</span></span>

<span data-ttu-id="ff6cc-344">Questa funzione viene chiamata quando la classe PIMA deve recuperare l'oggetto che gestisce la matrice nel sistema locale e lo invia nuovamente all'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-344">This function is called when the PIMA class needs to retrieve the object handles array in the local system and send it back to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-345">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-345">Parameters</span></span>

- <span data-ttu-id="ff6cc-346">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-346">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="ff6cc-347">**object_handles_format_code**: formattare il codice per gli handle</span><span class="sxs-lookup"><span data-stu-id="ff6cc-347">**object_handles_format_code**: Format code for the handles</span></span>
- <span data-ttu-id="ff6cc-348">**object_handles_association**: codice di associazione di oggetti</span><span class="sxs-lookup"><span data-stu-id="ff6cc-348">**object_handles_association**: Object association code</span></span>
- <span data-ttu-id="ff6cc-349">**object_handle_array**: indirizzo in cui archiviare gli handle</span><span class="sxs-lookup"><span data-stu-id="ff6cc-349">**object_handle_array**: Address where to store the handles</span></span>
- <span data-ttu-id="ff6cc-350">**object_handles_max_number**: numero massimo di handle nella matrice</span><span class="sxs-lookup"><span data-stu-id="ff6cc-350">**object_handles_max_number**: Maximum number of handles in the array</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-351">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-351">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_handles_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number)
{

    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *) pima -> ux_device_class_pima_application;

    /* Set the pima pointer to the pictbridge instance. */
    pictbridge -> ux_pictbridge_pima = (VOID *) pima;

    /* We say we have one object but the caller might specify different format code and associations. */
    object_info = pictbridge -> ux_pictbridge_object_client;

    /* Insert in the array the number of found handles so far: 0. */
    ux_utility_long_put((UCHAR *)object_handles_array, 0);

    /* Check the type demanded. */

    if (object_handles_format_code == 0 || object_handles_format_code ==
        0xFFFFFFFF || object_info -> ux_device_class_pima_object_format ==
        object_handles_format_code)
    {
        /* Insert in the array the number of found handles. This handle is for the client XML script. */
        ux_utility_long_put((UCHAR *)object_handles_array, 1);

        /* Adjust the array to point after the number of elements. */
        object_handles_array++;

        /* We have a candicate. Store the handle. */
        ux_utility_long_put((UCHAR *)object_handles_array, object_info ->
            ux_device_class_pima_object_handle_id);
    }

    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_info_get"></a><span data-ttu-id="ff6cc-352">ux_device_class_pima_object_info_get</span><span class="sxs-lookup"><span data-stu-id="ff6cc-352">ux_device_class_pima_object_info_get</span></span>

<span data-ttu-id="ff6cc-353">Restituisce le informazioni sull'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-353">Return the object information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-354">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-354">Prototype</span></span>

```C
UINT ux_device_class_pima_object_info_get(
    struct UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handle, 
    UX_SLAVE_CLASS_PIMA_OBJECT **object);
```

### <a name="description"></a><span data-ttu-id="ff6cc-355">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-355">Description</span></span>

<span data-ttu-id="ff6cc-356">Questa funzione viene chiamata quando la classe PIMA deve recuperare l'oggetto che gestisce la matrice nel sistema locale e lo invia nuovamente all'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-356">This function is called when the PIMA class needs to retrieve the object handles array in the local system and send it back to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-357">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-357">Parameters</span></span>

- <span data-ttu-id="ff6cc-358">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-358">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="ff6cc-359">**object_handles**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-359">**object_handles**: Handle of the object</span></span>
- <span data-ttu-id="ff6cc-360">**oggetto**: Indirizzo puntatore oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-360">**object**: Object pointer address</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-361">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-361">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_info_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, UX_SLAVE_CLASS_PIMA_OBJECT **object)
{
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Check the object handle. If this is handle 1 or 2 , we need to return the XML script object.
       If the handle is not 1 or 2, this is a JPEG picture or other object to be printed. */
    if ((object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE) ||
        (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST)) {

        /* Check what XML object is requested. It is either a request script or a response. */
        if (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE)
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge -> ux_pictbridge_object_host;
        else
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_client;
    } else
        /* Get the object info from the job info structure. */
        object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
            ux_pictbridge_jobinfo.ux_pictbridge_jobinfo_object;
    /* Return the pointer to this object. */
    *object = object_info;

    /* We are done. */
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_data_get"></a><span data-ttu-id="ff6cc-362">ux_device_class_pima_object_data_get</span><span class="sxs-lookup"><span data-stu-id="ff6cc-362">ux_device_class_pima_object_data_get</span></span>

<span data-ttu-id="ff6cc-363">Restituisce i dati dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-363">Return the object data</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-364">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-364">Prototype</span></span>

```C
UINT ux_device_class_pima_object_info_get(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length_requested,
    ULONG *object_actual_length);
```

### <a name="description"></a><span data-ttu-id="ff6cc-365">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-365">Description</span></span>

<span data-ttu-id="ff6cc-366">Questa funzione viene chiamata quando la classe PIMA deve recuperare i dati dell'oggetto nel sistema locale e inviarli nuovamente all'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-366">This function is called when the PIMA class needs to retrieve the object data in the local system and send it back to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-367">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-367">Parameters</span></span>

- <span data-ttu-id="ff6cc-368">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-368">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="ff6cc-369">**object_handle**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-369">**object_handle**: Handle of the object</span></span>
- <span data-ttu-id="ff6cc-370">**object_buffer**: Indirizzo buffer oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-370">**object_buffer**: Object buffer address</span></span>
- <span data-ttu-id="ff6cc-371">**object_length_requested**: lunghezza dei dati dell'oggetto richiesta dal client all'applicazione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-371">**object_length_requested**: Object data length requested by the client to the application</span></span>
- <span data-ttu-id="ff6cc-372">**object_actual_length**: lunghezza dei dati dell'oggetto restituita dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-372">**object_actual_length**: Object data length returned by the application</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-373">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-373">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_data_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, UCHAR *object_buffer, ULONG object_offset,
    ULONG object_length_requested, ULONG *object_actual_length)
{

    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    UCHAR *pima_object_buffer;
    ULONG actual_length;
    UINT status;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Check the object handle. If this is handle 1 or 2 , we need to return the XML script object.
       If the handle is not 1 or 2, this is a JPEG picture or other object to be printed. */
    if ((object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE) ||
        (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST))
    {
        /* Check what XML object is requested. It is either a request script or a response. */
        if (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE)
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_host;
        else
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_client;

       /* Is this the corrent handle ? */
       if (object_info -> ux_device_class_pima_object_handle_id == object_handle)
       {
           /* Get the pointer to the object buffer. */
           pima_object_buffer = object_info -> ux_device_class_pima_object_buffer;

           /* Copy the demanded object data portion. */
           ux_utility_memory_copy(object_buffer, pima_object_buffer +
               object_offset, object_length_requested);

           /* Update the length requested. for a demo, we do not do any checking. */
           *object_actual_length = object_length_requested;

           /* What cycle are we in ? */
           if (pictbridge -> ux_pictbridge_host_client_state_machine &
               UX_PICTBRIDGE_STATE_MACHINE_HOST_REQUEST)
            {
                /* Check if we are blocking for a client request. */
                if (pictbridge -> ux_pictbridge_host_client_state_machine &
                    UX_PICTBRIDGE_STATE_MACHINE_CLIENT_REQUEST_PENDING)

                    /* Yes we are pending, send an event to release the pending request. */
                    ux_utility_event_flags_set(&pictbridge ->
                        ux_pictbridge_event_flags_group,
                        UX_PICTBRIDGE_EVENT_FLAG_STATE_MACHINE_READY, TX_OR);

               /* Since we are in host request, this indicates we are done with the cycle. */
               pictbridge -> ux_pictbridge_host_client_state_machine =
                   UX_PICTBRIDGE_STATE_MACHINE_IDLE;

            }

            /* We have copied the requested data. Return OK. */
            return(UX_SUCCESS);

        }
    }
    else
    {

        /* Get the object info from the job info structure. */
        object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
            ux_pictbridge_jobinfo.ux_pictbridge_jobinfo_object;

        /* Obtain the data from the application jobinfo callback. */
        status = pictbridge -> ux_pictbridge_jobinfo.
            ux_pictbridge_jobinfo_object_data_read(pictbridge, object_buffer, object_offset,
            object_length_requested, &actual_length);

        /* Save the length returned. */
        *object_actual_length = actual_length;

        /* Return the application status. */
        return(status);

    }

    /* Could not find the handle. */

    return(UX_DEVICE_CLASS_PIMA_RC_INVALID_OBJECT_HANDLE);
}
```

## <a name="ux_device_class_pima_object_info_send"></a><span data-ttu-id="ff6cc-374">ux_device_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="ff6cc-374">ux_device_class_pima_object_info_send</span></span>

<span data-ttu-id="ff6cc-375">L'host invia le informazioni sull'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-375">Host sends the object information</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-376">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-376">Prototype</span></span>

```C
UINT ux_device_class_pima_object_info_send(
    UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, 
    ULONG *object_handle);
```

### <a name="description"></a><span data-ttu-id="ff6cc-377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-377">Description</span></span>

<span data-ttu-id="ff6cc-378">Questa funzione viene chiamata quando la classe PIMA deve ricevere le informazioni sull'oggetto nel sistema locale per l'archiviazione futura.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-378">This function is called when the PIMA class needs to receive the object information in the local system for future storage.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-379">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-379">Parameters</span></span>

- <span data-ttu-id="ff6cc-380">**Pima**: puntatore all'istanza della classe Pima</span><span class="sxs-lookup"><span data-stu-id="ff6cc-380">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="ff6cc-381">**oggetto**: puntatore all'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-381">**object**:  Pointer to the object</span></span>
- <span data-ttu-id="ff6cc-382">**object_handle**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-382">**object_handle**: Handle of the object</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-383">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-383">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_info_send(UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, ULONG *object_handle)
{
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info; UCHAR
    string_discovery_name[UX_PICTBRIDGE_MAX_FILE_NAME_SIZE];

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* We only have one object. */
    object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
        ux_pictbridge_object_host;

    /* Copy the demanded object info set. */
    ux_utility_memory_copy(object_info, object,
        UX_SLAVE_CLASS_PIMA_OBJECT_DATA_LENGTH);

    /* Store the object handle. In Pictbridge we only receive XML scripts so the handle is hardwired to 1. */
    object_info -> ux_device_class_pima_object_handle_id = 1;
    *object_handle = 1;

    /* Check state machine. If we are in discovery pending mode, check file name of this object. */
    if (pictbridge -> ux_pictbridge_discovery_state ==
        UX_PICTBRIDGE_DPSCLIENT_DISCOVERY_PENDING)
    {
        /* We are in the discovery mode. Check for file name. It must match
           HDISCVRY.DPS in Unicode mode. */

        /* Check if this is a script. */
        if (object_info -> ux_device_class_pima_object_format ==
            UX_DEVICE_CLASS_PIMA_OFC_SCRIPT)
        {

            /* Yes this is a script. We need to search for the HDISCVRY.DPS file name. Get the file name in a ascii format. */
            ux_utility_unicode_to_string(object_info ->
                ux_device_class_pima_object_filename,
                string_discovery_name);

            /* Now, compare it to the HDISCVRY.DPS file name. Check length first. */
            if (ux_utility_string_length_get(_ux_pictbridge_hdiscovery_name)
                == ux_utility_string_length_get(string_discovery_name))
            {

                /* So far, the length of name of the files are the same. Compare names now. */
                if(ux_utility_memory_compare(_ux_pictbridge_hdiscovery_name,
                    string_discovery_name,
                    ux_utility_string_length_get(string_discovery_name)) == UX_SUCCESS)
                {
                    /* We are done with discovery of the printer. We can now send notifications when the camera wants to print an object. */
                    pictbridge -> ux_pictbridge_discovery_state =
                        UX_PICTBRIDGE_DPSCLIENT_DISCOVERY_COMPLETE;

                    /* Set an event flag if the application is listening. */
                    ux_utility_event_flags_set(&pictbridge ->
                        ux_pictbridge_event_flags_group,
                        UX_PICTBRIDGE_EVENT_FLAG_DISCOVERY, TX_OR);

                    /* There is no object during th discovery cycle. */
                    return(UX_SUCCESS);
                }
            }
        }
    }
    /* What cycle are we in ? */
    if (pictbridge -> ux_pictbridge_host_client_state_machine ==
        UX_PICTBRIDGE_STATE_MACHINE_IDLE)

        /* Since we are in idle state, we must have received a request from the host. */
        pictbridge -> ux_pictbridge_host_client_state_machine =
            UX_PICTBRIDGE_STATE_MACHINE_HOST_REQUEST;

    /* We have copied the requested data. Return OK. */
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_data_send"></a><span data-ttu-id="ff6cc-384">ux_device_class_pima_object_data_send</span><span class="sxs-lookup"><span data-stu-id="ff6cc-384">ux_device_class_pima_object_data_send</span></span>

<span data-ttu-id="ff6cc-385">L'host invia i dati dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-385">Host sends the object data</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-386">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-386">Prototype</span></span>

```C
UINT ux_device_class_pima_object_data_send(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, 
    ULONG phase, 
    UCHAR *object_buffer,
    ULONG object_offset, 
    ULONG object_length);
```

### <a name="description"></a><span data-ttu-id="ff6cc-387">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-387">Description</span></span>

<span data-ttu-id="ff6cc-388">Questa funzione viene chiamata quando la classe PIMA deve ricevere i dati dell'oggetto nel sistema locale per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-388">This function is called when the PIMA class needs to receive the object data in the local system for storage.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-389">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-389">Parameters</span></span>

- <span data-ttu-id="ff6cc-390">**Pima**: puntatore all'istanza della classe Pima</span><span class="sxs-lookup"><span data-stu-id="ff6cc-390">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="ff6cc-391">**object_handle**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-391">**object_handle**: Handle of the object</span></span>
- <span data-ttu-id="ff6cc-392">**fase**: fase del trasferimento (attiva o completa)</span><span class="sxs-lookup"><span data-stu-id="ff6cc-392">**phase**: phase of the transfer (active or complete)</span></span>
- <span data-ttu-id="ff6cc-393">**object_buffer**: Indirizzo buffer oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-393">**object_buffer**: Object buffer address</span></span>
- <span data-ttu-id="ff6cc-394">**object_offset**: indirizzo dei dati</span><span class="sxs-lookup"><span data-stu-id="ff6cc-394">**object_offset**: Address of data</span></span>
- <span data-ttu-id="ff6cc-395">**object_length**: lunghezza dei dati dell'oggetto inviata dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-395">**object_length**: Object data length sent by application</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-396">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-396">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_data_send(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle,
    ULONG phase,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length)
{
    UINT status;
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    ULONG event_flag;
    UCHAR *pima_object_buffer;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Get the pointer to the pima object. */
    object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
        ux_pictbridge_object_host;

    /* Is this the corrent handle ? */
    if (object_info -> ux_device_class_pima_object_handle_id == object_handle)
    {
        /* Get the pointer to the object buffer. */
        pima_object_buffer = object_info ->
            ux_device_class_pima_object_buffer;

        /* Check the phase. We should wait for the object to be completed and the response sent back before parsing the object. */
        if (phase == UX_DEVICE_CLASS_PIMA_OBJECT_TRANSFER_PHASE_ACTIVE)
        {
            /* Copy the demanded object data portion. */
            ux_utility_memory_copy(pima_object_buffer + object_offset,
                object_buffer, object_length);

            /* Save the length of this object. */
            object_info -> ux_device_class_pima_object_length = object_length;

            /* We are not done yet. */
            return(UX_SUCCESS);
        }
        else
        {
            /* Completion of transfer. We are done. */
            return(UX_SUCCESS);
        }
    }
}
```

## <a name="ux_device_class_pima_object_delete"></a><span data-ttu-id="ff6cc-397">ux_device_class_pima_object_delete</span><span class="sxs-lookup"><span data-stu-id="ff6cc-397">ux_device_class_pima_object_delete</span></span>

<span data-ttu-id="ff6cc-398">Eliminare un oggetto locale</span><span class="sxs-lookup"><span data-stu-id="ff6cc-398">Delete a local object</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-399">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-399">Prototype</span></span>

```C
UINT ux_device_class_pima_object_delete(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle);
```

### <a name="description"></a><span data-ttu-id="ff6cc-400">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-400">Description</span></span>

<span data-ttu-id="ff6cc-401">Questa funzione viene chiamata quando la classe PIMA deve eliminare un oggetto nella risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-401">This function is called when the PIMA class needs to delete an object on the local storage.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-402">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-402">Parameters</span></span>

- <span data-ttu-id="ff6cc-403">**Pima**: puntatore all'istanza della classe Pima</span><span class="sxs-lookup"><span data-stu-id="ff6cc-403">**pima**: Pointer to the pima class instance</span></span>
- <span data-ttu-id="ff6cc-404">**object_handle**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="ff6cc-404">**object_handle**: Handle of the object</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-405">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-405">Example</span></span>

```C
UINT ux_pictbridge_dpsclient_object_delete(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle)
{
    /* Delete the object pointer by the handle. */

}
```

## <a name="usb-device-audio-class"></a><span data-ttu-id="ff6cc-406">Classe audio dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="ff6cc-406">USB Device Audio Class</span></span>

<span data-ttu-id="ff6cc-407">La classe audio del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-407">The USB device Audio class allows for a USB host system to communicate with the device as an audio device.</span></span> <span data-ttu-id="ff6cc-408">Questa classe è basata sulla classe USB standard e sull'audio USB standard 1,0 o 2,0.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-408">This class is based on the USB standard and USB Audio Class 1.0 or 2.0 standard.</span></span>

<span data-ttu-id="ff6cc-409">Un Framework di dispositivi conformi all'audio USB deve essere dichiarato dallo stack del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-409">A USB audio compliant device framework needs to be declared by the device stack.</span></span> <span data-ttu-id="ff6cc-410">Di seguito è riportato un esempio di un altoparlante audio 2,0:</span><span class="sxs-lookup"><span data-stu-id="ff6cc-410">An example of an Audio 2.0 speaker follows:</span></span>

```C
unsigned char device_framework_high_speed[] = {

    /* --- Device Descriptor 18 bytes
    0x00 bDeviceClass: Refer to interface
    0x00 bDeviceSubclass: Refer to interface
    0x00 bDeviceProtocol: Refer to interface

    idVendor & idProduct - https://www.linux-usb.org/usb.ids
    */

    /* 0 bLength, bDescriptorType */ 18, 0x01,
    /* 2 bcdUSB : 0x200 (2.00) */ 0x00, 0x02,
    /* 4 bDeviceClass : 0x00 (see interface) */ 0x00,
    /* 5 bDeviceSubClass : 0x00 (see interface) */ 0x00,
    /* 6 bDeviceProtocol : 0x00 (see interface) */ 0x00,
    /* 7 bMaxPacketSize0 */ 0x08,
    /* 8 idVendor, idProduct */ 0x84, 0x84, 0x03, 0x00,
    /* 12 bcdDevice */ 0x00, 0x02,
    /* 14 iManufacturer, iProduct, iSerialNumber */ 0, 0, 0,
    /* 17 bNumConfigurations */ 1,
    /* ---------------- Device Qualifier Descriptor */
    /* 0 bLength, bDescriptorType */ 10, 0x06,
    /* 2 bcdUSB : 0x200 (2.00) */ 0x00,0x02,
    /* 4 bDeviceClass : 0x00 (see interface) */ 0x00,
    /* 5 bDeviceSubClass : 0x00 (see interface) */ 0x00,
    /* 6 bDeviceProtocol : 0x00 (see interface) */ 0x00,
    /* 7 bMaxPacketSize0 */ 8,
    /* 8 bNumConfigurations */ 1,
    /* 9 bReserved */ 0,
    /* --- Configuration Descriptor (9+8+73+55=145, 0x91) */
    /* 0 bLength, bDescriptorType */ 9, 0x02,
    /* 2 wTotalLength */ 145, 0,
    /* 4 bNumInterfaces, bConfigurationValue */ 2, 1,
    /* 6 iConfiguration */ 0,
    /* 7 bmAttributes, bMaxPower */ 0x80, 50,
    /* ----------- Interface Association Descriptor */
    /* 0 bLength, bDescriptorType */ 8, 0x0B,
    /* 2 bFirstInterface, bInterfaceCount */ 0, 2,
    /* 4 bFunctionClass : 0x01 (Audio) */ 0x01,
    /* 5 bFunctionSubClass : 0x00 (UNDEFINED) */ 0x00,
    /* 6 bFunctionProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 7 iFunction */ 0,
    /* --- Interface Descriptor #0: Control (9+64=73) */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 0, 0,
    /* 4 bNumEndpoints */ 0,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioControl) */ 0x01,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* --- Audio 2.0 AC Interface Header Descriptor (9+8+17+18+12=64, 0x40) */
    /* 0 bLength */ 9,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x01,
    /* 3 bcdADC */ 0x00, 0x02,
    /* 5 bCategory : 0x08 (IO Box) */ 0x08,
    /* 6 wTotalLength */ 64, 0,
    /* 8 bmControls */ 0x00,
    /* -------- Audio 2.0 AC Clock Source Descriptor */
    /* 0 bLength */ 8,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x0A,
    /* 3 bClockID */ 0x10,
    /* 4 bmAttributes : 0x05 (Sync|InternalFixedClk) */ 0x05,
    /* 5 bmControls : 0x01 (FreqReadOnly) */ 0x01,
    /* 6 bAssocTerminal, iClockSource */ 0x00, 0,
    /* ------ Audio 2.0 AC Input Terminal Descriptor */
    /* 0 bLength */ 17,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x02, /* 3 bTerminalID */ 0x04,
    /* 4 wTerminalType : 0x0101 (USB Streaming) */ 0x01, 0x01,
    /* 6 bAssocTerminal, bCSourceID */ 0x00, 0x10,
    /* 8 bNrChannels */ 2,
    /* 9 bmChannelConfig */ 0x00, 0x00, 0x00, 0x00,
    /* 13 iChannelNames, bmControls, iTerminal */ 0, 0x00, 0x00, 0,
    /* -------- Audio 2.0 AC Feature Unit Descriptor */
    /* 0 bLength */ 18,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x06,
    /* 3 bUnitID, bSourceID */ 0x05, 0x04,
    /* 5 bmaControls(0) : 0x0F (VolumeRW|MuteRW) */ 0x0F, 0x00, 0x00, 0x00,
    /* 9 bmaControls(1) : 0x00000000 */ 0x00, 0x00, 0x00, 0x00,
    /* 13 bmaControls(1) : 0x00000000 */ 0x00, 0x00, 0x00, 0x00,
    /* . iFeature */ 0,
    /* ----- Audio 2.0 AC Output Terminal Descriptor */
    /* 0 bLength */ 12,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x03, /* 3 bTerminalID */ 0x06,
    /* 4 wTerminalType : 0x0301 (Speaker) */ 0x01, 0x03,
    /* 6 bAssocTerminal, bSourceID, bCSourceID */ 0x00, 0x05, 0x10,
    /* 9 bmControls, iTerminal */ 0x00, 0x00, 0,
    /* --- Interface Descriptor #1: Stream OUT (9+9+16+6+7+8=55) */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 1, 0,
    /* 4 bNumEndpoints */ 0,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioStream) */ 0x02,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* ----------------------- Interface Descriptor */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 1, 1,
    /* 4 bNumEndpoints */ 1,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioStream) */ 0x02,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* ----------- Audio 2.0 AS Interface Descriptor */
    /* 0 bLength */ 16,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x01,
    /* 3 bTerminalLink, bmControls */ 0x04, 0x00,
    /* 5 bFormatType : 0x01 (FORMAT_TYPE_I) */ 0x01,
    /* 6 bmFormats : 0x000000001 (PCM) */ 0x01, 0x00, 0x00, 0x00, /* 10 bNrChannels */ 2,
    /* 11 bmChannelConfig */ 0x00, 0x00, 0x00, 0x00,
    /* 15 iChannelNames */ 0, /* --------- Audio 2.0 AS Format Type Descriptor */
    /* 0 bLength */ 6,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x02,
    /* 3 bFormatType : 0x01 (FORMAT_TYPE_I) */ 0x01,
    /* 4 bSubslotSize, bBitResolution */ 2, 16,
    /* ------------------------- Endpoint Descriptor */
    /* 0 bLength, bDescriptorType */ 7, 0x05,
    /* 2 bEndpointAddress */ 0x02,
    /* 3 bmAttributes : 0x0D (Sync|ISO) */ 0x0D,
    /* 4 wMaxPacketSize : 0x0100 (256) */ 0x00, 0x01,
    /* 6 bInterval : 0x04 (1ms) */ 4,
    /* - Audio 2.0 AS ISO Audio Data Endpoint Descriptor */
    /* 0 bLength */ 8,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x25, 0x01,
    /* 3 bmAttributes, bmControls */ 0x00, 0x00,
    /* 5 bLockDelayUnits, wLockDelay */ 0x00, 0x00, 0x00,
};
```

<span data-ttu-id="ff6cc-411">La classe audio usa un Framework per dispositivi composito per raggruppare le interfacce (controllo e flusso).</span><span class="sxs-lookup"><span data-stu-id="ff6cc-411">The Audio class uses a composite device framework to group interfaces (control and streaming).</span></span> <span data-ttu-id="ff6cc-412">È necessario prestare attenzione quando si definisce il descrittore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-412">As a result care should be taken when defining the device descriptor.</span></span> <span data-ttu-id="ff6cc-413">USBX si basa sul descrittore IAD per comprendere internamente come associare le interfacce.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-413">USBX relies on the IAD descriptor to know internally how to bind interfaces.</span></span> <span data-ttu-id="ff6cc-414">Il descrittore IAD deve essere dichiarato prima delle interfacce (un'interfaccia AudioControl seguita da una o più interfacce AudioStreaming) e contenere la prima interfaccia della classe audio (l'interfaccia AudioControl) e il numero di interfacce associate.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-414">The IAD descriptor should be declared before the interfaces (an AudioControl interface followed by one or more AudioStreaming interfaces) and contain the first interface of the Audio class (the AudioControl interface) and how many interfaces are attached.</span></span>

<span data-ttu-id="ff6cc-415">Il funzionamento della classe audio varia a seconda che il dispositivo invii o riceva audio, ma in entrambi i casi viene usato un FIFO per l'archiviazione dei buffer del frame audio: se il dispositivo invia audio all'host, l'applicazione aggiunge i buffer del frame audio al FIFO che vengono successivamente inviati all'host da USBX; Se il dispositivo riceve audio dall'host, USBX aggiunge i buffer del frame audio ricevuti dall'host al FIFO, che vengono letti successivamente dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-415">The way the audio class works depends on whether the device is sending or receiving audio, but both cases use a FIFO for storing audio frame buffers: if the device is sending audio to the host, then the application adds audio frame buffers to the FIFO which are later sent to the host by USBX; if the device is receiving audio from the host, then USBX adds the audio frame buffers received from the host to the FIFO which are later read by the application.</span></span> <span data-ttu-id="ff6cc-416">Ogni flusso audio ha una propria FIFO e ogni buffer di frame audio è costituito da più esempi.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-416">Each audio stream has its own FIFO, and each audio frame buffer consists of multiple samples.</span></span>

<span data-ttu-id="ff6cc-417">L'inizializzazione della classe audio prevede le parti seguenti.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-417">The initialization of the Audio class expects the following parts.</span></span>

1. <span data-ttu-id="ff6cc-418">La classe audio prevede i parametri di flusso seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff6cc-418">Audio class expects the following streaming parameters:</span></span>

   ```C
   /* Set the parameters for Audio streams. */
   /* Set the application-defined callback that is invoked when the
      host requests a change to the alternate setting. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_callbacks
       .ux_device_class_audio_stream_change = demo_audio_read_change;

   /* Set the application-defined callback that is invoked whenever
      a USB packet (audio frame) is sent to or received from the host. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_callbacks
       .ux_device_class_audio_stream_frame_done = demo_audio_read_done;

   /* Set the number of audio frame buffers in the FIFO. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_max_frame _buffer_nb = UX_DEMO_FRAME_BUFFER_NB;

   /* Set the maximum size of each audio frame buffer in the FIFO. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_max_frame _buffer_size = UX_DEMO_MAX_FRAME_SIZE;

   /* Set the internally-defined audio processing thread entry pointer. If the application wishes to receive audio from the host
      (which is the case in this example), ux_device_class_audio_read_thread_entry should be used;
      if the application wishes to send data to the host, ux_device_class_audio_write_thread_entry should be used. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_entry = ux_device_class_audio_read_thread_entry;
   ```

2. <span data-ttu-id="ff6cc-419">La classe audio prevede i parametri della funzione seguenti.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-419">Audio class expects the following function parameters.</span></span>

   ```C
   /* Set the parameters for Audio device. */

   /* Set the number of streams. */
   audio_parameter.ux_device_class_audio_parameter_streams_nb = 1;

   /* Set the pointer to the first audio stream parameter.
      Note that we initialized this parameter in the previous section.
      Also note that for more than one streams, this should be an array. */
   audio_parameter.ux_device_class_audio_parameter_streams = audio_stream_parameter;

   /* Set the application-defined callback that is invoked when the audio class
      is activated i.e. device is connected to host. */
   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_slave_class_audio_instance_activate = demo_audio_instance_activate;

   /* Set the application-defined callback that is invoked when the audio class
      is deactivated i.e. device is disconnected from host. */

   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_slave_class_audio_instance_deactivate = demo_audio_instance_deactivate;

   /* Set the application-defined callback that is invoked when the stack receives a control request from the host.
      See below for more details.
   */
   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_device_class_audio_control_process = demo_audio20_request_process;

   /* Initialize the device Audio class. This class owns interfaces starting with 0. */
   status = ux_device_stack_class_register(_ux_system_slave_class_cdc_acm_name,
       ux_device_class_audio_entry, 1, 0, &audio_parameter);
   if(status!=UX_SUCCESS)
       return;
   ```

   <span data-ttu-id="ff6cc-420">Il callback della richiesta di controllo definito dall'applicazione (***ux_device_class_audio_control_process***; impostato nell'esempio precedente) viene richiamato quando lo stack riceve una richiesta di controllo dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-420">The application-defined control request callback (***ux_device_class_audio_control_process***; set in the previous example) is invoked when the stack receives a control request from the host.</span></span> <span data-ttu-id="ff6cc-421">Se la richiesta viene accettata e gestita (riconosciuta o bloccata), il callback deve restituire l'esito positivo; in caso contrario, deve essere restituito Error.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-421">If the request is accepted and handled (acknowledged or stalled) the callback must return success, otherwise error should be returned.</span></span>

   <span data-ttu-id="ff6cc-422">Il processo di richiesta di controllo specifico della classe è definito come callback definito dall'applicazione, perché le richieste di controllo sono molto diverse tra le versioni audio USB e una parte grande del processo di richiesta si riferisce al Framework del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-422">The class-specific control request process is defined as an application-defined callback because the control requests are very different between USB Audio versions and a large part of the request process relates to the device framework.</span></span> <span data-ttu-id="ff6cc-423">L'applicazione deve gestire correttamente le richieste per rendere il dispositivo funzionante.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-423">The application should handle requests correctly to make the device functional.</span></span>

   <span data-ttu-id="ff6cc-424">Poiché per un dispositivo audio, il volume, il mute e la frequenza di campionamento sono richieste di controllo comuni, i callback semplici e definiti internamente per diverse versioni audio USB sono introdotti nelle sezioni successive per l'uso da parte delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-424">Since for an audio device, volume, mute and sampling frequency are common control requests, simple, internally-defined callbacks for different USB audio versions are introduced in later sections for applications to use.</span></span> <span data-ttu-id="ff6cc-425">Per altri dettagli, vedere \***ux_device_class_audio10_control_process** _ e _ \*_ux_device_class_audio_control_request_\*\*.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-425">Refer to ***ux_device_class_audio10_control_process** _ and _ *_ux_device_class_audio_control_request_** for more details.</span></span>

<span data-ttu-id="ff6cc-426">Nel Framework del dispositivo audio il PID/VID viene archiviato nel descrittore del dispositivo (vedere il descrittore del dispositivo dichiarato in precedenza).</span><span class="sxs-lookup"><span data-stu-id="ff6cc-426">In the device framework of the Audio device, the PID/VID are stored in the device descriptor (see the device descriptor declared above).</span></span>

<span data-ttu-id="ff6cc-427">Quando un sistema host USB individua il dispositivo audio USB e monta la classe audio, il dispositivo può essere usato con qualsiasi lettore audio o registratore (a seconda del Framework).</span><span class="sxs-lookup"><span data-stu-id="ff6cc-427">When a USB host system discovers the USB Audio device and mounts the audio class, the device can be used with any audio player or recorder (depending on the framework).</span></span> <span data-ttu-id="ff6cc-428">Per informazioni di riferimento, vedere il sistema operativo host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-428">See the host Operating System for reference.</span></span>

<span data-ttu-id="ff6cc-429">Le API della classe audio sono definite di seguito.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-429">The Audio class APIs are defined below.</span></span>

## <a name="ux_device_class_audio_read_thread_entry"></a><span data-ttu-id="ff6cc-430">ux_device_class_audio_read_thread_entry</span><span class="sxs-lookup"><span data-stu-id="ff6cc-430">ux_device_class_audio_read_thread_entry</span></span>

<span data-ttu-id="ff6cc-431">Voce di thread per la lettura dei dati per la funzione audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-431">Thread entry for reading data for the Audio function.</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-432">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-432">Prototype</span></span>

```C
VOID ux_device_class_audio_read_thread_entry(ULONG audio_stream);
```

### <a name="description"></a><span data-ttu-id="ff6cc-433">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-433">Description</span></span>

<span data-ttu-id="ff6cc-434">Questa funzione viene passata al parametro di inizializzazione del flusso audio se si desidera leggere l'audio dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-434">This function is passed to the audio stream initialization parameter if reading audio from the host is desired.</span></span> <span data-ttu-id="ff6cc-435">Internamente, viene creato un thread con questa funzione come funzione di immissione. il thread stesso legge i dati audio tramite l'endpoint di uscita isocrono nella funzione audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-435">Internally, a thread is created with this function as its entry function; the thread itself reads audio data through the isochronous OUT endpoint in the Audio function.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-436">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-436">Parameters</span></span>

- <span data-ttu-id="ff6cc-437">**audio_stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-437">**audio_stream**: Pointer to the audio stream instance.</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-438">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-438">Example</span></span>

```C
/* Set parameter to initialize a stream for reading. */
audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_entry
     = ux_device_class_audio_read_thread_entry;
```

## <a name="ux_device_class_audio_write_thread_entry"></a><span data-ttu-id="ff6cc-439">ux_device_class_audio_write_thread_entry</span><span class="sxs-lookup"><span data-stu-id="ff6cc-439">ux_device_class_audio_write_thread_entry</span></span>

<span data-ttu-id="ff6cc-440">Voce di thread per la scrittura dei dati per la funzione audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-440">Thread entry for writing data for the Audio function</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-441">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-441">Prototype</span></span>

```C
VOID ux_device_class_audio_write_thread_entry(ULONG audio_stream);
```

### <a name="description"></a><span data-ttu-id="ff6cc-442">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-442">Description</span></span>

<span data-ttu-id="ff6cc-443">Questa funzione viene passata al parametro di inizializzazione del flusso audio se si desidera scrivere l'audio nell'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-443">This function is passed to the audio stream initialization parameter if writing audio to the host is desired.</span></span> <span data-ttu-id="ff6cc-444">Internamente, viene creato un thread con questa funzione come funzione di immissione. il thread scrive i dati audio tramite l'endpoint isocrono nella funzione audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-444">Internally, a thread is created with this function as its entry function; the thread itself writes audio data through the isochronous IN endpoint in the Audio function.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-445">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-445">Parameters</span></span>

- <span data-ttu-id="ff6cc-446">**audio_stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-446">**audio_stream**: Pointer to the audio stream instance.</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-447">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-447">Example</span></span>

```C
/* Set parameter to initialize as stream for writing. */
audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_en
    try = ux_device_class_audio_write_thread_entry;
```

## <a name="ux_device_class_audio_stream_get"></a><span data-ttu-id="ff6cc-448">ux_device_class_audio_stream_get</span><span class="sxs-lookup"><span data-stu-id="ff6cc-448">ux_device_class_audio_stream_get</span></span>

<span data-ttu-id="ff6cc-449">Ottenere un'istanza del flusso specifica per la funzione audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-449">Get specific stream instance for the Audio function</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-450">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-450">Prototype</span></span>

```C
UINT ux_device_class_audio_stream_get(
    UX_DEVICE_CLASS_AUDIO *audio,
    ULONG stream_index, 
    UX_DEVICE_CLASS_AUDIO_STREAM **stream);
```

### <a name="description"></a><span data-ttu-id="ff6cc-451">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-451">Description</span></span>

<span data-ttu-id="ff6cc-452">Questa funzione viene utilizzata per ottenere un'istanza del flusso della classe audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-452">This function is used to get a stream instance of audio class.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-453">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-453">Parameters</span></span>

- <span data-ttu-id="ff6cc-454">**audio**: puntatore all'istanza audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-454">**audio**: Pointer to the audio instance</span></span>
- <span data-ttu-id="ff6cc-455">**stream_index**: Indice dell'istanza del flusso basato su 0</span><span class="sxs-lookup"><span data-stu-id="ff6cc-455">**stream_index**: Stream instance index based on 0</span></span>
- <span data-ttu-id="ff6cc-456">**Stream**: puntatore al buffer per archiviare il puntatore dell'istanza del flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-456">**stream**: Pointer to buffer to store the audio stream instance pointer</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-457">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-457">Return Value</span></span>

- <span data-ttu-id="ff6cc-458">**UX_SUCCESS** (0x00) questa operazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="ff6cc-458">**UX_SUCCESS** (0x00) This operation was successful</span></span>
- <span data-ttu-id="ff6cc-459">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-459">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-460">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-460">Example</span></span>

```C
/* Get audio stream instance. */
status = ux_device_class_audio_stream_get(audio, 0, &stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_reception_start"></a><span data-ttu-id="ff6cc-461">ux_device_class_audio_reception_start</span><span class="sxs-lookup"><span data-stu-id="ff6cc-461">ux_device_class_audio_reception_start</span></span>

<span data-ttu-id="ff6cc-462">Avviare la ricezione di dati audio per il flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-462">Start audio data reception for the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-463">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-463">Prototype</span></span>

```C
UINT ux_device_class_audio_reception_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a><span data-ttu-id="ff6cc-464">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-464">Description</span></span>

<span data-ttu-id="ff6cc-465">Questa funzione viene usata per avviare la lettura dei dati audio nei flussi audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-465">This function is used to start audio data reading in audio streams.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-466">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-466">Parameters</span></span>

- <span data-ttu-id="ff6cc-467">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-467">**stream**: Pointer to the audio stream instance.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-468">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-468">Return Value</span></span>

- <span data-ttu-id="ff6cc-469">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-469">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-470">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-470">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-471">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è pieno.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-471">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is full.</span></span>
- <span data-ttu-id="ff6cc-472">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-472">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-473">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-473">Example</span></span>

```C
/* Start stream data reception. */
status = ux_device_class_audio_reception_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read8"></a><span data-ttu-id="ff6cc-474">ux_device_class_audio_sample_read8</span><span class="sxs-lookup"><span data-stu-id="ff6cc-474">ux_device_class_audio_sample_read8</span></span>

<span data-ttu-id="ff6cc-475">Leggere l'esempio a 8 bit dal flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-475">Read 8-bit sample from the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-476">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-476">Prototype</span></span>

```C
UINT ux_device_class_audio_sample_read8(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    UCHAR *buffer);
```

### <a name="description"></a><span data-ttu-id="ff6cc-477">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-477">Description</span></span>

<span data-ttu-id="ff6cc-478">Questa funzione legge i dati di esempio audio a 8 bit dal flusso specificato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-478">This function reads 8-bit audio sample data from the specified stream.</span></span>

<span data-ttu-id="ff6cc-479">In particolare, legge i dati di esempio dal buffer del frame audio corrente nella FIFO.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-479">Specifically, it reads the sample data from the current audio frame buffer in the FIFO.</span></span> <span data-ttu-id="ff6cc-480">Dopo aver letto l'ultimo esempio in un frame audio, il frame verrà liberato automaticamente in modo da poter essere usato per accettare più dati dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-480">Upon reading the last sample in an audio frame, the frame will be automatically freed so that it can be used to accept more data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-481">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-481">Parameters</span></span>

- <span data-ttu-id="ff6cc-482">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-482">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="ff6cc-483">**buffer**: puntatore al buffer per salvare il byte di esempio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-483">**buffer**: Pointer to the buffer to save sample byte.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-484">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-484">Return Value</span></span>

- <span data-ttu-id="ff6cc-485">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-485">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-486">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-486">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-487">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è null.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-487">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="ff6cc-488">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-488">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-489">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-489">Example</span></span>

```C
/* Read a byte in audio FIFO. */

status = ux_device_class_audio_sample_read8(stream, &sample_byte);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read16"></a><span data-ttu-id="ff6cc-490">ux_device_class_audio_sample_read16</span><span class="sxs-lookup"><span data-stu-id="ff6cc-490">ux_device_class_audio_sample_read16</span></span>

<span data-ttu-id="ff6cc-491">Leggere l'esempio a 16 bit dal flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-491">Read 16-bit sample from the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-492">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-492">Prototype</span></span>

```C
UINT ux_device_class_audio_sample_read16(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    USHORT *buffer);
```

### <a name="description"></a><span data-ttu-id="ff6cc-493">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-493">Description</span></span>

<span data-ttu-id="ff6cc-494">Questa funzione legge i dati di esempio audio a 16 bit dal flusso specificato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-494">This function reads 16-bit audio sample data from the specified stream.</span></span>

<span data-ttu-id="ff6cc-495">In particolare, legge i dati di esempio dal buffer del frame audio corrente nella FIFO.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-495">Specifically, it reads the sample data from the current audio frame buffer in the FIFO.</span></span> <span data-ttu-id="ff6cc-496">Dopo aver letto l'ultimo esempio in un frame audio, il frame verrà liberato automaticamente in modo da poter essere usato per accettare più dati dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-496">Upon reading the last sample in an audio frame, the frame will be automatically freed so that it can be used to accept more data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-497">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-497">Parameters</span></span>

- <span data-ttu-id="ff6cc-498">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-498">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="ff6cc-499">**buffer**: puntatore al buffer per salvare l'esempio a 16 bit.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-499">**buffer**: Pointer to the buffer to save the 16-bit sample.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-500">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-500">Return Value</span></span>

- <span data-ttu-id="ff6cc-501">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-501">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-502">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-502">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-503">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è null.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-503">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="ff6cc-504">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-504">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-505">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-505">Example</span></span>

```C
/* Read a 16-bit sample in audio FIFO. */

status = ux_device_class_audio_sample_read16(stream, &sample_word);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read24"></a><span data-ttu-id="ff6cc-506">ux_device_class_audio_sample_read24</span><span class="sxs-lookup"><span data-stu-id="ff6cc-506">ux_device_class_audio_sample_read24</span></span>

<span data-ttu-id="ff6cc-507">Leggere l'esempio a 24 bit dal flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-507">Read 24-bit sample from the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-508">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-508">Prototype</span></span>

```C
UINT ux_device_class_audio_sample_read24(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a><span data-ttu-id="ff6cc-509">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-509">Description</span></span>

<span data-ttu-id="ff6cc-510">Questa funzione legge i dati di esempio audio a 24 bit dal flusso specificato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-510">This function reads 24-bit audio sample data from the specified stream.</span></span>

<span data-ttu-id="ff6cc-511">In particolare, legge i dati di esempio dal buffer del frame audio corrente nella FIFO.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-511">Specifically, it reads the sample data from the current audio frame buffer in the FIFO.</span></span> <span data-ttu-id="ff6cc-512">Dopo aver letto l'ultimo esempio in un frame audio, il frame verrà liberato automaticamente in modo da poter essere usato per accettare più dati dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-512">Upon reading the last sample in an audio frame, the frame will be automatically freed so that it can be used to accept more data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-513">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-513">Parameters</span></span>

- <span data-ttu-id="ff6cc-514">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-514">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="ff6cc-515">**buffer**: puntatore al buffer per salvare l'esempio a 3 byte.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-515">**buffer**: Pointer to the buffer to save the 3-byte sample.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-516">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-516">Return Value</span></span>

- <span data-ttu-id="ff6cc-517">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-517">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-518">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-518">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-519">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è null.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-519">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="ff6cc-520">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-520">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-521">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-521">Example</span></span>

```C
/* Read 3 bytes to in audio FIFO. */

status = ux_device_class_audio_sample_read24(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read32"></a><span data-ttu-id="ff6cc-522">ux_device_class_audio_sample_read32</span><span class="sxs-lookup"><span data-stu-id="ff6cc-522">ux_device_class_audio_sample_read32</span></span>

<span data-ttu-id="ff6cc-523">Leggere l'esempio a 32 bit dal flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-523">Read 32-bit sample from the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-524">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-524">Prototype</span></span>

```C
UINT ux_device_class_audio_sample_read32(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a><span data-ttu-id="ff6cc-525">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-525">Description</span></span>

<span data-ttu-id="ff6cc-526">Questa funzione legge i dati di esempio audio a 32 bit dal flusso specificato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-526">This function reads 32-bit audio sample data from the specified stream.</span></span>

<span data-ttu-id="ff6cc-527">In particolare, legge i dati di esempio dal buffer del frame audio corrente nella FIFO.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-527">Specifically, it reads the sample data from the current audio frame buffer in the FIFO.</span></span> <span data-ttu-id="ff6cc-528">Dopo aver letto l'ultimo esempio in un frame audio, il frame verrà liberato automaticamente in modo da poter essere usato per accettare più dati dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-528">Upon reading the last sample in an audio frame, the frame will be automatically freed so that it can be used to accept more data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-529">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-529">Parameters</span></span>

- <span data-ttu-id="ff6cc-530">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-530">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="ff6cc-531">**buffer**: puntatore al buffer per salvare i dati a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-531">**buffer**: Pointer to the buffer to save the 4-byte data.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-532">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-532">Return Value</span></span>

- <span data-ttu-id="ff6cc-533">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-533">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-534">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-534">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-535">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è null.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-535">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="ff6cc-536">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-536">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-537">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-537">Example</span></span>

```C
/* Read 4 bytes in audio FIFO. */

status = ux_device_class_audio_sample_read32(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_get"></a><span data-ttu-id="ff6cc-538">ux_device_class_audio_read_frame_get</span><span class="sxs-lookup"><span data-stu-id="ff6cc-538">ux_device_class_audio_read_frame_get</span></span>

<span data-ttu-id="ff6cc-539">Ottenere l'accesso al frame audio nel flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-539">Get access to audio frame in the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-540">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-540">Prototype</span></span>

```C
UINT ux_device_class_audio_read_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a><span data-ttu-id="ff6cc-541">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-541">Description</span></span>

<span data-ttu-id="ff6cc-542">Questa funzione restituisce il primo buffer del frame audio e la relativa lunghezza nel FIFO del flusso specificato.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-542">This function returns the first audio frame buffer and its length in the specified stream's FIFO.</span></span> <span data-ttu-id="ff6cc-543">Al termine dell'elaborazione dei dati da parte dell'applicazione, è necessario utilizzare ux_device_class_audio_read_frame_free per liberare il buffer del frame nel FIFO.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-543">When the application is done processing the data, ux_device_class_audio_read_frame_free must be used to free the frame buffer in the FIFO.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-544">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-544">Parameters</span></span>

- <span data-ttu-id="ff6cc-545">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-545">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="ff6cc-546">**frame_data**: puntatore al puntatore dati in cui restituire il puntatore dati.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-546">**frame_data**: Pointer to data pointer to return the data pointer in.</span></span>
- <span data-ttu-id="ff6cc-547">**frame_length**: puntatore al buffer per salvare la lunghezza del frame in numero di byte.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-547">**frame_length**: Pointer to buffer to save the frame length in number of bytes.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-548">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-548">Return Value</span></span>

- <span data-ttu-id="ff6cc-549">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-549">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-550">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-550">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-551">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è null.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-551">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="ff6cc-552">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-552">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-553">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-553">Example</span></span>

```C
/* Get frame access. */

status = ux_device_class_audio_read_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_free"></a><span data-ttu-id="ff6cc-554">ux_device_class_audio_read_frame_free</span><span class="sxs-lookup"><span data-stu-id="ff6cc-554">ux_device_class_audio_read_frame_free</span></span>

<span data-ttu-id="ff6cc-555">Liberare un buffer del frame audio nel flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-555">Free an audio frame buffer in Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-556">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-556">Prototype</span></span>

```C
UINT ux_device_class_audio_read_frame_free(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a><span data-ttu-id="ff6cc-557">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-557">Description</span></span>

<span data-ttu-id="ff6cc-558">Questa funzione libera il buffer del frame audio all'inizio della FIFO del flusso specificato, in modo che possa ricevere dati dall'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-558">This function frees the audio frame buffer at the front of the specified stream's FIFO so that it can receive data from the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-559">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-559">Parameters</span></span>

- <span data-ttu-id="ff6cc-560">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-560">**stream**: Pointer to the audio stream instance.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-561">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-561">Return Value</span></span>

- <span data-ttu-id="ff6cc-562">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-562">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-563">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-563">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-564">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è null.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-564">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="ff6cc-565">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-565">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-566">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-566">Example</span></span>

```C
/* Refree a frame buffer in FIFO. */

status = ux_device_class_audio_read_frame_free(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_transmission_start"></a><span data-ttu-id="ff6cc-567">ux_device_class_audio_transmission_start</span><span class="sxs-lookup"><span data-stu-id="ff6cc-567">ux_device_class_audio_transmission_start</span></span>

<span data-ttu-id="ff6cc-568">Avviare la trasmissione di dati audio per il flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-568">Start audio data transmission for the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-569">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-569">Prototype</span></span>

```C
UINT ux_device_class_audio_transmission_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a><span data-ttu-id="ff6cc-570">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-570">Description</span></span>

<span data-ttu-id="ff6cc-571">Questa funzione viene usata per iniziare a inviare i dati audio scritti nel FIFO nella classe audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-571">This function is used to start sending audio data written to the FIFO in the audio class.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-572">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-572">Parameters</span></span>

- <span data-ttu-id="ff6cc-573">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-573">**stream**: Pointer to the audio stream instance.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-574">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-574">Return Value</span></span>

- <span data-ttu-id="ff6cc-575">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-575">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-576">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-576">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-577">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è null.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-577">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is null.</span></span>
- <span data-ttu-id="ff6cc-578">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-578">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-579">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-579">Example</span></span>

```C
/* Start stream data transmission. */

status = ux_device_class_audio_transmission_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_frame_write"></a><span data-ttu-id="ff6cc-580">ux_device_class_audio_frame_write</span><span class="sxs-lookup"><span data-stu-id="ff6cc-580">ux_device_class_audio_frame_write</span></span>

<span data-ttu-id="ff6cc-581">Scrivere un frame audio nel flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-581">Write an audio frame into the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-582">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-582">Prototype</span></span>

```C
UINT ux_device_class_audio_frame_write(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR *frame,
    ULONG frame_length);
```

### <a name="description"></a><span data-ttu-id="ff6cc-583">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-583">Description</span></span>

<span data-ttu-id="ff6cc-584">Questa funzione scrive un frame nel FIFO del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-584">This function writes a frame to the audio stream's FIFO.</span></span> <span data-ttu-id="ff6cc-585">I dati del frame vengono copiati nel buffer disponibile nella FIFO in modo che possano essere inviati all'host.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-585">The frame data is copied to the available buffer in the FIFO so that it can be sent to the host.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-586">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-586">Parameters</span></span>

- <span data-ttu-id="ff6cc-587">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-587">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="ff6cc-588">**frame**: puntatore ai dati del frame.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-588">**frame**: Pointer to frame data.</span></span>
- <span data-ttu-id="ff6cc-589">**frame_length** Lunghezza del frame in numero di byte.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-589">**frame_length** Frame length in number of bytes.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-590">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-590">Return Value</span></span>

- <span data-ttu-id="ff6cc-591">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-591">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-592">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-592">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-593">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è pieno.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-593">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is full.</span></span>
- <span data-ttu-id="ff6cc-594">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-594">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-595">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-595">Example</span></span>

```C
/* Get frame access. */

status = ux_device_class_audio_frame_write(stream, frame, frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_write_frame_get"></a><span data-ttu-id="ff6cc-596">ux_device_class_audio_write_frame_get</span><span class="sxs-lookup"><span data-stu-id="ff6cc-596">ux_device_class_audio_write_frame_get</span></span>

<span data-ttu-id="ff6cc-597">Ottenere l'accesso al frame audio nel flusso audio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-597">Get access to audio frame in the Audio stream</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-598">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-598">Prototype</span></span>

```C
UINT ux_device_class_audio_write_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a><span data-ttu-id="ff6cc-599">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-599">Description</span></span>

<span data-ttu-id="ff6cc-600">Questa funzione recupera l'indirizzo dell'ultimo buffer del frame audio della FIFO; Recupera anche la lunghezza del buffer del frame audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-600">This function retrieves the address of the last audio frame buffer of the FIFO; it also retrieves the length of the audio frame buffer.</span></span> <span data-ttu-id="ff6cc-601">Dopo che l'applicazione riempie il buffer del frame audio con i dati desiderati, è necessario usare ***ux_device_class_audio_write_frame_commit*** per aggiungere o eseguire il commit del buffer del frame nel FIFO.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-601">After the application fills the audio frame buffer with its desired data, ***ux_device_class_audio_write_frame_commit*** must be used to add/commit the frame buffer to the FIFO.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-602">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-602">Parameters</span></span>

- <span data-ttu-id="ff6cc-603">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-603">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="ff6cc-604">**frame_data**: puntatore al puntatore ai dati del frame per restituire il puntatore ai dati del frame.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-604">**frame_data**: Pointer to frame data pointer to return the frame data pointer in.</span></span>
- <span data-ttu-id="ff6cc-605">**frame_length** Puntatore al buffer per salvare la lunghezza del frame in numero di byte.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-605">**frame_length** Pointer to the buffer to save frame length in number of bytes .</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-606">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-606">Return Value</span></span>

- <span data-ttu-id="ff6cc-607">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-607">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-608">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-608">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-609">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è pieno.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-609">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is full.</span></span>
- <span data-ttu-id="ff6cc-610">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-610">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-611">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-611">Example</span></span>

```C
/* Get frame access. */

status = ux_device_class_audio_write_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
     return;
```

## <a name="ux_device_class_audio_write_frame_commit"></a><span data-ttu-id="ff6cc-612">ux_device_class_audio_write_frame_commit</span><span class="sxs-lookup"><span data-stu-id="ff6cc-612">ux_device_class_audio_write_frame_commit</span></span>

<span data-ttu-id="ff6cc-613">Eseguire il commit di un buffer del frame audio nel flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-613">Commit an audio frame buffer in Audio stream.</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-614">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-614">Prototype</span></span>

```C
UINT ux_device_class_audio_write_frame_commit(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG length);
```

### <a name="description"></a><span data-ttu-id="ff6cc-615">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-615">Description</span></span>

<span data-ttu-id="ff6cc-616">Questa funzione aggiunge/conferma l'ultimo buffer del frame audio alla FIFO, in modo che il buffer sia pronto per essere trasferito nell'host. Si noti che l'ultimo buffer del frame audio deve essere stato compilato tramite ux_device_class_write_frame_get.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-616">This function adds/commits the last audio frame buffer to the FIFO so the buffer is ready to be transferred to host; note the last audio frame buffer should have been filled out via ux_device_class_write_frame_get.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-617">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-617">Parameters</span></span>

- <span data-ttu-id="ff6cc-618">**Stream**: puntatore all'istanza del flusso audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-618">**stream**: Pointer to the audio stream instance.</span></span>
- <span data-ttu-id="ff6cc-619">**lunghezza**: numero di byte pronti nel buffer.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-619">**length**: Number of bytes ready in the buffer.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-620">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-620">Return Value</span></span>

- <span data-ttu-id="ff6cc-621">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-621">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-622">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'interfaccia è inattiva.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-622">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The interface is down.</span></span>
- <span data-ttu-id="ff6cc-623">Il buffer FIFO **UX_BUFFER_OVERFLOW** (0x5D) è fssull.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-623">**UX_BUFFER_OVERFLOW** (0x5d) FIFO buffer is fssull.</span></span>
- <span data-ttu-id="ff6cc-624">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-624">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-625">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-625">Example</span></span>

```C
/* Commit a frame after fill values in buffer. */

status = ux_device_class_audio_write_frame_commit(stream, 192);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio10_control_process"></a><span data-ttu-id="ff6cc-626">ux_device_class_audio10_control_process</span><span class="sxs-lookup"><span data-stu-id="ff6cc-626">ux_device_class_audio10_control_process</span></span>

<span data-ttu-id="ff6cc-627">Elabora richieste di controllo audio 1,0 USB</span><span class="sxs-lookup"><span data-stu-id="ff6cc-627">Process USB Audio 1.0 control requests</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-628">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-628">Prototype</span></span>

```C
UINT ux_device_class_audio10_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO10_CONTROL_GROUP *group);
```

### <a name="description"></a><span data-ttu-id="ff6cc-629">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-629">Description</span></span>

<span data-ttu-id="ff6cc-630">Questa funzione gestisce le richieste di base inviate dall'host nell'endpoint di controllo con un tipo specifico audio 1,0 USB.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-630">This function manages basic requests sent by the host on the control endpoint with a USB Audio 1.0 specific type.</span></span>

<span data-ttu-id="ff6cc-631">Le funzionalità audio 1,0 delle richieste volume e mute vengono elaborate nella funzione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-631">Audio 1.0 features of volume and mute requests are processed in the function.</span></span> <span data-ttu-id="ff6cc-632">Quando si elaborano le richieste, i dati predefiniti passati dall'ultimo parametro (gruppo) vengono usati per rispondere alle richieste e archiviare le modifiche del controllo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-632">When processing the requests, pre-defined data passed by the last parameter (group) is used to answer requests and store control changes.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-633">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-633">Parameters</span></span>

- <span data-ttu-id="ff6cc-634">**audio**: puntatore all'istanza audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-634">**audio**: Pointer to the audio instance.</span></span>
- <span data-ttu-id="ff6cc-635">**Transfer**: puntatore all'istanza della richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-635">**transfer**: Pointer to the transfer request instance.</span></span>
- <span data-ttu-id="ff6cc-636">**gruppo**: gruppo di dati per il processo di richiesta.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-636">**group**: Data group for request process.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-637">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-637">Return Value</span></span>

- <span data-ttu-id="ff6cc-638">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-638">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-639">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-639">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-640">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-640">Example</span></span>

```C
/* Initialize audio 1.0 control values. */

audio_control[0].ux_device_class_audio10_control_fu_id = 2;
audio_control[0].ux_device_class_audio10_control_mute[0] = 0;
audio_control[0].ux_device_class_audio10_control_volume[0] = 0;
audio_control[1].ux_device_class_audio10_control_fu_id = 5;
audio_control[1].ux_device_class_audio10_control_mute[0] = 0;
audio_control[1].ux_device_class_audio10_control_volume[0] = 0;

/* Handle request and update control values.
Note here only mute and volume for master channel is supported.
*/

status = ux_device_class_audio10_control_process(audio, transfer, &group);
if (status == UX_SUCCESS)
{
    /* Request handled, check changes */
    switch(audio_control[0].ux_device_class_audio10_control_changed)
    {
        case UX_DEVICE_CLASS_AUDIO10_CONTROL_MUTE_CHANGED:
        case UX_DEVICE_CLASS_AUDIO10_CONTROL_VOLUME_CHANGED:
        default: break;
    }
}
```

## <a name="ux_device_class_audio20_control_process"></a><span data-ttu-id="ff6cc-641">ux_device_class_audio20_control_process</span><span class="sxs-lookup"><span data-stu-id="ff6cc-641">ux_device_class_audio20_control_process</span></span>

<span data-ttu-id="ff6cc-642">Elabora richieste di controllo audio 1,0 USB</span><span class="sxs-lookup"><span data-stu-id="ff6cc-642">Process USB Audio 1.0 control requests</span></span>

### <a name="prototype"></a><span data-ttu-id="ff6cc-643">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ff6cc-643">Prototype</span></span>
```C
UINT ux_device_class_audio20_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO20_CONTROL_GROUP *group);
```

### <a name="description"></a><span data-ttu-id="ff6cc-644">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-644">Description</span></span>

<span data-ttu-id="ff6cc-645">Questa funzione gestisce le richieste di base inviate dall'host nell'endpoint di controllo con un tipo specifico audio 2,0 USB.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-645">This function manages basic requests sent by the host on the control endpoint with a USB Audio 2.0 specific type.</span></span>

<span data-ttu-id="ff6cc-646">Frequenza di campionamento audio 2,0 (presunta singola frequenza fissa), le funzionalità delle richieste di volume e di silenziamento vengono elaborate nella funzione.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-646">Audio 2.0 sampling rate (assumed single fixed frequency), features of volume and mute requests are processed in the function.</span></span> <span data-ttu-id="ff6cc-647">Quando si elaborano le richieste, i dati predefiniti passati dall'ultimo parametro (gruppo) vengono usati per rispondere alle richieste e archiviare le modifiche del controllo.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-647">When processing the requests, pre-defined data passed by the last parameter (group) is used to answer requests and store control changes.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff6cc-648">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff6cc-648">Parameters</span></span>

- <span data-ttu-id="ff6cc-649">**audio**: puntatore all'istanza audio.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-649">**audio**: Pointer to the audio instance.</span></span>
- <span data-ttu-id="ff6cc-650">**Transfer**: puntatore all'istanza della richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-650">**transfer**: Pointer to the transfer request instance.</span></span>
- <span data-ttu-id="ff6cc-651">**gruppo**: gruppo di dati per il processo di richiesta.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-651">**group**: Data group for request process.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff6cc-652">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ff6cc-652">Return Value</span></span>

- <span data-ttu-id="ff6cc-653">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="ff6cc-653">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="ff6cc-654">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="ff6cc-654">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="ff6cc-655">Esempio</span><span class="sxs-lookup"><span data-stu-id="ff6cc-655">Example</span></span>

```C
/* Initialize audio 2.0 control values. */

audio_control[0].ux_device_class_audio20_control_cs_id = 0x10;
audio_control[0].ux_device_class_audio20_control_sampling_frequency = 48000;
audio_control[0].ux_device_class_audio20_control_fu_id = 2;
audio_control[0].ux_device_class_audio20_control_mute[0] = 0;
audio_control[0].ux_device_class_audio20_control_volume_min[0] = 0;
audio_control[0].ux_device_class_audio20_control_volume_max[0] = 100;
audio_control[0].ux_device_class_audio20_control_volume[0] = 50;
audio_control[1].ux_device_class_audio20_control_cs_id = 0x10;
audio_control[1].ux_device_class_audio20_control_sampling_frequency = 48000;
audio_control[1].ux_device_class_audio20_control_fu_id = 5;
audio_control[1].ux_device_class_audio20_control_mute[0] = 0;
audio_control[1].ux_device_class_audio20_control_volume_min[0] = 0;
audio_control[1].ux_device_class_audio20_control_volume_max[0] = 100;
audio_control[1].ux_device_class_audio20_control_volume[0] = 50;

/* Handle request and update control values.
Note here only mute and volume for master channel is supported.
*/

status = ux_device_class_audio20_control_process(audio, transfer, &group);
if (status == UX_SUCCESS)
{
    /* Request handled, check changes */
    switch(audio_control[0].ux_device_class_audio20_control_changed)
    {
        case UX_DEVICE_CLASS_AUDIO20_CONTROL_MUTE_CHANGED:
        case UX_DEVICE_CLASS_AUDIO20_CONTROL_VOLUME_CHANGED:
        default: break;
    }
}
```
