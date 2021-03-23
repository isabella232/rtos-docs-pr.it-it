---
title: Capitolo 2-installazione e uso di Azure RTO TraceX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello strumento di analisi del sistema TraceX di Azure RTO.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 05d7fe3df38c7e8a3480c8ea0d4922a109de9ede
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823477"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-tracex"></a><span data-ttu-id="45659-103">Capitolo 2-installazione e uso di Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="45659-103">Chapter 2 - Installation and use of Azure RTOS TraceX</span></span>

<span data-ttu-id="45659-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello strumento di analisi del sistema TraceX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="45659-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS TraceX system analysis tool.</span></span> 

## <a name="product-distribution"></a><span data-ttu-id="45659-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="45659-105">Product Distribution</span></span>

<span data-ttu-id="45659-106">È possibile ottenere l'app TraceX da [Microsoft App Store](https://microsoft.com/store/apps) eseguendo la ricerca di TraceX o passando direttamente alla [pagina TraceX](https://www.microsoft.com/p/azure-rtos-tracex/9nf1lfd5xxg3?activetab=pivot:overviewtab).</span><span class="sxs-lookup"><span data-stu-id="45659-106">You can obtain the TraceX app from the [Microsoft App Store](https://microsoft.com/store/apps) by searching for TraceX, or by going directly to [the TraceX page](https://www.microsoft.com/p/azure-rtos-tracex/9nf1lfd5xxg3?activetab=pivot:overviewtab).</span></span> <span data-ttu-id="45659-107">Eseguire quindi le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="45659-107">Then do the following.</span></span>

1. <span data-ttu-id="45659-108">Dalla pagina TraceX nell'App Store, fare clic sul pulsante **Get** o **Install** per installare TraceX.</span><span class="sxs-lookup"><span data-stu-id="45659-108">From the TraceX page in the App Store, click the **Get** or **Install** button to install TraceX.</span></span>

1. <span data-ttu-id="45659-109">Nel browser potrebbe essere visualizzato un messaggio che chiede se si desidera aprire il Microsoft Store, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="45659-109">Your browser may display a message asking if you want to open the Microsoft Store, as shown in the figure below.</span></span> <span data-ttu-id="45659-110">In caso contrario, scegliere il pulsante **Apri** .</span><span class="sxs-lookup"><span data-stu-id="45659-110">If it does, choose the **Open** button.</span></span>
<span data-ttu-id="45659-111">![Scegliere Apri per installare TraceX.](../guix/media/guix-studio/open-ms-store.png)</span><span class="sxs-lookup"><span data-stu-id="45659-111">![Choose Open to install TraceX.](../guix/media/guix-studio/open-ms-store.png)</span></span>

1. <span data-ttu-id="45659-112">Al termine dell'installazione, scegliere il pulsante **Avvia** .</span><span class="sxs-lookup"><span data-stu-id="45659-112">When the install finishes, choose the **Launch** button.</span></span> 

## <a name="using-tracex"></a><span data-ttu-id="45659-113">Uso di TraceX</span><span class="sxs-lookup"><span data-stu-id="45659-113">Using TraceX</span></span>

<span data-ttu-id="45659-114">L'uso di TraceX è semplice come l'apertura di un file di traccia all'interno di TraceX.</span><span class="sxs-lookup"><span data-stu-id="45659-114">Using TraceX is as easy as opening a trace file inside TraceX!</span></span> <span data-ttu-id="45659-115">Eseguire TraceX tramite il pulsante \***Start** _.</span><span class="sxs-lookup"><span data-stu-id="45659-115">Run TraceX via the \***Start** _ button.</span></span> <span data-ttu-id="45659-116">A questo punto si osserverà l'interfaccia utente grafica (GUI) di TraceX.</span><span class="sxs-lookup"><span data-stu-id="45659-116">At this point you will observe the TraceX graphic user interface (GUI).</span></span> <span data-ttu-id="45659-117">A questo punto è possibile usare TraceX per visualizzare graficamente un buffer di traccia di destinazione esistente.</span><span class="sxs-lookup"><span data-stu-id="45659-117">You are now ready to use TraceX to graphically view an existing target trace buffer.</span></span> <span data-ttu-id="45659-118">A tale scopo, fare clic su _ *_file-> Apri,_* quindi immettere il file di traccia binario.</span><span class="sxs-lookup"><span data-stu-id="45659-118">This is easily done by clicking _ *_File -> Open,_*\* then entering the binary trace file.</span></span>

>[!IMPORTANT]
><span data-ttu-id="45659-119">*È anche possibile fare doppio clic su qualsiasi file di traccia con estensione **TRX,** che avvierà automaticamente TraceX.*</span><span class="sxs-lookup"><span data-stu-id="45659-119">*You can also double-click on any trace file with an extension of **trx,** which will automatically launch TraceX.*</span></span>

![Screenshot dell'interfaccia utente grafica di TraceX.](./media/user-guide/screen_shot_8.png)

<span data-ttu-id="45659-121">**FIGURA 1**</span><span class="sxs-lookup"><span data-stu-id="45659-121">**FIGURE 1**</span></span>

>[!IMPORTANT]
><span data-ttu-id="45659-122">*Vedere il **capitolo 5** per istruzioni su come generare buffer di traccia nella destinazione usando threadX.*</span><span class="sxs-lookup"><span data-stu-id="45659-122">*Refer to **Chapter 5** for instructions on how to generate trace buffers on the target using ThreadX.*</span></span>

## <a name="tracex-examples"></a><span data-ttu-id="45659-123">Esempi di TraceX</span><span class="sxs-lookup"><span data-stu-id="45659-123">TraceX Examples</span></span>

<span data-ttu-id="45659-124">La prima volta che si esegue l'applicazione TraceX o quando si aggiorna l'applicazione TraceX, verrà richiesto di installare i file di traccia di esempio TraceX e il file custom_events. trxc in una directory definita dall'utente nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="45659-124">The first time you run the TraceX application, or when the TraceX application is updated, you will be prompted to install the TraceX example trace files and the custom_events.trxc file to a user-defined directory on your local machine.</span></span>

<span data-ttu-id="45659-125">Al termine di questo passaggio di installazione, i file di traccia di esempio con estensione **TRX** si trovano nella sottodirectory **TraceFiles** della cartella di installazione.</span><span class="sxs-lookup"><span data-stu-id="45659-125">After this installation step in completed, the example trace files with the extension **trx** are found in the **TraceFiles** subdirectory of your installation folder.</span></span> <span data-ttu-id="45659-126">Questi esempi predefiniti consentiranno di familiarizzare con l'uso di TraceX nei buffer di traccia generati da ThreadX in esecuzione con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45659-126">These pre-built examples will help you get comfortable with using TraceX on the trace buffers generated by ThreadX running with your application.</span></span>

<span data-ttu-id="45659-127">Un file di traccia di esempio sempre presente è il file \***demo_threadx. TRX** _.</span><span class="sxs-lookup"><span data-stu-id="45659-127">One example trace file always present is the file \***demo_threadx.trx** _.</span></span> <span data-ttu-id="45659-128">In questo file di traccia di esempio viene illustrata l'esecuzione della demo ThreadX standard, come descritto nel capitolo 6 del manuale dell'utente di _ThreadX \*.</span><span class="sxs-lookup"><span data-stu-id="45659-128">This example trace file shows the execution of the standard ThreadX demo, as described in Chapter 6 of the _ThreadX User Guide\*.</span></span>

![Screenshot della finestra di dialogo Apri in TraceX.](./media/user-guide/screen_shot_9.png)

<span data-ttu-id="45659-130">**FIGURA 2**</span><span class="sxs-lookup"><span data-stu-id="45659-130">**FIGURE 2**</span></span>
