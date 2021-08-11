---
title: Capitolo 1 - Introduzione a Azure RTOS FTP NetX Duo
description: Il File Transfer Protocol (FTP) è un protocollo progettato per i trasferimenti di file.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a36357ce486d5ba8a68b23c829de6c4b821dfb3cc62f47b0958ff32deaa2f7a7
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791296"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-ftp"></a>Capitolo 1 - Introduzione a Azure RTOS FTP NetX Duo

Il File Transfer Protocol (FTP) è un protocollo progettato per i trasferimenti di file. FTP usa servizi reliable Transmission Control Protocol (TCP) per eseguire la funzione di trasferimento file. Per questo scopo, FTP è un protocollo di trasferimento file altamente affidabile. Ftp offre anche prestazioni elevate. Il trasferimento effettivo di file FTP viene eseguito su una connessione FTP dedicata. NetX Duo FTP supporta sia le reti IPv4 che le reti IPv6. IPv6 non modifica direttamente il protocollo FTP, anche se alcune modifiche nell'API FTP NetX originale sono necessarie per supportare IPv6 e verranno descritte in questo documento.

## <a name="ftp-requirements"></a>Requisiti FTP

Per funzionare correttamente, il pacchetto FTP NetX richiede NetX Duo. L'applicazione host deve creare un'istanza IP per l'esecuzione di servizi NetX e attività periodiche. Se l'esecuzione dell'applicazione host FTP su una rete IPv6, IPv6 e ICMPv6 deve essere abilitata nell'attività IP. TCP deve essere abilitato anche per le reti IPv6 o IPv4. L'applicazione host IPv6 deve impostare il relativo indirizzo IPv6 locale di collegamento e globale usando l'API IPv6 e/o DHCPv6. Un programma demo nella sezione "Small Example System" nel **capitolo 2** illustra come eseguire questa operazione.

Il server FTP e il client sono progettati anche per funzionare con l'file system FileX. Se FileX non è disponibile, lo sviluppatore host può implementare o sostituire il proprio file system in base alle linee guida suggerite in filex_stub.h definendo ognuno dei servizi elencati in tale file. Questo argomento viene illustrato nelle sezioni successive di questa guida.

La parte client FTP del pacchetto FTP NetX non presenta altri requisiti.

La parte server FTP del pacchetto FTP NetX presenta diversi requisiti aggiuntivi. Prima di tutto, richiede l'accesso completo alla porta TCP *nota 21* per la gestione di tutte le richieste di comando FTP client e alla porta *20* nota per la gestione di tutti i trasferimenti di dati FTP client.

## <a name="ftp-constraints"></a>Vincoli FTP

Lo standard FTP include molte opzioni relative alla rappresentazione dei dati dei file. NetX FTP non implementa le opzioni switch, ad esempio ls –al. Il server FTP NetX prevede di ricevere richieste e i relativi argomenti in un singolo pacchetto anziché in pacchetti consecutivi.

Analogamente alle UNIX, Ftp NetX presuppone i vincoli di formato di file seguenti:

- Tipo di file: **Binario**
- Formato file: **solo non stampa**
- Struttura file: **solo struttura di file**

## <a name="ftp-file-names"></a>Nomi di file FTP

I nomi di file FTP devono essere nel formato del file system di destinazione (in genere FileX). Devono essere stringhe ASCII con terminazione NULL, con informazioni sul percorso completo, se necessario. Non è stato specificato alcun limite per le dimensioni dei nomi di file FTP nell'implementazione FTP NetX. Tuttavia, le dimensioni del payload del pool di pacchetti devono essere in grado di contenere il percorso massimo e/o il nome file.

## <a name="ftp-client-commands"></a>Comandi client FTP

FTP dispone di un meccanismo semplice per l'apertura delle connessioni e l'esecuzione di operazioni su file e directory. Esiste fondamentalmente un set di comandi FTP standard emessi dal client dopo che una connessione è stata stabilita correttamente sulla porta TCP *nota 21.* Di seguito sono illustrati alcuni comandi FTP di base. Si noti che l'unica differenza quando FTP viene eseguito su IPv6 è che il comando PORT viene sostituito con il comando EPRT:

- Percorso CWD *Modifica directory di lavoro*
- DELE filename *Elimina il nome file specificato*
- EPRT ip_address, porta *Specificare l'indirizzo IPv6 e la porta dati client*
- Modalità di trasferimento passivo richiesta EPSV *per IPv6*
- Elenco directory *Get directory listing*
- Directory MKD *Crea nuova directory*
- Elenco directory NLST *Get directory*
- NOOP *Nessuna operazione, restituisce l'esito positivo*
- PASS password *Specificare la password per l'accesso*
- Modalità di trasferimento passivo richiesta PASV *per IPv4*
- PORT ip_address,porta *Specificare l'indirizzo IP e la porta dati client*
- Percorso PWD *Percorso della directory corrente di prelievo*
- QUIT *Termina connessione client*
- RETR filename *Legge il file specificato*
- Directory RMD *Elimina la directory specificata*
- RNFR oldfilename *Specificare il file da rinominare*
- RNTO newfilename *Rinominare il file in nome file specificato*
- NOME FILE STOR *Scrivere il file specificato*
- TIPO I *Selezionare un'immagine di file binario*
- NOME UTENTE *Specificare il nome utente per l'accesso*

Questi comandi ASCII vengono usati internamente dal software client FTP NetX per eseguire operazioni FTP con il server FTP.

## <a name="ftp-server-responses"></a>Risposte del server FTP

Dopo che il server FTP ha elaborata la richiesta client, restituisce una risposta codificata a 3 cifre in ASCII seguita da testo ASCII facoltativo. La risposta numerica viene usata dal software client FTP per determinare se l'operazione ha avuto esito positivo o negativo. L'elenco seguente mostra varie risposte del server FTP alle richieste client:

**Significato del primo campo numerico**

- 1xx *Stato preliminare positivo: un'altra risposta in arrivo.*
- 2xx *Stato di completamento positivo.*
- 3xx *Stato preliminare positivo: è necessario inviare un altro comando.*
- 4xx *Condizione di errore temporanea*.
- Condizione di errore *5xx.*

**Significato del secondo campo numerico**

- Errore di *sintassi* x0x nel comando .
- x1x *Messaggio informativo*.
- x2x *Connection related*.
- x3x *Authentication related*.
- x4x *Non specificato.*
- x5x *File system correlato*.

Ad esempio, a una richiesta client di disconnessione di una connessione FTP con il comando QUIT viene in genere risposto con un codice "221" dal server, se la disconnessione ha esito positivo.

## <a name="ftp-passive-transfer-mode"></a>Modalità di trasferimento passivo FTP

Per impostazione predefinita, il client FTP NetX Duo usa la modalità di trasporto attiva per scambiare dati sul socket di dati con il server FTP. Il problema di questa disposizione è che richiede al client FTP di aprire un socket del server TCP a cui connettersi al server FTP. Ciò rappresenta un possibile rischio per la sicurezza e può essere bloccato dal firewall client. La modalità di trasferimento passivo differisce dalla modalità di trasporto attiva in modo che il server FTP crei il socket del server TCP nella connessione dati. In questo modo si elimina il rischio di sicurezza (per il client FTP).

Per abilitare il trasferimento passivo dei dati, l'applicazione chiama nx_ftp_client_passive_mode_set *su* un client FTP creato in precedenza con il secondo argomento impostato su NX_TRUE. Successivamente, tutti i successivi servizi client FTP NetX Duo per il trasferimento dei dati (NLST, RETR, STOR) vengono tentati in modalità di trasporto passivo.

Il client FTP invia prima il comando passivo (nessun argomento), il comando PASV per IPv4 o il comando EPSV per IPv6. Se il server FTP supporta questa richiesta, restituirà la risposta 227 "OK" per PASV e la risposta 229 "OK" per EPSV. Il client invia quindi la richiesta, ad esempio RETR. Se il server rifiuta la modalità di trasferimento passivo, il servizio client FTP NetX Duo restituisce uno stato di errore.

Per disabilitare la modalità di trasporto passivo  e tornare alla modalità di trasporto attiva, l'applicazione chiama nx_ftp_client_passive_mode_set con il secondo argomento impostato su NX_FALSE.

## <a name="ftp-communication"></a>Comunicazione FTP

Il server FTP usa la *nota porta TCP 21* per il campo Richieste client. I client FTP possono usare qualsiasi porta TCP disponibile. La sequenza generale di eventi FTP è la seguente:

**Richieste file di lettura FTP**:

1. Problemi del client: TCP si connette alla porta 21 del server.
1. Il server invia una risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia una risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. *Applicazioni IPv4:* il client invia un messaggio "PORT" con indirizzo IP e porta.<br />*Applicazioni IPv6:* il client invia un messaggio "EPRT" con indirizzo IP e porta.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. Il client invia un messaggio "RETR" con il nome file da leggere.
1. Il server crea un socket di dati e si connette alla porta dati del client specificata nel comando "PORT".
1. Il server invia la risposta "125" al segnale che la lettura del file è stata avviata.
1. Il server invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene trasferito completamente.
1. Al termine, il server disconnette la connessione dati.
1. Il server invia la risposta "250" al segnale che la lettura del file ha esito positivo.
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" per segnalare che la disconnessione è riuscita.
1. Il server disconnette la connessione FTP.

Come accennato in precedenza, l'unica differenza tra l'esecuzione di FTP su IPv4 e

IPv6 è il comando PORT sostituito con il comando EPRT per IPv6

Se il client FTP effettua una richiesta di lettura in modalità di trasferimento passiva, la sequenza di comando è la seguente **(** le righe in grassetto indicano un passaggio diverso dalla modalità di trasferimento attiva):

1. Il client esegue la connessione TCP alla porta 21 del server.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia una risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. ***Applicazioni IPv4:* Il client invia il messaggio "PASV".**<br />**_Applicazioni IPv6:_ Il client invia il messaggio "EPSV".**
1. ***Applicazioni IPv4:* Il server invia la risposta "227" e l'indirizzo IP e la porta a cui il client deve connettersi per segnalare l'esito positivo.**<br />**_Applicazioni IPv6:_ Il server invia la risposta "229" e l'indirizzo IP e la porta a cui il client deve connettersi per segnalare l'esito positivo.**
1. Il client invia un messaggio "RETR" con il nome file da leggere.
1. **Il server crea il socket del server dati ed è in ascolto della richiesta di connessione client su questo socket usando la porta specificata nella risposta nel passaggio 10.**
1. **Il server invia la risposta "150" sul socket di controllo per segnalare che la lettura del file è stata avviata.**
1. Il server invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene trasferito completamente.
1. Al termine, il server disconnette la connessione dati.
1. **Il server invia la risposta "226" sul socket di controllo per segnalare che la lettura del file ha esito positivo.**
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" per segnalare che la disconnessione è riuscita.
1. Il server disconnette la connessione FTP.

**Richieste di scrittura FTP:**

1. Il client esegue la connessione TCP alla porta 21 del server.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia una risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. *Applicazioni IPv4:* il client invia un messaggio "PORT" con indirizzo IP e porta.<br />*Applicazioni IPv6:* il client invia un messaggio "EPRT" con indirizzo IP e porta.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "STOR" con il nome file da scrivere.
1. Il server crea un socket di dati e si connette alla porta dati client specificata nel comando "EPRT" o "PORT" precedente.
1. Il server invia la risposta "125" al segnale che la scrittura del file è stata avviata.
1. Il client invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene trasferito completamente.
1. Al termine, il client disconnette la connessione dati.
1. Il server invia la risposta "250" per segnalare che la scrittura del file ha esito positivo.
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" per segnalare che la disconnessione è riuscita.
1. Il server disconnette la connessione FTP.

Se il client FTP effettua una richiesta di scrittura in modalità di trasferimento passiva, la sequenza di comando è la seguente **(** le righe in grassetto indicano un passaggio diverso dalla modalità di trasferimento attiva):

1. Il client esegue la connessione TCP alla porta 21 del server.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia una risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia una risposta "200" per segnalare l'esito positivo.
1. ***Applicazioni IPv4:* Il client invia il messaggio "PASV".**<br />**_Applicazioni IPv6:_ Il client invia il messaggio "EPSV".**
1. ***Applicazioni IPv4:* Il server invia la risposta "227" e l'indirizzo IP e la porta a cui il client deve connettersi per segnalare l'esito positivo.**<br />**_Applicazioni IPv6:_ Il server invia la risposta "229" e l'indirizzo IP e la porta a cui il client deve connettersi per segnalare l'esito positivo.**
1. Il client invia il messaggio "STOR" con il nome file da scrivere.
1. **Il server crea il socket del server dati ed è in ascolto della richiesta di connessione client su questo socket usando la porta specificata nella risposta nel passaggio 10.**
1. **Il server invia una risposta "150" sul socket di controllo per segnalare che la scrittura del file è stata avviata.**
1. Il client invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene trasferito completamente.
1. Al termine, il client disconnette la connessione dati.
1. **Il server invia la risposta "226" sul socket di controllo per segnalare che la scrittura del file ha esito positivo.**
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" per segnalare che la disconnessione è riuscita.
1. Il server disconnette la connessione FTP.

## <a name="ftp-authentication"></a>FTP Authentication

Ogni volta che viene stabilita una connessione FTP, il client deve fornire al server un nome *utente e* una *password.* Alcuni siti FTP consentono il cosiddetto *FTP anonimo,* che consente l'accesso FTP senza un nome utente e una password specifici. Per questo tipo di connessione, è necessario che per il nome utente sia specificato "anonymous" e che la password sia un indirizzo di posta elettronica completo.

L'utente è responsabile di fornire a NETX FTP le routine di autenticazione di accesso e disconnessione. Questi vengono forniti durante l'nxd_ftp_server_create ***** e i _*_nx_ftp_server_create_*_ e vengono chiamati dall'elaborazione della password. La differenza tra i due è che i puntatori nxd_ftp_server_create _*_funzione_*_ di input per l'accesso e l'autenticazione di disconnessione prevedono che il tipo di indirizzo NetX Duo _*_NXD_ADDRESS_*_. Questo tipo di dati contiene sia i formati di indirizzo IPv4 che IPv6, rendendo questa funzione il servizio "duo" che supporta le reti IPv4 e IPv6. I puntatori *_a funzione di_* input _ nx_ftp_server_create * per le funzioni di accesso e di autenticazione di disconnessione prevedono il tipo di indirizzo IP ULONG. Questa funzione è limitata alle reti IPv4. Lo sviluppatore è invitato a usare il servizio "duo" quando possibile.

Se la *funzione login* restituisce NX_SUCCESS, la connessione viene autenticata e le operazioni FTP sono consentite. In caso contrario, se *la funzione login* restituisce un valore diverso NX_SUCCESS, il tentativo di connessione viene rifiutato.

## <a name="ftp-multi-thread-support"></a>Supporto multi-thread FTP

I servizi client FTP NetX possono essere chiamati contemporaneamente da più thread. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client FTP devono essere eseguite in sequenza dallo stesso thread.

## <a name="ftp-rfcs"></a>RFC FTP

NetX Duo FTP è conforme a RFC 959, RFC 2428 e alle RFC correlate.
