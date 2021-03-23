---
title: 'Capitolo 6: eventi di traccia di Azure RTO ThreadX'
description: Questo capitolo descrive gli eventi ThreadX di Azure RTO.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 8f0ff03d112597371059d925f64b7511454e123c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823459"
---
# <a name="chapter-6---azure-rtos-threadx-trace-events"></a>Capitolo 6: eventi di traccia di Azure RTO ThreadX

Questo capitolo descrive gli eventi ThreadX di Azure RTO. 

## <a name="list-of-events-and-icons"></a>Elenco di eventi e icone

Di seguito è riportato un elenco di eventi ThreadX visualizzati da TraceX:

| **Icona**                         | **Significato** |
| -------------------------------- | ------------------------------------- |
| ![Icona Riprendi thread interno](./media/user-guide/tx-events/image1.png)    | Ripresa thread interno  |
| ![Icona di sospensione thread interno](./media/user-guide/tx-events/image2.png)    | Sospensione thread interno |
| ![Icona di immissione della routine del servizio di interrupt](./media/user-guide/tx-events/image3.png)    | Routine del servizio di interrupt (ISR) invio |
| ![Icona di uscita della routine del servizio di interrupt](./media/user-guide/tx-events/image4.png)    | Uscita routine servizio di interrupt (ISR)  |
| ![Icona dell'intervallo di tempo interno](./media/user-guide/tx-events/image5.png)    | Sezione tempo interna |
| ![Icona in esecuzione](./media/user-guide/tx-events/image6.png)    | In esecuzione |
| ![Icona di allocazione del pool di blocchi](./media/user-guide/tx-events/image7.png)    | **Alloca pool di blocchi** (*tx_block_allocate*)  |
| ![Icona di creazione del pool di blocchi](./media/user-guide/tx-events/image8.png)    | **Creazione del pool di blocchi** (*tx_block_pool_create*) |
| ![Icona di eliminazione del pool di blocchi](./media/user-guide/tx-events/image9.png)    | **Eliminazione del pool di blocchi** (*tx_block_pool_delete*) |
| ![Icona Ottieni informazioni sul pool di blocchi](./media/user-guide/tx-events/image10.png)    | **Ottieni informazioni sul pool di blocchi** (*tx_block_pool_info_get*) |
| ![Informazioni sulle prestazioni del pool di blocco con](./media/user-guide/tx-events/image11.png)    | **Informazioni sulle prestazioni del pool di blocco Get** (*tx_block_pool_performance_info_get*) |
| ![Icona Ottieni informazioni sulle prestazioni del sistema del pool di blocchi](./media/user-guide/tx-events/image12.png)    | **Informazioni sulle prestazioni del sistema del pool di blocco Get** (*tx_block_pool_performance_system_info_get*) |
| ![Icona di priorità del pool di blocchi](./media/user-guide/tx-events/image13.png)    | **Priorità del pool di blocchi** (*tx_block_pool_prioritize*) |
| ![Icona Blocca versione in pool](./media/user-guide/tx-events/image14.png)    | **Blocca la versione al pool** (*tx_block_release*) |
| ![Icona alloca memoria pool di byte](./media/user-guide/tx-events/image15.png)    | **Memoria allocata pool di byte** (*tx_byte_allocate*) |
| ![Icona di creazione pool di byte](./media/user-guide/tx-events/image16.png)    | **Creazione pool di byte** (*tx_byte_pool_create*) |
| ![Icona di eliminazione del pool di byte](./media/user-guide/tx-events/image17.png)    | **Eliminazione pool di byte** (*tx_byte_pool_delete*) |
| ![Icona ottenere informazioni sul pool di byte](./media/user-guide/tx-events/image18.png)    | **Informazioni sul pool di byte get** (*tx_byte_pool_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni del pool di byte](./media/user-guide/tx-events/image19.png)    | **Informazioni sulle prestazioni del pool di byte get** (*tx_byte_pool_performance_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni del sistema del pool di byte](./media/user-guide/tx-events/image20.png)    | **Informazioni sulle prestazioni del sistema del pool di byte get** (*tx_byte_pool_performance_system_info_get*) |
| ![* Icona priorità pool di byte](./media/user-guide/tx-events/image21.png)    | **Priorità del pool di byte** (*tx_byte_pool_prioritize*) |
| ![Icona versione memoria byte in pool](./media/user-guide/tx-events/image22.png)    | **Rilascio memoria byte nel pool** (*tx_byte_release*) |
| ![Icona di creazione flag evento](./media/user-guide/tx-events/image23.png)    | **Creazione flag evento** (*tx_event_flags_create*) |
| ![Icona di eliminazione flag evento](./media/user-guide/tx-events/image24.png)    | **Flag evento Delete** (*tx_event_flags_delete*) |
| ![Icona di Get flag evento](./media/user-guide/tx-events/image25.png)    | **Flag evento Get** (*tx_event_flags_get*) |
| ![Icona ottenere informazioni sui flag di evento](./media/user-guide/tx-events/image26.png)    | **Informazioni sui flag evento Get** (*tx_event_flags_info_get*) |
| ![Icona delle informazioni sulle prestazioni di flag di evento](./media/user-guide/tx-events/image27.png)    | **Informazioni sulle prestazioni di flag evento Get** (*tx_event_flags_performance_info_get*) |
| ![Icona delle informazioni sulle prestazioni del sistema flag di evento](./media/user-guide/tx-events/image28.png)    | **Flag di evento informazioni sulle prestazioni del sistema Get** (*tx_event_flags_performance_system_info_get*) |
| ![Icona set di flag evento](./media/user-guide/tx-events/image29.png)    | **Flag evento impostati** (*tx_event_flags_set*) |
| ![Icona di impostazione notifica flag evento](./media/user-guide/tx-events/image30.png)    | **Flag evento set Notify** (*tx_event_flags_set_notify*) |
| ![Icona Abilita/Disabilita interrupt](./media/user-guide/tx-events/image31.png)    | **Abilita/Disabilita interrupt** (*tx_interrupt_control*) |
| ![Icona di creazione mutex](./media/user-guide/tx-events/image32.png)    | **Creazione mutex** (*tx_mutex_create*) |
| ![Icona di eliminazione mutex](./media/user-guide/tx-events/image33.png)    | **Eliminazione mutex** (*tx_mutex_delete*) |
| ![Icona di Get mutex](./media/user-guide/tx-events/image34.png)    | **Mutex Get** (*tx_mutex_get*) |
| ![Icona Ottieni informazioni mutex](./media/user-guide/tx-events/image35.png)    | **Informazioni sul mutex Get** (*tx_mutex_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni mutex](./media/user-guide/tx-events/image36.png)    | **Informazioni sulle prestazioni di mutex Get** (*tx_mutex_performance_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni del sistema mutex](./media/user-guide/tx-events/image37.png)    | **Informazioni sulle prestazioni del sistema mutex Get** (*tx_mutex_performance_system_info_get*) |
| ![Icona di priorità mutex](./media/user-guide/tx-events/image38.png)    | **Priorità mutex** (*tx_mutex_prioritize*) |
| ![Icona put mutex](./media/user-guide/tx-events/image39.png)    | **Mutex put** (*tx_mutex_put*) |
| ![Icona Crea coda](./media/user-guide/tx-events/image40.png)    | **Creazione coda** (*tx_queue_create*) |
| ![Icona di eliminazione della coda](./media/user-guide/tx-events/image41.png)    | **Elimina coda** (*tx_queue_delete*) |
| ![Icona di svuotamento della coda](./media/user-guide/tx-events/image42.png)    | **Svuotamento coda** (*tx_queue_flush*) |
| ![Icona Invia coda in primo piano](./media/user-guide/tx-events/image43.png)    | **Invio front** -end coda (*tx_queue_front_send*) |
| ![Icona Ottieni informazioni sulla coda](./media/user-guide/tx-events/image44.png)    | **Informazioni coda Get** (*tx_queue_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni della coda](./media/user-guide/tx-events/image45.png)    | **Informazioni sulle prestazioni della coda Get** (*tx_queue_performance_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni del sistema di Accodamento](./media/user-guide/tx-events/image46.png)    | **Informazioni sulle prestazioni del sistema di Accodamento Get** (*tx_queue_performance_system_info_get*) |
| ![Icona Accodamento priorità](./media/user-guide/tx-events/image47.png)    | **Priorità coda** (*tx_queue_prioritize*) |
| ![Icona del messaggio di ricezione della coda](./media/user-guide/tx-events/image48.png)    | **Messaggio di ricezione coda** (*tx_queue_receive*) |
| ![Icona Invia messaggio coda](./media/user-guide/tx-events/image49.png)    | **Messaggio di invio coda** (*tx_queue_send*) |
| ![Icona Invia notifica coda](./media/user-guide/tx-events/image50.png)    | **Notifica invio coda** (*tx_queue_send_notify*) |
| ![Icona put soffitto semaforo](./media/user-guide/tx-events/image51.png)    | **Soffitto semaforo put** (*tx_semaphore_ceiling_put*) |
| ![Icona Crea semaforo](./media/user-guide/tx-events/image52.png)    | **Creazione semaforo** (*tx_semaphore_create*) |
| ![Icona Elimina semaforo](./media/user-guide/tx-events/image53.png)    | **Eliminazione semaforo** (*tx_semaphore_delete*) |
| ![Icona Get semaforo](./media/user-guide/tx-events/image54.png)    | **Semaforo Get** (*tx_semaphore_get*) |
| ![Icona ottenere informazioni sul semaforo](./media/user-guide/tx-events/image55.png)    | **Informazioni sul semaforo Get** (*tx_semaphore_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni del semaforo](./media/user-guide/tx-events/image56.png)    | **Informazioni sulle prestazioni del semaforo Get** (*tx_semaphroe_performance_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni del sistema Semaphore](./media/user-guide/tx-events/image57.png)    | **Informazioni sulle prestazioni del sistema Semaphore Get** (*tx_semaphore_performance_system_info_get*) |
| ![Icona priorità semaforo](./media/user-guide/tx-events/image58.png)    | **Priorità del semaforo** (*tx_semaphore_prioritize*) |
| ![Icona put del semaforo](./media/user-guide/tx-events/image59.png)    | **Semaforo put** (*tx_semaphore_put*) |
| ![Icona di notifica put del semaforo](./media/user-guide/tx-events/image60.png)    | **Notifica put semaforo** (*tx_semaphore_put_notify*) |
| ![Icona Creazione thread](./media/user-guide/tx-events/image61.png)    | **Creazione thread** (*tx_thread_create*) |
| ![Icona di eliminazione thread](./media/user-guide/tx-events/image62.png)    | **Eliminazione thread** (*tx_thread_delete*) |
| ![Icona di notifica di uscita/immissione thread](./media/user-guide/tx-events/image63.png)    | **Notifica di uscita/immissione thread** (*tx_thread_entry_exit_notify*) |
| ![Icona di identificazione del thread](./media/user-guide/tx-events/image64.png)    | **Identificazione del thread** (*tx_thread_identify*) |
| ![Icona ottenere informazioni sul thread](./media/user-guide/tx-events/image65.png)    | **Informazioni sul thread Get** (*tx_thread_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni del thread](./media/user-guide/tx-events/image66.png)    | **Informazioni sulle prestazioni del thread Get** (*tx_thread_performance_info_get*) |
| ![Icona ottenere informazioni sistema prestazioni thread](./media/user-guide/tx-events/image67.png)    | **Informazioni sul sistema di prestazioni del thread Get** (*tx_thread_performance_system_info_get*) |
| ![Icona di modifica di precedenza thread](./media/user-guide/tx-events/image68.png)    | **Modifica di precedenza thread** (*tx_thread_preemption_change*) |
| ![Icona di modifica della priorità del thread](./media/user-guide/tx-events/image69.png)    | **Modifica della priorità del thread** (*tx_thread_priority_change*) |
| ![Icona di cessione thread](./media/user-guide/tx-events/image70.png)    | **Cessione thread** (*tx_thread_relinquish*) |
| ![Icona di reimpostazione thread](./media/user-guide/tx-events/image71.png)    | **Reimpostazione thread** (*tx_thread_reset*) |
| ![* Icona Riprendi thread](./media/user-guide/tx-events/image72.png)    | **Ripresa thread** (**tx_thread_resume*) |
| ![Icona sospensione thread](./media/user-guide/tx-events/image73.png)    | **Sospensione thread** (*tx_thread_sleep*) * |
| ![Icona di notifica errori stack di thread](./media/user-guide/tx-events/image74.png)    | **Notifica errori stack di thread** (*tx_thread_stack_error_notify*) |
| ![Icona di sospensione thread](./media/user-guide/tx-events/image75.png)    | **Sospensione thread** (*tx_thread_suspend*) |
| ![Icona termina thread](./media/user-guide/tx-events/image76.png)    | **Terminazione thread** (*tx_thread_terminate*) |
| ![Icona di modifica della sezione Tempo thread](./media/user-guide/tx-events/image77.png)    | **Modifica sezionamento tempo thread** (*tx_thread_time_slice_change*) |
| ![Icona interruzione thread di attesa](./media/user-guide/tx-events/image78.png)    | **Interruzione attesa thread** (*tx_thread_wait_abort*) |
| ![Icona Time Get](./media/user-guide/tx-events/image79.png)    | **Tempo di Get** (*tx_time_get*) |
| ![Icona del set di tempo](./media/user-guide/tx-events/image80.png)    | **Set di tempo** (*tx_time_set*) |
| ![* Icona attiva timer](./media/user-guide/tx-events/image81.png)    | **Attivazione timer** (*tx_timer_activate*) |
| ![Icona di modifica timer](./media/user-guide/tx-events/image82.png)    | **Modifica timer** (*tx_timer_change*) |
| ![Icona Crea timer](./media/user-guide/tx-events/image83.png)    | **Creazione timer** (*tx_timer_create*) |
| ![Icona Disattiva timer](./media/user-guide/tx-events/image84.png)    | **Disattiva timer** (*tx_timer_deactivate*) |
| ![Icona di eliminazione timer](./media/user-guide/tx-events/image85.png)    | **Timer Delete** (*tx_timer_delete*) |
| ![Icona ottenere informazioni sul timer](./media/user-guide/tx-events/image86.png)    | **Informazioni sul timer Get** (*tx_timer_info_get*) |
| ![Icona ottenere informazioni sulle prestazioni del timer](./media/user-guide/tx-events/image87.png)    | **Informazioni sulle prestazioni del timer Get** (*tx_timer_performance_info_get*) |
| ![* Icona ottenere informazioni sul sistema di prestazioni del timer](./media/user-guide/tx-events/image88.png)    | **Informazioni sul sistema di prestazioni del timer Get** (*tx_timer_performance_system_info_get*) |
| ![User-Defined eventicon](./media/user-guide/tx-events/image0.png)    | **Evento definito dall'utente** (vedere il capitolo 10)    |

## <a name="event-descriptions"></a>Descrizioni di eventi

### <a name="internal-thread-resume"></a>Ripresa thread interno

#### <a name="internal-thread-resume"></a>Ripresa thread interno

**Icona** ![ di Icona Riprendi thread interno](./media/user-guide/tx-events/image1.png)

**Descrizione**

Questo evento rappresenta l'elaborazione interna in ThreadX che riprende un thread per l'esecuzione. Se il thread specificato è la priorità più alta e la soglia di precedenza non blocca l'esecuzione, il sistema avvierà l'esecuzione di questo thread appena pronto.

**Campi informazioni**

- Info Field 1: puntatore al thread ripreso.
- Info Field 2: stato precedente del thread ripreso, come indicato di seguito:

  |  Stato thread                     | Valore        |
  |---------------------------------- | --------|
  |  TX_READY                         | 0       |
  |  TX_COMPLETED                     | 1       |
  |  TX_TERMINATED                    | 2       |
  |  TX_SUSPENDED                     | 3       |
  |  TX_SLEEP                         | 4       |
  |  TX_QUEUE_SUSP                    | 5       |
  |  TX_SEMAPHORE_SUSP                | 6       |
  |  TX_EVENT_FLAG                    | 7       |
  |  TX_BLOCK_MEMORY                  | 8       |
  |  TX_BYTE_MEMORY                   | 9       |
  |  TX_TCP_IP                        | 12      |
  |  TX_MUTEX_SUSP                    | 13      |

- Informazioni sul campo 3: valore del puntatore dello stack durante la chiamata. 
- Info Field 4: puntatore al thread con priorità più alta successiva da eseguire.

### <a name="internal-thread-suspend"></a>Sospensione thread interno

#### <a name="internal-thread-suspend"></a>Sospensione thread interno

**Icona** ![ di Icona di sospensione thread interno](./media/user-guide/tx-events/image2.png)

**Descrizione**

Questo evento rappresenta l'elaborazione interna in ThreadX che sospende l'esecuzione di un thread. Il thread successivo con priorità più alta pronto per l'esecuzione viene inserito nel quarto campo informazioni. Se questo valore è NULL, nessun altro thread è pronto per l'esecuzione e il sistema è inattivo.

**Campi informazioni**

- Info Field 1: puntatore al thread sospeso.
- Info Field 2: nuovo stato del thread sospeso, come indicato di seguito:

  |  Stato thread                     | Valore        |
  |---------------------------------- | --------|
  |  TX_COMPLETED                     | 1       |
  |  TX_TERMINATED                    | 2       |
  |  TX_SUSPENDED                     | 3       |
  |  TX_SLEEP                         | 4       |
  |  TX_QUEUE_SUSP                    | 5       |
  |  TX_SEMAPHORE_SUSP                | 6       |
  |  TX_EVENT_FLAG                    | 7       |
  |  TX_BLOCK_MEMORY                  | 8       |
  |  TX_BYTE_MEMORY                   | 9       |
  |  TX_TCP_IP                        | 12      |
  |  TX_MUTEX_SUSP                    | 13      |

- Informazioni sul campo 3: valore del puntatore dello stack durante la chiamata. Info Field 4: puntatore al thread con priorità più alta successiva da eseguire. Se NULL, il sistema è inattivo.

### <a name="interrupt-service-routine-isr-enter"></a>Routine del servizio di interrupt (ISR) invio 

#### <a name="enter-isr"></a>Immettere ISR 

**Icona** ![ di Icona di immissione I S R](./media/user-guide/tx-events/image3.png)

**Descrizione**

Questo evento rappresenta l'immissione di una routine del servizio di interrupt (ISR) nell'applicazione. L'esecuzione della routine del servizio di interrupt continua fino a quando non si verifica l'evento di uscita ISR.

**Campi informazioni**

- Informazioni campo 1: valore del puntatore dello stack durante la chiamata.
- Informazioni campo 2: numero ISR definito dall'applicazione (facoltativo).
- Informazioni sul campo 3: numero di interrupt annidati.
- Informazioni campo 4: flag di disabilitazione di precedenza interno.

### <a name="interrupt-service-routine-isr-exit"></a>Uscita routine servizio di interrupt (ISR) 

#### <a name="exit-isr"></a>Uscita ISR

**Icona** ![ di Icona di uscita I S R](./media/user-guide/tx-events/image4.png)

**Descrizione**

Questo evento rappresenta l'uscita da una routine del servizio di interrupt (ISR) nell'applicazione.

**Campi informazioni**

- Informazioni campo 1: valore del puntatore dello stack durante la chiamata.
- Informazioni campo 2: numero ISR definito dall'applicazione (facoltativo).
- Informazioni sul campo 3: numero di interrupt annidati.
- Informazioni campo 4: flag di disabilitazione di precedenza interno.

### <a name="internal-time-slice"></a>Sezione tempo interna

#### <a name="internal-time-slice"></a>Sezione tempo interna

**Icona** ![ di Icona dell'intervallo di tempo interno](./media/user-guide/tx-events/image5.png)

**Descrizione**

Questo evento rappresenta l'elaborazione interna in ThreadX che esegue l'operazione di sezionamento del tempo. Il thread successivo con la stessa priorità viene inserito nel primo campo informazioni. Se questo valore corrisponde al thread corrente, non è stato eseguito alcun intervallo di tempo.

- Info Field 1: puntatore al thread successivo da eseguire.
- Informazioni sul campo 2: numero di interrupt annidati.
- Informazioni campo 3: flag di disabilitazione di precedenza interno.
- Informazioni sul campo 4: valore del puntatore dello stack durante la chiamata.

### <a name="running"></a>In esecuzione

#### <a name="running-in-context"></a>In esecuzione nel contesto

**Icona** ![ di Icona in esecuzione](./media/user-guide/tx-events/image6.png)

**Descrizione**

Questo evento rappresenta l'esecuzione in un contesto di thread o in un sistema inattivo. Viene usato per illustrare le modifiche successive nel contesto in seguito a un interrupt.

**Campi informazioni**
- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="block-allocate"></a>Alloca blocco 

#### <a name="tx_block_allocate"></a>tx_block_allocate

**Icona** ![ di Icona di allocazione blocchi](./media/user-guide/tx-events/image7.png)

**Descrizione**

Questo evento rappresenta l'allocazione di un blocco di memoria tramite tx_block_allocate. In caso di esito positivo, l'indirizzo del blocco allocato viene restituito nel secondo campo informazioni.

**Campi informazioni**
- Info Field 1: puntatore al pool di blocchi corrispondente.
- Info Field 2: puntatore al blocco di memoria restituito (in caso di esito positivo).
- Info Field 3: l'opzione wait fornita alla chiamata tx_block_allocate.
- Informazioni campo 4: blocchi disponibili rimanenti nel pool dopo questa allocazione.

### <a name="block-pool-create"></a>Creazione di un pool di blocchi

#### <a name="tx_block_pool_create"></a>tx_block_pool_create

**Icona** ![ di Icona di creazione del pool di blocchi](./media/user-guide/tx-events/image8.png)

**Descrizione**

Questo evento rappresenta la creazione di un pool di blocchi di memoria tramite tx_block_pool_create.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo del pool di blocchi corrispondente.
- Info Field 2: puntatore all'area di memoria iniziale del pool.
- Info Field 3: numero di blocchi nel pool. Campo informazioni 4: dimensioni di ogni blocco nel pool in byte.

### <a name="block-pool-delete"></a>Eliminazione del pool di blocchi

#### <a name="tx_block_pool_delete"></a>tx_block_pool_delete

**Icona** ![ di Icona di eliminazione del pool di blocchi](./media/user-guide/tx-events/image9.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un pool di blocchi di memoria tramite tx_block_pool_delete.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo del pool di blocchi.
- Informazioni sul campo 2: valore del puntatore dello stack durante la chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="block-pool-information-get"></a>Ottieni informazioni sul pool di blocco 

#### <a name="tx_block_pool_info_get"></a>tx_block_pool_info_get

**Icona** ![ di Icona Ottieni informazioni sul pool di blocchi](./media/user-guide/tx-events/image10.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su un pool di blocchi di memoria tramite tx_block_pool_info_get.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo del pool di blocchi.
- Informazioni sul campo 2: valore del puntatore dello stack durante la chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="block-pool-performance-information-get"></a>Informazioni sulle prestazioni del pool di blocco Get

#### <a name="tx_block_pool_performance_info_get"></a>tx_block_pool_performance_info_get

**Icona** ![ di Icona Ottieni informazioni sulle prestazioni del pool di blocchi](./media/user-guide/tx-events/image11.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sulle prestazioni di un pool di blocchi di memoria tramite tx_block_pool_performance_info_get.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo del pool di blocchi.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="block-pool-performance-system-information-get"></a>Informazioni sul sistema di prestazioni del pool di blocchi Get

#### <a name="tx_block_pool_performance_system_info_get"></a>tx_block_pool_performance_system_info_get

**Icona** ![ di Icona Ottieni informazioni sul sistema di prestazioni del pool di blocchi](./media/user-guide/tx-events/image12.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative a tutti i pool di blocchi di memoria tramite tx_block_pool_performance_system_info_get.

**Campi informazioni**
- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="block-pool-prioritize"></a>Priorità del pool di blocchi

#### <a name="tx_block_pool_prioritize"></a>tx_block_pool_prioritize

**Icona** ![ di Icona di priorità del pool di blocchi](./media/user-guide/tx-events/image13.png)

**Descrizione**

Questo evento rappresenta l'inserimento del thread sospeso PrioritàMassima all'inizio dell'elenco di sospensioni del pool di blocchi. Se questa operazione viene eseguita prima di chiamare tx_block_release, il thread sospeso con la priorità più alta riceverà il blocco rilasciato.

**Campi informazioni**
- Campo informazioni 1: puntatore al pool di blocchi di memoria.
- Campo informazioni 2: numero di thread sospesi in questo pool di blocchi.
- Campo info 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="block-release"></a>Blocca versione 

#### <a name="tx_block_release"></a>tx_block_release

**Icona** ![ di Icona di rilascio del blocco](./media/user-guide/tx-events/image14.png)

**Descrizione**

Questo evento rappresenta il rilascio di un blocco precedentemente allocato al pool di blocchi.

**Campi informazioni**

- Campo informazioni 1: puntatore al pool di blocchi di memoria.
- Informazioni sul campo 2: puntatore a blocco da rilasciare.
- Campo info 3: numero di thread sospesi in questo pool di blocchi.
- Informazioni sul campo 4: puntatore dello stack al momento della chiamata.

### <a name="byte-allocate"></a>Allocazione byte 

#### <a name="tx_byte_allocate"></a>tx_byte_allocate

**Icona** ![ di Icona di allocazione byte](./media/user-guide/tx-events/image15.png)

**Descrizione**

Questo evento rappresenta l'allocazione della memoria tramite tx_byte_allocate. In caso di esito positivo, l'indirizzo della memoria allocata viene restituito nel secondo campo informazioni.

**Campi informazioni**
- Info Field 1: puntatore al pool di byte corrispondente.
- Info Field 2: puntatore alla memoria restituita (in caso di esito positivo).
- Campo info 3: numero di byte richiesti. Info Field 4: l'opzione wait fornita alla chiamata tx_byte_allocate.

### <a name="byte-pool-create"></a>Creazione pool di byte

#### <a name="tx_byte_pool_create"></a>tx_byte_pool_create

**Icona** ![ di Icona di creazione pool di byte](./media/user-guide/tx-events/image16.png)

**Descrizione**

Questo evento rappresenta la creazione di un pool di byte tramite tx_byte_pool_create.

**Campi informazioni**

- Info Field 1: puntatore al pool di byte corrispondente.
- Info Field 2: puntatore all'inizio dell'area di memoria. Campo info 3: numero di byte nel pool di byte.
- Info Field 4: il puntatore dello stack al momento della chiamata.

### <a name="byte-pool-delete"></a>Eliminazione pool di byte 

#### <a name="tx_byte_pool_delete"></a>tx_byte_pool_delete

**Icona** ![ di Icona di eliminazione del pool di byte](./media/user-guide/tx-events/image17.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un pool di byte tramite tx_byte_pool_delete.

**Campi informazioni**

- Info Field 1: puntatore al pool di byte corrispondente.
- Info Field 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="byte-pool-information-get"></a>Ottenere informazioni sul pool di byte

#### <a name="tx_byte_pool_info_get"></a>tx_byte_pool_info_get

**Icona** ![ di Icona ottenere informazioni sul pool di byte](./media/user-guide/tx-events/image18.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sul pool di byte tramite tx_byte_pool_info_get.

**Campi informazioni**

- Info Field 1: puntatore al pool di byte corrispondente.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="byte-pool-performance-info-get"></a>Informazioni sulle prestazioni del pool di byte Get 

#### <a name="tx_byte_pool_info_get"></a>tx_byte_pool_info_get

**Icona** ![ di Icona Ottieni informazioni sulle prestazioni del pool di byte](./media/user-guide/tx-events/image19.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sulle prestazioni del pool di byte tramite tx_byte_pool_performance_info_get.

**Campi informazioni**

- Info Field 1: puntatore al pool di byte corrispondente.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="byte-pool-performance-system-info-get"></a>Informazioni sul sistema di prestazioni del pool di byte Get 

#### <a name="tx_byte_pool_performance_system_info_get"></a>tx_byte_pool_performance_system_info_get

**Icona** ![ di Icona di informazioni sul sistema di prestazioni del pool di byte](./media/user-guide/tx-events/image20.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sul sistema delle prestazioni del pool di byte tramite tx_byte_pool_performance_system_info_get.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="byte-pool-prioritize"></a>Priorità del pool di byte

#### <a name="tx_byte_pool_prioritize"></a>tx_byte_pool_prioritize

**Icona** ![ di Icona priorità pool di byte](./media/user-guide/tx-events/image21.png)

**Descrizione**

Questo evento rappresenta la priorità dell'elenco di sospensioni del pool di byte tramite tx_byte_pool_prioritize.

**Campi informazioni**

- Info Field 1: puntatore al pool di byte corrispondente.
- Campo informazioni 2: numero di thread attualmente sospesi nel pool di byte.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="byte-release"></a>Versione byte

#### <a name="tx_byte_release"></a>tx_byte_release

**Icona** ![ di Icona versione byte](./media/user-guide/tx-events/image22.png)

**Descrizione**

Questo evento rappresenta il rilascio di un blocco di memoria allocato da un pool di byte tramite tx_byte_release.

**Campi informazioni**

- Info Field 1: puntatore al pool di byte corrispondente.
- Informazioni sul campo 2: puntatore alla memoria del pool di byte allocata in precedenza.
- Campo info 3: numero di thread sospesi in questo pool di byte.
- Campo informazioni 4: numero di byte di memoria disponibili.

### <a name="event-flags-create"></a>Creazione flag evento 

#### <a name="tx_event_flags_create"></a>tx_event_flags_create

**Icona** ![ di Icona di creazione flag evento](./media/user-guide/tx-events/image23.png)

**Descrizione**

Questo evento rappresenta la creazione di un nuovo gruppo di flag di evento tramite tx_event_flags_create.

**Campi informazioni** 
- Info Field 1: puntatore al blocco di controllo del gruppo di flag di evento.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="event-flags-delete"></a>Flag evento Delete 

#### <a name="tx_event_flags_delete"></a>tx_event_flags_delete

**Icona** ![ di Icona di eliminazione flag evento](./media/user-guide/tx-events/image24.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un gruppo di flag di evento tramite tx_event_flags_delete.

**Campi informazioni** 

- Info Field 1: puntatore al gruppo di flag di evento.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="event-flags-get"></a>Flag evento Get 

#### <a name="tx_event_flags_get"></a>tx_event_flags_get

**Icona** ![ di Icona flag evento gt](./media/user-guide/tx-events/image25.png)

**Descrizione**

Questo evento rappresenta il recupero dei flag di evento da un gruppo di flag di evento esistente tramite tx_event_flags_get.

**Campi informazioni**

- Info Field 1: puntatore al gruppo di flag di evento.
- Campo informazioni 2: Flag evento richiesti.
- Info Field 3: flag di evento attualmente impostati nel gruppo.
- Info Field 4: opzione richiesta sui flag di evento Get.

### <a name="event-flags-information-get"></a>Informazioni sui flag evento Get

#### <a name="tx_event_flags_info_get"></a>tx_event_flags_info_get

**Icona** ![ di Icona ottenere informazioni sui flag di evento](./media/user-guide/tx-events/image26.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_info_get.

**Campi informazioni**

- Info Field 1: puntatore al gruppo di flag di evento.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="event-flags-performance-information-get"></a>Flag evento informazioni sulle prestazioni Get 

#### <a name="tx_event_flags_performance_info_get"></a>tx_event_flags_performance_info_get

**Icona** ![ di Icona delle informazioni sulle prestazioni di flag di evento](./media/user-guide/tx-events/image27.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sulle prestazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_performance_info_get.

**Campi informazioni** 
- Info Field 1: puntatore al gruppo di flag di evento.
- Campo informazioni 2: non usato
- Campo info 3: non usato
- Campo informazioni 4: non usato

### <a name="event-flags-performance-system-info-get"></a>Flag evento prestazioni informazioni sistema Get

#### <a name="tx_event_flags_performance_system_info_get"></a>tx_event_flags_performance_system_info_get

**Icona** ![ di Icona di informazioni sul sistema delle prestazioni flag di evento](./media/user-guide/tx-events/image28.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sulle prestazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_performance_system_info_get.

**Campi informazioni**
- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="event-flags-set"></a>Flag evento impostati 

#### <a name="tx_event_flags_set"></a>tx_event_flags_set

**Icona** ![ di Icona set di flag evento](./media/user-guide/tx-events/image29.png)

**Descrizione**

Questo evento rappresenta l'impostazione o la cancellazione di flag di evento in un gruppo di flag di evento esistente tramite tx_event_flags_set.

**Campi informazioni**

- Info Field 1: puntatore al gruppo di flag di evento.
- Informazioni sul campo 2: Flag evento da impostare o deselezionare.
- Informazioni sul campo 3: e o l'opzione del flag evento.
- Campo informazioni 4: numero di thread sospesi nel gruppo di flag di evento.

### <a name="event-flags-set-notify"></a>Notifica di impostazione flag evento

#### <a name="tx_event_flags_set_notify"></a>tx_event_flags_set_notify

**Icona** ![ di Icona di impostazione notifica flag evento](./media/user-guide/tx-events/image30.png)

**Descrizione**

Questo evento rappresenta la registrazione di un callback di notifica per qualsiasi operazione di impostazione del flag evento su un gruppo di flag di evento esistente tramite tx_event_flags_set_notify.

**Campi informazioni**

- Info Field 1: puntatore al gruppo di flag di evento.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="interrupt-control"></a>Interrompi controllo 

#### <a name="tx_interrupt_control"></a>tx_interrupt_control

**Icona** ![ di Icona di controllo interrupt](./media/user-guide/tx-events/image31.png)

**Descrizione**

Questo evento rappresenta la modifica della postura di blocco di interrupt del processore tramite tx_interrupt_control.

**Campi informazioni**

- Campo informazioni 1: nuova postura interrupt.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="mutex-create"></a>Creazione mutex 

#### <a name="tx_mutex_create"></a>tx_mutex_create

**Icona** ![ di Icona di creazione mutex](./media/user-guide/tx-events/image32.png)

**Descrizione**

Questo evento rappresenta la creazione di un mutex tramite tx_mutex_create.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo mutex.
- Informazioni campo 2: opzione ereditarietà priorità
- (TX_INHERIT o TX_NO_INHERIT).
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="mutex-delete"></a>Eliminazione mutex 

#### <a name="tx_mutex_delete"></a>tx_mutex_delete

**Icona** ![ di Icona di eliminazione mutex](./media/user-guide/tx-events/image33.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un mutex tramite tx_mutex_delete.

**Campi informazioni** 

- Info Field 1: puntatore a mutex.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="mutex-get"></a>Get mutex 

#### <a name="tx_mutex_get"></a>tx_mutex_get

**Icona** ![ di Icona di Get mutex](./media/user-guide/tx-events/image34.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di un mutex tramite tx_mutex_get.

**Campi informazioni**

- Info Field 1: puntatore a mutex.
- Info Field 2: l'opzione wait fornita alla chiamata tx_mutex_get.
- Info Field 3: puntatore al thread proprietario del mutex (NULL implica che il mutex non è di proprietà).
- Campo info 4: numero di volte in cui il thread proprietario ha chiamato tx_mutex_get.

### <a name="mutex-information-get"></a>Informazioni sul mutex Get

#### <a name="tx_mutex_info_get"></a>tx_mutex_info_get

**Icona** ![ di Icona Ottieni informazioni mutex](./media/user-guide/tx-events/image35.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni mutex tramite tx_mutex_info_get.

**Campi informazioni**

- Info Field 1: puntatore a mutex.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="mutex-performance-information-get"></a>Informazioni sulle prestazioni mutex Get 

#### <a name="tx_mutex_performance_info_get"></a>tx_mutex_performance_info_get

**Icona** ![ di Icona ottenere informazioni sulle prestazioni mutex](./media/user-guide/tx-events/image36.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sulle prestazioni di mutex tramite tx_mutex_performance_info_get.

**Campi informazioni**

- Info Field 1: puntatore a mutex.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="mutex-performance-system-info-get"></a>Informazioni sul sistema delle prestazioni mutex Get

#### <a name="tx_mutex_performance_system_info_get"></a>tx_mutex_performance_system_info_get

**Icona** ![ di Icona informazioni sul sistema di prestazioni mutex](./media/user-guide/tx-events/image37.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sulle prestazioni del sistema mutex tramite tx_mutex_performance_system_info_get.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="mutex-prioritize"></a>Priorità mutex 

#### <a name="tx_mutex_prioritize"></a>tx_mutex_prioritize

**Icona** ![ di Icona di priorità mutex](./media/user-guide/tx-events/image38.png)

**Descrizione**

Questo evento rappresenta la priorità dell'elenco di sospensioni del mutex tramite tx_mutex_prioritize.

**Campi informazioni**

- Info Field 1: puntatore al mutex corrispondente.
- Campo informazioni 2: numero di thread attualmente sospesi sul mutex.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="mutex-put"></a>Mutex put 

#### <a name="tx_mutex_put"></a>tx_mutex_put

**Icona** ![ di Icona put mutex](./media/user-guide/tx-events/image39.png)

**Descrizione**

Questo evento rappresenta il rilascio di un mutex di proprietà precedente tramite tx_mutex_put.

**Campi informazioni**

- Info Field 1: puntatore al mutex corrispondente.
- Info Field 2: puntatore del thread proprietario del mutex.
- Campo info 3: numero di richieste Get mutex in attesa.
- Informazioni sul campo 4: puntatore dello stack al momento della chiamata.

### <a name="queue-create"></a>Creazione coda 

#### <a name="tx_queue_create"></a>tx_queue_create

**Icona** ![ di Icona Crea coda](./media/user-guide/tx-events/image40.png)

**Descrizione**

Questo evento rappresenta la creazione di una coda di messaggi tramite tx_queue_create.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo Queue.
- Informazioni sul campo 2: dimensioni del messaggio, in termini di parole a 32 bit.
- Info Field 3: puntatore all'avvio dell'area di memoria della coda.
- Campo informazioni 4: numero di byte nell'area memoria coda.

### <a name="queue-delete"></a>Elimina coda 

#### <a name="tx_queue_delete"></a>tx_queue_delete

**Icona** ![ di Icona di eliminazione della coda](./media/user-guide/tx-events/image41.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di una coda tramite tx_queue_delete.

**Campi informazioni**

- Info Field 1: puntatore alla coda.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="queue-flush"></a>Scaricamento coda 

#### <a name="tx_queue_flush"></a>tx_queue_flush

**Icona** ![ di Icona di svuotamento della coda](./media/user-guide/tx-events/image42.png)

**Descrizione**

Questo evento rappresenta lo svuotamento (cancellazione di tutti i contenuti della coda) di una coda tramite tx_queue_flush.

**Campi informazioni**

- Info Field 1: puntatore alla coda.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="queue-front-send"></a>Invio front-end della coda 

#### <a name="tx_queue_front_send"></a>tx_queue_front_send

**Icona** ![ di Icona Invia coda in primo piano](./media/user-guide/tx-events/image43.png)

**Descrizione**

Questo evento rappresenta l'invio di un messaggio all'inizio di una coda tramite tx_queue_front_send.

**Campi informazioni**

- Info Field 1: puntatore alla coda.
- Informazioni sul campo 2: puntatore all'avvio del messaggio.
- Informazioni sul campo 3: l'opzione wait fornita al
- chiamata tx_queue_front_send.
- Campo informazioni 4: numero di messaggi già accodati.

### <a name="queue-information-get"></a>Informazioni coda Get 

#### <a name="tx_queue_info_get"></a>tx_queue_info_get

**Icona** ![ di Icona Ottieni informazioni sulla coda](./media/user-guide/tx-events/image44.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su una coda tramite tx_queue_info_get.

**Campi informazioni** 
- Info Field 1: puntatore alla coda.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="queue-performance-info-get"></a>Informazioni sulle prestazioni della coda Get 

#### <a name="tx_queue_performance_info_get"></a>tx_queue_performance_info_get

**Icona** ![ di Icona ottenere informazioni sulle prestazioni della coda](./media/user-guide/tx-events/image45.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative a una coda tramite tx_queue_performance_info_get.

**Campi informazioni** 

- Info Field 1: puntatore alla coda.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="queue-performance-system-info-get"></a>Informazioni sul sistema di prestazioni della coda Get 

#### <a name="tx_queue_performance_system_info_get"></a>tx_queue_performance_system_info_get

**Icona** ![ di Icona di informazioni sul sistema delle prestazioni della coda](./media/user-guide/tx-events/image46.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni del sistema relative a tutte le code nel sistema.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="queue-prioritize"></a>Priorità coda 

#### <a name="tx_queue_prioritize"></a>tx_queue_prioritize

**Icona** ![ di Icona Accodamento priorità](./media/user-guide/tx-events/image47.png)

**Descrizione**

Questo evento rappresenta la priorità dell'elenco di sospensione della coda tramite tx_queue_prioritize.

**Campi informazioni** 

- Info Field 1: puntatore alla coda corrispondente.
- Campo informazioni 2: numero di thread attualmente sospesi nella coda.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

#### <a name="queue-receive"></a>Ricezione coda 

##### <a name="tx_queue_receive"></a>tx_queue_receive

**Icona** ![ di Icona di ricezione della coda](./media/user-guide/tx-events/image48.png)

**Descrizione**

Questo evento rappresenta la ricezione di un messaggio da una coda tramite tx_queue_receive.

**Campi informazioni** 

- Info Field 1: puntatore alla coda.
- Informazioni sul campo 2: puntatore alla destinazione per il messaggio. Info Field 3: opzione wait fornita alla chiamata.
- Campo informazioni 4: numero di messaggi attualmente in coda.

### <a name="queue-send"></a>Coda Invio 

#### <a name="tx_queue_send"></a>tx_queue_send

**Icona** ![ di Icona Invia coda](./media/user-guide/tx-events/image49.png)

**Descrizione**

Questo evento rappresenta l'invio di un messaggio a una coda tramite tx_queue_send.

**Campi informazioni** 

- Info Field 1: puntatore alla coda.
- Informazioni sul campo 2: puntatore al messaggio.
- Info Field 3: opzione wait fornita alla chiamata.
- Campo informazioni 4: numero di messaggi attualmente in coda.

### <a name="queue-send-notify"></a>Notifica invio coda 

#### <a name="tx_queue_send_notify"></a>tx_queue_send_notify

**Icona** ![ di Icona Invia notifica coda](./media/user-guide/tx-events/image50.png)

**Descrizione**

<p>Questo evento rappresenta la registrazione di un callback tramite tx_queue_send_notify, che viene chiamato ogni volta che un messaggio viene inviato a una coda.

**Campi informazioni** 

- Info Field 1: puntatore alla coda.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="semaphore-ceiling-put"></a>Soffitto semaforo put 

#### <a name="tx_semaphore_ceiling_put"></a>tx_semaphore_ceiling_put

**Icona** ![ di Icona put soffitto semaforo](./media/user-guide/tx-events/image51.png)

**Descrizione**

Questo evento rappresenta l'inserimento in un semaforo tramite tx_semaphore_ceiling_put. Questo comportamento è diverso da quello tx_semaphore_put in quanto il valore massimo del semaforo viene esaminato in modo che l'operazione PUT non consentisca di superare il valore massimo o il limite massimo.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al semaforo.
- Informazioni sul campo 2: conteggio corrente del semaforo.
- Campo info 3: numero di thread sospesi sul semaforo.
- Informazioni sul campo 4: limite massimo fornito alla chiamata.

#### <a name="semaphore-create"></a>Creazione semaforo 

##### <a name="tx_semaphore_create"></a>tx_semaphore_create

**Icona** ![ di Icona Crea semaforo](./media/user-guide/tx-events/image52.png)

**Descrizione**

Questo evento rappresenta la creazione di un semaforo tramite tx_semaphore_create.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo Semaphore.
- Informazioni sul campo 2: conteggio iniziale del semaforo.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="semaphore-delete"></a>Eliminazione del semaforo 

#### <a name="tx_semaphore_delete"></a>tx_semaphore_delete

**Icona** ![ di Icona Elimina semaforo](./media/user-guide/tx-events/image53.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un semaforo tramite tx_semaphore_delete.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al semaforo.
- NFO Field 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="semaphore-get"></a>Semaforo Get 

#### <a name="tx_semaphore_get"></a>tx_semaphore_get

**Icona** ![ di Icona Get semaforo](./media/user-guide/tx-events/image54.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di un semaforo tramite tx_semaphore_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al semaforo.
- Info Field 2: opzione wait fornita alla chiamata.
- Informazioni sul campo 3: conteggio corrente del semaforo.
- Informazioni sul campo 4: puntatore dello stack al momento della chiamata.

### <a name="semaphore-information-get"></a>Informazioni sul semaforo Get 

#### <a name="tx_semaphore_info_get"></a>tx_semaphore_info_get

**Icona** ![ di Icona ottenere informazioni sul semaforo](./media/user-guide/tx-events/image55.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di informazioni su un semaforo tramite tx_semaphore_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al semaforo.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="semaphore-performance-info-get"></a>Informazioni sulle prestazioni del semaforo Get 

#### <a name="tx_semaphore_performance_info_get"></a>tx_semaphore_performance_info_get

**Icona** ![ di Icona delle informazioni sulle prestazioni del semaforo](./media/user-guide/tx-events/image56.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative a un semaforo tramite tx_semaphore_performance_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al semaforo.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="semaphore-performance-system-info"></a>Informazioni sul sistema di prestazioni del semaforo 

#### <a name="tx_semaphore_performance_system_info_get"></a>tx_semaphore_performance_system_info_get

**Icona** ![ di Icona informazioni sistema prestazioni semaforo](./media/user-guide/tx-events/image57.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative a tutti i semafori del sistema tramite tx_semaphore_performance_system_info_get.

**Campi informazioni** 

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="semaphore-prioritize"></a>Priorità del semaforo 

#### <a name="tx_semaphore_prioritize"></a>tx_semaphore_prioritize

**Icona** ![ di Icona priorità semaforo](./media/user-guide/tx-events/image58.png)

**Descrizione**

Questo evento rappresenta la priorità dell'elenco di sospensioni del semaforo tramite tx_semaphore_prioritize.

**Campi informazioni**

- Info Field 1: puntatore al semaforo corrispondente.
- Campo informazioni 2: numero di thread attualmente sospesi sul semaforo.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="semaphore-put"></a>Semaforo put 

#### <a name="tx_semaphore_put"></a>tx_semaphore_put

**Icona** ![ di Icona put del semaforo](./media/user-guide/tx-events/image59.png)

**Descrizione**

Questo evento rappresenta il rilascio di un'istanza del semaforo tramite tx_semaphore_put.

**Campi informazioni** 

- Info Field 1: puntatore al semaforo corrispondente. Informazioni sul campo 2: conteggio corrente del semaforo.
- Campo info 3: numero di thread sospesi sul semaforo.
- Informazioni sul campo 4: puntatore dello stack al momento della chiamata.

### <a name="semaphore-put-notify"></a>Notifica put semaforo 

#### <a name="tx_semaphore_put_notify"></a>tx_semaphore_put_notify

**Icona** ![ di Icona di notifica put del semaforo](./media/user-guide/tx-events/image60.png)

**Descrizione**

Questo evento rappresenta la registrazione di un callback tramite tx_semaphore_put_notify chiamato ogni volta che viene inserita un'istanza del semaforo.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore al semaforo.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="thread-create"></a>Creazione thread 

#### <a name="tx_thread_create"></a>tx_thread_create

**Icona** ![ di Icona Creazione thread](./media/user-guide/tx-events/image61.png)

**Descrizione**

Questo evento rappresenta la creazione di un thread tramite tx_thread_create.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo thread.
- Informazioni sul campo 2: priorità del thread.
- Informazioni sul campo 3: puntatore dello stack per il thread.
- NFO Field 4: dimensioni dello stack in byte.

### <a name="thread-delete"></a>Eliminazione thread 

#### <a name="tx_thread_delete"></a>tx_thread_delete

**Icona** ![ di Icona di eliminazione thread](./media/user-guide/tx-events/image62.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un thread tramite tx_thread_delete.

**Campi informazioni** 

- Info Field 1: puntatore al thread.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="thread-entryexit-notify"></a>Notifica voce/uscita thread 

#### <a name="tx_thread_entry_exit_notify"></a>tx_thread_entry_exit_notify

**Icona** ![ di Icona di immissione/chiusura del thread](./media/user-guide/tx-events/image63.png)

**Descrizione**

Questo evento rappresenta la registrazione di un callback tramite tx_thread_entry_exit_notify chiamato ogni volta che un thread viene inserito o chiuso.

**Campi informazioni** 

- Info Field 1: puntatore al thread.
- Informazioni sul campo 2: stato del thread al momento della registrazione.
- Informazioni sul campo 3: puntatore allo stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

#### <a name="thread-identify"></a>Identificazione thread 

##### <a name="tx_thread_identify"></a>tx_thread_identify

**Icona** ![ di Icona di identificazione del thread](./media/user-guide/tx-events/image64.png)

**Descrizione**

Questo evento rappresenta il recupero del puntatore al thread corrente tramite tx_thread_identify.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="thread-information-get"></a>Informazioni sul thread Get 

#### <a name="tx_thread_info_get"></a>tx_thread_info_get

**Icona** ![ di Icona ottenere informazioni sul thread](./media/user-guide/tx-events/image65.png)

**Descrizione**

Questo evento rappresenta l'acquisizione di informazioni sul thread specificato tramite tx_thread_info_get.

**Campi informazioni**

- Info Field 1: puntatore al thread.
- Informazioni sul campo 2: stato del thread al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

#### <a name="thread-performance-information-get"></a>Informazioni sulle prestazioni del thread Get 

##### <a name="tx_thread_performance_info_get"></a>tx_thread_performance_info_get

**Icona** ![ di Icona ottenere informazioni sulle prestazioni del thread](./media/user-guide/tx-events/image66.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative al thread specificato tramite tx_thread_performance_info_get.

**Campi informazioni**

- Info Field 1: puntatore al thread.
- Informazioni sul campo 2: stato del thread al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="thread-performance-system-info-get"></a>Informazioni sul sistema di prestazioni del thread Get 

#### <a name="tx_thread_performance_system_info_get"></a>tx_thread_performance_system_info_get

**Icona** ![ di Icona di informazioni sul sistema delle prestazioni del thread](./media/user-guide/tx-events/image67.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni su tutti i thread tramite tx_thread_performance_system_info_get.

**Campi informazioni** 

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="thread-preemption-change"></a>Modifica di precedenza thread 

#### <a name="tx_thread_preemption_change"></a>tx_thread_preemption_change

**Icona** ![ di Icona di modifica di precedenza thread](./media/user-guide/tx-events/image68.png)

**Descrizione**

Questo evento rappresenta la modifica della soglia di precedenza di un thread tramite tx_thread_preemption_change.

**Campi informazioni** 

- Info Field 1: puntatore al thread.
- Campo informazioni 2: nuova soglia di precedenza.
- Campo informazioni 3: soglia di precedenza precedente.
- Informazioni sul campo 4: stato del thread al momento della chiamata.

### <a name="thread-priority-change"></a>Modifica della priorità del thread 

#### <a name="tx_thread_priority_change"></a>tx_thread_priority_change

**Icona** ![ di Icona di modifica della priorità del thread](./media/user-guide/tx-events/image69.png)

**Descrizione**

Questo evento rappresenta la modifica della priorità di un thread tramite tx_thread_priority_change.

- Campi informazioni 
- Info Field 1: puntatore al thread.
- Informazioni sul campo 2: nuova priorità.
- Informazioni sul campo 3: priorità precedente.
- Informazioni sul campo 4: stato del thread al momento della chiamata.

### <a name="thread-relinquish"></a>Cessione thread 

#### <a name="tx_thread_relinquish"></a>tx_thread_relinquish

**Icona** ![ di Icona di cessione thread](./media/user-guide/tx-events/image70.png)

**Descrizione**

Questo evento rappresenta l'abbandono del processore da un thread tramite tx_thread_relinquish.

**Campi informazioni**

- Info Field 1: puntatore dello stack al momento della chiamata.
- Info Field 2: puntatore al thread successivo da eseguire.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="thread-reset"></a>Reimpostazione thread 

#### <a name="tx_thread_reset"></a>tx_thread_reset

**Icona** ![ di Icona di reimpostazione thread](./media/user-guide/tx-events/image71.png)

**Descrizione**

Questo evento rappresenta la reimpostazione di un thread completato o terminato tramite tx_thread_reset.

**Campi informazioni**

- Info Field 1: puntatore al thread.
- Informazioni sul campo 2: stato del thread al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

#### <a name="thread-resume"></a>Ripresa thread 

##### <a name="tx_thread_resume"></a>tx_thread_resume

**Icona** ![ di Icona Riprendi thread](./media/user-guide/tx-events/image72.png)

**Descrizione**

Questo evento rappresenta il ripristino di un thread sospeso tramite tx_thread_resume.

**Campi informazioni**

- Info Field 1: puntatore al thread.
- Informazioni sul campo 2: stato del thread al momento della chiamata.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="thread-sleep"></a>Sospensione thread 

#### <a name="tx_thread_sleep"></a>tx_thread_sleep

**Icona** ![ di Icona sospensione thread](./media/user-guide/tx-events/image73.png)

**Descrizione**

Questo evento rappresenta la sospensione del thread corrente per un numero specificato di cicli del timer tramite tx_thread_sleep.

**Campi informazioni**

- Campo informazioni 1: numero di cicli per la sospensione.
- Informazioni sul campo 2: stato del thread al momento della chiamata.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="thread-stack-error-notify"></a>Notifica errori stack di thread 

#### <a name="tx_thread_stack_error_notify_event"></a>tx_thread_stack_error_notify_event

**Icona** ![ di Icona di notifica errori stack di thread](./media/user-guide/tx-events/image74.png)

**Descrizione**

Questo evento rappresenta la registrazione di una routine di notifica degli errori dello stack di thread tramite tx_thread_stack_error_notify_event.

**Campi informazioni** 

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="thread-suspend"></a>Sospensione thread 

#### <a name="tx_thread_suspend"></a>tx_thread_suspend

**Icona** ![ di Icona di sospensione thread](./media/user-guide/tx-events/image75.png)

**Descrizione**

Questo evento rappresenta la sospensione di un thread tramite tx_thread_suspend.

**Campi informazioni** 

- Info Field 1: puntatore al thread da sospendere.
- Informazioni sul campo 2: stato del thread al momento della chiamata.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="thread-terminate"></a>Terminazione thread 

#### <a name="tx_thread_terminate"></a>tx_thread_terminate

**Icona** ![ di Icona termina thread](./media/user-guide/tx-events/image76.png)

**Descrizione**

Questo evento rappresenta la terminazione di un thread tramite tx_thread_terminate.

**Campi informazioni** 

- Info Field 1: puntatore al thread da terminare.
- Informazioni sul campo 2: stato del thread al momento della chiamata.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="thread-time-slice-change"></a>Modifica Time-Slice thread 

#### <a name="tx_thread_time_slice_change"></a>tx_thread_time_slice_change

**Icona** ![ di Icona di modifica della sezione Tempo thread](./media/user-guide/tx-events/image77.png)

**Descrizione**

Questo evento rappresenta la modifica della sezione temporale di un thread tramite tx_thread_time_slice_change.

**Campi informazioni**

- Info Field 1: puntatore al thread.
- Campo informazioni 2: nuova sezione di tempo.
- Informazioni sul campo 3: intervallo di tempo precedente.
- Campo informazioni 4: non utilizzato.

### <a name="thread-wait-abort"></a>Interruzione attesa thread 

#### <a name="tx_thread_wait_abort"></a>tx_thread_wait_abort

**Icona** ![ di Icona interruzione thread di attesa](./media/user-guide/tx-events/image78.png)

**Descrizione**

Questo evento rappresenta l'interruzione della sospensione di un thread tramite tx_thread_wait_abort.

**Campi informazioni**

- Info Field 1: puntatore al thread.
- Informazioni sul campo 2: stato del thread al momento della chiamata.
- Informazioni sul campo 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: non utilizzato.

### <a name="time-get"></a>Tempo di ottenimento 

#### <a name="tx_time_get"></a>tx_time_get

**Icona** ![ di Icona Time Get](./media/user-guide/tx-events/image79.png)

**Descrizione**

Questo evento rappresenta il recupero del numero corrente di cicli del timer tramite tx_time_get.

**Campi informazioni**

- Campo informazioni 1: numero corrente di cicli del timer.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="time-set"></a>Set di tempo 

#### <a name="tx_time_set"></a>tx_time_set

**Icona** ![ di Icona del set di tempo](./media/user-guide/tx-events/image80.png)

**Descrizione**

Questo evento rappresenta l'impostazione del numero corrente di cicli del timer tramite tx_time_set.

**Campi informazioni**

- Campo informazioni 1: nuovo numero di cicli del timer.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="timer-activate"></a>Attivazione timer 

#### <a name="tx_timer_activate"></a>tx_timer_activate

**Icona** ![ di Icona di attivazione timer](./media/user-guide/tx-events/image81.png)

**Descrizione**

Questo evento rappresenta l'attivazione del timer specificato tramite tx_timer_activate.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al timer.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="timer-change"></a>Modifica timer 

#### <a name="tx_timer_change"></a>tx_timer_change

**Icona** ![ di Icona di modifica timer](./media/user-guide/tx-events/image82.png)

**Descrizione**

Questo evento rappresenta la modifica del timer specificato tramite tx_timer_change.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al timer.
- Campo informazioni 2: cicli di scadenza iniziali.
- Informazioni sul campo 3: pianificare i cicli di scadenza.
- Campo informazioni 4: non utilizzato.

### <a name="timer-create"></a>Creazione timer 

#### <a name="tx_timer_create"></a>tx_timer_create

**Icona** ![ di Icona Crea timer](./media/user-guide/tx-events/image83.png)

**Descrizione**

Questo evento rappresenta la creazione di un timer tramite tx_timer_create.

**Campi informazioni**

- Info Field 1: puntatore al blocco di controllo timer.
- Campo informazioni 2: cicli di scadenza iniziali.
- Informazioni sul campo 3: pianificare i cicli di scadenza.
- Informazioni sul campo 4: abilitazione automatica del valore, ovvero TX_AUTO_ACTIVATE (1) o TX_NO_ACTIVATE (0).

### <a name="timer-deactivate"></a>Timer disattivato 

#### <a name="tx_timer_deactivate"></a>tx_timer_deactivate

**Icona** ![ di Icona Disattiva timer](./media/user-guide/tx-events/image84.png)

**Descrizione**

Questo evento rappresenta la disattivazione di un timer tramite tx_timer_deactivate.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al timer.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="timer-delete"></a>Timer Delete 

#### <a name="tx_timer_delete"></a>tx_timer_delete

**Icona** ![ di Icona di eliminazione timer](./media/user-guide/tx-events/image85.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un timer tramite tx_timer_delete.

**Campi informazioni** 

- Informazioni sul campo 1: puntatore al timer.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="timer-information-get"></a>Informazioni sul timer Get 

#### <a name="tx_timer_info_get"></a>tx_timer_info_get

**Icona** ![ di Icona per ottenere informazioni sul timer](./media/user-guide/tx-events/image86.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sul timer tramite tx_timer_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al timer.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="timer-performance-information-get"></a>Informazioni sulle prestazioni del timer Get 

#### <a name="tx_timer_performance_info_get"></a>tx_timer_performance_info_get

**Icona** ![ di Icona ottenere informazioni sulle prestazioni del timer](./media/user-guide/tx-events/image87.png)

**Descrizione** 

Questo evento rappresenta il recupero delle informazioni sulle prestazioni del timer tramite tx_timer_performance_info_get.

**Campi informazioni**

- Informazioni sul campo 1: puntatore al timer.
- Informazioni sul campo 2: puntatore dello stack al momento della chiamata.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.

### <a name="timer-system-performance-info-get"></a>Informazioni sulle prestazioni del sistema timer Get 

#### <a name="tx_timer_performance_system_info_get"></a>tx_timer_performance_system_info_get

**Icona** ![ di Icona delle informazioni sulle prestazioni del sistema timer Get](./media/user-guide/tx-events/image88.png)


**Descrizione** 

Questo evento rappresenta il recupero di tutte le informazioni sulle prestazioni del timer tramite tx_timer_performance_system_info_get.

**Campi informazioni**

- Campo informazioni 1: non utilizzato.
- Campo informazioni 2: non utilizzato.
- Campo info 3: non utilizzato.
- Campo informazioni 4: non utilizzato.