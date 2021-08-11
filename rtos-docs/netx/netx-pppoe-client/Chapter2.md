---
title: Capitolo 2 - Installazione e uso di Azure RTOS client PpPoE NetX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo Azure RTOS del client PPPoE NetX.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 081fbbd917391a4183488f0fbf124cbd8499c5f8b6d619f7b6cff9f61e6d0bcb
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798793"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-pppoe-client"></a>Capitolo 2 - Installazione e uso di Azure RTOS client PpPoE NetX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo Azure RTOS del client PPPoE NetX.

## <a name="product-distribution"></a>Distribuzione del prodotto

PPPoE Client for NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Il pacchetto include i file seguenti:

 - **nx_pppoe_client.h** File di intestazione per PPPoE Client for NetX
 - **nx_pppoe_client.c** File di origine C per PPPoE Client for NetX
 - **nx_pppoe_client.pdf** Descrizione PDF del client PPPoE per NetX
 - **demo_netx_pppoe_client.c** Dimostrazione del client PPPoE NetX

## <a name="pppoe-client-installation"></a>Installazione del client PPPoE

Per usare il client PPPoE per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory *"\threadx\arm7\green",* i file *nx_pppoe_client.h* e *nx_pppoe_client.c* devono essere copiati in questa directory.

## <a name="using-pppoe-client"></a>Uso del client PPPoE

L'uso del client PPPoE per NetX è semplice. In pratica, il codice dell'applicazione deve includere *nx_pppoe_client.h* dopo aver incluso *tx_api.h* e *nx_api.h*, per poter usare rispettivamente ThreadX e NetX. Dopo *nx_pppoe_client.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione PPPoE Client specificate più avanti in questa guida. L'applicazione deve includere *anche nx_pppoe_client.c* nel processo di compilazione. Questo file deve essere compilato nello stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare il client PPPoE NetX.

## <a name="small-example-system"></a>Small Example System

Di seguito è riportato un esempio che illustra come usare netx PPPoE Client è descritto nella figura 1.1. In questo esempio il file di inclusione PPPoE Client *nx_pppoe_client.h* viene portato alla riga 50. Successivamente, il client PPPoE viene creato in *"thread_0_entry"* alla riga 238. Si noti che il client PPPoE deve essere creato dopo la creazione dell'istanza IP. L'istanza IP e l'istanza PPP vengono create e inizializzate dalla riga 142-220. Il blocco di controllo *"pppoe_client"* del client PPPoE è stato definito in precedenza come variabile globale alla riga 75. Le funzioni di invio e ricezione vengono impostate alla riga 238.

In generale, il modulo PPPoE deve essere usato con il modulo PPP. In questo esempio, il file di inclusione del client PPP *nx_ppp.h* viene portato alla riga 49. Successivamente, il client PPP viene creato alla riga 164. La riga 172 configura la funzione per l'invio di pacchetti PPP. La riga 179-190 configura gli indirizzi IP e definisce il protocollo pap. La riga 104-129 configura il nome utente e la password per il protocollo pap.

Dopo aver stabilito la sessione PPPoE. L'applicazione può *chiamare nx_pppoe_client_session_get* per ottenere le informazioni sulla sessione (indirizzo MAC del server e ID sessione) alla riga 264. PPP o Applicazione può *chiamare* nx_pppoe_client_session_packet_send per inviare pacchetti PPPoE alla riga 283.

Quando l'applicazione non elabora più il traffico PPP, può chiamare nx_pppoe_client_session_terminate *per* terminare la sessione PPPoE.

Si noti che in questo esempio il client PPPoE funziona contemporaneamente con lo stack IP normale e condivide un driver Ethernet. Passare lo stesso driver Ethernet per l'istanza IP normale alla riga 155 e l'istanza del client PPPoE alla riga 298.

> [!NOTE]
> Ridefinire **NX_PHYSICAL_HEADER** a 24 per garantire spazio sufficiente per il riempimento dell'intestazione fisica. Intestazione fisica:14(intestazione Ethernet) + 6 (intestazione PPPoE) + 2 (intestazione PPP) + 2 (allineamento a quattro byte).

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

**Figura 1.1 Esempio di utilizzo del client PPPoE con NetX**

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione del client PPPoE per NetX. L'elenco seguente descrive ogni elemento in dettaglio:

- **NX_DISABLE_ERROR_CHECKING** Questa opzione rimuove il controllo degli errori di base del client PPPoE. Viene in genere usato dopo il debug dell'applicazione.
- **NX_PPPOE_CLIENT_INITIALIZE_DRIVER_ENABLE** Se definito, abilita la funzionalità per inizializzare il driver Ethernet nel modulo PPPoE. Disabilita per impostazione predefinita.
- **NX_PPPOE_CLIENT_THREAD_TIME_SLICE** Opzione di intervallo di tempo per il thread del client PPPoE. Per impostazione predefinita, questo valore è TX_NO_TIME_SLICE.
- **NX_PPPOE_CLIENT_PADI_INIT_TIMEOUT** Definisce la pozione di attesa per la ritrasmissione iniziale dei pacchetti PADI. Per impostazione predefinita, questo valore è 1 secondo.
- **NX_PPPOE_CLIENT_PADI_COUNT** Definisce il numero di reti di trasmissione PADI consentite prima che la connessione venga considerata interrotta. Per impostazione predefinita, questo valore è 4.
- **NX_PPPOE_CLIENT_PADR_INIT_TIMEOUT** Definisce la pozione di attesa per la ritrasmissione iniziale dei pacchetti PADR. Per impostazione predefinita, questo valore è 1 secondo.
- **NX_PPPOE_CLIENT_PADR_COUNT** Definisce il numero di reti di trasmissione PADR consentite prima che la connessione venga considerata interrotta. Per impostazione predefinita, questo valore è 4.
- **NX_PPPOE_CLIENT_MAX_AC_NAME_SIZE** Definisce le dimensioni massime di AC-Name. Per impostazione predefinita, questo valore è 32.
- **NX_PPPOE_CLIENT_MAX_AC_COOKIE_SIZE** Definisce le dimensioni massime di AC-Cookie. Per impostazione predefinita, questo valore è 32.
- **NX_PPPOE_CLIENT_MAX_RELAY_SESSION_ID_SIZE** Definisce le dimensioni massime di Relay-Session-Id. Per impostazione predefinita, questo valore è 12.
- **NX_PPPOE_CLIENT_MIN_PACKET_PAYLOAD_SIZE** Specifica le dimensioni minime del payload del pacchetto per il client PPPoE. Se le dimensioni del payload del pacchetto sono maggiori di questo valore, è possibile evitare il concatenamento dei pacchetti. Per impostazione predefinita, questo valore è 1520 (dimensioni massime del payload di Ethernet 1500, intestazione Ethernet 14, CRC 2 e allineamento a quattro byte 4).
