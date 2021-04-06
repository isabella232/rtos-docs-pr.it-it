---
title: Capitolo 2-riferimenti alle API del kit del profilo di esecuzione
description: Questo capitolo documenta le funzioni API fornite da EPK.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a198e48bdacbc141fb3de4670cc7ea5ba079612d
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377601"
---
#  <a name="chapter-2--execution-profile-kit-api-references"></a>Capitolo 2 riferimenti all'API del kit del profilo di esecuzione

Il EPK ThreadX fornisce funzioni di accesso per ottenere le informazioni sul profilo di esecuzione, come indicato di seguito.

| &nbsp;Nome funzione | Descrizione |
| --- | --- |
| _tx_execution_thread_time_reset | Reimposta il tempo accumulato per un thread. |
| _tx_execution_thread_total_time_reset | Reimposta il tempo totale di thread accumulato. |
| _tx_execution_isr_time_reset | Reimposta il tempo ISR accumulato. |
| _tx_execution_idle_time_reset | Reimposta il tempo di inattività accumulato. |
| _tx_execution_thread_time_get ottenere il tempo di accumulo per un thread. |
| _tx_execution_thread_total_time_get | Ottiene il tempo totale di thread accumulato. |
| _tx_execution_isr_time_get | Ottenere il tempo ISR accumulato. |
| _tx_execution_idle_time_get | Ottenere il tempo di inattività accumulato. |

##  <a name="_tx_execution_thread_time_reset"></a>_tx_execution_thread_time_reset

Reimposta il tempo accumulato per un thread.

### <a name="prototype"></a>Prototipo

```C
UINT _tx_execution_thread_time_reset(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio imposta di nuovo il tempo di esecuzione del thread accumulato su zero.

### <a name="input-parameters"></a>Parametri di input

- **thread_ptr** Puntatore al thread.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) reimpostazione EPK riuscita.

### <a name="allowed-from"></a>Consentito da

Thread, timer e ISRs

### <a name="example"></a>Esempio

```c
/* Reset the execution time for thread_0.  */
status =  tx_execution_thread_time_reset(&thread_0);

/* If status is TX_SUCCESS thread_0's execution time is now 0.  */
```

### <a name="see-also"></a>Vedere anche

- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_thread_total_time_reset"></a>_tx_execution_thread_total_time_reset

Reimposta il tempo totale di thread accumulato.

### <a name="prototype"></a>Prototipo
```c
UINT _tx_execution_thread_total_time_reset(void);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il tempo totale di esecuzione del thread accumulato su zero.

### <a name="input-parameters"></a>Parametri di input

Nessuna.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) reimpostazione EPK riuscita.

### <a name="allowed-from"></a>Consentito da

- Thread, timer e ISRs

### <a name="example"></a>Esempio

```c
/* Reset the total execution time for all threads.  */
status =  tx_execution_thread_total_time_reset();

/* If status is TX_SUCCESS the total thread execution time is now 0.  */
```

### <a name="see-also"></a>Vedere anche

- _tx_execution_thread_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_isr_time_reset"></a>_tx_execution_isr_time_reset

Reimposta il tempo ISR accumulato.

### <a name="prototype"></a>Prototipo

```c
UINT _tx_execution_isr_time_reset(void);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il tempo totale di esecuzione ISR accumulato su zero.

### <a name="input-parameters"></a>Parametri di input

Nessuna.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) reimpostazione EPK riuscita.

**Consentito da**

- Thread, timer e ISRs

**Esempio**

```c
/* Reset the total ISR execution time.  */
status =  tx_execution_isr_time_reset();

/* If status is TX_SUCCESS the total ISR execution time is now 0.  */
```

### <a name="see-also"></a>Vedere anche

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_idle_time_reset"></a>_tx_execution_idle_time_reset

Reimposta il tempo di inattività accumulato.

### <a name="prototype"></a>Prototipo

```c
UINT _tx_execution_idle_time_reset(void);
```

### <a name="description"></a>Descrizione

Questo servizio imposta su zero il tempo di esecuzione totale inattivo accumulato.

### <a name="input-parameters"></a>Parametri di input

Nessuna.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) reimpostazione EPK riuscita.

### <a name="allowed-from"></a>Consentito da

- Thread, timer e ISRs

### <a name="example"></a>Esempio

```c
/* Reset the total idle execution time.  */
status =  tx_execution_idle_time_reset();

/* If status is TX_SUCCESS the total idle execution time is now 0.  */
```

### <a name="see-also"></a>Vedere anche

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_thread_time_get"></a>_tx_execution_thread_time_get

Ottenere il tempo di accumulo per un thread.

### <a name="prototype"></a>Prototipo

```c
UINT _tx_execution_thread_time_get(
    TX_THREAD *thread_ptr,
    EXECUTION_TIME *total_time);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene il tempo di esecuzione accumulato per un thread.

### <a name="input-parameters"></a>Parametri di input

- **thread_ptr** Puntatore al thread.

- **Total_time** Destinazione per \' i tempi di esecuzione del thread.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) EPK tempo riuscito Get.

### <a name="allowed-from"></a>Consentito da

Thread, timer e ISRs

### <a name="example"></a>Esempio

```c

/* Get the total thread execution time for thread_0.  */
status =  tx_execution_thread_time_get(&thread_0, &execution_time);

/* If status is TX_SUCCESS, execution_time contains the thread's
   execution time.  */
```

### <a name="see-also"></a>Vedere anche

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_thread_total_time_get"></a>_tx_execution_thread_total_time_get

Ottiene il tempo totale di thread accumulato.

### <a name="prototype"></a>Prototipo

```c
UINT _tx_execution_thread_total_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene il tempo totale di esecuzione del thread accumulato.

### <a name="input-parameters"></a>Parametri di input

- **Total_time** Destinazione per il tempo totale di esecuzione del thread.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) EPK tempo riuscito Get.

### <a name="allowed-from"></a>Consentito da

- Thread, timer e ISRs

### <a name="example"></a>Esempio

```c
EXECUTION_TIME *execution_time;

/* Get the total thread execution time.  */
status =  tx_execution_thread_total_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the thread
   execution time.  */
```

### <a name="see-also"></a>Vedere anche

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_isr_time_get"></a>_tx_execution_isr_time_get

Ottenere il tempo ISR accumulato.

### <a name="prototype"></a>Prototipo

```c
UINT _tx_execution_isr_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene il tempo di esecuzione ISR accumulato.

### <a name="input-parameters"></a>Parametri di input

- **Total_time** Destinazione per il tempo di esecuzione ISR totale.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) EPK tempo riuscito Get.

### <a name="allowed-from"></a>Consentito da

Thread, timer e ISRs

### <a name="example"></a>Esempio

```c
EXECUTION_TIME  *execution_time;

/* Get the total ISR execution time.  */
status =  tx_execution_isr_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the ISR
   execution time.  */
```

### <a name="see-also"></a>Vedere anche

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_idle_time_get"></a>_tx_execution_idle_time_get

### <a name="get-the-accumulated-idle-time"></a>Ottenere il tempo di inattività accumulato

### <a name="prototype"></a>Prototipo

```c
UINT _tx_execution_idle_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene il tempo di esecuzione inattivo accumulato.

### <a name="input-parameters"></a>Parametri di input

- **Total_time** Destinazione per il tempo di esecuzione totale di inattività.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) EPK tempo riuscito Get.

### <a name="allowed-from"></a>Consentito da

- Thread, timer e ISRs

### <a name="example"></a>Esempio

```c
EXECUTION_TIME  *execution_time;

/* Get the total idle execution time.  */
status =  tx_execution_idle_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the idle
   execution time.  */
```

### <a name="see-also"></a>Vedere anche

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
