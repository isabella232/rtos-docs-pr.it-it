---
title: Capitolo 1-Introduzione ad Azure RTO NetX POP3
description: L'API client POP3 NetX Duo è progettata per fornire un sistema di trasporto della posta elettronica per le piccole workstation per accedere ai maildrops client sui server POP3 per il recupero della posta client.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4d41da1e1e87e59c5c40674a58b288ac62ec8c78
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821752"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pop3"></a>Capitolo 1-Introduzione ad Azure RTO NetX POP3

Il Post Office Protocol versione 3 (POP3) è un protocollo progettato per fornire un sistema di trasporto della posta elettronica per le piccole workstation per accedere ai client maildrops sui server POP3 per il recupero della posta client. POP3 utilizza i servizi Transmission Control Protocol (TCP) per eseguire il trasferimento della posta. Per questo motivo, POP3 è un protocollo di trasferimento del contenuto altamente affidabile.

Tuttavia, POP3 non fornisce operazioni estese alla gestione della posta elettronica. In genere, la posta elettronica viene scaricata dal client e quindi eliminata dal alla maildrop. del server.

## <a name="netx-duo-pop3-client-requirements"></a>Requisiti del client POP3 di NetX Duo

### <a name="client-requirements"></a>Requisiti del client

L'API client POP3 NetX richiede un'istanza IP di NetX Duo creata in precedenza usando *nx_ip_create* e un pool di pacchetti NETX creato in precedenza usando *nx_packet_pool_create*. Poiché il client POP3 NetX Duo usa i servizi TCP, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di usare l'API client POP3 di NETX Duo nella stessa istanza di IP. Il client POP3 utilizza un socket TCP per connettersi a un server POP3 sulla porta POP3 del server. Questa impostazione viene in genere impostata sulla *porta nota 110, anche se per l'utilizzo di questa porta non è necessario alcun client POP3 né server.*

Le dimensioni del pool di pacchetti usato per la creazione del client POP3 sono configurabili dall'utente in termini di payload del pacchetto e numero di pacchetti disponibili. Se il pacchetto viene usato solo nel servizio di creazione client POP3, il payload del pacchetto non deve essere superiore a 100-120 byte a seconda della lunghezza del nome utente e della password oppure del digest APOP. Il comando utente con il nome utente dell'host locale è probabilmente il messaggio più grande inviato dal client POP3. È possibile condividere lo stesso pool di pacchetti nella nx_ip_create (pool di pacchetti predefinito IP) perché la operatiosn interna IP non richiede un payload di pacchetti molto grande per l'invio e la ricezione di dati di controllo TCP.

Tuttavia, non è in genere vantaggioso che il driver Ethernet usi lo stesso pool di pacchetti del pool di pacchetti client POP3. In genere, il payload del payload del pool di pacchetti di ricezione viene impostato come MTU dell'istanza IP (in genere 1500 byte) dell'interfaccia di rete che è molto più grande dei messaggi client POP3. I messaggi POP3 in arrivo normalmente sono dimensioni dei dati più grandi, quindi i messaggi del client POP3 in uscita

## <a name="netx-duo-pop3-client-creation"></a>Creazione del client POP3 di NetX Duo

Per la creazione del client POP3 sono disponibili due servizi. Il servizio consigliato è *nxd_pop3_client_create* che accetta un tipo di dati indirizzo NXD_ADDRESS che accetta indirizzi IPv4 o IPv6 per il server POP3. L'altro client POP3 crea il servizio, *nx_pop3_client_create*, accetta solo indirizzi IPv4 per il server POP3. Entrambi i servizi associano la porta TCP socket e si connettono al server POP3.

Dopo la connessione al server POP3, l'applicazione client POP3 può chiamare *nx_pop3_client _mail_items_get* per ottenere il numero di elementi di posta che si siedono nella relativa casella alla maildrop.:

```C
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
    UINT *number_mail_items, ULONG *maildrop_total_size);
```

Se uno o più elementi si trovano nel client alla maildrop., l'applicazione può ottenere le dimensioni di un elemento di posta elettronica specifico usando il servizio *nx_pop3_client_get_mail_item* :

```C
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *item_size);
```

Il primo elemento di posta in alla maildrop. è in corrispondenza dell'indice 1.

Per ottenere il messaggio di posta elettronica effettivo, l'applicazione può chiamare il servizio *nx_pop3_client_mail_item_get_message_data* per recuperare i pacchetti dei messaggi di posta elettronica fino a quando il servizio non indica che l'ultimo pacchetto viene ricevuto dall'argomento di input final_packet:

```C
UINT nx_pop3_client_mail_item_message_get(
    NX_POP3_CLIENT *client_ptr,
    NX_PACKET **recv_packet_ptr,
    ULONG *bytes_retrieved,
    UINT *final_packet);
```

Per eliminare un elemento di posta elettronica specifico, l'applicazione chiama *nx_pop3_client_mail_item_delete* con lo stesso indice usato nella chiamata *nx_pop3_client_get_mail_item* precedente.

Il client può essere eliminato utilizzando il servizio *nx_pop3_client_delete* . Si noti che l'applicazione deve eliminare il pool di pacchetti client POP3 usando il servizio *nx_packet_pool_delete* non è più usato.

## <a name="netx-duo-pop3-client-constraints"></a>Vincoli client POP3 di NetX Duo

Sono presenti alcuni vincoli nell'implementazione del client POP3 NetX Duo:

1. Il client POP3 NetX Duo non supporta il comando AUTH, Sebbene implementi l'autenticazione APOP usando DIGEST-MD5 per lo scambio di autenticazione del server client.
2. Il client POP3 NetX Duo non implementa tutti i comandi POP3 (ad esempio, i comandi TOP o UIDL). Di seguito è riportato un elenco di comandi che supporta:
   - NOOP
   - RSET

## <a name="netx-duo-pop3-client-login"></a>Accesso client POP3 NetX Duo

Un client POP3 NetX Duo deve autenticarsi (login) a un server POP3 per accedere a un alla maildrop.. Questa operazione può essere eseguita usando i comandi USER/PASS e fornendo un nome utente e una password noti al server POP3 oppure usando il comando APOP e il digest MD5 descritto di seguito.

Il nome utente è in genere un nome di dominio completo (contiene una parte locale e un nome di dominio, separati da un carattere "@"). Quando si usa l'utente dei comandi POP3 e si passa, il client invia il nome utente e la password non crittografati tramite Internet.

Per evitare i rischi di sicurezza derivanti da nome utente e password non crittografati, il client POP3 NetX Duo può essere configurato per l'uso dell'autenticazione APOP impostando il parametro *APOP_authentication* nel servizio *nxd_pop3_client_create* :

```C
UINT nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication,
    NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    NXD_ADDRESS *server_ip_address, ULONG server_port,
    CHAR *client_name,
    CHAR *client_password);
```

O per le applicazioni solo IPv4, il servizio *nx_pop3_client_create* :

```C
UINT  nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    ULONG server_ip_address,
    ULONG server_port, CHAR *client_name,
    CHAR *client_password);
```

Quando il client invia il comando APOP, accetta come unico argomento un digest MD5 contenente il dominio del server, l'ora locale e l'ID processo estratti dal messaggio di saluto del server, più la password del client. Il server POP3 creerà un digest MD5 contenente le stesse informazioni e se il digest MD5 corrisponde al digest MD5 del client, il client viene autenticato.

Se l'autenticazione di APOP ha esito negativo, il client POP3 di NetX Duo tenterà l'autenticazione utente/PASS.

## <a name="the-pop3-client-maildrop"></a>Alla maildrop. client POP3

Posta elettronica client viene archiviato in un server POP3 in una cassetta postale o "alla maildrop.". Un alla maildrop. client in un server POP3 viene rappresentato come un elenco basato su 1 di elementi di posta elettronica. Ovvero, a ogni messaggio viene fatto riferimento dal relativo indice nell'elenco alla maildrop. con il primo elemento di posta in corrispondenza dell'indice 1 (diverso da zero). I comandi POP3 fanno riferimento a elementi di posta elettronica specifici in base al relativo indice nell'elenco.

## <a name="the-pop3-protocol-state-machine"></a>Macchina a Stati del protocollo POP3

Il protocollo POP3 richiede che sia il client che il server mantengano lo stato della sessione POP3. Innanzitutto, il client tenta di connettersi al server POP3. Se ha esito positivo, immette nel protocollo POP3 con tre stati distinti definiti da RFC 1939. Lo stato iniziale è lo stato di autorizzazione in cui deve identificarsi con il server. Nello stato di autorizzazione, il client POP3 può emettere solo l'utente e i comandi PASS e, in questo ordine, oppure il comando APOP.

Una volta autenticato il client POP3, la sessione client entra nello stato della transazione. In questo stato il client può scaricare e richiedere l'eliminazione della posta elettronica. I comandi consentiti nello stato della transazione sono LIST, STAT, RETR, DELE, RSET e QUIT. In genere il client POP3 invia un comando STAT seguito da una serie di comandi RETR (uno per ogni elemento di posta nel relativo alla maildrop.).

Una volta che il client ha eseguito il comando QUIT, la sessione POP3 entra nello stato di aggiornamento in cui avvia la disconnessione TCP dal server. Per scaricare la posta in un altro momento, l'applicazione client POP3 può chiamare nx_pop3_client_mail_items_get per verificare la presenza di nuovi messaggi di posta elettronica in alla maildrop..

### <a name="pop3-server-reply-codes"></a>Codici di risposta del server POP3

- + OK il server usa questa risposta per accettare un comando client. Il server può includere informazioni aggiuntive dopo ' + OK ', ma non può presupporre che il client elabori tali informazioni, tranne nel caso di download dei dati del messaggio di posta elettronica o dei comandi LIST o DELE. Nel secondo caso, l'argomento "argument" dopo il comando fa riferimento all'indice dell'elemento di posta elettronica nel client alla maildrop..
- -ERR il server usa questa risposta per rifiutare un comando client. Il server può inviare ulteriori informazioni dopo '-ERR ', ma non può presupporre che il client elabori le informazioni.

### <a name="sample-pop3-client---server-session"></a>Sessione client POP3 di esempio-server

**Esempio di POP3 di base che usa USER/PASS:**

```
S: <wait for connection on TCP port 110>
C: <open connection>
S: +OK POP3 server ready <1896.697170952@dbc.mtview.ca.us>
C: USER mrose
S: +OK mrose is valid
C: PASS mvan99
S: +OK mrose is logged in
C: STAT
S: +OK 2 320
C: RETR 1
S: +OK 120 octets
S: <the POP3 server sends message 1>
S: .
C: DELE 1
S: +OK message 1 deleted
C: RETR 2
S: +OK 200 octets
S: <the POP3 server sends message 2>
S: .
C: DELE 2
S: +OK message 2 deleted
C: QUIT
S: +OK POP3 server signing off (maildrop empty)
C: <close connection>
S: <wait for next connection>
```

**Esempio di POP3 di base con APOP (e LIST anziché STAT):**

```
S: <wait for connection on TCP port 110>
C: <open connection>
S: +OK POP3 server ready <1896.697170952@dbc.mtview.ca.us>
C: APOP mrose c4c9334bac560ecc979e58001b3e22fb
S: +OK mrose's maildrop has 2 messages (320 octets)
C: LIST
S: +OK 2 messages (320 octets)
S: 1 120
S: 2 200
S: .
C: RETR 1
S: +OK 120 octets
S: <the POP3 server sends message 1>
S: .
C: DELE 1
S: +OK message 1 deleted
C: RETR 2
S: +OK 200 octets
S: <the POP3 server sends message 2>
S: .
C: DELE 2
S: +OK message 2 deleted
C: QUIT
S: +OK dewey POP3 server signing off (maildrop empty)
C: <close connection>
S: <wait for next connection>
```

## <a name="rfcs-supported-by-netx-duo-pop3-client"></a>RFC supportate dal client POP3 NetX Duo

NetX Duo client POP3 è conforme a RFC 1939.
