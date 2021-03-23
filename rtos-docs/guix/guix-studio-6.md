---
title: Codice generato da GUIX Studio
description: Al termine della modifica delle schermate e delle risorse, GUIX studio produce un set di file di output che possono essere incorporati nell'applicazione incorporata.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: f8868ec770aa8f7f35d2866b99e3eb8f501281a8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823033"
---
# <a name="chapter-6-guix-studio-generated-code"></a>Capitolo 6: codice generato da GUIX Studio

Al termine della modifica delle schermate e delle risorse, GUIX studio produce un set di file di output che possono essere incorporati nell'applicazione incorporata. I file di output vengono generati selezionando ***genera file di risorse** _ e _ *_genera specifiche_** dalla voce di menu progetto. I file di codice sorgente del linguaggio "c" generati da GUIX studio sono progettati per essere compilati e collegati al codice sorgente dell'applicazione incorporata. Se viene prodotto un file di risorse in formato binario, questo file deve essere programmato in un'area di archiviazione non volatile nella destinazione e la funzione API GUIX gx_binres_theme_install deve essere usata per installare le risorse binarie in fase di esecuzione.

Il codice dell'applicazione incorporata dell'utente fa riferimento al codice generato da GUIX Studio. Inoltre, il codice generato da GUIX studio prevede che nel codice dell'applicazione incorporata dell'utente siano definite tutte le funzioni personalizzate di disegno, gestione degli eventi e allocazione di memoria specificate nel progetto. In caso contrario, durante la compilazione dell'applicazione saranno presenti errori di collegamento.

> [!NOTE]
> L'utente non deve mai modificare il codice generato da GUIX studio e dovrebbe resistere a questa operazione. Tutte le modifiche all'interfaccia utente devono essere apportate nel progetto GUIX studio associato. Il progetto verrà mantenuto sincronizzato con l'applicazione incorporata.

## <a name="generating-resource-files"></a>Generazione di file di risorse

I file di risorse generati da GUIX Studio contengono strutture di dati preimpostate che definiscono tutte le risorse di GUIX Studio (colori, tipi di carattere, pixelmaps e stringhe), che sono in effetti tutte le risorse definite nel ***visualizzazione risorse*** del progetto. Questi file di risorse possono essere generati nel codice sorgente o in moduli binari.

Per impostazione predefinita, vengono generati due file, un file è un file di codice sorgente C standard e l'altro è un file di intestazione C che fornisce riferimenti esterni e costanti necessari per il codice dell'applicazione per accedere alle risorse GUIX definite nel progetto. I nomi dei file sono nel formato seguente:

**{*nome-progetto*} _resources. h**

**{*nome-progetto*} _resources. c**

Ad esempio, i file di risorse creati per il progetto "***Simple***" GUIX studio sono:

**simple_resources. h**

**simple_resources. c**

La generazione dei file di risorse viene eseguita selezionando l'opzione ***genera file di risorse** _ dall'opzione di menu _*_progetto_*_ . La destinazione dei file di risorse è specificata nella finestra di dialogo _*_Configura progetto_*_ , accessibile tramite l'opzione _*_Configura progetto/Visualizza_*_ nella voce di menu _ *_Configure_**.

Per le risorse Pixelmap e font, è possibile specificare un nome di file di output personalizzato per ogni Pixelmap e carattere nelle finestre di dialogo di modifica delle risorse associate. Questa funzionalità consente di inserire risorse di grandi dimensioni in file distinti, anziché inserire tutte le risorse in un unico file di output comune. Se non si specifica un nome file sottoposto a override per una risorsa di tipo carattere o Pixelmap, le risorse vengono scritte nel file di risorse comune.

Se si preferisce usare risorse binarie, è possibile specificare il formato di output di record s Raw o standard. Le risorse binarie non vengono compilate o collegate con il codice dell'applicazione, ma vengono invece caricate in fase di esecuzione tramite l'API gx_binres_them_load (). Questo servizio API compila le tabelle delle risorse che puntano alle risorse archiviate in memoria non volatile. È quindi possibile installare queste risorse con una visualizzazione specifica usando gx_display_theme_install ();

## <a name="generating-specification-code"></a>Generazione del codice di specifica

I file di specifica generati da GUIX Studio contengono tutto il codice C per creare l'interfaccia utente progettata in GUIX Studio. Questo codice fa anche riferimento ai file di risorse generati per questo progetto. Il codice dell'applicazione dell'utente effettuerà chiamate a questo codice per creare effettivamente gli oggetti dell'interfaccia utente definiti nel progetto. Inoltre, il codice dell'applicazione dell'utente contiene tutte le funzioni personalizzate di disegno, gestione degli eventi e allocazione di memoria specificate nel progetto. Per impostazione predefinita, vengono generati due file, un file è un file di codice sorgente C standard e l'altro è un file di intestazione C che fornisce riferimenti esterni e costanti necessari per il codice dell'applicazione per accedere alle specifiche di GUIX Studio. I nomi dei file sono nel formato seguente:

**{*nome-progetto*} _specifications. h**

**{*nome-progetto*} _specifications. c**

Ad esempio, i file di specifica creati per il progetto "***Simple***" GUIX studio sono:

**simple_specifications. h**

**simple_specifications. c**

La generazione dei file di specifica viene eseguita selezionando l'opzione ***genera file di specifiche** _ dall'opzione di menu _*_progetto_*_ . La destinazione dei file di specifica viene specificata nella finestra di dialogo _*_Configura progetto_*_ , accessibile tramite l'opzione _*_Configura progetto/Visualizza_*_ nella voce di menu _ *_Configure_**.

## <a name="integrating-with-user-code"></a>Integrazione con il codice utente

L'integrazione dei file di risorse e di specifiche generati da GUIX studio è semplice, attenersi semplicemente alla procedura seguente:

1. Copiare o rendere accessibili i file delle risorse e delle specifiche tramite le impostazioni del percorso all'ambiente di compilazione incorporato
2. Aggiungere tutti i file di risorse e di specifica al progetto IDE incorporato o al Makefile
3. Verificare che il codice incorporato dell'applicazione chiami le funzioni necessarie per inizializzare e creare l'interfaccia utente contenuta nei file delle risorse e delle specifiche
4. Verificare che il codice incorporato dell'applicazione contenga tutte le funzioni di disegno widget personalizzato, gestione eventi e allocazione di memoria
5. Compilare l'applicazione (compilazione e collegamento)
6. Eseguire l'applicazione.