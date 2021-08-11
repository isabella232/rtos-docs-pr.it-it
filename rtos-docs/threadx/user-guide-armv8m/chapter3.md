---
title: Capitolo 3 - API ThreadX per ARMv8-M
description: Questo capitolo contiene una descrizione dei servizi ThreadX specifici di ARMv8-M.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 99633db55a5d93eb32ce4fb5429f3fe2f9ab5137cffc30b27982f702cece1ca5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791500"
---
# <a name="chapter-3--threadx-apis-for-armv8-m"></a>API ThreadX capitolo 3 per ARMv8-M

Questo capitolo contiene una descrizione dei servizi ThreadX specifici di ARMv8-M in ordine alfabetico. I nomi sono progettati in modo da raggruppare tutti i servizi simili. Nella sezione "Valori restituiti" delle descrizioni seguenti, i  valori in **GRASSETTO** non sono interessati dalla definizione TX_DISABLE_ERROR_CHECKING usata per disabilitare il controllo degli errori dell'API; mentre i valori visualizzati in grassetto sono completamente disabilitati.

- [tx_thread_secure_stack_allocate](#tx_thread_secure_stack_allocate) Allocare uno stack di thread nella memoria protetta.
- [tx_thread_secure_stack_free](#tx_thread_secure_stack_free) Stack di thread libero nella memoria protetta

## <a name="tx_thread_secure_stack_allocate"></a>tx_thread_secure_stack_allocate

Allocare uno stack di thread nella memoria protetta.

### <a name="prototype"></a>Prototipo

```c
UINT tx_thread_secure_stack_allocate(
    TX_THREAD *thread_ptr, 
    ULONG stack_size);
```

### <a name="description"></a>Descrizione

Questo servizio alloca uno stack di dimensioni stack_size byte in memoria sicura. Questa funzione deve essere chiamata per ogni thread che chiama funzioni sicure.

### <a name="input-parameters"></a>Parametri di input

- **thread_ptr** Puntatore al thread creato in precedenza.

- **stack_size** Dimensioni dello stack sicuro.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Richiesta riuscita.

- **TX_SIZE_ERROR** (0x05) Dimensioni dello stack non compreso nell'intervallo.

- **TX_THREAD_ERROR** (0x0E) Puntatore di thread non valido.

- **TX_NO_MEMORY** (0x10) Impossibile allocare memoria.

- **TX_CALLER_ERROR** (0x13) Chiamante non valido di questo servizio.

- **TX_FEATURE_NOT_ENABLED** (0xFF) Il sistema è stato compilato per l'esecuzione in modalità sicura.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create thread.  */
tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0, pointer, DEMO_STACK_SIZE, 1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);

/* Allocate secure stack so this thread can call secure functions.  */
status = tx_thread_secure_stack_allocate(&thread_0, 256);

/* If status is TX_SUCCESS the request was successful.  */
```

### <a name="see-also"></a>Vedere anche

tx_thread_secure_stack_free

##  <a name="tx_thread_secure_stack_free"></a>tx_thread_secure_stack_free

Liberare uno stack di thread nella memoria protetta. 

### <a name="prototype"></a>Prototipo

```c
UINT tx_thread_secure_stack_free(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio libera lo stack sicuro di un thread nella memoria protetta. Questa funzione deve essere chiamata se un thread ha uno stack sicuro e quando il thread non deve più chiamare funzioni protette o il thread viene eliminato.

### <a name="input-parameters"></a>Parametri di input

- **thread_ptr** Puntatore al thread creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Richiesta riuscita.

- **TX_THREAD_ERROR** (0x0E) Puntatore di thread non valido.

- **TX_CALLER_ERROR** (0x13) Chiamante non valido di questo servizio.

- **TX_FEATURE_NOT_ENABLED** (0xFF) Il sistema è stato compilato per l'esecuzione in modalità sicura.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Free thread’s secure stack.  */
status = tx_thread_secure_stack_free(&thread_0);

/* If status is TX_SUCCESS the request was successful.  */

/* Delete thread.  */
tx_thread_delete(&thread_0);
```

## <a name="see-also"></a>Vedere anche

tx_thread_secure_stack_allocate
