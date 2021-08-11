---
title: Capitolo 3 - Descrizione dei Azure RTOS NetX Duo TFTP
description: Questo capitolo contiene una descrizione di tutti i servizi NetX Duo TFTP (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: db7b7469bda02597db6428ecbf080b37a095413411eef2abefb1c4804d7bb1d3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799064"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-tftp-services"></a>Capitolo 3 - Descrizione dei Azure RTOS NetX Duo TFTP

Questo capitolo contiene una descrizione di tutti i servizi NetX Duo TFTP (elencati di seguito) in ordine alfabetico. Se non diversamente specificato, tutti i servizi supportano le comunicazioni IPv6 e IPv4.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nxd_tftp_client_file_open:** *aprire il file client TFTP*

- **nxd_tftp_client_create**: *Creare un'istanza del client TFTP*

- **nxd_tftp_client_delete**: *Eliminare un'istanza del client TFTP*

- **nxd_tftp_client_error_info_get:** ottenere *informazioni sugli errori del client*

- **nxd_tftp_client_file_close**: *Chiudere il file client*

- **nxd_tftp_client_file_open**: *aprire il file client*

- **nxd_tftp_client_file_read:** *Leggere un blocco dal file client*

- **nxd_tftp_client_file_write**: *Blocco di scrittura nel file client*

- **nxd_tftp_client_packet_allocate**: *Allocare un pacchetto per la scrittura di file client*

- **nxd_tftp_client_set_interface:** *impostare l'interfaccia fisica per le richieste TFTP*

- **nxd_tftp_server_create:** Creare *un server TFTP*

- **nxd_tftp_server_delete**: *Eliminare il server TFTP*

- **nxd_tftp_server_start**: *Avviare il server TFTP*

- **nxd_tftp_server_stop:** *Arrestare il server TFTP*

> [!NOTE] 
> Gli equivalenti IPv4 di tutti i servizi elencati in precedenza sono disponibili in NetX Duo TFTP Client e Server, ad esempio *nx_tftp_server_create* e *nx_tftp_client_file_open*. Nelle pagine seguenti vengono fornite solo le descrizioni dell'API "Duo", ad esempio i servizi che iniziano *con nxd_*, . Se viene specificato NXD_ADDRESS \* input, l'API equivalente IPv4 chiama per l'input ULONG. In caso contrario, non esiste alcuna differenza nell'uso dell'API.

## <a name="nxd_tftp_client_create"></a>nxd_tftp_client_create

Creare un'istanza del client TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_create(NX_TFTP_CLIENT *tftp_client_ptr,  
     CHAR *tftp_client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client TFTP per l'istanza IP creata in precedenza.

> [!IMPORTANT]
> L'applicazione deve assicurarsi che l'IP e il pool di pacchetti forniti siano già stati creati. È inoltre necessario che UDP sia abilitato per l'istanza IP prima di chiamare questo servizio.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore al blocco di controllo client TFTP.

- **tftp_client_name** Nome di questa istanza del client TFTP

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

- **pool_ptr** Puntatore all'istanza del client TFTP del pool di pacchetti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**(0x00) Creazione TFTP riuscita.

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) Versione IP non valida o non supportata

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Ricevuto indirizzo IP del server non valido

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) Server ACK non ricevuto

- NX_PTR_ERROR (0x16) Indirizzo IP, pool o puntatore TFTP non valido.

- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="example"></a>Esempio

```C
/* Create a TFTP Client instance. */
status =  nxd_tftp_client_create(&my_tftp_client, “My TFTP Client”, 
                                                    &my_ip, &pool_ptr);

/* If status is NX_SUCCESS a TFTP Client instance was successfully
   created. */
```

## <a name="nxd_tftp_client_delete"></a>nxd_tftp_client_delete

Eliminare un'istanza del client TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_delete(NX_TFTP_CLIENT *tftp_client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del client TFTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore all'istanza del client TFTP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del client TFTP completata.

- NX_PTR_ERROR (0x16) Input puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete a TFTP Client instance. */
status =  nxd_tftp_client_delete(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP Client instance was successfully
   deleted. */
```

## <a name="nxd_tftp_client_error_info_get"></a>nxd_tftp_client_error_info_get

Ottenere informazioni sugli errori del client

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_error_info_get(NX_TFTP_CLIENT *tftp_client_ptr,
                        UINT *error_code, CHAR **error_string);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'ultimo codice di errore ricevuto e imposta il puntatore alla stringa di errore interna del client. In condizioni di errore, l'utente può visualizzare l'ultimo errore inviato dal server. Una stringa di errore Null indica che non è presente alcun errore.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore all'istanza del client TFTP creata in precedenza.

- **error_code** Puntatore all'area di destinazione per il codice di errore

- **error_string** Puntatore alla destinazione per la stringa di errore

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ottenere informazioni sull'errore TFTP riuscito.  

- NX_PTR_ERROR (0x16) Puntatore client TFTP non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Get error information for client. */
status =  nxd_tftp_client_error_info_get(&my_tftp_client, &error_code,
                    &error_string_ptr);

/* If status is NX_SUCCESS the error code and error string are available. */
```

## <a name="nxd_tftp_client_file_close"></a>nxd_tftp_client_file_close

Chiudere il file client

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_file_close(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT ip_type);
```

### <a name="description"></a>Descrizione

Questo servizio chiude il file aperto in precedenza da questa istanza del client TFTP. Un'istanza del client TFTP può avere un solo file aperto alla volta.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore all'istanza del client TFTP creata in precedenza.

- **ip_type** Indicare il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Chiusura del file TFTP completata.

- NX_PTR_ERROR (0x16) Input puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Close the previously opened file associated with “my_client”. */
status =  nxd_tftp_client_file_close(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP file is closed. */
```

## <a name="nx_tftp_client_file_open"></a>nx_tftp_client_file_open

Aprire il file client TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr, 
            CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
            open_type, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di aprire il file specificato nel server TFTP all'indirizzo IP specificato. Il file verrà aperto per la lettura o la scrittura. 

> [!NOTE] 
> Questo è limitato solo ai pacchetti IPv4 ed è destinato al supporto di applicazioni NetX TFTP. Gli sviluppatori sono invitati a convertire le applicazioni all'uso di servizi "duo" *equivalenti nxd_tftp_client_file_open.*

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore al blocco di controllo TFTP.

- **file_name** Nome file ASCII, con terminazione NULL e con le informazioni sul percorso appropriate.

- **server_ip_address** Indirizzo TFTP del server.

- **open_type** Tipo di richiesta aperta:

  **NX_TFTP_OPEN_FOR_READ** (0x01)

  **NX_TFTP_OPEN_FOR_WRITE** (0x02)

- **wait_option** Definisce per quanto tempo il servizio attenderà l'apertura del file del client TFTP. Le opzioni di attesa sono definite nel modo seguente:

  **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)

  **TX_WAIT_FOREVER** (0xFFFFFFFF) 
  
  Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso a tempo indeterminato fino a quando un server TFTP non risponde alla richiesta. 
  
  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server TFTP.

- **ip_type** Indicare il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) File client riuscito aperto

- **NX_TFTP_NOT_CLOSED** (0xC3) Il client ha già un file aperto

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Indirizzo del server non valido ricevuto

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) Nessun ACK ricevuto dal server

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Indirizzo IP del server non valido ricevuto

- **NX_TFTP_CODE_ERROR** (0x05) Codice errore ricevuto

- NX_PTR_ERROR (0x16) Input puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

- NX_IP_ADDRESS_ERROR (0x21) Indirizzo IP del server non valido

- NX_OPTION_ERROR (0x0A) Tipo di apertura non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Define the TFTP server address. */
NXD_ADDRESS server_ip_address;

server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server _ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server _ip_address.nxd_ip_address.v6[1] = 0xf101;
server _ip_address.nxd_ip_address.v6[2] = 0;
server _ip_address.nxd_ip_address.v6[3] = 0x101;

/* Open file “test.txt” for reading on the TFTP Server. */
status =  nxd_tftp_client_file_open(&my_tftp_client, “test.txt”,
        & server_ip_address, NX_TFTP_OPEN_FOR_READ, 200);

/* If status is NX_SUCCESS the “test.txt” file is now open for reading. */
```

## <a name="nxd_tftp_client_file_open"></a>nxd_tftp_client_file_open

Aprire il file client TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr,
        CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
        open_type, ULONG wait_option, UINT ip_type);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di aprire il file specificato nel server TFTP all'indirizzo IPv6 specificato. Il file verrà aperto per la lettura o la scrittura.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore al blocco di controllo TFTP.

- **file_name** Nome file ASCII, con terminazione NULL e con le informazioni sul percorso appropriate.

- **server_ip_address** Indirizzo TFTP del server.

- **open_type** Tipo di richiesta aperta:

  **NX_TFTP_OPEN_FOR_READ** (0x01)

  **NX_TFTP_OPEN_FOR_WRITE** (0x02)

- **wait_option** Definisce per quanto tempo il servizio attenderà l'apertura del file del client TFTP. Le opzioni di attesa sono definite nel modo seguente:

  **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)

  **TX_WAIT_FOREVER** (0xFFFFFFFF)

  Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso a tempo indeterminato fino a quando un server TFTP non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risposta del server TFTP.

- **ip_type** Indicare il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) File client riuscito aperto

- **NX_TFTP_NOT_CLOSED** (0xC3) Il client ha già un file aperto

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Indirizzo del server non valido ricevuto

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) Nessun ACK ricevuto dal server

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) Versione IP non valida

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Indirizzo IP del server non valido ricevuto

- **NX_TFTP_CODE_ERROR** (0x05) Codice errore ricevuto

- NX_PTR_ERROR (0x16) Input puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

- NX_IP_ADDRESS_ERROR (0x21) Indirizzo IP del server non valido

- NX_OPTION_ERROR (0x0A) Tipo di apertura non valido

- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Define the TFTP server address. */
NXD_ADDRESS server_ip_address;

server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server _ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server _ip_address.nxd_ip_address.v6[1] = 0xf101;
server _ip_address.nxd_ip_address.v6[2] = 0;
server _ip_address.nxd_ip_address.v6[3] = 0x101;

/* Open file “test.txt” for reading on the TFTP Server. */
status =  nxd_tftp_client_file_open(&my_tftp_client, “test.txt”,
                & server_ip_address, NX_TFTP_OPEN_FOR_READ, 200);

/* If status is NX_SUCCESS the “test.txt” file is now open for reading. */
```

## <a name="nxd_tftp_client_file_read"></a>nxd_tftp_client_file_read

Leggere un blocco dal file client

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_file_read(NX_TFTP_CLIENT *tftp_client_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a>Descrizione

Questo servizio legge un blocco di 512 byte dal file del client TFTP aperto in precedenza. Un blocco contenente meno di 512 byte segnala la fine del file.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore al blocco di controllo client TFTP.

- **packet_ptr** Destinazione per il pacchetto contenente il blocco letto dal file.

- **wait_option** Definisce per quanto tempo il servizio attenderà il completamento della lettura. Le opzioni di attesa sono definite nel modo seguente:

  **valore di timeout** (da 0x00000001 a 0xFFFFFFFE)

  **TX_WAIT_FOREVER** (0xFFFFFFFF)

  Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso a tempo indeterminato fino a quando il server TFTP non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa che il server TFTP invii un blocco del file.

- **ip_type** Indicare il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Lettura del blocco client riuscita

- **NX_TFTP_NOT_OPEN** (0xC3) Il file client specificato non è aperto per la lettura

- **NX_NO_PACKET** (0x01) Nessun pacchetto ricevuto dal server.

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Indirizzo del server non valido ricevuto

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) Nessun servizio ACK ricevuto dal server

- **NX_TFTP_END_OF_FILE** (0xC5) Fine del file rilevata (non un errore).

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) Versione IP non valida

- **NX_TFTP_CODE_ERROR** (0x05) Codice errore ricevuto

- **NX_TFTP_FAILED** (0xC2) Ricevuto codice TFTP sconosciuto

- **NX_TFTP_INVALID_BLOCK_NUMBER** (0x0A) Numero di blocco non valido ricevuto

- NX_PTR_ERROR (0x16) Input puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Read a block from a previously opened file of “my_client”. */
status =  nxd_tftp_client_file_read(&my_tftp_client, &return_packet_ptr, 200);

/* If status is NX_SUCCESS a block of the TFTP file is in the payload of
   “return_packet_ptr”. */
```

## <a name="nxd_tftp_client_file_write"></a>nxd_tftp_client_file_write

Scrivere un blocco nel file client

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_file_write(NX_TFTP_CLIENT *tftp_client_ptr,
            NX_PACKET *packet_ptr, ULONG wait_option, UINT ip_type);
```

### <a name="description"></a>Descrizione

Questo servizio scrive un blocco di 512 byte nel file del client TFTP aperto in precedenza. Se si specifica un blocco contenente meno di 512 byte, viene segnalata la fine del file.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore al blocco di controllo client TFTP.

- **packet_ptr** Pacchetto contenente il blocco da scrivere nel file.

- **wait_option** Definisce per quanto tempo il servizio attenderà il completamento della scrittura. Le opzioni di attesa sono definite come segue:

  **valore di timeout** (0x00000001 tramite 0xFFFFFFFE)

  **TX_WAIT_FOREVER** (0xFFFFFFFF)

  Se si TX_WAIT_FOREVER il thread chiamante viene sospeso per un periodo illimitato fino a quando il server TFTP non risponde alla richiesta.
 
  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa che il server TFTP invii un ACK per la richiesta di scrittura.

- **ip_type** Indicare il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Scrittura del blocco client riuscita

- **NX_TFTP_NOT_OPEN** (0xC3) Il file client specificato non è aperto per la scrittura

- **NX_TFTP_TIMEOUT** (0xC1) in attesa di Server ACK

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Indirizzo server non valido ricevuto

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) Nessun ACK ricevuto dal server

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) Versione IP non valida

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Indirizzo server non valido ricevuto

- **NX_TFTP_CODE_ERROR** (0x05) Codice di errore ricevuto

- NX_PTR_ERROR (0x16) Input del puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Write a block to the previously opened file of “my_client”. */
status =  nxd_tftp_client_file_write(&my_tftp_client, packet_ptr, 200);

/* If status is NX_SUCCESS the block in the payload of “packet_ptr” was 
   written to the TFTP file opened by “my_client”. */
```

## <a name="nxd_tftp_client_packet_allocate"></a>nxd_tftp_client_packet_allocate

Allocare un pacchetto per la scrittura di file client

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_packet_allocate(NX_PACKET_POOL *pool_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a>Descrizione

Questo servizio alloca un pacchetto UDP dal pool di pacchetti specificato e fa spazio all'intestazione TFTP a 4 byte prima che il pacchetto venga restituito al chiamante. Il chiamante può quindi compilare un buffer per la scrittura in un file client.

### <a name="input-parameters"></a>Parametri di input

- **pool_ptr** Puntatore al pool di pacchetti.

- **packet_ptr** Destinazione per il puntatore al pacchetto allocato.

- **wait_option** Definisce per quanto tempo il servizio attenderà il completamento dell'allocazione del pacchetto. Le opzioni di attesa sono definite come segue:

  **valore di timeout** (0x00000001 tramite 0xFFFFFFFE)

  **TX_WAIT_FOREVER** (0xFFFFFFFF)

  La TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino al completamento dell'allocazione.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa dell'allocazione dei pacchetti.

- **ip_type** Indicare il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Corretta allocazione pacchetti

- NX_PTR_ERROR (0x16) Input del puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Allocate a packet for TFTP file write. */
status =  nxd_tftp_client_packet_allocate(&my_pool, &packet_ptr, 200);

/* If status is NX_SUCCESS “packet_ptr” contains the new packet. */
```

## <a name="nxd_tftp_client_set_interface"></a>nxd_tftp_client_set_interface

Impostare l'interfaccia fisica per le richieste TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_set_interface(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT if_index);
```

### <a name="description"></a>Descrizione

Questo servizio utilizza l'indice dell'interfaccia di input per impostare l'interfaccia fisica per il client TFTP per l'invio e la ricezione di pacchetti TFTP. Il valore predefinito è zero per l'interfaccia primaria.

> [!NOTE]
> NetX Duo deve supportare l'indirizzamento multihome (v5.6 o versione successiva) per usare questo servizio.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore all'istanza del client TFTP

- **if_index** Indice dell'interfaccia fisica da usare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'interfaccia (0x0B) non è valida

- NX_PTR_ERROR (0x16) Input del puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

- NX_TFTP_INVALID_INTERFACE (0x0B) Input di interfaccia non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Specify the primary interface for TFTP requests. */
status =  nxd_tftp_client_set_interface(&client, 0);

/* If status is NX_SUCCESS the primary interface will be use for TFTP communications. */
```

## <a name="nxd_tftp_server_create"></a>nxd_tftp_server_create

Creare un server TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_server_create(NX_TFTP_SERVER *tftp_server_ptr,
            CHAR *tftp_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr, 
            VOID *stack_ptr, ULONG stack_size,
            NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un server TFTP che risponde alle richieste del client TFTP sulla porta 69. Il server deve essere avviato da una chiamata successiva *a nxd_tftp_server_start*.

> [!IMPORTANT]
> L'applicazione deve assicurarsi che l'istanza IP, il pool di pacchetti e l'istanza del supporto FileX specificati siano già stati creati. È inoltre necessario che UDP sia abilitato per l'istanza IP prima di chiamare questo servizio.

### <a name="input-parameters"></a>Parametri di input

- **tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.

- **tftp_server_name** Nome dell'istanza del server TFTP

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

- **media_ptr** Puntatore all'istanza del supporto FileX.

- **stack_ptr** Puntatore all'area dello stack del server TFTP.

- **stack_size** Numero di byte nello stack del server TFTP.

- **pool_ptr** Puntatore al pool di pacchetti TFTP. 

> [!NOTE]
> Il pool fornito deve avere payload di pacchetti di almeno 580 byte. <sup>1</sup>

<sup>1</sup> La parte di dati di un pacchetto è esattamente di 512 byte, ma le dimensioni del payload del pacchetto devono essere di almeno 572 byte. I byte rimanenti vengono usati per le intestazioni UDP, IPv6 ed Ethernet e i byte finali potenziali richiesti dal driver per l'allineamento.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione server riuscita

- **NX_TFTP_POOL_ERROR** (0xC6) Il pool di pacchetti ha dimensioni del pacchetto inferiori a 560 byte

- NX_PTR_ERROR (0x16) Input del puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Create a TFTP Server called “my_server”. */
status =  nxd_tftp_server_create(&my_server, “My TFTP Server”, &server_ip, 
                &ram_disk, stack_ptr, 2048, pool_ptr);

/* If status is NX_SUCCESS the TFTP Server is created. */
```

## <a name="nxd_tftp_server_delete"></a>nxd_tftp_server_delete

Eliminare il server TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_server_delete(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un server TFTP creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del server riuscita

- NX_PTR_ERROR (0x16) Input del puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the TFTP Server called “my_server”. */
status =  nxd_tftp_server_delete(&my_server);

/* If status is NX_SUCCESS the TFTP Server is deleted. */
```

## <a name="nxd_tftp_server_start"></a>nxd_tftp_server_start

Avviare il server TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_server_start(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia il server TFTP creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Avvio del server riuscito

- NX_PTR_ERROR (0x16) Input puntatore non valido.
 
### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Start the TFTP Server called “my_server”. */
status =  nxd_tftp_server_start(&my_server);

/* If status is NX_SUCCESS the TFTP Server is started. */
```

## <a name="nxd_tftp_server_stop"></a>nxd_tftp_server_stop

Arrestare il server TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_server_stop(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta il server TFTP creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Arresto del server riuscito

- NX_PTR_ERROR (0x16) Input del puntatore non valido.

- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop the TFTP Server called “my_server”. */
status =  nxd_tftp_server_stop(&my_server);

/* If status is NX_SUCCESS the TFTP Server is stopped. */
```