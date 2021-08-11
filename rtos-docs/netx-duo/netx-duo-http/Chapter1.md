---
title: Capitolo 1 - Introduzione alla Azure RTOS HTTP di NetX Duo
description: Questo capitolo presenta il modulo HTTP Azure RTOS NetX Duo.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 45f35f2c1bec142e10d29eedb6e5a88a8eb74771e5d4adf1d85b04a87ad59ab7
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796209"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-http"></a>Capitolo 1 - Introduzione alla Azure RTOS HTTP di NetX Duo

Il Hypertext Transfer Protocol (HTTP) è un protocollo progettato per il trasferimento di contenuto sul Web. HTTP è un protocollo semplice che usa i servizi Reliable Transmission Control Protocol (TCP) per eseguire la funzione di trasferimento del contenuto. Per questo, HTTP è un protocollo di trasferimento del contenuto altamente affidabile. HTTP è uno dei protocolli applicativi più usati. Tutte le operazioni sul Web utilizzano il protocollo HTTP. Azure RTOS NETX Duo HTTP supporta sia le reti IPv4 che le reti IPv6. IPv6 non modifica direttamente il protocollo HTTP, anche se alcune modifiche nell'API HTTP NetX Azure RTOS originale sono necessarie per supportare IPv6 e verranno descritte in questo documento.

## <a name="http-requirements"></a>Requisiti HTTP

Per funzionare correttamente, il pacchetto HTTP NetX Duo richiede l'installazione di NetX Duo (versione 5.2 o successiva). Inoltre, è necessario che sia già stata creata un'istanza IP e che TCP sia abilitato nella stessa istanza IP. Un'applicazione host IPv6 deve impostare l'indirizzo IPv6 locale e globale del collegamento usando l'API IPv6 e/o DHCPv6. Il file demo nella sezione "Small Example System" del **capitolo 2** illustra come eseguire questa operazione.

La parte client HTTP del pacchetto HTTP NetX Duo non ha altri requisiti.

La parte server HTTP del pacchetto HTTP NetX Duo presenta diversi requisiti aggiuntivi. In primo luogo, è necessario l'accesso completo alla porta TCP nota 80 per la gestione di tutte le richieste HTTP client. Il server HTTP è progettato anche per l'uso con i file incorporati file system. Se FileX non è disponibile, l'utente può convertire le parti di FileX usate nel proprio ambiente. Questo argomento verrà illustrato nelle sezioni successive di questa guida.

## <a name="http-constraints"></a>Vincoli HTTP

Il protocollo HTTP di NetX Duo implementa lo standard HTTP 1.0. Esistono tuttavia i vincoli seguenti:

1.  Le connessioni permanenti non sono supportate
2.  Il pipelining delle richieste non è supportato
3.  Il server HTTP supporta sia l'autenticazione digest di base che l'autenticazione digest MD5, ma non l'autenticazione MD5. Al momento, il client HTTP supporta solo l'autenticazione di base.
4.  Non è supportata alcuna compressione del contenuto.
5.  Le richieste TRACE, OPTIONS e CONNECT non sono supportate.
6.  Il pool di pacchetti associato al server o al client HTTP deve essere sufficientemente grande da contenere l'intestazione HTTP completa.
7.  I servizi client HTTP sono solo per il trasferimento del contenuto. In questo pacchetto non sono disponibili utilità di visualizzazione.

## <a name="http-url-resource-names"></a>URL HTTP (nomi di risorse)

Il protocollo HTTP è progettato per trasferire il contenuto sul Web. Il contenuto richiesto viene specificato dall'URL (Universal Resource Locator). Questo è il componente principale di ogni richiesta HTTP. Gli URL iniziano sempre con *un carattere "/"* e in genere corrispondono ai file nel server HTTP. Di seguito sono riportate le estensioni di file HTTP comuni:

| Estensione | Significato |
| --------- | ------- |
| .htm (o .html) | Hypertext Markup Language (HTML) |
| .txt | Testo ASCII normale |
| gif | Immagine GIF binaria |
| .xbm | Immagine Xbitmap binaria |

## <a name="http-client-requests"></a>Richieste client HTTP

HTTP dispone di un meccanismo semplice per la richiesta di contenuto Web. Esiste fondamentalmente un set di comandi HTTP standard emessi dal client dopo che una connessione è stata stabilita correttamente sulla porta TCP *nota 80.* Di seguito sono illustrati alcuni dei comandi HTTP di base:

| Comando HTTP | Significato |
| ------------ | ------- |
| GET resource HTTP/1.0 | *Ottenere la risorsa specificata* |
| RISORSA POST HTTP/1.0 | *Ottenere la risorsa specificata e passare l'input associato alla funzione HTTP* |
| RISORSA HEAD HTTP/1.0 | *Considerato come GET, ma non il contenuto viene restituito dal server HTTP* |
| PUT resource HTTP/1.0 | *Inserire la risorsa nel server HTTP* |
| DELETE resource HTTP/1.0 | *Eliminare una risorsa nel server* |

Questi comandi ASCII vengono generati internamente dai Web browser e dai servizi client HTTP NetX per eseguire operazioni HTTP con un server HTTP.

> [!NOTE]
> Per impostazione predefinita, l'applicazione client HTTP ha la porta di connessione 80. Tuttavia, può modificare la porta di connessione al server HTTP in fase di esecuzione usando il nx_http_client_set_connect_port servizio. Per altri dettagli su questo servizio, vedere il capitolo 4. Questo consente di gestire i server Web che usano occasionalmente porte alternative per le connessioni client.

## <a name="http-server-responses"></a>Risposte del server HTTP

Il server HTTP usa la stessa *porta TCP 80* nota per inviare risposte ai comandi client. Dopo l'elaborazione del comando Client, il server HTTP restituisce una stringa di risposta ASCII che include un codice di stato numerico a 3 cifre. La risposta numerica viene usata dal software client HTTP per determinare se l'operazione ha avuto esito positivo o negativo. Di seguito è riportato un elenco di varie risposte del server HTTP ai comandi client:

| Campo numerico | Significato |
| ------------- | ------- |
| *200* | *La richiesta ha avuto esito positivo.* |
| *400* |   *La richiesta non è stata formata correttamente* |
| *401* | *Richiesta non autorizzata, il client deve inviare l'autenticazione* |
| *404* | *La risorsa specificata nella richiesta non è stata trovata* |
| *500* | *Errore interno del server HTTP* |
| *501* | *Richiesta non implementata dal server HTTP* |
| *502* | *Il servizio non è disponibile* |

Ad esempio, una richiesta client riuscita di PUT per il file "test.htm" viene risposta con il messaggio "HTTP/1.0 200 OK".

## <a name="http-communication"></a>Comunicazione HTTP

Come accennato in precedenza, il server HTTP usa la porta TCP 80 nota per il campo Richieste client. I client HTTP possono usare qualsiasi porta TCP disponibile. La sequenza generale di eventi HTTP è la seguente:

### <a name="http-get-request"></a>Richiesta HTTP GET:

1.  Il client esegue la connessione TCP alla porta 80 del server.
2.  Il client invia la **richiesta "GET resource HTTP/1.0"**(insieme ad altre informazioni sull'intestazione).
3.  Il server compila un messaggio "**HTTP/1.0 200 OK**" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa (se presente).
4.  Il server esegue una disconnessione.
5.  Il client esegue una disconnessione.

### <a name="http-put-request"></a>Richiesta HTTP PUT:

1.  Il client esegue la connessione TCP alla porta 80 del server.
2.  Il client invia **la richiesta "PUT resource HTTP/1.0"** insieme ad altre informazioni sull'intestazione e seguita dal contenuto della risorsa.
3.  Il server compila un messaggio "**HTTP/1.0 200 OK**" con informazioni aggiuntive seguite immediatamente dal contenuto della risorsa.
4.  Il server esegue una disconnessione.
5.  Il client esegue una disconnessione.

> [!NOTE]
>Come accennato in precedenza, il client HTTP può modificare la porta di connessione predefinita da 80 a un'altra porta usando *il nx_http_client_set_connect_port* per i server Web che usano porte alternative per la connessione ai client.

## <a name="http-authentication"></a>Autenticazione HTTP

L'autenticazione HTTP è facoltativa e non è necessaria per tutte le richieste Web. Esistono due tipi di autenticazione, in particolare di base e digest. L'autenticazione di base equivale all'autenticazione del nome e della password presente in molti protocolli. Nell'autenticazione di base HTTP il nome e le password vengono concatenati e codificati nel formato Base64. Lo svantaggio principale dell'autenticazione di base è che il nome e la password vengono trasmessi apertamente nella richiesta. In questo modo il nome e la password possono essere rubati con facilità. L'autenticazione digest risolve questo problema non trasmettendo mai il nome e la password nella richiesta. Viene invece usato un algoritmo per derivare una chiave o un digest a 128 bit dal nome, dalla password e da altre informazioni. Il server HTTP NetX supporta l'algoritmo digest MD5 standard.

Quando è necessaria l'autenticazione? In pratica, il server HTTP decide se una risorsa richiesta richiede l'autenticazione. Se è necessaria l'autenticazione e la richiesta client non includeva l'autenticazione appropriata, al client viene inviata una risposta "HTTP/1.0 401 Unauthorized" con il tipo di autenticazione richiesto. Si prevede quindi che il client formi una nuova richiesta con l'autenticazione appropriata.

## <a name="http-authentication-callback"></a>Callback di autenticazione HTTP

Come accennato in precedenza, l'autenticazione HTTP è facoltativa e non è necessaria in tutti i trasferimenti Web. Inoltre, l'autenticazione dipende in genere dalle risorse. L'accesso ad alcune risorse nel server richiede l'autenticazione, mentre altre no. Il pacchetto server HTTP NetX consente all'applicazione di specificare (tramite la chiamata *nx_http_server_create)* una routine di callback di autenticazione che viene chiamata all'inizio della gestione di ogni richiesta client HTTP.

La routine di callback fornisce al server HTTP NetX le stringhe nome utente, password e area di autenticazione associate alla risorsa e restituisce il tipo di autenticazione necessario. Se non è necessaria alcuna autenticazione per la risorsa, il callback di autenticazione deve restituire il valore **di NX_HTTP_DONT_AUTHENTICATE**. In caso contrario, se è necessaria l'autenticazione di base per la risorsa specificata, la routine deve restituire **NX_HTTP_BASIC_AUTHENTICATE**. Infine, se è necessaria l'autenticazione del digest MD5, la routine di callback deve restituire **NX_HTTP_DIGEST_AUTHENTICATE**. Se non è necessaria alcuna autenticazione per qualsiasi risorsa fornita dal server HTTP, il callback non è necessario ed è possibile specificare un puntatore NULL alla chiamata di creazione del server HTTP.

Il formato della routine di callback di autenticazione dell'applicazione è molto semplice ed è definito di seguito:

```c
UINT nx_http_server_authentication_check(NX_HTTP_SERVER *server_ptr,
                                          UINT request_type, CHAR *resource,
                                          CHAR **name, CHAR **password,
                                          CHAR **realm);
```
I parametri di input sono definiti come segue:

| Parametro | Significato |
| --------- | --------|
| *request_type* | Specifica la richiesta del client HTTP. Le richieste valide sono definite come segue: <br/> **NX_HTTP_SERVER_GET_REQUEST**<br/>**NX_HTTP_SERVER_POST_REQUEST**<br/>**NX_HTTP_SERVER_HEAD_REQUEST**<br/>**NX_HTTP_SERVER_PUT_REQUEST**<br/>**NX_HTTP_SERVER_DELETE_REQUEST** |
| *Risorsa* | Risorsa specifica richiesta. |
| *nome* | Destinazione per il puntatore al nome utente richiesto. |
| *password* | Destinazione per il puntatore alla password richiesta. |
| *Regno* | Destinazione per il puntatore all'area di autenticazione per questa autenticazione. |

Il valore restituito della routine di autenticazione specifica se è necessaria l'autenticazione. ```name, password, and realm``` I puntatori non vengono usati se **NX_HTTP_DONT_AUTHENTICATE** viene restituito dalla routine di callback di autenticazione. In caso contrario, lo  sviluppatore del server HTTP deve assicurarsi che le NX_HTTP_MAX_USERNAME e **NX_HTTP_MAX_PASSWORD** definite in *nxd_http_server.h* siano sufficientemente grandi per il nome utente e la password specificati nel callback di autenticazione. Per impostazione predefinita, entrambe sono di dimensioni di 20 caratteri.

## <a name="http-invalid-usernamepassword-callback"></a>Callback http nome utente/password non valido

Il callback facoltativo di nome utente/password non valido nel server HTTP NetX viene richiamato se il server HTTP riceve una combinazione di nome utente e password non valida in una richiesta client. Se l'applicazione server HTTP registra un callback con il server HTTP, verrà richiamata se l'autenticazione di base o digest non riesce *in nx_http_server_get_process*, *in nx_http_server_put_process* o in *nx_http_server_delete_process*.

Per registrare un callback con il server HTTP, in NetX Duo HTTP Server è definito il servizio seguente.

```c
UINT nx_http_server_invalid_userpassword_notify_set(
                   NX_HTTP_SERVER *http_server_ptr,
                   UINT *invalid_username_password_callback)
                            (CHAR *resource,
                             NXD_ADDRESS *client_nxd_address,
                             UINT request_type))
```

I tipi di richiesta sono definiti come segue:
 - **NX_HTTP_SERVER_GET_REQUEST**
 - **NX_HTTP_SERVER_POST_REQUEST**
 - **NX_HTTP_SERVER_HEAD_REQUEST**
 - **NX_HTTP_SERVER_PUT_REQUEST**
 - **NX_HTTP_SERVER_DELETE_REQUEST**

## <a name="http-insert-gmt-date-header-callback"></a>HTTP Insert GMT Date Header Callback

È disponibile un callback facoltativo nel server HTTP NetX Duo per inserire un'intestazione di data nei messaggi di risposta. Questo callback viene richiamato quando il server HTTP risponde a una richiesta put o get

È disponibile un callback facoltativo nel server HTTP NetX Duo per inserire un'intestazione di data nei messaggi di risposta. Questo callback viene richiamato quando il server HTTP risponde a una richiesta put o get

Per registrare un callback di data GMT con il server HTTP, nel server HTTP NetX Duo è definito il servizio seguente.

```c
UINT  _nx_http_server_gmt_callback_set(
                    NX_HTTP_SERVER *server_ptr,
                    VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date)
```

Il NX_HTTP_SERVER_DATE di dati è definito come segue:

```c
typedef struct NX_HTTP_SERVER_DATE_STRUCT
{
    USHORT          nx_http_server_year;           /* Year                 */
    UCHAR           nx_http_server_month;          /* Month                */
    UCHAR           nx_http_server_day;            /* Day                  */
    UCHAR           nx_http_server_hour;           /* Hour              */
    UCHAR           nx_http_server_minute;         /* Minute               */
    UCHAR           nx_http_server_second;         /* Second               */
    UCHAR           nx_http_server_weekday;        /* Weekday              */
} NX_HTTP_SERVER_DATE;
```

## <a name="http-cache-info-get-callback"></a>Callback Get delle informazioni sulla cache HTTP

Il server HTTP ha un callback per richiedere la validità massima e la data dall'applicazione HTTP per una risorsa specifica. Queste informazioni vengono usate per determinare se il server HTTP invia l'intera pagina in risposta a una richiesta Client Get. Se il valore "if modified since" nella richiesta Client non viene trovato o non corrisponde alla data dell'ultima modifica restituita dal callback get cache, viene inviata l'intera pagina.

Per registrare il callback con il server HTTP, viene definito il servizio seguente:

```c
UINT  _nx_http_server_cache_info_callback_set(
                              NX_HTTP_SERVER *server_ptr,
                              UINT (*cache_info_get)
                                    (CHAR *, UINT *, NX_HTTP_SERVER_DATE *))
```

## <a name="http-multipart-support"></a>Supporto multipart HTTP

Multipurpose Internet Mail Extensions (MIME) era originariamente destinato al protocollo SMTP, ma il suo utilizzo è stato distribuito in HTTP. MIME consente ai messaggi di contenere tipi misti di messaggi (ad esempio image/jpg e text/plain) all'interno dello stesso messaggio. NetX Duo HTTP Server ha aggiunto servizi per determinare il tipo di contenuto nei messaggi HTTP contenenti MIME dal client. Per abilitare il supporto multipart HTTP e usare questi servizi, è necessario **NX_HTTP_MULTIPART_ENABLE** l'opzione di configurazione .

```c
UINT  nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_pptr,
                                       UCHAR *entity_header_buffer,
                                       ULONG buffer_size);

UINT  nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET **packet_pptr,
                                        ULONG *available_offset,
                                        ULONG *available_length)
```

Per altre informazioni sull'uso di questi servizi, vedere la relativa descrizione nel capitolo 3 "Descrizione dei servizi HTTP".

## <a name="http-multi-thread-support"></a>Supporto multi-thread HTTP

I servizi client HTTP NetX possono essere chiamati contemporaneamente da più thread. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client HTTP devono essere eseguite in sequenza dallo stesso thread.

## <a name="http-rfcs"></a>RFC HTTP

NetX HTTP è conforme a RFC1945 "Hypertext Transfer Protocol/1.0, RFC 2581 "TCP Congestion Control", RFC 1122 "Requirements for Internet Hosts" (Requisiti per gli host Internet) e RFC correlate.
