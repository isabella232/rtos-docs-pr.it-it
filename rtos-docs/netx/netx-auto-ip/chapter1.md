---
title: Capitolo 1 - Introduzione a Azure RTOS NetX AutoIP
description: Il Azure RTOS NetX AutoIP Protocol è un protocollo progettato per la configurazione dinamica degli indirizzi IPv4 in una rete locale.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cd41a50a8591426b4c32cf2105132d92bbe487d9f91860d05c65f1a65e6d1d1c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797008"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-autoip"></a>Capitolo 1 - Introduzione a Azure RTOS NetX AutoIP
  
Il Azure RTOS NetX AutoIP Protocol è un protocollo progettato per la configurazione dinamica degli indirizzi IPv4 in una rete locale. AutoIP è un protocollo semplice che usa le funzionalità ARP per eseguire la funzione di assegnazione automatica degli indirizzi IP. AutoIP alloca gli indirizzi nell'intervallo compreso tra 169.254.1.0 e 169.254.254.255.

## <a name="autoip-requirements"></a>Requisiti di AutoIP

Per funzionare correttamente, il pacchetto NetX AutoIP richiede che sia già stata creata un'istanza IP NetX. Inoltre, ARP deve essere abilitato nella stessa istanza IP. Il pacchetto NetX AutoIP non presenta altri requisiti.

## <a name="autoip-constraints"></a>Vincoli AutoIP 

Il protocollo NetX AutoIP implementa i requisiti dello standard RFC3927. Esistono tuttavia i vincoli seguenti:

1. Se si usa NETX DHCP, il thread DHCP deve essere creato con una priorità più alta rispetto sia al thread dell'istanza IP NetX che al thread AutoIP.
1. NetX AutoIP non fornisce un meccanismo per continuare a usare gli indirizzi IP meno usati.
1. Quando l'indirizzo IP cambia, l'applicazione è responsabile dell'rimozione di tutte le connessioni TCP esistenti e della loro ristabilizione nel nuovo indirizzo IP.

## <a name="autoip-protocol-implementation"></a>Implementazione del protocollo AutoIP

Il protocollo NetX AutoIP seleziona innanzitutto un indirizzo casuale nell'intervallo di indirizzi IPv4 AutoIP compreso tra 169.254.1.0 e 169.254.254.255. In alternativa, l'applicazione può forzare un indirizzo IP iniziale fornendolo alla ***nx_auto_ip_start*** funzione. Ciò è utile nelle situazioni in cui un indirizzo AutoIP è stato usato correttamente in un'esecuzione precedente.

Dopo aver selezionato un indirizzo AutoIP, NetX AutoIP invia una serie di probe ARP per l'indirizzo selezionato. Un probe ARP è costituito da un messaggio di richiesta ARP con l'indirizzo del mittente impostato su 0.0.0.0 e l'indirizzo di destinazione impostato sull'indirizzo AutoIP desiderato. Viene inviata una serie di probe ARP (il numero effettivo è determinato dalla definizione NX_AUTO_IP_PROBE_NUM). Se un altro nodo di rete risponde a questo probe o invia un probe identico per lo stesso indirizzo, viene selezionato in modo casuale un nuovo indirizzo AutoIP nell'intervallo di indirizzi IPv4 AutoIP e l'elaborazione del probe si ripete.

Se NX_AUTO_IP_PROBE_NUM probe vengono inviati senza alcuna risposta, NetX AutoIP elava una serie di annunci ARP per l'indirizzo selezionato. Un annuncio ARP è costituito da un messaggio di richiesta ARP con il mittente e l'indirizzo di destinazione nel messaggio ARP impostato sull'indirizzo AutoIP selezionato. Viene inviata una serie di messaggi di annuncio ARP, corrispondenti alla definizione NX_AUTO_IP_ANNOUNCE_NUM. Se un altro nodo di rete risponde a un messaggio di annuncio o invia un annuncio identico per lo stesso indirizzo, un nuovo indirizzo AutoIP viene selezionato in modo casuale nell'intervallo di indirizzi IPv4 AutoIP e l'elaborazione del probe viene avviata.

Quando il probe e l'annuncio vengono completati senza conflitti rilevati, l'indirizzo AutoIP selezionato viene considerato valido e l'istanza IP associata viene impostata con questo indirizzo.

## <a name="autoip-address-change"></a>Modifica dell'indirizzo AutoIP

Come accennato in precedenza, NetX AutoIP modifica l'indirizzo dell'istanza IP dopo l'elaborazione del probe e dell'annuncio. Il monitoraggio per questo caso non è molto importante. Tuttavia, è possibile che l'indirizzo AutoIP cambi in futuro. Le possibili cause includono conflitti di indirizzi AutoIP futuri e la risoluzione degli indirizzi DHCP. Per elaborare correttamente queste potenziali situazioni, l'applicazione deve usare l'API NetX seguente per avvisarla di qualsiasi modifica dell'indirizzo IP:

```c
nx_ip_address_change_notify(NX_IP *ip_ptr,
                            VOID (*ip_address_change_notify)(NX_IP *,VOID*),
                            VOID *additional_info);
```

L'elaborazione nella funzione *ip_address_change_notify* deve riavviare il processore NetX AutoIP o disabilitarla se DHCP ha successivamente risolto l'indirizzo IP. Fare riferimento alla sezione *Small Example System per* l'elaborazione di esempio.

## <a name="autoip-rfcs"></a>RFC AutoIP

NetX AutoIP è conforme a RFC3927 e alle RFC correlate.