---
title: Capitolo 1-Introduzione a NetX HTTP
description: In questo documento viene illustrato come il protocollo HTTP è un protocollo progettato per il trasferimento di contenuto sul Web.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6137cc0d8deb753d784be844d5abc7778dd62295
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822622"
---
# <a name="chapter-1---introduction-to-netx-http"></a>Capitolo 1-Introduzione a NetX HTTP

Il Hypertext Transfer Protocol (HTTP) è un protocollo progettato per il trasferimento del contenuto sul Web. HTTP è un protocollo semplice che utilizza i servizi di Transmission Control Protocol affidabili (TCP) per eseguire la relativa funzione di trasferimento del contenuto. Per questo motivo, HTTP è un protocollo di trasferimento del contenuto altamente affidabile. HTTP è uno dei protocolli applicativi più usati. Tutte le operazioni sul Web utilizzano il protocollo HTTP.

## <a name="http-requirements"></a>Requisiti HTTP

Per funzionare correttamente, il pacchetto HTTP NetX richiede l'installazione di un NetX (versione 5,2 o successiva). Inoltre, è necessario che sia già stata creata un'istanza IP e che sia stato abilitato il protocollo TCP nella stessa istanza di IP. Il file demo nella sezione "Small example System" del **capitolo 2** illustra come questa operazione viene eseguita.

La parte client HTTP del pacchetto HTTP NetX non ha altri requisiti.

La parte relativa al server HTTP del pacchetto HTTP NetX presenta diversi requisiti aggiuntivi. Per prima cosa, è necessario l'accesso completo alla *porta TCP 80 nota* per la gestione di tutte le richieste HTTP del client. Il server HTTP è anche progettato per l'uso con FileX Embedded file system. Se FileX non è disponibile, l'utente può trasferire le parti di FileX utilizzate nel proprio ambiente. Questo argomento viene descritto nelle sezioni successive di questa guida.

## <a name="http-constraints"></a>Vincoli HTTP 

Il protocollo HTTP NetX implementa lo standard HTTP 1,0. Tuttavia, sono presenti i vincoli seguenti:

1.  Le connessioni permanenti non sono supportate

2.  Il pipelining della richiesta non è supportato

3.  Il server HTTP supporta l'autenticazione di base e del digest MD5, ma non MD5-sess. Attualmente, il client HTTP supporta solo l'autenticazione di base.

4.  Non è supportata alcuna compressione del contenuto.

5.  Le richieste di traccia, opzioni e connessione non sono supportate.

6.  Il pool di pacchetti associato al server o al client HTTP deve essere sufficientemente grande da contenere l'intestazione HTTP completa.

7.  I servizi client HTTP sono destinati solo al trasferimento del contenuto. in questo pacchetto non sono disponibili utilità di visualizzazione.

## <a name="http-url-resource-names"></a>URL HTTP (nomi di risorse)

Il protocollo HTTP è progettato per trasferire il contenuto sul Web. Il contenuto richiesto viene specificato dall'URL (Universal Resource Locator). Questo è il componente principale di ogni richiesta HTTP. Gli URL iniziano sempre con il carattere "/" e in genere corrispondono ai file nel server HTTP. Di seguito sono elencate le estensioni di file HTTP comuni:

- **. htm (o. html)** Hypertext Markup Language (HTML)
- **txt** Testo ASCII normale
- **. gif** Immagine GIF binaria
- **. xbm** Immagine xbitmap binaria

## <a name="http-client-requests"></a>Richieste client HTTP

Il protocollo HTTP ha un meccanismo semplice per la richiesta di contenuto Web. È fondamentalmente disponibile un set di comandi HTTP standard emessi dal client dopo che una connessione è stata stabilita correttamente sulla *porta TCP 80*. Di seguito sono riportati alcuni dei comandi HTTP di base:

- OTTENERE la risorsa HTTP/1.0 *ottenere la risorsa specificata*
- POST Resource HTTP/1.0 *ottenere la risorsa specificata e passare l'input collegato al server http*
- Risorsa HEAD HTTP/1.0 *trattata come Get ma non il contenuto viene restituito dal server http*
- Inserisci risorsa HTTP/1.0 *posizione sul server http*
- Elimina risorsa HTTP/1.0 *Delete risorsa nel server*

Questi comandi ASCII vengono generati internamente dai Web browser e dai servizi client HTTP NetX per eseguire operazioni HTTP con un server HTTP.

>[!NOTE] 
> Per impostazione predefinita, l'applicazione client HTTP viene impostata sulla porta di connessione 80. Tuttavia, può modificare la porta di connessione al server HTTP in fase di esecuzione usando il servizio *nx_http_client_set_connect_port* . Per ulteriori informazioni su questo servizio, vedere il capitolo 4. In questo modo è possibile gestire i server Web che occasionalmente utilizzano porte alternative per le connessioni client.

## <a name="http-server-responses"></a>Risposte al server HTTP

Il server HTTP utilizza la stessa *porta TCP 80 nota* per inviare le risposte del comando client. Una volta che il server HTTP elabora il comando client, restituisce una stringa di risposta ASCII che include un codice di stato numerico a 3 cifre. La risposta numerica viene utilizzata dal software client HTTP per determinare se l'operazione ha avuto esito positivo o negativo. Di seguito è riportato un elenco di varie risposte del server HTTP ai comandi client:

- la *richiesta 200 è stata completata*
- la *richiesta 400 non è stata creata correttamente*
- 401 *richiesta non autorizzata, il client deve inviare l'autenticazione*
- 404 la *risorsa specificata nella richiesta non è stata trovata*
- 500 *errore interno del server http*
- *richiesta 501 non implementata dal server http*
- 502 il *servizio non è disponibile*

Ad esempio, una richiesta client corretta per inserire il file "test.htm" viene risposto con il messaggio "HTTP/1.0 200 OK".

## <a name="http-communication"></a>Comunicazione HTTP

Come indicato in precedenza, il server HTTP utilizza la *porta TCP nota 80* per il campo richieste client. I client HTTP possono usare qualsiasi porta TCP disponibile. La sequenza generale degli eventi HTTP è la seguente:

**Richiesta HTTP Get**:

1.  Il client invia la connessione TCP alla porta del server 80.

2.  Il client invia la richiesta "**Get Resource http/1.0**" (insieme ad altre informazioni di intestazione).

3.  Il server compila un messaggio "**http/1.0 200 OK**" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa (se presente).

4.  Il server esegue una disconnessione.

5.  Il client esegue una disconnessione.

**Richiesta HTTP PUT**:

1. Il client invia la connessione TCP alla porta del server 80.

2. Il client invia la richiesta "**put Resource http/1.0**", insieme ad altre informazioni di intestazione e seguita dal contenuto della risorsa.

3. Il server compila un messaggio "**http/1.0 200 OK**" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa.

4. Il server esegue una disconnessione.

5. Il client esegue una disconnessione.

>[!NOTE] 
> Come indicato in precedenza, il client HTTP può modificare la porta di connessione predefinita da 80 a un'altra porta usando il *nx_http_client_set_connect_port* per i server Web che usano porte alternative per connettersi ai client.

## <a name="http-authentication"></a>Autenticazione HTTP

L'autenticazione HTTP è facoltativa e non è obbligatoria per tutte le richieste Web. Esistono due tipi di autenticazione, ovvero *Basic* e *digest*. L'autenticazione di base equivale all'autenticazione del *nome* e della *password* presente in molti protocolli. Nell'autenticazione di base HTTP, il nome e le password vengono concatenati e codificati nel formato Base64. Lo svantaggio principale dell'autenticazione di base è il nome e la password vengono trasmessi apertamente nella richiesta. In questo modo è piuttosto semplice che il nome e la password vengano rubati. L'autenticazione del digest risolve questo problema senza trasmettere mai il nome e la password nella richiesta. Viene invece utilizzato un algoritmo per derivare una chiave o un digest a 128 bit dal nome, dalla password e da altre informazioni. Il server HTTP NetX supporta l'algoritmo digest MD5 standard.

Quando è richiesta l'autenticazione? In sostanza, il server HTTP decide se una risorsa richiesta richiede l'autenticazione. Se è richiesta l'autenticazione e la richiesta del client non include l'autenticazione corretta, al client viene inviata una risposta "HTTP/1.0 401 non autorizzato" con il tipo di autenticazione richiesto. Il client deve quindi creare una nuova richiesta con l'autenticazione corretta.

## <a name="http-authentication-callback"></a>Callback di autenticazione HTTP

Come indicato in precedenza, l'autenticazione HTTP è facoltativa e non è necessaria per tutti i trasferimenti Web. Inoltre, l'autenticazione è in genere dipendente dalle risorse. L'accesso ad alcune risorse sul server richiede l'autenticazione, mentre altri no. Il pacchetto del server HTTP NetX consente all'applicazione di specificare (tramite la chiamata ***nx_http_server_create*** ) una routine di callback di autenticazione che viene chiamata all'inizio della gestione di ogni richiesta del client http.

La routine di callback fornisce il server HTTP NetX con le stringhe di nome utente, password e area di autenticazione associate alla risorsa e restituisce il tipo di autenticazione necessario. Se non è necessaria alcuna autenticazione per la risorsa, il callback di autenticazione deve restituire il valore di **NX_HTTP_DONT_AUTHENTICATE**. In caso contrario, se è richiesta l'autenticazione di base per la risorsa specificata, la routine deve restituire **NX_HTTP_BASIC_AUTHENTICATE**. Infine, se è richiesta l'autenticazione digest MD5, la routine di callback deve restituire **NX_HTTP_DIGEST_AUTHENTICATE**. Se non è necessaria alcuna autenticazione per le risorse fornite dal server HTTP, il callback non è necessario e può essere fornito un puntatore NULL alla chiamata di creazione del server HTTP.

Il formato della routine di callback dell'applicazione di autenticazione è molto semplice e viene definito di seguito:

```c
UINT nx_http_server_authentication_check (NX_HTTP_SERVER *server_ptr,
                                         UINT request_type, CHAR *resource,
                                         CHAR **name, CHAR **password,
                                         CHAR **realm);
```

I parametri di input sono definiti come segue:

- *request_type* Specifica la richiesta client HTTP, le richieste valide sono definite come segue:
  - **NX_HTTP_SERVER_GET_REQUEST**
  - **NX_HTTP_SERVER_POST_REQUEST**
  - **NX_HTTP_SERVER_HEAD_REQUEST**
  - **NX_HTTP_SERVER_PUT_REQUEST**
  - **NX_HTTP_SERVER_DELETE_REQUEST**
- *risorsa* di Risorsa specifica richiesta.
- *nome* Destinazione per il puntatore al nome utente obbligatorio.
- *password* di Destinazione per il puntatore alla password richiesta.
- *area di autenticazione* Destinazione per il puntatore all'area di autenticazione per l'autenticazione.

Il valore restituito della routine di autenticazione specifica se è richiesta l'autenticazione. il nome, la password e i puntatori dell'area di autenticazione non vengono utilizzati se **NX_HTTP_DONT_AUTHENTICATE** viene restituito dalla routine di callback di autenticazione. In caso contrario, lo sviluppatore del server HTTP deve garantire che **NX_HTTP_MAX_USERNAME** e **NX_HTTP_MAX_PASSWORD** definiti in *nx_http_server. h* siano sufficientemente grandi per il nome utente e la password specificati nel callback di autenticazione. Per impostazione predefinita, le dimensioni sono pari a 20 caratteri.

## <a name="http-invalid-usernamepassword-callback"></a>Callback di nome utente/password non valido HTTP

Il callback facoltativo di nome utente/password non valido nel server HTTP NetX viene richiamato se il server HTTP riceve una combinazione di nome utente e password non valida in una richiesta client. Se l'applicazione server HTTP registra un callback con il server HTTP, verrà richiamato se l'autenticazione di base o Digest ha esito negativo *in nx_http_server_get_process*, in *nx_http_server_put_process* o *in nx_http_server_delete_process.*

Per registrare un callback con il server HTTP, il servizio seguente viene definito nel server HTTP NetX.

```c
UINT nx_http_server_invalid_userpassword_notify_set (NX_HTTP_SERVER *http_server_ptr,
                                                    UINT *invalid_username_password_callback)
                                                    (CHAR *resource,
                                                    ULONG *client_nx_address,
                                                    UINT request_type));
```
I tipi di richiesta sono definiti come segue:

- **NX_HTTP_SERVER_GET_REQUEST**
- **NX_HTTP_SERVER_POST_REQUEST**
- **NX_HTTP_SERVER_HEAD_REQUEST**
- **NX_HTTP_SERVER_PUT_REQUEST**
- **NX_HTTP_SERVER_DELETE_REQUEST**

## <a name="http-insert-gmt-date-header-callback"></a>Callback intestazione Data GMT inserimento HTTP

È disponibile un callback facoltativo nel server HTTP NetX per inserire un'intestazione di data nei messaggi di risposta. Questo callback viene richiamato quando il server HTTP sta rispondendo a una richiesta PUT o Get

Per registrare un callback della data GMT con il server HTTP, il servizio seguente viene definito nel server HTTP NetX.

```c
UINT _nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

Il tipo di dati NX_HTTP_SERVER_DATE viene definito nel modo seguente:

```c
typedef struct NX_HTTP_SERVER_DATE_STRUCT
{
    USHORT     nx_http_server_year;         /* Year        */
    UCHAR      nx_http_server_month;        /* Month       */
    UCHAR      nx_http_server_day;          /* Day         */
    UCHAR      nx_http_server_hour;         /* Hour        */
    UCHAR      nx_http_server_minute;       /* Minute      */
    UCHAR      nx_http_server_second;       /* Second      */
    UCHAR      nx_http_server_weekday;      /* Weekday     */
} NX_HTTP_SERVER_DATE;
```

## <a name="http-cache-info-get-callback"></a>Callback informazioni cache HTTP Get

Il server HTTP ha un callback per richiedere la validità massima e la data dall'applicazione HTTP per una risorsa specifica. Queste informazioni vengono usate per determinare se il server HTTP invia l'intera pagina in risposta a una richiesta Get del client. Se il "se modificato da" nella richiesta del client non viene trovato o non corrisponde alla data dell'Ultima modifica restituita dal callback Get cache, viene inviata l'intera pagina.

Per registrare il callback con il server HTTP, viene definito il seguente servizio:

```c
UINT _nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                                            UINT (*cache_info_get)
                                            (CHAR *, UINT *, NX_HTTP_SERVER_DATE *));
```

## <a name="http-multipart-support"></a>Supporto multipart HTTP

Multipurpose Internet Mail Extensions (MIME) è stato originariamente progettato per il protocollo SMTP, ma il suo utilizzo è stato distribuito in HTTP. MIME consente ai messaggi di contenere tipi di messaggi misti, ad esempio image/jpg e text/plain, all'interno dello stesso messaggio. Il server HTTP NetX ha aggiunto servizi per determinare il tipo di contenuto nei messaggi HTTP che contengono MIME dal client. Per abilitare il supporto multipart HTTP e utilizzare questi servizi, è necessario definire l'opzione di configurazione **NX_HTTP_MULTIPART_ENABLE** .

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                     NX_PACKET **packet_pptr,
                                     UCHAR *entity_header_buffer,
                                     ULONG buffer_size);

UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      ULONG *available_offset,
                                      ULONG *available_length);
```

Per altri dettagli sull'uso di questi servizi, vedere la descrizione nel capitolo 3 "Descrizione dei servizi HTTP".

## <a name="http-multi-thread-support"></a>Supporto multithreading HTTP

I servizi client HTTP NetX possono essere chiamati da più thread contemporaneamente. Tuttavia, le richieste di lettura o scrittura per un'istanza specifica del client HTTP devono essere eseguite in sequenza dallo stesso thread.

## <a name="http-rfcs"></a>RFC HTTP

Il protocollo HTTP di NetX è conforme a RFC1945 "Hypertext Transfer Protocol/1.0", RFC 2581 "TCP congestione del controllo", RFC 1122 "requisiti per gli host Internet" e RFC correlate.