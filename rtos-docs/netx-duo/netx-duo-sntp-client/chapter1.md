---
title: Capitolo 1 - Introduzione a Azure RTOS NetX Duo SNTP
description: Il Azure RTOS NetX Simple Network Time Protocol (SNTP) è un protocollo progettato per sincronizzare gli orologi su Internet.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a284871d8da9b8d6d220e962de5d27483dafab201b68d64d5c794c1edab50153
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798827"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-sntp"></a>Capitolo 1 - Introduzione a Azure RTOS NetX Duo SNTP 

Il Azure RTOS NetX Simple Network Time Protocol (SNTP) è un protocollo progettato per sincronizzare gli orologi su Internet. SNTP versione 4 è un protocollo semplificato basato sul protocollo NTP (Network Time Protocol). Usa i servizi UDP (User Datagram Protocol) per eseguire aggiornamenti temporati in un semplice protocollo senza stato. Anche se non è complesso come NTP, SNTP è altamente affidabile e accurato. Nella maggior parte dei siti Internet di oggi, SNTP offre una velocità di 1-50 millisecondi, a seconda delle caratteristiche dei percorsi di rete e di origine della sincronizzazione. SNTP offre molte opzioni per garantire l'affidabilità della ricezione degli aggiornamenti in tempo. La possibilità di passare a server alternativi, l'applicazione di algoritmi di back-off di polling e l'individuazione automatica del server ora sono solo alcuni dei mezzi per un client SNTP per gestire un ambiente del servizio ora Internet variabile. Ciò che manca di precisione costituisce per semplicità e semplicità di implementazione. SNTP è destinato principalmente a fornire meccanismi completi per accedere ai servizi nazionali di diffusione di ora e frequenza (ad esempio, server NTP).

## <a name="netx-duo-sntp-client-requirements"></a>Requisiti client SNTP di NetX Duo

Il client SNTP di NetX Duo richiede che sia già stata creata un'istanza IP. Inoltre, UDP deve essere abilitato nella stessa istanza IP  e deve avere accesso alla porta nota 123 per l'invio di dati temporici a un server SNTP, anche se anche le porte alternative funzioneranno. I client broadcast devono associare la porta UDP su cui il server di trasmissione invia, in genere 123. L'applicazione client NetX Duo SNTP deve avere uno o più indirizzi del server SNTP IP.

## <a name="netx-duo-sntp-client-limitations"></a>Limitazioni del client SNTP di NetX Duo 

La precisione nella rappresentazione dell'ora locale negli aggiornamenti dell'ora NTP gestiti dall'API client SNTP è limitata alla risoluzione in millisecondi.

Il client SNTP contiene un solo indirizzo del server SNTP in qualsiasi momento. Se tale server sembra non essere più valido, l'applicazione deve arrestare l'attività client SNTP e reinizializzarla con un altro indirizzo del server SNTP, usando la comunicazione SNTP broadcast o unicast.

Il client SNTP non supporta manycast.

Il client SNTP di NetX Duo non supporta i meccanismi di autenticazione per la verifica dei dati dei pacchetti ricevuti.

## <a name="netx-duo-sntp-client-operation"></a>Operazione client NetX Duo SNTP

RFC 4330 consiglia ai client SNTP di operare solo al livello più alto della rete locale e preferibilmente nelle configurazioni in cui nessun client NTP o SNTP dipende per la sincronizzazione. Il livello di strato riflette la posizione host nella gerarchia temporale NTP in cui il livello 1 è il livello più alto (un server di riferimento ora radice) e 15 è il livello più basso consentito (ad esempio Client). Lo strato minimo predefinito del client SNTP è 2.

Il client NetX Duo SNTP può operare in una delle due modalità di base, unicast o broadcast, per ottenere tempo su Internet. In modalità unicast, il client esegue il polling del server SNTP a intervalli regolari e attende di ricevere una risposta da tale server. Quando ne viene ricevuto uno, il client verifica che la risposta contenga un aggiornamento dell'ora valido applicando un set di "controlli di integrità" consigliati da RFC 4330. Il client applica quindi la differenza di ora, se presente, con l'orologio del server all'orologio locale. In modalità broadcast, il client rimane semplicemente in ascolto delle trasmissioni di aggiornamento dell'ora e mantiene l'orologio locale dopo l'applicazione di un set simile di controlli di integrità per verificare i dati relativi all'ora di aggiornamento. I controlli di integrità sono descritti in dettaglio nella sezione **SNTP Sanity Checks** riportata di seguito.

Prima che il client possa essere eseguito in entrambe le modalità, deve stabilire i parametri operativi. Questa operazione viene eseguita chiamando *nx_sntp_client_initialize_unicast* o *nx_sntp_client_initialize_broadcast* per le modalità unicast o broadcast, rispettivamente. Queste funzioni servono a impostare i timeout per la scadenza massima del tempo senza un aggiornamento valido, il limite per gli aggiornamenti non validi consecutivi ricevuti, un intervallo di polling per la modalità unicast, la modalità operazione, ad esempio unicast rispetto alla trasmissione e il server SNTP.

Se viene superato il limite di tempo massimo o il numero massimo di aggiornamenti non validi ricevuti, il client SNTP continua a essere eseguito ma imposta lo stato corrente del server SNTP su non valido. L'applicazione può eseguire il polling del client SNTP usando *il servizio nx_sntp_client_receiving_updates* per verificare che il server SNTP invii ancora aggiornamenti validi. In caso contrario, deve arrestare il thread client SNTP usando il *servizio nx_sntp_client_stop* e chiamare uno dei due servizi di inizializzazione per impostare un altro indirizzo del server SNTP. Per riavviare il client SNTP, l'applicazione chiama *nx_sntp_client_run_broadcast* o *nx_sntp_client_run_unicast*. Si noti che l'applicazione può modificare la modalità operativa del client SNTP nella chiamata di inizializzazione per passare alla modalità unicast o broadcast in base alle esigenze.

### <a name="local-clock-operation"></a>Operazione dell'orologio locale

Tempo SNTP in base al numero di secondi nell'orologio NTP master o al numero di secondi trascorsi nel primo periodo NTP, ad esempio dal 1° gennaio **1900 00:00:00** al 1 gennaio **1999 00:00:00**. Il significato di 01-01-1999 è stato quando si è verificato l'ultimo secondo intercalare. Questo valore è definito nel modo seguente:

\#definire NTP_SECONDS_AT_01011999 0xBA368E80

Prima dell'esecuzione del client SNTP, l'applicazione può inizializzare facoltativamente l'ora locale del client SNTP per il client da usare come ora di base. A tale scopo, deve usare il *nx_sntp_client_set_local_time* servizio. Questa operazione richiede il tempo in formato NTP, secondi e frazioni, dove frazione è il millisecondo nel tempo condensato NTP. Idealmente l'applicazione può ottenere un'ora SNTP da un'origine indipendente. Non è disponibile alcuna API per la conversione di anno, mese, data e ora in un'ora NTP nel client NetX Duo SNTP. Per una descrizione del formato ora NTP, vedere *RFC4330 "Simple Network Time Protocol (SNTP) Version 4 for IPv4, IPv6 and OSI".*

Se all'avvio del client SNTP non viene specificata alcuna ora locale di base, il client SNTP accetterà gli aggiornamenti SNTP senza confrontarlo con l'ora locale al primo aggiornamento. Successivamente, applierà i valori di aggiornamento dell'ora massima e minima per determinare se ne modificherà l'ora locale.

Per ottenere l'ora locale del client SNTP, l'applicazione può usare il *nx_sntp_client_get_local_time_extended* locale.

### <a name="sntp-sanity-checks"></a>Controlli di integrità SNTP 

Il client esamina il pacchetto in ingresso per i criteri seguenti:

  - L'indirizzo IP di origine deve corrispondere all'indirizzo IP del server corrente.

  - La porta di origine del mittente deve corrispondere alla porta di origine del server corrente.

  - La lunghezza del pacchetto deve essere la lunghezza minima per contenere un messaggio di ora SNTP.

Successivamente, i dati relativi all'ora vengono estratti dal buffer di pacchetti a cui il client applica quindi un set di controlli di integrità specifici:

  - L'indicatore leap impostato su 3 indica che il server non è sincronizzato. Il client deve tentare di trovare un server alternativo.

  - Un campo di stratum impostato su zero è noto come pacchetto Di bacia della morte (KOD). Il gestore KOD del client SMTP per questa situazione è un callback definito dall'utente. Il piccolo file demo di esempio contiene un semplice gestore KOD per questa situazione. Il campo REFERENCE ID (ID riferimento) contiene facoltativamente un codice che indica il motivo della risposta kod. In ogni caso, il gestore KOD deve indicare come gestire la ricezione di un bacio di morte dal server SNTP. In genere sarà necessario reinizializzare il client SNTP con un altro server SNTP.

  - La versione SNTP del server, lo strato e la modalità di funzionamento devono essere abbinati al servizio Client.

  - Se il client è configurato con un valore massimo di dispersione dell'orologio del server, il client controlla la dispersione dell'orologio del server solo al primo aggiornamento ricevuto e, se supera il valore massimo del client, il client rifiuta il server.

  - Anche i campi timestamp server devono superare controlli specifici. Per il server unicast, tutti i campi relativi all'ora devono essere compilati e non possono essere NULL. Il timestamp di origine deve essere uguale al timestamp di trasmissione nella richiesta del messaggio di ora SNTP del client. In questo modo il client viene protetto da intrusi dannosi e da comportamenti server non autorizzati. Il server di trasmissione deve compilare solo il timestamp di trasmissione. Poiché non riceve alcun valore dal client, non ha campi di ricezione o di origine da compilare.

    Un controllo dell'autenticità non riuscito marchia un aggiornamento dell'ora come aggiornamento dell'ora non valido. Il servizio di controllo dell'autenticità del client SNTP tiene traccia del numero di aggiornamenti di tempo non validi consecutivi ricevuti dallo stesso server.

Quando l'attività del thread del client SNTP controlla la validità di un pacchetto SNTP per l'applicazione all'ora locale del client SNTP, incrementa il conteggio del client SNTP Restituisce anche uno stato di errore al chiamante, ma si tratta di tutta l'elaborazione interna, quindi non è immediatamente visibile `nx_sntp_client_invalid_time_updates.` all'applicazione. Il modo per rilevare gli aggiornamenti dell'ora non riusciti è eseguire una query sul valore del client SNTP dopo aver ricevuto gli aggiornamenti dell'ora `nx_sntp_client_invalid_time_updates` del server SNTP.

Se l'aggiornamento dell'ora del server supera i controlli di integrità, il client tenta di elaborare i dati dell'ora all'ora locale. Se il client è configurato per il calcolo round trip, ad esempio il tempo di invio di una richiesta di aggiornamento al momento in cui ne viene ricevuta una, viene calcolato il round trip tempo. Questo valore viene dimezzato e quindi aggiunto all'ora del server.

Successivamente, se si tratta del primo aggiornamento ricevuto dal server SNTP corrente, il client SNTP determina se deve ignorare la differenza tra l'ora locale del server e quella del client. Successivamente, tutti gli aggiornamenti dal server SNTP vengono valutati per la differenza con l'ora locale del client.

La differenza tra l'ora client e quella del server viene confrontata con `NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT` . Se supera questo valore, i dati vengono generati. Se la differenza è minore della differenza, viene considerata `NX_SNTP_CLIENT_MIN_TIME_ADJUSTMENT` troppo piccola per richiedere la rettifica.

Passando tutti questi controlli, l'aggiornamento dell'ora viene quindi applicato al client SNTP con alcune correzioni per i ritardi nell'elaborazione interna del client SNTP.

### <a name="sntp-asynchronous-unicast-requests"></a>Richieste unicast asincrone SNTP 

Il client SNTP consente all'applicazione host di inviare in modo asincrono una richiesta unicast per l'ora corrente dal server NTP.

```C
UINT _nx_sntp_client_request_unicast_time(
NX_SNTP_CLIENT *client_ptr, 
UINT wait_option)
```

L'opzione wait è la scadenza per l'attesa di una risposta.

Se il server NTP risponde, il pacchetto viene sottoposto agli stessi controlli di elaborazione e integrità come descritto nella sezione precedente prima di aggiornare l'ora locale del client SNTP.

Se la chiamata restituisce il completamento corretto, l'applicazione può chiamare nx_sntp_client_utility_display_date_time *o* *nx_sntp_client_get_local_time_extended* per l'ora locale aggiornata.

Queste richieste unicast non interferiscono con la normale pianificazione del client SNTP per l'invio della richiesta unicast successiva o, se in modalità broadcast, quando prevedere la trasmissione NTP successiva.

### <a name="periodic-local-time-updates"></a>Aggiornamenti periodici dell'ora locale

La regolazione massima dell'ora locale viene impostata nell'opzione NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT (in millisecondi). L'intervallo di aggiornamento di polling per le operazioni client SNTP unicast viene impostato nell'opzione NX_SNTP_CLIENT_UNICAST_POLL_INTERVAL (in secondi). Se l'intervallo di polling è maggiore della regolazione massima, gli aggiornamenti successivi del server dopo il primo aggiornamento del server verranno rifiutati. Per evitare questo problema, il client SNTP aggiornerà periodicamente l'ora locale definita come NX_SNTP_UPDATE_TIMEOUT_INTERVAL. 

Se c'è una differenza di tempo tra l'ora dell'rtc sulla scheda e l'ora del server (su cui deve essere impostata l'ora locale del client SNTP), l'rtc deve essere sincronizzato con l'ora del client SNTP (non è illustrato in questo Manuale dell'utente).

Poiché gli aggiornamenti del server SNTP non devono essere eseguiti più di una volta all'ora, non è utile eseguire il polling del client SNTP per gli aggiornamenti del server o lo stato del server più spesso. Tuttavia, il client SNTP deve aggiornare l'orologio locale abbastanza spesso da non andare oltre il parametro di regolazione dell'ora massimo NX_SNTP_CLIENT_MAX_TIME_LAPSE.

In alternativa, la regolazione NX_SNTP_CLIENT_MAX_TIME_LAPSE può essere impostata su maggiore dell'aggiornamento di polling unicast (o su intervalli di trasmissione previsti). Quest'ultimo elimina la necessità di un orologio in tempo reale indipendente. L'intenzione del protocollo SNTP, tuttavia, è evitare la totale affidamento sugli aggiornamenti dell'ora di rete o dell'ora locale. Inoltre, gli aggiornamenti del server SNTP hanno lo scopo di evitare la deriva nell'orologio locale.

## <a name="multiple-network-interfaces"></a>Più interfacce di rete

Il client SNTP di NetX Duo può essere configurato per l'esecuzione su reti secondarie, purché tali reti siano registrate con l'istanza IP. Per altre informazioni su come registrare le reti secondarie, vedere il Manuale dell'utente di NetX Duo o NetX.

Nella chiamata *nx_sntp_client_create* impostare il terzo input, iface_index, sull'indice della rete su cui il client SNTP deve ricevere gli aggiornamenti dell'ora. L'interfaccia primaria è sempre in corrispondenza dell'indice 0. Il client NetX Duo SNTP non può supportare contemporaneamente gli aggiornamenti dell'ora su più interfacce di rete.

## <a name="sntp-and-ntp-rfcs"></a>RFC SNTP e NTP

Il client NetX Duo SNTP è conforme a RFC4330 "Simple Network Time Protocol (SNTP) Versione 4 per IPv4, IPv6 e OSI" e alle RFC correlate.