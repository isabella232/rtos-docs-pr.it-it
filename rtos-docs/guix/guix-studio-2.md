---
title: Installazione e uso di GUIX Studio
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo dello strumento di progettazione del sistema dell'interfaccia utente di GUIX Studio.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 55d2b0ac08bdceebdf286effe4bbc679320541243ff78359deafe0858a7b597e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116786473"
---
# <a name="chapter-2-installation-and-use-of-guix-studio"></a>Capitolo 2: Installazione e uso di GUIX Studio

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo dello strumento di progettazione del sistema dell'interfaccia utente di GUIX Studio. 

## <a name="product-distribution"></a>Distribuzione del prodotto

È possibile ottenere l'app GUIX Studio da [Microsoft App Store](https://microsoft.com/store/apps) cercando GUIX Studio o andando direttamente alla pagina [di GUIX Studio.](https://www.microsoft.com/p/azure-rtos-guix-studio/9pbm1k1r7q0f?activetab=pivot:overviewtab) Eseguire quindi le operazioni seguenti.

1. Nella pagina GUIX Studio del App Store fare clic sul pulsante **Get** or **Install** (Scarica o installa) per scaricare GUIX Studio.

1. Il browser potrebbe visualizzare un messaggio che chiede se si vuole aprire il Microsoft Store, come illustrato nella figura seguente. In caso contrario, scegliere il **pulsante** Apri.
![Scegliere Apri per installare GUIX Studio.](./media/guix-studio/open-ms-store.png)

1. Al termine dell'installazione, scegliere il **pulsante** Avvia.

1. La prima volta che GUIX Studio viene avviato, viene visualizzata una finestra di dialogo in cui viene chiesto se si vuole clonare il archivio GUIX nel computer locale. È possibile scegliere di clonare il repository, puntare a dove è già stato clonato il repository oppure scegliere di non clonare affatto il repository (nel qual caso, nel computer è installato un progetto di esempio).
![Scegliere di clonare il repo, puntare a un repo già clonato o ignorare.](./media/guix-studio/clone-repo.png)

> ![!NOTE]
> È possibile tornare a questa finestra  di dialogo in qualsiasi momento scegliendo Configura dal menu principale di GUIX Stuido, seguito da **GUIX Repository**.

Al termine del processo di avvio, si sarà pronti per usare GUIX Studio.

## <a name="using-guix-studio"></a>Uso di GUIX Studio

L'uso di GUIX Studio è semplice: è sufficiente eseguire GUIX Studio tramite il ***pulsante "Avvia".*** A questo punto si osserverà l'interfaccia utente di GUIX Studio. È ora possibile usare GUIX Studio per creare graficamente l'interfaccia utente incorporata. Da qui si crea un nuovo progetto o si apre un progetto esistente, inclusi i progetti di esempio GUIX.

> [!NOTE]
> È anche possibile fare doppio clic su qualsiasi file di progetto GUIX Studio con estensione "**gxp",** che avvierà automaticamente GUIX Studio e aprirà il progetto a cui si fa riferimento.

## <a name="guix-studio-project-samples"></a>Esempi di Project GUIX Studio

Una serie di file di progetto GUIX Studio di esempio con estensione "***gxp**" si trovano nella sottodirectory * _"Samples_**" dell'installazione. Questi progetti di esempio predefiniti consentono di ottenere familiarità con l'uso di GUIX Studio.

Un file di progetto di esempio sempre presente è il file ***samples/demo_guix_simple/guix_simple.gxp** _. Questo file di progetto di esempio mostra la definizione di un'interfaccia utente GUIX semplice, come descritto nel capitolo *_7_** di questo documento.

![Screenshot dell'interfaccia utente di GUIX Studio.](./media/guix-studio/image_10.png)

**Figura 1**

## <a name="keyboard-shortcuts"></a>Tasti di scelta rapida

- **CTRL+N:** Nuovo Project
- **CTRL+O:** Aprire Project
- **CTRL+S:** Salva Project
- **CTRL+MAIUSC+S:** Salva Project con nome
- **ALT+F4:** Uscita
