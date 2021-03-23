---
title: Capitolo 3-opzioni di configurazione del server DHCPv6 di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione delle opzioni di configurazione del server DHCPv6 di Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 30f6e1c657eb62ebec48d6bb8caafac320727146
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822907"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-server-configuration-options"></a>Capitolo 3-opzioni di configurazione del server DHCPv6 di Azure RTO NetX Duo

Sono disponibili diverse opzioni di configurazione per la creazione di un'applicazione server DHCPv6 NetX Duo. L'elenco seguente descrive tutti i dettagli:
  
- **NX_DISABLE_ERROR_CHECKING** Questa opzione rimuove il controllo degli errori di DHCPv6. Viene in genere attivata quando viene eseguito il debug dell'applicazione.  
  
- **NX_DHCPV6_SERVER_THREAD_STACK_SIZE** Definisce le dimensioni dello stack di thread DHCPv6. Per impostazione predefinita, la dimensione è di 4096 byte, che è più che sufficiente per la maggior parte delle applicazioni NetX Duo.

- **NX_DHCPV6_SERVER_THREAD_PRIORITY** Definisce la priorità del thread DHCPv6Server. Deve essere inferiore alla priorità dell'attività thread IP del server DHCPv6. Il valore predefinito è 2.

- **NX_DHCPV6_IP_LEASE_TIMER_INTERVAL** Intervallo di timer in secondi quando la funzione di immissione del timer di lease viene chiamata dall'utilità di pianificazione ThreadX. La funzione entry imposta un flag per il server DHCPv6 in modo da incrementare il tempo accumulato dei client nel lease dall'intervallo del timer. Per impostazione predefinita, questo valore è 60.

- **NX_DHCPV6_SESSION_TIMER_INTERVAL** Intervallo di timer in secondi quando la funzione di immissione del timer di sessione viene chiamata dall'utilità di pianificazione ThreadX. La funzione entry imposta un flag per il server DHCPv6 per incrementare tutto il tempo di sessione client attivo accumulato dall'intervallo del timer. Per impostazione predefinita, questo valore è 3.

Le definizioni seguenti si applicano al tipo di messaggio dell'opzione di stato e al messaggio configurabile dall'utente. L'opzione Status indica il risultato di una richiesta client:

- **NX_DHCPV6_STATUS_MESSAGE_SUCCESS** *"opzione Ia concessa"*

- **NX_DHCPV6_STATUS_NO_ADDRS_AVAILABLE** *"opzione Ia non concessa-nessun indirizzo disponibile"*

- **NX_DHCPV6_STATUS_MESSAGE_NO_BINDING** *"opzione Ia non concessa-richiesta client non valida"*

- **NX_DHCPV6_STATUS_MESSAGE_NOT_ON_LINK** *"opzione Ia non concessa-client non sul collegamento"*

- **NX_DHCPV6_STATUS_MESSAGE_USE_MULTICAST** *"opzione Ia non concessa-il client deve usare il multicast"*

- OPZIONE **NX_DHCPV6_STATUS_MESSAGE_NO_ADDRS_AVAILABLE** *Ia non concessa-nessun indirizzo disponibile*

- **NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID** Creare un server DUID con un ID assegnato al fornitore. Si noti che il tipo di DUID deve essere impostato NX_DHCPV6_DUID_TYPE_VENDOR_ASSIGNED.

- **NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_LENGTH** Imposta il limite superiore per l'ID assegnato al fornitore. Il valore predefinito è 48.

- **NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID** Imposta il tipo di organizzazione di DUID su tipo di fornitore privato.

- **NX_DHCPV6_PACKET_WAIT_OPTION** Definisce l'opzione wait per la chiamata al server *nx_udp_socket_receive* . Si tratta di un'operazione superficiale poiché il socket riceve un callback di notifica di ricezione da NetX Duo, quindi il pacchetto è già accodato quando il server DHCPv6 chiama la funzione receive. Il valore predefinito è 1 secondo (1 * NX_IP_PERIODIC_RATE).

- **NX_DHCPV6_SERVER_DUID_TYPE** Definisce il tipo di DUID del server che il server include in tutti i messaggi ai client. Il valore predefinito è link layer Plus Time (NX_DHCPV6_SERVER_DUID_TYPE_LINK_TIME).

- **NX_DHCPV6_SERVER_HW_TYPE** Definisce il tipo di hardware nel livello di collegamento DUID e le opzioni relative al livello di collegamento più tempo. Il valore predefinito è NX_DHCPV6_SERVER_HARDWARE_TYPE_ETHERNET.

- **NX_DHCPV6_PREFERENCE_VALUE** Definisce il valore dell'opzione di preferenza compreso tra 0 e 255, in cui maggiore è il valore più alto è la preferenza, nell'opzione DHCPv6 con lo stesso nome. Ciò indica al client la preferenza da inserire nell'offerta del server in cui sono disponibili più server DHCPv6 per l'assegnazione di indirizzi IP. Il valore 255 indica al client di scegliere questo server. Un valore pari a zero indica che il client è libero di scegliere. Il valore predefinito è zero.

- **NX_DHCPV6_MAX_OPTION_REQUEST_OPTIONS** Definisce il numero massimo di richieste di opzioni in una richiesta client che può essere salvato in un record client. Il valore predefinito è 6.

- **NX_DHCPV6_DEFAULT_T1_TIME** Tempo in secondi assegnato dal server in un lease di indirizzi client quando il client deve iniziare a rinnovare il proprio indirizzo IP. Il valore predefinito è 2000 secondi.

- **NX_DHCPV6_DEFAULT_T2_TIME** Tempo in secondi assegnato dal server in un lease di indirizzi client quando il client deve iniziare a riassociare il proprio indirizzo IP presumendo che il tentativo di rinnovo non sia riuscito. Il valore predefinito è 3000 secondi.

- **NX_DHCPV6_DEFAULT_PREFERRED_TIME** Definisce il tempo in secondi assegnato dal server per il momento in cui un lease di indirizzi IP client assegnato è deprecato. Il valore predefinito è 2 NX_DHCPV6_DEFAULT_T1_TIME.

- **NX_DHCPV6_DEFAULT_VALID_TIME** Definisce la scadenza in secondi assegnata dal server a un lease di indirizzi IP client assegnato. Al termine di questo periodo, l'indirizzo IP del client non è valido. Il valore predefinito è 2 NX_DHCPV6_DEFAULT_PREFERRED_TIME.

- **NX_DHCPV6_STATUS_MESSAGE_MAX** Definisce la dimensione massima del messaggio del server nel campo del messaggio di opzione di stato. Il valore predefinito è 100 byte.

- **NX_DHCPV6_MAX_LEASES** Definisce le dimensioni della tabella di lease IP del server, ad esempio il numero massimo di indirizzi IPv6 disponibili per il lease che è possibile archiviare. Per impostazione predefinita, tale valore è 100.

- **NX_DHCPV6_MAX_CLIENTS** Definisce le dimensioni della tabella di record client del server, ad esempio il numero massimo di client che possono essere archiviati. Questo valore deve essere minore o uguale al valore NX_DHCPV6_MAX_LEASES. Per impostazione predefinita, questo valore è 120.

- **NX_DHCPV6_PACKET_TIME_OUT** Definisce l'opzione wait nei cicli del timer per l'attesa del server DHCPv6 per le allocazioni dei pacchetti. Il valore predefinito è 3 * NX_DHCPV6_SERVER_TICKS_PER_SECOND.

- **NX_DHCPV6_PACKET_RECEIVE_WAIT** Definisce l'opzione wait nelle chiamate di allocazione pacchetti nel pool di pacchetti del server. Il valore predefinito è (3 * NX_DHCPV6_SERVER_TICKS_PER_SECOND) o 3 secondi.

- **NX_DHCPV6_PACKET_SIZE** Definisce il payload del pacchetto dei pacchetti del pool di pacchetti del server. Il valore predefinito è 500 byte.

- **NX_DHCPV6_PACKET_POOL_SIZE** Definisce le dimensioni del pool di pacchetti server per i pacchetti che il server alloca per inviare messaggi DHCPv6. Il valore predefinito è (10 * NX_DHCPV6_PACKET_SIZE).

- **NX_DHCPV6_TYPE_OF_SERVICE** Definisce il tipo di servizio per la trasmissione di pacchetti UDP. Per impostazione predefinita, questo valore è NX_IP_NORMAL.

- **NX_DHCPV6_FRAGMENT_OPTION** Definisce l'opzione di frammentazione del socket del server. Il valore predefinito è NX_DON ' T_FRAGMENT

- **NX_DHCPV6_TIME_TO_LIVE** Specifica il numero di router DHCPv6 che i pacchetti DHCPv6 dal server possono passare prima che i pacchetti vengano eliminati. Il valore predefinito è impostato su 0x80.

- **NX_DHCPV6_QUEUE_DEPTH** Specifica il numero di pacchetti da memorizzare nella coda di ricezione del socket UDP del server prima che NetX Duo elimini i pacchetti.