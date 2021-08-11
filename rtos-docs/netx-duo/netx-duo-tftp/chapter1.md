---
title: Capitolo 1 - Introduzione a Azure RTOS NetX Duo TFTP
description: Il Trivial File Transfer Protocol (TFTP) è un protocollo leggero progettato per i trasferimenti di file.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4854f96d8f230d7c1f21700ac731d6430854a950009d3ed51fbf90d37885f255
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791976"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-tftp"></a>Capitolo 1 - Introduzione a Azure RTOS NetX Duo TFTP 

Il Trivial File Transfer Protocol (TFTP) è un protocollo leggero progettato per i trasferimenti di file. A differenza dei protocolli più affidabili, TFTP non esegue un controllo completo degli errori e può anche avere prestazioni limitate perché è un protocollo di arresto e attesa. Dopo l'invio di un pacchetto di dati TFTP, il mittente attende che un ACK sia restituito dal destinatario. Sebbene sia semplice, limita la velocità effettiva TFTP complessiva. Il pacchetto TFTP consente agli host di usare il protocollo TFTP su reti IP.

## <a name="tftp-requirements"></a>Requisiti di TFTP

Per funzionare correttamente, la parte client TFTP del pacchetto NetX Duo TFTP richiede che sia già stata creata un'istanza IP. Inoltre, UDP deve essere abilitato nella stessa istanza IP. La parte Client del pacchetto NetX Duo TFTP non presenta altri requisiti.

La parte del server TFTP del pacchetto NetX Duo TFTP presenta diversi requisiti aggiuntivi. In primo luogo, è necessario l'accesso completo alla porta nota UDP *69* per la gestione di tutte le richieste TFTP del client. Il server TFTP è progettato anche per l'uso con l'file system FileX incorporato. Se FileX non è disponibile, l'utente può convertire le parti di FileX usate nel proprio ambiente. Questo argomento viene illustrato nelle sezioni successive di questa guida.

## <a name="tftp-file-names"></a>Nomi di file TFTP 

I nomi di file TFTP devono essere nel formato dell'file system. Devono essere stringhe ASCII con terminazione NULL, con informazioni sul percorso completo, se necessario. Non è previsto alcun limite per le dimensioni dei nomi di file TFTP nell'implementazione TFTP di NetX Duo.

## <a name="tftp-messages"></a>Messaggi TFTP

Il TFTP ha un meccanismo molto semplice per l'apertura, la lettura, la scrittura e la chiusura dei file. Ci sono fondamentalmente 2-4 byte di intestazione TFTP sotto l'intestazione UDP. La definizione dei messaggi aperti del file TFTP ha il formato seguente:

**oooof... f0OCTET0**

Dove:

- Campo opcode a 2 byte **oooo**  
0x0001 -> open per la lettura  
0x0002 -> Open for write

- **f... Campo f** n-byte Filename

- 0 carattere di terminazione NULL a 1 byte

- **OTTETTO** ASCII "OCTET" per specificare il trasferimento binario

- 0 carattere di terminazione NULL a 1 byte

La definizione dei messaggi di scrittura, ACK e di errore TFTP è leggermente diversa e viene definita come segue:

**oooobbbbd... D**

Dove:

- Campo opcode a 2 byte **oooo**  
0x0003 -> pacchetto dati  
0x0004 -> ACK per l'ultima lettura  
0x0005 -> condizione di errore  

- **bbbb** Campo Numero blocco a 2 byte (1-n)

- **d... d** campo dati a n byte


- 0x0001 (lettura) Nome file 0 OCTET 0

- 0x0002 (scrittura) Nome file 0 OCTET 0

## <a name="tftp-communication"></a>Comunicazione TFTP

I server TFTP utilizzano la nota porta UDP 69 per restare in ascolto delle richieste client. I socket client TFTP possono essere associati a qualsiasi porta UDP disponibile. Il payload del pacchetto di dati contenente il file da caricare o scaricare viene inviato in blocchi di 512 byte, fino all'ultimo pacchetto contenente < 512 byte. Di conseguenza, un pacchetto contenente meno di 512 byte segnala la fine del file. La sequenza generale di eventi è la seguente:

Richieste di file di lettura TFTP:

1.  Il client ea una richiesta "Apri per lettura" con il nome del file e attende una risposta dal server.

2.  Il server invia i primi 512 byte del file o meno se le dimensioni del file sono inferiori a 512 byte.

3.  Il client riceve i dati, invia un ACK e attende il pacchetto successivo dal server per i file contenenti più di 512 byte.

4.  La sequenza termina quando il client riceve un pacchetto contenente meno di 512 byte.

Richieste di scrittura TFTP:

1.  Il client ea una richiesta "Open for Write" con il nome del file e attende un ACK con un numero di blocco 0 dal server.

2.  Quando il server è pronto per scrivere il file, invia un ACK con un numero di blocco pari a zero.

3.  Il client invia i primi 512 byte del file (o meno per i file inferiori a 512 byte) al server e attende un ACK indietro.

4.  Il server invia un ACK dopo la scrittura dei byte.

5.  La sequenza termina quando il client completa la scrittura di un pacchetto contenente meno di 512 byte.
 

## <a name="tftp-server-session-timer"></a>Timer sessione server TFTP

Il server TFTP ha un numero limitato di slot di richieste client. Se una sessione client sembra essere eliminata, tale slot non può essere disponibile per il nuovo uso. Se tuttavia l'NX_TFTP_SERVER_RETRANSMIT_ENABLE è abilitata, il server NetX Duo TFTP crea un timer di sessione che monitora il timeout in ognuna delle sessioni client. Quando scade un timeout di sessione, viene terminato e tutti i file aperti vengono chiusi. Lo "slot" diventa quindi disponibile per un'altra richiesta client TFTP.

Per impostare il timeout, modificare l'opzione di configurazione NX_TFTP_SERVER_RETRANSMIT_TIMEOUT che per impostazione predefinita è 200 tick timer. L'intervallo tra i quali vengono controllati i timeout di sessione viene impostato dal NX_TFTP_SERVER_TIMEOUT_PERIOD che è 20 tick timer per impostazione predefinita.

Quando il client TFTP ha caricato (scritto) file nel supporto FileX TFTP, il supporto deve essere scaricato in modo che i dati possano essere scritti dal disco ram del server TFTP al supporto sottostante (memoria del disco del client TFTP). Questa operazione può essere eseguita usando fx_media_flush servizio se l'applicazione non vuole chiudere il server TFTP.

Tuttavia, dopo aver chiuso il server TFTP, l'applicazione deve, se non ha più uso per il supporto FileX, chiudere il supporto usando il fx_media_close locale. In questo modo i dati dei file verranno scaricati nuovamente sul disco del client TFTP, verranno chiuso i file aperti e le informazioni della directory verranno aggiornate nel supporto.

La sezione "Piccolo esempio" di questo capitolo ne illustra la procedura.

Una terza opzione per aggiornare il supporto FileX è compilare la libreria FileX con le opzioni FX_FAULT_TOLERANT o FX_FAULT_TOLERANT_DATA anziché usare i servizi FileX in modo esplicito. Se definito, FileX passa automaticamente le richieste di scrittura al driver multimediale. Queste opzioni possono limitare le prestazioni, ma offrono una maggiore protezione dai dati dei file persi o dai cluster persi. Per altre informazioni su questo e Su FileX in generale, vedere il Manuale dell'utente di Express Logic FileX.

## <a name="tftp-multi-thread-support"></a>Supporto multi-thread TFTP

I servizi client NetX Duo TFTP possono essere chiamati contemporaneamente da più thread. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client TFTP devono essere eseguite in sequenza dallo stesso thread.

## <a name="tftp-rfcs"></a>RFC TFTP

NetX Duo TFTP è conforme a RFC1350 e alle RFC correlate.

