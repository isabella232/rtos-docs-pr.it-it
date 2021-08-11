---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello stack di rete ad alte prestazioni Azure RTOS NetX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 942250cf864fca3c35b97ae731549c070ac2f2f2ef3ef8897e5cbf1e705e7c6a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801803"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx"></a>Capitolo 2 - Installazione e uso di Azure RTOS NetX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello stack di rete ad alte prestazioni Azure RTOS NetX.

## <a name="host-considerations"></a>Considerazioni sull'host

Lo sviluppo incorporato viene in genere eseguito Windows computer host Linux (Unix). Dopo aver compilato, collegato e generato l'eseguibile nell'host, l'applicazione viene scaricata nell'hardware di destinazione per l'esecuzione.

In genere il download di destinazione viene eseguito dall'interno del debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile del controllo dell'esecuzione di destinazione (go, halt, breakpoint e così via), nonché dell'accesso ai registri di memoria e del processore.

La maggior parte dei debugger degli strumenti di sviluppo comunica con l'hardware di destinazione tramite connessioni OCD (On-Chip Debug), ad esempio JTAG (IEEE 1149.1) e modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite In-Circuit di emulazione (ICE). Entrambe le connessioni OCD e ICE offrono soluzioni affidabili con intrusioni minime sul software residente di destinazione.

Come per le risorse usate nell'host, il codice sorgente per NetX viene fornito in formato ASCII e richiede circa 1 Mbyte di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

NetX richiede tra 5 KByte e 45 KByte di memoria Read-Only memoria (ROM) nella destinazione. Altri 1-5 KByte della memoria ad accesso casuale (RAM) della destinazione sono necessari per lo stack di thread NetX e altre strutture di dati globali.

NetX richiede inoltre l'uso di due oggetti timer ThreadX e di un oggetto mutex ThreadX. Queste funzionalità vengono usate per esigenze di elaborazione periodiche e per la protezione dei thread all'interno dello stack del protocollo NetX.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS NetX può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/netx/> .

Di seguito è riportato un elenco di diversi file importanti nel repository:

- ***nx_api.h:*** file di intestazione C contenente tutti gli elementi di sistema, le strutture di dati e i prototipi di servizio.
- ***nx_port.h:*** file di intestazione C contenente tutte le definizioni e le strutture dei dati specifici dello strumento di sviluppo e della destinazione.  
- ***demo_netx.c***: file C contenente una piccola applicazione demo.
- ***nx.a (o nx.lib)** _: versione binaria della libreria NetX C distribuita con il pacchetto _standard*.             |

## <a name="netx-installation"></a>Installazione di NetX

È possibile installare NetX clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository NetX nel PC:

```c
    git clone https://github.com/azure-rtos/netx
```

In alternativa, è possibile scaricare una copia del repository usando il **pulsante Scarica** nella GitHub principale.

Le istruzioni per la compilazione della libreria NetX sono disponibili anche nella prima pagina del repository online.

> [!IMPORTANT]
> Il software dell'applicazione deve accedere al file di libreria NetX (in genere ***nx.a** _ o _*_nx.lib_*_) e ai file di inclusione C _*_nx_api.h e nx_port.h_**. Questa operazione viene eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.

## <a name="using-netx"></a>Uso di NetX

Per usare NetX, il codice dell'applicazione deve includere ***nx_api.h** _ durante la compilazione e il collegamento con la libreria NetX _*_nx.a_*_ (o _ *_nx.lib_*)*.

Di seguito sono riportati i quattro passaggi necessari per la compilazione di un'applicazione NetX:

1. Includere il ***file nx_api.h*** in tutti i file dell'applicazione che usano servizi NetX o strutture di dati.
1. Inizializzare il sistema NetX chiamando ***nx_system_initialize** _ dalla funzione _ *_tx_application_define_** o da un thread dell'applicazione.  
1. Creare un'istanza IP, abilitare il protocollo ARP (Address Resolution Protocol), se necessario, e tutti i socket dopo ***nx_system_initialize*** chiamata.  
1. Compilare l'origine dell'applicazione e collegarsi alla libreria di runtime NetX ***nx.a** _ (o _*_nx.lib_**). L'immagine risultante può essere scaricata nella destinazione ed eseguita.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta NetX viene recapitata con uno o più esempi eseguiti in una rete effettiva o tramite un driver di rete simulato. È sempre buona idea che il sistema di esempio sia in esecuzione per primo.

Se il sistema di esempio non viene eseguito correttamente, eseguire le operazioni seguenti per restringere il problema:

1. Determinare la parte dell'esempio in esecuzione.
2. Aumentare le dimensioni dello stack in tutti i nuovi thread dell'applicazione.
3. Ricompilare la libreria NetX con le opzioni di debug appropriate elencate nella sezione delle opzioni di configurazione.
4. Esaminare la **NX_IP** per verificare se i pacchetti vengono inviati o ricevuti.
5. Esaminare il pool di pacchetti predefinito per verificare se sono disponibili pacchetti.
6. Assicurarsi che il driver di rete fornirà i pacchetti ARP e IP con le intestazioni sui limiti a 4 byte per le applicazioni che richiedono la connettività IP.
7. Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o cambia. Tali informazioni dovrebbero risultare utili per i tecnici del supporto tecnico.

Seguire le procedure descritte nell'argomento [Customer Support Center](about-this-guide.md) per inviare le informazioni raccolte dai passaggi per la risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compila la libreria NetX e l'applicazione con NetX, sono disponibili diverse opzioni di configurazione. Le opzioni di configurazione possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file di inclusione ***nx_user.h,*** se non diversamente specificato.

> [!IMPORTANT]
> Le opzioni definite in ***nx_user.h** _ vengono applicate solo se l'applicazione e la libreria NetX vengono compilate con _ *NX_INCLUDE_USER_DEFINE_FILE** definito.

Le sezioni seguenti elencano le opzioni di configurazione disponibili in NetX.

### <a name="system-configuration-options"></a>Opzioni di configurazione del sistema  

| Opzione  | Descrizione  |
|---|---|
| X_DEBUG | Definito, abilita le informazioni di debug di stampa facoltative disponibili dal driver di rete Ethernet ram. |
| NX_DISABLE_ERROR_CHECKING | Definito, rimuove l'API di controllo degli errori NetX di base e migliora le prestazioni. I codici restituiti dell'API che non sono interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella definizione dell'API. Questa definizione viene in genere usata dopo il debug dell'applicazione e quando il relativo utilizzo migliora le prestazioni e riduce le dimensioni del codice. |
| NX_DRIVER_DEFERRED_PROCESSING | Definito, abilita la gestione dei pacchetti del driver di rete posticipata. In questo modo il driver di rete può inserire un pacchetto nell'istanza IP e avere la routine di elaborazione reale chiamata dal thread helper IP interno di NetX. |
| NX_ENABLE_EXTENDED_NOTIFY_SUPPORT | Abilita più hook di callback nello stack. Queste funzioni di callback vengono usate dal livello wrapper BSD. Per impostazione predefinita, questa opzione non è definita. |
| NX_ENABLE_SOURCE_ADDRESS_CHECK | Definito, consente di controllare l'indirizzo di origine del pacchetto in ingresso. Per impostazione predefinita, questa opzione è disabilitata. |
| NX_LITTLE_ENDIAN | Definito, esegue lo scambio di byte necessario negli ambienti little endian per garantire che le intestazioni del protocollo siano nel formato big endian corretto. Si noti che il valore predefinito è in ***genere nx_port.h***. |
| NX_MAX_PHYSICAL_INTERFACES | Specifica il numero totale di interfacce di rete fisiche nel dispositivo. Il valore predefinito è 1 ed è definito in ***nx_api.h.*** Un dispositivo deve avere almeno un'interfaccia fisica. Si noti che non include l'interfaccia di loopback. |
| NX_PHYSICAL_HEADER | Specifica le dimensioni in byte dell'intestazione fisica del frame. Il valore predefinito è 16 (basato su un frame Ethernet tipico a 14 byte allineato al limite a 32 bit) ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima che _*_nx_api.h_*_ sia incluso, ad esempio in _ *_nx_user.h_*.* |

### <a name="arp-configuration-options"></a>Opzioni di configurazione ARP  

| Opzione  | Descrizione  |
|---|---|
| NX_ARP_DEFEND_BY_REPLY | Definito, consente a NetX di proteggere il proprio indirizzo IP inviando una risposta ARP. |
| NX_ARP_DEFEND_INTERVAL | Definisce l'intervallo, espresso in secondi, il modulo ARP invia il pacchetto di difesa successivo in risposta a un messaggio ARP in ingresso che indica un indirizzo in conflitto. |
| NX_ARP_DISABLE_AUTO_ARP_ENTRY | Rinominato in **NX_DISABLE_ARP_AUTO_ENTRY**. Anche se è ancora supportato, è consigliato l'uso di nuove **progettazioni NX_DISABLE_ARP_AUTO_ENTRY**.
| NX_ARP_EXPIRATION_RATE | Specifica il numero di secondi per cui le voci ARP rimangono valide. Il valore predefinito zero disabilita la scadenza o la scadenza delle voci ARP ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima *_dell'nx_api.h_**.
| NX_ARP_MAC_CHANGE_NOTIFICATION_ENABLE | Rinominato in **NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION**. Anche se è ancora supportato, le nuove progettazioni sono invitate a usare **NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION**. |
| NX_ARP_MAX_QUEUE_DEPTH | Specifica il numero massimo di pacchetti che possono essere accodati durante l'attesa di una risposta ARP. Il valore predefinito è 4 ed è definito in ***nx_api.h***. |
| NX_ARP_MAXIMUM_RETRIES | Specifica il numero massimo di tentativi ARP esecuti senza una risposta ARP. Il valore predefinito è 18 ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima di includere _*_nx_api.h_**. |
| NX_ARP_UPDATE_RATE | Specifica il numero di secondi tra i tentativi ARP. Il valore predefinito è 10, che rappresenta 10 secondi ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima di includere _*_nx_api.h_**. |
| NX_DISABLE_ARP_AUTO_ENTRY | Definito, disabilita l'immissione delle informazioni sulla richiesta ARP nella cache ARP. |
| NX_DISABLE_ARP_INFO | Definito, disabilita la raccolta di informazioni ARP. |
| NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION | Definito, consente a ARP di richiamare una funzione di notifica di callback al rilevamento dell'aggiornamento dell'indirizzo MAC. |

### <a name="icmp-configuration-options"></a>Opzioni di configurazione ICMP  

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_ICMP_INFO | Definito, disabilita la raccolta di informazioni ICMP. |
| NX_DISABLE_ICMP_RX_CHECKSUM | Disabilita il calcolo del checksum ICMP sui pacchetti ICMP ricevuti. Questa opzione è utile quando il driver dell'interfaccia di rete è in grado di verificare il checksum ICMP e l'applicazione non usa la funzionalità di frammentazione IP. Per impostazione predefinita, questa opzione non è definita. |
| NX_DISABLE_ICMP_TX_CHECKSUM | Disabilita il calcolo del checksum ICMP sui pacchetti ICMP trasmessi. Questa opzione è utile quando il driver dell'interfaccia di rete è in grado di calcolare il checksum ICMP e l'applicazione non usa la funzionalità di frammentazione IP. Per impostazione predefinita, questa opzione non è definita. |

### <a name="igmp-configuration-options"></a>Opzioni di configurazione IGMP  

| Opzione  | Descrizione  |
|---|---| 
| NX_DISABLE_IGMP_INFO | Definito, disabilita la raccolta di informazioni IGMP. |
| NX_DISABLE_IGMPV2 | Definito, disabilita il supporto IGMPv2 e NetX supporta solo IGMPv1. Per impostazione predefinita, questa opzione non è impostata ed è definita in ***nx_api.h***. |
| NX_MAX_MULTICAST_GROUPS | Specifica il numero massimo di gruppi multicast che possono essere uniti. Il valore predefinito è 7 ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima *_dell'nx_api.h_**. |

### <a name="ip-configuration-options"></a>Opzioni di configurazione IP

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_FRAGMENTATION | Definito, disabilita la frammentazione IP e la logica di riassemblaggio. |
| NX_DISABLE_IP_INFO | Definito, disabilita la raccolta di informazioni IP. |
| NX_DISABLE_IP_RX_CHECKSUM | Definito, disabilita la logica di checksum sui pacchetti IP ricevuti. Ciò è utile se il dispositivo di rete è in grado di verificare il checksum dell'intestazione IP e l'applicazione non usa la frammentazione IP. |
| NX_DISABLE_IP_TX_CHECKSUM | Definito, disabilita la logica di checksum sui pacchetti IP inviati. Ciò è utile nelle situazioni in cui il dispositivo di rete sottostante è in grado di generare il checksum dell'intestazione IP e l'applicazione non usa la frammentazione IP. |
| NX_DISABLE_LOOPBACK_INTERFACE | Definito, disabilita il supporto NetX per l'interfaccia di loopback. |
| NX_DISABLE_RX_SIZE_CHECKING | Definito, disabilita il controllo delle dimensioni sui pacchetti ricevuti. |
| NX_ENABLE_IP_STATIC_ROUTING | Definito, abilita il routing statico IP in cui a un indirizzo di destinazione può essere assegnato un indirizzo hop successivo specifico. Per impostazione predefinita, il routing statico IP è disabilitato. |
| NX_IP_PERIODIC_RATE | Definito, specifica il numero di tick del timer ThreadX in un secondo. Il valore predefinito è derivato dal simbolo ThreadX **TX_TIMER_TICKS_PER_SECOND,** che per impostazione predefinita è impostato su 100 (timer di 10 ms). Le applicazioni devono prestare attenzione quando modificano questo valore, poiché gli altri moduli NetX derivano le informazioni di intervallo **NX_IP_PERIODIC_RATE*.** |
| NX_IP_ROUTING_TABLE_SIZE | Definito, imposta il numero massimo di voci nella tabella di routing statico IP, ovvero un elenco di un'interfaccia in uscita e l'hop successivo
indirizzi per un determinato indirizzo di destinazione. Il valore predefinito è 8 ed è definito in ***nx_api.h.** _ Questo simbolo viene usato solo se _ *NX_ENABLE_IP_STATIC_ROUTING** è definito. |

### <a name="packet-configuration-options"></a>Opzioni di configurazione dei pacchetti  

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_PACKET_INFO | Definito, disabilita la raccolta di informazioni sul pool di pacchetti. | 
| NX_PACKET_HEADER_PAD | Definito, abilita la spaziatura interna verso la fine del blocco NX_PACKET controllo. Il numero di **parole ULONG** da riempire è definito da **NX_PACKET_HEADER_PAD_SIZE**. |
| NX_PACKET_HEADER_PAD_SIZE | Imposta il numero di **parole ULONG** da aggiungere alla struttura NX_PACKET, consentendo all'area del payload del pacchetto di iniziare in corrispondenza della struttura desiderata
Allineamento. Questa funzionalità è utile quando i descrittori del buffer di ricezione puntano direttamente NX_PACKET un'area di payload e la logica di ricezione dell'interfaccia di rete o la logica di operazione della cache prevede che l'indirizzo iniziale del buffer soddisfi determinati requisiti di allineamento. Questo valore diventa valido solo quando **NX_PACKET_HEADER_PAD** è definito . |

### <a name="rarp-configuration-options"></a>Opzioni di configurazione RARP  

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_RARP_INFO | Definito, disabilita la raccolta di informazioni RARP. |

### <a name="tcp-configuration-options"></a>Opzioni di configurazione TCP

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_RESET_DISCONNECT | Definito, disabilita l'elaborazione della reimpostazione durante la disconnessione quando il valore di timeout specificato viene specificato **come NX_NO_WAIT**. |
| NX_DISABLE_TCP_INFO | Definito, disabilita la raccolta di informazioni TCP. |
| NX_DISABLE_TCP_RX_CHECKSUM | Definito, disabilita la logica di checksum sui pacchetti TCP ricevuti. Ciò è utile solo nelle situazioni in cui il livello di collegamento dispone di checksum affidabile o elaborazione CRC o il driver di interfaccia è in grado di verificare il checksum TCP nell'hardware. |
| NX_DISABLE_TCP_TX_CHECKSUM | Definito, disabilita la logica di checksum per l'invio di pacchetti TCP. Ciò è utile solo nelle situazioni in cui la logica di checksum TCP ricevuta nel nodo di rete ricevente è disabilitata o il driver di rete sottostante è in grado di generare il checksum TCP. |
| NX_ENABLE_TCP_KEEPALIVE | Definito, abilita il timer keepalive TCP facoltativo. Le impostazioni predefinite non sono abilitate. |
| NX_ENABLE_TCP_MSS_CHECKING | Definito, abilita la verifica di MSS peer minimo prima di accettare una connessione TCP. Per usare questa funzionalità, è necessario **NX_ENABLE_TCP_MSS_MINIMUM** simbolo. Per impostazione predefinita, questa opzione non è abilitata. |
NX_ENABLE_TCP_WINDOW_SCALING | Abilita l'opzione di ridimensionamento della finestra per le applicazioni TCP. Se definita, l'opzione di ridimensionamento della finestra viene negoziata durante la fase di connessione TCP e l'applicazione è in grado di specificare dimensioni della finestra maggiori di 64 KB. L'impostazione predefinita non è abilitata (non definita). |
| NX_MAX_LISTEN_REQUESTS | Specifica il numero massimo di richieste di ascolto del server. Il valore predefinito è 10 ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima *_dell'nx_api.h_**. |
| NX_TCP_ACK_EVERY_N_PACKETS | Specifica il numero di pacchetti TCP da ricevere prima di inviare un ACK. Si noti **che NX_TCP_IMMEDIATE_ACK** è **abilitato, NX_TCP_ACK_EVERY_N_PACKETS** non lo è, questo valore viene impostato automaticamente su 1 per compatibilità con le versioni precedenti. |
| NX_TCP_ACK_TIMER_RATE | Specifica il modo in cui il numero di tick di sistema (NX_IP_PERIODIC_RATE) viene diviso per calcolare la velocità del timer per l'elaborazione tcp ACK ritardata. Il valore predefinito è 5, che rappresenta 200 ms, ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima di includere _*_nx_api.h_**. |
| NX_TCP_ENABLE_KEEPALIVE | Rinominato in **NX_ENABLE_TCP_KEEPALIVE**. Anche se è ancora supportato, le nuove progettazioni sono invitate a usare **NX_ENABLE_TCP_KEEPALIVE**. |
| NX_TCP_ENABLE_WINDOW_SCALING | Rinominato in **NX_ENABLE_TCP_WINDOW_SCALING**. Anche se è ancora supportato, le nuove progettazioni sono invitate a usare **NX_ENABLE_TCP_WINDOW_SCALING**. |
| NX_TCP_FAST_TIMER_RATE | Specifica come viene diviso il numero di tick interni NetX (NX_IP_PERIODIC_RATE) per calcolare la velocità del timer TCP. Il timer TCP rapido viene usato per guidare i vari timer TCP, incluso il timer ACK ritardato. Il valore predefinito è 10, che rappresenta 100 ms presupponendo che il timer ThreadX sia in esecuzione a 10 ms. Questo valore è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima di includere _*_nx_api.h_**. |
| NX_TCP_IMMEDIATE_ACK | Definito, abilita l'elaborazione della risposta ACK immediata TCP facoltativa. La definizione di questo simbolo equivale a **definire** NX_TCP_ACK_EVERY_N_PACKETS deve essere 1. |
| NX_TCP_KEEPALIVE_INITIAL | Specifica il numero di secondi di inattività prima dell'attivazione del timer keep-live. Il valore predefinito è 7200, che rappresenta 2 ore ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima di includere _*_nx_api.h_**. |
| NX_TCP_KEEPALIVE_RETRIES | Specifica il numero di tentativi keep-live consentiti prima che la connessione venga considerata interrotta. Il valore predefinito è 10, che rappresenta 10 tentativi, ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima *_dell'nx_api.h_**. |
| NX_TCP_KEEPALIVE_RETRY | Specifica il numero di secondi tra i tentativi del timer keep-live presupponendo che l'altro lato della connessione non risponda. Il valore predefinito è 75, che rappresenta 75 secondi tra un tentativo e l'altro ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima *_dell'nx_api.h_**. |
| NX_TCP_MAX_OUT_OF_ORDER_PACKETS | Simbolo che definisce il numero massimo di pacchetti TCP non in ordine che possono essere mantenuti nella coda di ricezione del socket TCP. Questo simbolo può essere usato per limitare il numero di pacchetti in coda nel socket di ricezione TCP, impedendo che il pool di pacchetti venga affamato. Per impostazione predefinita, questo simbolo non è definito, pertanto non esiste alcun limite al numero di pacchetti non in ordine in coda nel socket TCP. |
| NX_TCP_MAXIMUM_RETRIES | Specifica il numero di tentativi di trasmissione dei dati consentiti prima che la connessione venga considerata interrotta. Il valore predefinito è 10, che rappresenta 10 tentativi, ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima di includere _*_nx_api.h_**. |
| NX_TCP_MAXIMUM_TX_QUEUE | Specifica la profondità massima della coda di trasmissione TCP prima che le richieste di invio TCP siano sospese o rifiutate. Il valore predefinito è 20, il che significa che nella coda di trasmissione possono essere presenti al massimo 20 pacchetti in qualsiasi momento. Si noti che i pacchetti rimangono nella coda di trasmissione fino a quando non viene ricevuto un ACK che copre alcuni o tutti i dati del pacchetto dall'altro lato della connessione. Questa costante è definita in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima che includa _*_nx_api.h_**. |
| X_TCP_MSS_CHECKING_ENABLED | Rinominato in **NX_ENABLE_TCP_MSS_CHECKING**. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare **NX_ENABLE_TCP_MSS_CHECKING**. |
| NX_TCP_MSS_MINIMUM | Simbolo che definisce il valore MSS minimo accettato dal modulo TCP NetX. Questa funzionalità è abilitata da **NX_ENABLE_TCP_MSS_CHECK** |
| NX_TCP_RETRY_SHIFT | Specifica il modo in cui il periodo di timeout di ritrasmissione cambia tra i tentativi. Se questo valore è 0, il timeout di ritrasmissione iniziale corrisponde ai timeout di ritrasmissione successivi. Se questo valore è 1, ogni ritrasmissione successiva è due volte più lunga. Se questo valore è 2, ogni timeout di ritrasmissione successivo è quattro volte più lungo. Il valore predefinito è 0 ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima di includere _*_nx_api.h_**. |
| NX_TCP_TRANSMIT_TIMER_RATE| Specifica il modo in cui il numero di tick di sistema **NX_IP_PERIODIC_RATE**) viene diviso per calcolare la frequenza del timer per l'elaborazione dei tentativi di trasmissione TCP. Il valore predefinito è 1, che rappresenta 1 secondo, ed è definito in **_nx_tcp.h_*_. L'applicazione può eseguire l'override del* valore predefinito definendo il valore prima che includa _ _nx_api.h_**. |

### <a name="udp-configuration-options"></a>Opzioni di configurazione UDP
| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_UDP_INFO | Definito, disabilita la raccolta di informazioni UDP. |
| NX_DISABLE_UDP_RX_CHECKSUM | Definito, disabilita il calcolo del checksum UDP sui pacchetti UDP in ingresso. Ciò è utile se il driver dell'interfaccia di rete è in grado di verificare il checksum dell'intestazione UDP nell'hardware e l'applicazione non abilita la logica di frammentazione IP. |
| NX_DISABLE_UDP_TX_CHECKSUM | Definito, disabilita il calcolo del checksum UDP sui pacchetti UDP in uscita. Ciò è utile se il driver dell'interfaccia di rete è in grado di calcolare il checksum dell'intestazione UDP e inserire il valore nell'intestazione IP prima di trasmettere i dati e l'applicazione non abilita la logica di frammentazione IP. |

## <a name="netx-version-id"></a>ID versione NetX

La versione corrente di NetX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione di NetX dal file **nx_port.h.** Inoltre, questo file contiene una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di NetX esaminando la stringa **globale _nx_version_id** in **_nx_port.h_**.  

Il software applicativo può anche ottenere informazioni sulla versione dalle costanti illustrate di seguito, definite in ***nx_api.h**.*

Queste costanti identificano la versione corrente del prodotto in base al nome e alla versione principale e secondaria del prodotto.

```c
#define EL_PRODUCT_NETX

#define NETX_MAJOR_VERSION

#define NETX_MINOR_VERSION
```