---
title: Capitolo 1-Introduzione ad Azure RTO USBX Device stack
description: USBX è uno stack USB completo per applicazioni con Deep embedded. Questo capitolo introduce USBX, che descrive le applicazioni e i vantaggi.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 6965303f1fbf19212b9f7ff20f811a71fb207f54
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824527"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-device-stack"></a>Capitolo 1-Introduzione ad Azure RTO USBX Device stack

USBX è uno stack USB completo per applicazioni con Deep embedded. Questo capitolo introduce USBX, che descrive le applicazioni e i vantaggi 

## <a name="usbx-features"></a>Funzionalità di USBX

USBX supporta le tre specifiche USB esistenti: 1,1, 2,0 e OTG. È progettato per essere scalabile e può includere semplici topologie USB con un solo dispositivo connesso, oltre a topologie complesse con più dispositivi e hub a cascata. USBX supporta tutti i tipi di trasferimento dati dei protocolli USB: controllo, bulk, interrupt e isocrono.

USBX supporta sia il lato host che il lato dispositivo. Ogni lato è costituito da tre livelli.

- Livello controller
- Livello stack
- Livello classe

La relazione tra i livelli USB è la seguente:

![Livelli USB](media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a>Caratteristiche principali del prodotto

- Supporto completo del processore ThreadX
- Nessun royalties
- Completa codice sorgente ANSI C
- Prestazioni in tempo reale
- Supporto tecnico reattivo
- Supporto di più classi
- Istanze di più classi
- Integrazione di classi con ThreadX, FileX e NetX
- Supporto per dispositivi USB con più configurazioni
- Supporto per dispositivi compositi USB
- Supporto per il risparmio energia USB
- Supporto per USB OTG
- Esportare eventi di traccia per TraceX

## <a name="powerful-services-of-usbx"></a>Potenti servizi di USBX

### <a name="complete-usb-device-framework-support"></a>Supporto completo per il Framework di dispositivi USB

USBX può supportare i dispositivi USB più complessi, tra cui più configurazioni, più interfacce e più impostazioni alternative.

### <a name="easy-to-use-apis"></a>API facili da usare

USBX fornisce lo stack USB migliore con la massima incorporata in modo facile da comprendere e utilizzare. L'API USBX rende i servizi intuitivi e coerenti. Utilizzando le API della classe USBX fornite, l'applicazione utente non deve comprendere la complessità dei protocolli USB.
