---
title: Capitolo 3-Descrizione dei servizi client di Azure RTO NetX Duo MQTT
description: Questo capitolo contiene una descrizione di tutti i servizi client NetX Duo MQTT (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9cbb65946c45bfbc476091f7c604346e839a42fc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821800"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-mqtt-client-services"></a>Capitolo 3-Descrizione dei servizi client di Azure RTO NetX Duo MQTT

Questo capitolo contiene una descrizione di tutti i servizi client di Azure RTO NetX Duo MQTT (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nxd_mqtt_client_create** *creare un'istanza del client MQTT*
- **nxd_mqtt_client_will_message_set** *impostare il messaggio*
- **nxd_mqtt_client_client_login_set** *impostare il nome utente e la password di accesso client MQTT*
- **nxd_mqtt_client_connect** *connettere il client MQTT al broker*
- **nxd_mqtt_client_secure_connect** *connettere il client MQTT al broker con sicurezza TLS*
- **nxd_mqtt_client_publish** *pubblicare un messaggio tramite Service Broker.*
- **nxd_mqtt_client_subscribe** *sottoscrivere un argomento*
- **nxd_mqtt_client_unsubscribe** *annullare la sottoscrizione a un argomento*
- **nxd_mqtt_client_receive_notify_set** *impostare la funzione di callback di ricezione notifiche messaggio MQTT*
- **nxd_mqtt_client_message_get** *recuperare un messaggio dal broker*
- **nxd_mqtt_client_disconnect_notify_set** *impostare la funzione di callback Notify DISconnessione messaggio MQTT*
- **nxd_mqtt_client_disconnect** *disconnettere il client MQTT dal broker*
- **nxd_mqtt_client_delete** *eliminare l'istanza del client MQTT*

## <a name="nxd_mqtt_client_create"></a>nxd_mqtt_client_create

Creare un'istanza del client MQTT

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_create(NXD_MQTT_CLIENT *client_ptr,
    CHAR *client_name, CHAR *client_id,
    UINT client_id_length, NX_IP *ip_ptr, NX_PACKET_POOL
    *pool_ptr, VOID *stack_ptr, ULONG stack_size, UINT
    mqtt_thread_priority,
    VOID *memory_ptr, ULONG memory_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client MQTT nell'istanza IP specificata. La stringa *client_id* viene passata al server durante la fase di connessione MQTT come *identificatore client (ClientID)*. Vengono inoltre create le risorse ThreadX necessarie (thread attività del client MQTT, mutex, gruppo di flag di evento e socket TCP).

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **client_name** Stringa del nome del client.
- **client_id** Stringa ID client utilizzata durante la fase di connessione. MQTT broker Usa questa client_id per identificare in modo univoco un client.
- **client_id_length** Lunghezza della stringa dell'ID client, in byte.
- **ip_ptr** Puntatore all'istanza IP.
- **pool_ptr** Puntatore a un pool di pacchetti utilizzato dal client MQTT per il relativo funzionamento.
- **stack_ptr** Area dello stack per il thread del client MQTT.
- **stack_size** Dimensioni dell'area dello stack, in byte.
- **mqtt_thread_priority** Priorità del thread MQTT.
- **memory_ptr** Deprecato. Non più utilizzato.
- **memory_size** Deprecato. Non più utilizzato.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) ha creato il client MQTT.
- Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)
- NX_PTR_ERROR (0x07): blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti non validi.
- NXD_MQTT_INVALID_PARAMETER (0x10009) argomento non valido, will_retrain_flag o will_QoS valore.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
#define CLIENT_ID_STRING "My Test Client"

#define MQTT_THREAD_PRIORITY 2

NXD_MQTT_CLIENT my_client;
NX_IP ip_0; /* Assume ip_0 is created prior to MQTT client creation. */
NX_PACKET_POOL pool_0;/* Assume pool_0 is created prior to MQTT client creation. */
UCHAR mqtt_thread_stack[STACK_SIZE];

/* Create the MQTT Client instance on "ip_0". */
status = **nxd_mqtt_client_create**(&my_client, "my client",
    CLIENT_ID_STRING, stlren(CLIENT_ID_STRING),
    &ip_0, &pool_0, (VOID*)mqtt_thread_stack, STACK_SIZE,
    MQTT_THREAD_PRIORITY, NX_NULL, 0);

/* If status is NXD_MQTT_SUCCESS an MQTT Client instance was successfully created. */
```

## <a name="nxd_mqtt_client_will_message_set"></a>nxd_mqtt_client_will_message_set

Imposta il messaggio di messaggio

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_will_message_set(NXD_MQTT_CLIENT
    *client_ptr,
    Const UCHAR *will_topic,
    UINT will_topic_length
    Const UCHAR *will_message,
    UINT will_message_length,
    UINT will_retain_flag,
    UINT will_QoS);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'argomento facoltativo di e messaggio prima che il client si connetta al server. L'argomento deve essere una stringa con codifica UTF-8.

Il messaggio, se impostato, verrà trasmesso al broker come parte del messaggio CONNECT. Per questo motivo, l'applicazione che vuole usare il messaggio deve usare questo servizio prima di eseguire la connessione MQTT.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **will_topic** La stringa dell'argomento con codifica UTF-8. È necessario che l'argomento sia presente. Il chiamante deve contenere la stringa will_topic valida fino a quando non viene effettuata la chiamata *nx_mqtt_client_connect* .
- **will_topic_length** Numero di byte nella stringa dell'argomento della funzione
- **will_message** Messaggio definito dall'applicazione. Se il messaggio non è necessario, l'applicazione può impostare questo campo su *NX_NULL.*
- **will_message_length** Numero di byte nella stringa del messaggio di messaggio. Se will_message è impostato su NULL, will_message_length deve essere impostato su 0.
- **will_retain_flag** Indica se il server pubblica il messaggio come messaggio mantenuto. I valori validi sono *NX_TRUE* o *NX_FALSE.*
- **will_QoS** Valore QoS utilizzato dal server quando viene inviato un messaggio. I valori validi sono 0 o 1.  

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) imposta correttamente il messaggio di messaggio.
- I messaggi QoS di livello 2 **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) non sono supportati.
- NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido.
- NXD_MQTT_INVALID_PARAMETER (0x10009) argomento non valido, will_retrain_flag o will_QoS valore.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
#define WILL_TOPIC "my_will_topic"

#define WILL_MESSAGE "my will message"

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_will_message_set(&my_client,
    WILL_TOPIC, STRLEN(WILL_TOPIC),
    WILL_MESSAGE, STRLEN(WILL_MESSAGE),
    NX_TRUE, 0);

/* If status is NXD_MQTT_SUCCESS the will message is properly
configured for the session. It will be transmitted to the server
during MQTT connection. */
```

## <a name="nxd_mqtt_client_login_set"></a>nxd_mqtt_client_login_set

Imposta il nome utente e la password di accesso client MQTT

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_login_set(NXD_MQTT_CLIENT *client_ptr,
    Const UCHAR *username,
    UINT username_length
    Const UCHAR *password,
    UINT password_length);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il nome utente e la password, che viene usato durante la fase di connessione MQTT per lo scopo di autenticazione log.

L'account di accesso del client MQTT con nome utente e password è facoltativo. Nelle situazioni in cui il server richiede un nome utente e una password, il nome utente e la password devono essere impostati prima che venga stabilita la connessione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **nome utente** Stringa del nome utente con codifica UTF-8. Il chiamante deve lasciare valida la stringa del nome utente fino a quando non viene effettuata la chiamata *nx_mqtt_client_connect* .
- **username_length** Numero di byte nella stringa del nome utente
- **password** di Stringa password. Se la password non è obbligatoria, questo campo può essere impostato su NX_NULL.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) imposta correttamente il messaggio di messaggio.
- NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido.
- NXD_MQTT_INVALID_PARAMETER (0x10009) stringa nome utente non valida o stringa password.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
#define USERNAME "MY_NAME"

#define PASSWORD "MY_LOGIN_SECRET"

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_login_set(&my_client,
    USERNAME, STRLEN(USERNAME),
    PASSWORD, STRLEN(PASSWORD));

/* If status is NXD_MQTT_SUCCESS the username and the password 
are set for the session. This information will be 
transmitted to the server during MQTT connection. */
```

## <a name="nxd_mqtt_client_connect"></a>nxd_mqtt_client_connect

Connettere il client di MQTT al broker

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_connect(NXD_MQTT_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT keepalive, UINT clean_session, ULONG wait_option));
```

### <a name="description"></a>Descrizione

Questo servizio avvia una connessione al broker. Innanzitutto associa un socket TCP, quindi crea una connessione TCP. Supponendo che abbia esito positivo, viene creato un timer se è abilitata la funzionalità MQTT Keep Alive. Quindi si connette al server MQTT (Broker).

Si noti che questo servizio crea una connessione MQTT senza protezione TLS. Per creare una connessione MQTT protetta, è necessario che l'applicazione utilizzi il servizio ***nxd_mqtt_client_secure_connect ().***

Al momento della connessione, se il client imposta il *clean_session* su NX_FALSE, il client ritrasmette tutti i messaggi archiviati che non sono ancora stati riconosciuti.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **server_ip** Indirizzo IP broker.
- **SERVER_PORT** Numero di porta del broker. La porta predefinita per MQTT è definita come **_NXD_MQTT_PORT_** (1883).
- **keep_alive** Valore Keep-Alive, in secondi, da utilizzare durante la sessione. Il valore indica il tempo massimo tra due messaggi di controllo MQTT inviati al broker prima del timeout del client da parte del broker. Il valore 0 disattiva la funzionalità Keep-Alive.
- **clean_session** Indica se il server deve avviare la sessione pulita. Le opzioni valide sono **_NX_TRUE_*_ o _*_NX_FALSE._**
- **WAIT_OPTION** Tempo di attesa della connessione.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) connessione MQTT riuscita
- **NXD_MQTT_ALREADY_CONNECTED** (0X10001) il client è già connesso al broker.
- **NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT 
- Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)
- **NXD_MQTT_CONNECT_FAILURE** (0X10005) non è riuscito a connettersi al broker.
- **NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è in grado di inviare messaggi al broker.
- Il server **NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) ha risposto con errore
- Codice di risposta del server **NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081)
- Codice di risposta del server **NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082)
- Codice di risposta del server **NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083)
- Codice di risposta del server **NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084)
- Codice di risposta del server **NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085)
- NX_PTR_ERROR (0x07) non valido: blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NXD_ADDRESS broker_address;

/* Set up broker IP address */
broker_address.nxd_ip_version = 4;
broker_address.nxd_ip_address.v4 = MQTT_BROKER_ADDRESS;

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_connect(&my_client, &broker_address,
    NXD_MQTT_PORT,
    0, /* Turn off keepalive */
    NX_TRUE, /* Clean session flag set */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS a connection to the broker is successfully established. */
```

## <a name="nxd_mqtt_client_secure_connect"></a>nxd_mqtt_client_secure_connect

Connettere il client di MQTT al broker con sicurezza TLS

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_secure_connect(NXD_MQTT_CLIENT
    *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT (*tls_setup)(NXD_MQTT_CLIENT *,
        NX_SECURE_TLS_SESISON *,
        NX_SECURE_TLS_CERTIFICATE *,
        NX_SECURE_TLS_CERTIFICATE *),
    UINT keepalive, UINT connection_flag,
    UINT clean_session, ULONG wait_option));
```

### <a name="description"></a>Descrizione

Questo servizio è identico a ***nxd_mqtt_client_connect*** ad eccezione del fatto che la connessione passa attraverso il livello TLS anziché TCP. Pertanto, la comunicazione tra il client e il broker è protetta.

Il *tls_setup* definito dall'utente è una funzione di callback utilizzata dal client di MQTT prima di eseguire una connessione client MQTT. L'applicazione deve inizializzare NetX Secure TLS, configurare i parametri di sicurezza e caricare i certificati rilevanti da usare durante l'handshake TLS. L'handshake TLS effettivo si verifica dopo che è stata stabilita una connessione TCP sulla porta TLS MQTT del broker (porta TCP predefinita 8883). Una volta che l'handshake TLS ha avuto esito positivo, il pacchetto di controllo MQTT CONNECT viene inviato tramite TLS.

Per stabilire connessioni sicure, è necessario che sia disponibile la libreria NetX Secure TLS e che il client NetX Duo MQTT sia compilato con ***NX_SECURE_ENABLE*** definito.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **server_ip** Indirizzo IP broker.
- **SERVER_PORT** Numero di porta del broker. La porta predefinita per MQTT è definita come **_NXD_MQTT_TLS_PORT_** (8883).
- **tls_setup** Funzione di callback di configurazione TLS fornita dall'utente. Questa funzione di callback viene richiamata per configurare i parametri di connessione del client TLS.
- **keep_alive** Valore Keep-Alive da utilizzare durante la sessione. Il valore 0 disattiva la funzionalità Keep-Alive.
- **clean_session** Indica se il server deve avviare la sessione pulita. Le opzioni valide sono **_NX_TRUE_*_ o _*_NX_FALSE._**
- **WAIT_OPTION** Tempo di attesa della connessione.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) connessione client MQTT riuscita stabilita tramite TLS.
- **NXD_MQTT_ALREADY_CONNECTED** (0X10001) il client è già connesso al broker.
- **NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT 
- Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)
- **NXD_MQTT_CONNECT_FAILURE** (0X10005) non è riuscito a connettersi al broker.
- **NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è in grado di inviare messaggi al broker.
- Il server **NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) ha risposto con un messaggio di errore.
- Codice di risposta del server **NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081)
- Codice di risposta del server **NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082)
- Codice di risposta del server **NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083)
- Codice di risposta del server **NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084)
- Codice di risposta del server **NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085)
- NX_PTR_ERROR (0x07) non valido per il blocco di controllo MQTT o la struttura di indirizzi del server.
- La porta del server NX_INVALID_PORT (0x46) non può essere 0.
- Errore del parametro di input NXD_MQTT_INVALID_PARAMETER (0x10009)
- Il thread MQTT di NXD_MQTT_CLIENT_NOT_RUNNING (0x1000E) non è ancora stato avviato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* TLS setup routine. This function is responsible for setting up TLS parameters.*/
UINT tls_setup_callback(NXD_MQTT_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certificate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_certificate,
    UINT timeout)
{
/* Note this routine is simplified to highlight the
necessary steps to setup a TLS session. Each
application may employ different procedures suitable for
its TLS settings, such as cipher suite, certificates. */

/* Create a TLS session for the MQTT connection, and pass
in various crypto methods this session can use for the
initial TLS handshake. */

/* Load appropriate certificates, or set up session key for Pre-share key operation. */

/* Start the TLS session */

/* Return NX_SUCCESS if the TLS session is established. */
    return(NX_SUCCESS);
}

NXD_ADDRESS broker_address;

/* Set up broker IP address */
broker_address.nxd_ip_version = 4;
broker_address.nxd_ip_address.v4 = MQTT_BROKER_ADDRESS;

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_secure_connect(&my_client,
    &server_address, NXD_MQTT_TLS_PORT, tls_setup_callback,
    0, /* Turn off keepalive */
    NX_TRUE, /* Clean session set */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS the MQTT Client was successfully connected to the broker via TLS. */
```

## <a name="nxd_mqtt_client_publish"></a>nxd_mqtt_client_publish

Pubblicare un messaggio tramite Service Broker

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_publish(NXD_MQTT_CLIENT *client_ptr,
    CHAR *topic_name, UINT topic_name_length, CHAR *message, UINT
    message_length,
    UINT retain, UINT QoS, ULONG timeout);
```

### <a name="description"></a>Descrizione

Questo servizio pubblica un messaggio tramite Service Broker. La pubblicazione di messaggi di livello 2 QoS non è ancora supportata.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **topic_name** Argomento in cui pubblicare.
- **topic_name_length** Lunghezza dell'argomento in byte.
- **messaggio** di Puntatore al buffer dei messaggi.
- **message_length** Dimensioni del messaggio, in byte
- **Mantieni** Determina se il broker deve conservare il messaggio.
- **QoS** Valore QoS desiderato: 0 o 1.
- **timeout** Valore di timeout

### <a name="return-values"></a>Valori restituiti

- Creazione di un client MQTT riuscito **NXD_MQTT_SUCCESS** (0x00)
- Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004).
- **NXD_MQTT_PACKET_POOL_FAILURE** (0X10006) non è riuscito a ottenere il pacchetto dal pool di pacchetti.
- **NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è riuscito a comunicare con Service Broker.
- I messaggi QoS di livello 2 **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) non sono supportati.
- NX_PTR_ERROR (0x07) non valido: blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti
- Errore del parametro di input NXD_MQTT_INVALID_PARAMETER (0x10009)

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
CHAR *topic = "temperature";
CHAR *message = "100";

/* Publish the temperature value. */
status = nxd_mqtt_client_publish(&my_client,
    topic, STRLEN(topic),
    message, STRLEN(message),
    NX_TRUE, /* Server retains message. */);
    0, /* QOS */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS the message has been 
successfully sent to the broker. */
```

## <a name="nxd_mqtt_client_subscribe"></a>nxd_mqtt_client_subscribe

Sottoscrivere un argomento

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_subscribe(NXD_MQTT_CLIENT
    *mqtt_client_ptr, CHAR *topic_name,
    UINT topic_name_length, UINT QoS);
```

### <a name="description"></a>Descrizione

Questo servizio sottoscrive un argomento specifico. La sottoscrizione a messaggi QoS di livello 2 non è ancora supportata.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **topic_name** Argomento in cui pubblicare.
- **topic_name_length** Lunghezza dell'argomento in byte.
- **QoS il livello QoS desiderato:** 0 o 1.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) ha eseguito la sottoscrizione all'argomento.
- **NXD_MQTT_NOT_CONNECTED** (0X10002) il client non è connesso al broker.
- **NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT
- Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)
- **NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è in grado di inviare messaggi al broker.
- Il livello QoS di **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) 2messages non è supportato.
- NX_PTR_ERROR (0x07) non valido: blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti
- Il topic_name NXD_MQTT_INVALID_PARAMETER (0x10009) non è impostato oppure topic_name_length è zero oppure il valore QoS è non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Subscribe to the topic "temperature" with QoS level 0 */
CHAR *topic = "temperature";

status = nxd_mqtt_client_subscribe(&my_client, topic,
    STRLEN(topic), 0);

/* If status is NXD_MQTT_SUCCESS, the client successfully
subscribes to the topic "temperate". At this point the client
is ready for receiving messages from the broker. */
```

## <a name="nxd_mqtt_client_unsubscribe"></a>nxd_mqtt_client_unsubscribe

Annulla sottoscrizione da un argomento

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_unsubscribe(NXD_MQTT_CLIENT
    *mqtt_client_pr,
    CHAR *topic_name,
    UINT topic_name_length);
```

### <a name="description"></a>Descrizione

Questo servizio annulla la sottoscrizione da un argomento.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **topic_name** Argomento da cui annullare la sottoscrizione.
- **topic_name_length** Lunghezza dell'argomento in byte.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) ha annullato la sottoscrizione dall'argomento.
- **NXD_MQTT_NOT_CONNECTED** (0X10002) il client non è connesso al broker.
- **NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT.
- Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)
- **NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è in grado di inviare messaggi al broker.
- NX_PTR_ERROR (0x07) non valido puntatore a blocco di controllo MQTT
- Il topic_name NXD_MQTT_INVALID_PARAMETER (0x10009) non è impostato oppure topic_name_length è zero.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Subscribe to the topic "temperature" with QoS level 0 */
CHAR *topic = "temperature";

status = nxd_mqtt_client_unsubscribe(&my_client, topic,
    STRLEN(topic));

/* If status is NXD_MQTT_SUCCESS, the client successfully
unsubscribes the topic "temperate". */
```

## <a name="nxd_mqtt_client_receive_notify_set"></a>nxd_mqtt_client_receive_notify_set

Impostare la funzione di callback di ricezione notifiche messaggio MQTT

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_receive_notify_set(NXD_MQTT_CLIENT
    *client_ptr,
    VOID(*receive_notify)(NXD_MQTT_CLIENT* client_ptr,
    UINT message_count));
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback con il client MQTT. Al momento della ricezione di un messaggio pubblicato dal broker, il client MQTT archivia il messaggio nella coda di ricezione. Se la funzione di callback è impostata, la funzione di callback viene richiamata per notificare all'applicazione che un messaggio è pronto per essere recuperato. La funzione receive Notify accetta un puntatore al blocco di controllo client di MQTT e un *message_count* indicante il numero di messaggi disponibili nella coda di ricezione. Si noti che il numero può variare tra la notifica di ricezione e quando l'applicazione recupera questi messaggi, perché i nuovi messaggi possono essere arrivati nell'intervallo.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **receive_notify** Funzione di callback fornita dall'utente da richiamare alla ricezione di un messaggio.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) ha impostato correttamente la funzione receive Notify.
- NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Sample MQTT receive notify function. */

VOID my_notify_func(NXD_MQTT_CLIENT* client_ptr,
    UINT message_count)
{

/* On receiving a message, set an event flag to wake up the
application thread. The message will be received and
processed in the application thread. */
tx_event_flags_set(&mqtt_app_flag,
    MESSAGE_RECEIVED_EVENT, TX_OR);

/* All done. Return to the caller. */
    return;
}

/* Set the receive callback function. */
status = **nxd_mqtt_client_receive_notify_set**(&my_client,
    my_notify_func);

/* If status is NXD_MQTT_SUCCESS the notify function is properly set. */
```

## <a name="nxd_mqtt_client_message_get"></a>nxd_mqtt_client_message_get

Recuperare un messaggio dal broker

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_message_get(NXD_MQTT_CLIENT
    *client_ptr,
    UCHAR *topic_buffer, UINT topic_buffer_size,
    UINT *actual_topic_length, UCHAR *message_buffer,
    UINT message_buffer_size, UINT *actual_message_length);
```

### <a name="description"></a>Descrizione

Questo servizio recupera un messaggio pubblicato dal broker. Tutti i messaggi in arrivo vengono archiviati nella coda di ricezione. L'applicazione utilizza questo servizio per recuperare questi messaggi. Questa chiamata non è bloccata. Se la coda di ricezione è vuota, il servizio restituisce ***NXD_MQTT_NO_MESSAGE** _. Un'applicazione che desidera ricevere notifiche del messaggio in arrivo può chiamare il servizio _ *_nxd_mqtt_client_receive_notify_set_** per registrare una funzione di callback di ricezione.

Il chiamante deve fornire spazio di memoria per la stringa dell'argomento e il corpo del messaggio. Le dimensioni di questi due buffer vengono passate usando *topic_buffer_size* e *message_buffer_size*. Il numero effettivo di byte nella stringa dell'argomento e il corpo del messaggio vengono restituiti in *actual_topic_length* e *actual_message_length*. Se la lunghezza dell'argomento o la lunghezza del massaggio è maggiore dello spazio del buffer specificato, il servizio restituisce il codice di errore *NXD_MQTT_INSUFFICIENT_BUFFER_SIZE*.

L'applicazione deve allocare un buffer più grande e riprovare.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **topic_buffer** Puntatore alla posizione di memoria in cui viene copiata la stringa dell'argomento.
- **topic_buffer_size** Dimensioni del buffer dell'argomento.
- **actual_topic_length** Puntatore alla posizione di memoria in cui viene restituita la lunghezza effettiva dell'argomento.
- **message_buffer** Puntatore alla posizione di memoria in cui viene copiata la stringa del messaggio.
- **message_buffer_size** Dimensioni del buffer dei messaggi.
- **actual_message_length** Puntatore alla posizione di memoria in cui viene restituita la lunghezza del messaggio.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) ha recuperato correttamente il messaggio.
- Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)
- **NXD_MQTT_NO_MESSAGE** (0X1000A) la coda di ricezione è vuota.
- Il buffer dell'argomento di **NXD_MQTT_INSUFFICIENT_BUFFER_SIZE** (0x1000D) o il buffer dei messaggi è troppo piccolo per l'argomento o per il messaggio.
- NX_PTR_ERROR (0x07) non valido: blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti
- NXD_MQTT_INVALID_PARAMETER (0x10009) message_buffer o topic_buffer puntatore è NULL

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UCHAR topic[MAX_TOPIC_SIZE];
UCHAR message[MAX_TOPIC_SIZE];
UINT topic_length;
UINT message_length;

/* Retrieve a message from MQTT client receive queue. */
status = nxd_mqtt_client_message_get(&my_client, topic,
    sizeof(topic), &topic_length, message, sizeof(message),
    &message_length);

/* Check the return value. */
if(status == NXD_MQTT_SUCCESS)
{
/* A message is received. All done. */
}
else if (status == NXD_MQTT_NO_MESSAGE)
{
/* No more messages in the receive queue. All done. */
}
else
{
/* Receive error. */
}
```

## <a name="nxd_mqtt_client_disconnect_notify_set"></a>nxd_mqtt_client_disconnect_notify_set

Imposta la funzione di callback di disconnessione del messaggio MQTT

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_disconnect_notify_set(
    NXD_MQTT_CLIENT *client_ptr,
    VOID(*disconnect_notify)(NXD_MQTT_CLIENT* client_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback con il client MQTT. Quando MQTT rileva che la connessione al Broker viene persa, chiama questa funzione Notify per avvisare l'applicazione. Pertanto, l'applicazione può utilizzare questa funzione di callback per rilevare una connessione persa e per poter ristabilire la connessione al broker.

```c
VOID callback_func(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.
- **disconnect_notify** Funzione di callback fornita dall'utente da richiamare quando MQTT rileva che la connessione al Broker viene persa.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) ha impostato correttamente la funzione Disconnetti notifica.
- NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
VOID disconnect_notify(NXD_MQTT_CLIENT *client_ptr)
{
/* MQTT client is disconnected from the broker. Notify the application so it can re-connect to the broker. */
}

status = nxd_mqtt_client_disconnect_notify_set(client_ptr,
    disconnect_notify);
```

## <a name="nxd_mqtt_client_disconnect"></a>nxd_mqtt_client_disconnect

Disconnettere il client di MQTT dal broker

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_disconnect(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disconnette il client dal broker. Si noti che i messaggi nella coda di ricezione vengono rilasciati. I messaggi con QoS 1 nella coda di trasmissione non vengono rilasciati. Quando il client si riconnette al server, i messaggi QoS 1 possono essere elaborati, a meno che il client non si riconnetta al server con *clean_session* flag impostato su ***NX_TRUE***.

Se la connessione è stata effettuata con la protezione TLS, questo servizio chiuderà la sessione TLS prima di disconnettere la connessione TCP.

La chiamata di disconnessione socket TCP effettiva ha un'opzione wait definita da NXD_MQTT_SOCKET_TIMEOUT (cicli timer). Il valore predefinito è NX_WAIT_FOREVER. Per evitare una sospensione illimitata nel caso in cui la connessione di rete venga persa o il server non risponda, impostare questa opzione su un valore finito.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.

### <a name="return-values"></a>Valori restituiti

- La disconnessione di **NXD_MQTT_SUCCESS** (0x00) da Service Broker è stata completata
- **NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT.
- NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Disconnect from the broker. */
status = nxd_mqtt_client_disconnect(&my_client);

/* If status is NXD_MQTT_SUCCESS the client is successfully
disconnected from the broker. */
```

## <a name="nxd_mqtt_client_delete"></a>nxd_mqtt_client_delete

Eliminare l'istanza del client MQTT

### <a name="prototype"></a>Prototipo

```c
UINT nxd_mqtt_client_delete(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina l'istanza del client MQTT e rilascia le risorse interne. Questo servizio disconnette automaticamente il client dal broker se è ancora connesso. I messaggi non ancora trasmessi o non riconosciuti vengono rilasciati. Vengono rilasciati anche i messaggi ricevuti ma non recuperati dall'applicazione.

Se la connessione è stata effettuata con la protezione TLS, questo servizio chiude la sessione TLS prima di disconnettere la connessione TCP.

Dopo che il client è stato eliminato, un'applicazione che vuole usare il servizio MQTT deve creare una nuova istanza.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client MQTT.

### <a name="return-values"></a>Valori restituiti

- **NXD_MQTT_SUCCESS** (0x00) ha eliminato correttamente il client MQTT.
- NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the MQTT client instance. */
status = nxd_mqtt_client_delete(&my_client);

/* If status is NXD_MQTT_SUCCESS the client is successfully
deleted from the system. */
```
