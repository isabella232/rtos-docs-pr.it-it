---
title: Capitolo 1 - Introduzione a HTTP e HTTPS
description: Questo capitolo presenta il Azure RTOS Http/HTTPS di NetX Duo per il Web.
author: philmea
ms.author: philmea
ms.date: 07/24/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e5f50419be3171d3df8544d1b34d603822f339785923f8a8199dc5b5ddcac281
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801753"
---
# <a name="chapter-1---introduction-to-http-and-https"></a>Capitolo 1 - Introduzione a HTTP e HTTPS

Il Hypertext Transfer Protocol (HTTP) è un protocollo progettato per il trasferimento di contenuto sul Web. HTTP è un protocollo semplice che usa i servizi Reliable Transmission Control Protocol (TCP) per eseguire la funzione di trasferimento del contenuto. Per questo, HTTP è un protocollo di trasferimento del contenuto altamente affidabile. HTTP è uno dei protocolli applicativi più usati. Tutte le operazioni sul Web utilizzano il protocollo HTTP.

HTTPS è la versione sicura del protocollo HTTP, che implementa HTTP usando Transport Layer Security (TLS) per proteggere la connessione TCP sottostante. Oltre alla configurazione aggiuntiva necessaria per configurare TLS, HTTPS è fondamentalmente identico a HTTP in uso.

## <a name="general-http-requirements"></a>Requisiti HTTP generali

Per il corretto funzionamento, il pacchetto HTTP Web NetX richiede l'installazione di NetX Duo (versione 5.10 o successiva). È inoltre necessario creare un'istanza IP e il protocollo TCP deve essere abilitato nella stessa istanza IP. Per il supporto HTTPS, è necessario installare anche NetX Secure TLS (versione 5.11 o successiva) (vedere la sezione successiva). Il file demo nella sezione "Small Example System" del **capitolo 2** illustra come eseguire questa operazione.

La parte client HTTP del pacchetto HTTP Web NetX non presenta altri requisiti.

La parte Server HTTP del pacchetto HTTP Web NetX presenta diversi requisiti aggiuntivi. In primo luogo, è necessario l'accesso completo alla porta TCP *nota 80* per la gestione di tutte le richieste HTTP client (questa operazione può essere modificata dall'applicazione in qualsiasi altra porta TCP valida). Il server HTTP è progettato anche per l'uso con l'file system FileX incorporato. Se FileX non è disponibile, l'utente può convertire le parti di FileX usate nel proprio ambiente. Questo argomento verrà illustrato nelle sezioni successive di questa guida.

## <a name="https-requirements"></a>Requisiti HTTPS

Per il corretto funzionamento di HTTPS, il pacchetto HTTP Web NetX richiede l'installazione di NetX Duo (versione 5.10 o successiva) e di NetX Secure TLS (versione 5.11 o successiva). È inoltre necessario creare un'istanza IP e il protocollo TCP deve essere abilitato nella stessa istanza IP per l'uso con TLS. La sessione TLS dovrà essere inizializzata con le routine di crittografia appropriate, un certificato ca attendibile e lo spazio deve essere allocato per i certificati che verranno forniti dagli host del server remoto durante l'handshake TLS. Il file demo nella sezione "Small Example HTTPS System" del **capitolo 2** illustra come eseguire questa operazione.

La parte client HTTPS del pacchetto HTTP Web NetX non presenta altri requisiti.

La parte relativa al server HTTPS del pacchetto HTTP Web NetX presenta diversi requisiti aggiuntivi. In primo luogo, è necessario l'accesso completo alla porta TCP *nota 443* per la gestione di tutte le richieste HTTPS client (come nel caso di HTTP in testo non crittografato, questa porta può essere modificata dall'applicazione). In secondo momento, la sessione TLS dovrà essere inizializzata con routine di crittografia appropriate e un certificato di identità del server (o chiave precondidata). Il server HTTPS è progettato anche per l'uso con fileX incorporato file system. Se FileX non è disponibile, l'utente può convertire le parti di FileX usate nel proprio ambiente. L'uso di FileX viene illustrato nelle sezioni successive di questa guida.

Per altre informazioni sulle opzioni di configurazione per TLS, vedere la documentazione di NetX Secure.

Se non specificato, tutte le funzionalità HTTP descritte in questo documento si applicano anche a HTTPS.

## <a name="http-and-https-constraints"></a>Vincoli HTTP e HTTPS

Http Web NetX implementa lo standard HTTP 1.1. Tuttavia, di seguito sono riportati i vincoli seguenti:

1. Il pipelining delle richieste non è supportato
1. Il server HTTP supporta sia l'autenticazione digest di base che l'autenticazione digest MD5, ma non l'autenticazione MD5. Al momento, il client HTTP supporta solo l'autenticazione di base. Quando si usa TLS per HTTPS, è comunque possibile usare l'autenticazione HTTP.
1. Non è supportata alcuna compressione del contenuto.
1. Le richieste TRACE, OPTIONS e CONNECT non sono supportate.
1. Il pool di pacchetti associato al server o al client HTTP deve essere sufficientemente grande da contenere l'intestazione HTTP completa.
1. I servizi client HTTP sono solo per il trasferimento del contenuto. In questo pacchetto non sono disponibili utilità di visualizzazione.

## <a name="http-url-resource-names"></a>URL HTTP (nomi di risorse)

Il protocollo HTTP è progettato per trasferire il contenuto sul Web. Il contenuto richiesto viene specificato dall'URL (Universal Resource Locator). Questo è il componente principale di ogni richiesta HTTP. Gli URL iniziano sempre con un carattere "/" e in genere corrispondono ai file nel server HTTP. Di seguito sono riportate le estensioni di file HTTP comuni:

- **.htm** (o **.html**) Hypertext Markup Language (HTML)
- **.txt** Testo ASCII normale
- **.gif** Immagine GIF binaria
- **.xbm** Immagine Xbitmap binaria

## <a name="http-client-requests"></a>Richieste client HTTP

HTTP dispone di un meccanismo semplice per la richiesta di contenuto Web. È disponibile un set di comandi HTTP standard emessi dal client dopo che è stata stabilita una connessione sulla porta TCP *nota 80 (porta 443 per HTTPS).* Di seguito sono illustrati alcuni dei comandi HTTP di base:

- **GET *risorsa* HTTP/1.1** Ottenere la risorsa specificata
- **RISORSA  POST HTTP/1.1** Ottenere la risorsa specificata e passare l'input associato al server HTTP
- **RISORSA  HEAD HTTP/1.1** Considerato come GET, ma non il contenuto viene restituito dal server HTTP
- **PUT *resource* HTTP/1.1** Inserire la risorsa nel server HTTP
- **DELETE *resource* HTTP/1.1** Eliminare una risorsa nel server

Questi comandi ASCII vengono generati internamente dai Web browser e dai servizi client HTTP Web NetX per eseguire operazioni HTTP con un server HTTP.

Si noti che l'applicazione client HTTP deve usare la porta 80 o la porta 443 se si usa HTTPS. Entrambe le API HTTP client e server accettano la porta come parametro: le macro NX_WEB_HTTP_SERVER_PORT (porta 80) e NX_WEB_HTTPS_SERVER_PORT (porta 443) sono definite per praticità. La porta del server HTTP può essere modificata anche in fase di esecuzione *usando il nx_web_http_client_set_connect_port().* Per altri dettagli su questo servizio, vedere il capitolo 4.

## <a name="http-server-responses"></a>Risposte del server HTTP

Il server HTTP usa la stessa *porta TCP 80 nota (443* per HTTPS) per inviare le risposte dei comandi client. Dopo l'elaborazione del comando Client, il server HTTP restituisce una stringa di risposta ASCII che include un codice di stato numerico a 3 cifre. La risposta numerica viene usata dal software client HTTP per determinare se l'operazione ha avuto esito positivo o negativo. Di seguito è riportato un elenco di varie risposte del server HTTP ai comandi client:

- **200** Richiesta riuscita
- **400** Richiesta non formata correttamente
- **401 Richiesta** non autorizzata, il client deve inviare l'autenticazione
- **404** La risorsa specificata nella richiesta non è stata trovata
- **500** Errore interno del server HTTP
- **501** Richiesta non implementata dal server HTTP
- **Il servizio 502** non è disponibile

Ad esempio, una richiesta client riuscita per INSERIRE il file "test.htm" viene inviata una risposta con il messaggio "HTTP/1.1 200 OK".

## <a name="http-communication"></a>Comunicazione HTTP

Come accennato in precedenza, il server HTTP usa la nota porta *TCP 80 (443* per HTTPS) per il campo Richieste client. I client HTTP possono usare qualsiasi porta TCP disponibile per le connessioni in uscita. La sequenza generale di eventi HTTP è la seguente:

**Richiesta HTTP GET:**

1. Il client esegue la connessione TCP alla porta 80 (o 443 per HTTPS).
1. Se si usa HTTPS, la connessione TCP è seguita da un handshake TLS per autenticare il server e stabilire un canale sicuro.
1. Il client invia **la richiesta "GET *resource* HTTP/1.1"**(insieme ad altre informazioni di intestazione).
1. Il server compila un messaggio "**HTTP/1.1 200 OK**" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa (se presente).
1. Il server si disconnette dal client (TLS viene arrestato se viene usato HTTPS).
1. Il client si disconnette dal socket (TLS viene arrestato in seguito all'avviso di disconnessione dal server).

**Richiesta HTTP PUT:**

1. Il client esegue la connessione TCP alla porta 80 (o 443) del server.
1. Se si usa HTTPS, la connessione TCP è seguita da un handshake TLS per autenticare il server e stabilire un canale sicuro.
1. Il client invia la richiesta "PUT resource HTTP/1.1" insieme ad altre informazioni sull'intestazione e seguita dal contenuto della risorsa.
1. Il server compila un messaggio "HTTP/1.1 200 OK" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa.
1. Il server esegue una disconnessione.
1. Il client esegue una disconnessione.

> [!NOTE]
> Come accennato in precedenza, il server HTTP può modificare la porta di connessione predefinita (80 o 443) in fase di esecuzione un'altra porta usando *nx_web_http_client_set_connect_port()* per i server Web che usano porte alternative per la connessione ai client.

## <a name="http-authentication"></a>Autenticazione HTTP

L'autenticazione HTTP è facoltativa e non è necessaria per tutte le richieste Web. Esistono due tipi di autenticazione, in particolare *di base* e *digest.* L'autenticazione di base equivale *all'autenticazione* del *nome e della password* presente in molti protocolli. Nell'autenticazione di base HTTP il nome e le password vengono concatenati e codificati nel formato Base64. Lo svantaggio principale dell'autenticazione di base è che il nome e la password vengono trasmessi apertamente nella richiesta. In questo modo il nome e la password possono essere rubati con facilità. L'autenticazione digest risolve questo problema non trasmettendo mai il nome e la password nella richiesta. Viene invece usato un algoritmo per derivare un digest a 128 bit dal nome, dalla password e da altre informazioni. Il server HTTP Web NetX supporta l'algoritmo digest MD5 standard.

Quando è necessaria l'autenticazione? Il server HTTP decide se una risorsa richiesta richiede l'autenticazione. Se è necessaria l'autenticazione e la richiesta client non includeva l'autenticazione appropriata, al client viene inviata una risposta "HTTP/1.1 401 Non autorizzato" con il tipo di autenticazione richiesto. Si prevede quindi che il client formi una nuova richiesta con l'autenticazione appropriata.

Quando si usa HTTPS, il server HTTPS può comunque usare l'autenticazione HTTP. In questo caso, TLS viene usato per  crittografare tutto il traffico HTTP, in modo che l'uso dell'autenticazione HTTP di base non rappresenti un rischio per la sicurezza. *Anche l'autenticazione* digest è consentita, ma non offre miglioramenti significativi della sicurezza rispetto all'autenticazione di base su TLS.

## <a name="http-authentication-callback"></a>Callback di autenticazione HTTP

Come accennato in precedenza, l'autenticazione HTTP è facoltativa e non è necessaria in tutti i trasferimenti Web. Inoltre, l'autenticazione dipende in genere dalle risorse. L'accesso ad alcune risorse nel server richiede l'autenticazione, mentre altre no. Il pacchetto del server HTTP Web NetX consente all'applicazione di specificare (tramite la chiamata ***nx_web_http_server_create)*** una routine di callback di autenticazione che viene chiamata all'inizio della gestione di ogni richiesta client HTTP.

La routine di callback fornisce al server HTTP Web NetX le stringhe nome utente, password e area di autenticazione associate alla risorsa e restituisce il tipo di autenticazione necessario. Se non è necessaria alcuna autenticazione per la risorsa, il callback di autenticazione deve restituire il valore **di NX_WEB_HTTP_DONT_AUTHENTICATE**. In caso contrario, se è necessaria l'autenticazione di base per la risorsa specificata, la routine deve restituire **NX_WEB_HTTP_BASIC_AUTHENTICATE**. Infine, se è necessaria l'autenticazione del digest MD5, la routine di callback deve restituire **NX_WEB_HTTP_DIGEST_AUTHENTICATE**. Se non è necessaria alcuna autenticazione per qualsiasi risorsa fornita dal server HTTP, il callback non è necessario ed è possibile specificare un puntatore NULL alla chiamata di creazione del server HTTP.

Il formato della routine di callback di autenticazione dell'applicazione è molto semplice ed è definito di seguito:

```C
UINT nx_web_http_server_authentication_check(NX_WEB_HTTP_SERVER *server_ptr,
    UINT request_type, CHAR *resource,
    CHAR **name, CHAR **password,
    CHAR **realm);
```

I parametri di input sono definiti come segue:

- **request_type** Specifica la richiesta del client HTTP. Le richieste valide sono definite come segue:
  - **NX_WEB_HTTP_SERVER_GET_REQUEST**
  - **NX_WEB_HTTP_SERVER_POST_REQUEST**
  - **NX_WEB_HTTP_SERVER_HEAD_REQUEST**
  - **NX_WEB_HTTP_SERVER_PUT_REQUEST**
  - **NX_WEB_HTTP_SERVER_DELETE_REQUEST**
- **risorsa** Risorsa specifica richiesta.
- **name** Destinazione per il puntatore al nome utente richiesto.
- **password** Destinazione per il puntatore alla password richiesta.
- **area di autenticazione** Destinazione per il puntatore all'area di autenticazione per questa autenticazione.

Il valore restituito della routine di autenticazione specifica se è necessaria l'autenticazione. I puntatori name, password e realm non vengono usati se **NX_WEB_HTTP_DONT_AUTHENTICATE** viene restituito dalla routine di callback di autenticazione. In caso contrario, lo  sviluppatore del server HTTP deve assicurarsi che le NX_WEB_HTTP_MAX_USERNAME e **NX_WEB_HTTP_MAX_PASSWORD** definite in *nx_web_http_server.h* siano sufficienti per il nome utente e la password specificati nel callback di autenticazione. Entrambe hanno una dimensione predefinita di 20 caratteri.

## <a name="http-invalid-usernamepassword-callback"></a>Callback http nome utente/password non valido

Il callback facoltativo di nome utente/password non valido nel server HTTP Web NetX viene richiamato se il server HTTP riceve una combinazione di nome utente e password non valida in una richiesta client. Se l'applicazione server HTTP registra un callback con il server HTTP, verrà richiamata se l'autenticazione di base o digest non riesce *in nx_web_http_server_get_process(),* *in nx_web_http_server_put_process()* o *in nx_web_http_server_delete_process().*

Per registrare un callback con il server HTTP, viene definito il servizio seguente per il server HTTP Web NetX.

```C
UINT nx_web_http_server_invalid_userpassword_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*invalid_username_password_callback)
        (CHAR *resource, ULONG *client_nx_address,
        UINT request_type));
```

I tipi di richiesta sono definiti come segue:

- **NX_WEB_HTTP_SERVER_GET_REQUEST**
- **NX_WEB_HTTP_SERVER_POST_REQUEST**
- **NX_WEB_HTTP_SERVER_HEAD_REQUEST**
- **NX_WEB_HTTP_SERVER_PUT_REQUEST**
- **NX_WEB_HTTP_SERVER_DELETE_REQUEST**

## <a name="http-insert-gmt-date-header-callback"></a>HTTP Insert GMT Date Header Callback

È disponibile un callback facoltativo nel server HTTP Web NetX per inserire un'intestazione di data nei messaggi di risposta. Questo callback viene richiamato quando il server HTTP risponde a una richiesta put o get

Per registrare un callback di data GMT con il server HTTP, viene definito il servizio seguente.

```C
UINT nx_web_http_server_gmt_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID (*gmt_get)(NX_WEB_HTTP_SERVER_DATE *date);
```

Il NX_WEB_HTTP_SERVER_DATE di dati è definito come segue:

```C
typedef struct NX_WEB_HTTP_SERVER_DATE_STRUCT
{
    USHORT nx_web_http_server_year; /* Year */
    UCHAR nx_web_http_server_month; /* Month */
    UCHAR nx_web_http_server_day; /* Day */
    UCHAR nx_web_http_server_hour; /* Hour */
    UCHAR nx_web_http_server_minute; /* Minute */
    UCHAR nx_web_http_server_second; /* Second */
    UCHAR nx_web_http_server_weekday; /* Weekday */
} NX_WEB_HTTP_SERVER_DATE;
```

## <a name="http-cache-info-get-callback"></a>Callback Get delle informazioni sulla cache HTTP

Il server HTTP ha un callback per richiedere la durata e la data massime dall'applicazione HTTP per una risorsa specifica. Queste informazioni vengono usate per determinare se il server HTTP invia un'intera pagina in risposta a una richiesta Client Get. Se il valore "if modified since" nella richiesta Client non viene trovato o non corrisponde alla data dell'ultima modifica restituita dal callback get cache, viene inviata l'intera pagina.

Per registrare il callback con il server HTTP, viene definito il servizio seguente:

```C
UINT nx_web_http_server_cache_info_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT (*cache_info_get)
    (CHAR *, UINT *, NX_WEB_HTTP_SERVER_DATE *));
```

## <a name="http-chunked-transfer-coding-support"></a>Supporto della codifica per il trasferimento in blocchi HTTP

Quando non è possibile determinare la lunghezza totale del messaggio HTTP prima dell'invio, è possibile usare la funzionalità chunked transfer coding per inviare messaggi come serie di blocchi senza il campo di intestazione "Content-Length". Questa funzionalità è supportata in tutti i messaggi di richiesta e risposta HTTP. In quanto ricevitore, questa funzionalità è supportata e l'intestazione del blocco viene elaborata in modo trasparente dalla logica interna. In quanto mittente, *l'api nx_web_http_client_request_chunked_set* e *nx_web_http_server_response_chunked_set* devono essere richiamate rispettivamente dal client e dal server.

```C
UINT nx_web_http_client_request_chunked_set(NX_WEB_HTTP_CLIENT *client_ptr,
    UINT chunk_size,
    NX_PACKET *packet_ptr);

UINT nx_web_http_server_response_chunked_set(NX_WEB_HTTP_SERVER *server_ptr,
    UINT chunk_size,
    NX_PACKET *packet_ptr);
```

Per altre informazioni su questi servizi, vedere le relative descrizioni nel capitolo 3 "Descrizione dei servizi HTTP".

## <a name="http-multipart-support"></a>Supporto multipart HTTP

Multipurpose Internet Mail Extensions (MIME) era originariamente destinato al protocollo SMTP, ma il suo utilizzo è stato distribuito in HTTP. MIME consente ai messaggi di contenere tipi misti di messaggi (ad esempio image/jpg e text/plain) all'interno dello stesso messaggio. Il server HTTP Web NetX dispone di servizi per determinare il tipo di contenuto nei messaggi HTTP contenenti MIME dal client. Per abilitare il supporto multipart HTTP e usare questi servizi, è necessario **NX_WEB_HTTP_MULTIPART_ENABLE** l'opzione di configurazione .

```C
UINT nx_web_http_server_get_entity_header(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    UCHAR *entity_header_buffer,
    ULONG buffer_size);

UINT nx_web_http_server_get_entity_content(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    ULONG *available_offset,
    ULONG *available_length);
```

Per altri dettagli sull'uso di questi servizi, vedere la relativa descrizione nel capitolo 3 "Descrizione dei servizi HTTP".

## <a name="http-multi-thread-support"></a>Supporto multi-thread HTTP

I servizi client HTTP Web NetX possono essere chiamati contemporaneamente da più thread. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client HTTP devono essere eseguite in sequenza dallo stesso thread.

Se si usa HTTPS, i servizi client HTTP Web NetX possono essere chiamati da più thread, ma a causa della complessità aggiunta della funzionalità TLS sottostante ogni thread deve avere una singola istanza del client HTTP indipendente (struttura di controllo NX_WEB_HTTP_CLIENT).

## <a name="http-rfcs"></a>RFC HTTP

Http Web NetX è conforme a RFC1945 "Hypertext Transfer Protocol/1.0", RFC 2616 "Hypertext Transfer Protocol – HTTP/1.1", RFC 2581 "TCP Congestion Control", RFC 1122 "Requirements for Internet Hosts" e RFC correlate.

Per HTTPS, NetX Web HTTP è conforme a RFC 2818 "HTTP su TLS".
