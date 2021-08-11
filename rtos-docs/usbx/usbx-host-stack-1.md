---
title: Capitolo 1 - Introduzione all'Azure RTOS stack host USBX
description: Questo capitolo presenta lo stack di host USBX, descrivendone le applicazioni e i vantaggi.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: abe9b3e4f36a50af9c1267b2e6285b77feecd946660bf23691e70cb66f8bc042
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790998"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-host-stack"></a>Capitolo 1 - Introduzione all'Azure RTOS stack host USBX

USBX è uno stack USB completo per applicazioni con deep embedded. Questo capitolo presenta USBX, che ne descrive le applicazioni e i vantaggi.

## <a name="usbx-features"></a>Funzionalità USBX

USBX supporta le tre specifiche USB esistenti: 1.1, 2.0 e OTG. È progettato per essere scalabile e supporterà topologie USB semplici con un solo dispositivo connesso, nonché topologie complesse con più dispositivi e hub a cascata. USBX supporta tutti i tipi di trasferimento dei dati dei protocolli USB: controllo, blocco, interrupt e isocrone.

USBX supporta sia il lato host che il lato dispositivo. Ogni lato è costituito da tre livelli.

- Livello controller
- Livello stack
- Livello classe

La relazione tra i livelli USB è la seguente.

![Livelli USB](./media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a>Caratteristiche principali del prodotto

- Supporto completo del processore ThreadX
- No royalties
- Completare il codice sorgente ANSI C
- Prestazioni in tempo reale
- Supporto tecnico reattivo
- Supporto di più controller host
- Supporto di più classi
- Più istanze di classe
- Integrazione di classi con ThreadX, FileX e NetX
- Supporto per dispositivi USB con più configurazioni
- Supporto per dispositivi compositi USB
- Supporto per hub a cascata
- Supporto per il risparmio energia USB
- Supporto per USB OTG
- Esportare eventi di traccia per TraceX

## <a name="powerful-services-of-usbx"></a>Potenti servizi di USBX

### <a name="multiple-host-controller-support"></a>Supporto di più controller host

USBX può supportare più controller host USB in esecuzione simultaneamente. Questa funzionalità consente a USBX di supportare lo standard USB 2.0 usando lo schema di compatibilità con le versioni precedenti associato alla maggior parte dei controller host USB 2.0 attualmente sul mercato.

### <a name="usb-software-scheduler"></a>Utilità di pianificazione software USB

USBX contiene un'utilità di pianificazione software USB necessaria per supportare i controller USB che non dispongono dell'elaborazione dell'elenco di hardware. L'utilità di pianificazione del software USBX organizza i trasferimenti USB con la frequenza e la priorità corrette e indica al controller USB di eseguire ogni trasferimento.

### <a name="complete-usb-device-framework-support"></a>Supporto completo del framework di dispositivi USB

USBX può supportare i dispositivi USB più impegnativi, tra cui più configurazioni, più interfacce e più impostazioni alternative.

### <a name="easy-to-use-apis"></a>API facili da usare

USBX offre il miglior stack USB incorporato in modo facile da comprendere e usare. L'API USBX rende i servizi intuitivi e coerenti. Usando le API della classe USBX fornite, l'applicazione utente non deve comprendere la complessità dei protocolli USB.
