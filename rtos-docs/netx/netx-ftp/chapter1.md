---
title: Capitolo 1 - Introduzione a Azure RTOS FTP NetX
description: Il File Transfer Protocol (FTP) è un protocollo progettato per i trasferimenti di file. FTP usa servizi reliable Transmission Control Protocol (TCP) per eseguire la funzione di trasferimento file.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 35a7487720578ce8da578c490d96aa3c444ee818167b1bbd10833556e34b3dce
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799473"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-ftp"></a>Capitolo 1 - Introduzione a Azure RTOS FTP NetX

Il File Transfer Protocol (FTP) è un protocollo progettato per i trasferimenti di file. FTP usa servizi reliable Transmission Control Protocol (TCP) per eseguire la funzione di trasferimento file. Per questo scopo, FTP è un protocollo di trasferimento file altamente affidabile. Ftp offre anche prestazioni elevate. Il trasferimento effettivo di file FTP viene eseguito su una connessione FTP dedicata.

## <a name="ftp-requirements"></a>Requisiti FTP

Per il corretto funzionamento, il Azure RTOS FTP NetX richiede che sia già stata creata un'istanza IP NetX. È inoltre necessario che TCP sia abilitato nella stessa istanza IP. La parte client FTP del pacchetto FTP NetX non presenta altri requisiti.

La parte server FTP del pacchetto FTP NetX presenta diversi requisiti aggiuntivi. Prima di tutto, richiede l'accesso completo alla porta TCP *nota 21* per la gestione di tutte le richieste di comando FTP client e alla porta *20* nota per la gestione di tutti i trasferimenti di dati FTP client. Il server FTP è progettato anche per l'uso con l'file system FileX. Se FileX non è disponibile, l'utente può convertire le parti di FileX usate nel proprio ambiente. Questo argomento viene illustrato nelle sezioni successive di questa guida.

## <a name="ftp-constraints"></a>Vincoli FTP

Lo standard FTP include molte opzioni relative alla rappresentazione dei dati dei file. Analogamente alle implementazioni Unix, FTP NetX presuppone i vincoli di formato di file seguenti:

- Tipo di file: **Binario**
- Formato file: **solo non stampa**
- Struttura file: **solo struttura di file**
- Modalità di trasmissione: **solo modalità flusso**

## <a name="ftp-file-names"></a>Nomi di file FTP

I nomi di file FTP devono essere nel formato del file system di destinazione (in genere FileX). Devono essere stringhe ASCII con terminazione NULL, con informazioni sul percorso completo, se necessario. Non è stato specificato alcun limite per le dimensioni dei nomi di file FTP nell'implementazione FTP NetX. Tuttavia, le dimensioni del payload del pool di pacchetti devono essere in grado di contenere il percorso massimo e/o il nome file.

## <a name="ftp-client-commands"></a>Comandi client FTP

FTP dispone di un meccanismo semplice per l'apertura delle connessioni e l'esecuzione di operazioni su file e directory. Esiste fondamentalmente un set di comandi FTP standard emessi dal client dopo che una connessione è stata stabilita correttamente sulla porta TCP *nota 21.* Di seguito sono illustrati alcuni comandi FTP di base:

### <a name="ftp-command-and-meaning"></a>Comando FTP e significato

- **Percorso CWD:** modificare *la directory di lavoro*
- **DELE filename**: *Elimina il nome file specificato*
- **Directory LIST:** *ottenere l'elenco di directory*
- **Directory MKD:** *crea una nuova directory*
- **Directory NLST:** ottenere *l'elenco di directory*
- **NOOP:** *nessuna operazione, restituisce l'esito positivo*
- **PASS password**: *specificare la password per l'accesso*
- **PASV:** *richiedere la modalità di trasferimento passivo*
- **Percorso PWD:** *percorso della directory corrente di prelievo*
- **QUIT:** *termina la connessione client*
- **RETR filename**: *Legge il file specificato*
- **Directory RMD:** *elimina la directory specificata*
- **RNFR oldfilename:** *specificare il file da rinominare*
- **RNTO newfilename:** *rinominare il file in nome file specificato*
- **Nome file STOR:** *scrivere il file specificato*
- **TIPO I:** selezionare *l'immagine del file binario*
- **NOME UTENTE:** *specificare il nome utente per l'accesso*
- **PORT ip_address,port**: *specificare l'indirizzo IP e la porta dati client*

Questi comandi ASCII vengono usati internamente dal software client FTP NetX per eseguire operazioni FTP con il server FTP.

## <a name="ftp-server-responses"></a>Risposte del server FTP

Il server FTP usa la *nota porta TCP 21* per il campo Richieste di comando client. Quando il server FTP elabora il comando Client, restituisce una risposta numerica a 3 cifre in ASCII seguita da una stringa ASCII facoltativa. La risposta numerica viene usata dal software client FTP per determinare se l'operazione ha avuto esito positivo o negativo. Di seguito sono elencate varie risposte del server FTP ai comandi client:

### <a name="first-numeric-field-and-meaning"></a>Primo campo numerico e significato

- **1xx:** *stato preliminare positivo: è in arrivo un'altra risposta.*
- **2xx:** *stato di completamento positivo.*
- **3xx:** *stato preliminare positivo: è necessario inviare un altro comando.*
- **4xx:** *condizione di errore temporanea.*
- **5xx:** *condizione di errore.*

### <a name="second-numeric-field-and-meaning"></a>Secondo campo numerico e significato

- **x0x:** errore di sintassi nel comando.
- **x1x:** messaggio informativo.
- **x2x:** connessione correlata.
- **x3x:** autenticazione correlata.
- **x4x:** non specificato.
- **x5x:** correlato al file system.

Ad esempio, a una richiesta client di disconnessione di una connessione FTP con il comando QUIT viene in genere risposto con un codice "221" dal server, se la disconnessione ha esito positivo.

## <a name="ftp-passive-transfer-mode"></a>Modalità di trasferimento passivo FTP

Per impostazione predefinita, il client FTP NetX usa la modalità di trasporto attiva per scambiare dati sul socket di dati con il server FTP. Il problema di questa disposizione è che richiede al client FTP di aprire un socket del server TCP a cui connettersi al server FTP. Ciò rappresenta un possibile rischio per la sicurezza e può essere bloccato dal firewall client. La modalità di trasferimento passivo differisce dalla modalità di trasporto attiva in modo che il server FTP crei il socket del server TCP nella connessione dati. In questo modo si elimina il rischio di sicurezza (per il client FTP).

Per abilitare il trasferimento passivo dei dati, l'applicazione chiama nx_ftp_client_passive_mode_set *su* un client FTP creato in precedenza con il secondo argomento impostato su NX_TRUE. Successivamente, tutti i servizi client FTP NetX successivi per il trasferimento dei dati (NLST, RETR, STOR) vengono tentati in modalità di trasporto passivo.

Il client FTP invia prima il comando PASV (nessun argomento). Se il server FTP supporta questa richiesta, restituirà la risposta 227 "OK". Il client invia quindi la richiesta, ad esempio RETR. Se il server rifiuta la modalità di trasferimento passivo, il servizio Client FTP NetX restituisce uno stato di errore.

Per disabilitare la modalità di trasporto passivo  e tornare alla modalità di trasporto attiva, l'applicazione chiama nx_ftp_client_passive_mode_set con il secondo argomento impostato su NX_FALSE.

## <a name="ftp-communication"></a>Comunicazione FTP

Il server FTP usa la *nota porta TCP 21* per il campo Richieste client. I client FTP possono usare qualsiasi porta TCP disponibile. La sequenza generale di eventi FTP è la seguente:

### <a name="ftp-read-file-requests"></a>Richieste di file di lettura FTP

1. Problemi del client: TCP si connette alla porta 21 del server.
1. Il server invia una risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia una risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "PORT" con indirizzo IP e porta.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "RETR" con il nome file da leggere.
1. Il server crea un socket di dati e si connette alla porta dati client specificata nel comando "PORT".
1. Il server invia la risposta "125" all'avvio della lettura del file del segnale.
1. Il server invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene trasferito completamente.
1. Al termine, il server disconnette la connessione dati.
1. Il server invia la risposta "250" al segnale che la lettura del file ha esito positivo.
1. I client inviano "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" al segnale che la disconnessione ha esito positivo.
1. Il server disconnette la connessione FTP.

Come accennato in precedenza, l'unica differenza tra l'esecuzione di FTP su IPv4 e IPv6 è che il comando PORT viene sostituito con il comando EPRT per IPv6

Se il client FTP effettua una richiesta di lettura in modalità di trasferimento passivo, la sequenza di comando è la seguente **(** le righe in grassetto indicano un passaggio diverso dalla modalità di trasferimento attiva):

1. Problemi del client: TCP si connette alla porta 21 del server.
1. Il server invia una risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia una risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. **Il client invia il messaggio "PASV".**
1. **Il server invia la risposta "227" e l'indirizzo IP e la porta a cui il client deve connettersi per segnalare l'esito positivo.**
1. Il client invia il messaggio "RETR" con il nome file da leggere.
1. **Il server crea il socket del server dati e rimane in ascolto della richiesta di connessione client su questo socket usando la porta specificata nella risposta "227".**
1. **Il server invia una risposta "150" sul socket di controllo per segnalare che la lettura del file è stata avviata.**
1. Il server invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene trasferito completamente.
1. Al termine, il server disconnette la connessione dati.
1. **Il server invia la risposta "226" sul socket di controllo per segnalare che la lettura del file ha esito positivo.**
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" al segnale che la disconnessione ha esito positivo.
1. Il server disconnette la connessione FTP.

### <a name="ftp-write-requests"></a>Richieste di scrittura FTP

1. Problemi del client: TCP si connette alla porta 21 del server.
1. Il server invia una risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia una risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "PORT" con indirizzo IP e porta.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. Il client invia un messaggio "STOR" con il nome file da scrivere.
1. Il server crea un socket di dati e si connette alla porta dati client specificata nel comando "PORT".
1. Il server invia la risposta "125" al segnale che la scrittura del file è stata avviata.
1. Il client invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene trasferito completamente.
1. Al termine, il client disconnette la connessione dati.
1. Il server invia la risposta "250" al segnale che la scrittura del file ha esito positivo.
1. I client inviano "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" al segnale che la disconnessione ha esito positivo.
1. Il server disconnette la connessione FTP.

Se il client FTP effettua una richiesta di scrittura in modalità di trasferimento passivo, la sequenza di comando è la seguente **(** le righe in grassetto indicano un passaggio diverso dalla modalità di trasferimento attiva):

1. Problemi del client: TCP si connette alla porta 21 del server.
1. Il server invia una risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia una risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. **Il client invia il messaggio "PASV".**
1. **Il server invia la risposta "227" e l'indirizzo IP e la porta a cui il client deve connettersi per segnalare l'esito positivo.**
1. Il client invia un messaggio "STOR" con il nome file da scrivere.
1. **Il server crea il socket del server dati e rimane in ascolto della richiesta di connessione client su questo socket usando la porta specificata nella risposta "227".**
1. **Il server invia la risposta "150" sul socket di controllo per segnalare che la scrittura del file è stata avviata.**
1. Il client invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene trasferito completamente.
1. Al termine, il client disconnette la connessione dati.
1. **Il server invia la risposta "226" sul socket di controllo per segnalare che la scrittura del file ha esito positivo.**
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" al segnale che la disconnessione ha esito positivo.
1. Il server disconnette la connessione FTP.

## <a name="ftp-authentication"></a>FTP Authentication

Ogni volta che viene stabilita una connessione FTP, il client deve fornire al server un nome *utente* e una *password*. Alcuni siti FTP consentono ciò che viene chiamato *FTP anonimo,* che consente l'accesso FTP senza un nome utente e una password specifici. Per questo tipo di connessione, per nome utente deve essere specificato "anonimo" e la password deve essere un indirizzo di posta elettronica completo.

L'utente è responsabile della fornitura di NETX FTP con routine di autenticazione di accesso e disconnessione. Vengono forniti durante la funzione ***nx_ftp_server_create** _ e chiamati dall'elaborazione della password. Se la funzione _login* restituisce NX_SUCCESS, la connessione viene autenticata e sono consentite operazioni FTP. In caso contrario, se *la funzione di* accesso restituisce un valore diverso da NX_SUCCESS, il tentativo di connessione viene rifiutato.

## <a name="ftp-multi-thread-support"></a>Supporto multi-thread FTP

I servizi client FTP NetX possono essere chiamati contemporaneamente da più thread. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client FTP devono essere eseguite in sequenza dallo stesso thread.

## <a name="ftp-rfcs"></a>RFC FTP

NetX FTP è conforme a RFC959 e alle RFC correlate.