---
title: Capitolo 2-installazione e uso di Azure RTO NetX Duo HTTP
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP RTO NetX duo di Azure.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9a3ea37b180ab57a8dcd269092638fa74589836a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821869"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-http"></a>Capitolo 2-installazione e uso di Azure RTO NetX Duo HTTP

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP RTO NetX duo di Azure.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO NetX Duo può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netxduo/](https://github.com/azure-rtos/netxduo/) .

 - **nxd_http_client. h** File di intestazione per il client HTTP per NetX Duo
 - **nxd_http_server. h** File di intestazione per il server HTTP per NetX Duo
 - **nxd_http_client. c** File di origine C per il client HTTP per NetX Duo
 - **nxd_http_server. c** File di origine C per il server HTTP per NetX Duo
 - **nx_md5. c** Algoritmi digest MD5
 - **filex_stub. h** File stub se FileX non è presente
 - **nxd_http.pdf** Descrizione di HTTP per NetX Duo
 - **demo_netxduo_http. c** Dimostrazione HTTP di NetX Duo

## <a name="http-installation"></a>Installazione HTTP

Per poter usare HTTP per NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Ad esempio, se NetX Duo è installato nella directory *"\threadx\arm7\green"* , il *nxd_http_client. h*  e *nxd_http_client. c* per le applicazioni client http di NETX duo e *nxd_http_server. h* e *Nxd_http_server. c* per le applicazioni server http NETX Duo. *nx_md5. c* deve essere copiato in questa directory. Per la demo ' RAM driver ' Application NetX Duo HTTP client and server i file devono essere copiati nella stessa directory.

## <a name="using-http"></a>Uso di HTTP

L'uso di HTTP per NetX Duo è facile. In pratica, il codice dell'applicazione deve includere *nxd_http_client. h* e/o *nxd_http_server. h* dopo aver incluso *tx_api. h*, *fx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX, FILEX e NETX Duo. Una volta inclusi i file di intestazione HTTP, il codice dell'applicazione è in grado di eseguire le chiamate di funzione HTTP specificate più avanti in questa guida. L'applicazione deve includere anche *nxd_http_client. c*, *nxd_http_server. c* e *MD5. c* nel processo di compilazione. Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX Duo HTTP.

> [!NOTE]
> Se NX_HTTP_DIGEST_ENABLE non viene specificato nel processo di compilazione, non è necessario aggiungere il file MD5. c all'applicazione. Analogamente, se non sono richieste funzionalità client HTTP, il file *nxd_http_client. c* può essere omesso.

> [!NOTE]
> Poiché HTTP usa i servizi TCP NetX Duo, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di usare http.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come è facile usare NetX Duo HTTP è descritto nella figura 1,1 riportata di seguito. Questo esempio funziona con i servizi "Duo" disponibili nella posizione HTTP di NetX duo di #define USE_DUO alla riga 23. In caso contrario, usa l'equivalente HTTP legacy di NetX (solo per IPv4). Gli sviluppatori sono invitati a eseguire la migrazione di applicazioni esistenti a usando i servizi HTTP di NetX Duo.

Per specificare la comunicazione IPv6, l'applicazione definisce IPTYPE a IPv6 nella riga 24.

In questo esempio i file di inclusione HTTP *nxd_http_client. h* e *nxd_http_server. h* vengono introdotti nella riga 8 e 9. Successivamente, il thread del server HTTP helper, il pool di pacchetti e l'istanza IP vengono creati nelle righe 89 – 112. L'istanza IP del server HTTP deve essere abilitata per TCP, come illustrato nella riga 137. Il server HTTP viene quindi creato in alla riga 159.

Viene quindi creato il client HTTP. Prima viene creato il thread del client nella riga 172, seguito dal pool di pacchetti e dall'istanza IP, in modo analogo al server HTTP, nelle righe 186 – 200. Anche in questo caso l'istanza IP del client HTTP deve essere abilitata per TCP (riga 217).

Il thread del server HTTP viene eseguito e la prima attività è convalidare il proprio indirizzo IP con NetX Duo, che esegue nelle righe 423-450. Il server HTTP ora è pronto per l'esecuzione di richieste.

La prima attività del thread client HTTP è creare e formattare il supporto FileX (righe 236 e 260. Dopo l'inizializzazione del supporto, il client HTTP viene creato nella riga 271. Questa operazione deve essere eseguita prima che il server HTTP possa soddisfare le richieste HTTP. Deve quindi convalidare l'indirizzo IP con NetX duo che esegue nelle righe 282 – 316. Il client HTTP quindi crea e invia il file client_test.html al server HTTP, attende brevemente, quindi tenta di leggere il file dal server HTTP.

> [!NOTE]
> L'API client HTTP usa un servizio diverso se IPv6 non è abilitato (*nx_http_client_put_start* alla riga 343 e *nx_http_client_get_start* nella riga 399). Questo consente a NetX duo di supportare le applicazioni client HTTP NetX esistenti.

> [!NOTE]
> Le chiamate API client HTTP vengono effettuate con timeout relativamente brevi. Potrebbe essere necessario estendere tali timeout se un client HTTP sta comunicando con un server occupato o remoto in un processore più lento.

```c
1    /* This is a small demo of the NetX Duo HTTP Client Server API running on a
2       high-performance NetX Duo TCP/IP stack. This demo is applicable for
3       either IPv4 or IPv6 enabled applications. */
4    
5    #include   "tx_api.h"
6    #include   "fx_api.h"
7    #include   "nx_api.h"
8    #include   "nxd_http_client.h"
9    #include   "nxd_http_server.h"
10   
11   #define     DEMO_STACK_SIZE         2048  
12   
13   /* Set up FileX and file memory resources. */
14   CHAR            *ram_disk_memory;
15   FX_MEDIA        ram_disk;
16   unsigned char   media_memory[512];
17      
18   /* Define device drivers. */
19   extern void _fx_ram_driver(FX_MEDIA *media_ptr);
20   VOID        _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);
22   
23   #define USE_DUO        /* Use the duo service (not legacy netx) */
24   #define IPTYPE   6       /* Send packets over IPv6 */
25
26   /* Set up the HTTP client. */
27   TX_THREAD       client_thread;
28   NX_PACKET_POOL  client_pool;
29   NX_HTTP_CLIENT  my_client;
30   NX_IP           client_ip;
31   #define         CLIENT_PACKET_SIZE  (NX_HTTP_SERVER_MIN_PACKET_SIZE * 2)
32   void            thread_client_entry(ULONG thread_input);
33   
34   #define HTTP_SERVER_ADDRESS  IP_ADDRESS(1,2,3,4)
35   #define HTTP_CLIENT_ADDRESS  IP_ADDRESS(1,2,3,5)
36   
37   /* Set up the HTTP server */
38   
39   NX_HTTP_SERVER  my_server;
40   NX_PACKET_POOL  server_pool;
41   TX_THREAD       server_thread;
42   NX_IP           server_ip;
43   #define         SERVER_PACKET_SIZE  (NX_HTTP_SERVER_MIN_PACKET_SIZE * 2)
44   
45   void            thread_server_entry(ULONG thread_input);
46   #ifdef FEATURE_NX_IPV6
47   NXD_ADDRESS     server_ip_address;
48   #endif
49   
50   
51   /* Define the application's authentication check. This is called by
52      the HTTP server whenever a new request is received. */
53   UINT  authentication_check(NX_HTTP_SERVER *server_ptr, UINT request_type,
54               CHAR *resource, CHAR **name, CHAR **password, CHAR **realm)
55   {
56   
57       /* Just use a simple name, password, and realm for all
58          requests and resources. */
59       *name =     "name";
60       *password = "password";
61       *realm =    "NetX Duo HTTP demo";
62   
63       /* Request basic authentication. */
64       return(NX_HTTP_BASIC_AUTHENTICATE);
65   }
66   
67   /* Define main entry point. */
68   
69   int main()
70   {
71   
72       /* Enter the ThreadX kernel. */
73       tx_kernel_enter();
74   }
75   
76   
77   /* Define what the initial system looks like. */
78   void    tx_application_define(void *first_unused_memory)
79   {
80   
81   CHAR    *pointer;
82   UINT    status;
83   
84       
85       /* Setup the working pointer. */
86       pointer =  (CHAR *) first_unused_memory;
87   
88       /* Create a helper thread for the server. */
89       tx_thread_create(&server_thread, "HTTP Server thread", thread_server_entry, 0,  
90                        pointer, DEMO_STACK_SIZE,
91                        1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
92   
93       pointer =  pointer + DEMO_STACK_SIZE;
94   
95       /* Initialize the NetX system. */
96       nx_system_initialize();
97   
98       /* Create the server packet pool. */
99       status =  nx_packet_pool_create(&server_pool, "HTTP Server Packet Pool",
        SERVER_PACKET_SIZE, pointer, SERVER_PACKET_SIZE*4);
100
101  
102      pointer = pointer + SERVER_PACKET_SIZE * 4;
103  
104      /* Check for pool creation error. */
105      if (status)
106      {
107  
108          return;
109      }
110  
111      /* Create an IP instance. */
112      status = nx_ip_create(&server_ip, "HTTP Server IP", HTTP_SERVER_ADDRESS,
113                            0xFFFFFF00UL, &server_pool, _nx_ram_network_driver,
114                            pointer, 4096, 1);
115  
116      pointer =  pointer + 4096;
117  
118      /* Check for IP create errors. */
119      if (status)
120      {
121          printf("nx_ip_create failed. Status 0x%x\n", status);
122          return;
123      }
124  
125      /* Enable ARP and supply ARP cache memory for the server IP instance. */
126      status = nx_arp_enable(&server_ip, (void *) pointer, 1024);
127  
128      /* Check for ARP enable errors. */
129      if (status)
130      {
131          return;
132      }
133  
134      pointer = pointer + 1024;
135  
136       /* Enable TCP traffic. */
137      status = nx_tcp_enable(&server_ip);
138  
139      if (status)
140      {
141          return;
142      }
143  
144  #if (IP_TYPE==6)
145  
146      /* Set up HTTPv6 server, but we have to wait till its address has been
147         validated before we can start the thread_server_entry thread. */
148  
149      /* Set up the server's IPv6 address here. */
150      server_ip_address.nxd_ip_address.v6[3] = 0x105;
151      server_ip_address.nxd_ip_address.v6[2] = 0x0;
152      server_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
153      server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
154      server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
155  
156  #endif
157  
158      /* Create the NetX HTTP Server. */
159      status = nx_http_server_create(&my_server, "My HTTP Server", &server_ip,
            &ram_disk, pointer, 2048, &server_pool, authentication_check,
            NX_NULL);
160
161      if (status)
162      {
163          return;
164      }
165  
166      pointer =  pointer + 2048;
167  
168      /* Save the memory pointer for the RAM disk. */
169      ram_disk_memory =  pointer;
170  
171      /* Create the HTTP client thread. */
172      status = tx_thread_create(&client_thread, "HTTP Client", thread_client_entry, 0,  
173                       pointer, DEMO_STACK_SIZE,
174                       2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
175  
176      pointer =  pointer + DEMO_STACK_SIZE;
177  
178      /* Check for thread create error. */
179      if (status)
180      {
181  
182          return;
183      }
184  
185      /* Create the Client packet pool. */
186      status =  nx_packet_pool_create(&client_pool, "HTTP Client Packet Pool",
 SERVER_PACKET_SIZE, pointer, SERVER_PACKET_SIZE*4);

187
188  
189      pointer = pointer + SERVER_PACKET_SIZE * 4;
190  
191      /* Check for pool creation error. */
192      if (status)
193      {
194  
195          return;
196      }
197  
198  
199      /* Create an IP instance. */
200      status = nx_ip_create(&client_ip, "HTTP Client IP", HTTP_CLIENT_ADDRESS,
201                            0xFFFFFF00UL, &client_pool, _nx_ram_network_driver,
202                            pointer, 2048, 1);
203  
204      pointer =  pointer + 2048;
205  
206      /* Check for IP create errors. */
207      if (status)
208      {
209          return;
210      }
211  
212      nx_arp_enable(&client_ip, (void *) pointer, 1024);
213  
214      pointer =  pointer + 2048;
215  
216       /* Enable TCP traffic. */
217      nx_tcp_enable(&client_ip);
218  
219      return;
220  }
221  
222  
223  VOID thread_client_entry(ULONG thread_input)
224  {
225  
226  UINT            status;
227  NX_PACKET       *my_packet;
228  #ifdef FEATURE_NX_IPV6
229  NXD_ADDRESS     client_ip_address;
230  UINT            address_index;
230  #endif
231  
232  
233      /* Format the RAM disk - the memory for the RAM disk was setup in
234        tx_application_define above. This must be set up before the client(s) start
235        sending requests. */
236      status = fx_media_format(&ram_disk,
237                              _fx_ram_driver,         // Driver entry
238                              ram_disk_memory,        // RAM disk memory pointer
239                              media_memory,           // Media buffer pointer
240                              sizeof(media_memory),   // Media buffer size
241                              "MY_RAM_DISK",          // Volume Name
242                              1,                      // Number of FATs
243                              32,                     // Directory Entries
244                              0,                      // Hidden sectors
245                              256,                    // Total sectors
246                              128,                    // Sector size   
247                              1,                      // Sectors per cluster
248                              1,                      // Heads
249                              1);                     // Sectors per track
250  
251      /* Check the media format status. */
252      if (status != FX_SUCCESS)
253      {
254  
255          /* Error, bail out. */
256          return ;
257      }
258  
259      /* Open the RAM disk. */
260      status =  fx_media_open(&ram_disk, "RAM DISK", _fx_ram_driver, ram_disk_memory,
                media_memory, sizeof(media_memory));
261  
262      /* Check the media open status. */
263      if (status != FX_SUCCESS)
264      {
265  
266          /* Error, bail out. */
267          return ;
268      }
269  
270      /* Create an HTTP client instance. */
271      status = nx_http_client_create(&my_client, "HTTP Client", &client_ip,
                    &client_pool, 600);
272  
273      /* Check status. */
274      if (status != NX_SUCCESS)
275      {
276          return;
277      }
278  
279      /* Attempt to upload a file to the HTTP server. */
280  
281  
282  #if (IPTYPE== 6)
283  
284      /* Relinquish control so the HTTP server can get set up...*/
285      tx_thread_relinquish();
286  
287      /* Set up the client's IPv6 address here. */
288      client_ip_address.nxd_ip_address.v6[3] = 0x101;
289      client_ip_address.nxd_ip_address.v6[2] = 0x0;
290      client_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
291      client_ip_address.nxd_ip_address.v6[0] = 0x20010db1;
292      client_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
293                 
294      /* Here's where we make the HTTP Client IPv6 enabled. */
295  
296      nxd_ipv6_enable(&client_ip);
298      nxd_icmp_enable(&client_ip);     
299      
300      /* Wait till the IP task thread has set the device MAC address. */
302      tx_thread_sleep(100);
303  
305      /* Now update NetX Duo the Client's link local and global IPv6 address. */
306      nxd_ipv6_address_set(&server_ip, 0, NX_NULL, 10, &address_index)
307      nxd_ipv6_ address_set(&server_ip, 0, &client_ip_address, 64, &address_index);
311
313      /* Then make sure NetX Duo has had time to validate the addresses. */
314      
316      tx_thread_sleep(400);
317  
321      /* Now upload an HTML file to the HTTPv6 server. */
322      status =  nxd_http_client_put_start(&my_client, &server_ip_address,
323         "/client_test.htm", "name", "password", 103, 500);
324
325
326      /* Check status. */
327      if (status != NX_SUCCESS)
328      {
329
330          return;
331      }
332      
333
334  #else
335  
336      /* Relinquish control so the HTTP server can get set up...*/
337      tx_thread_relinquish();
338  
339      do
340      {
341      
342          /* Attempt to upload to the HTTP IPv4 server. */
343          status =  nx_http_client_put_start(&my_client, HTTP_SERVER_ADDRESS,
            "/client_test.htm", "name", "password", 103, 500);
344
345  
346          /* Check status. */
347          if (status != NX_SUCCESS)
348          {
349              tx_thread_sleep(100);
350          }
351  
352      } while (status != NX_SUCCESS);
353  
354  
355  #endif  /* (IPTYPE== 6) */
356  
357  
358      /* Allocate a packet. */
359      status =  nx_packet_allocate(&client_pool, &my_packet, NX_TCP_PACKET,
                        NX_WAIT_FOREVER);
360  
361      /* Check status. */
362      if (status != NX_SUCCESS)
363      {
364          return;
365      }
366  
367      /* Build a simple 103-byte HTML page. */
368      nx_packet_data_append(my_packet, "<HTML>\r\n", 8,
369                          &client_pool, NX_WAIT_FOREVER);
370      nx_packet_data_append(my_packet,
371                   "<HEAD><TITLE>NetX HTTP Test</TITLE></HEAD>\r\n", 44,
372                          &client_pool, NX_WAIT_FOREVER);
373      nx_packet_data_append(my_packet, "<BODY>\r\n", 8,
374                          &client_pool, NX_WAIT_FOREVER);
375      nx_packet_data_append(my_packet, "<H1>Another NetX Test Page!</H1>\r\n", 25,
376                          &client_pool, NX_WAIT_FOREVER);
377      nx_packet_data_append(my_packet, "</BODY>\r\n", 9,
378                          &client_pool, NX_WAIT_FOREVER);
379      nx_packet_data_append(my_packet, "</HTML>\r\n", 9,
380                          &client_pool, NX_WAIT_FOREVER);
381  
382      /* Complete the PUT by writing the total length. */
383      status =  nx_http_client_put_packet(&my_client, my_packet, 50);
384  
385      /* Check status. */
386      if (status != NX_SUCCESS)
387      {
388          return;
389      }
390  
391      /* Now GET the test file  */
392  
393  #ifdef USE_DUO
394  
395      status =  nxd_http_client_get_start(&my_client, &server_ip_address,
396                     "/client_test.htm", NX_NULL, 0, "name", "password", 50);
397  #else
398  
399      status =  nx_http_client_get_start(&my_client, HTTP_SERVER_ADDRESS,
                 "/client_test.htm",  NX_NULL, 0, "name", "password", 50);
400
401  #endif
402  
403      /* Check status. */
404      if (status != NX_SUCCESS)
405      {
406          return;
407      }
408  
409      status = nx_http_client_delete(&my_client);
410  
411      return;
413  }
414  
416  /* Define the helper HTTP server thread. */
417  void    thread_server_entry(ULONG thread_input)
418  {
419  
420  UINT            status;
421  #if (IPTYPE == 6)
422  UINT            address_index
423  NXD_ADDRESS     ip_address
424  
425      /* Allow time for the IP task to initialize the driver. */
426      tx_thread_sleep(100);
427
428    ip_address.nxd_ip_version = NX_IP_VERSION_V6;
429    ip_address.nxd_ip_address.v6[0] = 0x20010000;
430    ip_address.nxd_ip_address.v6[1] = 0;
431    ip_address.nxd_ip_address.v6[2] = 0;
432    ip_address.nxd_ip_address.v6[3] = 4;
433  
434      /* Here's where we make the HTTP server IPv6 enabled. */
435      nxd_ipv6_enable(&server_ip);
436      nxd_icmp_enable(&server_ip);
437  
438      /* Wait till the IP task thread has set the device MAC address. */
439      while (server_ip.nx_ip_arp_physical_address_msw == 0 ||
440             server_ip.nx_ip_arp_physical_address_lsw == 0)
441      {
442          tx_thread_sleep(30);
443      }
444  
445      nxd_ipv6_address_set(&server_ip, 0, NX_NULL, 10, &address_index)
446      nxd_ipv6_ address_set(&server_ip, 0, &ip_address, 64, &address_index);
447  
448      /* Wait for NetX Duo to validate server address. */
449      tx_thread_sleep(400);
450  
451  #endif  /* (IPTYPE == 6) */
452  
453      /* OK to start the HTTPv6 Server. */
454      status = nx_http_server_start(&my_server);
455  
456      if (status != NX_SUCCESS)
457      {
458          return;
459      }
460  
461      /* HTTP server ready to take requests! */
462  
463      /* Let the IP threads execute. */
464      tx_thread_relinquish();
465  
466      return;
467  }
```

**Figura 1,1 esempio di utilizzo HTTP con NetX Duo**

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la creazione di HTTP per NetX Duo. Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio. I valori predefiniti sono elencati, ma possono essere ridefiniti prima dell'inclusione di *nxd_http_client. h* e *nxd_http_server. h*:

 - **NX_DISABLE_ERROR_CHECKING** Definita, questa opzione rimuove il controllo degli errori HTTP di base. Viene in genere usato dopo il debug dell'applicazione
 - **NX_HTTP_SERVER_PRIORITY** Priorità del thread del server HTTP. Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.
 - **NX_HTTP_NO_FILEX** Definito, questa opzione fornisce uno stub per le dipendenze FileX. Se questa opzione è definita, il client HTTP funzionerà senza alcuna modifica. Il server HTTP dovrà essere modificato o l'utente dovrà creare un numero limitato di servizi FileX per il corretto funzionamento.
 - **NX_HTTP_TYPE_OF_SERVICE** Tipo di servizio richiesto per le richieste TCP HTTP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.
  - **NX_HTTP_SERVER_THREAD_TIME_SLICE** Numero di cicli del timer che il thread del server può eseguire prima di cedere ai thread con la stessa priorità. Il valore predefinito è 2.
 - **NX_HTTP_FRAGMENT_OPTION** L'abilitazione del frammento per le richieste TCP HTTP. Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP HTTP.
 - **NX_HTTP_SERVER_WINDOW_SIZE**   Dimensioni finestra socket server. Per impostazione predefinita, questo valore è di 2048 byte
 - **NX_HTTP_TIME_TO_LIVE** Specifica il numero di router che questo pacchetto può superare prima che venga eliminato. Il valore predefinito è impostato su 0x80.
 - **NX_HTTP_SERVER_TIMEOUT**   Consente di specificare il numero di cicli ThreadX per i quali i servizi interni sospendono. Il valore predefinito è impostato su 10 secondi (10 * NX_IP_PERIODIC_RATE).
 - **NX_HTTP_SERVER_TIMEOUT_ACCEPT** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_server_socket_accept* . Il valore predefinito è impostato su (10 * NX_IP_PERIODIC_RATE).
 - **NX_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_disconnect* . Il valore predefinito è impostato su 10 secondi (10 * NX_IP_PERIODIC_RATE).
 - **NX_HTTP_SERVER_TIMEOUT_RECEIVE** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_receive* . Il valore predefinito è impostato su 10 secondi (10 * NX_IP_PERIODIC_RATE).
 - **NX_HTTP_SERVER_TIMEOUT_SEND** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_send* . Il valore predefinito è impostato su 10 secondi (10 * NX_IP_PERIODIC_RATE).
 - **NX_HTTP_MAX_HEADER_FIELD** Specifica la dimensione massima del campo dell'intestazione HTTP. Il valore predefinito è 256.
 - **NX_HTTP_MULTIPART_ENABLE** Se definito, Abilita il server HTTP per supportare le richieste HTTP multipart.
 - **NX_HTTP_SERVER_MAX_PENDING**   Specifica il numero di connessioni che possono essere accodate per il server HTTP. Il valore predefinito è impostato su 5.
 - **NX_HTTP_MAX_RESOURCE** Specifica il numero di byte consentiti in un *nome di risorsa* fornito dal client. Il valore predefinito è impostato su 40.
 - **NX_HTTP_MAX_NAME** Specifica il numero di byte consentiti in un *nome utente* fornito dal client. Il valore predefinito è impostato su 20.
 - **NX_HTTP_MAX_PASSWORD** Specifica il numero di byte consentiti in una *password* fornita dal client. Il valore predefinito è impostato su 20.
 - **NX_HTTP_SERVER_MIN_PACKET_SIZE** Specifica la dimensione minima dei pacchetti nel pool specificato al momento della creazione del server. La dimensione minima è necessaria per garantire che l'intestazione HTTP completa possa essere contenuta in un unico pacchetto. Il valore predefinito è impostato su 600.
 - **NX_HTTP_CLIENT_MIN_PACKET_SIZE** Specifica la dimensione minima dei pacchetti nel pool specificato durante la creazione del client. La dimensione minima è necessaria per garantire che l'intestazione HTTP completa possa essere contenuta in un unico pacchetto. Il valore predefinito è impostato su 300.
 - **NX_HTTP_SERVER_RETRY_SECONDS** Imposta il timeout di ritrasmissione del socket del server in secondi. Il valore predefinito è impostato su 2.
 - **NX_HTTP_SERVER_ RETRY_MAX** Questo consente di impostare il numero massimo di ritrasmissioni sul socket del server. Il valore predefinito è impostato su 10.
 - **NX_HTTP_SERVER_ RETRY_SHIFT** Questo valore viene utilizzato per impostare il timeout di ritrasmissione successivo. Il timeout corrente viene moltiplicato per il numero di ritrasmissioni fino a questo punto, spostate in base al valore del turno di timeout del socket. Il valore predefinito è impostato su 1 per raddoppiare il timeout.
 - **NX_HTTP_SERVER_TRANSMIT_QUEUE_DEPTH** Specifica il numero massimo di pacchetti che possono essere accodati nella coda di ritrasmissione del socket server. Se il numero di pacchetti accodati raggiunge questo numero, non sarà più possibile inviare pacchetti fino a quando non vengono rilasciati uno o più pacchetti accodati. Il valore predefinito è impostato su 20.
