---
title: Capitolo 3-Descrizione dei servizi client POP3 di Azure RTO NetX
description: Questo capitolo contiene una descrizione di tutti i servizi client POP3 di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1a0ab96a454bea9f56ced0d7aa8de5d481b284e9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822565"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pop3-client-services"></a>Capitolo 3-Descrizione dei servizi client POP3 di Azure RTO NetX

Questo capitolo contiene una descrizione di tutti i servizi client POP3 di Azure RTO NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- nx_pop3_client_create: *creare un'istanza del client POP3*
- nx_pop3_client_delete: *eliminare un'istanza del client POP3*
- nx_pop3_client_ mail_item_get: *eliminare un elemento di posta elettronica client dal server alla maildrop.*
- nx_pop3_client_mail_item_get: *recuperare una dimensione del messaggio di posta elettronica specifica*
- nx_pop3_client_mail_items_get: *ottenere il numero di elementi di posta elettronica in alla maildrop.*
- nx_pop3_client_mail_item_message _get: *scaricare un messaggio di posta elettronica specifico*
- nx_pop3_client_mail_item_size_get: *ottenere le dimensioni di un elemento di posta elettronica specifico*

## <a name="nx_pop3_client_create"></a>nx_pop3_client_create

Creare un'istanza del client POP3

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
                        UINT APOP_authentication, NX_IP *ip_ptr,
                        NX_PACKET_POOL *packet_pool_ptr,
                        ULONG server_ip_address,
                        ULONG server_port,
                        CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client POP3 e ne configura la configurazione con i parametri di input.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al client da creare
- **APOP_authentication**: abilitare l'autenticazione APOP
- **ip_ptr**: puntatore a istanza IP
- **packet_pool_ptr**: puntatore al pool di pacchetti client
- **server_ip_address**: indirizzo del server POP3
- **SERVER_PORT**: porta server POP3
- **client_name**: puntatore al nome client
- **client_password**: puntatore alla password client

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) client creato correttamente
- **stato**: completamento dello stato delle chiamate al servizio NETX e threadX
- NX_PTR_ERROR: (0x07) parametro puntatore di input non valido
- NX_POP3_PARAM_ERROR: (0xB1) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
/* Create the POP3 Client. */

/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST                   "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD          "pass"
#define POP3_SERVER_ADDRESS         IP_ADDRESS(192,2,2,92
#define POP3_SERVER_PORT            110

/* Create a NetX POP3 Client instance. */
ULONG server_ip_address = IP_ADDRESS(1,2,3,4);
status = nx_pop3_client_create(&demo_client,
        NX_FALSE /* disable APOP authentication */,
        &client_ip, &client_packet_pool,
        server_ip_address, POP3_SERVER_PORT,
        LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_delete"></a>nx_pop3_client_delete

Eliminare un'istanza del client POP3

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr)
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un client POP3 creato in precedenza. Il servizio non elimina il pool di pacchetti client POP3. L'applicazione del dispositivo deve eliminare questa risorsa separatamente se non è più usata per il pool di pacchetti.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al client da eliminare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) client eliminato correttamente
- NX_PTR_ERROR: (0x07) parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a>nx_pop3_client_mail_item_delete

Elimina un elemento di posta specificato dal client alla maildrop.

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
                                    UINT mail_index)
```

### <a name="description"></a>Descrizione

Questo servizio Elimina l'elemento di posta specificato dal client alla maildrop.. È destinato a dopo il download dell'elemento di posta elettronica, anche se alcuni server POP3 possono eliminare automaticamente gli elementi di posta dopo essere stati richiesti dal client.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore all'istanza del client
- **mail_index**: indicizzare in alla maildrop. client

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la richiesta di eliminazione è riuscita
- **NX_POP3_INVALID_MAIL_ITEM**: (0xB2) indice elemento di posta elettronica non valido
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) il payload del pacchetto client è troppo piccolo per la richiesta POP3.
- **NX_POP3_SERVER_ERROR_STATUS**: (0xB4) il server risponde con lo stato di errore
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) input dell'indice di posta non valido
- NX_PTR_ERROR: (0x07) parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
ULONG     item_index;

/* Delete the POP3 Client mail item. */
status = nx_pop3_client_mail_item_delete(&demo_client, item_index);

/* If the server accepts the DELE request (and deletes the mail item), status = 
   NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_get"></a>nx_pop3_client_mail_item_get

Recupera un elemento di posta elettronica specificato

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
                                UINT mail_item, ULONG *item_size)
```

### <a name="description"></a>Descrizione

Questo servizio esegue una richiesta RETR per recuperare un elemento di posta dal client alla maildrop. specificato dall'indice mail_item. Dopo aver eseguito una richiesta RETR e aver ricevuto una risposta positiva dal server, il client può avviare il download del messaggio di posta elettronica usando il servizio *nx_pop3_client_mail_item_message_get* . Si noti che il servizio fornisce anche la dimensione dell'elemento di posta elettronica richiesto estratto dalla risposta del server.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore all'istanza del client
- **mail_item**: indicizzare in alla maildrop. client
- **item_size**: puntatore alla dimensione del messaggio di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) elemento di posta recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM**: (0xB2) indice elemento di posta elettronica non valido
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) il payload del pacchetto client è troppo piccolo per la richiesta POP3.
- **NX_POP3_SERVER_ERROR_STATUS**: (0xB4) il server risponde con lo stato di errore
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) input dell'indice di posta non valido
- NX_PTR_ERROR: (0x07) parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
ULONG     item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a>nx_pop3_client_mail_items_get

Recuperare il numero di elementi di posta elettronica in alla maildrop.

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
                                UINT *number_mail_items,
                                ULONG *maildrop_total_size)
```

### <a name="description"></a>Descrizione

Questo servizio esegue una richiesta STAT per recuperare il numero di elementi di posta e le dimensioni totali dei dati del messaggio di posta elettronica dal client alla maildrop..

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore all'istanza del client
- **number_mail_item**: numero di messaggi di posta elettronica nel client alla maildrop.
- **maildrop_total_size**: puntatore alla dimensione di tutti i messaggi di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) elemento di posta recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM**: (0xB2) indice elemento di posta elettronica non valido
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) il payload del pacchetto client è troppo piccolo per la richiesta POP3.
- **NX_POP3_SERVER_ERROR_STATUS**: (0xB4) il server risponde con lo stato di errore 
- NX_PTR_ERROR: (0x07) parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
UINT      number_mail_items;
ULONG     maildrop_total_size;

/* Retrieve the size and number of items in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &number_mail_items,
                                        &maildrop_total_size);

/* If the maildrop data was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_message_get"></a>nx_pop3_client_mail_item_message_get

Recupera il messaggio di elemento di posta specificato

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_item_message_get(
                NX_POP3_CLIENT *client_ptr,
                NX_PACKET **recv_packet_ptr,
                ULONG *bytes_retrieved,
                UINT *final_packet)
```

### <a name="description"></a>Descrizione

Questo servizio recupera il messaggio dell'elemento di posta, le dimensioni del messaggio di posta elettronica e se è l'ultimo pacchetto del messaggio di posta elettronica. Se `final_packet` è NX_TRUE il pacchetto a cui punta `recv_packet_ptr` è il pacchetto finale nel messaggio dell'elemento di posta elettronica.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore all'istanza del client
- **recv_packet_ptr**: ricevuto pacchetto di dati del messaggio
- **number_mail_item**: numero di messaggi di posta elettronica nel client alla maildrop.
- **maildrop_total_size**: puntatore alla dimensione di tutti i messaggi di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) elemento di posta recuperato correttamente
- **NX_POP3_CLIENT_INVALID_STATE**: (0xB7) il payload del pacchetto client è troppo piccolo per la richiesta POP3.
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
NX_PACKET     *recv_packet_ptr;
ULONG         bytes_retrieved;
UINT          final_packet;

/* Retrieve the size and number of items in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_message_get (&demo_client, &recv_packet_ptr,
                                                bytes_retrieved, final_packet);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_size_get"></a>nx_pop3_client_mail_item_size_get

Recupera la dimensione dell'elemento di posta elettronica specificato

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_item_size_get(
                NX_POP3_CLIENT *client_ptr,
                UINT mail_item, ULONG *size)
```

### <a name="description"></a>Descrizione

Questo servizio esegue una richiesta di elenco per ottenere la dimensione dell'elemento di posta elettronica specificato.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore all'istanza del client
- **mail_item**: indicizzare in alla maildrop. client
- **dimensioni**: puntatore alla dimensione del messaggio di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) elemento di posta recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM**: (0xB2) indice elemento di posta elettronica non valido
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) il payload del pacchetto client è troppo piccolo per la richiesta POP3.
- **NX_POP3_SERVER_ERROR_STATUS**: (0xB4) il server risponde con lo stato di errore
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) input dell'indice di posta non valido
- NX_PTR_ERROR: (0x07) parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
ULONG     size;
UINT      mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
