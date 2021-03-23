---
title: Capitolo 1-Introduzione ad Azure RTO NetX AutoIP
description: Il protocollo AutoIP NetX di Azure RTO è un protocollo progettato per la configurazione dinamica degli indirizzi IPv4 in una rete locale.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c26b4112814bb586e056246d68c2597d56df6085
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822754"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-autoip"></a>Capitolo 1-Introduzione ad Azure RTO NetX AutoIP
  
Il protocollo AutoIP NetX di Azure RTO è un protocollo progettato per la configurazione dinamica degli indirizzi IPv4 in una rete locale. AutoIP è un protocollo semplice che utilizza le funzionalità ARP per eseguire la relativa funzione di assegnazione automatica degli indirizzi IP. AutoIP alloca gli indirizzi nell'intervallo tra 169.254.1.0 e 169.254.254.255.

## <a name="autoip-requirements"></a>Requisiti di AutoIP

Per funzionare correttamente, il pacchetto NetX AutoIP richiede che sia già stata creata un'istanza IP NetX. Inoltre, è necessario abilitare ARP nella stessa istanza di IP. Il pacchetto AutoIP NetX non ha altri requisiti.

## <a name="autoip-constraints"></a>Vincoli AutoIP 

Il protocollo NetX AutoIP implementa i requisiti dello standard RFC3927. Esistono tuttavia i vincoli seguenti:

1. Se si usa NetX DHCP, è necessario creare il thread DHCP con una priorità più elevata rispetto al thread dell'istanza IP di NetX e al thread AutoIP.
1. NetX AutoIP non fornisce un meccanismo per continuare a utilizzare gli indirizzi IP precedenti.
1. Quando l'indirizzo IP viene modificato, l'applicazione è responsabile della rimozione di tutte le connessioni TCP esistenti e della relativa ridefinizione nel nuovo indirizzo IP.

## <a name="autoip-protocol-implementation"></a>Implementazione del protocollo AutoIP

Il protocollo NetX AutoIP seleziona innanzitutto un indirizzo casuale all'interno dell'intervallo di indirizzi IPv4 AutoIP di 169.254.1.0 tramite 169.254.254.255. In alternativa, l'applicazione può forzare un indirizzo IP iniziale fornendolo alla funzione ***nx_auto_ip_start*** . Questa operazione è utile nelle situazioni in cui un indirizzo AutoIP è stato usato correttamente in un'esecuzione precedente.

Una volta selezionato un indirizzo AutoIP, NetX AutoIP invia una serie di probe ARP per l'indirizzo selezionato. Un probe ARP è costituito da un messaggio di richiesta ARP con l'indirizzo mittente impostato su 0.0.0.0 e l'indirizzo di destinazione impostato sull'indirizzo AutoIP desiderato. Viene inviata una serie di probe ARP (il numero effettivo è determinato dall'NX_AUTO_IP_PROBE_NUM di definizione). Se un altro nodo di rete risponde a questo probe o Invia un probe identico per lo stesso indirizzo, viene selezionato in modo casuale un nuovo indirizzo AutoIP all'interno dell'intervallo di indirizzi IPv4 di AutoIP e l'elaborazione del probe si ripete.

Se NX_AUTO_IP_PROBE_NUM probe vengono inviati senza risposte, NetX AutoIP genera una serie di annunci ARP per l'indirizzo selezionato. Un annuncio ARP è costituito da un messaggio di richiesta ARP con il mittente e l'indirizzo di destinazione nel messaggio ARP impostato sull'indirizzo AutoIP selezionato. Viene inviata una serie di messaggi di annuncio ARP, corrispondenti al NX_AUTO_IP_ANNOUNCE_NUM define. Se un altro nodo di rete risponde a un messaggio di annuncio o Invia un annuncio identico per lo stesso indirizzo, viene selezionato in modo casuale un nuovo indirizzo AutoIP all'interno dell'intervallo di indirizzi IPv4 di AutoIP e l'elaborazione del probe viene riavviata.

Quando il probe e l'annuncio vengono completati senza conflitti rilevati, l'indirizzo AutoIP selezionato viene considerato valido e l'istanza IP associata viene impostata con questo indirizzo.

## <a name="autoip-address-change"></a>Modifica dell'indirizzo AutoIP

Come indicato in precedenza, NetX AutoIP modifica l'indirizzo dell'istanza IP dopo l'elaborazione del probe e dell'annuncio riuscita. Il monitoraggio per questo caso non è particolarmente importante. Tuttavia, è possibile che l'indirizzo AutoIP cambi in futuro. Le possibili cause includono i conflitti di indirizzi AutoIP futuri, nonché la risoluzione degli indirizzi DHCP. Per elaborare correttamente queste situazioni potenziali, l'applicazione deve usare l'API NetX seguente per avvisare l'IT di qualsiasi e tutte le modifiche all'indirizzo IP:

```c
nx_ip_address_change_notify(NX_IP *ip_ptr,
                            VOID (*ip_address_change_notify)(NX_IP *,VOID*),
                            VOID *additional_info);
```

L'elaborazione nella funzione *ip_address_change_notify* fornita deve riavviare il processore AutoIP di NETX o disabilitarla se l'indirizzo IP è stato risolto successivamente da DHCP. Per l'elaborazione di esempio, vedere la sezione di *sistema di esempio di piccole dimensioni* .

## <a name="autoip-rfcs"></a>RFC AutoIP

AutoIP NetX è conforme a RFC3927 e alle RFC correlate.