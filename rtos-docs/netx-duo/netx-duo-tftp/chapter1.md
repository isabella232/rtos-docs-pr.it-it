---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo TFTP
description: Il Trivial File Transfer Protocol (TFTP) è un protocollo leggero progettato per i trasferimenti di file.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4431b23e143d05214090547e7f179a6f5def8217
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821614"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-tftp"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo TFTP 

Il Trivial File Transfer Protocol (TFTP) è un protocollo leggero progettato per i trasferimenti di file. A differenza dei protocolli più affidabili, TFTP non esegue un controllo degli errori esteso e può anche avere prestazioni limitate perché si tratta di un protocollo di arresto e attesa. Dopo l'invio di un pacchetto di dati TFTP, il mittente attende che un ACK venga restituito dal destinatario. Sebbene questo sia semplice, limita la velocità effettiva complessiva di TFTP. Il pacchetto TFTP consente agli host di usare il protocollo TFTP su reti IP.

## <a name="tftp-requirements"></a>Requisiti TFTP

Per funzionare correttamente, la parte client TFTP del pacchetto TFTP NetX Duo richiede che sia già stata creata un'istanza IP. Inoltre, è necessario abilitare UDP nella stessa istanza di IP. La parte client del pacchetto TFTP NetX Duo non ha altri requisiti.

La parte relativa al server TFTP del pacchetto TFTP NetX Duo presenta diversi requisiti aggiuntivi. Per prima cosa, è necessario l'accesso completo alla *porta UDP ben nota 69* per la gestione di tutte le richieste TFTP del client. Il server TFTP è anche progettato per l'uso con FileX Embedded file system. Se FileX non è disponibile, l'utente può trasferire le parti di FileX utilizzate nel proprio ambiente. Questo argomento viene descritto nelle sezioni successive di questa guida.

## <a name="tftp-file-names"></a>Nomi file TFTP 

I nomi di file TFTP devono essere nel formato del file system di destinazione. Devono essere stringhe ASCII con terminazione NULL, con informazioni complete sul percorso, se necessario. Non esiste alcun limite specificato nelle dimensioni dei nomi file TFTP nell'implementazione TFTP NetX Duo.

## <a name="tftp-messages"></a>Messaggi TFTP

TFTP dispone di un meccanismo molto semplice per l'apertura, la lettura, la scrittura e la chiusura di file. Sono sostanzialmente presenti 2-4 byte di intestazione TFTP sotto l'intestazione UDP. La definizione del file TFTP i messaggi aperti presenta il formato seguente:

**oooof... f0OCTET0**

Dove:

- campo opcode a 2 byte **oooo**  
0x0001-> aperto per la lettura  
0x0002-> aperto per la scrittura

- **f...** campo del nome file f n-byte

- carattere di terminazione NULL a 0 1 byte

- **Ottetto** "Ottetto" ASCII per specificare il trasferimento binario

- carattere di terminazione NULL a 0 1 byte

La definizione dei messaggi TFTP Write, ACK e Error è leggermente diversa e viene definita nel modo seguente:

**oooobbbbd... d**

Dove:

- campo opcode a 2 byte **oooo**  
0x0003-pacchetto di dati >  
0x0004-ACK > per l'ultima lettura  
0x0005-condizione di errore >  

- **bbbb** 2-campo numero blocco byte (1-n)

- **d...** campo dati d n byte


- 0x0001 (lettura) nome file 0 ottetto 0

- 0x0002 (Write) nome file 0 ottetto 0

## <a name="tftp-communication"></a>Comunicazione TFTP

I server TFTP utilizzano la porta UDP 69 nota per ascoltare le richieste dei client. I socket client TFTP possono essere associati a qualsiasi porta UDP disponibile. Il payload del pacchetto di dati che contiene il file da caricare o scaricare viene inviato in blocchi di 512 byte, fino all'ultimo pacchetto che contiene < 512 byte. Pertanto, un pacchetto contenente meno di 512 byte segnala la fine del file. La sequenza generale degli eventi è la seguente:

Richieste di file di lettura TFTP:

1.  Il client invia una richiesta di apertura per la lettura con il nome del file e attende una risposta dal server.

2.  Il server invia i primi 512 byte del file o meno se le dimensioni del file sono inferiori a 512 byte.

3.  Il client riceve i dati, invia un ACK e attende il pacchetto successivo dal server per i file che contengono più di 512 byte.

4.  La sequenza termina quando il client riceve un pacchetto contenente meno di 512 byte.

Richieste di scrittura TFTP:

1.  Il client invia una richiesta di "apertura per la scrittura" con il nome del file e attende un ACK con un numero di blocco pari a 0 dal server.

2.  Quando il server è pronto per la scrittura del file, invia un ACK con un numero di blocco pari a zero.

3.  Il client invia al server i primi 512 byte del file (o meno per i file con una quantità inferiore a 512 byte) e attende la restituzione di un ACK.

4.  Il server invia un ACK dopo la scrittura dei byte.

5.  La sequenza termina quando il client completa la scrittura di un pacchetto contenente meno di 512 byte.
 

## <a name="tftp-server-session-timer"></a>Timer sessione server TFTP

Il server TFTP ha un numero limitato di slot di richiesta client. Se una sessione client sembra essere eliminata, lo slot non può essere disponibile per il riutilizzo. Tuttavia, se l'opzione NX_TFTP_SERVER_RETRANSMIT_ENABLE è abilitata, il server TFTP NetX duo crea un timer di sessione che monitora il timeout in ogni sessione client. Quando il timeout di una sessione scade, viene terminato e tutti i file aperti vengono chiusi. Quindi, lo slot diventa disponibile per un'altra richiesta client TFTP.

Per impostare il timeout, modificare l'opzione di configurazione NX_TFTP_SERVER_RETRANSMIT_TIMEOUT che, per impostazione predefinita, è 200 cicli del timer. Per impostazione predefinita, l'intervallo tra i timeout di sessione controllati viene impostato dal NX_TFTP_SERVER_TIMEOUT_PERIOD, ovvero 20 cicli del timer.

Quando il client TFTP ha caricato i file (scritti) nel supporto TFTP FileX, è necessario scaricare il supporto in modo che i dati possano essere scritti dal disco RAM del server TFTP nei supporti sottostanti (memoria disco del client TFTP). Questa operazione può essere eseguita utilizzando il servizio fx_media_flush se l'applicazione non desidera chiudere il server TFTP.

Tuttavia, dopo aver chiuso il server TFTP, l'applicazione dovrebbe, se non è più usata per il supporto FileX, quindi chiudere i supporti usando il servizio fx_media_close. In questo modo i dati dei file vengono scaricati nel disco del client TFTP, vengono chiusi i file aperti e aggiornati le informazioni della directory nel supporto.

La sezione "piccolo esempio" di questo capitolo illustra questa operazione.

Una terza opzione per l'aggiornamento del supporto FileX consiste nel compilare la libreria FileX con le opzioni FX_FAULT_TOLERANT o FX_FAULT_TOLERANT_DATA invece di usare i servizi FileX in modo esplicito. Se definito, FileX passa automaticamente le richieste di scrittura al driver multimediale. Queste opzioni possono limitare le prestazioni, ma offrire una maggiore protezione da dati di file persi o cluster persi. Per ulteriori informazioni su questo e FileX in generale, vedere la guida per l'utente di FileX per la logica rapida.

## <a name="tftp-multi-thread-support"></a>Supporto TFTP per più thread

I servizi client TFTP NetX Duo possono essere chiamati da più thread contemporaneamente. Tuttavia, le richieste di lettura o scrittura per un'istanza del client TFTP specifica devono essere eseguite in sequenza dallo stesso thread.

## <a name="tftp-rfcs"></a>RFC TFTP

NetX Duo TFTP è conforme a RFC1350 e alle RFC correlate.

