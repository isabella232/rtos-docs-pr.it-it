---
title: Capitolo 3-Descrizione funzionale di Azure RTO NetX Secure
description: Questo capitolo contiene una descrizione funzionale di NetX Secure TLS.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c28ad0255f99986a4ddfe5faefad81e70840e5e0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821590"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-secure"></a>Capitolo 3-Descrizione funzionale di Azure RTO NetX Secure

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Questo capitolo contiene una descrizione funzionale di Azure RTO NetX Secure TLS. Esistono due tipi principali di esecuzione del programma in un'applicazione TLS sicura NetX: inizializzazione e chiamate dell'interfaccia dell'applicazione. 

*NetX Secure presuppone l'esistenza di ThreadX e NetX/NetXDuo. Da ThreadX, sono necessari l'esecuzione di thread, la sospensione, i timer periodici e le strutture di esclusione reciproca. Da NetX/NetXDuo richiede le funzionalità di rete TCP/IP e i driver.*

## <a name="transport-layer-security-tls-and-secure-sockets-layer-ssl"></a>Transport Layer Security (TLS) e Secure Sockets Layer (SSL)

Il componente Secure Network Protocol di NetX Secure è un'implementazione del protocollo Transport Layer Security (TLS), come descritto in RFC 2246 (versione 1,0), 4346 (versione 1,1), 5246 (versione 1,2) e 8446 (versione 1,3). Sono incluse anche le routine di supporto per Basic X. 509 (RFC 5280).

NetX Secure TLS supporta le versioni TLS 1,2 e 1,3. Le implementazioni vengono fornite per le funzionalità TLS 1,0 e TLS 1,1 ora deprecate, ma devono essere inizializzate in modo esplicito e non sono consigliate per l'uso nei nuovi prodotti.

*Secure Sockets Layer* (SSL) è il nome originale di TLS prima che diventi uno standard in RFC 2246 e "SSL" viene spesso usato come nome generico per i protocolli TLS. L'ultima versione di SSL è 3,0 e TLS 1,0 viene a volte definito SSL versione 3,1. Tutte le versioni del protocollo "SSL" ufficiale sono considerate obsolete e non sicure e attualmente NetX Secure non fornisce un'implementazione SSL.

TLS specifica un protocollo per generare *chiavi di sessione* create durante l' *handshake* TLS tra un client e un server TLS e tali chiavi vengono usate per crittografare i dati inviati dall'applicazione durante la *sessione TLS.*

I dati TLS sono divisi in *record* equivalenti al concetto di pacchetto TCP. Ogni record TLS ha un'intestazione e i record TLS crittografati hanno anche un piè di pagina (hash di checksum). I record di handshake TLS hanno un'intestazione aggiuntiva incapsulata all'interno del record TLS più grande. Il record TLS è incapsulato dal protocollo di rete Transport Layer nello stesso modo in cui un pacchetto TCP viene incapsulato da un pacchetto IP.

### <a name="tls-13"></a>TLS 1,3

Nel 2018 agosto la specifica TLS 1,3 è stata finalizzata. La nuova versione del protocollo è un aggiornamento piuttosto significativo che modifica alcuni aspetti fondamentali della sicurezza e delle prestazioni sottostanti di TLS. Tuttavia, queste modifiche sono sostanzialmente invisibili per l'utente TLS tipico, perché si applicano principalmente alla macchina a stati di handshake TLS e alla generazione della chiave della sessione. Sono state aggiunte anche numerose funzionalità e estensioni facoltative. Di seguito è riportato un riepilogo delle modifiche e il modo in cui influiscano sulla funzionalità TLS.

- La macchina a stati di handshake è stata ottimizzata rimuovendo un intero scambio di messaggi dal server.
- La generazione delle chiavi è stata aggiornata in modo da usare una routine standardizzata denominata HKDF (funzione di derivazione della chiave basata su HMAC) e associa le chiavi della sessione a tutti i messaggi di handshake, anziché alcuni parametri SELECT.
- Tutti i ciphersuites TLS 1,2 e precedenti sono deprecati e non sono compatibili con TLS 1,3. Analogamente, tutte le ciphersuites di TLS 1,3 sono inutilizzabili con le versioni precedenti.
- Tutti i ciphersuites di TLS 1,3 forniscono la segretezza assoluta (PFS) usando chiavi effimere<sup>6</sup> 
- TLS 1,3 rimuove il "codice di autenticazione del messaggio" (MAC) in ogni record a favore dell'uso di crittografie AEAD<sup>7</sup>
- Sono state aggiunte altre funzionalità facoltative, incluso 0-RTT (tempo di round trip zero) che consente l'invio dei dati dell'applicazione durante l'handshake. 0-RTT è esclusivamente facoltativo e non è attualmente supportato in Azure RTO TLS.

TLS 1,3 non influisce in modo significativo sulle applicazioni utente. L'API rimane esattamente identica tra le versioni e ciphersuites sono contrassegnate in modo che sia possibile usare una singola tabella ciphersuite.

Per usare TLS 1,3, è necessario definire globalmente la macro NX_SECURE_TLS_ENABLE_TLS_1_3. TLS 1,3 è disabilitato per impostazione predefinita in Azure RTO TLS.

6. Le chiavi "effimere" sono coppie di chiavi asimmetriche generate durante l'handshake TLS e usate per lo scambio di segreti solo per tale sessione. La coppia di chiavi viene eliminata dopo l'uso. in questo modo si impedisce a un utente malintenzionato di accedere ai dati crittografati in una sessione TLS registrata anche se una chiave privata del certificato viene compromessa in qualsiasi momento in futuro, quindi "segretezza in diretta perfetta".

7. Crittografia autenticata con dati associati: modalità per le crittografie come AES che combina la crittografia e il controllo dell'integrità in un'unica operazione, eliminando la necessità di un hash separato dei dati per il controllo dell'integrità.

### <a name="tls-record-header"></a>Intestazione del record TLS

Qualsiasi record TLS valido deve avere un'intestazione TLS, come illustrato in errore. Origine riferimento non trovata.

![Diagramma di un'intestazione di record TLS.](media/image2.png)

Figura 1-intestazione del record TLS

I campi dell'intestazione del record TLS sono definiti come segue:

| Campo di intestazione TLS | Scopo     |
| ---------------- | ------------- |
| **Tipo di messaggio a 8 bit** | Questo campo contiene il tipo di record TLS da inviare. I tipi validi sono i seguenti:<br />-ChangeCipherSpec<sup>8</sup>: 0x14<br />-Avviso: 0x15<br />-Handshake: 0x16<br />-Dati applicazione: 0x17 |
| **Versione del protocollo a 16 bit** | Questo campo contiene la versione del protocollo TLS. I valori validi sono i seguenti:<br />-SSL 3,0:0x0300<br />-TLS 1,0:0x0301<br />-TLS 1,1:0x0302<br />-TLS 1,2:0x0303<br />- **TLS 1,3 <sup>9</sup>**: **0x0303** |
| **Lunghezza a 16 bit** | Questo campo contiene la lunghezza dei dati incapsulati nel record TLS. |

8. In TLS 1,3 il messaggio ChangeCipherSpec non viene più usato, sebbene sia comunque possibile inviarlo per motivi di compatibilità, nel qual caso il messaggio viene ignorato.

9. TLS 1,3 avrebbe tecnicamente un valore di 0x0304 se questo schema è stato proseguito, ma il protocollo è stato modificato in modo da avere la versione del protocollo effettiva in un'estensione, quindi tutti i record di TLS 1,3 usano 0x0303 nei campi versione protocollo per la compatibilità con le versioni precedenti.

### <a name="tls-handshake-record-header"></a>Intestazione del record di handshake TLS

Qualsiasi record di handshake TLS valido deve avere un'intestazione di handshake TLS, come illustrato nella figura 2.

![Diagramma di un'intestazione di record di handshake TLS.](media/image3.png)

Figura 2-intestazione del record di handshake TLS

I campi dell'intestazione del record di handshake TLS sono definiti come segue:

| Campo di intestazione TLS | Scopo |
| ---------------- |----------------------- |
| **Tipo di messaggio a 8 bit** | Questo campo contiene il tipo di record TLS da inviare. I tipi validi sono i seguenti:<br />-ChangeCipherSpec<sup>10</sup>: 0x14<br />-Avviso: 0x15<br />-Handshake: 0x16<br />-Dati applicazione: 0x17 |
| **Versione del protocollo a 16 bit** | Questo campo contiene la versione del protocollo TLS. I valori validi sono i seguenti:<br />-SSL 3,0:0x0300<br />-TLS 1,0:0x0301<br />-TLS 1,1:0x0302<br />-TLS 1,2:0x0303<br />- **TLS 1,3 <sup>11</sup>**: **0x0303** |
| **Lunghezza a 16 bit**    | Questo campo contiene la lunghezza dei dati incapsulati nel record TLS. |
| **Tipo di handshake a 8 bit** | Questo campo contiene il tipo di messaggio di handshake. I valori validi sono i seguenti (* i messaggi in **grassetto** sono stati aggiunti in TLS 1,3):<br />-HelloRequest: 0x00<br />-ClientHello: 0x01<br />-ServerHello: 0x02<br />- **HelloVerifyRequest**: **0x03**<br />- **NewSessionTicket**: **0x04**<br />- **EndOfEarlyData**: **0x05**<br />- **EncryptedExtensions**: **0x08**<br />-Certificato: 0x0B<br />-ServerKeyExchange: 0x0C<br />-CertificateRequest: 0x0D<br />-ServerHelloDone: 0x0E<br />-CertificateVerify: 0x0F<br />-ClientKeyExchange: 0x10<br />-Operazione completata: 0x14<br />- **Aggiornamento** della pagina: **0x18**<br />- **MessageHash**: **0xFE** |
| **Lunghezza a 24 bit**    | Questo campo contiene la lunghezza dei dati del messaggio di handshake. |

10. In TLS 1,3 il messaggio ChangeCipherSpec non viene più usato, sebbene sia comunque possibile inviarlo per motivi di compatibilità, nel qual caso il messaggio viene ignorato.

11. TLS 1,3 avrebbe tecnicamente un valore di 0x0304 se questo schema è stato proseguito, ma il protocollo è stato modificato in modo da avere la versione del protocollo effettiva in un'estensione, quindi tutti i record di TLS 1,3 usano 0x0303 nei campi versione protocollo per la compatibilità con le versioni precedenti.

### <a name="the-tls-handshake-and-tls-session"></a>Handshake TLS e sessione TLS

Un handshake TLS tipico (versioni 1.0-1.2) è illustrato nella figura 3. Un handshake TLS inizia quando il client TLS Invia un messaggio *ClientHello* a un server TLS, indicando il desiderio di avviare una sessione TLS. Il messaggio contiene informazioni sulla crittografia che il client desidera utilizzare per la sessione, insieme alle informazioni utilizzate per generare le chiavi di sessione in un secondo momento nell'handshake. Fino a quando non vengono generate le chiavi della sessione, tutti i messaggi nell'handshake TLS non vengono crittografati. TLS 1,3 modifica leggermente l'handshake: i dettagli vengono presentati nella sezione successiva.

Il server TLS risponde a ClientHello con un messaggio ServerHello, che indica una selezione dalle opzioni di crittografia fornite dal client. ServerHello è seguito da un messaggio di certificato, in cui il server fornisce un certificato digitale per autenticare l'identità nel client. Infine, il server invia un messaggio ServerHelloDone per indicare che non sono presenti altri messaggi da inviare. Il server può facoltativamente inviare altri messaggi dopo ServerHello e in alcuni casi potrebbe non inviare un messaggio di certificato, di conseguenza la necessità del messaggio ServerHelloDone.

Una volta che il client ha ricevuto tutti i messaggi del server, dispone di informazioni sufficienti per generare le chiavi della sessione. TLS esegue questa operazione creando un bit condiviso di dati casuali denominato *Master Secret*, che è a dimensione fissa e viene usato come valore di inizializzazione per generare tutte le chiavi necessarie una volta abilitata la crittografia. Il segreto pre-master viene crittografato usando l'algoritmo a chiave pubblica, ad esempio RSA, specificato nei messaggi Hello (vedere di seguito per informazioni sugli algoritmi a chiave pubblica) e la chiave pubblica fornita dal server nel certificato. Una funzionalità TLS facoltativa denominata chiavi precondivise (PSK) consente a ciphersuites che non usano un certificato, ma usano invece un valore segreto condiviso tra gli host (in genere tramite trasferimento fisico o un altro metodo protetto). Il segreto condiviso viene utilizzato per generare il segreto pre-master anziché utilizzare un messaggio crittografato per inviare il master secret. Vedere la sezione relativa alle chiavi precondivise di seguito.

Il segreto pre-master crittografato viene inviato al server nel messaggio ClientKeyExchange. Il server, al momento della ricezione del messaggio ClientKeyExchange, decrittografa il segreto pre-master usando la relativa chiave privata e continua a generare le chiavi della sessione in parallelo con il client TLS.

Una volta generate le chiavi della sessione, tutti gli altri messaggi possono essere crittografati usando l'algoritmo di chiave privata, ad esempio AES, selezionato nei messaggi Hello. Un messaggio finale non crittografato denominato ChangeCipherSpec viene inviato sia dal client che dal server per indicare che tutti gli altri messaggi verranno crittografati.

Il primo messaggio crittografato inviato sia dal client che dal server è anche il messaggio di handshake TLS finale, denominato completato. Questo messaggio contiene un hash di tutti i messaggi di handshake ricevuti e inviati. Questo hash viene utilizzato per verificare che nessuno dei messaggi nell'handshake sia stato alterato o danneggiato (che indica una possibile violazione della sicurezza).

Dopo la ricezione dei messaggi finiti e la verifica degli hash di handshake, la sessione TLS viene avviata e l'applicazione inizia a inviare e ricevere dati. Per la prima volta viene eseguito l'hashing di tutti i dati inviati da entrambi i lati durante la sessione TLS utilizzando l'algoritmo hash scelto nei messaggi Hello (per fornire l'integrità del messaggio) e crittografato utilizzando l'algoritmo di chiave privata scelto con le chiavi di sessione generate.

Infine, una sessione TLS può essere conclusa correttamente solo se il client o il server sceglie di eseguire questa operazione. Una sessione troncata è considerata una violazione della sicurezza (poiché un utente malintenzionato potrebbe tentare di impedire la ricezione di tutti i dati), quindi viene inviata una notifica speciale quando uno dei due lati desidera terminare la sessione, denominata avviso CloseNotify. Sia il client che il server devono inviare ed elaborare un avviso CloseNotify per un arresto corretto della sessione.

![Diagramma di un handshake TLS tipico.](media/image4.png)

Figura 3-handshake TLS tipico

### <a name="tls-13-handshake"></a>Handshake TLS 1,3

TLS 1,3 è una revisione piuttosto importante del protocollo TLS. La maggior parte delle modifiche è stata apportata all'handshake per migliorare la sicurezza e le prestazioni. Un handshake TLS 1,3 tipico è illustrato nella figura 4. La differenza principale si può notare nel numero di scambi tra il server e il client.

In TLS 1,2 e versioni precedenti, il server invia due voli<sup>12</sup> di messaggi, prima ServerHello e poi un messaggio ChangeCipherSpec prima di inviare il messaggio crittografato terminato che termina l'handshake. In TLS 1,3 il server invia tutti gli elementi del primo volo, ovvero ServerHello, Extensions, certificate e fine. Il messaggio ChangeCipherSpec è stato eliminato e il server genera le chiavi di sessione e avvia la crittografia dei messaggi di handshake immediatamente dopo ServerHello.

La nuova disposizione significa che l'handshake TLS è protetto dalla crittografia, limitando la quantità di dati di testo non crittografato a cui un utente malintenzionato può accedere. Inoltre, la rimozione del secondo volo del server (che era solo un ChangeCipherSpec seguito da un termine) significa che un client TLS non deve più attendere per iniziare a trasmettere i dati dell'applicazione: non appena il client invia il proprio messaggio terminato, la sessione viene avviata.

12. Un volo è semplicemente una raccolta di messaggi TLS inviati simultaneamente in un gruppo.

![Diagramma di un handshake TLS 1,3.](media/image5.png)

Figura 4: handshake TLS 1,3

> [!NOTE]
> *In TLS 1,3 è stata introdotta anche la nozione di "dati anticipati" e 0-RTT (tempo di round trip zero), il che significa che alcuni dati dell'applicazione possono essere inviati nel primo volo di messaggi. Questa funzionalità facoltativa è stata aggiunta principalmente come ottimizzazione per la velocità di risposta del Web browser, ad esempio per inviare intestazioni HTTP iniziali per avviare il rendering di una pagina. A partire da Azure RTO 6,0 questa funzionalità non è supportata.*

### <a name="initialization"></a>Inizializzazione

Lo stack TCP/IP NetX o NetXDuo deve essere inizializzato prima di usare NetX Secure TLS. Per informazioni su come inizializzare correttamente lo stack TCP/IP, vedere la guida dell'utente di NetX o NetXDuo.

Una volta inizializzato lo stack TCP/IP di NetX, è possibile abilitare TLS. Internamente, tutto il traffico di rete TLS e l'elaborazione vengono gestiti dallo stack NetX/NetXDuo senza richiedere l'intervento dell'utente. Tuttavia, TLS prevede alcuni requisiti specifici che devono essere gestiti separatamente dallo stack di rete sottostante. Questi parametri vengono assegnati al blocco di controllo TLS denominato ***NX_SECURE_TLS_SESSION** _ utilizzando il servizio _ *_nx_secure_tls_session_create_**.

In TLS sono disponibili due modalità, ovvero server e client, che possono essere abilitate in un'applicazione (ma solo una modalità per socket NetX), ognuna delle quali presenta requisiti specifici, descritti di seguito.

In entrambe le modalità, NetX Secure TLS richiede la creazione e la configurazione di un socket TCP (***NX_TCP_SOCKET** _) per le comunicazioni TCP con l'host remoto. Il socket TCP viene assegnato a un'istanza della sessione TLS con il servizio _ *_nx_secure_tls_session_start_**, descritto di seguito.

### <a name="initialization--tls-server"></a>Inizializzazione-server TLS

Oltre a un socket TCP, la modalità server TLS sicuro NetX richiede un *certificato digitale*, ovvero un documento usato per identificare il server TLS per il client TLS connesso e la *chiave privata* corrispondente dei certificati, in genere per l'algoritmo di crittografia RSA. Lo standard International Telecommunications Union X. 509 specifica il formato del certificato usato da TLS e sono disponibili numerose utilità per la creazione di certificati digitali X. 509.

Per NetX Secure TLS, il certificato X. 509 deve essere codificato in formato binario usando il formato Distinguished Encoding Rules (DER) di ASN. 1. DER è il formato binario standard TLS in transito per i certificati.

La chiave privata associata al certificato specificato deve essere in formato DER-Encoded PKCS # 1. La chiave privata viene usata solo sul dispositivo e non verrà mai trasmessa in rete. Mantieni le chiavi private sicure perché forniscono la sicurezza per le comunicazioni TLS!

Per inizializzare il certificato del server TLS, l'applicazione deve fornire un puntatore a un buffer che contiene il certificato X. 509 con codifica der e i dati facoltativi della chiave privata RSA con codifica DER PKCS # 1 usando il servizio ***nx_secure_x509_certificate_intialize** _, che popola la struttura _ *NX_SECURE_X509_CERT** con i dati del certificato appropriati per l'uso da parte di TLS.

Una volta inizializzato, il certificato del server deve essere aggiunto al blocco di controllo TLS utilizzando il servizio ***nx_secure_tls_local_certificate_add*** .

Una volta che il certificato del server è stato aggiunto al blocco di controllo TLS, il socket può essere usato per stabilire una connessione al server TLS sicura.

### <a name="initialization--tls-client"></a>Inizializzazione-client TLS

La modalità client TLS sicura di NetX richiede un *archivio certificati attendibile*, ovvero una raccolta di certificati digitali con codifica X. 509 provenienti da autorità di certificazione attendibili (CA). Questi certificati vengono considerati attendibili dal protocollo TLS e vengono usati come base per l'autenticazione dei certificati forniti dalle entità server TLS per il client TLS sicuro NetX.

Un certificato CA attendibile può essere *autofirmato* o firmato da un'altra CA, nel qual caso il certificato viene definito *CA intermedia* (ICA). In una tipica applicazione TLS, il server fornisce i certificati ICA insieme al certificato del server, ma l'unico requisito per la corretta autenticazione è che una catena di autorità emittenti (certificati usati per firmare altri certificati) può essere ritracciata dal certificato del server a un certificato CA attendibile nell'archivio certificati attendibili. Questa catena è nota come  *catena di attendibilità* o *catena di certificati*.

Per inizializzare una CA attendibile o un certificato ICA, l'applicazione deve fornire un puntatore a un buffer contenente il certificato X. 509 con codifica DER usando il servizio ***nx_secure_x509_certificate_intialize** _, che popola la struttura _ *NX_SECURE_X509_CERT** con i dati del certificato appropriati per l'uso da parte di TLS.

I certificati attendibili che sono stati inizializzati vengono quindi aggiunti al blocco di controllo TLS utilizzando il servizio ***nx_secure_tls_trusted_certificate_add*** . Se non si aggiunge un certificato, la sessione client TLS non riuscirà perché il protocollo TLS non potrà autenticare gli host server TLS remoti.

Il client TLS necessita inoltre di spazio per l'allocazione del certificato del server in ingresso (presupponendo che non venga utilizzata una modalità di chiave pre-condivisa). A partire da NetX Secure TLS 5,12, non è più necessario che l'applicazione allochi spazio per il certificato remoto. Tuttavia, l'opzione legacy per allocare spazio per un certificato del server è ancora disponibile e i certificati allocati dall'utente verranno utilizzati prima dell'ottimizzazione del buffer del certificato interno <sup>13</sup> . per ulteriori informazioni, vedere il servizio ***nx_secure_tls_remote_certificate_allocate*** .

Una volta che l'archivio certificati attendibile è stato creato e lo spazio per il certificato server è stato allocato, il socket può essere usato per stabilire una connessione client TLS sicura.

13. L'ottimizzazione utilizza il "buffer di pacchetti" fornito dall'applicazione utente alla sessione TLS utilizzando *nx_secure_tls_session_packet_buffer_set* per allocare le strutture di analisi X. 509 anziché utilizzare le strutture fornite dall'utente utilizzate nelle versioni precedenti di NETX Secure TLS. È probabile che si verifichi una catena di certificati che supera la dimensione del buffer di pacchetti, in questo caso è possibile che le dimensioni del buffer dei pacchetti siano aumentate oppure che sia possibile utilizzare *nx_secure_tls _remote_certificate_allocate* per allocare più spazio per la catena di certificati.

### <a name="application-interface-calls"></a>Chiamate dell'interfaccia dell'applicazione

Le applicazioni TLS protette NetX in genere eseguono chiamate di funzione dall'interno dei thread dell'applicazione in esecuzione in ThreadX RTO. Alcune inizializzazioni, in particolare per i protocolli di comunicazione di rete sottostanti (ad esempio TCP e IP), possono essere chiamate da ***tx_application_define *.** Per ulteriori informazioni sull'inizializzazione delle comunicazioni di rete, vedere il manuale dell'utente di NetX/NetXDuo.

TLS usa in modo intensivo le routine di crittografia che sono operazioni che richiedono un utilizzo intensivo del processore. In genere, queste operazioni verranno eseguite nel contesto del thread chiamante.

### <a name="tls-session-start"></a>Avvio sessione TLS

Per il funzionamento di TLS è necessario un protocollo di rete a livello di trasporto sottostante. Il protocollo usato in genere è TCP. Per stabilire una sessione TLS sicura NetX, è necessario stabilire una connessione TCP usando l'API TCP NetX/NetXDuo. È necessario creare un **NX_TCP_SOCKET** e una connessione stabilita usando i **_Servizi nx_tcp_server_socket_listen_*_ e _*_nx_tcp_server_socket_accept_*_ (per il server TLS) o il servizio _*_nx_tcp_client_socket_connect_** (per il client TLS).

Una volta stabilita una connessione TCP, il socket TCP viene quindi passato al servizio ***nx_secure_tls_session_start*** .

### <a name="tls-packet-allocation"></a>Allocazione pacchetti TLS

NetX Secure TLS usa la stessa struttura di pacchetti di NetX/NetXDuo TCP (***NX_PACKET** _) ad eccezione del fatto che anziché chiamare il servizio _*_nx_packet_allocate_*_ , è necessario chiamare il servizio _ *_nx_secure_tls_packet_allocate_** in modo che lo spazio per l'intestazione TLS possa essere allocato correttamente.

### <a name="tls-session-send"></a>Invio sessione TLS

Una volta avviata la sessione TLS, l'applicazione può inviare dati utilizzando il servizio ***nx_secure_tls_session_send** _. Il servizio di invio è identico in uso con il servizio _*_nx_tcp_socket_send_*_ , accettando una struttura di dati _*_NX_PACKET_*_ contenente i dati inviati, solo i dati verranno crittografati dallo stack di TLS sicuro NX prima di essere inviati e il pacchetto deve essere allocato usando _ *_nx_secure_tls_packet_allocate_* *.

### <a name="tls-session-receive"></a>Ricezione sessione TLS

Una volta avviata la sessione TLS, l'applicazione può iniziare a ricevere dati utilizzando il servizio ***nx_secure_tls_session_receive** _. Analogamente all'invio della sessione TLS, questo servizio è identico a _ *_nx_tcp_socket_receive_* *, ad eccezione del fatto che i dati in ingresso vengono decrittografati e verificati dallo stack TLS prima di essere restituiti nella struttura del pacchetto.

### <a name="tls-session-close"></a>Chiusura sessione TLS

Una volta completata la sessione TLS, sia il client che il server TLS devono inviare un avviso CloseNotify all'altro lato per arrestare la sessione. Entrambi i lati devono ricevere ed elaborare l'avviso per garantire una corretta chiusura della sessione.

Se l'host remoto invia un avviso CloseNotify, tutte le chiamate al servizio ***nx_secure_tls_session_receive** _ elaborerà l'avviso, invierà l'avviso corrispondente all'host remoto e restituirà il valore _ *_NX_SECURE_TLS_SESSION_CLOSED_* *. Una volta chiusa la sessione, eventuali ulteriori tentativi di inviare o ricevere dati con tale sessione TLS avranno esito negativo.

Se l'applicazione desidera chiudere la sessione TLS, il servizio ***nx_secure_tls_session_end** _ deve essere chiamato. Il servizio invierà l'avviso CloseNotify ed elaborerà la risposta CloseNotify. Se la risposta non viene ricevuta, viene restituito un valore di errore _ *_NX_SECURE_TLS_SESSION_CLOSE_FAIL_**, che indica che la sessione TLS non è stata arrestata in modo corretto, una possibile violazione della sicurezza.

### <a name="tls-alerts"></a>Avvisi TLS

TLS è progettato per garantire la massima sicurezza, quindi qualsiasi comportamento errato nel protocollo viene considerato una potenziale violazione della sicurezza. Per questo motivo, gli eventuali errori di elaborazione dei messaggi o di crittografia/decrittografia sono considerati errori irreversibili che terminano immediatamente l'handshake o la sessione.

Anche se la gestione degli errori in un'applicazione locale è relativamente semplice, l'host remoto deve essere in grado di rilevare che si è verificato un errore per gestire correttamente la situazione ed evitare ulteriori possibili violazioni della sicurezza. Per questo motivo, TLS invierà un messaggio di *avviso* all'host remoto su qualsiasi errore.

Gli avvisi vengono gestiti in modo analogo a qualsiasi altro messaggio TLS e vengono crittografati durante la sessione per impedire a un utente malintenzionato di raccogliere informazioni dal tipo di avviso fornito. Durante l'handshake, gli avvisi inviati hanno un ambito limitato per limitare la quantità di informazioni che possono essere ottenute da un potenziale utente malintenzionato.

L'avviso CloseNotify, usato per chiudere la sessione TLS, è l'unico avviso non irreversibile. Sebbene venga considerato un avviso e venga inviato come messaggio di avviso, un CloseNotify è diverso dagli altri avvisi in quanto non indica che si è verificato un errore.

Il valore di avviso e il "livello" (i livelli sono "avviso" e "irreversibile": la maggior parte degli avvisi TLS sono "irreversibili") sono definiti nelle RFC di TLS e indicano il tipo di errore che si è verificato. La maggior parte degli avvisi TLS diversi da CloseNotify può essere considerata un'indicazione di un potenziale problema di sicurezza e comporterà l'interruzione della sessione TLS o dell'handshake. Se una chiamata API TLS restituisce **NX_SECURE_TLS_ALERT_RECEIVED** (0x114), il servizio API **_nx_secure_tls_session_alert_value_get_** (nuovo in NetX Secure TLS versione 5,12) può essere usato per recuperare il valore e il livello di avviso TLS per l'applicazione da usare per le decisioni relative alle risposte ai problemi di sicurezza. Nella maggior parte dei casi, qualsiasi avviso ricevuto dall'host remoto diverso da CloseNotify deve essere considerato un errore irreversibile, sebbene esistano alcuni excptions: per altre informazioni, vedere le RFC di TLS.

### <a name="tls-session-renegotiation"></a>Rinegoziazione della sessione TLS

TLS supporta la nozione di "rinegoziazione", che è semplicemente una rinegoziazione dei parametri della sessione TLS all'interno del contesto di una sessione TLS esistente. Ciò significa che, in pratica, i nuovi messaggi di handshake vengono crittografati e autenticati utilizzando la sessione esistente. Il rinegoziazione viene usato quando un host TLS vuole generare nuovi parametri di sessione (ad esempio, generare nuove chiavi di sessione TLS) senza dover completare la sessione esistente. Ad esempio, la rinegoziazione potrebbe essere auspicabile quando i criteri di sicurezza per un'applicazione stabiliscono che le chiavi di sessione vengono usate solo per un periodo di tempo limitato, ma una sessione TLS rimane attiva dopo tale periodo di tempo.

Un problema con la rinegoziazione della sessione è che rende TLS vulnerabile a un attacco man-in-the-Middle specifico in cui un utente malintenzionato può convincere un server ad avviare una rinegoziazione con nuovi parametri, consentendo così all'autore dell'attacco di eseguire il Hijack della sessione TLS. Per attenuare questo problema, è stata introdotta l'estensione dell'indicazione di rinegoziazione sicura (vedere la sezione **Error). Origine riferimento non trovata.** sezione).

NetX Secure TLS supporta completamente il rinegoziazione delle sessioni e l'estensione per l'indicazione di rinegoziazione sicura.

Quando si ricevono dati da un host remoto, renegotations (e l'estensione) vengono gestiti automaticamente senza interazione tra le applicazioni. Se si desidera una notifica sulle rinegoziazioni della sessione, è possibile fornire un callback di rinegoziazione con il servizio *nx_secure_tls_session_renegotiate_callback_set* . Il callback verrà richiamato ogni volta che una rinegoziazione viene richiesta dall'host remoto, consentendo all'applicazione di eseguire l'azione, se necessario.

Per avviare una rinegoziazione da una sessione TLS attiva, è sufficiente richiamare il servizio *nx_secure_tls_session_renegotiate* nella sessione TLS desiderata.

### <a name="tls-session-resumption"></a>Ripresa della sessione TLS

La ripresa della sessione TLS non può essere confusa con la rinegoziazione della sessione, nonostante alcune analogie. Quando la *rinegoziazione* della sessione comporta l'avvio di un nuovo handshake in una sessione TLS esistente, la *ripresa* della sessione è una funzionalità puramente facoltativa che prevede il riavvio di una sessione TLS chiusa senza eseguire un handshake TLS completo. A tale scopo, un'implementazione di TLS può memorizzare nella cache i parametri e le chiavi della sessione, associando questi ultimi a un *ID di sessione,* un identificatore univoco fornito nell'handshake originale. Fornendo un ID di sessione a un server TLS, un client indica che una sessione TLS precedente tra gli host esisteva e è stata completata in passato e che il client possiede ancora lo stato per ristabilire la sessione con un handshake ridotto. Poiché le chiavi della sessione sono teoricamente ancora segrete e sono note solo dai due host che comunicano, il server può avviare una nuova sessione TLS e ignorare la maggior parte dell'handshake normale.

La ripresa della sessione può essere utile per evitare le operazioni di chiave pubblica potenzialmente costose usate per condividere la generazione di chiavi master secret e verificare le firme del certificato, ma richiede anche che i parametri della sessione, le chiavi e lo stato di crypotgraphic vengano mantenuti in memoria per tutte le sessioni possibili (almeno per un intervallo di tempo configurabile).

La versione corrente di NetX Secure TLS non supporta la ripresa della sessione: l'ID di sessione viene semplicemente ignorato dai server TLS e i client TLS forniscono sempre un ID di sessione NULL che richiede al server di eseguire un handshake completo. La mancanza di ripresa della sessione non dovrebbe causare problemi di interoperabilità poiché si tratta di una funzionalità completamente facoltativa e tutte le implementazioni di TLS devono avere come valore predefinito un handshake completo se l'ID sessione è NULL o non riconosciuto.

### <a name="protocol-layering"></a>Layering del protocollo

Il protocollo TLS si inserisce nello stack di rete tra il livello di trasporto (ad esempio TCP) e il livello dell'applicazione. TLS viene a volte considerato un protocollo di livello trasporto, di conseguenza la sicurezza a *livello di trasporto* , ma poiché funge da applicazione per quanto riguarda i protocolli di rete sottostanti (ad esempio TCP), viene talvolta raggruppato nel livello dell'applicazione.

TLS richiede un protocollo di livello trasporto che supporta il recapito in ordine e senza perdita di contenuti, ad esempio TCP. A causa di questo requisito, TLS non può essere eseguito su UDP Poiché UDP non garantisce il recapito di datagrammi. Un protocollo separato denominato *DTLS,* che è una versione modificata di TLS, viene usato per le applicazioni che richiedono la sicurezza di TLS su un protocollo di datagramma come UDP. NetX Secure supporta DTLS, ma la documentazione per DTLS è separata da questo documento.

![Diagramma dei livelli di protocollo TCP/IP e TLS.](media/image6.png)

Figura 5-livelli di protocollo TCP/IP e TLS

## <a name="network-communications-security"></a>Sicurezza delle comunicazioni di rete

La protezione delle comunicazioni tramite reti pubbliche e Internet è un argomento di importanza critica e l'oggetto di un ampio numero di libri, articoli e soluzioni. Questo argomento è molto complesso, ma può essere ridotto a una semplice idea: invio di informazioni su una rete, in modo che solo la destinazione prevista possa accedere o modificare tali informazioni. Questa operazione suddivide in tre concetti importanti: segretezza, integrità e autenticazione. Il protocollo TLS fornisce soluzioni per tutti e tre.

### <a name="secrecy"></a>Secrecy

Quando si inviano dati su una rete, è spesso importante che i dati non possano essere ottenuti da un'entità dannosa. Se i dati vengono inviati tramite una connessione TCP/IP, tutti gli utenti con accesso alla rete saranno in grado di leggere i dati utilizzando gli strumenti di rete facilmente disponibili. Per impedire che i dati vengano ottenuti, devono essere codificati in modo che non possano essere letti, tranne che dalla destinazione prevista, ma si tratta di un *segreto.* In TLS gli algoritmi di crittografia, ad esempio RSA e AES, forniscono la riservatezza.

### <a name="integrity"></a>Integrità

In alcuni casi, la segretezza non è sufficiente per proteggere i dati in transito in una rete. In alcuni casi, potrebbe essere possibile che un'entità dannosa modifichi il contenuto di un pacchetto TCP senza che sia necessario sapere cosa contiene il pacchetto. I dati crittografati possono essere modificati, il rendering della decrittografia non è valido o la modifica dei parametri del messaggio che portano a qualsiasi risultato che l'utente malintenzionato potrebbe essere interessato al raggiungimento. In rete non è possibile impedire a un utente malintenzionato di modificare i dati in transito, ma è possibile fornire un meccanismo per sapere se i dati sono stati modificati o meno. Quando i dati vengono modificati durante il transito, saranno noti e i dati possono essere rifiutati. Questo concetto è l' *integrità*. In TLS, l'integrità viene fornita da una classe di routine di crittografia note come *funzioni hash*. Alcuni esempi di funzioni hash sono MD5 e SHA-1.

### <a name="authentication"></a>Authentication

Il terzo concetto importante nella sicurezza delle comunicazioni di rete è l'idea che i dati devono essere comunicati solo alla destinazione prevista. Un utente malintenzionato può provare a rappresentare un'entità legittima per ricevere i dati destinati a un altro host. Anche se i dati vengono inviati con meccanismi di riservatezza e integrità, l'utente malintenzionato potrebbe ancora essere in grado di ottenere il risultato desiderato (un compromesso di comunicazioni sicure) attraverso questa operazione. Per evitare questo problema, è necessario un meccanismo per dimostrare l'identità di un host remoto prima dell'invio di tutti i dati sensibili. Il processo di dimostrazione dell'identità di un host remoto è l' *autenticazione.* In TLS l'autenticazione viene fornita utilizzando certificati digitali, funzioni hash e un meccanismo denominato *firme digitali* che utilizza una proprietà della crittografia a chiave pubblica (descritta di seguito). Con una *chiave precondivisa* (PSK) può essere fornita anche una forma di autenticazione limitata ma utile.

## <a name="tls-encryption"></a>Crittografia TLS

Il protocollo TLS è un Framework per fornire comunicazioni di rete sicure su Internet usando la crittografia. La crittografia viene in genere definita come il processo di codifica dei dati in modo che il recupero dei dati originali (o informazioni sui dati) sia estremamente difficile senza una *chiave*. Nella crittografia dei sistemi informatici si basa su una matematica complessa, ad esempio campi finiti, che può essere classificata in due tipi: *chiave privata* (o *crittografia simmetrica*) e *chiave pubblica* (o *crittografia asimmetrica*). Esempi di crittografia a chiave privata sono AES (Advanced Encryption Standard) e RC4 (riveste Cipher 4). Esempi di crittografia a chiave pubblica sono RSA (Rivet, Shamir, Adleson) e Diffie-Hellman crittografie.

Il protocollo TLS usa le routine di crittografia della chiave privata e della chiave pubblica per fornire un equilibrio tra prestazioni, sicurezza e flessibilità.

### <a name="private-key-encryption"></a>Crittografia Private-Key

La crittografia a chiave privata è stata usata per migliaia di anni. Le crittografie di sostituzione di base, in cui una lettera o una parola viene sostituita da un'altra lettera o parola non correlata, sono i primi esempi noti di crittografia, ma con l'avvento delle informazioni Age la crittografia della chiave privata è stata notevolmente migliorata.

Una crittografia a chiave privata usa una "chiave" che è semplicemente un valore (che potrebbe essere una parola, una frase o un numero nel caso generale) usato per codificare alcuni dati in modo che solo un'entità con accesso a tale chiave possa decodificare i dati in modo significativo. La chiave viene usata sia per la crittografia che per la decrittografia dei dati, di conseguenza l'altro nome della *crittografia simmetrica*.

La crittografia a chiave privata è in genere rapida e abbastanza semplice da implementare, anche se la matematica è molto complessa. Per questo motivo, TLS usa la crittografia a chiave privata per la maggior parte delle comunicazioni protette.

Tuttavia, la crittografia a chiave privata presenta un problema quando si tenta di applicarla alle comunicazioni di rete del computer generale: la chiave deve essere condivisa tra entrambi i computer che tentano di comunicare. In generale, non è pratico e spesso non è possibile comunicare una chiave privata in modo sicuro tra due computer su Internet, in quanto è possibile ipotizzare che il traffico di rete possa essere ottenuto da un numero qualsiasi di entità nei vari hop che i dati prendono quando vengono instradati attraverso Internet. Se la chiave viene ottenuta da un'entità dannosa, tutti i dati crittografati con tale chiave vengono compromessi. Poiché la maggior parte dei computer su Internet dispone solo di una connessione di rete e non di un altro canale sicuro per le comunicazioni, l'invio di chiavi sulla rete equivale a inviare i dati non crittografati, senza alcuna sicurezza.

Per questo motivo, la crittografia a chiave privata non è sufficiente per implementare un protocollo di sicurezza per le comunicazioni di rete di uso generale. Questo è il punto in cui la crittografia a chiave pubblica può essere utile.

NetX Secure TLS supporta la crittografia a chiave privata AES.

### <a name="public-key-encryption"></a>Crittografia a chiave pubblica

A differenza della crittografia a chiave privata, la crittografia a chiave pubblica è un concetto piuttosto nuovo, che è stato sviluppato nel 1970. Usando un concetto noto come "funzioni trap-door" in matematica, è stato rilevato che era disponibile un modo per condividere una chiave in una rete senza compromettere la sicurezza dei dati crittografati.

Il modo in cui funziona la crittografia a chiave pubblica è che la chiave, nel senso della crittografia a chiave privata descritta in precedenza, è suddivisa in due parti, una *chiave privata* e una *chiave pubblica*, da cui la crittografia a chiave pubblica ne ottiene il nome. Il concetto è che una di queste chiavi, in genere la chiave pubblica, viene utilizzata per la crittografia, mentre l'altra viene utilizzata per la decrittografia. Questa asimmetria di chiavi è il motivo dell'altro nome della crittografia a chiave pubblica: *crittografia asimmetrica*.

La matematica dietro la crittografia a chiave pubblica è piuttosto complessa, ma l'idea è che la chiave pubblica può essere usata *solo* per la crittografia e il recupero di tale chiave non consente di ottenere i dati crittografati. La chiave privata, a sua volta, è l'unico modo per decrittografare i dati crittografati con la chiave pubblica. Quindi, mantenendo il segreto della chiave privata, chiunque voglia comunicare in modo sicuro con il proprietario della chiave privata deve solo crittografare i propri dati con la chiave pubblica corrispondente con la certezza che solo un utente che possiede la chiave privata possa ottenere i dati protetti.

NetX Secure TLS supporta la crittografia a chiave pubblica RSA.

> [!IMPORTANT] 
> *RSA è un'operazione che richiede un utilizzo intensivo del processore se viene utilizzata l'implementazione del software RSA. Dimensioni maggiori delle chiavi aumentano la potenza di elaborazione richiesta da un fattore quadrato-4X più lento per un aumento di 2X della dimensione della chiave.*

### <a name="public-key-authentication"></a>Autenticazione Public-Key

Un effetto collaterale interessante del concetto di crittografia a chiave pubblica è che può essere usato per fornire l'autenticazione e la crittografia eseguendo l'operazione in ordine inverso: la crittografia con la chiave *privata* e la decrittografia tramite la chiave *pubblica* . Il meccanismo effettivo per eseguire questa operazione dipende dall'algoritmo a chiave pubblica usato, ma il concetto è lo stesso.

Per eseguire l'autenticazione usando l'autenticazione con chiave pubblica, il proprietario di una chiave privata crittografa alcuni dati (in genere un hash crittografico dei dati da autenticare) usando tale chiave privata. Quindi, un utente che desidera autenticare che i dati provenienti dal proprietario della chiave privata utilizza la chiave pubblica associata per decrittografare i dati, se la decrittografia ha esito positivo e supponendo che l'utente abbia considerato attendibile la validità della chiave pubblica, può essere certo che i dati provengono dal proprietario della chiave privata.

In TLS l'autenticazione con chiave pubblica viene usata per verificare la validità di un certificato digitale fornito da un server TLS (e, facoltativamente, del client TLS) usando le chiavi pubbliche dell'archivio certificati attendibili. Il certificato viene verificato rispetto a una chiave pubblica nell'archivio e i dati del certificato vengono usati per controllare l'identità del server.

NetX Secure TLS supporta l'autenticazione RSA.

### <a name="cryptographic-hashing"></a>Hashing crittografico

La crittografia non è l'unica operazione di crittografia utilizzata in TLS. Per garantire l'integrità dei messaggi durante una sessione TLS, è necessario un checksum per garantire che il contenuto del messaggio non sia stato alterato. Un semplice checksum (usato in TCP), tuttavia, non è sufficiente per garantire un livello di integrità accettabile, in quanto può essere facilmente sovvertito da un utente malintenzionato esperto. Il meccanismo utilizzato da TLS per fornire l'integrità dei messaggi è noto come *hash crittografico*.

La crittografia è una codifica 1:1, ovvero la completezza dei dati originali può essere ottenuta dai dati crittografati. Tuttavia, un hash esegue il mapping di una quantità arbitraria di dati in un valore a dimensione fissa, proprio come un checksum. A differenza di un semplice checksum, un hash è progettato specificamente per ridurre i *conflitti*, in cui i dati di input diversi hanno come risultato lo stesso output. Con un semplice checksum, se un bit viene capovolto da 1 a 0 e un altro bit da 0 a 1, il checksum è lo stesso. Con un hash crittografico, l'output potrebbe variare in modo significativo, rendendo difficile per un utente malintenzionato modificare i dati con hash e fare in modo che l'operazione hash sui dati modificati restituisca comunque lo stesso valore (e quindi verificando erroneamente l'integrità dei dati).

TLS usa una serie di algoritmi hash diversi per garantire l'integrità dei messaggi, sia messaggi dell'applicazione che messaggi di controllo TLS. Sono inclusi MD5, SHA-1 e SHA-256.

NetX Secure TLS supporta l'hashing MD5, SHA-1 e SHA-256.

## <a name="tls-extensions"></a>Estensioni TLS

TLS fornisce una serie di estensioni che forniscono funzionalità aggiuntive per alcune applicazioni. Queste estensioni vengono in genere inviate come parte dei messaggi ClientHello o ServerHello, indicando a un host remoto il desiderio di usare un'estensione o fornire dettagli aggiuntivi da usare per stabilire la sessione TLS sicura.

In generale, le estensioni forniscono parametri facoltativi a TLS all'inizio dell'handshake che guidano le operazioni di continuazione. Alcune estensioni richiedono l'input dell'applicazione o il processo decisionale, mentre altre vengono gestite automaticamente.

La tabella seguente descrive le estensioni TLS attualmente supportate da NetX Secure TLS:

| **Extension Name**              | **Descrizione**              |
| ------------------------------- |----------------------------- |
| Indicazione di rinegoziazione sicura | Questa estensione mitiga una vulnerabilità degli attacchi man-in-the-Middle che può verificarsi durante un handshake di rinegoziazione.|
| Indicazione nome server          | Questa estensione consente a un client TLS di fornire un nome DNS specifico a un server TLS, consentendo al server di selezionare le credenziali corrette (si presuppone che il server disponga di più certificati di identità e di rete entryPoints). |
| Algoritmi di firma            | Questa estensione consente a un client TLS di fornire un elenco di algoritmi di firma e hash accettabili a un server TLS. |

Panoramica delle estensioni TLS supportate

### <a name="secure-renegotiation-indication"></a>Indicazione di rinegoziazione sicura

TLS supporta la nozione di esecuzione di un handshake all'interno di una sessione TLS esistente, usando quindi la sessione stabilita per crittografare i messaggi di handshake. Questo processo consente di ristabilire le chiavi della sessione di crittografia senza terminare la sessione TLS (vedere la sezione "rinegoziazione della sessione TLS").

Sfortunatamente, dopo che TLS ha usato la rinegoziazione per un certo periodo di tempo, è stata individuata una vulnerabilità a un attacco man-in-the-Middle che sfruttava la funzionalità di rinegoziazione. Per chiudere la vulnerabilità, è stata introdotta l'estensione per l'indicazione di rinegoziazione sicura. In sostanza, l'estensione di rinegoziazione sicura utilizza l'hash dei messaggi completato dalla connessione stabilita per verificare che gli host originali partecipino all'handshake di rinegoziazione, in sostanza l'hash viene utilizzato come token di verifica nel presupposto che un utente malintenzionato non sia in grado di creare l'hash (che richiede l'accesso alle chiavi della sessione).

NetX Secure TLS gestisce automaticamente la rinegoziazione e usa l'estensione di rinegoziazione sicura per impostazione predefinita. Non è necessaria alcuna interazione con l'applicazione.

### <a name="server-name-indication"></a>Indicazione nome server

Durante l'handshake TLS, un client TLS prevede che un server remoto fornisca un certificato di identità in modo che il client possa autenticare il server. In alcuni casi, tuttavia, un server fornirà più servizi diversi con server "virtuali" diversi, ognuno con identità univoche. Nel caso di un singolo server con più identità, un client TLS può fornire un nome DNS specifico che verrà usato dal server per selezionare le credenziali appropriate, il meccanismo per fornire questo nome è l'estensione Indicazione nome server (SNI).

Per un'applicazione che usa l'estensione SNI, è necessaria una certa interazione. Per i client TLS, l'applicazione deve fornire un nome DNS da inviare al server remoto. Per i server TLS, l'applicazione deve leggere il nome DNS dall'estensione e selezionare un certificato appropriato da inviare di nuovo al client.

Le sezioni seguenti forniscono informazioni più dettagliate su come usare l'estensione SNI in NetX Secure TLS.

### <a name="sni-extension--tls-client"></a>Estensione SNI-client TLS

Un client TLS sicuro NetX che desidera usare l'estensione SNI deve fornire un nome DNS a TLS da fornire durante l'handshake. Questo nome deve essere inizializzato e fornito prima di avviare una sessione TLS poiché l'estensione viene inviata nel messaggio ClientHello che avvia il processo di handshake.

Il frammento di codice seguente illustra l'uso dell'estensione. Innanzitutto, un oggetto NX_SECURE_X509_DNS_NAME viene inizializzato con il nome del server desiderato. Quindi, prima di avviare la sessione TLS, il nome viene fornito a TLS usando l'API dell'estensione SNI. Una volta impostato il nome, non è richiesta alcuna azione aggiuntiva. Vedere le informazioni di riferimento sulle API nel capitolo 4  
  
Descrizione dei servizi NetX Secure per ulteriori informazioni sulle singole funzioni.

```C
/* The dns_name variable will contain our desired server name. */
UINT status;
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize the server DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, "www.example.com", 
                                            strlen("www.example.com"));


/* Initialize SNI extension in previously-initialized TLS Session. */
status = nx_secure_tls_session_sni_extension_set(&client_tls_session, &dns_name);

/* Now start the TLS session, starting with establishing the TCP connection – if 
   TLS is started before initializing the SNI extension, the extension will not be 
   sent in the ClientHello message! */
status = nx_tcp_client_socket_connect(&client_socket, IP_ADDRESS(1, 2, 3, 4), 443, 
                                      5 * NX_IP_PERIODIC_RATE);

status = nx_secure_tls_session_start(&client_tls_session, &client_socket, 
                                     NX_WAIT_FOREVER);
```
### <a name="sni-extension--tls-server"></a>Estensione SNI-server TLS

Sul lato server TLS, l'estensione SNI può essere elaborata dall'applicazione per selezionare le credenziali appropriate (ad esempio, certificate) da fornire al client remoto durante l'handshake. A tale scopo, l'applicazione deve fornire un callback di sessione che viene richiamato dopo la ricezione di un messaggio ClientHello.

Il codice di esempio per l'API nx_secure_tls_session_server_callback_set (vedere la pagina 122) illustra l'analisi di un'estensione SNI in ingresso usando un callback del server. In sostanza, il server TLS riceve un ClientHello e richiama il callback. Quindi, l'applicazione usa l'API *nx_secure_tls_session_sni_extension_parse* per analizzare i dati dell'estensione forniti al callback per trovare l'estensione SNI e restituire il nome DNS specificato (si noti che l'estensione supporta solo un singolo nome DNS). Una volta ottenuto il nome, l'applicazione lo usa per trovare e inviare il certificato di identità server appropriato (e la catena dell'emittente se applicabile).

### <a name="signature-algorithms-extension"></a>Estensione degli algoritmi di firma

Questa estensione è specifica di TLS 1,2 e consente a un client TLS di fornire un elenco di coppie di algoritmi di firma e hash accettabili che sono accettabili per la generazione e la verifica delle firme digitali. L'elenco viene generato automaticamente da NetX Secure TLS per i client TLS usando la tabella di crittografia fornita per *nx_secure_tls_session_create*. Non è necessaria alcuna interazione con l'applicazione.

## <a name="authentication-methods"></a>Authentication Methods

TLS fornisce il Framework per stabilire una connessione sicura tra due dispositivi su una rete non sicura, ma parte del problema sta conoscendo l'identità del dispositivo all'altra estremità della connessione. Senza un meccanismo per l'autenticazione dell'identità degli host remoti, diventa un'operazione semplice che un utente malintenzionato potrebbe rappresentare come un dispositivo attendibile.

Inizialmente, potrebbe sembrare che l'uso di indirizzi IP, gli indirizzi MAC hardware o DNS forniscono un livello di attendibilità relativamente elevato per l'identificazione degli host in una rete, ma con la natura della tecnologia TCP/IP e la facilità con cui gli indirizzi possono essere falsificati e le voci DNS danneggiate, ad esempio tramite l'avvelenamento della cache DNS, risulta evidente che TLS necessita di un ulteriore livello di protezione contro le identità fraudolente.

Esistono diversi meccanismi che possono fornire questo livello aggiuntivo di autenticazione per TLS, ma il più comune è il *certificato digitale.* Altri meccanismi includono chiavi precondivise (PSK) e schemi di password.

### <a name="digital-cerificates"></a>Certificati digitali

I certificati digitali sono il metodo più comune per autenticare un host remoto in TLS. In sostanza, un certificato digitale è un documento con una formattazione specifica che fornisce informazioni sull'identità per un dispositivo in una rete di computer.

TLS usa in genere un formato denominato X. 509, uno standard sviluppato dall'Unione di telecomunicazione internazionale, sebbene sia possibile usare altri formati di certificati se gli host TLS possono accettare il formato usato. X. 509 definisce un formato specifico per i certificati e varie codifiche che possono essere utilizzate per produrre un documento digitale. La maggior parte dei certificati X. 509 usati con TLS viene codificata usando una variante di ASN. 1, un altro standard di telecomunicazione. All'interno di ASN. 1 sono disponibili diverse codifiche digitali, ma la codifica più comune per i certificati TLS è lo standard Distinguished Encoding Rules (DER). DER è un subset semplificato delle regole di codifica di base ASN. 1 progettato per essere non ambiguo, semplificando l'analisi. In transito, i certificati TLS vengono in genere codificati in DER binario e questo è il formato previsto da NetX Secure per i certificati X. 509.

Sebbene i certificati binari in formato DER vengano usati nel protocollo TLS effettivo, possono essere generati e archiviati in una serie di codifiche diverse, con estensioni di file quali PEM, CRT e P12. Le diverse varianti vengono utilizzate da diverse applicazioni di produttori diversi, ma in genere possono essere convertite in DER utilizzando strumenti ampiamente disponibili.

La più comune delle codifiche alternative dei certificati è PEM. Il formato PEM (da Privacy-Enhanced mail) è una versione con codifica 64 della codifica DER utilizzata spesso in quanto la codifica produce testo stampabile che può essere facilmente inviato tramite posta elettronica o protocolli basati sul Web.

La generazione di un certificato per l'applicazione NetX Secure è generalmente al di fuori dell'ambito di questo manuale, ma lo strumento da riga di comando OpenSSL ([www.openssl.org](http://www.openssl.org)) è ampiamente disponibile ed è in grado di eseguire la conversione tra la maggior parte dei formati.

A seconda dell'applicazione, è possibile generare certificati, fornire certificati da un produttore o da un'organizzazione governativa oppure acquistare certificati da un'autorità di certificazione commerciale.

Per usare un certificato digitale nell'applicazione NetX Secure, è necessario innanzitutto convertire il certificato in un formato DER binario e, facoltativamente, convertire la chiave privata associata ("esponente privato" per RSA, ad esempio) in un formato binario, in genere una chiave RSA codificata der PKCS # 1 o una chiave ECC codificata DER. Al termine della conversione, è possibile caricare il certificato e la chiave privata nel dispositivo. Le opzioni possibili includono l'uso di un file system basato su Flash o la generazione di una matrice C dai dati (usando uno strumento come "XXD" da Linux) e la compilazione del certificato e della chiave nell'applicazione come dati costanti.

Una volta caricato il certificato nel dispositivo, è possibile usare l'API TLS per associare il certificato a una sessione TLS.

Per informazioni dettagliate ed esempi su come usare i certificati X. 509 con NetX Secure TLS, vedere la sezione "importazione di certificati X. 509 in NetX Secure".

Per ulteriori informazioni, fare riferimento ai seguenti servizi TLS nelle informazioni di riferimento sulle API:

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_add
- nx_secure_trusted_certificate_remove

### <a name="tls-client-certificate-specifics"></a>Specifiche del certificato client TLS

Le implementazioni client TLS in genere non richiedono il caricamento di un certificato "locale"<sup>14</sup> nel dispositivo. L'eccezione è rappresentata dal caso in cui l'autenticazione del certificato client è abilitata, ma questo è molto meno comune.

Per il caricamento di un client TLS è necessario che sia presente almeno un certificato "Trusted"<sup>15</sup> (è possibile che ne venga caricato altri se necessario) e che venga allocato spazio per un certificato "remoto"<sup>16</sup> .

Per ulteriori informazioni sull'aggiunta di certificati attendibili e sull'allocazione dello spazio per i certificati remoti, vedere le informazioni di riferimento sulle API TLS per i servizi seguenti: nx_secure_tls_remote_certificate_allocate, nx_secure_tls_trusted_certificate_add.

14. Un certificato "locale" è un certificato che identifica il dispositivo locale, ovvero fornisce informazioni sull'identità per il dispositivo su cui è caricata l'applicazione TLS.

15. Un certificato "attendibile" è un certificato che fornisce una base per l'attendibilità e l'autenticazione del dispositivo remoto, direttamente o tramite un'infrastruttura a chiave pubblica (PKI). La radice della catena di trust è in genere denominata "autorità di certificazione" o certificato della CA.

16. Un certificato "remoto" si riferisce al certificato inviato dall'host remoto durante l'handshake TLS. Fornisce l'identità per quell'host remoto ed è autenticato confrontandolo con un certificato "attendibile" nel dispositivo locale.

### <a name="tls-server-certificate-specifics"></a>Specifiche del certificato del server TLS

Le implementazioni del server TLS in genere non richiedono il caricamento di certificati "Trusted" sul dispositivo o sui certificati remoti da allocare. L'eccezione è rappresentata dal fatto che l'autenticazione del certificato client è abilitata (questo è meno comune).

Un server TLS richiede il caricamento di un certificato "locale" in modo che il server possa fornirlo al client remoto durante l'handshake TLS per autenticare il server nel client.

Per ulteriori informazioni sul caricamento dei certificati locali per l'utilizzo con le applicazioni server TLS NetX, vedere le informazioni di riferimento sulle API per i servizi seguenti: 
- nx_secure_tls_local_certificate_add, 
- nx_secure_tls_local_certificate_remove.

### <a name="pre-shared-keys-psk"></a>Chiavi precondivise (PSK)

Un meccanismo alternativo per fornire l'autenticazione di identificazione in TLS è il concetto di chiavi precondivise (PSK). L'uso di un ciphersuite PSK Elimina la necessità di eseguire le operazioni di crittografia a chiave pubblica con utilizzo intensivo del processore, un vantaggio per i dispositivi embedded con vincoli di risorse. La PSK sostituisce il certificato nell'handshake TLS e viene usato al posto del segreto pre-master crittografato per la generazione della chiave di sessione TLS.

I ciphersuites di PSK sono limitati nel senso che un segreto condiviso deve essere presente in entrambi i dispositivi prima che sia possibile stabilire una sessione TLS. Ciò significa che i dispositivi devono essere stati caricati con tale segreto usando un mezzo sicuro diverso da una connessione PSK TLS. precondivise può essere aggiornato tramite una connessione PSK TLS, ma il dispositivo deve necessariamente iniziare con una PSK che viene caricata tramite un altro meccanismo. Ad esempio, un dispositivo sensore e il relativo dispositivo gateway potrebbero essere caricati con precondivise nella Factory prima della spedizione oppure è possibile usare una connessione TLS standard (con un certificato) per caricare la PSK.

Le ciphersuites PSK sono disponibili in un paio di forme, descritte in RFC 4279. Il primo usa le chiavi RSA o Diffie-Hellman utilizzate allo stesso modo delle chiavi pubbliche trasmesse nel certificato negli handshake TLS standard. Il secondo formato, che è più usato in un ambiente con vincoli di risorse, usa un PSK usato per generare direttamente le chiavi della sessione (per l'uso da parte di AES, ad esempio), evitando l'uso delle operazioni RSA o Diffie-Hellman onerose.

NetX Secure supporta la seconda forma di PSK ciphersuites, consentendo alle applicazioni di rimuovere tutto il codice di crittografia a chiave pubblica e l'utilizzo della memoria. La PSK stessa non è una chiave AES, ma può essere considerata come una password da cui vengono generate le chiavi effettive. Esistono alcune restrizioni relative al valore di PSK, sebbene i valori più lunghi forniscano maggiore sicurezza (come per le password).

Per usare PSK con l'applicazione NetX Secure, è necessario innanzitutto definire la macro globale **NX_SECURE_ENABLE_PSK_CIPHERSUITES**. Questa operazione viene in genere eseguita tramite le impostazioni del compilatore, ma la definizione può anche essere inserita nel file di intestazione nx_secure_tls. h. Con la macro definita, il supporto di PSK ciphersuite verrà compilato nell'applicazione NetX Secure TLS.

Con il supporto di PSK abilitato, è possibile usare l'API TLS per configurare precondivise per l'applicazione. Ogni PSK richiederà un valore PSK (il segreto effettivo "Key"-Mantieni questo valore safe), un valore "Identity" usato per identificare il PSK specifico e un "hint di identità" usato da un server TLS per scegliere un particolare valore PSK.

La PSK può essere qualsiasi valore binario perché non viene mai inviato tramite una connessione di rete. La PSK può essere di qualsiasi valore fino a 64 byte di lunghezza.

L'identità e l'hint devono essere stringhe di caratteri stampabili formattate con UTF-8. I valori Identity e hint possono avere una lunghezza fino a 128 byte.

Identity e PSK formano una coppia univoca che viene caricata in ogni dispositivo della rete che deve comunicare tra loro.

Il "suggerimento" viene usato principalmente per la definizione di profili applicazione specifici per raggruppare precondivise in base alla funzione o al servizio. Questi valori devono essere concordati in anticipo e dipendono dall'applicazione. Ad esempio, l'applicazione server della riga di comando OpenSSL (con la funzionalità PSK abilitata) usa la stringa predefinita "Client_identity", che deve essere fornita da un client TLS per continuare con l'handshake TLS.

Per altre informazioni su precondivise, vedere le informazioni di riferimento sulle API NetX sicure per i servizi seguenti: nx_secure_tls_client_psk_set, nx_secure_tls_psk_add.

## <a name="importing-x509-certificates-into-netx-secure"></a>Importazione di certificati X. 509 in NetX Secure

Per la maggior parte delle connessioni TLS su Internet sono necessari certificati digitali. I certificati forniscono un metodo per l'autenticazione di host sconosciuti in precedenza tramite Internet tramite l'utilizzo di intermediari attendibili, in genere detti *autorità di certificazione* o CA. Per connettere il dispositivo NetX Secure a un servizio cloud commerciale, ad esempio Amazon Web Services, sarà necessario importare i certificati nell'applicazione eseguendone il caricamento nel dispositivo.

Insieme ai certificati, a volte è necessaria anche una *chiave privata* associata al certificato. In alcune applicazioni, ad esempio client TLS quando non si usa l'autenticazione del certificato client, il certificato da solo sarà sufficiente, ma se il certificato viene usato per identificare il dispositivo, sarà necessaria una chiave privata. Le chiavi private vengono in genere generate quando si crea il certificato e vengono archiviate in un file separato, spesso crittografate con una password.

### <a name="certificate-types"></a>Tipi di certificato

I certificati digitali vengono in genere usati per identificare le entità in una rete, ma a seconda di quale applicazione avranno proprietà leggermente diverse.

### <a name="local-certificates"></a>Certificati locali

Ai fini di questa documentazione, si fa riferimento a "certificati locali" come i certificati che forniscono un'identità per il dispositivo locale (un altro nome possibile può essere "certificato dispositivo"). Questi certificati verranno forniti a un host remoto quando l'host remoto vuole autenticare il dispositivo locale.

### <a name="remote-certificates"></a>Certificati remoti

In questa documentazione, "certificati remoti" si riferisce ai certificati forniti da un host remoto durante l'handshake TLS quando applicabile. È necessario allocare spazio per questi certificati oppure NetX Secure non sarà in grado di analizzarli e completare l'handshake TLS.

### <a name="signing-certificates"></a>Certificati di firma

Un "certificato di firma" viene usato per firmare digitalmente altri certificati o dati ai fini dell'autenticazione. Questi certificati possono essere certificati intermedi o radice in un'infrastruttura a chiave pubblica (PKI) e in genere non vengono usati per identificare singoli dispositivi o host.

### <a name="root-ca-certificates"></a>Certificati CA radice

"I certificati CA radice" sono certificati di firma che forniscono la base di un'infrastruttura a chiave pubblica e sono autofirmati, anziché essere firmati da un altro certificato di firma. Almeno un certificato CA radice è in genere necessario per un client TLS per verificare i server remoti.

### <a name="certificate-formats"></a>Formati dei certificati

I certificati digitali sono semplicemente file contenenti dati strutturati codificati utilizzando la sintassi ASN. 1. Esistono tuttavia diversi formati in cui è possibile archiviare i certificati ed è importante avere il formato corretto prima di caricare un certificato in un'applicazione NetX Secure.

I formati più comuni per i certificati sono DER e PEM. DER (per *Distinguished Encoding Rules*, un formato ASN. 1) è il formato binario utilizzato da TLS durante l'esecuzione dell'handshake iniziale. PEM (da *Privacy Enhanced Mail*) è una versione con codifica base 64 del formato der adatto per la posta elettronica o l'invio tramite HTTP sul Web. Diversi fornitori utilizzano estensioni di nome file diverse per i certificati, ad esempio ". pem" o ". CRT" per i certificati PEM e ". der" per i certificati DER. Se si dispone di un certificato che non è chiaro del formato utilizzato, l'apertura del file in un editor di testo consentirà di determinare il tipo poiché i file DER sono binari codificati e i file PEM sono testo ASCII normale che iniziano con l'intestazione "-----BEGIN CERTIFICAte-----".

NetX Secure richiede che il certificato sia in formato DER binario, quindi è necessario convertire il certificato in formato DER prima dell'importazione. Questa operazione può essere eseguita con strumenti prontamente disponibili, ad esempio OpenSSL.

Se è necessaria una chiave privata per l'applicazione, il file di chiave verrà codificato usando PEM o DER in un formato specifico (PKCS # 1 per RSA, RFC 5915 per ECC). Il file di chiave privata deve essere convertito in DER prima di essere importato.

I comandi OpenSSL seguenti sono forniti come esempio per la conversione di certificati e file di chiave RSA nel formato DER richiesto da NetX Secure (ECC è simile: fare riferimento alla documentazione di OpenSSL).

```C
openssl x509 -inform PEM -in <certificate> -outform DER -out cert.der
openssl x509 -inform PEM -in <root CA cert> -outform DER -out CA_cert.der
openssl rsa -inform PEM -in <private key> -outform DER -out private.key
```
### <a name="private-keys-and-certificates"></a>Chiavi private e certificati

Per i certificati che identificano un dispositivo, è necessario caricare la chiave privata associata insieme al certificato. La chiave privata (che può essere per uno degli algoritmi a chiave pubblica, ad esempio RSA, Diffie-Hellman o Elliptic-Curve crittografia) viene usata da un server TLS per decrittografare il materiale della chiave in ingresso ("pre-master secret") da un client TLS, eseguendo quindi l'autenticazione al client. Per un client TLS, se viene fornito un certificato di identità (un certificato con la chiave privata associata) e un server richiede un certificato client, la chiave privata viene usata per autenticare il client. nel caso di RSA, il client crittografa un token usando la chiave privata che il server decrittografa usando la chiave pubblica del client, fornita nel certificato client (Diffie-Hellman e l'autenticazione ECC avviene in modo simile, ma i dettagli sono leggermente diversi).

In NetX Secure il servizio *nx_secure_x509_certificate_initialize* viene usato per inizializzare un certificato X. 509 (vedere la sezione "caricamento di certificati nel dispositivo" per altre informazioni) e, facoltativamente, associare una chiave privata a tale certificato.

Se viene fornita una chiave privata, il certificato viene contrassegnato come certificato "Identity" usato per identificare il dispositivo. La chiave viene passata come BLOB binario contiguo e come lunghezza, con un tipo di chiave associato. Il tipo di chiave dipende dal tipo di chiave, ad esempio RSA, ECC e così via, e dal formato (ad esempio PKCS # 1 DER). Se non viene fornita alcuna chiave, il valore NX_SECURE_X509_KEY_TYPE_NONE (valore 0x0) può essere passato a indicare che non è stata fornita alcuna chiave (una lunghezza pari a 0 e un puntatore NX_NULL per il parametro dati otterrà lo stesso effetto).

La tabella seguente illustra i tipi di chiave noti per NetX Secure e l'identificatore di tipo associato da passare in *nx_secure_x509_certificate_initialize*. Verranno aggiunti altri tipi di chiave perché vengono aggiunti altri algoritmi di crittografia a NetX Secure.

| Identificatore                              | Algoritmo | Formato   | Codifica | Valore |
| --------------------------------------- | --------- | -------- | -------- | ----- |
| NX_SECURE_X509_KEY_TYPE_NONE            | nessuno      | N/D      | N/D      | 0x0   |
| NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER   | RSA       | PKCS # 1   | DER      | 0x1   |
| NX_SECURE_X509_KEY_TYPE_EC_DER          | ECDSA     | RFC 5915 | DER      | 0x2   |

### <a name="user-defined-private-key-types"></a>Tipi di chiave privata definiti dall'utente

I valori degli identificatori del tipo di chiave per il servizio *nx_secure_x509_certificate_initialize* regolano le azioni intraprese quando viene fornita la chiave privata. Per i tipi noti, i valori sono compresi nell'intervallo 0x0000 0000 – 0x0000 FFFF (ultimi 16 bit di un Unsigned Integer a 32 bit). Per le piattaforme con tipi di chiave personalizzati<sup>17</sup> (come nel caso di alcuni motori di crittografia basati su hardware), un tipo di chiave definito dall'utente compreso nell'intervallo 0x0000 1000-0xFFFF FFFF (primi 16 bit diversi da zero) può essere passato come tipo di chiave. Se viene impostato uno dei primi 16 bit del tipo di chiave, i dati della chiave privata vengono passati direttamente alla routine di crittografia appropriata, ad esempio RSA, fornita nella tabella TLS ciphersuite. I tipi di chiave definiti dall'utente non vengono analizzati o elaborati in altro modo prima di essere passati alla routine di crittografia. Inoltre, il tipo di chiave definito dall'utente verrà passato alla routine di crittografia in modo che sia possibile gestire qualsiasi elaborazione appropriata a tale livello.

Si noti che i tipi di chiave definiti dall'utente vengono in genere usati per piattaforme hardware specifiche che usano dati di chiave personalizzati (probabilmente crittografati). In genere ciò implica che i dati delle chiavi vengono generati o codificati usando un meccanismo specifico del fornitore dell'hardware (o nel caso di uno standard come PKCS # 11, uno standard specifico). Per ulteriori informazioni, consultare la documentazione della piattaforma hardware.

17. I tipi di chiave definiti dall'utente richiedono una routine di crittografia personalizzata corrispondente per gestire il formato della chiave personalizzata. La routine di crittografia deve avere un algoritmo corrispondente (ad esempio RSA) e essere passata in TLS nella tabella ciphersuite. 

### <a name="loading-certificates-onto-your-device"></a>Caricamento dei certificati nel dispositivo

Qualsiasi metodo per il caricamento di un file nel dispositivo sarà sufficiente per importare i certificati.

Il metodo più semplice per il caricamento di un certificato consiste nel convertire i dati binari con codifica DER in una matrice C e compilarli nell'applicazione come costante. Questa operazione può essere eseguita facilmente con strumenti come "XXD" in Linux (con l'opzione "-i").

In alternativa, è possibile caricare il certificato in un filesystem flash o in altre opzioni di archiviazione, purché sia possibile passare un puntatore ai dati del certificato nell'API NetX Secure.

### <a name="certificate-files-needed-for-netx-secure"></a>File di certificato necessari per NetX Secure

I file di certificato che è necessario importare dipendono dall'applicazione. In generale, i server TLS richiedono un certificato per identificare il dispositivo e i client TLS richiedono uno o più *certificati attendibili* per autenticare i server remoti. La tabella seguente illustra i certificati necessari per alcune applicazioni TLS diverse.

| **Opzioni/funzionalità TLS**                     | **Certificati/chiavi necessarie (minima)**              |
| ------------------------------------------------- | --------------------------------------------------- |
| Client TLS                                        | Certificato CA radice                                 |
| Server TLS                                        | Certificato locale, chiave privata per il certificato |
| Server TLS con autenticazione del certificato client | Certificato locale, chiave privata, CA radice             |
| Client TLS con autenticazione del certificato client | Certificato locale, chiave privata, CA radice             |
| Client o server TLS con solo chiavi precondivise    | None (PSK usato al posto dei certificati)             |

I servizi rilevanti per il caricamento dei certificati sono i seguenti:

| **Nome API**                                   | **Scopo**                                            |
| ---------------------------------------------- |------------------------------------------------------- |
| nx_secure_x509_certificate_initialize      | Deve essere chiamato per tutti i certificati per popolare la struttura di NX_SECURE_X509_CERT con i dati del certificato e la chiave privata. |
| nx_secure_tls_local_certificate_add       | Aggiungere un certificato locale a una sessione TLS per identificare il dispositivo.                                                                |
| nx_secure_tls_local_certificate_remove    | Rimuovere un certificato locale da una sessione TLS.                                                                                   |
| nx_secure_tls_remote_certificate_allocate | Allocare spazio per un certificato remoto (chiamato con una NX_SECURE_X509_CERT non inizializzata).                                   |
| nx_secure_tls_trusted_certificate_add     | Aggiungere un certificato a una sessione TLS come certificato attendibile per l'autenticazione di host remoti.                                     |
| nx_secure_tls_trusted_certificate_remove  | Rimuovere un certificato attendibile da una sessione TLS.                                                                                 |

### <a name="working-with-aws-iot-certificates"></a>Uso dei certificati di AWS

Nell'interfaccia Amazon Web Services Internet, selezionare "sicurezza" dal menu sidebar e selezionare "certificati". Creare un nuovo certificato e seguire le istruzioni per scaricare il nuovo certificato del dispositivo.

Una volta scaricati i certificati, sarà necessario convertirli in formato DER usando OpenSSL o un'utilità simile.

Nota: AWS fornirà anche un file di chiave pubblica. La chiave pubblica è contenuta nel certificato del dispositivo locale, pertanto non è necessario importarla nell'applicazione.

Ad esempio, di seguito sono riportati i comandi per convertire il certificato del dispositivo locale e la relativa chiave privata nel formato DER da usare con NetX Secure:

```C
openssl x509 -inform PEM -in <certificate> -outform DER -out cert.der
openssl x509 -inform PEM -in <root CA cert> -outform DER -out CA_cert.der
openssl rsa -inform PEM -in <private key> -outform DER -out private.key
```
I file convertiti possono essere importati nell'applicazione seguendo le istruzioni precedenti.

## <a name="x509-certificate-validation-in-netx-secure"></a>Convalida del certificato X. 509 in NetX Secure 

Quando si usa TLS con certificati X. 509 per l'identificazione e la verifica dell'host, è importante comprendere il modo in cui tali certificati vengono effettivamente convalidati. Sebbene la specifica TLS non fornisca istruzioni dettagliate su come convalidare un certificato, fa riferimento alla specifica X. 509 (RFC 5280). In generale, si prevede che TLS eseguirà almeno la convalida di base sui certificati in ingresso (i certificati forniti dall'host remoto durante l'handshake TLS) e che NetX Secure TLS non sia diverso.

### <a name="basic-x509-validation"></a>Convalida X. 509 di base

Per tutti i certificati in ingresso, NetX Secure TLS eseguirà la convalida di base del percorso X. 509. Il processo implica la verifica della firma digitale di ogni certificato rispetto al certificato dell'autorità emittente, che può essere fornito dall'host remoto o situato nell'archivio certificati attendibile (vedere la sezione "importazione di certificati X. 509 in NetX Secure" per altre informazioni sull'importazione di certificati attendibili). Il processo di convalida viene ripetuto in modo ricorsivo sui certificati dell'autorità emittente fino a quando non viene raggiunto un certificato attendibile o termina la catena (con un certificato autofirmato o un certificato dell'autorità emittente mancante). Se viene raggiunto un certificato attendibile, il certificato viene verificato; in caso contrario, viene rifiutato. Inoltre, in ogni fase del processo di verifica, la data di scadenza di ogni certificato viene verificata rispetto al tempo fornito dalla funzione timestamp applicazione (vedere il servizio "nx_secure_tls_session_time_function_set" per altre informazioni).

La specifica X. 509 fornisce anche un algoritmo per supportare i "criteri", che sono identificatori presenti in un'estensione X. 509 che possono essere controllati durante la convalida del percorso. NetX Secure considera attualmente i certificati X. 509 come se fosse definita l'opzione "anyPolicy", ovvero tutti i criteri sono accettabili e il controllo facoltativo dei criteri non viene eseguito. L'implementazione di NetX Secure X. 509 può essere aumentata con questa funzionalità in una versione futura. Per il momento, è possibile ottenere l'estensione dei criteri da un certificato usando l'API *nx_secure_x509_extension_find* .

Una volta completata la convalida del percorso di base, TLS richiamerà il callback di verifica del certificato fornito dall'applicazione usando l'API *nx_secure_tls_session_certificate_callback_set* . Se non viene fornito alcun callback, il certificato viene considerato attendibile dopo la convalida del percorso riuscito. Se viene fornito un callback, il callback eseguirà qualsiasi convalida aggiuntiva del certificato richiesto dall'applicazione. Il valore restituito dal callback viene usato per determinare se continuare con l'handshake TLS o per interrompere l'handshake a causa di un errore di convalida.

Il callback viene richiamato con un puntatore alla sessione TLS pertinente e un puntatore NX_SECURE_X509_CERT al certificato da convalidare. Tra la sessione TLS e il certificato, l'applicazione dispone di tutti i dati necessari da TLS per eseguire verifiche di verifica aggiuntive.

Per semplificare la convalida aggiuntiva, NetX Secure fornisce routine X. 509 per alcune operazioni comuni di convalida, tra cui la convalida DNS e il controllo dell'elenco di revoche di certificati. Tutte queste routine sono adatte per l'uso all'interno del callback di verifica del certificato, ma possono essere usate anche per eseguire il controllo non in linea dei certificati X. 509.

Nella tabella seguente sono riepilogate le funzioni di supporto disponibili per l'elaborazione di certificati X. 509. Le spiegazioni più dettagliate per le operazioni sono disponibili nelle sezioni seguenti e nella Guida di riferimento alle API del capitolo 4  
  
La descrizione di NetX Secure Services fornisce dettagli aggiuntivi sulle routine specifiche.

| **Nome API**                             | **Descrizione**                               |
| ---------------------------------------- | -------------------------------------- |
| nx_secure_x509_common_name_dns_check               | Verificare il nome comune del soggetto X. 509 e SubjectAltName rispetto a un nome DNS previsto |
| nx_secure_x509_crl_revocation_check                 | Verificare la presenza di un certificato revocato in un elenco di revoche di certificati X. 509 (CRL)       |
| nx_secure_x509_extended_key_usage_extension_parse | Analizza e trova un OID di utilizzo chiave esteso specifico in un certificato                   |
| nx_secure_x509_key_usage_extension_parse           | Analizzare e restituire l'utilizzo della chiave bit in un certificato                            |
| nx_secure_x509_extension_find                        | Trovare e restituire i dati ASN. 1 con codifica DER non elaborati per un'estensione specifica.            |

Funzioni helper X. 509 da usare nel callback di verifica del certificato

### <a name="x509-extensions"></a>Estensioni X. 509

La specifica X. 509 descrive una serie di "estensioni" che possono essere utilizzate per fornire informazioni aggiuntive che possono essere utilizzate nella verifica dei certificati. Nella maggior parte dei casi, queste estensioni sono facoltative e non sono necessarie per la convalida sicura di un certificato digitale rispetto a un certificato radice attendibile. Tuttavia, NetX Secure supporta alcune estensioni di base. Il supporto per estensioni aggiuntive può essere aggiunto nelle versioni future.

Le estensioni attualmente supportate sono elencate nella tabella seguente:

| Nome estensione           | Descrizione                                                                   | API pertinente                                             |
| ------------------------ | ----------------------------------------------------------------------------- | -------------------------------------------------------- |
| Utilizzo chiavi                | Fornisce usi accettabili per la chiave pubblica di un certificato in un bit         | nx_secure_x509_key_usage_extension_parse           |
| Utilizzo chiavi avanzato       | Fornisce altri usi accettabili per la chiave pubblica di un certificato tramite OID | nx_secure_x509_extended_key_usage_extension_parse |
| Nome alternativo soggetto | Fornisce nomi DNS alternativi rappresentati anche dal certificato   | nx_secure_x509_common_name_dns_check               |

### <a name="unsupported-x509-extensions"></a>Estensioni X. 509 non supportate

NetX Secure X. 509 implementazione fornisce un servizio per estrarre anche le estensioni non supportate: *nx_secure_x509_extension_find*. Questa API è destinata agli utenti avanzati perché richiede la conoscenza di ASN. 1 codificato DER per analizzare i dati restituiti. Viene usato internamente per estrarre le estensioni supportate, ma viene fornito per praticità nello sviluppo di supporto personalizzato per le estensioni X. 509.

Per utilizzare nx_secure_x509_extension_find, viene passato un NX_SECURE_X509_EXTENSION, insieme al certificato e a un ID estensione, ovvero una rappresentazione Integer della stringa OID a lunghezza variabile per un tipo di estensione noto. Un elenco completo di OID supportate per le estensioni X. 509 è disponibile nella Guida di riferimento alle API per nx_secure_x509_extension_find nella pagina 178.

La struttura NX_SECURE_X509_EXTENSION viene definita nel modo seguente:

```C
typedef struct NX_SECURE_X509_EXTENSION_STRUCT
{
    /* Identifier (maps to OID) for this extension. */
    USHORT nx_secure_x509_extension_id;

    /* Critical flag - boolean value. */
    USHORT nx_secure_x509_extension_critical;

    /* Pointer to DER-encoded extension data. */
    const UCHAR *nx_secure_x509_extension_data;
    ULONG        nx_secure_x509_extension_data_length;
} NX_SECURE_X509_EXTENSION;
```
Quando il servizio viene restituito correttamente, la struttura viene popolata con i dati rilevanti del certificato. Il campo nx_secure_x509_extension_id viene in genere usato per scopi interni, ma verrà popolato con la rappresentazione dell'intero OID pertinente. Il campo nx_secure_x509_extension_critical espone il valore del flag di estensione critico X. 509 (booleano). I campi nx_secure_x509_extension_data e nx_secure_x509_extension_data_length contengono un puntatore ai dati ASN. 1 con codifica DER per l'estensione e rispettivamente la lunghezza di tali dati.

L'analisi effettiva dei dati ASN. 1 dell'estensione esula dall'ambito di questo documento, ma se si ha accesso all'origine NetX Secure TLS è possibile vedere come viene eseguita l'analisi quando viene chiamato nx_secure_x509_extension_find per le estensioni supportate.

### <a name="x509-dns-validation"></a>Convalida DNS X. 509

Un'operazione di convalida dei certificati comune in TLS prevede il controllo del nome del dominio di Top-Level di un host remoto rispetto al certificato X. 509 fornito da tale host durante l'handshake TLS. Questa operazione consente di verificare che il certificato corrisponda effettivamente al server host che lo ha fornito, presupponendo che la ricerca DNS possa essere considerata attendibile. In NetX Secure TLS questa funzionalità viene fornita dal servizio **nx_secure_x509_common_name_dns_check**, che accetta il certificato e una stringa contenente la parte di TLD dell'URL usato per accedere all'host. Il TLD viene confrontato con il campo del nome comune del certificato e, se corrisponde, viene restituito NX_SUCCESS. Se il nome comune non corrisponde, la routine verificherà anche l'esistenza dell'estensione del certificato X. 509 *SubjectAltName*. Se è presente un subjectAltName, vengono controllate anche tutte le voci di DNSName nell'estensione rispetto al TLD fornito. Anche in questo caso, se viene restituita una corrispondenza, viene restituito NX_SUCCESS. Se non viene trovata alcuna corrispondenza, viene restituito un errore adatto per restituire il callback di convalida del certificato.

### <a name="x509-key-usage-and-extended-key-usage-extensions"></a>Utilizzo chiavi X. 509 ed estensioni utilizzo chiavi avanzato

Le estensioni utilizzo chiavi X. 509 e utilizzo chiavi avanzato forniscono informazioni sulla modalità di utilizzo della chiave pubblica di un certificato durante l'autenticazione del certificato. L'utilizzo della chiave viene fornito dall'autorità emittente del certificato quando il certificato viene firmato e emesso. L'utilizzo della chiave può essere utilizzato da un host TLS per verificare che il certificato sia autorizzato a essere utilizzato per autenticare un host TLS remoto ed eseguire altre operazioni.

L'estensione utilizzo chiavi è costituita da un bit semplice in cui ognuno dei bit rappresenta un utilizzo chiave specifico. Un elenco completo di questi valori è disponibile nella Guida di riferimento alle API per *nx_secure_x509_key_usage_extension_parse* nella pagina 183. Per una descrizione più completa dei bit di utilizzo chiave e dei relativi significati, vedere la specifica RFC 5280, sezione 4.2.1.3.

L'estensione utilizzo chiavi avanzato, ad esempio l'estensione utilizzo chiave, fornisce informazioni di utilizzo chiave accettabile. Tuttavia, per supportare utilizzi arbitrari, l'estensione utilizzo chiavi avanzato usa OID anziché bit. Quando si analizza un'estensione per l'utilizzo delle chiavi estesa in NetX Secure X. 509, un numero intero che rappresenta l'OID viene fornito dall'applicazione. il servizio *nx_secure_x509_extended_key_usage_extension_parse* restituirà quindi se tale OID è presente. Un elenco completo dei OID supportati per l'utilizzo chiavi avanzato è disponibile nella Guida di riferimento alle API per *nx_secure_x509_extended_key_usage_extension_parse* nella pagina 175. Per una descrizione più completa di OID e dei relativi significati, vedere la RFC 5280, sezione 4.2.1.12.

### <a name="x509-crl-revocation-status-checking"></a>Verifica dello stato di revoca CRL X. 509

X. 509 fornisce un meccanismo denominato *elenco di revoche di certificati* (CRL) che consente a un'autorità di firma digitale del certificato di revocare la validità dei certificati firmati. Qualsiasi applicazione che deve verificare i certificati da un'autorità di firma può ottenere un CRL e confrontare eventuali certificati firmati da tale autorità (emittente) rispetto al CRL per verificare se il relativo stato è stato revocato per qualche motivo, ad esempio una chiave privata compromessa. In questo modo, l'applicazione può evitare l'uso di certificati potenzialmente pericolosi che superano altri controlli di convalida del certificato.

Il recupero di un CRL viene eseguito da un'applicazione scaricando l'elenco con codifica DER da un server predefinito o con altri mezzi. Il programma di installazione effettivo varia a seconda dell'autorità emittente, quindi NetX Secure non fornisce un meccanismo per ottenere i CRL, ma fornisce una routine per verificare un certificato in base a un CRL, **nx_secure_x509_crl_revocation_check**.

L'API accetta un CRL con codifica DER, un archivio certificati, ad esempio quello in una sessione TLS, da controllare e il certificato da controllare. La routine convalida innanzitutto l'elenco CRL rispetto all'archivio attendibile (parte dell'archivio certificati fornito dall'applicazione). Questo è importante per la protezione da CRL fraudolenti usati per gli attacchi Denial of Service e stabilisce che l'elenco CRL è effettivamente dall'emittente appropriato. Dopo la convalida CRL, l'autorità emittente viene controllata: se l'emittente del CRL non corrisponde all'emittente del certificato, il CRL non è valido per il certificato e viene restituito un errore. L'applicazione deve determinare se l'handshake TLS può continuare a questo punto. Se le autorità emittenti corrispondono, viene eseguita la ricerca del numero di serie del certificato da convalidare nel CRL. Se il numero di serie è presente nell'elenco, viene restituito un errore che indica che il certificato è stato revocato. Se non viene trovata alcuna corrispondenza, viene restituito NX_SUCCESS.

## <a name="client-certificate-authentication-in-netx-secure-tls"></a>Autenticazione del certificato client in NetX Secure TLS

Quando si usa l'autenticazione del certificato X. 509, per il protocollo TLS è necessario che l'istanza del server TLS fornisca un certificato per l'identificazione, ma per impostazione predefinita non è necessario che l'istanza del client TLS fornisca un certificato per l'autenticazione, usando invece un'altra forma di autenticazione, ad esempio una combinazione di nome utente/password. Questo corrisponde all'uso più comune di TLS in Internet per i siti Web. Ad esempio, un sito di vendita al dettaglio online deve dimostrare a un potenziale cliente che utilizza un Web browser che il server è legittimo, ma l'utente utilizzerà un account di accesso/password per accedere a un account specifico.

Tuttavia, il caso predefinito non è sempre auspicabile, quindi TLS può facoltativamente consentire all'istanza del server TLS di richiedere un certificato dal client remoto. Quando questa funzionalità è abilitata, il server TLS invierà un messaggio CertificateRequest al client TLS durante l'handshake. Il client deve rispondere con un certificato autonomo e un messaggio CertificateVerify contenente un token crittografico per dimostrare che il client possiede la chiave privata corrispondente associata a tale certificato. Se la verifica ha esito negativo o il certificato non è connesso a un certificato attendibile nel server, l'handshake TLS ha esito negativo.

Esistono due casi distinti per l'autenticazione del certificato client in TLS: le sezioni seguenti illustrano entrambi i casi.

### <a name="client-certificate-authentication-for-tls-clients"></a>Autenticazione del certificato client per client TLS

Un client TLS può tentare una connessione a un server che richiede un certificato per l'autenticazione client. In questo caso il client deve fornire un certificato al server e verificare che sia proprietario della chiave privata corrispondente o che il server interromperà l'handshake TLS.

In NetX Secure TLS non esiste alcuna configurazione speciale per supportare questa funzionalità, ma l'applicazione dovrà fornire un certificato di identificazione locale per l'istanza del client TLS usando il servizio *nx_secure_tls_local_certificate_add* . Se l'applicazione non fornisce alcun certificato ma il server remoto usa l'autenticazione del certificato client e richiede un certificato, l'handshake TLS avrà esito negativo. Il certificato fornito alla sessione TLS con *nx_secure_tls_local_certificate_add* deve essere riconosciuto dal server remoto per completare l'handshake TLS.

### <a name="client-certificate-authentication-for-tls-servers"></a>Autenticazione del certificato client per i server TLS

Il caso del server TLS per l'autenticazione del certificato client è leggermente più complesso rispetto al case client TLS perché la funzionalità è facoltativa. In questo caso, il server TLS deve richiedere specificamente un certificato dal client TLS remoto, quindi elaborare il messaggio CertificateVerify per verificare che il client remoto sia proprietario della chiave privata corrispondente, quindi il server deve verificare che il certificato fornito dal client possa essere tracciato a un certificato nell'archivio certificati attendibili locale.

In NetX Secure TLS istanze del server, l'autenticazione del certificato client è controllata da <br>
il *client della <span class="underline"> _</span> sessione <span class="underline">_</span>TLS <span class="underline"> _</span> Secure <span class="underline">_</span>TLS <span class="underline"> _</span> verifica <span class="underline">_</span>Abilita* e<br>
*<span class="underline"> _</span> verifica <span class="underline">_</span>della disabilitazione dei servizi da client della <span class="underline"> _</span> sessione <span class="underline">_</span>TLS <span class="underline"> _</span> sicura <span class="underline">_</span>* .

Per abilitare l'autenticazione del certificato client, un'applicazione deve chiamare<br>
*<span class="underline"> _</span> verificare <span class="underline">_</span>che il client della <span class="underline"> _</span> sessione <span class="underline">_</span>TLS <span class="underline"> _</span> <span class="underline">_ sicura</span>sia abilitato* con l'istanza della sessione del server TLS prima di chiamare *nx_secure_tls_session_start*. Si noti che la chiamata a questo servizio in una sessione TLS utilizzata per le connessioni client TLS non avrà alcun effetto.

Quando è abilitata l'autenticazione del certificato client, il server TLS richiede un certificato dal client TLS remoto durante l'handshake TLS. In NetX Secure TLS server, il certificato client viene verificato rispetto all'archivio dei certificati attendibili creati con *nx <span class="underline"> _</span> <span class="underline">_ secure_tls</span><span class="underline"> _</span> certificato <span class="underline">_</span>attendibile aggiungere* dopo la catena dell'emittente X. 509. Il client remoto deve fornire una catena che connette il certificato di identità a un certificato nell'archivio attendibile oppure l'handshake TLS avrà esito negativo. Inoltre, se l'elaborazione del messaggio CertificateVerify ha esito negativo, anche l'handshake TLS avrà esito negativo.

I metodi di firma usati per il metodo CertificateVerify sono corretti per TLS versione 1,0 e TLS versione 1,1 e sono specificati dal server TLS in TLS versione 1,2. Per TLS 1,2, i metodi di firma supportati in genere seguono i metodi pertinenti forniti nella tabella del metodo crittografico, ma in genere RSA con SHA-256 (vedere la sezione "crittografia in NetX Secure TLS" per altre informazioni sull'inizializzazione di TLS con i metodi di crittografia).

## <a name="cryptography-in-netx-secure-tls"></a>Crittografia in NetX Secure TLS

TLS definisce un protocollo in cui è possibile usare la crittografia per proteggere le comunicazioni di rete. Per questo motivo, lascia che la crittografia effettiva venga usata in modo abbastanza ampio per gli utenti TLS. La specifica richiede l'implementazione di un solo ciphersuite: nel caso di TLS 1,2, ciphersuite è TLS_RSA_WITH_AES_128_CBC_SHA, che indica l'uso di RSA per le operazioni a chiave pubblica, AES in modalità CBC con chiavi a 128 bit per la crittografia della sessione e SHA-1 per gli hash di autenticazione dei messaggi.

Essendo conforme a TLS 1,2, NetX Secure Abilita il ciphersuite obbligatorio TLS_RSA_WITH_AES_128_CBC_SHA per impostazione predefinita, ma dato il numero di possibili implementazioni per ciascuno dei metodi crittografici a causa di funzionalità hardware e altre considerazioni, NetX Secure fornisce un'API di crittografia generica che consente a un utente di specificare i metodi crittografici da usare con TLS.

Nota: il meccanismo di API crittografico generico consente anche agli utenti di implementare il proprio ciphersuites, ma questa operazione è consigliata per gli utenti avanzati che hanno familiarità con le estensioni e ciphersuites di TLS. Se si è interessati a supportare il proprio ciphersuites, contattare il rappresentante della logica Express.

### <a name="cryptographic-methods"></a>Metodi crittografici

NetX Secure TLS implementa DES, 3DES, AES, MD5, HMAC-MD5, SHA-1, HMAC-SHA1, SHA-256, HMAC-SHA256, RSA e ECC (curve selezionate) nel software con driver hardware per alcune piattaforme hardware. Un'applicazione può usare le routine di crittografia fornite con NetX Secure o usare routine personalizzate fornite dall'utente finale o da terze parti.

Il *NX_CRYPTO_METHOD* è un blocco di controllo progettato in modo che un'applicazione descriva una particolare implementazione di un algoritmo di crittografia da usare con NETX Secure TLS. Con il *NX_CRYPTO_METHOD,* un'applicazione può integrare facilmente la propria implementazione della crittografia in NETX Secure. La struttura *NX_CRYPTO_METHOD* viene dichiarata come:

```C
typedef struct NX_CRYPTO_METHOD_STRUCT
{
    /* Symbolic name of the algorithm. */
    USHORT nx_crypto_algorithm;

    /* Size of the key, in bits. */
    USHORT nx_crypto_key_size_in_bits;

    /* Size of the IV block, in bits, used for encryption. */
    USHORT nx_crypto_IV_size_in_bits;

    /* Size of the ICV block, in bits, used for authentication. */
    USHORT nx_crypto_ICV_size_in_bits;

    /* Size of the crypto block, in bytes. */
    ULONG nx_crypto_block_size_in_bytes;

    /* Size of the metadata area. */
    ULONG nx_crypto_metadata_size;

    /* nx_crypto_init function initializes the crypto method with the
        "secret key" or other state  information. The initialization 
        routine should return a handle to the caller.  This handle is 
        used in subsequent crypto operations to identify the session.  
        */

    UINT (*nx_crypto_init) (NX_CRYPTO_METHOD     *method,
                            UCHAR               *key, 
                            NX_CRYPTO_KEY_SIZE   key_size_in_bits,
                            VOID               **handler,
                            VOID                *crypto_metadata,
                            VOID                 crypto_metadata_size);

    /* NetX Secure calls the nx_crypto_cleanup routine when a TLS
       session is to be deleted (or updated).  Resources allocated 
       during the crypto operation should be released in this routine.  
       */
    UINT (*nx_crypto_cleanup) (VOID *handler);

    /* nx_crypto_operation is the actual crypto or hash operation. Note 
       that both input and output buffers are prepared by the caller. 
       For encryption or decryption operations, the crypto operation 
       routine uses the output buffer for encrypted or decrypted data. 
       For authentication operations, the authentication routine shall 
       use the output buffer for the digest. */
    UINT (*nx_crypto_operation)(UINT  op, 
                  VOID              *handler, 
                  NX_CRYPTO_METHOD  *method,
                  UCHAR             *key,
                  NX_CRYPTO_KEY_SIZE key_size_in_bits,
                  UCHAR             *input,
                  ULONG              input_length_in_byte,
                  UCHAR             *iv_ptr,
                  UCHAR             *output,
                  ULONG              output_length_in_byte,
                  VOID              *crypto_metadata,
                  VOID               crypto_metadata_size,
                  NX_PACKET*         packet_ptr,
                  VOID (*nx_crypto_hw_process_callback(NX_PACKET 
                                                       *packet_ptr, 
                                                        UINT status);
} NX_CRYPTO_METHOD;
```

Di seguito è riportata la descrizione di ogni elemento nella struttura *NX_CRYPTO_METHOD* :

- nx_crypto_algorithm: questo campo identifica l'algoritmo descritto nel *Metodo* della variabile alcuni valori validi per NETX Secure TLS sono i seguenti (fare riferimento a nx_crypto_const. h per valori specifici):
    
  - NX_CRYPTO_NONE    
  - NX_CRYPTO_ENCRYPTION_NULL    
  - NX_CRYPTO_ENCRYPTION_AES_CBC    
  - NX_CRYPTO_AUTHENTICATION_NONE    
  - TLS_HASH_SHA_1    
  - TLS_HASH_SHA_256    
  - TLS_HASH_MD5    
  - TLS_CIPHER_RSA    
  - TLS_CIPHER_NULL

- nx_crypto_key_size_in_bits: questo campo specifica la dimensione della chiave privata usata dal metodo.

- nx_crypto_IV_size_in_bits: questo campo specifica la dimensione del vettore di inizializzazione (IV). Si noti che nella maggior parte dei casi il blocco IV viene usato solo per gli algoritmi di crittografia/decrittografia. Gli algoritmi di autenticazione e di verifica utilizzano raramente questo campo.

- nx_crypto_ICV_size_in_bits: questo campo specifica la dimensione del blocco del valore di controllo di integrità (ICV). Nota: questo blocco è per l'utilizzo IPsec e non è usato in TLS. Per ulteriori informazioni, vedere NetX Duo IPsec.

- nx_crypto_block_size_in_bytes: questo campo specifica le dimensioni in byte del blocco dell'algoritmo di crittografia per le crittografie basate su blocchi. Nella maggior parte dei casi questo viene usato dalle routine di crittografia e raramente dalle routine di autenticazione.

- nx_crypto_metadata_area_size: questo campo specifica la dimensione dell'area dei metadati richiesta da questo metodo. Ogni implementazione può richiedere una certa memoria per archiviare le informazioni sullo stato o per archiviare i dati intermedi, ad esempio il materiale di trasformazione della chiave, o per utilizzare come area scratch. La quantità di spazio richiesta da un'implementazione è specificata in questo campo. L'applicazione fornisce lo spazio di memoria durante la creazione di una sessione TLS. La funzione di crittografia è responsabile della gestione dell'area dei metadati.

- nx_crypto_init: questa è la funzione di inizializzazione per l'algoritmo crittografico. Per un'implementazione che non necessita di una routine di inizializzazione, questo campo può essere impostato su NX_NULL. Un utilizzo tipico di una funzione di inizializzazione consiste nell'inizializzare la struttura dei dati interni per l'algoritmo. NetX Secure TLS gestirà l'inizializzazione della routine di crittografia chiamando internamente questa funzione.

Il prototipo per la funzione di inizializzazione è:

```C
UINT crypto_init_function(NX_CRYPTO_METHOD *method, 
                          UCHAR *key, 
                          UINT  key_size_in_bits, 
                          VOID  **handle, 
                          VOID  *crypto_metadata_area, 
                          ULONG crypto_metadata_area_size);
```

  - il metodo è un puntatore al blocco di controllo del metodo Crypto.

  - Key è la stringa di chiave privata per l'elaborazione dei pacchetti di dati.

  - key_size_in_bits definisce la dimensione in bit della chiave privata.

  - handle è un elemento definito dall'implementazione che identifica una determinata sessione di crittografia. Il valore viene generato dalla routine di inizializzazione e viene passato di nuovo al chiamante. L'operazione di crittografia successiva o la routine di pulizia usano questo handle per identificare la sessione.

  - crypto_metadata è un puntatore all'area dei metadati richiesta dall'implementazione di questo algoritmo. Per gli algoritmi che non necessitano di un'area dei metadati questo campo è impostato su NX_NULL e la routine di inizializzazione non deve accedere all'area dei metadati.

  - crypto_metadata_size specifica la dimensione dell'area dei metadati. Per SAs creato senza area dei metadati, questo campo è impostato su zero e la routine di inizializzazione non deve accedere all'area dei metadati.

  - Questa routine deve restituire *NX_SUCCESS* se il processo di inizializzazione ha esito positivo. Il chiamante considera un errore qualsiasi altro valore restituito.

- nx_crypto_cleanup: questa è la routine di pulizia definita per l'implementazione di un algoritmo di crittografia. Viene richiamato quando una sessione TLS viene eliminata o riavviata.

Il prototipo per la funzione Cleanup è:

```C
UINT crypto_cleanup_function(VOID *handle);
```
- l'handle viene passato alla funzione CleanUp dal chiamante. L'handle viene inizializzato dalla routine di inizializzazione della crittografia e utilizzato per identificare lo stato dell'algoritmo crittografico.

- Questa routine deve restituire *NX_SUCCESS* se il processo di pulizia ha esito positivo. Il chiamante considera un errore qualsiasi altro valore restituito.

- nx_crypto_operation: questa è la routine che esegue i servizi di crittografia, decrittografia e autenticazione effettivi. Il prototipo di funzione della routine dell'operazione è:

```C
UINT crypto_operation_function(UINT   op,
          VOID  *handle,  
          NX_CRYPTO_METHOD* method,
          UCHAR *key,
          UCHAR  key_size_in_bits,
          UCHAR* input,
          ULONG  input_length_in_byte,
          UCHAR* iv_ptr,
          UCHAR* output,
          ULONG  output_length_in_byte,
          VOID *crypto_metadata,
          ULONG crypto_metadata_size,
          NX_PACKET *packet_ptr,
          VOID (*nx_crypto_hw_process_callback)(NX_PACKET 
                          *packet_ptr, UINT status));
```

- op indica il tipo di operazione che questa routine prevede di eseguire. I valori validi sono:
    
    - NX_CRYPTO_ENCRYPT
    - NX_CRYPTO_DECRYPT
    - NX_CRYPTO_AUTHENTICATE
    - NX_CRYPTO_VERIFY

- l'handle viene passato alla funzione Operation dal chiamante. Viene generato dalla routine di inizializzazione della crittografia.
- il metodo punta al blocco di controllo del metodo Crypto
- chiave che punta alla chiave privata usata per questa operazione
- key_size_in_bits è la dimensione della chiave privata in bit
- input è un puntatore all'inizio del messaggio da operare.
- input_length_in_byte viene passato dal chiamante per indicare le dimensioni del messaggio da operare.
- iv_ptr viene configurato dal chiamante in modo che punti all'inizio di un blocco IV. Si noti che la memoria per il blocco IV viene fornita dal chiamante. Per la crittografia, la funzione Operation deve scrivere le informazioni IV in questo blocco di memoria; per la decrittografia, la funzione Operation deve recuperare le informazioni IV da questo blocco di memoria. Gli algoritmi per l'autenticazione e l'operazione di verifica in genere non usano il vettore di inizializzazione.
- l'output viene configurato dal chiamante per puntare a un buffer di output. Si noti che la memoria per il buffer di output viene fornita dal chiamante. Per la crittografia, la funzione Operation deve scrivere il testo crittografato nel buffer di output. per la decrittografia, l'operazione deve scrivere il testo decifrato (testo non crittografato) nel buffer di output. per l'autenticazione, il valore hash deve essere scritto nel buffer di output. Per la verifica, il buffer di output viene usato per archiviare le informazioni hash.
- output_length_in_byte indica le dimensioni del buffer di output
- crypto_metadata punta all'area dei metadati che deve essere utilizzata da questa operazione di crittografia. L'area dei metadati di crittografia viene in genere inizializzata da crypto_init_function.
- crypto_metadata_size indica le dimensioni dell'area dei metadati.
- Questa routine deve restituire *NX_SUCCESS* se il processo dell'operazione ha esito positivo. Il chiamante considera un errore qualsiasi altro valore restituito.
- packet_ptr: pacchetto che contiene i dati in fase di elaborazione. Nota: questo parametro non è usato da TLS e deve essere impostato su NX_NULL.
- nx_crypto_hw_process_callback: funzione di callback fornita dal metodo di crittografia. Viene usato se la funzione Crypto viene fornita dall'hardware e richiede una routine di callback.

NetX Secure TLS fornisce i metodi di crittografia seguenti:

- *AES*  
- *RSA*  
- *NULL*

NetX Secure TLS fornisce i metodi di autenticazione seguenti:

- *HMAC-MD5*  
- *HMAC-SHA1*  
- *HMAC-SHA256*

Negli esempi seguenti viene illustrato come configurare la struttura di *NX_CRYPTO_METHOD* per l'utilizzo dei metodi di crittografia e autenticazione forniti da NETX Duo IPSec.

***AES***

```C
/* AES-CBC 128. */
NX_CRYPTO_METHOD crypto_method_aes_cbc_128 = 
{
    /* AES crypto algorithm                             */
    NX_CRYPTO_ENCRYPTION_AES_CBC,                       

    /* Key size in bits. For AES-128 this value is 128  */
    NX_CRYPTO_AES_128_KEY_LEN_IN_BITS,              
   
    /* IV size in bits.  For AES-128 this value is 128  */
    NX_CRYPTO_AES_IV_LEN_IN_BITS,

    /* ICV size in bits, not used.                      */
    0,                                              

    /* Block size in bytes.  For AES this value is 16   */
    (NX_CRYPTO_AES_BLOCK_SIZE_IN_BITS >> 3),        

    /* Metadata size in bytes, for AES this value is 262*/
    sizeof(NX_CRYPTO_AES),              

    /* AES-CBC initialization routine.                  */
    _nx_secure_crypto_method_aes_init,               

    /* AES-CBC cleanup routine, not used.               */
    NX_NULL,                                        

    /* AES-CBC operation                                */
    _nx_secure_crypto_method_aes_operation           
};

/* RSA. */
NX_CRYPTO_METHOD crypto_method_rsa = 
{
    /* RSA crypto algorithm                             */
    TLS_CIPHER_RSA,                       

    /* Key size. RSA key sizes vary, so set to 0.         */
    0,              
   
    /* IV size in bits.  RSA does not use an IV.         */
    0,

    /* ICV size in bits, not used.                      */
    0,                                              

    /* Block size in bytes.  RSA does not have a block size. */
    0,        

    /* Metadata size in bytes, for RSA use the control block. */
    sizeof(NX_CRYPTO_RSA),              

    /* RSA initialization routine.                  */
    _nx_secure_crypto_method_rsa_init,               

    /* Cleanup routine, not used.                    */
    NX_NULL,                                        

    /* RSA operation                                */
    _nx_secure_crypto_method_rsa_operation           

};
```
***NULL***

```C
/* NULL encryption method. */
NX_CRYPTO_METHOD crypto_method_null = 
{
    NX_CRYPTO_ENCRYPTION_NULL,/* Name of the crypto algorithm  */
    0,                        /* Key size in bits, not used    */
    0,                        /* IV size in bits, not used     */
    0,                        /* ICV size in bits, not used    */
    4,                        /* Block size in bytes           */
    0,                        /* Metadata size in bytes        */
    NX_NULL,                  /* Initialization routine,unused */
    NX_NULL,                  /* Cleanup routine, not used     */
    _nx_secure_crypto_method_null_operation  /* NULL operation  
*/
}; 
```
***HMAC-SHA1***
```C
NX_CRYPTO_METHOD crypto_method_hmac_sha1 = 
{
    /* HMAC SHA1 algorithm                               */
    TLS_HASH_SHA1,            


    /* Key size in bits. For HMAC-SHA1 this value is 160 */ 
    NX_CRYPTO_HMAC_SHA1_KEY_LEN_IN_BITS,              

    /* IV size in bits, not used                         */
    0,                                            

    /* Transmitted ICV size in bits. Unused.             */
    0, 

    /* Block size in bytes, not used                     */
    0,                                            

    /* Metadata size in bytes                            */
    sizeof(NX_SHA1_HMAC),                                            

    /* Initialization routine, not used                  */
    NX_NULL,                                      

    /* Cleanup routine, not used                         */
    NX_NULL,                                          

    /* HMAC SHA1 operation                               */
    _nx_secure_crypto_method_hmac_sha1_operation   
};
```
***NONE***

Un metodo speciale **NX_CRYPTO_NONE** viene utilizzato per segnalare al modulo IPsec che la crittografia o il servizio di autenticazione non è necessario. Viene configurato come segue:

```C
/* NX_CRYPTO_NONE means encryption or authentication
   method is not needed.  */
NX_CRYPTO_METHOD crypto_method_none = 
{
    NX_CRYPTO_NONE,       /* Name of the crypto algorithm */
    0,                    /* Key size in bits, not used   */
    0,                    /* IV size in bits, not used    */
    0,                    /* ICV size in bits, not used   */
    0,                    /* Block size in bytes          */
    0,                    /* Metadata size in bytes       */
    NX_NULL,              /* Initialization routine, not used */
    NX_NULL,              /* Cleanup routine, not used    */
    NX_NULL               /* NULL operation               */
};                                               
```
### <a name="initializing-tls-with-cryptographic-methods"></a>Inizializzazione di TLS con i metodi di crittografia

Dopo aver creato le routine di crittografia conformi alle firme del metodo crittografico descritte nella sezione precedente, sarà necessario passarle in TLS quando si Inizializza un blocco di controllo NX_SECURE_TLS_SESSION. Questa operazione viene eseguita nel nx_secure_tls_session_create del servizio TLS:

```C
UINT  nx_secure_tls_session_create(
              NX_SECURE_TLS_SESSION*     session_ptr,
              const NX_SECURE_TLS_CRYPTO*    tls_cipher_table,
              VOID*                encryption_metadata_area,
              ULONG                 encryption_metadata_size
);
```
- session_pointer è un puntatore al blocco di controllo NX_SECURE_TLS_SESSION.
- tls_cipher_table è un puntatore a un blocco di controllo NX_SECURE_TLS_CRYPTO, descritto di seguito.
- encryption_metadata_area punta allo spazio usato dalle routine di crittografia in TLS.
- encryption_metadata_size è la dimensione in byte dell'area dei metadati.

### <a name="elliptic-curve-cryptography-ecc-in-netx-secure-tls"></a>Crittografia a curva ellittica (ECC) in NetX Secure TLS

La crittografia a curva ellittica (ECC) fornisce uno schema di crittografia a chiave pubblica che può essere utilizzato al posto di RSA. ECC è in genere più veloce e USA chiavi più piccole rispetto a RSA, quindi può essere un'opzione utile per il protocollo TLS incorporato. Nelle versioni X-Ware precedenti ad Azure RTO 6,0, ECC è stato fornito come componente aggiuntivo, richiedendo l'installazione del codice sorgente ECC nel progetto. Azure RTO 6,0 integrato ECC nella codebase principale, quindi l'installazione dei file ECC non è più necessaria. Tuttavia, ECC richiede comunque la stessa inizializzazione delle versioni precedenti.

### <a name="supported-ecc-curves"></a>Curve ECC supportate

NetX Secure implementa parti delle curve in base a <http://www.secg.org/sec2-v2.pdf> . Le curve usufruire delle sono supportate<sup>18</sup>:

  - secp256r1 
  - secp384r1 
  - secp521r1 

Se vengono utilizzate altre curve ECC, la routine *nx_secure_tls_session_start ()* restituirà l'errore NX_SECURE_TLS_NO_SUPPORTED_CIPHERS a indicare che sono state utilizzate curve non supportate.

Si noti che la catena di certificati TLS può essere crittografata anche con gli algoritmi ECC. Anche se le curve fornite dal client TLS sono supportate, è possibile che la curva ECC usata nella catena di certificati non sia supportata. In questo caso, *nx_secure_tls_session_start* routine restituisce NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER.

Un esempio di tabella ciphersuite predefinito per ECC viene fornito in nx_crypto_generic_ciphersuites. c. Per ulteriori informazioni sulle tabelle ciphersuite, vedere la sezione relativa alla tabella di crittografia TLS.

18. Si noti che le implementazioni per le curve secp192r1 e secp224r1are sono fornite anche per le applicazioni legacy. Tuttavia, queste curve sono ora considerate vulnerabili e non devono essere usate per lo sviluppo di nuove applicazioni.

### <a name="crypto-methods-for-ecc"></a>Metodi di crittografia per ECC

Metodi di crittografia per gruppi a curva ellittica:

- NX_CRYPTO_METHOD crypto_method_ec_secp192<sup>15</sup>;  
- NX_CRYPTO_METHOD crypto_method_ec_secp224<sup>15</sup>;  
- NX_CRYPTO_METHOD crypto_method_ec_secp256;  
- NX_CRYPTO_METHOD crypto_method_ec_secp384;  
- NX_CRYPTO_METHOD crypto_method_ec_secp521;

I metodi di crittografia per le curve ECC sono definiti in nx_crypto_generic_ciphersuites. c.

Metodo Crypto per ECDHE:

- NX_CRYPTO_METHOD crypto_method_ecdhe;

Metodo Crypto per ECDSA:

- NX_CRYPTO_METHOD crypto_method_ecdsa;

I metodi di crittografia ECDSA e ECDHE sono definiti in nx_crypto_generic_ciphersuites. c.

Insieme ad altri metodi di crittografia, ad esempio RSA, SHA e AES, possono essere usati come blocchi predefiniti per la tabella di ricerca ciphersuite.

### <a name="enabling-ecc-support-for-tls"></a>Abilitazione del supporto ECC per TLS

ECC è abilitato per impostazione predefinita per TLS. Per disabilitare il supporto ECC, è necessario definire il simbolo NX_SECURE_DISABLE_ECC_CIPHERSUITE.

Per rendere effettive le modifiche, sarà necessario ricompilare la libreria protetta NetX e tutte le applicazioni che usano tale libreria.

Nel codice dell'applicazione, l'API n *x_secure_tls_ecc_initialize ()* deve essere chiamata dopo la creazione della sessione TLS. Questa API invia una notifica alla sessione TLS del tipo di curve da usare per le operazioni di scambio delle chiavi TLS e la verifica del certificato. Durante la fase di handshake TLS, se viene selezionato un algoritmo ECC, i parametri correlati alla curva ECC del client e del server per decidere quale curva usare.

Il segmento di codice seguente illustra come usare l'API. Si noti che gli argomenti (*nx_crypto_ecc_supported_groups, nx_crypto_ecc_supported_groups_size e nx_crypto_ecc_curves)* sono tutti definiti in *nx_crypto_generic_ciphersuites. c*. Questi simboli possono pertanto essere usati direttamente.

```C
status = nx_secure_tls_ecc_initialize(&tls_session,     
                    nx_crypto_ecc_supported_groups,      
                    nx_crypto_ecc_supported_groups_size,     
                    nx_crypto_ecc_curves);
```
La configurazione di esempio in nx_crypto_generic_ciphersuites. c contiene una tabella di ricerca ECC ciphersuite usata quando ECC è abilitato. Per usare ECC, è sufficiente passare nx_crypto_tls_ciphers_ecc come parametro della tabella ciphersuite durante la creazione di sessioni TLS con nx_secure_tls_session_create. La tabella di esempio contiene ciphersuites ECC e non ECC.

### <a name="tls-cryptographic-cipher-table"></a>Tabella di crittografia TLS

La struttura NX_SECURE_TLS_CRYPTO è definita come segue:

```C
typedef struct NX_SECURE_METHODS_STRUCT
{
    /* Table that maps ciphersuites to crypto methods. */
    NX_SECURE_TLS_CIPHERSUITE_INFO* nx_secure_tls_ciphersuite_lookup_table;
    USHORT nx_secure_tls_ciphersuite_lookup_table_size;

    /* Table that maps X.509 cipher identifiers to crypto methods. */
    NX_SECURE_X509_CRYPTO *nx_secure_tls_x509_cipher_table;
    USHORT nx_secure_tls_x509_cipher_table_size;

    /* Specific routines needed for specific TLS versions. */
#if (NX_SECURE_TLS_TLS_1_0_ENABLED || NX_SECURE_TLS_TLS_1_1_ENABLED)
    NX_CRYPTO_METHOD *nx_secure_tls_handshake_hash_md5_method;
    NX_CRYPTO_METHOD *nx_secure_tls_handshake_hash_sha1_method;
    NX_CRYPTO_METHOD *nx_secure_tls_prf_1_method;
#endif

#if (NX_SECURE_TLS_TLS_1_2_ENABLED)
    NX_CRYPTO_METHOD *nx_secure_tls_handshake_hash_sha256_method;
    NX_CRYPTO_METHOD *nx_secure_tls_prf_sha256_method;
#endif

#if (NX_SECURE_TLS_TLS_1_3_ENABLED)
    const NX_CRYPTO_METHOD *nx_secure_tls_hkdf_method;
    const NX_CRYPTO_METHOD *nx_secure_tls_hmac_method;
    const NX_CRYPTO_METHOD *nx_secure_tls_ecdhe_method;
#endif

} NX_SECURE_TLS_CRYPTO;
```
La tabella viene creata compilando le voci per questa struttura in una costante statica che si trova all'interno del progetto TLS sicuro NetX, che in genere si trova con le routine e i moduli crittografici.

Ad esempio, la libreria di crittografia solo software ("generico") fornita con NetX Secure contiene la definizione di tabella seguente (per il supporto di ciphersuite non ECC<sup>19</sup>):

```C
/* Define the cipher table object we can pass into TLS. */
const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers =
{
    /* TLS Ciphersuite lookup table and size. */
    _nx_crypto_ciphersuite_lookup_table,
    sizeof(_nx_crypto_ciphersuite_lookup_table) / 
    sizeof(NX_SECURE_TLS_CIPHERSUITE_INFO),

    /* X.509 certificate cipher table and size. */
    _nx_crypto_x509_cipher_lookup_table,
    sizeof(_nx_crypto_x509_cipher_lookup_table) / sizeof(NX_SECURE_X509_CRYPTO),

    /* TLS version-specific methods. */
#if (NX_SECURE_TLS_TLS_1_0_ENABLED || NX_SECURE_TLS_TLS_1_1_ENABLED)
    &crypto_method_md5,
    &crypto_method_sha1,
    &crypto_method_tls_prf_1,
#endif

#if (NX_SECURE_TLS_TLS_1_2_ENABLED)
    &crypto_method_sha256,
    &crypto_method_tls_prf_sha_256
#endif

#if (NX_SECURE_TLS_TLS_1_3_ENABLED)
    &crypto_method_hkdf,
    &crypto_method_hmac,
    &crypto_method_ecdhe,
#endif
};
```
Nella struttura la prima voce è la tabella TLS ciphersuite. La struttura NX_SECURE_TLS_CIPHERSUITE_INFO esegue il mapping delle routine di crittografia (sotto forma di puntatori NX_CRYPTO_METHOD) a ciphersuites specifici come definito nelle specifiche TLS. Il secondo valore è il numero di voci nella tabella a cui punta il primo campo.

Il campo successivo punta a una tabella di routine utilizzata da X. 509 quando si elaborano i certificati digitali e la struttura NX_SECURE_X509_CRYPTO è simile al formato NX_SECURE_TLS_CIPHERSUITE_INFO. Il campo seguente indica il numero di voci nella tabella.

Le tabelle di ricerca seguenti sono diverse routine necessarie per versioni specifiche di TLS. Ad esempio, prima della versione di TLS 1,2, le routine di generazione delle chiavi e di hash di handshake sono state corrette per l'uso di una combinazione di SHA-1 e MD5. i metodi per queste routine sono denominati in modo specifico nella struttura di crittografia poiché non sono collegati a ciphersuites specifici. In TLS versione 1,2, le routine di generazione e hashing delle chiavi vengono scelte da ciphersuite, ma per ciphersuites che non specificano le routine da usare, viene usato il metodo hash SHA-256 e la struttura di crittografia chiama tale routine in modo specifico.

TLS 1,3 richiede alcune crittografie specifiche aggiuntive per le varie operazioni.

19. Si noti che il supporto di TLS 1,3 richiede ECC: usare nx_crypto_tls_ciphers_ecc se TLS 1,3 è abilitato.

### <a name="tls-ciphersuite-lookup-table"></a>Tabella di ricerca TLS CipherSuite

Per compilare la tabella di crittografia per TLS, sarà anche necessario creare una tabella di ricerca ciphersuite che esegue il mapping delle routine di crittografia a identificatori ciphersuite specifici. Gli identificatori sono valori registrati da IANA universali. Per ulteriori informazioni, vedere le RFC di TLS. Le routine rappresentano i 5 metodi distinti usati in ogni ciphersuite (alcuni ciphersuites potrebbero non usare tutti i 5): crittografia pubblica, autenticazione a chiave pubblica, crittografia della sessione, routine hash della sessione e funzione di Pseudo-Random TLS (PRF). Nella tabella seguente vengono illustrati i 5 metodi seguenti:

| **Categoria routine**      | **Descrizione**                                                                                       | **Algoritmi di esempio**                                            |
| ------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Crittografia pubblica             | Usato per scambiare chiavi durante l'handshake TLS                                                        | RSA, Diffie-Hellman, ECC                                          |
| Autenticazione a chiave pubblica | Usato per autenticare o firmare i dati durante l'handshake TLS                                            | RSA, DSS                                                          |
| Crittografia della sessione            | Algoritmo a chiave simmetrica usato per crittografare i dati dell'applicazione durante la sessione TLS                       | AES, RC4                                                          |
| Hash della sessione              | Utilizzato per mantenere l'integrità dei messaggi durante la sessione TLS (garantisce che i dati non siano stati modificati) | SHA-1, SHA-256                                                    |
| PRF TLS                   | Utilizzato per generare il materiale della chiave e nell'hash di handshake nell'handshake TLS                          | PRF si basa su routine hash – SHA-1 + MD5, SHA-256, SHA-512 |

La struttura NX_SECURE_TLS_CIPHERSUITE_INFO viene definita nel modo seguente:

```C
typedef struct NX_SECURE_TLS_CIPHERSUITE_INFO_struct
{
    /* The IANA value of the ciphersuite as defined by the TLS spec.*/
    USHORT nx_secure_tls_ciphersuite;

    /* The Public Key operation in this suite - RSA or DH. */
    NX_CRYPTO_METHOD *nx_secure_tls_public_cipher;

    /* The Public Authentication method used for signing data. */
    NX_CRYPTO_METHOD *nx_secure_tls_public_auth;

    /* The session cipher being used - AES, RC4, etc. */
    NX_CRYPTO_METHOD *nx_secure_tls_session_cipher;

    /* The size of the initialization vectors for the session cipher (bytes).*/
    USHORT nx_secure_tls_iv_size;

    /* The key size for the session cipher (bytes). */
    UCHAR nx_secure_tls_session_key_size;

    /* The hash being used - MD5, SHA-1, SHA-256, etc. */
    NX_CRYPTO_METHOD *nx_secure_tls_hash;

    /* The size of the hash being used. SHA-1 is 20 bytes, MD5 is 16 bytes.*/
    USHORT nx_secure_tls_hash_size;

    /* The TLS PRF being used – this is only for TLSv1.2. */
    NX_CRYPTO_METHOD *nx_secure_tls_prf;

} NX_SECURE_TLS_CIPHERSUITE_INFO;
```
Il campo nx_secure_tls_ciphersuite contiene il valore IANA ciphersuite e i puntatori NX_CRYPTO_METHOD rappresentano i 5 metodi usati da tale ciphersuite. I valori scalari (nx_secure_tls_iv_size, nx_secure_tls_key_size e nx_secure_tls_hash_size) sono informativi e forniscono informazioni che potrebbero non essere disponibili nelle voci NX_CRYPTO_METHOD.

Si esaminerà ad esempio il valore predefinito di ciphersuite per TLS, TLS_RSA_WITH_AES_128_CBC_SHA, che specifica l'uso di RSA, AES-CBC con chiavi a 128 bit e SHA-1 per l'hashing della sessione. Per questo ciphersuite non è specificata alcuna PRF TLS, quindi in modalità TLSv 1.2 verrà usata la PRF predefinita SHA-256. Si noti che tutti i ciphersuites utilizzano la PRF SHA-1 + MD5 in TLS 1,0 e 1,1, indipendentemente dalla PRF specificata nella tabella.

La voce nella tabella NX_SECURE_TLS_CIPHERSUITE_INFO nella libreria di crittografia generica è definita nel modo seguente:

```C
{ 
  TLS_RSA_WITH_AES_128_CBC_SHA,     /* Ciphersuite identifier */
  &crypto_method_rsa,               /* Public-key cipher (NX_CRYPTO_METHOD)*/
  &crypto_method_rsa,               /* Authentication method(NX_CRYPTO_METHOD)*/
  &crypto_method_aes_cbc_128,       /* Session cipher method(NX_CRYPTO_METHOD)*/
  16,                               /* Session cipher IV size in bytes */
  16,                               /* Session cipher key size in bytes */
  &crypto_method_hmac_sha1,         /* Session hash routine(NX_CRYPTO_METHOD) */
  20,                               /* Session hash output size in bytes */
  &crypto_method_tls_prf_sha_256    /* TLSv1.2 PRF */
},
```

Si noti che per la crittografia della sessione la dimensione della chiave è determinata da ciphersuite, ma per i metodi a chiave pubblica la dimensione della chiave non è nota fino a quando l'handshake TLS non è in corso poiché le chiavi pubbliche sono contenute nei certificati digitali scambiati durante l'handshake.

### <a name="x509-cipher-lookup-table"></a>Tabella di ricerca crittografica X. 509

Analogamente alla tabella NX_SECURE_TLS_CIPHERSUITE_INFO, la struttura NX_SECURE_X509_CRYPTO esegue il mapping delle routine di crittografia ai valori noti. Nel caso di X. 509, gli identificatori sono effettivamente OID definiti da X. 509 e registrati con i corpi degli standard ISO e ITU. OID sono valori multibyte a lunghezza variabile progettati per identificare in modo univoco le varie informazioni in diversi standard di telecomunicazione, incluse le routine crittografiche usate nei certificati digitali. A causa del fatto che OID sono a lunghezza variabile, NetX Secure TLS esegue il mapping dei valori OID ufficiali alle costanti a lunghezza fissa utilizzate internamente (vedere nx_secure_x509. h). Queste costanti vengono utilizzate nella struttura di NX_SECURE_X509_CRYPTO, definita nel modo seguente:

```C
/* Structure to hold X.509 cryptographic routine information. */
typedef struct NX_SECURE_X509_CRYPTO_struct
{
    /* Internal NetX Secure identifier for certificate "ciphersuite" which consists
       of a hash and a public key operation. These can be mapped to OIDs in X.509.
        */
    USHORT nx_secure_x509_crypto_identifier;

    /* Public-Key Cryptographic method used by certificates. */
    NX_CRYPTO_METHOD *nx_secure_x509_public_cipher_method;

    /* Hash method used by certificates. */
    NX_CRYPTO_METHOD *nx_secure_x509_hash_method;
} NX_SECURE_X509_CRYPTO;
```

Il primo campo, *nx_secure_x509_crypto_identifier*, è la rappresentazione OID interna utilizzata da NETX Secure.

Il secondo e il terzo campo puntano a NX_CRYPTO_METHOD oggetti che rappresentano i metodi crittografici identificati dall'OID, un'operazione a chiave pubblica abbinata a una routine hash. Si noti che ogni certificato digitale può avere più di un OID per le routine crittografiche.

La tabella dei metodi per X. 509 viene costruita in modo analogo alla tabella di ricerca ciphersuite. Si esaminerà ad esempio l'OID per RSA_SHA1. L'OID effettivo per RSA_SHA1 è il seguente:

```C
{iso(1) member-body(2) us(840) rsadsi(113549) pkcs(1) pkcs-1(1) sha1-with-rsa-
signature(5)}
```
L'OID è rappresentato nella sintassi ASN. 1 e ha un valore numerico pari a 1.2.840.113549.1.1.5. Questo valore viene quindi codificato in formato binario, creando i byte seguenti:

```C
UCHAR RSA_SHA1_OID = { 0x2A, 0x86, 0x48, 0x86, 0xF7, 0x0D, 0x01, 0x01, 0x05 };
```
La conversione effettiva da ASN. 1 al formato binario esula dall'ambito di questo documento. Per ulteriori informazioni, cercare le codifiche ASN. 1 per OID. La rappresentazione binaria di OID supportata da NetX Secure si trova nel file *nx_secure_x509. c*.

Una volta ottenuto un mapping dell'OID effettivo a una costante riconosciuta internamente, è possibile creare una voce per RSA_SHA1 nella tabella NX_SECURE_X509_CRYPTO:

```C
{ 
    NX_SECURE_TLS_X509_TYPE_RSA_SHA_1,    /* Internal OID constant. */
    &crypto_method_rsa,                   /* RSA method (NX_CRYPTO_METHOD). */ 
    &crypto_method_sha1                   /* SHA-1 method (NX_CRYPTO_METHOD). */
}, 
```
### <a name="default-tls-routines"></a>Routine TLS predefinite

Come indicato in precedenza, TLS richiede alcune routine predefinite per la generazione delle chiavi e la verifica dei messaggi durante l'handshake. La routine primaria è la funzione TLS Pseudo-Random o PRF. PRF è basato su routine hash e può essere usato per generare una quantità arbitraria di dati pseudo-casuali<sup>20</sup> per la generazione di chiavi o altri scopi.

Oltre a PRF, ogni versione di TLS usa le routine hash predefinite che devono essere fornite anche. Per le versioni TLS 1,0 e 1,1, le routine hash sono MD5 e SHA-1. Per la versione 1,2 di TLS è necessario solo SHA-256.

Nella struttura di NX_SECURE_TLS_CRYPTO sono presenti puntatori NX_CRYPTO_METHOD per MD5, SHA-1, SHA-256, TLS versione 1.0/1.1 PRF e il valore predefinito di TLS 1,2 PRF.

Il supporto di TLS 1,3 aggiunge campi per HKDF (generazione di chiavi), HMAC (per operazioni di hashing specifiche usate durante l'handshake) e ECDHE (obbligatorio per la funzionalità TLS 1,3).

In Generic software Cryptography Library sono disponibili versioni software di TLS PRF. Per TLS 1.0/1.1 questa funzione viene chiamata *nx_crypto_tls_prf_1*. Per TLS 1,2, la funzione viene chiamata *nx_secure_tls_prf_sha256*. Il suffisso "1" rappresenta la PRF TLS 1,0 legacy e il suffisso "SHA256" si riferisce al fatto che la PRF predefinita TLS 1,2 è basata su SHA-256. Quando è necessario il supporto per altre routine PRF, il suffisso per tali routine rifletterà il metodo hash utilizzato. Poiché le routine PRF sono basate su metodi hash, le routine hash sottostanti possono essere accelerate in modo indipendente su diverse piattaforme di destinazione.

Oltre alle tabelle di ricerca TLS ciphersuite e X. 509, con le routine PRF e hash predefinite compilate nella struttura NX_SECURE_TLS_CRYPTO possono essere popolate e usate per inizializzare una sessione TLS.

20. "Pseudo-casuale" si riferisce al fatto che la PRF è deterministica, vale a dire che produrrà sempre lo stesso output in base allo stesso input, ma casuale nel fatto che l'output non è stimabile. TLS usa questa proprietà di PRF per generare le chiavi della sessione da diversi dati pubblici combinati con la master secret scambiata durante l'handshake usando una crittografia a chiave pubblica, ad esempio RSA.

### <a name="cryptographic-metadata"></a>Metadati crittografici

Prima di poter inizializzare la sessione TLS con la tabella NX_SECURE_TLS_CRYPTO, è necessario allocare spazio nel buffer per i metadati della routine di crittografia. I metadati vengono usati per archiviare tutti gli Stati associati a una routine specifica, rappresentati dal relativo blocco di controllo. Il campo *nx_crypto_metadata_area_size* di ogni NX_CRYPTO_METHOD deve essere impostato sulla dimensione della struttura di controllo associata a tale routine o l'inizializzazione TLS non riuscirà a tenere conto dello spazio necessario, causando probabilmente problemi di sovraccarico del buffer.

Prima della creazione della sessione TLS, è necessario allocare il buffer dei metadati. Il buffer viene diviso automaticamente per nx_secure_tls_session_create e lo spazio viene riservato per ogni routine fornita nella tabella del metodo crittografico. Si noti che poiché un solo ciphersuite è attivo alla volta in una sessione TLS, il numero di ciphersuites supportati non influisce sull'area dei metadati necessaria. lo spazio viene riservato per ognuna delle 5 routine ciphersuite usando la dimensione massima del blocco di controllo per tale categoria nella tabella di ricerca ciphersuite.

Per semplificare il calcolo delle dimensioni del buffer dei metadati, il *nx_secure_metadata_size_calculate* del servizio esegue gli stessi calcoli nx_secure_tls_session_create ma restituisce semplicemente la dimensione totale necessaria del buffer dei metadati in byte.

### <a name="initializing-the-tls-session"></a>Inizializzazione della sessione TLS

Una volta creati gli oggetti NX_CRYPTO_METHOD e NX_SECURE_TLS_CRYPTO e l'area dei metadati riservata, è possibile inizializzare una sessione TLS come indicato di seguito (i valori ricavati dagli esempi precedenti):

```C
/* Pointer to the platform-specific cipher table. */
extern nx_crypto_tls_ciphers;

/* Cryptographic routine metadata buffer. Size is determined by calling 
nx_secure_tls_metadata_size_calculate with the nx_crypto_tls_ciphers table referenced 
above. */
UCHAR crypto_metadata[4500];

/* Initialize our TLS session using our cipher table and metadata area. Note that we can 
use sizeof for the metadata array because the size parameter expects the size in bytes.*/

nx_secure_tls_session_create(
    &tls_session,            /* Pointer to TLS session.      */
    &nx_crypto_tls_ciphers,  /* Pointer to cipher table.     */
    crypto_metadata,         /* Cryptography metadata buffer.*/
    sizeof(crypto_metadata), /* Size of metadata buffer.     */
);
```
