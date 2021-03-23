---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo MQTT
description: Per il pacchetto client NetX Duo MQTT è necessario che NetX Duo (versione 5,10 o successiva) sia installato, configurato correttamente e che sia stata creata l'istanza IP.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2e13b997f987e2fd82569bcb1904218908313d70
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821815"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mqtt"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo MQTT

## <a name="netx-duo-mqtt-requirements"></a>Requisiti di NetX Duo MQTT

Il pacchetto client di Azure RTO NetX Duo MQTT richiede l'installazione, la configurazione corretta e la creazione dell'istanza IP di NetX Duo (versione 5,10 o successiva). Il modulo TCP deve essere abilitato nel sistema. Inoltre, se è necessaria la sicurezza TLS, è necessario configurare il modulo TLS sicuro NetX in base al parametro di sicurezza richiesto dal broker.

## <a name="netx-duo-mqtt-specification"></a>Specifica MQTT di NetX Duo

NetX Duo MQTT client implementate è conforme a OASIS MQTT versione 3.1.1 ottobre 29<sup>°</sup> 2014. La specifica si trova in:

- [http://mqtt.org/](http://mqtt.org/)

## <a name="netx-duo-mqtt-basic-operation"></a>Operazione di base di NetX Duo MQTT

MQTT (trasporto di telemetria della coda di messaggi) si basa sul modello del Sottoscrittore di pubblicazione. Un client può pubblicare informazioni ad altri client tramite un broker. Un client, se interessato a un argomento, può sottoscrivere l'argomento tramite il broker. Un broker è responsabile della distribuzione dei messaggi pubblicati ai client che sottoscrivono l'argomento. In questo modello di server di pubblicazione-Sottoscrittore, più client possono pubblicare dati con lo stesso argomento. Un client riceverà un messaggio pubblicato se il client sottoscrive lo stesso argomento.

A seconda del caso di utilizzo, un client può scegliere uno dei tre livelli di QoS durante la pubblicazione di un messaggio:

- **QoS 0**: il messaggio viene recapitato al massimo una volta. I messaggi inviati con QoS 0 potrebbero andare persi.
- **QoS 1**: il messaggio viene recapitato almeno una volta. I messaggi inviati con QoS 1 possono essere recapitati più di una volta.
- **QoS 2**: il messaggio viene recapitato una sola volta. È garantito che i messaggi inviati con QoS 2 siano recapitati senza duplicati.

> [!NOTE]
> Questa implementazione del client MQTT non supporta i messaggi QoS di livello 2.

Poiché QoS 1 e QoS 2 sono garantiti per essere recapitati, il Broker tiene traccia dello stato dei messaggi QoS 1 e QoS 2 inviati a ogni client. Questa operazione è particolarmente importante per i client che prevedono messaggi QoS1 o QoS 2. Il client può essere disconnesso dal broker, ad esempio quando il client viene riavviato o il collegamento di comunicazione è temporaneamente perduto. Il broker deve archiviare i messaggi QoS 1 e QoS 2 in modo che i messaggi possano essere recapitati in un secondo momento dopo che il client è stato riconnesso al broker. Tuttavia, il client può scegliere di non ricevere messaggi non aggiornati dal broker dopo la riconnessione. Il client può eseguire questa operazione avviando la connessione con il flag di *clean_session* impostato su ***NX_TRUE** _. In questo caso, al momento della ricezione del messaggio MQTT CONNECT, il broker deve rimuovere tutte le informazioni di sessione associate a questo client, inclusi i messaggi QoS 1 o QoS 2 non recapitati o non confermati. Se il _flag clean_session * è per ***NX_FALSE**_, il server dovrà inviare di nuovo i messaggi QoS 1 e QoS 2. Il client MQTT invia anche nuovamente eventuali messaggi non riconosciuti se _clean_session * è impostato su ***NX_TRUE *.** Questo riconoscimento è diverso dall'ACK del livello TCP, sebbene ciò avvenga. Il client MQTT Invia un riconoscimento al broker.

Un'applicazione crea un'istanza del client MQTT chiamando ***nxd_mqtt_client_create ()** _. Una volta creato il client, l'applicazione può connettersi al broker chiamando _*_nxd_mqtt_client_connect ()_*_. Dopo la connessione al broker, il client può sottoscrivere un argomento chiamando _*_nxd_mqtt_client_subscribe ()_*_ o pubblicare un argomento chiamando _ *_nxd_mqtt_client_publish ()_* *.

I messaggi MQTT in ingresso vengono archiviati nella coda di ricezione nell'istanza del client MQTT. L'applicazione recupera questi messaggi chiamando ***nxd_mqtt_client_message_get ()***. Se sono presenti messaggi nella coda di ricezione, al chiamante viene restituito il primo messaggio, ad esempio il meno recente, dalla coda. Viene restituita anche la stringa dell'argomento del messaggio.

> [!NOTE]
> La funzione ***nxd_mqtt_client_message_get ()** _ non viene bloccata se la coda di ricezione del client MQTT è vuota. La funzione restituisce immediatamente il codice restituito _ *_NXD_MQTT_NO_MESSAGE_* *. L'applicazione deve considerare questo valore restituito come indicazione che la coda di ricezione è vuota, non un errore.

Per evitare il polling della coda di ricezione per i messaggi in arrivo, l'applicazione può registrare una funzione di callback con il client MQTT chiamando ***nxd_mqtt_client_recieve_notify_set ()***. La funzione di callback viene dichiarata come:

```c
VOID (*receive_notify_callback)(NXD_MQTT_CLIENT *client_ptr, 
    UINT message_count);
```

Quando il client MQTT riceve messaggi dal broker, richiama la funzione di callback se la funzione è impostata. La funzione di callback passa il puntatore al blocco di controllo client e a un valore di conteggio messaggi. Il valore di conteggio messaggi indica il numero di messaggi MQTT nella coda di ricezione. Si noti che questa funzione di callback viene eseguita nel contesto del thread del client MQTT. Pertanto, la funzione di callback non deve eseguire alcuna routine che possa bloccare il thread del client MQTT. La funzione di callback deve attivare il thread dell'applicazione per chiamare ***nxd_mqtt_client_message_get ()*** per recuperare i messaggi.

Per disconnettere e terminare il servizio client MQTT, l'applicazione deve usare il servizio ***nxd_mqtt_client_disconnect ()** _ e _*_nxd_mqtt_client_delete ()._*_ La chiamata di _*_nxd_mqtt_client_disconnect ()_*_ disconnette semplicemente la connessione TCP al broker. Rilascia i messaggi già ricevuti e archiviati nella coda di ricezione. Tuttavia, non rilascia i messaggi QoS di livello 1 nella coda di trasmissione. I messaggi QoS di livello 1 vengono ritrasmessi alla connessione, supponendo che il flag di _*_clean_session_*_ sia impostato su _ *_NX_FALSE._**

Il broker può inoltre disconnettersi dal client. Quando la connessione TCP tra il client e il Broker viene terminata, l'applicazione può ricevere una notifica tramite la funzione Disconnetti notifica. Per usare il meccanismo di notifica, l'applicazione installa la funzione Disconnect Notify chiamando ***nxd_mqtt_client_disconnect_notify_set *.** Una volta osservata una disconnessione TCP e la sessione MQTT è stata creata, viene richiamata la funzione di notifica.

La chiamata di ***nxd_mqtt_client_delete ()*** rilascia tutti i blocchi di messaggi nella coda di trasmissione e nella coda di ricezione. Vengono eliminati anche i messaggi di livello 1 di QoS non riconosciuti.

## <a name="secure-mqtt-connection"></a>Connessione MQTT protetta

Il client MQTT esegue una connessione sicura al broker usando il modulo TLS sicuro NetX. Il numero di porta predefinito per MQTT con sicurezza TLS è 8883, definito in ***NXD_MQTT_TLS_PORT***.

Per creare una connessione MQTT sicura al broker, è necessario negoziare una sessione TLS dopo che è stata stabilita una connessione TCP, prima che i messaggi di MQTT CONNECT possano essere inviati al broker. La configurazione della sessione TLS viene eseguita chiamando ***nxd_mqtt_client_secure_connect ()*** e passando una funzione di callback del programma di installazione TLS definita dall'utente. Durante la fase di connessione MQTT, una volta stabilita la connessione TCP, il client richiama la funzione di callback dell'installazione TLS per avviare un processo di handshake TLS appropriato. Una volta stabilita la sessione TLS, il client continua il messaggio MQTT CONNECT sul canale sicuro.

La funzione di callback definita dall'utente accetta cinque valori di input e viene dichiarata come:

```c
UINT tls_Setup_callback(NXD_MQTT_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certificate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_cerfiticate);
```

Di seguito è riportata una descrizione dei parametri di input:

- **client_ptr**: puntatore al blocco di controllo client MQTT.
- **session_ptr**: puntatore al blocco di controllo della sessione TLS.
- **certificate_ptr**: puntatore al blocco di controllo del certificato. La funzione di installazione configura questo certificato prima di inviarlo al broker.
- **trusted_certificate_ptr**: puntatore al certificato attendibile. La funzione di installazione TLS configura il certificato attendibile per autenticare il server.

Nella funzione di installazione di TLS, l'applicazione è responsabile della creazione di una sessione TLS e della configurazione della sessione con un certificato appropriato. Nello pseudo codice seguente viene illustrata una tipica procedura di avvio della sessione TLS. Per informazioni dettagliate sull'uso delle API TLS, il lettore fa riferimento alla guida dell'utente di NetX Secure TLS.

Di seguito è riportato un esempio di callback di installazione TLS:

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
