---
title: Capitolo 3 - Descrizione funzionale Azure RTOS DTLS sicuro di NetX
description: Questo capitolo contiene una descrizione funzionale Azure RTOS DTLS sicuro di NetX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7db319e45c6d1f4a2030734fc01fefc4f3907aebeec1b3f47a5bde57dd5bfcc4
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797091"
---
# <a name="chapter-3-functional-description-of-azure-rtos-netx-secure-dtls"></a>Capitolo 3: Descrizione funzionale Azure RTOS DTLS sicuri di NetX

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Questo capitolo contiene una descrizione funzionale Azure RTOS DTLS sicuro di NetX. Esistono due tipi principali di esecuzione del programma in un'applicazione NetX Secure DTLS: inizializzazione e chiamate all'interfaccia dell'applicazione. 

NetX Secure presuppone l'esistenza di ThreadX e NetX/NetXDuo. ThreadX richiede l'esecuzione del thread, la sospensione, i timer periodici e le funzionalità di esclusione reciproca. Da NetX/NetXDuo sono necessari i driver e le funzionalità di rete UDP e IP.

## <a name="datagram-transport-layer-security-dtls-and-transport-layer-security-tls"></a>Datagram Transport Layer Security (DTLS) e Transport Layer Security (TLS)

NetX Secure DTLS implementa il protocollo Datagram Transport Layer Security versione 1.2 definito in RFC 6347. DTLS versione 1.0 è stato definito in RFC 4347 e corrispondeva a TLS versione 1.1. Poiché DTLS è essenzialmente un'estensione a TLS, si è deciso che la versione successiva userebbe lo stesso numero di versione della versione di TLS corrispondente. Pertanto, non esiste alcuna versione DTLS 1.1 perché DTLS versione 1.2 corrisponde a TLS versione 1.2.

> [!NOTE]
> NetX Secure supporta DTLS versione 1.2. DTLS 1.0 (RFC 4347) **non è** attualmente supportato.

*Secure Sockets Layer* (SSL) era il nome originale di TLS prima che diventasse uno standard in RFC 2246 e "SSL" viene spesso usato come nome generico per i protocolli TLS. L'ultima versione di SSL era 3.0 e TLS 1.0 viene talvolta definito SSL versione 3.1. Tutte le versioni del protocollo "SSL" ufficiale sono considerate obsolete e non sicure e attualmente NetX Secure non fornisce un'implementazione SSL.

TLS specifica un protocollo  per generare le chiavi di sessione create durante *l'handshake* TLS tra un client TLS e un server e tali chiavi vengono usate per crittografare i dati inviati dall'applicazione durante la sessione *TLS.*

DTLS è strettamente associato a TLS, in quanto i mechansim di sicurezza sottostanti vengono condivisi tra i protocolli. TLS, tuttavia, è progettato per funzionare su un protocollo del livello di trasporto che fornisce garanzie sul recapito e sull'ordine dei pacchetti (quasi sempre TCP in pratica) e non funzionerà su un protocollo non affidabile come UDP. Proprio a causa di UDP è stato introdotto DTLS: DTLS è stato progettato per gestire la natura inaffidabile di UDP e protocolli simili. A tale scopo, include la logica di ordinamento e affidabilità (ad esempio la ritrasmissione dei dati eliminati) simile ai protocolli affidabili come TCP.

Una descrizione completa di TLS è inclusa nel capitolo 3 della Guida dell'utente di NetX Secure TLS, quindi questo documento si concentrerà sulle differenze tra TLS e DTLS.

### <a name="dtls-record-header"></a>Intestazione del record DTLS

Qualsiasi record DTLS valido deve avere un'intestazione DTLS, come illustrato nella figura 1. L'intestazione è la stessa di TLS con l'aggiunta di due nuovi campi: *l'era* a 16 bit e il numero di sequenza a 48 *bit*, descritto di seguito.

![Diagramma di un'intestazione di record DTLS.](media/image2.png)

**Figura 1 - Intestazione del record DTLS**

I campi dell'intestazione del record TLS sono definiti come segue:

| Campo di intestazione TLS | Scopo  |
| ---------------- | --------- |
| **Tipo di messaggio a 8 bit** | Questo campo contiene il tipo di record DTLS inviato. I tipi validi sono i seguenti:<br />- ChangeCipherSpec: 0x14<br />- Avviso: 0x15<br />- Handshake: 0x16<br />- Dati dell'applicazione: 0x17<br /> |
| **Versione del protocollo a 16 bit** | Questo campo contiene la versione del protocollo DTLS. I valori validi sono i seguenti:<br />- DTLS 1.1: 0xFEFD |
|  **Epoch a 16 bit** |  Questo campo contiene il valore DTLS "epoch", ovvero un contatore che viene incrementato ogni volta che viene modificato lo stato della crittografia, ad esempio quando si generano nuove chiavi di sessione.  |
|  **Numero di sequenza a 48 bit** |  Questo campo contiene un numero di sequenza che identifica questo record specifico. Viene usato da DTLS per mantenere l'ordinamento dei record e verificare la necessità di ritrasmissione. |
|  **Lunghezza a 16 bit** |  Questo campo contiene la lunghezza dei dati incapsulati nel record DTLS.  |

### <a name="dtls-handshake-record-header"></a>Intestazione record handshake DTLS

Qualsiasi record di handshake DTLS valido deve avere un'intestazione handshake DTLS, come illustrato nella figura 2.

![Diagramma di un'intestazione di record handshake DTLS.](media/image3.png)

**Figura 2 - Intestazione del record handshake DTLS**

I campi dell'intestazione del record handshake DTLS sono definiti come segue:

| Campo di intestazione TLS | Scopo  |
| ---------------- | ------------------------------------------------ |
| **Tipo di messaggio a 8 bit** | Questo campo contiene il tipo di record DTLS inviato. I tipi validi sono i seguenti:<br />- ChangeCipherSpec: 0x14<br />- Avviso: 0x15<br />- Handshake: 0x16<br />- Dati dell'applicazione: 0x17 |
|  **Epoch a 16 bit** | Questo campo contiene il valore DTLS "epoch", ovvero un contatore che viene incrementato ogni volta che viene modificato lo stato della crittografia, ad esempio quando si generano nuove chiavi di sessione. |
|  **Numero di sequenza a 48 bit** | Questo campo contiene un numero di sequenza che identifica questo record specifico. Viene usato da DTLS per mantenere l'ordinamento dei record e verificare la necessità di ritrasmissione. |
|  **Versione del protocollo a 16 bit** | Questo campo contiene la versione del protocollo DTLS. I valori validi sono i seguenti:<br />- DTLS 1.1: 0xFEFD |
| **Lunghezza a 16 bit** | Questo campo contiene la lunghezza dei dati incapsulati nel record DTLS. |
| **Tipo di handshake a 8 bit** | Questo campo contiene il tipo di messaggio handshake. I valori validi sono i seguenti:<br />- HelloRequest: 0x00<br />- ClientHello: 0x01<br />- ServerHello: 0x02<br />- Certificato: 0x0B<br />- ServerKeyExchange: 0x0C<br />- CertificateRequest: 0x0D<br />- ServerHelloDone: 0x0E<br />- CertificateVerify: 0x0F<br />- ClientKeyExchange: 0x10<br />- Completato: 0x14 |
| **Lunghezza a 24 bit** | Questo campo contiene la lunghezza dei dati del messaggio di handshake. |
| **Numero di sequenza a 16 bit** | Questo campo contiene un numero di sequenza. |

### <a name="the-dtls-handshake-and-dtls-session"></a>Handshake e sessione DTLS DTLS

Un tipico handshake DTLS è illustrato nella figura 3. È quasi identico all'handshake TLS tipico con una differenza importante: quando il messaggio ClientHello viene inviato per la prima volta, il server risponde con un nuovo messaggio specifico di DTLS, *HelloVerifyRequest,* che contiene un "cookie". Il client DTLS deve rispondere con un secondo messaggio ClientHello contenente il cookie prima che l'handshake possa procedere. Questo meccanismo è stato aggiunto a DTLS per impedire determinati attacchi Denial of Service (DoS) poiché UDP è un protocollo senza connessione (TCP richiede una connessione/porta dedicata, quindi TLS non è avariato dallo stesso problema).

Un handshake DTLS inizia quando il client invia un messaggio *ClientHello* a un server DTLS, indicando il suo desiderio di avviare una sessione DTLS. Il messaggio contiene informazioni sulla crittografia che il client vuole usare per la sessione, insieme alle informazioni usate per generare le chiavi di sessione in un secondo momento nell'handshake. Fino a quando non vengono generate le chiavi di sessione, tutti i messaggi nell'handshake DTLS non vengono crittografati. Come accennato in precedenza, il server DTLS può inviare un helloVerifyRequest in risposta a ClientHello, forzando il client a rispondere con un secondo ClientHello aggiornato.

Alla ricezione del secondo messaggio ClientHello, il server DTLS verificherà il cookie e, se corretto, risponderà con un messaggio ServerHello che indica una selezione tra le opzioni di crittografia fornite dal client. ServerHello è seguito da un messaggio di certificato, in cui il server fornisce un certificato digitale per autenticare la propria identità al client (se viene usata la verifica X.509). Infine, il server invia un messaggio ServerHelloDone per indicare che non sono presenti altri messaggi da inviare. Il server può facoltativamente inviare altri messaggi dopo ServerHello e in alcuni casi potrebbe non inviare un messaggio di certificato (ad esempio quando vengono usate chiavi precondivie), quindi la necessità del messaggio ServerHelloDone.

Dopo che il client ha ricevuto tutti i messaggi del server, ha informazioni sufficienti per generare le chiavi di sessione. TLS/DTLS esegue questa operazione creando un bit condiviso di dati casuali denominato *segreto pre-master*, che è di dimensioni fisse e viene usato come valore di seed per generare tutte le chiavi necessarie dopo l'allocazione della crittografia. Il segreto pre-master viene crittografato usando l'algoritmo a chiave pubblica (ad esempio RSA) specificato nei messaggi Hello (vedere di seguito per informazioni sugli algoritmi a chiave pubblica) e la chiave pubblica fornita dal server nel certificato. Una funzionalità TLS/DTLS facoltativa denominata Chiavi precondi condivise (PSK) abilita i ciphersuit che non usano un certificato ma usano invece un valore segreto condiviso tra gli host (in genere tramite trasferimento fisico o un altro metodo protetto). Quando PSK è abilitata, la chiave privata precondicondita viene usata per generare il segreto pre-master. Vedere la sezione chiavi precondicondite in "Metodi di autenticazione" più avanti.

In un handshake TLS/DTLS consueto, il segreto pre-master crittografato viene inviato al server nel messaggio ClientKeyExchange. Il server, alla ricezione del messaggio ClientKeyExchange, decrittografa il segreto pre-master usando la relativa chiave privata e procede alla generazione delle chiavi di sessione in parallelo con il client TLS/DTLS.

Dopo la generazione delle chiavi di sessione, tutti gli altri messaggi possono essere crittografati usando l'algoritmo a chiave privata (ad esempio AES) selezionato nei messaggi Hello. Un messaggio non crittografato finale denominato ChangeCipherSpec viene inviato sia dal client che dal server per indicare che tutti gli altri messaggi verranno crittografati.

Il primo messaggio crittografato inviato sia dal client che dal server è anche il messaggio di handshake TLS finale, denominato Finished. Questo messaggio contiene un hash di tutti i messaggi di handshake ricevuti e inviati. Questo hash viene usato per verificare che nessuno dei messaggi nell'handshake sia stato manomesso o danneggiato (che indica una possibile violazione della sicurezza).

Dopo la ricezione dei messaggi Finished e la verifica degli hash di handshake, viene avviata la sessione TLS/DTLS e l'applicazione inizia a inviare e ricevere dati. Per tutti i dati inviati da entrambi i lati durante la sessione TLS/DTLS viene prima eseguito l'hashing usando l'algoritmo hash scelto nei messaggi Hello (per garantire l'integrità del messaggio) e crittografato usando l'algoritmo a chiave privata scelto con le chiavi di sessione generate.

Infine, una sessione TLS/DTLS può essere terminata correttamente solo se il client o il server sceglie di eseguire questa operazione. Una sessione troncata viene considerata una violazione della sicurezza (poiché un utente malintenzionato potrebbe tentare di impedire la ricezione di tutti i dati inviati) quindi viene inviata una notifica speciale quando uno dei due lati vuole terminare la sessione, denominato avviso CloseNotify. Sia il client che il server devono inviare ed elaborare un avviso CloseNotify per un arresto corretto della sessione.

![Diagramma di una tipica sessione di handshake DTLS.](media/image4.png)

**Figura 3- Tipico handshake DTLS**

### <a name="initialization"></a>Inizializzazione

Lo stack NetX o NetXDuo deve essere inizializzato prima di usare NetX Secure DTLS. Per informazioni su come inizializzare correttamente lo stack TCP/IP per l'operazione UDP, vedere il Manuale dell'utente di NetX o NetXDuo.

Dopo l'inizializzazione di NetX UDP, È possibile usare DTLS. Internamente, tutto il traffico di rete e l'elaborazione DTLS vengono gestiti dallo stack NetX/NetXDuo senza richiedere l'intervento dell'utente. Tuttavia, DTLS presenta alcuni requisiti specifici che devono essere gestiti separatamente dallo stack di rete sottostante. L'operazione del client DTLS questi parametri vengono assegnati al blocco di controllo DTLS denominato ***NX_SECURE_DTLS_SESSION** _. Per il funzionamento del server DTLS, il blocco di controllo è denominato _ *_NX_SECURE_DTLS_SERVER_** e contiene l'infrastruttura necessaria per gestire più sessioni DTLS su una singola porta UDP. Si noti che questo è diverso da TLS, in cui ogni sessione TLS è associata a una singola porta TCP.

Le due modalità DTLS, Server e Client, possono essere abilitate in un'applicazione (ma solo una modalità per ogni socket NetX) e ognuna ha requisiti specifici, come descritto di seguito.

### <a name="initialization--dtls-server"></a>Inizializzazione - Server DTLS

La modalità NetX Secure DTLS Server differisce dalla modalità server TLS a causa dell'uso di UDP per il protocollo di trasporto di rete sottostante. Con TCP, la porta è associata a un singolo host remoto per la durata della sessione TLS. UDP non ha alcuna nozione di stato per quanto riguarda l'host remoto, quindi le richieste DTLS provenienti da host diversi verranno tutte ricevute sulla stessa interfaccia UDP. Pertanto, DTLS deve mantenere lo stato della sessione anziché basarsi sul socket come con TLS e TCP. Per questo motivo, il blocco di controllo del server DTLS (NX_SECURE_DTLS_SERVER) gestisce un mapping delle informazioni sull'host remoto (indirizzo IP e porta) alle sessioni DTLS. Tutti i dati in ingresso sul socket UDP assegnato a un server DTLS verranno mappati a una sessione DTLS nuova o esistente basata sull'host remoto. Per questo motivo, la creazione del server DTLS richiede diversi parametri aggiuntivi oltre a quanto richiesto dal client TLS e DTLS.

Oltre al blocco di controllo del server DTLS, ai ciphersuit TLS e al buffer dei metadati/scratchspace di crittografia, i server DTLS richiedono un buffer per mantenere le sessioni DTLS e un buffer di riassemblaggio pacchetti usato per decrittografare i record DTLS in ingresso.

Oltre ai buffer di sessione, i server DTLS richiedono un certificato digitale *,* ovvero un documento usato per identificare il server TLS al client TLS che si connette e i certificati corrispondenti alla chiave privata *,* in genere per l'algoritmo di crittografia RSA. Lo standard International Telecommunications Union X.509 specifica il formato del certificato usato da TLS/DTLS e sono disponibili numerose utilità per la creazione di certificati digitali X.509.

Per NetX Secure DTLS, il certificato X.509 deve essere codificato in formato binario usando il formato Distinguished Encoding Rules (DER) asN.1. DER è il formato binario tls over-the-wire standard per i certificati.

La chiave privata associata al certificato fornito deve essere DER-Encoded formato PKCS#1. La chiave privata viene usata solo nel dispositivo e non verrà mai trasmessa in rete. Mantenere al sicuro le chiavi private perché forniscono la sicurezza per le comunicazioni TLS/DTLS.

Per inizializzare il certificato del server DTLS, l'applicazione deve fornire un puntatore a un buffer contenente il certificato X.509 con codifica DER e i dati facoltativi della chiave privata RSA PKCS#1 con codifica DER usando il servizio ***nx_secure_x509_certificate_intialize,*** che popola la struttura **NX_SECURE_X509_CERT** con i dati del certificato appropriati per l'uso da parte di TLS.

Dopo l'inizializzazione, il certificato del server deve essere aggiunto al blocco di controllo TLS usando il ***nx_secure_dtls_server_local_certificate_add*** servizio.

Dopo aver aggiunto il certificato del server al blocco di controllo server DTLS, il server può essere usato per le comunicazioni DTLS sicure (vedere l'esempio precedente).

### <a name="initialization--dtls-client"></a>Inizializzazione - Client DTLS

La modalità client DTLS sicura NetX è semplice rispetto al server DTLS poiché esiste una sola connessione in uscita all'host remoto sul socket UDP.

Per configurare un client DTLS, è necessario un archivio certificati *attendibili,* ovvero una raccolta di certificati digitali con codifica X.509 provenienti da autorità di certificazione (CA) attendibili. Questi certificati vengono considerati "attendibili" dal protocollo DTLS e fungono da base per l'autenticazione dei certificati forniti dalle entità server DTLS all'applicazione Client DTLS sicura NetX.

Un certificato CA attendibile può essere *autofirmato* o firmato da un'altra CA, nel qual caso tale certificato è denominato *CA* intermedia (ICA). In una tipica applicazione TLS/DTLS, il server fornisce i certificati ICA insieme al relativo certificato server, ma l'unico requisito per la corretta autenticazione è che una catena di autorità emittente (certificati usati per firmare altri certificati) possa essere tracciata dal certificato del server a un certificato CA attendibile nell'archivio certificati attendibili. Questa catena è nota come catena *di certificati* o catena *di certificati.*

Per inizializzare un certificato CA o ICA attendibile, l'applicazione deve fornire un puntatore a un buffer contenente il certificato X.509 con codifica DER usando il servizio ***nx_secure_x509_certificate_intialize** _, che popola la struttura _ *NX_SECURE_X509_CERT** con i dati del certificato appropriati per l'uso da parte di TLS.

Il client DTLS necessita anche di spazio per l'allocazione del certificato del server in ingresso (presupponendo che non venga usata una modalità chiave precondipartito) e di un buffer per l'assemblaggio di pacchetti in record DTLS da decrittografare. Questi buffer vengono passati come  parametri al servizio nx_secure_dtls_session_create (per altre informazioni, vedere le informazioni di riferimento sulle API).

I certificati attendibili inizializzati vengono quindi aggiunti al blocco di controllo della sessione DTLS creato usando il ***nx_secure_dtls_session_trusted_certificate_add*** servizio. Se non si aggiunge un certificato, la sessione del client DTLS avrà esito negativo perché il protocollo DTLS non sarà in grado di autenticare gli host del server remoti.

Dopo aver creato l'archivio certificati attendibili, è possibile usare la sessione per stabilire una connessione client TLS sicura.

### <a name="application-interface-calls"></a>Chiamate all'interfaccia dell'applicazione

Le applicazioni NetX Secure DTLS in genere effettuano chiamate di funzione dai thread dell'applicazione in esecuzione nell'RTOS ThreadX. Alcune inizializzazioni, in particolare per i protocolli di comunicazione di rete sottostanti (ad esempio UDP e IP) possono essere chiamate da ***tx_application_define*.** Per altre informazioni sull'inizializzazione delle comunicazioni di rete, vedere il Manuale dell'utente di NetX/NetXDuo.

DTLS usa in modo intensivo le routine di crittografia che sono operazioni a elevato utilizzo di processore. In genere, queste operazioni verranno eseguite nel contesto del thread chiamante.

### <a name="dtls-session-start"></a>Avvio sessione DTLS

Per funzionare, DTLS richiede un protocollo di rete a livello di trasporto sottostante. Il protocollo in genere usato è TCP. Per stabilire una sessione TLS sicura di NetX, è necessario **** **NX_UDP_SOCKET** un nx_secure_dtls_client_session_start nel servizio per i client DTLS.

I server DTLS funzionano in modo diverso. Il socket UDP usato per le richieste client DTLS in ingresso è contenuto nel blocco di controllo NX_SECURE_DTLS_SERVER e viene inizializzato nella chiamata a ***nx_secure_dtls_server_create** _, che accetta la porta UDP locale come parametro. Il servizio _*_nx_secure_dtls_server_start_*_ viene quindi usato per avviare il server DTLS per gestire le richieste in ingresso. Tutte le richieste in ingresso vengono gestite nelle routine di callback fornite nx_secure_dtls_server_create*: una per le connessioni e una per _le notifiche di ricezione. È l'applicazione a_ gestire l'avvio della sessione DTLS quando viene ricevuta una notifica di connessione (il callback di notifica di connessione viene richiamato da DTLS) chiamando * nx_secure_dtls_server_session_start . L'applicazione deve anche gestire i dati in ingresso quando viene richiamato il callback di notifica di ricezione (che segue un handshake DTLS completato) chiamando _*_nx_secure_dtls_session_receive_**. I dettagli sono forniti nell'esempio precedente e nelle informazioni di riferimento sulle API per ognuno dei servizi indicati in precedenza.

### <a name="dtls-packet-allocation"></a>Allocazione di pacchetti DTLS

NetX Secure DTLS usa la stessa struttura di pacchetti di NetX/NetXDuo TCP (* NX_PACKET _),**ad** eccezione del fatto che invece di chiamare il _*_servizio nx_packet_allocate,_*_ è necessario chiamare il servizio _ *_nx_secure_dtls_packet_allocate_** in modo che lo spazio per l'intestazione DTLS possa essere allocato correttamente.

### <a name="dtls-session-send"></a>Invio sessione DTLS

Dopo l'avvio della sessione TLS, l'applicazione può inviare dati usando ***nx_secure_dtls_session_send*** servizio. Il servizio di trasmissione è identico al servizio ***nx_udp_socket_send** _, che prende una struttura di dati _ *_NX_PACKET_** contenente i dati inviati, un indirizzo IP di destinazione e una porta UDP di destinazione.

> [!IMPORTANT]
> Quando si inviano dati tramite nx_secure_dtls_session_send, è importante usare lo stesso indirizzo IP e la stessa porta usati per stabilire la sessione DTLS, a meno che non sia disponibile un meccanismo per spostare la sessione in un nuovo indirizzo e in una porta UDP in tempo reale (questo non è comune).

Tutti i dati inviati tramite DTLS verranno crittografati dallo stack NX Secure DTLS e dalle routine di crittografia configurate prima dell'invio.

### <a name="dtls-session-receive"></a>Ricezione sessione DTLS

Dopo l'avvio della sessione DTLS, l'applicazione può iniziare a ricevere dati usando il servizio ***nx_secure_Dtls_session_receive** _. Analogamente _all'invio_ della sessione DTLS, questo servizio è identico a _* nx_udp_socket_receive **, ad eccezione del fatto che i dati in ingresso vengono decrittografati e verificati dallo stack DTLS prima di essere restituiti nella struttura dei pacchetti.

### <a name="tls-session-close"></a>Chiusura della sessione TLS

Al termine di una sessione DTLS, sia il client che il server DTLS devono inviare un avviso CloseNotify all'altro lato per arrestare la sessione. Entrambi i lati devono ricevere ed elaborare l'avviso per garantire un arresto corretto della sessione.

Se l'host remoto invia un avviso CloseNotify, qualsiasi chiamata al servizio ***nx_secure_dtls_session_receive** _ eelaborare l'avviso, inviare l'avviso corrispondente all'host remoto e restituire il valore _*_NX_SECURE_TLS_SESSION_CLOSED_**. Dopo la chiusura della sessione, qualsiasi altro tentativo di inviare o ricevere dati con tale sessione DTLS avrà esito negativo.

Se l'applicazione vuole chiudere la sessione TLS, è **necessario nx_secure_dtls_session_end** il servizio * nx_secure_dtls_session_end _. Il servizio invierà l'avviso CloseNotify ed eelaborare la risposta CloseNotify. Se la risposta non viene ricevuta, verrà restituito il valore di errore _ *_NX_SECURE_TLS_SESSION_CLOSE_FAIL_** , che indica che la sessione DTLS non è stata arrestato in modo pulito, una possibile violazione della sicurezza.

### <a name="tlsdtls-alerts"></a>Avvisi TLS/DTLS

TLS/DTLS è progettato per garantire la massima sicurezza, quindi qualsiasi comportamento errante nel protocollo è considerato una potenziale violazione della sicurezza. Per questo motivo, eventuali errori nell'elaborazione dei messaggi o nella crittografia/decrittografia vengono considerati errori irreversibili che terminano immediatamente l'handshake o la sessione.

Anche se la gestione degli errori in un'applicazione locale è relativamente semplice, l'host remoto deve sapere che si è verificato un errore per gestire correttamente la situazione ed evitare altre possibili violazioni della sicurezza. Per questo motivo, TLS/DTLS invierà un messaggio *di* avviso all'host remoto in caso di errore.

Gli avvisi vengono trattati come qualsiasi altro messaggio TLS/DTLS e vengono crittografati durante la sessione per impedire a un utente malintenzionato di raccogliere informazioni dal tipo di avviso fornito. Durante l'handshake, gli avvisi inviati sono limitati nell'ambito per limitare la quantità di informazioni che possono essere ottenute da un potenziale utente malintenzionato.

L'avviso CloseNotify, usato per chiudere la sessione TLS/DTLS, è l'unico avviso non irreversibile. Sebbene sia considerato un avviso e inviato come messaggio di avviso, closeNotify è diverso da altri avvisi perché non indica che si è verificato un errore.

### <a name="tlsdtls-session-renegotiation-and-resumption"></a>Rinegoziazione e ripresa della sessione TLS/DTLS

TLS supporta la nozione di "rinegoziazione", che è semplicemente una rinegoziazione dei parametri di sessione TLS nel contesto di una sessione TLS esistente.

La ripresa *della sessione* TLS non deve essere confusa con la *rinegoziazione della sessione,* nonostante alcune analogie. Quando la *rinegoziazione* della sessione comporta l'avvio di  un nuovo handshake all'interno di una sessione TLS esistente, la ripresa della sessione è una funzionalità puramente facoltativa che prevede il riavvio di una sessione TLS chiusa senza eseguire un handshake TLS completo.

NX Secure DTLS gestisce le richieste di rinegoziazione in ingresso dagli host remoti. Non supporta **la** ripresa della sessione. Una descrizione più completa di queste funzionalità è disponibile nel capitolo 3 della Guida dell'utente di NetX Secure TLS.

### <a name="protocol-layering"></a>Livelli di protocollo

Il protocollo TLS (e quindi anche DTLS) si inserisce nello stack di rete tra il livello di trasporto (ad esempio TCP o UDP) e il livello applicazione. TLS viene talvolta considerato un protocollo a livello di trasporto (quindi *Transport Layer* Security), ma poiché funge da applicazione per quanto riguarda i protocolli di rete sottostanti, viene talvolta raggruppato nel livello applicazione.

TLS richiede un protocollo del livello di trasporto che supporta il recapito in ordine e senza perdita, ad esempio TCP. A causa di questo requisito, TLS non può essere eseguito su UDP perché UDP non garantisce il recapito di datagrammi. *DTLS* è una versione modificata di TLS, usata per le applicazioni che necessitano della sicurezza di TLS su un protocollo di datagrammi come UDP.

![Diagramma della strattura di un protocollo TLS.](media/image6.png)

**Figura 4- Livelli di protocollo TCP/IP, UDP e TLS/DTLS**

## <a name="network-communications-security-and-encryption"></a>Sicurezza e crittografia delle comunicazioni di rete

La protezione delle comunicazioni tramite reti pubbliche e Internet è un argomento di importanza critica e oggetto di un numero elevato di libri, articoli e soluzioni. L'argomento è estremamente complesso, ma può essere ridotto a un'idea semplice: l'invio di informazioni in rete in modo che solo la destinazione prevista possa accedere a queste informazioni o modificarle. Questo si suddivide in tre concetti importanti: segretezza, integrità e autenticazione. Il protocollo TLS/DTLS fornisce soluzioni per tutti e tre.

La crittografia viene usata in modi diversi per fornire segretezza, integrità e autenticazione all'interno dei protocolli TLS e DTLS. La crittografia deve essere fornita a TLS o DTLS al momento della creazione di una sessione o di un'istanza del server, perché TLS fornisce un framework flessibile per l'uso della crittografia e non della crittografia stessa. NetX Secure DTLS fornisce le routine di crittografia necessarie per la maggior parte delle applicazioni, quindi non è necessario preoccuparsi di trovare la crittografia appropriata.

Una descrizione più dettagliata di questi argomenti è disponibile nel capitolo 3 della Guida dell'utente di NetX Secure TLS.

## <a name="tls-and-dtls-extensions"></a>Estensioni TLS e DTLS

TLS (e quindi DTLS) fornisce una serie di estensioni che forniscono funzionalità aggiuntive per determinate applicazioni. Queste estensioni vengono in genere inviate come parte dei messaggi ClientHello o ServerHello, che indicano a un host remoto la voglia di usare un'estensione o fornire dettagli aggiuntivi per l'uso per stabilire la sessione TLS sicura.

NetX Secure DTLS supporta tutte le estensioni disponibili in NetX Secure TLS e una descrizione completa di tali estensioni è disponibile nella Guida per l'utente di NetX Secure TLS, capitolo 3.

## <a name="authentication-methods"></a>Authentication Methods

TLS e DTLS forniscono il framework per stabilire una connessione sicura tra due dispositivi su una rete non sicura, ma parte del problema è conoscere l'identità del dispositivo dall'altra parte della connessione. Senza un meccanismo per autenticare l'identità degli host remoti, diventa un'operazione semplice che un utente malintenzionato può rappresentare come un dispositivo attendibile.

Inizialmente, potrebbe sembrare che l'uso di indirizzi IP, indirizzi MAC hardware o DNS fornirebbe un livello di attendibilità relativamente elevato per l'identificazione degli host in una rete, ma data la natura della tecnologia TCP/IP e la facilità con cui gli indirizzi possono essere falsificati e le voci DNS danneggiate (ad esempio tramite un poisoning della cache DNS), è chiaro che TLS richiede un ulteriore livello di protezione dalle identità fraudolente.

Esistono diversi meccanismi che possono fornire questo ulteriore livello di autenticazione per TLS, ma il più comune è il *certificato digitale.* Altri meccanismi includono chiavi precondizioni (PSK) e schemi di password.

### <a name="digital-cerificates"></a>Cerificati digitali

I certificati digitali sono il metodo più comune per l'autenticazione di un host remoto in TLS. Essenzialmente, un certificato digitale è un documento con formattazione specifica che fornisce informazioni di identità per un dispositivo in una rete di computer.

TLS usa in genere un formato denominato X.509, uno standard sviluppato dall'International Telecommunication Union, anche se è possibile usare altri formati di certificati se gli host TLS possono accettare il formato usato. X.509 definisce un formato specifico per i certificati e varie codifiche che possono essere usate per produrre un documento digitale. La maggior parte dei certificati X.509 usati con TLS viene codificata usando una variante di ASN.1, un altro standard di telecomunicazioni. All'interno di ASN.1 sono disponibili diverse codifiche digitali, ma la codifica più comune per i certificati TLS è lo standard Distinguished Encoding Rules (DER). DER è un subset semplificato delle regole di codifica di base (BER) ASN.1 progettate per non ambiguità, semplificando l'analisi. In transito, i certificati TLS vengono in genere codificati in der binario e questo è il formato previsto da NetX Secure per i certificati X.509.

Anche se i certificati binari in formato DER vengono usati nel protocollo TLS effettivo, possono essere generati e archiviati in diverse codifiche, con estensioni di file come pem, crt e p12. Le diverse varianti vengono usate da applicazioni diverse di produttori diversi, ma in genere tutte possono essere convertite in DER usando strumenti ampiamente disponibili.

La codifica dei certificati alternativa più comune è PEM. Il formato PEM (da Privacy-Enhanced Mail) è una versione codificata in base 64 della codifica DER spesso usata perché la codifica comporta un testo stampabile che può essere facilmente inviato tramite posta elettronica o protocolli basati sul Web.

La generazione di un certificato per l'applicazione NetX Secure non rientra in genere nell'ambito di questo manuale, ma lo strumento da riga di comando OpenSSL ([www.openssl.org](http://www.openssl.org)) è ampiamente disponibile e può essere convertito tra la maggior parte dei formati.

A seconda dell'applicazione, è possibile generare certificati personalizzati, essere forniti da un produttore o un'organizzazione governativa o acquistare certificati da un'autorità di certificazione commerciale.

Per usare un certificato digitale nell'applicazione NetX Secure, è prima necessario convertire il certificato in un formato DER binario e, facoltativamente, convertire la chiave privata associata (l'esponente privato" per RSA, ad esempio) in un formato binario, in genere una chiave RSA con codifica PKCS#1. Al termine della conversione, è necessario caricare il certificato e la chiave privata nel dispositivo. Le opzioni possibili includono l'uso di un file system basato su flash o la generazione di una matrice C dai dati (usando uno strumento come "xxd" da Linux) e la compilazione del certificato e della chiave nell'applicazione come dati costanti.

Dopo aver caricato il certificato nel dispositivo, è possibile usare l'API DTLS per associare il certificato a una sessione o a un server DTLS.

Per informazioni dettagliate ed esempi su come usare i certificati X.509 con NetX Secure DTLS, vedere la sezione "Importazione di certificati X.509 in NetX Secure" nel Manuale dell'utente di NetX Secure TLS.

Per altre informazioni, vedere i servizi DTLS seguenti nelle informazioni di riferimento sulle API:

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

Le implementazioni del client DTLS in genere non richiedono il caricamento di un certificato locale nel dispositivo. Un certificato locale è un certificato che identifica il dispositivo locale. In particolare, un certificato locale fornisce informazioni sull'identità per il dispositivo su cui viene caricata l'applicazione TLS/DTLS. L'eccezione è quando è abilitata l'autenticazione del certificato client, ma questa operazione è meno comune.

Un client DTLS richiede il caricamento di almeno un certificato attendibile (se necessario ne possono caricare altri) e lo spazio per l'allocazione di un certificato remoto. Un certificato attendibile è un certificato che fornisce una base per l'attendibilità e l'autenticazione del dispositivo remoto, direttamente o tramite un'infrastruttura a chiave pubblica (PKI). La radice della catena di attendibilità è in genere denominata autorità di certificazione o certificato CA. Un certificato remoto fa riferimento al certificato inviato dall'host remoto durante l'handshake TLS. Fornisce l'identità per l'host remoto e viene autenticato confrontandolo con un certificato attendibile nel dispositivo locale.

Per altre informazioni sull'aggiunta di certificati attendibili e sull'allocazione di spazio per i certificati remoti, vedere le informazioni di riferimento sulle API TLS per i servizi seguenti: nx_secure_dtls_session_create, nx_secure_dtls_session_trusted_certificate_add.

### <a name="tlsdtls-server-certificate-specifics"></a>Specifiche del certificato del server TLS/DTLS

Le implementazioni del server DTLS in genere non richiedono il caricamento di certificati "attendibili" nel dispositivo o l'allocazione dei certificati remoti. L'eccezione è che quando è abilitata l'autenticazione del certificato client.

Un server TLS richiede il caricamento di un certificato "locale" (o "identità") in modo che il server possa fornirlo al client remoto durante l'handshake TLS per autenticare il server al client.

Per altre informazioni sul caricamento di certificati locali da usare con le applicazioni server NETX TLS, vedere le informazioni di riferimento sulle API per i servizi seguenti: nx_secure_dtls_server_local_certificate_add, nx_secure_dtls_server_local_certificate_remove.


### <a name="pre-shared-keys-psk"></a>Chiavi precondicondite (PSK)

Un meccanismo alternativo per fornire l'autenticazione di identificazione in TLS è la nozione di chiavi precondicondite (PSK). L'uso di una crittografia PSK elimina la necessità di eseguire operazioni di crittografia a chiave pubblica a elevato utilizzo di processore, un elemento fondamentale per i dispositivi incorporati con vincoli di risorse. La chiave PSK sostituisce il certificato nell'handshake TLS/DTLS e viene usata al posto del segreto pre-master crittografato per la generazione della chiave di sessione TLS/DTLS.

Le ciphersuit PSK sono limitate nel senso che un segreto condiviso deve essere presente in entrambi i dispositivi prima di poter stabilire una sessione TLS/DTLS. Ciò significa che i dispositivi devono essere stati caricati con tale segreto usando alcuni mezzi sicuri diversi da una connessione PSK TLS. I pacchetti PSK possono essere aggiornati tramite una connessione PSK TLS, ma il dispositivo deve necessariamente iniziare con una chiave PSK caricata tramite un altro meccanismo. Ad esempio, un dispositivo sensore e il relativo dispositivo gateway possono essere caricati con psk nella factory prima della spedizione oppure è possibile usare una connessione TLS standard (con un certificato) per caricare la chiave PSK.

Le ciphersuitE PSK sono in due forme, descritte in RFC 4279. La prima usa le chiavi RSA o Diffie-Hellman usate nello stesso modo delle chiavi pubbliche trasmesse nel certificato negli handshake TLS standard. La seconda forma, che è più usata in un ambiente con vincoli di risorse, usa una chiave PSK usata per generare direttamente le chiavi di sessione (ad esempio, per l'uso da parte di AES), evitando l'uso delle costose operazioni RSA o Diffie-Hellman.

NetX Secure supporta la seconda forma di crittografie PSK, consentendo alle applicazioni di rimuovere tutto il codice di crittografia a chiave pubblica e l'utilizzo della memoria. La chiave PSK non è una chiave AES, ma può essere considerata più simile a una password da cui vengono generate le chiavi effettive. Esistono poche restrizioni su ciò che può essere il valore PSK, anche se i valori più lunghi offrono una maggiore sicurezza (come con le password).

Per usare PSK con l'applicazione NetX Secure, è innanzitutto necessario definire la macro **globale NX_SECURE_ENABLE_PSK_CIPHERSUITES**. Questa operazione viene in genere eseguita tramite le impostazioni del compilatore, ma la definizione può essere inserita anche nel file di intestazione nx_secure_tls.h. Con la macro definita, il supporto della crittografia PSK verrà compilato nell'applicazione NetX Secure DTLS.

Con il supporto PSK abilitato, è quindi possibile usare l'API DTLS per configurare i file PSK per l'applicazione. Ogni chiave PSK richiederà un valore PSK (la "chiave" privata effettiva: mantenere questo valore sicuro), un valore "identity" usato per identificare la chiave PSK specifica e un "hint di identità" usato da un server TLS per scegliere un valore PSK specifico.

La chiave PSK stessa può essere qualsiasi valore binario perché non viene mai inviata tramite una connessione di rete. PSK può avere una lunghezza massima di 64 byte.

L'identità e l'hint devono essere stringhe di caratteri stampabili formattate con UTF-8. I valori identity e hint possono avere una lunghezza massima di 128 byte.

L'identità e PSK formano una coppia univoca che viene caricata in ogni dispositivo della rete che deve comunicare tra loro.

L'"hint" viene usato principalmente per definire profili di applicazione specifici per raggruppare i file PSK in base alla funzione o al servizio. Questi valori devono essere concordati in anticipo e dipendono dall'applicazione. Ad esempio, l'applicazione server della riga di comando OpenSSL (con PSK abilitato) usa la stringa predefinita "Client_identity", che deve essere fornita da un client TLS per continuare con l'handshake TLS.

Per altre informazioni su PSK, vedere le informazioni di riferimento sull'API NetX Secure per i servizi seguenti: nx_secure_dtls_psk_add, nx_secure_dtls_server_psk_add.

## <a name="importing-x509-certificates-into-netx-secure"></a>Importazione di certificati X.509 in NetX Secure

I certificati digitali sono necessari per la maggior parte delle connessioni TLS su Internet. I certificati forniscono un metodo per l'autenticazione di host precedentemente sconosciuti su Internet tramite l'uso di intermediari attendibili, in genere denominati autorità di certificazione *o* AUTORITÀ di certificazione. Per connettere il dispositivo NetX Secure a un servizio cloud commerciale (ad esempio Amazon Web Services), è necessario importare i certificati nell'applicazione caricandoli nel dispositivo.

Insieme ai certificati, a volte è necessaria anche una *chiave* privata associata al certificato. In alcune applicazioni ,ad esempio il client TLS quando l'autenticazione del certificato client non è in uso, il certificato sarà sufficiente, ma se il certificato viene usato per identificare il dispositivo, sarà necessaria una chiave privata. Le chiavi private vengono in genere generate quando si crea il certificato e vengono archiviate in un file separato, spesso crittografate con una password.

Per una descrizione dettagliata dell'importazione di certificati in applicazioni NetX Secure, vedere il capitolo 3 nella Guida dell'utente di NetX Secure TLS.

## <a name="client-certificate-authentication-in-netx-secure-tls"></a>Autenticazione del certificato client in NetX Secure TLS

Quando si usa l'autenticazione con certificato X.509, il protocollo TLS/DTLS richiede che l'istanza del server DTLS fornisci un certificato per l'identificazione, ma per impostazione predefinita l'istanza del client DTLS non deve fornire un certificato per l'autenticazione, usando invece un'altra forma di autenticazione ,ad esempio una combinazione di nome utente/password. Corrisponde all'uso più comune di TLS su Internet per i siti Web. Ad esempio, un sito di vendita al dettaglio online deve dimostrare a un potenziale cliente che usa un Web browser che il server è legittimo, ma l'utente userà un account di accesso/password per accedere a un account specifico.

Tuttavia, il caso predefinito non è sempre consigliabile, quindi TLS/DTLS consente facoltativamente all'istanza del server DTLS di richiedere un certificato dal client remoto. Quando questa funzionalità è abilitata, il server DTLS invierà un messaggio CertificateRequest al client DTLS durante l'handshake. Il client deve rispondere con un certificato proprio e un messaggio CertificateVerify che contiene un token di crittografia che dimostra che il client è proprietario della chiave privata corrispondente associata a tale certificato. Se la verifica non riesce o il certificato non è connesso a un certificato attendibile nel server, l'handshake TLS ha esito negativo.

Esistono due casi distinti per l'autenticazione del certificato client in TLS: le sezioni seguenti illustrano entrambi i casi.

### <a name="client-certificate-authentication-for-dtls-clients"></a>Autenticazione del certificato client per i client DTLS

Un client DTLS può tentare una connessione a un server che richiede un certificato per l'autenticazione client. In questo caso, il client deve fornire un certificato al server e verificare che sia proprietario della chiave privata corrispondente oppure il server terminerà l'handshake DTLS.

In NetX Secure DTLS non è disponibile alcuna configurazione speciale per supportare questa funzionalità, ma l'applicazione dovrà fornire un certificato di identificazione locale per l'istanza del client TLS usando il servizio *nx_secure_tls_session_local_certificate_add* locale. Se l'applicazione non specifica alcun certificato ma il server remoto usa l'autenticazione del certificato client e richiede un certificato, l'handshake DTLS avrà esito negativo. Il certificato fornito alla sessione DTLS *con nx_secure_dtls_session_local_certificate_add* deve essere riconosciuto dal server remoto per completare l'handshake DTLS.

### <a name="client-certificate-authentication-for-tls-servers"></a>Autenticazione del certificato client per i server TLS

Il caso del server DTLS per l'autenticazione del certificato client è leggermente più complesso rispetto al caso del client DTLS a causa della funzionalità facoltativa. In questo caso, il server TLS deve richiedere in modo specifico un certificato dal client TLS remoto, quindi elaborare il messaggio CertificateVerify per verificare che il client remoto sia proprietario della chiave privata corrispondente e quindi il server deve verificare che il certificato fornito dal client possa essere tracciato in un certificato nell'archivio certificati attendibili locale.

Nelle istanze del server NETX Secure TLS l'autenticazione del certificato client è controllata dai nx_secure_dtls_server_x509_client_verify_configure *e* *nx_secure_dtls_server_x509_client_verify_disable* client.

Per abilitare l'autenticazione del certificato client, un'applicazione deve chiamare *nx_secure_dtls_server_x509_client_verify_configure* con l'istanza di sessione del server DTLS prima di chiamare *nx_secure_dtls_server_start*. La verifica richiede che sia allocato spazio per i certificati client in ingresso, che viene fornito come parametro per *nx_secure_dtls_server_x509_client_verify_configure.* Si noti che il buffer deve essere sufficientemente grande da contenere la catena di certificati di dimensioni massime fornita da un client per il numero di sessioni *del server DTLS.* Ogni sessione del server richiede spazio che verrà allocato dal singolo buffer fornito. Assicurarsi che il buffer sia sufficientemente grande o che si verifichi un errore se la catena di certificati client specificata è troppo grande.

Quando l'autenticazione del certificato client è abilitata, il server DTLS richiederà un certificato dal client DTLS remoto durante l'handshake DTLS. In NetX Secure DTLS Server, il certificato client viene controllato rispetto *all'archivio dei* certificati attendibili creati con nx_secure_dtls_server_trusted_certificate_add seguendo la catena di autorità di certificazione X.509. Il client remoto deve fornire una catena che connette il certificato di identità a un certificato nell'archivio attendibile o l'handshake DTLS avrà esito negativo. Inoltre, se l'elaborazione del messaggio CertificateVerify ha esito negativo, anche l'handshake DTLS avrà esito negativo.

I metodi di firma usati per il metodo CertificateVerify sono corretti per TLS versione 1.0 e TLS versione 1.1 e sono specificati dal server TLS in TLS versione 1.2, su cui è basato NetX Secure DTLS. Per DTLS 1.2, i metodi di firma supportati in genere seguono i metodi pertinenti forniti nella tabella dei metodi di crittografia, ma in genere RSA con SHA-256 (vedere la sezione "Crittografia in NetX Secure TLS" per altre informazioni sull'inizializzazione di TLS con metodi di crittografia).

## <a name="cryptography-in-netx-secure-tls"></a>Crittografia in NetX Secure TLS

TLS definisce un protocollo in cui la crittografia può essere usata per proteggere le comunicazioni di rete. Di conseguenza, lascia la crittografia effettiva da usare piuttosto ampia per gli utenti TLS. La specifica richiede solo l'implementazione di un singolo ciphersuite: nel caso di TLS 1.2, la crittografia è TLS_RSA_WITH_AES_128_CBC_SHA, che indica l'uso di RSA per le operazioni a chiave pubblica, AES in modalità CBC con chiavi a 128 bit per la crittografia della sessione e SHA-1 per gli hash di autenticazione dei messaggi.

Essendo conforme a TLS 1.2, NetX Secure abilita la crittografia TLS_RSA_WITH_AES_128_CBC_SHA obbligatoria per impostazione predefinita, ma considerando il numero di possibili implementazioni per ognuno dei metodi di crittografia a causa delle funzionalità hardware e di altre considerazioni, NetX Secure fornisce un'API di crittografia generica che consente a un utente di specificare i metodi di crittografia da usare con TLS.

> [!NOTE]
> Il meccanismo api crittografico generico consente anche agli utenti di implementare le proprie ciphersuit, ma è consigliabile per gli utenti avanzati che hanno familiarità con le estensioni e le ciphersuit TLS. Se si è interessati a supportare le proprie ciphersuit, contattare il rappresentante di Express Logic.

Per una descrizione dettagliata su come configurare i metodi di crittografia per DTLS, vedere la Guida dell'utente di NetX Secure TLS, capitolo 3. Lo stesso processo si applica sia a TLS che a DTLS.
