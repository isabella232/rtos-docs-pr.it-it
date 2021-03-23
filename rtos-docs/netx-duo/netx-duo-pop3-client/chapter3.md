---
title: Capitolo 3-Descrizione dei servizi client POP3
description: Questo capitolo contiene una descrizione di tutti i servizi client POP3 di NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1f7681c8f3fe161db8a37a82574ab7d5e9bf348e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821746"
---
# <a name="chapter-3---description-of-pop3-client-services"></a>Capitolo 3-Descrizione dei servizi client POP3

Questo capitolo contiene una descrizione di tutti i servizi client POP3 di NetX Duo (elencati di seguito) in ordine alfabetico.

> [!NOTE]
> Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="nx_pop3_client_create"></a>nx_pop3_client_create

Creare un'istanza del client POP3 per IPv4

### <a name="prototype"></a>Prototipo

```C
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    ULONG server_ip_address, ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client POP3. Supporta solo indirizzi server POP3 IPv4.

Si noti che l'applicazione del dispositivo deve prima creare un'istanza IP e un pool di pacchetti affinché il client POP3 trasmetta i pacchetti. Questo pool di pacchetti creato per essere utilizzato esclusivamente dall'attività client POP3 o dallo stesso pool di pacchetti utilizzato nella creazione dell'istanza IP. Il pool di pacchetti può anche essere condiviso con il pool di pacchetti di driver Ethernet, ma ciò presenta lo svantaggio di usare pool di pacchetti di grandi dimensioni il cui payload è destinato alla ricezione di un payload di pacchetti potenzialmente grande per il client POP3 per inviare pacchetti di messaggi POP3 relativamente piccoli al server.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al client da creare
- **APOP_authentication** Abilitare l'autenticazione APOP
- **puntatore ip_ptr** all'istanza IP
- **packet_pool_ptr** Puntatore al pool di pacchetti client
- **server_ip_address** Indirizzo IPv4 del server POP3
- **SERVER_PORT** Porta server POP3
- **client_name** Puntatore al nome client
- **client_password** Puntatore alla password client

### <a name="return-values"></a>Valori restituiti

- Creazione del client **NX_SUCCESS** (0x00) completata
- **stato** di Stato di completamento delle chiamate al servizio NetX Duo e ThreadX
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido
- NX_POP3_PARAM_ERROR (0xB1) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Create the POP3 Client. Note that the Client uses its password for its APOP shared
    secret. */

/* Set up user defined callback services. */
/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD "pass"
#define POP3_SERVER_ADDRESS IP_ADDRESS(192,2,2,92)
#define POP3_SERVER_PORT 110

/* Create a NetX POP3 Client instance. */
status = nx_pop3_client_create(&demo_client,
    NX_FALSE /* disable APOP authentication */,
    &client_ip, &client_packet_pool,
    POP3_SERVER_ADDRESS, POP3_SERVER_PORT,
    LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nxd_pop3_client_create"></a>nxd_pop3_client_create

Creare un'istanza del client POP3 per IPv4 o IPv6

### <a name="prototype"></a>Prototipo

```C
UINT nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    NXD_ADDRESS *server_ip_address,
    ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client POP3. Supporta indirizzi server POP3 sia IPv4 che IPv6. Per ulteriori informazioni sul processo di creazione del client POP3, vedere il servizio *nx_pop3_client_create* descritto in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al client da creare
- **APOP_authentication** Abilitare l'autenticazione APOP
- **ip_ptr** Puntatore a istanza IP
- **packet_pool_ptr** Puntatore al pool di pacchetti client
- **server_ip_address** Indirizzo IPv4 o IPv6 del server POP3
- **SERVER_PORT** Porta server POP3
- **client_name**  Puntatore al nome client
- **client_password** Puntatore alla password client

### <a name="return-values"></a>Valori restituiti

- Creazione del client **NX_SUCCESS** (0x00) completata
- **stato** di Stato di completamento delle chiamate al servizio NetX Duo e ThreadX
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido
- NX_POP3_PARAM_ERROR (0xB1) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Create the POP3 Client. */

/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD "pass"
#define POP3_SERVER_PORT 110

/* Create a NetX POP3 Client instance. Also note the details of IPv6 address validation
    and enabling IPv6 and ICMPv6 services on the IP task are not shown here. See the
    NetX Duo User Guide for more details on this process.
*/
NXD_ADDRESS server_ip_address;

/* Set client IP interface address. */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0xf101;
server_ip_address.nxd_ip_address.v6[2] = 0;
server_ip_address.nxd_ip_address.v6[3] = 0x101;
status = nxd_pop3_client_create(&demo_client,
    NX_FALSE /* disable APOP authentication */,
    &client_ip, &client_packet_pool,
    &server_ip_address, POP3_SERVER_PORT,
    LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_delete"></a>nx_pop3_client_delete

Eliminare un'istanza del client POP3

### <a name="prototype"></a>Prototipo

```C
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un client POP3 creato in precedenza. Il servizio non elimina il pool di pacchetti client POP3. L'applicazione del dispositivo deve eliminare questa risorsa separatamente se non è più usata per il pool di pacchetti.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al client da eliminare

### <a name="return-values"></a>Valori restituiti

- Il client **NX_SUCCESS** (0x00) è stato eliminato
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a>nx_pop3_client_mail_item_delete

Elimina un elemento di posta specificato dal client alla maildrop.

### <a name="prototype"></a>Prototipo

```C
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
    UINT mail_index);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina l'elemento di posta specificato dal client alla maildrop.. È destinato a dopo il download dell'elemento di posta elettronica, anche se alcuni server POP3 possono eliminare automaticamente gli elementi di posta dopo essere stati richiesti dal client.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore all'istanza del client
- **mail_index** Indicizza in alla maildrop. client

### <a name="return-values"></a>Valori restituiti

- Richiesta di eliminazione **NX_SUCCESS** (0x00) riuscita
- **NX_POP3_INVALID_MAIL_ITEM**(0xB2) indice elemento di posta elettronica non valido
- Il payload del pacchetto client **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**(0xB6) è troppo piccolo per la richiesta POP3.
- Il server **NX_POP3_SERVER_ERROR_STATUS**(0xB4) risponde con lo stato di errore
- NX_POP3_CLIENT_INVALID_INDEX (0xB8) input dell'indice di posta non valido
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
ULONG item_index;

/* Delete the POP3 Client mail item. */
status = nx_pop3_client_mail_item_delete(&demo_client, item_index);

/* If the server accepts the DELE request (and deletes the mail item), status =
    NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_get"></a>nx_pop3_client_mail_item_get

Recupera un elemento di posta elettronica specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *item_size);
```

### <a name="description"></a>Descrizione

Questo servizio esegue una richiesta RETR per recuperare un elemento di posta dal client alla maildrop. specificato dall'indice mail_item. Dopo aver eseguito una richiesta RETR e aver ricevuto una risposta positiva dal server, il client può avviare il download del messaggio di posta elettronica usando il servizio *nx_pop3_client_mail_item_message_get* . Si noti che il servizio fornisce anche la dimensione dell'elemento di posta elettronica richiesto estratto dalla risposta del server.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore all'istanza del client
- **mail_item** Indicizza in alla maildrop. client
- **item_size** Puntatore alla dimensione del messaggio di posta elettronica

### <a name="return-values"></a>Valori restituiti

- Elemento di posta **NX_SUCCESS** (0x00) recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) indice elemento di posta elettronica non valido
- Il payload del pacchetto client **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) è troppo piccolo per la richiesta POP3.
- Il server **NX_POP3_SERVER_ERROR_STATUS** (0xB4) risponde con lo stato di errore
- NX_POP3_CLIENT_INVALID_INDEX (0xB8) input dell'indice di posta non valido
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
ULONG item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a>nx_pop3_client_mail_items_get

Recuperare il numero di elementi di posta elettronica in alla maildrop.

### <a name="prototype"></a>Prototipo

```C
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
    UINT *number_mail_items,
    ULONG *maildrop_total_size);
```

### <a name="description"></a>Descrizione

Questo servizio esegue una richiesta STAT per recuperare il numero di elementi di posta e le dimensioni totali dei dati del messaggio di posta elettronica dal client alla maildrop..

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore all'istanza del client
- **number_mail_item** Numero di messaggi nella alla maildrop. client
- **maildrop_total_size** Puntatore alla dimensione di tutti i messaggi di posta elettronica

### <a name="return-values"></a>Valori restituiti

- Elemento di posta **NX_SUCCESS** (0x00) recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) indice elemento di posta elettronica non valido
- Il payload del pacchetto client **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) è troppo piccolo per la richiesta POP3.
- Il server **NX_POP3_SERVER_ERROR_STATUS** (0xB4) risponde con lo stato di errore
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
UINT number_mail_items;

ULONG maildrop_total_size;

/* Retrieve the size and number of items in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_get (&demo_client, 1, &number_mail_items,
    &maildrop_total_size);

/* If the maildrop data was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_message_get"></a>nx_pop3_client_mail_item_message_get

Recupera il messaggio di elemento di posta specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_pop3_client_mail_item_message_get(
    NX_POP3_CLIENT *client_ptr,
    NX_PACKET **recv_packet_ptr,
    ULONG *bytes_retrieved,
    UINT *final_packet);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il messaggio dell'elemento di posta, le dimensioni del messaggio di posta elettronica e se è l'ultimo pacchetto del messaggio di posta elettronica. Se final_packet è NX_TRUE il pacchetto a cui punta recv_packet_ptr è il pacchetto finale nel messaggio dell'elemento di posta elettronica.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore all'istanza del client
- **recv_packet_ptr** È stato ricevuto il pacchetto dei dati del messaggio
- **number_mail_item** Numero di messaggi nella alla maildrop. client
- **maildrop_total_size** Puntatore alla dimensione di tutti i messaggi di posta elettronica

### <a name="return-values"></a>Valori restituiti

- Elemento di posta **NX_SUCCESS** (0x00) recuperato correttamente
- Il payload del pacchetto client **NX_POP3_CLIENT_INVALID_STATE** (0xB7) è troppo piccolo per la richiesta POP3.
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
NX_PACKET *recv_packet_ptr;

ULONG bytes_retrieved;

UINT final_packet;

/* Retrieve the size and number of items in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_message_get (&demo_client, &recv_packet_ptr,
    bytes_retrieved, final_packet);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_size_get"></a>nx_pop3_client_mail_item_size_get

Recupera la dimensione dell'elemento di posta elettronica specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_pop3_client_mail_item_size_get(
    NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *size);
```

### <a name="description"></a>Descrizione

Questo servizio esegue una richiesta di elenco per ottenere la dimensione dell'elemento di posta elettronica specificato.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore all'istanza del client
- **mail_item** Indicizza in alla maildrop. client
- **dimensioni** Puntatore alla dimensione del messaggio di posta elettronica

### <a name="return-values"></a>Valori restituiti

- Elemento di posta **NX_SUCCESS** (0x00) recuperato correttamente
- **NX_POP3_INVALID_MAIL_ITEM** (0xB2) indice elemento di posta elettronica non valido
- Il payload del pacchetto client **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) è troppo piccolo per la richiesta POP3.
- Il server **NX_POP3_SERVER_ERROR_STATUS** (0xB4) risponde con lo stato di errore
- NX_POP3_CLIENT_INVALID_INDEX (0xB8) input dell'indice di posta non valido
- Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da

Codice dell'applicazione

### <a name="example"></a>Esempio

```C
ULONG size;

UINT mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
