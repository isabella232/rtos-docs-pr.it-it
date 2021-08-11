---
title: Capitolo 2 - Installazione e uso del Azure RTOS DHCP NetX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS server DHCP NetX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 04cbf4c9529538c3b5db6f8045a28bbcad5861c6ce846a898fa3ba1c7d97b19f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799575"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-dhcp-server"></a>Capitolo 2 - Installazione e uso del Azure RTOS DHCP NetX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS dhcp NetX.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS server DHCP NetX può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_dhcp_server.h:** file di intestazione per il server DHCP NetX
- **nx_dhcp_server.c**: file di origine C per il server DHCP NetX
- **nx_dhcp_server.pdf**: Descrizione PDF del server DHCP NetX
- **demo_netx_dhcp_server.c**: Dimostrazione del server DHCP NetX

## <a name="dhcp-installation"></a>Installazione DHCP

Per usare il server DHCP NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_dhcp_server.h* e *nx_dhpc_server.c* devono essere copiati in questa directory.

## <a name="using-netx-dhcp-server"></a>Uso del server DHCP NetX

L'uso del server DHCP NetX è semplice. In pratica, il codice dell'applicazione deve includere *nx_dhcp_server.h* dopo aver incluso *rispettivamente tx_api.h* e *nx_api.h*, per poter usare rispettivamente ThreadX e NetX. Dopo *nx_dhcp_server.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione DHCP specificate più avanti in questa guida. L'applicazione deve includere *anche nx_dhcp_server.c* nel processo di compilazione. Questo file deve essere compilato nello stesso modo degli altri file dell'applicazione e il relativo modulo oggetto deve essere collegato insieme ai file dell'applicazione. Per altre informazioni sull'uso del server DHCP NetX, vedere le sezioni seguenti Requisiti del server [DHCP NetX](#requirements-of-the-netx-dhcp-server) e [Vincoli del server DHCP NetX](#constraints-of-the-netx-dhcp-server).

> [!NOTE]
> Poiché DHCP utilizza i servizi UDP NetX,  è necessario nx_udp_enable UDP prima di usare DHCP.

## <a name="requirements-of-the-netx-dhcp-server"></a>Requisiti del server DHCP NetX

Il server DHCP NetX richiede una porta socket UDP assegnata alla porta DHCP nota 67. Per creare il server DHCP, l'applicazione deve creare un pool di pacchetti con payload del pacchetto di almeno 548 byte più intestazioni IP, UDP ed Ethernet (che hanno un totale di 44 byte con allineamento a 4 byte).

Si presuppone che server e client utilizzino entrambe le impostazioni degli indirizzi hardware Ethernet:

- **Tipo di hardware:** 1
- **Lunghezza hardware:** 6
- **Hop :** 0

### <a name="multiple-client-sessions"></a>Più sessioni client

Il server DHCP NetX può gestire più sessioni client mantenendo una tabella di client DHCP attivi e lo "stato" che il client si trova negli stati DHCP INIT, BOOT, SELECTING, REQUESTING, RENEWING e così via. Se il timeout della sessione scade prima di ricevere il messaggio client successivo, a meno che tale client non sia associato a un lease IP, il server cancella i dati della sessione client e restituisce l'indirizzo IP assegnato al pool disponibile. Se il server riceve più messaggi DISCOVER dallo stesso client, il server reimposta il timeout della sessione e mantiene l'indirizzo IP riservato al client per l'accettazione in un messaggio REQUEST successivo.

Il server DHCP NetX accetta anche la richiesta DHCP client a stato singolo, ad esempio il client invia solo un messaggio REQUEST. Si presuppone che al client sia stato precedentemente assegnato un lease IP dal server DHCP.

### <a name="setting-interface-specific-network-parameters-server-responses"></a>Impostazione delle risposte del server dei parametri di rete specifici dell'interfaccia

L'applicazione può impostare il router, subnet mask e i parametri del server DNS per ogni interfaccia che gestisce le richieste client DHCP, usando il *nx_dhcp_set_interface_network_parameters* servizio. In caso contrario, questi parametri vengono predefiniti per il gateway IP nell'interfaccia primaria del server, rispettivamente la subnet di rete DHCP e l'indirizzo IP del server DHCP.

Il server DHCP include questi parametri nei dati delle opzioni dei messaggi DHCP inviati ai client DHCP.

### <a name="assigning-ip-addresses-to-the-client"></a>Assegnazione di indirizzi IP al client

Se il messaggio DISCOVER client non specifica un indirizzo IP richiesto, il server DHCP può usarne uno dal proprio pool. Se il server non ha indirizzi IP disponibili, invierà al client un messaggio NACK.

Il server DHCP NetX concederà l'indirizzo IP richiesto nel messaggio RICHIESTA client, purché l'indirizzo IP sia disponibile e sia disponibile nel database degli indirizzi IP del server. L'applicazione crea l'elenco di indirizzi IP disponibili del server per l'assegnazione ai client DHCP usando il *nx_dhcp_create_server_ip_address_list* locale. Se il server non ha gli indirizzi IP richiesti o è assegnato a un altro host, invierà al client un messaggio NACK.

Quando il server DHCP riceve una richiesta client, identifica il client in modo univoco usando l'indirizzo MAC client nel campo Indirizzo MAC client nel messaggio DHCP. Se il client cambia l'indirizzo MAC o viene spostato altrove in un'altra subnet, deve inviare un messaggio RELEASE al server per restituire l'indirizzo IP al pool disponibile e richiedere un nuovo indirizzo IP nello stato INIT.

Per informazioni dettagliate, vedere la figura 1.1 della **sezione Small Example System.** Il numero di indirizzi IP salvati nell'istanza del server DHCP è limitato alle dimensioni della matrice di indirizzi del server nel blocco di controllo server DHCP e definito dall'opzione configurabile NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE.

### <a name="ip-address-lease-times"></a>Tempi di lease degli indirizzi IP

Il server DHCP accetterà anche la richiesta Del lease del client se il tempo di lease è inferiore al tempo di lease predefinito del server definito nell'opzione configurabile NX_DHCP_DEFAULT_LEASE_TIME. I tempi di rinnovo e riassociato assegnati al client sono rispettivamente il 50% e l'85% del tempo di lease, a meno che il tempo di lease non sia infinito (0xFFFFFFFF), nel qual caso anche i tempi di rinnovo e riassociato sono impostati su infinito.

### <a name="dhcp-server-timeouts"></a>Timeout del server DHCP

Il server DHCP ha un timeout di sessione configurabile dall'utente, NX_DHCP_CLIENT_SESSION_TIMEOUT attesa del successivo messaggio client DHCP, a meno che la sessione non venga completata. Il timeout viene reimpostato quando il server riceve il messaggio successivo dal client indipendentemente dal fatto che sia lo stesso messaggio inviato in precedenza.

### <a name="internal-error-handling"></a>Gestione degli errori interni

Il server DHCP riceve ed elabora i pacchetti client DHCP nella *nx_dhcp_listen_for_messages* funzione. Questa funzione interromperà l'elaborazione del pacchetto client DHCP corrente se il pacchetto non è valido o il server DHCP rileva un errore interno.n x_dhcp_listen_for_messages restituisce uno stato di errore. Il thread del server DHCP rinuncia brevemente al controllo dell'utilità di pianificazione ThreadX prima di chiamare questa funzione per ricevere il messaggio client DHCP successivo. Nella versione corrente non è disponibile alcun supporto di registrazione per i valori restituiti dallo stato di errore *nx_dhcp_listen_for_messages.*

### <a name="option-55-parameter-request-list"></a>Opzione 55: Elenco richieste parametri

Il server DHCP NetX deve essere configurato con un set di opzioni da caricare nell'elenco Parameter Request Option (55) nei messaggi OFFER e DHCPACK che trasmette al client. Queste opzioni devono includere i dati di configurazione critici di rete per la rete client e per impostazione predefinita è definito come indirizzo IP del router, subnet mask e server DNS. L'elenco di opzioni è un elenco delimitato da spazi e definito nell'elenco configurabile dall'NX_DHCP_DEFAULT_SERVER_OPTION_LIST. Si noti che il numero di opzioni specificato in questo elenco deve essere uguale NX_DHCP_DEFAULT_OPTION_LIST_SIZE definito dall'utente.

## <a name="constraints-of-the-netx-dhcp-server"></a>Vincoli del server DHCP NetX

### <a name="dhcp-messages"></a>Messaggi DHCP

Il server DHCP NetX non verifica che un indirizzo IP non sia stato assegnato altrove nella rete prima di concedere l'indirizzo IP al client. Se sono presenti più server DHCP, questo può essere vero. *In base a RFC 2131,* è responsabilità del client verificare che l'indirizzo IP sia univoco nella rete ,ad esempio eseguendo il ping dell'indirizzo. In caso contrario, il server deve ricevere un messaggio DECLINE con l'indirizzo IP per aggiornare il database dal client.

Il server DHCP NetX non emettere FORCE_RENEW messaggi. Il client DHCP deve rinnovare il lease dell'indirizzo IP. Tuttavia, il server DHCP monitora il tempo rimanente su tutti gli indirizzi IP assegnati nel relativo database. Quando un lease di indirizzi IP scade, tale indirizzo IP viene restituito al pool di indirizzi IP disponibili. Di conseguenza, il client deve rinnovare/riassociare attivamente il lease dell'indirizzo IP.

I dati della sessione vengono cancellati non appena il client viene concesso ("associato") a un lease IP (o ne viene rinnovato uno esistente). Se un pacchetto client risulta falso o il timeout del client tra le risposte, i dati della sessione vengono cancellati.

### <a name="saving-data-between-reboots"></a>Salvataggio dei dati tra un riavvio e l'altro

Il server DHCP NetX salva i dati client, inclusi i parametri della richiesta DHCP, in una tabella di record client. Questa tabella non viene archiviata in memoria non volatile, quindi se l'host del server DHCP deve riavviare le informazioni non vengono salvate tra un riavvio e l'altro.

Il server DHCP NetX salva i dati di lease degli indirizzi IP in una tabella di indirizzi IP. Questa tabella non viene archiviata in memoria non volatile, quindi se l'host del server DHCP deve riavviare le informazioni non vengono salvate tra un riavvio e l'altro.

### <a name="relay-agents"></a>Agenti di inoltro

Il server DHCP NetX è configurato con un indirizzo IP zero per il campo "Agente di inoltro" perché non supporta le richieste DHCP fuori rete.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di quanto sia semplice usare il server DHCP NetX è descritto nella figura 1.1 riportata di seguito. In questo esempio il file di inclusione DHCP *nx_dhcp_server.h* viene portato alla riga 5. Le dimensioni dello stack dei thread del server DHCP, le dimensioni dello stack dei thread IP e le dimensioni dello stack dei thread di test sono tutte definite nelle righe da 7 a 13.

In primo luogo, viene creata un'attività del thread di test facoltativa per l'arresto, il riavvio e infine l'eliminazione del server DHCP con la funzione "*test_thread_entry*" alla riga 57. Un blocco di controllo server DHCP "*dhcp_server*" è definito come variabile globale alla riga 20. Si noti che il pool di pacchetti del server viene creato con pacchetti con un payload di almeno la dimensione del messaggio DHCP standard (548 byte più i byte di intestazione IP e UDP). Dopo aver creato correttamente un'istanza IP per il server DHCP, l'applicazione crea il server DHCP nella riga 96. Successivamente, l'applicazione consente all'istanza IP del server di essere abilitata per UDP. Prima di avviare il server DHCP, l'elenco di indirizzi IP disponibili viene creato nella riga 137 usando il *nx_dhcp_create_server_ip_address_list* servizio. I parametri di configurazione di rete vengono impostati nella riga 138 seguente usando il *servizio nx_dhcp_set_interface_network_parameters,* i servizi server DHCP diventano disponibili quando l'applicazione chiama il *nx_dhcp_server_start* alla riga 141. L'attività del thread di test illustra l'uso dell'arresto e del riavvio del server DHCP.

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

Figura 1.1 Esempio di applicazione server DHCP NetX

## <a name="configuration-options"></a>Opzioni di configurazione

Esistono diverse opzioni di configurazione per la creazione del server DHCP NetX. L'elenco seguente descrive ognuno in dettaglio:  
  
- **NX_DISABLE_ERROR_CHECKING:** questa opzione rimuove il controllo degli errori DHCP di base. Viene in genere usato dopo il debug dell'applicazione.  
- **NX_DHCP_SERVER_THREAD_PRIORITY:** questa opzione specifica la priorità del thread del server DHCP. Per impostazione predefinita, questo valore specifica che il thread DHCP viene eseguito con priorità 2.
- **NX_DHCP_TYPE_OF_SERVICE:** questa opzione specifica il tipo di servizio necessario per le richieste UDP DHCP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio di pacchetti IP.
- **NX_DHCP_FRAGMENT_OPTION**: frammento abilitato per le richieste UDP DHCP. Per impostazione predefinita, questo valore è impostato su NX_DONT_FRAGMENT per disabilitare la frammentazione UDP.
- **NX_DHCP_TIME_TO_LIVE**: specifica il numero di router che il pacchetto può superare prima di essere eliminato. Il valore predefinito è 0x80.
- **NX_DHCP_QUEUE_DEPTH** Specifica il numero di pacchetti che il socket del server DHCP mantiene prima di scaricare la coda. Il valore predefinito è 5.
- **NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: specifica il timeout in tick del timer per il server DHCP NetX in attesa dell'allocazione di un pacchetto dal relativo pool di pacchetti. Il valore predefinito è impostato su NX_IP_PERIODIC_RATE.
- **NX_DHCP_SUBNET_MASK:** questa è la subnet mask con cui deve essere configurato il client DHCP. Il valore predefinito è impostato su 0xFFFFFF00.
- **NX_DHCP_FAST_PERIODIC_TIME_INTERVAL:** periodo di timeout in tick del timer per il timer rapido del server DHCP per controllare il tempo rimanente della sessione e gestire le sessioni che si sono verificate.
- **NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL:** periodo di timeout in tick timer per il timer lento del server DHCP per controllare il tempo di lease dell'indirizzo IP rimanente e gestire il lease che si è verificato.
- **NX_DHCP_CLIENT_SESSION_TIMEOUT**: periodo di timeout in tick timer che il server DHCP attenderà per ricevere il successivo messaggio client DHCP.
- **NX_DHCP_DEFAULT_LEASE_TIME:** tempo di lease dell'indirizzo IP in secondi assegnato al client DHCP e la base per il calcolo dei tempi di rinnovo e riassociato viene assegnata anche al client. Il valore predefinito è impostato su 0xFFFFFFFF (infinito).
- **NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE:** dimensioni dell'array del server DHCP per contenere gli indirizzi IP disponibili per l'assegnazione al client. Il valore predefinito è 20.
- **NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: dimensioni dell'array server DHCP per contenere i record client. Il valore predefinito è 50.
- **NX_DHCP_CLIENT_OPTIONS_MAX**: dimensione della matrice nell'istanza del client DHCP per contenere tutte le opzioni richieste nell'elenco di richieste di parametri nella sessione corrente. Il valore predefinito è 12.
- **NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: buffer che contiene l'elenco predefinito di opzioni del server DHCP da fornire al client DHCP corrente nell'elenco di richieste di parametri. Il valore predefinito è "1 3 6".
- **NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE:** dimensioni della matrice che contiene l'elenco predefinito di opzioni del server DHCP. Il valore predefinito è 3.
- **NX_DHCP_SERVER_HOSTNAME_MAX:** dimensioni del buffer per contenere il nome host del server. Il valore predefinito è (32).
- **NX_DHCP_CLIENT_HOSTNAME_MAX:** dimensioni del buffer per il nome host del client nella sessione client del server DHCP corrente. Il valore predefinito è (32).
