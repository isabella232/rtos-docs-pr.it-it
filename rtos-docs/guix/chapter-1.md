---
title: Capitolo 1 - Introduzione a GUIX
description: GUIX è un'implementazione in tempo reale ad alte prestazioni di un'interfaccia utente grafica progettata esclusivamente per applicazioni Azure RTOS basate su ThreadX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e85aab43ba803212875f1fef3ba0bee8484c25b015e400d3b927d492177202b8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784114"
---
# <a name="chapter-1---introduction-to-azure-rtos-guix"></a>Capitolo 1 - Introduzione a Azure RTOS GUIX

Azure RTOS GUIX (GUIX) è un'implementazione in tempo reale ad alte prestazioni di un framework di interfaccia grafica progettato esclusivamente per applicazioni basate su ThreadX incorporate. Questo capitolo contiene un'introduzione a GUIX e una descrizione delle applicazioni e dei vantaggi.

## <a name="guix-feature-overview"></a>Panoramica della funzionalità GUIX

A differenza di molte altre implementazioni gui, GUIX è progettato per essere versatile e passare facilmente da piccole applicazioni basate su micro controller a quelle che usano potenti processori RISC e DSP. Questo è in netto contrasto con il dominio pubblico o altre implementazioni commerciali originariamente destinate agli ambienti workstation, ma poi compresse in progettazioni incorporate. Di seguito è fornita una panoramica delle funzionalità GUIX:

- Facile da usare con lo strumento di progettazione basato su host GUIX Studio

- Ambiente di run-time GUIX Win32 per la prototipazione ospitata completa

- Supporta la maggior parte dei processori supportati da ThreadX

- Scritto esclusivamente in ANSI C

- Neutro endiano

- Interfaccia utente grafica incorporata più piccola e veloce

- Configurabile in fase di esecuzione, numero di oggetti, dimensioni dello schermo e così via.

- Interfaccia del driver video facile da scrivere

- Supporto del colore (fino a 32 bpp), del colore monocromatico e della scala di grigi

- Supporto multilingue tramite la codifica di stringhe UTF8 e le risorse stringa

- Tipi di carattere gratuiti predefiniti e facile da aggiungere nuovi tipi di carattere

- Sono supportati più canvas di disegno di varie dimensioni

- Più display di diverse dimensioni e profondità dei colori supportati

- Supporto della transizione dello schermo (dissolvenza in entrata, dissolvenza in uscita, scorrimento rapido e così via)

- Supporto di touch screen, movimenti e tastiera virtuale

- Compressione bitmap

- Supporto per alpha blending

- Supporto di dithering

- Supporto anti-aliasing

- Interfaccia e temi

- Fusione dell'area di disegno

- Completare la gestione delle finestre

  - Relazione padre/figlio

  - Creazione dinamica, eliminazione, ridimensionamento, spostamento
  - Gestione e disegno di eventi separati 
  - Ordine Z
  - Ritaglio e visualizzazioni

- Set completo di widget

  - Vari tipi di pulsante, dispositivi di scorrimento e quadranti

  - Elenco a discesa
  
  - Prompt

  - Visualizzazione testo su più righe
  
  - Input di testo singolo e multilinea
  
  - Rotelline di scorrimento numerico e testuale
  
  - Windows e barre di scorrimento
  
  - Indicatore di stato radiale
  
  - Sprite

### <a name="ansi-c-source-code"></a>Codice sorgente ANSI C

GUIX è scritto completamente in ANSI C ed è portabile immediatamente a qualsiasi architettura del processore con un compilatore ANSI C e il supporto ThreadX. Anche se scritto in ANSI C, GUIX usa un modello orientato a oggetti e l'ereditarietà.

### <a name="not-a-black-box"></a>Non una scatola nera

La maggior parte delle distribuzioni di GUIX include il codice sorgente C completo. In questo modo si eliminano i problemi di "black box" che si verificano con molte implementazioni dell'interfaccia utente grafica commerciale. Usando GUIX, gli sviluppatori di applicazioni possono vedere esattamente cosa sta facendo l'interfaccia utente grafica. Non ci sono misteri.

La presenza del codice sorgente consente anche modifiche specifiche dell'applicazione. Anche se non è consigliabile, è certamente utile avere la possibilità di modificare l'interfaccia utente grafica, se necessaria. Queste funzionalità sono particolarmente confortanti per gli sviluppatori abituati a lavorare con prodotti di dominio pubblico o interno. Si prevede di avere codice sorgente e la possibilità di modificarlo. GUIX è il software GUI finale per tali sviluppatori.

## <a name="embedded-gui-applications"></a>Applicazioni con interfaccia utente grafica incorporata

Le applicazioni GUI incorporate sono applicazioni che hanno un requisito dell'interfaccia utente ed eseguono su microprocessori nascosti all'interno di prodotti come telefoni cellulari, apparecchiature di comunicazione, motori automobilistici, stampanti laser, dispositivi medici e così via. Tali applicazioni hanno quasi sempre alcuni vincoli di memoria e prestazioni. Un'altra distinzione dell'interfaccia utente grafica incorporata è che il software e l'hardware hanno uno scopo dedicato.

### <a name="real-time-gui-software"></a>Software GUI in tempo reale

In pratica, il software GUI che deve eseguire l'elaborazione entro un periodo di tempo esatto è detto *software* GUI in tempo reale e, quando vengono imposti vincoli di tempo alle applicazioni GUI, vengono classificati come applicazioni in tempo reale. Le applicazioni GUI incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con il mondo esterno.

## <a name="guix-benefits"></a>Vantaggi di GUIX

I vantaggi principali dell'uso di GUIX per le applicazioni incorporate sono i requisiti di memoria ad alte prestazioni, funzionalità elevate e molto piccole. GUIX è anche completamente integrato con il sistema operativo in tempo reale ThreadX Azure RTOS ad alte prestazioni e multitasking.

### <a name="improved-responsiveness"></a>Velocità di risposta migliorata

Il prodotto GUIX ad alte prestazioni consente alle applicazioni di rispondere più velocemente che mai. Ciò è particolarmente importante per le applicazioni incorporate che hanno un volume significativo di informazioni visive o rigorosi requisiti di temporizzazione per la visualizzazione di tali informazioni.

### <a name="software-maintenance"></a>Manutenzione del software

L'uso di GUIX consente agli sviluppatori di partizionare facilmente gli aspetti dell'interfaccia utente grafica dell'applicazione incorporata. Questo partizionamento semplifica l'intero processo di sviluppo e migliora in modo significativo la manutenzione futura del software.

### <a name="increased-throughput"></a>Maggiore velocità effettiva

GUIX offre l'interfaccia utente grafica con le prestazioni più elevate disponibili, che trasferisce direttamente all'applicazione incorporata. Le applicazioni GUIX sono in grado di elaborare le informazioni dell'interfaccia utente più velocemente rispetto alle applicazioni non GUIX.

### <a name="processor-isolation"></a>Isolamento del processore

GUIX offre un'interfaccia affidabile e indipendente dal processore tra l'applicazione e il processore sottostante e l'hardware di visualizzazione. In questo modo, gli sviluppatori possono concentrarsi sugli aspetti di alto livello dell'interfaccia utente anziché dedicarsi più tempo alla gestione dei problemi hardware di visualizzazione.

### <a name="ease-of-use"></a>Facilità d'uso

GUIX è progettato in base allo sviluppatore di applicazioni. L'architettura GUIX e l'interfaccia delle chiamate di servizio sono facili da comprendere. Di conseguenza, gli sviluppatori GUIX possono usare rapidamente le funzionalità avanzate.

### <a name="improve-time-to-market"></a>Migliorare il time-to-market

Le potenti funzionalità di GUIX accelerano il processo di sviluppo software. GUIX astrae la maggior parte dei problemi hardware del processore e della visualizzazione, rimuovendo quindi questi problemi dalla maggior parte dell'implementazione dell'interfaccia utente dell'applicazione. Questa funzionalità, insieme alla facilità d'uso e al set di funzionalità avanzate, consente di ottenere un time-to-market più rapido.

### <a name="protecting-the-software-investment"></a>Protezione dell'investimento software

GUIX è scritto esclusivamente in ANSI C ed è completamente integrato con il sistema operativo Azure RTOS ThreadX in tempo reale. Ciò significa che le applicazioni GUIX sono immediatamente portabili a tutti i processori supportati da ThreadX. Meglio ancora, un'architettura del processore completamente nuova può essere supportata con ThreadX in poche settimane. Di conseguenza, l'uso di GUIX garantisce il percorso di migrazione dell'applicazione e protegge l'investimento di sviluppo originale.
