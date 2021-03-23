---
title: Riga di comando di GUIX Studio
description: GUIX Studio fornisce la chiamata della riga di comando utile per le pipeline di compilazione necessarie per aggiornare i file di output generati da studio.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9f9bfc67c524a77b5bf736407bf2ca372ce98308
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822196"
---
# <a name="chapter-9-guix-studio-command-line"></a><span data-ttu-id="4e6c5-103">Capitolo 9: riga di comando di GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="4e6c5-103">Chapter 9: GUIX Studio Command Line</span></span>

<span data-ttu-id="4e6c5-104">GUIX Studio supporta la chiamata della riga di comando, utile per le pipeline di compilazione richieste per aggiornare i file di output generati da studio.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-104">GUIX Studio supports command-line invocation,  which is useful for build pipelines that are required to update of the Studio-generated output files.</span></span>

## <a name="command-line-usage"></a><span data-ttu-id="4e6c5-105">Utilizzo Command-Line</span><span class="sxs-lookup"><span data-stu-id="4e6c5-105">Command-Line Usage</span></span>

<span data-ttu-id="4e6c5-106">**Sintassi:** guix_studio \[ \] \[ argomento Option\]</span><span class="sxs-lookup"><span data-stu-id="4e6c5-106">**Usage:** guix_studio \[OPTION\] \[ARGUMENT\]</span></span>

<span data-ttu-id="4e6c5-107">Aprire il progetto *. GXP* .</span><span class="sxs-lookup"><span data-stu-id="4e6c5-107">Open the *.gxp* project.</span></span>

<span data-ttu-id="4e6c5-108">Aprire il progetto studio e generare i file di output desiderati.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-108">Open the Studio project and generate desired output files.</span></span>


<span data-ttu-id="4e6c5-109">**Esempi:**</span><span class="sxs-lookup"><span data-stu-id="4e6c5-109">**Examples:**</span></span>

`guix_studio demo.gxp`  
<span data-ttu-id="4e6c5-110">Apri progetto "demo. GXP"</span><span class="sxs-lookup"><span data-stu-id="4e6c5-110">Open "demo.gxp" project</span></span>


`guix_studio.exe –p demo.gxp`  
<span data-ttu-id="4e6c5-111">Apri progetto "demo. GXP"</span><span class="sxs-lookup"><span data-stu-id="4e6c5-111">Open "demo.gxp" project</span></span>


`guix_studio.exe –n –p demo.gxp`  
<span data-ttu-id="4e6c5-112">Genera tutti i file di output del progetto demo. GXP.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-112">Generate all output files of demo.gxp project.</span></span>

`guix_studio.exe –n –r –p demo.gxp`  
<span data-ttu-id="4e6c5-113">Genera file di risorse del progetto demo. GXP</span><span class="sxs-lookup"><span data-stu-id="4e6c5-113">Generate resource files of demo.gxp project</span></span>


## <a name="command-line-options"></a><span data-ttu-id="4e6c5-114">Opzioni della riga di comando</span><span class="sxs-lookup"><span data-stu-id="4e6c5-114">Command-Line Options</span></span>

```C
***-n --nogui***  
```

<span data-ttu-id="4e6c5-115">Opzione "nogui".</span><span class="sxs-lookup"><span data-stu-id="4e6c5-115">The "nogui" option.</span></span> <span data-ttu-id="4e6c5-116">Indicare a GUIX studio di essere eseguito senza avviare l'interfaccia dell'interfaccia utente di windowing.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-116">Tell GUIX Studio to run without starting the windowing UI interface.</span></span>

```C
***-o pathname***  
***--log***  
```

<span data-ttu-id="4e6c5-117">Opzione log, specificare un file di log.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-117">Log option, specify a log file.</span></span>

```C
***-b***  
***--binary***  
```

<span data-ttu-id="4e6c5-118">Opzione di risorsa binaria.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-118">Binary resource option.</span></span> <span data-ttu-id="4e6c5-119">Produce un file di risorse binario anziché un file C.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-119">Produces a binary resource file rather than a C file.</span></span>

```C
***-d display1, display2***  
***--display***  
```

<span data-ttu-id="4e6c5-120">Opzione nome visualizzato.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-120">Display names option.</span></span> <span data-ttu-id="4e6c5-121">Se si usa questa opzione, solo i nomi visualizzati specificati verranno inclusi in tutti i file delle risorse o delle specifiche generate.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-121">If this option is used, then only the specified display names are included in any generated resource or specification files.</span></span> <span data-ttu-id="4e6c5-122">Se questa opzione non viene usata, vengono incluse tutte le visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-122">If this option is not used,  all displays are included.</span></span>

```C
***-t theme1, theme2***  
***--theme***  
```

<span data-ttu-id="4e6c5-123">Opzione nome tema/i.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-123">Theme name(s) option.</span></span> <span data-ttu-id="4e6c5-124">Se si usa questa opzione, solo i nomi di tema specificati verranno inclusi in tutti i file delle risorse o delle specifiche generate.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-124">If this option is used, then only the specified theme names are included in any generated resource or specification files.</span></span> <span data-ttu-id="4e6c5-125">Se questa opzione non viene usata, vengono inclusi tutti i temi.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-125">If this option is not used, all themes are included.</span></span>

```C
***-l langage1, language2***  
***--language***  
```

<span data-ttu-id="4e6c5-126">Opzione del nome della lingua.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-126">Language name(s) option.</span></span> <span data-ttu-id="4e6c5-127">Se si usa questa opzione, i nomi di lingua specificati vengono inclusi nei file di risorse o di specifica generati.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-127">If this option is used,  the specified language names are included in the generated resource or specification files.</span></span> <span data-ttu-id="4e6c5-128">In caso contrario, verranno inclusi tutti i nomi di lingua.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-128">Otherwise all language names are included.</span></span>

```C
***-r [filename]***  
***--resource***  
```

<span data-ttu-id="4e6c5-129">L'opzione resource specifica che studio deve produrre un file di risorse per le visualizzazioni designate in precedenza, i temi e le lingue.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-129">The resource option, specifies that Studio should produce a resource file for previously designated display(s), theme(s), and language(s).</span></span>

```C
***-s [filename]***  
***--specification***  
```

<span data-ttu-id="4e6c5-130">L'opzione specifica, specifica che studio deve produrre un file di specifica per gli schermi designati, i temi e le lingue.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-130">The specification option, specify that studio should produce a specification file for designated display(s), theme(s), and language(s).</span></span>

```C
***-p project_pathname***  
***--project***  
```

<span data-ttu-id="4e6c5-131">Nome percorso progetto, specificare il progetto di esempio da caricare.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-131">Project pathname option, specify the example project to be loaded.</span></span>

```C
***-i [pathname]***  
***--import***  
```

<span data-ttu-id="4e6c5-132">Importa la stringa da un file di formato CSV o XLIFF.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-132">Import string from xliff or csv format file.</span></span>

<span data-ttu-id="4e6c5-133">***--big_endian***</span><span class="sxs-lookup"><span data-stu-id="4e6c5-133">***--big_endian***</span></span>  
<span data-ttu-id="4e6c5-134">Generare dati di risorse in formato big endian.</span><span class="sxs-lookup"><span data-stu-id="4e6c5-134">Generate resource data in big-endian format.</span></span>
