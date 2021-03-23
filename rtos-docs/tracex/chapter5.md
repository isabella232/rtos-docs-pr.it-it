---
title: Capitolo 5-generazione di buffer di traccia
description: Questo capitolo contiene una descrizione della creazione di un buffer di eventi TraceX di Azure RTO e descrive anche il formato sottostante del buffer.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: f296137d23b9f3c1c4fd115947bb50a32b768123
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823426"
---
# <a name="chapter-5---generating-trace-buffers"></a>Capitolo 5-generazione di buffer di traccia

Questo capitolo contiene una descrizione della creazione di un buffer di eventi TraceX di Azure RTO e descrive anche il formato sottostante del buffer.

## <a name="threadx-event-trace-support"></a>Supporto per la traccia eventi ThreadX

ThreadX fornisce il supporto predefinito per la traccia degli eventi per tutti i servizi ThreadX, le modifiche allo stato del thread e gli eventi definiti dall'utente. La funzionalità di traccia degli eventi di ThreadX è progettata principalmente come strumento post-mortem per analizzare le ultime attività "n" nell'applicazione. Da queste informazioni, lo sviluppatore può individuare problemi e/o potenziali destinazioni di ottimizzazione.

TraceX Visualizza graficamente il buffer di traccia eventi compilato da ThreadX. Di seguito viene descritto come compilare il buffer e viene descritto il formato sottostante del buffer.

## <a name="enabling-event-trace"></a>Abilitazione della traccia eventi

Per abilitare la traccia eventi, definire le costanti timestamp, compilare la libreria ThreadX con **TX_ENABLE_EVENT_TRACE** definito e abilitare la traccia chiamando la funzione **tx_trace_enable** .

## <a name="defining-time-stamp-constants"></a>Definizione di costanti Time-Stamp

Le costanti timestamp sono progettate per fornire al controllo dello sviluppatore il timestamp usato nelle voci della traccia eventi. Di seguito sono riportate le due costanti timestamp e i relativi valori predefiniti:

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ++_tx_trace_simulated_time
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK   0xFFFFFFFFUL
#endif
```

Le costanti precedenti sono definite in **tx_port. h** e creano un timestamp "Fake" che viene semplicemente incrementato di uno per ogni evento. Di seguito è riportato un esempio di definizione di timestamp effettiva:

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ((ULONG) 0x0x13000004)
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK 0xFFFFFFFFUL
#endif
```

Le costanti sopra indicate specificano un timer a 32 bit ottenuto leggendo l'indirizzo 0x13000004. La maggior parte dei timestamp specifici dell'applicazione devono essere impostati in modo analogo.

## <a name="exporting-the-trace-buffer"></a>Esportazione del buffer di traccia

TraceX richiede il buffer di traccia in un formato di file binario, Intel HEX o Motorola S-record nell'host. Il modo più semplice per eseguire questa operazione consiste nell'arrestare la destinazione e indicare al debugger di eseguire il dump dell'area di memoria fornita per ***tx_trace_enable*** funzione in un file nell'host.

> [!WARNING]
>***Prestare attenzione a non arrestare la destinazione all'interno di un codice di raccolta della traccia. Questa operazione può causare informazioni di traccia non valide. Se il programma viene interrotto all'interno di ThreadX, è preferibile eseguire un'istruzione/routine di ogni macro di inserimento della traccia prima di eseguire il dump del buffer di traccia.***

> [!IMPORTANT]
> *Nell'Appendice D viene illustrato come eseguire il dump del buffer di traccia da un'ampia gamma di strumenti di sviluppo.*

## <a name="extended-event-trace-api"></a>API di traccia degli eventi estesi

Quando ThreadX viene compilato con **TX_ENABLE_EVENT_TRACE** definito, per l'applicazione sono disponibili le nuove API di traccia eventi seguenti:

- tx_trace_enable: *Abilita traccia eventi*
- tx_trace_event_filter: *Filtra evento/i specificato/i*
- tx_trace_event_unfilter: non *filtrare gli eventi specificati*
- tx_trace_disable: *Disabilita traccia eventi*
- tx_trace_isr_enter_insert: *Inserisci l'evento di traccia ISR*
- tx_trace_isr_exit_insert: *Inserisci evento di traccia di uscita ISR*
- tx_trace_buffer_full_notify: *registrare il callback dell'applicazione completo del buffer di traccia*
- tx_trace_user_event_insert: *Inserisci evento utente*

### <a name="tx_trace_enable"></a>tx_trace_enable

Abilitare la traccia eventi

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_enable (VOID *trace_buffer_start,
     ULONG trace_buffer_size, ULONG registry_entries);
```

#### <a name="description"></a>Descrizione
Questo servizio Abilita la traccia eventi all'interno di ThreadX. Il buffer di traccia e il numero massimo di oggetti ThreadX vengono forniti dall'applicazione.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

- **trace_buffer_start**: puntatore all'inizio del buffer di traccia fornito dall'utente.
- **trace_buffer_size**: numero totale di byte nella memoria per il buffer di traccia. Maggiore è il buffer di traccia, maggiore è il numero di voci che è in grado di archiviare.
- **registry_entries**: numero di oggetti threadX dell'applicazione da tenere nel registro di traccia. Il registro di sistema viene utilizzato per correlare gli indirizzi di oggetto con i nomi degli oggetti. Questa operazione è particolarmente utile per gli strumenti di analisi della traccia GUI.

#### <a name="return-values"></a>Valori restituiti

- Abilitazione della traccia eventi riuscita **TX_SUCCESS** (0x00).
- Dimensioni del buffer di traccia **TX_SIZE_ERROR** (0x05) specificate troppo piccole. Deve essere sufficientemente grande per l'intestazione di traccia, il registro oggetti e almeno una voce di traccia.
- La traccia eventi **TX_NOT_DONE** (0x20) è già stata abilitata.
- Il sistema **TX_FEATURE_NOT_ENABLED** (0xFF) non è stato compilato con la traccia abilitata.

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

Filtra eventi specificati

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_event_filter (ULONG  vent_filter_bits);
```

#### <a name="description"></a>Descrizione

Questo servizio filtra gli eventi specificati da inserire nel buffer di traccia attivo. Si noti che per impostazione predefinita nessun evento viene filtrato dopo la chiamata di *tx_trace_enable* .

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

- **event_filter_bits**: bit che corrispondono agli eventi da filtrare. È possibile filtrare più eventi semplicemente ORing insieme le costanti appropriate. Le costanti valide per questa variabile sono definite come segue:

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

- **TX_SUCCESS** (0x00) filtro eventi riuscito.
- Il sistema **TX_FEATURE_NOT_ENABLED** (0xFF) non è stato compilato con la traccia abilitata.

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

Non filtrare gli eventi specificati

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_event_unfilter (ULONG event_unfilter_bits);
```

#### <a name="description"></a>Descrizione

Questo servizio è in grado di filtrare gli eventi specificati in modo che vengano inseriti nel buffer di traccia attivo.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

- **event_unfilter_bits**: bit che corrispondono agli eventi da defiltrare. È possibile che più eventi non vengano filtrati semplicemente o-insieme alle costanti appropriate. Le costanti valide per questa variabile sono definite come segue:

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

- Defiltro evento riuscito **TX_SUCCESS** (0x00).
- Il sistema **TX_FEATURE_NOT_ENABLED** (0xFF) non è stato compilato con la traccia abilitata.

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

#### <a name="disable-event-tracing"></a>Disabilita traccia eventi

#### <a name="prototype"></a>Prototipo

```c
UINT tx_trace_disable (VOID);
```

#### <a name="description"></a>Descrizione

Questo servizio Disabilita la traccia eventi all'interno di ThreadX. Questa operazione può essere utile se l'applicazione desidera bloccare il buffer di traccia dell'evento corrente ed eventualmente trasferirlo esternamente durante la fase di esecuzione. Una volta disabilitato, è possibile chiamare il **tx_trace_enable** per avviare di nuovo la traccia.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

Nessuna.

#### <a name="return-values"></a>Valori restituiti

- Disattivazione della traccia eventi riuscita **TX_SUCCESS** (0x00).
- La traccia eventi **TX_NOT_DONE** (0x20) non è stata abilitata.
- Il sistema **TX_FEATURE_NOT_ENABLED** (0xFF) non è stato compilato con la traccia abilitata.

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

#### <a name="insert-isr-enter-event"></a>Inserisci evento di immissione ISR

#### <a name="prototype"></a>Prototipo

```c
VOID tx_trace_isr_enter_insert (ULONG isr_id);
```

#### <a name="description"></a>Descrizione

Questo servizio inserisce l'evento di immissione ISR nel buffer di traccia eventi. Deve essere chiamato dall'applicazione all'inizio dell'elaborazione ISR. Il parametro fornito deve identificare l'ISR specifico per l'applicazione.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input 
- **isr_id**: valore specifico dell'applicazione per identificare l'ISR.

#### <a name="return-values"></a>Valori restituiti

**Nessuno**

#### <a name="allowed-from"></a>Consentito da 

ISRs

#### <a name="example"></a>Esempio

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */

status = tx_trace_isr_enter_insert (3);

/* If status is TX_SUCCESS the ISR entry event was inserted. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_isr_exit_insert"></a>tx_trace_isr_exit_insert

#### <a name="insert-isr-exit-event"></a>Inserisci evento di uscita ISR

#### <a name="prototype"></a>Prototipo

```c
VOID tx_trace_isr_exit_insert (ULONG isr_id);
```

#### <a name="description"></a>Descrizione

Questo servizio inserisce l'evento di immissione ISR nel buffer di traccia eventi. Deve essere chiamato dall'applicazione all'inizio dell'elaborazione ISR. Il parametro fornito dovrebbe identificare l'ISR per l'applicazione.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input 

- **isr_id**: valore specifico dell'applicazione per identificare l'ISR.

#### <a name="return-values"></a>Valori restituiti

**Nessuno**

#### <a name="allowed-from"></a>Consentito da

ISRs

#### <a name="example"></a>Esempio

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */ 

status = tx_trace_isr_exit_insert (3);

/* If status is TX_SUCCESS the ISR exit event was inserted. */
```

#### <a name="see-also"></a>Vedere anche

tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert

### <a name="tx_trace_buffer_full_notify"></a>tx_trace_buffer_full_notify

#### <a name="register-trace-buffer-full-application-callback"></a>Registra callback dell'applicazione completo del buffer di traccia

#### <a name="prototype"></a>Prototipo

```c
VOID tx_trace_buffer_full_notify (VOID (*full_buffer_callback)(VOID *));
```

#### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback dell'applicazione che viene chiamata da ThreadX quando il buffer di traccia diventa pieno. L'applicazione può quindi scegliere di disabilitare la traccia e/o possibilmente di configurare un nuovo buffer di traccia.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

- **full_buffer_callback**: funzione dell'applicazione da chiamare quando il buffer di traccia è pieno. Il valore NULL disabilita il callback di notifica.

#### <a name="return-values"></a>Valori restituiti

**Nessuno**

#### <a name="allowed-from"></a>Consentito da

ISRs

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

Questo servizio inserisce l'evento utente nel buffer di traccia. Gli ID evento utente devono essere maggiori della costante **TX_TRACE_USER_EVENT_START**, che è definita come 4096. Il numero massimo di eventi utente è definito dalla costante **TX_TRACE_USER_EVENT_END**, che è definita come 65535. Tutti gli eventi all'interno di questo intervallo sono disponibili per l'applicazione. I campi delle informazioni sono specifici dell'applicazione.

> [!IMPORTANT]
> La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.

#### <a name="input-parameters"></a>Parametri di input

- **event_id**: l'identificazione dell'evento specifico dell'applicazione e deve iniziare essere maggiore di **TX_TRACE_USER_EVENT_START** e minore o uguale a **TX_TRACE_USER_EVENT_END**.
- **info_field_1**: campo delle informazioni specifiche dell'applicazione.
- **info_field_2**: campo delle informazioni specifiche dell'applicazione.
- **info_field_3**: campo delle informazioni specifiche dell'applicazione.
- **info_field_4**: campo delle informazioni specifiche dell'applicazione.

#### <a name="return-values"></a>Valori restituiti
- **TX_SUCCESS** (0x00) inserimento evento utente riuscito.
- La traccia eventi **TX_NOT_DONE** (0x20) non è abilitata.
- **TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con la traccia abilitata.

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