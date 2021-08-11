---
title: Capitolo 2 - Installazione e uso di Azure RTOS client NetX Duo MQTT
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client NetX Duo MQTT.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: faf9d84b8b2bce12a99a72198a396b121055a8eef975349f53833a180092e0a3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797535"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-mqtt-client"></a>Capitolo 2 - Installazione e uso di Azure RTOS client NetX Duo MQTT

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS client NetX Duo MQTT.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il client MQTT per NetX Duo è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include due file di origine, uno di inclusione e un file che contiene questo documento, come indicato di seguito:

- **nxd_mqtt_client.h** File di intestazione per il client MQTT per NetX Duo
- **nxd_mqtt_client.c** File di origine C per il client MQTT per NetX Duo
- **nxd_mqtt_client.pdf** Descrizione del client MQTT per NetX Duo
- **demo_mqtt_client.c** Dimostrazione di NetX Duo MQTT

## <a name="mqtt-client-installation"></a>Installazione del client MQTT

Per usare il client MQTT per NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Ad esempio, se NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_mqtt_client.h* e *nxd_mqtt_client.c* per netX Duo MQTT Client devono essere copiati in questa directory.

## <a name="using-mqtt-client"></a>Uso del client MQTT

L'uso del client MQTT per NetX Duo è semplice. Fondamentalmente, il codice dell'applicazione deve includere *nxd_mqtt_client.h* dopo aver incluso *rispettivamente tx_api.h* e *nx_api.h*, per poter usare rispettivamente ThreadX e NetX Duo. Dopo aver incluso i file di intestazione del client MQTT, il codice dell'applicazione può usare i servizi MQTT descritti più avanti in questa guida. L'applicazione deve anche *includere nxd_mqtt_client.c* nel processo di compilazione. Questi file devono essere compilati nello stesso modo degli altri file dell'applicazione e il relativo modulo oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare il client NetX Duo MQTT.

## <a name="using-mqtt-client-with-netx-secure-tls"></a>Uso del client MQTT con NetX Secure TLS

Per usare il client MQTT con il modulo NetX Secure TLS, l'applicazione deve avere installato il modulo NetX Secure TLS e includere *nx_secure_tls_api.h* *e nx_crypto.h*. La libreria MQTT deve essere compilata con il ***simbolo NX_SECURE_ENABLE*** definito.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la creazione di client MQTT per NetX Duo. Di seguito è riportato un elenco di tutte le opzioni, in cui ognuna è descritta in dettaglio. I valori predefiniti sono elencati, ma possono essere ridefiniti prima *dell'inclusione di nxd_mqtt_client.h.*

- **NX_DISABLE_ERROR_CHECKING**: definita, questa opzione rimuove il controllo degli errori del client MQTT di base. Viene in genere usato dopo il debug dell'applicazione.
- **NX_SECURE_ENABLE**: definito, il client MQTT viene compilato con il supporto TLS.
La definizione di questo simbolo richiede l'installazione del modulo NetX Secure TLS.
*NX_SECURE_ENABLE* non è abilitato per impostazione predefinita.**
- **NXD_MQTT_REQUIRE_TLS**: definito, l'applicazione deve usare TLS per connettersi al broker MQTT. Questa funzionalità richiede *NX_SECURE_ENABLE* definita. Per impostazione predefinita, questo simbolo non è definito.
- **NXD_MQTT_MAXIMUM_TRANSMIT_QUEUE_DEPTH:** definita, la profondità della coda di trasmissione MQTT è abilitata. Deve essere un numero intero positivo.
- **NXD_MQTT_MAX_TOPIC_NAME_LENGTH:** deprecato.
- **NXD_MQTT_MAX_MESSAGE_LENGTH:** deprecato.
- **NXD_MQTT_KEEPALIVE_TIMER_RATE**: definisce la frequenza del timer MQTT, in tick timer ThreadX. Questo timer viene usato per tenere traccia dell'ora dopo l'invio dell'ultimo messaggio di controllo MQTT e invia un messaggio PINGREQ MQTT prima della scadenza dell'ora keep-alive. Questo timer viene attivato se il client si connette al broker con un valore di timer keep-alive impostato. Il valore predefinito è TX_TIMER_TICKS_PER_SECOND, ovvero un timer di un secondo.
- **NXD_MQTT_PING_TIMEOUT_DELAY**: definisce il tempo di attesa del client MQTT per PINGRESP dal broker dopo l'invio di MQTT PINGREQ. Se dopo questo ritardo di timeout non viene ricevuto alcun PINGRESP, il client considera il broker come non reattivo e si disconnette dal broker. Il ritardo predefinito del timeout PING TX_TIMER_TICKS_PER_SECOND, ovvero un secondo.
- **NXD_MQTT_SOCKET_TIMEOUT**: definisce il timeout nella chiamata di disconnessione del socket TCP durante la disconnessione dal server MQTT in tick timer. Il valore predefinito è NX_WAIT_FOREVER.

## <a name="sample-mqtt-program"></a>Programma MQTT di esempio

Il programma seguente illustra una semplice applicazione MQTT. Per semplicità, si presuppone che i codici restituiti siano riusciti, pertanto non viene eseguito alcun altro controllo degli errori.

```c
#define LOCAL_SERVER_ADDRESS (IP_ADDRESS(192, 168, 1, 81))

/*******************************************************/
/* IOT MQTT Client Example                             */
/*******************************************************/
#define DEMO_STACK_SIZE 2048
#define CLIENT_ID_STRING "mytestclient"
#define MQTT_CLIENT_STACK_SIZE 4096
#define STRLEN(p) (sizeof(p) - 1)

/* Declare the MQTT thread stack space. */
static ULONG mqtt_client_stack[MQTT_CLIENT_STACK_SIZE / sizeof(ULONG)];

/* Declare the MQTT client control block. */
static NXD_MQTT_CLIENT mqtt_client;

/* Define the symbol for signaling a received message. */

/* Define the test threads. */

#define TOPIC_NAME "topic"

#define MESSAGE_STRING "This is a message. "

/* Define the priority of the MQTT internal thread. */
#define MQTT_THREAD_PRIORTY 2

/* Define the MQTT keep alive timer for 5 minutes */
#define MQTT_KEEP_ALIVE_TIMER 300
#define QOS0 0
#define QOS1 1

/* Declare event flag, which is used in this demo. */
TX_EVENT_FLAGS_GROUP mqtt_app_flag;
#define DEMO_MESSAGE_EVENT 1
#define DEMO_ALL_EVENTS 3

/* Declare buffers to hold message and topic. */
static UCHAR message_buffer[NXD_MQTT_MAX_MESSAGE_LENGTH];
static UCHAR topic_buffer[NXD_MQTT_MAX_TOPIC_NAME_LENGTH];

/* Declare the disconnect notify function. */
static VOID my_disconnect_func(NXD_MQTT_CLIENT *client_ptr)
{
    printf("client disconnected from server\n");
}

static VOID my_notify_func(NXD_MQTT_CLIENT* client_ptr, UINT number_of_messages)
{
    tx_event_flags_set(&mqtt_app_flag, DEMO_MESSAGE_EVENT, TX_OR);
    return;
}

static ULONG error_counter;
void demo_mqtt_client_local(NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr)
{
    UINT status;
    NXD_ADDRESS server_ip;
    ULONG events;
    UINT topic_length, message_length;

    /* Create MQTT client instance. */
    nxd_mqtt_client_create(&mqtt_client, "my_client",
        CLIENT_ID_STRING, STRLEN(CLIENT_ID_STRING), ip_ptr, pool_ptr,
        (VOID*)mqtt_client_stack, sizeof(mqtt_client_stack),
        MQTT_THREAD_PRIORTY, NX_NULL, 0);

    /* Register the disconnect notification function. */
    nxd_mqtt_client_disconnect_notify_set(&mqtt_client, my_disconnect_func);

    /* Create an event flag for this demo. */
    status = tx_event_flags_create(&mqtt_app_flag, "my app event");
    server_ip.nxd_ip_version = 4;
    server_ip.nxd_ip_address.v4 = LOCAL_SERVER_ADDRESS;

    /* Start the connection to the server. */
    nxd_mqtt_client_connect(&mqtt_client, &server_ip, NXD_MQTT_PORT, 
        MQTT_KEEP_ALIVE_TIMER, 0, NX_WAIT_FOREVER);

    /* Subscribe to the topic with QoS level 0. */
    nxd_mqtt_client_subscribe(&mqtt_client, TOPIC_NAME, STRLEN(TOPIC_NAME),
        QOS0);

    /* Set the receive notify function. */
    nxd_mqtt_client_receive_notify_set(&mqtt_client, my_notify_func);

    /* Publish a message with QoS Level 1. */
    nxd_mqtt_client_publish(&mqtt_client, TOPIC_NAME,
        STRLEN(TOPIC_NAME), (CHAR*)MESSAGE_STRING, 
        STRLEN(MESSAGE_STRING), 0, QOS1, NX_WAIT_FOREVER);

    /* Now wait for the broker to publish the message. */
    tx_event_flags_get(&mqtt_app_flag, DEMO_ALL_EVENTS,
        TX_OR_CLEAR, &events, TX_WAIT_FOREVER);

    if(events & DEMO_MESSAGE_EVENT)
    {
        nxd_mqtt_client_message_get(&mqtt_client, topic_buffer,
            sizeof(topic_buffer), &topic_length, message_buffer,
            sizeof(message_buffer), &message_length);

        topic_buffer[topic_length] = 0;

        message_buffer[message_length] = 0;

        printf("topic = %s, message = %s\n", topic_buffer, message_buffer);
    }

    /* Now unsubscribe the topic. */
    nxd_mqtt_client_unsubscribe(&mqtt_client, TOPIC_NAME,
        STRLEN(TOPIC_NAME));

    /* Disconnect from the broker. */
    nxd_mqtt_client_disconnect(&mqtt_client);

    /* Delete the client instance, release all the resources. */
    nxd_mqtt_client_delete(&mqtt_client);
    return;
}
```
