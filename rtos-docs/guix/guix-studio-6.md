---
title: Codice generato da GUIX Studio
description: Dopo aver modificato le schermate e le risorse, GUIX Studio produce un set di file di output che possono essere incorporati nell'applicazione incorporata.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 78b1ec1eea3ec2fcae48c64ad15931f44f34538c876dc8a267c2b1a84234320a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785703"
---
# <a name="chapter-6-guix-studio-generated-code"></a>Capitolo 6: Codice generato da GUIX Studio

Dopo aver modificato le schermate e le risorse, GUIX Studio produce un set di file di output che possono essere incorporati nell'applicazione incorporata. I file di output vengono generati selezionando * Genera file **di risorse** _ e _ *_Genera_* specifiche * dalla Project menu. I file di codice sorgente del linguaggio "c" generati da GUIX Studio devono essere compilati e collegati al codice sorgente dell'applicazione incorporato. Se viene prodotto un file di risorse in formato binario, questo file deve essere programmato in un'area di archiviazione non volatile nella destinazione e la funzione API GUIX gx_binres_theme_install deve essere usata per installare le risorse binarie in fase di esecuzione.

Il codice dell'applicazione incorporata dell'utente fa riferimento al codice generato da GUIX Studio. Inoltre, il codice generato da GUIX Studio prevede che tutte le funzioni personalizzate di disegno, gestione degli eventi e allocazione di memoria dei widget specificate nel progetto siano definite nel codice dell'applicazione incorporata dell'utente. In caso contrario, durante la compilazione dell'applicazione saranno presenti errori di collegamento.

> [!NOTE]
> L'utente non deve mai modificare il codice generato da GUIX Studio e deve opporsi a questa operazione. Tutte le modifiche dell'interfaccia utente devono essere apportate nel progetto GUIX Studio associato. In questo modo il progetto verrà sincronizzato con l'applicazione incorporata.

## <a name="generating-resource-files"></a>Generazione di file di risorse

I file di risorse generati da GUIX Studio contengono strutture di dati preimpostate che definiscono tutte le risorse di GUIX Studio (colori, tipi di carattere, pixelmap e stringhe), ovvero tutte le risorse definite nel ***Visualizzazione risorse*** del progetto. Questi file di risorse possono essere generati in codice sorgente o in formato binario.

Per impostazione predefinita, vengono generati due file, uno è un file di codice sorgente C standard e l'altro è un file di intestazione C che fornisce riferimenti esterni e costanti necessari al codice dell'applicazione per accedere alle risorse GUIX definite nel progetto. I nomi dei file hanno il formato seguente:

**{*project-name*}_resources.h**

**{*project-name*}_resources.c**

Ad esempio, i file di risorse creati per il progetto "***simple***" GUIX Studio sono:

**simple_resources.h**

**simple_resources.c**

La generazione dei file di risorse viene eseguita selezionando l'opzione * Genera file di **risorse** _ nell'opzione _*_Project_*_ menu. La destinazione dei file di risorse viene specificata nella finestra di dialogo _*_Configura_*_ Project, accessibile tramite l'opzione Configura _*_Project/Visualizza_*_ nella *_voce_* di menu _ Configura *.

Per le risorse Pixelmap e Font, è possibile specificare un nome file di output personalizzato per ogni mappa pixel e tipo di carattere nelle finestre di dialogo di modifica delle risorse associate. Questa funzionalità consente di inserire risorse molto grandi in file distinti, anziché inserire tutte le risorse in un file di output comune. Se non si specifica un nome file sottoposto a override per un tipo di carattere o una risorsa pixelmap, tali risorse vengono scritte nel file di risorse comune.

Se si preferisce usare le risorse binarie, è possibile specificare il formato di output s-record standard o non elaborato. Le risorse binarie non vengono compilate o collegate al codice dell'applicazione, ma vengono invece caricate in fase di esecuzione usando l'API gx_binres_them_load(). Questo servizio API crea tabelle di risorse che puntano alle risorse archiviate nella memoria non volatile. È quindi possibile installare queste risorse con una visualizzazione specifica usando gx_display_theme_install();

## <a name="generating-specification-code"></a>Generazione del codice di specifica

I file di specifica generati da GUIX Studio contengono tutto il codice C per creare l'interfaccia utente progettata in GUIX Studio. Questo codice fa anche riferimento ai file di risorse generati per questo progetto. Il codice dell'applicazione dell'utente effettua chiamate a questo codice per creare effettivamente gli oggetti dell'interfaccia utente definiti nel progetto. Inoltre, il codice dell'applicazione dell'utente contiene tutte le funzioni personalizzate di disegno dei widget, gestione degli eventi e allocazione di memoria specificate nel progetto. Per impostazione predefinita, vengono generati due file, uno è un file di codice sorgente C standard e l'altro è un file di intestazione C che fornisce riferimenti esterni e costanti necessari per il codice dell'applicazione per accedere alle specifiche di GUIX Studio. I nomi dei file hanno il formato seguente:

**{*project-name*}_specifications.h**

**{*project-name*}_specifications.c**

Ad esempio, i file di specifica creati per il progetto "***simple***" GUIX Studio sono:

**simple_specifications.h**

**simple_specifications.c**

La generazione dei file di specificaviene eseguita selezionando l'opzione * Genera file di specifica _ _*_nell'opzione_*_ Project menu. La destinazione dei file di specifica viene specificata nella finestra di dialogo _*_Configura Project,_*_ accessibile tramite l'opzione Configura _*_Project/Visualizza_*_ nella *_voce_* di menu _ Configura *.

## <a name="integrating-with-user-code"></a>Integrazione con il codice utente

L'integrazione dei file di risorse e specifiche generati da GUIX Studio è semplice, è sufficiente seguire questa procedura:

1. Copiare o rendere accessibili i file di risorse e specifiche tramite le impostazioni del percorso nell'ambiente di compilazione incorporato
2. Aggiungere tutti i file di risorse e specifiche al progetto IDE incorporato o al makefile
3. Assicurarsi che il codice incorporato dell'applicazione chiami le funzioni necessarie per inizializzare e creare l'interfaccia utente contenuta nei file resource e specification
4. Assicurarsi che il codice incorporato dell'applicazione contenga tutte le funzioni di disegno, gestione degli eventi e allocazione di memoria dei widget personalizzati necessarie
5. Compilare l'applicazione (compilazione e collegamento)
6. Eseguire l'applicazione.