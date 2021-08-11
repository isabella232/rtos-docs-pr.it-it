---
title: Capitolo 1 - Introduzione al client POP3 netx Azure RTOS
description: L Azure RTOS'API client POP3 NetX fornisce un sistema di trasporto posta per le workstation di piccole dimensioni per accedere a Maildrop client nei server POP3 per il recupero della posta client.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6abaa778da6203d0df367894165cb29ca629ab5e24403a35af1995f032cf0d4c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798809"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pop3-client"></a>Capitolo 1 - Introduzione al client POP3 netx Azure RTOS

Post Office Protocol versione 3 (POP3) è un protocollo progettato per fornire un sistema di trasporto della posta per workstation di piccole dimensioni per accedere a maildrop client nei server POP3 per il recupero della posta client. POP3 usa Transmission Control Protocol (TCP) per eseguire il trasferimento della posta. Per questo scopo, POP3 è un protocollo di trasferimento del contenuto altamente affidabile.

POP3, tuttavia, non offre operazioni estese sulla gestione della posta. In genere, la posta elettronica viene scaricata dal client e quindi eliminata dal maildrop del server.

## <a name="netx-pop3-client-requirements"></a>Requisiti del client POP3 NetX

### <a name="client-requirements"></a>Requisiti del client

L Azure RTOS'API client POP3 NetX richiede un'istanza IP NetX creata in precedenza usando *nx_ip_create* e un pool di pacchetti NetX creato in precedenza *usando nx_packet_pool_create*. Poiché il client POP3 NetX utilizza i servizi TCP, è necessario che TCP sia abilitato con la chiamata *nx_tcp_enable* prima di usare i servizi client POP3 NetX nella stessa istanza IP. Il client POP3 usa un socket TCP per connettersi a un server POP3 sulla porta POP3 del server. Questo valore viene in genere impostato sulla *porta nota 110,* anche se per usare questa porta non è necessario né client POP3 né server.

Le dimensioni del pool di pacchetti usate nella creazione del client POP3 sono configurabili dall'utente in termini di payload del pacchetto e numero di pacchetti disponibili. Se il pacchetto viene usato solo nel servizio di creazione client POP3, il payload del pacchetto non deve essere superiore a 100-120 byte a seconda della lunghezza del nome utente e della password o del digest APOP. Il comando USER con il nome utente dell'host locale è probabilmente il messaggio più grande inviato dal client POP3. È possibile condividere lo stesso pool di pacchetti nel nx_ip_create (pool di pacchetti predefinito IP) perché le operazioni interne IP non richiedono un payload di pacchetti molto grande per l'invio e la ricezione di dati di controllo TCP.

Tuttavia, potrebbe non essere vantaggioso per il driver di rete usare lo stesso pool di pacchetti del pool di pacchetti client POP3. In genere, il payload del payload del pool di pacchetti di ricezione è impostato sull'MTU dell'istanza IP (in genere 1500 byte) dell'interfaccia di rete molto più grande dei messaggi del client POP3. I messaggi POP3 in ingresso sono in genere dati molto più grandi e quindi messaggi client POP3 in uscita

## <a name="netx-pop3-client-creation"></a>Creazione del client POP3 NetX

Il servizio di creazione client POP3 *nx_pop3_client_create* il socket TCP e connettersi al server POP3.

Dopo la connessione al server POP3, l'applicazione client POP3 può chiamare nx_pop3_client _mail_items_get per ottenere il numero di elementi di posta elettronica presenti nella relativa casella di controllo: 

```c
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
                                UINT *number_mail_items,
                                ULONG *maildrop_total_size)
```

Se uno o più elementi sono presenti nel maildrop client, l'applicazione può ottenere le dimensioni di un elemento di posta specifico, usando il *nx_pop3_client_get_mail_item* servizio:

```c
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
                                UINT mail_item,
                                ULONG *item_size)
```

Il primo elemento di posta elettronica nel maildrop si trova nell'indice 1.

Per ottenere il messaggio di posta elettronica effettivo, l'applicazione può chiamare il servizio *nx_pop3_client_mail_item_get_message_data* per recuperare i pacchetti di messaggio di posta finché il servizio non indica che l'ultimo pacchetto viene ricevuto dall'argomento di input final_packet di input:

```c
UINT nx_pop3_client_mail_item_message_get(
                        NX_POP3_CLIENT *client_ptr,
                        NX_PACKET **recv_packet_ptr,
                        ULONG *bytes_retrieved,
                        UINT *final_packet)
```

Per eliminare un elemento di posta elettronica specifico, l'applicazione chiama nx_pop3_client_mail_item_delete *con* lo stesso indice usato nella chiamata nx_pop3_client_get_mail_item *precedente.*

Il client può essere eliminato usando il *nx_pop3_client_delete* client. Si noti che l'applicazione deve eliminare il pool di pacchetti client POP3 usando il servizio *nx_packet_pool_delete* non è più in uso.

## <a name="netx-pop3-client-constraints"></a>Vincoli del client POP3 NetX

Esistono alcuni vincoli nell'implementazione del client POP3 NetX:

1. Il client POP3 NetX non supporta il comando AUTH anche se implementa l'autenticazione APOP usando DIGEST-MD5 per lo scambio di autenticazione del server client.

1. NetX POP3 Client non implementa tutti i comandi POP3 ,ad esempio i comandi TOP o UIDL. Di seguito è riportato un elenco di comandi supportati:
   - NOOP
   - RSET

## <a name="netx-pop3-client-login"></a>Accesso client POP3 NetX

Un client POP3 NetX deve autenticarsi (account di accesso) a un server POP3 per accedere a un maildrop. A tale scopo, è possibile usare i comandi USER/PASS e fornire un nome utente e una password noti al server POP3 oppure usando il comando APOP e il digest MD5 descritti di seguito.

Il nome utente è in genere un nome di dominio completo (contiene una parte locale e un nome di dominio, separati da un carattere '@'). Quando si usano i comandi POP3 USER e PASS, il client invia il nome utente e la password non crittografati tramite Internet.

Per evitare il rischio di sicurezza di password e nome utente non crittografati, il client POP3 NetX può essere configurato per l'uso dell'autenticazione APOP impostando il parametro *APOP_authentication* nel servizio *nx_pop3_client_create:*

```c
UINT  nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
                            UINT APOP_authentication,
                            NX_IP *ip_ptr,
                            NX_PACKET_POOL *packet_pool_ptr,
                            NXD_ADDRESS *server_ip_address, ULONG server_port,
                            CHAR *client_name,
                            CHAR *client_password)
```

In caso contrario, solo per le applicazioni IPv4, *nx_pop3_client_create* servizio:

```c
UINT  nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
                            UINT APOP_authentication,
                            NX_IP *ip_ptr,
                            NX_PACKET_POOL *packet_pool_ptr,
                            ULONG server_ip_address,
                            ULONG server_port, CHAR *client_name,
                            CHAR *client_password)
```

Quando il client invia il comando APOP, accetta un digest MD5 contenente il dominio del server, l'ora locale e l'ID processo estratti dal messaggio di saluto del server, oltre alla password del client. Il server POP3 creerà un digest MD5 contenente le stesse informazioni e, se il digest MD5 corrisponde al digest MD5 del client, il client viene autenticato.

Se l'autenticazione APOP non riesce, il client POP3 NetX tenterà l'autenticazione USER/PASS.

## <a name="the-pop3-client-maildrop"></a>The POP3 Client Maildrop

La posta client viene archiviata in un server POP3 in una cassetta postale o "maildrop". Un maildrop client in un server POP3 è rappresentato come un elenco di elementi di posta elettronica basato su 1. Ovvero, ogni messaggio viene indicato dal relativo indice nell'elenco di maildrop con il primo elemento di posta in corrispondenza dell'indice 1 (diverso da zero). I comandi POP3 fanno riferimento a elementi di posta elettronica specifici in base al relativo indice in questo elenco.

## <a name="the-pop3-protocol-state-machine"></a>Macchina a stati del protocollo POP3

Il protocollo POP3 richiede che client e server mantengano lo stato della sessione POP3. In primo luogo, il client tenta di connettersi al server POP3. Se ha esito positivo, entra nel protocollo POP3 che ha tre stati distinti definiti da RFC 1939. Lo stato iniziale è lo stato di autorizzazione in cui deve identificarsi nel server. Nello stato Autorizzazione, il client POP3 può eseguire solo i comandi USER e PASS e in tale ordine o il comando APOP.

Dopo l'autenticazione del client POP3, la sessione client entra nello stato Transazione. In questo stato, il client può scaricare e richiedere l'eliminazione della posta elettronica. I comandi consentiti nello stato Transaction sono LIST, STAT, RETR, DELE, RSET e QUIT. In genere il client POP3 invia un comando STAT seguito da una serie di comandi RETR (uno per ogni elemento di posta nel relativo maildrop).

Dopo che il client ha eseguito il comando QUIT, la sessione POP3 entra nello stato Di aggiornamento in cui avvia la disconnessione TCP dal server. Per scaricare la posta in un secondo momento, l'applicazione client POP3 può chiamare in qualsiasi momento per verificare la presenza di `nx_pop3_client_mail_items_get` nuovi messaggi nel maildrop.

### <a name="pop3-server-reply-codes"></a>Codici di risposta del server POP3

- **+OK:** il server usa questa risposta per accettare un comando client. Il server può includere informazioni aggiuntive dopo "+OK", ma non può presupporre che il client eelaborare queste informazioni, ad eccezione del caso di download dei dati dei messaggi di posta o dei comandi LIST o DELE. Nel secondo caso, l'argomento 'argument' dopo il comando fa riferimento all'indice dell'elemento di posta nel maildrop client.

- **-ERR:** il server usa questa risposta per rifiutare un comando client. Il server può inviare informazioni aggiuntive dopo "-ERR", ma non può presupporre che il client eserciti queste informazioni.

### <a name="sample-pop3-client---server-session"></a>Client POP3 di esempio - Sessione server

**Esempio POP3 di base con USER/PASS:**

```c
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

**Esempio POP3 di base con APOP (e LIST invece di STAT):**

```c
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

## <a name="rfcs-supported-by-netx-pop3-client"></a>RFC supportate dal client POP3 NetX

NetX Client POP3 è conforme a RFC 1939.
