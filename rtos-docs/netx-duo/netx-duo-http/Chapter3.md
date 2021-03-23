---
title: Capitolo 3-Descrizione dei servizi HTTP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi HTTP RTO NetX duo di Azure (elencati di seguito) in ordine alfabetico, ad eccezione dell'equivalente ' NetX ' (solo IPv4) dello stesso servizio.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 703071cd5a1d0677a3e995fccfe35d8b1dbbd9f3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821872"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-http-services"></a>Capitolo 3-Descrizione dei servizi HTTP di Azure RTO NetX Duo

Questo capitolo contiene una descrizione di tutti i servizi HTTP RTO NetX duo di Azure (elencati di seguito) in ordine alfabetico, ad eccezione dell'equivalente ' NetX ' (solo IPv4) dello stesso servizio.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in GRASSetto non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

**Servizi client HTTP:**

- **nx_http_client_create** *creare un'istanza del client http*
- **nx_http_client_delete** *eliminare un'istanza client http*
- **nx_http_client_get_start** *avviare una richiesta HTTP Get (solo IPv4)*
- **nx_http_client_get_start_extended** *avviare una richiesta HTTP Get (solo IPv4)*
- **nxd_http_client_get_start** *avviare una richiesta HTTP Get (IPv4 o IPv6)*
- **nxd_http_client_get_start_extended** *avviare una richiesta HTTP Get (IPv4 o IPv6)*
- **nx_http_client_get_packet** *ottenere un pacchetto di dati di risorse successivo*
- **nx_http_client_put_start** *avviare una richiesta HTTP PUT (solo IPv4)*
- **nx_http_client_put_start_extended** *avviare una richiesta HTTP PUT (solo IPv4)*
- **nxd_http_client_put_start** *avviare una richiesta HTTP PUT (IPv4 o IPv6)*
- **nxd_http_client_put_start_extended** *avviare una richiesta HTTP PUT (IPv4 o IPv6)*
- **nx_http_client_put_packet** *inviare il pacchetto di dati di risorse successivo*
- **nx_http_client_set_connect_port** *modificare la porta per la connessione al server http*

**Servizi server HTTP:**

- **nx_http_server_cache_info_callback_set** *impostare il callback per recuperare l'età e la data dell'Ultima modifica dell'URL specificato*
- **nx_http_server_callback_data_send** *inviare dati http da una funzione di callback*
- **nx_http_server_callback_generate_response_header** *creare l'intestazione della risposta nelle funzioni di callback*
- **nx_http_server_callback_generate_response_header_extended** *creare l'intestazione della risposta nelle funzioni di callback*
- **nx_http_server_callback_packet_send** *inviare un pacchetto http da un callback http*
- **nx_http_server_callback_response_send** *inviare risposta dalla funzione di callback*
- **nx_http_server_callback_response_send_extended** *inviare risposta dalla funzione di callback*
- **nx_http_server_content_get** *ottenere contenuto dalla richiesta*
- **nx_http_server_content_get_extended** *ottenere contenuto dalla richiesta; supporta le richieste vuote (lunghezza del contenuto pari a zero)*
- **nx_http_server_content_length_get** *ottenere la lunghezza del contenuto nella richiesta*
- **nx_http_server_content_length_get_extended** *ottenere la lunghezza del contenuto nella richiesta; supporta le richieste vuote (lunghezza del contenuto pari a zero)*
- **nx_http_server_create** *creare un'istanza del server http*
- **nx_http_server_delete** * eliminare un'istanza del server http *
- **nx_http_server_get_entity_content** *la dimensione e la posizione del contenuto dell'entità nell'URL*
- **nx_http_server_get_entity_header** l' *intestazione dell'entità Extract URL nel buffer specificato*
- **nx_http_server_gmt_callback_set** *impostare il callback per recuperare la data e l'ora GMT*
- **nx_http_server_invalid_userpassword_notify_set** *impostare il callback quando in una richiesta client non è stato ricevuto un nome utente e una password non validi*
- **nx_http_server_mime_maps_additional_set** *definire mappe MIME aggiuntive per HTML*
- **nx_http_server_packet_content_find** *estrarre la lunghezza del contenuto nell'intestazione HTTP e impostare il puntatore all'inizio dei dati del contenuto*
- **nx_http_server_packet_get** *ricevere direttamente il pacchetto client*
- **nx_http_server_param_get** *ottenere il parametro dalla richiesta*
- **nx_http_server_query_get** *ottenere una query dalla richiesta*
- **nx_http_server_start** *avviare il server http*
- **nx_http_server_stop** *arrestare il server http*
- **nx_http_server_type_get (obsoleto)** *estrarre il tipo http, ad esempio text/plain dall'intestazione*
- **nx_http_server_type_get_extended** *estrarre il tipo http, ad esempio text/plain dall'intestazione*
- **nx_http_server_digest_authenticate_notify_set** *impostare la funzione di callback autenticazione digest*
- **nx_http_server_authentication_check_set** *impostare la funzione di callback per il controllo dell'autenticazione*

## <a name="nx_http_client_create"></a>nx_http_client_create

Creare un'istanza del client PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_create(NX_HTTP_CLIENT *client_ptr,
            CHAR *client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr,
            ULONG window_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client HTTP nell'istanza IP specificata.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **client_name** Nome dell'istanza del client HTTP.
 - **ip_ptr** Puntatore all'istanza IP.
 - **pool_ptr** Puntatore al pool di pacchetti predefinito. Si noti che i pacchetti in questo pool devono avere un payload sufficientemente grande per gestire l'intestazione della risposta completa. Questa impostazione è definita da NX_HTTP_CLIENT_MIN_PACKET_SIZE in *nx_http. h*.
 - **window_size** Dimensioni della finestra di ricezione del socket TCP del client.

### <a name="return-values"></a>Valori restituiti

 - Creazione client HTTP riuscita **NX_SUCCESS** (0x00)
 - NX_PTR_ERROR (0x07) puntatore HTTP, ip_ptr o pool di pacchetti non valido
 - Dimensioni del payload NX_HTTP_POOL_ERROR (0xE9) non valide nel pool di pacchetti

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status =  nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);

/* If status is NX_SUCCESS an HTTP Client instance was successfully created. */
```

## <a name="nx_http_client_delete"></a>nx_http_client_delete

Eliminare un'istanza client HTTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del client HTTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.

### <a name="return-values"></a>Valori restituiti

 - Eliminazione client HTTP riuscita **NX_SUCCESS** (0x00)
 - NX_PTR_ERROR (0x07) puntatore HTTP non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the HTTP Client instance “my_client.”  */
status =  nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully deleted. */
```

## <a name="nx_http_client_get_start"></a>nx_http_client_get_start

Avvia una richiesta HTTP GET su IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, CHAR *input_ptr,
            UINT input_size, CHAR *username, CHAR *password,
            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il rinvio delle richieste Get.

Questo servizio funziona solo sulla rete IPv4. Per le applicazioni che devono connettersi alla rete IPv6, è necessario usare *nxd_http_client_get_start_extended ()* .

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_client_get_start_extended ()* o *nxd_http_client_get_start_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **risorsa** di Puntatore alla stringa URL per la risorsa richiesta.
 - **input_ptr** Puntatore a dati aggiuntivi per la richiesta GET. Questo indirizzo è facoltativo. Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.
 - **input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **password** di Puntatore alla password facoltativa per l'autenticazione.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP. Le opzioni di attesa sono definite come segue:

    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - Il client HTTP è stato inviato **NX_SUCCESS** (0x00). OTTENERE il messaggio di avvio.
 - Errore del client HTTP interno **NX_HTTP_ERROR** (0XE0)
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - **NX_HTTP_FAILED** (0xe2) errore client HTTP che comunica con il server http.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi.
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                           NX_NULL, 0, “myname”, “mypassword”, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */


#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                            POST_MESSAGE, sizeof(POST_MESSAGE),
                            “myname”, “mypassword”, 1000);


/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST request
   for TEST.HTM and successfully sent. */
```

## <a name="nx_http_client_get_start_extended"></a>nx_http_client_get_start_extended

Avvia una richiesta HTTP GET su IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, UINT resource_length,
            CHAR *input_ptr, UINT input_size, CHAR *username,
            UINT username_length, CHAR *password, UINT password_length,
            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il rinvio delle richieste Get.

Questo servizio funziona solo sulla rete IPv4. Per le applicazioni che devono connettersi alla rete IPv6, è necessario usare *nxd_http_client_get_start_extended ()* .

Questo servizio sostituisce *nx_http_client_get_start ()*. È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **puntatore di risorsa** alla stringa URL per la risorsa richiesta.
 - **resource_length** Lunghezza della stringa URL per la risorsa richiesta.
 - **input_ptr** Puntatore a dati aggiuntivi per la richiesta GET. Questo indirizzo è facoltativo. Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.
 - **input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** di Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - Il client HTTP è stato inviato **NX_SUCCESS** (0x00). OTTENERE il messaggio di avvio
 - Errore del client HTTP interno **NX_HTTP_ERROR** (0XE0)
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - **NX_HTTP_FAILED** (0xe2) errore client HTTP che comunica con il server http.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi.
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */


#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                     9, POST_MESSAGE, sizeof(POST_MESSAGE),
                                     “myname”, 6, “mypassword”, 10, 1000);


/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST request
   for TEST.HTM and successfully sent. */
```

## <a name="nxd_http_client_get_start"></a>nxd_http_client_get_start

Inviare una richiesta HTTP GET (IPv4 o IPv6)

### <a name="prototype"></a>Prototipo

```c
UINT nxd_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
                NXD_ADDRESS *server_ip, CHAR *resource,
                CHAR *input_ptr, UINT input_size, CHAR *username, CHAR *password, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza. Può essere usato per connettersi a una rete IPv4 o IPv6. Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.

> [!NOTE]
>La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il rinvio delle richieste Get.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_client_get_start_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **Server_ip** Indirizzo IP del server HTTP.
 - **risorsa** di Puntatore alla stringa URL per la risorsa richiesta.
 - **input_ptr** Puntatore a dati aggiuntivi per la richiesta GET. Questo indirizzo è facoltativo. Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.
 - **input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** di Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato la richiesta Get
 - La password di **NX_HTTP_PASSWORD_TOO_LONG** (0xF0) supera la dimensione del buffer
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - I parametri del pacchetto **NX_HTTP_FAILED** (0XE2) non sono validi.
 - Il nome o la password di **NX_HTTP_AUTHENTICATION_ERROR** (0XEB) non è valido
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;


/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nxd_http_client_get_start(&my_client, server_ip_address, “/TEST.HTM”,
NX_NULL, 0, “myname”, “mypassword”, 1000);


/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */
```

## <a name="nxd_http_client_get_start_extended"></a>nxd_http_client_get_start_extended

Inviare una richiesta HTTP GET (IPv4 o IPv6)

### <a name="prototype"></a>Prototipo

```c
UINT nxd_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
                NXD_ADDRESS *server_ip, CHAR *resource,
                UINT resource_length, CHAR *input_ptr,
                UINT input_size, CHAR *username, UINT
                username_length, CHAR *password, UINT
                password_length, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza. Può essere usato per connettersi a una rete IPv4 o IPv6. Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il rinvio delle richieste Get.

Questo servizio sostituisce *nxd_http_client_get_start ()*. È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **Server_ip** Indirizzo IP del server HTTP.
 - **risorsa** di Puntatore alla stringa URL per la risorsa richiesta.
 - **resource_length** Lunghezza della stringa URL per la risorsa richiesta.
 - **input_ptr** Puntatore a dati aggiuntivi per la richiesta GET. Questo indirizzo è facoltativo. Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.
 - **input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** di Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa internamente per elaborare il client HTTP Get Start. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato la richiesta Get
 - La password di **NX_HTTP_PASSWORD_TOO_LONG** (0xF0) supera la dimensione del buffer
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - I parametri del pacchetto **NX_HTTP_FAILED** (0XE2) non sono validi.
 - Il nome o la password di **NX_HTTP_AUTHENTICATION_ERROR** (0XEB) non è valido
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;


/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nxd_http_client_get_start_extended(&my_client, server_ip_address,
                                             “/TEST.HTM”, 9, NX_NULL, 0, “myname”,
        6, “mypassword”, 10, 1000);


/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_http_client_get_packet"></a>nx_http_client_get_packet

Ottenere il pacchetto di dati di risorse successivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET **packet_ptr, ULONG
                               wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il pacchetto successivo di contenuto della risorsa richiesta dalla chiamata *nx_http_client_get_start* precedente. Le chiamate successive a questa routine devono essere apportate fino a quando non viene ricevuto lo stato di restituzione del NX_HTTP_GET_DONE.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **packet_ptr** Destinazione per il puntatore del pacchetto che contiene il contenuto parziale delle risorse.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del pacchetto HTTP client Get. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) client http con esito positivo Get Packet.
 - **NX_HTTP_GET_DONE** (0XEC) client HTTP Get packet is done
 - Il client HTTP **NX_HTTP_NOT_READY** (0xea) non è in modalità Get.
 - Lunghezza del pacchetto **NX_HTTP_BAD_PACKET_LENGTH** (0XED) non valida
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Get the next packet of resource content on the HTTP Client “my_client.”
   Note that the nx_http_client_get_start routine must have been called
   previously. */
status =  nx_http_client_get_packet(&my_client, &next_packet, 1000);


/* If status is NX_SUCCESS, the next packet of content is pointed to
   by “next_packet”. */
```

## <a name="nx_http_client_put_start"></a>nx_http_client_put_start

Avvia una richiesta HTTP PUT su IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               ULONG ip_address, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP specificato. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet ()* per inviare effettivamente il contenuto della risorsa al server http.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il riferimento a richieste PUT.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_client_put_start_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **risorsa** di Puntatore alla stringa URL per la risorsa richiesta.
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **password** di Puntatore alla password facoltativa per l'autenticazione.
 - **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato una richiesta PUT
 - Nome utente di **NX_HTTP_USERNAME_TOO_LONG** (0xF1) troppo grande per il buffer
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP Server
   at IP address 1.2.3.5. */
status =  nx_http_client_put_start(&my_client, IP_ADDRESS(1, 2, 3, 5),
“/TEST.HTM”, “myname”, “mypassword”, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
   started. */
```

## <a name="nx_http_client_put_start_extended"></a>nx_http_client_put_start_extended

Avvia una richiesta HTTP PUT su IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
           ULONG ip_address, CHAR *resource, UINT resource_length,
           CHAR *username,UINT username_length, CHAR *password,
           UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP specificato. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet ()* per inviare effettivamente il contenuto della risorsa al server http.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il riferimento a richieste PUT.

Questo servizio sostituisce *nx_http_client_put_start ()*. È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **risorsa** di Puntatore alla stringa URL per la risorsa richiesta.
 - **resource_length** Lunghezza della stringa URL per la risorsa da inviare al server.
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** di Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato una richiesta PUT
 - Nome utente di **NX_HTTP_USERNAME_TOO_LONG** (0xF1) troppo grande per il buffer
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP Server
   at IP address 1.2.3.5. */
status =  nx_http_client_put_start_extended(&my_client, IP_ADDRESS(1, 2, 3, 5),
“/TEST.HTM”, 9, “myname”, 6, “mypassword”, 10, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
   started. */
```

## <a name="nxd_http_client_put_start"></a>nxd_http_client_put_start

Avviare una richiesta HTTP PUT (IPv4 o IPv6)

### <a name="prototype"></a>Prototipo

```c
UINT nxd_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               NXD_ADDRESS *server_ip, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inserire (inviare) la risorsa specificata sul server HTTP nell'indirizzo IP fornito su IPv6. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet ()* per inviare effettivamente il contenuto della risorsa al server http.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il riferimento a richieste PUT.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_client_put_start_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **server_ip** Indirizzo IP del server HTTP.
 - **risorsa** di Puntatore alla stringa URL per la risorsa da inviare al server.
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **password** di Puntatore alla password facoltativa per l'autenticazione.
 - **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato la richiesta PUT del client http
 - Errore interno del client HTTP **NX_HTTP_ERROR** (0XE0)
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - Errore del client HTTP di **NX_HTTP_FAILED** (0xe2) che comunica con il server http
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;

/* Start an HTTP PUT to place the 20-byte resource Client_test.HTM” on the HTTPv6  
   Server. */
status =  nxd_http_client_put_start(&my_client, &server_ip_address,
                                    "/client_test.htm", "name", "password", 103, 50);

/* If status is NX_SUCCESS, the PUT operation for Client_test.HTM has successfully
   been started. */
```

## <a name="nxd_http_client_put_start_extended"></a>nxd_http_client_put_start_extended

Avviare una richiesta HTTP PUT (IPv4 o IPv6)

### <a name="prototype"></a>Prototipo

```c
UINT nxd_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
          NXD_ADDRESS *server_ip, CHAR *resource, UINT resource_length,
          CHAR *username, UINT username_length, CHAR *password,
          UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inserire (inviare) la risorsa specificata sul server HTTP nell'indirizzo IP fornito su IPv6. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet ()* per inviare effettivamente il contenuto della risorsa al server http.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il riferimento a richieste PUT.

Questo servizio sostituisce *nxd_http_client_put_start ()*. È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **risorsa** di Puntatore alla stringa URL per la risorsa richiesta.
 - **resource_length** Lunghezza della stringa URL per la risorsa da inviare al server.
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** di Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato la richiesta PUT del client http
 - Errore interno del client HTTP **NX_HTTP_ERROR** (0XE0)
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - Errore del client HTTP di NX_HTTP_FAILED (0xE2) che comunica con il server HTTP
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;

/* Start an HTTP PUT to place the 20-byte resource Client_test.HTM” on the HTTPv6  
   Server. */
status =  nxd_http_client_put_start_extended(&my_client, &server_ip_address,
                                            "/client_test.htm", 16, "name", 4, "password", 8, 103, 50);

/* If status is NX_SUCCESS, the PUT operation for Client_test.HTM has successfully
   been started. */
```

## <a name="nx_http_client_put_packet"></a>nx_http_client_put_packet

Invia pacchetto di dati di risorse successivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET *packet_ptr,
                               ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inviare il pacchetto successivo di contenuto di risorse al server HTTP.

> [!NOTE]
> Questa routine deve essere chiamata ripetutamente fino a quando la lunghezza combinata dei pacchetti inviati è uguale alla "total_bytes" specificata nella chiamata *nx_http_client_put_start* precedente.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **packet_ptr** Puntatore al contenuto successivo della risorsa da inviare al server HTTP.
 - **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa internamente per elaborare il pacchetto PUT del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (0x00000001 tramite 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - Il pacchetto client HTTP è stato inviato **NX_SUCCESS** (0x00).
 - Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto
 - **NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0XEE) ha ricevuto il codice di errore del server
 - Lunghezza del pacchetto **NX_HTTP_BAD_PACKET_LENGTH** (0XED) non valida
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi
 - Il server **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) risponde prima del completamento dell'operazione Put
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - Pacchetto di NX_INVALID_PACKET (0x12) troppo piccolo per l'intestazione TCP
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Send a 20-byte packet representing the content of the resource
   “/TEST.HTM” to the HTTP Server. */
status =  nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr, NX_PACKET *packet_ptr, ULONG wait_option);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM has
   successfully been sent. */
```

## <a name="nx_http_client_set_connect_port"></a>nx_http_client_set_connect_port

Impostare la porta di connessione sul server

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_set_connect_port(NX_HTTP_CLIENT *client_ptr,
                                      UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio modifica la porta di connessione per la connessione al server HTTP alla porta specificata in fase di esecuzione. In caso contrario, il valore predefinito della porta di connessione è 80. Questo metodo deve essere chiamato prima di *nx_http_client_get_start ()* e *nx_http_client_put_start ()* , ad esempio quando il client HTTP si connette al server.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **porta** Porta per la connessione al server.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) modifica la porta
 - La porta NX_INVALID_PORT (0x46) supera il valore massimo (0xFFFF) o è zero
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread, inizializzazione

### <a name="example"></a>Esempio

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status =  nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a>nx_http_server_cache_info_callback_set

Impostare il callback per il recupero della validità e della data massima dell'URL

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                         UINT (*cache_info_get)(CHAR *resource,
                                                 UINT *max_age,
                                                 NX_HTTP_SERVER_DATE
                                                      *date));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il servizio di callback richiamato per ottenere la data di validità massima e dell'Ultima modifica della risorsa specificata.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **cache_info_get** Puntatore al callback
 - **max_age** Puntatore alla durata massima di una risorsa
 - **dati** di Puntatore alla data dell'Ultima modifica restituita.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha impostato correttamente il callback
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione

### <a name="example"></a>Esempio

```c
NX_HTTP_SERVER my_server;

UINT cache_info_get(CHAR *resource, UINT *max_age,
                           NX_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_http_server_create and before the HTTP  
   server is set by nx_http_server_start(), set the cache info callback: */

status = nx_http_server_cache_info_callback_set(&my_server, cache_info_get);


/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_http_server_callback_data_send"></a>nx_http_server_callback_data_send

Inviare dati da una funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                       VOID *data_ptr,
                                       ULONG data_length);
```

### <a name="description"></a>Descrizione

Questo servizio invia i dati nel pacchetto fornito dalla routine di callback dell'applicazione. Questa operazione viene in genere usata per inviare i dati dinamici associati alle richieste GET/POST.

> [!NOTE]
> Se viene utilizzata questa funzione, la routine di callback è responsabile dell'invio dell'intera risposta nel formato corretto. Inoltre, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **DATA_PTR** Puntatore ai dati da inviare.
 - **Data_length**  Numero di byte da inviare.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato correttamente i dati del server
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
  CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
                (strcmp(resource, "/test.htm") == 0))
    {

        /* Found it, override the GET processing by sending the resource
    contents directly. */

        nx_http_server_callback_data_send(server_ptr,
    "HTTP/1.0 200 \r\nContent-Length:
    103\r\nContent-Type: text/html\r\n\r\n",
    63);

        nx_http_server_callback_data_send(server_ptr, "<HTML>\r\n<HEAD><TITLE>NetX
    HTTP Test </TITLE></HEAD>\r\n
    <BODY>\r\n<H1>NetX Test Page
    </H1>\r\n</BODY>\r\n</HTML>\r\n", 103);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_generate_response_header"></a>nx_http_server_callback_generate_response_header

Creare un'intestazione della risposta in una funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_generate_response_header(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT content_length,
                        CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a>Descrizione

Questo servizio chiama la funzione interna *_nx_http_server_generate_response_header* quando il server HTTP risponde alle richieste Get, put e Delete del client. È destinato all'uso nelle funzioni di callback del server HTTP quando l'applicazione server HTTP sta progettando la propria risposta al client.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_server_callback_generate_response_header_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **packet_pptr** Puntatore a un puntatore di pacchetto allocato per il messaggio
 - **status_code** Indicare lo stato della risorsa. Esempi:
    - **NX_HTTP_STATUS_OK**
    - **NX_HTTP_STATUS_MODIFIED**
    - **NX_HTTP_STATUS_INTERNAL_ERROR**
 - **CONTENT_LENGTH** Dimensioni del contenuto in byte
 - **content_type** Tipo di HTTP, ad esempio "text/plain"
 - **additional_header** Puntatore a testo intestazione aggiuntivo

### <a name="return-values"></a>Valori restituiti

 - Intestazione creazione **NX_SUCCESS** (0x00) completata
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
CHAR demotestbuffer[] = "<html>\r\n\r\n<head>\r\n\r\n<title>Main   \
            Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n   \  </body>\r\n</html>\r\n";

     /* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
 CHAR *resource, NX_PACKET *recv_packet_ptr)
      {

NX_PACKET   *sresp_packet_ptr;
ULONG       string_length;
CHAR        temp_string[30];
ULONG       length = 0;


   length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length =  (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr ->
nx_http_server_request_resource, temp_string,
sizeof(temp_string));

       /* Null terminate the string. */
   temp_string[temp] = 0;

       /* Now build a response header with server status is OK and no additional header  
          info. */
   status = nx_http_server_callback_generate_response_header(http_server_ptr,
                  &resp_packet_ptr, NX_HTTP_STATUS_OK,
                  length, temp_string, NX_NULL);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                 length,  server_ptr ->
                 nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
       nx_packet_release(resp_packet_ptr);
       return status;
   }



/* Now send the packet! */
           status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                      resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
      nx_packet_release(resp_packet_ptr);

      return status;
   }

/* Let HTTP server know the response has been sent. */
  return NX_HTTP_CALLBACK_COMPLETED;

     }
```

## <a name="nx_http_server_callback_generate_response_header_extended"></a>nx_http_server_callback_generate_response_header_extended

Creare un'intestazione della risposta in una funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_generate_response_header_extended(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT status_code_length,
                        UINT content_length,
                        CHAR *content_type, UINT content_type_length,
                        CHAR *additional_header,
                        UINT additional_header_length);
```

### <a name="description"></a>Descrizione

Questo servizio chiama la funzione interna *_nx_http_server_generate_response_header ()* quando il server HTTP risponde alle richieste Get, put e Delete del client. È destinato all'uso nelle funzioni di callback del server HTTP quando l'applicazione server HTTP sta progettando la propria risposta al client.

Questo servizio sostituisce *nx_http_server_callback_generate_response_header ()*. Questa versione fornisce informazioni aggiuntive sulla lunghezza della funzione di callback.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **packet_pptr** Puntatore a un puntatore di pacchetto allocato per il messaggio
 - **status_code** Indicare lo stato della risorsa. Esempi:
    - **NX_HTTP_STATUS_OK**
    - **NX_HTTP_STATUS_MODIFIED**
    - **NX_HTTP_STATUS_INTERNAL_ERROR**
 - **status_code** Lunghezza del codice di stato
 - **CONTENT_LENGTH** Dimensioni del contenuto in byte
 - **content_type** Tipo di HTTP, ad esempio "text/plain"
 - **content_type_length** Lunghezza del tipo HTTP
 - **additional_header** Puntatore a testo intestazione aggiuntivo
 - **additional_header_length** Lunghezza del testo dell'intestazione aggiuntivo

### <a name="return-values"></a>Valori restituiti

 - Intestazione creazione **NX_SUCCESS** (0x00) completata
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
CHAR demotestbuffer[] = "<html>\r\n\r\n<head>\r\n\r\n<title>Main   \
     Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n   \  </body>\r\n</html>\r\n";

     /* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
 CHAR *resource, NX_PACKET *recv_packet_ptr)
      {

NX_PACKET   *sresp_packet_ptr;
ULONG       string_length;
CHAR        temp_string[30];
ULONG       length = 0;


   length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length =  (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr ->
nx_http_server_request_resource, temp_string,
sizeof(temp_string));

       /* Null terminate the string. */
   temp_string[temp] = 0;

       /* Now build a response header with server status is OK and no additional header  
          info. */
   status = nx_http_server_callback_generate_response_header_extended(
                             http_server_ptr, &resp_packet_ptr, NX_HTTP_STATUS_OK,
              sizeof(NX_HTTP_STATUS_OK) - 1, length,
              temp_string, string_length, NX_NULL, 0);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                 length,  server_ptr ->
                 nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
       nx_packet_release(resp_packet_ptr);
       return status;
   }



/* Now send the packet! */
           status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                      resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
      nx_packet_release(resp_packet_ptr);

      return status;
   }

/* Let HTTP server know the response has been sent. */
  return NX_HTTP_CALLBACK_COMPLETED;

     }
```

## <a name="nx_http_server_callback_packet_send"></a>nx_http_server_callback_packet_send

Inviare un pacchetto HTTP dalla funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_packet_send(NX_HTTP_SERVER *server_ptr,
                                         NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia una risposta server HTTP completa da un callback HTTP. Il pacchetto viene inviato dal server HTTP al _TIMEOUT_SEND NX_HTTP_SERVER. L'intestazione e i dati HTTP devono essere aggiunti al pacchetto. Se lo stato restituito indica un errore, l'applicazione HTTP deve rilasciare il pacchetto.

Il callback deve restituire NX_HTTP_CALLBACK_COMPLETED.

Per un esempio più dettagliato, vedere *nx_http_server_callback_generate_response_header ()* .

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **packet_ptr** Puntatore al pacchetto da inviare

### <a name="return-values"></a>Valori restituiti

 - Il pacchetto server è stato inviato **NX_SUCCESS** (0x00)
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* The packet is appended with HTTP header and data and is ready to send to the
   Client directly. */

   status = nx_http_server_callback_response_send(server_ptr, packet_ptr);

   if (status != NX_SUCCESS)
   {

    nx_packet_release(packet_ptr);
   }

    return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_callback_response_send"></a>nx_http_server_callback_response_send

Invia risposta dalla funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
                                           CHAR *header,
                                           CHAR *information,
                                           CHAR additional_info);
```

### <a name="description"></a>Descrizione

Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione. Questa operazione viene in genere usata per inviare risposte personalizzate associate alle richieste GET/POST.

> [!NOTE]
> Se viene utilizzata questa funzione, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_server_callback_response_send_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **intestazione** di Puntatore alla stringa di intestazione della risposta.
 - **informazioni** su Puntatore alla stringa di informazioni.
 - **additional_info** Puntatore alla stringa di informazioni aggiuntiva.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato una risposta server

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                        CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
               (strcmp(resource, "/test.htm") == 0))
    {

        /* In this example, we will complete the GET processing with
           a resource not found response. */
     nx_http_server_callback_response_send(server_ptr,
                      "HTTP/1.0 404 ",
                      "NetX HTTP Server unable to find  
                       file: ", resource);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_response_send_extended"></a>nx_http_server_callback_response_send_extended

Invia risposta dalla funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_response_send_extended(
                                          NX_HTTP_SERVER *server_ptr,
                                          CHAR *header,
                                          UINT header_length,
                                          CHAR *information,
                                          UINT information_length,
                                          CHAR *additional_info,
                                          UINT additional_info_length);
```

### <a name="description"></a>Descrizione

Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione. Questa operazione viene in genere usata per inviare risposte personalizzate associate alle richieste GET/POST.

> [!NOTE]
> Se viene utilizzata questa funzione, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.

Questo servizio sostituisce *nx_http_server_callback_response_send ()*. Questa versione accetta informazioni di lunghezza aggiuntive come argomenti.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **intestazione** di Puntatore alla stringa di intestazione della risposta.
 - **HEADER_LENGTH** Lunghezza della stringa di intestazione della risposta.
 - **informazioni** su Puntatore alla stringa di informazioni.
 - **information_length** Lunghezza della stringa di informazioni.
 - **additional_info** Puntatore alla stringa di informazioni aggiuntiva.
 - **additional_info_length** Lunghezza della stringa di informazioni aggiuntiva.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha inviato una risposta server

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                        CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
               (strcmp(resource, "/test.htm") == 0))
    {

        /* In this example, we will complete the GET processing with
           a resource not found response. */
     nx_http_server_callback_response_send_extended(
                                             server_ptr,
                      "HTTP/1.0 404 ", 12,
                      "NetX HTTP Server unable to find  
                       file: ", 38, resource, 9);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_content_get"></a>nx_http_server_content_get

Ottenere contenuto dalla richiesta

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_content_get(NX_HTTP_SERVER *server_ptr,
                                NX_PACKET *packet_ptr,
                                ULONG byte_offset,
                                CHAR *destination_ptr,
                                UINT destination_size,
                                UINT *actual_size);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di recuperare la quantità specificata di contenuto dalla richiesta client HTTP POST o PUT. Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_server_content_get_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.
 - **byte_offset** Numero di byte da sfalsare nell'area del contenuto.
 - **destination_ptr** Puntatore all'area di destinazione per il contenuto.
 - **destination_size** Numero massimo di byte disponibili nell'area di destinazione.
 - **actual_size** Puntatore alla variabile di destinazione che verrà impostata sulle dimensioni effettive del contenuto copiato.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) il contenuto del server http riuscito Get
 - Errore interno del server HTTP **NX_HTTP_ERROR** (0XE0)
 - **NX_HTTP_DATA_END** (0xE7) fine del contenuto della richiesta
 - TIMEOUT del server HTTP **NX_HTTP_TIMEOUT** (0xE1) per il recupero del pacchetto di contenuto successivo
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Assuming we are in the application’s request notify callback
   routine, retrieve up to 100 bytes of content starting at offset
   0. */
status =  nx_http_server_content_get(&my_server, packet_ptr,
                      0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
   request content. */
```

## <a name="nx_http_server_content_get_extended"></a>nx_http_server_content_get_extended

Ottieni contenuto dalla richiesta/supporta la lunghezza del contenuto di lunghezza zero

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_content_get_extended(NX_HTTP_SERVER *server_ptr,
                                         NX_PACKET *packet_ptr,
                                         ULONG byte_offset,
                                         CHAR *destination_ptr,
                                         UINT destination_size,
                                         UINT *actual_size);
```

### <a name="description"></a>Descrizione

Questo servizio è quasi identico a *nx_http_server_content_get ()* . tenta di recuperare la quantità specificata di contenuto dalla richiesta del client HTTP post o put. Tuttavia, gestisce le richieste con lunghezza del contenuto pari a zero (' Empty request ') come richiesta valida. Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).

Questo servizio sostituisce *nx_http_server_content_get ()*. Questa versione richiede che il chiamante fornisca informazioni di lunghezza aggiuntive.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo server HTTP.
 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.
 - **byte_offset** Numero di byte da sfalsare nell'area del contenuto.
 - **destination_ptr** Puntatore all'area di destinazione per il contenuto.
 - **destination_size** Numero massimo di byte disponibili nell'area di destinazione.
 - **actual_size** Puntatore alla variabile di destinazione che verrà impostata sulle dimensioni effettive del contenuto copiato.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) contenuto http riuscito Get
 - Errore interno del server HTTP **NX_HTTP_ERROR** (0XE0)
 - **NX_HTTP_DATA_END** (0xE7) fine del contenuto della richiesta
 - TIMEOUT del server HTTP **NX_HTTP_TIMEOUT** (0xE1) nel recupero del pacchetto successivo
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Assuming we are in the application’s request notify callback
   routine, retrieve up to 100 bytes of content starting at offset
   0. */
status =  nx_http_server_content_get_extended(&my_server, packet_ptr,
                               0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
   request content. */
```

## <a name="nx_http_server_content_length_get"></a>nx_http_server_content_length_get

Ottenere la lunghezza del contenuto nella richiesta

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_content_length_get(NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito. Se non è presente alcun contenuto HTTP, questa routine restituisce un valore pari a zero. Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_server_content_length_get_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.

### <a name="return-values"></a>Valori restituiti

 - **lunghezza contenuto** In errore, viene restituito un valore pari a zero  

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Assuming we are in the application’s request notify callback
   routine, get the content length of the HTTP Client request. */
length =  nx_http_server_content_length_get(packet_ptr);

/* The “length” variable now contains the length of the HTTP Client
   request content area. */
```

## <a name="nx_http_server_content_length_get_extended"></a>nx_http_server_content_length_get_extended

Ottenere la lunghezza del contenuto nella richiesta/supporta la lunghezza del contenuto pari a zero valore

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                                UINT *content_length);
```

### <a name="description"></a>Descrizione

Questo servizio è simile a *nx_http_server_content_length_get;* tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito. Tuttavia, il valore restituito indica lo stato di completamento corretto e il valore di lunghezza effettivo viene restituito nel puntatore di input ```content_length``` . Se non è presente alcun contenuto HTTP/lunghezza contenuto = 0, questa routine restituisce ancora uno stato di completamento corretto e il puntatore di input content_length punta a una lunghezza valida (zero). Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).

Questo servizio sostituisce *nx_http_server_content_length_get ()*.

### <a name="input-parameters"></a>Parametri di input

 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.
 - **CONTENT_LENGTH** Puntatore al valore recuperato dal campo lunghezza contenuto

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) contenuto server riuscito Get
 - Formato dell'intestazione HTTP **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) non corretto
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Assuming we are in the application’s request notify callback
   routine, get the content length of the HTTP Client request. */
ULONG content_length;

status =  nx_http_server_content_length_get_extended(packet_ptr, &content_length);

/* If the “status” variable indicates successful completion, the“length” variable
   contains the length of the HTTP Client request content area. */
```

## <a name="nx_http_server_create"></a>nx_http_server_create

Creare un'istanza del server HTTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_create(NX_HTTP_SERVER *http_server_ptr,
      CHAR *http_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr,
      VOID *stack_ptr, ULONG stack_size, NX_PACKET_POOL *pool_ptr,
      UINT (*authentication_check)(NX_HTTP_SERVER *server_ptr,
            UINT request_type, CHAR *resource, CHAR **name,
            CHAR **password, CHAR **realm),
      UINT (*request_notify)(NX_HTTP_SERVER *server_ptr,
            UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server HTTP, che viene eseguita nel contesto del proprio thread ThreadX. Le routine di callback dell'applicazione *authentication_check* e request_notify facoltative forniscono al software dell'applicazione il controllo sulle operazioni di base del server http.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore al blocco di controllo server HTTP.
 - **http_server_name** Puntatore al nome del server HTTP.
 - **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
 - **media_ptr** Puntatore a un'istanza del supporto FileX creata in precedenza.
 - **stack_ptr** Puntatore all'area dello stack di thread del server HTTP.
 - **stack_size** Puntatore alla dimensione dello stack del thread del server HTTP.
 - **authentication_check** Puntatore a funzione per la routine di controllo dell'autenticazione dell'applicazione. Se specificato, questa routine viene chiamata per ogni richiesta del client HTTP. Se questo parametro è NULL, non verrà eseguita alcuna autenticazione.
 - **request_notify** Puntatore della funzione alla routine di notifica della richiesta dell'applicazione. Se specificato, questa routine viene chiamata prima dell'elaborazione del server HTTP della richiesta. Questo consente di reindirizzare il nome della risorsa o i campi all'interno di una risorsa da aggiornare prima di completare la richiesta del client HTTP.

### <a name="return-values"></a>Valori restituiti

 - Creazione del server HTTP riuscita **NX_SUCCESS** (0x00).
 - NX_PTR_ERROR (0x07) server HTTP, IP, supporti, stack o puntatore al pool di pacchetti non validi.
 - Il payload del pacchetto di NX_HTTP_POOL_ERROR (0xE9) del pool non è sufficiente per contenere la richiesta HTTP completa.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create an HTTP Server instance called “my_server.”  */
status =  nx_http_server_create(&my_server, “my server”, &ip_0, &ram_disk,
              stack_ptr, stack_size, &pool_0,
              my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_http_server_delete"></a>nx_http_server_delete

Eliminare un'istanza del server HTTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_delete(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del server HTTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore al blocco di controllo server HTTP.

### <a name="return-values"></a>Valori restituiti

 - Eliminazione del server HTTP riuscita **NX_SUCCESS** (0x00)
 - NX_PTR_ERROR (0x07) puntatore al server HTTP non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the HTTP Server instance called “my_server.”  */
status =  nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a>nx_http_server_get_entity_content

Recuperare il percorso e la lunghezza dei dati dell'entità

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_pptr,
                                       ULONG *available_offset,
                                       ULONG *available_length);
```

### <a name="description"></a>Descrizione

Questo servizio determina la posizione dell'inizio dei dati all'interno dell'entità multiparte corrente nei messaggi client ricevuti e la lunghezza dei dati che non includono la stringa di limite. Il server HTTP interno aggiorna i propri offset in modo che questa funzione possa essere richiamata nello stesso datagramma client per i messaggi con più entità. Il puntatore al pacchetto viene aggiornato al pacchetto successivo in cui il messaggio del client è un datagramma con più pacchetti.

> [!NOTE]
> Per usare questo servizio NX_HTTP_MULTIPART_ENABLE necessario abilitarlo.

Per ulteriori informazioni, vedere [*nx_http_server_get_entity_header*](#nx_http_server_get_entity_header) .

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al server HTTP
 - **packet_pptr** Puntatore alla posizione del puntatore del pacchetto. Si noti che l'applicazione non deve rilasciare questo pacchetto.
 - **available_offset** Puntatore all'offset dei dati dell'entità dal puntatore a prependi del pacchetto
 - **available_length** Puntatore alla lunghezza dei dati dell'entità

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha recuperato correttamente le dimensioni e la posizione del contenuto dell'entità
 - Il contenuto **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) per i marcatori multipart interni del server http è già stato trovato
 - Errore HTTP interno NX_HTTP_ERROR (0xE0)
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_HTTP_SERVER my_server;

UINT        offset, length;
NX_PACKET  *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
   the entity header to determine details about the multipart data. If
   successful, it then calls this service to get the location of entity data: */

status =  nx_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
&length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
   entity data. */
```

## <a name="nx_http_server_get_entity_header"></a>nx_http_server_get_entity_header

Recupera il contenuto dell'intestazione dell'entità

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      UCHAR *entity_header_buffer,
                                      ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'intestazione dell'entità nel buffer specificato. Il server HTTP interno aggiorna i propri puntatori per individuare la prossima entità multipart in un datagramma client con più intestazioni di entità. Il puntatore al pacchetto viene aggiornato al pacchetto successivo in cui il messaggio del client è un datagramma con più pacchetti.

> [!NOTE]
> Per usare questo servizio NX_HTTP_MULTIPART_ENABLE necessario abilitarlo.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al server HTTP
 - **packet_pptr** Puntatore alla posizione del puntatore del pacchetto. Si noti che l'applicazione non deve rilasciare questo pacchetto.
 - **entity_header_buffer** Puntatore alla posizione in cui archiviare l'intestazione dell'entità
 - **BUFFER_SIZE** Dimensioni del buffer di input

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha recuperato correttamente l'intestazione dell'entità
 - Campo di intestazione dell'entità **NX_HTTP_NOT_FOUND** **(0xE6)** non trovato
 - Tempo di **NX_HTTP_TIMEOUT** **(0xE1)** scaduto per la ricezione del pacchetto successivo per il messaggio client Multipack
 - Errore HTTP interno NX_HTTP_ERROR (0xE0)
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                              CHAR *resource, NX_PACKET *packet_ptr)
      {

        NX_PACKET   *sresp_packet_ptr;
        UINT        offset, length;
        NX_PACKET   *response_pkt;
        UCHAR       buffer[1440];

        /* Process multipart data. */
        if(request_type == NX_HTTP_SERVER_POST_REQUEST)
        {

       /* Get the content header. */
       while(nx_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
                                         sizeof(buffer)) == NX_SUCCESS)
   {

      /* Header obtained successfully. Get the content data location. */
      while(nx_http_server_get_entity_content(server_ptr, &packet_ptr, &offset,
                                              &length) == NX_SUCCESS)
      {
           /* Write content data to buffer. */
           nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                                         &length);
           buffer[length] = 0;
      }

    }

    /* Generate HTTP header. */
    status = nx_http_server_callback_generate_response_header(server_ptr,
                         &response_pkt, NX_HTTP_STATUS_OK, 800, "text/html",
                         "Server: NetXDuo HTTP 5.3\r\n");

    if(status == NX_SUCCESS)
    {
        if(nx_http_server_callback_packet_send(server_ptr, response_pkt) !=
  NX_SUCCESS)
 {
                nx_packet_release(response_pkt);
     }
    }


}
else
{
    /* Indicate we have not processed the response to client yet.*/
    return(NX_SUCCESS);
}

/* Indicate the response to client is transmitted. */
return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_gmt_callback_set"></a>nx_http_server_gmt_callback_set

Impostare il callback per ottenere la data e l'ora GMT

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback per ottenere la data e l'ora GMT con un server HTTP creato in precedenza. Questo servizio viene richiamato con il server HTTP che sta creando un'intestazione nel server HTTP risposte al client.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al server HTTP
 - **gmt_getv** Puntatore al callback GMT
 - **DATEV** Puntatore alla data recuperata

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha impostato correttamente il callback
 - NX_PTR_ERROR (0x07) il puntatore al pacchetto o al parametro non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_HTTP_SERVER my_server;

VOID get_gmt(NX_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the GMT
   retrieve callback: */

status =  nx_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
   response header date. */
```

## <a name="nx_http_server_invalid_userpassword_notify_set"></a>nx_http_server_invalid_userpassword_notify_set

Impostare il callback su per gestire l'utente o la password non valida

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_invalid_userpassword_notify_set(
            NX_HTTP_SERVER *http_server_ptr,
            UINT (*invalid_username_password_callback)
                        (CHAR *resource,
                        NXD_ADDRESS *client_address,
                        UINT request_type));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback richiamato quando viene ricevuto un nome utente e una password non validi in una richiesta GET, put o Delete del client, mediante l'autenticazione digest o di base. Il server HTTP deve essere creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al server HTTP
 - **invalid_username_password_callback** Puntatore a callback utente/pass non valido
 - **risorsa** di Puntatore alla risorsa specificata dal client
 - **CLIENT_ADDRESS** Puntatore all'indirizzo client. Può essere IPv4 o IPv6
 - **request_type** Indica il tipo di richiesta client. Può essere:
    - NX_HTTP_SERVER_GET_REQUEST
    - NX_HTTP_SERVER_POST_REQUEST
    - NX_HTTP_SERVER_HEAD_REQUEST
    - NX_HTTP_SERVER_PUT_REQUEST
    - NX_HTTP_SERVER_DELETE_REQUEST

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha impostato correttamente il callback
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_HTTP_SERVER my_server;
VOID invalid_username_password_callback (NX_ CHAR *resource,
                                         NXD_ADDRESS *client_address,
                                         UINT   request_type);

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the invalid
   username password callback: */

status =  nx_http_server_gmt_callback_set(&my_server,
                                          invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
   will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_http_server_mime_maps_additional_set"></a>nx_http_server_mime_maps_additional_set

Impostare mappe MIME aggiuntive per HTML

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_mime_maps_additional_set(
                        NX_HTTP_SERVER *server_ptr,
                        NX_HTTP_SERVER_MIME_MAP *mime_maps,
                        UINT mime_maps_num);
```

### <a name="description"></a>Descrizione

Questo servizio consente allo sviluppatore di applicazioni HTTP di aggiungere altri tipi MIME dai tipi MIME predefiniti forniti dal server HTTP NetX Duo (vedere *nx_http_server_get_type* per l'elenco dei tipi definiti).

Quando viene ricevuta una richiesta client, ad esempio una richiesta GET, il server HTTP analizza il tipo di file richiesto dall'intestazione HTTP usando il set di mappe MIME aggiuntivo e, se non viene trovata alcuna corrispondenza, Cerca una corrispondenza nella mappa MIME predefinita del server HTTP. Se non viene trovata alcuna corrispondenza, il valore predefinito del tipo MIME è "text/plain".

Se la funzione request Notify è registrata con il server HTTP, il callback della richiesta di notifica può chiamare *nx_http_server_type_retrieve ()* per analizzare il tipo di file.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore all'istanza del server HTTP
 - **mime_maps** Puntatore a una matrice di mappa MIME
 - **mime_map_num** Numero di mappe MIME nella matrice

### <a name="return-values"></a>Valori restituiti

 - Set di mappe MIME del server HTTP con **NX_SUCCESS** (0x00) riuscito
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* my_server is an NX_HTTP_SERVER previously created. */

NX_HTTP_SERVER_MIME_MAP my_mime_maps [2];

static NX_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc",      "yourtype/abc"},
    {"xyz",      "mytype/xyz"},
};

status =  nx_http_server_mime_maps_additional_set(&my_server,
                                                  &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP  
  server MIME map set.” */
```

## <a name="nx_http_server_packet_content_find"></a>nx_http_server_packet_content_find

Estrarre la lunghezza del contenuto e impostare il puntatore all'inizio dei dati

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_packet_content_find(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET **packet_ptr,
                                        UINT *content_length);
```

### <a name="description"></a>Descrizione

Questo servizio estrae la lunghezza del contenuto dall'intestazione HTTP. Aggiorna inoltre il pacchetto fornito come indicato di seguito: il puntatore del pacchetto Prepend (inizio della posizione del buffer dei pacchetti in cui scrivere) viene impostato sul contenuto HTTP (dati) appena passata l'intestazione HTTP.

Se l'inizio del contenuto non viene trovato nel pacchetto corrente, la funzione attende la ricezione del pacchetto successivo utilizzando l'opzione NX_HTTP_SERVER_TIMEOUT_RECEIVE wait.

> [!NOTE]
> Questo metodo non deve essere chiamato prima di chiamare *nx_http_server_get_entity_header* perché modifica il puntatore anteposto dopo l'intestazione dell'entità.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore all'istanza del server HTTP
 - **packet_ptr** Puntatore al puntatore del pacchetto per la restituzione del pacchetto con puntatore anteposto aggiornato
 - **CONTENT_LENGTH** Puntatore a Estratto ```content_length```

### <a name="return-values"></a>Valori restituiti

 - È stata trovata la lunghezza del contenuto HTTP **NX_SUCCESS** (0x00) e l'aggiornamento del pacchetto è riuscito
 - Tempo di **NX_HTTP_TIMEOUT** (0xE1) scaduto in attesa del pacchetto successivo
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
The server has received a Client request packet, recv_packet_ptr, and the packet
content find service is called from the request notify callback function
registered with the HTTP server. */

UINT content_length;

status =  nx_http_server_packet_content_find(server_ptr, recv_packet_ptr,
                                             &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
   and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_http_server_packet_get"></a>nx_http_server_packet_get

Ricevere il pacchetto HTTP successivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_packet_get(NX_HTTP_SERVER *server_ptr,
                              NX_PACKET **packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il pacchetto successivo ricevuto sul socket del server HTTP. L'opzione Attendi per la ricezione di un pacchetto è NX_HTTP_SERVER_TIMEOUT_RECEIVE.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore all'istanza del server HTTP
 - **packet_ptr** Puntatore al pacchetto ricevuto

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha ricevuto il pacchetto successivo
 - Tempo di **NX_HTTP_TIMEOUT** (0xE1) scaduto in attesa del pacchetto successivo
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* The HTTP server pointed to by server_ptr is previously created and started. */

UINT content_length;
NX_PACKET *recv_packet_ptr;

status =  nx_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_http_server_param_get"></a>nx_http_server_param_get

Ottenere il parametro dalla richiesta

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_param_get(NX_PACKET *packet_ptr,
                              UINT param_number, CHAR *param_ptr,
                              UINT max_param_size);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di recuperare il parametro URL HTTP specificato nel pacchetto di richiesta fornito. Se il parametro HTTP richiesto non è presente, questa routine restituisce lo stato NX_HTTP_NOT_FOUND. Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).

### <a name="input-parameters"></a>Parametri di input

 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che l'applicazione non deve rilasciare questo pacchetto.
 - **param_number** Numero logico del parametro a partire da zero, da sinistra a destra nell'elenco dei parametri.
 - **param_ptr** Area di destinazione per copiare il parametro.
 - **max_param_size** Dimensioni massime dell'area di destinazione del parametro.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) parametro Server http riuscito Get
 - Il parametro specificato **NX_HTTP_NOT_FOUND** (0xE6) non è stato trovato
 - Il parametro della richiesta **NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xf3) non è terminato correttamente
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Assuming we are in the application’s request notify callback
   routine, get the first parameter of the HTTP Client request. */

status =  nx_http_server_param_get(request_packet_ptr, 0, param_destination,
               30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
   in “param_destination.” */
```

## <a name="nx_http_server_query_get"></a>nx_http_server_query_get

Ottenere una query dalla richiesta

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_query_get(NX_PACKET *packet_ptr, UINT query_number,
                   CHAR *query_ptr, UINT max_query_size);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di recuperare la query URL HTTP specificata nel pacchetto di richiesta fornito. Se la query HTTP richiesta non è presente, questa routine restituisce lo stato NX_HTTP_NOT_FOUND. Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).

### <a name="input-parameters"></a>Parametri di input

 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che l'applicazione non deve rilasciare questo pacchetto.
 - **query_number** Numero logico del parametro a partire da zero, da sinistra a destra nell'elenco di query.
 - **query_ptr** Area di destinazione per la copia della query.
 - **max_query_size** Dimensioni massime dell'area di destinazione della query.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) query del server http riuscita Get
 - Dimensioni della query di **NX_HTTP_FAILED** (0xe2) troppo piccole.
 - Impossibile trovare la query specificata **NX_HTTP_NOT_FOUND** (0xE6)
 - **NX_HTTP_NO_QUERY_PARSED** (0XF2) nessuna query nella richiesta client
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Assuming we are in the application’s request notify callback
   routine, get the first query of the HTTP Client request. */
status =  nx_http_server_query_get(request_packet_ptr, 0, query_destination,
                30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
   in “query_destination.” */
```

## <a name="nx_http_server_start"></a>nx_http_server_start

Avviare il server HTTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_start(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'istanza del server HTTP create in precedenza.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - Avvio del server **NX_SUCCESS** (0x00) riuscito
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Start the HTTP Server instance “my_server.”  */
status =  nx_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_http_server_stop"></a>nx_http_server_stop

Arrestare il server HTTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_stop(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta l'istanza del server HTTP create in precedenza. Questa routine deve essere chiamata prima di eliminare un'istanza del server HTTP.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - Arresto server riuscito **NX_SUCCESS** (0x00)
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the HTTP Server instance “my_server.”  */
status =  nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a>nx_http_server_type_get

Estrai il tipo di file dalla richiesta HTTP client

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                             CHAR *name, CHAR *http_type_string);
```

### <a name="description"></a>Descrizione

> [!NOTE]
> questo servizio è deprecato. Gli utenti sono invitati a usare il servizio *nx_http_server_type_retrieve ()*.

Questo servizio estrae il tipo di richiesta HTTP nel buffer http_type_string e la sua lunghezza nel valore restituito dal nome del buffer di input, in genere l'URL. Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene impostato il tipo "text/plain". In caso contrario, confronta il tipo Estratto con le mappe MIME predefinite del server HTTP per una corrispondenza. Le mappe MIME predefinite nel server HTTP NetX Duo sono:

 - testo **HTML** /HTML
 - testo **htm** /HTML
 - testo **txt** /normale
 - immagine **gif** /gif
 - immagine **jpg** /JPEG
 - icona immagine **ico** /x

Se specificato, verrà inoltre cercato un set definito dall'utente di mappe MIME aggiuntive. Per ulteriori informazioni sulle mappe definite dall'utente, vedere *nx_http_server_mime_maps_addtional_set ()* .

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_server_type_get_extended ()*.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP
 - **puntatore al nome** del buffer da cercare
 - **http_type_string** (puntatore al tipo HTML Estratto)

### <a name="return-values"></a>Valori restituiti

 - **Lunghezza della stringa in byte** Il valore diverso da zero è success. Zero indica un errore.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```c
/* my_server is a previously created HTTP server, which starts accepting client
   requests when nx_http_server_start is called*/

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
    string_length =  nx_http_server_type_get(&my_server_ptr,
                my_server.nx_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
```

## <a name="nx_http_server_type_get_extended"></a>nx_http_server_type_get_extended

Estrai il tipo di file dalla richiesta HTTP client

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_type_get_extended(
                                    NX_HTTP_SERVER *http_server_ptr,
                                    CHAR *name, CHAR *http_type_string,
                                    UINT http_type_string_max_size);
```

### <a name="description"></a>Descrizione

Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la sua lunghezza nel valore restituito dal *nome* del buffer di input, in genere l'URL. Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene impostato il tipo "text/plain". In caso contrario, confronta il tipo Estratto con le mappe MIME predefinite del server HTTP per una corrispondenza. Le mappe MIME predefinite nel server HTTP NetX Duo sono:

 - testo **HTML** /HTML
 - testo **htm** /HTML
 - testo **txt** /normale
 - immagine **gif** /gif
 - immagine **jpg** /JPEG
 - icona immagine **ico** /x

Se specificato, verrà inoltre cercato un set definito dall'utente di mappe MIME aggiuntive. Per ulteriori informazioni sulle mappe definite dall'utente, vedere *nx_http_server_mime_maps_addtional_set ()* .

Questo servizio sostituisce *nx_http_server_type_get ()*. Questa versione fornisce informazioni aggiuntive sulla lunghezza.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP
 - **nome** Puntatore al buffer in cui eseguire la ricerca
 - **name_length** Lunghezza del buffer da cercare
 - **http_type_string** (puntatore al tipo HTML Estratto)
 - **http_type_string_max_size** Dimensioni del buffer di http_type_string

### <a name="return-values"></a>Valori restituiti

 - **Lunghezza della stringa in byte** Il valore diverso da zero è success. Zero indica un errore.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```c
/* my_server is a previously created HTTP server, which starts accepting client
   requests when nx_http_server_start is called*/

CHAR temp_string[20];
UINT string_length;

/* Get the length of request resource. */
    if (_nx_utility_string_length_check(
                    my_server.nx_http_server_request_resource, &resource_length,
                    sizeof(my_server.nx_http_server_request_resource) - 1))
           {
               return;
           }

/* Extract the HTTP type. */
    string_length =  nx_http_server_type_get_extended(&my_server,
               my_server.nx_http_server_request_resource, resource_length,
               temp_string, sizeof(temp_string));

/* If string_length is non zero, the HTTP string is extracted. */
```

Per un esempio più dettagliato, vedere la descrizione per [*nx_http_server_callback_generate_response_header*](#nx_http_server_callback_generate_response_header).

## <a name="nx_http_server_digest_authenticate_notify_set"></a>nx_http_server_digest_authenticate_notify_set

Imposta funzione di callback autenticazione digest

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_digest_authenticate_notify_set(
       NX_HTTP_SERVER *http_server_ptr,
       UINT (*digest_authenticate_callback)(NX_HTTP_SERVER *server_ptr,
                                            CHAR *name_ptr,
                                            CHAR *realm_ptr,
                                            CHAR *password_ptr,
                                            CHAR *method,
                                            CHAR *authorization_uri,
                                            CHAR *authorization_nc,
                                            CHAR *authorization_cnonce
                                           ));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback richiamato quando viene eseguita l'autenticazione del digest.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP
 - **digest_authenticate_callback** Puntatore al callback di autenticazione del digest

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha impostato correttamente il callback
 - NX_PTR_ERROR (0x07) input puntatore non valido
 - Autenticazione del digest NX_NOT_SUPPORTED (0x4B) non abilitata

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```c
UINT digest_authenticate_callback(NX_HTTP_SERVER *server_ptr, CHAR *name_ptr,
                                  CHAR *realm_ptr, CHAR *password_ptr, CHAR *method,
                                  CHAR *authorization_uri, CHAR *authorization_nc,
                                  CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the digest authenticate callback: */

status =  nx_http_server_digest_authenticate_notify_set (&my_server,
    digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
   will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_http_server_authentication_check_set"></a>nx_http_server_authentication_check_set

Imposta la funzione di callback per il controllo dell'autenticazione

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_authentication_check_set(
       NX_HTTP_SERVER *http_server_ptr,
       UINT (*authentication_check_extended)(
                                            NX_HTTP_SERVER *server_ptr,
                                            UINT request_type,
                                            CHAR *resource,
                                            CHAR **name,
                                            UINT *name_length,
                                            CHAR **password,
                                            UINT *password_length,
                                            CHAR **realm,
                                            UINT *realm_length
                                            ));
```

### <a name="description"></a>Descrizione

Questo servizio imposta la funzione di callback del controllo dell'autenticazione.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP
 - **authentication_check_extended** Puntatore al controllo di autenticazione dell'applicazione

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) ha impostato correttamente il callback
 - NX_PTR_ERROR (0x07) input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```c
static UINT  authentication_check_extended(NX_HTTP_SERVER *server_ptr,
                                           UINT request_type, CHAR *resource,
                                           CHAR **name, UINT *name_length,
                                           CHAR **password, UINT *password_length,
                                           CHAR **realm, UINT *realm_length)
{

    /* Just use a simple name, password, and realm for all
       requests and resources. */
    *name =     "name";
    *password = "password";
    *realm =    "NetX Duo HTTP demo";
    *name_length = 4;
    *password_length = 8;
    *realm_length = 18;

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the
   authentication checking callback: */

nx_http_server_authentication_check_set (&my_server,
                                         authentication_check_extended);
```
