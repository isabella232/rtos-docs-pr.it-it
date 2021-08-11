---
title: Capitolo 3 - Descrizione funzionale Azure RTOS NetX LWM2M
description: Questo capitolo contiene una descrizione funzionale Azure RTOS NetX LWM2M.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6424023a02aedf43c7433c9adc09231b8c146af13b9bddc15ebd1f2fc02e8c8a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784938"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-lwm2m"></a>Capitolo 3 - Descrizione funzionale Azure RTOS NetX LWM2M

Questo capitolo contiene una descrizione funzionale Azure RTOS NetX LWM2M.

## <a name="lwm2m-client-initialization"></a>Inizializzazione del client LWM2M

Il client LWM2M viene inizializzato chiamando ***nx_lwm2m_client_create*** servizio. Il client LWM2M viene eseguito nel proprio thread e può segnalare alcuni eventi all'applicazione tramite l'uso di callback o chiamando metodi degli oggetti personalizzati implementati dall'applicazione.

Inoltre, le sessioni client LWM2M devono essere create chiamando nx_lwm2m_client_session_create per ***abilitare*** la comunicazione con uno o più server. Una sessione può comunicare con due tipi diversi di server: un server Bootstrap o un server LWM2M (Gestione dispositivi).

### <a name="bootstrap-server-session"></a>Sessione del server Bootstrap

Una sessione di comunicazione con un server Bootstrap viene usata per effettuare il provisioning delle informazioni essenziali nel client LWM2M per consentire al client LWM2M di eseguire l'operazione "Registra" con uno o più server LWM2M. Questo tipo di server viene usato durante le modalità bootstrap avviata dal client e avviata dal server.

L'applicazione può avviare una sessione bootstrap chiamando ***nx_lwm2m_client_session_bootstrap** _ o _*_nx_lwm2m_client_session_bootstrap_dtls_*_, deve fornire l'indirizzo IP e il numero di porta del server e un ID istanza dell'oggetto di sicurezza facoltativo. La _*_nx_lwm2m_client_session_bootstrap_*_ usa la comunicazione non sicura, mentre _ *_nx_lwm2m_client_session_bootstrap_dtls_** stabilisce una connessione DTLS protetta con il server.

Se l'operazione bootstrap ha esito positivo, il server Bootstrap deve aver creato le istanze dell'oggetto di sicurezza per i server Bootstrap e LWM2M e le istanze dell'oggetto server per i server LWM2M. L'applicazione deve usare queste informazioni per stabilire una sessione con i server LWM2M.

I dati bootstrap devono essere salvati in memoria non volatile dall'applicazione per configurare il client LWM2M al successivo riavvio del dispositivo.

### <a name="lwm2m-server-session"></a>Sessione del server LWM2M

Una sessione di comunicazione con un server LWM2M viene usata per la registrazione, la gestione dei dispositivi e l'abilitazione del servizio.

L'applicazione può registrare il client LWM2M in un server chiamando ***nx_lwm2m_client_session_register** _ _*_o nx_lwm2m_client_session_register_dtls_*_, deve fornire l'indirizzo IP e il numero di porta del server e l'ID server breve che corrisponde a un'istanza dell'oggetto server esistente. La _*_nx_lwm2m_client_session_register_*_ usa la comunicazione non sicura, mentre _ *_nx_lwm2m_client_session_register_dtls_** stabilisce una connessione DTLS protetta con il server.

L'applicazione può deregistrare il client LWM2M chiamando ***nx_lwm2m_client_session_deregister** _, e chiedere al client di inviare un messaggio "Update" chiamando _*_nx_lwm2m_client_session_update_**.

### <a name="session-state-callback"></a>Callback dello stato della sessione

L'applicazione registra un callback al momento della creazione di una sessione che viene chiamata quando lo stato della sessione viene aggiornato, la funzione di callback NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK ha il prototipo seguente:

```c
typedef VOID (*NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK)
        (NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state);
```

Vengono definiti gli stati seguenti:

- **NX_LWM2M_CLIENT_SESSION_INIT:** stato iniziale dopo la creazione della sessione.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING:** il client è in attesa della scadenza del timer "Hold Off" o del bootstrap avviato dal server.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**: il client ha inviato un messaggio "Richiesta" al server Bootstrap (bootstrap avviato dal client).

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**: il client riceve dati dal server Bootstrap.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:** il server Bootstrap ha inviato un messaggio "Finished".

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:** la sessione bootstrap non è riuscita.

- **NX_LWM2M_CLIENT_SESSION_REGISTERING:** il client ha inviato un messaggio "Registra" al server LWM2M.

- **NX_LWM2M_CLIENT_SESSION_REGISTERED**: il client è registrato nel server LWM2M.

- **NX_LWM2M_CLIENT_SESSION_UPDATING:** il client ha inviato un messaggio 'Update' al server LWM2M.

- **NX_LWM2M_CLIENT_SESSION_DEREGISTERING:** il client ha inviato un messaggio di "Deregistrazione" al server LWM2M.

- **NX_LWM2M_CLIENT_SESSION_DEREGISTERED:** il client viene de-registrato dal server LWM2M.

- **NX_LWM2M_CLIENT_SESSION_DISABLED:** il server LWM2M è disabilitato. Un 'Register' verrà inviato dopo la scadenza del timer di disabilitazione.

- **NX_LWM2M_CLIENT_SESSION_ERROR:** l'operazione di registrazione o aggiornamento al server LWM2M non è riuscita.

- **NX_LWM2M_CLIENT_SESSION_DELETED:** l'istanza dell'oggetto server corrispondente al server LWM2M è stata eliminata. In caso di errore, l'applicazione può recuperare la causa dell'errore **_chiamando nx_lwm2m_client_session_error_get_**.

## <a name="local-device-management"></a>Gestione dei dispositivi locali

L'applicazione può accedere agli oggetti del client LWM2M usando le funzioni di gestione dei dispositivi locali. Vengono fornite le funzioni seguenti:

- ***nx_lwm2m_client_object_read***: legge le risorse da un'istanza dell'oggetto.

- ***nx_lwm2m_client_object_discover***: ottenere l'elenco delle risorse di un'istanza dell'oggetto.

- ***nx_lwm2m_client_object_write***: Scrivere risorse in un'istanza di oggetto

- ***nx_lwm2m_client_object_execute***: eseguire l'operazione Execute su una risorsa di un'istanza dell'oggetto.

- ***nx_lwm2m_client_object_create***: creare una nuova istanza dell'oggetto.

- ***nx_lwm2m_client_object_delete***: elimina un'istanza dell'oggetto esistente.

- ***nx_lwm2m_client_object_get_next:*** ottenere l'ID oggetto successivo implementato dal client LWM2M.

- ***nx_lwm2m_client_object_instance_get_next***: ottiene l'istanza successiva di un oggetto.

## <a name="resource-information"></a>Informazioni sulle risorse

Durante la lettura e la scrittura in oggetti, una risorsa è rappresentata dalla NX_LWM2M_RESOURCE struttura . Questa struttura contiene l'ID della risorsa/istanza e il relativo valore. La codifica del valore dipende dal tipo e dall'origine (applicazione o rete).

La NX_LWM2M_RESOURCE ha la definizione seguente:

```c
typedef struct NX_LWM2M_RESOURCE_STRUCT
{
    NX_LWM2M_ID     nx_lwm2m_resource_id;
    UCHAR           nx_lwm2m_resource_type;
    union
    {
        struct
        {
            const VOID *     nx_lwm2m_resource_buffer_ptr;
            UINT             nx_lwm2m_resource_buffer_length;
        } nx_lwm2m_resource_bufferdata;
        const CHAR *         nx_lwm2m_resource_stringdata;
        NX_LWM2M_INT32       nx_lwm2m_resource_integer32data;
        NX_LWM2M_INT64       nx_lwm2m_resource_integer64data;
        NX_LWM2M_FLOAT32     nx_lwm2m_resource_float32data;
        NX_LWM2M_FLOAT64     nx_lwm2m_resource_float64data;
        NX_LWM2M_BOOL        nx_lwm2m_resource_booleandata;
        NX_LWM2M_OBJLNK      nx_lwm2m_resource_objlnkdata;
        
        struct
        {
            const VOID *     nx_lwm2m_resource_multiple_ptr;
            UINT             nx_lwm2m_resource_multiple_dim;
        } nx_lwm2m_resource_multipledata;
    } nx_lwm2m_resource_value;
} NX_LWM2M_RESOURCE;
```

- **nx_lwm2m_resource_id**: ID della risorsa o dell'istanza.
- **nx_lwm2m_resource_type:** il tipo del valore, vedere di seguito.
- **nx_lwm2m_resource_value:** il valore della risorsa dipende dal tipo del valore.

Vengono definiti i tipi di valori seguenti:

- **NX_LWM2M_RESOURCE_NONE:** risorsa vuota.

- **NX_LWM2M_RESOURCE_STRING**: valore stringa UTF-8 con terminazione Null archiviato in *nx_lwm2m_resource_stringdata*.

- **NX_LWM2M_RESOURCE_INTEGER32**: valore integer a 32 bit archiviato in *nx_lwm2m_resource_integer32data*.

- **NX_LWM2M_RESOURCE_INTEGER64**: valore integer a 64 bit archiviato in *nx_lwm2m_resource_integer64data*.

- **NX_LWM2M_RESOURCE_FLOAT32**: valore a virgola mobile a 32 bit archiviato in *nx_lwm2m_resource_float32data*.

- **NX_LWM2M_RESOURCE_FLOAT64**: valore a virgola mobile a 64 bit archiviato in *nx_lwm2m_resource_float64data*.

- **NX_LWM2M_RESOURCE_BOOLEAN**: valore booleano archiviato in *nx_lwm2m_resource_booleandata*.

- **NX_LWM2M_RESOURCE_OPAQUE:** valore opaco definito da *nx_lwm2m_resource_bufferdata*.

- **NX_LWM2M_RESOURCE_OBJLNK:** valore di Object Link archiviato in *nx_lwm2m_resource_objlnkdata*.

- **NX_LWM2M_RESOURCE_TLV**: valore con codifica TLV definito da *nx_lwm2m_resource_bufferdata*.

- **NX_LWM2M_RESOURCE_TEXT**: valore Plain-Text codificato definito da *nx_lwm2m_resource_bufferdata*.

- **NX_LWM2M_RESOURCE_MULTIPLE**: una risorsa multipla definita da *nx_lwm2m_resource_multipledata*. *nx_lwm2m_resource_multiple_ptr* è un puntatore a una matrice **di NX_LWM2M_RESOURCE** contenenti informazioni su ogni istanza di risorsa.

- **NX_LWM2M_RESOURCE_MULTIPLE_TLV**: una risorsa multipla definita da *nx_lwm2m_resource_multipledata*. *nx_lwm2m_resource_multiple_ptr* è un puntatore a un buffer con codifica TLV.

Per recuperare il valore e controllarne il tipo, l'applicazione non deve mai accedere direttamente al campo *nx_lwm2m_resource_value* quando si recupera un valore da una struttura NX_LWM2M_RESOURCE. Vengono definite le funzioni seguenti:

- ***nx_lwm2m_resource_get_***: ottenere un valore con il tipo specificato.
- ***nx_lwm2m_resource_multiple_get_:*** ottenere un valore con il tipo specificato da una risorsa multipla.

La macro **NX_LWM2M_RESOURCE_IS_MULTIPLE**(tipo) può essere usata per verificare se un tipo di risorsa è una risorsa multipla.

## <a name="object-implementation"></a>Implementazione di oggetti

Il client LWM2M implementa gli oggetti OMA LWM2M obbligatori: Sicurezza (0), Server (1), Controllo di accesso (2) e Dispositivo (3). Altri oggetti specifici del dispositivo devono essere implementati dall'applicazione.

Per definire un oggetto vengono usate due strutture di dati: la struttura NX_LWM2M_OBJECT definisce l'implementazione dell'oggetto, inclusi l'ID oggetto e i metodi dell'oggetto, e la struttura NX_LWM2M_OBJECT_INSTANCE contiene i dati di un'istanza dell'oggetto.

La NX_LWM2M_OBJECT struttura presenta la definizione seguente:

```c
typedef struct NX_LWM2M_OBJECT_STRUCT
{
    NX_LWM2M_OBJECT * nx_lwm2m_object_next;
    NX_LWM2M_ID nx_lwm2m_object_id;
    UINT (*nx_lwm2m_object_read)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
        NX_LWM2M_RESOURCE *values);
    UINT (*nx_lwm2m_object_discover)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT *num_resources,
        NX_LWM2M_RESOURCE_INFO *resources);
    UINT (*nx_lwm2m_object_write)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values, const
        NX_LWM2M_RESOURCE *values, UINT write_op);
    UINT (*nx_lwm2m_object_execute)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
        const CHAR *args_ptr, UINT args_length);
    UINT (*nx_lwm2m_object_create)(NX_LWM2M_OBJECT * object_ptr,
        NX_LWM2M_ID instance_id, UINT num_values, const NX_LWM2M_RESOURCE
        *values, NX_LWM2M_OBJECT_INSTANCE **instance_ptr);
    UINT (*nx_lwm2m_object_delete)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr);
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instances;
} NX_LWM2M_OBJECT;
```

- **nx_lwm2m_object_next**: oggetto successivo nell'elenco.
- **nx_lwm2m_object_id**: ID oggetto.
- **nx_lwm2m_object_read:** il metodo 'Read', vedere di seguito.
- **nx_lwm2m_object_discover:** il metodo "Discover", vedere di seguito.
- **nx_lwm2m_object_write:** il metodo 'Write', vedere di seguito.
- **nx_lwm2m_object_execute:** il metodo 'Execute', vedere di seguito.
- **nx_lwm2m_object_create:** il metodo 'Create', vedere di seguito.
- **nx_lwm2m_object_delete:** il metodo "Delete", vedere di seguito.
- **nx_lwm2m_object_instances:** elenco di istanze di oggetti con terminazione NULL.

La NX_LWM2M_OBJECT_INSTANCE struttura presenta la definizione seguente:

```c
typedef struct NX_LWM2M_OBJECT_INSTANCE_STRUCT
{
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instance_next;
    NX_LWM2M_ID nx_lwm2m_object_instance_id;
} NX_LWM2M_OBJECT_INSTANCE;
```

- **nx_lwm2m_object_instance_next**: l'istanza successiva nell'elenco.
- **nx_lwm2m_object_instance_id:** ID dell'istanza dell'oggetto.

L'oggetto deve implementare i metodi corrispondenti alle operazioni definite dall'interfaccia di gestione dei dispositivi LWM2M: 'Read', 'Discover', 'Write', 'Execute', 'Create' e 'Delete'. I metodi 'Create' e 'Delete' possono essere impostati su NULL se l'oggetto non supporta la creazione dinamica di istanze.

### <a name="the-read-method"></a>Metodo 'Read'

Il metodo 'Read' viene usato per leggere i valori delle risorse da un'istanza dell'oggetto. La funzione ha la definizione seguente:

```c
UINT nx_lwm2m_object_read(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    NX_LWM2M_RESOURCE *values_ptr);
```

I parametri di input sono definiti come segue:

- **object_ptr:** puntatore all'implementazione dell'oggetto .

- **instance_ptr:** puntatore all'istanza dell'oggetto.

- **num_values:** numero di risorse da leggere.

- **values_ptr:** puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse da leggere. Al ritorno la matrice viene riempita con i tipi e i valori corrispondenti.

### <a name="the-discover-method"></a>Metodo 'Discover'

Il metodo 'Discover' viene usato per recuperare l'elenco di tutte le risorse implementate da un oggetto . La funzione ha la definizione seguente:

```c
UINT nx_lwm2m_object_discover(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT *num_resources_ptr,
    NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

I parametri di input sono definiti come segue:

- **object_ptr:** puntatore all'implementazione dell'oggetto .

- **instance_ptr:** puntatore all'istanza dell'oggetto.

- **num_resources_ptr:** in input le dimensioni del buffer di destinazione, nell'output il numero di elementi scritto nel buffer.

- **resources_ptr:** puntatore al buffer di destinazione.

Le informazioni sulla risorsa vengono restituite in NX_LWM2M_RESOURCE_INFO struttura definita come segue:

```c
typedef struct NX_LWM2M_RESOURCE_INFO_STRUCT
{
    NX_LWM2M_ID     nx_lwm2m_resource_info_id;
    USHORT          nx_lwm2m_resource_info_flags;
    UINT            nx_lwm2m_resource_info_dim;
} NX_LWM2M_RESOURCE_INFO;
```

- **nx_lwm2m_resource_info_id**: ID della risorsa.

- **nx_lwm2m_resource_info_flags**: vedere di seguito.

- **nx_lwm2m_resource_info_dim:** dimensione di Più risorse se il flag NX_LWM2M_RESOURCE_INFO_MULTIPLE è impostato.

Il campo *nx_lwm2m_resource_flags* può avere i valori seguenti:

- 0: singola risorsa leggibile.

- **NX_LWM2M_RESOURCE_INFO_MULTIPLE:** è necessario definire nx_lwm2m_resource_info_dim *più* risorse.

- **NX_LWM2M_RESOURCE_INFO_EXECUTABLE:** risorsa eseguibile o non leggibile.

### <a name="the-write-method"></a>Metodo 'Write'

Il metodo 'Write' viene usato per aggiornare o sostituire le risorse di un'istanza dell'oggetto. La funzione ha la definizione seguente:

```c
UINT nx_lwm2m_object_write(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

I parametri di input sono definiti come segue:

- **object_ptr:** puntatore all'implementazione dell'oggetto .
- **instance_ptr:** puntatore all'istanza dell'oggetto.
- **num_values:** numero di risorse da scrivere.
- **values_ptr:** puntatore ai valori delle risorse.
- **write_op:** tipo di operazioni di scrittura.

Le operazioni di scrittura seguenti possono essere specificate nel *parametro write_op* :

- 0 Aggiornamento parziale: aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate &mdash; le altre risorse esistenti.

- **NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Sostituisci istanza: sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa specificati.

- **NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Sostituisci risorsa: sostituisce le risorse con i nuovi valori di risorsa forniti (usati per sostituire più risorse).

- **NX_LWM2M_OBJECT_WRITE_CREATE** &mdash; Crea istanza: inizializza l'istanza dell'oggetto appena creata con i valori di risorsa specificati (chiamati dal *nx_lwm2m_object_create* metodo ).

- **NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Write: chiamato durante la sequenza bootstrap.

### <a name="the-execute-method"></a>Metodo 'Execute'

Il metodo 'Execute' implementa l'esecuzione di una risorsa oggetto. La funzione ha la definizione seguente:

```c
UINT nx_lwm2m_object_execute(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr);
```

I parametri di input sono definiti come segue:

- **object_ptr:** puntatore all'implementazione dell'oggetto
- **instance_ptr:** puntatore all'istanza dell'oggetto.
- **resource_id**: ID risorsa.
- **arguments_ptr:** puntatore agli argomenti dell'operazione di esecuzione. Può essere NULL se *arguments_length* è zero.
- **arguments_length**: lunghezza degli argomenti.

La funzione deve restituire NX_LWM2M_NOT_FOUND se l'ID risorsa non esiste o NX_LWM2M_METHOD_NOT_ALLOWED se non supporta l'esecuzione.

### <a name="the-create-method"></a>Metodo 'Create'

Il metodo 'Create' implementa la creazione di una nuova istanza dell'oggetto. La funzione ha la definizione seguente:

```c
UINT nx_lwm2m_object_create(NX_LWM2M_OBJECT * object_ptr,
    NX_LWM2M_ID instance_id, UINT num_values, const NX_LWM2M_RESOURCE *values_ptr,
    NX_LWM2M_OBJECT_INSTANCE **instance_ptr, NX_LWM2M_BOOL bootstrap);
```

I parametri di input sono definiti come segue:

- **object_ptr:** puntatore all'implementazione dell'oggetto .
- **instance_id**: ID della nuova istanza.
- **num_values**: numero di risorse da inizializzare.
- **values_ptr:** puntatore ai valori delle risorse.
- **instance_ptr:** puntatore al puntatore di destinazione dell'istanza creata.
- **bootstrap:** True se chiamato dalla sequenza bootstrap.

L'oggetto deve allocare e inizializzare una nuova istanza di Object usando l'elenco fornito di valori di risorsa.

### <a name="the-delete-method"></a>Metodo 'Delete'

Il metodo 'Delete' implementa l'eliminazione di un'istanza di oggetto. La funzione ha la definizione seguente:

```c
UINT nx_lwm2m_object_delete(NX_LWM2M_OBJECT *object_ptr,
                NX_LWM2M_OBJECT_INSTANCE *instance_ptr);
```

I parametri di input sono definiti come segue:

- **object_ptr:** puntatore all'implementazione dell'oggetto .
- **instance_ptr:** puntatore all'istanza dell'oggetto.

In caso di esito positivo, l'oggetto deve rilasciare i dati dell'istanza dell'oggetto e qualsiasi altra risorsa allocata dall'istanza.

### <a name="adding-object-implementations-and-instances-to-the-lwm2m-client"></a>Aggiunta di implementazioni di oggetti e istanze al client LWM2M

L'applicazione può aggiungere una nuova implementazione dell'oggetto al client LWM2M chiamando il ***nx_lwm2m_client_object_add*** servizio.

Se l'oggetto non supporta la creazione dinamica di istanze, ad esempio se è una singola istanza di Object, il campo *nx_lwm2m_object_instances* della struttura di oggetti deve puntare all'elenco delle strutture di istanze statiche.

Se l'oggetto supporta la creazione dinamica di *istanze,* nx_lwm2m_object_instances deve essere impostato su NULL e il servizio ***nx_lwm2m_client_object_create*** deve essere usato per chiamare il metodo 'Create' dell'oggetto.

## <a name="example-of-lwm2m-client-application"></a>Esempio di applicazione client LWM2M

Il codice seguente è un esempio di una semplice applicazione client LWM2M che implementa un dispositivo personalizzato costituito da un sensore di temperatura e da un interruttore di luce.

Il dispositivo consente a un server di leggere il valore del sensore di temperatura e lo stato booleano dell'interruttore di luce e di impostare l'interruttore della luce su on/off.

```c
#include "nx_lwm2m_client.h"

/* Custom Object implementation */
/* Define the Custom Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_OBJECT_INSTANCE     lwm2m;

    /* Resources Data */
    NX_LWM2M_FLOAT32             temperature;
    NX_LWM2M_BOOL                light;
} MYOBJECT_INSTANCE;

/* Define the Resources IDs */
#define MYOBJECT_RES_TEMPERATURE     0 /* temperature sensor */
#define MYOBJECT_RES_LIGHT           1 /* light switch */

/* Define the 'Read' Method */
UINT myobject_read(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr,
    UINT num_values, NX_LWM2M_RESOURCE *values)
{
    UINT i;
    for (i=0; i<num_values; i++)
    {
        switch (values[i].nx_lwm2m_resource_id)
        {
        case MYOBJECT_RES_TEMPERATURE:

            /* return the temperature value */
            values[i].nx_lwm2m_resource_type = NX_LWM2M_RESOURCE_FLOAT32;
            values[i].nx_lwm2m_resource_value.nx_lwm2m_resource_float32data =
                ((MYOBJECT_INSTANCE *) instance_ptr)->temperature;
            break;
        case MYOBJECT_RES_LIGHT:

            /* return the state of the light switch */
            values[i].nx_lwm2m_resource_type = NX_LWM2M_RESOURCE_BOOLEAN;
            values[i].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata =
                ((MYOBJECT_INSTANCE *) instance_ptr)->light;
            break;

        default:

            /* unknown resource ID */
            return NX_LWM2M_NOT_FOUND;
        }
    }
    return NX_SUCCESS;
}

/* Define the 'Discover' method */
UINT myobject_discover(NX_LWM2M_OBJECT *object_ptr, NX_LWM2M_OBJECT_INSTANCE *instance_ptr,
                                    UINT *num_resources, NX_LWM2M_RESOURCE_INFO *resources)
{
    if (*num_resources < 2)
    {
        return NX_LWM2M_BUFFER_TOO_SMALL;
    }

    /* return the list of supported resources IDs */
    *num_resources = 2;
    resources[0].nx_lwm2m_resource_info_id        = MYOBJECT_RES_TEMPERATURE;
    resources[0].nx_lwm2m_resource_info_flags     = 0;
    resources[1].nx_lwm2m_resource_info_id        = MYOBJECT_RES_LIGHT;
    resources[1].nx_lwm2m_resource_info_flags     = 0;
    return NX_SUCCESS;
}

/* Define the 'Write' method */
UINT myobject_write(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    const NX_LWM2M_RESOURCE *values, UINT flags)
{
    UINT i;
    for (i=0; i<num_values; i++)
    {
        UINT ret;
        switch (values[i].nx_lwm2m_resource_id)
        {

        case MYOBJECT_RES_TEMPERATURE:

            /* read-only resource */
            return NX_LWM2M_METHOD_NOT_ALLOWED;

        case MYOBJECT_RES_LIGHT:

            /* assign boolean value */

            ret = nx_lwm2m_resource_get_boolean(&values[i],
                &((MYOBJECT_INSTANCE *) instance_ptr)->light);

            if (ret != NX_SUCCESS)
            {

                /* invalid value type */
                return ret;
            }
            break;

        default:

            /* unknown resource ID */
            return NX_LWM2M_NOT_FOUND;
        }
    }
    return NX_SUCCESS;
}

/* Define the 'Execute' method */
UINT myobject_execute(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
    const CHAR *args_ptr, UINT args_length)
{
    switch (resource_id)
    {

    case MYOBJECT_RES_TEMPERATURE:
    case MYOBJECT_RES_LIGHT:

        /* read-only resource */
        return NX_LWM2M_METHOD_NOT_ALLOWED;

    default:

        /* unknown resource ID */
        return NX_LWM2M_NOT_FOUND;

    }
}

/* NetX data */
NX_IP                       ip;
NX_PACKET_POOL              packet_pool;

/* LWM2M Client data */
NX_LWM2M_CLIENT             client;
ULONG                       client_stack[4096 / sizeof(ULONG)];
NX_LWM2M_CLIENT_SESSION     session;

/* Custom Object Data */
NX_LWM2M_OBJECT             myobject;
MYOBJECT_INSTANCE           myinstance;

/* Define the session state callback */
void session_callback(NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state)
{
    switch (state)
    {

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:

        /* Bootstrap session done, we can register to the LWM2M Server */
        {
            NX_LWM2M_ID security_id;

            /* find the Security Object Instance of the LWM2M Server */
            security_id = NX_LWM2M_RESERVED_ID;
            while (nx_lwm2m_client_object_instance_get_next(&client,
                NX_LWM2M_SECURITY_OBJECT_ID, &security_id) == NX_SUCCESS)
            {
                NX_LWM2M_RESOURCE res[3];

                /* retrieve instance data: */
                /* Bootstrap server flag */
                res[0].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_BOOTSTRAP_ID;

                /* URI of server */
                res[1].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_URI_ID;

                /* Short Server ID */
                res[2].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_SHORT_SERVER_ID;

                /* Read Object Instance: */
                nx_lwm2m_client_object_read(&client,
                    NX_LWM2M_SECURITY_OBJECT_ID, security_id, 3, res);

                /* Not a bootstrap server? */
                if (!res[0].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata)
                {
                    ULONG ip_addr;
                    UINT udp_port;

                    /* get IP address and UDP port from server URI */
                    parse_uri(res[1].nx_lwm2m_resource_value.nx_lwm2m_resource_stringdata, &ip_addr, &udp_port);

                    /* Start registration to the LWM2M server */
                    nx_lwm2m_client_session_register(&session,
                        (NX_LWM2M_ID) res[2].nx_lwm2m_resource_value.
                        nx_lwm2m_resource_integer32data,
                        ip_addr, udp_port);
                    break;
                }
            }
        }
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:

        /* Failed to Bootstrap the LWM2M Client. */
        break;

    case NX_LWM2M_CLIENT_SESSION_REGISTERED:

        /* Registration to the LWM2M Client done. */
        break;

    case NX_LWM2M_CLIENT_SESSION_ERROR:

        /* Failed to register to the LWM2M Client. */
        break;
    }
}

/* Application main thread */
void application_thread(ULONG info)
{
    NX_LWM2M_RESOURCE res[4];
    NX_LWM2M_ID security_id;

    /* Create the LWM2M client */
    nx_lwm2m_client_create(&client, &ip, &packet_pool, NX_LWM2M_COAP_PORT,
        "mylwm2mclient", NULL, NX_LWM2M_BINDING_U,
        client_stack, sizeof(client_stack));

    /* Define our custom object */
    myobject.nx_lwm2m_object_id           = 1024;
    myobject.nx_lwm2m_object_read         = myobject_read;
    myobject.nx_lwm2m_object_discover     = myobject_discover;
    myobject.nx_lwm2m_object_write        = myobject_write;
    myobject.nx_lwm2m_object_execute      = myobject_execute;
    myobject.nx_lwm2m_object_create       = NULL;
    myobject.nx_lwm2m_object_delete       = NULL;

    /* Define a single instance */
    myobject.nx_lwm2m_object_instances             = (NX_LWM2M_OBJECT_INSTANCE *) &myinstance;
    myinstance.lwm2m.nx_lwm2m_object_instance_id   = 0;
    myinstance.lwm2m.nx_lwm2m_object_instance_next = NULL;
    myinstance.temperature                         = 22.5f;
    myinstance.light                               = NX_FALSE;

    /* Add the object to the LWM2M Client */
    nx_lwm2m_client_object_add(&client, &myobject);

    /* Create a security entry for the bootstrap server */
    security_id = 0;

    /* set the URI of the server */
    res[0].nx_lwm2m_resource_id                                 = NX_LWM2M_SECURITY_URI_ID;
    res[0].nx_lwm2m_resource_type                               = NX_LWM2M_RESOURCE_STRING;
    res[0].nx_lwm2m_resource_value.nx_lwm2m_resource_stringdata = "coap://1.2.3.4";

    /* set the Bootstrap flag */
    res[1].nx_lwm2m_resource_id                                  = NX_LWM2M_SECURITY_BOOTSTRAP_ID;
    res[1].nx_lwm2m_resource_type                                = NX_LWM2M_RESOURCE_BOOLEAN;
    res[1].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata = NX_TRUE;

    /* set the security mode */
    res[2].nx_lwm2m_resource_id                                    = NX_LWM2M_SECURITY_MODE_ID;
    res[2].nx_lwm2m_resource_type                                  = NX_LWM2M_RESOURCE_INTEGER32;
    res[2].nx_lwm2m_resource_value.nx_lwm2m_resource_integer32data =
    NX_LWM2M_SECURITY_MODE_NOSEC;

    /* set the Hold Off timer */
    res[3].nx_lwm2m_resource_id                                    = NX_LWM2M_SECURITY_HOLD_OFF_ID;
    res[3].nx_lwm2m_resource_type                                  = NX_LWM2M_RESOURCE_INTEGER32;
    res[3].nx_lwm2m_resource_value.nx_lwm2m_resource_integer32data = 10;
    nx_lwm2m_client_object_create(&client, NX_LWM2M_SECURITY_OBJECT_ID,
        &security_id, 4, res);

    /* Create a session */
    nx_lwm2m_client_session_create(&session, &client, session_callback);

    /* start bootstrap session */
    nx_lwm2m_client_session_bootstrap(&session, security_id,
                            IP_ADDRESS(1, 2, 3, 4), 5683);

    /* Application main loop */
    while (1)
    {
        /* ...application code... */
    }

    /* Terminate the LWM2M Client */
    nx_lwm2m_client_delete(&client);
}
```
