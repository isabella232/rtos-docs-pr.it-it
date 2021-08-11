---
title: Azure RTOS per l'utente di TraceX
description: Questa guida contiene informazioni complete su Azure RTOS TraceX, lo strumento di analisi di sistema basato Windows Microsoft.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 89a39112d6fc6d231408179ebb3867c21f927326930a1610529b142aa71a1027
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784071"
---
# <a name="about-this-guide"></a>Informazioni sulla guida

Questa guida contiene informazioni complete su Azure RTOS TraceX, lo strumento di analisi di sistema basato Windows Microsoft Microsoft Azure RTOS.

È destinato allo sviluppatore di software in tempo reale incorporato usando Azure RTOS ThreadX Real-Time Operating System (RTOS) e componenti aggiuntivi. Lo sviluppatore deve avere familiarità con i concetti Azure RTOS ThreadX Azure RTOS FileX e Azure RTOS NetX.

## <a name="organization"></a>Organization

- [Capitolo 1:](chapter1.md) contiene una panoramica di base Azure RTOS TraceX e ne descrive la relazione con lo sviluppo in tempo reale.
- [Capitolo 2:](chapter2.md) illustra i passaggi di base per installare e usare Azure RTOS TraceX per analizzare l'applicazione.
- [Capitolo 3:](chapter3.md) descrive le principali funzionalità di Azure RTOS TraceX.
- [Capitolo 4:](chapter4.md) informazioni dettagliate sulle funzionalità di analisi delle prestazioni Azure RTOS TraceX.
- [Capitolo 5:](chapter5.md) descrive come configurare Azure RTOS ThreadX, Azure RTOS FileX e Azure RTOS NetX per generare un buffer di traccia visualizzabile da Azure RTOS TraceX.
- [Capitolo 6:](chapter6.md) descrive in dettaglio Azure RTOS traceX.
- [Capitolo 7:](chapter7.md) descrive in dettaglio Azure RTOS eventi FileX.
- [Capitolo 8:](chapter8.md) descrive in dettaglio Azure RTOS eventi NetX.
- [Capitolo 9:](chapter9.md) descrive in dettaglio Azure RTOS eventi USBX.
- [Capitolo 10:](chapter10.md) descrive in dettaglio la creazione di eventi utente personalizzati.
- [Capitolo 11:](chapter11.md) descrive in dettaglio il buffer di traccia interno.
- [Appendice A:](appendix-a.md) Azure RTOS file specifico della porta ThreadX con l'origine timestamp per la raccolta di eventi di traccia.
- [Appendice B:](appendix-b.md) Azure RTOS file *threadX tx_trace.h* che mostra i dettagli di implementazione relativi al buffer di traccia eventi.
- [Appendice C:](appendix-c.md) riepiloga le utilità della riga di comando per la conversione di vari formati di file Azure RTOS file binari TraceX.
- [Appendice D:](appendix-d.md) esempi di dump dei file di traccia da vari strumenti di sviluppo.

## <a name="guide-conventions"></a>Convenzioni della guida

*Corsivo:* il carattere tipografico indica i titoli dei libri, sottolinea le parole importanti e indica le variabili.

**Grassetto:** il carattere tipografico indica i nomi dei file, le parole chiave e sottolinea ulteriormente le parole e le variabili importanti.

> [!NOTE]
> Indica le informazioni della nota.

## <a name="customer-support-center"></a>Centro supporto clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica in modo da poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o Azure RTOS ThreadX che ha preceduto il problema.
3. Contenuto della stringa *_tx_version_id* disponibile nel file *tx_port.h* della distribuzione. Questa stringa fornirà informazioni preziose relative all'ambiente di run-time.
4. Contenuto nella RAM della variabile *_tx_build_options* ULONG. Questa variabile contiene informazioni su come è stata compilata la Azure RTOS ThreadX.
