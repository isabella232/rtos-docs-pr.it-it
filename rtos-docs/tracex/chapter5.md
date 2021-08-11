---
title: Capitolo 5- Generazione di buffer di traccia
description: Questo capitolo contiene una descrizione su come compilare un buffer Azure RTOS eventi TraceX e descrive anche il formato sottostante del buffer.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 7d5c90675728fc7e374d625f5a9ae27340268ca8398200c68fb7113a84aa2983
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801785"
---
# <a name="chapter-5---generating-trace-buffers"></a>Capitolo 5- Generazione di buffer di traccia

Questo capitolo contiene una descrizione su come compilare un buffer Azure RTOS eventi TraceX e descrive anche il formato sottostante del buffer.

## <a name="threadx-event-trace-support"></a>Supporto di Traccia eventi ThreadX

ThreadX fornisce il supporto predefinito della traccia eventi per tutti i servizi ThreadX, le modifiche dello stato dei thread e gli eventi definiti dall'utente. La funzionalità di traccia degli eventi ThreadX è progettata principalmente come strumento post-mortem per analizzare le ultime attività "n" nell'applicazione. Da queste informazioni, lo sviluppatore può individuare problemi e/o potenziali obiettivi di ottimizzazione.

TraceX visualizza graficamente il buffer di traccia eventi compilato da ThreadX. Di seguito viene descritto come compilare il buffer e viene descritto il formato sottostante del buffer.

## <a name="enabling-event-trace"></a>Abilitazione di Traccia eventi

Per abilitare la traccia eventi, definire le costanti timestamp, compilare la libreria ThreadX con **TX_ENABLE_EVENT_TRACE** definito e abilitare la traccia chiamando la **funzione tx_trace_enable.**

## <a name="defining-time-stamp-constants"></a>Definizione di Time-Stamp costanti

Le costanti timestamp sono progettate per fornire allo sviluppatore il controllo sul timestamp usato nelle voci di traccia degli eventi. Le due costanti timestamp e i relativi valori predefiniti sono i seguenti:

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ++_tx_trace_simulated_time
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK   0xFFFFFFFFUL
#endif
```

Le costanti precedenti sono definite in **tx_port.h** e creano un timestamp "fittizio" che viene semplicemente incrementato di uno per ogni evento. Di seguito è riportato un esempio di una definizione timestamp effettiva:

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ((ULONG) 0x0x13000004)
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK 0xFFFFFFFFUL
#endif
```

Le costanti precedenti specificano un timer a 32 bit ottenuto leggendo l'indirizzo 0x13000004. La maggior parte dei timestamp specifici dell'applicazione deve essere impostata in modo simile.

## <a name="exporting-the-trace-buffer"></a>Esportazione del buffer di traccia

TraceX richiede il buffer di traccia in un formato di file binario, Intel HEX o Motorola S-Record nell'host. Il modo più semplice per eseguire questa operazione è arrestare la destinazione e indicare al debugger di eseguire il dump dell'area di memoria fornita tx_trace_enable funzione ***in*** un file nell'host.

> [!WARNING]
>***Prestare attenzione a non arrestare la destinazione all'interno di un codice di raccolta di tracce. Questa operazione può causare informazioni di traccia non valide. Se il programma viene interrotto all'interno di ThreadX, è meglio eseguire un'istruzione alla macro di inserimento della traccia prima di eseguire il dump del buffer di traccia.***

> [!IMPORTANT]
> *L'Appendice D illustra come eseguire il dump del buffer di traccia da un'ampia gamma di strumenti di sviluppo.*

## <a name="extended-event-trace-api"></a>API traccia eventi estesi

Quando ThreadX viene compilato **TX_ENABLE_EVENT_TRACE** definito, le nuove API di traccia degli eventi seguenti sono disponibili per l'applicazione:

- tx_trace_enable: Abilitare *la traccia eventi*
- tx_trace_event_filter: *Filtrare gli eventi specificati*
- tx_trace_event_unfilter: Rimuovere *il filtro degli eventi specificati*
- tx_trace_disable: *Disabilitare la traccia eventi*
- tx_trace_isr_enter_insert: Inserire *l'evento di traccia enter ISR*
- tx_trace_isr_exit_insert: Inserire *l'evento di traccia di uscita isr*
- tx_trace_buffer_full_notify: *Registrare il callback completo dell'applicazione del buffer di traccia*
- tx_trace_user_event_insert: Inserire *un evento utente*

### <a name="tx_trace_enable"></a>tx_trace_enable

Abilitare la traccia eventi

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_enable (VOID *trace_buffer_start,
     ULONG trace_buffer_size, ULONG registry_entries);
```

#### <a name="description"></a>Descrizione
Questo servizio abilita la traccia degli eventi all'interno di ThreadX. Il buffer di traccia e il numero massimo di oggetti ThreadX vengono forniti dall'applicazione.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate **TX_ENABLE_EVENT_TRACE** per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

- **trace_buffer_start**: puntatore all'inizio del buffer di traccia fornito dall'utente.
- **trace_buffer_size**: numero totale di byte nella memoria per il buffer di traccia. Maggiore è la dimensione del buffer di traccia, maggiore sarà il numero di voci che è in grado di archiviare.
- **registry_entries**: numero di oggetti ThreadX dell'applicazione da mantenere nel Registro di sistema di traccia. Il Registro di sistema viene usato per correlare gli indirizzi degli oggetti con i nomi degli oggetti. Ciò è estremamente utile per gli strumenti di analisi delle tracce gui.

#### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) L'abilitazione della traccia eventi è riuscita.
- **TX_SIZE_ERROR** (0x05) Dimensioni del buffer di traccia specificate troppo piccole. Deve essere sufficientemente grande per l'intestazione di traccia, il Registro di sistema dell'oggetto e almeno una voce di traccia.
- **TX_NOT_DONE** (0x20) Traccia eventi era già abilitata.
- **TX_FEATURE_NOT_ENABLED** sistema (0xFF) non è stato compilato con la traccia abilitata.

#### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

#### <a name="example"></a>Esempio

```c
UCHAR my_trace_buffer[64000];

/* Enable event tracing using the global "my_trace_buffer" memory and supporting a maximum of 30 ThreadX objects in the registry. */
status = tx_trace_enable (&my_trace_buffer, 64000, 30);

/* If status is TX_SUCCESS the event tracing is enabled. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_event_filter"></a>tx_trace_event_filter

Filtrare gli eventi specificati

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_event_filter (ULONG  vent_filter_bits);
```

#### <a name="description"></a>Descrizione

Questo servizio filtra gli eventi specificati dall'inserimento nel buffer di traccia attivo. Si noti che per impostazione predefinita non viene filtrato alcun *evento dopo tx_trace_enable* chiamata a .

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate **TX_ENABLE_EVENT_TRACE** per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

- **event_filter_bits**: bit che corrispondono agli eventi da filtrare. È possibile filtrare più eventi semplicemente o riunire le costanti appropriate. Le costanti valide per questa variabile sono definite come segue:

```c
TX_TRACE_ALL_EVENTS                   0x000007FF
TX_TRACE_INTERNAL_EVENTS              0x00000001
TX_TRACE_BLOCK_POOL_EVENTS            0x00000002
TX_TRACE_BYTE_POOL_EVENTS             0x00000004
TX_TRACE_EVENT_FLAGS_EVENTS           0x00000008
TX_TRACE_INTERRUPT_CONTROL_EVENT      0x00000010
TX_TRACE_MUTEX_EVENTS                 0x00000020
TX_TRACE_QUEUE_EVENTS                 0x00000040
TX_TRACE_SEMAPHORE_EVENTS             0x00000080
TX_TRACE_THREAD_EVENTS                0x00000100
TX_TRACE_TIME_EVENTS                  0x00000200
TX_TRACE_TIMER_EVENTS                 0x00000400
FX_TRACE_ALL_EVENTS                   0x00007800
FX_TRACE_INTERNAL_EVENTS              0x00000800
FX_TRACE_MEDIA_EVENTS                 0x00001000
FX_TRACE_DIRECTORY_EVENTS             0x00002000
FX_TRACE_FILE_EVENTS                  0x00004000
NX_TRACE_ALL_EVENTS                   0x00FF8000
NX_TRACE_INTERNAL_EVENTS              0x00008000
NX_TRACE_ARP_EVENTS                   0x00010000
NX_TRACE_ICMP_EVENTS                  0x00020000
NX_TRACE_IGMP_EVENTS                  0x00040000
NX_TRACE_IP_EVENTS                    0x00080000
NX_TRACE_PACKET_EVENTS                0x00100000
NX_TRACE_RARP_EVENTS                  0x00200000
NX_TRACE_TCP_EVENTS                   0x00400000
NX_TRACE_UDP_EVENTS                   0x00800000
UX_TRACE_ALL_EVENTS                   0x7F000000
UX_TRACE_ERRORS                       0x01000000
UX_TRACE_HOST_STACK_EVENTS            0x02000000
UX_TRACE_DEVICE_STACK_EVENTS          0x04000000
UX_TRACE_HOST_CONTROLLER_EVENTS       0x08000000
UX_TRACE_DEVICE_CONTROLLER_EVENTS     0x10000000
UX_TRACE_HOST_CLASS_EVENTS            0x20000000
UX_TRACE_DEVICE_CLASS_EVENTS          0x40000000
```

#### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Riuscito.
- **TX_FEATURE_NOT_ENABLED** sistema (0xFF) non è stato compilato con la traccia abilitata.

#### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

#### <a name="example"></a>Esempio

```c
/* Filter queue and byte pool events from trace buffer. */

status = tx_trace_event_filter (TX_TRACE_QUEUE_EVENTS | TX_TRACE_BYTE_POOL_EVENTS);

/* If status is TX_SUCCESS all queue and byte pool events are filtered. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_event_unfilter"></a>tx_trace_event_unfilter

Annullare il filtro degli eventi specificati

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_event_unfilter (ULONG event_unfilter_bits);
```

#### <a name="description"></a>Descrizione

Questo servizio annulla il filtro degli eventi specificati in modo che siano inseriti nel buffer di traccia attivo.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate **TX_ENABLE_EVENT_TRACE** per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

- **event_unfilter_bits**: bit che corrispondono agli eventi da rimuovere dal filtro. Più eventi possono essere non filtrati semplicemente o unendo insieme le costanti appropriate. Le costanti valide per questa variabile sono definite come segue:

```c
TX_TRACE_ALL_EVENTS                  0x000007FF
TX_TRACE_INTERNAL_EVENTS             0x00000001
TX_TRACE_BLOCK_POOL_EVENTS           0x00000002
TX_TRACE_BYTE_POOL_EVENTS            0x00000004
TX_TRACE_EVENT_FLAGS_EVENTS          0x00000008
TX_TRACE_INTERRUPT_CONTROL_EVENT     0x00000010
TX_TRACE_MUTEX_EVENTS                0x00000020
TX_TRACE_QUEUE_EVENTS                0x00000040
TX_TRACE_SEMAPHORE_EVENTS            0x00000080
TX_TRACE_THREAD_EVENTS               0x00000100
TX_TRACE_TIME_EVENTS                 0x00000200
TX_TRACE_TIMER_EVENTS                0x00000400
FX_TRACE_ALL_EVENTS                  0x00007800
FX_TRACE_INTERNAL_EVENTS             0x00000800
FX_TRACE_MEDIA_EVENTS                0x00001000
FX_TRACE_DIRECTORY_EVENTS            0x00002000
FX_TRACE_FILE_EVENTS                 0x00004000
NX_TRACE_ALL_EVENTS                  0x00FF8000
NX_TRACE_INTERNAL_EVENTS             0x00008000
NX_TRACE_ARP_EVENTS                  0x00010000
NX_TRACE_ICMP_EVENTS                 0x00020000
NX_TRACE_IGMP_EVENTS                 0x00040000
NX_TRACE_IP_EVENTS                   0x00080000
NX_TRACE_PACKET_EVENTS               0x00100000
NX_TRACE_RARP_EVENTS                 0x00200000
NX_TRACE_TCP_EVENTS                  0x00400000
NX_TRACE_UDP_EVENTS                  0x00800000
UX_TRACE_ALL_EVENTS                  0x7F000000
UX_TRACE_ERRORS                      0x01000000
UX_TRACE_HOST_STACK_EVENTS           0x02000000
UX_TRACE_DEVICE_STACK_EVENTS         0x04000000
UX_TRACE_HOST_CONTROLLER_EVENTS      0x08000000
UX_TRACE_DEVICE_CONTROLLER_EVENTS    0x10000000
UX_TRACE_HOST_CLASS_EVENTS           0x20000000
UX_TRACE_DEVICE_CLASS_EVENTS         0x40000000
```

#### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) L'evento Successful non viene filtrato.
- **TX_FEATURE_NOT_ENABLED** sistema (0xFF) non è stato compilato con la traccia abilitata.

#### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

#### <a name="example"></a>Esempio

```c
/* Un-filter queue and byte pool events from trace buffer. */ 
status = 
  tx_trace_event_unfilter (TX_TRACE_QUEUE_EVENTS | TX_TRACE_BYTE_POOL_EVENTS);

/* If status is TX_SUCCESS all queue and byte pool events are un-filtered. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_filter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_disable"></a>tx_trace_disable

#### <a name="disable-event-tracing"></a>Disabilitare la traccia eventi

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_disable (VOID);
```

#### <a name="description"></a>Descrizione

Questo servizio disabilita la traccia degli eventi all'interno di ThreadX. Ciò può essere utile se l'applicazione vuole bloccare il buffer di traccia eventi corrente ed eventualmente trasportarlo esternamente durante la fase di esecuzione. Una volta disabilitato, il **tx_trace_enable** può essere chiamato per avviare di nuovo la traccia.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** per usare la traccia degli eventi.

#### <a name="input-parameters"></a>Parametri di input

Nessuno.

#### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) L'analisi eventi è stata disabilitata.
- **TX_NOT_DONE** (0x20) La traccia eventi non è stata abilitata.
- **TX_FEATURE_NOT_ENABLED** (0xFF) Il sistema non è stato compilato con la traccia abilitata.

#### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

#### <a name="example"></a>Esempio 

```c
/* Disable event tracing. */ 
status = tx_trace_disable ();

/* If status is TX_SUCCESS the event tracing is disabled. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_isr_enter_insert"></a>tx_trace_isr_enter_insert

#### <a name="insert-isr-enter-event"></a>Evento Enter di Inserimento ISR

#### <a name="prototype"></a>Prototipo

```c
VOID tx_trace_isr_enter_insert (ULONG isr_id);
```

#### <a name="description"></a>Descrizione

Questo servizio inserisce l'evento enter ISR nel buffer di traccia degli eventi. Deve essere chiamato dall'applicazione all'inizio dell'elaborazione ISR. Il parametro fornito deve identificare l'ISR specifico per l'applicazione.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** per usare la traccia degli eventi.

#### <a name="input-parameters"></a>Parametri di input 
- **isr_id:** valore specifico dell'applicazione per identificare l'ISR.

#### <a name="return-values"></a>Valori restituiti

**Nessuno**

#### <a name="allowed-from"></a>Consentito da 

ISR

#### <a name="example"></a>Esempio

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */

status = tx_trace_isr_enter_insert (3);

/* If status is TX_SUCCESS the ISR entry event was inserted. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_isr_exit_insert"></a>tx_trace_isr_exit_insert

#### <a name="insert-isr-exit-event"></a>Insert ISR exit event (Inserisci evento di uscita ISR)

#### <a name="prototype"></a>Prototipo

```c
VOID tx_trace_isr_exit_insert (ULONG isr_id);
```

#### <a name="description"></a>Descrizione

Questo servizio inserisce l'evento di immissione ISR nel buffer di traccia eventi. Deve essere chiamato dall'applicazione all'inizio dell'elaborazione ISR. Il parametro fornito deve identificare l'ISR per l'applicazione.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** per usare la traccia degli eventi.

#### <a name="input-parameters"></a>Parametri di input 

- **isr_id:** valore specifico dell'applicazione per identificare l'ISR.

#### <a name="return-values"></a>Valori restituiti

**Nessuno**

#### <a name="allowed-from"></a>Consentito da

ISR

#### <a name="example"></a>Esempio

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */ 

status = tx_trace_isr_exit_insert (3);

/* If status is TX_SUCCESS the ISR exit event was inserted. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_buffer_full_notify"></a>tx_trace_buffer_full_notify

#### <a name="register-trace-buffer-full-application-callback"></a>Registrare il callback completo dell'applicazione del buffer di traccia

#### <a name="prototype"></a>Prototipo

```c
VOID tx_trace_buffer_full_notify (VOID (*full_buffer_callback)(VOID *));
```

#### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback dell'applicazione chiamata da ThreadX quando il buffer di traccia diventa pieno. L'applicazione può quindi scegliere di disabilitare la traccia e/o eventualmente di configurare un nuovo buffer di traccia.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** per usare la traccia degli eventi.

#### <a name="input-parameters"></a>Parametri di input

- **full_buffer_callback:** funzione dell'applicazione da chiamare quando il buffer di traccia è pieno. Il valore NULL disabilita il callback di notifica.

#### <a name="return-values"></a>Valori restituiti

**Nessuno**

#### <a name="allowed-from"></a>Consentito da

ISR

#### <a name="example"></a>Esempio

```c
y_trace_is_full(void *trace_buffer_start)

{

     /* Application specific processing goes here! */

}

/* Register the "my_trace_is_full" function to be called whenever the trace buffer fills. */

status = tx_trace_buffer_full_notify (my_trace_is_full);

/* If status is TX_SUCCESS the "my_trace_is_full" function is registered. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_user_event_insert

### <a name="tx_trace_user_event_insert"></a>tx_trace_user_event_insert

#### <a name="insert-user-event"></a>Inserisci evento utente

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_user_event_insert (ULONG event_id, 
   ULONG info_field_1, ULONG info_field_2,
   ULONG info_field_3, ULONG info_field_4);
```

#### <a name="description"></a>Descrizione

Questo servizio inserisce l'evento utente nel buffer di traccia. Gli ID evento utente devono essere maggiori della **costante TX_TRACE_USER_EVENT_START**, che è definito come 4096. L'evento utente massimo è definito dalla costante **TX_TRACE_USER_EVENT_END**, che è definita come 65535. Tutti gli eventi all'interno di questo intervallo sono disponibili per l'applicazione. I campi di informazioni sono specifici dell'applicazione.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** per usare la traccia degli eventi.

#### <a name="input-parameters"></a>Parametri di input

- **event_id:** identificazione dell'evento specifico dell'applicazione e deve essere maggiore di **TX_TRACE_USER_EVENT_START** e minore o uguale a **TX_TRACE_USER_EVENT_END**.
- **info_field_1:** campo informazioni specifiche dell'applicazione.
- **info_field_2:** campo delle informazioni specifiche dell'applicazione.
- **info_field_3:** campo delle informazioni specifiche dell'applicazione.
- **info_field_4:** campo informazioni specifiche dell'applicazione.

#### <a name="return-values"></a>Valori restituiti
- **TX_SUCCESS** (0x00) Inserimento dell'evento utente riuscito.
- **TX_NOT_DONE** (0x20) La traccia eventi non è abilitata.
- **TX_FEATURE_NOT_ENABLED** (0xFF) Il sistema non è stato compilato con la traccia abilitata.

#### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

#### <a name="example"></a>Esempio

```c
/* Insert user event 3000, with info fields of 1, 2, 3, 4. */ 

status = tx_trace_user_event_insert (3000, 1, 2, 3, 4);

/* If status is TX_SUCCESS the user event was inserted. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify