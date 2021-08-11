---
title: Capitolo 3 - Descrizione dei Azure RTOS HTTP NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi HTTP di NetX Duo Azure RTOS (elencati di seguito) in ordine alfabetico, ad eccezione dell'equivalente "NetX" (solo IPv4) dello stesso servizio.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 09add7bb20a8e104ba41583c0dbf4d574b8e6c9e6b3a3deed71d8fa8c8942ce2
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796481"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-http-services"></a>Capitolo 3 - Descrizione dei Azure RTOS HTTP NetX Duo

Questo capitolo contiene una descrizione di tutti i servizi HTTP di NetX Duo Azure RTOS (elencati di seguito) in ordine alfabetico, ad eccezione dell'equivalente "NetX" (solo IPv4) dello stesso servizio.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in grassetto non sono interessati dalla definizione **di NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

**Servizi client HTTP:**

- **nx_http_client_create** *creare un'istanza del client HTTP*
- **nx_http_client_delete** *un'istanza del client HTTP*
- **nx_http_client_get_start** *avviare una richiesta HTTP GET (solo IPv4)*
- **nx_http_client_get_start_extended** *avviare una richiesta HTTP GET (solo IPv4)*
- **nxd_http_client_get_start** *avviare una richiesta HTTP GET (IPv4 o IPv6)*
- **nxd_http_client_get_start_extended** *avviare una richiesta HTTP GET (IPv4 o IPv6)*
- **nx_http_client_get_packet** *ottenere il pacchetto di dati della risorsa successivo*
- **nx_http_client_put_start** *avviare una richiesta HTTP PUT (solo IPv4)*
- **nx_http_client_put_start_extended** *avviare una richiesta HTTP PUT (solo IPv4)*
- **nxd_http_client_put_start** *avviare una richiesta HTTP PUT (IPv4 o IPv6)*
- **nxd_http_client_put_start_extended** *avviare una richiesta HTTP PUT (IPv4 o IPv6)*
- **nx_http_client_put_packet** *Inviare il pacchetto di dati della risorsa successivo*
- **nx_http_client_set_connect_port** *modificare la porta per connettersi al server HTTP*

**Servizi server HTTP:**

- **nx_http_server_cache_info_callback_set impostare** *il callback per recuperare l'età e la data dell'ultima modifica dell'URL specificato*
- **nx_http_server_callback_data_send** *Inviare dati HTTP dalla funzione di callback*
- **nx_http_server_callback_generate_response_header** *creare un'intestazione di risposta nelle funzioni di callback*
- **nx_http_server_callback_generate_response_header_extended** *creare un'intestazione di risposta nelle funzioni di callback*
- **nx_http_server_callback_packet_send** *Inviare un pacchetto HTTP da un callback HTTP*
- **nx_http_server_callback_response_send** *invia risposta dalla funzione di callback*
- **nx_http_server_callback_response_send_extended** *invia risposta dalla funzione di callback*
- **nx_http_server_content_get** *ottenere contenuto dalla richiesta*
- **nx_http_server_content_get_extended** *ottenere il contenuto dalla richiesta; supporta richieste vuote (lunghezza contenuto pari a zero)*
- **nx_http_server_content_length_get** *ottenere la lunghezza del contenuto nella richiesta*
- **nx_http_server_content_length_get_extended** *ottenere la lunghezza del contenuto nella richiesta; supporta richieste vuote (lunghezza contenuto pari a zero)*
- **nx_http_server_create** *creare un'istanza del server HTTP*
- **nx_http_server_delete** * Eliminare un'istanza del server HTTP*
- **nx_http_server_get_entity_content** *restituire dimensioni e posizione del contenuto dell'entità nell'URL*
- **nx_http_server_get_entity_header l'intestazione** *dell'entità URL nel buffer specificato*
- **nx_http_server_gmt_callback_set impostare** *il callback per recuperare data e ora GMT*
- **nx_http_server_invalid_userpassword_notify_set** *impostare il callback per quando vengono ricevuti nome utente e password non validi in una richiesta client*
- **nx_http_server_mime_maps_additional_set** *definire mappe MIME aggiuntive per HTML*
- **nx_http_server_packet_content_find** *estrai la lunghezza del contenuto nell'intestazione HTTP e imposta il puntatore all'inizio dei dati del contenuto*
- **nx_http_server_packet_get** *ricevere pacchetti client direttamente*
- **nx_http_server_param_get** *il parametro Get dalla richiesta*
- **nx_http_server_query_get** *ottenere una query dalla richiesta*
- **nx_http_server_start** *avviare il server HTTP*
- **nx_http_server_stop** *arrestare il server HTTP*
- **nx_http_server_type_get (deprecato) Estrarre il** tipo HTTP, ad esempio *text/plain dall'intestazione*
- **nx_http_server_type_get_extended** *estrai il tipo HTTP, ad esempio text/plain dall'intestazione*
- **nx_http_server_digest_authenticate_notify_set** *funzione di callback Set digest authenticate*
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
 - **pool_ptr** Puntatore al pool di pacchetti predefinito. Si noti che i pacchetti in questo pool devono avere un payload sufficientemente grande da gestire l'intestazione di risposta completa. Questo valore è definito da NX_HTTP_CLIENT_MIN_PACKET_SIZE in *nx_http.h*.
 - **window_size** Dimensioni della finestra di ricezione del socket TCP del client.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Creazione client HTTP riuscita
 - NX_PTR_ERROR (0x07) HTTP, ip_ptr o puntatore del pool di pacchetti non valido
 - NX_HTTP_POOL_ERROR (0xE9) Dimensioni del payload non valide nel pool di pacchetti

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status =  nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);

/* If status is NX_SUCCESS an HTTP Client instance was successfully created. */
```

## <a name="nx_http_client_delete"></a>nx_http_client_delete

Eliminare un'istanza del client HTTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del client HTTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Eliminazione del client HTTP riuscita
 - NX_PTR_ERROR (0x07) Puntatore HTTP non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the HTTP Client instance “my_client.”  */
status =  nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully deleted. */
```

## <a name="nx_http_client_get_start"></a>nx_http_client_get_start

Avviare una richiesta HTTP GET su IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, CHAR *input_ptr,
            UINT input_size, CHAR *username, CHAR *password,
            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi effettuare più chiamate a nx_http_client_get_packet per *recuperare* pacchetti di dati corrispondenti al contenuto della risorsa richiesto.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio o a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle ``` “/index.htm” ``` ```http://abc.website.com/index.htm``` richieste GET.

Questo servizio funziona solo sulla rete IPv4. Per le applicazioni che devono connettersi alla rete IPv6, *è nxd_http_client_get_start_extended()* .

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la *migrazione nx_http_client_get_start_extended()* *o nxd_http_client_get_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
 - **input_ptr** Puntatore a dati aggiuntivi per la richiesta GET. Questo indirizzo è facoltativo. Se valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene usato un POST anziché un'operazione GET.
 - **input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .
 - **username** Puntatore al nome utente facoltativo per l'autenticazione.
 - **password** Puntatore alla password facoltativa per l'autenticazione.
 - **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:

    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso a tempo indeterminato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Il client HTTP è stato inviato correttamente. Messaggio di avvio GET.
 - **NX_HTTP_ERROR** (0xE0) Errore interno del client HTTP
 - **NX_HTTP_NOT_READY** (0xEA) Client HTTP non pronto
 - **NX_HTTP_FAILED** (0xE2) Errore del client HTTP che comunica con il server HTTP.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Nome e/o password non validi.
 - NX_PTR_ERROR (0x07) Input puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Avviare una richiesta HTTP GET su IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, UINT resource_length,
            CHAR *input_ptr, UINT input_size, CHAR *username,
            UINT username_length, CHAR *password, UINT password_length,
            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "resource" sull'istanza del client HTTP creata in precedenza. Se questa routine restituisce NX_SUCCESS, l'applicazione può eseguire più chiamate a nx_http_client_get_packet per *recuperare* pacchetti di dati corrispondenti al contenuto della risorsa richiesto.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio, oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle ``` “/index.htm” ``` ```http://abc.website.com/index.htm``` richieste GET.

Questo servizio funziona solo sulla rete IPv4. Per le applicazioni che devono connettersi alla rete IPv6, *nxd_http_client_get_start_extended()* deve essere usato.

Questo servizio sostituisce *nx_http_client_get_start()*. Richiede al chiamante di specificare la lunghezza della risorsa, il nome utente e la password.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **resource Puntatore** alla stringa URL per la risorsa richiesta.
 - **resource_length** Lunghezza della stringa URL per la risorsa richiesta.
 - **input_ptr** Puntatore a dati aggiuntivi per la richiesta GET. Questo indirizzo è facoltativo. Se valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene usato un post anziché un'operazione GET.
 - **input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .
 - **username** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso a tempo indeterminato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Il client HTTP è stato inviato correttamente. Messaggio di avvio GET
 - **NX_HTTP_ERROR** (0xE0) Errore interno del client HTTP
 - **NX_HTTP_NOT_READY** (0xEA) Client HTTP non pronto
 - **NX_HTTP_FAILED** (0xE2) Errore del client HTTP che comunica con il server HTTP.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Nome e/o password non validi.
 - NX_PTR_ERROR (0x07) Input puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "resource" sull'istanza del client HTTP creata in precedenza. Può essere usato per connettersi alla rete IPv4 o IPv6. Se questa routine restituisce NX_SUCCESS, l'applicazione può eseguire più chiamate a nx_http_client_get_packet per *recuperare* pacchetti di dati corrispondenti al contenuto della risorsa richiesto.

> [!NOTE]
>La stringa di risorsa può fare riferimento a un file locale, ad esempio, oppure può fare riferimento a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle ``` “/index.htm” ``` ```http://abc.website.com/index.htm``` richieste GET.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione *a nxd_http_client_get_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **Server_ip** Indirizzo IP del server HTTP.
 - **resource** Puntatore alla stringa URL per la risorsa richiesta.
 - **input_ptr** Puntatore a dati aggiuntivi per la richiesta GET. Questo indirizzo è facoltativo. Se valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene usato un post anziché un'operazione GET.
 - **input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .
 - **username** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **wait_option** Definisce per quanto tempo il servizio attenderà la richiesta di avvio get del client HTTP. Le opzioni di attesa sono definite nel modo seguente:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso a tempo indeterminato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) La richiesta GET è stata inviata correttamente
 - **NX_HTTP_PASSWORD_TOO_LONG** (0xF0) La password supera le dimensioni del buffer
 - **NX_HTTP_NOT_READY** (0xEA) Client HTTP non pronto
 - **NX_HTTP_FAILED** (0xE2) Parametri di pacchetto non validi.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Nome o password non validi
 - NX_PTR_ERROR (0x07) Input puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "resource" nell'istanza del client HTTP creata in precedenza. Può essere usato per connettersi alla rete IPv4 o IPv6. Se questa routine restituisce NX_SUCCESS, l'applicazione può quindi effettuare più chiamate a nx_http_client_get_packet per *recuperare* pacchetti di dati corrispondenti al contenuto della risorsa richiesto.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio, oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle ``` “/index.htm” ``` ```http://abc.website.com/index.htm``` richieste GET.

Questo servizio sostituisce *nxd_http_client_get_start()*. Richiede al chiamante di specificare la lunghezza della risorsa, il nome utente e la password.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **Server_ip** Indirizzo IP del server HTTP.
 - **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
 - **resource_length** Lunghezza della stringa URL per la risorsa richiesta.
 - **input_ptr** Puntatore a dati aggiuntivi per la richiesta GET. Questo indirizzo è facoltativo. Se valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene usato un POST anziché un'operazione GET.
 - **input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **wait_option** Definisce il tempo di attesa interno del servizio per elaborare l'avvio del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer che rimangono sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successfully sent GET request (Invio della richiesta GET completato)
 - **NX_HTTP_PASSWORD_TOO_LONG** password (0xF0) supera le dimensioni del buffer
 - **NX_HTTP_NOT_READY** client HTTP (0xEA) non pronto
 - **NX_HTTP_FAILED** (0xE2) Parametri di pacchetto non validi.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Nome o password non valido
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Ottenere il pacchetto di dati della risorsa successivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET **packet_ptr, ULONG
                               wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il pacchetto successivo di contenuto della risorsa richiesta dalla chiamata nx_http_client_get_start *precedente.* Le chiamate successive a questa routine devono essere effettuate fino a quando non viene ricevuto lo NX_HTTP_GET_DONE restituito.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **packet_ptr** Destinazione per il puntatore a pacchetto contenente contenuto parziale della risorsa.
 - **wait_option** Definisce per quanto tempo il servizio attenderà il pacchetto get del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer che rimangono sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Get packet (Ottieni pacchetto client HTTP riuscito).
 - **NX_HTTP_GET_DONE(0xEC)** HTTP Client get packet is done
 - **NX_HTTP_NOT_READY** client HTTP (0xEA) non in modalità get.
 - **NX_HTTP_BAD_PACKET_LENGTH** (0xED) Lunghezza pacchetto non valida
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Avviare una richiesta HTTP PUT su IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               ULONG ip_address, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP specificato. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet()* per inviare effettivamente il contenuto della risorsa al server HTTP.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio, oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle ``` “/index.htm” ``` ```http://abc.website.com/index.htm``` richieste PUT.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la *migrazione nxd_http_client_put_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **password** Puntatore alla password facoltativa per l'autenticazione.
 - **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive *nx_http_client_put_packet* deve essere uguale a questo valore.
 - **wait_option** Definisce per quanto tempo il servizio attenderà l'avvio di HTTP Client PUT. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server HTTP

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successfully sent PUT request (Invio della richiesta PUT completato)
 - **NX_HTTP_USERNAME_TOO_LONG** (0xF1) Nome utente troppo grande per il buffer
 - **NX_HTTP_NOT_READY** client HTTP (0xEA) non pronto
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Avviare una richiesta HTTP PUT su IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
           ULONG ip_address, CHAR *resource, UINT resource_length,
           CHAR *username,UINT username_length, CHAR *password,
           UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP specificato. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet()* per inviare effettivamente il contenuto della risorsa al server HTTP.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio, oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle ``` “/index.htm” ``` ```http://abc.website.com/index.htm``` richieste PUT.

Questo servizio sostituisce *nx_http_client_put_start()*. Richiede al chiamante di specificare la lunghezza della risorsa, il nome utente e la password.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
 - **resource_length** Lunghezza della stringa URL per la risorsa da inviare al server.
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive nx_http_client_put_packet *deve* essere uguale a questo valore.
 - **wait_option** Definisce per quanto tempo il servizio attenderà l'avvio di HTTP Client PUT. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successfully sent PUT request (Invio della richiesta PUT completato)
 - **NX_HTTP_USERNAME_TOO_LONG** (0xF1) Nome utente troppo grande per il buffer
 - **NX_HTTP_NOT_READY** client HTTP (0xEA) non pronto
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio tenta di inserire (inviare) la risorsa specificata nel server HTTP all'indirizzo IP fornito tramite IPv6. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet()* per inviare effettivamente il contenuto della risorsa al server HTTP.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio, oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle ``` “/index.htm” ``` ```http://abc.website.com/index.htm``` richieste PUT.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la *migrazione nxd_http_client_put_start_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **server_ip** Indirizzo IP del server HTTP.
 - **risorsa** Puntatore alla stringa URL per la risorsa da inviare al server.
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **password** Puntatore alla password facoltativa per l'autenticazione.
 - **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive nx_http_client_put_packet *deve* essere uguale a questo valore.
 - **wait_option** Definisce per quanto tempo il servizio attenderà l'avvio di HTTP Client PUT. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successfully sent HTTP Client PUT request (Invio della richiesta PUT del client HTTP completato)
 - **NX_HTTP_ERROR** interno del client HTTP 0xE0 (0xE0)
 - **NX_HTTP_NOT_READY** client HTTP (0xEA) non pronto
 - **NX_HTTP_FAILED** client HTTP (0xE2) durante la comunicazione con il server HTTP
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio tenta di inserire (inviare) la risorsa specificata nel server HTTP all'indirizzo IP fornito tramite IPv6. Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet()* per inviare effettivamente il contenuto della risorsa al server HTTP.

> [!NOTE]
> La stringa di risorsa può fare riferimento a un file locale, ad esempio, oppure a un altro URL, ad esempio se il server HTTP indica che supporta il riferimento alle ``` “/index.htm” ``` ```http://abc.website.com/index.htm``` richieste PUT.

Questo servizio sostituisce *nxd_http_client_put_start()*. Richiede al chiamante di specificare la lunghezza della risorsa, il nome utente e la password.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **ip_address** Indirizzo IP del server HTTP.
 - **risorsa** Puntatore alla stringa URL per la risorsa richiesta.
 - **resource_length** Lunghezza della stringa URL per la risorsa da inviare al server.
 - **nome utente** Puntatore al nome utente facoltativo per l'autenticazione.
 - **username_length** Lunghezza del nome utente facoltativo per l'autenticazione.
 - **password** Puntatore alla password facoltativa per l'autenticazione.
 - **password_length** Lunghezza della password facoltativa per l'autenticazione.
 - **total_bytes** Byte totali della risorsa inviata. Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive nx_http_client_put_packet *deve* essere uguale a questo valore.
 - **wait_option** Definisce per quanto tempo il servizio attenderà l'avvio di HTTP Client PUT. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successfully sent HTTP Client PUT request (Invio della richiesta PUT del client HTTP completato)
 - **NX_HTTP_ERROR** interno del client HTTP 0xE0 (0xE0)
 - **NX_HTTP_NOT_READY** client HTTP (0xEA) non pronto
 - NX_HTTP_FAILED client HTTP (0xE2) durante la comunicazione con il server HTTP
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_SIZE_ERROR (0x09) Dimensioni totali della risorsa non valide
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Inviare il pacchetto di dati della risorsa successivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET *packet_ptr,
                               ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di inviare il pacchetto successivo di contenuto della risorsa al server HTTP.

> [!NOTE]
> Questa routine deve essere chiamata in modo ripetitivo finché la lunghezza combinata dei pacchetti inviati non è uguale al valore "total_bytes" specificato nella chiamata *nx_http_client_put_start* precedente.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **packet_ptr** Puntatore al contenuto successivo della risorsa da inviare al server HTTP.
 - **wait_option** Definisce il tempo di attesa interno del servizio per elaborare il pacchetto PUT del client HTTP. Le opzioni di attesa sono definite come segue:
    - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)
    - **TX_WAIT_FOREVER** (0xFFFFFFFF)

    Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando il server HTTP non risponde alla richiesta.

    La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risposta del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Il pacchetto client HTTP è stato inviato correttamente.
 - **NX_HTTP_NOT_READY** client HTTP (0xEA) non pronto
 - **NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) Received Server error code
 - **NX_HTTP_BAD_PACKET_LENGTH** (0xED) Lunghezza pacchetto non valida
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Nome e/o password non validi
 - **NX_HTTP_INCOMPLETE_PUT_ERROR** server (0xEF) risponde prima del completamento di PUT
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_INVALID_PACKET (0x12) Pacchetto troppo piccolo per l'intestazione TCP
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio modifica la porta di connessione durante la connessione al server HTTP alla porta specificata in fase di esecuzione. In caso contrario, il valore predefinito della porta di connessione è 80. Questo metodo deve essere *chiamato prima nx_http_client_get_start()* *e nx_http_client_put_start(),* ad esempio quando il client HTTP si connette al server.

### <a name="input-parameters"></a>Parametri di input

 - **client_ptr** Puntatore al blocco di controllo client HTTP.
 - **porta** Porta per la connessione al server.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Modifica della porta completata
 - NX_INVALID_PORT (0x46) La porta supera il valore massimo (0xFFFF) o è zero
 - NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

thread, inizializzazione

### <a name="example"></a>Esempio

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status =  nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a>nx_http_server_cache_info_callback_set

Impostare il callback per recuperare la validità e la data ma massima dell'URL

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                         UINT (*cache_info_get)(CHAR *resource,
                                                 UINT *max_age,
                                                 NX_HTTP_SERVER_DATE
                                                      *date));
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
 - NX_PTR_ERROR (0x07) Input del puntatore non valido

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

Inviare dati dalla funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                       VOID *data_ptr,
                                       ULONG data_length);
```

### <a name="description"></a>Descrizione

Questo servizio invia i dati nel pacchetto fornito dalla routine di callback dell'applicazione. Viene in genere usato per inviare dati dinamici associati a richieste GET/POST.

> [!NOTE]
> Se si usa questa funzione, la routine di callback è responsabile dell'invio dell'intera risposta nel formato corretto. Inoltre, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **data_ptr** Puntatore ai dati da inviare.
 - **data_length**  Numero di byte da inviare.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) I dati del server sono stati inviati correttamente
 - NX_PTR_ERROR (0x07) Input del puntatore non valido

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

Creare un'intestazione di risposta in una funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_generate_response_header(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT content_length,
                        CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a>Descrizione

Questo servizio chiama la funzione interna *_nx_http_server_generate_response_header* quando il server HTTP risponde alle richieste get, put ed delete del client. È destinato all'uso nelle funzioni di callback del server HTTP quando l'applicazione server HTTP sta progettando la risposta al client.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la *migrazione nxd_http_server_callback_generate_response_header_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **packet_pptr** Puntatore a un puntatore a pacchetto allocato per il messaggio
 - **status_code** Indica lo stato della risorsa. Esempi:
    - **NX_HTTP_STATUS_OK**
    - **NX_HTTP_STATUS_MODIFIED**
    - **NX_HTTP_STATUS_INTERNAL_ERROR**
 - **content_length** Dimensioni del contenuto in byte
 - **content_type** Tipo di HTTP, ad esempio "text/plain"
 - **additional_header** Puntatore al testo aggiuntivo dell'intestazione

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) L'intestazione è stata creata correttamente
 - NX_PTR_ERROR (0x07) Input puntatore non valido

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

Creare un'intestazione di risposta in una funzione di callback

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

Questo servizio chiama la funzione interna *_nx_http_server_generate_response_header()* quando il server HTTP risponde alle richieste get, put ed delete client. È destinato all'uso nelle funzioni di callback del server HTTP quando l'applicazione server HTTP sta progettando la risposta al client.

Questo servizio sostituisce *nx_http_server_callback_generate_response_header()*. Questa versione fornisce informazioni aggiuntive sulla lunghezza alla funzione di callback.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **packet_pptr** Puntatore a un puntatore a pacchetto allocato per il messaggio
 - **status_code** Indicare lo stato della risorsa. Esempi:
    - **NX_HTTP_STATUS_OK**
    - **NX_HTTP_STATUS_MODIFIED**
    - **NX_HTTP_STATUS_INTERNAL_ERROR**
 - **status_code** Lunghezza del codice di stato
 - **content_length** Dimensioni del contenuto in byte
 - **content_type** Tipo di HTTP, ad esempio "text/plain"
 - **content_type_length** Lunghezza del tipo HTTP
 - **additional_header** Puntatore al testo aggiuntivo dell'intestazione
 - **additional_header_length** Lunghezza del testo aggiuntivo dell'intestazione

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) L'intestazione è stata creata correttamente
 - NX_PTR_ERROR (0x07) Input puntatore non valido

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

Questo servizio invia una risposta completa del server HTTP da un callback HTTP. Il server HTTP invierà il pacchetto con il NX_HTTP_SERVER _TIMEOUT_SEND. L'intestazione HTTP e i dati devono essere aggiunti al pacchetto. Se lo stato restituito indica un errore, l'applicazione HTTP deve rilasciare il pacchetto.

Il callback deve restituire NX_HTTP_CALLBACK_COMPLETED.

Vedere *nx_http_server_callback_generate_response_header()* per un esempio più dettagliato.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **packet_ptr** Puntatore al pacchetto da inviare

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Pacchetto server inviato correttamente
 - NX_PTR_ERROR (0x07) Input puntatore non valido

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

Inviare una risposta dalla funzione di callback

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
                                           CHAR *header,
                                           CHAR *information,
                                           CHAR additional_info);
```

### <a name="description"></a>Descrizione

Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione. Viene in genere usato per inviare risposte personalizzate associate alle richieste GET/POST.

> [!NOTE]
> Se si usa questa funzione, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione *a nxd_http_server_callback_response_send_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **intestazione** Puntatore alla stringa di intestazione della risposta.
 - **informazioni** Puntatore alla stringa di informazioni.
 - **additional_info** Puntatore alla stringa di informazioni aggiuntive.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Risposta del server inviata correttamente

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

Inviare una risposta dalla funzione di callback

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

Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione. Viene in genere usato per inviare risposte personalizzate associate alle richieste GET/POST.

> [!NOTE]
> Se si usa questa funzione, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.

Questo servizio sostituisce *nx_http_server_callback_response_send()*. Questa versione accetta informazioni aggiuntive sulla lunghezza come argomenti.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **intestazione** Puntatore alla stringa di intestazione della risposta.
 - **header_length** Lunghezza della stringa di intestazione della risposta.
 - **informazioni** Puntatore alla stringa di informazioni.
 - **information_length** Lunghezza della stringa di informazioni.
 - **additional_info** Puntatore alla stringa di informazioni aggiuntive.
 - **additional_info_length** Lunghezza della stringa di informazioni aggiuntive.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Risposta del server inviata correttamente

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

Questo servizio tenta di recuperare la quantità specificata di contenuto dalla richiesta del client HTTP POST o PUT. Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la *migrazione nx_http_server_content_get_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback di notifica della richiesta.
 - **byte_offset** Numero di byte di cui eseguire l'offset nell'area del contenuto.
 - **destination_ptr** Puntatore all'area di destinazione per il contenuto.
 - **destination_size** Numero massimo di byte disponibili nell'area di destinazione.
 - **actual_size** Puntatore alla variabile di destinazione che verrà impostata sulla dimensione effettiva del contenuto copiato.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successful HTTP Server content get (Ottiene il contenuto del server HTTP riuscito)
 - **NX_HTTP_ERROR** interno del server HTTP 0xE0 (0xE0)
 - **NX_HTTP_DATA_END** (0xE7) Fine della richiesta
 - **NX_HTTP_TIMEOUT** timeout (0xE1) del server HTTP nel recupero del pacchetto di contenuto successivo
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Ottiene il contenuto dalla richiesta/supporta la lunghezza del contenuto di lunghezza zero

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

Questo servizio è quasi identico *nx_http_server_content_get();* tenta di recuperare la quantità specificata di contenuto dalla richiesta post o put http client. Gestisce tuttavia le richieste con lunghezza del contenuto pari a zero ('empty request') come richiesta valida. Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create()).*

Questo servizio sostituisce *nx_http_server_content_get()*. Questa versione richiede al chiamante di fornire informazioni aggiuntive sulla lunghezza.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback di notifica della richiesta.
 - **byte_offset** Numero di byte di cui eseguire l'offset nell'area del contenuto.
 - **destination_ptr** Puntatore all'area di destinazione per il contenuto.
 - **destination_size** Numero massimo di byte disponibili nell'area di destinazione.
 - **actual_size** Puntatore alla variabile di destinazione che verrà impostata sulla dimensione effettiva del contenuto copiato.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successful HTTP content get
 - **NX_HTTP_ERROR** interno del server HTTP 0xE0 (0xE0)
 - **NX_HTTP_DATA_END** (0xE7) Fine della richiesta
 - **NX_HTTP_TIMEOUT** (0xE1) del server HTTP per ottenere il pacchetto successivo
 - NX_PTR_ERROR (0x07) Input puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito. Se non è presente contenuto HTTP, questa routine restituisce un valore pari a zero. Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create()).*

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la *migrazione nx_http_server_content_length_get_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback di notifica della richiesta.

### <a name="return-values"></a>Valori restituiti

 - **lunghezza del contenuto** In caso di errore, viene restituito un valore pari a zero  

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

Ottiene la lunghezza del contenuto nella richiesta/supporta la lunghezza del contenuto pari a zero

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                                UINT *content_length);
```

### <a name="description"></a>Descrizione

Questo servizio è simile a *nx_http_server_content_length_get;* tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito. Tuttavia, il valore restituito indica lo stato di completamento corretto e il valore della lunghezza effettiva viene restituito nel puntatore di input ```content_length``` . Se non è presente alcun contenuto HTTP/Lunghezza contenuto = 0, questa routine restituisce comunque uno stato di completamento corretto e il puntatore di input content_length punta a una lunghezza valida (zero). Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).

Questo servizio sostituisce *nx_http_server_content_length_get()*.

### <a name="input-parameters"></a>Parametri di input

 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che questo pacchetto non deve essere rilasciato dal callback di notifica della richiesta.
 - **content_length** Puntatore al valore recuperato dal campo Lunghezza contenuto

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successful Server content get
 - **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Formato di intestazione HTTP non corretto
 - NX_PTR_ERROR (0x07) Input del puntatore non valido

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

Questo servizio crea un'istanza del server HTTP, che viene eseguita nel contesto del proprio thread ThreadX. Le routine *authentication_check* e request_notify callback dell'applicazione forniscono all'applicazione il controllo software sulle operazioni di base del server HTTP.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore al blocco di controllo del server HTTP.
 - **http_server_name** Puntatore al nome del server HTTP.
 - **ip_ptr** Puntatore all'istanza IP creata in precedenza.
 - **media_ptr** Puntatore all'istanza del supporto FileX creata in precedenza.
 - **stack_ptr** Puntatore all'area dello stack di thread del server HTTP.
 - **stack_size** Puntatore alle dimensioni dello stack dei thread del server HTTP.
 - **authentication_check** Puntatore a funzione alla routine di controllo dell'autenticazione dell'applicazione. Se specificato, questa routine viene chiamata per ogni richiesta del client HTTP. Se questo parametro è NULL, non verrà eseguita alcuna autenticazione.
 - **request_notify** Puntatore a funzione alla routine di notifica della richiesta dell'applicazione. Se specificato, questa routine viene chiamata prima dell'elaborazione del server HTTP della richiesta. In questo modo è possibile reindirizzare il nome della risorsa o aggiornare i campi all'interno di una risorsa prima di completare la richiesta del client HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Creazione del server HTTP completata.
 - NX_PTR_ERROR (0x07) Puntatore del server HTTP, IP, supporto, stack o pool di pacchetti non valido.
 - NX_HTTP_POOL_ERROR (0xE9) Il payload del pacchetto del pool non è sufficientemente grande da contenere una richiesta HTTP completa.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

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

```c
/* Delete the HTTP Server instance called “my_server.”  */
status =  nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a>nx_http_server_get_entity_content

Recuperare la posizione e la lunghezza dei dati dell'entità

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_pptr,
                                       ULONG *available_offset,
                                       ULONG *available_length);
```

### <a name="description"></a>Descrizione

Questo servizio determina la posizione dell'inizio dei dati all'interno dell'entità multipart corrente nei messaggi client ricevuti e la lunghezza dei dati che non includono la stringa limite. Il server HTTP internamente aggiorna i propri offset in modo che questa funzione possa essere chiamata nuovamente nello stesso datagramma client per i messaggi con più entità. Il puntatore a pacchetto viene aggiornato al pacchetto successivo in cui il messaggio client è un datagramma a più pacchetti.

> [!NOTE]
> NX_HTTP_MULTIPART_ENABLE deve essere abilitato per usare questo servizio.

Vedere [*nx_http_server_get_entity_header*](#nx_http_server_get_entity_header) per altri dettagli.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al server HTTP
 - **packet_pptr** Puntatore alla posizione del puntatore a pacchetto. Si noti che l'applicazione non deve rilasciare questo pacchetto.
 - **available_offset** Puntatore all'offset dei dati di entità dal puntatore anteposto al pacchetto
 - **available_length** Puntatore alla lunghezza dei dati di entità

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Le dimensioni e la posizione del contenuto dell'entità sono state recuperate correttamente
 - **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) Il contenuto per i marcatori multipart interni del server HTTP è già stato trovato
 - NX_HTTP_ERROR (0xE0) Errore HTTP interno
 - NX_PTR_ERROR (0x07) Input puntatore non valido

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

Recuperare il contenuto dell'intestazione di entità

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      UCHAR *entity_header_buffer,
                                      ULONG buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'intestazione dell'entità nel buffer specificato. Il server HTTP internamente aggiorna i propri puntatori per individuare l'entità multipart successiva in un datagramma client con più intestazioni di entità. Il puntatore a pacchetto viene aggiornato al pacchetto successivo in cui il messaggio client è un datagramma a più pacchetti.

> [!NOTE]
> NX_HTTP_MULTIPART_ENABLE deve essere abilitato per usare questo servizio.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al server HTTP
 - **packet_pptr** Puntatore alla posizione del puntatore a pacchetto. Si noti che l'applicazione non deve rilasciare questo pacchetto.
 - **entity_header_buffer** Puntatore alla posizione in cui archiviare l'intestazione dell'entità
 - **buffer_size** Dimensioni del buffer di input

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Heade entità recuperato correttamente
 - **NX_HTTP_NOT_FOUND** **(0xE6) Campo intestazione** entità non trovato
 - **NX_HTTP_TIMEOUT** **(0xE1)** Tempo scaduto per ricevere il pacchetto successivo per il messaggio client multipacket
 - NX_HTTP_ERROR (0xE0) Errore HTTP interno
 - NX_PTR_ERROR (0x07) Input puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Impostare il callback per ottenere data e ora GMT

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback per ottenere data e ora GMT con un server HTTP creato in precedenza. Questo servizio viene richiamato con il server HTTP che crea un'intestazione nelle risposte del server HTTP al client.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al server HTTP
 - **gmt_getv** Puntatore al callback GMT
 - **datev** Puntatore alla data recuperata

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Impostare correttamente il callback
 - NX_PTR_ERROR (0x07) Puntatore a pacchetto o parametro non valido.

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

Impostare il callback su per gestire utente/password non validi

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

Questo servizio imposta il callback richiamato quando un nome utente e una password non validi vengono ricevuti in una richiesta client get, put o delete, tramite digest o autenticazione di base. Il server HTTP deve essere creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore al server HTTP
 - **invalid_username_password_callback** Puntatore a un callback utente/passaggio non valido
 - **risorsa** Puntatore alla risorsa specificata dal client
 - **client_address** Puntatore all'indirizzo client. Può essere IPv4 o IPv6
 - **request_type** Indica il tipo di richiesta client. Può essere:
    - NX_HTTP_SERVER_GET_REQUEST
    - NX_HTTP_SERVER_POST_REQUEST
    - NX_HTTP_SERVER_HEAD_REQUEST
    - NX_HTTP_SERVER_PUT_REQUEST
    - NX_HTTP_SERVER_DELETE_REQUEST

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Impostare correttamente il callback
 - NX_PTR_ERROR (0x07) Input del puntatore non valido

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

Questo servizio consente allo sviluppatore di applicazioni HTTP di aggiungere altri tipi MIME dai tipi MIME predefiniti forniti da NetX Duo HTTP Server (vedere *nx_http_server_get_type* per l'elenco dei tipi definiti).

Quando viene ricevuta una richiesta client, ad esempio una richiesta GET, il server HTTP analizza il tipo di file richiesto dall'intestazione HTTP usando preferibilmente il set di mapping MIME aggiuntivo e, se non viene trovata alcuna corrispondenza, cerca una corrispondenza nella mappa MIME predefinita del server HTTP. Se non viene trovata alcuna corrispondenza, per impostazione predefinita il tipo MIME è "text/plain".

Se la funzione request notify è registrata con il server HTTP, il callback di notifica della richiesta può chiamare *nx_http_server_type_retrieve()* per analizzare il tipo di file.

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

Questo servizio estrae la lunghezza del contenuto dall'intestazione HTTP. Aggiorna anche il pacchetto fornito come segue: il puntatore anteposto al pacchetto (inizio della posizione del buffer di pacchetti in cui scrivere) viene impostato sul contenuto HTTP (dati) appena passato all'intestazione HTTP.

Se l'inizio del contenuto non viene trovato nel pacchetto corrente, la funzione attende che il pacchetto successivo sia ricevuto usando l'opzione NX_HTTP_SERVER_TIMEOUT_RECEIVE wait.

> [!NOTE]
> Questo metodo non deve essere chiamato prima *di nx_http_server_get_entity_header* perché modifica il puntatore anteposto dopo l'intestazione dell'entità.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore all'istanza del server HTTP
 - **packet_ptr** Puntatore al puntatore al pacchetto per la restituzione del pacchetto con puntatore anteposto aggiornato
 - **content_length** Puntatore a estratto ```content_length```

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** contenuto HTTP (0x00) trovato e il pacchetto è stato aggiornato correttamente
 - **NX_HTTP_TIMEOUT** (0xE1) Tempo scaduto in attesa del pacchetto successivo
 - NX_PTR_ERROR (0x07) Input del puntatore non valido

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

Questo servizio restituisce il pacchetto successivo ricevuto sul socket del server HTTP. L'opzione wait per ricevere un pacchetto è NX_HTTP_SERVER_TIMEOUT_RECEIVE.

### <a name="input-parameters"></a>Parametri di input

 - **server_ptr** Puntatore all'istanza del server HTTP
 - **packet_ptr** Puntatore al pacchetto ricevuto

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Pacchetto successivo ricevuto
 - **NX_HTTP_TIMEOUT** (0xE1) Tempo scaduto in attesa del pacchetto successivo
 - NX_PTR_ERROR (0x07) Input puntatore non valido

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
 - **param_number** Numero logico del parametro che inizia da zero, da sinistra a destra nell'elenco di parametri.
 - **param_ptr** Area di destinazione in cui copiare il parametro.
 - **max_param_size** Dimensioni massime dell'area di destinazione del parametro.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Successful HTTP Server parameter get
 - **NX_HTTP_NOT_FOUND** (0xE6) Parametro specificato non trovato
 - **NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) Request parameter not properly terminated (Il parametro di richiesta (0xF3) non è stato terminato correttamente
 - NX_PTR_ERROR (0x07) Input del puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio tenta di recuperare la query dell'URL HTTP specificata nel pacchetto di richiesta fornito. Se la query HTTP richiesta non è presente, questa routine restituisce lo stato NX_HTTP_NOT_FOUND. Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).

### <a name="input-parameters"></a>Parametri di input

 - **packet_ptr** Puntatore al pacchetto di richiesta del client HTTP. Si noti che l'applicazione non deve rilasciare questo pacchetto.
 - **query_number** Numero logico del parametro che inizia da zero, da sinistra a destra nell'elenco di query.
 - **query_ptr** Area di destinazione in cui copiare la query.
 - **max_query_size** Dimensioni massime dell'area di destinazione della query.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Query del server HTTP riuscita
 - **NX_HTTP_FAILED** (0xE2) Dimensioni query troppo piccole.
 - **NX_HTTP_NOT_FOUND** (0xE6) Query specificata non trovata
 - **NX_HTTP_NO_QUERY_PARSED** (0xF2) Nessuna query nella richiesta client
 - NX_PTR_ERROR (0x07) Input puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio avvia l'istanza del server HTTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Avvio del server riuscito
 - NX_PTR_ERROR (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

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

Questo servizio arresta l'istanza del server HTTP creata in precedenza. Questa routine deve essere chiamata prima di eliminare un'istanza del server HTTP.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP.

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Arresto del server riuscito
 - NX_PTR_ERROR (0x07) Input puntatore non valido
 - NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the HTTP Server instance “my_server.”  */
status =  nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a>nx_http_server_type_get

Estrarre il tipo di file dalla richiesta HTTP client

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                             CHAR *name, CHAR *http_type_string);
```

### <a name="description"></a>Descrizione

> [!NOTE]
> questo servizio è deprecato. Gli utenti sono invitati a usare il servizio *nx_http_server_type_retrieve()*.

Questo servizio estrae il tipo di richiesta HTTP nel buffer http_type_string e la relativa lunghezza nel valore restituito dal nome del buffer di input, in genere l'URL. Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene utilizzato il tipo "text/plain". In caso contrario, confronta il tipo estratto con i mapping MIME predefiniti del server HTTP per trovare una corrispondenza. Le mappe MIME predefinite nel server HTTP NetX Duo sono:

 - **html** text/html
 - **htm** text/html
 - **txt** text/plain
 - **gif** image/gif
 - **jpg** image/jpeg
 - **ico** image/x-icon

Se specificato, esegue anche la ricerca in un set definito dall'utente di mappe MIME aggiuntive. Vedere *nx_http_server_mime_maps_addtional_set() per* altri dettagli sulle mappe definite dall'utente.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione *a nx_http_server_type_get_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP
 - **name Puntatore** al buffer da cercare
 - **http_type_string** (puntatore al tipo HTML estratto)

### <a name="return-values"></a>Valori restituiti

 - **Lunghezza della stringa in byte** Il valore diverso da zero è esito positivo. Zero indica un errore.

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

Estrarre il tipo di file dalla richiesta HTTP client

### <a name="prototype"></a>Prototipo

```c
UINT nx_http_server_type_get_extended(
                                    NX_HTTP_SERVER *http_server_ptr,
                                    CHAR *name, CHAR *http_type_string,
                                    UINT http_type_string_max_size);
```

### <a name="description"></a>Descrizione

Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la relativa lunghezza nel valore restituito dal nome *del* buffer di input, in genere l'URL. Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene utilizzato il tipo "text/plain". In caso contrario, confronta il tipo estratto con i mapping MIME predefiniti del server HTTP per trovare una corrispondenza. Le mappe MIME predefinite nel server HTTP NetX Duo sono:

 - **html** text/html
 - **htm** text/html
 - **txt** text/plain
 - **gif** image/gif
 - **jpg** image/jpeg
 - **ico** image/x-icon

Se specificato, esegue anche la ricerca in un set definito dall'utente di mappe MIME aggiuntive. Vedere *nx_http_server_mime_maps_addtional_set() per* altri dettagli sulle mappe definite dall'utente.

Questo servizio sostituisce *nx_http_server_type_get()*. Questa versione fornisce informazioni aggiuntive sulla lunghezza.

### <a name="input-parameters"></a>Parametri di input

 - **http_server_ptr** Puntatore all'istanza del server HTTP
 - **name** Puntatore al buffer da cercare
 - **name_length** Lunghezza del buffer da cercare
 - **http_type_string** (puntatore al tipo HTML estratto)
 - **http_type_string_max_size** Dimensioni del buffer http_type_string dati

### <a name="return-values"></a>Valori restituiti

 - **Lunghezza della stringa in byte** Il valore diverso da zero è esito positivo. Zero indica un errore.

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

Impostare la funzione di callback di autenticazione digest

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
 - **digest_authenticate_callback** Puntatore al callback di autenticazione digest

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Impostare correttamente il callback
 - NX_PTR_ERROR (0x07) Input puntatore non valido
 - NX_NOT_SUPPORTED (0x4B) L'autenticazione del digest non è abilitata

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

Impostare la funzione di callback di controllo dell'autenticazione

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
 - **authentication_check_extended** Puntatore al controllo dell'autenticazione dell'applicazione

### <a name="return-values"></a>Valori restituiti

 - **NX_SUCCESS** (0x00) Impostare correttamente il callback
 - NX_PTR_ERROR (0x07) Input puntatore non valido

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
