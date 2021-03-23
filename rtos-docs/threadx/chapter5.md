---
title: Capitolo 5-driver di dispositivo per Azure RTO ThreadX
description: Questo capitolo contiene una descrizione dei driver di dispositivo per Azure RTO ThreadX.
author: philmea
ms.author: philmea
ms.date: 05/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2432b291f2b3fa7d6d798b8b4c187dd20b97db6b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823261"
---
# <a name="chapter-5---device-drivers-for-azure-rtos-threadx"></a><span data-ttu-id="d8c44-103">Capitolo 5-driver di dispositivo per Azure RTO ThreadX</span><span class="sxs-lookup"><span data-stu-id="d8c44-103">Chapter 5 - Device Drivers for Azure RTOS ThreadX</span></span>

<span data-ttu-id="d8c44-104">Questo capitolo contiene una descrizione dei driver di dispositivo per Azure RTO ThreadX.</span><span class="sxs-lookup"><span data-stu-id="d8c44-104">This chapter contains a description of device drivers for Azure RTOS ThreadX.</span></span> <span data-ttu-id="d8c44-105">Le informazioni presentate in questo capitolo sono progettate per aiutare gli sviluppatori a scrivere driver specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-105">The information presented in this chapter is designed to help developers write application-specific drivers.</span></span>

## <a name="device-driver-introduction"></a><span data-ttu-id="d8c44-106">Introduzione al driver di dispositivo</span><span class="sxs-lookup"><span data-stu-id="d8c44-106">Device Driver Introduction</span></span>

<span data-ttu-id="d8c44-107">La comunicazione con l'ambiente esterno è un componente importante della maggior parte delle applicazioni incorporate.</span><span class="sxs-lookup"><span data-stu-id="d8c44-107">Communication with the external environment is an important component of most embedded applications.</span></span> <span data-ttu-id="d8c44-108">Questa comunicazione viene eseguita tramite dispositivi hardware accessibili al software dell'applicazione incorporato.</span><span class="sxs-lookup"><span data-stu-id="d8c44-108">This communication is accomplished through hardware devices that are accessible to the embedded application software.</span></span> <span data-ttu-id="d8c44-109">I componenti software responsabili della gestione di tali dispositivi sono comunemente denominati *driver di dispositivo*.</span><span class="sxs-lookup"><span data-stu-id="d8c44-109">The software components responsible for managing such devices are commonly called *device drivers*.</span></span>

<span data-ttu-id="d8c44-110">I driver di dispositivo in sistemi incorporati e in tempo reale sono intrinsecamente dipendenti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-110">Device drivers in embedded, real-time systems are inherently application dependent.</span></span> <span data-ttu-id="d8c44-111">Questo vale per due motivi principali: la vasta gamma di hardware di destinazione e i requisiti di prestazioni ugualmente vasti imposti sulle applicazioni in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="d8c44-111">This is true for two principal reasons: the vast diversity of target hardware and the equally vast performance requirements imposed on real-time applications.</span></span> <span data-ttu-id="d8c44-112">Per questo motivo, è praticamente impossibile fornire un set comune di driver che soddisfino i requisiti di ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-112">Because of this, it is virtually impossible to provide a common set of drivers that will meet the requirements of every application.</span></span> <span data-ttu-id="d8c44-113">Per questi motivi, le informazioni contenute in questo capitolo sono progettate per aiutare gli utenti a personalizzare i driver di dispositivo threadX *fuori piano* e scrivere i propri driver specifici.</span><span class="sxs-lookup"><span data-stu-id="d8c44-113">For these reasons, the information in this chapter is designed to help users customize *off-the-shelf* ThreadX device drivers and write their own specific drivers.</span></span>

## <a name="driver-functions"></a><span data-ttu-id="d8c44-114">Funzioni driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-114">Driver Functions</span></span>

<span data-ttu-id="d8c44-115">I driver di dispositivo ThreadX sono costituiti da otto aree funzionali di base, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d8c44-115">ThreadX device drivers are composed of eight basic functional areas, as follows.</span></span>

- <span data-ttu-id="d8c44-116">**Inizializzazione driver**</span><span class="sxs-lookup"><span data-stu-id="d8c44-116">**Driver Initialization**</span></span>
- <span data-ttu-id="d8c44-117">**Controllo driver**</span><span class="sxs-lookup"><span data-stu-id="d8c44-117">**Driver Control**</span></span>
- <span data-ttu-id="d8c44-118">**Accesso driver**</span><span class="sxs-lookup"><span data-stu-id="d8c44-118">**Driver Access**</span></span>
- <span data-ttu-id="d8c44-119">**Input driver**</span><span class="sxs-lookup"><span data-stu-id="d8c44-119">**Driver Input**</span></span>
- <span data-ttu-id="d8c44-120">**Output driver**</span><span class="sxs-lookup"><span data-stu-id="d8c44-120">**Driver Output**</span></span>
- <span data-ttu-id="d8c44-121">**Interrupt driver**</span><span class="sxs-lookup"><span data-stu-id="d8c44-121">**Driver Interrupts**</span></span>
- <span data-ttu-id="d8c44-122">**Stato driver**</span><span class="sxs-lookup"><span data-stu-id="d8c44-122">**Driver Status**</span></span>
- <span data-ttu-id="d8c44-123">**Terminazione driver**</span><span class="sxs-lookup"><span data-stu-id="d8c44-123">**Driver Termination**</span></span>

<span data-ttu-id="d8c44-124">Ad eccezione dell'inizializzazione, ogni area funzionale del driver è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="d8c44-124">With the exception of initialization, each driver functional area is optional.</span></span> <span data-ttu-id="d8c44-125">L'elaborazione esatta in ogni area è inoltre specifica del driver di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-125">Furthermore, the exact processing in each area is specific to the device driver.</span></span>

### <a name="driver-initialization"></a><span data-ttu-id="d8c44-126">Inizializzazione driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-126">Driver Initialization</span></span>
<span data-ttu-id="d8c44-127">Questa area funzionale è responsabile dell'inizializzazione del dispositivo hardware effettivo e delle strutture di dati interne del driver.</span><span class="sxs-lookup"><span data-stu-id="d8c44-127">This functional area is responsible for initialization of the actual hardware device and the internal data structures of the driver.</span></span> <span data-ttu-id="d8c44-128">La chiamata di altri servizi driver non è consentita fino al completamento dell'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-128">Calling other driver services is not allowed until initialization is complete.</span></span>

> [!NOTE]
> <span data-ttu-id="d8c44-129">\* Il componente della funzione di inizializzazione del driver viene in genere chiamato dalla funzione \***tx_application_define** _ o da un'inizializzazione thread._</span><span class="sxs-lookup"><span data-stu-id="d8c44-129">\*The driver's initialization function component is typically called from the \***tx_application_define** _ function or from an initialization thread._</span></span>

### <a name="driver-control"></a><span data-ttu-id="d8c44-130">Controllo driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-130">Driver Control</span></span>

<span data-ttu-id="d8c44-131">Una volta che il driver è stato inizializzato e pronto per l'operazione, l'area funzionale è responsabile del controllo di Runtime.</span><span class="sxs-lookup"><span data-stu-id="d8c44-131">After the driver is initialized and ready for operation, this functional area is responsible for run-time control.</span></span> <span data-ttu-id="d8c44-132">In genere, il controllo in fase di esecuzione è costituito da modifiche al dispositivo hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="d8c44-132">Typically, run-time control consists of making changes to the underlying hardware device.</span></span> <span data-ttu-id="d8c44-133">Gli esempi includono la modifica della velocità in baud di un dispositivo seriale o la ricerca di un nuovo settore su un disco.</span><span class="sxs-lookup"><span data-stu-id="d8c44-133">Examples include changing the baud rate of a serial device or seeking a new sector on a disk.</span></span>

### <a name="driver-access"></a><span data-ttu-id="d8c44-134">Accesso driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-134">Driver Access</span></span>

<span data-ttu-id="d8c44-135">Alcuni driver di dispositivo vengono chiamati solo da un singolo thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-135">Some device drivers are called only from a single application thread.</span></span> <span data-ttu-id="d8c44-136">In questi casi, questa area funzionale non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="d8c44-136">In such cases, this functional area is not needed.</span></span> <span data-ttu-id="d8c44-137">Tuttavia, nelle applicazioni in cui più thread necessitano dell'accesso simultaneo ai driver, l'interazione deve essere controllata aggiungendo le funzionalità di assegnazione/rilascio nel driver di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-137">However, in applications where multiple threads need simultaneous driver access, their interaction must be controlled by adding assign/ release facilities in the device driver.</span></span> <span data-ttu-id="d8c44-138">In alternativa, l'applicazione può utilizzare un semaforo per controllare l'accesso dei driver ed evitare overhead e complicazioni aggiuntive all'interno del driver.</span><span class="sxs-lookup"><span data-stu-id="d8c44-138">Alternatively, the application may use a semaphore to control driver access and avoid extra overhead and complication inside the driver.</span></span>

### <a name="driver-input"></a><span data-ttu-id="d8c44-139">Input driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-139">Driver Input</span></span>

<span data-ttu-id="d8c44-140">Questa area funzionale è responsabile di tutti gli input del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-140">This functional area is responsible for all device input.</span></span> <span data-ttu-id="d8c44-141">I problemi principali associati all'input del driver coinvolgono in genere il modo in cui l'input viene memorizzato nel buffer e il modo in cui i thread attendono tale input.</span><span class="sxs-lookup"><span data-stu-id="d8c44-141">The principal issues associated with driver input usually involve how the input is buffered and how threads wait for such input.</span></span>

### <a name="driver-output"></a><span data-ttu-id="d8c44-142">Output driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-142">Driver Output</span></span>

<span data-ttu-id="d8c44-143">Questa area funzionale è responsabile di tutti gli output del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-143">This functional area is responsible for all device output.</span></span> <span data-ttu-id="d8c44-144">I problemi principali associati all'output del driver comportano in genere il modo in cui l'output viene memorizzato nel buffer e i thread in attesa di eseguire l'output.</span><span class="sxs-lookup"><span data-stu-id="d8c44-144">The principal issues associated with driver output usually involve how the output is buffered and how threads wait to perform output.</span></span>

### <a name="driver-interrupts"></a><span data-ttu-id="d8c44-145">Interrupt driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-145">Driver Interrupts</span></span>

<span data-ttu-id="d8c44-146">La maggior parte dei sistemi in tempo reale si basa su interrupt hardware per notificare al driver l'input, l'output, il controllo e gli eventi di errore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-146">Most real-time systems rely on hardware interrupts to notify the driver of device input, output, control, and error events.</span></span> <span data-ttu-id="d8c44-147">Gli interrupt forniscono tempi di risposta garantiti a tali eventi esterni.</span><span class="sxs-lookup"><span data-stu-id="d8c44-147">Interrupts provide a guaranteed response time to such external events.</span></span> <span data-ttu-id="d8c44-148">Anziché gli interrupt, il software del driver potrebbe controllare periodicamente l'hardware esterno per tali eventi.</span><span class="sxs-lookup"><span data-stu-id="d8c44-148">Instead of interrupts, the driver software may periodically check the external hardware for such events.</span></span> <span data-ttu-id="d8c44-149">Questa tecnica è denominata *polling*.</span><span class="sxs-lookup"><span data-stu-id="d8c44-149">This technique is called *polling*.</span></span> <span data-ttu-id="d8c44-150">È meno tempo reale degli interrupt, ma il polling può essere utile per alcune applicazioni meno in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="d8c44-150">It is less real-time than interrupts, but polling may make sense for some less real-time applications.</span></span>

### <a name="driver-status"></a><span data-ttu-id="d8c44-151">Stato driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-151">Driver Status</span></span>

<span data-ttu-id="d8c44-152">Questa area di funzione è responsabile della fornitura di statistiche e stato di run-time associate all'operazione del driver.</span><span class="sxs-lookup"><span data-stu-id="d8c44-152">This function area is responsible for providing run-time status and statistics associated with the driver operation.</span></span> <span data-ttu-id="d8c44-153">Le informazioni gestite da questa area di funzione includono in genere quanto segue.</span><span class="sxs-lookup"><span data-stu-id="d8c44-153">Information managed by this function area typically includes the following.</span></span>

- <span data-ttu-id="d8c44-154">Stato corrente del dispositivo</span><span class="sxs-lookup"><span data-stu-id="d8c44-154">Current device status</span></span>
- <span data-ttu-id="d8c44-155">Byte di input</span><span class="sxs-lookup"><span data-stu-id="d8c44-155">Input bytes</span></span>
- <span data-ttu-id="d8c44-156">Byte di output</span><span class="sxs-lookup"><span data-stu-id="d8c44-156">Output bytes</span></span>
- <span data-ttu-id="d8c44-157">Conteggi errori del dispositivo</span><span class="sxs-lookup"><span data-stu-id="d8c44-157">Device error counts</span></span>

### <a name="driver-termination"></a><span data-ttu-id="d8c44-158">Terminazione driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-158">Driver Termination</span></span>

<span data-ttu-id="d8c44-159">Questa area funzionale è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="d8c44-159">This functional area is optional.</span></span> <span data-ttu-id="d8c44-160">È necessario solo se il driver e/o il dispositivo hardware fisico devono essere arrestati.</span><span class="sxs-lookup"><span data-stu-id="d8c44-160">It is only required if the driver and/or the physical hardware device need to be shut down.</span></span> <span data-ttu-id="d8c44-161">Dopo la terminazione, il driver non deve essere chiamato di nuovo fino a quando non viene reinizializzato.</span><span class="sxs-lookup"><span data-stu-id="d8c44-161">After being terminated, the driver must not be called again until it is reinitialized.</span></span>

## <a name="simple-driver-example"></a><span data-ttu-id="d8c44-162">Esempio di driver semplice</span><span class="sxs-lookup"><span data-stu-id="d8c44-162">Simple Driver Example</span></span>

<span data-ttu-id="d8c44-163">Un esempio è il modo migliore per descrivere un driver di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-163">An example is the best way to describe a device driver.</span></span> <span data-ttu-id="d8c44-164">In questo esempio, il driver presuppone un semplice dispositivo hardware seriale con un registro di configurazione, un registro di input e un registro di output.</span><span class="sxs-lookup"><span data-stu-id="d8c44-164">In this example, the driver assumes a simple serial hardware device with a configuration register, an input register, and an output register.</span></span> <span data-ttu-id="d8c44-165">Questo semplice esempio di driver illustra le aree funzionali di inizializzazione, input, output e interrupt.</span><span class="sxs-lookup"><span data-stu-id="d8c44-165">This simple driver example illustrates the initialization, input, output, and interrupt functional areas.</span></span>

### <a name="simple-driver-initialization"></a><span data-ttu-id="d8c44-166">Inizializzazione driver semplice</span><span class="sxs-lookup"><span data-stu-id="d8c44-166">Simple Driver Initialization</span></span>

<span data-ttu-id="d8c44-167">La funzione ***tx_sdriver_initialize*** del driver semplice crea due semafori di conteggio usati per gestire l'operazione di input e output del driver.</span><span class="sxs-lookup"><span data-stu-id="d8c44-167">The ***tx_sdriver_initialize*** function of the simple driver creates two counting semaphores that are used to manage the driver's input and output operation.</span></span> <span data-ttu-id="d8c44-168">Il semaforo di input viene impostato dall'ISR di input quando un carattere viene ricevuto dal dispositivo hardware seriale.</span><span class="sxs-lookup"><span data-stu-id="d8c44-168">The input semaphore is set by the input ISR when a character is received by the serial hardware device.</span></span> <span data-ttu-id="d8c44-169">Per questo motivo, il semaforo di input viene creato con un conteggio iniziale pari a zero.</span><span class="sxs-lookup"><span data-stu-id="d8c44-169">Because of this, the input semaphore is created with an initial count of zero.</span></span>

<span data-ttu-id="d8c44-170">Viceversa, il semaforo di output indica la disponibilità del registro di trasmissione hardware seriale.</span><span class="sxs-lookup"><span data-stu-id="d8c44-170">Conversely, the output semaphore indicates the availability of the serial hardware transmit register.</span></span> <span data-ttu-id="d8c44-171">Viene creato con un valore di uno per indicare che il registro di trasmissione è inizialmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="d8c44-171">It is created with a value of one to indicate the transmit register is initially available.</span></span>

<span data-ttu-id="d8c44-172">La funzione di inizializzazione è anche responsabile dell'installazione dei gestori di interrupt vettori di basso livello per le notifiche di input e output.</span><span class="sxs-lookup"><span data-stu-id="d8c44-172">The initialization function is also responsible for installing the low-level interrupt vector handlers for input and output notifications.</span></span> <span data-ttu-id="d8c44-173">Analogamente ad altre routine del servizio di interrupt ThreadX, il gestore di basso livello deve chiamare \***_tx_thread_context_save** _ prima di chiamare il semplice PVR del driver.</span><span class="sxs-lookup"><span data-stu-id="d8c44-173">Like other ThreadX interrupt service routines, the low-level handler must call \***_tx_thread_context_save** _ before calling the simple driver ISR.</span></span> <span data-ttu-id="d8c44-174">Una volta che il driver ISR restituisce, il gestore di basso livello deve chiamare _ \* _ _tx_thread_context_restore_\* \*.</span><span class="sxs-lookup"><span data-stu-id="d8c44-174">After the driver ISR returns, the low-level handler must call _\*_ _tx_thread_context_restore_\*\*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8c44-175">\* È importante che l'inizializzazione venga chiamata prima di qualsiasi altra funzione del driver.</span><span class="sxs-lookup"><span data-stu-id="d8c44-175">\*It is important that initialization is called before any of the other driver functions.</span></span> <span data-ttu-id="d8c44-176">L'inizializzazione del driver viene in genere chiamata da ***tx_application_define***.</span><span class="sxs-lookup"><span data-stu-id="d8c44-176">Typically, driver initialization is called from ***tx_application_define***.</span></span>

```c
VOID tx_sdriver_initialize(VOID)
{
    /* Initialize the two counting semaphores used to control
    the simple driver I/O. */
    tx_semaphore_create(&tx_sdriver_input_semaphore,
                        "simple driver input semaphore", 0);
    tx_semaphore_create(&tx_sdriver_output_semaphore,
                        "simple driver output semaphore", 1);

    /* Setup interrupt vectors for input and output ISRs.
    The initial vector handling should call the ISRs
    defined in this file. */

    /* Configure serial device hardware for RX/TX interrupt
    generation, baud rate, stop bits, etc. */
}
```
<span data-ttu-id="d8c44-177">**FIGURA 9. Inizializzazione driver semplice**</span><span class="sxs-lookup"><span data-stu-id="d8c44-177">**FIGURE 9. Simple Driver Initialization**</span></span>

### <a name="simple-driver-input"></a><span data-ttu-id="d8c44-178">Input di driver semplice</span><span class="sxs-lookup"><span data-stu-id="d8c44-178">Simple Driver Input</span></span>

<span data-ttu-id="d8c44-179">Input per il driver semplice Centra intorno al semaforo di input.</span><span class="sxs-lookup"><span data-stu-id="d8c44-179">Input for the simple driver centers around the input semaphore.</span></span> <span data-ttu-id="d8c44-180">Quando viene ricevuto un interrupt di input seriale del dispositivo, viene impostato il semaforo di input.</span><span class="sxs-lookup"><span data-stu-id="d8c44-180">When a serial device input interrupt is received, the input semaphore is set.</span></span> <span data-ttu-id="d8c44-181">Se uno o più thread sono in attesa di un carattere dal driver, il thread in attesa del più lungo viene ripreso.</span><span class="sxs-lookup"><span data-stu-id="d8c44-181">If one or more threads are waiting for a character from the driver, the thread waiting the longest is resumed.</span></span> <span data-ttu-id="d8c44-182">Se nessun thread è in attesa, il semaforo rimane semplicemente impostato fino a quando un thread non chiama la funzione di input dell'unità.</span><span class="sxs-lookup"><span data-stu-id="d8c44-182">If no threads are waiting, the semaphore simply remains set until a thread calls the drive input function.</span></span>

<span data-ttu-id="d8c44-183">Esistono diverse limitazioni alla gestione semplice dell'input dei driver.</span><span class="sxs-lookup"><span data-stu-id="d8c44-183">There are several limitations to the simple driver input handling.</span></span> <span data-ttu-id="d8c44-184">Il più significativo è il potenziale per eliminare i caratteri di input.</span><span class="sxs-lookup"><span data-stu-id="d8c44-184">The most significant is the potential for dropping input characters.</span></span> <span data-ttu-id="d8c44-185">Questa operazione è possibile perché non esiste la possibilità di memorizzare nel buffer i caratteri di input che arrivano prima che il carattere precedente venga elaborato.</span><span class="sxs-lookup"><span data-stu-id="d8c44-185">This is possible because there is no ability to buffer input characters that arrive before the previous character is processed.</span></span> <span data-ttu-id="d8c44-186">Questa operazione viene gestita facilmente mediante l'aggiunta di un buffer di caratteri di input.</span><span class="sxs-lookup"><span data-stu-id="d8c44-186">This is easily handled by adding an input character buffer.</span></span>

> [!NOTE]
> <span data-ttu-id="d8c44-187">*Solo i thread sono autorizzati a chiamare il*  \* **tx_sdriver_input** _ _function. \*</span><span class="sxs-lookup"><span data-stu-id="d8c44-187">*Only threads are allowed to call the* ***tx_sdriver_input** _ _function.*</span></span>

<span data-ttu-id="d8c44-188">Nella figura 10 è illustrato il codice sorgente associato all'input di un driver semplice.</span><span class="sxs-lookup"><span data-stu-id="d8c44-188">Figure 10 shows the source code associated with simple driver input.</span></span>

```c
UCHAR tx_sdriver_input(VOID)
{
  /* Determine if there is a character waiting. If not,
  suspend. */
  tx_semaphore_get(&tx_sdriver_input_semaphore,
  TX_WAIT_FOREVER;

  /* Return character from serial RX hardware register. */
  return(*serial_hardware_input_ptr);
}
  VOID tx_sdriver_input_ISR(VOID)
{
  /* See if an input character notification is pending. */
  if (!tx_sdriver_input_semaphore.tx_semaphore_count)
  {
    /* If not, notify thread of an input character. */
    tx_semaphore_put(&tx_sdriver_input_semaphore);
  }
}
```
<span data-ttu-id="d8c44-189">**FIGURA 10. Input di driver semplice**</span><span class="sxs-lookup"><span data-stu-id="d8c44-189">**FIGURE 10. Simple Driver Input**</span></span>

### <a name="simple-driver-output"></a><span data-ttu-id="d8c44-190">Output di driver semplice</span><span class="sxs-lookup"><span data-stu-id="d8c44-190">Simple Driver Output</span></span>

<span data-ttu-id="d8c44-191">L'elaborazione dell'output usa il semaforo di output per segnalare quando il registro di trasmissione del dispositivo seriale è gratuito.</span><span class="sxs-lookup"><span data-stu-id="d8c44-191">Output processing utilizes the output semaphore to signal when the serial device's transmit register is free.</span></span> <span data-ttu-id="d8c44-192">Prima che un carattere di output venga effettivamente scritto nel dispositivo, viene ottenuto il semaforo di output.</span><span class="sxs-lookup"><span data-stu-id="d8c44-192">Before an output character is actually written to the device, the output semaphore is obtained.</span></span> <span data-ttu-id="d8c44-193">Se non è disponibile, la trasmissione precedente non è ancora completa.</span><span class="sxs-lookup"><span data-stu-id="d8c44-193">If it is not available, the previous transmit is not yet complete.</span></span>

<span data-ttu-id="d8c44-194">L'ISR di output è responsabile della gestione dell'interrupt completo di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-194">The output ISR is responsible for handling the transmit complete interrupt.</span></span> <span data-ttu-id="d8c44-195">L'elaborazione dell'output ISR equivale a impostare il semaforo di output, consentendo in questo modo l'output di un altro carattere.</span><span class="sxs-lookup"><span data-stu-id="d8c44-195">Processing of the output ISR amounts to setting the output semaphore, thereby allowing output of another character.</span></span>

> [!NOTE]
> <span data-ttu-id="d8c44-196">*Solo i thread sono autorizzati a chiamare il*  \* **tx_sdriver_output** _ _function. \*</span><span class="sxs-lookup"><span data-stu-id="d8c44-196">*Only threads are allowed to call the* ***tx_sdriver_output** _ _function.*</span></span>

<span data-ttu-id="d8c44-197">Nella figura 11 viene illustrato il codice sorgente associato all'output di un driver semplice.</span><span class="sxs-lookup"><span data-stu-id="d8c44-197">Figure 11 shows the source code associated with simple driver output.</span></span>

```c
VOID tx_sdriver_output(UCHAR alpha)
{
  /* Determine if the hardware is ready to transmit a
  character. If not, suspend until the previous output
  completes. */
  tx_semaphore_get(&tx_sdriver_output_semaphore,
                                          TX_WAIT_FOREVER);

  /* Send the character through the hardware. */
  *serial_hardware_output_ptr = alpha;
}
  
VOID tx_sdriver_output_ISR(VOID)
{
  /* Notify thread last character transmit is
  complete. */
  tx_semaphore_put(&tx_sdriver_output_semaphore);
}
```
<span data-ttu-id="d8c44-198">**FIGURA 11. Output di driver semplice**</span><span class="sxs-lookup"><span data-stu-id="d8c44-198">**FIGURE 11. Simple Driver Output**</span></span>

### <a name="simple-driver-shortcomings"></a><span data-ttu-id="d8c44-199">Limitazioni semplici per i driver</span><span class="sxs-lookup"><span data-stu-id="d8c44-199">Simple Driver Shortcomings</span></span>

<span data-ttu-id="d8c44-200">Questo semplice esempio di driver di dispositivo illustra l'idea di base di un driver di dispositivo ThreadX.</span><span class="sxs-lookup"><span data-stu-id="d8c44-200">This simple device driver example illustrates the basic idea of a ThreadX device driver.</span></span> <span data-ttu-id="d8c44-201">Tuttavia, poiché il driver di dispositivo semplice non risolve il buffer dei dati o problemi di overhead, non rappresenta completamente i driver ThreadX reali.</span><span class="sxs-lookup"><span data-stu-id="d8c44-201">However, because the simple device driver does not address data buffering or any overhead issues, it does not fully represent real-world ThreadX drivers.</span></span> <span data-ttu-id="d8c44-202">Nella sezione seguente vengono descritti alcuni dei problemi più avanzati associati ai driver di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-202">The following section describes some of the more advanced issues associated with device drivers.</span></span>

## <a name="advanced-driver-issues"></a><span data-ttu-id="d8c44-203">Problemi relativi ai driver avanzati</span><span class="sxs-lookup"><span data-stu-id="d8c44-203">Advanced Driver Issues</span></span>

<span data-ttu-id="d8c44-204">Come indicato in precedenza, i driver di dispositivo presentano requisiti univoci come le rispettive applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d8c44-204">As mentioned previously, device drivers have requirements as unique as their applications.</span></span> <span data-ttu-id="d8c44-205">Alcune applicazioni possono richiedere una grande quantità di buffer di dati, mentre un'altra applicazione potrebbe richiedere un driver ottimizzato ISRs a causa di interrupt del dispositivo ad alta frequenza.</span><span class="sxs-lookup"><span data-stu-id="d8c44-205">Some applications may require an enormous amount of data buffering while another application may require optimized driver ISRs because of high-frequency device interrupts.</span></span>

### <a name="io-buffering"></a><span data-ttu-id="d8c44-206">Buffer I/O</span><span class="sxs-lookup"><span data-stu-id="d8c44-206">I/O Buffering</span></span>

<span data-ttu-id="d8c44-207">Il buffering dei dati nelle applicazioni embedded in tempo reale richiede una pianificazione considerevole.</span><span class="sxs-lookup"><span data-stu-id="d8c44-207">Data buffering in real-time embedded applications requires considerable planning.</span></span> <span data-ttu-id="d8c44-208">Parte della progettazione è determinata dal dispositivo hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="d8c44-208">Some of the design is dictated by the underlying hardware device.</span></span> <span data-ttu-id="d8c44-209">Se il dispositivo fornisce l'I/O di base per i byte, probabilmente si tratta di un semplice buffer circolare.</span><span class="sxs-lookup"><span data-stu-id="d8c44-209">If the device provides basic byte I/O, a simple circular buffer is probably in order.</span></span> <span data-ttu-id="d8c44-210">Tuttavia, se il dispositivo fornisce l'I/O a blocchi, DMA o pacchetti, è probabile che venga garantito uno schema di gestione del buffer.</span><span class="sxs-lookup"><span data-stu-id="d8c44-210">However, if the device provides block, DMA, or packet I/O, a buffer management scheme is probably warranted.</span></span>

### <a name="circular-byte-buffers"></a><span data-ttu-id="d8c44-211">Buffer di byte circolari</span><span class="sxs-lookup"><span data-stu-id="d8c44-211">Circular Byte Buffers</span></span>

<span data-ttu-id="d8c44-212">I buffer di byte circolari vengono in genere usati nei driver che gestiscono un semplice dispositivo hardware seriale come UART.</span><span class="sxs-lookup"><span data-stu-id="d8c44-212">Circular byte buffers are typically used in drivers that manage a simple serial hardware device like a UART.</span></span> <span data-ttu-id="d8c44-213">Due buffer circolari vengono spesso utilizzati in situazioni di questo tipo: uno per l'input e uno per l'output.</span><span class="sxs-lookup"><span data-stu-id="d8c44-213">Two circular buffers are most often used in such situations—one for input and one for output.</span></span>

<span data-ttu-id="d8c44-214">Ogni buffer di byte circolari è costituito da un'area di memoria byte (in genere una matrice di **UCHAR**), un puntatore di lettura e un puntatore di scrittura.</span><span class="sxs-lookup"><span data-stu-id="d8c44-214">Each circular byte buffer is comprised of a byte memory area (typically an array of **UCHAR** s), a read pointer, and a write pointer.</span></span> <span data-ttu-id="d8c44-215">Un buffer viene considerato vuoto quando il puntatore di lettura e i puntatori di scrittura fanno riferimento alla stessa posizione di memoria nel buffer.</span><span class="sxs-lookup"><span data-stu-id="d8c44-215">A buffer is considered empty when the read pointer and the write pointers reference the same memory location in the buffer.</span></span> <span data-ttu-id="d8c44-216">L'inizializzazione del driver imposta i puntatori del buffer di lettura e scrittura sull'indirizzo iniziale del buffer.</span><span class="sxs-lookup"><span data-stu-id="d8c44-216">Driver initialization sets both the read and write buffer pointers to the beginning address of the buffer.</span></span>

### <a name="circular-buffer-input"></a><span data-ttu-id="d8c44-217">Input del buffer circolare</span><span class="sxs-lookup"><span data-stu-id="d8c44-217">Circular Buffer Input</span></span>

<span data-ttu-id="d8c44-218">Il buffer di input viene usato per mantenere i caratteri che arrivano prima che l'applicazione sia pronta.</span><span class="sxs-lookup"><span data-stu-id="d8c44-218">The input buffer is used to hold characters that arrive before the application is ready for them.</span></span> <span data-ttu-id="d8c44-219">Quando viene ricevuto un carattere di input (in genere in una routine del servizio di interrupt), il nuovo carattere viene recuperato dal dispositivo hardware e inserito nel buffer di input nella posizione a cui punta il puntatore di scrittura.</span><span class="sxs-lookup"><span data-stu-id="d8c44-219">When an input character is received (usually in an interrupt service routine), the new character is retrieved from the hardware device and placed into the input buffer at the location pointed to by the write pointer.</span></span> <span data-ttu-id="d8c44-220">Il puntatore di scrittura viene quindi spostato nella posizione successiva nel buffer.</span><span class="sxs-lookup"><span data-stu-id="d8c44-220">The write pointer is then advanced to the next position in the buffer.</span></span> <span data-ttu-id="d8c44-221">Se la posizione successiva si trova oltre la fine del buffer, il puntatore di scrittura viene impostato sull'inizio del buffer.</span><span class="sxs-lookup"><span data-stu-id="d8c44-221">If the next position is past the end of the buffer, the write pointer is set to the beginning of the buffer.</span></span> <span data-ttu-id="d8c44-222">La condizione della coda completa viene gestita annullando l'avanzamento del puntatore di scrittura se il nuovo puntatore di scrittura è uguale al puntatore di lettura.</span><span class="sxs-lookup"><span data-stu-id="d8c44-222">The queue full condition is handled by canceling the write pointer advancement if the new write pointer is the same as the read pointer.</span></span>

<span data-ttu-id="d8c44-223">Le richieste di byte di input dell'applicazione al driver esaminano prima di tutto i puntatori di lettura e scrittura del buffer di input.</span><span class="sxs-lookup"><span data-stu-id="d8c44-223">Application input byte requests to the driver first examine the read and write pointers of the input buffer.</span></span> <span data-ttu-id="d8c44-224">Se i puntatori di lettura e scrittura sono identici, il buffer è vuoto.</span><span class="sxs-lookup"><span data-stu-id="d8c44-224">If the read and write pointers are identical, the buffer is empty.</span></span> <span data-ttu-id="d8c44-225">In caso contrario, se il puntatore di lettura non è lo stesso, il byte a cui punta il puntatore di lettura viene copiato dal buffer di input e il puntatore di lettura viene spostato nella posizione del buffer successiva.</span><span class="sxs-lookup"><span data-stu-id="d8c44-225">Otherwise, if the read pointer is not the same, the byte pointed to by the read pointer is copied from the input buffer and the read pointer is advanced to the next buffer location.</span></span> <span data-ttu-id="d8c44-226">Se il nuovo puntatore di lettura si trova oltre la fine del buffer, viene reimpostato all'inizio.</span><span class="sxs-lookup"><span data-stu-id="d8c44-226">If the new read pointer is past the end of the buffer, it is reset to the beginning.</span></span> <span data-ttu-id="d8c44-227">Nella figura 12 viene illustrata la logica per il buffer di input circolare.</span><span class="sxs-lookup"><span data-stu-id="d8c44-227">Figure 12 shows the logic for the circular input buffer.</span></span>

```c
UCHAR   tx_input_buffer[MAX_SIZE];
UCHAR   tx_input_write_ptr;
UCHAR   tx_input_read_ptr;

/* Initialization. */
tx_input_write_ptr =    &tx_input_buffer[0];
tx_input_read_ptr =     &tx_input_buffer[0];

/* Input byte ISR... UCHAR alpha has character from device. */
save_ptr = tx_input_write_ptr;
*tx_input_write_ptr++ = alpha;
if (tx_input_write_ptr > &tx_input_buffer[MAX_SIZE-1])
    tx_input_write_ptr = &tx_input_buffer[0]; /* Wrap */
if (tx_input_write_ptr == tx_input_read_ptr)
    tx_input_write_ptr = save_ptr; /* Buffer full */

/* Retrieve input byte from buffer... */
if (tx_input_read_ptr != tx_input_write_ptr)
{
  alpha = *tx_input_read_ptr++;
  if (tx_input_read_ptr > &tx_input_buffer[MAX_SIZE-1])
      tx_input_read_ptr = &tx_input_buffer[0];
}
```
<span data-ttu-id="d8c44-228">**FIGURA 12. Logica per il buffer di input circolare**</span><span class="sxs-lookup"><span data-stu-id="d8c44-228">**FIGURE 12. Logic for Circular Input Buffer**</span></span>

> [!NOTE]
> <span data-ttu-id="d8c44-229">\* Per un'operazione affidabile, potrebbe essere necessario bloccare gli interrupt quando si modificano i puntatori di lettura e scrittura dei buffer circolari di input e di output.</span><span class="sxs-lookup"><span data-stu-id="d8c44-229">\*For reliable operation, it may be necessary to lockout interrupts when manipulating the read and write pointers of both the input and output circular buffers.</span></span> *

### <a name="circular-output-buffer"></a><span data-ttu-id="d8c44-230">Buffer di output circolare</span><span class="sxs-lookup"><span data-stu-id="d8c44-230">Circular Output Buffer</span></span>

<span data-ttu-id="d8c44-231">Il buffer di output viene usato per contenere i caratteri che sono arrivati per l'output prima che il dispositivo hardware abbia terminato di inviare il byte precedente.</span><span class="sxs-lookup"><span data-stu-id="d8c44-231">The output buffer is used to hold characters that have arrived for output before the hardware device finished sending the previous byte.</span></span> <span data-ttu-id="d8c44-232">L'elaborazione del buffer di output è simile all'elaborazione del buffer di input, ad eccezione del fatto che l'elaborazione di interrupt completa di trasmissione manipola il puntatore di lettura dell'output, mentre la richiesta di output dell'applicazione utilizza il puntatore di scrittura di</span><span class="sxs-lookup"><span data-stu-id="d8c44-232">Output buffer processing is similar to input buffer processing, except the transmit complete interrupt processing manipulates the output read pointer, while the application output request utilizes the output write pointer.</span></span>
<span data-ttu-id="d8c44-233">In caso contrario, l'elaborazione del buffer di output è la stessa.</span><span class="sxs-lookup"><span data-stu-id="d8c44-233">Otherwise, the output buffer processing is the same.</span></span> <span data-ttu-id="d8c44-234">Nella figura 13 viene illustrata la logica per il buffer di output circolare.</span><span class="sxs-lookup"><span data-stu-id="d8c44-234">Figure 13 shows the logic for the circular output buffer.</span></span>

```c
UCHAR   tx_output_buffer[MAX_SIZE];
UCHAR   tx_output_write_ptr;
UCHAR   tx_output_read_ptr;

/* Initialization. */
tx_output_write_ptr = &tx_output_buffer[0];
tx_output_read_ptr = &tx_output_buffer[0];

/* Transmit complete ISR... Device ready to send. */
if (tx_output_read_ptr != tx_output_write_ptr)
{
  *device_reg = *tx_output_read_ptr++;
  if (tx_output_read_reg > &tx_output_buffer[MAX_SIZE-1])
      tx_output_read_ptr = &tx_output_buffer[0];
}

/* Output byte driver service. If device busy, buffer! */
save_ptr = tx_output_write_ptr;
*tx_output_write_ptr++ = alpha;
if (tx_output_write_ptr > &tx_output_buffer[MAX_SIZE-1])
    tx_output_write_ptr = &tx_output_buffer[0]; /* Wrap */
if (tx_output_write_ptr == tx_output_read_ptr)
    tx_output_write_ptr = save_ptr; /* Buffer full! */
```
<span data-ttu-id="d8c44-235">**FIGURA 13. Logica per il buffer di output circolare**</span><span class="sxs-lookup"><span data-stu-id="d8c44-235">**FIGURE 13. Logic for Circular Output Buffer**</span></span>

### <a name="buffer-io-management"></a><span data-ttu-id="d8c44-236">Gestione I/O del buffer</span><span class="sxs-lookup"><span data-stu-id="d8c44-236">Buffer I/O Management</span></span>

<span data-ttu-id="d8c44-237">Per migliorare le prestazioni dei microprocessori incorporati, molti dispositivi dispositivo periferico trasmettono e ricevono dati con i buffer forniti dal software.</span><span class="sxs-lookup"><span data-stu-id="d8c44-237">To improve the performance of embedded microprocessors, many peripheral device devices transmit and receive data with buffers supplied by software.</span></span> <span data-ttu-id="d8c44-238">In alcune implementazioni, è possibile usare più buffer per trasmettere o ricevere singoli pacchetti di dati.</span><span class="sxs-lookup"><span data-stu-id="d8c44-238">In some implementations, multiple buffers may be used to transmit or receive individual packets of data.</span></span>

<span data-ttu-id="d8c44-239">Le dimensioni e la posizione dei buffer di I/O sono determinate dall'applicazione e/o dal software del driver.</span><span class="sxs-lookup"><span data-stu-id="d8c44-239">The size and location of I/O buffers is determined by the application and/or driver software.</span></span> <span data-ttu-id="d8c44-240">In genere, i buffer sono di dimensioni fisse e gestiti all'interno di un pool di memoria del blocco ThreadX.</span><span class="sxs-lookup"><span data-stu-id="d8c44-240">Typically, buffers are fixed in size and managed within a ThreadX block memory pool.</span></span> <span data-ttu-id="d8c44-241">La figura 14 descrive un buffer di I/O tipico e un pool di memoria blocco ThreadX che gestisce l'allocazione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-241">Figure 14 describes a typical I/O buffer and a ThreadX block memory pool that manages their allocation.</span></span>

```c
typedef struct TX_IO_BUFFER_STRUCT
{
      struct TX_IO_BUFFER_STRUCT *tx_next_packet;
      struct TX_IO_BUFFER_STRUCT *tx_next_buffer;
      UCHAR tx_buffer_area[TX_MAX_BUFFER_SIZE];
} TX_IO_BUFFER;

TX_BLOCK_POOL tx_io_block_pool;

/* Create a pool of I/O buffers. Assume that the pointer
"free_memory_ptr"points to an available memory area that
is 64 KBytes in size. */
tx_block_pool_create(&tx_io_block_pool,
                  "Sample IO Driver Buffer Pool",
                  free_memory_ptr, 0x10000,
                  sizeof(TX_IO_BUFFER));
```

<span data-ttu-id="d8c44-242">**FIGURA 14. Buffer I/O**</span><span class="sxs-lookup"><span data-stu-id="d8c44-242">**FIGURE 14. I/O Buffer**</span></span>

### <a name="tx_io_buffer"></a><span data-ttu-id="d8c44-243">TX_IO_BUFFER</span><span class="sxs-lookup"><span data-stu-id="d8c44-243">TX_IO_BUFFER</span></span>

<span data-ttu-id="d8c44-244">Il typedef TX_IO_BUFFER è costituito da due puntatori.</span><span class="sxs-lookup"><span data-stu-id="d8c44-244">The typedef TX_IO_BUFFER consists of two pointers.</span></span> <span data-ttu-id="d8c44-245">Il puntatore **tx_next_packet** viene usato per collegare più pacchetti nell'elenco di input o output.</span><span class="sxs-lookup"><span data-stu-id="d8c44-245">The **tx_next_packet** pointer is used to link multiple packets on either the input or output list.</span></span> <span data-ttu-id="d8c44-246">Il puntatore **tx_next_buffer** viene usato per collegare i buffer che costituiscono un singolo pacchetto di dati dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-246">The **tx_next_buffer** pointer is used to link together buffers that make up an individual packet of data from the device.</span></span> <span data-ttu-id="d8c44-247">Entrambi i puntatori vengono impostati su NULL quando il buffer viene allocato dal pool.</span><span class="sxs-lookup"><span data-stu-id="d8c44-247">Both of these pointers are set to NULL when the buffer is allocated from the pool.</span></span> <span data-ttu-id="d8c44-248">Inoltre, alcuni dispositivi potrebbero richiedere un altro campo per indicare la quantità di dati effettivamente contenuti nell'area del buffer.</span><span class="sxs-lookup"><span data-stu-id="d8c44-248">In addition, some devices may require another field to indicate how much of the buffer area actually contains data.</span></span>

### <a name="buffered-io-advantage"></a><span data-ttu-id="d8c44-249">Vantaggio I/O memorizzato nel buffer</span><span class="sxs-lookup"><span data-stu-id="d8c44-249">Buffered I/O Advantage</span></span>

<span data-ttu-id="d8c44-250">Quali sono i vantaggi di uno schema di I/O del buffer?</span><span class="sxs-lookup"><span data-stu-id="d8c44-250">What are the advantages of a buffer I/O scheme?</span></span> <span data-ttu-id="d8c44-251">Il vantaggio principale è che i dati non vengono copiati tra i registri dei dispositivi e la memoria dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-251">The biggest advantage is that data is not copied between the device registers and the application's memory.</span></span> <span data-ttu-id="d8c44-252">Al contrario, il driver fornisce al dispositivo una serie di puntatori del buffer.</span><span class="sxs-lookup"><span data-stu-id="d8c44-252">Instead, the driver provides the device with a series of buffer pointers.</span></span> <span data-ttu-id="d8c44-253">L'I/O del dispositivo fisico utilizza direttamente la memoria buffer fornita.</span><span class="sxs-lookup"><span data-stu-id="d8c44-253">Physical device I/O utilizes the supplied buffer memory directly.</span></span>

<span data-ttu-id="d8c44-254">L'utilizzo del processore per copiare pacchetti di dati di input o di output è estremamente costoso e deve essere evitato in qualsiasi situazione di I/O a velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="d8c44-254">Using the processor to copy input or output packets of information is extremely costly and should be avoided in any high throughput I/O situation.</span></span>

<span data-ttu-id="d8c44-255">Un altro vantaggio dell'approccio i/O memorizzato nel buffer consiste nel fatto che gli elenchi di input e output non dispongono di condizioni complete.</span><span class="sxs-lookup"><span data-stu-id="d8c44-255">Another advantage to the buffered I/O approach is that the input and output lists do not have full conditions.</span></span> <span data-ttu-id="d8c44-256">Tutti i buffer disponibili possono trovarsi in uno dei due elenchi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="d8c44-256">All of the available buffers can be on either list at any one time.</span></span> <span data-ttu-id="d8c44-257">Questo è un contrasto con i semplici buffer circolari di byte presentati in precedenza nel capitolo.</span><span class="sxs-lookup"><span data-stu-id="d8c44-257">This contrasts with the simple byte circular buffers presented earlier in the chapter.</span></span> <span data-ttu-id="d8c44-258">Ognuna aveva una dimensione fissa determinata in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="d8c44-258">Each had a fixed size determined at compilation.</span></span>

### <a name="buffered-driver-responsibilities"></a><span data-ttu-id="d8c44-259">Responsabilità dei driver memorizzati nel buffer</span><span class="sxs-lookup"><span data-stu-id="d8c44-259">Buffered Driver Responsibilities</span></span>

<span data-ttu-id="d8c44-260">I driver di dispositivo memorizzati nel buffer sono interessati solo alla gestione degli elenchi collegati di buffer di I/O.</span><span class="sxs-lookup"><span data-stu-id="d8c44-260">Buffered device drivers are only concerned with managing linked lists of I/O buffers.</span></span> <span data-ttu-id="d8c44-261">Per i pacchetti ricevuti prima che il software dell'applicazione sia pronto, viene mantenuto un elenco di buffer di input.</span><span class="sxs-lookup"><span data-stu-id="d8c44-261">An input buffer list is maintained for packets that are received before the application software is ready.</span></span> <span data-ttu-id="d8c44-262">Viceversa, un elenco di buffer di output viene mantenuto per i pacchetti inviati più velocemente di quanto possa essere gestito dal dispositivo hardware.</span><span class="sxs-lookup"><span data-stu-id="d8c44-262">Conversely, an output buffer list is maintained for packets being sent faster than the hardware device can handle them.</span></span> <span data-ttu-id="d8c44-263">La figura 15 Mostra semplici elenchi collegati di input e output di pacchetti di dati e i buffer che compongono ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d8c44-263">Figure 15 shows simple input and output linked lists of data packets and the buffer(s) that make up each packet.</span></span>

<span data-ttu-id="d8c44-264">**Elenco di input**</span><span class="sxs-lookup"><span data-stu-id="d8c44-264">**Input List**</span></span>

![Elenco di input](./media/user-guide/input-list.png)

<span data-ttu-id="d8c44-266">**Elenco output**</span><span class="sxs-lookup"><span data-stu-id="d8c44-266">**Output List**</span></span>

![Elenco output](./media/user-guide/output-list.png)

<span data-ttu-id="d8c44-268">**FIGURA 15. Elenchi di Input-Output**</span><span class="sxs-lookup"><span data-stu-id="d8c44-268">**FIGURE 15. Input-Output Lists**</span></span>

<span data-ttu-id="d8c44-269">Interfaccia applicazioni con driver memorizzati nel buffer con gli stessi buffer di I/O.</span><span class="sxs-lookup"><span data-stu-id="d8c44-269">Applications interface with buffered drivers with the same I/O buffers.</span></span> <span data-ttu-id="d8c44-270">Alla trasmissione, il software applicativo fornisce al driver uno o più buffer da trasmettere.</span><span class="sxs-lookup"><span data-stu-id="d8c44-270">On transmit, application software provides the driver with one or more buffers to transmit.</span></span> <span data-ttu-id="d8c44-271">Quando il software dell'applicazione richiede l'input, il driver restituisce i dati di input nei buffer di I/O.</span><span class="sxs-lookup"><span data-stu-id="d8c44-271">When the application software requests input, the driver returns the input data in I/O buffers.</span></span>

> [!NOTE]
> <span data-ttu-id="d8c44-272">*In alcune applicazioni può essere utile creare un'interfaccia di input del driver che richiede all'applicazione di scambiare un buffer libero per un buffer di input dal driver. Questo potrebbe ridurre l'elaborazione dell'allocazione del buffer all'interno del driver.*</span><span class="sxs-lookup"><span data-stu-id="d8c44-272">*In some applications, it may be useful to build a driver input interface that requires the application to exchange a free buffer for an input buffer from the driver. This might alleviate some buffer allocation processing inside of the driver.*</span></span>

### <a name="interrupt-management"></a><span data-ttu-id="d8c44-273">Gestione interrupt</span><span class="sxs-lookup"><span data-stu-id="d8c44-273">Interrupt Management</span></span>

<span data-ttu-id="d8c44-274">In alcune applicazioni, la frequenza di interrupt del dispositivo può impedire la scrittura dell'ISR in C o l'interazione con ThreadX a ogni interrupt.</span><span class="sxs-lookup"><span data-stu-id="d8c44-274">In some applications, the device interrupt frequency may prohibit writing the ISR in C or to interact with ThreadX on each interrupt.</span></span> <span data-ttu-id="d8c44-275">Se, ad esempio, si accetta 25US per salvare e ripristinare il contesto interrotto, non è consigliabile eseguire un intero contesto di salvataggio se la frequenza di interrupt è 50us.</span><span class="sxs-lookup"><span data-stu-id="d8c44-275">For example, if it takes 25us to save and restore the interrupted context, it would not be advisable to perform a full context save if the interrupt frequency was 50us.</span></span> <span data-ttu-id="d8c44-276">In questi casi, per gestire la maggior parte degli interrupt del dispositivo viene usato un linguaggio ISR (Small assembly language).</span><span class="sxs-lookup"><span data-stu-id="d8c44-276">In such cases, a small assembly language ISR is used to handle most of the device interrupts.</span></span> <span data-ttu-id="d8c44-277">Questo ISR con overhead ridotto interagisce solo con ThreadX quando è necessario.</span><span class="sxs-lookup"><span data-stu-id="d8c44-277">This low-overhead ISR would only interact with ThreadX when necessary.</span></span>

<span data-ttu-id="d8c44-278">Una discussione simile si trova nella discussione sulla gestione degli interrupt alla fine del capitolo 3.</span><span class="sxs-lookup"><span data-stu-id="d8c44-278">A similar discussion can be found in the interrupt management discussion at the end of Chapter 3.</span></span>

### <a name="thread-suspension"></a><span data-ttu-id="d8c44-279">Sospensione thread</span><span class="sxs-lookup"><span data-stu-id="d8c44-279">Thread Suspension</span></span>

<span data-ttu-id="d8c44-280">Nell'esempio di driver semplice illustrato in precedenza in questo capitolo, il chiamante del servizio di input sospende se un carattere non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d8c44-280">In the simple driver example presented earlier in this chapter, the caller of the input service suspends if a character is not available.</span></span> <span data-ttu-id="d8c44-281">In alcune applicazioni questo potrebbe non essere accettabile.</span><span class="sxs-lookup"><span data-stu-id="d8c44-281">In some applications, this might not be acceptable.</span></span>

<span data-ttu-id="d8c44-282">Se, ad esempio, il thread responsabile dell'elaborazione dell'input da un driver dispone anche di altre mansioni, la sospensione solo sull'input del driver probabilmente non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="d8c44-282">For example, if the thread responsible for processing input from a driver also has other duties, suspending on just the driver input is probably not going to work.</span></span> <span data-ttu-id="d8c44-283">Al contrario, il driver deve essere personalizzato per richiedere l'elaborazione in modo analogo al modo in cui vengono effettuate altre richieste di elaborazione al thread.</span><span class="sxs-lookup"><span data-stu-id="d8c44-283">Instead, the driver needs to be customized to request processing similar to the way other processing requests are made to the thread.</span></span>

<span data-ttu-id="d8c44-284">Nella maggior parte dei casi, il buffer di input viene inserito in un elenco collegato e un messaggio di evento di input viene inviato alla coda di input del thread.</span><span class="sxs-lookup"><span data-stu-id="d8c44-284">In most cases, the input buffer is placed on a linked list and an input event message is sent to the thread's input queue.</span></span>
