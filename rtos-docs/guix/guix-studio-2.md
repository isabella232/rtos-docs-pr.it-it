---
title: Installazione e uso di GUIX Studio
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello strumento di progettazione del sistema dell'interfaccia utente di GUIX Studio.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d7b5f94c26842b408ea1b00aeeb78e111bea3623
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823072"
---
# <a name="chapter-2-installation-and-use-of-guix-studio"></a><span data-ttu-id="f3167-103">Capitolo 2: installazione e uso di GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="f3167-103">Chapter 2: Installation and Use of GUIX Studio</span></span>

<span data-ttu-id="f3167-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello strumento di progettazione del sistema dell'interfaccia utente di GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="f3167-104">This chapter contains a description of various issues related to installation, setup, and usage of the GUIX Studio UI system design tool.</span></span> 

## <a name="product-distribution"></a><span data-ttu-id="f3167-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="f3167-105">Product Distribution</span></span>

<span data-ttu-id="f3167-106">È possibile ottenere l'app GUIX studio da [Microsoft App Store](https://microsoft.com/store/apps) eseguendo la ricerca di GUIX Studio oppure accedendo direttamente alla [pagina di GUIX Studio](https://www.microsoft.com/p/azure-rtos-guix-studio/9pbm1k1r7q0f?activetab=pivot:overviewtab).</span><span class="sxs-lookup"><span data-stu-id="f3167-106">You can obtain the GUIX Studio app from the [Microsoft App Store](https://microsoft.com/store/apps) by searching for GUIX Studio, or by going directly to [the GUIX Studio page](https://www.microsoft.com/p/azure-rtos-guix-studio/9pbm1k1r7q0f?activetab=pivot:overviewtab).</span></span> <span data-ttu-id="f3167-107">Eseguire quindi le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="f3167-107">Then do the following.</span></span>

1. <span data-ttu-id="f3167-108">Dalla pagina di GUIX studio nell'App Store, fare clic sul pulsante **Get** o **Install** per scaricare GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="f3167-108">From the GUIX Studio page in the App Store, click the **Get** or **Install** button to download GUIX Studio.</span></span>

1. <span data-ttu-id="f3167-109">Nel browser potrebbe essere visualizzato un messaggio che chiede se si desidera aprire il Microsoft Store, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="f3167-109">Your browser may display a message asking if you want to open the Microsoft Store, as shown in the figure below.</span></span> <span data-ttu-id="f3167-110">In caso contrario, scegliere il pulsante **Apri** .</span><span class="sxs-lookup"><span data-stu-id="f3167-110">If it does, choose the **Open** button.</span></span>
<span data-ttu-id="f3167-111">![Scegliere Apri per installare GUIX Studio.](./media/guix-studio/open-ms-store.png)</span><span class="sxs-lookup"><span data-stu-id="f3167-111">![Choose Open to install GUIX Studio.](./media/guix-studio/open-ms-store.png)</span></span>

1. <span data-ttu-id="f3167-112">Al termine dell'installazione, scegliere il pulsante **Avvia** .</span><span class="sxs-lookup"><span data-stu-id="f3167-112">When the install finishes, choose the **Launch** button.</span></span>

1. <span data-ttu-id="f3167-113">La prima volta che si avvia GUIX studio, viene visualizzata una finestra di dialogo in cui viene chiesto se si vuole clonare il repository GUIX nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f3167-113">The first time that GUIX Studio launches, it displays a dialog box asking if you want to clone the GUIX repo to your local computer.</span></span> <span data-ttu-id="f3167-114">È possibile scegliere di clonare il repository, scegliere la posizione in cui è già stato clonato il repository o scegliere di non clonare il repository, nel qual caso è installato un progetto di esempio nel computer.</span><span class="sxs-lookup"><span data-stu-id="f3167-114">You can either choose to clone the repository, point to where you have already cloned the repo, or choose not to clone the repo at all (in which case, one example project is installed on your computer).</span></span>
<span data-ttu-id="f3167-115">![Scegliere di clonare il repository, puntare a un repository già clonato o ignorare.](./media/guix-studio/clone-repo.png)</span><span class="sxs-lookup"><span data-stu-id="f3167-115">![Choose to clone the repo, point to an already-cloned repo, or skip.](./media/guix-studio/clone-repo.png)</span></span>

> <span data-ttu-id="f3167-116">!</span><span class="sxs-lookup"><span data-stu-id="f3167-116">!</span></span>[!NOTE]
> <span data-ttu-id="f3167-117">È possibile tornare a questa finestra di dialogo in qualsiasi momento scegliendo **Configura** dal menu principale di GUIX STUIDO, seguito dal **repository GUIX**.</span><span class="sxs-lookup"><span data-stu-id="f3167-117">You can return to this dialog box at any time by choosing **Configure** from the main menu of GUIX Stuido, followed by **GUIX Repository**.</span></span>

<span data-ttu-id="f3167-118">Al termine del processo di avvio, sarà possibile usare GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="f3167-118">After the startup process is finished, you will be ready to use GUIX Studio.</span></span>

## <a name="using-guix-studio"></a><span data-ttu-id="f3167-119">Uso di GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="f3167-119">Using GUIX Studio</span></span>

<span data-ttu-id="f3167-120">L'uso di GUIX studio è semplice: è sufficiente eseguire GUIX Studio tramite il pulsante "***Avvia***".</span><span class="sxs-lookup"><span data-stu-id="f3167-120">Using GUIX Studio is easy - simply run GUIX Studio via the "***Start***" button.</span></span> <span data-ttu-id="f3167-121">A questo punto si osserverà l'interfaccia utente di GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="f3167-121">At this point you will observe the GUIX Studio UI.</span></span> <span data-ttu-id="f3167-122">A questo punto è possibile usare GUIX Studio per creare graficamente l'interfaccia utente incorporata.</span><span class="sxs-lookup"><span data-stu-id="f3167-122">You are now ready to use GUIX Studio to graphically create your embedded UI.</span></span> <span data-ttu-id="f3167-123">Da qui è possibile creare un nuovo progetto o aprire un progetto esistente, inclusi i progetti di esempio GUIX.</span><span class="sxs-lookup"><span data-stu-id="f3167-123">From here you create a new project or open an existing project, including the GUIX example projects.</span></span>

> [!NOTE]
> <span data-ttu-id="f3167-124">È anche possibile fare doppio clic su un file di progetto di GUIX studio con l'estensione "**GXP",** che avvierà automaticamente GUIX studio e aprirà il progetto a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="f3167-124">You can also double-click on any GUIX Studio project file with an extension of "**gxp,**" which will automatically launch GUIX Studio and open the referenced project.</span></span>

## <a name="guix-studio-project-samples"></a><span data-ttu-id="f3167-125">Esempi di progetti di GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="f3167-125">GUIX Studio Project Samples</span></span>

<span data-ttu-id="f3167-126">Una serie di esempi di file di progetto di GUIX studio con estensione "\***GXP**_" si trova nella_ \* sottodirectory "_Samples_\* \*" dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="f3167-126">A series of example GUIX Studio project files with the extension "\***gxp**_" are found in the "_\*_Samples_\*\*" sub-directory of your installation.</span></span> <span data-ttu-id="f3167-127">Questi progetti di esempio predefiniti ti aiuteranno a familiarizzare con l'uso di GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="f3167-127">These pre-built example projects will help you get comfortable with using GUIX Studio.</span></span>

<span data-ttu-id="f3167-128">Un file di progetto di esempio sempre presente è il file \***Samples/demo_guix_simple/guix_simple. GXP** _.</span><span class="sxs-lookup"><span data-stu-id="f3167-128">One example project file that is always present is the file \***samples/demo_guix_simple/guix_simple.gxp** _.</span></span> <span data-ttu-id="f3167-129">Questo file di progetto di esempio mostra la definizione di una semplice interfaccia utente di GUIX, come descritto in _ *_capitolo 7_*\* di questo documento.</span><span class="sxs-lookup"><span data-stu-id="f3167-129">This example project file shows the definition of a simple GUIX UI, as described in _ *_Chapter 7_*\* of this document.</span></span>

![Screenshot dell'interfaccia utente di GUIX Studio.](./media/guix-studio/image_10.png)

<span data-ttu-id="f3167-131">**Figura 1**</span><span class="sxs-lookup"><span data-stu-id="f3167-131">**Figure 1**</span></span>

## <a name="keyboard-shortcuts"></a><span data-ttu-id="f3167-132">Tasti di scelta rapida</span><span class="sxs-lookup"><span data-stu-id="f3167-132">Keyboard Shortcuts</span></span>

- <span data-ttu-id="f3167-133">**CTRL + N:** Nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="f3167-133">**Ctrl + N:** New Project</span></span>
- <span data-ttu-id="f3167-134">**CTRL + O:** Apri progetto</span><span class="sxs-lookup"><span data-stu-id="f3167-134">**Ctrl + O:** Open Project</span></span>
- <span data-ttu-id="f3167-135">**CTRL + S:** Salva progetto</span><span class="sxs-lookup"><span data-stu-id="f3167-135">**Ctrl + S:** Save Project</span></span>
- <span data-ttu-id="f3167-136">**CTRL + MAIUSC + S:** Salva progetto con nome</span><span class="sxs-lookup"><span data-stu-id="f3167-136">**Ctrl + Shift + S:** Save Project As</span></span>
- <span data-ttu-id="f3167-137">**ALT + F4:** Uscita</span><span class="sxs-lookup"><span data-stu-id="f3167-137">**Alt + F4:** Exit</span></span>
