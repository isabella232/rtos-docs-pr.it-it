---
title: Riga di comando di GUIX Studio
description: GUIX Studio offre una chiamata da riga di comando utile per le pipeline di compilazione necessarie per aggiornare i file di output generati da Studio.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: bd88054d974aabea30b50c6f4e10b4c5df9994db03ab84a4a5d8f9394b4d6ed8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785397"
---
# <a name="chapter-9-guix-studio-command-line"></a>Capitolo 9: Riga di comando di GUIX Studio

GUIX Studio supporta la chiamata dalla riga di comando, utile per le pipeline di compilazione necessarie per aggiornare i file di output generati da Studio.

## <a name="command-line-usage"></a>Command-Line utilizzo

**Utilizzo: guix_studio** \[ OPTION \] \[ ARGUMENT\]

Aprire il *progetto con estensione gxp.*

Aprire il progetto di Studio e generare i file di output desiderati.


**Esempi:**

`guix_studio demo.gxp`  
Aprire il progetto "demo.gxp"


`guix_studio.exe –p demo.gxp`  
Aprire il progetto "demo.gxp"


`guix_studio.exe –n –p demo.gxp`  
Generare tutti i file di output del progetto demo.gxp.

`guix_studio.exe –n –r –p demo.gxp`  
Generare i file di risorse del progetto demo.gxp


## <a name="command-line-options"></a>Opzioni della riga di comando

```C
***-n --nogui***  
```

Opzione "nogui". Indicare a GUIX Studio di eseguire senza avviare l'interfaccia utente di windowing.

```C
***-o pathname***  
***--log***  
```

Opzione log, specificare un file di log.

```C
***-b***  
***--binary***  
```

Opzione della risorsa binaria. Produce un file di risorse binario anziché un file C.

```C
***-d display1, display2***  
***--display***  
```

Opzione Nomi visualizzati. Se si usa questa opzione, in tutti i file di risorse o di specifica generati vengono inclusi solo i nomi visualizzati specificati. Se questa opzione non viene utilizzata, vengono incluse tutte le schermi.

```C
***-t theme1, theme2***  
***--theme***  
```

Opzione nome/i tema. Se si usa questa opzione, in tutti i file di risorse o di specifica generati vengono inclusi solo i nomi dei temi specificati. Se questa opzione non viene usata, vengono inclusi tutti i temi.

```C
***-l langage1, language2***  
***--language***  
```

Opzione nome/i linguaggio. Se si utilizza questa opzione, i nomi di lingua specificati vengono inclusi nei file di risorse o di specifica generati. In caso contrario, vengono inclusi tutti i nomi delle lingue.

```C
***-r [filename]***  
***--resource***  
```

L'opzione della risorsa specifica che Studio deve produrre un file di risorse per le impostazioni di visualizzazione, i temi e le lingue designati in precedenza.

```C
***-s [filename]***  
***--specification***  
```

L'opzione specification specifica specifica che Studio deve produrre un file di specifica per le lingue, i temi e le lingue designati.

```C
***-p project_pathname***  
***--project***  
```

Project'opzione pathname specificare il progetto di esempio da caricare.

```C
***-i [pathname]***  
***--import***  
```

Importare una stringa da un file di formato xliff o CSV.

***--big_endian***  
Generare i dati delle risorse in formato big-endian.
