---
title: Azure RTOS utente di USBX Device Stack
description: Questa guida fornisce informazioni complete su Azure RTOS USBX, il software di base USB ad alte prestazioni di Microsoft
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 042398377766a3e73f72d4dbba0478ba707d378a379fd33de7808675eb96f257
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788763"
---
# <a name="azure-rtos-usbx-device-stack-user-guide"></a>Azure RTOS utente di USBX Device Stack

Questa guida fornisce informazioni complete su Azure RTOS USBX, il software di base USB ad alte prestazioni di Microsoft.

È destinato allo sviluppatore di software in tempo reale incorporato. Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale, la specifica USB e il linguaggio di programmazione C.

Per informazioni tecniche relative a USB, vedere la specifica USB e le specifiche della classe USB che possono essere scaricate all'indirizzo https://www.USB.org/developers

## <a name="organization"></a>Organization

- [**Capitolo 1**](usbx-device-stack-1.md) : contiene un'introduzione Azure RTOS USBX

- [**Capitolo 2:**](usbx-device-stack-2.md) illustra i passaggi di base per installare e usare Azure RTOS USBX con l'applicazione ThreadX

- [**Capitolo 3:**](usbx-device-stack-3.md) descrive i componenti funzionali dello stack Azure RTOS dispositivo USBX

- [**Capitolo 4:**](usbx-device-stack-4.md) descrive i Azure RTOS stack di dispositivi USBX

- [**Capitolo 5:**](usbx-device-stack-5.md) descrive ogni Azure RTOS di dispositivo USBX, incluse le RELATIVE API

## <a name="customer-support-center"></a>Centro supporto clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica in modo da poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o Azure RTOS ThreadX che ha preceduto il problema.
3. Contenuto della stringa **_tx_version_id** disponibile nel file **_tx_port.h_** della distribuzione. Questa stringa fornirà informazioni preziose relative all'ambiente di esecuzione.
4. Contenuto nella RAM della variabile *_tx_build_options* **ULONG.** Questa variabile contiene informazioni su come è stata compilata la Azure RTOS ThreadX.
