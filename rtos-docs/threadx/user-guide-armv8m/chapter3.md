---
title: Capitolo 3-API ThreadX per ARMv8-M
description: Questo capitolo descrive i servizi ThreadX specifici di ARMv8-M.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 14bdfab3d56476d52ba91f859cec4af4ab7f4bef
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377598"
---
# <a name="chapter-3--threadx-apis-for-armv8-m"></a>Capitolo 3 API ThreadX per ARMv8-M

Questo capitolo contiene una descrizione dei servizi ThreadX specifici di ARMv8-M in ordine alfabetico. I nomi sono progettati in modo da raggruppare tutti i servizi simili. Nella sezione "valori restituiti" nelle descrizioni seguenti i valori in **grassetto** non sono interessati dal **TX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API; mentre i valori visualizzati in non grassetto sono completamente disabilitati.

- [tx_thread_secure_stack_allocate](#tx_thread_secure_stack_allocate) Allocare uno stack di thread nella memoria protetta.
- [tx_thread_secure_stack_free](#tx_thread_secure_stack_free) Stack di thread libero in memoria protetta

## <a name="tx_thread_secure_stack_allocate"></a>tx_thread_secure_stack_allocate

Allocare uno stack di thread nella memoria protetta.

### <a name="prototype"></a>Prototipo

```c
UINT tx_thread_secure_stack_allocate(
    TX_THREAD *thread_ptr, 
    ULONG stack_size);
```

### <a name="description"></a>Descrizione

Questo servizio alloca uno stack di dimensioni stack_size byte nella memoria protetta. Questa funzione deve essere chiamata per ogni thread che chiama funzioni protette.

### <a name="input-parameters"></a>Parametri di input

- **thread_ptr** Puntatore al thread creato in precedenza.

- **stack_size** Dimensioni dello stack protetto.

### <a name="return-values"></a>Valori restituiti

- La richiesta di **TX_SUCCESS** (0x00) è riuscita.

- Dimensioni dello stack di **TX_SIZE_ERROR** (0x05) non comprese nell'intervallo.

- **TX_THREAD_ERROR** (0x0E) puntatore al thread non valido.

- **TX_NO_MEMORY** (0x10) non è in grado di allocare memoria.

- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.

- **TX_FEATURE_NOT_ENABLED** (0Xff) il sistema è stato compilato per l'esecuzione in modalità protetta.

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

Questo servizio libera lo stack sicuro di un thread nella memoria protetta. Questa funzione deve essere chiamata se un thread dispone di uno stack sicuro e quando il thread non deve più chiamare funzioni protette o se il thread viene eliminato.

### <a name="input-parameters"></a>Parametri di input

- **thread_ptr** Puntatore al thread creato in precedenza.

### <a name="return-values"></a>Valori restituiti

- La richiesta di **TX_SUCCESS** (0x00) è riuscita.

- **TX_THREAD_ERROR** (0x0E) puntatore al thread non valido.

- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.

- **TX_FEATURE_NOT_ENABLED** (0Xff) il sistema è stato compilato per l'esecuzione in modalità protetta.

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
