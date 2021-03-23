---
title: Capitolo 2-installazione e uso di Azure RTO NetX BSD
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente RTO NetX BSD di Azure.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7539565ccd4956c5354be45000efab8318dc606c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822748"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-bsd"></a>Capitolo 2-installazione e uso di Azure RTO NetX BSD

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente RTO NetX BSD di Azure.

## <a name="product-distribution"></a>Distribuzione del prodotto

È possibile ottenere Azure RTO NetX BSD dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_bsd. h**: file di intestazione per NETX BSD
- **nx_bsd. c**: file di origine c per NETX BSD
- **nx_bsd.pdf**: manuale dell'utente per NETX BSD

File demo:
- **bsd_demo_tcp. c**
- **bsd_demo_udp. c**

## <a name="netx-bsd-installation"></a>Installazione di NetX BSD

Per poter usare NetX BSD, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_bsd. h* e *nx_bsd. c* devono essere copiati in questa directory.

## <a name="building-the-threadx-and-netx-components-of-a-bsd-application"></a>Compilazione dei componenti ThreadX e NetX di un'applicazione BSD

### <a name="threadx"></a>ThreadX

La libreria ThreadX deve definire *bsd_errno* nell'archiviazione locale di thread. Si consiglia la seguente procedura:

1. In *tx_port. h*, impostare una delle macro TX_THREAD_EXTENSION come indicato di seguito:

  ```c
  #define TX_THREAD_EXTENSION_3     int bsd_errno
  ```

2. Ricompilare la libreria ThreadX.

> [!NOTE]
> Se TX_THREAD_EXTENSION_3 è già in uso, l'utente è libero di usare una delle altre macro TX_THREAD_EXTENSION.

### <a name="netx"></a>NetX

Prima di usare NetX BSD Services, è necessario compilare la libreria NetX con NX_ENABLE_EXTENDED_NOTIFY_SUPPORT definito (ad esempio, in *nx_user. h*). Per impostazione predefinita, non è definito.

## <a name="using-netx-bsd"></a>Uso di NetX BSD

L'uso di BSD per NetX è facile. In pratica, il codice dell'applicazione deve includere *nx_bsd. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX. Una volta incluso *nx_bsd. h* , il codice dell'applicazione è in grado di usare i servizi BSD specificati più avanti in questa guida. Nell'applicazione deve inoltre essere incluso *nx_bsd. c* nel processo di compilazione. Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX BSD.

Per usare i servizi NetX BSD, l'applicazione deve creare un'istanza IP, un pool di pacchetti e inizializzare i servizi BSD chiamando *bsd_initialize.* Questa procedura è illustrata nella sezione "piccolo esempio" più avanti in questa guida. Il prototipo è illustrato di seguito:

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                  CHAR *free_memory_ptr, ULONG bsd_thread_stack_size,
                  UINT bsd_thread_priority);
```

Gli ultimi tre parametri vengono utilizzati per la creazione di un thread per eseguire attività periodiche, ad esempio la verifica degli eventi TCP e la definizione dello spazio dello stack dei thread.

> [!NOTE]
> A differenza dei socket BSD, che funzionano nell'ordine di rete bye, NetX funziona nell'ordine dei byte dell'host del processore host. Per motivi di compatibilità con l'origine, le macro htons (), ntohs (), htonl (), ntohl () sono state definite, ma non modificano l'argomento passato.

## <a name="netx-bsd-limitations"></a>Limitazioni di NetX BSD

A causa di problemi relativi alle prestazioni e all'architettura, NetX BSD non supporta tutte le funzionalità socket di BSD 4,3:

I flag INT non sono supportati per le chiamate *Send, ricezione, SendTo* e *recvfrom* .

## <a name="netx-bsd-with-dns-support"></a>NetX BSD con supporto DNS

Se NX_BSD_ENABLE_DNS è stato definito, NetX BSD può inviare query DNS per ottenere informazioni sul nome host o sull'indirizzo IP dell'host. Questa funzionalità richiede che un client DNS NetX venga creato in precedenza usando il servizio *nx_dns_create* . Uno o più indirizzi IP del server DNS noti devono essere registrati con l'istanza DNS usando il *nx_dns_server_add* per l'aggiunta degli indirizzi del server.

I servizi DNS e l'allocazione di memoria vengono usati dai servizi *funzione getaddrinfo* e *GetNameInfo* :

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
              const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
              char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

Quando l'applicazione BSD chiama *funzione getaddrinfo* con un nome host, NETX BSD chiamerà uno dei servizi seguenti per ottenere l'indirizzo IP:

- nx_dns_ipv4_address_by_name_get
- nx_dns_cname_get

Per *nx_dns_ipv4_address_by_name_get*, NETX BSD usa le aree di memoria ipv4_addr_buffer. Le dimensioni di questi buffer sono definite da ( `NX_BSD_IPV4_ADDR_PER_HOST * 4` ).

Per restituire le informazioni sull'indirizzo da *funzione getaddrinfo*, NETX BSD usa la tabella di memoria a blocchi threadX *nx_bsd_addrinfo_pool_memory*, la cui area di memoria è definita da un altro set di opzioni configurabili, *NX_BSD_IPV4_ADDR_MAX_NUM*.

Per ulteriori informazioni sulle opzioni di configurazione precedenti, vedere **Opzioni di configurazione** .

Inoltre, se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito e l'input dell'host è un nome canonico, NetX BSD alloca la memoria in modo dinamico da un pool di blocchi creato in precedenza *_nx_bsd_cname_block_pool*

> [!NOTE]
> Dopo la chiamata a *funzione getaddrinfo* , l'applicazione BSD è responsabile del rilascio della memoria a cui fa riferimento l'argomento res alla tabella dei blocchi usando il servizio *FreeAddrInfo* .

## <a name="configuration-options"></a>Opzioni di configurazione

Le opzioni configurabili dall'utente in *nx_bsd. h* consentono all'applicazione di ottimizzare i socket NETX BSD per i requisiti specifici. Di seguito è riportato un elenco di questi parametri:

- **NX_BSD_TCP_WINDOW**: utilizzato nelle chiamate di creazione socket TCP. 65535 è una tipica dimensione della finestra per Ethernet 100Mb. Il valore predefinito è 65535.
- **NX_BSD_SOCKFD_START** Si tratta dell'indice logico per il valore iniziale del descrittore del file socket BSD. Per impostazione predefinita, questa opzione è 32.
- **NX_BSD_MAX_SOCKETS** Specifica il numero massimo di socket totali disponibili nel livello BSD e deve essere un multiplo di 32. per impostazione predefinita, il valore è 32.
- **NX_BSD_SOCKET_QUEUE_MAX** Specifica il numero massimo di pacchetti UDP archiviati nella coda del socket di ricezione. Il valore predefinito è 5.
- **NX_BSD_MAX_LISTEN_BACKLOG** Specifica le dimensioni della coda di ascolto (' backlog ') per i socket TCP BSD. Il valore predefinito è 5.
- **NX_MICROSECOND_PER_CPU_TICK** Specifica il numero di microsecondi per ogni interrupt del timer
- **NX_BSD_TIMEOUT** Specifica il timeout nei cicli del timer per le chiamate interne NetX richieste da BSD. Il valore predefinito è 20 * NX_IP_PERIODIC_RATE.
- **NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: specifica il timeout nei cicli del timer per la chiamata di disconnessione NETX. Il valore predefinito è 1.
- **NX_BSD_PRINT_ERRORS** Se impostato, lo stato di errore restituito da una funzione BSD restituisce un numero di riga e il tipo di errore, ad esempio NX_SOC_ERROR in cui si è verificato l'errore. A questo scopo, lo sviluppatore dell'applicazione deve definire l'output di debug. L'impostazione predefinita è disabilitata e non è stato specificato alcun output di debug in *nx_bsd. h*
- **NX_BSD_TIMER_RATE** Intervallo dopo il quale viene eseguita l'attività del timer periodico BSD. Il valore predefinito è 1 secondo (1 * NX_IP_PERIODIC_RATE).
- **NX_BSD_TIMEOUT_PROCESS_IN_TIMER** Se impostata, questa opzione consente l'esecuzione del processo di timeout BSD nel contesto del timer di sistema. Il comportamento predefinito è Disabled. Questa funzionalità è descritta in modo più dettagliato nel capitolo 2 "installazione e uso di NetX BSD".
- **NX_BSD_ENABLE_DNS** Se abilitata, NetX BSD invierà una query DNS per un nome host o un indirizzo IP host. Richiede che un'istanza del client DNS venga creata e avviata in precedenza. Per impostazione predefinita, non è abilitato.
- **NX_BSD_IPV4_ADDR_MAX_NUM** Numero massimo di indirizzi IPv4 restituiti da *funzione getaddrinfo*. Questo insieme a NX_BSD_IPV4_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi di NetX BSD nx_bsd_addrinfo_block_pool per l'allocazione dinamica della memoria per l'archiviazione delle informazioni di indirizzo in *funzione getaddrinfo*. Il valore predefinito è 5.
- **NX_BSD_IPV4_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv4 archiviati per ogni query DNS. Il valore predefinito è 5.

## <a name="bsd-socket-options"></a>Opzioni socket BSD

Il seguente elenco di opzioni socket NetX BSD può essere abilitato (o disabilitato) in fase di esecuzione in base a ogni socket usando il servizio *setsockopt* :

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, const
                void *option_value, INT option_length);
```

Esistono due impostazioni diverse per *option_level*.

Il primo tipo di opzioni dei socket di runtime è SOL_SOCKET per le opzioni a livello di socket. Per abilitare un'opzione a livello di socket, chiamare *setsockopt* con option_level impostato su SOL_SOCKET e option_name impostato sull'opzione specifica, ad esempio SO_BROADCAST. Per recuperare un'impostazione di opzione, chiamare *getsockopt* per la option_name con option_level di nuovo impostato su SOL_SOCKET.

Di seguito è riportato l'elenco delle opzioni del livello di socket del runtime.

- **SO_BROADCAST**: se impostato, consente l'invio e la ricezione di pacchetti broadcast da NETX Sockets. Questo è il comportamento predefinito per NetX. Questa funzionalità è presente in tutti i socket.
- **SO_ERROR**: usato per ottenere lo stato del socket per l'operazione socket precedente del socket specificato, usando il servizio *getsockopt* . Questa funzionalità è presente in tutti i socket.
- **SO_KEEPALIVE**: se impostato, Abilita la funzionalità TCP keep alive. A tale scopo, è necessario compilare la libreria NetX con NX_TCP_ENABLE_KEEPALIVE definito in *nx_user. h*. Per impostazione predefinita, questa funzionalità è disabilitata.
- **SO_RCVTIMEO**: imposta l'opzione wait in secondi per la ricezione dei pacchetti nei socket NETX BSD. Il valore predefinito è il NX_WAIT_FOREVER (0xFFFFFFFF) o, se il blocco non è abilitato, NX_NO_WAIT (0x0).
- **SO_RCVBUF**: consente di impostare le dimensioni della finestra del socket TCP. Il valore predefinito, NX_BSD_TCP_WINDOW, è impostato su 64K per i socket TCP BSD. Per impostare la dimensione superiore a 65535, è necessario che la libreria NetX venga compilata con il NX_TCP_ENABLE_WINDOW_SCALING essere definito.
- **SO_REUSEADDR**: se impostato, consente di eseguire il mapping di più socket a una porta. L'utilizzo tipico è per il socket del server TCP. Si tratta del comportamento predefinito dei socket NetX.

Il secondo tipo di opzioni del socket di run-time è il livello di opzione IP. Per abilitare un'opzione a livello IP, chiamare *setsockopt* con option_level impostato su IP_PROTO e option_name impostato sull'opzione, ad esempio IP_MULTICAST_TTL. Per recuperare un'impostazione di opzione, chiamare *getsockopt* per la option_name con option_level di nuovo impostato su IP_PROTO.

Di seguito è riportato l'elenco delle opzioni di livello IP di run-time.

- **IP_MULTICAST_TTL**: imposta la durata (TTL) per i socket UDP. Il valore predefinito è NX_IP_TIME_TO_LIVE (0x80) al momento della creazione del socket. È possibile eseguire l'override di questo valore chiamando *setsockopt* con questa opzione socket.
- **IP_ADD_MEMBERSHIP**: se impostata, questa opzione Abilita il socket BSD (si applica solo ai socket UDP) per l'aggiunta al gruppo IGMP specificato.
- **IP_DROP_MEMBERSHIP**: se impostata, questa opzione Abilita il socket BSD (si applica solo ai socket UDP) per lasciare il gruppo IGMP specificato.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come usare NetX BSD è illustrato nella figura 1,0 riportata di seguito. In questo esempio il file di inclusione *nx_bsd. h* viene introdotto nella riga 7. Successivamente, l'istanza IP *bsd_ip* e *bsd_pool* pool di pacchetti vengono creati come variabili globali alle righe 20 e 21. Si noti che questa demo usa un driver di rete RAM (virtuale) (riga 41). Il client e il server condividono lo stesso indirizzo IP in una singola istanza IP in questo esempio.

I thread client e server vengono creati alla riga 303 e 309 in *tx_application_define* che imposta l'applicazione ed è definita nelle righe 293-361. Al termine della creazione dell'istanza IP alla riga 327, l'istanza IP è abilitata per i servizi TCP alla riga 350. L'ultimo requisito prima che i servizi BSD possano essere usati è chiamare *bsd_initialize* alla riga 360 per configurare tutte le strutture di dati e NETX e le risorse threadX necessarie per BSD.

Nella funzione entry thread server *thread_1_entry,* definita nella riga 381-397, l'applicazione attende il driver per inizializzare NETX con i parametri di rete. Al termine, viene chiamato *tcpServer,* definito sulla riga 146-253, per gestire i dettagli della configurazione del socket del server TCP.

*tcpServer* crea il socket Master chiamando il servizio *socket* alla riga 159 e lo associa al socket di ascolto usando la chiamata *Bind* alla riga 176. Viene quindi configurata per l'ascolto delle richieste di connessione alla riga 191. Si noti che il socket master non accetta una richiesta di connessione. Viene eseguito in un ciclo continuo che chiama *Select* ogni volta per rilevare le richieste di connessione. Al socket BSD secondario scelto da una matrice di socket BSD viene assegnata la richiesta di connessione dopo la chiamata al servizio *Accept* alla riga 218.

Sul lato client, la funzione di immissione thread del client *thread_0_entry*, definita nelle righe 366-377, deve attendere anche che NETX venga inizializzato dal driver. Qui attendiamo semplicemente il lato server. Chiama quindi *TcpClient* definito alla riga 54-142, per gestire i dettagli della configurazione del socket del client TCP e la richiesta di una connessione TCP.

Il socket client TCP viene creato alla riga 68. Il socket è associato all'indirizzo IP specificato e tenta di connettersi al server TCP chiamando *Connect* alla riga 84. È ora possibile iniziare l'invio e la ricezione di pacchetti.

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
