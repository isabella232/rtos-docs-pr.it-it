---
title: Appendice F - GuiX RTOS Binding Services
description: Informazioni sui servizi di associazione RTOS GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7928e1781be03969de25901ebbe728e6554e96befb59c860f4ea53663c28932d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784598"
---
# <a name="appendix-f---guix-rtos-binding-services"></a>Appendice F - GuiX RTOS Binding Services

GUIX richiede servizi di thread o attività, mutex, coda di eventi e servizi di temporizzazione che forniscono l'RTOS sottostante. Per impostazione predefinita GUIX è configurato per utilizzare il sistema operativo ThreadX in tempo reale per fornire questi servizi. Per convertire GUIX in un altro sistema operativo, lo sviluppatore deve # definire la direttiva preprocessore GX_DISABLE_THREADX_BINDING e ricompilare la libreria GUIX per rimuovere le dipendenze ThreadX. Inoltre, lo sviluppatore dovrà fornire le definizioni di macro e le funzioni di supporto seguenti. Esempi di queste definizioni di macro e funzioni di supporto sono disponibili nei file gx_system_rtos_bind.h e gx_system_rtos_bind.c, che forniscono un esempio di integrazione rtos generica.

Macro di Integrazione di sistema:

**GX_RTOS_BINDING_INITIALIZE**

Questa macro viene richiamata durante l'inizializzazione del sistema. La macro deve essere definita per chiamare qualsiasi funzione necessaria per preparare i servizi di sistema rtos o le risorse rtos prima dell'uso. Questa è l'opportunità dell'associazione di preparare le risorse rtos che GUIX userà.

**GX_SYSTEM_THREAD_START**

Questa macro viene richiamata quando l'attività o il thread GUIX deve iniziare l'esecuzione. Questa macro deve essere definita per chiamare una funzione che avvia l'esecuzione del thread GUIX. Il punto di ingresso al thread GUIX viene passato alla funzione chiamata. La firma della funzione chiamata deve essere

**UINT *function_name*(VOID (thread_entry_point)(VOID));**

Questa funzione deve restituire GX_SUCCESS se il thread viene avviato correttamente o GX_FAILURE.

**GX_EVENT_PUSH**

Questa macro viene richiamata per eseguire il push di un evento nella coda di eventi FIFO usata da GUIX. Quando si esegue il porting a un nuovo rtos, è responsabilità dell'utente implementare questa coda di eventi in modo thread-safe. GX_EVENT le strutture devono essere copiate in questa coda e copiate da questa coda, ad esempio una coda di puntatori GX_EVENT non funzionerà, poiché gli eventi GUIX possono essere variabili automatiche dalla visualizzazione del producer di eventi. La firma della funzione chiamata da questa macro deve essere:

**UINT *function_name* (GX_EVENT *event_ptr);**

Questa funzione deve restituire GX_SUCCESS se l'evento viene inserito nella coda degli eventi, in caso contrario deve restituire GX_FAILURE.

**GX_EVENT_POP**

Questa macro viene richiamata per rimuovere l'evento head (meno recente) dalla coda di eventi GUIX e copiarlo nel percorso richiesto. Questa funzione deve essere in grado di bloccare o attendere facoltativamente un evento se non sono presenti eventi nella coda eventi. La firma della funzione richiamata da questa macro deve essere

UINT function_name(GX_EVENT *put_event, GX_BOOL wait)

Se il parametro wait == GX_TRUE, la funzione non deve restituire finché non viene fornito un evento. Se il parametro wait è GX_FALSE, la funzione deve restituire immediatamente con o senza un evento .

Se un evento viene recuperato dalla coda, deve essere copiato nel percorso put_event e lo stato restituito è GX_SUCCESS. In caso contrario, lo stato restituito GX_FAILURE.

**GX_EVENT_FOLD**

Questa macro viene richiamata da GUIX per ripiegare un evento nella coda di eventi FIFO. La rimozione di un evento significa che se nella coda esiste già un evento dello stesso tipo, tale voce viene aggiornato per contenere il payload del nuovo evento. Se nella coda non viene trovato un evento esistente dello stesso tipo, viene inserito un nuovo evento nella coda. 

Per le associazioni che non possono implementare la funzionalità di fold degli eventi, è accettabile richiamare semplicemente il GX_EVENT_PUSH.

**GX_TIMER_START**

Questa macro viene richiamata quando GUIX deve ricevere un input timer periodico. Questa macro deve richiamare un servizio che avvia il servizio timer periodico RTOS di basso livello. Se il servizio timer RTOS non può essere arrestato e avviato facilmente, è accettabile ma meno efficiente lasciare il servizio in esecuzione in qualsiasi momento.

Quando il servizio timer RTOS di basso livello scade periodicamente, l'associazione deve chiamare la funzione di sistema GUIX _gx_system_timer_expiration(0); La chiamata periodica di questa funzione è la funzione che determina i servizi timer del widget del timer GUIX di alto livello.

**GX_TIMER_STOP**

Questa macro viene richiamata quando GUIX non richiede più un timer periodico, ovvero non sono in esecuzione timer GUIX attivi. Se il servizio timer RTOS non può essere arrestato e avviato facilmente, è accettabile ma meno efficiente lasciare il servizio in esecuzione in qualsiasi momento e definire questa macro per non eseguire alcuna operazione.

**GX_SYSTEM_MUTEX_LOCK**

Questa macro viene richiamata da GUIX durante le sezioni di codice critiche per impedire a un'altra attività di pre-svuotare e modificare strutture di dati comuni, causando potenzialmente un danneggiamento. Questa macro deve chiamare una funzione che implementa il servizio di blocco delle risorse RTOS appropriato.

Se non si utilizzano mai servizi API GUIX al di fuori del thread GUIX, è possibile definire questa macro per non eseguire alcuna operazione.

**GX_SYSTEM_MUTEX_UNLOCK**

Questa macro viene richiamata alla fine delle sezioni di codice critiche e deve sbloccare la risorsa GUIX usando il servizio RTOS sottostante appropriato. Se non si utilizzano mai servizi API GUIX al di fuori del thread GUIX, è possibile definire questa macro per non eseguire alcuna operazione.

**GX_SYSTEM_TIME_GET**

Questa macro deve chiamare una funzione che restituisce l'ora di sistema corrente è "tick di sistema", che in genere è il numero di interrupt timer di basso livello che si sono verificati dall'avvio del sistema. Questo servizio viene usato per calcolare la velocità della penna dell'evento tocco per i movimenti di input tocco. La firma della funzione richiamata da questa macro deve essere:

**ULONG *function_name*(VOID);**

**GX_CURRENT_THREAD**

Questa macro viene richiamata per identificare il thread attualmente in esecuzione. Il servizio chiamato da questa macro deve restituire void *, ovvero il tipo di dati usato dal sistema operativo per identificare il thread di esecuzione corrente deve essere eseguito il cast a void * per essere restituito a GUX.

Un esempio completo di un'associazione RTOS generica viene implementato nei file gx_system_rtos_bind.h e gx_system_rtos_bind.c