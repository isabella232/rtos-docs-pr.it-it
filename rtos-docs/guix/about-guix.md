---
title: Guida per l'utente di Azure RTOS GUIX
description: Questa guida contiene informazioni complete su Azure RTO GUIX, il prodotto GUI a prestazioni elevate di Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: b7af0fba59b599c9c8db3ab80a3271eacfd11992
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823195"
---
# <a name="about-guix-user-guide"></a>Informazioni sul manuale dell'utente di GUIX

Questa guida contiene informazioni complete su Azure RTO GUIX, il prodotto GUI a prestazioni elevate di Microsoft. È destinato agli sviluppatori di software in tempo reale incorporati che conoscono i concetti di base dell'interfaccia utente grafica, Azure RTO ThreadX e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1-Introduzione ad Azure RTO GUIX](chapter-1.md)

[Capitolo 2-installazione e uso di Azure RTO GUIX](chapter-2.md)

[Capitolo 3-Panoramica funzionale di Azure RTO GUIX](chapter-3.md)

[Capitolo 4-Descrizione dei servizi GUIX di Azure RTO](chapter-4.md)

[Capitolo 5-driver di visualizzazione GUIX di Azure RTO](chapter-5.md)  

[Esempio di GUIX di Azure RTO](guix-example.md)

[Appendice A-definizioni dei colori GUIX di Azure RTO](appendix-a.md)

[Appendice B-formati di colore GUIX di Azure RTO](appendix-b.md)

[Appendice C-stili del widget GUIX di Azure RTO](appendix-c.md)

[Appendice D: attributi pennello, Canvas e sfumatura di Azure RTO GUIX](appendix-d.md)

[Appendice E-Descrizione evento GUIX di Azure RTO](appendix-e.md)

[Appendice F-Azure RTO GUIX RTO binding Services](appendix-f.md)

[Appendice G-struttura del tipo di carattere GUIX di Azure RTO](appendix-g.md)

[Appendice H-Azure RTO GUIX Build-Time flag di configurazione](appendix-h.md)

[Appendice I-strutture di informazioni GUIX di Azure RTO](appendix-i.md)

## <a name="guide-conventions"></a>Convenzioni della Guida

*Italics* : il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.

**Grassetto** -Typeface indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.

> [!IMPORTANT]
> I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.

## <a name="azure-rtos-guix-data-types"></a>Tipi di dati GUIX di Azure RTO

Oltre ai tipi di dati della struttura di controllo GUIX di Azure RTO personalizzati, sono disponibili diversi tipi di dati speciali usati nelle interfacce di chiamata del servizio GUIX di Azure RTO. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per garantire la portabilità tra diversi compilatori C. L'implementazione esatta viene ereditata da ThreadX ed è disponibile nel file ***tx_port. h*** incluso nella distribuzione di threadX.

Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio GUIX di Azure RTO e dei relativi significati:

| <!-- --> | <!-- --> |
| --------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **UINT**             | Unsigned Integer di base. Questo tipo è mappato al tipo di dati senza segno più pratico.                                |
| **INT**              | Intero con segno di base. Questo tipo è mappato al tipo di dati con segno più pratico.                                    |
| **ULONG**            | Tipo long senza segno. Questo tipo deve supportare i dati senza segno a 32 bit.                                                      |
| **VUOTO**             | Quasi sempre equivalente al tipo void del compilatore.                                                                 |
| **GX_CHAR**         | Spesso typedef come tipo char definito dal compilatore.                                                               |
| **GX_BYTE**          | tipo con segno a 8 bit.                                                                                                    |
| **GX_UBYTE**         | tipo senza segno a 8 bit.                                                                                                  |
| **GX_VALUE**        | tipo con segno a 16 o 32 bit. Definito in base alle esigenze per ottenere prestazioni ottimali sul sistema di destinazione.                                |
| **GX_FIXED_VAL**   | Tipo di dati numerico a virgola fissa.                                                                                        |
| **GX_RESOURCE_ID** | Tipo long senza segno.                                                                                                   |
| **GX_COLOR**        | Tipo long senza segno.                                                                                                   |
| **GX_STRING**       | Struttura che contiene GX_CHAR \* gx_string_ptr e UINT gx_string_length.                                          |
| **GX_POINT**        | Struttura contenente gx_point_x e gx_point_y.                                                                   |
| **GX_RECTANGLE**    | Struttura che contiene i campi gx_rectangle_left, gx_rectangle_top, gx_rectangle_right e gx_rectangle_bottom. |
| **GX_GLYPH**        | Struttura che contiene le metriche del glifo.                                                                                   |
| **GX_FONT**         | Struttura che contiene le metriche dei tipi di carattere.                                                                                    |
| **GX_BRUSH**        | Struttura che contiene le metriche del pennello.                                                                               |
**GX_PIXELMAP**       | Struttura che contiene le metriche di Pixelmap.

I tipi di dati aggiuntivi vengono usati all'interno dell'origine GUIX di Azure RTO. Si trovano nei file ***tx_port. h** _ o _ *_gx_port. h_**.

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.

2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o GUIX RTO di Azure che hanno preceduto il problema.

3. Il contenuto delle stringhe _tx_version_id e _gx_version_id trovate nei file ***tx_port. h**_ e _ *_gx_port. h_** della distribuzione. Queste stringhe forniranno informazioni preziose sull'ambiente di run-time.

4. Contenuto della RAM delle variabili ULONG seguenti:

    **_tx_build_options** **_gx_system_build_options**

    Queste variabili forniranno informazioni su come sono state compilate le librerie di Azure RTO ThreadX e Azure RTO GUIX.

5. Contenuto della RAM delle variabili ULONG seguenti:

    **_gx_system_last_error** **_gx_system_error_count**

    Queste variabili tengono traccia degli errori interni del sistema in Azure RTO GUIX. Se il _gx_system_error_count è maggiore di uno, impostare un punto di interruzione sulla funzione return nella funzione _gx_system_error_process e fornire il valore di _gx_system_last_error a questo punto. Verrà restituito il primo errore interno del sistema GUIX di Azure RTO.

6. Un buffer di traccia acquisito immediatamente dopo che il problema è stato rilevato. Questa operazione viene eseguita compilando le librerie Azure RTO ThreadX e Azure RTO GUIX con TX_ENABLE_EVENT_TRACE e chiamando tx_trace_enable con le informazioni sul buffer di traccia.

7. Il progetto di Azure RTO GUIX studio in uso, se applicabile, o almeno un piccolo progetto sufficiente per dimostrare la carenza di report.
