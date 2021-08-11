---
title: Capitolo 1 - Introduzione a Azure RTOS NetX Duo MQTT
description: Il pacchetto client NetX Duo MQTT richiede che NetX Duo (versione 5.10 o successiva) sia installato, configurato correttamente e che l'istanza IP sia stata creata.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be650186b233d0f1202beecc22f4bd8bc0af4dbe0f677704d09df057fcbc34fc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797739"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mqtt"></a>Capitolo 1 - Introduzione a Azure RTOS NetX Duo MQTT

## <a name="netx-duo-mqtt-requirements"></a>Requisiti di NetX Duo MQTT

Il pacchetto client Azure RTOS NetX Duo MQTT richiede che NetX Duo (versione 5.10 o successiva) sia installato, configurato correttamente e che l'istanza IP sia stata creata. Il modulo TCP deve essere abilitato nel sistema. Inoltre, se è necessaria la sicurezza TLS, il modulo NetX Secure TLS deve essere configurato in base al parametro di sicurezza richiesto dal broker.

## <a name="netx-duo-mqtt-specification"></a>Specifica di NetX Duo MQTT

L'implementazione del client NetX Duo MQTT è conforme a OASIS MQTT versione 3.1.1 del<sup>29</sup> ottobre 2014. La specifica è disponibile in:

- [http://mqtt.org/](http://mqtt.org/)

## <a name="netx-duo-mqtt-basic-operation"></a>Funzionamento di base di NetX Duo MQTT

MQTT (Message Queue Telemetry Transport) è basato sul modello server di pubblicazione-sottoscrittore. Un client può pubblicare informazioni ad altri client tramite un broker. Un client, se interessato a un argomento, può sottoscrivere l'argomento tramite il broker. Un broker è responsabile del recapito dei messaggi pubblicati ai client che sottoscriveno l'argomento. In questo modello di server di pubblicazione-sottoscrittore, più client possono pubblicare dati con lo stesso argomento. Un client riceverà un messaggio pubblicato se il client sottoscrive lo stesso argomento.

A seconda del caso d'uso, un client può scegliere uno dei 3 livelli QoS quando pubblica un messaggio:

- **QoS 0:** il messaggio viene recapitato al massimo una volta. I messaggi inviati con QoS 0 potrebbero essere persi.
- **QoS 1:** il messaggio viene recapitato almeno una volta. I messaggi inviati con QoS 1 possono essere recapitati più volte.
- **QoS 2:** il messaggio viene recapitato una sola volta. È garantito il recapito dei messaggi inviati con QoS 2, senza duplicazione.

> [!NOTE]
> Questa implementazione del client MQTT non supporta i messaggi QoS di livello 2.

Poiché viene garantito il recapito di QoS 1 e QoS 2, il broker tiene traccia dello stato dei messaggi QoS 1 e QoS 2 inviati a ogni client. Ciò è particolarmente importante per i client che prevedono messaggi QoS1 o QoS 2. Il client può essere disconnesso dal broker, ad esempio quando il client viene riavviato o il collegamento di comunicazione viene temporaneamente perso. Il broker deve archiviare i messaggi QoS 1 e QoS 2 in modo che i messaggi possano essere recapitati in un secondo momento dopo la riconnessione del client al broker. Tuttavia, il client può scegliere di non ricevere messaggi non obsoleti dal broker dopo la riconnessione. Il client può eseguire questa operazione avviando la connessione con il flag *clean_session* impostato su ***NX_TRUE** _. In questo caso, alla ricezione del messaggio MQTT CONNECT, il broker scarterà tutte le informazioni di sessione associate al client, inclusi i messaggi QoS 1 o QoS 2 non recapitati o non confermati. Se il flag clean_session* è _***NX_FALSE**_, il server invii nuovamente i messaggi QoS 1 e QoS 2. Il client MQTT invia di nuovo anche tutti i messaggi non riconosciuti se _clean_session* è impostato su ***NX_TRUE*.** Questo riconoscimento è diverso dal livello TCP ACK, anche se ciò avviene anche in questo caso. Il client MQTT invia un acknowledgment al broker.

Un'applicazione crea un'istanza del client MQTT chiamando ***nxd_mqtt_client_create()** _. Dopo aver creato il client, l'applicazione può connettersi al broker _*_chiamando nxd_mqtt_client_connect()_*_. Dopo la connessione al broker, il client può sottoscrivere un argomento chiamando _*_nxd_mqtt_client_subscribe()_*_ o pubblicare un argomento chiamando _*_nxd_mqtt_client_publish()_**.

I messaggi MQTT in ingresso vengono archiviati nella coda di ricezione nell'istanza del client MQTT. L'applicazione recupera questi messaggi ***chiamando nxd_mqtt_client_message_get()***. Se sono presenti messaggi nella coda di ricezione, il primo messaggio della coda, ad esempio il meno recente, viene restituito al chiamante. Viene restituita anche la stringa dell'argomento del messaggio.

> [!NOTE]
> La funzione ***nxd_mqtt_client_message_get()** _ non si blocca se la coda di ricezione del client MQTT è vuota. La funzione restituisce immediatamente il risultato con il codice restituito _*_NXD_MQTT_NO_MESSAGE_**. L'applicazione deve considerare questo valore restituito come un'indicazione che la coda di ricezione è vuota, non un errore.

Per evitare il polling della coda di ricezione per i messaggi in arrivo, l'applicazione può registrare una funzione di callback con il client MQTT chiamando ***nxd_mqtt_client_recieve_notify_set()***. La funzione di callback viene dichiarata come:

```c
VOID (*receive_notify_callback)(NXD_MQTT_CLIENT *client_ptr, 
    UINT message_count);
```

Quando il client MQTT riceve messaggi dal broker, richiama la funzione di callback se la funzione è impostata. La funzione di callback passa il puntatore al blocco di controllo client e un valore di conteggio dei messaggi. Il valore relativo al numero di messaggi indica il numero di messaggi MQTT nella coda di ricezione. Si noti che questa funzione di callback viene eseguita nel contesto del thread del client MQTT. Pertanto, la funzione di callback non deve eseguire procedure che potrebbero bloccare il thread del client MQTT. La funzione di callback deve attivare il thread dell'applicazione ***per chiamare nxd_mqtt_client_message_get()*** per recuperare i messaggi.

Per disconnettere e terminare il servizio client MQTT, l'applicazione deve usare il servizio ***nxd_mqtt_client_disconnect()** _ _*_e nxd_mqtt_client_delete()._*_ La _*_chiamata nxd_mqtt_client_disconnect()_*_ disconnette semplicemente la connessione TCP al broker. Rilascia i messaggi già ricevuti e archiviati nella coda di ricezione. Tuttavia, non rilascia messaggi QoS di livello 1 nella coda di trasmissione. I messaggi QoS di livello 1 vengono ritrasmessi al momento della connessione, presupponendo che il flag _*_clean_session_*_ sia impostato su _ *_NX_FALSE._**

Il broker può anche disconnettersi dal client. Quando la connessione TCP tra il client e il broker viene terminata, l'applicazione può ricevere una notifica tramite la funzione di notifica della disconnessione. Per usare il meccanismo di notifica, l'applicazione installa la funzione disconnect notify chiamando ***nxd_mqtt_client_disconnect_notify_set*.** Dopo che è stata osservata una disconnessione TCP e la sessione MQTT è stata creata, viene richiamata la funzione di notifica.

La ***chiamata nxd_mqtt_client_delete()*** rilascia tutti i blocchi di messaggi nella coda di trasmissione e nella coda di ricezione. Vengono eliminati anche i messaggi QoS di livello 1 non contrassegnati.

## <a name="secure-mqtt-connection"></a>Proteggere la connessione MQTT

Il client MQTT esegue una connessione sicura al broker usando il modulo NetX Secure TLS. Il numero di porta predefinito per MQTT con sicurezza TLS è 8883, definito in ***NXD_MQTT_TLS_PORT***.

Per creare una connessione MQTT sicura al broker, è necessario negoziare una sessione TLS dopo che è stata stabilita una connessione TCP, prima che i messaggi MQTT CONNECT possano essere inviati al broker. La configurazione della sessione TLS viene eseguita chiamando ***nxd_mqtt_client_secure_connect()*** e passando una funzione di callback di configurazione TLS definita dall'utente. Durante la fase di connessione MQTT, una volta stabilita la connessione TCP, il client richiama la funzione di callback di configurazione TLS per avviare un processo di handshake TLS appropriato. Dopo aver stabilito la sessione TLS, il client continua il messaggio MQTT CONNECT sul canale sicuro.

La funzione di callback definita dall'utente accetta cinque valori di input ed è dichiarata come:

```c
UINT tls_Setup_callback(NXD_MQTT_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certificate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_cerfiticate);
```

Di seguito è riportata una descrizione dei parametri di input:

- **client_ptr**: puntatore al blocco di controllo client MQTT.
- **session_ptr:** puntatore al blocco di controllo della sessione TLS.
- **certificate_ptr:** puntatore al blocco di controllo del certificato. La funzione di configurazione configura questo certificato prima di inviarlo al broker.
- **trusted_certificate_ptr**: puntatore al certificato attendibile. La funzione di installazione di TLS configura il certificato attendibile per autenticare il server.

Nella funzione di configurazione di TLS l'applicazione è responsabile della creazione di una sessione TLS e della configurazione della sessione con un certificato appropriato. Lo pseudocodice seguente illustra una tipica procedura di avvio della sessione TLS. Per informazioni dettagliate sull'uso delle API TLS, vedere il Manuale dell'utente di NetX Secure TLS.

Di seguito è riportato un esempio di callback di configurazione TLS:

```c
UINT tls_setup_callback(NXD_MQTT_CLIENT *client_pt
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certrifcate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_certificate_ptr)
{
    /* Initialize TLS module */
    nx_secure_tls_initialize();

    /* Create a TLS session */
    nx_secure_tls_session_create(session_ptr, …);

    /* Need to allocate space for the certificate coming in from the broker. */
    memset(certificate_ptr), 0, sizeof(NX_SECURE_TLS_CERTIFICATE));

    nx_secure_tls_remote_certificate_allocate(session_ptr, certificate_ptr);

    /* Add a CA Certificate to our trusted store for verifying incomingserver certificates. */
    nx_secure_tls_certificate_initialize(
        trusted_certificate_ptr,
        ca_cert_der,
        ca_cert_der_len, NULL, 0);
    nx_secure_tls_trusted_certificate_add(session_ptr,
        trusted_certificate));
}
```

## <a name="known-limitations-of-the-netx-duo-mqtt-client"></a>Limitazioni note del client NetX Duo MQTT

- NetX Duo MQTT non supporta l'invio o la ricezione di messaggi QoS di livello 2.
- NetX Duo MQTT non supporta i pacchetti concatenati.
