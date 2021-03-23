---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo FTP
description: Il File Transfer Protocol (FTP) è un protocollo progettato per i trasferimenti di file.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1d56b20b1c7d719d1b7d9c8c5b2fe234d5577da3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821890"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-ftp"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo FTP

Il File Transfer Protocol (FTP) è un protocollo progettato per i trasferimenti di file. FTP utilizza servizi di Transmission Control Protocol affidabili (TCP) per eseguire la relativa funzione di trasferimento file. Per questo motivo, FTP è un protocollo di trasferimento di file altamente affidabile. Anche FTP è a prestazioni elevate. Il trasferimento effettivo dei file FTP viene eseguito in una connessione FTP dedicata. NetX Duo FTP supporta le reti IPv4 e IPv6. IPv6 non modifica direttamente il protocollo FTP, sebbene alcune modifiche nell'API FTP NetX originale siano necessarie per supportare IPv6 e verranno descritte in questo documento.

## <a name="ftp-requirements"></a>Requisiti FTP

Per funzionare correttamente, il pacchetto FTP NetX richiede NetX Duo. L'applicazione host deve creare un'istanza IP per l'esecuzione di servizi NetX e le attività periodiche. Se l'applicazione host FTP viene eseguita su una rete IPv6, è necessario abilitare IPv6 e ICMPv6 nell'attività IP. TCP deve essere abilitato anche per le reti IPv6 o IPv4. L'applicazione host IPv6 deve impostare il linklocal e l'indirizzo IPv6 globale usando l'API IPv6 e/o DHCPv6. Un programma demo nella sezione "Small example System" del **capitolo 2** illustra come questa operazione viene eseguita.

Il client e il server FTP sono anche progettati per funzionare con FileX Embedded file system. Se FileX non è disponibile, lo sviluppatore dell'host può implementare o sostituire il proprio file system lungo le linee guida suggerite in filex_stub. h definendo ognuno dei servizi elencati nel file. Questo argomento viene descritto nelle sezioni successive di questa guida.

La parte client FTP del pacchetto FTP NetX non ha altri requisiti.

La parte relativa al server FTP del pacchetto FTP NetX presenta diversi requisiti aggiuntivi. Per prima cosa, è necessario l'accesso completo alla *porta 21 Nota* TCP per gestire tutte le richieste di comandi FTP client e la *porta 20 nota* per gestire tutti i trasferimenti di dati FTP del client.

## <a name="ftp-constraints"></a>Vincoli FTP

Lo standard FTP offre molte opzioni relative alla rappresentazione dei dati del file. NetX FTP non implementa opzioni switch, ad esempio ls – al. Il server FTP NetX prevede di ricevere le richieste e i relativi argomenti in un singolo pacchetto anziché in pacchetti consecutivi.

Analogamente alle implementazioni di UNIX, NetX FTP presuppone i vincoli di formato di file seguenti:

- Tipo di file: **Binary**
- Formato file: **solo non stampa**
- Struttura del file: **solo struttura di file**

## <a name="ftp-file-names"></a>Nomi file FTP

I nomi dei file FTP devono essere nel formato del file system di destinazione (in genere FileX). Devono essere stringhe ASCII con terminazione NULL, con informazioni complete sul percorso, se necessario. Non è previsto alcun limite per le dimensioni dei nomi file FTP nell'implementazione FTP NetX. Tuttavia, le dimensioni del payload del pool di pacchetti devono essere in grado di contenere il percorso e/o il nome di file massimo.

## <a name="ftp-client-commands"></a>Comandi client FTP

FTP dispone di un meccanismo semplice per l'apertura di connessioni e l'esecuzione di operazioni su file e directory. È fondamentalmente disponibile un set di comandi FTP standard emessi dal client dopo che una connessione è stata stabilita correttamente sulla *porta 21 TCP nota*. Di seguito sono riportati alcuni dei comandi FTP di base. Si noti che l'unica differenza quando FTP viene eseguito su IPv6 è che il comando PORT viene sostituito con il comando EPRT:

- Directory di *lavoro della modifica* del percorso CWD
- DELE filename *Delete nome file specificato*
- EPRT ip_address, porta *fornire l'indirizzo IPv6 e la porta dati client*
- *Modalità di trasferimento passivo della richiesta EPSV per IPv6*
- ELENCO di directory *Get* directory
- La directory MKD *Crea una nuova directory*
- *Visualizzazione* directory directory NLST
- NOOP *No Operation, restituisce Success*
- PASSA password *specificare la password per l'accesso*
- PASV *richiedere la modalità di trasferimento passivo per IPv4*
- Porta ip_address, porta *fornire l'indirizzo IP e la porta dati client*
- Percorso della *directory corrente del pickup* del percorso pwd
- USCIRE dalla *connessione client di terminazione*
- RETR nome *file specificato*
- Directory RMD *eliminazione directory specificata*
- RNFR OldFileName *specificare il file da rinominare*
- RNTO nomenuovofile *rinominare il file in un nome file specificato*
- Il *file specificato Write filename Write*
- TIPO *seleziono immagine file binario*
- Nome utente *specificare il nome utente per l'accesso*

Questi comandi ASCII vengono usati internamente dal software client FTP NetX per eseguire operazioni FTP con il server FTP.

## <a name="ftp-server-responses"></a>Risposte server FTP

Una volta che il server FTP elabora la richiesta client, restituisce una risposta codificata a 3 cifre in ASCII seguita da testo ASCII facoltativo. La risposta numerica viene utilizzata dal software client FTP per determinare se l'operazione ha avuto esito positivo o negativo. Nell'elenco seguente vengono illustrate le diverse risposte del server FTP alle richieste client:

**Primo significato campo numerico**

- *stato preliminare positivo 1xx: verrà inviata un'altra risposta*.
- *stato di completamento positivo* 2xx.
- *stato preliminare positivo 3xx: è necessario inviare un altro comando*.
- *condizione di errore temporaneo* 4xx.
- *condizione di errore 5xx.*

**Secondo significato del campo numerico**

- *errore di sintassi x0x nel comando*.
- *messaggio informativo* X1X.
- *connessione X2X correlata*.
- *correlato all'autenticazione* x3x.
- x4x non *specificato*.
- *correlato al file System* x5x.

Una richiesta client di disconnessione di una connessione FTP con il comando QUIT, ad esempio, viene in genere risposta con il codice "221" del server, se la disconnessione ha esito positivo.

## <a name="ftp-passive-transfer-mode"></a>Modalità di trasferimento passivo FTP

Per impostazione predefinita, il client FTP NetX Duo usa la modalità di trasporto attiva per scambiare dati sul socket di dati con il server FTP. Il problema di questa disposizione è che richiede al client FTP di aprire un socket del server TCP per il server FTP a cui connettersi. Questo rappresenta un possibile rischio per la sicurezza e può essere bloccato dal firewall client. La modalità di trasferimento passivo è diversa dalla modalità di trasporto attiva perché il server FTP crea il socket del server TCP sulla connessione dati. In questo modo si eliminano i rischi per la sicurezza (per il client FTP).

Per abilitare il trasferimento dati passivo, l'applicazione chiama *nx_ftp_client_passive_mode_set* su un client FTP creato in precedenza con il secondo argomento impostato su NX_TRUE. In seguito, tutti i servizi client FTP NetX Duo successivi per il trasferimento dei dati (NLST, RETR, STOR) vengono tentati nella modalità di trasporto passiva.

Il client FTP invia prima di tutto il comando passivo (senza argomenti), il comando PASV per il comando IPv4 o EPSV per IPv6. Se il server FTP supporta questa richiesta, restituirà la risposta 227 "OK" per PASV e la risposta 229 "OK" per EPSV. Quindi il client invia la richiesta, ad esempio RETR. Se il server rifiuta la modalità di trasferimento passivo, il servizio client FTP NetX Duo restituisce uno stato di errore.

Per disabilitare la modalità di trasporto passiva e tornare alla modalità di trasporto attiva, l'applicazione chiama *nx_ftp_client_passive_mode_set* con il secondo argomento impostato su NX_FALSE.

## <a name="ftp-communication"></a>Comunicazione FTP

Il server FTP utilizza la *porta TCP 21 Nota* per il campo delle richieste del client. I client FTP possono usare qualsiasi porta TCP disponibile. La sequenza generale degli eventi FTP è la seguente:

**Richieste di file di lettura FTP**:

1. Il client invia la connessione TCP alla porta del server 21.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia la risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. *Applicazioni IPv4*: il client invia il messaggio "porta" con indirizzo IP e porta.<br />*Applicazioni IPv6*: il client invia un messaggio "EPRT" con indirizzo IP e porta.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "RETR" con il nome del file da leggere.
1. Il server crea il socket di dati e si connette con la porta dati client specificata nel comando "porta".
1. Il server invia la risposta "125" alla lettura del file di segnale avviata.
1. Il server invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene completamente trasferito.
1. Al termine, il server disconnette la connessione dati.
1. Il server invia la risposta "250" alla lettura del file di segnale completata.
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" alla disconnessione del segnale riuscita.
1. Il server disconnette la connessione FTP.

Come indicato in precedenza, l'unica differenza tra FTP in esecuzione su IPv4 e

IPv6 è il comando porta sostituito con il comando EPRT per IPv6

Se il client FTP effettua una richiesta di lettura nella modalità di trasferimento passivo, la sequenza di comandi è la seguente (le linee in **grassetto** indicano un passaggio diverso rispetto alla modalità di trasferimento attiva):

1. Il client invia la connessione TCP alla porta del server 21.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia la risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. ***Applicazioni IPv4:* Il client invia il messaggio "PASV".**<br />**_Applicazioni IPv6:_ Il client invia il messaggio "EPSV".**
1. ***Applicazioni IPv4:* Il server invia la risposta "227", l'indirizzo IP e la porta a cui il client si connette per segnalare l'esito positivo.**<br />**_Applicazioni IPv6:_ Il server invia la risposta "229", l'indirizzo IP e la porta a cui il client si connette per segnalare l'esito positivo.**
1. Il client invia il messaggio "RETR" con il nome del file da leggere.
1. **Il server crea un socket del server di dati e rimane in attesa della richiesta di connessione del client su questo socket usando la porta specificata nella risposta nel passaggio 10.**
1. **Il server invia la risposta "150" sul socket di controllo per segnalare che la lettura del file è stata avviata.**
1. Il server invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene completamente trasferito.
1. Al termine, il server disconnette la connessione dati.
1. **Il server invia la risposta "226" sul socket di controllo per segnalare che la lettura del file è riuscita.**
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" alla disconnessione del segnale riuscita.
1. Il server disconnette la connessione FTP.

**Richieste di scrittura FTP**:

1. Il client invia la connessione TCP alla porta del server 21.
1. Il server invia la risposta "220" per segnalare l'esito positivo.
1. Il client invia il messaggio "USER" con "username".
1. Il server invia la risposta "331" per segnalare l'esito positivo.
1. Il client invia il messaggio "PASS" con "password".
1. Il server invia la risposta "230" per segnalare l'esito positivo.
1. Il client invia il messaggio "TYPE I" per il trasferimento binario.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. *Applicazioni IPv4*: il client invia il messaggio "porta" con indirizzo IP e porta.<br />*Applicazioni IPv6*: il client invia un messaggio "EPRT" con indirizzo IP e porta.
1. Il server invia la risposta "200" per segnalare l'esito positivo.
1. Il client invia il messaggio "STOR" con il nome file da scrivere.
1. Il server crea il socket di dati e si connette con la porta dati client specificata nel comando "EPRT" o "PORT" precedente.
1. Il server invia la risposta "125" alla scrittura del file di segnale avviata.
1. Il client invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene completamente trasferito.
1. Al termine, il client disconnette la connessione dati.
1. Il server invia la risposta "250" alla scrittura del file di segnale riuscita.
1. Il client invia "QUIT" per terminare la connessione FTP.
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
1. ***Applicazioni IPv4:* Il client invia il messaggio "PASV".**<br />**_Applicazioni IPv6:_ Il client invia il messaggio "EPSV".**
1. ***Applicazioni IPv4:* Il server invia la risposta "227", l'indirizzo IP e la porta a cui il client si connette per segnalare l'esito positivo.**<br />**_Applicazioni IPv6:_ Il server invia la risposta "229", l'indirizzo IP e la porta a cui il client si connette per segnalare l'esito positivo.**
1. Il client invia il messaggio "STOR" con il nome file da scrivere.
1. **Il server crea un socket del server di dati e rimane in attesa della richiesta di connessione del client su questo socket usando la porta specificata nella risposta nel passaggio 10.**
1. **Il server invia la risposta "150" sul socket di controllo per segnalare che la scrittura del file è stata avviata.**
1. Il client invia il contenuto del file tramite la connessione dati. Questo processo continua fino a quando il file non viene completamente trasferito.
1. Al termine, il client disconnette la connessione dati.
1. **Il server invia la risposta "226" sul socket di controllo per segnalare che la scrittura del file è riuscita.**
1. Il client invia "QUIT" per terminare la connessione FTP.
1. Il server invia la risposta "221" alla disconnessione del segnale riuscita.
1. Il server disconnette la connessione FTP.

## <a name="ftp-authentication"></a>FTP Authentication

Ogni volta che si verifica una connessione FTP, il client deve fornire al server un *nome utente* e una *password*. Alcuni siti FTP consentono il cosiddetto *FTP anonimo*, che consente l'accesso FTP senza un nome utente e una password specifici. Per questo tipo di connessione è necessario specificare "Anonymous" per il nome utente e la password deve essere un indirizzo di posta elettronica completo.

L'utente è responsabile della fornitura di NetX FTP con le routine di autenticazione per l'accesso e la disconnessione. Questi vengono forniti durante i servizi ***nxd_ftp_server_create** _ e _*_nx_ftp_server_create_*_ e chiamati dall'elaborazione della password. La differenza tra i due è la _*_nxd_ftp_server_create_*_ i puntatori della funzione di input per l'accesso e le funzioni di autenticazione di disconnessione prevedono il tipo di indirizzo NetX Duo _*_NXD_ADDRESS_*_. Questo tipo di dati include entrambi i formati di indirizzi IPv4 o IPv6, rendendo questa funzione il servizio "Duo" che supporta le reti IPv4 e IPv6. I puntatori a funzione di input _ *_nx_ftp_server_create_** per le funzioni di autenticazione login e logout prevedono un tipo di indirizzo IP ULONG. Questa funzione è limitata alle reti IPv4. Lo sviluppatore è invitato a usare il servizio "Duo" ogni volta che è possibile.

Se la funzione *login* restituisce NX_SUCCESS, la connessione viene autenticata e sono consentite operazioni FTP. In caso contrario, se la funzione *login* restituisce un valore diverso da NX_SUCCESS, il tentativo di connessione viene rifiutato.

## <a name="ftp-multi-thread-support"></a>Supporto multithreading FTP

I servizi client FTP NetX possono essere chiamati da più thread contemporaneamente. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client FTP devono essere eseguite in sequenza dallo stesso thread.

## <a name="ftp-rfcs"></a>RFC FTP

NetX Duo FTP è conforme a RFC 959, RFC 2428 e RFC correlate.
