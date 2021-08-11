---
title: Capitolo 1 - Panoramica
author: philmea
description: Questo articolo è una panoramica dei Azure RTOS ThreadX
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9018c10e6fe92b2237ec94b633f2f0030ad1cef4bcbcb7afa5ace20548f012ed
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799430"
---
# <a name="chapter-1-overview"></a>Capitolo 1: Panoramica

Il componente ThreadX Module fornisce un'infrastruttura per le applicazioni per caricare dinamicamente i moduli compilati separatamente dalla parte residente dell'applicazione. Ciò è particolarmente utile nelle situazioni in cui le dimensioni del codice dell'applicazione superano la memoria disponibile. Può anche essere utile quando è necessario aggiungere nuove funzionalità dopo la distribuzione dell'immagine di base. Inoltre, il caricamento dinamico dei moduli può essere usato quando sono necessari aggiornamenti parziali del firmware.

La protezione della memoria per il modulo caricato è facoltativa, in base alle proprietà specificate nel preambolo del modulo. Quando si specifica la protezione della memoria, l'hardware di gestione della memoria del processore viene configurato in modo che a tutti i thread del modulo sia consentito solo l'accesso al codice e alla memoria dei dati del modulo. Qualsiasi accesso o esecuzione di memoria estranea comporterà un errore di memoria e il thread del modulo in errore verrà terminato. Se l'applicazione registra un callback di notifica degli errori di memoria, verrà chiamato anche questo metodo per avvisare l'applicazione dell'errore di memoria.

Il componente ThreadX Module si basa sull'applicazione per fornire un'area di memoria in cui è possibile caricare i moduli. L'area di istruzioni di ogni modulo può essere eseguita sul posto o copiata nell'area di memoria del modulo RAM per l'esecuzione. In tutti i casi, i requisiti di memoria dei dati del modulo vengono allocati dall'area di memoria del modulo.

Non sono previsti limiti al numero di moduli che possono essere caricati contemporaneamente (oltre alla quantità di memoria disponibile), mentre è presente una sola copia del codice di Gestione moduli residente. La figura 1 illustra la relazione tra Gestione moduli e i moduli stessi.

![Moduli e relazione di Gestione moduli](media/image2.png)

**Figura 1** Moduli e Gestione moduli

Ogni modulo deve avere una propria area di memoria, che è responsabilità dell'applicazione definire. Il modulo e Gestione moduli interagiscono tramite una funzione di distribuzione software tramite ID richiesta predefiniti che corrispondono ai servizi ThreadX richiesti dal modulo. Inoltre, il modulo è necessario per fornire un singolo punto di ingresso del thread, nonché le dimensioni dello stack, la priorità, l'ID modulo, la dimensione/priorità dello stack del thread di callback e così via. Queste informazioni sono definite nel preambolo di ogni modulo.

Gestione moduli è responsabile della creazione del thread del modulo iniziale e dell'avvio dell'esecuzione. Dopo l'esecuzione del thread iniziale del modulo, Gestione moduli è responsabile dell'impostazione sul campo di tutte le richieste api ThreadX effettuate dal modulo. Un modulo ha accesso completo all'API ThreadX, inclusa la possibilità di creare thread aggiuntivi all'interno del modulo.  
  
Le convenzioni di denominazione del codice sorgente del modulo sono semplici: tutti i file di origine di Gestione moduli sono denominati ***txm_module_manager_ \**** e tutti i file associati esclusivamente al modulo omettono la parte **_"manager_*_" del nome. Il file di inclusione principale _*_txm_module.h_** è condiviso dal codice sorgente del modulo e del gestore.
