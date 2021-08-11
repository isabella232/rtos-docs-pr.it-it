---
title: Azure RTOS utente dello stack host USBX
description: Questa guida fornisce informazioni complete su Azure RTOS USBX, il software di base USB ad alte prestazioni di Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: a41f1b386156be6f8fa773fe2b90bb873cff0fd0e8636bc4d3d8f75295bf7f19
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802550"
---
# <a name="azure-rtos-usbx-host-stack-user-guide"></a>Azure RTOS utente dello stack host USBX

Questa guida fornisce informazioni complete su Azure RTOS USBX, il software di base USB ad alte prestazioni di Microsoft.

È destinato allo sviluppatore di software incorporato in tempo reale. Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale, la specifica USB e il linguaggio di programmazione C.

Per informazioni tecniche relative a USB, vedere la specifica USB e le specifiche della classe USB che possono essere scaricate all'indirizzo [https://www.USB.org/developers](https://www.USB.org/developers)

## <a name="organization"></a>Organization

- [**Capitolo 1:**](usbx-host-stack-1.md) contiene un'introduzione Azure RTOS USBX

- [**Capitolo 2:**](usbx-host-stack-2.md) illustra i passaggi di base per installare e usare Azure RTOS USBX con l'Azure RTOS ThreadX

- [**Capitolo 3:**](usbx-host-stack-3.md) fornisce una panoramica funzionale della Azure RTOS USBX e informazioni di base su USB

- [**Capitolo 4-**](usbx-host-stack-4.md) Dettagli dell'interfaccia dell'applicazione per Azure RTOS USBX in modalità host

- [**Capitolo 5:**](usbx-host-stack-5.md) descrive le API delle classi host AZURE RTOS USBX

- [**Capitolo 6:**](usbx-host-stack-6.md) descrive la Azure RTOS USBX CDC-ECM

## <a name="customer-support-center"></a>Customer Support Center

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto.

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o Azure RTOS ThreadX che ha preceduto il problema.
3. Contenuto della stringa *_tx_version_id* specificata nel file *tx_port.h* della distribuzione. Questa stringa fornirà informazioni importanti relative all'ambiente di run-time.
4. Contenuto nella RAM della variabile *_tx_build_options* ULONG. Questa variabile contiene informazioni su come è stata Azure RTOS la libreria ThreadX.
