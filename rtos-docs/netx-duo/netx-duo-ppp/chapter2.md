---
title: Capitolo 2-installazione e uso di Azure RTO NetX Duo Point-to-Point Protocol (PPP)
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente RTO NetX Duo Point-to-Point Protocol (PPP) di Azure.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2270a2668884dbecc8368d4ee130e419afa92491
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821731"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-point-to-point-protocol-ppp"></a>Capitolo 2-installazione e uso di Azure RTO NetX Duo Point-to-Point Protocol (PPP)

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente RTO NetX Duo Point-to-Point Protocol (PPP) di Azure.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il pacchetto Azure RTO NetX Duo Point-to-Point Protocol (PPP) è disponibile all'indirizzo <https://github.com/azure-rtos/netxduo> . Il pacchetto include i file seguenti:

- **nx_ppp. h**: file di intestazione per PPP per NETX
- **nx_ppp. c**: file di origine c per PPP per NETX
- **nx_ppp.pdf**: Descrizione PDF di PPP per NETX
- dimostrazione di **demo_netx_ppp. c**: NETX PPP

## <a name="ppp-installation"></a>Installazione di PPP

Per poter usare PPP per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_ppp. h* e *nx_ppp. c* devono essere copiati in questa directory.

## <a name="using-ppp"></a>Uso di PPP

L'uso di PPP per NetX è facile. In pratica, il codice dell'applicazione deve includere *nx_ppp. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX. Una volta incluso *nx_ppp. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione PPP specificate più avanti in questa guida. Nell'applicazione deve inoltre essere incluso *nx_ppp. c* nel processo di compilazione. Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX PPP.

## <a name="using-modems"></a>Uso di modem

Se è necessario un modem per la connessione a Internet, è necessario tenere presenti alcune considerazioni speciali per poter usare il prodotto NetX PPP. In pratica, l'utilizzo di un modem introduce logica di inizializzazione e logica aggiuntive per la perdita di comunicazione. Inoltre, la maggior parte della logica aggiuntiva del modem viene eseguita al di fuori del contesto di NetX PPP. Il flusso di base dell'uso di NetX PPP con un modem è simile al seguente:

1. Inizializza modem

1. Comporre il provider di servizi Internet (ISP)

1. Attendi connessione

1. Attendi richiesta UserID

1. Avviare NetX PPP [PPP in Operation]

1. Perdita di comunicazione

1. Arrestare NetX PPP (o riavviare tramite nx_ppp_restart)

### <a name="initialize-modem"></a>Inizializza modem

Utilizzando la routine di output seriale di basso livello dell'applicazione, il modem viene inizializzato tramite una serie di comandi per caratteri ASCII. per ulteriori informazioni, vedere la documentazione del modem.

### <a name="dial-internet-service-provider"></a>Connessione al provider di servizi Internet

Utilizzando la routine di output seriale di basso livello dell'applicazione, al modem viene richiesto di comporre il provider di servizi Internet. Il codice seguente, ad esempio, è tipico di una stringa ASCII utilizzata per comporre un ISP al numero 123-4567:

"ATDT123456\r"

### <a name="wait-for-connection"></a>Attendi connessione

A questo punto, l'applicazione attende di ricevere indicazioni dal modem che è stata stabilita una connessione. Questa operazione viene eseguita cercando i caratteri della routine di input seriale di basso livello dell'applicazione. In genere, i modem restituiscono una stringa ASCII "CONNECT" quando è stata stabilita una connessione.

### <a name="wait-for-user-id-prompt"></a>Attendi richiesta ID utente

Una volta stabilita la connessione, l'applicazione deve ora attendere una richiesta di accesso iniziale da parte del provider di servizi Internet. Che in genere assume la forma di una stringa ASCII come "login?"

### <a name="start-netx-ppp"></a>Avviare NetX PPP

A questo punto, è possibile avviare NetX PPP. Questa operazione viene eseguita chiamando il servizio *nx_ppp_create* seguito dal servizio *nx_ip_create* . Potrebbero essere richiesti anche servizi aggiuntivi per abilitare PAP e configurare gli indirizzi IP PPP. Per ulteriori informazioni, consultare le sezioni seguenti di questa guida.

### <a name="loss-of-communication"></a>Perdita di comunicazione

Dopo l'avvio di PPP, le informazioni non PPP vengono passate alla routine "Gestione pacchetti non valida" specificata dall'applicazione al servizio *nx_ppp_create* . In genere, i modem inviano una stringa ASCII, ad esempio "nessun vettore", in caso di perdita della comunicazione con il provider di servizi Internet. Quando l'applicazione riceve un pacchetto non PPP con tali informazioni, è consigliabile arrestare l'istanza di NetX PPP o riavviare la macchina a stati PPP tramite l'API *nx_ppp_restart* .

### <a name="stop-netx-ppp"></a>Arrestare NetX PPP

L'arresto di NetX PPP è piuttosto semplice. In pratica, tutti i socket creati devono essere non associati ed eliminati. Eliminare quindi l'istanza IP tramite il servizio *nx_ip_delete* . Una volta eliminata l'istanza IP, è necessario chiamare il servizio *nx_ppp_delete* per completare il processo di arresto di PPP. A questo punto, l'applicazione è ora in grado di tentare di ristabilire la comunicazione con il provider di servizi Internet.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio che illustra la semplicità di utilizzo di NetX PPP è descritto nella figura 1,1 riportata di seguito. In questo esempio il file di inclusione PPP *nx_ppp. h* viene introdotto nella riga 3. Successivamente, il PPP viene creato in *"tx_application_define*" alla riga 56. Il blocco di controllo PPP "*my_ppp*" è stato definito come variabile globale alla riga 9 precedente. 

>[!NOTE]
>Prima di creare l'istanza IP, è necessario creare il PPP. Al termine della creazione di PPP e IP, il thread "*my_thread*" attende che il collegamento PPP venga attivo alla riga 98. Alla riga 104, PPP e NetX sono completamente operativi.

Il primo elemento non illustrato in questo esempio è l'ISR di ricezione di byte seriale dell'applicazione. Sarà necessario chiamare *nx_ppp_byte_receive* con "*my_ppp*" e il byte ricevuto come parametri di input.

```c
0001 #include   "tx_api.h"
0002 #include   "nx_api.h"
0003 #include   "nx_ppp.h"
0004
#define     DEMO_STACK_SIZE         4096
TX_THREAD               my_thread;
NX_PACKET_POOL          my_pool;
NX_IP                   my_ip;
NX_PPP                  my_ppp;

/* Define function prototypes. */

void    my_thread_entry(ULONG thread_input);
void    my_serial_driver_byte_output(UCHAR byte);
void    my_invalid_packet_handler(NX_PACKET *packet_ptr);
 
/* Define main entry point. */
intmain()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
 }


/* Define what the initial system looks like. */

void    tx_application_define(void *first_unused_memory)
{

CHAR    *pointer;
UINT    status;

/* Setup the working pointer. */
pointer =  (CHAR *) first_unused_memory;

/* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0,  
                  pointer, DEMO_STACK_SIZE, 
                  2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status =  nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                                    1024, pointer, 64000);
    pointer = pointer + 64000;

    /* Check for pool creation error. */
    if (status)
        error_counter++;

    /* Create a PPP instance. */
    status = nx_ppp_create(&my_ppp, “My PPP”, &my_ip, pointer, 1024, 2, 
                           &my_pool, my_invalid_packet_handler, my_serial_driver_byte_output);
    pointer =  pointer + 1024;
    /* Check for PPP creation pool. */
    if (status)
        error_counter++;

    /* Create an IP instance with the PPP driver. */
    status = nx_ip_create(&my_ip,"My NetX IP Instance", 
                           IP_ADDRESS(216,2,3,1), 0xFFFFFF00, &my_pool, 
                           nx_ppp_driver, pointer, DEMO_STACK_SIZE, 1);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for IP create errors. */
    if (status)
        error_counter++;

    /* Enable ICMP for my IP Instance. */
    status =  nx_icmp_enable(&my_ip);

    /* Check for ICMP enable errors. */
    if (status)
        error_counter++;

    /* Enable UDP. */
    status =  nx_udp_enable(&my_ip);
    if (status)
        error_counter++;
}

/* Define my thread. */
void    my_thread_entry(ULONG thread_input)
{

UINT        status;
ULONG       ip_status;
NX_PACKET   *my_packet;

/* Wait for the PPP link in my_ip to become enabled. */
    status =  nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,&ip_status,3000);

    /* Check for IP status error. */
    if (status) 
        return;

    /* Link is fully up and operational. All NetX activities 
    are now available. */

}
```
## <a name="configuration-options"></a>Opzioni di configurazione

Per la compilazione di PPP per NetX sono disponibili diverse opzioni di configurazione. L'elenco seguente descrive tutti i dettagli:

- **NX_DISABLE_ERROR_CHECKING**: definito, questa opzione rimuove il controllo degli errori PPP di base. Viene in genere usato dopo il debug dell'applicazione.
- **NX_PPP_PPPOE_ENABLE**: se definito, PPP è in grado di trasmettere pacchetti tramite Ethernet
- **NX_PPP_BASE_TIMEOUT**: definisce la frequenza del periodo (nei cicli del timer) in cui l'attività del thread PPP viene riattivata per verificare la presenza di eventi PPP. Il valore predefinito è 1 * NX_IP_PERIODIC_RATE (100 cicli).
- **NX_PPP_DISABLE_INFO**: se definito, la raccolta di informazioni PPP interna è disabilitata.
- **NX_PPP_DEBUG_LOG_ENABLE**: se definito, il log di debug PPP interno è abilitato.
- **NX_PPP_DEBUG_LOG_PRINT_ENABLE**: se definito, viene abilitato il log di debug di PPP interno *printf* a *stdio* . Questa operazione è valida solo se è abilitato anche il log di debug.
- **NX_PPP_DEBUG_LOG_SIZE**: dimensioni del log di debug (numero di voci nel log di debug). Al raggiungimento dell'ultima voce, l'acquisizione di debug esegue il wrapping sulla prima voce e sovrascrive tutti i dati acquisiti in precedenza. Il valore predefinito è 50.
- **NX_PPP_DEBUG_FRAME_SIZE**: quantità massima di dati acquisiti da un payload del pacchetto ricevuto e salvati nell'output di debug. Il valore predefinito è 50.
- **NX_PPP_DISABLE_CHAP**: se definito, viene rimossa la logica CHAP interna di PPP, inclusa la logica digest MD5.
- **NX_PPP_DISABLE_PAP**: se definito, viene rimossa la logica PAP per PPP interna.
- **NX_PPP_DNS_OPTION_DISABLE**: se definito, l'opzione del server DNS primario è disabilitata nella risposta protocollo IPCP. Per impostazione predefinita, questa opzione non è definita.
- **NX_PPP_DNS_ADDRESS_MAX_RETRIES**: specifica il numero di volte in cui l'host PPP richiederà un indirizzo del server DNS dal peer nello stato protocollo IPCP. Questa operazione non ha alcun effetto se viene definito NX_PPP_DNS_OPTION_DISABLE. Il valore predefinito è 2.
- **NX_PPP_HASHED_VALUE_SIZE**: specifica le dimensioni delle stringhe "valore hash" usate nell'autenticazione CHAP. Il valore predefinito è impostato su 16 byte, ma può essere ridefinito prima dell'inclusione di *nx_ppp. h.*
- **NX_PPP_MAX_LCP_PROTOCOL_RETRIES**: definisce il numero massimo di tentativi se il PPP scade prima di inviare un altro messaggio di richiesta di configurazione LCP. Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento è inattivo. Il valore predefinito è 20.
- **NX_PPP_MAX_PAP_PROTOCOL_RETRIES**: definisce il numero massimo di tentativi se il PPP scade prima di inviare un altro messaggio di richiesta di autenticazione PAP. Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento è inattivo. Il valore predefinito è 20.
- **NX_PPP_MAX_CHAP_PROTOCOL_RETRIES**: definisce il numero massimo di tentativi se il PPP scade prima di inviare un altro messaggio di verifica CHAP. Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento è inattivo. Il valore predefinito è 20.
- **NX_PPP_MAX_IPCP_PROTOCOL_RETRIES**: definisce il numero massimo di tentativi se il PPP scade prima di inviare un altro messaggio di richiesta di configurazione protocollo IPCP. Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento è inattivo. Il valore predefinito è 20.
- **NX_PPP_MRU**: specifica l'unità di ricezione massima (MRU) per PPP. Per impostazione predefinita, questo valore è 1.500 byte (valore minimo). Questa definizione può essere impostata dall'applicazione prima di includere *nx_ppp. h*.
- **NX_PPP_MINIMUM_MRU**: specifica la quantità minima di MRU ricevuta in un messaggio di richiesta di configurazione LCP. Per impostazione predefinita, questo valore è 1.500 byte (valore minimo). Questa definizione può essere impostata dall'applicazione prima di includere *nx_ppp. h*.
- **NX_PPP_NAME_SIZE**: specifica le dimensioni delle stringhe "Name" usate per l'autenticazione. Il valore predefinito è impostato su 32bytes, ma può essere ridefinito prima dell'inclusione di * nx_ppp. h.
- **NX_PPP_PASSWORD_SIZE**: specifica le dimensioni delle stringhe "password" usate per l'autenticazione. Il valore predefinito è impostato su 32bytes, ma può essere ridefinito prima dell'inclusione di *nx_ppp. h.*
- **NX_PPP_PROTOCOL_TIMEOUT**: definisce l'opzione Wait (in secondi) per l'attività PPP per la ricezione di una risposta a un messaggio di richiesta di protocollo PPP. Il valore predefinito è 4 secondi.
- **NX_PPP_RECEIVE_TIMEOUTS**: definisce il numero di volte in cui l'attività del thread PPP scade in attesa di ricevere il carattere successivo in un flusso di messaggi PPP. Successivamente, PPP rilascia il pacchetto e inizia ad attendere la ricezione del messaggio PPP successivo. Il valore predefinito è 4.
- **NX_PPP_SERIAL_BUFFER_SIZE**: specifica le dimensioni del buffer seriale dei caratteri di ricezione. Per impostazione predefinita, questo valore è pari a 3.000 byte. Questa definizione può essere impostata dall'applicazione prima di includere *nx_ppp. h*.
- **NX_PPP_TIMEOUT**: definisce l'opzione Wait (nei cicli del timer) per l'allocazione dei pacchetti per la trasmissione di dati e per il buffer dei dati seriali PPP in pacchetti da inviare al livello IP. Il valore predefinito è 4 * NX_IP_PERIODIC_RATE (400 cicli).
- **NX_PPP_THREAD_TIME_SLICE**: opzione di sezionamento del tempo per i thread PPP. Per impostazione predefinita, questo valore è TX_NO_TIME_SLICE. Questa definizione può essere impostata dall'applicazione prima di includere *nx_ppp. h*.
- **NX_PPP_VALUE_SIZE**: specifica le dimensioni delle stringhe "value" usate nell'autenticazione CHAP. Il valore predefinito è impostato su 32bytes, ma può essere ridefinito prima dell'inclusione di nx_ppp. h.