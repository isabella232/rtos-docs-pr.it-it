---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo TFTP
description: Il Trivial File Transfer Protocol (TFTP) è un protocollo leggero progettato per i trasferimenti di file.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4431b23e143d05214090547e7f179a6f5def8217
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821614"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-tftp"></a><span data-ttu-id="62467-103">Capitolo 1-Introduzione ad Azure RTO NetX Duo TFTP</span><span class="sxs-lookup"><span data-stu-id="62467-103">Chapter 1 - Introduction to Azure RTOS NetX Duo TFTP</span></span> 

<span data-ttu-id="62467-104">Il Trivial File Transfer Protocol (TFTP) è un protocollo leggero progettato per i trasferimenti di file.</span><span class="sxs-lookup"><span data-stu-id="62467-104">The Trivial File Transfer Protocol (TFTP) is a lightweight protocol designed for file transfers.</span></span> <span data-ttu-id="62467-105">A differenza dei protocolli più affidabili, TFTP non esegue un controllo degli errori esteso e può anche avere prestazioni limitate perché si tratta di un protocollo di arresto e attesa.</span><span class="sxs-lookup"><span data-stu-id="62467-105">Unlike more robust protocols, TFTP does not perform extensive error checking and can also have limited performance because it is a stop-and-wait protocol.</span></span> <span data-ttu-id="62467-106">Dopo l'invio di un pacchetto di dati TFTP, il mittente attende che un ACK venga restituito dal destinatario.</span><span class="sxs-lookup"><span data-stu-id="62467-106">After a TFTP data packet is sent, the sender waits for an ACK to be returned by the recipient.</span></span> <span data-ttu-id="62467-107">Sebbene questo sia semplice, limita la velocità effettiva complessiva di TFTP.</span><span class="sxs-lookup"><span data-stu-id="62467-107">Although this is simple, it does limit the overall TFTP throughput.</span></span> <span data-ttu-id="62467-108">Il pacchetto TFTP consente agli host di usare il protocollo TFTP su reti IP.</span><span class="sxs-lookup"><span data-stu-id="62467-108">The TFTP package enables hosts to use the TFTP protocol over IP networks.</span></span>

## <a name="tftp-requirements"></a><span data-ttu-id="62467-109">Requisiti TFTP</span><span class="sxs-lookup"><span data-stu-id="62467-109">TFTP Requirements</span></span>

<span data-ttu-id="62467-110">Per funzionare correttamente, la parte client TFTP del pacchetto TFTP NetX Duo richiede che sia già stata creata un'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="62467-110">In order to function properly, the TFTP Clients portion of the NetX Duo TFTP package requires that an IP instance has already been created.</span></span> <span data-ttu-id="62467-111">Inoltre, è necessario abilitare UDP nella stessa istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="62467-111">In addition, UDP must be enabled on that same IP instance.</span></span> <span data-ttu-id="62467-112">La parte client del pacchetto TFTP NetX Duo non ha altri requisiti.</span><span class="sxs-lookup"><span data-stu-id="62467-112">The Client portion of the NetX Duo TFTP package has no further requirements.</span></span>

<span data-ttu-id="62467-113">La parte relativa al server TFTP del pacchetto TFTP NetX Duo presenta diversi requisiti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="62467-113">The TFTP Server portion of the NetX Duo TFTP package has several additional requirements.</span></span> <span data-ttu-id="62467-114">Per prima cosa, è necessario l'accesso completo alla *porta UDP ben nota 69* per la gestione di tutte le richieste TFTP del client.</span><span class="sxs-lookup"><span data-stu-id="62467-114">First, it requires complete access to the UDP *well known port 69* for handling all client TFTP requests.</span></span> <span data-ttu-id="62467-115">Il server TFTP è anche progettato per l'uso con FileX Embedded file system.</span><span class="sxs-lookup"><span data-stu-id="62467-115">The TFTP Server is also designed for use with the FileX embedded file system.</span></span> <span data-ttu-id="62467-116">Se FileX non è disponibile, l'utente può trasferire le parti di FileX utilizzate nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="62467-116">If FileX is not available, the user may port the portions of FileX used to their own environment.</span></span> <span data-ttu-id="62467-117">Questo argomento viene descritto nelle sezioni successive di questa guida.</span><span class="sxs-lookup"><span data-stu-id="62467-117">This is discussed in later sections of this guide.</span></span>

## <a name="tftp-file-names"></a><span data-ttu-id="62467-118">Nomi file TFTP</span><span class="sxs-lookup"><span data-stu-id="62467-118">TFTP File Names</span></span> 

<span data-ttu-id="62467-119">I nomi di file TFTP devono essere nel formato del file system di destinazione.</span><span class="sxs-lookup"><span data-stu-id="62467-119">TFTP file names should be in the format of the target file system.</span></span> <span data-ttu-id="62467-120">Devono essere stringhe ASCII con terminazione NULL, con informazioni complete sul percorso, se necessario.</span><span class="sxs-lookup"><span data-stu-id="62467-120">They should be NULL terminated ASCII strings, with full path information if necessary.</span></span> <span data-ttu-id="62467-121">Non esiste alcun limite specificato nelle dimensioni dei nomi file TFTP nell'implementazione TFTP NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="62467-121">There is no specified limit in the size of TFTP file names in the NetX Duo TFTP implementation.</span></span>

## <a name="tftp-messages"></a><span data-ttu-id="62467-122">Messaggi TFTP</span><span class="sxs-lookup"><span data-stu-id="62467-122">TFTP Messages</span></span>

<span data-ttu-id="62467-123">TFTP dispone di un meccanismo molto semplice per l'apertura, la lettura, la scrittura e la chiusura di file.</span><span class="sxs-lookup"><span data-stu-id="62467-123">The TFTP has a very simple mechanism for opening, reading, writing, and closing files.</span></span> <span data-ttu-id="62467-124">Sono sostanzialmente presenti 2-4 byte di intestazione TFTP sotto l'intestazione UDP.</span><span class="sxs-lookup"><span data-stu-id="62467-124">There are basically 2-4 bytes of TFTP header underneath the UDP header.</span></span> <span data-ttu-id="62467-125">La definizione del file TFTP i messaggi aperti presenta il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="62467-125">The definition of the TFTP file open messages has the following format:</span></span>

<span data-ttu-id="62467-126">**oooof... f0OCTET0**</span><span class="sxs-lookup"><span data-stu-id="62467-126">**oooof…f0OCTET0**</span></span>

<span data-ttu-id="62467-127">Dove:</span><span class="sxs-lookup"><span data-stu-id="62467-127">Where:</span></span>

- <span data-ttu-id="62467-128">campo opcode a 2 byte **oooo**</span><span class="sxs-lookup"><span data-stu-id="62467-128">**oooo** 2-byte Opcode field</span></span>  
<span data-ttu-id="62467-129">0x0001-> aperto per la lettura</span><span class="sxs-lookup"><span data-stu-id="62467-129">0x0001 -> Open for read</span></span>  
<span data-ttu-id="62467-130">0x0002-> aperto per la scrittura</span><span class="sxs-lookup"><span data-stu-id="62467-130">0x0002 -> Open for write</span></span>

- <span data-ttu-id="62467-131">**f...** campo del nome file f n-byte</span><span class="sxs-lookup"><span data-stu-id="62467-131">**f…f** n-byte Filename field</span></span>

- <span data-ttu-id="62467-132">carattere di terminazione NULL a 0 1 byte</span><span class="sxs-lookup"><span data-stu-id="62467-132">0  1-byte NULL termination character</span></span>

- <span data-ttu-id="62467-133">**Ottetto** "Ottetto" ASCII per specificare il trasferimento binario</span><span class="sxs-lookup"><span data-stu-id="62467-133">**OCTET** ASCII “OCTET” to specify binary transfer</span></span>

- <span data-ttu-id="62467-134">carattere di terminazione NULL a 0 1 byte</span><span class="sxs-lookup"><span data-stu-id="62467-134">0  1-byte NULL termination character</span></span>

<span data-ttu-id="62467-135">La definizione dei messaggi TFTP Write, ACK e Error è leggermente diversa e viene definita nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="62467-135">The definition of the TFTP write, ACK, and error messages are slightly different and are defined as follows:</span></span>

<span data-ttu-id="62467-136">**oooobbbbd... d**</span><span class="sxs-lookup"><span data-stu-id="62467-136">**oooobbbbd…d**</span></span>

<span data-ttu-id="62467-137">Dove:</span><span class="sxs-lookup"><span data-stu-id="62467-137">Where:</span></span>

- <span data-ttu-id="62467-138">campo opcode a 2 byte **oooo**</span><span class="sxs-lookup"><span data-stu-id="62467-138">**oooo** 2-byte Opcode field</span></span>  
<span data-ttu-id="62467-139">0x0003-pacchetto di dati ></span><span class="sxs-lookup"><span data-stu-id="62467-139">0x0003 -> Data packet</span></span>  
<span data-ttu-id="62467-140">0x0004-ACK > per l'ultima lettura</span><span class="sxs-lookup"><span data-stu-id="62467-140">0x0004 -> ACK for last read</span></span>  
<span data-ttu-id="62467-141">0x0005-condizione di errore ></span><span class="sxs-lookup"><span data-stu-id="62467-141">0x0005 -> Error condition</span></span>  

- <span data-ttu-id="62467-142">**bbbb** 2-campo numero blocco byte (1-n)</span><span class="sxs-lookup"><span data-stu-id="62467-142">**bbbb** 2-byte Block Number field (1-n)</span></span>

- <span data-ttu-id="62467-143">**d...** campo dati d n byte</span><span class="sxs-lookup"><span data-stu-id="62467-143">**d…d** n-byte Data field</span></span>


- <span data-ttu-id="62467-144">0x0001 (lettura) nome file 0 ottetto 0</span><span class="sxs-lookup"><span data-stu-id="62467-144">0x0001 (read) File Name 0 OCTET 0</span></span>

- <span data-ttu-id="62467-145">0x0002 (Write) nome file 0 ottetto 0</span><span class="sxs-lookup"><span data-stu-id="62467-145">0x0002 (write) File Name 0 OCTET 0</span></span>

## <a name="tftp-communication"></a><span data-ttu-id="62467-146">Comunicazione TFTP</span><span class="sxs-lookup"><span data-stu-id="62467-146">TFTP Communication</span></span>

<span data-ttu-id="62467-147">I server TFTP utilizzano la porta UDP 69 nota per ascoltare le richieste dei client.</span><span class="sxs-lookup"><span data-stu-id="62467-147">TFTP Servers utilize the well-known UDP port 69 to listen for Client requests.</span></span> <span data-ttu-id="62467-148">I socket client TFTP possono essere associati a qualsiasi porta UDP disponibile.</span><span class="sxs-lookup"><span data-stu-id="62467-148">TFTP Client sockets may bind to any available UDP port.</span></span> <span data-ttu-id="62467-149">Il payload del pacchetto di dati che contiene il file da caricare o scaricare viene inviato in blocchi di 512 byte, fino all'ultimo pacchetto che contiene < 512 byte.</span><span class="sxs-lookup"><span data-stu-id="62467-149">Data packet payload containing the file to upload or download is sent in 512 byte chunks, until the last packet containing < 512 bytes.</span></span> <span data-ttu-id="62467-150">Pertanto, un pacchetto contenente meno di 512 byte segnala la fine del file.</span><span class="sxs-lookup"><span data-stu-id="62467-150">Therefore a packet containing fewer than 512 bytes signals the end of file.</span></span> <span data-ttu-id="62467-151">La sequenza generale degli eventi è la seguente:</span><span class="sxs-lookup"><span data-stu-id="62467-151">The general sequence of events is as follows:</span></span>

<span data-ttu-id="62467-152">Richieste di file di lettura TFTP:</span><span class="sxs-lookup"><span data-stu-id="62467-152">TFTP Read File Requests:</span></span>

1.  <span data-ttu-id="62467-153">Il client invia una richiesta di apertura per la lettura con il nome del file e attende una risposta dal server.</span><span class="sxs-lookup"><span data-stu-id="62467-153">The Client issues an “Open For Read” request with the file name and waits for a reply from the Server.</span></span>

2.  <span data-ttu-id="62467-154">Il server invia i primi 512 byte del file o meno se le dimensioni del file sono inferiori a 512 byte.</span><span class="sxs-lookup"><span data-stu-id="62467-154">The Server sends the first 512 bytes of the file or less if the file size is less than 512 bytes.</span></span>

3.  <span data-ttu-id="62467-155">Il client riceve i dati, invia un ACK e attende il pacchetto successivo dal server per i file che contengono più di 512 byte.</span><span class="sxs-lookup"><span data-stu-id="62467-155">The Client receives data, sends an ACK, and waits for the next packet from the Server for files containing more than 512 bytes.</span></span>

4.  <span data-ttu-id="62467-156">La sequenza termina quando il client riceve un pacchetto contenente meno di 512 byte.</span><span class="sxs-lookup"><span data-stu-id="62467-156">The sequence ends when the Client receives a packet containing fewer than 512 bytes.</span></span>

<span data-ttu-id="62467-157">Richieste di scrittura TFTP:</span><span class="sxs-lookup"><span data-stu-id="62467-157">TFTP Write Requests:</span></span>

1.  <span data-ttu-id="62467-158">Il client invia una richiesta di "apertura per la scrittura" con il nome del file e attende un ACK con un numero di blocco pari a 0 dal server.</span><span class="sxs-lookup"><span data-stu-id="62467-158">The Client issues an “Open for Write” request with the file name and waits for an ACK with a block number of 0 from the Server.</span></span>

2.  <span data-ttu-id="62467-159">Quando il server è pronto per la scrittura del file, invia un ACK con un numero di blocco pari a zero.</span><span class="sxs-lookup"><span data-stu-id="62467-159">When the Server is ready to write the file, it sends an ACK with a block number of zero.</span></span>

3.  <span data-ttu-id="62467-160">Il client invia al server i primi 512 byte del file (o meno per i file con una quantità inferiore a 512 byte) e attende la restituzione di un ACK.</span><span class="sxs-lookup"><span data-stu-id="62467-160">The Client sends the first 512 bytes of the file (or less for files less than 512 bytes) to the Server and waits for an ACK back.</span></span>

4.  <span data-ttu-id="62467-161">Il server invia un ACK dopo la scrittura dei byte.</span><span class="sxs-lookup"><span data-stu-id="62467-161">The Server sends an ACK after the bytes are written.</span></span>

5.  <span data-ttu-id="62467-162">La sequenza termina quando il client completa la scrittura di un pacchetto contenente meno di 512 byte.</span><span class="sxs-lookup"><span data-stu-id="62467-162">The sequence ends when the Client completes writing a packet containing fewer than 512 bytes.</span></span>
 

## <a name="tftp-server-session-timer"></a><span data-ttu-id="62467-163">Timer sessione server TFTP</span><span class="sxs-lookup"><span data-stu-id="62467-163">TFTP Server Session Timer</span></span>

<span data-ttu-id="62467-164">Il server TFTP ha un numero limitato di slot di richiesta client.</span><span class="sxs-lookup"><span data-stu-id="62467-164">The TFTP Server has a limited number of client request slots.</span></span> <span data-ttu-id="62467-165">Se una sessione client sembra essere eliminata, lo slot non può essere disponibile per il riutilizzo.</span><span class="sxs-lookup"><span data-stu-id="62467-165">If a client session appears to be dropped, that slot cannot be available for re-use.</span></span> <span data-ttu-id="62467-166">Tuttavia, se l'opzione NX_TFTP_SERVER_RETRANSMIT_ENABLE è abilitata, il server TFTP NetX duo crea un timer di sessione che monitora il timeout in ogni sessione client.</span><span class="sxs-lookup"><span data-stu-id="62467-166">However if the NX_TFTP_SERVER_RETRANSMIT_ENABLE option is enabled, the NetX Duo TFTP Server creates an session timer that monitors the timeout on each of its client sessions.</span></span> <span data-ttu-id="62467-167">Quando il timeout di una sessione scade, viene terminato e tutti i file aperti vengono chiusi.</span><span class="sxs-lookup"><span data-stu-id="62467-167">When a session timeout expires it is terminated and any open files are closed.</span></span> <span data-ttu-id="62467-168">Quindi, lo slot diventa disponibile per un'altra richiesta client TFTP.</span><span class="sxs-lookup"><span data-stu-id="62467-168">Thus the ‘slot’ becomes available for another TFTP Client request.</span></span>

<span data-ttu-id="62467-169">Per impostare il timeout, modificare l'opzione di configurazione NX_TFTP_SERVER_RETRANSMIT_TIMEOUT che, per impostazione predefinita, è 200 cicli del timer.</span><span class="sxs-lookup"><span data-stu-id="62467-169">To set the timeout, adjust the configuration option NX_TFTP_SERVER_RETRANSMIT_TIMEOUT which by default is 200 timer ticks.</span></span> <span data-ttu-id="62467-170">Per impostazione predefinita, l'intervallo tra i timeout di sessione controllati viene impostato dal NX_TFTP_SERVER_TIMEOUT_PERIOD, ovvero 20 cicli del timer.</span><span class="sxs-lookup"><span data-stu-id="62467-170">The interval between which session timeouts are checked is set by the NX_TFTP_SERVER_TIMEOUT_PERIOD which is 20 timer ticks by default.</span></span>

<span data-ttu-id="62467-171">Quando il client TFTP ha caricato i file (scritti) nel supporto TFTP FileX, è necessario scaricare il supporto in modo che i dati possano essere scritti dal disco RAM del server TFTP nei supporti sottostanti (memoria disco del client TFTP).</span><span class="sxs-lookup"><span data-stu-id="62467-171">When the TFTP Client has uploaded (written) files to the TFTP FileX media, the media needs to be flushed so that data can be written from the TFTP server ram disk to the underlying media (TFTP Client disk memory).</span></span> <span data-ttu-id="62467-172">Questa operazione può essere eseguita utilizzando il servizio fx_media_flush se l'applicazione non desidera chiudere il server TFTP.</span><span class="sxs-lookup"><span data-stu-id="62467-172">This can be done using the fx_media_flush service if the application does not wish to close the TFTP Server.</span></span>

<span data-ttu-id="62467-173">Tuttavia, dopo aver chiuso il server TFTP, l'applicazione dovrebbe, se non è più usata per il supporto FileX, quindi chiudere i supporti usando il servizio fx_media_close.</span><span class="sxs-lookup"><span data-stu-id="62467-173">However, after closing the TFTP server, the application should, if it has no further use for the FileX media, then close the media using the fx_media_close service.</span></span> <span data-ttu-id="62467-174">In questo modo i dati dei file vengono scaricati nel disco del client TFTP, vengono chiusi i file aperti e aggiornati le informazioni della directory nel supporto.</span><span class="sxs-lookup"><span data-stu-id="62467-174">This will flush the file data back to the TFTP Client disk, close open files, and update the directory information to the media.</span></span>

<span data-ttu-id="62467-175">La sezione "piccolo esempio" di questo capitolo illustra questa operazione.</span><span class="sxs-lookup"><span data-stu-id="62467-175">The “Small Example” section in this chapter demonstrates this.</span></span>

<span data-ttu-id="62467-176">Una terza opzione per l'aggiornamento del supporto FileX consiste nel compilare la libreria FileX con le opzioni FX_FAULT_TOLERANT o FX_FAULT_TOLERANT_DATA invece di usare i servizi FileX in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="62467-176">A third option for updating the FileX media is to compile the FileX library with the FX_FAULT_TOLERANT or the FX_FAULT_TOLERANT_DATA options instead of using FileX services explicitly.</span></span> <span data-ttu-id="62467-177">Se definito, FileX passa automaticamente le richieste di scrittura al driver multimediale.</span><span class="sxs-lookup"><span data-stu-id="62467-177">If defined, FileX automatically passes write requests to the media driver.</span></span> <span data-ttu-id="62467-178">Queste opzioni possono limitare le prestazioni, ma offrire una maggiore protezione da dati di file persi o cluster persi.</span><span class="sxs-lookup"><span data-stu-id="62467-178">These options may limit performance but offer greater protection from lost file data or lost clusters.</span></span> <span data-ttu-id="62467-179">Per ulteriori informazioni su questo e FileX in generale, vedere la guida per l'utente di FileX per la logica rapida.</span><span class="sxs-lookup"><span data-stu-id="62467-179">For more information about this and FileX in general, please see the Express Logic FileX User Guide.</span></span>

## <a name="tftp-multi-thread-support"></a><span data-ttu-id="62467-180">Supporto TFTP per più thread</span><span class="sxs-lookup"><span data-stu-id="62467-180">TFTP Multi-Thread Support</span></span>

<span data-ttu-id="62467-181">I servizi client TFTP NetX Duo possono essere chiamati da più thread contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="62467-181">The NetX Duo TFTP Client services can be called from multiple threads simultaneously.</span></span> <span data-ttu-id="62467-182">Tuttavia, le richieste di lettura o scrittura per un'istanza del client TFTP specifica devono essere eseguite in sequenza dallo stesso thread.</span><span class="sxs-lookup"><span data-stu-id="62467-182">However, read or write requests for a particular TFTP Client instance should be done in sequence from the same thread.</span></span>

## <a name="tftp-rfcs"></a><span data-ttu-id="62467-183">RFC TFTP</span><span class="sxs-lookup"><span data-stu-id="62467-183">TFTP RFCs</span></span>

<span data-ttu-id="62467-184">NetX Duo TFTP è conforme a RFC1350 e alle RFC correlate.</span><span class="sxs-lookup"><span data-stu-id="62467-184">NetX Duo TFTP is compliant with RFC1350 and related RFCs.</span></span>

