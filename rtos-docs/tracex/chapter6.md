---
title: Capitolo 6 - Azure RTOS di traccia ThreadX
description: Questo capitolo descrive i Azure RTOS ThreadX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 9fefc43002d4e0d6df817ad56d79b3e41a3d649504be50f5a39f67c1896b2e9a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116800340"
---
# <a name="chapter-6---azure-rtos-threadx-trace-events"></a>Capitolo 6 - Azure RTOS di traccia ThreadX

Questo capitolo descrive i Azure RTOS ThreadX. 

## <a name="list-of-events-and-icons"></a>Elenco di eventi e icone

Di seguito è riportato un elenco di eventi ThreadX visualizzati da TraceX:

| **Icona**                         | **Significato** |
| -------------------------------- | ------------------------------------- |
| ![Icona di ripresa del thread interno](./media/user-guide/tx-events/image1.png)    | Ripresa del thread interno  |
| ![Icona di sospensione del thread interno](./media/user-guide/tx-events/image2.png)    | Sospensione del thread interno |
| ![Icona Interrompi routine servizio Invio](./media/user-guide/tx-events/image3.png)    | Routine di servizio di interruzione (ISR) Invio |
| ![Icona Interrompi routine di routine del servizio](./media/user-guide/tx-events/image4.png)    | Interruzione della routine del servizio (ISR) Uscita  |
| ![Icona della sezione temporale interna](./media/user-guide/tx-events/image5.png)    | Intervallo di tempo interno |
| ![Icona In esecuzione](./media/user-guide/tx-events/image6.png)    | In esecuzione |
| ![Icona di allocazione pool di blocchi](./media/user-guide/tx-events/image7.png)    | **Allocazione pool a** blocchi (*tx_block_allocate*)  |
| ![Icona di creazione del pool di blocchi](./media/user-guide/tx-events/image8.png)    | **Creazione del pool a** blocchi (*tx_block_pool_create*) |
| ![Icona di eliminazione del pool di blocchi](./media/user-guide/tx-events/image9.png)    | **Eliminazione del pool** *a blocchi*( tx_block_pool_delete ) |
| ![Icona Ottieni informazioni sul pool di blocchi](./media/user-guide/tx-events/image10.png)    | **Ottenere informazioni sul pool** *di blocchi*( tx_block_pool_info_get ) |
| ![Ottenere informazioni sulle prestazioni del pool di blocchi](./media/user-guide/tx-events/image11.png)    | **Ottenere informazioni sulle prestazioni del pool** di blocchi (*tx_block_pool_performance_info_get*) |
| ![Icona di visualizzazione delle informazioni sulle prestazioni del sistema del pool di blocchi](./media/user-guide/tx-events/image12.png)    | **Ottenere informazioni sulle prestazioni del sistema** del pool di blocchi (*tx_block_pool_performance_system_info_get*) |
| ![Icona Blocca priorità pool](./media/user-guide/tx-events/image13.png)    | **Priorità del pool di blocchi** (*tx_block_pool_prioritize*) |
| ![Icona Blocca versione nel pool](./media/user-guide/tx-events/image14.png)    | **Blocca versione nel pool** (*tx_block_release*) |
| ![Icona alloca memoria nel pool di byte](./media/user-guide/tx-events/image15.png)    | **Memoria allocata nel pool di** byte (*tx_byte_allocate*) |
| ![Icona di creazione del pool di byte](./media/user-guide/tx-events/image16.png)    | **Creazione del pool di byte** (*tx_byte_pool_create*) |
| ![Icona di eliminazione del pool di byte](./media/user-guide/tx-events/image17.png)    | **Eliminazione del pool di** byte (*tx_byte_pool_delete*) |
| ![Icona ottieni informazioni sul pool di byte](./media/user-guide/tx-events/image18.png)    | **Informazioni sul pool di byte get** (*tx_byte_pool_info_get*) |
| ![Icona ottieni informazioni sulle prestazioni del pool di byte](./media/user-guide/tx-events/image19.png)    | **Ottenere informazioni sulle prestazioni del pool di byte** (*tx_byte_pool_performance_info_get*) |
| ![Icona get delle informazioni sulle prestazioni del sistema del pool di byte](./media/user-guide/tx-events/image20.png)    | **Ottenere informazioni sulle prestazioni del sistema** del pool di byte (*tx_byte_pool_performance_system_info_get*) |
| ![Icona *Priorità pool di byte](./media/user-guide/tx-events/image21.png)    | **Priorità pool di byte** (*tx_byte_pool_prioritize*) |
| ![Icona byte memory release to pool](./media/user-guide/tx-events/image22.png)    | **Rilascio della memoria in byte nel pool** (*tx_byte_release*) |
| ![Icona di creazione dei flag di evento](./media/user-guide/tx-events/image23.png)    | **Creazione di flag di** evento (*tx_event_flags_create*) |
| ![Icona di eliminazione dei flag di evento](./media/user-guide/tx-events/image24.png)    | **Eliminazione dei flag di** evento (*tx_event_flags_delete*) |
| ![Icona get dei flag di evento](./media/user-guide/tx-events/image25.png)    | **Flag di evento get** (*tx_event_flags_get*) |
| ![Icona get delle informazioni sui flag di evento](./media/user-guide/tx-events/image26.png)    | **Informazioni sui flag di evento get** (*tx_event_flags_info_get*) |
| ![Icona get delle informazioni sulle prestazioni dei flag di evento](./media/user-guide/tx-events/image27.png)    | **Informazioni sulle prestazioni dei flag di evento get** (*tx_event_flags_performance_info_get*) |
| ![Icona get delle informazioni sulle prestazioni di sistema dei flag di evento](./media/user-guide/tx-events/image28.png)    | **Event flags system performance information get** (*tx_event_flags_performance_system_info_get*) |
| ![Icona di impostazione dei flag di evento](./media/user-guide/tx-events/image29.png)    | **Flag di evento impostati** (*tx_event_flags_set*) |
| ![Icona di notifica impostata per i flag di evento](./media/user-guide/tx-events/image30.png)    | **I flag di evento impostano notify** (*tx_event_flags_set_notify*) |
| ![Icona di abilitazione/disabilitazione dell'interrupt](./media/user-guide/tx-events/image31.png)    | **Interrupt enable/disable** (*tx_interrupt_control*) |
| ![Icona di creazione mutex](./media/user-guide/tx-events/image32.png)    | **Creazione mutex** (*tx_mutex_create*) |
| ![Icona di eliminazione mutex](./media/user-guide/tx-events/image33.png)    | **Eliminazione mutex** (*tx_mutex_delete*) |
| ![Icona di mutex get](./media/user-guide/tx-events/image34.png)    | **Mutex get** (*tx_mutex_get*) |
| ![Icona Di visualizzazione delle informazioni sui mutex](./media/user-guide/tx-events/image35.png)    | **Informazioni mutex get** (*tx_mutex_info_get*) |
| ![Icona get delle informazioni sulle prestazioni del mutex](./media/user-guide/tx-events/image36.png)    | **Ottenere informazioni sulle prestazioni del mutex** (*tx_mutex_performance_info_get*) |
| ![Icona get delle informazioni sulle prestazioni del sistema mutex](./media/user-guide/tx-events/image37.png)    | **Informazioni sulle prestazioni del sistema mutex get** (*tx_mutex_performance_system_info_get*) |
| ![Icona di assegnazione delle priorità dei mutex](./media/user-guide/tx-events/image38.png)    | **Priorità mutex** (*tx_mutex_prioritize*) |
| ![Icona di mutex put](./media/user-guide/tx-events/image39.png)    | **Mutex put** (*tx_mutex_put*) |
| ![Icona di creazione della coda](./media/user-guide/tx-events/image40.png)    | **Creazione della** coda (*tx_queue_create*) |
| ![Icona di eliminazione della coda](./media/user-guide/tx-events/image41.png)    | **Eliminazione coda** (*tx_queue_delete*) |
| ![Icona scaricamento coda](./media/user-guide/tx-events/image42.png)    | **Scaricamento della** coda (*tx_queue_flush*) |
| ![Icona Di accodamento per l'invio in primo piano](./media/user-guide/tx-events/image43.png)    | **Accodamento front-send** (*tx_queue_front_send*) |
| ![Icona Per ottenere informazioni sulla coda](./media/user-guide/tx-events/image44.png)    | **Informazioni sulla coda get** (*tx_queue_info_get*) |
| ![Icona ottieni informazioni sulle prestazioni della coda](./media/user-guide/tx-events/image45.png)    | **Ottenere informazioni sulle prestazioni della coda** (*tx_queue_performance_info_get*) |
| ![Icona ottieni informazioni sulle prestazioni del sistema di accodamento](./media/user-guide/tx-events/image46.png)    | **Ottenere informazioni sulle prestazioni del sistema** della coda (*tx_queue_performance_system_info_get*) |
| ![Icona di assegnazione delle priorità della coda](./media/user-guide/tx-events/image47.png)    | **Priorità della coda** (*tx_queue_prioritize*) |
| ![Icona del messaggio di ricezione della coda](./media/user-guide/tx-events/image48.png)    | **Messaggio di ricezione coda** (*tx_queue_receive*) |
| ![Icona del messaggio di invio della coda](./media/user-guide/tx-events/image49.png)    | **Messaggio di invio della** coda (*tx_queue_send*) |
| ![Icona di notifica di invio della coda](./media/user-guide/tx-events/image50.png)    | **Notifica di invio della** coda (*tx_queue_send_notify*) |
| ![Icona del semaforo ceiling put](./media/user-guide/tx-events/image51.png)    | **Semaphore ceiling put** (*tx_semaphore_ceiling_put*) |
| ![Icona Crea semaforo](./media/user-guide/tx-events/image52.png)    | **Creazione del semaforo** (*tx_semaphore_create*) |
| ![Icona di eliminazione del semaforo](./media/user-guide/tx-events/image53.png)    | **Eliminazione del semaforo** (*tx_semaphore_delete*) |
| ![Icona get del semaforo](./media/user-guide/tx-events/image54.png)    | **Semaforo get** (*tx_semaphore_get*) |
| ![Icona Ottieni informazioni sul semaforo](./media/user-guide/tx-events/image55.png)    | **Informazioni sul semaforo get** (*tx_semaphore_info_get*) |
| ![Icona ottieni informazioni sulle prestazioni del semaforo](./media/user-guide/tx-events/image56.png)    | **Ottenere informazioni sulle prestazioni del semaforo** (*tx_semaphroe_performance_info_get*) |
| ![Icona get delle informazioni sulle prestazioni del sistema del semaforo](./media/user-guide/tx-events/image57.png)    | **Ottenere informazioni sulle prestazioni del sistema del semaforo** (*tx_semaphore_performance_system_info_get*) |
| ![Icona di assegnazione delle priorità del semaforo](./media/user-guide/tx-events/image58.png)    | **Priorità del semaforo** (*tx_semaphore_prioritize*) |
| ![Icona Put del semaforo](./media/user-guide/tx-events/image59.png)    | **Semaforo put** (*tx_semaphore_put*) |
| ![Icona di notifica di Semaphore put](./media/user-guide/tx-events/image60.png)    | **Notifica put del semaforo** (*tx_semaphore_put_notify*) |
| ![Icona Crea thread](./media/user-guide/tx-events/image61.png)    | **Creazione di thread** (*tx_thread_create*) |
| ![Icona Di eliminazione thread](./media/user-guide/tx-events/image62.png)    | **Eliminazione thread** (*tx_thread_delete*) |
| ![Icona di notifica di uscita/ingresso del thread](./media/user-guide/tx-events/image63.png)    | **Notifica di uscita/ingresso del thread** (*tx_thread_entry_exit_notify*) |
| ![Icona identificazione thread](./media/user-guide/tx-events/image64.png)    | **Identificazione thread** (*tx_thread_identify*) |
| ![Icona Per ottenere le informazioni sui thread](./media/user-guide/tx-events/image65.png)    | **Informazioni sul thread get** (*tx_thread_info_get*) |
| ![Icona get delle informazioni sulle prestazioni dei thread](./media/user-guide/tx-events/image66.png)    | **Ottenere informazioni sulle prestazioni dei thread** (*tx_thread_performance_info_get*) |
| ![Icona get delle informazioni sul sistema per le prestazioni dei thread](./media/user-guide/tx-events/image67.png)    | **Ottenere informazioni sul sistema delle** prestazioni dei thread (*tx_thread_performance_system_info_get*) |
| ![Icona di modifica della preemption dei thread](./media/user-guide/tx-events/image68.png)    | **Modifica di preemption dei thread** (*tx_thread_preemption_change*) |
| ![Icona di modifica della priorità dei thread](./media/user-guide/tx-events/image69.png)    | **Modifica della priorità dei** thread (*tx_thread_priority_change*) |
| ![Icona Disinserzione thread](./media/user-guide/tx-events/image70.png)    | **Thread relinquish** (*tx_thread_relinquish*) |
| ![Icona reimpostazione thread](./media/user-guide/tx-events/image71.png)    | **Reimpostazione del** thread (*tx_thread_reset*) |
| ![*Icona Di ripresa thread](./media/user-guide/tx-events/image72.png)    | **Ripresa thread** (**tx_thread_resume*) |
| ![Icona Sospensione thread](./media/user-guide/tx-events/image73.png)    | **Sospensione thread** (*tx_thread_sleep*)* |
| ![Icona di notifica degli errori dello stack di thread](./media/user-guide/tx-events/image74.png)    | **Notifica degli errori dello stack** di thread (*tx_thread_stack_error_notify*) |
| ![Icona Di sospensione thread](./media/user-guide/tx-events/image75.png)    | **Sospensione thread** (*tx_thread_suspend*) |
| ![Icona terminazione thread](./media/user-guide/tx-events/image76.png)    | **Terminazione del thread** (*tx_thread_terminate*) |
| ![Icona di modifica della sezione temporale del thread](./media/user-guide/tx-events/image77.png)    | **Modifica della sezione temporale del thread** (*tx_thread_time_slice_change*) |
| ![Icona interruzione attesa thread](./media/user-guide/tx-events/image78.png)    | **Interruzione dell'attesa** *del thread*( tx_thread_wait_abort ) |
| ![Icona time get](./media/user-guide/tx-events/image79.png)    | **Time get** (*tx_time_get*) |
| ![Icona del set di tempo](./media/user-guide/tx-events/image80.png)    | **Set di tempo** (*tx_time_set*) |
| ![*Icona di attivazione del timer](./media/user-guide/tx-events/image81.png)    | **Attivazione timer** (*tx_timer_activate*) |
| ![Icona di modifica del timer](./media/user-guide/tx-events/image82.png)    | **Modifica del timer** (*tx_timer_change*) |
| ![Icona Crea timer](./media/user-guide/tx-events/image83.png)    | **Creazione timer** (*tx_timer_create*) |
| ![Icona di disattivazione del timer](./media/user-guide/tx-events/image84.png)    | **Disattivazione timer** (*tx_timer_deactivate*) |
| ![Icona Di eliminazione timer](./media/user-guide/tx-events/image85.png)    | **Eliminazione timer** (*tx_timer_delete*) |
| ![Icona Per ottenere informazioni sul timer](./media/user-guide/tx-events/image86.png)    | **Informazioni sul timer get** (*tx_timer_info_get*) |
| ![Icona Ottieni informazioni sulle prestazioni del timer](./media/user-guide/tx-events/image87.png)    | **Ottenere informazioni sulle prestazioni del timer** (*tx_timer_performance_info_get*) |
| ![*Icona ottieni informazioni sul sistema delle prestazioni del timer](./media/user-guide/tx-events/image88.png)    | **Informazioni sul sistema delle prestazioni del timer get** (*tx_timer_performance_system_info_get*) |
| ![User-Defined Eventicon](./media/user-guide/tx-events/image0.png)    | **Evento definito dall'utente** (vedere il capitolo 10)    |

## <a name="event-descriptions"></a>Descrizioni di eventi

### <a name="internal-thread-resume"></a>Ripresa del thread interno

#### <a name="internal-thread-resume"></a>Ripresa del thread interno

**Icona** ![ Icona di ripresa del thread interno](./media/user-guide/tx-events/image1.png)

**Descrizione**

Questo evento rappresenta l'elaborazione interna in ThreadX che riprende un thread per l'esecuzione. Se il thread specificato ha la priorità più alta e preemption-threshold non ne blocca l'esecuzione, il sistema inizierà a eseguire questo nuovo thread pronto.

**Campi di informazioni**

- Campo informazioni 1: puntatore al thread da riprendere.
- Campo informazioni 2: stato precedente del thread ripreso, come indicato di seguito:

  |  Stato del thread                     | Valore        |
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

- Campo informazioni 3: valore del puntatore dello stack durante la chiamata. 
- Campo informazioni 4: puntatore al thread con priorità più alta successivo da eseguire.

### <a name="internal-thread-suspend"></a>Sospensione del thread interno

#### <a name="internal-thread-suspend"></a>Sospensione del thread interno

**Icona** ![ Icona di sospensione del thread interno](./media/user-guide/tx-events/image2.png)

**Descrizione**

Questo evento rappresenta l'elaborazione interna in ThreadX che sospende l'esecuzione di un thread. Il thread con priorità più alta successivo pronto per l'esecuzione viene inserito nel quarto campo delle informazioni. Se questo valore è NULL, non sono disponibili altri thread pronti per l'esecuzione e il sistema è inattivo.

**Campi di informazioni**

- Campo informazioni 1: puntatore al thread sospeso.
- Campo informazioni 2: nuovo stato del thread sospeso, come indicato di seguito:

  |  Stato del thread                     | Valore        |
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

- Campo informazioni 3: valore del puntatore dello stack durante la chiamata. Campo informazioni 4: puntatore al thread con priorità più alta successivo da eseguire. Se NULL, il sistema è inattivo.

### <a name="interrupt-service-routine-isr-enter"></a>Interrupt Service Routine (ISR) enter 

#### <a name="enter-isr"></a>Immettere ISR 

**Icona** ![ Immettere l'icona I S R](./media/user-guide/tx-events/image3.png)

**Descrizione**

Questo evento rappresenta l'immissione di una routine del servizio di interrupt (ISR) nell'applicazione. L'esecuzione della routine del servizio di interruzione continua fino a quando non si verifica l'evento di uscita isr.

**Campi di informazioni**

- Campo informazioni 1: valore del puntatore dello stack durante la chiamata.
- Campo Info 2: Numero ISR definito dall'applicazione (facoltativo).
- Campo Info 3: Numero di interrupt annidati.
- Campo informazioni 4: flag di disabilitazione della preemption interna.

### <a name="interrupt-service-routine-isr-exit"></a>Interruzione dell'uscita della routine del servizio (ISR) 

#### <a name="exit-isr"></a>Uscire da ISR

**Icona** ![ Icona Esci da I S R](./media/user-guide/tx-events/image4.png)

**Descrizione**

Questo evento rappresenta l'uscita di una routine del servizio di interrupt (ISR) nell'applicazione.

**Campi di informazioni**

- Campo informazioni 1: valore del puntatore dello stack durante la chiamata.
- Campo Info 2: Numero ISR definito dall'applicazione (facoltativo).
- Campo Info 3: Numero di interrupt annidati.
- Campo informazioni 4: flag di disabilitazione della preemption interna.

### <a name="internal-time-slice"></a>Intervallo di tempo interno

#### <a name="internal-time-slice"></a>Intervallo di tempo interno

**Icona** ![ Icona della sezione temporale interna](./media/user-guide/tx-events/image5.png)

**Descrizione**

Questo evento rappresenta l'elaborazione interna in ThreadX che esegue l'operazione time-slice. Il thread successivo con la stessa priorità viene inserito nel primo campo delle informazioni. Se questo valore è lo stesso del thread corrente, non è stato eseguito alcun intervallo di tempo.

- Campo informazioni 1: puntatore al thread successivo da eseguire.
- Campo Info 2: Numero di interrupt annidati.
- Campo informazioni 3: flag di disabilitazione della preemption interna.
- Campo informazioni 4: valore del puntatore dello stack durante la chiamata.

### <a name="running"></a>In esecuzione

#### <a name="running-in-context"></a>Esecuzione nel contesto

**Icona** ![ Icona In esecuzione](./media/user-guide/tx-events/image6.png)

**Descrizione**

Questo evento rappresenta l'esecuzione all'interno di un contesto di thread o di un sistema inattivo. Viene usato per illustrare le modifiche successive nel contesto in seguito a un'interruzione.

**Campi di informazioni**
- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="block-allocate"></a>Blocca allocazione 

#### <a name="tx_block_allocate"></a>tx_block_allocate

**Icona** ![ Icona di allocazione del blocco](./media/user-guide/tx-events/image7.png)

**Descrizione**

Questo evento rappresenta l'allocazione di un blocco di memoria tramite tx_block_allocate. In caso di esito positivo, l'indirizzo del blocco allocato viene restituito nel secondo campo di informazioni.

**Campi di informazioni**
- Campo informazioni 1: puntatore al pool di blocchi corrispondente.
- Campo informazioni 2: puntatore al blocco di memoria restituito (se l'operazione riesce).
- Campo informazioni 3: opzione di attesa fornita alla tx_block_allocate chiamata.
- Campo informazioni 4: blocchi rimanenti disponibili nel pool dopo questa allocazione.

### <a name="block-pool-create"></a>Creazione del pool di blocchi

#### <a name="tx_block_pool_create"></a>tx_block_pool_create

**Icona** ![ Icona di creazione del pool di blocchi](./media/user-guide/tx-events/image8.png)

**Descrizione**

Questo evento rappresenta la creazione di un pool di blocchi di memoria tramite tx_block_pool_create.

**Campi di informazioni**

- Info Field 1: puntatore al blocco di controllo del pool di blocchi corrispondente.
- Campo informazioni 2: puntatore all'area di memoria iniziale del pool.
- Campo informazioni 3: numero di blocchi nel pool. Campo informazioni 4: dimensioni in byte di ogni blocco nel pool.

### <a name="block-pool-delete"></a>Eliminazione pool a blocchi

#### <a name="tx_block_pool_delete"></a>tx_block_pool_delete

**Icona** ![ Icona di eliminazione del pool in blocchi](./media/user-guide/tx-events/image9.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un pool di blocchi di memoria tramite tx_block_pool_delete.

**Campi di informazioni**

- Campo informazioni 1: puntatore al blocco di controllo del pool di blocchi.
- Campo informazioni 2: valore del puntatore dello stack durante la chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="block-pool-information-get"></a>Ottenere informazioni sul pool di blocchi 

#### <a name="tx_block_pool_info_get"></a>tx_block_pool_info_get

**Icona** ![ Icona Ottieni informazioni sul pool di blocchi](./media/user-guide/tx-events/image10.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su un pool di blocchi di memoria tramite tx_block_pool_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al blocco di controllo del pool di blocchi.
- Campo informazioni 2: valore del puntatore dello stack durante la chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="block-pool-performance-information-get"></a>Ottenere informazioni sulle prestazioni del pool di blocchi

#### <a name="tx_block_pool_performance_info_get"></a>tx_block_pool_performance_info_get

**Icona** ![ Icona ottieni informazioni sulle prestazioni del pool di blocchi](./media/user-guide/tx-events/image11.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni di un pool di blocchi di memoria tramite tx_block_pool_performance_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al blocco di controllo del pool di blocchi.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="block-pool-performance-system-information-get"></a>Ottenere le prestazioni del pool System Information blocchi

#### <a name="tx_block_pool_performance_system_info_get"></a>tx_block_pool_performance_system_info_get

**Icona** ![ Icona Ottieni informazioni sul sistema per le prestazioni del pool di blocchi](./media/user-guide/tx-events/image12.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni di tutti i pool di blocchi di memoria tramite tx_block_pool_performance_system_info_get.

**Campi di informazioni**
- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="block-pool-prioritize"></a>Classificare in ordine di priorità i pool di blocchi

#### <a name="tx_block_pool_prioritize"></a>tx_block_pool_prioritize

**Icona** ![ Icona di assegnazione delle priorità ai pool di blocchi](./media/user-guide/tx-events/image13.png)

**Descrizione**

Questo evento rappresenta l'inserimento del thread sospeso con priorità più elevata all'inizio dell'elenco di sospensione del pool di blocchi. Se questa operazione viene eseguita prima di chiamare tx_block_release, il thread sospeso con priorità più alta riceverà il blocco rilasciato.

**Campi di informazioni**
- Campo informazioni 1: puntatore del pool di blocchi di memoria.
- Campo informazioni 2: numero di thread sospesi in questo pool di blocchi.
- Campo informazioni 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: Non usato.

### <a name="block-release"></a>Blocca versione 

#### <a name="tx_block_release"></a>tx_block_release

**Icona** ![ Icona Blocca versione](./media/user-guide/tx-events/image14.png)

**Descrizione**

Questo evento rappresenta il rilascio di un blocco allocato in precedenza al pool di blocchi.

**Campi di informazioni**

- Campo informazioni 1: puntatore del pool di blocchi di memoria.
- Campo informazioni 2: puntatore al blocco da rilasciare.
- Campo informazioni 3: numero di thread sospesi in questo pool di blocchi.
- Campo informazioni 4: puntatore dello stack al momento della chiamata.

### <a name="byte-allocate"></a>Byte Allocate 

#### <a name="tx_byte_allocate"></a>tx_byte_allocate

**Icona** ![ Icona di allocazione byte](./media/user-guide/tx-events/image15.png)

**Descrizione**

Questo evento rappresenta l'allocazione di memoria tramite tx_byte_allocate. In caso di esito positivo, l'indirizzo della memoria allocata viene restituito nel secondo campo di informazioni.

**Campi di informazioni**
- Campo informazioni 1: puntatore al pool di byte corrispondente.
- Campo informazioni 2: puntatore alla memoria restituita (in caso di esito positivo).
- Campo informazioni 3: numero di byte richiesti. Campo informazioni 4: opzione di attesa fornita al tx_byte_allocate chiamata.

### <a name="byte-pool-create"></a>Creazione pool di byte

#### <a name="tx_byte_pool_create"></a>tx_byte_pool_create

**Icona** ![ Icona di creazione del pool di byte](./media/user-guide/tx-events/image16.png)

**Descrizione**

Questo evento rappresenta la creazione di un pool di byte tramite tx_byte_pool_create.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pool di byte corrispondente.
- Campo informazioni 2: puntatore all'inizio dell'area di memoria. Campo informazioni 3: numero di byte nel pool di byte.
- Campo informazioni 4: puntatore dello stack al momento della chiamata.

### <a name="byte-pool-delete"></a>Eliminazione pool di byte 

#### <a name="tx_byte_pool_delete"></a>tx_byte_pool_delete

**Icona** ![ Icona di eliminazione del pool di byte](./media/user-guide/tx-events/image17.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un pool di byte tramite tx_byte_pool_delete.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pool di byte corrispondente.
- Campo informazioni 2: puntatore dello stack al momento della chiamata.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="byte-pool-information-get"></a>Ottenere informazioni sul pool di byte

#### <a name="tx_byte_pool_info_get"></a>tx_byte_pool_info_get

**Icona** ![ Icona ottieni informazioni sul pool di byte](./media/user-guide/tx-events/image18.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sul pool di byte tramite tx_byte_pool_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pool di byte corrispondente.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="byte-pool-performance-info-get"></a>Ottenere informazioni sulle prestazioni del pool di byte 

#### <a name="tx_byte_pool_info_get"></a>tx_byte_pool_info_get

**Icona** ![ Icona ottieni informazioni sulle prestazioni del pool di byte](./media/user-guide/tx-events/image19.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni del pool di byte tramite tx_byte_pool_performance_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pool di byte corrispondente.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="byte-pool-performance-system-info-get"></a>Ottenere informazioni sul sistema per le prestazioni del pool di byte 

#### <a name="tx_byte_pool_performance_system_info_get"></a>tx_byte_pool_performance_system_info_get

**Icona** ![ Icona ottieni informazioni sul sistema per le prestazioni del pool di byte](./media/user-guide/tx-events/image20.png)

**Descrizione**

Questo evento rappresenta il recupero delle informazioni sul sistema delle prestazioni del pool di byte tramite tx_byte_pool_performance_system_info_get.

**Campi di informazioni**

- Info Campo 1: Non usato.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="byte-pool-prioritize"></a>Priorità pool di byte

#### <a name="tx_byte_pool_prioritize"></a>tx_byte_pool_prioritize

**Icona** ![ Icona di assegnazione delle priorità del pool di byte](./media/user-guide/tx-events/image21.png)

**Descrizione**

Questo evento rappresenta la priorità dell'elenco di sospensione del pool di byte tramite tx_byte_pool_prioritize.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pool di byte corrispondente.
- Campo informazioni 2: numero di thread attualmente sospesi nel pool di byte.
- Campo informazioni 3: Puntatore dello stack al momento della chiamata.
- Campo info 4: Non usato.

### <a name="byte-release"></a>Versione byte

#### <a name="tx_byte_release"></a>tx_byte_release

**Icona** ![ Icona di rilascio dei byte](./media/user-guide/tx-events/image22.png)

**Descrizione**

Questo evento rappresenta il rilascio di un blocco di memoria allocato da un pool di byte tramite tx_byte_release.

**Campi di informazioni**

- Campo informazioni 1: puntatore al pool di byte corrispondente.
- Campo informazioni 2: puntatore alla memoria del pool di byte allocata in precedenza.
- Campo informazioni 3: numero di thread sospesi in questo pool di byte.
- Campo informazioni 4: numero di byte di memoria disponibili.

### <a name="event-flags-create"></a>Creazione di flag di evento 

#### <a name="tx_event_flags_create"></a>tx_event_flags_create

**Icona** ![ Icona di creazione dei flag di evento](./media/user-guide/tx-events/image23.png)

**Descrizione**

Questo evento rappresenta la creazione di un nuovo gruppo di flag di evento tramite tx_event_flags_create.

**Campi di informazioni** 
- Campo informazioni 1: puntatore al blocco di controllo del gruppo di flag di evento.
- Campo informazioni 2: Puntatore dello stack al momento della chiamata.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="event-flags-delete"></a>Eliminazione dei flag di evento 

#### <a name="tx_event_flags_delete"></a>tx_event_flags_delete

**Icona** ![ Icona di eliminazione dei flag di evento](./media/user-guide/tx-events/image24.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un gruppo di flag di evento tramite tx_event_flags_delete.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al gruppo di flag di evento.
- Campo informazioni 2: Puntatore dello stack al momento della chiamata.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="event-flags-get"></a>Get dei flag di evento 

#### <a name="tx_event_flags_get"></a>tx_event_flags_get

**Icona** ![ Icona Flag di evento >](./media/user-guide/tx-events/image25.png)

**Descrizione**

Questo evento rappresenta il recupero di flag di evento da un gruppo di flag di evento esistente tramite tx_event_flags_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al gruppo di flag di evento.
- Campo informazioni 2: flag di evento richiesti.
- Campo informazioni 3: flag di evento attualmente impostati nel gruppo.
- Info Field 4: opzione richiesta per i flag di evento get.

### <a name="event-flags-information-get"></a>Informazioni sui flag di evento Get

#### <a name="tx_event_flags_info_get"></a>tx_event_flags_info_get

**Icona** ![ Icona get delle informazioni sui flag di evento](./media/user-guide/tx-events/image26.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al gruppo di flag di evento.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="event-flags-performance-information-get"></a>Informazioni sulle prestazioni dei flag di evento Get 

#### <a name="tx_event_flags_performance_info_get"></a>tx_event_flags_performance_info_get

**Icona** ![ Icona get delle informazioni sulle prestazioni dei flag di evento](./media/user-guide/tx-events/image27.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_performance_info_get.

**Campi di informazioni** 
- Campo informazioni 1: puntatore al gruppo di flag di evento.
- Campo informazioni 2: Non usato
- Campo informazioni 3: Non usato
- Campo informazioni 4: Non usato

### <a name="event-flags-performance-system-info-get"></a>Event Flags Performance System Info Get

#### <a name="tx_event_flags_performance_system_info_get"></a>tx_event_flags_performance_system_info_get

**Icona** ![ Icona get delle informazioni di sistema sulle prestazioni dei flag di evento](./media/user-guide/tx-events/image28.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_performance_system_info_get.

**Campi di informazioni**
- Info Campo 1: Non usato.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="event-flags-set"></a>Flag di evento impostati 

#### <a name="tx_event_flags_set"></a>tx_event_flags_set

**Icona** ![ Icona di impostazione dei flag di evento](./media/user-guide/tx-events/image29.png)

**Descrizione**

Questo evento rappresenta l'impostazione (o la cancellazione) dei flag di evento in un gruppo di flag di evento esistente tramite tx_event_flags_set.

**Campi di informazioni**

- Campo informazioni 1: puntatore al gruppo di flag di evento.
- Campo informazioni 2: flag di evento da impostare (o cancellare).
- Campo informazioni 3: opzione del flag di evento AND o OR.
- Campo informazioni 4: numero di thread sospesi nel gruppo di flag di eventi.

### <a name="event-flags-set-notify"></a>Notifica dell'impostazione dei flag di evento

#### <a name="tx_event_flags_set_notify"></a>tx_event_flags_set_notify

**Icona** ![ Icona di notifica impostata per i flag di evento](./media/user-guide/tx-events/image30.png)

**Descrizione**

Questo evento rappresenta la registrazione di un callback di notifica per qualsiasi operazione di impostazione del flag di evento in un gruppo di flag di evento esistente tramite tx_event_flags_set_notify.

**Campi di informazioni**

- Campo informazioni 1: puntatore al gruppo di flag di evento.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="interrupt-control"></a>Controllo interrupt 

#### <a name="tx_interrupt_control"></a>tx_interrupt_control

**Icona** ![ Icona del controllo Interrupt](./media/user-guide/tx-events/image31.png)

**Descrizione**

Questo evento rappresenta la modifica della posizione di blocco dell'interrupt del processore tramite tx_interrupt_control.

**Campi di informazioni**

- Info Field 1: New interrupt posture (Campo info 1): nuova posizione di interruzione.
- Campo informazioni 2: Puntatore dello stack al momento della chiamata.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="mutex-create"></a>Creazione mutex 

#### <a name="tx_mutex_create"></a>tx_mutex_create

**Icona** ![ Icona di creazione mutex](./media/user-guide/tx-events/image32.png)

**Descrizione**

Questo evento rappresenta la creazione di un mutex tramite tx_mutex_create.

**Campi di informazioni**

- Info Field 1: Puntatore al blocco di controllo mutex.
- Campo informazioni 2: opzione di ereditarietà della priorità
- (TX_INHERIT o TX_NO_INHERIT).
- Campo informazioni 3: Puntatore dello stack al momento della chiamata.
- Campo info 4: Non usato.

### <a name="mutex-delete"></a>Eliminazione mutex 

#### <a name="tx_mutex_delete"></a>tx_mutex_delete

**Icona** ![ Icona di eliminazione mutex](./media/user-guide/tx-events/image33.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un mutex tramite tx_mutex_delete.

**Campi di informazioni** 

- Info Campo 1: Puntatore al mutex.
- Campo informazioni 2: Puntatore dello stack al momento della chiamata.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="mutex-get"></a>Mutex Get 

#### <a name="tx_mutex_get"></a>tx_mutex_get

**Icona** ![ Icona di mutex get](./media/user-guide/tx-events/image34.png)

**Descrizione**

Questo evento rappresenta l'ottenimento di un mutex tramite tx_mutex_get.

**Campi di informazioni**

- Info Campo 1: Puntatore al mutex.
- Campo info 2: l'opzione di attesa fornita alla tx_mutex_get chiamata.
- Campo informazioni 3: puntatore al thread proprietario del mutex (NULL implica che il mutex non è di proprietà).
- Campo informazioni 4: numero di volte in cui il thread proprietario ha chiamato tx_mutex_get.

### <a name="mutex-information-get"></a>Ottenere informazioni sui mutex

#### <a name="tx_mutex_info_get"></a>tx_mutex_info_get

**Icona** ![ Icona Di visualizzazione delle informazioni sui mutex](./media/user-guide/tx-events/image35.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni mutex tramite tx_mutex_info_get.

**Campi di informazioni**

- Info Campo 1: Puntatore al mutex.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="mutex-performance-information-get"></a>Ottenere informazioni sulle prestazioni del mutex 

#### <a name="tx_mutex_performance_info_get"></a>tx_mutex_performance_info_get

**Icona** ![ Icona ottieni informazioni sulle prestazioni mutex](./media/user-guide/tx-events/image36.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni del mutex tramite tx_mutex_performance_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al mutex.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="mutex-performance-system-info-get"></a>Mutex Performance System Info Get

#### <a name="tx_mutex_performance_system_info_get"></a>tx_mutex_performance_system_info_get

**Icona** ![ Icona ottieni informazioni sul sistema per le prestazioni mutex](./media/user-guide/tx-events/image37.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni del sistema mutex tramite tx_mutex_performance_system_info_get.

**Campi di informazioni**

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="mutex-prioritize"></a>Assegnare priorità ai mutex 

#### <a name="tx_mutex_prioritize"></a>tx_mutex_prioritize

**Icona** ![ Icona di assegnazione delle priorità mutex](./media/user-guide/tx-events/image38.png)

**Descrizione**

Questo evento rappresenta la priorità dell'elenco delle sospensioni del mutex tramite tx_mutex_prioritize.

**Campi di informazioni**

- Info Field 1: puntatore al mutex corrispondente.
- Campo informazioni 2: numero di thread attualmente sospesi nel mutex.
- Campo informazioni 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: Non usato.

### <a name="mutex-put"></a>Mutex Put 

#### <a name="tx_mutex_put"></a>tx_mutex_put

**Icona** ![ Icona Disassocazione mutex](./media/user-guide/tx-events/image39.png)

**Descrizione**

Questo evento rappresenta il rilascio di un mutex di proprietà in precedenza tramite tx_mutex_put.

**Campi di informazioni**

- Info Field 1: puntatore al mutex corrispondente.
- Campo informazioni 2: puntatore del thread proprietario del mutex.
- Campo informazioni 3: numero di richieste get mutex in sospeso.
- Campo informazioni 4: puntatore dello stack al momento della chiamata.

### <a name="queue-create"></a>Creazione coda 

#### <a name="tx_queue_create"></a>tx_queue_create

**Icona** ![ Icona di creazione della coda](./media/user-guide/tx-events/image40.png)

**Descrizione**

Questo evento rappresenta la creazione di una coda di messaggi tramite tx_queue_create.

**Campi di informazioni**

- Campo informazioni 1: puntatore al blocco di controllo della coda.
- Campo informazioni 2: dimensione del messaggio, in termini di parole a 32 bit.
- Campo informazioni 3: puntatore all'inizio dell'area di memoria della coda.
- Campo informazioni 4: numero di byte nell'area di memoria della coda.

### <a name="queue-delete"></a>Eliminazione coda 

#### <a name="tx_queue_delete"></a>tx_queue_delete

**Icona** ![ Icona di eliminazione della coda](./media/user-guide/tx-events/image41.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di una coda tramite tx_queue_delete.

**Campi di informazioni**

- Campo informazioni 1: puntatore alla coda.
- Campo informazioni 2: puntatore dello stack al momento della chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="queue-flush"></a>Scaricamento coda 

#### <a name="tx_queue_flush"></a>tx_queue_flush

**Icona** ![ Icona di scaricamento della coda](./media/user-guide/tx-events/image42.png)

**Descrizione**

Questo evento rappresenta lo scaricamento (cancellazione di tutto il contenuto della coda) di una coda tramite tx_queue_flush.

**Campi di informazioni**

- Campo informazioni 1: puntatore alla coda.
- Campo informazioni 2: puntatore dello stack al momento della chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="queue-front-send"></a>Front-send della coda 

#### <a name="tx_queue_front_send"></a>tx_queue_front_send

**Icona** ![ Icona di front-send della coda](./media/user-guide/tx-events/image43.png)

**Descrizione**

Questo evento rappresenta l'invio di un messaggio all'inizio di una coda tramite tx_queue_front_send.

**Campi di informazioni**

- Campo informazioni 1: puntatore alla coda.
- Campo informazioni 2: puntatore all'inizio del messaggio.
- Campo informazioni 3: opzione wait fornita al
- tx_queue_front_send chiamata.
- Campo informazioni 4: numero di messaggi già accodati.

### <a name="queue-information-get"></a>Ottenere informazioni sulla coda 

#### <a name="tx_queue_info_get"></a>tx_queue_info_get

**Icona** ![ Icona Ottieni informazioni sulla coda](./media/user-guide/tx-events/image44.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su una coda tramite tx_queue_info_get.

**Campi di informazioni** 
- Campo informazioni 1: puntatore alla coda.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="queue-performance-info-get"></a>Ottenere informazioni sulle prestazioni della coda 

#### <a name="tx_queue_performance_info_get"></a>tx_queue_performance_info_get

**Icona** ![ Icona ottieni informazioni sulle prestazioni della coda](./media/user-guide/tx-events/image45.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni di una coda tramite tx_queue_performance_info_get.

**Campi di informazioni** 

- Campo informazioni 1: puntatore alla coda.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="queue-performance-system-info-get"></a>Ottenere informazioni di sistema sulle prestazioni della coda 

#### <a name="tx_queue_performance_system_info_get"></a>tx_queue_performance_system_info_get

**Icona** ![ Icona Ottieni informazioni sul sistema per le prestazioni della coda](./media/user-guide/tx-events/image46.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni del sistema relative a tutte le code nel sistema.

**Campi di informazioni**

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="queue-prioritize"></a>Classificare le code in ordine di priorità 

#### <a name="tx_queue_prioritize"></a>tx_queue_prioritize

**Icona** ![ Icona di assegnazione delle priorità alle code](./media/user-guide/tx-events/image47.png)

**Descrizione**

Questo evento rappresenta l'assegnazione delle priorità all'elenco di sospensione della coda tramite tx_queue_prioritize.

**Campi di informazioni** 

- Info Field 1: puntatore alla coda corrispondente.
- Campo informazioni 2: numero di thread attualmente sospesi nella coda.
- Campo informazioni 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: Non usato.

#### <a name="queue-receive"></a>Ricezione coda 

##### <a name="tx_queue_receive"></a>tx_queue_receive

**Icona** ![ Icona di ricezione della coda](./media/user-guide/tx-events/image48.png)

**Descrizione**

Questo evento rappresenta la ricezione di un messaggio da una coda tramite tx_queue_receive.

**Campi di informazioni** 

- Campo informazioni 1: puntatore alla coda.
- Campo informazioni 2: puntatore alla destinazione del messaggio. Campo informazioni 3: opzione wait fornita alla chiamata.
- Campo informazioni 4: numero di messaggi attualmente in coda.

### <a name="queue-send"></a>Invio in coda 

#### <a name="tx_queue_send"></a>tx_queue_send

**Icona** ![ Icona di invio in coda](./media/user-guide/tx-events/image49.png)

**Descrizione**

Questo evento rappresenta l'invio di un messaggio a una coda tramite tx_queue_send.

**Campi di informazioni** 

- Campo informazioni 1: puntatore alla coda.
- Campo informazioni 2: puntatore al messaggio.
- Campo informazioni 3: opzione wait fornita alla chiamata.
- Campo informazioni 4: numero di messaggi attualmente in coda.

### <a name="queue-send-notify"></a>Notifica di invio coda 

#### <a name="tx_queue_send_notify"></a>tx_queue_send_notify

**Icona** ![ Icona di notifica dell'invio in coda](./media/user-guide/tx-events/image50.png)

**Descrizione**

<p>Questo evento rappresenta la registrazione di un callback tramite tx_queue_send_notify che viene chiamato ogni volta che un messaggio viene inviato a una coda.

**Campi di informazioni** 

- Campo informazioni 1: puntatore alla coda.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="semaphore-ceiling-put"></a>Semaphore Ceiling Put 

#### <a name="tx_semaphore_ceiling_put"></a>tx_semaphore_ceiling_put

**Icona** ![ Icona Semaphore ceiling put](./media/user-guide/tx-events/image51.png)

**Descrizione**

Questo evento rappresenta l'inserimento in un semaforo tramite tx_semaphore_ceiling_put. Questo comportamento è diverso tx_semaphore_put perché il valore massimo del semaforo viene esaminato in modo che l'operazione put non sia autorizzata a superare il valore massimo o il limite massimo.

**Campi di informazioni**

- Campo informazioni 1: puntatore al semaforo.
- Campo informazioni 2: conteggio semaforo corrente.
- Campo informazioni 3: numero di thread sospesi nel semaforo.
- Campo informazioni 4: limite massimo fornito alla chiamata.

#### <a name="semaphore-create"></a>Creazione del semaforo 

##### <a name="tx_semaphore_create"></a>tx_semaphore_create

**Icona** ![ Icona Crea semaforo](./media/user-guide/tx-events/image52.png)

**Descrizione**

Questo evento rappresenta la creazione di un semaforo tramite tx_semaphore_create.

**Campi di informazioni**

- Info Field 1: puntatore al blocco di controllo semaforo.
- Campo informazioni 2: conteggio semaforo iniziale.
- Campo informazioni 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: Non usato.

### <a name="semaphore-delete"></a>Eliminazione del semaforo 

#### <a name="tx_semaphore_delete"></a>tx_semaphore_delete

**Icona** ![ Icona di eliminazione del semaforo](./media/user-guide/tx-events/image53.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un semaforo tramite tx_semaphore_delete.

**Campi di informazioni**

- Campo informazioni 1: puntatore al semaforo.
- nfo Campo 2: puntatore dello stack al momento della chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="semaphore-get"></a>Get del semaforo 

#### <a name="tx_semaphore_get"></a>tx_semaphore_get

**Icona** ![ Icona Ottieni semaforo](./media/user-guide/tx-events/image54.png)

**Descrizione**

Questo evento rappresenta l'acquisizione di un semaforo tramite tx_semaphore_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al semaforo.
- Campo informazioni 2: opzione wait fornita alla chiamata.
- Campo informazioni 3: conteggio semaforo corrente.
- Campo informazioni 4: puntatore dello stack al momento della chiamata.

### <a name="semaphore-information-get"></a>Ottenere informazioni sul semaforo 

#### <a name="tx_semaphore_info_get"></a>tx_semaphore_info_get

**Icona** ![ Icona Ottieni informazioni semaforo](./media/user-guide/tx-events/image55.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni su un semaforo tramite tx_semaphore_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al semaforo.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="semaphore-performance-info-get"></a>Ottenere informazioni sulle prestazioni del semaforo 

#### <a name="tx_semaphore_performance_info_get"></a>tx_semaphore_performance_info_get

**Icona** ![ Icona Ottieni informazioni sulle prestazioni del semaforo](./media/user-guide/tx-events/image56.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni relative a un semaforo tramite tx_semaphore_performance_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al semaforo.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="semaphore-performance-system-info"></a>Informazioni sistema prestazioni semaforo 

#### <a name="tx_semaphore_performance_system_info_get"></a>tx_semaphore_performance_system_info_get

**Icona** ![ Icona informazioni sistema prestazioni semaforo](./media/user-guide/tx-events/image57.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni su tutti i semafori nel sistema tramite tx_semaphore_performance_system_info_get.

**Campi di informazioni** 

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="semaphore-prioritize"></a>Assegnare priorità al semaforo 

#### <a name="tx_semaphore_prioritize"></a>tx_semaphore_prioritize

**Icona** ![ Icona di assegnazione delle priorità al semaforo](./media/user-guide/tx-events/image58.png)

**Descrizione**

Questo evento rappresenta la priorità dell'elenco delle sospensioni del semaforo tramite tx_semaphore_prioritize.

**Campi di informazioni**

- Info Field 1: puntatore al semaforo corrispondente.
- Campo informazioni 2: numero di thread attualmente sospesi nel semaforo.
- Campo informazioni 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: Non usato.

### <a name="semaphore-put"></a>Semaphore Put 

#### <a name="tx_semaphore_put"></a>tx_semaphore_put

**Icona** ![ Icona Put del semaforo](./media/user-guide/tx-events/image59.png)

**Descrizione**

Questo evento rappresenta il rilascio di un'istanza del semaforo tramite tx_semaphore_put.

**Campi di informazioni** 

- Info Field 1: puntatore al semaforo corrispondente. Campo informazioni 2: conteggio semaforo corrente.
- Campo informazioni 3: numero di thread sospesi nel semaforo.
- Campo informazioni 4: puntatore dello stack al momento della chiamata.

### <a name="semaphore-put-notify"></a>Notifica Put del semaforo 

#### <a name="tx_semaphore_put_notify"></a>tx_semaphore_put_notify

**Icona** ![ Icona Invia notifica del semaforo](./media/user-guide/tx-events/image60.png)

**Descrizione**

Questo evento rappresenta la registrazione di un callback tramite tx_semaphore_put_notify chiamato ogni volta che viene inserita un'istanza del semaforo.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al semaforo.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="thread-create"></a>Creazione di thread 

#### <a name="tx_thread_create"></a>tx_thread_create

**Icona** ![ Icona crea thread](./media/user-guide/tx-events/image61.png)

**Descrizione**

Questo evento rappresenta la creazione di un thread tramite tx_thread_create.

**Campi di informazioni**

- Campo informazioni 1: puntatore al blocco di controllo del thread.
- Campo informazioni 2: priorità del thread.
- Campo informazioni 3: puntatore dello stack per thread.
- nfo Campo 4: dimensioni dello stack in byte.

### <a name="thread-delete"></a>Eliminazione thread 

#### <a name="tx_thread_delete"></a>tx_thread_delete

**Icona** ![ Icona di eliminazione thread](./media/user-guide/tx-events/image62.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un thread tramite tx_thread_delete.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al thread.
- Campo informazioni 2: puntatore dello stack al momento della chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="thread-entryexit-notify"></a>Notifica di ingresso/uscita del thread 

#### <a name="tx_thread_entry_exit_notify"></a>tx_thread_entry_exit_notify

**Icona** ![ Icona di notifica di ingresso/uscita del thread](./media/user-guide/tx-events/image63.png)

**Descrizione**

Questo evento rappresenta la registrazione di un callback tramite tx_thread_entry_exit_notify che viene chiamato ogni volta che un thread viene immesso o chiuso.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al thread.
- Campo informazioni 2: stato del thread al momento della registrazione.
- Campo informazioni 3: puntatore allo stack al momento della chiamata.
- Campo informazioni 4: Non usato.

#### <a name="thread-identify"></a>Identificazione thread 

##### <a name="tx_thread_identify"></a>tx_thread_identify

**Icona** ![ Icona di identificazione thread](./media/user-guide/tx-events/image64.png)

**Descrizione**

Questo evento rappresenta il recupero del puntatore del thread corrente tramite tx_thread_identify.

**Campi di informazioni**

- Campo informazioni 1: non usato.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="thread-information-get"></a>Ottenere informazioni sui thread 

#### <a name="tx_thread_info_get"></a>tx_thread_info_get

**Icona** ![ Icona ottieni informazioni thread](./media/user-guide/tx-events/image65.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sul thread specificato tramite tx_thread_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al thread.
- Campo informazioni 2: stato del thread al momento della chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

#### <a name="thread-performance-information-get"></a>Ottenere informazioni sulle prestazioni dei thread 

##### <a name="tx_thread_performance_info_get"></a>tx_thread_performance_info_get

**Icona** ![ Icona get delle informazioni sulle prestazioni dei thread](./media/user-guide/tx-events/image66.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni sul thread specificato tramite tx_thread_performance_info_get.

**Campi di informazioni**

- Info Campo 1: Puntatore al thread.
- Campo informazioni 2: stato del thread al momento della chiamata.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="thread-performance-system-info-get"></a>Ottenere informazioni sul sistema per le prestazioni dei thread 

#### <a name="tx_thread_performance_system_info_get"></a>tx_thread_performance_system_info_get

**Icona** ![ Icona Ottieni informazioni sul sistema per le prestazioni dei thread](./media/user-guide/tx-events/image67.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sulle prestazioni di tutti i thread tramite tx_thread_performance_system_info_get.

**Campi di informazioni** 

- Info Campo 1: Non usato.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="thread-preemption-change"></a>Modifica di preemption dei thread 

#### <a name="tx_thread_preemption_change"></a>tx_thread_preemption_change

**Icona** ![ Icona di modifica della preemption dei thread](./media/user-guide/tx-events/image68.png)

**Descrizione**

Questo evento rappresenta la modifica della soglia di preemption di un thread tramite tx_thread_preemption_change.

**Campi di informazioni** 

- Info Campo 1: Puntatore al thread.
- Info Campo 2: nuova soglia di preemption.
- Info Field 3: Previous preemption-threshold.Info Field 3: Previous preemption-threshold.
- Campo informazioni 4: stato del thread al momento della chiamata.

### <a name="thread-priority-change"></a>Modifica della priorità dei thread 

#### <a name="tx_thread_priority_change"></a>tx_thread_priority_change

**Icona** ![ Icona di modifica della priorità dei thread](./media/user-guide/tx-events/image69.png)

**Descrizione**

Questo evento rappresenta la modifica della priorità di un thread tramite tx_thread_priority_change.

- Campi di informazioni 
- Info Campo 1: Puntatore al thread.
- Campo info 2: nuova priorità.
- Campo informazioni 3: priorità precedente.
- Campo informazioni 4: stato del thread al momento della chiamata.

### <a name="thread-relinquish"></a>Thread Relinquish 

#### <a name="tx_thread_relinquish"></a>tx_thread_relinquish

**Icona** ![ Icona Disinserzione thread](./media/user-guide/tx-events/image70.png)

**Descrizione**

Questo evento rappresenta la rinuncia del processore da un thread tramite tx_thread_relinquish.

**Campi di informazioni**

- Campo informazioni 1: Puntatore dello stack al momento della chiamata.
- Campo informazioni 2: puntatore al thread successivo da eseguire.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="thread-reset"></a>Reimpostazione dei thread 

#### <a name="tx_thread_reset"></a>tx_thread_reset

**Icona** ![ Icona reimpostazione thread](./media/user-guide/tx-events/image71.png)

**Descrizione**

Questo evento rappresenta la reimpostazione di un thread completato o terminato tramite tx_thread_reset.

**Campi di informazioni**

- Info Campo 1: Puntatore al thread.
- Campo informazioni 2: stato del thread al momento della chiamata.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

#### <a name="thread-resume"></a>Ripresa di thread 

##### <a name="tx_thread_resume"></a>tx_thread_resume

**Icona** ![ Icona Di ripresa thread](./media/user-guide/tx-events/image72.png)

**Descrizione**

Questo evento rappresenta la ripresa di un thread sospeso tramite tx_thread_resume.

**Campi di informazioni**

- Info Campo 1: Puntatore al thread.
- Campo informazioni 2: stato del thread al momento della chiamata.
- Campo informazioni 3: Puntatore dello stack al momento della chiamata.
- Campo info 4: Non usato.

### <a name="thread-sleep"></a>Sospensione dei thread 

#### <a name="tx_thread_sleep"></a>tx_thread_sleep

**Icona** ![ Icona sospensione thread](./media/user-guide/tx-events/image73.png)

**Descrizione**

Questo evento rappresenta la sospensione del thread corrente per un numero specificato di tick del timer tramite tx_thread_sleep.

**Campi di informazioni**

- Info Campo 1: numero di tick per cui sospendere.
- Campo informazioni 2: stato del thread al momento della chiamata.
- Campo informazioni 3: Puntatore dello stack al momento della chiamata.
- Campo info 4: Non usato.

### <a name="thread-stack-error-notify"></a>Notifica degli errori dello stack di thread 

#### <a name="tx_thread_stack_error_notify_event"></a>tx_thread_stack_error_notify_event

**Icona** ![ Icona di notifica degli errori dello stack di thread](./media/user-guide/tx-events/image74.png)

**Descrizione**

Questo evento rappresenta la registrazione di una routine di notifica degli errori dello stack di thread tramite tx_thread_stack_error_notify_event.

**Campi di informazioni** 

- Info Campo 1: Non usato.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Campo info 4: Non usato.

### <a name="thread-suspend"></a>Sospensione dei thread 

#### <a name="tx_thread_suspend"></a>tx_thread_suspend

**Icona** ![ Icona Di sospensione thread](./media/user-guide/tx-events/image75.png)

**Descrizione**

Questo evento rappresenta la sospensione di un thread tramite tx_thread_suspend.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al thread da sospendere.
- Campo informazioni 2: stato del thread al momento della chiamata.
- Campo informazioni 3: Puntatore dello stack al momento della chiamata.
- Campo info 4: Non usato.

### <a name="thread-terminate"></a>Thread Terminate 

#### <a name="tx_thread_terminate"></a>tx_thread_terminate

**Icona** ![ Icona di terminazione del thread](./media/user-guide/tx-events/image76.png)

**Descrizione**

Questo evento rappresenta la chiusura di un thread tramite tx_thread_terminate.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al thread da terminare.
- Campo informazioni 2: stato del thread al momento della chiamata.
- Campo informazioni 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: Non usato.

### <a name="thread-time-slice-change"></a>Modifica Time-Slice thread 

#### <a name="tx_thread_time_slice_change"></a>tx_thread_time_slice_change

**Icona** ![ Icona di modifica dell'intervallo di tempo del thread](./media/user-guide/tx-events/image77.png)

**Descrizione**

Questo evento rappresenta la modifica dell'intervallo di tempo di un thread tramite tx_thread_time_slice_change.

**Campi di informazioni**

- Campo informazioni 1: puntatore al thread.
- Campo informazioni 2: nuovo intervallo di tempo.
- Campo informazioni 3: intervallo di tempo precedente.
- Campo informazioni 4: Non usato.

### <a name="thread-wait-abort"></a>Thread Wait Abort 

#### <a name="tx_thread_wait_abort"></a>tx_thread_wait_abort

**Icona** ![ Icona thread wait abort](./media/user-guide/tx-events/image78.png)

**Descrizione**

Questo evento rappresenta l'interruzione della sospensione di un thread tramite tx_thread_wait_abort.

**Campi di informazioni**

- Campo informazioni 1: puntatore al thread.
- Campo informazioni 2: stato del thread al momento della chiamata.
- Campo informazioni 3: puntatore dello stack al momento della chiamata.
- Campo informazioni 4: Non usato.

### <a name="time-get"></a>Time Get 

#### <a name="tx_time_get"></a>tx_time_get

**Icona** ![ Icona Time Get (Ottieni ora)](./media/user-guide/tx-events/image79.png)

**Descrizione**

Questo evento rappresenta il recupero del numero corrente di tick del timer tramite tx_time_get.

**Campi di informazioni**

- Campo informazioni 1: numero corrente di tick del timer.
- Campo informazioni 2: puntatore dello stack al momento della chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="time-set"></a>Set di tempo 

#### <a name="tx_time_set"></a>tx_time_set

**Icona** ![ Icona del set di tempo](./media/user-guide/tx-events/image80.png)

**Descrizione**

Questo evento rappresenta l'impostazione del numero corrente di tick del timer tramite tx_time_set.

**Campi di informazioni**

- Campo informazioni 1: nuovo numero di tick del timer.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="timer-activate"></a>Attivazione timer 

#### <a name="tx_timer_activate"></a>tx_timer_activate

**Icona** ![ Icona di attivazione timer](./media/user-guide/tx-events/image81.png)

**Descrizione**

Questo evento rappresenta l'attivazione del timer specificato tramite tx_timer_activate.

**Campi di informazioni**

- Campo informazioni 1: puntatore al timer.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="timer-change"></a>Modifica timer 

#### <a name="tx_timer_change"></a>tx_timer_change

**Icona** ![ Icona di modifica timer](./media/user-guide/tx-events/image82.png)

**Descrizione**

Questo evento rappresenta la modifica del timer specificato tramite tx_timer_change.

**Campi di informazioni**

- Campo informazioni 1: puntatore al timer.
- Campo informazioni 2: tick di scadenza iniziale.
- Campo informazioni 3: ripianificare i tick di scadenza.
- Campo informazioni 4: Non usato.

### <a name="timer-create"></a>Creazione timer 

#### <a name="tx_timer_create"></a>tx_timer_create

**Icona** ![ Icona di creazione timer](./media/user-guide/tx-events/image83.png)

**Descrizione**

Questo evento rappresenta la creazione di un timer tramite tx_timer_create.

**Campi di informazioni**

- Campo informazioni 1: puntatore al blocco di controllo timer.
- Campo informazioni 2: tick di scadenza iniziale.
- Campo informazioni 3: ripianificare i tick di scadenza.
- Campo informazioni 4: valore di abilitazione automatica, TX_AUTO_ACTIVATE (1) o TX_NO_ACTIVATE (0).

### <a name="timer-deactivate"></a>Disattivazione timer 

#### <a name="tx_timer_deactivate"></a>tx_timer_deactivate

**Icona** ![ Icona di disattivazione del timer](./media/user-guide/tx-events/image84.png)

**Descrizione**

Questo evento rappresenta la disattivazione di un timer tramite tx_timer_deactivate.

**Campi di informazioni**

- Campo informazioni 1: puntatore al timer.
- Campo informazioni 2: puntatore dello stack al momento della chiamata.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="timer-delete"></a>Eliminazione timer 

#### <a name="tx_timer_delete"></a>tx_timer_delete

**Icona** ![ Icona di eliminazione timer](./media/user-guide/tx-events/image85.png)

**Descrizione**

Questo evento rappresenta l'eliminazione di un timer tramite tx_timer_delete.

**Campi di informazioni** 

- Campo informazioni 1: puntatore al timer.
- Campo informazioni 2: Non usato.
- Campo informazioni 3: Non usato.
- Campo informazioni 4: Non usato.

### <a name="timer-information-get"></a>Ottenere informazioni sul timer 

#### <a name="tx_timer_info_get"></a>tx_timer_info_get

**Icona** ![ Icona Timer get information (Ottieni informazioni timer)](./media/user-guide/tx-events/image86.png)

**Descrizione**

Questo evento rappresenta il recupero di informazioni sul timer tramite tx_timer_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al timer.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="timer-performance-information-get"></a>Ottenere informazioni sulle prestazioni del timer 

#### <a name="tx_timer_performance_info_get"></a>tx_timer_performance_info_get

**Icona** ![ Icona Ottieni informazioni sulle prestazioni del timer](./media/user-guide/tx-events/image87.png)

**Descrizione** 

Questo evento rappresenta il recupero di informazioni sulle prestazioni del timer tramite tx_timer_performance_info_get.

**Campi di informazioni**

- Campo informazioni 1: puntatore al timer.
- Campo informazioni 2: puntatore stack al momento della chiamata.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.

### <a name="timer-system-performance-info-get"></a>Ottenere informazioni sulle prestazioni del sistema timer 

#### <a name="tx_timer_performance_system_info_get"></a>tx_timer_performance_system_info_get

**Icona** ![ Icona Ottieni informazioni sulle prestazioni del sistema timer](./media/user-guide/tx-events/image88.png)


**Descrizione** 

Questo evento rappresenta il recupero di tutte le informazioni sulle prestazioni del timer tramite tx_timer_performance_system_info_get.

**Campi di informazioni**

- Info Campo 1: Non usato.
- Info Campo 2: Non usato.
- Info Campo 3: Non usato.
- Info Campo 4: Non usato.