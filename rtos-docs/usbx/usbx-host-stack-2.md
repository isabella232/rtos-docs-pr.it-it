---
title: Capitolo 2-installazione dello stack host di Azure RTO USBX
description: Informazioni su come installare lo stack host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 4c33f95b8ac268c557fd947a1303ec3af315a37e
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377085"
---
# <a name="chapter-2---azure-rtos-usbx-host-stack-installation"></a><span data-ttu-id="9e833-103">Capitolo 2-installazione dello stack host di Azure RTO USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-103">Chapter 2 - Azure RTOS USBX Host Stack Installation</span></span>

## <a name="host-considerations"></a><span data-ttu-id="9e833-104">Considerazioni sull'host</span><span class="sxs-lookup"><span data-stu-id="9e833-104">Host Considerations</span></span>

### <a name="computer-type"></a><span data-ttu-id="9e833-105">Tipo computer</span><span class="sxs-lookup"><span data-stu-id="9e833-105">Computer Type</span></span>

<span data-ttu-id="9e833-106">Lo sviluppo incorporato viene in genere eseguito nei computer host Windows o UNIX.</span><span class="sxs-lookup"><span data-stu-id="9e833-106">Embedded development is usually performed on Windows PC or Unix host computers.</span></span> <span data-ttu-id="9e833-107">Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9e833-107">After the application is compiled, linked, and located on the host, it is downloaded to the target hardware for execution.</span></span>

### <a name="download-interfaces"></a><span data-ttu-id="9e833-108">Interfacce di download</span><span class="sxs-lookup"><span data-stu-id="9e833-108">Download Interfaces</span></span>

<span data-ttu-id="9e833-109">Il download di destinazione viene in genere eseguito tramite un'interfaccia seriale RS-232, sebbene le interfacce parallele, USB e Ethernet stiano diventando più diffuse.</span><span class="sxs-lookup"><span data-stu-id="9e833-109">Usually, the target download is done over an RS-232 serial interface, although parallel interfaces, USB, and Ethernet are becoming more popular.</span></span> <span data-ttu-id="9e833-110">Per le opzioni disponibili, vedere la documentazione dello strumento di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="9e833-110">See the development tool documentation for available options.</span></span>

### <a name="debugging-tools"></a><span data-ttu-id="9e833-111">Strumenti di debug</span><span class="sxs-lookup"><span data-stu-id="9e833-111">Debugging Tools</span></span>

<span data-ttu-id="9e833-112">Il debug viene eseguito in genere sullo stesso collegamento del download dell'immagine del programma.</span><span class="sxs-lookup"><span data-stu-id="9e833-112">Debugging is done typically over the same link as the program image download.</span></span> <span data-ttu-id="9e833-113">Sono disponibili diversi debugger, a partire da piccoli programmi di monitoraggio in esecuzione nella destinazione tramite il monitoraggio di debug in background (BDM) e gli strumenti di In-Circuit Emulator (ICE).</span><span class="sxs-lookup"><span data-stu-id="9e833-113">A variety of debuggers exist, ranging from small monitor programs running on the target through Background Debug Monitor (BDM) and In-Circuit Emulator (ICE) tools.</span></span> <span data-ttu-id="9e833-114">Lo strumento ICE fornisce il debug più affidabile dell'hardware di destinazione effettivo.</span><span class="sxs-lookup"><span data-stu-id="9e833-114">The ICE tool provides the most robust debugging of actual target hardware.</span></span>

### <a name="required-hard-disk-space"></a><span data-ttu-id="9e833-115">Spazio su disco rigido richiesto</span><span class="sxs-lookup"><span data-stu-id="9e833-115">Required Hard Disk Space</span></span>

<span data-ttu-id="9e833-116">Il codice sorgente per USBX viene fornito in formato ASCII e richiede circa 500 KB di spazio sul disco rigido del computer host.</span><span class="sxs-lookup"><span data-stu-id="9e833-116">The source code for USBX is delivered in ASCII format and requires approximately 500 KBytes of space on the host computer's hard disk.</span></span>

## <a name="target-considerations"></a><span data-ttu-id="9e833-117">Considerazioni sulla destinazione</span><span class="sxs-lookup"><span data-stu-id="9e833-117">Target Considerations</span></span>

<span data-ttu-id="9e833-118">USBX richiede tra 24 KByte e 64 Kbyte di memoria di sola lettura (ROM) nella destinazione in modalità host.</span><span class="sxs-lookup"><span data-stu-id="9e833-118">USBX requires between 24 KBytes and 64 KBytes of Read Only Memory (ROM) on the target in host mode.</span></span> <span data-ttu-id="9e833-119">La quantità di memoria richiesta dipende dal tipo di controller usato e dalle classi USB collegate a USBX.</span><span class="sxs-lookup"><span data-stu-id="9e833-119">The amount of memory required is dependent on the type of controller used and the USB classes linked to USBX.</span></span> <span data-ttu-id="9e833-120">Sono necessari altri 32 KByte della memoria ad accesso casuale (RAM) della destinazione per le strutture di dati globali USBX e il pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="9e833-120">Another 32 KBytes of the target's Random Access Memory (RAM) are required for USBX global data structures and memory pool.</span></span> <span data-ttu-id="9e833-121">È anche possibile modificare questo pool di memoria in base al numero previsto di dispositivi sul dispositivo USB e al tipo di controller USB.</span><span class="sxs-lookup"><span data-stu-id="9e833-121">This memory pool can also be adjusted depending on the expected number of devices on the USB and the type of USB controller.</span></span> <span data-ttu-id="9e833-122">Il lato dispositivo USBX richiede circa 10-12 K di ROM a seconda del tipo di controller del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e833-122">The USBX device side requires roughly 10-12 K of ROM depending on the type of device controller.</span></span> <span data-ttu-id="9e833-123">L'utilizzo della memoria RAM dipende dal tipo di classe emulata dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e833-123">The RAM memory usage depends on the type of class emulated by the device.</span></span>

<span data-ttu-id="9e833-124">USBX si basa anche su semafori, mutex e thread ThreadX per la protezione di più thread e la sospensione di I/O e l'elaborazione periodica per il monitoraggio della topologia del bus USB.</span><span class="sxs-lookup"><span data-stu-id="9e833-124">USBX also relies on ThreadX semaphores, mutexes, and threads for multiple thread protection, and I/O suspension and periodic processing for monitoring the USB bus topology.</span></span>

### <a name="product-distribution"></a><span data-ttu-id="9e833-125">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="9e833-125">Product Distribution</span></span>

<span data-ttu-id="9e833-126">Azure RTO USBX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/usbx/> .</span><span class="sxs-lookup"><span data-stu-id="9e833-126">Azure RTOS USBX can be obtained from our public source code repository at <https://github.com/azure-rtos/usbx/>.</span></span>

<span data-ttu-id="9e833-127">Di seguito è riportato un elenco di diversi file importanti nel repository:</span><span class="sxs-lookup"><span data-stu-id="9e833-127">The following is a list of several important files in the repository:</span></span>

- <span data-ttu-id="9e833-128">***ux_api. h***: questo file di intestazione C contiene tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.</span><span class="sxs-lookup"><span data-stu-id="9e833-128">***ux_api.h***: This C header file contains all system equates, data structures, and service prototypes.</span></span>
- <span data-ttu-id="9e833-129">***ux_port. h***: questo file di intestazione C contiene tutte le definizioni e le strutture dei dati specifici dello strumento di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="9e833-129">***ux_port.h***: This C header file contains all development-tool-specific data definitions and structures.</span></span>
- <span data-ttu-id="9e833-130">***UX. lib***: è la versione binaria della libreria C di USBX.</span><span class="sxs-lookup"><span data-stu-id="9e833-130">***ux.lib***: This is the binary version of the USBX C library.</span></span> <span data-ttu-id="9e833-131">Viene distribuito con il pacchetto standard.</span><span class="sxs-lookup"><span data-stu-id="9e833-131">It is distributed with the standard package.</span></span>
- <span data-ttu-id="9e833-132">***demo_usbx. c***: il file c contenente una demo USBX semplice</span><span class="sxs-lookup"><span data-stu-id="9e833-132">***demo_usbx.c***: The C file containing a simple USBX demo</span></span>

<span data-ttu-id="9e833-133">Tutti i nomi di file sono in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="9e833-133">All filenames are in lower-case.</span></span> <span data-ttu-id="9e833-134">Questa convenzione di denominazione rende più semplice convertire i comandi in piattaforme di sviluppo Unix.</span><span class="sxs-lookup"><span data-stu-id="9e833-134">This naming convention makes it easier to convert the commands to Unix development platforms.</span></span>

## <a name="usbx-installation"></a><span data-ttu-id="9e833-135">Installazione di USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-135">USBX Installation</span></span>

<span data-ttu-id="9e833-136">USBX viene installato clonando il repository GitHub nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="9e833-136">USBX is installed by cloning the GitHub repository to your local machine.</span></span> <span data-ttu-id="9e833-137">Di seguito è riportata la sintassi tipica per la creazione di un clone del repository USBX nel PC:</span><span class="sxs-lookup"><span data-stu-id="9e833-137">The following is typical syntax for creating a clone of the USBX repository on your PC:</span></span>

```powershell
    git clone https://github.com/azure-rtos/usbx
```

<span data-ttu-id="9e833-138">In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.</span><span class="sxs-lookup"><span data-stu-id="9e833-138">Alternatively you can download a copy of the repository using the download button on the GitHub main page.</span></span>

<span data-ttu-id="9e833-139">Sono inoltre disponibili istruzioni per la compilazione della libreria USBX nella pagina iniziale del repository online.</span><span class="sxs-lookup"><span data-stu-id="9e833-139">You will also find instructions for building the USBX library on the front page of the online repository.</span></span>

<span data-ttu-id="9e833-140">Le istruzioni generali riportate di seguito si applicano praticamente a qualsiasi installazione:</span><span class="sxs-lookup"><span data-stu-id="9e833-140">The following general instructions apply to virtually any installation:</span></span>

1. <span data-ttu-id="9e833-141">Usare la stessa directory in cui è stato precedentemente installato ThreadX nel disco rigido host.</span><span class="sxs-lookup"><span data-stu-id="9e833-141">Use the same directory in which you previously installed ThreadX on the host hard drive.</span></span> <span data-ttu-id="9e833-142">Tutti i nomi di USBX sono univoci e non interferiscono con l'installazione precedente di USBX.</span><span class="sxs-lookup"><span data-stu-id="9e833-142">All USBX names are unique and will not interfere with the previous USBX installation.</span></span>
2. <span data-ttu-id="9e833-143">Aggiungere una chiamata a \***ux_system_initialize** _ a o quasi all'inizio di _ *_tx_application_define_.* \* Qui vengono inizializzate le risorse USBX.</span><span class="sxs-lookup"><span data-stu-id="9e833-143">Add a call to ***ux_system_initialize** _ at or near the beginning of _ *_tx_application_define_.** This is where the USBX resources are initialized.</span></span>
3. <span data-ttu-id="9e833-144">Aggiungere una chiamata a \*\**ux_host_stack_initialize *.**</span><span class="sxs-lookup"><span data-stu-id="9e833-144">Add a call to \***ux_host_stack_initialize\*.**</span></span>
4. <span data-ttu-id="9e833-145">Aggiungere una o più chiamate per inizializzare il USBX richiesto.</span><span class="sxs-lookup"><span data-stu-id="9e833-145">Add one or more calls to initialize the required USBX.</span></span>
5. <span data-ttu-id="9e833-146">Aggiungere una o più chiamate per inizializzare i controller host disponibili nel sistema.</span><span class="sxs-lookup"><span data-stu-id="9e833-146">Add one or more calls to initialize the host controllers available in the system.</span></span>
6. <span data-ttu-id="9e833-147">Potrebbe essere necessario modificare il file tx_low_level_initialize. c per aggiungere l'inizializzazione hardware di basso livello e il routing vettoriale di interrupt.</span><span class="sxs-lookup"><span data-stu-id="9e833-147">It may be required to modify the tx_low_level_initialize.c file to add low-level hardware initialization and interrupt vector routing.</span></span> <span data-ttu-id="9e833-148">Questa operazione è specifica della piattaforma hardware e non verrà discussa qui.</span><span class="sxs-lookup"><span data-stu-id="9e833-148">This is specific to the hardware platform and will not be discussed here.</span></span>
7. <span data-ttu-id="9e833-149">Compilare il codice sorgente dell'applicazione e il collegamento con le librerie di runtime USBX e ThreadX (FileX e/o NETX potrebbero essere necessari anche se la classe di archiviazione USB e/o le classi di rete USB devono essere compilate in), UX. a (o UX. lib) e TX. a (o TX. lib).</span><span class="sxs-lookup"><span data-stu-id="9e833-149">Compile application source code and link with the USBX and ThreadX run time libraries (FileX and/or Netx may also be required if the USB storage class and/or USB network classes are to be compiled in), ux.a (or ux.lib) and tx.a (or tx.lib).</span></span> <span data-ttu-id="9e833-150">Il risultante può essere scaricato nella destinazione ed eseguito.</span><span class="sxs-lookup"><span data-stu-id="9e833-150">The resulting can be downloaded to the target and executed.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="9e833-151">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="9e833-151">Configuration Options</span></span>

<span data-ttu-id="9e833-152">Sono disponibili diverse opzioni di configurazione per la compilazione della libreria USBX.</span><span class="sxs-lookup"><span data-stu-id="9e833-152">There are several configuration options for building the USBX library.</span></span> <span data-ttu-id="9e833-153">Tutte le opzioni si trovano in ***ux_user. h***.</span><span class="sxs-lookup"><span data-stu-id="9e833-153">All options are located in the ***ux_user.h***.</span></span>

<span data-ttu-id="9e833-154">Nell'elenco seguente vengono illustrate tutte le opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9e833-154">The list below details each configuration option.</span></span>


- <span data-ttu-id="9e833-155">**UX_PERIODIC_RATE**: questo valore rappresenta il numero di cicli al secondo per una piattaforma hardware specifica.</span><span class="sxs-lookup"><span data-stu-id="9e833-155">**UX_PERIODIC_RATE**: This value represents how many ticks per seconds for a specific hardware platform.</span></span> <span data-ttu-id="9e833-156">Il valore predefinito è 1000, che indica un segno di cicli per millisecondo.</span><span class="sxs-lookup"><span data-stu-id="9e833-156">The default is 1000 indicating one tick per millisecond.</span></span>
- <span data-ttu-id="9e833-157">**UX_MAX_CLASS_DRIVER**: questo valore è il numero massimo di classi che possono essere caricate da USBX.</span><span class="sxs-lookup"><span data-stu-id="9e833-157">**UX_MAX_CLASS_DRIVER**: This value is the maximum number of classes that can be loaded by USBX.</span></span> <span data-ttu-id="9e833-158">Questo valore rappresenta il contenitore della classe e non il numero di istanze di una classe.</span><span class="sxs-lookup"><span data-stu-id="9e833-158">This value represents the class container and not the number of instances of a class.</span></span> <span data-ttu-id="9e833-159">Ad esempio, se una particolare implementazione di USBX necessita della classe Hub, della classe Printer e della classe di archiviazione, il valore di UX_MAX_CLASS_DRIVER può essere impostato su 3 indipendentemente dal numero di dispositivi che appartengono a tali classi.</span><span class="sxs-lookup"><span data-stu-id="9e833-159">For instance, if a particular implementation of USBX needs the hub class, the printer class, and the storage class, then the UX_MAX_CLASS_DRIVER value can be set to 3 regardless of the number of devices that belong to these classes.</span></span>
- <span data-ttu-id="9e833-160">**UX_MAX_HCD**: questo valore rappresenta il numero di controller host diversi disponibili nel sistema.</span><span class="sxs-lookup"><span data-stu-id="9e833-160">**UX_MAX_HCD**: This value represents the number of different host controllers that are available in the system.</span></span> <span data-ttu-id="9e833-161">Per il supporto USB 1,1, questo valore sarà per lo più 1.</span><span class="sxs-lookup"><span data-stu-id="9e833-161">For USB 1.1 support, this value will mostly be 1.</span></span> <span data-ttu-id="9e833-162">Per il supporto USB 2,0, questo valore può essere maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="9e833-162">For USB 2.0 support this value can be more than 1.</span></span> <span data-ttu-id="9e833-163">Questo valore rappresenta il numero di controller host simultanei in esecuzione nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="9e833-163">This value represents the number of concurrent host controllers running at the same time.</span></span> <span data-ttu-id="9e833-164">Se ad esempio sono presenti due istanze di OHCI in esecuzione o un EHCI e un controller OHCI in esecuzione, il UX_MAX_HCD deve essere impostato su 2.</span><span class="sxs-lookup"><span data-stu-id="9e833-164">If for instance, there are two instances of OHCI running or one EHCI and one OHCI controllers running, the UX_MAX_HCD should be set to 2.</span></span> 
- <span data-ttu-id="9e833-165">**UX_MAX_DEVICES**: questo valore rappresenta il numero massimo di dispositivi che possono essere collegati al dispositivo USB.</span><span class="sxs-lookup"><span data-stu-id="9e833-165">**UX_MAX_DEVICES**: This value represents the maximum number of devices that can be attached to the USB.</span></span> <span data-ttu-id="9e833-166">Normalmente, il numero massimo teorico su un singolo USB è 127 dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9e833-166">Normally, the theoretical maximum number on a single USB is 127 devices.</span></span> <span data-ttu-id="9e833-167">Per ridurre la memoria, questo valore può essere ridotto.</span><span class="sxs-lookup"><span data-stu-id="9e833-167">This value can be scaled down to conserve memory.</span></span> <span data-ttu-id="9e833-168">Si noti che questo valore rappresenta il numero totale di dispositivi indipendentemente dal numero di bus USB nel sistema.</span><span class="sxs-lookup"><span data-stu-id="9e833-168">It should be noted that this value represents the total number of devices regardless of the number of USB buses in the system.</span></span>
- <span data-ttu-id="9e833-169">**UX_MAX_ED**: questo valore rappresenta il numero massimo di EDS nel pool di controller.</span><span class="sxs-lookup"><span data-stu-id="9e833-169">**UX_MAX_ED**: This value represents the maximum number of EDs in the controller pool.</span></span> <span data-ttu-id="9e833-170">Questo numero viene assegnato solo a un controller.</span><span class="sxs-lookup"><span data-stu-id="9e833-170">This number is assigned to one controller only.</span></span> <span data-ttu-id="9e833-171">Se sono presenti più istanze di controller, questo valore viene usato da ogni singolo controller.</span><span class="sxs-lookup"><span data-stu-id="9e833-171">If multiple instances of controllers are present, this value is used by each individual controller.</span></span>
- <span data-ttu-id="9e833-172">**UX_MAX_TD e UX_MAX_ISO_TD**: questo valore rappresenta il numero massimo di TDS regolari e isocroni nel pool di controller.</span><span class="sxs-lookup"><span data-stu-id="9e833-172">**UX_MAX_TD and UX_MAX_ISO_TD**: This value represents the maximum number of regular and isochronous TDs in the controller pool.</span></span> <span data-ttu-id="9e833-173">Questo numero viene assegnato solo a un controller.</span><span class="sxs-lookup"><span data-stu-id="9e833-173">This number is assigned to one controller only.</span></span> <span data-ttu-id="9e833-174">Se sono presenti più istanze di controller, questo valore viene usato da ogni singolo controller.</span><span class="sxs-lookup"><span data-stu-id="9e833-174">If multiple instances of controllers are present, this value is used by each individual controller.</span></span>
- <span data-ttu-id="9e833-175">**UX_THREAD_STACK_SIZE**: questo valore corrisponde alla dimensione dello stack in byte per i thread USBX.</span><span class="sxs-lookup"><span data-stu-id="9e833-175">**UX_THREAD_STACK_SIZE**: This value is the size of the stack in bytes for the USBX threads.</span></span> <span data-ttu-id="9e833-176">Può essere in genere 1024 byte o 2048 byte a seconda del processore usato e del controller host.</span><span class="sxs-lookup"><span data-stu-id="9e833-176">It can be typically 1024 bytes or 2048 bytes depending on the processor used and the host controller.</span></span>
- <span data-ttu-id="9e833-177">**UX_HOST_ENUM_THREAD_STACK_SIZE**: questo valore corrisponde alla dimensione dello stack del thread di enumerazione host USB.</span><span class="sxs-lookup"><span data-stu-id="9e833-177">**UX_HOST_ENUM_THREAD_STACK_SIZE**: This value is the stack size of the USB host enumeration thread.</span></span> <span data-ttu-id="9e833-178">Se il simbolo non è impostato, le dimensioni dello stack del thread di enumerazione dell'host USBX vengono impostate su **UX_THREAD_STACK_SIZE**.</span><span class="sxs-lookup"><span data-stu-id="9e833-178">If this symbol I not set, the USBX host enumeration thread stack size is set to **UX_THREAD_STACK_SIZE**.</span></span> 
- <span data-ttu-id="9e833-179">**UX_HOST_HCD_THREAD_STACK_SIZE**: questo valore corrisponde alla dimensione dello stack del thread HCD dell'host USB.</span><span class="sxs-lookup"><span data-stu-id="9e833-179">**UX_HOST_HCD_THREAD_STACK_SIZE**: This value is the stack size of the USB host HCD thread.</span></span> <span data-ttu-id="9e833-180">Se il simbolo non è impostato, le dimensioni dello stack dei thread HCD dell'host USBX sono impostate su **UX_THREAD_STACK_SIZE**.</span><span class="sxs-lookup"><span data-stu-id="9e833-180">If this symbol I not set, the USBX host HCD thread stack size is set to **UX_THREAD_STACK_SIZE**.</span></span>
- <span data-ttu-id="9e833-181">**UX_THREAD_PRIORITY_ENUM**: valore di priorità threadX per i thread di enumerazione USBX che monitora la topologia del bus.</span><span class="sxs-lookup"><span data-stu-id="9e833-181">**UX_THREAD_PRIORITY_ENUM**: This is the ThreadX priority value for the USBX enumeration threads that monitors the bus topology.</span></span>
- <span data-ttu-id="9e833-182">**UX_THREAD_PRIORITY_CLASS**: valore di priorità threadX per i thread USBX standard.</span><span class="sxs-lookup"><span data-stu-id="9e833-182">**UX_THREAD_PRIORITY_CLASS**: This is the ThreadX priority value for the standard USBX threads.</span></span>
- <span data-ttu-id="9e833-183">**UX_THREAD_PRIORITY_KEYBOARD**: valore di priorità threadX per la classe della tastiera USBX HID.</span><span class="sxs-lookup"><span data-stu-id="9e833-183">**UX_THREAD_PRIORITY_KEYBOARD**: This is the ThreadX priority value for the USBX HID keyboard class.</span></span>
- <span data-ttu-id="9e833-184">**UX_THREAD_PRIORITY_HCD**: valore di priorità threadX per il thread del controller host.</span><span class="sxs-lookup"><span data-stu-id="9e833-184">**UX_THREAD_PRIORITY_HCD**: This is the ThreadX priority value for the host controller thread.</span></span>
- <span data-ttu-id="9e833-185">**UX_NO_TIME_SLICE**: questo valore definisce effettivamente l'intervallo di tempo che verrà usato per i thread.</span><span class="sxs-lookup"><span data-stu-id="9e833-185">**UX_NO_TIME_SLICE**: This value actually defines the time slice that will be used for threads.</span></span> <span data-ttu-id="9e833-186">Se, ad esempio, viene definito su 0, la porta di destinazione ThreadX non utilizza intervalli di tempo.</span><span class="sxs-lookup"><span data-stu-id="9e833-186">For example, if defined to 0, the ThreadX target port does not use time slices.</span></span>
- <span data-ttu-id="9e833-187">**UX_MAX_HOST_LUN**: questo valore rappresenta il numero massimo di unità logiche SCSI rappresentate nel driver della classe di archiviazione host.</span><span class="sxs-lookup"><span data-stu-id="9e833-187">**UX_MAX_HOST_LUN**: This value represents the maximum number of SCSI logical units represented in the host storage class driver.</span></span>
- <span data-ttu-id="9e833-188">**UX_HOST_CLASS_STORAGE_INCLUDE_LEGACY_PROTOCOL_SUPPORT**: se definito, questo valore include il codice per gestire i dispositivi di archiviazione che usano il protocollo CB o CBI, ad esempio i dischi floppy.</span><span class="sxs-lookup"><span data-stu-id="9e833-188">**UX_HOST_CLASS_STORAGE_INCLUDE_LEGACY_PROTOCOL_SUPPORT**: If defined, this value includes code to handle storage devices that use the CB or CBI protocol (such as floppy disks).</span></span> <span data-ttu-id="9e833-189">È disattivata per impostazione predefinita perché questi protocolli sono obsoleti, sostituiti dal trasporto Bulk Only (il protocollo BOT, che praticamente tutti i dispositivi di archiviazione moderni usano).</span><span class="sxs-lookup"><span data-stu-id="9e833-189">It is off by default because these protocols are obsolete, being superseded by the Bulk Only Transport (BOT protocol, which virtually all modern storage devices use.</span></span>
- <span data-ttu-id="9e833-190">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE**: se definito, questo valore causa ux_host_class_hid_keyboard_key_get solo le modifiche apportate alle chiavi, le pressioni di tasto e le versioni di chiave.</span><span class="sxs-lookup"><span data-stu-id="9e833-190">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE**: If defined, this value causes ux_host_class_hid_keyboard_key_get to only report key changes that is, key presses and key releases.</span></span> <span data-ttu-id="9e833-191">Per impostazione predefinita, viene segnalato solo quando un tasto è inattivo.</span><span class="sxs-lookup"><span data-stu-id="9e833-191">By default, it only reports when a key is down.</span></span>
- <span data-ttu-id="9e833-192">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_KEY_DOWN_ONLY**: utilizzato solo se viene definito **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** .</span><span class="sxs-lookup"><span data-stu-id="9e833-192">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_KEY_DOWN_ONLY**: Only used if **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** is defined.</span></span> <span data-ttu-id="9e833-193">Se definito, fa in modo che ux_host_class_hid_keyboard_key_get solo le modifiche alla pressione del tasto. le modifiche apportate/rilasciate della chiave non vengono segnalate.</span><span class="sxs-lookup"><span data-stu-id="9e833-193">If defined, causes ux_host_class_hid_keyboard_key_get to only report key pressed/down changes; key released/up changes are not reported.</span></span>
- <span data-ttu-id="9e833-194">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_LOCK_KEYS**: utilizzato solo se viene definito **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** .</span><span class="sxs-lookup"><span data-stu-id="9e833-194">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_LOCK_KEYS**: Only used if **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** is defined.</span></span> <span data-ttu-id="9e833-195">Se definito, causa ux_host_class_hid_keyboard_key_get le modifiche alla chiave di blocco (CapsLock/NumLock/ScrollLock).</span><span class="sxs-lookup"><span data-stu-id="9e833-195">If defined, causes ux_host_class_hid_keyboard_key_get to report lock key (CapsLock/NumLock/ScrollLock) changes.</span></span>
- <span data-ttu-id="9e833-196">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_MODIFIER_KEYS**: utilizzato solo se viene definito **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** .</span><span class="sxs-lookup"><span data-stu-id="9e833-196">**UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_MODIFIER_KEYS**: Only used if **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** is defined.</span></span> <span data-ttu-id="9e833-197">Se definito, fa sì che ux_host_class_hid_keyboard_key_get le modifiche del tasto di modifica (Ctrl/Alt/Shift/GUI).</span><span class="sxs-lookup"><span data-stu-id="9e833-197">If defined, causes ux_host_class_hid_keyboard_key_get to report modifier key (Ctrl/Alt/Shift/GUI) changes.</span></span>
- <span data-ttu-id="9e833-198">**UX_HOST_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**: se definito, questo valore rappresenta il numero di pacchetti nella classe host CDC-ECM.</span><span class="sxs-lookup"><span data-stu-id="9e833-198">**UX_HOST_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**: If defined, this value represents the number of packets in the CDC-ECM host class.</span></span> <span data-ttu-id="9e833-199">Il valore predefinito è 16.</span><span class="sxs-lookup"><span data-stu-id="9e833-199">The default is 16.</span></span>

## <a name="source-code-tree"></a><span data-ttu-id="9e833-200">Albero del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="9e833-200">Source Code Tree</span></span>

<span data-ttu-id="9e833-201">I file USBX sono disponibili in più directory.</span><span class="sxs-lookup"><span data-stu-id="9e833-201">The USBX files are provided in several directories.</span></span>

![Albero del codice sorgente](media/usbx-host-stack/source-code-tree.png)

<span data-ttu-id="9e833-203">Per rendere i file riconoscibili con i rispettivi nomi, è stata adottata la convenzione seguente:</span><span class="sxs-lookup"><span data-stu-id="9e833-203">In order to make the files recognizable by their names, the following convention has been adopted:</span></span>

| <span data-ttu-id="9e833-204">Nome suffisso file</span><span class="sxs-lookup"><span data-stu-id="9e833-204">File Suffix Name</span></span> | <span data-ttu-id="9e833-205">Descrizione file</span><span class="sxs-lookup"><span data-stu-id="9e833-205">File description</span></span>                          |
| ---------------- | ----------------------------------------- |
| <span data-ttu-id="9e833-206">ux_host_stack</span><span class="sxs-lookup"><span data-stu-id="9e833-206">ux_host_stack</span></span>    | <span data-ttu-id="9e833-207">USBX file core dello stack host</span><span class="sxs-lookup"><span data-stu-id="9e833-207">usbx host stack core files</span></span>                |
| <span data-ttu-id="9e833-208">ux_host_class</span><span class="sxs-lookup"><span data-stu-id="9e833-208">ux_host_class</span></span>    | <span data-ttu-id="9e833-209">file delle classi dello stack host USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-209">usbx host stack classes files</span></span>             |
| <span data-ttu-id="9e833-210">ux_hcd</span><span class="sxs-lookup"><span data-stu-id="9e833-210">ux_hcd</span></span>           | <span data-ttu-id="9e833-211">file driver del controller dello stack host USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-211">usbx host stack controller driver files</span></span>   |
| <span data-ttu-id="9e833-212">ux_device_stack</span><span class="sxs-lookup"><span data-stu-id="9e833-212">ux_device_stack</span></span>  | <span data-ttu-id="9e833-213">file principali dello stack di dispositivi USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-213">usbx device stack core files</span></span>              |
| <span data-ttu-id="9e833-214">ux_device_class</span><span class="sxs-lookup"><span data-stu-id="9e833-214">ux_device_class</span></span>  | <span data-ttu-id="9e833-215">file delle classi dello stack del dispositivo USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-215">usbx device stack classes files</span></span>           |
| <span data-ttu-id="9e833-216">ux_dcd</span><span class="sxs-lookup"><span data-stu-id="9e833-216">ux_dcd</span></span>           | <span data-ttu-id="9e833-217">file driver del controller dello stack del dispositivo USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-217">usbx device stack controller driver files</span></span> |
| <span data-ttu-id="9e833-218">ux_otg</span><span class="sxs-lookup"><span data-stu-id="9e833-218">ux_otg</span></span>           | <span data-ttu-id="9e833-219">file correlati driver del controller USBX OTG</span><span class="sxs-lookup"><span data-stu-id="9e833-219">usbx otg controller driver related files</span></span>  |
| <span data-ttu-id="9e833-220">ux_pictbridge</span><span class="sxs-lookup"><span data-stu-id="9e833-220">ux_pictbridge</span></span>    | <span data-ttu-id="9e833-221">file PictBridge USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-221">usbx pictbridge files</span></span>                     |
| <span data-ttu-id="9e833-222">ux_utility</span><span class="sxs-lookup"><span data-stu-id="9e833-222">ux_utility</span></span>       | <span data-ttu-id="9e833-223">funzioni di utilità USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-223">usbx utility functions</span></span>                    |
| <span data-ttu-id="9e833-224">demo_usbx</span><span class="sxs-lookup"><span data-stu-id="9e833-224">demo_usbx</span></span>        | <span data-ttu-id="9e833-225">file dimostrativi per USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-225">demonstration files for USBX</span></span>              |

## <a name="initialization-of-usbx-resources"></a><span data-ttu-id="9e833-226">Inizializzazione delle risorse di USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-226">Initialization of USBX resources</span></span>

<span data-ttu-id="9e833-227">USBX dispone di un proprio gestore della memoria.</span><span class="sxs-lookup"><span data-stu-id="9e833-227">USBX has its own memory manager.</span></span> <span data-ttu-id="9e833-228">La memoria deve essere allocata a USBX prima che il lato host o dispositivo di USBX venga inizializzato.</span><span class="sxs-lookup"><span data-stu-id="9e833-228">The memory needs to be allocated to USBX before the host or device side of USBX is initialized.</span></span> <span data-ttu-id="9e833-229">Il gestore della memoria USBX può supportare i sistemi in cui è possibile memorizzare nella cache la memoria.</span><span class="sxs-lookup"><span data-stu-id="9e833-229">USBX memory manager can accommodate systems where memory can be cached.</span></span>

<span data-ttu-id="9e833-230">La funzione seguente inizializza le risorse di memoria USBX con 128 KB di memoria normale e nessun pool separato per la memoria sicura della cache:</span><span class="sxs-lookup"><span data-stu-id="9e833-230">The following function initializes USBX memory resources with 128K of regular memory and no separate pool for cache safe memory:</span></span>

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

<span data-ttu-id="9e833-231">Il prototipo per la ux_system_initialize è il seguente.</span><span class="sxs-lookup"><span data-stu-id="9e833-231">The prototype for the ux_system_initialize is as follows.</span></span>

```c
UINT ux_system_initialize( 
    VOID *regular_memory_pool_start,
    ULONG regular_memory_size,
    VOID *cache_safe_memory_pool_start,
    ULONG cache_safe_memory_size);
```

### <a name="input-parameters"></a><span data-ttu-id="9e833-232">Parametri di input:</span><span class="sxs-lookup"><span data-stu-id="9e833-232">Input parameters:</span></span>

- <span data-ttu-id="9e833-233">**regular_memory_pool_start** Inizio del pool di memoria normale.</span><span class="sxs-lookup"><span data-stu-id="9e833-233">**regular_memory_pool_start** Beginning of the regular memory pool.</span></span>
- <span data-ttu-id="9e833-234">**regular_memory_size** Dimensioni del pool di memoria normale.</span><span class="sxs-lookup"><span data-stu-id="9e833-234">**regular_memory_size** Size of the regular memory pool.</span></span>
- <span data-ttu-id="9e833-235">**cache_safe_memory_pool_start** Inizio del pool di memoria sicuro della cache.</span><span class="sxs-lookup"><span data-stu-id="9e833-235">**cache_safe_memory_pool_start** Beginning of the cache safe memory pool.</span></span>
- <span data-ttu-id="9e833-236">**cache_safe_memory_size** Dimensioni del pool di memoria sicuro della cache.</span><span class="sxs-lookup"><span data-stu-id="9e833-236">**cache_safe_memory_size** Size of the cache safe memory pool.</span></span>    |

<span data-ttu-id="9e833-237">Non tutti i sistemi richiedono la definizione di memoria protetta dalla cache.</span><span class="sxs-lookup"><span data-stu-id="9e833-237">Not all systems require the definition of cache safe memory.</span></span> <span data-ttu-id="9e833-238">In tale sistema, i valori passati durante l'inizializzazione per il puntatore di memoria verranno impostati su UX_NULL e le dimensioni del pool su 0.</span><span class="sxs-lookup"><span data-stu-id="9e833-238">In such a system, the values passed during the initialization for the memory pointer will be set to UX_NULL and the size of the pool to 0.</span></span> <span data-ttu-id="9e833-239">USBX utilizzerà quindi il normale pool di memoria anziché il pool di sicurezza della cache.</span><span class="sxs-lookup"><span data-stu-id="9e833-239">USBX will then use the regular memory pool in lieu of the cache safe pool.</span></span>

<span data-ttu-id="9e833-240">In un sistema in cui la memoria normale non è protetta dalla cache e un controller richiede l'esecuzione di memoria DMA (come OHCI, controller EHCI tra gli altri) è necessario definire un pool di memoria in un'area di sicurezza della cache.</span><span class="sxs-lookup"><span data-stu-id="9e833-240">In a system where the regular memory is not cache safe and a controller requires to perform DMA memory (like OHCI, EHCI controllers amongst others) it is necessary to define a memory pool in a cache safe zone.</span></span>

## <a name="uninitialization-of-usbx-resources"></a><span data-ttu-id="9e833-241">Inizializzazione delle risorse di USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-241">Uninitialization of USBX resources</span></span>

<span data-ttu-id="9e833-242">USBX può essere terminato rilasciando le risorse.</span><span class="sxs-lookup"><span data-stu-id="9e833-242">USBX can be terminated by releasing its resources.</span></span> <span data-ttu-id="9e833-243">Prima di terminare il USBX, tutte le classi e le risorse del controller devono essere terminate correttamente.</span><span class="sxs-lookup"><span data-stu-id="9e833-243">Prior to terminating usbx, all classes and controller resources need to be terminated properly.</span></span> <span data-ttu-id="9e833-244">La funzione seguente consente di uninizializzare le risorse di memoria USBX:</span><span class="sxs-lookup"><span data-stu-id="9e833-244">The following function uninitializes USBX memory resources :</span></span>

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

<span data-ttu-id="9e833-245">Il prototipo per la ux_system_initialize è il seguente.</span><span class="sxs-lookup"><span data-stu-id="9e833-245">The prototype for the ux_system_initialize is as follows.</span></span>

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-host-controllers"></a><span data-ttu-id="9e833-246">Definizione dei controller host USB</span><span class="sxs-lookup"><span data-stu-id="9e833-246">Definition of USB Host Controllers</span></span>

<span data-ttu-id="9e833-247">È necessario definire almeno un controller host USB per il funzionamento di USBX in modalità host.</span><span class="sxs-lookup"><span data-stu-id="9e833-247">It is required to define at least one USB host controller for USBX to operate in host mode.</span></span> <span data-ttu-id="9e833-248">Il file di inizializzazione dell'applicazione deve contenere questa definizione.</span><span class="sxs-lookup"><span data-stu-id="9e833-248">The application initialization file should contain this definition.</span></span> <span data-ttu-id="9e833-249">La riga seguente esegue la definizione di un controller host generico.</span><span class="sxs-lookup"><span data-stu-id="9e833-249">The following line performs the definition of a generic host controller.</span></span>

```c
ux_host_stack_hcd_register("ux_hcd_controller",
        ux_hcd_controller_initialize, 0xd0000, 0x0a);
```

<span data-ttu-id="9e833-250">Il ux_host_stack_hcd_register presenta il seguente prototipo.</span><span class="sxs-lookup"><span data-stu-id="9e833-250">The ux_host_stack_hcd_register has the following prototype.</span></span>

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_initialize_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

<span data-ttu-id="9e833-251">La funzione ux_host_stack_hcd_register presenta i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e833-251">The ux_host_stack_hcd_register function has the following parameters.</span></span>

- <span data-ttu-id="9e833-252">**hcd_name**: stringa del nome del controller</span><span class="sxs-lookup"><span data-stu-id="9e833-252">**hcd_name**: string of the controller name</span></span>
- <span data-ttu-id="9e833-253">**hcd_initialize_function**: funzione di inizializzazione del controller</span><span class="sxs-lookup"><span data-stu-id="9e833-253">**hcd_initialize_function**: initialization function of the controller</span></span>
- <span data-ttu-id="9e833-254">**hcd_param1**: in genere il valore io o la memoria usata dal controller</span><span class="sxs-lookup"><span data-stu-id="9e833-254">**hcd_param1**: usually the IO value or Memory used by the controller</span></span>
- <span data-ttu-id="9e833-255">**hcd_param2**: in genere l'IRQ usato dal controller</span><span class="sxs-lookup"><span data-stu-id="9e833-255">**hcd_param2**: usually the IRQ used by the controller</span></span>

<span data-ttu-id="9e833-256">Nell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="9e833-256">In our previous example:</span></span>

- <span data-ttu-id="9e833-257">"ux_hcd_controller" è il nome del controller</span><span class="sxs-lookup"><span data-stu-id="9e833-257">"ux_hcd_controller" is the name of the controller</span></span>
- <span data-ttu-id="9e833-258">"ux_hcd_controller_initialize" è la routine di inizializzazione per il controller host</span><span class="sxs-lookup"><span data-stu-id="9e833-258">"ux_hcd_controller_initialize" is the initialization routine for the host controller</span></span>
- <span data-ttu-id="9e833-259">0xD0000 è l'indirizzo in cui i registri del controller host sono visibili in memoria</span><span class="sxs-lookup"><span data-stu-id="9e833-259">0xd0000 is the address at which the host controller registers are visible in memory</span></span>
- <span data-ttu-id="9e833-260">e 0x0A è l'IRQ usato dal controller host.</span><span class="sxs-lookup"><span data-stu-id="9e833-260">and 0x0a is the IRQ used by the host controller.</span></span>

<span data-ttu-id="9e833-261">Di seguito è riportato un esempio di inizializzazione di USBX in modalità host con un controller host e diverse classi.</span><span class="sxs-lookup"><span data-stu-id="9e833-261">Following is an example of the initialization of USBX in host mode with one host controller and several classes.</span></span>

```c
UINT status;

/* Initialize USBX. */
ux_system_initialize(memory_ptr, (128*1024),0,0);

/* The code below is required for installing the USBX host stack. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, host stack has been initialized. */

/* Register all the host classes for this USBX implementation. */
status = ux_host_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_storage", ux_host_class_storage_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_printer", ux_host_class_printer_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_audio", ux_host_class_audio_entry);

/* If status equals UX_SUCCESS, host class has been registered. */

/* Register all the USB host controllers available in this system. */ 
status = ux_host_stack_hcd_register("ux_hcd_controller", ux_hcd_controller_initialize, 0x300000, 0x0a);

/* If status equals UX_SUCCESS, USB host controllers have been registered. */
```

## <a name="definition-of-host-classes"></a><span data-ttu-id="9e833-262">Definizione delle classi host</span><span class="sxs-lookup"><span data-stu-id="9e833-262">Definition of Host Classes</span></span>

<span data-ttu-id="9e833-263">È necessario definire una o più classi host con USBX.</span><span class="sxs-lookup"><span data-stu-id="9e833-263">It is required to define one or more host classes with USBX.</span></span> <span data-ttu-id="9e833-264">Una classe USB è necessaria per guidare un dispositivo USB dopo che lo stack USB ha configurato il dispositivo USB.</span><span class="sxs-lookup"><span data-stu-id="9e833-264">A USB class is required to drive a USB device after the USB stack has configured the USB device.</span></span> <span data-ttu-id="9e833-265">Una classe USB è specifica del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e833-265">A USB class is specific to the device.</span></span> <span data-ttu-id="9e833-266">Una o più classi potrebbero essere necessarie per guidare un dispositivo USB a seconda del numero di interfacce contenute nei descrittori di dispositivo USB.</span><span class="sxs-lookup"><span data-stu-id="9e833-266">One or more classes may be required to drive a USB device depending on the number of interfaces contained in the USB device descriptors.</span></span>

<span data-ttu-id="9e833-267">Questo è un esempio di registrazione della classe HUB.</span><span class="sxs-lookup"><span data-stu-id="9e833-267">This is an example of the registration of the HUB class.</span></span>

```c
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);
```

<span data-ttu-id="9e833-268">Il prototipo della funzione ux_host_class_register è il seguente.</span><span class="sxs-lookup"><span data-stu-id="9e833-268">The function ux_host_class_register has the following prototype.</span></span>

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name, 
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

- <span data-ttu-id="9e833-269">**class_name** è il nome della classe</span><span class="sxs-lookup"><span data-stu-id="9e833-269">**class_name** is the name of the class</span></span>
- <span data-ttu-id="9e833-270">**class_entry_address** è il punto di ingresso della classe</span><span class="sxs-lookup"><span data-stu-id="9e833-270">**class_entry_address** is the entry point of the class</span></span>

<span data-ttu-id="9e833-271">Nell'esempio di inizializzazione della classe HUB:</span><span class="sxs-lookup"><span data-stu-id="9e833-271">In the example of the HUB class initialization:</span></span>

- <span data-ttu-id="9e833-272">"ux_host_class_hub" è il nome della classe Hub</span><span class="sxs-lookup"><span data-stu-id="9e833-272">"ux_host_class_hub" is the name of the hub class</span></span>
- <span data-ttu-id="9e833-273">ux_host_class_hub_entry è il punto di ingresso della classe HUB.</span><span class="sxs-lookup"><span data-stu-id="9e833-273">ux_host_class_hub_entry is the entry point of the HUB class.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9e833-274">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9e833-274">Troubleshooting</span></span>

<span data-ttu-id="9e833-275">USBX viene fornito con un file dimostrativo e un ambiente di simulazione.</span><span class="sxs-lookup"><span data-stu-id="9e833-275">USBX is delivered with a demonstration file and a simulation environment.</span></span> <span data-ttu-id="9e833-276">È sempre consigliabile ottenere prima di tutto la piattaforma dimostrativa, sia nell'hardware di destinazione che in una piattaforma dimostrativa specifica.</span><span class="sxs-lookup"><span data-stu-id="9e833-276">It is always a good idea to get the demonstration platform running first—either on the target hardware or a specific demonstration platform.</span></span>

<span data-ttu-id="9e833-277">Se il sistema dimostrativo non funziona, provare a eseguire le operazioni seguenti per restringere il problema.</span><span class="sxs-lookup"><span data-stu-id="9e833-277">If the demonstration system does not work, try the following things to narrow the problem.</span></span>

## <a name="usbx-version-id"></a><span data-ttu-id="9e833-278">ID versione USBX</span><span class="sxs-lookup"><span data-stu-id="9e833-278">USBX Version ID</span></span>

<span data-ttu-id="9e833-279">La versione corrente di USBX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9e833-279">The current version of USBX is available both to the user and the application software during run-time.</span></span> <span data-ttu-id="9e833-280">Il programmatore può ottenere la versione di USBX dall'esame del file \***ux_port. h** _.</span><span class="sxs-lookup"><span data-stu-id="9e833-280">The programmer can obtain the USBX version from examination of the \***ux_port.h** _ file.</span></span> <span data-ttu-id="9e833-281">Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente.</span><span class="sxs-lookup"><span data-stu-id="9e833-281">In addition, this file also contains a version history of the corresponding port.</span></span> <span data-ttu-id="9e833-282">Il software applicativo può ottenere la versione di USBX esaminando la stringa globale _ *_ _ux_version_id_* _, definita in _ *_ux_port. h_* \*.</span><span class="sxs-lookup"><span data-stu-id="9e833-282">Application software can obtain the USBX version by examining the global string _ *_ _ux_version_id_* _, which is defined in _\*_ux_port.h_\*\*.</span></span>
