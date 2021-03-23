---
title: Capitolo 2-installazione e uso del client DHCP NetX di Azure RTO
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client DHCP NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9224a4df70b8199032066e30108250a3baeb65f5
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822703"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-dhcp-client"></a>Capitolo 2-installazione e uso del client DHCP NetX di Azure RTO

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente DHCP NetX di Azure RTO.

## <a name="product-distribution"></a>Distribuzione del prodotto

DHCP per NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_dhcp. h** File di intestazione per DHCP per NetX

- **nx_dhcp. c** File di origine C per DHCP per NetX

- **nx_dhcp.pdf** Descrizione PDF di DHCP per NetX

- **demo_netx_dhcp. c** Dimostrazione di NetX DHCP

- **demo_netx_multihome_dhcp_client. c** Dimostrazione del client DHCP NetX di DHCP su più interfacce

## <a name="dhcp-installation"></a>Installazione DHCP

Per usare DHCP per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_dhcp. h* e *nx_dhcp. c* devono essere copiati in questa directory.

## <a name="using-dhcp"></a>Utilizzo di DHCP

L'uso di DHCP per NetX è facile. In pratica, il codice dell'applicazione deve includere *nx_dhcp. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX. Una volta incluso *nx_dhcp. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione DHCP specificate più avanti in questa guida. Nell'applicazione deve inoltre essere incluso *nx_dhcp. c* nel processo di compilazione. Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX DHCP.

Si noti che poiché DHCP usa i servizi UDP NetX, è necessario abilitare UDP con la chiamata *nx_udp_enable* prima di usare DHCP.

Per ottenere un indirizzo IP assegnato in precedenza, il client DHCP può avviare il processo DHCP con il messaggio di richiesta e l'opzione 50 "indirizzo IP richiesto" per il server DHCP. Il server DHCP risponderà con un messaggio ACK se l'indirizzo IP viene concesso al client o a un NACK se rifiutato. Nel secondo caso, il client DHCP riavvia il processo DHCP in stato INIT con un messaggio di individuazione e nessun indirizzo IP richiesto. L'applicazione host crea innanzitutto il client DHCP, quindi chiama il servizio API *nx_dhcp_request_client_ip* per impostare l'indirizzo IP richiesto prima di avviare il processo DHCP con *nx_dhcp_start*. Un esempio di applicazione DHCP è disponibile altrove in questo documento per altri dettagli.

## <a name="in-the-bound-state"></a>Nello stato associato

Mentre il client DHCP è nello stato associato, il thread del client DHCP elabora lo stato del client una volta per ogni intervallo (come specificato da NX_DHCP_TIME_INTERVAL) e decrementa il tempo rimanente nel lease IP assegnato al client. Quando il tempo di rinnovo è scaduto, lo stato del client DHCP viene aggiornato allo stato di rinnovo in cui il client richiederà un rinnovo dal server DHCP.


## <a name="sending-dhcp-messages-to-the-server"></a>Invio di messaggi DHCP al server

Il client DHCP dispone di servizi API che consentono all'applicazione host di inviare un messaggio al server DHCP. Si noti che questi servizi non sono destinati all'applicazione host per eseguire manualmente il protocollo client DHCP perché inviano principalmente il messaggio senza necessariamente aggiornare lo stato interno del client DHCP.

  - *nx_dhcp_release*: Invia un messaggio di rilascio al server quando l'applicazione host lascia la rete o deve rinunciare all'indirizzo IP.

  - *nx_dhcp_decline*: Invia un messaggio di rifiuto al server se l'applicazione host determina indipendentemente dal client DHCP che l'indirizzo IP è già in uso.

  - *nx_dhcp_forcerenew*: Invia un messaggio Forcerenew al server

  - *nx_dhcp_send_request*: accetta come argomento un tipo di messaggio DHCP, come specificato in *nx_dhcp. h*, e invia il messaggio al server. Questa operazione viene utilizzata principalmente per l'invio del messaggio di notifica DHCP.

Vedere "*Descrizione dei servizi DHCP*" per altre informazioni su questi servizi in altre parti di questo documento.

## <a name="starting-and-stopping-the-dhcp-client"></a>Avvio e arresto del client DHCP

Per arrestare il client DHCP, indipendentemente dal fatto che abbia raggiunto uno stato associato, l'applicazione host chiama *nx_dhcp_stop*.

Per riavviare un client DHCP, l'applicazione host deve prima arrestare il client DHCP utilizzando il servizio *nx_dhcp_stop* descritto in precedenza. L'host può quindi chiamare *nx_dhcp_start* per riprendere il client DHCP. Se l'applicazione host desidera cancellare un profilo client DHCP precedente, ad esempio uno ottenuto da un server DHCP precedente in un'altra rete, l'applicazione host deve chiamare *nx_dhcp_reinitialize* per eseguire internamente questa attività prima di chiamare nx_dhcp_start.

Una sequenza tipica potrebbe essere:

```C
nx_dhcp_stop(&my_dhcp);

nx_dhcp_reinitialize(&my_dhcp);

nx_dhcp_start(&my_dhcp);
```

Per le applicazioni DHCP in esecuzione su una sola interfaccia DHCP, l'arresto del client DHCP disattiva anche il timer del CLIENT DHCP. Quindi non tiene più traccia del tempo rimanente nel lease IP. L'arresto del client DHCP su una particolare interfaccia non attiverà il timer del client DHCP, ma arresterà gli aggiornamenti del timer fino al tempo rimanente nel lease IP su tale interfaccia.

Pertanto, non è consigliabile arrestare il client DHCP, a meno che l'applicazione host non richieda il riavvio o il cambio di rete.

## <a name="using-the-dhcp-client-with-auto-ip"></a>Uso del client DHCP con IP automatico

Il client DHCP NetX funziona contemporaneamente al protocollo IP automatico nelle applicazioni in cui DHCP e IP automatico garantiscono un indirizzo in cui non è garantito che un server DHCP sia disponibile o non risponde. Tuttavia, se l'host non è in grado di rilevare un server o di ottenere un indirizzo IP assegnato, può passare al protocollo IP automatico per un indirizzo IP locale. Tuttavia, prima di procedere, è consigliabile arrestare temporaneamente il client DHCP mentre l'IP automatico passa attraverso le fasi "probe" e "Defense". Quando un indirizzo IP automatico viene assegnato all'host, il client DHCP può essere riavviato e se un server DHCP diventa disponibile, l'indirizzo IP host può accettare l'indirizzo IP offerto dal server DHCP mentre l'applicazione è in esecuzione.

L'IP automatico di NetX dispone di una notifica di modifica dell'indirizzo per l'host per monitorare le attività in caso di modifica di un indirizzo IP.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come usare NetX è descritto nella figura 1,1 riportata di seguito. Il client DHCP viene creato "*my_thread_entry*" alla riga 101. Al termine della creazione, il processo DHCP viene avviato alla chiamata a *nx_dhcp_start* alla riga 108. A questo punto, i tentativi del client DHCP vengono avviati per contattare il server DHCP. Durante questo processo, il codice dell'applicazione attende che un indirizzo IP valido venga registrato con l'istanza IP usando il servizio *nx_ip_status_check* (o *nx_ip_interface_status_check* per un'interfaccia secondaria) a partire dalla riga 95. Questa operazione viene in genere eseguita in un ciclo con un'opzione di attesa più breve.

Dopo la riga 127, DHCP ha ricevuto un indirizzo IP valido e l'applicazione può continuare, usando i servizi TCP/IP di NetX nel modo desiderato.

```C
#include  "tx_api.h"
#include  "nx_api.h"
#include  "nx_dhcp.h"

#define   DEMO_STACK_SIZE     4096
TX_THREAD        my_thread;
NX_PACKET_POOL     my_pool;
NX_IP          my_ip;
NX_DHCP         my_dhcp;

/* Define function prototypes. */

void  my_thread_entry(ULONG thread_input);
void  my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
{

  /* Enter the ThreadX kernel. */
  tx_kernel_enter();
}


/* Define what the initial system looks like. */

void  tx_application_define(void *first_unused_memory)
{

CHAR  *pointer;
UINT  status;

  
  /* Setup the working pointer. */
  pointer = (CHAR *) first_unused_memory;

  /* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0, 
            pointer, DEMO_STACK_SIZE, 
            2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Initialize the NetX system. */
  nx_system_initialize();

  /* Create a packet pool. */
  status = nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                     1024, pointer, 64000);
  pointer = pointer + 64000;

  /* Check for pool creation error. */
  if (status)
    error_counter++;

  /* Create an IP instance without an IP address. */
  status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
      0xFFFFFF00, &my_pool, my_netx_driver, pointer, 
      DEMO_STACK_SIZE, 1);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Check for IP create errors. */
  if (status)
    error_counter++;

  /* Enable ARP and supply ARP cache memory for my IP Instance. */
  status = nx_arp_enable(&my_ip, (void *) pointer, 1024);
  pointer = pointer + 1024;

  /* Check for ARP enable errors. */
  if (status)
    error_counter++;

  /* Enable UDP. */
  status = nx_udp_enable(&my_ip);
  if (status)
    error_counter++;
}


/* Define my thread. */

void  my_thread_entry(ULONG thread_input)
{

UINT    status;
ULONG    actual_status;
NX_PACKET  *my_packet;

  /* Wait for the link to come up. */
  do
  {

    /* Get the link status. */
    status = nx_ip_status_check(&my_ip, NX_IP_LINK_ENABLED, 
                            &actual_status, 100);

  } while (status != NX_SUCCESS);

  /* Create a DHCP instance. */
  status = nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

  /* Check for DHCP create error. */
  if (status)
    error_counter++;

  /* Start DHCP. */
  nx_dhcp_start(&my_dhcp);

  /* Check for DHCP start error. */
  if (status)
    error_counter++;

  /* Wait for IP address to be resolved through DHCP. */
  nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                        (ULONG *) &status, 100000);

  /* Check to see if we have a valid IP address. */
  if (status)
  {
    error_counter++;
    return;
  }
  else
  {

        /* Yes, a valid IP address is now on lease… All NetX
      services are available.
  }
}
```

Figura 1,1 esempio di uso di DHCP con NetX

## <a name="multi-server-environments"></a>Ambienti multiserver

Nelle reti in cui è presente più di un server DHCP, il client DHCP accetta il primo messaggio di offerta server DHCP ricevuto, avanza sullo stato della richiesta e ignora le altre offerte ricevute.

## <a name="arp-probes"></a>Probe ARP

Il client DHCP può essere configurato in modo da inviare uno o più Probe ARP dopo l'assegnazione di indirizzi IP dal server DHCP per verificare che l'indirizzo IP non sia già in uso. Il passaggio del probe ARP è consigliato da RFC 2131 ed è particolarmente importante in ambienti con più di un server DHCP. Se l'applicazione host abilita l'opzione NX_DHCP_CLIENT_SEND_ARP_PROBE (vedere le **Opzioni di configurazione** nel capitolo due per le opzioni aggiuntive del probe ARP), il client DHCP invierà un probe ARP "autoindirizzato" e aspetterà il tempo specificato per una risposta. Se non viene ricevuto alcun valore, il client DHCP passa allo stato associato. Se viene ricevuta una risposta, il client DHCP presuppone che l'indirizzo sia già in uso. Invia automaticamente un messaggio di rifiuto al server e reinizializza il client per riavviare i probe DHCP dallo stato INIT. Viene riavviata la macchina a stati DHCP e il client invia un altro messaggio di individuazione al server.

## <a name="bootp-protocol"></a>Protocollo BOOTP

Il client DHCP supporta anche il protocollo BOOTP e il protocollo DHCP. Per abilitare questa opzione e utilizzare BOOTP anziché DHCP, l'applicazione host deve impostare l'opzione di configurazione NX_DHCP_BOOTP_ENABLE. L'applicazione host può comunque richiedere indirizzi IP specifici nel protocollo BOOTP. Tuttavia, il client DHCP non supporta il caricamento del sistema operativo host, perché a volte viene usato BOOTP.

## <a name="dhcp-on-a-secondary-interface"></a>DHCP in un'interfaccia secondaria

Il client DHCP NetX può essere eseguito su interfacce secondarie anziché sull'interfaccia primaria predefinita.

Per eseguire NetX DHCP client su un'interfaccia di rete secondaria, l'applicazione host deve impostare l'indice di interfaccia del client DHCP sull'interfaccia secondaria usando il *nx_dhcp_set_interface_index* servizio API. L'interfaccia deve essere già collegata all'interfaccia di rete primaria usando il servizio *nx_ip_interface_attach* . Per ulteriori informazioni sul fissaggio delle interfacce secondarie, vedere la guida dell'utente di NetX.

Nella figura 1,2 è riportato di seguito un esempio di sistema in cui l'applicazione host si connette al server DHCP sull'interfaccia secondaria. Alla riga 65, l'interfaccia secondaria è collegata all'attività IP con un indirizzo IP null. Alla riga 104, dopo la creazione dell'istanza del client DHCP, l'indice dell'interfaccia client DHCP viene impostato su 1 (ad esempio, l'offset dall'interfaccia principale, ovvero l'indice 0), chiamando *nx_dhcp_set_interface_index*. Il client DHCP è quindi pronto per l'avvio nella riga 108.

```C
#include  "tx_api.h"
#include  "nx_api.h"
#include  "nx_dhcp.h"

#define   DEMO_STACK_SIZE     4096
TX_THREAD        my_thread;
NX_PACKET_POOL     my_pool;
NX_IP          my_ip;
NX_DHCP         my_dhcp;

/* Define function prototypes. */

void  my_thread_entry(ULONG thread_input);
void  my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
{

  /* Enter the ThreadX kernel. */
  tx_kernel_enter();
}


/* Define what the initial system looks like. */

void  tx_application_define(void *first_unused_memory)
{

CHAR  *pointer;
UINT  status;

  
  /* Setup the working pointer. */
  pointer = (CHAR *) first_unused_memory;

  /* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0, 
            pointer, DEMO_STACK_SIZE, 
            2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Initialize the NetX system. */
  nx_system_initialize();

  /* Create a packet pool. */
  status = nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                     1024, pointer, 64000);
  pointer = pointer + 64000;

  /* Check for pool creation error. */
  if (status)
    error_counter++;

  /* Create an IP instance without an IP address. */
  status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
       0xFFFFFF00, &my_pool, my_netx_driver, pointer, STACK_SIZE, 1);
  pointer = pointer + DEMO_STACK_SIZE;

  /* Check for IP create errors. */
  if (status)
    error_counter++;

  status = _nx_ip_interface_attach(&ip_0, "port_2", IP_ADDRESS(0, 0, 0,0), 
                            0xFFFFFF00UL, my_netx_driver);
                            
  /* Enable ARP and supply ARP cache memory for my IP Instance. */
  status = nx_arp_enable(&my_ip, (void *) pointer, 1024);
  pointer = pointer + 1024;

  /* Check for ARP enable errors. */
  if (status)
    error_counter++;

  /* Enable UDP. */
  status = nx_udp_enable(&my_ip);
  if (status)
    error_counter++;
}


void  my_thread_entry(ULONG thread_input)
{

UINT    status;
ULONG    status;
NX_PACKET  *my_packet;

  /* Wait for the link to come up. */
  do
  {

    /* Get the link status. */
    status = nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,& status,100);
  } while (status != NX_SUCCESS);

  /* Create a DHCP instance. */
  status = nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

  /* Check for DHCP create error. */
  if (status)
    error_counter++;

  /* Set the DHCP client interface to the secondary interface. 
    status = nx_dhcp_set_interface_index(&my_dhcp, 1);


  /* Start DHCP. */
  nx_dhcp_start(&my_dhcp);

  /* Check for DHCP start error. */
  if (status)
    error_counter++;

  /* Wait for IP address to be resolved through DHCP. */
  nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                        (ULONG *) &status, 100000);

  /* Check to see if we have a valid IP address. */
  if (status)
  {
    error_counter++;
    return;
  }
  else
  {

        /* Yes, a valid IP address is now on lease… All NetX
      services are available.
  }
}
```

Figura 1,2 esempio di DHCP per NetX con supporto multihome

## <a name="dhcp-client-on-multiple-interfaces-simultaneously"></a>Client DHCP su più interfacce simultaneamente

Per eseguire il client DHCP su più interfacce, NX_MAX_PHYSICAL_INTERFACES in *nx_api. h* deve essere impostato sul numero di interfacce fisiche connesse al dispositivo. Per impostazione predefinita, questo valore è 1 (ad esempio, l'interfaccia primaria). Per registrare un'interfaccia aggiuntiva per l'istanza IP, usare il servizio *nx_ip_interface_attach* . Per ulteriori informazioni sul fissaggio delle interfacce secondarie, vedere la guida dell'utente di NetX.

Il passaggio successivo consiste nell'impostare il NX_DHCP_CLIENT_MAX_RECORDS in *nx_dhcp. h* sul numero massimo di interfacce previste per l'esecuzione simultanea di DHCP. Si noti che NX_DHCP_CLIENT_MAX_RECORDS non deve necessariamente essere uguale NX_MAX_PHYSICAL_INTERFACES. Ad esempio, NX_MAX_PHYSICAL_INTERFACES può essere 3 e NX_DHCP_CLIENT_MAX_RECORDS uguale a 2. In questa configurazione, solo due interfacce (e possono essere due delle tre interfacce fisiche in qualsiasi momento) delle tre interfacce fisiche possono eseguire DHCP in un momento qualsiasi. I record client DHCP non dispongono di un mapping uno-a-uno alle interfacce di rete, ad esempio il record client 1 non è correlato automaticamente all'indice di interfaccia fisica 1.

NX_DHCP_CLIENT_MAX_RECORDS possono anche essere impostate su un valore maggiore di NX_MAX_PHYSICAL_INTERFACES, ma ciò creerebbe record client inutilizzati e sarà un uso inefficiente della memoria.

Prima di poter avviare DHCP su qualsiasi interfaccia, l'applicazione deve abilitare tali interfacce chiamando *nx_dhcp_interface_enable*. Si noti che l'eccezione è l'interfaccia primaria abilitata automaticamente nella chiamata *nx_dhcp_create* (e che può essere disabilitata usando il servizio *nx_dhcp_interface_disable* illustrato di seguito).

In qualsiasi momento, un'interfaccia può essere disabilitata per DHCP o DHCP può essere arrestata in tale interfaccia indipendentemente dalle altre interfacce che eseguono DHCP.

Come indicato in precedenza, per abilitare un'interfaccia specifica per DHCP, usare il servizio *nx_dhcp_interface_enable* e specificare l'indice dell'interfaccia fisica nell'argomento di input. È possibile abilitare fino a NX_DHCP_CLIENT_MAX_RECORDS interfacce con l'unica limitazione che l'argomento di input dell'indice di interfaccia sia minore di NX_MAX_PHYSICAL_INTERFACES.

Per avviare DHCP in un'interfaccia specifica, usare il servizio *nx_dhcp_interface_start* . Per avviare DHCP in tutte le interfacce abilitate, usare il servizio *nx_dhcp_start* . (Le interfacce che hanno già avviato DHCP non saranno interessate da *nx_dhcp_start*).

Per arrestare DHCP in un'interfaccia, usare il servizio *nx_dhcp_interface_stop* . È necessario che DHCP sia già stato avviato su tale interfaccia o che venga restituito uno stato di errore. Per arrestare DHCP in tutte le interfacce abilitate, usare il servizio *nx_dhcp_stop* . DHCP può essere arrestato indipendentemente dalle altre interfacce in qualsiasi momento.

La maggior parte dei servizi client DHCP esistenti ha un equivalente ' Interface ', ad esempio *nx_dhcp_interface_release* è l'equivalente specifico dell'interfaccia di *nx_dhcp_release.* Se il client DHCP è configurato per una singola interfaccia, eseguirà la stessa operazione.

Si noti che i servizi client DHCP non specifici dell'interfaccia si applicano in genere a tutte le interfacce, ma non a tutti. Nel secondo caso, il servizio non specifico dell'interfaccia si applica alla prima interfaccia DHCP abilitata disponibile nella ricerca nell'elenco dei record di interfaccia del client DHCP. Vedere la **Descrizione dei servizi** nel capitolo tre per informazioni sul modo in cui viene eseguito un servizio specifico non di interfaccia quando sono abilitate più interfacce per DHCP.

Nella sequenza di esempio riportata di seguito, l'istanza IP dispone di due interfacce di rete e viene eseguita prima DHCP sull'interfaccia secondaria. In un secondo momento, avvia DHCP sull'interfaccia principale. Rilascia quindi l'indirizzo IP sull'interfaccia primaria e riavvia DHCP sull'interfaccia primaria:

```C
nx_dhcp_create(&my_dhcp_client);
/* By default this enables primary interface for DHCP. */

nx_dhcp_interface_enable(&my_dhcp_client, 1); 
/* Secondary interface is enabled. */

nx_dhcp_interface_start(&my_dhcp_client, 1); 
/* DHCP is started on secondary interface. */

/* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); 
/* DHCP is started on primary interface. */

nx_dhcp_interface_release(&my_dhcp_client, 0); 

/* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); 
/* DHCP is restarted on primary interface. */
```

Per un elenco completo dei servizi specifici dell'interfaccia, vedere la **Descrizione dei servizi** nel capitolo tre.

## <a name="configuration-options"></a>Opzioni di configurazione

Le opzioni DHCP configurabili dall'utente in *nx_dhcp. h* consentono all'applicazione host di ottimizzare il client DHCP in base ai requisiti specifici. Di seguito è riportato un elenco di questi parametri:  
  
- **NX_DHCP_ENABLE_BOOTP** Definita, questa opzione Abilita il protocollo BOOTP anziché DHCP. Per impostazione predefinita, questa opzione è disabilitata.

- **NX_DHCP_CLIENT_RESTORE_STATE** Se definito, consente al client DHCP di salvare lo stato corrente della licenza client DHCP, incluso il tempo rimanente per il lease, e ripristinare lo stato tra i riavvii delle applicazioni client DHCP. Il valore predefinito è Disattivata.

- **NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL** Se impostato, il client DHCP non creerà il proprio pool di pacchetti. Per impostare il pool di pacchetti client DHCP, l'applicazione host deve utilizzare il servizio nx_dhcp_packet_pool_set. Il valore predefinito è Disattivata.

- **NX_DHCP_CLIENT_SEND_ARP_PROBE** Questa impostazione consente al client DHCP di inviare un probe ARP dopo l'assegnazione degli indirizzi IP per verificare che l'indirizzo DHCP assegnato non sia di proprietà di un altro host. Questa opzione è disabilitata per impostazione predefinita.

- **NX_DHCP_ARP_PROBE_WAIT** Definisce l'intervallo di tempo durante il quale il client DHCP attende una risposta dopo l'invio di un probe ARP. Il valore predefinito è un secondo (1 * NX_IP_PERIODIC_RATE)

- **NX_DHCP_ARP_PROBE_MIN** Definisce la variazione minima nell'intervallo tra l'invio di probe ARP. Per impostazione predefinita, il valore viene impostato su 1 secondo.

- **NX_DHCP_ARP_PROBE_MAX** Definisce la variazione massima nell'intervallo tra l'invio di probe ARP. Per impostazione predefinita, il valore viene impostato su 2 secondi.

- **NX_DHCP_ARP_PROBE_NUM** Definisce il numero di probe ARP inviati per determinare se l'indirizzo IP assegnato dal server DHCP è già in uso. Per impostazione predefinita, il valore viene impostato su 3 Probe.

- **NX_DHCP_RESTART_WAIT** Definisce il periodo di attesa del client DHCP per riavviare DHCP se l'indirizzo IP assegnato al client DHCP è già in uso. Per impostazione predefinita, il valore viene impostato su 10 secondi.

- **NX_DHCP_CLIENT_MAX_RECORDS** Specifica il numero massimo di record di interfaccia da salvare nell'istanza del client DHCP. Un record di interfaccia client DHCP è un record del client DHCP in esecuzione su un'interfaccia specifica. Il valore predefinito è impostato come numero di interfacce fisiche (NX_MAX_PHYSICAL_INTERFACES).

- **NX_DHCP_CLIENT_SEND_MAX_DHCP_MESSAGE_OPTION** Definito, consente al client DHCP di inviare l'opzione dimensioni massime messaggi DHCP. Questa opzione è disabilitata per impostazione predefinita.

- **NX_DHCP_CLIENT_ENABLE_HOST_NAME_CHECK** In questo modo, il client DHCP deve controllare il nome host di input nella chiamata nx_dhcp_create per la lunghezza o i caratteri non validi. Questa opzione è disabilitata per impostazione predefinita.

- **NX_DHCP_THREAD_PRIORITY** Priorità del thread DHCP. Per impostazione predefinita, questo valore specifica che il thread DHCP viene eseguito con priorità 3.

- **NX_DHCP_THREAD_STACK_SIZE** Dimensioni dello stack di thread DHCP. Per impostazione predefinita, le dimensioni sono pari a 2048 byte.

- **NX_DHCP_TIME_INTERVAL** Intervallo in secondi durante il quale viene eseguita la funzione di scadenza del timer del client DHCP. Questa funzione Aggiorna tutti i timeout nel processo DHCP, ad esempio se i messaggi devono essere ritrasmessi o lo stato del client DHCP è stato modificato. Per impostazione predefinita, questo valore è di 1 secondo.

- **NX_DHCP_OPTIONS_BUFFER_SIZE** Dimensioni del buffer delle opzioni DHCP. Per impostazione predefinita, questo valore è 312.

- **NX_DHCP_PACKET_PAYLOAD** Specifica la dimensione in byte del payload del pacchetto client DHCP. Il valore predefinito è NX_DHCP_MINIMUM_IP_DATAGRAM + dimensioni dell'intestazione fisica. Le dimensioni dell'intestazione fisica in una rete wireline sono in genere le dimensioni del frame Ethernet.

- **NX_DHCP_PACKET_POOL_SIZE** Specifica le dimensioni del pool di pacchetti client DHCP. Il valore predefinito è (5 * NX_DHCP_PACKET_PAYLOAD), che fornirà quattro pacchetti più spazio per l'overhead interno del pool di pacchetti.

- **NX_DHCP_MIN_RETRANS_TIMEOUT** Specifica l'opzione di attesa minima per la ricezione di una risposta del server DHCP al messaggio client prima della ritrasmissione del messaggio. Il valore predefinito è RFC 2131 consigliato 4 secondi.

- **NX_DHCP_MAX_RETRANS_TIMEOUT** Specifica l'opzione di attesa massima per la ricezione di una risposta del server DHCP al messaggio client prima della ritrasmissione del messaggio. Il valore predefinito è RFC 2131 consigliato 64 secondi.

- **NX_DHCP_MIN_RENEW_TIMEOUT** Specifica l'opzione di attesa minima per la ricezione di un messaggio server DHCP e l'invio di una richiesta di rinnovo dopo che il client DHCP è associato a un indirizzo IP. Il valore predefinito è 60 secondi. Tuttavia, il client DHCP utilizza il rinnovo e la riassociazione dei tempi di scadenza dal messaggio del server DHCP prima che venga impostato il timeout di rinnovo minimo.

- **NX_DHCP_TYPE_OF_SERVICE** Tipo di servizio necessario per le richieste UDP DHCP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.

- **NX_DHCP_FRAGMENT_OPTION** L'abilitazione del frammento per le richieste UDP DHCP. Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione UDP DHCP.

- **NX_DHCP_TIME_TO_LIVE** Specifica il numero di router che questo pacchetto può superare prima che venga eliminato. Il valore predefinito è impostato su 0x80.

- **NX_DHCP_QUEUE_DEPTH** Specifica il numero massimo di profondità della coda di ricezione. Il valore predefinito è impostato su 4.
