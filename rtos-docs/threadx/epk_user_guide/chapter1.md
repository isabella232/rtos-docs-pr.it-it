---
title: Capitolo 1-Introduzione al kit del profilo di esecuzione
description: Questo capitolo contiene un'introduzione ad Azure RTO ThreadX Execution Profile Kit (EPK).
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d30676437535229ad5bdbca10dcc9ca009d6e74
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377618"
---
# <a name="chapter-1--introduction-to-the-execution-profile-kit"></a>Capitolo 1 Introduzione al kit del profilo di esecuzione

Il EPK (ThreadX Execution Profile Kit) fornisce un'infrastruttura per le applicazioni che consentono di tenere traccia dinamica del tempo di esecuzione per i thread, le routine del servizio di interrupt (ISRs) e le condizioni di sistema inattive. Questa operazione è particolarmente utile per l'ottimizzazione e l'ottimizzazione dell'applicazione per ottenere le prestazioni massime. Tuttavia, è anche un utile strumento di debug.

EPK si basa sugli \" hook \" incorporati nella logica di pianificazione di threadX nel codice dell'assembly chiamati sulla voce del thread, sulla chiusura del thread, sulla voce ISR e sull'uscita ISR. Le routine EPK calcolano l'intervallo di tempo tra questi eventi e archiviano l'ora Delta nelle variabili globali, nonché i membri del blocco di controllo **TX_THREAD** .

> [!NOTE]
> *Lo sviluppatore può modificare o persino sostituire queste funzioni hook con la propria logica per abilitare o disabilitare i pin di i/O in modo da fornire visibilità hardware a un'applicazione threadX in esecuzione*.

## 

## <a name="epk-requirements"></a>Requisiti di EPK

Per il funzionamento di EPK è necessario ThreadX 6,0 (o versione successiva). Il EPK richiede anche una \" ragionevole \" risoluzione, incrementando l'origine del tempo hardware. La risoluzione più ragionevole sarebbe in genere qualcosa in una scala microsecondo. Se la risoluzione è troppo grande, il numero massimo di contatori EPK sarà troppo rapido. Viceversa, se la risoluzione è troppo piccola, non è possibile un intervallo preciso. L'origine del tempo applicazione è definita in ***tx_execution_profile. h** _ dalla macro _ * TX_EXECUTION_TIME_SOURCE * *.

Il compilatore C deve supportare il tipo \" unsigned long long \" per i contatori totali senza segno a 64 bit. Inoltre, EPK presuppone che le variabili globali siano inizializzate dal codice di avvio della fase di esecuzione del compilatore. In caso contrario, le variabili globali definite in ***tx_execution_profile. c*** devono essere inizializzate su 0 dall'applicazione.

## <a name="epk-installation"></a>Installazione di EPK

Per installare il EPK ThreadX, attenersi alla procedura seguente e ricompilare l'intera applicazione e la libreria ThreadX.

1. Includere i file di origine EPK (***tx_execution_profile. h** _ e _*_tx_execution_profile. c_*_) nel progetto di compilazione della libreria threadX. Questi file possono trovarsi nel [repository threadX di Azure RTO](<https://github.com/azure-rtos/threadx>) nella cartella _ *_Utility/Execution_Profile_**).

1. In ***tx_port. h** _ definire la macro _ *TX_THREAD_EXTENSION_3** come indicato di seguito.
```
    #define TX_THREAD_EXTENSION_3 unsigned long long tx_thread_execution_time_total; \
    unsigned long tx_thread_execution_time_last_start;
```

3. Definire la macro **TX_EXECUTION_TIME_SOURCE** in **_tx_execution_profile. h_** per eseguire il mapping all'origine del tempo hardware.

1. Verificare che l'ambiente di compilazione definisca **TX_ENABLE_EXECUTION_CHANGE_NOTIFY** in modo che gli hook di pianificazione vengano chiamati dal codice dell'assembly threadX.

1. Se si vuole usare l'origine ora 64 bit, vedere il file ***tx_execution_profile. h*** per istruzioni su come eseguire questa operazione.

1. Ricompilare l'intera libreria e l'applicazione in modo che tutte le opzioni siano compilate correttamente.

A questo punto è possibile usare EPK con l'applicazione.

##  <a name="epk-example"></a>Esempio di EPK 

Di seguito è riportato un esempio di EPK usato in una dimostrazione ThreadX standard, configurato con un'origine timer a 32 bit che incrementa 7,2 volte al microsecondo. 

La macro **TX_EXECUTION_TIME_SOURCE** viene definita per prelevare il registro timer mappato alla memoria in 0xE0001004, come indicato di seguito.
```
(EXECUTION_TIME_SOURCE_TYPE) \*((ULONG \*) 0xE0001004)
```

Se si lascia che la dimostrazione venga eseguita per cinque secondi, vengono restituiti i risultati seguenti.

![Risultati dell'esecuzione della demo.](media/demo_results.png)

Poiché la dimostrazione ThreadX standard non ha tempo di inattività (i thread 1 e 2 vengono eseguiti in modo continuo), il EPK segnala correttamente zero per il tempo di inattività. I valori di tempo totale ISR e thread possono essere divisi per 7,2 per derivare i microsecondi per ogni categoria di esecuzione. Il EPK fornisce anche le API per accedere a queste informazioni (vedere il [capitolo 2](chapter2.md)).