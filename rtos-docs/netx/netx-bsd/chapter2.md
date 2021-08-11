---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX BSD
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS BSD NetX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c04175ec18dff160faf853d675c9c85c9a0c6fbc5e834c410a7cb97a739c69f8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796702"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-bsd"></a>Capitolo 2 - Installazione e uso di Azure RTOS NetX BSD

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS BSD NetX.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS BSD NetX può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_bsd.h:** file di intestazione per NetX BSD
- **nx_bsd.c**: file di origine C per NetX BSD
- **nx_bsd.pdf**: Manuale dell'utente per NetX BSD

File demo:
- **bsd_demo_tcp.c**
- **bsd_demo_udp.c**

## <a name="netx-bsd-installation"></a>Installazione di NetX BSD

Per usare NetX BSD, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_bsd.h* e *nx_bsd.c* devono essere copiati in questa directory.

## <a name="building-the-threadx-and-netx-components-of-a-bsd-application"></a>Compilazione dei componenti ThreadX e NetX di un'applicazione BSD

### <a name="threadx"></a>ThreadX

La libreria ThreadX deve *definire* bsd_errno nell'archiviazione locale del thread. È consigliabile seguire questa procedura:

1. In *tx_port.h* impostare una delle macro TX_THREAD_EXTENSION seguenti:

  ```c
  #define TX_THREAD_EXTENSION_3     int bsd_errno
  ```

2. Ricompilare la libreria ThreadX.

> [!NOTE]
> Se TX_THREAD_EXTENSION_3 già usato, l'utente è libero di usare una delle altre macro TX_THREAD_EXTENSION macro.

### <a name="netx"></a>Netx

Prima di usare NetX BSD Services, la libreria NetX deve essere compilata con NX_ENABLE_EXTENDED_NOTIFY_SUPPORT definito (ad esempio in *nx_user.h*). Per impostazione predefinita, non è definito.

## <a name="using-netx-bsd"></a>Uso di NetX BSD

L'uso di BSD per NetX è semplice. In pratica, il codice dell'applicazione deve includere *nx_bsd.h* dopo aver incluso *rispettivamente tx_api.h* e *nx_api.h*, per poter usare rispettivamente ThreadX e NetX. Dopo *nx_bsd.h,* il codice dell'applicazione può usare i servizi BSD specificati più avanti in questa guida. L'applicazione deve anche *includere nx_bsd.c* nel processo di compilazione. Questo file deve essere compilato nello stesso modo degli altri file dell'applicazione e il relativo modulo oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX BSD.

Per utilizzare i servizi BSD NetX, l'applicazione deve creare un'istanza IP, un pool di pacchetti e inizializzare i servizi BSD chiamando *bsd_initialize.* Questo è illustrato nella sezione "Piccolo esempio" più avanti in questa guida. Il prototipo è illustrato di seguito:

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                  CHAR *free_memory_ptr, ULONG bsd_thread_stack_size,
                  UINT bsd_thread_priority);
```

Gli ultimi tre parametri vengono usati per creare un thread per l'esecuzione di attività periodiche, ad esempio il controllo degli eventi TCP e la definizione dello spazio dello stack di thread.

> [!NOTE]
> A differenza dei socket BSD, che funzionano in ordine bye di rete, NetX funziona nell'ordine dei byte host del processore host. Per motivi di compatibilità con l'origine, le macro htons(), ntohs(), htonl()), ntohl() sono state definite, ma non modificare l'argomento passato.

## <a name="netx-bsd-limitations"></a>Limitazioni di NetX BSD

A causa di problemi di prestazioni e architettura, NetX BSD non supporta tutte le funzionalità del socket BSD 4.3:

I flag INT non sono supportati per *le chiamate send, recv, sendto* *e recvfrom.*

## <a name="netx-bsd-with-dns-support"></a>NetX BSD con supporto DNS

Se NX_BSD_ENABLE_DNS definito, NetX BSD può inviare query DNS per ottenere informazioni sul nome host o sull'indirizzo IP dell'host. Questa funzionalità richiede che un client DNS NetX sia stato creato in precedenza usando il *nx_dns_create* servizio. Uno o più indirizzi IP del server DNS noti devono essere registrati con l'istanza DNS *usando* il nx_dns_server_add per l'aggiunta di indirizzi del server.

I servizi DNS e l'allocazione di memoria vengono usati *dai servizi getaddrinfo* *e getnameinfo:*

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
              const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
              char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

Quando l'applicazione BSD chiama *getaddrinfo* con un nome host, NetX BSD chiamerà uno dei servizi seguenti per ottenere l'indirizzo IP:

- nx_dns_ipv4_address_by_name_get
- nx_dns_cname_get

Ad *nx_dns_ipv4_address_by_name_get*, NetX BSD usa le ipv4_addr_buffer di memoria. Le dimensioni di questi buffer sono definite da ( `NX_BSD_IPV4_ADDR_PER_HOST * 4` ).

Per restituire informazioni sull'indirizzo da *getaddrinfo*, NetX BSD usa la tabella di memoria a blocchi ThreadX *nx_bsd_addrinfo_pool_memory*, la cui area di memoria è definita da un altro set di *opzioni configurabili, NX_BSD_IPV4_ADDR_MAX_NUM*.

Per **altri dettagli sulle** opzioni di configurazione precedenti, vedere Opzioni di configurazione.

Inoltre, se NX_DNS_ENABLE_EXTENDED_RR_TYPES definito e l'input host è un nome canonico, NetX BSD alloca la memoria in modo dinamico da un pool di blocchi creato in *precedenza _nx_bsd_cname_block_pool*

> [!NOTE]
> Dopo aver *chiamato getaddrinfo,* l'applicazione BSD è responsabile del rilascio della memoria a cui punta l'argomento res alla tabella di blocco usando il *servizio freeaddrinfo.*

## <a name="configuration-options"></a>Opzioni di configurazione

Le opzioni configurabili dall'utente *in nx_bsd.h* consentono all'applicazione di ottimizzare i socket BSD NetX per i requisiti specifici. Di seguito è riportato un elenco di questi parametri:

- **NX_BSD_TCP_WINDOW**: usato nelle chiamate di creazione del socket TCP. 65535 è una tipica dimensione della finestra per 100 Mb Ethernet. Il valore predefinito è 65535.
- **NX_BSD_SOCKFD_START** Si tratta dell'indice logico per il valore di avvio del descrittore del file socket BSD. Per impostazione predefinita, questa opzione è 32.
- **NX_BSD_MAX_SOCKETS** Specifica il numero massimo di socket totali disponibili nel livello BSD e deve essere un multiplo di 32. Il valore predefinito è 32.
- **NX_BSD_SOCKET_QUEUE_MAX** Specifica il numero massimo di pacchetti UDP archiviati nella coda del socket di ricezione. Il valore predefinito è 5.
- **NX_BSD_MAX_LISTEN_BACKLOG** Specifica le dimensioni della coda di attesa ('backlog') per i socket TCP BSD. Il valore predefinito è 5.
- **NX_MICROSECOND_PER_CPU_TICK** Specifica il numero di microsecondi per interrupt timer
- **NX_BSD_TIMEOUT** Specifica il timeout nei tick timer nelle chiamate interne NetX richieste da BSD. Il valore predefinito è 20*NX_IP_PERIODIC_RATE.
- **NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: specifica il timeout nei tick timer nella chiamata di disconnessione NetX. Il valore predefinito è 1.
- **NX_BSD_PRINT_ERRORS** Se impostato, il valore restituito dello stato di errore di una funzione BSD restituisce un numero di riga e un tipo di errore, ad esempio NX_SOC_ERROR in cui si verifica l'errore. Ciò richiede allo sviluppatore dell'applicazione di definire l'output di debug. L'impostazione predefinita è disabilitata e non viene specificato alcun output di debug *in nx_bsd.h*
- **NX_BSD_TIMER_RATE** Intervallo dopo il quale viene eseguita l'attività timer periodica BSD. Il valore predefinito è 1 secondo (1 * NX_IP_PERIODIC_RATE).
- **NX_BSD_TIMEOUT_PROCESS_IN_TIMER** Se impostata, questa opzione consente l'esecuzione del processo di timeout BSD nel contesto del timer di sistema. Il comportamento predefinito è disabilitato. Questa funzionalità è descritta in modo più dettagliato nel capitolo 2 "Installazione e uso di NetX BSD".
- **NX_BSD_ENABLE_DNS** Se abilitata, NetX BSD invierà una query DNS per un nome host o un indirizzo IP host. Richiede che un'istanza del client DNS sia stata creata e avviata in precedenza. Per impostazione predefinita, non è abilitato.
- **NX_BSD_IPV4_ADDR_MAX_NUM** Numero massimo di indirizzi IPv4 restituiti da *getaddrinfo*. Insieme a NX_BSD_IPV4_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi NetX BSD nx_bsd_addrinfo_block_pool allocare dinamicamente memoria per l'archiviazione delle informazioni in *getaddrinfo*. Il valore predefinito è 5.
- **NX_BSD_IPV4_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv4 archiviati per ogni query DNS. Il valore predefinito è 5.

## <a name="bsd-socket-options"></a>Opzioni socket BSD

L'elenco seguente di opzioni socket BSD NetX può essere abilitato (o disabilitato) in fase di esecuzione in base al socket usando il *servizio setsockopt:*

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, const
                void *option_value, INT option_length);
```

Esistono due impostazioni diverse *per* option_level .

Il primo tipo di opzioni socket in fase di esecuzione è SOL_SOCKET per le opzioni a livello di socket. Per abilitare un'opzione a livello di socket, chiamare *setsockopt* con option_level impostato su SOL_SOCKET e option_name impostato sull'opzione specifica, ad esempio SO_BROADCAST. Per recuperare un'impostazione di opzione, chiamare *getsockopt* per il option_name con option_level impostato nuovamente su SOL_SOCKET.

Di seguito è riportato l'elenco delle opzioni a livello di socket in fase di esecuzione.

- **SO_BROADCAST:** se impostato, consente l'invio e la ricezione di pacchetti broadcast dai socket Netx. Questo è il comportamento predefinito per NetX. Tutti i socket hanno questa funzionalità.
- **SO_ERROR**: usato per ottenere lo stato del socket nell'operazione socket precedente del socket specificato, usando il *servizio getsockopt.* Tutti i socket hanno questa funzionalità.
- **SO_KEEPALIVE:** se impostato, abilita la funzionalità Keep Alive TCP. Questa operazione richiede che la libreria NetX sia compilata NX_TCP_ENABLE_KEEPALIVE definita in *nx_user.h*. Per impostazione predefinita, questa funzionalità è disabilitata.
- **SO_RCVTIMEO**: imposta l'opzione di attesa in secondi per la ricezione di pacchetti nei socket BSD NetX. Il valore predefinito è NX_WAIT_FOREVER (0xFFFFFFFF) o, se non è abilitato il blocco, NX_NO_WAIT (0x0).
- **SO_RCVBUF**: imposta le dimensioni della finestra del socket TCP. Il valore predefinito, NX_BSD_TCP_WINDOW, è impostato su 64.000 per i socket TCP BSD. Per impostare le dimensioni su 65535, è necessario che la libreria NetX sia compilata con la NX_TCP_ENABLE_WINDOW_SCALING essere definita.
- **SO_REUSEADDR:** se impostato, consente di eseguire il mapping di più socket a una porta. L'utilizzo tipico è per il socket del server TCP. Questo è il comportamento predefinito dei socket NetX.

Il secondo tipo di opzioni socket in fase di esecuzione è il livello di opzione IP. Per abilitare un'opzione a livello di IP, chiamare *set di chiamateockopt* con option_level impostato su IP_PROTO e option_name impostato sull'opzione , ad esempio IP_MULTICAST_TTL. Per recuperare un'impostazione di opzione, chiamare *getsockopt* per il option_name con option_level impostato nuovamente su IP_PROTO.

Di seguito è riportato l'elenco delle opzioni del livello IP della fase di esecuzione.

- **IP_MULTICAST_TTL**: imposta il tempo di vita per i socket UDP. Il valore predefinito è NX_IP_TIME_TO_LIVE (0x80) quando viene creato il socket. Questo valore può essere sostituito chiamando *setsockopt con* questa opzione socket.
- **IP_ADD_MEMBERSHIP:** se impostata, questa opzione consente al socket BSD (si applica solo ai socket UDP) di partecipare al gruppo IGMP specificato.
- **IP_DROP_MEMBERSHIP:** se impostata, questa opzione consente al socket BSD (si applica solo ai socket UDP) di uscire dal gruppo IGMP specificato.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come usare NetX BSD è illustrato nella figura 1.0 seguente. In questo esempio il file di *inclusione nx_bsd.h* viene portato alla riga 7. Successivamente, l'istanza IP *bsd_ip* pool *di* pacchetti bsd_pool vengono create come variabili globali alle righe 20 e 21. Si noti che questa demo usa un driver di rete ram (virtuale) (riga 41). In questo esempio il client e il server condivideranno lo stesso indirizzo IP nella singola istanza IP.

I thread client e server vengono creati nelle righe 303 e 309 *in tx_application_define che* configura l'applicazione ed è definito nelle righe 293-361. Al termine della creazione dell'istanza IP alla riga 327, l'istanza IP viene abilitata per i servizi TCP alla riga 350. L'ultimo requisito prima che sia possibile usare i servizi *BSD* è chiamare bsd_initialize alla riga 360 per configurare tutte le strutture di dati e le risorse NetX e ThreadX necessarie per BSD.

Nella funzione di immissione del thread del server, *thread_1_entry,* definita nelle righe 381-397, l'applicazione attende che il driver inizializza NetX con i parametri di rete. Al termine, chiama *tcpServer,* definito nelle righe 146-253, per gestire i dettagli della configurazione del socket del server TCP.

*tcpServer* crea il socket master chiamando il *servizio socket* sulla riga 159  e lo associa al socket di ascolto usando la chiamata bind sulla riga 176. Viene quindi configurato per l'ascolto delle richieste di connessione alla riga 191. Si noti che il socket master non accetta una richiesta di connessione. Viene eseguito in un ciclo continuo che chiama *select ogni* volta per rilevare le richieste di connessione. A un socket BSD secondario scelto da una matrice di socket BSD viene assegnata la richiesta di connessione dopo aver chiamato il servizio *accept* alla riga 218.

Sul lato Client, anche la funzione di immissione del thread client, *thread_0_entry*, definita nelle righe 366-377, deve attendere l'inizializzazione di NetX da parte del driver. In questo caso è sufficiente attendere che il lato server lo faccia. Chiama quindi *tcpClient* definito nella riga 54-142 per gestire i dettagli della configurazione del socket client TCP e della richiesta di una connessione TCP.

Il socket client TCP viene creato alla riga 68. Il socket è associato all'indirizzo IP specificato e tenta di connettersi al server TCP chiamando *connect* sulla riga 84. È ora possibile iniziare a inviare e ricevere pacchetti.

```c
1 /*  This is a small demo of BSD Wrapper for the high-performance NetX TCP/IP stack.
2     This demo demonstrate TCP connection, disconnection, sending, and receiving using
3     ARP and a simulated Ethernet driver. */
4
5 #include     "tx_api.h"
6 #include     "nx_api.h"
7 #include     "nx_bsd.h"
8 #include     <string.h>
9 #include     <stdlib.h>
10
11 #define         DEMO_STACK_SIZE         (16*1024)
12
13
14 /* Define the ThreadX and NetX object control blocks... */
15
16 TX_THREAD       thread_0;
17 TX_THREAD       thread_1;
18
19
20 NX_PACKET_POOL  bsd_pool;
21 NX_IP           bsd_ip;
22
23
24 /* Define the counters used in the demo application... */
25
26 ULONG           error_counter;
27
28 /* Define fd_set for select call */
29 fd_set          master_list,read_ready,read_ready1;
30
31
32 /* Define thread prototypes. */
33
34 VOID            thread_0_entry(ULONG thread_input);
35 VOID            thread_1_entry(ULONG thread_input);
36
37 VOID            tcpClient(CHAR *msg0);
38 VOID            tcpServer(VOID);
39 INT             HandleClient(INT sock);
40
41 VOID            _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
42
43
44 /* Define main entry point. */
45
46 int main()
47 {
48
49     /* Enter the ThreadX kernel. */
50     tx_kernel_enter();
51 }
52
53
54 VOID tcpClient(CHAR *msg0)
55 {
56
57 INT     status,status1,send_counter;
58 INT     sock_tcp_1,length,length1;
59 struct  sockaddr_in echoServAddr;       /* Echo server address */
60 struct  sockaddr_in localAddr;          /* Local address */
61 struct  sockaddr_in remoteAddr;         /* Remote address */
62
63 UINT    echoServPort; /* Echo Server Port */
64 CHAR    rcvBuffer1[32]
65
66
67     /* Create BSD TCP Socket */
68     sock_tcp_1 = **socket**( PF_INET, SOCK_STREAM, IPPROTO_TCP);
69     if (sock_tcp_1 == -1)
70     {
71         printf("\nError: BSD TCP Client socket create \n");
72         return;
73     }
74
75     printf("\nBSD TCP Client socket created %lu \n", sock_tcp_1);
76     /* Fill destination port and IP address */
77     echoServPort = 12;
78     memset(&echoServAddr, 0, sizeof(echoServAddr));
79     echoServAddr.sin_family = PF_INET;
80     echoServAddr.sin_addr.s_addr = htonl(0x01020304);
81     echoServAddr.sin_port = echoServPort;
82
83     /* Now connect this client the server */
84     status1 = connect(sock_tcp_1, (struct sockaddr *)&echoServAddr, sizeof(echoServAddr));
85     /* Check for error. */
86     if (status1 != OK)
87     {
88         printf("\nError: BSD TCP Client socket Connect, %d \n",sock_tcp_1);
89         status = soc_close(sock_tcp_1);
90         if (status != ERROR)
91             printf("\nConnect ERROR so BSD Client Socket Closed: %d\n",sock_tcp_1);
92         else
93             printf("\nError: BSD Client Socket close %d\n",sock_tcp_1);
94         return;
95     }
96     /* Get and print source and destination information */
97     printf("\nBSD TCP Client socket: %d connected \n", sock_tcp_1);
98
99     status = getsockname(sock_tcp_1, (struct sockaddr *)&localAddr, &length);
100    printf("Client port = %lu , Client = %lu,", 
            localAddr.sin_port, localAddr.sin_addr.s_addr);
101    status = getpeername( sock_tcp_1, (struct sockaddr *) &remoteAddr, &length1);
102    printf("Remote port = %lu, Remote IP = %lu \n", 
            remoteAddr.sin_port remoteAddr.sin_addr.s_addr);
103
104    send_counter = 1;
105
106    /* Now receive the echoed packet from the server */
107    while(1)
108    {
109        tx_thread_sleep(2);
110
111        printf("\nClient sock: %d Sending packet No: %d to
                server\n",sock_tcp_1,send_counter);
112        status = send(sock_tcp_1,msg0, sizeof(msg0), 0);
113        if (status == ERROR)
114            printf("Error: BSD Client Socket send %d\n",sock_tcp_1);
115        else
116        {
117            printf("\nMessage sent: %s\n",msg0);
118            send_counter++;
119        }
120
121        status = recv(sock_tcp_1, (VOID *)rcvBuffer1, 31,0);
122        if (status == 0)
123            break;
124
125        rcvBuffer1[status] = 0;
126
127        if (status != ERROR)
128            printf("\nBSD Client Socket: %d received %lu bytes: %s ", 
                        sock_tcp_1,(ULONG)status,rcvBuffer1);
129        else
130            printf("\nError: BSD Client Socket receive %d \n",sock_tcp_1);
131
132    }
133
134    /* close this client socket */
135    status = soc_close(sock_tcp_1);
136    if (status != ERROR)
137        printf("\nBSD Client Socket Closed %d\n",sock_tcp_1);
138    else
139        printf("\nError: BSD Client Socket close %d \n",sock_tcp_1);
140
141    /* End */
142 }
143
144
145
146 void tcpServer(void)
147 {
148
149 INT         status,status1,sock,sock_tcp_2,i;
150 struct      sockaddr_in echoServAddr; /* Echo server address */
151 struct      sockaddr_in ClientAddr;
152
153 INT         Clientlen;
154 UINT        echoServPort; /* Echo Server Port */
155
156 INT         maxfd;
157
158 /* Create BSD TCP Server Socket */
159     sock_tcp_2 = socket( PF_INET, SOCK_STREAM, IPPROTO_TCP);
160     if (sock_tcp_2 == -1)
161     {
162         printf("Error: BSD TCP Server socket create\n");
163         return;
164     }
165     else
166         printf("BSD TCP Server socket created \n");
167
168     /* Now fill server side information */
169     echoServPort = 12;
170     memset(&echoServAddr, 0, sizeof(echoServAddr));
171     echoServAddr.sin_family = PF_INET;
172     echoServAddr.sin_addr.s_addr = htonl(0x01020304);
173     echoServAddr.sin_port = echoServPort;
174
175     /* Bind this server socket */
176         status = bind(sock_tcp_2, (struct sockaddr *) &echoServAddr, sizeof(echoServAddr));
177     if (status < 0)
178     {
179         printf("Error: BSD TCP Server Socket Bind \n");
180         return;
181     }
182     else
183         printf("BSD TCP Server Socket bound \n");
184
185     FD_ZERO(&master_list);
186     FD_ZERO(&read_ready);
187     FD_SET(sock_tcp_2,&master_list);
188     maxfd = sock_tcp_2;
189
190     /* Now listen for any client connections for this server socket */
191     status = listen(sock_tcp_2,5);
192     if (status < 0)
193     {
194         printf("Error: BSD TCP Server Socket Listen\n");
195         return;
196     }
197     else
198         printf("BSD TCP Server Socket Listen complete, ");
199
200     /* All set to accept client connections */
201     printf("Now accepting client connections\n");
202
203     /* Loop to create and establish server connections. */
204     while(1)
205     {
206
207         read_ready = master_list;
208         tx_thread_sleep(2); /* Allow some time to other threads too */
209         status = select(maxfd+1,&read_ready,0,0,0);
210         if (status == ERROR)
211         {
212             continue;
213         }
214
215         status = FD_ISSET(sock_tcp_2,&read_ready);
216         if(status)
217         {
218             sock = accept(sock_tcp_2,(struct sockaddr*)&ClientAddr, &Clientlen);
219
220             /* Add this new connection to our master list */
221             FD_SET(sock,&master_list);
222             if ( sock \maxfd)
223             {
224                 maxfd = sock;
225             }
226
227             continue;
228         }
229         for (i = 0; i < (maxfd+1); i++)
230         {
231             if (( i != sock_tcp_2) && (FD_ISSET(i,&master_list)) && 
                    (FD_ISSET(i,&read_ready)))
232             {
233                 status1 = HandleClient(i);
234                 if (status1 == 0)
235                 {
236                     status1 = soc_close(i);
237                     if (status1 == OK)
238                     {
239                         FD_CLR(i,&master_list);
240                         printf("\nBSD Server Socket:%d closed\n",i);
241                     }
242                     else
243                         printf("\nError:BSD Server Socket:%d close\n",i);
244                 }
245
246             }
247         }
248
249         /* Loop back to check any next client connection */
250
251     } /* While(1) ends */
252
253 }
254
255 CHAR     rcvBuffer[128];
256
257 INT     HandleClient(INT sock)
258 {
259
260 INT     status;
261
262
263     status = recv(sock, (VOID *)rcvBuffer, 128,0);
264     if (status == ERROR )
265     {
266         printf("\n BSD Server Socket:%d receive \n",sock);
267         return(ERROR);
268     }
269
270     /* a zero return from a recv() call indicates client is terminated! */
271     if (status == 0)
272     {
273         /* Done with this client , close this secondary server socket */
274         return(status);
275     }
276
277     /* print data received from the client */
278     printf("\nBSD Server Socket:%d received %lu bytes: %s \n", sock, (ULONG)status,rcvBuffer);
279
280     /* And echo the same data to the client */
281     status = send(sock,rcvBuffer, status + 1, 0);
282     if (status == ERROR )
283     {
284         printf("\nError: BSD Server Socket:%d send \n",sock);
285         return(ERROR);
286     }
287     return(status);
288 }
289
290
291 /* Define what the initial system looks like. */
292
293 void     tx_application_define(void *first_unused_memory)
294 {
295
296 CHAR     *pointer;
297 UINT     status;
298
299     /* Setup the working pointer. */
300     pointer = (CHAR *) first_unused_memory;
301
302     /* Create a client thread. */
303     tx_thread_create(&thread_0, "Client1", thread_0_entry, 0,
304         pointer, DEMO_STACK_SIZE, 2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
305
306     pointer = pointer + DEMO_STACK_SIZE;
307
308     /* Create a server thread. */
309     tx_thread_create(&thread_1, "Server", thread_1_entry, 0,
310         pointer, DEMO_STACK_SIZE,1,1, TX_NO_TIME_SLICE, TX_AUTO_START);
311
312     pointer = pointer + DEMO_STACK_SIZE;
313
314     /* Initialize the NetX system. */
315     nx_system_initialize();
316
317     /* Create a BSD packet pool. */
318     status = nx_packet_pool_create(&bsd_pool,"NetX BSD Packet Pool", 128
                                        pointer, 16384);
319     pointer = pointer + 16384;
320     if (status)
321     {
322         error_counter++;
323         printf("Error in creating BSD packet pool\n!");
324     }
325
326     /* Create an IP instance for BSD. */
327     status = nx_ip_create(&bsd_ip, "NetX IP Instance 2", IP_ADDRESS(1, 2, 3, 4),
                              0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                              pointer, 2048, 1);
328
329     pointer = pointer + 2048;
330
331     if (status)
332     {
333         error_counter++;
334         printf("Error creating BSD IP instance\n!");
335     }
336
337     /* Enable ARP and supply ARP cache memory for BSD IP Instance */
338     status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
339     pointer = pointer + 1024;
340
341     /* Check ARP enable status. */
342     if (status)
343     {
344         error_counter++;
345         printf("Error in Enable ARP and supply ARP cache memory to BSD IP instance\n");
346     }
347
348     /* Enable TCP processing for BSD IP instances. */
349
350     status = nx_tcp_enable(&bsd_ip);
351
352     /* Check TCP enable status. */
353     if (status)
354     {
355         error_counter++;
356         printf("Error in Enable TCP \n");
357     }
358
359     /* Now initialize BSD Scoket Wrapper */
360     status = bsd_initialize(&bsd_ip, &bsd_pool,pointer, 2048, 1);
361 }
362
363
364 /* Define the test threads. */
365
366 void     thread_0_entry)ULONG thread_input)
367 {
368
369 CHAR     *msg0 = "Client 1:
                     "ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<> \
                     "ABCDEFGHIJKLMNOPQRSTUVWXYZ<>END";
370
371     /* Wait till Server side is all set */
372     tx_thread_sleep(2);
373     while (1)
374     {
375         tcpClient(msg0);
376         tx_thread_sleep(1);
377     }
378 }
379
380 /* Define the server thread entry function. */
381 void     thread_1_entry(ULONG thread_input)
382 {
383
384 UINT     status;
385 ULONG    actual_status;
386
387 /* Ensure the IP instance has been initialized. */
388 status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE, &actual_status, 100);
389
390 /* Check status... */
391 if (status != NX_SUCCESS)
392 {
393     error_counter++;
394     return;
395 }
396 /* Start a TCP Server */
397 tcpServer();
398 }
399
```
