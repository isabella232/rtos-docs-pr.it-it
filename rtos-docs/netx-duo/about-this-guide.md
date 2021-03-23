---
title: Informazioni sul manuale dell'utente di Azure RTO NetX Duo
description: Questa guida contiene informazioni complete su Azure RTO NetX Duo, lo stack Dual Network IPv4/IPv6 a prestazioni elevate Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b1eef5bfa28f13d7a6b627792f96039b252f2355
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822142"
---
# <a name="about-the-azure-rtos-netx-duo-user-guide"></a>Informazioni sul manuale dell'utente di Azure RTO NetX Duo

Questa guida contiene informazioni complete su Azure RTO NetX Duo, lo stack Dual Network IPv4/IPv6 a prestazioni elevate Microsoft. 

È concepito per gli sviluppatori di software in tempo reale incorporati che conoscono i concetti di base sulla rete, Azure RTO ThreadX e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1](chapter1.md) -introduce Azure RTO NETX Duo

[Capitolo 2](chapter2.md) : fornisce i passaggi di base per installare e usare Azure RTO NETX Duo con l'applicazione threadX

[Capitolo 3](chapter3.md) -Panoramica funzionale del sistema Azure RTO NETX Duo e informazioni di base sugli standard di rete TCP/IP

[Capitolo 4](chapter4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO NETX Duo

[Capitolo 5](chapter5.md) -descrive i driver di rete per Azure RTO NETX Duo

[Appendice A](appendix-a.md) -Azure RTO NETX Duo Services

[Appendice B](appendix-b.md) -costanti di Azure RTO NETX Duo

[Appendice C](appendix-c.md) -tipi di dati di Azure RTO NETX Duo

[Appendice D](appendix-d.md) -BSD-Compatible API socket

[Appendice E](appendix-e.md) -grafico ASCII

## <a name="guide-conventions"></a>Convenzioni della Guida

Italics: il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.

**Grassetto** -Typeface indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.

> [!IMPORTANT]
> I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.
 
> [!WARNING]
> I simboli di avviso attirano l'attenzione sulle situazioni che gli sviluppatori devono evitare perché potrebbero causare errori irreversibili.

## <a name="azure-rtos-netx-duo-data-types"></a>Tipi di dati di Azure RTO NetX Duo

Oltre ai tipi di dati personalizzati della struttura di controllo di Azure RTO NetX Duo, sono disponibili diversi tipi di dati speciali usati nelle interfacce di chiamata del servizio Azure RTO NetX Duo. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per garantire la portabilità tra diversi compilatori C. L'implementazione esatta viene ereditata da ThreadX ed è disponibile nel file ***tx_port. h*** incluso nella distribuzione di threadX.

Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio RTO NetX duo di Azure e dei relativi significati:

**Uint**: Unsigned Integer di base. Questo tipo deve supportare i dati senza segno a 32 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico.  
**ULONG**: tipo long senza segno. Questo tipo deve supportare i dati senza segno a 32 bit.
**Void**: quasi sempre equivalente al tipo void del compilatore.  
**Char**: più spesso un tipo di carattere standard a 8 bit.  

I tipi di dati aggiuntivi vengono usati nell'origine Azure RTO NetX Duo. Si trovano nei file ***tx_port. h** _ o _ *_nx_port. h_**.

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o al duo NetX di Azure RTO che hanno preceduto il problema.
3. Il contenuto delle stringhe _tx_version_id e _nx_version_id trovate nei file tx_port. h e nx_port. h della distribuzione. Queste stringhe forniranno informazioni preziose sull'ambiente di run-time.
4. Contenuto della RAM delle variabili ULONG seguenti:

    **_tx_build_options**

    **_nx_system_build_options1**

    **_nx_system_build_options2**

    **_nx_system_build_options3**

    **_nx_system_build_options4**

    **_nx_system_build_options5**

    Queste variabili forniranno informazioni su come sono state compilate le librerie di Azure RTO ThreadX e Azure RTO NetX Duo.

5. Un buffer di traccia acquisito immediatamente dopo che il problema è stato rilevato. Questa operazione viene eseguita compilando le librerie di Azure RTO ThreadX e Azure RTO NetX Duo con TX_ENABLE_EVENT_TRACE e chiamando tx_trace_enable con le informazioni del buffer di traccia.
