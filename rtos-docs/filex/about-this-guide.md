---
title: Guida dell'utente di Azure RTO FileX
description: Questa guida contiene informazioni complete su Azure RTO FileX, il file system in tempo reale ad alte prestazioni di Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 640d9ed4c8037d3af6c5f45158c9496ad1258a3c
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550100"
---
# <a name="about-this-filex-user-guide"></a>Informazioni su questo manuale dell'utente di FileX

Questa guida contiene informazioni complete su Azure RTO FileX, il file system incorporato a prestazioni elevate e in tempo reale da Microsoft. Per ottenere il massimo da questa guida, è necessario avere familiarità con le funzioni del sistema operativo in tempo reale standard, i servizi FAT file system e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1](chapter1.md) -introduce Azure RTO FILEX

[Capitolo 2](chapter2.md) : descrive i passaggi di base per installare e usare Azure RTO FILEX con l'applicazione Azure RTO threadX

[Capitolo 3](chapter3.md) -Panoramica funzionale del sistema Azure RTO FILEX e informazioni di base sui formati FAT file System

[Capitolo 4](chapter4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO FILEX

[Capitolo 5](chapter5.md) -descrive il driver RAM FILEX di Azure RTO fornito e come scrivere i driver FILEX di Azure RTO personalizzati

[Capitolo 6](chapter6.md) : descrive il modulo a tolleranza di errore FILEX di Azure RTO

[Appendice A](appendix-a.md) -Servizi FILEX di Azure RTO

[Appendice B](appendix-b.md) -costanti FILEX di Azure RTO

[Appendice C](appendix-c.md) -tipi di dati FILEX di Azure RTO

[Appendice D](appendix-d.md) -grafico ASCII

## <a name="guide-conventions"></a>Convenzioni della Guida

*Italics* : il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.

**Grassetto** -Typeface indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.

> [!NOTE]
> I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.

> [!IMPORTANT]
> I simboli di avviso attirano l'attenzione sulle situazioni che gli sviluppatori devono evitare perché potrebbero causare errori irreversibili.

## <a name="filex-data-types"></a>Tipi di dati FileX

Oltre ai tipi di dati personalizzati della struttura di controllo FileX di Azure RTO, è disponibile una serie di tipi di dati speciali usati nelle interfacce di chiamata del servizio FileX di Azure RTO. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per garantire la portabilità tra diversi compilatori C. L'implementazione esatta viene ereditata da Azure RTO ThreadX ed è disponibile nel file tx_port. h incluso nella distribuzione ThreadX di Azure RTO.

Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio FileX di Azure RTO e dei relativi significati.

| Tipo  | Descrizione  |
|---|---|
| **UINT** | Unsigned Integer di base. Questo tipo deve supportare i dati senza segno a 8 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico. |
| **ULONG** | Tipo long senza segno. Questo tipo deve supportare i dati senza segno a 32 bit. |
| **VUOTO** | Quasi sempre equivalente al tipo void del compilatore. |
| **CHAR** | Spesso un tipo di carattere standard a 8 bit. |
| **ULONG64** | tipo di dati Unsigned Integer a 64 bit. |

I tipi di dati aggiuntivi vengono usati all'interno dell'origine FileX. Si trovano nei file ***tx_port. h** _ o _ *_fx_port. h_**.

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto.

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o FileX che hanno preceduto il problema.
3. Il contenuto delle stringhe _tx_version_id e _fx_version_id trovate nei file ***tx_port. h**_ e _ *_fx_port. h_** della distribuzione. Queste stringhe forniranno informazioni preziose sull'ambiente di run-time.
4. Contenuto della RAM delle variabili **ULONG** seguenti. Queste variabili forniranno informazioni sulla modalità di compilazione delle librerie ThreadX e FileX:

    **_tx_build_options**

    **_fx_system_build_options1**

    **_fx_system_build_options2**

    **_fx_system_build_options3**
