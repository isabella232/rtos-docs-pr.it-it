---
title: Capitolo 3 - Considerazioni sulla classe DPUMP USBX
description: USBX contiene una classe DPUMP per il lato host e dispositivo. Questa classe non è una classe standard di per sé, ma piuttosto un esempio che illustra come creare un dispositivo semplice usando due pipe bulk e inviando dati avanti e indietro su queste due pipe
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d453d9ee19b9bc7ca7809102f087f46fdde05dc62b756d9eb3f38f493805be4
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791151"
---
# <a name="chapter-3---usbx-dpump-class-considerations"></a>Capitolo 3 - Considerazioni sulla classe DPUMP USBX

USBX contiene una **classe DPUMP** per il lato host e dispositivo. Questa classe non è una classe standard di per sé, ma piuttosto un esempio che illustra come creare un dispositivo semplice usando due pipe bulk e inviando dati avanti e indietro su queste due pipe. La **classe DPUMP** può essere usata per avviare una classe personalizzata o per i dispositivi RS232 legacy.

Diagramma di flusso USB DPUMP:

![Grafico delle Flow USB DPUMP](./media/usbx-device-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-device-class"></a>Classe di dispositivo USBX DPUMP

La classe **DPUMP del** dispositivo usa un thread che viene avviato al momento della connessione all'host USB. Il thread attende un pacchetto in arrivo nell'endpoint bulk out. Quando un pacchetto viene ricevuto, copia il contenuto nel buffer dell'endpoint Bulk In e invia una transazione su questo endpoint, in attesa che l'host esezioni una richiesta di lettura da questo endpoint. In questo modo viene fornito un meccanismo di loopback tra gli endpoint Bulk Out e Bulk In.
