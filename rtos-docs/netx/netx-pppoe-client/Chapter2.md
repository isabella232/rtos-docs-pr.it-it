---
title: Capitolo 2-installazione e uso del client PPPoE NetX di Azure RTO
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client PPPoE NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 17d910647db7b207280b3fbd9e90c468293a8e67
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822541"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-pppoe-client"></a><span data-ttu-id="e26fd-103">Capitolo 2-installazione e uso del client PPPoE NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e26fd-103">Chapter 2 - Installation and Use of Azure RTOS NetX PPPoE Client</span></span>

<span data-ttu-id="e26fd-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client PPPoE NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="e26fd-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX PPPoE Client component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="e26fd-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="e26fd-105">Product Distribution</span></span>

<span data-ttu-id="e26fd-106">Il client PPPoE per NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="e26fd-106">The PPPoE Client for NetX is available at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span> <span data-ttu-id="e26fd-107">Il pacchetto include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="e26fd-107">The package includes the following files:</span></span>

 - <span data-ttu-id="e26fd-108">**nx_pppoe_client. h** File di intestazione per il client PPPoE per NetX</span><span class="sxs-lookup"><span data-stu-id="e26fd-108">**nx_pppoe_client.h** Header file for PPPoE Client for NetX</span></span>
 - <span data-ttu-id="e26fd-109">**nx_pppoe_client. c** File di origine C per il client PPPoE per NetX</span><span class="sxs-lookup"><span data-stu-id="e26fd-109">**nx_pppoe_client.c** C Source file for PPPoE Client for NetX</span></span>
 - <span data-ttu-id="e26fd-110">**nx_pppoe_client.pdf** Descrizione PDF del client PPPoE per NetX</span><span class="sxs-lookup"><span data-stu-id="e26fd-110">**nx_pppoe_client.pdf** PDF description of PPPoE Client for NetX</span></span>
 - <span data-ttu-id="e26fd-111">**demo_netx_pppoe_client. c** Dimostrazione del client PPPoE NetX</span><span class="sxs-lookup"><span data-stu-id="e26fd-111">**demo_netx_pppoe_client.c** NetX PPPoE Client demonstration</span></span>

## <a name="pppoe-client-installation"></a><span data-ttu-id="e26fd-112">Installazione client PPPoE</span><span class="sxs-lookup"><span data-stu-id="e26fd-112">PPPoE Client Installation</span></span>

<span data-ttu-id="e26fd-113">Per poter usare il client PPPoE per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="e26fd-113">In order to use PPPoE Client for NetX, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="e26fd-114">Se, ad esempio, NetX è installato nella directory *"\threadx\arm7\green"* , i file *nx_pppoe_client. h* e *nx_pppoe_client. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="e26fd-114">For example, if NetX is installed in the directory *“\threadx\arm7\green”* then the *nx_pppoe_client.h* and *nx_pppoe_client.c* files should be copied into this directory.</span></span>

## <a name="using-pppoe-client"></a><span data-ttu-id="e26fd-115">Uso del client PPPoE</span><span class="sxs-lookup"><span data-stu-id="e26fd-115">Using PPPoE Client</span></span>

<span data-ttu-id="e26fd-116">L'uso del client PPPoE per NetX è facile.</span><span class="sxs-lookup"><span data-stu-id="e26fd-116">Using PPPoE Client for NetX is easy.</span></span> <span data-ttu-id="e26fd-117">In pratica, il codice dell'applicazione deve includere *nx_pppoe_client. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX.</span><span class="sxs-lookup"><span data-stu-id="e26fd-117">Basically, the application code must include *nx_pppoe_client.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="e26fd-118">Una volta incluso *nx_pppoe_client. h* , il codice dell'applicazione è quindi in grado di eseguire le chiamate della funzione client PPPoE specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="e26fd-118">Once *nx_pppoe_client.h* is included, the application code is then able to make the PPPoE Client function calls specified later in this guide.</span></span> <span data-ttu-id="e26fd-119">Nell'applicazione deve inoltre essere incluso *nx_pppoe_client. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="e26fd-119">The application must also include *nx_pppoe_client.c* in the build process.</span></span> <span data-ttu-id="e26fd-120">Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e26fd-120">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="e26fd-121">Questo è tutto ciò che è necessario per usare il client PPPoE di NetX.</span><span class="sxs-lookup"><span data-stu-id="e26fd-121">This is all that is required to use NetX PPPoE Client.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="e26fd-122">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="e26fd-122">Small Example System</span></span>

<span data-ttu-id="e26fd-123">Di seguito è riportato un esempio che illustra come usare NetX PPPoE client è descritto nella figura 1,1.</span><span class="sxs-lookup"><span data-stu-id="e26fd-123">The following is an example that illustrates how to use NetX PPPoE Client is described in Figure 1.1.</span></span> <span data-ttu-id="e26fd-124">In questo esempio il file di inclusione client PPPoE *nx_pppoe_client. h* viene portato alla riga 50.</span><span class="sxs-lookup"><span data-stu-id="e26fd-124">In this example, the PPPoE Client include file *nx_pppoe_client.h* is brought in at line 50.</span></span> <span data-ttu-id="e26fd-125">Successivamente, il client PPPoE viene creato in *"thread_0_entry"* alla riga 238.</span><span class="sxs-lookup"><span data-stu-id="e26fd-125">Next, PPPoE Client is created in *”thread_0_entry”* at line 238.</span></span> <span data-ttu-id="e26fd-126">Si noti che il client PPPoE deve essere creato dopo avere creato l'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="e26fd-126">Note that PPPoE Client should be created after create the IP instance.</span></span> <span data-ttu-id="e26fd-127">L'istanza IP e l'istanza di PPP vengono create e inizializzate line142-220.</span><span class="sxs-lookup"><span data-stu-id="e26fd-127">The IP instance and PPP instance are created and initialized line142-220.</span></span> <span data-ttu-id="e26fd-128">Il blocco di controllo client PPPoE *"pppoe_client"* è stato definito come variabile globale alla riga 75 in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e26fd-128">The PPPoE Client control block *“pppoe_client”* was defined as a global variable at line 75 previously.</span></span> <span data-ttu-id="e26fd-129">Le funzioni di trasmissione e ricezione vengono impostate alla riga 238.</span><span class="sxs-lookup"><span data-stu-id="e26fd-129">The send and receive functions are set at line 238.</span></span>

<span data-ttu-id="e26fd-130">In generale, è consigliabile usare il modulo PPPoE con il modulo PPP.</span><span class="sxs-lookup"><span data-stu-id="e26fd-130">In general, PPPoE module should be used with PPP module.</span></span> <span data-ttu-id="e26fd-131">In questo esempio, il client PPP include il file *nx_ppp. h* viene portato alla riga 49.</span><span class="sxs-lookup"><span data-stu-id="e26fd-131">In this example, the PPP Client include file *nx_ppp.h* is brought in at line 49.</span></span> <span data-ttu-id="e26fd-132">Successivamente, il client PPP viene creato alla riga 164.</span><span class="sxs-lookup"><span data-stu-id="e26fd-132">Next, PPP Client is created at line 164.</span></span> <span data-ttu-id="e26fd-133">Riga 172 impostare la funzione per l'invio del pacchetto PPP.</span><span class="sxs-lookup"><span data-stu-id="e26fd-133">Line 172 setup the function to send PPP packet.</span></span> <span data-ttu-id="e26fd-134">Riga 179-190 installazione degli indirizzi IP e definizione del protocollo PAP.</span><span class="sxs-lookup"><span data-stu-id="e26fd-134">Line 179-190 setup the IP addresses and define the pap protocol.</span></span> <span data-ttu-id="e26fd-135">Riga 104-129 impostare il nome utente e la password per il protocollo PAP.</span><span class="sxs-lookup"><span data-stu-id="e26fd-135">Line 104-129 setup the user name and password for pap protocol.</span></span>

<span data-ttu-id="e26fd-136">Dopo la sessione PPPoE stabilita.</span><span class="sxs-lookup"><span data-stu-id="e26fd-136">After the PPPoE session established.</span></span> <span data-ttu-id="e26fd-137">L'applicazione può chiamare *nx_pppoe_client_session_get* per ottenere le informazioni sulla sessione, ovvero l'indirizzo MAC del server e l'ID sessione, alla riga 264.</span><span class="sxs-lookup"><span data-stu-id="e26fd-137">The application can call *nx_pppoe_client_session_get* to get the session information (server MAC address and session id) at line 264.</span></span> <span data-ttu-id="e26fd-138">Il PPP o l'applicazione può chiamare *nx_pppoe_client_session_packet_send* per inviare il pacchetto PPPoE alla riga 283.</span><span class="sxs-lookup"><span data-stu-id="e26fd-138">PPP or Application can call *nx_pppoe_client_session_packet_send* to send PPPoE packet at line 283.</span></span>

<span data-ttu-id="e26fd-139">Quando l'applicazione non elabora più il traffico PPP, l'applicazione può chiamare *nx_pppoe_client_session_terminate* per terminare la sessione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="e26fd-139">When the application no longer process PPP traffic, the application can call *nx_pppoe_client_session_terminate* to terminate the PPPoE session.</span></span>

<span data-ttu-id="e26fd-140">Si noti che in questo esempio il client PPPoE funziona con lo stack IP normale e condivide un driver Ethernet.</span><span class="sxs-lookup"><span data-stu-id="e26fd-140">Note, in this example, PPPoE Client work with normal IP stack at the same time, and share one Ethernet driver.</span></span> <span data-ttu-id="e26fd-141">Passare lo stesso driver Ethernet per l'istanza IP normale alla riga 155 e l'istanza del client PPPoE alla riga 298.</span><span class="sxs-lookup"><span data-stu-id="e26fd-141">Pass the same Ethernet driver for normal IP instance at line 155 and PPPoE Client instance at line 298.</span></span>

> [!NOTE]
> <span data-ttu-id="e26fd-142">Ridefinire **NX_PHYSICAL_HEADER** a 24 per garantire spazio sufficiente per la compilazione dell'intestazione fisica.</span><span class="sxs-lookup"><span data-stu-id="e26fd-142">Redefine **NX_PHYSICAL_HEADER** to 24 to ensure enough space for filling in physical header.</span></span> <span data-ttu-id="e26fd-143">Intestazione fisica: 14 (intestazione Ethernet) + 6 (intestazione PPPoE) + 2 (intestazione PPP) + 2 (allineamento a quattro byte).</span><span class="sxs-lookup"><span data-stu-id="e26fd-143">Physical header:14(Ethernet header) + 6(PPPoE header) + 2(PPP header) + 2(four-byte alignment).</span></span>

```c
  1 /**************************************************************************/
  2 /**************************************************************************/
  3 /**                                                                       */
  4 /** NetX PPPoE Client stack Component                                     */
  5 /**                                                                       */
  6 /**   This is a small demo of the high-performance NetX PPPoE Client      */
  7 /**   stack. This demo includes IP instance, PPPoE Client and PPP Client  */
  8 /**   stack. Create one IP instance includes two interfaces to support    */
  9 /**   for normal IP stack and PPPoE Client, PPPoE Client can use the      */
 10 /**   mutex of IP instance to send PPPoE message when share one Ethernet  */
 11 /**   driver. PPPoE Client work with normal IP instance at the same time. */
 12 /**                                                                       */
 13 /**   Note1: Substitute your Ethernet driver instead of                   */
 14 /**   _nx_ram_network_driver before run this demo                         */
 15 /**                                                                       */
 16 /**   Note2: Prerequisite for using PPPoE.                                */
 17 /**   Redefine NX_PHYSICAL_HEADER to 24 to ensure enough space for filling*/
 18 /**   in physical header. Physical header:14(Ethernet header)             */
 19 /**    + 6(PPPoE header) + 2(PPP header) + 2(four-byte aligment)          */
 20 /**                                                                       */
 21 /**************************************************************************/
 22 /**************************************************************************/
 23
 24
 25       /*****************************************************************/
 26       /*                          NetX Stack                           */
 27       /*****************************************************************/
 28
 29                                             /***************************/
 30                                             /*        PPP Client       */
 31                                             /***************************/
 32
 33                                             /***************************/
 34                                             /*       PPPoE Client      */
 35                                             /***************************/
 36       /***************************/         /***************************/
 37       /*    Normal Ethernet Type */         /*    PPPoE Ethernet Type  */
 38       /***************************/         /***************************/
 39       /***************************/         /***************************/
 40       /*       Interface 0       */         /*       Interface 1       */
 41       /***************************/         /***************************/
 42
 43       /*****************************************************************/
 44       /*                       Ethernet Dirver                         */
 45       /*****************************************************************/
 46
 47 #include   "tx_api.h"
 48 #include   "nx_api.h"
 49 #include   "nx_ppp.h"
 50 #include   "nx_pppoe_client.h"
 51
 52 /* Defined NX_PPP_PPPOE_ENABLE if use Express Logic's PPP, since PPP module has been modified
       to match PPPoE moduler under this definition.  */
 53 #ifdef NX_PPP_PPPOE_ENABLE
 54
 55 /* If the driver is not initialized in other module, define NX_PPPOE_CLIENT_INITIALIZE_DRIVER_ENABLE
       to initialize the driver in PPPoE module .
 56    In this demo, the driver has been initialized in IP module.  */
 57 #ifndef NX_PPPOE_CLIENT_INITIALIZE_DRIVER_ENABLE
 58
 59 /* Define the block size.  */
 60 #define     NX_PACKET_POOL_SIZE     ((1536 + sizeof(NX_PACKET)) * 30)
 61 #define     DEMO_STACK_SIZE         2048
 62 #define     PPPOE_THREAD_SIZE       2048
 63
 64 /* Define the ThreadX and NetX object control blocks...  */
 65 TX_THREAD               thread_0;
 66
 67 /* Define the packet pool and IP instance for normal IP instnace.  */
 68 NX_PACKET_POOL          pool_0;
 69 NX_IP                   ip_0;
 70
71 /* Define the PPP Client instance.  */
 72 NX_PPP                  ppp_client;
 73
 74 /* Define the PPPoE Client instance.  */
 75 NX_PPPOE_CLIENT         pppoe_client;
 76
 77 /* Define the counters.  */
 78 CHAR                    *pointer;
 79 ULONG                   error_counter;
 80
 81 /* Define thread prototypes.  */
 82 void    thread_0_entry(ULONG thread_input);
 83
 84 /***** Substitute your PPP driver entry function here *********/
 85 extern void    _nx_ppp_driver(NX_IP_DRIVER *driver_req_ptr);
 86
 87 /***** Substitute your Ethernet driver entry function here *********/
 88 extern void    _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);
 89
 90 /* Define the porting layer function for Express Logic's PPP to simulate TTP's PPP.
 91    Functions to be provided by PPP for calling by the PPPoE Stack.  */
 92 void    ppp_client_packet_send(NX_PACKET *packet_ptr);
 93 void    pppoe_client_packet_receive(NX_PACKET *packet_ptr);
 94
 95 /* Define main entry point.  */
 96
 97 int main()
 98 {
 99
100     /* Enter the ThreadX kernel.  */
101     tx_kernel_enter();
102 }
103
104 UINT generate_login(CHAR *name, CHAR *password)
105 {
106
107     /* Make a name and password, called "myname" and "mypassword".  */
108     name[0] = 'm';
109     name[1] = 'y';
110     name[2] = 'n';
111     name[3] = 'a';
112     name[4] = 'm';
113     name[5] = 'e';
114     name[6] = (CHAR) 0;
115
116     password[0] = 'm';
117     password[1] = 'y';
118     password[2] = 'p';
119     password[3] = 'a';
120     password[4] = 's';
121     password[5] = 's';
122     password[6] = 'w';
123     password[7] = 'o';
124     password[8] = 'r';
125     password[9] = 'd';
126     password[10] = (CHAR) 0;
127
128     return(NX_SUCCESS);
129 }
130
131 /* Define what the initial system looks like.  */
132
133 void    tx_application_define(void *first_unused_memory)
134 {
135
136 UINT    status;
137
138     /* Setup the working pointer.  */
139     pointer =  (CHAR *) first_unused_memory;
140
141     /* Initialize the NetX system.  */
142     nx_system_initialize();
143
144     /* Create a packet pool for normal IP instance.  */
145     status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool",
146                                    (1536 + sizeof(NX_PACKET)),
147                                    pointer, NX_PACKET_POOL_SIZE);
148     pointer = pointer + NX_PACKET_POOL_SIZE;
149
150     /* Check for error.  */
151     if (status)
152         error_counter++;
153
154     /* Create an normal IP instance.  */
155     status = nx_ip_create(&ip_0, "NetX IP Instance", IP_ADDRESS(192, 168, 100, 44), 0xFFFFFF00UL,
156                           &pool_0, _nx_ram_network_driver, pointer, 2048, 1);
157     pointer = pointer + 2048;
158
159     /* Check for error.  */
160     if (status)
161         error_counter++;
162
163     /* Create the PPP instance.  */
164     status = nx_ppp_create(&ppp_client, "PPP Instance", &ip_0, pointer, 2048, 1,
165                            &pool_0, NX_NULL, NX_NULL); pointer = pointer + 2048;
166
167     /* Check for PPP create error.   */
168     if (status)
169         error_counter++;
170
171     /* Set the PPP packet send function.  */
172     status = nx_ppp_packet_send_set(&ppp_client, ppp_client_packet_send);
173
174     /* Check for PPP packet send function set error.   */
175     if (status)
176         error_counter++;
177
178     /* Define IP address. This PPP instance is effectively the client since it doesn't have
           any IP addresses. */
179     status = nx_ppp_ip_address_assign(&ppp_client, IP_ADDRESS(0, 0, 0, 0), IP_ADDRESS(0, 0, 0, 0));
180
181     /* Check for PPP IP address assign error.   */
182     if (status)
183         error_counter++;
184
185     /* Setup PAP, this PPP instance is effectively the since it generates the name and password
           for the peer..  */
186     status = nx_ppp_pap_enable(&ppp_client, generate_login, NX_NULL);
187
188     /* Check for PPP PAP enable error.  */
189     if (status)
190         error_counter++;
191
192     /* Attach an interface for PPP.  */
193     status = nx_ip_interface_attach(&ip_0, "Second Interface For PPP", IP_ADDRESS(0, 0, 0, 0), 0,
                                        nx_ppp_driver);
194
195     /* Check for error.  */
196     if (status)
197         error_counter++;
198
199     /* Enable ARP and supply ARP cache memory for Normal IP Instance.  */
200     status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
201     pointer = pointer + 1024;
202
203     /* Check for ARP enable errors.  */
204     if (status)
205         error_counter++;
206
207     /* Enable ICMP */
208     status = nx_icmp_enable(&ip_0);
209     if(status)
210         error_counter++;
211
212     /* Enable UDP traffic.  */
213     status =  nx_udp_enable(&ip_0);
214     if (status)
215         error_counter++;
216
217     /* Enable TCP traffic.  */
218     status =  nx_tcp_enable(&ip_0);
219     if (status)
220         error_counter++;
221
222     /* Create the main thread.  */
223     tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
224                      pointer, DEMO_STACK_SIZE,
225                      4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);
226     pointer =  pointer + DEMO_STACK_SIZE;
227
228 }
229
230 /* Define the test threads.  */
231
232 void    thread_0_entry(ULONG thread_input)
233 {
234 UINT    status;
235 ULONG   ip_status;
236
237     /* Create the PPPoE instance.  */
238     status =  nx_pppoe_client_create(&pppoe_client, (UCHAR *)"PPPoE Client",  &ip_0,  0,
        &pool_0, pointer, PPPOE_THREAD_SIZE, 4, _nx_ram_network_driver, pppoe_client_packet_receive);
239     pointer = pointer + PPPOE_THREAD_SIZE;
240     if (status)
241     {
242         error_counter++;
243         return;
244     }
245
246     /* Establish PPPoE Client sessione.  */
247     status = nx_pppoe_client_session_connect(&pppoe_client, NX_WAIT_FOREVER);
248     if (status)
249     {
250         error_counter++;
251         return;
252     }
253
254     /* Wait for the link to come up.  */
255     status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_ADDRESS_RESOLVED,
                                              &ip_status, NX_WAIT_FOREVER);
256     if (status)
257     {
258         error_counter++;
259         return;
260     }
261
262     /* Get the PPPoE Server physical address and Session ID after establish PPPoE Session.  */
263     /*
264     status = nx_pppoe_client_session_get(&pppoe_client, &server_mac_msw,
                                             &server_mac_lsw, &session_id);
265     if (status)
266         error_counter++;
267     */
268 }
269
270 /* PPPoE Client receive function.  */
271 void    pppoe_client_packet_receive(NX_PACKET *packet_ptr)
272 {
273
274     /* Call PPP Client to receive the PPP data fame.  */
275     nx_ppp_packet_receive(&ppp_client, packet_ptr);
276 }
277
278 /* PPP Client send function.  */
279 void    ppp_client_packet_send(NX_PACKET *packet_ptr)
280 {
281
282     /* Directly Call PPPoE send function to send out the data through PPPoE module.  */
283     nx_pppoe_client_session_packet_send(&pppoe_client, packet_ptr);
284 }
285 #endif /* NX_PPPOE_CLIENT_INITIALIZE_DRIVER_ENABLE  */
286
287 #endif /* NX_PPP_PPPOE_ENABLE  */
```

<span data-ttu-id="e26fd-144">**Figura 1,1 esempio di utilizzo del client PPPoE con NetX**</span><span class="sxs-lookup"><span data-stu-id="e26fd-144">**Figure 1.1 Example of PPPoE Client use with NetX**</span></span>

## <a name="configuration-options"></a><span data-ttu-id="e26fd-145">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="e26fd-145">Configuration Options</span></span>

<span data-ttu-id="e26fd-146">Sono disponibili diverse opzioni di configurazione per la creazione di client PPPoE per NetX.</span><span class="sxs-lookup"><span data-stu-id="e26fd-146">There are several configuration options for building PPPoE Client for NetX.</span></span> <span data-ttu-id="e26fd-147">L'elenco seguente descrive tutti i dettagli:</span><span class="sxs-lookup"><span data-stu-id="e26fd-147">The following list describes each in detail:</span></span>

- <span data-ttu-id="e26fd-148">**NX_DISABLE_ERROR_CHECKING** Definita, questa opzione rimuove il controllo degli errori client PPPoE di base.</span><span class="sxs-lookup"><span data-stu-id="e26fd-148">**NX_DISABLE_ERROR_CHECKING** Defined, this option removes the basic PPPoE Client error checking.</span></span> <span data-ttu-id="e26fd-149">Viene in genere usato dopo il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e26fd-149">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="e26fd-150">**NX_PPPOE_CLIENT_INITIALIZE_DRIVER_ENABLE** Se definito, Abilita la funzionalità per inizializzare il driver Ethernet nel modulo PPPoE.</span><span class="sxs-lookup"><span data-stu-id="e26fd-150">**NX_PPPOE_CLIENT_INITIALIZE_DRIVER_ENABLE** If defined, enables the feature to initialize the Ethernet driver in PPPoE module.</span></span> <span data-ttu-id="e26fd-151">Viene disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e26fd-151">It disables by default.</span></span>
- <span data-ttu-id="e26fd-152">**NX_PPPOE_CLIENT_THREAD_TIME_SLICE** Opzione relativa al tempo di sezionamento per il thread del client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="e26fd-152">**NX_PPPOE_CLIENT_THREAD_TIME_SLICE** Time-slice option for PPPoE Client thread.</span></span> <span data-ttu-id="e26fd-153">Per impostazione predefinita, questo valore è TX_NO_TIME_SLICE.</span><span class="sxs-lookup"><span data-stu-id="e26fd-153">By default, this value is TX_NO_TIME_SLICE.</span></span>
- <span data-ttu-id="e26fd-154">**NX_PPPOE_CLIENT_PADI_INIT_TIMEOUT** Definisce la pozione di attesa per la ritrasmissione iniziale dei pacchetti PADI.</span><span class="sxs-lookup"><span data-stu-id="e26fd-154">**NX_PPPOE_CLIENT_PADI_INIT_TIMEOUT** This defines the wait potion for initial retransmitting PADI packets.</span></span> <span data-ttu-id="e26fd-155">Per impostazione predefinita, questo valore è di 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="e26fd-155">By default, this value is 1 second.</span></span>
- <span data-ttu-id="e26fd-156">**NX_PPPOE_CLIENT_PADI_COUNT** Questo consente di definire il numero di ritiri di trasmissione PADI consentiti prima che la connessione venga considerata interruppe.</span><span class="sxs-lookup"><span data-stu-id="e26fd-156">**NX_PPPOE_CLIENT_PADI_COUNT** This defines how many PADI transmit retires are allowed before the connection is deemed broken.</span></span> <span data-ttu-id="e26fd-157">Per impostazione predefinita, questo valore è 4.</span><span class="sxs-lookup"><span data-stu-id="e26fd-157">By default, this value is 4.</span></span>
- <span data-ttu-id="e26fd-158">**NX_PPPOE_CLIENT_PADR_INIT_TIMEOUT** Definisce la pozione di attesa per la ritrasmissione iniziale dei pacchetti PADR.</span><span class="sxs-lookup"><span data-stu-id="e26fd-158">**NX_PPPOE_CLIENT_PADR_INIT_TIMEOUT** This defines the wait potion for initial retransmitting PADR packets.</span></span> <span data-ttu-id="e26fd-159">Per impostazione predefinita, questo valore è di 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="e26fd-159">By default, this value is 1 second.</span></span>
- <span data-ttu-id="e26fd-160">**NX_PPPOE_CLIENT_PADR_COUNT** Questo consente di definire il numero di retire di trasmissione PADR consentite prima che la connessione venga considerata interruppe.</span><span class="sxs-lookup"><span data-stu-id="e26fd-160">**NX_PPPOE_CLIENT_PADR_COUNT** This defines how many PADR transmit retires are allowed before the connection is deemed broken.</span></span> <span data-ttu-id="e26fd-161">Per impostazione predefinita, questo valore è 4.</span><span class="sxs-lookup"><span data-stu-id="e26fd-161">By default, this value is 4.</span></span>
- <span data-ttu-id="e26fd-162">**NX_PPPOE_CLIENT_MAX_AC_NAME_SIZE** Definisce la dimensione massima del nome AC.</span><span class="sxs-lookup"><span data-stu-id="e26fd-162">**NX_PPPOE_CLIENT_MAX_AC_NAME_SIZE** This defines the max size of AC-Name.</span></span> <span data-ttu-id="e26fd-163">Per impostazione predefinita, questo valore è 32.</span><span class="sxs-lookup"><span data-stu-id="e26fd-163">By default, this value is 32.</span></span>
- <span data-ttu-id="e26fd-164">**NX_PPPOE_CLIENT_MAX_AC_COOKIE_SIZE** Definisce le dimensioni massime del cookie AC.</span><span class="sxs-lookup"><span data-stu-id="e26fd-164">**NX_PPPOE_CLIENT_MAX_AC_COOKIE_SIZE** This defines the max size of AC-Cookie.</span></span> <span data-ttu-id="e26fd-165">Per impostazione predefinita, questo valore è 32.</span><span class="sxs-lookup"><span data-stu-id="e26fd-165">By default, this value is 32.</span></span>
- <span data-ttu-id="e26fd-166">**NX_PPPOE_CLIENT_MAX_RELAY_SESSION_ID_SIZE** Definisce le dimensioni massime di relay-Session-ID. Per impostazione predefinita, questo valore è 12.</span><span class="sxs-lookup"><span data-stu-id="e26fd-166">**NX_PPPOE_CLIENT_MAX_RELAY_SESSION_ID_SIZE** This defines the max size of Relay-Session-Id. By default, this value is 12.</span></span>
- <span data-ttu-id="e26fd-167">**NX_PPPOE_CLIENT_MIN_PACKET_PAYLOAD_SIZE** Specifica le dimensioni minime del payload del pacchetto per il client PPPoE.</span><span class="sxs-lookup"><span data-stu-id="e26fd-167">**NX_PPPOE_CLIENT_MIN_PACKET_PAYLOAD_SIZE** Specifies the Minimum packet payload size for PPPoE Client.</span></span> <span data-ttu-id="e26fd-168">Se le dimensioni del payload del pacchetto sono maggiori di questo valore, può evitare di concatenare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e26fd-168">If the packet payload size is greater than this value, can avoid packet chained.</span></span> <span data-ttu-id="e26fd-169">Per impostazione predefinita, questo valore è 1520 (la dimensione massima del payload è Ethernet 1500, l'intestazione Ethernet 14, l'allineamento CRC 2 e 4 byte).</span><span class="sxs-lookup"><span data-stu-id="e26fd-169">By default, this value is 1520 (Maximum Payload Size of Ethernet 1500, Ethernet Header 14, CRC 2 and Four-byte alignment 4).</span></span>
