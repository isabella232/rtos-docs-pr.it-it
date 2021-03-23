---
title: Guida dell'utente dello stack host di Azure RTO USBX
description: In questa guida vengono fornite informazioni complete su Azure RTO USBX, il software USB Foundation a prestazioni elevate di Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 243b12c4757ee945def8fea01c0d4114e39312ce
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823234"
---
# <a name="azure-rtos-usbx-host-stack-user-guide"></a>Guida dell'utente dello stack host di Azure RTO USBX

In questa guida vengono fornite informazioni complete su Azure RTO USBX, il software USB Foundation a prestazioni elevate di Microsoft.

È progettato per lo sviluppatore di software in tempo reale incorporato. Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale, le specifiche USB e il linguaggio di programmazione C.

Per informazioni tecniche relative a USB, vedere la specifica USB e le specifiche della classe USB che è possibile scaricare all'indirizzo [https://www.USB.org/developers](https://www.USB.org/developers)

## <a name="organization"></a>Organization

- [**Capitolo 1**](usbx-host-stack-1.md) -contiene un'introduzione ad Azure RTO USBX

- [**Capitolo 2**](usbx-host-stack-2.md) : descrive i passaggi di base per installare e usare Azure RTO USBX con l'applicazione Azure RTO threadX

- [**Capitolo 3**](usbx-host-stack-3.md) -Panoramica funzionale di Azure RTO USBX e informazioni di base su USB

- [**Capitolo 4**](usbx-host-stack-4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO USBX in modalità host

- [**Capitolo 5**](usbx-host-stack-5.md) -descrive le API delle classi host USBX di Azure RTO

- [**Capitolo 6**](usbx-host-stack-6.md) -Descrizione della classe CDC-ECM USBX di Azure RTO

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto.

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX RTO di Azure che hanno preceduto il problema.
3. Contenuto della stringa di *_tx_version_id* trovata nel file *tx_port. h* della distribuzione. Questa stringa fornirà informazioni preziose sull'ambiente di run-time.
4. Contenuto della RAM della variabile *_tx_build_options* ULONG. Questa variabile fornirà informazioni su come è stata creata la libreria ThreadX di Azure RTO.
