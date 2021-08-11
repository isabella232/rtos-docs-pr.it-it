---
title: Informazioni sulla Azure RTOS ThreadX
description: Questa guida fornisce informazioni complete su Azure RTOS ThreadX, il kernel microsoft ad alte prestazioni in tempo reale.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 28f088409fdd5e2c075cbf90b21d3d260c811806066e74bffc395207cde0239c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802125"
---
# <a name="about-the-azure-rtos-threadx-guide"></a>Informazioni sulla Azure RTOS ThreadX

Questa guida fornisce informazioni complete su Azure RTOS ThreadX, il kernel microsoft ad alte prestazioni in tempo reale. 

È destinato allo sviluppatore di software in tempo reale incorporato. Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale e con il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1-](chapter1.md) Fornisce una panoramica di base di ThreadX Azure RTOS e della relazione con lo sviluppo incorporato in tempo reale

[Capitolo 2:](chapter2.md) illustra i passaggi di base per installare e  usare Azure RTOS ThreadX nell'applicazione

[Capitolo 3](chapter3.md) - Descrive in dettaglio il funzionamento funzionale di Azure RTOS ThreadX, il kernel ad alte prestazioni in tempo reale

[Capitolo 4](chapter4.md) - Dettagli dell'interfaccia dell'applicazione per Azure RTOS ThreadX

[Capitolo 5](chapter5.md) - Descrizione della scrittura di driver di I/O per Azure RTOS ThreadX

[Capitolo 6](chapter6.md) - Descrive l'applicazione dimostrativa fornita con ogni Azure RTOS di supporto del processore ThreadX

[Appendice A](appendix-a.md) - AZURE RTOS API ThreadX

[Appendice B](appendix-b.md) - Azure RTOS ThreadX

[Appendice C](appendix-c.md) : Azure RTOS di dati ThreadX

[Appendice D](appendix-d.md) - Grafico ASCII

## <a name="guide-conventions"></a>Convenzioni della guida

*Corsivo:* il carattere tipografico indica i titoli dei libri, sottolinea le parole importanti e indica i parametri.

**Grassetto:** il carattere tipografico indica parole chiave, costanti, nomi dei tipi, elementi dell'interfaccia utente, nomi di variabili e sottolinea ulteriormente parole importanti.

***Corsivo e grassetto:*** il carattere tipografico indica i nomi di file e i nomi delle funzioni.

> [!IMPORTANT]
> I simboli di informazioni richiamano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulle funzioni.

> [!WARNING]
> I simboli di avviso richiamano l'attenzione su situazioni in cui gli sviluppatori devono prestare attenzione a evitare perché potrebbero causare errori irreversibili.

## <a name="azure-rtos-threadx-data-types"></a>Azure RTOS di dati ThreadX

Oltre ai tipi di dati personalizzati Azure RTOS struttura del controllo ThreadX, sono disponibili una serie di tipi di dati speciali usati nelle interfacce di chiamata del servizio ThreadX Azure RTOS threadX. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per assicurare la portabilità tra compilatori C diversi. L'implementazione esatta è disponibile nel file ***tx_port.h*** incluso nell'origine.

Di seguito è riportato un elenco di Azure RTOS di dati delle chiamate al servizio ThreadX e dei relativi significati associati:

| Tipo di dati  | Descrizione |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Uint** | Intero senza segno di base. Questo tipo deve supportare dati senza segno a 8 bit. Viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico. |
| **Ulong** | Tipo long senza segno. Questo tipo deve supportare dati senza segno a 32 bit. |
| **Vuoto** | Quasi sempre equivalente al tipo void del compilatore. |
| **CHAR** | Il più delle volte è un tipo di carattere standard a 8 bit. |
|  |  |

All'interno dell'origine ThreadX vengono Azure RTOS tipi di dati aggiuntivi. Si trovano anche nel file ***tx_port.h.***

## <a name="customer-support-center"></a>Centro supporto clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica in modo da poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o Azure RTOS ThreadX che ha preceduto il problema.
3. Contenuto della stringa *_tx_version_id* disponibile nel file *tx_port.h* della distribuzione. Questa stringa fornirà informazioni preziose relative all'ambiente di esecuzione.
4. Contenuto nella RAM della variabile **_tx_build_options** **ULONG.** Questa variabile contiene informazioni su come è stata compilata la Azure RTOS ThreadX.
