---
title: Capitolo 3-Descrizione dei servizi TFTP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi TFTP NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 56f0d8edb991fff6ae30b6411e375ace58c544f7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821611"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-tftp-services"></a>Capitolo 3-Descrizione dei servizi TFTP di Azure RTO NetX Duo

Questo capitolo contiene una descrizione di tutti i servizi TFTP NetX Duo (elencati di seguito) in ordine alfabetico. Se non diversamente specificato, tutti i servizi supportano le comunicazioni IPv6 e IPv4.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nxd_tftp_client_file_open**: *aprire il file del client TFTP*

- **nxd_tftp_client_create**: *creare un'istanza del client TFTP*

- **nxd_tftp_client_delete**: *eliminare un'istanza del client TFTP*

- **nxd_tftp_client_error_info_get**: *ottenere informazioni sugli errori del client*

- **nxd_tftp_client_file_close**: *chiudere il file client*

- **nxd_tftp_client_file_open**: *Apri file client*

- **nxd_tftp_client_file_read**: *leggere un blocco dal file client*

- **nxd_tftp_client_file_write**: *scrittura del blocco nel file client*

- **nxd_tftp_client_packet_allocate**: *allocare il pacchetto per la scrittura del file client*

- **nxd_tftp_client_set_interface**: *impostare l'interfaccia fisica per le richieste TFTP*

- **nxd_tftp_server_create**: *creare un server TFTP*

- **nxd_tftp_server_delete**: *eliminare il server TFTP*

- **nxd_tftp_server_start**: *avvio del server TFTP*

- **nxd_tftp_server_stop**: *arrestare il server TFTP*

> [!NOTE] 
> Gli equivalenti IPv4 di tutti i servizi elencati in precedenza sono disponibili nel client e nel server TFTP NetX Duo, ad esempio *nx_tftp_server_create* e *nx_tftp_client_file_open*. Nelle pagine seguenti vengono fornite solo le descrizioni dell'API "Duo", ad esempio i servizi che iniziano con *nxd_*. Quando \* viene specificato un input di NXD_ADDRESS, l'API equivalente IPv4 chiama per l'input ULONG. In caso contrario, non esiste alcuna differenza nell'uso dell'API.

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
> L'applicazione deve assicurarsi che l'indirizzo IP e il pool di pacchetti specificati siano già stati creati. Inoltre, è necessario abilitare UDP per l'istanza IP prima di chiamare il servizio.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore al blocco di controllo client TFTP.

- **tftp_client_name** Nome dell'istanza del client TFTP

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

- **pool_ptr** Puntatore all'istanza del client TFTP del pool di pacchetti.

### <a name="return-values"></a>Valori restituiti

- Creazione TFTP riuscita **NX_SUCCESS**(0x00).

- La versione di IP **NX_TFTP_INVALID_IP_VERSION** (0X0C) non è valida o non è supportata

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) indirizzo IP del server non valido ricevuto

- ACK server **NX_TFTP_NO_ACK_RECEIVED** (0x09) non ricevuti

- NX_PTR_ERROR (0x16) un IP, un pool o un puntatore TFTP non valido.

- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

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

Questo servizio Elimina un'istanza del client TFTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore a un'istanza del client TFTP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Eliminazione del client TFTP riuscita **NX_SUCCESS** (0x00).

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

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

Ottenere informazioni sull'errore del client

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_error_info_get(NX_TFTP_CLIENT *tftp_client_ptr,
                        UINT *error_code, CHAR **error_string);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'ultimo codice di errore ricevuto e imposta il puntatore sulla stringa di errore interna del client. In condizioni di errore, l'utente può visualizzare l'ultimo errore inviato dal server. Una stringa di errore null indica che non è presente alcun errore.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore a un'istanza del client TFTP creata in precedenza.

- **error_code** Puntatore all'area di destinazione per il codice di errore

- **ERROR_STRING** Puntatore alla destinazione per la stringa di errore

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) informazioni sugli errori TFTP riuscite.  

- NX_PTR_ERROR (0x16) puntatore client TFTP non valido.

- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

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

Chiudi file client

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_file_close(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT ip_type);
```

### <a name="description"></a>Descrizione

Questo servizio chiude il file precedentemente aperto da questa istanza del client TFTP. A un'istanza del client TFTP può essere aperto un solo file alla volta.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore a un'istanza del client TFTP creata in precedenza.

- **ip_type** Indica il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- Chiusura del file TFTP **NX_SUCCESS** (0x00) completata.

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è un input puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Close the previously opened file associated with “my_client”. */
status =  nxd_tftp_client_file_close(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP file is closed. */
```

## <a name="nx_tftp_client_file_open"></a>nx_tftp_client_file_open

Apri file client TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr, 
            CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
            open_type, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di aprire il file specificato nel server TFTP all'indirizzo IP specificato. Il file verrà aperto per la lettura o la scrittura. 

> [!NOTE] 
> Questo è limitato solo ai pacchetti IPv4 ed è destinato a supportare le applicazioni TFTP NetX. Gli sviluppatori sono invitati a trasferire le proprie applicazioni a utilizzando il servizio "Duo" equivalente *nxd_tftp_client_file_open.*

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore al blocco di controllo TFTP.

- **file_name** Nome file ASCII, con terminazione NULL e con le informazioni sul percorso appropriate.

- **server_ip_address** Indirizzo TFTP del server.

- **open_type** Tipo di richiesta aperta:

  **NX_TFTP_OPEN_FOR_READ** (0x01)

  **NX_TFTP_OPEN_FOR_WRITE** (0x02)

- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'apertura del file del client TFTP. Le opzioni di attesa sono definite come segue:

  **valore di timeout** (0x00000001 tramite 0xfffffffe)

  **TX_WAIT_FOREVER** (0xFFFFFFFF) 
  
  Se si seleziona TX_WAIT_FOREVER, il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server TFTP non risponde alla richiesta. 
  
  La selezione di un valore numerico (1-0xFFFFFFFE) consente di specificare il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server TFTP.

- **ip_type** Indica il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- Apertura del file client **NX_SUCCESS** (0x00) riuscita

- Il client **NX_TFTP_NOT_CLOSED** (0xC3) ha già aperto il file

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) nessun ACK ricevuto dal server

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) IP del server non valido ricevuto

- Codice di errore ricevuto **NX_TFTP_CODE_ERROR** (0x05)

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

- NX_IP_ADDRESS_ERROR (0x21) indirizzo IP del server non valido

- Tipo aperto NX_OPTION_ERROR (0x0A) non valido

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

Apri file client TFTP

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

- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'apertura del file del client TFTP. Le opzioni di attesa sono definite come segue:

  **valore di timeout** (0x00000001 tramite 0xfffffffe)

  **TX_WAIT_FOREVER** (0xFFFFFFFF)

  Se si seleziona TX_WAIT_FOREVER, il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server TFTP non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) consente di specificare il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server TFTP.

- **ip_type** Indica il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- Apertura del file client **NX_SUCCESS** (0x00) riuscita

- Il client **NX_TFTP_NOT_CLOSED** (0xC3) ha già aperto il file

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) nessun ACK ricevuto dal server

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) versione IP non valida

- **NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) IP del server non valido ricevuto

- Codice di errore ricevuto **NX_TFTP_CODE_ERROR** (0x05)

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

- NX_IP_ADDRESS_ERROR (0x21) indirizzo IP del server non valido

- Tipo aperto NX_OPTION_ERROR (0x0A) non valido

- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

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

Leggi un blocco dal file client

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

- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del completamento dell'operazione di lettura. Le opzioni di attesa sono definite come segue:

  **valore di timeout** (0x00000001 tramite 0xfffffffe)

  **TX_WAIT_FOREVER** (0xFFFFFFFF)

  Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server TFTP non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi mentre è in attesa che il server TFTP invii un blocco del file.

- **ip_type** Indica il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- Lettura blocco client riuscita **NX_SUCCESS** (0x00)

- Il file client specificato **NX_TFTP_NOT_OPEN** (0xC3) non è aperto per la lettura

- **NX_NO_PACKET** (0x01) non è stato ricevuto alcun pacchetto dal server.

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) nessun ACK ricevuto dal server

- È stata rilevata la fine del file **NX_TFTP_END_OF_FILE** (0XC5) (non un errore).

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) versione IP non valida

- Codice di errore ricevuto **NX_TFTP_CODE_ERROR** (0x05)

- **NX_TFTP_FAILED** (0xC2) codice TFTP sconosciuto ricevuto

- **NX_TFTP_INVALID_BLOCK_NUMBER** (0x0A) numero di blocco non valido ricevuto

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

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

- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del completamento della scrittura. Le opzioni di attesa sono definite come segue:

  **valore di timeout** (0x00000001 tramite 0xfffffffe)

  **TX_WAIT_FOREVER** (0xFFFFFFFF)

  Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server TFTP non risponde alla richiesta.
 
  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi mentre è in attesa che il server TFTP invii un ACK per la richiesta di scrittura.

- **ip_type** Indica il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- Scrittura blocco client riuscita **NX_SUCCESS** (0x00)

- Il file client specificato **NX_TFTP_NOT_OPEN** (0xC3) non è aperto per la scrittura

- Timeout **NX_TFTP_TIMEOUT** (0xC1) in attesa di ACK server

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto

- **NX_TFTP_NO_ACK_RECEIVED** (0x09) nessun ACK ricevuto dal server

- **NX_TFTP_INVALID_IP_VERSION** (0x0C) versione IP non valida

- **NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto

- Codice di errore ricevuto **NX_TFTP_CODE_ERROR** (0x05)

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

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

Alloca pacchetto per la scrittura di file client

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_packet_allocate(NX_PACKET_POOL *pool_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a>Descrizione

Questo servizio alloca un pacchetto UDP dal pool di pacchetti specificato e crea spazio per l'intestazione TFTP a 4 byte prima che il pacchetto venga restituito al chiamante. Il chiamante può quindi compilare un buffer per la scrittura in un file client.

### <a name="input-parameters"></a>Parametri di input

- **pool_ptr** Puntatore al pool di pacchetti.

- **packet_ptr** Destinazione per il puntatore al pacchetto allocato.

- **WAIT_OPTION** Definisce per quanto tempo il servizio attenderà il completamento dell'allocazione del pacchetto. Le opzioni di attesa sono definite come segue:

  **valore di timeout** (0x00000001 tramite 0xfffffffe)

  **TX_WAIT_FOREVER** (0xFFFFFFFF)

  Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino al completamento dell'allocazione.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi in attesa dell'allocazione dei pacchetti.

- **ip_type** Indica il protocollo IP da usare. Le opzioni valide sono IPv4 (4) o IPv6 (6).

### <a name="return-values"></a>Valori restituiti

- Allocazione pacchetto riuscita **NX_SUCCESS** (0x00)

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Allocate a packet for TFTP file write. */
status =  nxd_tftp_client_packet_allocate(&my_pool, &packet_ptr, 200);

/* If status is NX_SUCCESS “packet_ptr” contains the new packet. */
```

## <a name="nxd_tftp_client_set_interface"></a>nxd_tftp_client_set_interface

Imposta l'interfaccia fisica per le richieste TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_client_set_interface(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT if_index);
```

### <a name="description"></a>Descrizione

Questo servizio usa l'indice dell'interfaccia di input per impostare l'interfaccia fisica per il client TFTP per l'invio e la ricezione di pacchetti TFTP. Il valore predefinito è zero, per l'interfaccia primaria.

> [!NOTE]
> NetX Duo deve supportare l'indirizzamento multihome (v 5.6 o versione successiva) per usare questo servizio.

### <a name="input-parameters"></a>Parametri di input

- **tftp_client_ptr** Puntatore all'istanza del client TFTP

- **if_index** Indice dell'interfaccia fisica da usare

### <a name="return-values"></a>Valori restituiti

- L'input dell'interfaccia (0x0B) dell'interfaccia non è valido per il **NX_SUCCESS** (0x00)

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

- Input dell'interfaccia NX_TFTP_INVALID_INTERFACE (0x0B) non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Specify the primary interface for TFTP requests. */
status =  nxd_tftp_client_set_interface(&client, 0);

/* If status is NX_SUCCESS the primary interface will be use for TFTP communications. */
```

## <a name="nxd_tftp_server_create"></a>nxd_tftp_server_create

Crea server TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_server_create(NX_TFTP_SERVER *tftp_server_ptr,
            CHAR *tftp_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr, 
            VOID *stack_ptr, ULONG stack_size,
            NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un server TFTP che risponde alle richieste del client TFTP sulla porta 69. Il server deve essere avviato da una chiamata successiva a *nxd_tftp_server_start*.

> [!IMPORTANT]
> L'applicazione deve verificare che siano già state create le istanze IP, il pool di pacchetti e l'istanza del supporto FileX specificati. Inoltre, è necessario abilitare UDP per l'istanza IP prima di chiamare il servizio.

### <a name="input-parameters"></a>Parametri di input

- **tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.

- **tftp_server_name** Nome dell'istanza del server TFTP

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

- **media_ptr** Puntatore all'istanza del supporto FileX.

- **stack_ptr** Puntatore all'area dello stack del server TFTP.

- **stack_size** Numero di byte nello stack del server TFTP.

- **pool_ptr** Puntatore al pool di pacchetti TFTP. 

> [!NOTE]
> Il pool fornito deve avere payload di pacchetti di almeno 580 byte. <sup>1</sup>

<sup>1</sup> la parte relativa ai dati di un pacchetto è esattamente 512 byte, ma le dimensioni del payload del pacchetto devono essere di almeno 572 byte. I byte rimanenti vengono usati per le intestazioni UDP, IPv6 e Ethernet e i potenziali byte finali richiesti dal driver per l'allineamento.

### <a name="return-values"></a>Valori restituiti

- Creazione di un server **NX_SUCCESS** (0x00) riuscita

- Il pool di pacchetti **NX_TFTP_POOL_ERROR** (0xc6) ha una dimensione del pacchetto inferiore a 560 byte

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

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

Elimina server TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_server_delete(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un server TFTP creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.

### <a name="return-values"></a>Valori restituiti

- Eliminazione server riuscita **NX_SUCCESS** (0x00)

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the TFTP Server called “my_server”. */
status =  nxd_tftp_server_delete(&my_server);

/* If status is NX_SUCCESS the TFTP Server is deleted. */
```

## <a name="nxd_tftp_server_start"></a>nxd_tftp_server_start

Avvia server TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_server_start(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia il server TFTP creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.

### <a name="return-values"></a>Valori restituiti

- Avvio del server **NX_SUCCESS** (0x00) riuscito

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.
 
### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Start the TFTP Server called “my_server”. */
status =  nxd_tftp_server_start(&my_server);

/* If status is NX_SUCCESS the TFTP Server is started. */
```

## <a name="nxd_tftp_server_stop"></a>nxd_tftp_server_stop

Arresta server TFTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_tftp_server_stop(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta il server TFTP creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.

### <a name="return-values"></a>Valori restituiti

- Arresto server riuscito **NX_SUCCESS** (0x00)

- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop the TFTP Server called “my_server”. */
status =  nxd_tftp_server_stop(&my_server);

/* If status is NX_SUCCESS the TFTP Server is stopped. */
```