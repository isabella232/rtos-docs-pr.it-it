---
title: Capitolo 3-Considerazioni sulle classi DPUMP di USBX
description: USBX contiene una classe DPUMP per l'host e il lato dispositivo. Questa classe non è una classe standard, ma piuttosto un esempio che illustra come creare un dispositivo semplice usando due pipe bulk e inviando i dati in queste due pipe
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c7870f1984fe3104d30e3b9efd82010218acbe27
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824518"
---
# <a name="chapter-3---usbx-dpump-class-considerations"></a>Capitolo 3-Considerazioni sulle classi DPUMP di USBX

USBX contiene una classe **DPUMP** per l'host e il lato dispositivo. Questa classe non è una classe standard, ma piuttosto un esempio in cui viene illustrato come creare un dispositivo semplice utilizzando due pipe bulk e inviando i dati in queste due pipe. La classe **DPUMP** può essere usata per avviare una classe personalizzata o per i dispositivi RS232 legacy.

Diagramma di flusso DPUMP USB:

![Diagramma di flusso DPUMP USB](./media/usbx-device-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-device-class"></a>Classe USBX DPUMP Device

La classe Device **DPUMP** usa un thread, che viene avviato al momento della connessione all'host USB. Il thread attende un pacchetto in arrivo nell'endpoint in blocco. Quando viene ricevuto un pacchetto, il contenuto viene copiato in blocco nel buffer dell'endpoint e viene inviata una transazione sull'endpoint, in attesa che l'host invii una richiesta di lettura da questo endpoint. In questo modo viene fornito un meccanismo di loopback tra le operazioni bulk e bulk negli endpoint.
