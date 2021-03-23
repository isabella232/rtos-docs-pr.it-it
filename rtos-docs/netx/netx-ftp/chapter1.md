---
title: Capitolo 1-Introduzione ad Azure RTO NetX FTP
description: Il File Transfer Protocol (FTP) è un protocollo progettato per i trasferimenti di file. FTP utilizza servizi di Transmission Control Protocol affidabili (TCP) per eseguire la relativa funzione di trasferimento file.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 86e132daf96f9039631234f10c8e239b61ad5126
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822637"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-ftp"></a>Capitolo 1-Introduzione ad Azure RTO NetX FTP

Il File Transfer Protocol (FTP) è un protocollo progettato per i trasferimenti di file. FTP utilizza servizi di Transmission Control Protocol affidabili (TCP) per eseguire la relativa funzione di trasferimento file. Per questo motivo, FTP è un protocollo di trasferimento di file altamente affidabile. Anche FTP è a prestazioni elevate. Il trasferimento effettivo dei file FTP viene eseguito in una connessione FTP dedicata.

## <a name="ftp-requirements"></a>Requisiti FTP

Per funzionare correttamente, il pacchetto FTP NetX di Azure RTO richiede che sia già stata creata un'istanza IP NetX. Inoltre, è necessario abilitare TCP nella stessa istanza di IP. La parte client FTP del pacchetto FTP NetX non ha altri requisiti.

La parte relativa al server FTP del pacchetto FTP NetX presenta diversi requisiti aggiuntivi. Per prima cosa, è necessario l'accesso completo alla *porta 21 Nota* TCP per gestire tutte le richieste di comandi FTP client e la *porta 20 nota* per gestire tutti i trasferimenti di dati FTP del client. Il server FTP è anche progettato per l'uso con FileX Embedded file system. Se FileX non è disponibile, l'utente può trasferire le parti di FileX utilizzate nel proprio ambiente. Questo argomento viene descritto nelle sezioni successive di questa guida.

## <a name="ftp-constraints"></a>Vincoli FTP

Lo standard FTP offre molte opzioni relative alla rappresentazione dei dati del file. Analogamente alle implementazioni di UNIX, NetX FTP presuppone i vincoli di formato di file seguenti:

- Tipo di file: **Binary**
- Formato file: **solo non stampa**
- Struttura del file: **solo struttura di file**
- Modalità di trasmissione: **solo modalità flusso**

## <a name="ftp-file-names"></a>Nomi file FTP

I nomi dei file FTP devono essere nel formato del file system di destinazione (in genere FileX). Devono essere stringhe ASCII con terminazione NULL, con informazioni complete sul percorso, se necessario. Non è previsto alcun limite per le dimensioni dei nomi file FTP nell'implementazione FTP NetX. Tuttavia, le dimensioni del payload del pool di pacchetti devono essere in grado di contenere il percorso e/o il nome di file massimo.

## <a name="ftp-client-commands"></a>Comandi client FTP

FTP dispone di un meccanismo semplice per l'apertura di connessioni e l'esecuzione di operazioni su file e directory. È fondamentalmente disponibile un set di comandi FTP standard emessi dal client dopo che una connessione è stata stabilita correttamente sulla *porta 21 TCP nota*. Di seguito sono riportati alcuni dei comandi FTP di base:

### <a name="ftp-command-and-meaning"></a>Comando e significato FTP

- **Percorso CWD**: *modifica directory di lavoro*
- **Dele filename**: *eliminare il nome file specificato*
- **Elenco directory**: *Ottieni visualizzazione directory*
- **Directory MKD**: *Crea nuova directory*
- **NLST directory**: *Ottieni visualizzazione directory*
- **NoOp**: *Nessuna operazione, restituisce esito positivo*
- **Pass password**: *specificare la password per l'accesso*
- **PASV**: *richiedere la modalità di trasferimento passivo*
- **Percorso pwd**: *percorso della directory corrente del prelievo*
- **Quit**: *Termina connessione client*
- **Retr nomefile**: *lettura file specificato*
- **RMD directory**: *eliminare la directory specificata*
- **RNFR OldFileName**: *specificare il file da rinominare*
- **RNTO nomenuovofile**: *rinominare il file in un nome file specificato*
- **Stor filename**: *Scrivi file specificato*
- **Tipo I**: *selezionare l'immagine del file binario*
- **Nome utente utente**: *specificare il nome utente per l'accesso*
- Porta **ip_address, porta**: *specificare l'indirizzo IP e la porta dati client*

Questi comandi ASCII vengono usati internamente dal software client FTP NetX per eseguire operazioni FTP con il server FTP.

## <a name="ftp-server-responses"></a>Risposte server FTP

Il server FTP utilizza la *Nota porta TCP 21* per il campo richieste del comando client. Una volta che il server FTP elabora il comando client, viene restituita una risposta numerica a 3 cifre in ASCII seguita da una stringa ASCII facoltativa. La risposta numerica viene utilizzata dal software client FTP per determinare se l'operazione ha avuto esito positivo o negativo. Di seguito sono elencate diverse risposte al server FTP per i comandi client:

### <a name="first-numeric-field-and-meaning"></a>Primo campo numerico e significato

- **1xx**: *stato preliminare positivo: verrà inviata un'altra risposta*.
- **2xx**: *stato di completamento positivo*.
- **3xx**: *stato preliminare positivo: è necessario inviare un altro comando*.
- **4xx**: *condizione di errore temporanea*.
- **5xx**: *condizione di errore.*

### <a name="second-numeric-field-and-meaning"></a>Secondo campo numerico e significato

- **x0x**: errore di sintassi nel comando.
- **X1X**: messaggio informativo.
- **X2X**: connessione correlata.
- **x3x**: correlato all'autenticazione.
- **x4x**: non specificato.
- **x5x**: correlato al file System.

Una richiesta client di disconnessione di una connessione FTP con il comando QUIT, ad esempio, viene in genere risposta con il codice "221" del server, se la disconnessione ha esito positivo.

## <a name="ftp-passive-transfer-mode"></a>Modalità di trasferimento passivo FTP

Per impostazione predefinita, il client FTP NetX usa la modalità di trasporto attiva per scambiare dati sul socket di dati con il server FTP. Il problema di questa disposizione è che richiede al client FTP di aprire un socket del server TCP per il server FTP a cui connettersi. Questo rappresenta un possibile rischio per la sicurezza e può essere bloccato dal firewall client. La modalità di trasferimento passivo è diversa dalla modalità di trasporto attiva perché il server FTP crea il socket del server TCP sulla connessione dati. In questo modo si eliminano i rischi per la sicurezza (per il client FTP).

Per abilitare il trasferimento dati passivo, l'applicazione chiama *nx_ftp_client_passive_mode_set* su un client FTP creato in precedenza con il secondo argomento impostato su NX_TRUE. In seguito, tutti i servizi client FTP NetX successivi per il trasferimento dei dati (NLST, RETR, STOR) vengono tentati nella modalità di trasporto passiva.

Il client FTP invia prima il comando PASV (nessun argomento). Se il server FTP supporta questa richiesta, restituirà la risposta 227 "OK". Quindi il client invia la richiesta, ad esempio RETR. Se il server rifiuta la modalità di trasferimento passivo, il servizio client FTP NetX restituisce uno stato di errore.

Per disabilitare la modalità di trasporto passiva e tornare alla modalità di trasporto attiva, l'applicazione chiama *nx_ftp_client_passive_mode_set* con il secondo argomento impostato su NX_FALSE.

## <a name="ftp-communication"></a>Comunicazione FTP

Il server FTP utilizza la *porta TCP 21 Nota* per il campo delle richieste del client. I client FTP possono usare qualsiasi porta TCP disponibile. La sequenza generale degli eventi FTP è la seguente:

### <a name="ftp-read-file-requests"></a>Richieste di file di lettura FTP

1. Il client invia la connessione TCP alla porta del server 21.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia la risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "porta" con indirizzo IP e porta.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "RETR" con il nome del file da leggere.
1. Il server crea il socket di dati e si connette con la porta dati client specificata nel comando "porta".
1. Il server invia la risposta "125" alla lettura del file di segnale avviata.
1. Il server invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene completamente trasferito.
1. Al termine, il server disconnette la connessione dati.
1. Il server invia la risposta "250" alla lettura del file di segnale completata.
1. I client inviano "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" alla disconnessione del segnale riuscita.
1. Il server disconnette la connessione FTP.

Come indicato in precedenza, l'unica differenza tra l'FTP in esecuzione su IPv4 e IPv6 è il comando PORT viene sostituito con il comando EPRT per IPv6

Se il client FTP effettua una richiesta di lettura nella modalità di trasferimento passivo, la sequenza di comandi è la seguente (le linee in **grassetto** indicano un passaggio diverso rispetto alla modalità di trasferimento attiva):

1. Il client invia la connessione TCP alla porta del server 21.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia la risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. **Il client invia il messaggio "PASV".**
1. **Il server invia la risposta "227", l'indirizzo IP e la porta a cui il client si connette per segnalare l'esito positivo.**
1. Il client invia il messaggio "RETR" con il nome del file da leggere.
1. **Il server crea un socket del server di dati e rimane in attesa della richiesta di connessione del client su questo socket usando la porta specificata nella risposta "227".**
1. **Il server invia la risposta "150" sul socket di controllo per segnalare che la lettura del file è stata avviata.**
1. Il server invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene completamente trasferito.
1. Al termine, il server disconnette la connessione dati.
1. **Il server invia la risposta "226" sul socket di controllo per segnalare che la lettura del file è riuscita.**
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" alla disconnessione del segnale riuscita.
1. Il server disconnette la connessione FTP.

### <a name="ftp-write-requests"></a>Richieste di scrittura FTP

1. Il client invia la connessione TCP alla porta del server 21.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia la risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "porta" con indirizzo IP e porta.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "STOR" con il nome file da scrivere.
1. Il server crea il socket di dati e si connette con la porta dati client specificata nel comando "porta".
1. Il server invia la risposta "125" alla scrittura del file di segnale avviata.
1. Il client invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene completamente trasferito.
1. Al termine, il client disconnette la connessione dati.
1. Il server invia la risposta "250" alla scrittura del file di segnale riuscita.
1. I client inviano "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" alla disconnessione del segnale riuscita.
1. Il server disconnette la connessione FTP.

Se il client FTP effettua una richiesta di scrittura nella modalità di trasferimento passivo, la sequenza di comandi è la seguente (le linee in **grassetto** indicano un passaggio diverso rispetto alla modalità di trasferimento attiva):

1. Il client invia la connessione TCP alla porta del server 21.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia la risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. **Il client invia il messaggio "PASV".**
1. **Il server invia la risposta "227", l'indirizzo IP e la porta a cui il client si connette per segnalare l'esito positivo.**
1. Il client invia il messaggio "STOR" con il nome file da scrivere.
1. **Il server crea un socket del server di dati e rimane in attesa della richiesta di connessione del client su questo socket usando la porta specificata nella risposta "227".**
1. **Il server invia la risposta "150" sul socket di controllo per segnalare che la scrittura del file è stata avviata.**
1. Il client invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene completamente trasferito.
1. Al termine, il client disconnette la connessione dati.
1. **Il server invia la risposta "226" sul socket di controllo per segnalare che la scrittura del file è riuscita.**
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" alla disconnessione del segnale riuscita.
1. Il server disconnette la connessione FTP.

## <a name="ftp-authentication"></a>FTP Authentication

Ogni volta che si verifica una connessione FTP, il client deve fornire al server un *nome utente* e una *password*. Alcuni siti FTP consentono il cosiddetto *FTP anonimo*, che consente l'accesso FTP senza un nome utente e una password specifici. Per questo tipo di connessione è necessario specificare "Anonymous" per il nome utente e la password deve essere un indirizzo di posta elettronica completo.

L'utente è responsabile della fornitura di NetX FTP con le routine di autenticazione per l'accesso e la disconnessione. Questi vengono forniti durante la funzione ***nx_ftp_server_create** _ e vengono chiamati dall'elaborazione della password. Se la funzione _login * restituisce NX_SUCCESS, la connessione viene autenticata e sono consentite operazioni FTP. In caso contrario, se la funzione *login* restituisce un valore diverso da NX_SUCCESS, il tentativo di connessione viene rifiutato.

## <a name="ftp-multi-thread-support"></a>Supporto multithreading FTP

I servizi client FTP NetX possono essere chiamati da più thread contemporaneamente. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client FTP devono essere eseguite in sequenza dallo stesso thread.

## <a name="ftp-rfcs"></a>RFC FTP

L'FTP NetX è conforme a RFC959 e alle RFC correlate.