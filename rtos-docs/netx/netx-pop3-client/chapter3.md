---
title: Capitolo 3 - Descrizione dei Azure RTOS client POP3 NetX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS client POP3 NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f68d6ac942c829dbf6eb9be334328b1b58a47ea370a73d37f471ec32cd46a360
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782388"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pop3-client-services"></a>Capitolo 3 - Descrizione dei Azure RTOS client POP3 NetX

Questo capitolo contiene una descrizione di tutti i Azure RTOS client POP3 NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **grassetto** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- nx_pop3_client_create: Creare *un'istanza del client POP3*
- nx_pop3_client_delete: *Eliminare un'istanza del client POP3*
- nx_pop3_client_ mail_item_get: *Eliminare un elemento di posta elettronica client dal server maildrop*
- nx_pop3_client_mail_item_get: Recuperare *una dimensione specifica del messaggio di posta elettronica*
- nx_pop3_client_mail_items_get: Ottenere *il numero di elementi di posta elettronica in maildrop*
- nx_pop3_client_mail_item_message _get: Scaricare *un messaggio di posta elettronica specifico*
- nx_pop3_client_mail_item_size_get: ottenere *le dimensioni di un elemento di posta elettronica specifico*

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

Questo servizio crea un'istanza del client POP3 e ne imposta la configurazione con i parametri di input.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr:** Puntatore al client da creare
- **APOP_authentication:** Abilitare l'autenticazione APOP
- **ip_ptr:** Puntatore all'istanza IP
- **packet_pool_ptr:** Puntatore al pool di pacchetti client
- **server_ip_address:** indirizzo del server POP3
- **server_port:** Porta del server POP3
- **client_name:** Puntatore al nome del client
- **client_password:** Puntatore alla password del client

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Client successfully created (Client creato correttamente)
- **status:** completamento dello stato delle chiamate ai servizi NetX e ThreadX
- NX_PTR_ERROR: (0x07) Parametro puntatore di input non valido
- NX_POP3_PARAM_ERROR: (0xB1) Input non puntatore non valido

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

Questo servizio elimina un client POP3 creato in precedenza. Non che questo servizio non elimini il pool di pacchetti del client POP3. L'applicazione del dispositivo deve eliminare questa risorsa separatamente se non è più in uso per il pool di pacchetti.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr:** Puntatore al client da eliminare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Il client è stato eliminato correttamente
- NX_PTR_ERROR: (0x07) Parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```c
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a>nx_pop3_client_mail_item_delete

Elimina un elemento di posta specificato dal messaggio di posta elettronica client

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
                                    UINT mail_index)
```

### <a name="description"></a>Descrizione

Questo servizio elimina l'elemento di posta specificato dal messaggio di posta elettronica client. È destinato a dopo il download dell'elemento di posta elettronica, anche se alcuni server POP3 possono eliminare automaticamente gli elementi di posta dopo essere stati richiesti dal client.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr:** Puntatore all'istanza del client
- **mail_index:** Inviare un indice alla posta elettronica del client

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Eliminazione richiesta riuscita
- **NX_POP3_INVALID_MAIL_ITEM:**(0xB2) Indice degli elementi di posta non valido
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD:** payload del pacchetto client (0xB6) troppo piccolo per la richiesta POP3.
- **NX_POP3_SERVER_ERROR_STATUS:**(0xB4) Il server risponde con stato di errore
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Input dell'indice di posta elettronica non valido
- NX_PTR_ERROR: (0x07) Parametro puntatore di input non valido

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

Recupera un elemento di posta specificato

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
                                UINT mail_item, ULONG *item_size)
```

### <a name="description"></a>Descrizione

Questo servizio effettua una richiesta RETR per recuperare un elemento di posta dal messaggio di posta elettronica client specificato dall'indice mail_item. Dopo aver inviato una richiesta RETR e aver ricevuto una risposta positiva dal server, il client può iniziare a scaricare il messaggio di posta elettronica usando il *nx_pop3_client_mail_item_message_get* servizio. Si noti che il servizio fornisce anche le dimensioni dell'elemento di posta richiesto estratto dalla risposta del server.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr:** Puntatore all'istanza del client
- **mail_item:** Index into Client maildrop
- **item_size:** Puntatore alle dimensioni del messaggio di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Elemento di posta elettronica recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM:**(0xB2) Indice degli elementi di posta non valido
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD:** payload del pacchetto client (0xB6) troppo piccolo per la richiesta POP3.
- **NX_POP3_SERVER_ERROR_STATUS:**(0xB4) Il server risponde con stato di errore
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Input dell'indice di posta elettronica non valido
- NX_PTR_ERROR: (0x07) Parametro puntatore di input non valido

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

Recuperare il numero di elementi di posta elettronica in maildrop

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
                                UINT *number_mail_items,
                                ULONG *maildrop_total_size)
```

### <a name="description"></a>Descrizione

Questo servizio effettua una richiesta STAT per recuperare il numero di elementi di posta elettronica e le dimensioni totali dei dati dei messaggi di posta elettronica dal messaggio di posta elettronica client.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr:** Puntatore all'istanza del client
- **number_mail_item:** Numero di messaggi di posta elettronica nella inviare tramite posta elettronica client
- **maildrop_total_size:** puntatore alle dimensioni di tutti i messaggi di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Elemento di posta elettronica recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM:**(0xB2) Indice degli elementi di posta non valido
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD:** payload del pacchetto client (0xB6) troppo piccolo per la richiesta POP3.
- **NX_POP3_SERVER_ERROR_STATUS:**(0xB4) Il server risponde con stato di errore 
- NX_PTR_ERROR: (0x07) Parametro puntatore di input non valido

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

Recupera il messaggio dell'elemento di posta specificato

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_item_message_get(
                NX_POP3_CLIENT *client_ptr,
                NX_PACKET **recv_packet_ptr,
                ULONG *bytes_retrieved,
                UINT *final_packet)
```

### <a name="description"></a>Descrizione

Questo servizio recupera il messaggio dell'elemento di posta, le dimensioni del messaggio di posta elettronica e se si tratta dell'ultimo pacchetto nel messaggio di posta elettronica. Se `final_packet` è NX_TRUE il pacchetto a cui punta è il pacchetto finale nel messaggio dell'elemento di `recv_packet_ptr` posta.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr:** Puntatore all'istanza del client
- **recv_packet_ptr:** Pacchetto di dati del messaggio ricevuto
- **number_mail_item:** Numero di messaggi di posta elettronica nella inviare tramite posta elettronica client
- **maildrop_total_size:** puntatore alle dimensioni di tutti i messaggi di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Elemento di posta elettronica recuperato correttamente
- **NX_POP3_CLIENT_INVALID_STATE:** payload del pacchetto client (0xB7) troppo piccolo per la richiesta POP3.
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido

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

Recupera le dimensioni dell'elemento di posta specificato

### <a name="prototype"></a>Prototipo

```c
UINT nx_pop3_client_mail_item_size_get(
                NX_POP3_CLIENT *client_ptr,
                UINT mail_item, ULONG *size)
```

### <a name="description"></a>Descrizione

Questo servizio effettua una richiesta LIST per ottenere le dimensioni dell'elemento di posta specificato.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr:** Puntatore all'istanza del client
- **mail_item:** Index into Client maildrop
- **size:** puntatore alle dimensioni del messaggio di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Elemento di posta elettronica recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM:**(0xB2) Indice degli elementi di posta non valido
- **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD:** payload del pacchetto client (0xB6) troppo piccolo per la richiesta POP3.
- **NX_POP3_SERVER_ERROR_STATUS:**(0xB4) Il server risponde con stato di errore
- NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Input dell'indice di posta elettronica non valido
- NX_PTR_ERROR: (0x07) Parametro puntatore di input non valido

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
