---
title: Capitolo 3-componenti funzionali dello stack di dispositivi USBX
description: Questo capitolo contiene una descrizione dello stack di dispositivi USB embedded a prestazioni elevate di USBX da una prospettiva funzionale.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: a20fed71cbee8c50519be4a971eb191e0cc93915
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823330"
---
# <a name="chapter-3---functional-components-of-usbx-device-stack"></a><span data-ttu-id="69667-103">Capitolo 3-componenti funzionali dello stack di dispositivi USBX</span><span class="sxs-lookup"><span data-stu-id="69667-103">Chapter 3 - Functional Components of USBX Device Stack</span></span>

<span data-ttu-id="69667-104">Questo capitolo contiene una descrizione dello stack di dispositivi USB embedded a prestazioni elevate di USBX da una prospettiva funzionale.</span><span class="sxs-lookup"><span data-stu-id="69667-104">This chapter contains a description of the high performance USBX embedded USB device stack from a functional perspective.</span></span>

## <a name="execution-overview"></a><span data-ttu-id="69667-105">Panoramica dell'esecuzione</span><span class="sxs-lookup"><span data-stu-id="69667-105">Execution Overview</span></span>

<span data-ttu-id="69667-106">USBX per il dispositivo è costituito da diversi componenti.</span><span class="sxs-lookup"><span data-stu-id="69667-106">USBX for the device is composed of several components.</span></span>

- <span data-ttu-id="69667-107">Inizializzazione</span><span class="sxs-lookup"><span data-stu-id="69667-107">Initialization</span></span>
- <span data-ttu-id="69667-108">Chiamate dell'interfaccia dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="69667-108">Application interface calls</span></span>
- <span data-ttu-id="69667-109">Classi di dispositivi</span><span class="sxs-lookup"><span data-stu-id="69667-109">Device Classes</span></span>
- <span data-ttu-id="69667-110">Stack dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="69667-110">USB Device Stack</span></span>
- <span data-ttu-id="69667-111">Controller del dispositivo</span><span class="sxs-lookup"><span data-stu-id="69667-111">Device controller</span></span>
- <span data-ttu-id="69667-112">Gestione VBUS</span><span class="sxs-lookup"><span data-stu-id="69667-112">VBUS manager</span></span>

<span data-ttu-id="69667-113">Il diagramma seguente illustra lo stack di dispositivi USBX.</span><span class="sxs-lookup"><span data-stu-id="69667-113">The following diagram illustrates the USBX Device stack.</span></span>

![Stack di dispositivi USBX](media/usbx-device-stack/usbx-device-stack.png)

### <a name="initialization"></a><span data-ttu-id="69667-115">Inizializzazione</span><span class="sxs-lookup"><span data-stu-id="69667-115">Initialization</span></span>

<span data-ttu-id="69667-116">Per attivare USBX, è necessario chiamare la funzione ***ux_system_initialize*** .</span><span class="sxs-lookup"><span data-stu-id="69667-116">In order to activate USBX, the function ***ux_system_initialize*** must be called.</span></span> <span data-ttu-id="69667-117">Questa funzione Inizializza le risorse di memoria di USBX.</span><span class="sxs-lookup"><span data-stu-id="69667-117">This function initializes the memory resources of USBX.</span></span>

<span data-ttu-id="69667-118">Per attivare le funzionalità del dispositivo USBX, è necessario chiamare la funzione ***ux_device_stack_initialize*** .</span><span class="sxs-lookup"><span data-stu-id="69667-118">In order to activate USBX device facilities, the function ***ux_device_stack_initialize*** must be called.</span></span> <span data-ttu-id="69667-119">Questa funzione inizializza a sua volta tutte le risorse usate dallo stack di dispositivi USBX, ad esempio thread ThreadX, mutex e semafori.</span><span class="sxs-lookup"><span data-stu-id="69667-119">This function will in turn initialize all the resources used by the USBX device stack such as ThreadX threads, mutexes, and semaphores.</span></span>

<span data-ttu-id="69667-120">L'inizializzazione dell'applicazione consente di attivare il controller del dispositivo USB e una o più classi USB.</span><span class="sxs-lookup"><span data-stu-id="69667-120">It is up to the application initialization to activate the USB device controller and one or more USB classes.</span></span> <span data-ttu-id="69667-121">Contrariamente al lato host USB, il lato dispositivo può avere un solo driver del controller USB in esecuzione in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="69667-121">Contrary to the USB host side, the device side can have only one USB controller driver running at any time.</span></span> <span data-ttu-id="69667-122">Quando le classi sono state registrate nello stack e la funzione di inizializzazione dei controller del dispositivo è stata chiamata, il bus è attivo e lo stack risponderà ai comandi di reimpostazione del bus e enumerazione host.</span><span class="sxs-lookup"><span data-stu-id="69667-122">When the classes have been registered to the stack and the device controller(s) initialization function has been called, the bus is active and the stack will reply to bus reset and host enumeration commands.</span></span>

### <a name="application-interface-calls"></a><span data-ttu-id="69667-123">Chiamate dell'interfaccia dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="69667-123">Application Interface Calls</span></span>

<span data-ttu-id="69667-124">In USBX sono disponibili due livelli di API.</span><span class="sxs-lookup"><span data-stu-id="69667-124">There are two levels of APIs in USBX.</span></span>

- <span data-ttu-id="69667-125">API dello stack di dispositivi USB</span><span class="sxs-lookup"><span data-stu-id="69667-125">USB Device Stack APIs</span></span>
- <span data-ttu-id="69667-126">API della classe dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="69667-126">USB Device Class APIs</span></span>

<span data-ttu-id="69667-127">In genere, un'applicazione USBX non deve chiamare alcuna API dello stack di dispositivi USB.</span><span class="sxs-lookup"><span data-stu-id="69667-127">Normally, a USBX application should not have to call any of the USB device stack APIs.</span></span> <span data-ttu-id="69667-128">La maggior parte delle applicazioni accederà solo alle API della classe USB.</span><span class="sxs-lookup"><span data-stu-id="69667-128">Most applications will only access the USB Class APIs.</span></span>

### <a name="usb-device-stack-apis"></a><span data-ttu-id="69667-129">API dello stack di dispositivi USB</span><span class="sxs-lookup"><span data-stu-id="69667-129">USB Device Stack APIs</span></span>

<span data-ttu-id="69667-130">Le API dello stack di dispositivi sono responsabili della registrazione dei componenti del dispositivo USBX, ad esempio le classi e il Framework del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-130">The device stack APIs are responsible for the registration of USBX device components such as classes and the device framework.</span></span>

### <a name="usb-device-class-apis"></a><span data-ttu-id="69667-131">API della classe dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="69667-131">USB Device Class APIs</span></span>

<span data-ttu-id="69667-132">Le API della classe sono molto specifiche per ogni classe USB.</span><span class="sxs-lookup"><span data-stu-id="69667-132">The Class APIs are very specific to each USB class.</span></span> <span data-ttu-id="69667-133">La maggior parte delle API comuni per le classi USB fornisce servizi quali l'apertura e la chiusura di un dispositivo, la lettura e la scrittura in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-133">Most of the common APIs for USB classes provided services such as opening/closing a device and reading from and writing to a device.</span></span> <span data-ttu-id="69667-134">Le API sono simili per natura al lato host.</span><span class="sxs-lookup"><span data-stu-id="69667-134">The APIs are similar in nature to the host side.</span></span>

## <a name="device-framework"></a><span data-ttu-id="69667-135">Framework del dispositivo</span><span class="sxs-lookup"><span data-stu-id="69667-135">Device Framework</span></span>

<span data-ttu-id="69667-136">Il lato dispositivo USB è responsabile della definizione del Framework del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-136">The USB device side is responsible for the definition of the device framework.</span></span> <span data-ttu-id="69667-137">Il Framework del dispositivo è suddiviso in tre categorie, come descritto nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="69667-137">The device framework is divided into three categories, as described in the following sections.</span></span>

### <a name="definition-of-the-components-of-the-device-framework"></a><span data-ttu-id="69667-138">Definizione dei componenti del Framework del dispositivo</span><span class="sxs-lookup"><span data-stu-id="69667-138">Definition of the Components of the Device Framework</span></span>

<span data-ttu-id="69667-139">La definizione di ogni componente del Framework del dispositivo è correlata alla natura del dispositivo e alle risorse usate dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-139">The definition of each component of the device framework is related to the nature of the device and the resources utilized by the device.</span></span> <span data-ttu-id="69667-140">Di seguito sono riportate le categorie principali.</span><span class="sxs-lookup"><span data-stu-id="69667-140">Following are the main categories.</span></span>

- <span data-ttu-id="69667-141">Descrittore dispositivo</span><span class="sxs-lookup"><span data-stu-id="69667-141">Device Descriptor</span></span>
- <span data-ttu-id="69667-142">Descrittore di configurazione</span><span class="sxs-lookup"><span data-stu-id="69667-142">Configuration Descriptor</span></span>
- <span data-ttu-id="69667-143">Descrittore di interfaccia</span><span class="sxs-lookup"><span data-stu-id="69667-143">Interface Descriptor</span></span>
- <span data-ttu-id="69667-144">Descrittore dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="69667-144">Endpoint Descriptor</span></span>

<span data-ttu-id="69667-145">USBX supporta la definizione dei componenti del dispositivo sia per la velocità elevata che per quella completa (la velocità ridotta viene gestita allo stesso modo della velocità massima).</span><span class="sxs-lookup"><span data-stu-id="69667-145">USBX supports device component definition for both high and full speed (low speed being treated the same way as full speed).</span></span> <span data-ttu-id="69667-146">Ciò consente al dispositivo di funzionare in modo diverso quando si è connessi a un host ad alta velocità o a velocità intera.</span><span class="sxs-lookup"><span data-stu-id="69667-146">This allows the device to operate differently when connected to a high speed or full speed host.</span></span> <span data-ttu-id="69667-147">Le differenze tipiche sono le dimensioni di ogni endpoint e la potenza usata dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-147">The typical differences are the size of each endpoint and the power consumed by the device.</span></span>

<span data-ttu-id="69667-148">La definizione del componente del dispositivo assume il formato di una stringa di byte che segue la specifica USB.</span><span class="sxs-lookup"><span data-stu-id="69667-148">The definition of the device component takes the form of a byte string that follows the USB specification.</span></span> <span data-ttu-id="69667-149">La definizione è contigua e l'ordine in cui il Framework è rappresentato in memoria sarà uguale a quello restituito all'host durante l'enumerazione.</span><span class="sxs-lookup"><span data-stu-id="69667-149">The definition is contiguous and the order in which the framework is represented in memory will be the same as the one returned to the host during enumeration.</span></span>

<span data-ttu-id="69667-150">Di seguito è riportato un esempio di un Framework di dispositivi per un disco flash USB ad alta velocità.</span><span class="sxs-lookup"><span data-stu-id="69667-150">Following is an example of a device framework for a high speed USB Flash Disk.</span></span>

```c
#define DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED 60
UCHAR device_framework_high_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40, 0x0a, 0x07, 0x25, 0x40, 0x01, 0x00, 0x01, 0x02, 0x03, 0x01,

    /* Device qualifier descriptor */
    0x0a, 0x06, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40, 0x01, 0x00,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0, 0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50, 0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x00, 0x02, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x00, 0x02, 0x00
};
```

### <a name="definition-of-the-strings-of-the-device-framework"></a><span data-ttu-id="69667-151">Definizione delle stringhe del Framework del dispositivo</span><span class="sxs-lookup"><span data-stu-id="69667-151">Definition of the Strings of the Device Framework</span></span>

<span data-ttu-id="69667-152">Le stringhe sono facoltative in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-152">Strings are optional in a device.</span></span> <span data-ttu-id="69667-153">Il loro scopo è consentire all'host USB di conoscere il produttore del dispositivo, il nome del prodotto e il numero di revisione tramite stringhe Unicode.</span><span class="sxs-lookup"><span data-stu-id="69667-153">Their purpose is to let the USB host know about the manufacturer of the device, the product name, and the revision number through Unicode strings.</span></span>

<span data-ttu-id="69667-154">Le stringhe principali sono indici incorporati nei descrittori di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-154">The main strings are indexes embedded in the device descriptors.</span></span> <span data-ttu-id="69667-155">Gli indici di stringhe aggiuntive possono essere incorporati in interfacce singole.</span><span class="sxs-lookup"><span data-stu-id="69667-155">Additional strings indexes can be embedded into individual interfaces.</span></span>

<span data-ttu-id="69667-156">Supponendo che il Framework del dispositivo precedente includa tre indici stringa incorporati nel descrittore del dispositivo, la definizione di Framework di stringa potrebbe essere simile a questo codice di esempio</span><span class="sxs-lookup"><span data-stu-id="69667-156">Assuming the device framework above has three string indexes embedded into the device descriptor, the string framework definition could look like this example code.</span></span>

```c
/* String Device Framework:
    Byte 0 and 1: Word containing the language ID: 0x0904 for US
    Byte 2 : Byte containing the index of the descriptor
    Byte 3 : Byte containing the length of the descriptor string
*/

#define STRING_FRAMEWORK_LENGTH 38 UCHAR string_framework[] = {
    /* Manufacturer string descriptor: Index 1 */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72, 0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,

    /* Product string descriptor: Index 2 */
    0x09, 0x04, 0x02, 0x0c,
    0x4D, 0x4C, 0x36, 0x39, 0x36, 0x35, 0x30, 0x30,
    0x20, 0x53, 0x44, 0x4B,

    /* Serial Number string descriptor: Index 3 */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31
};
```

<span data-ttu-id="69667-157">Se per ogni velocità è necessario usare stringhe diverse, è necessario usare indici diversi perché gli indici sono indipendenti dalla velocità.</span><span class="sxs-lookup"><span data-stu-id="69667-157">If different strings have to be used for each speed, different indexes must be used as the indexes are speed agnostic.</span></span>

<span data-ttu-id="69667-158">La codifica della stringa è basata su UNICODE.</span><span class="sxs-lookup"><span data-stu-id="69667-158">The encoding of the string is UNICODE-based.</span></span> <span data-ttu-id="69667-159">Per ulteriori informazioni sullo standard di codifica UNICODE, fare riferimento alla pubblicazione seguente:</span><span class="sxs-lookup"><span data-stu-id="69667-159">For more information on the UNICODE encoding standard refer to the following publication:</span></span>

<span data-ttu-id="69667-160">*Lo standard Unicode, la codifica dei caratteri in tutto il mondo, la versione 1., i volumi 1 e 2, Unicode Consortium, Addison-Wesley Publishing Company, Reading MA.*</span><span class="sxs-lookup"><span data-stu-id="69667-160">*The Unicode Standard, Worldwide Character Encoding, Version 1., Volumes 1 and 2, The Unicode Consortium, Addison-Wesley Publishing Company, Reading MA.*</span></span>

### <a name="definition-of-the-languages-supported-by-the-device-for-each-string"></a><span data-ttu-id="69667-161">Definizione delle lingue supportate dal dispositivo per ogni stringa</span><span class="sxs-lookup"><span data-stu-id="69667-161">Definition of the Languages Supported by the Device for each String</span></span>

<span data-ttu-id="69667-162">USBX è in grado di supportare più lingue, anche se la lingua inglese è quella predefinita.</span><span class="sxs-lookup"><span data-stu-id="69667-162">USBX has the ability to support multiple languages although English is the default.</span></span> <span data-ttu-id="69667-163">La definizione di ogni lingua per i descrittori di stringa è sotto forma di una matrice di definizioni di linguaggi definita come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="69667-163">The definition of each language for the string descriptors is in the form of an array of languages definition defined as follows.</span></span>

```c
#define LANGUAGE_ID_FRAMEWORK_LENGTH 2
UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

<span data-ttu-id="69667-164">Per supportare altre lingue, è sufficiente aggiungere la definizione a doppio byte del codice della lingua dopo il codice inglese predefinito.</span><span class="sxs-lookup"><span data-stu-id="69667-164">To support additional languages, simply add the language code double-byte definition after the default English code.</span></span> <span data-ttu-id="69667-165">Il codice della lingua è stato definito da Microsoft nel documento.</span><span class="sxs-lookup"><span data-stu-id="69667-165">The language code has been defined by Microsoft in the document.</span></span>

<span data-ttu-id="69667-166">*Sviluppo di software internazionale per Windows 95 e Windows NT, Nadine Kano, Microsoft Press, Redmond WA*</span><span class="sxs-lookup"><span data-stu-id="69667-166">*Developing International Software for Windows 95 and Windows NT, Nadine Kano, Microsoft Press, Redmond WA*</span></span>

## <a name="vbus-manager"></a><span data-ttu-id="69667-167">Gestione VBUS</span><span class="sxs-lookup"><span data-stu-id="69667-167">VBUS Manager</span></span>

<span data-ttu-id="69667-168">Nella maggior parte delle progettazioni di dispositivi USB, VBUS non fa parte del dispositivo USB core, ma piuttosto connesso a un GPIO esterno, che monitora il segnale di linea.</span><span class="sxs-lookup"><span data-stu-id="69667-168">In most USB device designs, VBUS is not part of the USB Device core but rather connected to an external GPIO, which monitors the line signal.</span></span>

<span data-ttu-id="69667-169">Di conseguenza, VBUS deve essere gestito separatamente dal driver del controller del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-169">As a result, VBUS has to be managed separately from the device controller driver.</span></span>

<span data-ttu-id="69667-170">Spetta all'applicazione fornire il controller del dispositivo con l'indirizzo del VBUS IO.</span><span class="sxs-lookup"><span data-stu-id="69667-170">It is up to the application to provide the device controller with the address of the VBUS IO.</span></span> <span data-ttu-id="69667-171">VBUS deve essere inizializzato prima dell'inizializzazione del controller del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69667-171">VBUS must be initialized prior to the device controller initialization.</span></span>

<span data-ttu-id="69667-172">A seconda della specifica della piattaforma per il monitoraggio di VBUS, è possibile consentire al driver del controller di gestire i segnali VBUS dopo che l'i/o VBUS è stato inizializzato o, se ciò non è possibile, l'applicazione deve fornire il codice per la gestione di VBUS.</span><span class="sxs-lookup"><span data-stu-id="69667-172">Depending on the platform specification for monitoring VBUS, it is possible to let the controller driver handle VBUS signals after the VBUS IO is initialized or if this is not possible, the application has to provide the code for handling VBUS.</span></span>

<span data-ttu-id="69667-173">Se l'applicazione desidera gestire VBUS autonomamente, l'unico requisito consiste nel chiamare la funzione ***ux_device_stack_disconnect*** quando viene rilevato che un dispositivo è stato estratto.</span><span class="sxs-lookup"><span data-stu-id="69667-173">If the application wishes to handle VBUS by itself, its only requirement is to call the function ***ux_device_stack_disconnect*** when it detects that a device has been extracted.</span></span> <span data-ttu-id="69667-174">Non è necessario informare il controller quando viene inserito un dispositivo perché il controller verrà riattivato quando viene rilevato il segnale di reimpostazione del BUS di asserzione/deasserzione.</span><span class="sxs-lookup"><span data-stu-id="69667-174">It is not necessary to inform the controller when a device is inserted because the controller will wake up when the BUS RESET assert/deassert signal is detected.</span></span>
