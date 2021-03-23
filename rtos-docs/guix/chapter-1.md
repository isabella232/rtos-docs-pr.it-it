---
title: Capitolo 1-Introduzione a GUIX
description: GUIX è un'implementazione in tempo reale a prestazioni elevate di un'interfaccia utente progettata esclusivamente per applicazioni incorporate basate su Azure RTO ThreadX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b90da988a03d59b1bca3f5584164d641bef96454
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823108"
---
# <a name="chapter-1---introduction-to-azure-rtos-guix"></a>Capitolo 1-Introduzione ad Azure RTO GUIX

Azure RTO GUIX (GUIX) è un'implementazione in tempo reale a prestazioni elevate di un Framework di interfaccia grafica progettato esclusivamente per applicazioni incorporate basate su ThreadX. Questo capitolo contiene un'introduzione a GUIX e una descrizione delle relative applicazioni e vantaggi.

## <a name="guix-feature-overview"></a>Panoramica della funzionalità GUIX

A differenza di molte altre implementazioni GUI, GUIX è progettato per essere versatile, con scalabilità semplice da piccole applicazioni basate su micro-controller, a quelle che usano potenti processori RISC e DSP. Si tratta di un contrasto netto rispetto a un dominio pubblico o ad altre implementazioni commerciali destinate originariamente agli ambienti di workstation, ma vengono quindi compresse in progettazioni incorporate. Di seguito viene riportata una panoramica delle funzionalità di GUIX:

- Facile da usare con lo strumento di progettazione basato su host GUIX Studio

- Ambiente di runtime Win32 GUIX per la prototipazione host completa

- Supporta la maggior parte dei processori supportati da ThreadX

- Scritto esclusivamente in ANSI C

- Endian neutro

- GUI incorporata più piccola e veloce

- Configurabile in fase di esecuzione, numero di oggetti, dimensioni dello schermo e così via.

- Interfaccia del driver di visualizzazione facile da scrivere

- Colore (fino alla profondità del colore di 32-BPP), supporto monocromatico e scala di grigi

- Supporto multilingue tramite codifica di stringhe UTF8 e risorse di stringa

- Tipi di carattere gratuiti predefiniti e facile aggiunta di nuovi tipi di carattere

- Sono supportate più Canvas di disegno di diverse dimensioni

- Sono supportate più visualizzazioni di dimensioni e profondità dei colori diverse

- Supporto della transizione dello schermo (dissolvenza, dissolvenza, scorrimento e così via)

- Supporto per touchscreen, movimenti e tastiera virtuale

- Compressione bitmap

- Supporto per la fusione alfa

- Supporto del dithering

- Supporto anti-aliasing

- Personalizzazione e temi

- Blending Canvas

- Gestione completa della finestra

  - Relazione padre/figlio

  - Creazione dinamica, eliminazione, ridimensionamento, trasferimento
  - Creazione e gestione di eventi distinti 
  - Ordine Z
  - Ritaglio e visualizzazioni

- Set completo di widget

  - Vari tipi di pulsanti, dispositivi di scorrimento e comparazioni

  - Elenco a discesa
  
  - Prompt

  - Visualizzazione di testo su più righe
  
  - Input di testo a riga singola e a più righe
  
  - Rotellina di scorrimento numerica e testuale
  
  - Finestre e barre di scorrimento
  
  - Indicatore di stato radiale
  
  - Sprite

### <a name="ansi-c-source-code"></a>Codice sorgente ANSI C

GUIX è scritto completamente in ANSI C ed è immediatamente portabile in qualsiasi architettura del processore con un compilatore ANSI C e il supporto di ThreadX. Sebbene sia scritto in ANSI C, GUIX utilizza un modello orientato a oggetti ed ereditarietà.

### <a name="not-a-black-box"></a>Non è una scatola nera

La maggior parte delle distribuzioni di GUIX include il codice sorgente C completo. In questo modo si eliminano i problemi "black-box" che si verificano con molte implementazioni GUI commerciali. Con GUIX, gli sviluppatori di applicazioni possono vedere esattamente cosa sta facendo l'interfaccia utente grafica, ma non ci sono misteri.

Il codice sorgente consente anche modifiche specifiche dell'applicazione. Sebbene non sia consigliato, è senz'altro utile avere la possibilità di modificare l'interfaccia utente grafica, se necessaria. Queste funzionalità sono particolarmente confortanti per gli sviluppatori abituati a lavorare con prodotti di dominio interno o pubblico. Si aspettano che il codice sorgente sia in grado di modificarlo. GUIX è il software GUI finale per tali sviluppatori.

## <a name="embedded-gui-applications"></a>Applicazioni GUI incorporate

Le applicazioni GUI incorporate sono applicazioni con requisiti di interfaccia utente e vengono eseguite su microprocessori nascosti all'interno di prodotti quali telefoni cellulari, apparecchiature di comunicazione, motori automobilistici, stampanti laser, dispositivi medicali e così via. Tali applicazioni presentano quasi sempre alcuni vincoli di memoria e di prestazioni. Un'altra distinzione della GUI incorporata è che il software e l'hardware hanno uno scopo dedicato.

### <a name="real-time-gui-software"></a>Software GUI in tempo reale

In pratica, il software GUI che deve eseguire l'elaborazione in un periodo di tempo esatto viene chiamato software *GUI in tempo reale* e quando i vincoli temporali vengono applicati alle applicazioni GUI, vengono classificati come applicazioni in tempo reale. Le applicazioni GUI incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con il mondo esterno.

## <a name="guix-benefits"></a>Vantaggi di GUIX

I principali vantaggi derivanti dall'utilizzo di GUIX per le applicazioni incorporate sono i requisiti di memoria elevate, con funzionalità avanzate e molto ridotte. GUIX è anche completamente integrato con il sistema operativo in tempo reale multitasking di Azure RTO ThreadX per le prestazioni elevate.

### <a name="improved-responsiveness"></a>Velocità di risposta migliorata

Il prodotto GUIX a prestazioni elevate consente alle applicazioni di rispondere più rapidamente che mai. Questo è particolarmente importante per le applicazioni incorporate che hanno un volume significativo di informazioni visive o requisiti di temporizzazione rigidi per la visualizzazione di tali informazioni.

### <a name="software-maintenance"></a>Manutenzione del software

L'uso di GUIX consente agli sviluppatori di partizionare facilmente gli aspetti dell'interfaccia utente grafica dell'applicazione incorporata. Questo partizionamento rende l'intero processo di sviluppo semplice e migliora significativamente la manutenzione futura del software.

### <a name="increased-throughput"></a>Maggiore velocità effettiva

GUIX fornisce l'interfaccia utente grafica a prestazioni elevate disponibile, che trasferisce direttamente all'applicazione incorporata. Le applicazioni GUIX sono in grado di elaborare le informazioni dell'interfaccia utente più velocemente di quelle non GUIX.

### <a name="processor-isolation"></a>Isolamento processore

GUIX fornisce un'interfaccia affidabile e indipendente dal processore tra l'applicazione e il processore sottostante e l'hardware di visualizzazione. Ciò consente agli sviluppatori di concentrarsi sugli aspetti di alto livello dell'interfaccia utente piuttosto che spendere più tempo per la visualizzazione dei problemi hardware.

### <a name="ease-of-use"></a>Semplicità d'uso

GUIX è progettato tenendo presente lo sviluppatore di applicazioni. L'architettura GUIX e l'interfaccia di chiamata del servizio sono facili da comprendere. Di conseguenza, gli sviluppatori GUIX possono usare rapidamente le funzionalità avanzate.

### <a name="improve-time-to-market"></a>Miglioramento del time-to-Market

Le potenti funzionalità di GUIX accelerano il processo di sviluppo del software. GUIX estrae la maggior parte del processore e visualizza problemi hardware, eliminando così questi problemi dalla maggior parte dell'implementazione dell'interfaccia utente dell'applicazione. Questa funzionalità, abbinata alla semplicità d'uso e al set di funzionalità avanzate, comporta tempi di immissione sul mercato più rapidi.

### <a name="protecting-the-software-investment"></a>Protezione dell'investimento software

GUIX è scritto esclusivamente in ANSI C ed è completamente integrato con il sistema operativo Azure RTO ThreadX in tempo reale. Ciò significa che le applicazioni GUIX sono immediatamente portabili a tutti i processori supportati da ThreadX. Meglio ancora, un'architettura del processore completamente nuova può essere supportata con ThreadX in poche settimane. Di conseguenza, l'uso di GUIX garantisce il percorso di migrazione dell'applicazione e protegge l'investimento di sviluppo originale.
