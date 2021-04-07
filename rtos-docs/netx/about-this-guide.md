---
title: Informazioni sul manuale dell'utente di Azure RTO NetX
description: Questa guida contiene informazioni complete su Azure RTO NetX, lo stack di rete a prestazioni elevate Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 01077e3315e87b918cdfd47423d8e0c1b6bbdbbd
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550270"
---
# <a name="about-the-azure-rtos-netx-user-guide"></a>Informazioni sul manuale dell'utente di Azure RTO NetX

Questa guida contiene informazioni complete su Azure RTO NetX, lo stack di rete a prestazioni elevate Microsoft.

È concepito per gli sviluppatori di software in tempo reale incorporati che conoscono i concetti di base sulla rete, Azure RTO ThreadX e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1](chapter1.md) -introduce Azure RTO NETX

[Capitolo 2](chapter2.md) : descrive i passaggi di base per installare e usare Azure RTO NETX con l'applicazione threadX.

[Capitolo 3](chapter3.md) : viene fornita una panoramica funzionale del sistema NETX di Azure RTO e delle informazioni di base sugli standard di rete TCP/IP.

[Capitolo 4](chapter4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO NETX.

[Capitolo 5](chapter5.md) : descrive i driver di rete per Azure RTO NETX.

[Appendice A](appendix-a.md) -Servizi NETX di Azure RTO

[Appendice B](appendix-b.md) -costanti NETX di Azure RTO

[Appendice C](appendix-c.md) -tipi di dati NETX di Azure RTO

[Appendice D](appendix-d.md) -BSD-Compatible API socket

[Appendice E](appendix-e.md) -grafico ASCII

## <a name="azure-rtos-netx-data-types"></a>Tipi di dati NetX di Azure RTO

Oltre ai tipi di dati della struttura di controllo NetX di Azure RTO personalizzati, sono disponibili diversi tipi di dati speciali usati nelle interfacce di chiamata del servizio NetX di Azure RTO. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per garantire la portabilità tra diversi compilatori C. L'implementazione esatta viene ereditata da ThreadX ed è disponibile nel file ***tx_port. h*** incluso nella distribuzione di threadX.

Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio NetX di Azure RTO e dei relativi significati:

| Tipi di dati | Descrizione  |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **UINT**  | Unsigned Integer di base. Questo tipo deve supportare i dati senza segno a 32 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico. |
| **ULONG** | Tipo long senza segno. Questo tipo deve supportare i dati senza segno a 32 bit.                                                                      |
| **VUOTO**  | Quasi sempre equivalente al tipo void del compilatore.                                                                                 |
| **CHAR**  | Spesso un tipo di carattere standard a 8 bit.                                                                                           |

I tipi di dati aggiuntivi vengono usati all'interno dell'origine NetX di Azure RTO. Si trovano nei file ***tx_port. h** _ o _ *_nx_port. h_**.

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.

2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o NetX RTO di Azure che hanno preceduto il problema.

3. Il contenuto delle stringhe **_tx_version_id** e **_nx_version_id** trovate nei file **_tx_port. h_*_ e _*_nx_port. h_** della distribuzione. Queste stringhe forniranno informazioni preziose sull'ambiente di run-time.

4. Contenuto della RAM delle variabili **ULONG** seguenti:

    **_tx_build_options**

    **_nx_system_build_options1**

    **_nx_system_build_options2**

    **_nx_system_build_options3**

    **_nx_system_build_options4**

    **_nx_system_build_options5**

    Queste variabili forniranno informazioni su come sono state compilate le librerie di Azure RTO ThreadX e Azure RTO NetX.

5. Un buffer di traccia acquisito immediatamente dopo che il problema è stato rilevato. Questa operazione viene eseguita compilando le librerie Azure RTO ThreadX e Azure RTO NetX con **TX_ENABLE_EVENT_TRACE** e chiamando **tx_trace_enable** con le informazioni sul buffer di traccia. Per informazioni dettagliate, vedere la guida dell'utente di Azure RTO TraceX.
