---
title: Capitolo 3 - Descrizione dei servizi FTP
description: Questo capitolo contiene una descrizione di tutti i servizi FTP NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d08d3c07f7be016ece68ff2f58b9ac5ba93ded780105bce362674ed36b5b885d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792367"
---
# <a name="chapter-3---description-of-ftp-services"></a>Capitolo 3 - Descrizione dei servizi FTP

Questo capitolo contiene una descrizione di tutti i servizi FTP NetX (elencati di seguito) in ordine alfabetico (ad eccezione dei casi in cui gli equivalenti IPv4 e IPv6 dello stesso servizio sono abbinati tra loro).

> [!NOTE]
> Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="nx_ftp_client_connect"></a>nx_ftp_client_connect

Connessione a un server FTP su IPv4

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG server_ip, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio connette l'istanza del client FTP NetX creata in precedenza al server FTP all'indirizzo IP fornito.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **server_ip** Indirizzo IP del server FTP.
- **username** Nome utente client per l'autenticazione.
- **password** Password client per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la connessione client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response (Il valore di timeout (da 0x00000001 a 0xFFFFFFFE) Consente di specificare il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Connessione FTP riuscita.
- **NX_TFTP_EXPECTED_22X_CODE** (0xDB) Non è stata ricevuta una risposta 22X (ok)
- **NX_FTP_EXPECTED_23X_CODE** (0xDC) Non è stata ricevuta una risposta 23X (ok)
- **NX_FTP_EXPECTED_33X_CODE** (0xDE) Non è stata ricevuta una risposta 33X (ok)
- **NX_FTP_NOT_DISCONNECTED** client (0xD4) è già connesso.
- NX_PTR_ERROR (0x07) Input puntatore non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.
- NX_IP_ADDRESS_ERROR (0x21) Indirizzo IP non valido.

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

Connessione a un server FTP con supporto IPv6

### <a name="prototype"></a>Prototipo

```C
UINT nxd_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    NXD_ADDRESS *server_ipduo, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio connette l'istanza del client FTP NetX Duo creata in precedenza al server FTP all'indirizzo IP fornito. Sono supportate entrambe le reti IPv4 e IPv6.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **server_ipduo** Indirizzo IP del server FTP.
- **username** Nome utente client per l'autenticazione.
- **password** Password client per l'autenticazione.
- **wait_option** Definisce per quanto tempo il servizio attenderà la connessione client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response (Il valore di timeout (da 0x00000001 a 0xFFFFFFFE) Consente di specificare il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Connessione FTP riuscita.
- **NX_TFTP_EXPECTED_22X_CODE** (0xDB) Non è stata ricevuta una risposta 22X (ok)
- **NX_FTP_EXPECTED_23X_CODE** (0xDC) Non è stata ricevuta una risposta 23X (ok)
- **NX_FTP_EXPECTED_33X_CODE** (0xDE) Non è stata ricevuta una risposta 33X (ok)
- **NX_FTP_NOT_DISCONNECTED** (0xD4) Il client è già connesso
- NX_PTR_ERROR (0x07) Inout puntatore non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.
- NX_IP_ADDRESS_ERROR (0x21) Indirizzo IP non valido.

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
- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **window_size** Dimensioni della finestra annunciate per i socket TCP di questo client FTP.
- **pool_ptr** Puntatore al pool di pacchetti predefinito per questo client FTP. Si noti che il payload minimo del pacchetto deve essere sufficientemente grande da contenere il percorso completo e il nome del file o della directory.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione del client FTP riuscita.
- NX_PTR_ERROR (0x07) Input puntatore non valido.

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

Questo servizio elimina un'istanza del client FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del client FTP riuscita.
- **NX_FTP_NOT_DISCONNECTED** client FTP (0xD4) non disconnesso
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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
- **directory_name** Nome della directory da creare.
- **wait_option** Definisce per quanto tempo il servizio attenderà la creazione della directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione della directory FTP riuscita.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Impostare la directory predefinita nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la directory predefinita nel server FTP connesso al client FTP specificato. Questa directory predefinita si applica solo alla connessione del client.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **directory_path** Nome del percorso della directory da impostare.
- **wait_option** Definisce per quanto tempo il servizio attenderà il set di directory predefinito FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostazione predefinita FTP riuscita.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Eliminare la directory nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio elimina la directory specificata nel server FTP connesso al client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **directory_name** Nome della directory da eliminare.
- **wait_option** Definisce per quanto tempo il servizio attenderà l'eliminazione della directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione della directory FTP riuscita.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Questo servizio ottiene il contenuto della directory specificata nel server FTP connesso al client FTP specificato. Il puntatore al pacchetto fornito conterrà una o più voci di directory. Ogni voce è separata da una \<cr/lf\> combinazione. Il ***nx_ftp_client_directory_listing_continue*** deve essere chiamato per completare l'operazione di ottenere la directory.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **directory_name** Nome della directory di cui ottenere il contenuto.
- **packet_ptr** Puntatore al puntatore del pacchetto di destinazione. In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory.
- **wait_option** Definisce per quanto tempo il servizio attenderà l'elenco di directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Elenco di directory FTP riuscito.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_NOT_ENABLED** (0x14) (IPv6) non abilitato
- **NX_FTP_EXPECTED_1XX_CODE** (0xD9) Non è stata ricevuta una risposta 1XX (ok)
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Continuare l'elenco di directory dal server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio continua a ottenere il contenuto della directory specificata nel server FTP connesso al client FTP specificato. Dovrebbe essere stato immediatamente preceduto da una chiamata a ***nx_ftp_client_directory_listing_get***. In caso di esito positivo, il puntatore del pacchetto fornito conterrà una o più voci di directory. Questa routine deve essere chiamata fino a quando non viene ricevuto NX_FTP_END_OF_LISTING stato di errore.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **packet_ptr** Puntatore al puntatore del pacchetto di destinazione. In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory, separate da un <cr/lf>.
- **wait_option** Definisce per quanto tempo il servizio attenderà l'elenco di directory FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Elenco di directory FTP riuscito.
- **NX_FTP_END_OF_LISTING** (0xD8) Non sono presenti altre voci in questa directory.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Disconnettersi dal server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio disconnette una connessione al server FTP stabilita in precedenza con il client FTP specificato.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **wait_option** Definisce per quanto tempo il servizio attenderà la disconnessione del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Disconnessione FTP riuscita.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Disconnect “my_client” from the FTP Server. */

status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, “my_client” has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a>nx_ftp_client_file_close

Chiudere il file client

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio chiude un file aperto in precedenza nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **wait_option** Definisce per quanto tempo il servizio attenderà la chiusura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Chiusura del file FTP completata.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_FTP_NOT_OPEN (0xD5)** File non aperto; non può chiuderlo
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Eliminare un file nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio elimina il file specificato nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **file_name** Nome del file da eliminare.
- **wait_option** Definisce per quanto tempo il servizio attenderà l'eliminazione del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del file FTP completata.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Questo servizio apre il file specificato, per la lettura o la scrittura, nel server FTP connesso in precedenza all'istanza client specificata.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **file_name** Nome del file da aprire.
- **open_type** È **NX_FTP_OPEN_FOR_READ** o **NX_FTP_OPEN_FOR_WRITE**.
- **wait_option** Definisce per quanto tempo il servizio attenderà l'apertura del file del client FTP. Le opzioni di attesa sono definite come segue:
  - **valore di timeout** (da 0x00000001 a 0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da sospendere durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) La selezione TX_WAIT_FOREVER causa la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il file FTP è stato aperto correttamente.
- **NX_OPTION_ERROR** (0x0A) Tipo aperto non valido.
- **NX_FTP_NOT_CONNECTED** (0xD3) FTP Client non è connesso.
- **NX_FTP_NOT_CLOSED** (0xD6) FTP Client è già aperto.
- **NX_NO_FREE_PORTS** (0x45) Nessuna porta TCP disponibile da assegnare
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Questo servizio legge un pacchetto da un file aperto in precedenza. Deve essere chiamato in modo ripetitivo fino a quando non viene ricevuto NX_FTP_END_OF_FILE stato .

Si noti che il chiamante non alloca un pacchetto per questo servizio.  È necessario fornire solo un puntatore a un puntatore a pacchetto. Questo servizio aggiornerà il puntatore del pacchetto in modo che punti a un pacchetto recuperato dalla coda di ricezione del socket.  Se viene restituito uno stato riuscito, significa che è disponibile un pacchetto ed è responsabilità del chiamante rilasciare il pacchetto al termine dell'operazione.

Se viene restituito uno stato diverso da zero (stato di errore o NX_FTP_END_OF_FILE), il chiamante non rilascia il pacchetto. In caso contrario, viene generato un errore quando il puntatore del pacchetto è NULL.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **packet_ptr** Puntatore alla destinazione per il puntatore del pacchetto di dati da archiviare. In caso di esito positivo, il pacchetto contiene alcuni o tutti gli elementi del file.
- **wait_option** Definisce per quanto tempo il servizio attenderà la lettura del file del client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response (Il valore di timeout (da 0x00000001 a 0xFFFFFFFE) Consente di specificare il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Lettura del file FTP riuscita.
- **NX_FTP_NOT_OPEN** (0xD5) il client FTP non viene aperto.
- **NX_FTP_END_OF_FILE** (0xD7) Condizione di fine file.
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Rinominare il file nel server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
    CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio rinomina un file nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **filename** Nome corrente del file.
- **new_filename** Nuovo nome per il file.
- **wait_option** Definisce per quanto tempo il servizio attenderà la ridenominazione del file del client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response (Il valore di timeout (da 0x00000001 a 0xFFFFFFFE) Consente di specificare il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ridenominazione del file FTP riuscita.
- **NX_FTP_NOT_CONNECTED** (0xD3) il client FTP non è connesso.
- **NX_FTP_EXPECTED_3XX_CODE** (0XDD) Non ha ricevuto la risposta 3XX (ok)
- **NX_FTP_EXPECTED_2XX_CODE** (0xDA) Non è stata ricevuta una risposta 2XX (ok)
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Scrivere nel file

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio scrive un pacchetto di dati nel file aperto in precedenza nel server FTP.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **packet_ptr** Puntatore a pacchetto contenente i dati da scrivere.
- **wait_option** Definisce per quanto tempo il servizio attenderà la scrittura del file del client FTP. Le opzioni di attesa sono definite nel modo seguente:
  - **timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response (Il valore di timeout (da 0x00000001 a 0xFFFFFFFE) Consente di specificare il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server FTP.
  - **TX_WAIT_FOREVER** (0xFFFFFFFF) Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando un server FTP non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Scrittura del file FTP riuscita.
- **NX_FTP_NOT_OPEN** (0xD5) il client FTP non viene aperto.
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Questo servizio abilita la modalità di trasferimento passivo se l'input passive_mode_enabled è impostato su NX_TRUE in un'istanza del client FTP creata in precedenza in modo che le chiamate successive per leggere o scrivere file (RETR, STOR) o scaricare un elenco di directory (NLST) siano eseguite in modalità di trasferimento. Per disabilitare il trasferimento in modalità passiva e tornare al comportamento predefinito della modalità di trasferimento attiva, chiamare questa funzione con l'input passive_mode_enabled impostato su NX_FALSE.

### <a name="input-parameters"></a>Parametri di input

- **ftp_client_ptr** Puntatore al blocco di controllo client FTP.
- **passive_mode_enabled** Se impostato su NX_TRUE, la modalità passiva è abilitata.<br />Se impostata su NX_FALSE, la modalità passiva è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostato correttamente in modalità passiva.
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a>nx_ftp_server_create

Creare un server FTP

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

Questo servizio crea un'istanza del server FTP nell'istanza IP NetX specificata e creata in precedenza. Si noti che il server FTP deve essere avviato con una chiamata a ***nx_ftp_server_start*** che inizi l'operazione.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.
- **ftp_server_name** Nome del server FTP.
- **ip_ptr** Puntatore all'istanza IP NetX associata. Si noti che può essere presente un solo server FTP per un'istanza IP.
- **media_ptr** Puntatore all'istanza del supporto FileX associata.
- **stack_ptr** Puntatore alla memoria per l'area dello stack del thread del server FTP interno.
- **stack_size** Dimensione dell'area dello stack specificata *da stack_ptr*.
- **pool_ptr** Puntatore al pool di pacchetti NetX predefinito. Si noti che le dimensioni del payload dei pacchetti nel pool devono essere sufficientemente grandi da contenere il nome file/percorso più grande.
- **ftp_login** Puntatore a funzione alla funzione di accesso dell'applicazione. Questa funzione fornisce il nome utente e la password dal client che richiede una connessione e l'indirizzo client nel tipo di dati ULONG. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.
- **ftp_logout** Puntatore a funzione alla funzione di disconnessione dell'applicazione. Questa funzione fornisce il nome utente e la password dal client che richiede una disconnessione e l'indirizzo client nel tipo di dati ULONG. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione del server FTP riuscita.
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.

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

Creare un server FTP con supporto IPv4 e IPv6

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

Questo servizio crea un'istanza del server FTP nell'istanza IP NetX specificata e creata in precedenza. Si noti che il server FTP deve comunque essere avviato con una chiamata a ***nx_ftp_server_start*** che inizi l'operazione dopo la creazione del server.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.
- **ftp_server_name** Nome del server FTP.
- **ip_ptr** Puntatore all'istanza IP NetX associata. Si noti che può essere presente un solo server FTP per un'istanza IP.
- **media_ptr** Puntatore all'istanza del supporto FileX associata.
- **stack_ptr** Puntatore alla memoria per l'area dello stack del thread del server FTP interno.
- **stack_size** Dimensione dell'area dello stack specificata *da stack_ptr*.
- **pool_ptr** Puntatore al pool di pacchetti NetX predefinito. Si noti che le dimensioni del payload dei pacchetti nel pool devono essere sufficientemente grandi da contenere il nome file/percorso più grande.
- **ftp_login_duo** Puntatore a funzione alla funzione di accesso dell'applicazione. A questa funzione vengono forniti il nome utente e la password dal client che richiede una connessione e un puntatore all'indirizzo client nel NXD_ADDRESS dati. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.
- **ftp_logout_duo** Puntatore a funzione alla funzione di disconnessione dell'applicazione. A questa funzione vengono forniti il nome utente e la password dal client che richiede una disconnessione e un puntatore all'indirizzo client nel NXD_ADDRESS dati. Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione del server FTP riuscita.
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Eliminare il server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del server FTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del server FTP completata.
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the FTP Server “my_server”. */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a>nx_ftp_server_start

Avviare il server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia un'istanza del server FTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Avvio del server FTP riuscito.
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start the FTP Server “my_server”. */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a>nx_ftp_server_stop

Arrestare il server FTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta un'istanza del server FTP creata in precedenza e avviata.

### <a name="input-parameters"></a>Parametri di input

- **ftp_server_ptr** Puntatore al blocco di controllo del server FTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Arresto del server FTP riuscito.
- NX_PTR_ERROR (0x07) Puntatore FTP non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop the FTP Server “my_server”. */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
