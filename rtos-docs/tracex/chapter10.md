---
title: Capitolo 10 - Eventi utente del cliente
description: Questo capitolo contiene una descrizione di come creare eventi definiti dall'utente e icone personalizzate e campi di informazioni per tali eventi.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: b287436fb7f61df846bb0c84d910f5c095bc1f8f6635305e97c9e8b7aab64655
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790382"
---
# <a name="chapter-10---customer-user-events"></a>Capitolo 10 - Eventi utente del cliente

Questo capitolo contiene una descrizione di come creare eventi definiti dall'utente e icone personalizzate e campi di informazioni per tali eventi. Questo capitolo include le sezioni seguenti: 

## <a name="inserting-user-defined-events"></a>Inserimento User-Defined eventi

ThreadX consente agli sviluppatori di registrare i propri eventi definiti dall'utente, fornendo informazioni ancora più utili che possono essere visualizzate graficamente da TraceX. I numeri di evento definiti dall'utente sono diversi da

**TX_TRACE_USER_EVENT_START** (4096) fino **TX_TRACE_USER_EVENT_END** (65535), inclusi. La posizione degli eventi nel buffer di traccia viene eseguita ***tramite*** tx_trace_user_event_insert , definito nel capitolo 5. Nell'esempio seguente vengono chiamate due chiamate per inserire due eventi definiti dall'utente nel buffer di traccia corrente nella destinazione, ad esempio l'evento definito dall'utente 4096 e l'evento 4098:

```c
tx_trace_user_event_insert(4096, 1, 2, 3, 4);
tx_trace_user_event_insert(4098,0x100,0x200,0x300,0x400);
```

## <a name="default-display-of-user-defined-events"></a>Visualizzazione predefinita degli User-Defined predefiniti

![Icona dell'evento definito dall'utente](./media/user-guide/tx-events/image0.png)

Per impostazione predefinita, TraceX visualizza tutti gli eventi utente con un'icona evento definita dall'utente predefinita, come descritto nel capitolo 6. La figura 28 mostra l'icona dell'evento definita dall'utente predefinita per gli eventi 452 e 453, che sono stati inseriti nel buffer eventi tramite gli esempi precedenti ***tx_trace_user_event_insert*** eventi.

![Screenshot della visualizzazione predefinita degli eventi definiti dall'utente. ](./media/user-guide/10.1.png)
 **FIGURA 28**

Sono disponibili informazioni dettagliate anche per gli eventi definiti dall'utente. La figura 28 mostra le informazioni dettagliate sull'evento 452, che ha il numero di evento 4096 e mostra i quattro campi di informazioni specificati.

![Screenshot della visualizzazione dettagliata degli eventi definiti dall'utente. ](./media/user-guide/10.2.png)
 **FIGURA 29**

## <a name="defining-custom-user-defined-event-icons"></a>Definizione di icone di User-Defined personalizzate

TraceX offre inoltre all'utente la possibilità di creare icone di eventi personalizzate definite dall'utente e etichette di campo di informazioni personalizzate. Questa funzionalità viene ottenuta aggiungendo le specifiche dell'icona dell'evento al file **di configurazione * tracex_custom.trxc** _. Questo file si trova nella sottodirectory _ *_CustomEvents_** della directory di installazione di TraceX definita dall'utente, che per impostazione predefinita è c:\Azure_RTOS\TraceX. Nella figura 30 è illustrato un percorso di directory di esempio.

![Screenshot di un percorso di directory di esempio. ](./media/user-guide/custom_events_folder.png)
 **FIGURA 30**

Il file ***tracex_custom.trxc*** è un semplice file di testo ASCII contenente zero o più definizioni di eventi personalizzati. Di seguito è riportato il formato del file.

```c
//Comments
**Start **
[custom event definition(s)] **End **
```

Ogni riga tra Start e End viene usata per definire un singolo evento personalizzato. TraceX fornisce una versione modello di questo file senza eventi personalizzati definiti (niente tra le etichette "Start&quot; ed &quot;End"). Il formato di una definizione di evento personalizzato è il seguente:

**number, name, abbreviation, top_color, bottom_color, label1, label2, label2, label4**

dove:

- number: definisce il numero di evento definito dall'utente, compreso tra 4096 e 65535, inclusi.</th>
- name: definisce il nome logico per l'evento definito dall'utente.</td>
- abbreviazione: definisce l'abbreviazione di evento definita dall'utente di due lettere.</td>
- top_color: definisce il valore RGB per la metà superiore dell'icona, ovvero un numero a tre cifre tra parentesi. Alcune definizioni RGB tipiche sono
  - BLACK = (0,0,0)       
  - BIANCO = (255.255.255)
  - RED = (255,0,0)     
  - VERDE = (0,255,0)     
  - BLU = (0,0,255)     
  - GIALLO = (255.255,0)   
  - CIANO = (0,255,255)   
  - MAGENTA = (255,0,255)   
  L'uso della specifica RBG offre all'utente un'ampia gamma di colori per ogni icona definita dall'utente. Per altre informazioni sulla definizione dei colori RBG, vedere: https://en.wikipedia.org/wiki/RGB#Digital_representations
- botton_color: definisce il valore RGB per la metà inferiore dell'icona, ovvero un numero a tre cifre tra parentesi.
- label1: etichetta per ***info_field_1** _, come specificato nella chiamata _ *_tx_trace_user_event_insert_** .
- label2: etichetta per ***info_field_2** _, come specificato nella chiamata _ *_tx_trace_user_event_insert_** .
- label3: etichetta per ***info_field_3** _, come specificato nella chiamata _ *_tx_trace_user_event_insert_** .
- label4: etichetta per ***info_field_4** _, come specificato nella chiamata _ *_tx_trace_user_event_insert_** .

Le definizioni di esempio per ognuno dei due eventi definiti dall'utente usati in questo capitolo sono illustrate nella figura 10.4. La prima definizione è per l'evento 4096 alla riga 5 del file *** tracex_custom.trxc** _. Questa definizione assegna all'evento 4096 definito dall'utente il nome _*First_User_Event***, specifica un'abbreviazione di due lettere fe **,** rende rossa la parte superiore dell'icona, la parte inferiore dell'icona verde e assegna ai campi informazioni il nome **First_Info1**, **First_Info2**, **First_Info3** e **First_Info4**. L'evento definito dall'utente 4098 viene definito in modo analogo alla riga 6 di **_tracex_custom.trxc_**.

![Screenshot delle definizioni di esempio per gli eventi definiti dall'utente. ](./media/user-guide/10.4.png)
 **FIGURA 31**

Poiché il file *** tracex_custom.trxc** _ viene letto da TraceX durante l'inizializzazione, TraceX deve essere chiuso e riavviato prima che le definizioni delle icone personalizzate possano essere applicate. La figura 32 mostra la visualizzazione traceX degli eventi definiti dall'utente 452 e 453 con le icone degli eventi personalizzati definite in _*_tracex_custom.trxc_**.

![Screenshot della visualizzazione TraceX degli eventi definiti dall'utente con le icone degli eventi personalizzati. ](./media/user-guide/10.5.png)
 **FIGURA 32**

Le informazioni aggiuntive nella definizione dell'evento personalizzato vengono visualizzate quando l'evento selezionato usa un doppio clic, il passaggio del mouse o il pulsante dell'evento corrente. La figura 33 mostra la selezione con doppio clic sull'evento 452. Il nome dell'evento e i campi di informazioni corrispondono tutti alla definizione di esempio aggiunta ***a tracex_custom.trxc***.

![Screenshot della selezione con doppio clic su un evento. ](./media/user-guide/10.6.png)
 **FIGURA 33**
