---
title: Capitolo 10-eventi utente del cliente
description: Questo capitolo contiene una descrizione di come creare eventi definiti dall'utente e campi di informazioni e icone personalizzati per tali eventi.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 635c2d79922de9d5649bab841ae946cac862056c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823510"
---
# <a name="chapter-10---customer-user-events"></a>Capitolo 10-eventi utente del cliente

Questo capitolo contiene una descrizione di come creare eventi definiti dall'utente e campi di informazioni e icone personalizzati per tali eventi. In questo capitolo sono incluse le seguenti sezioni: 

## <a name="inserting-user-defined-events"></a>Inserimento di eventi User-Defined

ThreadX offre agli sviluppatori la possibilità di registrare gli eventi definiti dall'utente, fornendo informazioni ancora più utili che possono essere visualizzate graficamente da TraceX. I numeri di evento definiti dall'utente sono compresi tra

**TX_TRACE_USER_EVENT_START** (4096) tramite **TX_TRACE_USER_EVENT_END** (65535), inclusi. La posizione degli eventi nel buffer di traccia viene eseguita tramite la ***tx_trace_user_event_insert***, definita nel capitolo 5. Nell'esempio seguente viene eseguita una chiamata per inserire due eventi definiti dall'utente nel buffer di traccia corrente nella destinazione, ovvero l'evento definito dall'utente 4096 e l'evento 4098:

```c
tx_trace_user_event_insert(4096, 1, 2, 3, 4);
tx_trace_user_event_insert(4098,0x100,0x200,0x300,0x400);
```

## <a name="default-display-of-user-defined-events"></a>Visualizzazione predefinita degli eventi di User-Defined

![Icona evento definito dall'utente](./media/user-guide/tx-events/image0.png)

Per impostazione predefinita, TraceX Visualizza tutti gli eventi utente con l'icona di un evento predefinito definito dall'utente, come descritto nel capitolo 6. La figura 28 Mostra l'icona dell'evento predefinito definito dall'utente per gli eventi 452 e 453, che sono stati inseriti nel buffer degli eventi tramite gli esempi di ***tx_trace_user_event_insert*** precedenti.

![Screenshot della visualizzazione predefinita degli eventi definiti dall'utente. ](./media/user-guide/10.1.png)
 **Figura 28**

Sono inoltre disponibili informazioni dettagliate per gli eventi definiti dall'utente. La figura 28 Mostra le informazioni dettagliate sugli eventi per l'evento 452, che presenta il numero di evento 4096 e Mostra i quattro campi di informazioni specificati.

![Screenshot della visualizzazione dettagliata degli eventi definiti dall'utente. ](./media/user-guide/10.2.png)
 **Figura 29**

## <a name="defining-custom-user-defined-event-icons"></a>Definizione di icone evento User-Defined personalizzate

TraceX offre inoltre agli utenti la possibilità di creare icone personalizzate dell'evento definite dall'utente e etichette dei campi di informazioni personalizzate. Questa funzionalità viene eseguita aggiungendo le specifiche dell'icona dell'evento al file di configurazione ***tracex_custom. trxc** _. Questo file si trova nella sottodirectory _ *_CustomEvents_** della directory di installazione TraceX definita dall'utente, che per impostazione predefinita è C:\ Azure_RTOS \tracex. Un percorso di directory di esempio è illustrato nella figura 30.

![Screenshot di un percorso di directory di esempio. ](./media/user-guide/custom_events_folder.png)
 **Figura 30**

Il file di configurazione dell'evento personalizzato ***tracex_custom. trxc*** è un semplice file di testo ASCII che contiene zero o più definizioni di evento personalizzate. Di seguito è riportato il formato del file.

```c
//Comments
**Start **
[custom event definition(s)] **End **
```

Ogni riga tra inizio e fine viene utilizzata per definire un singolo evento personalizzato. TraceX fornisce una versione modello di questo file senza eventi personalizzati definiti (niente tra le etichette "Start" e "end"). Il formato di una definizione di evento personalizzata è il seguente:

**numero, nome, abbreviazione, top_color, bottom_color, Label1, Label2, Label2, label4**

dove:

- Number: definisce il numero di evento definito dall'utente, compreso tra 4096 e 65535, inclusi.</th>
- Nome: definisce il nome logico per l'evento definito dall'utente.</td>
- Abbreviazione: definisce l'abbreviazione di evento definito dall'utente di due lettere.</td>
- top_color: definisce il valore RGB per la metà superiore dell'icona, ovvero un numero di tre cifre tra parentesi. Alcune definizioni RGB tipiche sono
  - NERO = (0, 0, 0)       
  - BIANCO = (255.255.255)
  - ROSSO = (255, 0, 0)     
  - VERDE = (0255, 0)     
  - BLU = (0255)     
  - GIALLO = (255255, 0)   
  - CYAN = (0255.255)   
  - MAGENTA = (255, 0255)   
  L'uso della specifica RBG offre all'utente un'ampia gamma di colori per ogni icona definita dall'utente. Per ulteriori informazioni sulla definizione di colore RBG, vedere: https://en.wikipedia.org/wiki/RGB#Digital_representations
- botton_color: definisce il valore RGB per la metà inferiore dell'icona, ovvero un numero di tre cifre tra parentesi.
- Label1: etichetta per ***info_field_1** _, come specificato nella chiamata _ *_tx_trace_user_event_insert_**.
- Label2: etichetta per ***info_field_2** _, come specificato nella chiamata _ *_tx_trace_user_event_insert_**.
- Label3: etichetta per ***info_field_3** _, come specificato nella chiamata _ *_tx_trace_user_event_insert_**.
- Label4: etichetta per ***info_field_4** _, come specificato nella chiamata _ *_tx_trace_user_event_insert_**.

Le definizioni di esempio per ognuno dei due eventi definiti dall'utente usati in questo capitolo sono illustrate nella figura 10,4. La prima definizione è relativa all'evento 4096 alla riga 5 del file ***tracex_custom. trxc** _. Questa definizione fornisce un evento definito dall'utente 4096 il nome _ * First_User_Event * *, specifica un'abbreviazione di due lettere di **Fe**, rende la parte superiore dell'icona rossa, la parte inferiore dell'icona verde e denomina i campi informativi come **First_Info1**, **First_Info2**, **First_Info3** e **First_Info4**. L'evento 4098 definito dall'utente è definito in modo analogo alla riga 6 di **_tracex_custom. trxc_**.

![Screenshot delle definizioni di esempio per gli eventi definiti dall'utente. ](./media/user-guide/10.4.png)
 **Figura 31**

Poiché il file ***tracex_custom. trxc** _ viene letto da TRACEx durante l'inizializzazione, è necessario chiudere e riavviare TRACEx per rendere effettive le definizioni delle icone personalizzate. La figura 32 Mostra la visualizzazione TraceX degli eventi definiti dall'utente 452 e 453 con le icone di evento personalizzate definite in _ *_tracex_custom. trxc_* *.

![Screenshot della visualizzazione TraceX degli eventi definiti dall'utente con le icone dell'evento personalizzato. ](./media/user-guide/10.5.png)
 **Figura 32**

Le informazioni aggiuntive nella definizione di evento personalizzato vengono visualizzate quando si seleziona l'evento usando un doppio clic, un passaggio del mouse o facendo clic sul pulsante evento corrente. La figura 33 Mostra la selezione di doppio clic nell'evento 452. Il nome dell'evento e i campi delle informazioni corrispondono alla definizione di esempio aggiunta a ***tracex_custom. trxc***.

![Screenshot della selezione del doppio clic per un evento. ](./media/user-guide/10.6.png)
 **Figura 33**
