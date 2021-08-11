---
title: Capitolo 1 - Introduzione al client SMTP Azure RTOS NetX Duo
description: Il Simple Mail Transfer Protocol (SMTP) è un protocollo per il trasferimento della posta tra reti e Internet.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: df8c6b6920577ebfc18ed9252761401c30822c034e30d7ae95b25778707f53d5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797823"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-smtp-client"></a>Capitolo 1 - Introduzione al client SMTP Azure RTOS NetX Duo

Il Simple Mail Transfer Protocol (SMTP) è un protocollo per il trasferimento della posta tra reti e Internet. Usa i servizi Reliable Transmission Control Protocol (TCP) per eseguire la funzione di trasferimento del contenuto.

## <a name="netx-duo-smtp-client-requirements"></a>Requisiti del client SMTP di NetX Duo

Il client SMTP di NetX Duo richiede la creazione di un'istanza IP di NetX Duo e di un pool di pacchetti NetX Duo. Il client SMTP utilizza un socket TCP per connettersi a un server SMTP sulla *porta nota 25. Pertanto,* TCP deve essere prima abilitato chiamando il *nx_tcp_enable* in un'istanza IP creata in precedenza.

La chiamata di creazione del client SMTP (nxd_smtp_client_create) richiede un pool di pacchetti creato in precedenza per la trasmissione di comandi SMTP al server e per l'invio del messaggio di posta elettronica effettivo. Il payload del pacchetto dipende dalle dimensioni previste del contenuto della posta e deve consentire TCP, l'intestazione IP e l'intestazione MAC. Si noti che l'intestazione IPv6 è di 40 byte, mentre l'intestazione IPv4 è di 20 byte.

Se l'intero messaggio di posta elettronica non può essere contenuto in un pacchetto, il client SMTP alloca pacchetti aggiuntivi per contenere il resto del messaggio.

## <a name="netx-duo-smtp-client-constraints"></a>Vincoli del client SMTP di NetX Duo

Anche se il protocollo SMTP di NetX Duo implementa gli standard RFC 2821 e 2554, esistono alcuni vincoli:

1. Il client SMTP di NetX Duo supporta solo l'autenticazione LOGIN e PLAIN, ma non l'autenticazione digest CRAM-MD5.
2. I messaggi del client SMTP di NetX Duo sono limitati a un destinatario per ogni elemento di posta e un solo messaggio di posta elettronica per ogni connessione TCP al server SMTP.
3. Le opzioni VRFY, SEND, SOML, EXPN, SAML, ETRN, TURN e SIZE SMTP non sono supportate.
4. Il client SMTP non è un browser di posta ("agente utente di posta") che viene in genere usato per la creazione del messaggio di posta elettronica. Si tratta solo di un "agente di trasferimento della posta". Fornirà l'elaborazione necessaria del corpo del messaggio di posta elettronica per il trasporto SMTP, come specificato in RFC 2821. Non controlla la sintassi corretta del contenuto, ad esempio il percorso del destinatario e il percorso inverso. Non esiste alcuna restrizione a ciò che si trova nel buffer di posta elettronica, ad esempio dati MIME o messaggi di testo non crittografato. Il formato del messaggio di posta, specificato in RFC 2822 per includere intestazioni e corpo del messaggio, non è compreso nell'ambito dell'API client SMTP.

## <a name="commands-supported-by-netx-duo-smtp-client"></a>Comandi supportati dal client SMTP di NetX Duo

Il client SMTP di NetX Duo usa i comandi seguenti durante una sessione di posta elettronica con un server SMTP.

- **EHLO** Il client desidera avviare una sessione che include alcuni o tutti i servizi SMTP del protocollo di estensione disponibili dal server SMTP. Questo è il valore predefinito.
- **HELO** Il client desidera avviare una sessione limitata ai servizi SMTP di base.
- **POSTA ELETTRONICA** Il client desidera che il server riceva la posta elettronica del client.
- **Autenticazione** Il client vuole avviare l'autenticazione dal server.
- **RCPT** Il client vuole inviare una cassetta postale di un altro host a cui si vuole recapitare il messaggio di posta elettronica.
- **DATI** Il client desidera avviare l'invio dei dati del messaggio di posta al server.
- **QUIT** Il client desidera terminare la sessione.

## <a name="getting-started"></a>Attività iniziali

L'applicazione client SMTP crea un'istanza IP e abilita TCP su tale istanza IP. Crea quindi il client SMTP usando il servizio seguente:

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

Il *client_packet_pool_ptr* è un puntatore a un pool di pacchetti creato in precedenza che il client SMTP userà per inviare messaggi al server SMTP.

Si noti che un'applicazione deve *fornire un from_address* per il dispositivo locale e un indirizzo IP del server. Tutti gli indirizzi devono essere nomi di dominio completi. Un nome di dominio completo contiene una parte locale e un nome di dominio, separati da un carattere "@". Si noti che il client SMTP non controlla la  sintassi del *from_address* o del recipient_address nel nx_smtp_mail_send seguente.

Dopo aver creato il client SMTP, l'applicazione client SMTP crea un elemento di posta elettronica con un messaggio di posta elettronica SMTP formattato correttamente e invia la richiesta al client SMTP usando l'API seguente:

```C
UINT nx_smtp_mail_send(NX_SMTP_CLIENT *client_ptr,
    CHAR *recipient_address, UINT priority,
    CHAR *subject, CHAR *mail_body,
    UINT mail_body_length);
```

Non esiste essenzialmente alcuna differenza nell'esecuzione del client SMTP su IPv4 o IPv6 dal punto di vista dell'utente. Le differenze tra i due protocolli IP vengono gestite nel livello NetX Duo sottostante.

Si noti che un'applicazione che vuole inviare messaggi di posta elettronica deve fornire un indirizzo del destinatario *nella nx_smtp_client_mail* chiamata.

Per l'autenticazione, i nomi utente possono essere nomi di dominio completi o visualizzare nomi utente. Ciò dipende dal modo in cui il server esegue l'autenticazione.

La demo nella sezione Small Example più avanti in questo Manuale dell'utente illustra come deve essere formattato il messaggio. Lo stato se l'elemento di posta elettronica è stato inviato correttamente verrà NX_SUCCESS. Se si verifica un errore, sia che si tratta di un errore interno, di una connessione TCP interrotta o della ricezione di un codice di errore di risposta del *server,* nx_smtp_mail_send restituirà uno stato di errore diverso da zero.

Quando si invia un elemento di posta elettronica, il client SMTP di NetX Duo crea una nuova connessione TCP con il server SMTP e avvia una sessione SMTP. In questa sessione il client invia una serie di comandi al server SMTP come parte del protocollo SMTP, in modo da inviare il messaggio di posta elettronica effettivo. La connessione TCP viene quindi terminata, indipendentemente dal risultato della sessione SMTP.

Dopo la trasmissione della posta elettronica, indipendentemente dall'esito positivo o negativo, il client SMTP viene restituito allo stato "iniziale" e può essere utilizzato per un'altra sessione di trasferimento della posta.

## <a name="netx-duo-smtp-authentication"></a>Autenticazione SMTP di NetX Duo

L'autenticazione consente ai client SMTP di dimostrare la propria identità al server SMTP e di inviare la posta elettronica come utenti attendibili. La maggior parte dei server SMTP commerciali richiede l'autenticazione dei client.

In genere, i dati di autenticazione sono costituiti dal nome utente e dalla password del mittente. Durante una richiesta di autenticazione, il server richiede queste informazioni e il client risponde inviando i dati richiesti in formato codificato. Il server decodifica i dati e tenta di trovare una corrispondenza nel relativo database utente. Se viene trovato, il server indica che l'autenticazione ha esito positivo. L'autenticazione SMTP è definita in [RFC 2554.](http://www.ietf.org/rfc/rfc2554.txt)

Esistono due tipi di autenticazione, in particolare *di base* e *digest.* Il digest non è supportato nell'attuale client SMTP di NetX Duo e non verrà illustrato qui. L'autenticazione di base equivale *all'autenticazione con* *nome e password* descritta in precedenza. Nell'autenticazione di base SMTP, il nome e le password sono codificati in base 64. Il vantaggio dell'autenticazione di base è la facilità di implementazione e l'uso diffuso. Lo svantaggio principale dell'autenticazione di base è che i dati relativi al nome e alla password vengono trasmessi apertamente nella richiesta.

### <a name="plain-authentication"></a>Autenticazione normale

Il client SMTP di NetX Duo invia un comando AUTH con il parametro PLAIN. Se il server SMTP di NetX Duo supporta questo tipo di autenticazione, risponderà con un codice di risposta 334. Il client risponde con un singolo messaggio di nome utente e password con codifica Base64 al server. Se il server determina che l'autenticazione client ha esito positivo, risponde con il codice di esito positivo 235.

### <a name="login-authentication"></a>Autenticazione dell'account di accesso

Il client SMTP di NetX Duo invia un comando AUTH con il parametro LOGIN. Se il server SMTP di NetX Duo supporta questo tipo di autenticazione, risponderà con un codice di risposta 334 come inizio della richiesta di autenticazione. Invia un prompt con codifica Base64 al client, che in genere è "Username". Il client decodifica il prompt e risponde con un nome utente con codifica Base64. Se il server accetta il nome utente client, invia una richiesta con codifica Base64 per la password client. Il client risponde con una password con codifica Base64. Se il server determina che l'autenticazione client ha esito positivo, risponde con il codice di esito positivo 235.

### <a name="no-authentication"></a>Nessuna autenticazione

Alcuni server SMTP sono configurati senza autenticazione. In tal caso, la risposta 250 al messaggio EHLO del client non elenca alcun tipo di autenticazione. Tuttavia, nessun tipo di autenticazione elencato non significa necessariamente che il server non richieda o supporti l'autenticazione. Se il client è configurato per l'autenticazione PLAIN o LOGIN in questa situazione, l'attività thread del client NetX Duo verrà impostata su PLAIN per impostazione predefinita. Se il client è configurato per NESSUNO, il passaggio di autenticazione viene ignorato e lo stato SMTP passa allo stato MAIL.

Si noti che se il client è configurato per nessuna autenticazione e il server SMTP supporta l'autenticazione, il tipo di autenticazione client viene commutato su PLAIN.

## <a name="rfcs-supported-by-netx-duo-smtp-client"></a>RFC supportate dal client SMTP di NetX Duo

L'API client SMTP di NetX Duo è conforme alle specifiche RFC2821 "Simple Mail Transfer Protocol" e RFC 2554 "SMTP Service Extension for Authentication". “
