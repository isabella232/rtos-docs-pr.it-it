---
title: Guida dell'utente di Azure RTO TraceX
description: Questa guida contiene informazioni complete su Azure RTO TraceX, lo strumento di analisi del sistema basato su Microsoft Windows di Microsoft.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 92d886b19a0c67292cd4f6a5f8bd7f9d3106374b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823774"
---
# <a name="about-this-guide"></a>Informazioni sulla guida

Questa guida contiene informazioni complete su Azure RTO TraceX, lo strumento di analisi del sistema basato su Microsoft Windows per Microsoft Azure RTO.

È destinato agli sviluppatori di software embedded in tempo reale che usano Azure RTO ThreadX Real-Time sistema operativo (RTO) e componenti aggiuntivi. Lo sviluppatore deve avere familiarità con i concetti standard di Azure RTO ThreadX Azure RTO FileX e Azure RTO NetX.

## <a name="organization"></a>Organization

- [Capitolo 1](chapter1.md) : contiene una panoramica di base di Azure RTO TraceX e ne descrive la relazione con lo sviluppo in tempo reale.
- [Capitolo 2](chapter2.md) : fornisce i passaggi di base per installare e usare Azure RTO TraceX per analizzare immediatamente l'applicazione.
- [Capitolo 3](chapter3.md) : descrive le funzionalità principali di Azure RTO TraceX.
- [Capitolo 4](chapter4.md) : dettagli delle funzionalità di analisi delle prestazioni di Azure RTO TraceX.
- [Capitolo 5](chapter5.md) : descrive come configurare Azure RTO threadX, Azure RTO FILEX e Azure RTO NETX per generare un buffer di traccia visualizzabile da Azure RTO TraceX.
- [Capitolo 6](chapter6.md) : descrive in modo dettagliato gli eventi TraceX di Azure RTO.
- [Capitolo 7](chapter7.md) : descrive in modo dettagliato gli eventi FILEX di Azure RTO.
- [Capitolo 8](chapter8.md) : descrive in modo dettagliato gli eventi NETX di Azure RTO.
- [Capitolo 9](chapter9.md) : descrive in modo dettagliato gli eventi USBX di Azure RTO.
- [Capitolo 10](chapter10.md) : descrive in modo dettagliato la creazione di eventi utente personalizzati.
- [Capitolo 11](chapter11.md) -Descrizione dettagliata del buffer di traccia interno.
- [Appendice a](appendix-a.md) -file specifico della porta di Azure RTO threadX con l'origine timestamp per la raccolta di eventi di traccia.
- [Appendice B](appendix-b.md) -Azure rto threadX *tx_trace file con estensione h* che mostra i dettagli di implementazione relativi al buffer di traccia eventi.
- [Appendice C](appendix-c.md) -riepiloga le utilità della riga di comando per la conversione di diversi formati di file in file binari TraceX RTO di Azure appropriati.
- [Appendice D](appendix-d.md) -esempi di dump dei file di traccia da diversi strumenti di sviluppo.

## <a name="guide-conventions"></a>Convenzioni della Guida

*Italics* : il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.

**Grassetto** -Typeface indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.

> [!NOTE]
> Indica le informazioni di nota.

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX RTO di Azure che hanno preceduto il problema.
3. Contenuto della stringa di *_tx_version_id* trovata nel file *tx_port. h* della distribuzione. Questa stringa fornirà informazioni preziose sull'ambiente di run-time.
4. Contenuto della RAM della variabile *_tx_build_options* ULONG. Questa variabile fornirà informazioni su come è stata creata la libreria ThreadX di Azure RTO.
