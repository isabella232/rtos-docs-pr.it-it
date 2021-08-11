---
title: Manuale dell'utente di GUIX Studio
description: Questa guida fornisce informazioni complete su GUIX Studio, l'ambiente di sviluppo rapido dell'interfaccia utente basato su Microsoft Windows progettato specificamente per la libreria di runtime GUIX di Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 2c36fb794816cb1acd51ec81f48c0dabe509336f27914050b6206f19bf8ceeff
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116789834"
---
# <a name="chapter-1-introduction-to-azure-rtos-guix-studio"></a>Capitolo 1: Introduzione a Azure RTOS GUIX Studio

Azure RTOS GUIX Studio è un ambiente di sviluppo rapido dell'interfaccia utente basato su Microsoft Windows progettato appositamente per la libreria di runtime GUIX di Microsoft.

Gli sviluppatori di interfaccia utente incorporata possono usare la finestra di progettazione dello schermo GUIX Studio WYSIWYG per creare e aggiornare rapidamente l'interfaccia utente incorporata usando l'ambiente di run-time GUIX. Le progettazioni di GUIX Studio vengono salvate e gestite in un file di progetto di GUIX Studio con estensione gxp. Quando la progettazione è pronta per l'esecuzione nella destinazione, GUIX Studio genera codice C che contiene tutte le informazioni e il codice necessari sull'interfaccia utente.

## <a name="guix-studio-requirements"></a>Requisiti di GUIX Studio

Per funzionare correttamente, GUIX Studio di Microsoft *richiede Windows XP* (o versione superiore). Il sistema deve avere almeno 200 MB di RAM, 2 GB di spazio disponibile su disco rigido e una visualizzazione minima di 1024x768 con 256 colori. Inoltre, l'applicazione incorporata deve essere in esecuzione *in ThreadX/GUIX V6.0* o versione successiva.

Per poter compilare ed eseguire l'applicazione incorporata dell'interfaccia utente come eseguibile autonomo di Microsoft Windows, è necessario anche un compilatore o un ambiente di compilazione in grado di compilare codice sorgente C per produrre un eseguibile di Microsoft Windows. Il pacchetto di valutazione incluso in GUIX Studio include anche Visual Studio soluzioni e file di progetto compatibili con 2019 per ognuna delle applicazioni di esempio fornite. Se si usa un compilatore diverso, sarà necessario creare file di progetto personalizzati o creare file allo scopo di compilare le applicazioni di esempio oppure contattare il supporto tecnico all'indirizzo https://aka.ms/azrtos-support .

## <a name="guix-studio-constraints"></a>Vincoli di GUIX Studio

Lo strumento di progettazione dell'interfaccia utente di GUIX Studio presenta diversi vincoli, come indicato di seguito:

- Un massimo di 4 viene visualizzato per ogni progetto.
- Un massimo di 100.000 widget per progetto GUIX Studio.
- Un massimo di 100.000 risorse distinte, ad esempio colori, tipi di carattere, mappe pixel, stringhe e così via.