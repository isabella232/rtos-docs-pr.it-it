---
title: Capitolo 3-componenti funzionali di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione dello stack TCP/IP di Azure RTO NetX Duo a prestazioni elevate dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 31900c7b822c88079e4b9fe28a8a388d20f819aa
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106549845"
---
# <a name="chapter-3---functional-components-of-azure-rtos-netx-duo"></a>Capitolo 3-componenti funzionali di Azure RTO NetX Duo

Questo capitolo contiene una descrizione dello stack TCP/IP di Azure RTO NetX Duo a prestazioni elevate dal punto di vista funzionale. 

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Esistono cinque tipi di esecuzione del programma all'interno di un'applicazione NetX Duo: inizializzazione, chiamate di interfaccia dell'applicazione, thread IP interno, timer periodici IP e driver di rete.

> [!NOTE]
> *NetX Duo presuppone l'esistenza di ThreadX e dipende dall'esecuzione del thread, dalla sospensione, dai timer periodici e dalle strutture di esclusione reciproca.*

### <a name="initialization"></a>Inizializzazione

Il servizio ***nx_system_initialize** _ deve essere chiamato prima di chiamare qualsiasi altro servizio NETX Duo. L'inizializzazione del sistema può essere chiamata dalla funzione ThreadX _ *_tx_application_define_** o dai thread dell'applicazione.

Dopo che ***nx_system_initialize** _ restituisce, il sistema è pronto per la creazione di pool di pacchetti e istanze IP. Poiché la creazione di un'istanza IP richiede un pool di pacchetti predefinito, è necessario che esista almeno un pool di pacchetti NetX duo prima di creare un'istanza IP. La creazione di pool di pacchetti e istanze IP è consentita dalla funzione di inizializzazione ThreadX _ *_tx_application_define_** e dai thread dell'applicazione.

Internamente, la creazione di un'istanza IP viene eseguita in due parti: la prima parte viene eseguita nel contesto del chiamante, dal ***tx_application_define*** o dal contesto del thread dell'applicazione. Ciò include la configurazione della struttura dei dati IP e la creazione di varie risorse IP, incluso il thread IP interno. La seconda parte viene eseguita durante l'esecuzione iniziale dal thread IP interno. Questo è il punto in cui il driver di rete, fornito durante la prima parte della creazione dell'IP, viene chiamato per la prima volta. La chiamata del driver di rete dal thread IP interno consente al driver di eseguire operazioni di I/O e di sospendere durante l'elaborazione dell'inizializzazione.

Quando il driver di rete viene restituito dalla relativa elaborazione di inizializzazione, la creazione dell'indirizzo IP è stata completata.

Per l'inizializzazione di IPv6 in NetX Duo sono necessari alcuni altri servizi NetX Duo. Sono descritte più dettagliatamente nella sezione [IPv6 in NETX Duo](#ipv6-in-netx-duo) più avanti in questo capitolo.

> [!NOTE]
> *Il **nx_ip_status_check** del servizio NETX Duo è disponibile per ottenere informazioni sull'istanza IP e lo stato dell'interfaccia principale. Tali informazioni di stato includono se il collegamento è stato inizializzato, abilitato e l'indirizzo IP è stato risolto. Queste informazioni vengono usate per sincronizzare i thread dell'applicazione che richiedono l'uso di un'istanza IP appena creata. Per i sistemi multihome, vedere [supporto multihome](#multihome-support). **nx_ip_interface_status_check** è disponibile per ottenere 3information sull'interfaccia specificata.*

### <a name="application-interface-calls"></a>Chiamate dell'interfaccia dell'applicazione

Le chiamate dall'applicazione vengono eseguite in gran parte dai thread dell'applicazione in esecuzione in ThreadX RTO. Tuttavia, alcuni servizi di inizializzazione, creazione e abilitazione possono essere chiamati da ***tx_application_define***. Le sezioni "consentito da" del [capitolo 4-Descrizione dei servizi di Azure RTO NETX Duo](chapter4.md) indicano da quale può essere chiamato ogni servizio NETX Duo.

Nella maggior parte dei casi, l'elaborazione di attività intensive, ad esempio il calcolo dei checksum, viene eseguita nel contesto del thread chiamante, senza bloccare l'accesso ad altri thread all'istanza IP. Ad esempio, sulla trasmissione, il calcolo del checksum UDP viene eseguito all'interno del servizio ***nx_udp_socket_send** _, prima di chiamare la funzione di invio IP sottostante. In un pacchetto ricevuto, il checksum UDP viene calcolato nel servizio _ *_nx_udp_socket_receive_**, eseguito nell'oggetto del thread dell'applicazione. Ciò consente di impedire il blocco delle richieste di rete di thread con priorità più alta a causa dell'elaborazione di calcoli di checksum intensivi nei thread con priorità più bassa.

I valori, ad esempio gli indirizzi IP e i numeri di porta, vengono passati alle API nell'ordine dei byte dell'host. Internamente, questi valori vengono archiviati anche nell'ordine dei byte dell'host. Ciò consente agli sviluppatori di visualizzare facilmente i valori tramite un debugger. Quando questi valori vengono programmati in un frame per la trasmissione, vengono convertiti in ordine byte di rete.

### <a name="internal-ip-thread"></a>Thread IP interno

Come indicato in precedenza, ogni istanza IP in NetX Duo dispone di un proprio thread. La priorità e le dimensioni dello stack del thread IP interno sono definite nel servizio ***nx_ip_create*** . Il thread IP interno viene creato in modalità pronta per l'esecuzione. Se il thread IP ha una priorità più elevata rispetto al thread chiamante, è possibile che si verifichi la precedenza all'interno della chiamata di creazione IP.

Il punto di ingresso del thread IP interno si trova nella funzione interna _ ***nx_ip_thread_entry***. Quando viene avviato, il thread IP interno completa innanzitutto l'inizializzazione del driver di rete, che consiste nell'effettuare tre chiamate al driver di rete specifico dell'applicazione. La prima chiamata consiste nel connettersi al driver di rete all'istanza IP, seguita da una chiamata di inizializzazione, che consente al driver di rete di passare attraverso il processo di inizializzazione. Dopo che il driver di rete è stato restituito dall'inizializzazione (potrebbe sospendere in attesa della corretta configurazione dell'hardware), il thread IP interno chiama di nuovo il driver di rete per abilitare il collegamento. Quando il driver di rete viene restituito dalla chiamata di attivazione del collegamento, il thread IP interno immette un controllo del ciclo Forever per i vari eventi che richiedono l'elaborazione per questa istanza IP. Gli eventi elaborati in questo ciclo includono la ricezione di pacchetti IP posticipati, l'assembly dei frammenti di pacchetti IP, l'elaborazione dei ping ICMP, l'elaborazione IGMP, l'elaborazione della coda di pacchetti TCP, l'elaborazione periodica TCP, i timeout degli assembly dei frammenti IP e l'elaborazione periodica di IGMP. Gli eventi includono inoltre le attività di risoluzione degli indirizzi. Elaborazione di pacchetti ARP e elaborazione periodica ARP in IPv4, rilevamento di indirizzi duplicati, richiesta router e individuazione vicina in IPv6.

> [!CAUTION]
> *Le funzioni di callback di NetX Duo, inclusi i callback di ascolto e disconnessione, vengono chiamate dal thread IP interno, non dal thread chiamante originale. È necessario che l'applicazione non venga sospesa all'interno di una funzione di callback NetX Duo.*

### <a name="ip-periodic-timers"></a>Timer periodici IP

Per ogni istanza IP sono usati due timer periodici ThreadX. Il primo è un timer di un secondo per ARP, IGMP, TCP timeout e anche l'elaborazione del frammento IP del riassemblaggio. Il secondo timer è un timer di 100 ms per guidare il timeout di ritrasmissione TCP e le operazioni correlate a IPv6.

### <a name="network-driver"></a>Driver di rete

Ogni istanza IP in NetX duo ha un'interfaccia primaria, identificata dal driver di dispositivo specificato nel servizio ***nx_ip_create*** . Il driver di rete è responsabile della gestione di varie richieste NetX Duo, tra cui la trasmissione di pacchetti, la ricezione di pacchetti e le richieste di stato e controllo. 

Per un sistema multi-Home, l'istanza IP dispone di più interfacce, ciascuna con un driver di rete associato che esegue queste attività per la rispettiva interfaccia.

Il driver di rete deve inoltre gestire gli eventi asincroni che si verificano sui supporti. Gli eventi asincroni dai supporti includono la ricezione di pacchetti, il completamento della trasmissione del pacchetto e le modifiche dello stato. NetX Duo fornisce al driver di rete numerose funzioni di accesso per gestire vari eventi. Queste funzioni sono progettate per essere chiamate dalla parte di routine del servizio di interrupt del driver di rete. Per le reti IPv4, il driver di rete deve inoltrare tutti i pacchetti ARP ricevuti al ***_nx_arp_packet_deferred_receive*** funzione interna. Tutti i pacchetti RARP devono essere inoltrati alla funzione ***_nx_rarp_packet_deferred_receive** _ interna. Sono disponibili due opzioni per i pacchetti IP. Se è necessario inviare rapidamente i pacchetti IP, i pacchetti IP in ingresso devono essere inoltrati a _ *_ _nx_ip_packet_receive_* _ per l'elaborazione immediata. Ciò migliora notevolmente le prestazioni di NetX Duo nella gestione dei pacchetti IP. In caso contrario, è necessario inoltrare i pacchetti IP a _ *_ _nx_ip_packet_deferred_receive_**. Questo servizio posiziona il pacchetto IP nella coda di elaborazione posticipata, dove viene quindi gestito dal thread IP interno, che comporta la quantità minima di tempo di elaborazione ISR.

Il driver di rete può anche rinviare l'elaborazione di interrupt per esaurire il contesto del thread IP. In questa modalità, l'ISR deve salvare le informazioni necessarie, chiamare la funzione interna ***_nx_ip_driver_deferred_processing*** e confermare il controller di interrupt. Questo servizio invia una notifica al thread IP per pianificare un callback al driver di dispositivo per completare il processo dell'evento che ha causato l'interruzione.

Alcuni controller di rete sono in grado di eseguire il calcolo e la convalida del checksum dell'intestazione TCP/IP nell'hardware, senza occupare risorse di CPU utili. Per sfruttare i vantaggi della funzionalità hardware Capability, NetX Duo fornisce opzioni per abilitare o disabilitare diversi calcoli di checksum software in fase di compilazione, nonché per attivare o disattivare il calcolo dei checksum in fase di esecuzione, se il driver di dispositivo è in grado di comunicare con il livello IP relativo alle funzionalità hardware. Per informazioni più dettagliate sulla scrittura di driver di rete NetX Duo, vedere il [capitolo 5-driver di rete di Azure RTO NETX Duo](chapter5.md) .

### <a name="multihome-support"></a>Supporto multihome

NetX Duo supporta i sistemi connessi a più dispositivi fisici usando una singola istanza IP. Ogni interfaccia fisica viene assegnata a un blocco di controllo dell'interfaccia nell'istanza IP. Le applicazioni che vogliono usare un sistema multihome devono definire il valore per ***NX_MAX_PHSYCIAL_INTERFACES** _ al numero di dispositivi fisici collegati al sistema e ricompilare la libreria NETX Duo. Per impostazione predefinita _ *_NX_MAX_PHYSICAL_INTERFACES_** è impostato su uno, creando un blocco di controllo dell'interfaccia nell'istanza IP.

L'applicazione NetX duo crea una singola istanza IP per il dispositivo primario usando il servizio ***nx_ip_create** _. Per ogni dispositivo di rete aggiuntivo, l'applicazione connette il dispositivo all'istanza IP usando il servizio _ *_nx_ip_interface_attach_**.

Ogni struttura di interfaccia di rete contiene un subset di informazioni di rete sull'interfaccia di rete contenuta nel blocco di controllo IP, tra cui indirizzo IPv4 dell'interfaccia, subnet mask, dimensioni MTU IP e informazioni sugli indirizzi del livello MAC.

> [!NOTE]
> *NetX Duo con supporto multihome è compatibile con le versioni precedenti di NetX Duo. I servizi che non accettano informazioni esplicite sull'interfaccia vengono predefiniti per il dispositivo di rete primario.*

L'interfaccia primaria ha indice zero nell'elenco di istanze IP. A ogni dispositivo successivo collegato all'istanza IP viene assegnato l'indice successivo.

Tutti i servizi del protocollo di livello superiore per i quali è abilitata l'istanza IP, inclusi TCP, UDP, ICMP e IGMP, sono disponibili per tutti i dispositivi collegati.

Nella maggior parte dei casi, NetX Duo può determinare l'indirizzo di origine migliore da usare durante la trasmissione di un pacchetto. La selezione dell'indirizzo di origine è basata sull'indirizzo di destinazione. Sono stati aggiunti i servizi NetX Duo per consentire alle applicazioni di specificare un indirizzo di origine specifico da usare, nei casi in cui l'indirizzo di destinazione non può essere determinato da quello più adatto. Un esempio è costituito da un sistema multihome, un'applicazione deve inviare un pacchetto a una trasmissione IPv4 o a indirizzi di destinazione multicast.

I servizi specifici per lo sviluppo di applicazioni multihome includono quanto segue:

- *nx_igmp_multicast_interface_join*
- *nx_igmp_multicast_interface_leave*
- *nx_ip_driver_interface_direct_command*
- *nx_ip_interface_address_get*
- *nx_ip_interface_address_mapping_configure*
- *nx_ip_interface_address_set*  
- *nx_ip_interface_attach*
- *nx_ip_interface_capability_get* 
- *nx_ip_interface_capability_set*
- *nx_ip_interface_detach*
- *nx_ip_interface_info_get*
- *nx_ip_interface_mtu_set*
- *nx_ip_interface_physical_address_get*
- *nx_ip_interface_physical_address_set*
- *nx_ip_interface_status_check*
- *nx_ip_raw_packet_source_send*
- *nx_ipv4_multicast_interface_join*
- *nx_ipv4_multicast_interface_leave*
- *nx_udp_socket_source_send*
- *nxd_ipv6_multicast_interface_join*
- *nxd_ipv6_multicast_interface_leave* 
- *nxd_udp_socket_source_send*
- *nxd_icmp_source_ping*
- *nxd_ip_raw_packet_source_send*
- *nxd_udp_socket_source_send*

Questi servizi sono descritti in modo più dettagliato nella [Descrizione dei servizi NETX Duo](chapter4.md).

### <a name="loopback-interface"></a>Interfaccia loopback

L'interfaccia di loopback è un'interfaccia di rete speciale senza collegamento fisico associato a. L'interfaccia di loopback consente alle applicazioni di comunicare utilizzando l'indirizzo di loopback IPv4 127.0.0.1 per utilizzare un'interfaccia di loopback logica, assicurarsi che l'opzione configurabile ***NX_DISABLE_LOOPBACK_INTERFACE*** non sia impostata.

### <a name="interface-control-blocks"></a>Blocchi di controllo dell'interfaccia

Il numero di blocchi di controllo dell'interfaccia nell'istanza IP è il numero di interfacce fisiche (definite da ***NX_MAX_PHYSICAL_INTERFACES** _) più l'interfaccia di loopback se abilitata. Il numero totale di interfacce è definito in _ *_NX_MAX_IP_INTERFACES_* *.

## <a name="protocol-layering"></a>Layering del protocollo

Il protocollo TCP/IP implementato da NetX Duo è un protocollo a più livelli, che significa che i protocolli più complessi sono basati su protocolli sottostanti più semplici. In TCP/IP, il protocollo di livello più basso si trova a *livello di collegamento* e viene gestito dal driver di rete. Questo livello è in genere destinato a Ethernet, ma può anche essere Fiber, seriale o praticamente qualsiasi supporto fisico.

Sopra il livello di collegamento è il *livello di rete*. In TCP/IP, questo è l'indirizzo IP, che è essenzialmente responsabile dell'invio e della ricezione di pacchetti semplici, in modo ottimale, in tutta la rete. I protocolli di tipo gestione come ICMP e IGMP vengono in genere categorizzati anche come livelli di rete, anche se si basano su IP per l'invio e la ricezione.

Il *livello di trasporto* è posizionato sopra il livello di rete. Questo livello è responsabile della gestione del flusso di dati tra gli host nella rete. Sono disponibili due tipi di servizi di trasporto supportati da NetX Duo: UDP e TCP. I servizi UDP garantiscono l'invio e la ricezione dei dati tra due host senza connessione, mentre TCP fornisce un servizio affidabile orientato alla connessione tra due entità host.

Questo livello viene riflesso nei pacchetti di dati di rete effettivi. Ogni livello in TCP/IP contiene un blocco di informazioni denominato intestazione. Questa tecnica relativa ai dati circostanti (e possibilmente alle informazioni sul protocollo) con un'intestazione viene in genere chiamata incapsulamento dei dati. Nella figura 1 viene illustrato un esempio di livello NetX Duo e nella figura 2 viene illustrato l'incapsulamento dei dati risultante per i dati UDP inviati.

![Layering del protocollo](./media/user-guide/image12.jpg)

**FIGURA 1. Layering del protocollo**

## <a name="packet-pools"></a>Pool di pacchetti

L'allocazione di pacchetti in modo rapido e deterministico è sempre una sfida nelle applicazioni di rete in tempo reale. Tenendo presente questo aspetto, NetX Duo fornisce la possibilità di creare e gestire più pool di pacchetti di rete a dimensione fissa.

Poiché i pool di pacchetti NetX Duo sono costituiti da blocchi di memoria a dimensione fissa, non si verificano mai problemi di frammentazione interna. Naturalmente, la frammentazione causa comportamenti intrinsecamente non deterministici. Inoltre, il tempo necessario per allocare e liberare un pacchetto NetX Duo equivale a una semplice manipolazione di elenchi collegati. Inoltre, l'allocazione e la deallocazione dei pacchetti vengono eseguite all'inizio dell'elenco disponibile. In questo modo si fornisce l'elaborazione dell'elenco collegato più veloce possibile.

![Incapsulamento dei dati UDP](./media/user-guide/image13.png)

**FIGURA 2. Incapsulamento dei dati UDP**

La mancanza di flessibilità è in genere lo svantaggio principale dei pool di pacchetti a dimensione fissa. Determinare le dimensioni del payload dei pacchetti ottimali che gestiscono anche il pacchetto in ingresso peggiore è un'attività difficile. I pacchetti NetX Duo affrontano questo problema con una funzionalità facoltativa denominata concatenamento dei pacchetti. Un pacchetto di rete effettivo può essere composto da uno o più pacchetti NetX Duo collegati tra loro. Inoltre, l'intestazione del pacchetto mantiene un puntatore all'inizio del pacchetto. Quando vengono aggiunti altri protocolli, questo puntatore viene semplicemente spostato all'indietro e la nuova intestazione viene scritta direttamente davanti ai dati. Senza la tecnologia flessibile dei pacchetti, lo stack dovrebbe allocare un altro buffer e copiare i dati in un nuovo buffer con la nuova intestazione, che sta elaborando in modo intensivo.

Poiché le dimensioni del payload del pacchetto sono fisse per un determinato pool di pacchetti, i dati dell'applicazione più grandi delle dimensioni del payload richiederebbero più pacchetti concatenati. Quando si compila un pacchetto con dati utente, l'applicazione utilizzerà il servizio ***nx_packet_data_append***. Questo servizio sposta i dati dell'applicazione in un pacchetto. Nei casi in cui un pacchetto non è sufficiente per contenere i dati utente, vengono allocati pacchetti aggiuntivi per archiviare i dati utente. Per utilizzare il concatenamento dei pacchetti, il driver deve essere in grado di ricevere o trasmettere da pacchetti concatenati.

Per i sistemi incorporati che non devono utilizzare la funzionalità di concatenamento dei pacchetti, la libreria NetX Duo può essere compilata con ***NX_DISABLE_PACKET_CHAIN** _ per rimuovere la logica di concatenamento dei pacchetti. Si noti che la frammentazione IP e la funzionalità di riassemblaggio potrebbero dover utilizzare la funzionalità dei pacchetti concatenati. Di conseguenza, la definizione di _*_NX_DISABLE_PACKET_CHAIN_*_ richiede anche la definizione di _ *_NX_DISABLE_FRAGMENTATION_**. 

Ogni pool di memoria del pacchetto NetX Duo è una risorsa pubblica. NetX Duo non pone vincoli sulla modalità di utilizzo di pool di pacchetti. 

### <a name="packet-pool-memory-area"></a>Area memoria pool di pacchetti

L'area di memoria per il pool di pacchetti viene specificata durante la creazione. Analogamente ad altre aree di memoria per gli oggetti ThreadX e NetX Duo, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione. 

Si tratta di una funzionalità importante grazie alla notevole flessibilità offerta dall'applicazione. Si supponga, ad esempio, che un prodotto di comunicazione disponga di un'area di memoria ad alta velocità per i buffer di rete. Questa area di memoria è facilmente utilizzabile rendendola in un pool di memoria pacchetti NetX Duo.

### <a name="creating-packet-pools"></a>Creazione di pool di pacchetti

I pool di pacchetti vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Non sono previsti limiti per il numero di pool di memoria pacchetti in un'applicazione NetX Duo.

### <a name="dual-packet-pool"></a>Pool di pacchetti doppio

In genere, le dimensioni del payload del pool di pacchetti IP predefinito sono sufficienti a supportare le dimensioni dei fotogrammi fino alla MTU dell'interfaccia di rete. Durante il normale funzionamento, il thread IP deve inviare messaggi quali ARP, i messaggi di controllo TCP, i messaggi IGMP, i messaggi ICMPv6. Questi messaggi usano i pacchetti allocati dal pool di pacchetti predefinito nell'istanza IP. In un sistema con vincoli di memoria in cui la quantità di memoria disponibile per il pool di pacchetti è limitata, l'uso di un singolo pool di pacchetti (con le dimensioni del payload elevato per la corrispondenza delle dimensioni MTU) potrebbe non essere una soluzione ottimale. NetX Duo consente all'applicazione di installare un pool di pacchetti ausiliario, in cui le dimensioni del payload sono inferiori. Una volta installato il pool di pacchetti ausiliario, il thread helper IP alloca i pacchetti dal pool di pacchetti predefinito o dal pool ausiliario, a seconda delle dimensioni del messaggio trasmesso. Per un pool di pacchetti ausiliari, le dimensioni del payload di 200 byte funzionano con la maggior parte dei messaggi trasmessi dal thread helper IP.

Per impostazione predefinita, la libreria NetX Duo è compilata senza abilitare il pool di pacchetti doppio. Per abilitare la funzionalità, compilare la libreria con ***NX_DUAL_PACKET_POOL_ENABLE** _ defined. Il pool di pacchetti ausiliario può essere impostato chiamando _ *_nx_ip_auxiliary_packet_pool_set_* *.

È anche possibile creare più di un pool di pacchetti. Ad esempio, un pool di pacchetti di trasmissione viene creato con una dimensione ottimale del payload per le dimensioni dei messaggi previsti. Un pool di pacchetti di ricezione viene creato nel driver con le dimensioni del payload impostate sul valore MTU del driver, perché non è possibile stimare le dimensioni dei pacchetti ricevuti.

### <a name="packet-header-nx_packet"></a>NX_PACKET intestazione pacchetto   
Per impostazione predefinita, NetX Duo posiziona l'intestazione del pacchetto immediatamente prima dell'area del payload del pacchetto. Il pool di memoria pacchetti è fondamentalmente una serie di pacchetti, ovvero le intestazioni seguite immediatamente dal payload del pacchetto. L'intestazione del pacchetto (***NX_PACKET***) e il layout del pool di pacchetti sono illustrati nella figura 3.

Per i driver dei dispositivi di rete che sono in grado di eseguire zero operazioni di copia, in genere l'indirizzo iniziale dell'area del payload del pacchetto viene programmato nella logica DMA. Alcuni motori DMA hanno requisiti di allineamento nell'area del payload. Per rendere l'indirizzo iniziale dell'area di payload allineato correttamente per il motore DMA o l'operazione della cache, l'utente può definire il simbolo ***NX_PACKET_ALIGNMENT***.

> [!WARNING]
> *È importante che il driver di rete usi la funzione **nx_packet_transmit_release** al termine della trasmissione di un pacchetto. Questa funzione verifica che il pacchetto non faccia parte di una coda di output TCP prima che venga effettivamente inserito nel pool disponibile.*

![Layout dell'intestazione e del pool di pacchetti](./media/user-guide/image14.jpg)

**FIGURA 3. Layout dell'intestazione e del pool di pacchetti**

I campi dell'intestazione del pacchetto sono definiti nel modo seguente. Si noti che questa tabella non è un elenco completo di tutti i membri della struttura *NX_PACKET* .

|Intestazione pacchetto | Scopo |
|---|---|
|***nx_packet_pool_owner***|Questo campo fa riferimento al pool di pacchetti proprietario del pacchetto specifico. Quando il pacchetto viene rilasciato, viene rilasciato a questo particolare pool. Con la proprietà del pool all'interno di ogni pacchetto, è possibile che un datagramma si estenda su più pacchetti da più pool di pacchetti.|
|***nx_packet_next** _|Questo campo fa riferimento al pacchetto successivo all'interno dello stesso frame. Se è NULL, non sono presenti pacchetti aggiuntivi che fanno parte del frame. Questo campo viene usato anche per contenere pacchetti frammentati fino a quando non è possibile riassemblare l'intero pacchetto. viene rimosso se _ *_NX_DISABLE_PACKET_CHAIN_* * è definito.|
|***nx_packet_last** _|Questo campo punta all'ultimo pacchetto all'interno dello stesso pacchetto di rete. Se NULL, questo pacchetto rappresenta l'intero pacchetto di rete. Questo campo viene rimosso se _ *_NX_DISABLE_PACKET_CHAIN_* * è definito.|
|***nx_packet_length** _| Questo campo contiene il numero totale di byte nell'intero pacchetto di rete, incluso il totale di tutti i byte in tutti i pacchetti concatenati dal membro _nx_packet_next *.|
|***nx_packet_ip_interface***| Questo campo è il blocco di controllo dell'interfaccia che viene assegnato al pacchetto quando viene ricevuto dal driver di interfaccia e da NetX Duo per i pacchetti in uscita. Un blocco di controllo dell'interfaccia descrive l'interfaccia, ad esempio l'indirizzo di rete, l'indirizzo MAC, l'indirizzo IP e lo stato dell'interfaccia, ad esempio collegamento abilitato e mapping fisico obbligatorio.|
|***nx_packet_data_start** _| Questo campo punta all'inizio dell'area del payload fisico del pacchetto. Non è necessario che si trovi immediatamente dopo l'intestazione NX_PACKET, ma è l'impostazione predefinita per il servizio _ *_nx_packet_pool_create_**.|
|***nx_packet_data_end** _|Questo campo punta alla fine dell'area del payload fisico del pacchetto. La differenza tra questo campo e il campo _nx_packet_data_start * rappresenta le dimensioni del payload.|
|***nx_packet_prepend_ptr** _|Questo campo fa riferimento alla posizione in cui vengono aggiunti i dati dei pacchetti, ovvero l'intestazione del protocollo o i dati effettivi, davanti ai dati dei pacchetti esistenti (se presenti) nell'area del payload del pacchetto. Deve essere maggiore o uguale alla posizione del puntatore _nx_packet_data_start * e minore o uguale al puntatore di *nx_packet_append_ptr* .|
> [!CAUTION]
> *Per motivi di prestazioni, NetX Duo presuppone che, quando il pacchetto viene passato ai servizi di NetX Duo per la trasmissione, il puntatore anteposto punti all'indirizzo allineato a parole lunghe.*

| Intestazione pacchetto | Scopo |
|---|---|
|***nx_packet_append_ptr** _|Questo campo punta alla fine dei dati attualmente presenti nell'area del payload del pacchetto. Deve trovarsi tra la posizione di memoria a cui punta _nx_packet_prepend_ptr * e *nx_packet_data_end.* La differenza tra questo campo e il campo *nx_packet_prepend_ptr* rappresenta la quantità di dati in questo pacchetto.|
|***nx_packet_packet_pad** _|Questo campo definisce la lunghezza del riempimento in parole a 4 byte per ottenere il requisito di allineamento desiderato. Questo campo viene rimosso se _*_NX_PACKET_HEADER_PAD_*_ non è definito. In alternativa, è possibile usare _*_NX_PACKET_ALIGNMENT_*_ anziché definire _nx_packet_header_pad. *|

### <a name="packet-header-offsets"></a>Offset dell'intestazione del pacchetto

Le dimensioni dell'intestazione del pacchetto sono definite in modo da consentire spazio sufficiente per contenere le dimensioni dell'intestazione. Il servizio ***nx_packet_allocate*** viene utilizzato per allocare un pacchetto e per regolare il puntatore anteposto nel pacchetto in base al tipo di pacchetto specificato. Il tipo di pacchetto indica a NetX Duo l'offset necessario per inserire l'intestazione del protocollo, ad esempio UDP, TCP o ICMP, davanti ai dati del protocollo.

I tipi seguenti sono definiti in NetX Duo per prendere in considerazione l'intestazione IP e l'intestazione del livello fisico (Ethernet) nel pacchetto. Nel secondo caso, si presuppone che sia 16 byte tenendo in considerazione l'allineamento richiesto di 4 byte. I pacchetti IPv4 sono ancora definiti in NetX Duo per le applicazioni per l'allocazione di pacchetti per reti IPv4. Si noti che se la libreria NetX Duo è compilata con IPv6 abilitato, i tipi di pacchetti generici (ad esempio NX_IP_PACKET) vengono mappati alla versione IPv6. Se la libreria NetX Duo è compilata senza IPv6 abilitato, viene eseguito il mapping di questi tipi di pacchetti generici alla versione IPv4.

La tabella seguente illustra i simboli definiti con IPv6 abilitato:

|**Tipo di pacchetto** |**Valore** |
|---|---|
|NX_IPv6_PACKET (NX_IP_PACKET) | 0x38 |
|NX_UDPv6_PACKET (NX_UDP_PACKET) |0x40 |
|NX_TCPv6_PACKET (NX_TCP_PACKET) |0x4c |
|NX_IPv4_PACKET |0x24 |
|NX_IPv4_UDP_PACKET |0x2c |
|NX_IPv4_TCP_PACKET |0x38 |

La tabella seguente illustra i simboli definiti con IPv6 disabilitato:

|**Tipo di pacchetto** |**Valore** |
|---|---|
|NX_IPv4_PACKET (NX_IP_PACKET) |0x24 |
|NX_IPv4_UDP_PACKET (NX_UDP_PACKET) |0x2c |
|NX_IPv4_TCP_PACKET (NX_TCP_PACKET) |0x38 |

Si noti che questi valori vengono modificati se *NX_IPSEC_ENABLE* viene definito. Per le applicazioni che utilizzano IPsec, vedere la guida dell'utente di NetX Duo IPsec per ulteriori informazioni.

### <a name="pool-capacity"></a>Capacità pool

Il numero di pacchetti in un pool di pacchetti è una funzione delle dimensioni del payload e il numero totale di byte nell'area di memoria fornita al servizio di creazione del pool di pacchetti. La capacità del pool viene calcolata dividendo le dimensioni del pacchetto (incluse le dimensioni dell'intestazione NX_PACKET, le dimensioni del payload e l'allineamento appropriato) nel numero totale di byte nell'area di memoria specificata.

### <a name="payload-area-alignment"></a>Allineamento area payload

La progettazione di pool di pacchetti in NetX Duo supporta la copia zero. A livello di driver di dispositivo, il driver è in grado di assegnare l'area di payload direttamente nei descrittori del buffer per la ricezione dei dati. A volte il motore DMA o il meccanismo di sincronizzazione della cache richiede che l'indirizzo iniziale dell'area del payload disponga di un determinato requisito di allineamento. Questa operazione può essere eseguita definendo il requisito di allineamento desiderato (in byte) in ***NX_PACKET_ALIGNMENT***. Quando si crea un pool di pacchetti, l'indirizzo iniziale dell'area del payload verrà allineato a questo valore. Per impostazione predefinita, l'indirizzo iniziale è allineato a 4 byte.

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono sospendere l'attesa di un pacchetto da un pool vuoto. Quando un pacchetto viene restituito al pool, al thread sospeso viene assegnato questo pacchetto e ripreso.

Se più thread sono sospesi nello stesso pool di pacchetti, vengono ripresi nell'ordine in cui sono stati sospesi (FIFO).

### <a name="pool-statistics-and-errors"></a>Statistiche ed errori del pool

Se abilitata, il software di gestione pacchetti NetX Duo tiene traccia di diverse statistiche ed errori che possono risultare utili per l'applicazione. Per i pool di pacchetti vengono mantenute le statistiche e i report degli errori seguenti:

- Totale pacchetti nel pool
- Pacchetti disponibili nel pool
- Totale allocazioni pacchetti
- Richieste di allocazione vuote del pool
- Sospensioni di allocazione vuote del pool
- Versioni di pacchetti non valide

Tutte le statistiche e le segnalazioni degli errori, ad eccezione del numero totale e dei pacchetti gratuiti nel pool, sono compilate nella libreria NetX Duo, a meno che non sia definito ***NX_DISABLE_PACKET_INFO** _. Questi dati sono disponibili per l'applicazione con il servizio _ *_nx_packet_pool_info_get_**.

### <a name="packet-pool-control-block-nx_packet_pool"></a>Blocco di controllo del pool di pacchetti NX_PACKET_POOL

Le caratteristiche di ogni pool di memoria dei pacchetti sono disponibili nel relativo blocco di controllo. Contiene informazioni utili, ad esempio l'elenco collegato di pacchetti gratuiti, il numero di pacchetti disponibili e le dimensioni del payload per i pacchetti in questo pool. Questa struttura viene definita nel file ***nx_api. h*** .

I blocchi di controllo del pool di pacchetti possono trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione.

## <a name="ipv4-protocol"></a>Protocollo IPv4

Il componente IP (Internet Protocol) di NetX Duo è responsabile dell'invio e della ricezione di pacchetti IPv4 su Internet. In NetX Duo è il componente responsabile dell'invio e della ricezione di messaggi TCP, UDP, ICMP e IGMP, usando il driver di rete sottostante.

NetX Duo supporta sia il protocollo IPv4 (RFC 791) che il protocollo IPv6 (RFC 2460). In questa sezione viene illustrato il protocollo IPv4. IPv6 verrà illustrato nella sezione successiva.

### <a name="ipv4-addresses"></a>Indirizzi IPv4

Ogni host su Internet dispone di un identificatore univoco a 32 bit denominato indirizzo IP. Sono disponibili cinque classi di indirizzi IPv4, come illustrato nella figura 4. Gli intervalli delle cinque classi di indirizzi IPv4 sono i seguenti:

|Classe|Range|
|---|---|
|A |da 0.0.0.0 a 127.255.255.255|
|B |da 128.0.0.0 a 191.255.255.255|
|C |da 192.0.0.0 a 223.255.255.255|
|D |da 224.0.0.0 a 239.255.255.255|
|E |da 240.0.0.0 a 247.255.255.255|

![Diagramma della struttura di indirizzi IPv4.](./media/user-guide/ipv4-address-structure.png)

### <a name="figure-4-ipv4-address-structure"></a>FIGURA 4. Struttura degli indirizzi IPv4

Sono disponibili anche tre tipi di specifiche degli indirizzi: *unicast*, *broadcast* e *multicast*. Gli indirizzi unicast sono gli indirizzi IPv4 che identificano un host specifico su Internet. Gli indirizzi unicast possono essere un indirizzo IPv4 di origine o di destinazione. Un indirizzo di trasmissione identifica tutti gli host in una rete o una subnet specifica e può essere utilizzato solo come indirizzi di destinazione. Gli indirizzi broadcast vengono specificati con la parte dell'ID host dell'indirizzo impostato su uno. Indirizzi multicast (classe D) specificare un gruppo dinamico di host su Internet. I membri del gruppo multicast possono partecipare e lasciare ogni volta che desiderano.

> [!IMPORTANT]
> *Solo i protocolli senza connessione come UDP su IPv4 possono utilizzare la trasmissione e la funzionalità di broadcast limitata del gruppo multicast.*

> [!IMPORTANT]
> * La macro *ip_address* è definita in ***nx_api. h** _. Consente di specificare facilmente gli indirizzi IPv4 usando le virgole anziché i punti. Ad esempio, _IP_ADDRESS (128, 0, 0, 0) * specifica il primo indirizzo della classe B illustrato nella figura 4. *

### <a name="ipv4-gateway-address"></a>Indirizzo IPv4 gateway

I gateway di rete assistono gli host sulle proprie reti per inoltrare pacchetti destinati a destinazioni esterne al dominio locale. Ogni nodo ha una certa conoscenza dell'hop successivo da inviare a, ovvero la destinazione di uno degli elementi adiacenti o tramite una tabella di routing statica preprogrammata. Tuttavia, se questi approcci hanno esito negativo, il nodo deve inoltrare il pacchetto al gateway predefinito, con una migliore conoscenza su come instradare il pacchetto alla relativa destinazione. Si noti che il gateway predefinito deve essere direttamente accessibile tramite una delle interfacce fisiche collegate all'istanza IP. L'applicazione chiama ***nx_ip_gateway_address_set** _ per configurare l'indirizzo del gateway predefinito IPv4. Usare il _*_nx_ip_gateway_address_get_*_ di servizio per recuperare le impostazioni correnti del gateway IPv4. Per cancellare l'impostazione del gateway, l'applicazione deve usare il servizio _ *_nx_ip_gateway_address_clear_**.

### <a name="ipv4-header"></a>Intestazione IPv4

Per ogni pacchetto IPv4 da inviare su Internet, è necessario che disponga di un'intestazione IPv4. Quando protocolli di livello superiore (UDP, TCP, ICMP o IGMP) chiamano il componente IP per inviare un pacchetto, il modulo di trasmissione IPv4 inserisce un'intestazione IPv4 davanti ai dati. Viceversa, quando i pacchetti IP vengono ricevuti dalla rete, il componente IP rimuove l'intestazione IPv4 dal pacchetto prima del recapito ai protocolli di livello superiore. La figura 5 Mostra il formato dell'intestazione IP.

![Formato dell'intestazione IPv4](./media/user-guide/ipv4-header-format.png)

### <a name="figure-5-ipv4-header-format"></a>FIGURA 5. Formato dell'intestazione IPv4

> [!IMPORTANT]
> *È previsto che tutte le intestazioni nell'implementazione TCP/IP siano in formato **Big Endian** . In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso. Ad esempio, la versione a 4 bit e la lunghezza dell'intestazione a 4 bit dell'intestazione IP devono trovarsi sul primo byte dell'intestazione.*

I campi dell'intestazione IPv4 sono definiti come segue:

|&nbsp;Campo di intestazione IPv4 &nbsp; |Scopo |
|---|---|
|***versione a 4 bit*** |Questo campo contiene la versione di IP rappresentata da questa intestazione. Per IP versione 4, che è supportata da NetX Duo, il valore di questo campo è 4. |
|***lunghezza intestazione a 4 bit*** |Questo campo specifica il numero di parole a 32 bit nell'intestazione IP. Se non sono presenti parole di opzione, il valore per questo campo è 5. |
|***tipo di servizio (TOS) a 8 bit*** |Questo campo specifica il tipo di servizio richiesto per il pacchetto IP. Le richieste valide sono le seguenti:<br />-Normale: 0x00 <br />-Ritardo minimo: 0x00<br />-Dati massimi: 0x08<br />-Massima affidabilità: 0x04<br />-Costo minimo: 0x02 |
|***Lunghezza totale a 16 bit*** |Questo campo contiene la lunghezza totale del datagramma IP in byte, inclusa l'intestazione IP. Un datagramma IP è l'unità di base delle informazioni disponibili in una rete Internet TCP/IP. Contiene un indirizzo di origine e di destinazione oltre ai dati. Poiché si tratta di un campo a 16 bit, le dimensioni massime di un datagramma IP sono pari a 65.535 byte.|
|***identificazione a 16 bit*** |Il campo è un numero usato per identificare in modo univoco ogni datagramma IP inviato da un host. Questo numero viene in genere incrementato dopo l'invio di un datagramma IP. È particolarmente utile per assemblare frammenti di pacchetti IP ricevuti.|
|***flag a 3 bit*** |Questo campo contiene informazioni sulla frammentazione IP. Il bit 14 è il bit "not Fragment". Se questo bit è impostato, il datagramma IP in uscita non verrà frammentato. Il bit 13 è il bit "More Fragments". Se questo bit è impostato, sono presenti più frammenti. Se questo bit è chiaro, questo è l'ultimo frammento del pacchetto IP.|
|***offset frammento a 13 bit*** |Questo campo contiene i 13 bit superiori dell'offset del frammento. Per questo motivo, gli offset dei frammenti sono consentiti solo su limiti di 8 byte. Il primo frammento di un datagramma IP frammentato avrà un set di bit "più frammenti" e un offset pari a 0.|
|***durata (TTL) a 8 bit*** |Questo campo contiene il numero di router che questo datagramma può superare, che sostanzialmente limita la durata del datagramma.|
|***protocollo a 8 bit***|Questo campo specifica il protocollo che usa il datagramma IP. Di seguito è riportato un elenco di protocolli validi e dei relativi valori:<br />-ICMP: 0x01 <br />-IGMP: 0x02<br />-TCP: 0X06<br />-UDP: 0X11 |
|***checksum a 16 bit*** |Questo campo contiene il checksum a 16 bit che copre solo l'intestazione IP. Nei protocolli di livello superiore sono presenti checksum aggiuntivi che coprono il payload IP. |
|***Indirizzo IP di origine a 32 bit*** |Questo campo contiene l'indirizzo IP del mittente ed è sempre un indirizzo host. |
|***Indirizzo IP di destinazione a 32 bit*** |Questo campo contiene l'indirizzo IP del destinatario o dei ricevitori se l'indirizzo è un indirizzo broadcast o multicast. |

### <a name="creating-ip-instances"></a>Creazione di istanze IP

Le istanze IP vengono create durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. L'indirizzo IPv4 iniziale, network mask, il pool di pacchetti predefinito, il driver multimediale e la memoria e la priorità del thread IP interno vengono definiti dal servizio ***nx_ip_create*** anche se l'applicazione intende utilizzare solo reti IPv6. Se l'applicazione Inizializza l'istanza IP con il relativo indirizzo IPv4 impostato su un indirizzo non valido (0.0.0.0), si presuppone che l'indirizzo dell'interfaccia venga risolto dalla configurazione manuale in un secondo momento, tramite RARP o tramite DHCP o protocolli simili.

Per i sistemi con più interfacce di rete, l'interfaccia principale viene designata quando si chiama ***nx_ip_create** _. Ogni interfaccia aggiuntiva può essere collegata alla stessa istanza IP chiamando _ *_nx_ip_interface_attach_* *. Questo servizio archivia informazioni sull'interfaccia di rete (ad esempio indirizzo IP, network mask) nel blocco di controllo dell'interfaccia e associa l'istanza del driver al blocco di controllo dell'interfaccia nell'istanza IP. Quando il driver riceve un pacchetto di dati, deve archiviare le informazioni sull'interfaccia nella struttura NX_PACKET prima di inoltrarle alla logica di ricezione IP. Nota è necessario che un'istanza IP sia già stata creata prima di eseguire il fissaggio di qualsiasi interfaccia.

I servizi IPv6 non vengono avviati dopo aver chiamato ***nx_ip_create** _. Le applicazioni che desiderano utilizzare i servizi IPv6 devono chiamare il servizio _ *_nx_ipv6_enable_** per avviare IPv6.

Nella rete IPv6 ogni interfaccia in un'istanza IP può avere più indirizzi globali IPv6. Oltre a usare DHCPv6 per l'assegnazione di indirizzi IPv6, un dispositivo può usare anche la configurazione automatica degli indirizzi senza stato. Ulteriori informazioni sono disponibili nelle sezioni "blocco di controllo IP" e "risoluzione degli indirizzi IPv6" più avanti in questo capitolo.

### <a name="ip-send"></a>Invio IP

L'elaborazione dell'invio IP in NetX Duo è molto semplificata. Il puntatore anteposto nel pacchetto viene spostato all'indietro per contenere l'intestazione IP. L'intestazione IP viene completata (con tutte le opzioni specificate dal livello del protocollo chiamante), il checksum IP viene calcolato in linea (solo per i pacchetti IPv4) e il pacchetto viene inviato al driver di rete associato. Inoltre, la frammentazione in uscita è coordinata anche all'interno dell'elaborazione di trasmissione IP.

Per IPv4, NetX Duo avvia le richieste ARP se è necessario un mapping fisico per l'indirizzo IP di destinazione. IPv6 usa l'individuazione Neighbor per il mapping IPv6-address-tophysical-Address.

> [!NOTE]
> *Per la connettività IPv4, i pacchetti che richiedono la risoluzione degli indirizzi IP (ad esempio, il mapping fisico) vengono accodati nella coda ARP finché il numero di pacchetti in coda non supera la profondità della coda ARP (definita dal simbolo **NX_ARP_MAX_QUEUE_DEPTH**). Se viene raggiunta la profondità della coda, NetX Duo rimuoverà il pacchetto meno recente nella coda e continuerà ad attendere la risoluzione degli indirizzi per i pacchetti rimanenti accodati. D'altra parte, se non viene risolta una voce ARP, i pacchetti in sospeso sulla voce ARP vengono rilasciati al timeout della voce ARP.*

Per i sistemi con più interfacce di rete, NetX Duo sceglie un'interfaccia basata sull'indirizzo IP di destinazione. La procedura seguente si applica al processo di selezione:

1. Se il mittente specifica un'interfaccia in uscita e l'interfaccia è valida, usare tale interfaccia.
2. Se un indirizzo di destinazione è broadcast IPv4 o multicast, viene utilizzata la prima interfaccia fisica abilitata.
3. Se l'indirizzo di destinazione viene trovato nella tabella di routing statica, viene utilizzata l'interfaccia associata al gateway.
4. Se la destinazione è on-link, viene utilizzata l'interfaccia di collegamento.
5. Se l'indirizzo di destinazione è un indirizzo locale del collegamento (169.254.0.0/16), viene utilizzata la prima interfaccia valida.
6. Se è configurato il gateway predefinito, usare l'interfaccia associata al gateway predefinito per trasmettere il pacchetto.
7. Infine, se uno degli indirizzi IP dell'interfaccia validi è indirizzo locale del collegamento (169.254.0.0/16), questa interfaccia viene utilizzata come indirizzo di origine per la trasmissione.
8. Il pacchetto di output viene eliminato se non si verificano errori.

### <a name="ip-receive"></a>Ricezione IP

L'elaborazione di ricezione IP viene chiamata dal driver di rete o dal thread IP interno (per l'elaborazione dei pacchetti nella coda di pacchetti ricevuta posticipata). L'elaborazione di ricezione IP esamina il campo protocollo e tenta di inviare il pacchetto al componente protocollo appropriato. Prima che il pacchetto venga effettivamente inviato, l'intestazione IP viene rimossa facendo avanzare il puntatore anteposto oltre l'intestazione IP.

L'elaborazione della ricezione IP rileva inoltre i pacchetti IP frammentati ed esegue i passaggi necessari per riassemblarli se la frammentazione è abilitata. Se la frammentazione è necessaria ma non abilitata, il pacchetto viene eliminato.

NetX Duo determina l'interfaccia di rete appropriata in base all'interfaccia specificata nel pacchetto. Se l'interfaccia del pacchetto è NULL, NetX Duo imposta come valore predefinito l'interfaccia primaria. Questa operazione viene eseguita per garantire la compatibilità con i driver Ethernet NetX Duo legacy.

### <a name="raw-ip-send"></a>Invio IP non elaborato

Un pacchetto IP non elaborato è un frame IP che contiene il payload del protocollo di livello superiore non direttamente supportato (ed elaborato) da NetX Duo. Un pacchetto non elaborato consente agli sviluppatori di definire le proprie applicazioni basate su IP. Un'applicazione può inviare pacchetti IP non elaborati direttamente usando il servizio ***nxd_ip_raw_packet_send** _ se l'elaborazione di pacchetti IP non elaborati è stata abilitata con il servizio di _*_nx_ip_raw_packet_enabled_*_ . Quando si trasmette un pacchetto unicast in una rete IPv6, NetX Duo determina automaticamente l'indirizzo IPv6 di origine migliore da usare per inviare i pacchetti in base all'indirizzo di destinazione. Se l'indirizzo di destinazione è un indirizzo multicast (o broadcast per IPv4), tuttavia, NetX Duo utilizzerà per impostazione predefinita la prima interfaccia (primaria). Pertanto, per inviare tali pacchetti alle interfacce secondarie, l'applicazione deve usare il servizio _ *_nx_ip_raw_packet_source_send_** per specificare l'indirizzo di origine da usare per il pacchetto in uscita.

### <a name="raw-ip-receive"></a>Ricezione di indirizzi IP non elaborati

Se l'elaborazione dei pacchetti IP non elaborati è abilitata, l'applicazione può ricevere pacchetti IP non elaborati tramite il servizio ***nx_ip_raw_packet_receive** _. Tutti i pacchetti in ingresso vengono elaborati in base al protocollo specificato nell'intestazione IP. Se il protocollo specifica UDP, TCP, IGMP o ICMP, NetX Duo elaborerà il pacchetto utilizzando il gestore appropriato per il tipo di protocollo del pacchetto. Se il protocollo non è uno di questi protocolli e la ricezione di indirizzi IP non elaborati è abilitata, il pacchetto in arrivo verrà inserito nella coda dei pacchetti non elaborati in attesa che l'applicazione la riceva tramite il _servizio *_nx_ip_raw_packet_receive_**. I thread dell'applicazione possono inoltre sospendere con un timeout facoltativo durante l'attesa di un pacchetto IP non elaborato. Il numero di pacchetti che è possibile accodare nella coda dei pacchetti non elaborati è limitato. Il valore massimo è definito in ***NX_IP_RAW_MAX_QUEUE_DEPTH**, il_ cui valore predefinito è 20. Un'applicazione può modificare il valore massimo chiamando il servizio _ *_nx_ip_raw_receive_queue_max_set_**.

In alternativa, la libreria NetX Duo può essere compilata con ***NX_ENABLE_IP_RAW_PACKET_FILTER *.** In questa modalità di funzionamento, l'applicazione fornisce una funzione di callback che viene richiamata ogni volta che viene ricevuto un pacchetto con un tipo di protocollo non gestito. La logica di ricezione IP invia il pacchetto alla routine di filtro di ricezione dei pacchetti non elaborati definita dall'utente. La routine di filtro decide se memorizzare o meno il pacchetto non elaborato per un processo futuro. Il valore restituito dalla routine di callback indica se il pacchetto è stato elaborato dal filtro di ricezione dei pacchetti non elaborati. Se il pacchetto viene elaborato dalla funzione di callback, il pacchetto deve essere rilasciato dopo che l'applicazione è stata eseguita con il pacchetto. In caso contrario, NetX Duo è responsabile del rilascio del pacchetto. Per ulteriori informazioni sull'utilizzo della funzione di filtro dei pacchetti non elaborati, fare riferimento al **_nx_ip_raw_packet_filter_set_** .

> [!NOTE]
> * La funzione wrapper BSD per NetX duo si basa sulla funzione di filtro dei pacchetti non elaborati per gestire i socket non elaborati BSD. Per supportare il socket non elaborato nel wrapper BSD, è pertanto necessario compilare la libreria NetX Duo con ***NX_ENABLE_IP_RAW_PACKET_FILTER** _ defined e l'applicazione non deve usare il _*_nx_ip_raw_packet_filter_set_*_ per installare il proprio filtro pacchetti non elaborati Functions._

### <a name="default-packet-pool"></a>Pool di pacchetti predefinito

A ogni istanza IP viene assegnato un pool di pacchetti predefinito durante la creazione. Questo pool di pacchetti viene utilizzato per allocare pacchetti per ARP, RARP, ICMP, IGMP, diversi pacchetti di controllo TCP (SYN, ACK e così via), individuazione router adiacenti, individuazione router e rilevamento di indirizzi duplicati. Se il pool di pacchetti predefinito è vuoto quando NetX Duo deve allocare un pacchetto, NetX Duo potrebbe dover interrompere l'operazione specifica e restituirà un messaggio di errore, se possibile.

### <a name="ip-helper-thread"></a>Thread helper IP

Ogni istanza IP ha un thread helper. Questo thread è responsabile della gestione di tutte le operazioni di elaborazione dei pacchetti posticipate e di tutte le elaborazioni periodiche. Il thread helper IP viene creato in ***nx_ip_create.*** Questo è il punto in cui al thread viene assegnato lo stack e la priorità. Si noti che la prima elaborazione nel thread helper IP consiste nel completare l'inizializzazione del driver di rete associata al servizio di creazione IP. Al termine dell'inizializzazione del driver di rete, il thread di supporto avvia un ciclo infinito per elaborare le richieste periodiche e del pacchetto.

> [!IMPORTANT]
> *Se si verifica un comportamento inspiegabile all'interno del thread helper IP, l'aumento delle dimensioni dello stack durante il servizio di creazione IP è il primo passaggio di debug. Se lo stack è troppo piccolo, il thread helper IP potrebbe probabilmente sovrascrivere la memoria, che potrebbe causare problemi insoliti.*

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono sospendere il tentativo di ricevere pacchetti IP non elaborati. Dopo la ricezione di un pacchetto non elaborato, il nuovo pacchetto viene assegnato al primo thread sospeso e il thread viene ripreso. I servizi NetX Duo per la ricezione di pacchetti hanno tutti un timeout di sospensione facoltativo. Quando viene ricevuto un pacchetto o il timeout scade, il thread dell'applicazione viene ripreso con lo stato di completamento appropriato.

### <a name="ip-statistics-and-errors"></a>Statistiche IP ed errori

Se abilitata, NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per ogni istanza IP vengono mantenute le statistiche e i report degli errori seguenti:

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

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_ip_info_get***.

### <a name="ip-control-block-nx_ip"></a>NX_IP del blocco di controllo IP

Le caratteristiche di ogni istanza IP si trovano nel relativo blocco di controllo. Contiene informazioni utili quali gli indirizzi IP e le maschere di rete di ogni dispositivo di rete e una tabella di indirizzi IP adiacenti e mapping di indirizzi hardware fisici. Questa struttura viene definita nel _file ***nx_api. h**. Se IPv6 è abilitato, contiene anche una matrice di indirizzi IPv6, il cui numero è specificato dall'opzione configurabile dall'utente _ *_NX_MAX_IPV6_ADDRESSES_* *. Il valore predefinito consente a ogni interfaccia di rete fisica di avere tre indirizzi IPv6.

I blocchi di controllo dell'istanza IP possono trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione.

### <a name="static-ipv4-routing"></a>Routing IPv4 statico

La funzionalità di routing statico consente a un'applicazione di specificare una rete IPv4 e l'indirizzo hop successivo per indirizzi IP di destinazione specifici fuori rete. Se il routing statico è abilitato, NetX Duo Cerca nella tabella di routing statica una voce corrispondente all'indirizzo di destinazione del pacchetto da inviare. Se non viene trovata alcuna corrispondenza, NetX Duo Cerca nell'elenco di interfacce fisiche e sceglie un indirizzo IP di origine e un indirizzo hop successivo in base all'indirizzo IP di destinazione e al network mask. Se la destinazione non corrisponde ad alcuno degli indirizzi IP dei driver di rete collegati all'istanza IP, NetX Duo sceglie un'interfaccia connessa direttamente al gateway predefinito e usa l'indirizzo IP dell'interfaccia come indirizzo di origine e il gateway predefinito come hop successivo.

Le voci possono essere aggiunte e rimosse dalla tabella di routing statica usando rispettivamente i servizi ***nx_ip_static_route_add** _ e _ *_nx_ip_static_route_delete_**. Per utilizzare il routing statico, l'applicazione host deve abilitare questa funzionalità definendo ***NX_ENABLE_IP_STATIC_ROUTING.***

> [!NOTE]
> *Quando si aggiunge una voce alla tabella di routing statica, NetX duo controlla la presenza di una voce corrispondente per l'indirizzo di destinazione specificato già nella tabella. Se ne esiste uno, fornisce la preferenza alla voce con la rete più piccola (prefisso più lungo) nell'network mask.*

### <a name="ipv4-forwarding"></a>Inoltri IPv4

Se il pacchetto IPv4 in ingresso non è destinato a questo nodo e la funzionalità di invio IPv4 è abilitata, NetX Duo tenta di inviare il pacchetto tramite le altre interfacce.  

### <a name="ip-fragmentation"></a>Frammentazione IP

Il dispositivo di rete potrebbe avere limiti per le dimensioni dei pacchetti in uscita. Questo limite è denominato MTU (Maximum Transmission Unit). MTU IP è la dimensione massima del frame IP che un driver del livello di collegamento è in grado di trasmettere senza frammentazione del pacchetto IP. Durante la fase di inizializzazione di un driver di dispositivo, il modulo driver deve configurare le dimensioni MTU IP tramite il servizio ***nx_ip_interface_mtu_set.***

Sebbene non sia consigliabile, l'applicazione può generare datagrammi di dimensioni superiori rispetto alla MTU IP sottostante supportata dal dispositivo. Prima di trasmettere tale datagramma IP, il livello IP deve frammentare questi pacchetti. Alla ricezione di frame IP frammentati, l'estremità ricevente deve archiviare tutti i frame IP frammentati con lo stesso ID di frammentazione e riassemblarli nell'ordine. Se la logica di ricezione IP non è in grado di raccogliere tutti i frammenti per ripristinare il frame IP originale nel tempo, vengono rilasciati tutti i frammenti. È il protocollo di livello superiore per rilevare tale perdita di pacchetti e ripristinarla.

La frammentazione IP si applica ai pacchetti IPv4 e IPv6.

Per supportare la frammentazione IP e l'operazione di riassemblaggio, progettazione sistema deve abilitare la funzionalità di frammentazione IP in NetX Duo usando il servizio ***nx_ip_fragment_enable*** . Se questa funzionalità non è abilitata, i pacchetti IP frammentati in ingresso vengono eliminati, oltre a pacchetti che superano il MTU del driver di rete.

> [!NOTE]
> * La logica di frammentazione IP può essere rimossa completamente definendo ***NX_DISABLE_FRAGMENTATION** _ quando si compila la libreria NETX Duo. Questa operazione consente di ridurre le dimensioni del codice di NetX Duo. Si noti che in questo caso le funzioni di frammentazione/riassemblaggio IPv4 e IPv6 sono disabled._

> [!NOTE]
> *Se **NX_DISABLE_CHAINED_PACKET** è definito, la frammentazione IP deve essere disabilitata.*

> [!NOTE]
> *In una rete IPv6, i router non frammentano un datagramma se la dimensione del datagramma supera la dimensione MTU minima. Pertanto, spetta al dispositivo mittente determinare il valore MTU minimo tra l'origine e la destinazione e assicurarsi che la dimensione del datagramma IP non superi il valore MTU del percorso. In NetX Duo è possibile abilitare l'individuazione MTU del percorso IPv6 compilando la libreria NetX Duo con il simbolo **NX_ENABLE_IPV6_PATH_MTU_DISCOVERY** definito.*

## <a name="address-resolution-protocol-arp-in-ipv4"></a>ARP (Address Resolution Protocol) in IPv4

Il protocollo ARP (Address Resolution Protocol) è responsabile del mapping dinamico degli indirizzi IPv4 a 32 bit a quelli del supporto fisico sottostante (RFC 826). Ethernet è il supporto fisico più comune e supporta gli indirizzi a 48 bit. La necessità di ARP è determinata dal driver di rete fornito al servizio ***nx_ip_create** _. Se è necessario il mapping fisico, il driver di rete deve usare il servizio _ *_nx_interface_address_mapping_needed_** per configurare correttamente l'interfaccia del driver.

### <a name="arp-enable"></a>Abilitazione ARP

Per il corretto funzionamento di ARP, l'applicazione deve prima essere abilitata dall'applicazione con il servizio ***nx_arp_enable*** . Questo servizio configura varie strutture di dati per l'elaborazione ARP, inclusa la creazione di un'area della cache ARP dalla memoria fornita al servizio di abilitazione ARP.

### <a name="arp-cache"></a>Cache ARP

La cache ARP può essere visualizzata come una matrice di strutture di dati di mapping ARP interne. Ogni struttura interna è in grado di gestire la relazione tra un indirizzo IP e un indirizzo hardware fisico. Ogni struttura di dati dispone inoltre di puntatori di collegamento, in modo che possa essere parte di più elenchi collegati.

L'applicazione può cercare un indirizzo IP dalla cache ARP specificando l'indirizzo MAC hardware usando il servizio ***nx_arp_ip_address_find** _ se il mapping esiste nella tabella ARP. Analogamente, il servizio _ *_nx_arp_hardware_address_find_** restituisce l'indirizzo Mac per un determinato indirizzo IP.

### <a name="arp-dynamic-entries"></a>Voci dinamiche ARP

Per impostazione predefinita, il servizio ARP Enable inserisce tutte le voci della cache ARP nell'elenco delle voci ARP dinamiche disponibili. Una voce ARP dinamica viene allocata da questo elenco di NetX Duo quando viene rilevata una richiesta di invio a un indirizzo IP non mappato. Dopo l'allocazione, la voce ARP viene configurata e viene inviata una richiesta ARP al supporto fisico.

È possibile creare una voce dinamica anche dal servizio ***nx_arp_dynamic_entry_set***.

> [!IMPORTANT]
> *Se tutte le voci ARP dinamiche sono in uso, la voce ARP usata meno di recente viene sostituita con un nuovo mapping.*

### <a name="arp-static-entries"></a>Voci statiche ARP

L'applicazione può anche impostare il mapping ARP statico usando l'_service ***nx_arp_static_entry_create**. Questo servizio alloca una voce ARP dall'elenco di voci ARP dinamiche e la inserisce nell'elenco statico con le informazioni di mapping fornite dall'applicazione. Le voci ARP statiche non sono soggette a riutilizzo o invecchiamento. L'applicazione può eliminare una voce statica utilizzando il servizio _*_nx_arp_static_entry_delete_*_. Per rimuovere tutte le voci statiche nella tabella ARP, è possibile che l'applicazione utilizzi il servizio _ *_nx_arp_static_entries_delete_* *.

### <a name="automatic-arp-entry"></a>Voce ARP automatica

NetX duo registra il mapping IP/MAC del peer dopo le risposte del peer alla richiesta ARP. NetX Duo implementa anche la funzionalità di voce ARP automatica in cui registra il mapping degli indirizzi IP/MAC peer in base alle richieste ARP non richieste dalla rete. Questa funzionalità consente di popolare la tabella ARP con le informazioni sul peer, riducendo il ritardo necessario per il ciclo di richiesta/risposta ARP. Tuttavia, il lato negativo dell'abilitazione di ARP automatico è che la tabella ARP tende a riempirsi rapidamente in una rete occupata con molti nodi sul collegamento locale, il che porterebbe alla sostituzione della voce ARP.

Questa funzionalità è abilitata per impostazione predefinita. Per disabilitarla, è necessario compilare la libreria NetX Duo con il simbolo ***NX_DISABLE_ARP_AUTO_ENTRY*** definito.</p>

### <a name="arp-messages"></a>Messaggi ARP

Come indicato in precedenza, viene inviato un messaggio di richiesta ARP quando l'attività IP rileva che il mapping è necessario per un indirizzo IP. Le richieste ARP vengono inviate periodicamente (ogni ***NX_ARP_UPDATE_RATE** _ secondi) finché non viene ricevuta una risposta ARP corrispondente. Viene eseguito un totale di _ *_NX_ARP_MAXIMUM_RETRIES_** richieste ARP prima che il tentativo ARP venga abbandonato. Quando viene ricevuta una risposta ARP, le informazioni sull'indirizzo fisico associate vengono archiviate nella voce ARP presente nella cache.

Per i sistemi multihome, NetX Duo determina quale interfaccia inviare le richieste e le risposte ARP in base all'indirizzo di destinazione specificato.

> [!NOTE]
> *I pacchetti IP in uscita vengono accodati mentre NetX Duo attende la risposta ARP. Il numero di pacchetti IP in uscita accodati viene definito dalla costante **NX_ARP_MAX_QUEUE_DEPTH**.*

NetX Duo risponde inoltre alle richieste ARP da altri nodi nella rete IPv4 locale. Quando viene effettuata una richiesta ARP esterna che corrisponde all'indirizzo IP corrente dell'interfaccia che riceve la richiesta ARP, NetX Duo compila un messaggio di risposta ARP che contiene l'indirizzo fisico corrente.

I formati delle richieste e delle risposte ARP Ethernet sono illustrati nella figura 6 e sono descritti di seguito.

| **Campo richiesta/risposta &nbsp;**         | **Scopo**            |
| ---------------------------------- | ---------------------- |
| ***Indirizzo di destinazione Ethernet*** | Questo campo di 6 byte contiene l'indirizzo di destinazione per la risposta ARP ed è un broadcast (tutti) per le richieste ARP. Questo campo viene configurato dal driver di rete. 
| ***Indirizzo di origine Ethernet***      | Questo campo di 6 byte contiene l'indirizzo del mittente della richiesta o della risposta ARP e viene configurato dal driver di rete. |
| ***Tipo di frame*** | Questo campo a 2 byte contiene il tipo di frame Ethernet presente e, per le richieste e le risposte ARP, è uguale a 0x0806. Questo è l'ultimo campo che il driver di rete è responsabile della configurazione. |
| ***Tipo di hardware*** | Questo campo a 2 byte contiene il tipo di hardware, ovvero 0x0001 per Ethernet. |
| ***Tipo di protocollo*** | Questo campo a 2 byte contiene il tipo di protocollo, ovvero 0x0800 per gli indirizzi IP. |
| ***Dimensioni hardware*** | Questo campo a 1 byte contiene le dimensioni degli indirizzi hardware, ovvero 6 per gli indirizzi Ethernet. |

![Diagramma del formato del pacchetto ARP.](./media/user-guide/arp-packet-format.png)

**FIGURA 6. Formato del pacchetto ARP**

| Campo richiesta/risposta &nbsp; | Scopo |
|---|---|
| ***Dimensioni protocollo*** | Questo campo a 1 byte contiene le dimensioni dell'indirizzo IP, ovvero 4 per gli indirizzi IP. |
| ***Codice operativo*** | Questo campo a 2 byte contiene l'operazione per questo pacchetto ARP. Una richiesta ARP viene specificata con il valore di 0x0001, mentre una risposta ARP viene rappresentata da un valore di 0x0002. |
| ***Indirizzo Ethernet mittente*** | Questo campo a 6 byte contiene l'indirizzo Ethernet del mittente. |
| ***Indirizzo IP mittente*** | Questo campo a 4 byte contiene l'indirizzo IP del mittente. |
| ***Indirizzo Ethernet di destinazione*** | Questo campo a 6 byte contiene l'indirizzo Ethernet della destinazione. |
| ***Indirizzo IP di destinazione*** | Questo campo a 4 byte contiene l'indirizzo IP della destinazione. |

> [!NOTE]
> *Le richieste e le risposte ARP sono pacchetti a livello Ethernet. Tutti gli altri pacchetti TCP/IP sono incapsulati da un'intestazione del pacchetto IP.*

> [!NOTE]
> *È previsto che tutti i messaggi ARP nell'implementazione TCP/IP siano in formato **Big Endian** . In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

### <a name="arp-aging"></a>Durata ARP

NetX supporta l'invalidamento automatico della voce ARP dinamica. ***NX_ARP_EXPIRATION_RATE** _ specifica il numero di secondi per cui un indirizzo IP stabilito per il mapping fisico rimane valido. Dopo la scadenza, la voce ARP viene rimossa dalla cache ARP. Il tentativo successivo di inviare all'indirizzo IP corrispondente comporterà una nuova richiesta ARP. Impostando _ *_NX_ARP_EXPIRATION_RATE_** su zero, viene disabilitata la durata ARP, che è la configurazione predefinita.

### <a name="arp-defend"></a>Difesa ARP

Quando viene ricevuta una richiesta ARP o un pacchetto di risposta ARP e il mittente ha lo stesso indirizzo IP, che è in conflitto con l'indirizzo IP del nodo, NetX Duo invia una richiesta ARP per tale indirizzo come difesa. Se il pacchetto ARP dei conflitti viene ricevuto più di una volta in 10 secondi, NetX Duo non invia più pacchetti di difesa. L'intervallo predefinito di 10 secondi può essere ridefinito da ***NX_ARP_DEFEND_INTERVAL** _. Questo comportamento segue i criteri specificati in 2.4 (c) di RFC5227. Poiché Windows XP ignora l'annuncio ARP come risposta per il probe ARP, l'utente può definire _ *_NX_ARP_DEFEND_BY_REPLY_** per inviare la risposta ARP come difesa aggiuntiva.

### <a name="arp-statistics-and-errors"></a>Statistiche ed errori ARP

Se abilitata, il software ARP NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per l'elaborazione ARP di ogni IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale richieste ARP inviate
- Totale richieste ARP ricevute
- Totale risposte ARP inviate 
- Totale risposte ARP ricevute 
- Totale voci dinamiche ARP 
- Totale voci statiche ARP 
- Totale voci ARP obsolete 
- Totale messaggi ARP non validi 

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_arp_info_get*** .

## <a name="reverse-address-resolution-protocol-rarp-in-ipv4"></a>Protocollo RARP (Reverse Address Resolution Protocol) in IPv4

Il protocollo RARP (inverso Address Resolution Protocol) è il protocollo per la richiesta di assegnazione di rete degli indirizzi IP a 32 bit dell'host (RFC 903). Questa operazione viene eseguita tramite una richiesta RARP e continua periodicamente finché un membro di rete non assegna un indirizzo IP all'interfaccia di rete host in una risposta RARP. L'applicazione crea un'istanza IP dal servizio ***nx_ip_create*** con un indirizzo IP zero. Se RARP è abilitato dall'applicazione, può usare il protocollo RARP per richiedere un indirizzo IP dal server di rete accessibile tramite l'interfaccia con un indirizzo IP zero.

### <a name="rarp-enable"></a>Abilitazione di RARP

Per usare RARP, l'applicazione deve creare l'istanza IP con un indirizzo IP pari a zero, quindi abilitare RARP usando il servizio ***nx_rarp_enable***. Per i sistemi multihome, almeno un dispositivo di rete associato all'istanza IP deve avere un indirizzo IP uguale a zero. L'elaborazione di RARP invia periodicamente messaggi di richiesta RARP per il sistema NetX duo che richiede un indirizzo IP fino a quando non viene ricevuta una risposta RARP valida con l'indirizzo IP di rete designato. A questo punto, l'elaborazione di RARP è stata completata.

Dopo l'abilitazione di RARP, questo viene disabilitato automaticamente dopo la risoluzione di tutti gli indirizzi di interfaccia. L'applicazione può forzare l'interruzione di RARP utilizzando il servizio ***nx_rarp_disable***.

### <a name="rarp-request"></a>Richiesta RARP

Il formato di un pacchetto di richiesta RARP è quasi identico al pacchetto ARP illustrato nella [Figura 6](#arp-messages). L'unica differenza è che il campo tipo di frame è 0x8035 e il campo del *codice operativo* è 3, che designa una richiesta RARP. Come indicato in precedenza, le richieste RARP verranno inviate periodicamente (ogni ***NX_RARP_UPDATE_RATE*** secondi) finché non viene ricevuta una risposta RARP con l'indirizzo IP assegnato alla rete.

> [!NOTE]
> *È previsto che tutti i messaggi RARP nell'implementazione TCP/IP siano in formato **Big Endian** . In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

### <a name="rarp-reply"></a>Risposta RARP

I messaggi di risposta RARP vengono ricevuti dalla rete e contengono l'indirizzo IP assegnato alla rete per questo host. Il formato di un pacchetto di risposta RARP è quasi identico al pacchetto ARP illustrato nella figura 6. L'unica differenza è che il campo tipo di frame è 0x8035 e il campo del *codice operativo* è 4, che definisce una risposta RARP. Dopo la ricezione, l'indirizzo IP viene configurato nell'istanza IP, la richiesta di RARP periodica è disabilitata e l'istanza IP è ora pronta per le normali operazioni di rete.

Per gli host multihomed, l'indirizzo IP viene applicato all'interfaccia di rete richiedente. Se sono presenti altre interfacce di rete che richiedono ancora un'assegnazione di indirizzi IP, il servizio di RARP periodico continua fino a quando non vengono risolte tutte le richieste di indirizzi IP dell'interfaccia.

> [!NOTE]
> *L'applicazione non deve usare l'istanza IP fino al completamento dell'elaborazione di RARP. Il **nx_ip_status_check** può essere utilizzato dalle applicazioni per attendere il completamento del RARP. Per i sistemi multihome, l'applicazione non deve usare l'interfaccia richiedente fino al completamento dell'elaborazione di RARP su tale interfaccia. È possibile controllare lo stato dell'indirizzo IP nel dispositivo secondario con il servizio **nx_ip_interface_status_check** .*

### <a name="rarp-statistics-and-errors"></a>Statistiche ed errori di RARP

Se abilitata, il software NetX Duo RARP tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per l'elaborazione RARP di ogni IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale richieste RARP inviate
- Totale risposte RARP ricevute
- Totale messaggi non validi RARP

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_rarp_info_get*** .

## <a name="internet-control-message-protocol-icmp"></a>Internet Control Message Protocol (ICMP)

Internet Control Message Protocol per IPv4 (ICMP) è limitato al passaggio delle informazioni sugli errori e sul controllo tra i membri della rete IP. Internet Control Message Protocol per IPv6 (ICMPv6) gestisce anche le informazioni sugli errori e sui controlli ed è necessario per i protocolli di risoluzione degli indirizzi, ad esempio il rilevamento degli indirizzi duplicati (DAD) e la configurazione automatica degli indirizzi senza stato.

Come la maggior parte degli altri livelli applicazione (ad esempio TCP/IP), i messaggi ICMP e ICMPv6 sono incapsulati da un'intestazione IP con la designazione del protocollo ICMP (o ICMPv6).

### <a name="icmp-statistics-and-errors"></a>Statistiche ed errori ICMP

Se abilitata, NetX Duo tiene traccia di diversi errori e statistiche ICMP che possono risultare utili per l'applicazione. Per l'elaborazione ICMP di ogni IP vengono mantenute le statistiche e i report degli errori seguenti: 

- Totale ping ICMP inviati  
- Timeout totali ping ICMP 
- Totale thread ping ICMP sospesi 
- Totale risposte ping ICMP ricevute 
- Totale errori di checksum ICMP 
- Totale messaggi non gestiti ICMP 

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_icmp_info_get*** .

## <a name="icmpv4-services-in-netx-duo"></a>Servizi ICMPv4 in NetX Duo

### <a name="icmpv4-enable"></a>Abilitazione di ICMPv4

Prima che i messaggi ICMPv4 possano essere elaborati da NetX Duo, l'applicazione deve chiamare il servizio ***nx_icmp_enable*** per abilitare l'elaborazione del ICMPv4. Al termine di questa operazione, l'applicazione può emettere richieste ping e i pacchetti ping in ingresso del campo.  

### <a name="icmpv4-echo-request"></a>Richiesta echo ICMPv4

Una richiesta echo è un tipo di messaggio ICMPv4 che viene in genere usato per verificare l'esistenza di un nodo specifico nella rete, come identificato dall'indirizzo IP dell'host. Il popolare comando ping viene implementato utilizzando i messaggi ICMP Echo Request/Echo Reply. Se l'host specifico è presente, lo stack di rete elabora la richiesta e le risposte ping con una risposta ping. Figura 7 dettagli del formato del messaggio ping ICMPv4.

![Messaggio ping ICMPv4](./media/user-guide/icmpv4-ping-message.png)  

**FIGURA 7. Messaggio ping ICMPv4**

> [!NOTE]
> *Tutti i messaggi ICMPv4 nell'implementazione di TCP/IP devono essere nel formato **Big Endian** . In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

Di seguito viene descritto il formato dell'intestazione ICMPv4:

|Campo di intestazione |Scopo |
|---|---|
|**Tipo** |Questo campo specifica il messaggio ICMPv4 (BITS 31-24). I più comuni sono:<br />-0: risposta echo<br />-3: destinazione non raggiungibile<br />-8: richiesta echo<br />-11: tempo superato<br />-12: problema del parametro |
|**Codice** |Questo campo è specifico del contesto nel campo del tipo (BITS 23-16). Per una richiesta o una risposta echo il codice è impostato su zero.|
|**Checksum** |Questo campo contiene il checksum a 16 bit della somma di complemento a uno del messaggio ICMPv4, inclusa l'intera intestazione ICMPv4 che inizia con il campo tipo. Prima di generare il checksum, il campo checksum viene cancellato.|
|**Identificazione** | Questo campo contiene un valore ID che identifica l'host. un host deve usare l'ID Estratto da una richiesta ECHO nella risposta ECHO (BITS 31-16).|
|**Numero di sequenza** |Questo campo contiene un valore ID. un host deve usare l'ID Estratto da una richiesta ECHO nella risposta ECHO (BITS 31-16). Diversamente dal campo identificatore, questo valore verrà modificato in una richiesta echo successiva dallo stesso host (BITS 15-0).|

### <a name="icmpv4-echo-response"></a>Risposta echo ICMPv4    
Una risposta ping è un altro tipo di messaggio ICMP generato internamente dal componente ICMP in risposta a una richiesta ping esterna. Oltre al riconoscimento, la risposta ping contiene anche una copia dei dati utente forniti nella richiesta ping.

### <a name="icmpv4-error-messages"></a>Messaggi di errore ICMPv4   
In NetX Duo sono supportati i seguenti messaggi di errore ICMPv4: 
- Destinazione non raggiungibile 
- Tempo massimo 
- Problema di parametro

## <a name="internet-group-management-protocol-igmp"></a>IGMP (Internet Group Management Protocol)

Il protocollo IGMP (Internet Group Management Protocol) fornisce un dispositivo per comunicare con gli elementi adiacenti e i relativi router che intende ricevere o aggiungere un gruppo multicast IPv4 (RFC 1112 e RFC 2236). Un gruppo multicast è essenzialmente una raccolta dinamica di membri di rete ed è rappresentato da un indirizzo IP di classe D. I membri del gruppo multicast possono uscire in qualsiasi momento e i nuovi membri possono partecipare in qualsiasi momento. Il coordinamento necessario per l'aggiunta e l'uscita del gruppo è la responsabilità di IGMP.

> [!NOTE]
> *IGMP è progettato solo per i gruppi multicast IPv4. Non può essere utilizzato nella rete IPv6.*

### <a name="igmp-enable"></a>Abilitazione IGMP     
Prima che qualsiasi attività multicast possa essere eseguita in NetX Duo, l'applicazione deve chiamare il servizio ***nx_igmp_enable*** . Questo servizio esegue l'inizializzazione IGMP di base per la preparazione delle richieste multicast.

### <a name="multicast-ipv4-addressing"></a>Indirizzamento IPv4 multicast  
Come indicato in precedenza, gli indirizzi multicast sono effettivamente di classe D indirizzi IP, come illustrato nella [Figura 4](#ipv4-addresses). I 28 bit inferiori dell'indirizzo della classe D corrispondono all'ID del gruppo multicast. Sono disponibili una serie di indirizzi multicast predefiniti. Tuttavia, l' *Indirizzo All Hosts* (244.0.0.1) è particolarmente importante per l'elaborazione IGMP. L' *indirizzo tutti gli host* viene usato dai router per eseguire una query su tutti i membri multicast per segnalare i gruppi multicast a cui appartengono.  

### <a name="physical-address-mapping-in-ipv4"></a>Mapping degli indirizzi fisici in IPv4
Gli indirizzi multicast della classe D vengono mappati direttamente agli indirizzi Ethernet fisici compresi tra 01.00.5 e 00.00.00 tramite 01.00.5 e 7F. FF. FF. I 23 bit inferiori della mappa indirizzi IP multicast direttamente ai 23 bit inferiori dell'indirizzo Ethernet.

### <a name="multicast-group-join"></a>Join gruppo multicast
Le applicazioni che devono partecipare a un particolare gruppo multicast possono eseguire questa operazione chiamando il servizio ***nx_igmp_multicast_join*** . Questo servizio tiene traccia del numero di richieste da unire in join a questo gruppo multicast. Se si tratta della prima applicazione requestto join al gruppo multicast, viene inviato un report IGMP sulla rete primaria indicante che l'intenzione di questo host è partecipare al gruppo. Successivamente, il driver di rete viene chiamato per configurare per l'ascolto dei pacchetti con l'indirizzo Ethernet per questo gruppo multicast.

In un sistema multihome, se il gruppo multicast è accessibile tramite un'interfaccia specifica, l'applicazione deve usare il servizio ***nx_igmp_multicast_interface_join** _ invece di _ *_nx_igmp_multicast_join_* *, che è limitato ai gruppi multicast nella rete primaria.

### <a name="multicast-group-leave"></a>Uscita gruppo multicast   
Le applicazioni che devono lasciare un gruppo multicast precedentemente aggiunto possono eseguire questa operazione chiamando il servizio ***nx_igmp_multicast_leave*** . Questo servizio riduce il numero interno associato al numero di volte in cui è stato aggiunto il gruppo. Se non sono presenti richieste di join in attesa per un gruppo, il driver di rete viene chiamato per disabilitare l'ascolto dei pacchetti con l'indirizzo Ethernet del gruppo multicast.

### <a name="multicast-loopback"></a>Loopback multicast    
Un'applicazione potrebbe voler ricevere il traffico multicast originato da una delle origini nello stesso nodo. A questo scopo, il componente multicast IP deve avere il loopback abilitato utilizzando il servizio ***nx_igmp_loopback_enable***.

### <a name="igmp-report-message"></a>Messaggio report IGMP      
Quando l'applicazione viene aggiunta a un gruppo multicast, viene inviato un messaggio di report IGMP tramite la rete per indicare che l'intenzione dell'host deve essere aggiunta a un particolare gruppo multicast. Il formato del messaggio del report IGMP è illustrato nella figura 8. L'indirizzo del gruppo multicast viene utilizzato sia per il messaggio di gruppo nel messaggio del report IGMP che per l'indirizzo IP di destinazione.

Nella figura precedente (Figura 8), l'intestazione IGMP contiene un campo versione/tipo, risposta massima

![Diagramma di un messaggio di report IGMP.](./media/user-guide/image17.jpg)

**FIGURA 8. Messaggio report IGMP**

Time, un campo checksum e un campo Address gruppo multicast. Per i messaggi IGMPv1, il campo tempi di risposta massimi è sempre impostato su zero, perché non fa parte del protocollo IGMPv1. Il campo tempo di risposta massimo viene impostato quando l'host riceve un messaggio IGMP di tipo query e viene cancellato quando un host riceve il messaggio del tipo di report di un altro host come definito dal protocollo IGMPv2.

Di seguito viene descritto il formato di intestazione IGMP:

|Campo di intestazione|Scopo|
|---|---|
|**Versione** |Questo campo specifica la versione IGMP (BITS 31-28).|
|**Tipo** |Questo campo specifica il tipo di messaggio IGMP (BITS 27 -24).|
|**Tempo di risposta massimo** |Non utilizzato in IGMP v1. In IGMP V2 questo campo funge da tempo di risposta massimo.|
|**Checksum** |Questo campo contiene il checksum a 16 bit della somma del complemento a uno del messaggio IGMP che inizia con la versione IGMP (BITS 0-15)|
|**Indirizzo del gruppo** |Indirizzo IP del gruppo di classe D a 32 bit|

I messaggi di report IGMP vengono inviati anche in risposta ai messaggi di query IGMP inviati da un router multicast. I router multicast inviano periodicamente messaggi di query per vedere quali host richiedono ancora l'appartenenza al gruppo. I messaggi di query hanno lo stesso formato del messaggio di report IGMP illustrato nella figura 8. Le uniche differenze sono il tipo IGMP è uguale a 1 e il campo Indirizzo gruppo è impostato su 0. I messaggi di query IGMP vengono inviati all'indirizzo IP *tutti gli host* dal router multicast. Un host che desidera comunque mantenere l'appartenenza al gruppo risponde inviando un altro messaggio di report IGMP.

> [!NOTE]
> *È previsto che tutti i messaggi nell'implementazione TCP/IP siano in formato **Big Endian** . In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

### <a name="igmp-statistics-and-errors"></a>Statistiche ed errori IGMP    
<th><p>Se abilitata, il software IGMP NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per l'elaborazione IGMP di ogni IP vengono mantenute le statistiche e i report degli errori seguenti: 

- Totale report IGMP inviati 
- Totale query IGMP ricevute 
- Totale errori di checksum IGMP 
- Totale gruppi correnti IGMP aggiunti 

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_igmp_info_get***. 

### <a name="multicast-without-igmp"></a>Multicast senza IGMP  
L'applicazione che prevede il traffico multicast IPv4 può aggiungere un indirizzo di gruppo multicast senza richiamare messaggi IGMP utilizzando il servizio ***nx_ipv4_multicast_interface_join***. Questo servizio indica al livello IPv4 e al driver di interfaccia sottostante di accettare i pacchetti dall'indirizzo multicast IPv4 designato. Tuttavia, non vengono inviati o elaborati messaggi di gestione gruppi IGMP per questo gruppo.

L'applicazione non vuole più ricevere traffico dal gruppo può usare il servizio ***nx_ipv4_multicast_interface_leave.***

## <a name="ipv6-in-netx-duo"></a>IPv6 in NetX Duo

### <a name="ipv6-addresses"></a>Indirizzi IPv6   
Gli indirizzi IPv6 sono di 128 bit. L'architettura dell'indirizzo IPv6 è descritta nella specifica RFC 4291. L'indirizzo è diviso in un prefisso contenente i bit più significativi e un indirizzo host contenente i bit inferiori. Il prefisso indica il tipo di indirizzo ed è approssimativamente l'equivalente dell'indirizzo di rete nella rete IPv4.

IPv6 presenta tre tipi di specifiche di indirizzo: unicast, anycast (non supportato in NetX Duo) e multicast. Gli indirizzi unicast sono gli indirizzi IP che identificano un host specifico su Internet. Gli indirizzi unicast possono essere un indirizzo IP di origine o di destinazione. Indirizzi multicast specificare un gruppo dinamico di host su Internet. I membri del gruppo multicast possono partecipare e lasciare ogni volta che desiderano.

IPv6 non dispone dell'equivalente del meccanismo di trasmissione IPv4. La possibilità di inviare un pacchetto a tutti gli host può essere eseguita inviando un pacchetto al gruppo multicast tutti gli host locale del collegamento.

IPv6 utilizza indirizzi multicast per eseguire le procedure di individuazione router adiacenti, individuazione router e configurazione automatica degli indirizzi senza stato.

Esistono due tipi di indirizzi unicast IPv6: collegare indirizzi locali, in genere costruiti combinando il prefisso locale di collegamento noto con l'indirizzo MAC dell'interfaccia e gli indirizzi IP globali, che hanno anche la parte prefisso e la parte dell'ID host. Un indirizzo globale può essere configurato manualmente oppure tramite la configurazione automatica degli indirizzi senza stato o DHCPv6. NetX Duo supporta sia l'indirizzo locale del collegamento che l'indirizzo globale.

Per supportare sia i formati IPv4 che IPv6, NetX Duo fornisce un nuovo tipo di dati, NXD_ADDRESS, per contenere gli indirizzi IPv4 e IPv6. La definizione di questa struttura è illustrata di seguito. Il campo Address è un'Unione di indirizzi IPv4 e IPv6.

```c
typedef struct NXD_ADDRESS_STRUCT
{
    ULONG nxd_ip_version;
    union
    {
        ULONG v4;
        ULONG v6[4];
    } nxd_ip_address;
} NXD_ADDRESS;
```

Nella struttura NXD_ADDRESS il primo elemento, *nxd_ip_version*, indica la versione IPv4 o IPv6. I valori supportati sono NX_IP_VERSION_V4 o NX_IP_VERSION_V6. *nxd_ip_version* indica il campo nell'Unione *nxd_ip_address* da utilizzare come indirizzo IP. I servizi API NetX Duo accettano in genere un puntatore alla struttura NXD_ADDRESS come argomento di input, anziché l'indirizzo IP ULONG (32 bit).

### <a name="link-local-addresses"></a>Collega indirizzi locali     
Un indirizzo locale del collegamento è valido solo nella rete locale. Un dispositivo può inviare e ricevere pacchetti a un altro dispositivo nella stessa rete dopo che è stato assegnato un indirizzo locale collegamento valido. Un'applicazione assegna un indirizzo locale rispetto al collegamento chiamando il ***nxd_ipv6_address_set*** del servizio NETX Duo, con il parametro della lunghezza del prefisso impostato su 10. L'applicazione può fornire un indirizzo locale al collegamento al servizio oppure può semplicemente usare NX_NULL come indirizzo locale del collegamento e consentire a NetX duo di creare un indirizzo locale del collegamento in base all'indirizzo MAC del dispositivo.

L'esempio seguente indica a NetX duo di configurare l'indirizzo locale del collegamento con una lunghezza del prefisso pari a 10 nel dispositivo primario (indice 0) usando il relativo indirizzo MAC:

```c
nxd_ipv6_address_set(ip_ptr, 0, NX_NULL, 10, NX_NULL);
```
Nell'esempio precedente, se l'indirizzo MAC dell'interfaccia è 54:32:10:1A: BC: 67, l'indirizzo locale rispetto al collegamento corrispondente sarà:

```c
FE80::5632:10FF:FE1A:BC67
```
Si noti che la parte relativa all'ID host dell'indirizzo IPv6 (**5632:10FF: FE1A: BC67**) è costituita dall'indirizzo Mac a 6 byte, con le modifiche seguenti:

- **0xFFFE** inserito tra i byte 3 e 4 byte dell'indirizzo Mac
- Il secondo bit più basso del primo byte dell'indirizzo MAC (U/L bit) è impostato su 1

Vedere la specifica RFC 2464 (trasmissione di pacchetti IPv6 su rete Ethernet) per ulteriori informazioni su come costruire la parte host di un indirizzo IPv6 dall'indirizzo MAC dell'interfaccia.

Sono disponibili alcuni indirizzi multicast speciali per l'invio di messaggi multicast a uno o più host in IPv6:

| Group  | Indirizzo   | Descrizione  |
|---|---|---|
|Gruppo tutti i nodi |**FF02:: 1** |Tutti gli host nella rete locale|
|Gruppo tutti i router |**FF02:: 2** |Tutti i router nella rete locale|
|Nodo sollecitato |**FF02:: 1: FF00:0/104** |Illustrato di seguito|

Un indirizzo multicast del nodo richiesto è destinato a host specifici nel collegamento locale anziché a tutti gli host IPv6. È costituito dal prefisso **FF02:: 1: FF00:0/104**, che corrisponde a 104 bit e agli ultimi 24 bit dell'indirizzo IPv6 di destinazione. Ad esempio, un indirizzo IPv6 **205B: 209D: D028:: F058: D1C8:1024** ha un indirizzo multicast Solicitednode indirizzo **FF02:: 1: FFC8:1024**.

> [!IMPORTANT]
> *La notazione con due punti e virgola indica che i bit intermedi sono tutti zeri. **FF02:: 1: FF00:0/104** completamente espanso* , ad esempio **FF02:0000:0000:0000:0000:0001: FF00:0000**

### <a name="global-addresses"></a>Indirizzi globali    
Un esempio di indirizzo globale IPv6 è **2001:0123:4567:89AB: CDEF:: 1** NETX Duo archivia gli indirizzi IPv6 nella struttura NXD_ADDRESS. Nell'esempio seguente, la variabile NXD_ADDRESS **global_ipv6_address** contiene un indirizzo IPv6 unicast. Nell'esempio seguente viene illustrato un dispositivo NetX Duo per la creazione di un indirizzo globale IPv6 specifico per il dispositivo primario:

```c
NXD_ADDRESS global_ipv6_address;
UINT        primary_interface_index = 0;

global_ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
global_ipv6_address.nxd_ip_address.v6[0] = 0x20010123;
global_ipv6_address.nxd_ip_address.v6[1] = 0x456789AB;
global_ipv6_address.nxd_ip_address.v6[2] = 0xCDEF0000;
global_ipv6_address.nxd_ip_address.v6[3] = 0x00000001;

status = nxd_ipv6_address_set(
            &ip_0,
            primary_interface_index,
            &global_ipv6_address,
            64,
            NX_NULL);
```
Si noti che il prefisso di questo indirizzo IPv6 è **2001:0123:4567:89AB**, che è lunga 64 bit ed è una lunghezza del prefisso comune per gli indirizzi IPv6 unicast globali su Ethernet.

La struttura NXD_ADDRESS include anche indirizzi IPv4. Un indirizzo IP di **192.1.168.10** (**0xC001A80A**) archiviato in global_ipv4_address avrà il layout di memoria seguente:

|Campo |valore |
|---|---|
|global_ipv4_address global_ipv4_address.nxd_ip_version |NX_IP_VERSION_V4|
|global_ipv4_address global_ipv4_address.nxd_ip_address. v4 |0xC001A80A|

Quando un'applicazione passa un indirizzo ai servizi NetX Duo, il campo *nxd_ip_version* deve specificare la versione IP corretta per la gestione dei pacchetti corretta.

Per garantire la compatibilità con le applicazioni NetX esistenti, NetX Duo supporta tutti i servizi NetX. Internamente, NetX Duo converte il tipo di indirizzo IPv4 ULONG in un tipo di dati NXD_ADDRESS prima di inviarlo al servizio NetX Duo effettivo.

Nell'esempio seguente viene illustrata la somiglianza e le differenze tra i servizi in NetX e NetX Duo.

```c
/* Make a connection to the destination IPv4 address
   192.1.168.12 through an already created TCP socket bound
   to the well known HTTP port number 80. */

global_ipv4_address.nxd_ip_version = NX_IP_VERSION_V4;
global_ipv4_address.nxd_ip_address.v4 = 0xC001A80C;

nxd_tcp_client_socket_connect(&tcp_socket,
                              &global_ipv4_address,
                              port_number,
                              NX_WAIT_FOREVER);
```

L'API NetX equivalente è la seguente:

```c
ULONG         server_ip = 0xC001A80C;
NX_TCP_SOCKET tcp_socket;
UINT          port_number = 80;

nx_tcp_client_socket_connect(&tcp_socket,
                             server_ip,
                             port_number,
                             NX_WAIT_FOREVER); 
```

> [!IMPORTANT]
> *Gli sviluppatori di applicazioni sono invitati a usare la versione NXD di queste API*.

### <a name="ipv6-default-routers"></a>Router predefiniti IPv6    
IPv6 usa un router predefinito per inoltrare i pacchetti alle destinazioni offlink. Il servizio NetX Duo ***nxd_ipv6_default_router_add*** consente a un'applicazione di aggiungere un router IPv6 alla tabella dei router predefiniti. Per altri servizi router predefiniti offerti da NetX Duo, vedere il capitolo 4 "Descrizione dei servizi".  

Quando si inoltrano pacchetti IPv6, NetX Duo verifica innanzitutto se la destinazione del pacchetto è on-link. In caso contrario, NetX duo controlla la tabella di routing predefinita per un router valido per l'inoltro del pacchetto fuori collegamento a.  

Per rimuovere un router dalla tabella dei router predefiniti IPv6, l'applicazione deve utilizzare il servizio ***nxd_ipv6_default_router_delete** _. Per ottenere le voci della tabella dei router predefiniti IPv6, utilizzare il servizio _ *_nxd_ipv6_default_router_entry_get_* *.

### <a name="ipv6-header"></a>Intestazione IPv6    
L'intestazione IPv6 è stata modificata dall'intestazione IPv4. Quando si alloca un pacchetto, il chiamante specifica il protocollo dell'applicazione (ad esempio UDP, TCP), le dimensioni del buffer in byte e il limite di hop.   

Nella figura 9 è illustrato il formato dell'intestazione IPv6 e la tabella elenca i componenti dell'intestazione.

![Diagramma del formato dell'intestazione IPv6.](./media/user-guide/image18.png)

**FIGURA 9. Formato dell'intestazione IPv6**

|Intestazione IP | Scopo |
|---|---|
|Versione |campo a 4 bit per la versione IP. Per le reti IPv6, il valore in questo campo deve essere 6; Per le reti IPv4 deve essere 4.|
|Classe di traffico |campo a 8 bit in cui sono archiviate le informazioni sulla classe di traffico. Questo campo non viene usato da NetX Duo.|
|Etichetta flusso |campo a 20 bit per identificare in modo univoco il flusso, se presente, a cui è associato un pacchetto. Un valore pari a zero indica che il pacchetto non appartiene a un determinato flusso. Questo campo sostituisce il campo *TOS* in IPv4.|
|Lunghezza del payload |campo a 16 bit che indica la quantità di dati in byte del pacchetto IPv6 che segue l'intestazione di base IPv6. Sono inclusi tutti i dati e l'intestazione del protocollo incapsulato.|
|Intestazione successiva | campo a 8 bit che indica il tipo dell'intestazione dell'estensione che segue l'intestazione di base IPv6. Questo campo sostituisce il campo *protocollo* in IPv4.|
|Limite hop |campo a 8 bit che limita il numero di router a cui il pacchetto può passare. Questo campo sostituisce il campo *TTL* in IPv4.|
|Indirizzo di origine |campo a 128 bit che archivia l'indirizzo IPv6 del mittente.|
|Indirizzo di destinazione |campo a 128 bit che piaghe l'indirizzo IPv6 della destinazione.|

### <a name="enabling-ipv6-in-netx-duo"></a>Abilitazione di IPv6 in NetX Duo    
Per impostazione predefinita, IPv6 è abilitato in NetX Duo. I servizi IPv6 sono abilitati in NetX Duo Se l'opzione configurabile ***NX_DISABLE_IPV6** _ in _nx_user. h * non è definita. Se ***NX_DISABLE_IPV6*** è stato definito, NETX Duo offrirà solo servizi IPv4 e tutti i moduli e i servizi relativi a IPv6 non saranno incorporati nella libreria NETX Duo.

Il servizio seguente viene fornito per le applicazioni per la configurazione dell'indirizzo IPv6 del dispositivo: ***nxd_ipv6_address_set***

Oltre a impostare manualmente gli indirizzi IPv6 del dispositivo, il sistema può usare anche la configurazione automatica degli indirizzi senza stato. Per usare questa opzione, l'applicazione deve chiamare ***nxd_ipv6_enable** _ per avviare i servizi IPv6 nel dispositivo. Inoltre, è necessario avviare i servizi ICMPv6 chiamando _*_nxd_icmp_enable_*_, che consente a NETX duo di eseguire servizi quali la richiesta di router, l'individuazione dei router adiacenti e il rilevamento di indirizzi duplicati. Si noti che _*_nx_icmp_enable_*_ avvia solo ICMP per i servizi IPv4. _*_nxd_icmp_enable_*_ avvia i servizi ICMP sia per IPv4 che per IPv6. Se il sistema non necessita di servizi ICMPv6, è possibile usare _ *_nx_icmp_enable_**, in modo che il modulo ICMPv6 non sia collegato al sistema.

Nell'esempio seguente viene illustrata una tipica procedura di inizializzazione IPv6 di NetX Duo.

```c
/* Assume ip_0 has been created and IPv4 services (such as ARP,
   ICMP, have been enabled. */
#define SECONDARY_INTERFACE 1

/* Enable IPv6 */
status = nxd_ipv6_enable(&ip_0);

if(status != NX_SUCCESS)
{
    /* nxd_ipv6_enable failed. */
}

/* Enable ICMPv6 */
status = nxd_icmp_enable(&ip_0);
if(status != NX_SUCCESS)
{
    /* nxd_icmp_enable failed. */
}

/* Configure the link local address on the primary interface. */
status = nxd_ipv6_address_set(&ip_0, 0, NX_NULL, 10, NX_NULL);

/* Configure ip_0 primary interface global address. */
ip_address.nxd_ip_version = NX_IP_VERSION_V6
ip_address.nxd_ip_address.v6[0] = 0x20010db8;
ip_address.nxd_ip_address.v6[1] = 0x0000f101;
ip_address.nxd_ip_address.v6[2] = 0;
ip_address.nxd_ip_address.v6[3] = 0x202;

/* Configure global address of the primary interface. */
status = nxd_ipv6_address_set(&ip_0, SECONDARY_INTERFACE,
                              &ip_address, 64, NX_NULL);
```                              

I protocolli di livello superiore (ad esempio TCP e UDP) possono essere abilitati prima o dopo l'avvio di IPv6.

> [!IMPORTANT]  
> *I servizi IPv6 sono disponibili solo dopo l'inizializzazione del thread IP e l'abilitazione del dispositivo.*

Una volta abilitata l'interfaccia (ad esempio, il driver di dispositivo dell'interfaccia è pronto per l'invio e la ricezione dei dati ed è stato ottenuto un indirizzo locale di collegamento valido), il dispositivo può ottenere indirizzi IPv6 globali con uno dei metodi seguenti:

- Configurazione automatica degli indirizzi senza stato;  
- Configurazione manuale degli indirizzi IPv6;  
- Configurazione degli indirizzi tramite DHCPv6 (con pacchetto DHCPv6 facoltativo)

I primi due metodi sono descritti di seguito. Il terzo metodo (DHCPv6) viene descritto nel pacchetto DHCP.

### <a name="stateless-address-autoconfiguration-using-router-solicitation"></a>Configurazione automatica degli indirizzi senza stato con richiesta router      
I dispositivi NetX Duo possono configurare automaticamente le interfacce quando si è connessi a una rete IPv6 con un router che fornisce informazioni sul prefisso. I dispositivi che richiedono la configurazione automatica degli indirizzi senza stato inviano messaggi di richiesta router (RS). I router nella rete rispondono ai messaggi di annuncio router (RA) richiesti. I messaggi RA pubblicizzano i prefissi che identificano gli indirizzi di rete associati a un collegamento. I dispositivi generano quindi un identificatore univoco per la rete a cui è collegato il dispositivo. L'indirizzo viene formato combinando il prefisso e il relativo identificatore univoco. In questo modo, sulla ricezione dei messaggi RA, gli host generano il proprio indirizzo IP. I router possono anche inviare messaggi RA non richiesti periodici. 

> [!WARNING]
> *NETX Duo consente a un'applicazione di abilitare o disabilitare la configurazione automatica degli indirizzi senza stato in fase di esecuzione. Per abilitare questa funzionalità, è necessario compilare la libreria NetX Duo con **NX_IPV6_STATELESS_AUTOCONFIG_CONTROL** definito. Quando questa funzionalità è abilitata, le applicazioni possono usare **nxd_ipv6_stateless_address_autoconfigure_enable** e **nxd_ipv6_stateless_address_autocofigure_disable** per abilitare o disabilitare la configurazione automatica degli indirizzi* senza stato IPv6.

### <a name="manual-ipv6-address-configuration"></a>Configurazione manuale degli indirizzi IPv6     
Se è necessario un indirizzo IPv6 specifico, è possibile che l'applicazione utilizzi ***nxd_ipv6_address_set*** per configurare manualmente un indirizzo IPv6. Un'interfaccia di rete può avere più indirizzi IPv6. Tuttavia, tenere presente che il numero totale di indirizzi IPv6 in un sistema, ottenuti tramite la configurazione automatica degli indirizzi senza stato o tramite la configurazione manuale, non può superare ***NX_MAX_IPV6_ADDRESSES***.

Nell'esempio seguente viene illustrato come configurare manualmente un indirizzo globale nell'interfaccia principale (dispositivo 0) in ip_0:

```c
NXD_ADDRESS global_address;
global_address.nxd_ip_version = NX_IP_VERSION_V6;
global_address.nxd_ip_address.v6[0] = 0x20010000;
global_address.nxd_ip_address.v6[1] = 0x00000000;
global_address.nxd_ip_address.v6[2] = 0x00000000;
global_address.nxd_ip_address.v6[3] = 0x0000ABCD;
```

L'host chiama quindi il servizio NetX Duo seguente per assegnare questo indirizzo come indirizzo IP globale:

```c
status = nxd_ipv6_address_set(&ip_0, 0,  
                              &global_address, 64
                              NX_NULL);
```

### <a name="duplicate-address-detection-dad"></a>Rilevamento degli indirizzi duplicati (DAD)    
Dopo la configurazione dell'indirizzo IPv6 da parte di un sistema, l'indirizzo viene contrassegnato come *provvisorio*. Se il rilevamento degli indirizzi duplicati (DAD), descritto nella specifica RFC 4862, è abilitato, NetX Duo invia automaticamente i messaggi di richiesta router adiacente (NS) con questo indirizzo provvisorio come destinazione. Se nessun host nella rete risponde a questi messaggi NS entro un determinato periodo di tempo, si presuppone che l'indirizzo sia univoco nel collegamento locale e che il relativo stato sia transito allo stato valido. A questo punto, l'applicazione può iniziare a usare questo indirizzo IP per la comunicazione.  

La funzionalità DAD fa parte del modulo ICMPv6. Pertanto, l'applicazione deve abilitare i servizi ICMPv6 prima che un indirizzo appena configurato possa passare attraverso il processo padre. In alternativa, è possibile disattivare il processo padre definendo l'opzione ***NX_DISABLE_IPV6_DAD** _ nell'ambiente di compilazione della libreria NETX Duo (definito come _*_nx_user. h_*_). Durante il processo padre, il parametro _*_NX_IPV6_DAD_TRANSMITS_*_ determina il numero di messaggi NS inviati da NETX duo senza ricevere una risposta per determinare se l'indirizzo è univoco. Per impostazione predefinita, e consigliato da RFC 4862, _ *_NX_IPV6_DAD_TRANSMITS_** è impostato su 3. Se si imposta questo simbolo su zero, il padre viene disabilitato in modo efficace.

Se ICMPv6 o DAD non è abilitato nel momento in cui l'applicazione assegna un indirizzo IPv6, il padre non viene eseguito e NetX Duo imposta lo stato dell'indirizzo IPv6 su valido immediatamente.

NetX Duo non è in grado di comunicare sulla rete IPv6 finché il relativo collegamento locale e/o indirizzo globale non è valido. Una volta ottenuto un indirizzo valido, NetX Duo tenta di trovare una corrispondenza tra l'indirizzo di destinazione di un pacchetto in ingresso e uno degli indirizzi IPv6 configurati o un indirizzo multicast abilitato. Se non viene trovata alcuna corrispondenza, il pacchetto viene eliminato. 

> [!WARNING]  
> * Durante il processo di DAD, il numero di pacchetti NS di DAD da trasmettere viene definito da ***NX_IPV6_DAD_TRANSMITS**_, che per impostazione predefinita è 3, e per impostazione predefinita esiste un ritardo di un secondo tra ogni messaggio NS di dad inviato. Pertanto, in un sistema con DAD abilitato, dopo l'assegnazione di un indirizzo IPv6 (e presumendo che non si tratta di un indirizzo duplicato), si verifica un ritardo di circa 3 secondi prima che l'indirizzo IP sia in uno stato valido ed è pronto per la comunicazione._

Le applicazioni potrebbero voler ricevere notifiche quando vengono modificati gli indirizzi IPv6 nel sistema. Per abilitare la funzionalità di notifica delle modifiche degli indirizzi IPv6, è necessario compilare la libreria NetX Duo con il simbolo **NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY** definito. Una volta abilitata la funzionalità, le applicazioni possono installare la funzione di callback usando il servizio **_nxd_ipv6_address_change_notify_** .

Quando viene modificato un indirizzo IPv6 o diventa non valido, viene richiamata la funzione di callback fornita dall'utente con le informazioni seguenti:

| Funzione  | Descrizione  |
|---|---|
|ip_ptr |Puntatore all'istanza IP|
|interface_index |Indice dell'interfaccia di rete a cui è associato l'indirizzo IPv6
|ipv6_addr_index |Indice della tabella degli indirizzi IPv6|
|ipv6_address |Puntatore all'indirizzo IPv6, sotto forma di matrice di quattro Integer ULONG. Gli indirizzi Pv6 vengono presentati in ordine byte host.|

### <a name="ipv6-multicast-support-in-netx-duo"></a>Supporto multicast IPv6 in NetX Duo      
Indirizzi multicast specificare un gruppo dinamico di host su Internet. I membri del gruppo multicast possono partecipare e lasciare ogni volta che desiderano. NetX Duo implementa diversi protocolli ICMPv6, tra cui il rilevamento degli indirizzi duplicati, l'individuazione dei router adiacenti e l'individuazione dei router, che richiedono la funzionalità multicast IP. NetX duo prevede pertanto che il driver di dispositivo sottostante supporti le operazioni multicast.

Quando NetX Duo deve partecipare o lasciare un gruppo multicast, ad esempio l'indirizzo multicast a tutti i nodi e l'indirizzo multicast del *nodo richiesto* , emette un comando driver per il driver di dispositivo per partecipare o lasciare un indirizzo MAC multicast. Il comando del driver per l'aggiunta dell'indirizzo multicast è ***NX_LINK_MULTICAST_JOIN** _. Per lasciare un indirizzo multicast, NetX Duo emette il comando driver _ *_NX_LINK_MULTICAST_LEAVE_* *. Per il corretto funzionamento dei protocolli ICMPv6, il driver di dispositivo deve implementare i due comandi seguenti.

Le applicazioni possono partecipare a un gruppo multicast IPv6 utilizzando il servizio ***nxd_ipv6_multicast_interface_join *.** Questo servizio registra l'indirizzo multicast con lo stack IP, quindi notifica al driver di dispositivo specificato l'indirizzo multicast IPv6. Per lasciare un gruppo multicast, le applicazioni usano il servizio ***nxd_ipv6_multicast_interface_leave.***

### <a name="neighbor-discovery-nd"></a>Individuazione router adiacenti (ND)    
Individuazione router adiacenti è un protocollo nelle reti IPv6 per il mapping degli indirizzi fisici agli indirizzi IPv6 (indirizzo globale o indirizzo locale del collegamento). Questo mapping viene mantenuto nella cache di individuazione Neighbor (cache ND). Il processo ND è l'equivalente del processo ARP in IPv4 e la cache ND è simile alla tabella ARP. Un nodo IPv6 può ottenere l'indirizzo MAC adiacente usando il protocollo di individuazione Neighbor (ND). Invia un messaggio di richiesta (NS) adiacente all'indirizzo multicast del nodo con richiesta all-node e attende un messaggio di annuncio adiacente corrispondente (NA). L'indirizzo MAC ottenuto tramite questo processo viene archiviato nella cache ND.

Ogni istanza IP ha una cache ND. La cache ND viene mantenuta come una matrice di voci. La dimensione della matrice viene definita in fase di compilazione impostando l'opzione ***NX_IPV6_NEIGHBOR_CACHE_SIZE** _ che in _ *_nx_user. h_* *. Si noti che tutte le interfacce collegate a un'istanza IP condividono la stessa cache ND.

All'avvio di NetX Duo, l'intera cache ND è vuota. Durante l'esecuzione del sistema, NetX Duo aggiorna automaticamente la cache ND, aggiungendo ed eliminando le voci in base al protocollo ND. Tuttavia, un'applicazione può aggiornare anche la cache ND aggiungendo ed eliminando manualmente le voci della cache usando i servizi NetX Duo seguenti:

- ***nxd_nd_cache_entry_delete***  
- ***nxd_nd_cache_entry_set***   
- ***nxd_nd_cache_invalidate***

Quando si inviano e ricevono pacchetti IPv6, NetX Duo aggiorna automaticamente la tabella della cache ND.

## <a name="internet-control-message-protocol-in-ipv6-icmpv6"></a>Internet Control Message Protocol in IPv6 (ICMPv6)  

Il ruolo di ICMPv6 in IPv6 è stato notevolmente esteso per supportare il mapping degli indirizzi IPv6 e l'individuazione dei router. Inoltre, NetX Duo ICMPv6 supporta la richiesta e la risposta echo, le segnalazioni errori ICMPv6 e i messaggi di reindirizzamento ICMPv6.

### <a name="icmpv6-enable"></a>Abilita ICMPv6    
Prima che i messaggi ICMPv6 possano essere elaborati da NetX Duo, l'applicazione deve chiamare il servizio ***nxd_icmp_enable*** per abilitare l'elaborazione ICMPv6 come descritto in precedenza. 

### <a name="icmpv6-messages"></a>Messaggi ICMPv6     
La struttura dell'intestazione ICMPv6 è simile alla struttura dell'intestazione ICMPv4. Come illustrato di seguito, l'intestazione ICMPv6 di base contiene i tre campi, tipo, codice e checksum, oltre alla lunghezza variabile dei dati delle opzioni ICMPv6. 

![Diagramma di un'intestazione ICMPv6 di base.](./media/user-guide/image19.png)

**FIGURA 10. Intestazione ICMPv6 di base**

|Campo |Dimensioni (byte) |Descrizione |
|-----|-----|-----|
|     | 1   |Identifica il tipo di messaggio ICMPv6; |
|     |     |1 destinazione non raggiungibile |
|     |     |2 pacchetti troppo grandi |
|     |     |3 volte superato |
|     |     |4 problema di parametro |
|     |     |128 richiesta echo |
|     |     |129 risposta echo |
|     |     |133 richiesta router |
|     |     |Annuncio router 134 |
|     |     |135 richiesta Neighbor |
|     |     |136 annuncio adiacente |
|     |     |Messaggio di reindirizzamento 137 |
|Codice | 1   |Qualifica ulteriormente il tipo di messaggio ICMPv6. Utilizzato generalmente con i messaggi di errore. Se non viene usato, viene impostato su zero. I messaggi di richiesta/risposta echo e NS non lo usano.|
|Checksum | 2 |campo checksum a 16 bit per l'intestazione ICMP. Si tratta di un complemento a 16 bit dell'intero messaggio ICMPv6, inclusa l'intestazione ICMPv6. Include anche una pseudo-intestazione dell'indirizzo di origine IPv6, l'indirizzo di destinazione e la lunghezza del payload del pacchetto. |

Di seguito è riportato un esempio di intestazione di richiesta Neighbor.

![Diagramma di un'intestazione di richiesta Neighbor di esempio.](./media/user-guide/image20.jpg)

**FIGURA 11. Intestazione ICMPv6 per un messaggio di richiesta router adiacente**

|Campo |Dimensioni (byte) |Descrizione |
|-----|-----|-----|
|Type | 1   |Identifica il tipo di messaggio ICMPv6 per i messaggi di richiesta adiacenti. Il valore è 135. |
|Codice | 1   |Non usato. Impostare su 0. |
|Checksum | 2  |campo checksum a 16 bit per l'intestazione ICMPv6. |
|Riservato | 4  |4 byte riservati impostati su 0. |
|Indirizzo di destinazione | 16  |Indirizzo IPv6 della destinazione della richiesta. Per la risoluzione degli indirizzi IPv6, questo è l'indirizzo IP unicast effettivo del dispositivo il cui indirizzo del livello di collegamento deve essere risolto. |
|Opzioni | Variabile |Informazioni facoltative specificate dal protocollo di individuazione Neighbor. |

### <a name="icmpv6-ping-request"></a>Richiesta ping ICMPv6
Nelle applicazioni NetX Duo utilizzare ***nxd_icmp_ping*** per emettere richieste ping IPv6 o IPv4, in base all'indirizzo IP di destinazione specificato nei parametri.  

### <a name="icmpv6-ping-response"></a>Risposta ping ICMPv6
Una risposta del ping ICMPv6 è un altro tipo di messaggio ICMPv6 generato internamente dal componente ICMPv6 in risposta a una richiesta di ping ICMPv6 esterna. In aggiunta al riconoscimento, la risposta al ping ICMPv6 contiene anche una copia dei dati utente specificati nella richiesta ping ICMPv6.  

### <a name="thread-suspension"></a>Sospensione thread
I thread dell'applicazione possono sospendere durante il tentativo di effettuare il ping di un altro membro di rete. Dopo la ricezione di una risposta ping, il messaggio di risposta ping viene assegnato al primo thread sospeso e il thread viene ripreso. Come tutti i servizi NetX Duo, la sospensione su una richiesta ping presenta un timeout facoltativo.  

### <a name="other-icmpv6-messages"></a>Altri messaggi ICMPv6
I messaggi ICMPv6 sono necessari per le seguenti funzionalità:  

- Individuazione router adiacenti  
- Configurazione automatica degli indirizzi senza stato 
- Individuazione router 
- Rilevamento non raggiungibilità adiacente  

### <a name="neighbor-unreachability-router-and-prefix-discovery"></a>Individuazione router e prefisso Neighbor    
Il rilevamento di non raggiungibilità adiacente, l'individuazione dei router e l'individuazione del prefisso sono basati sul protocollo di individuazione adiacente e sono descritti di seguito. 

***Rilevamento non raggiungibilità neighbor:*** Un dispositivo IPv6 cerca nell'indirizzo del livello di collegamento di destinazione la cache di individuazione vicina (ND) per l'invio di un pacchetto. La destinazione immediata, a volte definita "hop successivo", può essere la destinazione effettiva sullo stesso collegamento o un router se la destinazione è off. Una voce della cache ND contiene lo stato della raggiungibilità di un router adiacente.

Uno stato raggiungibile indica che il router adiacente è considerato raggiungibile. Un router adiacente è raggiungibile se ha ricevuto recentemente la conferma della ricezione dei pacchetti inviati al router adiacente. La conferma in NetX duo ha la forma di ricevere un messaggio NA dal router adiacente in risposta a un messaggio NS inviato dal dispositivo NetX Duo. NetX Duo cambierà anche lo stato dello stato Neighbor in REACHable se l'applicazione chiama il servizio NetX Duo ***nxd_nd_cache_entry_set*** per immettere manualmente un record della cache.

***Individuazione router:*** Un dispositivo IPv6 usa un router per inoltrare tutti i pacchetti destinati a destinazioni di collegamento off. Può inoltre utilizzare le informazioni inviate dal router, ad esempio i messaggi di annuncio router (RA), per configurare gli indirizzi IPv6 globali.

Un dispositivo nella rete può avviare il processo di individuazione del router inviando un messaggio di richiesta router (RS) all'indirizzo multicast All-router (FF01:: 2). In alternativa, è possibile attendere l'indirizzo multicast a tutti i nodi (FF:: 1) per un RA periodico dai router.

Un messaggio RA contiene le informazioni sul prefisso per la configurazione di un indirizzo IPv6 per la rete. In NetX Duo, la richiesta del router è abilitata per impostazione predefinita e può essere disabilitata impostando l'opzione di configurazione ***NX_DISABLE_ICMPV6_ROUTER_SOLICITATION** _ in _ *_nx_user. h_* *. Vedere le opzioni di configurazione nel capitolo "installazione e uso di NetX Duo" per altre informazioni sull'impostazione dei parametri di richiesta router. 

***Individuazione prefisso***: un dispositivo IPv6 usa l'individuazione del prefisso per scoprire quali host di destinazione sono accessibili direttamente senza passare attraverso un router. Queste informazioni vengono rese disponibili per il dispositivo IPv6 da messaggi RA dal router. Il dispositivo IPv6 archivia le informazioni sul prefisso in una tabella dei prefissi. L'individuazione dei prefissi corrisponde a un prefisso della tabella dei prefissi di dispositivo IPv6 a un indirizzo di destinazione. Un prefisso corrisponde a un indirizzo di destinazione se tutti i bit nel prefisso corrispondono ai bit più significativi dell'indirizzo di destinazione. Se più di un prefisso copre un indirizzo, viene selezionato il prefisso più lungo.

### <a name="icmpv6-error-messages"></a>Messaggi di errore ICMPv6    
In NetX Duo sono supportati i messaggi di errore ICMPv6 seguenti:  

- Destinazione non raggiungibile  
- Pacchetto troppo grande  
- Tempo massimo  
- Problema di parametro  

## <a name="user-datagram-protocol-udp"></a>UDP (User Datagram Protocol)

Il protocollo UDP (User Datagram Protocol) fornisce la forma più semplice di trasferimento dei dati tra i membri di rete (RFC 768). I pacchetti di dati UDP vengono inviati da un membro di rete a un altro nel modo migliore possibile. ovvero, non esiste alcun meccanismo incorporato per il riconoscimento da parte del destinatario del pacchetto. Inoltre, per l'invio di un pacchetto UDP non è necessario stabilire alcuna connessione in anticipo. Per questo motivo, la trasmissione dei pacchetti UDP è molto efficiente.

Per gli sviluppatori che eseguono la migrazione delle applicazioni NetX a NetX Duo sono disponibili solo alcune modifiche di base della funzionalità UDP tra NetX e NetX Duo. Questo è dovuto al fatto che IPv6 riguarda principalmente il livello IP sottostante. Tutti i servizi UDP NetX Duo possono essere utilizzati per la connettività IPv4 o IPv6.

### <a name="udp-header"></a>Intestazione UDP       
UDP posiziona una semplice intestazione del pacchetto davanti ai dati dell'applicazione durante la trasmissione e rimuove un'intestazione UDP simile dal pacchetto alla ricezione prima di consegnare un pacchetto UDP ricevuto all'applicazione. UDP usa il protocollo IP per l'invio e la ricezione di pacchetti, ovvero è presente un'intestazione IP davanti all'intestazione UDP quando il pacchetto si trova nella rete. Nella figura 12 viene illustrato il formato dell'intestazione UDP.

![Diagramma del formato di intestazione UDP.](./media/user-guide/image21.png)

### <a name="figure-12-udp-header"></a>FIGURA 12. Intestazione UDP

> [!NOTE]
> *È previsto che tutte le intestazioni nell'implementazione di UDP/IP siano in formato **Big Endian** . In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso.*

Di seguito viene descritto il formato dell'intestazione UDP:

|Campo di intestazione |Scopo |
|---|---|
|**numero di porta di origine a 16 bit** |Questo campo contiene la porta da cui viene inviato il pacchetto UDP. Le porte UDP valide sono comprese tra 1 e 0xFFFF. |
|**numero porta di destinazione a 16 bit** |Questo campo contiene la porta UDP a cui viene inviato il pacchetto. Le porte UDP valide sono comprese tra 1 e 0xFFFF. |
|**lunghezza UDP a 16 bit** |Questo campo contiene il numero di byte nel pacchetto UDP, incluse le dimensioni dell'intestazione UDP. |
|**checksum UDP a 16 bit** |Questo campo contiene il checksum a 16 bit per il pacchetto, tra cui l'intestazione UDP, l'area dati del pacchetto e l'intestazione pseudo-IP. |

### <a name="udp-enable"></a>Abilita UDP   
Prima che sia possibile la trasmissione di pacchetti UDP, l'applicazione deve prima abilitare UDP chiamando il servizio ***nx_udp_enable*** . Dopo l'abilitazione, l'applicazione è gratuita per inviare e ricevere pacchetti UDP.  

### <a name="udp-socket-create"></a>Creazione socket UDP    
I socket UDP vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Il tipo di servizio, la durata (TTL) e la profondità della coda di ricezione specificati sono definiti dal servizio ***nx_udp_socket_create*** . Non sono previsti limiti per il numero di socket UDP in un'applicazione.

### <a name="udp-checksum"></a>Checksum UDP   
Il protocollo IPv6 richiede un calcolo del checksum dell'intestazione UDP sui dati dei pacchetti, mentre nel protocollo IPv4 è facoltativo.  

UDP specifica un checksum a 16 bit a complemento di uno che copre la pseudo intestazione IP (costituita dall'indirizzo IP di origine, indirizzo IP di destinazione e la parola IP di protocollo/lunghezza), l'intestazione UDP e i dati del pacchetto UDP. Le uniche differenze tra i checksum dei pacchetti UDP IPv4 e IPv6 sono rappresentati dal fatto che gli indirizzi IP di origine e di destinazione sono 32 bit in IPv4 mentre in IPv6 sono di 128 bit. Se il checksum UDP calcolato è 0, viene archiviato come tutti i valori (0xFFFF). Se per il socket di invio è disabilitata la logica di checksum UDP, nel campo checksum UDP viene inserito uno zero per indicare che il checksum non è stato calcolato.

Se il checksum UDP non corrisponde al checksum calcolato dal ricevitore, il pacchetto UDP viene semplicemente ignorato.

Nella rete IPv4 il checksum UDP è facoltativo. NetX Duo consente a un'applicazione di abilitare o disabilitare il calcolo del checksum UDP in base al socket. Per impostazione predefinita, la logica di checksum del socket UDP è abilitata. L'applicazione può disabilitare la logica di checksum per un particolare socket UDP chiamando il servizio ***nx_udp_socket_checksum_disable** _. Nella rete IPv6, tuttavia, il checksum UDP è obbligatorio. Pertanto, il servizio _ *_nx_udp_socket_checksum_disable_** non disabilita la logica di checksum UDP durante l'invio di un pacchetto tramite la rete IPv6.

Alcuni controller Ethernet sono in grado di generare rapidamente il checksum UDP. Se il sistema è in grado di utilizzare la funzionalità di calcolo di checksum hardware, la libreria NetX Duo può essere compilata senza la logica di checksum. Per disabilitare il checksum del software UDP, è necessario compilare la libreria NetX Duo con i simboli seguenti definiti: ***NX_DISABLE_UDP_TX_CHECKSUM** _ e _*_NX_DISABLE_UDP_RX_CHECKSUM_*_ (descritto nel capitolo due). Le opzioni di configurazione eliminano completamente la logica di checksum UDP da NetX Duo, mentre la chiamata al servizio _ *_nx_udp_socket_checksum_disable_** consente all'applicazione di disabilitare l'elaborazione del checksum UDP IPv4 per ogni socket.

### <a name="udp-ports-and-binding"></a>Porte e binding UDP      
Una porta UDP è un endpoint logico nel protocollo UDP. Nel componente UDP di NetX Duo sono presenti 65.535 porte valide, comprese tra 1 e 0xFFFF. Per inviare o ricevere dati UDP, l'applicazione deve prima creare un socket UDP, quindi associarlo a una porta desiderata. Dopo aver associato un socket UDP a una porta, l'applicazione può inviare e ricevere dati su tale socket.

### <a name="udp-fast-pathtrade"></a>Percorso veloce UDP&trade;   
Il percorso veloce UDP &trade; è il nome di un percorso di overhead dei pacchetti basso tramite l'implementazione UDP di NETX Duo. L'invio di un pacchetto UDP richiede solo alcune chiamate di funzione: ***nx_udp_socket_send** _, _*_nx_ip_packet_send_*_ e la chiamata finale al driver di rete. _*_nx_udp_socket_send_*_ è disponibile in NETX Duo per le applicazioni NETX esistenti ed è applicabile solo ai pacchetti IPv4. Il metodo preferito, tuttavia, consiste nell'usare _ *_nxd_udp_socket_send_** servizio descritto di seguito. Nella ricezione di pacchetti UDP, il pacchetto UDP viene inserito nella coda di ricezione socket UDP appropriata o recapitato a un thread dell'applicazione sospesa in una singola chiamata di funzione dall'elaborazione dell'interrupt di ricezione del driver di rete. Questa logica altamente ottimizzata per l'invio e la ricezione di pacchetti UDP è l'essenza della tecnologia di percorso veloce UDP.  

### <a name="udp-packet-send"></a>Invio pacchetti UDP    
L'invio di dati UDP su reti IPv6 o IPv4 viene eseguito facilmente chiamando la funzione ***nxd_udp_socket_send** _. Il chiamante deve impostare la versione IP nel campo _nx_ip_version * del parametro del puntatore NXD_ADDRESS. NetX Duo determinerà l'indirizzo di origine migliore per i pacchetti UDP trasmessi in base all'indirizzo IPv4/IPv6 di destinazione. Questo servizio posiziona un'intestazione UDP davanti ai dati del pacchetto e la invia alla rete usando una routine di invio IP interna. Non vi è alcuna sospensione di thread per l'invio di pacchetti UDP perché tutte le trasmissioni di pacchetti UDP vengono elaborate immediatamente. 

Per le destinazioni multicast o broadcast, l'applicazione deve specificare l'indirizzo IP di origine da usare se il dispositivo NetX duo ha più indirizzi IP tra cui scegliere. Questa operazione può essere eseguita con i servizi ***nxd_udp_socket_source_send.***

> [!IMPORTANT]    
> *Se **nx_udp_socket_send** viene usato per la trasmissione di pacchetti broadcast o multicast, l'indirizzo IP della prima interfaccia abilitata viene usato come indirizzo di origine*.

> [!NOTE] 
> *Se per questo socket è abilitata la logica di checksum UDP, l'operazione di checksum viene eseguita nel contesto del thread chiamante, senza bloccare l'accesso alle strutture di dati UDP o IP*. 

> [!WARNING]    
> *I dati di payload UDP che risiedono nella struttura di NX_PACKET devono trovarsi su un confine di parola lungo. L'applicazione deve lasciare spazio sufficiente tra il puntatore Prepend e il puntatore di avvio dati per NetX Duo per inserire le intestazioni UDP, IP e supporti fisici*.

### <a name="udp-packet-receive"></a>Ricezione pacchetti UDP    
I thread dell'applicazione possono ricevere pacchetti UDP da un socket particolare chiamando ***nx_udp_socket_receive***. La funzione di ricezione socket recapita il pacchetto meno recente nella coda di ricezione del socket. Se non sono presenti pacchetti nella coda di ricezione, il thread chiamante può sospendere (con un timeout facoltativo) finché non arriva un pacchetto.

L'elaborazione dei pacchetti di ricezione UDP (in genere chiamata dal gestore di interrupt di ricezione del driver di rete) è responsabile del posizionamento del pacchetto nella coda di ricezione del socket UDP o del recapito al primo thread sospeso in attesa di un pacchetto. Se il pacchetto viene accodato, l'elaborazione della ricezione controlla anche la profondità massima della coda di ricezione associata al socket. Se il pacchetto appena accodato supera la profondità della coda, il pacchetto meno recente nella coda viene eliminato.

### <a name="udp-receive-notify"></a>Ricezione notifica UDP   
Se il thread dell'applicazione deve elaborare i dati ricevuti da più di un socket, è necessario usare la funzione ***nx_udp_socket_receive_notify*** . Questa funzione registra una funzione di callback del pacchetto di ricezione per il socket. Ogni volta che viene ricevuto un pacchetto nel socket, viene eseguita la funzione di callback.

Il contenuto della funzione di callback è applicationspecific; Tuttavia, sarebbe più probabile che contengano la logica per informare il thread di elaborazione che un pacchetto è ora disponibile nel socket corrispondente.

### <a name="peer-address-and-port"></a>Indirizzo e porta peer   
Alla ricezione di un pacchetto UDP, l'applicazione può trovare l'indirizzo IP e il numero di porta del mittente usando il ***nx_udp_packet_info_extract*** del servizio. In seguito all'esito positivo, questo servizio fornisce informazioni sull'indirizzo IP del mittente, sul numero di porta del mittente e sull'interfaccia locale tramite cui è stato ricevuto il pacchetto.  

### <a name="thread-suspension"></a>Sospensione thread   
Come indicato in precedenza, i thread dell'applicazione possono sospendere il tentativo di ricezione di un pacchetto UDP su una determinata porta UDP. Dopo la ricezione di un pacchetto su tale porta, questo viene assegnato al primo thread sospeso e il thread viene quindi ripreso. Un timeout facoltativo è disponibile quando si sospende un pacchetto di ricezione UDP, una funzionalità disponibile per la maggior parte dei servizi NetX Duo.  

### <a name="udp-socket-statistics-and-errors"></a>Statistiche ed errori di socket UDP     
Se abilitata, il software socket UDP NetX Duo tiene traccia di diverse statistiche ed errori che possono risultare utili per l'applicazione. Per ogni istanza IP/UDP vengono mantenute le statistiche e i report degli errori seguenti:

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

Tutte le statistiche e i report degli errori sono disponibili per l'applicazione con il servizio ***nx_udp_info_get** _ per le statistiche UDP raccolte su tutti i socket UDP e il servizio _ *_nx_udp_socket_info_get_** per le statistiche UDP sul socket UDP specificato.

### <a name="udp-socket-control-block-nx_udp_socket"></a>NX_UDP_SOCKET blocco di controllo socket UDP
Le caratteristiche di ogni socket UDP si trovano nel blocco di controllo NX_UDP_SOCKET associato. Contiene informazioni utili, ad esempio il collegamento alla struttura dei dati IP, l'interfaccia di rete per i percorsi di invio e ricezione, la porta associata e la coda dei pacchetti di ricezione. Questa struttura viene definita nel file ***nx_api. h*** .

## <a name="transmission-control-protocol-tcp"></a>Transmission Control Protocol (TCP)

Il Transmission Control Protocol (TCP) fornisce un trasferimento dei dati di flusso affidabile tra due membri di rete (RFC 793). Tutti i dati inviati da un membro della rete vengono verificati e riconosciuti dal membro di destinazione. Inoltre, i due membri devono avere stabilito una connessione prima del trasferimento dei dati. Il risultato è il trasferimento affidabile dei dati; Tuttavia, richiede un sovraccarico sostanziale rispetto al trasferimento dei dati UDP descritto in precedenza.

Ad eccezione di quanto indicato, non sono presenti modifiche nei servizi API del protocollo TCP tra NetX e NetX Duo, perché IPv6 riguarda principalmente il livello IP sottostante. Tutti i servizi TCP NetX Duo possono essere utilizzati per le connessioni IPv4 o IPv6.

### <a name="tcp-header"></a>Intestazione TCP   
Sulla trasmissione, l'intestazione TCP viene posizionata davanti ai dati dell'utente. Alla ricezione, l'intestazione TCP viene rimossa dal pacchetto in ingresso, lasciando solo i dati utente disponibili per l'applicazione. TCP utilizza il protocollo IP per inviare e ricevere pacchetti, ovvero è presente un'intestazione IP davanti all'intestazione TCP quando il pacchetto si trova nella rete. Nella figura 13 viene illustrato il formato dell'intestazione TCP.

![Diagramma del formato dell'intestazione TCP.](./media/user-guide/image22.png)

### <a name="figure-13-tcp-header"></a>FIGURA 13. Intestazione TCP

Di seguito viene descritto il formato dell'intestazione TCP:

|Campo di intestazione &nbsp; |Scopo |
|------|------|
| **numero di porta di origine a 16 bit** | Questo campo contiene la porta a cui viene inviato il pacchetto TCP. Le porte TCP valide sono comprese tra 1 e 0xFFFF. |
| **porta di destinazione a 16 bit** | Questo campo contiene la porta TCP a cui viene inviato il pacchetto. Le porte TCP valide sono comprese tra 1 e 0xFFFF. |
| **numero di sequenza a 32 bit** | Questo campo contiene il numero di sequenza per i dati inviati da questa entità finale della connessione. La sequenza originale viene stabilita durante la sequenza di connessione iniziale tra due nodi TCP. Ogni trasferimento di dati da tale punto genera un incremento del numero di sequenza in base alla quantità di byte inviati. |
| **numero di riconoscimento a 32 bit** | Questo campo contiene il numero di sequenza corrispondente all'ultimo byte ricevuto da questo lato della connessione. Viene utilizzato per determinare se i dati inviati in precedenza sono stati ricevuti correttamente dall'altra entità finale della connessione. |
| **lunghezza intestazione a 4 bit** | Questo campo contiene il numero di parole a 32 bit nell'intestazione TCP. Se nell'intestazione TCP non è presente alcuna opzione, il campo è 5. |
| **bit di codice a 6 bit** |Questo campo contiene i sei bit di codice diversi usati per indicare le varie informazioni di controllo associate alla connessione. I bit di controllo sono definiti nel modo seguente: <BR \> -Urg (21): data presen<BR \> -ACK (20): il numero di riconoscimento è valido<BR \> -PSH (19): gestire immediatamente questi dati<BR \> -RST (18): reimpostare la connessione<BR \> -SYN (17): sincronizzare i numeri di sequenza (usati per stabilire la connessione) <BR \> -pinna (16): il mittente è terminato con la trasmissione (usato per chiudere la |
|**finestra a 16 bit** |Questo campo viene usato per il controllo di flusso. Contiene la quantità di byte che il socket può attualmente ricevere. Questo viene essenzialmente usato per il controllo di flusso. Il mittente è responsabile di assicurarsi che i dati da inviare vengano inseriti nella finestra annunciata del destinatario. |
|**checksum TCP a 16 bit** |Questo campo contiene il checksum a 16 bit per il pacchetto, tra cui l'intestazione TCP, l'area dati del pacchetto e l'intestazione pseudo-IP. |
|**Puntatore urgente a 16 bit** |Questo campo contiene l'offset positivo dell'ultimo byte dei dati urgenti. Questo campo è valido solo se il bit di codice URG è impostato nell'intestazione. |

> [!NOTE]  
> *È previsto che tutte le intestazioni nell'implementazione TCP/IP siano in formato **Big Endian** . In questo formato, il byte più significativo della parola risiede nell'indirizzo di byte più basso*.

### <a name="tcp-enable"></a>Abilitazione TCP       
Prima che le connessioni TCP e le trasmissioni di pacchetti siano possibili, l'applicazione deve prima abilitare TCP chiamando il servizio ***nx_tcp_enable*** . Dopo l'abilitazione, l'applicazione è gratuita per accedere a tutti i servizi TCP.  

### <a name="tcp-socket-create"></a>Creazione socket TCP    
I socket TCP vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Il tipo di servizio, la durata (TTL) e le dimensioni della finestra sono definiti dal servizio ***nx_tcp_socket_create*** . Non sono previsti limiti per il numero di socket TCP in un'applicazione.  

### <a name="tcp-checksum"></a>Checksum TCP     
TCP specifica un checksum a 16 bit a complemento di uno che copre la pseudo intestazione IP, costituita dall'indirizzo IP di origine, dall'indirizzo IP di destinazione e dalla parola IP di protocollo/lunghezza, l'intestazione TCP e i dati del pacchetto TCP. L'unica differenza tra i checksum dell'intestazione dei pacchetti TCP IPv4 e IPv6 è che gli indirizzi IP di origine e di destinazione sono 32 bit in IPv4 e 128 bit in IPv6. 

Alcuni controller di rete sono in grado di eseguire il calcolo e la convalida del checksum TCP nell'hardware. Per tali sistemi, le applicazioni potrebbero voler usare la logica di checksum hardware il più possibile per ridurre il sovraccarico di Runtime. Le applicazioni possono disabilitare la logica di calcolo del checksum TCP dalla libreria NetX Duo in fase di compilazione definendo ***NX_DISABLE_TCP_TX_CHECKSUM** _ e _ *_NX_DISABLE_TCP_RX_CHECKSUM_* *. In questo modo, il codice di checksum TCP non viene compilato in. Tuttavia, è necessario prestare attenzione se il pacchetto NetX Duo IPsec facoltativo è installato e la connessione TCP potrebbe dover attraversare un canale sicuro. In questo caso, i dati nei pacchetti appartenenti alla connessione TCP sono già crittografati e la maggior parte dei moduli di checksum TCP hardware presenti nel driver di rete non è in grado di generare un valore di checksum corretto dal payload TCP crittografato.

Per risolvere questo problema, l'applicazione mantiene la logica di checksum TCP disponibile nella libreria e utilizza la funzionalità di interfaccia. Con la funzionalità di funzionalità dell'interfaccia abilitata, il modulo TCP sa come gestire correttamente il checksum TCP se il driver è anche in grado di calcolare il valore di checksum:

1) Se il pacchetto TCP non è soggetto a un processo IPsec, l'hardware dell'interfaccia di rete è in grado di calcolare il checksum. Il modulo TCP non tenta pertanto di calcolare il checksum.

2) Se il pacchetto IPsec è installato e il pacchetto TCP è soggetto a un processo IPsec, il modulo TCP calcola il checksum nel software prima di inviare il pacchetto al livello IPsec.

### <a name="tcp-port"></a>Porta TCP     
Una porta TCP è un punto di connessione logico nel protocollo TCP. Nel componente TCP di NetX Duo sono presenti 65.535 porte valide, comprese tra 1 e 0xFFFF. Diversamente da UDP, in cui i dati di una porta possono essere inviati a qualsiasi altra porta di destinazione, una porta TCP è connessa a un'altra porta TCP specifica e solo quando viene stabilita la connessione può essere effettuato il trasferimento dei dati, e solo tra le due porte che costituiscono la connessione.

> [!IMPORTANT]
> Le *porte TCP sono completamente separate dalle porte UDP. ad esempio, la porta UDP numero 1 non ha alcuna relazione con la porta TCP numero 1*.

### <a name="client-server-model"></a>Modello di Client-Server     
Per usare TCP per il trasferimento dei dati, è prima necessario stabilire una connessione tra i due socket TCP. La creazione della connessione viene eseguita in modalità client-server. Il lato client della connessione è il lato che avvia la connessione, mentre il lato server è semplicemente in attesa delle richieste di connessione client prima che venga eseguita qualsiasi elaborazione.

> [!IMPORTANT]
> *Per i dispositivi multihome, NETX Duo determina automaticamente l'indirizzo di origine da usare per la connessione e l'indirizzo hop successivo in base all'indirizzo IP di destinazione della connessione. Poiché il protocollo TCP è limitato all'invio di pacchetti a indirizzi di destinazione unicast (ad esempio, non broadcast), NetX Duo non richiede un "hint" per la scelta dell'indirizzo IPv6 di origine*.

### <a name="tcp-socket-state-machine"></a>Macchina a stati socket TCP      
La connessione tra due socket TCP (un client e un server) è complessa e viene gestita in modo analogo a una macchina a Stati. Ogni socket TCP viene avviato in uno stato chiuso. Tramite gli eventi di connessione viene eseguita la migrazione della macchina a stati di ogni socket nello stato stabilito, ovvero la posizione in cui viene eseguita la maggior parte del trasferimento dei dati in TCP. Quando un lato della connessione non desidera più inviare dati, si disconnette. Dopo la disconnessione dell'altro lato, il socket TCP torna allo stato CLOSED. Questo processo viene ripetuto ogni volta che un client e un server TCP stabiliscono e chiudono una connessione. La figura 14 Mostra i vari Stati della macchina a stati TCP.

### <a name="tcp-client-connection"></a>Connessione client TCP       
Come indicato in precedenza, il lato client della connessione TCP avvia una richiesta di connessione a un server TCP. Prima di poter effettuare una richiesta di connessione, è necessario abilitare il protocollo TCP nell'istanza IP del client. Inoltre, il socket TCP del client deve essere creato successivamente con il servizio ***nx_tcp_socket_create** _ e associato a una porta tramite il servizio _ *_nx_tcp_client_socket_bind_**.

Quando il socket client viene associato, il servizio ***nxd_tcp_client_socket_connect*** viene usato per stabilire una connessione con un server TCP. Si noti che il socket deve trovarsi in uno stato chiuso per avviare un tentativo di connessione. Stabilire la connessione inizia con NetX duo che emette un pacchetto SYN e quindi attende un pacchetto SYN ACK dal server, che indica l'accettazione della richiesta di connessione. Dopo la ricezione dell'ACK SYN, NetX Duo risponde con un pacchetto ACK e promuove lo stato stabilito del socket client.

![Diagramma degli Stati della macchina a stati TCP.](./media/user-guide/image24.png)   

**FIGURA 14. Stati della macchina a stati TCP**


> [!WARNING]
> *Le applicazioni devono utilizzare **Nxd_tcp_client_socket_connect** per le connessioni TCP IPv4 e IPv6. Le applicazioni possono comunque usare **nx_tcp_client_socket_connect** per le connessioni TCP IPv4, ma gli sviluppatori sono invitati a usare **nxd_tcp_client_socket_connect** perché **nx_tcp_client_socket_connect** alla fine saranno deprecate*.

*Analogamente, **nxd_tcp_socket_peer_info_get** funziona con connessioni TCP IPv4 o IPv6. Tuttavia, **nx_tcp_socket_peer_info_get** è ancora disponibile per le applicazioni legacy. Gli sviluppatori sono invitati a usare **nxd_tcp_socket_peer_info_get** in futuro*.

### <a name="tcp-client-disconnection"></a>Disconnessione del client TCP    
La chiusura della connessione viene eseguita chiamando ***nx_tcp_socket_disconnect***. Se non viene specificata alcuna sospensione, il socket client invia un pacchetto RST al socket del server e posiziona il socket nello stato CLOSED. In caso contrario, se viene richiesta una sospensione, viene eseguito il protocollo di disconnessione TCP completo, come indicato di seguito: 

- Se il server ha avviato in precedenza una richiesta di disconnessione (il socket client ha già ricevuto un pacchetto FIN, ha risposto con un ACK ed è nello stato di attesa di chiusura), NetX duo promuove lo stato del socket TCP del client allo stato dell'ultimo ACK e invia un pacchetto FIN. Attende quindi un ACK dal server prima di completare la disconnessione e di entrare nello stato CLOSED.

- Se invece il client è il primo ad avviare una richiesta di disconnessione (il server non si è disconnesso e il socket si trova ancora nello stato stabilito), NetX Duo Invia un pacchetto FIN per avviare la disconnessione e attende la ricezione di una pinna e di un ACK dal server prima di completare la disconnessione e di collocare il socket in uno stato chiuso.

Se nella coda di trasmissione socket sono ancora presenti pacchetti, NetX Duo sospende il timeout specificato per consentire la conferma dei pacchetti. Se il timeout scade, NetX Duo svuota la coda di trasmissione del socket client. 

Per disassociare la porta dal socket client, l'applicazione chiama ***nx_tcp_client_socket_unbind***. Il socket deve trovarsi in uno stato chiuso o nel processo di disconnessione (ad esempio, lo stato di attesa programmato) prima che la porta venga rilasciata; in caso contrario, viene restituito un errore.

Infine, se l'applicazione non necessita più del socket client, chiama ***nx_tcp_socket_delete*** per eliminare il socket.

### <a name="tcp-server-connection"></a>Connessione al server TCP      
Il lato server di una connessione TCP è passivo; ovvero, il server attende che un client avvii una richiesta di connessione. Per accettare una connessione client, è prima necessario abilitare TCP sull'istanza IP chiamando il servizio ***nx_tcp_enable** _. Successivamente, l'applicazione deve creare un socket TCP usando il servizio _ *_nx_tcp_socket_create_**.  

Il socket del server deve essere configurato anche per l'ascolto delle richieste di connessione. Questa operazione viene eseguita tramite il servizio ***nx_tcp_server_socket_listen*** . Questo servizio posiziona il socket del server nello stato di ascolto e associa la porta del server specificata al socket.

> [!NOTE] 
> *Per impostare una routine di callback di ascolto del socket, l'applicazione specifica la funzione di callback appropriata per l'argomento tcp_listen_callback del servizio di **nx_tcp_server_socket_listen** . Questa funzione di callback dell'applicazione viene quindi eseguita da NetX Duo ogni volta che viene richiesta una nuova connessione sulla porta del server. L'elaborazione nel callback è sotto il controllo dell'applicazione.*

Per accettare le richieste di connessione client, l'applicazione chiama il servizio ***nx_tcp_server_socket_accept** _. Il socket del server deve essere in uno stato di attesa o in uno stato SYN ricevuto (ovvero, il server è in stato di ascolto e ha ricevuto un pacchetto SYN da un client che ha richiesto una connessione) per chiamare il servizio Accept. Uno stato restituito correttamente da _ *_nx_tcp_server_socket_accept_** indica che la connessione è stata configurata e che il socket del server si trova nello stato stabilita.

Dopo che il socket del server dispone di una connessione valida, le richieste di connessione client aggiuntive vengono accodate fino alla profondità specificata dal *listen_queue_size, passate* al  * servizio **nx_tcp_server_socket_listen** _. Per elaborare le connessioni successive su una porta del server, l'applicazione deve chiamare _ *_nx_tcp_server_socket_relisten_** con un socket disponibile, ovvero un socket in uno stato chiuso. Si noti che è possibile usare lo stesso socket del server se la connessione precedente associata al socket è terminata e lo stato del socket è CLOSED.

### <a name="tcp-server-disconnection"></a>Disconnessione del server TCP     
La chiusura della connessione viene eseguita chiamando ***nx_tcp_socket_disconnect***. Se non viene specificata alcuna sospensione, il socket del server invia un pacchetto RST al socket client e posiziona il socket nello stato CLOSED. In caso contrario, se viene richiesta una sospensione, viene eseguito il protocollo di disconnessione TCP completo, come indicato di seguito:

- Se il client ha avviato in precedenza una richiesta di disconnessione (il socket del server ha già ricevuto un pacchetto FIN, ha risposto con un ACK ed è nello stato di attesa di chiusura), NetX duo promuove lo stato del socket TCP per l'ultimo stato ACK e invia un pacchetto FIN. Attende quindi un ACK dal client prima di completare la disconnessione e di entrare nello stato CLOSED.

- Se invece il server è il primo ad avviare una richiesta di disconnessione (il client non si è disconnesso e il socket si trova ancora nello stato stabilito), NetX Duo Invia un pacchetto FIN per avviare la disconnessione e attende la ricezione di una pinna e di un ACK dal client prima di completare la disconnessione e di collocare il socket in uno stato chiuso.

Se nella coda di trasmissione socket sono ancora presenti pacchetti, NetX Duo sospende il timeout specificato per consentire la conferma di tali pacchetti. Se il timeout scade, NetX Duo Scarica la coda di trasmissione del socket del server.

Una volta completata l'elaborazione della disconnessione e il socket del server si trova nello stato CLOSED, l'applicazione deve chiamare il servizio ***nx_tcp_server_socket_unaccept** _ per terminare l'associazione di questo socket con la porta del server. Si noti che questo servizio deve essere chiamato dall'applicazione anche se _*_nx_tcp_socket_disconnect_*_ o _*_nx_tcp_server_socket_accept_*_ restituiscono uno stato di errore. Una volta restituito il _*_nx_tcp_server_socket_unaccept_*_ , il socket può essere utilizzato come un socket client o server o anche eliminato se non è più necessario. Se si desidera accettare un'altra connessione client sulla stessa porta del server, è necessario chiamare il servizio _ *_nx_tcp_server_socket_relisten_** su questo socket.

Nel segmento di codice seguente viene illustrata la sequenza di chiamate utilizzate da un server TCP tipico:

```c
/* Set up a previously created TCP socket to
   listen on port 12 */
nx_tcp_server_socket_listen()

/* Loop to make a (another) connection. */
while(1)
{
    /* Wait for a client socket connection request
       for 100 ticks. */
    nx_tcp_server_socket_accept();

    /* (Send and receive TCP messages with the TCP
       client) */

    /* Disconnect the server socket. */
    nx_tcp_socket_disconnect();

    /* Remove this server socket from listening on
       the port. */
    nx_tcp_server_socket_unaccept(&server_socket);
    /* Set up server socket to relisten on the
       same port for the next client. */
    nx_tcp_server_socket_relisten();
}
```

### <a name="mss-validation"></a>Convalida MSS      
La dimensione massima del segmento (MSS) è la quantità massima di byte che un host TCP può ricevere senza essere frammentato dal livello IP sottostante. Durante la fase di creazione della connessione TCP, entrambe le terminazioni scambiano il proprio valore TCP MSS, in modo che il mittente non invii un segmento di dati TCP maggiore della MSS del destinatario. Il modulo NetX Duo TCP convaliderà facoltativamente il valore MSS annunciato del peer prima di stabilire una connessione. Per impostazione predefinita, NetX Duo non abilita tale controllo. Le applicazioni che desiderano eseguire la convalida MSS definiranno ***NX_ENABLE_TCP_MSS_CHECK** _ quando compilano la libreria NETX Duo e il valore minimo sarà definito in _*_NX_TCP_MSS_MINIMUM_*_. Le connessioni TCP in ingresso con valori MSS inferiori a _ *_NX_TCP_MSS_MINIMUM_** verranno eliminate.

### <a name="stop-listening-on-a-server-port"></a>Interrompi ascolto su una porta del server    
Se l'applicazione non desidera più restare in ascolto delle richieste di connessione client su una porta del server specificata in precedenza da una chiamata al servizio ***nx_tcp_server_socket_listen** _, l'applicazione chiama semplicemente il servizio _ *_nx_tcp_server_socket_unlisten_**. Questo servizio posiziona tutti i socket in attesa di una connessione nello stato CLOSED e rilascia tutti i pacchetti di richieste di connessione client in coda. 

### <a name="tcp-window-size"></a>Dimensioni finestra TCP   
Durante le fasi di installazione e trasferimento dei dati della connessione, ogni porta segnala la quantità di dati che è in grado di gestire, denominata dimensione della finestra. Quando i dati vengono ricevuti ed elaborati, questa dimensione della finestra viene regolata dinamicamente. In TCP un mittente può inviare solo una quantità di dati che si inserisce nella finestra del destinatario. In sostanza, le dimensioni della finestra forniscono il controllo di flusso per il trasferimento dei dati in ogni direzione della connessione.   

### <a name="tcp-packet-send"></a>Invio di pacchetti TCP     
L'invio di dati TCP viene eseguito facilmente chiamando la funzione ***nx_tcp_socket_send*** . Se le dimensioni dei dati trasmessi sono maggiori del valore MSS del socket o della dimensione della finestra di ricezione peer corrente, a seconda del valore più piccolo, la logica interna TCP suddivide i dati che rientrano in min (MSS, finestra di ricezione peer) per la trasmissione. Questo servizio compila quindi un'intestazione TCP davanti al pacchetto (incluso il calcolo del checksum). Se le dimensioni della finestra del ricevitore non sono pari a zero, il chiamante invierà il maggior numero di dati possibile per riempire le dimensioni della finestra del ricevitore. Se la finestra di ricezione diventa zero, il chiamante potrebbe sospendere e attendere che le dimensioni della finestra del destinatario aumentino sufficiente per l'invio del pacchetto. In qualsiasi momento, più thread possono sospendere durante il tentativo di invio di dati tramite lo stesso socket. 

> [!WARNING]  
> *I dati TCP che risiedono nella struttura di NX_PACKET devono trovarsi su un limite di parole lunghe. Inoltre, è necessario disporre di spazio sufficiente tra il puntatore anteposto e il puntatore di avvio dati per inserire le intestazioni TCP, IP e supporti fisici*.

### <a name="tcp-packet-retransmit"></a>Ritrasmissione del pacchetto TCP      
I pacchetti TCP trasmessi in precedenza venivano effettivamente archiviati internamente fino a quando non viene restituito un ACK dall'altro lato della connessione. Se i dati trasmessi non vengono riconosciuti entro il periodo di timeout, il pacchetto archiviato viene inviato nuovamente e viene impostato il periodo di timeout successivo. Quando viene ricevuto un ACK, vengono infine rilasciati tutti i pacchetti analizzati dal numero di riconoscimento nella coda di trasmissione interna.  

> [!WARNING]   
> *L'applicazione non deve riutilizzare il pacchetto o modificare il contenuto del pacchetto dopo che nx_tcp_socket_send () restituisce con NX_SUCCESS. Il pacchetto trasmesso viene infine rilasciato dall'elaborazione interna di NetX Duo dopo che i dati sono stati riconosciuti dall'altra entità finale*.

### <a name="tcp-keepalive"></a>Keepalive TCP     
La funzionalità TCP keepalive consente a un socket di rilevare se il peer si disconnette o meno senza terminazione corretta, ad esempio se il peer si è arrestato in modo anomalo, oppure per impedire a determinate funzionalità di monitoraggio della rete di terminare una connessione per lunghi periodi di inattività. Il protocollo keepalive TCP funziona inviando periodicamente un frame TCP senza dati e il numero di sequenza impostato su uno inferiore al numero di sequenza corrente. Alla ricezione di tale frame TCP keepalive, il destinatario, se ancora attivo, risponde con un ACK per il numero di sequenza corrente. Questa operazione completa la transazione KeepAlive.  

Per impostazione predefinita, la funzionalità KeepAlive non è abilitata. Per usare questa funzionalità, è necessario compilare la libreria NetX Duo con ***NX_ENABLE_TCP_KEEPALIVE** _ defined. Il simbolo _ *_NX_TCP_KEEPALIVE_INITIAL_** specifica il numero di secondi di inattività prima dell'avvio del frame KeepAlive.  

### <a name="tcp-packet-receive"></a>Ricezione di pacchetti TCP   
L'elaborazione dei pacchetti di ricezione TCP (chiamata dal thread helper IP) è responsabile della gestione di varie azioni di connessione e disconnessione, oltre che dell'elaborazione di riconoscimento della trasmissione. Inoltre, l'elaborazione dei pacchetti TCP receive è responsabile dell'inserimento dei pacchetti con i dati di ricezione nella coda di ricezione del socket TCP appropriato o del recapito del pacchetto al primo thread sospeso in attesa di un pacchetto.

### <a name="tcp-receive-notify"></a>Notifica di ricezione TCP     
Se il thread dell'applicazione deve elaborare i dati ricevuti da più di un socket, è necessario usare la funzione ***nx_tcp_socket_receive_notify*** . Questa funzione registra una funzione di callback del pacchetto di ricezione per il socket. Ogni volta che viene ricevuto un pacchetto nel socket, viene eseguita la funzione di callback.  

Il contenuto della funzione di callback è applicationspecific; Tuttavia, la funzione conterrebbe probabilmente la logica per informare il thread di elaborazione che un pacchetto è disponibile nel socket corrispondente. 

### <a name="thread-suspension"></a>Sospensione thread      
Come indicato in precedenza, i thread dell'applicazione possono sospendere il tentativo di ricevere dati da una determinata porta TCP. Dopo la ricezione di un pacchetto su tale porta, questo viene assegnato al primo thread sospeso e il thread viene quindi ripreso. Un timeout facoltativo è disponibile quando si sospende un pacchetto di ricezione TCP, una funzionalità disponibile per la maggior parte dei servizi NetX Duo.  

La sospensione dei thread è disponibile anche per la connessione (client e server), l'associazione client e i servizi di disconnessione.  

### <a name="tcp-socket-statistics-and-errors"></a>Statistiche ed errori del socket TCP     
Se abilitata, il software socket TCP NetX Duo tiene traccia di diverse statistiche ed errori che possono risultare utili per l'applicazione. Per ogni istanza IP/TCP vengono mantenute le statistiche e i report degli errori seguenti:   

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

### <a name="tcp-socket-control-block-nx_tcp_socket"></a>NX_TCP_SOCKET blocco di controllo socket TCP      
Le caratteristiche di ogni socket TCP si trovano nel blocco di controllo *NX_TCP_SOCKET* associato, che contiene informazioni utili, ad esempio il collegamento alla struttura dei dati IP, l'interfaccia di connessione di rete, la porta associata e la coda dei pacchetti di ricezione. Questa struttura viene definita nel file ***nx_api. h*** .