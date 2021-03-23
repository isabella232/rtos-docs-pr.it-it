---
title: Capitolo 2-installazione e uso di Azure RTO NetX Duo BSD
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente BSD di Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 582661bc66c51341fc098de9ff7b6fa2a7d746de
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822058"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-bsd"></a>Capitolo 2-installazione e uso di Azure RTO NetX Duo BSD

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente BSD di Azure RTO NetX Duo.

## <a name="product-distribution"></a>Distribuzione del prodotto

È possibile ottenere Azure RTO NetX Duo BSD dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nxd_bsd. h**: file di intestazione per NETX Duo BSD
- **nxd_bsd. c**: file di origine c per NETX Duo BSD
- **nxd_bsd.pdf**: manuale dell'utente per NETX Duo BSD

File demo:

- **bsd_demo_udp. c**
- **bsd_demo_tcp. c**
- **bsd_demo_raw. c**

## <a name="netx-duo-bsd-installation"></a>Installazione di NetX Duo BSD

Per usare NetX Duo BSD, l'intera distribuzione citata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_bsd. h* e *nxd_bsd. c* devono essere copiati in questa directory.

## <a name="building-the-threadx-and-netx-duo-components-of-a-bsd-application"></a>Compilazione dei componenti ThreadX e NetX duo di un'applicazione BSD

### <a name="threadx"></a>ThreadX

La libreria ThreadX deve definire `bsd_errno` nell'archiviazione locale di thread. Si consiglia la seguente procedura:

1. In *tx_port. h*, impostare una delle macro TX_THREAD_EXTENSION come indicato di seguito:
   - `#define TX_THREAD_EXTENSION_3     int bsd_errno`

1. Ricompilare la libreria ThreadX.

> [!NOTE]
> Se TX_THREAD_EXTENSION_3 è già in uso, l'utente è libero di usare una delle altre macro TX_THREAD_EXTENSION.

### <a name="netx-duo"></a>NetX Duo

Prima di usare NetX Duo BSD Services, è necessario compilare la libreria NetX Duo con NX_ENABLE_EXTENDED_NOTIFY_SUPPORT definito. Per impostazione predefinita, non è definito. Se è necessario usare i socket raw BSD, è necessario compilare la libreria NetX Duo con NX_ENABLE_IP_RAW_PACKET_FILTER definito.

## <a name="using-netx-duo-bsd"></a>Uso di NetX Duo BSD

Un progetto di applicazione NetX Duo BSD deve includere *nxd_bsd. h* dopo aver incluso *tx_api. h* e *nx_api. h* per poter usare i servizi BSD specificati più avanti in questa guida. Nell'applicazione deve inoltre essere incluso *nxd_bsd. c* nel processo di compilazione. Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX Duo BSD.

Per usare i servizi BSD di NetX Duo, l'applicazione deve creare un'istanza IP, creare un pool di pacchetti per il livello BSD da cui allocare i pacchetti, allocare spazio di memoria per lo stack dei thread BSD interno e specificare la priorità del thread BSD interno. Il livello BSD viene inizializzato chiamando *bsd_initialize* e passando i parametri. Questa procedura è illustrata in "piccoli esempi" più avanti in questo documento, ma il prototipo è illustrato di seguito:

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                    *CHAR *bsd_thread_stack_area,
                    *ULONG bsd_thread_stack_size,
                    *UINT bsd_thread_priority*);
```

Il default_ip è l'istanza IP su cui opera il livello BSD. Il default_pool viene usato dai servizi BSD per allocare pacchetti da. I due parametri successivi: bsd_thread_stack_area, bsd_thread_stack_size definisce l'area dello stack utilizzata dal thread BSD interno e l'ultimo parametro, bsd_thread_priority, imposta la priorità del thread.

## <a name="netx-duo-bsd-raw-socket-support"></a>Supporto di socket raw NetX Duo BSD

NetX Duo BSD supporta anche i socket non elaborati. Per usare i socket non elaborati in NetX Duo BSD, è necessario compilare la libreria NetX Duo con NX_ENABLE_IP_RAW_PACKET_FILTER definito. Per impostazione predefinita, non è definito. L'applicazione deve quindi abilitare l'elaborazione socket non elaborata per un'istanza di IP creata in precedenza chiamando *nx_ip_raw_packet_enable.*

Per creare un socket non elaborato in NetX Duo BSD, l'applicazione usa il *socket* di creazione del servizio socket e specifica la famiglia di protocolli, il tipo di socket e il protocollo:

```c
sock_1 = socket(INT protocolFamily, INT socket_type, INT protocol)
```

protocolFamily è AF_INET per i socket IPv4 o AF_INET6 per i socket IPv6, supponendo che IPv6 sia abilitato nell'istanza IP. Il socket_type deve essere impostato su SOCK_RAW. il protocollo è specifico dell'applicazione.

Per inviare e ricevere pacchetti non elaborati, nonché chiudere un socket non elaborato, l'applicazione usa in genere gli stessi servizi BSD di UDP, ad esempio *SendTo, recvfrom, Select* e *soc_close*. I socket non elaborati non supportano i servizi BSD *Accept* o *Listen* .

- Per impostazione predefinita, i dati non elaborati IPv4 ricevuti includono l'intestazione IPv4.  Viceversa, i dati non elaborati IPv6 ricevuti non includono l'intestazione IPv6.

- Per impostazione predefinita, quando si inviano pacchetti IPv6 o IPv4 non elaborati, il livello wrapper BSD aggiunge l'intestazione IPv6 o IPv4 prima di inviare i dati.

NetX Duo BSD supporta opzioni di socket non elaborate aggiuntive, tra cui IP_RAW_RX_NO_HEADER, IP_HDRINCL e IP_RAW_IPV6_HDRINCL.

Se IP_RAW_RX_NO_HEADER è impostato, l'intestazione IPv4 viene rimossa in modo che i dati ricevuti non contengano l'intestazione IPv4 e la lunghezza del messaggio segnalata non includa l'intestazione IPv4.  Per i socket IPv6, per impostazione predefinita la ricezione del socket non elaborato non include l'intestazione IPv6, equivalente al set di opzioni IP_RAW_RX_NO_HEADER. È possibile che l'applicazione utilizzi il servizio *setsockopt* per deselezionare l'opzione IP_RAW_RX_NO_HEADER, una volta deselezionata l'opzione IP_RAW_RX_NO_HEADER, i dati non elaborati IPv6 ricevuti includono l'intestazione IPv6 e la lunghezza del messaggio segnalata include l'intestazione IPv6.

Questa opzione non ha alcun effetto sui dati trasmessi IPv4 o IPv6.

Se IP_HDRINCL è impostato, l'applicazione include l'intestazione IPv4 quando si inviano i dati.  Questa opzione non ha alcun effetto sulla trasmissione IPv6 e non è definita per impostazione predefinita. Se IP_RAW_IPV6_HDRINCL è impostato, l'applicazione include l'intestazione IPv6 quando si inviano i dati.  Questa opzione non ha alcun effetto sulla trasmissione IPv4 e non è definita per impostazione predefinita.

IP_HDRINCL e IP_RAW_IPV6_HDRINCL non hanno alcun effetto sulla ricezione IPv4 o IPv6.

> [!NOTE]
> La specifica del socket BSD 4,3 specifica che il kernel deve copiare il pacchetto non elaborato in ogni buffer di ricezione del socket. Tuttavia, in NetX Duo BSD, se vengono creati più socket che condividono lo stesso protocollo, il comportamento non è definito.

## <a name="netx-duo-bsd-raw-packet-support"></a>Supporto per pacchetti RAW NetX Duo BSD

Per abilitare il supporto dei pacchetti non elaborati per PPPoE, è necessario compilare il wrapper NetX Duo BSD con NX_BSD_RAW_PPPOE_SUPPORT abilitato.

Il comando seguente crea un socket BSD per gestire i pacchetti non elaborati PPPoE:

```c
Sockfd = socket(AF_PACKET, SOCK_RAW, protocol);
```

L'implementazione corrente di BSD supporta solo due tipi di protocollo nella famiglia di AF_PACKET

- `ETHERTYPE_PPPOE_DISC`: Pacchetti di individuazione PPPoE. Nel frame di dati MAC, i pacchetti di individuazione hanno il tipo di frame Ethernet 0x8863.

- `ETHERTYPE_PPPOE_SESS`: Pacchetti della sessione PPP. Nel frame di dati MAC, i pacchetti di sessione hanno il tipo di frame Ethernet 0x8864.

La struttura `sockaddr_ll` viene utilizzata per specificare i parametri durante l'invio o la ricezione di frame PPPoE.

`struct sockaddr_ll` viene dichiarata come:

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
> Non tutti i campi della struttura vengono utilizzati da `sendto()` o `recvfrom()` . Vedere la descrizione seguente per informazioni su come configurare `sockaddr_ll` per l'invio e la ricezione di pacchetti PPPoE.

Il socket creato nella famiglia di AF_PACKET può essere usato per inviare pacchetti di individuazione PPPoE o pacchetti di sessioni PPP, indipendentemente dal protocollo specificato. Quando si trasmette un pacchetto PPPoE, l'applicazione deve preparare il buffer che include il frame PPPoE correttamente formattato, incluse le intestazioni MAC (indirizzo MAC di destinazione, indirizzo MAC di origine e tipo di frame). La dimensione del buffer include l'intestazione Ethernet a 14 byte.

Lo `sockaddr_ll` struct `sll_ifindex` viene usato per indicare l'interfaccia fisica da usare per l'invio del pacchetto. Il resto dei campi nella struttura non viene utilizzato. I valori impostati sui campi non usati vengono ignorati dal processo interno di BSD.

Il blocco di codice seguente illustra come trasmettere un pacchetto PPPoE:

```c
struct sockaddr_ll peer_addr;

/* Transmit a PPPoE frame using the primary network interface. */
peer_addr.sll_ifindex = 0;
n = sendto(sockfd, frame, frame_size, 0, (struct
        sockaddr*)&peer_addr, sizeof(peer_addr));
```

Il valore restituito indica il numero di byte trasmessi. Poiché i pacchetti PPPoE sono basati su messaggi, in una trasmissione corretta, il numero di byte inviati corrisponde alla dimensione del pacchetto, inclusa l'intestazione Ethernet a 14 byte.

I pacchetti PPPoE possono essere ricevuti tramite `recvfrom()` . Il buffer di ricezione deve essere sufficientemente grande da contenere il messaggio di dimensioni MTU Ethernet. Il pacchetto PPPoE ricevuto include l'intestazione Ethernet a 14 byte. Alla ricezione di pacchetti PPPoE, i pacchetti di individuazione PPPoE possono essere ricevuti solo dal socket creato con il protocollo `ETHERTYPE_PPPOE_DISC` . Analogamente, i pacchetti di sessione PPP possono essere ricevuti solo dal socket creato con il protocollo `ETHERTYPE_PPPOE_SESS` . Se vengono creati più socket per lo stesso tipo di protocollo, i pacchetti PPPoE in arrivo vengono inoltrati al socket creato per primo. Se il primo socket creato per il protocollo viene chiuso, il socket successivo nell'ordine di creazione viene usato per la ricezione di questi pacchetti.

Dopo la ricezione di un pacchetto PPPoE, i campi seguenti nello `sockaddr_ll` struct sono validi:
- **sll_family**: impostato dall'interno BSD da AF_PACKET
- **sll_ifindex**: indica l'interfaccia da cui viene ricevuto il pacchetto
- **sll_protocol**: impostare sul tipo di pacchetto ricevuto: `ETHERTYPE_PPPOE_DISC` o `ETHERTYPE_PPPOE_SESS`

## <a name="eliminating-internal-bsd-thread"></a>Eliminazione del thread BSD interno

Per impostazione predefinita, BSD utilizza un thread interno per eseguire parte dell'elaborazione. Nei sistemi con vincoli di memoria limitati, BSD può essere compilato con NX_BSD_TIMEOUT_PROCESS_IN_TIMER definito, che elimina il thread BSD interno e usa invece un timer interno per eseguire la stessa elaborazione. In questo modo si elimina la memoria necessaria per il blocco e lo stack di controllo dei thread BSD interni. Tuttavia, l'elaborazione del timer complessiva è significativamente aumentata e anche l'elaborazione BSD può essere eseguita con una priorità più alta del necessario.

Per configurare i socket BSD per l'esecuzione nel contesto del timer ThreadX, definire NX_BSD_TIMEOUT_PROCESS_IN_TIMER in *nxd_bsd. h*. Se il livello BSD è configurato per eseguire le attività BSD nel contesto del timer, nella chiamata a *bsd_initialize* i tre parametri seguenti vengono ignorati e devono essere impostati su null:

- **bsd_thread_stack_area**
- **bsd_thread_stack_size**
- **bsd_thread_priority**

## <a name="netx-duo-bsd-with-dns-support"></a>NetX Duo BSD con supporto DNS

Se NX_BSD_ENABLE_DNS è stato definito, NetX Duo BSD può inviare query DNS per ottenere informazioni sul nome host o sull'indirizzo IP dell'host. Questa funzionalità richiede che un client DNS NetX venga creato in precedenza usando il servizio *nx_dns_create* . Uno o più indirizzi IP del server DNS noti devono essere registrati con l'istanza DNS utilizzando il servizio *nx_dns_server_add* per aggiungere indirizzi server IPv4 o utilizzando il servizio *nxd_dns_server_add* per aggiungere indirizzi server IPv4 o IPv6.

I servizi DNS e l'allocazione di memoria vengono usati dai servizi *funzione getaddrinfo* e *GetNameInfo* :

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
        const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
        char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

Quando l'applicazione BSD chiama *funzione getaddrinfo* con un nome host, NETX BSD chiamerà uno dei servizi seguenti per ottenere l'indirizzo IP:

- **nx_dns_ipv4_address_by_name_get**
- **nxd_dns_ipv6_address_by_name_get**
- **nx_dns_cname_get**

Per *nx_dns_ipv4_address_by_name_get* e *NXD_DNS_IPV6_ADDRESS_BY_NAME_GET*, NETX BSD USA rispettivamente le aree di memoria ipv4_addr_buffer e ipv6_addr_buffer. Le dimensioni di questi buffer sono definite rispettivamente da (NX_BSD_IPV4_ADDR_PER_HOST * 4) e (NX_BSD_IPV6_ADDR_PER_HOST * 16).

Per restituire le informazioni sull'indirizzo da *funzione getaddrinfo*, NETX BSD usa la tabella di memoria a blocchi threadX nx_bsd_addrinfo_pool_memory, la cui area di memoria è definita da un altro set di opzioni configurabili, NX_BSD_IPV4_ADDR_MAX_NUM e NX_BSD_IPV6_ADDR_MAX_NUM.

Per ulteriori informazioni sulle opzioni di configurazione precedenti, vedere **Opzioni di configurazione generali** .

Inoltre, se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito e l'input dell'host è un nome canonico, NetX Duo BSD allocherà la memoria dinamicamente da un pool di blocchi creato in precedenza ' _nx_bsd_cname_block_pool

> [!NOTE]
> Dopo la chiamata a *funzione getaddrinfo* , l'applicazione BSD è responsabile del rilascio della memoria a cui fa riferimento l'argomento res alla tabella dei blocchi usando il servizio *FreeAddrInfo* .

## <a name="netx-duo-bsd-limitations"></a>Limitazioni di NetX Duo BSD

A causa di problemi relativi alle prestazioni e all'architettura, NetX Duo BSD non supporta tutte le funzionalità socket di BSD 4,3:

I flag INT non sono supportati per le chiamate *Send, ricezione, SendTo* e *recvfrom* .

## <a name="general-configuration-options"></a>Opzioni di configurazione generali

Le opzioni configurabili dall'utente in *nxd_bsd. h* consentono all'applicazione di ottimizzare i socket NETX Duo BSD per i requisiti specifici dell'applicazione.

Di seguito è riportato l'elenco delle opzioni configurabili impostate in fase di compilazione:

- **NX_BSD_TCP_WINDOW**: utilizzato nelle chiamate di creazione socket TCP. 64K è la tipica dimensione della finestra per Ethernet 100Mb. Il valore predefinito è 65535.

- **NX_BSD_SOCKFD_START**: si tratta dell'indice logico per il valore iniziale del descrittore del file socket BSD. Per impostazione predefinita, questa opzione è 32.

- **NX_BSD_MAX_SOCKETS**: specifica il numero massimo di socket totali disponibili nel livello BSD e deve essere un multiplo di 32. Per impostazione predefinita, il valore è 32.

- **NX_BSD_SOCKET_QUEUE_MAX**: specifica il numero massimo di pacchetti UDP archiviati nella coda del socket di ricezione. Il valore predefinito è 5.

- **NX_BSD_MAX_LISTEN_BACKLOG**: specifica le dimensioni della coda di ascolto (' backlog ') per i socket TCP BSD. Il valore predefinito è 5.

- **NX_MICROSECOND_PER_CPU_TICK**: specifica il numero di microsecondi per ogni segno di timer dell'utilità di pianificazione.

- **NX_BSD_TIMEOUT**: specifica il timeout nei cicli del timer per le chiamate interne NETX Duo richieste da BSD. Il valore predefinito è (20 * NX_IP_PERIODIC_RATE).

- **NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: specifica il timeout nei cicli del timer per la chiamata di disconnessione NETX Duo. Il valore predefinito è 1.

- **NX_BSD_PRINT_ERRORS**: se impostato, lo stato di errore restituito da una funzione BSD restituisce un numero di riga e il tipo di errore, ad esempio NX_SOC_ERROR in cui si è verificato l'errore. A questo scopo, lo sviluppatore dell'applicazione deve definire l'output di debug. L'impostazione predefinita è disabilitata e non è stato specificato alcun output di debug in *nxd_bsd. h*.

- **NX_BSD_TIMER_RATE**: intervallo dopo il quale viene eseguita l'attività del timer periodico BSD. Il valore predefinito è 1 secondo (1 * NX_IP_PERIODIC_RATE).

- **NX_BSD_TIMEOUT_PROCESS_IN_TIMER**: se impostata, questa opzione consente l'esecuzione del processo di timeout di BSD nel contesto del timer di sistema. Il comportamento predefinito è Disabled. Questa funzionalità è descritta in modo più dettagliato nel capitolo 2 "installazione e uso di NetX Duo BSD".

- **NX_BSD_RAW_PPPOE_SUPPORT**: Abilita supporto per i pacchetti PPPoE non elaborati. Per impostazione predefinita, questa opzione non è abilitata.

- **NX_BSD_ENABLE_DNS**: se abilitata, NETX Duo BSD invierà una query DNS per un nome host o un indirizzo IP host. Richiede che un'istanza del client DNS venga creata e avviata in precedenza. Per impostazione predefinita, non è abilitato.

- **NX_BSD_SOCKET_RAW_PROTOCOL_TABLE_SIZE**: definisce la dimensione della tabella di socket non elaborata. Il valore deve essere una potenza di due. NetX BSD crea una matrice di socket di tipo NX_BSD_SOCKETS per l'invio e la ricezione di pacchetti non elaborati. NX_ENABLE_IP_RAW_PACKET_FILTER deve essere abilitato. Per impostazione predefinita, è 32.

- **NX_BSD_IPV4_ADDR_MAX_NUM**: numero massimo di indirizzi IPv4 restituiti da *funzione getaddrinfo*. Questo insieme a NX_BSD_IPV6_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi di NetX BSD nx_bsd_addrinfo_block_pool per l'allocazione dinamica della memoria per l'archiviazione delle informazioni di indirizzo in *funzione getaddrinfo*. Il valore predefinito è 5.

- **NX_BSD_IPV6_ADDR_MAX_NUM**: numero massimo di indirizzi IPv6 restituiti da *funzione getaddrinfo*. Questo insieme a NX_BSD_IPV4_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi di NetX BSD nx_bsd_addrinfo_block_pool per l'allocazione dinamica della memoria per l'archiviazione delle informazioni di indirizzo in *funzione getaddrinfo*.

- **NX_BSD_IPV4_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv4 archiviati per ogni query DNS. Il valore predefinito è 5.

- **NX_BSD_IPV6_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv6 archiviati per ogni query DNS. Il valore predefinito è 2.

## <a name="bsd-socket-options"></a>Opzioni socket BSD

Il seguente elenco di opzioni socket NetX Duo BSD può essere abilitato (o disabilitato) in fase di esecuzione in base a ogni socket usando il servizio *setsockopt* :

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, 
                const void *option_value, INT option_length);
```

Esistono due impostazioni diverse per option_level.

Il primo tipo di opzioni dei socket di runtime è SOL_SOCKET per le opzioni a livello di socket. Per abilitare un'opzione a livello di socket, chiamare *setsockopt* con option_level impostato su SOL_SOCKET e option_name impostato sull'opzione specifica, ad esempio SO_BROADCAST *.* Per recuperare un'impostazione di opzione, chiamare *getsockopt* per la option_name con option_level di nuovo impostato su SOL_SOCKET.

Di seguito è riportato l'elenco delle opzioni del livello di socket del runtime.

- **SO_BROADCAST**: se impostato, consente l'invio e la ricezione di pacchetti broadcast da NETX Sockets. Questo è il comportamento predefinito per NetX Duo. Questa funzionalità è presente in tutti i socket.

- **SO_ERROR**: usato per ottenere lo stato del socket per l'operazione socket precedente del socket specificato, usando il servizio *getsockopt* . Questa funzionalità è presente in tutti i socket.

- **SO_KEEPALIVE**: se impostato, Abilita la funzionalità TCP keep alive. Questa operazione richiede che la libreria NetX Duo venga compilata con NX_TCP_ENABLE_KEEPALIVE definito in *nx_user. h*. Per impostazione predefinita, questa funzionalità è disabilitata.

- **SO_RCVTIMEO**: imposta l'opzione wait in secondi per la ricezione dei pacchetti nei socket BSD NETX Duo. Il valore predefinito è il NX_WAIT_FOREVER (0xFFFFFFFF) o, se il blocco non è abilitato, NX_NO_WAIT (0x0).

- **SO_RCVBUF**: consente di impostare le dimensioni della finestra del socket TCP. Il valore predefinito, NX_BSD_TCP_WINDOW, è impostato su 64K per i socket TCP BSD. Per impostare la dimensione superiore a 65535, è necessario che la libreria NetX Duo venga compilata con il NX_TCP_ENABLE_WINDOW_SCALING essere definito.

- **SO_REUSEADDR**: se impostato, consente di eseguire il mapping di più socket a una porta. L'utilizzo tipico è per il socket del server TCP. Si tratta del comportamento predefinito dei socket NetX Duo.

Il secondo tipo di opzioni del socket di run-time è il livello di opzione IP. Per abilitare un'opzione a livello IP, chiamare *setsockopt* con option_level impostato su IP_PROTO e option_name impostato sull'opzione, ad esempio IP_MULTICAST_TTL *.* Per recuperare un'impostazione di opzione, chiamare *getsockopt* per la option_name con option_level di nuovo impostato su IP_PROTO.

Di seguito è riportato l'elenco delle opzioni di livello IP di run-time.

- **IP_MULTICAST_TTL**: imposta la durata (TTL) per i socket UDP. Il valore predefinito è NX_IP_TIME_TO_LIVE (0x80) al momento della creazione del socket. È possibile eseguire l'override di questo valore chiamando *setsockopt* con questa opzione socket.

- **IP_RAW_IPV6_HDRINCL**: se questa opzione è impostata, l'applicazione chiamante deve aggiungere un'intestazione IPv6 e, facoltativamente, le intestazioni dell'applicazione ai dati trasmessi su socket IPv6 non elaborati creati da BSD. Per usare questa opzione, è necessario abilitare l'elaborazione di socket non elaborati nell'attività IP.

- **IP_ADD_MEMBERSHIP**: se impostata, questa opzione Abilita il socket BSD (si applica solo ai socket UDP) per l'aggiunta al gruppo IGMP specificato.

- **IP_DROP_MEMBERSHIP**: se impostata, questa opzione Abilita il socket BSD (si applica solo ai socket UDP) per lasciare il gruppo IGMP specificato.

- **IP_HDRINCL**: se questa opzione è impostata, l'applicazione chiamante deve aggiungere l'intestazione IP e, facoltativamente, le intestazioni dell'applicazione ai dati trasmessi in socket IPv4 non elaborati creati in BSD. Per usare questa opzione, è necessario abilitare l'elaborazione di socket non elaborati nell'attività IP.

- **IP_RAW_RX_NO_HEADER**: Se deselezionata, l'intestazione IPv6 viene inclusa con i dati ricevuti per i socket IPv6 non elaborati creati in BSD. Le intestazioni IPv6 vengono rimosse per impostazione predefinita nei socket IPv6 non elaborati BSD e la lunghezza del pacchetto non include l'intestazione IPv6.

Se impostato, l'intestazione IPv4 viene rimossa dai dati ricevuti su socket raw BSD di tipo IPv4. Le intestazioni IPv4 sono incluse per impostazione predefinita nei socket IPv4 non elaborati BSD e la lunghezza dei pacchetti include l'intestazione IPv4.

Questa opzione non ha alcun effetto sui dati di trasmissione IPv4 o IPv6.

## <a name="small-ipv4-example"></a>Piccolo esempio IPv4

Di seguito è riportato un esempio di come usare i servizi NetX Duo BSD per le reti IPv4. In questo esempio il file di inclusione *nxd_bsd. h* viene introdotto nella riga 8. Successivamente, l'istanza IP *bsd_ip* e *bsd_pool* pool di pacchetti vengono creati come variabili globali alle righe 20 e 21. Si noti che questa demo usa un driver di rete RAM (virtuale)*, _nx_ram_network_driver*. Il client e il server condividono lo stesso indirizzo IP in una singola istanza IP in questo esempio.

I thread client e server vengono creati nelle righe 62 e 68. Il pool di pacchetti BSD per la trasmissione di pacchetti viene creato alla riga 78 e usato nella creazione dell'istanza IP alla riga 87. Si noti che all'attività thread IP viene assegnata la priorità 1 nella chiamata *nx_ip_create* . Questo thread deve essere l'attività con priorità più elevata definita nel programma per ottimizzare le prestazioni di NetX.

L'istanza IP è abilitata per i servizi ARP e TCP rispettivamente sulle righe 88 e 110. L'ultimo requisito prima che i servizi BSD possano essere usati è chiamare *bsd_initialize* alla riga 120 per configurare tutte le strutture di dati e le risorse NETX e threadX necessarie per BSD.

La funzione entry thread server è definita successivamente. Il socket TCP BSD viene creato alla riga 149. La porta e l'indirizzo IP del server sono impostati sulle righe 160-163. Si noti l'uso delle macro dell'ordine dei byte da host a rete *htonl* e *htons* applicati alla porta e all'indirizzo IP. Questo è conforme alla specifica del socket BSD che i dati in più byte vengono inviati ai servizi BSD nell'ordine dei byte di rete.

Successivamente, il socket del server master viene associato alla porta usando il servizio *Bind* alla riga 166. Questo è il socket in ascolto per le richieste di connessione TCP tramite il servizio *Listen* sulla riga 180. Da qui la funzione thread del server, *thread_server_entry*, esegue cicli per verificare la presenza di eventi di ricezione tramite la chiamata *select* alla riga 202. Se un evento Receive è una richiesta di connessione, che viene determinata confrontando l'elenco Read Ready, viene chiamato *Accept* sulla riga 213. Un socket del server figlio viene assegnato per gestire la richiesta di connessione e aggiunto all'elenco principale dei socket del server TCP connessi a un client alla riga 223. Se non sono presenti nuove richieste di connessione, il thread del server verificherà tutti i socket attualmente connessi per gli eventi di ricezione nel ciclo for a partire dalla riga 236. Quando viene rilevato un evento di ricezione in attesa, chiama *Send* e *ricezione* su tale socket fino a quando non vengono ricevuti dati (connessione chiusa sull'altro lato) e il socket viene chiuso utilizzando il servizio *soc_close* alla riga 277.

Al termine dell'impostazione del thread del server, la funzione di immissione thread del client *thread_client_entry,* crea un socket alla riga 326 e si connette con il socket del server TCP utilizzando la chiamata di *connessione* alla riga 337. Esegue quindi il ciclo per inviare e ricevere pacchetti usando rispettivamente i servizi *Send* e *ricezione* . Quando non vengono ricevuti altri dati, il socket viene chiuso alla riga 398 usando il servizio *soc_close* . Dopo la disconnessione, la funzione di immissione thread del client crea un nuovo socket TCP ed effettua un'altra richiesta di connessione nel ciclo while avviato alla riga 321.

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

## <a name="small-ipv6-example-system"></a>Sistema di esempio IPv6 piccolo

Un esempio di come usare i servizi NetX Duo BSD per le reti IPv6 è descritto nel programma riportato di seguito. Questo esempio è molto simile al programma demo IPv4 descritto in precedenza con alcune importanti differenze.

I thread client e server, il pool di pacchetti BSD, l'istanza IP e l'inizializzazione BSD si verificano come per i socket BSD IPv4.

Nella funzione entry thread server *thread_server_entry*, definisce un paio di variabili IPv6 usando *sockaddr_in6* e *NXD_ADDRESS* tipi di dati sulle righe 145-148. Il tipo di dati NXD_ADDRESS può archiviare i tipi di indirizzi sia IPv4 che IPv6.

Successivamente, il thread del server Abilita IPv6 e ICMPv6 nell'istanza IP usando rispettivamente il servizio *nxd_ipv6_enable* e *nxd_icmpv6_enable* alla riga 161 e 169. Successivamente, il collegamento indirizzi IP globali e locali viene registrato con l'istanza IP. Questa operazione viene eseguita usando il servizio *nxd_ipv6_address_set* sulle righe 180 e 195. Quindi dorme abbastanza a lungo affinché l'attività del thread IP completi il protocollo di rilevamento degli indirizzi duplicati e registri questi indirizzi come indirizzi validi nella chiamata *tx_thread_sleep* alla riga 201.

Successivamente, il socket del server TCP viene creato con l'argomento di input del tipo di AF_INET6 socket alla riga 204. La porta e l'indirizzo IPv6 del socket sono impostati sulle righe 216-221, di nuovo l'uso delle macro *htonl* e *htons* per inserire i dati nell'ordine dei byte di rete per i servizi socket BSD. Da questo punto in poi, la funzione entry thread server è praticamente identica all'esempio IPv4.

La funzione di immissione thread del client, *thread_client_entry*, viene definita successivamente. Si noti che poiché il client TCP in questo esempio condivide la stessa istanza IP e l'indirizzo IPv6 del server TCP, non è necessario abilitare nuovamente i servizi IPv6 o ICMPv6 nell'istanza IP. Inoltre, l'indirizzo IPv6 è già registrato con l'istanza IP. Al contrario, la funzione di immissione thread del client attende semplicemente la riga 368 per la configurazione del server. L'indirizzo del server e la porta sono impostati, usando le macro dell'ordine dei byte dell'host alla rete nelle righe 387-392, quindi il client può connettersi al server TCP alla riga 412. Si noti che i tipi di dati degli indirizzi IP locali nelle righe 378-383 vengono usati solo per illustrare rispettivamente i servizi *getsockname* e *getpeername* sulle righe 425 e 434. Poiché i dati provengono dalla rete, la rete deve ospitare le macro dell'ordine dei byte, come usato nelle righe 378-383.

Successivamente la funzione di immissione thread del client entra in un ciclo in cui viene creato un socket TCP, effettua una connessione TCP e invia e riceve i dati con il server TCP fino a quando non vengono ricevuti più dati praticamente identici a quelli dell'esempio IPv4. Il socket viene quindi chiuso alla riga 483, viene sospesa brevemente e viene creato un altro socket TCP e viene richiesta una connessione al server TCP.

Una differenza importante con l'esempio IPv4 è che le chiamate *socket* specificano un socket IPv6 usando l'argomento di input AF_INET6. Un'altra differenza importante è che la chiamata di *connessione* del client TCP accetta un tipo di dati *sockaddr_in6* e un argomento length impostato sulla dimensione del tipo di dati *sockaddr_in6* .

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
