---
title: Capitolo 3 - Descrizione client dei servizi client SMTP
description: Questo capitolo contiene una descrizione di tutti i servizi client SMTP di NetX Duo (elencati di seguito) in ordine di utilizzo in una tipica applicazione client SMTP.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bc54e7763c4a3977ef4d760bc92025b1cda792b979d741fc7b82f8f1a3f2901b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797807"
---
# <a name="chapter-3---client-description-of-smtp-client-services"></a>Capitolo 3 - Descrizione client dei servizi client SMTP

Questo capitolo contiene una descrizione di tutti i servizi client SMTP di NetX Duo (elencati di seguito) in ordine di utilizzo in una tipica applicazione client SMTP.

> [!NOTE]
> Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **grassetto** non sono interessati dalla definizione **_NX_DISABLE_ERROR_CHECKING_** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="nxd_smtp_client_create"></a>nxd_smtp_client_create

Creare un'istanza del client SMTP

### <a name="prototype"></a>Prototipo

```C
UINT nxd_smtp_client_create(NX_SMTP_CLIENT *client_ptr,
    NX_IP *ip_ptr, NX_PACKET_POOL
    *client_packet_pool_ptr,
    CHAR *username, CHAR *password,
    CHAR *from_address,
    CHAR *client_domain,
    UINT authentication_type, NXD_ADDRESS *server_address,
    UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client SMTP nell'istanza IP specificata.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SMTP;
- **ip_ptr** Puntatore all'istanza IP;
- **packet_pool_ptr** Puntatore al pool di pacchetti client;
- **nome utente** Nome utente con terminazione NULL** per l'autenticazione
- **password** Password con terminazione NULL per l'autenticazione
- **from_address** Indirizzo del mittente con terminazione NULL
- **client_domain** Nome di dominio con terminazione NULL
- **authentication_type** Tipo di autenticazione client. I tipi supportati sono:
  - NX_SMTP_CLIENT_AUTH_LOGIN
  - NX_SMTP_CLIENT_AUTH_PLAIN
  - NX_SMTP_CLIENT_AUTH_NONE
- **server_address** Puntatore all'indirizzo IP del server SMTP
- **server_port** Porta TCP del server SMTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client SMTP (0x00) è stato creato correttamente. Stato di creazione del socket TCP
- NX_SMTP_INVALID_PARAM (0xA5) Input non puntatore non valido
- NX_IP_ADDRESS_ERROR (0x21) Tipo di indirizzo IP non valido
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

codice dell'applicazione

### <a name="example"></a>Esempio

```C
/* Create the SMTP Client instance. */
NX_PACKET_POOL client_packet_pool;
NX_IP client_ip;
NX_SMTP_CLIENT demo_client;

#define USERNAME “myusername”
#define PASSWORD “mypassword”
#define FROM_ADDRESS “<myname@mycompany.com>”
#define LOCAL_DOMAIN “mycompany.com”
#define SERVER_PORT 25

/* Define client authentication type as LOGIN. 
    If not specified or unknown the SMTP Client will set it to PLAIN. */
#define CLIENT_AUTHENTICATION_TYPE NX_SMTP_CLIENT_AUTH_LOGIN

NXD_ADDRESS server_ip_address;

#ifdef USE_IPV6
    /* Set up the Server IPv6 address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    server_ip_address.nxd_ip_address.v6[1] = 0xf101;
    server_ip_address.nxd_ip_address.v6[2] = 0;
    server_ip_address.nxd_ip_address.v6[3] = 0x106;
#else
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_IP_ADDRESS;
#endif

status = nxd_smtp_client_create(&demo_client, &client_ip, &client_packet_pool,
    USERNAME, PASSWORD, FROM_ADDRESS,
    LOCAL_DOMAIN, CLIENT_AUTHENTICATION_TYPE,
    &server_ip_address, SERVER_PORT);

/* If an SMTP Client instance was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_smtp_client_delete"></a>nx_smtp_client_delete

Eliminare un'istanza del client SMTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_smtp_client_delete(NX_SMTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del client SMTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore all'istanza del client SMTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il client è stato eliminato
- NX_PTR_ERROR (0x07) Parametro puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the SMTP Client instance “my_client.” */

NX_SMTP_CLIENT demo_client;

status = nx_smtp_client_delete(&demo_client);

/* If an SMTP Client instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_smtp_mail_send"></a>nx_smtp_mail_send

Creare e inviare un elemento di posta SMTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_smtp_mail_send(NX_SMTP_CLIENT *client_ptr,
    CHAR *recipient_address,
    UINT priority, CHAR *subject,
    CHAR *mail_body,
    UINT mail_body_length);
```

### <a name="description"></a>Descrizione

Questo servizio crea e invia un elemento di posta SMTP. Il client SMTP stabilisce una connessione TCP con il server SMTP e invia una serie di comandi SMTP. Se non si verificano errori, trasmetterà il messaggio di posta elettronica al server. Indipendentemente dal fatto che il messaggio venga inviato correttamente, la connessione TCP verrà terminata e verrà restituito uno stato che indica il risultato della trasmissione della posta. L'applicazione può chiamare questo servizio per tutti i messaggi di posta elettronica che deve inviare senza limiti.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al client SMTP
- **recipient_address** Indirizzo del destinatario con terminazione NULL.
- **oggetto** Testo della riga dell'oggetto con terminazione NULL;.
- **priorità** Livello di priorità al quale viene recapitata la posta elettronica
- **mail_body** Puntatore al messaggio di posta elettronica
- **mail_body_length** Dimensioni del messaggio di posta elettronica

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Posta elettronica inviata correttamente
- **NX_SMTP_CLIENT_NOT_INITIALIZED(0xB2)** Smtp Client instance not initialized for SMTP session status Outcome of SMTP session (L'istanza del client SMTP non è stata inizializzata per lo stato della sessione SMTP Risultato della sessione SMTP)
- NX_PTR_ERROR (0x07) Parametro puntatore non valido
- NX_SMTP_INVALID_PARAM (0xA5) Input non puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Create and send a Client mail item. */

#define RECIPIENT_ADDRESS “<your@yourcompany.com>”
#define SUBJECT “NetX Duo SMTP Client Demo”
#define MAIL_BODY "NetX Duo SMTP client is an SMTP client ” \
    “implementation for embedded devices \r\n” \
    "to send email to SMTP servers.\r\n"

status = nx_smtp_mail_send(&demo_client, RECIPIENT_ADDRESS,
    NX_SMTP_MAIL_PRIORITY_NORMAL,
    SUBJECT_LINE, MAIL_BODY,
    sizeof(MAIL_BODY) - 1);

/* Return status being NX_SUCCESS indicates the mail has been
    successfully sent. */
```
