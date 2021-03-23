---
title: Appendice D-dump e buffer di traccia
description: Il dump del buffer di traccia creato da Azure RTO ThreadX in un file nel computer host viene eseguito tramite i comandi e/o le utilità forniti dallo strumento di sviluppo specifico usato.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 30f6b5e329feeb2dca37dda391fd738aba587c9a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823627"
---
# <a name="appendix-d---dumping-and-trace-buffer"></a><span data-ttu-id="73f43-103">Appendice D-dump e buffer di traccia</span><span class="sxs-lookup"><span data-stu-id="73f43-103">Appendix D - Dumping and trace buffer</span></span>

<span data-ttu-id="73f43-104">Il dump del buffer di traccia creato da Azure RTO ThreadX in un file nel computer host viene eseguito tramite i comandi e/o le utilità forniti dallo strumento di sviluppo specifico usato.</span><span class="sxs-lookup"><span data-stu-id="73f43-104">Dumping the trace buffer created by Azure RTOS ThreadX to a file on the host computer is done via commands and/or utilities provided by the specific development tool being used.</span></span> <span data-ttu-id="73f43-105">Questa appendice contiene esempi di dump di un buffer di traccia in un file host in alcuni degli strumenti di sviluppo più diffusi usati con ThreadX.</span><span class="sxs-lookup"><span data-stu-id="73f43-105">This appendix contains examples of dumping a trace buffer to a host file in some of the more popular development tools used with ThreadX.</span></span> 

## <a name="benchx-tools"></a><span data-ttu-id="73f43-106">Strumenti BenchX</span><span class="sxs-lookup"><span data-stu-id="73f43-106">BenchX Tools</span></span>

<span data-ttu-id="73f43-107">È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti BenchX selezionando il pulsante ***Archivia memoria nel file** _ nella _visualizzazione di memoria_* \*, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="73f43-107">The trace buffer can be dumped to a host file easily with the BenchX tools by selecting the ***Store Memory To File** _ button within the _*_Memory View_\*\*, as shown below:</span></span>

![Screenshot della visualizzazione della memoria negli strumenti BenchX.](./media/user-guide/image642.jpg)

<span data-ttu-id="73f43-109">A questo punto, specificare l'indirizzo del buffer di traccia, le dimensioni, il nome del file di destinazione (incluso il percorso), quindi selezionare il pulsante ***Salva*** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="73f43-109">At this point, specify the trace buffer address, size, destination file name (including path), and select the ***Save*** button as shown below.</span></span> <span data-ttu-id="73f43-110">Verrà creato il file di traccia binario per la visualizzazione in TraceX.</span><span class="sxs-lookup"><span data-stu-id="73f43-110">This will create the binary trace file for viewing within TraceX.</span></span>

![Screenshot della finestra di dialogo Salva strumenti BenchX.](./media/user-guide/image643.jpg)

## <a name="realview-tools"></a><span data-ttu-id="73f43-112">Strumenti RealView</span><span class="sxs-lookup"><span data-stu-id="73f43-112">RealView Tools</span></span>

<span data-ttu-id="73f43-113">È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti ARM RealView immettendo il comando seguente al prompt della riga di comando in RealView:</span><span class="sxs-lookup"><span data-stu-id="73f43-113">The trace buffer can be dumped to a host file easily with the ARM RealView tools by entering the following command at the command-line prompt in RealView:</span></span>

```c 
> WRITEFILE,raw trace_file.trx=0x6860..0xE560
```

<span data-ttu-id="73f43-114">Al termine, il file ***trace_file. TRX*** conterrà il buffer di traccia che si trova a partire dall'indirizzo 0x6860 e passa all'indirizzo 0xE560.</span><span class="sxs-lookup"><span data-stu-id="73f43-114">Upon completion, the file ***trace_file.trx*** will contain the trace buffer that is located starting at the address 0x6860 and goes up to address 0xE560.</span></span> <span data-ttu-id="73f43-115">Questo file è pronto per la visualizzazione da TraceX.</span><span class="sxs-lookup"><span data-stu-id="73f43-115">This file is ready for viewing by TraceX.</span></span>

## <a name="iar-tools"></a><span data-ttu-id="73f43-116">Strumenti IAR</span><span class="sxs-lookup"><span data-stu-id="73f43-116">IAR Tools</span></span>

<span data-ttu-id="73f43-117">È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti IAR semplicemente facendo clic con il pulsante destro del mouse nella visualizzazione memoria e selezionando la ***memoria Salva...***</span><span class="sxs-lookup"><span data-stu-id="73f43-117">The trace buffer can be dumped to a host file easily with the IAR tools by simply right-clicking in the memory view and selecting the ***Memory Save…***</span></span> <span data-ttu-id="73f43-118">come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="73f43-118">option, as shown below.</span></span>

![Screenshot dell'opzione di salvataggio della memoria negli strumenti IAR.](./media/user-guide/image0_311.jpg)

<span data-ttu-id="73f43-120">Questa operazione comporta la visualizzazione della finestra di dialogo \***Save Memory** _.</span><span class="sxs-lookup"><span data-stu-id="73f43-120">This results in the \***Memory Save** _ dialog to be displayed.</span></span> <span data-ttu-id="73f43-121">Immettere l'indirizzo iniziale e finale e il nome del file di traccia, quindi selezionare il pulsante _*_Salva_*_ .</span><span class="sxs-lookup"><span data-stu-id="73f43-121">Enter the starting and ending address and the trace file name, then select the _*_Save_*_ button.</span></span> <span data-ttu-id="73f43-122">Nell'esempio riportato di seguito, gli strumenti IAR salvano il buffer di traccia specificato in record ESADECIMALi Intel nel file _ *_trace_file. Hex_* \*.</span><span class="sxs-lookup"><span data-stu-id="73f43-122">In the example shown below, the IAR tools save the specified trace buffer into Intel HEX records in the file _\*_trace_file.hex_\*\*.</span></span>

![Screenshot della finestra di dialogo di salvataggio della memoria per gli strumenti IAR.](./media/user-guide/image648.jpg)

<span data-ttu-id="73f43-124">A questo punto, il buffer di traccia è stato salvato nel file ***trace_file. Hex*** nell'host ed è pronto per la visualizzazione con TraceX.</span><span class="sxs-lookup"><span data-stu-id="73f43-124">At this point, we have the trace buffer saved in the ***trace_file.hex*** file on the host and is ready for viewing with TraceX.</span></span>

## <a name="codewarrior-tools"></a><span data-ttu-id="73f43-125">Strumenti di CodeWarrior</span><span class="sxs-lookup"><span data-stu-id="73f43-125">CodeWarrior Tools</span></span>

<span data-ttu-id="73f43-126">È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti di CodeWarrior immettendo il comando \***Save** _ nella finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="73f43-126">The trace buffer can be dumped to a host file easily with the CodeWarrior tools by entering the \***save** _ command in the Command Window.</span></span> <span data-ttu-id="73f43-127">Il comando di esempio _ *_Save_*\* seguente presuppone che il buffer di traccia inizi in corrispondenza di 0x102200 e termina in corrispondenza di 0x109F00:</span><span class="sxs-lookup"><span data-stu-id="73f43-127">The following example _ *_save_*\* command assumes the trace buffer starts at 0x102200 and ends at 0x109F00:</span></span>

```c
> save –b p:0x102200..0x109F00 trace_file.trx -a 32bit
```

<span data-ttu-id="73f43-128">Ciò comporta il salvataggio del buffer di traccia nel file ***trace_file. TRX*** nell'host.</span><span class="sxs-lookup"><span data-stu-id="73f43-128">This results in the trace buffer being saved in the file ***trace_file.trx*** on the host.</span></span>

## <a name="mplab-tools"></a><span data-ttu-id="73f43-129">Strumenti MPLAB</span><span class="sxs-lookup"><span data-stu-id="73f43-129">MPLAB Tools</span></span>

<span data-ttu-id="73f43-130">MPLAB è in grado di creare un file di traccia compatibile con TraceX tramite l'utilità di esportazione tabella, che consente l'esportazione di qualsiasi intervallo di memoria in un file host.</span><span class="sxs-lookup"><span data-stu-id="73f43-130">MPLAB can create a TraceX-compatible trace file through its Export Table utility, which allows the export of any range of memory to a host file.</span></span> <span data-ttu-id="73f43-131">Per utilizzare questa utilità per creare un file di traccia per TraceX, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="73f43-131">To use this utility to create a trace file for TraceX, proceed as follows:</span></span>

<span data-ttu-id="73f43-132">**Passaggio 1** Aprire una finestra memoria selezionando Visualizza-> memoria.</span><span class="sxs-lookup"><span data-stu-id="73f43-132">**Step 1** Open a memory window by selecting View -> Memory.</span></span>

![Screenshot della memoria selezionata dal menu Visualizza.](./media/user-guide/image0_316.jpg)

<span data-ttu-id="73f43-134">**Passaggio 2** Fare clic con il pulsante destro del mouse nella **visualizzazione memoria** per visualizzare un elenco di opzioni.</span><span class="sxs-lookup"><span data-stu-id="73f43-134">**Step 2** Right-click within the **Memory View** to display a list of options.</span></span> <span data-ttu-id="73f43-135">Specificare il **formato di visualizzazione-1 byte** per selezionare la visualizzazione di byte.</span><span class="sxs-lookup"><span data-stu-id="73f43-135">Specify **Display Format -1 Byte** to select byte display..</span></span>

![Screenshot della visualizzazione memoria con l'opzione formato di visualizzazione selezionata.](./media/user-guide/image650.png)

![Screenshot della finestra di dialogo Vai a.](./media/user-guide/image651.jpg)

<span data-ttu-id="73f43-138">**Passaggio 3** Fare di nuovo clic con il pulsante destro del mouse nella finestra **visualizzazione memoria** e scegliere **Vai a**. verrà visualizzata una finestra di dialogo in cui è possibile specificare l'indirizzo del buffer dell'evento.</span><span class="sxs-lookup"><span data-stu-id="73f43-138">**Step 3** Right-click again within the **Memory View** Window and select **Go To**, which opens a dialog box that enables you to specify the address of the event buffer.</span></span> <span data-ttu-id="73f43-139">Questo esempio Mostra **_event_buffer_** visualizzato.</span><span class="sxs-lookup"><span data-stu-id="73f43-139">This example shows **_event_buffer_** being displayed.</span></span>

![Screenshot della visualizzazione memoria con l'opzione Vai a selezionata.](./media/user-guide/image0_312.jpg)

![Screenshot di un esempio che mostra il event_buffer visualizzato.](./media/user-guide/image653.png)

<span data-ttu-id="73f43-142">**Passaggio 4** In questo modo viene evidenziato il contenuto della prima posizione del buffer di traccia, che è sempre la stringa BTXT....</span><span class="sxs-lookup"><span data-stu-id="73f43-142">**Step 4** This highlights the contents of the first location of the trace buffer, which is always the string BTXT….</span></span>

![Screenshot della prima posizione del buffer di traccia.](./media/user-guide/image0_313.jpg)

<span data-ttu-id="73f43-144">**Passaggio 5** A questo punto, fare di nuovo clic con il pulsante destro del mouse per visualizzare il menu opzioni e selezionare **Esporta tabella**.</span><span class="sxs-lookup"><span data-stu-id="73f43-144">**Step 5** Now, right-click again to bring up the options menu, and select **Export Table**.</span></span>

![Screenshot della visualizzazione memoria con l'opzione Esporta tabella selezionata.](./media/user-guide/image0_314.jpg)

<span data-ttu-id="73f43-146">**Passaggio 6** Verrà visualizzata la finestra di dialogo **Esporta tabella** , come illustrato.</span><span class="sxs-lookup"><span data-stu-id="73f43-146">**Step 6** This brings up the **Export Table** dialog, as shown.</span></span> <span data-ttu-id="73f43-147">Consente di specificare l'intervallo di indirizzi da esportare.</span><span class="sxs-lookup"><span data-stu-id="73f43-147">Specify the range of addresses to export.</span></span> <span data-ttu-id="73f43-148">Per un buffer di traccia da 8 KB, come nel caso di questo esempio, specificare l'intervallo da 0xA00006AC a 0xA00026AC e immettere un nome per il file host da creare (demo_threadx. TRX in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="73f43-148">For an 8K trace buffer, as is the case in this example, specify the range 0xA00006AC to 0xA00026AC, and enter a name for the host file to be created (demo_threadx.trx in this example).</span></span>

<span data-ttu-id="73f43-149">! [[Screenshot della finestra di dialogo Esporta come.](./media/user-guide/image656.jpg)</span><span class="sxs-lookup"><span data-stu-id="73f43-149">![[Screenshot of the Export As dialog.](./media/user-guide/image656.jpg)</span></span>

<span data-ttu-id="73f43-150">**Passaggio 7** Viene creato un file denominato **demo_threadx. TRX** nell'host e questo file può essere aperto da TraceX.</span><span class="sxs-lookup"><span data-stu-id="73f43-150">**Step 7** A file named **demo_threadx.trx** will be created on the host, and this file can be opened by TraceX.</span></span>

## <a name="ghs-tools"></a><span data-ttu-id="73f43-151">Strumenti GHS</span><span class="sxs-lookup"><span data-stu-id="73f43-151">GHS Tools</span></span>

<span data-ttu-id="73f43-152">È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti GHS immettendo il comando seguente al prompt della riga di comando nella finestra di comando debug:</span><span class="sxs-lookup"><span data-stu-id="73f43-152">The trace buffer can be dumped to a host file easily with the GHS tools by entering the following command at the command-line prompt in the debug command window:</span></span>

```c
memdump raw c:releasethreadxdemo_threadx.trx event_buffer 32768
```

<span data-ttu-id="73f43-153">Al termine, il file **demo_threadx. TRX** conterrà il buffer di traccia che si trova nel event_buffer con una dimensione di 32.768 byte ed è pronto per la visualizzazione da parte di TraceX.</span><span class="sxs-lookup"><span data-stu-id="73f43-153">Upon completion, the file **demo_threadx.trx** will contain the trace buffer that is located in the event_buffer with a size of 32,768 bytes and is ready for viewing by TraceX.</span></span>

## <a name="renesas-hew"></a><span data-ttu-id="73f43-154">Renesas</span><span class="sxs-lookup"><span data-stu-id="73f43-154">Renesas HEW</span></span>

<span data-ttu-id="73f43-155">È possibile eseguire facilmente il dump del buffer di traccia in un file host con gli strumenti di reimpostazione della NASA, seguendo i tre passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="73f43-155">The trace buffer can be dumped to a host file easily with the Renasas HEW tools by following the three steps (and substeps) below:</span></span>

<span data-ttu-id="73f43-156">**Passaggio 1** Aprire la finestra memoria.</span><span class="sxs-lookup"><span data-stu-id="73f43-156">**Step 1** Open Memory Window.</span></span>

<span data-ttu-id="73f43-157">! [[Screenshot della finestra memoria.](./media/user-guide/image657.jpg)</span><span class="sxs-lookup"><span data-stu-id="73f43-157">![[Screenshot of the Memory Window.](./media/user-guide/image657.jpg)</span></span>

<span data-ttu-id="73f43-158">**Passaggio 2** Posizionare il cursore nella finestra memoria e fare clic con il pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="73f43-158">**Step 2** Place cursor within memory window and right click.</span></span>

![Screenshot della finestra memoria con l'opzione Salva selezionata.](./media/user-guide/image0_315.jpg)

<span data-ttu-id="73f43-160">**Passaggio 3** Selezionare Salva, quindi nella finestra Salva memoria come eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="73f43-160">**Step 3** Select Save, then in the Save Memory As window do the following:</span></span>

- <span data-ttu-id="73f43-161">Selezionare formato file: Binary.</span><span class="sxs-lookup"><span data-stu-id="73f43-161">Select File format: Binary.</span></span>
- <span data-ttu-id="73f43-162">Specificare filename: come desiderato</span><span class="sxs-lookup"><span data-stu-id="73f43-162">Specify Filename: As Desired</span></span>
- <span data-ttu-id="73f43-163">Specificare l'indirizzo iniziale: trace_buffer</span><span class="sxs-lookup"><span data-stu-id="73f43-163">Specify Start address: trace_buffer</span></span>
- <span data-ttu-id="73f43-164">Specifica indirizzo finale: (trace_buffer + dimensioni)</span><span class="sxs-lookup"><span data-stu-id="73f43-164">Specify End address: (trace_buffer+size)</span></span>
- <span data-ttu-id="73f43-165">Specificare le dimensioni di accesso: 1</span><span class="sxs-lookup"><span data-stu-id="73f43-165">Specify Access size: 1</span></span>
- <span data-ttu-id="73f43-166">Fare clic su Salva.</span><span class="sxs-lookup"><span data-stu-id="73f43-166">Click Save</span></span>

![Screenshot della finestra di dialogo Salva memoria con nome.](./media/user-guide/image659.jpg)