---
title: Capitolo 5-API di gestione moduli
author: philmea
description: Questo articolo è un riepilogo delle API di gestione dei moduli disponibili per la parte residente dell'applicazione.
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ca0fee443c23fd1bdd34651f4a7b31cf71f886f0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821389"
---
# <a name="chapter-5---module-manager-apis"></a>Capitolo 5-API di gestione moduli

## <a name="summary-of-module-manager-apis"></a>Riepilogo delle API di gestione dei moduli

Sono disponibili diverse API aggiuntive per la parte residente dell'applicazione, come indicato di seguito.

- ***txm_module_manager_external_memory_enable** _-_Enable accedere al modulo a uno spazio di memoria condiviso *
- ***txm_module_manager_file_load** il modulo _-_Load dal file tramite FILEX *
- ***txm_module_manager_in_place_load** _-_Load dati del modulo, eseguire sul posto *
- ***txm_module_manager_initialize** _-_Initialize gestione moduli *
- ***txm_module_manager_mm_initialize** _-_Initialize l'hardware di gestione della memoria *
- ***txm_module_manager_maximum_module_priority_set** _-_Set priorità massima consentita per il thread in un modulo *
- ***txm_module_manager_memory_fault_notify** _-_Register un callback dell'applicazione in un errore di memoria *
- ***txm_module_manager_memory_load** _-_Load il modulo dalla memoria *
- ***txm_module_manager_object_pool_create** _-_Create un pool di oggetti per i moduli *
- ***txm_module_manager_properties_get** _-_Get proprietà del modulo *
- ***txm_module_manager_start** _-_Start l'esecuzione del modulo specificato *
- ***txm_module_manager_stop** _-_Stop l'esecuzione del modulo specificato *
- ***txm_module_manager_unload** _-_Unload il modulo *

---

## <a name="txm_module_manager_external_memory_enable"></a>txm_module_manager_external_memory_enable

Abilitare il modulo per accedere a uno spazio di memoria condiviso.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_external_memory_enable(
     TXM_MODULE_INSTANCE *module_instance,
     VOID *start_address,
     ULONG length,
     UINT attributes);
```

### <a name="description"></a>Descrizione

Questo servizio crea una voce nella tabella hardware di gestione della memoria per un'area di memoria condivisa a cui il modulo può accedere.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore all'istanza del modulo.
- **start_address** Indirizzo iniziale dell'area di memoria condivisa.
- **lunghezza** Lunghezza dell'area di memoria condivisa.
- **attributi** di Attributi dell'area di memoria (cache, lettura, scrittura e così via). Gli attributi sono specifici della porta; vedere [appendice](appendix.md) per formato attributi.

### <a name="return-values"></a>Valori restituiti

- Creazione della voce di memoria **TX_SUCCESS** (0x00) completata.
- Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata o funzionalità non disponibile.
- L'istanza del modulo **TX_PTR_ERROR** (0X03) non è valida.
- Il modulo **TX_START_ERROR** (0x10) non è in stato caricato.
- **TXM_MODULE_ALIGNMENT_ERROR** (0xF0) non valido per l'allineamento degli indirizzi iniziali.
- Proprietà incompatibili **TXM_MODULE_INVALID_PROPERTIES** (0xf3).

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Create a shared memory space 256 bytes long at address 0x64005000
   with read & write, no execute, outer & inner write back cache
   attributes. Note that these attributes are port-specific. */
txm_module_manager_external_memory_enable(&my_module, (VOID*)0x64005000, 256, 0x3F);
```

---

## <a name="txm_module_manager_file_load"></a>txm_module_manager_file_load

Caricare il modulo dal file tramite FileX.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_file_load(
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```

### <a name="description"></a>Descrizione

Questo servizio carica l'immagine binaria del modulo contenuto nel file specificato nell'area di memoria del modulo e la prepara per l'esecuzione. Si presuppone che il supporto fornito sia già aperto.

> [!NOTE]
> Il sistema FileX viene usato per caricare il file. Per abilitare l'accesso FileX, è necessario compilare il modulo, la libreria di moduli, il gestore dei moduli e la libreria ThreadX (con le origini di Module Manager) con **FX_FILEX_PRESENT** definito nei progetti.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore all'istanza del modulo.
- **module_name** Nome del modulo.
- **media_ptr** Puntatore ai supporti FileX già aperti.
- **file_name** Nome del file binario del modulo.

### <a name="return-values"></a>Valori restituiti

- Il caricamento del modulo **TX_SUCCESS** (0x00) è riuscito.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.
- Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.
- **TX_NO_MEMORY** (0x10) memoria insufficiente per caricare il modulo.
- Il supporto **TX_NOT_DONE** (0x20) non è aperto, il file non è stato trovato o il file non è valido.
- Puntatore al modulo **TX_PTR_ERROR** (0X03) non valido.
- Allineamento di **TXM_MODULE_ALIGNMENT_ERROR** (0xF0) non valido.
- Il modulo **TXM_MODULE_ALREADY_LOADED** (0xF1) è già caricato.
- **TXM_MODULE_INVALID** (0xF2) | Preambolo del modulo non valido.
- Proprietà incompatibili **TXM_MODULE_INVALID_PROPERTIES** (0xf3).

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager. */
status = txm_module_manager_initialize((VOID*)0x64010000,0x10000);

/* Load the module from a binary file. */
status = txm_module_manager_file_load(&my_module, "my module",
                                      &sdio_disk, "demo_thread_module.bin");

/* Start the module. */
status = txm_module_manager_start(&my_module);
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_in_place_load
- txm_module_manager_memory_load
- txm_module_manager_unload

---

## <a name="txm_module_manager_in_place_load"></a>txm_module_manager_in_place_load

Caricare solo i dati del modulo, eseguire il modulo in un percorso esistente.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_in_place_load(
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    VOID *location);
```

### <a name="description"></a>Descrizione

Questo servizio carica l'area dati del modulo solo nell'area di memoria del modulo e la prepara per l'esecuzione. L'esecuzione del codice del modulo sarà sul posto, ovvero dall'offset degli indirizzi specificato dal preambolo del modulo nella posizione specificata.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore all'istanza del modulo.
- **module_name** Nome del modulo.
- **posizione** Puntatore all'area di codice del modulo, preambolo.

### <a name="return-values"></a>Valori restituiti

- Il caricamento del modulo **TX_SUCCESS** (0x00) è riuscito.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.
- Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.
- **TX_NO_MEMORY** (0x10) memoria insufficiente per caricare il modulo.
- **TX_PTR_ERROR** (0x03) puntatore non valido, istanza del modulo o preambolo del modulo.
- Allineamento di **TXM_MODULE_ALIGNMENT_ERROR** (0xF0) non valido.
- Il modulo **TXM_MODULE_ALREADY_LOADED** (0xF1) è già caricato.
- Preambolo del modulo **TXM_MODULE_INVALID** (0XF2) non valido.
- Proprietà incompatibili **TXM_MODULE_INVALID_PROPERTIES** (0xf3).

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Start the module. */
txm_module_manager_start(&my_module);
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_file_load
- txm_module_manager_memory_load
- txm_module_manager_unload

---

## <a name="txm_module_manager_initialize"></a>txm_module_manager_initialize

Inizializzare Gestione moduli.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_initialize(
    VOID *module_memory_start,
    ULONG module_memory_size);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza le risorse interne di gestione moduli, inclusa l'area di memoria usata per il caricamento dei moduli.

### <a name="input-parameters"></a>Parametri di input

- **module_memory_start** Puntatore all'inizio della memoria del modulo.
- **module_memory_size** Dimensioni in byte della memoria del modulo.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) inizializzazione riuscita.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Initialize the module manager with 64KB of RAM starting at
   address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_object_pool_create

---

## <a name="txm_module_manager_initialize_mmu"></a>txm_module_manager_initialize_mmu

Inizializzare l'hardware di gestione della memoria.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_initialize_mmu(VOID);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza la MMU.

### <a name="input-parameters"></a>Parametri di input

Nessuno

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) inizializzazione riuscita.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Initialize the MMU. */
txm_module_manager_initialize_mmu();
```

---

## <a name="txm_module_manager_maximum_module_priority_set"></a>txm_module_manager_maximum_module_priority_set

Imposta la priorità massima dei thread consentita in un modulo.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_maximum_module_priority_set(
         TXM_MODULE_INSTANCE *module_instance,
         UINT priority);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la priorità massima dei thread consentita in un modulo.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore all'istanza del modulo.
- **priorità** di Priorità massima thread.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) inizializzazione riuscita.
- Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.
- L'istanza del modulo **TX_PTR_ERROR** (0X03) non è valida.
- Il modulo **TX_START_ERROR** (0x10) non è in stato caricato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Set the maximum thread priority in my_module to 5. */
txm_module_manager_maximum_module_priority_set(&my_module, 5);
```

---

## <a name="txm_module_manager_memory_fault_notify"></a>txm_module_manager_memory_fault_notify

Registrare un callback dell'applicazione in un errore di memoria.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_memory_fault_notify(
     VOID (*notify_function)(TX_THREAD *, MODULE_INSTANCE *));
```

### <a name="description"></a>Descrizione

Questo servizio registra la funzione di callback di notifica di errore di memoria dell'applicazione specificata con gestione moduli. Se si verifica un errore di memoria, questa funzione viene chiamata con un puntatore al thread danneggiato e l'istanza del modulo corrispondente al thread danneggiato. L'elaborazione del gestore dei moduli termina automaticamente il thread danneggiato, ma lascia invariati tutti gli altri thread del modulo. Spetta all'applicazione decidere cosa fare con il modulo associato all'errore di memoria.

Vedere lo struct **_txm_module_manager_memory_fault_info** interno per informazioni specifiche sullo stesso errore di memoria.

> [!NOTE]
> La funzione di callback di notifica di errore di memoria viene eseguita direttamente dall'eccezione di errore della memoria, quindi è possibile chiamare solo le API ThreadX consentite dalle routine del servizio di interrupt. Pertanto, per arrestare e scaricare il modulo che causa il danneggiamento, il callback di notifica dell'applicazione deve inviare un segnale a un'attività dell'applicazione in modo che il modulo possa essere arrestato e scaricato.

### <a name="input-parameters"></a>Parametri di input

- **notify_function** Puntatore a funzione al callback di notifica di errore di memoria dell'applicazione. Se si specifica un valore NULL, la notifica di errore di memoria viene disabilitata.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) registrazione della funzione di notifica riuscita.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Register a memory fault callback. */
txm_module_manager_memory_fault_notify(my_memory_fault_handler);
```

---

## <a name="txm_module_manager_memory_load"></a>txm_module_manager_memory_load

Caricare il modulo dalla memoria.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_memory_load (
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    VOID *location);
```

### <a name="description"></a>Descrizione

Questo servizio carica il codice e l'area dati del modulo nell'area di memoria del modulo configurata da ***txm_module_manager_initialize*** e la prepara per l'esecuzione.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore all'istanza del modulo.
- **module_name** Nome del modulo.
- **posizione** Puntatore all'area di codice del modulo, preambolo.

### <a name="return-values"></a>Valori restituiti

- Il caricamento del modulo **TX_SUCCESS** (0x00) è riuscito.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.
- Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.
- **TX_NO_MEMORY** (0x10) memoria insufficiente per caricare il modulo.
- **TX_PTR_ERROR** (0x03) puntatore non valido, istanza del modulo o preambolo del modulo.
- Allineamento di **TXM_MODULE_ALIGNMENT_ERROR** (0xF0) non valido.
- Il modulo **TXM_MODULE_ALREADY_LOADED** (0xF1) è già caricato.
- Preambolo del modulo **TXM_MODULE_INVALID** (0XF2) non valido.
- Proprietà incompatibili **TXM_MODULE_INVALID_PROPERTIES** (0xf3).

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
TXM_MODULE_INSTANCE     my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
 txm_module_manager_memory_load(&my_module, "my module", (VOID *) 0x080F0000);
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_file_load
- txm_module_manager_in_place_load
- txm_module_manager_unload

---

## <a name="txm_module_manager_object_pool_create"></a>txm_module_manager_object_pool_create

Creare un pool di oggetti per i moduli.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_object_pool_create(
    VOID *pool_memory_start,
    ULONG pool_memory_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un pool di memoria oggetto di gestione moduli da cui i moduli possono allocare oggetti ThreadX/NetX, mantenendo l'oggetto di sistema fuori dall'area di memoria del modulo.

### <a name="input-parameters"></a>Parametri di input

- **pool_memory_start** Puntatore all'inizio della memoria dell'oggetto.
- **pool_memory_size** Dimensioni in byte del pool di memoria dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) inizializzazione riuscita.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Create an object memory pool in the next 64KB of memory. */
txm_module_manager_object_pool_create((VOID *) 0x64020000, 0x10000);
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_initialize

---

## <a name="txm_module_manager_properties_get"></a>txm_module_manager_properties_get

Ottenere le proprietà del modulo.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_properties_get(
    TXM_MODULE_INSTANCE *module_instance,
    ULONG *module_properties_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce le proprietà (specificate nel preambolo) di un modulo.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore all'istanza del modulo.
- **module_properties_ptr** Puntatore alla destinazione per le proprietà del modulo.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** (0x00) inizializzazione riuscita.
- **TX_PTR_ERROR** (0x03) puntatore non valido.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
TXM_MODULE_INSTANCE     my_module;
ULONG                   module_properties;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Create an object memory pool in the next 64KB of memory. */
txm_module_manager_object_pool_create((VOID *) 0x64020000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Get module properties. */
txm_module_manager_properties_get(&my_module, &module_properties);
```

---

## <a name="txm_module_manager_start"></a>txm_module_manager_start

Avviare l'esecuzione del modulo.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_start(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'esecuzione del modulo già caricato specificato.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore a un'istanza del modulo caricata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Inizio del modulo **TX_SUCCESS** (0x00) riuscito.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.
- Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.
- Il puntatore o l'istanza del modulo **TX_PTR_ERROR** (0X03) non è valido.
- Il modulo **TX_START_ERROR** (0x10) è già stato avviato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Start the module. */
txm_module_manager_start(&my_module);

/* Let the module run for a while. */
tx_thread_sleep(2000);

/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_stop

---

## <a name="txm_module_manager_stop"></a>txm_module_manager_stop

Arrestare l'esecuzione del modulo.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_stop(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a>Descrizione

Questo servizio arresta un modulo caricato in precedenza e avviato. L'arresto di un modulo include l'esecuzione del thread di arresto facoltativo del modulo, la terminazione di tutti i thread e l'eliminazione di tutte le risorse associate al modulo.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore all'istanza del modulo.

### <a name="return-values"></a>Valori restituiti

- Interruzione del modulo riuscita **TX_SUCCESS** (0x00).
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.
- Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.
- Il puntatore o l'istanza del modulo **TX_PTR_ERROR** (0X03) non è valido.
- Il modulo **TX_START_ERROR** (0x10) non è stato avviato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start the module. */
txm_module_manager_start(&my_module);

/* Let the module run for a while. */
tx_thread_sleep(20000);

/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_start

---

## <a name="txm_module_manager_unload"></a>txm_module_manager_unload

Scaricare il modulo.

### <a name="prototype"></a>Prototipo

```c
UINT txm_module_manager_unload(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a>Descrizione

Questo servizio Scarica il modulo caricato e arrestato in precedenza, liberando tutte le risorse di memoria del modulo associate.

### <a name="input-parameters"></a>Parametri di input

- **module_instance** Puntatore all'istanza del modulo.

### <a name="return-values"></a>Valori restituiti

- **TX_SUCCESS** 0x00) lo scaricamento del modulo è riuscito.
- Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.
- Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.
- Il modulo o il modulo **TX_NOT_DONE** (0x20) non è stato arrestato.
- Il puntatore o l'istanza del modulo **TX_PTR_ERROR** (0X03) non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
status = txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a>Vedere anche

- txm_module_manager_file_load
- txm_module_manager_in_place_load
- txm_module_manager_memory_load
- txm_module_manager_stop
