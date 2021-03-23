---
title: Capitolo 2-installazione e uso di Azure RTO NetX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello stack di rete ad alte prestazioni Azure RTO NetX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 80d6ba18f47ad2b017dfa32260c83ba074a6dbac
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821542"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx"></a>Capitolo 2-installazione e uso di Azure RTO NetX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello stack di rete ad alte prestazioni Azure RTO NetX.

## <a name="host-considerations"></a>Considerazioni sull'host

Lo sviluppo incorporato viene in genere eseguito nei computer host Windows o Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e il file eseguibile viene generato nell'host, viene scaricato nell'hardware di destinazione per l'esecuzione.

Il download di destinazione viene in genere eseguito dal debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile di fornire il controllo di esecuzione di destinazione (go, Halt, breakpoint e così via), nonché di accedere ai registri della memoria e del processore.

La maggior parte dei debugger dello strumento di sviluppo comunica con l'hardware di destinazione tramite connessioni di debug (OCD) on-chip come JTAG (IEEE 1149,1) e la modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite connessioni di In-Circuit emulazione (ICE). Le connessioni OCD e ICE forniscono soluzioni affidabili con intrusione minima sul software residente di destinazione.

Per quanto riguarda le risorse usate nell'host, il codice sorgente per NetX viene fornito in formato ASCII e richiede circa 1 MB di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

NetX richiede tra 5 Kbyte e 45 kByte di memoria Read-Only (ROM) nella destinazione. Per lo stack di thread NetX e altre strutture di dati globali sono necessari un altro da 1 a 5 Kbyte della memoria ad accesso casuale (RAM) della destinazione.

Inoltre, NetX richiede l'uso di due oggetti timer ThreadX e di un oggetto mutex ThreadX. Queste funzionalità vengono usate per le esigenze di elaborazione periodica e la protezione dei thread all'interno dello stack del protocollo NetX.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO NetX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/netx/> .

Di seguito è riportato un elenco di diversi file importanti nel repository:

- ***nx_api. h***: file di intestazione C contenente tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.
- ***nx_port. h***: file di intestazione C contenente tutte le strutture e le definizioni dei dati specifici dello strumento di sviluppo e della destinazione.  
- ***demo_netx. c***: file c contenente una piccola applicazione demo.
- ***NX. a (o NX. lib)** _: versione binaria della libreria NETX C distribuita con il pacchetto _Standard *.             |

## <a name="netx-installation"></a>Installazione di NetX

È possibile installare NetX clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository NetX nel PC:

```c
    git clone https://github.com/azure-rtos/netx
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante **download** nella pagina principale di GitHub.

Sono inoltre disponibili istruzioni per la compilazione della libreria NetX nella pagina iniziale del repository online.

> [!IMPORTANT]
> Il software applicativo deve accedere al file di libreria NetX (in genere ***NX. a** _ o _*_NX. lib_*_) e i file di inclusione C _ *_nx_api. h e nx_port. h_* *. Questa operazione può essere eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.

## <a name="using-netx"></a>Uso di NetX

Per usare NetX, è necessario che il codice dell'applicazione includa ***nx_api. h** _ durante la compilazione e il collegamento con la libreria NETX _*_NX. a_*_ (o _ *_NX. lib_*) *.

Di seguito sono riportati i quattro passaggi necessari per la compilazione di un'applicazione NetX:

1. Includere il file ***nx_api. h*** in tutti i file dell'applicazione che utilizzano i servizi o le strutture di dati NETX.
1. Inizializzare il sistema NetX chiamando ***nx_system_initialize** _ dalla funzione _ *_tx_application_define_** o da un thread dell'applicazione.  
1. Creare un'istanza IP, abilitare il protocollo ARP (Address Resolution Protocol), se necessario, e i socket dopo la chiamata di ***nx_system_initialize*** .  
1. Compilare l'origine dell'applicazione e il collegamento con la libreria di runtime NetX ***NX. a** _ (o _ *_NX. lib_* *). L'immagine risultante può essere scaricata nella destinazione ed eseguita.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta NetX viene fornita con uno o più esempi eseguiti in una rete effettiva o tramite un driver di rete simulato. È sempre consigliabile eseguire prima il sistema di esempio.

Se il sistema di esempio non viene eseguito correttamente, eseguire le operazioni seguenti per restringere il problema:

1. Determinare la quantità di esempio in esecuzione.
2. Aumentare le dimensioni dello stack in qualsiasi nuovo thread dell'applicazione.
3. Ricompilare la libreria NetX con le opzioni di debug appropriate elencate nella sezione opzione di configurazione.
4. Esaminare la struttura **NX_IP** per verificare se i pacchetti vengono inviati o ricevuti.
5. Esaminare il pool di pacchetti predefinito per verificare se sono presenti pacchetti disponibili.
6. Verificare che il driver di rete fornisca i pacchetti ARP e IP con le relative intestazioni su limiti di 4 byte per le applicazioni che richiedono la connettività IP.
7. Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o è stato modificato. Tali informazioni dovrebbero risultare utili per i tecnici del supporto tecnico.

Seguire le procedure descritte nell'argomento [Customer Support Center](about-this-guide.md) per inviare le informazioni raccolte dalla procedura di risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compilano la libreria NetX e l'applicazione tramite NetX, sono disponibili diverse opzioni di configurazione. Le opzioni di configurazione possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file di inclusione ***nx_user. h*** , salvo diversa indicazione.

> [!IMPORTANT]
> Le opzioni definite in ***nx_user. h** _ vengono applicate solo se l'applicazione e la libreria NETX sono compilate con _ *NX_INCLUDE_USER_DEFINE_FILE** definito.

Le sezioni seguenti elencano le opzioni di configurazione disponibili in NetX.

### <a name="system-configuration-options"></a>Opzioni di configurazione del sistema  

| Opzione  | Descrizione  |
|---|---|
| X_DEBUG | Definito, Abilita le informazioni di debug di stampa facoltative disponibili dal driver di rete Ethernet RAM. |
| NX_DISABLE_ERROR_CHECKING | Definito, rimuove l'API di base per il controllo degli errori di NetX e migliora le prestazioni. I codici restituiti dall'API che non sono interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella definizione dell'API. Questa definizione viene in genere utilizzata dopo il debug dell'applicazione e quando il suo utilizzo migliora le prestazioni e riduce le dimensioni del codice. |
| NX_DRIVER_DEFERRED_PROCESSING | Definito, Abilita la gestione dei pacchetti del driver di rete posticipata. In questo modo, il driver di rete può inserire un pacchetto nell'istanza IP e fare in modo che la routine di elaborazione reale venga chiamata dal thread di supporto IP interno di NetX. |
| NX_ENABLE_EXTENDED_NOTIFY_SUPPORT | Abilita più hook di callback nello stack. Queste funzioni di callback vengono usate dal livello wrapper BSD. Per impostazione predefinita, questa opzione non è definita. |
| NX_ENABLE_SOURCE_ADDRESS_CHECK | Definito, consente di controllare l'indirizzo di origine del pacchetto in ingresso. Per impostazione predefinita, questa opzione è disabilitata. |
| NX_LITTLE_ENDIAN | Definito, esegue lo scambio di byte necessario negli ambienti little endian per assicurarsi che le intestazioni di protocollo siano nel formato big endian appropriato. Si noti che il valore predefinito è in genere configurato in ***nx_port. h***. |
| NX_MAX_PHYSICAL_INTERFACES | Specifica il numero totale di interfacce di rete fisiche nel dispositivo. Il valore predefinito è 1 ed è definito in ***nx_api. h***. Un dispositivo deve avere almeno un'interfaccia fisica. Si noti che non include l'interfaccia di loopback. |
| NX_PHYSICAL_HEADER | Specifica la dimensione in byte dell'intestazione fisica del frame. Il valore predefinito è 16 (basato su un tipico frame Ethernet a 14 byte allineato al limite di 32 bit) ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _*_nx_api. h_*_ , ad esempio in _ *_nx_user. h_*. * |

### <a name="arp-configuration-options"></a>Opzioni di configurazione ARP  

| Opzione  | Descrizione  |
|---|---|
| NX_ARP_DEFEND_BY_REPLY | Definito, consente a NetX di difendere il proprio indirizzo IP inviando una risposta ARP. |
| NX_ARP_DEFEND_INTERVAL | Definisce l'intervallo in secondi durante il quale il modulo ARP invia il successivo pacchetto di difesa in risposta a un messaggio ARP in arrivo che indica un indirizzo in conflitto. |
| NX_ARP_DISABLE_AUTO_ARP_ENTRY | Rinominato in **NX_DISABLE_ARP_AUTO_ENTRY**. Sebbene sia ancora supportato, è consigliabile usare nuove progettazioni per usare **NX_DISABLE_ARP_AUTO_ENTRY**.
| NX_ARP_EXPIRATION_RATE | Specifica il numero di secondi per cui le voci ARP restano valide. Il valore predefinito zero disabilita la scadenza o l'invecchiamento delle voci ARP ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.
| NX_ARP_MAC_CHANGE_NOTIFICATION_ENABLE | Rinominato in **NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION**. Sebbene sia ancora supportato, è consigliabile usare nuove progettazioni per usare **NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION**. |
| NX_ARP_MAX_QUEUE_DEPTH | Specifica il numero massimo di pacchetti che possono essere accodati in attesa di una risposta ARP. Il valore predefinito è 4 ed è definito in ***nx_api. h***. |
| NX_ARP_MAXIMUM_RETRIES | Specifica il numero massimo di tentativi ARP eseguiti senza una risposta ARP. Il valore predefinito è 18 ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _ *_nx_api. h_* *. |
| NX_ARP_UPDATE_RATE | Specifica il numero di secondi tra i tentativi ARP. Il valore predefinito è 10, che rappresenta 10 secondi, ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _ *_nx_api. h_* *. |
| NX_DISABLE_ARP_AUTO_ENTRY | Definito, Disabilita l'immissione delle informazioni sulla richiesta ARP nella cache ARP. |
| NX_DISABLE_ARP_INFO | Definito, Disabilita la raccolta di informazioni ARP. |
| NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION | Definito, consente a ARP di richiamare una funzione di notifica di callback al rilevamento dell'indirizzo MAC aggiornato. |

### <a name="icmp-configuration-options"></a>Opzioni di configurazione ICMP  

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_ICMP_INFO | Definito, Disabilita la raccolta di informazioni ICMP. |
| NX_DISABLE_ICMP_RX_CHECKSUM | Disabilita il calcolo del checksum ICMP nei pacchetti ICMP ricevuti. Questa opzione è utile quando il driver dell'interfaccia di rete è in grado di verificare il checksum ICMP e l'applicazione non usa la funzionalità di frammentazione IP. Per impostazione predefinita, questa opzione non è definita. |
| NX_DISABLE_ICMP_TX_CHECKSUM | Disabilita il calcolo del checksum ICMP nei pacchetti ICMP trasmessi. Questa opzione è utile quando il driver dell'interfaccia di rete è in grado di calcolare il checksum ICMP e l'applicazione non usa la funzionalità di frammentazione IP. Per impostazione predefinita, questa opzione non è definita. |

### <a name="igmp-configuration-options"></a>Opzioni di configurazione IGMP  

| Opzione  | Descrizione  |
|---|---| 
| NX_DISABLE_IGMP_INFO | Definito, Disabilita la raccolta di informazioni IGMP. |
| NX_DISABLE_IGMPV2 | Definisce, Disabilita il supporto IGMPv2 e NetX supporta solo IGMPv1. Per impostazione predefinita, questa opzione non è impostata ed è definita in ***nx_api. h***. |
| NX_MAX_MULTICAST_GROUPS | Specifica il numero massimo di gruppi multicast che è possibile unire in join. Il valore predefinito è 7 ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**. |

### <a name="ip-configuration-options"></a>Opzioni di configurazione IP

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_FRAGMENTATION | Definito, Disabilita la frammentazione IP e la logica di riassemblaggio. |
| NX_DISABLE_IP_INFO | Definito, Disabilita la raccolta di informazioni IP. |
| NX_DISABLE_IP_RX_CHECKSUM | Definito, Disabilita la logica di checksum nei pacchetti IP ricevuti. Questa operazione è utile se il dispositivo di rete è in grado di verificare il checksum dell'intestazione IP e l'applicazione non usa la frammentazione IP. |
| NX_DISABLE_IP_TX_CHECKSUM | Definito, Disabilita la logica di checksum sui pacchetti IP inviati. Questa operazione è utile nelle situazioni in cui il dispositivo di rete sottostante è in grado di generare il checksum dell'intestazione IP e l'applicazione non usa la frammentazione IP. |
| NX_DISABLE_LOOPBACK_INTERFACE | Definito, Disabilita il supporto NetX per l'interfaccia di loopback. |
| NX_DISABLE_RX_SIZE_CHECKING | Definito, Disabilita il controllo delle dimensioni sui pacchetti ricevuti. |
| NX_ENABLE_IP_STATIC_ROUTING | Definito, Abilita il routing statico IP in cui a un indirizzo di destinazione può essere assegnato un indirizzo hop successivo specifico. Per impostazione predefinita, il routing statico IP è disabilitato. |
| NX_IP_PERIODIC_RATE | Definito, specifica il numero di cicli del timer ThreadX in un secondo. Il valore predefinito è derivato dal simbolo ThreadX **TX_TIMER_TICKS_PER_SECOND,** che per impostazione predefinita è impostato su 100 (timer 10 ms). Le applicazioni devono prestare attenzione quando si modifica questo valore, poiché il resto dei moduli NetX derivano le informazioni sulla temporizzazione da **NX_IP_PERIODIC_RATE *.** |
| NX_IP_ROUTING_TABLE_SIZE | Definito, imposta il numero massimo di voci nella tabella di routing statica IP, che è un elenco di un'interfaccia in uscita e l'hop successivo
indirizzi per un indirizzo di destinazione specificato. Il valore predefinito è 8 ed è definito in ***nx_api. h.** _ Questo simbolo viene utilizzato solo se _ *NX_ENABLE_IP_STATIC_ROUTING** è definito. |

### <a name="packet-configuration-options"></a>Opzioni di configurazione pacchetti  

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_PACKET_INFO | Definito, Disabilita la raccolta di informazioni sul pool di pacchetti. | 
| NX_PACKET_HEADER_PAD | Definito, Abilita la spaziatura interna verso la fine del blocco di controllo NX_PACKET. Il numero di parole **ULONG** da riempire è definito da **NX_PACKET_HEADER_PAD_SIZE**. |
| NX_PACKET_HEADER_PAD_SIZE | Imposta il numero di parole **ULONG** da riempire alla struttura NX_PACKET, consentendo all'area del payload del pacchetto di iniziare in corrispondenza dell'oggetto desiderato.
allineamento. Questa funzionalità è utile quando i descrittori del buffer di ricezione puntano direttamente all'area del payload NX_PACKET e la logica di ricezione dell'interfaccia di rete o la logica dell'operazione della cache prevede che l'indirizzo iniziale del buffer soddisfi determinati requisiti di allineamento. Questo valore diventa valido solo quando viene definito **NX_PACKET_HEADER_PAD** . |

### <a name="rarp-configuration-options"></a>Opzioni di configurazione di RARP  

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_RARP_INFO | Definito, Disabilita la raccolta di informazioni di RARP. |

### <a name="tcp-configuration-options"></a>Opzioni di configurazione TCP

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_RESET_DISCONNECT | Definito, Disabilita l'elaborazione della reimpostazione durante la disconnessione quando il valore di timeout specificato viene specificato come **NX_NO_WAIT**. |
| NX_DISABLE_TCP_INFO | Definito, Disabilita la raccolta di informazioni TCP. |
| NX_DISABLE_TCP_RX_CHECKSUM | Definito, Disabilita la logica di checksum nei pacchetti TCP ricevuti. Questa operazione è utile solo nelle situazioni in cui il livello di collegamento presenta un'elaborazione affidabile di checksum o CRC oppure il driver di interfaccia è in grado di verificare il checksum TCP nell'hardware. |
| NX_DISABLE_TCP_TX_CHECKSUM | Definito, Disabilita la logica di checksum per l'invio di pacchetti TCP. Questa operazione è utile solo nelle situazioni in cui il nodo di rete ricevente ha la logica di checksum TCP ricevuta disabilitata o se il driver di rete sottostante è in grado di generare il checksum TCP. |
| NX_ENABLE_TCP_KEEPALIVE | Definito, Abilita il timer TCP keepalive facoltativo. Le impostazioni predefinite non sono abilitate. |
| NX_ENABLE_TCP_MSS_CHECKING | Definito, Abilita la verifica del peer MSS minimo prima di accettare una connessione TCP. Per usare questa funzionalità, è necessario definire il simbolo **NX_ENABLE_TCP_MSS_MINIMUM** . Per impostazione predefinita, questa opzione non è abilitata. |
NX_ENABLE_TCP_WINDOW_SCALING | Abilita l'opzione di scalabilità della finestra per le applicazioni TCP. Se definito, l'opzione di scalabilità della finestra viene negoziata durante la fase di connessione TCP e l'applicazione è in grado di specificare una dimensione della finestra maggiore di 64K. L'impostazione predefinita non è abilitata (non definita). |
| NX_MAX_LISTEN_REQUESTS | Specifica il numero massimo di richieste di ascolto del server. Il valore predefinito è 10 e viene definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**. |
| NX_TCP_ACK_EVERY_N_PACKETS | Specifica il numero di pacchetti TCP da ricevere prima di inviare un ACK. Nota Se **NX_TCP_IMMEDIATE_ACK** è abilitato ma **NX_TCP_ACK_EVERY_N_PACKETS** non è, questo valore viene impostato automaticamente su 1 per compatibilità con le versioni precedenti. |
| NX_TCP_ACK_TIMER_RATE | Specifica il modo in cui il numero di cicli di sistema (NX_IP_PERIODIC_RATE) viene diviso per calcolare la frequenza del timer per l'elaborazione ACK ritardata TCP. Il valore predefinito è 5, che rappresenta 200ms, ed è definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _ *_nx_api. h_* *. |
| NX_TCP_ENABLE_KEEPALIVE | Rinominato in **NX_ENABLE_TCP_KEEPALIVE**. Sebbene sia ancora supportato, è consigliabile usare nuove progettazioni per usare **NX_ENABLE_TCP_KEEPALIVE**. |
| NX_TCP_ENABLE_WINDOW_SCALING | Rinominato in **NX_ENABLE_TCP_WINDOW_SCALING**. Sebbene sia ancora supportato, è consigliabile usare nuove progettazioni per usare **NX_ENABLE_TCP_WINDOW_SCALING**. |
| NX_TCP_FAST_TIMER_RATE | Specifica il modo in cui viene diviso il numero di NetX interni (NX_IP_PERIODIC_RATE) per calcolare la velocità del timer TCP veloce. Il timer TCP veloce viene usato per guidare i vari timer TCP, incluso il timer ACK ritardato. Il valore predefinito è 10, che rappresenta 100 MS presumendo che il timer ThreadX sia in esecuzione in 10 ms. Questo valore è definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _ *_nx_api. h_* *. |
| NX_TCP_IMMEDIATE_ACK | Definito, Abilita l'elaborazione facoltativa della risposta ACK immediata TCP. La definizione di questo simbolo equivale alla definizione di **NX_TCP_ACK_EVERY_N_PACKETS** come 1. |
| NX_TCP_KEEPALIVE_INITIAL | Specifica il numero di secondi di inattività prima dell'attivazione del timer KeepAlive. Il valore predefinito è 7200, che rappresenta 2 ore, ed è definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _ *_nx_api. h_* *. |
| NX_TCP_KEEPALIVE_RETRIES | Specifica il numero di tentativi KeepAlive consentiti prima che la connessione venga considerata interruppe. Il valore predefinito è 10, che rappresenta 10 tentativi e viene definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**. |
| NX_TCP_KEEPALIVE_RETRY | Specifica il numero di secondi tra i tentativi del timer KeepAlive, presumendo che l'altro lato della connessione non stia rispondendo. Il valore predefinito è 75, che rappresenta 75 secondi tra i tentativi e viene definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**. |
| NX_TCP_MAX_OUT_OF_ORDER_PACKETS | Simbolo che definisce il numero massimo di pacchetti TCP non ordinati che possono essere conservati nella coda di ricezione socket TCP. Questo simbolo può essere utilizzato per limitare il numero di pacchetti accodati nel socket di ricezione TCP, evitando che il pool di pacchetti venga esaurito. Per impostazione predefinita, questo simbolo non è definito, pertanto non esiste alcun limite al numero di pacchetti non ordinati accodati nel socket TCP. |
| NX_TCP_MAXIMUM_RETRIES | Specifica il numero di tentativi di trasmissione dati consentiti prima che la connessione venga considerata interruppe. Il valore predefinito è 10, che rappresenta 10 tentativi e viene definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _ *_nx_api. h_* *. |
| NX_TCP_MAXIMUM_TX_QUEUE | Specifica la profondità massima della coda di trasmissione TCP prima della sospensione o del rifiuto delle richieste di invio TCP. Il valore predefinito è 20, il che significa che un massimo di 20 pacchetti può trovarsi nella coda di trasmissione in un determinato momento. Si noti che i pacchetti vengono mantenuti nella coda di trasmissione fino a quando non viene ricevuto un ACK che copre alcuni o tutti i dati del pacchetto dall'altro lato della connessione. Questa costante è definita in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima che includa _ *_nx_api. h_* *. |
| X_TCP_MSS_CHECKING_ENABLED | Rinominato in **NX_ENABLE_TCP_MSS_CHECKING**. Sebbene sia ancora supportato, è consigliabile usare nuove progettazioni per usare **NX_ENABLE_TCP_MSS_CHECKING**. |
| NX_TCP_MSS_MINIMUM | Simbolo che definisce il valore di MSS minimo NetX il modulo TCP accettato. Questa funzionalità è abilitata da **NX_ENABLE_TCP_MSS_CHECK** |
| NX_TCP_RETRY_SHIFT | Specifica la modalità di modifica del periodo di timeout di ritrasmissione tra i tentativi. Se questo valore è 0, il timeout di ritrasmissione iniziale è uguale a quello dei successivi timeout di ritrasmissione. Se questo valore è 1, ogni ritrasmissione successiva è due volte più lungo. Se questo valore è 2, ogni timeout di ritrasmissione successivo è quattro volte più lungo. Il valore predefinito è 0 ed è definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _ *_nx_api. h_* *. |
| NX_TCP_TRANSMIT_TIMER_RATE| Specifica il modo in cui viene diviso il numero di cicli di sistema **NX_IP_PERIODIC_RATE**) per calcolare la frequenza del timer per l'elaborazione dei tentativi di trasmissione TCP. Il valore predefinito è 1, che rappresenta 1 secondo, ed è definito in **_nx_tcp. h_*_. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima che includa _*_nx_api. h_**. |

### <a name="udp-configuration-options"></a>Opzioni di configurazione UDP
| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_UDP_INFO | Definito, Disabilita la raccolta di informazioni UDP. |
| NX_DISABLE_UDP_RX_CHECKSUM | Definito, Disabilita il calcolo del checksum UDP sui pacchetti UDP in ingresso. Questa operazione è utile se il driver dell'interfaccia di rete è in grado di verificare il checksum dell'intestazione UDP nell'hardware e l'applicazione non Abilita la logica di frammentazione IP. |
| NX_DISABLE_UDP_TX_CHECKSUM | Definito, Disabilita il calcolo del checksum UDP nei pacchetti UDP in uscita. Questa operazione è utile se il driver dell'interfaccia di rete è in grado di calcolare il checksum dell'intestazione UDP e di inserire il valore nell'intestazione IP prima di trasmettere i dati e l'applicazione non Abilita la logica di frammentazione IP. |

## <a name="netx-version-id"></a>ID versione NetX

La versione corrente di NetX è disponibile sia per l'utente sia per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione NetX dal file **nx_port. h** . Inoltre, questo file contiene una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di NetX esaminando la stringa globale **_nx_version_id** in **_nx_port. h_**.  

Il software applicativo può inoltre ottenere informazioni sulla versione dalle costanti illustrate di seguito, definite in ***nx_api. h**. *

Queste costanti identificano la versione corrente del prodotto in base al nome e alla versione principale e secondaria del prodotto.

```c
#define EL_PRODUCT_NETX

#define NETX_MAJOR_VERSION

#define NETX_MINOR_VERSION
```