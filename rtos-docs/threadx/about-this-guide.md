---
title: Informazioni sulla guida di Azure RTO ThreadX
description: Questa guida fornisce informazioni complete su Azure RTO ThreadX, il kernel in tempo reale a prestazioni elevate Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ad9f782942bcdbb2dc49a9c841d865d97bcb1d4e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822496"
---
# <a name="about-the-azure-rtos-threadx-guide"></a>Informazioni sulla guida di Azure RTO ThreadX

Questa guida fornisce informazioni complete su Azure RTO ThreadX, il kernel in tempo reale a prestazioni elevate Microsoft. 

È progettato per lo sviluppatore di software in tempo reale incorporato. Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1](chapter1.md) : viene fornita una panoramica di base di Azure RTO threadX e della relativa relazione con lo sviluppo incorporato in tempo reale

[Capitolo 2](chapter2.md) : fornisce i *passaggi di base* per installare e usare Azure RTO threadX nell'applicazione immediatamente

[Capitolo 3](chapter3.md) : descrive in dettaglio il funzionamento funzionale di Azure RTO threadX, il kernel in tempo reale a prestazioni elevate

[Capitolo 4](chapter4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO threadX

[Capitolo 5](chapter5.md) -Descrizione della scrittura di driver i/O per le applicazioni threadX di Azure RTO

[Capitolo 6](chapter6.md) : descrive l'applicazione dimostrativa fornita con ogni pacchetto per il supporto del processore threadX di Azure RTO

[Appendice A](appendix-a.md) -API threadX di Azure RTO

[Appendice B](appendix-b.md) -costanti threadX di Azure RTO

[Appendice C](appendix-c.md) -tipi di dati threadX di Azure RTO

[Appendice D](appendix-d.md) -grafico ASCII

## <a name="guide-conventions"></a>Convenzioni della Guida

*Corsivo* : il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica i parametri.

**Grassetto** -Typeface indica parole chiave, costanti, nomi di tipi, elementi dell'interfaccia utente, nomi di variabili e enfatizza ulteriormente le parole importanti.

***Italics e grassetto*** -Typeface denota i nomi di file e di funzione.

> [!IMPORTANT]
> I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.

> [!WARNING]
> I simboli di avviso attirano l'attenzione sulle situazioni in cui gli sviluppatori devono essere attenti a evitare perché potrebbero causare errori irreversibili.

## <a name="azure-rtos-threadx-data-types"></a>Tipi di dati ThreadX di Azure RTO

Oltre ai tipi di dati personalizzati della struttura di controllo ThreadX di Azure RTO, è disponibile una serie di tipi di dati speciali usati nelle interfacce di chiamata del servizio ThreadX di Azure RTO. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per assicurare la portabilità tra diversi compilatori C. L'implementazione esatta si trova nel file ***tx_port. h*** incluso nell'origine.

Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio ThreadX di Azure RTO e dei relativi significati:

| Tipo di dati  | Descrizione |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **UINT** | Unsigned Integer di base. Questo tipo deve supportare i dati senza segno a 8 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico. |
| **ULONG** | Tipo long senza segno. Questo tipo deve supportare i dati senza segno a 32 bit. |
| **VUOTO** | Quasi sempre equivalente al tipo void del compilatore. |
| **CHAR** | Spesso un tipo di carattere standard a 8 bit. |
|  |  |

I tipi di dati aggiuntivi vengono usati all'interno dell'origine ThreadX di Azure RTO. Si trovano anche nel file ***tx_port. h*** .

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX RTO di Azure che hanno preceduto il problema.
3. Contenuto della stringa di *_tx_version_id* trovata nel file *tx_port. h* della distribuzione. Questa stringa fornirà informazioni preziose sull'ambiente di run-time.
4. Contenuto della RAM della variabile **_tx_build_options** **ULONG** . Questa variabile fornirà informazioni su come è stata creata la libreria ThreadX di Azure RTO.
