---
title: Capitolo 3 - Descrizione funzionale di Azure RTOS NetX Secure
description: Questo capitolo contiene una descrizione funzionale di NetX Secure TLS.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 711195e60771ebd467c69df49ef7665f32e13a17c21ca839404e829449cf1401
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797984"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-secure"></a>Capitolo 3 - Descrizione funzionale di Azure RTOS NetX Secure

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Questo capitolo contiene una descrizione funzionale Azure RTOS NetX Secure TLS. Esistono due tipi principali di esecuzione del programma in un'applicazione NETX Secure TLS: inizializzazione e chiamate all'interfaccia dell'applicazione. 

*NetX Secure presuppone l'esistenza di ThreadX e NetX/NetXDuo. Da ThreadX, richiede l'esecuzione del thread, la sospensione, i timer periodici e le funzionalità di esclusione reciproca. Da NetX/NetXDuo sono necessari i driver e le strutture di rete TCP/IP.*

## <a name="transport-layer-security-tls-and-secure-sockets-layer-ssl"></a>Transport Layer Security (TLS) e Secure Sockets Layer (SSL)

Il componente secure network protocol di NetX secure è un'implementazione del protocollo Transport Layer Security (TLS), come descritto in RFC 2246 (versione 1.0), 4346 (versione 1.1), 5246 (versione 1.2) e 8446 (versione 1.3). Sono incluse anche routine di supporto per X.509 di base (RFC 5280).

NetX Secure TLS supporta le versioni 1.2 e 1.3 di TLS. Le implementazioni vengono fornite per TLS 1.0 e TLS 1.1, ora deprecate, ma devono essere inizializzate in modo esplicito e non sono consigliate per l'uso nei nuovi prodotti.

*Secure Sockets Layer* (SSL) era il nome originale di TLS prima che diventasse uno standard in RFC 2246 e "SSL" viene spesso usato come nome generico per i protocolli TLS. L'ultima versione di SSL era la 3.0 e TLS 1.0 è talvolta denominato SSL versione 3.1. Tutte le versioni del protocollo "SSL" ufficiale sono considerate obsolete e non sicure e attualmente NetX Secure non fornisce un'implementazione SSL.

TLS specifica un protocollo  per generare le chiavi di sessione create durante *l'handshake* TLS tra un client e un server TLS e tali chiavi vengono usate per crittografare i dati inviati dall'applicazione durante la sessione *TLS.*

I dati TLS sono *suddivisi in* record che sono equivalenti in concetto a un pacchetto TCP. Ogni record TLS ha un'intestazione e anche i record crittografati CON TLS hanno un piè di pagina (hash checksum). I record di handshake TLS hanno un'intestazione aggiuntiva incapsulata all'interno del record TLS più grande. Il record TLS viene incapsulato dal protocollo di rete del livello trasporto nello stesso modo in cui un pacchetto TCP viene incapsulato da un pacchetto IP.

### <a name="tls-13"></a>TLS 1.3

Ad agosto 2018 è stata finalizzata la specifica TLS 1.3. La nuova versione del protocollo è un aggiornamento piuttosto significativo che modifica alcuni aspetti fondamentali della sicurezza e delle prestazioni sottostanti di TLS. Tuttavia, queste modifiche sono in gran parte invisibili all'utente TLS tipico perché si applicano principalmente alla generazione di chiavi della sessione e della macchina a stati dell'handshake TLS. Sono state aggiunte anche alcune funzionalità ed estensioni facoltative. Di seguito è riportato un riepilogo delle modifiche e del modo in cui influiscono sulla funzionalità TLS.

- La macchina a stati dell'handshake è stata ottimizzata rimuovendo un intero scambio di messaggi dal server.
- La generazione di chiavi è stata aggiornata in modo da usare una routine standardizzata denominata HKDF (HMAC-based Key Derivation Function) e consente di aggiungere le chiavi di sessione a tutti i messaggi di handshake (anziché ad alcuni parametri select).
- Tutti i protocolli di crittografia TLS 1.2 e precedenti sono deprecati e non sono compatibili con TLS 1.3. Analogamente, tutti i pacchetti di crittografia TLS 1.3 non sono utilizzabili con le versioni precedenti.
- Tutti i pacchetti di crittografia TLS 1.3 forniscono PFS (Perfect Forward Secrecy) usando chiavi effimere<sup>6</sup> 
- TLS 1.3 rimuove il "codice di autenticazione del messaggio" (MAC) in ogni record a favore dell'uso di crittografia AEAD<sup>7</sup>
- Sono state aggiunte alcune funzionalità facoltative aggiuntive, tra cui 0-RTT (Zero Round Trip Time) che consente l'invio dei dati dell'applicazione durante l'handshake. 0-RTT è puramente facoltativo e non è attualmente supportato Azure RTOS TLS.

TLS 1.3 non influisce in modo significativo sulle applicazioni utente. L'API rimane esattamente la stessa tra le versioni e i ciphersuit sono contrassegnati in modo da poter usare una singola tabella ciphersuite.

Per usare TLS 1.3, la macro NX_SECURE_TLS_ENABLE_TLS_1_3 deve essere definita a livello globale. TLS 1.3 è disabilitato per impostazione predefinita Azure RTOS TLS.

6. Le chiavi "effimere" sono coppie di chiavi asimmetriche generate durante l'handshake TLS e usate per lo scambio di segreti solo per quella sessione. La coppia di chiavi viene rimossa dopo l'uso, in modo da impedire a un utente malintenzionato di accedere ai dati crittografati in una sessione TLS registrata anche se una chiave privata del certificato viene compromessa in qualsiasi momento in futuro, quindi "Perfect Forward Secrecy".

7. Crittografia autenticata con dati associati: modalità per crittografie come AES che combina la crittografia e il controllo dell'integrità in una singola operazione, eliminando la necessità di un hash separato dei dati per il controllo dell'integrità.

### <a name="tls-record-header"></a>Intestazione del record TLS

Qualsiasi record TLS valido deve avere un'intestazione TLS, come illustrato in Errore. Origine di riferimento non trovata.

![Diagramma di un'intestazione di record TLS.](media/image2.png)

Figura 1: Intestazione del record TLS

I campi dell'intestazione del record TLS sono definiti come segue:

| Campo di intestazione TLS | Scopo     |
| ---------------- | ------------- |
| **Tipo di messaggio a 8 bit** | Questo campo contiene il tipo di record TLS inviato. I tipi validi sono i seguenti:<br />- ChangeCipherSpec<sup>8:</sup>0x14<br />- Avviso: 0x15<br />- Handshake: 0x16<br />- Dati applicazione: 0x17 |
| **Versione del protocollo a 16 bit** | Questo campo contiene la versione del protocollo TLS. I valori validi sono i seguenti:<br />- SSL 3.0: 0x0300<br />- TLS 1.0: 0x0301<br />- TLS 1.1: 0x0302<br />- TLS 1.2: 0x0303<br />- **TLS 1.3 <sup>9:</sup>** **0x0303** |
| **Lunghezza a 16 bit** | Questo campo contiene la lunghezza dei dati incapsulati nel record TLS. |

8. In TLS 1.3 il messaggio ChangeCipherSpec non viene più usato, anche se può comunque essere inviato per motivi di compatibilità, nel qual caso il messaggio viene ignorato.

9. Tls 1.3 avrebbe tecnicamente un valore di 0x0304 se questo schema è stato continuato, ma il protocollo è stato modificato per avere la versione effettiva del protocollo in un'estensione, quindi tutti i record TLS 1.3 usano 0x0303 nei campi della versione del protocollo per la compatibilità con le versioni precedenti.

### <a name="tls-handshake-record-header"></a>Intestazione del record handshake TLS

Qualsiasi record di handshake TLS valido deve avere un'intestazione handshake TLS, come illustrato nella figura 2.

![Diagramma di un'intestazione di record handshake TLS.](media/image3.png)

Figura 2 - Intestazione del record handshake TLS

I campi dell'intestazione del record handshake TLS sono definiti come segue:

| Campo di intestazione TLS | Scopo |
| ---------------- |----------------------- |
| **Tipo di messaggio a 8 bit** | Questo campo contiene il tipo di record TLS inviato. I tipi validi sono i seguenti:<br />- ChangeCipherSpec<sup>10:</sup>0x14<br />- Avviso: 0x15<br />- Handshake: 0x16<br />- Dati applicazione: 0x17 |
| **Versione del protocollo a 16 bit** | Questo campo contiene la versione del protocollo TLS. I valori validi sono i seguenti:<br />- SSL 3.0: 0x0300<br />- TLS 1.0: 0x0301<br />- TLS 1.1: 0x0302<br />- TLS 1.2: 0x0303<br />- **TLS 1.3 <sup>11:</sup>** **0x0303** |
| **Lunghezza a 16 bit**    | Questo campo contiene la lunghezza dei dati incapsulati nel record TLS. |
| **Tipo di handshake a 8 bit** | Questo campo contiene il tipo di messaggio handshake. I valori validi sono i seguenti (*i messaggi in **grassetto** sono stati aggiunti in TLS 1.3):<br />- HelloRequest: 0x00<br />- ClientHello: 0x01<br />- ServerHello: 0x02<br />- **HelloVerifyRequest:** **0x03**<br />- **NewSessionTicket:** **0x04**<br />- **EndOfEarlyData:** **0x05**<br />- **EncryptedExtensions:** **0x08**<br />- Certificato: 0x0B<br />- ServerKeyExchange: 0x0C<br />- CertificateRequest: 0x0D<br />- ServerHelloDone: 0x0E<br />- CertificateVerify: 0x0F<br />- ClientKeyExchange: 0x10<br />- Operazione completata: 0x14<br />- **KeyUpdate**: **0x18**<br />- **MessageHash**: **0xFE** |
| **Lunghezza a 24 bit**    | Questo campo contiene la lunghezza dei dati del messaggio di handshake. |

10. In TLS 1.3 il messaggio ChangeCipherSpec non viene più usato, anche se può comunque essere inviato per motivi di compatibilità, nel qual caso il messaggio viene ignorato.

11. Tls 1.3 avrebbe tecnicamente un valore di 0x0304 se questo schema è stato continuato, ma il protocollo è stato modificato per avere la versione effettiva del protocollo in un'estensione, quindi tutti i record TLS 1.3 usano 0x0303 nei campi della versione del protocollo per la compatibilità con le versioni precedenti.

### <a name="the-tls-handshake-and-tls-session"></a>Handshake TLS e sessione TLS

Un tipico handshake TLS (versioni 1.0-1.2) è illustrato nella figura 3. Un handshake TLS inizia quando il client TLS invia un messaggio *ClientHello* a un server TLS, indicando il suo voler avviare una sessione TLS. Il messaggio contiene informazioni sulla crittografia che il client vuole usare per la sessione, insieme alle informazioni usate per generare le chiavi di sessione in un secondo momento nell'handshake. Fino a quando non vengono generate le chiavi di sessione, tutti i messaggi nell'handshake TLS non vengono crittografati. TLS 1.3 modifica leggermente l'handshake. I dettagli vengono presentati nella sezione successiva.

Il server TLS risponde a ClientHello con un messaggio ServerHello, che indica una selezione tra le opzioni di crittografia fornite dal client. ServerHello è seguito da un messaggio di certificato, in cui il server fornisce un certificato digitale per autenticare la propria identità al client. Infine, il server invia un messaggio ServerHelloDone per indicare che non sono presenti altri messaggi da inviare. Il server può facoltativamente inviare altri messaggi dopo ServerHello e in alcuni casi potrebbe non inviare un messaggio certificato, quindi la necessità del messaggio ServerHelloDone.

Dopo che il client ha ricevuto tutti i messaggi del server, ha informazioni sufficienti per generare le chiavi di sessione. TLS esegue questa operazione creando un bit condiviso di dati casuali denominato *pre-master secret,* che è di dimensioni fisse e viene usato come valore di seed per generare tutte le chiavi necessarie dopo l'allocazione della crittografia. Il segreto pre-master viene crittografato usando l'algoritmo a chiave pubblica (ad esempio RSA) specificato nei messaggi Hello (vedere di seguito per informazioni sugli algoritmi a chiave pubblica) e la chiave pubblica fornita dal server nel certificato. Una funzionalità TLS facoltativa denominata Chiavi precondi condivise (PSK) consente di usare ciphersuit che non usano un certificato ma usano invece un valore segreto condiviso tra gli host (in genere tramite trasferimento fisico o un altro metodo protetto). Il segreto condiviso viene usato per generare il segreto pre-master anziché usare un messaggio crittografato per inviare il segreto pre-master. Vedere la sezione Chiavi precondicondite più avanti.

Il segreto pre-master crittografato viene inviato al server nel messaggio ClientKeyExchange. Il server, alla ricezione del messaggio ClientKeyExchange, decrittografa il segreto pre-master usando la relativa chiave privata e procede alla generazione delle chiavi di sessione in parallelo con il client TLS.

Dopo la generazione delle chiavi di sessione, tutti gli altri messaggi possono essere crittografati usando l'algoritmo a chiave privata (ad esempio AES) selezionato nei messaggi Hello. Un messaggio non crittografato finale denominato ChangeCipherSpec viene inviato sia dal client che dal server per indicare che tutti gli altri messaggi verranno crittografati.

Il primo messaggio crittografato inviato sia dal client che dal server è anche il messaggio di handshake TLS finale, denominato Finished. Questo messaggio contiene un hash di tutti i messaggi di handshake ricevuti e inviati. Questo hash viene usato per verificare che nessuno dei messaggi nell'handshake sia stato manomesso o danneggiato (che indica una possibile violazione della sicurezza).

Dopo la ricezione dei messaggi Finished e la verifica degli hash di handshake, viene avviata la sessione TLS e l'applicazione inizia a inviare e ricevere dati. Per tutti i dati inviati da entrambi i lati durante la sessione TLS viene prima eseguito l'hashing usando l'algoritmo hash scelto nei messaggi Hello (per garantire l'integrità dei messaggi) e crittografati usando l'algoritmo a chiave privata scelto con le chiavi di sessione generate.

Infine, una sessione TLS può essere terminata correttamente solo se il client o il server sceglie di eseguire questa operazione. Una sessione troncata viene considerata una violazione della sicurezza (poiché un utente malintenzionato potrebbe tentare di impedire la ricezione di tutti i dati inviati) quindi viene inviata una notifica speciale quando uno dei due lati vuole terminare la sessione, denominato avviso CloseNotify. Sia il client che il server devono inviare ed elaborare un avviso CloseNotify per un arresto corretto della sessione.

![Diagramma di un handshake TLS tipico.](media/image4.png)

Figura 3: Handshake TLS tipico

### <a name="tls-13-handshake"></a>TLS 1.3 Handshake

TLS 1.3 è una revisione piuttosto importante del protocollo TLS. La maggior parte delle modifiche sono state apportate all'handshake per migliorare la sicurezza e le prestazioni. Un tipico handshake TLS 1.3 è illustrato nella figura 4. La differenza principale si può vedere nel numero di scambi tra il server e il client.

In TLS 1.2 e versioni precedenti, il server invia due voli<sup>12</sup> di messaggi: prima Il ServerHello e quindi un messaggio ChangeCipherSpec prima di inviare il messaggio crittografato Finished che termina l'handshake. In TLS 1.3 il server invia tutti gli elementi nel primo volo: ServerHello, estensioni, certificato e Completato. Il messaggio ChangeCipherSpec è stato eliminato e il server genera le chiavi di sessione e avvia la crittografia dei messaggi di handshake immediatamente dopo ServerHello.

La nuova disposizione significa che più dell'handshake TLS è protetto dalla crittografia, limitando la quantità di dati in testo non crittografato a cui un utente malintenzionato può accedere. Inoltre, la rimozione del secondo volo del server (che era solo un ChangeCipherSpec seguito da un oggetto Finished) significa che un client TLS non deve più attendere per avviare la trasmissione dei dati dell'applicazione. Non appena il client invia il proprio messaggio Finished , la sessione viene avviata.

12. Un volo è semplicemente una raccolta di messaggi TLS inviati contemporaneamente in un gruppo.

![Diagramma di un handshake TLS 1.3.](media/image5.png)

Figura 4 - Handshake TLS 1.3

> [!NOTE]
> *TLS 1.3 ha introdotto anche la nozione di "dati anticipati" e 0-RTT (zero round trip time), vale a dire che alcuni dati dell'applicazione possono essere inviati nel primo volo di messaggi. Questa funzionalità facoltativa è stata aggiunta principalmente come ottimizzazione per la velocità di risposta del Web browser,ad esempio per inviare intestazioni HTTP iniziali per avviare il rendering di una pagina. A Azure RTOS 6.0 questa funzionalità NON è supportata.*

### <a name="initialization"></a>Inizializzazione

Lo stack TCP/IP NetX o NetXDuo deve essere inizializzato prima di usare NetX Secure TLS. Per informazioni su come inizializzare correttamente lo stack TCP/IP, vedere il Manuale dell'utente di NetX o NetXDuo.

Dopo l'inizializzazione dello stack TCP/IP NetX, è possibile abilitato TLS. Internamente, tutto il traffico di rete TLS e l'elaborazione vengono gestiti dallo stack NetX/NetXDuo senza richiedere l'intervento dell'utente. TUTTAVIA, TLS presenta alcuni requisiti specifici che devono essere gestiti separatamente dallo stack di rete sottostante. Questi parametri vengono assegnati al blocco di controllo TLS denominato ***NX_SECURE_TLS_SESSION** _ usando il servizio _ *_nx_secure_tls_session_create_**.

TLS ha due modalità, Server e Client, che possono essere abilitate in un'applicazione (ma solo una modalità per ogni socket NetX) e ognuna ha requisiti specifici, come descritto di seguito.

In entrambe le modalità, NetX Secure TLS richiede la creazione e la configurazione di un socket TCP (***NX_TCP_SOCKET** _) per le comunicazioni TCP con l'host remoto. Il socket TCP viene assegnato a un'istanza di sessione TLS con il servizio _ *_nx_secure_tls_session_start_**, come descritto di seguito.

### <a name="initialization--tls-server"></a>Inizializzazione - Server TLS

Oltre a un socket TCP, la modalità server NETX Secure TLS richiede un certificato digitale *,* ovvero un documento usato per identificare il server TLS al client TLS che si connette e i certificati corrispondenti alla chiave privata *,* in genere per l'algoritmo di crittografia RSA. Lo standard X.509 dell'International Telecommunications Union specifica il formato del certificato usato da TLS e sono disponibili numerose utilità per la creazione di certificati digitali X.509.

Per NetX Secure TLS, il certificato X.509 deve essere codificato in formato binario usando il formato Distinguished Encoding Rules (DER) asn.1. DER è il formato binario tls over-the-wire standard per i certificati.

La chiave privata associata al certificato fornito deve essere DER-Encoded formato PKCS#1. La chiave privata viene usata solo nel dispositivo e non verrà mai trasmessa in rete. Mantenere al sicuro le chiavi private perché forniscono la sicurezza per le comunicazioni TLS.

Per inizializzare il certificato del server TLS, l'applicazione deve fornire un puntatore a un buffer contenente il certificato X.509 con codifica DER e i dati facoltativi della chiave privata RSA PKCS#1 con codifica DER usando il servizio ***nx_secure_x509_certificate_intialize** _, che popola la struttura _ *NX_SECURE_X509_CERT** con i dati del certificato appropriati per l'uso da parte di TLS.

Dopo l'inizializzazione, il certificato del server deve essere aggiunto al blocco di controllo TLS usando il ***nx_secure_tls_local_certificate_add*** servizio.

Dopo che il certificato del server è stato aggiunto al blocco di controllo TLS, il socket può essere usato per stabilire una connessione sicura al server TLS.

### <a name="initialization--tls-client"></a>Inizializzazione - Client TLS

La modalità client TLS sicuro netx richiede un archivio certificati *attendibili,* ovvero una raccolta di certificati digitali con codifica X.509 provenienti da autorità di certificazione (CA) attendibili. Questi certificati vengono considerati "attendibili" dal protocollo TLS e fungono da base per l'autenticazione dei certificati forniti dalle entità server TLS al client TLS sicuro NetX.

Un certificato CA attendibile può essere *autofirmato* o firmato da un'altra CA, nel qual caso tale certificato è denominato *CA* intermedia (ICA). In una tipica applicazione TLS, il server fornisce i certificati ICA insieme al relativo certificato server, ma l'unico requisito per la corretta autenticazione è che una catena di autorità emittente (certificati usati per firmare altri certificati) possa essere tracciata dal certificato del server a un certificato CA attendibile nell'archivio certificati attendibili. Questa catena è nota come catena *di certificati* o catena *di certificati.*

Per inizializzare un certificato CA o ICA attendibile, l'applicazione deve fornire un puntatore a un buffer contenente il certificato X.509 con codifica DER usando il servizio ***nx_secure_x509_certificate_intialize** _, che popola la struttura _ *NX_SECURE_X509_CERT** con i dati del certificato appropriati per l'uso da parte di TLS.

I certificati attendibili inizializzati vengono quindi aggiunti al blocco di controllo TLS usando il ***nx_secure_tls_trusted_certificate_add*** sicurezza. Se non si aggiunge un certificato, la sessione del client TLS avrà esito negativo perché il protocollo TLS non sarà in grado di autenticare gli host del server TLS remoti.

Il client TLS necessita anche di spazio per l'allocazione del certificato del server in ingresso (presupponendo che non venga usata la modalità chiave precondipartita). A data di NetX Secure TLS 5.12, non è più necessario che l'applicazione alloca spazio per il certificato remoto. Tuttavia, l'opzione legacy per allocare spazio per un certificato del server è ancora disponibile e i certificati allocati dall'utente verranno usati prima dell'ottimizzazione del buffer del certificato <sup>interno 13.</sup> Per altre informazioni, vedere il servizio ***nx_secure_tls_remote_certificate_allocate.***

Dopo la creazione dell'archivio certificati attendibili e l'allocazione dello spazio per il certificato del server, è possibile usare il socket per stabilire una connessione client TLS sicura.

13. L'ottimizzazione usa il "buffer di pacchetti" fornito dall'applicazione utente alla sessione TLS usando nx_secure_tls_session_packet_buffer_set per *allocare* le strutture di analisi X.509 invece di usare le strutture fornite dall'utente usate nelle versioni precedenti di NetX Secure TLS. È improbabile che una catena di certificati superi le dimensioni del buffer di pacchetti. In questo caso è possibile aumentare le dimensioni del buffer dei pacchetti o usare *nx_secure_tls _remote_certificate_allocate* per allocare più spazio per la catena di certificati.

### <a name="application-interface-calls"></a>Chiamate all'interfaccia dell'applicazione

Le applicazioni NETX Secure TLS in genere effettuano chiamate di funzione dall'interno dei thread dell'applicazione in esecuzione nell'RTOS ThreadX. Alcune inizializzazioni, in particolare per i protocolli di comunicazione di rete sottostanti (ad esempio TCP e IP) possono essere chiamate da ***tx_application_define*.** Per altre informazioni sull'inizializzazione delle comunicazioni di rete, vedere il Manuale dell'utente di NetX/NetXDuo.

TLS usa in modo intensivo le routine di crittografia che sono operazioni a elevato utilizzo di processore. In genere, queste operazioni verranno eseguite nel contesto del thread chiamante.

### <a name="tls-session-start"></a>Avvio sessione TLS

Per il funzionamento di TLS è necessario un protocollo di rete a livello di trasporto sottostante. Il protocollo in genere usato è TCP. Per stabilire una sessione NETX Secure TLS, è necessario stabilire una connessione TCP usando l'API TCP NetX/NetXDuo. È **NX_TCP_SOCKET** creare un nx_tcp_server_socket_listen e stabilire una connessione usando i servizi **_nx_tcp_server_socket_listen_ _ e *_*_nx_tcp_server_socket_accept_ _ *(per il server TLS)* o il servizio _ _nx_tcp_client_socket_connect_** (per il client TLS).

Una volta stabilita una connessione TCP, il socket TCP viene quindi passato ***al nx_secure_tls_session_start*** servizio.

### <a name="tls-packet-allocation"></a>Allocazione di pacchetti TLS

NetX Secure TLS usa la stessa struttura di pacchetti di NetX/NetXDuo TCP (* NX_PACKET _),**ad** eccezione del fatto che invece di chiamare il servizio _*_nx_packet_allocate,_*_ è necessario chiamare il servizio _ *_nx_secure_tls_packet_allocate_** in modo che lo spazio per l'intestazione TLS possa essere allocato correttamente.

### <a name="tls-session-send"></a>Invio di sessioni TLS

Dopo l'avvio della sessione TLS, l'applicazione può inviare dati usando il **nx_secure_tls_session_send** _. Il servizio di invio è identico in uso al servizio _*_nx_tcp_socket_send,_*_ prendendo una struttura di dati _*_NX_PACKET_*_ contenente i dati inviati, solo i dati verranno crittografati dallo stack NX Secure TLS prima dell'invio e il pacchetto deve essere allocato usando _*_nx_secure_tls_packet_allocate_**.

### <a name="tls-session-receive"></a>Ricezione sessione TLS

Dopo l'avvio della sessione TLS, l'applicazione può iniziare a ricevere dati usando il **nx_secure_tls_session_receive** _. Analogamente _all'invio_ della sessione TLS, questo servizio è identico a _* nx_tcp_socket_receive **, ad eccezione del fatto che i dati in ingresso vengono decrittografati e verificati dallo stack TLS prima di essere restituiti nella struttura dei pacchetti.

### <a name="tls-session-close"></a>Chiusura della sessione TLS

Al termine di una sessione TLS, il client e il server TLS devono inviare un avviso CloseNotify all'altro lato per arrestare la sessione. Entrambi i lati devono ricevere ed elaborare l'avviso per garantire un arresto corretto della sessione.

Se l'host remoto invia un avviso CloseNotify, qualsiasi chiamata al servizio ***nx_secure_tls_session_receive** _ eelaborare l'avviso, inviare l'avviso corrispondente all'host remoto e restituire il valore _*_NX_SECURE_TLS_SESSION_CLOSED_**. Dopo la chiusura della sessione, qualsiasi altro tentativo di inviare o ricevere dati con tale sessione TLS avrà esito negativo.

Se l'applicazione vuole chiudere la sessione TLS, è **necessario nx_secure_tls_session_end** il servizio * nx_secure_tls_session_end _. Il servizio invierà l'avviso CloseNotify ed eelaborare la risposta CloseNotify. Se la risposta non viene ricevuta, verrà restituito un valore di errore _ *_NX_SECURE_TLS_SESSION_CLOSE_FAIL_** , che indica che la sessione TLS non è stata arrestato in modo corretto, una possibile violazione della sicurezza.

### <a name="tls-alerts"></a>Avvisi TLS

TLS è progettato per garantire la massima sicurezza, quindi qualsiasi comportamento errante nel protocollo viene considerato una potenziale violazione della sicurezza. Per questo motivo, eventuali errori nell'elaborazione dei messaggi o nella crittografia/decrittografia sono considerati errori irreversibili che terminano immediatamente l'handshake o la sessione.

Anche se la gestione degli errori in un'applicazione locale è relativamente semplice, l'host remoto deve sapere che si è verificato un errore per gestire correttamente la situazione ed evitare eventuali ulteriori violazioni della sicurezza. Per questo motivo, TLS invierà un *messaggio di* avviso all'host remoto in caso di errore.

Gli avvisi vengono trattati come qualsiasi altro messaggio TLS e vengono crittografati durante la sessione per impedire a un utente malintenzionato di raccogliere informazioni dal tipo di avviso fornito. Durante l'handshake, gli avvisi inviati hanno un ambito limitato per limitare la quantità di informazioni che possono essere ottenute da un potenziale utente malintenzionato.

L'avviso CloseNotify, usato per chiudere la sessione TLS, è l'unico avviso non irreversibile. Sebbene sia considerato un avviso e inviato come messaggio di avviso, closeNotify è diverso da altri avvisi in quanto non indica che si è verificato un errore.

Il valore dell'avviso e il "livello" (i livelli sono "avviso" e "irreversibile". La maggior parte degli avvisi TLS è "irreversibile") sono definiti nelle RFC TLS e indicano il tipo di errore che si è verificato. La maggior parte degli avvisi TLS diversi da CloseNotify può essere considerata un'indicazione di un potenziale problema di sicurezza e comporta l'interruzione della sessione o dell'handshake TLS. Se una chiamata API TLS restituisce **NX_SECURE_TLS_ALERT_RECEIVED** (0x114), il servizio API **_nx_secure_tls_session_alert_value_get_** (novità di NetX Secure TLS versione 5.12) può essere usato per recuperare il valore e il livello di avviso TLS che l'applicazione può usare per eventuali decisioni relative alle risposte ai problemi di sicurezza. Nella maggior parte dei casi, qualsiasi avviso ricevuto dall'host remoto diverso da CloseNotify deve essere considerato un errore irreversibile, anche se sono presenti alcuni escption. Per altre informazioni, vedere le RFC TLS.

### <a name="tls-session-renegotiation"></a>Rinegoziazione della sessione TLS

TLS supporta la nozione di "rinegoziazione", che è semplicemente una rinegoziazione dei parametri della sessione TLS all'interno del contesto di una sessione TLS esistente. Ciò significa in pratica che i nuovi messaggi di handshake vengono crittografati e autenticati usando la sessione esistente. La rinegoziazione viene usata quando un host TLS vuole generare nuovi parametri di sessione (ad esempio, generare nuove chiavi di sessione TLS) senza dover completare la sessione esistente. Ad esempio, la rinegoziazione può essere utile quando i criteri di sicurezza per un'applicazione stabilino che le chiavi di sessione vengono usate solo per un periodo di tempo limitato, ma una sessione TLS rimane attiva oltre tale periodo.

Un problema con la rinegoziazione della sessione è che rende TLS vulnerabile a un attacco Man-in-the-Middle specifico in cui un utente malintenzionato può far sì che un server avvii una rinegoziazione con nuovi parametri, consentendo così all'utente malintenzionato di hijack della sessione TLS. Per attenuare questo problema, è stata introdotta l'estensione Indicazione di rinegoziazione sicura (vedere la sezione **Errore! Origine di riferimento non trovata.** sezione .

NetX Secure TLS supporta completamente la rinegoziazione della sessione e l'estensione Secure Renegotiation Indication.

Quando si ricevono dati da un host remoto, le riattivazioni (e l'estensione) vengono gestite automaticamente senza l'interazione dell'applicazione. Se si desidera notificare le rinegoziazioni di sessione, è possibile che venga fornito un callback di rinegoziazione *con il nx_secure_tls_session_renegotiate_callback_set* servizio. Il callback verrà richiamato ogni volta che l'host remoto richiede una rinegoziazione, consentendo all'applicazione di intervenire se necessario.

Per avviare una rinegoziazione da una sessione TLS attiva, è sufficiente richiamare il *servizio* nx_secure_tls_session_renegotiate nella sessione TLS desiderata.

### <a name="tls-session-resumption"></a>Ripresa della sessione TLS

La ripresa della sessione TLS non deve essere confusa con la rinegoziazione della sessione, nonostante alcune analogie. Quando la *rinegoziazione* della sessione comporta l'avvio di  un nuovo handshake all'interno di una sessione TLS esistente, la ripresa della sessione è una funzionalità puramente facoltativa che comporta il riavvio di una sessione TLS chiusa senza eseguire un handshake TLS completo. A tale scopo, un'implementazione TLS può memorizzare nella cache i parametri e le chiavi della sessione, associandoli a un ID di *sessione,* un identificatore univoco fornito nell'handshake originale. Fornendo un ID sessione a un server TLS, un client indica che una sessione TLS precedente tra gli host esisteva e è stata completata in passato e che il client possiede ancora lo stato per ristabilire la sessione con un handshake ridotto. Poiché le chiavi di sessione sono teoricamente ancora segrete e note solo dai due host di comunicazione, il server può avviare una nuova sessione TLS e ignorare la maggior parte dell'handshake normale.

La ripresa della sessione può essere utile per evitare le operazioni di chiave pubblica potenzialmente costose usate per condividere il master secret di generazione della chiave e verificare le firme del certificato, ma richiede anche che i parametri della sessione, le chiavi e lo stato cripotgrafico siano mantenuti in memoria per tutte le sessioni possibili (almeno per un intervallo di tempo configurabile).

La versione corrente di NetX Secure TLS non supporta la ripresa della sessione. L'ID sessione viene semplicemente ignorato dai server TLS e i client TLS forniscono sempre un ID di sessione NULL che richiede al server di eseguire un handshake completo. La mancanza di ripresa della sessione non dovrebbe causare problemi di interoperazione perché si tratta di una funzionalità completamente facoltativa e tutte le implementazioni TLS devono usare per impostazione predefinita un handshake completo se l'ID sessione è NULL o non riconosciuto.

### <a name="protocol-layering"></a>Layering del protocollo

Il protocollo TLS si inserisce nello stack di rete tra il livello di trasporto (ad esempio TCP) e il livello dell'applicazione. TLS viene talvolta considerato un protocollo a livello di trasporto (da qui *Transport Layer* Security), ma poiché funge da applicazione per quanto riguarda i protocolli di rete sottostanti (ad esempio TCP), a volte viene raggruppato nel livello dell'applicazione.

TLS richiede un protocollo a livello di trasporto che supporta il recapito in ordine e senza perdita di dati, ad esempio TCP. A causa di questo requisito, TLS non può essere eseguito su UDP perché UDP non garantisce il recapito dei datagrammi. Un protocollo separato denominato *DTLS,* che è una versione modificata di TLS, viene usato per le applicazioni che necessitano della sicurezza di TLS su un protocollo di datagramma come UDP. NetX Secure supporta DTLS, ma la documentazione per DTLS è separata da questo documento.

![Diagramma dei livelli di protocollo TCP/IP e TLS.](media/image6.png)

Figura 5- Livelli del protocollo TCP/IP e TLS

## <a name="network-communications-security"></a>Sicurezza delle comunicazioni di rete

La protezione delle comunicazioni su reti pubbliche e Internet è un argomento di importanza critica e soggetto a un numero elevato di libri, articoli e soluzioni. L'argomento è estremamente complesso, ma può essere ridotto a un'idea semplice: l'invio di informazioni in rete in modo che solo la destinazione prevista possa accedere a queste informazioni o modificarle. Questo si suddivide in tre concetti importanti: segreto, integrità e autenticazione. Il protocollo TLS offre soluzioni per tutti e tre.

### <a name="secrecy"></a>Segreto

Quando si inviano dati in rete, è spesso importante che i dati non siano ottenuti da un'entità dannosa. Se i dati vengono inviati tramite una connessione TCP/IP, chiunque abbia accesso alla rete sarà in grado di leggere i dati usando strumenti di rete facilmente disponibili. Per impedire che i dati vengano ottenuti, devono essere codificati in modo che non siano leggibile se non dalla destinazione prevista. Si tratta *di una segretezza.* In TLS gli algoritmi di crittografia, ad esempio RSA e AES, forniscono la segretezza.

### <a name="integrity"></a>Integrità

In alcuni casi, la segretezza non è sufficiente per proteggere i dati in una rete. In alcuni casi, un'entità dannosa potrebbe modificare il contenuto di un pacchetto TCP senza dover conoscere il contenuto di tale pacchetto. I dati crittografati possono essere modificati, rendendo non valida la decrittografia o modificando i parametri del messaggio, ottenendo qualsiasi risultato che l'utente malintenzionato possa essere interessato a ottenere. Nella rete non è possibile impedire a un utente malintenzionato di modificare i dati in transito, ma è possibile fornire un meccanismo per sapere se i dati sono stati modificati. Quando i dati vengono modificati in transito, saranno noti e i dati possono essere rifiutati. Questo concetto è *l'integrità*. In TLS l'integrità viene fornita da una classe di routine di crittografia note come *funzioni hash.* Alcuni esempi di funzioni hash sono MD5 e SHA-1.

### <a name="authentication"></a>Authentication

Il terzo concetto importante della sicurezza delle comunicazioni di rete è l'idea che i dati debbano essere comunicati solo alla destinazione prevista. Un utente malintenzionato potrebbe tentare di rappresentare un'entità legittima per ricevere dati destinati a un altro host. Anche se i dati vengono inviati con meccanismi di segretezza e integrità, l'utente malintenzionato potrebbe comunque riuscire a ottenere il risultato desiderato (una compromissione delle comunicazioni sicure) attraverso questo processo. Per evitare questo problema, è necessario un meccanismo per dimostrare l'identità di un host remoto prima dell'invio di dati sensibili. Il processo di dimostrazione dell'identità di un host remoto è *l'autenticazione.* In TLS l'autenticazione viene fornita usando certificati digitali, funzioni hash e un meccanismo denominato firme digitali che usa una proprietà della crittografia a chiave pubblica (descritta di seguito).  Una forma di autenticazione limitata ma utile può essere fornita anche con *una chiave precondifazione* (PSK).

## <a name="tls-encryption"></a>Crittografia TLS

Il protocollo TLS è un framework per fornire comunicazioni di rete sicure su Internet che utilizzano la crittografia. La crittografia viene in genere definita come processo di codifica dei dati in modo che ottenere i dati originali (o le informazioni su tali dati) sia estremamente difficile senza una *chiave*. Nei sistemi informatici la crittografia si basa su calcoli matematici complessi come i campi finiti e può essere classificata in due *tipi:* chiave privata (o crittografia *simmetrica)* e chiave pubblica *(o* crittografia *asimmetrica).* Esempi di crittografia della chiave privata sono AES (Advanced Encryption Standard) e RC4 (Rivest Cipher 4). Esempi di crittografia a chiave pubblica sono rsa (Rivest, Shamir, Adleson) e Diffie-Hellman crittografia.

Il protocollo TLS usa routine di crittografia a chiave privata e a chiave pubblica per offrire un equilibrio tra prestazioni, sicurezza e flessibilità.

### <a name="private-key-encryption"></a>Private-Key crittografia

La crittografia a chiave privata è in uso da migliaia di anni. Le crittografie di sostituzione di base (in cui una lettera o una parola viene sostituita da un'altra lettera o parola non correlata) sono i primi esempi noti di crittografia, ma con l'avvento della crittografia della chiave privata in base all'età delle informazioni è stata notevolmente migliorata.

Una crittografia a chiave privata usa una "chiave" che è semplicemente un valore (che può essere una parola, una frase o un numero in generale) usato per codificare in qualche modo alcuni dati in modo che solo un'entità che aveva accesso a tale chiave possa decodificare i dati in modo significativo. La chiave viene usata sia per la crittografia che per la decrittografia dei dati, pertanto l'altro nome *è la crittografia simmetrica.*

Le crittografia a chiave privata sono in genere veloci e piuttosto semplici da implementare, anche se le operazioni matematiche coinvolte sono estremamente complesse. Per questo motivo, TLS usa la crittografia a chiave privata per la maggior parte delle comunicazioni sicure.

Tuttavia, la crittografia della chiave privata presenta un problema quando si tenta di applicarla alle comunicazioni di rete di computer generali: la chiave deve essere condivisa tra entrambi i computer che tentano di comunicare. In generale, è poco pratico e spesso impossibile comunicare una chiave privata in modo sicuro tra due computer su Internet, poiché si presuppone che il traffico di rete possa essere ottenuto da un numero qualsiasi di entità nei vari hop che i dati accettano quando vengono instradati attraverso Internet. Se la chiave viene ottenuta da un'entità dannosa, tutti i dati crittografati con tale chiave vengono compromessi. Poiché la maggior parte dei computer su Internet dispone solo di una connessione di rete e non di un altro canale sicuro per le comunicazioni, l'invio di chiavi in rete è in grado di inviare i dati non crittografati, senza alcuna sicurezza.

Per questo motivo, la crittografia della chiave privata non è sufficiente per implementare un protocollo di sicurezza per le comunicazioni di rete per utilizzo generico. Qui può essere utile la crittografia a chiave pubblica.

NetX Secure TLS supporta la crittografia a chiave privata AES.

### <a name="public-key-encryption"></a>Crittografia a chiave pubblica

A differenza della crittografia a chiave privata, la crittografia a chiave pubblica è un concetto piuttosto nuovo, sviluppato negli anni '70. Usando un concetto noto come "funzioni trap-door" in matematica, si è scoperto che esisteva un modo per condividere una chiave in rete senza compromettere la sicurezza dei dati crittografati.

Il funzionamento della crittografia *a* chiave pubblica è che la chiave (nel senso della  crittografia a chiave privata descritta in precedenza) è suddivisa in due parti, una chiave privata e una chiave pubblica, da cui la crittografia a chiave pubblica ottiene il nome. Il concetto è che una di queste chiavi (in genere la chiave pubblica) viene usata per la crittografia, mentre l'altra viene usata per la decrittografia. Questa asimmetria delle chiavi è il motivo dell'altro nome per la crittografia a chiave pubblica: crittografia *asimmetrica.*

La matematica alla base della crittografia a chiave pubblica è  piuttosto complessa, ma l'idea è che la chiave pubblica possa essere usata solo per la crittografia e ottenere tale chiave non consente di ottenere dati crittografati. La chiave privata, a sua volta, è l'unico modo per decrittografare i dati crittografati usando la chiave pubblica. Pertanto, mantenendo il segreto della chiave privata, chiunque voglia comunicare in modo sicuro con il proprietario di tale chiave privata deve solo crittografare i dati con la chiave pubblica corrispondente con la consapevolezza che solo un utente in possesso di tale chiave privata può ottenere i dati protetti.

NetX Secure TLS supporta la crittografia a chiave pubblica RSA.

> [!IMPORTANT] 
> *RSA è un'operazione a elevato utilizzo di processore se viene usata l'implementazione rsa del software. Le dimensioni maggiori delle chiavi aumentano la potenza di elaborazione richiesta da un fattore quadrato: 4X più lenta per un aumento 2X delle dimensioni della chiave.*

### <a name="public-key-authentication"></a>Public-Key autenticazione

Un effetto collaterale interessante del concetto di crittografia a chiave pubblica è che può essere usato per fornire  l'autenticazione e  la crittografia eseguendo l'operazione inversa: crittografia con la chiave privata e decrittografia con la chiave pubblica. Il meccanismo effettivo per eseguire questa operazione dipende dall'algoritmo a chiave pubblica in uso, ma il concetto è lo stesso.

Per eseguire l'autenticazione con l'autenticazione con chiave pubblica, il proprietario di una chiave privata crittografa alcuni dati (in genere un hash crittografico dei dati da autenticare) usando tale chiave privata. Quindi, un utente che vuole autenticare che i dati provenivano dal proprietario della chiave privata usa la chiave pubblica associata per decrittografare i dati. Se la decrittografia ha esito positivo e supponendo che l'utente abbia considerato attendibile la validità della chiave pubblica, l'utente può essere certo che i dati provenivano dal proprietario della chiave privata.

In TLS l'autenticazione con chiave pubblica viene usata per verificare la validità di un certificato digitale fornito da un server TLS (e, facoltativamente, dal client TLS) usando le chiavi pubbliche dell'archivio certificati attendibili. Il certificato viene verificato rispetto a una chiave pubblica nell'archivio e i dati nel certificato vengono usati per controllare l'identità del server.

NetX Secure TLS supporta l'autenticazione RSA.

### <a name="cryptographic-hashing"></a>Hash crittografico

La crittografia non è l'unica operazione di crittografia usata in TLS. Per garantire l'integrità del messaggio durante una sessione TLS, è necessario un checksum per assicurarsi che il contenuto del messaggio non sia stato manomesso. Tuttavia, un semplice checksum (come viene usato in TCP) non è sufficiente per garantire un livello di integrità accettabile perché può essere facilmente sovvertita da un utente malintenzionato esperto. Il meccanismo usato da TLS per fornire l'integrità dei messaggi è noto come *hash crittografico.*

La crittografia è una codifica 1:1, che consente di ottenere l'intera parte dei dati originali dai dati crittografati. Tuttavia, un hash esegue il mapping di una quantità arbitraria di dati in un valore di dimensione fissa, proprio come un checksum. A differenza di un semplice checksum, un hash è progettato specificamente per ridurre le *collisioni,* in cui dati di input diversi generano lo stesso output. In un semplice checksum, se un bit viene capovolto da 1 a 0 e un altro bit da 0 a 1, il checksum è lo stesso. Con un hash crittografico, l'output sarebbe notevolmente diverso, rendendo difficile per un utente malintenzionato modificare i dati con hash e fare in modo che l'operazione hash sui dati modificati abbia comunque lo stesso valore (verificando in modo falso l'integrità di questi dati).

TLS usa diversi algoritmi hash per garantire l'integrità dei messaggi, sia dei messaggi dell'applicazione che dei messaggi di controllo TLS. tra cui MD5, SHA-1 e SHA-256.

NetX Secure TLS supporta l'hash MD5, SHA-1 e SHA-256.

## <a name="tls-extensions"></a>Estensioni TLS

TLS offre una serie di estensioni che forniscono funzionalità aggiuntive per determinate applicazioni. Queste estensioni vengono in genere inviate come parte dei messaggi ClientHello o ServerHello, che indicano a un host remoto la voglia di usare un'estensione o fornire dettagli aggiuntivi per l'uso per stabilire la sessione TLS sicura.

In generale, le estensioni forniscono parametri facoltativi a TLS all'inizio dell'handshake che guidano le operazioni successive. Alcune estensioni richiedono l'input dell'applicazione o il processo decisionale, mentre altre vengono gestite automaticamente.

La tabella seguente descrive le estensioni TLS attualmente supportate da NetX Secure TLS:

| **Extension Name**              | **Descrizione**              |
| ------------------------------- |----------------------------- |
| Indicazione della rinegoziazione sicura | Questa estensione riduce una vulnerabilità di attacco man-in-the-middle che può verificarsi durante un handshake di rinegoziazione.|
| Indicazione nome server          | Questa estensione consente a un client TLS di fornire un nome DNS specifico a un server TLS, consentendo al server di selezionare le credenziali corrette (presuppone che il server abbia più certificati di identità e punti di ingresso di rete). |
| Algoritmi di firma            | Questa estensione consente a un client TLS di fornire un elenco di algoritmi di firma e hash accettabili a un server TLS. |

Panoramica delle estensioni TLS supportate

### <a name="secure-renegotiation-indication"></a>Indicazione della rinegoziazione sicura

TLS supporta la nozione di esecuzione di un handshake all'interno di una sessione TLS esistente, usando in tal modo la sessione stabilita per crittografare i messaggi di handshake. Questo processo consente di stabilire di nuovo le chiavi della sessione di crittografia senza terminare la sessione TLS (vedere la sezione "Rinegoziazione della sessione TLS").

Sfortunatamente, dopo che TLS usava la rinegoziazione per un certo periodo di tempo, si è scoperto che esisteva una vulnerabilità a un attacco Man-in-the-Middle che sfruttava la funzionalità di rinegoziazione. Per chiudere la vulnerabilità, è stata introdotta l'estensione Secure Renegotiation Indication. Essenzialmente, l'estensione di rinegoziazione sicura usa l'hash del messaggio Finished dalla connessione stabilita per verificare che gli host originali partecipano all'handshake di rinegoziazione. Essenzialmente, l'hash viene usato come token di verifica presupponendo che un utente malintenzionato non sia in grado di forgerlo (che richiederebbe l'accesso alle chiavi di sessione).

NetX Secure TLS gestisce automaticamente la rinegoziazione e usa l'estensione di rinegoziazione sicura per impostazione predefinita. Non è necessaria alcuna interazione con l'applicazione.

### <a name="server-name-indication"></a>Indicazione nome server

Durante l'handshake TLS, un client TLS prevede che un server remoto fornirà un certificato di identità in modo che il client possa autenticare il server. In alcuni casi, tuttavia, un server fornirà più servizi diversi con server "virtuali" diversi, ognuno con identità univoche. Nel caso di un singolo server con più identità, un client TLS può fornire un nome DNS specifico che verrà utilizzato dal server per selezionare le credenziali appropriate. Il meccanismo per specificare questo nome è l'estensione Indicazione nome server (SNI).

Per un'applicazione che usa l'estensione SNI, è necessaria un'interazione. Per i client TLS, l'applicazione deve fornire un nome DNS da inviare al server remoto. Per i server TLS, l'applicazione deve leggere il nome DNS dall'estensione e selezionare un certificato appropriato da inviare al client.

Le sezioni seguenti forniscono altri dettagli su come usare l'estensione SNI in NetX Secure TLS.

### <a name="sni-extension--tls-client"></a>Estensione SNI - Client TLS

Un client NETX Secure TLS che vuole usare l'estensione SNI deve fornire un nome DNS a TLS da fornire durante l'handshake. Questo nome deve essere inizializzato e fornito prima di avviare una sessione TLS perché l'estensione viene inviata nel messaggio ClientHello che avvia il processo di handshake.

Il frammento di codice seguente illustra l'uso dell'estensione . In primo luogo, NX_SECURE_X509_DNS_NAME'oggetto viene inizializzato con il nome del server desiderato. Quindi, prima di avviare la sessione TLS, il nome viene fornito a TLS usando l'API di estensione SNI. Dopo aver impostato il nome, non sono necessarie altre azioni. Vedere le informazioni di riferimento sulle API nel capitolo 4  
  
Descrizione di NetX Secure Services per altre informazioni sulle singole funzioni.

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
### <a name="sni-extension--tls-server"></a>Estensione SNI - Server TLS

Sul lato server TLS, l'estensione SNI può essere elaborata dall'applicazione per selezionare le credenziali appropriate (ad esempio il certificato) da fornire al client remoto durante l'handshake. A tale scopo, l'applicazione deve fornire un callback di sessione che viene richiamato dopo la ricezione di un messaggio ClientHello.

Il codice di esempio per l'API nx_secure_tls_session_server_callback_set (vedere la pagina 122) illustra l'analisi di un'estensione SNI in ingresso usando un callback del server. Essenzialmente, il server TLS riceve un clientHello e richiama il callback. L'applicazione usa quindi l'API *nx_secure_tls_session_sni_extension_parse* per analizzare i dati dell'estensione forniti al callback per trovare l'estensione SNI e restituire il nome DNS fornito (si noti che l'estensione supporta solo un singolo nome DNS). Dopo aver ottenuto il nome, l'applicazione lo usa per trovare e inviare il certificato di identità del server appropriato (e la catena di autorità di certificazione, se applicabile).

### <a name="signature-algorithms-extension"></a>Estensione algoritmi di firma

Questa estensione è specifica di TLS 1.2 e consente a un client TLS di fornire un elenco di coppie di firme e algoritmi hash accettabili per l'uso nella generazione e nella verifica delle firme digitali. L'elenco viene generato automaticamente da NetX Secure TLS per i client TLS usando la tabella di crittografia fornita *nx_secure_tls_session_create*. Non è necessaria alcuna interazione con l'applicazione.

## <a name="authentication-methods"></a>Authentication Methods

TLS fornisce il framework per stabilire una connessione sicura tra due dispositivi su una rete non sicura, ma parte del problema è conoscere l'identità del dispositivo sull'altra estremità della connessione. Senza un meccanismo per autenticare l'identità degli host remoti, diventa un'operazione semplice che un utente malintenzionato può rappresentare come un dispositivo attendibile.

Inizialmente, potrebbe sembrare che l'uso di indirizzi IP, indirizzi MAC hardware o DNS fornirebbe un livello di attendibilità relativamente elevato per l'identificazione degli host in una rete, ma data la natura della tecnologia TCP/IP e la facilità con cui gli indirizzi possono essere falsificati e le voci DNS danneggiate (ad esempio tramite un poisoning della cache DNS), è chiaro che TLS richiede un ulteriore livello di protezione dalle identità fraudolente.

Esistono diversi meccanismi che possono fornire questo ulteriore livello di autenticazione per TLS, ma il più comune è il *certificato digitale.* Altri meccanismi includono chiavi precondizioni (PSK) e schemi di password.

### <a name="digital-cerificates"></a>Cerificati digitali

I certificati digitali sono il metodo più comune per l'autenticazione di un host remoto in TLS. Essenzialmente, un certificato digitale è un documento con formattazione specifica che fornisce informazioni di identità per un dispositivo in una rete di computer.

TLS usa in genere un formato denominato X.509, uno standard sviluppato dall'International Telecommunication Union, anche se è possibile usare altri formati di certificati se gli host TLS possono accettare il formato usato. X.509 definisce un formato specifico per i certificati e varie codifiche che possono essere usate per produrre un documento digitale. La maggior parte dei certificati X.509 usati con TLS viene codificata usando una variante di ASN.1, un altro standard di telecomunicazioni. All'interno di ASN.1 sono disponibili diverse codifiche digitali, ma la codifica più comune per i certificati TLS è lo standard Distinguished Encoding Rules (DER). DER è un subset semplificato delle regole di codifica di base (BER) ASN.1 progettate per non ambiguità, semplificando l'analisi. In transito, i certificati TLS vengono in genere codificati in der binario e questo è il formato previsto da NetX Secure per i certificati X.509.

Anche se i certificati binari in formato DER vengono usati nel protocollo TLS effettivo, possono essere generati e archiviati in diverse codifiche, con estensioni di file come pem, crt e p12. Le diverse varianti vengono usate da applicazioni diverse di produttori diversi, ma in genere tutte possono essere convertite in DER usando strumenti ampiamente disponibili.

La codifica dei certificati alternativa più comune è PEM. Il formato PEM (da Privacy-Enhanced Mail) è una versione codificata in base 64 della codifica DER spesso usata perché la codifica comporta un testo stampabile che può essere facilmente inviato tramite posta elettronica o protocolli basati sul Web.

La generazione di un certificato per l'applicazione NetX Secure non rientra in genere nell'ambito di questo manuale, ma lo strumento da riga di comando OpenSSL ([www.openssl.org](http://www.openssl.org)) è ampiamente disponibile e può essere convertito tra la maggior parte dei formati.

A seconda dell'applicazione, è possibile generare certificati personalizzati, essere forniti da un produttore o un'organizzazione governativa o acquistare certificati da un'autorità di certificazione commerciale.

Per usare un certificato digitale nell'applicazione NetX Secure, è necessario innanzitutto convertire il certificato in un formato DER binario e, facoltativamente, convertire la chiave privata associata (l'esponente privato" per RSA, ad esempio) in un formato binario, in genere una chiave RSA con codifica PKCS#1 o UNA chiave ECC con codifica DER. Al termine della conversione, è necessario caricare il certificato e la chiave privata nel dispositivo. Le opzioni possibili includono l'uso di un file system basato su flash o la generazione di una matrice C dai dati (usando uno strumento come "xxd" da Linux) e la compilazione del certificato e della chiave nell'applicazione come dati costanti.

Dopo aver caricato il certificato nel dispositivo, è possibile usare l'API TLS per associare il certificato a una sessione TLS.

Per informazioni dettagliate ed esempi su come usare i certificati X.509 con NetX Secure TLS, vedere la sezione "Importazione di certificati X.509 in NetX Secure".

Per altre informazioni, vedere i servizi TLS seguenti nelle informazioni di riferimento sulle API:

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_add
- nx_secure_trusted_certificate_remove

### <a name="tls-client-certificate-specifics"></a>Specifiche del certificato client TLS

Le implementazioni client TLS in genere non richiedono il caricamento di un certificato "locale"<sup>14</sup> nel dispositivo. L'eccezione è quando è abilitata l'autenticazione del certificato client, ma questo è molto meno comune.

Un client TLS richiede il caricamento di almeno un certificato "attendibile"<sup>15</sup> (se necessario ne possono caricare altri) e lo spazio per l'allocazione di un certificato "remoto"<sup>16.</sup>

Per altre informazioni sull'aggiunta di certificati attendibili e sull'allocazione di spazio per i certificati remoti, vedere le informazioni di riferimento sulle API TLS per i servizi seguenti: nx_secure_tls_remote_certificate_allocate, nx_secure_tls_trusted_certificate_add.

14. Un certificato "locale" è un certificato che identifica il dispositivo locale, ovvero fornisce informazioni di identità per il dispositivo su cui viene caricata l'applicazione TLS.

15. Un certificato "attendibile" è un certificato che fornisce una base per l'attendibilità e l'autenticazione del dispositivo remoto, direttamente o tramite un'infrastruttura a chiave pubblica (PKI). La radice della catena di attendibilità è in genere denominata "autorità di certificazione" o certificato CA.

16. Un certificato "remoto" fa riferimento al certificato inviato dall'host remoto durante l'handshake TLS. Fornisce l'identità per l'host remoto e viene autenticato confrontandolo con un certificato "attendibile" nel dispositivo locale.

### <a name="tls-server-certificate-specifics"></a>Specifiche del certificato del server TLS

Le implementazioni del server TLS in genere non richiedono il caricamento di certificati "attendibili" nel dispositivo o certificati remoti da allocare. L'eccezione è che quando è abilitata l'autenticazione del certificato client (questa operazione è meno comune).

Un server TLS richiede il caricamento di un certificato "locale" in modo che il server possa fornirlo al client remoto durante l'handshake TLS per autenticare il server nel client.

Per altre informazioni sul caricamento di certificati locali da usare con le applicazioni server NETX TLS, vedere le informazioni di riferimento sulle API per i servizi seguenti: 
- nx_secure_tls_local_certificate_add, 
- nx_secure_tls_local_certificate_remove.

### <a name="pre-shared-keys-psk"></a>Chiavi precondicondite (PSK)

Un meccanismo alternativo per fornire l'autenticazione di identificazione in TLS è la nozione di chiavi precondicondite (PSK). L'uso di una crittografia PSK elimina la necessità di eseguire operazioni di crittografia a chiave pubblica a elevato utilizzo di processore, un elemento fondamentale per i dispositivi incorporati con vincoli di risorse. La chiave PSK sostituisce il certificato nell'handshake TLS e viene usata al posto del segreto pre-master crittografato per la generazione della chiave di sessione TLS.

Le ciphersuit PSK sono limitate nel senso che un segreto condiviso deve essere presente in entrambi i dispositivi prima di poter stabilire una sessione TLS. Ciò significa che i dispositivi devono essere stati caricati con tale segreto usando alcuni mezzi sicuri diversi da una connessione PSK TLS. I pacchetti PSK possono essere aggiornati tramite una connessione PSK TLS, ma il dispositivo deve necessariamente iniziare con una chiave PSK caricata tramite un altro meccanismo. Ad esempio, un dispositivo sensore e il relativo dispositivo gateway possono essere caricati con psk nella factory prima della spedizione oppure è possibile usare una connessione TLS standard (con un certificato) per caricare la chiave PSK.

Le ciphersuitE PSK sono in due forme, descritte in RFC 4279. La prima usa le chiavi RSA o Diffie-Hellman usate nello stesso modo delle chiavi pubbliche trasmesse nel certificato negli handshake TLS standard. La seconda forma, che è più usata in un ambiente con vincoli di risorse, usa una chiave PSK usata per generare direttamente le chiavi di sessione (ad esempio, per l'uso da parte di AES), evitando l'uso delle costose operazioni RSA o Diffie-Hellman.

NetX Secure supporta la seconda forma di crittografie PSK, consentendo alle applicazioni di rimuovere tutto il codice di crittografia a chiave pubblica e l'utilizzo della memoria. La chiave PSK non è una chiave AES, ma può essere considerata più simile a una password da cui vengono generate le chiavi effettive. Esistono poche restrizioni su ciò che può essere il valore PSK, anche se i valori più lunghi offrono una maggiore sicurezza (come con le password).

Per usare PSK con l'applicazione NetX Secure, è innanzitutto necessario definire la macro **globale NX_SECURE_ENABLE_PSK_CIPHERSUITES**. Questa operazione viene in genere eseguita tramite le impostazioni del compilatore, ma la definizione può essere inserita anche nel file di intestazione nx_secure_tls.h. Con la macro definita, il supporto della crittografia PSK verrà compilato nell'applicazione NetX Secure TLS.

Con il supporto PSK abilitato, è quindi possibile usare l'API TLS per configurare i pacchetti PSK per l'applicazione. Ogni chiave PSK richiederà un valore PSK (la "chiave" privata effettiva: mantenere questo valore sicuro), un valore "identity" usato per identificare la chiave PSK specifica e un "hint di identità" usato da un server TLS per scegliere un valore PSK specifico.

La chiave PSK stessa può essere qualsiasi valore binario perché non viene mai inviata tramite una connessione di rete. PSK può avere una lunghezza massima di 64 byte.

L'identità e l'hint devono essere stringhe di caratteri stampabili formattate con UTF-8. I valori identity e hint possono avere una lunghezza massima di 128 byte.

L'identità e PSK formano una coppia univoca che viene caricata in ogni dispositivo della rete che deve comunicare tra loro.

L'"hint" viene usato principalmente per definire profili di applicazione specifici per raggruppare i file PSK in base alla funzione o al servizio. Questi valori devono essere concordati in anticipo e dipendono dall'applicazione. Ad esempio, l'applicazione server della riga di comando OpenSSL (con PSK abilitato) usa la stringa predefinita "Client_identity", che deve essere fornita da un client TLS per continuare con l'handshake TLS.

Per altre informazioni su PSK, vedere le informazioni di riferimento sull'API NetX Secure per i servizi seguenti: nx_secure_tls_client_psk_set, nx_secure_tls_psk_add.

## <a name="importing-x509-certificates-into-netx-secure"></a>Importazione di certificati X.509 in NetX Secure

I certificati digitali sono necessari per la maggior parte delle connessioni TLS su Internet. I certificati forniscono un metodo per l'autenticazione di host precedentemente sconosciuti su Internet tramite l'uso di intermediari attendibili, in genere denominati autorità di certificazione *o* AUTORITÀ di certificazione. Per connettere il dispositivo NetX Secure a un servizio cloud commerciale (ad esempio Amazon Web Services), è necessario importare i certificati nell'applicazione caricandoli nel dispositivo.

Insieme ai certificati, a volte è necessaria anche una *chiave* privata associata al certificato. In alcune applicazioni ,ad esempio il client TLS quando l'autenticazione del certificato client non è in uso, il certificato sarà sufficiente, ma se il certificato viene usato per identificare il dispositivo, sarà necessaria una chiave privata. Le chiavi private vengono in genere generate quando si crea il certificato e vengono archiviate in un file separato, spesso crittografate con una password.

### <a name="certificate-types"></a>Tipi di certificato

I certificati digitali vengono in genere usati per identificare le entità in una rete, ma a seconda dell'applicazione avranno proprietà leggermente diverse.

### <a name="local-certificates"></a>Certificati locali

Ai fini di questa documentazione, si farà riferimento ai "certificati locali" come certificati che forniscono un'identità per il dispositivo locale (un altro nome possibile potrebbe essere "certificato del dispositivo"). Questi certificati verranno forniti a un host remoto quando l'host remoto desidera autenticare il dispositivo locale.

### <a name="remote-certificates"></a>Certificati remoti

In questa documentazione, "certificati remoti" si riferisce ai certificati forniti da un host remoto durante l'handshake TLS, se applicabile. Lo spazio per questi certificati deve essere allocato o NetX Secure non sarà in grado di analizzarli e completare l'handshake TLS.

### <a name="signing-certificates"></a>Firma dei certificati

Un "certificato di firma" viene usato per firmare digitalmente altri certificati o dati ai fini dell'autenticazione. Questi certificati possono essere certificati intermedi o radice all'interno di un'infrastruttura a chiave pubblica (PKI) e in genere non vengono usati per identificare singoli dispositivi o host.

### <a name="root-ca-certificates"></a>Certificati CA radice

I "certificati CA radice" sono certificati di firma che forniscono la base di un'infrastruttura a chiave pubblica e sono autofirmati, anziché essere firmati da un altro certificato di firma. Almeno un certificato CA radice è in genere necessario per la verifica dei server remoti da parte di un client TLS.

### <a name="certificate-formats"></a>Formati dei certificati

I certificati digitali sono semplicemente file contenenti dati strutturati codificati usando la sintassi ASN.1. Esistono tuttavia diversi formati in cui è possibile archiviare i certificati ed è importante avere il formato corretto prima di caricare un certificato in un'applicazione NetX Secure.

I formati più comuni per i certificati sono DER e PEM. DER *(per Distinguished Encoding Rules*, un formato ASN.1) è il formato binario usato da TLS durante l'esecuzione dell'handshake iniziale. PEM (da *Privacy Enhanced Mail*) è una versione con codifica Base 64 del formato DER adatta per l'invio tramite posta elettronica o tramite HTTP sul Web. Fornitori diversi usano estensioni di file diverse per i certificati, ad esempio ".pem" o ".crt" per i certificati PEM e ".der" per i certificati DER. Se si dispone di un certificato e non è chiaro il formato usato, l'apertura del file in un editor di testo consentirà di determinare il tipo poiché i file DER sono binari codificati e i file PEM sono normali testo ASCII che iniziano con l'intestazione "-----BEGIN CERTIFICATE-----".

NetX Secure richiede che il certificato sia in formato DER binario, quindi è necessario convertire il certificato in formato DER prima dell'importazione. Questa operazione può essere eseguita con strumenti immediatamente disponibili, ad esempio OpenSSL.

Se è necessaria una chiave privata per l'applicazione, il file di chiave verrà codificato usando PEM o DER in un formato specifico (PKCS#1 per RSA, RFC 5915 per ECC). Il file di chiave privata dovrà essere convertito in DER prima di essere importato.

I comandi OpenSSL seguenti sono disponibili come esempio per la conversione di certificati e file di chiave RSA nel formato DER richiesto da NetX Secure (ECC è simile, vedere la documentazione di OpenSSL).

```C
openssl x509 -inform PEM -in <certificate> -outform DER -out cert.der
openssl x509 -inform PEM -in <root CA cert> -outform DER -out CA_cert.der
openssl rsa -inform PEM -in <private key> -outform DER -out private.key
```
### <a name="private-keys-and-certificates"></a>Chiavi private e certificati

Per i certificati che identificano un dispositivo, la chiave privata associata deve essere caricata insieme al certificato. La chiave privata (che può essere per uno degli algoritmi a chiave pubblica, ad esempio RSA, Diffie-Hellman o crittografia Elliptic-Curve) viene usata da un server TLS per decrittografare il materiale della chiave in ingresso (il "pre-master secret") da un client TLS, autenticando così se stesso al client. Per un client TLS, se viene fornito un certificato di identità (un certificato con la chiave privata associata) e un server richiede un certificato client, la chiave privata viene usata per autenticare il client. Nel caso di RSA il client crittografa un token usando la chiave privata che il server decrittografa usando la chiave pubblica del client,  fornito nel certificato client (l'autenticazione Diffie-Hellman e ECC avviene in modo simile, ma i dettagli sono leggermente diversi).

In NetX secure  il nx_secure_x509_certificate_initialize del servizio viene usato per inizializzare un certificato X.509 (per altre informazioni, vedere la sezione "Caricamento di certificati nel dispositivo") e, facoltativamente, per associare una chiave privata a tale certificato.

Se viene fornita una chiave privata, il certificato viene contrassegnato come certificato di "identità" usato per identificare il dispositivo. La chiave viene passata come BLOB binario contiguo e una lunghezza, con un tipo di chiave associato. Il tipo di chiave dipende dal tipo di chiave (ad esempio RSA, ECC e così via) e dal formato (ad esempio PKCS#1 DER). Se non viene specificata alcuna chiave, il valore NX_SECURE_X509_KEY_TYPE_NONE (valore 0x0) può essere passato per indicare che non viene fornita alcuna chiave (una lunghezza pari a 0 e un puntatore NX_NULL per il parametro di dati avrà lo stesso effetto).

La tabella seguente illustra i tipi di chiave noti a NetX Secure e l'identificatore del tipo associato da passare *nx_secure_x509_certificate_initialize*. Altri tipi di chiave verranno aggiunti quando vengono aggiunti altri algoritmi di crittografia a NetX Secure.

| Identificatore                              | Algoritmo | Formato   | Codifica | Valore |
| --------------------------------------- | --------- | -------- | -------- | ----- |
| NX_SECURE_X509_KEY_TYPE_NONE            | Nessuno      | N/D      | N/D      | 0x0   |
| NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER   | RSA       | PKCS#1   | Der      | 0x1   |
| NX_SECURE_X509_KEY_TYPE_EC_DER          | Ecdsa     | RFC 5915 | Der      | 0x2   |

### <a name="user-defined-private-key-types"></a>Tipi di chiave privata definiti dall'utente

I valori degli identificatori del tipo di chiave per il *servizio nx_secure_x509_certificate_initialize* regolano le azioni eseguite quando viene fornita la chiave privata. Per i tipi noti, i valori sono nell'intervallo 0x0000 0000 – 0x0000 FFFF (ultimi 16 bit di un intero senza segno a 32 bit). Per le piattaforme con tipi di chiave personalizzati<sup>17</sup> (come nel caso di alcuni motori di crittografia basati su hardware), un tipo di chiave definito dall'utente nell'intervallo 0x0000 1000-0xFFFF FFFF (primi 16 bit diversi da zero) può essere passato come tipo di chiave. Se uno dei primi 16 bit del tipo di chiave è impostato, i dati della chiave privata vengono passati direttamente alla routine crittografica appropriata (ad esempio RSA) fornita nella tabella di crittografia TLS. I tipi di chiave definiti dall'utente non vengono analizzati o elaborati in altro modo prima di essere passati alla routine crittografica. Inoltre, il tipo di chiave definito dall'utente verrà passato anche alla routine crittografica in modo che qualsiasi elaborazione appropriata possa essere gestita a tale livello.

Si noti che i tipi di chiave definiti dall'utente vengono in genere usati per piattaforme hardware specifiche che utilizzano dati di chiave personalizzati (possibilmente crittografati). Ciò implica in genere che i dati chiave vengono generati o codificati usando un meccanismo specifico per tale fornitore di hardware (o nel caso di uno standard come PKCS#11, uno standard specifico). Per altre informazioni, vedere la documentazione della piattaforma hardware.

17. I tipi di chiave definiti dall'utente richiedono una routine crittografica personalizzata corrispondente per gestire il formato della chiave personalizzata. La routine crittografica deve avere un algoritmo corrispondente ,ad esempio RSA, e deve essere passata a TLS nella tabella ciphersuite. 

### <a name="loading-certificates-onto-your-device"></a>Caricamento di certificati nel dispositivo

Qualsiasi metodo per caricare un file nel dispositivo sarà sufficiente per importare i certificati.

Il metodo più semplice per caricare un certificato è convertire i dati binari con codifica DER in una matrice C e compilarli nell'applicazione come costante. Questa operazione può essere eseguita facilmente con strumenti come "xxd" in Linux (con l'opzione "-i").

In alternativa, è possibile caricare il certificato in un file system flash o in altre opzioni di archiviazione, purché sia possibile passare un puntatore ai dati del certificato nell'API NetX Secure.

### <a name="certificate-files-needed-for-netx-secure"></a>File di certificato necessari per NetX Secure

I file di certificato da importare dipendono dall'applicazione. In generale, i server TLS richiedono un certificato per identificare il dispositivo e i client TLS richiedono uno o più *certificati attendibili* per autenticare i server remoti. La tabella seguente illustra i certificati necessari per alcune applicazioni TLS diverse.

| **Funzionalità/opzioni TLS**                     | **Certificati/chiavi necessari (minimo)**              |
| ------------------------------------------------- | --------------------------------------------------- |
| TLS Client                                        | Certificato CA radice                                 |
| TLS Server                                        | Certificato locale, chiave privata per il certificato |
| Server TLS con autenticazione del certificato client | Certificato locale, chiave privata, CA radice             |
| Client TLS con autenticazione del certificato client | Certificato locale, chiave privata, CA radice             |
| Client o server TLS solo con chiavi precondidite    | Nessuno (PSK usato al posto dei certificati)             |

I servizi pertinenti per il caricamento dei certificati sono i seguenti:

| **Nome API**                                   | **Scopo**                                            |
| ---------------------------------------------- |------------------------------------------------------- |
| nx_secure_x509_certificate_initialize      | Deve essere chiamato perché tutti i certificati popolino la struttura NX_SECURE_X509_CERT con i dati del certificato e la chiave privata. |
| nx_secure_tls_local_certificate_add       | Aggiungere un certificato locale a una sessione TLS per identificare il dispositivo.                                                                |
| nx_secure_tls_local_certificate_remove    | Rimuovere un certificato locale da una sessione TLS.                                                                                   |
| nx_secure_tls_remote_certificate_allocate | Allocare spazio per un certificato remoto (chiamato con un NX_SECURE_X509_CERT).                                   |
| nx_secure_tls_trusted_certificate_add     | Aggiungere un certificato a una sessione TLS come certificato attendibile per l'autenticazione degli host remoti.                                     |
| nx_secure_tls_trusted_certificate_remove  | Rimuovere un certificato attendibile da una sessione TLS.                                                                                 |

### <a name="working-with-aws-iot-certificates"></a>Uso dei certificati IoT di AWS

Nell'Amazon Web Services IoT selezionare "Sicurezza" dal menu della barra laterale e selezionare "Certificati". Creare un nuovo certificato e seguire le istruzioni per scaricare il nuovo certificato del dispositivo.

Dopo aver scaricato i certificati, è necessario convertirli in formato DER usando OpenSSL o un'utilità simile.

NOTA: AWS fornirà anche un file di chiave pubblica. La chiave pubblica è contenuta nel certificato del dispositivo locale, quindi non deve essere importata nell'applicazione.

Ad esempio, di seguito sono riportati i comandi per convertire il certificato del dispositivo locale e la relativa chiave privata in formato DER per l'uso con NetX Secure:

```C
openssl x509 -inform PEM -in <certificate> -outform DER -out cert.der
openssl x509 -inform PEM -in <root CA cert> -outform DER -out CA_cert.der
openssl rsa -inform PEM -in <private key> -outform DER -out private.key
```
I file convertiti possono essere importati nell'applicazione seguendo le istruzioni precedenti.

## <a name="x509-certificate-validation-in-netx-secure"></a>Convalida del certificato X.509 in NetX Secure 

Quando si usa TLS con certificati X.509 per l'identificazione e la verifica dell'host, è importante comprendere come tali certificati vengono effettivamente convalidati. Anche se la specifica TLS non fornisce istruzioni dettagliate su come convalidare un certificato, fa riferimento alla specifica X.509 (RFC 5280). In generale, si prevede che TLS eseguirà almeno la convalida di base sui certificati in ingresso (i certificati forniti dall'host remoto durante l'handshake TLS) e NetX Secure TLS non è diverso.

### <a name="basic-x509-validation"></a>Convalida X.509 di base

Per qualsiasi certificato in ingresso, NetX Secure TLS eseguirà la convalida del percorso X.509 di base. Il processo comporta il controllo della firma digitale di ogni certificato rispetto al certificato dell'autorità di certificazione, che può essere fornito dall'host remoto o trovarsi nell'archivio certificati attendibili (vedere la sezione "Importazione di certificati X.509 in NetX Secure" per altre informazioni sull'importazione di certificati attendibili). Il processo di convalida viene ripetuto in modo ricorsivo nei certificati dell'autorità di certificazione fino a quando non viene raggiunto un certificato attendibile o la catena termina (con un certificato autofirmato o un certificato dell'autorità di certificazione mancante). Se viene raggiunto un certificato attendibile, il certificato viene verificato, in caso contrario viene rifiutato. Inoltre, in ogni fase del processo di verifica la data di scadenza di ogni certificato viene verificata rispetto all'ora fornita dalla funzione timestamp dell'applicazione (vedere il servizio "nx_secure_tls_session_time_function_set" per altre informazioni).

La specifica X.509 fornisce anche un algoritmo per supportare i "criteri", ovvero gli identificatori presenti in un'estensione X.509 che possono essere controllati durante la convalida del percorso. NetX Secure considera attualmente i certificati X.509 come se fosse definita l'opzione "anyPolicy", cio' tutti i criteri sono accettabili e il controllo dei criteri facoltativo non viene eseguito. L'implementazione di NetX Secure X.509 può essere aumentata con questa funzionalità in una versione futura. Per il momento, l'estensione dei criteri può essere ottenuta da un certificato usando l'API *nx_secure_x509_extension_find.*

Al termine della convalida del percorso di base, TLS richiama il callback di verifica del certificato fornito dall'applicazione usando l'API *nx_secure_tls_session_certificate_callback_set.* Se non viene fornito alcun callback, il certificato viene considerato attendibile dopo la convalida del percorso. Se viene fornito un callback, il callback eseguirà qualsiasi convalida aggiuntiva del certificato richiesto dall'applicazione. Il valore restituito dal callback viene usato per determinare se continuare con l'handshake TLS o interrompere l'handshake a causa di un errore di convalida.

Il callback viene richiamato con un puntatore alla sessione TLS pertinente e NX_SECURE_X509_CERT puntatore al certificato da convalidare. Tra la sessione TLS e il certificato, l'applicazione ha tutti i dati di cui ha bisogno da TLS per eseguire controlli di verifica aggiuntivi.

Per facilitare la convalida aggiuntiva, NetX Secure fornisce routine X.509 per alcune operazioni di convalida comuni, tra cui la convalida DNS e il controllo dell'elenco di revoche di certificati. Tutte queste routine sono adatte per l'uso all'interno del callback di verifica del certificato, ma possono anche essere usate per eseguire il controllo non in linea dei certificati X.509.

La tabella seguente riepiloga le funzioni helper disponibili per l'elaborazione dei certificati X.509. Le spiegazioni più dettagliate per le operazioni sono disponibili nelle sezioni seguenti e nelle informazioni di riferimento sulle API nel capitolo 4  
  
La descrizione di NetX Secure Services fornisce dettagli aggiuntivi sulle routine specifiche.

| **Nome API**                             | **Descrizione**                               |
| ---------------------------------------- | -------------------------------------- |
| nx_secure_x509_common_name_dns_check               | Verificare il nome comune del soggetto X.509 e SubjectAltName rispetto a un nome DNS previsto |
| nx_secure_x509_crl_revocation_check                 | Verificare la presenza di un certificato revocato in un elenco di revoche di certificati X.509 (CRL)       |
| nx_secure_x509_extended_key_usage_extension_parse | Analizzare e trovare un OID di utilizzo della chiave estesa specifico in un certificato                   |
| nx_secure_x509_key_usage_extension_parse           | Analizzare e restituire il campo di bit di utilizzo della chiave in un certificato                            |
| nx_secure_x509_extension_find                        | Trovare e restituire i dati ASN.1 con codifica DER non elaborati per un'estensione specifica.            |

Funzioni helper X.509 da usare nel callback di verifica del certificato

### <a name="x509-extensions"></a>Estensioni X.509

La specifica X.509 descrive una serie di "estensioni" che possono essere usate per fornire informazioni aggiuntive che possono essere utilizzate nella verifica dei certificati. Per la maggior parte, queste estensioni sono facoltative e non sono necessarie per la convalida sicura di un certificato digitale rispetto a un certificato radice attendibile. Tuttavia, NetX Secure supporta alcune estensioni di base. Il supporto per le estensioni aggiuntive può essere aggiunto nelle versioni future.

Le estensioni attualmente supportate sono elencate nella tabella seguente:

| Nome estensione           | Descrizione                                                                   | API pertinente                                             |
| ------------------------ | ----------------------------------------------------------------------------- | -------------------------------------------------------- |
| Utilizzo chiavi                | Fornisce utilizzi accettabili per la chiave pubblica di un certificato in un campo di bit         | nx_secure_x509_key_usage_extension_parse           |
| Utilizzo chiavi avanzato       | Fornisce altri usi accettabili per la chiave pubblica di un certificato tramite OID | nx_secure_x509_extended_key_usage_extension_parse |
| Nome alternativo soggetto | Fornisce nomi DNS alternativi rappresentati anche dal certificato   | nx_secure_x509_common_name_dns_check               |

### <a name="unsupported-x509-extensions"></a>Estensioni X.509 non supportate

L'implemenazione X.509 di NetX Secure offre anche un servizio per estrarre le *estensioni non* supportate: nx_secure_x509_extension_find . Questa API è destinata agli utenti avanzati perché richiede la conoscenza di ASN.1 con codifica DER per analizzare i dati restituiti. Viene usato internamente per estrarre le estensioni supportate, ma viene fornito per praticità nello sviluppo di supporto personalizzato per le estensioni X.509.

Per usare nx_secure_x509_extension_find, viene passato un NX_SECURE_X509_EXTENSION insieme al certificato e a un ID estensione, ovvero una rappresentazione integer della stringa OID a lunghezza variabile per un tipo di estensione noto. Un elenco completo degli OID supportati per le estensioni X.509 è disponibile nelle informazioni di riferimento sulle API nx_secure_x509_extension_find a pagina 178.

La NX_SECURE_X509_EXTENSION struttura è definita come segue:

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
Quando il servizio viene restituito correttamente, la struttura verrà popolata con i dati rilevanti del certificato. Il nx_secure_x509_extension_id campo viene in genere usato per scopi interni, ma verrà popolato con la rappresentazione OID integer pertinente. Il nx_secure_x509_extension_critical campo espone il valore del flag di estensione critico X.509 (booleano). I nx_secure_x509_extension_data e nx_secure_x509_extension_data_length contengono rispettivamente un puntatore ai dati ASN.1 con codifica DER per l'estensione e alla lunghezza di questi dati.

L'analisi effettiva dei dati ASN.1 dell'estensione non è nell'ambito di questo documento, ma se si ha accesso all'origine NetX Secure TLS è possibile vedere come viene eseguita l'analisi ovunque nx_secure_x509_extension_find sia chiamato per le estensioni supportate.

### <a name="x509-dns-validation"></a>Convalida DNS X.509

Un'operazione di convalida del certificato comune in TLS comporta il controllo del nome di dominio Top-Level (TLD) di un host remoto rispetto al certificato X.509 fornito da tale host durante l'handshake TLS. Questa operazione consente di garantire che il certificato corrisponda effettivamente al server host che lo ha fornito, presupponendo che la ricerca DNS possa essere attendibile. In NetX Secure TLS questa funzionalità viene fornita dal servizio **nx_secure_x509_common_name_dns_check**, che accetta il certificato e una stringa contenente la parte TLD dell'URL usata per accedere all'host. Il valore TLD viene confrontato con il campo Nome comune del certificato e, se corrisponde, NX_SUCCESS restituito. Se il nome comune non corrisponde, la routine verifica anche l'esistenza dell'estensione del certificato X.509 *subjectAltName*. Se è presente un subjectAltName, tutte le voci DNSName nell'estensione vengono controllate anche in base al valore TLD fornito. Anche in questo caso, in caso di corrispondenza, NX_SUCCESS restituito. Se non viene trovata alcuna corrispondenza, viene restituito un errore adatto per la restituzione dal callback di convalida del certificato.

### <a name="x509-key-usage-and-extended-key-usage-extensions"></a>X.509 Key Usage ed Extended Key Usage Extensions

Le estensioni X.509 Key Usage e Extended Key Usage forniscono informazioni su come usare la chiave pubblica di un certificato durante l'autenticazione del certificato. L'utilizzo della chiave viene fornito dall'autorità emittente del certificato quando il certificato viene firmato ed emesso. L'utilizzo della chiave può essere usato da un host TLS per verificare che il certificato sia autorizzato a essere usato per autenticare un host TLS remoto ed eseguire altre operazioni.

L'estensione Utilizzo chiavi è costituita da un semplice campo di bit in cui ognuno dei bit rappresenta un utilizzo specifico della chiave. Un elenco completo di questi valori è disponibile nelle informazioni di riferimento sulle API *nx_secure_x509_key_usage_extension_parse* a pagina 183. Per una descrizione più completa dei bit di utilizzo delle chiavi e dei relativi significati, vedere RFC 5280, sezione 4.2.1.3.

L'estensione Utilizzo chiavi esteso, come l'estensione Utilizzo chiavi, fornisce informazioni accettabili sull'utilizzo delle chiavi. Tuttavia, per supportare gli utilizzi arbitrari, l'estensione Utilizzo chiavi esteso usa gli OID anziché un campo di bit. Quando si analizza un'estensione utilizzo chiavi esteso in NetX Secure X.509, un intero che rappresenta l'OID viene fornito dall'applicazione. Il servizio *nx_secure_x509_extended_key_usage_extension_parse* restituirà quindi se tale OID è presente. Un elenco completo degli OID supportati per l'utilizzo della chiave estesa è disponibile nelle informazioni di *riferimento* sulle API nx_secure_x509_extended_key_usage_extension_parse a pagina 175. Per una descrizione più completa degli OID e dei relativi significati, vedere RFC 5280, sezione 4.2.1.12.

### <a name="x509-crl-revocation-status-checking"></a>Controllo dello stato di revoca CRL X.509

X.509 fornisce un meccanismo denominato Elenco di *revoche* di certificati (CRL) che consente a un'autorità di firma del certificato digitale di revocare la validità dei certificati firmati. Qualsiasi applicazione che deve verificare i certificati da un'autorità di firma può ottenere un CRL e confrontare tutti i certificati firmati da tale autorità (autorità emittente) con il CRL per verificare se il proprio stato è stato revocato per qualche motivo (ad esempio, una chiave privata compromessa). In questo modo, l'applicazione può evitare l'uso di certificati potenzialmente pericolosi che superano altri controlli di convalida dei certificati.

L'ottenimento di un CRL viene eseguito da un'applicazione scaricando l'elenco con codifica DER da un server predefinito o tramite altri mezzi. La configurazione effettiva varia da autorità di certificazione a autorità di certificazione, quindi NetX Secure non fornisce un meccanismo per ottenere CRL, ma fornisce una routine per controllare un certificato rispetto a un CRL, **nx_secure_x509_crl_revocation_check**.

L'API accetta un CRL con codifica DER, un archivio certificati (ad esempio quello in una sessione TLS) da verificare e il certificato da controllare. La routine convalida innanzitutto il CRL stesso rispetto all'archivio attendibile (parte dell'archivio certificati fornito dall'applicazione). Questo è importante per proteggere da CRL fraudolenti usati per attacchi Denial of Service e stabilisce che il CRL è effettivamente dell'autorità di emittente appropriata. Dopo la convalida CRL, viene verificata l'autorità di certificazione: se l'autorità emittente del CRL non corrisponde all'autorità emittente del certificato, il CRL non è valido per tale certificato e viene restituito un errore. L'applicazione deve determinare se l'handshake TLS può continuare a questo punto. Se le autorità di certificazione corrispondono, nell'elenco CRL viene cercato il numero di serie del certificato da convalidare. Se il numero di serie è presente nell'elenco, viene restituito un errore che indica che il certificato è stato revocato. Se non viene trovata alcuna corrispondenza, NX_SUCCESS restituito.

## <a name="client-certificate-authentication-in-netx-secure-tls"></a>Autenticazione del certificato client in NetX Secure TLS

Quando si usa l'autenticazione del certificato X.509, il protocollo TLS richiede che l'istanza del server TLS fornisa un certificato per l'identificazione, ma per impostazione predefinita l'istanza del client TLS non deve fornire un certificato per l'autenticazione, usando invece un'altra forma di autenticazione (ad esempio, una combinazione di nome utente/password). Corrisponde all'uso più comune di TLS in Internet per i siti Web. Ad esempio, un sito di vendita online deve dimostrare a un potenziale cliente che usa un Web browser che il server è legittimo, ma l'utente userà un account di accesso/password per accedere a un account specifico.

Tuttavia, il caso predefinito non è sempre auspicabile, quindi TLS consente facoltativamente all'istanza del server TLS di richiedere un certificato dal client remoto. Quando questa funzionalità è abilitata, il server TLS invierà un messaggio CertificateRequest al client TLS durante l'handshake. Il client deve rispondere con un proprio certificato e un messaggio CertificateVerify che contiene un token di crittografia che dimostra che il client è proprietario della chiave privata corrispondente associata al certificato. Se la verifica non riesce o il certificato non è connesso a un certificato attendibile nel server, l'handshake TLS non riesce.

Esistono due casi distinti per l'autenticazione del certificato client in TLS: le sezioni seguenti illustrano entrambi i casi.

### <a name="client-certificate-authentication-for-tls-clients"></a>Autenticazione del certificato client per i client TLS

Un client TLS può tentare una connessione a un server che richiede un certificato per l'autenticazione client. In questo caso, il client deve fornire un certificato al server e verificare che sia proprietario della chiave privata corrispondente, in caso il server terminerà l'handshake TLS.

In NetX Secure TLS non è disponibile alcuna configurazione speciale per *supportare* questa funzionalità, ma l'applicazione dovrà fornire un certificato di identificazione locale per l'istanza del client TLS usando il nx_secure_tls_local_certificate_add servizio. Se l'applicazione non specifica alcun certificato ma il server remoto usa l'autenticazione del certificato client e richiede un certificato, l'handshake TLS avrà esito negativo. Il certificato fornito alla sessione TLS *con nx_secure_tls_local_certificate_add* deve essere riconosciuto dal server remoto per completare l'handshake TLS.

### <a name="client-certificate-authentication-for-tls-servers"></a>Autenticazione del certificato client per i server TLS

Il caso del server TLS per l'autenticazione del certificato client è leggermente più complesso del caso del client TLS perché la funzionalità è facoltativa. In questo caso, il server TLS deve richiedere in modo specifico un certificato al client TLS remoto, quindi elaborare il messaggio CertificateVerify per verificare che il client remoto sia proprietario della chiave privata corrispondente e quindi il server deve verificare che il certificato fornito dal client possa essere tracciato in un certificato nell'archivio certificati attendibili locale.

Nelle istanze del server NETX Secure TLS l'autenticazione del certificato client è controllata da <br>
la *verifica del client <span class="underline"> _</span> <span class="underline">_</span><span class="underline"> _</span> di <span class="underline">_</span><span class="underline"> _</span> sessione <span class="underline">_</span>TLS* sicuro nx abilita e<br>
*nx <span class="underline"> _</span> secure tls <span class="underline">_</span><span class="underline"> _</span> session <span class="underline">_</span>client verify <span class="underline"> _</span> disable <span class="underline">_</span>* services.

Per abilitare l'autenticazione del certificato client, un'applicazione deve chiamare<br>
*Verificare <span class="underline"> _</span> l'abilitazione <span class="underline">_</span><span class="underline"> _</span> del <span class="underline">_</span>client <span class="underline"> _</span> <span class="underline">_</span>* di sessione TLS sicuro nx con l'istanza di sessione del server TLS prima di *nx_secure_tls_session_start*. Si noti che la chiamata di questo servizio in una sessione TLS usata per le connessioni client TLS non avrà alcun effetto.

Quando l'autenticazione del certificato client è abilitata, il server TLS richiederà un certificato dal client TLS remoto durante l'handshake TLS. Nel server NETX Secure TLS il certificato client viene controllato rispetto all'archivio dei certificati attendibili creati con *nx <span class="underline"> _</span> secure_tls <span class="underline">_</span>trusted <span class="underline"> _</span> certificate <span class="underline">_</span>add* dopo la catena di autorità di certificazione X.509. Il client remoto deve fornire una catena che connette il certificato di identità a un certificato nell'archivio attendibile, in caso di esito negativo dell'handshake TLS. Inoltre, se l'elaborazione del messaggio CertificateVerify non riesce, anche l'handshake TLS avrà esito negativo.

I metodi di firma usati per il metodo CertificateVerify sono corretti per TLS versione 1.0 e TLS versione 1.1 e sono specificati dal server TLS nella versione 1.2 di TLS. Per TLS 1.2, i metodi di firma supportati seguono in genere i metodi pertinenti forniti nella tabella dei metodi di crittografia, ma in genere RSA con SHA-256 (vedere la sezione "Crittografia in NetX Secure TLS" per altre informazioni sull'inizializzazione di TLS con metodi di crittografia).

## <a name="cryptography-in-netx-secure-tls"></a>Crittografia in NetX Secure TLS

TLS definisce un protocollo in cui la crittografia può essere usata per proteggere le comunicazioni di rete. Di conseguenza, lascia aperta la crittografia effettiva per gli utenti TLS. La specifica richiede solo l'implementazione di un singolo ciphersuite: nel caso di TLS 1.2, il ciphersuite è TLS_RSA_WITH_AES_128_CBC_SHA, che indica l'uso di RSA per le operazioni a chiave pubblica, AES in modalità CBC con chiavi a 128 bit per la crittografia della sessione e SHA-1 per gli hash di autenticazione dei messaggi.

Essendo conforme a TLS 1.2, NetX Secure abilita la crittografia TLS_RSA_WITH_AES_128_CBC_SHA obbligatoria per impostazione predefinita, ma considerando il numero di implementazioni possibili per ognuno dei metodi di crittografia a causa delle funzionalità hardware e di altre considerazioni, NetX Secure fornisce un'API di crittografia generica che consente a un utente di specificare quali metodi di crittografia usare con TLS.

NOTA: il meccanismo dell'API di crittografia generica consente anche agli utenti di implementare i propri pacchetti di crittografia, ma è consigliato per gli utenti avanzati che hanno familiarità con le estensioni e le crittografie TLS. Se si è interessati a supportare i propri ciphersuit, contattare il rappresentante di Express Logic.

### <a name="cryptographic-methods"></a>Metodi di crittografia

NetX Secure TLS implementa DES, 3DES, AES, MD5, HMAC-MD5, SHA-1, HMAC-SHA1, SHA-256, HMAC-SHA256, RSA ed ECC (curve selezionate) nel software con driver hardware per determinate piattaforme hardware. Un'applicazione può usare le routine crittografiche fornite con NetX Secure oppure routine personalizzate fornite dall'utente finale o da terze parti.

Il *NX_CRYPTO_METHOD* è un blocco di controllo progettato per un'applicazione per descrivere una particolare implementazione di un algoritmo di crittografia da usare con NetX Secure TLS. Con *l'NX_CRYPTO_METHOD, un'applicazione* può integrare facilmente la propria implementazione di crittografia in NetX Secure. La *NX_CRYPTO_METHOD* viene dichiarata come:

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

Di seguito è riportata la descrizione di ogni *elemento nella NX_CRYPTO_METHOD* struttura :

- nx_crypto_algorithm: questo campo identifica l'algoritmo  descritto nel metodo della variabile Alcuni valori validi per NetX Secure TLS sono i seguenti (vedere nx_crypto_const.h per valori specifici):
    
  - NX_CRYPTO_NONE    
  - NX_CRYPTO_ENCRYPTION_NULL    
  - NX_CRYPTO_ENCRYPTION_AES_CBC    
  - NX_CRYPTO_AUTHENTICATION_NONE    
  - TLS_HASH_SHA_1    
  - TLS_HASH_SHA_256    
  - TLS_HASH_MD5    
  - TLS_CIPHER_RSA    
  - TLS_CIPHER_NULL

- nx_crypto_key_size_in_bits: questo campo specifica le dimensioni della chiave privata usata dal metodo .

- nx_crypto_IV_size_in_bits: questo campo specifica le dimensioni del vettore di inizializzazione (IV). Si noti che nella maggior parte dei casi il blocco IV viene usato solo per gli algoritmi di crittografia/decrittografia. Gli algoritmi di autenticazione e verifica usano raramente questo campo.

- nx_crypto_ICV_size_in_bits: questo campo specifica le dimensioni del blocco di controllo dell'integrità (ICV). NOTA: questo blocco è per l'utilizzo di IPsec e non viene usato in TLS. Per altre informazioni, vedere NetX Duo IPsec.

- nx_crypto_block_size_in_bytes: questo campo specifica le dimensioni in byte del blocco dell'algoritmo di crittografia per le crittografie basate su blocchi. Nella maggior parte dei casi viene usato dalle routine di crittografia e raramente dalle routine di autenticazione.

- nx_crypto_metadata_area_size: questo campo specifica le dimensioni dell'area dei metadati richiesta da questo metodo. Ogni implementazione può richiedere una certa memoria per archiviare le informazioni sullo stato o per archiviare dati intermedi (ad esempio materiale di trasformazione chiave) o da usare come area scratch. La quantità di spazio richiesta da un'implementazione viene specificata in questo campo. L'applicazione fornisce lo spazio di memoria durante la creazione di una sessione TLS. La funzione di crittografia è responsabile della gestione di questa area dei metadati.

- nx_crypto_init: funzione di inizializzazione per l'algoritmo di crittografia. Per un'implementazione che non richiede una routine di inizializzazione, questo campo può essere impostato su NX_NULL. Un uso tipico di una funzione di inizializzazione è l'inizializzazione della struttura dei dati interna per l'algoritmo. NetX Secure TLS gestirà l'inizializzazione della routine crittografica chiamando internamente questa funzione.

Il prototipo per la funzione di inizializzazione è:

```C
UINT crypto_init_function(NX_CRYPTO_METHOD *method, 
                          UCHAR *key, 
                          UINT  key_size_in_bits, 
                          VOID  **handle, 
                          VOID  *crypto_metadata_area, 
                          ULONG crypto_metadata_area_size);
```

  - method è un puntatore al blocco di controllo del metodo di crittografia.

  - key è la stringa della chiave privata per l'elaborazione dei pacchetti di dati.

  - key_size_in_bits definisce la dimensione della chiave privata, in bit.

  - handle è un elemento definito dall'implementazione che identifica una particolare sessione di crittografia. Il valore viene generato dalla routine di inizializzazione e viene passato di nuovo al chiamante. L'operazione di crittografia successiva o la routine di pulizia usano questo handle per identificare la sessione.

  - crypto_metadata è un puntatore all'area dei metadati richiesta dall'implementazione di questo algoritmo. Per gli algoritmi che non necessitano di un'area dei metadati, questo campo è impostato su NX_NULL e la routine di inizializzazione non deve accedere all'area dei metadati.

  - crypto_metadata_size specifica le dimensioni dell'area dei metadati. Per le APPLICAZIONI create senza area dei metadati, questo campo è impostato su zero e la routine di inizializzazione non deve accedere all'area dei metadati.

  - Questa routine *restituirà* NX_SUCCESS se il processo di inizializzazione ha esito positivo. Il chiamante considera qualsiasi altro valore restituito come errore.

- nx_crypto_cleanup: routine di pulizia definita per l'implementazione di un algoritmo di crittografia. Viene richiamato quando una sessione TLS viene eliminata o riavviata.

Il prototipo per la funzione cleanup è:

```C
UINT crypto_cleanup_function(VOID *handle);
```
- L'handle viene passato alla funzione di pulizia dal chiamante. L'handle viene inizializzato dalla routine di inizializzazione della crittografia e usato per identificare lo stato dell'algoritmo di crittografia.

- Questa routine *restituirà* NX_SUCCESS se il processo di pulizia ha esito positivo. Il chiamante considera qualsiasi altro valore restituito come errore.

- nx_crypto_operation: routine che esegue i servizi di crittografia, decrittografia e autenticazione effettivi. Il prototipo di funzione della routine dell'operazione è:

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

- op indica il tipo di operazione che questa routine deve eseguire. I valori validi sono:
    
    - NX_CRYPTO_ENCRYPT
    - NX_CRYPTO_DECRYPT
    - NX_CRYPTO_AUTHENTICATE
    - NX_CRYPTO_VERIFY

- L'handle viene passato alla funzione dell'operazione dal chiamante. Viene generato dalla routine di inizializzazione della crittografia.
- il metodo punta al blocco di controllo del metodo crypto
- punta alla chiave privata usata per questa operazione
- key_size_in_bits è la dimensione della chiave privata in bit
- input è un puntatore all'inizio del messaggio su cui operare.
- input_length_in_byte viene passato dal chiamante per indicare le dimensioni del messaggio su cui operare.
- iv_ptr viene impostata dal chiamante in modo che punti all'inizio di un blocco di inizializzazione. Si noti che la memoria per il blocco di inizializzazione viene fornita dal chiamante. Per la crittografia, la funzione dell'operazione deve scrivere le informazioni sul vettore di inizializzazione in questo blocco di memoria. per la decrittografia, la funzione dell'operazione deve recuperare le informazioni sul vettore di inizializzazione da questo blocco di memoria. Gli algoritmi per l'autenticazione e l'operazione di verifica in genere non usano il vettore di inizializzazione.
- output viene impostata dal chiamante in modo che punti a un buffer di output. Si noti che la memoria per il buffer di output viene fornita dal chiamante. Per la crittografia, la funzione dell'operazione deve scrivere il testo crittografato nel buffer di output. per la decrittografia, l'operazione deve scrivere il testo decifrato (testo non crittografato) nel buffer di output; per l'autenticazione, il valore hash deve essere scritto nel buffer di output. Per la verifica, il buffer di output viene usato per archiviare le informazioni hash.
- output_length_in_byte indica le dimensioni del buffer di output
- crypto_metadata punta all'area dei metadati che deve essere usata da questa operazione di crittografia. L'area dei metadati di crittografia viene in genere inizializzata da crypto_init_function.
- crypto_metadata_size indica le dimensioni dell'area dei metadati.
- Questa routine *restituirà* NX_SUCCESS se il processo dell'operazione ha esito positivo. Il chiamante considera qualsiasi altro valore restituito come errore.
- packet_ptr: pacchetto che contiene i dati elaborati. NOTA: questo parametro non viene usato da TLS e deve essere impostato su NX_NULL.
- nx_crypto_hw_process_callback: funzione di callback fornita dal metodo di crittografia. Viene usato se la funzione di crittografia viene fornita dall'hardware e richiede una routine di callback.

NetX Secure TLS offre i metodi di crittografia seguenti:

- *AES*  
- *RSA*  
- *NULL*

NetX Secure TLS offre i metodi di autenticazione seguenti:

- *HMAC-MD5*  
- *HMAC-SHA1*  
- *HMAC-SHA256*

Gli esempi seguenti illustrano come configurare la *NX_CRYPTO_METHOD* per usare i metodi di crittografia e autenticazione forniti da NetX Duo IPsec.

***Aes:***

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

Un metodo speciale **NX_CRYPTO_NONE** usato per segnalare al modulo IPsec che la crittografia o il servizio di autenticazione non è necessario. Viene configurato come segue:

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
### <a name="initializing-tls-with-cryptographic-methods"></a>Inizializzazione di TLS con metodi di crittografia

Dopo aver creato le routine crittografiche conformi alle firme del metodo di crittografia descritte nella sezione precedente, è necessario passarle in TLS quando si inizializza un blocco di controllo NX_SECURE_TLS_SESSION di crittografia. Questa operazione viene eseguita nel servizio TLS nx_secure_tls_session_create:

```C
UINT  nx_secure_tls_session_create(
              NX_SECURE_TLS_SESSION*     session_ptr,
              const NX_SECURE_TLS_CRYPTO*    tls_cipher_table,
              VOID*                encryption_metadata_area,
              ULONG                 encryption_metadata_size
);
```
- session_pointer è un puntatore al blocco NX_SECURE_TLS_SESSION di controllo.
- tls_cipher_table è un puntatore a un blocco NX_SECURE_TLS_CRYPTO di controllo, descritto di seguito.
- encryption_metadata_area punta allo spazio usato dalle routine crittografiche in TLS.
- encryption_metadata_size è la dimensione in byte dell'area dei metadati.

### <a name="elliptic-curve-cryptography-ecc-in-netx-secure-tls"></a>Crittografia a curva ellittica (ECC) in NetX Secure TLS

Elliptic Curve Cryptography (ECC) fornisce uno schema di crittografia a chiave pubblica che può essere usato al posto di RSA. ECC è in genere più veloce e usa chiavi più piccole rispetto a RSA, quindi può essere un'opzione utile per TLS incorporato. Nelle versioni X-Ware precedenti Azure RTOS 6.0, ECC è stato fornito come componente aggiuntivo, richiedendo l'installazione del codice sorgente ECC nel progetto. Azure RTOS ECC integrato 6.0 nella codebase della riga principale, quindi l'installazione dei file ECC non è più necessaria. Ecc, tuttavia, richiede comunque la stessa inizializzazione delle versioni precedenti.

### <a name="supported-ecc-curves"></a>Curve ECC supportate

NetX Secure implementa parti delle curve in base a <http://www.secg.org/sec2-v2.pdf> . Le curve difollowing sono<sup>supportate 18:</sup>

  - secp256r1 
  - secp384r1 
  - secp521r1 

Se vengono usate altre curve ECC, la routine *nx_secure_tls_session_start()* restituirà l'errore NX_SECURE_TLS_NO_SUPPORTED_CIPHERS che indica che sono state usate curve non supportate.

Si noti che la catena di certificati TLS può essere crittografata anche dagli algoritmi ECC. Anche se le curve fornite dal client TLS sono supportate, è possibile che la curva ECC usata nella catena di certificati non sia supportata. In questo caso, *nx_secure_tls_session_start* routine restituisce NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER.

In nx_crypto_generic_ciphersuites.c è disponibile un esempio di tabella di crittografia predefinita per ECC. Per altre informazioni sulle tabelle di crittografia, vedere la sezione "Tabella di crittografia TLS".

18. Si noti che le implementazioni per le curve secp192r1 e secp224r1 sono fornite anche per le applicazioni legacy. Tuttavia, queste curve sono ora considerate deboli e NON DEVONO essere usate per lo sviluppo di nuove applicazioni.

### <a name="crypto-methods-for-ecc"></a>Metodi di crittografia per ECC

Metodi di crittografia per i gruppi di curve ellittiche:

- NX_CRYPTO_METHOD crypto_method_ec_secp192<sup>15</sup>;  
- NX_CRYPTO_METHOD crypto_method_ec_secp224<sup>15</sup>;  
- NX_CRYPTO_METHOD crypto_method_ec_secp256;  
- NX_CRYPTO_METHOD crypto_method_ec_secp384;  
- NX_CRYPTO_METHOD crypto_method_ec_secp521;

I metodi di crittografia per le curve ECC sono definiti in nx_crypto_generic_ciphersuites.c.

Metodo di crittografia per ECDHE:

- NX_CRYPTO_METHOD crypto_method_ecdhe;

Metodo di crittografia per ECDSA:

- NX_CRYPTO_METHOD crypto_method_ecdsa;

I metodi di crittografia ECDSA e ECDHE sono definiti in nx_crypto_generic_ciphersuites.c.

Insieme ad altri metodi di crittografia, ad esempio RSA, SHA, AES, possono essere usati come blocchi predefiniti per la tabella di ricerca ciphersuite.

### <a name="enabling-ecc-support-for-tls"></a>Abilitazione del supporto ECC per TLS

ECC è abilitato per impostazione predefinita per TLS. Per disabilitare il supporto ECC, è necessario NX_SECURE_DISABLE_ECC_CIPHERSUITE il simbolo.

Per fare in modo che la modifica sia effettiva, è necessario ricompilare netx secure library e tutte le applicazioni che usano tale libreria.

Nel codice dell'applicazione l'API n *x_secure_tls_ecc_initialize()* deve essere chiamata dopo la creazione della sessione TLS. Questa API notifica alla sessione TLS il tipo di curve da usare per le operazioni di scambio delle chiavi TLS e la verifica dei certificati. Durante la fase di handshake TLS, se viene selezionato un algoritmo ECC, il client e il server scambiano i parametri relativi alla curva ECC per decidere quale curva usare.

Il segmento di codice seguente illustra come usare l'API. Si noti che gli argomenti (*nx_crypto_ecc_supported_groups, nx_crypto_ecc_supported_groups_size e nx_crypto_ecc_curves)* sono tutti definiti in *nx_crypto_generic_ciphersuites.c*. Questi simboli possono quindi essere usati direttamente.

```C
status = nx_secure_tls_ecc_initialize(&tls_session,     
                    nx_crypto_ecc_supported_groups,      
                    nx_crypto_ecc_supported_groups_size,     
                    nx_crypto_ecc_curves);
```
La configurazione di esempio in nx_crypto_generic_ciphersuites.c contiene una tabella di ricerca di crittografia ECC usata quando ECC è abilitato. Per usare ECC, è sufficiente passare nx_crypto_tls_ciphers_ecc come parametro di tabella ciphersuite durante la creazione di sessioni TLS con nx_secure_tls_session_create. La tabella di esempio contiene sia ciphersuit ECC che non ECC.

### <a name="tls-cryptographic-cipher-table"></a>Tabella di crittografia TLS

La NX_SECURE_TLS_CRYPTO struttura è definita come:

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
La tabella viene creata compilando le voci per questa struttura in una costante statica che si trova all'interno del progetto NetX Secure TLS, che in genere si trova con le routine e i moduli crittografici.

Ad esempio, la libreria crittografica solo software ("generica") fornita con NetX Secure contiene la definizione di tabella seguente (per il supporto di crittografie non ECC<sup>19):</sup>

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
Nella struttura la prima voce è la tabella tls ciphersuite. La NX_SECURE_TLS_CIPHERSUITE_INFO esegue il mapping delle routine crittografiche (sotto forma di puntatori NX_CRYPTO_METHOD) a specifiche crittografie, come definito nelle specifiche TLS. Il secondo valore è il numero di voci nella tabella a cui punta il primo campo.

Il campo successivo punta a una tabella di routine usate da X.509 durante l'elaborazione di certificati digitali e la struttura NX_SECURE_X509_CRYPTO è simile nel formato a NX_SECURE_TLS_CIPHERSUITE_INFO. Il campo seguente è il numero di voci nella tabella .

Nella tabella di ricerca sono riportate alcune routine necessarie per versioni specifiche di TLS. Ad esempio, prima di TLS versione 1.2, le routine di generazione della chiave e hashing dell'handshake erano fisse per usare una combinazione di SHA-1 e MD5. I metodi per queste routine sono definiti in modo specifico nella struttura di crittografia perché non sono collegati a specifici ciphersuit. In TLS versione 1.2 le routine di generazione e hash delle chiavi vengono scelte dal ciphersuite, ma per i ciphersuit che non specificano le routine da usare, viene usato il metodo hash SHA-256 e la struttura di crittografia chiama in modo specifico tale routine.

TLS 1.3 richiede alcune operazioni di crittografia aggiuntive specifiche.

19. Si noti che il supporto di TLS 1.3 richiede ECC: usare nx_crypto_tls_ciphers_ecc se TLS 1.3 è abilitato.

### <a name="tls-ciphersuite-lookup-table"></a>Tabella di ricerca ciphersuite TLS

Per compilare la tabella di crittografia per TLS, è anche necessario creare una tabella di ricerca ciphersuite che esegue il mapping delle routine crittografiche a identificatori di crittografia specifici. Gli identificatori sono valori registrati con IANA universali. Per altre informazioni, vedere RFC TLS. Le routine rappresentano i 5 metodi separati usati in ogni ciphersuite (alcuni ciphersuit potrebbero non usare tutti e 5): crittografia pubblica, autenticazione a chiave pubblica, crittografia di sessione, routine hash di sessione e funzione Pseudo-Random TLS (PRF). La tabella seguente illustra ognuno dei 5 metodi:

| **Categoria routine**      | **Descrizione**                                                                                       | **Algoritmi di esempio**                                            |
| ------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Crittografia pubblica             | Usato per scambiare chiavi durante l'handshake TLS                                                        | RSA, Diffie-Hellman, ECC                                          |
| Autenticazione con chiave pubblica | Usato per autenticare o firmare i dati durante l'handshake TLS                                            | RSA, DSS                                                          |
| Crittografia di sessione            | Algoritmo a chiave simmetrica usato per crittografare i dati dell'applicazione durante la sessione TLS                       | AES, RC4                                                          |
| Hash di sessione              | Usato per mantenere l'integrità dei messaggi durante la sessione TLS (assicura che i dati non sono stati modificati) | SHA-1, SHA-256                                                    |
| TLS PRF                   | Usato per generare il materiale della chiave e nell'hash dell'handshake nell'handshake TLS                          | La funzione PRF si basa su routine hash: SHA-1 + MD5, SHA-256, SHA-512 |

La NX_SECURE_TLS_CIPHERSUITE_INFO è definita come segue:

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
Il nx_secure_tls_ciphersuite contiene il valore di crittografia IANA e i puntatori NX_CRYPTO_METHOD rappresentano i 5 metodi usati da tale crittografia. I valori scalari (nx_secure_tls_iv_size, nx_secure_tls_key_size e nx_secure_tls_hash_size) sono in informazioni, fornendo informazioni che potrebbero non essere disponibili nelle NX_CRYPTO_METHOD seguenti.

Verrà ad esempio illustrata la crittografia predefinita per TLS, TLS_RSA_WITH_AES_128_CBC_SHA, che specifica l'uso di RSA, AES-CBC con chiavi a 128 bit e SHA-1 per l'hashing della sessione. Non viene specificato alcun PRF TLS per questo ciphersuite, quindi in modalità TLSv1.2 verrà utilizzata la PRF SHA-256 predefinita. Si noti che in TLS 1.0 e 1.1 tutti i protocolli di crittografia usano il PRF SHA-1+MD5, indipendentemente dal PRF specificato nella tabella.

La voce nella tabella NX_SECURE_TLS_CIPHERSUITE_INFO nella libreria di crittografia generica è definita come segue:

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

Si noti che per la crittografia di sessione la dimensione della chiave è determinata dal ciphersuite, ma per i metodi a chiave pubblica la dimensione della chiave non è nota fino a quando non è in corso l'handshake TLS perché le chiavi pubbliche sono contenute nei certificati digitali s scambiati durante l'handshake.

### <a name="x509-cipher-lookup-table"></a>Tabella di ricerca crittografata X.509

Analogamente alla NX_SECURE_TLS_CIPHERSUITE_INFO, la struttura NX_SECURE_X509_CRYPTO esegue il mapping delle routine crittografiche a valori noti. Nel caso di X.509, gli identificatori sono effettivamente OID definiti da X.509 e registrati con gli standard ISO e ITU. Gli OID sono valori multi byte a lunghezza variabile progettati per identificare in modo univoco varie informazioni in vari standard di telecomunicazione, incluse le routine crittografiche usate nei certificati digitali. A causa del fatto che gli OID sono a lunghezza variabile, NetX Secure TLS esegue il mapping dei valori OID ufficiali alle costanti a lunghezza fissa usate internamente (vedere nx_secure_x509.h). Queste costanti vengono usate nella NX_SECURE_X509_CRYPTO, definita come segue:

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

Il primo campo, *nx_secure_x509_crypto_identifier*, è la rappresentazione OID interna usata da NetX Secure.

Il secondo e il terzo campo puntano NX_CRYPTO_METHOD oggetti che rappresentano i metodi di crittografia identificati dall'OID, un'operazione di chiave pubblica associata a una routine hash. Si noti che ogni certificato digitale può avere più di un OID per le routine crittografiche.

La tabella dei metodi per X.509 viene costruita nello stesso modo della tabella di ricerca ciphersuite. Ad esempio, si analerà l'OID per RSA_SHA1. L'OID effettivo per RSA_SHA1 è il seguente:

```C
{iso(1) member-body(2) us(840) rsadsi(113549) pkcs(1) pkcs-1(1) sha1-with-rsa-
signature(5)}
```
L'OID è rappresentato nella sintassi ASN.1 e ha un valore numerico di 1.2.840.113549.1.1.5. Questo valore viene quindi codificato in formato binario, creando i byte seguenti:

```C
UCHAR RSA_SHA1_OID = { 0x2A, 0x86, 0x48, 0x86, 0xF7, 0x0D, 0x01, 0x01, 0x05 };
```
La conversione effettiva da ASN.1 al formato binario ese supera l'ambito di questo documento. Per altre informazioni, cercare codifiche ASN.1 per gli OID. La rappresentazione binaria degli OID supportati da NetX Secure è disponibile nel file *nx_secure_x509.c*.

Dopo aver creato un mapping dell'OID effettivo a una costante riconosciuta internamente, è possibile creare una voce per RSA_SHA1 nella NX_SECURE_X509_CRYPTO seguente:

```C
{ 
    NX_SECURE_TLS_X509_TYPE_RSA_SHA_1,    /* Internal OID constant. */
    &crypto_method_rsa,                   /* RSA method (NX_CRYPTO_METHOD). */ 
    &crypto_method_sha1                   /* SHA-1 method (NX_CRYPTO_METHOD). */
}, 
```
### <a name="default-tls-routines"></a>Routine TLS predefinite

Come accennato in precedenza, TLS richiede alcune routine predefinite per la generazione di chiavi e la verifica dei messaggi durante l'handshake. La routine principale è la funzione Pseudo-Random TLS o PRF. La funzione PRF è basata su routine hash e può essere usata per generare una quantità arbitraria di dati pseudocasa casuali<sup>20</sup> per la generazione di chiavi o per altri scopi.

Oltre al PRF, ogni versione di TLS usa routine hash predefinite che devono essere fornite. Per le versioni 1.0 e 1.1 di TLS, tali routine hash sono MD5 e SHA-1. TLS versione 1.2 richiede solo SHA-256.

Nella struttura NX_SECURE_TLS_CRYPTO sono presenti puntatori NX_CRYPTO_METHOD per MD5, SHA-1, SHA-256, la PRF TLS versione 1.0/1.1 e la PRF TLS 1.2 predefinita.

Il supporto di TLS 1.3 aggiunge campi per HKDF (generazione di chiavi), HMAC (per operazioni di hashing specifiche usate durante l'handshake) e ECDHE (obbligatorio per la funzionalità TLS 1.3).

Nella libreria di crittografia software generica sono disponibili versioni software della PRF TLS. Per TLS 1.0/1.1, questa funzione viene chiamata *nx_crypto_tls_prf_1*. Per TLS 1.2, la funzione viene chiamata *nx_secure_tls_prf_sha256*. Il suffisso "1" rappresenta la PRF TLS 1.0 legacy e il suffisso "sha256" fa riferimento al fatto che la PRF predefinita di TLS 1.2 è basata su SHA-256. Quando è necessario il supporto per altre routine PRF, il suffisso per tali routine rifletterà il metodo hash usato. Poiché le routine PRF sono basate su metodi hash, le routine hash sottostanti possono essere accelerate dall'hardware in modo indipendente su piattaforme di destinazione diverse.

Oltre alle tabelle di ricerca TLS ciphersuite e X.509, con le routine PRF e hash predefinite compilate nella struttura NX_SECURE_TLS_CRYPTO possono essere popolate e usate per inizializzare una sessione TLS.

20. "Pseudo-casuale" si riferisce al fatto che la funzione PRF è deterministica, ovvero produrrà sempre lo stesso output in base allo stesso input, ma casuale nel fatto che l'output non è prevedibile. TLS usa questa proprietà del PRF per generare le chiavi di sessione da vari dati pubblici combinati con il master secret scambiato durante l'handshake usando una crittografia a chiave pubblica come RSA.

### <a name="cryptographic-metadata"></a>Metadati crittografici

Prima di poter inizializzare la sessione TLS con la tabella NX_SECURE_TLS_CRYPTO, è necessario allocare spazio nel buffer per i metadati della routine crittografica. I metadati vengono usati per archiviare tutto lo stato associato a una particolare routine, rappresentata dal relativo blocco di controllo. Il *campo nx_crypto_metadata_area_size* di ogni NX_CRYPTO_METHOD deve essere impostato sulle dimensioni della struttura di controllo associata a tale routine. In caso contrario, l'inizializzazione TLS non sarà in grado di gestire correttamente lo spazio necessario, causando possibili problemi di sovraccarico del buffer.

Prima di creare la sessione TLS, è necessario allocare il buffer dei metadati. Il buffer viene diviso automaticamente per nx_secure_tls_session_create e lo spazio è riservato per ognuna delle routine fornite nella tabella del metodo di crittografia. Si noti che poiché in una sessione TLS è attivo un solo ciphersuite alla volta, il numero di ciphersuit supportati non influisce sul necessario spazio dei metadati. Lo spazio è riservato per ognuna delle 5 routine ciphersuite che usano la dimensione massima del blocco di controllo per tale categoria nella tabella di ricerca ciphersuite.

Per semplificare il calcolo delle dimensioni del  buffer dei metadati, il nx_secure_metadata_size_calculate del servizio esegue gli stessi calcoli di nx_secure_tls_session_create ma restituisce semplicemente la dimensione totale richiesta del buffer dei metadati in byte.

### <a name="initializing-the-tls-session"></a>Inizializzazione della sessione TLS

Dopo aver creato gli NX_CRYPTO_METHOD e NX_SECURE_TLS_CRYPTO e aver riservato l'area dei metadati, è possibile inizializzare una sessione TLS come indicato di seguito (valori degli esempi precedenti):

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
