---
title: Capitolo 4 - API dei moduli
author: philmea
ms.author: philmea
description: Questo articolo è un riepilogo delle API aggiuntive disponibili per un modulo.
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1c7590d0ccddc606a6cacdfeb3b3a99631e125554b524c4ce65c8154e65a20ee
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799133"
---
# <a name="chapter-4---module-apis"></a>Capitolo 4 - API dei moduli

## <a name="summary-of-module-apis"></a>Riepilogo delle API dei moduli

Sono disponibili diverse funzioni API aggiuntive per un modulo, come indicato di seguito:

- ***txm_module_application_request** _ - _Application richiesta specifica al codice residente*
- ***txm_module_object_allocate** _ - Memoria _Allocate all'esterno del modulo per l'oggetto*
- ***txm_module_object_deallocate** _ - memoria _Deallocate oggetto allocata in precedenza*
- ***txm_module_object_pointer_get** _ - _Find oggetto di sistema e recuperare il puntatore a un oggetto*
- ***txm_module_object_pointer_get_extended** _ - _Find oggetto di sistema e recuperare il puntatore all'oggetto, sicurezza della lunghezza del nome*

## <a name="return-values"></a>Valori restituiti

Per alcune API Azure RTOS vengono restituiti altri codici di errore. Questi codici di errore aggiuntivi sono definiti come segue:

- **TXM_MODULE_INVALID_PROPERTIES** (0xF3): indica che il modulo non dispone delle proprietà corrette per effettuare una chiamata API. Ad esempio, chiamare le API di traccia in modalità utente.
- **TXM_MODULE_INVALID_MEMORY** (0xF4): indica che la memoria fornita dal modulo non è valida o si trova in una posizione non valida. Ad esempio, nei moduli protetti da memoria, i blocchi di controllo degli oggetti non possono trovarsi in memoria a cui il modulo può accedere.
- **TXM_MODULE_INVALID_CALLBACK** (0xF5): il callback specificato nell'API non è compreso nell'intervallo del codice del modulo e pertanto non è valido.

---

## <a name="txm_module_application_request"></a>txm_module_application_request

Richiesta specifica dell'applicazione al codice residente.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_application_request(
    ULONG request, 
    ULONG param_1,
    ULONG param_2,
    ULONG param_3);
```

### <a name="description"></a>Descrizione

Questo servizio effettua la richiesta specificata alla parte residente dell'applicazione. Si presuppone che la struttura della richiesta sia preparata prima della chiamata. L'elaborazione effettiva della richiesta avviene nel codice residente nella funzione ***_txm_module_manager_application_request***. Per impostazione predefinita, questa funzione viene lasciata vuota ed è progettata per la modifica da parte dello sviluppatore di applicazioni residenti.

### <a name="input-parameters"></a>Parametri di input

- **richiesta** ID richiesta (definito dall'applicazione)
- **param_1** Primo parametro
- **param_2** Secondo parametro
- **param_3** Terzo parametro

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Richiesta riuscita.
- **TX_NOT_AVAILABLE** (0x1D) Richiesta non supportata dal codice residente.

### <a name="allowed-from"></a>Consentito da

Thread del modulo

### <a name="example"></a>Esempio

```c
/* Call application resident code with ID=77 and the
   parameters set to 1, 2, 3. */
status = txm_module_application_request(77, 1, 2, 3);

/* If status is TX_SUCCESS the request was successful. */
```

---

## <a name="txm_module_object_allocate"></a>txm_module_object_allocate

Allocare memoria nel pool di oggetti (creato dall'applicazione residente) per un blocco di controllo dell'oggetto modulo.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_object_allocate(
   VOID **object_ptr, 
   ULONG object_size);
```

### <a name="description"></a>Descrizione

Questo servizio alloca memoria per un oggetto modulo dalla memoria esterna al modulo, che consente di evitare il danneggiamento del blocco di controllo dell'oggetto da parte del codice del modulo. Nei sistemi protetti da memoria, tutti i blocchi di controllo degli oggetti devono essere allocati con questa API prima di poter essere creati.

### <a name="input-parameters"></a>Parametri di input

- **object_ptr** Destinazione del puntatore a oggetto al completamento dell'allocazione.
- **object_size** Dimensione in byte dell'oggetto da allocare.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Allocato oggetto riuscito.
- **TX_NO_MEMORY** (0x10) Memoria insufficiente.
- **TX_NOT_AVAILABLE** (0x1D) Gestione moduli non ha creato un pool di oggetti da cui eseguire l'allocazione

### <a name="allowed-from"></a>Consentito da

Thread del modulo

### <a name="example"></a>Esempio

```c
TX_QUEUE *queue_pointer;

/* Allocate a control block for a module message queue. */
status = txm_module_object_allocate(&queue_pointer, sizeof(TX_QUEUE));

/* If status is TX_SUCCESS the queue_pointer points to
   memory allocated outside of the module and can be supplied
   to tx_queue_create to create a queue for the module. */
```

### <a name="see-also"></a>Vedere anche

- txm_module_object_deallocate
- txm_module_object_pointer_get

---

## <a name="txm_module_object_deallocate"></a>txm_module_object_deallocate

Deallocare la memoria degli oggetti allocata in precedenza

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_object_deallocate(VOID *object_ptr);
```

### <a name="description"></a>Descrizione

***Questo servizio è stato deprecato perché non è più necessario.***

La memoria allocata in precedenza ***tramite txm_module_object_allocate**_ viene deallocata nel* servizio _ _tx_ \_ _delete .***

### <a name="input-parameters"></a>Parametri di input

- **object_ptr** Puntatore a oggetto da deallocare.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Allocato oggetto riuscito.

### <a name="allowed-from"></a>Consentito da

Thread del modulo

### <a name="example"></a>Esempio

```c
TX_QUEUE *queue_pointer;

/* Deallocate control block for a module message queue. */
status = txm_module_object_deallocate(queue_pointer);

/* If status is TX_SUCCESS the object memory associated
   with queue_pointer is deallocated. */
```

### <a name="see-also"></a>Vedere anche

- txm_module_object_allocate
- txm_module_object_pointer_get

---

## <a name="txm_module_object_pointer_get"></a>txm_module_object_pointer_get

Trovare l'oggetto di sistema e recuperare il puntatore all'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_object_pointer_get(
   UINT object_type, CHAR *name, 
   VOID **object_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il puntatore all'oggetto di un tipo specifico con un nome specifico. Se l'oggetto non viene trovato, viene restituito un errore. In caso contrario, se l'oggetto viene trovato, l'indirizzo dell'oggetto viene inserito in "object_ptr". Questo puntatore può quindi essere usato per effettuare chiamate al servizio di sistema, interagire con il codice residente e/o altri moduli caricati nel sistema.

### <a name="input-parameters"></a>Parametri di input

- **object_type** Tipo di oggetto ThreadX richiesto. I tipi validi sono i seguenti:
  - TXM_BLOCK_POOL_OBJECT
  - TXM_BYTE_POOL_OBJECT
  - TXM_EVENT_FLAGS_OBJECT
  - TXM_MUTEX_OBJECT
  - TXM_QUEUE_OBJECT
  - TXM_SEMAPHORE_OBJECT
  - TXM_THREAD_OBJECT
  - TXM_TIMER_OBJECT
  - TXM_IP_OBJECT
  - TXM_PACKET_POOL_OBJECT
  - TXM_UDP_SOCKET_OBJECT
  - TXM_TCP_SOCKET_OBJECT
- **name** Nome dell'oggetto specifico dell'applicazione come definito al momento della creazione dell'oggetto.
- **object_ptr** Destinazione per il puntatore a oggetto.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Operazione riuscita dell'oggetto.
- **TX_OPTION_ERROR** (0x08) Tipo di oggetto non valido.
- **TX_PTR_ERROR** (0x03) Destinazione non valida.
- **TX_SIZE_ERROR** (0x05) Dimensioni non valide.
- **TX_NO_INSTANCE** oggetto (0x0D) non trovato.

### <a name="allowed-from"></a>Consentito da

Thread del modulo

### <a name="example"></a>Esempio

```c
TX_QUEUE *queue_pointer;

/* Find the pointer for "fft_queue" in the resident part
   of the application. */
status = txm_module_object_pointer_get(TXM_QUEUE_OBJECT,
         "fft_queue", &queue_pointer);

/* If status is TX_SUCCESS the found queue pointer is in
   "queue_pointer". This queue pointer can then be used to
   send messages to the "fft_queue." */
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_object_pointer_get_extended

---

## <a name="txm_module_object_pointer_get_extended"></a>txm_module_object_pointer_get_extended

Trovare l'oggetto di sistema e recuperare il puntatore dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_object_pointer_get_extended(UINT object_type,
                                            CHAR *name,
                                            UINT name_length,
                                            VOID **object_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il puntatore a un oggetto di un particolare tipo con un nome specifico. Se l'oggetto non viene trovato, viene restituito un errore. In caso contrario, se l'oggetto viene trovato, l'indirizzo dell'oggetto viene inserito in "object_ptr". Questo puntatore può quindi essere usato per effettuare chiamate al servizio di sistema, per interagire con il codice residente e/o altri moduli caricati nel sistema.

### <a name="input-parameters"></a>Parametri di input

- **object_type** Tipo di oggetto ThreadX richiesto. I tipi validi sono i seguenti:
  - TXM_BLOCK_POOL_OBJECT
  - TXM_BYTE_POOL_OBJECT
  - TXM_EVENT_FLAGS_OBJECT
  - TXM_MUTEX_OBJECT
  - TXM_QUEUE_OBJECT
  - TXM_SEMAPHORE_OBJECT
  - TXM_THREAD_OBJECT
  - TXM_TIMER_OBJECT
  - TXM_IP_OBJECT
  - TXM_PACKET_POOL_OBJECT
  - TXM_UDP_SOCKET_OBJECT
  - TXM_TCP_SOCKET_OBJECT
- **name** Nome dell'oggetto specifico dell'applicazione come definito al momento della creazione dell'oggetto.
- **name_length** Lunghezza del nome.
- **object_ptr** Destinazione per il puntatore all'oggetto.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) Successful object get.
- **TX_OPTION_ERROR** (0x08) Tipo di oggetto non valido.
- **TX_PTR_ERROR** (0x03) Destinazione non valida.
- **TX_SIZE_ERROR** (0x05) Dimensioni non valide.
- **TX_NO_INSTANCE** oggetto (0x0D) non trovato.

### <a name="allowed-from"></a>Consentito da

Thread del modulo

### <a name="example"></a>Esempio

```c
TX_QUEUE *queue_pointer;

/* Find the pointer for "fft_queue" in the resident part
   of the application. */
   status = txm_module_object_pointer_get_extended(TXM_QUEUE_OBJECT,
            "fft_queue", 9, &queue_pointer);

/* If status is TX_SUCCESS the found queue pointer is in
   "queue_pointer". This queue pointer can then be used to
   send messages to the "fft_queue." */
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_object_pointer_get
