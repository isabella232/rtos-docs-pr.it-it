---
title: Appendice F-GUIX RTO binding Services
description: Informazioni sui servizi di binding RTO di GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1d94dbb9d7d53ec3e1900188142974cc981dfea9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823174"
---
# <a name="appendix-f---guix-rtos-binding-services"></a>Appendice F-GUIX RTO binding Services

GUIX richiede servizi thread o attività, mutex, coda di eventi e servizi di temporizzazione che forniscono il RTO sottostante. Per impostazione predefinita, GUIX è configurato per usare il sistema operativo ThreadX in tempo reale per fornire questi servizi. Per trasferire GUIX a un altro sistema operativo, lo sviluppatore deve # definire la direttiva del pre-processore GX_DISABLE_THREADX_BINDING e ricompilare la libreria GUIX per rimuovere le dipendenze ThreadX. Inoltre, lo sviluppatore dovrà fornire le seguenti definizioni di macro e funzioni di supporto. Esempi di queste definizioni di macro e funzioni di supporto sono disponibili nei file gx_system_rtos_bind. h e gx_system_rtos_bind. c, che forniscono un esempio di integrazione RTO generica.

Macro di integrazione di sistema:

**GX_RTOS_BINDING_INITIALIZE**

Questa macro viene richiamata durante l'inizializzazione del sistema. È necessario definire la macro per chiamare qualsiasi funzione necessaria per preparare i servizi di sistema RTO o le risorse RTO prima di usare. Si tratta dell'opportunità di associazione per preparare le risorse RTO che GUIX utilizzerà.

**GX_SYSTEM_THREAD_START**

Questa macro viene richiamata quando l'attività o il thread di GUIX deve iniziare l'esecuzione. Questa macro deve essere definita per chiamare una funzione che avvierà il thread GUIX in esecuzione. Il punto di ingresso al thread GUIX viene passato alla funzione chiamata. La firma della funzione chiamata deve essere

**UINT *function_name*(void (thread_entry_point) (void));**

Questa funzione deve restituire GX_SUCCESS se il thread è stato avviato correttamente oppure GX_FAILURE.

**GX_EVENT_PUSH**

Questa macro viene richiamata per eseguire il push di un evento nella coda degli eventi FIFO utilizzata da GUIX. Quando si esegue il porting a un nuovo RTO, è responsabilità dell'utente implementare questa coda di eventi in modo thread-safe. GX_EVENT le strutture devono essere copiate in questa coda e copiate fuori dalla coda, ad esempio una coda di GX_EVENT puntatori non funzionerà, poiché gli eventi GUIX possono essere variabili automatiche dalla visualizzazione del producer di eventi. La firma della funzione chiamata da questa macro deve essere:

**UINT *function_name* (GX_EVENT *event_ptr);**

Questa funzione deve restituire GX_SUCCESS se l'evento viene inserito nella coda degli eventi, in caso contrario deve restituire GX_FAILURE.

**GX_EVENT_POP**

Questa macro viene richiamata per rimuovere l'evento Head (meno recente) dalla coda degli eventi GUIX e copiarlo nel percorso richiesto. Questa funzione deve essere in grado di bloccare o attendere un evento se non sono presenti eventi nella coda degli eventi. La firma della funzione richiamata da questa macro deve essere

UINT function_name (GX_EVENT * put_event, GX_BOOL Wait)

Se il parametro Wait = = GX_TRUE, la funzione non deve essere restituita fino a quando non viene fornito un evento. Se il parametro Wait è GX_FALSE, la funzione deve restituire immediatamente con o senza un evento.

Se un evento viene recuperato dalla coda, deve essere copiato nel percorso put_event e lo stato restituito è GX_SUCCESS. In caso contrario, lo stato restituito deve essere GX_FAILURE.

**GX_EVENT_FOLD**

Questa macro viene richiamata da GUIX per ridurre un evento nella coda degli eventi FIFO. La riduzione di un evento significa che se un evento dello stesso tipo esiste già nella coda, tale voce è Update per contenere il payload del nuovo evento. Se un evento esistente dello stesso tipo non viene trovato nella coda, viene eseguito il push di un nuovo evento nella coda. 

Per le associazioni che non possono implementare la funzionalità di riduzioni degli eventi, è accettabile richiamare semplicemente il GX_EVENT_PUSH.

**GX_TIMER_START**

Questa macro viene richiamata quando GUIX deve ricevere un input timer periodico. Questa macro dovrebbe richiamare un servizio che avvia il servizio timer periodico di RTO di basso livello. Se non è possibile arrestare e avviare facilmente il servizio timer RTO, è accettabile, ma meno efficiente, lasciare il servizio in esecuzione in qualsiasi momento.

Quando il servizio timer RTO di basso livello scade periodicamente, è necessario che l'associazione chiami la funzione di sistema GUIX _gx_system_timer_expiration (0); La chiamata periodica di questa funzione è l'elemento che guida i servizi timer del timer GUIX di alto livello.

**GX_TIMER_STOP**

Questa macro viene richiamata quando GUIX non necessita più di un timer periodico (ovvero non è in esecuzione alcun timer GUIX attivo). Se non è possibile arrestare e avviare facilmente il servizio timer RTO, è accettabile, ma meno efficiente, lasciare l'esecuzione di questo servizio in qualsiasi momento e definire questa macro per non eseguire alcuna operazione.

**GX_SYSTEM_MUTEX_LOCK**

Questa macro viene richiamata da GUIX durante le sezioni di codice critiche per impedire l'esecuzione di un'altra attività da svuotamento e la modifica di strutture di dati comuni, causando potenzialmente il danneggiamento. Questa macro deve chiamare una funzione che implementa il servizio di blocco di risorse RTO appropriato.

Se non si usano mai servizi API GUIX all'esterno del thread GUIX, è possibile definire questa macro per non eseguire alcuna operazione.

**GX_SYSTEM_MUTEX_UNLOCK**

Questa macro viene richiamata alla fine delle sezioni di codice critiche e dovrebbe sbloccare la risorsa GUIX usando il servizio RTO sottostante appropriato. Se non si usano mai servizi API GUIX all'esterno del thread GUIX, è possibile definire questa macro per non eseguire alcuna operazione.

**GX_SYSTEM_TIME_GET**

Questa macro deve chiamare una funzione che restituisce l'ora di sistema corrente è "i cicli di sistema", che è in genere il numero di interrupt del timer di basso livello che si sono verificati dall'avvio del sistema. Questo servizio viene usato per calcolare la velocità di penna dell'evento Touch per i movimenti di input di tocco. La firma della funzione richiamata da questa macro deve essere:

***Function_name* ulong (void);**

**GX_CURRENT_THREAD**

Questa macro viene richiamata per identificare il thread attualmente in esecuzione. Il servizio chiamato da questa macro deve restituire un valore void *, vale a dire che il tipo di dati utilizzato dal sistema operativo per identificare il thread di esecuzione corrente deve essere eseguito il cast a void * per essere restituito a GUX.

Un esempio completo di associazione RTO generica viene implementato nel file gx_system_rtos_bind. h e gx_system_rtos_bind. c.