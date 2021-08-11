---
title: Capitolo 2 - Installazione e uso di Azure RTOS client NetX Duo DHCPv6
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS del client NetX Duo DHCPv6.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 481e29cc674edfa7e437e8e14253172b89aeae6856114192f4ca5b35717c91e0
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791534"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-dhcpv6-client"></a>Capitolo 2 - Installazione e uso di Azure RTOS client NetX Duo DHCPv6

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS del client NetX Duo DHCPv6.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il client NetX Duo DHCPv6 è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nxd_dhcpv6_client.h** File di intestazione per il client NetX DuoDHCPv6

- **nxd_dhcpv6_client.c** File di codice sorgente per il client NetX Duo DHCPv6

- **demo_netxduo_dhcpv6_client.c** Programma di esempio che illustra la configurazione del client NetX Duo DHCPv6

- **nxd_dhcpv6_client.pdf** Descrizione PDF del client NetX Duo DHCPv6

## <a name="netx-duo-dhcpv6-client-installation"></a>Installazione del client NetX Duo DHCPv6

Per usare l'API client DHCPv6 di NetX Duo, l'intera distribuzione indicata in precedenza può essere copiata nella stessa directory in cui è installato NetX Duo. Ad esempio, se NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_dhcpv6_client.h* e *nxd_dhpcv6_client.c* possono essere copiati in questa directory.

## <a name="using-the-netx-duo-dhcpv6-client"></a>Uso del client NetX Duo DHCPv6

Il codice dell'applicazione deve includere *nxd_dhcpv6_client.h* dopo aver incluso *tx_api.h* e *nx_api.h* per usare rispettivamente i servizi client DHCPv6, ThreadX e NetX Duo. *nxd_dhcpv6_client.c* deve essere compilato nel progetto nello stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato con i file dell'applicazione.

### <a name="span-classunderlineclient-dhcp-unique-identifier-duidspan"></a><span class="underline">DUID (Client DHCP Unique Identifier)</span>

Il DUID client definisce in modo univoco ogni client in una rete. Un'applicazione deve creare un DUID client prima di richiedere un indirizzo IPv6 a un server. Il DUID client viene incluso automaticamente in tutti i messaggi inviati al server. Per creare un DUID, l'applicazione chiama il servizio *nx_dhcpv6_create_client_duid:*
```C
UINT nx_dhcpv6_create_client_duid(NX_DHCPV6 *dhcpv6_ptr, 
                                  UINT duid_type, 
                                  UINT hardware_type, ULONG time);
```

L'applicazione chiama questo servizio e specifica il tipo di DUID (solo livello di collegamento o livello di collegamento più tempo). Per il livello di collegamento e i DUID di tempo, questo servizio fornirà il campo dell'ora se l'input dell'ora non è specificato.

Per i dispositivi che si riavviano e desiderano usare un lease di indirizzi IPv6 assegnato in precedenza, l'applicazione deve creare il DUID client come quello usato quando viene assegnato l'indirizzo IPv6. L'indirizzo del livello di collegamento è tutto ciò che serve per creare un DUID client del livello di collegamento. Questa operazione non richiede una precedente archiviazione di memoria non volatile se il dispositivo ha accesso all'indirizzo del livello di collegamento. Per i DUID di tipo time, l'applicazione deve avere accesso ai dati della stessa ora usati nella creazione duID precedente e ciò richiede memoria non volatile. I client che non dispongono di alcuna risorsa di archiviazione stabile non devono usare DUID di tipo time.

### <a name="span-classunderlineclient-identity-association-for-non-temporary-addresses-ianaspan"></a><span class="underline">Associazione di identità client per indirizzi non temporanei (IANA)</span>

L'applicazione deve creare un indirizzo IANA e, facoltativamente, uno o più indirizzi IA prima di richiedere un indirizzo IPv6. A tale scopo, l'applicazione chiama *nx_dhcpv6_create_client_iana* servizio. Per creare un'opzione di indirizzo IA, l'applicazione chiama il servizio *nx_dhcpv6_add_client_ia* con un indirizzo IPv6 richiesto e valori di durata come suggerimento per il server.

IANA e i relativi IA definiscono in modo cumulativo i parametri di assegnazione degli indirizzi IPv6 del client:

Prima di avviare il client DHCPv6, l'applicazione client DHCPv6 crea un'interfaccia IANA *usando* nx_dhcpv6_create_client_iana servizio:

```C
UINT    nx_dhcpv6_create_client_iana(NX_DHCPV6 *dhcpv6_ptr, 
                                     UINT IA_ident, ULONG T1, ULONG T2);
```

Deve anche creare uno o più IA usando il *servizio nx_dhcpv6_create_client_ia* e gli indirizzi IPv6 richiesti prima di avviare il client DHCPv6.

```C
UINT    nx_dhcpv6_add_client_ia(NX_DHCPV6 *dhcpv6_ptr, 
                                NXD_ADDRESS *ipv6_address, 
                                ULONG preferred_lifetime, 
                                ULONG valid_lifetime);
```

> [!NOTE]
> Il numero di indirizzi IA creati dall'applicazione non può superare NX_DHCPV6_MAX_IA_ADDRESS parametro il cui valore predefinito è 1.

Il client NetX Duo DHCPv6 supporta nx_dhcpv6_create_client_ia per le applicazioni client DHCPv6 legacy e che è identico a *nx_dhcpv6_add_client_ia,* ma gli sviluppatori sono invitati a usare il *servizio* nx_dhcpv6_add_client_ia. 

Questi servizi sono illustrati in "Small Example System" in altre parti di questo capitolo.

### <a name="span-classunderlinenon-volatile-memory-considerations-to-reuse-ianas-and-iasspan"></a><span class="underline">Considerazioni sulla memoria non volatile per il riutilizzo di IANA e IA</span>

L'applicazione deve salvare i parametri IANA T1, T2 e l'identificatore IANA in memoria non volatile se vuole usare gli stessi indirizzi al riavvio. L'applicazione deve anche salvare il proprio IA che include il relativo indirizzo IPv6 in memoria non volatile.

L'applicazione deve inoltre archiviare il tempo trascorso che è stato associato ai lease di indirizzi IPv6 assegnati alla memoria non volatile in caso di arresto. A tale scopo, chiama *il nx_dhcpv6_get_time_accrued* prima di arrestare il client DHCPv6.

```C
UINT nx_dhcpv6_get_time_accrued(NX_DHCPV6 *dhcpv6_ptr, 
                                ULONG *time_accrued);
```

Supponendo che l'applicazione abbia un orologio indipendente per tenere traccia dell'intervallo di tempo dal momento in cui è stato arrestato e riavviato il client DHCPv6 dopo un riavvio, viene aggiunto a tale tempo trascorso al tempo accumulato nel lease IPv6 prima dell'arresto. Avvia ora l'attività thread client con il tempo totale trascorso associato al lease IPv6 come input nv_time seguente:

```C
UINT nx_dhcpv6_start(NX_DHCPV6 *dhcpv6_ptr, ULONG nv_time);
```

A questo punto, l'attività del thread del client DHCPv6 prenderà il controllo del tempo accumulato nel lease IPv6 per il momento in cui rinnovare il lease.

### <a name="span-classunderlinesetting-dhcpv6-option-dataspan"></a><span class="underline">Impostazione dei dati delle opzioni DHCPv6</span>

Prima di richiedere un lease IPv6, l'applicazione può richiedere altri dati dei parametri di rete, ad esempio il server DNS e il server di ora. Alcuni di questi parametri hanno servizi specifici. Di seguito sono riportati alcuni esempi:

```C
UINT  nx_dhcpv6_request_option_DNS_server(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT enable)

UINT  nx_dhcpv6_request_option_time_server(NX_DHCPV6 *dhcpv6_ptr, 
                                           UINT enable);
```

### <a name="span-classunderlineinitiating-the-ipv6-address-requestspan"></a><span class="underline">Avvio della richiesta dell'indirizzo IPv6</span>

L'applicazione avvia il thread del client DHCPv6 chiamando *nx_dhcpv6_start* servizio con un input zero-time. Per avviare il protocollo DHCPv6 per richiedere un indirizzo IPv6, l'applicazione chiama *nx_dhcpv6_request_solicit.*

Se l'applicazione vuole usare un lease IPv6 assegnato in precedenza, chiama nx_dhcpv6_start *con* un input di tempo diverso da zero. Non deve chiamare *nx_dhcpv6_request_solicit*.

Successivamente, l'applicazione non deve eseguire altre attività e il client DHCPv6 eseguirà automaticamente il monitoraggio quando è il momento di rinnovare o riassociare un indirizzo IPv6.

## <a name="small-example-system"></a>Small Example System

Un esempio di quanto sia semplice usare il client NetX Duo DHCPv6 è descritto nel piccolo esempio seguente usando un client DHCPv6 e un driver "RAM" virtuale. Questa demo presuppone un dispositivo con una sola interfaccia di rete fisica.

*tx_application_define* crea un pool di pacchetti per il client DHCPv6 per l'invio di messaggi DHCPv6. Crea anche un thread dell'applicazione e un'istanza IP. Abilita quindi UDP e ICMP su IP nelle righe 130-148. Il client DHCPv6 viene quindi creato con le funzioni di callback state change (*dhcpv6_state_change_notify* ) e server error (*dhcpv6_server_error_handler*) nella riga 151.

Nella funzione di immissione thread *client, thread_client_entry*, l'indirizzo IP client è configurato con un indirizzo locale di collegamento e abilitato per i servizi IPv6 e ICMPv6 alle righe 202-217. Prima di avviare il client DHCPv6, l'applicazione crea un DUID client, un'opzione IANA e un'opzione di indirizzo IA nelle righe 219-303. L'opzione indirizzo IA è facoltativa se il client desidera richiedere un indirizzo IPv6 e durate valide e preferite dal server. Il server può concedere o meno l'indirizzo IPv6 richiesto o i tempi di lease. L'applicazione può aggiungere altre opzioni IA (fino NX_DHCPV6_MAX_IA_ADDRESS) a cui assegnare più indirizzi globali.

Infine, l'applicazione imposta varie opzioni per richiedere i parametri di rete nei messaggi al server DHCPv6. L'attività client DHCPv6 viene avviata chiamando *nx_dhcpv6_start* nella riga 306 e il protocollo DHCPv6 effettivo viene avviato nello stato SOLICIT con la chiamata *a nx_dhcpv6_request_solicit* nella riga 317. Il client DHCPv6 gestisce quindi automaticamente l'innalzamento di livello dello stato del client tramite il protocollo DHCPv6 fino a quando non viene associato a un indirizzo o non si verifica un errore. Durante questo periodo di tempo, l'applicazione attende il completamento del protocollo, nonché il completamento del rilevamento degli indirizzi duplicati (DUPLICATE Address Detection) se l'istanza IP è configurata per ILVA (configurazione predefinita).

Dopo la chiamata tx_thread_sleep, l'applicazione controlla i parametri globali impostati nel callback di modifica dello stato per determinare l'esito positivo dell'attività client DHCPv6 per l'assegnazione di un lease IPv6 e, in tal caso, il controllo DELL'univocità. Questa operazione viene eseguita usando i contatori impostati nelle funzioni di modifica dello stato e di callback degli errori del server. L'applicazione esegue il polling di conteggi non zero di address_not_assigned, address_expired e server_errors per l'assegnazione di indirizzi non riuscita. Se il numero di bound_addresses è diverso da zero (almeno un indirizzo assegnato correttamente), verifica la presenza di un address_failed_dad diverso da zero per un controllo NON RIUSCITO. Di seguito viene fornita una spiegazione della modifica dello stato e dei callback degli errori del server:

Il callback di modifica dello *stato, dhcpv6_state_change_notify*, lo stato client DHCPv6 precedente e corrente per determinare se il client ha ricevuto risposte server valide:

  - *dhcpv6_state_change_notify* verifica la presenza di transizioni direttamente da SOLICIT a INIT e, in tal caso, incrementa un contatore per il client DHCPv6 che non riceve risposte dal server.

*Successivamente dhcpv6_state_change_notify* verifica se il client è stato assegnato (associato) a uno o più indirizzi IPv6:

  - Se il nuovo stato è BOUND, incrementa un contatore di indirizzi associati al client.
    
Il *dhcpv6_state_change_notify* verifica anche la presenza di un controllo NON riuscito DI TIPO CHECK:

  - Se lo stato passa da DECLINE a INIT, il client DHCPv6 non ha superato il controllo DELL'ISTRUZIONE PER UNO degli indirizzi assegnati e incrementa il numero di assegnazioni di indirizzi non riusciti.
    
L'ultimo controllo *eseguito dhcpv6_state_change_notify* in questo esempio è che un indirizzo assegnato correttamente che ha superato il controllo DELLA CONVALIDA NON può essere rinnovato o riassociato:

  - Se lo stato cambia da REBIND a INIT, il client non ha avuto risposte alle richieste RENEW o REBIND e *dhcpv6_state_change_notify* incrementa il numero di indirizzi scaduti.

Il *dhcpv6_server_error_handler* se viene notificato dall'attività client DHCPv6 di uno stato di errore ricevuto dal server incrementa il numero di errori del server.

Supponendo che tutto vada bene, l'applicazione esegue una query sul client DHCPv6 per i dati degli indirizzi, inclusi i tempi di lease. Ottiene un conteggio degli indirizzi validi (assegnati correttamente) chiamando il servizio *nx_dhcpv6_get_valid_ip_address_count* e il tempo di rinnovo in IANA (si applica a tutti gli indirizzi IA assegnati) chiamando *nx_dhcpv6_get_iana_lease_time* sulle righe 372-392. Esegue quindi una query sul client DHCPv6 per ognuna delle relative opzioni IA per l'indirizzo IPv6 e i tempi di lease in base all'indice degli indirizzi.

Alcuni servizi client DHCPv6 (*nx_dhcpv6_get_lease_time_data, nx_dhcpv6_get_IP_address*) non richiedono un indice di indirizzi come input e restituiscono parametri DHCPv6 per l'indirizzo globale del client primario. Questa opzione è adatta per i client con un singolo indirizzo IPv6 globale quando *chiama nx_dhcpv6_get_valid_ip_address_lease_time* nella riga 384.

La configurazione del client DHCPv6, NX_DHCPV6_CLIENT_RESTORE_STATE, t consente a un sistema di ripristinare un client DHCPv6 creato in precedenza in stato associato tra un riavvio del sistema e l'altro. Chiamando il *nx_dhcpv6_client_get_record* per ottenere il record del client DHCPv6 tra un riavvio del sistema e l'altro alla riga 434, chiamando *il nx_dhcpv6_client_restore_record per* archiviare il record del client DHCPv6 dopo l'accensione del sistema sulla riga 525.

L'applicazione rilascia quindi gli indirizzi assegnati usando *nx_dhcpv6_request_release* servizio nella riga 552. Per riavviare l'applicazione, arresta il client DHCPv6 con il servizio *nx_dhcpv6_client_stop* nella riga 567 e cancella tutti gli indirizzi IPv6 registrati con l'istanza IP configurata tramite il client DHCPv6. A tale scopo, chiama *nx_dhcpv6_reinitialize* nella riga 578. Riavvia quindi l'attività client DHCPv6 *con* nx_dhcpv6_start e *nx_dhcpv6_request_solicit* come in precedenza.

Il client DHCPv6 viene eliminato con la chiamata a *nx_dhcpv6_delete* nella riga 626. Si noti che non elimina il pool di pacchetti creato per il client DHCPv6 perché questo pool di pacchetti viene usato anche dall'istanza IP. In caso contrario, dovrebbe eliminare il pool di pacchetti se non è più necessario usarlo con il servizio di nx_packet_pool_delete NetX *Duo.*

```C
/* This is a small demo of the NetX Duo DHCPv6 Client for the high-performance NetX Duo stack. */

#include    <stdio.h>
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nxd_dhcpv6_client.h"

#ifdef FEATURE_NX_IPV6
#define     DEMO_STACK_SIZE         2048

/* Set the client address, and request these address from DHCPv6 Server. */
/*
#define     NX_DHCPV6_REQUEST_IA_ADDRESS
*/

/* Set the list of DHCPv6 option data (timezone, DNS server, timer server, domain name)to get from the DHCPv6 server. */

#define     NX_DHCPV6_REQUEST_OPTION


/* Add the fully qualified domain name to request whether the DHCPv6 server SHOULD or SHOULD NOT perform the AAAA RR or DNS updates. */

#define     NX_DHCPV6_REQUEST_FQDN_OPTION


/* Define the ThreadX and NetX object control blocks... */

NX_PACKET_POOL          pool_0;
TX_THREAD               thread_client;
NX_IP                   client_ip;

/* Define the Client and Server instances. */

NX_DHCPV6               dhcp_client;

/* Define the error counter used in the demo application... */
ULONG                   error_counter;
CHAR                    *pointer;

/* Define thread prototypes. */
void    thread_client_entry(ULONG thread_input);

/***** Substitute your ethernet driver entry function here *********/
extern VOID    _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

/* Declare DHCPv6 Client callbacks */
VOID dhcpv6_state_change_notify(NX_DHCPV6 *dhcpv6_ptr, UINT old_state, UINT new_state);
VOID dhcpv6_server_error_handler(NX_DHCPV6 *dhcpv6_ptr, UINT op_code, UINT status_code, UINT message_type);

/* Set up globals for tracking changes to DHCPv6 Client from callback services. */
UINT state_changes = 0;
UINT address_expired = 0;
UINT address_failed_dad = 0;
UINT bound_addresses = 0;
UINT address_not_assigned = 0;
UINT server_errors = 0;

/* Define some DHCPv6 parameters. */

#define DHCPV6_IANA_ID      0xC0DEDBAD
#define DHCPV6_T1           NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_T2           NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_RENEW_TIME   NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_REBIND_TIME  NX_DHCPV6_INFINITE_LEASE
#define PACKET_PAYLOAD      500
#define PACKET_POOL_SIZE    (5*PACKET_PAYLOAD)

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}


/* Define what the initial system looks like. */

void    tx_application_define(void *first_unused_memory)
{

UINT    status;

    /* Setup the working pointer. */
    pointer =  (CHAR *) first_unused_memory;

    /* Create the Client thread. */
    status = tx_thread_create(&thread_client, "Client thread", thread_client_entry, 0,
                              pointer, DEMO_STACK_SIZE, 8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Check for IP create errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status =  nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 1024,  pointer, PACKET_POOL_SIZE);

    pointer = pointer + PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Create a Client IP instance. */
    status = nx_ip_create(&client_ip, "Client IP", IP_ADDRESS(0, 0, 0, 0),
                          0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                          pointer, 2048, 1);

    pointer =  pointer + 2048;

    /* Check for IP create errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Enable UDP traffic for sending DHCPv6 messages. */
    status =  nx_udp_enable(&client_ip);

    /* Check for UDP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Enable ICMP. */
    status =  nx_icmp_enable(&client_ip);

    /* Check for ICMP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Create the DHCPv6 Client. */
    status =  nx_dhcpv6_client_create(&dhcp_client, &client_ip, "DHCPv6 Client",
                                      &pool_0, pointer, 2048, dhcpv6_state_change_notify,
                                      dhcpv6_server_error_handler);

    /* Check for errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Update the stack pointer because we need it again. */
    pointer = pointer + 2048;

    /* Yield control to DHCPv6 threads and ThreadX. */
    return;
}


/* Define the Client host application thread. */

void    thread_client_entry(ULONG thread_input)
{

UINT        status;
ULONG       T1, T2;
UINT        address_count;
UINT        address_index = 0;
NXD_ADDRESS valid_ipv6_address;
ULONG       preferred_lifetime;
ULONG       valid_lifetime;
UINT        ia_count = 1;

#ifdef NX_DHCPV6_REQUEST_IA_ADDRESS
NXD_ADDRESS ipv6_address;
#endif

#ifdef NX_DHCPV6_REQUEST_OPTION
UCHAR       buffer[200];
NXD_ADDRESS dns_server;
#endif

#ifdef NX_DHCPV6_CLIENT_RESTORE_STATE
ULONG       current_time;
ULONG       elapsed_time;
NX_DHCPV6_CLIENT_RECORD dhcpv6_client_record;
#endif


    state_changes = 0;

    /* Establish the link local address for the host. The RAM driver creates
       a virtual MAC address of 0x1122334456. */
    status = nxd_ipv6_address_set(&client_ip, 0, NX_NULL, 10, NULL);

    if (status)
    {
        error_counter++;
        return;
    }

    /* Let NetX Duo get initialized. */
    tx_thread_sleep(50);

    /* Enable the Client IP for IPv6 and ICMPv6 services. */
    nxd_ipv6_enable(&client_ip);
    nxd_icmp_enable(&client_ip);

    /* Create a Link Layer Plus Time DUID for the DHCPv6 Client. Set time ID field
       to NULL; the DHCPv6 Client API will supply one. */
    status = nx_dhcpv6_create_client_duid(&dhcp_client, NX_DHCPV6_DUID_TYPE_LINK_TIME,
                                          NX_DHCPV6_HW_TYPE_IEEE_802, 0);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Create the DHCPv6 client's Identity Association (IA-NA) now.

       Note that if this host had already been assigned in IPv6 lease, it
       would have to use the assigned T1 and T2 values in loading the DHCPv6
       client with an IANA block.
    */
    status = nx_dhcpv6_create_client_iana(&dhcp_client, DHCPV6_IANA_ID, DHCPV6_T1,  DHCPV6_T2);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

#ifdef NX_DHCPV6_REQUEST_IA_ADDRESS
    memset(&ipv6_address,0x0, sizeof(NXD_ADDRESS));
    ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
    ipv6_address.nxd_ip_address.v6[0] = 0x3ffe0501;
    ipv6_address.nxd_ip_address.v6[1] = 0xffff0100;
    ipv6_address.nxd_ip_address.v6[2] = 0x00000000;
    ipv6_address.nxd_ip_address.v6[3] = 0x0000abcd;

    /* Create an IA address option.
        Note that if this host had already been assigned in IPv6 lease, it
        would have to use the assigned IPv6 address, preferred and valid lifetime
        values in loading the DHCPv6 Client with an IA block.
    */
    status = nx_dhcpv6_add_client_ia(&dhcp_client, &ipv6_address,DHCPV6_RENEW_TIME, DHCPV6_REBIND_TIME);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* If the DHCPv6 Client is configured for a maximum number of IA addresses
       greater than 1, we can add another IA address if the device requires
       multiple global IPv6 addresses. */
    if(NX_DHCPV6_MAX_IA_ADDRESS >= 2)
    {
        memset(&ipv6_address,0x0, sizeof(NXD_ADDRESS));
        ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
        ipv6_address.nxd_ip_address.v6[0] = 0x3ffe0501;
        ipv6_address.nxd_ip_address.v6[1] = 0xffff0100;
        ipv6_address.nxd_ip_address.v6[2] = 0x00000000;
        ipv6_address.nxd_ip_address.v6[3] = 0x00001234;

        /* Add another  IA address option. */
        status = nx_dhcpv6_add_client_ia(&dhcp_client, &ipv6_address, DHCPV6_RENEW_TIME, DHCPV6_REBIND_TIME);

        if (status != NX_SUCCESS)
        {
            error_counter++;
            return;
        }
    }
#endif /* NX_DHCPV6_REQUEST_IA_ADDRESS  */

#ifdef NX_DHCPV6_REQUEST_OPTION
    /* Set the list of DHCPv6 option data to get from the DHCPv6 server if needed. */
    nx_dhcpv6_request_option_timezone(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_DNS_server(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_time_server(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_domain_name(&dhcp_client, NX_TRUE);
#endif /* NX_DHCPV6_REQUEST_OPTION */


#ifdef NX_DHCPV6_REQUEST_FQDN_OPTION
    /* Set the DHCPv6 Client FQDN option.
       operation: NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR         DHCPv6 Client choose to updating the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the client.
                  NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE   DHCPv6 Client choose to updating the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the client to the server.
                  NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE   DHCPv6 Client choose to request that the server perform no DNS updatest on its behalf. */
    nx_dhcpv6_request_option_FQDN(&dhcp_client, "DHCPv6-Client", NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR);
#endif /* NX_DHCPV6_REQUEST_FQDN_OPTION */

    /* Start up the NetX DHCPv6 Client thread task. */
    status =  nx_dhcpv6_start(&dhcp_client);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Start the DHCPv6 by sending a Solicit message out on the network. */
    status = nx_dhcpv6_request_solicit(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Is the DHCPv6 Client request for address assignment successfully started? */
    if (status == NX_SUCCESS)
    {

        /* If Duplicate Address Detection (DAD) is enabled in NetX Duo, e.g. #NXDUO_DISABLE_DAD
           not defined, allow time for NetX Duo to verify the address is unique on our network.
         */
        tx_thread_sleep(500);

        /* Check the bound address. */
        if (bound_addresses != ia_count)
        {

            /* Attempt to find out why DHCPv6 failed, where...*/

            if (server_errors > 0)
            {
                /* Actually you would compare server_error count with number of IA's added
                   to determine if any addresses were assigned. */
                printf("Server error, not all address assigned\n");
            }

            if (address_not_assigned > 0)
            {
                /* Actually you would compare address not assigned count with number of IA's added
                   to determine if any addresses were assigned. */

                printf("No servers responded to some or all of our IAs\n");
            }

        }

        /* Regardless if the DHCPv6 Client achieved a bound state, check for DAD
           failures. */
        if (address_failed_dad > 0)
        {
            /* Actually you would compare failed dad count with number of IA's added
               to determine if any addresses were assigned. */

            printf("Some or all of our IAs failed DAD\n");

        }

        /* Successfully assigned IPv6 addresses! */

        /* Get the count of valid IPv6 address obtained by DHCPv6. */
        status = nx_dhcpv6_get_valid_ip_address_count(&dhcp_client, &address_count);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IPv6 address and related lifetimes by address index. This index is the
           index into the DHCPv6 Client address table. Not to be confused with the IP
           instance address table! */
        status = nx_dhcpv6_get_valid_ip_address_lease_time(&dhcp_client, address_index,
                                                           &valid_ipv6_address, 
                                                               &preferred_lifetime,
                                                           &valid_lifetime);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IANA options for when to start renew/rebind requests. These time
           parameters are the same for all IPv6 addresses assigned in the Client
           e.g. IANA returned from Server. */
        status = nx_dhcpv6_get_iana_lease_time(&dhcp_client, &T1, &T2);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /*****************************************************************************/
        /* These are 'legacy' DHCPv6 services and are for the most part identical to the services
           above except they default to the primary global IPv6 address regardless if the
           Client was assigned more than one global IPv6 address. */

        /* Now check the assigned lease times. */
        status = nx_dhcpv6_get_lease_time_data(&dhcp_client, &T1, &T2,
                                               &preferred_lifetime, &valid_lifetime);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IP address. */
        status = nx_dhcpv6_get_IP_address(&dhcp_client, &valid_ipv6_address);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Bound state. */

#ifdef NX_DHCPV6_CLIENT_RESTORE_STATE

        /* Get the DHCPv6 Client record. */
        nx_dhcpv6_client_get_record(&dhcp_client, &dhcpv6_client_record);

        /* Delete DHCPv6 instance. */
        nx_dhcpv6_client_delete(&dhcp_client);

        /* Delete IP instance. */
        status = nx_ip_delete(&client_ip);

        /* Check for error. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Create a Client IP instance. */
        status = nx_ip_create(&client_ip, "Client IP", IP_ADDRESS(0, 0, 0, 0),
                              0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                              pointer, 2048, 1);

        pointer =  pointer + 2048;

        /* Check for IP create errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable UDP traffic for sending DHCPv6 messages. */
        status =  nx_udp_enable(&client_ip);

        /* Check for UDP enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable ICMP. */
        status =  nx_icmp_enable(&client_ip);

        /* Check for ICMP enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable the Client IP for IPv6 and ICMPv6 services. */
        status = nxd_ipv6_enable(&client_ip);
        status += nxd_icmp_enable(&client_ip);

        /* Check for IPv6 and ICMPv6 enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Establish the link local address for the host. The RAM driver creates
           a virtual MAC address of 0x1122334456. */
        status = nxd_ipv6_address_set(&client_ip, 0, NX_NULL, 10, NULL);

        if (status)
        {
            error_counter++;
            return;
        }

        /* If Duplicate Address Detection (DAD) is enabled in NetX Duo, e.g. #NXDUO_DISABLE_DAD
           not defined, allow time for NetX Duo to verify the address is unique on our network.
         */
        tx_thread_sleep(500);

        /* Create the DHCPv6 Client. */
        status =  nx_dhcpv6_client_create(&dhcp_client, &client_ip, "DHCPv6 Client",
                                          &pool_0, pointer, 2048, dhcpv6_state_change_notify,
                                          dhcpv6_server_error_handler);

        /* Check for errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Update the stack pointer because we need it again. */
        pointer = pointer + 2048;

        /* Restore the DHCPv6 record. */
        nx_dhcpv6_client_restore_record(&dhcp_client, &dhcpv6_client_record, 5);

        /* Resume the DHCPv6 service. */
        nx_dhcpv6_resume(&dhcp_client);
#endif


#ifdef NX_DHCPV6_REQUEST_OPTION

        /* Get the DNS Server address. */
        nx_dhcpv6_get_DNS_server_address(&dhcp_client, 0, &dns_server);

        /* Get the domain name. */
        memset(buffer, 0, sizeof(buffer));

        nx_dhcpv6_get_other_option_data(&dhcp_client, NX_DHCPV6_DOMAIN_NAME_OPTION, buffer, 200); // Try to get DNS info got from DHCPv6 Server

        /* Get the domain name. */
        memset(buffer, 0, sizeof(buffer));

        /* Get the time zone. */
        nx_dhcpv6_get_other_option_data(&dhcp_client, NX_DHCPV6_NEW_POSIX_TIMEZONE_OPTION, buffer, 200); // Try to get DNS info got from DHCPv6 Server
#endif

        /* At some point, we may wish to release the IPv6 address lease e.g. the device
           is leaving the network or powering down. In that case we inform the
           DHCPv6 Server that we are releasing the address lease. */
        status = nx_dhcpv6_request_release(&dhcp_client);

        /* Check status. */
        if (status != NX_SUCCESS)
        {

            error_counter++;
            return;
        }

        /* Send the release message. */
        tx_thread_sleep(100);
    }

    /* Stopping the Client task. */
    status = nx_dhcpv6_stop(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Clear the previously assigned IPv6 addresses from the Client and IP address table. */
    status = nx_dhcpv6_reinitialize(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Start up the Client task again. */
    status = nx_dhcpv6_start(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Begin the request process by sending a Solicit message with the IA created above
       with our preferred IPv6 address. */
    status = nx_dhcpv6_request_solicit(&dhcp_client);
    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Wait a bit before releasing the IP address and terminating the client. */
    tx_thread_sleep(500);

    /* Ok, lets stop the application. Again we DO NOT plan
       to keep the IPv6 address we were assigned and need to release it
       back to the DHCPv6 server. */
    status = nx_dhcpv6_request_release(&dhcp_client);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    /* Now delete the DHCPv6 client and release ThreadX and
       NetX Duo resources back to the system. */
    nx_dhcpv6_client_delete(&dhcp_client);


    return;

}


/* This is the notification from the DHCPv6 Client task that it has changed
   state in the DHCPv6 protocol, for example getting assigned an IPv6 lease and
   achieving the bound state or an IPv6 lease expires and being reset to
   the init state.
*/
VOID dhcpv6_state_change_notify(NX_DHCPV6 *dhcpv6_ptr, UINT old_state, UINT new_state)
{


    /* Increment state change counter. */
    state_changes++;

    /* Check if the Client attempted to request an IPv6 lease but no servers
       responded. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_SOLICIT) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that either DAD failed or IP lease expired. */
        address_not_assigned++;
    }

    /* Check if the Client has been assigned an IPv6 lease. */
    if (new_state == NX_DHCPV6_STATE_BOUND_TO_ADDRESS)
    {
        bound_addresses++;
    }

   /* Check if the Client was bound, but failed the uniqueness check
       (Duplicate Address Detection) and was reset to the INIT state. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_DECLINE) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that DAD failed on Client IA. */
        address_failed_dad++;
    }

    /* Check if the Client was bound, attempted renew the lease but the
       IPv6 address renewal/rebinding failed. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_REBIND) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that the IP lease expired. */
        address_expired++;
    }



    /* Other checks are possible. */

}

/* This is the notification from the DHCPv6 Client task that it received an error
   from the server (status code) in response to the Client's last DHCPv6 message.
*/

VOID dhcpv6_server_error_handler(NX_DHCPV6 *dhcpv6_ptr, UINT op_code, UINT status_code, UINT message_type)
{

    /* Increment the server error count. */
    server_errors++;

    /* This should distinguish between receiving a server error and no server
       available to assign the Client an IPv6 address if the Client fails
       to get assigned an address. */
}

#endif /* FEATURE_NX_IPV6 */
```
