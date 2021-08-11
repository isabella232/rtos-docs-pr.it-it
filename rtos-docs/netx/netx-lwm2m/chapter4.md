---
title: Capitolo 4 - Descrizione dei Azure RTOS NetX LWM2M
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX LWM2M (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 171f8577d252027548c24ec92f11f03c1fae768f1676f476256c13b8e8dc4175
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799082"
---
# <a name="chapter-4---description-of-azure-rtos-netx-lwm2m-services"></a>Capitolo 4 - Descrizione dei Azure RTOS NetX LWM2M

Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX LWM2M (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **grassetto** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

### <a name="lwm2m-client-management"></a>Gestione client LWM2M

- **nx_lwm2m_client_create:** Creare *il client LWM2M*
- **nx_lwm2m_client_delete:** Eliminare *il client LWM2M*
- **nx_lwm2m_client_lock:** *Bloccare il client LWM2M*
- **nx_lwm2m_client_object_add:** Aggiungere *l'implementazione dell'oggetto al client LWM2M*
- **nx_lwm2m_client_unlock:** *Sbloccare il client LWM2M*

### <a name="lwm2m-client-session-management"></a>Gestione delle sessioni client LWM2M

- **nx_lwm2m_client_session_bootstrap**: *Avviare una sessione con un server Bootstrap*
- **nx_lwm2m_client_session_bootstrap_dtls**: *Avviare una sessione protetta con un server Bootstrap*
- **nx_lwm2m_client_session_create:** Creare *una sessione client LWM2M*
- **nx_lwm2m_client_session_delete:** *Elimina sessione client LWM2M*
- **nx_lwm2m_client_session_deregister**: *Terminare una sessione con un server LWM2M*
- **nx_lwm2m_client_session_error_get:** Ottenere *l'ultimo errore di una sessione*
- **nx_lwm2m_client_session_register:** Avviare *una sessione con un server LWM2M*
- **nx_lwm2m_client_session_register_dtls:** Avviare *una sessione protetta con un server LWM2M*
- **nx_lwm2m_client_session_update:** Aggiornare *una sessione con un server LWM2M*

### <a name="security-object-implementation"></a>Implementazione degli oggetti di sicurezza

- **nx_lwm2m_client_security_key_callbacks_set:** Impostare *i callback di gestione delle chiavi di sicurezza*

### <a name="device-object-implementation"></a>Implementazione dell'oggetto dispositivo

- **nx_lwm2m_client_device_callbacks_set:** Impostare *i callback dell'applicazione dell'oggetto dispositivo*
- **nx_lwm2m_client_device_error_push:** Aggiungere *il codice di errore all'oggetto dispositivo*
- **nx_lwm2m_client_device_error_reset**: *Reimposta i codici di errore dell'oggetto dispositivo*
- **nx_lwm2m_client_device_resource_changed:** Modifica *del segnale della risorsa oggetto dispositivo*

### <a name="custom-objects-implementation"></a>Implementazione di oggetti personalizzati

- **nx_lwm2m_object_resource_changed:** segnala *la modifica di un valore di risorsa di un'istanza dell'oggetto*

### <a name="local-device-management"></a>Gestione dei dispositivi locali

- **nx_lwm2m_client_object_create:** Creare *una nuova istanza dell'oggetto*
- **nx_lwm2m_client_object_delete:** *Eliminare un'istanza dell'oggetto*
- **nx_lwm2m_client_object_discover:** Individuare *le risorse di un'istanza di oggetto*
- **nx_lwm2m_client_object_execute:** Eseguire *la risorsa di un'istanza di oggetto*
- **nx_lwm2m_client_object_get_next:** ottenere *l'elenco degli oggetti implementati dal client LWM2M*
- **nx_lwm2m_client_object_instance_get_next**: *ottenere l'elenco di istanze di un oggetto*
- **nx_lwm2m_client_object_read:** Leggere *i valori delle risorse di un'istanza dell'oggetto*
- **nx_lwm2m_client_object_write:** Modificare *i valori delle risorse di un'istanza di object*

### <a name="resources-values-decoding"></a>Decodifica dei valori delle risorse

- **nx_lwm2m_resource_get_boolean**: *Ottenere il valore di una risorsa booleana*
- **nx_lwm2m_resource_get_float32**: *ottenere il valore di una risorsa a virgola mobile a 32 bit*
- **nx_lwm2m_resource_get_float64**: *ottenere il valore di una risorsa a virgola mobile a 64 bit*
- **nx_lwm2m_resource_get_integer32**: ottenere il valore di una risorsa integer *a 32 bit*
- **nx_lwm2m_resource_get_integer64**: *ottenere il valore di una risorsa integer a 64 bit*
- **nx_lwm2m_resource_get_objlnk**: *ottenere il valore di una risorsa collegamento a oggetti*
- **nx_lwm2m_resource_get_opaque**: *ottenere il valore di una risorsa opaca*
- **nx_lwm2m_resource_get_string**: *ottenere il valore di una risorsa stringa*
- **nx_lwm2m_resource_multiple_get_boolean:** ottenere *il valore di un'istanza di risorsa multipla di risorsa booleana*
- **nx_lwm2m_resource_multiple_get_float32:** ottenere *il valore di un'istanza di* più risorse a virgola mobile a 32 bit
- **nx_lwm2m_resource_multiple_get_float64:** ottenere *il valore di un'istanza di* più risorse a virgola mobile a 64 bit
- **nx_lwm2m_resource_multiple_get_integer32**: *Ottenere il valore di un'istanza di* più risorse integer a 32 bit
- **nx_lwm2m_resource_multiple_get_integer64**: *ottenere il valore di un'istanza di più risorse integer a 64 bit*
- **nx_lwm2m_resource_multiple_get_objlnk:** ottenere *il valore di un'istanza di più risorse di Collegamento oggetto*
- **nx_lwm2m_resource_multiple_get_opaque**: *ottenere il valore di un'istanza di più risorse opaca*
- **nx_lwm2m_resource_multiple_get_string**: *ottenere il valore di un'istanza di più risorse stringa*

### <a name="firmware-update-object"></a>Oggetto di aggiornamento del firmware

- **nx_lwm2m_firmware_create:** Creare *un oggetto di aggiornamento del firmware*
- **nx_lwm2m_firmware_package_info_set:** Impostare *le informazioni sul pacchetto di aggiornamento del firmware*
- **nx_lwm2m_firmware_result_set:** Impostare *il risultato dell'aggiornamento del firmware*
- **nx_lwm2m_firmware_state_set:** Impostare *lo stato di aggiornamento del firmware*

## <a name="nx_lwm2m_client_create"></a>nx_lwm2m_client_create

Creare il client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_create(NX_LWM2M_CLIENT *client_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr, UINT local_port, const CHAR *name_ptr,
    const CHAR *msisdn_ptr, UCHAR binding_modes, VOID *stack_ptr, ULONG stack_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client LWM2M, che viene eseguita nel contesto del proprio thread ThreadX.

Il client LWM2M implementa i seguenti oggetti OMA LWM2M: Sicurezza (0), Server (1), Controllo di accesso (2) e Dispositivo (3). Le altre implementazioni di oggetti devono essere aggiunte dall'applicazione.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **ip_ptr:** puntatore a un'istanza IP creata in precedenza.
- **packet_pool_ptr**: puntatore al pool di pacchetti predefinito per questo client LWM2M.
- **local_port**: porta UDP locale usata per la comunicazione non sicura.
- **name_ptr:** puntatore al nome dell'endpoint del client LWM2M.
- **msisdn_ptr:** il puntatore al file MSISDN in cui il client LWM2M può essere raggiunto per l'uso con l'associazione SMS, può essere NULL se l'associazione SMS non è supportata.
- **binding_modes:** l'associazione e le modalità supportate dal client LWM2M devono essere una combinazione di flag NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S e NX_LWM2M_BINDING_SQ.
- **stack_ptr:** puntatore all'area dello stack di thread del client LWM2M.
- **stack_size:** dimensioni dello stack dei thread del client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** il client LWM2M è stato creato correttamente.
- **NX_LWM2M_ERROR:** errore di creazione del client LWM2M.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_delete"></a>nx_lwm2m_client_delete

Eliminare il client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del client LWM2M creata in precedenza.

Anche tutte le sessioni attualmente collegate al client vengono eliminate da questa chiamata.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** il client LWM2M è stato eliminato correttamente.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_device_callbacks_set"></a>nx_lwm2m_client_device_callbacks_set

Impostare i callback dell'applicazione dell'oggetto dispositivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_READ_CALLBACK read_callback,
    NX_LWM2M_CLIENT_DEVICE_DISCOVER_CALLBACK discover_callback,
    NX_LWM2M_CLIENT_DEVICE_WRITE_CALLBACK write_callback,
    NX_LWM2M_CLIENT_DEVICE_EXECUTE_CALLBACK execute_callback);
```

### <a name="description"></a>Descrizione

Questo servizio installa i callback dell'applicazione per l'implementazione di operazioni sulle risorse oggetto dispositivo LWM2M non gestite dal client LWM2M.

Il client LWM2M implementa le risorse seguenti: codice di errore (11), codice di errore di reimpostazione (12) e associazione e modalità supportate (16), le operazioni alle altre risorse vengono reindirizzate all'applicazione.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **read_callback:** callback del metodo 'Read'.
- **discover_callback:** callback del metodo 'Discover'.
- **write_callback:** callback del metodo 'Write'.
- **execute_callback:** callback del metodo 'Execute'.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_device_error_push"></a>nx_lwm2m_client_device_error_push

Aggiungere il codice di errore all'oggetto dispositivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_error_push(NX_LWM2M_CLIENT *client_ptr, UCHAR code);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una nuova istanza alla risorsa Codice errore (11) del dispositivo oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **code:** nuovo codice di errore.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BUFFER_TOO_SMALL:** è stato raggiunto il numero massimo di codici di errore archiviati.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_device_error_reset"></a>nx_lwm2m_client_device_error_reset

Reimpostare i codici di errore dell'oggetto dispositivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina tutte le istanze delle risorse con codice di errore dall'oggetto dispositivo. Equivale all'esecuzione del codice di errore di reimpostazione della risorsa (12).

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_device_resource_changed"></a>nx_lwm2m_client_device_resource_changed

Modifica del segnale della risorsa oggetto dispositivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_resource_changed(NX_LWM2M_CLIENT *client_ptr,
                                    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Descrizione

Il servizio viene usato dall'applicazione per segnalare al client LWM2M che una risorsa del dispositivo oggetto è stata modificata. Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **resource:** puntatore alla struttura che descrive la risorsa modificata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_lock"></a>nx_lwm2m_client_lock

Bloccare il client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_lock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio blocca il client LWM2M per impedire l'accesso concurente agli oggetti LWM2M dai server o da un altro thread dell'applicazione.

Se il client LWM2M è attualmente bloccato da un altro thread, la funzione si blocca fino a quando il client LWM2M non viene sbloccato.

Le chiamate nx_lwm2m_client_lock()/nx_lwm2m_client_unlock() possono essere annidate.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_add"></a>nx_lwm2m_client_object_add

Aggiungere l'implementazione dell'oggetto al client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_add(NX_LWM2M_CLIENT *client_ptr,
                                NX_LWM2M_OBJECT *object_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una nuova implementazione dell'oggetto al client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_ptr**: puntatore alla struttura che definisce l'implementazione dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_ALREADY_EXIST:** l'ID oggetto esiste già.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_create"></a>nx_lwm2m_client_object_create

Creare una nuova istanza dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_create(NX_LWM2M_CLIENT *client_ptr,
            NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr,
            UINT num_values, const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione 'Create' su un oggetto del client LWM2M per creare una nuova istanza dell'oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_id:** ID oggetto.
- **instance_id_ptr**: puntatore all'ID della nuova istanza, può essere NULL se il client LWM2M deve assegnare un ID istanza. Se l'ID è il valore riservato 65535, il client LWM2M assegna un ID istanza. Se non è NULL, l'ID assegnato viene restituito dopo la chiamata.
- **num_values**: numero di valori da impostare.
- **values_ptr**: puntatore a una matrice di valori di risorsa per inizializzare la nuova istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_ALREADY_EXIST**: l'ID istanza dell'oggetto esiste già.
- **NX_LWM2M_METHOD_NOT_ALLOWED:** l'oggetto non supporta la creazione di istanze.
- **NX_LWM2M_NO_MEMORY**: impossibile allocare memoria per archiviare la nuova istanza.
- **NX_LWM2M_NOT_FOUND:** l'ID oggetto non esiste.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_delete"></a>nx_lwm2m_client_object_delete

Eliminare un'istanza dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_delete(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di eliminazione su un'istanza di oggetto del client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_id:** ID oggetto.
- **instance_id**: ID dell'istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_METHOD_NOT_ALLOWED:** l'oggetto non supporta l'eliminazione dell'istanza.
- **NX_LWM2M_NOT_FOUND**: l'ID oggetto o l'ID istanza dell'oggetto non esiste.
- NX_PTR_ERROR puntatore non valido.

## <a name="nx_lwm2m_client_object_discover"></a>nx_lwm2m_client_object_discover

Individuare le risorse di un'istanza dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_discover(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT *num_resources_ptr, NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione "Discover" su un'istanza di oggetto del client LWM2M. Viene restituito l'elenco delle risorse implementate dall'oggetto .

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_id:** ID oggetto.
- **instance_id**: ID dell'istanza dell'oggetto.
- **num_resources_ptr:** all'input la dimensione del buffer di destinazione, nell'output viene restituito il numero di elementi scritto nel buffer.
- **resources_ptr**: puntatore al buffer di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BUFFER_TOO_SMALL:** il buffer delle risorse è troppo piccolo per archiviare l'elenco delle risorse.
- **NX_LWM2M_NOT_FOUND**: l'ID oggetto o l'ID istanza dell'oggetto non esiste.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_execute"></a>nx_lwm2m_client_object_execute

Eseguire una risorsa di un'istanza dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_execute(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr, UINT arguments_length);
```

### <a name="description"></a>Descrizione

Questo servizio esegue l'operazione 'Execute' su una risorsa dell'istanza dell'oggetto del client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_id:** ID oggetto.
- **instance_id**: ID dell'istanza dell'oggetto.
- **resource_id**: ID risorsa.
- **arguments_ptr**: puntatore agli argomenti dell'operazione di esecuzione. Può essere NULL se arguments_length è zero.
- **arguments_length**: lunghezza degli argomenti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: la risorsa non supporta l'operazione di esecuzione.
- **NX_LWM2M_NOT_FOUND:** l'ID oggetto, l'ID istanza dell'oggetto o l'ID risorsa non esiste.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_get_next"></a>nx_lwm2m_client_object_get_next

Ottenere l'elenco degli oggetti implementati dal client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_get_next(NX_LWM2M_CLIENT *client_ptr,
                                    NX_LWM2M_ID *object_id_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'ID dell'oggetto successivo implementato dal client LWM2M. Se l'ID oggetto corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito il primo ID oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_id_ptr**: puntatore all'ID oggetto corrente. In fase di restituzione contiene l'ID oggetto successivo implementato dal client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_NOT_FOUND**: l'ID oggetto specificato è l'ultimo del database.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_instance_get_next"></a>nx_lwm2m_client_object_instance_get_next

Ottenere l'elenco di istanze di un oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_instance_get_next(NX_LWM2M_CLIENT *client_ptr,
                    NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'ID dell'istanza dell'oggetto successiva dell'oggetto specificato. Se l'ID istanza corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito l'ID della prima istanza.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_id:** ID oggetto.
- **instance_id_ptr**: puntatore all'ID istanza dell'oggetto corrente. In fase di restituzione contiene l'ID istanza successivo dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_NOT_FOUND**: l'ID istanza specificato è l'ultimo dell'oggetto o l'ID oggetto non è implementato.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_read"></a>nx_lwm2m_client_object_read

Leggere i valori delle risorse di un'istanza dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_read(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT num_values, NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di lettura su un'istanza di oggetto del client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_id:** ID oggetto.
- **instance_id**: ID dell'istanza dell'oggetto.
- **num_values:** numero di risorse da leggere.
- **values_ptr**: puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse da leggere. Al ritorno, la matrice viene riempita con i tipi e i valori corrispondenti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_METHOD_NOT_ALLOWED:** una risorsa non supporta l'operazione di lettura.
- **NX_LWM2M_NOT_FOUND:** l'ID oggetto, l'ID istanza dell'oggetto o un ID risorsa non esiste.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_write"></a>nx_lwm2m_client_object_write

Modificare i valori delle risorse di un'istanza dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_write(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, UINT num_values,
        const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di scrittura su un'istanza di oggetto del client LWM2M.

Le operazioni di scrittura seguenti possono essere specificate nel *write_op* seguente:

- **0** &mdash; Aggiornamento parziale: aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate le altre risorse esistenti.

- **NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Sostituisci istanza: sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa forniti.

- **NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Sostituisci risorsa: sostituisce le risorse con i nuovi valori delle risorse forniti (usati per sostituire più risorse).

- **NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Scrittura bootstrap: indica una chiamata da una sequenza bootstrap.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **object_id:** ID oggetto.
- **instance_id**: ID dell'istanza dell'oggetto.
- **num_values**: numero di risorse da scrivere.
- **values_ptr**: puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse, i tipi e i valori da scrivere.
- **write_op:** tipo di operazione di scrittura.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING:** il tipo di una risorsa non è valido.
- **NX_LWM2M_BUFFER_TOO_SMALL:** la lunghezza di un valore è troppo grande per essere archiviata nell'istanza di .
- **NX_LWM2M_METHOD_NOT_ALLOWED:** una risorsa non supporta l'operazione di scrittura.
- **NX_LWM2M_NO_MEMORY:** impossibile allocare memoria per archiviare un valore di risorsa.
- **NX_LWM2M_NOT_ACCEPTABLE:** il valore di una risorsa non è valido.
- **NX_LWM2M_NOT_FOUND:** l'ID oggetto, l'ID istanza dell'oggetto o un ID risorsa non esiste.
- NX_OPTION_ERROR: tipo di operazione di scrittura non valido.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_security_key_callbacks_set"></a>nx_lwm2m_client_security_key_callbacks_set

Impostare i callback di gestione delle chiavi degli oggetti di sicurezza

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_security_key_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_CLIENT_SECURITY_KEY_WRITE_CALLBACK write_callback,
                NX_LWM2M_CLIENT_SECURITY_KEY_DELETE_CALLBACK delete_callback);
```

### <a name="description"></a>Descrizione

Questo servizio installa i callback dell'applicazione per l'implementazione di operazioni sulle risorse dell'oggetto di sicurezza LWM2M correlate alle chiavi di sicurezza.

Il client LWM2M delega la gestione delle chiavi di sicurezza all'applicazione durante le sessioni bootstrap. I callback verranno chiamati quando il server Bootstrap scrive o elimina le risorse seguenti in un'istanza dell'oggetto di sicurezza: chiave pubblica o identità (3), chiave pubblica del server (4), chiave privata (5).

L'applicazione è responsabile dell'archiviazione dei dati delle chiavi e della configurazione delle sessioni DTLS usate dal client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.
- **write_callback:** callback del metodo chiave 'Write'.
- **delete_callback:** callback del metodo chiave 'Delete'.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_bootstrap"></a>nx_lwm2m_client_session_bootstrap

Avviare una sessione con un server Bootstrap

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_bootstrap(NX_LWM2M_CLIENT_SESSION
    *session_ptr, NX_LWM2M_ID security_id, ULONG ip_address, UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione con un server Bootstrap. Il server deve avere un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.

Se la risorsa 'Hold Off' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà un bootstrap avviato dal server, se non viene avviato alcun bootstrap dal server dopo questo periodo di tempo verrà eseguito un boostrap avviato dal client.

Qualsiasi sessione attiva corrente viene interrotta da questa chiamata e sostituita dalla nuova sessione del server Bootstrap.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.
- **security_id:** l'ID dell'istanza di sicurezza del server Bootstrap deve essere impostato su NX_LWM2M_RESERVED_ID (65535) se nel server Bootstrap non è definita alcuna istanza di sicurezza.
- **ip_address**: indirizzo IP del server.
- **port**: porta UDP del server.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_NOT_FOUND:** non è presente alcuna istanza dell'oggetto di sicurezza corrispondente all'ID dell'istanza di sicurezza.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a>nx_lwm2m_client_session_bootstrap_dtls

Avviare una sessione protetta con un server Bootstrap

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID security_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione con un server Bootstrap usando una connessione DTLS sicura. Il server deve avere un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.

Prima di chiamare questa funzione, la sessione DTLS deve essere stata configurata con i pacchetti di crittografia e il materiale della chiave appropriato. NX_SECURE_ENABLE_DTLS deve essere definito.

Se la risorsa 'Hold Off' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà un bootstrap avviato dal server, se non viene avviato alcun bootstrap dal server dopo questo periodo di tempo verrà eseguito un boostrap avviato dal client.

Qualsiasi sessione attiva corrente viene interrotta da questa chiamata e sostituita dalla nuova sessione del server Bootstrap.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.
- **security_id:** l'ID dell'istanza di sicurezza del server Bootstrap deve essere impostato su NX_LWM2M_RESERVED_ID (65535) se nel server Bootstrap non è definita alcuna istanza di sicurezza.
- **ip_address**: indirizzo IP del server.
- **port**: porta UDP del server.
- **dtls_session_ptr:** sessione DTLS da usare per la sessione bootstrap.
- **dtls_local_port**: porta UDP locale usata per la sessione DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_NOT_FOUND:** non è presente alcuna istanza dell'oggetto di sicurezza corrispondente all'ID dell'istanza di sicurezza.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_create"></a>nx_lwm2m_client_session_create

Creare una sessione client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_create(NX_LWM2M_CLIENT_SESSION *session_ptr,
         NX_LWM2M_CLIENT *client_ptr,
         NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK state_callback);
```

### <a name="description"></a>Descrizione

Questo servizio crea una nuova sessione client LWM2M collegata a un client LWM2M esistente. La sessione viene usata dal client LWM2M per comunicare con un server Bootstrap o un server LWM2M.

L'applicazione deve fornire una funzione di callback che verrà chiamata quando lo stato della sessione viene aggiornato.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.
- **client_ptr:** puntatore al client LWM2M creato in precedenza.
- **state_callback:** callback dell'applicazione che viene chiamato quando lo stato della sessione è stato modificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_delete"></a>nx_lwm2m_client_session_delete

Eliminare la sessione client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina una sessione client LWM2M.

Quando un client LWM2M viene eliminato chiamando nx_lwm2m_client_delete vengono eliminate anche tutte le sessioni collegate al client.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_deregister"></a>nx_lwm2m_client_session_deregister

Terminare una sessione con un server LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di deregistrazione in un server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_NOT_REGISTERED**: il client non è registrato nel server.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_error_get"></a>nx_lwm2m_client_session_error_get

Ottenere l'ultimo errore di una sessione

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il codice di errore della sessione quando la sessione si trova in uno stato di errore.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** la sessione non è in stato di errore.
- **NX_LWM2M_ADDRESS_ERROR:** indirizzo del server non valido.
- **NX_LWM2M_BUFFER_TOO_SMALL:** il payload della richiesta non rientra nel buffer di rete.
- **NX_LWM2M_DTLS_ERROR:** impossibile stabilire una connessione protetta con il server.
- **NX_LWM2M_ERROR:** errore non specificato.
- **NX_LWM2M_FORBIDDEN:** registrazione rifiutata dal server.
- **NX_LWM2M_NOT_FOUND:** client non trovato dal server durante l'aggiornamento/annullamento della registrazione.
- **NX_LWM2M_SERVER_INSTANCE_DELETED:** l'istanza dell'oggetto server corrispondente alla sessione è stata eliminata.
- **NX_LWM2M_TIMED_OUT:** nessuna risposta dal server.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_register"></a>nx_lwm2m_client_session_register

Avviare una sessione con un server LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_register(NX_LWM2M_CLIENT_SESSION *session_ptr,
                    NX_LWM2M_ID server_id, ULONG ip_address, UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione 'Register' in un server LWM2M. Il server deve avere un'istanza del server corrispondente nell'oggetto server.

Se la registrazione ha esito positivo, il client LWM2M e processerà ulteriori operazioni dal server e invierà periodicamente messaggi "Update" fino a quando il client non viene de-registrato.

Qualsiasi sessione attiva corrente viene interrotta da questa chiamata e sostituita dalla nuova sessione del server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.
- **server_id**: ID server breve del server LWM2M.
- **ip_address**: indirizzo IP del server.
- **port**: porta UDP del server.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_NOT_FOUND:** non è presente alcuna istanza dell'oggetto server corrispondente all'ID server breve.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_register_dtls"></a>nx_lwm2m_client_session_register_dtls

Avviare una sessione protetta con un server LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_register_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID server_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione 'Register' in un server LWM2M usando una connessione DTLS sicura. Il server deve avere un'istanza del server corrispondente nell'oggetto server.

Prima di chiamare questa funzione, la sessione DTLS deve essere stata configurata con i pacchetti di crittografia e il materiale della chiave appropriato. NX_SECURE_ENABLE_DTLS deve essere definito.

Ogni sessione DTLS usa il proprio socket UDP per la comunicazione, pertanto la porta dtls_local_port deve essere diversa per ogni sessione se l'applicazione crea diverse sessioni protette.

Se la registrazione ha esito positivo, il client LWM2M e processerà ulteriori operazioni dal server e invierà periodicamente messaggi "Update" fino a quando il client non viene de-registrato.

Qualsiasi sessione attiva corrente viene interrotta da questa chiamata e sostituita dalla nuova sessione del server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.
- **server_id**: ID server breve del server LWM2M.
- **ip_address**: indirizzo IP del server.
- **port**: porta UDP del server.
- **dtls_session_ptr:** sessione DTLS da usare per la sessione LWM2M.
- **dtls_local_port**: porta UDP locale usata per la sessione DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_NOT_FOUND:** non è presente alcuna istanza dell'oggetto server corrispondente all'ID server breve.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_update"></a>nx_lwm2m_client_session_update

Aggiornare una sessione con un server LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di aggiornamento in un server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr:** puntatore al blocco di controllo sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_NOT_REGISTERED**: il client non è registrato nel server.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_unlock"></a>nx_lwm2m_client_unlock

Sbloccare il client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio sblocca la previoulsy del client LWM2M bloccata da una chiamata a nx_lwm2m_client_unlock().

### <a name="parameters"></a>Parametri

- **client_ptr:** puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_firmware_create"></a>nx_lwm2m_firmware_create

Creare un oggetto di aggiornamento del firmware

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_firmware_create(NX_LWM2M_FIRMWARE *firmware_ptr,
    NX_LWM2M_CLIENT *client_ptr, UINT protocols,
    NX_LWM2M_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_FIRMWARE_UPDATE_CALLBACK update_callback);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza un oggetto di aggiornamento del firmware e aggiunge l'oggetto a un client LWM2M creato in precedenza. L'oggetto di aggiornamento del firmware implementa le risorse per la comunicazione con un server LWM2M, ma l'applicazione deve fornire callback per l'implementazione delle operazioni effettive sul firmware (dowload, archiviazione e aggiornamento del firmware).

Il parametro protocols indica quali protocolli sono supportati dall'applicazione per il recupero del firmware con la risorsa "URI pacchetto". Vengono definiti i flag seguenti:

NX_LWM2M_FIRMWARE_PROTOCOL_COAP, NX_LWM2M_FIRMWARE_PROTOCOL_COAPS, NX_LWM2M_FIRMWARE_PROTOCOL_HTTP, NX_LWM2M_FIRMWARE_PROTOCOL_HTPPS.

### <a name="parameters"></a>Parametri

- **firmware_ptr:** puntatore al blocco di controllo Firmware Object.
- **client_ptr:** puntatore al client LWM2M creato in modo previso.
- **protocols:** flag che indicano i protocolli supportati dalla risorsa URI del pacchetto.
- **package_callback:** deve essere NULL [TBD].
- **package_uri_callback:** callback usato per implementare la risorsa URI del pacchetto.
- **update_callback:** callback usato per implementare la risorsa Update.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_firmware_package_info_set"></a>nx_lwm2m_firmware_package_info_set

Impostare le informazioni sul pacchetto di aggiornamento del firmware

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_firmware_package_info_set(NX_LWM2M_FIRMWARE *firmware_ptr,
                                const CHAR *name, const CHAR *version);
```

### <a name="description"></a>Descrizione

Questo servizio modifica i valori delle risorse 'PkgName' (6) e 'PkgVersion' (7) dell'oggetto di aggiornamento del firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr:** puntatore all'oggetto di aggiornamento del firmware.
- **name**: nuovo valore di Nome pacchetto.
- **version:** nuovo valore della versione del pacchetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_firmware_result_set"></a>nx_lwm2m_firmware_result_set

Impostare il risultato dell'aggiornamento del firmware

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_firmware_result_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR result);
```

### <a name="description"></a>Descrizione

Questo servizio modifica il valore della risorsa "Risultato aggiornamento" (5) dell'oggetto di aggiornamento del firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr**: puntatore all'oggetto di aggiornamento del firmware.
- **result:** nuovo valore della risorsa Risultato aggiornamento.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_firmware_state_set"></a>nx_lwm2m_firmware_state_set

Impostare lo stato di aggiornamento del firmware

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_firmware_state_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR state);
```

### <a name="description"></a>Descrizione

Questo servizio modifica il valore della risorsa 'State' (3) dell'oggetto di aggiornamento del firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr**: puntatore all'oggetto di aggiornamento del firmware.
- **state:** nuovo valore della risorsa State.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_object_resource_changed"></a>nx_lwm2m_object_resource_changed

Segnalare la modifica di un valore di risorsa di un'istanza di oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_object_resource_changed(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato da un'implementazione object per segnala al client LWM2M che uno dei relativi valori di risorsa è stato modificato. Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.

### <a name="parameters"></a>Parametri

- **object_ptr:** puntatore all'implementazione dell'oggetto.
- **instance_ptr**: puntatore all'istanza dell'oggetto.
- **resource:** puntatore alla struttura che descrive la risorsa modificata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_resource_get_boolean"></a>nx_lwm2m_resource_get_boolean

Ottenere il valore di una risorsa booleana

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_boolean(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa booleana.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore della risorsa.
- **bool_ptr:** puntatore al valore booleano di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore booleano.

## <a name="nx_lwm2m_resource_get_float32"></a>nx_lwm2m_resource_get_float32

Ottenere il valore di una risorsa a virgola mobile a 32 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_float32(const NX_LWM2M_RESOURCE *value,
                                NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa a virgola mobile a 32 bit.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore della risorsa.
- **float32_ptr:** puntatore al valore a virgola mobile a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore a virgola mobile.

## <a name="nx_lwm2m_resource_get_float64"></a>nx_lwm2m_resource_get_float64

Ottenere il valore di una risorsa a virgola mobile a 64 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_float64(const NX_LWM2M_RESOURCE *value,
                                NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa a virgola mobile a 64 bit.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore della risorsa.
- **float64_ptr**: puntatore al valore a virgola mobile a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore a virgola mobile.

## <a name="nx_lwm2m_resource_get_integer32"></a>nx_lwm2m_resource_get_integer32

Ottenere il valore di una risorsa integer a 32 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_integer32(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa integer a 32 bit.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore della risorsa.
- **int32_ptr:** puntatore al valore Integer a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING:** il valore della risorsa non è un valore Integer o il valore Integer non rientra in un numero a 32 bit.

## <a name="nx_lwm2m_resource_get_integer64"></a>nx_lwm2m_resource_get_integer64

Ottenere il valore di una risorsa integer a 64 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_integer64(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa integer a 64 bit.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore della risorsa.
- **int64_ptr**: puntatore al valore Integer a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore Integer.

## <a name="nx_lwm2m_resource_get_objlnk"></a>nx_lwm2m_resource_get_objlnk

Ottenere il valore di una risorsa collegamento a oggetti

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_objlnk(const NX_LWM2M_RESOURCE *value,
                                    NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa collegamento a oggetti.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore della risorsa.
- **objlnk_ptr:** puntatore al valore di Object Link di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING:** il valore della risorsa non è un valore di Collegamento oggetto.

## <a name="nx_lwm2m_resource_get_opaque"></a>nx_lwm2m_resource_get_opaque

Ottenere il valore di una risorsa opaca

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_opaque(const NX_LWM2M_RESOURCE *value,
            const VOID **opaque_ptr_ptr, UINT *opaque_length_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa opaca.

Un valore di risorsa opaco è costituito da un puntatore a un buffer e da una lunghezza.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore della risorsa.
- **opaque_ptr_ptr:** puntatore al puntatore al buffer opaco di destinazione.
- **opaque_length_ptr:** puntatore alla lunghezza del buffer opaco di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING:** il valore della risorsa non è un valore Opaco.

## <a name="nx_lwm2m_resource_get_string"></a>nx_lwm2m_resource_get_string

Ottenere il valore di una risorsa stringa

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_string(const NX_LWM2M_RESOURCE *value,
            const CHAR **string_ptr_ptr, UINT *string_length_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa stringa.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore della risorsa.
- **string_ptr_ptr:** puntatore al puntatore alla stringa di destinazione.
- **string_length_ptr:** puntatore alla lunghezza della stringa di destinazione. Può essere NULL se la stringa ha terminazione Null.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_ENCODING:** il valore della risorsa non è un valore String.

## <a name="nx_lwm2m_resource_multiple_get_boolean"></a>nx_lwm2m_resource_multiple_get_boolean

Ottenere il valore di un'istanza booleana di più risorse di risorse

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_boolean(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa booleana da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore di più risorse.
- **index**: indice dell'istanza di da recuperare nella matrice di valori resource.
- **instance_id_ptr:** puntatore all'ID istanza di destinazione.
- **bool_ptr:** puntatore al valore booleano di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER:** l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING:** la risorsa non è una risorsa multipla o il valore della risorsa non è un valore booleano.

## <a name="nx_lwm2m_resource_multiple_get_float32"></a>nx_lwm2m_resource_multiple_get_float32

Ottenere il valore di un'istanza di più risorse a virgola mobile a 32 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_float32(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa a virgola mobile a 32 bit da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore di più risorse.
- **index**: indice dell'istanza di da recuperare nella matrice di valori resource.
- **instance_id_ptr:** puntatore all'ID istanza di destinazione.
- **float32_ptr:** puntatore al valore a virgola mobile a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER:** l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING:** la risorsa non è una risorsa multipla o il valore della risorsa non è un valore a virgola mobile.

## <a name="nx_lwm2m_resource_multiple_get_float64"></a>nx_lwm2m_resource_multiple_get_float64

Ottenere il valore di un'istanza di più risorse a virgola mobile a 64 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_float64(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa a virgola mobile a 64 bit da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore di più risorse.
- **index**: indice dell'istanza di da recuperare nella matrice di valori resource.
- **instance_id_ptr:** puntatore all'ID istanza di destinazione.
- **float64_ptr:** puntatore al valore a virgola mobile a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER:** l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING:** la risorsa non è una risorsa multipla o il valore della risorsa non è un valore a virgola mobile.

## <a name="nx_lwm2m_resource_multiple_get_integer32"></a>nx_lwm2m_resource_multiple_get_integer32

Ottenere il valore di un'istanza di più risorse integer a 32 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_integer32(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa integer a 32 bit da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore di più risorse.
- **index**: indice dell'istanza di da recuperare nella matrice di valori resource.
- **instance_id_ptr:** puntatore all'ID istanza di destinazione.
- **int32_ptr:** puntatore al valore Integer a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER:** l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla o il valore della risorsa non è un valore Integer oppure il valore Integer non rientra in un numero a 32 bit.

## <a name="nx_lwm2m_resource_multiple_get_integer64"></a>nx_lwm2m_resource_multiple_get_integer64

Ottenere il valore di un'istanza di più risorse integer a 64 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_integer64(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa integer a 64 bit da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore di più risorse.
- **index**: indice dell'istanza di da recuperare nella matrice di valori resource.
- **instance_id_ptr:** puntatore all'ID istanza di destinazione.
- **int64_ptr:** puntatore al valore Integer a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER:** l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING:** la risorsa non è una risorsa multipla o il valore della risorsa non è un valore Integer.

## <a name="nx_lwm2m_resource_multiple_get_objlnk"></a>nx_lwm2m_resource_multiple_get_objlnk

Ottenere il valore di un'istanza di più risorse di Collegamento oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_objlnk(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa Collegamento oggetto da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore di più risorse.
- **index:** indice dell'istanza di da recuperare nella matrice di valori resource.
- **instance_id_ptr**: puntatore all'ID istanza di destinazione.
- **objlnk_ptr**: puntatore al valore di Object Link di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER:** l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING:** la risorsa non è una risorsa multipla o il valore della risorsa non è un valore di Collegamento oggetto.

## <a name="nx_lwm2m_resource_multiple_get_opaque"></a>nx_lwm2m_resource_multiple_get_opaque

Ottenere il valore di un'istanza di più risorse opaca

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_opaque(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const VOID **opaque_ptr_ptr,
    UINT *opaque_length_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa opaca da più risorse.

Un valore di risorsa opaco è costituito da un puntatore a un buffer e da una lunghezza.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore di più risorse.
- **index:** indice dell'istanza di da recuperare nella matrice di valori resource.
- **instance_id_ptr**: puntatore all'ID istanza di destinazione.
- **opaque_ptr_ptr:** puntatore al puntatore al buffer opaco di destinazione.
- **opaque_length_ptr:** puntatore alla lunghezza del buffer opaco di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER:** l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING:** la risorsa non è una risorsa multipla o il valore della risorsa non è un valore Opaco.

## <a name="nx_lwm2m_resource_multiple_get_string"></a>nx_lwm2m_resource_multiple_get_string

Ottenere il valore di un'istanza di più risorse stringa

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_string(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const CHAR **string_ptr_ptr,
    UINT *string_length_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa stringa da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value:** puntatore alla descrizione del valore di più risorse.
- **index:** indice dell'istanza di da recuperare nella matrice di valori resource.
- **instance_id_ptr**: puntatore all'ID istanza di destinazione.
- **string_ptr_ptr:** puntatore al puntatore della stringa di destinazione.
- **string_length_ptr**: puntatore alla lunghezza della stringa di destinazione. Può essere NULL se la stringa ha terminazione Null.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER:** l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla o il valore dell'istanza non è un valore String.
