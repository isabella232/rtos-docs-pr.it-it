---
title: Informazioni sul Manuale Azure RTOS'utente di NetX
description: Questa guida contiene informazioni complete su Azure RTOS NetX, lo stack di rete Microsoft ad alte prestazioni.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d77997e8c5bac598f382e1169a56727af09ab108f57c90cc6265df0691b5926
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796413"
---
# <a name="about-the-azure-rtos-netx-user-guide"></a>Informazioni sul Manuale Azure RTOS'utente di NetX

Questa guida contiene informazioni complete su Azure RTOS NetX, lo stack di rete Microsoft ad alte prestazioni.

È destinato agli sviluppatori di software incorporati in tempo reale che hanno familiarità con i concetti di base relativi alla rete, Azure RTOS ThreadX e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1](chapter1.md) - Introduzione Azure RTOS NetX

[Capitolo 2:](chapter2.md) illustra i passaggi di base per installare e usare Azure RTOS NetX con l'applicazione ThreadX.

[Capitolo 3](chapter3.md) : fornisce una panoramica funzionale del sistema NetX Azure RTOS e informazioni di base sugli standard di rete TCP/IP.

[Capitolo 4](chapter4.md) - Dettagli dell'interfaccia dell'applicazione per Azure RTOS NetX.

[Capitolo 5](chapter5.md) - Descrive i driver di rete per Azure RTOS NetX.

[Appendice A](appendix-a.md) - Azure RTOS Servizi NetX

[Appendice B](appendix-b.md) - Azure RTOS costanti NetX

[Appendice C](appendix-c.md) - Azure RTOS di dati NetX

[Appendice D](appendix-d.md) - API BSD-Compatible Socket

[Appendice E](appendix-e.md) - Grafico ASCII

## <a name="azure-rtos-netx-data-types"></a>Azure RTOS di dati NetX

Oltre ai tipi di dati Azure RTOS struttura del controllo NetX personalizzati, esistono diversi tipi di dati speciali usati nelle interfacce di chiamata Azure RTOS netx. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per garantire la portabilità tra compilatori C diversi. L'implementazione esatta viene ereditata da ThreadX e si trova nel file ***tx_port.h*** incluso nella distribuzione ThreadX.

Di seguito è riportato un elenco di Azure RTOS di dati delle chiamate al servizio NetX e dei relativi significati associati:

| Tipi di dati | Descrizione  |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Uint**  | Intero senza segno di base. Questo tipo deve supportare dati senza segno a 32 bit. viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico. |
| **Ulong** | Tipo long senza segno. Questo tipo deve supportare dati senza segno a 32 bit.                                                                      |
| **Vuoto**  | Quasi sempre equivalente al tipo void del compilatore.                                                                                 |
| **CHAR**  | In genere è un tipo di carattere standard a 8 bit.                                                                                           |

I tipi di dati aggiuntivi vengono usati all'interno Azure RTOS'origine NetX. Si trovano nei file ***tx_port.h** _ o _ *_nx_port.h_**.

## <a name="customer-support-center"></a>Customer Support Center

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.

2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o Azure RTOS NetX che ha preceduto il problema.

3. Contenuto delle stringhe **_tx_version_id** e **_nx_version_id** presenti nei **_file tx_port.h_ _ e *_*_nx_port.h_** della distribuzione. Queste stringhe forniranno informazioni importanti relative all'ambiente di run-time.

4. Contenuto nella RAM delle variabili **ULONG** seguenti:

    **_tx_build_options**

    **_nx_system_build_options1**

    **_nx_system_build_options2**

    **_nx_system_build_options3**

    **_nx_system_build_options4**

    **_nx_system_build_options5**

    Queste variabili forniscono informazioni su come sono state compilate Azure RTOS ThreadX e Azure RTOS librerie NetX.

5. Buffer di traccia acquisito immediatamente dopo il rilevato problema. Questa operazione viene eseguita compilando le librerie NetX Azure RTOS ThreadX e Azure RTOS con **TX_ENABLE_EVENT_TRACE** e chiamando **tx_trace_enable** con le informazioni sul buffer di traccia. Per informazioni dettagliate, vedere Azure RTOS'utente di TraceX.
