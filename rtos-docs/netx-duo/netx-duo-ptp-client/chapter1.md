---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo PTP client
description: Questo capitolo contiene un'introduzione al client PTP di Azure RTO NetX Duo.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5beec64bd6d74e3bed06be15255d6bd4a940ba64
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821710"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-ptp-client"></a><span data-ttu-id="2104b-103">Capitolo 1-Introduzione ad Azure RTO NetX Duo PTP client</span><span class="sxs-lookup"><span data-stu-id="2104b-103">Chapter 1 - Introduction to Azure RTOS NetX Duo PTP Client</span></span>

<span data-ttu-id="2104b-104">Azure RTO NetX Duo PTP implementa la parte client della versione 2, IEEE 1588-2008 del protocollo PTP (Precision Time Protocol).</span><span class="sxs-lookup"><span data-stu-id="2104b-104">The Azure RTOS NetX Duo PTP implements the client part of the Precision Time Protocol (PTP) version 2, IEEE 1588-2008.</span></span> <span data-ttu-id="2104b-105">Viene usato per sincronizzare gli orologi tra MCU nella rete locale comunicando tra loro tramite pacchetti multicast IPv4 o IPv6.</span><span class="sxs-lookup"><span data-stu-id="2104b-105">It is used to synchronize clocks among MCUs on the local network by communicating each other via IPv4 or IPv6 multicast packets.</span></span>

## <a name="netx-duo-ptp-client-setup"></a><span data-ttu-id="2104b-106">Installazione del client NetX Duo PTP</span><span class="sxs-lookup"><span data-stu-id="2104b-106">NetX Duo PTP Client Setup</span></span>

<span data-ttu-id="2104b-107">Per funzionare correttamente, il pacchetto client PTP richiede che sia già stata creata un'istanza IP di NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="2104b-107">In order to function properly, the PTP client package requires that a NetX Duo IP instance has already been created.</span></span>

<span data-ttu-id="2104b-108">Per impostazione predefinita, il client PTP si unisce al gruppo multicast IPv4.</span><span class="sxs-lookup"><span data-stu-id="2104b-108">By default, the PTP client joins IPv4 multicast group.</span></span> <span data-ttu-id="2104b-109">Per eseguire il client PTP su una rete IPv6, `NX_ENABLE_IPV6_MULTICAST` è necessario definire quando si compila la libreria NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="2104b-109">In order to run the PTP client on an IPv6 network, `NX_ENABLE_IPV6_MULTICAST` must be defined when building NetX Duo library.</span></span>

<span data-ttu-id="2104b-110">Quando si crea il client PTP, l'applicazione deve fornire una funzione di callback per gestire i timestamp dei pacchetti in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="2104b-110">When creating the PTP client, the application must provide a callback function to handle timestamps of incoming and outgoing packets.</span></span> <span data-ttu-id="2104b-111">Per ottenere una risoluzione elevata, è consigliabile che le applicazioni generino timestamp usando un timer ad alta risoluzione.</span><span class="sxs-lookup"><span data-stu-id="2104b-111">To achieve high resolution, we recommend applications to generate timestamps using a high resolution timer.</span></span> <span data-ttu-id="2104b-112">Per eseguire il PTP sul simulatore, viene fornita un'implementazione basata su software `nx_ptp_client_soft_clock_callback` .</span><span class="sxs-lookup"><span data-stu-id="2104b-112">To run the PTP on simulator, a software-based implementation `nx_ptp_client_soft_clock_callback` is provided.</span></span>

<span data-ttu-id="2104b-113">Il client PTP richiede un pool di pacchetti per la trasmissione di messaggi PTP.</span><span class="sxs-lookup"><span data-stu-id="2104b-113">The PTP client requires a packet pool for transmitting PTP messages.</span></span> <span data-ttu-id="2104b-114">Le dimensioni del payload del pool di pacchetti non devono essere minori di `NX_UDP_PACKET + NX_PTP_CLIENT_PACKET_DATA_SIZE` , ovvero 108 byte per IPv4 e 128 byte se IPv6 è abilitato.</span><span class="sxs-lookup"><span data-stu-id="2104b-114">The payload size of packet pool must be no less than `NX_UDP_PACKET + NX_PTP_CLIENT_PACKET_DATA_SIZE`, which is 108 bytes for IPv4, and 128 bytes if IPv6 is enabled.</span></span>

<span data-ttu-id="2104b-115">Dopo aver creato il client PTP, l'applicazione può avviare il client PTP.</span><span class="sxs-lookup"><span data-stu-id="2104b-115">After creating the PTP Client, the application can start the PTP client.</span></span> <span data-ttu-id="2104b-116">La sincronizzazione viene eseguita nel thread Helper PTP.</span><span class="sxs-lookup"><span data-stu-id="2104b-116">The synchronization is done in the PTP helper thread.</span></span> <span data-ttu-id="2104b-117">È possibile specificare una funzione di callback degli eventi.</span><span class="sxs-lookup"><span data-stu-id="2104b-117">An event callback function can be specified.</span></span> <span data-ttu-id="2104b-118">Verrà richiamato quando si verifica uno degli eventi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2104b-118">It will be invoked when any one of the following events happen.</span></span>
* <span data-ttu-id="2104b-119">Un Master è selezionato;</span><span class="sxs-lookup"><span data-stu-id="2104b-119">A master is selected;</span></span> 
* <span data-ttu-id="2104b-120">L'ora viene calibrata.</span><span class="sxs-lookup"><span data-stu-id="2104b-120">The time is calibrated.</span></span>
* <span data-ttu-id="2104b-121">Timeout del master.</span><span class="sxs-lookup"><span data-stu-id="2104b-121">A master times out.</span></span>

## <a name="netx-duo-ptp-client-messages"></a><span data-ttu-id="2104b-122">Messaggi client PTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="2104b-122">NetX Duo PTP Client Messages</span></span>

<span data-ttu-id="2104b-123">Il client PTP NetX Duo implementa solo il meccanismo di richiesta-risposta ritardata.</span><span class="sxs-lookup"><span data-stu-id="2104b-123">The NetX Duo PTP client implements the delay request-response mechanism only.</span></span> <span data-ttu-id="2104b-124">Il client PTP apre due porte UDP.</span><span class="sxs-lookup"><span data-stu-id="2104b-124">The PTP client  opens two UDP ports.</span></span> <span data-ttu-id="2104b-125">*319* per il messaggio di **evento** e *320* per il messaggio **generale** .</span><span class="sxs-lookup"><span data-stu-id="2104b-125">*319* for **event** message and *320* for **general** message.</span></span> <span data-ttu-id="2104b-126">Per questo meccanismo sono disponibili cinque tipi di messaggio.</span><span class="sxs-lookup"><span data-stu-id="2104b-126">There are five types of message for this mechanism.</span></span>

* <span data-ttu-id="2104b-127">**Annunciare**.</span><span class="sxs-lookup"><span data-stu-id="2104b-127">**Announce**.</span></span> <span data-ttu-id="2104b-128">Si tratta di un messaggio di evento.</span><span class="sxs-lookup"><span data-stu-id="2104b-128">This is an event message.</span></span> <span data-ttu-id="2104b-129">Viene usato per la selezione del clock principale.</span><span class="sxs-lookup"><span data-stu-id="2104b-129">It is used for master clock selection.</span></span>
* <span data-ttu-id="2104b-130">**Sincronizzazione**. Si tratta di un messaggio di evento.</span><span class="sxs-lookup"><span data-stu-id="2104b-130">**Sync**. This is an event message.</span></span> <span data-ttu-id="2104b-131">Viene usato per inviare il timestamp di origine e calcolare il ritardo del percorso da master a client.</span><span class="sxs-lookup"><span data-stu-id="2104b-131">It is used to send origin timestamp and calculate the path delay from master to client.</span></span>
* <span data-ttu-id="2104b-132">**Follow_Up**.</span><span class="sxs-lookup"><span data-stu-id="2104b-132">**Follow_Up**.</span></span> <span data-ttu-id="2104b-133">Si tratta di un messaggio generale.</span><span class="sxs-lookup"><span data-stu-id="2104b-133">This is a general message.</span></span> <span data-ttu-id="2104b-134">È facoltativo e viene usato per correggere il timestamp di origine nel messaggio di sincronizzazione correlato.</span><span class="sxs-lookup"><span data-stu-id="2104b-134">It is optional and used to correct the origin timestamp in related Sync message.</span></span> <span data-ttu-id="2104b-135">Viene inviato solo quando viene impostato il bit a due fasi nel flag di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="2104b-135">It is sent only when the two step bit in Sync flag is set.</span></span>
* <span data-ttu-id="2104b-136">**Delay_Req**.</span><span class="sxs-lookup"><span data-stu-id="2104b-136">**Delay_Req**.</span></span> <span data-ttu-id="2104b-137">Si tratta di un messaggio di evento.</span><span class="sxs-lookup"><span data-stu-id="2104b-137">This is an event message.</span></span> <span data-ttu-id="2104b-138">Viene inviato dal client PTP per calcolare il ritardo del percorso da client a master, alla ricezione Delay_Resp.</span><span class="sxs-lookup"><span data-stu-id="2104b-138">It is sent from PTP client to calculate the path delay from client to master, on receiving Delay_Resp.</span></span>
* <span data-ttu-id="2104b-139">**Delay_Resp**.</span><span class="sxs-lookup"><span data-stu-id="2104b-139">**Delay_Resp**.</span></span> <span data-ttu-id="2104b-140">Si tratta di un messaggio di evento.</span><span class="sxs-lookup"><span data-stu-id="2104b-140">This is an event message.</span></span> <span data-ttu-id="2104b-141">Viene inviato da master a client per calcolare il ritardo del percorso dal client al database master.</span><span class="sxs-lookup"><span data-stu-id="2104b-141">It is sent from master to client to calculate the path delay from client to master.</span></span>

<span data-ttu-id="2104b-142">*Si noti che l'algoritmo "Best master clock" non è implementato. Solo il primo clock master viene accettato quando il client PTP è in stato di ascolto.*</span><span class="sxs-lookup"><span data-stu-id="2104b-142">*Note, "best master clock" algorithm is not implemented. Only the first master clock is accepted when the PTP client is in listening state.*</span></span>

## <a name="netx-duo-ptp-client-clock-callback"></a><span data-ttu-id="2104b-143">Callback Clock client PTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="2104b-143">NetX Duo PTP Client Clock Callback</span></span>
<span data-ttu-id="2104b-144">Per sincronizzare clock dal master, il client PTP necessita di un orologio locale.</span><span class="sxs-lookup"><span data-stu-id="2104b-144">To synchronize clock from master, PTP client needs a local clock.</span></span> <span data-ttu-id="2104b-145">Una funzione di callback clock viene passata nel client PTP durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="2104b-145">A clock callback function is passed into PTP client during creation.</span></span> <span data-ttu-id="2104b-146">Il formato della routine di callback dell'orologio è definito di seguito.</span><span class="sxs-lookup"><span data-stu-id="2104b-146">The format of the clock callback routine is  defined below.</span></span>
```C
UINT ptp_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```
<span data-ttu-id="2104b-147">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="2104b-147">The input parameters are defined as follows:</span></span>
* <span data-ttu-id="2104b-148">*client_ptr* punta al client PTP.</span><span class="sxs-lookup"><span data-stu-id="2104b-148">*client_ptr* points to PTP client.</span></span>
* <span data-ttu-id="2104b-149">*Operation* specifica l'operazione di callback. i valori validi sono definiti come illustrato nell'elenco seguente.</span><span class="sxs-lookup"><span data-stu-id="2104b-149">*operation* specifies the callback operation, valid values are defined as shown in the list below.</span></span>
  * <span data-ttu-id="2104b-150">**NX_PTP_CLIENT_CLOCK_INIT** Inizializza Clock.</span><span class="sxs-lookup"><span data-stu-id="2104b-150">**NX_PTP_CLIENT_CLOCK_INIT** Initialize clock.</span></span>
  * <span data-ttu-id="2104b-151">**NX_PTP_CLIENT_CLOCK_SET** Imposta il timestamp corrente specificato da `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="2104b-151">**NX_PTP_CLIENT_CLOCK_SET** Set current timestamp specified by `time_ptr`.</span></span>
  * <span data-ttu-id="2104b-152">**NX_PTP_CLIENT_CLOCK_GET** Restituisce il timestamp corrente a `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="2104b-152">**NX_PTP_CLIENT_CLOCK_GET** Return current timestamp to `time_ptr`.</span></span>
  * <span data-ttu-id="2104b-153">**NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Estrarre il timestamp da `packet_ptr` a `time_ptr` .</span><span class="sxs-lookup"><span data-stu-id="2104b-153">**NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Extract timestamp from `packet_ptr` to `time_ptr`.</span></span>
  * <span data-ttu-id="2104b-154">**NX_PTP_CLIENT_CLOCK_ADJUST** Imposta il timestamp corrente inferiore a *1* secondo.</span><span class="sxs-lookup"><span data-stu-id="2104b-154">**NX_PTP_CLIENT_CLOCK_ADJUST** Adjust current timestamp less than *1* second.</span></span>
  * <span data-ttu-id="2104b-155">**NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Contrassegnare il `packet_ptr` che richiede per notificare al client PTP il timestamp al momento della trasmissione.</span><span class="sxs-lookup"><span data-stu-id="2104b-155">**NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Mark the `packet_ptr` which requires to notify PTP client the timestamp when it is transmitted.</span></span>
  * <span data-ttu-id="2104b-156">**NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Aggiornare il timer soft.</span><span class="sxs-lookup"><span data-stu-id="2104b-156">**NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Update soft timer.</span></span> <span data-ttu-id="2104b-157">Può essere ignorato dal clock dell'hardware.</span><span class="sxs-lookup"><span data-stu-id="2104b-157">It can be ignored by hardware clock.</span></span>
* <span data-ttu-id="2104b-158">*time_ptr* punta al timestamp.</span><span class="sxs-lookup"><span data-stu-id="2104b-158">*time_ptr* points to timestamp.</span></span>
* <span data-ttu-id="2104b-159">*packet_ptr* punta al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2104b-159">*packet_ptr* points to packet.</span></span>
* <span data-ttu-id="2104b-160">*callback_data* punta ai dati di callback opachi.</span><span class="sxs-lookup"><span data-stu-id="2104b-160">*callback_data* points to opaque callback data.</span></span>

<span data-ttu-id="2104b-161">Il tipo di dati NX_PTP_TIME viene definito nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="2104b-161">The NX_PTP_TIME data type is defined as follows.</span></span>
```C
typedef struct NX_PTP_TIME_STRUCT
{
    /* The MSB of the number of seconds */
    LONG  second_high;

    /* The LSB of the number of seconds */
    ULONG second_low;

    /* The number of nanoseconds */
    LONG  nanosecond;
} NX_PTP_TIME;
```

## <a name="netx-duo-ptp-client-event-callback"></a><span data-ttu-id="2104b-162">Callback evento client NetX Duo PTP</span><span class="sxs-lookup"><span data-stu-id="2104b-162">NetX Duo PTP Client Event Callback</span></span>
<span data-ttu-id="2104b-163">È possibile configurare la funzione di callback degli eventi per notificare all'applicazione lo stato del client PTP.</span><span class="sxs-lookup"><span data-stu-id="2104b-163">The event callback function can be setup to notify application the state of PTP client.</span></span> <span data-ttu-id="2104b-164">Il formato della routine di callback degli eventi viene definito come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2104b-164">The format of the event callback routine is defined as shown below.</span></span>
```C
UINT event_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT event, 
    VOID *event_data, 
    VOID *callback_data);
```
<span data-ttu-id="2104b-165">I parametri di input sono.</span><span class="sxs-lookup"><span data-stu-id="2104b-165">The input parameters are.</span></span>
* <span data-ttu-id="2104b-166">*client_ptr* punta al client PTP.</span><span class="sxs-lookup"><span data-stu-id="2104b-166">*client_ptr* points to PTP client.</span></span>
* <span data-ttu-id="2104b-167">*evento* specifica l'evento di callback. i valori validi sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="2104b-167">*event* specifies the callback event, valid values are defined as:</span></span>
  * <span data-ttu-id="2104b-168">**NX_PTP_CLIENT_EVENT_MASTER** È stato selezionato un clock master.</span><span class="sxs-lookup"><span data-stu-id="2104b-168">**NX_PTP_CLIENT_EVENT_MASTER** A master clock is selected.</span></span>
  * <span data-ttu-id="2104b-169">**NX_PTP_CLIENT_EVENT_SYNC** Il client PTP è calibrato.</span><span class="sxs-lookup"><span data-stu-id="2104b-169">**NX_PTP_CLIENT_EVENT_SYNC** PTP client is calibrated.</span></span>
  * <span data-ttu-id="2104b-170">**NX_PTP_CLIENT_EVENT_TIMEOUT** Il clock principale è il timeout.</span><span class="sxs-lookup"><span data-stu-id="2104b-170">**NX_PTP_CLIENT_EVENT_TIMEOUT** Master clock is timeout.</span></span>
* <span data-ttu-id="2104b-171">*event_data* specifica i dati correlati all'evento.</span><span class="sxs-lookup"><span data-stu-id="2104b-171">*event_data* specifies the data related to event.</span></span> <span data-ttu-id="2104b-172">Quando l'evento viene **NX_PTP_CLIENT_EVENT_MASTER**, event_data punta all' `NX_PTP_CLIENT_MASTER` istanza di.</span><span class="sxs-lookup"><span data-stu-id="2104b-172">When event is **NX_PTP_CLIENT_EVENT_MASTER**, event_data points to `NX_PTP_CLIENT_MASTER` instance.</span></span> <span data-ttu-id="2104b-173">Quando l'evento viene **NX_PTP_CLIENT_EVENT_SYNC**, i dati dell'evento puntano all' `NX_PTP_CLIENT_SYNC` istanza.</span><span class="sxs-lookup"><span data-stu-id="2104b-173">When event is **NX_PTP_CLIENT_EVENT_SYNC**, event data points to `NX_PTP_CLIENT_SYNC` instance.</span></span>

## <a name="netx-duo-ptp-client-communication"></a><span data-ttu-id="2104b-174">Comunicazione client PTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="2104b-174">NetX Duo PTP Client Communication</span></span>
<span data-ttu-id="2104b-175">Come indicato in precedenza, il client PTP NetX Duo supporta solo il meccanismo di richiesta-risposta di ritardo.</span><span class="sxs-lookup"><span data-stu-id="2104b-175">As mentioned previously, NetX Duo PTP client only supports delay request-response mechanism.</span></span> <span data-ttu-id="2104b-176">Questo meccanismo misura il ritardo del percorso medio tra il client e il clock master come riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2104b-176">This mechanism measures the mean path delay between the client and the master clock as below:</span></span>
1. <span data-ttu-id="2104b-177">Il client riceve il messaggio di *annuncio* dal master e lo seleziona come master migliore.</span><span class="sxs-lookup"><span data-stu-id="2104b-177">Client receives *Announce* message from master and select it as best master.</span></span>
1. <span data-ttu-id="2104b-178">Il client riceve il messaggio di *sincronizzazione* dal database master.</span><span class="sxs-lookup"><span data-stu-id="2104b-178">Client receives *Sync* message from master.</span></span> <span data-ttu-id="2104b-179">Il timestamp *T1* è il timestamp di origine in questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="2104b-179">The timestamp *t1* is the origin timestamp in this message.</span></span> <span data-ttu-id="2104b-180">Il timestamp *T2* viene letto dall'orologio locale quando viene ricevuto questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="2104b-180">The timestamp *t2* is read from local clock when this message is received.</span></span>
1. <span data-ttu-id="2104b-181">Il client riceve *Follow_Up* messaggio dal master.</span><span class="sxs-lookup"><span data-stu-id="2104b-181">Client receives *Follow_Up* message from master.</span></span> <span data-ttu-id="2104b-182">Questo messaggio è facoltativo e valido solo quando è impostato due passaggi nel flag di *sincronizzazione* .</span><span class="sxs-lookup"><span data-stu-id="2104b-182">This message is optional and valid only when two step in *Sync* flag is set.</span></span> <span data-ttu-id="2104b-183">Il timestamp *T1* viene quindi aggiornato al timestamp di origine in questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="2104b-183">Then the timestamp *t1* is updated to the origin timestamp in this message.</span></span>
1. <span data-ttu-id="2104b-184">Il client invia *Delay_Req* messaggio al database master.</span><span class="sxs-lookup"><span data-stu-id="2104b-184">Client sends *Delay_Req* message to master.</span></span> <span data-ttu-id="2104b-185">Il timestamp *T3* viene letto dall'orologio locale quando viene trasmesso il messaggio.</span><span class="sxs-lookup"><span data-stu-id="2104b-185">The timestamp *t3* is read from local clock when the message is transmitted.</span></span>
1. <span data-ttu-id="2104b-186">Il client riceve *Delay_Resp* messaggio dal master.</span><span class="sxs-lookup"><span data-stu-id="2104b-186">Client receives *Delay_Resp* message from master.</span></span> <span data-ttu-id="2104b-187">Il timestamp *T4* è il timestamp di ricezione in questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="2104b-187">The timestamp *t4* is the receive timestamp in this message.</span></span>

<span data-ttu-id="2104b-188">Il ritardo medio del percorso viene calcolato come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2104b-188">The mean path delay is computed as shown below.</span></span>
```C
<meanPathDelay>=[(t2-t1)+(t4-t3)]/2
```
<span data-ttu-id="2104b-189">L'offset dal master viene calcolato come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2104b-189">The offset from master is computed as shown below.</span></span>
```C
<offsetFromMaster>=client_clock-master_clock
                  =(t2-t1)-<meanPathDelay>
```

> [!NOTE]
> <span data-ttu-id="2104b-190">\***CorrectionField** _ viene ignorato durante la calculation._</span><span class="sxs-lookup"><span data-stu-id="2104b-190">\*The \***correctionField** _ is ignored during the calculation._</span></span>