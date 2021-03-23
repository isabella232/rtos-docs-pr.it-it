---
title: Capitolo 2-installazione e uso di Azure RTO NetX LWM2M
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente LWM2M NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8c13d3b092d3a5b59bd0369f6ffc162509d02590
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822604"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-lwm2m"></a>Capitolo 2-installazione e uso di Azure RTO NetX LWM2M

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente LWM2M NetX di Azure RTO.

## <a name="product-distribution"></a>Distribuzione del prodotto

NetX LWM2M è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Il pacchetto include tre file di origine, uno di inclusione e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_lwm2m_client. h**: file di intestazione per il client Lwm2m di NETX

- **nx_lwm2m_ *. c/h**: file di origine c/h per NETX lwm2m

- **demo_netx_lwm2m_client. c**: file di origine c per NETX demo client lwm2m

- **NetX_LWM2M_User_Guide.pdf**: Descrizione PDF del prodotto NETX LWM2M

## <a name="netx-lwm2m-installation"></a>Installazione di NetX LWM2M

Per poter usare NetX LWM2M, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\\ threadX \\ ARM7 \\ green*", il *nx_lwm2m&#42;. &#42;* i file devono essere copiati in questa directory.

## <a name="using-netx-lwm2m"></a>Uso di NetX LWM2M

L'uso di NetX LWM2M è facile. In pratica, il codice dell'applicazione deve includere *nx_lwm2m_client. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter usare threadX e NETX. Una volta incluso *nx_lwm2m_client. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione lwm2m NETX specificate più avanti in questa guida. L'applicazione deve inoltre importare i file di *nx_lwm2m&#42;. &#42;* nella libreria NETX.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione quando si compila la libreria client di LWM2M e l'applicazione usando il client LWM2M. Le opzioni di configurazione possono essere definite nell'origine dell'applicazione, nella riga di comando, se non diversamente specificato.

### <a name="nx_lwm2m_client_disable_error_checking"></a>NX_LWM2M_CLIENT_DISABLE_ERROR_CHECKING

Definito, rimuove l'API di base per il controllo degli errori del client LWM2M e migliora le prestazioni. I codici restituiti dell'API non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella definizione dell'API.

### <a name="nx_lwm2m_client_disable_float"></a>NX_LWM2M_CLIENT_DISABLE_FLOAT

Definito, rimuove il supporto dei valori numerici a virgola mobile. Se disabilitato, il client LWM2M non è in grado di supportare risorse con tipo di dati float.

### <a name="nx_lwm2m_client_disable_float64"></a>NX_LWM2M_CLIENT_DISABLE_FLOAT64

Definito, rimuove il supporto dei valori numerici a virgola mobile a 64 bit. Il client LWM2M può comunque ricevere messaggi TLV contenenti numeri a virgola mobile a 64 bit, ma i valori vengono convertiti in virgola mobile a 32 bit per l'elaborazione.

### <a name="nx_lwm2m_client_priority"></a>NX_LWM2M_CLIENT_PRIORITY

Specifica la priorità del thread del client LWM2M. Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.

### <a name="nx_lwm2m_client_max_device_errors"></a>NX_LWM2M_CLIENT_MAX_DEVICE_ERRORS

Specifica il numero massimo di codici di errore archiviati dall'oggetto dispositivo. Il valore predefinito è 8.

### <a name="nx_lwm2m_client_max_security_instances"></a>NX_LWM2M_CLIENT_MAX_SECURITY_INSTANCES

Specifica il numero massimo di istanze di oggetti di sicurezza. Il valore predefinito è 2 per supportare un server bootstrap e un server standard.

### <a name="nx_lwm2m_client_max_server_instances"></a>NX_LWM2M_CLIENT_MAX_SERVER_INSTANCES

Specifica il numero massimo di istanze di oggetti server. Il valore predefinito è 1 per il supporto di un singolo server standard.

### <a name="nx_lwm2m_client_max_server_uri"></a>NX_LWM2M_CLIENT_MAX_SERVER_URI

Specifica la lunghezza massima di un URI del server, incluso il carattere null di terminazione. Il valore predefinito è 128.

### <a name="nx_lwm2m_client_max_access_control_instances"></a>NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_INSTANCES

Specifica il numero massimo di istanze del controllo di accesso. Il valore predefinito è 0, che disabilita il controllo di accesso. Se l'applicazione supporta più di un server LWM2M, il numero massimo di istanze del controllo di accesso deve essere impostato sul numero massimo di istanze di oggetti che il client LWM2M supporterà, perché è necessario creare un'istanza del controllo di accesso per ogni istanza dell'oggetto, ad eccezione delle istanze degli oggetti di sicurezza.

### <a name="nx_lwm2m_client_max_access_control_acls"></a>NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_ACLS

Specifica il numero massimo di risorse ACL per ogni istanza del controllo di accesso. Il valore predefinito è 4.

### <a name="nx_lwm2m_client_max_notifications"></a>NX_LWM2M_CLIENT_MAX_NOTIFICATIONS

Specifica il numero massimo di notifiche che il client LWM2M supporterà. Un server LWM2M può impostare notifiche su oggetti, istanze di oggetti e risorse. Il valore predefinito è 8.

### <a name="nx_lwm2m_client_max_resources"></a>NX_LWM2M_CLIENT_MAX_RESOURCES

Specifica il numero massimo di risorse per oggetto. Il valore predefinito è (32).

### <a name="nx_lwm2m_client_bootstrap_idle_timer"></a>NX_LWM2M_CLIENT_BOOTSTRAP_IDLE_TIMER

Specifica il tempo massimo di attesa per le richieste del server di bootstrap quando viene avviata la sessione bootstrap prima di interrompere la sessione. Il valore predefinito è 60 secondi.

### <a name="nx_lwm2m_client_dtls_start_timeout"></a>NX_LWM2M_CLIENT_DTLS_START_TIMEOUT

Specifica il tempo massimo di attesa per il completamento dell'handshake DTLS. Il valore predefinito è 30 secondi.

### <a name="nx_lwm2m_client_dtls_end_timeout"></a>NX_LWM2M_CLIENT_DTLS_END_TIMEOUT

Specifica il tempo massimo di attesa per il completamento dell'arresto del DTLS. Il valore predefinito è 5 secondi.
