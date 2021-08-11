---
title: Capitolo 3 - Descrizione dei servizi HTTP
description: Questo capitolo contiene una descrizione di tutti i servizi HTTP Web NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f7d711a67b6e129b87dc08bfd54857ffc4bc3d26c34001fe336d2b673fc53752
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801734"
---
# <a name="chapter-3---description-of-http-services"></a>Capitolo 3 - Descrizione dei servizi HTTP

Questo capitolo contiene una descrizione di tutti i servizi HTTP Web NetX (elencati di seguito) in ordine alfabetico.

> [!NOTE]
> Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="http-and-https-client-api"></a>API client HTTP e HTTPS

## <a name="nx_web_http_client_connect"></a>nx_web_http_client_connect

Aprire un socket di testo non crittografato in un server HTTP per richieste personalizzate

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_connect(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip,
    UINT server_port, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTP in testo non** crittografato.

Questo servizio apre un socket TCP in testo non crittografato a un server HTTP, ma non invia alcuna richiesta. Le richieste vengono create con n *x_web_http_client_request_initialize()* e inviate *usando nx_web_http_client_request_send()*. È possibile aggiungere intestazioni HTTP personalizzate alla richiesta *usando nx_web_http_client_request_header_add()*.

L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta. **Ciò consente richieste HTTP personalizzate destinate ad applicazioni specifiche.**

> [!NOTE]
> I nx_web_http_client_*_start vengono forniti per praticità (ad esempio *nx_web_http_client_get_start*()) e gestiscono la generazione della richiesta e la connessione socket. È possibile usare questi servizi *anziché nx_web_http_client_connect()* e le routine correlate se non sono necessarie intestazioni HTTP personalizzate nelle richieste.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **server_ip** Indirizzo IP del server HTTP remoto.
- **server_port** Porta nel server HTTP remoto (ad esempio 80 per HTTP).
- **wait_option** Definisce per quanto tempo il servizio attenderà le operazioni di rete sottostanti. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Connessione riuscita del socket TCP.
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_WEB_HTTP_NOT_READY (0x3000A) Un'altra richiesta è già in corso.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NXD_ADDRESS server_ip_addr;

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

nx_web_http_client_connect(&my_client, &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get* until the entire response is retrieved. */

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);
    /* Process response packets… */
}
```

## <a name="nx_web_http_client_create"></a>nx_web_http_client_create

Creare un'istanza del client HTTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_create(NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr,
    ULONG window_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client HTTP nell'istanza IP specificata. L'istanza client può essere usata per HTTP o HTTPS. Vedere i servizi *nx_web_http_client_connect()* *e nx_web_http_client_secure_connect()* per altre informazioni sull'avvio di un'istanza HTTP o HTTPS. Vedere anche l'API per *nx_web_http_client_get_**, *nx_web_http_client_put_**, *nx_web_http_client_post_** chiamate semplici di metodi GET, PUT e POST.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **client_name** Nome dell'istanza del client HTTP.
- **ip_ptr** Puntatore all'istanza IP.
- **pool_ptr** Puntatore al pool di pacchetti predefinito. Si noti che i pacchetti in questo pool devono avere un payload sufficientemente grande per gestire l'intestazione di risposta completa. Questo valore è definito da *NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE* in *nx_web_http_client.h*.
- **window_size** Dimensioni della finestra di ricezione del socket TCP del client.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione riuscita del client HTTP
- NX_PTR_ERROR (0x16) Puntatore HTTP, ip_ptr o pool di pacchetti non valido
- NX_WEB_HTTP_POOL_ERROR (0x30009) Dimensioni del payload non valide nel pool di pacchetti

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Create the HTTP Client instance "my_client" on "ip_0". */
status = nx_web_http_client_create(&my_client, "my client", &ip_0, &pool_0, 8192);

/* If status is NX_SUCCESS an HTTP Client instance was successfully
    created. */
```

## <a name="nx_web_http_client_delete"></a>nx_web_http_client_delete

Eliminare un'istanza del client HTTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_delete(NX_WEB_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del client HTTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del client HTTP riuscita
- NX_PTR_ERROR (0x16) Puntatore HTTP non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the HTTP Client instance "my_client." */
status = nx_web_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully
    deleted. */
```

## <a name="nx_web_http_client_delete_start"></a>nx_web_http_client_delete_start

Avviare una richiesta HTTP DELETE in testo non crittografato

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_delete_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTP in testo non** crittografato.

Questo servizio tenta di inviare una richiesta DELETE per la risorsa specificata dal puntatore "resource" sull'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi chiamare *nx_web_http_client_response_body_get()* per recuperare la risposta del server.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

Questa API è deprecata. Gli sviluppatori sono invitati a *usare nx_web_http_client_delete_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **resource** Puntatore alla stringa URL per la risorsa richiesta.
- **username** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Messaggio di richiesta DELETE client HTTP
- **NX_WEB_HTTP_ERROR** (0x30000) Errore interno del client HTTP
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- **NX_WEB_HTTP_FAILED** (0x30002) errore del client HTTP che comunica con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_start(&my_client, &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_delete_start_extended"></a>nx_web_http_client_delete_start_extended

Avviare una richiesta HTTP DELETE in testo non crittografato

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_delete_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTP in testo non** crittografato.

Questo servizio tenta di inviare una richiesta DELETE per la risorsa specificata dal puntatore "resource" sull'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi chiamare *nx_web_http_client_response_body_get()* per recuperare la risposta del server.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_delete_start* (). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **resource** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **username** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Messaggio di richiesta DELETE client HTTP
- **NX_WEB_HTTP_ERROR** (0x30000) Errore interno del client HTTP
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- **NX_WEB_HTTP_FAILED** (0x30002) errore del client HTTP che comunica con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_start_extended(&my_client,
    &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_delete_secure_start"></a>nx_web_http_client_delete_secure_start

Avviare una richiesta HTTPS DELETE crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_delete_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di inviare una richiesta DELETE per la risorsa specificata dal puntatore "resource" sull'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi chiamare *nx_web_http_client_response_body_get()* per recuperare la risposta del server.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_delete_secure_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **resource** Puntatore alla stringa URL per la risorsa richiesta. la risorsa deve essere con terminazione NULL.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **username** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio i certificati).
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Messaggio di richiesta DELETE client HTTP
- **NX_WEB_HTTP_ERROR** (0x30000) Errore interno del client HTTP
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- **NX_WEB_HTTP_FAILED** (0x30002) errore del client HTTP che comunica con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_delete_secure_start_extended"></a>nx_web_http_client_delete_secure_start_extended

Avviare una richiesta HTTPS DELETE crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_delete_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di inviare una richiesta DELETE per la risorsa specificata dal puntatore "resource" sull'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi chiamare *nx_web_http_client_response_body_get()* per recuperare la risposta del server.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_delete_secure_start*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **resource** Puntatore alla stringa URL per la risorsa richiesta. la risorsa deve essere con terminazione NULL.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali ,ad esempio i certificati.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Messaggio di richiesta DELETE del client HTTP
- **NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client (Errore interno del client HTTP)
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- **NX_WEB_HTTP_FAILED** errore (0x30002) del client HTTP durante la comunicazione con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_secure_start_extended(&my_client,
    &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_get_start"></a>nx_web_http_client_get_start

Avviare una richiesta HTTP GET in testo non crittografato

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_get_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per HTTP **in testo non** crittografato.

Questo servizio tenta di ottenere la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi effettuare più chiamate *a nx_web_http_client_response_body_get()* per recuperare pacchetti di dati corrispondenti al contenuto della risorsa richiesto.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" o a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_get_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message (Messaggio di avvio GET client HTTP inviato)
- **NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client (Errore interno del client HTTP)
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- **NX_WEB_HTTP_FAILED** errore (0x30002) del client HTTP durante la comunicazione con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    multiple times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_start_extended"></a>nx_web_http_client_get_start_extended

Avviare una richiesta HTTP GET in testo non crittografato

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_get_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per HTTP **in testo non** crittografato.

Questo servizio tenta di ottenere la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi effettuare più chiamate *a nx_web_http_client_response_body_get()* per recuperare pacchetti di dati corrispondenti al contenuto della risorsa richiesto.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" o a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

Le stringhe di risorsa, host, nome utente e password devono avere terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_get_start*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message (Messaggio di avvio GET client HTTP inviato)
- **NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client (Errore interno del client HTTP)
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- **NX_WEB_HTTP_FAILED** errore (0x30002) del client HTTP durante la comunicazione con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_start_extended(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    multiple times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_secure_start"></a>nx_web_http_client_get_secure_start

Avviare una richiesta HTTPS GET crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_get_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
        NX_SECURE_TLS_SESSION *tls_session),
        ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di ottenere la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi effettuare più chiamate *a nx_web_http_client_response_body_get()* per recuperare pacchetti di dati corrispondenti al contenuto della risorsa richiesto.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" o a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_get_secure_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali ,ad esempio i certificati.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message (Messaggio di avvio GET client HTTP inviato)
- **NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client (Errore interno del client HTTP)
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- **NX_WEB_HTTP_FAILED** errore (0x30002) del client HTTP durante la comunicazione con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started
    and is so far successful. The client must now call
    *nx_web_http_client_response_body_get()* multiple times to
    retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_secure_start_extended"></a>nx_web_http_client_get_secure_start_extended

Avviare una richiesta HTTPS GET crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_get_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di ottenere la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi effettuare più chiamate *a nx_web_http_client_response_body_get()* per recuperare pacchetti di dati corrispondenti al contenuto della risorsa richiesto.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" o a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

Le stringhe di risorsa, host, nome utente e password devono avere terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_secure_start*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali ,ad esempio i certificati.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message (Messaggio di avvio GET client HTTP inviato)
- **NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client (Errore interno del client HTTP)
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- **NX_WEB_HTTP_FAILED** errore (0x30002) del client HTTP durante la comunicazione con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM
    is started and is so far successful. The client must now call
    *nx_web_http_client_response_body_get()* multiple times to retrieve
    the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_head_start"></a>nx_web_http_client_head_start

Avviare una richiesta HTTP HEAD in testo non crittografato

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_head_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per HTTP **in testo non** crittografato.

Questo servizio tenta di recuperare i metadati HEAD per la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi chiamare *nx_web_http_client_response_body_get()* per recuperare la risposta.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" o a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_head_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Messaggio di richiesta HEAD client HTTP
- **NX_WEB_HTTP_ERROR** (0x30000) Errore interno del client HTTP
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- **NX_WEB_HTTP_FAILED** (0x30002) errore del client HTTP che comunica con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_head_start_extended"></a>nx_web_http_client_head_start_extended

Avviare una richiesta HTTP HEAD in testo non crittografato

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_head_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTP in testo non** crittografato.

Questo servizio tenta di recuperare i metadati HEAD per la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi chiamare *nx_web_http_client_response_body_get()* per recuperare la risposta.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_head_start*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **resource** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **username** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Messaggio di richiesta HEAD client HTTP
- **NX_WEB_HTTP_ERROR** (0x30000) Errore interno del client HTTP
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- **NX_WEB_HTTP_FAILED** (0x30002) errore del client HTTP che comunica con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_head_secure_start"></a>nx_web_http_client_head_secure_start

Avviare una richiesta HTTPS HEAD crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_head_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di recuperare i metadati HEAD per la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi chiamare *nx_web_http_client_response_body_get()* per recuperare la risposta del server corrispondente al contenuto della risorsa richiesto.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_head_secure_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **resource** Puntatore alla stringa URL per la risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **username** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio i certificati).
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Messaggio di richiesta HEAD client HTTP
- **NX_WEB_HTTP_ERROR** (0x30000) Errore interno del client HTTP
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- **NX_WEB_HTTP_FAILED** (0x30002) errore del client HTTP che comunica con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_head_secure_start_extended"></a>nx_web_http_client_head_secure_start_extended

Avviare una richiesta HTTPS HEAD crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_head_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di recuperare i metadati HEAD per la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi chiamare *nx_web_http_client_response_body_get()* per recuperare la risposta del server corrispondente al contenuto della risorsa richiesto.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` GET.

Le stringhe di risorsa, host, nome utente e password devono avere terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_head_secure_start*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta nel server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali ,ad esempio i certificati.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message (Messaggio di richiesta HEAD client HTTP inviato correttamente)
- **NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client (Errore interno del client HTTP)
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- **NX_WEB_HTTP_FAILED** errore (0x30002) del client HTTP durante la comunicazione con il server HTTP.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_request_packet_allocate"></a>nx_web_http_client_request_packet_allocate

Allocare un pacchetto HTTP(S)

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_request_packet_allocate(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di allocare un pacchetto per HTTP(S) client.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **packet_ptr** Puntatore al pacchetto allocato.
- **wait_option** Definisce il tempo di attesa in tick se non sono disponibili pacchetti nel pool di pacchetti. Le opzioni di attesa sono definite come segue:
  - **NX_NO_WAIT** (0x00000000)
  - **NX_WAIT_FOREVER** (0xFFFFFFFF)
  - **timeout in tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Corretta allocazione pacchetti
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a *tx_thread_wait_abort*.
- **NX_INVALID_PARAMETERS** (0x4D) Le dimensioni del pacchetto non supportano il protocollo.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Allocate a packet for HTTP(S) Client and suspend for a maximum of 5 timer
    ticks if the pool is empty. */
status = nx_web_http_client_request_packet_allocate(&my_client, &packet_ptr, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
    variable packet_ptr. */
```

## <a name="nx_web_http_client_post_start"></a>nx_web_http_client_post_start

Avviare una richiesta HTTP POST

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_post_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host,
    CHAR *username, CHAR *password,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per HTTP **in testo non** crittografato.

Questo servizio tenta di inviare una richiesta POST con la risorsa specificata al server HTTP all'indirizzo IP e alla porta specificati. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet* per inviare il contenuto della risorsa al server HTTP.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` PUT.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_post_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta TCP sul server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa da inviare al server.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *a nx_web_http_client_put_packet()* deve essere uguale a questo valore.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent POST request
- **NX_WEB_HTTP_USERNAME_TOO_LONG** nome utente (0x30012) troppo grande per il buffer
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start an HTTP POST to post the 20-byte resource "/TEST.HTM" to the HTTP Server
    at IP address 1.2.3.5. */
status = nx_web_http_client_post_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_start_extended"></a>nx_web_http_client_post_start_extended

Avviare una richiesta HTTP POST

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_post_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per HTTP **in testo non** crittografato.

Questo servizio tenta di inviare una richiesta POST con la risorsa specificata al server HTTP all'indirizzo IP e alla porta specificati. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet* per inviare il contenuto della risorsa al server HTTP.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` PUT.

Le stringhe di risorsa, host, nome utente e password devono avere terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_post_start* (). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta TCP sul server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *a nx_web_http_client_put_packet()* deve essere uguale a questo valore.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent POST request
- **NX_WEB_HTTP_USERNAME_TOO_LONG** nome utente (0x30012) troppo grande per il buffer
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start an HTTP POST to post the 20-byte resource "/TEST.HTM" to the HTTP Server
    at IP address 1.2.3.5. */
status = nx_web_http_client_post_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_secure_start"></a>nx_web_http_client_post_secure_start

Avviare una richiesta HTTPS POST crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_post_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di inviare una richiesta POST con la risorsa specificata al server HTTPS all'indirizzo IP e alla porta specificati. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet()* per inviare il contenuto della risorsa al server HTTP.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` PUT.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_post_secure_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta TCP sul server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa da inviare al server.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *a nx_web_http_client_put_packet()* deve essere uguale a questo valore.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali ,ad esempio i certificati.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent POST request
- **NX_WEB_HTTP_USERNAME_TOO_LONG** nome utente (0x30012) troppo grande per il buffer
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_secure_start_extended"></a>nx_web_http_client_post_secure_start_extended

Avviare una richiesta HTTPS POST crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_post_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di inviare una richiesta POST con la risorsa specificata al server HTTPS all'indirizzo IP e alla porta specificati. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet()* per inviare il contenuto della risorsa al server HTTP.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` PUT.

Le stringhe di risorsa, host, nome utente e password devono avere terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_post_secure_start* (). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta TCP sul server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *a nx_web_http_client_put_packet()* deve essere uguale a questo valore.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio i certificati).
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La richiesta POST è stata inviata correttamente
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Nome utente troppo grande per il buffer
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_start"></a>nx_web_http_client_put_start

Avviare una richiesta HTTP PUT

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_put_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTP in testo non** crittografato.

Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP e alla porta forniti. Se questa routine ha esito positivo, il codice dell'applicazione deve eseguire chiamate successive alla routine *nx_web_http_client_put_packet()* per inviare il contenuto della risorsa al server HTTP.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta le richieste PUT di `http://abc.website.com/index.htm` riferimento.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_put_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta TCP nel server HTTP remoto.
- **resource** Puntatore alla stringa URL per la risorsa da inviare al server.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **username** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *a nx_web_http_client_put_packet()* deve essere uguale a questo valore.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La richiesta PUT è stata inviata correttamente
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Nome utente troppo grande per il buffer
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTP Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_start_extended"></a>nx_web_http_client_put_start_extended

Avviare una richiesta HTTP PUT

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_put_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTP in testo non** crittografato.

Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP e alla porta forniti. Se questa routine ha esito positivo, il codice dell'applicazione deve eseguire chiamate successive alla routine *nx_web_http_client_put_packet()* per inviare il contenuto della risorsa al server HTTP.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta le richieste PUT di `http://abc.website.com/index.htm` riferimento.

Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_put_start* (). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta TCP nel server HTTP remoto.
- **resource** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **username** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *a nx_web_http_client_put_packet()* deve essere uguale a questo valore.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La richiesta PUT è stata inviata correttamente
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Nome utente troppo grande per il buffer
- **NX_WEB_HTTP_NOT_READY** (0x3000A) Client HTTP non pronto
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTP Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_secure_start"></a>nx_web_http_client_put_secure_start

Avviare una richiesta HTTPS PUT crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_put_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTPS all'indirizzo IP e alla porta specificati. Se questa routine ha esito positivo, il codice dell'applicazione deve eseguire chiamate successive alla routine *nx_web_http_client_put_packet()* per inviare il contenuto della risorsa al server HTTP.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta le richieste PUT di `http://abc.website.com/index.htm` riferimento.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_put_secure_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta TCP sul server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa da inviare al server.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *a nx_web_http_client_put_packet()* deve essere uguale a questo valore.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali ,ad esempio i certificati.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent PUT request (Invio della richiesta PUT completato)
- **NX_WEB_HTTP_USERNAME_TOO_LONG** nome utente (0x30012) troppo grande per il buffer
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_secure_start_extended"></a>nx_web_http_client_put_secure_start_extended

Avviare una richiesta HTTPS PUT crittografata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_put_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTPS all'indirizzo IP e alla porta specificati. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet()* per inviare il contenuto della risorsa al server HTTP.

Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm", oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle richieste `http://abc.website.com/index.htm` PUT.

Le stringhe di risorsa, host, nome utente e password devono avere terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_put_secure_start*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **ip_address** Indirizzo IP del server HTTP.
- **server_port** Porta TCP sul server HTTP remoto.
- **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *a nx_web_http_client_put_packet()* deve essere uguale a questo valore.
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali ,ad esempio i certificati.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully sent PUT request (Invio della richiesta PUT completato)
- **NX_WEB_HTTP_USERNAME_TOO_LONG** nome utente (0x30012) troppo grande per il buffer
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_packet"></a>nx_web_http_client_put_packet

Inviare il pacchetto di dati della risorsa successivo

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_put_packet(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inviare il pacchetto successivo di contenuto della risorsa al server HTTP per le operazioni PUT e POST. Si noti che questa routine deve essere chiamata in modo ripetitivo finché la lunghezza combinata dei pacchetti inviati non è uguale al valore "total_bytes" specificato nella chiamata *nx_web_http_client_put_start()* o *nx_web_http_client_post_start()* precedente (o alle versioni sicure corrispondenti).

Questo servizio controlla anche la presenza di una risposta dal server nel caso in cui si sia verificato un problema durante la connessione HTTP (o HTTPS).

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **packet_ptr** Puntatore al contenuto successivo della risorsa da inviare al server HTTP.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il pacchetto client HTTP è stato inviato correttamente.
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non pronto
- **NX_WEB_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0x3000E) Received Server error code**
- **NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000D) Lunghezza pacchetto non valida
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Nome e/o password non validi
- **NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** server (0x3000F) risponde prima del completamento di PUT
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_INVALID_PACKET (0x12) Pacchetto troppo piccolo per l'intestazione TCP
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send a 20-byte packet representing the content of the resource
    "/TEST.HTM" to the HTTP Server. */

status = nx_web_http_client_put_packet(&client_ptr, packet_ptr, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM has
    successfully been sent. */
```

## <a name="nx_web_http_client_request_chunked_set"></a>nx_web_http_client_request_chunked_set

Impostare il trasferimento in blocchi per la richiesta HTTP(S)

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_request_chunked_set(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT chunk_size, NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio usa la codifica di trasferimento in blocchi per inviare una richiesta HTTP(S) personalizzata al server specificato nella chiamata *nx_web_http_client_connect()* o *nx_web_http_client_secure_connect()* che in precedenza ha stabilito la connessione socket all'host remoto.

> [!NOTE]
> Se l'applicazione usa la codifica di trasferimento in blocchi per inviare un pacchetto di dati della richiesta, deve chiamare questo servizio *dopo* aver chiamato nx_web_http_client_request_packet_allocate () e prima di nx_web_http_client_reqeust_packet_send *().*

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **chunk_size** Dimensioni dei dati in blocchi in ottetti.
- **packet_ptr** Puntatore al pacchetto di dati della richiesta HTTP(S).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Correttamente impostato in blocchi.
- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTPS server. */

nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a PUT request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_PUT,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_TRUE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the PUT operation. */
nx_web_http_client_request_send(&my_client, 1000);

/* Create a new data packet request on the HTTP(S) client instance. */
nx_web_http_client_request_packet_allocate(&my_client,
    &my_packet,
    NX_WAIT_FOREVER);

/* Set the chunked transfer. */
status = nx_web_http_client_request_chunked_set(&my_client, 128, my_packet);

/* At this point, user can fill the data into my_packet. */
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet request to server. */
nx_web_http_client_request_packet_send(&my_client, my_packet,
    0, NX_WAIT_FOREVER);
```

## <a name="nx_web_http_client_request_header_add"></a>nx_web_http_client_request_header_add

Aggiungere un'intestazione personalizzata a una richiesta HTTP personalizzata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_request_header_add(
    NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *field_name, UINT name_length,
    CHAR *field_value, UINT value_length,
    UINT wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'intestazione personalizzata (sotto forma di nome e valore di campo) a una richiesta HTTP personalizzata creata con n *x_web_http_client_request_initialize().*

L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta. **Ciò consente richieste HTTP personalizzate destinate ad applicazioni specifiche.**

> [!NOTE]
> I nx_web_http_client_ \* _start vengono forniti per praticità. Tutte queste funzioni usano questa routine internamente (insieme *a nx_web_http_client_request_initialize())* per creare e inviare richieste HTTP.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **field_name** Stringa del nome del campo ,ad esempio "Content-Type".
- **name_length** Lunghezza della stringa del nome di campo in byte.
- **field_value** Stringa del valore del campo ,ad esempio "application/octet-stream".
- **value_length** Lunghezza della stringa del valore in byte.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta di intestazione alla richiesta completata.
- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */

nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server
    by repeatedly calling *nx_web_http_client_response_body_get()*
    until the entire response is retrieved. */

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_initialize"></a>nx_web_http_client_request_initialize

Inizializzare una richiesta HTTP personalizzata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_request_initialize(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT method, CHAR *resource, CHAR *host,
    UINT input_size, UINT transfer_encoding_trunked,
    CHAR *username, CHAR *password, UINT wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio crea una richiesta HTTP personalizzata e la associa all'istanza del client HTTP. A differenza della più semplice *nx_web_http_client_get_start()* (insieme ai metodi per PUT, POST e alle versioni sicure associate di tali API), la richiesta personalizzata non viene inviata fino a quando non viene chiamato *il servizio nx_web_http_client_request_send().*

L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta ***usando il servizio nx_web_http_client_request_header_add().*** Ciò consente richieste HTTP personalizzate destinate ad applicazioni specifiche.

> [!NOTE]
> I nx_web_http_client_ \* _start vengono forniti per praticità. Tutte queste funzioni usano questa routine internamente (insieme a *nx_web_http_client_request_send())* per creare e inviare richieste HTTP.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_client_request_initialize_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **metodo** Metodo di richiesta HTTP da usare. Le opzioni sono definite come segue:
  - **NX_WEB_HTTP_METHOD_NONE (0x0)**
  - **NX_WEB_HTTP_METHOD_GET (0x1)**
  - **NX_WEB_HTTP_METHOD_PUT (0x2)**
  - **NX_WEB_HTTP_METHOD_POST (0x3)**
  - **NX_WEB_HTTP_METHOD_DELETE (0x4)**
  - **NX_WEB_HTTP_METHOD_HEAD (0x5)**
- **risorsa** Nome della risorsa da trasferire.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **input_size** Dimensioni dei dati di input per PUT e POST. Passare 0 per altre operazioni.
- **transfer_encoding_trunked** Parametro riservato per il supporto futuro del trasferimento trunked.
- **nome utente** Nome utente per le risorse protette.
- **password** Password per le risorse protette.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della richiesta completata.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_WEB_HTTP_METHOD_ERROR (0x30014) Mancano alcune informazioni necessarie (ad esempio, input_size per PUT o POST).

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */

status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get()* until the entire response is retrieved. */
get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_initialize_extended"></a>nx_web_http_client_request_initialize_extended

Inizializzare una richiesta HTTP personalizzata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_request_initialize_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, UINT method,
    CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length,
    UINT input_size, UINT transfer_encoding_trunked,
    CHAR *username, UINT username_length,
    CHAR *password, UINT password_length, UINT wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio crea una richiesta HTTP personalizzata e la associa all'istanza del client HTTP. A differenza della più semplice *nx_web_http_client_get_start()* (insieme ai metodi per PUT, POST e alle versioni sicure associate di tali API), la richiesta personalizzata non viene inviata fino a quando non viene chiamato *il servizio nx_web_http_client_request_send().*

L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta ***usando il servizio nx_web_http_client_request_header_add().*** Ciò consente richieste HTTP personalizzate destinate ad applicazioni specifiche.

> [!NOTE]
> I nx_web_http_client_ \* _start vengono forniti per praticità. Tutte queste funzioni usano questa routine internamente (insieme a *nx_web_http_client_request_send())* per creare e inviare richieste HTTP.

Le stringhe di risorsa, host, nome utente e password devono avere terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_client_request_initialize*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **metodo** Metodo di richiesta HTTP da usare. Le opzioni sono definite come segue:
  - **NX_WEB_HTTP_METHOD_NONE (0x0)**
  - **NX_WEB_HTTP_METHOD_GET (0x1)**
  - **NX_WEB_HTTP_METHOD_PUT (0x2)**
  - **NX_WEB_HTTP_METHOD_POST (0x3)**
  - **NX_WEB_HTTP_METHOD_DELETE (0x4)**
  - **NX_WEB_HTTP_METHOD_HEAD (0x5)**
- **resource** Nome della risorsa da trasferire.
- **resource_length** Lunghezza della stringa della risorsa richiesta.
- **host** Stringa con terminazione Null del nome di dominio del server. Questa stringa viene trasmessa nel campo intestazione host HTTP. La stringa host non può essere NULL.
- **host_length** Lunghezza della stringa dell'host.
- **input_size** Dimensioni dei dati di input per PUT e POST. Passare 0 per altre operazioni.
- **transfer_encoding_trunked** Parametro riservato per il supporto del trasferimento trunk futuro.
- **username** Puntatore al nome utente facoltativo per l'autenticazione.
- **username_length** Lunghezza della stringa del nome utente per l'autenticazione.
- **password** Puntatore alla password facoltativa per l'autenticazione.
- **password_length** Lunghezza della stringa della password per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della richiesta completata.
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_WEB_HTTP_METHOD_ERROR (0x30014) Mancano alcune informazioni necessarie (ad esempio, input_size per PUT o POST).

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize_extended(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "test.txt ", sizeof("test.txt ") – 1,
    "host.com", sizeof("host.com") – 1,
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    0,
    NX_NULL, /* password */
    0,
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);


/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get()* until the entire response is retrieved. */
get_status = NX_SUCCESS;
while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_packet_send"></a>nx_web_http_client_request_packet_send

Inviare un pacchetto di dati di richiesta HTTP(S) al server remoto

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_request_packet_send(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET *packet_ptr, UINT more_date,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto di dati di richiesta HTTP(S) personalizzato creato con *nx_web_http_client_request_packet_allocate* () al server specificato nella chiamata *nx_web_http_client_connect()* o *nx_web_http_client_secure_connect(*) che ha stabilito in precedenza la connessione socket all'host remoto.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **packet_ptr** Puntatore al pacchetto di dati della richiesta HTTP(S).
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio riuscito del pacchetto di dati della richiesta.
- NX_PTR_ERROR (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a PUT request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_PUT,
    "https://192.168.1.150/test.txt ", "host.com",
    128, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the PUT operation. */
nx_web_http_client_request_send(&my_client, 1000);

/* Create a new data packet request on the HTTP(S) client instance. */
nx_web_http_client_request_packet_allocate(&my_client,
    &my_packet,
    NX_WAIT_FOREVER);

/* At this point, user can fill the data into my_packet. */
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet request to server. */
status = nx_web_http_client_request_packet_send(&my_client,
    my_packet,
    0,
    NX_WAIT_FOREVER);
```

## <a name="nx_web_http_client_request_send"></a>nx_web_http_client_request_send

Inviare una richiesta HTTP personalizzata

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_request_send(NX_WEB_HTTP_CLIENT *client_ptr,
    UINT wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia una richiesta HTTP personalizzata creata con *nx_web_http_client_request_initialize()* al server specificato in *nx_web_http_client_connect()* o *nx_web_http_client_secure_connect()* che hanno stabilito in precedenza la connessione socket all'host remoto.

L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta usando ***il servizio nx_web_http_client_request_header_add().*** Ciò consente richieste HTTP personalizzate destinate ad applicazioni specifiche.

> [!NOTE]
> I nx_web_http_client_ \* _start vengono forniti per praticità. Queste funzioni usano tutte questa routine internamente (insieme *a nx_web_http_client_request_initialize())* per creare e inviare richieste HTTP.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio della richiesta riuscito.
- NX_PTR_ERROR (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by
    repeatedly calling *nx_web_http_client_response_body_get* until
    the entire response is retrieved. */

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_response_body_get"></a>nx_web_http_client_response_body_get

Ottenere il pacchetto di dati delle risorse successivo

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_response_body_get(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET **packet_ptr, ULONG
    wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il pacchetto successivo di contenuto della risorsa richiesto dalla richiesta precedente. Le chiamate successive a questa routine devono essere effettuate fino a quando non viene ricevuto lo stato restituito NX_WEB_HTTP_GET_DONE.)

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **packet_ptr** Destinazione per il puntatore a pacchetto contenente il contenuto parziale della risorsa.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando NX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ottenere correttamente il pacchetto client HTTP.
- **NX_WEB_HTTP_GET_DONE** (0x3000C) Il pacchetto get del client HTTP è stato eseguito
- **NX_WEB_HTTP_NOT_READY** client HTTP (0x3000A) non in modalità get.
- **NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000D) Lunghezza del pacchetto non valida
- **NX_WEB_HTTP_STATUS_CODE_CONTINUE** (0x3001A) Codice di stato HTTP 100 Continua
- **NX_WEB_HTTP_STATUS_CODE_SWITCHING_PROTOCOLS** (0x3001B) Codice di stato HTTP 101 Switching Protocols
- **NX_WEB_HTTP_STATUS_CODE_CREATED** (0x3001C) Codice di stato HTTP 201 Creato
- **NX_WEB_HTTP_STATUS_CODE_ACCEPTED** (0x3001D) Codice di stato HTTP 202 accettato
- **NX_WEB_HTTP_STATUS_CODE_NON_AUTH_INFO** (0x3001E) Codice di stato HTTP 203 Informazioni non autorevoli
- **NX_WEB_HTTP_STATUS_CODE_NO_CONTENT** (0x3001F) Codice di stato HTTP 204 Nessun contenuto
- **NX_WEB_HTTP_STATUS_CODE_RESET_CONTENT** (0x30020) Codice di stato HTTP 205 Reimposta contenuto
- **NX_WEB_HTTP_STATUS_CODE_PARTIAL_CONTENT** (0x30021) Codice di stato HTTP 206 Contenuto parziale
- **NX_WEB_HTTP_STATUS_CODE_MULTIPLE_CHOICES** (0x30022) Codice di stato HTTP 300 Scelte multiple
- **NX_WEB_HTTP_STATUS_CODE_MOVED_PERMANETLY** (0x30023) Codice di stato HTTP 301 Spostato in modo permanente
- **NX_WEB_HTTP_STATUS_CODE_FOUND** (0x30024) Codice di stato HTTP 302 Trovato
- **NX_WEB_HTTP_STATUS_CODE_SEE_OTHER** (0x30025) Codice di stato HTTP 303 Vedere altro
- **NX_WEB_HTTP_STATUS_CODE_NOT_MODIFIED** (0x30026) Codice di stato HTTP 304 Non modificato
- **NX_WEB_HTTP_STATUS_CODE_USE_PROXY** (0x30027) Codice di stato HTTP 305 Usare il proxy
- **NX_WEB_HTTP_STATUS_CODE_TEMPORARY_REDIRECT** (0x30028) HTTP con codice di stato HTTP 307 Reindirizzamento temporaneo
- **NX_WEB_HTTP_STATUS_CODE_BAD_REQUEST** (0x30029) Codice di stato HTTP 400 Richiesta non valida
- **NX_WEB_HTTP_STATUS_CODE_UNAUTHORIZED** (0x3002A) Codice di stato HTTP 401 Non autorizzato
- **NX_WEB_HTTP_STATUS_CODE_PAYMENT_REQUIRED** (0x3002B) Codice di stato HTTP 402 Pagamento richiesto
- **NX_WEB_HTTP_STATUS_CODE_FORBIDDEN** (0x3002C) Codice di stato HTTP 403 Accesso negato
- **NX_WEB_HTTP_STATUS_CODE_NOT_FOUND** (0x3002D) Codice di stato HTTP 404 Non trovato
- **NX_WEB_HTTP_STATUS_CODE_METHOD_NOT_ALLOWED** (0x3002E) Codice di stato HTTP 405 Metodo non consentito
- **NX_WEB_HTTP_STATUS_CODE_NOT_ACCEPTABLE** (0x3002F) Codice di stato HTTP 406 Non accettabile
- **NX_WEB_HTTP_STATUS_CODE_PROXY_AUTH_REQUIRED** (0x30030) Http status code 407 Proxy Authentication Required
- **NX_WEB_HTTP_STATUS_CODE_REQUEST_TIMEOUT** (0x30031) HTTP con codice di stato HTTP 408 Timeout richiesta
- **NX_WEB_HTTP_STATUS_CODE_CONFLICT** (0x30032) Conflitto del codice di stato HTTP 409
- **NX_WEB_HTTP_STATUS_CODE_GONE** (0x30033) Codice di stato HTTP 410 Non più visualizzato
- **NX_WEB_HTTP_STATUS_CODE_LENGTH_REQUIRED** (0x30034) Codice di stato HTTP 411 Lunghezza richiesta
- **NX_WEB_HTTP_STATUS_CODE_PRECONDITION_FAILED** (0x30035) Codice di stato HTTP 412 Precondizione non riuscita
- **NX_WEB_HTTP_STATUS_CODE_ENTITY_TOO_LARGE** (0x30036) Codice di stato HTTP 413 Entità richiesta troppo grande
- **NX_WEB_HTTP_STATUS_CODE_URL_TOO_LARGE** (0x30037) HTTP con codice di stato HTTP 414 Url richiesta troppo grande
- **NX_WEB_HTTP_STATUS_CODE_UNSUPPORTED_MEDIA** (0x30038) Codice di stato HTTP 415 Tipo di supporto non supportato
- **NX_WEB_HTTP_STATUS_CODE_RANGE_NOT_SATISFY** (0x30039) Codice di stato HTTP 416 Intervallo richiesto non soddisfabile
- **NX_WEB_HTTP_STATUS_CODE_EXPECTATION_FAILED** (0x3003A) Codice di stato HTTP 417 Previsione non riuscita
- **NX_WEB_HTTP_STATUS_CODE_INTERNAL_ERROR** (0x3003B) http status code 500 Internal Server Error (Errore interno del server)
- **NX_WEB_HTTP_STATUS_CODE_NOT_IMPLEMENTED** (0x3003C) Codice di stato HTTP 501 Non implementato
- **NX_WEB_HTTP_STATUS_CODE_BAD_GATEWAY** (0x3003D) Codice di stato HTTP 502 - Gateway non valido
- **NX_WEB_HTTP_STATUS_CODE_SERVICE_UNAVAILABLE** (0x3003E) Codice di stato HTTP 503 Servizio non disponibile
- **NX_WEB_HTTP_STATUS_CODE_GATEWAY_TIMEOUT** (0x3003F) codice di stato HTTP 504 Timeout gateway
- **NX_WEB_HTTP_STATUS_CODE_VERSION_ERROR** (0x30040) Codice di stato HTTP 505 Versione HTTP non supportata
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Get the next packet of resource content on the HTTP Client "my_client."
    Note that the nx_web_http_client_get_start() routine must have been called
    previously. */
status = nx_web_http_client_response_body_get(&my_client, &next_packet, 1000);

/* If status is NX_SUCCESS, the next packet of content is pointed to
    by "next_packet". */
```

## <a name="nx_web_http_client_response_header_callback_set"></a>nx_web_http_client_response_header_callback_set

Impostare il callback da richiamare durante l'elaborazione delle intestazioni HTTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_response_header_callback_set(
    NX_WEB_HTTP_CLIENT *client_ptr,
    VOID (*callback_function)(NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *field_name, UINT field_name_length,
    CHAR *field_value, UINT field_value_length));
```

### <a name="description"></a>Descrizione

Questo servizio assegna un callback che verrà richiamato ogni volta che il client HTTP Web NetX elabora un'intestazione HTTP in una risposta in ingresso da un server HTTP remoto. Il callback viene richiamato una volta per ogni intestazione nella risposta durante l'elaborazione. Il callback consente a un'applicazione client HTTP di accedere a ognuna delle intestazioni nella risposta del server HTTP per eseguire qualsiasi azione desiderata oltre all'elaborazione di base del client HTTP Web NetX.

### <a name="input-parameters"></a>Parametri di input

**client_ptr** Puntatore al blocco di controllo client HTTP.

**callback_function** Callback richiamato durante l'elaborazione dell'intestazione della risposta. Il callback viene richiamato con il nome e il valore del campo come stringhe (e le relative lunghezze). Ad esempio, l'intestazione "Content-Length: 100" causerebbe la chiamata della funzione con "Content-Length" per *field_name* e la stringa "100" per *field_value*.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Assegnazione del callback riuscita.
- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Setup a callback to print out header information as it is processed. */
VOID http_response_callback(NX_WEB_HTTP_CLIENT *client_ptr, CHAR *field_name,
    UINT field_name_length, CHAR *field_value,
    UINT field_value_length)
{
    CHAR name[100];
    CHAR value[100];
    memset(name, 0, sizeof(name));

    memset(value, 0, sizeof(value));

    strncpy(name, field_name, field_name_length);
    strncpy(value, field_value, field_value_length);

    printf("Received header: \n");
    printf("\tField name: %s (%d bytes)\n", name, field_name_length);
    printf("\tValue: %s (%d bytes)\n\n", value, field_value_length);
}

/* Assign the callback to the HTTP client instance. */
nx_web_http_client_response_header_callback_set(&my_client,
    http_response_callback);

/* Start a GET operation to get a response from the HTTP server. */
status = nx_web_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "myname", "mypassword", 1000);

/* When the HTTP server returns a response to the GET request, NetX Web HTTP
    Client will invoke the http_response_callback function for each header
    processed in the HTTP response. */
```

## <a name="nx_web_http_client_secure_connect"></a>nx_web_http_client_secure_connect

Aprire una sessione TLS a un server HTTPS per le richieste personalizzate

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_client_secure_connect(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls),
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo metodo è per **HTTPS protetto da** TLS.

Questo servizio apre una sessione TLS protetta a un server HTTPS, ma non invia alcuna richiesta. Le richieste vengono create con n *x_web_http_client_request_initialize()* e inviate *usando nx_web_http_client_request_send().* È possibile aggiungere intestazioni HTTP personalizzate alla richiesta *usando nx_web_http_client_request_header_add()*.

L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta. **Ciò consente richieste HTTP personalizzate destinate ad applicazioni specifiche.**

> [!NOTE]
> I nx_web_http_client_ \* _start vengono forniti per praticità. Tutte queste funzioni usano questa routine internamente (insieme *a nx_web_http_client_request_initialize())* per creare e inviare richieste HTTP.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **server_ip** Indirizzo IP del server HTTPS remoto.
- **server_port** Porta nel server HTTPS remoto (ad esempio, 443 per HTTPS).
- **tls_setup** Callback usato per configurare la configurazione TLS. L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali ,ad esempio i certificati.
- **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite come segue:
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Connessione della sessione TLS riuscita.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_WEB_HTTP_NOT_READY (0x3000A) Un'altra richiesta è già in corso.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect to a remote HTTPS server. */
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

nx_web_http_client_secure_connect(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get* until the entire response is retrieved. */

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);
    /* Process response packets… */
}
```

## <a name="http-and-https-server-api"></a>API server HTTP e HTTPS

## <a name="nx_web_http_server_cache_info_callback_set"></a>nx_web_http_server_cache_info_callback_set

Impostare il callback per recuperare la validità e la data ma massima dell'URL

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_cache_info_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT (*cache_info_get)(CHAR *resource,
    UINT *max_age,
    NX_WEB_HTTP_SERVER_DATE *date));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il servizio di callback richiamato per ottenere la durata massima e la data dell'ultima modifica della risorsa specificata.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **cache_info_get** Puntatore al callback
- **max_age** Puntatore alla durata massima di una risorsa
- **dati** Puntatore alla data dell'ultima modifica restituita.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente il callback
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione

### <a name="example"></a>Esempio

```C
NX_WEB_HTTP_SERVER my_server;

UINT cache_info_get(CHAR *resource, UINT *max_age,
    NX_WEB_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_web_http_server_create and before the HTTP
    server is set by nx_web_http_server_start(), set the cache info callback: */
status = nx_web_http_server_cache_info_callback_set(&my_server, cache_info_get);

/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_web_http_server_callback_data_send"></a>nx_web_http_server_callback_data_send

Inviare dati dalla funzione di callback

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_callback_data_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID *data_ptr, ULONG data_length);
```

### <a name="description"></a>Descrizione

Questo servizio invia i dati nel pacchetto fornito dalla routine di callback dell'applicazione. Viene in genere usato per inviare dati dinamici associati alle richieste GET/POST. Si noti che se si usa questa funzione, la routine di callback è responsabile dell'invio dell'intera risposta nel formato corretto. Inoltre, la routine di callback deve restituire lo stato di NX_WEB_HTTP_CALLBACK_COMPLETED.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **data_ptr** Puntatore ai dati da inviare.
- **data_length** Numero di byte da inviare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati del server sono stati inviati correttamente
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* Found it, override the GET processing by sending the resource
            contents directly. */
        nx_web_http_server_callback_data_send(server_ptr,
            "HTTP/1.0 200 \r\nContent-Length:" "103\r\nContent-Type: text/html\r\n\r\n",
            63);

        nx_web_http_server_callback_data_send(server_ptr, "<HTML>\r\n<HEAD><TITLE>NetX"
            "HTTP Test </TITLE></HEAD>\r\n"
            :<BODY>\r\n<H1>NetX Test Page"
            "</H1>\r\n</BODY>\r\n</HTML>\r\n", 103);

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_callback_generate_response_header"></a>nx_web_http_server_callback_generate_response_header

Creare un'intestazione di risposta in una funzione di callback

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_callback_generate_response_header(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    CHAR *status_code, UINT content_length,
    CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato nella routine di callback del server HTTP(S) (definita dall'applicazione) per generare un'intestazione di risposta HTTP. La routine di callback del server viene richiamata quando il server HTTP risponde alle richieste CLIENT GET, PUT e DELETE che richiedono una risposta HTTP. Questa funzione accetta le informazioni di risposta dall'applicazione e genera l'intestazione di risposta appropriata. Per altre informazioni sulla routine di callback delle richieste server, vedere il *nx_web_http_server_create()* del servizio.

Questa API è deprecata. Gli sviluppatori sono invitati a *usare nx_web_http_server_callback_generate_response_header_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **packet_pptr** Puntatore a un puntatore a pacchetto allocato per il messaggio
- **status_code** Indicare lo stato della risorsa. Esempi:
  - **NX_WEB_HTTP_STATUS_OK**
  - **NX_WEB_HTTP_STATUS_MODIFIED**
  - **NX_WEB_HTTP_STATUS_INTERNAL_ERROR**
- **content_length** Dimensioni del contenuto in byte
- **content_type** Tipo di HTTP, ad esempio "text/plain"
- **additional_header** Puntatore al testo aggiuntivo dell'intestazione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Intestazione HTML creata correttamente
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
CHAR demotestbuffer[] = "<html>> r\n\r\n<head>> r\n\r\n<title>Main \
    Window</title>> r\n</head>> r\n\r\n<body>Test message\r\n \ </body>> r\n</html>> r\n";

/* my_request_notify* is the application request notify callback registered
    with the HTTP server in *nx_web_http_server_create*,
    creates a response to the received Client request. */

UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET *resp_packet_ptr;
    ULONG string_length;
    CHAR temp_string[30];
    ULONG length = 0;
    length = strlen(&demotestbuffer[0]);

    /* Derive the client request type from the client request. */
    nx_web_http_server_type_extract(server_ptr,
        server_ptr -> nx_web_http_server_request_resource,
        temp_string, sizeof(temp_string), &string_length);

    /* Null terminate the string. */
    temp_string[string_length] = 0;

    /* Now build a response header with server status is OK and no additional header info. */
    status = nx_web_http_server_callback_generate_response_header(http_server_ptr,
        &resp_packet_ptr, NX_WEB_HTTP_STATUS_OK,
        length, temp_string, NX_NULL);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
    status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
        strlen(&demotestbuffer[0]), server_ptr >>
        nx_web_http_server_packet_pool_ptr, NX_WAIT_FOREVER);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
    status = nx_web_http_server_callback_packet_send(
        &(server_ptr -> nx_web_http_server_socket),
        resp_packet_ptr);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Let HTTP server know the response has been sent. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);
}
```

## <a name="nx_web_http_server_callback_generate_response_header_extended"></a>nx_web_http_server_callback_generate_response_header_extended

Creare un'intestazione di risposta in una funzione di callback

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_callback_generate_response_header_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    CHAR *status_code, UINT status_code_length,
    UINT content_length, CHAR *content_type,
    UINT content_type_length,
    CHAR* additional_header,
    UINT additional_header_length);
```

### <a name="description"></a>Descrizione

Questo servizio viene usato nella routine di callback del server HTTP(S) (definita dall'applicazione) per generare un'intestazione di risposta HTTP. La routine di callback del server viene richiamata quando il server HTTP risponde alle richieste CLIENT GET, PUT e DELETE che richiedono una risposta HTTP. Questa funzione accetta le informazioni di risposta dall'applicazione e genera l'intestazione di risposta appropriata. Per altre informazioni sulla routine di callback delle richieste server, vedere il *nx_web_http_server_create()* del servizio.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **packet_pptr** Puntatore a un puntatore a pacchetto allocato per il messaggio
- **status_code** Indicare lo stato della risorsa. Esempi:
  - **NX_WEB_HTTP_STATUS_OK**
  - **NX_WEB_HTTP_STATUS_MODIFIED**
  - **NX_WEB_HTTP_STATUS_INTERNAL_ERROR**
- **status_code_length** Lunghezza stringa del codice di stato
- **content_length** Dimensioni del contenuto in byte
- **content_type** Tipo di HTTP, ad esempio "text/plain"
- **content_type_length** Lunghezza stringa del tipo di contenuto
- **additional_header** Puntatore al testo aggiuntivo dell'intestazione
- **additional_header_length** Lunghezza del testo aggiuntivo dell'intestazione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Intestazione HTML creata correttamente
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
CHAR demotestbuffer[] = "<html>> r\n\r\n<head>> r\n\r\n<title>Main \
    Window</title>> r\n</head>> r\n\r\n<body>Test message\r\n \ </body>> r\n</html>> r\n";

/* my_request_notify* is the application request notify callback
    registered with the HTTP server in *nx_web_http_server_create*,
    creates a response to the received Client request. */

UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET *resp_packet_ptr;
    ULONG string_length;
    CHAR temp_string[30];
    ULONG length = 0;
    length = strlen(&demotestbuffer[0]);

    /* Derive the client request type from the client request. */
    nx_web_http_server_type_extract(server_ptr,
        server_ptr -> nx_web_http_server_request_resource,
        temp_string, sizeof(temp_string), &string_length);

    /* Null terminate the string. */
    temp_string[string_length] = 0;

    /* Now build a response header with server status is OK and no additional header info. */
    status = nx_web_http_server_callback_generate_response_header_extended(http_server_ptr,
        &resp_packet_ptr, NX_WEB_HTTP_STATUS_OK,
        sizeof(NX_WEB_HTTP_STATUS_OK) – 1,
        length, temp_string, string_length NX_NULL, 0);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
    status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
        strlen(&demotestbuffer[0]), server_ptr >>
        nx_web_http_server_packet_pool_ptr, NX_WAIT_FOREVER);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
    status = nx_web_http_server_callback_packet_send(
        &(server_ptr -> nx_web_http_server_socket),
        resp_packet_ptr);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Let HTTP server know the response has been sent. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);

}
```

## <a name="nx_web_http_server_callback_packet_send"></a>nx_web_http_server_callback_packet_send

Inviare un pacchetto HTTP dalla funzione di callback

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_callback_packet_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia una risposta completa del server HTTP da un callback HTTP. Il server HTTP invierà il pacchetto con il NX_WEB_HTTP_SERVER _TIMEOUT_SEND. L'intestazione HTTP e i dati devono essere aggiunti al pacchetto. Se lo stato restituito indica un errore, l'applicazione HTTP deve rilasciare il pacchetto.

Il callback deve restituire NX_WEB_HTTP_CALLBACK_COMPLETED.

Vedere *nx_web_http_server_callback_generate_response_header()* per un esempio più dettagliato.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP
- **packet_ptr** Puntatore al pacchetto da inviare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il pacchetto del server HTTP è stato inviato correttamente
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* The packet is appended with HTTP header and data
    and is ready to send to the Client directly. */
status = nx_web_http_server_callback_packet_send(server_ptr, packet_ptr);

if (status != NX_SUCCESS)
{
    nx_packet_release(packet_ptr);
}

return(NX_WEB_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_web_http_server_callback_response_send"></a>nx_web_http_server_callback_response_send

Inviare una risposta dalla funzione di callback

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_callback_response_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    CHAR *header,
    CHAR *information,
    CHAR additional_info);
```

### <a name="description"></a>Descrizione

Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione. Viene in genere usato per inviare risposte personalizzate associate alle richieste GET/POST. Si noti che se viene usata questa funzione, la routine di callback deve restituire lo stato di NX_WEB_HTTP_CALLBACK_COMPLETED.

questo servizio è deprecato. Gli sviluppatori sono invitati a *usare nx_web_http_server_callback_response_send_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **intestazione** Puntatore alla stringa di intestazione della risposta.
- **informazioni** Puntatore alla stringa di informazioni.
- **additional_info** Puntatore alla stringa di informazioni aggiuntive.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Risposta del server HTTP inviata correttamente

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
            a resource not found response. */
        nx_web_http_server_callback_response_send(server_ptr,
            "HTTP/1.0 404 ",
            "NetX HTTP Server unable to find file: ",
            resource);

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_callback_response_send_extended"></a>nx_web_http_server_callback_response_send_extended

Inviare una risposta dalla funzione di callback

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_callback_response_send_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    CHAR *header, UINT header_length,
    CHAR *information,
    UINT information_length,
    CHAR additional_info,
    UINT additional_info_length);
```

### <a name="description"></a>Descrizione

Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione. Viene in genere usato per inviare risposte personalizzate associate alle richieste GET/POST. Si noti che se viene usata questa funzione, la routine di callback deve restituire lo stato di NX_WEB_HTTP_CALLBACK_COMPLETED.

Le stringhe di intestazione, informazioni e additional_info devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.

Questo servizio sostituisce *nx_web_http_server_callback_response_send*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **intestazione** Puntatore alla stringa di intestazione della risposta.
- **header_length** Lunghezza della stringa di intestazione della risposta.
- **informazioni** Puntatore alla stringa di informazioni.
- **Information_length** Lunghezza della stringa di informazioni.
- **additional_info** Puntatore alla stringa di informazioni aggiuntive.
- **additional_info_length** Lunghezza della stringa di informazioni aggiuntive.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Risposta del server HTTP inviata correttamente

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
            a resource not found response. */
        nx_web_http_server_callback_response_send_extended(server_ptr,
            "HTTP/1.0 404 ",
            sizeof("HTTP/1.0 404 ") – 1,
            "NetX HTTP Server unable to find file: ",
            sizeof("NetX HTTP Server unable to find file: ") – 1,
            resource, strlen(resource));

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_content_get"></a>nx_web_http_server_content_get

Ottenere contenuto dalla richiesta

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_content_get(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr,
    ULONG byte_offset,
    CHAR *destination_ptr,
    UINT destination_size,
    UINT *actual_size);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di recuperare la quantità specificata di contenuto dalla richiesta del client HTTP POST o PUT. Deve essere chiamato dal callback di notifica delle richieste dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create()*).

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback di notifica della richiesta.
- **byte_offset** Numero di byte da offset nell'area del contenuto.
- **destination_ptr** Puntatore all'area di destinazione per il contenuto.
- **destination_size** Numero massimo di byte disponibili nell'area di destinazione.
- **actual_size** Puntatore alla variabile di destinazione che verrà impostata sulla dimensione effettiva del contenuto copiato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ottenere il contenuto del server HTTP riuscito
- **NX_WEB_HTTP_ERROR** (0x30000) Errore interno del server HTTP
- **NX_WEB_HTTP_DATA_END** (0x30007) Fine del contenuto della richiesta
- **NX_WEB_HTTP_TIMEOUT** (0x30001) timeout del server HTTP per ottenere il pacchetto di contenuto successivo
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Assuming we are in the application’s request notify callback
    routine, retrieve up to 100 bytes of content starting at offset
    0. */
status = nx_web_http_server_content_get(&my_server, packet_ptr,
    0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, "my_buffer" contains "actual_size" bytes of
    request content. */
```

## <a name="nx_web_http_server_content_get_extended"></a>nx_web_http_server_content_get_extended

Ottenere contenuto dalla richiesta/supporta lunghezza del contenuto di lunghezza zero

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_content_get_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr,
    ULONG byte_offset,
    CHAR *destination_ptr,
    UINT destination_size,
    UINT *actual_size);
```

### <a name="description"></a>Descrizione

Questo servizio è quasi identico a *nx_web_http_server_content_get()*; tenta di recuperare la quantità specificata di contenuto dalla richiesta client HTTP POST o PUT. Gestisce tuttavia le richieste con lunghezza del contenuto pari a zero ('richiesta vuota') come richiesta valida. Deve essere chiamato dal callback di notifica delle richieste dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create()*).

Questo servizio sostituisce *nx_web_http_server_content_get*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback di notifica della richiesta.
- **byte_offset** Numero di byte da offset nell'area del contenuto.
- **destination_ptr** Puntatore all'area di destinazione per il contenuto.
- **destination_size** Numero massimo di byte disponibili nell'area di destinazione.
- **actual_size** Puntatore alla variabile di destinazione che verrà impostata sulla dimensione effettiva del contenuto copiato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ottenere contenuto HTTP riuscito
- **NX_WEB_HTTP_ERROR** (0x30000) Errore interno del server HTTP
- **NX_WEB_HTTP_DATA_END** (0x30007) Fine del contenuto della richiesta
- **NX_WEB_HTTP_TIMEOUT** (0x30001) timeout del server HTTP per ottenere il pacchetto successivo
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Assuming we are in the application’s request notify callback
    routine, retrieve up to 100 bytes of content starting at offset
    0. */
status = nx_web_http_server_content_get_extended(&my_server, packet_ptr,
    0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, "my_buffer" contains "actual_size" bytes of
    request content. */
```

## <a name="nx_web_http_server_content_length_get"></a>nx_web_http_server_content_length_get

Ottenere la lunghezza del contenuto nella richiesta/supporta la lunghezza del contenuto pari a zero valore

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_content_length_get(
    NX_PACKET *packet_ptr,
    UINT *content_length);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito. Il valore restituito indica lo stato di completamento corretto e il valore della lunghezza effettiva viene restituito nel puntatore di input content_length. Se non è presente alcun contenuto HTTP/Lunghezza contenuto = 0, questa routine restituisce comunque uno stato di completamento corretto e il puntatore di input content_length punta a una lunghezza valida (zero). Deve essere chiamato dal callback di notifica delle richieste dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create()*).

### <a name="input-parameters"></a>Parametri di input

- **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback di notifica della richiesta.
- **content_length** Puntatore al valore recuperato dal campo Lunghezza contenuto

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ottiene la lunghezza del contenuto del server HTTP riuscita
- **NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) Formato di intestazione HTTP non corretto
- NX_PTR_ERROR (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Assuming we are in the application’s request notify callback
    routine, get the content length of the HTTP Client request. */

ULONG content_length;
status = nx_web_http_server_content_length_get(packet_ptr, &content_length);

/* If the "status" variable indicates successful completion, the "length"
    Variable contains the length of the HTTP Client request content area. */
```

## <a name="nx_web_http_server_create"></a>nx_web_http_server_create

Creare un'istanza del server HTTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_create(NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *http_server_name, NX_IP *ip_ptr, UINT server_port,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*authentication_check)(NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type, CHAR *resource, CHAR **name,
        CHAR **password, CHAR **realm),
    UINT (*request_notify)(NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server HTTP, che viene eseguita nel contesto del proprio thread ThreadX. Le routine *authentication_check* e *request_notify* callback dell'applicazione offrono all'applicazione il controllo software sulle operazioni di base del server HTTP.

Questo servizio viene usato per creare sia server HTTP in testo non crittografato che server HTTPS protetti da TLS. Per abilitare HTTPS tramite TLS, vedere il servizio *nx_web_http_server_secure_configure()*.

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore al blocco di controllo del server HTTP.
- **http_server_name** Puntatore al nome del server HTTP.
- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **server_port** Porta di ascolto TCP per l'istanza del server.
- **media_ptr** Puntatore all'istanza del supporto FileX creata in precedenza.
- **stack_ptr** Puntatore all'area dello stack di thread del server HTTP.
- **stack_size** Puntatore alle dimensioni dello stack dei thread del server HTTP.
- **authentication_check** Puntatore a funzione alla routine di controllo dell'autenticazione dell'applicazione. Se specificato, questa routine viene chiamata per ogni richiesta del client HTTP. Se questo parametro è NULL, non verrà eseguita alcuna autenticazione. Questo parametro è deprecato. Chiamare *invece nx_web_http_server_authenticate_check_set*() .
- **request_notify** Puntatore a funzione alla routine di notifica della richiesta dell'applicazione. Se specificato, questa routine viene chiamata prima dell'elaborazione del server HTTP della richiesta. In questo modo è possibile reindirizzare il nome della risorsa o aggiornare i campi all'interno di una risorsa prima di completare la richiesta del client HTTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione del server HTTP completata.
- NX_PTR_ERROR (0x07) Puntatore del server HTTP, IP, supporto, stack o pool di pacchetti non valido.
- NX_WEB_HTTP_POOL_ERROR (0x30009) Il payload del pacchetto del pool non è sufficientemente grande da contenere una richiesta HTTP completa.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Create an HTTP Server instance called "my_server." */
status = nx_web_http_server_create(&my_server, "my server", &ip_0,
    NX_WEB_HTTPS_SERVER_PORT, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_web_http_server_delete"></a>nx_web_http_server_delete

Eliminare un'istanza del server HTTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_delete(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del server HTTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore al blocco di controllo del server HTTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del server HTTP riuscita
- NX_PTR_ERROR (0x07) Puntatore server HTTP non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the HTTP Server instance called "my_server." */
status = nx_web_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_web_http_server_get_entity_content"></a>nx_web_http_server_get_entity_content

Recuperare la posizione e la lunghezza dei dati dell'entità

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_get_entity_content(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    ULONG *available_offset,
    ULONG *available_length);
```

### <a name="description"></a>Descrizione

Questo servizio determina la posizione dell'inizio dei dati all'interno dell'entità multipart corrente nei messaggi client ricevuti e la lunghezza dei dati che non includono la stringa limite. Internamente, il server HTTP aggiorna i propri offset in modo che questa funzione possa essere chiamata nuovamente nello stesso datagramma client per i messaggi con più entità. Il puntatore a pacchetto viene aggiornato al pacchetto successivo in cui il messaggio client è un datagramma a più pacchetti.

Si noti NX_WEB_HTTP_MULTIPART_ENABLE deve essere abilitato per usare questo servizio. Si noti anche che l'applicazione non deve rilasciare il pacchetto a cui punta packet_pptr. Questa operazione viene eseguita internamente dal server HTTP.

Per *altri dettagli, vedere nx_web_http_server_get_entity_header()* .

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al server HTTP
- **packet_pptr** Puntatore alla posizione del puntatore a pacchetto. Si noti che l'applicazione non deve rilasciare questo pacchetto
- **available_offset** Puntatore all'offset dei dati di entità dal puntatore anteposto al pacchetto
- **available_length** Puntatore alla lunghezza dei dati di entità

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Le dimensioni e la posizione del contenuto dell'entità sono state recuperate correttamente
- **NX_WEB_HTTP_BOUNDARY_ALREADY_FOUND** (0x30016) Il contenuto per i marcatori multipart interni del server HTTP è già stato trovato
- NX_WEB_HTTP_ERROR (0x30000) Errore interno del server HTTP
- NX_PTR_ERROR (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_WEB_HTTP_SERVER my_server;
UINT offset, length;
NX_PACKET *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
    the entity header to determine details about the multipart data. If
    successful, it then calls this service to get the location of entity data: */
status = nx_web_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
    &length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
    entity data. */
```

## <a name="nx_web_http_server_get_entity_header"></a>nx_web_http_server_get_entity_header

Recuperare il contenuto dell'intestazione di entità

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_get_entity_header(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    UCHAR *entity_header_buffer,
    ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'intestazione dell'entità nel buffer specificato. Il server HTTP internamente aggiorna i propri puntatori per individuare l'entità multipart successiva in un datagramma client con più intestazioni di entità. Il puntatore a pacchetto viene aggiornato al pacchetto successivo in cui il messaggio client è un datagramma a più pacchetti.

Si noti NX_WEB_HTTP_MULTIPART_ENABLE deve essere abilitato per usare questo servizio. Si noti anche che l'applicazione non deve rilasciare il pacchetto a cui punta packet_pptr.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al server HTTP
- **packet_pptr** Puntatore alla posizione del puntatore a pacchetto. Si noti che l'applicazione non deve rilasciare questo pacchetto
- **entity_header_buffer** Puntatore alla posizione in cui archiviare l'intestazione dell'entità
- **buffer_size** Dimensioni del buffer di input

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'intestazione dell'entità è stata recuperata correttamente
- **NX_WEB_HTTP_NOT_FOUND** (0x30006) Campo intestazione entità non trovato
- **NX_WEB_HTTP_TIMEOUT** (0x30001) Tempo scaduto per ricevere il pacchetto successivo per il messaggio client multipacket
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_WEB_HTTP_ERROR (0x30000) Errore HTTP interno

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Buffer to hold data we are extracting from the request. */
UCHAR buffer[1440];

/* *my_request_notify()* is the application request notify callback
    registered with the HTTP server in *nx_web_http_server_create()*,
    creates a response to the received Client request. */
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    UINT offset, length;
    NX_PACKET *response_pkt;

    /* Process multipart data. */
    if(request_type == NX_WEB_HTTP_SERVER_POST_REQUEST)
    {
        /* Get the content header. */
        while(nx_web_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
            sizeof(buffer)) == NX_SUCCESS)
        {
            /* Header obtained successfully. Get the content data location. */
            while(nx_web_http_server_get_entity_content(server_ptr,
                &packet_ptr, &offset, &length) == NX_SUCCESS)
            {
                /* Write content data to buffer. */
                nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                    &length);
                buffer[length] = 0;
            }
        }

        /* Generate HTTP header. */
        status = nx_web_http_server_callback_generate_response_header(server_ptr,
            &response_pkt, NX_WEB_HTTP_STATUS_OK, 800, "text/html",
            "Server: NetX WEB HTTP 5.10\r\n");

        if(status == NX_SUCCESS)
        {
            if(nx_web_http_server_callback_packet_send(server_ptr, response_pkt) !=
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
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);
}

```

## <a name="nx_web_http_server_gmt_callback_set"></a>nx_web_http_server_gmt_callback_set

Impostare il callback per ottenere data e ora GMT

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_gmt_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID (*gmt_get)(NX_WEB_HTTP_SERVER_DATE *date);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback per ottenere data e ora GMT con un server HTTP creato in precedenza. Questo servizio viene richiamato con il server HTTP che crea un'intestazione nelle risposte del server HTTP al client.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al server HTTP
- **gmt_get** Puntatore al callback GMT
- **date** Puntatore alla data recuperata

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente il callback
- NX_PTR_ERROR (0x07) Puntatore a parametro o pacchetto non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_WEB_HTTP_SERVER my_server;

VOID get_gmt(NX_WEB_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_web_http_server_create(),
    and before starting HTTP services when nx_web_http_server_start() is called,
    set the GMT retrieve callback: */
status = nx_web_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
    response header date. */
```

## <a name="nx_web_http_server_invalid_userpassword_notify_set"></a>nx_web_http_server_invalid_userpassword_notify_set

Impostare il callback per gestire utente/password non validi

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_invalid_userpassword_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*invalid_username_password_callback)
        (CHAR *resource,
        ULONG client_address,
        UINT request_type));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback richiamato quando viene ricevuto un nome utente e una password non validi in una richiesta Client get, put o delete, tramite l'autenticazione digest o di base. Il server HTTP deve essere creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al server HTTP
- **invalid_username_password_callback** Puntatore a un callback utente/passaggio non valido
- **risorsa** Puntatore alla risorsa specificata dal client
- **client_address** Indirizzo client
- **request_type** Indica il tipo di richiesta client. Può essere:
  - *NX_WEB_HTTP_SERVER_GET_REQUEST*
  - *NX_WEB_HTTP_SERVER_POST_REQUEST NX_WEB_HTTP_SERVER_HEAD_REQUEST*
  - *NX_WEB_HTTP_SERVER_PUT_REQUEST NX_WEB_HTTP_SERVER_DELETE_REQUEST*

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente il callback
- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_WEB_HTTP_SERVER my_server;

VOID invalid_username_password_callback(NX_CHAR *resource,
    ULONG client_address,
    UINT request_type);

/* After the HTTP server is created by calling nx_web_http_server_create,
    and before starting HTTP services when nx_web_http_server_start() is called,
    set the invalid username password callback: */

status = nx_web_http_server_invalid_userpassword_notify_set( (&my_server,
    invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
    will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_web_http_server_mime_maps_additional_set"></a>nx_web_http_server_mime_maps_additional_set

Impostare mappe MIME aggiuntive per HTML

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_mime_maps_additional_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_WEB_HTTP_SERVER_MIME_MAP *mime_maps,
    UINT mime_maps_num);
```

### <a name="description"></a>Descrizione

Questo servizio consente allo sviluppatore di applicazioni HTTP di aggiungere altri tipi MIME dai tipi MIME predefiniti forniti dal server HTTP Web NetX. Vedere *nx_web_http_server_get_type() per* l'elenco dei tipi definiti.

Quando viene ricevuta una richiesta client, ad esempio una richiesta GET, il server HTTP analizza il tipo di file richiesto dall'intestazione HTTP usando preferibilmente il set di mapping MIME aggiuntivo e, se non viene trovata alcuna corrispondenza, cerca una corrispondenza nella mappa MIME predefinita del server HTTP. Se non viene trovata alcuna corrispondenza, per impostazione predefinita il tipo MIME è "text/plain".

Se la funzione request notify è registrata con il server HTTP, il callback di notifica della richiesta può chiamare *nx_web_http_server_type_get_extended()* per analizzare il tipo di file.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore all'istanza del server HTTP
- **mime_maps** Puntatore a una matrice di mappe MIME
- **mime_map_num** Numero di mappe MIME nella matrice

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) set di mapping MIME server HTTP riuscito
- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* my_server is an NX_WEB_HTTP_SERVER previously created. */
static NX_WEB_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc", "yourtype/abc"},
    {"xyz", "mytype/xyz"},
};

status = nx_web_http_server_mime_maps_additional_set(&my_server,
    &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP
    server MIME map set." */
```

## <a name="nx_web_http_server_response_packet_allocate"></a>nx_web_http_server_response_packet_allocate

Allocare un pacchetto HTTP(S)

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_response_packet_allocate(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di allocare un pacchetto per il server HTTP(S).

Si noti che se un'API NetX o HTTP Server successiva che usa questo pacchetto come **input** ha esito negativo, ad esempio nx_packet_data_append o **nx_web_http_server_callback_packet_send, l'applicazione è responsabile del rilascio del pacchetto. **

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al blocco di controllo del server HTTP.
- **packet_ptr** Puntatore al pacchetto allocato.
- **wait_option** Definisce il tempo di attesa in tick se non sono disponibili pacchetti nel pool di pacchetti. Le opzioni di attesa sono definite come segue:
  - **NX_NO_WAIT** (0x00000000) Se si NX_NO_WAIT il thread chiamante viene restituito immediatamente se la richiesta non può essere soddisfatta.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) La selezione NX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.
  - **valore** di timeout (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Corretta allocazione pacchetti
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a *tx_thread_wait_abort*.
- **NX_INVALID_PARAMETERS** (0x4D) Le dimensioni del pacchetto non supportano il protocollo.
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Allocate a packet for HTTP(S) Server and suspend for a maximum of 5 timer
    ticks if the pool is empty. */
status = nx_web_http_server_response_packet_allocate(&my_client, &packet_ptr, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
    variable packet_ptr. */
```

## <a name="nx_web_http_server_packet_content_find"></a>nx_web_http_server_packet_content_find

Estrarre la lunghezza del contenuto e impostare il puntatore all'inizio dei dati

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_packet_content_find(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr,
    UINT *content_length);
```

### <a name="description"></a>Descrizione

Questo servizio estrae la lunghezza del contenuto dall'intestazione HTTP. Aggiorna anche il pacchetto fornito nel modo seguente: il puntatore anteposto al pacchetto (inizio della posizione del buffer di pacchetti in cui scrivere) viene impostato sul contenuto HTTP (dati) appena passato all'intestazione HTTP.

Se l'inizio del contenuto non viene trovato nel pacchetto corrente, la funzione attende che il pacchetto successivo sia ricevuto usando l'opzione NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE wait.

Si noti che non deve essere chiamato *prima di chiamare nx_web_http_server_get_entity_header()* perché modifica il puntatore anteposto al pacchetto dopo l'intestazione dell'entità.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore all'istanza del server HTTP
- **packet_ptr** Puntatore al puntatore al pacchetto per la restituzione del pacchetto con puntatore anteposto aggiornato
- **content_length** Puntatore ai dati content_length

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** contenuto HTTP (0x00) trovato e il pacchetto è stato aggiornato correttamente
- **NX_WEB_HTTP_TIMEOUT** (0x30001) Tempo scaduto in attesa del pacchetto successivo
- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
    The server has received a Client request packet, recv_packet_ptr,
    and the packet content find service is called from the request notify callback
    function registered with the HTTP server. */

UINT content_length;

status = nx_web_http_server_packet_content_find(server_ptr, recv_packet_ptr,
    &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
    and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_web_http_server_packet_get"></a>nx_web_http_server_packet_get

Ricevere il pacchetto HTTP successivo

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_packet_get(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il pacchetto successivo ricevuto sul socket del server HTTP. L'opzione wait per ricevere un pacchetto è NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE.

Si noti che, in caso di esito positivo, l'applicazione è responsabile del rilascio del pacchetto.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore all'istanza del server HTTP
- **packet_ptr** Puntatore al pacchetto ricevuto

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ricevuto pacchetto HTTP successivo
- **NX_WEB_HTTP_TIMEOUT** (0x30001) Tempo scaduto in attesa del pacchetto successivo
- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* The HTTP server pointed to by server_ptr is previously created and started. */
UINT content_length;
NX_PACKET *recv_packet_ptr;

status = nx_web_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_web_http_server_param_get"></a>nx_web_http_server_param_get

Ottenere il parametro dalla richiesta

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_param_get(NX_PACKET *packet_ptr,
    UINT param_number, CHAR *param_ptr,
    UINT *param_size, UINT max_param_size);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di recuperare il parametro URL HTTP specificato nel pacchetto di richiesta fornito. Se il parametro HTTP richiesto non è presente, questa routine restituisce lo stato NX_WEB_HTTP_NOT_FOUND. Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create()*).

### <a name="input-parameters"></a>Parametri di input

- **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che l'applicazione non deve rilasciare questo pacchetto.
- **param_number** Numero logico del parametro che inizia da zero, da sinistra a destra nell'elenco di parametri.
- **param_ptr** Area di destinazione in cui copiare il parametro.
- **param_size** Restituisce la lunghezza totale dei dati del parametro (in byte).
- **max_param_size** Dimensioni massime dell'area di destinazione del parametro.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successful HTTP Server parameter get
- **NX_WEB_HTTP_NOT_FOUND** (0x30006) Parametro specificato non trovato
- **NX_WEB_HTTP_IMPROPERLY_TERMINATED_PARAM** (0x30015) Request parameter not properly terminated (Il parametro di richiesta (0x30015) non è stato terminato correttamente
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Assuming we are in the application’s request notify callback
    routine, get the first parameter of the HTTP Client request. */

status = nx_web_http_server_param_get(request_packet_ptr, 0, param_destination,
    &param_size, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
    in "param_destination" and the size of that string can be found
    in the variable "param_size." */
```

## <a name="nx_web_http_server_query_get"></a>nx_web_http_server_query_get

Ottenere una query dalla richiesta

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_query_get(NX_PACKET *packet_ptr,
    UINT query_number,
    CHAR *query_ptr,
    CHAR *query_size,
    UINT max_query_size);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di recuperare la query dell'URL HTTP specificata nel pacchetto di richiesta fornito. Se la query HTTP richiesta non è presente, questa routine restituisce lo stato NX_WEB_HTTP_NOT_FOUND. Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create()*).

### <a name="input-parameters"></a>Parametri di input

- **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che l'applicazione non deve rilasciare questo pacchetto.
- **query_number** Numero logico del parametro che inizia da zero, da sinistra a destra nell'elenco di query.
- **query_ptr** Area di destinazione in cui copiare la query.
- **query_size** Restituisce le dimensioni dei dati della query (in byte).
- **max_query_size** Dimensioni massime della destinazione della query

quell'area.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Query del server HTTP riuscita
- **NX_WEB_HTTP_FAILED** (0x30002) Dimensioni query troppo piccole.
- **NX_WEB_HTTP_NOT_FOUND** (0x30006) Query specificata non trovata
- **NX_WEB_HTTP_NO_QUERY_PARSED** (0x30013) Nessuna query nella richiesta client
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Assuming we are in the application’s request notify callback
    routine, get the first query of the HTTP Client request. */

status = nx_web_http_server_query_get(request_packet_ptr, 0,
    query_destination, &query_size, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
    in "query_destination" and the length of that string can be found in the
    variable "query_size". */
```

## <a name="nx_web_http_server_response_chunked_set"></a>nx_web_http_server_response_chunked_set

Impostare il trasferimento in blocchi per la risposta HTTP(S)

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_response_chunked_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT chunk_size, NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio usa la codifica di trasferimento in blocchi per inviare un pacchetto di dati di risposta HTTP(S) personalizzato creato *con nx_web_http_server_response_packet_allocate*() al client.

> [!NOTE]
> Se l'applicazione usa la codifica di trasferimento in blocchi per inviare un pacchetto di dati di risposta, deve chiamare questo servizio *dopo* aver chiamato nx_web_http_server_response_packet_allocate () e prima di nx_web_http_server_callback_packet_send *().*

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client HTTP.
- **chunk_size** Dimensioni dei dati in blocchi in ottetti.
- **packet_ptr** Puntatore al pacchetto di dati della richiesta HTTP(S).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Set completato in blocchi.
- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Generate HTTP header. */
nx_web_http_server_callback_generate_response_header(server_ptr,
    &response_pkt, NX_WEB_HTTP_STATUS_OK, 0, "text/html",
    "Transfer-Encoding: chunked\r\n");

/* Create a new data packet response on the HTTP(S) Server instance. */
nx_web_http_server_response_packet_allocate(&my_server, &my_packet, NX_WAIT_FOREVER);

/* Set the chunked transfer. */
status = nx_web_http_server_response_chunked_set(&my_server, 128, my_packet)

/* At this point, user can fill the data into my_packet. */
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet response to client. */
nx_web_http_server_callback_packet_send(&my_server, my_packet);
```

## <a name="nx_web_http_server_secure_configure"></a>nx_web_http_server_secure_configure

Configurare un server HTTP per l'uso di TLS per HTTPS sicuro

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_secure_configure(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    const NX_SECURE_TLS_CRYPTO *crypto_table,
    VOID *metadata_buffer, ULONG metadata_size,
    UCHAR* packet_buffer, UINT packet_buffer_size,
    NX_SECURE_X509_CERT *identity_certificate,
    NX_SECURE_X509_CERT *trusted_certificates[],
    UINT trusted_certs_num,
    NX_SECURE_X509_CERT *remote_certificates[],
    UINT remote_certs_num,
    UCHAR *remote_certificate_buffer,
    UINT remote_cert_buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio configura un'istanza del server HTTP Web NetX creata in precedenza per l'uso di TLS per le comunicazioni HTTPS sicure. I parametri vengono usati per configurare tutte le sessioni TLS possibili con stato identico in modo che ogni client HTTPS in ingresso presenti un comportamento coerente. Il numero di sessioni TLS viene controllato usando la macro NX_WEB_HTTP_SESSION_MAX.

La tabella di routine crittografica (tabella ciphersuite) viene condivisa tra tutte le sessioni TLS perché contiene solo puntatori a funzione.

I buffer di riassemblaggio dei metadati e dei pacchetti sono divisi equamente tra tutte le sessioni TLS. Se le dimensioni del buffer non sono divisibile in modo uniforme per il numero di sessioni, il resto non verrà usato.

Il certificato di identità passato viene usato da tutte le sessioni. Durante l'operazione TLS, il certificato di identità del server viene letto solo da , quindi le copie non sono necessarie per ogni sessione.

I certificati attendibili vengono aggiunti a ogni sessione TLS nel server HTTPS. Questi vengono usati per l'autenticazione del certificato client che viene abilitata automaticamente quando viene fornito spazio del certificato remoto.

La matrice di certificati remoti e il buffer sono condivisi per impostazione predefinita tra tutte le sessioni TLS. I certificati remoti vengono usati per l'autenticazione del certificato client che viene abilitata automaticamente quando il numero di certificati remoti è diverso da zero. A causa della condivisione del buffer, alcune sessioni possono bloccarsi durante la convalida del certificato.

Per disabilitare l'autenticazione del certificato client, passare NX_NULL per il parametro remote_certificates e il valore 0 per il parametro remote_certs_num.

I valori restituiti includeranno tutti i codici di errore TLS risultanti da problemi nella configurazione delle sessioni TLS.

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore all'istanza del server HTTP.
- **crypto_table** Puntatore alla tabella di crittografia TLS.
- **metadata_buffer** Puntatore al buffer dei metadati crittografici.
- **metadata_size** Dimensioni del buffer dei metadati crittografici.
- **packet_buffer** Buffer di riassemblaggio dei pacchetti TLS.
- **packet_buffer** Dimensione del buffer di pacchetti TLS: deve essere uguale a (<dimensioni del buffer TLS* NX_WEB_HTTP_SESSION_MAX).
- **identity_certificate** Certificato di identità del server TLS: verrà usato per tutte le sessioni del server HTTPS.
- **trusted_certificates** Puntatore alla matrice di NX_SECURE_X509_CERT, utilizzato per convalidare i certificati client in ingresso se l'autenticazione del certificato client è abilitata passando un valore diverso da zero per il *parametro remote_certs_num.*
- **trusted_certs_num** Numero di certificati attendibili nella *matrice trusted_certificates.*
- **remote_certificates** Puntatore alla matrice di NX_SECURE_X509_CERT, utilizzato per i certificati client in ingresso.
- **remote_certs_num** Numero di certificati remoti. Deve essere il numero massimo di certificati previsti dai client. L'autenticazione del certificato client viene abilitata automaticamente quando è diverso da zero.
- **remote_certificate_buffer** Buffer per contenere i certificati remoti in ingresso dai client se è abilitata l'autenticazione del certificato client. remote_cert_buffer_size dimensioni del buffer dei certificati remoti. Deve essere uguale a (<dimensioni massime previste del \* certificato remote_certs_num).


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.
- **NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Un tipo di messaggio TLS ricevuto non è corretto.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) Una crittografia fornita dall'host remoto non è supportata.
- **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) L'elaborazione del messaggio durante l'handshake TLS non è riuscita.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Un messaggio in arrivo non ha superato un controllo MAC hash.
- **NX_SECURE_TLS_TCP_SEND_FAILE** (0x109) L'invio di un socket TCP sottostante non è riuscito.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Un messaggio in arrivo ha un campo di lunghezza non valido.
- **NX_SECURE_TLS_BAD_CIPHERSPE** (0x10B) Un messaggio ChangeCipherSpec in ingresso non è corretto.
- **NX_SECURE_TLS_INVALID_SERVER_CER** (0x10C) Un certificato TLS in ingresso non è utilizzabile per identificare il server TLS remoto.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) La crittografia a chiave pubblica fornita dall'host remoto non è supportata.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) L'host remoto non ha indicato ciphersuit supportati dallo stack NETX Secure TLS.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Un messaggio TLS ricevuto ha una versione TLS sconosciuta nell'intestazione.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Un messaggio TLS ricevuto aveva una versione TLS nota ma non supportata nell'intestazione.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Un'allocazione interna di pacchetti TLS non è riuscita.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) L'host remoto ha fornito un certificato non valido.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) L'host remoto ha inviato un avviso che indica un errore e termina la sessione TLS.
- **NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Create the HTTPS Server. */

status = nx_web_http_server_create(&my_server, "My HTTP Server",
    &ip_0, &ram_disk, &server_stack, sizeof(server_stack),
    &pool_0, authentication_check, server_request_callback);

/* Initialize device certificate (used for all sessions in HTTPS server). */
nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
    device_cert_der_len, NX_NULL, 0,
    device_cert_key_der, device_cert_key_der_len,
    NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

/* Setup TLS session for the HTTPS server.
    Note that since the remote_certs_num parameter is 0,
    no trusted certificates are needed, and Client certificate authentication is disabled. */
status = nx_web_http_server_secure_configure(&my_server, &nx_crypto_tls_ciphers,
    crypto_metadata,
    sizeof(crypto_metadata),
    tls_packet_buffer, sizeof(tls_packet_buffer),
    &certificate, NX_NULL, 0, NX_NULL, 0, NX_NULL, 0);

/* Start an HTTPS Server with TLS. */
status = nx_web_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_web_http_server_start"></a>nx_web_http_server_start

Avviare il server HTTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_start(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia un'istanza del server HTTP o HTTPS creata in precedenza.

I server HTTPS condividono la stessa API di HTTP. Per abilitare HTTPS usando TLS in un server HTTP, vedere il servizio *nx_web_http_server_secure_configure().*

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore all'istanza del server HTTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Avvio del server HTTP riuscito
- NX_PTR_ERROR (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Start the HTTP Server instance "my_server." */
status = nx_web_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_web_http_server_stop"></a>nx_web_http_server_stop

Arrestare il server HTTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_stop(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta l'istanza del server HTTP creata in precedenza. Questa routine deve essere chiamata prima di eliminare un'istanza del server HTTP.

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore all'istanza del server HTTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Arresto del server HTTP riuscito
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop the HTTP Server instance "my_server." */
status = nx_web_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_web_http_server_type_get"></a>nx_web_http_server_type_get

Estrarre il tipo di file dalla richiesta HTTP client

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_type_get(NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *name, CHAR *http_type_string,
    UINT *string_size);
```

### <a name="description"></a>Descrizione

> [!NOTE]
> questo servizio è deprecato. Gli utenti sono invitati a usare il *servizio nx_web_http_server_type_get_extended()*.

Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la relativa lunghezza *in* string_size dal nome *del* buffer di input, in genere l'URL. Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene utilizzato il tipo "text/plain". In caso contrario, confronta il tipo estratto con i mapping MIME predefiniti del server HTTP per trovare una corrispondenza. Le mappe MIME predefinite nel server HTTP Web NetX sono:

- html text/html
- htm text/html
- txt text/plain
- gif image/gif
- jpg image/jpeg
- ico image/x-icon

Se specificato, esegue anche la ricerca in un set definito dall'utente di mappe MIME aggiuntive. Vedere *nx_web_http_server_mime_maps_addtional_set() per* altri dettagli sulle mappe definite dall'utente.

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore all'istanza del server HTTP
- **name** Puntatore al buffer da cercare
- **http_type_string** Puntatore alla stringa di tipo HTML estratta
- **string_size** Puntatore per restituire la lunghezza della stringa di tipo HTML estratto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Estrazione riuscita del tipo
- NX_PTR_ERROR (0x07) Input puntatore non valido
- **NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) Restituito "text/plain" predefinito.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```C
/* my_server is a previously created HTTP server, which starts accepting client
    requests when *nx_web_http_server_start* is called */

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
string_length = nx_web_http_server_type_get(&my_server_ptr,
    my_server.nx_web_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
    For a more detailed example, see the description for
    *nx_web_http_server_callback_generate_response_header().*
```

## <a name="nx_web_http_server_type_get_extended"></a>nx_web_http_server_type_get_extended

Estrarre il tipo di file dalla richiesta HTTP client

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_type_get_extended(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *name, UINT name_length,
    CHAR *http_type_string,
    UINT http_type_string_max_size,
    UINT *string_size);
```

### <a name="description"></a>Descrizione

Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la relativa lunghezza *in* string_size dal nome *del* buffer di input, in genere l'URL. Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene utilizzato il tipo "text/plain". In caso contrario, confronta il tipo estratto con i mapping MIME predefiniti del server HTTP per trovare una corrispondenza. Le mappe MIME predefinite nel server HTTP Web NetX sono:

- html text/html
- htm text/html
- txt text/plain
- gif image/gif
- jpg image/jpeg
- ico image/x-icon

Se specificato, esegue anche la ricerca in un set definito dall'utente di mappe MIME aggiuntive. Vedere *nx_web_http_server_mime_maps_addtional_set() per* altri dettagli sulle mappe definite dall'utente.

Questo servizio sostituisce *nx_web_http_server_type_get*(). Questa versione richiede ai chiamanti di fornire informazioni sulla lunghezza alla funzione.

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore all'istanza del server HTTP
- **name** Puntatore al buffer da cercare
- **name_length** Lunghezza del nome
- **http_type_string** Puntatore alla stringa di tipo HTML estratta
- **http_type_string_max_size** Dimensioni della dimensione http_type_string buffer
- **string_size** Puntatore per restituire una stringa di tipo HTML estratto

Lunghezza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Estrazione riuscita del tipo
- NX_PTR_ERROR (0x07) Input puntatore non valido
- **NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) Restituito "text/plain" predefinito.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```C
/* my_server is a previously created HTTP server, which starts accepting client
    requests when *nx_web_http_server_start* is called */

CHAR temp_string[20];
UINT string_length;
UINT ret;

/* Extract the HTTP type. */
ret = nx_web_http_server_type_get_extended(&my_server_ptr,
    my_server.nx_web_http_server_request_resource,
    strlen(my_server.nx_web_http_server_request_resource),
    temp_string,sizeof(temp_string), &string_length);

/* If string_length is non zero, the HTTP string is extracted. */
    For a more detailed example, see the description for
    *nx_web_http_server_callback_generate_response_header().*
```

## <a name="nx_web_http_server_digest_authenticate_notify_set"></a>nx_web_http_server_digest_authenticate_notify_set

Impostare la funzione di callback di autenticazione digest

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_digest_authenticate_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*digest_authenticate_callback)(NX_WEB_HTTP_SERVER *server_ptr,
        CHAR *name_ptr,
        CHAR *realm_ptr,
        CHAR *password_ptr,
        CHAR *method,
        CHAR *authorization_uri,
        CHAR *authorization_nc,
        CHAR *authorization_cnonce));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback richiamato quando viene eseguita l'autenticazione del digest.

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore all'istanza del server HTTP
- **digest_authenticate_callback** Puntatore al callback di autenticazione digest

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente il callback
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_NOT_SUPPORTED (0x4B) L'autenticazione del digest non è abilitata

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```C
UINT digest_authenticate_callback(NX_WEB_HTTP_SERVER *server_ptr, CHAR *name_ptr,
    CHAR *realm_ptr, CHAR *password_ptr, CHAR *method,
    CHAR *authorization_uri, CHAR *authorization_nc,
    CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_WEB_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_web_http_server_create, and
    before starting HTTP services when nx_web_http_server_start is called, set the digest authenticate callback: */
status = nx_web_http_server_digest_authenticate_notify_set(&my_server,
    digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
    will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_web_http_server_authenticate_check_set"></a>nx_web_http_server_authenticate_check_set

Impostare la funzione di callback di autenticazione digest

### <a name="prototype"></a>Prototipo

```C
UINT nx_web_http_server_digest_authenticate_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*authentication_check_extended)(
        NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type,
        CHAR *resource,
        CHAR **name,
        UINT *name_length,
        CHAR **password,
        UINT password_length,
        CHAR **realm,
        UINT *realm_length));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback richiamato quando viene eseguito il controllo di autenticazione.

### <a name="input-parameters"></a>Parametri di input

- **http_server_ptr** Puntatore all'istanza del server HTTP
- **authenticate_check_externded** Puntatore per autenticare il callback di controllo

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente il callback
- NX_PTR_ERROR (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```C
UINT authenticate_check_callback(NX_WEB_HTTP_SERVER *server_ptr,
    UINT request_type,
    CHAR *name_ptr, UCHAR *resource, UCHAR **name,
    UINT *name_length, UCHAR **password,
    UINT *password_length, UCHAR **realm,
    UINT *realm_length)
{
    *name = "name";
    *name_length = 4;
    *password = "password";
    *password_length = 8;
    *realm = "realm";
    *realm_length = 5;
    return(NX_SUCCESS);
}

NX_WEB_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_web_http_server_create, and
    before starting HTTP services when nx_web_http_server_start is called, set the authenticate check callback: */

status = nx_web_http_digest_authenticate_check_set (&my_server,
    authenticate_check_callback);

/* If status equals NX_SUCCESS, the authenticate_check_callback function
    will be called when the HTTP server performs authenticate check. */
```
