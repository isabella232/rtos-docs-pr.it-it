---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo SNTP
description: Azure RTO NetX Simple Network Time Protocol (SNTP) è un protocollo progettato per sincronizzare gli orologi in Internet.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b3e1170197c6c4981060459104da80e354fac5db
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821656"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-sntp"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo SNTP 

Azure RTO NetX Simple Network Time Protocol (SNTP) è un protocollo progettato per sincronizzare gli orologi in Internet. SNTP versione 4 è un protocollo semplificato basato sul protocollo NTP (Network Time Protocol). USA i servizi UDP (User Datagram Protocol) per eseguire gli aggiornamenti temporali in un protocollo semplice e senza stato. Sebbene non sia complesso come NTP, SNTP è altamente affidabile e accurato. Nella maggior parte dei casi di Internet di oggi, SNTP offre un'accuratezza di 1-50 millisecondi, a seconda delle caratteristiche dei percorsi di origine e di rete della sincronizzazione. SNTP offre molte opzioni per garantire l'affidabilità della ricezione degli aggiornamenti temporali. Possibilità di passare a server alternativi, applicando gli algoritmi di polling e l'individuazione automatica del server ora, solo alcuni dei modi in cui un client SNTP gestisce un ambiente del servizio di tempo Internet variabile. Ciò che manca in precisione è costituito dalla semplicità e dalla facilità di implementazione. SNTP è concepito principalmente per fornire meccanismi completi per accedere ai servizi di diffusione di ora e frequenza nazionali (ad esempio, server NTP).

## <a name="netx-duo-sntp-client-requirements"></a>Requisiti del client NetX Duo SNTP

Il client NetX Duo SNTP richiede che sia già stata creata un'istanza IP. Inoltre, è necessario abilitare UDP nella stessa istanza IP e avere accesso alla porta *nota* 123 per inviare i dati temporali a un server SNTP, anche se le porte alternative funzioneranno. I client broadcast devono associare la porta UDP su cui è in corso l'invio del server di trasmissione, in genere 123. L'applicazione client NetX Duo SNTP deve avere uno o più indirizzi IP SNTP server.

## <a name="netx-duo-sntp-client-limitations"></a>Limitazioni di NetX Duo SNTP client 

La precisione nella rappresentazione dell'ora locale negli aggiornamenti del tempo NTP gestiti dall'API client SNTP è limitata alla risoluzione dei millisecondi.

Il client SNTP dispone solo di un singolo indirizzo del server di SNTP in qualsiasi momento. Se il server non risulta più valido, l'applicazione deve arrestare l'attività client SNTP e reinizializzarla con un altro indirizzo del server SNTP, usando la comunicazione broadcast o unicast SNTP.

Il client SNTP non supporta manycast.

NetX Duo SNTP client non supporta i meccanismi di autenticazione per la verifica dei dati di pacchetti ricevuti.

## <a name="netx-duo-sntp-client-operation"></a>Operazione client NetX Duo SNTP

RFC 4330 consiglia di usare i client di SNTP solo nel primo strato della rete locale e preferibilmente nelle configurazioni in cui nessun client NTP o SNTP è dipendente dalla sincronizzazione. Il livello di strato riflette la posizione dell'host nella gerarchia del tempo NTP in cui lo strato 1 è il livello più alto (un server radice) e 15 è il livello più basso consentito (ad esempio, client). Lo strato minimo predefinito del client SNTP è 2.

Il client NetX Duo SNTP può funzionare in una delle due modalità di base, unicast o broadcast, per ottenere tempo su Internet. In modalità unicast, il client esegue il polling del server SNTP a intervalli regolari e attende la ricezione di una risposta da tale server. Quando ne viene ricevuta una, il client verifica che la risposta contenga un aggiornamento dell'ora valido applicando un set di ' verifiche di integrità' consigliate da RFC 4330. Il client applica quindi la differenza di tempo, se presente, con l'orologio del server al proprio orologio locale. In modalità broadcast il client ascolta solo le trasmissioni di aggiornamento del tempo e mantiene il proprio orologio locale dopo aver applicato un set di controlli di integrità per verificare i dati relativi all'ora di aggiornamento. I controlli di integrità sono descritti in dettaglio nella sezione **controlli di integrità di SNTP** riportata di seguito.

Prima che il client possa essere eseguito in una delle due modalità, deve stabilirne i parametri operativi. Questa operazione viene eseguita chiamando rispettivamente *nx_sntp_client_initialize_unicast* o *nx_sntp_client_initialize_broadcast* per le modalità unicast o broadcast. Queste funzioni impostano i timeout per un intervallo di tempo massimo senza un aggiornamento valido, il limite per gli aggiornamenti consecutivi non validi ricevuti, un intervallo di polling per la modalità unicast, la modalità operativa, ad esempio unicast rispetto a broadcast e il server SNTP.

Se viene superato il limite massimo di tempo o di aggiornamenti non validi ricevuti, il client SNTP continua a essere eseguito, ma imposta lo stato corrente del server SNTP su non valido. L'applicazione può eseguire il polling del client SNTP usando il servizio *nx_sntp_client_receiving_updates* per verificare che il server SNTP stia ancora inviando aggiornamenti validi. In caso contrario, deve arrestare il thread del client SNTP usando il servizio *nx_sntp_client_stop* e chiamare uno dei due servizi Initialize per impostare un altro indirizzo del server SNTP. Per riavviare il client SNTP, l'applicazione chiama *nx_sntp_client_run_broadcast* o *nx_sntp_client_run_unicast*. Si noti che l'applicazione può modificare la modalità operativa del client SNTP nella chiamata di inizializzazione per passare a unicast o broadcast nel modo desiderato.

### <a name="local-clock-operation"></a>Operazione Clock locale

Il tempo di SNTP basato sul numero di secondi sul clock NTP master o sul numero di secondi trascorsi nel primo periodo NTP, ad esempio dal 1 gennaio **1900 00:00:00 al** 1 ° gennaio **1999 00:00:00**. Il significato di 01-01-1999 era quello in cui si è verificato l'ultimo salto. Questo valore viene definito come segue:

\#definire NTP_SECONDS_AT_01011999 0xBA368E80

Prima di eseguire il client SNTP, l'applicazione può facoltativamente inizializzare l'ora locale del client SNTP per il client da usare come tempo di riferimento. A tale scopo, è necessario usare il servizio *nx_sntp_client_set_local_time* . Questa operazione richiede l'ora in formato NTP, secondi e frazione, dove frazioni è il millisecondo nel tempo di riduzione del NTP. Idealmente l'applicazione può ottenere un SNTP tempo da un'origine indipendente. Non è disponibile alcuna API per la conversione di anno, mese, data e ora in un'ora NTP nel client NetX Duo SNTP. Per una descrizione del formato dell'ora NTP, vedere *RFC4330 "Simple Network Time Protocol (SNTP) versione 4 per IPv4, IPv6 e OSI".*

Se non viene specificata un'ora locale di base all'avvio del client di SNTP, il client di SNTP accetterà gli aggiornamenti di SNTP senza confrontare l'ora locale al primo aggiornamento. Successivamente, verranno applicati i valori massimo e minimo di aggiornamento del tempo per determinare se verrà modificata l'ora locale.

Per ottenere l'ora locale del client SNTP, l'applicazione può usare il servizio *nx_sntp_client_get_local_time_extended* .

### <a name="sntp-sanity-checks"></a>Controlli di integrità SNTP 

Il client esamina il pacchetto in ingresso per i criteri seguenti:

  - L'indirizzo IP di origine deve corrispondere all'indirizzo IP del server corrente.

  - La porta di origine del mittente deve corrispondere alla porta di origine del server corrente.

  - La lunghezza del pacchetto deve essere la lunghezza minima per contenere un messaggio di ora SNTP.

Successivamente, i dati relativi all'ora vengono estratti dal buffer dei pacchetti a cui il client applica una serie di "verifiche di integrità" specifiche:

  - L'indicatore Leap impostato su 3 indica che il server non è sincronizzato. Il client deve tentare di trovare un server alternativo.

  - Un campo strato impostato su zero è noto come un pacchetto di un bacio di morte (codice di esempio). Il gestore di codice del client SMTP per questa situazione è un callback definito dall'utente. Il piccolo file demo di esempio contiene un semplice gestore di codice per questa situazione. Il campo ID di riferimento contiene facoltativamente un codice che indica il motivo della risposta di codice. In ogni caso, il gestore di codice deve indicare come gestire la ricezione di un bacio di morte dal server SNTP. In genere è necessario reinizializzare il client SNTP con un altro server SNTP.

  - La versione, lo strato e la modalità di funzionamento del server SNTP devono corrispondere al servizio client.

  - Se il client è configurato con un valore massimo di dispersione di clock del server, il client controlla la dispersione di clock del server al primo aggiornamento ricevuto e, se supera il numero massimo, il client rifiuta il server.

  - I campi timestamp del server devono anche superare controlli specifici. Per il server unicast, tutti i campi temporali devono essere compilati e non possono essere NULL. Il timestamp di origine deve corrispondere all'indicatore di tempo di trasmissione nella richiesta del messaggio SNTP Time del client. In questo modo si protegge il client da intrusioni dannose e dal comportamento dei server non autorizzati. Il server di broadcast deve compilare solo il timestamp di trasmissione. Poiché non riceve nulla dal client, non ha alcun campo Receive o origination da compilare.

    Una verifica di integrità non riuscita i marchi aggiornano l'ora come aggiornamento ora non valido. Il servizio verifica integrità client SNTP tiene traccia del numero di aggiornamenti temporali non validi consecutivi ricevuti dallo stesso server.

Quando l'attività thread client di SNTP verifica la validità di un pacchetto SNTP per l'applicazione al tempo locale del client SNTP, incrementa il conteggio del client SNTP `nx_sntp_client_invalid_time_updates.` . viene inoltre restituito lo stato di errore al chiamante, ma si tratta di un'elaborazione interna che non è immediatamente visibile all'applicazione. Per rilevare gli aggiornamenti in caso di errore, è possibile eseguire una query sul valore del client SNTP `nx_sntp_client_invalid_time_updates` dopo aver ricevuto gli aggiornamenti dell'ora del server di SNTP.

Se l'aggiornamento temporale del server supera i controlli di integrità, il client tenta di elaborare i dati temporali nell'ora locale. Se il client è configurato per round trip calcolo, ad esempio il tempo di invio di una richiesta di aggiornamento al momento della ricezione, viene calcolato il tempo di round trip. Questo valore è dimezzato e quindi aggiunto all'ora del server.

Se quindi si tratta del primo aggiornamento ricevuto dal server SNTP corrente, il client SNTP determina se ignorare la differenza tra l'ora locale del server e del client. In seguito, tutti gli aggiornamenti dal server SNTP vengono valutati in base alla differenza con l'ora locale del client.

La differenza tra il client e l'ora del server viene confrontata con `NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT` . Se supera questo valore, i dati vengono eliminati. Se la differenza è inferiore `NX_SNTP_CLIENT_MIN_TIME_ADJUSTMENT` a, la differenza viene considerata troppo piccola per richiedere la regolazione.

Passando tutti questi controlli, l'aggiornamento ora viene applicato al client SNTP con alcune correzioni per i ritardi nell'elaborazione client SNTP interna.

### <a name="sntp-asynchronous-unicast-requests"></a>Richieste unicast asincrone SNTP 

Il client SNTP consente all'applicazione host di inviare in modo asincrono una richiesta unicast per l'ora corrente dal server NTP.

```C
UINT _nx_sntp_client_request_unicast_time(
NX_SNTP_CLIENT *client_ptr, 
UINT wait_option)
```

L'opzione Wait è la scadenza per l'attesa di una risposta.

Se il server NTP risponde, il pacchetto viene sottoposto alla stessa elaborazione e ai controlli di integrità, come descritto nella sezione precedente, prima di aggiornare l'ora locale del client SNTP.

Se la chiamata restituisce un esito positivo, l'applicazione può chiamare *nx_sntp_client_utility_display_date_time* o *nx_sntp_client_get_local_time_extended* per l'ora locale aggiornata.

Queste richieste unicast non interferiscono con la normale pianificazione client di SNTP per l'invio della richiesta unicast successiva o in modalità broadcast, quando si prevede la successiva trasmissione NTP.

### <a name="periodic-local-time-updates"></a>Aggiornamenti periodici dell'ora locale

La regolazione massima dell'ora locale è impostata nell'opzione NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT (in millisecondi). L'intervallo di aggiornamento di polling per le operazioni client unicast SNTP è impostato nell'opzione NX_SNTP_CLIENT_UNICAST_POLL_INTERVAL (in secondi). Se l'intervallo di polling è maggiore della regolazione massima, gli aggiornamenti successivi del server dopo l'aggiornamento del primo server verranno rifiutati. Per evitare che ciò accada, il client SNTP aggiornerà l'ora locale definita periodicamente come NX_SNTP_UPDATE_TIMEOUT_INTERVAL. 

Se c'è una differenza di tempo tra l'RTC in bacheca e l'ora del server (che l'ora locale del client di SNTP deve essere impostata su), il RTC deve essere sincronizzato con il tempo client di SNTP (non viene illustrato in questo manuale dell'utente).

Poiché gli aggiornamenti del server SNTP non devono essere eseguiti più spesso di una volta all'ora, non è utile eseguire il polling del client di SNTP per gli aggiornamenti del server o lo stato del server più spesso. Tuttavia, il client di SNTP deve aggiornare il clock locale abbastanza spesso da non superare il parametro di regolazione del tempo massimo NX_SNTP_CLIENT_MAX_TIME_LAPSE.

In alternativa, il NX_SNTP_CLIENT_MAX_TIME_LAPSE di regolazione massima può essere impostato su un valore maggiore rispetto all'aggiornamento di polling unicast (o a intervalli di trasmissione previsti). Il secondo Elimina la necessità di un clock in tempo reale indipendente. Tuttavia, l'intento del protocollo SNTP è evitare la dipendenza totale dagli aggiornamenti locali dell'RTC o della rete. Inoltre, gli aggiornamenti del server SNTP sono destinati a impedire la deriva nell'orologio orario locale.

## <a name="multiple-network-interfaces"></a>Più interfacce di rete

NetX Duo SNTP client può essere configurato per l'esecuzione in reti secondarie purché tali reti siano registrate con l'istanza IP. Per ulteriori informazioni su come registrare le reti secondarie, vedere il manuale dell'utente di NetX Duo o NetX.

Nella chiamata *nx_sntp_client_create* impostare il terzo input, iface_index, sull'indice della rete per il client SNTP per la ricezione degli aggiornamenti temporali in. L'interfaccia primaria è sempre in corrispondenza dell'indice 0. NetX Duo SNTP client non può supportare gli aggiornamenti temporali simultaneamente su più interfacce di rete.

## <a name="sntp-and-ntp-rfcs"></a>RFC SNTP e NTP

NetX Duo SNTP client è conforme a RFC4330 "Simple Network Time Protocol (SNTP) versione 4 per IPv4, IPv6 e OSI" e RFC correlati.