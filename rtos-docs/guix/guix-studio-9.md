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
# <a name="chapter-9-guix-studio-command-line"></a>Capitolo 9: riga di comando di GUIX Studio

GUIX Studio supporta la chiamata della riga di comando, utile per le pipeline di compilazione richieste per aggiornare i file di output generati da studio.

## <a name="command-line-usage"></a>Utilizzo Command-Line

**Sintassi:** guix_studio \[ \] \[ argomento Option\]

Aprire il progetto *. GXP* .

Aprire il progetto studio e generare i file di output desiderati.


**Esempi:**

`guix_studio demo.gxp`  
Apri progetto "demo. GXP"


`guix_studio.exe –p demo.gxp`  
Apri progetto "demo. GXP"


`guix_studio.exe –n –p demo.gxp`  
Genera tutti i file di output del progetto demo. GXP.

`guix_studio.exe –n –r –p demo.gxp`  
Genera file di risorse del progetto demo. GXP


## <a name="command-line-options"></a>Opzioni della riga di comando

```C
***-n --nogui***  
```

Opzione "nogui". Indicare a GUIX studio di essere eseguito senza avviare l'interfaccia dell'interfaccia utente di windowing.

```C
***-o pathname***  
***--log***  
```

Opzione log, specificare un file di log.

```C
***-b***  
***--binary***  
```

Opzione di risorsa binaria. Produce un file di risorse binario anziché un file C.

```C
***-d display1, display2***  
***--display***  
```

Opzione nome visualizzato. Se si usa questa opzione, solo i nomi visualizzati specificati verranno inclusi in tutti i file delle risorse o delle specifiche generate. Se questa opzione non viene usata, vengono incluse tutte le visualizzazioni.

```C
***-t theme1, theme2***  
***--theme***  
```

Opzione nome tema/i. Se si usa questa opzione, solo i nomi di tema specificati verranno inclusi in tutti i file delle risorse o delle specifiche generate. Se questa opzione non viene usata, vengono inclusi tutti i temi.

```C
***-l langage1, language2***  
***--language***  
```

Opzione del nome della lingua. Se si usa questa opzione, i nomi di lingua specificati vengono inclusi nei file di risorse o di specifica generati. In caso contrario, verranno inclusi tutti i nomi di lingua.

```C
***-r [filename]***  
***--resource***  
```

L'opzione resource specifica che studio deve produrre un file di risorse per le visualizzazioni designate in precedenza, i temi e le lingue.

```C
***-s [filename]***  
***--specification***  
```

L'opzione specifica, specifica che studio deve produrre un file di specifica per gli schermi designati, i temi e le lingue.

```C
***-p project_pathname***  
***--project***  
```

Nome percorso progetto, specificare il progetto di esempio da caricare.

```C
***-i [pathname]***  
***--import***  
```

Importa la stringa da un file di formato CSV o XLIFF.

***--big_endian***  
Generare dati di risorse in formato big endian.
