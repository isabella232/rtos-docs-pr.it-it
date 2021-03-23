---
title: Capitolo 5-driver di rete di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione dei driver di rete per Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ede57b7512f4a1a4c30759f428962739aaa2777c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822088"
---
# <a name="chapter-5---azure-rtos-netx-duo-network-drivers"></a>Capitolo 5-driver di rete di Azure RTO NetX Duo

Questo capitolo contiene una descrizione dei driver di rete per Azure RTO NetX Duo. Le informazioni presentate sono progettate per aiutare gli sviluppatori a scrivere driver di rete specifici dell'applicazione per NetX Duo.

## <a name="driver-introduction"></a>Introduzione al driver

La struttura NX_IP contiene tutti gli elementi necessari per la gestione di una singola istanza IP. Sono incluse informazioni generali sul protocollo TCP/IP, nonché la routine di immissione del driver di rete fisica specifico dell'applicazione. La routine di immissione del driver viene definita durante il servizio ***nx_ip_create** _. È possibile aggiungere altri dispositivi all'istanza IP tramite il servizio _ *_nx_ip_interface_attach_**.

La comunicazione tra NetX Duo e il driver di rete dell'applicazione viene eseguita tramite la struttura della richiesta **NX_IP_DRIVER** . Questa struttura viene spesso definita localmente nello stack del chiamante e viene quindi rilasciata dopo la restituzione del driver e della funzione chiamante. La struttura viene definita come indicato di seguito.

```c
typedef struct NX_IP_DRIVER_STRUCT
{
      UINT           nx_ip_driver_command;
      UINT           nx_ip_driver_status;
      ULONG          nx_ip_driver_physical_address_msw;
      ULONG          nx_ip_driver_physical_address_lsw;
      NX_PACKET      *nx_ip_driver_packet;
      ULONG          *nx_ip_driver_return_ptr;
      NX_IP          *nx_ip_driver_ptr;
      NX_INTERFACE   *nx_ip_driver_interface;01
} NX_IP_DRIVER;
```
## <a name="driver-entry"></a>Voce driver 

NetX Duo richiama la funzione di immissione del driver di rete per l'inizializzazione dei driver e per l'invio di pacchetti e per varie operazioni di controllo e stato, inclusa l'inizializzazione e l'abilitazione del dispositivo di rete. NetX Duo invia comandi al driver di rete impostando il campo ***nx_ip_driver_command** _ nella struttura della richiesta _ *NX_IP_DRIVER**. La funzione entry driver ha il formato seguente:

```c
VOID my_driver_entry(NX_IP_DRIVER *request);
```
## <a name="driver-requests"></a>Richieste driver

NetX duo crea la richiesta di driver con un comando specifico e richiama la funzione di immissione del driver per eseguire il comando. Poiché ogni driver di rete ha una singola funzione entry, NetX duo esegue tutte le richieste attraverso la struttura dei dati della richiesta del driver. Il membro ***nx_ip_driver_command** _ della struttura dei dati della richiesta del driver (_* NX_IP_DRIVER * *) definisce la richiesta. Le informazioni sullo stato vengono restituite al chiamante nel membro **_nx_ip_driver_status_*_. Se questo campo è _ * NX_SUCCESS * *, la richiesta del driver è stata completata correttamente.

NetX Duo serializza tutti gli accessi al driver. Pertanto, il driver non deve gestire più thread in modo asincrono chiamando la funzione entry. Si noti che la funzione driver di dispositivo viene eseguita con il mutex IP bloccato. Pertanto la funzione interna del driver di dispositivo non verrà bloccata.

In genere, il driver di dispositivo gestisce anche gli interrupt. Pertanto, tutte le funzioni del driver devono essere interrotte.

### <a name="driver-initialization"></a>Inizializzazione driver   
Sebbene l'elaborazione effettiva dell'inizializzazione dei driver sia specifica dell'applicazione, in genere è costituita dalla struttura dei dati e dall'inizializzazione dell'hardware fisico. Le informazioni richieste da NetX Duo per l'inizializzazione dei driver sono l'unità di trasmissione massima (MTU) IP, ovvero il numero di byte disponibili per il payload del livello IP, inclusa l'intestazione IPv4 o IPv6, e se l'interfaccia fisica necessita di un mapping logico a fisico. Il driver configura il valore MTU dell'interfaccia chiamando ***nx_ip_interface_mtu_set***.

Il driver di dispositivo deve chiamare ***nx_ip_interface_address_mapping_configure** _ per informare NETX Duo se è necessario o meno il mapping degli indirizzi di interfaccia. Se è necessario il mapping degli indirizzi, il driver è responsabile della configurazione dell'interfaccia con un indirizzo MAC valido e fornisce l'indirizzo MAC a NetX tramite _ *_nx_ip_interface_physical_address_set_* *.

Quando il driver di rete riceve la richiesta di INIZIALIZZAzione NX_LINK da NetX Duo, riceve un puntatore al blocco di controllo IP come parte del blocco di controllo delle richieste NX_IP_DRIVER illustrato in precedenza.

Dopo che l'applicazione chiama ***nx_ip_create***, il thread helper IP invia una richiesta di driver con il set di comandi per NX_LINK_INITIALIZE al driver per inizializzare l'interfaccia di rete fisica. Per la richiesta Initialize vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER | Significato    |
| ------------------------- | ----------------------------- |
| nx_ip_driver_command   | NX_LINK_INITIALIZE    |
| nx_ip_driver_ptr       | Puntatore all'istanza IP. Questo valore deve essere salvato dal driver in modo che la funzione driver possa trovare l'istanza IP su cui operare.    |
| nx_ip_driver_interface | Puntatore alla struttura dell'interfaccia di rete all'interno dell'istanza di IP. Queste informazioni devono essere salvate dal driver. Durante la ricezione di pacchetti, il driver deve utilizzare le informazioni sulla struttura dell'interfaccia quando invia il pacchetto allo stack. È possibile ottenere l'indice di interfaccia (indice del dispositivo) leggendo il membro nx_interface_index all'interno della struttura di dati. |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di inizializzare l'interfaccia specificata nell'istanza IP, verrà restituito uno stato di errore diverso da zero. |


> [!NOTE]  
> *Il driver viene effettivamente chiamato dal thread helper IP creato per l'istanza IP. Pertanto, la routine del driver deve evitare l'esecuzione di operazioni di blocco o il thread helper IP potrebbe bloccarsi, causando ritardi non vincolati per le applicazioni che si basano sul thread IP*.

### <a name="enable-link"></a>Abilita collegamento   
Il thread helper IP Abilita quindi la rete fisica impostando il comando del driver su NX_LINK_ENABLE nella richiesta del driver e inviando la richiesta al driver di rete. Questo errore si verifica poco dopo che il thread helper IP ha completato la richiesta di inizializzazione. L'abilitazione del collegamento può essere semplice quanto impostare il campo *nx_interface_link_up* nell'istanza dell'interfaccia. Ma potrebbe anche comportare la manipolazione dell'hardware fisico. Per la richiesta Enable link vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER       | Significato                      |
| ------------------------- | ---------------------------- |
| nx_ip_driver_command   | NX_LINK_ENABLE   |
| nx_ip_driver_ptr       | Puntatore a istanza IP  |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di abilitare l'interfaccia specificata, verrà restituito uno stato di errore diverso da zero. |

### <a name="disable-link"></a>Disabilita collegamento   
Questa richiesta viene effettuata da NetX duo durante l'eliminazione di un'istanza IP dal servizio ***nx_ip_delete** _. In alternativa, un'applicazione può emettere questo comando per disabilitare temporaneamente il collegamento per risparmiare energia. Questo servizio Disabilita l'interfaccia di rete fisica nell'istanza IP. L'elaborazione per disabilitare il collegamento può essere semplice quanto la cancellazione del _flag nx_interface_link_up * nell'istanza dell'interfaccia. Ma potrebbe anche comportare la manipolazione dell'hardware fisico. In genere si tratta di un'operazione inversa dell'operazione ***Enable link**_ . Dopo che il collegamento è stato disabilitato, l'operazione richiesta dell'applicazione _ *_Abilita collegamento_** per abilitare l'interfaccia.

Per la richiesta di disabilitazione del collegamento vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER     | Significato                      |
| ------------------------- | ---------------------------- |
| nx_ip_driver_command   | NX_LINK_DISABLE    |
| nx_ip_driver_ptr       | Puntatore a istanza IP   |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia   |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di disabilitare l'interfaccia specificata nell'istanza IP, verrà restituito uno stato di errore diverso da zero. |

### <a name="uninitialize-link"></a>Uninitialize (collegamento)   
Questa richiesta viene effettuata da NetX duo durante l'eliminazione di un'istanza IP dal servizio ***nx_ip_delete** _. Questa richiesta annullata l'inizializzazione dell'interfaccia e rilascia tutte le risorse create durante la fase di inizializzazione. In genere si tratta di un'operazione inversa dell'operazione _ *_Initialize link_**. Quando l'interfaccia è uninitalized, il dispositivo non può essere usato finché l'interfaccia non viene inizializzata nuovamente.

Per la richiesta di disabilitazione del collegamento vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER    | Significato                  |
|------------------------|--------------------------|
| nx_ip_driver_command   | NX_LINK_UNINITIALZE      |
| nx_ip_driver_ptr       | Puntatore a istanza IP   |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di annullare l'inizializzazione dell'interfaccia specificata nell'istanza IP, verrà restituito uno stato di errore diverso da zero. |

### <a name="packet-send"></a>Invio pacchetti   
Questa richiesta viene eseguita durante l'elaborazione di trasmissione IPv4 o IPv6 interna, che tutti i protocolli NetX Duo utilizzano per trasmettere i pacchetti (ad eccezione di ARP, RARP). Alla ricezione del comando di invio di pacchetti, il *nx_packet_prepend_ptr* punta all'inizio del pacchetto da inviare, ovvero l'inizio dell'intestazione IPv4 o IPv6. *nx_packet_length* indica le dimensioni totali (in byte) dei dati da trasmettere. Se *nx_packet_next* è valido, il datagramma IP in uscita viene archiviato in più pacchetti, il driver è necessario per seguire il pacchetto concatenato e trasmettere l'intero frame. Si noti che l'area dati valida in ogni pacchetto concatenato viene archiviata tra *nx_packet_prepend_ptr* e *nx_packet_append_ptr*.

Il driver è responsabile della costruzione di un'intestazione fisica. Se è necessario un indirizzo fisico per il mapping degli indirizzi IP (ad esempio Ethernet), il livello IP ha già risolto l'indirizzo MAC. L'indirizzo MAC di destinazione viene passato dall'istanza IP, archiviato in *nx_ip_driver_physical_address_msw e nx_ip_driver_physical_address_lsw*.

Dopo l'aggiunta dell'intestazione fisica, l'elaborazione di trasmissione dei pacchetti chiama quindi la funzione di output del driver per trasmettere il pacchetto.

Per la richiesta di invio del pacchetto vengono usati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER              | Significato                               |
| -----------------------------------| --------------------------------------|
| nx_ip_driver_command            | NX_LINK_PACKET_SEND                |
| nx_ip_driver_ptr                | Puntatore a istanza IP                |
| nx_ip_driver_packet             | Puntatore al pacchetto da inviare         |
| nx_ip_driver_interface          | Puntatore all'istanza dell'interfaccia.    |
| nx_ip_driver_physical_address_msw | Più significativi 32 bit di indirizzo fisico (solo se è necessario il mapping fisico) |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo fisico (solo se è necessario il mapping fisico) |
| nx_ip_driver_status             | Stato di completamento. Se il driver non è in grado di inviare il pacchetto, verrà restituito uno stato di errore diverso da zero. |

### <a name="packet-broadcastipv4-packets-only"></a>Trasmissione pacchetti (solo pacchetti IPv4)  
Questa richiesta è quasi identica alla richiesta di invio del pacchetto. L'unica differenza è che i campi indirizzo fisico di destinazione sono impostati sull'indirizzo MAC broadcast Ethernet. Per la richiesta di trasmissione pacchetti vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER                | Significato                                                                                                  |
|------------------------------------|----------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_PACKET_BROADCAST                                                                                 |
| nx_ip_driver_ptr                   | Puntatore a istanza IP                                                                                   |
| nx_ip_driver_packet                | Puntatore al pacchetto da inviare                                                                            |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (broadcast)                                                                                   |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (broadcast)                                                                                   |
| nx_ip_driver_interface             | Puntatore all'istanza dell'interfaccia.                                                                       |
| nx_ip_driver_status                | Stato di completamento. Se il driver non è in grado di inviare il pacchetto, verrà restituito uno stato di errore diverso da zero. |

### <a name="arp-send"></a>Invio ARP  
Questa richiesta è simile anche alla richiesta di invio di pacchetti IP. L'unica differenza è che l'intestazione Ethernet specifica un pacchetto ARP anziché un pacchetto IP e i campi dell'indirizzo fisico di destinazione sono impostati su indirizzo di trasmissione MAC. Per la richiesta di invio ARP vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER                | Significato                                                                                                      |
|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_ARP_SEND                                                                                             |
| nx_ip_driver_ptr                   | Puntatore a istanza IP                                                                                       |
| nx_ip_driver_packet                | Puntatore al pacchetto da inviare                                                                                |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (broadcast)                                                                                       |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (broadcast)                                                                                       |
| nx_ip_driver_interface             | Puntatore all'istanza dell'interfaccia.                                                                           |
| nx_ip_driver_status                | Stato di completamento. Se il driver non è in grado di inviare il pacchetto ARP, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Se il mapping fisico non è necessario, l'implementazione della richiesta non è obbligatoria*.

*Sebbene ARP sia stato sostituito con il protocollo di individuazione Neighbor e il protocollo di individuazione router in IPv6, i driver di rete Ethernet devono comunque essere compatibili con i peer e i router IPv4. Pertanto, i driver devono comunque gestire i pacchetti ARP*.

### <a name="arp-response-send"></a>Invio risposta ARP  
Questa richiesta è quasi identica alla richiesta di invio di pacchetti ARP. L'unica differenza è che i campi dell'indirizzo fisico di destinazione vengono passati dall'istanza IP. Per la richiesta di invio risposta ARP vengono usati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER                  | Significato                                  |
| -------------------------------------- | -----------------------------------------|
| nx_ip_driver_command                | NX_LINK_ARP_RESPONSE_SEND            |
| nx_ip_driver_ptr                    | Puntatore a istanza IP   |
| nx_ip_driver_packet                 | Puntatore al pacchetto da inviare          |
| nx_ip_driver_physical_address_msw | Più significativi 32 bit di indirizzo fisico |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo fisico |
| nx_ip_driver_interface              | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status                 | Stato di completamento. Se il driver non è in grado di inviare il pacchetto ARP, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Se il mapping fisico non è necessario, l'implementazione della richiesta non è obbligatoria*.

### <a name="rarp-send"></a>Invio di RARP   
Questa richiesta è quasi identica alla richiesta di invio di pacchetti ARP. Le uniche differenze sono il tipo di intestazione del pacchetto e i campi dell'indirizzo fisico non sono necessari perché la destinazione fisica è sempre un indirizzo di broadcast.

Per la richiesta di invio RARP vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER                | Significato                                                                                                       |
|------------------------------------|---------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_RARP_SEND                                                                                             |
| nx_ip_driver_ptr                   | Puntatore a istanza IP                                                                                        |
| nx_ip_driver_packet                | Puntatore al pacchetto da inviare                                                                                 |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (broadcast)                                                                                        |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (broadcast)                                                                                        |
| nx_ip_driver_interface             | Puntatore all'istanza dell'interfaccia.                                                                            |
| nx_ip_driver_status                | Stato di completamento. Se il driver non è in grado di inviare il pacchetto RARP, viene restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Le applicazioni che richiedono il servizio RARP devono implementare questo comando*.

### <a name="multicast-group-join"></a>Join gruppo multicast   
Questa richiesta viene effettuata con il servizio ***nx_igmp_multicast_interface join** _ e _*_Nx_ipv4_multicast_interface_join_*_ nel servizio IPv4, _ *_nxd_ipv6_multicast_interface_join_** in IPv6 e varie operazioni richieste da IPv6. Il driver di rete accetta l'indirizzo del gruppo multicast fornito e configura il supporto fisico per accettare i pacchetti in ingresso da tale indirizzo del gruppo multicast. Si noti che per i driver che non supportano il filtro multicast, la logica di ricezione del driver potrebbe essere in modalità promiscua. In questo caso, è possibile che il driver debba filtrare i frame in ingresso in base all'indirizzo MAC di destinazione, riducendo così la quantità di traffico passato nell'istanza IP. Per la richiesta di join del gruppo multicast vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER                  | Significato                                 |
| -------------------------------------- | --------------------------------------- |
| nx_ip_driver_command                | NX_LINK_MULTICAST_JOIN               |
| nx_ip_driver_ptr                    | Puntatore a istanza IP  |
| nx_ip_driver_physical_address_msw | Più significativi 32 bit di indirizzo multicast fisico |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo multicast fisico |
| nx_ip_driver_interface              | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status                 | Stato di completamento. Se il driver non è in grado di partecipare al gruppo multicast, verrà restituito uno stato di errore diverso da zero. |

> [!NOTE]  
> Per le *applicazioni IPv6 è necessario implementare il multicast nel driver per i protocolli basati su ICMPv6, ad esempio la configurazione degli indirizzi. Tuttavia, per le applicazioni IPv4, l'implementazione di questa richiesta non è necessaria se non sono necessarie funzionalità multicast*.

> [!IMPORTANT]  
> *Se IPv6 non è abilitato e le funzionalità multicast non sono richieste da IPv4, l'implementazione della richiesta non è obbligatoria*.

### <a name="multicast-group-leave"></a>Uscita gruppo multicast  
Questa richiesta viene richiamata chiamando in modo esplicito i servizi ***nx_igmp_multicast_interface_leave** _ o _*_Nx_ipv4_multicast_interface_leave_*_ nel servizio IPv4, _ *_nxd_ipv6_multicast_interface_leave_** in IPv6 o da varie operazioni NETX Duo interne necessarie per IPv6. Il driver rimuove l'indirizzo multicast Ethernet fornito dall'elenco multicast. Dopo che un host ha lasciato un gruppo multicast, i pacchetti in rete con questo indirizzo multicast Ethernet non vengono più ricevuti da questa istanza di IP. Per la richiesta di uscita del gruppo multicast vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER              | Significato                              |
| -----------------------------------| -------------------------------------|
| nx_ip_driver_command            | NX_LINK_MULTICAST_LEAVE           |
| nx_ip_driver_ptr                | Puntatore a istanza IP   |
| nx_ip_driver_physical_address_msw | Più significativi 32 bit di indirizzo multicast fisico |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo multicast fisico |
| nx_ip_driver_interface              | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status                 | Stato di completamento. Se il driver non è in grado di uscire dal gruppo multicast, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Se non sono richieste funzionalità multicast per IPv4 o IPv6, non è necessaria l'implementazione di questa richiesta*.

### <a name="attach-interface"></a>Connetti interfaccia  
Questa richiesta viene richiamata da NetX Duo al driver di dispositivo, consentendo al driver di associare l'istanza di driver all'istanza IP corrispondente e all'istanza dell'interfaccia fisica all'interno dell'IP. Per la richiesta di interfaccia di associazione vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER    | Significato                  |
|------------------------|--------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_ATTACH |
| nx_ip_driver_ptr       | Puntatore a istanza IP   |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia.|
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di scollegare l'interfaccia specificata per l'istanza IP, verrà restituito uno stato di errore diverso da zero. |

### <a name="detach-interface"></a>Scollega interfaccia    
Questa richiesta viene richiamata da NetX Duo al driver di dispositivo, consentendo al driver di annullare l'associazione dell'istanza del driver con l'istanza IP corrispondente e l'istanza dell'interfaccia fisica all'interno dell'IP. Per la richiesta di interfaccia di associazione vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER    | Significato                                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_DETACH                                                                                                                   |
| nx_ip_driver_ptr       | Puntatore a istanza IP                                                                                                                     |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia.                                                                                                         |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di collegare l'interfaccia specificata all'istanza IP, verrà restituito uno stato di errore diverso da zero. |

### <a name="get-link-status"></a>Ottenere lo stato del collegamento    
L'applicazione può eseguire una query sullo stato del collegamento dell'interfaccia di rete tramite il servizio NetX Duo Service ***nx_ip_interface_status_check*** per qualsiasi interfaccia nell'host. Per ulteriori informazioni su questi servizi, vedere il capitolo 4 "Descrizione dei servizi NetX Duo" nella pagina 149.

Lo stato del collegamento è contenuto nel campo *nx_interface_link_up* della struttura NX_INTERFACE a cui punta *nx_ip_driver_interface* puntatore. Per la richiesta di stato del collegamento vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER       | Significato                  |
| --------------------------- | -------------------------|
| nx_ip_driver_command     | NX_LINK_GET_STATUS    |
| nx_ip_driver_ptr         | Puntatore a istanza IP   |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire lo stato. |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia   |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere lo stato specifico, verrà restituito uno stato di errore diverso da zero. |

> [!NOTE]  
> ***nx_ip_status_check** _ è ancora disponibile per verificare lo stato dell'interfaccia principale. Tuttavia, gli sviluppatori di applicazioni sono invitati a usare il servizio specifico dell'interfaccia: _ *_nx_ip_interface_status_check._**

### <a name="get-link-speed"></a>Ottenere la velocità del collegamento  
Questa richiesta viene effettuata dall'interno del servizio ***nx_ip_driver_direct_command*** . Il driver archivia la velocità di linea del collegamento nella destinazione specificata. Per la richiesta di velocità della linea di collegamento vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER   | Significato                   |
| ------------------------| ------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_SPEED          |
| nx_ip_driver_ptr         | Puntatore a istanza IP                                                                                         |
| nx_ip_driver_return_ptr | Puntatore alla destinazione in cui posizionare la velocità della riga                                                             |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia                                                                              |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere informazioni sulla velocità, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene utilizzata internamente da NETX Duo, quindi la relativa implementazione è facoltativa*.

### <a name="get-duplex-type"></a>Ottenere il tipo duplex   
Questa richiesta viene effettuata dall'interno del servizio ***nx_ip_driver_direct_command*** . Il driver archivia il tipo duplex del collegamento nella destinazione specificata. Per la richiesta di tipo duplex vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER   | Significato                                                                                                    |
| --------------------------- | -------------------------------------------------------------------------------------------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_DUPLEX_TYPE                                                                                    |
| nx_ip_driver_ptr         | Puntatore a istanza IP                                                                                         |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il tipo duplex                                                            |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia                                                                              |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere informazioni duplex, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene utilizzata internamente da NETX Duo, quindi la relativa implementazione è facoltativa*.

### <a name="get-error-count"></a>Ottenere il conteggio degli errori   
Questa richiesta viene effettuata dall'interno del servizio ***nx_ip_driver_direct_command*** . Il driver archivia il numero di errori del collegamento nella destinazione specificata. Per supportare questa funzionalità, il driver deve tenere traccia degli errori dell'operazione. Per la richiesta di conteggio degli errori di collegamento vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER   | Significato                   |
| --------------------------- | -------------------------------|
| nx_ip_driver_command     | NX_LINK_GET_ERROR_COUNT   |
| nx_ip_driver_ptr         | Puntatore a istanza IP   |
| nx_ip_driver_return_ptr | Puntatore alla destinazione in cui inserire il numero di errori |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia|
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere il conteggio degli errori, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]
> *Questa richiesta non viene utilizzata internamente da NETX Duo, quindi la relativa implementazione è facoltativa*.

### <a name="get-receive-packet-count"></a>Ottenere il numero di pacchetti di ricezione    
Questa richiesta viene effettuata dall'interno del servizio ***nx_ip_driver_direct_command*** . Il driver archivia il numero di pacchetti di ricezione del collegamento nella destinazione specificata. Per supportare questa funzionalità, il driver deve tenere traccia del numero di pacchetti ricevuti. I membri NX_IP_DRIVER seguenti vengono utilizzati per la richiesta di conteggio dei pacchetti di ricezione dei collegamenti.

| &nbsp;Membro NX_IP_DRIVER       | Significato                        |
| --------------------------- | -------------------------------|
| nx_ip_driver_command     | NX_LINK_GET_RX_COUNT      |
| nx_ip_driver_ptr         | Puntatore a istanza IP  |
| nx_ip_driver_return_ptr | Puntatore alla destinazione in cui inserire il numero di pacchetti di ricezione   |
| nx_ip_driver_interface   | Puntatore all'interfaccia di rete fisica  |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere il conteggio delle ricevute, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene utilizzata internamente da NETX Duo, quindi la relativa implementazione è facoltativa*.

### <a name="get-transmit-packet-count"></a>Ottenere il numero di pacchetti di trasmissione   
Questa richiesta viene effettuata dall'interno del servizio ***nx_ip_driver_direct_command*** . Il driver archivia il numero di pacchetti di trasmissione del collegamento nella destinazione specificata. Per supportare questa funzionalità, il driver deve tenere traccia di ogni pacchetto trasmesso in ogni interfaccia. Per la richiesta di conteggio dei pacchetti di trasmissione dei collegamenti vengono usati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER   | Significato                   |
| ----------------------- | ------------------------- |
| nx_ip_driver_command | NX_LINK_GET_TX_COUNT  |
| nx_ip_driver_ptr     | Puntatore a istanza IP    |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il numero di pacchetti di trasmissione  |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia   |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere il conteggio di trasmissione, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene utilizzata internamente da NETX Duo, quindi la relativa implementazione è facoltativa*.

### <a name="get-allocation-errors"></a>Ottenere errori di allocazione   
Questa richiesta viene effettuata dall'interno del servizio ***nx_ip_driver_direct_command*** . Il driver archivia il numero di errori di allocazione del pool di pacchetti nella destinazione specificata. Per la richiesta di conteggio degli errori di allocazione dei collegamenti vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER       | Significato                       |
| --------------------------- | ----------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_ALLOC_ERRORS  |
| nx_ip_driver_ptr         | Puntatore a istanza IP     |
| nx_ip_driver_return_ptr | Puntatore alla destinazione in cui inserire il numero di errori di allocazione  |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia  |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere errori di allocazione, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene utilizzata internamente da NETX Duo, quindi la relativa implementazione è facoltativa*.

### <a name="driver-deferred-processing"></a>Elaborazione posticipata del driver    
Questa richiesta viene eseguita dal thread helper IP in risposta al driver che chiama la routine _* **nx_ip_driver_deferred_processing**_ da un ISR di trasmissione o ricezione. Questo consente al driver ISR di rinviare l'elaborazione di ricezione e trasmissione del pacchetto al thread helper IP, riducendo così la quantità da elaborare nell'ISR. Il campo _nx_interface_additional_link_info * nella struttura NX_INTERFACE a cui punta *nx_ip_driver_interface* può essere usato dal driver per archiviare le informazioni sull'evento di elaborazione posticipata dal contesto del thread di supporto IP. Per l'evento di elaborazione posticipata vengono utilizzati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER     | Significato                           |
| ------------------------- | --------------------------------- |
| nx_ip_driver_command   | NX_LINK_DEFERRED_PROCESSING    |
| nx_ip_driver_ptr       | Puntatore a istanza IP            |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |

### <a name="set-physical-address"></a>Imposta indirizzo fisico  
Questa richiesta viene effettuata dall'interno del servizio ***nx_ip_interface_physical_address_set** _. Questo servizio consente a un'applicazione di modificare l'indirizzo fisico dell'interfaccia in fase di esecuzione. Alla ricezione di questo comando, il driver è necessario per riconfigurare l'indirizzo hardware dell'interfaccia di rete per l'indirizzo fisico fornito. Poiché l'istanza IP ha già il nuovo indirizzo, non è necessario chiamare il servizio _ *_nx_ip_interface_address_set_** da questo comando.

Per la richiesta di comando utente vengono usati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER      | Significato                      |
| -------------------------- | ---------------------------- |
| nx_ip_driver_command    | NX_LINK_SET_PHYSICAL_ADDRESS  |
| nx_ip_driver_ptr        | Puntatore a istanza IP  |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia   |
| nx_ip_driver_physical_ad dress_msw | Più significativi 32 bit del nuovo indirizzo fisico  |
| nx_ip_driver_physical_ad dress_lsw | Meno significativi 32 bit del nuovo indirizzo fisico  |
| nx_ip_driver_status                  | Stato di completamento. Se il driver non è in grado di riconfigurare l'indirizzo fisico, verrà restituito uno stato di errore diverso da zero. |

### <a name="user-commands"></a>Comandi utente    
Questa richiesta viene effettuata dall'interno del servizio ***nx_ip_driver_direct_command*** . Il driver elabora i comandi utente specifici dell'applicazione. Per la richiesta di comando utente vengono usati i membri NX_IP_DRIVER seguenti.

| &nbsp;Membro NX_IP_DRIVER       | Significato                       |
| --------------------------- | ----------------------------- |
| nx_ip_driver_command     | NX_LINK_USER_COMMAND       |
| nx_ip_driver_ptr         | Puntatore a istanza IP        |
| nx_ip_driver_return_ptr | Definita dall'utente       |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia    |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di eseguire i comandi dell'utente, verrà restituito uno stato di errore diverso da zero. |

> [!IMPORTANT] 
> *Questa richiesta non viene utilizzata internamente da NETX Duo, quindi la relativa implementazione è facoltativa*.

### <a name="unimplemented-commands"></a>Comandi non implementati  
Per i comandi non implementati dal driver di rete il campo stato restituito deve essere impostato su NX_UNHANDLED_COMMAND.

## <a name="driver-capability"></a>Funzionalità driver

Alcune interfacce di rete offrono funzionalità di offload di checksum. I driver di dispositivo possono sfruttare le accelerazioni hardware per liberare tempo della CPU dall'esecuzione di diversi calcoli di checksum.

A seconda del livello di supporto del checksum hardware dall'hardware, il driver di dispositivo deve informare l'istanza IP della funzionalità hardware abilitata. In questo modo, l'istanza IP è in grado di riconoscere la funzionalità hardware e di eseguire l'offload del maggior volume possibile per l'hardware. Il driver deve usare l'API ***nx_ip_interface_capability_set*** per impostare tutte le funzionalità che l'interfaccia fisica è in grado di gestire.

È possibile utilizzare le seguenti funzionalità:

- NX_INTERFACE_CAPABILITY_IPV4_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_IPV4_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_TCP_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_TCP_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_UDP_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_UDP_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_ICMPV4_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_ICMPV4_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_ICMPV6_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_ICMPV6_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_IGMP_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_IGMP_RX_CHECKSUM

Per un calcolo di checksum che può essere eseguito nell'hardware, il driver deve configurare correttamente l'hardware o i descrittori del buffer, in modo che il checksum per un pacchetto in uscita possa essere generato e inserito nell'intestazione dall'hardware. Alla ricezione di un pacchetto, la logica di checksum hardware dovrebbe essere in grado di verificare il valore di checksum. Se il valore di checksum non è corretto, il frame ricevuto deve essere rimosso.

Anche con la capacità di eseguire il calcolo del checksum nell'hardware, l'istanza IP mantiene comunque la funzionalità di checksum. In alcuni scenari, ad esempio un datagramma UDP che passa attraverso la protezione IPsec, il checksum UDP deve essere calcolato nel software prima di passare il frame UDP allo stack. La maggior parte della funzionalità di checksum hardware non supporta il calcolo del checksum per un segmento di dati protetto da IPsec. Per un frame UDP o ICMP che deve essere frammentato, il checksum UDP o ICMP deve essere calcolato nel software. La maggior parte della logica di checksum hardware non gestisce il caso in cui i dati vengono suddivisi in più frame.

## <a name="driver-output"></a>Output driver  

Per tutte le richieste di trasmissione pacchetti precedentemente indicate è necessaria una funzione di output implementata nel driver. La logica di trasmissione specifica è specifica dell'hardware, ma in genere è costituita dal controllo della capacità hardware di inviare il pacchetto immediatamente. Se possibile, il payload del pacchetto (e i payload aggiuntivi nella catena di pacchetti) vengono caricati in uno o più buffer di trasmissione hardware e viene avviata un'operazione di trasmissione. Se il pacchetto non rientra nei buffer di trasmissione disponibili, il pacchetto deve essere accodato e trasmesso quando i buffer di trasmissione diventano disponibili.

La coda di trasmissione consigliata è un elenco collegato singolarmente, con puntatori Head e tail. I nuovi pacchetti vengono aggiunti alla fine della coda, mantenendo il pacchetto più vecchio in primo piano. Il campo *nx_packet_queue_next* viene usato come collegamento successivo nella coda del pacchetto. Il driver definisce i puntatori Head e tail della coda di trasmissione.

> [!CAUTION]  
> *Poiché l'accesso a questa coda viene eseguito dal thread e dalle parti di interrupt del driver, è necessario che la protezione degli interrupt venga posizionata intorno alle modifiche della coda*.

La maggior parte delle implementazioni di hardware fisico genera un interrupt al completamento della trasmissione del pacchetto. Quando il driver riceve tale interrupt, in genere rilascia le risorse associate al pacchetto appena trasmesso. Nel caso in cui la logica di trasmissione legga i dati direttamente dal buffer di NX_PACKET, il driver deve usare il servizio ***nx_packet_transmit_release*** per rilasciare il pacchetto associato all'interruzione di trasmissione completa al pool di pacchetti disponibile. Il driver esamina quindi la coda di trasmissione per i pacchetti aggiuntivi in attesa di essere inviati. Il numero di pacchetti di trasmissione in coda che rientrano nei buffer di trasmissione hardware viene rimosso dalla coda e caricato nei buffer. Questa operazione è seguita dall'avvio di un'altra operazione di invio.

Non appena i dati nel NX_PACKET sono stati spostati nel formato FIFO del trasmettitore (o, nel caso in cui un driver supporti un'operazione di copia zero, i dati in NX_PACKET sono stati trasmessi), il driver deve spostare il *nx_packet_prepend_ptr* all'inizio dell'intestazione IP prima di chiamare ***nx_packet_transmit_release.** _ Ricordarsi di modificare di conseguenza _nx_packet_length * campo. Se un frame IP è costituito da più pacchetti, è necessario rilasciare solo l'intestazione della catena di pacchetti.

## <a name="driver-input"></a>Input driver

Al momento della ricezione di un interrupt del pacchetto ricevuto, il driver di rete recupera il pacchetto dai buffer di ricezione hardware fisico e compila un pacchetto NetX Duo valido. La creazione di un pacchetto NetX Duo valido comporta l'impostazione del campo lunghezza appropriato e il concatenamento di più pacchetti se le dimensioni del pacchetto in entrata sono maggiori di un singolo payload del pacchetto. Una volta compilato correttamente, il *prepend_ptr* viene spostato dopo l'intestazione del livello fisico e il pacchetto di ricezione viene inviato a NETX Duo.

NetX Duo presuppone che le intestazioni IP (IPv4 e IPv6) e ARP siano allineate su un limite **ULONG** . Il driver NetX Duo deve pertanto garantire questo allineamento. Negli ambienti Ethernet questa operazione viene eseguita avviando l'intestazione Ethernet due byte a partire dall'inizio del pacchetto. Quando il *nx_packet_prepend_ptr* viene spostato oltre l'intestazione Ethernet, l'indirizzo IP sottostante (IPv4 e IPv6) o l'intestazione ARP è allineato a 4 byte.

> [!WARNING] 
> *Per le differenze importanti tra le intestazioni Ethernet IPv6 e IPv6, vedere la sezione "intestazioni Ethernet" riportata di seguito*.

In NetX Duo sono disponibili diverse funzioni di pacchetti di ricezione. Se il pacchetto ricevuto è un pacchetto ARP, viene chiamato _* **nx_arp_packet_deferred_receive**_ . Se il pacchetto ricevuto è un pacchetto RARP, viene chiamato _ _*_nx_rarp_packet_deferred_receive_*_ . Sono disponibili diverse opzioni per la gestione dei pacchetti IP in ingresso. Per la gestione più veloce dei pacchetti IP, viene chiamato _ _*_nx_ip_packet_receive_*_ . Questo approccio ha il minor sovraccarico, ma richiede una maggiore elaborazione nel gestore del servizio di interrupt di ricezione (ISR) del driver. Per l'elaborazione ISR minima _ _ *_nx_ip_packet_deferred_receive_** viene chiamato il metodo.

Dopo che il nuovo pacchetto di ricezione è stato compilato correttamente, i buffer di ricezione dell'hardware fisico sono impostati per ricevere più dati. Questa operazione potrebbe richiedere l'allocazione di pacchetti NetX Duo e l'inserimento dell'indirizzo di payload nel buffer di ricezione hardware oppure è sufficiente modificare un'impostazione nel buffer di ricezione hardware. Per ridurre al minimo le possibilità di sovraccarico, è importante che i buffer di ricezione dell'hardware dispongano di buffer disponibili appena possibile dopo la ricezione di un pacchetto.

> [!IMPORTANT] 
> *I buffer di ricezione iniziali vengono impostati durante l'inizializzazione del driver*.

### <a name="deferred-receive-packet-handling"></a>Gestione dei pacchetti di ricezione posticipata  
Il driver può rinviare l'elaborazione dei pacchetti di ricezione al thread helper IP di NetX Duo. Per alcune applicazioni questa operazione può essere necessaria per ridurre al minimo l'elaborazione di ISR e i pacchetti eliminati. 

Per usare la gestione posticipata dei pacchetti, la libreria NetX Duo deve prima essere compilata con ***NX_DRIVER_DEFERRED_PROCESSING** _ defined. Questa operazione aggiunge la logica del pacchetto posticipato al thread helper IP di NetX Duo. Successivamente, alla ricezione di un pacchetto di dati, il driver deve chiamare __nx_ip_packet_deferred_receive ():*

```c
_nx_ip_packet_deferred_receive(ip_ptr, packet_ptr);
```
La funzione receive posticipata inserisce il pacchetto di ricezione rappresentato da *packet_ptr* in un FIFO (elenco collegato) e invia una notifica al thread helper IP. Dopo l'esecuzione, l'helper IP chiama ripetutamente la funzione di gestione posticipata per elaborare ogni pacchetto posticipato. L'elaborazione posticipata del gestore include in genere la rimozione dell'intestazione del livello fisico (in genere Ethernet) del pacchetto e l'invio a una di queste funzioni di ricezione NetX Duo:

- ***_nx_ip_packet_receive***
- ***_nx_arp_packet_deferred_receive***
- ***_nx_rarp_packet_deferred_receive***

## <a name="ethernet-headers"></a>Intestazioni Ethernet 

Una delle differenze più significative tra IPv6 e IPv4 per le intestazioni Ethernet è l'impostazione del tipo di frame. Quando si inviano pacchetti, il driver Ethernet è responsabile dell'impostazione del tipo di frame Ethernet nei pacchetti in uscita. Per i pacchetti IPv6, il tipo di frame deve essere 0x86DD; per i pacchetti IPv4, il tipo di frame dovrebbe essere 0x0800.

Il seguente segmento di codice illustra questo processo:

```c
NX_PACKET *packet_ptr;
packet_ptr = driver_req_ptr -> nx_ip_driver_packet;
if (packet_ptr -> nx_packet_ip_version == NX_IP_VERSION_V4)
{

   /* Set Ethernet frame type to IPv4 /*
   ethernet_frame_ptr -> frame_type = 0x0800;

   /* Swap endian-ness for little endian targets.*/
   NX_CHANGE_USHORT_ENDIAN(ethernet_frame_ptr -> frame_type);
}
else if (packet_ptr -> nx_packet_ip_version == NX_IP_VERSION_V6)
{

   /* Set Ethernet frame type to IPv6. /*
   ethernet_frame_ptr -> frame_type = 0x86DD;

   /* Swap endian-ness for little endian targets.*/
   NX_CHANGE_USHORT_ENDIAN(ethernet_frame_ptr -> frame_type);
}
else
{

   /* Unknown IP version. Free the packet we will not send. */
   nx_packet_transmit_release(packet_ptr);
}
```
Analogamente, per i pacchetti in ingresso, il driver Ethernet deve determinare il tipo di pacchetto dal tipo di frame Ethernet. Deve essere implementato per accettare i tipi di frame IPv6 (0x86DD), IPv4 (0x0800), ARP (0x0806) e RARP (0x8035).

## <a name="example-ram-ethernet-network-driver"></a>Driver di rete Ethernet RAM di esempio

Il sistema di dimostrazione NetX Duo viene fornito con un piccolo driver di rete basato su RAM, definito nel file ***nx_ram_network_driver. c.*** Questo driver presuppone che le istanze IP si trovino nella stessa rete e assegna semplicemente indirizzi hardware virtuali (indirizzi MAC) a ogni istanza del dispositivo appena vengono creati. Questo file fornisce un esempio efficace della struttura di base dei driver di rete fisica NetX Duo. Gli utenti possono sviluppare i propri driver di rete utilizzando il Framework driver presentato in questo esempio.

La funzione entry del driver di rete è ***_nx_ram_network_driver (),** _ che viene passata alla chiamata di creazione dell'istanza IP. Le funzioni di immissione per interfacce di rete aggiuntive possono essere passate nel servizio _nx_ip_interface_attach () *. Una volta avviata l'esecuzione dell'istanza IP, viene richiamata la funzione di immissione driver per inizializzare e abilitare il dispositivo (fare riferimento al case **NX_LINK_INITIALIZE** e **NX_LINK_ENABLE**). Dopo l'emissione del comando di **NX_LINK_ENABLE** , il dispositivo deve essere pronto per la trasmissione e la ricezione di pacchetti. 

L'istanza IP trasmette i pacchetti di rete tramite uno di questi comandi:

|                                 |                                                                |
| ------------------------------- | -------------------------------------------------------------- |
| ***NX_LINK_PACKET_SEND***    | È in corso la trasmissione di un pacchetto IPv4 o IPv6,                   |
| ***NX_LINK_ARP_SEND***       | È in corso la trasmissione di una richiesta ARP o di un pacchetto di risposta ARP,    |
| ***NX_LINK_ARP_RARP_SEND*** | È in corso la trasmissione di una richiesta o di un pacchetto di risposta ARP inverso. |

Durante l'elaborazione di questi comandi, il driver di rete deve anteporre l'intestazione del frame Ethernet appropriata e quindi inviarla all'hardware sottostante per la trasmissione. Durante il processo di trasmissione, il driver di rete dispone della proprietà esclusiva dell'area buffer dei pacchetti. Quindi, una volta che i dati sono stati trasmessi (o dopo che i dati sono stati copiati nel buffer di trasferimento interno del driver), il driver di rete è responsabile del rilascio del buffer di pacchetti spostando prima il puntatore anteposto dopo l'intestazione Ethernet nell'intestazione IP (e modificando di conseguenza la lunghezza del pacchetto), chiamando il servizio ***nx_packet_transmit_release ()*** per rilasciare il pacchetto. Il rilascio del pacchetto dopo la trasmissione dei dati provocherà la perdita di pacchetti.

Il driver di dispositivo di rete è inoltre responsabile della gestione dei pacchetti di dati in ingresso. Nell'esempio di driver RAM il pacchetto ricevuto viene elaborato dalla funzione ***_nx_ram_network_driver_receive ()***. Quando il dispositivo riceve un frame Ethernet, il driver è responsabile dell'archiviazione dei dati nella struttura NX_PACKET. Si noti che NetX Duo presuppone che l'intestazione IP venga avviata dall'indirizzo allineato a 4 byte. Poiché la lunghezza dell'intestazione Ethernet è 14byte, è necessario che il driver memorizzi l'inizio dell'intestazione Ethernet a un indirizzo allineato a 2 byte per garantire che l'intestazione IP venga avviata a un indirizzo allineato a 4 byte.