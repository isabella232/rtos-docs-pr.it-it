---
title: Capitolo 3 - Componenti funzionali di Azure RTOS NetX Duo
description: Questo capitolo contiene una descrizione delle prestazioni elevate Azure RTOS stack TCP/IP di NetX Duo dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 32af483db1f97b45bfe3d334b8c79d984dedc8470a37ce1d4164331549b6954c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788963"
---
# <a name="chapter-3---functional-components-of-azure-rtos-netx-duo"></a>Capitolo 3 - Componenti funzionali di Azure RTOS NetX Duo

Questo capitolo contiene una descrizione delle prestazioni elevate Azure RTOS stack TCP/IP di NetX Duo dal punto di vista funzionale. 

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Esistono cinque tipi di esecuzione del programma all'interno di un'applicazione NetX Duo: inizializzazione, chiamate all'interfaccia dell'applicazione, thread IP interno, timer periodici IP e driver di rete.

> [!NOTE]
> *NetX Duo presuppone l'esistenza di ThreadX e dipende dall'esecuzione del thread, dalla sospensione, dai timer periodici e dalle funzionalità di esclusione reciproca.*

### <a name="initialization"></a>Inizializzazione

Il servizio ***nx_system_initialize** _ deve essere chiamato prima che venga chiamato qualsiasi altro servizio NetX Duo. L'inizializzazione del sistema può essere chiamata dalla funzione ThreadX _ *_tx_application_define_** o dai thread dell'applicazione.

Dopo che *** nx_system_initialize** _ restituisce , il sistema è pronto per creare pool di pacchetti e istanze IP. Poiché la creazione di un'istanza IP richiede un pool di pacchetti predefinito, deve esistere almeno un pool di pacchetti NetX Duo prima di creare un'istanza IP. La creazione di pool di pacchetti e istanze IP è consentita dalla funzione di *_inizializzazione_* ThreadX _ tx_application_define * e dai thread dell'applicazione.

Internamente, la creazione di un'istanza IP viene eseguita in due parti: la prima parte viene eseguita all'interno del contesto del chiamante, ***da tx_application_define*** o dal contesto di un thread dell'applicazione. Ciò include la configurazione della struttura dei dati IP e la creazione di varie risorse IP, incluso il thread IP interno. La seconda parte viene eseguita durante l'esecuzione iniziale dal thread IP interno. In questo caso viene chiamato per la prima volta il driver di rete, fornito durante la prima parte della creazione dell'indirizzo IP. La chiamata del driver di rete dal thread IP interno consente al driver di eseguire operazioni di I/O e sospendere durante l'elaborazione dell'inizializzazione.

Quando il driver di rete viene restituito dall'elaborazione dell'inizializzazione, la creazione dell'indirizzo IP è stata completata.

L'inizializzazione di IPv6 in NetX Duo richiede alcuni servizi NetX Duo aggiuntivi. Queste informazioni sono descritte in modo più dettagliato nella sezione [IPv6 in NetX Duo](#ipv6-in-netx-duo) più avanti in questo capitolo.

> [!NOTE]
> *Il servizio NetX Duo **nx_ip_status_check** disponibile per ottenere informazioni sull'istanza IP e sul relativo stato dell'interfaccia primaria. Tali informazioni sullo stato includono se il collegamento è inizializzato, abilitato e l'indirizzo IP viene risolto. Queste informazioni vengono usate per sincronizzare i thread dell'applicazione che devono usare un'istanza IP appena creata. Per i sistemi multihome, vedere [Supporto multihome.](#multihome-support) **nx_ip_interface_status_check** è disponibile per ottenere 3informazioni sull'interfaccia specificata.*

### <a name="application-interface-calls"></a>Chiamate all'interfaccia dell'applicazione

Le chiamate dall'applicazione vengono in gran parte effettuate da thread dell'applicazione in esecuzione nell'RTOS ThreadX. Tuttavia, alcuni servizi di inizializzazione, creazione e abilitazione possono essere chiamati ***da tx_application_define***. Le sezioni "Allowed From" del capitolo 4 - Descrizione di [Azure RTOS NetX Duo Services](chapter4.md) indicano da cui è possibile chiamare ogni servizio NetX Duo.

Nella maggior parte dei casi, l'elaborazione di attività intensive come il calcolo dei checksum viene eseguita all'interno del contesto del thread chiamante, senza bloccare l'accesso di altri thread all'istanza IP. Durante la trasmissione, ad esempio, il calcolo del checksum UDP viene eseguito all'interno del servizio ***nx_udp_socket_send** _, prima di chiamare la funzione di invio IP sottostante. In un pacchetto ricevuto, il checksum UDP viene calcolato nel servizio _ *_nx_udp_socket_receive_** , eseguito nel del thread dell'applicazione. Ciò consente di evitare lo stallo delle richieste di rete di thread con priorità più elevata a causa dell'elaborazione di calcoli di checksum intensivi nei thread con priorità inferiore.

I valori, ad esempio indirizzi IP e numeri di porta, vengono passati alle API nell'ordine dei byte dell'host. Internamente questi valori vengono archiviati anche nell'ordine dei byte dell'host. Ciò consente agli sviluppatori di visualizzare facilmente i valori tramite un debugger. Quando questi valori vengono programmati in un frame per la trasmissione, vengono convertiti nell'ordine dei byte di rete.

### <a name="internal-ip-thread"></a>Thread IP interno

Come accennato, ogni istanza IP in NetX Duo ha un proprio thread. La priorità e le dimensioni dello stack del thread IP interno sono definite nel ***nx_ip_create*** servizio. Il thread IP interno viene creato in modalità ready-to-execute. Se il thread IP ha una priorità più alta rispetto al thread chiamante, la precedenza può verificarsi all'interno della chiamata di creazione IP.

Il punto di ingresso del thread IP interno si trova nella funzione interna _ ***nx_ip_thread_entry***. All'avvio, il thread IP interno completa prima l'inizializzazione del driver di rete, che consiste nell'effettuare tre chiamate al driver di rete specifico dell'applicazione. La prima chiamata è connettere il driver di rete all'istanza IP, seguita da una chiamata di inizializzazione, che consente al driver di rete di eseguire il processo di inizializzazione. Dopo che il driver di rete è stato restituito dall'inizializzazione (potrebbe essere sospeso durante l'attesa della corretta configurazione dell'hardware), il thread IP interno chiama nuovamente il driver di rete per abilitare il collegamento. Dopo che il driver di rete è stato restituito dalla chiamata di abilitazione del collegamento, il thread IP interno entra in un ciclo permanente verificando la presenza di vari eventi che necessitano di elaborazione per questa istanza IP. Gli eventi elaborati in questo ciclo includono la ricezione posticipata dei pacchetti IP, l'assembly del frammento di pacchetti IP, l'elaborazione ping ICMP, l'elaborazione IGMP, l'elaborazione della coda di pacchetti TCP, l'elaborazione periodica TCP, i timeout dell'assembly del frammento IP e l'elaborazione periodica IGMP. Gli eventi includono anche le attività di risoluzione degli indirizzi. Elaborazione di pacchetti ARP ed elaborazione periodica ARP in IPv4, Rilevamento indirizzi duplicati, Richiesta router e Individuazione router adiacente in IPv6.

> [!CAUTION]
> *Le funzioni di callback di NetX Duo, inclusi i callback di ascolto e disconnessione, vengono chiamate dal thread IP interno, non dal thread chiamante originale. L'applicazione deve fare attenzione a non sospendere all'interno di qualsiasi funzione di callback di NetX Duo.*

### <a name="ip-periodic-timers"></a>Timer periodici IP

Per ogni istanza IP vengono usati due timer periodici ThreadX. Il primo è un timer di un secondo per ARP, IGMP, timeout TCP e determina anche l'elaborazione del riassemblo dei frammenti IP. Il secondo timer è un timer di 100 ms per guidare il timeout di ritrasmissione TCP e le operazioni correlate a IPv6.

### <a name="network-driver"></a>Driver di rete

Ogni istanza IP in NetX Duo ha un'interfaccia primaria, identificata dal relativo driver di dispositivo specificato nel nx_ip_create ***servizio.*** Il driver di rete è responsabile della gestione di varie richieste NetX Duo, tra cui trasmissione di pacchetti, ricezione di pacchetti e richieste di stato e controllo. 

Per un sistema multi-home, l'istanza IP ha più interfacce, ognuna con un driver di rete associato che esegue queste attività per la rispettiva interfaccia.

Il driver di rete deve anche gestire gli eventi asincroni che si verificano nel supporto. Gli eventi asincroni dai supporti includono la ricezione di pacchetti, il completamento della trasmissione di pacchetti e le modifiche di stato. NetX Duo fornisce al driver di rete diverse funzioni di accesso per gestire vari eventi. Queste funzioni sono progettate per essere chiamate dalla parte di routine del servizio interrupt del driver di rete. Per le reti IPv4, il driver di rete deve inoltrare tutti i pacchetti ARP ricevuti alla _nx_arp_packet_deferred_receive ***funzione*** interna. Tutti i pacchetti RARP devono essere inoltrati a ***_nx_rarp_packet_deferred_receive** _ funzione interna. Sono disponibili due opzioni per i pacchetti IP. Se è necessario un invio rapido di pacchetti IP, i pacchetti IP in ingresso devono essere inoltrati a *_ _nx_ip_packet_receive_* _ per l'elaborazione immediata. Ciò migliora notevolmente le prestazioni di NetX Duo nella gestione dei pacchetti IP. In caso contrario, è necessario inoltrare pacchetti IP *a _ _ _nx_ip_packet_deferred_receive_** . Questo servizio inserisce il pacchetto IP nella coda di elaborazione posticipata in cui viene quindi gestito dal thread IP interno, con il risultato della quantità minima di tempo di elaborazione ISR.

Il driver di rete può anche rinviare l'elaborazione dell'interrupt per l'esecuzione fuori dal contesto del thread IP. In questa modalità, l'ISR deve salvare le informazioni necessarie, chiamare la funzione interna ***_nx_ip_driver_deferred_processing*** e confermare il controller di interrupt. Questo servizio notifica al thread IP di pianificare un callback al driver di dispositivo per completare il processo dell'evento che causa l'interruzione.

Alcuni controller di rete sono in grado di eseguire il calcolo e la convalida del checksum dell'intestazione TCP/IP nell'hardware, senza occupare risorse preziose della CPU. Per sfruttare i vantaggi della funzionalità hardware, NetX Duo offre opzioni per abilitare o disabilitare vari calcoli del checksum software in fase di compilazione, oltre ad attivare o disattivare il calcolo del checksum in fase di esecuzione, se il driver di dispositivo è in grado di comunicare con il livello IP su è funzionalità hardware. Per informazioni più dettagliate sulla scrittura [di driver di rete NetX Duo, vedere](chapter5.md) capitolo 5 - Azure RTOS driver di rete NetX Duo.

### <a name="multihome-support"></a>Supporto multihome

NetX Duo supporta i sistemi connessi a più dispositivi fisici usando una singola istanza IP. Ogni interfaccia fisica viene assegnata a un blocco di controllo dell'interfaccia nell'istanza IP. Le applicazioni che vogliono usare un sistema multihome devono definire il valore per ***NX_MAX_PHSYCIAL_INTERFACES** _ al numero di dispositivi fisici collegati al sistema e ricompilare la libreria NetX Duo. Per impostazione predefinita _ *_NX_MAX_PHYSICAL_INTERFACES_** è impostato su uno, creando un blocco di controllo dell'interfaccia nell'istanza IP.

L'applicazione NetX Duo crea una singola istanza IP per il dispositivo primario usando ***nx_ip_create** _service. Per ogni dispositivo di rete aggiuntivo, l'applicazione collega il dispositivo all'istanza IP usando il servizio _ *_nx_ip_interface_attach_**.

Ogni struttura dell'interfaccia di rete contiene un subset di informazioni di rete sull'interfaccia di rete contenute nel blocco di controllo IP, tra cui l'indirizzo IPv4 dell'interfaccia, subnet mask, le dimensioni MTU IP e le informazioni sull'indirizzo a livello MAC.

> [!NOTE]
> *NetX Duo con supporto multihome è compatibile con le versioni precedenti di NetX Duo. Per impostazione predefinita, i servizi che non accettano informazioni esplicite sull'interfaccia sono il dispositivo di rete primario.*

L'interfaccia primaria ha indice zero nell'elenco di istanze IP. A ogni dispositivo successivo collegato all'istanza IP viene assegnato l'indice successivo.

Tutti i servizi di protocollo di livello superiore per cui è abilitata l'istanza IP, inclusi TCP, UDP, ICMP e IGMP, sono disponibili per tutti i dispositivi collegati.

Nella maggior parte dei casi, NetX Duo può determinare l'indirizzo di origine migliore da usare per la trasmissione di un pacchetto. La selezione dell'indirizzo di origine si basa sull'indirizzo di destinazione. I servizi NetX Duo vengono aggiunti per consentire alle applicazioni di specificare un indirizzo di origine specifico da usare, nei casi in cui il più adatto non può essere determinato dall'indirizzo di destinazione. Ad esempio, in un sistema multihome un'applicazione deve inviare un pacchetto a un indirizzo di destinazione multicast o broadcast IPv4.

I servizi specifici per lo sviluppo di applicazioni multihome includono:

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

Questi servizi sono illustrati in modo più dettagliato in [Descrizione di NetX Duo Services.](chapter4.md)

### <a name="loopback-interface"></a>Interfaccia loopback

L'interfaccia di loopback è un'interfaccia di rete speciale a cui non è collegato un collegamento fisico. L'interfaccia di loopback consente alle applicazioni di comunicare usando l'indirizzo di loopback IPv4 127.0.0.1 Per usare un'interfaccia di loopback logico, assicurarsi che l'opzione configurabile ***NX_DISABLE_LOOPBACK_INTERFACE*** non sia impostata.

### <a name="interface-control-blocks"></a>Blocchi di controllo dell'interfaccia

Il numero di blocchi di controllo dell'interfaccia nell'istanza IP è il numero di interfacce fisiche (definite da ***NX_MAX_PHYSICAL_INTERFACES** _) più l'interfaccia di loopback, se abilitata. Il numero totale di interfacce è definito in __*_ NX_MAX_IP_INTERFACES **.

## <a name="protocol-layering"></a>Layering del protocollo

Il protocollo TCP/IP implementato da NetX Duo è un protocollo a più livelli, che significa che i protocolli più complessi sono compilati in base a protocolli sottostanti più semplici. In TCP/IP il protocollo di livello più basso è a *livello di collegamento* e viene gestito dal driver di rete. Questo livello è in genere destinato a Ethernet, ma può anche essere in fibra ottica, seriale o praticamente qualsiasi supporto fisico.

Sopra il livello di collegamento si trova il *livello di rete*. In TCP/IP si tratta dell'ip, che è fondamentalmente responsabile dell'invio e della ricezione di pacchetti semplici attraverso la rete nel modo più efficiente possibile. I protocolli di tipo gestione come ICMP e IGMP sono in genere anche classificati come livelli di rete, anche se si basano su IP per l'invio e la ricezione.

Il *livello di* trasporto si posiziona sopra il livello di rete. Questo livello è responsabile della gestione del flusso di dati tra gli host nella rete. NetX Duo supporta due tipi di servizi di trasporto: UDP e TCP. I servizi UDP offrono il massimo sforzo per inviare e ricevere dati tra due host in modo senza connessione, mentre TCP offre un servizio orientato alla connessione affidabile tra due entità host.

Questo layering si riflette nei pacchetti di dati di rete effettivi. Ogni livello in TCP/IP contiene un blocco di informazioni denominato intestazione. Questa tecnica di dati circostante (ed eventualmente informazioni sul protocollo) con un'intestazione è in genere denominata incapsulamento dei dati. La figura 1 mostra un esempio di layering di NetX Duo e la Figura 2 mostra l'incapsulamento dei dati risultante per i dati UDP inviati.

![Layering del protocollo](./media/user-guide/image12.jpg)

**FIGURA 1. Layering del protocollo**

## <a name="packet-pools"></a>Pool di pacchetti

L'allocazione di pacchetti in modo rapido e deterministico è sempre una sfida nelle applicazioni di rete in tempo reale. A questo scopo, NetX Duo offre la possibilità di creare e gestire più pool di pacchetti di rete di dimensioni fisse.

Poiché i pool di pacchetti di NetX Duo sono costituiti da blocchi di memoria di dimensioni fisse, non si verificano mai problemi di frammentazione interna. Naturalmente, la frammentazione causa un comportamento intrinsecamente non deterministico. Inoltre, il tempo necessario per allocare e liberare un pacchetto NetX Duo è necessario per la semplice manipolazione dell'elenco collegato. Inoltre, l'allocazione e la deallocazione dei pacchetti vengono eseguite all'inizio dell'elenco disponibile. In questo modo si garantisce la massima velocità di elaborazione dell'elenco collegato.

![Incapsulamento dei dati UDP](./media/user-guide/image13.png)

**FIGURA 2. Incapsulamento dei dati UDP**

La mancanza di flessibilità è in genere lo svantaggio principale dei pool di pacchetti di dimensioni fisse. Determinare le dimensioni ottimali del payload dei pacchetti che gestisce anche il pacchetto in ingresso nel caso peggiore è un'attività difficile. I pacchetti NetX Duo affrontano questo problema con una funzionalità facoltativa denominata concatenamento di pacchetti. Un pacchetto di rete effettivo può essere costituito da uno o più pacchetti NetX Duo collegati tra loro. Inoltre, l'intestazione del pacchetto mantiene un puntatore all'inizio del pacchetto. Quando vengono aggiunti altri protocolli, questo puntatore viene semplicemente spostato indietro e la nuova intestazione viene scritta direttamente davanti ai dati. Senza la tecnologia dei pacchetti flessibile, lo stack dovrebbe allocare un altro buffer e copiare i dati in un nuovo buffer con la nuova intestazione, che richiede un'elaborazione intensiva.

Poiché le dimensioni di ogni payload del pacchetto sono fisse per un determinato pool di pacchetti, i dati dell'applicazione di dimensioni superiori a quelle del payload richiederebbero più pacchetti concatenati. Quando si compila un pacchetto con i dati utente, l'applicazione userà il servizio ***nx_packet_data_append***. Questo servizio sposta i dati dell'applicazione in un pacchetto. Nelle situazioni in cui un pacchetto non è sufficiente per contenere i dati utente, vengono allocati pacchetti aggiuntivi per archiviare i dati utente. Per usare il concatenamento dei pacchetti, il driver deve essere in grado di ricevere o trasmettere da pacchetti concatenati.

Per i sistemi incorporati che non devono usare la funzionalità di concatenamento dei pacchetti, la libreria NetX Duo può essere compilata con ***NX_DISABLE_PACKET_CHAIN** _ per rimuovere la logica di concatenamento dei pacchetti. Si noti che la funzionalità frammentazione IP e riassemblaggio potrebbe richiedere l'utilizzo della funzionalità di pacchetti concatenati. Pertanto, la _*_NX_DISABLE_PACKET_CHAIN_*_ richiede la *_definizione NX_DISABLE_FRAGMENTATION_* _ NX_DISABLE_FRAGMENTATION * . 

Ogni pool di memoria di pacchetti di NetX Duo è una risorsa pubblica. NetX Duo non pone vincoli sul modo in cui vengono usati i pool di pacchetti. 

### <a name="packet-pool-memory-area"></a>Area di memoria del pool di pacchetti

L'area di memoria per il pool di pacchetti viene specificata durante la creazione. Analogamente ad altre aree di memoria per gli oggetti ThreadX e NetX Duo, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione. 

Si tratta di una funzionalità importante a causa della notevole flessibilità che offre all'applicazione. Si supponga, ad esempio, che un prodotto di comunicazione abbia un'area di memoria ad alta velocità per i buffer di rete. Questa area di memoria viene facilmente utilizzata rendendola in un pool di memoria di pacchetti NetX Duo.

### <a name="creating-packet-pools"></a>Creazione di pool di pacchetti

I pool di pacchetti vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Non sono previsti limiti al numero di pool di memoria di pacchetti in un'applicazione NetX Duo.

### <a name="dual-packet-pool"></a>Pool di pacchetti doppio

In genere le dimensioni del payload del pool di pacchetti IP predefinito sono sufficientemente grandi da contenere le dimensioni dei frame fino all'MTU dell'interfaccia di rete. Durante il normale funzionamento, il thread IP deve inviare messaggi come ARP, messaggi di controllo TCP, messaggi IGMP, messaggi ICMPv6. Questi messaggi usano i pacchetti allocati dal pool di pacchetti predefinito nell'istanza IP. In un sistema con vincoli di memoria in cui la quantità di memoria disponibile per il pool di pacchetti è limitata, l'uso di un singolo pool di pacchetti (con dimensioni del payload di grandi dimensioni corrispondenti alle dimensioni MTU) potrebbe non essere una soluzione ottimale. NetX Duo consente all'applicazione di installare un pool di pacchetti ausiliario, in cui le dimensioni del payload sono inferiori. Dopo aver installato il pool di pacchetti ausiliario, il thread helper IP alloca pacchetti dal pool di pacchetti predefinito o dal pool ausiliario, a seconda delle dimensioni del messaggio trasmesso. Per un pool di pacchetti ausiliario, una dimensione del payload di 200 byte funziona con la maggior parte dei messaggi trasmessi dal thread helper IP.

Per impostazione predefinita, la libreria NetX Duo viene compilata senza abilitare il doppio pool di pacchetti. Per abilitare la funzionalità, compilare la libreria con *** NX_DUAL_PACKET_POOL_ENABLE** _ definito. È quindi possibile impostare il pool di pacchetti ausiliario chiamando _*_nx_ip_auxiliary_packet_pool_set_**.

È anche possibile creare più pool di pacchetti. Ad esempio, viene creato un pool di pacchetti di trasmissione con dimensioni di payload ottimali per le dimensioni previste dei messaggi. Nel driver viene creato un pool di pacchetti di ricezione con una dimensione del payload impostata sull'MTU del driver, poiché non è possibile prevedere le dimensioni dei pacchetti ricevuti.

### <a name="packet-header-nx_packet"></a>Intestazione pacchetto NX_PACKET   
Per impostazione predefinita, NetX Duo posiziona l'intestazione del pacchetto immediatamente prima dell'area del payload del pacchetto. Il pool di memoria dei pacchetti è fondamentalmente una serie di pacchetti, ovvero intestazioni seguite immediatamente dal payload dei pacchetti. L'intestazione del ***pacchetto ( NX_PACKET***) e il layout del pool di pacchetti sono mostrati nella figura 3.

Per i driver di dispositivi di rete che sono in grado di eseguire zero operazioni di copia, in genere l'indirizzo iniziale dell'area del payload del pacchetto viene programmato nella logica DMA. Alcuni motori DMA hanno requisiti di allineamento nell'area del payload. Per fare in modo che l'indirizzo iniziale dell'area del payload sia allineato correttamente per il motore DMA o per l'operazione di cache, l'utente può definire il ***simbolo NX_PACKET_ALIGNMENT***.

> [!WARNING]
> *È importante che il driver di rete usi la **nx_packet_transmit_release** al termine della trasmissione di un pacchetto. Questa funzione verifica che il pacchetto non sia in una coda di output TCP prima di essere effettivamente inserito nuovamente nel pool disponibile.*

![Layout dell'intestazione del pacchetto e del pool di pacchetti](./media/user-guide/image14.jpg)

**FIGURA 3. Layout dell'intestazione del pacchetto e del pool di pacchetti**

I campi dell'intestazione del pacchetto sono definiti come segue. Si noti che questa tabella non è un elenco completo di tutti i membri nella *NX_PACKET* struttura .

|Intestazione del pacchetto | Scopo |
|---|---|
|***nx_packet_pool_owner***|Questo campo punta al pool di pacchetti proprietario di questo particolare pacchetto. Quando il pacchetto viene rilasciato, viene rilasciato a questo pool specifico. Con la proprietà del pool all'interno di ogni pacchetto, è possibile che un datagramma si estendono su più pacchetti da più pool di pacchetti.|
|***nx_packet_next** _|Questo campo punta al pacchetto successivo all'interno dello stesso frame. Se NULL, non sono presenti pacchetti aggiuntivi che fanno parte del frame. Questo campo viene usato anche per contenere pacchetti frammentati fino a quando l'intero pacchetto non può essere riassemblato. viene rimosso se _*_NX_DISABLE_PACKET_CHAIN_**è definito.|
|***nx_packet_last** _|Questo campo punta all'ultimo pacchetto all'interno dello stesso pacchetto di rete. Se NULL, questo pacchetto rappresenta l'intero pacchetto di rete. Questo campo viene rimosso se _*_NX_DISABLE_PACKET_CHAIN_ è definito **.|
|***nx_packet_length** _| Questo campo contiene il numero totale di byte nell'intero pacchetto di rete, incluso il totale di tutti i byte in tutti i pacchetti concatenati dal _nx_packet_next*membro.|
|***nx_packet_ip_interface***| Questo campo è il blocco di controllo dell'interfaccia assegnato al pacchetto quando viene ricevuto dal driver di interfaccia e da NetX Duo per i pacchetti in uscita. Un blocco di controllo dell'interfaccia descrive l'interfaccia, ad esempio l'indirizzo di rete, l'indirizzo MAC, l'indirizzo IP e lo stato dell'interfaccia, ad esempio il collegamento abilitato e il mapping fisico obbligatorio.|
|***nx_packet_data_start** _| Questo campo punta all'inizio dell'area del payload fisico di questo pacchetto. Non deve essere immediatamente dopo l'intestazione NX_PACKET, ma è l'impostazione predefinita per il servizio _ *_nx_packet_pool_create_**.|
|***nx_packet_data_end** _|Questo campo punta alla fine dell'area del payload fisico di questo pacchetto. La differenza tra questo campo e il campo _nx_packet_data_start* rappresenta le dimensioni del payload.|
|***nx_packet_prepend_ptr** _|Questo campo punta alla posizione in cui i dati del pacchetto, ovvero l'intestazione del protocollo o i dati effettivi, vengono aggiunti davanti ai dati del pacchetto esistenti (se presenti) nell'area del payload del pacchetto. Deve essere maggiore o uguale alla posizione del puntatore _nx_packet_data_start* e minore o uguale al puntatore *nx_packet_append_ptr.*|
> [!CAUTION]
> *Per motivi di prestazioni, NetX Duo presuppone che quando il pacchetto viene passato ai servizi NetX Duo per la trasmissione, il puntatore anteposto punta all'indirizzo allineato alle parole lunghe.*

| Intestazione del pacchetto | Scopo |
|---|---|
|***nx_packet_append_ptr** _|Questo campo punta alla fine dei dati attualmente presenti nell'area del payload del pacchetto. Deve essere compreso tra la posizione di memoria a cui punta _nx_packet_prepend_ptr* e *nx_packet_data_end.* La differenza tra questo campo e *il campo nx_packet_prepend_ptr* rappresenta la quantità di dati in questo pacchetto.|
|***nx_packet_packet_pad** _|Questo campo definisce la lunghezza del riempimento in parole a 4 byte per ottenere il requisito di allineamento desiderato. Questo campo viene rimosso _*_se NX_PACKET_HEADER_PAD_*_ non è definito. In _*_alternativa NX_PACKET_ALIGNMENT_*_ possibile usare invece di definire _nx_packet_header_pad.*|

### <a name="packet-header-offsets"></a>Offset dell'intestazione del pacchetto

Le dimensioni dell'intestazione del pacchetto vengono definite per consentire spazio sufficiente per contenere le dimensioni dell'intestazione. Il ***nx_packet_allocate*** viene usato per allocare un pacchetto e regola il puntatore anteposto nel pacchetto in base al tipo di pacchetto specificato. Il tipo di pacchetto indica a NetX Duo l'offset necessario per inserire l'intestazione del protocollo (ad esempio UDP, TCP o ICMP) davanti ai dati del protocollo.

I tipi seguenti sono definiti in NetX Duo per prendere in considerazione l'intestazione IP e l'intestazione del livello fisico (Ethernet) nel pacchetto. Nel secondo caso, si presuppone che siano 16 byte tenendo in considerazione l'allineamento a 4 byte richiesto. I pacchetti IPv4 sono ancora definiti in NetX Duo per le applicazioni per allocare pacchetti per le reti IPv4. Si noti che se la libreria NetX Duo viene compilata con IPv6 abilitato, i tipi di pacchetti generici (ad esempio NX_IP_PACKET) vengono mappati alla versione IPv6. Se la libreria NetX Duo viene compilata senza IPv6 abilitato, questi tipi di pacchetti generici vengono mappati alla versione IPv4.

La tabella seguente mostra i simboli definiti con IPv6 abilitato:

|**Tipo di pacchetto** |**Valore** |
|---|---|
|NX_IPv6_PACKET (NX_IP_PACKET) | 0x38 |
|NX_UDPv6_PACKET (NX_UDP_PACKET) |0x40 |
|NX_TCPv6_PACKET (NX_TCP_PACKET) |0x4c |
|NX_IPv4_PACKET |0x24 |
|NX_IPv4_UDP_PACKET |0x2c |
|NX_IPv4_TCP_PACKET |0x38 |

La tabella seguente mostra i simboli definiti con IPv6 disabilitato:

|**Tipo di pacchetto** |**Valore** |
|---|---|
|NX_IPv4_PACKET (NX_IP_PACKET) |0x24 |
|NX_IPv4_UDP_PACKET (NX_UDP_PACKET) |0x2c |
|NX_IPv4_TCP_PACKET (NX_TCP_PACKET) |0x38 |

Si noti che questi valori cambieranno *se NX_IPSEC_ENABLE* è definito . Per le applicazioni che usano IPsec, fare riferimento al Manuale dell'utente di NetX Duo IPsec per altre informazioni.

### <a name="pool-capacity"></a>Capacità del pool

Il numero di pacchetti in un pool di pacchetti è una funzione delle dimensioni del payload e del numero totale di byte nell'area di memoria fornita al servizio di creazione del pool di pacchetti. La capacità del pool viene calcolata dividendo le dimensioni del pacchetto (incluse le dimensioni dell'intestazione NX_PACKET, le dimensioni del payload e l'allineamento appropriato) nel numero totale di byte nell'area di memoria fornita.

### <a name="payload-area-alignment"></a>Allineamento dell'area di payload

La progettazione di pool di pacchetti in NetX Duo supporta la copia zero. A livello di driver di dispositivo, il driver è in grado di assegnare l'area del payload direttamente nei descrittori del buffer per la ricezione dei dati. A volte il motore DMA o il meccanismo di sincronizzazione della cache richiede che l'indirizzo iniziale dell'area del payload abbia un determinato requisito di allineamento. Questo risultato può essere ottenuto definendo il requisito di allineamento desiderato (in ***byte)*** in NX_PACKET_ALIGNMENT . Quando si crea un pool di pacchetti, l'indirizzo iniziale dell'area di payload verrà allineato a questo valore. Per impostazione predefinita, l'indirizzo iniziale è allineato a 4 byte.

### <a name="thread-suspension"></a>Sospensione dei thread

I thread dell'applicazione possono essere sospesi durante l'attesa di un pacchetto da un pool vuoto. Quando un pacchetto viene restituito al pool, il thread sospeso viene assegnato e ripreso.

Se più thread vengono sospesi nello stesso pool di pacchetti, vengono ripresi nell'ordine in cui sono stati sospesi (FIFO).

### <a name="pool-statistics-and-errors"></a>Statistiche ed errori del pool

Se abilitato, il software di gestione dei pacchetti NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per i pool di pacchetti vengono mantenute le statistiche e i report degli errori seguenti:

- Totale pacchetti nel pool
- Pacchetti liberi nel pool
- Totale allocazioni di pacchetti
- Richieste di allocazione vuote del pool
- Sospensioni di allocazione vuote del pool
- Versioni di pacchetti non valide

Tutte queste statistiche e segnalazioni errori, ad eccezione del numero totale e gratuito di pacchetti nel pool, sono incorporate nella libreria NetX Duo, a meno che **non venga** definito * NX_DISABLE_PACKET_INFO _ . Questi dati sono disponibili per l'applicazione con il servizio _ *_nx_packet_pool_info_get_**.

### <a name="packet-pool-control-block-nx_packet_pool"></a>Blocco di controllo del pool di pacchetti NX_PACKET_POOL

Le caratteristiche di ogni pool di memoria di pacchetti si trovano nel relativo blocco di controllo. Contiene informazioni utili, ad esempio l'elenco collegato di pacchetti gratuiti, il numero di pacchetti gratuiti e le dimensioni del payload per i pacchetti in questo pool. Questa struttura è definita nel file ***nx_api.h.***

I blocchi di controllo del pool di pacchetti possono trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

## <a name="ipv4-protocol"></a>Protocollo IPv4

Il componente IP (Internet Protocol) di NetX Duo è responsabile dell'invio e della ricezione di pacchetti IPv4 su Internet. In NetX Duo è il componente responsabile dell'invio e della ricezione di messaggi TCP, UDP, ICMP e IGMP, utilizzando il driver di rete sottostante.

NetX Duo supporta sia il protocollo IPv4 (RFC 791) che il protocollo IPv6 (RFC 2460). Questa sezione illustra IPv4. IPv6 è illustrato nella sezione successiva.

### <a name="ipv4-addresses"></a>Indirizzi IPv4

Ogni host su Internet ha un identificatore univoco a 32 bit denominato indirizzo IP. Esistono cinque classi di indirizzi IPv4, come descritto nella figura 4. Gli intervalli delle cinque classi di indirizzi IPv4 sono i seguenti:

|Classe|Intervallo|
|---|---|
|Una |Da 0.0.0.0 a 127.255.255.255|
|B |Da 128.0.0.0 a 191.255.255.255.255|
|C |Da 192.0.0.0 a 223.255.255.255|
|D |Da 224.0.0.0 a 239.255.255.255.255|
|E |Da 240.0.0.0 a 247.255.255.255|

![Diagramma della struttura degli indirizzi IPv4.](./media/user-guide/ipv4-address-structure.png)

### <a name="figure-4-ipv4-address-structure"></a>FIGURA 4. Struttura degli indirizzi IPv4

Esistono anche tre tipi di specifiche di indirizzo: *unicast,* *broadcast* e *multicast.* Gli indirizzi unicast sono gli indirizzi IPv4 che identificano un host specifico su Internet. Gli indirizzi unicast possono essere un indirizzo IPv4 di origine o di destinazione. Un indirizzo broadcast identifica tutti gli host in una rete specifica o in una rete secondaria e può essere usato solo come indirizzi di destinazione. Gli indirizzi broadcast vengono specificati con la parte dell'ID host dell'indirizzo impostata su uno. Gli indirizzi multicast (classe D) specificano un gruppo dinamico di host su Internet. I membri del gruppo multicast possono partecipare e uscire ogni volta che lo desiderano.

> [!IMPORTANT]
> *Solo i protocolli senza connessione come UDP su IPv4 possono utilizzare la trasmissione e la funzionalità di trasmissione limitata del gruppo multicast.*

> [!IMPORTANT]
> *La macro *IP_ADDRESS* definita in ***nx_api.h** _. Consente di specificare facilmente gli indirizzi IPv4 usando virgole anziché punti. Ad esempio, _IP_ADDRESS(128,0,0,0)* specifica il primo indirizzo di classe B illustrato nella figura 4.*

### <a name="ipv4-gateway-address"></a>Indirizzo gateway IPv4

I gateway di rete assiste gli host nelle reti per l'inoltro di pacchetti destinati a destinazioni esterne al dominio locale. Ogni nodo è a conoscenza dell'hop successivo a cui inviare, uno dei relativi elementi adiacenti di destinazione o tramite una tabella di routing statica pre-programmata. Tuttavia, se questi approcci hanno esito negativo, il nodo deve inoltrare il pacchetto al gateway predefinito, che ha una conoscenza migliore su come instradare il pacchetto alla destinazione. Si noti che il gateway predefinito deve essere accessibile direttamente tramite una delle interfacce fisiche collegate all'istanza IP. L'applicazione chiama ***nx_ip_gateway_address_set** _ per configurare l'indirizzo del gateway predefinito IPv4. Usare il servizio _*_nx_ip_gateway_address_get_*_ per recuperare le impostazioni correnti del gateway IPv4. L'applicazione userà il servizio _ *_nx_ip_gateway_address_clear_** per cancellare l'impostazione del gateway.

### <a name="ipv4-header"></a>Intestazione IPv4

Per poter inviare qualsiasi pacchetto IPv4 su Internet, deve avere un'intestazione IPv4. Quando i protocolli di livello superiore (UDP, TCP, ICMP o IGMP) chiamano il componente IP per inviare un pacchetto, il modulo di trasmissione IPv4 posiziona un'intestazione IPv4 davanti ai dati. Al contrario, quando i pacchetti IP vengono ricevuti dalla rete, il componente IP rimuove l'intestazione IPv4 dal pacchetto prima del recapito ai protocolli di livello superiore. La figura 5 mostra il formato dell'intestazione IP.

![Formato intestazione IPv4](./media/user-guide/ipv4-header-format.png)

### <a name="figure-5-ipv4-header-format"></a>FIGURA 5. Formato intestazione IPv4

> [!IMPORTANT]
> *È previsto che tutte le intestazioni nell'implementazione TCP/IP siano in **big endian** predefinito. In questo formato, il byte più significativo della parola si trova all'indirizzo di byte più basso. Ad esempio, la versione a 4 bit e la lunghezza dell'intestazione a 4 bit dell'intestazione IP devono trovarsi nel primo byte dell'intestazione.*

I campi dell'intestazione IPv4 sono definiti come segue:

|Campo intestazione &nbsp; IPv4 &nbsp; |Scopo |
|---|---|
|***Versione a 4 bit*** |Questo campo contiene la versione dell'indirizzo IP rappresentato da questa intestazione. Per IP versione 4, che è il supporto di NetX Duo, il valore di questo campo è 4. |
|***Lunghezza intestazione a 4 bit*** |Questo campo specifica il numero di parole a 32 bit nell'intestazione IP. Se non sono presenti parole di opzione, il valore di questo campo è 5. |
|***Tipo di servizio a 8 bit (TOS)*** |Questo campo specifica il tipo di servizio richiesto per questo pacchetto IP. Le richieste valide sono le seguenti:<br />- Normale: 0x00 <br />- Ritardo minimo: 0x00<br />- Numero massimo di dati: 0x08<br />- Affidabilità massima: 0x04<br />- Costo minimo: 0x02 |
|***Lunghezza totale a 16 bit*** |Questo campo contiene la lunghezza totale in byte del datagramma IP, inclusa l'intestazione IP. Un datagramma IP è l'unità di base delle informazioni disponibili in una rete Internet TCP/IP. Contiene un indirizzo di origine e di destinazione oltre ai dati. Poiché si tratta di un campo a 16 bit, la dimensione massima di un datagramma IP è di 65.535 byte.|
|***Identificazione a 16 bit*** |Il campo è un numero usato per identificare in modo univoco ogni datagramma IP inviato da un host. Questo numero viene in genere incrementato dopo l'invio di un datagramma IP. È particolarmente utile per assemblare frammenti di pacchetti IP ricevuti.|
|***Flag a 3 bit*** |Questo campo contiene informazioni sulla frammentazione IP. Il bit 14 è il bit "don't fragment". Se questo bit è impostato, il datagramma IP in uscita non verrà frammentato. Il bit 13 è il bit "more fragments". Se questo bit è impostato, sono presenti più frammenti. Se questo bit è chiaro, questo è l'ultimo frammento del pacchetto IP.|
|***Offset del frammento a 13 bit*** |Questo campo contiene i 13 bit superiori dell'offset del frammento. Per questo scopo, gli offset dei frammenti sono consentiti solo su limiti a 8 byte. Il primo frammento di un datagramma IP frammentato avrà il bit "more fragments" impostato e l'offset sarà 0.|
|***Durata (TTL) a 8 bit*** |Questo campo contiene il numero di router che questo datagramma può passare, limitando fondamentalmente la durata del datagramma.|
|***Protocollo a 8 bit***|Questo campo specifica il protocollo che usa il datagramma IP. Di seguito è riportato un elenco di protocolli validi e dei relativi valori:<br />- ICMP: 0x01 <br />- IGMP: 0x02<br />- TCP: 0X06<br />- UDP: 0X11 |
|***Checksum a 16 bit*** |Questo campo contiene il checksum a 16 bit che copre solo l'intestazione IP. Sono disponibili checksum aggiuntivi nei protocolli di livello superiore che coprono il payload IP. |
|***Indirizzo IP di origine a 32 bit*** |Questo campo contiene l'indirizzo IP del mittente ed è sempre un indirizzo host. |
|***Indirizzo IP di destinazione a 32 bit*** |Questo campo contiene l'indirizzo IP del ricevitore o dei ricevitori se l'indirizzo è un indirizzo broadcast o multicast. |

### <a name="creating-ip-instances"></a>Creazione di istanze IP

Le istanze IP vengono create durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. L'indirizzo IPv4 iniziale, il network mask, il pool di pacchetti predefinito, il driver multimediale e la memoria e la priorità del thread IP interno vengono definiti dal servizio ***nx_ip_create*** anche se l'applicazione intende utilizzare solo reti IPv6. Se l'applicazione inizializza l'istanza IP con il relativo indirizzo IPv4 impostato su un indirizzo non valido (0.0.0.0), si presuppone che l'indirizzo di interfaccia verrà risolto dalla configurazione manuale in un secondo momento, tramite RARP o tramite DHCP o protocolli simili.

Per i sistemi con più interfacce di rete, l'interfaccia primaria viene designata quando si chiama ***nx_ip_create** _. Ogni interfaccia aggiuntiva può essere collegata alla stessa istanza IP chiamando _*_nx_ip_interface_attach_**. Questo servizio archivia le informazioni sull'interfaccia di rete (ad esempio indirizzo IP, network mask) nel blocco di controllo dell'interfaccia e associa l'istanza del driver al blocco di controllo dell'interfaccia nell'istanza IP. Quando il driver riceve un pacchetto di dati, deve archiviare le informazioni sull'interfaccia nella struttura NX_PACKET prima di inoltrarla alla logica di ricezione IP. Si noti che un'istanza IP deve essere già stata creata prima di collegare le interfacce.

I servizi IPv6 non vengono avviati dopo la chiamata di ***nx_ip_create** _. Le applicazioni che vogliono usare i servizi IPv6 devono chiamare il servizio _ *_nx_ipv6_enable_** per avviare IPv6.

Nella rete IPv6 ogni interfaccia in un'istanza IP può avere più indirizzi globali IPv6. Oltre a usare DHCPv6 per l'assegnazione di indirizzi IPv6, un dispositivo può usare anche la configurazione automatica degli indirizzi senza stato. Altre informazioni sono disponibili nelle sezioni "Blocco di controllo IP" e "Risoluzione degli indirizzi IPv6" più avanti in questo capitolo.

### <a name="ip-send"></a>Invio IP

L'elaborazione delle trasmissioni IP in NetX Duo è molto semplificata. Il puntatore anteposto nel pacchetto viene spostato indietro per contenere l'intestazione IP. L'intestazione IP viene completata (con tutte le opzioni specificate dal livello del protocollo chiamante), il checksum IP viene calcolato inline (solo per i pacchetti IPv4) e il pacchetto viene inviato al driver di rete associato. Inoltre, la frammentazione in uscita viene coordinata anche dall'interno dell'elaborazione di invio IP.

Per IPv4, NetX Duo avvia le richieste ARP se è necessario il mapping fisico per l'indirizzo IP di destinazione. IPv6 usa l'individuazione router adiacenti per il mapping indirizzo-indirizzo-fisico-IPv6.

> [!NOTE]
> *Per la connettività IPv4, i pacchetti che richiedono la risoluzione degli indirizzi IP (ad esempio, il mapping fisico) vengono accodati nella coda ARP finché il numero di pacchetti in coda supera la profondità della coda ARP (definita dal simbolo **NX_ARP_MAX_QUEUE_DEPTH**). Se viene raggiunta la profondità della coda, NetX Duo rimuoverà il pacchetto meno recente nella coda e continuerà ad attendere la risoluzione degli indirizzi per i pacchetti rimanenti accodati. D'altra parte, se una voce ARP non viene risolta, i pacchetti in sospeso nella voce ARP vengono rilasciati in caso di timeout della voce ARP.*

Per i sistemi con più interfacce di rete, NetX Duo sceglie un'interfaccia basata sull'indirizzo IP di destinazione. La procedura seguente si applica al processo di selezione:

1. Se il mittente specifica un'interfaccia in uscita e l'interfaccia è valida, utilizzare tale interfaccia.
2. Se un indirizzo di destinazione è broadcast O multicast IPv4, viene utilizzata la prima interfaccia fisica abilitata.
3. Se l'indirizzo di destinazione viene trovato nella tabella di routing statico, viene usata l'interfaccia associata al gateway.
4. Se la destinazione è on-link, viene usata l'interfaccia on-link.
5. Se l'indirizzo di destinazione è un indirizzo locale del collegamento (169.254.0.0/16), viene usata la prima interfaccia valida.
6. Se il gateway predefinito è configurato, usare l'interfaccia associata al gateway predefinito per trasmettere il pacchetto.
7. Infine, se uno degli indirizzi IP di interfaccia validi è l'indirizzo locale del collegamento (169.254.0.0/16), questa interfaccia viene usata come indirizzo di origine per la trasmissione.
8. Il pacchetto di output viene eliminato se tutte le attività precedenti hanno esito negativo.

### <a name="ip-receive"></a>Ricezione IP

L'elaborazione della ricezione IP viene chiamata dal driver di rete o dal thread IP interno (per l'elaborazione dei pacchetti nella coda di pacchetti posticipata ricevuta). L'elaborazione della ricezione IP esamina il campo del protocollo e tenta di inviare il pacchetto al componente del protocollo appropriato. Prima che il pacchetto venga effettivamente inviato, l'intestazione IP viene rimossa spostando il puntatore anteposto oltre l'intestazione IP.

L'elaborazione della ricezione IP rileva anche i pacchetti IP frammentati ed esegue i passaggi necessari per riassemblarli se la frammentazione è abilitata. Se la frammentazione è necessaria ma non abilitata, il pacchetto viene eliminato.

NetX Duo determina l'interfaccia di rete appropriata in base all'interfaccia specificata nel pacchetto. Se l'interfaccia del pacchetto è NULL, NetX Duo imposta come predefinita l'interfaccia primaria. Questa operazione viene eseguita per garantire la compatibilità con i driver NetX Duo Ethernet legacy.

### <a name="raw-ip-send"></a>Invio IP non elaborato

Un pacchetto IP non elaborato è un frame IP che contiene il payload del protocollo di livello superiore non supportato (ed elaborato) direttamente da NetX Duo. Un pacchetto non elaborato consente agli sviluppatori di definire le proprie applicazioni basate su IP. Un'applicazione può inviare pacchetti IP non elaborati direttamente usando il servizio ***nxd_ip_raw_packet_send** _ se l'elaborazione di pacchetti IP non elaborati è stata abilitata _*_con il nx_ip_raw_packet_enabled_*_ servizio. Quando si trasmette un pacchetto unicast in una rete IPv6, NetX Duo determina automaticamente l'indirizzo IPv6 di origine migliore da usare per inviare i pacchetti in uscita, in base all'indirizzo di destinazione. Se l'indirizzo di destinazione è un indirizzo multicast (o broadcast per IPv4), tuttavia, NetX Duo per impostazione predefinita verrà impostata sulla prima interfaccia (primaria). Pertanto, per inviare tali pacchetti su interfacce secondarie, l'applicazione deve usare il servizio _ *_nx_ip_raw_packet_source_send_** per specificare l'indirizzo di origine da usare per il pacchetto in uscita.

### <a name="raw-ip-receive"></a>Ricezione IP non elaborato

Se è abilitata l'elaborazione di pacchetti IP non elaborati, l'applicazione può ricevere pacchetti IP non elaborati tramite il servizio ***nx_ip_raw_packet_receive** _. Tutti i pacchetti in ingresso vengono elaborati in base al protocollo specificato nell'intestazione IP. Se il protocollo specifica UDP, TCP, IGMP o ICMP, NetX Duo eelaborare il pacchetto usando il gestore appropriato per il tipo di protocollo di pacchetto. Se il protocollo non è uno di questi protocolli e la ricezione IP non elaborata è abilitata, il pacchetto in ingresso verrà inserito nella coda di pacchetti non elaborati in attesa che l'applicazione lo riceva tramite il _*_servizio nx_ip_raw_packet_receive_**. Inoltre, i thread dell'applicazione possono essere sospesi con un timeout facoltativo durante l'attesa di un pacchetto IP non elaborato. Il numero di pacchetti che possono essere accodati nella coda di pacchetti non elaborati è limitato. Il valore massimo è definito in ***NX_IP_RAW_MAX_QUEUE_DEPTH**_, il cui valore predefinito è 20. Un'applicazione può modificare il valore massimo chiamando il servizio _ *_nx_ip_raw_receive_queue_max_set_**.

In alternativa, la libreria NetX Duo può essere compilata con ***NX_ENABLE_IP_RAW_PACKET_FILTER*.** In questa modalità di funzionamento, l'applicazione fornisce una funzione di callback che viene richiamata ogni volta che viene ricevuto un pacchetto con un tipo di protocollo non gestito. La logica di ricezione IP inoltra il pacchetto alla routine del filtro di ricezione di pacchetti non elaborati definita dall'utente. La routine di filtro decide se mantenere o meno il pacchetto non elaborato per un processo futuro. Il valore restituito dalla routine di callback indica se il pacchetto è stato elaborato dal filtro di ricezione di pacchetti non elaborati. Se il pacchetto viene elaborato dalla funzione di callback, il pacchetto deve essere rilasciato dopo che l'applicazione è stata completata con il pacchetto. In caso contrario, NetX Duo è responsabile del rilascio del pacchetto. Per altre informazioni **_nx_ip_raw_packet_filter_set_** usare la funzione di filtro di pacchetti non elaborati, vedere l'nx_ip_raw_packet_filter_set.

> [!NOTE]
> *La funzione wrapper BSD per NetX Duo si basa sulla funzione di filtro di pacchetti non elaborati per gestire i socket non elaborati BSD. Pertanto, per supportare socket non elaborati nel wrapper BSD, la libreria NetX Duo deve essere compilata con ***NX_ENABLE_IP_RAW_PACKET_FILTER** _ definito e l'applicazione non deve usare _*_il nx_ip_raw_packet_filter_set_*_ per installare il proprio filtro di pacchetti non elaborati functions._

### <a name="default-packet-pool"></a>Pool di pacchetti predefinito

A ogni istanza IP viene assegnato un pool di pacchetti predefinito durante la creazione. Questo pool di pacchetti viene usato per allocare pacchetti per ARP, RARP, ICMP, IGMP, vari pacchetti di controllo TCP (SYN, ACK e così via), individuazione router adiacenti, individuazione router e rilevamento di indirizzi duplicati. Se il pool di pacchetti predefinito è vuoto quando NetX Duo deve allocare un pacchetto, Potrebbe essere necessario interrompere l'operazione specifica e, se possibile, restituirà un messaggio di errore.

### <a name="ip-helper-thread"></a>IP Helper Thread

Ogni istanza IP ha un thread helper. Questo thread è responsabile della gestione di tutte le elaborazioni di pacchetti posticipate e di tutte le elaborazioni periodiche. Il thread helper IP viene creato in ***nx_ip_create.*** Questo è il punto in cui al thread vengono dati lo stack e la priorità. Si noti che la prima elaborazione nel thread helper IP è il completamento dell'inizializzazione del driver di rete associata al servizio di creazione ip. Al termine dell'inizializzazione del driver di rete, il thread helper avvia un ciclo infinito per elaborare i pacchetti e le richieste periodiche.

> [!IMPORTANT]
> *Se viene visualizzato un comportamento inspiegabile all'interno del thread helper IP, l'aumento delle dimensioni dello stack durante il servizio di creazione dell'indirizzo IP è il primo passaggio di debug. Se lo stack è troppo piccolo, il thread helper IP potrebbe sovrascrivere la memoria, causando problemi insoliti.*

### <a name="thread-suspension"></a>Sospensione dei thread

I thread dell'applicazione possono essere sospesi durante il tentativo di ricevere pacchetti IP non elaborati. Dopo la ricezione di un pacchetto non elaborato, il nuovo pacchetto viene assegnato al primo thread sospeso e il thread viene ripreso. Tutti i servizi NetX Duo per la ricezione di pacchetti hanno un timeout di sospensione facoltativo. Quando viene ricevuto un pacchetto o il timeout scade, il thread dell'applicazione viene ripreso con lo stato di completamento appropriato.

### <a name="ip-statistics-and-errors"></a>Statistiche IP ed errori

Se abilitato, NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per ogni istanza IP vengono mantenute le statistiche e i report degli errori seguenti:

- Totale pacchetti IP inviati
- Totale byte IP inviati
- Totale pacchetti IP ricevuti
- Totale byte IP ricevuti
- Totale pacchetti IP non validi
- Totale pacchetti di ricezione IP eliminati
- Totale errori checksum ricezione IP
- Totale pacchetti di invio IP eliminati
- Totale frammenti IP inviati
- Totale frammenti IP ricevuti

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con ***il nx_ip_info_get*** servizio.

### <a name="ip-control-block-nx_ip"></a>Blocco di controllo IP NX_IP

Le caratteristiche di ogni istanza IP si trovano nel relativo blocco di controllo. Contiene informazioni utili, ad esempio gli indirizzi IP e le maschere di rete di ogni dispositivo di rete, e una tabella di mapping degli indirizzi IP e hardware fisici adiacenti. Questa struttura è definita nel file ***nx_api.h** _file. Se IPv6 è abilitato, contiene anche una matrice di indirizzi IPv6, il cui numero è specificato dall'opzione configurabile dall'utente _*_NX_MAX_IPV6_ADDRESSES_**. Il valore predefinito consente a ogni interfaccia di rete fisica di avere tre indirizzi IPv6.

I blocchi di controllo dell'istanza IP possono trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

### <a name="static-ipv4-routing"></a>Routing IPv4 statico

La funzionalità di routing statico consente a un'applicazione di specificare una rete IPv4 e un indirizzo hop successivo per specifici indirizzi IP di destinazione fuori rete. Se il routing statico è abilitato, NetX Duo cerca nella tabella di routing statico una voce corrispondente all'indirizzo di destinazione del pacchetto da inviare. Se non viene trovata alcuna corrispondenza, NetX Duo cerca nell'elenco delle interfacce fisiche e sceglie un indirizzo IP di origine e un indirizzo hop successivo in base all'indirizzo IP di destinazione e all'indirizzo network mask. Se la destinazione non corrisponde ad alcuno degli indirizzi IP dei driver di rete collegati all'istanza IP, NetX Duo sceglie un'interfaccia direttamente connessa al gateway predefinito e usa l'indirizzo IP dell'interfaccia come indirizzo di origine e il gateway predefinito come hop successivo.

È possibile aggiungere e rimuovere voci dalla tabella di routing statica usando rispettivamente i servizi ***nx_ip_static_route_add** _ e _ *_nx_ip_static_route_delete_** . Per usare il routing statico, l'applicazione host deve abilitare questa funzionalità definendo ***NX_ENABLE_IP_STATIC_ROUTING.***

> [!NOTE]
> *Quando si aggiunge una voce alla tabella di routing statico, NetX Duo verifica la presenza di una voce corrispondente per l'indirizzo di destinazione specificato già presente nella tabella. Se ne esiste una, dà la preferenza alla voce con la rete più piccola (prefisso più lungo) nel network mask.*

### <a name="ipv4-forwarding"></a>Inoltro IPv4

Se il pacchetto IPv4 in ingresso non è destinato a questo nodo ed è abilitata la funzionalità di inoltro IPv4, NetX Duo tenta di inoltrare il pacchetto tramite le altre interfacce.  

### <a name="ip-fragmentation"></a>Frammentazione IP

Il dispositivo di rete può avere limiti sulle dimensioni dei pacchetti in uscita. Questo limite è detto unità massima di trasmissione (MTU). L'MTU IP è la dimensione massima del frame IP che un driver del livello di collegamento è in grado di trasmettere senza frammentare il pacchetto IP. Durante una fase di inizializzazione del driver di dispositivo, il modulo driver deve configurare le dimensioni MTU ip tramite il servizio ***nx_ip_interface_mtu_set.***

Sebbene non sia consigliabile, l'applicazione può generare datagrammi di dimensioni superiori al valore MTU IP sottostante supportato dal dispositivo. Prima di trasmettere tale datagramma IP, il livello IP deve frammentare questi pacchetti. Alla ricezione di frame IP frammentati, l'estremità ricevente deve archiviare tutti i frame IP frammentati con lo stesso ID frammentazione e riassemblarli in ordine. Se la logica di ricezione IP non è in grado di raccogliere tutti i frammenti per ripristinare il frame IP originale nel tempo, vengono rilasciati tutti i frammenti. È il protocollo di livello superiore a rilevare tale perdita di pacchetti e a recuperarlo.

La frammentazione IP si applica ai pacchetti IPv4 e IPv6.

Per supportare la frammentazione IP e l'operazione di riassemblaggio, la finestra di progettazione del sistema deve abilitare la funzionalità di frammentazione IP in NetX Duo usando il ***nx_ip_fragment_enable*** ip. Se questa funzionalità non è abilitata, i pacchetti IP frammentati in ingresso vengono eliminati, nonché i pacchetti che superano il valore MTU del driver di rete.

> [!NOTE]
> *La logica di frammentazione IP può essere rimossa completamente definendo ***NX_DISABLE_FRAGMENTATION** _ durante la compilazione della libreria NetX Duo. In questo modo è possibile ridurre le dimensioni del codice di NetX Duo. Si noti che in questa situazione, entrambe le funzioni di frammentazione/riassemblaggio IPv4 e IPv6 sono disabled._

> [!NOTE]
> *Se **NX_DISABLE_CHAINED_PACKET** è definito, la frammentazione IP deve essere disabilitata.*

> [!NOTE]
> *In una rete IPv6, i router non frammentano un datagramma se le dimensioni del datagramma superano le dimensioni minime MTU. Di conseguenza, è il dispositivo mittente a determinare il valore minimo di MTU tra l'origine e la destinazione e a garantire che le dimensioni del datagramma IP non superino il percorso MTU. In NetX Duo l'individuazione MTU PATH IPv6 **può essere** abilitata creando la libreria NetX Duo con il simbolo NX_ENABLE_IPV6_PATH_MTU_DISCOVERY definito.*

## <a name="address-resolution-protocol-arp-in-ipv4"></a>Protocollo ARP (Address Resolution Protocol) in IPv4

Il protocollo ARP (Address Resolution Protocol) è responsabile del mapping dinamico degli indirizzi IPv4 a 32 bit a quelli dei supporti fisici sottostanti (RFC 826). Ethernet è il supporto fisico più tipico e supporta indirizzi a 48 bit. La necessità di ARP è determinata dal driver di rete fornito al servizio ***nx_ip_create** _. Se è necessario il mapping fisico, il driver di rete deve usare il servizio _ *_nx_interface_address_mapping_needed_** per configurare correttamente l'interfaccia del driver.

### <a name="arp-enable"></a>ARP Enable

Per il corretto funzionamento, ARP deve prima essere abilitato dall'applicazione con ***il nx_arp_enable*** servizio. Questo servizio configura varie strutture di dati per l'elaborazione ARP, inclusa la creazione di un'area della cache ARP dalla memoria fornita al servizio ARP enable.

### <a name="arp-cache"></a>ARP Cache

La cache ARP può essere visualizzata come una matrice di strutture di dati di mapping ARP interne. Ogni struttura interna è in grado di mantenere la relazione tra un indirizzo IP e un indirizzo hardware fisico. Inoltre, ogni struttura di dati ha puntatori di collegamento in modo che possa far parte di più elenchi collegati.

L'applicazione può cercare un indirizzo IP dalla cache ARP fornendo l'indirizzo MAC hardware usando il servizio ***nx_arp_ip_address_find** _ se il mapping esiste nella tabella ARP. Analogamente, il servizio _ *_nx_arp_hardware_address_find_** restituisce l'indirizzo MAC per un determinato indirizzo IP.

### <a name="arp-dynamic-entries"></a>Voci dinamiche ARP

Per impostazione predefinita, il servizio ARP enable inserisce tutte le voci nella cache ARP nell'elenco delle voci ARP dinamiche disponibili. NetX Duo allocare una voce ARP dinamica da questo elenco quando viene rilevata una richiesta di invio a un indirizzo IP non mappato. Dopo l'allocazione, viene impostata la voce ARP e viene inviata una richiesta ARP al supporto fisico.

Una voce dinamica può essere creata anche dal ***servizio*** nx_arp_dynamic_entry_set .

> [!IMPORTANT]
> *Se tutte le voci ARP dinamiche sono in uso, la voce ARP usata meno di recente viene sostituita con un nuovo mapping.*

### <a name="arp-static-entries"></a>Voci statiche ARP

L'applicazione può anche configurare il mapping ARP statico usando il simbolo ***nx_arp_static_entry_create** _service. Questo servizio alloca una voce ARP dall'elenco di voci ARP dinamiche e la inserisce nell'elenco statico con le informazioni di mapping fornite dall'applicazione. Le voci ARP statiche non sono soggette a riutilizzo o annidamento. L'applicazione può eliminare una voce statica usando il _*_nx_arp_static_entry_delete_*_. Per rimuovere tutte le voci statiche nella tabella ARP, l'applicazione può usare il servizio _*_nx_arp_static_entries_delete_**.

### <a name="automatic-arp-entry"></a>Voce ARP automatica

NetX Duo registra il mapping IP/MAC del peer dopo le risposte del peer alla richiesta ARP. NetX Duo implementa anche la funzionalità di immissione automatica ARP in cui registra il mapping degli indirizzi IP/MAC peer in base alle richieste ARP non richieste dalla rete. Questa funzionalità consente alla tabella ARP di essere popolata con informazioni peer, riducendo il ritardo necessario per passare attraverso il ciclo di richiesta/risposta ARP. Tuttavia, lo svantaggio dell'abilitazione automatica di ARP è che la tabella ARP tende a riempirsi rapidamente in una rete occupata con molti nodi nel collegamento locale, il che alla fine porterebbe alla sostituzione della voce ARP.

Questa funzionalità è abilitata per impostazione predefinita. Per disabilitarla, la libreria NetX Duo deve essere compilata con il simbolo ***NX_DISABLE_ARP_AUTO_ENTRY*** definito.</p>

### <a name="arp-messages"></a>Messaggi ARP

Come accennato in precedenza, viene inviato un messaggio di richiesta ARP quando l'attività IP rileva che è necessario il mapping per un indirizzo IP. Le richieste ARP vengono inviate periodicamente (ogni ***NX_ARP_UPDATE_RATE** _ secondi) fino a quando non viene ricevuta una risposta ARP corrispondente. Un totale di _ *_NX_ARP_MAXIMUM_RETRIES_** le richieste ARP vengono effettuate prima dell'abbandono del tentativo ARP. Quando viene ricevuta una risposta ARP, le informazioni sull'indirizzo fisico associato vengono archiviate nella voce ARP presente nella cache.

Per i sistemi multihome, NetX Duo determina quale interfaccia inviare le richieste e le risposte ARP in base all'indirizzo di destinazione specificato.

> [!NOTE]
> *I pacchetti IP in uscita vengono accodati mentre NetX Duo attende la risposta ARP. Il numero di pacchetti IP in uscita in coda è definito dalla **costante NX_ARP_MAX_QUEUE_DEPTH**.*

NetX Duo risponde anche alle richieste ARP da altri nodi nella rete IPv4 locale. Quando viene effettuata una richiesta ARP esterna che corrisponde all'indirizzo IP corrente dell'interfaccia che riceve la richiesta ARP, NetX Duo crea un messaggio di risposta ARP che contiene l'indirizzo fisico corrente.

I formati delle richieste e delle risposte ARP Ethernet sono illustrati nella figura 6 e sono descritti di seguito.

| **Campo &nbsp; richiesta/risposta**         | **Scopo**            |
| ---------------------------------- | ---------------------- |
| ***Indirizzo di destinazione Ethernet*** | Questo campo a 6 byte contiene l'indirizzo di destinazione per la risposta ARP ed è una trasmissione (tutte quelle) per le richieste ARP. Questo campo viene installato dal driver di rete. 
| ***Indirizzo di origine Ethernet***      | Questo campo a 6 byte contiene l'indirizzo del mittente della richiesta o della risposta ARP ed è configurato dal driver di rete. |
| ***Tipo di frame*** | Questo campo a 2 byte contiene il tipo di frame Ethernet presente e, per le richieste e le risposte ARP, è uguale a 0x0806. Questo è l'ultimo campo che il driver di rete è responsabile della configurazione. |
| ***Tipo di hardware*** | Questo campo a 2 byte contiene il tipo di hardware, che 0x0001 per Ethernet. |
| ***Tipo di protocollo*** | Questo campo a 2 byte contiene il tipo di protocollo, che è 0x0800 per gli indirizzi IP. |
| ***Dimensioni hardware*** | Questo campo a 1 byte contiene le dimensioni dell'indirizzo hardware, ovvero 6 per gli indirizzi Ethernet. |

![Diagramma del formato di pacchetto ARP.](./media/user-guide/arp-packet-format.png)

**FIGURA 6. Formato pacchetto ARP**

| Campo di &nbsp; richiesta/risposta | Scopo |
|---|---|
| ***Dimensioni del protocollo*** | Questo campo a 1 byte contiene le dimensioni dell'indirizzo IP, ovvero 4 per gli indirizzi IP. |
| ***Codice operazione*** | Questo campo a 2 byte contiene l'operazione per questo pacchetto ARP. Una richiesta ARP viene specificata con il valore 0x0001, mentre una risposta ARP è rappresentata da un valore di 0x0002. |
| ***Indirizzo Ethernet mittente*** | Questo campo a 6 byte contiene l'indirizzo Ethernet del mittente. |
| ***Indirizzo IP mittente*** | Questo campo a 4 byte contiene l'indirizzo IP del mittente. |
| ***Indirizzo Ethernet di destinazione*** | Questo campo a 6 byte contiene l'indirizzo Ethernet della destinazione. |
| ***Indirizzo IP di destinazione*** | Questo campo a 4 byte contiene l'indirizzo IP della destinazione. |

> [!NOTE]
> *Le richieste e le risposte ARP sono pacchetti a livello di Ethernet. Tutti gli altri pacchetti TCP/IP sono incapsulati da un'intestazione di pacchetto IP.*

> [!NOTE]
> *È previsto che tutti i messaggi ARP nell'implementazione TCP/IP siano in **big endian** formato. In questo formato, il byte più significativo della parola si trova all'indirizzo di byte più basso.*

### <a name="arp-aging"></a>ARP Aging

NetX supporta l'invalidazione dinamica automatica delle voci ARP. ***NX_ARP_EXPIRATION_RATE** _ specifica il numero di secondi in cui un indirizzo IP stabilito per il mapping fisico rimane valido. Dopo la scadenza, la voce ARP viene rimossa dalla cache ARP. Il successivo tentativo di invio all'indirizzo IP corrispondente comporta una nuova richiesta ARP. *_L'impostazione di _ NX_ARP_EXPIRATION_RATE_** su zero disabilita l'aging ARP, ovvero la configurazione predefinita.

### <a name="arp-defend"></a>Difesa ARP

Quando viene ricevuta una richiesta ARP o un pacchetto di risposta ARP e il mittente ha lo stesso indirizzo IP, che è in conflitto con l'indirizzo IP di questo nodo, NetX Duo invia una richiesta ARP per tale indirizzo come difesa. Se il pacchetto ARP in conflitto viene ricevuto più di una volta in 10 secondi, NetX Duo non invia altri pacchetti di difesa. L'intervallo predefinito di 10 secondi può essere ridefinito da ***NX_ARP_DEFEND_INTERVAL** _. Questo comportamento segue i criteri specificati nella versione 2.4(c) di RFC5227. Poiché Windows XP ignora l'annuncio ARP come risposta per il probe ARP, l'utente può definire _ *_NX_ARP_DEFEND_BY_REPLY_** per inviare la risposta ARP come difesa aggiuntiva.

### <a name="arp-statistics-and-errors"></a>Statistiche ed errori ARP

Se abilitato, il software NetX Duo ARP tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per l'elaborazione ARP di ogni IP:

- Totale richieste ARP inviate
- Totale richieste ARP ricevute
- Totale risposte ARP inviate 
- Totale risposte ARP ricevute 
- Totale voci dinamiche ARP 
- Totale voci statiche ARP 
- Totale voci ARP obsoleti 
- Totale messaggi ARP non validi 

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con il ***nx_arp_info_get*** servizio.

## <a name="reverse-address-resolution-protocol-rarp-in-ipv4"></a>RaRP (Reverse Address Resolution Protocol) in IPv4

Il protocollo RARP (Reverse Address Resolution Protocol) è il protocollo per richiedere l'assegnazione di rete degli indirizzi IP a 32 bit dell'host (RFC 903). Questa operazione viene eseguita tramite una richiesta RARP e continua periodicamente fino a quando un membro della rete non assegna un indirizzo IP all'interfaccia di rete host in una risposta RARP. L'applicazione crea un'istanza IP dal servizio ***nx_ip_create*** con un indirizzo IP pari a zero. Se RARP è abilitato dall'applicazione, può usare il protocollo RARP per richiedere un indirizzo IP dal server di rete accessibile tramite l'interfaccia con un indirizzo IP pari a zero.

### <a name="rarp-enable"></a>Abilitazione RARP

Per usare RARP, l'applicazione deve creare l'istanza IP con un indirizzo IP pari a zero, quindi abilitare RARP usando il servizio ***nx_rarp_enable***. Per i sistemi multihome, almeno un dispositivo di rete associato all'istanza IP deve avere un indirizzo IP pari a zero. L'elaborazione RARP invia periodicamente messaggi di richiesta RARP per il sistema NetX Duo che richiedono un indirizzo IP fino a quando non viene ricevuta una risposta RARP valida con l'indirizzo IP designato di rete. A questo punto, l'elaborazione RARP è completa.

Dopo aver abilitato RARP, viene disabilitato automaticamente dopo la risoluzione di tutti gli indirizzi dell'interfaccia. L'applicazione può forzare la terminazione di RARP usando il servizio ***nx_rarp_disable***.

### <a name="rarp-request"></a>Richiesta RARP

Il formato di un pacchetto di richiesta RARP è quasi identico al pacchetto ARP illustrato [nella figura 6.](#arp-messages) L'unica differenza è che il campo del tipo di frame 0x8035 e il campo *Codice* operazione è 3, che designa una richiesta RARP. Come accennato in precedenza, le richieste RARP verranno inviate ***periodicamente*** (ogni NX_RARP_UPDATE_RATE secondi) fino a quando non viene ricevuta una risposta RARP con l'indirizzo IP assegnato di rete.

> [!NOTE]
> *È previsto che tutti i messaggi RARP nell'implementazione TCP/IP siano in **big endian** formato. In questo formato, il byte più significativo della parola si trova all'indirizzo di byte più basso.*

### <a name="rarp-reply"></a>Risposta RARP

I messaggi di risposta RARP vengono ricevuti dalla rete e contengono l'indirizzo IP assegnato alla rete per questo host. Il formato di un pacchetto di risposta RARP è quasi identico al pacchetto ARP illustrato nella figura 6. L'unica differenza è che il campo del tipo di frame 0x8035 il campo *Codice* operazione è 4, che definisce una risposta RARP. Dopo la ricezione, l'indirizzo IP viene specificato nell'istanza IP, la richiesta RARP periodica è disabilitata e l'istanza IP è ora pronta per il normale funzionamento della rete.

Per gli host multihome, l'indirizzo IP viene applicato all'interfaccia di rete richiedente. Se sono ancora presenti altre interfacce di rete che richiedono un'assegnazione di indirizzi IP, il servizio RARP periodico continua fino a quando non vengono risolte tutte le richieste di indirizzi IP dell'interfaccia.

> [!NOTE]
> *L'applicazione non deve usare l'istanza IP fino al completamento dell'elaborazione RARP. Il **nx_ip_status_check** può essere usato dalle applicazioni per attendere il completamento di RARP. Per i sistemi multihome, l'applicazione non deve usare l'interfaccia richiedente fino al completamento dell'elaborazione RARP su tale interfaccia. Lo stato dell'indirizzo IP nel dispositivo secondario può essere controllato con il **nx_ip_interface_status_check** servizio.*

### <a name="rarp-statistics-and-errors"></a>Statistiche ed errori RARP

Se abilitato, il software RARP NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per l'elaborazione RARP di ogni IP:

- Totale richieste RARP inviate
- Totale risposte RARP ricevute
- Totale messaggi RARP non validi

Tutte queste statistiche e i report degli errori sono disponibili per l'applicazione con il ***nx_rarp_info_get*** servizio.

## <a name="internet-control-message-protocol-icmp"></a>Internet Control Message Protocol (ICMP)

Internet Control Message Protocol per IPv4 (ICMP) è limitato al passaggio di informazioni di errore e controllo tra i membri della rete IP. Internet Control Message Protocol per IPv6 (ICMPv6) gestisce anche le informazioni sugli errori e sul controllo ed è necessario per i protocolli di risoluzione degli indirizzi, ad esempio il rilevamento degli indirizzi duplicati (DAD) e la configurazione automatica degli indirizzi senza stato.

Come la maggior parte degli altri messaggi del livello applicazione (ad esempio, TCP/IP), i messaggi ICMP e ICMPv6 sono incapsulati da un'intestazione IP con la designazione del protocollo ICMP (o ICMPv6).

### <a name="icmp-statistics-and-errors"></a>Statistiche ed errori ICMP

Se abilitata, NetX Duo tiene traccia di diverse statistiche ed errori ICMP che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per l'elaborazione ICMP di ogni indirizzo IP: 

- Totale ping ICMP inviati  
- Totale timeout ping ICMP 
- Totale thread ping ICMP sospesi 
- Totale risposte ping ICMP ricevute 
- Totale errori di checksum ICMP 
- Totale messaggi ICMP non gestiti 

Tutte queste statistiche e i report degli errori sono disponibili per l'applicazione con il ***nx_icmp_info_get*** servizio.

## <a name="icmpv4-services-in-netx-duo"></a>Servizi ICMPv4 in NetX Duo

### <a name="icmpv4-enable"></a>Abilitazione di ICMPv4

Prima che i messaggi ICMPv4 possano essere elaborati da NetX Duo, l'applicazione deve chiamare il ***servizio nx_icmp_enable*** per abilitare l'elaborazione ICMPv4. Al termine, l'applicazione può inviare richieste ping e inviare pacchetti ping in ingresso.  

### <a name="icmpv4-echo-request"></a>Richiesta echo ICMPv4

Una richiesta echo è un tipo di messaggio ICMPv4 che viene in genere usato per verificare l'esistenza di un nodo specifico nella rete, come identificato dal relativo indirizzo IP host. Il comando ping comune viene implementato usando i messaggi di richiesta echo/risposta echo ICMP. Se l'host specifico è presente, il relativo stack di rete elabora la richiesta ping e le risposte con una risposta ping. La figura 7 illustra in dettaglio il formato del messaggio ping ICMPv4.

![Messaggio ping ICMPv4](./media/user-guide/icmpv4-ping-message.png)  

**FIGURA 7. Messaggio ping ICMPv4**

> [!NOTE]
> *È previsto che tutti i messaggi ICMPv4 nell'implementazione TCP/IP siano in **big endian** formato. In questo formato, il byte più significativo della parola si trova all'indirizzo di byte più basso.*

Di seguito viene descritto il formato di intestazione ICMPv4:

|Campo intestazione |Scopo |
|---|---|
|**Tipo** |Questo campo specifica il messaggio ICMPv4 (bit 31-24). I più comuni sono:<br />- 0: Echo Reply<br />- 3: Destinazione non raggiungibile<br />- 8: Echo Request<br />- 11: Tempo superato<br />- 12: Problema di parametro |
|**Codice** |Questo campo è specifico del contesto nel campo del tipo (bit 23-16). Per una richiesta echo o una risposta, il codice è impostato su zero.|
|**Checksum** |Questo campo contiene il checksum a 16 bit della somma complementare del messaggio ICMPv4, inclusa l'intera intestazione ICMPv4 che inizia con il campo Tipo. Prima di generare il checksum, il campo checksum viene cancellato.|
|**Identificazione** | Questo campo contiene un valore ID che identifica l'host. un host deve usare l'ID estratto da una richiesta ECHO in ECHO REPLY (bit 31-16).|
|**Numero di sequenza** |Questo campo contiene un valore ID. un host deve usare l'ID estratto da una richiesta ECHO in ECHO REPLY (bit 31-16). A differenza del campo dell'identificatore, questo valore cambierà in una successiva richiesta Echo dallo stesso host (bit 15-0).|

### <a name="icmpv4-echo-response"></a>Risposta echo ICMPv4    
Una risposta ping è un altro tipo di messaggio ICMP generato internamente dal componente ICMP in risposta a una richiesta ping esterna. Oltre all'acknowledgement, la risposta ping contiene anche una copia dei dati utente forniti nella richiesta ping.

### <a name="icmpv4-error-messages"></a>Messaggi di errore ICMPv4   
In NetX Duo sono supportati i messaggi di errore ICMPv4 seguenti: 
- Destinazione non raggiungibile 
- Tempo di superamento 
- Problema con i parametri

## <a name="internet-group-management-protocol-igmp"></a>IGMP (Internet Group Management Protocol)

Il Internet Group Management Protocol (IGMP) fornisce un dispositivo per comunicare con i router adiacenti che intende ricevere o aggiungere a un gruppo multicast IPv4 (RFC 1112 e RFC 2236). Un gruppo multicast è fondamentalmente una raccolta dinamica di membri di rete ed è rappresentato da un indirizzo IP di classe D. I membri del gruppo multicast possono uscire in qualsiasi momento e i nuovi membri possono essere uniti in qualsiasi momento. Il coordinamento necessario per l'aggiunta e l'uscita dal gruppo è responsabilità del gruppo IGMP.

> [!NOTE]
> *IGMP è progettato solo per i gruppi multicast IPv4. Non può essere usato nella rete IPv6.*

### <a name="igmp-enable"></a>Abilitazione IGMP     
Prima che qualsiasi attività di multicasting possa avere luogo in NetX Duo, l'applicazione deve chiamare ***il nx_igmp_enable*** servizio. Questo servizio esegue l'inizializzazione IGMP di base in preparazione per le richieste multicast.

### <a name="multicast-ipv4-addressing"></a>Indirizzamento IPv4 multicast  
Come accennato in precedenza, gli indirizzi multicast sono in realtà indirizzi IP di classe D, come illustrato [nella figura 4.](#ipv4-addresses) I 28 bit inferiori dell'indirizzo di classe D corrispondono all'ID del gruppo multicast. È presente una serie di indirizzi multicast predefiniti. Tuttavia, *l'indirizzo di tutti* gli host (244.0.0.1) è particolarmente importante per l'elaborazione IGMP. *L'indirizzo di tutti gli* host viene usato dai router per eseguire query su tutti i membri multicast per segnalare a quali gruppi multicast appartengono.  

### <a name="physical-address-mapping-in-ipv4"></a>Mapping degli indirizzi fisici in IPv4
Gli indirizzi multicast di classe D vengono mappati direttamente agli indirizzi Ethernet fisici compresi tra 01.00.5e.00.00.00 e 01.00.5e.7f.ff.ff. I 23 bit inferiori dell'indirizzo IP multicast vengono mappati direttamente ai 23 bit inferiori dell'indirizzo Ethernet.

### <a name="multicast-group-join"></a>Join a gruppi multicast
Le applicazioni che devono essere unite a un determinato gruppo multicast possono eseguire questa operazione chiamando il ***nx_igmp_multicast_join*** servizio. Questo servizio tiene traccia del numero di richieste per l'aggiunta a questo gruppo multicast. Se questa è la prima richiesta dell'applicazione a partecipare al gruppo multicast, nella rete primaria viene inviato un report IGMP che indica l'intenzione dell'host di partecipare al gruppo. Viene quindi chiamato il driver di rete per configurare l'ascolto dei pacchetti con l'indirizzo Ethernet per questo gruppo multicast.

In un sistema multihome, se il gruppo multicast è accessibile tramite un'interfaccia specifica, l'applicazione deve usare il servizio ***nx_igmp_multicast_interface_join** _ anziché _*_nx_igmp_multicast_join_**, limitato ai gruppi multicast nella rete primaria.

### <a name="multicast-group-leave"></a>Multicast Group Leave   
Le applicazioni che devono lasciare un gruppo multicast aggiunto in precedenza possono eseguire questa operazione chiamando ***il nx_igmp_multicast_leave*** servizio. Questo servizio riduce il conteggio interno associato al numero di volte in cui il gruppo è stato aggiunto. Se non sono presenti richieste di join in sospeso per un gruppo, viene chiamato il driver di rete per disabilitare l'ascolto dei pacchetti con l'indirizzo Ethernet di questo gruppo multicast.

### <a name="multicast-loopback"></a>Multicast Loopback    
Un'applicazione potrebbe voler ricevere traffico multicast proveniente da una delle origini nello stesso nodo. A tale scopo, è necessario che il componente multicast IP abbia abilitato il loopback usando il ***nx_igmp_loopback_enable***.

### <a name="igmp-report-message"></a>Messaggio del report IGMP      
Quando l'applicazione viene aggiunta a un gruppo multicast, viene inviato un messaggio di report IGMP tramite la rete per indicare l'intenzione dell'host di partecipare a un gruppo multicast specifico. Il formato del messaggio del report IGMP è illustrato nella figura 8. L'indirizzo del gruppo multicast viene utilizzato sia per il messaggio di gruppo nel messaggio di report IGMP che per l'indirizzo IP di destinazione.

Nella figura precedente (Figura 8) l'intestazione IGMP contiene un campo versione/tipo, risposta massima

![Diagramma di un messaggio di report IGMP.](./media/user-guide/image17.jpg)

**FIGURA 8. Messaggio del report IGMP**

time, un campo checksum e un campo di indirizzo del gruppo multicast. Per i messaggi IGMPv1, il campo Tempo di risposta massimo è sempre impostato su zero, perché non fa parte del protocollo IGMPv1. Il campo Tempo di risposta massimo viene impostato quando l'host riceve un messaggio IGMP di tipo query e viene cancellato quando un host riceve il messaggio di tipo Report di un altro host, come definito dal protocollo IGMPv2.

Di seguito viene descritto il formato di intestazione IGMP:

|Campo intestazione|Scopo|
|---|---|
|**Version** |Questo campo specifica la versione IGMP (bit 31- 28).|
|**Tipo** |Questo campo specifica il tipo di messaggio IGMP (bit 27 -24).|
|**Tempo di risposta massimo** |Non usato in IGMP v1. In IGMP v2 questo campo funge da tempo di risposta massimo.|
|**Checksum** |Questo campo contiene il checksum a 16 bit della somma complementare del messaggio IGMP a partire dalla versione IGMP (bit 0-15)|
|**Indirizzo gruppo** |Indirizzo IP del gruppo D di classe D a 32 bit|

I messaggi di report IGMP vengono inviati anche in risposta ai messaggi di query IGMP inviati da un router multicast. I router multicast inviano periodicamente messaggi di query per vedere quali host richiedono ancora l'appartenenza al gruppo. I messaggi di query hanno lo stesso formato del messaggio del report IGMP illustrato nella figura 8. Le uniche differenze sono il tipo IGMP è uguale a 1 e il campo dell'indirizzo del gruppo è impostato su 0. I messaggi di query IGMP vengono inviati *all'indirizzo* IP di tutti gli host dal router multicast. Un host che vuole comunque mantenere l'appartenenza al gruppo risponde inviando un altro messaggio di report IGMP.

> [!NOTE]
> *È previsto che tutti i messaggi nell'implementazione TCP/IP siano in **big endian** formato. In questo formato, il byte più significativo della parola risiede all'indirizzo di byte più basso.*

### <a name="igmp-statistics-and-errors"></a>Statistiche ed errori IGMP    
<th><p>Se abilitato, il software IGMP di NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per l'elaborazione IGMP di ogni IP: 

- Totale report IGMP inviati 
- Totale query IGMP ricevute 
- Totale errori di checksum IGMP 
- Totale gruppi correnti IGMP aggiunti 

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con ***il nx_igmp_info_get*** servizio. 

### <a name="multicast-without-igmp"></a>Multicast senza IGMP  
L'applicazione che prevede il traffico multicast IPv4 può essere aggiunta a un indirizzo di gruppo multicast senza richiamare i messaggi IGMP usando il nx_ipv4_multicast_interface_join ***.*** Questo servizio indica al livello IPv4 e al driver di interfaccia sottostante di accettare pacchetti dall'indirizzo multicast IPv4 designato. Non sono tuttavia presenti messaggi di gestione del gruppo IGMP inviati o elaborati per questo gruppo.

L'applicazione non vuole più ricevere traffico dal gruppo può usare il servizio ***nx_ipv4_multicast_interface_leave.***

## <a name="ipv6-in-netx-duo"></a>IPv6 in NetX Duo

### <a name="ipv6-addresses"></a>Indirizzi IPv6   
Gli indirizzi IPv6 sono a 128 bit. L'architettura dell'indirizzo IPv6 è descritta in RFC 4291. L'indirizzo è suddiviso in un prefisso contenente i bit più significativi e in un indirizzo host contenente i bit inferiori. Il prefisso indica il tipo di indirizzo ed è approssimativamente equivalente all'indirizzo di rete nella rete IPv4.

IPv6 ha tre tipi di specifiche di indirizzo: unicast, anycast (non supportato in NetX Duo) e multicast. Gli indirizzi unicast sono gli indirizzi IP che identificano un host specifico su Internet. Gli indirizzi unicast possono essere un indirizzo IP di origine o di destinazione. Gli indirizzi multicast specificano un gruppo dinamico di host su Internet. I membri del gruppo multicast possono partecipare e uscire ogni volta che lo desiderano.

IPv6 non ha l'equivalente del meccanismo di trasmissione IPv4. La possibilità di inviare un pacchetto a tutti gli host può essere ottenuta inviando un pacchetto al gruppo multicast link-local all hosts.

IPv6 usa indirizzi multicast per eseguire le procedure di individuazione router adiacente, individuazione router e configurazione automatica degli indirizzi senza stato.

Esistono due tipi di indirizzi unicast IPv6: indirizzi locali di collegamento, in genere costruiti combinando il prefisso locale del collegamento noto con l'indirizzo MAC dell'interfaccia e indirizzi IP globali, che include anche la parte relativa al prefisso e l'ID host. Un indirizzo globale può essere configurato manualmente o tramite la configurazione automatica degli indirizzi senza stato o DHCPv6. NetX Duo supporta sia l'indirizzo locale del collegamento che l'indirizzo globale.

Per supportare sia i formati IPv4 che IPv6, NetX Duo offre un nuovo tipo di dati, NXD_ADDRESS, per contenere gli indirizzi IPv4 e IPv6. La definizione di questa struttura è illustrata di seguito. Il campo address è un'unione di indirizzi IPv4 e IPv6.

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

Nella struttura NXD_ADDRESS, il primo elemento, *nxd_ip_version*, indica la versione IPv4 o IPv6. I valori supportati sono NX_IP_VERSION_V4 o NX_IP_VERSION_V6. *nxd_ip_version* indica quale campo nell'unione nxd_ip_address *da* usare come indirizzo IP. I servizi API NetX Duo in genere accettano un puntatore NXD_ADDRESS struttura come argomento di input al posto dell'indirizzo IP ULONG (32 bit).

### <a name="link-local-addresses"></a>Collegare indirizzi locali     
Un indirizzo locale di collegamento è valido solo nella rete locale. Un dispositivo può inviare e ricevere pacchetti a un altro dispositivo nella stessa rete dopo l'assegnazione di un indirizzo locale di collegamento valido. Un'applicazione assegna un indirizzo locale di collegamento chiamando il servizio NetX Duo ***nxd_ipv6_address_set***, con il parametro prefix length impostato su 10. L'applicazione può fornire un indirizzo locale di collegamento al servizio oppure usare semplicemente NX_NULL come indirizzo locale del collegamento e consentire a NetX Duo di costruire un indirizzo locale del collegamento in base all'indirizzo MAC del dispositivo.

L'esempio seguente indica a NetX Duo di configurare l'indirizzo locale del collegamento con una lunghezza di prefisso pari a 10 nel dispositivo primario (indice 0) usando il relativo indirizzo MAC:

```c
nxd_ipv6_address_set(ip_ptr, 0, NX_NULL, 10, NX_NULL);
```
Nell'esempio precedente, se l'indirizzo MAC dell'interfaccia è 54:32:10:1A:BC:67, l'indirizzo link-local corrispondente sarà:

```c
FE80::5632:10FF:FE1A:BC67
```
Si noti che la parte dell'ID host dell'indirizzo IPv6 (**5632:10FF:FE1A:BC67**) è costituito dall'indirizzo MAC a 6 byte, con le modifiche seguenti:

- **0xFFFE** inserito tra il byte 3 e il byte 4 dell'indirizzo MAC
- Il secondo bit più basso del primo byte dell'indirizzo MAC (bit U/L) è impostato su 1

Per altre informazioni su come costruire la parte host di un indirizzo IPv6 dall'indirizzo MAC dell'interfaccia, vedere RFC 2464 (Trasmissione di pacchetti IPv6 tramite rete Ethernet).

Esistono alcuni indirizzi multicast speciali per l'invio di messaggi multicast a uno o più host in IPv6:

| Group  | Indirizzo   | Descrizione  |
|---|---|---|
|Gruppo tutti i nodi |**FF02::1** |Tutti gli host nella rete locale|
|Gruppo tutti i router |**FF02::2** |Tutti i router nella rete locale|
|Nodo richiesto |**FF02::1:FF00:0/104** |Spiegato di seguito|

Un indirizzo multicast di nodo richiesto è destinato a host specifici nel collegamento locale anziché a tutti gli host IPv6. È costituito dal prefisso **FF02::1:FF00:0/104**, ovvero 104 bit e gli ultimi 24 bit dell'indirizzo IPv6 di destinazione. Ad esempio, un indirizzo IPv6 **205B:209D:D028::F058:D1C8:1024** ha un indirizzo multicast solicitednode con indirizzo **FF02::1:FFC8:1024**.

> [!IMPORTANT]
> *La notazione dei due punti indica che i bit interviene sono tutti zeri. **FF02::1:FF00:0/104*** completamente espanso è simile a **FF02:0000:0000:0000:0000:0001:FF00:0000**

### <a name="global-addresses"></a>Indirizzi globali    
Un esempio di indirizzo globale IPv6 **è 2001:0123:4567:89AB:CDEF::1** NetX Duo archivia gli indirizzi IPv6 nella struttura NXD_ADDRESS. Nell'esempio seguente la variabile NXD_ADDRESS contiene **global_ipv6_address** un indirizzo IPv6 unicast. L'esempio seguente illustra un dispositivo NetX Duo che crea un indirizzo globale IPv6 specifico per il dispositivo primario:

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
Si noti che il prefisso di questo indirizzo IPv6 è **2001:0123:4567:89AB**, che è lungo 64 bit ed è una lunghezza di prefisso comune per gli indirizzi IPv6 unicast globali su Ethernet.

La NXD_ADDRESS contiene anche indirizzi IPv4. Un indirizzo IP **192.1.168.10** (**0xC001A80A**) archiviato in global_ipv4_address avrebbe il layout di memoria seguente:

|Campo |Valore |
|---|---|
|global_ipv4_address.nxd_ip_version |NX_IP_VERSION_V4|
|global_ipv4_address.nxd_ip_address.v4 |0xC001A80A|

Quando un'applicazione passa un indirizzo ai  servizi NetX Duo, il campo nxd_ip_version deve specificare la versione IP corretta per la corretta gestione dei pacchetti.

Per essere compatibile con le versioni precedenti delle applicazioni NetX esistenti, NetX Duo supporta tutti i servizi NetX. Internamente, NetX Duo converte il tipo di indirizzo IPv4 ULONG in un tipo di dati NXD_ADDRESS prima di inoltrarlo al servizio NetX Duo effettivo.

L'esempio seguente illustra la somiglianza e le differenze tra i servizi in NetX e NetX Duo.

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

Di seguito è riportata l'API NetX equivalente:

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
> Gli sviluppatori di applicazioni sono invitati a usare la versione *nxd di queste API*.

### <a name="ipv6-default-routers"></a>Router predefiniti IPv6    
IPv6 usa un router predefinito per inoltrare i pacchetti alle destinazioni offlink. Il servizio NetX Duo ***nxd_ipv6_default_router_add*** a un'applicazione di aggiungere un router IPv6 alla tabella del router predefinita. Per altri servizi router predefiniti offerti da NetX Duo, vedere il capitolo 4 "Descrizione dei servizi".  

Quando si inoltrano pacchetti IPv6, NetX Duo verifica innanzitutto se la destinazione del pacchetto è in collegamento. In caso contrario, NetX Duo controlla la tabella di routing predefinita per un router valido a cui inoltrare il pacchetto off-link.  

Per rimuovere un router dalla tabella del router predefinito IPv6, l'applicazione deve usare il servizio ***nxd_ipv6_default_router_delete** _. Per ottenere le voci della tabella del router predefinito IPv6, usare il servizio _*_nxd_ipv6_default_router_entry_get_**.

### <a name="ipv6-header"></a>Intestazione IPv6    
L'intestazione IPv6 è stata modificata dall'intestazione IPv4. Quando si alloca un pacchetto, il chiamante specifica il protocollo dell'applicazione (ad esempio UDP, TCP), le dimensioni del buffer in byte e il limite hop.   

La figura 9 illustra il formato dell'intestazione IPv6 e la tabella elenca i componenti dell'intestazione.

![Diagramma del formato di intestazione IPv6.](./media/user-guide/image18.png)

**FIGURA 9. Formato intestazione IPv6**

|Intestazione IP | Scopo |
|---|---|
|Versione |Campo a 4 bit per la versione IP. Per le reti IPv6, il valore in questo campo deve essere 6. Per le reti IPv4 deve essere 4.|
|Classe di traffico |Campo a 8 bit che archivia le informazioni sulla classe di traffico. Questo campo non viene usato da NetX Duo.|
|Flow Etichetta |Campo a 20 bit per identificare in modo univoco il flusso, se presente, a cui è associato un pacchetto. Il valore zero indica che il pacchetto non appartiene a un flusso specifico. Questo campo sostituisce il *campo TOS* in IPv4.|
|Lunghezza del payload |Campo a 16 bit che indica la quantità di dati in byte del pacchetto IPv6 che segue l'intestazione di base IPv6. Sono inclusi tutti i dati e l'intestazione del protocollo incapsulati.|
|Intestazione successiva | Campo a 8 bit che indica il tipo di intestazione dell'estensione che segue l'intestazione di base IPv6. Questo campo sostituisce il *campo Protocollo* in IPv4.|
|Limite hop |Campo a 8 bit che limita il numero di router che il pacchetto può passare. Questo campo sostituisce il *campo TTL* in IPv4.|
|Indirizzo di origine |Campo a 128 bit che archivia l'indirizzo IPv6 del mittente.|
|Indirizzo di destinazione |Campo a 128 bit che sona l'indirizzo IPv6 della destinazione.|

### <a name="enabling-ipv6-in-netx-duo"></a>Abilitazione di IPv6 in NetX Duo    
Per impostazione predefinita, IPv6 è abilitato in NetX Duo. I servizi IPv6 sono abilitati in NetX Duo se l'opzione configurabile ***NX_DISABLE_IPV6** _ in _nx_user.h* non è definita. Se ***NX_DISABLE_IPV6*** è definito, NetX Duo offrirà solo servizi IPv4 e tutti i moduli e i servizi correlati a IPv6 non sono incorporati nella libreria NetX Duo.

Il servizio seguente viene fornito per le applicazioni per configurare l'indirizzo IPv6 del dispositivo: ***nxd_ipv6_address_set***

Oltre a impostare manualmente gli indirizzi IPv6 del dispositivo, il sistema può anche usare la configurazione automatica degli indirizzi senza stato. Per usare questa opzione, l'applicazione deve chiamare ***nxd_ipv6_enable** _ per avviare i servizi IPv6 nel dispositivo. Inoltre, i servizi ICMPv6 devono essere avviati chiamando nxd_icmp_enable , che consente _*_a_*_ NetX Duo di eseguire servizi come Router Solicitation, Neighbor Discovery e Duplicate Address Detection. Si noti _*_nx_icmp_enable_*_ avvia solo ICMP per i servizi IPv4. _*_nxd_icmp_enable_*_ avvia i servizi ICMP per IPv4 e IPv6. Se il sistema non richiede servizi ICMPv6, è possibile usare _ *_nx_icmp_enable_** in modo che il modulo ICMPv6 non sia collegato al sistema.

L'esempio seguente illustra una tipica procedura di inizializzazione IPv6 di NetX Duo.

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

I protocolli di livello superiore, ad esempio TCP e UDP, possono essere abilitati prima o dopo l'avvio di IPv6.

> [!IMPORTANT]  
> *I servizi IPv6 sono disponibili solo dopo che il thread IP è stato inizializzato e il dispositivo è abilitato.*

Dopo aver abilitato l'interfaccia (ad esempio, il driver di dispositivo dell'interfaccia è pronto per inviare e ricevere dati ed è stato ottenuto un indirizzo locale di collegamento valido), il dispositivo può ottenere indirizzi IPv6 globali con uno dei metodi seguenti:

- Configurazione automatica degli indirizzi senza stato;  
- Configurazione manuale degli indirizzi IPv6;  
- Configurazione degli indirizzi tramite DHCPv6 (con pacchetto DHCPv6 facoltativo)

I primi due metodi sono descritti di seguito. Il terzo metodo (DHCPv6) è descritto nel pacchetto DHCP.

### <a name="stateless-address-autoconfiguration-using-router-solicitation"></a>Configurazione automatica degli indirizzi senza stato tramite richiesta router      
I dispositivi NetX Duo possono configurare automaticamente le interfacce quando sono connessi a una rete IPv6 con un router che fornisce informazioni sul prefisso. I dispositivi che richiedono la configurazione automatica degli indirizzi senza stato inviano messaggi RS (Router Solicitation). I router nella rete rispondono con messaggi di annuncio router richiesto. I messaggi RA annunciano prefissi che identificano gli indirizzi di rete associati a un collegamento. I dispositivi generano quindi un identificatore univoco per la rete a cui è collegato il dispositivo. L'indirizzo viene formato combinando il prefisso e il relativo identificatore univoco. In questo modo, alla ricezione dei messaggi ra, gli host generano il proprio indirizzo IP. I router possono anche inviare messaggi ra periodici non richieste. 

> [!WARNING]
> *NetX Duo consente a un'applicazione di abilitare o disabilitare la configurazione automatica degli indirizzi senza stato in fase di esecuzione. Per abilitare questa funzionalità, la libreria NetX Duo deve essere compilata **NX_IPV6_STATELESS_AUTOCONFIG_CONTROL** definita. Dopo aver abilitato questa funzionalità, le  applicazioni* possono usare nxd_ipv6_stateless_address_autoconfigure_enable e nxd_ipv6_stateless_address_autocofigure_disable per abilitare o disabilitare la configurazione automatica degli indirizzi senza stato IPv6.

### <a name="manual-ipv6-address-configuration"></a>Configurazione manuale degli indirizzi IPv6     
Se è necessario un indirizzo IPv6 specifico, l'applicazione può usare nxd_ipv6_address_set ***per*** configurare manualmente un indirizzo IPv6. Un'interfaccia di rete può avere più indirizzi IPv6. Tenere tuttavia presente che il numero totale di indirizzi IPv6 in un sistema, ottenuto tramite la configurazione automatica degli indirizzi senza stato o tramite la configurazione manuale, non può superare ***NX_MAX_IPV6_ADDRESSES***.

L'esempio seguente illustra come configurare manualmente un indirizzo globale nell'interfaccia primaria (dispositivo 0) in ip_0:

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

### <a name="duplicate-address-detection-dad"></a>Rilevamento di indirizzi duplicati (LIVELLO)    
Dopo che un sistema ha configurato il proprio indirizzo IPv6, l'indirizzo viene contrassegnato come *TENTATIVE.* Se è abilitato il rilevamento di indirizzi duplicati (DUPLICATE Address Detection), descritto in RFC 4862, NetX Duo invia automaticamente i messaggi neighbor solicitation (NS) con questo indirizzo provvisorio come destinazione. Se nessun host nella rete risponde a questi messaggi NS entro un determinato periodo di tempo, si presuppone che l'indirizzo sia univoco nel collegamento locale e il relativo stato transiti allo stato VALID. A questo punto l'applicazione può iniziare a usare questo indirizzo IP per la comunicazione.  

La funzionalità PIÙ COMPLETA fa parte del modulo ICMPv6. Pertanto, l'applicazione deve abilitare i servizi ICMPv6 prima che un nuovo indirizzo configurato possa passare attraverso il processo DELLA RIGA DI COMANDO. In alternativa, è possibile disattivare il processo DISE definendo l'opzione ***NX_DISABLE_IPV6_DAD** _ nell'ambiente di compilazione della libreria NetX Duo (definito _*_come nx_user.h)._*_ Durante il processo DI BILANCIAMENTO del carico, il parametro _*_NX_IPV6_DAD_TRANSMITS_*_ determina il numero di messaggi NS inviati da NetX Duo senza ricevere una risposta per determinare che l'indirizzo è univoco. Per impostazione predefinita e consigliata da RFC 4862, _ *_NX_IPV6_DAD_TRANSMITS_** è impostato su 3. L'impostazione di questo simbolo su zero disabilita in modo efficace LA FUNZIONE DI ACCESSO.

Se ICMPv6 o LA NOTAZIONE NON è abilitata quando l'applicazione assegna un indirizzo IPv6, l'operazione NON VIENE eseguita e NetX Duo imposta immediatamente lo stato dell'indirizzo IPv6 su VALID.

NetX Duo non può comunicare nella rete IPv6 finché il collegamento non è valido e/o l'indirizzo globale. Dopo aver ottenuto un indirizzo valido, NetX Duo tenta di trovare una corrispondenza tra l'indirizzo di destinazione di un pacchetto in ingresso e uno degli indirizzi IPv6 configurati o un indirizzo multicast abilitato. Se non viene trovata alcuna corrispondenza, il pacchetto viene eliminato. 

> [!WARNING]  
> *Durante il processo DELL'utente, il numero di pacchetti NS DI CUI trasmettere è definito da ***NX_IPV6_DAD_TRANSMITS**, che per impostazione predefinita è 3 e per impostazione predefinita si verifica un ritardo di un secondo tra l'invio di ogni messaggio _NS DI TIPO NS. Pertanto, in_ un sistema in cui è abilitata l'opzione LARTE, dopo l'assegnazione di un indirizzo IPv6 (e presupponendo che non si tratta di un indirizzo duplicato), si verifica un ritardo di circa 3 secondi prima che l'indirizzo IP sia in uno stato VALIDO e sia pronto per la comunicazione.

Le applicazioni potrebbero voler ricevere notifiche quando gli indirizzi IPv6 nel sistema vengono modificati. Per abilitare la funzionalità di notifica della modifica dell'indirizzo IPv6, la libreria NetX Duo deve essere compilata con il simbolo **NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY** definito. Dopo aver abilitato la funzionalità, le applicazioni possono installare la funzione di callback usando il **_nxd_ipv6_address_change_notify_** servizio.

Quando un indirizzo IPv6 viene modificato o diventa non valido, la funzione di callback fornita dall'utente viene richiamata con le informazioni seguenti:

| Funzione  | Descrizione  |
|---|---|
|ip_ptr |Puntatore all'istanza IP|
|interface_index |Indice dell'interfaccia di rete a cui è associato questo indirizzo IPv6
|ipv6_addr_index |Indice della tabella degli indirizzi IPv6|
|ipv6_address |Puntatore all'indirizzo IPv6, sotto forma di matrice di quattro interi ULONG. Gli indirizzi Pv6 vengono presentati nell'ordine dei byte dell'host.|

### <a name="ipv6-multicast-support-in-netx-duo"></a>Supporto multicast IPv6 in NetX Duo      
Gli indirizzi multicast specificano un gruppo dinamico di host su Internet. I membri del gruppo multicast possono partecipare e uscire ogni volta che desiderano. NetX Duo implementa diversi protocolli ICMPv6, tra cui il rilevamento di indirizzi duplicati, l'individuazione router adiacenti e l'individuazione router, che richiedono funzionalità multicast IP. Pertanto, NetX Duo prevede che il driver di dispositivo sottostante supporti le operazioni multicast.

Quando NetX Duo deve partecipare o uscire da un gruppo multicast,ad esempio l'indirizzo multicast a tutti i nodi e l'indirizzo *multicast* del nodo richiesto, esegue un comando del driver al driver di dispositivo per aggiungere o lasciare un indirizzo MAC multicast. Il comando del driver per l'unione dell'indirizzo multicast è ***NX_LINK_MULTICAST_JOIN** _. Per lasciare un indirizzo multicast, NetX Duo emittente il comando del driver _*_NX_LINK_MULTICAST_LEAVE_**. Il driver di dispositivo deve implementare questi due comandi per il corretto funzionamento dei protocolli ICMPv6.

Le applicazioni possono aggiungersi a un gruppo multicast IPv6 usando il servizio ***nxd_ipv6_multicast_interface_join*.** Questo servizio registra l'indirizzo multicast con lo stack IP e quindi invia una notifica al driver di dispositivo specificato dell'indirizzo multicast IPv6. Per lasciare un gruppo multicast, le applicazioni usano il servizio ***nxd_ipv6_multicast_interface_leave.***

### <a name="neighbor-discovery-nd"></a>Individuazione router adiacenti (ND)    
Individuazione router adiacenti è un protocollo nelle reti IPv6 per il mapping di indirizzi fisici agli indirizzi IPv6 (indirizzo globale o indirizzo locale del collegamento). Questo mapping viene mantenuto nella cache di individuazione router adiacenti (cache ND). Il processo ND è l'equivalente del processo ARP in IPv4 e la cache ND è simile alla tabella ARP. Un nodo IPv6 può ottenere l'indirizzo MAC del router adiacente usando il protocollo ND (Neighbor Discovery). Invia un messaggio NS (Neighbor Solicitation) all'indirizzo multicast del nodo richiesto da tutti i nodi e attende un messaggio di annuncio adiacente corrispondente. L'indirizzo MAC ottenuto tramite questo processo viene archiviato nella cache ND.

Ogni istanza IP ha una cache ND. La cache ND viene gestita come matrice di voci. Le dimensioni della matrice vengono definite in fase di compilazione impostando **l'opzione*** NX_IPV6_NEIGHBOR_CACHE_SIZE _ che in _*_nx_user.h_**. Si noti che tutte le interfacce collegate a un'istanza IP condividono la stessa cache ND.

L'intera cache ND è vuota all'avvio di NetX Duo. Durante l'esecuzione del sistema, NetX Duo aggiorna automaticamente la cache ND, aggiungendo ed eliminando le voci in base al protocollo ND. Tuttavia, un'applicazione può anche aggiornare la cache ND aggiungendo ed eliminando manualmente le voci della cache usando i servizi NetX Duo seguenti:

- ***nxd_nd_cache_entry_delete***  
- ***nxd_nd_cache_entry_set***   
- ***nxd_nd_cache_invalidate***

Quando si inviano e ricevono pacchetti IPv6, NetX Duo aggiorna automaticamente la tabella della cache ND.

## <a name="internet-control-message-protocol-in-ipv6-icmpv6"></a>Internet Control Message Protocol in IPv6 (ICMPv6)  

Il ruolo di ICMPv6 in IPv6 è stato notevolmente ampliato per supportare il mapping degli indirizzi IPv6 e l'individuazione router. Inoltre, NetX Duo ICMPv6 supporta la richiesta e la risposta echo, le segnalazioni degli errori ICMPv6 e i messaggi di reindirizzamento ICMPv6.

### <a name="icmpv6-enable"></a>Abilitazione di ICMPv6    
Prima che i messaggi ICMPv6 possano essere elaborati da NetX Duo, l'applicazione deve chiamare il ***servizio nxd_icmp_enable*** per abilitare l'elaborazione ICMPv6, come illustrato in precedenza. 

### <a name="icmpv6-messages"></a>Messaggi ICMPv6     
La struttura dell'intestazione ICMPv6 è simile alla struttura di intestazione ICMPv4. Come illustrato di seguito, l'intestazione ICMPv6 di base contiene i tre campi, tipo, codice e checksum, oltre alla lunghezza variabile dei dati dell'opzione ICMPv6. 

![Diagramma di un'intestazione ICMPv6 di base.](./media/user-guide/image19.png)

**FIGURA 10. Intestazione ICMPv6 di base**

|Campo |Dimensioni (byte) |Descrizione |
|-----|-----|-----|
|     | 1   |Identifica il tipo di messaggio ICMPv6. |
|     |     |1 Destinazione non raggiungibile |
|     |     |2 Pacchetto troppo grande |
|     |     |3 Tempo superato |
|     |     |4 Problema di parametro |
|     |     |128 Richiesta Echo |
|     |     |129 Echo Reply |
|     |     |133 Router Solicitation |
|     |     |Annuncio router 134 |
|     |     |135 Neighbor Solicitation |
|     |     |136 Annuncio adiacente |
|     |     |137 Messaggio di reindirizzamento |
|Codice | 1   |Qualifica ulteriormente il tipo di messaggio ICMPv6. Usato in genere con messaggi di errore. Se non viene usato, viene impostato su zero. I messaggi echo request/reply e NS non lo usano.|
|Checksum | 2 |Campo checksum a 16 bit per l'intestazione ICMP. Si tratta di un complemento a 16 bit dell'intero messaggio ICMPv6, inclusa l'intestazione ICMPv6. Include anche una pseudo-intestazione dell'indirizzo di origine IPv6, dell'indirizzo di destinazione e della lunghezza del payload del pacchetto. |

Di seguito è riportata un'intestazione Neighbor Solicitation di esempio.

![Diagramma di un esempio di intestazione Neighbor Solicitation.](./media/user-guide/image20.jpg)

**FIGURA 11. Intestazione ICMPv6 per un messaggio di richiesta adiacente**

|Campo |Dimensioni (byte) |Descrizione |
|-----|-----|-----|
|Type | 1   |Identifica il tipo di messaggio ICMPv6 per i messaggi di richiesta adiacenti. Il valore è 135. |
|Codice | 1   |Non usato. Impostare su 0. |
|Checksum | 2  |Campo checksum a 16 bit per l'intestazione ICMPv6. |
|Riservato | 4  |4 byte riservati impostati su 0. |
|Indirizzo di destinazione | 16  |Indirizzo IPv6 della destinazione della richiesta. Per la risoluzione degli indirizzi IPv6, si tratta dell'indirizzo IP unicast effettivo del dispositivo il cui indirizzo del livello di collegamento deve essere risolto. |
|Opzioni | Variabile |Informazioni facoltative specificate dal protocollo di individuazione adiacente. |

### <a name="icmpv6-ping-request"></a>Richiesta ping ICMPv6
Nelle applicazioni NetX Duo ***nxd_icmp_ping*** per inviare richieste ping IPv6 o IPv4, in base all'indirizzo IP di destinazione specificato nei parametri.  

### <a name="icmpv6-ping-response"></a>Risposta ping ICMPv6
Una risposta ping ICMPv6 è un altro tipo di messaggio ICMPv6 generato internamente dal componente ICMPv6 in risposta a una richiesta ping ICMPv6 esterna. Oltre all'acknowledgement, la risposta ping ICMPv6 contiene anche una copia dei dati utente forniti nella richiesta ping ICMPv6.  

### <a name="thread-suspension"></a>Sospensione dei thread
I thread dell'applicazione possono essere sospesi durante il tentativo di eseguire il ping di un altro membro di rete. Dopo aver ricevuto una risposta ping, il messaggio di risposta ping viene assegnato al primo thread sospeso e tale thread viene ripreso. Come tutti i servizi NetX Duo, la sospensione in una richiesta ping ha un timeout facoltativo.  

### <a name="other-icmpv6-messages"></a>Altri messaggi ICMPv6
I messaggi ICMPv6 sono necessari per le funzionalità seguenti:  

- Individuazione router adiacenti  
- Configurazione automatica degli indirizzi senza stato 
- Individuazione router 
- Rilevamento dell'irraggiungibilità adiacente  

### <a name="neighbor-unreachability-router-and-prefix-discovery"></a>Individuazione di router e prefissi adiacenti non raggiungibili    
Il rilevamento dell'irraggiungibilità dei router adiacenti, l'individuazione router e l'individuazione dei prefissi sono basati sul protocollo Neighbor Discovery e sono descritti di seguito. 

***Rilevamento dell'irraggiungibilità adiacente:*** Un dispositivo IPv6 cerca nella cache ND (Neighbor Discovery) l'indirizzo del livello di collegamento di destinazione quando vuole inviare un pacchetto. La destinazione immediata, a volte definita "hop successivo", può essere la destinazione effettiva nello stesso collegamento oppure può essere un router se la destinazione non è collegata. Una voce della cache ND contiene lo stato sulla raggiungibilità di un vicino.

Uno stato REACHABLE indica che l'adiacente è considerato raggiungibile. Un router adiacente è raggiungibile se ha ricevuto di recente la conferma che sono stati ricevuti i pacchetti inviati al router adiacente. La conferma in NetX Duo ha la forma di ricevere un messaggio NA dal vicino in risposta a un messaggio NS inviato dal dispositivo NetX Duo. NetX Duo cambierà anche lo stato dello stato adiacente in REACHABLE se l'applicazione chiama il servizio NetX Duo ***nxd_nd_cache_entry_set*** per immettere manualmente un record della cache.

***Individuazione router:*** Un dispositivo IPv6 usa un router per inoltrare tutti i pacchetti destinati a destinazioni fuori collegamento. Può anche usare le informazioni inviate dal router, ad esempio messaggi di annuncio router (RA), per configurare i relativi indirizzi IPv6 globali.

Un dispositivo nella rete può avviare il processo di individuazione router inviando un messaggio di richiesta router (RS) all'indirizzo multicast all-router (FF01::2). Oppure può attendere l'indirizzo multicast all-node (FF::1) per un'ra periodica dai router.

Un messaggio RA contiene le informazioni sul prefisso per la configurazione di un indirizzo IPv6 per la rete. In NetX Duo la richiesta router è abilitata per impostazione predefinita e può essere disabilitata impostando l'opzione di configurazione ***NX_DISABLE_ICMPV6_ROUTER_SOLICITATION** _ in _*_nx_user.h_**. Per altri dettagli sull'impostazione dei parametri di richiesta router, vedere Opzioni di configurazione nel capitolo "Installazione e uso di NetX Duo". 

***Individuazione del prefisso:*** un dispositivo IPv6 usa l'individuazione dei prefissi per scoprire quali host di destinazione sono accessibili direttamente senza passare attraverso un router. Queste informazioni vengono rese disponibili per il dispositivo IPv6 dai messaggi ra dal router. Il dispositivo IPv6 archivia le informazioni sul prefisso in una tabella di prefisso. L'individuazione del prefisso corrisponde a un prefisso dalla tabella del prefisso del dispositivo IPv6 a un indirizzo di destinazione. Un prefisso corrisponde a un indirizzo di destinazione se tutti i bit nel prefisso corrispondono ai bit più significativi dell'indirizzo di destinazione. Se più di un prefisso copre un indirizzo, viene selezionato il prefisso più lungo.

### <a name="icmpv6-error-messages"></a>Messaggi di errore ICMPv6    
In NetX Duo sono supportati i messaggi di errore ICMPv6 seguenti:  

- Destinazione non raggiungibile  
- Pacchetto troppo grande  
- Superamento del tempo  
- Problema dei parametri  

## <a name="user-datagram-protocol-udp"></a>Udp (User Datagram Protocol)

Il protocollo UDP (User Datagram Protocol) fornisce la forma più semplice di trasferimento dei dati tra i membri di rete (RFC 768). I pacchetti di dati UDP vengono inviati da un membro di rete a un altro in modo ottimale; Ad esempio, non esiste un meccanismo predefinito per l'acknowledgement da parte del destinatario del pacchetto. Inoltre, l'invio di un pacchetto UDP non richiede che sia stabilita alcuna connessione in anticipo. Per questo, la trasmissione di pacchetti UDP è molto efficiente.

Per gli sviluppatori che migrano le applicazioni NetX a NetX Duo, esistono solo alcune modifiche di base nella funzionalità UDP tra NetX e NetX Duo. Questo perché IPv6 riguarda principalmente il livello IP sottostante. Tutti i servizi UDP di NetX Duo possono essere usati per la connettività IPv4 o IPv6.

### <a name="udp-header"></a>Intestazione UDP       
UDP inserisce una semplice intestazione di pacchetto davanti ai dati dell'applicazione durante la trasmissione e rimuove un'intestazione UDP simile dal pacchetto alla ricezione prima di recapitare un pacchetto UDP ricevuto all'applicazione. UDP usa il protocollo IP per l'invio e la ricezione di pacchetti, il che significa che è presente un'intestazione IP davanti all'intestazione UDP quando il pacchetto è in rete. La figura 12 mostra il formato dell'intestazione UDP.

![Diagramma del formato dell'intestazione UDP.](./media/user-guide/image21.png)

### <a name="figure-12-udp-header"></a>FIGURA 12. Intestazione UDP

> [!NOTE]
> *È previsto che tutte le intestazioni nell'implementazione UDP/IP siano in **big endian** formato. In questo formato, il byte più significativo della parola si trova all'indirizzo di byte più basso.*

Di seguito viene descritto il formato dell'intestazione UDP:

|Campo intestazione |Scopo |
|---|---|
|**Numero di porta di origine a 16 bit** |Questo campo contiene la porta da cui viene inviato il pacchetto UDP. Le porte UDP valide sono da 1 a 0xFFFF. |
|**Numero di porta di destinazione a 16 bit** |Questo campo contiene la porta UDP a cui viene inviato il pacchetto. Le porte UDP valide sono da 1 a 0xFFFF. |
|**Lunghezza UDP a 16 bit** |Questo campo contiene il numero di byte nel pacchetto UDP, incluse le dimensioni dell'intestazione UDP. |
|**Checksum UDP a 16 bit** |Questo campo contiene il checksum a 16 bit per il pacchetto, tra cui l'intestazione UDP, l'area dati del pacchetto e la pseudo intestazione IP. |

### <a name="udp-enable"></a>Abilitazione UDP   
Prima che sia possibile la trasmissione di pacchetti UDP, l'applicazione deve prima abilitare UDP chiamando il ***nx_udp_enable*** servizio. Dopo aver abilitato, l'applicazione è libera di inviare e ricevere pacchetti UDP.  

### <a name="udp-socket-create"></a>Creazione di socket UDP    
I socket UDP vengono creati durante l'inizializzazione o durante il runtime dai thread dell'applicazione. Il tipo iniziale di servizio, il tempo di vita e la profondità della coda di ricezione sono definiti dal ***nx_udp_socket_create*** servizio. Non sono previsti limiti al numero di socket UDP in un'applicazione.

### <a name="udp-checksum"></a>UDP Checksum   
Il protocollo IPv6 richiede un calcolo del checksum dell'intestazione UDP sui dati del pacchetto, mentre nel protocollo IPv4 è facoltativo.  

UDP specifica un checksum a 16 bit complementare che copre la pseudo intestazione IP (costituita dall'indirizzo IP di origine, dall'indirizzo IP di destinazione e dalla parola IP protocollo/lunghezza), dall'intestazione UDP e dai dati del pacchetto UDP. Le uniche differenze tra i checksum di intestazione del pacchetto UDP IPv4 e IPv6 sono che gli indirizzi IP di origine e di destinazione sono a 32 bit in IPv4 mentre in IPv6 sono a 128 bit. Se il checksum UDP calcolato è 0, viene archiviato come tutti quelli (0xFFFF). Se nel socket di invio la logica di checksum UDP è disabilitata, viene inserito uno zero nel campo checksum UDP per indicare che il checksum non è stato calcolato.

Se il checksum UDP non corrisponde al checksum calcolato dal ricevitore, il pacchetto UDP viene semplicemente eliminato.

Nella rete IPv4 il checksum UDP è facoltativo. NetX Duo consente a un'applicazione di abilitare o disabilitare il calcolo del checksum UDP per ogni socket. Per impostazione predefinita, la logica di checksum del socket UDP è abilitata. L'applicazione può disabilitare la logica di checksum per un socket UDP specifico chiamando il metodo ***nx_udp_socket_checksum_disable** _service. Nella rete IPv6, tuttavia, il checksum UDP è obbligatorio. Pertanto, il servizio _ *_nx_udp_socket_checksum_disable_** non disabilita la logica di checksum UDP quando si invia un pacchetto tramite la rete IPv6.

Alcuni controller Ethernet sono in grado di generare il checksum UDP in tempo reale. Se il sistema è in grado di usare la funzionalità di calcolo del checksum hardware, la libreria NetX Duo può essere compilata senza la logica di checksum. Per disabilitare il checksum software UDP, la libreria NetX Duo deve essere compilata con i simboli seguenti definiti: ***NX_DISABLE_UDP_TX_CHECKSUM** _ _*_e NX_DISABLE_UDP_RX_CHECKSUM_*_ (descritto nel capitolo 2). Le opzioni di configurazione rimuovono completamente la logica di checksum UDP da NetX Duo, mentre la chiamata al servizio _ *_nx_udp_socket_checksum_disable_** consente all'applicazione di disabilitare l'elaborazione del checksum UDP IPv4 per ogni socket.

### <a name="udp-ports-and-binding"></a>Porte UDP e binding      
Una porta UDP è un punto finale logico nel protocollo UDP. Nel componente UDP di NetX Duo sono presenti 65.535 porte valide, comprese tra 1 e 0xFFFF. Per inviare o ricevere dati UDP, l'applicazione deve prima creare un socket UDP e quindi associarlo a una porta desiderata. Dopo l'associazione di un socket UDP a una porta, l'applicazione può inviare e ricevere dati su tale socket.

### <a name="udp-fast-pathtrade"></a>Percorso rapido UDP&trade;   
Il percorso rapido UDP è il nome di un percorso a basso &trade; sovraccarico di pacchetti tramite l'implementazione UDP di NetX Duo. L'invio di un pacchetto UDP richiede solo alcune chiamate di funzione: ***nx_udp_socket_send** _, _*_nx_ip_packet_send_*_ e la chiamata finale al driver di rete. _*_nx_udp_socket_send_*_ è disponibile in NetX Duo per le applicazioni NetX esistenti ed è applicabile solo per i pacchetti IPv4. Il metodo preferito, tuttavia, è usare il servizio _ *_nxd_udp_socket_send_** illustrato di seguito. Alla ricezione di pacchetti UDP, il pacchetto UDP viene inserito nella coda di ricezione socket UDP appropriata o recapitato a un thread dell'applicazione sospeso in una singola chiamata di funzione dall'elaborazione dell'interrupt di ricezione del driver di rete. Questa logica altamente ottimizzata per l'invio e la ricezione di pacchetti UDP è l'essenziale della tecnologia UDP Fast Path.  

### <a name="udp-packet-send"></a>Invio di pacchetti UDP    
L'invio di dati UDP su reti IPv6 o IPv4 è facile chiamando la funzione ***nxd_udp_socket_send** _. Il chiamante deve impostare la versione IP nel campo _nx_ip_version* del parametro NXD_ADDRESS puntatore. NetX Duo determinerà l'indirizzo di origine migliore per i pacchetti UDP trasmessi in base all'indirizzo IPv4/IPv6 di destinazione. Questo servizio inserisce un'intestazione UDP davanti ai dati del pacchetto e la invia alla rete usando una routine di invio IP interno. Non esiste alcuna sospensione del thread per l'invio di pacchetti UDP perché tutte le trasmissioni di pacchetti UDP vengono elaborate immediatamente. 

Per le destinazioni multicast o broadcast, l'applicazione deve specificare l'indirizzo IP di origine da usare se il dispositivo NetX Duo ha più indirizzi IP tra cui scegliere. Questa operazione può essere eseguita con i servizi ***nxd_udp_socket_source_send.***

> [!IMPORTANT]    
> *Se **nx_udp_socket_send** viene usato per* la trasmissione di pacchetti multicast o broadcast, l'indirizzo IP della prima interfaccia abilitata viene usato come indirizzo di origine .

> [!NOTE] 
> Se per questo socket è abilitata la logica di *checksum UDP,* l'operazione di checksum viene eseguita nel contesto del thread chiamante, senza bloccare l'accesso alle strutture di dati UDP o IP. 

> [!WARNING]    
> *I dati del payload UDP che risiedono nella struttura NX_PACKET devono trovarsi su un limite di parola lunga. L'applicazione deve lasciare spazio sufficiente* tra il puntatore anteposto e il puntatore di avvio dei dati per NetX Duo per posizionare le intestazioni udp, IP e fisiche dei supporti .

### <a name="udp-packet-receive"></a>Ricezione pacchetti UDP    
I thread dell'applicazione possono ricevere pacchetti UDP da un socket specifico ***chiamando nx_udp_socket_receive***. La funzione di ricezione socket recapita il pacchetto meno recente nella coda di ricezione del socket. Se non sono presenti pacchetti nella coda di ricezione, il thread chiamante può sospendere (con un timeout facoltativo) fino all'arrivo di un pacchetto.

L'elaborazione del pacchetto di ricezione UDP (in genere chiamata dal gestore di interrupt di ricezione del driver di rete) è responsabile dell'inserimento del pacchetto nella coda di ricezione del socket UDP o del recapito al primo thread sospeso in attesa di un pacchetto. Se il pacchetto viene accodato, l'elaborazione di ricezione controlla anche la profondità massima della coda di ricezione associata al socket. Se il pacchetto appena accodato supera la profondità della coda, il pacchetto meno recente nella coda viene eliminato.

### <a name="udp-receive-notify"></a>Notifica di ricezione UDP   
Se il thread dell'applicazione deve elaborare i dati ricevuti da più socket, ***nx_udp_socket_receive_notify*** usare la funzione . Questa funzione registra una funzione di callback del pacchetto di ricezione per il socket. Ogni volta che viene ricevuto un pacchetto nel socket, viene eseguita la funzione di callback.

Il contenuto della funzione di callback è specifico dell'applicazione; Tuttavia, probabilmente conterrà la logica per informare il thread di elaborazione che un pacchetto è ora disponibile nel socket corrispondente.

### <a name="peer-address-and-port"></a>Indirizzo e porta peer   
Alla ricezione di un pacchetto UDP, l'applicazione può trovare l'indirizzo IP e il numero di porta del mittente usando il servizio ***nx_udp_packet_info_extract***. In caso di esito positivo, questo servizio fornisce informazioni sull'indirizzo IP del mittente, sul numero di porta del mittente e sull'interfaccia locale tramite cui è stato ricevuto il pacchetto.  

### <a name="thread-suspension"></a>Sospensione dei thread   
Come accennato in precedenza, i thread dell'applicazione possono essere sospesi durante il tentativo di ricevere un pacchetto UDP su una determinata porta UDP. Dopo che un pacchetto è stato ricevuto su tale porta, viene assegnato al primo thread sospeso e il thread viene quindi ripreso. Un timeout facoltativo è disponibile quando si sospende un pacchetto di ricezione UDP, una funzionalità disponibile per la maggior parte dei servizi NetX Duo.  

### <a name="udp-socket-statistics-and-errors"></a>Statistiche ed errori dei socket UDP     
Se abilitato, il software socket UDP di NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Le statistiche e i report degli errori seguenti vengono mantenuti per ogni istanza IP/UDP:

- Totale pacchetti UDP inviati  
- Totale byte UDP inviati  
- Totale pacchetti UDP ricevuti   
- Totale byte UDP ricevuti  
- Totale pacchetti UDP non validi  
- Totale pacchetti di ricezione UDP eliminati  
- Totale errori checksum ricezione UDP  
- Pacchetti socket UDP inviati  
- Byte socket UDP inviati  
- Pacchetti socket UDP ricevuti   
- Byte socket UDP ricevuti  
- Pacchetti socket UDP in coda  
- Pacchetti di ricezione socket UDP eliminati  
- Errori di checksum del socket UDP  

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con il servizio ***nx_udp_info_get** _ per le statistiche UDP su tutti i socket UDP e il servizio _ *_nx_udp_socket_info_get_** per le statistiche UDP sul socket UDP specificato.

### <a name="udp-socket-control-block-nx_udp_socket"></a>Blocco di controllo socket UDP NX_UDP_SOCKET
Le caratteristiche di ogni socket UDP si trovano nel blocco di NX_UDP_SOCKET controllo associato. Contiene informazioni utili, ad esempio il collegamento alla struttura dei dati IP, l'interfaccia di rete per i percorsi di invio e ricezione, la porta associata e la coda di pacchetti di ricezione. Questa struttura è definita nel file ***nx_api.h.***

## <a name="transmission-control-protocol-tcp"></a>TCP (Transmission Control Protocol)

Il Transmission Control Protocol (TCP) fornisce un trasferimento affidabile dei dati di flusso tra due membri di rete (RFC 793). Tutti i dati inviati da un membro di rete vengono verificati e riconosciuti dal membro ricevente. Inoltre, i due membri devono avere stabilito una connessione prima di qualsiasi trasferimento dei dati. Tutto ciò comporta un trasferimento affidabile dei dati. tuttavia richiede un sovraccarico sostanzialmente maggiore rispetto al trasferimento dei dati UDP descritto in precedenza.

Fatta eccezione per quanto specificato, non sono state apportate modifiche ai servizi API del protocollo TCP tra NetX e NetX Duo perché IPv6 riguarda principalmente il livello IP sottostante. Tutti i servizi TCP di NetX Duo possono essere usati per le connessioni IPv4 o IPv6.

### <a name="tcp-header"></a>Intestazione TCP   
Durante la trasmissione, l'intestazione TCP viene posizionata davanti ai dati dell'utente. Durante la ricezione, l'intestazione TCP viene rimossa dal pacchetto in ingresso, lasciando solo i dati utente disponibili per l'applicazione. TCP usa il protocollo IP per inviare e ricevere pacchetti, il che significa che è presente un'intestazione IP davanti all'intestazione TCP quando il pacchetto è in rete. La figura 13 mostra il formato dell'intestazione TCP.

![Diagramma del formato dell'intestazione TCP.](./media/user-guide/image22.png)

### <a name="figure-13-tcp-header"></a>FIGURA 13. Intestazione TCP

Di seguito viene descritto il formato dell'intestazione TCP:

|Campo &nbsp; intestazione |Scopo |
|------|------|
| **Numero di porta di origine a 16 bit** | Questo campo contiene la porta su cui viene inviato il pacchetto TCP. Le porte TCP valide sono da 1 a 0xFFFF. |
| **Porta di destinazione a 16 bit** | Questo campo contiene la porta TCP a cui viene inviato il pacchetto. Le porte TCP valide sono da 1 a 0xFFFF. |
| **Numero di sequenza a 32 bit** | Questo campo contiene il numero di sequenza per i dati inviati da questa estremità della connessione. La sequenza originale viene stabilita durante la sequenza di connessione iniziale tra due nodi TCP. Ogni trasferimento di dati da tale punto comporta un incremento del numero di sequenza della quantità di byte inviati. |
| **Numero di acknowledgement a 32 bit** | Questo campo contiene il numero di sequenza corrispondente all'ultimo byte ricevuto da questo lato della connessione. Viene utilizzato per determinare se i dati inviati in precedenza sono stati ricevuti correttamente dall'altra estremità della connessione. |
| **Lunghezza dell'intestazione a 4 bit** | Questo campo contiene il numero di parole a 32 bit nell'intestazione TCP. Se nell'intestazione TCP non sono presenti opzioni, questo campo è 5. |
| **Bit di codice a 6 bit** |Questo campo contiene i sei diversi bit di codice usati per indicare varie informazioni di controllo associate alla connessione. I bit di controllo sono definiti come segue:<br \> - NUMERIC (21): Urgent data presen<br \> - ACK (20): Acknowledgement number is valid<br - PSH (19): Handle this data immediately (Gestire immediatamente questi dati) \><br - \> RST (18): Reset the connection<br \> - SYN (17): Synchronize sequence numbers (used to establish connection)<br \> - FIN (16): Sender is finished with transmit (used to close connection) |
|**Finestra a 16 bit** |Questo campo viene usato per il controllo di flusso. Contiene la quantità di byte che il socket può attualmente ricevere. Questo viene usato fondamentalmente per il controllo di flusso. Il mittente è responsabile di assicurarsi che i dati da inviare siano adatti alla finestra annunciata del ricevitore. |
|**Checksum TCP a 16 bit** |Questo campo contiene il checksum a 16 bit per il pacchetto, incluse l'intestazione TCP, l'area dei dati del pacchetto e la pseudo-intestazione IP. |
|**Puntatore urgente a 16 bit** |Questo campo contiene l'offset positivo dell'ultimo byte dei dati urgenti. Questo campo è valido solo se il bit di codice VBA è impostato nell'intestazione. |

> [!NOTE]  
> *È previsto che tutte le intestazioni nell'implementazione TCP/IP siano in **big endian** formato. In questo formato, il byte più significativo della parola risiede all'indirizzo di byte più basso*.

### <a name="tcp-enable"></a>TCP Enable       
Prima che siano possibili connessioni TCP e trasmissioni di pacchetti, è necessario che l'applicazione abiliti TCP chiamando ***il nx_tcp_enable*** servizio. Una volta abilitata, l'applicazione può accedere gratuitamente a tutti i servizi TCP.  

### <a name="tcp-socket-create"></a>Creazione di socket TCP    
I socket TCP vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Il tipo iniziale di servizio, la time-to-live e le dimensioni della finestra sono definiti dal ***nx_tcp_socket_create*** servizio. Non sono previsti limiti al numero di socket TCP in un'applicazione.  

### <a name="tcp-checksum"></a>TCP Checksum     
TCP specifica un checksum a 16 bit complementare che copre la pseudo-intestazione IP, costituita dall'indirizzo IP di origine, dall'indirizzo IP di destinazione e dalla parola IP del protocollo/lunghezza, dall'intestazione TCP e dai dati del pacchetto TCP. L'unica differenza tra i checksum dell'intestazione tcp IPv4 e IPv6 è che gli indirizzi IP di origine e di destinazione sono a 32 bit in IPv4 e a 128 bit in IPv6. 

Alcuni controller di rete sono in grado di eseguire il calcolo e la convalida del checksum TCP nell'hardware. Per questi sistemi, è possibile che le applicazioni vogliano usare il più possibile la logica di checksum hardware per ridurre il sovraccarico di runtime. Le applicazioni possono disabilitare completamente la logica di calcolo del checksum TCP dalla libreria NetX Duo in fase di compilazione definendo ***NX_DISABLE_TCP_TX_CHECKSUM** _ e _*_NX_DISABLE_TCP_RX_CHECKSUM_**. In questo modo, il codice checksum TCP non viene compilato in . È tuttavia necessario prestare attenzione se è installato il pacchetto IPsec di NetX Duo facoltativo e la connessione TCP potrebbe dover attraversare un canale sicuro. In questo caso, i dati nei pacchetti appartenenti alla connessione TCP sono già crittografati e la maggior parte dei moduli di checksum TCP hardware presenti nel driver di rete non è in grado di generare un valore di checksum corretto dal payload TCP crittografato.

Per risolvere questo problema, l'applicazione deve mantenere la logica di checksum TCP disponibile nella libreria e usare la funzionalità di interfaccia . Con la funzionalità di interfaccia abilitata, il modulo TCP sa come gestire correttamente il checksum TCP se il driver è anche in grado di calcolare il valore di checksum:

1) Se il pacchetto TCP non è soggetto al processo IPsec, l'hardware dell'interfaccia di rete è in grado di calcolare il checksum. Di conseguenza, il modulo TCP non tenta di calcolare il checksum.

2) Se il pacchetto IPsec è installato e il pacchetto TCP è soggetto al processo IPsec, il modulo TCP calcola il checksum nel software prima di inviare il pacchetto al livello IPsec.

### <a name="tcp-port"></a>Porta TCP     
Una porta TCP è un punto di connessione logico nel protocollo TCP. Nel componente TCP di NetX Duo sono presenti 65.535 porte valide, comprese tra 1 e 0xFFFF. A differenza del protocollo UDP in cui i dati di una porta possono essere inviati a qualsiasi altra porta di destinazione, una porta TCP è connessa a un'altra porta TCP specifica e solo quando viene stabilita questa connessione può verificarsi qualsiasi trasferimento dei dati e solo tra le due porte che la connettono.

> [!IMPORTANT]
> *Le porte TCP sono completamente separate dalle porte UDP.* Ad esempio, il numero di porta UDP 1 non ha alcuna relazione con il numero di porta TCP 1.

### <a name="client-server-model"></a>Client-Server modello     
Per utilizzare TCP per il trasferimento dei dati, è innanzitutto necessario stabilire una connessione tra i due socket TCP. La creazione della connessione viene eseguita in modalità client-server. Il lato client della connessione è il lato che avvia la connessione, mentre il lato server attende semplicemente le richieste di connessione client prima che venga eseguita qualsiasi elaborazione.

> [!IMPORTANT]
> Per i dispositivi multihome, NetX Duo determina automaticamente l'indirizzo di origine da usare per la connessione e l'indirizzo hop successivo in base all'indirizzo *IP di destinazione della connessione. Poiché TCP* è limitato all'invio di pacchetti a indirizzi di destinazione unicast (ad esempio nonbroadcast), NetX Duo non richiede un "hint" per la scelta dell'indirizzo IPv6 di origine.

### <a name="tcp-socket-state-machine"></a>Macchina a stati del socket TCP      
La connessione tra due socket TCP (un client e un server) è complessa e viene gestita in modalità macchina a stati. Ogni socket TCP inizia con uno stato CLOSED. Tramite gli eventi di connessione, la macchina a stati di ogni socket esegue la migrazione allo stato ESTABLISHED, che è il punto in cui viene eseguita la maggior parte del trasferimento dei dati in TCP. Quando un lato della connessione non vuole più inviare dati, si disconnette. Dopo la disconnessione dell'altro lato, il socket TCP torna allo stato CLOSED. Questo processo si ripete ogni volta che un client e un server TCP stabiliscono e chiudono una connessione. La figura 14 mostra i vari stati della macchina a stati TCP.

### <a name="tcp-client-connection"></a>Connessione client TCP       
Come accennato in precedenza, il lato client della connessione TCP avvia una richiesta di connessione a un server TCP. Prima di poter eseguire una richiesta di connessione, è necessario che TCP sia abilitato nell'istanza IP del client. Inoltre, il socket TCP del client deve essere successivamente creato con il servizio ***nx_tcp_socket_create** _ e associato a una porta tramite il servizio _ *_nx_tcp_client_socket_bind_**.

Dopo l'associazione del socket client, ***il nxd_tcp_client_socket_connect*** viene usato per stabilire una connessione con un server TCP. Si noti che il socket deve essere in stato CLOSED per avviare un tentativo di connessione. Per stabilire la connessione, NetX Duo emette un pacchetto SYN e quindi attende un pacchetto SYN ACK dal server, che indica l'accettazione della richiesta di connessione. Dopo la ricezione di SYN ACK, NetX Duo risponde con un pacchetto ACK e alza di livello il socket client allo stato ESTABLISHED.

![Diagramma degli stati della macchina a stati TCP.](./media/user-guide/image24.png)   

**FIGURA 14. Stati della macchina a stati TCP**


> [!WARNING]
> *Le applicazioni devono **nxd_tcp_client_socket_connect** per le connessioni TCP IPv4 e IPv6. Le applicazioni possono comunque **usare nx_tcp_client_socket_connect** per le connessioni TCP IPv4, ma **gli*** sviluppatori sono invitati a usare nxd_tcp_client_socket_connect perché nx_tcp_client_socket_connect sarà deprecato.

*Analogamente, **nxd_tcp_socket_peer_info_get** funziona con le connessioni TCP IPv4 o IPv6. Tuttavia, **nx_tcp_socket_peer_info_get** è ancora disponibile per le applicazioni legacy. Gli sviluppatori sono invitati a **usare nxd_tcp_socket_peer_info_get** in futuro.*

### <a name="tcp-client-disconnection"></a>Disconnessione del client TCP    
La chiusura della connessione viene eseguita chiamando ***nx_tcp_socket_disconnect***. Se non viene specificata alcuna sospensione, il socket client invia un pacchetto RST al socket del server e posiziona il socket nello stato CLOSED. In caso contrario, se viene richiesta una sospensione, viene eseguito il protocollo di disconnessione TCP completo, come indicato di seguito: 

- Se il server ha avviato in precedenza una richiesta di disconnessione (il socket client ha già ricevuto un pacchetto FIN, ha risposto con un ACK e si trova nello stato CLOSE WAIT), NetX Duo alza di livello lo stato del socket TCP del client allo stato LAST ACK e invia un pacchetto FIN. Attende quindi un ACK dal server prima di completare la disconnessione e di entrare nello stato CLOSED.

- Se, d'altra parte, il client è il primo ad avviare una richiesta di disconnessione (il server non si è disconnesso e il socket è ancora nello stato ESTABLISHED), NetX Duo invia un pacchetto FIN per avviare la disconnessione e attende di ricevere un fin e un ACK dal server prima di completare la disconnessione e posizionare il socket in uno stato CLOSED.

Se sono ancora presenti pacchetti nella coda di trasmissione socket, NetX Duo sospende il timeout specificato per consentire il riconoscimento dei pacchetti. Se il timeout scade, NetX Duo svuota la coda di trasmissione del socket client. 

Per disassociare la porta dal socket client, l'applicazione ***chiama nx_tcp_client_socket_unbind***. Il socket deve essere in uno stato CLOSED o in corso di disconnessione (ad esempio, lo stato TIMED WAIT) prima che la porta venga rilasciata. In caso contrario, viene restituito un errore.

Infine, se l'applicazione non necessita più del socket client, chiama ***nx_tcp_socket_delete*** per eliminare il socket.

### <a name="tcp-server-connection"></a>Connessione al server TCP      
Il lato server di una connessione TCP è passivo. ad esempio il server attende che un client avvii la richiesta di connessione. Per accettare una connessione client, è prima necessario che TCP sia abilitato nell'istanza IP chiamando il servizio ***nx_tcp_enable** _. Successivamente, l'applicazione deve creare un socket TCP usando il servizio _ *_nx_tcp_socket_create_**.  

Anche il socket del server deve essere configurato per l'ascolto delle richieste di connessione. A tale scopo, è possibile ***usare nx_tcp_server_socket_listen*** servizio. Questo servizio posiziona il socket del server nello stato LISTEN e associa la porta del server specificata al socket.

> [!NOTE] 
> *Per impostare una routine di callback di ascolto del socket, l'applicazione specifica la funzione di callback appropriata per l'argomento tcp_listen_callback del **nx_tcp_server_socket_listen** corrente. Questa funzione di callback dell'applicazione viene quindi eseguita da NetX Duo ogni volta che viene richiesta una nuova connessione sulla porta del server. L'elaborazione nel callback è sotto il controllo dell'applicazione.*

Per accettare le richieste di connessione client, l'applicazione chiama il servizio ***nx_tcp_server_socket_accept** _. Il socket del server deve essere in uno stato LISTEN o SYN RECEIVED (ad esempio, il server si trova nello stato LISTEN e ha ricevuto un pacchetto SYN da un client che richiede una connessione) per chiamare il servizio accept. Lo stato restituito da _ *_nx_tcp_server_socket_accept_** indica che la connessione è stata impostata e che il socket del server si trova nello stato ESTABLISHED.

Dopo che il socket del server ha una connessione valida, le richieste di connessione client aggiuntive vengono accodati fino alla profondità specificata dal *listen_queue_size,* passato nel  * **nx_tcp_server_socket_listen** _service. Per elaborare le connessioni successive su una porta del server, l'applicazione deve chiamare _ *_nx_tcp_server_socket_relisten_** con un socket disponibile, ad esempio un socket in stato CLOSED. Si noti che è possibile usare lo stesso socket del server se la connessione precedente associata al socket è stata completata e il socket è nello stato CLOSED.

### <a name="tcp-server-disconnection"></a>Disconnessione del server TCP     
La chiusura della connessione viene eseguita chiamando ***nx_tcp_socket_disconnect***. Se non viene specificata alcuna sospensione, il socket del server invia un pacchetto RST al socket client e posiziona il socket nello stato CLOSED. In caso contrario, se viene richiesta una sospensione, viene eseguito il protocollo di disconnessione TCP completo, come indicato di seguito:

- Se il client ha avviato in precedenza una richiesta di disconnessione (il socket del server ha già ricevuto un pacchetto FIN, ha risposto con un ACK e si trova nello stato CLOSE WAIT), NetX Duo alza di livello lo stato del socket TCP allo stato LAST ACK e invia un pacchetto FIN. Attende quindi un ACK dal client prima di completare la disconnessione e di entrare nello stato CLOSED.

- Se invece il server è il primo ad avviare una richiesta di disconnessione (il client non si è disconnesso e il socket è ancora nello stato ESTABLISHED), NetX Duo invia un pacchetto FIN per avviare la disconnessione e attende di ricevere una FIN e un ACK dal client prima di completare la disconnessione e posizionare il socket in uno stato CLOSED.

Se nella coda di trasmissione del socket sono ancora presenti pacchetti, NetX Duo sospende il timeout specificato per consentire il riconoscimento di tali pacchetti. Se il timeout scade, NetX Duo scarica la coda di trasmissione del socket del server.

Al termine dell'elaborazione della disconnessione e quando il socket del server si trova nello stato CLOSED, l'applicazione deve chiamare il servizio ***nx_tcp_server_socket_unaccept** _ per terminare l'associazione di questo socket con la porta del server. Si noti che questo servizio deve essere chiamato dall'applicazione _*_anche se nx_tcp_socket_disconnect_*_ o _*_nx_tcp_server_socket_accept_*_ restituisce uno stato di errore. Al termine _*_nx_tcp_server_socket_unaccept,_*_ il socket può essere usato come socket client o server o anche eliminato se non è più necessario. Se si desidera accettare un'altra connessione client sulla stessa porta del server, è *_necessario chiamare il_* servizio _ nx_tcp_server_socket_relisten * su questo socket.

Il segmento di codice seguente illustra la sequenza di chiamate utilizzate da un tipico server TCP:

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
Dimensioni massime segmento (MSS) è la quantità massima di byte che un host TCP può ricevere senza essere frammentata dal livello IP sottostante. Durante la fase di creazione della connessione TCP, entrambe le estremità scambiano il proprio valore MSS TCP, in modo che il mittente non invii un segmento di dati TCP più grande del mss del ricevitore. Il modulo TCP di NetX Duo convalida facoltativamente il valore MSS annunciato del peer prima di stabilire una connessione. Per impostazione predefinita, NetX Duo non abilita tale controllo. Le applicazioni che vogliono eseguire la convalida MSS devono definire ***NX_ENABLE_TCP_MSS_CHECK** _ durante la compilazione della libreria NetX Duo e il valore minimo deve essere definito in _*_NX_TCP_MSS_MINIMUM_*_. Le connessioni TCP in ingresso con valori MSS inferiori a _ *_NX_TCP_MSS_MINIMUM_** vengono eliminate.

### <a name="stop-listening-on-a-server-port"></a>Arrestare l'ascolto su una porta del server    
Se l'applicazione non vuole più restare in ascolto delle richieste di connessione client su una porta del server specificata in precedenza da una chiamata al servizio ***nx_tcp_server_socket_listen** _, l'applicazione chiama semplicemente il servizio _ *_nx_tcp_server_socket_unlisten_**. Questo servizio inserisce qualsiasi socket in attesa di una connessione nello stato CLOSED e rilascia tutti i pacchetti di richiesta di connessione client in coda. 

### <a name="tcp-window-size"></a>Dimensioni finestra TCP   
Durante le fasi di configurazione e trasferimento dei dati della connessione, ogni porta segnala la quantità di dati che può gestire, denominata dimensione della finestra. Quando i dati vengono ricevuti ed elaborati, le dimensioni della finestra vengono modificate dinamicamente. In TCP un mittente può inviare solo una quantità di dati che rientra nella finestra del ricevitore. In sostanza, le dimensioni della finestra forniscono il controllo di flusso per il trasferimento dei dati in ogni direzione della connessione.   

### <a name="tcp-packet-send"></a>TCP Packet Send     
L'invio di dati TCP viene facilmente ottenuto chiamando ***nx_tcp_socket_send*** funzione . Se le dimensioni dei dati trasmessi sono maggiori del valore MSS del socket o della finestra di ricezione peer corrente, a seconda di quale sia la dimensione minore, la logica interna TCP disconnette i dati che rientra in min (MSS, finestra di ricezione peer) per la trasmissione. Questo servizio crea quindi un'intestazione TCP davanti al pacchetto (incluso il calcolo del checksum). Se le dimensioni della finestra del ricevitore non sono pari a zero, il chiamante invierà il maggior numero di dati possibile per riempire le dimensioni della finestra del ricevitore. Se la finestra di ricezione diventa zero, il chiamante può sospendere e attendere che le dimensioni della finestra del ricevitore aumentino sufficientemente per l'invio del pacchetto. In qualsiasi momento, più thread possono essere sospesi durante il tentativo di inviare dati tramite lo stesso socket. 

> [!WARNING]  
> *I dati TCP che risiedono nella struttura NX_PACKET dati devono trovarsi su un confine lungo. Inoltre, deve essere disponibile* spazio sufficiente tra il puntatore anteposto e il puntatore di avvio dei dati per posizionare le intestazioni TCP, IP e fisiche dei supporti .

### <a name="tcp-packet-retransmit"></a>Ritrasmissione pacchetti TCP      
I pacchetti TCP trasmessi in precedenza vengono effettivamente archiviati internamente fino a quando non viene restituito un ACK dall'altro lato della connessione. Se i dati trasmessi non vengono riconosciuti entro il periodo di timeout, il pacchetto archiviato viene inviato nuovamente e viene impostato il periodo di timeout successivo. Quando viene ricevuto un ACK, tutti i pacchetti coperti dal numero di acknowledgement nella coda di trasmissione interna vengono infine rilasciati.  

> [!WARNING]   
> L'applicazione non riutilizza il pacchetto né modifica il contenuto del pacchetto *dopo nx_tcp_socket_send() restituisce con NX_SUCCESS. Il pacchetto trasmesso viene infine rilasciato dall'elaborazione interna di NetX Duo dopo che i dati sono stati riconosciuti dall'altra estremità.*

### <a name="tcp-keepalive"></a>TCP Keepalive     
La funzionalità Keepalive TCP consente a un socket di rilevare se il peer si disconnette senza terminazione corretta (ad esempio, il peer si è interrotto) o di impedire a determinate funzionalità di monitoraggio della rete di terminare una connessione per lunghi periodi di inattività. Tcp Keepalive funziona inviando periodicamente un frame TCP senza dati e il numero di sequenza impostato su uno in meno rispetto al numero di sequenza corrente. Alla ricezione di tale frame Keepalive TCP, il destinatario, se ancora attivo, risponde con un ACK per il numero di sequenza corrente. Questa operazione completa la transazione keep-live.  

Per impostazione predefinita, la funzionalità keepalive non è abilitata. Per usare questa funzionalità, la libreria NetX Duo deve essere compilata con ***NX_ENABLE_TCP_KEEPALIVE** _ definito. Il simbolo _ *_NX_TCP_KEEPALIVE_INITIAL_** specifica il numero di secondi di inattività prima dell'avvio del frame keep-live.  

### <a name="tcp-packet-receive"></a>Ricezione pacchetti TCP   
L'elaborazione dei pacchetti di ricezione TCP (chiamata dal thread helper IP) è responsabile della gestione di varie azioni di connessione e disconnessione, nonché della trasmissione dell'elaborazione acknowledge. Inoltre, l'elaborazione dei pacchetti di ricezione TCP è responsabile dell'inserimento di pacchetti con dati di ricezione nella coda di ricezione del socket TCP appropriato o del recapito del pacchetto al primo thread sospeso in attesa di un pacchetto.

### <a name="tcp-receive-notify"></a>Notifica di ricezione TCP     
Se il thread dell'applicazione deve elaborare i dati ricevuti da più socket, ***nx_tcp_socket_receive_notify*** usare la funzione . Questa funzione registra una funzione di callback del pacchetto di ricezione per il socket. Ogni volta che viene ricevuto un pacchetto nel socket, viene eseguita la funzione di callback.  

Il contenuto della funzione di callback è specifico dell'applicazione; Tuttavia, la funzione conterrà probabilmente la logica per informare il thread di elaborazione che un pacchetto è disponibile nel socket corrispondente. 

### <a name="thread-suspension"></a>Sospensione dei thread      
Come accennato in precedenza, i thread dell'applicazione possono essere sospesi durante il tentativo di ricevere dati da una determinata porta TCP. Dopo che un pacchetto è stato ricevuto su tale porta, viene assegnato al primo thread sospeso e il thread viene quindi ripreso. Un timeout facoltativo è disponibile quando si sospende un pacchetto di ricezione TCP, una funzionalità disponibile per la maggior parte dei servizi NetX Duo.  

La sospensione dei thread è disponibile anche per i servizi di connessione (client e server), associazione client e disconnessione.  

### <a name="tcp-socket-statistics-and-errors"></a>Statistiche ed errori del socket TCP     
Se abilitato, il software socket TCP di NetX Duo tiene traccia di diverse statistiche ed errori che possono essere utili per l'applicazione. Per ogni istanza IP/TCP vengono mantenute le statistiche e i report degli errori seguenti:   

- Totale pacchetti TCP inviati  
- Totale byte TCP inviati  
- Totale pacchetti TCP ricevuti   
- Totale byte TCP ricevuti   
- Totale pacchetti TCP non validi   
- Totale pacchetti di ricezione TCP eliminati    
- Totale errori checksum ricezione TCP   
- Totale connessioni TCP   
- Totale disconnessioni TCP   
- Totale connessioni TCP eliminate    
- Totale ritrasmissioni pacchetti TCP   
- Pacchetti socket TCP inviati   
- Byte socket TCP inviati   
- Pacchetti socket TCP ricevuti   
- Byte socket TCP ricevuti   
- Ritrasmissioni di pacchetti socket TCP    
- Pacchetti socket TCP in coda    
- Errori di checksum del socket TCP    
- Stato socket TCP    
- Profondità coda trasmissione socket TCP    
- Dimensioni della finestra di trasmissione del socket TCP    
- Dimensioni della finestra di ricezione del socket TCP    

Tutte queste statistiche e segnalazioni errori sono disponibili per l'applicazione con il servizio ***nx_tcp_info_get** _ per le statistiche TCP totali e il servizio _ *_nx_tcp_socket_info_get_** per le statistiche TCP per ogni socket.

### <a name="tcp-socket-control-block-nx_tcp_socket"></a>Blocco di controllo socket TCP NX_TCP_SOCKET      
Le caratteristiche di ogni socket TCP si trovano nel blocco di controllo *NX_TCP_SOCKET* associato, che contiene informazioni utili, ad esempio il collegamento alla struttura dei dati IP, l'interfaccia di connessione di rete, la porta associata e la coda di pacchetti di ricezione. Questa struttura è definita nel file ***nx_api.h.***