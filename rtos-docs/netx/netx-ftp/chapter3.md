---
title: Capitolo 3 - Descrizione dei Azure RTOS FTP NetX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS FTP NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1aec01088236dcae359c0273a0206c10ea09201eb486478ebd678529413badae
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799456"
---
# <a name="chapter-3---description-of-azure-rtos-netx-ftp-services"></a>Capitolo 3 - Descrizione dei Azure RTOS FTP NetX

Questo capitolo contiene una descrizione di tutti i Azure RTOS FTP NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_ftp_client_connect**: *Connessione al server FTP*
- **nx_ftp_client_create**: *Creare un'istanza del client FTP*
- **nx_ftp_client_delete**: *Eliminare un'istanza del client FTP*
- **nx_ftp_client_directory_create**: *Creare una directory nel server*
- **nx_ftp_client_directory_default_set:** impostare *la directory predefinita nel server*
- **nx_ftp_client_directory_delete**: *Eliminare una directory nel server*
- **nx_ftp_client_directory_listing_get:** Ottenere *l'elenco di directory dal server*
- **nx_ftp_client_directory_listing_continue:** continuare *l'elenco di directory dal server*
- **nx_ftp_client_disconnect**: *Disconnettersi dal server FTP*
- **nx_ftp_client_file_close**: *Chiudere il file client*
- **nx_ftp_client_file_delete**: *Elimina file nel server*
- **nx_ftp_client_file_open**: *Aprire il file client*
- **nx_ftp_client_file_read**: *Lettura da file*
- **nx_ftp_client_file_rename**: *Rinominare il file nel server*
- **nx_ftp_client_file_write**: *Scrivere nel file*
- **nx_ftp_server_create**: *Creare un server FTP*
- **nx_ftp_server_delete**: *Elimina server FTP*
- **nx_ftp_server_start**: *Avviare il server FTP*
- **nx_ftp_server_stop**: *Arrestare il server FTP*

## <a name="nx_ftp_client_connect"></a>nx_ftp_client_connect

Connessione a un server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
        ULONG server_ip, CHAR *username, CHAR *password,
        ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio connette l'istanza del client FTP creata in precedenza al server FTP all'indirizzo IP fornito.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **server_ip**: indirizzo IP del server FTP.
- **username:** nome utente client per l'autenticazione.
- **password:** password client per l'autenticazione.
- **wait_option**: definisce per quanto tempo il servizio attenderà la connessione client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 attraverso 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un tempo indefinito fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Connessione FTP riuscita.
- **NX_TFTP_EXPECTED_22X_CODE:**(0xDB) Non è stata ricevuta una risposta 22X (ok)
- **NX_FTP_EXPECTED_23X_CODE**: (0xDC) Non è stata ricevuta una risposta 23X (ok)
- **NX_FTP_EXPECTED_33X_CODE:**(0xDE) Non è stata ricevuta una risposta 33X (ok)
- **NX_FTP_NOT_DISCONNECTED:**(0xD4) Il client è già connesso.
- NX_PTR_ERROR: (0x07) Inout puntatore non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.
- NX_IP_ADDRESS_ERROR: (0x21) Indirizzo IP non valido.

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

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **ftp_client_name**: nome del client FTP.
- **ip_ptr:** puntatore all'istanza IP creata in precedenza.
- **window_size:** dimensioni della finestra annunciate per il socket TCP di questo client FTP.
- **pool_ptr:** puntatore al pool di pacchetti predefinito per questo client FTP. Si noti che il payload minimo del pacchetto deve essere sufficientemente grande da contenere il percorso completo e il nome del file o della directory.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione del client FTP riuscita.
- NX_PTR_ERROR: (0x16) Ftp, puntatore IP o puntatore del pool di pacchetti non valido. puntatore password.

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

Questo servizio elimina un'istanza del client FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Eliminazione del client FTP riuscita.
- **NX_FTP_NOT_DISCONNECTED:**(0xD4) Errore di eliminazione del client FTP.
- NX_PTR_ERROR: (0x16) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **directory_name**: nome della directory da creare.
- **wait_option**: definisce per quanto tempo il servizio attenderà la creazione della directory FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 attraverso 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un tempo indefinito fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione della directory FTP riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) Non è stata ricevuta una risposta 2XX (ok) 
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido. 
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Impostare la directory predefinita nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
                                CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la directory predefinita nel server FTP connesso al client FTP specificato. Questa directory predefinita si applica solo alla connessione del client.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **directory_path**: nome del percorso della directory da impostare.
- **wait_option**: definisce per quanto tempo il servizio attenderà il set di directory predefinito FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 attraverso 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un tempo indefinito fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Impostazione predefinita FTP riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) Non è stata ricevuta una risposta 2XX (ok) 
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido. 
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Eliminare la directory nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio elimina la directory specificata nel server FTP connesso al client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **directory_name**: nome della directory da eliminare.
- **wait_option**: definisce per quanto tempo il servizio attenderà l'eliminazione della directory FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 attraverso 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un tempo indefinito fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Eliminazione della directory FTP riuscita.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) Non è stata ricevuta una risposta 2XX (ok) 
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido. 
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Ottenere un elenco di directory dal server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
                            CHAR *directory_name, NX_PACKET **packet_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene il contenuto della directory specificata nel server FTP connesso al client FTP specificato. Il puntatore di pacchetto fornito conterrà una o più voci di directory. Ogni voce è separata da una &lt; combinazione cr/lf\. Il ***nx_ftp_client_directory_listing_continue***: deve essere chiamato per completare l'operazione di lettura della directory.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **directory_name:** nome della directory di cui ottenere il contenuto.
- **packet_ptr:** puntatore al puntatore al pacchetto di destinazione. In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory.
- **wait_option**: definisce per quanto tempo il servizio attenderà l'elenco di directory FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 attraverso 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un tempo indefinito fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Elenco di directory FTP riuscito.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_NOT_ENABLED:** servizio (0x14) (IPv6) non abilitato
- **NX_FTP_EXPECTED_1XX_CODE:**(0xD9) Non è stata ricevuta una risposta 1XX (ok)
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Continuare l'elenco di directory dal server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT
                    *ftp_client_ptr, NX_PACKET **packet_ptr,
                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio continua a ottenere il contenuto della directory specificata nel server FTP connesso al client FTP specificato. Deve essere stato immediatamente preceduto da una chiamata a ***nx_ftp_client_directory_listing_get***. In caso di esito positivo, il puntatore di pacchetto fornito conterrà una o più voci di directory. Questa routine deve essere chiamata fino a quando non viene ricevuto NX_FTP_END_OF_LISTING stato del servizio.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **packet_ptr:** puntatore al puntatore al pacchetto di destinazione. In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory, separate da &lt; cr/lf &gt; .
- **wait_option**: definisce per quanto tempo il servizio attenderà l'elenco di directory FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 attraverso 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un tempo indefinito fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Elenco di directory FTP riuscito.
- **NX_FTP_END_OF_LISTING**: (0xD8) Non sono presenti altre voci in questa directory.
- **NX_FTP_NOT_CONNECTED:** il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

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

Disconnettersi dal server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio disconnette una connessione al server FTP stabilita in precedenza con il client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **wait_option**: definisce per quanto tempo il servizio attenderà la disconnessione del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Disconnessione FTP riuscita.
- **NX_FTP_NOT_CONNECTED:** il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Disconnect "my_client" from the FTP Server. */
status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, "my_client" has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a>nx_ftp_client_file_close

Chiudere il file client

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio chiude un file aperto in precedenza nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **wait_option**: definisce per quanto tempo il servizio attenderà la chiusura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Chiusura del file FTP completata.
- **NX_FTP_NOT_CONNECTED:** il client FTP (0xD3) non è connesso.
- **NX_FTP_NOT_OPEN (0xD5):** File non aperto; non può chiuderlo
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

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

Eliminare un file nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio elimina il file specificato nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **file_name**: nome del file da eliminare.
- **wait_option**: definisce per quanto tempo il servizio attenderà l'eliminazione del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Eliminazione del file FTP completata.
- **NX_FTP_NOT_CONNECTED:** il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

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

Questo servizio apre il file specificato, per la lettura o la scrittura, nel server FTP connesso in precedenza all'istanza client specificata.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **file_name**: nome del file da aprire.
- **open_type**: **NX_FTP_OPEN_FOR_READ** o **NX_FTP_OPEN_FOR_WRITE**.
- **wait_option**: definisce per quanto tempo il servizio attenderà l'apertura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout**: (0x00000001 tramite 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Apertura del file FTP riuscita.
- **NX_OPTION_ERROR**: (0x0A) Tipo aperto non valido.
- **NX_FTP_NOT_CONNECTED:** il client FTP (0xD3) non è connesso.
- **NX_FTP_NOT_CLOSED:**(0xD6) FTP Client è già aperto.
- **NX_NO_FREE_PORTS:**(0x45) Nessuna porta TCP disponibile per l'assegnazione
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

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

Questo servizio legge un pacchetto da un file aperto in precedenza. Deve essere chiamato in modo ripetitivo fino a quando non viene ricevuto NX_FTP_END_OF_FILE stato .

Si noti che il chiamante non alloca un pacchetto per questo servizio.  È necessario fornire solo un puntatore a un puntatore a pacchetto. Questo servizio aggiornerà il puntatore del pacchetto in modo che punti a un pacchetto recuperato dalla coda di ricezione del socket.  Se viene restituito uno stato riuscito, significa che è disponibile un pacchetto ed è responsabilità del chiamante rilasciare il pacchetto al termine dell'operazione.

Se viene restituito uno stato diverso da zero (stato di errore o NX_FTP_END_OF_FILE), il chiamante non rilascia il pacchetto. In caso contrario, viene generato un errore quando il puntatore del pacchetto è NULL.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **packet_ptr:** puntatore alla destinazione per il puntatore del pacchetto di dati recuperato dalla coda. In caso di esito positivo, i dati del pacchetto contengono parte o tutto il file.
- **wait_option**: definisce per quanto tempo il servizio attenderà la lettura del file del client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 a 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso a tempo indeterminato fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Lettura del file FTP completata.
- **NX_FTP_NOT_OPEN**: il client FTP (0xD5) non è aperto.
- **NX_FTP_END_OF_FILE**: (0xD7) Condizione di fine file.
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Rinominare il file nel server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
                                CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio rinomina un file nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **filename:** nome corrente del file.
- **new_filename:** nuovo nome per il file.
- **wait_option**: definisce per quanto tempo il servizio attenderà la ridenominazione del file del client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 a 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso a tempo indeterminato fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Ridenominazione del file FTP completata.
- **NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.
- **NX_FTP_EXPECTED_3XX_CODE:**(0XDD) Non ha ricevuto la risposta 3XX (ok)
- **NX_FTP_EXPECTED_2XX_CODE:**(0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Scrivere nel file

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
                    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio scrive un pacchetto di dati nel file aperto in precedenza nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **packet_ptr:** puntatore a pacchetto contenente i dati da scrivere.
- **wait_option**: definisce per quanto tempo il servizio attenderà la scrittura del file del client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **valore di timeout**: (0x00000001 a 0xFFFFFFFE)
  - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso a tempo indeterminato fino a quando un server FTP non risponde alla richiesta. La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Scrittura del file FTP riuscita.
- **NX_FTP_NOT_OPEN**: il client FTP (0xD5) non è aperto.
- NX_PTR_ERROR: (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

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

Questo servizio abilita la modalità di trasferimento passivo se l'input passive_mode_enabled è impostato su NX_TRUE in un'istanza del client FTP creata in precedenza in modo che le chiamate successive per leggere o scrivere file (RETR, STOR) o scaricare un elenco di directory (NLST) siano eseguite in modalità di trasferimento. Per disabilitare il trasferimento in modalità passiva e tornare al comportamento predefinito della modalità di trasferimento attiva, chiamare questa funzione con l'input passive_mode_enabled impostato su NX_FALSE.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr:** puntatore al blocco di controllo client FTP.
- **passive_mode_enabled**:
  - Se impostato su NX_TRUE, la modalità passiva è abilitata.
  - Se impostata su NX_FALSE, la modalità passiva è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Impostato correttamente in modalità passiva.
- NX_PTR_ERROR: (0x16) Puntatore FTP non valido.
- NX_INVALID_PARAMETERS: (0x4D) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a>nx_ftp_server_create

Creare un server FTP

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

Questo servizio crea un'istanza del server FTP nell'istanza IP NetX specificata e creata in precedenza. Si noti che il server FTP deve essere avviato con una chiamata a ***nx_ftp_server_start*** che inizi l'operazione.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr:** puntatore al blocco di controllo del server FTP.
- **ftp_server_name**: nome del server FTP.
- **ip_ptr:** puntatore all'istanza IP NetX associata. Si noti che può essere presente un solo server FTP per un'istanza IP.
- **media_ptr:** puntatore all'istanza del supporto FileX associata.
- **stack_ptr:** puntatore alla memoria per l'area dello stack del thread del server FTP interno.
- **stack_size**: dimensione dell'area dello stack specificata da *stack_ptr*.
- **pool_ptr:** puntatore al pool di pacchetti NetX predefinito. Si noti che le dimensioni del payload dei pacchetti nel pool devono essere sufficientemente grandi da contenere il nome file/percorso più grande.
- **ftp_login:** puntatore a funzione alla funzione di accesso dell'applicazione. Questa funzione fornisce il nome utente e la password dal client che richiede una connessione. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.
- **ftp_logout:** puntatore a funzione alla funzione di disconnessione dell'applicazione. Questa funzione fornisce il nome utente e la password dal client che richiede una disconnessione. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione del server FTP riuscita.
- NX_PTR_ERROR: (0x16) Puntatore FTP non valido.

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

Eliminare il server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del server FTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr:** puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Eliminazione del server FTP completata.
- NX_PTR_ERROR: (0x16) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the FTP Server "my_server". */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a>nx_ftp_server_start

Avviare il server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia un'istanza del server FTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr:** puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Avvio del server FTP riuscito.
- NX_PTR_ERROR: (0x16) Puntatore FTP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```c
/* Start the FTP Server "my_server". */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a>nx_ftp_server_stop

Arrestare il server FTP

### <a name="prototype"></a>Prototipo

```c
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta un'istanza del server FTP creata in precedenza e avviata.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr:** puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Arresto del server FTP riuscito.
- NX_PTR_ERROR: (0x16) Puntatore FTP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the FTP Server "my_server". */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
