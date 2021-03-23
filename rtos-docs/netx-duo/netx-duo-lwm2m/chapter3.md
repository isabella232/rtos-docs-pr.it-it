---
title: Capitolo 3-Descrizione funzionale del client LWM2M
description: Questo capitolo contiene una descrizione funzionale del client LWM2M.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 24b7ff66fb4d060075eb6bc81bed45b3479e18dc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821842"
---
# <a name="chapter-3--functional-description-of-lwm2m-client"></a>Descrizione funzionale del capitolo 3 del client LWM2M

> Questo capitolo contiene una descrizione funzionale del client LWM2M.

## <a name="lwm2m-client-initialization"></a>Inizializzazione del client LWM2M

Il client LWM2M viene inizializzato chiamando ***nx_lwm2m_client_create*** servizio. Il client LWM2M viene eseguito nel proprio thread e può segnalare alcuni eventi all'applicazione tramite l'uso di callback o chiamando metodi degli oggetti personalizzati implementati dall'applicazione.

Inoltre, è necessario creare sessioni client di LWM2M chiamando ***nx_lwm2m_client_session_create*** per abilitare la comunicazione con uno o più server. Una sessione può comunicare con due tipi diversi di server: un server bootstrap o un server LWM2M (gestione dei dispositivi).

### <a name="bootstrap-server-session"></a>Sessione del server bootstrap

Una sessione di comunicazione con un server bootstrap viene utilizzata per eseguire il provisioning di informazioni essenziali nel client di LWM2M per consentire al client di LWM2M di eseguire l'operazione "Register" con uno o più server LWM2M. Questo tipo di server viene utilizzato durante le modalità bootstrap avviate dal client e avviate dal server.

L'applicazione può avviare una sessione di bootstrap chiamando ***nx_lwm2m_client_session_bootstrap** _ o _*_nx_lwm2m_client_session_bootstrap_dtls_*_, deve fornire l'indirizzo IP e il numero di porta del server e l'ID istanza di un oggetto di sicurezza facoltativo. La funzione _*_nx_lwm2m_client_session_bootstrap_*_ utilizza la comunicazione non protetta, mentre _ *_nx_lwm2m_client_session_bootstrap_dtls_** stabilisce una connessione DTLS protetta con il server.

Se l'operazione di bootstrap ha esito positivo, il server di bootstrap deve avere creato le istanze degli oggetti di sicurezza per i server bootstrap e LWM2M e le istanze dell'oggetto server per i server LWM2M. L'applicazione può chiamare ***nx_lwm2m_client_session_register_info_get*** per ottenere informazioni sui server lwm2m e usare queste informazioni per stabilire una sessione con i server lwm2m.

I dati bootstrap devono essere salvati nella memoria non volatile dall'applicazione per configurare il client di LWM2M al riavvio successivo del dispositivo.

### <a name="lwm2m-server-session"></a>Sessione del server LWM2M

Una sessione di comunicazione con un server LWM2M viene usata per la registrazione, la gestione dei dispositivi e l'abilitazione del servizio.

L'applicazione può registrare il client LWM2M in un server chiamando ***nx_lwm2m_client_session_register** _ o _*_nx_lwm2m_client_session_register_dtls_*_, deve fornire l'indirizzo IP e il numero di porta del server e l'ID del server breve che corrisponde a un'istanza dell'oggetto server esistente. La funzione _*_nx_lwm2m_client_session_register_*_ utilizza la comunicazione non protetta, mentre _ *_nx_lwm2m_client_session_register_dtls_** stabilisce una connessione DTLS protetta con il server.

L'applicazione può annullare la registrazione del client LWM2M chiamando ***nx_lwm2m_client_session_deregister** _ e chiedere al client di inviare un messaggio di aggiornamento chiamando _ *_nx_lwm2m_client_session_update_* *.

### <a name="session-state-callback"></a>Callback dello stato della sessione

L'applicazione registra un callback al momento della creazione di una sessione che viene chiamata quando viene aggiornato lo stato della sessione, la funzione di callback **NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK** dispone del prototipo seguente.

typedef VOID ( \* NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK) (NX_LWM2M_CLIENT_SESSION \* session_ptr, stato uint);

Sono definiti gli Stati seguenti.

| &nbsp;Stato sessione | Descrizione |
| --- | --- |
| **NX_LWM2M_CLIENT_SESSION_INIT** | Stato iniziale dopo la creazione della sessione. |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING** | Il client è in attesa della scadenza del timer ' Mantieni fuori ' o bootstrap avviato dal server. |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING** | Il client ha inviato un messaggio "Request" al server bootstrap (bootstrap avviato dal client). |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED** | Il client riceve i dati dal server bootstrap. |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED** | Il server bootstrap ha inviato un messaggio "finito". |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR** | La sessione bootstrap non è riuscita. |
| **NX_LWM2M_CLIENT_SESSION_REGISTERING** | Il client ha inviato un messaggio di "registro" al server LWM2M. |
| **NX_LWM2M_CLIENT_SESSION_REGISTERED** | Il client viene registrato nel server LWM2M. |
| **NX_LWM2M_CLIENT_SESSION_UPDATING** | Il client ha inviato un messaggio di aggiornamento al server LWM2M. |
| **NX_LWM2M_CLIENT_SESSION_DEREGISTERING** | Il client ha inviato un messaggio "de-Register" al server LWM2M. |
| **NX_LWM2M_CLIENT_SESSION_DEREGISTERED** | Il client viene deregistrato dal server LWM2M. |
| **NX_LWM2M_CLIENT_SESSION_DISABLED** | Il server LWM2M è disabilitato. Un'Register ' verrà inviato dopo la scadenza del timer di disabilitazione. |
| **NX_LWM2M_CLIENT_SESSION_ERROR** | L'operazione di registrazione o aggiornamento al server LWM2M non è riuscita. |
| **NX_LWM2M_CLIENT_SESSION_DELETED** | L'istanza dell'oggetto server corrispondente al server LWM2M è stata eliminata. |

In caso di errore, l'applicazione può recuperare la causa dell'errore chiamando ***nx_lwm2m_client_session_error_get***.

## <a name="local-device-management"></a>Gestione dei dispositivi locali

L'applicazione può accedere agli oggetti del client LWM2M usando le funzioni di gestione dei dispositivi locali. Sono disponibili le funzioni seguenti.

| &nbsp;Nome funzione | Descrizione |
| --- | --- |
| ***nx_lwm2m_client_object_read*** | Leggere le risorse da un'istanza dell'oggetto. |
| ***nx_lwm2m_client_object_discover*** | Ottiene l'elenco delle risorse di un'istanza dell'oggetto.
| ***nx_lwm2m_client_object_write*** | Scrivere le risorse in un'istanza dell'oggetto. |
| ***nx_lwm2m_client_object_execute*** | Eseguire l'operazione Execute su una risorsa di un'istanza dell'oggetto. |
| ***nx_lwm2m_client_object_create*** | Creare una nuova istanza dell'oggetto. |
| ***nx_lwm2m_client_object_delete*** | Eliminare un'istanza dell'oggetto esistente. |
| ***nx_lwm2m_client_object_next_get*** | Ottenere l'ID oggetto successivo dal client LWM2M. |
| ***nx_lwm2m_client_object_instance_next_get*** | Ottiene l'istanza successiva di un oggetto. |

## <a name="resource-information"></a>Informazioni sulle risorse

Durante la lettura e la scrittura negli oggetti, una risorsa viene rappresentata dalla struttura NX_LWM2M_CLIENT_RESOURCE. Questa struttura contiene l'ID della risorsa o dell'istanza e il relativo valore.

Le funzioni seguenti vengono fornite per impostare le informazioni e il valore della risorsa.

| &nbsp;Nome funzione | Descrizione |
| --- | --- |
| ***nx_lwm2m_client_resource_info_set*** | Impostare informazioni sulle risorse: ID risorsa e operazione: lettura, scrittura, ESEGUIbile. |
| ***nx_lwm2m_client_resource_string_set*** | Impostare il valore della risorsa come stringa. |
| ***nx_lwm2m_client_resource_integer32_set*** | Impostare il valore della risorsa come intero a 32 bit. |
| ***nx_lwm2m_client_resource_integer64_set*** | Impostare il valore della risorsa come intero a 64 bit. |
| ***nx_lwm2m_client_resource_float32_set*** | Impostare il valore della risorsa come float a 32 bit. |
| ***nx_lwm2m_client_resource_float64_set*** | Impostare il valore della risorsa come float a 64 bit. |
| ***nx_lwm2m_client_resource_boolean_set*** | Impostare il valore della risorsa come valore booleano. |
| ***nx_lwm2m_client_resource_objlnk_set*** | Impostare il valore della risorsa come collegamento all'oggetto. |
| ***nx_lwm2m_client_resource_opaque_set*** | Impostare il valore della risorsa come opaco. |
| ***nx_lwm2m_client_resource_instance_set*** | Impostare il valore della risorsa come istanza di per più risorse. |
| ***nx_lwm2m_client_resource_dim_set*** | Impostare la dimensione della risorsa per più risorse per l'individuazione. |

Le funzioni seguenti vengono fornite per ottenere informazioni sulle risorse e valore.

| &nbsp;Nome funzione | Descrizione |
| --- | --- |
| ***nx_lwm2m_client_resource_info_get*** | Ottenere informazioni sulle risorse: ID risorsa e operazione: lettura, scrittura, ESEGUIbile. |
| ***nx_lwm2m_client_resource_string_get*** | Ottenere il valore di una risorsa di stringa. |
| ***nx_lwm2m_client_resource_integer32_get*** | Ottenere il valore di una risorsa Integer a 32 bit. |
| ***nx_lwm2m_client_resource_integer64_get*** | Ottenere il valore di una risorsa Integer a bit B4. |
| ***nx_lwm2m_client_resource_float32_get*** | Ottenere il valore di una risorsa float a 32 bit. |
| ***nx_lwm2m_client_resource_float64_get*** | Ottenere il valore di una risorsa float a 64 bit. |
| ***nx_lwm2m_client_resource_boolean_get*** | Ottenere il valore di una risorsa booleana. |
| ***nx_lwm2m_client_resource_objlnk_get*** | Ottenere il valore di una risorsa di collegamento a un oggetto. |
| ***nx_lwm2m_client_resource_opaque_get*** | Ottenere il valore di una risorsa opaca. |
| ***nx_lwm2m_client_resource_instance_get*** | Ottenere l'istanza della risorsa per più risorse. |
| ***nx_lwm2m_client_resource_dim_get*** | Ottenere la dimensione di risorsa per più risorse. |

## <a name="object-implementation"></a>Implementazione di oggetti

Il client LWM2M implementa gli oggetti LWM2M OMA obbligatori: Security (0), server (1), Access Control (2) e Device (3). Altri oggetti specifici del dispositivo devono essere implementati dall'applicazione.

Per definire un oggetto vengono usate due strutture di dati: la struttura NX_LWM2M_CLIENT_OBJECT definisce l'implementazione dell'oggetto, inclusi l'ID oggetto e i metodi dell'oggetto, e la struttura NX_LWM2M_CLIENT_OBJECT_INSTANCE contiene i dati di un'istanza dell'oggetto.

Sono disponibili le funzioni seguenti.

| &nbsp;Nome funzione | Descrizione |
| --- | --- |
| ***nx_lwm2m_client_object_add*** | Aggiungere l'implementazione dell'oggetto al client LwM2M. |
| ***nx_lwm2m_client_object_remove*** | Rimuovere l'implementazione dell'oggetto dal client LwM2M. |
| ***nx_lwm2m_client_object_instance_add*** | Aggiungere l'istanza dell'oggetto all'oggetto. |
| ***nx_lwm2m_client_object_instance_remove*** | Rimuovere l'istanza dell'oggetto dall'oggetto. |

La funzione di callback del metodo Object presenta la firma riportata di seguito.

```c
typedef UINT (*NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK)(
    UINT operation, 
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr,
    NX_LWM2M_CLIENT_RESOURCE *resource,
    UINT *resource_count,
    VOID *args_ptr,
    UINT args_length);
```

### <a name="the-read-method"></a>Metodo ' Read '

Il metodo ' Read ' viene usato per leggere i valori delle risorse da un'istanza dell'oggetto. I parametri sono definiti nel modo seguente.

| Parametro | Descrizione |
| --- | --- |
| **operation** | **NX_LWM2M_CLIENT_OBJECT_READ** |
| **object_ptr** | Puntatore all'implementazione dell'oggetto. |
| **instance_ptr** | Puntatore all'istanza dell'oggetto. |
| **risorse** | Puntatore a una matrice di **NX_LWM2M_CLIENT_RESOURCE** contenente gli ID delle risorse da leggere. In restituzione la matrice viene riempita con i tipi e i valori corrispondenti. |
| **resource_count** | Puntatore al numero di risorse da leggere. |
| **args_ptr** | Parametro non utilizzato per la lettura. |
| **args_length** | Parametro non utilizzato per la lettura. |

### <a name="the-discover-method"></a>Metodo ' Discover '

Il metodo ' Discover ' viene usato per recuperare l'elenco di tutte le risorse implementate da un oggetto. I parametri sono definiti nel modo seguente.

| Parametro | Descrizione |
| --- | --- |
| **operation** | **NX_LWM2M_CLIENT_OBJECT_DISCOVER** |
| **object_ptr** | Puntatore all'implementazione dell'oggetto. |
| **instance_ptr** | Puntatore all'istanza dell'oggetto. |
| **risorse** | Puntatore a una matrice di NX_LWM2M_CLIENT_RESOURCE. In restituzione la matrice viene riempita con le informazioni sulle risorse corrispondenti. |
| **resource_count** | Puntatore al numero di risorse da individuare. Al momento della restituzione, questo parametro deve essere aggiornato come valore true. |
| **args_ptr** | Parametro non utilizzato per l'individuazione. |
| **args_length** | Parametro non utilizzato per l'individuazione. |

### <a name="the-write-method"></a>Metodo ' Write '

Il metodo ' Write ' viene usato per aggiornare o sostituire le risorse di un'istanza dell'oggetto. I parametri sono definiti nel modo seguente.

| Parametro  | Descrizione |
| --- | --- |
| **operation** | **NX_LWM2M_CLIENT_OBJECT_WRITE** |
| **object_ptr** | Puntatore all'implementazione dell'oggetto. |
| **instance_ptr** | Puntatore all'istanza dell'oggetto. |
| **risorse** | Puntatore a una matrice di **NX_LWM2M_CLIENT_RESOURCE** contenente gli ID delle risorse da leggere. In restituzione la matrice viene riempita con i tipi e i valori corrispondenti. |
| **resource_count** | Puntatore al numero di risorse da individuare. |
| **args_ptr** | Scrivi flag. |
| **args_length** | Lunghezza degli argomenti. |

È possibile specificare le operazioni di scrittura seguenti per il parametro del *flag* .

| Operazione | Azione | Descrizione |
| --- | ---| --- |
| 0 | Aggiornamento parziale | Aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate le altre risorse esistenti.
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE** | Sostituisci istanza | Sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa specificati.
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE** |  Sostituisci risorsa | Sostituisce le risorse con i nuovi valori di risorsa forniti, usati per sostituire più risorse. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_CREATE** | creare un'istanza | Inizializza l'istanza dell'oggetto appena creata con i valori di risorsa forniti, chiamati dal metodo **_nx_lwm2m_object_create_** . |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP** | Scrittura bootstrap | Chiamato durante la sequenza di bootstrap. |

### <a name="the-execute-method"></a>Metodo ' Execute '

Il metodo ' Execute ' implementa l'esecuzione di una risorsa dell'oggetto.

I parametri di input sono definiti nel modo seguente.

| Parametro  | Descrizione |
| --- | --- |
| **operation** | NX_LWM2M_CLIENT_OBJECT_EXECUTE |
| **object_ptr** | Puntatore all'implementazione dell'oggetto. |
| **instance_ptr** | Puntatore all'istanza dell'oggetto. |
| **risorse** | Puntatore a una matrice di **NX_LWM2M_CLIENT_RESOURCE** contenente gli ID delle risorse da leggere. In restituzione la matrice viene riempita con i tipi e i valori corrispondenti. |
| **resource_count** | Puntatore al numero di risorse da individuare. |
| **args_ptr** | Puntatore agli argomenti. |
| **args_length** | Lunghezza degli argomenti.  |

La funzione deve restituire **NX_LWM2M_CLIENT_NOT_FOUND** se l'ID risorsa non esiste oppure **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** se non supporta l'esecuzione.

### <a name="the-create-method"></a>Metodo ' Create '

Il metodo ' Create ' implementa la creazione di una nuova istanza dell'oggetto.

I parametri di input sono definiti nel modo seguente.

| Parametro  | Descrizione |
| --- | --- |
| **operation** | **NX_LWM2M_CLIENT_OBJECT_CREATE** |
| **object_ptr** | Puntatore all'implementazione dell'oggetto. |
| **instance_ptr** | Parametro non utilizzato. |
| **risorse** | Puntatore a una matrice di **NX_LWM2M_CLIENT_RESOURCE** contenente gli ID delle risorse da leggere. In restituzione la matrice viene riempita con i tipi e i valori corrispondenti. |
| **resource_count** | Puntatore al numero di risorse da individuare. |
| **args_ptr** | ID istanza dell'oggetto. |
| **args_length** | Lunghezza degli argomenti. |

### <a name="the-delete-method"></a>Metodo ' Delete '

Il metodo ' Delete ' implementa l'eliminazione di un'istanza dell'oggetto, i parametri di input vengono definiti come indicato di seguito.

| Parametro  | Descrizione |
| --- | --- |
| **operation** | NX_LWM2M_CLIENT_OBJECT_DELETE |
| **object_ptr** | Puntatore all'implementazione dell'oggetto. |
| **instance_ptr** | Puntatore all'istanza dell'oggetto. |
| **risorse** | Parametro non utilizzato. |
| **resource_count** | Parametro non utilizzato. |
| **args_ptr** | Parametro non utilizzato. |
| **args_length** | Parametro non utilizzato. |

In caso di esito positivo, l'oggetto deve rilasciare i dati dell'istanza dell'oggetto e qualsiasi altra risorsa allocata dall'istanza.

## <a name="example-of-lwm2m-client-application"></a>Esempio di applicazione client LWM2M

Il codice seguente è un esempio di una semplice applicazione client LWM2M che implementa un dispositivo personalizzato costituito da un sensore di temperatura e da un Commuter leggero.

Il dispositivo consente a un server di leggere il valore del sensore di temperatura e lo stato booleano del Commuter e di impostare lo switch di luce su on/off.

```c
#include "nx_lwm2m_client.h"


/* Custom Object implementation. */

/* Temperature Object ID and resource IDs. */
#define IPSO_TEMPERATURE_OBJECT_ID   3303

#define IPSO_RESOURCE_MIN_VALUE      5601
#define IPSO_RESOURCE_MAX_VALUE      5602
#define IPSO_RESOURCE_RESET_MINMAX   5605
#define IPSO_RESOURCE_VALUE          5700
#define IPSO_RESOURCE_UNITS          5701

/* Actuation Object ID and resource IDs. */
#define IPSO_ACTUATION_OBJECT_ID     3306

#define IPSO_RESOURCE_ONOFF          5850

/* Define the Temperature Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_CLIENT_OBJECT_INSTANCE    object_instance;

    /* Resources Data */
    NX_LWM2M_FLOAT32                   temperature;
    NX_LWM2M_FLOAT32                   min_temperature;
    NX_LWM2M_FLOAT32                   max_temperature;

} IPSO_TEMPERATURE_INSTANCE;

/* Define the Actuation Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_CLIENT_OBJECT_INSTANCE    object_instance;

    /* Resources Data */
    NX_LWM2M_BOOL                      onoff;

} IPSO_ACTUATION_INSTANCE;

/* IPSO Temperature */
/* Define the 'Read' Method */
UINT ipso_temperature_read(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count)
{
IPSO_TEMPERATURE_INSTANCE *temp = ((IPSO_TEMPERATURE_INSTANCE *) instance_ptr);
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_MIN_VALUE:

            /* return the minimum measured temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> min_temperature);
            break;

        case IPSO_RESOURCE_MAX_VALUE:

            /* return the maximum measured temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> max_temperature);
            break;

        case IPSO_RESOURCE_VALUE:

            /* return the temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> temperature);
            break;

        case IPSO_RESOURCE_RESET_MINMAX:

            /* Not readable */
            return(NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED);

        case IPSO_RESOURCE_UNITS:

            /* return the temperature units */
            nx_lwm2m_client_resource_string_set(&resource[i], "Cel", 3);
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}

/* Define the 'Discover' method */
UINT ipso_temperature_discover(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resources, UINT *resource_count)
{
    if (*resource_count < 5)
    {
        return(NX_LWM2M_CLIENT_BUFFER_TOO_SMALL);
    }

    /* return the list of supported resources IDs */
    *resource_count = 5;
    nx_lwm2m_client_resource_info_set(&resources[0], IPSO_RESOURCE_MIN_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[1], IPSO_RESOURCE_MAX_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[2], IPSO_RESOURCE_RESET_MINMAX, NX_LWM2M_CLIENT_RESOURCE_OPERATION_EXECUTABLE);
    nx_lwm2m_client_resource_info_set(&resources[3], IPSO_RESOURCE_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[4], IPSO_RESOURCE_UNITS, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);

    return(NX_SUCCESS);
}

/* Define the 'Execute' method */
UINT ipso_temperature_execute(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, const CHAR *args_ptr, UINT args_length)
{
IPSO_TEMPERATURE_INSTANCE *temp = ((IPSO_TEMPERATURE_INSTANCE *) instance_ptr);
NX_LWM2M_CLIENT_RESOURCE value;
NX_LWM2M_ID resource_id;

    /* Get resource id */
    nx_lwm2m_client_resource_info_get(resource, &resource_id, NX_NULL);

    switch (resource_id)
    {

    case IPSO_RESOURCE_MIN_VALUE:
    case IPSO_RESOURCE_MAX_VALUE:
    case IPSO_RESOURCE_VALUE:
    case IPSO_RESOURCE_UNITS:

        /* read-only resource */
        return(NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED);

    case IPSO_RESOURCE_RESET_MINMAX:

        /* reset min/max values to current temperature */
        nx_lwm2m_client_resource_float32_set(&value, temp -> temperature);
        if (temp -> min_temperature != temp -> temperature)
        {
            temp -> min_temperature = temp -> temperature;
            nx_lwm2m_client_resource_info_set(&value, IPSO_RESOURCE_MIN_VALUE, NX_NULL);
            nx_lwm2m_client_object_resource_changed(object_ptr, instance_ptr, &value);
        }
        if (temp -> max_temperature != temp -> temperature)
        {
            temp -> max_temperature = temp -> temperature;
            nx_lwm2m_client_resource_info_set(&value, IPSO_RESOURCE_MAX_VALUE, NX_NULL);
            nx_lwm2m_client_object_resource_changed(object_ptr, instance_ptr, &value);
        }

        break;

    default:

        /* unknown resource ID */
        return(NX_LWM2M_CLIENT_NOT_FOUND);
    }

    return(NX_SUCCESS);
}

/* Define the operation callback function of Temperature Object */
UINT ipso_temperature_operation(UINT operation, NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT *resource_count, VOID *args_ptr, UINT args_length)
{

    switch (operation)
    {
    case NX_LWM2M_CLIENT_OBJECT_READ:

        /* Call read function */
        return ipso_temperature_read(object_ptr, object_instance_ptr, resource, *resource_count);
    case NX_LWM2M_CLIENT_OBJECT_DISCOVER:

        /* Call discover function */
        return ipso_temperature_discover(object_ptr, object_instance_ptr, resource, resource_count);

    case NX_LWM2M_CLIENT_OBJECT_EXECUTE:

        /* Call execute function */
        return ipso_temperature_execute(object_ptr, object_instance_ptr, resource, args_ptr, args_length);
    default:

        /*Unsupported operation */
        return(NX_LWM2M_CLIENT_NOT_SUPPORTED);
    }
}


/* IPSO Actuation */
/* Define the 'Read' Method */
UINT ipso_actuation_read(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count)
{
IPSO_ACTUATION_INSTANCE *act = ((IPSO_ACTUATION_INSTANCE *) instance_ptr);
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_ONOFF:

            /* return the on/off value */
            nx_lwm2m_client_resource_boolean_set(&resource[i], act -> onoff);
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}


/* Define the 'Discover' method */
UINT ipso_actuation_discover(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resources, UINT *resource_count)
{
    if (*resource_count < 1)
    {
        return(NX_LWM2M_CLIENT_BUFFER_TOO_SMALL);
    }

    /* return the list of supported resources IDs */
    *resource_count = 1;
    nx_lwm2m_client_resource_info_set(&resources[0], IPSO_RESOURCE_ONOFF, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ_WRITE);

    return(NX_SUCCESS);
}

/* Define the 'Write' method */
UINT ipso_actuation_write(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count, UINT flags)
{
IPSO_ACTUATION_INSTANCE *act = ((IPSO_ACTUATION_INSTANCE *) instance_ptr);
UINT ret;
NX_LWM2M_BOOL onoff;
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_ONOFF:

            /* assign on/off boolean value */
            ret = nx_lwm2m_client_resource_boolean_get(&resource[i], &onoff);
            if (ret != NX_SUCCESS)
            {
                /* invalid value type */
                return(ret);
            }
            if (onoff != act->onoff)
            {
                act->onoff = onoff;

                printf("Set actuation switch %s\n", onoff ? "On" : "Off");
            }
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}

/* Define the operation callback function of Actuation Object */
UINT ipso_actuation_operation(UINT operation, NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT *resource_count, VOID *args_ptr, UINT args_length)
{
UINT write_op;

    switch (operation)
    {
    case NX_LWM2M_CLIENT_OBJECT_READ:

        /* Call read function */
        return ipso_actuation_read(object_ptr, object_instance_ptr, resource, *resource_count);
    case NX_LWM2M_CLIENT_OBJECT_DISCOVER:

        /* Call discover function */
        return ipso_actuation_discover(object_ptr, object_instance_ptr, resource, resource_count);
    case NX_LWM2M_CLIENT_OBJECT_WRITE:

        /* Get the type of write operation */
        write_op = *(UINT *)args_ptr;

        /* Call write function */
        return ipso_actuation_write(object_ptr, object_instance_ptr, resource, *resource_count, write_op);
    default:

        /* Unsupported operation */
        return(NX_LWM2M_CLIENT_NOT_SUPPORTED);
    }
}


/* NetX data.  */
NX_IP                   ip_0;
NX_PACKET_POOL          pool_0;

/* LWM2M Client data.  */
NX_LWM2M_CLIENT         client;
ULONG                   client_stack[4096 / sizeof(ULONG)];
NX_LWM2M_CLIENT_SESSION session;

/* Objects and instances.  */
NX_LWM2M_CLIENT_OBJECT      temperature_object;
NX_LWM2M_CLIENT_OBJECT      actuation_object;
IPSO_TEMPERATURE_INSTANCE   temperature_instance;
IPSO_ACTUATION_INSTANCE     actuation_instance;

/* Define the session state callback */
void session_callback(NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state)
{
    printf("LWM2M Callback: -> %d\n", state);

    switch (state)
    {

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING:

        printf("Start client initiated bootstrap\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED:

        printf("Got message from boostrap server\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:

         /* Bootstrap session done, we can register to the LWM2M Server */
        printf( "Boostrap finished.\n");
#ifdef BOOTSTRAP
        tx_semaphore_put(&semaphore_bootstarp_finish);
#endif
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:

        /* Failed to Bootstrap the LWM2M Client. */
        printf( "Failed to boostrap device, error=%02x\n", nx_lwm2m_client_session_error_get(session_ptr));
        break;

    case NX_LWM2M_CLIENT_SESSION_REGISTERED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device registered.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_DISABLED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device disabled.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_DEREGISTERED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device deregistered.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_ERROR:

        /* Failed to register to the LWM2M Client. */
        printf( "Failed to register device, error=%02x\n", nx_lwm2m_client_session_error_get(session_ptr));
        break;
    }
}


/* Application main thread */
void application_thread(ULONG info)
{

UINT status;
NX_LWM2M_ID server_id = 0;
NXD_ADDRESS server_addr;
CHAR *server_uri = NX_NULL;
UINT server_uri_len = 0;
UCHAR security_mode = 0;
   
    /* Create the LWM2M client */
    status = nx_lwm2m_client_create(&client, &ip_0, &pool_0, "nxlwm2mclient", sizeof("nxlwm2mclient") - 1, NX_NULL, 0, NX_LWM2M_CLIENT_BINDING_U, client_stack, sizeof(client_stack), 4);
    if (status)
    {
        return;
    }

    /* Define our custom objects: */
    /* Add Temperature Object */
    status = nx_lwm2m_client_object_add(&client, &temperature_object, IPSO_TEMPERATURE_OBJECT_ID, ipso_temperature_operation);
    if (status)
    {
        return;
    }

    /* Define a single instance */
    temperature_instance.temperature = 22.5f;
    temperature_instance.min_temperature = temperature_instance.temperature;
    temperature_instance.max_temperature = temperature_instance.temperature;
    status = nx_lwm2m_client_object_instance_add(&temperature_object, &temperature_instance.object_instance, NX_NULL);
    if (status)
    {
        return;
    }

    /* Add Actuation Object */
    status = nx_lwm2m_client_object_add(&client, &actuation_object, IPSO_ACTUATION_OBJECT_ID, ipso_actuation_operation);
    if (status)
    {
        return;
    }

    /* Define a single instance */
    actuation_instance.onoff = NX_FALSE;
    status = nx_lwm2m_client_object_instance_add(&actuation_object, &actuation_instance.object_instance, NX_NULL);
    if (status)
    {
        return;
    }

    /* Create a session */
    status = nx_lwm2m_client_session_create(&session, &client, session_callback);
    if (status)
    {
        return;
}

    /* Set bootstrap server address.  */
    server_addr.nxd_ip_version = NX_IP_VERSION_V4;
    server_addr.nxd_ip_address.v4 = IP_ADDRESS(23, 97, 187, 154);

    printf("Start boostraping\r\n");
    status = nx_lwm2m_client_session_bootstrap(&session, 0, &server_addr, 5783);
    if (status)
    {
        return;
    }

    status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_len, &security_mode, NX_NULL, NX_NULL, NX_NULL, NX_NULL, NX_NULL, NX_NULL);
    if (status || (security_mode != NX_LWM2M_CLIENT_SECURITY_MODE_NOSEC))
    {
        return;
    }

printf("Register to LWM2M server\r\n");
status = nx_lwm2m_client_session_register(&session, server_id, &server_addr, 5683);

    if (status)
    {
        return;
    }

    /* Application main loop */
    while (1)
    {

        /* application code... */
        tx_thread_sleep(NX_IP_PERIODIC_RATE);
    }

    /* Terminate the LWM2M Client */
    nx_lwm2m_client_delete(&client);
}

```