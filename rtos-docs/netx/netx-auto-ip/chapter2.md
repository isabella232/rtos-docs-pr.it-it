---
title: Capitolo 2-installazione e uso di Azure RTO NetX AutoIP
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente AutoIP NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 269a3b4e9754fdc19e2cf1482d483fad2b841de9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821515"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-autoip"></a>Capitolo 2-installazione e uso di Azure RTO NetX AutoIP

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente AutoIP NetX di Azure RTO.

## <a name="product-distribution"></a>Distribuzione del prodotto

AutoIP per NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Il pacchetto include tre file di origine, uno di inclusione e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_auto_ip. h**: file di intestazione per NETX AutoIP
- **nx_auto_ip. c**: file di origine c per NETX AutoIP
- **demo_netx_auto_ip. c**: file di origine c per NETX demo AutoIP
- **nx_auto_ip.pdf**: Descrizione PDF di NETX AutoIP

## <a name="autoip-installation"></a>Installazione di AutoIP

Per poter usare NetX AutoIP, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_auto_ip. h*, *nx_auto_ip. c* e *demo_netx_auto_ip. c* devono essere copiati in questa directory.

## <a name="using-autoip"></a>Uso di AutoIP

L'uso di NetX AutoIP è facile. In pratica, il codice dell'applicazione deve includere *nx_auto_ip. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter usare threadX e NETX. Una volta incluso *nx_auto_ip. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione AutoIP specificate più avanti in questa guida. Nell'applicazione deve inoltre essere incluso *nx_auto_ip. c* nel processo di compilazione. Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX AutoIP.

> [!NOTE]
> Poiché AutoIP usa i servizi ARP NetX, è necessario abilitare ARP con la chiamata *nx_arp_enable* prima di usare AutoIP.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come è facile usare NetX AutoIP è descritto nella figura 1,1, riportata di seguito. In questo esempio, il file di inclusione AutoIP *nx_auto_ip. h* viene portato alla riga 002. Successivamente, viene creata l'istanza di NetX AutoIP in "*tx_application_define*" alla riga 090. Si noti che il blocco di controllo NetX AutoIP "auto_ip_0" è stato definito in precedenza come variabile globale alla riga 015. Una volta completata la creazione, viene avviato un AutoIP NetX alla riga 098. L'elaborazione della funzione di callback per la modifica dell'indirizzo IP inizia alla riga 105, che viene usata per gestire i conflitti successivi o la possibile risoluzione degli indirizzi DHCP.

> [!NOTE]
> Nell'esempio seguente si presuppone che il dispositivo host sia un dispositivo a Home singolo. Per un dispositivo multihomed, l'applicazione host può usare il servizio AutoIP NetX *nx_auto_ip_interface_* impostato per specificare un'interfaccia di rete secondaria per verificare la presenza di un indirizzo IP. Per ulteriori informazioni sulla configurazione di applicazioni multihomed, vedere la **Guida dell'utente di NETX** . Si noti inoltre che l'applicazione host deve usare l'API NetX *nx_status_ip_interface_check* per verificare che AutoIP abbia ottenuto un indirizzo IP.

## <a name="example-of-autoip-use-with-netx"></a>Esempio di utilizzo di AutoIP con NetX

```c
000 #include "tx_api.h"
001 #include "nx_api.h"
002 #include "nx_auto_ip.h"
003
004 #define         DEMO_STACK_SIZE         4096
005
006 /* Define the ThreadX and NetX object control blocks... */
007
008 TX_THREAD         thread_0;
009 NX_PACKET_POOL    pool_0;
010 NX_IP             ip_0;
011
012
013 /* Define the AUTO IP structures for the IP instance. */
014
015 NX_AUTO_IP         auto_ip_0;
016
017
018 /* Define the counters used in the demo application... */
019
020 ULONG             thread_0_counter;
021 ULONG             address_changes;
022 ULONG             error_counter;
023
024
025 /* Define thread prototypes. */
026
027 void     thread_0_entry(ULONG thread_input);
028 void     ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address);
029 void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
030
031
032 /* Define main entry point. */
033
034 int main()
035 {
036
037     /* Enter the ThreadX kernel. */
038     tx_kernel_enter();
039 }
040
041
042 /* Define what the initial system looks like. */
043
044 void     tx_application_define(void *first_unused_memory)
045 {
046
047 CHAR     *pointer;
048 UINT     status;
049
050
051     /* Setup the working pointer. */
052     pointer = (CHAR *) first_unused_memory;
053
054     /* Create the main thread. */
055     tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
056                     pointer, DEMO_STACK_SIZE,
057                     16, 16, 1, TX_AUTO_START);
058
059     pointer = pointer + DEMO_STACK_SIZE;
060
061     /* Initialize the NetX system. */
062     nx_system_initialize();
063
064     /* Create a packet pool. */
065     status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 128,
066                                     pointer, 4096);
067                                     pointer = pointer + 4096;
068
069     if (status)
070         error_counter++;
071
072     /* Create an IP instance. */
073     status = nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(0, 0, 0, 0),
074                             0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
075                             pointer, 4096, 1);
076                             pointer = pointer + 4096;
077
078     if (status)
079         error_counter++;
080
081     /* Enable ARP and supply ARP cache memory for IP Instance 0. */
082     status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
083     pointer = pointer + 1024;
084
085     /* Check ARP enable status. */
086     if (status)
087         error_counter++;
088
089     /* Create the AutoIP instance for IP Instance 0. */
090     status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);
091     pointer = pointer + 4096;
092
093     /* Check AutoIP create status. */
094     if (status)
095         error_counter++;
096
097     /* Start AutoIP instances. */
098     status = nx_auto_ip_start(&auto_ip_0, 0 /*IP_ADDRESS(169,254,254,255)*/);
099
100     /* Check AutoIP start status. */
101     if (status)
102         error_counter++;
103
104     /* Register an IP address change function for IP Instance 0. */
105     status = nx_ip_address_change_notify(&ip_0, ip_address_changed,
106                                         (void *) &auto_ip_0);
107
108     /* Check IP address change notify status. */
109     if (status)
110         error_counter++;
111     }
112
113
114     /* Define the test thread. */
115
116     void thread_0_entry(ULONG thread_input)
117     {
118
119     UINT      status;
120     ULONG     actual_status;
121
122
123          /* Wait for IP address to be resolved. */
124         do
125         {
126
127             /* Call IP status check routine. */
128             status = nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED,
129                                         &actual_status, 10000);
130
131         } while (status != NX_SUCCESS);
132
133         /* Since the IP address is resolved at this point, the application
134         can now fully utilize NetX! */
135
136         while(1)
137         {
138
139
140
141             /* Increment thread 0's counter. */
142             thread_0_counter++;
143
144             /* Sleep... */
145             tx_thread_sleep(10);
146         }
147     }
148
149
150     void ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address)
151     {
152
153     ULONG         ip_address;
154     ULONG         network_mask;
155     NX_AUTO_IP    *auto_ip_ptr;
156
157
158     /* Setup pointer to auto IP instance. */
159     auto_ip_ptr = (NX_AUTO_IP *) auto_ip_address;
160
161     /* Pickup the current IP address. */
162     nx_ip_address_get(ip_ptr, &ip_address, &network_mask);
163
164     /* Determine if the IP address has changed back to zero. If so,
165     make sure the AutoIP instance is started. */
166     if (ip_address == 0)
167     {
168
169         /* Get the last AutoIP address for this node. */
170         nx_auto_ip_get_address(auto_ip_ptr, &ip_address);
171
172         /* Start this AutoIP instance. */
173         nx_auto_ip_start(auto_ip_ptr, ip_address);
174     }
175
176     /* Determine if IP address has transitioned to a non local IP address. */
177     else if ((ip_address & 0xFFFF0000UL) != IP_ADDRESS(169, 254, 0, 0))
178     {
179
180         /* Stop the AutoIP processing. */
181         nx_auto_ip_stop(auto_ip_ptr);
182     }
183
184     /* Increment a counter. */
185     address_changes++;
186 }
```

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione di NetX AutoIP. Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:

- **NX_DISABLE_ERROR_CHECKING**: definito, questa opzione rimuove il controllo degli errori di AutoIP di base. Viene in genere usato dopo il debug dell'applicazione.
- **NX_AUTO_IP_PROBE_WAIT**: numero di secondi di attesa prima dell'invio del primo Probe. Per impostazione predefinita, questo valore è definito come 1.
- **NX_AUTO_IP_PROBE_NUM**: numero di probe ARP da inviare. Per impostazione predefinita, questo valore è definito come 3.
- **NX_AUTO_IP_PROBE_MIN**: numero minimo di secondi di attesa tra l'invio di probe. Per impostazione predefinita, questo valore è definito come 1.
- **NX_AUTO_IP_PROBE_MAX**: numero massimo di secondi di attesa tra l'invio di probe. Per impostazione predefinita, questo valore è definito come 2.
- **NX_AUTO_IP_MAX_CONFLICTS**: numero di conflitti di AutoIP prima di aumentare i ritardi di elaborazione. Per impostazione predefinita, questo valore è definito come 10.
- **NX_AUTO_IP_RATE_LIMIT_INTERVAL**: numero di secondi per l'estensione del periodo di attesa quando viene superato il numero totale di conflitti. Per impostazione predefinita, questo valore è definito come 60.
- **NX_AUTO_IP_ANNOUNCE_WAIT**: numero di secondi di attesa prima dell'invio dell'annuncio. Per impostazione predefinita, questo valore è definito come 2.
- **NX_AUTO_IP_ANNOUNCE_NUM**: numero di annunci ARP da inviare. Per impostazione predefinita, questo valore è definito come 2.
- **NX_AUTO_IP_ANNOUNCE_INTERVAL**: numero di secondi di attesa tra le annunci di invio. Per impostazione predefinita, questo valore è definito come 2.
- **NX_AUTO_IP_DEFEND_INTERVAL**: numero di secondi di attesa tra le annunci di difesa. Per impostazione predefinita, questo valore è definito come 10.