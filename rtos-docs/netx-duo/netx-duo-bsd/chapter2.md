---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX Duo BSD
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del Azure RTOS NetX Duo BSD.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 560621e528c8ce98013ce505ea1511f466317f4a087aa44cc0e70cb4d4b8ed1e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788508"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-bsd"></a>Capitolo 2 - Installazione e uso di Azure RTOS NetX Duo BSD

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del Azure RTOS NetX Duo BSD.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS NetX Duo BSD può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nxd_bsd.h:** file di intestazione per NetX Duo BSD
- **nxd_bsd.c:** file di origine C per NetX Duo BSD
- **nxd_bsd.pdf:** Manuale dell'utente per NetX Duo BSD

File demo:

- **bsd_demo_udp.c**
- **bsd_demo_tcp.c**
- **bsd_demo_raw.c**

## <a name="netx-duo-bsd-installation"></a>Installazione di NetX Duo BSD

Per usare NetX Duo BSD, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Ad esempio, se NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_bsd.h* e *nxd_bsd.c* devono essere copiati in questa directory.

## <a name="building-the-threadx-and-netx-duo-components-of-a-bsd-application"></a>Compilazione dei componenti ThreadX e NetX Duo di un'applicazione BSD

### <a name="threadx"></a>ThreadX

La libreria ThreadX deve definire `bsd_errno` nell'archiviazione locale del thread. È consigliabile seguire questa procedura:

1. In *tx_port.h* impostare una delle macro TX_THREAD_EXTENSION seguenti:
   - `#define TX_THREAD_EXTENSION_3     int bsd_errno`

1. Ricompilare la libreria ThreadX.

> [!NOTE]
> Se TX_THREAD_EXTENSION_3 è già in uso, l'utente può usare una delle altre macro TX_THREAD_EXTENSION.

### <a name="netx-duo"></a>NetX Duo

Prima di usare i servizi BSD di NetX Duo, la libreria NetX Duo deve essere compilata con NX_ENABLE_EXTENDED_NOTIFY_SUPPORT definite. Per impostazione predefinita, non è definito. Se è necessario usare i socket non elaborati BSD, la libreria NetX Duo deve essere compilata con NX_ENABLE_IP_RAW_PACKET_FILTER definiti.

## <a name="using-netx-duo-bsd"></a>Uso di NetX Duo BSD

Un progetto di applicazione NetX Duo BSD deve includere *nxd_bsd.h* dopo aver incluso *tx_api.h* e *nx_api.h* per poter usare i servizi BSD specificati più avanti in questa guida. L'applicazione deve anche *includere nxd_bsd.c* nel processo di compilazione. Questo file deve essere compilato nello stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX Duo BSD.

Per usare i servizi BSD di NetX Duo, l'applicazione deve creare un'istanza IP, creare un pool di pacchetti da cui il livello BSD alloca i pacchetti, allocare spazio di memoria per lo stack di thread BSD interno e specificare la priorità del thread BSD interno. Il livello BSD viene inizializzato chiamando *bsd_initialize* e passando i parametri. Questo è illustrato in "Piccoli esempi" più avanti in questo documento, ma il prototipo è illustrato di seguito:

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                    *CHAR *bsd_thread_stack_area,
                    *ULONG bsd_thread_stack_size,
                    *UINT bsd_thread_priority*);
```

Il default_ip è l'istanza IP su cui opera il livello BSD. Il default_pool viene usato dai servizi BSD da cui allocare i pacchetti. I due parametri successivi: bsd_thread_stack_area, bsd_thread_stack_size definisce l'area dello stack usata dal thread BSD interno e l'ultimo parametro, bsd_thread_priority, imposta la priorità del thread.

## <a name="netx-duo-bsd-raw-socket-support"></a>Supporto per socket non elaborati NetX Duo BSD

NetX Duo BSD supporta anche socket non elaborati. Per usare socket non elaborati in NetX Duo BSD, la libreria NetX Duo deve essere compilata con NX_ENABLE_IP_RAW_PACKET_FILTER definiti. Per impostazione predefinita, non è definito. L'applicazione deve quindi abilitare l'elaborazione socket non elaborata per un'istanza IP creata in precedenza chiamando *nx_ip_raw_packet_enable.*

Per creare un socket non elaborato in NetX Duo BSD, l'applicazione usa il socket di creazione del *socket* di servizio e specifica la famiglia di protocolli, il tipo di socket e il protocollo:

```c
sock_1 = socket(INT protocolFamily, INT socket_type, INT protocol)
```

protocolFamily è AF_INET per i socket IPv4 o AF_INET6 per i socket IPv6, presupponendo che IPv6 sia abilitato nell'istanza IP. La socket_type deve essere impostata su SOCK_RAW. il protocollo è specifico dell'applicazione.

Per inviare e ricevere pacchetti non elaborati e chiudere un socket non elaborato, l'applicazione usa in genere gli stessi servizi BSD di udp, ad esempio *sendto, recvfrom, select* e soc_close *.* I socket non elaborati non supportano i servizi BSD *accept* o *listen.*

- Per impostazione predefinita, i dati non elaborati IPv4 ricevuti includono l'intestazione IPv4.  Al contrario, i dati non elaborati IPv6 ricevuti non includono l'intestazione IPv6.

- Per impostazione predefinita, quando si inviano pacchetti IPv6 o IPv4 non elaborati, il livello wrapper BSD aggiunge l'intestazione IPv6 o IPv4 prima di inviare i dati.

NetX Duo BSD supporta opzioni aggiuntive per socket non elaborati, tra cui IP_RAW_RX_NO_HEADER, IP_HDRINCL e IP_RAW_IPV6_HDRINCL.

Se IP_RAW_RX_NO_HEADER è impostata, l'intestazione IPv4 viene rimossa in modo che i dati ricevuti non contengano l'intestazione IPv4 e la lunghezza del messaggio segnalata non includa l'intestazione IPv4.  Per i socket IPv6, per impostazione predefinita la ricezione di socket non elaborati non include l'intestazione IPv6, equivalente all'impostazione dell IP_RAW_RX_NO_HEADER predefinita. L'applicazione può usare il servizio *setsockopt* per deselezionare l'opzione IP_RAW_RX_NO_HEADER. Una volta deselezionata l'opzione IP_RAW_RX_NO_HEADER, i dati non elaborati IPv6 ricevuti includerebbero l'intestazione IPv6 e la lunghezza del messaggio segnalata includerà l'intestazione IPv6.

Questa opzione non ha alcun effetto sui dati trasmessi IPv4 o IPv6.

Se IP_HDRINCL è impostata, l'applicazione include l'intestazione IPv4 durante l'invio dei dati.  Questa opzione non ha alcun effetto sulla trasmissione IPv6 e non è definita per impostazione predefinita. Se IP_RAW_IPV6_HDRINCL è impostata, l'applicazione include l'intestazione IPv6 durante l'invio dei dati.  Questa opzione non ha alcun effetto sulla trasmissione IPv4 e non è definita per impostazione predefinita.

IP_HDRINCL e IP_RAW_IPV6_HDRINCL non hanno alcun effetto sulla ricezione IPv4 o IPv6.

> [!NOTE]
> La specifica del socket BSD 4.3 specifica che il kernel deve copiare il pacchetto non elaborato in ogni buffer di ricezione socket. Tuttavia, in NetX Duo BSD, se vengono creati più socket che condividono lo stesso protocollo, il comportamento non è definito.

## <a name="netx-duo-bsd-raw-packet-support"></a>Supporto dei pacchetti non elaborati di NetX Duo BSD

Per abilitare il supporto dei pacchetti non elaborati per PPPoE, il wrapper BSD di NetX Duo deve essere compilato con NX_BSD_RAW_PPPOE_SUPPORT abilitata.

Il comando seguente crea un socket BSD per gestire pacchetti PPPoE non elaborati:

```c
Sockfd = socket(AF_PACKET, SOCK_RAW, protocol);
```

L'implementazione BSD corrente supporta solo due tipi di protocollo AF_PACKET famiglia

- `ETHERTYPE_PPPOE_DISC`: pacchetti di individuazione PPPoE. Nel frame di dati MAC i pacchetti discovery hanno il tipo di frame Ethernet 0x8863.

- `ETHERTYPE_PPPOE_SESS`: pacchetti di sessione PPP. Nel frame di dati MAC i pacchetti di sessione hanno il tipo di frame Ethernet 0x8864.

La struttura `sockaddr_ll` viene utilizzata per specificare i parametri durante l'invio o la ricezione di frame PPPoE.

`struct sockaddr_ll` viene dichiarato come:

```c
struct sockaddr_ll
{
    USHORT  sll_family;     /* Must be AF_PACKET */
    USHORT  sll_protocol;   /* LL frame type */
    INT     sll_ifindex;    /* Interface Index. */
    USHORT  sll_hatype;     /* Header type */
    UCHAR   sll_pkttype;    /* Packet type */
    UCHAR   sll_halen;      /* Length of address */
    UCHAR   sll_addr[8];    /* Physical layer address */
};
```

> [!NOTE]
> Non tutti i campi della struttura vengono usati da `sendto()` o `recvfrom()` . Vedere la descrizione seguente su come configurare per `sockaddr_ll` l'invio e la ricezione di pacchetti PPPoE.

I socket creati nella AF_PACKET possono essere usati per inviare pacchetti di individuazione PPPoE o pacchetti di sessione PPP, indipendentemente dal protocollo specificato. Quando si trasmette un pacchetto PPPoE, l'applicazione deve preparare il buffer che include il frame PPPoE formattato correttamente, incluse le intestazioni MAC (indirizzo MAC di destinazione, indirizzo MAC di origine e tipo di frame). Le dimensioni del buffer includono l'intestazione Ethernet a 14 byte.

Struct `sockaddr_ll` , utilizzato per indicare `sll_ifindex` l'interfaccia fisica da utilizzare per l'invio di questo pacchetto. Gli altri campi della struttura non vengono usati. I valori impostati per i campi inutilizzati vengono ignorati dal processo interno BSD.

Il blocco di codice seguente illustra come trasmettere un pacchetto PPPoE:

```c
struct sockaddr_ll peer_addr;

/* Transmit a PPPoE frame using the primary network interface. */
peer_addr.sll_ifindex = 0;
n = sendto(sockfd, frame, frame_size, 0, (struct
        sockaddr*)&peer_addr, sizeof(peer_addr));
```

Il valore restituito indica il numero di byte trasmessi. Poiché i pacchetti PPPoE sono basati su messaggi, in caso di trasmissione riuscita, il numero di byte inviati corrisponde alle dimensioni del pacchetto, inclusa l'intestazione Ethernet a 14 byte.

I pacchetti PPPoE possono essere ricevuti tramite `recvfrom()` . Il buffer di ricezione deve essere sufficientemente grande da contenere i messaggi con dimensioni MTU Ethernet. Il pacchetto PPPoE ricevuto include un'intestazione Ethernet a 14 byte. Alla ricezione di pacchetti PPPoE, i pacchetti di individuazione PPPoE possono essere ricevuti solo dal socket creato con il protocollo `ETHERTYPE_PPPOE_DISC` . Analogamente, i pacchetti di sessione PPP possono essere ricevuti solo dal socket creato con il protocollo `ETHERTYPE_PPPOE_SESS` . Se vengono creati più socket per lo stesso tipo di protocollo, i pacchetti PPPoE in arrivo vengono inoltrati per primi al socket creato. Se il primo socket creato per il protocollo viene chiuso, per la ricezione di questi pacchetti viene usato il socket successivo nell'ordine di creazione.

Dopo la ricezione di un pacchetto PPPoE, i campi seguenti nello `sockaddr_ll` struct sono validi:
- **sll_family:** impostata dal BSD interno per essere AF_PACKET
- **sll_ifindex**: indica l'interfaccia da cui viene ricevuto il pacchetto
- **sll_protocol**: impostare sul tipo di pacchetto ricevuto: `ETHERTYPE_PPPOE_DISC` o `ETHERTYPE_PPPOE_SESS`

## <a name="eliminating-internal-bsd-thread"></a>Eliminazione del thread BSD interno

Per impostazione predefinita, BSD usa un thread interno per eseguire parte dell'elaborazione. Nei sistemi con vincoli di memoria rigidi è possibile creare unità BSD con NX_BSD_TIMEOUT_PROCESS_IN_TIMER definito, eliminando così il thread BSD interno e utilizzando invece un timer interno per eseguire la stessa elaborazione. In questo modo si elimina la memoria necessaria per il blocco di controllo del thread BSD interno e lo stack. Tuttavia, l'elaborazione timer complessiva è notevolmente aumentata e l'elaborazione BSD può anche essere eseguita con una priorità più alta del necessario.

Per configurare i socket BSD per l'esecuzione nel contesto del timer ThreadX, NX_BSD_TIMEOUT_PROCESS_IN_TIMER in *nxd_bsd.h*. Se il livello BSD è configurato per eseguire le attività BSD nel contesto del timer, nella chiamata *a bsd_initialize* i tre parametri seguenti vengono ignorati e devono essere impostati su NULL:

- **bsd_thread_stack_area**
- **bsd_thread_stack_size**
- **bsd_thread_priority**

## <a name="netx-duo-bsd-with-dns-support"></a>NetX Duo BSD con supporto DNS

Se NX_BSD_ENABLE_DNS è definito, NetX Duo BSD può inviare query DNS per ottenere informazioni sul nome host o sull'IP dell'host. Questa funzionalità richiede che un client DNS NetX sia stato creato in precedenza usando *nx_dns_create* servizio. Uno o più indirizzi IP noti del server DNS devono essere registrati con l'istanza DNS usando il servizio *nx_dns_server_add* per l'aggiunta di indirizzi del server IPv4 o usando il *servizio nxd_dns_server_add* per l'aggiunta di indirizzi server IPv4 o IPv6.

I servizi DNS e l'allocazione di memoria vengono usati *dai servizi getaddrinfo* *e getnameinfo:*

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
        const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
        char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

Quando l'applicazione BSD chiama *getaddrinfo* con un nome host, NetX BSD chiamerà uno dei servizi seguenti per ottenere l'indirizzo IP:

- **nx_dns_ipv4_address_by_name_get**
- **nxd_dns_ipv6_address_by_name_get**
- **nx_dns_cname_get**

Per *nx_dns_ipv4_address_by_name_get* e *nxd_dns_ipv6_address_by_name_get*, NetX BSD usa rispettivamente le ipv4_addr_buffer e ipv6_addr_buffer di memoria. Le dimensioni di questi buffer sono definite rispettivamente da (NX_BSD_IPV4_ADDR_PER_HOST * 4) e (NX_BSD_IPV6_ADDR_PER_HOST * 16).

Per restituire informazioni sull'indirizzo da *getaddrinfo*, NetX BSD usa la tabella di memoria a blocchi ThreadX nx_bsd_addrinfo_pool_memory, la cui area di memoria è definita da un altro set di opzioni configurabili, NX_BSD_IPV4_ADDR_MAX_NUM e NX_BSD_IPV6_ADDR_MAX_NUM.

Per **altri dettagli sulle opzioni** di configurazione precedenti, vedere Opzioni di configurazione generali.

Inoltre, se NX_DNS_ENABLE_EXTENDED_RR_TYPES definito e l'input dell'host è un nome canonico, NetX Duo BSD alloca la memoria in modo dinamico da un pool di blocchi creato in precedenza _nx_bsd_cname_block_pool

> [!NOTE]
> Dopo aver *chiamato getaddrinfo,* l'applicazione BSD è responsabile del rilascio della memoria a cui punta l'argomento res nella tabella dei blocchi usando il *servizio freeaddrinfo.*

## <a name="netx-duo-bsd-limitations"></a>Limitazioni di NetX Duo BSD

A causa di problemi di prestazioni e architettura, NetX Duo BSD non supporta tutte le funzionalità dei socket BSD 4.3:

I flag INT non sono supportati per le chiamate *send, recv, sendto* *e recvfrom.*

## <a name="general-configuration-options"></a>Opzioni di configurazione generali

Le opzioni configurabili dall'utente in *nxd_bsd.h* consentono all'applicazione di ottimizzare i socket BSD di NetX Duo per i requisiti specifici dell'applicazione.

Di seguito è riportato l'elenco delle opzioni configurabili impostate in fase di compilazione:

- **NX_BSD_TCP_WINDOW**: usato nelle chiamate di creazione di socket TCP. 64 KB è la dimensione tipica della finestra per Ethernet da 100 Mb. Il valore predefinito è 65535.

- **NX_BSD_SOCKFD_START:** indice logico per il valore iniziale del descrittore del file socket BSD. Per impostazione predefinita, questa opzione è 32.

- **NX_BSD_MAX_SOCKETS**: specifica il numero massimo di socket totali disponibili nel livello BSD e deve essere un multiplo di 32. Il valore predefinito è 32.

- **NX_BSD_SOCKET_QUEUE_MAX**: specifica il numero massimo di pacchetti UDP archiviati nella coda del socket di ricezione. Il valore predefinito è 5.

- **NX_BSD_MAX_LISTEN_BACKLOG**: specifica le dimensioni della coda di ascolto ('backlog') per i socket TCP BSD. Il valore predefinito è 5.

- **NX_MICROSECOND_PER_CPU_TICK**: specifica il numero di microsecondi per tick del timer dell'utilità di pianificazione.

- **NX_BSD_TIMEOUT:** specifica il timeout nei tick del timer nelle chiamate interne di NetX Duo richieste da BSD. Il valore predefinito è (20 * NX_IP_PERIODIC_RATE).

- **NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT:** specifica il timeout nei tick del timer nella chiamata di disconnessione di NetX Duo. Il valore predefinito è 1.

- **NX_BSD_PRINT_ERRORS:** se impostato, il risultato dello stato di errore di una funzione BSD restituisce un numero di riga e un tipo di errore, ad esempio NX_SOC_ERROR in cui si verifica l'errore. A questo scopo, lo sviluppatore dell'applicazione deve definire l'output di debug. L'impostazione predefinita è disabilitata e non viene specificato alcun output di debug *in nxd_bsd.h.*

- **NX_BSD_TIMER_RATE:** intervallo dopo il quale viene eseguita l'attività timer periodica BSD. Il valore predefinito è 1 secondo (1 * NX_IP_PERIODIC_RATE).

- **NX_BSD_TIMEOUT_PROCESS_IN_TIMER:** se impostata, questa opzione consente l'esecuzione del processo di timeout BSD nel contesto del timer di sistema. Il comportamento predefinito è disabilitato. Questa funzionalità è descritta più dettagliatamente nel capitolo 2 "Installazione e uso di NetX Duo BSD".

- **NX_BSD_RAW_PPPOE_SUPPORT:** abilita il supporto dei pacchetti non elaborati PPPoE. Per impostazione predefinita, questa opzione non è abilitata.

- **NX_BSD_ENABLE_DNS:** se abilitata, NetX Duo BSD invierà una query DNS per un nome host o un indirizzo IP host. Richiede che un'istanza del client DNS sia stata creata e avviata in precedenza. Per impostazione predefinita, non è abilitato.

- **NX_BSD_SOCKET_RAW_PROTOCOL_TABLE_SIZE**: definisce le dimensioni della tabella socket non elaborata. Il valore deve essere una potenza di due. NetX BSD crea una matrice di socket di tipo NX_BSD_SOCKETS per l'invio e la ricezione di pacchetti non elaborati. NX_ENABLE_IP_RAW_PACKET_FILTER deve essere abilitato. Per impostazione predefinita è 32.

- **NX_BSD_IPV4_ADDR_MAX_NUM**: numero massimo di indirizzi IPv4 restituiti da *getaddrinfo*. Questo insieme a NX_BSD_IPV6_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi NetX BSD nx_bsd_addrinfo_block_pool per l'allocazione dinamica della memoria all'archiviazione delle informazioni di indirizzo in *getaddrinfo*. Il valore predefinito è 5.

- **NX_BSD_IPV6_ADDR_MAX_NUM**: numero massimo di indirizzi IPv6 restituiti da *getaddrinfo*. Questo insieme NX_BSD_IPV4_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi NetX BSD nx_bsd_addrinfo_block_pool per l'allocazione dinamica della memoria all'archiviazione delle informazioni sugli indirizzi in *getaddrinfo*.

- **NX_BSD_IPV4_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv4 archiviati per ogni query DNS. Il valore predefinito è 5.

- **NX_BSD_IPV6_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv6 archiviati per ogni query DNS. Il valore predefinito è 2.

## <a name="bsd-socket-options"></a>Opzioni socket BSD

L'elenco seguente di opzioni socket BSD di NetX Duo può essere abilitato (o disabilitato) in fase di esecuzione per ogni socket usando il *servizio setsockopt:*

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, 
                const void *option_value, INT option_length);
```

Sono disponibili due impostazioni diverse per option_level.

Il primo tipo di opzioni socket in fase di esecuzione è SOL_SOCKET per le opzioni a livello di socket. Per abilitare un'opzione a livello di socket, chiamare *setsockopt* con option_level impostato su SOL_SOCKET e option_name impostato sull'opzione specifica, ad esempio SO_BROADCAST *.* Per recuperare un'impostazione di opzione, chiamare *getsockopt* per il option_name con option_level impostato nuovamente su SOL_SOCKET.

Di seguito è riportato l'elenco delle opzioni a livello di socket in fase di esecuzione.

- **SO_BROADCAST:** se impostato, consente l'invio e la ricezione di pacchetti broadcast dai socket Netx. Questo è il comportamento predefinito per NetX Duo. Tutti i socket hanno questa funzionalità.

- **SO_ERROR**: usato per ottenere lo stato del socket nell'operazione socket precedente del socket specificato, usando il *servizio getsockopt.* Tutti i socket hanno questa funzionalità.

- **SO_KEEPALIVE:** se impostata, abilita la funzionalità Keep-Alive TCP. Ciò richiede che la libreria NetX Duo sia compilata con NX_TCP_ENABLE_KEEPALIVE definito in *nx_user.h.* Per impostazione predefinita, questa funzionalità è disabilitata.

- **SO_RCVTIMEO:** imposta l'opzione di attesa in secondi per la ricezione di pacchetti nei socket BSD di NetX Duo. Il valore predefinito è NX_WAIT_FOREVER (0xFFFFFFFF) o, se non è abilitato il blocco, NX_NO_WAIT (0x0).

- **SO_RCVBUF**: imposta le dimensioni della finestra del socket TCP. Il valore predefinito, NX_BSD_TCP_WINDOW, è impostato su 64 KB per i socket TCP BSD. Per impostare le dimensioni su 65535, è necessario che la libreria NetX Duo sia compilata con il NX_TCP_ENABLE_WINDOW_SCALING essere definito.

- **SO_REUSEADDR:** se impostata, in questo modo è possibile eseguire il mapping di più socket a una porta. L'utilizzo tipico è per il socket del server TCP. Questo è il comportamento predefinito dei socket NetX Duo.

Il secondo tipo di opzioni socket in fase di esecuzione è il livello di opzione IP. Per abilitare un'opzione del livello IP, chiamare *setsockopt* con option_level impostato su IP_PROTO e option_name impostato sull'opzione , ad esempio IP_MULTICAST_TTL *.* Per recuperare un'impostazione di opzione, chiamare *getsockopt* per il option_name con option_level impostato di nuovo su IP_PROTO.

Di seguito è riportato l'elenco delle opzioni del livello IP della fase di esecuzione.

- **IP_MULTICAST_TTL**: imposta la tempo di vita per i socket UDP. Il valore predefinito è NX_IP_TIME_TO_LIVE (0x80) quando viene creato il socket. È possibile eseguire l'override di questo valore chiamando *setsockopt con* questa opzione socket.

- **IP_RAW_IPV6_HDRINCL:** se questa opzione è impostata, l'applicazione chiamante deve aggiungere un'intestazione IPv6 e facoltativamente intestazioni dell'applicazione ai dati trasmessi su socket IPv6 non elaborati creati da BSD. Per usare questa opzione, l'elaborazione socket non elaborata deve essere abilitata nell'attività IP.

- **IP_ADD_MEMBERSHIP:** se impostata, questa opzione consente al socket BSD (si applica solo ai socket UDP) di partecipare al gruppo IGMP specificato.

- **IP_DROP_MEMBERSHIP:** se impostata, questa opzione consente al socket BSD (si applica solo ai socket UDP) di uscire dal gruppo IGMP specificato.

- **IP_HDRINCL:** se questa opzione è impostata, l'applicazione chiamante deve aggiungere l'intestazione IP e facoltativamente le intestazioni dell'applicazione ai dati trasmessi su socket IPv4 non elaborati creati in BSD. Per usare questa opzione, l'elaborazione socket non elaborata deve essere abilitata nell'attività IP.

- **IP_RAW_RX_NO_HEADER:** se deselezionata, l'intestazione IPv6 viene inclusa con i dati ricevuti per i socket IPv6 non elaborati creati in BSD. Le intestazioni IPv6 vengono rimosse per impostazione predefinita nei socket IPv6 non elaborati BSD e la lunghezza del pacchetto non include l'intestazione IPv6.

Se impostata, l'intestazione IPv4 viene rimossa dai dati ricevuti nei socket non elaborati BSD di tipo IPv4. Le intestazioni IPv4 sono incluse per impostazione predefinita nei socket IPv4 non elaborati BSD e la lunghezza del pacchetto include l'intestazione IPv4.

Questa opzione non ha effetto sui dati di trasmissione IPv4 o IPv6.

## <a name="small-ipv4-example"></a>Esempio di IPv4 di piccole dimensioni

Di seguito è descritto un esempio di come usare i servizi BSD netX Duo per le reti IPv4. In questo esempio il file di *inclusione nxd_bsd.h* viene portato alla riga 8. Successivamente, l'istanza IP *bsd_ip* pool *di* pacchetti bsd_pool vengono create come variabili globali alle righe 20 e 21. Si noti che questa demo usa un driver di rete ram (virtuale),*_nx_ram_network_driver*. In questo esempio il client e il server condivideranno lo stesso indirizzo IP nella singola istanza IP.

I thread client e server vengono creati nelle righe 62 e 68. Il pool di pacchetti BSD per la trasmissione di pacchetti viene creato alla riga 78 e usato nella creazione dell'istanza IP alla riga 87. Si noti che all'attività thread IP viene data la priorità 1 *nella nx_ip_create* chiamata. Questo thread deve essere l'attività con la priorità più alta definita nel programma per ottenere prestazioni NetX ottimali.

L'istanza IP è abilitata per i servizi ARP e TCP rispettivamente nelle righe 88 e 110. L'ultimo requisito prima che sia possibile  usare i servizi BSD è chiamare bsd_initialize alla riga 120 per configurare tutte le strutture di dati e le risorse NetX e ThreadX necessarie per BSD.

La funzione di immissione del thread del server viene definita successivamente. Il socket TCP BSD viene creato alla riga 149. L'indirizzo IP e la porta del server sono impostati sulle righe 160-163. Si noti l'uso di macro dell'ordine dei byte da host a rete *htonl* *e htons* applicate all'indirizzo IP e alla porta. Questo è conforme alla specifica del socket BSD che i dati multi byte vengono inviati ai servizi BSD nell'ordine dei byte di rete.

Successivamente, il socket del server master viene associato alla porta usando il *servizio di* associazione alla riga 166. Si tratta del socket di ascolto per le richieste di connessione TCP che usano il *servizio di* ascolto alla riga 180. Da qui la funzione del thread del server, *thread_server_entry*, esegue un ciclo per verificare la presenza di eventi di ricezione usando la chiamata *select* alla riga 202. Se un evento di ricezione è una richiesta di connessione, determinata confrontando l'elenco pronto per la lettura, chiama *accept* alla riga 213. Un socket del server figlio viene assegnato per gestire la richiesta di connessione e aggiunto all'elenco master dei socket del server TCP connessi a un client alla riga 223. Se non sono presenti nuove richieste di connessione, il thread del server verifica la presenza di eventi di ricezione in tutti i socket attualmente connessi nel ciclo for a partire dalla riga 236. Quando viene rilevato un evento di ricezione in attesa, chiama *send* e *recv* su tale socket finché non viene ricevuto alcun dato (connessione chiusa sull'altro lato) e il socket viene chiuso usando il servizio *soc_close* sulla riga 277.

Dopo aver impostato il thread del server, la funzione di immissione del thread *client, thread_client_entry,* crea un  socket alla riga 326 e si connette al socket del server TCP usando la chiamata connect alla riga 337. Esegue quindi un ciclo per inviare e ricevere pacchetti usando rispettivamente i servizi *send* *e recv.* Quando non vengono ricevuti altri dati, il socket viene chiuso alla riga 398 usando il *soc_close* dati. Dopo la disconnessione, la funzione di immissione del thread client crea un nuovo socket TCP ed effettua un'altra richiesta di connessione nel ciclo while avviato alla riga 321.

```c
/* This is a small demo of BSD Wrapper for the high-performance NetX Duo
TCP/IP stack which uses standard BSD services for TCP connection, sending,
and receiving using a simulated Ethernet driver. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nxd_bsd.h"
#include     <string.h>
#include     <stdlib.h>

#define     DEMO_STACK_SIZE     (16*1024)
#define     SERVER_PORT         87
#define     CLIENT_PORT         77

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_server;
TX_THREAD         thread_client;
NX_PACKET_POOL    bsd_pool;
NX_IP             bsd_ip;

/* Define some global data. */
CHAR     *msg0 = "Client 1:
    ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQR
    STUVWXYZ<>END";

INT     maxfd;

/* Define the counters used in the demo application... */

ULONG     error_counter;

/* Define fd_sets for the BSD server socket. */
fd_set     master_list, read_ready;

/* Define thread prototypes. */

VOID     thread_server_entry(ULONG thread_input);
VOID     thread_client_entry(ULONG thread_input);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */
int     main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{
CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create a server thread. */
    tx_thread_create(&thread_server, "Server", thread_server_entry, 0,
                    pointer, DEMO_STACK_SIZE, 8, 8, TX_NO_TIME_SLICE,
                    TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Create a Client thread. */
    tx_thread_create(&thread_client, "Client", thread_client_entry, 0,
                    pointer, DEMO_STACK_SIZE, 16, 16, TX_NO_TIME_SLICE,
                    TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a BSD packet pool. */
    status = nx_packet_pool_create(&bsd_pool, "NetX BSD Packet Pool", 128,
                                pointer, 16384);

    pointer = pointer + 16384;
    if (status)
    {
        error_counter++;
        printf("Error in creating BSD packet pool\n!");
    }

    /* Create an IP instance for BSD. */
    status = nx_ip_create(&bsd_ip, "BSD IP Instance", IP_ADDRESS(1,2,3,4),
                    0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                    pointer, 2048, 1);
                    pointer = pointer + 2048;

    if (status)
    {
        error_counter++;
        printf("Error creating BSD IP instance\n!");
    }

    /* Enable ARP and supply ARP cache memory for BSD IP Instance */
    status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable ARP \n");
    }

    /* Enable TCP processing for BSD IP instances. */
    status = nx_tcp_enable(&bsd_ip);

    /* Check TCP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable TCP \n");
    }

    /* Now initialize BSD Scoket Wrapper */
    status = bsd_initialize (&bsd_ip, &bsd_pool,pointer, 2048, 2);
}

/* Define the Server thread. */
CHAR     Server_Rcv_Buffer[100];

VOID     thread_server_entry(ULONG thread_input)
{

INT       status, sock, sock_tcp_server;
ULONG     actual_status;
INT       Clientlen;
INT       i;
UINT      is_set = NX_FALSE;
struct    sockaddr_in serverAddr;
struct    sockaddr_in ClientAddr;

    tx_thread_sleep(100);

    status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE,
        &actual_status, 100);

    /* Check status... */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Create BSD TCP Socket */
    sock_tcp_server = socket(AF_INET, SOCK_STREAM, 0);

    if (sock_tcp_server == -1)
    {
        printf("Error on Server socket %d create \n", sock_tcp_server);
        return;
    }

    printf("Server socket %d created\n", sock_tcp_server);

    /* Set the server port and IP address */
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    serverAddr.sin_port = htons(SERVER_PORT);

    /* Bind this server socket */
    status = bind (sock_tcp_server, (struct sockaddr *) &serverAddr,
                sizeof(serverAddr));

    if (status < 0)
    {
        printf("Error on Server Socket %d Bind \n", sock_tcp_server);
        return;
    }

    FD_ZERO(&master_list);
    FD_ZERO(&read_ready);
    FD_SET(sock_tcp_server,&master_list);
    maxfd = sock_tcp_server;

    /* Now listen for any client connections for this server socket */
    status = listen (sock_tcp_server, 5);
    if (status < 0)
    {
        printf("Error on Server Socket %d Listen\n", sock_tcp_server);
        return;
    }
    else
        printf("Server socket %d listen complete\n", sock_tcp_server);

    /* All set to accept client connections */

    /* Loop to create and establish server connections. */
    while(1)
    {

        printf("\n");

        read_ready = master_list;

        tx_thread_sleep(20); /* Allow some time to other threads too */

        /* Let the underlying TCP stack determine the timeout. */
        status = select(maxfd + 1, &read_ready, 0, 0, 0);

        if ((status == 0xFFFFFFFF) || (status == 0))
        {

            printf("Error with select. Status 0x%x\n", status);

            continue;
        }

        /* Check for a connection request. */
        is_set = FD_ISSET(sock_tcp_server, &read_ready);

        if(is_set)
        {

            Clientlen = sizeof(ClientAddr);

            sock = accept(sock_tcp_server,(struct sockaddr*)&ClientAddr,
                        &Clientlen);

            /* Add this new connection to our master list */
            FD_SET(sock, &master_list);

            if ( sock \maxfd)
            {

                maxfd = sock;
            }

            continue;
        }

        /* Check the set of 'ready' sockets, e.g connected to remote host and
        waiting for notice of packets received. */
        for (i = NX_BSD_SOCKFD_START; i < (maxfd+1+NX_BSD_SOCKFD_START); i++)
        {

            if ((i != sock_tcp_server) &&
                (FD_ISSET(i , &master_list)) &&
                (FD_ISSET(i , &read_ready)))
            {

                while(1)
                {

                    status = recv(i, (VOID *)Server_Rcv_Buffer, 100, 0);

                    if (status == 0)
                    {
                        printf("(Server received no data from Client on
                            socket %d)\n", i);
                        break;
                    }
                    else if (status == NX_SOC_ERROR)
                    {
                        printf("Error on Server receiving data from Client on
                            socket %d\n", i);
                        break;
                    }
                    if(status == SERVER_RCV_BUFFER_SIZE) status--;
                    Server_Rcv_Buffer[status] = 0;
                    printf("Server socket %d received %d bytes: %s\n ",
                            i, (ULONG)status, Server_Rcv_Buffer);

                    status = send(i, "Hello\n", sizeof("Hello\n"), 0);

                    if (status == NX_SOC_ERROR)
                    {
                        printf("Error on Server socket %d sending data to
                        Client\n", i);
                    }
                    else
                    {
                        printf("Server socket %d message sent to Client:
                        Hello\n", i);
                    }
                }

                /* Close this socket */
                status = soc_close(i);

                if (status != NX_SOC_ERROR)
                {
                    printf("Server socket %d closed \n", i);
                }
                else
                {
                    printf("Error on closing Server socket %d \n", i);
                }
            }
        }

    /* Loop back to check any next client connection */
    }
}

CHAR     Client_Rcv_Buffer[100];

VOID     thread_client_entry(ULONG thread_input)
{

INT        status;
INT        sock_tcp_client, length;
struct     sockaddr_in echoServAddr;
struct     sockaddr_in localAddr; /

    /* Let the server side get set up. */
    tx_thread_sleep(200);

    /* Set local port for displaying IP address and port. */
    memset(&localAddr, 0, sizeof(localAddr));
    localAddr.sin_family = AF_INET;
    localAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    localAddr.sin_port = htons(CLIENT_PORT);

    /* Set server port and IP address which we need to connect. */
    memset(&echoServAddr, 0, sizeof(echoServAddr));
    echoServAddr.sin_family = AF_INET;
    echoServAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    echoServAddr.sin_port = htons(SERVER_PORT);

    /* Now make client connections with the server. */
    while (1)
    {

        printf("\n");

        /* Create BSD TCP Socket */
        sock_tcp_client = socket( AF_INET, SOCK_STREAM, 0);

        if (sock_tcp_client == -1)
        {
            printf("Error on Client socket %d create \n", sock_tcp_client);
            return;
        }

        printf("Client socket %d created\n", sock_tcp_client);

        /* Now connect this client to the server */
        status = connect(sock_tcp_client, (struct sockaddr *)&echoServAddr,
                        sizeof(echoServAddr));

        /* Check for error. */
        if (status != OK)
        {
            printf("Error on Client socket %d connect\n", sock_tcp_client);
                    soc_close(sock_tcp_client);
            return;
        }

        /* Get and print source and destination information */
        printf("Client socket %d connected \n", sock_tcp_client);

        status = getsockname(sock_tcp_client, (struct sockaddr *)&localAddr,
                            &length);

        printf("Client port = %lu , Client = 0x%x,",
            htonl(localAddr.sin_port), htonl(localAddr.sin_addr.s_addr));

        length = sizeof(struct sockaddr_in);

        status = getpeername( sock_tcp_client, (struct sockaddr *)
                            &echoServAddr, &length);

        printf("Remote port = %lu, Remote IP = 0x%x \n",
                htonl(echoServAddr.sin_port),
                htonl(echoServAddr.sin_addr.s_addr));

        /* Now receive the echoed packet from the server */
        while(1)
        {

            printf("Client sock %d sending packet to server\n",
            sock_tcp_client);

            status = send(sock_tcp_client, "Hello", (sizeof("Hello")), 0);

            if (status == ERROR)
            {
                printf("Error: Client Socket (%d) send \n", sock_tcp_client);
            }
            else
            {
                printf("Client socket %d sent message Hello\n",
                        sock_tcp_client);
            }

            status = recv(sock_tcp_client, (VOID *)Client_Rcv_Buffer,100,0);

            if (status <= 0)
            {

                if (status < 0)
                {
                    380 printf("Error on Client receiving on socket %d \n",
                            sock_tcp_client);
                }
                else
                {
                    printf("Nothing received by Client on socket %d\n",
                            sock_tcp_client);
                }

                break;
            }
            else
            {
                printf("Client socket %d received %d bytes: %s\n",
                        sock_tcp_client,
                        status, Client_Rcv_Buffer);
            }

        }

        /* close this client socket */
        status = soc_close(sock_tcp_client);

        if (status != ERROR)
        {
            printf("Client Socket %d closed\n", sock_tcp_client);
        }
        else
        {
            printf("Error on Client Socket %d on close \n", sock_tcp_client);
        }

        /* Make another Client connection...*/

    }
}
```

## <a name="small-ipv6-example-system"></a>Piccolo sistema di esempio IPv6

Un esempio di come usare i servizi BSD netX Duo per reti IPv6 è descritto nel programma seguente. Questo esempio è molto simile al programma demo IPv4 descritto in precedenza con alcune importanti differenze.

I thread client e server, il pool di pacchetti BSD, l'istanza IP e l'inizializzazione BSD si verificano come per i socket BSD IPv4.

Nella funzione di immissione del thread del server, *thread_server_entry*, definisce un paio di variabili IPv6 usando i tipi di dati *sockaddr_in6* e *NXD_ADDRESS* sulle righe 145-148. Il NXD_ADDRESS di dati può effettivamente archiviare sia i tipi di indirizzo IPv4 che IPv6.

Successivamente, il thread del server abilita IPv6 e ICMPv6 nell'istanza IP usando il *servizio nxd_ipv6_enable* *e nxd_icmpv6_enable* rispettivamente nella riga 161 e 169. Successivamente, gli indirizzi IP locali e globali del collegamento vengono registrati con l'istanza IP. Questa operazione viene eseguita usando *il nxd_ipv6_address_set* nelle righe 180 e 195. L'attività del thread IP viene quindi sufficientemente lunga da completare il protocollo  di rilevamento degli indirizzi duplicati e registrare questi indirizzi come indirizzi validi nella chiamata tx_thread_sleep alla riga 201.

Successivamente, il socket del server TCP viene creato con l'argomento AF_INET6 di input del tipo di socket alla riga 204. L'indirizzo e la porta IPv6 del socket sono impostati sulle righe 216-221, anche in questo caso notando l'uso di macro *htonl* e *htons* per inserire i dati nell'ordine dei byte di rete per i servizi socket BSD. Da qui in avanti, la funzione di immissione del thread del server è praticamente identica all'esempio IPv4.

La funzione di immissione del thread *client, thread_client_entry*, viene definita successivamente. Si noti che poiché il client TCP in questo esempio condivide la stessa istanza IP e lo stesso indirizzo IPv6 del server TCP, non è necessario abilitare nuovamente i servizi IPv6 o ICMPv6 nell'istanza IP. Inoltre, anche l'indirizzo IPv6 è già registrato con l'istanza IP. Al contrario, la funzione di immissione del thread client attende semplicemente la riga 368 per la configurazione del server. L'indirizzo del server e la porta vengono impostati, usando le macro dell'ordine dei byte da host a rete sulle righe 387-392 e quindi il client può connettersi al server TCP alla riga 412. Si noti che i tipi di dati dell'indirizzo IP locale nelle righe 378-383 vengono usati solo per illustrare i servizi *getsockname* e *getpeername* rispettivamente nelle righe 425 e 434. Poiché i dati vengono provenienti dalla rete, la rete deve ospitare macro per l'ordine dei byte usate nelle righe 378-383.

Successivamente, la funzione di immissione thread client entra in un ciclo in cui crea un socket TCP, crea una connessione TCP e invia e riceve dati con il server TCP fino a quando non vengono ricevuti altri dati praticamente uguali all'esempio IPv4. Chiude quindi il socket alla riga 483, sospende brevemente e crea un altro socket TCP e richiede una connessione al server TCP.

Una differenza importante con l'esempio IPv4 è che le chiamate *socket* specificano un socket IPv6 usando l'AF_INET6 di input. Un'altra differenza importante è che la chiamata *tcp* client *connect* accetta un tipo di dati sockaddr_in6 e un argomento di lunghezza impostato sulla dimensione del sockaddr_in6 *dati.*

```c
/* This is a small demo of BSD Wrapper for the high-performance NetX Duo
TCP/IP stack which uses standard BSD services for TCP connection,
disconnection, sending, and receiving using a simulated Ethernet driver. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nxd_bsd.h"
#include     <string.h>
#include     <stdlib.h>

#define     DEMO_STACK_SIZE     (16*1024)
#define     SERVER_PORT         87
#define     CLIENT_PORT         77

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_server;
TX_THREAD         thread_client;
NX_PACKET_POOL    bsd_pool;
NX_IP             bsd_ip;

/* Define some global data. */
CHAR     *msg0 = "Client 1:
    ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>END";

INT     maxfd;

/* Define the counters used in the demo application... */
ULONG     error_counter;

/* Define fd_sets for the BSD server socket. */
fd_set     master_list, read_ready;

/* Define thread prototypes. */
VOID     thread_server_entry(ULONG thread_input);
VOID     thread_client_entry(ULONG thread_input);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

int     main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void tx_application_define(void *first_unused_memory)
{
CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create a server thread. */
    tx_thread_create(&thread_server, "Server", thread_server_entry, 0,
                    pointer, DEMO_STACK_SIZE, 8, 8,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Create a Client thread. */
    tx_thread_create(&thread_client, "Client", thread_client_entry, 0,
                    pointer, DEMO_STACK_SIZE, 16, 16,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a BSD packet pool. */
    status = nx_packet_pool_create(&bsd_pool, "NetX BSD Packet Pool",
    128, pointer, 16384);

    pointer = pointer + 16384;

    if (status)
    {
        error_counter++;
        printf("Error in creating BSD packet pool\n!");
    }

    /* Create an IP instance for BSD. */
    status = nx_ip_create(&bsd_ip, "BSD IP Instance", IP_ADDRESS(1,2,3,4),
                        0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                        pointer, 2048, 1);
                        pointer = pointer + 2048;

    if (status)
    {
        error_counter++;
        printf("Error creating BSD IP instance\n!");
    }

    /* Enable ARP and supply ARP cache memory for BSD IP Instance */
    status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in enable ARP on BSD IP instance\n");
    }

    /* Enable TCP processing for BSD IP instances. */
    status = nx_tcp_enable(&bsd_ip);

    /* Check TCP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable TCP \n");
    }

    /* Now initialize BSD Scoket Wrapper */
    status = bsd_initialize(&bsd_ip, &bsd_pool,pointer, 2048, 2);

    /* Check BSD initialize status. */
    if (status)
    {
        error_counter++;
        printf("Error in BSD initialize \n");
    }

    pointer = pointer + 2048;
}

/* Define the Server thread. */
CHAR     Server_Rcv_Buffer[100];

VOID     thread_server_entry(ULONG thread_input)
{

INT             status, sock, sock_tcp_server;
ULONG           actual_status;
INT             Clientlen;
INT             i;
UINT            is_set = NX_FALSE;
NXD_ADDRESS     ip_address;
struct          sockaddr_in6 serverAddr;
struct          sockaddr_in6 ClientAddr;
UINT            iface_index, address_index;

    status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE,
            &actual_status, 100);

    /* Check status... */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable IPv6 */
    status = nxd_ipv6_enable(&bsd_ip);
    if((status != NX_SUCCESS) && (status != NX_ALREADY_ENABLED))
    {
        printf("Error with IPv6 enable 0x%x\n", status);
        return;
    }

    /* Enable ICMPv6 */
    status = nxd_icmp_enable(&bsd_ip);

    if(status)
    {
        printf("Error with ECMPv6 enable 0x%x\n", status);
        return;
    }

    /* Set the primary interface for our DNS IPv6 addresses. */
    iface_index = 0;

    /* This assumes we are using the primary network interface (index 0). */
    status = nxd_ipv6_address_set(&bsd_ip, iface_index, NX_NULL, 10,
                                &address_index);

    if (status)
        return;

    /* Set ip_0 interface address. */
    ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    ip_address.nxd_ip_address.v6[0] = htonl(0x20010db8);
    ip_address.nxd_ip_address.v6[1] = htonl(0x0000f101);
    ip_address.nxd_ip_address.v6[2] = 0;
    ip_address.nxd_ip_address.v6[3] = htonl(0x101);

    /* Set the host global IP address. We are assuming a 64
    bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&bsd_ip, iface_index, &ip_address, 64,
                                &address_index);

    if (status)
        return;

    /* Wait for IPv6 stack to finish DAD process. */
    tx_thread_sleep(400);

    /* Create BSD TCP Socket */
    sock_tcp_server = socket(AF_INET6, SOCK_STREAM, 0);

    if (sock_tcp_server == -1)
    {
        printf("\nError: BSD TCP Server socket create \n");
        return;
    }

    printf("\nBSD TCP Server socket created %lu \n", sock_tcp_server);

    /* Set the server port and IP address */
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    serverAddr.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    serverAddr.sin6_addr._S6_un._S6_u32[2] = 0x0;
    serverAddr.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    serverAddr.sin6_port = htons(SERVER_PORT);
    serverAddr.sin6_family = AF_INET6;

    /* Bind this server socket */
    status = bind(sock_tcp_server, (struct sockaddr *) &serverAddr,
                    sizeof(serverAddr));

    if (status < 0)
    {
        printf("Error: Server Socket Bind \n");
        return;
    }

    FD_ZERO(&master_list);
    FD_ZERO(&read_ready);
    FD_SET(sock_tcp_server,&master_list);
    maxfd = sock_tcp_server;

    /* Now listen for any client connections for this server socket */
    status = listen(sock_tcp_server, 5);
    if (status < 0)
    {
        printf("Error: Server Socket Listen\n");
        return;
    }
    else
        printf("Server Listen complete\n");

    /* All set to accept client connections */
    printf("Now accepting client connections\n");

    /* Loop to create and establish server connections. */
    while(1)
    {

        printf("\n");

        read_ready = master_list;

        tx_thread_sleep(20); /* Allow some time to other threads too */

        /* Let the underlying TCP stack determine the timeout. */
        status = select(maxfd + 1, &read_ready, 0, 0, 0);

        if ( (status == 0xFFFFFFFF) || (status == 0) )
        {
            printf("Error with select? Status 0x%x. Try again\n", status);

            continue;
        }

        /* Detected a connection request. */
        is_set = FD_ISSET(sock_tcp_server,&read_ready);

        if(is_set)
        {

            Clientlen = sizeof(ClientAddr);

            sock = accept(sock_tcp_server,
            (struct sockaddr*)&ClientAddr,
            &Clientlen);

            /* Add this new connection to our master list */
            FD_SET(sock, &master_list);

            if ( sock \maxfd)
            {
                printf("New connection %d\n", sock);

                maxfd = sock;
            }

            continue;
        }

        /* Check the set of 'ready' sockets, e.g connected to remote host and
        waiting for notice of packets received. */
        for (i = NX_BSD_SOCKFD_START; i < (maxfd+1+NX_BSD_SOCKFD_START); i++)
        {

            if ((i != sock_tcp_server) &&
                (FD_ISSET(i, &master_list)) &&
                (FD_ISSET(i, &read_ready)))
            {

                while(1)
                {

                    status = recv(i, (VOID *)Server_Rcv_Buffer, 100, 0);

                    if (status == 0)
                    {
                        printf("(Server socket %d received no data from
                                Client)\n", i);

                        break;
                    }
                    else if (status == 0xFFFFFFFF)
                    {
                        printf("Error on Server socket %d receiving data from
                                Client\n", i);

                        break;
                    }

                    printf("Server socket %d received from Client %lu bytes:
                            %s\n ", i, (ULONG)status,
                            Server_Rcv_Buffer);

                    status = send(i, "Hello\n", sizeof("Hello\n"), 0);

                    if (status == ERROR)
                    {
                        printf("Error on Server socket %d sending data to
                                Client \n", i);
                    }
                    else
                    {
                        printf("Server socket %d message sent to Client:
                                Hello\n", i);
                    }
                }

                /* Close this socket */
                status = soc_close(i);

                if (status != ERROR)
                {
                    printf("Server socket %d closing\n", i);
                }
                else
                {

                    printf("Error on Server socket %d closing\n", i);
                }
            }
        }

        /* Loop back to check any next client connection */
    }
}

#define     CLIENT_BUFFER_SIZE 100
CHAR        Client_Rcv_Buffer[CLIENT_BUFFER_SIZE];

VOID        thread_client_entry(ULONG thread_input)
{

INT         status;
INT         sock_tcp_client, length;
struct      sockaddr_in6 echoServAddr6;
struct      sockaddr_in6 localAddr6; address */

    /* Wait for the server side to get set up, including the DAD process. */
    tx_thread_sleep(500);

    /* ICMPv6 and IPv6 should already be enabled on the IP instance
    by the server thread entry function. */

    /* Further the IPv6 address is already established with the IP instance.
    so no need to wait for DAD completion. */

    /* Set local port and IP address (used only for getsockname call). */
    memset(&localAddr6, 0, sizeof(localAddr6));
    localAddr6.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    localAddr6.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    localAddr6.sin6_addr._S6_un._S6_u32[2] = 0x0;
    localAddr6.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    localAddr6.sin6_port = htons(CLIENT_PORT);
    localAddr6.sin6_family = AF_INET6;

    /* Set Server port and IP address to connect to the TCP server. */
    memset(&echoServAddr6, 0, sizeof(echoServAddr6));
    echoServAddr6.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    echoServAddr6.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    echoServAddr6.sin6_addr._S6_un._S6_u32[2] = 0x0;
    echoServAddr6.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    echoServAddr6.sin6_port = htons(SERVER_PORT);
    echoServAddr6.sin6_family = AF_INET6;

    /* Now make client connections with the server. */
    while (1)
    {
        printf("\n");

        /* Create BSD TCP Socket */

        sock_tcp_client = socket(AF_INET6, SOCK_STREAM, 0);

        if (sock_tcp_client == -1)
        {
            printf("Error on Client socket %d create \n");
            return;
        }

        printf("Client socket %d created \n", sock_tcp_client);

        /* Now connect this client to the server */
        status = connect(sock_tcp_client, (struct sockaddr *)&echoServAddr6,
                sizeof(echoServAddr6));

        /* Check for error. */
        if (status != NX_SOC_OK)
        {
            printf("Error on Client socket %d connect\n");
            soc_close(sock_tcp_client);
            return;

        }

        /* Get and print source and destination information */
        printf("Client socket %d connected \n", sock_tcp_client);

        status = getsockname(sock_tcp_client, (struct sockaddr *)&localAddr6,
        &length);

        printf("Client port = %lu , Client = 0x%x 0x%x 0x%x 0x%x,",
                ntohs(localAddr6.sin6_port),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[0]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[1]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[2]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[3]));

        length = sizeof(struct sockaddr_in6);

        status = getpeername(sock_tcp_client, (struct sockaddr *)
                            &echoServAddr6, &length);

        printf("Remote port = %lu, Remote IP = 0x%x 0x%x 0x%x 0x%x \n",
                ntohs(echoServAddr6.sin6_port),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[0]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[1]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[2]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[3]));

        /* Now receive the echoed packet from the server */
        while(1)
        {

            printf("Client sock %d sending packet to server\n",
                sock_tcp_client);

            status = send(sock_tcp_client, "Hello", sizeof("Hello"), 0);

            if (status == NX_SOC_ERROR)
            {
                printf("Error on Client Socket (%d) send \n",
                        sock_tcp_client);
            }
            else
            {
                printf("Client socket %d sent message: Hello\n",
                        sock_tcp_client);
            }

            status = recv(sock_tcp_client, (VOID *)Client_Rcv_Buffer,
                        CLIENT_BUFFER_SIZE, 0);

            if (status <= 0)
            {

                if (status < 0)
                {
                    printf("Error on Client receiving on socket %d \n",
                            sock_tcp_client);
                }
                else
                {
                    printf("Client received no data on socket %d\n",
                            sock_tcp_client);
                }

            break;
            }
            else
            {
                printf("Client socket %d received %d bytes and this message:
                        %s\n", sock_tcp_client, status,
                        Client_Rcv_Buffer);
            }

        }

        /* close this client socket */
        status = oc_close(sock_tcp_client);

        if (status != NX_SOC_ERROR)
        {
            printf("Client Socket %d closed\n", sock_tcp_client);
        }
        else
        {
            printf("Error on Client Socket %d on close \n", sock_tcp_client);
        }

        /* Make another Client connection...*/

    }
}
```
