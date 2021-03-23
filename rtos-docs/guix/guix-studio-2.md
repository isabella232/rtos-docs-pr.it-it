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
# <a name="chapter-2-installation-and-use-of-guix-studio"></a>Capitolo 2: installazione e uso di GUIX Studio

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello strumento di progettazione del sistema dell'interfaccia utente di GUIX Studio. 

## <a name="product-distribution"></a>Distribuzione del prodotto

È possibile ottenere l'app GUIX studio da [Microsoft App Store](https://microsoft.com/store/apps) eseguendo la ricerca di GUIX Studio oppure accedendo direttamente alla [pagina di GUIX Studio](https://www.microsoft.com/p/azure-rtos-guix-studio/9pbm1k1r7q0f?activetab=pivot:overviewtab). Eseguire quindi le operazioni seguenti.

1. Dalla pagina di GUIX studio nell'App Store, fare clic sul pulsante **Get** o **Install** per scaricare GUIX Studio.

1. Nel browser potrebbe essere visualizzato un messaggio che chiede se si desidera aprire il Microsoft Store, come illustrato nella figura seguente. In caso contrario, scegliere il pulsante **Apri** .
![Scegliere Apri per installare GUIX Studio.](./media/guix-studio/open-ms-store.png)

1. Al termine dell'installazione, scegliere il pulsante **Avvia** .

1. La prima volta che si avvia GUIX studio, viene visualizzata una finestra di dialogo in cui viene chiesto se si vuole clonare il repository GUIX nel computer locale. È possibile scegliere di clonare il repository, scegliere la posizione in cui è già stato clonato il repository o scegliere di non clonare il repository, nel qual caso è installato un progetto di esempio nel computer.
![Scegliere di clonare il repository, puntare a un repository già clonato o ignorare.](./media/guix-studio/clone-repo.png)

> ![!NOTE]
> È possibile tornare a questa finestra di dialogo in qualsiasi momento scegliendo **Configura** dal menu principale di GUIX STUIDO, seguito dal **repository GUIX**.

Al termine del processo di avvio, sarà possibile usare GUIX Studio.

## <a name="using-guix-studio"></a>Uso di GUIX Studio

L'uso di GUIX studio è semplice: è sufficiente eseguire GUIX Studio tramite il pulsante "***Avvia***". A questo punto si osserverà l'interfaccia utente di GUIX Studio. A questo punto è possibile usare GUIX Studio per creare graficamente l'interfaccia utente incorporata. Da qui è possibile creare un nuovo progetto o aprire un progetto esistente, inclusi i progetti di esempio GUIX.

> [!NOTE]
> È anche possibile fare doppio clic su un file di progetto di GUIX studio con l'estensione "**GXP",** che avvierà automaticamente GUIX studio e aprirà il progetto a cui si fa riferimento.

## <a name="guix-studio-project-samples"></a>Esempi di progetti di GUIX Studio

Una serie di esempi di file di progetto di GUIX studio con estensione "***GXP**_" si trova nella_ * sottodirectory "_Samples_* *" dell'installazione. Questi progetti di esempio predefiniti ti aiuteranno a familiarizzare con l'uso di GUIX Studio.

Un file di progetto di esempio sempre presente è il file ***Samples/demo_guix_simple/guix_simple. GXP** _. Questo file di progetto di esempio mostra la definizione di una semplice interfaccia utente di GUIX, come descritto in _ *_capitolo 7_** di questo documento.

![Screenshot dell'interfaccia utente di GUIX Studio.](./media/guix-studio/image_10.png)

**Figura 1**

## <a name="keyboard-shortcuts"></a>Tasti di scelta rapida

- **CTRL + N:** Nuovo progetto
- **CTRL + O:** Apri progetto
- **CTRL + S:** Salva progetto
- **CTRL + MAIUSC + S:** Salva progetto con nome
- **ALT + F4:** Uscita
