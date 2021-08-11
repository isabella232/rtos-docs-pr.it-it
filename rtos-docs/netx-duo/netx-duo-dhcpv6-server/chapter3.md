---
title: Capitolo 3 - Azure RTOS di configurazione del server NetX Duo DHCPv6
description: Questo capitolo contiene una descrizione delle Azure RTOS di configurazione del server NetX Duo DHCPv6.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1dc0d6e41118a2f67fe98758f1f31f84d074d7af342b9db93162ffe6354077ea
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792129"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-server-configuration-options"></a>Capitolo 3 - Azure RTOS di configurazione del server NetX Duo DHCPv6

Sono disponibili diverse opzioni di configurazione per la compilazione di un'applicazione server NetX Duo DHCPv6. L'elenco seguente descrive ogni elemento in dettaglio:
  
- **NX_DISABLE_ERROR_CHECKING** Questa opzione rimuove il controllo degli errori DHCPv6. In genere è abilitata durante il debug dell'applicazione.  
  
- **NX_DHCPV6_SERVER_THREAD_STACK_SIZE** Definisce le dimensioni dello stack di thread DHCPv6. Per impostazione predefinita, la dimensione è di 4096 byte, che è più che sufficiente per la maggior parte delle applicazioni NetX Duo.

- **NX_DHCPV6_SERVER_THREAD_PRIORITY** Definisce la priorità del thread DHCPv6Server. Deve essere inferiore alla priorità dell'attività thread IP del server DHCPv6. Il valore predefinito è 2.

- **NX_DHCPV6_IP_LEASE_TIMER_INTERVAL** Intervallo del timer in secondi quando la funzione di immissione del timer di lease viene chiamata dall'utilità di pianificazione ThreadX. La funzione entry imposta un flag per il server DHCPv6 per incrementare il tempo accumulato di tutti i client nel lease in base all'intervallo del timer. Per impostazione predefinita, questo valore è 60.

- **NX_DHCPV6_SESSION_TIMER_INTERVAL** Intervallo del timer in secondi quando la funzione di immissione del timer della sessione viene chiamata dall'utilità di pianificazione ThreadX. La funzione entry imposta un flag per il server DHCPv6 per incrementare tutte le sessioni client attive accumulate dall'intervallo del timer. Per impostazione predefinita, questo valore è 3.

Le seguenti definisce si applicano al tipo di messaggio dell'opzione di stato e al messaggio configurabile dall'utente. L'opzione status indica il risultato di una richiesta client:

- **NX_DHCPV6_STATUS_MESSAGE_SUCCESS** *"OPZIONE IA CONCESSA"*

- **NX_DHCPV6_STATUS_NO_ADDRS_AVAILABLE** *"OPZIONE IA NON SONO DISPONIBILI INDIRIZZI SENZA CONCESSIONE"*

- **NX_DHCPV6_STATUS_MESSAGE_NO_BINDING** *"OPZIONE IA NON CONCESSA-RICHIESTA CLIENT NON VALIDA"*

- **NX_DHCPV6_STATUS_MESSAGE_NOT_ON_LINK** *"OPZIONE IA NON CONCESSA-CLIENT NON SUL COLLEGAMENTO"*

- **NX_DHCPV6_STATUS_MESSAGE_USE_MULTICAST** *"OPZIONE IA NON CONCESSA-CLIENT DEVE USARE MULTICAST"*

- **NX_DHCPV6_STATUS_MESSAGE_NO_ADDRS_AVAILABLE'OPZIONE** *IA NON SONO DISPONIBILI INDIRIZZI SENZA CONCESSIONE*

- **NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID** Creare un DUID del server con un ID assegnato dal fornitore. Si noti che il tipo DUID deve essere impostato NX_DHCPV6_DUID_TYPE_VENDOR_ASSIGNED.

- **NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_LENGTH** Imposta il limite superiore per l'ID assegnato dal fornitore. Il valore predefinito è 48.

- **NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID** Imposta il tipo aziendale del DUID sul tipo di fornitore privato.

- **NX_DHCPV6_PACKET_WAIT_OPTION** In questo modo viene definita l'opzione di attesa per la *chiamata nx_udp_socket_receive* server. Si tratta di una funzionalità perché il socket ha un callback di notifica di ricezione da NetX Duo, quindi il pacchetto è già accodato quando il server DHCPv6 chiama la funzione di ricezione. Il valore predefinito è 1 secondo (1 * NX_IP_PERIODIC_RATE).

- **NX_DHCPV6_SERVER_DUID_TYPE** Definisce il tipo DUID del server che il server include in tutti i messaggi ai client. Il valore predefinito è livello di collegamento più tempo (NX_DHCPV6_SERVER_DUID_TYPE_LINK_TIME).

- **NX_DHCPV6_SERVER_HW_TYPE** Definisce il tipo di hardware nel livello di collegamento DUID e il livello di collegamento più le opzioni tempor. Il valore predefinito è NX_DHCPV6_SERVER_HARDWARE_TYPE_ETHERNET.

- **NX_DHCPV6_PREFERENCE_VALUE** In questo modo viene definito il valore dell'opzione di preferenza compreso tra 0 e 255, dove maggiore è il valore, maggiore è la preferenza, nell'opzione DHCPv6 con lo stesso nome. Questo indica al client quale preferenza inserire nell'offerta di questo server in cui sono disponibili più server DHCPv6 per assegnare gli indirizzi IP. Il valore 255 indica al client di scegliere questo server. Il valore zero indica che il client è libero di scegliere. Il valore predefinito è zero.

- **NX_DHCPV6_MAX_OPTION_REQUEST_OPTIONS** Definisce il numero massimo di richieste di opzioni in una richiesta client che possono essere salvate in un record client. Il valore predefinito è 6.

- **NX_DHCPV6_DEFAULT_T1_TIME** Tempo in secondi assegnato dal server in un lease dell'indirizzo client per il momento in cui il client deve iniziare a rinnovare il proprio indirizzo IP. Il valore predefinito è 2000 secondi.

- **NX_DHCPV6_DEFAULT_T2_TIME** Tempo in secondi assegnato dal server in un lease dell'indirizzo client per il momento in cui il client deve iniziare a riassociare il proprio indirizzo IP presupponendo che il tentativo di rinnovo non sia riuscito. Il valore predefinito è 3000 secondi.

- **NX_DHCPV6_DEFAULT_PREFERRED_TIME** Definisce il tempo in secondi assegnato dal server per il momento in cui un lease di indirizzo IP client assegnato è deprecato. Il valore predefinito è 2 NX_DHCPV6_DEFAULT_T1_TIME.

- **NX_DHCPV6_DEFAULT_VALID_TIME** Definisce la scadenza in secondi assegnata dal server in un lease di indirizzo IP client assegnato. Alla scadenza di questo periodo di tempo, l'indirizzo IP del client non è valido. Il valore predefinito è 2 NX_DHCPV6_DEFAULT_PREFERRED_TIME.

- **NX_DHCPV6_STATUS_MESSAGE_MAX** Definisce le dimensioni massime del messaggio del server nel campo del messaggio dell'opzione di stato . Il valore predefinito è 100 byte.

- **NX_DHCPV6_MAX_LEASES** Definisce le dimensioni della tabella di lease IP del server, ad esempio il numero massimo di indirizzi IPv6 disponibili per il lease che possono essere archiviati. Per impostazione predefinita, tale valore è 100.

- **NX_DHCPV6_MAX_CLIENTS** Definisce le dimensioni della tabella dei record client del server,ad esempio il numero massimo di client che è possibile archiviare. Questo valore deve essere minore o uguale al valore NX_DHCPV6_MAX_LEASES. Per impostazione predefinita, questo valore è 120.

- **NX_DHCPV6_PACKET_TIME_OUT** Definisce l'opzione di attesa nei tick del timer per l'attesa del server DHCPv6 nelle allocazioni di pacchetti. Il valore predefinito è 3 * NX_DHCPV6_SERVER_TICKS_PER_SECOND.

- **NX_DHCPV6_PACKET_RECEIVE_WAIT** Definisce l'opzione wait nelle chiamate di allocazione di pacchetti nel pool di pacchetti del server. Il valore predefinito è (3 * NX_DHCPV6_SERVER_TICKS_PER_SECOND) o 3 secondi.

- **NX_DHCPV6_PACKET_SIZE** Definisce il payload dei pacchetti del pool di pacchetti del server. Il valore predefinito è 500 byte.

- **NX_DHCPV6_PACKET_POOL_SIZE** Definisce le dimensioni del pool di pacchetti del server per i pacchetti che verranno allocati dal server per l'invio di messaggi DHCPv6. Il valore predefinito è (10 * NX_DHCPV6_PACKET_SIZE).

- **NX_DHCPV6_TYPE_OF_SERVICE** Definisce il tipo di servizio per la trasmissione di pacchetti UDP. Per impostazione predefinita, questo valore è NX_IP_NORMAL.

- **NX_DHCPV6_FRAGMENT_OPTION** In questo modo viene definita l'opzione Frammentazione socket server. Il valore predefinito è NX_DON'T_FRAGMENT

- **NX_DHCPV6_TIME_TO_LIVE** Specifica il numero di router pacchetti DHCPv6 dal server può 'hop' passare prima che i pacchetti vengono eliminati. Il valore predefinito è impostato su 0x80.

- **NX_DHCPV6_QUEUE_DEPTH** Specifica il numero di pacchetti da mantenere nella coda di ricezione del socket UDP del server prima che NetX Duo scarti i pacchetti.