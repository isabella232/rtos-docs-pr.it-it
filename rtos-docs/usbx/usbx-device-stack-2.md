---
title: Capitolo 2-installazione dello stack di dispositivi USBX di Azure RTO
description: Informazioni su come installare lo stack di dispositivi USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 62f036af27c5da29baf9cba58b5b26631167c3a1
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377153"
---
# <a name="chapter-2---azure-rtos-usbx-device-stack-installation"></a><span data-ttu-id="6b487-103">Capitolo 2-installazione dello stack di dispositivi USBX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="6b487-103">Chapter 2 - Azure RTOS USBX Device Stack Installation</span></span>

## <a name="host-considerations"></a><span data-ttu-id="6b487-104">Considerazioni sull'host</span><span class="sxs-lookup"><span data-stu-id="6b487-104">Host Considerations</span></span>

### <a name="computer-type"></a><span data-ttu-id="6b487-105">Tipo computer</span><span class="sxs-lookup"><span data-stu-id="6b487-105">Computer Type</span></span>

<span data-ttu-id="6b487-106">Lo sviluppo incorporato viene in genere eseguito nei computer host Windows o UNIX.</span><span class="sxs-lookup"><span data-stu-id="6b487-106">Embedded development is usually performed on Windows PC or Unix host computers.</span></span> <span data-ttu-id="6b487-107">Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6b487-107">After the application is compiled, linked, and located on the host, it is downloaded to the target hardware for execution.</span></span>

### <a name="download-interfaces"></a><span data-ttu-id="6b487-108">Interfacce di download</span><span class="sxs-lookup"><span data-stu-id="6b487-108">Download Interfaces</span></span>

<span data-ttu-id="6b487-109">Il download di destinazione viene in genere eseguito tramite un'interfaccia seriale RS-232, sebbene le interfacce parallele, USB e Ethernet stiano diventando più diffuse.</span><span class="sxs-lookup"><span data-stu-id="6b487-109">Usually the target download is done over an RS-232 serial interface, although parallel interfaces, USB, and Ethernet are becoming more popular.</span></span> <span data-ttu-id="6b487-110">Per le opzioni disponibili, vedere la documentazione dello strumento di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6b487-110">See the development tool documentation for available options.</span></span>

### <a name="debugging-tools"></a><span data-ttu-id="6b487-111">Strumenti di debug</span><span class="sxs-lookup"><span data-stu-id="6b487-111">Debugging Tools</span></span>

<span data-ttu-id="6b487-112">Il debug viene eseguito in genere sullo stesso collegamento del download dell'immagine del programma.</span><span class="sxs-lookup"><span data-stu-id="6b487-112">Debugging is done typically over the same link as the program image download.</span></span> <span data-ttu-id="6b487-113">Sono disponibili diversi debugger, a partire da piccoli programmi di monitoraggio in esecuzione nella destinazione tramite il monitoraggio di debug in background (BDM) e gli strumenti di In-Circuit Emulator (ICE).</span><span class="sxs-lookup"><span data-stu-id="6b487-113">A variety of debuggers exist, ranging from small monitor programs running on the target through Background Debug Monitor (BDM) and In-Circuit Emulator (ICE) tools.</span></span> <span data-ttu-id="6b487-114">Lo strumento ICE fornisce il debug più affidabile dell'hardware di destinazione effettivo.</span><span class="sxs-lookup"><span data-stu-id="6b487-114">The ICE tool provides the most robust debugging of actual target hardware.</span></span>

### <a name="required-hard-disk-space"></a><span data-ttu-id="6b487-115">Spazio su disco rigido richiesto</span><span class="sxs-lookup"><span data-stu-id="6b487-115">Required Hard Disk Space</span></span>

<span data-ttu-id="6b487-116">Il codice sorgente per USBX viene fornito in formato ASCII e richiede circa 500 KB di spazio sul disco rigido del computer host.</span><span class="sxs-lookup"><span data-stu-id="6b487-116">The source code for USBX is delivered in ASCII format and requires approximately 500 KBytes of space on the host computer's hard disk.</span></span>

### <a name="target-considerations"></a><span data-ttu-id="6b487-117">Considerazioni sulla destinazione</span><span class="sxs-lookup"><span data-stu-id="6b487-117">Target Considerations</span></span>

<span data-ttu-id="6b487-118">USBX richiede tra 24 KByte e 64 Kbyte di memoria di sola lettura (ROM) nella destinazione in modalità host.</span><span class="sxs-lookup"><span data-stu-id="6b487-118">USBX requires between 24 KBytes and 64 KBytes of Read Only Memory (ROM) on the target in host mode.</span></span> <span data-ttu-id="6b487-119">La quantità di memoria richiesta dipende dal tipo di controller usato e dalle classi USB collegate a USBX.</span><span class="sxs-lookup"><span data-stu-id="6b487-119">The amount of memory required is dependent on the type of controller used and the USB classes linked to USBX.</span></span> <span data-ttu-id="6b487-120">Sono necessari altri 32 KByte della memoria ad accesso casuale (RAM) della destinazione per le strutture di dati globali USBX e il pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="6b487-120">Another 32 KBytes of the target's Random Access Memory (RAM) are required for USBX global data structures and memory pool.</span></span> <span data-ttu-id="6b487-121">È anche possibile modificare questo pool di memoria in base al numero previsto di dispositivi sul dispositivo USB e al tipo di controller USB.</span><span class="sxs-lookup"><span data-stu-id="6b487-121">This memory pool can also be adjusted depending on the expected number of devices on the USB and the type of USB controller.</span></span> <span data-ttu-id="6b487-122">Il lato dispositivo USBX richiede circa 10-12 K di ROM a seconda del tipo di controller del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6b487-122">The USBX device side requires roughly 10-12 K of ROM depending on the type of device controller.</span></span> <span data-ttu-id="6b487-123">L'utilizzo della memoria RAM dipende dal tipo di classe emulata dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6b487-123">The RAM memory usage depends on the type of class emulated by the device.</span></span>

<span data-ttu-id="6b487-124">USBX si basa anche su semafori, mutex e thread ThreadX per la protezione di più thread e la sospensione di I/O e l'elaborazione periodica per il monitoraggio della topologia del bus USB.</span><span class="sxs-lookup"><span data-stu-id="6b487-124">USBX also relies on ThreadX semaphores, mutexes, and threads for multiple thread protection, and I/O suspension and periodic processing for monitoring the USB bus topology.</span></span>

### <a name="product-distribution"></a><span data-ttu-id="6b487-125">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="6b487-125">Product Distribution</span></span>

<span data-ttu-id="6b487-126">Azure RTO USBX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/usbx/> .</span><span class="sxs-lookup"><span data-stu-id="6b487-126">Azure RTOS USBX can be obtained from our public source code repository at <https://github.com/azure-rtos/usbx/>.</span></span>

<span data-ttu-id="6b487-127">Di seguito è riportato un elenco di diversi file importanti nel repository.</span><span class="sxs-lookup"><span data-stu-id="6b487-127">The following is a list of several important files in the repository.</span></span>

* <span data-ttu-id="6b487-128">***ux_api. h***: questo file di intestazione C contiene tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.</span><span class="sxs-lookup"><span data-stu-id="6b487-128">***ux_api.h***: This C header file contains all system equates, data structures, and service prototypes.</span></span>
* <span data-ttu-id="6b487-129">***ux_port. h***: questo file di intestazione C contiene tutte le definizioni e le strutture dei dati specifici dello strumento di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6b487-129">***ux_port.h***: This C header file contains all development-tool-specific data definitions and structures.</span></span>
* <span data-ttu-id="6b487-130">***UX. lib***: è la versione binaria della libreria C di USBX.</span><span class="sxs-lookup"><span data-stu-id="6b487-130">***ux.lib***:  This is the binary version of the USBX C library.</span></span> <span data-ttu-id="6b487-131">Viene distribuito con il pacchetto standard.</span><span class="sxs-lookup"><span data-stu-id="6b487-131">It is distributed with the standard package.</span></span>
* <span data-ttu-id="6b487-132">***demo_usbx. c***: il file c contenente una demo USBX semplice</span><span class="sxs-lookup"><span data-stu-id="6b487-132">***demo_usbx.c***: The C file containing a simple USBX demo</span></span>

<span data-ttu-id="6b487-133">Tutti i nomi di file sono in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="6b487-133">All filenames are in lower-case.</span></span> <span data-ttu-id="6b487-134">Questa convenzione di denominazione rende più semplice convertire i comandi in piattaforme di sviluppo Unix.</span><span class="sxs-lookup"><span data-stu-id="6b487-134">This naming convention makes it easier to convert the commands to Unix development platforms.</span></span>

## <a name="usbx-installation"></a><span data-ttu-id="6b487-135">Installazione di USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-135">USBX Installation</span></span>

<span data-ttu-id="6b487-136">USBX viene installato clonando il repository GitHub nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="6b487-136">USBX is installed by cloning the GitHub repository to your local machine.</span></span> <span data-ttu-id="6b487-137">Di seguito è riportata la sintassi tipica per la creazione di un clone del repository USBX nel PC:</span><span class="sxs-lookup"><span data-stu-id="6b487-137">The following is typical syntax for creating a clone of the USBX repository on your PC:</span></span>

```c
    git clone https://github.com/azure-rtos/usbx
```

<span data-ttu-id="6b487-138">In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.</span><span class="sxs-lookup"><span data-stu-id="6b487-138">Alternatively you can download a copy of the repository using the download button on the GitHub main page.</span></span>

<span data-ttu-id="6b487-139">Sono inoltre disponibili istruzioni per la compilazione della libreria USBX nella pagina iniziale del repository online.</span><span class="sxs-lookup"><span data-stu-id="6b487-139">You will also find instructions for building the USBX library on the front page of the online repository.</span></span>

<span data-ttu-id="6b487-140">Le istruzioni generali riportate di seguito si applicano praticamente a qualsiasi installazione:</span><span class="sxs-lookup"><span data-stu-id="6b487-140">The following general instructions apply to virtually any installation:</span></span>

1. <span data-ttu-id="6b487-141">Usare la stessa directory in cui è stato precedentemente installato ThreadX nel disco rigido host.</span><span class="sxs-lookup"><span data-stu-id="6b487-141">Use the same directory in which you previously installed ThreadX on the host hard drive.</span></span> <span data-ttu-id="6b487-142">Tutti i nomi di USBX sono univoci e non interferiscono con l'installazione precedente di USBX.</span><span class="sxs-lookup"><span data-stu-id="6b487-142">All USBX names are unique and will not interfere with the previous USBX installation.</span></span>
1. <span data-ttu-id="6b487-143">Aggiungere una chiamata a \***ux_system_initialize** _ all'inizio di _ *_tx_application_define_* \*.</span><span class="sxs-lookup"><span data-stu-id="6b487-143">Add a call to ***ux_system_initialize** _ at or near the beginning of _*_tx_application_define_\*\*.</span></span> <span data-ttu-id="6b487-144">Questa è la posizione in cui vengono inizializzate le risorse di USBX.</span><span class="sxs-lookup"><span data-stu-id="6b487-144">This is where the USBX resources are initialized.</span></span>
1. <span data-ttu-id="6b487-145">Aggiungere una chiamata a \*\**ux_device_stack_initialize *.**</span><span class="sxs-lookup"><span data-stu-id="6b487-145">Add a call to \***ux_device_stack_initialize\*.**</span></span>
1. <span data-ttu-id="6b487-146">Aggiungere una o più chiamate per inizializzare le classi USBX obbligatorie (classi host e/o dispositivi)</span><span class="sxs-lookup"><span data-stu-id="6b487-146">Add one or more calls to initialize the required USBX classes (either host and/or devices classes)</span></span>
1. <span data-ttu-id="6b487-147">Aggiungere una o più chiamate per inizializzare il controller del dispositivo disponibile nel sistema.</span><span class="sxs-lookup"><span data-stu-id="6b487-147">Add one or more calls to initialize the device controller available in the system.</span></span>
1. <span data-ttu-id="6b487-148">Potrebbe essere necessario modificare il file tx_low_level_initialize. c per aggiungere l'inizializzazione hardware di basso livello e il routing vettoriale di interrupt.</span><span class="sxs-lookup"><span data-stu-id="6b487-148">It may be required to modify the tx_low_level_initialize.c file to add low-level hardware initialization and interrupt vector routing.</span></span> <span data-ttu-id="6b487-149">Questo è specifico per la piattaforma hardware e non verrà discusso qui. |</span><span class="sxs-lookup"><span data-stu-id="6b487-149">This is specific to the hardware platform and will not be discussed here.|</span></span>
1. <span data-ttu-id="6b487-150">Compilare il codice sorgente dell'applicazione e il collegamento con le librerie di runtime USBX e ThreadX (FileX e/o NETX potrebbero essere necessari anche se la classe di archiviazione USB e/o le classi di rete USB devono essere compilate in), UX. a (o UX. lib) e TX. a (o TX. lib).</span><span class="sxs-lookup"><span data-stu-id="6b487-150">Compile application source code and link with the USBX and ThreadX run time libraries (FileX and/or Netx may also be required if the USB storage class and/or USB network classes are to be compiled in), ux.a (or ux.lib) and tx.a (or tx.lib).</span></span> <span data-ttu-id="6b487-151">Il risultato può essere scaricato nella destinazione ed eseguito.</span><span class="sxs-lookup"><span data-stu-id="6b487-151">The resulting can be downloaded to the target and executed!</span></span>

## <a name="configuration-options"></a><span data-ttu-id="6b487-152">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="6b487-152">Configuration Options</span></span>

<span data-ttu-id="6b487-153">Sono disponibili diverse opzioni di configurazione per la compilazione della libreria USBX.</span><span class="sxs-lookup"><span data-stu-id="6b487-153">There are several configuration options for building the USBX library.</span></span> <span data-ttu-id="6b487-154">Tutte le opzioni si trovano in ***ux_user. h***.</span><span class="sxs-lookup"><span data-stu-id="6b487-154">All options are located in the ***ux_user.h***.</span></span>

<span data-ttu-id="6b487-155">Nell'elenco seguente vengono illustrate tutte le opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6b487-155">The list below details each configuration option.</span></span>

| <span data-ttu-id="6b487-156">Opzione di configurazione &nbsp;</span><span class="sxs-lookup"><span data-stu-id="6b487-156">Configuration&nbsp;Option</span></span> | <span data-ttu-id="6b487-157">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b487-157">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b487-158">**UX_PERIODIC_RATE**</span><span class="sxs-lookup"><span data-stu-id="6b487-158">**UX_PERIODIC_RATE**</span></span> | <span data-ttu-id="6b487-159">Questo valore rappresenta il numero di cicli al secondo per una piattaforma hardware specifica.</span><span class="sxs-lookup"><span data-stu-id="6b487-159">This value represents how many ticks per seconds for a specific hardware platform.</span></span> <span data-ttu-id="6b487-160">Il valore predefinito è 1000 che indica 1 segno di cicli per millisecondo.</span><span class="sxs-lookup"><span data-stu-id="6b487-160">The default is 1000 indicating 1 tick per millisecond.</span></span> |
| <span data-ttu-id="6b487-161">**UX_THREAD_STACK_SIZE**</span><span class="sxs-lookup"><span data-stu-id="6b487-161">**UX_THREAD_STACK_SIZE**</span></span> | <span data-ttu-id="6b487-162">Questo valore corrisponde alla dimensione dello stack in byte per i thread USBX.</span><span class="sxs-lookup"><span data-stu-id="6b487-162">This value is the size of the stack in bytes for the USBX threads.</span></span> <span data-ttu-id="6b487-163">Può essere in genere 1024 byte o 2048 byte a seconda del processore usato e del controller host.</span><span class="sxs-lookup"><span data-stu-id="6b487-163">It can be typically 1024 bytes or 2048 bytes depending on the processor used and the host controller.</span></span> |
| <span data-ttu-id="6b487-164">**UX_THREAD_PRIORITY_ENUM**</span><span class="sxs-lookup"><span data-stu-id="6b487-164">**UX_THREAD_PRIORITY_ENUM**</span></span> | <span data-ttu-id="6b487-165">Si tratta del valore di priorità ThreadX per i thread di enumerazione USBX che monitora la topologia del bus.</span><span class="sxs-lookup"><span data-stu-id="6b487-165">This is the ThreadX priority value for the USBX enumeration threads that monitors the bus topology.</span></span> |
| <span data-ttu-id="6b487-166">**UX_THREAD_PRIORITY_CLASS**</span><span class="sxs-lookup"><span data-stu-id="6b487-166">**UX_THREAD_PRIORITY_CLASS**</span></span> | <span data-ttu-id="6b487-167">Si tratta del valore di priorità ThreadX per i thread USBX standard.</span><span class="sxs-lookup"><span data-stu-id="6b487-167">This is the ThreadX priority value for the standard USBX threads.</span></span> |
| <span data-ttu-id="6b487-168">**UX_THREAD_PRIORITY_KEYBOARD**</span><span class="sxs-lookup"><span data-stu-id="6b487-168">**UX_THREAD_PRIORITY_KEYBOARD**</span></span> | <span data-ttu-id="6b487-169">Si tratta del valore di priorità ThreadX per la classe della tastiera USBX HID.</span><span class="sxs-lookup"><span data-stu-id="6b487-169">This is the ThreadX priority value for the USBX HID keyboard class.</span></span> |
| <span data-ttu-id="6b487-170">**UX_THREAD_PRIORITY_DCD**</span><span class="sxs-lookup"><span data-stu-id="6b487-170">**UX_THREAD_PRIORITY_DCD**</span></span> | <span data-ttu-id="6b487-171">Si tratta del valore di priorità ThreadX per il thread del controller del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6b487-171">This is the ThreadX priority value for the device controller thread.</span></span> |
| <span data-ttu-id="6b487-172">**UX_NO_TIME_SLICE**</span><span class="sxs-lookup"><span data-stu-id="6b487-172">**UX_NO_TIME_SLICE**</span></span> | <span data-ttu-id="6b487-173">Questo valore definisce effettivamente l'intervallo di tempo che verrà usato per i thread.</span><span class="sxs-lookup"><span data-stu-id="6b487-173">This value actually defines the time slice that will be used for threads.</span></span> <span data-ttu-id="6b487-174">Se, ad esempio, viene definito su 0, la porta di destinazione ThreadX non utilizza intervalli di tempo.</span><span class="sxs-lookup"><span data-stu-id="6b487-174">For example, if defined to 0, the ThreadX target port does not use time slices.</span></span> |
| <span data-ttu-id="6b487-175">**UX_MAX_SLAVE_CLASS_DRIVER**</span><span class="sxs-lookup"><span data-stu-id="6b487-175">**UX_MAX_SLAVE_CLASS_DRIVER**</span></span> | <span data-ttu-id="6b487-176">Questo è il numero massimo di classi USBX che possono essere registrate tramite ux_device_stack_class_register.</span><span class="sxs-lookup"><span data-stu-id="6b487-176">This is the maximum number of USBX classes that can be registered via ux_device_stack_class_register.</span></span> |
| <span data-ttu-id="6b487-177">**UX_MAX_SLAVE_LUN**</span><span class="sxs-lookup"><span data-stu-id="6b487-177">**UX_MAX_SLAVE_LUN**</span></span> | <span data-ttu-id="6b487-178">Questo valore rappresenta il numero corrente di unità logiche SCSI rappresentate nel driver della classe di archiviazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6b487-178">This value represents the current number of SCSI logical units represented in the device storage class driver.</span></span> |
| <span data-ttu-id="6b487-179">**UX_SLAVE_CLASS_STORAGE_INCLUDE_MMC**</span><span class="sxs-lookup"><span data-stu-id="6b487-179">**UX_SLAVE_CLASS_STORAGE_INCLUDE_MMC**</span></span> | <span data-ttu-id="6b487-180">Se definito, la classe di archiviazione gestirà i comandi Multimedia (MMC), ovvero DVD-ROM.</span><span class="sxs-lookup"><span data-stu-id="6b487-180">If defined, the storage class will handle Multi-Media Commands (MMC) that is, DVD-ROM.</span></span> |
| <span data-ttu-id="6b487-181">**UX_DEVICE_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**</span><span class="sxs-lookup"><span data-stu-id="6b487-181">**UX_DEVICE_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**</span></span> | <span data-ttu-id="6b487-182">Questo valore rappresenta il numero di pacchetti NetX nel pool di pacchetti della classe CDC-ECM.</span><span class="sxs-lookup"><span data-stu-id="6b487-182">This value represents the number of NetX packets in the CDC-ECM class' packet pool.</span></span> <span data-ttu-id="6b487-183">Il valore predefinito è 16.</span><span class="sxs-lookup"><span data-stu-id="6b487-183">The default is 16.</span></span> |
| <span data-ttu-id="6b487-184">**UX_SLAVE_REQUEST_CONTROL_MAX_LENGTH**</span><span class="sxs-lookup"><span data-stu-id="6b487-184">**UX_SLAVE_REQUEST_CONTROL_MAX_LENGTH**</span></span> | <span data-ttu-id="6b487-185">Questo valore rappresenta il numero massimo di byte ricevuti su un endpoint di controllo nello stack del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6b487-185">This value represents the maximum number of bytes received on a control endpoint in the device stack.</span></span> <span data-ttu-id="6b487-186">Il valore predefinito è 256 byte, ma può essere ridotto in ambienti di vincoli di memoria.</span><span class="sxs-lookup"><span data-stu-id="6b487-186">The default is 256 bytes but can be reduced in memory constraint environments.</span></span> |
| <span data-ttu-id="6b487-187">**UX_DEVICE_CLASS_HID_EVENT_BUFFER_LENGTH**</span><span class="sxs-lookup"><span data-stu-id="6b487-187">**UX_DEVICE_CLASS_HID_EVENT_BUFFER_LENGTH**</span></span> | <span data-ttu-id="6b487-188">Questo valore rappresenta la lunghezza massima in byte di un report nascosto.</span><span class="sxs-lookup"><span data-stu-id="6b487-188">This value represents the maximum length in bytes of a HID report.</span></span> |
| <span data-ttu-id="6b487-189">**UX_DEVICE_CLASS_HID_MAX_EVENTS_QUEUE**</span><span class="sxs-lookup"><span data-stu-id="6b487-189">**UX_DEVICE_CLASS_HID_MAX_EVENTS_QUEUE**</span></span> | <span data-ttu-id="6b487-190">Questo valore rappresenta il numero massimo di report HID che possono essere accodati in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="6b487-190">This value represents the maximum number of HID reports that can be queued at once.</span></span> |
| <span data-ttu-id="6b487-191">**UX_SLAVE_REQUEST_DATA_MAX_LENGTH**</span><span class="sxs-lookup"><span data-stu-id="6b487-191">**UX_SLAVE_REQUEST_DATA_MAX_LENGTH**</span></span> | <span data-ttu-id="6b487-192">Questo valore rappresenta il numero massimo di byte ricevuti in un endpoint bulk nello stack del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6b487-192">This value represents the maximum number of bytes received on a bulk endpoint in the device stack.</span></span> <span data-ttu-id="6b487-193">Il valore predefinito è 4096 byte, ma può essere ridotto in ambienti di vincoli di memoria.</span><span class="sxs-lookup"><span data-stu-id="6b487-193">The default is 4096 bytes but can be reduced in memory constraint environments.</span></span> |

## <a name="source-code-tree"></a><span data-ttu-id="6b487-194">Albero del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="6b487-194">Source Code Tree</span></span>

<span data-ttu-id="6b487-195">I file USBX sono disponibili in più directory.</span><span class="sxs-lookup"><span data-stu-id="6b487-195">The USBX files are provided in several directories.</span></span>

![Albero del codice sorgente](media/usbx-device-stack/source-code-tree.png)

<span data-ttu-id="6b487-197">Per rendere i file riconoscibili con i rispettivi nomi, è stata adottata la convenzione seguente:</span><span class="sxs-lookup"><span data-stu-id="6b487-197">In order to make the files recognizable by their names, the following convention has been adopted:</span></span>

| <span data-ttu-id="6b487-198">Nome suffisso file</span><span class="sxs-lookup"><span data-stu-id="6b487-198">File Suffix Name</span></span>  | <span data-ttu-id="6b487-199">Descrizione file</span><span class="sxs-lookup"><span data-stu-id="6b487-199">File description</span></span>                          |
| ----------------- | ----------------------------------------- |
| <span data-ttu-id="6b487-200">ux_host_stack</span><span class="sxs-lookup"><span data-stu-id="6b487-200">ux_host_stack</span></span>   | <span data-ttu-id="6b487-201">USBX file core dello stack host</span><span class="sxs-lookup"><span data-stu-id="6b487-201">usbx host stack core files</span></span>                |
| <span data-ttu-id="6b487-202">ux_host_class</span><span class="sxs-lookup"><span data-stu-id="6b487-202">ux_host_class</span></span>   | <span data-ttu-id="6b487-203">file delle classi dello stack host USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-203">usbx host stack classes files</span></span>             |
| <span data-ttu-id="6b487-204">ux_hcd</span><span class="sxs-lookup"><span data-stu-id="6b487-204">ux_hcd</span></span>           | <span data-ttu-id="6b487-205">file driver del controller dello stack host USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-205">usbx host stack controller driver files</span></span>   |
| <span data-ttu-id="6b487-206">ux_device_stack</span><span class="sxs-lookup"><span data-stu-id="6b487-206">ux_device_stack</span></span> | <span data-ttu-id="6b487-207">file principali dello stack di dispositivi USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-207">usbx device stack core files</span></span>              |
| <span data-ttu-id="6b487-208">ux_device_class</span><span class="sxs-lookup"><span data-stu-id="6b487-208">ux_device_class</span></span> | <span data-ttu-id="6b487-209">file delle classi dello stack del dispositivo USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-209">usbx device stack classes files</span></span>           |
| <span data-ttu-id="6b487-210">ux_dcd</span><span class="sxs-lookup"><span data-stu-id="6b487-210">ux_dcd</span></span>           | <span data-ttu-id="6b487-211">file driver del controller dello stack del dispositivo USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-211">usbx device stack controller driver files</span></span> |
| <span data-ttu-id="6b487-212">ux_otg</span><span class="sxs-lookup"><span data-stu-id="6b487-212">ux_otg</span></span>           | <span data-ttu-id="6b487-213">file correlati driver del controller USBX OTG</span><span class="sxs-lookup"><span data-stu-id="6b487-213">usbx otg controller driver related files</span></span>  |
| <span data-ttu-id="6b487-214">ux_pictbridge</span><span class="sxs-lookup"><span data-stu-id="6b487-214">ux_pictbridge</span></span>    | <span data-ttu-id="6b487-215">file PictBridge USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-215">usbx pictbridge files</span></span>                     |
| <span data-ttu-id="6b487-216">ux_utility</span><span class="sxs-lookup"><span data-stu-id="6b487-216">ux_utility</span></span>       | <span data-ttu-id="6b487-217">funzioni di utilità USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-217">usbx utility functions</span></span>                    |
| <span data-ttu-id="6b487-218">demo_usbx</span><span class="sxs-lookup"><span data-stu-id="6b487-218">demo_usbx</span></span>        | <span data-ttu-id="6b487-219">file dimostrativi per USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-219">demonstration files for USBX</span></span>              |

## <a name="initialization-of-usbx-resources"></a><span data-ttu-id="6b487-220">Inizializzazione delle risorse di USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-220">Initialization of USBX resources</span></span>

<span data-ttu-id="6b487-221">USBX dispone di un proprio gestore della memoria.</span><span class="sxs-lookup"><span data-stu-id="6b487-221">USBX has its own memory manager.</span></span> <span data-ttu-id="6b487-222">La memoria deve essere allocata a USBX prima che il lato host o dispositivo di USBX venga inizializzato.</span><span class="sxs-lookup"><span data-stu-id="6b487-222">The memory needs to be allocated to USBX before the host or device side of USBX is initialized.</span></span> <span data-ttu-id="6b487-223">Il gestore della memoria USBX può supportare i sistemi in cui è possibile memorizzare nella cache la memoria.</span><span class="sxs-lookup"><span data-stu-id="6b487-223">USBX memory manager can accommodate systems where memory can be cached.</span></span>

<span data-ttu-id="6b487-224">La funzione seguente inizializza le risorse di memoria USBX con 128 K di memoria normale e nessun pool separato per la memoria sicura della cache:</span><span class="sxs-lookup"><span data-stu-id="6b487-224">The following function initializes USBX memory resources with 128 K of regular memory and no separate pool for cache safe memory:</span></span>

```c
/* Initialize USBX Memory */
ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

<span data-ttu-id="6b487-225">Il prototipo per la ux_system_initialize è il seguente:</span><span class="sxs-lookup"><span data-stu-id="6b487-225">The prototype for the ux_system_initialize is as follows:</span></span>

```c
UINT ux_system_initialize(VOID *regular_memory_pool_start,
        ULONG regular_memory_size,
        VOID *cache_safe_memory_pool_start,
        ULONG cache_safe_memory_size);
```

<span data-ttu-id="6b487-226">Parametri di input:</span><span class="sxs-lookup"><span data-stu-id="6b487-226">Input parameters:</span></span>

| <span data-ttu-id="6b487-227">Parametro</span><span class="sxs-lookup"><span data-stu-id="6b487-227">Parameter</span></span>                          | <span data-ttu-id="6b487-228">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b487-228">Description</span></span>                             |
| ---------------------------------- | --------------------------------------- |
| <span data-ttu-id="6b487-229">VOID \* regular_memory_pool_start</span><span class="sxs-lookup"><span data-stu-id="6b487-229">VOID \*regular_memory_pool_start</span></span>    | <span data-ttu-id="6b487-230">Inizio del pool di memoria normale</span><span class="sxs-lookup"><span data-stu-id="6b487-230">Beginning of the regular memory pool</span></span>    |
| <span data-ttu-id="6b487-231">Regular_memory_size ULONG</span><span class="sxs-lookup"><span data-stu-id="6b487-231">ULONG regular_memory_size</span></span>          | <span data-ttu-id="6b487-232">Dimensioni del pool di memoria normale</span><span class="sxs-lookup"><span data-stu-id="6b487-232">Size of the regular memory pool</span></span>         |
| <span data-ttu-id="6b487-233">VOID \* cache_safe_memory_pool_start</span><span class="sxs-lookup"><span data-stu-id="6b487-233">VOID \*cache_safe_memory_pool_start</span></span> | <span data-ttu-id="6b487-234">Inizio del pool di memoria sicuro della cache</span><span class="sxs-lookup"><span data-stu-id="6b487-234">Beginning of the cache safe memory pool</span></span> |
| <span data-ttu-id="6b487-235">Cache_safe_memory_size ULONG</span><span class="sxs-lookup"><span data-stu-id="6b487-235">ULONG cache_safe_memory_size</span></span>       | <span data-ttu-id="6b487-236">Dimensioni del pool di memoria sicuro della cache</span><span class="sxs-lookup"><span data-stu-id="6b487-236">Size of the cache safe memory pool</span></span>      |

<span data-ttu-id="6b487-237">Non tutti i sistemi richiedono la definizione di memoria protetta dalla cache.</span><span class="sxs-lookup"><span data-stu-id="6b487-237">Not all systems require the definition of cache safe memory.</span></span> <span data-ttu-id="6b487-238">In tale sistema, i valori passati durante l'inizializzazione per il puntatore di memoria verranno impostati su UX_NULL e le dimensioni del pool su 0.</span><span class="sxs-lookup"><span data-stu-id="6b487-238">In such a system, the values passed during the initialization for the memory pointer will be set to UX_NULL and the size of the pool to 0.</span></span> <span data-ttu-id="6b487-239">USBX utilizzerà quindi il normale pool di memoria anziché il pool di sicurezza della cache.</span><span class="sxs-lookup"><span data-stu-id="6b487-239">USBX will then use the regular memory pool in lieu of the cache safe pool.</span></span>

<span data-ttu-id="6b487-240">In un sistema in cui la memoria normale non è protetta dalla cache e un controller richiede per eseguire la memoria DMA è necessario definire un pool di memoria in un'area di sicurezza della cache.</span><span class="sxs-lookup"><span data-stu-id="6b487-240">In a system where the regular memory is not cache safe and a controller requires to perform DMA memory it is necessary to define a memory pool in a cache safe zone.</span></span>

## <a name="uninitialization-of-usbx-resources"></a><span data-ttu-id="6b487-241">Inizializzazione delle risorse di USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-241">Uninitialization of USBX resources</span></span>

<span data-ttu-id="6b487-242">USBX può essere terminato rilasciando le risorse.</span><span class="sxs-lookup"><span data-stu-id="6b487-242">USBX can be terminated by releasing its resources.</span></span> <span data-ttu-id="6b487-243">Prima di terminare il USBX, tutte le classi e le risorse del controller devono essere terminate correttamente.</span><span class="sxs-lookup"><span data-stu-id="6b487-243">Prior to terminating usbx, all classes and controller resources need to be terminated properly.</span></span> <span data-ttu-id="6b487-244">La funzione seguente consente di uninizializzare le risorse di memoria USBX:</span><span class="sxs-lookup"><span data-stu-id="6b487-244">The following function uninitializes USBX memory resources:</span></span>

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

<span data-ttu-id="6b487-245">Il prototipo per la ux_system_initialize è il seguente:</span><span class="sxs-lookup"><span data-stu-id="6b487-245">The prototype for the ux_system_initialize is as follows:</span></span>

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-device-controller"></a><span data-ttu-id="6b487-246">Definizione del controller del dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="6b487-246">Definition of USB Device Controller</span></span>

<span data-ttu-id="6b487-247">Per il funzionamento in modalità dispositivo è possibile definire un solo controller di dispositivo USB in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="6b487-247">Only one USB device controller can be defined at any time to operate in device mode.</span></span> <span data-ttu-id="6b487-248">Il file di inizializzazione dell'applicazione deve contenere questa definizione.</span><span class="sxs-lookup"><span data-stu-id="6b487-248">The application initialization file should contain this definition.</span></span> <span data-ttu-id="6b487-249">La riga seguente esegue la definizione di un controller USB generico:</span><span class="sxs-lookup"><span data-stu-id="6b487-249">The following line performs the definition of a generic usb controller:</span></span>

```c
ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);
```

<span data-ttu-id="6b487-250">L'inizializzazione del dispositivo USB presenta il seguente prototipo:</span><span class="sxs-lookup"><span data-stu-id="6b487-250">The USB device initialization has the following prototype:</span></span>

```c
UINT ux_dcd_controller_initialize(ULONG dcd_io,
    ULONG dcd_irq, ULONG dcd_vbus_address);
```

<span data-ttu-id="6b487-251">con i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b487-251">with the following parameters:</span></span>

| <span data-ttu-id="6b487-252">Pararmeter</span><span class="sxs-lookup"><span data-stu-id="6b487-252">Pararmeter</span></span>               | <span data-ttu-id="6b487-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6b487-253">Description</span></span>                      |
| ------------------------ | -------------------------------- |
| <span data-ttu-id="6b487-254">Dcd_io ULONG</span><span class="sxs-lookup"><span data-stu-id="6b487-254">ULONG dcd_io</span></span>            | <span data-ttu-id="6b487-255">Indirizzo dell'IO del controller</span><span class="sxs-lookup"><span data-stu-id="6b487-255">Address of the controller IO</span></span>     |
| <span data-ttu-id="6b487-256">Dcd_irq ULONG</span><span class="sxs-lookup"><span data-stu-id="6b487-256">ULONG dcd_irq</span></span>           | <span data-ttu-id="6b487-257">Interrupt utilizzato dal controller</span><span class="sxs-lookup"><span data-stu-id="6b487-257">Interrupt used by the controller</span></span> |
| <span data-ttu-id="6b487-258">Dcd_vbus_address ULONG</span><span class="sxs-lookup"><span data-stu-id="6b487-258">ULONG dcd_vbus_address</span></span> | <span data-ttu-id="6b487-259">Indirizzo del GPIO VBUS</span><span class="sxs-lookup"><span data-stu-id="6b487-259">Address of the VBUS GPIO</span></span>         |

<span data-ttu-id="6b487-260">L'esempio seguente è l'inizializzazione di USBX in modalità dispositivo con la classe del dispositivo di archiviazione e un controller generico:</span><span class="sxs-lookup"><span data-stu-id="6b487-260">The following example is the initialization of USBX in device mode with the storage device class and a generic controller:</span></span>

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024), 0, 0);

/* The code below is required for installing the device portion of USBX */
status = ux_device_stack_initialize(&device_framework_high_speed,
    DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED, &device_framework_full_speed,
    DEVICE_FRAMEWORK_LENGTH_FULL_SPEED, &string_framework,
    STRING_FRAMEWORK_LENGTH, &language_id_framework,
    LANGUAGE_ID_FRAMEWORK_LENGTH, UX_NULL);

/* If status equals UX_SUCCESS, installation was successful. */

/* Store the number of LUN in this device storage instance: single LUN. */
storage_parameter.ux_slave_class_storage_parameter_number_lun = 1;

/* Initialize the storage class parameters for reading/writing to the Flash Disk. */
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_last_lba = 0x1e6bfe;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_block_length = 512;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_type = 0;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_removable_flag = 0x80;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read = tx_demo_thread_flash_media_read;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_write = tx_demo_thread_flash_media_write;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_status = tx_demo_thread_flash_media_status;

/* Initialize the device storage class. The class is connected with interface 0 */
status = ux_device_stack_class_register(ux_system_slave_class_storage_name ux_device_class_storage_entry,
    ux_device_class_storage_thread,0, (VOID *)&storage_parameter);

/* Register the device controllers available in this system */
status = ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);

/* If status equals UX_SUCCESS, registration was successful. */
```

## <a name="troubleshooting"></a><span data-ttu-id="6b487-261">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="6b487-261">Troubleshooting</span></span>

<span data-ttu-id="6b487-262">USBX viene fornito con un file dimostrativo e un ambiente di simulazione.</span><span class="sxs-lookup"><span data-stu-id="6b487-262">USBX is delivered with a demonstration file and a simulation environment.</span></span> <span data-ttu-id="6b487-263">È sempre consigliabile ottenere prima di tutto la piattaforma dimostrativa, sia nell'hardware di destinazione che in una piattaforma dimostrativa specifica.</span><span class="sxs-lookup"><span data-stu-id="6b487-263">It is always a good idea to get the demonstration platform running first—either on the target hardware or a specific demonstration platform.</span></span>

## <a name="usbx-version-id"></a><span data-ttu-id="6b487-264">ID versione USBX</span><span class="sxs-lookup"><span data-stu-id="6b487-264">USBX Version ID</span></span>

<span data-ttu-id="6b487-265">La versione corrente di USBX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6b487-265">The current version of USBX is available both to the user and the application software during run-time.</span></span> <span data-ttu-id="6b487-266">Il programmatore può ottenere la versione di USBX dall'esame del file \***ux_port. h** _.</span><span class="sxs-lookup"><span data-stu-id="6b487-266">The programmer can obtain the USBX version from examination of the \***ux_port.h** _ file.</span></span> <span data-ttu-id="6b487-267">Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente.</span><span class="sxs-lookup"><span data-stu-id="6b487-267">In addition, this file also contains a version history of the corresponding port.</span></span> <span data-ttu-id="6b487-268">Il software applicativo può ottenere la versione di USBX esaminando la stringa globale _ *_ _ux_version_id_* _, definita in _ *_ux_port. h_* \*.</span><span class="sxs-lookup"><span data-stu-id="6b487-268">Application software can obtain the USBX version by examining the global string _ *_ _ux_version_id_* _, which is defined in _\*_ux_port.h_\*\*.</span></span>
