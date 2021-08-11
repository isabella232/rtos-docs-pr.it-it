---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX Duo Point-to-Point Protocol (PPP)
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente Azure RTOS NetX Duo Point-to-Point Protocol (PPP).
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 141197daa87b40ebe2ea34ff096a0b01b260e9296a33e3b678f11400d5d46ab6
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797161"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-point-to-point-protocol-ppp"></a>Capitolo 2 - Installazione e uso di Azure RTOS NetX Duo Point-to-Point Protocol (PPP)

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente Azure RTOS NetX Duo Point-to-Point Protocol (PPP).

## <a name="product-distribution"></a>Distribuzione del prodotto

Il Azure RTOS NetX Duo Point-to-Point Protocol (PPP) è disponibile all'indirizzo <https://github.com/azure-rtos/netxduo> . Il pacchetto include i file seguenti:

- **nx_ppp.h:** file di intestazione per PPP per NetX
- **nx_ppp.c**: file di origine C per PPP per NetX
- **nx_ppp.pdf**: Descrizione PDF di PPP per NetX
- **demo_netx_ppp.c**: Dimostrazione di NetX PPP

## <a name="ppp-installation"></a>Installazione PPP

Per usare PPP per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_ppp.h* e *nx_ppp.c* devono essere copiati in questa directory.

## <a name="using-ppp"></a>Uso di PPP

L'uso di PPP per NetX è semplice. In pratica, il codice dell'applicazione deve includere *nx_ppp.h* dopo aver incluso *tx_api.h* e *nx_api.h*, per poter usare rispettivamente ThreadX e NetX. Dopo *nx_ppp.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione PPP specificate più avanti in questa guida. L'applicazione deve anche *includere nx_ppp.c* nel processo di compilazione. Questo file deve essere compilato nello stesso modo degli altri file dell'applicazione e il relativo modulo oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX PPP.

## <a name="using-modems"></a>Uso di modem

Se è necessario un modem per la connessione a Internet, per usare il prodotto NetX PPP sono necessarie alcune considerazioni speciali. In pratica, l'uso di un modem introduce logica di inizializzazione aggiuntiva e logica per la perdita di comunicazione. Inoltre, la maggior parte della logica del modem aggiuntiva viene eseguita al di fuori del contesto di NetX PPP. Il flusso di base dell'uso di NetX PPP con un modem è simile al seguente:

1. Inizializzare il modem

1. Dial Internet Service Provider (ISP)

1. Attendere la connessione

1. Attendere la richiesta dell'ID utente

1. Avviare NetX PPP [PPP in esecuzione]

1. Perdita di comunicazione

1. Arrestare NetX PPP (o riavviare tramite nx_ppp_restart)

### <a name="initialize-modem"></a>Inizializzare il modem

Usando la routine di output seriale di basso livello dell'applicazione, il modem viene inizializzato tramite una serie di comandi di caratteri ASCII (per altri dettagli, vedere la documentazione del modem).

### <a name="dial-internet-service-provider"></a>Comporre un provider di servizi Internet

Usando la routine di output seriale di basso livello dell'applicazione, al modem viene richiesto di chiamare l'ISP. Ad esempio, il codice seguente è tipico di una stringa ASCII usata per comporre un ISP al numero 123-4567:

"ATDT123456\r"

### <a name="wait-for-connection"></a>Attendere la connessione

A questo punto, l'applicazione attende di ricevere dal modem l'indicazione che è stata stabilita una connessione. Questa operazione viene eseguita cercando i caratteri della routine di input seriale di basso livello dell'applicazione. In genere, i modem restituiscono una stringa ASCII "CONNECT" quando è stata stabilita una connessione.

### <a name="wait-for-user-id-prompt"></a>Attendere la richiesta dell'ID utente

Dopo aver stabilito la connessione, l'applicazione deve ora attendere una richiesta di accesso iniziale dall'ISP. Questo in genere assume la forma di una stringa ASCII come "Login?"

### <a name="start-netx-ppp"></a>Avviare NetX PPP

A questo punto, è possibile iniziare netx PPP. Questa operazione viene eseguita chiamando il servizio *nx_ppp_create* seguito dal *nx_ip_create* servizio. Potrebbero essere necessari anche servizi aggiuntivi per abilitare PAP e configurare gli indirizzi IP PPP. Per altre informazioni, vedere le sezioni seguenti di questa guida.

### <a name="loss-of-communication"></a>Perdita di comunicazione

Dopo l'avvio di PPP, tutte le informazioni non PPP vengono passate alla routine "Gestione pacchetti non validi" specificata dall'applicazione nx_ppp_create *servizio.* In genere, i modem inviano una stringa ASCII, ad esempio "NO CARRIER" quando la comunicazione viene persa con l'ISP. Quando l'applicazione riceve un pacchetto non PPP con tali informazioni, deve procedere all'arresto dell'istanza PPP di NetX o al riavvio della macchina a stati PPP tramite l'API *nx_ppp_restart.*

### <a name="stop-netx-ppp"></a>Arrestare NetX PPP

L'arresto di NetX PPP è piuttosto semplice. In pratica, tutti i socket creati devono essere non associati ed eliminati. Eliminare quindi l'istanza IP tramite il *nx_ip_delete* servizio. Dopo l'eliminazione dell'istanza IP, *è necessario chiamare nx_ppp_delete* servizio per completare il processo di arresto di PPP. A questo punto, l'applicazione è ora in grado di tentare di ristabilire la comunicazione con l'ISP.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio che illustra quanto sia semplice usare NetX PPP è descritto nella figura 1.1 riportata di seguito. In questo esempio il file di inclusione PPP *nx_ppp.h* viene portato alla riga 3. PPP viene quindi creato in *"tx_application_define"* alla riga 56. Il blocco di controllo PPP "*my_ppp*" è stato definito come variabile globale alla riga 9 in precedenza. 

>[!NOTE]
>PPP deve essere creato prima di creare l'istanza IP. Dopo la creazione di PPP e IP, il thread "*my_thread*" attende che il collegamento PPP venga attivo alla riga 98. Alla riga 104, sia PPP che NetX sono completamente operativi.

L'unico elemento non illustrato in questo esempio è l'ISR di ricezione di byte seriali dell'applicazione. Sarà necessario chiamare nx_ppp_byte_receive *con* "*my_ppp*" e il byte ricevuto come parametri di input.

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

Esistono diverse opzioni di configurazione per la compilazione di PPP per NetX. L'elenco seguente descrive ognuno in dettaglio:

- **NX_DISABLE_ERROR_CHECKING**: definita, questa opzione rimuove il controllo degli errori PPP di base. Viene in genere usato dopo il debug dell'applicazione.
- **NX_PPP_PPPOE_ENABLE:** se definito, PPP può trasmettere il pacchetto tramite Ethernet
- **NX_PPP_BASE_TIMEOUT**: definisce la frequenza del periodo (in tick timer) in cui l'attività del thread PPP viene ri svegliata per verificare la presenza di eventi PPP. Il valore predefinito è 1*NX_IP_PERIODIC_RATE (100 tick).
- **NX_PPP_DISABLE_INFO:** se definita, la raccolta di informazioni PPP interne è disabilitata.
- **NX_PPP_DEBUG_LOG_ENABLE:** se definito, il log di debug PPP interno è abilitato.
- **NX_PPP_DEBUG_LOG_PRINT_ENABLE:Se** definito, il log di debug PPP interno *printf* in *stdio* è abilitato. Questa operazione è valida solo se è abilitato anche il log di debug.
- **NX_PPP_DEBUG_LOG_SIZE**: dimensioni del log di debug (numero di voci nel log di debug). Al raggiungimento dell'ultima voce, l'acquisizione di debug esegue il wrapping della prima voce e sovrascrive tutti i dati acquisiti in precedenza. Il valore predefinito è 50.
- **NX_PPP_DEBUG_FRAME_SIZE:** quantità massima di dati acquisiti da un payload del pacchetto ricevuto e salvati nell'output di debug. Il valore predefinito è 50.
- **NX_PPP_DISABLE_CHAP:** se definita, viene rimossa la logica CHAP PPP interna, inclusa la logica digest MD5.
- **NX_PPP_DISABLE_PAP:** se definita, viene rimossa la logica PAP PPP interna.
- **NX_PPP_DNS_OPTION_DISABLE:** se definita, l'opzione server DNS primario è disabilitata nella risposta IPCP. Per impostazione predefinita, questa opzione non è definita.
- **NX_PPP_DNS_ADDRESS_MAX_RETRIES**: specifica quante volte l'host PPP richiederà un indirizzo del server DNS dal peer nello stato IPCP. Questa operazione non ha alcun effetto NX_PPP_DNS_OPTION_DISABLE definito. Il valore predefinito è 2.
- **NX_PPP_HASHED_VALUE_SIZE**: specifica le dimensioni delle stringhe di "valore hash" usate nell'autenticazione CHAP. Il valore predefinito è impostato su 16 byte, ma può essere ridefinito prima dell'inclusione *di nx_ppp.h.*
- **NX_PPP_MAX_LCP_PROTOCOL_RETRIES:** definisce il numero massimo di tentativi se si verifica il timeout del PPP prima di inviare un altro messaggio di richiesta di configurazione LCP. Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento non è disponibile. Il valore predefinito è 20.
- **NX_PPP_MAX_PAP_PROTOCOL_RETRIES:** definisce il numero massimo di tentativi se si verifica il timeout del PPP prima di inviare un altro messaggio di richiesta di autenticazione PAP. Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento non è disponibile. Il valore predefinito è 20.
- **NX_PPP_MAX_CHAP_PROTOCOL_RETRIES:** definisce il numero massimo di tentativi se si verifica il timeout del PPP prima di inviare un altro messaggio di richiesta CHAP. Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento non è disponibile. Il valore predefinito è 20.
- **NX_PPP_MAX_IPCP_PROTOCOL_RETRIES:** definisce il numero massimo di tentativi se si verifica il timeout del PPP prima di inviare un altro messaggio di richiesta di configurazione IPCP. Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento non è disponibile. Il valore predefinito è 20.
- **NX_PPP_MRU**: specifica l'unità di ricezione massima (MRU) per PPP. Per impostazione predefinita, questo valore è 1.500 byte (valore minimo). Questa definizione può essere impostata dall'applicazione prima *dell'inclusione di nx_ppp.h.*
- **NX_PPP_MINIMUM_MRU**: specifica la MRU minima ricevuta in un messaggio di richiesta di configurazione LCP. Per impostazione predefinita, questo valore è 1.500 byte (valore minimo). Questa definizione può essere impostata dall'applicazione prima *dell'inclusione di nx_ppp.h.*
- **NX_PPP_NAME_SIZE**: specifica le dimensioni delle stringhe "name" usate nell'autenticazione. Il valore predefinito è impostato su 32byte, ma può essere ridefinito prima dell'inclusione di *nx_ppp.h.
- **NX_PPP_PASSWORD_SIZE**: specifica le dimensioni delle stringhe "password" usate nell'autenticazione. Il valore predefinito è impostato su 32byte, ma può essere ridefinito prima dell'inclusione *di nx_ppp.h.*
- **NX_PPP_PROTOCOL_TIMEOUT**: definisce l'opzione di attesa (in secondi) per l'attività PPP per ricevere una risposta a un messaggio di richiesta del protocollo PPP. Il valore predefinito è 4 secondi.
- **NX_PPP_RECEIVE_TIMEOUTS:** definisce il numero di volte in cui si verifica il timeout dell'attività del thread PPP in attesa di ricevere il carattere successivo in un flusso di messaggi PPP. Successivamente, PPP rilascia il pacchetto e inizia ad attendere la ricezione del messaggio PPP successivo. Il valore predefinito è 4.
- **NX_PPP_SERIAL_BUFFER_SIZE**: specifica le dimensioni del buffer seriale dei caratteri di ricezione. Per impostazione predefinita, questo valore è 3.000 byte. Questa definizione può essere impostata dall'applicazione prima *dell'inclusione di nx_ppp.h.*
- **NX_PPP_TIMEOUT**: definisce l'opzione di attesa (in tick timer) per l'allocazione dei pacchetti per trasmettere i dati, nonché il buffer dei dati seriali PPP in pacchetti da inviare al livello IP. Il valore predefinito è 4*NX_IP_PERIODIC_RATE (400 tick).
- **NX_PPP_THREAD_TIME_SLICE:** opzione Time-slice per i thread PPP. Per impostazione predefinita, questo valore è TX_NO_TIME_SLICE. Questa definizione può essere impostata dall'applicazione prima *dell'inclusione di nx_ppp.h.*
- **NX_PPP_VALUE_SIZE**: specifica le dimensioni delle stringhe "valore" usate nell'autenticazione CHAP. Il valore predefinito è impostato su 32byte, ma può essere ridefinito prima dell'inclusione di nx_ppp.h.