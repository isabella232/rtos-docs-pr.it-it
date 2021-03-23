---
title: Capitolo 1-Panoramica
author: philmea
description: Questo articolo è una panoramica dei moduli ThreadX di Azure RTO
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 0c9698086468d7bb41c33ebe9fa9d1ebb61b5f1f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821401"
---
# <a name="chapter-1-overview"></a>Capitolo 1: Panoramica

Il componente del modulo ThreadX fornisce un'infrastruttura per le applicazioni per caricare dinamicamente i moduli compilati separatamente dalla parte residente dell'applicazione. Questa operazione è particolarmente utile nelle situazioni in cui le dimensioni del codice dell'applicazione superano la memoria disponibile. Può anche essere utile quando è necessario aggiungere nuove funzionalità dopo la distribuzione dell'immagine principale. Inoltre, è possibile usare i moduli per il caricamento dinamico quando sono necessari aggiornamenti parziali del firmware.

La protezione della memoria per il modulo caricato è facoltativa, in base alle proprietà specificate nel preambolo del modulo. Quando si specifica la protezione della memoria, l'hardware di gestione della memoria del processore viene configurato in modo che tutti i thread del modulo possano accedere solo al codice e alla memoria dati del modulo. Eventuali accessi o esecuzioni di memoria estranei provocheranno un errore di memoria e il thread del modulo danneggiato verrà interrotto. Se l'applicazione registra un callback di notifica di errore di memoria, verrà chiamato anche per avvertire l'applicazione dell'errore di memoria.

Il componente del modulo ThreadX si basa sull'applicazione per fornire un'area di memoria in cui è possibile caricare i moduli. L'area di istruzioni di ogni modulo può essere eseguita sul posto o essere copiata nell'area di memoria del modulo RAM per l'esecuzione. In tutti i casi, i requisiti di memoria dei moduli vengono allocati dall'area memoria del modulo.

Non sono previsti limiti per il numero di moduli che possono essere caricati contemporaneamente, a parte la quantità di memoria disponibile, mentre è presente una sola copia del codice del gestore dei moduli residente. Nella figura 1 viene illustrata la relazione tra gestione moduli e i moduli.

![Relazione tra moduli e gestione moduli](media/image2.png)

**Figura 1** Moduli e gestione moduli

Ogni modulo deve avere una propria area di memoria, che è responsabilità dell'applicazione definire. Il modulo e gestione moduli interagiscono tramite una funzione di distribuzione software tramite ID richiesta predefiniti che corrispondono ai servizi ThreadX richiesti dal modulo. Il modulo è necessario anche per fornire un punto di ingresso a thread singolo, nonché le dimensioni dello stack, la priorità, l'ID del modulo, la dimensione/priorità dello stack dei thread di callback e così via. Queste informazioni vengono definite nel preambolo di ogni modulo.

Gestione moduli è responsabile della creazione del thread del modulo iniziale e dell'avvio dell'esecuzione. Quando il thread iniziale del modulo è in esecuzione, gestione moduli è responsabile del campo di tutte le richieste API ThreadX effettuate dal modulo. Un modulo ha accesso completo all'API ThreadX, inclusa la possibilità di creare thread aggiuntivi all'interno del modulo.  
  
Le convenzioni di denominazione del codice sorgente del modulo sono semplici: tutti i file di origine di gestione moduli sono denominati ***txm_module_manager_ \**** e tutti i file associati esclusivamente al modulo omettono la parte "**_Manager_*_" del nome. Il file di inclusione principale _*_txm_module. h_** è condiviso dal codice sorgente di gestione e modulo.
