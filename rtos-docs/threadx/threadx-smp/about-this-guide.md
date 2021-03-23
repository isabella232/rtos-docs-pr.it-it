---
title: Informazioni sulla guida
description: Questa guida fornisce informazioni complete su Azure RTO ThreadX SMP, il kernel in tempo reale embedded a prestazioni elevate Microsoft.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2399666b5b4d7c34db50d539e200c90f06f7235f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821350"
---
# <a name="about-this-guide"></a>Informazioni sulla guida

Questa guida fornisce informazioni complete su Azure RTO ThreadX SMP, il kernel in tempo reale embedded a prestazioni elevate Microsoft.

È progettato per lo sviluppatore di software in tempo reale incorporato. Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

| Capitolo       | Panoramica                    |
| ------------- | ---------------------------------------------------------------------------------------------------------- |
| **Capitolo 1** | Viene fornita una panoramica di base di ThreadX SMP e della relativa relazione con lo sviluppo incorporato in tempo reale.           |
| **Capitolo 2** | Fornisce i passaggi di base per installare e usare ThreadX SMP nell' *applicazione immediatamente.*           |
| **Capitolo 3** | Viene descritto in dettaglio il funzionamento funzionale di ThreadX SMP, il kernel SMP in tempo reale ad alte prestazioni.    |
| **Capitolo 4** | Descrive l'interfaccia dell'applicazione per ThreadX SMP.                                                        |
| **Capitolo 5** | Viene descritto come scrivere i driver I/O per le applicazioni SMP di ThreadX.                                                |
| **Capitolo 6** | Viene descritta l'applicazione dimostrativa fornita con ogni pacchetto del supporto del processore SMP di ThreadX. |
| **Appendice A** | API SMP di ThreadX        |
| **Appendice B** | Costanti SMP ThreadX  |
| **Appendice C** | Tipi di dati SMP di ThreadX |
| **Appendice D** | Grafico ASCII            |

## <a name="guide-conventions"></a>Convenzioni della Guida

- *Corsivo*  -  il *carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.*
- **Grassetto**  -  il **carattere tipografico indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.**

> [!IMPORTANT]
> I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.

> [!WARNING]
> I simboli di avviso attirano l'attenzione sulle situazioni in cui gli sviluppatori devono essere attenti a evitare perché potrebbero causare errori irreversibili.

## <a name="threadx-smp-data-types"></a>Tipi di dati SMP di ThreadX

Oltre ai tipi di dati personalizzati della struttura di controllo SMP ThreadX, è disponibile una serie di tipi di dati speciali usati nelle interfacce di chiamata del servizio SMP di ThreadX. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per assicurare la portabilità tra diversi compilatori C. L'implementazione esatta si trova nel file ***tx_port. h*** incluso nel disco di distribuzione.

Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio SMP di ThreadX e dei relativi significati:

| Tipo di dati          | Significato                                                          |
| --------- | --------------------------------------------------------- |
| **UINT**  | Unsigned Integer di base. Questo tipo deve supportare i dati senza segno a 8 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico. |
| **ULONG** | Tipo long senza segno. Questo tipo deve supportare i dati senza segno a 32 bit.                                                                     |
| **VUOTO**  | Quasi sempre equivalente al tipo void del compilatore.                                                                                |
| **CHAR**  | Spesso un tipo di carattere standard a 8 bit.                                                                                          |

Nell'origine SMP ThreadX vengono usati tipi di dati aggiuntivi. Si trovano anche nel file ***tx_port. h*** .

## <a name="customer-support-center"></a>Centro assistenza clienti

Posta elettronica di supporto: [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) pagina Web: Azure.com/RTOS

### <a name="latest-product-information"></a>Informazioni più recenti sul prodotto

Visitare il sito Web azure.com/rtos e selezionare l'opzione di menu "supporto" per trovare le informazioni più recenti sul supporto online, incluse le informazioni sulle versioni più recenti del prodotto SMP ThreadX.

### <a name="what-we-need-from-you"></a>Elementi necessari

Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.
2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX SMP che hanno preceduto il problema.
3. Contenuto della stringa ***_tx_version_id** _ trovata nel file _ *_tx_port. h_** della distribuzione. Questa stringa fornirà informazioni preziose sull'ambiente di run-time.
4. Contenuto della RAM della variabile ***_tx_build_options*** ULONG. Questa variabile fornirà informazioni sul modo in cui è stata compilata la libreria ThreadX SMP.

### <a name="where-to-send-comments-about-this-guide"></a>Dove inviare commenti sulla guida

Inviare tramite posta elettronica eventuali commenti e suggerimenti al centro assistenza clienti all'indirizzo [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) immettere "THREADX SMP User Guide" nella riga dell'oggetto.
