---
title: Capitolo 4-Descrizione dei servizi CLIENT di LWM2M
description: Questo capitolo contiene una descrizione di tutti i servizi client di LWM2M in ordine alfabetico.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 825a215ba756b39b6d76e6cc773c288e8b8aab01
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821833"
---
# <a name="chapter-4--description-of-lwm2m-client-services"></a>Capitolo 4 Descrizione dei servizi CLIENT di LWM2M

Questo capitolo contiene una descrizione di tutti i servizi client di LWM2M elencati di seguito in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal  **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

**Gestione client LWM2M:**

- nx_lwm2m_client_create: *creare un client lwm2m*

- nx_lwm2m_client_delete: *eliminare il client lwm2m*

- nx_lwm2m_client_lock: *bloccare il client lwm2m*

- nx_lwm2m_client_unlock: *sbloccare il client lwm2m*

**Gestione delle sessioni client di LWM2M:**

- nx_lwm2m_client_session_create: *creare una sessione client lwm2m*

- nx_lwm2m_client_session_delete: *eliminare la sessione del client lwm2m*

- nx_lwm2m_client_session_bootstrap: *avviare una sessione con un server bootstrap*

- nx_lwm2m_client_session_bootstrap_dtls: *avviare una sessione protetta con un server bootstrap*

- nx_lwm2m_client_session_register_info_get: *ottenere informazioni sul registro del server lwm2m*

- nx_lwm2m_client_session_register: *avviare una sessione con un server lwm2m*

- nx_lwm2m_client_session_register_dtls: *avviare una sessione protetta con un server lwm2m*

- nx_lwm2m_client_session_update: *aggiornare una sessione con un server lwm2m*

- nx_lwm2m_client_session_deregister: *terminare una sessione con un server lwm2m*

- nx_lwm2m_client_session_error_get: *ottenere l'ultimo errore di una sessione*

**Implementazione dell'oggetto dispositivo:**

- nx_lwm2m_client_device_callbacks_set: *impostare i callback dell'applicazione oggetto dispositivo*

- nx_lwm2m_client_device_error_push: *aggiungere il codice di errore all'oggetto dispositivo*

- nx_lwm2m_client_device_error_reset: *Reimposta i codici di errore dell'oggetto dispositivo*

- nx_lwm2m_client_device_resource_changed: *modifica del segnale della risorsa oggetto dispositivo*

**Implementazione dell'oggetto di aggiornamento del firmware:**

- nx_lwm2m_firmware_create: *creare un oggetto di aggiornamento del firmware*

- nx_lwm2m_firmware_package_info_set: *impostare le informazioni sul pacchetto di aggiornamento del firmware*

- nx_lwm2m_firmware_result_set: *impostare il risultato dell'aggiornamento del firmware*

- nx_lwm2m_firmware_state_set: *impostare lo stato di aggiornamento del firmware*

**Implementazione di oggetti personalizzati:**

- nx_lwm2m_client_object_add: *aggiungere l'implementazione dell'oggetto al client lwm2m*

- nx_lwm2m_client_object_remove: *rimuovere l'implementazione dell'oggetto dal client lwm2m*

- nx_lwm2m_client_object_instance_add: *aggiungere un'istanza dell'oggetto al client lwm2m*

- nx_lwm2m_client_object_instance_remove: *rimuovere l'istanza dell'oggetto dal client lwm2m*

- nx_lwm2m_object_resource_changed: *modifica del segnale di un valore di risorsa di un'istanza dell'oggetto*

**Gestione dei dispositivi locali**

- nx_lwm2m_client_object_create: *creare una nuova istanza dell'oggetto*

- nx_lwm2m_client_object_delete: *eliminare un'istanza dell'oggetto*

- nx_lwm2m_client_object_discover: *individuazione delle risorse di un'istanza dell'oggetto*

- nx_lwm2m_client_object_execute: *eseguire la risorsa di un'istanza dell'oggetto*

- nx_lwm2m_client_object_next_get: *Ottiene l'elenco di oggetti implementati dal client lwm2m*

- nx_lwm2m_client_object_instance_next_get: *Ottiene l'elenco di istanze di un oggetto*

- nx_lwm2m_client_object_read: *leggere i valori delle risorse di un'istanza dell'oggetto*

- nx_lwm2m_client_object_write: *modificare i valori delle risorse di un'istanza dell'oggetto*

**Impostazione informazioni risorse e valori:**

- nx_lwm2m_client_resource_info_set: *impostare le informazioni sulla risorsa*

- nx_lwm2m_client_resource_string_set: *impostare il valore della risorsa come stringa*

- nx_lwm2m_client_resource_integer32_set: *impostare il valore della risorsa come intero a 32 bit*

- nx_lwm2m_client_resource_integer64_set: *impostare il valore della risorsa come intero a 64 bit*

- nx_lwm2m_client_resource_float32_set: *impostare il valore della risorsa come float a 32 bit*

- nx_lwm2m_client_resource_float64_set: *impostare il valore della risorsa come float a 64 bit*

- nx_lwm2m_client_resource_boolean_set: *impostare il valore della risorsa come valore booleano*

- nx_lwm2m_client_resource_objlnk_set: *impostare il valore della risorsa come collegamento all'oggetto*

- nx_lwm2m_client_resource_opaque_set: *impostare il valore della risorsa come opaco*

- nx_lwm2m_client_resource_instance_set: *impostare il valore della risorsa come istanza di per più risorse*
-
- nx_lwm2m_client_resource_dim_set: *impostare la dimensione della risorsa per più risorse.*

**Informazioni sulle risorse e valori per ottenere:**

- nx_lwm2m_client_resource_info_get: *ottenere le informazioni sulle risorse*

- nx_lwm2m_client_resource_string_get: *recuperare il valore di una risorsa di stringa*

- nx_lwm2m_client_resource_integer32_get: *recuperare il valore di una risorsa Integer a 32 bit*

- nx_lwm2m_client_resource_integer64_get: *recuperare il valore di una risorsa Integer a 64 bit*

- nx_lwm2m_client_resource_float32_get: *recuperare il valore di una risorsa float a 32 bit*

- nx_lwm2m_client_resource_float64_get: *recuperare il valore di una risorsa float a 64 bit*

- nx_lwm2m_client_resource_boolean_get: *recuperare il valore di una risorsa booleana*

- nx_lwm2m_client_resource_objlnk_get: *recuperare il valore di una risorsa di collegamento a un oggetto*

- nx_lwm2m_client_resource_opaque_get: *recuperare il valore di una risorsa opaca*

- nx_lwm2m_client_resource_instance_get: *ottenere l'istanza della risorsa per più risorse*

- nx_lwm2m_client_resource_dim_get: *ottenere la dimensione della risorsa per più risorse.*

## <a name="nx_lwm2m_client_create"></a>nx_lwm2m_client_create

Crea un client LWM2M.

### <a name="prototype"></a>Prototipo

```C
UINT nx_lwm2m_client_create(
    NX_LWM2M_CLIENT client_ptr,
    NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    const CHAR *name_ptr,
    UINT name_length,
    const CHAR *msisdn_ptr,
    UINT msisdn_length,
    UCHAR binding_modes,
    VOID *stack_ptr,
    ULONG stack_size,
    UINT priority);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client LWM2M, che viene eseguita nel contesto del proprio thread ThreadX.

Il client LWM2M implementa i seguenti oggetti LWM2M OMA: Security (0), server (1), controllo di accesso (2) e Device (3). Le altre implementazioni di oggetti devono essere aggiunte dall'applicazione.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **packet_pool_ptr** Puntatore al pool di pacchetti predefinito per il client LWM2M.
- **name_ptr** Puntatore al nome dell'endpoint del client LWM2M.
- **name_length** Lunghezza del nome dell'endpoint del client LWM2M.
- **msisdn_ptr** Puntatore a MSISDN in cui è possibile raggiungere il client LWM2M per l'utilizzo con l'associazione SMS. può essere NULL se l'associazione SMS non è supportata.
- **msisdn_length** Lunghezza del numero MSISDN.
- **binding_modes** Il binding e le modalità supportate dal client LWM2M devono essere costituiti da una combinazione di flag di NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S e NX_LWM2M_BINDING_SQ.
- **stack_ptr** Puntatore all'area dello stack di thread del client LWM2M.
- **stack_size** Dimensioni dello stack dei thread del client LWM2M.
- **priorità** di Priorità del client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Il client LWM2M è stato creato correttamente.
- **NX_LWM2M_CLIENT_ERROR** Errore di creazione del client LWM2M.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.
- **NX_PTR_ERROR** Puntatore non valido.
- **NX_SIZE_ERROR** Dimensioni dello stack non valide.
- **NX_OPTION_ERROR** Priorità non valida.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```C
/* Create LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client, &ip_0, &pool_0, 
  "netxlwm2mclient", sizeof("netxlwm2mclient") - 1,           
                                NX_NULL, 0, NX_LWM2M_CLIENT_BINDING_U, 
                                stack_ptr, stack_size, priority);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully created.  */
```

## <a name="nx_lwm2m_client_delete"></a>nx_lwm2m_client_delete

Elimina un client LWM2M.

### <a name="prototype"></a>Prototipo

```C
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del client LWM2M creata in precedenza.

Tutte le sessioni attualmente associate al client vengono eliminate anche da questa chiamata.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Il client LWM2M è stato eliminato correttamente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Delete the LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_device_callback_set"></a>nx_lwm2m_client_device_callback_set

Imposta il callback dell'applicazione di un oggetto dispositivo.

### <a name="prototype"></a>Prototipo

```C
UINT **nx_lwm2m_client_device_callback_set**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_OPERATION_CALLBACK operation_callback);
```

### <a name="description"></a>Descrizione

Questo servizio installa il callback dell'applicazione per l'implementazione di operazioni sulle risorse dell'oggetto dispositivo LWM2M che non sono gestite dal client LWM2M.

Il client LWM2M implementa le risorse seguenti: codice errore (11), Reimposta codice errore (12), binding supportato e modalità (16), le operazioni per le altre risorse vengono reindirizzate all'applicazione.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **operation_callback** Callback dell'operazione per "Read", "Discover", "Write" ed "Execute".

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Il callback dell'operazione è stato impostato correttamente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set device callback.  */
status = nx_lwm2m_client_device_callback_set(&lwm2m_client, device_operation);

/* If status is NX_SUCCESS a device callback was successfully set.  */
```

## <a name="nx_lwm2m_client_device_error_push"></a>nx_lwm2m_client_device_error_push
Aggiunge un codice di errore a un oggetto dispositivo.

### <a name="prototype"></a>Prototipo

```C
UINT **nx_lwm2m_client_device_error_push**(
    NX_LWM2M_CLIENT *client_ptr,
    UCHAR code);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una nuova istanza alla risorsa del codice di errore (11) del dispositivo dell'oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **codice** Nuovo codice di errore.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL**

Il numero massimo di codici di errore archiviati è

è stato raggiunto.

NX_PTR_ERROR puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```C
/* Push device error 1 (Low battery power) to server.  */
status = nx_lwm2m_client_device_error_push(&lwm2m_client, 1);

/* If status is NX_SUCCESS a device error was successfully pushed.  */
```

## <a name="nx_lwm2m_client_device_error_reset"></a>nx_lwm2m_client_device_error_reset

Reimposta i codici di errore dell'oggetto dispositivo.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina tutte le istanze di risorse del codice di errore dall'oggetto dispositivo. Equivale a eseguire il codice di errore di reimpostazione della risorsa (12).

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Delete all device error code.  */
status = nx_lwm2m_client_device_error_reset(&lwm2m_client);

/* If status is NX_SUCCESS, reset device error successfully.  */
```

## <a name="nx_lwm2m_client_device_resource_changed"></a>nx_lwm2m_client_device_resource_changed

Segnala una modifica a una risorsa oggetto dispositivo.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_resource_changed(
    NX_LWM2M_CLIENT *client_ptr, 
    const NX_LWM2M_RESOURCE *resource);

```

### <a name="description"></a>Descrizione

Il servizio viene usato dall'applicazione per segnalare al client LWM2M che una risorsa del dispositivo oggetto è cambiata. Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **risorsa** di Puntatore alla struttura che descrive la risorsa che è stata modificata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Change device resource.  */
status = nx_lwm2m_client_device_resource_changed(&lwm2m_client, &resource);

/* If status is NX_SUCCESS, a device resource was successfully changed.  */
```

##  <a name="nx_lwm2m_client_firmware_create"></a>nx_lwm2m_client_firmware_create

Creare un oggetto firmware del client LWM2M. 

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_firmware_create(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    NX_LWM2M_CLIENT *client_ptr, 
    UINT protocols,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_URI_CALLBACK update_callback);
```

### <a name="description"></a>Descrizione

Il servizio viene usato dall'applicazione per creare un oggetto firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr** Puntatore all'oggetto firmware del client LWM2M.
- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **protocolli** di Protocolli supportati.
- **package_callback** Callback del pacchetto.
- **package_uri_callback** Callback dell'URI del pacchetto.
- **update_callback** Callback dell'aggiornamento.

### <a name="return-values"></a>Valori restituiti

**NX_SUCCESS** Operazione completata.
**NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Create firmware object.  */
status = nx_lwm2m_client_firmware_create(&firmware, &lwm2m_client,     
                                         NX_LWM2M_CLIENT_FIRMWARE_PROTOCOL_HTTP, 
                                         NX_NULL, firmware_packet_uri,
                                         firmware_update);

/* If status is NX_SUCCESS, firmware object was successfully created.  */
```

##  <a name="nx_lwm2m_client_firmware_package_info_set"></a>nx_lwm2m_client_firmware_package_info_set

Imposta le informazioni del pacchetto del firmware del client LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_firmware_package_info_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    const CHAR *name, 
    UINT name_length, 
    const CHAR *version, 
    UINT version_length);
```

### <a name="description"></a>Descrizione

Il servizio viene utilizzato dall'applicazione per impostare le risorse di informazioni sul pacchetto dell'oggetto di aggiornamento del firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr** Puntatore all'oggetto firmware del client LWM2M.
- **nome** Nome del pacchetto del firmware.
- **name_length** Lunghezza del nome.
- **versione** di Versione del pacchetto del firmware.
- **version_length** Lunghezza della versione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the package information resources of the firmware object.  */
status = nx_lwm2m_client_firmware_package_info_set(&firmware, 2m_client,     
                                    “LWM2M Firmware”, sizeof(“LWM2M Firmware”) -1,
                                    “1.0.0.0”, sizeof(“1.0.0.0”) - 1);

/* If status is NX_SUCCESS, package information resources was successfully set. */
```

##  <a name="nx_lwm2m_client_firmware_result_set"></a>nx_lwm2m_client_firmware_result_set

Imposta la risorsa risultato aggiornamento dell'oggetto aggiornamento firmware.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_firmware_result_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a>Descrizione

Il servizio viene usato dall'applicazione per impostare la risorsa del risultato dell'aggiornamento dell'oggetto di aggiornamento del firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr** Puntatore all'oggetto firmware del client LWM2M.
- **risultato** Risultato dell'aggiornamento.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the update result resource of the firmware object.  */
status = nx_lwm2m_client_firmware_result_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_RESULT_SUCCESS);

/* If status is NX_SUCCESS, the update result resource was successfully set.  */
```

##  <a name="nx_lwm2m_client_firmware_state_set"></a>nx_lwm2m_client_firmware_state_set

Imposta la risorsa risultato aggiornamento dell'oggetto aggiornamento firmware.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_firmware_state_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a>Descrizione

Il servizio viene usato dall'applicazione per impostare lo stato dell'oggetto di aggiornamento del firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr** Puntatore all'oggetto firmware del client LWM2M.
- **stato** di Stato dell'oggetto firmware.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the state of the firmware object.  */
status = nx_lwm2m_client_firmware_state_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_STATE_IDLE);

/* If status is NX_SUCCESS, the state was successfully set.  */
```

## <a name="nx_lwm2m_client_lock"></a>nx_lwm2m_client_lock

Blocca il client LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT **nx_lwm2m_client_lock**(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio blocca il client LWM2M per impedire l'accesso simultaneo agli oggetti LWM2M dai server o da un altro thread dell'applicazione.

Se il client LWM2M è attualmente bloccato da un altro thread, la funzione si bloccherà fino a quando non viene sbloccato il client LWM2M.

Le chiamate alle coppie ***nx_lwm2m_client_lock** _/_ *_nx_lwm2m_client_unlock_** possono essere nidificate.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Lock the LWM2M client.  */
status = nx_lwm2m_client_lock(&lwm2m_client);

/* If status is NX_SUCCESS, lwm2m client was successfully locked.  */
```

## <a name="nx_lwm2m_client_object_add"></a>nx_lwm2m_client_object_add

Aggiunge un'implementazione dell'oggetto al client LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT **nx_lwm2m_client_object_add**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK object_operation);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una nuova implementazione dell'oggetto al client di LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_ptr** Puntatore alla struttura che definisce l'implementazione dell'oggetto.
- **object_id** ID dell'oggetto.
- **object_operation** Funzione di callback dell'operazione dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** ID oggetto già esistente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Add new object to the lwm2m client.  */
status = nx_lwm2m_client_object_add(&lwm2m_client, &object, 
                                    3303, object_operation);

/* If status is NX_SUCCESS, the new object was successfully added.  */
```

## <a name="nx_lwm2m_client_object_create"></a>nx_lwm2m_client_object_create

Crea una nuova istanza dell'oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_create(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di creazione su un oggetto del client LWM2M per creare una nuova istanza dell'oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_id** ID dell'oggetto.
- **instance_id_ptr** Puntatore all'ID della nuova istanza, può essere **null** se il client LWM2M deve assegnare un ID istanza. Se l'ID è il valore riservato 65535, il client LWM2M assegnerà un ID istanza. Se non è NULL, l'ID assegnato viene restituito dopo la chiamata.
- **num_values** Numero di valori da impostare.
- **values_ptr** Puntatore a una matrice di valori di risorsa per inizializzare la nuova istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** L'ID dell'istanza dell'oggetto esiste già.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** L'oggetto non supporta la creazione di istanze.
- **NX_LWM2M_CLIENT_NO_MEMORY** Impossibile allocare memoria per archiviare la nuova istanza.
- **NX_LWM2M_CLIENT_NOT_FOUND** L'ID oggetto non esiste.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Create new object instance.  */
status = nx_lwm2m_client_object_create(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, a new object instance was successfully created.  */
```

## <a name="nx_lwm2m_client_object_delete"></a>nx_lwm2m_client_object_delete

Elimina un'istanza dell'oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_delete(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di eliminazione su un'istanza di oggetto del client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_id** ID dell'oggetto.
- **Instance_Id** ID dell'istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** L'oggetto non supporta l'eliminazione dell'istanza.
- **NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto o ID istanza oggetto inesistente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Delete an object instance.  */
status = nx_lwm2m_client_object_delete(&lwm2m_client, 3303, 0);

/* If status is NX_SUCCESS, an object instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_object_discover"></a>nx_lwm2m_client_object_discover

Individua le risorse di un'istanza dell'oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_discover(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT *num_resources,
    NX_LWM2M_CLIENT_RESOURCE *resources);

```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di individuazione su un'istanza dell'oggetto del client LWM2M, restituisce l'elenco delle risorse implementate dall'oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_id** ID dell'oggetto.
- **Instance_Id** ID dell'istanza dell'oggetto.
- **num_resources** In input dimensione del buffer di destinazione, in output il numero di elementi scritti nel buffer.
- **risorse** di Puntatore al buffer di destinazione.

### <a name="return-values"></a>Valori restituiti

- *NX_SUCCESS** operazione riuscita.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Il buffer di risorse è troppo piccolo per archiviare l'elenco di risorse.
- **NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto o ID istanza oggetto inesistente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
NX_LWM2M_CLIENT_RESOURCE resources[10]
UINT num_resources = 10;

/* Discover object resources.  */
status = nx_lwm2m_client_object_discover(&lwm2m_client, 3303, 0, 
                                         &num_resources, resource);

/* If status is NX_SUCCESS, discover object resources successfully.  */
```

## <a name="nx_lwm2m_client_object_execute"></a>nx_lwm2m_client_object_execute

Esegue un'operazione di esecuzione su una risorsa di un'istanza dell'oggetto.

### <a name="prototype"></a>Prototipo

```C
UINT **nx_lwm2m_client_object_execute**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr,
    UINT arguments_length);
```

### <a name="description"></a>Descrizione

Questo servizio esegue l'operazione di esecuzione su una risorsa dell'istanza di oggetto del client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_id** ID dell'oggetto.
- **Instance_Id** ID dell'istanza dell'oggetto.
- **resource_id** ID della risorsa.
- **arguments_ptr** Puntatore agli argomenti dell'operazione di esecuzione. Può essere NULL se arguments_length è zero.
- **arguments_length** Lunghezza degli argomenti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Il buffer di risorse è troppo piccolo per archiviare l'elenco di risorse.
- **NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto o ID istanza oggetto inesistente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Execute object resource.  */
status = nx_lwm2m_client_object_execute (&lwm2m_client, 3303, 0, 0,  
                                         “5”, 1);

/* If status is NX_SUCCESS, an object resource was successfully executed.  */
```

## <a name="nx_lwm2m_client_object_instance_add"></a>nx_lwm2m_client_object_instance_add

Aggiunge un'implementazione dell'istanza di oggetto a un oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_instance_add(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una nuova implementazione dell'istanza di oggetto al client di LWM2M. Se il valore di instance_id_ptr è **NX_LWM2M_CLIENT_RESERVED_ID**, il client di LWM2M assegna automaticamente un ID istanza non usato. in caso contrario, il client LWM2M utilizzerà il valore impostato per l'applicazione. Una volta aggiunta la nuova istanza, l'instance_id verrà compilata instance_id_ptr per tornare all'applicazione.

### <a name="parameters"></a>Parametri

- **object_ptr** Puntatore alla struttura che definisce l'implementazione dell'oggetto.
- **instance_ptr** Puntatore alla struttura che definisce l'implementazione dell'istanza dell'oggetto.
- **instance_id_ptr** Puntatore all'ID dell'istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_CLIENT_LWM2M_ALREADY_EXIST** ID oggetto già esistente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Add new object instance to the object.  */
status = nx_lwm2m_client_object_instance_add(&object, &object_instance,
                                             &instance_id);

/* If status is NX_SUCCESS, the new object instance was successfully added.  */
```

## <a name="nx_lwm2m_client_object_instance_next_get"></a>nx_lwm2m_client_object_instance_next_get

Ottiene l'istanza successiva di un oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_instance_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'ID dell'istanza di oggetto successiva dell'oggetto specificato. Se l'ID istanza corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito l'ID della prima istanza.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_id** ID dell'oggetto.
- **instance_id_ptr** Puntatore all'ID dell'istanza dell'oggetto corrente. In return contiene l'ID dell'istanza successiva dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_CLIENT_LWM2M_NOT_FOUND** L'ID istanza specificato è l'ultimo dell'oggetto o l'ID oggetto non è implementato.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the next instance of an object.  */
status = nx_lwm2m_client_object_instance_next_get(&lwm2m_client, 3303, 
                                                  &instance_id);

/* If status is NX_SUCCESS, get the next instance successfully.  */
```

## <a name="nx_lwm2m_client_object_instance_remove"></a>nx_lwm2m_client_object_instance_remove

Rimuove un'implementazione dell'istanza di oggetto da un oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_instance_remove(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove un'istanza di oggetto da un oggetto.

### <a name="parameters"></a>Parametri

- ***object_ptr*** Puntatore alla struttura che definisce l'implementazione dell'oggetto.
- **instance_ptr** Puntatore alla struttura che definisce l'implementazione dell'istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** ID oggetto già esistente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Remove object instance from an object.  */
status = nx_lwm2m_client_object_instance_remove(&object, &object_instance);

/* If status is NX_SUCCESS, the object instance was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_next_get"></a>nx_lwm2m_client_object_next_get

Ottiene l'oggetto successivo del client LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID \*object_id_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'ID dell'oggetto successivo implementato dal client LWM2M. Se l'ID oggetto corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito il primo ID oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_id_ptr** Puntatore all'ID dell'oggetto corrente. Il risultato restituito contiene l'ID oggetto successivo implementato dal client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_NOT_FOUND** L'ID oggetto specificato è l'ultimo del database.
**NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the next object of lwm2m client.  */
status = nx_lwm2m_client_object_next_get(&lwm2m_client, &object_id);

/* If status is NX_SUCCESS, get the next object successfully.  */
```

## <a name="nx_lwm2m_client_object_read"></a>nx_lwm2m_client_object_read

Legge i valori resource's di un'istanza di oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_read(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di lettura su un'istanza di oggetto del client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_id** ID dell'oggetto.
- **Instance_Id** ID dell'istanza dell'oggetto.
- **num_values** Numero di risorse da leggere.
- **values_ptr** Puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse da leggere. In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Una risorsa non supporta l'operazione di lettura.
- **NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto, ID istanza oggetto o ID risorsa inesistente.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Read the object resources.  */
status = nx_lwm2m_client_object_read(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, the resources were successfully read.  */
```

## <a name="nx_lwm2m_client_object_remove"></a>nx_lwm2m_client_object_remove

Rimuove un'implementazione dell'istanza di oggetto da un oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_remove(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove un oggetto dal client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_ptr** Puntatore alla struttura che definisce l'implementazione dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** ID oggetto già esistente.
- **NX_PTR_ERROR** Puntatore non valido.
- **NX_LWM2M_CLIENT_FORBIDDEN** La rimozione dell'oggetto interno non è consentita.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Remove object from lwm2m client.  */
status = nx_lwm2m_client_object_remove(&lwm2m_client, &object);

/* If status is NX_SUCCESS, the object was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_resource_changed"></a>nx_lwm2m_client_object_resource_changed

Segnala una modifica di una risorsa dell'oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_resource_changed(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Descrizione

Il servizio viene usato dall'applicazione per segnalare al client LWM2M che una risorsa dell'oggetto è stata modificata. Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.

### <a name="parameters"></a>Parametri

- **object_ptr** Puntatore alla struttura che definisce l'implementazione dell'oggetto.
- ***instance_ptr*** Puntatore alla struttura che definisce l'implementazione dell'istanza dell'oggetto.
- **risorsa** di Puntatore alla struttura che descrive la risorsa che è stata modificata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Change object resource.  */
status = nx_lwm2m_client_object_resource_changed(&object, &instance, &resource);

/* If status is NX_SUCCESS, a resource was successfully changed.  */
```

## <a name="nx_lwm2m_client_object_write"></a>nx_lwm2m_client_object_write

Modifica i valori della risorsa di un'istanza dell'oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_write(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr,
    UINT write_op);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di scrittura su un'istanza di oggetto del client LWM2M.

È possibile specificare le operazioni di scrittura seguenti per il parametro *write_op* .

| Valore | Operazione di scrittura &nbsp; | Descrizione |
| --- | ---| --- |
| 0 | Aggiornamento parziale | Aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate le altre risorse esistenti. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE** | Sostituisci istanza | Sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa specificati. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE** | Sostituisci risorsa | Sostituisce le risorse con i nuovi valori di risorsa forniti, usati per sostituire più risorse. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP** | Scrittura bootstrap | Indica una chiamata da una sequenza di bootstrap. |

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.
- **object_id** ID dell'oggetto.
- **Instance_Id** ID dell'istanza dell'oggetto.
- **num_values** Numero di risorse da scrivere.
- **values_ptr** Puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse, i tipi e i valori da scrivere.
- **write_op** Tipo di operazione di scrittura.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il tipo di una risorsa non è valido.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** La lunghezza di un valore è troppo grande per essere archiviata nell'istanza di.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Una risorsa non supporta l'operazione di scrittura.
- **NX_LWM2M_CLIENT_NO_MEMORY** Impossibile allocare memoria per archiviare un valore di risorsa.
- **NX_LWM2M_CLIENT_NOT_ACCEPTABLE** Il valore di una risorsa non è valido.
- **NX_LWM2M_CLIENT_NOT_FOUND** ID oggetto, ID istanza oggetto o ID risorsa inesistente.
- **NX_OPTION_ERROR** Tipo di operazione di scrittura non valido. 
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Write object resources.  */
status = nx_lwm2m_client_object_write(&lwm2m_client, 3303, 0, 2, &resource,
                                      NX_LWM2M_CLIENT_OBJECT_WRITE_UPDATE);

/* If status is NX_SUCCESS, write object resources successfully.  */
```

## <a name="nx_lwm2m_client_resource_boolean_get"></a>nx_lwm2m_client_resource_boolean_get

Ottiene il valore di una risorsa booleana.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_boolean_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa booleana.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla descrizione del valore della risorsa.
- **bool_ptr** Puntatore al valore booleano di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore booleano.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the value of a Boolean resource.  */
status = nx_lwm2m_client_resource_boolean_get(&resource, &bool);

/* If status is NX_SUCCESS, the value of Boolean resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_boolean_set"></a>nx_lwm2m_client_resource_boolean_set

Imposta il valore di una risorsa booleana.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_boolean_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_BOOL bool_data);
```

### <a name="description"></a>Descrizione

Il servizio imposta il valore di una risorsa booleana.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **bool_data** Dati booleani.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the value of a Boolean resource.  */
status = nx_lwm2m_client_resource_boolean_set(&resource, NX_TRUE);

/* If status is NX_SUCCESS, the value of Boolean resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_dim_get"></a>nx_lwm2m_client_resource_dim_get

Ottiene la dimensione della risorsa per più risorse

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_dim_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    UCHAR *dim);
```

### <a name="description"></a>Descrizione

Il servizio recupera la dimensione della risorsa per più risorse.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- puntatore **Dim** alla dimensione di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore booleano.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the resource dimension for multiple resource.  */
status = nx_lwm2m_client_resource_dim_get(&resource, &dim);

/* If status is NX_SUCCESS, the resource dimension was successfully get. */
```

## <a name="nx_lwm2m_client_resource_dim_set"></a>nx_lwm2m_client_resource_dim_set

Imposta la dimensione della risorsa per più risorse.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_dim_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    CHAR dim);
```

### <a name="description"></a>Descrizione

Il servizio imposta la dimensione della risorsa per più risorse.

### <a name="parameters"></a>Parametri

- **valore** di Puntatore alla descrizione del valore della risorsa.
- valore **Dim** della dimensione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the resource dimension.  */
status = nx_lwm2m_client_resource_dim_set(&resource, 3);

/* If status is NX_SUCCESS, the resource dimension was successfully set. */
```

## <a name="nx_lwm2m_client_resource_float32_get"></a>nx_lwm2m_client_resource_float32_get

Ottiene il valore di una risorsa **float** a 32 bit.

### <a name="prototype"></a>Prototipo

```C
UINT nx_lwm2m_client_resource_float32_get(
    NX_LWM2M_CLIENT_RESOURCE *resource,
    NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa **float** a 32 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **float32_ptr** Puntatore al valore **float** a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore booleano.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```C
/* Get the value of a 32-Bit float resource.  */
status = nx_lwm2m_client_resource_float32_get(&resource, &float32);

/* If status is NX_SUCCESS, the value of 32-Bit float resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_float32_set"></a>nx_lwm2m_client_resource_float32_set

Imposta il valore di una risorsa **float** a 32 bit

### <a name="prototype"></a>Prototipo

```C
UINT nx_lwm2m_client_resource_float32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource,
    NX_LWM2M_FLOAT32 float32_data);
```

### <a name="description"></a>Descrizione

Il servizio imposta il valore di una risorsa **float** a 32 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **float32_data** dati **float** a 32 bit.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the value of a 32-Bit float resource.  */
status = nx_lwm2m_client_resource_float32_set(&resource, 1.24);

/* If status is NX_SUCCESS, the value of 32-Bit float resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_float64_get"></a>nx_lwm2m_client_resource_float64_get

Ottiene il valore di una risorsa float a 64 bit.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_float64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa **float** a 64 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **float64_ptr** Puntatore al valore **float** a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore float.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the value of a 64-Bit float resource.  */
status = nx_lwm2m_client_resource_float64_get(&resource, &float64);

/* If status is NX_SUCCESS, the value of 64-Bit float resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_float64_set"></a>nx_lwm2m_client_resource_float64_set

Imposta il valore di una risorsa **float** a 64 bit.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_float64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_FLOAT64 float64_data);
```

### <a name="description"></a>Descrizione

Il servizio imposta il valore di una risorsa **float** a 64 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **float64_data** dati **float** a 64 bit.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the value of a 64-Bit float resource.  */
status = nx_lwm2m_client_resource_float64_set(&resource, 1.24);

/* If status is NX_SUCCESS, the value of 64-Bit float resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_info_get"></a>nx_lwm2m_client_resource_info_get

Ottiene le informazioni sulla risorsa.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_info_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *resource_id, 
    ULONG *operation);
```

### <a name="description"></a>Descrizione

Il servizio recupera le informazioni sulla risorsa della risorsa.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **resource_id** Puntatore all'ID risorsa di destinazione.
- **operazione** di Puntatore all'operazione della risorsa di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the resource information.  */
status = nx_lwm2m_client_resource_info_get(&resource, &resource_id, &operation);

/* If status is NX_SUCCESS, the resource information was successfully get. */
```

## <a name="nx_lwm2m_client_resource_info_set"></a>nx_lwm2m_client_resource_info_set

Imposta le informazioni sulla risorsa.

### <a name="prototype"></a>Prototipo

```C
UINT nx_lwm2m_client_resource_info_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    NX_LWM2M_FLOAT64 float64_data);
```

### <a name="description"></a>Descrizione

Il servizio imposta le informazioni sulla risorsa.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **resource_id** ID della risorsa.
- **operazione** di Operazione della risorsa.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the resource information.  */
status = nx_lwm2m_client_resource_info_set(&resource, 0, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);

/* If status is NX_SUCCESS, the resource information was successfully set. */
```

## <a name="nx_lwm2m_client_resource_instances_get"></a>nx_lwm2m_client_resource_instances_get

Ottiene l'istanza di più risorse.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_instances_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_CLIENT_RESOURCE *resource_instances, 
    UINT *count);
```

### <a name="description"></a>Descrizione

Il servizio recupera le informazioni sulla risorsa della risorsa.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **resource_instances** Puntatore all'ID risorsa di destinazione.
- **numero** di Puntatore al conteggio.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore booleano.
- **NX_LWM2M_CLIENT_NO_MEMORY** Nessuna memoria per compilare le istanze.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the resource information.  */
status = nx_lwm2m_client_resource_instances_get(&resource, &resource_instances,
                                                &count);

/* If status is NX_SUCCESS, the instances of multiple resource information were successfully get. */
```

## <a name="nx_lwm2m_client_resource_instances_set"></a>nx_lwm2m_client_resource_instances_set

Imposta le istanze della risorsa.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_instances_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_CLIENT_RESOURCE *resource_instances, 
    UINT count);
```
### <a name="description"></a>Descrizione

Il servizio imposta le istanze di risorse per più risorse.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **resource_instance** Puntatore a istanze di risorse.
- **numero** di Conteggio delle istanze di risorse.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the resource information.  */
status = nx_lwm2m_client_resource_instances_set(&resource, &resource_instance, 2);

/* If status is NX_SUCCESS, the resource instances were successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer32_get"></a>nx_lwm2m_client_resource_integer32_get

Ottiene il valore di una risorsa Integer a 32 bit.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_integer32_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 *integer32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa Integer a 32 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **integer32_ptr** Puntatore al valore integer a 32 bit.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore intero.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_get(&resource, &integer32);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer32_set"></a>nx_lwm2m_client_resource_integer32_set

Imposta il valore di una risorsa Integer a 32 bit.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_integer32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 integer32_data);
```

### <a name="description"></a>Descrizione

Il servizio imposta il valore di una risorsa Integer a 32 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **integer32_data** dati integer a 32 bit.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_set(&resource, 8);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer64_get"></a>nx_lwm2m_client_resource_integer64_get

Ottiene il valore di una risorsa Integer a 64 bit.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_integer64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 *integer64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa Integer a 64 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **integer64_ptr** Puntatore al valore integer a 64 bit.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore integer a 64 bit.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_get(&resource, &integer64);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer64_set"></a>nx_lwm2m_client_resource_integer64_set

## <a name="set-the-value-of-a-64-bit-integer-resource"></a>Impostare il valore di una risorsa Integer a 64 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_integer64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 integer64_data);
```

### <a name="description"></a>Descrizione

Il servizio imposta il valore di una risorsa Integer a 64 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **integer64_data** intero a 64 bit.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_set(&resource, 32323);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully set. */
```

##  <a name="nx_lwm2m_client_resource_objlnk_get"></a>nx_lwm2m_client_resource_objlnk_get

Ottiene il valore di una risorsa di collegamento a un oggetto.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_objlnk_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *object_id, 
    NX_LWM2M_ID *instance_id);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore del collegamento all'oggetto.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **object_id** Puntatore all'ID dell'oggetto.
- **Instance_Id** Puntatore all'ID dell'istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore di collegamento all'oggetto.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the value of the object link resource.  */
status = nx_lwm2m_client_resource_objlnk_get(&resource, &object_id, &instance_id);

/* If status is NX_SUCCESS, the object link value was successfully get. */
```

## <a name="nx_lwm2m_client_resource_objlnk_set"></a>nx_lwm2m_client_resource_objlnk_set

Imposta le istanze di risorse

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_objlnk_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    NX_LWM2M_ID object_id, 
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Descrizione

Il servizio imposta il valore della risorsa collegamento a oggetti.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **object_id** ID oggetto.
- **Instance_Id** ID istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the value of object link resource.  */
status = nx_lwm2m_client_resource_objlnk_set(&resource, 3303, 2);

/* If status is NX_SUCCESS, the value of object link resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_opaque_get"></a>nx_lwm2m_client_resource_opaque_get

Ottiene il valore di una risorsa opaca.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_opaque_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const VOID **opaque_ptr, 
    UINT \*opaque_length);
```


### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa opaca. Un valore di risorsa opaco è costituito da un puntatore a un buffer e una lunghezza.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **opaque_ptr** Puntatore ai dati opachi.
- **opaque_length** Puntatore alla lunghezza dei dati opachi.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è una risorsa opaca.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_get(&resource, &opaque_ptr, &opaque_length);

/* If status is NX_SUCCESS, the value of opaque resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_opaque_set"></a>nx_lwm2m_client_resource_opaque_set

Imposta il valore di una risorsa opaca.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_opaque_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    VOID *opaque_ptr, 
    UINT opaque_length);
```

### <a name="description"></a>Descrizione

Il servizio imposta il valore di una risorsa opaca.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **opaque_ptr** Puntatore ai dati opachi.
- **opaque_length** Lunghezza dei dati opachi.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_set(&resource, “AQIDBAU=”, 8);

/* If status is NX_SUCCESS, the value of opaque resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_string_get"></a>nx_lwm2m_client_resource_string_get

Ottiene il valore di una risorsa di stringa.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_string_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const CHAR **string_ptr, 
    UINT *string_length);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa di stringa.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **string_ptr** Puntatore al puntatore della stringa di destinazione.
- **string_length** Puntatore alla lunghezza della stringa di destinazione. Può essere **null** se la stringa è con terminazione null.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Il valore della risorsa non è un valore stringa.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the value of a string resource.  */
status = nx_lwm2m_client_resource_string_get(&resource, &string_ptr, &string_length);

/* If status is NX_SUCCESS, the value of string resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_string_set"></a>nx_lwm2m_client_resource_string_set

Imposta il valore di una risorsa di stringa.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_resource_string_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    CHAR *string_ptr, 
    UINT string_length);
```

### <a name="description"></a>Descrizione

Il servizio imposta il valore di una risorsa Integer a 64 bit.

### <a name="parameters"></a>Parametri

- **risorsa** di Puntatore alla risorsa.
- **string_ptr** Puntatore alla stringa.
- **string_length** Lunghezza della stringa.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Set the value of a string resource.  */
status = nx_lwm2m_client_resource_string_set(&resource, “test”, sizeof(“test”) - 1);

/* If status is NX_SUCCESS, the value of string resource was successfully set. */
```

## <a name="nx_lwm2m_client_session_bootstrap"></a>nx_lwm2m_client_session_bootstrap

Avvia una sessione con un server bootstrap.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_bootstrap(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID security_id, 
    ULONG ip_address, 
    UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione con un server bootstrap. Il server deve disporre di un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.

Se la risorsa ' Mantieni fuori ' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà il bootstrap avviato dal server, se non è stato avviato alcun bootstrap dal server dopo questo periodo di tempo in cui verrà eseguito un bootstrap avviato dal client.

Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server bootstrap.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.
- **security_id** L'ID dell'istanza di sicurezza del server bootstrap deve essere impostato su NX_LWM2M_RESERVED_ID (65535) se nel server bootstrap non è definita alcuna istanza di sicurezza.
- **ip_address** Indirizzo IP del server.
- **porta** Porta UDP del server.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_ERROR** Errore bootstrap.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Start bootstrap.  */
status = nx_lwm2m_client_session_bootstrap(&lwm2m_client, 0, &ip_address, 5783);

/* If status is NX_SUCCESS, start bootstrap successfully.  */
```

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a>nx_lwm2m_client_session_bootstrap_dtls

Avvia una sessione protetta con un server bootstrap

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID security_id, 
    ULONG ip_address, 
    UINT port, 
    NX_SECURE_DTLS_SESSION *dtls_session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione con un server bootstrap usando una connessione DTLS sicura. Il server deve disporre di un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.

Prima di chiamare questa funzione, è necessario che la sessione DTLS sia stata configurata con i pacchetti di crittografia e il materiale della chiave appropriati. È necessario definire **NX_SECURE_ENABLE_DTLS** .

Se la risorsa ' Mantieni fuori ' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà il bootstrap avviato dal server, se non è stato avviato alcun bootstrap dal server dopo questo periodo di tempo in cui verrà eseguito un bootstrap avviato dal client. 

Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server bootstrap.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.
- **security_id** L'ID dell'istanza di sicurezza del server bootstrap deve essere impostato su **NX_LWM2M_RESERVED_ID** (65535) se nel server bootstrap non è definita alcuna istanza di sicurezza.
- **ip_address** Indirizzo IP del server.
- **porta** Porta UDP del server.
- **dtls_session_ptr** Sessione DTLS da utilizzare per la sessione bootstrap.
- **dtls_local_port** Porta UDP locale utilizzata per la sessione DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_ERROR** Errore bootstrap.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Start bootstrap with DTLS.  */
status = nx_lwm2m_client_session_bootstrap_dtls(&lwm2m_client, 0, &ip_address, 5784, &dtls_session);

/* If status is NX_SUCCESS, start bootstrap successfully.  */
```

## <a name="nx_lwm2m_client_session_create"></a>nx_lwm2m_client_session_create

Crea una sessione client LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_create(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK state_callback);
```

### <a name="description"></a>Descrizione

Questo servizio crea una nuova sessione client di LWM2M collegata a un client LWM2M esistente. La sessione viene usata dal client LWM2M per comunicare con un server bootstrap o un server LWM2M. 

L'applicazione deve fornire una funzione di callback che verrà chiamata quando viene aggiornato lo stato della sessione.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.
- **client_ptr** Puntatore al client LWM2M creato in precedenza.
- **state_callback** Callback dell'applicazione che viene chiamato quando lo stato della sessione viene modificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Create session.  */
status = nx_lwm2m_client_session_create(&session, &lwm2m_client, session_callback);

/* If status is NX_SUCCESS, a session was successfully created.  */
```

## <a name="nx_lwm2m_client_session_delete"></a>nx_lwm2m_client_session_delete

Elimina una sessione client LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina una sessione client di LWM2M.

Quando un client LWM2M viene eliminato chiamando nx_lwm2m_client_delete vengono eliminate anche tutte le sessioni associate al client.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Delete session.  */
status = nx_lwm2m_client_session_delete(&session);

/* If status is NX_SUCCESS, a session was successfully deleted.  */
```

## <a name="nx_lwm2m_client_session_deregister"></a>nx_lwm2m_client_session_deregister

Termina una sessione con un server LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di annullamento della registrazione in un server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_NOT_REGISTERED** Il client non è registrato nel server.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* De-register session.  */
status = nx_lwm2m_client_session_deregister(&session);

/* If status is NX_SUCCESS, session was successfully de-registered.  */
```

## <a name="nx_lwm2m_client_session_error_get"></a>nx_lwm2m_client_session_error_get

Ottiene l'ultimo errore di una sessione.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il codice di errore della sessione quando la sessione è in stato di errore.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** La sessione non è in stato di errore.
- **NX_LWM2M_CLIENT_ADDRESS_ERROR** Indirizzo server non valido.
- **NX_LWM2M_ CLIENT_BUFFER_TOO_SMALL** Il payload della richiesta non rientra nel buffer di rete.
- **NX_LWM2M_ CLIENT_DTLS_ERROR** Impossibile stabilire una connessione protetta con il server.
- **NX_LWM2M_ CLIENT_ERROR** Errore non specificato.
- **NX_LWM2M_ CLIENT_FORBIDDEN** La registrazione è stata rifiutata dal server.
- **NX_LWM2M_ CLIENT_NOT_FOUND** Client non trovato dal server durante l'aggiornamento/annullamento della registrazione.
- **NX_LWM2M_ CLIENT_SERVER_INSTANCE_DELETED** L'istanza dell'oggetto server corrispondente alla sessione è stata eliminata.
- **NX_LWM2M_ CLIENT_TIMED_OUT** Nessuna risposta dal server.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the error.  */
status = nx_lwm2m_client_session_error_get(&session);
```
## <a name="nx_lwm2m_client_session_register"></a>nx_lwm2m_client_session_register

Avvia una sessione con un server LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_register(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID server_id, 
    ULONG ip_address, 
    UINT port);
```


### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di registrazione in un server LWM2M. Il server deve disporre di un'istanza del server corrispondente nell'oggetto server.

Se la registrazione ha esito positivo, il client LWM2M elaborerà ulteriori operazioni dal server e invierà periodicamente messaggi di aggiornamento finché il client non viene deregistrato.

Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.
- **server_id** ID server breve del server LWM2M.
- **ip_address** Indirizzo IP del server.
- **porta** Porta UDP del server.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_ERROR** Errore bootstrap.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Start register.  */
status = nx_lwm2m_client_session_register (&lwm2m_client, 123, &ip_address, 5683);

/* If status is NX_SUCCESS, start register successfully.  */
```

## <a name="nx_lwm2m_client_session_register_dtls"></a>nx_lwm2m_client_session_register_dtls

Avvia una sessione protetta con un server LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_register_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID server_id, 
    ULONG ip_address, 
    UINT port,
    NX_SECURE_DTLS_SESSION *dtls_session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di registrazione in un server LWM2M usando una connessione DTLS sicura. Il server deve disporre di un'istanza del server corrispondente nell'oggetto server.

Prima di chiamare questa funzione, è necessario che la sessione DTLS sia stata configurata con i pacchetti di crittografia e il materiale della chiave appropriati. È necessario definire **NX_SECURE_ENABLE_DTLS** .

Se la registrazione ha esito positivo, il client LWM2M elaborerà ulteriori operazioni dal server e invierà periodicamente messaggi di aggiornamento finché il client non viene deregistrato.

Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.
- **server_id** ID server breve del server LWM2M.
- **ip_address** Indirizzo IP del server.
- **porta** Porta UDP del server.
- **dtls_session_ptr** Sessione DTLS da utilizzare per la sessione LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_ERROR** Errore bootstrap.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** La porta non è disponibile.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Start register with DTLS.  */
status = nx_lwm2m_client_session_register_dtls(&lwm2m_client, 123, &ip_address, 5683, &dtls_session);

/* If status is NX_SUCCESS, start register with DTLS successfully.  */
```

## <a name="nx_lwm2m_client_session_register_info_get"></a>nx_lwm2m_client_session_register_info_get

Avvia una sessione protetta con un server LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_register_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    UINT security_instance_id, 
    NX_LWM2M_ID *server_id,
    CHAR **server_uri, 
    UINT *server_uri_length, 
    UCHAR *security_mode, 
    UCHAR **pub_key_or_id, 
    UINT *pub_key_or_id_len, 
    UCHAR **server_pub_key, 
    UINT *server_pub_key_len, 
    UCHAR **secret_key, 
    UINT *secret_key_len);
```

### <a name="description"></a>Descrizione

Una volta stabilita una sessione di comunicazione con un server bootstrap. L'applicazione può chiamare questa API per ottenere le informazioni sul server e sulla sicurezza per il passaggio di registrazione successivo.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.
- **security_instance_id** ID istanza di sicurezza.
- **server_id** Puntatore all'ID del server di destinazione.
- **server_uri** Puntatore all'URI del server di destinazione.
- **server_uri_len** Puntatore alla lunghezza dell'URI del server di destinazione.
- **security_mode** Puntatore alla modalità di sicurezza di destinazione.
- **pub_key_or_id** Puntatore alla chiave pubblica o all'identità di destinazione.
- **pub_key_or_id_len** Puntatore alla chiave pubblica della destinazione o alla lunghezza dell'identità.
- **server_pub_key** Puntatore alla chiave pubblica del server di destinazione.
- **server_pub_key_len** Puntatore alla lunghezza della chiave pubblica del server di destinazione.
- **SECRET_KEY** Puntatore alla chiave privata di destinazione.
- **secret_key_len** Puntatore alla lunghezza della chiave privata di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nessuna istanza di oggetto di sicurezza.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Get the register information.  */
status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_length, &security_mode, &pub_key_or_id, &pub_key_or_id_len, NX_NULL, NX_NULL, &secret_key, &secret_key_len);

/* If status is NX_SUCCESS, the register information was successfully gotten.  */
```

## <a name="nx_lwm2m_client_session_update"></a>nx_lwm2m_client_session_update

Aggiorna una sessione con un server LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di aggiornamento in un server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr** Puntatore al blocco di controllo della sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_LWM2M_CLIENT_NOT_REGISTERED** Il client non è registrato nel server.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Update a session.  */
status = nx_lwm2m_client_session_update(&session);

/* If status is NX_SUCCESS, a session was successfully updated.  */
```

## <a name="nx_lwm2m_client_unlock"></a>nx_lwm2m_client_unlock

Sblocca un client LWM2M.

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Sblocca il client LWM2M precedentemente bloccato da una chiamata a ***nx_lwm2m_client_unlock***.

### <a name="parameters"></a>Parametri

- **client_ptr** Puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** Operazione completata.
- **NX_PTR_ERROR** Puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
/* Unlock lwm2m client.  */
status = nx_lwm2m_client_unlock(&lwm2m_client);

/* If status is NX_SUCCESS, unlock lwm2m client successfully.  */
```