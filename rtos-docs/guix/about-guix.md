---
title: Guida per l'utente di Azure RTOS GUIX
description: Questa guida contiene informazioni complete su Azure RTOS GUIX, il prodotto GUI ad alte prestazioni di Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: e7cc1f44648111a75cd6b28d6b98480b721af9c8521e8fcb8cdac6f24c5514e7
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784700"
---
# <a name="about-guix-user-guide"></a>Informazioni sulla Guida dell'utente GUIX

Questa guida contiene informazioni complete su Azure RTOS GUIX, il prodotto GUI ad alte prestazioni di Microsoft. È destinato agli sviluppatori di software in tempo reale incorporati che hanno familiarità con i concetti di base dell'interfaccia utente grafica, Azure RTOS ThreadX e il linguaggio di programmazione C.

## <a name="organization"></a>Organization

[Capitolo 1 - Introduzione a Azure RTOS GUIX](chapter-1.md)

[Capitolo 2 - Installazione e uso di Azure RTOS GUIX](chapter-2.md)

[Capitolo 3 - Panoramica funzionale di Azure RTOS GUIX](chapter-3.md)

[Capitolo 4 - Descrizione dei Azure RTOS GUIX](chapter-4.md)

[Capitolo 5 - Azure RTOS driver di visualizzazione GUIX](chapter-5.md)  

[Azure RTOS GUIX di esempio](guix-example.md)

[Appendice A - Azure RTOS di colori GUIX](appendix-a.md)

[Appendice B - Azure RTOS di colori GUIX](appendix-b.md)

[Appendice C - Azure RTOS di widget GUIX](appendix-c.md)

[Appendice D : Azure RTOS pennello GUIX, canvas e sfumatura](appendix-d.md)

[Appendice E - Descrizione Azure RTOS evento GUIX](appendix-e.md)

[Appendice F - Azure RTOS di binding RTOS GUIX](appendix-f.md)

[Appendice G - Azure RTOS carattere GUIX](appendix-g.md)

[Appendice H : Azure RTOS di configurazione Build-Time GUIX](appendix-h.md)

[Appendice I - Azure RTOS di informazioni GUIX](appendix-i.md)

## <a name="guide-conventions"></a>Convenzioni della guida

*Corsivo:* il carattere tipografico indica i titoli dei libri, sottolinea le parole importanti e indica le variabili.

**Grassetto:** il carattere tipografico indica i nomi dei file, le parole chiave e sottolinea ulteriormente le parole e le variabili importanti.

> [!IMPORTANT]
> I simboli di informazioni richiamano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulle funzioni.

## <a name="azure-rtos-guix-data-types"></a>Azure RTOS di dati GUIX

Oltre ai tipi di dati personalizzati Azure RTOS struttura del controllo GUIX, sono disponibili diversi tipi di dati speciali usati nelle interfacce Azure RTOS di chiamata del servizio GUIX. Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante. Questa operazione viene eseguita per garantire la portabilità tra compilatori C diversi. L'implementazione esatta viene ereditata da ThreadX ed è disponibile nel file ***tx_port.h*** incluso nella distribuzione ThreadX.

Di seguito è riportato un elenco di Azure RTOS di dati delle chiamate al servizio GUIX e dei relativi significati associati:

| <!-- --> | <!-- --> |
| --------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Uint**             | Intero senza segno di base. Questo tipo viene mappato al tipo di dati senza segno più pratico.                                |
| **INT**              | Intero con segno di base. Questo tipo viene mappato al tipo di dati con segno più pratico.                                    |
| **Ulong**            | Tipo long senza segno. Questo tipo deve supportare dati senza segno a 32 bit.                                                      |
| **Vuoto**             | Quasi sempre equivalente al tipo void del compilatore.                                                                 |
| **GX_CHAR**         | Il più delle volte typedefed come tipo char definito dal compilatore.                                                               |
| **GX_BYTE**          | Tipo con segno a 8 bit.                                                                                                    |
| **GX_UBYTE**         | Tipo senza segno a 8 bit.                                                                                                  |
| **GX_VALUE**        | Tipo con segno a 16 o 32 bit. Definito in base alle esigenze per ottenere prestazioni ottimali nel sistema di destinazione.                                |
| **GX_FIXED_VAL**   | Tipo di dati numerico a virgola fissa.                                                                                        |
| **GX_RESOURCE_ID** | Tipo long senza segno.                                                                                                   |
| **GX_COLOR**        | Tipo long senza segno.                                                                                                   |
| **GX_STRING**       | Struttura contenente GX_CHAR \* gx_string_ptr e UINT gx_string_length.                                          |
| **GX_POINT**        | Struttura contenente gx_point_x e gx_point_y.                                                                   |
| **GX_RECTANGLE**    | Struttura contenente gx_rectangle_left, gx_rectangle_top, gx_rectangle_right e gx_rectangle_bottom campi. |
| **GX_GLYPH**        | Struttura contenente le metriche dei glifi.                                                                                   |
| **GX_FONT**         | Struttura contenente le metriche dei tipi di carattere.                                                                                    |
| **GX_BRUSH**        | Struttura contenente le metriche del pennello.                                                                               |
**GX_PIXELMAP**       | Struttura contenente le metriche della mappa pixel.

All'interno dell'origine GUIX vengono Azure RTOS tipi di dati aggiuntivi. Si trovano nei file ***tx_port.h** _ o _ *_gx_port.h_** .

## <a name="customer-support-center"></a>Centro supporto clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica in modo da poter risolvere in modo più efficiente la richiesta di supporto:

1. Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotto in modo affidabile.

2. Descrizione dettagliata delle modifiche apportate all'applicazione e/o Azure RTOS GUIX che ha preceduto il problema.

3. Contenuto delle stringhe _tx_version_id e gx_version_id presenti nei file _***tx_port.h**_ e _ *_gx_port.h_** della distribuzione. Queste stringhe forniscono informazioni utili sull'ambiente di esecuzione.

4. Contenuto nella RAM delle variabili ULONG seguenti:

    **_tx_build_options** **_gx_system_build_options**

    Queste variabili forniscono informazioni su come sono state compilate le librerie Azure RTOS ThreadX e Azure RTOS GUIX.

5. Contenuto nella RAM delle variabili ULONG seguenti:

    **_gx_system_last_error** **_gx_system_error_count**

    Queste variabili tengono traccia degli errori di sistema interni in Azure RTOS GUIX. Se il _gx_system_error_count è maggiore di uno, impostare un punto di interruzione sulla funzione restituita nella funzione _gx_system_error_process e specificare il valore di _gx_system_last_error a questo punto. Verrà restituito il primo errore di Azure RTOS di sistema GUIX interno.

6. Buffer di traccia acquisito immediatamente dopo che è stato rilevato il problema. Questa operazione viene eseguita compilando le librerie GUIX Azure RTOS ThreadX e Azure RTOS con TX_ENABLE_EVENT_TRACE e chiamando tx_trace_enable con le informazioni sul buffer di traccia.

7. Il Azure RTOS progetto GUIX Studio in uso, se applicabile, o almeno un piccolo progetto sufficiente a dimostrare la mancanza di segnalazione.
