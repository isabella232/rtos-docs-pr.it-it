---
title: Capitolo 1-Introduzione ad Azure RTO USBX stack host
description: USBX è uno stack USB completo per applicazioni con Deep embedded. Questo capitolo introduce USBX, che descrive le applicazioni e i vantaggi.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9ee49903e764e20316438be16b47d2d9208b1363
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824449"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-host-stack"></a>Capitolo 1-Introduzione ad Azure RTO USBX stack host

USBX è uno stack USB completo per applicazioni con Deep embedded. Questo capitolo introduce USBX, che descrive le applicazioni e i vantaggi.

## <a name="usbx-features"></a>Funzionalità di USBX

USBX supportano le tre specifiche USB esistenti: 1,1, 2,0 e OTG. È progettato per essere scalabile e può includere semplici topologie USB con un solo dispositivo connesso, oltre a topologie complesse con più dispositivi e hub a cascata. USBX supporta tutti i tipi di trasferimento dati dei protocolli USB: controllo, bulk, interrupt e isocrono.

USBX supporta sia il lato host che il lato dispositivo. Ogni lato è costituito da tre livelli.

- Livello controller
- Livello stack
- Livello classe

La relazione tra i livelli USB è la seguente.

![Livelli USB](./media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a>Caratteristiche principali del prodotto

- Supporto completo del processore ThreadX
- Nessun royalties
- Completa codice sorgente ANSI C
- Prestazioni in tempo reale
- Supporto tecnico reattivo
- Supporto per più controller host
- Supporto di più classi
- Istanze di più classi
- Integrazione di classi con ThreadX, FileX e NetX
- Supporto per dispositivi USB con più configurazioni
- Supporto per dispositivi compositi USB
- Supporto per gli hub a catena
- Supporto per il risparmio energia USB
- Supporto per USB OTG
- Esportare eventi di traccia per TraceX

## <a name="powerful-services-of-usbx"></a>Potenti servizi di USBX

### <a name="multiple-host-controller-support"></a>Supporto per più controller host

USBX può supportare più controller host USB in esecuzione simultanea. Questa funzionalità consente a USBX di supportare lo standard USB 2,0 usando lo schema di compatibilità con le versioni precedenti associato alla maggior parte dei controller host USB 2,0 attualmente disponibili sul mercato.

### <a name="usb-software-scheduler"></a>Utilità di pianificazione software USB

USBX contiene un'utilità di pianificazione software USB necessaria per supportare i controller USB per i quali non è disponibile l'elaborazione dell'elenco hardware. L'utilità di pianificazione del software USBX organizzerà i trasferimenti USB con la frequenza di servizio e priorità corretta e indicherà al controller USB di eseguire ogni trasferimento.

### <a name="complete-usb-device-framework-support"></a>Supporto completo per il Framework di dispositivi USB

USBX può supportare i dispositivi USB più complessi, tra cui più configurazioni, più interfacce e più impostazioni alternative.

### <a name="easy-to-use-apis"></a>API facili da usare

USBX fornisce lo stack USB molto più efficace in modo che sia facile da comprendere e utilizzare. L'API USBX rende i servizi intuitivi e coerenti. Utilizzando le API della classe USBX fornite, l'applicazione utente non deve comprendere la complessità dei protocolli USB.
