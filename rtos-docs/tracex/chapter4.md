---
title: Capitolo 4-analisi delle prestazioni di TraceX in Azure RTO
description: Questo capitolo descrive lo strumento di analisi delle prestazioni di Azure RTO TraceX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 6cf1b5bd5349efd97c3afc8a9e7f57f477f06f8f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823441"
---
# <a name="chapter-4---azure-rtos-tracex-performance-analysis"></a>Capitolo 4-analisi delle prestazioni di TraceX in Azure RTO

Questo capitolo descrive lo strumento di analisi delle prestazioni TraceX di Azure RTO:

## <a name="performance-analysis"></a>Analisi delle prestazioni

TraceX fornisce l'analisi delle prestazioni incorporata dei file di traccia. *Sono prontamente* disponibili informazioni quali il *profilo di esecuzione*, i *servizi più diffusi*, l' *utilizzo dello stack di thread* e varie *statistiche sulle prestazioni,* incluse le statistiche FILEX e NETX. Queste informazioni sono disponibili tramite la voce di menu ***Visualizza*** . 


## <a name="execution-profile"></a>Profilo di esecuzione

Selezionando il pulsante ***Genera profilo di esecuzione** _ o _*_Visualizza-esecuzione_*_ profilo viene visualizzato il profilo di esecuzione TraceX per il file di traccia attualmente caricato. Il profilo di esecuzione associato alla traccia dimostrativa ThreadX di esempio è illustrato in _ * figura 19 * *.

![Screenshot del profilo di esecuzione associato alla traccia dimostrativa di ThreadX di esempio.](./media/user-guide/execution_profile.png)

**FIGURA 19**

L'esempio illustrato nella **Figura 19** indica che quasi il 45% del tempo di elaborazione si trova all'interno del **_thread 2_*_ e quasi il 51% del tempo di elaborazione si trova all'interno di _*_thread 1_** questo è logico poiché la maggior parte della traccia Mostra i thread che inviano e ricevono messaggi. In questo esempio, i contesti di esecuzione rimanenti hanno solo una piccola quantità di tempo di esecuzione.

## <a name="popular-services"></a>Servizi più diffusi

Selecting ***View->Popular Services** _ presenta i servizi più diffusi nel file di traccia attualmente caricato. Per impostazione predefinita, queste informazioni vengono visualizzate per l'intero sistema. Tuttavia, sono disponibili anche i servizi più diffusi per thread specifici. I servizi più diffusi nella traccia dimostrativa ThreadX di esempio sono illustrati in _ * figure 20 * *.

![Screenshot dei servizi più diffusi nella traccia dimostrativa ThreadX di esempio.](./media/user-guide/popular_services.png)

**FIGURA 20**

L'esempio illustrato nella **Figura 20** indica che **_tx_queue_send_*_ e _*_tx_queue_receive_** sono i due servizi più diffusi in questa traccia. Questo comportamento è coerente con il comportamento della dimostrazione ThreadX standard da cui questa traccia è stata acquisita.

Per questa analisi è possibile selezionare thread specifici usando l'elenco di selezione a discesa nella parte superiore della finestra. **Nella figura 21** è illustrata questa analisi per il **_thread 3_**.

![Screenshot dell'analisi per un TraceX Popular Services.](./media/user-guide/popular_services_thread3.png)

**FIGURA 21**

## <a name="thread-stack-usage-analysis-for-thread-3"></a>Utilizzo dello stack di thread ![Analisi per il thread 3.](./media/user-guide/screen_shot_17.png)

Selezionando il pulsante ***genera utilizzo stack thread** _ o _*_Visualizza-> utilizzo stack thread_*_ viene visualizzato l'utilizzo dello stack per ogni thread nel file di traccia. Questa operazione viene eseguita da ThreadX, incluso il puntatore dello stack del thread corrente in molte delle voci di traccia del file. Un utilizzo dello stack pari al 100% indica che si è verificato un overflow dello stack ed è necessario correggerlo nell'applicazione. Se non è presente alcuna esecuzione del thread in questo file di traccia, l'utilizzo dello stack per il thread viene visualizzato allo 0%. L'utilizzo dello stack di thread nella traccia dimostrativa ThreadX di esempio è illustrato in _ * figura 22 * *.

![Screenshot dell'utilizzo dello stack di thread TraceX.](./media/user-guide/thread_stack_usage.png)

**FIGURA 22**

Nell'esempio illustrato nella **Figura 22** viene indicato che la maggior parte dei thread in questa traccia ha un utilizzo dello stack compreso tra il 9% e il 12%.

## <a name="performance-statistics"></a>Statistiche sulle prestazioni

Selezionando il pulsante ***genera statistiche prestazioni** _ o _ *_Visualizza-> statistiche prestazioni_** vengono visualizzate le statistiche sulle prestazioni del file di traccia attualmente caricato. Per impostazione predefinita, queste informazioni vengono visualizzate per l'intero sistema. Tuttavia, le statistiche sulle prestazioni sono disponibili anche per ogni thread specifico.

Le statistiche sulle prestazioni della traccia dimostrativa ThreadX di esempio sono illustrate nella **Figura 23**.

![Screenshot delle statistiche sulle prestazioni di TraceX.](./media/user-guide/performance_statistics.png)

**FIGURA 23**

L'esempio illustrato nella **Figura 23** indica che sono presenti 18 cambi di contesto in questo file di traccia, oltre a cinque interruzioni di thread, a 16 sospensioni dei thread, a 19 riprese dei thread e a tre interruzioni. Non sono state trovate inversioni di priorità in questo file di traccia. Si noti che esistono due categorie di inversioni di priorità, ovvero *deterministiche* e non *deterministiche*. Le inversioni con priorità deterministica sono inversione di priorità in cui un thread è bloccato su un mutex di proprietà di un thread con priorità inferiore. Un'inversione di priorità non deterministica è la posizione in cui viene eseguito un thread con priorità inferiore differente durante un'inversione di priorità deterministica. In un secondo momento può causare un comportamento imprevisto dell'applicazione e deve essere studiato attentamente.

## <a name="filex-statistics"></a>Statistiche FileX

Selezionando ***View-> FILEX Statistics** _ vengono visualizzate le statistiche sulle prestazioni di filex del file di traccia attualmente caricato. Queste informazioni vengono visualizzate per l'intero sistema, su tutti aperti. oggetti/media. Le statistiche sulle prestazioni della traccia dimostrativa FileX di esempio sono visualizzate in _ * figura 24 * *.

![Screenshot delle statistiche di FileX.](./media/user-guide/filex_statistics.png)

**FIGURA 24**

L'esempio illustrato nella **Figura 27** indica che sono presenti 19. /media si apre, 19.. /media chiude, 19.. /Media Scarica, 18 letture directory, 19 Scritture directory e 18 mancati riscontri nella cache di directory. È possibile visualizzare le informazioni aggiuntivi scorrendo verso il basso nella finestra statistiche.

## <a name="netx-statistics"></a>Statistiche NetX

Selezionando ***View-NETX Statistics** _ vengono visualizzate le statistiche sulle prestazioni di NETX del file di traccia attualmente caricato. Queste informazioni vengono visualizzate per l'intero sistema. Le statistiche sulle prestazioni della traccia dimostrativa NetX di esempio sono illustrate in _ * figure 25 * *.

![Screenshot delle statistiche di NetX.](./media/user-guide/netx_statistics.png)

**FIGURA 25**

L'esempio illustrato nella **Figura 25** indica che non sono presenti eventi ARP, ping o UDP, ma sono stati inviati 30 pacchetti ip, 1.368 byte IP inviati, 30 pacchetti IP ricevuti e 1.360 byte IP ricevuti.

## <a name="trace-file-information"></a>Informazioni sul file di traccia

Selezionare ***Visualizza-> informazioni sul file di traccia** _ presenta alcune informazioni di base sul file di traccia aperto. Queste informazioni includono l'ordine dei byte del file, le dimensioni dell'origine dell'ora, il numero massimo di byte per ogni nome di oggetto e l'indirizzo di base di tutti i puntatori del file di traccia. _ *Figure 26** Visualizza le informazioni sul file di traccia per il file di traccia standard **_demo_threadx. TRX_** .

![Screenshot delle informazioni sul file TraceX.](./media/user-guide/trace_file_info.png)

**FIGURA 26**

## <a name="raw-trace-dump"></a>Dump traccia RAW

Selezionando ***View-> RAW Trace dump** _ viene visualizzata una finestra di dialogo per assegnare un nome al file contenente il dump di traccia non elaborato. Una volta immesso il nome e il percorso del file, TraceX compila il file di traccia non elaborato in formato testo e avvia _*_notepad.exe_*_ per visualizzarlo. _ *Figura 27** Visualizza il dump del file di traccia non elaborato per il file di traccia standard **_demo_threadx. TRX_** .

![Screenshot del dump di traccia non elaborato.](./media/user-guide/raw_trace_dump.png)

**FIGURA 27**
