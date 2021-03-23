---
title: Capitolo 1-Introduzione a HTTP e HTTPS
description: Questo capitolo presenta il modulo HTTP/HTTPS di Azure RTO NetX Duo per il Web.
author: philmea
ms.author: philmea
ms.date: 07/24/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c784843e4d3f11ee306e866223c0a19bfcba3b85
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822898"
---
# <a name="chapter-1---introduction-to-http-and-https"></a>Capitolo 1-Introduzione a HTTP e HTTPS

Il Hypertext Transfer Protocol (HTTP) è un protocollo progettato per il trasferimento del contenuto sul Web. HTTP è un protocollo semplice che utilizza i servizi di Transmission Control Protocol affidabili (TCP) per eseguire la relativa funzione di trasferimento del contenuto. Per questo motivo, HTTP è un protocollo di trasferimento del contenuto altamente affidabile. HTTP è uno dei protocolli applicativi più usati. Tutte le operazioni sul Web utilizzano il protocollo HTTP.

HTTPS è la versione protetta del protocollo HTTP, che implementa HTTP usando Transport Layer Security (TLS) per proteggere la connessione TCP sottostante. Oltre alla configurazione aggiuntiva necessaria per impostare TLS, HTTPS è sostanzialmente identico a HTTP in uso.

## <a name="general-http-requirements"></a>Requisiti HTTP generali

Per funzionare correttamente, il pacchetto HTTP Web NetX richiede l'installazione di NetX Duo (versione 5,10 o successiva). Inoltre, è necessario creare un'istanza IP ed è necessario abilitare TCP nella stessa istanza di IP. Per il supporto HTTPS, è necessario installare anche NetX Secure TLS (versione 5,11 o successiva). vedere la sezione successiva. Il file demo nella sezione "Small example System" del **capitolo 2** illustra il modo in cui questa operazione viene eseguita.

La parte client HTTP del pacchetto HTTP Web NetX non ha altri requisiti.

La parte relativa al server HTTP del pacchetto HTTP Web NetX presenta diversi requisiti aggiuntivi. Per prima cosa, è necessario l'accesso completo alla *porta tcp 80 nota* per la gestione di tutte le richieste HTTP del client. questa impostazione può essere modificata dall'applicazione su qualsiasi altra porta TCP valida. Il server HTTP è anche progettato per l'uso con FileX Embedded file system. Se FileX non è disponibile, l'utente può trasferire le parti di FileX utilizzate nel proprio ambiente. Questo argomento viene descritto nelle sezioni successive di questa guida.

## <a name="https-requirements"></a>Requisiti HTTPS

Per il corretto funzionamento di HTTPS, il pacchetto HTTP Web NetX richiede che siano installati NetX Duo (versione 5,10 o successiva) e NetX Secure TLS (versione 5,11 o successiva). Inoltre, è necessario creare un'istanza IP ed è necessario abilitare TCP nella stessa istanza IP per l'uso con TLS. È necessario inizializzare la sessione TLS con le routine di crittografia appropriate, un certificato CA attendibile e allocare spazio per i certificati che verranno forniti dagli host server remoti durante l'handshake TLS. Il file demo nella sezione "Small example HTTPS System" del **capitolo 2** indicherà come questa operazione viene eseguita.

La parte client HTTPS del pacchetto HTTP Web NetX non ha altri requisiti.

La parte relativa al server HTTPS del pacchetto HTTP Web NetX presenta diversi requisiti aggiuntivi. Per prima cosa, richiede l'accesso completo alla *porta TCP 443 nota* per la gestione di tutte le richieste HTTPS del client (come nel caso di http non crittografato, questa porta può essere modificata dall'applicazione). In secondo luogo, sarà necessario inizializzare la sessione TLS con le routine crittografiche appropriate e con un certificato di identità del server (o con una chiave precondivisa). Il server HTTPS è anche progettato per l'uso con FileX Embedded file system. Se FileX non è disponibile, l'utente può trasferire le parti di FileX utilizzate nel proprio ambiente. L'uso di FileX è descritto nelle sezioni successive di questa guida.

Per altre informazioni sulle opzioni di configurazione per TLS, vedere la documentazione di NetX Secure.

Se non specificato, tutte le funzionalità HTTP descritte in questo documento si applicano anche a HTTPS.

## <a name="http-and-https-constraints"></a>Vincoli HTTP e HTTPS

NetX Web HTTP implementa lo standard HTTP 1,1. Ecco tuttavia i vincoli seguenti:

1. Il pipelining della richiesta non è supportato
1. Il server HTTP supporta l'autenticazione di base e del digest MD5, ma non MD5-sess. Attualmente, il client HTTP supporta solo l'autenticazione di base. Quando si utilizza TLS per HTTPS, è possibile che venga comunque utilizzata l'autenticazione HTTP.
1. Non è supportata alcuna compressione del contenuto.
1. Le richieste di traccia, opzioni e connessione non sono supportate.
1. Il pool di pacchetti associato al server o al client HTTP deve essere sufficientemente grande da contenere l'intestazione HTTP completa.
1. I servizi client HTTP sono destinati solo al trasferimento del contenuto. in questo pacchetto non sono disponibili utilità di visualizzazione.

## <a name="http-url-resource-names"></a>URL HTTP (nomi di risorse)

Il protocollo HTTP è progettato per trasferire il contenuto sul Web. Il contenuto richiesto viene specificato dall'URL (Universal Resource Locator). Questo è il componente principale di ogni richiesta HTTP. Gli URL iniziano sempre con il carattere "/" e in genere corrispondono ai file nel server HTTP. Di seguito sono elencate le estensioni di file HTTP comuni:

- Hypertext Markup Language **. htm** (o **. HTML**) (HTML)
- **txt** Testo ASCII normale
- **. gif** Immagine GIF binaria
- **. xbm** Immagine xbitmap binaria

## <a name="http-client-requests"></a>Richieste client HTTP

Il protocollo HTTP ha un meccanismo semplice per la richiesta di contenuto Web. È disponibile un set di comandi HTTP standard emessi dal client dopo che una connessione è stata stabilita correttamente sulla *porta TCP nota 80 (porta 443 per HTTPS)*. Di seguito sono riportati alcuni dei comandi HTTP di base:

- **Ottieni *risorsa* http/1.1** Ottenere la risorsa specificata
- **Post- *risorsa* http/1.1** Ottiene la risorsa specificata e passa l'input collegato al server HTTP
- ***Risorsa* Head http/1.1** Gestito come GET ma non contenuto viene restituito dal server HTTP
- **Inserisci *risorsa* http/1.1** Inserisci risorsa nel server HTTP
- **Elimina *risorsa* http/1.1** Elimina risorsa nel server

Questi comandi ASCII vengono generati internamente dai Web browser e dai servizi client HTTP Web di NetX per eseguire operazioni HTTP con un server HTTP.

Si noti che l'applicazione client HTTP deve usare la porta 80 o la porta 443 se viene usato HTTPS. Entrambe le API HTTP client e server accettano la porta come parametro: le macro NX_WEB_HTTP_SERVER_PORT (porta 80) e NX_WEB_HTTPS_SERVER_PORT (porta 443) sono definite per praticità. La porta del server HTTP può anche essere modificata in fase di esecuzione tramite il servizio *nx_web_http_client_set_connect_port ()* . Per ulteriori informazioni su questo servizio, vedere il capitolo 4.

## <a name="http-server-responses"></a>Risposte al server HTTP

Il server HTTP utilizza la stessa *porta TCP 80 (443 per HTTPS)* per inviare le risposte del comando client. Una volta che il server HTTP elabora il comando client, restituisce una stringa di risposta ASCII che include un codice di stato numerico a 3 cifre. La risposta numerica viene utilizzata dal software client HTTP per determinare se l'operazione ha avuto esito positivo o negativo. Di seguito è riportato un elenco di varie risposte del server HTTP ai comandi client:

- la richiesta **200** è stata completata
- la richiesta **400** non è stata creata correttamente
- **401** richiesta non autorizzata, il client deve inviare l'autenticazione
- **404** la risorsa specificata nella richiesta non è stata trovata
- **500** errore interno del server http
- richiesta **501** non implementata dal server http
- **502** il servizio non è disponibile

Ad esempio, una richiesta client corretta per inserire il file "test.htm" viene risposto con il messaggio "HTTP/1.1 200 OK".

## <a name="http-communication"></a>Comunicazione HTTP

Come indicato in precedenza, il server HTTP utilizza la *porta TCP nota 80 (443 per HTTPS)* per il campo delle richieste client. I client HTTP possono usare qualsiasi porta TCP disponibile per le connessioni in uscita. La sequenza generale degli eventi HTTP è la seguente:

**Richiesta HTTP Get**:

1. Il client invia la connessione TCP al server porta 80 (o 443 per HTTPS).
1. Se si utilizza HTTPS, la connessione TCP è seguita da un handshake TLS per autenticare il server e stabilire un canale sicuro.
1. Il client invia la richiesta "**get *Resource* http/1.1**" (insieme ad altre informazioni di intestazione).
1. Il server compila un messaggio "**http/1.1 200 OK**" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa (se presente).
1. Il server si disconnette dal client (TLS viene arrestato se viene usato HTTPS).
1. Il client si disconnette dal socket (TLS viene arrestato dopo l'avviso di disconnessione dal server).

**Richiesta HTTP PUT**:

1. Il client invia la connessione TCP al server porta 80 (o 443).
1. Se si utilizza HTTPS, la connessione TCP è seguita da un handshake TLS per autenticare il server e stabilire un canale sicuro.
1. Il client invia la richiesta "PUT Resource HTTP/1.1", insieme ad altre informazioni di intestazione e seguita dal contenuto della risorsa.
1. Il server compila un messaggio "HTTP/1.1 200 OK" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa.
1. Il server esegue una disconnessione.
1. Il client esegue una disconnessione.

> [!NOTE]
> Come indicato in precedenza, il server HTTP può modificare la porta di connessione predefinita (80 o 443) in fase di esecuzione un'altra porta usando il *nx_web_http_client_set_connect_port ()* per i server Web che usano porte alternative per connettersi ai client.

## <a name="http-authentication"></a>Autenticazione HTTP

L'autenticazione HTTP è facoltativa e non è necessaria per tutte le richieste Web. Esistono due tipi di autenticazione, ovvero *Basic* e *digest*. L'autenticazione di base equivale all'autenticazione del *nome* e della *password* presente in molti protocolli. Nell'autenticazione di base HTTP, il nome e le password vengono concatenati e codificati nel formato Base64. Lo svantaggio principale dell'autenticazione di base è il nome e la password vengono trasmessi apertamente nella richiesta. In questo modo è piuttosto semplice che il nome e la password vengano rubati. L'autenticazione del digest risolve questo problema senza trasmettere mai il nome e la password nella richiesta. Viene invece usato un algoritmo per derivare un digest a 128 bit da nome, password e altre informazioni. Il server HTTP Web NetX supporta l'algoritmo digest MD5 standard.

Quando è richiesta l'autenticazione? Il server HTTP decide se una risorsa richiesta richiede l'autenticazione. Se è richiesta l'autenticazione e la richiesta del client non include l'autenticazione corretta, al client viene inviata una risposta "HTTP/1.1 401 non autorizzato" con il tipo di autenticazione richiesto. Il client deve quindi creare una nuova richiesta con l'autenticazione corretta.

Quando si utilizza HTTPS, il server HTTPS può comunque utilizzare l'autenticazione HTTP. In questo caso, TLS viene usato per crittografare tutto il traffico HTTP, quindi l'uso dell'autenticazione HTTP di *base* non costituisce un rischio per la sicurezza. L'autenticazione del *digest* è consentita, ma non offre miglioramenti significativi per la sicurezza rispetto all'autenticazione di base su TLS.

## <a name="http-authentication-callback"></a>Callback di autenticazione HTTP

Come indicato in precedenza, l'autenticazione HTTP è facoltativa e non è necessaria per tutti i trasferimenti Web. Inoltre, l'autenticazione è in genere dipendente dalle risorse. L'accesso ad alcune risorse sul server richiede l'autenticazione, mentre altri no. Il pacchetto del server HTTP Web NetX consente all'applicazione di specificare (tramite la chiamata ***nx_web_http_server_create*** ) una routine di callback di autenticazione che viene chiamata all'inizio della gestione di ogni richiesta del client http.

La routine di callback fornisce il server HTTP Web NetX con le stringhe di nome utente, password e area di autenticazione associate alla risorsa e restituisce il tipo di autenticazione necessario. Se non è necessaria alcuna autenticazione per la risorsa, il callback di autenticazione deve restituire il valore di **NX_WEB_HTTP_DONT_AUTHENTICATE**. In caso contrario, se è richiesta l'autenticazione di base per la risorsa specificata, la routine deve restituire **NX_WEB_HTTP_BASIC_AUTHENTICATE**. Infine, se è richiesta l'autenticazione digest MD5, la routine di callback deve restituire **NX_WEB_HTTP_DIGEST_AUTHENTICATE**. Se non è necessaria alcuna autenticazione per le risorse fornite dal server HTTP, il callback non è necessario e può essere fornito un puntatore NULL alla chiamata di creazione del server HTTP.

Il formato della routine di callback dell'applicazione di autenticazione è molto semplice e viene definito di seguito:

```C
UINT nx_web_http_server_authentication_check(NX_WEB_HTTP_SERVER *server_ptr,
    UINT request_type, CHAR *resource,
    CHAR **name, CHAR **password,
    CHAR **realm);
```

I parametri di input sono definiti come segue:

- **request_type** Specifica la richiesta client HTTP, le richieste valide sono definite come segue:
  - **NX_WEB_HTTP_SERVER_GET_REQUEST**
  - **NX_WEB_HTTP_SERVER_POST_REQUEST**
  - **NX_WEB_HTTP_SERVER_HEAD_REQUEST**
  - **NX_WEB_HTTP_SERVER_PUT_REQUEST**
  - **NX_WEB_HTTP_SERVER_DELETE_REQUEST**
- **risorsa** di Risorsa specifica richiesta.
- **nome** Destinazione per il puntatore al nome utente obbligatorio.
- **password** di Destinazione per il puntatore alla password richiesta.
- **area di autenticazione** Destinazione per il puntatore all'area di autenticazione per l'autenticazione.

Il valore restituito della routine di autenticazione specifica se è richiesta l'autenticazione. il nome, la password e i puntatori dell'area di autenticazione non vengono utilizzati se **NX_WEB_HTTP_DONT_AUTHENTICATE** viene restituito dalla routine di callback di autenticazione. In caso contrario, lo sviluppatore del server HTTP deve garantire che **NX_WEB_HTTP_MAX_USERNAME** e **NX_WEB_HTTP_MAX_PASSWORD** definiti in *nx_web_http_server. h* siano sufficientemente grandi per il nome utente e la password specificati nel callback di autenticazione. Entrambi hanno una dimensione predefinita di 20 caratteri.

## <a name="http-invalid-usernamepassword-callback"></a>Callback di nome utente/password non valido HTTP

Il callback facoltativo di nome utente/password non valido nel server HTTP Web NetX viene richiamato se il server HTTP riceve una combinazione di nome utente e password non valida in una richiesta client. Se l'applicazione server HTTP registra un callback con il server HTTP, verrà richiamato se l'autenticazione di base o Digest ha esito negativo *in nx_web_http_server_get_process ()*, in *nx_web_http_server_put_process ()* o *in nx_web_http_server_delete_process ().*

Per registrare un callback con il server HTTP, viene definito il seguente servizio per il server HTTP Web NetX.

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

## <a name="http-insert-gmt-date-header-callback"></a>Callback intestazione Data GMT inserimento HTTP

È disponibile un callback facoltativo nel server HTTP Web NetX per inserire un'intestazione di data nei messaggi di risposta. Questo callback viene richiamato quando il server HTTP sta rispondendo a una richiesta PUT o Get

Per registrare un callback della data GMT con il server HTTP, viene definito il seguente servizio.

```C
UINT nx_web_http_server_gmt_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID (*gmt_get)(NX_WEB_HTTP_SERVER_DATE *date);
```

Il tipo di dati NX_WEB_HTTP_SERVER_DATE viene definito nel modo seguente:

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

## <a name="http-cache-info-get-callback"></a>Callback informazioni cache HTTP Get

Il server HTTP ha un callback per richiedere la validità e la data massime dall'applicazione HTTP per una risorsa specifica. Queste informazioni vengono usate per determinare se il server HTTP Invia un'intera pagina in risposta a una richiesta Get del client. Se il "se modificato da" nella richiesta del client non viene trovato o non corrisponde alla data dell'Ultima modifica restituita dal callback Get cache, viene inviata l'intera pagina.

Per registrare il callback con il server HTTP, viene definito il seguente servizio:

```C
UINT nx_web_http_server_cache_info_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT (*cache_info_get)
    (CHAR *, UINT *, NX_WEB_HTTP_SERVER_DATE *));
```

## <a name="http-chunked-transfer-coding-support"></a>Supporto per la codifica di trasferimento Chunked HTTP

Quando non è possibile determinare la lunghezza totale del messaggio HTTP prima di inviarlo, la funzionalità di codifica di trasferimento Chunked può essere usata per inviare messaggi come serie di blocchi senza il campo di intestazione "Content-Length". Questa funzionalità è supportata in tutti i messaggi di richiesta e risposta HTTP. Come ricevitore, questa funzionalità è supportata e l'intestazione del blocco viene elaborata in modo trasparente dalla logica interna. Come mittente, le API *nx_web_http_client_request_chunked_set* e *nx_web_http_server_response_chunked_set* devono essere richiamate rispettivamente dal client e dal server.

```C
UINT nx_web_http_client_request_chunked_set(NX_WEB_HTTP_CLIENT *client_ptr,
    UINT chunk_size,
    NX_PACKET *packet_ptr);

UINT nx_web_http_server_response_chunked_set(NX_WEB_HTTP_SERVER *server_ptr,
    UINT chunk_size,
    NX_PACKET *packet_ptr);
```

Per ulteriori informazioni su questi servizi, vedere le relative descrizioni nel capitolo 3 "Descrizione dei servizi HTTP".

## <a name="http-multipart-support"></a>Supporto multipart HTTP

Multipurpose Internet Mail Extensions (MIME) è stato originariamente progettato per il protocollo SMTP, ma il suo utilizzo è stato distribuito in HTTP. MIME consente ai messaggi di contenere tipi di messaggi misti, ad esempio image/jpg e text/plain, all'interno dello stesso messaggio. Il server HTTP Web NetX dispone di servizi per determinare il tipo di contenuto nei messaggi HTTP che contengono MIME dal client. Per abilitare il supporto multipart HTTP e utilizzare questi servizi, è necessario definire l'opzione di configurazione **NX_WEB_HTTP_MULTIPART_ENABLE** .

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

Per altri dettagli sull'uso di questi servizi, vedere la descrizione nel capitolo 3 "Descrizione dei servizi HTTP".

## <a name="http-multi-thread-support"></a>Supporto multithreading HTTP

I servizi client HTTP Web NetX possono essere chiamati da più thread contemporaneamente. Tuttavia, le richieste di lettura o scrittura per un'istanza specifica del client HTTP devono essere eseguite in sequenza dallo stesso thread.

Se si usa HTTPS, i servizi client HTTP Web NetX possono essere chiamati da più thread, ma a causa della complessità aggiunta della funzionalità TLS sottostante ogni thread deve avere una singola istanza del client HTTP indipendente (struttura di controllo NX_WEB_HTTP_CLIENT).

## <a name="http-rfcs"></a>RFC HTTP

Il protocollo HTTP Web di NetX è conforme a RFC1945 "Hypertext Transfer Protocol/1.0", RFC 2616 "Hypertext Transfer Protocol – HTTP/1.1", RFC 2581 "TCP congestione congestione", RFC 1122 "requisiti per gli host Internet" e RFC correlati.

Per HTTPS, HTTP Web NetX è conforme a RFC 2818 "HTTP over TLS".
