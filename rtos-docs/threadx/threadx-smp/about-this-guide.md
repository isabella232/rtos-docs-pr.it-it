---
title: Informazioni sulla guida
description: Questa guida fornisce informazioni complete su Azure RTOS ThreadX SMP, il kernel microsoft incorporato in tempo reale ad alte prestazioni.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6a8758bff2f205b06448905634172c05dd7fe189cce9fbe3977f6080c51eb95d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784785"
---
# <a name="about-this-guide"></a>Informazioni sulla guida

Questa guida fornisce informazioni complete su Azure RTOS ThreadX SMP, il kernel microsoft incorporato in tempo reale ad alte prestazioni.

È destinato allo sviluppatore di software incorporato in tempo reale. Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale e con il linguaggio di programmazione C.

## <a name="organization"></a>Organization

| Capitolo       | Panoramica                    |
| ------------- | ---------------------------------------------------------------------------------------------------------- |
| **Capitolo 1** | Fornisce una panoramica di base di ThreadX SMP e della relazione con lo sviluppo incorporato in tempo reale.           |
| **Capitolo 2** | Illustra i passaggi di base per installare e usare ThreadX SMP nell'applicazione.           |
| **Capitolo 3** | Descrive in dettaglio il funzionamento di ThreadX SMP, il kernel SMP in tempo reale ad alte prestazioni.    |
| **Capitolo 4** | Dettagli dell'interfaccia dell'applicazione per ThreadX SMP.                                                        |
| **Capitolo 5** | Descrive la scrittura di driver di I/O per applicazioni ThreadX SMP.                                                |
| **Capitolo 6** | Descrive l'applicazione dimostrativa fornita con ogni pacchetto di supporto del processore SMP ThreadX. |
| **Appendice A** | ThreadX SMP API        |
| **Appendice B** | Costanti SMP ThreadX  |
| **Appendice C** | Tipi di dati SMP ThreadX |
| **Appendice D** | Grafico ASCII            |

## <a name="guide-conventions"></a>Convenzioni della guida

- *Corsivo*  -  *il carattere tipografico indica i titoli dei libri,* evidenzia le parole importanti e indica le variabili.
- **Carattere grassetto**  -  **il carattere tipografico indica i nomi dei file e le parole chiave ed evidenzia ulteriormente le parole e le variabili importanti.**

> [!IMPORTANT]
> I simboli di informazioni richiamano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.

> [!WARNING]
> I simboli di avviso richiamano l'attenzione su situazioni in cui gli sviluppatori devono prestare attenzione a evitare perché potrebbero causare errori irreversibili.

## <a name="threadx-smp-data-types"></a>Tipi di dati SMP ThreadX

Oltre ai tipi di dati della struttura di controllo SMP ThreadX personalizzati, sono disponibili una serie di tipi di dati speciali usati nelle interfacce di chiamata del servizio ThreadX SMP. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per assicurare la portabilità tra compilatori C diversi. L'implementazione esatta è disponibile nel file ***tx_port.h*** incluso nel disco di distribuzione.

Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio ThreadX SMP e dei relativi significati associati:

| Tipo di dati          | Significato                                                          |
| --------- | --------------------------------------------------------- |
| **Uint**  | Intero senza segno di base. Questo tipo deve supportare dati senza segno a 8 bit. viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico. |
| **Ulong** | Tipo long senza segno. Questo tipo deve supportare dati senza segno a 32 bit.                                                                     |
| **Vuoto**  | Quasi sempre equivalente al tipo void del compilatore.                                                                                |
| **CHAR**  | In genere è un tipo di carattere standard a 8 bit.                                                                                          |

All'interno dell'origine ThreadX SMP vengono usati tipi di dati aggiuntivi. Si trovano anche nel file ***tx_port.h.***

## <a name="customer-support-center"></a>Customer Support Center

Messaggio di posta elettronica di [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) supporto: Pagina Web: azure.com/rtos

### <a name="latest-product-information"></a>Ultime informazioni sul prodotto

Visitare il azure.com/rtos Web e selezionare l'opzione di menu "Supporto" per trovare le informazioni di supporto online più recenti, incluse le informazioni sulle versioni più recenti del prodotto ThreadX SMP.

### <a name="what-we-need-from-you"></a>Elementi necessari per l'utente

Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o a ThreadX SMP che hanno preceduto il problema.
3. Contenuto della stringa ***_tx_version_id** _ presente nel file _ *_tx_port.h_** della distribuzione. Questa stringa fornirà informazioni importanti relative all'ambiente di run-time.
4. Contenuto nella RAM della variabile ***_tx_build_options*** ULONG. Questa variabile contiene informazioni su come è stata compilata la libreria SMP ThreadX.

### <a name="where-to-send-comments-about-this-guide"></a>Dove inviare commenti su questa guida

Inviare commenti e suggerimenti tramite posta elettronica al Customer Support Center [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) all'indirizzo Immettere "ThreadX SMP User Guide" (Guida dell'utente di ThreadX SMP) nella riga dell'oggetto.
