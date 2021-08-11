---
title: Capitolo 3 - Azure RTOS di configurazione di NetX Duo DHCPv6
description: Sono disponibili diverse opzioni di configurazione per la Azure RTOS NetX Duo DHCPv6.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 129d1421215452448b1de4626fdeda530a5466bd63ed0c758676c3ad60f9d6fb
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782422"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-configuration-options"></a>Capitolo 3 - Azure RTOS di configurazione di NetX Duo DHCPv6

Sono disponibili diverse opzioni di configurazione per la Azure RTOS NetX Duo DHCPv6. L'elenco seguente descrive ognuno in dettaglio:  
  
  
- **NX_DHCPV6_THREAD_PRIORITY** Priorità del thread client. Per impostazione predefinita, questo valore specifica che il thread client viene eseguito con priorità 2.

- **NX_DHCPV6_MUTEX_WAIT** Opzione di timeout per ottenere un blocco esclusivo su un mutex del client DHCPv6. Il valore predefinito è TX_WAIT_FOREVER.

- **NX_DHCPV6_TICKS_PER_SECOND** Rapporto tra tick e secondi. Dipende dal processore. Il valore predefinito è 100.

- **NX_DHCPV6_IP_LIFETIME_TIMER_INTERVAL**  Intervallo di tempo in secondi in cui il timer di durata IP aggiorna il periodo di tempo in cui l'indirizzo IP corrente è stato assegnato al client. Per impostazione predefinita, questo valore è 1.

- **NX_DHCPV6_SESSION_TIMER_INTERVAL**  Intervallo di tempo in secondi in cui il timer della sessione aggiorna il periodo di tempo durante il quale il client è stato in sessione comunicando con il server. Per impostazione predefinita, questo valore è 1.

- **NX_DHCPV6_MAX_IA_ADDRESS** Numero massimo di indirizzi IA che possono essere aggiunti al record client. Il valore predefinito è 1. 

- **NX_DHCPV6_NUM_DNS_SERVERS** Numero di server DNS da archiviare nel record client. Il valore predefinito è 2.

- **NX_DHCPV6_NUM_TIME_SERVERS** Numero di server di tempo da archiviare nel record client. Il valore predefinito è 1.

- **NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE**  Dimensioni del buffer nel record client per contenere il nome di dominio di rete del client. Il valore predefinito è 30.

- **NX_DHCPV6_TIME_ZONE_BUFFER_SIZE**  Dimensioni del buffer nel record client per contenere il fuso orario del client. Il valore predefinito è 10.

- **NX_DHCPV6_MAX_MESSAGE_SIZE** Dimensione del buffer nel record client per contenere il messaggio di stato dell'opzione in una risposta del server. Il valore predefinito è 100 byte.

- **NX_DHCPV6_PACKET_TIME_OUT** Timeout in secondi per l'allocazione di un pacchetto dal pool di pacchetti client. Il valore predefinito è 3 secondi.

- **NX_DHCPV6_TYPE_OF_SERVICE** Definisce il tipo di servizio per la trasmissione di pacchetti UDP dal socket client DHCPv6. Il valore predefinito è **NX_IP_NORMAL**.

- **NX_DHCPV6_TIME_TO_LIVE** Numero di volte in cui un pacchetto client viene inoltrato da un router di rete prima che il pacchetto venga eliminato. Il valore predefinito è 0x80.

- **NX_DHCPV6_QUEUE_DEPTH** Specifica il numero di pacchetti da mantenere nella coda di ricezione socket UDP client prima che NetX Duo scarti i pacchetti. Il valore predefinito è 5.

## <a name="dhcpv6-message-transmission"></a>Trasmissione di messaggi DHCPv6

È presente un set di opzioni client DHCPv6 per l'impostazione dei parametri sulla trasmissione di messaggi DHCPv6. Si tratta di: 

  - timeout iniziale

  - ritardo massimo alla prima trasmissione

  - timeout di ritrasmissione massimo 

  - numero massimo di ritrasmissioni 

  - durata massima di attesa della risposta del server

Questi parametri si applicano a ognuno dei messaggi del client DHCPv6:

- Sollecitare

- Richiesta

- Rinnovare

- Riassociare

- RELEASE

- Declino

- CONFERMA

- Informare

Di seguito è riportato un elenco completo di queste opzioni configurabili e delle relative impostazioni predefinite 

values:

```C
NX_DHCPV6_FIRST_SOL_MAX_DELAY                   (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_INIT_SOL_TRANSMISSION_TIMEOUT         (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_SOL_RETRANSMISSION_TIMEOUT        (120 *
                                                NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_SOL_RETRANSMISSION_COUNT          0
NX_DHCPV6_MAX_SOL_RETRANSMISSION_DURATION       0

NX_DHCPV6_INIT_REQ_TRANSMISSION_TIMEOUT         (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_REQ_RETRANSMISSION_TIMEOUT        (30 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_REQ_RETRANSMISSION_COUNT          10
NX_DHCPV6_MAX_REQ_RETRANSMISSION_DURATION       0

NX_DHCPV6_INIT_RENEW_TRANSMISSION_TIMEOUT       (10*NX_DHCPV6_TICKS_PER_SECOND)     
NX_DHCPV6_MAX_RENEW_RETRANSMISSION_TIMEOUT      (600*   
                                                NX_DHCPV6_TICKS_PER_SECOND)  
NX_DHCPV6_MAX_RENEW_RETRANSMISSION_COUNT        0

NX_DHCPV6_INIT_REBIND_TRANSMISSION_TIMEOUT      (10*NX_DHCPV6_TICKS_PER_SECOND)     
NX_DHCPV6_MAX_REBIND_RETRANSMISSION_TIMEOUT     (600*  
                                                NX_DHCPV6_TICKS_PER_SECOND)  
NX_DHCPV6_MAX_REBIND_RETRANSMISSION_COUNT       0 

NX_DHCPV6_INIT_RELEASE_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_TIMEOUT    0 
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_COUNT      5  
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_DURATION   0

NX_DHCPV6_INIT_DECLINE_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_TIMEOUT    0
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_COUNT      5  
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_DURATION   0
NX_DHCPV6_FIRST_CONFIRM_MAX_DELAY               (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_INIT_CONFIRM_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_TIMEOUT    (4*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_COUNT      0  
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_DURATION   10

NX_DHCPV6_FIRST_INFORM_MAX_DELAY                (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_INIT_INFORM_TRANSMISSION_TIMEOUT      (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_TIMEOUT     (120*   
                                                NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_COUNT       0 
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_DURATION    0
```

Per nessun limite per un timeout di ritrasmissione, impostare il numero di ritrasmissioni dei messaggi su 0. Per nessun limite al numero di volte in cui un messaggio client DHCPv6 viene ritrasmesso (tentativi), impostare il numero di ritrasmissioni dei messaggi su 0.

> [!NOTE]
> Indipendentemente dalla lunghezza del timeout o dal numero di tentativi, quando un indirizzo IPv6 scade la durata valida, viene rimosso dalla tabella degli indirizzi IP e non può più essere usato dal client. Il client NetX Duo DHCPv6 inizierà automaticamente a inviare messaggi SOLICIT che richiedono un nuovo indirizzo IPv6.