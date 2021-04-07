---
title: Capitolo 3-Descrizione funzionale di Azure RTO NetX Secure DTLS
description: Questo capitolo contiene una descrizione funzionale di Azure RTO NetX Secure DTLS.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 347bd83fa8c72ced2e8678a92ec5c5f8393c136d
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550202"
---
# <a name="chapter-3-functional-description-of-azure-rtos-netx-secure-dtls"></a>Capitolo 3: Descrizione funzionale di Azure RTO NetX Secure DTLS

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Questo capitolo contiene una descrizione funzionale di Azure RTO NetX Secure DTLS. Esistono due tipi principali di esecuzione del programma in un'applicazione NetX Secure DTLS: inizializzazione e chiamate dell'interfaccia dell'applicazione. 

NetX Secure presuppone l'esistenza di ThreadX e NetX/NetXDuo. Da ThreadX, sono necessari l'esecuzione di thread, la sospensione, i timer periodici e le strutture di esclusione reciproca. Da NetX/NetXDuo richiede le funzionalità di rete UDP e IP e i driver.

## <a name="datagram-transport-layer-security-dtls-and-transport-layer-security-tls"></a>Datagramma Transport Layer Security (DTLS) e Transport Layer Security (TLS)

NetX Secure DTLS implementa il datagramma Transport Layer Security protocollo versione 1,2 definito in RFC 6347. DTLS versione 1,0 è stata definita in RFC 4347 e corrisponde a TLS versione 1,1. Poiché DTLS è essenzialmente un'estensione di TLS, è stato deciso che la versione successiva utilizzerebbe lo stesso numero di versione della versione TLS corrispondente. Quindi, non esiste alcuna versione di DTLS 1,1 perché DTLS versione 1,2 corrisponde a TLS versione 1,2.

> [!NOTE]
> NetX Secure supporta DTLS versione 1,2. DTLS 1,0 (RFC 4347) **non** è attualmente supportato.

*Secure Sockets Layer* (SSL) è il nome originale di TLS prima che diventi uno standard in RFC 2246 e "SSL" viene spesso usato come nome generico per i protocolli TLS. L'ultima versione di SSL è 3,0 e TLS 1,0 viene a volte definito SSL versione 3,1. Tutte le versioni del protocollo "SSL" ufficiale sono considerate obsolete e non sicure e attualmente NetX Secure non fornisce un'implementazione SSL.

TLS specifica un protocollo per generare *chiavi di sessione* create durante l' *handshake* TLS tra un client e un server TLS e tali chiavi vengono usate per crittografare i dati inviati dall'applicazione durante la *sessione TLS.*

DTLS è strettamente associato a TLS, perché i mechansims di sicurezza sottostanti sono condivisi tra i protocolli. Tuttavia, TLS è progettato per funzionare su un protocollo di livello trasporto che fornisce garanzie sul recapito e sull'ordine dei pacchetti (quasi sempre TCP in pratica) e non funzionerà su un protocollo non affidabile come UDP. È proprio a causa di UDP che DTLS è stato introdotto: DTLS è stato progettato per gestire la natura inaffidabile di UDP e protocolli simili. Questa operazione viene eseguita includendo la logica di ordinamento e affidabilità (ad esempio la ritrasmissione dei dati eliminati) simile a protocolli affidabili come TCP.

Una descrizione completa di TLS è inclusa nel capitolo 3 del manuale dell'utente di NetX Secure TLS, quindi questo documento si focalizzerà sulle differenze tra TLS e DTLS.

### <a name="dtls-record-header"></a>Intestazione del record DTLS

Qualsiasi record DTLS valido deve avere un'intestazione DTLS, come illustrato nella figura 1. L'intestazione è uguale a TLS con l'aggiunta di due nuovi campi: l' *Epoch* a 16 bit e il *numero di sequenza* a 48 bit, descritto di seguito.

![Diagramma di un'intestazione di record DTLS.](media/image2.png)

**Figura 1-intestazione del record DTLS**

I campi dell'intestazione del record TLS sono definiti come segue:

| Campo di intestazione TLS | Scopo  |
| ---------------- | --------- |
| **Tipo di messaggio a 8 bit** | Questo campo contiene il tipo di record DTLS da inviare. I tipi validi sono i seguenti:<br />-ChangeCipherSpec: 0x14<br />-Avviso: 0x15<br />-Handshake: 0x16<br />-Dati applicazione: 0x17<br /> |
| **Versione del protocollo a 16 bit** | Questo campo contiene la versione del protocollo DTLS. I valori validi sono i seguenti:<br />-DTLS 1,1:0xFEFD |
|  **Epoch a 16 bit** |  Questo campo contiene il DTLS "Epoch", che è un contatore incrementato ogni volta che viene modificato lo stato di crittografia, ad esempio quando si generano nuove chiavi di sessione.  |
|  **Numero di sequenza a 48 bit** |  Questo campo contiene un numero di sequenza che identifica questo record specifico. Viene usato da DTLS per gestire l'ordinamento dei record e verificare la necessità di ritrasmissione. |
|  **Lunghezza a 16 bit** |  Questo campo contiene la lunghezza dei dati incapsulati nel record DTLS.  |

### <a name="dtls-handshake-record-header"></a>Intestazione del record di handshake DTLS

Qualsiasi record di handshake DTLS valido deve avere un'intestazione di handshake DTLS, come illustrato nella figura 2.

![Diagramma di un'intestazione di record di handshake DTLS.](media/image3.png)

**Figura 2-intestazione del record di handshake DTLS**

I campi dell'intestazione del record di handshake DTLS sono definiti come segue:

| Campo di intestazione TLS | Scopo  |
| ---------------- | ------------------------------------------------ |
| **Tipo di messaggio a 8 bit** | Questo campo contiene il tipo di record DTLS da inviare. I tipi validi sono i seguenti:<br />-ChangeCipherSpec: 0x14<br />-Avviso: 0x15<br />-Handshake: 0x16<br />-Dati applicazione: 0x17 |
|  **Epoch a 16 bit** | Questo campo contiene il DTLS "Epoch", che è un contatore incrementato ogni volta che viene modificato lo stato di crittografia, ad esempio quando si generano nuove chiavi di sessione. |
|  **Numero di sequenza a 48 bit** | Questo campo contiene un numero di sequenza che identifica questo record specifico. Viene usato da DTLS per gestire l'ordinamento dei record e verificare la necessità di ritrasmissione. |
|  **Versione del protocollo a 16 bit** | Questo campo contiene la versione del protocollo DTLS. I valori validi sono i seguenti:<br />-DTLS 1,1:0xFEFD |
| **Lunghezza a 16 bit** | Questo campo contiene la lunghezza dei dati incapsulati nel record DTLS. |
| **Tipo di handshake a 8 bit** | Questo campo contiene il tipo di messaggio di handshake. I valori validi sono i seguenti:<br />-HelloRequest: 0x00<br />-ClientHello: 0x01<br />-ServerHello: 0x02<br />-Certificato: 0x0B<br />-ServerKeyExchange: 0x0C<br />-CertificateRequest: 0x0D<br />-ServerHelloDone: 0x0E<br />-CertificateVerify: 0x0F<br />-ClientKeyExchange: 0x10<br />-Operazione completata: 0x14 |
| **Lunghezza a 24 bit** | Questo campo contiene la lunghezza dei dati del messaggio di handshake. |
| **Numero di sequenza a 16 bit** | Questo campo contiene un numero di sequenza. |

### <a name="the-dtls-handshake-and-dtls-session"></a>DTLS handshake e DTLS Session

Nella figura 3 è illustrato un handshake DTLS tipico. È quasi identico al tipico handshake TLS con una differenza importante: quando il messaggio ClientHello viene inviato per la prima volta, il server risponde con un nuovo messaggio specifico di DTLS, *HelloVerifyRequest* che contiene un "cookie". Il client DTLS deve rispondere con un secondo messaggio ClientHello contenente tale cookie prima che l'handshake possa proseguire. Questo meccanismo è stato aggiunto a DTLS per impedire determinati attacchi Denial of Service (DoS) Poiché UDP è un protocollo senza connessione (TCP richiede una connessione/porta dedicata in modo che TLS non soffra dello stesso problema).

Un handshake DTLS inizia quando il client invia un messaggio *ClientHello* a un server DTLS, indicando il desiderio di avviare una sessione DTLS. Il messaggio contiene informazioni sulla crittografia che il client desidera utilizzare per la sessione, insieme alle informazioni utilizzate per generare le chiavi di sessione in un secondo momento nell'handshake. Fino a quando non vengono generate le chiavi della sessione, tutti i messaggi nell'handshake DTLS non vengono crittografati. Come indicato in precedenza, il server DTLS può inviare un HelloVerifyRequest in risposta a ClientHello, forzando il client a rispondere con un secondo ClientHello aggiornato.

Quando riceve il secondo messaggio ClientHello, il server DTLS verificherà il cookie e se la correzione risponderà con un messaggio ServerHello che indica una selezione dalle opzioni di crittografia fornite dal client. ServerHello è seguito da un messaggio di certificato, in cui il server fornisce un certificato digitale per autenticare la propria identità al client (se viene utilizzata la verifica X. 509). Infine, il server invia un messaggio ServerHelloDone per indicare che non sono presenti altri messaggi da inviare. Il server può facoltativamente inviare altri messaggi dopo ServerHello e in alcuni casi potrebbe non inviare un messaggio di certificato, ad esempio quando vengono usate chiavi precondivise, quindi la necessità del messaggio ServerHelloDone.

Una volta che il client ha ricevuto tutti i messaggi del server, dispone di informazioni sufficienti per generare le chiavi della sessione. Questa operazione viene eseguita da TLS/DTLS creando un bit condiviso di dati casuali denominato *Master Secret*, che è a dimensione fissa e viene utilizzato come valore di inizializzazione per generare tutte le chiavi necessarie quando la crittografia è abilitata. Il segreto pre-master viene crittografato usando l'algoritmo a chiave pubblica, ad esempio RSA, specificato nei messaggi Hello (vedere di seguito per informazioni sugli algoritmi a chiave pubblica) e la chiave pubblica fornita dal server nel certificato. Una funzionalità facoltativa TLS/DTLS denominata chiavi precondivise (PSK) consente a ciphersuites che non usano un certificato, ma usano invece un valore segreto condiviso tra gli host (in genere tramite trasferimento fisico o un altro metodo protetto). Quando è abilitata la funzionalità PSK, la chiave privata precondivisa viene utilizzata per generare il segreto pre-master. Vedere la sezione relativa alle chiavi già condivise in "metodi di autenticazione" di seguito.

In un handshake TLS/DTLS consueto, il segreto pre-master crittografato viene inviato al server nel messaggio ClientKeyExchange. Il server, dopo la ricezione del messaggio ClientKeyExchange, decrittografa il segreto pre-master usando la relativa chiave privata e continua a generare le chiavi della sessione in parallelo con il client TLS/DTLS.

Una volta generate le chiavi della sessione, tutti gli altri messaggi possono essere crittografati usando l'algoritmo di chiave privata, ad esempio AES, selezionato nei messaggi Hello. Un messaggio finale non crittografato denominato ChangeCipherSpec viene inviato sia dal client che dal server per indicare che tutti gli altri messaggi verranno crittografati.

Il primo messaggio crittografato inviato sia dal client che dal server è anche il messaggio di handshake TLS finale, denominato completato. Questo messaggio contiene un hash di tutti i messaggi di handshake ricevuti e inviati. Questo hash viene utilizzato per verificare che nessuno dei messaggi nell'handshake sia stato alterato o danneggiato (che indica una possibile violazione della sicurezza).

Dopo la ricezione dei messaggi finiti e la verifica degli hash di handshake, viene avviata la sessione TLS/DTLS e l'applicazione inizia a inviare e ricevere dati. Per la prima volta viene eseguito l'hashing di tutti i dati inviati da entrambi i lati durante la sessione TLS/DTLS usando l'algoritmo hash scelto nei messaggi Hello (per fornire l'integrità del messaggio) e crittografati usando l'algoritmo di chiave privata scelto con le chiavi di sessione generate.

Infine, una sessione TLS/DTLS può essere conclusa correttamente solo se il client o il server sceglie di eseguire questa operazione. Una sessione troncata è considerata una violazione della sicurezza (poiché un utente malintenzionato potrebbe tentare di impedire la ricezione di tutti i dati), quindi viene inviata una notifica speciale quando uno dei due lati desidera terminare la sessione, denominata avviso CloseNotify. Sia il client che il server devono inviare ed elaborare un avviso CloseNotify per un arresto corretto della sessione.

![Diagramma di una tipica sessione di handshake DTLS.](media/image4.png)

**Figura 3: handshake DTLS tipico**

### <a name="initialization"></a>Inizializzazione

Lo stack NetX o NetXDuo deve essere inizializzato prima di usare NetX Secure DTLS. Per informazioni su come inizializzare correttamente lo stack TCP/IP per l'operazione UDP, vedere la guida dell'utente di NetX o NetXDuo.

Dopo l'inizializzazione di NetX UDP, è possibile abilitare DTLS. Internamente tutto il traffico di rete e l'elaborazione di DTLS vengono gestiti dallo stack NetX/NetXDuo senza richiedere l'intervento dell'utente. Tuttavia, DTLS presenta alcuni requisiti specifici che devono essere gestiti separatamente dallo stack di rete sottostante. Operazione client DTLS questi parametri sono assegnati al blocco di controllo DTLS denominato ***NX_SECURE_DTLS_SESSION** _. Per l'operazione del server DTLS, il blocco di controllo viene chiamato _ *_NX_SECURE_DTLS_SERVER_** e contiene l'infrastruttura necessaria per gestire più sessioni DTLS in una singola porta UDP. si noti che questo è diverso da TLS, in cui a ogni sessione TLS è associato a una singola porta TCP.

Le due modalità DTLS, server e client, possono essere abilitate in un'applicazione (ma solo una modalità per socket NetX) e ognuna hanno requisiti specifici, descritti di seguito.

### <a name="initialization--dtls-server"></a>Inizializzazione-server DTLS

La modalità server DTLS Secure NetX è diversa dalla modalità server TLS a causa dell'utilizzo di UDP per il protocollo di trasporto di rete sottostante. Con TCP, la porta è associata a un singolo host remoto per la durata della sessione TLS. Il protocollo UDP non ha alcuna nozione di stato per quanto riguarda l'host remoto, quindi le richieste DTLS da host diversi verranno tutte ricevute nella stessa interfaccia UDP. Di conseguenza, DTLS deve mantenere lo stato della sessione anziché basarsi sul socket come con TLS e TCP. Per questo motivo, il blocco di controllo del server DTLS (NX_SECURE_DTLS_SERVER) mantiene un mapping delle informazioni sull'host remoto (indirizzo IP e porta) alle sessioni di DTLS. Tutti i dati in ingresso nel socket UDP assegnato a un server DTLS verranno mappati a una sessione DTLS nuova o esistente basata sull'host remoto. Per questo motivo, la creazione del server DTLS richiede diversi parametri oltre a quelli necessari per i client TLS e DTLS.

Oltre al blocco di controllo server DTLS, a ciphersuites TLS e al buffer di area scratch/metadati di crittografia, i server DTLS richiedono un buffer per mantenere le sessioni DTLS e un buffer di riassemblaggio pacchetti usato per decrittografare i record DTLS in arrivo.

Oltre ai buffer della sessione, i server DTLS richiedono un *certificato digitale*, ovvero un documento usato per identificare il server TLS per il client TLS connesso e la *chiave privata* corrispondente dei certificati, in genere per l'algoritmo di crittografia RSA. Lo standard International Telecommunications Union X. 509 specifica il formato del certificato usato da TLS/DTLS e sono disponibili numerose utilità per la creazione di certificati digitali X. 509.

Per NetX Secure DTLS, il certificato X. 509 deve essere codificato in formato binario usando il formato Distinguished Encoding Rules (DER) di ASN. 1. DER è il formato binario standard TLS in transito per i certificati.

La chiave privata associata al certificato specificato deve essere in formato DER-Encoded PKCS # 1. La chiave privata viene usata solo sul dispositivo e non verrà mai trasmessa in rete. Mantieni sicure le chiavi private perché forniscono la sicurezza per le comunicazioni TLS/DTLS.

Per inizializzare il certificato del server DTLS, è necessario che l'applicazione fornisca un puntatore a un buffer che contiene il certificato X. 509 con codifica der e i dati facoltativi della chiave privata PKCS # 1 RSA codificata con il servizio ***nx_secure_x509_certificate_intialize*** , che popola la struttura **NX_SECURE_X509_CERT** con i dati del certificato appropriati per l'uso da parte di TLS.

Una volta inizializzato, il certificato del server deve essere aggiunto al blocco di controllo TLS utilizzando il servizio ***nx_secure_dtls_server_local_certificate_add*** .

Una volta che il certificato del server è stato aggiunto al blocco di controllo del server DTLS, il server può essere usato per le comunicazioni DTLS sicure (vedere l'esempio precedente).

### <a name="initialization--dtls-client"></a>Inizializzazione-client DTLS

NetX Secure DTLS Client Mode è un'operazione semplice rispetto al server DTLS poiché esiste una sola connessione in uscita all'host remoto sul socket UDP.

Per configurare un client DTLS, è necessario un *archivio certificati attendibile*, ovvero una raccolta di certificati digitali con codifica X. 509 provenienti da autorità di certificazione attendibili (CA). Questi certificati vengono considerati attendibili dal protocollo DTLS e vengono usati come base per l'autenticazione dei certificati forniti dalle entità del server DTLS all'applicazione client Secure DTLS di NetX.

Un certificato CA attendibile può essere *autofirmato* o firmato da un'altra CA, nel qual caso il certificato viene definito *CA intermedia* (ICA). In una tipica applicazione TLS/DTLS il server fornisce i certificati ICA insieme al certificato del server, ma l'unico requisito per la corretta autenticazione è che una catena di autorità emittenti (certificati usati per firmare altri certificati) può essere ritracciata dal certificato del server a un certificato CA attendibile nell'archivio certificati attendibili. Questa catena è nota come *catena di attendibilità* o *catena di certificati*.

Per inizializzare una CA attendibile o un certificato ICA, l'applicazione deve fornire un puntatore a un buffer contenente il certificato X. 509 con codifica DER usando il servizio ***nx_secure_x509_certificate_intialize** _, che popola la struttura _ *NX_SECURE_X509_CERT** con i dati del certificato appropriati per l'uso da parte di TLS.

Il client DTLS necessita inoltre di spazio per l'allocazione del certificato del server in ingresso (presupponendo che non venga utilizzata una modalità di chiave pre-condivisa) e un buffer per l'assemblaggio dei pacchetti nei record DTLS da decrittografare. Questi buffer vengono passati come parametri al servizio ***nx_secure_dtls_session_create*** . per altre informazioni, vedere riferimento all'API.

I certificati attendibili che sono stati inizializzati vengono quindi aggiunti al blocco di controllo della sessione DTLS creato tramite il servizio ***nx_secure_dtls_session_trusted_certificate_add*** . Se non si aggiunge un certificato, la sessione client di DTLS non riuscirà perché il protocollo DTLS non sarà in grado di autenticare gli host server remoti.

Una volta creata l'archivio certificati attendibili, la sessione può essere usata per stabilire una connessione client TLS sicura.

### <a name="application-interface-calls"></a>Chiamate dell'interfaccia dell'applicazione

Le applicazioni NetX sicure DTLS in genere eseguono chiamate di funzione dall'interno dei thread dell'applicazione in esecuzione con ThreadX RTO. Alcune inizializzazioni, in particolare per i protocolli di comunicazione di rete sottostanti (ad esempio UDP e IP), possono essere chiamate da ***tx_application_define *.** Per ulteriori informazioni sull'inizializzazione delle comunicazioni di rete, vedere il manuale dell'utente di NetX/NetXDuo.

DTLS USA in modo intensivo le routine di crittografia che sono operazioni che richiedono un utilizzo intensivo del processore. In genere, queste operazioni verranno eseguite nel contesto del thread chiamante.

### <a name="dtls-session-start"></a>Avvio della sessione di DTLS

Per il funzionamento di DTLS è necessario un protocollo di rete a livello di trasporto sottostante. Il protocollo usato in genere è TCP. Per stabilire una sessione TLS sicura NetX, è necessario creare una **NX_UDP_SOCKET** e passarla al servizio **_Nx_secure_dtls_client_session_start_** per i client DTLS.

I server DTLS funzionano in modo diverso. Il socket UDP usato per le richieste client DTLS in ingresso è contenuto all'interno del blocco di controllo NX_SECURE_DTLS_SERVER e viene inizializzato nella chiamata a ***nx_secure_dtls_server_create** _, che accetta la porta UDP locale come parametro. Il _*_nx_secure_dtls_server_start_*_ del servizio viene quindi utilizzato per avviare il server DTLS per la gestione delle richieste in ingresso. Tutte le richieste in ingresso vengono gestite nelle routine di callback fornite per _nx_secure_dtls_server_create *: una per le connessioni e una per le notifiche di ricezione. L'applicazione deve gestire l'avvio della sessione DTLS quando viene ricevuta una notifica di connessione (la chiamata a Connect Notify viene richiamata da DTLS) chiamando ***nx_secure_dtls_server_session_start**_. L'applicazione deve inoltre gestire i dati in ingresso quando viene richiamato il callback di notifica di ricezione (che segue un handshake DTLS completato) chiamando _ *_nx_secure_dtls_session_receive_* *. I dettagli di questa operazione sono disponibili nell'esempio precedente e nella Guida di riferimento alle API per ognuno dei servizi menzionati in precedenza.

### <a name="dtls-packet-allocation"></a>Allocazione pacchetti DTLS

NetX Secure DTLS usa la stessa struttura di pacchetti di NetX/NetXDuo TCP (***NX_PACKET** _) ad eccezione del fatto che anziché chiamare il servizio _*_nx_packet_allocate_*_ , è necessario chiamare il servizio _ *_nx_secure_dtls_packet_allocate_** in modo che lo spazio per l'intestazione DTLS possa essere allocato correttamente.

### <a name="dtls-session-send"></a>Invio sessione DTLS

Una volta avviata la sessione TLS, l'applicazione può inviare dati utilizzando il servizio ***nx_secure_dtls_session_send*** . Il servizio di invio è identico in uso al servizio ***nx_udp_socket_send** _, accettando una struttura di dati _ *_NX_PACKET_** contenente i dati inviati, un indirizzo IP di destinazione e una porta UDP di destinazione.

> [!IMPORTANT]
> Quando si inviano dati con nx_secure_dtls_session_send, è importante usare lo stesso indirizzo IP e la stessa porta usati per stabilire la sessione DTLS, a meno che non esista un meccanismo per spostare la sessione in un nuovo indirizzo e una porta UDP in tempo reale (questo non è comune).

Tutti i dati inviati tramite DTLS verranno crittografati dallo stack NX Secure DTLS e dalle routine di crittografia configurate prima di essere inviate.

### <a name="dtls-session-receive"></a>Ricezione sessione DTLS

Una volta avviata la sessione DTLS, l'applicazione può iniziare a ricevere dati utilizzando il servizio ***nx_secure_Dtls_session_receive** _. Analogamente all'invio della sessione DTLS, questo servizio è identico a _ *_nx_udp_socket_receive_* *, ad eccezione del fatto che i dati in ingresso vengono decrittografati e verificati dallo stack DTLS prima di essere restituiti nella struttura del pacchetto.

### <a name="tls-session-close"></a>Chiusura sessione TLS

Una volta completata la sessione DTLS, il client e il server DTLS devono inviare un avviso CloseNotify all'altro lato per arrestare la sessione. Entrambi i lati devono ricevere ed elaborare l'avviso per garantire una corretta chiusura della sessione.

Se l'host remoto invia un avviso CloseNotify, tutte le chiamate al servizio ***nx_secure_dtls_session_receive** _ elaborerà l'avviso, invierà l'avviso corrispondente all'host remoto e restituirà il valore _ *_NX_SECURE_TLS_SESSION_CLOSED_* *. Una volta chiusa la sessione, eventuali ulteriori tentativi di invio o ricezione di dati con la sessione DTLS avranno esito negativo.

Se l'applicazione desidera chiudere la sessione TLS, il servizio ***nx_secure_dtls_session_end** _ deve essere chiamato. Il servizio invierà l'avviso CloseNotify ed elaborerà la risposta CloseNotify. Se la risposta non viene ricevuta, viene restituito un valore di errore _ *_NX_SECURE_TLS_SESSION_CLOSE_FAIL_**, che indica che la sessione DTLS non è stata arrestata in modo corretto, una possibile violazione della sicurezza.

### <a name="tlsdtls-alerts"></a>Avvisi TLS/DTLS

TLS/DTLS è progettato per garantire la massima sicurezza, quindi qualsiasi comportamento errato nel protocollo viene considerato una potenziale violazione della sicurezza. Per questo motivo, gli eventuali errori di elaborazione dei messaggi o di crittografia/decrittografia sono considerati errori irreversibili che terminano immediatamente l'handshake o la sessione.

Anche se la gestione degli errori in un'applicazione locale è relativamente semplice, l'host remoto deve essere in grado di rilevare che si è verificato un errore per gestire correttamente la situazione ed evitare ulteriori possibili violazioni della sicurezza. Per questo motivo, TLS/DTLS invierà un messaggio di *avviso* all'host remoto su qualsiasi errore.

Gli avvisi vengono gestiti in modo analogo a qualsiasi altro messaggio TLS/DTLS e vengono crittografati durante la sessione per impedire a un utente malintenzionato di raccogliere informazioni dal tipo di avviso fornito. Durante l'handshake, gli avvisi inviati hanno un ambito limitato per limitare la quantità di informazioni che possono essere ottenute da un potenziale utente malintenzionato.

L'avviso CloseNotify, usato per chiudere la sessione TLS/DTLS, è l'unico avviso non irreversibile. Sebbene venga considerato un avviso e venga inviato come messaggio di avviso, un CloseNotify è diverso dagli altri avvisi in quanto non indica che si è verificato un errore.

### <a name="tlsdtls-session-renegotiation-and-resumption"></a>Rinegoziazione e ripresa della sessione TLS/DTLS

TLS supporta la nozione di "rinegoziazione", che è semplicemente una rinegoziazione dei parametri della sessione TLS all'interno del contesto di una sessione TLS esistente.

La *ripresa* della sessione TLS non può essere confusa con la *rinegoziazione* della sessione, nonostante alcune analogie. Quando la *rinegoziazione* della sessione comporta l'avvio di un nuovo handshake in una sessione TLS esistente, la *ripresa* della sessione è una funzionalità puramente facoltativa che prevede il riavvio di una sessione TLS chiusa senza eseguire un handshake TLS completo.

NX Secure DTLS gestisce le richieste di rinegoziazione in ingresso dagli host remoti. **Non supporta la ripresa** della sessione. Una descrizione più completa di queste funzionalità è disponibile nel capitolo 3 della Guida dell'utente di NetX Secure TLS.

### <a name="protocol-layering"></a>Layering del protocollo

Il protocollo TLS (e quindi DTLS) si inserisce nello stack di rete tra il livello di trasporto (ad esempio TCP o UDP) e il livello dell'applicazione. TLS viene a volte considerato un protocollo di livello trasporto, di conseguenza la sicurezza a *livello di trasporto* , ma poiché funge da applicazione per quanto riguarda i protocolli di rete sottostanti, viene talvolta raggruppato nel livello dell'applicazione.

TLS richiede un protocollo di livello trasporto che supporta il recapito in ordine e senza perdita di contenuti, ad esempio TCP. A causa di questo requisito, TLS non può essere eseguito su UDP Poiché UDP non garantisce il recapito di datagrammi. *DTLS* è una versione modificata di TLS. viene usato per le applicazioni che richiedono la sicurezza di TLS su un protocollo di datagramma come UDP.

![Diagramma di un livello del protocollo TLS.](media/image6.png)

**Figura 4-livelli di protocollo TCP/IP, UDP e TLS/DTLS**

## <a name="network-communications-security-and-encryption"></a>Sicurezza e crittografia delle comunicazioni di rete

La protezione delle comunicazioni tramite reti pubbliche e Internet è un argomento di importanza critica e l'oggetto di un ampio numero di libri, articoli e soluzioni. Questo argomento è molto complesso, ma può essere ridotto a una semplice idea: invio di informazioni su una rete, in modo che solo la destinazione prevista possa accedere o modificare tali informazioni. Questa operazione suddivide in tre concetti importanti: segretezza, integrità e autenticazione. Il protocollo TLS/DTLS fornisce soluzioni per tutti e tre.

La crittografia viene usata in modi diversi per garantire segrete, integrità e autenticazione nei protocolli TLS e DTLS. La crittografia deve essere fornita a TLS o DTLS al momento della creazione di una sessione o di un'istanza del server, poiché TLS fornisce un framework flessibile per l'uso della crittografia e non la crittografia stessa. NetX Secure DTLS fornisce le routine di crittografia necessarie per la maggior parte delle applicazioni, pertanto non è necessario preoccuparsi di trovare la crittografia appropriata.

Una descrizione più dettagliata di questi argomenti è disponibile nel capitolo 3 del manuale dell'utente di NetX Secure TLS.

## <a name="tls-and-dtls-extensions"></a>Estensioni TLS e DTLS

TLS (e pertanto DTLS) fornisce una serie di estensioni che forniscono funzionalità aggiuntive per alcune applicazioni. Queste estensioni vengono in genere inviate come parte dei messaggi ClientHello o ServerHello, indicando a un host remoto il desiderio di usare un'estensione o fornire dettagli aggiuntivi da usare per stabilire la sessione TLS sicura.

NetX Secure DTLS supporta tutte le estensioni disponibili in NetX Secure TLS e una descrizione completa di queste sono disponibili nella Guida per l'utente di NetX Secure TLS, capitolo 3.

## <a name="authentication-methods"></a>Authentication Methods

TLS e DTLS forniscono il Framework per stabilire una connessione sicura tra due dispositivi su una rete non sicura, ma parte del problema sta conoscendo l'identità del dispositivo all'altra estremità della connessione. Senza un meccanismo per l'autenticazione dell'identità degli host remoti, diventa un'operazione semplice che un utente malintenzionato potrebbe rappresentare come un dispositivo attendibile.

Inizialmente, potrebbe sembrare che l'uso di indirizzi IP, gli indirizzi MAC hardware o DNS forniscono un livello di attendibilità relativamente elevato per l'identificazione degli host in una rete, ma con la natura della tecnologia TCP/IP e la facilità con cui gli indirizzi possono essere falsificati e le voci DNS danneggiate, ad esempio tramite l'avvelenamento della cache DNS, risulta evidente che TLS necessita di un ulteriore livello di protezione contro le identità fraudolente.

Esistono diversi meccanismi che possono fornire questo livello aggiuntivo di autenticazione per TLS, ma il più comune è il *certificato digitale.* Altri meccanismi includono chiavi precondivise (PSK) e schemi di password.

### <a name="digital-cerificates"></a>Certificati digitali

I certificati digitali sono il metodo più comune per autenticare un host remoto in TLS. In sostanza, un certificato digitale è un documento con una formattazione specifica che fornisce informazioni sull'identità per un dispositivo in una rete di computer.

TLS usa in genere un formato denominato X. 509, uno standard sviluppato dall'Unione di telecomunicazione internazionale, sebbene sia possibile usare altri formati di certificati se gli host TLS possono accettare il formato usato. X. 509 definisce un formato specifico per i certificati e varie codifiche che possono essere utilizzate per produrre un documento digitale. La maggior parte dei certificati X. 509 usati con TLS viene codificata usando una variante di ASN. 1, un altro standard di telecomunicazione. All'interno di ASN. 1 sono disponibili diverse codifiche digitali, ma la codifica più comune per i certificati TLS è lo standard Distinguished Encoding Rules (DER). DER è un subset semplificato delle regole di codifica di base ASN. 1 progettato per essere non ambiguo, semplificando l'analisi. In transito, i certificati TLS vengono in genere codificati in DER binario e questo è il formato previsto da NetX Secure per i certificati X. 509.

Sebbene i certificati binari in formato DER vengano usati nel protocollo TLS effettivo, possono essere generati e archiviati in una serie di codifiche diverse, con estensioni di file quali PEM, CRT e P12. Le diverse varianti vengono utilizzate da diverse applicazioni di produttori diversi, ma in genere possono essere convertite in DER utilizzando strumenti ampiamente disponibili.

La più comune delle codifiche alternative dei certificati è PEM. Il formato PEM (da Privacy-Enhanced mail) è una versione con codifica 64 della codifica DER utilizzata spesso in quanto la codifica produce testo stampabile che può essere facilmente inviato tramite posta elettronica o protocolli basati sul Web.

La generazione di un certificato per l'applicazione NetX Secure è generalmente al di fuori dell'ambito di questo manuale, ma lo strumento da riga di comando OpenSSL ([www.openssl.org](http://www.openssl.org)) è ampiamente disponibile ed è in grado di eseguire la conversione tra la maggior parte dei formati.

A seconda dell'applicazione, è possibile generare certificati, fornire certificati da un produttore o da un'organizzazione governativa oppure acquistare certificati da un'autorità di certificazione commerciale.

Per usare un certificato digitale nell'applicazione NetX Secure, è necessario innanzitutto convertire il certificato in un formato DER binario e, facoltativamente, convertire la chiave privata associata ("esponente privato" per RSA, ad esempio) in un formato binario, in genere una chiave RSA codificata in formato PKCS # 1. Al termine della conversione, è possibile caricare il certificato e la chiave privata nel dispositivo. Le opzioni possibili includono l'uso di un file system basato su Flash o la generazione di una matrice C dai dati (usando uno strumento come "XXD" da Linux) e la compilazione del certificato e della chiave nell'applicazione come dati costanti.

Una volta caricato il certificato nel dispositivo, è possibile usare l'API DTLS per associare il certificato a una sessione o a un server di DTLS.

Per informazioni dettagliate ed esempi su come usare i certificati X. 509 con NetX Secure DTLS, vedere la sezione relativa all'importazione di certificati X. 509 in NetX Secure nel manuale dell'utente di NetX Secure TLS.

Per ulteriori informazioni, fare riferimento ai seguenti servizi DTLS nelle informazioni di riferimento sulle API:

- nx_secure_x509_certificate_initialize,
- nx_secure_dtls_session_local_certificate_add,
- nx_secure_dtls_server_local_certificate_add,
- nx_secure_dtls_session_local_certificate_remove,
- nx_secure_dtls_server_local_certificate_remove,
- nx_secure_dtls_session_trusted_certificate_add,
- nx_secure_dtls_server_trusted_certificate_add,
- nx_secure_dtls_session_trusted_certificate_remove
- nx_secure_dtls_server_trusted_certificate_remove

### <a name="tls-client-certificate-specifics"></a>Specifiche del certificato client TLS

Le implementazioni client di DTLS in genere non richiedono il caricamento di un certificato locale nel dispositivo. Un certificato locale è un certificato che identifica il dispositivo locale. In particolare, un certificato locale fornisce informazioni sull'identità per il dispositivo su cui viene caricata l'applicazione TLS/DTLS. L'eccezione è rappresentata dal caso in cui l'autenticazione del certificato client è abilitata, ma è meno comune.

Un client DTLS richiede che venga caricato almeno un certificato attendibile (è possibile che ne venga caricato altri se richiesto) e che sia disponibile spazio per l'allocazione di un certificato remoto. Un certificato attendibile è un certificato che fornisce una base per l'attendibilità e l'autenticazione del dispositivo remoto, direttamente o tramite un'infrastruttura a chiave pubblica (PKI). La radice della catena di trust è in genere denominata autorità di certificazione o certificato della CA. Un certificato remoto fa riferimento al certificato inviato dall'host remoto durante l'handshake TLS. Fornisce l'identità per quell'host remoto ed è autenticato confrontandolo con un certificato attendibile nel dispositivo locale.

Per ulteriori informazioni sull'aggiunta di certificati attendibili e sull'allocazione dello spazio per i certificati remoti, vedere le informazioni di riferimento sulle API TLS per i servizi seguenti: nx_secure_dtls_session_create, nx_secure_dtls_session_trusted_certificate_add.

### <a name="tlsdtls-server-certificate-specifics"></a>Specifiche del certificato del server TLS/DTLS

Le implementazioni del server DTLS in genere non richiedono il caricamento di certificati "Trusted" sul dispositivo o sui certificati remoti da allocare. L'eccezione è rappresentata dal momento in cui è abilitata l'autenticazione del certificato client.

Un server TLS richiede il caricamento di un certificato "locale" (o "identità"), in modo che il server possa fornirlo al client remoto durante l'handshake TLS per autenticare il server al client.

Per altre informazioni sul caricamento dei certificati locali per l'uso con le applicazioni server TLS NetX, vedere le informazioni di riferimento sulle API per i servizi seguenti: nx_secure_dtls_server_local_certificate_add, nx_secure_dtls_server_local_certificate_remove.


### <a name="pre-shared-keys-psk"></a>Chiavi precondivise (PSK)

Un meccanismo alternativo per fornire l'autenticazione di identificazione in TLS è il concetto di chiavi precondivise (PSK). L'uso di un ciphersuite PSK Elimina la necessità di eseguire le operazioni di crittografia a chiave pubblica con utilizzo intensivo del processore, un vantaggio per i dispositivi embedded con vincoli di risorse. La PSK sostituisce il certificato nell'handshake TLS/DTLS e viene usato al posto del segreto pre-master crittografato per la generazione della chiave di sessione TLS/DTLS.

I ciphersuites di PSK sono limitati nel senso che un segreto condiviso deve essere presente in entrambi i dispositivi prima che sia possibile stabilire una sessione TLS/DTLS. Ciò significa che i dispositivi devono essere stati caricati con tale segreto usando un mezzo sicuro diverso da una connessione PSK TLS. precondivise può essere aggiornato tramite una connessione PSK TLS, ma il dispositivo deve necessariamente iniziare con una PSK che viene caricata tramite un altro meccanismo. Ad esempio, un dispositivo sensore e il relativo dispositivo gateway potrebbero essere caricati con precondivise nella Factory prima della spedizione oppure è possibile usare una connessione TLS standard (con un certificato) per caricare la PSK.

Le ciphersuites PSK sono disponibili in un paio di forme, descritte in RFC 4279. Il primo usa le chiavi RSA o Diffie-Hellman utilizzate allo stesso modo delle chiavi pubbliche trasmesse nel certificato negli handshake TLS standard. Il secondo formato, che è più usato in un ambiente con vincoli di risorse, usa un PSK usato per generare direttamente le chiavi della sessione (per l'uso da parte di AES, ad esempio), evitando l'uso delle operazioni RSA o Diffie-Hellman onerose.

NetX Secure supporta la seconda forma di PSK ciphersuites, consentendo alle applicazioni di rimuovere tutto il codice di crittografia a chiave pubblica e l'utilizzo della memoria. La PSK stessa non è una chiave AES, ma può essere considerata come una password da cui vengono generate le chiavi effettive. Esistono alcune restrizioni relative al valore di PSK, sebbene i valori più lunghi forniscano maggiore sicurezza (come per le password).

Per usare PSK con l'applicazione NetX Secure, è necessario innanzitutto definire la macro globale **NX_SECURE_ENABLE_PSK_CIPHERSUITES**. Questa operazione viene in genere eseguita tramite le impostazioni del compilatore, ma la definizione può anche essere inserita nel file di intestazione nx_secure_tls. h. Con la macro definita, il supporto di PSK ciphersuite verrà compilato nell'applicazione NetX Secure DTLS.

Con il supporto di PSK abilitato, è possibile usare l'API DTLS per configurare precondivise per l'applicazione. Ogni PSK richiederà un valore PSK (il segreto effettivo "Key"-Mantieni questo valore safe), un valore "Identity" usato per identificare il PSK specifico e un "hint di identità" usato da un server TLS per scegliere un particolare valore PSK.

La PSK può essere qualsiasi valore binario perché non viene mai inviato tramite una connessione di rete. La PSK può essere di qualsiasi valore fino a 64 byte di lunghezza.

L'identità e l'hint devono essere stringhe di caratteri stampabili formattate con UTF-8. I valori Identity e hint possono avere una lunghezza fino a 128 byte.

Identity e PSK formano una coppia univoca che viene caricata in ogni dispositivo della rete che deve comunicare tra loro.

Il "suggerimento" viene usato principalmente per la definizione di profili applicazione specifici per raggruppare precondivise in base alla funzione o al servizio. Questi valori devono essere concordati in anticipo e dipendono dall'applicazione. Ad esempio, l'applicazione server della riga di comando OpenSSL (con la funzionalità PSK abilitata) usa la stringa predefinita "Client_identity", che deve essere fornita da un client TLS per continuare con l'handshake TLS.

Per altre informazioni su precondivise, vedere le informazioni di riferimento sulle API NetX sicure per i servizi seguenti: nx_secure_dtls_psk_add, nx_secure_dtls_server_psk_add.

## <a name="importing-x509-certificates-into-netx-secure"></a>Importazione di certificati X. 509 in NetX Secure

Per la maggior parte delle connessioni TLS su Internet sono necessari certificati digitali. I certificati forniscono un metodo per l'autenticazione di host sconosciuti in precedenza tramite Internet tramite l'utilizzo di intermediari attendibili, in genere detti *autorità di certificazione* o CA. Per connettere il dispositivo NetX Secure a un servizio cloud commerciale, ad esempio Amazon Web Services, sarà necessario importare i certificati nell'applicazione eseguendone il caricamento nel dispositivo.

Insieme ai certificati, a volte è necessaria anche una *chiave privata* associata al certificato. In alcune applicazioni, ad esempio client TLS quando non si usa l'autenticazione del certificato client, il certificato da solo sarà sufficiente, ma se il certificato viene usato per identificare il dispositivo, sarà necessaria una chiave privata. Le chiavi private vengono in genere generate quando si crea il certificato e vengono archiviate in un file separato, spesso crittografate con una password.

Per una descrizione dettagliata dell'importazione di certificati in applicazioni NetX Secure, vedere il capitolo 3 del manuale dell'utente di NetX Secure TLS.

## <a name="client-certificate-authentication-in-netx-secure-tls"></a>Autenticazione del certificato client in NetX Secure TLS

Quando si usa l'autenticazione del certificato X. 509, il protocollo TLS/DTLS richiede che l'istanza del server DTLS fornisca un certificato per l'identificazione, ma per impostazione predefinita l'istanza del client DTLS non deve fornire un certificato per l'autenticazione, usando invece un'altra forma di autenticazione, ad esempio una combinazione di nome utente/password. Questo corrisponde all'uso più comune di TLS in Internet per i siti Web. Ad esempio, un sito di vendita al dettaglio online deve dimostrare a un potenziale cliente che utilizza un Web browser che il server è legittimo, ma l'utente utilizzerà un account di accesso/password per accedere a un account specifico.

Tuttavia, il caso predefinito non è sempre auspicabile, quindi TLS/DTLS facoltativamente consente all'istanza del server DTLS di richiedere un certificato dal client remoto. Quando questa funzionalità è abilitata, il server DTLS invierà un messaggio CertificateRequest al client DTLS durante l'handshake. Il client deve rispondere con un certificato autonomo e un messaggio CertificateVerify contenente un token crittografico per dimostrare che il client possiede la chiave privata corrispondente associata a tale certificato. Se la verifica ha esito negativo o il certificato non è connesso a un certificato attendibile nel server, l'handshake TLS ha esito negativo.

Esistono due casi distinti per l'autenticazione del certificato client in TLS: le sezioni seguenti illustrano entrambi i casi.

### <a name="client-certificate-authentication-for-dtls-clients"></a>Autenticazione del certificato client per client DTLS

Un client DTLS può tentare una connessione a un server che richiede un certificato per l'autenticazione client. In questo caso il client deve fornire un certificato al server e verificare che sia proprietario della chiave privata corrispondente o che il server terminerà l'handshake DTLS.

In NetX Secure DTLS non è disponibile alcuna configurazione speciale per supportare questa funzionalità, ma l'applicazione dovrà fornire un certificato di identificazione locale per l'istanza del client TLS usando il servizio *nx_secure_tls_session_local_certificate_add* . Se l'applicazione non fornisce alcun certificato ma il server remoto usa l'autenticazione del certificato client e richiede un certificato, l'handshake DTLS avrà esito negativo. Il certificato fornito alla sessione DTLS con *nx_secure_dtls_session_local_certificate_add* deve essere riconosciuto dal server remoto per completare l'handshake DTLS.

### <a name="client-certificate-authentication-for-tls-servers"></a>Autenticazione del certificato client per i server TLS

Il caso del server DTLS per l'autenticazione del certificato client è leggermente più complesso rispetto al caso del client di DTLS perché la funzionalità è facoltativa. In questo caso, il server TLS deve richiedere specificamente un certificato dal client TLS remoto, quindi elaborare il messaggio CertificateVerify per verificare che il client remoto sia proprietario della chiave privata corrispondente, quindi il server deve verificare che il certificato fornito dal client possa essere tracciato a un certificato nell'archivio certificati attendibili locale.

Nelle istanze del server TLS protette NetX, l'autenticazione del certificato client è controllata dai servizi *nx_secure_dtls_server_x509_client_verify_configure* e *nx_secure_dtls_server_x509_client_verify_disable* .

Per abilitare l'autenticazione del certificato client, un'applicazione deve chiamare *nx_secure_dtls_server_x509_client_verify_configure* con l'istanza della sessione del server DTLS prima di chiamare *nx_secure_dtls_server_start*. Per la verifica è necessario allocare spazio per i certificati client in ingresso forniti come parametro per *nx_secure_dtls_server_x509_client_verify_configure.* Si noti che il buffer deve essere sufficientemente grande da contenere la catena di certificati a dimensione massima fornita da un client per *il numero di sessioni del server DTLS*. Ogni sessione del server richiede spazio che verrà allocato dal singolo buffer fornito. Verificare che il buffer sia sufficientemente grande o che si verifichi un errore se la catena di certificati client specificata è troppo grande.

Quando è abilitata l'autenticazione del certificato client, il server DTLS richiederà un certificato dal client DTLS remoto durante l'handshake DTLS. In NetX Secure DTLS server, il certificato client viene verificato rispetto all'archivio dei certificati attendibili creati con *nx_secure_dtls_server_trusted_certificate_add* seguendo la catena di emittenti X. 509. Il client remoto deve fornire una catena che connette il certificato di identità a un certificato nell'archivio attendibile oppure l'handshake DTLS avrà esito negativo. Inoltre, se l'elaborazione del messaggio CertificateVerify ha esito negativo, anche l'handshake DTLS avrà esito negativo.

I metodi di firma usati per il metodo CertificateVerify sono corretti per TLS versione 1,0 e TLS versione 1,1 e sono specificati dal server TLS in TLS versione 1,2, su cui si basa NetX Secure DTLS. Per DTLS 1,2, i metodi di firma supportati in genere seguono i metodi pertinenti forniti nella tabella del metodo crittografico, ma in genere RSA con SHA-256 (vedere la sezione "crittografia in NetX Secure TLS" per altre informazioni sull'inizializzazione di TLS con i metodi di crittografia).

## <a name="cryptography-in-netx-secure-tls"></a>Crittografia in NetX Secure TLS

TLS definisce un protocollo in cui è possibile usare la crittografia per proteggere le comunicazioni di rete. Per questo motivo, lascia che la crittografia effettiva venga usata in modo abbastanza ampio per gli utenti TLS. La specifica richiede l'implementazione di un solo ciphersuite: nel caso di TLS 1,2, ciphersuite è TLS_RSA_WITH_AES_128_CBC_SHA, che indica l'uso di RSA per le operazioni a chiave pubblica, AES in modalità CBC con chiavi a 128 bit per la crittografia della sessione e SHA-1 per gli hash di autenticazione dei messaggi.

Essendo conforme a TLS 1,2, NetX Secure Abilita il ciphersuite obbligatorio TLS_RSA_WITH_AES_128_CBC_SHA per impostazione predefinita, ma dato il numero di possibili implementazioni per ciascuno dei metodi crittografici a causa di funzionalità hardware e altre considerazioni, NetX Secure fornisce un'API di crittografia generica che consente a un utente di specificare i metodi crittografici da usare con TLS.

> [!NOTE]
> Il meccanismo di API crittografico generico consente inoltre agli utenti di implementare il proprio ciphersuites, ma questa opzione è consigliata per gli utenti avanzati che hanno familiarità con le estensioni e ciphersuites di TLS. Se si è interessati a supportare il proprio ciphersuites, contattare il rappresentante della logica Express.

Per informazioni dettagliate su come configurare i metodi crittografici per DTLS, vedere il manuale dell'utente di NetX Secure TLS, capitolo 3. Lo stesso processo si applica sia a TLS che a DTLS.
