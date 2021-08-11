---
title: Informazioni sulla guida Azure RTOS'utente di NetX Duo
description: Questa guida contiene informazioni complete su Azure RTOS NetX Duo, lo stack di rete duale IPv4/IPv6 ad alte prestazioni microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 032cca3ccdaa7600732d52894d63e5bef366010abaa1145417201f48cb034ab5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790174"
---
# <a name="about-the-azure-rtos-netx-duo-user-guide"></a>Informazioni sulla guida Azure RTOS'utente di NetX Duo

Questa guida contiene informazioni complete su Azure RTOS NetX Duo, lo stack di rete duale IPv4/IPv6 ad alte prestazioni microsoft. 

È destinato agli sviluppatori di software in tempo reale incorporati che hanno familiarità con i concetti di rete di base, Azure RTOS ThreadX e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1](chapter1.md) - Introduzione Azure RTOS NetX Duo

[Capitolo 2:](chapter2.md) Illustra i passaggi di base per installare e usare Azure RTOS NetX Duo con l'applicazione ThreadX

[Capitolo 3](chapter3.md) - Offre una panoramica funzionale del sistema NetX Duo Azure RTOS informazioni di base sugli standard di rete TCP/IP

[Capitolo 4](chapter4.md) - Dettagli dell'interfaccia dell'applicazione per Azure RTOS NetX Duo

[Capitolo 5](chapter5.md) - Descrive i driver di rete per Azure RTOS NetX Duo

[Appendice A](appendix-a.md) - Azure RTOS NetX Duo Services

[Appendice B](appendix-b.md) - Azure RTOS costanti NetX Duo

[Appendice C](appendix-c.md) - Azure RTOS di dati NetX Duo

[Appendice D](appendix-d.md) - API BSD-Compatible Socket

[Appendice E](appendix-e.md) - Grafico ASCII

## <a name="guide-conventions"></a>Convenzioni della guida

Corsivo: il carattere tipografico indica i titoli dei libri, sottolinea le parole importanti e indica le variabili.

**Grassetto:** il carattere tipografico indica i nomi dei file, le parole chiave e sottolinea ulteriormente le parole e le variabili importanti.

> [!IMPORTANT]
> I simboli di informazioni richiamano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulle funzioni.
 
> [!WARNING]
> I simboli di avviso richiamano l'attenzione su situazioni che gli sviluppatori devono evitare perché potrebbero causare errori irreversibili.

## <a name="azure-rtos-netx-duo-data-types"></a>Azure RTOS di dati NetX Duo

Oltre ai tipi di dati personalizzati Azure RTOS struttura del controllo NetX Duo, sono disponibili diversi tipi di dati speciali usati nelle interfacce di chiamata del servizio NetX Duo Azure RTOS. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per garantire la portabilità tra compilatori C diversi. L'implementazione esatta viene ereditata da ThreadX ed è disponibile nel file ***tx_port.h*** incluso nella distribuzione ThreadX.

Di seguito è riportato un elenco di Azure RTOS di dati delle chiamate al servizio NetX Duo e dei relativi significati associati:

**UINT:** intero senza segno di base. Questo tipo deve supportare dati senza segno a 32 bit. Viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico.  
**ULONG:** tipo long senza segno. Questo tipo deve supportare dati senza segno a 32 bit.
**VOID**: quasi sempre equivalente al tipo void del compilatore.  
**CHAR:** spesso un tipo di carattere standard a 8 bit.  

Nell'origine Azure RTOS NetX Duo vengono usati tipi di dati aggiuntivi. Si trovano nei file ***tx_port.h** _ o _ *_nx_port.h_** .

## <a name="customer-support-center"></a>Centro supporto clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica in modo da poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o Azure RTOS NetX Duo che ha preceduto il problema.
3. Contenuto delle stringhe _tx_version_id e _nx_version_id presenti nei file tx_port.h e nx_port.h della distribuzione. Queste stringhe forniscono informazioni preziose relative all'ambiente di esecuzione.
4. Contenuto nella RAM delle variabili ULONG seguenti:

    **_tx_build_options**

    **_nx_system_build_options1**

    **_nx_system_build_options2**

    **_nx_system_build_options3**

    **_nx_system_build_options4**

    **_nx_system_build_options5**

    Queste variabili forniscono informazioni su Azure RTOS come sono state compilate le librerie threadX e Azure RTOS NetX Duo.

5. Buffer di traccia acquisito immediatamente dopo che è stato rilevato il problema. Questa operazione viene eseguita creando le librerie Azure RTOS ThreadX e Azure RTOS NetX Duo con TX_ENABLE_EVENT_TRACE e chiamando tx_trace_enable con le informazioni sul buffer di traccia.
