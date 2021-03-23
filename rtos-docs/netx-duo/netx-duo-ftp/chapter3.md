---
title: Capitolo 3-Descrizione dei servizi FTP
description: Questo capitolo contiene una descrizione di tutti i servizi FTP NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d721d8bd3e08d8cccdc13011807b4c5017c84173
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821884"
---
# <a name="chapter-3---description-of-ftp-services"></a>Capitolo 3-Descrizione dei servizi FTP

Questo capitolo contiene una descrizione di tutti i servizi FTP NetX (elencati di seguito) in ordine alfabetico, ad eccezione del caso in cui gli equivalenti IPv4 e IPv6 dello stesso servizio siano abbinati.

> [!NOTE]
> Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="nx_ftp_client_connect"></a>nx_ftp_client_connect

Connettersi a un server FTP tramite IPv4

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG server_ip, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio connette l'istanza del client FTP NetX creata in precedenza al server FTP all'indirizzo IP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **server_ip** Indirizzo IP del server FTP.
- **nome utente** Nome utente del client per l'autenticazione.
- **password** di Password client per l'autenticazione.
- **WAIT_OPTION** Definisce il tempo di attesa del servizio per la connessione client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) connessione FTP riuscita.
- **NX_TFTP_EXPECTED_22X_CODE** (0xDB) non ha ricevuto una risposta 22x (OK)
- **NX_FTP_EXPECTED_23X_CODE** (0xdc) non ha ricevuto una risposta 23x (OK)
- **NX_FTP_EXPECTED_33X_CODE** (0xDE) non ha ricevuto una risposta 33x (OK)
- Il client **NX_FTP_NOT_DISCONNECTED** (0xd4) è già connesso.
- L'input del puntatore NX_PTR_ERROR (0x07) non è valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.
- NX_IP_ADDRESS_ERROR (0x21) indirizzo IP non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect the FTP Client instance “my_client” to the FTP Server at

IP address 1.2.3.4. */

status = nx_ftp_client_connect(&my_client, IP_ADDRESS(1,2,3,4), NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
    connected to the FTP Server. */
```

### <a name="see-also"></a>Vedere anche

nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nxd_ftp_client_connect

## <a name="nxd_ftp_client_connect"></a>nxd_ftp_client_connect

Connettersi a un server FTP con supporto IPv6

### <a name="prototype"></a>Prototipo

```C
UINT nxd_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    NXD_ADDRESS *server_ipduo, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio connette l'istanza del client FTP NetX Duo creata in precedenza al server FTP all'indirizzo IP specificato. Sono supportate sia reti IPv4 che IPv6.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **server_ipduo** Indirizzo IP del server FTP.
- **nome utente** Nome utente del client per l'autenticazione.
- **password** di Password client per l'autenticazione.
- **WAIT_OPTION** Definisce il tempo di attesa del servizio per la connessione client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) connessione FTP riuscita.
- **NX_TFTP_EXPECTED_22X_CODE** (0xDB) non ha ricevuto una risposta 22x (OK)
- **NX_FTP_EXPECTED_23X_CODE** (0xdc) non ha ricevuto una risposta 23x (OK)
- **NX_FTP_EXPECTED_33X_CODE** (0xDE) non ha ricevuto una risposta 33x (OK)
- Il client **NX_FTP_NOT_DISCONNECTED** (0xd4) è già connesso
- NX_PTR_ERROR (0x07) puntatore non valido InOut.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.
- NX_IP_ADDRESS_ERROR (0x21) indirizzo IP non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Connect an FTP Client instance to the FTP Server. */

/* Set up an IPv6 address for the server here.
    Note this could also be an IPv4 address as well*/

server_ip_addr.nxd_ip_address.v6[3] = 0x106;
server_ip_addr.nxd_ip_address.v6[2] = 0x0;
server_ip_addr.nxd_ip_address.v6[1] = 0x0000f101;
server_ip_addr.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V6;

status = nxd_ftp_client_connect(&my_client, server_ip_addr, NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
    connected to the FTP Server. */
```

### <a name="see-also"></a>Vedere anche

nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nx_ftp_client_connect

## <a name="nx_ftp_client_create"></a>nx_ftp_client_create

Creare un'istanza del client FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **ftp_client_name** Nome del client FTP.
- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **window_size** Dimensioni della finestra annunciata per i socket TCP del client FTP.
- **pool_ptr** Puntatore al pool di pacchetti predefinito per il client FTP. Si noti che il payload del pacchetto minimo deve essere sufficientemente grande da contenere il percorso completo e il nome del file o della directory.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) creazione client FTP riuscita.
- L'input del puntatore NX_PTR_ERROR (0x07) non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```C
/* Create the FTP Client instance “my_client.” */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
    2000, &client_pool);
/* If status is NX_SUCCESS the FTP Client instance was successfully created. */
```

## <a name="nx_ftp_client_delete"></a>nx_ftp_client_delete

Eliminare un'istanza del client FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del client FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) eliminazione client FTP riuscita.
- Client FTP **NX_FTP_NOT_DISCONNECTED** (0xd4) non disconnesso
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the FTP Client instance “my_client.” */

status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a>nx_ftp_client_directory_create

Creare una directory nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio crea la directory specificata nel server FTP connesso al client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **DIRECTORY_NAME** Nome della directory da creare.
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della creazione della directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione directory FTP riuscita.
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Create the directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_create(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” was successfully created. */
```

## <a name="nx_ftp_client_directory_default_set"></a>nx_ftp_client_directory_default_set

Imposta la directory predefinita nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la directory predefinita sul server FTP connesso al client FTP specificato. Questa directory predefinita si applica solo alla connessione del client.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **directory_path** Nome del percorso della directory da impostare.
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del set di directory predefinito FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) impostazione predefinita FTP riuscita.
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the default directory to “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_default_set(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a>nx_ftp_client_directory_delete

Elimina directory nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina la directory specificata nel server FTP connesso al client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **DIRECTORY_NAME** Nome della directory da eliminare.
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'eliminazione della directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) eliminazione directory FTP riuscita.
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_delete(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a>nx_ftp_client_directory_listing_get

Ottenere l'elenco di directory dal server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene il contenuto della directory specificata nel server FTP connesso al client FTP specificato. Il puntatore al pacchetto fornito conterrà una o più voci di directory. Ogni voce è separata da una \<cr/lf\> combinazione. Per completare l'operazione di Get della directory è necessario chiamare il ***nx_ftp_client_directory_listing_continue*** .

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **DIRECTORY_NAME** Nome della directory da cui ottenere il contenuto.
- **packet_ptr** Puntatore al puntatore del pacchetto di destinazione. In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory.
- **WAIT_OPTION** Definisce il tempo di attesa del servizio per la visualizzazione della directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- Elenco di directory FTP riuscite **NX_SUCCESS** (0x00).
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- Servizio **NX_NOT_ENABLED** (0x14) (IPv6) non abilitato
- **NX_FTP_EXPECTED_1XX_CODE** (0xD9) non ha ricevuto una risposta 1xx (OK)
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Get the contents of directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_listing_get(&my_client, “my_dir”, &my_packet,
    200);

/* If status is NX_SUCCESS, one or more entries of the directory “my_dir”
    can be found in “my_packet”. */
```

## <a name="nx_ftp_client_directory_listing_continue"></a>nx_ftp_client_directory_listing_continue

Continua Inserzione directory dal server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio continua a ottenere il contenuto della directory specificata nel server FTP connesso al client FTP specificato. Dovrebbe essere stato immediatamente preceduto da una chiamata a ***nx_ftp_client_directory_listing_get***. In caso di esito positivo, il puntatore al pacchetto fornito conterrà una o più voci di directory. Questa routine deve essere chiamata fino a quando non viene ricevuto uno stato di NX_FTP_END_OF_LISTING.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **packet_ptr** Puntatore al puntatore del pacchetto di destinazione. In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory, separate da un> di <CR/LF.
- **WAIT_OPTION** Definisce il tempo di attesa del servizio per la visualizzazione della directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- Elenco di directory FTP riuscite **NX_SUCCESS** (0x00).
- **NX_FTP_END_OF_LISTING** (0XD8) non sono presenti altre voci in questa directory.
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Continue getting the contents of directory “my_dir” on the FTP Server
    connected to the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_listing_continue(&my_client, &my_packet,
    200);

/* If status is NX_SUCCESS, one or more entries of the directory “my_dir”
    can be found in “my_packet”. */
```

## <a name="nx_ftp_client_disconnect"></a>nx_ftp_client_disconnect

Disconnetti dal server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio disconnette una connessione al server FTP stabilita in precedenza con il client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **WAIT_OPTION** Definisce per quanto tempo il servizio attenderà la disconnessione del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- Disconnessione FTP **NX_SUCCESS** (0x00) riuscita.
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Disconnect “my_client” from the FTP Server. */

status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, “my_client” has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a>nx_ftp_client_file_close

Chiudi file client

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio chiude un file aperto in precedenza nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della chiusura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- Chiusura del file FTP **NX_SUCCESS** (0x00) completata.
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- **NX_FTP_NOT_OPEN (0xD5)** Il file non è aperto; impossibile chiuderla
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Close previously opened file of client “my_client” on the FTP Server. */

status = nx_ftp_client_file_close(&my_client, 200);

/* If status is NX_SUCCESS, the file opened previously in the “my_client” FTP
    connection has been closed. */
```

## <a name="nx_ftp_client_file_delete"></a>nx_ftp_client_file_delete

Elimina file nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina il file specificato sul server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **file_name** Nome del file da eliminare.
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'eliminazione del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- Eliminazione file FTP riuscita **NX_SUCCESS** (0x00).
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the file “my_file.txt” on the FTP Server using the previously
    connected client “my_client.” */

status = nx_ftp_client_file_delete(&my_client, “my_file.txt”, 200);

/* If status is NX_SUCCESS, the file “my_file.txt” on the FTP Server is
    deleted. */
```

## <a name="nx_ftp_client_file_open"></a>nx_ftp_client_file_open

Apre il file nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_open(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, UINT open_type, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio apre il file specificato, per la lettura o la scrittura, sul server FTP precedentemente connesso all'istanza client specificata.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **file_name** Nome del file da aprire.
- **open_type** **NX_FTP_OPEN_FOR_READ** o **NX_FTP_OPEN_FOR_WRITE**.
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'apertura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- Apertura del file FTP **NX_SUCCESS** (0x00) completata.
- Il tipo aperto **NX_OPTION_ERROR** (0X0A) non è valido.
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- Il client FTP **NX_FTP_NOT_CLOSED** (0xD6) è già aperto.
- **NX_NO_FREE_PORTS** (0X45) non sono disponibili porte TCP da assegnare
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Open the file “my_file.txt” for reading on the FTP Server using the previously
    connected client “my_client.” */

status = nx_ftp_client_file_open(&my_client, “my_file.txt”, NX_FTP_OPEN_FOR_READ,
    200);

/* If status is NX_SUCCESS, the file “my_file.txt” on the FTP Server is
    open for reading. */
```

## <a name="nx_ftp_client_file_read"></a>nx_ftp_client_file_read

Lettura da file

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_read(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio legge un pacchetto da un file aperto in precedenza. Deve essere chiamato ripetutamente fino a quando non viene ricevuto uno stato di NX_FTP_END_OF_FILE.

Si noti che il chiamante non alloca un pacchetto per questo servizio.  È necessario fornire solo un puntatore a un puntatore di pacchetto. Questo servizio aggiornerà il puntatore del pacchetto in modo che punti a un pacchetto recuperato dalla coda di ricezione del socket.  Se viene restituito uno stato di esito positivo, significa che è disponibile un pacchetto ed è responsabilità del chiamante rilasciare il pacchetto quando viene eseguito.

Se viene restituito uno stato diverso da zero (stato di errore o NX_FTP_END_OF_FILE), il chiamante non rilascia il pacchetto. In caso contrario, viene generato un errore se il puntatore del pacchetto è NULL.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **packet_ptr** Puntatore alla destinazione per il puntatore del pacchetto di dati da archiviare. Se l'operazione ha esito positivo, il pacchetto parte o tutto il contenuto del file.
- **WAIT_OPTION** Definisce per quanto tempo il servizio attenderà la lettura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- Lettura del file FTP **NX_SUCCESS** (0x00) completata.
- Il client FTP **NX_FTP_NOT_OPEN** (0xD5) non è aperto.
- **NX_FTP_END_OF_FILE** la condizione di fine del file (0xD7).
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
NX_PACKET   *my_packet;

/* Read a packet of data from the file “my_file.txt” that was previously opened
    from the client “my_client.” */

status = nx_ftp_client_file_read(&my_client, &my_packet, 200);

/* Check status.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else
{
    /* Release packet when done with it. */
    nx_packet_release(my_packet);
}

/* If status is NX_SUCCESS, the packet pointer, “my_packet” points to the packet
    that contains the next bytes from the file. If the file is completely
    downloaded, an NX_FTP_END_OF_FILE status is returned (no packet retrieved). */
```

## <a name="nx_ftp_client_file_rename"></a>nx_ftp_client_file_rename

Rinomina file nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
    CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio Rinomina un file nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **nome file** Nome corrente del file.
- **new_filename** Nuovo nome per il file.
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della ridenominazione del file client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ridenominazione del file FTP riuscita.
- Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.
- **NX_FTP_EXPECTED_3XX_CODE** (0XDD) non ha ricevuto la risposta 3xx (OK)
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Rename file “my_file.txt” to “new_file.txt” on the previously connected
    Client instance “my_client.” */

status = nx_ftp_client_file_rename(&my_client, “my_file.txt”, “new_file.txt”,
    200);

/* If status is NX_SUCCESS, the file has been renamed. */
```

## <a name="nx_ftp_client_file_write"></a>nx_ftp_client_file_write

Scrivi nel file

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio scrive un pacchetto di dati nel file precedentemente aperto sul server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **packet_ptr** Puntatore di pacchetto contenente i dati da scrivere.
- **WAIT_OPTION** Definisce il tempo di attesa del servizio per la scrittura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) scrittura del file FTP riuscita.
- Il client FTP **NX_FTP_NOT_OPEN** (0xD5) non è aperto.
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Write the data contained in “my_packet” to the previously opened file
    “my_file.txt”. */

status = nx_ftp_client_file_write(&my_client, my_packet, 200);

/* If status is NX_SUCCESS, the file has been written to. */
```

## <a name="nx_ftp_client_passive_mode_set"></a>nx_ftp_client_passive_mode_set

Abilitare o disabilitare la modalità di trasferimento passivo

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_passive_mode_set(NX_FTP_CLIENT *ftp_client_ptr,
    UINT passive_mode_enabled);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita la modalità di trasferimento passivo se l'input passive_mode_enabled è impostato su NX_TRUE su un'istanza del client FTP creata in precedenza in modo che le chiamate successive ai file di lettura o scrittura (RETR, STOR) o scaricano un elenco di directory (NLST) vengano eseguite in modalità di trasferimento. Per disabilitare il trasferimento in modalità passiva e tornare al comportamento predefinito della modalità di trasferimento attivo, chiamare questa funzione con il passive_mode_enabled input impostato su NX_FALSE.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **passive_mode_enabled** Se è impostato su NX_TRUE, viene abilitata la modalità passiva.<br />Se impostato su NX_FALSE, la modalità passiva è disabilitata.

### <a name="return-values"></a>Valori restituiti

- Impostazione della modalità passiva **NX_SUCCESS** (0x00) riuscita.
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a>nx_ftp_server_create

Crea server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
    CHAR *ftp_server_name, NX_IP *ip_ptr,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*ftp_login)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        ULONG client_ip_address,
        UINT client_port, CHAR *name, CHAR *password,
        CHAR *extra_info),
    UINT (*ftp_logout)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        ULONG client_ip_address, UINT client_port,
         CHAR *name, CHAR *password, CHAR *extra_info));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server FTP nell'istanza IP di NetX specificata e creata in precedenza. Si noti che è necessario avviare il server FTP con una chiamata a ***nx_ftp_server_start*** per avviare l'operazione.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.
- **ftp_server_name** Nome del server FTP.
- **ip_ptr** Puntatore all'istanza IP di NetX associata. Si noti che può essere presente un solo server FTP per un'istanza IP.
- **media_ptr** Puntatore all'istanza del supporto FileX associata.
- **stack_ptr** Puntatore alla memoria per l'area dello stack del thread del server FTP interno.
- **stack_size** Dimensioni dell'area dello stack specificata dal *stack_ptr*.
- **pool_ptr** Puntatore al pool di pacchetti NetX predefinito. Si noti che la dimensione del payload dei pacchetti nel pool deve essere sufficientemente grande da contenere il nome file o il percorso più grande.
- **ftp_login** Puntatore alla funzione di accesso dell'applicazione. Questa funzione fornisce il nome utente e la password del client che richiede una connessione e l'indirizzo client nel tipo di dati ULONG. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.
- **ftp_logout** Puntatore a funzione per la funzione di disconnessione dell'applicazione. Questa funzione fornisce il nome utente e la password del client che richiede una disconnessione e l'indirizzo client nel tipo di dati ULONG. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.

### <a name="return-values"></a>Valori restituiti

- Creazione del server FTP riuscita **NX_SUCCESS** (0x00).
- NX_PTR_ERROR (0x07) puntatore FTP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```C
/* Create the FTP Server “my_server” on the IP instance “ip_0” using the
    “ram_disk” media. */

status = nx_ftp_server_create(&my_server, “My Server Name”, &ip_0, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_login, my_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nxd_ftp_server_create"></a>nxd_ftp_server_create

Creazione di un server FTP con supporto IPv4 e IPv6

### <a name="prototype"></a>Prototipo

```C
UINT nxd_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
    CHAR *ftp_server_name, NX_IP *ip_ptr,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*ftp_login_duo)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        NXD_ADDRESS *client_ip_address, UINT client_port, CHAR *name,
        CHAR *password, CHAR *extra_info),
    UINT (*ftp_logout_duo)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        NXD_ADDRESS *client_ip_address, UINT client_port, CHAR *name,
        CHAR *password, CHAR *extra_info));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server FTP nell'istanza IP di NetX specificata e creata in precedenza. Si noti che è ancora necessario avviare il server FTP con una chiamata a ***nx_ftp_server_start*** per avviare l'operazione dopo la creazione del server.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.
- **ftp_server_name** Nome del server FTP.
- **ip_ptr** Puntatore all'istanza IP di NetX associata. Si noti che può essere presente un solo server FTP per un'istanza IP.
- **media_ptr** Puntatore all'istanza del supporto FileX associata.
- **stack_ptr** Puntatore alla memoria per l'area dello stack del thread del server FTP interno.
- **stack_size** Dimensioni dell'area dello stack specificata dal *stack_ptr*.
- **pool_ptr** Puntatore al pool di pacchetti NetX predefinito. Si noti che la dimensione del payload dei pacchetti nel pool deve essere sufficientemente grande da contenere il nome file o il percorso più grande.
- **ftp_login_duo** Puntatore alla funzione di accesso dell'applicazione. Questa funzione fornisce il nome utente e la password del client che richiede una connessione e un puntatore all'indirizzo client nel tipo di dati NXD_ADDRESS. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.
- **ftp_logout_duo** Puntatore a funzione per la funzione di disconnessione dell'applicazione. Questa funzione fornisce il nome utente e la password del client che richiede una disconnessione e un puntatore all'indirizzo client nel tipo di dati NXD_ADDRESS. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.

### <a name="return-values"></a>Valori restituiti

- Creazione del server FTP riuscita **NX_SUCCESS** (0x00).
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```C
/* Create the FTP Server “my_server” on the IP instance “ip_0” using the
    “ram_disk” media. */

status = nxd_ftp_server_create(&my_server, “My Server Name”, &ip_0, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_duo_login, my_duo_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nx_ftp_server_delete"></a>nx_ftp_server_delete

Elimina server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del server FTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- Eliminazione del server FTP riuscita **NX_SUCCESS** (0x00).
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the FTP Server “my_server”. */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a>nx_ftp_server_start

Avvia server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia un'istanza del server FTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- Avvio del server FTP **NX_SUCCESS** (0x00) riuscito.
- NX_PTR_ERROR (0x07) puntatore FTP non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start the FTP Server “my_server”. */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a>nx_ftp_server_stop

Arresta server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio interrompe un'istanza del server FTP creata e avviata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- L'arresto del server FTP **NX_SUCCESS** (0x00) è riuscito.
- NX_PTR_ERROR (0x07) puntatore FTP non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop the FTP Server “my_server”. */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
