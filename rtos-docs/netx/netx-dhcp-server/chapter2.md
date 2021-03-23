---
title: Capitolo 2-installazione e uso del server DHCP NetX di Azure RTO
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente server DHCP NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 034a4d74c566fbfe94981a42b7e06e7f2ee79d25
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822694"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-dhcp-server"></a>Capitolo 2-installazione e uso del server DHCP NetX di Azure RTO

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente DHCP NetX di Azure RTO.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il server DHCP NetX di Azure RTO può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_dhcp_server. h**: file di intestazione per il server DHCP NETX
- **nx_dhcp_server. c**: file di origine c per il server DHCP NETX
- **nx_dhcp_server.pdf**: Descrizione PDF del server DHCP NETX
- **demo_netx_dhcp_server. c**: NETX server DHCP demo

## <a name="dhcp-installation"></a>Installazione DHCP

Per usare il server DHCP NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_dhcp_server. h* e *nx_dhpc_server. c* devono essere copiati in questa directory.

## <a name="using-netx-dhcp-server"></a>Uso del server DHCP NetX

L'uso del server DHCP NetX è facile. In pratica, il codice dell'applicazione deve includere *nx_dhcp_server. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX. Una volta incluso *nx_dhcp_server. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione DHCP specificate più avanti in questa guida. Nell'applicazione deve inoltre essere incluso *nx_dhcp_server. c* nel processo di compilazione. Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Per ulteriori informazioni sull'utilizzo del server DHCP NetX, vedere le sezioni seguenti [requisiti del dhcpserver NETX](#requirements-of-the-netx-dhcp-server) e [vincoli del server DHCP NETX](#constraints-of-the-netx-dhcp-server).

> [!NOTE]
> Poiché DHCP usa i servizi UDP NetX, è necessario abilitare UDP con la chiamata *nx_udp_enable* prima di usare DHCP.

## <a name="requirements-of-the-netx-dhcp-server"></a>Requisiti del server DHCP NetX

Il server DHCP NetX richiede una porta del socket UDP assegnata alla porta DHCP 67 ben nota. Per creare il server DHCP, l'applicazione deve creare un pool di pacchetti con payload di pacchetti di almeno 548 byte più le intestazioni IP, UDP e Ethernet (con un totale di 44 byte con allineamento a 4 byte).

Si presuppone che il server e il client utilizzino entrambe le impostazioni degli indirizzi hardware Ethernet:

- **Tipo di hardware**: 1
- **Lunghezza hardware**: 6
- **Hop**: 0

### <a name="multiple-client-sessions"></a>Più sessioni client

Il server DHCP di NetX è in grado di gestire più sessioni client mantenendo una tabella dei client DHCP attivi e lo stato del client, ad esempio gli Stati DHCP INIT, BOOT, SELECTing, REQUESTing, RINNOVAting e così via. Se il timeout della sessione scade prima di ricevere il messaggio client successivo, a meno che il client non sia associato a un lease IP, il server cancellerà i dati della sessione client e restituirà l'indirizzo IP assegnato nuovamente al pool disponibile. Se il server riceve più messaggi di individuazione dallo stesso client, il server reimposta il timeout della sessione e mantiene l'indirizzo IP riservato affinché il client accetti in un messaggio di richiesta successivo.

Il server DHCP NetX accetta anche la richiesta DHCP a stato singolo, ad esempio il client invia solo un messaggio di richiesta. Si presuppone che al client sia stato precedentemente assegnato un lease IP dal server DHCP.

### <a name="setting-interface-specific-network-parameters-server-responses"></a>Impostazione delle risposte del server dei parametri di rete specifici dell'interfaccia

L'applicazione può impostare i parametri del router, subnet mask e del server DNS per ogni interfaccia che gestisce le richieste dei client DHCP, usando il servizio *nx_dhcp_set_interface_network_parameters* . In caso contrario, questi parametri vengono impostati rispettivamente sul gateway IP sull'interfaccia principale del server, sulla subnet di rete DHCP e sull'indirizzo IP del server DHCP.

Il server DHCP include questi parametri nei dati delle opzioni dei messaggi DHCP inviati ai client DHCP.

### <a name="assigning-ip-addresses-to-the-client"></a>Assegnazione di indirizzi IP al client

Se il messaggio di individuazione del client non specifica un indirizzo IP richiesto, il server DHCP può utilizzarne uno dal proprio pool. Se il server non dispone di indirizzi IP disponibili, invierà al client un messaggio NACK.

Il server DHCP NetX concederà l'indirizzo IP richiesto nel messaggio di richiesta client purché l'indirizzo IP sia disponibile e si trovi nel database degli indirizzi IP del server. L'applicazione crea l'elenco di indirizzi IP disponibili per l'assegnazione ai client DHCP utilizzando il servizio *nx_dhcp_create_server_ip_address_list* . Se il server non dispone degli indirizzi IP richiesti oppure viene assegnato a un altro host, invierà al client un messaggio NACK.

Quando il server DHCP riceve una richiesta client, identifica il client in modo univoco utilizzando l'indirizzo MAC del client nel campo indirizzo MAC client del messaggio DHCP. Se il client modifica l'indirizzo MAC o viene spostato altrove su un'altra subnet, deve inviare un messaggio di rilascio al server per restituire l'indirizzo IP al pool disponibile e richiedere un nuovo indirizzo IP nello stato INIT.

Per informazioni dettagliate, vedere la figura 1,1 della sezione **sistema di esempio di piccole dimensioni** . Il numero di indirizzi IP salvati nell'istanza del server DHCP è limitato alle dimensioni della matrice di indirizzi del server nel blocco di controllo server DHCP e viene definito dall'opzione configurabile NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE.

### <a name="ip-address-lease-times"></a>Tempi di lease degli indirizzi IP

Il server DHCP accetterà anche il tempo di lease del client di richiesta se tale tempo di lease è inferiore al tempo di lease predefinito del server, definito nell'opzione configurabile NX_DHCP_DEFAULT_LEASE_TIME. I tempi di rinnovo e di riassociazione assegnati al client sono rispettivamente del 50% e del 85% del tempo di lease, a meno che il tempo di lease non sia infinito (0xFFFFFFFF), nel qual caso i tempi di rinnovo e di riassociazione vengono impostati anche su infinito.

### <a name="dhcp-server-timeouts"></a>Timeout server DHCP

Il server DHCP dispone di un timeout di sessione configurabile dall'utente, NX_DHCP_CLIENT_SESSION_TIMEOUT, per attendere il successivo messaggio del client DHCP, a meno che la sessione non venga completata. Il timeout viene reimpostato quando il server riceve il messaggio successivo dal client indipendentemente dal fatto che sia lo stesso messaggio inviato in precedenza.

### <a name="internal-error-handling"></a>Gestione interna degli errori

Il server DHCP riceve ed elabora i pacchetti client DHCP nella funzione *nx_dhcp_listen_for_messages* . Questa funzione interrompe l'elaborazione del pacchetto client DHCP corrente se il pacchetto non è valido o se il server DHCP rileva un errore interno. n *x_dhcp_listen_for_messages* restituisce uno stato di errore. Il thread del server DHCP cede il controllo brevemente all'utilità di pianificazione di ThreadX prima di chiamare questa funzione per ricevere il successivo messaggio del client DHCP. Nella versione corrente non è disponibile alcun supporto per la registrazione per lo stato di errore restituito da *nx_dhcp_listen_for_messages.*

### <a name="option-55-parameter-request-list"></a>Opzione 55: elenco di richieste di parametri

Il server DHCP di NetX deve essere configurato con un set di opzioni per caricare nell'elenco di opzioni di richiesta parametro (55) nell'offerta e i messaggi DHCPACK trasmessi al client. Queste opzioni includono i dati di configurazione di rete critici per la rete client e per impostazione predefinita è definito come indirizzo IP del router, subnet mask e server DNS. L'elenco di opzioni è un elenco delimitato da spazi e definito nell'NX_DHCP_DEFAULT_SERVER_OPTION_LIST configurabile dall'utente. Si noti che il numero di opzioni specificato in questo elenco deve essere uguale NX_DHCP_DEFAULT_OPTION_LIST_SIZE anche definito dall'utente.

## <a name="constraints-of-the-netx-dhcp-server"></a>Vincoli del server DHCP NetX

### <a name="dhcp-messages"></a>Messaggi DHCP

Il server DHCP NetX non verifica che un indirizzo IP sia stato assegnato altrove sulla rete prima di concedere l'indirizzo IP al client. Se sono presenti più server DHCP, è possibile che questo sia il caso. *In base allo standard RFC 2131, è responsabilità del cliente verificare che l'indirizzo IP sia univoco sulla propria rete,* ad esempio eseguendo il ping dell'indirizzo. In caso contrario, il server deve ricevere un messaggio di rifiuto con l'indirizzo IP per aggiornare il relativo database dal client.

Il server DHCP NetX non emette messaggi di FORCE_RENEW. È il client DHCP a rinnovare il lease di indirizzi IP. Tuttavia, il server DHCP monitora il tempo rimanente per tutti gli indirizzi IP assegnati nel database. Quando un lease di indirizzi IP scade, l'indirizzo IP viene restituito al pool di indirizzi IP disponibili. Quindi spetta al client rinnovare/riassociare attivamente il lease degli indirizzi IP.

I dati della sessione vengono cancellati non appena il client viene concesso ("associato") a un lease IP (o uno esistente viene rinnovato). Se un pacchetto client dimostra un falso o si verifica il timeout del client tra le risposte, i dati della sessione vengono cancellati.

### <a name="saving-data-between-reboots"></a>Salvataggio dei dati tra i riavvii

Il server DHCP NetX Salva i dati client inclusi i parametri di richiesta DHCP in una tabella di record client. Questa tabella non è archiviata nella memoria non volatile, pertanto se l'host del server DHCP deve riavviare tali informazioni non vengono salvate tra i riavvii.

Il server DHCP NetX Salva i dati di lease degli indirizzi IP in una tabella di indirizzi IP. Questa tabella non è archiviata nella memoria non volatile, pertanto se l'host del server DHCP deve riavviare tali informazioni non vengono salvate tra i riavvii.

### <a name="relay-agents"></a>Agenti di inoltro

Il server DHCP NetX è configurato con un indirizzo IP zero per il campo "agente di inoltro" perché non supporta le richieste DHCP di rete.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come è facile usare il server DHCP NetX è descritto nella figura 1,1 riportata di seguito. In questo esempio il file di inclusione DHCP *nx_dhcp_server. h* viene portato nella riga 5. Dimensioni dello stack di thread del server DHCP, dimensioni dello stack del thread IP e dimensioni dello stack del thread di test sono tutte definite nelle righe 7-13.

Per prima cosa, un'attività del thread di test facoltativa per l'arresto, il riavvio e la fine dell'eliminazione del server DHCP viene creata con la funzione "*test_thread_entry*" alla riga 57. Un blocco di controllo server DHCP "*dhcp_server*" viene definito come variabile globale alla riga 20. Si noti che il pool di pacchetti del server viene creato con i pacchetti con un payload almeno pari al messaggio DHCP standard (548 byte più i byte di intestazione IP e UDP). Dopo aver creato un'istanza IP per il server DHCP, l'applicazione crea il server DHCP alla riga 96. Successivamente, l'applicazione consente all'istanza IP del server di essere abilitata per UDP. Prima di avviare il server DHCP, l'elenco di indirizzi IP disponibili viene creato nella riga 137 usando il servizio *nx_dhcp_create_server_ip_address_list* . I parametri di configurazione di rete vengono impostati nella riga 138 seguente utilizzando il servizio *nx_dhcp_set_interface_network_parameters* , i servizi server DHCP diventano disponibili quando l'applicazione chiama il *nx_dhcp_server_start* alla riga 141. Nell'attività Test thread viene illustrato l'utilizzo dell'arresto e del riavvio del server DHCP.

```c
/* This is a small demo of NetX DHCP Server for the high-performance NetX TCP/IP stack. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nx_dhcp_server.h"

#define     DEMO_TEST_STACK_SIZE       2048
#define     DEMO_SERVER_STACK_SIZE     2048
#define     SERVER_IP_ADDRESS_LIST     "192.168.2.10 192.168.2.11 192.168.2.12"
#define     PACKET_PAYLOAD             1000
#define     PACKET_POOL_SIZE           (PACKET_PAYLOAD * 10)
#define     SERVER_IP_THREAD_STACK     2048

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD          test_thread;
NX_PACKET_POOL     server_pool;
NX_IP              server_ip;
NX_DHCP_SERVER     dhcp_server;

/* Define the counters used in the demo application... */

ULONG             state_changes;

/* Define thread prototypes. */

void     test_thread_entry(ULONG thread_input);
void     nx_etherDriver_mcf5485(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
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

    /* Create the test thread. */
    status = tx_thread_create(&test_thread, "test thread", test_thread_entry, 0,
                pointer, TEST_STACK_SIZE, 1, 1, TX_NO_TIME_SLICE, TX_DONT_START);

    if (status)
    {
        printf("Error with DHCP test thread create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create the DHCP Server packet pool. */
    status = nx_packet_pool_create(&server_pool, "NetX Main Packet Pool",
                                PACKET_PAYLOAD, pointer, PACKET_POOL_SIZE);
                                pointer = pointer + PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {
        printf("Error with DHCP server packet pool create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server IP instance. */
    status = nx_ip_create(&server_ip, "NetX DHCP Server IP", NX_DHCP_SERVER_IP_ADDRESS,
                        0xFFFFFF00UL, &server_pool, nx_etherDriver_mcf5485, pointer,
                        SERVER_IP_THREAD_STACK, 1);

    pointer = pointer + DEMO_IP_THREAD_STACK;

    /* Check for IP create errors. */
    if (status)
    {
        printf("Error with DHCP server IP task create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server instance. */
    status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                    DEMO_SERVER_STACK_SIZE,"DHCP Server", &server_pool);

    if (status)
    {
        printf("Error with DHCP server create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_SERVER_STACK_SIZE;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status = nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors. */
    if (status)
    {
        printf("Error with ARP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable UDP traffic. */
    status = nx_udp_enable(&server_ip);

    /* Check for UDP enable errors. */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable ICMP to enable the ping utility. */
    status = nx_icmp_enable(&server_ip);

    /* Check for errors. */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
    }

    status = nx_dhcp_create_server_ip_address_list(&dhcp_server, iface_index,
                START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);
    status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                                        NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                                        IP_ADDRESS(10,0,0,1));

    /* Start the DHCP Server. */
    status = nx_dhcp_server_start(&dhcp_server);

    tx_thread_resume(&test_thread);
}

/* Define the test thread. */
void     test_thread_entry(ULONG thread_input)
{

UINT     status;
UINT     keep_spinning;

    /* Just let the test thread be idle till we're ready to shut things down. */
    keep_spinning = 1;
    while(keep_spinning)
    {
        tx_thread_sleep(300);
    }

    printf("Stopping the server...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(500);

    printf("Starting the server...\n");
    status = nx_dhcp_server_start(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server start. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(600);

    printf("Stopping the server for good...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(200);

    printf("Deleting the server...\n");
    status = nx_dhcp_server_delete(&dhcp_server);
    if (status)
    {
        printf("Error with DHCP server delete. Status 0x%x\r\n", status);
        return;
    }
}
```

Figura 1,1 esempio di applicazione server DHCP NetX

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione del server DHCP NetX. L'elenco seguente descrive tutti i dettagli:  
  
- **NX_DISABLE_ERROR_CHECKING**: questa opzione rimuove il controllo degli errori DHCP di base. Viene in genere usato dopo il debug dell'applicazione.  
- **NX_DHCP_SERVER_THREAD_PRIORITY**: questa opzione specifica la priorità del thread del server DHCP. Per impostazione predefinita, questo valore specifica che il thread DHCP viene eseguito con priorità 2.
- **NX_DHCP_TYPE_OF_SERVICE**: questa opzione specifica il tipo di servizio necessario per le richieste UDP DHCP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.
- **NX_DHCP_FRAGMENT_OPTION**: abilitazione del frammento per le richieste UDP DHCP. Per impostazione predefinita, questo valore è impostato su NX_DONT_FRAGMENT per disabilitare la frammentazione UDP.
- **NX_DHCP_TIME_TO_LIVE**: specifica il numero di router che il pacchetto può superare prima che venga eliminato. Il valore predefinito è 0x80.
- **NX_DHCP_QUEUE_DEPTH** Specifica il numero di pacchetti che il socket del server DHCP mantiene prima di scaricare la coda. Il valore predefinito è 5.
- **NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: specifica il timeout nei cicli del timer in modo che il server DHCP NETX attenda l'allocazione di un pacchetto dal relativo pool di pacchetti. Il valore predefinito è impostato su NX_IP_PERIODIC_RATE.
- **NX_DHCP_SUBNET_MASK**: subnet mask il client DHCP deve essere configurato con. Il valore predefinito è impostato su 0xFFFFFF00.
- **NX_DHCP_FAST_PERIODIC_TIME_INTERVAL**: periodo di timeout nei cicli del timer per il timer rapido del server DHCP per il controllo del tempo di sessione rimanente e per la gestione delle sessioni scadute.
- **NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL**: periodo di timeout nei segni di graduazione del timer per il timer del server DHCP lento per verificare il tempo di lease degli indirizzi IP rimanente e gestire il lease scaduto.
- **NX_DHCP_CLIENT_SESSION_TIMEOUT**: periodo di timeout nei cicli del timer il server DHCP attenderà di ricevere il successivo messaggio del client DHCP.
- **NX_DHCP_DEFAULT_LEASE_TIME**: tempo di lease degli indirizzi IP in secondi assegnato al client DHCP e la base per calcolare il rinnovo e i tempi di riassociazione assegnati anche al client. Il valore predefinito è impostato su 0xFFFFFFFF (Infinity).
- **NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE**: dimensione della matrice di server DHCP per l'assegnazione di indirizzi IP disponibili per l'assegnazione al client. Il valore predefinito è 20.
- **NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: dimensione dell'array di server DHCP per la conservazione dei record client. Il valore predefinito è 50.
- **NX_DHCP_CLIENT_OPTIONS_MAX**: dimensione della matrice nell'istanza del client DHCP per contenere tutte le opzioni richieste nell'elenco di richieste di parametri nella sessione corrente. Il valore predefinito è 12.
- **NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: si tratta del buffer che contiene l'elenco predefinito di opzioni del server DHCP da fornire al client DHCP corrente nell'elenco di richieste di parametri. Il valore predefinito è "1 3 6".
- **NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE**: dimensione della matrice in cui è contenuto l'elenco predefinito di opzioni del server DHCP. Il valore predefinito è 3.
- **NX_DHCP_SERVER_HOSTNAME_MAX**: dimensione del buffer per contenere il nome host del server. Il valore predefinito è (32).
- **NX_DHCP_CLIENT_HOSTNAME_MAX**: dimensione del buffer per contenere il nome host del client nella sessione client del server DHCP corrente. Il valore predefinito è (32).
