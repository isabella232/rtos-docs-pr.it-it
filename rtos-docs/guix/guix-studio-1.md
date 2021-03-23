---
title: Manuale dell'utente di GUIX Studio
description: In questa guida vengono fornite informazioni complete su GUIX studio, l'ambiente di sviluppo dell'interfaccia utente rapido basato su Microsoft Windows appositamente progettato per la libreria di runtime GUIX di Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 6a5d628581d4c6b44ff093bac45790d6e2755349
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823075"
---
# <a name="chapter-1-introduction-to-azure-rtos-guix-studio"></a>Capitolo 1: introduzione ad Azure RTO GUIX Studio

Azure RTO GUIX studio è un ambiente di sviluppo di interfaccia utente rapido basato su Microsoft Windows appositamente progettato per la libreria di runtime GUIX di Microsoft.

Gli sviluppatori di interfacce utente Embedded possono utilizzare la finestra di progettazione della schermata di GUIX Studio WYSIWYG per creare e aggiornare rapidamente l'interfaccia utente incorporata utilizzando l'ambiente di runtime GUIX. Le progettazioni di GUIX Studio vengono salvate e mantenute in un file di progetto di GUIX studio, con estensione GXP. Quando la progettazione è pronta per l'esecuzione nella destinazione, GUIX Studio genera il codice C che contiene tutte le informazioni e il codice dell'interfaccia utente necessari.

## <a name="guix-studio-requirements"></a>Requisiti di GUIX Studio

Per funzionare correttamente, GUIX studio di Microsoft richiede *Windows XP* (o versione successiva). Il sistema deve avere almeno 200 MB di RAM, 2 GB di spazio disponibile su disco rigido e una visualizzazione minima di 1024x768 con 256 colori. Inoltre, l'applicazione incorporata deve essere in esecuzione in *threadX/GUIX v 6.0* o versione successiva.

Se si desidera essere in grado di compilare ed eseguire l'applicazione dell'interfaccia utente incorporata come eseguibile di Microsoft Windows autonomo, sarà necessario anche un compilatore o un ambiente di compilazione in grado di compilare codice sorgente C per produrre un eseguibile di Microsoft Windows. Il pacchetto di valutazione incluso in GUIX Studio include anche le soluzioni e i file di progetto compatibili con Visual Studio 2019 per ognuna delle applicazioni di esempio fornite. Se si usa un compilatore diverso, sarà necessario creare i file di progetto personalizzati o creare file ai fini della compilazione delle applicazioni di esempio oppure contattare il supporto tecnico all'indirizzo https://aka.ms/azrtos-support .

## <a name="guix-studio-constraints"></a>Vincoli di GUIX Studio

Lo strumento di progettazione dell'interfaccia utente di GUIX studio presenta diversi vincoli, come indicato di seguito:

- Viene visualizzato un massimo di 4 per progetto.
- Un massimo di 100.000 widget per ogni progetto di GUIX Studio.
- Un massimo di 100.000 risorse distinte, ad esempio, colori, tipi di carattere, pixelmaps, stringhe e così via.