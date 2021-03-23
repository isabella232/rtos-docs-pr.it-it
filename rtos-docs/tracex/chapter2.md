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
# <a name="chapter-2---installation-and-use-of-azure-rtos-tracex"></a>Capitolo 2-installazione e uso di Azure RTO TraceX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello strumento di analisi del sistema TraceX di Azure RTO. 

## <a name="product-distribution"></a>Distribuzione del prodotto

È possibile ottenere l'app TraceX da [Microsoft App Store](https://microsoft.com/store/apps) eseguendo la ricerca di TraceX o passando direttamente alla [pagina TraceX](https://www.microsoft.com/p/azure-rtos-tracex/9nf1lfd5xxg3?activetab=pivot:overviewtab). Eseguire quindi le operazioni seguenti.

1. Dalla pagina TraceX nell'App Store, fare clic sul pulsante **Get** o **Install** per installare TraceX.

1. Nel browser potrebbe essere visualizzato un messaggio che chiede se si desidera aprire il Microsoft Store, come illustrato nella figura seguente. In caso contrario, scegliere il pulsante **Apri** .
![Scegliere Apri per installare TraceX.](../guix/media/guix-studio/open-ms-store.png)

1. Al termine dell'installazione, scegliere il pulsante **Avvia** . 

## <a name="using-tracex"></a>Uso di TraceX

L'uso di TraceX è semplice come l'apertura di un file di traccia all'interno di TraceX. Eseguire TraceX tramite il pulsante ***Start** _. A questo punto si osserverà l'interfaccia utente grafica (GUI) di TraceX. A questo punto è possibile usare TraceX per visualizzare graficamente un buffer di traccia di destinazione esistente. A tale scopo, fare clic su _ *_file-> Apri,_* quindi immettere il file di traccia binario.

>[!IMPORTANT]
>*È anche possibile fare doppio clic su qualsiasi file di traccia con estensione **TRX,** che avvierà automaticamente TraceX.*

![Screenshot dell'interfaccia utente grafica di TraceX.](./media/user-guide/screen_shot_8.png)

**FIGURA 1**

>[!IMPORTANT]
>*Vedere il **capitolo 5** per istruzioni su come generare buffer di traccia nella destinazione usando threadX.*

## <a name="tracex-examples"></a>Esempi di TraceX

La prima volta che si esegue l'applicazione TraceX o quando si aggiorna l'applicazione TraceX, verrà richiesto di installare i file di traccia di esempio TraceX e il file custom_events. trxc in una directory definita dall'utente nel computer locale.

Al termine di questo passaggio di installazione, i file di traccia di esempio con estensione **TRX** si trovano nella sottodirectory **TraceFiles** della cartella di installazione. Questi esempi predefiniti consentiranno di familiarizzare con l'uso di TraceX nei buffer di traccia generati da ThreadX in esecuzione con l'applicazione.

Un file di traccia di esempio sempre presente è il file ***demo_threadx. TRX** _. In questo file di traccia di esempio viene illustrata l'esecuzione della demo ThreadX standard, come descritto nel capitolo 6 del manuale dell'utente di _ThreadX *.

![Screenshot della finestra di dialogo Apri in TraceX.](./media/user-guide/screen_shot_9.png)

**FIGURA 2**
