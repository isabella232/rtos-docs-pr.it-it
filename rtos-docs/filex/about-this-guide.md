---
title: Azure RTOS utente di FileX
description: Questa guida contiene informazioni complete su Azure RTOS FileX, l'ambiente ad alte prestazioni in tempo file system di Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 48fe70fc3cff6e656328d38b2583116e58a6c98510d5f0554f81a7b728f95457
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782405"
---
# <a name="about-this-filex-user-guide"></a>Informazioni su questo manuale dell'utente di FileX

Questa guida contiene informazioni complete su Azure RTOS FileX, le funzionalità incorporate in tempo reale e ad alte prestazioni file system da Microsoft. Per ottenere il massimo da questa guida, è necessario avere familiarità con le funzioni standard del sistema operativo in tempo reale, i servizi file system FAT e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1](chapter1.md) - Introduzione Azure RTOS FileX

[Capitolo 2:](chapter2.md) Illustra i passaggi di base per installare e usare Azure RTOS FileX con l'Azure RTOS ThreadX

[Capitolo 3](chapter3.md) - Offre una panoramica funzionale del Azure RTOS FileX system e informazioni di base sui formati di file system FAT

[Capitolo 4](chapter4.md) - Dettagli dell'interfaccia dell'applicazione per Azure RTOS FileX

[Capitolo 5](chapter5.md) - Descrive il driver RAM FileX Azure RTOS fornito e come scrivere driver FileX Azure RTOS personalizzati

[Capitolo 6](chapter6.md) - Descrive il modulo Azure RTOS a tolleranza di errore FileX

[Appendice A](appendix-a.md) - Azure RTOS FileX Services

[Appendice B](appendix-b.md) - Azure RTOS costanti FileX

[Appendice C](appendix-c.md) - Azure RTOS di dati FileX

[Appendice D](appendix-d.md) - Grafico ASCII

## <a name="guide-conventions"></a>Convenzioni della guida

*Corsivo:* il carattere tipografico indica i titoli dei libri, sottolinea le parole importanti e indica le variabili.

**Grassetto:** il carattere tipografico indica i nomi dei file, le parole chiave e sottolinea ulteriormente le parole e le variabili importanti.

> [!NOTE]
> I simboli di informazioni richiamano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulle funzioni.

> [!IMPORTANT]
> I simboli di avviso richiamano l'attenzione su situazioni che gli sviluppatori devono evitare perché potrebbero causare errori irreversibili.

## <a name="filex-data-types"></a>Tipi di dati FileX

Oltre ai tipi di dati personalizzati Azure RTOS struttura del controllo FileX, è disponibile una serie di tipi di dati speciali usati nelle interfacce Azure RTOS di chiamata del servizio FileX. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per garantire la portabilità tra compilatori C diversi. L'implementazione esatta viene ereditata da Azure RTOS ThreadX ed è disponibile nel file tx_port.h incluso nella distribuzione Azure RTOS ThreadX.

Di seguito è riportato un elenco di Azure RTOS di dati delle chiamate al servizio FileX e dei relativi significati associati.

| Tipo  | Descrizione  |
|---|---|
| **Uint** | Intero senza segno di base. Questo tipo deve supportare dati senza segno a 8 bit. Viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico. |
| **Ulong** | Tipo long senza segno. Questo tipo deve supportare dati senza segno a 32 bit. |
| **Vuoto** | Quasi sempre equivalente al tipo void del compilatore. |
| **CHAR** | Il più delle volte è un tipo di carattere standard a 8 bit. |
| **ULONG64** | Tipo di dati Integer senza segno a 64 bit. |

All'interno dell'origine FileX vengono usati tipi di dati aggiuntivi. Si trovano nei file ***tx_port.h** _ o _ *_fx_port.h_**.

## <a name="customer-support-center"></a>Centro supporto clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica in modo da poter risolvere in modo più efficiente la richiesta di supporto.

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o a FileX che hanno preceduto il problema.
3. Contenuto delle stringhe _tx_version_id e fx_version_id presenti nei file _***tx_port.h**_ e _ *_fx_port.h_** della distribuzione. Queste stringhe forniscono informazioni preziose relative all'ambiente di esecuzione.
4. Contenuto nella RAM delle variabili **ULONG** seguenti. Queste variabili forniscono informazioni su come sono state compilate le librerie ThreadX e FileX:

    **_tx_build_options**

    **_fx_system_build_options1**

    **_fx_system_build_options2**

    **_fx_system_build_options3**
