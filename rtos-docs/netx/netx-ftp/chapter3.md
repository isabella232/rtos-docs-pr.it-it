---
title: Capitolo 3-Descrizione dei servizi FTP NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi FTP NetX di Azure RTO (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b05d03c45607c45acf32474cf8e40861532c5fae
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822625"
---
# <a name="chapter-3---description-of-azure-rtos-netx-ftp-services"></a>Capitolo 3-Descrizione dei servizi FTP NetX di Azure RTO

Questo capitolo contiene una descrizione di tutti i servizi FTP NetX di Azure RTO (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_ftp_client_connect**: *connettersi al server FTP*
- **nx_ftp_client_create**: *creare un'istanza del client FTP*
- **nx_ftp_client_delete**: *eliminare un'istanza del client FTP*
- **nx_ftp_client_directory_create**: *creare una directory nel server*
- **nx_ftp_client_directory_default_set**: *impostare la directory predefinita nel server*
- **nx_ftp_client_directory_delete**: *eliminare una directory nel server*
- **nx_ftp_client_directory_listing_get**: *ottenere un elenco di directory dal server*
- **nx_ftp_client_directory_listing_continue**: *continua la visualizzazione della directory dal server*
- **nx_ftp_client_disconnect**: *disconnettersi dal server FTP*
- **nx_ftp_client_file_close**: *chiudere il file client*
- **nx_ftp_client_file_delete**: *eliminare un file nel server*
- **nx_ftp_client_file_open**: *Apri file client*
- **nx_ftp_client_file_read**: *lettura da file*
- **nx_ftp_client_file_rename**: *rinominare il file nel server*
- **nx_ftp_client_file_write**: *scrittura nel file*
- **nx_ftp_server_create**: *creare un server FTP*
- **nx_ftp_server_delete**: *eliminare il server FTP*
- **nx_ftp_server_start**: *avviare il server FTP*
- **nx_ftp_server_stop**: *arrestare il server FTP*

## <a name="nx_ftp_client_connect"></a>nx_ftp_client_connect

Connettersi a un server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
        ULONG server_ip, CHAR *username, CHAR *password,
        ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio connette l'istanza del client FTP precedentemente creata al server FTP all'indirizzo IP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **server_ip**: indirizzo IP del server FTP.
- **username**: nome utente del client per l'autenticazione.
- **password**: password client per l'autenticazione.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la connessione client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) connessione FTP riuscita.
- **NX_TFTP_EXPECTED_22X_CODE**: (0xDB) non ha ricevuto una risposta 22x (OK)
- **NX_FTP_EXPECTED_23X_CODE**: (0xdc) non ha ricevuto una risposta 23x (OK)
- **NX_FTP_EXPECTED_33X_CODE**: (0xDE) non ha ricevuto una risposta 33x (OK)
- **NX_FTP_NOT_DISCONNECTED**: il client (0xd4) è già connesso.
- NX_PTR_ERROR: (0x07) puntatore non valido InOut.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.
- NX_IP_ADDRESS_ERROR: (0x21) indirizzo IP non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Connect the FTP Client instance "my_client" to the FTP Server at
    IP address 1.2.3.4. */
status = nx_ftp_client_connect(&my_client, IP_ADDRESS(1,2,3,4), NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
connected to the FTP Server. */
```

## <a name="nx_ftp_client_create"></a>nx_ftp_client_create

Creare un'istanza del client FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **ftp_client_name**: nome del client FTP.
- **ip_ptr**: puntatore all'istanza IP creata in precedenza.
- **window_size**: dimensioni della finestra annunciata per il socket TCP del client FTP.
- **pool_ptr**: puntatore al pool di pacchetti predefinito per il client FTP. Si noti che il payload del pacchetto minimo deve essere sufficientemente grande da contenere il percorso completo e il nome del file o della directory.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) creazione client FTP riuscita.
- NX_PTR_ERROR: (0x16) protocollo FTP, puntatore IP o puntatore al pool di pacchetti non valido. puntatore alla password.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Create the FTP Client instance "my_client." */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
                                2000, &client_pool);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
created. */
```

## <a name="nx_ftp_client_delete"></a>nx_ftp_client_delete

Eliminare un'istanza del client FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del client FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione client FTP riuscita.
- **NX_FTP_NOT_DISCONNECTED**: (0xd4) errore di eliminazione del client FTP.
- NX_PTR_ERROR: (0x16) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the FTP Client instance "my_client." */
status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a>nx_ftp_client_directory_create

Creare una directory nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio crea la directory specificata nel server FTP connesso al client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **DIRECTORY_NAME**: nome della directory da creare.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la creazione della directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la creazione della directory FTP è riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK) 
- NX_PTR_ERROR: (0x07) puntatore FTP non valido. 
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Create the directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_create(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" was successfully  
    created. */
```

## <a name="nx_ftp_client_directory_default_set"></a>nx_ftp_client_directory_default_set

Imposta la directory predefinita nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
                                CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la directory predefinita sul server FTP connesso al client FTP specificato. Questa directory predefinita si applica solo alla connessione del client.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **directory_path**: nome del percorso della directory da impostare.
- **WAIT_OPTION**: definisce per quanto tempo il servizio resterà in attesa del set di directory predefinito FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) il set predefinito di FTP è riuscito.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK) 
- NX_PTR_ERROR: (0x07) puntatore FTP non valido. 
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Set the default directory to "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_default_set(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a>nx_ftp_client_directory_delete

Elimina directory nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina la directory specificata nel server FTP connesso al client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **DIRECTORY_NAME**: nome della directory da eliminare.
- **WAIT_OPTION**: definisce per quanto tempo il servizio resterà in attesa dell'eliminazione della directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione directory FTP riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK) 
- NX_PTR_ERROR: (0x07) puntatore FTP non valido. 
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_delete(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a>nx_ftp_client_directory_listing_get

Ottenere l'elenco di directory dal server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
                            CHAR *directory_name, NX_PACKET **packet_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene il contenuto della directory specificata nel server FTP connesso al client FTP specificato. Il puntatore al pacchetto fornito conterrà una o più voci di directory. Ogni voce è separata da una &lt; combinazione CR/LF \. Per completare l'operazione di Get della directory è necessario chiamare il ***nx_ftp_client_directory_listing_continue***:.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **DIRECTORY_NAME**: nome della directory da cui ottenere il contenuto.
- **packet_ptr**: puntatore al puntatore del pacchetto di destinazione. In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per l'elenco di directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) elenco di directory FTP riuscite.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_NOT_ENABLED**: (0X14) servizio (IPv6) non abilitato
- **NX_FTP_EXPECTED_1XX_CODE**: (0xD9) non ha ricevuto una risposta 1xx (OK)
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Get the contents of directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_listing_get(&my_client, "my_dir", &my_packet,
                                            200);

/* If status is NX_SUCCESS, one or more entries of the directory "my_dir"
    can be found in "my_packet". */
```

## <a name="nx_ftp_client_directory_listing_continue"></a>nx_ftp_client_directory_listing_continue

Continua Inserzione directory dal server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT
                    *ftp_client_ptr, NX_PACKET **packet_ptr,
                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio continua a ottenere il contenuto della directory specificata nel server FTP connesso al client FTP specificato. Dovrebbe essere stato immediatamente preceduto da una chiamata a ***nx_ftp_client_directory_listing_get***. In caso di esito positivo, il puntatore al pacchetto fornito conterrà una o più voci di directory. Questa routine deve essere chiamata fino a quando non viene ricevuto uno stato di NX_FTP_END_OF_LISTING.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **packet_ptr**: puntatore al puntatore del pacchetto di destinazione. In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory, separate da &lt; CR/LF &gt; .
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per l'elenco di directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) elenco di directory FTP riuscite.
- **NX_FTP_END_OF_LISTING**: (0XD8) non sono presenti altre voci in questa directory.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Continue getting the contents of directory "my_dir" on the FTP Server
    connected to the FTP Client instance "my_client." */
status = nx_ftp_client_directory_listing_continue(&my_client, &my_packet,
                                                200);

/* If status is NX_SUCCESS, one or more entries of the directory "my_dir"
    can be found in "my_packet". */
```

## <a name="nx_ftp_client_disconnect"></a>nx_ftp_client_disconnect

Disconnetti dal server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio disconnette una connessione al server FTP stabilita in precedenza con il client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **WAIT_OPTION**: definisce per quanto tempo il servizio attenderà la disconnessione del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la DISconnessione FTP è riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Disconnect "my_client" from the FTP Server. */
status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, "my_client" has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a>nx_ftp_client_file_close

Chiudi file client

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio chiude un file aperto in precedenza nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la chiusura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) chiusura file FTP riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_NOT_OPEN (0xD5)**: file non aperto; impossibile chiuderla
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Close previously opened file of client "my_client" on the FTP Server. */
status = nx_ftp_client_file_close(&my_client, 200);

/* If status is NX_SUCCESS, the file opened previously in the "my_client" FTP
    connection has been closed. */
```

## <a name="nx_ftp_client_file_delete"></a>nx_ftp_client_file_delete

Elimina file nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina il file specificato sul server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **file_name**: nome del file da eliminare.
- **WAIT_OPTION**: definisce per quanto tempo il servizio resterà in attesa dell'eliminazione del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione file FTP riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the file "my_file.txt" on the FTP Server using the previously
    connected client "my_client." */
status = nx_ftp_client_file_delete(&my_client, "my_file.txt", 200);

/* If status is NX_SUCCESS, the file "my_file.txt" on the FTP Server is
    deleted. */
```

## <a name="nx_ftp_client_file_open"></a>nx_ftp_client_file_open

Apre il file nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_open(NX_FTP_CLIENT *ftp_client_ptr,
        CHAR *file_name, UINT open_type, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio apre il file specificato, per la lettura o la scrittura, sul server FTP precedentemente connesso all'istanza client specificata.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **file_name**: nome del file da aprire.
- **open_type**: **NX_FTP_OPEN_FOR_READ** o **NX_FTP_OPEN_FOR_WRITE**.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per l'apertura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'apertura del file FTP è riuscita.
- **NX_OPTION_ERROR**: (0x0A) tipo aperto non valido.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_NOT_CLOSED**: il client FTP (0xD6) è già aperto.
- **NX_NO_FREE_PORTS**: (0X45) non sono disponibili porte TCP da assegnare
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Open the file "my_file.txt" for reading on the FTP Server using the previously
    connected client "my_client." */
status = nx_ftp_client_file_open(&my_client, "my_file.txt", NX_FTP_OPEN_FOR_READ,
                                200);

/* If status is NX_SUCCESS, the file "my_file.txt" on the FTP Server is
    open for reading. */
```

## <a name="nx_ftp_client_file_read"></a>nx_ftp_client_file_read

Lettura da file

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_read(NX_FTP_CLIENT *ftp_client_ptr,
                NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio legge un pacchetto da un file aperto in precedenza. Deve essere chiamato ripetutamente fino a quando non viene ricevuto uno stato di NX_FTP_END_OF_FILE.

Si noti che il chiamante non alloca un pacchetto per questo servizio.  È necessario fornire solo un puntatore a un puntatore di pacchetto. Questo servizio aggiornerà il puntatore del pacchetto in modo che punti a un pacchetto recuperato dalla coda di ricezione del socket.  Se viene restituito uno stato di esito positivo, significa che è disponibile un pacchetto ed è responsabilità del chiamante rilasciare il pacchetto quando viene eseguito.

Se viene restituito uno stato diverso da zero (stato di errore o NX_FTP_END_OF_FILE), il chiamante non rilascia il pacchetto. In caso contrario, viene generato un errore se il puntatore del pacchetto è NULL.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **packet_ptr**: puntatore alla destinazione per il puntatore al pacchetto di dati recuperato dalla coda. In caso di esito positivo, i dati del pacchetto contengono parte o tutto il file.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la lettura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la lettura del file FTP è riuscita.
- **NX_FTP_NOT_OPEN**: il client FTP (0xD5) non è aperto.
- **NX_FTP_END_OF_FILE**: (0xD7) la condizione di fine del file.
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
       NX_PACKET   *my_packet;

/* Read a packet of data from the file "my_file.txt" that was previously opened
    from the client "my_client." */

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

/* If status is NX_SUCCESS, the packet pointer, "my_packet" points to the packet
that contains the next bytes from the file. If the file is completely
downloaded, an NX_FTP_END_OF_FILE status is returned (no packet retrieved). */
```

## <a name="nx_ftp_client_file_rename"></a>nx_ftp_client_file_rename

Rinomina file nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
                                CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio Rinomina un file nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **filename**: nome corrente del file.
- **new_filename**: nuovo nome per il file.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la ridenominazione del file client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la ridenominazione del file FTP è riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_3XX_CODE**: (0XDD) non ha ricevuto la risposta 3xx (OK)
- **NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Rename file "my_file.txt" to "new_file.txt" on the previously connected
    Client instance "my_client." */

status = nx_ftp_client_file_rename(&my_client, "my_file.txt", "new_file.txt",
                                    200);

/* If status is NX_SUCCESS, the file has been renamed. */
```

## <a name="nx_ftp_client_file_write"></a>nx_ftp_client_file_write

Scrivi nel file

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
                    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio scrive un pacchetto di dati nel file precedentemente aperto sul server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **packet_ptr**: puntatore al pacchetto contenente i dati da scrivere.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la scrittura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xfffffffe)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) scrittura del file FTP riuscita.
- **NX_FTP_NOT_OPEN**: il client FTP (0xD5) non è aperto.
- NX_PTR_ERROR: (0x07) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Write the data contained in "my_packet" to the previously opened file
    "my_file.txt". */

status = nx_ftp_client_file_write(&my_client, my_packet, 200);

/* If status is NX_SUCCESS, the file has been written to. */
```

## <a name="nx_ftp_client_passive_mode_set"></a>nx_ftp_client_passive_mode_set

Abilitare o disabilitare la modalità di trasferimento passivo

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_passive_mode_set(NX_FTP_CLIENT *ftp_client_ptr,
                                    UINT passive_mode_enabled);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita la modalità di trasferimento passivo se l'input passive_mode_enabled è impostato su NX_TRUE su un'istanza del client FTP creata in precedenza in modo che le chiamate successive ai file di lettura o scrittura (RETR, STOR) o scaricano un elenco di directory (NLST) vengano eseguite in modalità di trasferimento. Per disabilitare il trasferimento in modalità passiva e tornare al comportamento predefinito della modalità di trasferimento attivo, chiamare questa funzione con il passive_mode_enabled input impostato su NX_FALSE.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr**: puntatore al blocco di controllo client FTP.
- **passive_mode_enabled**:
  - Se è impostato su NX_TRUE, viene abilitata la modalità passiva.
  - Se impostato su NX_FALSE, la modalità passiva è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) impostato in modalità passiva riuscita.
- NX_PTR_ERROR: (0x16) puntatore FTP non valido.
- NX_INVALID_PARAMETERS: (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a>nx_ftp_server_create

Crea server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
        CHAR *ftp_server_name, NX_IP *ip_ptr,
        FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
        NX_PACKET_POOL *pool_ptr,
        UINT (*ftp_login)(struct NX_FTP_SERVER_STRUCT
                *ftp_server_ptr, ULONG client_ip_address,
                UINT client_port, CHAR *name, CHAR *password,
                CHAR *extra_info),
        UINT (*ftp_logout)(struct NX_FTP_SERVER_STRUCT
                *ftp_server_ptr, ULONG client_ip_address,
                UINT client_port, CHAR *name, CHAR *password,
                CHAR *extra_info));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server FTP nell'istanza IP di NetX specificata e creata in precedenza. Si noti che è necessario avviare il server FTP con una chiamata a ***nx_ftp_server_start*** per avviare l'operazione.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr**: puntatore al blocco di controllo del server FTP.
- **ftp_server_name**: nome del server FTP.
- **ip_ptr**: puntatore all'istanza IP NETX associata. Si noti che può essere presente un solo server FTP per un'istanza IP.
- **media_ptr**: puntatore all'istanza del supporto FILEX associata.
- **stack_ptr**: puntatore alla memoria per l'area dello stack del thread del server FTP interno.
- **stack_size**: dimensioni dell'area dello stack specificata da *stack_ptr*.
- **pool_ptr**: puntatore al pool di pacchetti NETX predefinito. Si noti che la dimensione del payload dei pacchetti nel pool deve essere sufficientemente grande da contenere il nome file o il percorso più grande.
- **ftp_login**: puntatore a funzione per la funzione di accesso dell'applicazione. Questa funzione fornisce il nome utente e la password del client che richiede una connessione. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.
- **ftp_logout**: puntatore a funzione per la funzione di disconnessione dell'applicazione. Questa funzione fornisce il nome utente e la password del client che richiede una disconnessione. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la creazione del server FTP è riuscita.
- NX_PTR_ERROR: (0x16) puntatore FTP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Create the FTP Server "my_server" on the IP instance "ip_0" using the
    "ram_disk" media. */

status = nx_ftp_server_create(&my_server, "My Server Name", &ip_0, &ram_disk,
                                stack_ptr, stack_size, &pool_0,
                                my_login, my_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nx_ftp_server_delete"></a>nx_ftp_server_delete

Elimina server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del server FTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr**: puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione del server FTP riuscita.
- NX_PTR_ERROR: (0x16) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the FTP Server "my_server". */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a>nx_ftp_server_start

Avvia server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia un'istanza del server FTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr**: puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) avvio del server FTP riuscito.
- NX_PTR_ERROR: (0x16) puntatore FTP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Start the FTP Server "my_server". */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a>nx_ftp_server_stop

Arresta server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio interrompe un'istanza del server FTP creata e avviata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr**: puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'arresto del server FTP è riuscito.
- NX_PTR_ERROR: (0x16) puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the FTP Server "my_server". */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
