---
title: Capitolo 2-installazione e uso di Azure RTO ThreadX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del kernel ThreadX di Azure RTO ad alte prestazioni.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e1bf85d363b07c81f226d494107eae9ba18114a7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821359"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-threadx"></a><span data-ttu-id="defc0-103">Capitolo 2-installazione e uso di Azure RTO ThreadX</span><span class="sxs-lookup"><span data-stu-id="defc0-103">Chapter 2 - Installation and Use of Azure RTOS ThreadX</span></span>

<span data-ttu-id="defc0-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del kernel ThreadX di Azure RTO ad alte prestazioni.</span><span class="sxs-lookup"><span data-stu-id="defc0-104">This chapter contains a description of various issues related to installation, setup, and usage of the high-performance Azure RTOS ThreadX kernel.</span></span>

## <a name="host-considerations"></a><span data-ttu-id="defc0-105">Considerazioni sull'host</span><span class="sxs-lookup"><span data-stu-id="defc0-105">Host Considerations</span></span>

<span data-ttu-id="defc0-106">Il software incorporato viene in genere sviluppato in computer host Windows o Linux (Unix).</span><span class="sxs-lookup"><span data-stu-id="defc0-106">Embedded software is usually developed on Windows or Linux (Unix) host computers.</span></span> <span data-ttu-id="defc0-107">Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="defc0-107">After the application is compiled, linked, and located on the host, it is downloaded to the target hardware for execution.</span></span>

<span data-ttu-id="defc0-108">Il download di destinazione viene in genere eseguito dal debugger dello strumento di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="defc0-108">Usually the target download is done from within the development tool debugger.</span></span> <span data-ttu-id="defc0-109">Al termine del download, il debugger è responsabile per fornire il controllo dell'esecuzione di destinazione (go, Halt, breakpoint e così via), nonché per accedere ai registri della memoria e del processore.</span><span class="sxs-lookup"><span data-stu-id="defc0-109">After the download has completed, the debugger is responsible for providing target execution control (go, halt, breakpoint, etc.) as well as access to memory and processor registers.</span></span>

<span data-ttu-id="defc0-110">La maggior parte dei debugger dello strumento di sviluppo comunica con l'hardware di destinazione tramite connessioni di debug (OCD) on-chip come JTAG (IEEE 1149,1) e la modalità di debug in background (BDM).</span><span class="sxs-lookup"><span data-stu-id="defc0-110">Most development tool debuggers communicate with the target hardware via on-chip debug (OCD) connections such as JTAG (IEEE 1149.1) and Background Debug Mode (BDM).</span></span> <span data-ttu-id="defc0-111">I debugger comunicano anche con l'hardware di destinazione tramite connessioni di In-Circuit emulazione (ICE).</span><span class="sxs-lookup"><span data-stu-id="defc0-111">Debuggers also communicate with target hardware through In-Circuit Emulation (ICE) connections.</span></span> <span data-ttu-id="defc0-112">Le connessioni OCD e ICE forniscono soluzioni affidabili con intrusione minima sul software residente di destinazione.</span><span class="sxs-lookup"><span data-stu-id="defc0-112">Both OCD and ICE connections provide robust solutions with minimal intrusion on the target resident software.</span></span>

<span data-ttu-id="defc0-113">Per quanto riguarda le risorse usate nell'host, il codice sorgente per ThreadX viene fornito in formato ASCII e richiede circa 1 MB di spazio sul disco rigido del computer host.</span><span class="sxs-lookup"><span data-stu-id="defc0-113">As for resources used on the host, the source code for ThreadX is delivered in ASCII format and requires approximately 1 MByte of space on the host computer's hard disk.</span></span>

## <a name="target-considerations"></a><span data-ttu-id="defc0-114">Considerazioni sulla destinazione</span><span class="sxs-lookup"><span data-stu-id="defc0-114">Target Considerations</span></span>

<span data-ttu-id="defc0-115">ThreadX richiede tra 2 kbyte e 20 KByte di memoria di sola lettura (ROM) nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="defc0-115">ThreadX requires between 2 KBytes and 20 KBytes of Read Only Memory (ROM) on the target.</span></span> <span data-ttu-id="defc0-116">Richiede anche un altro da 1 a 2 KB della memoria ad accesso casuale (RAM) della destinazione per lo stack di sistema ThreadX e altre strutture di dati globali.</span><span class="sxs-lookup"><span data-stu-id="defc0-116">It also requires another 1 to 2 KBytes of the target's Random Access Memory (RAM) for the ThreadX system stack and other global data structures.</span></span>

<span data-ttu-id="defc0-117">Per le funzioni correlate al timer, ad esempio i timeout delle chiamate al servizio, il sezionamento di tempo e i timer dell'applicazione per funzionare, l'hardware di destinazione sottostante deve fornire un'origine di interrupt periodica.</span><span class="sxs-lookup"><span data-stu-id="defc0-117">For timer-related functions like service call time-outs, time-slicing, and application timers to function, the underlying target hardware must provide a periodic interrupt source.</span></span> <span data-ttu-id="defc0-118">Se il processore dispone di questa funzionalità, viene utilizzato da ThreadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-118">If the processor has this capability, it is utilized by ThreadX.</span></span> <span data-ttu-id="defc0-119">In caso contrario, se il processore di destinazione non è in grado di generare un interrupt periodico, l'hardware dell'utente deve fornirlo.</span><span class="sxs-lookup"><span data-stu-id="defc0-119">Otherwise, if the target processor does not have the ability to generate a periodic interrupt, the user's hardware must provide it.</span></span> <span data-ttu-id="defc0-120">Il programma di installazione e configurazione dell'interrupt del timer si trova in genere nel file di assembly ***tx_initialize_low_level*** nella distribuzione di threadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-120">Setup and configuration of the timer interrupt is typically located in the ***tx_initialize_low_level*** assembly file in the ThreadX distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="defc0-121">*ThreadX è ancora funzionante anche se non è disponibile un'origine interrupt del timer periodica. Tuttavia, nessuno dei servizi correlati al timer è funzionante.*</span><span class="sxs-lookup"><span data-stu-id="defc0-121">*ThreadX is still functional even if no periodic timer interrupt source is available. However, none of the timer-related services are functional.*</span></span>

## <a name="product-distribution"></a><span data-ttu-id="defc0-122">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="defc0-122">Product Distribution</span></span>

<span data-ttu-id="defc0-123">Azure RTO ThreadX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/threadx/> .</span><span class="sxs-lookup"><span data-stu-id="defc0-123">Azure RTOS ThreadX can be obtained from our public source code repository at <https://github.com/azure-rtos/threadx/>.</span></span>

<span data-ttu-id="defc0-124">Di seguito è riportato un elenco di diversi file importanti nel repository.</span><span class="sxs-lookup"><span data-stu-id="defc0-124">The following is a list of several important files in the repository.</span></span>

| <span data-ttu-id="defc0-125">Nome file</span><span class="sxs-lookup"><span data-stu-id="defc0-125">Filename</span></span> | <span data-ttu-id="defc0-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="defc0-126">Description</span></span> |
|------------------- | ----------- |
| <span data-ttu-id="defc0-127">**tx_api. h**</span><span class="sxs-lookup"><span data-stu-id="defc0-127">**tx_api.h**</span></span>                      | <span data-ttu-id="defc0-128">File di intestazione C contenente tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.</span><span class="sxs-lookup"><span data-stu-id="defc0-128">C header file containing all system equates, data structures, and service prototypes.</span></span>                                                             |
| <span data-ttu-id="defc0-129">**tx_port. h**</span><span class="sxs-lookup"><span data-stu-id="defc0-129">**tx_port.h**</span></span>                     | <span data-ttu-id="defc0-130">File di intestazione C contenente tutte le strutture e le definizioni dei dati dello strumento di sviluppo e del targetspecific.</span><span class="sxs-lookup"><span data-stu-id="defc0-130">C header file containing all development-tool and targetspecific data definitions and structures.</span></span>                                                 |
| <span data-ttu-id="defc0-131">**demo_threadx. c**</span><span class="sxs-lookup"><span data-stu-id="defc0-131">**demo_threadx.c**</span></span>                | <span data-ttu-id="defc0-132">File C contenente una piccola applicazione demo.</span><span class="sxs-lookup"><span data-stu-id="defc0-132">C file containing a small demo application.</span></span>                                                                                                       |
| <span data-ttu-id="defc0-133">**TX. a (o TX. lib)**</span><span class="sxs-lookup"><span data-stu-id="defc0-133">**tx.a (or tx.lib)**</span></span>              | <span data-ttu-id="defc0-134">Versione binaria della libreria ThreadX C distribuita con il pacchetto *standard* .</span><span class="sxs-lookup"><span data-stu-id="defc0-134">Binary version of the ThreadX C library that is distributed with the *standard* package.</span></span>                                                          |
|                                   |                                                                                                                                                   |

>[!NOTE]
><span data-ttu-id="defc0-135">*Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione rende più semplice convertire i comandi in piattaforme di sviluppo Linux (Unix).*</span><span class="sxs-lookup"><span data-stu-id="defc0-135">*All file names are in lower-case. This naming convention makes it easier to convert the commands to Linux (Unix) development platforms.*</span></span>

## <a name="threadx-installation"></a><span data-ttu-id="defc0-136">Installazione di ThreadX</span><span class="sxs-lookup"><span data-stu-id="defc0-136">ThreadX Installation</span></span>

<span data-ttu-id="defc0-137">ThreadX viene installato clonando il repository GitHub nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="defc0-137">ThreadX is installed by cloning the GitHub repository to your local machine.</span></span> <span data-ttu-id="defc0-138">Di seguito è riportata la sintassi tipica per la creazione di un clone del repository ThreadX nel PC.</span><span class="sxs-lookup"><span data-stu-id="defc0-138">The following is typical syntax for creating a clone of the ThreadX repository on your PC.</span></span>

```c
    git clone https://github.com/azure-rtos/threadx
```

<span data-ttu-id="defc0-139">In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.</span><span class="sxs-lookup"><span data-stu-id="defc0-139">Alternatively you can download a copy of the repository using the download button on the GitHub main page.</span></span>

<span data-ttu-id="defc0-140">Sono inoltre disponibili istruzioni per la compilazione della libreria ThreadX nella pagina iniziale del repository online.</span><span class="sxs-lookup"><span data-stu-id="defc0-140">You will also find instructions for building the ThreadX library on the front page of the online repository.</span></span>

> [!NOTE]
> <span data-ttu-id="defc0-141">\* Il software applicativo deve accedere al file di libreria ThreadX (in genere **TX. a** o **TX. lib**) e i file di inclusione C **_tx_api. h_* _ e _*_tx_port. h_\*_.</span><span class="sxs-lookup"><span data-stu-id="defc0-141">*Application software needs access to the ThreadX library file (usually **tx.a** or **tx.lib**) and the C include files **_tx_api.h_* _ and _*_tx_port.h_*_.</span></span> <span data-ttu-id="defc0-142">Questa operazione può essere eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nello sviluppo di applicazioni area._</span><span class="sxs-lookup"><span data-stu-id="defc0-142">This is accomplished either by setting the appropriate path for the development tools or by copying these files into the application development area._</span></span>

## <a name="using-threadx"></a><span data-ttu-id="defc0-143">Uso di ThreadX</span><span class="sxs-lookup"><span data-stu-id="defc0-143">Using ThreadX</span></span>

<span data-ttu-id="defc0-144">Per utilizzare ThreadX, è necessario che il codice dell'applicazione includa ***tx_api. h** _ durante la compilazione e il collegamento con la libreria di runtime threadX _*_TX. a_\*_ (o _ *_TX. lib_* \*).</span><span class="sxs-lookup"><span data-stu-id="defc0-144">To use ThreadX, the application code must include ***tx_api.h** _ during compilation and link with the ThreadX run-time library _*_tx.a_*_ (or _*_tx.lib_\*\*).</span></span>

<span data-ttu-id="defc0-145">Per compilare un'applicazione ThreadX, è necessario eseguire quattro passaggi.</span><span class="sxs-lookup"><span data-stu-id="defc0-145">There are four steps required to build a ThreadX application.</span></span>

1. <span data-ttu-id="defc0-146">Includere il file ***tx_api. h*** in tutti i file dell'applicazione che utilizzano i servizi o le strutture di dati threadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-146">Include the ***tx_api.h*** file in all application files that use ThreadX services or data structures.</span></span>

1. <span data-ttu-id="defc0-147">Creare la funzione C \***Main** _ standard.</span><span class="sxs-lookup"><span data-stu-id="defc0-147">Create the standard C \***main** _ function.</span></span> <span data-ttu-id="defc0-148">Questa funzione deve chiamare _ *_tx_kernel_enter_*\* per avviare threadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-148">This function must eventually call _ *_tx_kernel_enter_*\* to start ThreadX.</span></span> <span data-ttu-id="defc0-149">Prima di immettere il kernel, è possibile aggiungere un'inizializzazione specifica dell'applicazione che non include ThreadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-149">Application-specific initialization that does not involve ThreadX may be added prior to entering the kernel.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="defc0-150">\* La funzione di immissione ThreadX \***tx_kernel_enter** _ non restituisce alcun risultato.</span><span class="sxs-lookup"><span data-stu-id="defc0-150">\*The ThreadX entry function \***tx_kernel_enter** _ does not return.</span></span> <span data-ttu-id="defc0-151">Quindi, assicurarsi di non inserire alcuna chiamata di elaborazione o di funzione dopo it._</span><span class="sxs-lookup"><span data-stu-id="defc0-151">So be sure not to place any processing or function calls after it._</span></span>

1. <span data-ttu-id="defc0-152">Creare la funzione ***tx_application_define*** .</span><span class="sxs-lookup"><span data-stu-id="defc0-152">Create the ***tx_application_define*** function.</span></span> <span data-ttu-id="defc0-153">Questo è il punto in cui vengono create le risorse di sistema iniziali.</span><span class="sxs-lookup"><span data-stu-id="defc0-153">This is where the initial system resources are created.</span></span> <span data-ttu-id="defc0-154">Esempi di risorse di sistema includono thread, code, pool di memoria, gruppi di flag di evento, mutex e semafori.</span><span class="sxs-lookup"><span data-stu-id="defc0-154">Examples of system resources include threads, queues, memory pools, event flags groups, mutexes, and semaphores.</span></span>

1. <span data-ttu-id="defc0-155">Compilare l'origine e il collegamento dell'applicazione con la libreria di runtime ThreadX ***TX. lib***.</span><span class="sxs-lookup"><span data-stu-id="defc0-155">Compile application source and link with the ThreadX run-time library ***tx.lib***.</span></span> <span data-ttu-id="defc0-156">L'immagine risultante può essere scaricata nella destinazione ed eseguita.</span><span class="sxs-lookup"><span data-stu-id="defc0-156">The resulting image can be downloaded to the target and executed!</span></span>

## <a name="small-example-system"></a><span data-ttu-id="defc0-157">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="defc0-157">Small Example System</span></span>

<span data-ttu-id="defc0-158">Il piccolo sistema di esempio nella figura 1 illustra la creazione di un singolo thread con priorità 3.</span><span class="sxs-lookup"><span data-stu-id="defc0-158">The small example system in Figure 1 shows the creation of a single thread with a priority of 3.</span></span> <span data-ttu-id="defc0-159">Il thread viene eseguito, incrementa un contatore, quindi dorme per un tick del clock.</span><span class="sxs-lookup"><span data-stu-id="defc0-159">The thread executes, increments a counter, then sleeps for one clock tick.</span></span>
<span data-ttu-id="defc0-160">Questo processo continua per sempre.</span><span class="sxs-lookup"><span data-stu-id="defc0-160">This process continues forever.</span></span>

```c
#include "tx_api.h"
unsigned long my_thread_counter = 0;
TX_THREAD my_thread;
main( )
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter( );
}
void tx_application_define(void *first_unused_memory)
{
    /* Create my_thread! */
    tx_thread_create(&my_thread, "My Thread",
    my_thread_entry, 0x1234, first_unused_memory, 1024,
    3, 3, TX_NO_TIME_SLICE, TX_AUTO_START);
}
void my_thread_entry(ULONG thread_input)
{
    /* Enter into a forever loop. */
    while(1)
    {
        /* Increment thread counter. */
        my_thread_counter++;
        /* Sleep for 1 tick. */
        tx_thread_sleep(1);
    }
}
```

<span data-ttu-id="defc0-161">**FIGURA 1. Modello per lo sviluppo di applicazioni**</span><span class="sxs-lookup"><span data-stu-id="defc0-161">**FIGURE 1. Template for Application Development**</span></span>

<span data-ttu-id="defc0-162">Sebbene questo sia un semplice esempio, fornisce un modello efficace per lo sviluppo di applicazioni reali.</span><span class="sxs-lookup"><span data-stu-id="defc0-162">Although this is a simple example, it provides a good template for real application development.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="defc0-163">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="defc0-163">Troubleshooting</span></span>

<span data-ttu-id="defc0-164">Ogni porta ThreadX viene fornita con un'applicazione dimostrativa.</span><span class="sxs-lookup"><span data-stu-id="defc0-164">Each ThreadX port is delivered with a demonstration application.</span></span> <span data-ttu-id="defc0-165">È sempre consigliabile ottenere prima di tutto il sistema dimostrativo in esecuzione, nell'hardware di destinazione effettivo o nell'ambiente simulato.</span><span class="sxs-lookup"><span data-stu-id="defc0-165">It is always a good idea to first get the demonstration system running—either on actual target hardware or simulated environment.</span></span>

<span data-ttu-id="defc0-166">Se il sistema dimostrativo non viene eseguito correttamente, di seguito sono riportati alcuni suggerimenti per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="defc0-166">If the demonstration system does not execute properly, the following are some troubleshooting tips.</span></span>

1. <span data-ttu-id="defc0-167">Determinare la quantità della dimostrazione in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="defc0-167">Determine how much of the demonstration is running.</span></span>
1. <span data-ttu-id="defc0-168">Aumentare le dimensioni dello stack (questo aspetto è più importante nel codice dell'applicazione effettivo rispetto a quello per la dimostrazione).</span><span class="sxs-lookup"><span data-stu-id="defc0-168">Increase stack sizes (this is more important in actual application code than it is for the demonstration).</span></span>
1. <span data-ttu-id="defc0-169">Ricompilare la libreria ThreadX con TX_ENABLE_STACK_CHECKING definito.</span><span class="sxs-lookup"><span data-stu-id="defc0-169">Rebuild the ThreadX library with TX_ENABLE_STACK_CHECKING defined.</span></span> <span data-ttu-id="defc0-170">Questo consente il controllo dello stack ThreadX incorporato.</span><span class="sxs-lookup"><span data-stu-id="defc0-170">This enables the built-in ThreadX stack checking.</span></span>
1. <span data-ttu-id="defc0-171">Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="defc0-171">Temporarily bypass any recent changes to see if the problem disappears or changes.</span></span> <span data-ttu-id="defc0-172">Tali informazioni dovrebbero risultare utili per supportare i tecnici.</span><span class="sxs-lookup"><span data-stu-id="defc0-172">Such information should prove useful to support engineers.</span></span>

<span data-ttu-id="defc0-173">Seguire le procedure descritte in "[Customer Support Center](about-this-guide.md#customer-support-center)" per inviare le informazioni raccolte dalle procedure per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="defc0-173">Follow the procedures outlined in "[Customer Support Center](about-this-guide.md#customer-support-center)" to send the information gathered from the troubleshooting steps.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="defc0-174">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="defc0-174">Configuration Options</span></span>

<span data-ttu-id="defc0-175">Quando si compilano la libreria ThreadX e l'applicazione tramite ThreadX, sono disponibili diverse opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="defc0-175">There are several configuration options when building the ThreadX library and the application using ThreadX.</span></span> <span data-ttu-id="defc0-176">Le opzioni seguenti possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file di inclusione ***tx_user. h*** .</span><span class="sxs-lookup"><span data-stu-id="defc0-176">The options below can be defined in the application source, on the command line, or within the ***tx_user.h*** include file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="defc0-177">\* Le opzioni definite in ***tx_user. h** _ vengono applicate solo se l'applicazione e la libreria threadX sono compilate con _ *TX_INCLUDE_USER_DEFINE_FILE** definito.\*</span><span class="sxs-lookup"><span data-stu-id="defc0-177">*Options defined in ***tx_user.h** _ are applied only if the application and ThreadX library are built with _ *TX_INCLUDE_USER_DEFINE_FILE** defined.*</span></span>

### <a name="smallest-configuration"></a><span data-ttu-id="defc0-178">Configurazione minima</span><span class="sxs-lookup"><span data-stu-id="defc0-178">Smallest Configuration</span></span>

<span data-ttu-id="defc0-179">Per le dimensioni del codice più ridotte, è necessario considerare le seguenti opzioni di configurazione di ThreadX (in assenza di tutte le altre opzioni).</span><span class="sxs-lookup"><span data-stu-id="defc0-179">For the smallest code size, the following ThreadX configuration options should be considered (in absence of all other options).</span></span>

```c
TX_DISABLE_ERROR_CHECKING
TX_DISABLE_PREEMPTION_THRESHOLD
TX_DISABLE_NOTIFY_CALLBACKS
TX_DISABLE_REDUNDANT_CLEARING
TX_DISABLE_STACK_FILLING
TX_NOT_INTERRUPTABLE
TX_TIMER_PROCESS_IN_ISR
```

### <a name="fastest-configuration"></a><span data-ttu-id="defc0-180">Configurazione più veloce</span><span class="sxs-lookup"><span data-stu-id="defc0-180">Fastest Configuration</span></span>

<span data-ttu-id="defc0-181">Per l'esecuzione più veloce, le stesse opzioni di configurazione usate per la configurazione più piccola in precedenza, ma con queste opzioni considerate anche.</span><span class="sxs-lookup"><span data-stu-id="defc0-181">For the fastest execution, the same configuration options used for the Smallest Configuration previously, but with these options also considered.</span></span>

```c
TX_REACTIVATE_INLINE
TX_INLINE_THREAD_RESUME_SUSPEND
```

<span data-ttu-id="defc0-182">Sono descritte le [Opzioni di configurazione dettagliate](#detailed-configuration-options) .</span><span class="sxs-lookup"><span data-stu-id="defc0-182">[Detailed configuration options](#detailed-configuration-options) are described.</span></span>

### <a name="global-time-source"></a><span data-ttu-id="defc0-183">Origine ora globale</span><span class="sxs-lookup"><span data-stu-id="defc0-183">Global Time Source</span></span>

<span data-ttu-id="defc0-184">Per altri Microsoft Azure prodotti RTO (FileX, NetX, GUIX, USBX e così via), ThreadX definisce il numero di cicli del timer ThreadX che rappresentano un secondo.</span><span class="sxs-lookup"><span data-stu-id="defc0-184">For other Microsoft Azure RTOS products (FileX, NetX, GUIX, USBX, etc.), ThreadX defines the number of ThreadX timer ticks that represents one second.</span></span> <span data-ttu-id="defc0-185">Altre derivano i requisiti temporali in base a questa costante.</span><span class="sxs-lookup"><span data-stu-id="defc0-185">Others derive their time requirements based on this constant.</span></span> <span data-ttu-id="defc0-186">Per impostazione predefinita, il valore è 100, supponendo un interrupt 10 ms periodico.</span><span class="sxs-lookup"><span data-stu-id="defc0-186">By default, the value is 100, assuming a 10ms periodic interrupt.</span></span> <span data-ttu-id="defc0-187">È possibile che l'utente esegua l'override di questo valore definendo TX_TIMER_TICKS_PER_SECOND con il valore desiderato in ***tx_port. h*** o all'interno dell'IDE o della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="defc0-187">The user may override this value by defining TX_TIMER_TICKS_PER_SECOND with the desired value in ***tx_port.h*** or within the IDE or command line.</span></span>

### <a name="detailed-configuration-options"></a><span data-ttu-id="defc0-188">Opzioni di configurazione dettagliate</span><span class="sxs-lookup"><span data-stu-id="defc0-188">Detailed Configuration Options</span></span>

<span data-ttu-id="defc0-189">**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="defc0-189">**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="defc0-190">Quando viene definita, questa opzione consente di raccogliere informazioni sulle prestazioni nei pool di byte.</span><span class="sxs-lookup"><span data-stu-id="defc0-190">When defined, this option enables the gathering of performance information on byte pools.</span></span> <span data-ttu-id="defc0-191">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-191">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-192">**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="defc0-192">**TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="defc0-193">Quando viene definita, questa opzione consente di raccogliere informazioni sulle prestazioni nei pool di byte.</span><span class="sxs-lookup"><span data-stu-id="defc0-193">When defined, this option enables the gathering of performance information on byte pools.</span></span> <span data-ttu-id="defc0-194">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-194">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-195">**TX_DISABLE_ERROR_CHECKING**</span><span class="sxs-lookup"><span data-stu-id="defc0-195">**TX_DISABLE_ERROR_CHECKING**</span></span>

<span data-ttu-id="defc0-196">Ignora il controllo degli errori di chiamata al servizio di base.</span><span class="sxs-lookup"><span data-stu-id="defc0-196">Bypasses basic service call error checking.</span></span> <span data-ttu-id="defc0-197">Quando viene definito nell'origine dell'applicazione, tutto il controllo degli errori dei parametri di base è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="defc0-197">When defined in the application source, all basic parameter error checking is disabled.</span></span> <span data-ttu-id="defc0-198">Questo può migliorare le prestazioni fino al 30% e può anche ridurre le dimensioni dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="defc0-198">This may improve performance by as much as 30% and may also reduce the image size.</span></span>

> [!NOTE]
> <span data-ttu-id="defc0-199">*È possibile disabilitare il controllo degli errori solo se l'applicazione è in grado di garantire che tutti i parametri di input siano sempre validi in tutte le circostanze, inclusi i parametri di input derivati dall'input esterno. Se all'API viene fornito un input non valido con il controllo degli errori disabilitato, il comportamento risultante non è definito e potrebbe causare un danneggiamento della memoria o un arresto anomalo del sistema.*</span><span class="sxs-lookup"><span data-stu-id="defc0-199">*It is only safe to disable error checking if the application can absolutely guarantee all input parameters are always valid under all circumstances, including input parameters derived from external input. If invalid input is supplied to the API with error checking disabled, the resulting behavior is undefined and could result in memory corruption or system crash.*</span></span>

> [!NOTE]
> <span data-ttu-id="defc0-200">*I valori restituiti dell'API ThreadX non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella sezione "valori restituiti" della descrizione di ogni API del capitolo 4. I valori restituiti non in grassetto sono void se il controllo degli errori viene disabilitato usando l'opzione TX_DISABLE_ERROR_CHECKING.*</span><span class="sxs-lookup"><span data-stu-id="defc0-200">*ThreadX API return values not affected by disabling error checking are listed in bold in the “Return Values” section of each API description in Chapter 4. The nonbold return values are void if error checking is disabled by using the TX_DISABLE_ERROR_CHECKING option.*</span></span>

<span data-ttu-id="defc0-201">**TX_DISABLE_NOTIFY_CALLBACKS**</span><span class="sxs-lookup"><span data-stu-id="defc0-201">**TX_DISABLE_NOTIFY_CALLBACKS**</span></span>

<span data-ttu-id="defc0-202">Quando definito, Disabilita i callback di notifica per diversi oggetti ThreadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-202">When defined, disables the notify callbacks for various ThreadX objects.</span></span> <span data-ttu-id="defc0-203">L'utilizzo di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="defc0-203">Using this option slightly reduces code size and improves performance.</span></span> <span data-ttu-id="defc0-204">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-204">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-205">**TX_DISABLE_PREEMPTION_THRESHOLD**</span><span class="sxs-lookup"><span data-stu-id="defc0-205">**TX_DISABLE_PREEMPTION_THRESHOLD**</span></span>

<span data-ttu-id="defc0-206">Una volta definito, Disabilita la funzionalità di soglia di precedenza e riduce leggermente le dimensioni del codice e migliora le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="defc0-206">When defined, disables the preemption-threshold feature and slightly reduces code size and improves performance.</span></span> <span data-ttu-id="defc0-207">Naturalmente, le funzionalità di soglia di precedenza non sono più disponibili.</span><span class="sxs-lookup"><span data-stu-id="defc0-207">Of course, the preemption-threshold capabilities are no longer available.</span></span> <span data-ttu-id="defc0-208">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-208">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-209">**TX_DISABLE_REDUNDANT_CLEARING**</span><span class="sxs-lookup"><span data-stu-id="defc0-209">**TX_DISABLE_REDUNDANT_CLEARING**</span></span>

<span data-ttu-id="defc0-210">Quando definito, rimuove la logica per l'inizializzazione di strutture di dati C globali ThreadX su zero.</span><span class="sxs-lookup"><span data-stu-id="defc0-210">When defined, removes the logic for initializing ThreadX global C data structures to zero.</span></span> <span data-ttu-id="defc0-211">Questa operazione deve essere usata solo se il codice di inizializzazione del compilatore imposta tutti i dati globali non inizializzati su zero.</span><span class="sxs-lookup"><span data-stu-id="defc0-211">This should only be used if the compiler's initialization code sets all un-initialized C global data to zero.</span></span> <span data-ttu-id="defc0-212">L'utilizzo di questa opzione riduce leggermente le dimensioni del codice e migliora le prestazioni durante l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="defc0-212">Using this option slightly reduces code size and improves performance during initialization.</span></span> <span data-ttu-id="defc0-213">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-213">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-214">**TX_DISABLE_STACK_FILLING**</span><span class="sxs-lookup"><span data-stu-id="defc0-214">**TX_DISABLE_STACK_FILLING**</span></span>

<span data-ttu-id="defc0-215">Quando viene definito, Disabilita l'inserimento del valore 0xEF in ogni byte dello stack di ogni thread al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="defc0-215">When defined, disables placing the 0xEF value in each byte of each thread's stack when created.</span></span> <span data-ttu-id="defc0-216">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-216">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-217">**TX_ENABLE_EVENT_TRACE**</span><span class="sxs-lookup"><span data-stu-id="defc0-217">**TX_ENABLE_EVENT_TRACE**</span></span>

<span data-ttu-id="defc0-218">Quando viene definito, ThreadX Abilita il codice di raccolta eventi per la creazione di un buffer di traccia TraceX.</span><span class="sxs-lookup"><span data-stu-id="defc0-218">When defined, ThreadX enables the event gathering code for creating a TraceX trace buffer.</span></span>

<span data-ttu-id="defc0-219">**TX_ENABLE_STACK_CHECKING**</span><span class="sxs-lookup"><span data-stu-id="defc0-219">**TX_ENABLE_STACK_CHECKING**</span></span>

<span data-ttu-id="defc0-220">Quando definito, Abilita il controllo dello stack in fase di esecuzione ThreadX, che include l'analisi dello stack usato e l'esame dei "limiti" del modello di dati prima e dopo l'area dello stack.</span><span class="sxs-lookup"><span data-stu-id="defc0-220">When defined, enables ThreadX run-time stack checking, which includes analysis of how much stack has been used and examination of data pattern "fences" before and after the stack area.</span></span> <span data-ttu-id="defc0-221">Se viene rilevato un errore dello stack, viene chiamato il gestore degli errori dello stack dell'applicazione registrato.</span><span class="sxs-lookup"><span data-stu-id="defc0-221">If a stack error is detected, the registered application stack error handler is called.</span></span> <span data-ttu-id="defc0-222">Questa opzione comporta un sovraccarico leggermente maggiore e una dimensione del codice.</span><span class="sxs-lookup"><span data-stu-id="defc0-222">This option does result in slightly increased overhead and code size.</span></span> <span data-ttu-id="defc0-223">Per ulteriori informazioni, esaminare la funzione API ***tx_thread_stack_error_notify*** .</span><span class="sxs-lookup"><span data-stu-id="defc0-223">Review the ***tx_thread_stack_error_notify*** API function for more information.</span></span> <span data-ttu-id="defc0-224">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-224">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-225">**TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="defc0-225">**TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="defc0-226">Quando definito, Abilita la raccolta di informazioni sulle prestazioni nei gruppi di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="defc0-226">When defined, enables the gathering of performance information on event flags groups.</span></span> <span data-ttu-id="defc0-227">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-227">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-228">**TX_INLINE_THREAD_RESUME_SUSPEND**</span><span class="sxs-lookup"><span data-stu-id="defc0-228">**TX_INLINE_THREAD_RESUME_SUSPEND**</span></span>

<span data-ttu-id="defc0-229">Quando viene definito, ThreadX migliora le chiamate API ***tx_thread_resume** _ e _ *_tx_thread_suspend_** tramite il codice inline.</span><span class="sxs-lookup"><span data-stu-id="defc0-229">When defined, ThreadX improves the ***tx_thread_resume** _ and _ *_tx_thread_suspend_** API calls via in-line code.</span></span> <span data-ttu-id="defc0-230">Questo aumenta le dimensioni del codice, ma migliora le prestazioni di queste due chiamate API.</span><span class="sxs-lookup"><span data-stu-id="defc0-230">This increases code size but enhances performance of these two API calls.</span></span>

<span data-ttu-id="defc0-231">**TX_MAX_PRIORITIES**</span><span class="sxs-lookup"><span data-stu-id="defc0-231">**TX_MAX_PRIORITIES**</span></span>

<span data-ttu-id="defc0-232">Definisce i livelli di priorità per ThreadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-232">Defines the priority levels for ThreadX.</span></span> <span data-ttu-id="defc0-233">I valori validi sono compresi tra 32 e 1024 (inclusi) e *devono* essere divisibile in modo uniforme per 32.</span><span class="sxs-lookup"><span data-stu-id="defc0-233">Legal values range from 32 through 1024 (inclusive) and *must* be evenly divisible by 32.</span></span> <span data-ttu-id="defc0-234">L'aumento del numero di livelli di priorità supportati aumenta l'utilizzo della RAM di 128 byte per ogni gruppo di 32 priorità.</span><span class="sxs-lookup"><span data-stu-id="defc0-234">Increasing the number of priority levels supported increases the RAM usage by 128 bytes for every group of 32 priorities.</span></span> <span data-ttu-id="defc0-235">Tuttavia, esiste solo un effetto trascurabile sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="defc0-235">However, there is only a negligible effect on performance.</span></span> <span data-ttu-id="defc0-236">Per impostazione predefinita, questo valore è impostato su 32 livelli di priorità.</span><span class="sxs-lookup"><span data-stu-id="defc0-236">By default, this value is set to 32 priority levels.</span></span>

<span data-ttu-id="defc0-237">**TX_MINIMUM_STACK**</span><span class="sxs-lookup"><span data-stu-id="defc0-237">**TX_MINIMUM_STACK**</span></span>

<span data-ttu-id="defc0-238">Definisce la dimensione minima dello stack (in byte).</span><span class="sxs-lookup"><span data-stu-id="defc0-238">Defines the minimum stack size (in bytes).</span></span> <span data-ttu-id="defc0-239">Viene usato per il controllo degli errori quando vengono creati i thread.</span><span class="sxs-lookup"><span data-stu-id="defc0-239">It is used for error checking when threads are created.</span></span> <span data-ttu-id="defc0-240">Il valore predefinito è specifico della porta ed è disponibile in ***tx_port. h***.</span><span class="sxs-lookup"><span data-stu-id="defc0-240">The default value is port-specific and is found in ***tx_port.h***.</span></span>

<span data-ttu-id="defc0-241">**TX_MISRA_ENABLE**</span><span class="sxs-lookup"><span data-stu-id="defc0-241">**TX_MISRA_ENABLE**</span></span>

<span data-ttu-id="defc0-242">Quando viene definito, ThreadX utilizza le convenzioni conformi a MISRA C.</span><span class="sxs-lookup"><span data-stu-id="defc0-242">When defined, ThreadX utilizes MISRA C compliant conventions.</span></span> <span data-ttu-id="defc0-243">Per informazioni dettagliate, vedere  ***ThreadX_MISRA_Compliance.pdf*** .</span><span class="sxs-lookup"><span data-stu-id="defc0-243">Refer to  ***ThreadX_MISRA_Compliance.pdf*** for details.</span></span>

<span data-ttu-id="defc0-244">**TX_MUTEX_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="defc0-244">**TX_MUTEX_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="defc0-245">Quando definito, Abilita la raccolta di informazioni sulle prestazioni nei mutex.</span><span class="sxs-lookup"><span data-stu-id="defc0-245">When defined, enables the gathering of performance information on mutexes.</span></span> <span data-ttu-id="defc0-246">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-246">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-247">**TX_NO_TIMER**</span><span class="sxs-lookup"><span data-stu-id="defc0-247">**TX_NO_TIMER**</span></span>

<span data-ttu-id="defc0-248">Quando è definito, la logica del timer ThreadX è completamente disabilitata.</span><span class="sxs-lookup"><span data-stu-id="defc0-248">When defined, the ThreadX timer logic is completely disabled.</span></span> <span data-ttu-id="defc0-249">Questa operazione è utile nei casi in cui le funzionalità del timer ThreadX (sospensione thread, timeout API, sezionamento del tempo e timer applicazione) non vengono utilizzate.</span><span class="sxs-lookup"><span data-stu-id="defc0-249">This is useful in cases where the ThreadX timer features (thread sleep, API timeouts, time-slicing, and application timers) are not utilized.</span></span> <span data-ttu-id="defc0-250">Se **TX_NO_TIMER** è specificato, è necessario definire anche l'opzione **TX_TIMER_PROCESS_IN_ISR** .</span><span class="sxs-lookup"><span data-stu-id="defc0-250">If **TX_NO_TIMER** is specified, the option **TX_TIMER_PROCESS_IN_ISR** must also be defined.</span></span>

<span data-ttu-id="defc0-251">**TX_NOT_INTERRUPTABLE**</span><span class="sxs-lookup"><span data-stu-id="defc0-251">**TX_NOT_INTERRUPTABLE**</span></span>

<span data-ttu-id="defc0-252">Quando viene definito, ThreadX non tenta di ridurre al minimo il tempo di blocco dell'interrupt.</span><span class="sxs-lookup"><span data-stu-id="defc0-252">When defined, ThreadX does not attempt to minimize interrupt lockout time.</span></span> <span data-ttu-id="defc0-253">Questo comporta un'esecuzione più rapida, ma aumenta leggermente il tempo di blocco dell'interrupt.</span><span class="sxs-lookup"><span data-stu-id="defc0-253">This results in faster execution but does slightly increase interrupt lockout time.</span></span>

<span data-ttu-id="defc0-254">**TX_QUEUE_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="defc0-254">**TX_QUEUE_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="defc0-255">Quando definito, consente la raccolta di informazioni sulle prestazioni sulle code.</span><span class="sxs-lookup"><span data-stu-id="defc0-255">When defined, enables the gathering of performance information on queues.</span></span> <span data-ttu-id="defc0-256">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-256">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-257">**TX_REACTIVATE_INLINE**</span><span class="sxs-lookup"><span data-stu-id="defc0-257">**TX_REACTIVATE_INLINE**</span></span>

<span data-ttu-id="defc0-258">Quando definito, esegue la riattivazione dei timer ThreadX inline invece di usare una chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="defc0-258">When defined, performs reactivation of ThreadX timers inline instead of using a function call.</span></span> <span data-ttu-id="defc0-259">Ciò migliora le prestazioni, ma aumenta leggermente le dimensioni del codice.</span><span class="sxs-lookup"><span data-stu-id="defc0-259">This improves performance but slightly increases code size.</span></span> <span data-ttu-id="defc0-260">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-260">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-261">**TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="defc0-261">**TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="defc0-262">Quando definito, Abilita la raccolta di informazioni sulle prestazioni sui semafori.</span><span class="sxs-lookup"><span data-stu-id="defc0-262">When defined, enables the gathering of performance information on semaphores.</span></span> <span data-ttu-id="defc0-263">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-263">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-264">**TX_THREAD_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="defc0-264">**TX_THREAD_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="defc0-265">Quando definito, Abilita la raccolta di informazioni sulle prestazioni nei thread.</span><span class="sxs-lookup"><span data-stu-id="defc0-265">When defined, enables the gathering of performance information on threads.</span></span> <span data-ttu-id="defc0-266">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-266">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-267">**TX_TIMER_ENABLE_PERFORMANCE_INFO**</span><span class="sxs-lookup"><span data-stu-id="defc0-267">**TX_TIMER_ENABLE_PERFORMANCE_INFO**</span></span>

<span data-ttu-id="defc0-268">Quando definito, consente la raccolta di informazioni sulle prestazioni sui timer.</span><span class="sxs-lookup"><span data-stu-id="defc0-268">When defined, enables the gathering of performance information on timers.</span></span> <span data-ttu-id="defc0-269">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-269">By default, this option is not defined.</span></span>

<span data-ttu-id="defc0-270">**TX_TIMER_PROCESS_IN_ISR**</span><span class="sxs-lookup"><span data-stu-id="defc0-270">**TX_TIMER_PROCESS_IN_ISR**</span></span>

<span data-ttu-id="defc0-271">Una volta definito, Elimina il thread del timer interno di sistema per ThreadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-271">When defined, eliminates the internal system timer thread for ThreadX.</span></span> <span data-ttu-id="defc0-272">Ciò comporta un miglioramento delle prestazioni sugli eventi del timer e requisiti di RAM più piccoli, perché lo stack del timer e il blocco di controllo non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="defc0-272">This results in improved performance on timer events and smaller RAM requirements because the timer stack and control block are no longer needed.</span></span> <span data-ttu-id="defc0-273">Tuttavia, se si usa questa opzione, l'elaborazione della scadenza del timer viene spostata al livello ISR del timer.</span><span class="sxs-lookup"><span data-stu-id="defc0-273">However, using this option moves all the timer expiration processing to the timer ISR level.</span></span> <span data-ttu-id="defc0-274">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="defc0-274">By default, this option is not defined.</span></span>

> [!NOTE]
> <span data-ttu-id="defc0-275">*I servizi consentiti dai timer potrebbero non essere consentiti da ISRs e pertanto potrebbero non essere consentiti quando si usa questa opzione.*</span><span class="sxs-lookup"><span data-stu-id="defc0-275">*Services allowed from timers may not be allowed from ISRs and thus might not be allowed when using this option.*</span></span>

<span data-ttu-id="defc0-276">**TX_TIMER_THREAD_PRIORITY**</span><span class="sxs-lookup"><span data-stu-id="defc0-276">**TX_TIMER_THREAD_PRIORITY**</span></span>

<span data-ttu-id="defc0-277">Definisce la priorità del thread timer interno di sistema ThreadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-277">Defines the priority of the internal ThreadX system timer thread.</span></span> <span data-ttu-id="defc0-278">Il valore predefinito è priority 0, ovvero la priorità più alta in ThreadX.</span><span class="sxs-lookup"><span data-stu-id="defc0-278">The default value is priority 0—the highest priority in ThreadX.</span></span> <span data-ttu-id="defc0-279">Il valore predefinito è definito in ***tx_port. h***.</span><span class="sxs-lookup"><span data-stu-id="defc0-279">The default value is defined in ***tx_port.h***.</span></span>

<span data-ttu-id="defc0-280">**TX_TIMER_THREAD_STACK_SIZE**</span><span class="sxs-lookup"><span data-stu-id="defc0-280">**TX_TIMER_THREAD_STACK_SIZE**</span></span>

<span data-ttu-id="defc0-281">Definisce la dimensione dello stack (in byte) del thread del timer di sistema ThreadX interno.</span><span class="sxs-lookup"><span data-stu-id="defc0-281">Defines the stack size (in bytes) of the internal ThreadX system timer thread.</span></span> <span data-ttu-id="defc0-282">Questo thread elabora tutte le richieste di sospensione del thread, nonché tutti i timeout delle chiamate al servizio.</span><span class="sxs-lookup"><span data-stu-id="defc0-282">This thread processes all thread sleep requests as well as all service call timeouts.</span></span> <span data-ttu-id="defc0-283">Inoltre, tutte le routine di callback del timer applicazione vengono richiamate da questo contesto.</span><span class="sxs-lookup"><span data-stu-id="defc0-283">In addition, all application timer callback routines are invoked from this context.</span></span> <span data-ttu-id="defc0-284">Il valore predefinito è specifico della porta ed è disponibile in ***tx_port. h***.</span><span class="sxs-lookup"><span data-stu-id="defc0-284">The default value is port-specific and is found in ***tx_port.h***.</span></span>

## <a name="threadx-version-id"></a><span data-ttu-id="defc0-285">ID versione ThreadX</span><span class="sxs-lookup"><span data-stu-id="defc0-285">ThreadX Version ID</span></span>

<span data-ttu-id="defc0-286">Il programmatore può ottenere la versione di ThreadX dall'esame del file \***tx_port. h** _.</span><span class="sxs-lookup"><span data-stu-id="defc0-286">The programmer can obtain the ThreadX version from examination of the \***tx_port.h** _ file.</span></span> <span data-ttu-id="defc0-287">Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente.</span><span class="sxs-lookup"><span data-stu-id="defc0-287">In addition, this file also contains a version history of the corresponding port.</span></span> <span data-ttu-id="defc0-288">Il software applicativo può ottenere la versione di ThreadX esaminando la stringa globale _ \* _tx_version_id \* \*.</span><span class="sxs-lookup"><span data-stu-id="defc0-288">Application software can obtain the ThreadX version by examining the global string _\*_tx_version_id\*\*.</span></span>
