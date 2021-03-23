---
title: Capitolo 4-Descrizione dei servizi LWM2M NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi LWM2M di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d5a402790387c2720db304fe93d74252494d7638
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822577"
---
# <a name="chapter-4---description-of-azure-rtos-netx-lwm2m-services"></a>Capitolo 4-Descrizione dei servizi LWM2M NetX di Azure RTO

Questo capitolo contiene una descrizione di tutti i servizi LWM2M di Azure RTO NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

### <a name="lwm2m-client-management"></a>Gestione client LWM2M

- **nx_lwm2m_client_create**: *creare un client lwm2m*
- **nx_lwm2m_client_delete**: *eliminare il client lwm2m*
- **nx_lwm2m_client_lock**: *bloccare il client lwm2m*
- **nx_lwm2m_client_object_add**: *aggiungere l'implementazione dell'oggetto al client lwm2m*
- **nx_lwm2m_client_unlock**: *sbloccare il client lwm2m*

### <a name="lwm2m-client-session-management"></a>Gestione delle sessioni client di LWM2M

- **nx_lwm2m_client_session_bootstrap**: *avviare una sessione con un server bootstrap*
- **nx_lwm2m_client_session_bootstrap_dtls**: *avviare una sessione protetta con un server bootstrap*
- **nx_lwm2m_client_session_create**: *creare una sessione client lwm2m*
- **nx_lwm2m_client_session_delete**: *eliminare la sessione del client lwm2m*
- **nx_lwm2m_client_session_deregister**: *terminare una sessione con un server lwm2m*
- **nx_lwm2m_client_session_error_get**: *ottenere l'ultimo errore di una sessione*
- **nx_lwm2m_client_session_register**: *avviare una sessione con un server lwm2m*
- **nx_lwm2m_client_session_register_dtls**: *avviare una sessione protetta con un server lwm2m*
- **nx_lwm2m_client_session_update**: *aggiornare una sessione con un server lwm2m*

### <a name="security-object-implementation"></a>Implementazione di oggetti di sicurezza

- **nx_lwm2m_client_security_key_callbacks_set**: *impostare i callback di gestione delle chiavi di sicurezza*

### <a name="device-object-implementation"></a>Implementazione di oggetti dispositivo

- **nx_lwm2m_client_device_callbacks_set**: *impostare i callback dell'applicazione oggetto dispositivo*
- **nx_lwm2m_client_device_error_push**: *aggiungere il codice di errore all'oggetto dispositivo*
- **nx_lwm2m_client_device_error_reset**: *Reimposta i codici di errore dell'oggetto dispositivo*
- **nx_lwm2m_client_device_resource_changed**: *modifica del segnale della risorsa oggetto dispositivo*

### <a name="custom-objects-implementation"></a>Implementazione di oggetti personalizzati

- **nx_lwm2m_object_resource_changed**: *modifica del segnale di un valore di risorsa di un'istanza dell'oggetto*

### <a name="local-device-management"></a>Gestione dei dispositivi locali

- **nx_lwm2m_client_object_create**: *creare una nuova istanza dell'oggetto*
- **nx_lwm2m_client_object_delete**: *eliminare un'istanza dell'oggetto*
- **nx_lwm2m_client_object_discover**: *individuazione delle risorse di un'istanza dell'oggetto*
- **nx_lwm2m_client_object_execute**: *eseguire la risorsa di un'istanza dell'oggetto*
- **nx_lwm2m_client_object_get_next**: *Ottiene l'elenco di oggetti implementati dal client lwm2m*
- **nx_lwm2m_client_object_instance_get_next**: *Ottiene l'elenco di istanze di un oggetto*
- **nx_lwm2m_client_object_read**: *leggere i valori delle risorse di un'istanza dell'oggetto*
- **nx_lwm2m_client_object_write**: *modificare i valori delle risorse di un'istanza dell'oggetto*

### <a name="resources-values-decoding"></a>Decodifica dei valori delle risorse

- **nx_lwm2m_resource_get_boolean**: *recuperare il valore di una risorsa booleana*
- **nx_lwm2m_resource_get_float32**: *ottiene il valore di una risorsa a virgola mobile a 32 bit*
- **nx_lwm2m_resource_get_float64**: *ottiene il valore di una risorsa a virgola mobile a 64 bit*
- **nx_lwm2m_resource_get_integer32**: *recuperare il valore di una risorsa Integer a 32 bit*
- **nx_lwm2m_resource_get_integer64**: *recuperare il valore di una risorsa Integer a 64 bit*
- **nx_lwm2m_resource_get_objlnk**: *recuperare il valore di una risorsa di collegamento a un oggetto*
- **nx_lwm2m_resource_get_opaque**: *recuperare il valore di una risorsa opaca*
- **nx_lwm2m_resource_get_string**: *recuperare il valore di una risorsa di stringa*
- **nx_lwm2m_resource_multiple_get_boolean**: *recuperare il valore di una risorsa booleana per più istanze di risorse*
- **nx_lwm2m_resource_multiple_get_float32**: *ottiene il valore di un'istanza a virgola mobile a virgola mobile a 32 bit*
- **nx_lwm2m_resource_multiple_get_float64**: *ottiene il valore di un'istanza a virgola mobile a virgola mobile a 64 bit*
- **nx_lwm2m_resource_multiple_get_integer32**: *ottiene il valore di un'istanza di risorsa Integer a 32 bit*
- **nx_lwm2m_resource_multiple_get_integer64**: *ottiene il valore di un'istanza di risorsa Integer a 64 bit*
- **nx_lwm2m_resource_multiple_get_objlnk**: *recuperare il valore di un oggetto collegamento a più istanze di risorse*
- **nx_lwm2m_resource_multiple_get_opaque**: *ottiene il valore di un'istanza di più risorse opaca*
- **nx_lwm2m_resource_multiple_get_string**: *recuperare il valore di una stringa con più istanze di risorse*

### <a name="firmware-update-object"></a>Oggetto di aggiornamento del firmware

- **nx_lwm2m_firmware_create**: *creare un oggetto di aggiornamento del firmware*
- **nx_lwm2m_firmware_package_info_set**: *impostare le informazioni sul pacchetto di aggiornamento del firmware*
- **nx_lwm2m_firmware_result_set**: *impostare il risultato dell'aggiornamento del firmware*
- **nx_lwm2m_firmware_state_set**: *impostare lo stato di aggiornamento del firmware*

## <a name="nx_lwm2m_client_create"></a>nx_lwm2m_client_create

Crea client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_create(NX_LWM2M_CLIENT *client_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr, UINT local_port, const CHAR *name_ptr,
    const CHAR *msisdn_ptr, UCHAR binding_modes, VOID *stack_ptr, ULONG stack_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client LWM2M, che viene eseguita nel contesto del proprio thread ThreadX.

Il client LWM2M implementa i seguenti oggetti LWM2M OMA: Security (0), server (1), controllo di accesso (2) e Device (3). Le altre implementazioni di oggetti devono essere aggiunte dall'applicazione.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **ip_ptr**: puntatore all'istanza IP creata in precedenza.
- **packet_pool_ptr**: puntatore al pool di pacchetti predefinito per il client LWM2M.
- **local_port**: porta UDP locale utilizzata per la comunicazione non protetta.
- **name_ptr**: puntatore al nome dell'endpoint del client LWM2M.
- **msisdn_ptr**: puntatore a MSISDN in cui è possibile raggiungere il client LWM2M per l'utilizzo con l'associazione SMS, può essere null se l'associazione SMS non è supportata.
- **binding_modes**: l'associazione e le modalità supportate dal client LWM2M devono essere una combinazione di flag NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S e NX_LWM2M_BINDING_SQ.
- **stack_ptr**: puntatore all'area dello stack di thread del client LWM2M.
- **stack_size**: dimensioni dello stack dei thread del client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: il client LWM2M è stato creato correttamente.
- **NX_LWM2M_ERROR**: errore di creazione del client LWM2M.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_delete"></a>nx_lwm2m_client_delete

Elimina client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del client LWM2M creata in precedenza.

Tutte le sessioni attualmente associate al client vengono eliminate anche da questa chiamata.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: il client LWM2M è stato eliminato correttamente.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_device_callbacks_set"></a>nx_lwm2m_client_device_callbacks_set

Imposta callback applicazione oggetto dispositivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_READ_CALLBACK read_callback,
    NX_LWM2M_CLIENT_DEVICE_DISCOVER_CALLBACK discover_callback,
    NX_LWM2M_CLIENT_DEVICE_WRITE_CALLBACK write_callback,
    NX_LWM2M_CLIENT_DEVICE_EXECUTE_CALLBACK execute_callback);
```

### <a name="description"></a>Descrizione

Questo servizio installa i callback dell'applicazione per l'implementazione di operazioni sulle risorse dell'oggetto dispositivo LWM2M che non sono gestite dal client LWM2M.

Il client LWM2M implementa le risorse seguenti: codice errore (11), Reimposta codice errore (12), binding supportato e modalità (16), le operazioni per le altre risorse vengono reindirizzate all'applicazione.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **Read_Callback**: callback del metodo ' Read '.
- **discover_callback**: callback del metodo ' Discover '.
- **write_callback**: callback del metodo ' Write '.
- **execute_callback**: callback del metodo ' Execute '.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_device_error_push"></a>nx_lwm2m_client_device_error_push

Aggiungere il codice di errore all'oggetto dispositivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_error_push(NX_LWM2M_CLIENT *client_ptr, UCHAR code);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una nuova istanza alla risorsa del codice di errore (11) del dispositivo dell'oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **Code**: nuovo codice di errore.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BUFFER_TOO_SMALL**: è stato raggiunto il numero massimo di codici di errore archiviati.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_device_error_reset"></a>nx_lwm2m_client_device_error_reset

Reimposta i codici di errore dell'oggetto dispositivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina tutte le istanze di risorse del codice di errore dall'oggetto dispositivo. Equivale a eseguire il codice di errore di reimpostazione della risorsa (12).

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_device_resource_changed"></a>nx_lwm2m_client_device_resource_changed

Modifica del segnale della risorsa oggetto dispositivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_device_resource_changed(NX_LWM2M_CLIENT *client_ptr,
                                    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Descrizione

Il servizio viene usato dall'applicazione per segnalare al client LWM2M che una risorsa del dispositivo oggetto è cambiata. Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **Resource**: puntatore alla struttura che descrive la risorsa che è stata modificata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_lock"></a>nx_lwm2m_client_lock

Blocca client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_lock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio blocca il client LWM2M per impedire l'accesso concurent agli oggetti LWM2M dai server o da un altro thread dell'applicazione.

Se il client LWM2M è attualmente bloccato da un altro thread, la funzione si bloccherà fino a quando non viene sbloccato il client LWM2M.

È possibile nidificare le chiamate alle coppie nx_lwm2m_client_lock ()/nx_lwm2m_client_unlock ().

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_add"></a>nx_lwm2m_client_object_add

Aggiungere l'implementazione dell'oggetto al client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_add(NX_LWM2M_CLIENT *client_ptr,
                                NX_LWM2M_OBJECT *object_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una nuova implementazione dell'oggetto al client di LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_ptr**: puntatore alla struttura che definisce l'implementazione dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_ALREADY_EXIST**: l'ID oggetto esiste già.
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

Questo servizio esegue un'operazione di creazione su un oggetto del client LWM2M per creare una nuova istanza dell'oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_id**: ID oggetto.
- **instance_id_ptr**: puntatore all'ID della nuova istanza, può essere null se il client LWM2M deve assegnare un ID istanza. Se l'ID è il valore riservato 65535, il client LWM2M assegnerà un ID istanza. Se non è NULL, l'ID assegnato viene restituito dopo la chiamata.
- **num_values**: numero di valori da impostare.
- **values_ptr**: puntatore a una matrice di valori di risorsa per inizializzare la nuova istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_ALREADY_EXIST**: l'ID dell'istanza dell'oggetto esiste già.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: l'oggetto non supporta la creazione di istanze.
- **NX_LWM2M_NO_MEMORY**: non è possibile allocare memoria per archiviare la nuova istanza.
- **NX_LWM2M_NOT_FOUND**: l'ID oggetto non esiste.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_delete"></a>nx_lwm2m_client_object_delete

Eliminare un'istanza di oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_delete(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di eliminazione su un'istanza di oggetto del client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_id**: ID oggetto.
- **Instance_Id**: ID dell'istanza dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: l'oggetto non supporta l'eliminazione dell'istanza.
- **NX_LWM2M_NOT_FOUND**: l'ID oggetto o l'ID istanza oggetto non esiste.
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

Questo servizio esegue un'operazione di individuazione su un'istanza dell'oggetto del client LWM2M, restituisce l'elenco delle risorse implementate dall'oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_id**: ID oggetto.
- **Instance_Id**: ID dell'istanza dell'oggetto.
- **num_resources_ptr**: in input la dimensione del buffer di destinazione, in output il numero di elementi scritti nel buffer.
- **resources_ptr**: puntatore al buffer di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita..
- **NX_LWM2M_BUFFER_TOO_SMALL**: il buffer di risorse è troppo piccolo per archiviare l'elenco di risorse.
- **NX_LWM2M_NOT_FOUND**: l'ID oggetto o l'ID istanza oggetto non esiste.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_execute"></a>nx_lwm2m_client_object_execute

Esegui risorsa di un'istanza dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_execute(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr, UINT arguments_length);
```

### <a name="description"></a>Descrizione

Questo servizio esegue l'operazione di esecuzione su una risorsa dell'istanza di oggetto del client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_id**: ID oggetto.
- **Instance_Id**: ID dell'istanza dell'oggetto.
- **resource_id**: ID risorsa.
- **arguments_ptr**: puntatore agli argomenti dell'operazione di esecuzione. Può essere NULL se arguments_length è zero.
- **arguments_length**: lunghezza degli argomenti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: la risorsa non supporta l'operazione di esecuzione.
- **NX_LWM2M_NOT_FOUND**: ID oggetto, ID istanza oggetto o ID risorsa inesistente.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_get_next"></a>nx_lwm2m_client_object_get_next

Ottenere l'elenco di oggetti implementati dal client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_get_next(NX_LWM2M_CLIENT *client_ptr,
                                    NX_LWM2M_ID *object_id_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'ID dell'oggetto successivo implementato dal client LWM2M. Se l'ID oggetto corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito il primo ID oggetto.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_id_ptr**: puntatore all'ID dell'oggetto corrente. Il risultato restituito contiene l'ID oggetto successivo implementato dal client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita..
- **NX_LWM2M_NOT_FOUND**: l'ID oggetto specificato è l'ultimo del database.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_object_instance_get_next"></a>nx_lwm2m_client_object_instance_get_next

Ottiene l'elenco di istanze di un oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_object_instance_get_next(NX_LWM2M_CLIENT *client_ptr,
                    NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'ID dell'istanza di oggetto successiva dell'oggetto specificato. Se l'ID istanza corrente è impostato su NX_LWM2M_RESERVED_ID (65535), viene restituito l'ID della prima istanza.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_id**: ID oggetto.
- **instance_id_ptr**: puntatore all'ID dell'istanza dell'oggetto corrente. In return contiene l'ID dell'istanza successiva dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita..
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

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_id**: ID oggetto.
- **Instance_Id**: ID dell'istanza dell'oggetto.
- **num_values**: numero di risorse da leggere.
- **values_ptr**: puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse da leggere. In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: una risorsa non supporta l'operazione di lettura.
- **NX_LWM2M_NOT_FOUND**: ID oggetto, ID istanza oggetto o ID risorsa inesistente.
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

È possibile specificare le operazioni di scrittura seguenti per il parametro *write_op* :

- **0** &mdash; aggiornamento parziale: aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate le altre risorse esistenti,

- **NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Sostituisci istanza: sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa specificati.

- **NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Sostituisci risorsa: sostituisce le risorse con i nuovi valori di risorsa forniti, usati per sostituire più risorse.

- **NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Write: indica una chiamata da una sequenza di bootstrap.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **object_id**: ID oggetto.
- **Instance_Id**: ID dell'istanza dell'oggetto.
- **num_values**: numero di risorse da scrivere.
- **values_ptr**: puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse, i tipi e i valori da scrivere.
- **write_op**: tipo di operazione di scrittura.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il tipo di una risorsa non è valido.
- **NX_LWM2M_BUFFER_TOO_SMALL**: la lunghezza di un valore è troppo grande per essere archiviata nell'istanza di.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: una risorsa non supporta l'operazione di scrittura.
- **NX_LWM2M_NO_MEMORY**: non è possibile allocare memoria per archiviare un valore di risorsa.
- **NX_LWM2M_NOT_ACCEPTABLE**: il valore di una risorsa non è valido.
- **NX_LWM2M_NOT_FOUND**: ID oggetto, ID istanza oggetto o ID risorsa inesistente.
- NX_OPTION_ERROR: tipo di operazione di scrittura non valido.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_security_key_callbacks_set"></a>nx_lwm2m_client_security_key_callbacks_set

Imposta callback di gestione delle chiavi degli oggetti di sicurezza

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_security_key_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_CLIENT_SECURITY_KEY_WRITE_CALLBACK write_callback,
                NX_LWM2M_CLIENT_SECURITY_KEY_DELETE_CALLBACK delete_callback);
```

### <a name="description"></a>Descrizione

Questo servizio installa i callback dell'applicazione per l'implementazione delle operazioni sulle risorse degli oggetti di sicurezza LWM2M correlate alle chiavi di sicurezza.

Il client LWM2M delega la gestione delle chiavi di sicurezza all'applicazione durante le sessioni di bootstrap. i callback verranno chiamati quando il server di bootstrap scrive o Elimina le risorse seguenti in un'istanza dell'oggetto di sicurezza: chiave pubblica o identità (3), chiave pubblica del server (4), chiave privata (5).

L'applicazione è responsabile dell'archiviazione dei dati delle chiavi e della configurazione delle sessioni DTLS usate dal client LWM2M.

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.
- **write_callback**: callback del metodo della chiave ' Write '.
- **delete_callback**: callback del metodo della chiave ' Delete '.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_bootstrap"></a>nx_lwm2m_client_session_bootstrap

Avviare una sessione con un server bootstrap

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_bootstrap(NX_LWM2M_CLIENT_SESSION
    *session_ptr, NX_LWM2M_ID security_id, ULONG ip_address, UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione con un server bootstrap. Il server deve disporre di un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.

Se la risorsa ' Mantieni fuori ' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà il bootstrap avviato dal server, se non è stato avviato alcun bootstrap dal server dopo questo periodo di tempo in cui verrà eseguito un bootstrap avviato dal client.

Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server bootstrap.

### <a name="parameters"></a>Parametri

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.
- **security_id**: l'ID dell'istanza di sicurezza del server bootstrap deve essere impostato su NX_LWM2M_RESERVED_ID (65535) se nel server bootstrap non è definita alcuna istanza di sicurezza.
- **ip_address**: indirizzo IP del server.
- **Port**: porta UDP del server.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_NOT_FOUND**: non è presente alcuna istanza di oggetto di sicurezza corrispondente all'ID dell'istanza di sicurezza.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a>nx_lwm2m_client_session_bootstrap_dtls

Avviare una sessione protetta con un server bootstrap

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID security_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una sessione con un server bootstrap usando una connessione DTLS sicura. Il server deve disporre di un'istanza di sicurezza corrispondente nell'oggetto di sicurezza.

Prima di chiamare questa funzione, è necessario che la sessione DTLS sia stata configurata con i pacchetti di crittografia e il materiale della chiave appropriati. È necessario definire NX_SECURE_ENABLE_DTLS.

Se la risorsa ' Mantieni fuori ' è diversa da zero nell'istanza di sicurezza associata a questo server, la sessione attenderà il bootstrap avviato dal server, se non è stato avviato alcun bootstrap dal server dopo questo periodo di tempo in cui verrà eseguito un bootstrap avviato dal client.

Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server bootstrap.

### <a name="parameters"></a>Parametri

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.
- **security_id**: l'ID dell'istanza di sicurezza del server bootstrap deve essere impostato su NX_LWM2M_RESERVED_ID (65535) se nel server bootstrap non è definita alcuna istanza di sicurezza.
- **ip_address**: indirizzo IP del server.
- **Port**: porta UDP del server.
- **dtls_session_ptr**: la sessione DTLS da usare per la sessione bootstrap.
- **dtls_local_port**: la porta UDP locale utilizzata per la sessione DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_NOT_FOUND**: non è presente alcuna istanza di oggetto di sicurezza corrispondente all'ID dell'istanza di sicurezza.
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

Questo servizio crea una nuova sessione client di LWM2M collegata a un client LWM2M esistente. La sessione viene usata dal client LWM2M per comunicare con un server bootstrap o un server LWM2M.

L'applicazione deve fornire una funzione di callback che verrà chiamata quando viene aggiornato lo stato della sessione.

### <a name="parameters"></a>Parametri

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.
- **client_ptr**: puntatore al client LWM2M creato in precedenza.
- **state_callback**: callback dell'applicazione che viene chiamato quando lo stato della sessione viene modificato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_delete"></a>nx_lwm2m_client_session_delete

Elimina sessione client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina una sessione client di LWM2M.

Quando un client LWM2M viene eliminato chiamando nx_lwm2m_client_delete vengono eliminate anche tutte le sessioni associate al client.

### <a name="parameters"></a>Parametri

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_deregister"></a>nx_lwm2m_client_session_deregister

Terminare una sessione con un server LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di annullamento della registrazione in un server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_NOT_REGISTERED**: il client non è registrato nel server.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_error_get"></a>nx_lwm2m_client_session_error_get

Ottenere l'ultimo errore di una sessione

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il codice di errore della sessione quando la sessione è in stato di errore.

### <a name="parameters"></a>Parametri

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: la sessione non è in stato di errore.
- **NX_LWM2M_ADDRESS_ERROR**: Indirizzo server non valido.
- **NX_LWM2M_BUFFER_TOO_SMALL**: il payload della richiesta non rientra nel buffer di rete.
- **NX_LWM2M_DTLS_ERROR**: non è stato possibile stabilire una connessione protetta con il server.
- **NX_LWM2M_ERROR**: errore non specificato.
- **NX_LWM2M_FORBIDDEN**: la registrazione è stata rifiutata dal server.
- **NX_LWM2M_NOT_FOUND**: il client non è stato trovato dal server durante l'aggiornamento/annullamento della registrazione.
- **NX_LWM2M_SERVER_INSTANCE_DELETED**: l'istanza dell'oggetto server corrispondente alla sessione è stata eliminata.
- **NX_LWM2M_TIMED_OUT**: nessuna risposta dal server.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_session_register"></a>nx_lwm2m_client_session_register

Avviare una sessione con un server LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_session_register(NX_LWM2M_CLIENT_SESSION *session_ptr,
                    NX_LWM2M_ID server_id, ULONG ip_address, UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio esegue un'operazione di registrazione in un server LWM2M. Il server deve disporre di un'istanza del server corrispondente nell'oggetto server.

Se la registrazione ha esito positivo, il client LWM2M elaborerà ulteriori operazioni dal server e invierà periodicamente messaggi di aggiornamento finché il client non viene deregistrato.

Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.
- **server_id**: ID server breve del server LWM2M.
- **ip_address**: indirizzo IP del server.
- **Port**: porta UDP del server.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita..
- **NX_LWM2M_NOT_FOUND**: non esiste alcuna istanza dell'oggetto server corrispondente all'ID server breve.
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

Questo servizio esegue un'operazione di registrazione in un server LWM2M usando una connessione DTLS sicura. Il server deve disporre di un'istanza del server corrispondente nell'oggetto server.

Prima di chiamare questa funzione, è necessario che la sessione DTLS sia stata configurata con i pacchetti di crittografia e il materiale della chiave appropriati. È necessario definire NX_SECURE_ENABLE_DTLS.

Ogni sessione DTLS usa il proprio socket UDP per la comunicazione, quindi la porta locale dtls_local_port deve essere diversa per ogni sessione se l'applicazione crea diverse sessioni sicure.

Se la registrazione ha esito positivo, il client LWM2M elaborerà ulteriori operazioni dal server e invierà periodicamente messaggi di aggiornamento finché il client non viene deregistrato.

Tutte le sessioni attive correnti vengono interrotte dalla chiamata e sostituite dalla nuova sessione del server LWM2M.

### <a name="parameters"></a>Parametri

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.
- **server_id**: ID server breve del server LWM2M.
- **ip_address**: indirizzo IP del server.
- **Port**: porta UDP del server.
- **dtls_session_ptr**: la sessione DTLS da usare per la sessione LWM2M.
- **dtls_local_port**: la porta UDP locale utilizzata per la sessione DTLS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_NOT_FOUND**: non esiste alcuna istanza dell'oggetto server corrispondente all'ID server breve.
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

- **session_ptr**: puntatore al blocco di controllo della sessione client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_NOT_REGISTERED**: il client non è registrato nel server.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_client_unlock"></a>nx_lwm2m_client_unlock

Sbloccare il client LWM2M

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Sblocca il previoulsy client di LWM2M bloccato da una chiamata a nx_lwm2m_client_unlock ().

### <a name="parameters"></a>Parametri

- **client_ptr**: puntatore al blocco di controllo client LWM2M.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_firmware_create"></a>nx_lwm2m_firmware_create

Crea oggetto aggiornamento firmware

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_firmware_create(NX_LWM2M_FIRMWARE *firmware_ptr,
    NX_LWM2M_CLIENT *client_ptr, UINT protocols,
    NX_LWM2M_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_FIRMWARE_UPDATE_CALLBACK update_callback);
```

### <a name="description"></a>Descrizione

Questo servizio Inizializza un oggetto di aggiornamento del firmware e aggiunge l'oggetto a un client LWM2M creato in precedenza. L'oggetto di aggiornamento del firmware implementa le risorse per la comunicazione con un server LWM2M, ma l'applicazione deve fornire callback per implementare le operazioni effettive nel firmware (dowloading, archiviazione e aggiornamento del firmware).

Il parametro Protocols indica i protocolli supportati dall'applicazione per il recupero del firmware con la risorsa ' URI pacchetto '. vengono definiti i flag seguenti:

NX_LWM2M_FIRMWARE_PROTOCOL_COAP, NX_LWM2M_FIRMWARE_PROTOCOL_COAPS, NX_LWM2M_FIRMWARE_PROTOCOL_HTTP NX_LWM2M_FIRMWARE_PROTOCOL_HTPPS.

### <a name="parameters"></a>Parametri

- **firmware_ptr**: puntatore al blocco di controllo dell'oggetto firmware.
- **client_ptr**: puntatore a PREVISOUSLY creato LWM2M client.
- **protocolli**: flag che indicano i protocolli supportati dalla risorsa URI del pacchetto.
- **package_callback**: deve essere null [TBD].
- **package_uri_callback**: callback utilizzato per implementare la risorsa URI del pacchetto.
- **update_callback**: callback utilizzato per implementare la risorsa di aggiornamento.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_firmware_package_info_set"></a>nx_lwm2m_firmware_package_info_set

Impostare le informazioni sul pacchetto di aggiornamento del firmware

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_firmware_package_info_set(NX_LWM2M_FIRMWARE *firmware_ptr,
                                const CHAR *name, const CHAR *version);
```

### <a name="description"></a>Descrizione

Questo servizio modifica i valori delle risorse ' PkgName ' (6) è PkgVersion ' (7) dell'oggetto di aggiornamento del firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr**: puntatore all'oggetto di aggiornamento del firmware.
- **nome**: nuovo valore del nome del pacchetto.
- **Version**: nuovo valore della versione del pacchetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_firmware_result_set"></a>nx_lwm2m_firmware_result_set

Imposta il risultato dell'aggiornamento del firmware

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_firmware_result_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR result);
```

### <a name="description"></a>Descrizione

Questo servizio modifica il valore della risorsa ' aggiornamento risultato ' (5) dell'oggetto aggiornamento firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr**: puntatore all'oggetto di aggiornamento del firmware.
- **risultato**: nuovo valore della risorsa del risultato dell'aggiornamento.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_firmware_state_set"></a>nx_lwm2m_firmware_state_set

Imposta lo stato di aggiornamento del firmware

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_firmware_state_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR state);
```

### <a name="description"></a>Descrizione

Questo servizio modifica il valore della risorsa ' state ' (3) dell'oggetto di aggiornamento del firmware.

### <a name="parameters"></a>Parametri

- **firmware_ptr**: puntatore all'oggetto di aggiornamento del firmware.
- **stato**: nuovo valore della risorsa di stato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- NX_PTR_ERROR: puntatore non valido.

## <a name="nx_lwm2m_object_resource_changed"></a>nx_lwm2m_object_resource_changed

Modifica del segnale di un valore di risorsa di un'istanza dell'oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_object_resource_changed(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato da un'implementazione dell'oggetto per segnalare al client LWM2M che uno dei relativi valori di risorsa è stato modificato. Il client LWM2M invierà una notifica se la risorsa viene osservata da un server LWM2M.

### <a name="parameters"></a>Parametri

- **object_ptr**: puntatore all'implementazione dell'oggetto.
- **instance_ptr**: puntatore all'istanza dell'oggetto.
- **Resource**: puntatore alla struttura che descrive la risorsa che è stata modificata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
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

- **valore**: puntatore alla descrizione del valore della risorsa.
- **bool_ptr**: puntatore al valore booleano di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
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

- **valore**: puntatore alla descrizione del valore della risorsa.
- **float32_ptr**: puntatore al valore a virgola mobile a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
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

- **valore**: puntatore alla descrizione del valore della risorsa.
- **float64_ptr**: puntatore al valore a virgola mobile a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore a virgola mobile.

## <a name="nx_lwm2m_resource_get_integer32"></a>nx_lwm2m_resource_get_integer32

Ottenere il valore di una risorsa Integer a 32 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_integer32(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa Integer a 32 bit.

### <a name="parameters"></a>Parametri

- **valore**: puntatore alla descrizione del valore della risorsa.
- **int32_ptr**: puntatore al valore Integer a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore intero oppure il valore integer non rientra in un numero a 32 bit.

## <a name="nx_lwm2m_resource_get_integer64"></a>nx_lwm2m_resource_get_integer64

Ottenere il valore di una risorsa Integer a 64 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_integer64(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa Integer a 64 bit.

### <a name="parameters"></a>Parametri

- **valore**: puntatore alla descrizione del valore della risorsa.
- **int64_ptr**: puntatore al valore Integer a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore integer.

## <a name="nx_lwm2m_resource_get_objlnk"></a>nx_lwm2m_resource_get_objlnk

Ottenere il valore di una risorsa di collegamento a un oggetto

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_objlnk(const NX_LWM2M_RESOURCE *value,
                                    NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa di collegamento a un oggetto.

### <a name="parameters"></a>Parametri

- **valore**: puntatore alla descrizione del valore della risorsa.
- **objlnk_ptr**: puntatore al valore del collegamento all'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore di collegamento a un oggetto.

## <a name="nx_lwm2m_resource_get_opaque"></a>nx_lwm2m_resource_get_opaque

Ottenere il valore di una risorsa opaca

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_opaque(const NX_LWM2M_RESOURCE *value,
            const VOID **opaque_ptr_ptr, UINT *opaque_length_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa opaca.

Un valore di risorsa opaco è costituito da un puntatore a un buffer e una lunghezza.

### <a name="parameters"></a>Parametri

- **valore**: puntatore alla descrizione del valore della risorsa.
- **opaque_ptr_ptr**: puntatore al puntatore al buffer opaco di destinazione.
- **opaque_length_ptr**: puntatore alla lunghezza del buffer opaco di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore opaco.

## <a name="nx_lwm2m_resource_get_string"></a>nx_lwm2m_resource_get_string

Ottenere il valore di una risorsa di stringa

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_get_string(const NX_LWM2M_RESOURCE *value,
            const CHAR **string_ptr_ptr, UINT *string_length_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di una risorsa di stringa.

### <a name="parameters"></a>Parametri

- **valore**: puntatore alla descrizione del valore della risorsa.
- **string_ptr_ptr**: puntatore al puntatore della stringa di destinazione.
- **string_length_ptr**: puntatore alla lunghezza della stringa di destinazione. Può essere NULL se la stringa è con terminazione null.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_ENCODING**: il valore della risorsa non è un valore stringa.

## <a name="nx_lwm2m_resource_multiple_get_boolean"></a>nx_lwm2m_resource_multiple_get_boolean

Ottenere il valore di una risorsa booleana più istanze di risorse

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_boolean(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa booleana da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value**: puntatore alla descrizione del valore di più risorse.
- **index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.
- **instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.
- **bool_ptr**: puntatore al valore booleano di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore booleano.

## <a name="nx_lwm2m_resource_multiple_get_float32"></a>nx_lwm2m_resource_multiple_get_float32

Ottenere il valore di un'istanza a virgola mobile a virgola mobile a 32 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_float32(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa a virgola mobile a 32 bit da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value**: puntatore alla descrizione del valore di più risorse.
- **index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.
- **instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.
- **float32_ptr**: puntatore al valore a virgola mobile a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore a virgola mobile.

## <a name="nx_lwm2m_resource_multiple_get_float64"></a>nx_lwm2m_resource_multiple_get_float64

Ottenere il valore di un'istanza a virgola mobile a virgola mobile a 64 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_float64(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa a virgola mobile a 64 bit da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value**: puntatore alla descrizione del valore di più risorse.
- **index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.
- **instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.
- **float64_ptr**: puntatore al valore a virgola mobile a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore a virgola mobile.

## <a name="nx_lwm2m_resource_multiple_get_integer32"></a>nx_lwm2m_resource_multiple_get_integer32

Ottenere il valore di un'istanza di più risorse di un Integer a 32 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_integer32(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa Integer a 32 bit da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value**: puntatore alla descrizione del valore di più risorse.
- **index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.
- **instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.
- **int32_ptr**: puntatore al valore Integer a 32 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore intero oppure il valore integer non rientra in un numero a 32 bit.

## <a name="nx_lwm2m_resource_multiple_get_integer64"></a>nx_lwm2m_resource_multiple_get_integer64

Ottenere il valore di un'istanza di più risorse di un Integer a 64 bit

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_integer64(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa Integer a 64 bit da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value**: puntatore alla descrizione del valore di più risorse.
- **index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.
- **instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.
- **int64_ptr**: puntatore al valore Integer a 64 bit di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore integer.

## <a name="nx_lwm2m_resource_multiple_get_objlnk"></a>nx_lwm2m_resource_multiple_get_objlnk

Ottenere il valore di un oggetto collegamento a più istanze di risorse

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_objlnk(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa collegamento a un oggetto da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value**: puntatore alla descrizione del valore di più risorse.
- **index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.
- **instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.
- **objlnk_ptr**: puntatore al valore del collegamento all'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore di collegamento a un oggetto.

## <a name="nx_lwm2m_resource_multiple_get_opaque"></a>nx_lwm2m_resource_multiple_get_opaque

Ottenere il valore di un'istanza di più risorse opaca

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_opaque(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const VOID **opaque_ptr_ptr,
    UINT *opaque_length_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa opaca da una risorsa multipla.

Un valore di risorsa opaco è costituito da un puntatore a un buffer e una lunghezza.

### <a name="parameters"></a>Parametri

- **value**: puntatore alla descrizione del valore di più risorse.
- **index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.
- **instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.
- **opaque_ptr_ptr**: puntatore al puntatore al buffer opaco di destinazione.
- **opaque_length_ptr**: puntatore alla lunghezza del buffer opaco di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore della risorsa non è un valore opaco.

## <a name="nx_lwm2m_resource_multiple_get_string"></a>nx_lwm2m_resource_multiple_get_string

Ottenere il valore di una stringa con più istanze di risorse

### <a name="prototype"></a>Prototipo

```c
UINT nx_lwm2m_resource_multiple_get_string(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const CHAR **string_ptr_ptr,
    UINT *string_length_ptr);
```

### <a name="description"></a>Descrizione

Il servizio recupera il valore di un'istanza di risorsa stringa da una risorsa multipla.

### <a name="parameters"></a>Parametri

- **value**: puntatore alla descrizione del valore di più risorse.
- **index**: Indice dell'istanza da recuperare nella matrice di valori di risorsa.
- **instance_id_ptr**: puntatore all'ID dell'istanza di destinazione.
- **string_ptr_ptr**: puntatore al puntatore della stringa di destinazione.
- **string_length_ptr**: puntatore alla lunghezza della stringa di destinazione. Può essere NULL se la stringa è con terminazione null.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: operazione riuscita.
- **NX_LWM2M_BAD_PARAMETER**: l'indice non è compreso nell'intervallo.
- **NX_LWM2M_BAD_ENCODING**: la risorsa non è una risorsa multipla oppure il valore dell'istanza non è un valore stringa.
