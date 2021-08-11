---
title: Capitolo 4- Analisi Azure RTOS delle prestazioni tracex
description: In questo capitolo viene descritto il Azure RTOS di analisi delle prestazioni TraceX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 719f27ef54091e2db9eefa982ce0c27561079b5b3a254d3fd09cc46d8f66f252
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788638"
---
# <a name="chapter-4---azure-rtos-tracex-performance-analysis"></a>Capitolo 4- Analisi Azure RTOS delle prestazioni tracex

Questo capitolo descrive lo strumento Azure RTOS di analisi delle prestazioni TraceX:

## <a name="performance-analysis"></a>Analisi delle prestazioni

TraceX fornisce l'analisi delle prestazioni incorporata dei file di traccia. Informazioni quali il profilo *di* *esecuzione,* i servizi più diffusi, l'utilizzo *dello stack* di thread e varie statistiche sulle *prestazioni,* tra cui le statistiche FileX e NetX, sono immediatamente disponibili. Queste informazioni sono disponibili tramite la ***voce di*** menu Visualizza. 


## <a name="execution-profile"></a>Profilo di esecuzione

Selezionando il pulsante ***Genera profilo di** esecuzione _ o Visualizza _*_-Profilo_*_ di esecuzione viene presentato il profilo di esecuzione TraceX per il file di traccia attualmente caricato. Il profilo di esecuzione associato all'esempio di traccia dimostrativa ThreadX è illustrato nella _*Figura 19**.

![Screenshot del profilo di esecuzione associato alla traccia dimostrativa threadX di esempio.](./media/user-guide/execution_profile.png)

**FIGURA 19**

L'esempio illustrato nella figura **19** indica che quasi il 45% del tempo di elaborazione si trova all'interno del thread 2 _ e quasi ***il 51%* del tempo di elaborazione si trova all'interno di _ _thread 1._** Questo è logico perché la maggior parte della traccia mostra che questi thread inviano e ricevono messaggi. I contesti di esecuzione rimanenti hanno solo una piccola quantità di tempo di esecuzione in questo esempio.

## <a name="popular-services"></a>Servizi più diffusi

Se si seleziona ***Visualizza ->Popular Services** _ vengono presentati i servizi più diffusi nel file di traccia attualmente caricato. Per impostazione predefinita, queste informazioni vengono visualizzate per l'intero sistema. Tuttavia, sono disponibili anche i servizi più diffusi per thread specifici. I servizi più diffusi nella traccia dimostrativa di Esempio ThreadX sono illustrati nella _*Figura 20**.

![Screenshot dei servizi più diffusi nella traccia dimostrativa di Esempio ThreadX.](./media/user-guide/popular_services.png)

**FIGURA 20**

L'esempio illustrato **nella figura 20** indica che tx_queue_send _ e ***_*_tx_queue_receive_** sono i due servizi più diffusi in questa traccia. Questo comportamento è coerente con il comportamento della dimostrazione ThreadX standard da cui è stata acquisita questa traccia.

È possibile selezionare thread specifici per questa analisi usando l'elenco a discesa nella parte superiore di questa finestra. **La figura 21** mostra questa analisi per **_il thread 3._**

![Screenshot dell'analisi per i servizi più diffusi di TraceX.](./media/user-guide/popular_services_thread3.png)

**FIGURA 21**

## <a name="thread-stack-usage-analysis-for-thread-3"></a>Utilizzo dello stack di thread ![Analisi per il thread 3.](./media/user-guide/screen_shot_17.png)

Selezionando il pulsante ***Genera utilizzo stack** thread _ o Visualizza _*_->_*_ Utilizzo stack thread viene presentato l'utilizzo dello stack per ogni thread nel file di traccia. Questa operazione viene eseguita da ThreadX, incluso il puntatore dello stack di thread corrente in molte delle voci di traccia nel file. Un utilizzo dello stack del 100% indica che si è verificata un overflow dello stack e deve essere corretto nell'applicazione. Se non è presente alcuna esecuzione di thread all'interno di questo file di traccia, l'utilizzo dello stack per tale thread viene visualizzato allo 0%. L'utilizzo dello stack di thread nella traccia dimostrativa threadX di esempio è illustrato nella _*Figura 22**.

![Screenshot dell'utilizzo dello stack di thread TraceX.](./media/user-guide/thread_stack_usage.png)

**FIGURA 22**

L'esempio illustrato nella **figura 22** indica che la maggior parte dei thread in questa traccia ha un utilizzo dello stack compreso tra il 9% e il 12%.

## <a name="performance-statistics"></a>Statistiche sulle prestazioni

Selezionando il pulsante ***Genera statistiche** prestazioni _ o _ Visualizza *_-> Statistiche_* prestazioni * vengono visualizzate le statistiche sulle prestazioni del file di traccia attualmente caricato. Per impostazione predefinita, queste informazioni vengono visualizzate per l'intero sistema. Tuttavia, le statistiche sulle prestazioni sono disponibili anche per ogni thread specifico.

Le statistiche sulle prestazioni della traccia dimostrativa ThreadX di esempio sono illustrate **nella figura 23.**

![Screenshot delle statistiche sulle prestazioni di TraceX.](./media/user-guide/performance_statistics.png)

**FIGURA 23**

L'esempio illustrato nella figura **23** indica che sono presenti 18 commutatori di contesto in questo file di traccia, oltre a cinque interruzioni di thread, 16 sospensioni di thread, 19 ripresi di thread e tre interrupt. Non sono state trovate inversioni di priorità in questo file di traccia. Si noti che esistono due categorie di inversione di priorità, in altrettanti, *deterministici* *e non deterministici.* Le inversione di priorità deterministica sono inversione di priorità in cui un thread viene bloccato in un mutex di proprietà di un thread con priorità inferiore. Un'inversione di priorità non deterministica è la posizione in cui viene eseguito un thread con priorità inferiore diverso durante un'inversione di priorità deterministica. Più avanti può causare un comportamento di temporizzazione imprevisto nell'applicazione e deve essere esaminato con attenzione.

## <a name="filex-statistics"></a>Statistiche FileX

Selezionando ***Visualizza -> Statistiche FileX** _ vengono visualizzate le statistiche sulle prestazioni FileX del file di traccia attualmente caricato. Queste informazioni vengono visualizzate per l'intero sistema, in tutti i file aperti. Oggetti /media. Le statistiche sulle prestazioni della traccia dimostrativa FileX di esempio sono mostrate nella _*Figura 24**.

![Screenshot delle statistiche FileX.](./media/user-guide/filex_statistics.png)

**FIGURA 24**

L'esempio illustrato **nella figura 27** indica che sono presenti 19 . /media opens, 19 .. /media chiude, 19 .. /media flushes, 18 operazioni di lettura della directory, 19 scritture nella directory e 18 mancati riscontri nella cache della directory. Le informazioni aggiuntive possono essere visualizzate scorrendo verso il basso nella finestra delle statistiche.

## <a name="netx-statistics"></a>Statistiche NetX

Selezionando ***Visualizza -NetX Statistics** _ vengono visualizzate le statistiche sulle prestazioni NetX del file di traccia attualmente caricato. Queste informazioni vengono visualizzate per l'intero sistema. Le statistiche sulle prestazioni della traccia dimostrativa NetX di esempio sono illustrate nella _*Figura 25**.

![Screenshot delle statistiche NetX.](./media/user-guide/netx_statistics.png)

**FIGURA 25**

L'esempio illustrato nella figura **25** indica che non sono stati ricevuti eventi ARP, Ping o UDP, ma sono stati inviati 30 pacchetti IP, 1.368 byte IP inviati, 30 pacchetti IP ricevuti e 1.360 byte IP ricevuti.

## <a name="trace-file-information"></a>Informazioni sul file di traccia

Selezionando ***Visualizza -> informazioni sul file di traccia** _ vengono presentate alcune informazioni di base sul file di traccia aperto. Queste informazioni includono l'ordine dei byte del file, le dimensioni dell'origine ora, il numero massimo di byte per ogni nome di oggetto e l'indirizzo di base di tutti i puntatori del file di traccia. _ *Figura 26** mostra le informazioni sul file di traccia per il file **_di traccia demo_threadx.trx_** standard.

![Screenshot delle informazioni sul file TraceX.](./media/user-guide/trace_file_info.png)

**FIGURA 26**

## <a name="raw-trace-dump"></a>Dump di traccia non elaborato

Selezionando ***Visualizza -> dump di traccia** non elaborato _ viene visualizzata una finestra di dialogo per assegnare un nome al file contenente il dump di traccia non elaborato. Dopo aver immesso il nome e il percorso del file, TraceX compila il file di traccia non elaborato in formato testo e _*_notepad.exe_*_ per visualizzarlo. _ *Figura 27** mostra il dump del file di traccia non elaborato per il file **_di traccia demo_threadx.trx_** standard.

![Screenshot del dump di traccia non elaborato.](./media/user-guide/raw_trace_dump.png)

**FIGURA 27**
