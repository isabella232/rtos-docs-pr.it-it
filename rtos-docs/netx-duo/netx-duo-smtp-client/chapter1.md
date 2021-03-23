---
title: Capitolo 1-Introduzione al client SMTP di Azure RTO NetX Duo
description: Il Simple Mail Transfer Protocol (SMTP) è un protocollo per il trasferimento di messaggi tra reti e Internet.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f58a0c235f5c2cd108ba97afe676ffa9b66e715c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821698"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-smtp-client"></a>Capitolo 1-Introduzione al client SMTP di Azure RTO NetX Duo

Il Simple Mail Transfer Protocol (SMTP) è un protocollo per il trasferimento di messaggi tra reti e Internet. USA i servizi di Reliable Transmission Control Protocol (TCP) per eseguire la relativa funzione di trasferimento del contenuto.

## <a name="netx-duo-smtp-client-requirements"></a>Requisiti del client SMTP NetX Duo

Per il client SMTP NetX Duo è necessario creare un'istanza IP di NetX Duo e un pool di pacchetti NetX Duo. Il client SMTP utilizza un socket TCP per connettersi a un server SMTP sul *noto porta 25. Pertanto*, è necessario abilitare il protocollo TCP chiamando il servizio *nx_tcp_enable* su un'istanza IP creata in precedenza.

Per la chiamata di creazione del client SMTP (nxd_smtp_client_create) è necessario un pool di pacchetti creato in precedenza per trasmettere i comandi SMTP al server e per inviare il messaggio di posta elettronica effettivo. Il payload dei pacchetti dipende dalle dimensioni previste del contenuto della posta e deve consentire l'intestazione TCP, IP e MAC. (Si noti che l'intestazione IPv6 è 40 byte mentre l'intestazione IPv4 è 20 byte).

Se l'intero messaggio di posta elettronica non può essere inserito in un pacchetto, il client SMTP alloca pacchetti aggiuntivi per contenere il resto del messaggio.

## <a name="netx-duo-smtp-client-constraints"></a>Vincoli client SMTP NetX Duo

Sebbene il protocollo SMTP NetX Duo implementi gli standard RFC 2821 e 2554, esistono alcuni vincoli:

1. Il client SMTP NetX Duo supporta solo l'accesso e l'autenticazione semplice, ma non l'autenticazione del digest CRAM-MD5.
2. I messaggi del client SMTP NetX Duo sono limitati a un destinatario per ogni elemento di posta elettronica e a un solo messaggio di posta elettronica per connessione TCP con il server SMTP.
3. Le opzioni SMTP VRFY, SEND, SOML, EXPN, SAML, ETRN, TURN e SIZE non sono supportate.
4. Il client SMTP non è il browser della posta elettronica ("agente utente di posta elettronica"), che in genere viene utilizzato per la creazione del messaggio di posta elettronica. Si tratta di un "Mail Transfer Agent". Fornirà l'elaborazione necessaria del corpo del messaggio di posta elettronica per il trasporto SMTP come specificato nella RFC 2821. Non controlla il contenuto per la sintassi corretta, ad esempio il destinatario e il percorso inverso. Non esiste alcuna restrizione presente nel buffer di posta elettronica, ad esempio i dati MIME o i messaggi di testo non crittografati. Il formato del messaggio di posta elettronica, specificato nella RFC 2822, per includere le intestazioni e il corpo del messaggio esula dall'ambito dell'API client SMTP.

## <a name="commands-supported-by-netx-duo-smtp-client"></a>Comandi supportati dal client SMTP NetX Duo

Il client SMTP NetX Duo usa i comandi seguenti durante una sessione di posta elettronica con un server SMTP.

- **EHLO** Il client desidera avviare una sessione che include alcuni o tutti i servizi SMTP del protocollo di estensione disponibili dal server SMTP. Questo è il valore predefinito.
- **HELO** Il client desidera avviare una sessione limitata ai servizi SMTP di base.
- **Posta elettronica** Il client desidera che il server riceva la posta client.
- **Autenticazione** di Il client desidera avviare l'autenticazione dal server.
- **RCPT** Il client desidera inviare una cassetta postale di un altro host a cui si desidera recapitare il messaggio.
- **Dati** di Il client desidera avviare l'invio di dati del messaggio di posta elettronica al server.
- **Chiudi** Il client desidera terminare la sessione.

## <a name="getting-started"></a>Introduzione

L'applicazione client SMTP crea un'istanza IP e un Abilita TCP sull'istanza IP. Viene quindi creato il client SMTP utilizzando il seguente servizio:

```C
UINT nxd_smtp_client_create(NX_SMTP_CLIENT *client_ptr,
    NX_IP *ip_ptr, NX_PACKET_POOL
    *client_packet_pool_ptr,
    CHAR *username, CHAR *password,
    CHAR *from_address,
    CHAR *client_domain,
    UINT authentication_type,
    NXD_ADDRESS *server_address, UINT port);
```

Il *client_packet_pool_ptr* è un puntatore a un pool di pacchetti creato in precedenza che il client SMTP utilizzerà per inviare messaggi al server SMTP.

Si noti che un'applicazione deve fornire un *from_address* per il dispositivo locale e un indirizzo IP del server. Tutti gli indirizzi devono essere nomi di dominio completi. Un nome di dominio completo contiene una parte locale e un nome di dominio, separati da un carattere "@". Si noti che il client SMTP non controlla la sintassi del *from_address* o del *recipient_address* nel servizio nx_smtp_mail_send di seguito.

Una volta creato il client SMTP, l'applicazione client SMTP crea un elemento di posta con un messaggio di posta SMTP formattato correttamente e Invia la richiesta di invio all'elemento di posta elettronica al client SMTP usando l'API seguente:

```C
UINT nx_smtp_mail_send(NX_SMTP_CLIENT *client_ptr,
    CHAR *recipient_address, UINT priority,
    CHAR *subject, CHAR *mail_body,
    UINT mail_body_length);
```

Non esiste essenzialmente alcuna differenza nell'esecuzione del client SMTP su IPv4 o IPv6 dal punto di vista dell'utente. Le differenze tra i due protocolli IP sono gestite nel livello NetX Duo sottostante.

Si noti che un'applicazione che desidera inviare messaggi di posta elettronica deve fornire un indirizzo del destinatario nella chiamata *nx_smtp_client_mail* .

Per l'autenticazione, i nomi utente possono essere nomi di dominio completi o visualizzare i nomi utente. Questo dipende dal modo in cui il server esegue l'autenticazione.

La demo nella sezione di esempio di piccole dimensioni più avanti in questo manuale dell'utente illustra come deve essere formattato il messaggio. Lo stato se l'elemento di posta elettronica è stato inviato correttamente sarà NX_SUCCESS. Se si verifica un errore, indipendentemente dal fatto che si tratti di un errore interno, una connessione TCP intermittente o la ricezione di un codice di errore di risposta del server, *nx_smtp_mail_send* restituirà uno stato di errore diverso da zero.

Quando si invia un elemento di posta elettronica, il client SMTP NetX duo crea una nuova connessione TCP con il server SMTP e avvia una sessione SMTP. In questa sessione, il client invia una serie di comandi al server SMTP come parte del protocollo SMTP, culminante nell'invio del messaggio di posta elettronica effettivo. La connessione TCP viene quindi terminata, indipendentemente dal risultato della sessione SMTP.

Dopo la trasmissione della posta elettronica, indipendentemente dall'esito positivo o negativo, il client SMTP viene restituito allo stato "iniziale" e può essere utilizzato per un'altra sessione di trasferimento della posta elettronica.

## <a name="netx-duo-smtp-authentication"></a>Autenticazione SMTP di NetX Duo

L'autenticazione è un modo per consentire ai client SMTP di dimostrare la propria identità al server SMTP e di consegnare la posta come utenti attendibili. Per la maggior parte dei server SMTP commerciali è necessario autenticare i client.

In genere, i dati di autenticazione sono costituiti dal nome utente e dalla password del mittente. Durante una richiesta di autenticazione, il server richiede queste informazioni e il client risponde inviando i dati richiesti in formato codificato. Il server decodifica i dati e tenta di trovare una corrispondenza nel relativo database utente. Se trovato, il server indica che l'autenticazione ha avuto esito positivo. L'autenticazione SMTP è definita nella [specifica RFC 2554](http://www.ietf.org/rfc/rfc2554.txt).

Esistono due tipi di autenticazione, ovvero *Basic* e *digest*. Il digest non è supportato nel client SMTP NetX Duo corrente e non verrà discusso qui. L'autenticazione di base equivale al *nome* e all'autenticazione della *password* descritti in precedenza. Nell'autenticazione di base SMTP, il nome e le password sono con codifica Base64. Il vantaggio dell'autenticazione di base è la semplicità di implementazione e l'uso generalizzato. Lo svantaggio principale dell'autenticazione di base è che i dati relativi al nome e alla password vengono trasmessi apertamente nella richiesta.

### <a name="plain-authentication"></a>Autenticazione semplice

Il client SMTP NetX Duo Invia un comando di autenticazione con il parametro PLAIN. Se il server SMTP NetX Duo supporta questo tipo di autenticazione, risponderà con un codice di risposta 334. Il client risponde con un singolo nome utente e password con codifica base64 al server. Se il server determina che l'autenticazione client ha esito positivo, risponde con il codice di esito positivo 235.

### <a name="login-authentication"></a>Autenticazione dell'account di accesso

Il client SMTP NetX Duo Invia un comando di autenticazione con il parametro LOGIN. Se il server SMTP NetX Duo supporta questo tipo di autenticazione, risponderà con un codice di risposta 334 come inizio dell'autenticazione ' Challenge '. Invia un prompt con codifica base64 al client, che in genere è "username". Il client decodifica la richiesta e risponde con un nome utente con codifica Base64. Se il server accetta il nome utente del client, invia una richiesta con codifica Base64 per la password client. Il client risponde con una password con codifica Base64. Se il server determina che l'autenticazione client ha esito positivo, risponde con il codice di esito positivo 235.

### <a name="no-authentication"></a>Nessuna autenticazione

Alcuni server SMTP sono configurati senza autenticazione. In tal caso, la risposta 250 al messaggio EHLO client non consentirà di elencare alcun tipo di autenticazione. Tuttavia, nessun tipo di autenticazione elencato non implica necessariamente che il server non richieda o supporti l'autenticazione. Se il client è configurato per l'autenticazione normale o di accesso in questa situazione, per impostazione predefinita l'attività thread client NetX Duo verrà impostata su normale. Se il client è configurato per nessuno, il passaggio di autenticazione viene ignorato e lo stato SMTP passa allo stato della posta.

Si noti che se il client è configurato per nessuna autenticazione e il server SMTP supporta l'autenticazione, il tipo di autenticazione client viene impostato come normale.

## <a name="rfcs-supported-by-netx-duo-smtp-client"></a>RFC supportate dal client SMTP NetX Duo

L'API client SMTP NetX Duo è conforme all'estensione del servizio SMTP RFC2821 "Simple Mail Transfer Protocol" e RFC 2554 "per l'autenticazione. “
