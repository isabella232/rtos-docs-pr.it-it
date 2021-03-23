---
title: Capitolo 3-componenti funzionali di Azure RTO NetX
description: Questo capitolo contiene una descrizione dello stack TCP/IP di Azure RTO NetX a prestazioni elevate dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: db23aa152b2765ac7cc9be098723fc5df0947484
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822790"
---
# <a name="chapter-3---functional-components-of-azure-rtos-netx"></a>Capitolo 3-componenti funzionali di Azure RTO NetX

Questo capitolo contiene una descrizione dello stack TCP/IP di Azure RTO NetX a prestazioni elevate dal punto di vista funzionale. 

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Esistono cinque tipi di esecuzione del programma all'interno di un'applicazione NetX: inizializzazione, chiamate dell'interfaccia dell'applicazione, thread IP interno, timer periodici IP e driver di rete.

> [!IMPORTANT]
> NetX richiede l'installazione di ThreadX e dipende dall'esecuzione del thread, dalla sospensione, dai timer periodici e dalle strutture di esclusione reciproca.

### <a name="initialization"></a>Inizializzazione

Il servizio ***nx_system_initialize** _ deve essere chiamato prima di chiamare qualsiasi altro servizio NETX. L'inizializzazione del sistema può essere chiamata dalla routine ThreadX _ *_tx_application_define_** o dai thread dell'applicazione.

Dopo che ***nx_system_initialize** _ restituisce, il sistema è pronto per la creazione di pool di pacchetti e istanze IP. Poiché la creazione di un'istanza IP richiede un pool di pacchetti predefinito, è necessario che esista almeno un pool di pacchetti NetX prima di creare un'istanza IP. La creazione di pool di pacchetti e istanze IP è consentita dalla funzione di inizializzazione ThreadX _ *_tx_application_define_** e dai thread dell'applicazione.

Internamente, la creazione di un'istanza IP viene eseguita in due parti. La prima parte viene eseguita nel contesto del chiamante, dal ***tx_application_define*** o dal contesto del thread di un'applicazione. Ciò include la configurazione della struttura dei dati IP e la creazione di varie risorse IP, incluso il thread IP interno. La seconda parte viene eseguita durante l'esecuzione iniziale dal thread IP interno. Questo è il punto in cui il driver di rete, fornito durante la prima parte della creazione dell'IP, viene chiamato per la prima volta. La chiamata del driver di rete dal thread IP interno consente al driver di eseguire operazioni di I/O e di sospendere durante l'elaborazione dell'inizializzazione. Quando il driver di rete viene restituito dalla relativa elaborazione di inizializzazione, la creazione dell'indirizzo IP è stata completata.

> [!IMPORTANT]
> Il **nx_ip_status_check** del servizio NETX è disponibile per ottenere informazioni sull'istanza IP e lo stato dell'interfaccia principale. Tali informazioni di stato includono il fatto che il collegamento sia inizializzato, abilitato e che l'indirizzo IP venga risolto. Queste informazioni vengono usate per sincronizzare i thread dell'applicazione che richiedono l'uso di un'istanza IP appena creata. Per i sistemi multihome, vedere "supporto multihome" di seguito. **nx_ip_interface_status_check** è disponibile per ottenere informazioni sull'interfaccia specificata.

### <a name="application-interface-calls"></a>Chiamate dell'interfaccia dell'applicazione

Le chiamate dall'applicazione vengono eseguite in gran parte dai thread dell'applicazione in esecuzione in ThreadX RTO. Tuttavia, alcuni servizi di inizializzazione, creazione e abilitazione possono essere chiamati da ***tx_application_define***. Le sezioni "consentito da" del capitolo 4 indicano da quale servizio NetX è possibile chiamare.

Nella maggior parte dei casi, l'elaborazione di attività intensive, ad esempio il calcolo dei checksum, viene eseguita nel contesto del thread chiamante, senza bloccare l'accesso di altri thread all'istanza IP. Ad esempio, sulla trasmissione, il calcolo del checksum UDP viene eseguito all'interno del servizio ***nx_udp_socket_send*** , prima di chiamare la funzione di invio IP sottostante. In un pacchetto ricevuto, il checksum UDP viene calcolato nel servizio ***nx_udp_socket_receive*** , eseguito nel contesto del thread dell'applicazione. Ciò consente di impedire il blocco delle richieste di rete di thread con priorità più alta a causa dell'elaborazione di calcoli di checksum intensivi nei thread con priorità più bassa.

I valori, ad esempio gli indirizzi IP e i numeri di porta, vengono passati alle funzioni API nell'ordine dei byte dell'host. Internamente, questi valori vengono archiviati anche nell'ordine dei byte dell'host. Ciò consente agli sviluppatori di visualizzare facilmente i valori tramite un debugger. Quando questi valori vengono programmati in un frame per la trasmissione, vengono convertiti in ordine byte di rete.

### <a name="internal-ip-thread"></a>Thread IP interno

Come indicato in precedenza, ogni istanza IP in NetX ha il proprio thread. La priorità e le dimensioni dello stack del thread IP interno sono definite nel servizio ***nx_ip_create*** . Il thread IP interno viene creato in modalità pronta per l'esecuzione. Se il thread IP ha una priorità più elevata rispetto al thread chiamante, è possibile che si verifichi la precedenza all'interno della chiamata di creazione IP.

Il punto di ingresso del thread IP interno si trova nella funzione interna ***_nx_ip_thread_entry***. Quando viene avviato, il thread IP interno completa innanzitutto l'inizializzazione del driver di rete, che consiste nell'effettuare tre chiamate al driver di rete specifico dell'applicazione. La prima chiamata consiste nel connettersi al driver di rete all'istanza IP, seguita da una chiamata di inizializzazione, che consente al driver di rete di passare attraverso il processo di inizializzazione. Dopo che il driver di rete è stato restituito dall'inizializzazione (potrebbe sospendere in attesa della corretta configurazione dell'hardware), il thread IP interno chiama di nuovo il driver di rete per abilitare il collegamento. 

Quando il driver di rete viene restituito dalla chiamata di Abilita collegamento, il thread IP interno entra in un ciclo infinito verificando la presenza di diversi eventi che necessitano di elaborazione per questa istanza IP. Gli eventi elaborati in questo ciclo includono la ricezione di pacchetti IP posticipati, l'assembly dei frammenti di pacchetti IP, l'elaborazione dei ping ICMP, l'elaborazione IGMP, l'elaborazione della coda di pacchetti TCP, l'elaborazione periodica TCP, i timeout degli assembly dei frammenti IP e l'elaborazione periodica di IGMP. Gli eventi includono inoltre le attività di risoluzione degli indirizzi: elaborazione dei pacchetti ARP e elaborazione periodica ARP nella rete IP.

> [!NOTE]
> *Le funzioni di callback NetX, inclusi i callback di ascolto e disconnessione, vengono chiamate dal thread IP interno, non dal thread chiamante originale. È necessario che l'applicazione non venga sospesa all'interno di una funzione di callback NetX.*

### <a name="ip-periodic-timers"></a>Timer periodici IP
Per ogni istanza IP sono usati due timer periodici ThreadX. Il primo è un timer di un secondo per ARP, IGMP, TCP timeout e anche l'elaborazione del frammento IP del riassemblaggio. Il secondo timer è un timer 100 ms per guidare il timeout di ritrasmissione TCP.

### <a name="network-driver"></a>Driver di rete
Ogni istanza IP in NetX ha un'interfaccia primaria, identificata dal relativo driver di dispositivo specificato nel servizio ***nx_ip_create*** . Il driver di rete è responsabile della gestione di varie richieste NetX, tra cui la trasmissione di pacchetti, la ricezione di pacchetti e le richieste di stato e controllo.

Per un sistema multi-Home, l'istanza IP dispone di più interfacce, ciascuna con un driver di rete associato che esegue queste attività per la rispettiva interfaccia.

Il driver di rete deve inoltre gestire gli eventi asincroni che si verificano sui supporti. Gli eventi asincroni dai supporti includono la ricezione di pacchetti, il completamento della trasmissione del pacchetto e le modifiche dello stato. NetX fornisce al driver di rete numerose funzioni di accesso per gestire vari eventi. Queste funzioni sono progettate per essere chiamate dalla parte di routine del servizio di interrupt del driver di rete. Per le reti IP, il driver di rete deve inoltrare tutti i pacchetti ARP ricevuti alla funzione interna ***_nx_arp_packet_deferred_receive** _. Tutti i pacchetti RARP devono essere inoltrati a _ *_ _nx_rarp_packet_deferred_receive_* _ funzione interna. Sono disponibili due opzioni per i pacchetti IP. Se è necessario inviare rapidamente i pacchetti IP, i pacchetti IP in ingresso devono essere inoltrati a _ *_ _nx_ip_packet_receive_* _ per l'elaborazione immediata. Ciò migliora notevolmente le prestazioni di NetX nella gestione dei pacchetti IP. In caso contrario, il driver di rete deve inoltrare i pacchetti IP a _ * _ _nx_ip_packet_deferred_receive_* *. Questo servizio posiziona il pacchetto IP nella coda di elaborazione posticipata, dove viene quindi gestito dal thread IP interno, che comporta la quantità minima di tempo di elaborazione ISR.

Il driver di rete può anche rinviare l'elaborazione di interrupt per esaurire il contesto del thread IP. In questa modalità, l'ISR deve salvare le informazioni necessarie, chiamare la funzione interna ***_nx_ip_driver_deferred_processing*** e confermare il controller di interrupt. Questo servizio invia una notifica al thread IP per pianificare un callback al driver di dispositivo per completare l'elaborazione dell'evento che provoca l'interruzione.

Alcuni controller di rete sono in grado di eseguire il calcolo e la convalida del checksum dell'intestazione TCP/IP nell'hardware, senza occupare risorse di CPU utili. Per sfruttare i vantaggi della funzionalità hardware funzionalità, NetX fornisce opzioni per abilitare o disabilitare diversi calcoli di checksum software in fase di compilazione, nonché per attivare o disattivare il calcolo dei checksum in fase di esecuzione. Per informazioni più dettagliate sulla scrittura di driver di rete NetX, vedere "[capitolo 5 driver di rete NETX](chapter5.md)".

### <a name="multihome-support"></a>Supporto multihome
NetX supporta i sistemi connessi a più dispositivi fisici usando una singola istanza IP. Ogni interfaccia fisica viene assegnata a un blocco di controllo dell'interfaccia nell'istanza IP. Le applicazioni che desiderano utilizzare un sistema multihome devono definire il valore per **NX_MAX_PHSYCIAL_INTERFACES** al numero di dispositivi fisici collegati al sistema e ricompilare la libreria NETX. Per impostazione predefinita **NX_MAX_PHYSICAL_INTERFACES** è impostato su uno, creando un blocco di controllo dell'interfaccia nell'istanza IP.

L'applicazione NetX crea una singola istanza IP per il dispositivo primario usando il servizio ***nx_ip_create** _. Per ogni dispositivo di rete aggiuntivo, l'applicazione connette il dispositivo all'istanza IP usando il servizio _ *_nx_ip_interface_attach_**.

Ogni struttura di interfaccia di rete contiene un subset di informazioni di rete sull'interfaccia di rete contenuta nel blocco di controllo IP, tra cui indirizzo IP dell'interfaccia, subnet mask, dimensioni MTU IP e informazioni sugli indirizzi del livello MAC.

> [!IMPORTANT]
> *NetX con supporto multihome è compatibile con le versioni precedenti di NetX. I servizi che non accettano informazioni esplicite sull'interfaccia vengono predefiniti per il dispositivo di rete primario.*

L'interfaccia primaria ha indice zero nell'elenco di istanze IP. A ogni dispositivo successivo collegato all'istanza IP viene assegnato l'indice successivo.

Tutti i servizi del protocollo di livello superiore per i quali è abilitata l'istanza IP, inclusi TCP, UDP, ICMP e IGMP, sono disponibili per tutti i dispositivi collegati.

Nella maggior parte dei casi, NetX è in grado di determinare l'indirizzo di origine migliore da usare durante la trasmissione di un pacchetto. La selezione dell'indirizzo di origine è basata sull'indirizzo di destinazione. I servizi NetX vengono forniti per consentire alle applicazioni di specificare un indirizzo di origine specifico da usare, nei casi in cui l'indirizzo di destinazione non può essere determinato da quello più adatto. Un esempio è costituito da un sistema multihome, un'applicazione deve inviare un pacchetto a un indirizzo di trasmissione IP o di destinazione multicast.

I servizi specifici per lo sviluppo di applicazioni multihome includono quanto segue:

*nx_igmp_multicast_interface_join nx_ip_driver_interface_direct_command nx_ip_interface_address_get nx_ip_interface_address_set nx_ip_interface_attach nx_ip_interface_info_get nx_ip_interface_status_check nx_ip_raw_packet_interface_send nx_udp_socket_interface_send*

Questi servizi sono descritti in modo più dettagliato in "[capitolo 4-Descrizione dei servizi NETX di Azure RTO](chapter4.md)".

### <a name="loopback-interface"></a>Interfaccia loopback
L'interfaccia di loopback è un'interfaccia di rete speciale senza collegamento fisico associato a. L'interfaccia di loopback consente alle applicazioni di comunicare utilizzando l'indirizzo IP di loopback 127.0.0.1

Per utilizzare un'interfaccia di loopback logica, assicurarsi che l'opzione configurabile ***NX_DISABLE_LOOPBACK_INTERFACE*** non sia impostata.

### <a name="interface-control-blocks"></a>Blocchi di controllo dell'interfaccia
Il numero di blocchi di controllo dell'interfaccia nell'istanza IP è il numero di interfacce fisiche (definite da ***NX_MAX_PHYSICAL_INTERFACES** _) più l'interfaccia di loopback se abilitata. Il numero totale di interfacce è definito in _ *_NX_MAX_IP_INTERFACES_* *.

## <a name="protocol-layering"></a>Layering del protocollo

Il protocollo TCP/IP implementato da NetX è un protocollo sovrapposto, che significa che i protocolli più complessi sono basati su protocolli sottostanti più semplici. In TCP/IP, il protocollo di livello più basso si trova a *livello di collegamento* e viene gestito dal driver di rete. Questo livello è in genere destinato a Ethernet, ma può anche essere Fiber, seriale o praticamente qualsiasi supporto fisico.

Sopra il livello di collegamento è il *livello di rete*. In TCP/IP, questo è l'indirizzo IP, che è essenzialmente responsabile dell'invio e della ricezione di pacchetti semplici, in modo ottimale, attraverso la rete. I protocolli di tipo di gestione come ICMP e IGMP vengono in genere categorizzati anche come livelli di rete, anche se si basano su IP per l'invio e la ricezione.

Il *livello di trasporto* è posizionato sopra il livello di rete. Questo livello è responsabile della gestione del flusso di dati tra gli host nella rete. Sono disponibili due tipi di servizi di trasporto supportati da NetX: UDP e TCP. I servizi UDP garantiscono l'invio e la ricezione dei dati tra due host senza connessione, mentre TCP fornisce un servizio affidabile orientato alla connessione tra due entità host.

Questo livello viene riflesso nei pacchetti di dati di rete effettivi. Ogni livello in TCP/IP contiene un blocco di informazioni denominato intestazione. Questa tecnica relativa ai dati circostanti (e possibilmente alle informazioni sul protocollo) con un'intestazione viene in genere chiamata incapsulamento dei dati. Nella figura 1 viene illustrato un esempio di NetX layering e la figura 2 Mostra l'incapsulamento dei dati risultante per i dati UDP inviati.

![Layering del protocollo](./media/user-guide/protocol-layering.png)

**FIGURA 1. Layering del protocollo**

![Incapsulamento dei dati UDP](./media/user-guide/udp-data-encapsulation.png)

**FIGURA 2. Incapsulamento dei dati UDP**

## <a name="packet-pools"></a>Pool di pacchetti

L'allocazione di pacchetti in modo rapido e deterministico è sempre una sfida nelle applicazioni di rete in tempo reale. Tenendo presente questo aspetto, NetX offre la possibilità di creare e gestire più pool di pacchetti di rete a dimensione fissa.

Poiché i pool di pacchetti NetX sono costituiti da blocchi di memoria a dimensione fissa, non si verificano mai problemi di frammentazione interna. Naturalmente, la frammentazione causa comportamenti intrinsecamente non deterministici.

Inoltre, il tempo necessario per allocare e liberare un pacchetto NetX equivale a una semplice manipolazione di elenchi collegati. Inoltre, l'allocazione e la deallocazione dei pacchetti vengono eseguite all'inizio dell'elenco disponibile. In questo modo si fornisce l'elaborazione dell'elenco collegato più veloce possibile.

La mancanza di flessibilità è in genere lo svantaggio principale dei pool di pacchetti a dimensione fissa. Determinare le dimensioni del payload dei pacchetti ottimali che gestiscono anche il pacchetto in ingresso peggiore è un'attività difficile. I pacchetti NetX affrontano questo problema con una funzionalità facoltativa denominata *concatenamento dei pacchetti*. Un pacchetto di rete effettivo può essere composto da uno o più pacchetti NetX collegati tra loro. Inoltre, l'intestazione del pacchetto mantiene un puntatore all'inizio del pacchetto. Quando vengono aggiunti altri protocolli, questo puntatore viene semplicemente spostato all'indietro e la nuova intestazione viene scritta direttamente davanti ai dati. Senza la tecnologia flessibile dei pacchetti, lo stack dovrebbe allocare un altro buffer e copiare i dati in un nuovo buffer con la nuova intestazione, che sta elaborando in modo intensivo.

Poiché le dimensioni del payload del pacchetto sono fisse per un determinato pool di pacchetti, i dati dell'applicazione di dimensioni maggiori rispetto alle dimensioni del payload richiedono la concatenazione di più pacchetti. Quando si compila un pacchetto con dati utente, l'applicazione deve utilizzare il servizio ***nx_packet_data_append***. Questo servizio sposta i dati dell'applicazione in un pacchetto. Nei casi in cui un pacchetto non è sufficiente per contenere i dati utente, vengono allocati pacchetti aggiuntivi per archiviare i dati utente. Per utilizzare il concatenamento dei pacchetti, il driver deve essere in grado di ricevere o trasmettere da pacchetti concatenati.

Ogni pool di memoria del pacchetto NetX è una risorsa pubblica. NetX non impone vincoli sul modo in cui vengono utilizzati i pool di pacchetti.

### <a name="packet-pool-memory-area"></a>Area memoria pool di pacchetti
L'area di memoria per il pool di pacchetti viene specificata durante la creazione. Analogamente ad altre aree di memoria per gli oggetti ThreadX e NetX, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione. Si tratta di una funzionalità importante grazie alla notevole flessibilità offerta dall'applicazione. Si supponga, ad esempio, che un prodotto di comunicazione disponga di un'area di memoria ad alta velocità per i buffer di rete. Questa area di memoria è facilmente utilizzabile rendendola in un pool di memoria pacchetti NetX.

### <a name="creating-packet-pools"></a>Creazione di pool di pacchetti
I pool di pacchetti vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Non sono previsti limiti per il numero di pool di memoria pacchetti in un'applicazione NetX.

### <a name="packet-header-nx_packet"></a>NX_PACKET intestazione pacchetto
Per impostazione predefinita, NetX inserisce l'intestazione del pacchetto immediatamente prima dell'area del payload del pacchetto. Il pool di memoria pacchetti è fondamentalmente una serie di pacchetti, ovvero le intestazioni seguite immediatamente dal payload del pacchetto. L'intestazione del pacchetto (***NX_PACKET***) e il layout del pool di pacchetti sono illustrati nella figura 3.

Per i driver dei dispositivi di rete che sono in grado di eseguire zero operazioni di copia, in genere l'indirizzo iniziale dell'area del payload del pacchetto viene programmato nella logica DMA. Alcuni motori DMA hanno requisiti di allineamento nell'area del payload.

> [!IMPORTANT]
> * È necessario che il driver di rete chiami la funzione ***nx_packet_transmit_release** _ al termine della trasmissione di un pacchetto. Questa funzione verifica che il pacchetto non faccia parte di una coda di output TCP prima che venga effettivamente inserito nel pool disponibile. La mancata chiamata di questa funzione può comportare behavior._ imprevedibili

![Layout dell'intestazione e del pool di pacchetti](./media/user-guide/packet-header-packet-pool-layout.png)

**FIGURA 3. Layout dell'intestazione e del pool di pacchetti**

I campi dell'intestazione del pacchetto vengono definiti come illustrato nella tabella seguente. Si noti che questa tabella non è un elenco completo di tutti i membri della struttura *NX_PACKET* .

| Intestazione pacchetto          | Scopo                                                                                                                                                                                                                                                                                                                            |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *nx_packet_pool_owner*   | Questo campo fa riferimento al pool di pacchetti proprietario del pacchetto specifico. Quando il pacchetto viene rilasciato, viene rilasciato a questo particolare pool. Con la proprietà del pool all'interno di ogni pacchetto, è possibile che un datagramma si estenda su più pacchetti da più pool di pacchetti.                                                         |
| *nx_packet_next*         | Questo campo fa riferimento al pacchetto successivo all'interno dello stesso frame. Se è NULL, non sono presenti pacchetti aggiuntivi che fanno parte del frame. |
| *nx_packet_last*         | Questo campo punta all'ultimo pacchetto all'interno dello stesso pacchetto di rete. Se NULL, questo pacchetto rappresenta l'intero pacchetto di rete.  |
| *nx_packet_length*       | Questo campo contiene il numero totale di byte nell'intero pacchetto di rete, incluso il totale di tutti i byte in tutti i pacchetti concatenati dal membro *nx_packet_next* . |
| *nx_packet_ip_interface* | Questo campo è il blocco di controllo dell'interfaccia che viene assegnato al pacchetto quando viene ricevuto dal driver di interfaccia e da NetX per i pacchetti in uscita. Un blocco di controllo dell'interfaccia descrive l'interfaccia, ad esempio l'indirizzo di rete, l'indirizzo MAC, l'indirizzo IP e lo stato dell'interfaccia, ad esempio collegamento abilitato e mapping fisico obbligatorio. |
| *nx_packet_data_start*   | Questo campo punta all'inizio dell'area del payload fisico del pacchetto. Non è necessario che si trovi immediatamente dopo l'intestazione NX_PACKET, ma è l'impostazione predefinita per il servizio ***nx_packet_pool_create*** . |
| *nx_packet_data_end*     | Questo campo punta alla fine dell'area del payload fisico del pacchetto. La differenza tra questo campo e il campo nx_packet_data_start rappresenta le dimensioni del payload. |
| *nx_packet_prepend_ptr*  | Questo campo fa riferimento alla posizione in cui vengono aggiunti i dati dei pacchetti, ovvero l'intestazione del protocollo o i dati effettivi, davanti ai dati dei pacchetti esistenti (se presenti) nell'area del payload del pacchetto. Deve essere maggiore o uguale alla posizione del puntatore *nx_packet_data_start* e minore o uguale al puntatore di *nx_packet_append_ptr* .  *Per motivi di prestazioni, NetX presuppone che, quando il pacchetto viene passato nei servizi NetX per la trasmissione, il puntatore anteposto punti all'indirizzo allineato a parole lunghe.* |
| *nx_packet_append_ptr*    | Questo campo punta alla fine dei dati attualmente presenti nell'area del payload del pacchetto. Deve trovarsi tra la posizione di memoria a cui punta *nx_packet_prepend_ptr* e *nx_packet_data_end*. La differenza tra questo campo e il campo *nx_packet_prepend_ptr* rappresenta la quantità di dati in questo pacchetto. |
| *nx_packet_fragment_next* | Questo campo viene utilizzato per contenere pacchetti frammentati fino a quando non è possibile riassemblare l'intero pacchetto. |
| *nx_packet_pad*           | Questo campo definisce la lunghezza del riempimento in parole a 4 byte per ottenere il requisito di allineamento desiderato. Questo campo viene rimosso se *NX_PACKET_HEADER_PAD* non è definito. |
|  |  |

### <a name="packet-header-offsets"></a>Offset dell'intestazione del pacchetto

Le dimensioni dell'intestazione del pacchetto sono definite in modo da consentire spazio sufficiente per contenere le dimensioni dell'intestazione. Il servizio *nx_packet_allocate* viene utilizzato per allocare un pacchetto e per regolare il puntatore anteposto nel pacchetto in base al tipo di pacchetto specificato. Il tipo di pacchetto indica a NetX l'offset necessario per inserire l'intestazione del protocollo, ad esempio UDP, TCP o ICMP, davanti ai dati del protocollo.

I tipi seguenti sono definiti in NetX per prendere in considerazione l'intestazione IP e l'intestazione del livello fisico (Ethernet) nel pacchetto. Nel secondo caso, si presuppone che sia 16 byte tenendo in considerazione l'allineamento richiesto di 4 byte. I pacchetti IP sono ancora definiti in NetX per le applicazioni per l'allocazione di pacchetti per le reti IP. La tabella seguente illustra i simboli definiti:

| Tipo di pacchetto   | Valore |
|---------------|-------|
| NX_IP_PACKET  | 0x24  |
| NX_UDP_PACKET | 0x2c  |
| NX_TCP_PACKET | 0x38  |
|               |       |

### <a name="pool-capacity"></a>Capacità pool
Il numero di pacchetti in un pool di pacchetti è una funzione delle dimensioni del payload e il numero totale di byte nell'area di memoria fornita al servizio di creazione del pool di pacchetti. La capacità del pool viene calcolata dividendo le dimensioni del pacchetto (incluse le dimensioni dell'intestazione NX_PACKET, le dimensioni del payload e l'allineamento appropriato) nel numero totale di byte nell'area di memoria specificata.

### <a name="thread-suspension"></a>Sospensione thread
I thread dell'applicazione possono sospendere l'attesa di un pacchetto da un pool vuoto. Quando un pacchetto viene restituito al pool, al thread sospeso viene assegnato questo pacchetto e ripreso.

Se più thread vengono sospesi nello stesso pool di pacchetti, vengono ripresi nell'ordine in cui sono stati sospesi (FIFO).

### <a name="pool-statistics-and-errors"></a>Statistiche ed errori del pool
Se abilitata, gli **errori** software di gestione pacchetti di NETX tengono traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per i pool di pacchetti vengono mantenute le statistiche e i report degli errori seguenti:

* Totale pacchetti nel pool
* Pacchetti disponibili nel pool
* Richieste di allocazione vuote del pool
* Sospensioni di allocazione vuote del pool
* Versioni di pacchetti non valide

Tutte le statistiche e le segnalazioni degli errori, ad eccezione del numero totale e dei pacchetti gratuiti nel pool, sono incorporate nella libreria NetX a meno che non sia definito ***NX_DISABLE_PACKET_INFO** _. Questi dati sono disponibili per l'applicazione con il servizio _ *_nx_packet_pool_info_get_**.

### <a name="packet-pool-control-block-nx_packet_pool"></a>Blocco di controllo del pool di pacchetti NX_PACKET_POOL

Le caratteristiche di ogni pool di memoria dei pacchetti sono disponibili nel relativo blocco di controllo. Contiene informazioni utili, ad esempio l'elenco collegato di pacchetti gratuiti, il numero di pacchetti disponibili e le dimensioni del payload per i pacchetti in questo pool. Questa struttura viene definita nel file *nx_api. h* .

I blocchi di controllo del pool di pacchetti possono trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione.

## <a name="ip-protocol"></a>Protocollo IP

Il componente IP (Internet Protocol) di NetX è responsabile dell'invio e della ricezione di pacchetti IP in Internet. In NetX, è il componente responsabile dell'invio e della ricezione di messaggi TCP, UDP, ICMP e IGMP, usando il driver di rete sottostante.

NetX supporta il protocollo IP (RFC 791)

### <a name="ip-addresses"></a>Indirizzi IP

Ogni host su Internet dispone di un identificatore univoco a 32 bit denominato indirizzo IP. Sono disponibili cinque classi di indirizzi IP, come illustrato nella figura 4. Gli intervalli delle cinque classi di indirizzi IP sono i seguenti:

| Classe | Range                        |
|-------|------------------------------|
| A     | da 0.0.0.0 a 127.255.255.255   |
| B     | da 128.0.0.0 a 191.255.255.255 |
| C     | da 192.0.0.0 a 223.255.255.255 |
| D     | da 224.0.0.0 a 239.255.255.255 |
| E     | da 240.0.0.0 a 247.255.255.255 |

**7 bit a 24 bit**

![Struttura degli indirizzi IP](./media/user-guide/ip-address-structure.png)

**FIGURA 4. Struttura degli indirizzi IP**

Sono disponibili anche tre tipi di specifiche degli indirizzi: *unicast*, *broadcast* e *multicast*. Gli indirizzi unicast sono gli indirizzi IP che identificano un host specifico su Internet. Gli indirizzi unicast possono essere un indirizzo IP di origine o di destinazione. Un indirizzo di trasmissione identifica tutti gli host in una rete o una subnet specifica e può essere utilizzato solo come indirizzi di destinazione. Gli indirizzi broadcast vengono specificati con la parte dell'ID host dell'indirizzo impostato su uno. Indirizzi multicast (classe D) specificare un gruppo dinamico di host su Internet. I membri del gruppo multicast possono partecipare e lasciare ogni volta che desiderano.

> [!IMPORTANT]
> *Solo i protocolli senza connessione come UDP su IP possono utilizzare la trasmissione e la funzionalità di broadcast limitata del gruppo multicast.*

> [!IMPORTANT]
> *La macro* Ip_address *è definito in*  * **nx_api. h** _. Consente di specificare facilmente gli indirizzi IP usando le virgole anziché i punti. Ad esempio, IP_ADDRESS (128, 0, 0, 0) _specifies il primo indirizzo della classe B illustrato nella figura 4. *

### <a name="ip-gateway-address"></a>Indirizzo IP gateway

I gateway di rete assistono gli host sulle proprie reti per inoltrare pacchetti destinati a destinazioni esterne al dominio locale. Ogni nodo ha una certa conoscenza dell'hop successivo da inviare a, ovvero la destinazione di uno degli elementi adiacenti o tramite una tabella di routing statica preprogrammata. Tuttavia, se questi approcci hanno esito negativo, il nodo deve inoltrare il pacchetto al gateway predefinito, con ulteriori informazioni su come instradare il pacchetto alla relativa destinazione. Si noti che il gateway predefinito deve essere direttamente accessibile tramite una delle interfacce fisiche collegate all'istanza IP. L'applicazione chiama ***nx_ip_gateway_address_set*** per configurare l'indirizzo IP del gateway predefinito.

### <a name="ip-header"></a>Intestazione IP

Per ogni pacchetto IP da inviare su Internet, deve avere un'intestazione IP. Quando protocolli di livello superiore (UDP, TCP, ICMP o IGMP) chiamano il componente IP per inviare un pacchetto, il modulo trasmissione IP inserisce un'intestazione IP davanti ai dati. Viceversa, quando i pacchetti IP vengono ricevuti dalla rete, il componente IP rimuove l'intestazione IP dal pacchetto prima del recapito ai protocolli di livello superiore. La figura 5 Mostra il formato dell'intestazione IP.

![Formato intestazione IP](./media/user-guide/ip-header-format.png)

**FIGURA 5. Formato intestazione IP**

> [!IMPORTANT]
> *È previsto che tutte le intestazioni nell'implementazione TCP/IP siano in formato big endian. In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso. Ad esempio, la versione a 4 bit e la lunghezza dell'intestazione a 4 bit dell'intestazione IP devono trovarsi sul primo byte dell'intestazione.*

I campi dell'intestazione IP sono definiti come segue:

**Scopo campo intestazione IP**

***versione a 4 bit*** Questo campo contiene la versione di IP rappresentata da questa intestazione. Per IP versione 4, che è il supporto di NetX, il valore di questo campo è 4.

***lunghezza intestazione a 4 bit*** Questo campo specifica il numero di parole a 32 bit nell'intestazione IP. Se non sono presenti parole di opzione, il valore per questo campo è 5.

***tipo di servizio (TOS) a 8 bit*** Questo campo specifica il tipo di servizio richiesto per il pacchetto IP. Le richieste valide sono le seguenti:

| **Richiesta TOS**     | **Valore** |
| ------------------- | --------- |
| Normale              | 0x00      |
| Ritardo minimo       | 0x10      |
| Numero massimo di dati        | 0x08      |
| Affidabilità massima | 0x04      |
| Costo minimo        | 0x02      |

***lunghezza totale a 16 bit*** Questo campo contiene la lunghezza totale del datagramma IP in byte, inclusa l'intestazione IP. Un datagramma IP è l'unità di base delle informazioni disponibili in una rete Internet TCP/IP. Contiene un indirizzo di origine e di destinazione oltre ai dati. Poiché si tratta di un campo a 16 bit, le dimensioni massime di un datagramma IP sono pari a 65.535 byte.

***identificazione a 16 bit*** Il campo è un numero usato per identificare in modo univoco ogni datagramma IP inviato da un host. Questo numero viene in genere incrementato dopo l'invio di un datagramma IP. È particolarmente utile per assemblare frammenti di pacchetti IP ricevuti.

***flag a 3 bit*** Questo campo contiene informazioni sulla frammentazione IP. Il bit 14 è il bit "not Fragment". Se questo bit è impostato, il datagramma IP in uscita non verrà frammentato. Il bit 13 è il bit "More Fragments". Se questo bit è impostato, sono presenti più frammenti. Se questo bit è chiaro, questo è l'ultimo frammento del pacchetto IP.

**Scopo campo intestazione IP**

***offset frammento a 13 bit*** Questo campo contiene i 13 bit superiori dell'offset del frammento. Per questo motivo, gli offset dei frammenti sono consentiti solo su limiti di 8 byte. Il primo frammento di un datagramma IP frammentato avrà un set di bit "più frammenti" e un offset pari a 0.

***durata (TTL) a 8 bit*** Questo campo contiene il numero di router che possono essere superati dal datagramma, che limita la durata del datagramma.

***protocollo a 8 bit*** Questo campo specifica il protocollo che usa il datagramma IP. Di seguito è riportato un elenco di protocolli validi e dei relativi valori:

| Protocollo | Valore |
|----------|-------|
| ICMP     | 0x01  |
| IGMP     | 0x02  |
| TCP      | 0X06  |
| UDP      | 0X11  |
|          |       |


***checksum a 16 bit*** Questo campo contiene il checksum a 16 bit che copre solo l'intestazione IP. Nei protocolli di livello superiore sono presenti checksum aggiuntivi che coprono il payload IP.

***indirizzo IP di origine a 32 bit*** Questo campo contiene l'indirizzo IP del mittente ed è sempre un indirizzo host.

***indirizzo IP di destinazione a 32 bit*** Questo campo contiene l'indirizzo IP del destinatario o dei ricevitori se l'indirizzo è un indirizzo broadcast o multicast.

### <a name="creating-ip-instances"></a>Creazione di istanze IP

Le istanze IP vengono create durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. L'indirizzo IP iniziale, network mask, il pool di pacchetti predefinito, il driver multimediale e la memoria e la priorità del thread IP interno sono definiti dal servizio *nx_ip_create* . Se l'applicazione Inizializza l'istanza IP con il relativo indirizzo IP impostato su un indirizzo non valido (0.0.0.0), si presuppone che l'indirizzo dell'interfaccia venga risolto dalla configurazione manuale in un secondo momento, tramite RARP o tramite DHCP o protocolli simili.

Per i sistemi con più interfacce di rete, l'interfaccia principale viene designata quando si chiama *nx_ip_create*. Ogni interfaccia aggiuntiva può essere collegata alla stessa istanza IP chiamando *nx_ip_interface_attach*. Questo servizio archivia informazioni sull'interfaccia di rete (ad esempio indirizzo IP, network mask) nel blocco di controllo dell'interfaccia e associa l'istanza del driver al blocco di controllo dell'interfaccia nell'istanza IP. Quando il driver riceve un pacchetto di dati, deve archiviare le informazioni sull'interfaccia nella struttura NX_PACKET prima di inoltrarle alla logica di ricezione IP. Nota è necessario che un'istanza IP sia già stata creata prima di eseguire il fissaggio di qualsiasi interfaccia.

 ### <a name="ip-send"></a>Invio IP
 L'elaborazione dell'invio IP in NetX è molto semplificata.

Il puntatore anteposto nel pacchetto viene spostato all'indietro per contenere l'intestazione IP. L'intestazione IP viene completata (con tutte le opzioni specificate dal livello del protocollo chiamante), il checksum IP viene calcolato in linea e il pacchetto viene inviato al driver di rete associato. Inoltre, la frammentazione in uscita è coordinata anche all'interno dell'elaborazione di trasmissione IP.

Per IP, NetX avvia le richieste ARP se è necessario il mapping fisico per l'indirizzo IP di destinazione.

> [!IMPORTANT]
> *Per la connettività IP, i pacchetti che richiedono la risoluzione degli indirizzi IP (ad esempio, il mapping fisico) vengono accodati nella coda ARP finché il numero di pacchetti in coda non supera la profondità della coda ARP (definita dal* *simbolo **NX_ARP_MAX_QUEUE_DEPTH**). Se* *viene raggiunta la profondità della coda, NETX rimuoverà il pacchetto meno recente nella coda e continuerà ad attendere la risoluzione degli indirizzi per i pacchetti rimanenti accodati. D'altra parte, se non viene risolta una voce ARP, i pacchetti in sospeso sulla voce ARP vengono rilasciati al timeout della voce ARP.*

Per i sistemi con più interfacce di rete, NetX sceglie un'interfaccia basata sull'indirizzo IP di destinazione. La procedura seguente si applica al processo di selezione:

1. Se un indirizzo di destinazione è broadcast IP o multicast e se è specificata un'interfaccia in uscita valida, utilizzare tale interfaccia. In caso contrario, viene utilizzata la prima interfaccia fisica.

2. Se l'indirizzo di destinazione viene trovato nella tabella di routing statica, viene utilizzata l'interfaccia associata al gateway.

3. Se la destinazione è on-link, viene utilizzata l'interfaccia di collegamento.

4. Se l'indirizzo di destinazione è un indirizzo di loopback 127.0.0.1, viene utilizzata l'interfaccia di loopback.

5. Se il gateway predefinito è configurato correttamente, usare l'interfaccia associata al gateway predefinito per trasmettere il pacchetto.

6. Il pacchetto di output viene eliminato se non si verificano errori.

### <a name="ip-receive"></a>Ricezione IP

L'elaborazione di ricezione IP viene chiamata dal driver di rete o dal thread IP interno (per l'elaborazione dei pacchetti nella coda di pacchetti ricevuta posticipata). L'elaborazione di ricezione IP esamina il campo protocollo e tenta di inviare il pacchetto al componente protocollo appropriato. Prima che il pacchetto venga effettivamente inviato, l'intestazione IP viene rimossa facendo avanzare il puntatore anteposto oltre l'intestazione IP.

L'elaborazione della ricezione IP rileva inoltre i pacchetti IP frammentati ed esegue i passaggi necessari per riassemblarli se la frammentazione è abilitata. Se la frammentazione è necessaria ma non abilitata, il pacchetto viene eliminato.

NetX determina l'interfaccia di rete appropriata in base all'interfaccia specificata nel pacchetto. Se l'interfaccia del pacchetto è NULL, l'impostazione predefinita di NetX è l'interfaccia primaria. Questa operazione viene eseguita per garantire la compatibilità con i driver Ethernet NetX legacy.

### <a name="raw-ip-send"></a>Invio IP non elaborato

Un pacchetto IP non elaborato è un frame IP che contiene il payload del protocollo di livello superiore non direttamente supportato ed elaborato da NetX. Un pacchetto non elaborato consente agli sviluppatori di definire le proprie applicazioni basate su IP. Un'applicazione può inviare pacchetti IP non elaborati direttamente usando il servizio ***nx_ip_raw_packet_send** _ se l'elaborazione di pacchetti IP non elaborati è stata abilitata con il servizio di _*_nx_ip_raw_packet_enabled_*_ . Se l'indirizzo di destinazione è un indirizzo multicast o broadcast, tuttavia, NetX per impostazione predefinita è la prima interfaccia (primaria). Pertanto, per inviare tali pacchetti alle interfacce secondarie, l'applicazione deve usare il servizio _ *_nx_ip_raw_packet_interface_send_** per specificare l'indirizzo di origine da usare per il pacchetto in uscita.

### <a name="raw-ip-receive"></a>Ricezione di indirizzi IP non elaborati

Se l'elaborazione dei pacchetti IP non elaborati è abilitata, l'applicazione può ricevere pacchetti IP non elaborati tramite il servizio ***nx_ip_raw_packet_receive** _. Tutti i pacchetti in ingresso vengono elaborati in base al protocollo specificato nell'intestazione IP. Se il protocollo specifica UDP, TCP, IGMP o ICMP, NetX elaborerà il pacchetto utilizzando il gestore appropriato per il tipo di protocollo del pacchetto. Se il protocollo non è uno di questi protocolli e la ricezione di indirizzi IP non elaborati è abilitata, il pacchetto in arrivo verrà inserito nella coda dei pacchetti non elaborati in attesa che l'applicazione la riceva tramite il servizio _ *_nx_ip_raw_packet_receive_**. I thread dell'applicazione possono inoltre sospendere con un timeout facoltativo durante l'attesa di un pacchetto IP non elaborato.

### <a name="default-packet-pool"></a>Pool di pacchetti predefinito

A ogni istanza IP viene assegnato un pool di pacchetti predefinito durante la creazione. Questo pool di pacchetti viene usato per allocare pacchetti per ARP, RARP, ICMP, IGMP, diversi pacchetti di controllo TCP (ad esempio SYN, ACK). Se il pool di pacchetti predefinito è vuoto quando NetX deve allocare un pacchetto, NetX potrebbe dover interrompere l'operazione specifica e restituirà un messaggio di errore, se possibile.

### <a name="ip-helper-thread"></a>Thread helper IP

Ogni istanza IP ha un thread helper. Questo thread è responsabile della gestione di tutte le operazioni di elaborazione dei pacchetti posticipate e di tutte le elaborazioni periodiche. Il thread helper IP viene creato in ***nx_ip_create.*** Questo è il punto in cui al thread viene assegnato lo stack e la priorità. Si noti che la prima elaborazione nel thread helper IP consiste nel completare l'inizializzazione del driver di rete associata al servizio di creazione IP. Al termine dell'inizializzazione del driver di rete, il thread di supporto avvia un ciclo infinito per elaborare le richieste periodiche e del pacchetto.

> [!IMPORTANT]
> *Se si verifica un comportamento inspiegabile all'interno del thread helper IP, l'aumento delle dimensioni dello stack durante il servizio di creazione IP è il primo passaggio di debug. Se lo stack è troppo piccolo, il thread helper IP potrebbe probabilmente sovrascrivere la memoria, che potrebbe causare problemi insoliti.*

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono sospendere il tentativo di ricevere pacchetti IP non elaborati. Dopo la ricezione di un pacchetto non elaborato, il nuovo pacchetto viene assegnato al primo thread sospeso e il thread viene ripreso. I servizi NetX per la ricezione di pacchetti hanno tutti un timeout di sospensione facoltativo. Quando viene ricevuto un pacchetto o il timeout scade, il thread dell'applicazione viene ripreso con lo stato di completamento appropriato.

### <a name="ip-statistics-and-errors"></a>Statistiche IP ed errori

Se abilitata, il NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per ogni istanza IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale pacchetti IP inviati
- Totale byte IP inviati
- Totale pacchetti IP ricevuti
- Totale byte IP ricevuti
- Totale pacchetti IP non validi
- Totale pacchetti di ricezione IP eliminati
- Totale errori di checksum di ricezione IP
- Totale pacchetti di invio IP eliminati
- Totale frammenti IP inviati
- Totale frammenti IP ricevuti

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_ip_info_get*** .

### <a name="ip-control-block-nx_ip"></a>NX_IP del blocco di controllo IP

Le caratteristiche di ogni istanza IP si trovano nel relativo blocco di controllo. Contiene informazioni utili quali gli indirizzi IP e le maschere di rete di ogni dispositivo di rete e una tabella di indirizzi IP adiacenti e mapping di indirizzi hardware fisici. Questa struttura è definita nei blocchi di controllo dell'istanza IP del ***nx_api. h*** può trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendolo al di fuori dell'ambito di qualsiasi funzione.

### <a name="static-ip-routing"></a>Routing IP statico

La funzionalità di routing statico consente a un'applicazione di specificare una rete IP e l'indirizzo hop successivo per indirizzi IP di destinazione specifici fuori rete. Se il routing statico è abilitato, NetX Cerca nella tabella di routing statica una voce corrispondente all'indirizzo di destinazione del pacchetto da inviare. Se non viene trovata alcuna corrispondenza, NetX esegue la ricerca nell'elenco di interfacce fisiche e sceglie un indirizzo IP di origine e un indirizzo hop successivo in base all'indirizzo IP di destinazione e al network mask. Se la destinazione non corrisponde ad alcuno degli indirizzi IP dei driver di rete collegati all'istanza IP, NetX sceglie un'interfaccia connessa direttamente al gateway predefinito e usa l'indirizzo IP dell'interfaccia come indirizzo di origine e il gateway predefinito come hop successivo.

Le voci possono essere aggiunte e rimosse dalla tabella di routing statica usando rispettivamente i servizi ***nx_ip_static_route_add*** e ***nx_ip_static_route_delete** _. Per usare il routing statico, l'applicazione host deve abilitare questa funzionalità definendo _ *_NX_ENABLE_IP_STATIC_ROUTING_*. *

> [!IMPORTANT]
> *Quando si aggiunge una voce alla tabella di routing statica, NetX verifica la presenza di una voce corrispondente per l'indirizzo di destinazione specificato già nella tabella. Se ne esiste uno, fornisce la preferenza alla voce con la rete più piccola (prefisso più lungo) nell'network mask.*

### <a name="ip-fragmentation"></a>Frammentazione IP

Il dispositivo di rete potrebbe avere limiti per le dimensioni dei pacchetti in uscita. Questo limite è denominato MTU (Maximum Transmission Unit). MTU IP è la dimensione massima del frame IP che un driver del livello di collegamento è in grado di trasmettere senza frammentazione del pacchetto IP. Durante la fase di inizializzazione di un driver di dispositivo, il modulo driver deve configurare le dimensioni MTU IP tramite il servizio ***nx_ip_interface_mtu_set**. *

Sebbene non sia consigliabile, l'applicazione può generare datagrammi di dimensioni superiori rispetto alla MTU IP sottostante supportata dal dispositivo. Prima di trasmettere tale datagramma IP, il livello IP deve frammentare questi pacchetti. Alla ricezione di frame IP frammentati, l'estremità ricevente deve archiviare tutti i frame IP frammentati con lo stesso ID di frammentazione e riassemblarli nell'ordine. Se la logica di ricezione IP non è in grado di raccogliere tutti i frammenti per ripristinare il frame IP originale nel tempo, vengono rilasciati tutti i frammenti. È il protocollo di livello superiore per rilevare tale perdita di pacchetti e ripristinarla.

Per supportare la frammentazione IP e l'operazione di riassemblaggio, progettazione sistema deve abilitare la funzionalità di frammentazione IP in NetX usando il servizio ***nx_ip_fragment_enable*** . Se questa funzionalità non è abilitata, i pacchetti IP frammentati in ingresso vengono eliminati, oltre a pacchetti che superano il MTU del driver di rete.

> [!IMPORTANT]
> *La logica di frammentazione IP può essere rimossa completamente definendo*  * **NX_DISABLE_FRAGMENTATION** _ _when la compilazione della libreria theNetX. Questa operazione consente di ridurre le dimensioni del codice di NetX. *

## <a name="address-resolution-protocol-arp-in-ip"></a>ARP (Address Resolution Protocol) nell'IP

Il protocollo ARP (Address Resolution Protocol) è responsabile del mapping dinamico degli indirizzi IP a 32 bit a quelli del supporto fisico sottostante (RFC 826). Ethernet è il supporto fisico più comune e supporta gli indirizzi a 48 bit. La necessità di ARP è determinata dal driver di rete fornito al servizio ***nx_ip_create*** . Se è necessario un mapping fisico, il driver di rete deve impostare il flag ***nx_interface_address_mapping_needed*** nell'interfaccia strcuture.

### <a name="arp-enable"></a>Abilitazione ARP
Per il corretto funzionamento di ARP, l'applicazione deve prima essere abilitata dall'applicazione con il servizio ***nx_arp_enable*** . Questo servizio configura varie strutture di dati per l'elaborazione ARP, inclusa la creazione di un'area della cache ARP dalla memoria fornita al servizio di abilitazione ARP.

### <a name="arp-cache"></a>Cache ARP
La cache ARP può essere visualizzata come una matrice di strutture di dati di mapping ARP interne. Ogni struttura interna è in grado di gestire la relazione tra un indirizzo IP e un indirizzo hardware fisico. Ogni struttura di dati dispone inoltre di puntatori di collegamento, in modo che possa essere parte di più elenchi collegati.

L'applicazione può cercare un indirizzo IP dalla cache ARP specificando l'indirizzo MAC hardware usando il servizio ***nx_arp_ip_address_find** _ se il mapping esiste nella tabella ARP. Analogamente, il servizio _ *_nx_arp_hardware_address_find_** restituisce l'indirizzo Mac per un determinato indirizzo IP.


### <a name="arp-dynamic-entries"></a>Voci dinamiche ARP

Per impostazione predefinita, il servizio ARP Enable inserisce tutte le voci della cache ARP nell'elenco delle voci ARP dinamiche disponibili. Una voce ARP dinamica viene allocata da questo elenco NetX quando viene rilevata una richiesta di invio a un indirizzo IP non mappato. Dopo l'allocazione, la voce ARP viene configurata e viene inviata una richiesta ARP al supporto fisico.

È possibile creare una voce dinamica anche dal servizio ***nx_arp_dynamic_entry_set***.

> [!IMPORTANT]
> *Se tutte le voci ARP dinamiche sono in uso, la voce ARP usata meno di recente viene sostituita con un nuovo mapping.*

### <a name="arp-static-entries"></a>Voci statiche ARP
L'applicazione può anche impostare il mapping ARP statico usando il servizio ***nx_arp_static_entry_create*** . Questo servizio alloca una voce ARP dall'elenco di voci ARP dinamiche e la inserisce nell'elenco statico con le informazioni di mapping fornite dall'applicazione. Le voci ARP statiche non sono soggette a riutilizzo o invecchiamento. L'applicazione può eliminare una voce statica utilizzando il servizio ***nx_arp_static_entry_delete***.
Per rimuovere tutte le voci statiche nella tabella ARP, è possibile che l'applicazione utilizzi il ***nx_arp_static_entries_delete*** di servizio.

### <a name="automatic-arp-entry"></a>Voce ARP automatica
NetX registra il mapping IP/MAC del peer dopo le risposte del peer alla richiesta ARP. NetX implementa anche la funzionalità di immissione automatica di ARP in cui registra il mapping degli indirizzi IP/MAC peer in base alle richieste ARP non richieste dalla rete. Questa funzionalità consente di popolare la tabella ARP con le informazioni sul peer, riducendo il ritardo necessario per il ciclo di richiesta/risposta ARP. Tuttavia, il lato negativo dell'abilitazione di ARP automatico è che la tabella ARP tende a riempirsi rapidamente in una rete occupata con molti nodi sul collegamento locale, il che porterebbe alla sostituzione della voce ARP.

Questa funzionalità è abilitata per impostazione predefinita. Per disabilitarla, è necessario compilare la libreria NetX con il simbolo ***NX_DISABLE_ARP_AUTO_ENTRY*** definito.

### <a name="arp-messages"></a>Messaggi ARP

Come indicato in precedenza, viene inviato un messaggio di richiesta ARP quando l'attività IP rileva che il mapping è necessario per un indirizzo IP. Le richieste ARP vengono inviate periodicamente (ogni ***NX_ARP_UPDATE_RATE** _ secondi) finché non viene ricevuta una risposta ARP corrispondente. Viene eseguito un totale di _ *_NX_ARP_MAXIMUM_RETRIES_** richieste ARP prima che il tentativo ARP venga abbandonato. Quando viene ricevuta una risposta ARP, le informazioni sull'indirizzo fisico associate vengono archiviate nella voce ARP presente nella cache.

Per i sistemi multihome, NetX determina quale interfaccia inviare le richieste e le risposte ARP in base all'indirizzo di destinazione specificato.

> [!IMPORTANT]
> *I pacchetti IP in uscita vengono accodati mentre NETX attende la risposta ARP. Il numero di pacchetti IP in uscita* *accodati viene definito dalla costante*  * **NX_ARP_MAX_QUEUE_DEPTH**. *

NetX risponde anche alle richieste ARP da altri nodi nella rete IP locale. Quando viene effettuata una richiesta ARP esterna che corrisponde all'indirizzo IP corrente dell'interfaccia che riceve la richiesta ARP, NetX compila un messaggio di risposta ARP che contiene l'indirizzo fisico corrente.

I formati delle richieste e delle risposte ARP Ethernet sono illustrati nella figura 6 e sono descritti di seguito:

| Campo richiesta/risposta       | Scopo    |
|------------------------------|-----------------|
| Indirizzo di destinazione Ethernet | Questo campo di 6 byte contiene l'indirizzo di destinazione per la risposta ARP ed è un broadcast (tutti) per le richieste ARP. Questo campo viene configurato dal driver di rete. |
| Indirizzo di origine Ethernet      | Questo campo di 6 byte contiene l'indirizzo del mittente della richiesta o della risposta ARP e viene configurato dal driver di rete. |
| Tipo di frame                   | Questo campo a 2 byte contiene il tipo di frame Ethernet presente e, per le richieste e le risposte ARP, è uguale a 0x0806. Questo è l'ultimo campo che il driver di rete è responsabile della configurazione. |
| Tipo di hardware                | Questo campo a 2 byte contiene il tipo di hardware, ovvero 0x0001 per Ethernet. |
| Tipo di protocollo                | Questo campo a 2 byte contiene il tipo di protocollo, ovvero 0x0800 per gli indirizzi IP. |
| Dimensioni hardware                | Questo campo a 1 byte contiene le dimensioni degli indirizzi hardware, ovvero 6 per gli indirizzi Ethernet. |


![Formato del pacchetto ARP](./media/user-guide/arp-packet-format.png)

**FIGURA 6. Formato del pacchetto ARP**

| Campo richiesta/risposta | Scopo  |
|---|---|
| Dimensioni protocollo | Questo campo a 1 byte contiene le dimensioni dell'indirizzo IP, ovvero 4 per gli indirizzi IP.  |
| Codice operativo | Questo campo a 2 byte contiene l'operazione per questo pacchetto ARP. Una richiesta ARP viene specificata con il valore di 0x0001, mentre una risposta ARP viene rappresentata da un valore di 0x0002.  |
| Indirizzo Ethernet mittente | Questo campo a 6 byte contiene l'indirizzo Ethernet del mittente. |
| Indirizzo IP mittente | Questo campo a 4 byte contiene l'indirizzo IP del mittente. |
| Indirizzo Ethernet di destinazione | Questo campo a 6 byte contiene l'indirizzo Ethernet della destinazione. |
| Indirizzo IP di destinazione | Questo campo a 4 byte contiene l'indirizzo IP della destinazione. |

> [!IMPORTANT]
> *Le richieste e le risposte ARP sono pacchetti a livello Ethernet. Tutti gli altri pacchetti TCP/IP sono incapsulati da un'intestazione del pacchetto IP.*

> [!IMPORTANT]
> *È previsto che tutti i messaggi ARP nell'implementazione TCP/IP siano in formato big endian. In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

### <a name="arp-aging"></a>Durata ARP

NetX supporta l'invalidamento automatico della voce ARP dinamica. ***NX_ARP_EXPIRATION_RATE** _specifies il numero di secondi per cui un indirizzo IP stabilito al mapping fisico rimane valido. Dopo la scadenza, la voce ARP viene rimossa dalla cache ARP. Il tentativo successivo di inviare all'indirizzo IP corrispondente comporterà una nuova richiesta ARP. Impostando _ *_NX_ARP_EXPIRATION_RATE_** su zero, viene disabilitata la durata ARP, che è la configurazione predefinita.

### <a name="arp-defend"></a>Difesa ARP

Quando viene ricevuta una richiesta ARP o un pacchetto di risposta ARP e il mittente ha lo stesso indirizzo IP, che è in conflitto con l'indirizzo IP del nodo, NetX invia una richiesta ARP per tale indirizzo come difesa. Se il pacchetto ARP dei conflitti viene ricevuto più di una volta in 10 secondi, NetX non invia più pacchetti di difesa. L'intervallo predefinito di 10 secondi può essere ridefinito da ***NX_ARP_DEFEND_INTERVAL** _. Questo comportamento segue i criteri specificati in 2.4 (c) di RFC5227. Poiché Windows XP ignora l'annuncio ARP come risposta per il probe ARP, l'utente può definire _ *_NX_ARP_DEFEND_BY_REPLY_* * per inviare la risposta ARP come difesa aggiuntiva.

### <a name="arp-statistics-and-errors"></a>Statistiche ed errori ARP

Se abilitata, il software ARP NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per l'elaborazione ARP di ogni IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale richieste ARP inviate
- Totale richieste ARP ricevute
- Totale risposte ARP inviate
- Totale risposte ARP ricevute
- Totale voci dinamiche ARP
- Totale voci statiche ARP
- Totale voci ARP obsolete
- Totale messaggi ARP non validi

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_arp_info_get*** .

## <a name="reverse-address-resolution-protocol-rarp-in-ip"></a>Protocollo RARP (Reverse Address Resolution Protocol) nell'IP

Il protocollo RARP (inverso Address Resolution Protocol) è il protocollo per la richiesta di assegnazione di rete degli indirizzi IP a 32 bit dell'host (RFC 903). Questa operazione viene eseguita tramite una richiesta RARP e continua periodicamente finché un membro di rete non assegna un indirizzo IP all'interfaccia di rete host in una risposta RARP. L'applicazione crea un'istanza IP dal servizio ***nx_ip_create*** con un indirizzo IP zero. Se RARP è abilitato dall'applicazione, può usare il protocollo RARP per richiedere un indirizzo IP dal server di rete accessibile tramite l'interfaccia con un indirizzo IP zero.

### <a name="rarp-enable"></a>Abilitazione di RARP

Per usare RARP, l'applicazione deve creare l'istanza IP con un indirizzo IP pari a zero, quindi abilitare RARP usando il servizio ***nx_rarp_enable***. Per i sistemi multihome, almeno un dispositivo di rete associato all'istanza IP deve avere un indirizzo IP uguale a zero. L'elaborazione di RARP invia periodicamente messaggi di richiesta RARP per il sistema NetX che richiedono un indirizzo IP fino a quando non viene ricevuta una risposta RARP valida con l'indirizzo IP di rete designato. A questo punto, l'elaborazione di RARP è stata completata.

Dopo l'abilitazione di RARP, questo viene disabilitato automaticamente dopo la risoluzione di tutti gli indirizzi di interfaccia. L'applicazione può forzare l'interruzione di RARP utilizzando il servizio ***nx_rarp_disable***.

###  <a name="rarp-request"></a>Richiesta RARP

Il formato di un pacchetto di richiesta RARP è quasi identico al pacchetto ARP illustrato nella figura 6 nell'argomento [messaggi ARP](#arp-messages). L'unica differenza è che il campo tipo di frame è 0x8035 e il campo del *codice operativo* è 3, che designa una richiesta RARP. Come indicato in precedenza, le richieste RARP verranno inviate periodicamente (ogni ***NX_RARP_UPDATE_RATE*** secondi) finché non viene ricevuta una risposta RARP con l'indirizzo IP assegnato alla rete.

> [!IMPORTANT]
> *È previsto che tutti i messaggi RARP nell'implementazione TCP/IP siano in formato big endian. In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

### <a name="rarp-reply"></a>Risposta RARP

I messaggi di risposta RARP vengono ricevuti dalla rete e contengono l'indirizzo IP assegnato alla rete per questo host. Il formato di un pacchetto di risposta RARP è quasi identico al pacchetto ARP illustrato nella figura 6. L'unica differenza è che il campo tipo di frame è 0x8035 e il campo del *codice operativo* è 4, che definisce una risposta RARP. Dopo la ricezione, l'indirizzo IP viene configurato nell'istanza IP, la richiesta di RARP periodica è disabilitata e l'istanza IP è ora pronta per le normali operazioni di rete.

Per gli host multihomed, l'indirizzo IP viene applicato all'interfaccia di rete richiedente. Se sono presenti altre interfacce di rete che richiedono ancora un'assegnazione di indirizzi IP, il servizio di RARP periodico continua fino a quando non vengono risolte tutte le richieste di indirizzi IP dell'interfaccia.

> [!IMPORTANT]
> *L'applicazione non deve usare l'istanza IP fino al completamento dell'elaborazione di RARP. Il **nx_ip_status_check** può essere utilizzato dalle applicazioni per attendere il completamento del RARP. Per i sistemi multihome, l'applicazione non deve usare l'interfaccia richiedente fino al completamento dell'elaborazione di RARP su tale interfaccia. È possibile controllare lo stato dell'indirizzo IP nel dispositivo secondario con il servizio **nx_ip_interface_status_check** .*

### <a name="rarp-statistics-and-errors"></a>Statistiche ed errori di RARP

Se abilitata, il software NetX RARP tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per l'elaborazione RARP di ogni IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale richieste RARP inviate
- Totale risposte RARP ricevute
- Totale messaggi non validi RARP

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_rarp_info_get*** .

## <a name="internet-control-message-protocol-icmp"></a>Internet Control Message Protocol (ICMP)

Internet Control Message Protocol per IP (ICMP) è limitato al passaggio delle informazioni sugli errori e sul controllo tra i membri della rete IP.

Come per la maggior parte degli altri messaggi di livello applicazione (ad esempio TCP/IP), i messaggi ICMP sono incapsulati da un'intestazione IP con la designazione del protocollo ICMP.

### <a name="icmp-statistics-and-errors"></a>Statistiche ed errori ICMP

Se abilitata, NetX tiene traccia di diversi errori e statistiche ICMP che possono risultare utili per l'applicazione. Per l'elaborazione ICMP di ogni IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale ping ICMP inviati
- Timeout totali ping ICMP
- Totale thread ping ICMP sospesi
- Totale risposte ping ICMP ricevute
- Totale errori di checksum ICMP
- Totale messaggi non gestiti ICMP

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_icmp_info_get*** .

### <a name="icmp-enable"></a>Abilita ICMP
Prima che i messaggi ICMP possano essere elaborati da NetX, l'applicazione deve chiamare il servizio ***nx_icmp_enable*** per abilitare l'elaborazione ICMP. Al termine di questa operazione, l'applicazione può emettere richieste ping e i pacchetti ping in ingresso del campo.

### <a name="icmp-echo-request"></a>Richiesta echo ICMP
Una richiesta echo è un tipo di messaggio ICMP usato in genere per verificare l'esistenza di un nodo specifico nella rete, come identificato dall'indirizzo IP dell'host. Il popolare comando ping viene implementato utilizzando i messaggi ICMP Echo Request/Echo Reply. Se l'host specifico è presente, lo stack di rete elabora la richiesta e le risposte ping con una risposta ping. Figura 7 dettagli del formato del messaggio ping ICMP.

![Messaggio ping ICMP](./media/user-guide/icmp-ping-message.png)

**FIGURA 7. Messaggio ping ICMP**

> [!IMPORTANT]
> *È previsto che tutti i messaggi ICMP nell'implementazione TCP/IP siano in formato big endian. In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

Nella tabella seguente viene descritto il formato di intestazione ICMP:

| Campo di intestazione    | Scopo |
|-----------------|---------------------------------------------------|
| Tipo            | Questo campo specifica il messaggio ICMP (BITS 31-24). Le più comuni sono: 0 Echo Reply 8 richiesta echo |
| Codice            | Questo campo è specifico del contesto nel campo del tipo (BITS 23-16). Per una richiesta o una risposta echo il codice è impostato su zero. |
| Checksum        | Questo campo contiene il checksum a 16 bit della somma di complemento a uno del messaggio ICMP, inclusa l'intera intestazione ICMP che inizia con il campo tipo. Prima di generare il checksum, il campo checksum viene cancellato.                 |
| Identification  | Questo campo contiene un valore ID che identifica l'host. un host deve usare l'ID Estratto da una richiesta ECHO nella risposta ECHO (BITS 31-16). |
| Numero di sequenza | Questo campo contiene un valore ID. un host deve usare l'ID Estratto da una richiesta ECHO nella risposta ECHO (BITS 31-16). Diversamente dal campo identificatore, questo valore verrà modificato in una richiesta echo successiva dallo stesso host (BITS 15-0). |


### <a name="icmp-echo-response"></a>Risposta echo ICMP
Una risposta ping è un altro tipo di messaggio ICMP generato internamente dal componente ICMP in risposta a una richiesta ping esterna. Oltre al riconoscimento, la risposta ping contiene anche una copia dei dati utente forniti nella richiesta ping.

## <a name="internet-group-management-protocol-igmp"></a>IGMP (Internet Group Management Protocol)

Il protocollo IGMP (Internet Group Management Protocol) fornisce un dispositivo per comunicare con gli elementi adiacenti e i relativi router che intende ricevere o aggiungere un gruppo multicast IP (RFC 1112 e RFC 2236). Un gruppo multicast è essenzialmente una raccolta dinamica di membri di rete ed è rappresentato da un indirizzo IP di classe D. I membri del gruppo multicast possono uscire in qualsiasi momento e i nuovi membri possono partecipare in qualsiasi momento. Il coordinamento necessario per l'aggiunta e l'uscita del gruppo è la responsabilità di IGMP.

### <a name="igmp-enable"></a>Abilitazione IGMP

Prima che qualsiasi attività multicast possa essere eseguita in NetX, l'applicazione deve chiamare il servizio ***nx_igmp_enable*** . Questo servizio esegue l'inizializzazione IGMP di base per la preparazione delle richieste multicast.

### <a name="multicast-ip-addressing"></a>Indirizzi IP multicast

Come indicato in precedenza, gli indirizzi multicast sono effettivamente di classe D indirizzi IP, come illustrato nella figura 4 nella pagina 58. I 28 bit inferiori dell'indirizzo della classe D corrispondono all'ID del gruppo multicast. Sono disponibili una serie di indirizzi multicast predefiniti. Tuttavia, l' *Indirizzo All Hosts* (244.0.0.1) è particolarmente importante per l'elaborazione IGMP. L' *indirizzo tutti gli host* viene usato dai router per eseguire una query su tutti i membri multicast per segnalare i gruppi multicast a cui appartengono.

### <a name="physical-address-mapping-in-ip"></a>Mapping degli indirizzi fisici nell'IP

Gli indirizzi multicast della classe D vengono mappati direttamente agli indirizzi Ethernet fisici compresi tra 01.00.5 e 00.00.00 tramite 01.00.5 e 7F. FF. FF. I 23 bit inferiori della mappa indirizzi IP multicast direttamente ai 23 bit inferiori dell'indirizzo Ethernet.

### <a name="multicast-group-join"></a>Join gruppo multicast

Le applicazioni che devono partecipare a un particolare gruppo multicast possono eseguire questa operazione chiamando il servizio ***nx_igmp_multicast_join*** . Questo servizio tiene traccia del numero di richieste da unire in join a questo gruppo multicast. Se si tratta della prima richiesta dell'applicazione per l'aggiunta al gruppo multicast, viene inviato un report IGMP sulla rete primaria indicante che l'intenzione dell'host è partecipare al gruppo. Successivamente, il driver di rete viene chiamato per configurare per l'ascolto dei pacchetti con l'indirizzo Ethernet per questo gruppo multicast.

In un sistema multihome, se il gruppo multicast è accessibile tramite un'interfaccia specifica, l'applicazione deve utilizzare il ***nx_igmp_multicast_interface_join*** di servizio anziché ***nx_igmp_multicast_join**, * che è limitato ai gruppi multicast nella rete primaria.

### <a name="multicast-group-leave"></a>Uscita gruppo multicast

Le applicazioni che devono lasciare un gruppo multicast precedentemente aggiunto possono eseguire questa operazione chiamando il servizio ***nx_igmp_multicast_leave*** . Questo servizio riduce il numero interno associato al numero di volte in cui è stato aggiunto il gruppo. Se non sono presenti richieste di join in attesa per un gruppo, il driver di rete viene chiamato per disabilitare l'ascolto dei pacchetti con l'indirizzo Ethernet del gruppo multicast

### <a name="multicast-loopback"></a>Loopback multicast

Un'applicazione potrebbe voler ricevere il traffico multicast originato da una delle origini nello stesso nodo. A questo scopo, il componente multicast IP deve avere il loopback abilitato utilizzando il servizio ***nx_igmp_loopback_enable***.

### <a name="igmp-report-message"></a>Messaggio report IGMP

Quando l'applicazione viene aggiunta a un gruppo multicast, viene inviato un messaggio di report IGMP tramite la rete per indicare che l'intenzione dell'host deve essere aggiunta a un particolare gruppo multicast. Il formato del messaggio del report IGMP è illustrato nella figura 8. L'indirizzo del gruppo multicast viene utilizzato sia per il messaggio di gruppo nel messaggio del report IGMP che per l'indirizzo IP di destinazione.

![Messaggio report IGMP](./media/user-guide/igmp-report-message.png)

**FIGURA 8. Messaggio report IGMP**

Nella figura precedente (Figura 8), l'intestazione IGMP contiene un campo versione/tipo, il tempo di risposta massimo, un campo di checksum e un campo dell'indirizzo del gruppo multicast. Per i messaggi IGMPv1, il campo tempi di risposta massimi è sempre impostato su zero, perché non fa parte del protocollo IGMPv1. Il campo tempo di risposta massimo viene impostato quando l'host riceve un messaggio IGMP di tipo query e viene cancellato quando un host riceve il messaggio del tipo di report di un altro host come definito dal protocollo IGMPv2.

Di seguito viene descritto il formato di intestazione IGMP:

| **Campo di intestazione**          | **Scopo** |
|-----------------------|--------------------------------------------------------------------|
| Versione               | Questo campo specifica la versione IGMP (BITS 31-28).                                                                               |
| Tipo                  | Questo campo specifica il tipo di messaggio IGMP (BITS 27 -24).                                                                       |
| Tempo di risposta massimo | Non utilizzato in IGMPv1. In IGMPv2 questo campo funge da tempo di risposta massimo.                                                      |
| Checksum              | Questo campo contiene il checksum a 16 bit della somma del complemento a uno del messaggio IGMP che inizia con la versione IGMP (BITS 0-15) |
| Indirizzo del gruppo         | Indirizzo IP del gruppo di classe D a 32 bit |


I messaggi di report IGMP vengono inviati anche in risposta ai messaggi di query IGMP inviati da un router multicast. I router multicast inviano periodicamente messaggi di query per vedere quali host richiedono ancora l'appartenenza al gruppo. I messaggi di query hanno lo stesso formato del messaggio di report IGMP illustrato nella figura 8. Le uniche differenze sono il tipo IGMP è uguale a 1 e il campo Indirizzo gruppo è impostato su 0. I messaggi di query IGMP vengono inviati all'indirizzo IP *tutti gli host* dal router multicast. Un host che desidera comunque mantenere l'appartenenza al gruppo risponde inviando un altro messaggio di report IGMP.

> [!IMPORTANT]
> *È previsto che tutti i messaggi nell'implementazione TCP/IP siano in formato **Big Endian** . In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

### <a name="igmp-statistics-and-errors"></a>Statistiche ed errori IGMP

Se abilitata, il software IGMP NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per l'elaborazione IGMP di ogni IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale report IGMP inviati
- Totale query IGMP ricevute
- Totale errori di checksum IGMP
- Totale gruppi correnti IGMP aggiunti

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_igmp_info_get*** .

## <a name="user-datagram-protocol-udp"></a>UDP (User Datagram Protocol)

Il protocollo UDP (User Datagram Protocol) fornisce la forma più semplice di trasferimento dei dati tra i membri di rete (RFC 768). I pacchetti di dati UDP vengono inviati da un membro di rete a un altro nel modo migliore possibile. ovvero, non esiste alcun meccanismo incorporato per il riconoscimento da parte del destinatario del pacchetto. Inoltre, per l'invio di un pacchetto UDP non è necessario stabilire alcuna connessione in anticipo. Per questo motivo, la trasmissione dei pacchetti UDP è molto efficiente.

### <a name="udp-header"></a>Intestazione UDP
UDP posiziona una semplice intestazione del pacchetto davanti ai dati dell'applicazione durante la trasmissione e rimuove un'intestazione UDP simile dal pacchetto alla ricezione prima di consegnare un pacchetto UDP ricevuto all'applicazione. UDP usa il protocollo IP per l'invio e la ricezione di pacchetti, ovvero è presente un'intestazione IP davanti all'intestazione UDP quando il pacchetto si trova nella rete. Nella figura 9 è illustrato il formato dell'intestazione UDP.

![Intestazione UDP](./media/user-guide/udp-header.png)

**FIGURA 9. Intestazione UDP**

> [!IMPORTANT]
> *È previsto che tutte le intestazioni nell'implementazione di UDP/IP siano in formato big endian. In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

Di seguito viene descritto il formato dell'intestazione UDP:

| Campo di intestazione                   | Scopo |
|--------------------------------|---------------------------------------------|
| numero di porta di origine a 16 bit      | Questo campo contiene la porta da cui viene inviato il pacchetto UDP. Le porte UDP valide sono comprese tra 1 e 0xFFFF. |
| numero porta di destinazione a 16 bit | Questo campo contiene la porta UDP a cui viene inviato il pacchetto. Le porte UDP valide sono comprese tra 1 e 0xFFFF.   |
| lunghezza UDP a 16 bit   | Questo campo contiene il numero di byte nel pacchetto UDP, incluse le dimensioni dell'intestazione UDP.                                  |
| checksum UDP a 16 bit | Questo campo contiene il checksum a 16 bit per il pacchetto, tra cui l'intestazione UDP, l'area dati del pacchetto e l'intestazione pseudo-IP. |

### <a name="udp-enable"></a>Abilita UDP

Prima che sia possibile la trasmissione di pacchetti UDP, l'applicazione deve prima abilitare UDP chiamando il servizio ***nx_udp_enable*** . Dopo l'abilitazione, l'applicazione è gratuita per inviare e ricevere pacchetti UDP.

### <a name="udp-socket-create"></a>Creazione socket UDP

I socket UDP vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Il tipo di servizio, la durata (TTL) e la profondità della coda di ricezione specificati sono definiti dal servizio ***nx_udp_socket_create*** . Non sono previsti limiti per il numero di socket UDP in un'applicazione.

### <a name="udp-checksum"></a>Checksum UDP

UDP specifica un checksum a 16 bit a complemento di uno che copre la pseudo intestazione IP (costituita dall'indirizzo IP di origine, indirizzo IP di destinazione e la parola IP di protocollo/lunghezza), l'intestazione UDP e i dati del pacchetto UDP. Se il checksum UDP calcolato è 0, viene archiviato come tutti i valori (0xFFFF). Se per il socket di invio è disabilitata la logica di checksum UDP, nel campo checksum UDP viene inserito uno zero per indicare che il checksum non è stato calcolato. Se il checksum UDP non corrisponde al checksum calcolato dal ricevitore, il pacchetto UDP viene semplicemente ignorato.

Nella rete IP, il checksum UDP è facoltativo. NetX consente a un'applicazione di abilitare o disabilitare il calcolo del checksum UDP per singolo socket. Per impostazione predefinita, la logica di checksum del socket UDP è abilitata. L'applicazione può disabilitare la logica di checksum per un particolare socket UDP chiamando il servizio ***nx_udp_socket_checksum_disable*** .

Alcuni controller Ethernet sono in grado di generare rapidamente il checksum UDP. Se il sistema è in grado di utilizzare la funzionalità di calcolo di checksum hardware, la libreria NetX può essere compilata senza la logica di checksum. Per disabilitare il checksum del software UDP, è necessario compilare la libreria NetX con i simboli seguenti definiti: ***NX_DISABLE_UDP_TX_CHECKSUM*** e ***NX_DISABLE_UDP_RX_CHECKSUM **_ (descritto nel [capitolo 2](chapter2.md)). Le opzioni di configurazione rimuovono completamente la logica di checksum UDP da NetX, durante la chiamata del servizio _* nx_udp_socket_checksum_disable*** consente all'applicazione di disabilitare l'elaborazione del checksum UDP IP in base a ogni socket.

### <a name="udp-ports-and-binding"></a>Porte e binding UDP

Una porta UDP è un endpoint logico nel protocollo UDP. Nel componente UDP di NetX sono presenti 65.535 porte valide, comprese tra 1 e 0xFFFF. Per inviare o ricevere dati UDP, l'applicazione deve prima creare un socket UDP, quindi associarlo a una porta desiderata. Dopo aver associato un socket UDP a una porta, l'applicazione può inviare e ricevere dati su tale socket.

### <a name="udp-fast-pathtrade"></a>Percorso veloce UDP&trade;

Il percorso veloce UDP &trade; è il nome di un percorso di overhead dei pacchetti basso tramite l'implementazione UDP di NETX. L'invio di un pacchetto UDP richiede solo alcune chiamate di funzione: ***nx_udp_socket_send** _, _*_nx_ip_packet_send_*_ e la chiamata finale al driver di rete. _*_nx_udp_socket_send_*_ è disponibile in NETX per le applicazioni NETX esistenti ed è applicabile solo ai pacchetti IP. Il metodo preferito, tuttavia, consiste nell'usare _ *_nx_udp_socket_send_** servizio descritto di seguito. Nella ricezione di pacchetti UDP, il pacchetto UDP viene inserito nella coda di ricezione socket UDP appropriata o recapitato a un thread dell'applicazione sospesa in una singola chiamata di funzione dall'elaborazione dell'interrupt di ricezione del driver di rete. Questa logica altamente ottimizzata per l'invio e la ricezione di pacchetti UDP è l'essenza della tecnologia di percorso veloce UDP.

### <a name="udp-packet-send"></a>Invio pacchetti UDP

L'invio di dati UDP su reti IP viene eseguito facilmente chiamando la funzione ***nx_udp_socket_send** _. Il chiamante deve impostare la versione IP nel campo _IP Address *. NetX determinerà l'indirizzo di origine migliore per i pacchetti UDP trasmessi in base all'indirizzo IP di destinazione. Questo servizio posiziona un'intestazione UDP davanti ai dati del pacchetto e la invia alla rete usando una routine di invio IP interna. Non vi è alcuna sospensione di thread per l'invio di pacchetti UDP perché tutte le trasmissioni di pacchetti UDP vengono elaborate immediatamente.

Per le destinazioni multicast o broadcast, l'applicazione deve specificare l'indirizzo IP di origine da usare se il dispositivo NetX dispone di più indirizzi IP tra cui scegliere. Questa operazione può essere eseguita con i servizi ***nx_udp_socket_interface_send.***

> [!IMPORTANT]
> *Se **nx_udp_socket_send** viene usato per la trasmissione di pacchetti broadcast o multicast, l'indirizzo IP della prima interfaccia viene usato come indirizzo di origine.*

> [!IMPORTANT]
> *Se per questo socket è abilitata la logica di checksum UDP, l'operazione di checksum viene eseguita nel contesto del thread chiamante, senza bloccare l'accesso alle strutture di dati UDP o IP.*

> [!NOTE]
> *I dati di payload UDP che risiedono nella struttura di **NX_PACKET** devono trovarsi su un confine di parola lungo. L'applicazione deve lasciare spazio sufficiente tra il puntatore anteposto e il puntatore di avvio dati per NetX per inserire le intestazioni dei supporti UDP, IP e fisici.*

### <a name="udp-packet-receive"></a>Ricezione pacchetti UDP

I thread dell'applicazione possono ricevere pacchetti UDP da un socket particolare chiamando ***nx_udp_socket_receive***. La funzione di ricezione socket recapita il pacchetto meno recente nella coda di ricezione del socket. Se non sono presenti pacchetti nella coda di ricezione, il thread chiamante può sospendere (con un timeout facoltativo) finché non arriva un pacchetto.

L'elaborazione dei pacchetti di ricezione UDP (in genere chiamata dal gestore di interrupt di ricezione del driver di rete) è responsabile del posizionamento del pacchetto nella coda di ricezione del socket UDP o del recapito al primo thread sospeso in attesa di un pacchetto. Se il pacchetto viene accodato, l'elaborazione della ricezione controlla anche la profondità massima della coda di ricezione associata al socket. Se il pacchetto appena accodato supera la profondità della coda, il pacchetto meno recente nella coda viene eliminato.

### <a name="udp-receive-notify"></a>Ricezione notifica UDP

Se il thread dell'applicazione deve elaborare i dati ricevuti da più di un socket, è necessario usare la funzione ***nx_udp_socket_receive_notify*** . Questa funzione registra una funzione di callback del pacchetto di ricezione per il socket. Ogni volta che viene ricevuto un pacchetto nel socket, viene eseguita la funzione di callback.

Il contenuto della funzione di callback è specifico dell'applicazione. Tuttavia, sarebbe più probabile che contengano la logica per informare il thread di elaborazione che un pacchetto è ora disponibile nel socket corrispondente.

### <a name="peer-address-and-port"></a>Indirizzo e porta peer

Alla ricezione di un pacchetto UDP, l'applicazione può trovare l'indirizzo IP e il numero di porta del mittente usando il ***nx_udp_packet_info_extract*** del servizio. In seguito all'esito positivo, questo servizio fornisce informazioni sull'indirizzo IP del mittente, sul numero di porta del mittente e sull'interfaccia locale tramite cui è stato ricevuto il pacchetto.

### <a name="thread-suspension"></a>Sospensione thread

Come indicato in precedenza, i thread dell'applicazione possono sospendere il tentativo di ricezione di un pacchetto UDP su una determinata porta UDP. Dopo la ricezione di un pacchetto su tale porta, questo viene assegnato al primo thread sospeso e il thread viene quindi ripreso. Un timeout facoltativo è disponibile quando si sospende un pacchetto di ricezione UDP, una funzionalità disponibile per la maggior parte dei servizi NetX.

### <a name="udp-socket-statistics-and-errors"></a>Statistiche ed errori di socket UDP

Se abilitata, il software socket UDP NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per ogni istanza IP/UDP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale pacchetti UDP inviati
- Totale byte UDP inviati
- Totale pacchetti UDP ricevuti
- Totale byte UDP ricevuti
- Totale pacchetti UDP non validi
- Totale pacchetti di ricezione UDP eliminati
- Totale errori di checksum di ricezione UDP
- Pacchetti socket UDP inviati
- Byte socket UDP inviati
- Pacchetti socket UDP ricevuti
- Byte socket UDP ricevuti
- Pacchetti socket UDP in coda
- Pacchetti di ricezione socket UDP eliminati
- Errori di checksum del socket UDP

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_udp_info_get*** per le statistiche UDP accumulate su tutti i socket UDP e il servizio ***nx_udp_socket_info_get*** per le statistiche UDP sul socket UDP specificato.

### <a name="udp-socket-control-block-nx_udp_socket"></a>NX_UDP_SOCKET blocco di controllo socket UDP

Le caratteristiche di ogni socket UDP si trovano nel blocco di controllo **NX_UDP_SOCKET** associato. Contiene informazioni utili, ad esempio il collegamento alla struttura dei dati IP, l'interfaccia di rete per i percorsi di invio e ricezione, la porta associata e la coda dei pacchetti di ricezione. Questa struttura viene definita nel file **_nx_api. h_** .

## <a name="transmission-control-protocol-tcp"></a>Transmission Control Protocol (TCP)

Il Transmission Control Protocol (TCP) fornisce un trasferimento dei dati di flusso affidabile tra due membri di rete (RFC 793). Tutti i dati inviati da un membro della rete vengono verificati e riconosciuti dal membro di destinazione. Inoltre, i due membri devono avere stabilito una connessione prima del trasferimento dei dati. Il risultato è il trasferimento affidabile dei dati; Tuttavia, richiede un sovraccarico sostanziale rispetto al trasferimento dei dati UDP descritto in precedenza.

### <a name="tcp-header"></a>Intestazione TCP

Sulla trasmissione, l'intestazione TCP viene posizionata davanti ai dati dell'utente. Alla ricezione, l'intestazione TCP viene rimossa dal pacchetto in ingresso, lasciando solo i dati utente disponibili per l'applicazione. TCP utilizza il protocollo IP per inviare e ricevere pacchetti, ovvero è presente un'intestazione IP davanti all'intestazione TCP quando il pacchetto si trova nella rete. Nella figura 10 è illustrato il formato dell'intestazione TCP.

![Intestazione TCP](./media/user-guide/tcp-header.png)

**FIGURA 10. Intestazione TCP**

Di seguito viene descritto il formato dell'intestazione TCP:

| Campo di intestazione | Scopo |
|---|---|
| numero di porta di origine a 16 bit | Questo campo contiene la porta a cui viene inviato il pacchetto TCP. Le porte TCP valide sono comprese tra 1 e 0xFFFF. |
| numero porta di destinazione a 16 bit | Questo campo contiene la porta TCP a cui viene inviato il pacchetto. Le porte TCP valide sono comprese tra 1 e 0xFFFF. |
| numero di sequenza a 32 bit | Questo campo contiene il numero di sequenza per i dati inviati da questa entità finale della connessione. La sequenza originale viene stabilita durante la sequenza di connessione iniziale tra due nodi TCP. Ogni trasferimento di dati da tale punto genera un incremento del numero di sequenza in base alla quantità di byte inviati. |
| numero di riconoscimento a 32 bit | Questo campo contiene il numero di sequenza corrispondente all'ultimo byte ricevuto da questo lato della connessione. Viene utilizzato per determinare se i dati inviati in precedenza sono stati ricevuti correttamente dall'altra entità finale della connessione. |
| lunghezza intestazione a 4 bit           | Questo campo contiene il numero di parole a 32 bit nell'intestazione TCP. Se nell'intestazione TCP non è presente alcuna opzione, il campo è 5. |
| bit di codice a 6 bit               | Questo campo contiene i sei bit di codice diversi usati per indicare le varie informazioni di controllo associate alla connessione. I bit del controllo vengono definiti come segue: |



| Nome | bit | Significato                                                     |
|------|-----|-------------------------------------------------------------|
| URG  | 21  | Dati urgenti presenti                                         |
| ACK  | 20  | Il numero di riconoscimento è valido                             |
| PSH  | 19  | Gestisci immediatamente questi dati                                |
| RST  | 18  | Reimposta la connessione                                        |
| SYN  | 17  | Sincronizzare i numeri di sequenza (usati per stabilire la connessione) |
| FIN  | 16  | Il mittente è terminato con la trasmissione (usata per chiudere la connessione) |

**finestra a 16 bit**

Questo campo viene usato per il controllo di flusso. Contiene la quantità di byte che il socket può attualmente ricevere. Questo viene essenzialmente usato per il controllo di flusso. Il mittente è responsabile di assicurarsi che i dati da inviare vengano inseriti nella finestra annunciata del destinatario.

| **Campo di intestazione**          | **Scopo** |
| ------------------------- | --- |
| **checksum TCP a 16 bit**   | Questo campo contiene il checksum a 16 bit per il pacchetto, tra cui l'intestazione TCP, l'area dati del pacchetto e l'intestazione pseudo-IP.                |
| **Puntatore urgente a 16 bit** | Questo campo contiene l'offset positivo dell'ultimo byte dei dati urgenti. Questo campo è valido solo se il bit di codice URG è impostato nell'intestazione. |

> [!IMPORTANT]
> *È previsto che tutte le intestazioni nell'implementazione TCP/IP siano in formato big endian. In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

### <a name="tcp-enable"></a>Abilitazione TCP

Prima che le connessioni TCP e le trasmissioni di pacchetti siano possibili, l'applicazione deve prima abilitare TCP chiamando il servizio nx_tcp_enable. Dopo l'abilitazione, l'applicazione è gratuita per accedere a tutti i servizi TCP.

### <a name="tcp-socket-create"></a>Creazione socket TCP

I socket TCP vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Il tipo di servizio, la durata (TTL) e le dimensioni della finestra sono definiti dal servizio ***nx_tcp_socket_create*** . Non sono previsti limiti per il numero di socket TCP in un'applicazione.

### <a name="tcp-checksum"></a>Checksum TCP

TCP specifica un checksum a 16 bit a complemento di uno che copre la pseudo intestazione IP, costituita dall'indirizzo IP di origine, dall'indirizzo IP di destinazione e dalla parola IP di protocollo/lunghezza, l'intestazione TCP e i dati del pacchetto TCP.

Alcuni controller di rete sono in grado di eseguire il calcolo e la convalida del checksum TCP nell'hardware. Per tali sistemi, le applicazioni potrebbero voler usare la logica di checksum hardware il più possibile per ridurre il sovraccarico di Runtime. Le applicazioni possono disabilitare completamente la logica di calcolo del checksum TCP dalla libreria NetX in fase di compilazione definendo **NX_DISABLE_TCP_TX_CHECKSUM** e **NX_DISABLE_TCP_RX_CHECKSUM**. In questo modo, il codice di checksum TCP non viene compilato in.

### <a name="tcp-port"></a>Porta TCP

Una porta TCP è un punto di connessione logico nel protocollo TCP. Nel componente TCP di NetX sono presenti 65.535 porte valide, comprese tra 1 e 0xFFFF. Diversamente da UDP, in cui i dati di una porta possono essere inviati a qualsiasi altra porta di destinazione, una porta TCP è connessa a un'altra porta TCP specifica e solo quando viene stabilita la connessione può essere effettuato il trasferimento dei dati, e solo tra le due porte che costituiscono la connessione.

> [!IMPORTANT]
> *Le porte TCP sono completamente separate dalle porte UDP; ad esempio, la porta UDP numero 1 non ha alcuna relazione con la porta TCP numero 1.*

## <a name="client-server-model"></a>Modello di Client-Server

Per usare TCP per il trasferimento dei dati, è prima necessario stabilire una connessione tra i due socket TCP. La creazione della connessione viene eseguita in modalità client-server. Il lato client della connessione è il lato che avvia la connessione, mentre il lato server è semplicemente in attesa delle richieste di connessione client prima che venga eseguita qualsiasi elaborazione.

> [!IMPORTANT]
> *Per i dispositivi multihome, NetX determina automaticamente l'indirizzo di origine da usare per la connessione e l'indirizzo hop successivo in base all'indirizzo IP di destinazione della connessione.*

### <a name="tcp-socket-state-machine"></a>Macchina a stati socket TCP

La connessione tra due socket TCP (un client e un server) è complessa e viene gestita in modo analogo a una macchina a Stati. Ogni socket TCP viene avviato in uno stato chiuso. Tramite gli eventi di connessione viene eseguita la migrazione della macchina a stati di ogni socket nello stato stabilito, ovvero la posizione in cui viene eseguita la maggior parte del trasferimento dei dati in TCP. Quando un lato della connessione non desidera più inviare dati, si disconnette. Dopo la disconnessione dell'altro lato, il socket TCP torna allo stato CLOSED. Questo processo viene ripetuto ogni volta che un client e un server TCP stabiliscono e chiudono una connessione. La figura 11 Mostra i vari Stati della macchina a stati TCP.

![Stati della macchina a stati TCP](./media/user-guide/states-tcp-state-machine.png)

### <a name="figure-11-states-of-the-tcp-state-machine"></a>FIGURA 11. Stati della macchina a stati TCP

### <a name="tcp-client-connection"></a>Connessione client TCP

Come indicato in precedenza, il lato client della connessione TCP avvia una richiesta di connessione a un server TCP. Prima di poter effettuare una richiesta di connessione, è necessario abilitare il protocollo TCP nell'istanza IP del client. Inoltre, il socket TCP del client deve essere creato successivamente con il servizio ***nx_tcp_socket_create** _ e associato a una porta tramite il servizio _*_nx_tcp_client_socket_bind_*_ . Dopo aver associato il socket client, il servizio _ *_nx_tcp_client_socket_connect_** viene usato per stabilire una connessione con un server TCP. Si noti che il socket deve trovarsi in uno stato chiuso per avviare un tentativo di connessione. Stabilire la connessione inizia con NetX che emette un pacchetto SYN e quindi attende un pacchetto SYN ACK dal server, che indica l'accettazione della richiesta di connessione. Dopo la ricezione dell'ACK SYN, NetX risponde con un pacchetto ACK e promuove lo stato stabilito del socket client.

### <a name="tcp-client-disconnection"></a>Disconnessione del client TCP

La chiusura della connessione viene eseguita chiamando ***nx_tcp_socket_disconnect***. Se non viene specificata alcuna sospensione, il socket client invia un pacchetto RST al socket del server e posiziona il socket nello stato CLOSED. In caso contrario, se viene richiesta una sospensione, viene eseguito il protocollo di disconnessione TCP completo, come indicato di seguito:

- Se il server ha avviato in precedenza una richiesta di disconnessione (il socket client ha già ricevuto un pacchetto FIN, ha risposto con un ACK ed è nello stato di attesa di chiusura), NetX promuove lo stato del socket TCP del client all'ultimo stato ACK e invia un pacchetto FIN. Attende quindi un ACK dal server prima di completare la disconnessione e di entrare nello stato CLOSED.

- Se invece il client è il primo ad avviare una richiesta di disconnessione (il server non si è disconnesso e il socket si trova ancora nello stato stabilito), NetX Invia un pacchetto FIN per avviare la disconnessione e attende la ricezione di una pinna e di un ACK dal server prima di completare la disconnessione e di collocare il socket in uno stato chiuso.

Se nella coda di trasmissione del socket sono ancora presenti pacchetti, NetX sospende il timeout specificato per consentire la conferma dei pacchetti. Se il timeout scade, NetX svuota la coda di trasmissione del socket client.

Per disassociare la porta dal socket client, l'applicazione chiama ***nx_tcp_client_socket_unbind***. Il socket deve trovarsi in uno stato chiuso o nel processo di disconnessione (ad esempio, lo stato di attesa programmato) prima che la porta venga rilasciata; in caso contrario, viene restituito un errore.

Infine, se l'applicazione non necessita più del socket client, chiama ***nx_tcp_socket_delete*** per eliminare il socket.

### <a name="tcp-server-connection"></a>Connessione al server TCP

Il lato server di una connessione TCP è passivo; ovvero, il server attende che un client avvii una richiesta di connessione. Per accettare una connessione client, è prima necessario abilitare TCP sull'istanza IP chiamando il servizio ***nx_tcp_enable** _. Successivamente, l'applicazione deve creare un socket TCP usando il servizio _ *_nx_tcp_socket_create_**.

Il socket del server deve essere configurato anche per l'ascolto delle richieste di connessione. Questa operazione viene eseguita tramite il servizio ***nx_tcp_server_socket_listen*** . Questo servizio posiziona il socket del server nello stato di ascolto e associa la porta del server specificata al socket.

> [!IMPORTANT]
> *Per impostare una routine di callback di ascolto del socket, l'applicazione specifica la funzione di callback appropriata per l'argomento tcp_listen_callback del servizio di **nx_tcp_server_socket_listen** . Questa funzione di callback dell'applicazione viene quindi eseguita da NetX ogni volta che viene richiesta una nuova connessione sulla porta del server. L'elaborazione nel callback è sotto il controllo dell'applicazione.*

Per accettare le richieste di connessione client, l'applicazione chiama il servizio ***nx_tcp_server_socket_accept** _. Il socket del server deve essere in uno stato di attesa o in uno stato SYN ricevuto (ovvero, il server è in stato di ascolto e ha ricevuto un pacchetto SYN da un client che ha richiesto una connessione) per chiamare il servizio Accept. Uno stato restituito correttamente da _ *_nx_tcp_server_socket_accept_** indica che la connessione è stata configurata e che il socket del server si trova nello stato stabilita.

Dopo che il socket del server dispone di una connessione valida, le richieste di connessione client aggiuntive vengono accodate fino alla profondità specificata dal *listen_queue_size*, passate al servizio ***nx_tcp_server_socket_listen** _. Per elaborare le connessioni successive su una porta del server, l'applicazione deve chiamare _ *_nx_tcp_server_socket_relisten_** con un socket disponibile, ovvero un socket in uno stato chiuso. Si noti che è possibile usare lo stesso socket del server se la connessione precedente associata al socket è terminata e lo stato del socket è CLOSED.

### <a name="tcp-server-disconnection"></a>Disconnessione del server TCP

La chiusura della connessione viene eseguita chiamando ***nx_tcp_socket_disconnect***. Se non viene specificata alcuna sospensione, il socket del server invia un pacchetto RST al socket client e posiziona il socket nello stato CLOSED. In caso contrario, se viene richiesta una sospensione, viene eseguito il protocollo di disconnessione TCP completo, come indicato di seguito: |

- Se il client ha avviato in precedenza una richiesta di disconnessione (il socket del server ha già ricevuto un pacchetto FIN, ha risposto con un ACK ed è nello stato di attesa di chiusura), NetX promuove lo stato del socket TCP per l'ultimo stato ACK e invia un pacchetto FIN. Attende quindi un ACK dal client prima di completare la disconnessione e di entrare nello stato CLOSED.

- Se invece il server è il primo ad avviare una richiesta di disconnessione (il client non si è disconnesso e il socket si trova ancora nello stato stabilito), NetX Invia un pacchetto FIN per avviare la disconnessione e attende la ricezione di una pinna e di un ACK dal client prima di completare la disconnessione e di collocare il socket in uno stato chiuso.

Se nella coda di trasmissione del socket sono ancora presenti pacchetti, NetX sospende il timeout specificato per consentire la conferma di tali pacchetti. Se il timeout scade, NetX Scarica la coda di trasmissione del socket del server.

Una volta completata l'elaborazione della disconnessione e il socket del server si trova nello stato CLOSED, l'applicazione deve chiamare il servizio ***nx_tcp_server_socket_unaccept*** per terminare l'associazione di questo socket con la porta del server. Si noti che questo servizio deve essere chiamato dall'applicazione anche se ***nx_tcp_socket_disconnect*** o ***nx_tcp_server_socket_accept** _ restituisce uno stato di errore. Dopo la restituzione di _ *_nx_tcp_server_socket_unaccept_**, il socket può essere utilizzato come socket client o server o anche eliminato se non è più necessario. Se si desidera accettare un'altra connessione client sulla stessa porta del server, è necessario chiamare il servizio ***nx_tcp_server_socket_relisten*** su questo socket.

Nel segmento di codice seguente viene illustrata la sequenza di chiamate utilizzate da un server TCP tipico:

```c
/* Set up a previously created TCP socket to listen on port 12 */

nx_tcp_server_socket_listen()

/* Loop to make a (another) connection. */
while(1) {

    /* Wait for a client socket connection request for 100 ticks. */
    nx_tcp_server_socket_accept();

    /* (Send and receive TCP messages with the TCP client) */

    /* Disconnect the server socket. */
    nx_tcp_socket_disconnect();

    /* Remove this server socket from listening on the port. */

    nx_tcp_server_socket_unaccept(&server_socket);

    /* Set up server socket to relisten on the same port for the next
    client. */
    nx_tcp_server_socket_relisten();
}
```

### <a name="mss-validation"></a>Convalida MSS

La dimensione massima del segmento (MSS) è la quantità massima di byte che un host TCP può ricevere senza essere frammentato dal livello IP sottostante. Durante la fase di creazione della connessione TCP, entrambe le terminazioni scambiano il proprio valore TCP MSS, in modo che il mittente non invii un segmento di dati TCP maggiore della MSS del destinatario. Il modulo NetX TCP convaliderà facoltativamente il valore MSS annunciato del peer prima di stabilire una connessione. Per impostazione predefinita, NetX non Abilita un controllo di questo tipo. Le applicazioni che desiderano eseguire la convalida MSS definiranno ***NX_ENABLE_TCP_MSS_CHECKING** _ quando compilano la libreria NETX e il valore minimo verrà definito in _*_NX_TCP_MSS_MINIMUM_*_. Le connessioni TCP in ingresso con valori MSS inferiori a _ *_NX_TCP_MSS_MINIMUM_** verranno eliminate.

### <a name="stop-listening-on-a-server-port"></a>Interrompi ascolto su una porta del server

Se l'applicazione non desidera più restare in ascolto delle richieste di connessione client su una porta del server specificata in precedenza da una chiamata al servizio ***nx_tcp_server_socket_listen** _, l'applicazione chiama semplicemente il servizio _ *_nx_tcp_server_socket_unlisten_**. Questo servizio posiziona tutti i socket in attesa di una connessione nello stato CLOSED e rilascia tutti i pacchetti di richieste di connessione client in coda.

### <a name="tcp-window-size"></a>Dimensioni finestra TCP

Durante le fasi di installazione e trasferimento dei dati della connessione, ogni porta segnala la quantità di dati che è in grado di gestire, denominata dimensione della finestra. Quando i dati vengono ricevuti ed elaborati, questa dimensione della finestra viene regolata dinamicamente. In TCP un mittente può inviare solo una quantità di dati che si inserisce nella finestra del destinatario. In sostanza, le dimensioni della finestra forniscono il controllo di flusso per il trasferimento dei dati in ogni direzione della connessione.

### <a name="tcp-packet-send"></a>Invio di pacchetti TCP

L'invio di dati TCP viene eseguito facilmente chiamando la funzione ***nx_tcp_socket_send*** . Se le dimensioni dei dati trasmessi sono maggiori del valore MSS del socket o della dimensione della finestra di ricezione peer corrente, a seconda del valore più piccolo, la logica interna TCP suddivide i dati che rientrano in min (MSS, finestra di ricezione peer) per la trasmissione. Questo servizio compila quindi un'intestazione TCP davanti al pacchetto (incluso il calcolo del checksum). Se le dimensioni della finestra del ricevitore non sono pari a zero, il chiamante invierà il maggior numero di dati possibile per riempire le dimensioni della finestra del ricevitore. Se la finestra di ricezione diventa zero, il chiamante potrebbe sospendere e attendere che le dimensioni della finestra del destinatario aumentino sufficiente per l'invio del pacchetto. In qualsiasi momento, più thread possono sospendere durante il tentativo di invio di dati tramite lo stesso socket.

> [!IMPORTANT]
> *I dati TCP che risiedono nella struttura di NX_PACKET devono trovarsi su un limite di parole lunghe. Inoltre, è necessario disporre di spazio sufficiente tra il puntatore anteposto e il puntatore di avvio dati per inserire le intestazioni TCP, IP e supporti fisici.*

### <a name="tcp-packet-retransmit"></a>Ritrasmissione del pacchetto TCP

I pacchetti TCP trasmessi in precedenza venivano effettivamente archiviati internamente fino a quando non viene restituito un ACK dall'altro lato della connessione. Se i dati trasmessi non vengono riconosciuti entro il periodo di timeout, il pacchetto archiviato viene inviato nuovamente e viene impostato il periodo di timeout successivo. Quando viene ricevuto un ACK, vengono infine rilasciati tutti i pacchetti analizzati dal numero di riconoscimento nella coda di trasmissione interna.

> [!IMPORTANT]
> * L'applicazione non deve riutilizzare il pacchetto o modificare il contenuto del pacchetto dopo che la funzione ***nx_tcp_socket_send** _ restituisce con NX_SUCCESS. Il pacchetto trasmesso viene infine rilasciato dall'elaborazione interna NetX dopo che i dati sono stati riconosciuti dagli altri end._

### <a name="tcp-keepalive"></a>Keepalive TCP

La funzionalità TCP keepalive consente a un socket di rilevare se il peer si disconnette o meno senza terminazione corretta, ad esempio se il peer si è arrestato in modo anomalo, oppure per impedire a determinate funzionalità di monitoraggio della rete di terminare una connessione per lunghi periodi di inattività. Il protocollo keepalive TCP funziona inviando periodicamente un frame TCP senza dati e il numero di sequenza impostato su uno inferiore al numero di sequenza corrente. Alla ricezione di tale frame TCP keepalive, il destinatario, se ancora attivo, risponde con un ACK per il numero di sequenza corrente. Questa operazione completa la transazione KeepAlive.

Per impostazione predefinita, la funzionalità KeepAlive non è abilitata. Per usare questa funzionalità, è necessario compilare la libreria NetX con ***NX_ENABLE_TCP_KEEPALIVE** _ defined. Il simbolo _ *_NX_TCP_KEEPALIVE_INITIAL_** specifica il numero di secondi di inattività prima dell'avvio del frame KeepAlive.

### <a name="tcp-packet-receive"></a>Ricezione di pacchetti TCP

L'elaborazione dei pacchetti di ricezione TCP (chiamata dal thread helper IP) è responsabile della gestione di varie azioni di connessione e disconnessione, oltre che dell'elaborazione di riconoscimento della trasmissione. Inoltre, l'elaborazione dei pacchetti TCP receive è responsabile dell'inserimento dei pacchetti con i dati di ricezione nella coda di ricezione del socket TCP appropriato o del recapito del pacchetto al primo thread sospeso in attesa di un pacchetto.

### <a name="tcp-receive-notify"></a>Notifica di ricezione TCP

Se il thread dell'applicazione deve elaborare i dati ricevuti da più di un socket, è necessario usare la funzione ***nx_tcp_socket_receive_notify*** . Questa funzione registra una funzione di callback del pacchetto di ricezione per il socket. Ogni volta che viene ricevuto un pacchetto nel socket, viene eseguita la funzione di callback.

Il contenuto della funzione di callback è specifico dell'applicazione. Tuttavia, la funzione conterrebbe probabilmente la logica per informare il thread di elaborazione che un pacchetto è disponibile nel socket corrispondente.

### <a name="thread-suspension"></a>Sospensione thread

Come indicato in precedenza, i thread dell'applicazione possono sospendere il tentativo di ricevere dati da una determinata porta TCP. Dopo la ricezione di un pacchetto su tale porta, questo viene assegnato al primo thread sospeso e il thread viene quindi ripreso. Un timeout facoltativo è disponibile quando si sospende un pacchetto di ricezione TCP, una funzionalità disponibile per la maggior parte dei servizi NetX.

La sospensione dei thread è disponibile anche per la connessione (client e server), l'associazione client e i servizi di disconnessione.

### <a name="tcp-socket-statistics-and-errors"></a>Statistiche ed errori del socket TCP

Se abilitata, il software socket TCP NetX tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per ogni istanza IP/TCP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale pacchetti TCP inviati
- Totale byte TCP inviati
- Totale pacchetti TCP ricevuti
- Totale byte TCP ricevuti
- Totale pacchetti TCP non validi
- Totale pacchetti di ricezione TCP eliminati
- Totale errori di checksum di ricezione TCP
- Totale connessioni TCP
- Totale disconnessioni TCP
- Totale connessioni TCP eliminate
- Totale ritrasmissioni dei pacchetti TCP
- Pacchetti socket TCP inviati
- Byte socket TCP inviati
- Pacchetti socket TCP ricevuti
- Byte socket TCP ricevuti
- Ritrasmette i pacchetti socket TCP
- Pacchetti socket TCP in coda
- Errori di checksum del socket TCP
- Stato socket TCP
- Profondità coda di trasmissione socket TCP
- Dimensioni finestra di trasmissione socket TCP
- Dimensioni della finestra di ricezione socket TCP

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_tcp_info_get** _ per le statistiche TCP totali e il servizio _ *_nx_tcp_socket_info_get_** per le statistiche TCP per socket.

## <a name="tcp-socket-control-block-nx_tcp_socket"></a>NX_TCP_SOCKET blocco di controllo socket TCP

Le caratteristiche di ogni socket TCP si trovano nel blocco di controllo *NX_TCP_SOCKET* associato, che contiene informazioni utili, ad esempio il collegamento alla struttura dei dati IP, l'interfaccia di connessione di rete, la porta associata e la coda dei pacchetti di ricezione. Questa struttura viene definita nel file ***nx_api. h*** .
