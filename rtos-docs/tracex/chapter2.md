---
title: Capitolo 2 - Installazione e uso di Azure RTOS TraceX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, all'installazione e all'utilizzo dello Azure RTOS di analisi di sistema TraceX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 1a375975ef80cfb7b56466f5d91ed9a0ca00a20a38108e1b81f4fe8e5d85278d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802192"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-tracex"></a>Capitolo 2 - Installazione e uso di Azure RTOS TraceX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, all'installazione e all'utilizzo dello Azure RTOS di analisi di sistema TraceX. 

## <a name="product-distribution"></a>Distribuzione del prodotto

È possibile ottenere l'app TraceX da [Microsoft App Store](https://microsoft.com/store/apps) cercando TraceX o andando direttamente alla [pagina TraceX](https://www.microsoft.com/p/azure-rtos-tracex/9nf1lfd5xxg3?activetab=pivot:overviewtab). Eseguire quindi le operazioni seguenti.

1. Nella pagina TraceX del App Store fare clic sul pulsante **Get** or Install (Ottieni **o** installa) per installare TraceX.

1. Il browser potrebbe visualizzare un messaggio che chiede se si vuole aprire il Microsoft Store, come illustrato nella figura seguente. In caso contrario, scegliere il **pulsante** Apri.
![Scegliere Apri per installare TraceX.](../guix/media/guix-studio/open-ms-store.png)

1. Al termine dell'installazione, scegliere il **pulsante** Avvia. 

## <a name="using-tracex"></a>Uso di TraceX

L'uso di TraceX è semplice quanto l'apertura di un file di traccia all'interno di TraceX. Eseguire TraceX tramite il pulsante ***Start** _. A questo punto si osserverà l'interfaccia utente grafica (GUI) di TraceX. È ora possibile usare TraceX per visualizzare graficamente un buffer di traccia di destinazione esistente. Questa operazione viene eseguita facilmente facendo clic su _ *_File -> Apri,_** e quindi immettendo il file di traccia binario.

>[!IMPORTANT]
>*È anche possibile fare doppio clic su qualsiasi file di traccia con estensione **trx,** che avvierà automaticamente TraceX.*

![Screenshot dell'interfaccia utente grafica di TraceX.](./media/user-guide/screen_shot_8.png)

**FIGURA 1**

>[!IMPORTANT]
>*Fare riferimento **al capitolo 5** per istruzioni su come generare buffer di traccia nella destinazione usando ThreadX.*

## <a name="tracex-examples"></a>Esempi di TraceX

La prima volta che si esegue l'applicazione TraceX o quando l'applicazione TraceX viene aggiornata, verrà richiesto di installare i file di traccia di esempio TraceX e il file custom_events.trxc in una directory definita dall'utente nel computer locale.

Al termine di questo passaggio di installazione in , i file di traccia di esempio con estensione **trx** si trovano nella sottodirectory **TraceFiles** della cartella di installazione. Questi esempi predefiniti consentono di ottenere familiarità con l'uso di TraceX nei buffer di traccia generati da ThreadX in esecuzione con l'applicazione.

Un file di traccia di esempio sempre presente è il file ***demo_threadx.trx** _. Questo file di traccia di esempio mostra l'esecuzione della demo ThreadX standard, come descritto nel capitolo 6 della Guida dell'_ThreadX'utente*.

![Screenshot della finestra di dialogo di apertura in TraceX.](./media/user-guide/screen_shot_9.png)

**FIGURA 2**
