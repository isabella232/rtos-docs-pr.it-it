---
title: Manuale dell'utente dello stack di dispositivi USBX di Azure RTO
description: In questa guida vengono fornite informazioni complete su Azure RTO USBX, il software USB Foundation a prestazioni elevate di Microsoft
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: c8e9360c8b72adbc41f840a48e333668c489399e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821332"
---
# <a name="azure-rtos-usbx-device-stack-user-guide"></a>Manuale dell'utente dello stack di dispositivi USBX di Azure RTO

In questa guida vengono fornite informazioni complete su Azure RTO USBX, il software USB Foundation a prestazioni elevate di Microsoft.

È progettato per lo sviluppatore di software in tempo reale incorporato. Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale, le specifiche USB e il linguaggio di programmazione C.

Per informazioni tecniche relative a USB, vedere la specifica USB e le specifiche della classe USB che è possibile scaricare all'indirizzo https://www.USB.org/developers

## <a name="organization"></a>Organization

- [**Capitolo 1**](usbx-device-stack-1.md) -contiene un'introduzione ad Azure RTO USBX

- [**Capitolo 2**](usbx-device-stack-2.md) : fornisce i passaggi di base per installare e usare Azure RTO USBX con l'applicazione threadX

- [**Capitolo 3**](usbx-device-stack-3.md) : descrive i componenti funzionali dello stack di dispositivi USBX di Azure RTO

- [**Capitolo 4**](usbx-device-stack-4.md) : descrive i servizi dello stack di dispositivi USBX di Azure RTO

- [**Capitolo 5**](usbx-device-stack-5.md) : descrive ogni classe di dispositivi USBX di Azure RTO, incluse le relative API

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX RTO di Azure che hanno preceduto il problema.
3. Contenuto della stringa di **_tx_version_id** trovata nel file **_tx_port. h_** della distribuzione. Questa stringa fornirà informazioni preziose sull'ambiente di run-time.
4. Contenuto della RAM della variabile *_tx_build_options* **ULONG** . Questa variabile fornirà informazioni su come è stata creata la libreria ThreadX di Azure RTO.
