---
title: Capitolo 5 - Azure RTOS di rete NetX Duo
description: Questo capitolo contiene una descrizione dei driver di rete per Azure RTOS NetX Duo.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d30e14ce1865e2fbce4a6e00cff787c859b32be
ms.sourcegitcommit: 20a136b06a25e31bbde718b4d12a03ddd8db9051
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2021
ms.locfileid: "123552416"
---
# <a name="chapter-5---azure-rtos-netx-duo-network-drivers"></a>Capitolo 5 - Azure RTOS di rete NetX Duo

Questo capitolo contiene una descrizione dei driver di rete per Azure RTOS NetX Duo. Le informazioni presentate sono progettate per consentire agli sviluppatori di scrivere driver di rete specifici dell'applicazione per NetX Duo.

## <a name="driver-introduction"></a>Introduzione al driver

La NX_IP contiene tutti gli elementi per gestire una singola istanza IP. Sono incluse informazioni generali sul protocollo TCP/IP, nonché la routine di immissione del driver di rete fisica specifico dell'applicazione. La routine di immissione del driver viene definita durante il servizio *** nx_ip_create** _. È possibile aggiungere altri dispositivi all'istanza IP tramite il servizio _ *_nx_ip_interface_attach_**.

La comunicazione tra NetX Duo e il driver di rete dell'applicazione viene eseguita tramite la **NX_IP_DRIVER** della richiesta. Questa struttura viene spesso definita in locale nello stack del chiamante e viene quindi rilasciata dopo la restituzione del driver e della funzione chiamante. La struttura è definita come segue.

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

NetX Duo richiama la funzione di ingresso del driver di rete per l'inizializzazione del driver e per l'invio di pacchetti e per varie operazioni di controllo e stato, tra cui l'inizializzazione e l'abilitazione del dispositivo di rete. NetX Duo evade i comandi al driver di rete impostando il campo ***nx_ip_driver_command** _ nella struttura di richiesta _ *NX_IP_DRIVER** . Il formato della funzione di immissione driver è il seguente:

```c
VOID my_driver_entry(NX_IP_DRIVER *request);
```
## <a name="driver-requests"></a>Richieste driver

NetX Duo crea la richiesta del driver con un comando specifico e richiama la funzione di ingresso del driver per eseguire il comando. Poiché ogni driver di rete ha una singola funzione di immissione, NetX Duo effettua tutte le richieste tramite la struttura dei dati delle richieste del driver. ***nx_ip_driver_command** _ membro della struttura dei dati della richiesta del driver (_*NX_IP_DRIVER**) definisce la richiesta. Le informazioni sullo stato vengono segnalate al chiamante nel membro **_nx_ip_driver_status_*_. Se questo campo è _*NX_SUCCESS**, la richiesta del driver è stata completata correttamente.

NetX Duo serializza tutti gli accessi al driver. Pertanto, il driver non deve gestire più thread in modo asincrono chiamando la funzione di ingresso. Si noti che la funzione del driver di dispositivo viene eseguita con il mutex IP bloccato. Pertanto, la funzione interna del driver di dispositivo non deve bloccarsi.

In genere il driver di dispositivo gestisce anche gli interrupt. Pertanto, tutte le funzioni del driver devono essere sicure per gli interrupt.

### <a name="driver-initialization"></a>Inizializzazione del driver   
Anche se l'elaborazione effettiva dell'inizializzazione del driver è specifica dell'applicazione, in genere è costituita dalla struttura dei dati e dall'inizializzazione dell'hardware fisico. Le informazioni richieste da NetX Duo per l'inizializzazione del driver sono l'unità di trasmissione massima IP (MTU), ovvero il numero di byte disponibili per il payload a livello IP, inclusa l'intestazione IPv4 o IPv6, e se l'interfaccia fisica richiede il mapping da logico a fisico. Il driver configura il valore MTU dell'interfaccia chiamando ***nx_ip_interface_mtu_set***.

Il driver di dispositivo deve chiamare ***nx_ip_interface_address_mapping_configure** _ per informare NetX Duo se è necessario o meno il mapping degli indirizzi dell'interfaccia. Se è necessario il mapping degli indirizzi, il driver è responsabile della configurazione dell'interfaccia con un indirizzo MAC valido e di fornire l'indirizzo MAC a NetX _tramite_ _* nx_ip_interface_physical_address_set **.

Quando il driver di rete riceve la richiesta NX_LINK INITIALIZE da NetX Duo, riceve un puntatore al blocco di controllo IP come parte del blocco di controllo della richiesta NX_IP_DRIVER illustrato in precedenza.

Dopo che l'applicazione nx_ip_create ***,*** il thread helper IP invia una richiesta di driver con il comando impostato su NX_LINK_INITIALIZE al driver per inizializzare l'interfaccia di rete fisica. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di inizializzazione.

| NX_IP_DRIVER &nbsp; membro | Significato    |
| ------------------------- | ----------------------------- |
| nx_ip_driver_command   | NX_LINK_INITIALIZE    |
| nx_ip_driver_ptr       | Puntatore all'istanza IP. Questo valore deve essere salvato dal driver in modo che la funzione del driver possa trovare l'istanza IP su cui operare.    |
| nx_ip_driver_interface | Puntatore alla struttura dell'interfaccia di rete all'interno dell'istanza IP. Queste informazioni devono essere salvate dal driver. Al momento della ricezione dei pacchetti, il driver userà le informazioni sulla struttura dell'interfaccia quando invia il pacchetto nello stack. L'indice dell'interfaccia (indice del dispositivo) può essere ottenuto leggendo il membro nx_interface_index all'interno di questa struttura di dati. |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di inizializzare l'interfaccia specificata sull'istanza IP, restituirà uno stato di errore diverso da zero. |


> [!NOTE]  
> *Il driver viene effettivamente chiamato dal thread helper IP creato per l'istanza IP. Pertanto, la routine del driver* deve evitare di eseguire operazioni di blocco o il thread helper IP potrebbe bloccarsi, causando ritardi non associati alle applicazioni che si basano sul thread IP .

### <a name="enable-link"></a>Abilita collegamento   
Successivamente, il thread helper IP abilita la rete fisica impostando il comando del driver su NX_LINK_ENABLE nella richiesta del driver e inviando la richiesta al driver di rete. Questa situazione si verifica poco dopo il completamento della richiesta di inizializzazione da parte del thread helper IP. L'abilitazione del collegamento può essere semplice come *l'impostazione del campo nx_interface_link_up* nell'istanza dell'interfaccia. Ma può anche comportare la manipolazione dell'hardware fisico. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di collegamento di abilitazione.

| NX_IP_DRIVER &nbsp; membro       | Significato                      |
| ------------------------- | ---------------------------- |
| nx_ip_driver_command   | NX_LINK_ENABLE   |
| nx_ip_driver_ptr       | Puntatore all'istanza IP  |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di abilitare l'interfaccia specificata, restituirà uno stato di errore diverso da zero. |

### <a name="disable-link"></a>Disabilita collegamento   
Questa richiesta viene effettuata da NetX Duo durante l'eliminazione di un'istanza IP da parte del servizio *** nx_ip_delete** _. In alternativa, un'applicazione può eseguire questo comando per disabilitare temporaneamente il collegamento per risparmiare energia. Questo servizio disabilita l'interfaccia di rete fisica nell'istanza IP. L'elaborazione per disabilitare il collegamento può essere semplice come cancellare il _flag nx_interface_link_up* nell'istanza dell'interfaccia. Ma può anche comportare la manipolazione dell'hardware fisico. In genere si tratta di un'operazione inversa dell'operazione ***Abilita collegamento.**_ Dopo la disabilitazione del collegamento, l'applicazione richiede l'operazione _ *_Abilita collegamento_** per abilitare l'interfaccia.

I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di disabilitazione del collegamento.

| NX_IP_DRIVER &nbsp; membro     | Significato                      |
| ------------------------- | ---------------------------- |
| nx_ip_driver_command   | NX_LINK_DISABLE    |
| nx_ip_driver_ptr       | Puntatore all'istanza IP   |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia   |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di disabilitare l'interfaccia specificata nell'istanza IP, restituirà uno stato di errore diverso da zero. |

### <a name="uninitialize-link"></a>Annulla inizializzazione collegamento   
Questa richiesta viene effettuata da NetX Duo durante l'eliminazione di un'istanza IP da parte del servizio *** nx_ip_delete** _. Questa richiesta annulla l'inizializzazione dell'interfaccia e rilascia le risorse create durante la fase di inizializzazione. In genere si tratta di un'operazione inversa *_dell'operazione_* _ Initialize Link *. Dopo che l'interfaccia non è stata inizializzata, il dispositivo non può essere usato fino a quando l'interfaccia non viene inizializzata di nuovo.

I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di disabilitazione del collegamento.

| NX_IP_DRIVER &nbsp; membro    | Significato                  |
|------------------------|--------------------------|
| nx_ip_driver_command   | NX_LINK_UNINITIALZE      |
| nx_ip_driver_ptr       | Puntatore all'istanza IP   |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di annullare l'inizializzazione dell'interfaccia specificata per l'istanza IP, restituirà uno stato di errore diverso da zero. |

### <a name="packet-send"></a>Invio di pacchetti   
Questa richiesta viene effettuata durante l'elaborazione interna di invio IPv4 o IPv6, che tutti i protocolli NetX Duo usano per trasmettere pacchetti (ad eccezione di ARP, RARP). Alla ricezione del comando packet send, il *nx_packet_prepend_ptr* punta all'inizio del pacchetto da inviare, ovvero l'inizio dell'intestazione IPv4 o IPv6. *nx_packet_length* indica le dimensioni totali (in byte) dei dati trasmessi. Se *nx_packet_next* è valido, il datagramma IP in uscita viene archiviato in più pacchetti, il driver deve seguire il pacchetto concatenato e trasmettere l'intero frame. Si noti che l'area dati valida in ogni pacchetto concatenato viene archiviata *tra* nx_packet_prepend_ptr e *nx_packet_append_ptr*.

Il driver è responsabile della costruzione dell'intestazione fisica. Se è necessario il mapping dell'indirizzo fisico all'indirizzo IP (ad esempio Ethernet), il livello IP ha già risolto l'indirizzo MAC. L'indirizzo MAC di destinazione viene passato dall'istanza IP, archiviato in *nx_ip_driver_physical_address_msw e nx_ip_driver_physical_address_lsw*.

Dopo aver aggiunto l'intestazione fisica, l'elaborazione dell'invio di pacchetti chiama quindi la funzione di output del driver per trasmettere il pacchetto.

I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di invio di pacchetti.

| NX_IP_DRIVER &nbsp; membro              | Significato                               |
| -----------------------------------| --------------------------------------|
| nx_ip_driver_command            | NX_LINK_PACKET_SEND                |
| nx_ip_driver_ptr                | Puntatore all'istanza IP                |
| nx_ip_driver_packet             | Puntatore al pacchetto da inviare         |
| nx_ip_driver_interface          | Puntatore all'istanza dell'interfaccia.    |
| nx_ip_driver_physical_address_msw | 32 bit più significativi di indirizzo fisico (solo se è necessario il mapping fisico) |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo fisico (solo se è necessario il mapping fisico) |
| nx_ip_driver_status             | Stato di completamento. Se il driver non è in grado di inviare il pacchetto, restituirà uno stato di errore diverso da zero. |

### <a name="packet-broadcastipv4-packets-only"></a>Trasmissione pacchetti (solo pacchetti IPv4)  
Questa richiesta è quasi identica alla richiesta di invio di pacchetti. L'unica differenza è che i campi dell'indirizzo fisico di destinazione sono impostati sull'indirizzo MAC broadcast Ethernet. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di trasmissione di pacchetti.

| NX_IP_DRIVER &nbsp; membro                | Significato                                                                                                  |
|------------------------------------|----------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_PACKET_BROADCAST                                                                                 |
| nx_ip_driver_ptr                   | Puntatore all'istanza IP                                                                                   |
| nx_ip_driver_packet                | Puntatore al pacchetto da inviare                                                                            |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (trasmissione)                                                                                   |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (trasmissione)                                                                                   |
| nx_ip_driver_interface             | Puntatore all'istanza dell'interfaccia.                                                                       |
| nx_ip_driver_status                | Stato di completamento. Se il driver non è in grado di inviare il pacchetto, restituirà uno stato di errore diverso da zero. |

### <a name="arp-send"></a>Invio ARP  
Questa richiesta è simile alla richiesta di invio di pacchetti IP. L'unica differenza è che l'intestazione Ethernet specifica un pacchetto ARP anziché un pacchetto IP e i campi dell'indirizzo fisico di destinazione sono impostati sull'indirizzo di trasmissione MAC. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di invio ARP.

| NX_IP_DRIVER &nbsp; membro                | Significato                                                                                                      |
|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_ARP_SEND                                                                                             |
| nx_ip_driver_ptr                   | Puntatore all'istanza IP                                                                                       |
| nx_ip_driver_packet                | Puntatore al pacchetto da inviare                                                                                |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (trasmissione)                                                                                       |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (trasmissione)                                                                                       |
| nx_ip_driver_interface             | Puntatore all'istanza dell'interfaccia.                                                                           |
| nx_ip_driver_status                | Stato di completamento. Se il driver non è in grado di inviare il pacchetto ARP, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Se il mapping fisico non è necessario, l'implementazione di questa richiesta non è necessaria.*

Anche se ARP è stato sostituito con il protocollo di individuazione router adiacenti e il protocollo di individuazione router in IPv6, i driver di rete Ethernet devono essere ancora compatibili con *i peer e i router IPv4. Pertanto, i driver devono comunque gestire i pacchetti ARP*.

### <a name="arp-response-send"></a>Invio risposta ARP  
Questa richiesta è quasi identica alla richiesta di pacchetto di invio ARP. L'unica differenza è che i campi dell'indirizzo fisico di destinazione vengono passati dall'istanza IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di invio della risposta ARP.

| NX_IP_DRIVER &nbsp; membro                  | Significato                                  |
| -------------------------------------- | -----------------------------------------|
| nx_ip_driver_command                | NX_LINK_ARP_RESPONSE_SEND            |
| nx_ip_driver_ptr                    | Puntatore all'istanza IP   |
| nx_ip_driver_packet                 | Puntatore al pacchetto da inviare          |
| nx_ip_driver_physical_address_msw | 32 bit più significativi di indirizzo fisico |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo fisico |
| nx_ip_driver_interface              | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status                 | Stato di completamento. Se il driver non è in grado di inviare il pacchetto ARP, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Se il mapping fisico non è necessario, l'implementazione di questa richiesta non è necessaria.*

### <a name="rarp-send"></a>RARP Send   
Questa richiesta è quasi identica alla richiesta di pacchetto di invio ARP. Le uniche differenze sono il tipo di intestazione del pacchetto e i campi dell'indirizzo fisico non sono necessari perché la destinazione fisica è sempre un indirizzo broadcast.

I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di invio RARP.

| NX_IP_DRIVER &nbsp; membro                | Significato                                                                                                       |
|------------------------------------|---------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_RARP_SEND                                                                                             |
| nx_ip_driver_ptr                   | Puntatore all'istanza IP                                                                                        |
| nx_ip_driver_packet                | Puntatore al pacchetto da inviare                                                                                 |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (trasmissione)                                                                                        |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (trasmissione)                                                                                        |
| nx_ip_driver_interface             | Puntatore all'istanza dell'interfaccia.                                                                            |
| nx_ip_driver_status                | Stato di completamento. Se il driver non è in grado di inviare il pacchetto RARP, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Le applicazioni che richiedono il servizio RARP devono implementare questo comando*.

### <a name="multicast-group-join"></a>Aggiunta a un gruppo multicast   
Questa richiesta viene effettuata con il servizio ***nx_igmp_multicast_interface join** _ e _*_nx_ipv4_multicast_interface_join_*_ in IPv4, _ *_nxd_ipv6_multicast_interface_join_** in IPv6 e varie operazioni richieste da IPv6. Il driver di rete accetta l'indirizzo del gruppo multicast fornito e configura il supporto fisico per accettare i pacchetti in ingresso dall'indirizzo del gruppo multicast. Si noti che per i driver che non supportano il filtro multicast, la logica di ricezione del driver potrebbe essere in modalità promiscua. In questo caso, il driver potrebbe dover filtrare i frame in ingresso in base all'indirizzo MAC di destinazione, riducendo così la quantità di traffico passato nell'istanza IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di aggiunta a gruppi multicast.

| NX_IP_DRIVER &nbsp; membro                  | Significato                                 |
| -------------------------------------- | --------------------------------------- |
| nx_ip_driver_command                | NX_LINK_MULTICAST_JOIN               |
| nx_ip_driver_ptr                    | Puntatore all'istanza IP  |
| nx_ip_driver_physical_address_msw | 32 bit più significativi di indirizzo multicast fisico |
| nx_ip_driver_physical_address_lsw | Meno significativi a 32 bit di indirizzo multicast fisico |
| nx_ip_driver_interface              | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status                 | Stato di completamento. Se il driver non è in grado di partecipare al gruppo multicast, restituirà uno stato di errore diverso da zero. |

> [!NOTE]  
> Le applicazioni IPv6 richiedono l'implementazione del multicast nel driver per i protocolli basati su *ICMPv6, ad esempio la configurazione degli indirizzi. Tuttavia, per le applicazioni IPv4, l'implementazione* di questa richiesta non è necessaria se non sono necessarie funzionalità multicast.

> [!IMPORTANT]  
> *Se IPv6 non è abilitato e le funzionalità multicast* non sono richieste da IPv4, l'implementazione di questa richiesta non è necessaria.

### <a name="multicast-group-leave"></a>Gruppo multicast leave  
Questa richiesta viene richiamata chiamando in modo esplicito i servizi ***nx_igmp_multicast_interface_leave** _ _*_o nx_ipv4_multicast_interface_leave_*_ in IPv4, _ *_nxd_ipv6_multicast_interface_leave_** in IPv6 o da varie operazioni interne di NetX Duo necessarie per IPv6. Il driver rimuove l'indirizzo multicast Ethernet fornito dall'elenco multicast. Dopo che un host ha lasciato un gruppo multicast, i pacchetti in rete con questo indirizzo multicast Ethernet non vengono più ricevuti da questa istanza IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di lasciare il gruppo multicast.

| NX_IP_DRIVER &nbsp; membro              | Significato                              |
| -----------------------------------| -------------------------------------|
| nx_ip_driver_command            | NX_LINK_MULTICAST_LEAVE           |
| nx_ip_driver_ptr                | Puntatore all'istanza IP   |
| nx_ip_driver_physical_address_msw | 32 bit più significativi di indirizzo multicast fisico |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo multicast fisico |
| nx_ip_driver_interface              | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status                 | Stato di completamento. Se il driver non è in grado di uscire dal gruppo multicast, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Se le funzionalità multicast non sono richieste da IPv4 o IPv6, l'implementazione* di questa richiesta non è necessaria.

### <a name="attach-interface"></a>Interfaccia di collegamento  
Questa richiesta viene richiamata da NetX Duo al driver di dispositivo, consentendo al driver di associare l'istanza del driver all'istanza IP corrispondente e all'istanza dell'interfaccia fisica all'interno dell'INDIRIZZO IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di interfaccia di collegamento.

| NX_IP_DRIVER &nbsp; membro    | Significato                  |
|------------------------|--------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_ATTACH |
| nx_ip_driver_ptr       | Puntatore all'istanza IP   |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia.|
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di scollegare l'interfaccia specificata nell'istanza IP, restituirà uno stato di errore diverso da zero. |

### <a name="detach-interface"></a>Scollegare l'interfaccia    
Questa richiesta viene richiamata da NetX Duo al driver di dispositivo, consentendo al driver di dissociare l'istanza del driver con l'istanza IP corrispondente e l'istanza dell'interfaccia fisica all'interno dell'indirizzo IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di interfaccia di collegamento.

| NX_IP_DRIVER &nbsp; membro    | Significato                                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_DETACH                                                                                                                   |
| nx_ip_driver_ptr       | Puntatore all'istanza IP                                                                                                                     |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia.                                                                                                         |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di collegare l'interfaccia specificata all'istanza IP, restituirà uno stato di errore diverso da zero. |

### <a name="get-link-status"></a>Ottenere lo stato del collegamento    
L'applicazione può eseguire query sullo stato del collegamento all'interfaccia di rete usando il servizio NetX Duo ***nx_ip_interface_status_check*** per qualsiasi interfaccia nell'host. Per altri dettagli su questi servizi, vedere il capitolo 4 "Descrizione di NetX Duo Services" a pagina 149.

Lo stato del collegamento è contenuto nel *campo nx_interface_link_up* nella struttura NX_INTERFACE a cui punta nx_ip_driver_interface *puntatore.* I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di stato del collegamento.

| NX_IP_DRIVER &nbsp; membro       | Significato                  |
| --------------------------- | -------------------------|
| nx_ip_driver_command     | NX_LINK_GET_STATUS    |
| nx_ip_driver_ptr         | Puntatore all'istanza IP   |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per posizionare lo stato. |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia   |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere uno stato specifico, restituirà uno stato di errore diverso da zero. |

> [!NOTE]  
> ***nx_ip_status_check** _ è ancora disponibile per controllare lo stato dell'interfaccia primaria. Tuttavia, gli sviluppatori di applicazioni sono invitati a usare il servizio specifico dell'interfaccia: _ *_nx_ip_interface_status_check._**

### <a name="get-link-speed"></a>Ottenere la velocità di collegamento  
Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia la velocità della linea del collegamento nella destinazione fornita. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di velocità della linea di collegamento.

| NX_IP_DRIVER &nbsp; membro   | Significato                   |
| ------------------------| ------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_SPEED          |
| nx_ip_driver_ptr         | Puntatore all'istanza IP                                                                                         |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per posizionare la velocità della linea                                                             |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia                                                                              |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere informazioni sulla velocità, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene usata internamente da NetX Duo, quindi la relativa implementazione è facoltativa.*

### <a name="get-duplex-type"></a>Ottenere il tipo duplex   
Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il tipo duplex del collegamento nella destinazione fornita. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di tipo duplex.

| NX_IP_DRIVER &nbsp; membro   | Significato                                                                                                    |
| --------------------------- | -------------------------------------------------------------------------------------------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_DUPLEX_TYPE                                                                                    |
| nx_ip_driver_ptr         | Puntatore all'istanza IP                                                                                         |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per posizionare il tipo duplex                                                            |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia                                                                              |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere informazioni duplex, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene usata internamente da NetX Duo, quindi la relativa implementazione è facoltativa.*

### <a name="get-error-count"></a>Ottenere il conteggio degli errori   
Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il numero di errori del collegamento nella destinazione fornita. Per supportare questa funzionalità, il driver deve tenere traccia degli errori dell'operazione. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di conteggio degli errori di collegamento.

| NX_IP_DRIVER &nbsp; membro   | Significato                   |
| --------------------------- | -------------------------------|
| nx_ip_driver_command     | NX_LINK_GET_ERROR_COUNT   |
| nx_ip_driver_ptr         | Puntatore all'istanza IP   |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il conteggio degli errori |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia|
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere il numero di errori, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]
> *Questa richiesta non viene usata internamente da NetX Duo, quindi la relativa implementazione è facoltativa.*

### <a name="get-receive-packet-count"></a>Ottenere il numero di pacchetti di ricezione    
Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il numero di pacchetti di ricezione del collegamento nella destinazione fornita. Per supportare questa funzionalità, il driver deve tenere traccia del numero di pacchetti ricevuti. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di conteggio pacchetti di ricezione del collegamento.

| NX_IP_DRIVER &nbsp; membro       | Significato                        |
| --------------------------- | -------------------------------|
| nx_ip_driver_command     | NX_LINK_GET_RX_COUNT      |
| nx_ip_driver_ptr         | Puntatore all'istanza IP  |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il numero di pacchetti di ricezione   |
| nx_ip_driver_interface   | Puntatore all'interfaccia di rete fisica  |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere il numero di ricezione, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene usata internamente da NetX Duo, quindi la relativa implementazione è facoltativa.*

### <a name="get-transmit-packet-count"></a>Ottenere il numero di pacchetti di trasmissione   
Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il numero di pacchetti di trasmissione del collegamento nella destinazione fornita. Per supportare questa funzionalità, il driver deve tenere traccia di ogni pacchetto trasmesso su ogni interfaccia. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di conteggio pacchetti di trasmissione del collegamento.

| NX_IP_DRIVER &nbsp; membro   | Significato                   |
| ----------------------- | ------------------------- |
| nx_ip_driver_command | NX_LINK_GET_TX_COUNT  |
| nx_ip_driver_ptr     | Puntatore all'istanza IP    |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il numero di pacchetti di trasmissione  |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia   |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere il numero di trasmissioni, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene usata internamente da NetX Duo, quindi la relativa implementazione è facoltativa.*

### <a name="get-allocation-errors"></a>Ottenere gli errori di allocazione   
Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il conteggio degli errori di allocazione del pool di pacchetti del collegamento nella destinazione fornita. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di conteggio degli errori di allocazione dei collegamenti.

| NX_IP_DRIVER &nbsp; membro       | Significato                       |
| --------------------------- | ----------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_ALLOC_ERRORS  |
| nx_ip_driver_ptr         | Puntatore all'istanza IP     |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il conteggio degli errori di allocazione  |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia  |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di ottenere errori di allocazione, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT]  
> *Questa richiesta non viene usata internamente da NetX Duo, quindi la relativa implementazione è facoltativa.*

### <a name="driver-deferred-processing"></a>Elaborazione posticipata del driver    
Questa richiesta viene effettuata dal thread helper IP in risposta al driver che chiama la _routine *_ nx_ip_driver_deferred_processing da un ISR di trasmissione o ricezione. Ciò consente al driver ISR di rinviare l'elaborazione di ricezione e trasmissione del pacchetto al thread helper IP e quindi ridurre la quantità di elaborazione nell'ISR. Il campo _nx_interface_additional_link_info* nella struttura NX_INTERFACE a cui punta *nx_ip_driver_interface* può essere usato dal driver per archiviare informazioni sull'evento di elaborazione posticipata dal contesto del thread helper IP. I membri NX_IP_DRIVER seguenti vengono usati per l'evento di elaborazione posticipata.

| NX_IP_DRIVER &nbsp; membro     | Significato                           |
| ------------------------- | --------------------------------- |
| nx_ip_driver_command   | NX_LINK_DEFERRED_PROCESSING    |
| nx_ip_driver_ptr       | Puntatore all'istanza IP            |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |

### <a name="set-physical-address"></a>Impostare l'indirizzo fisico  
Questa richiesta viene effettuata dall'interno di ***nx_ip_interface_physical_address_set** _service. Questo servizio consente a un'applicazione di modificare l'indirizzo fisico dell'interfaccia in fase di esecuzione. Quando si riceve questo comando, il driver è necessario per configurare nuovamente l'indirizzo hardware dell'interfaccia di rete per l'indirizzo fisico fornito. Poiché l'istanza IP ha già il nuovo indirizzo, non è necessario chiamare il servizio _ *_nx_ip_interface_address_set_** da questo comando.

I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di comando dell'utente.

| NX_IP_DRIVER &nbsp; membro      | Significato                      |
| -------------------------- | ---------------------------- |
| nx_ip_driver_command    | NX_LINK_SET_PHYSICAL_ADDRESS  |
| nx_ip_driver_ptr        | Puntatore all'istanza IP  |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia   |
| nx_ip_driver_physical_ad dress_msw | 32 bit più significativi del nuovo indirizzo fisico  |
| nx_ip_driver_physical_ad dress_lsw | 32 bit meno significativi del nuovo indirizzo fisico  |
| nx_ip_driver_status                  | Stato di completamento. Se il driver non è in grado di riconfigurare l'indirizzo fisico, restituirà uno stato di errore diverso da zero. |

### <a name="user-commands"></a>Comandi utente    
Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver elabora i comandi utente specifici dell'applicazione. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di comando dell'utente.

| NX_IP_DRIVER &nbsp; membro       | Significato                       |
| --------------------------- | ----------------------------- |
| nx_ip_driver_command     | NX_LINK_USER_COMMAND       |
| nx_ip_driver_ptr         | Puntatore all'istanza IP        |
| nx_ip_driver_return_ptr | Definita dall'utente       |
| nx_ip_driver_interface   | Puntatore all'istanza dell'interfaccia    |
| nx_ip_driver_status      | Stato di completamento. Se il driver non è in grado di eseguire i comandi utente, restituirà uno stato di errore diverso da zero. |

> [!IMPORTANT] 
> *Questa richiesta non viene usata internamente da NetX Duo, quindi la relativa implementazione è facoltativa.*

### <a name="unimplemented-commands"></a>Comandi non implementati  
I comandi non implementati dal driver di rete devono avere il campo stato restituito impostato su NX_UNHANDLED_COMMAND.

## <a name="driver-capability"></a>Funzionalità del driver

Alcune interfacce di rete offrono funzionalità di offload checksum. I driver di dispositivo possono sfruttare le accelerazioni hardware per liberare tempo di CPU dall'esecuzione di vari calcoli di checksum.

A seconda del livello di supporto del checksum hardware dall'hardware, il driver di dispositivo deve informare l'istanza IP della funzionalità hardware abilitata. In questo modo, l'istanza IP è a conoscenza della funzionalità hardware e scarica il maggior numero possibile di calcoli nell'hardware. Il driver deve usare l'API ***nx_ip_interface_capability_set*** impostare tutte le funzionalità che l'interfaccia fisica è in grado di gestire.

È possibile usare le funzionalità seguenti:

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

Per un calcolo del checksum che può essere eseguito nell'hardware, il driver deve configurare correttamente l'hardware o i descrittori del buffer in modo che il checksum per un pacchetto in uscita possa essere generato e inserito nell'intestazione dall'hardware. Alla ricezione di un pacchetto, la logica di checksum hardware deve essere in grado di verificare il valore di checksum. Se il valore di checksum non è corretto, il frame ricevuto deve essere eliminato.

Anche con la possibilità di eseguire il calcolo del checksum nell'hardware, l'istanza IP mantiene comunque la funzionalità di checksum. In alcuni scenari, ad esempio un datagramma UDP che passa attraverso la protezione IPsec, il checksum UDP deve essere calcolato nel software prima di passare il frame UDP nello stack. La maggior parte delle funzionalità di checksum hardware non supporta il calcolo del checksum per un segmento di dati protetto da IPsec. Per un frame UDP o ICMP che deve essere frammentato, il checksum UDP o ICMP deve essere calcolato nel software. La maggior parte della logica di checksum hardware non gestisce il caso in cui i dati vengono suddivisi in più frame.

## <a name="driver-output"></a>Driver Output  

Tutte le richieste di trasmissione di pacchetti menzionate in precedenza richiedono una funzione di output implementata nel driver. La logica di trasmissione specifica è specifica dell'hardware, ma in genere consiste nel controllare la capacità hardware per inviare immediatamente il pacchetto. Se possibile, il payload del pacchetto (e i payload aggiuntivi nella catena di pacchetti) vengono caricati in uno o più buffer di trasmissione hardware e viene avviata un'operazione di trasmissione. Se il pacchetto non rientra nei buffer di trasmissione disponibili, deve essere accodato e trasmesso quando i buffer di trasmissione diventano disponibili.

La coda di trasmissione consigliata è un elenco collegato con puntatori head e tail. I nuovi pacchetti vengono aggiunti alla fine della coda, mantenendo il pacchetto meno recente in primo piano. Il *nx_packet_queue_next* campo viene usato come collegamento successivo del pacchetto nella coda. Il driver definisce i puntatori head e tail della coda di trasmissione.

> [!CAUTION]  
> *Poiché a questa coda si accede da parti* di thread e interrupt del driver, la protezione degli interrupt deve essere posizionata intorno alle modifiche della coda.

La maggior parte delle implementazioni di hardware fisico genera un interrupt al completamento della trasmissione di pacchetti. Quando il driver riceve un interrupt di questo tipo, in genere rilascia le risorse associate al pacchetto appena trasmesso. Se la logica di trasmissione legge i dati direttamente dal buffer NX_PACKET, il driver deve usare il servizio ***nx_packet_transmit_release*** per rilasciare il pacchetto associato all'interrupt completo di trasmissione al pool di pacchetti disponibile. Successivamente, il driver esamina la coda di trasmissione per trovare altri pacchetti in attesa di essere inviati. Poiché molti pacchetti di trasmissione in coda che rientrano nei buffer di trasmissione hardware vengono deaccodati e caricati nei buffer. Questa operazione è seguita dall'avvio di un'altra operazione di invio.

Non appena i dati nel NX_PACKET sono stati spostati nel trasmettitore FIFO (o nel caso in cui un driver supporti l'operazione di copia zero, i dati in NX_PACKET sono stati trasmessi), il driver deve spostare il *nx_packet_prepend_ptr* all'inizio dell'intestazione IP prima di chiamare ***nx_packet_transmit_release.** _ Ricordarsi di regolare _nx_packet_length* campo di conseguenza. Se un frame IP è costituito da più pacchetti, deve essere rilasciata solo la testa della catena di pacchetti.

## <a name="driver-input"></a>Driver Input

Alla ricezione di un interrupt di pacchetto ricevuto, il driver di rete recupera il pacchetto dai buffer di ricezione hardware fisico e compila un pacchetto NetX Duo valido. La creazione di un pacchetto NetX Duo valido comporta la configurazione del campo di lunghezza appropriato e il concatenamento di più pacchetti se le dimensioni del pacchetto in ingresso sono maggiori di un singolo payload di pacchetto. Una volta compilato correttamente, il *prepend_ptr* viene spostato dopo l'intestazione del livello fisico e il pacchetto di ricezione viene inviato a NetX Duo.

NetX Duo presuppone che le intestazioni IP (IPv4 e IPv6) e ARP siano allineate su un **limite ULONG.** Il driver NetX Duo deve pertanto garantire questo allineamento. Negli ambienti Ethernet questa operazione viene eseguita avviando l'intestazione Ethernet a due byte dall'inizio del pacchetto. Quando il *nx_packet_prepend_ptr* viene spostato oltre l'intestazione Ethernet, l'indirizzo IP sottostante (IPv4 e IPv6) o l'intestazione ARP è allineato a 4 byte.

> [!WARNING] 
> *Per importanti differenze tra le intestazioni Ethernet IPv6 e IPv6,* vedere la sezione "Intestazioni Ethernet" più avanti.

In NetX Duo sono disponibili diverse funzioni per i pacchetti di ricezione. Se il pacchetto ricevuto è un pacchetto ARP, nx_arp_packet_deferred_receive viene chiamato . _*_ Se il pacchetto ricevuto è un pacchetto RARP, viene chiamato _ _*_nx_rarp_packet_deferred_receive._*_ Sono disponibili diverse opzioni per la gestione dei pacchetti IP in ingresso. Per la gestione più rapida dei pacchetti IP, viene chiamato _ _*_nx_ip_packet_receive._*_ Questo approccio presenta il minor sovraccarico, ma richiede una maggiore elaborazione nel gestore del servizio di interrupt di ricezione del driver. Per l'elaborazione ISR minima viene *_chiamato __ nx_ip_packet_deferred_receive_** .

Dopo la corretta creazione del nuovo pacchetto di ricezione, i buffer di ricezione dell'hardware fisico vengono configurati per ricevere più dati. Questa operazione potrebbe richiedere l'allocazione di pacchetti NetX Duo e l'inserimento dell'indirizzo del payload nel buffer di ricezione hardware oppure potrebbe semplicemente essere necessario modificare un'impostazione nel buffer di ricezione hardware. Per ridurre al minimo le possibilità di sovraccarico, è importante che i buffer di ricezione dell'hardware abbiano buffer disponibili non appena possibile dopo la ricezione di un pacchetto.

> [!IMPORTANT] 
> *I buffer di ricezione iniziali vengono programmati durante l'inizializzazione del driver*.

### <a name="deferred-receive-packet-handling"></a>Gestione dei pacchetti di ricezione posticipata  
Il driver può rinviare l'elaborazione dei pacchetti al thread helper IP di NetX Duo. Per alcune applicazioni può essere necessario ridurre al minimo l'elaborazione isr e i pacchetti eliminati. 

Per usare la gestione dei pacchetti posticipata, la libreria NetX Duo deve prima essere compilata con ***NX_DRIVER_DEFERRED_PROCESSING** _ definito. In questo modo la logica del pacchetto posticipata viene aggiunta al thread helper IP di NetX Duo. Successivamente, alla ricezione di un pacchetto di dati, il driver deve chiamare __nx_ip_packet_deferred_receive():*

```c
_nx_ip_packet_deferred_receive(ip_ptr, packet_ptr);
```
La funzione di ricezione posticipata inserisce il pacchetto di ricezione rappresentato da *packet_ptr* in un FIFO (elenco collegato) e invia una notifica al thread helper IP. Dopo l'esecuzione, l'helper IP chiama in modo ripetitivo la funzione di gestione posticipata per elaborare ogni pacchetto posticipato. L'elaborazione del gestore posticipata include in genere la rimozione dell'intestazione del livello fisico del pacchetto (in genere Ethernet) e l'invio a una di queste funzioni di ricezione NetX Duo:

- ***_nx_ip_packet_receive***
- ***_nx_arp_packet_deferred_receive***
- ***_nx_rarp_packet_deferred_receive***

## <a name="ethernet-headers"></a>Intestazioni Ethernet 

Una delle differenze più significative tra IPv6 e IPv4 per le intestazioni Ethernet è l'impostazione del tipo di frame. Quando si inviano pacchetti, il driver Ethernet è responsabile dell'impostazione del tipo di frame Ethernet nei pacchetti in uscita. Per i pacchetti IPv6, il tipo di frame deve essere 0x86DD; per i pacchetti IPv4, il tipo di frame deve essere 0x0800.

Il segmento di codice seguente illustra questo processo:

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

## <a name="example-ram-ethernet-network-driver"></a>Driver di rete Ethernet ram di esempio

Il sistema dimostrativo NetX Duo viene fornito con un piccolo driver di rete basato su RAM, definito nel file ***nx_ram_network_driver.c.*** Questo driver presuppone che le istanze IP siano tutte nella stessa rete e semplicemente assegni indirizzi hardware virtuali (indirizzi MAC) a ogni istanza del dispositivo durante la creazione. Questo file fornisce un buon esempio della struttura di base dei driver di rete fisici NetX Duo. Gli utenti possono sviluppare i propri driver di rete usando il framework di driver presentato in questo esempio.

La funzione entry del driver di rete è ***_nx_ram_network_driver()),** _ che viene passato alla chiamata create dell'istanza IP. Le funzioni di immissione per interfacce di rete aggiuntive possono essere passate al servizio _nx_ip_interface_attach()*. Dopo l'avvio dell'esecuzione dell'istanza IP, viene richiamata la funzione  di immissione del driver per inizializzare e abilitare il dispositivo (vedere il case NX_LINK_INITIALIZE **e NX_LINK_ENABLE**). Dopo aver **NX_LINK_ENABLE** comando, il dispositivo deve essere pronto per trasmettere e ricevere pacchetti. 

L'istanza IP trasmette i pacchetti di rete tramite uno dei comandi seguenti:

| Comando                         |  Descrizione                                                   |
| ------------------------------- | -------------------------------------------------------------- |
| ***NX_LINK_PACKET_SEND***    | È in corso la trasmissione di un pacchetto IPv4 o IPv6,                   |
| ***NX_LINK_ARP_SEND***       | È in corso la trasmissione di una richiesta ARP o di un pacchetto di risposta ARP.    |
| ***NX_LINK_ARP_RARP_SEND*** | È in corso la trasmissione di un pacchetto di richiesta o risposta ARP inverso, |

Durante l'elaborazione di questi comandi, il driver di rete deve anteporre l'intestazione del frame Ethernet appropriata e quindi inviarla all'hardware sottostante per la trasmissione. Durante il processo di trasmissione, il driver di rete ha la proprietà esclusiva dell'area del buffer di pacchetti. Pertanto, dopo la trasmissione dei dati (o dopo che i dati sono stati copiati nel buffer di trasferimento interno del driver), il driver di rete è responsabile del rilascio del buffer di pacchetti spostando prima il puntatore anteposto oltre l'intestazione Ethernet nell'intestazione IP (e regolare di conseguenza la lunghezza del pacchetto) e quindi chiamando il ***servizio nx_packet_transmit_release()*** per rilasciare il pacchetto. Il non rilascio del pacchetto dopo la trasmissione dei dati causerà la perdita dei pacchetti.

Il driver di dispositivo di rete è anche responsabile della gestione dei pacchetti di dati in ingresso. Nell'esempio del driver RAM, il pacchetto ricevuto viene elaborato dalla ***funzione _nx_ram_network_driver_receive()***. Quando il dispositivo riceve un frame Ethernet, il driver è responsabile dell'archiviazione dei dati NX_PACKET struttura. Si noti che NetX Duo presuppone che l'intestazione IP inizi da un indirizzo allineato a 4 byte. Poiché la lunghezza dell'intestazione Ethernet è 14byte, il driver deve archiviare l'inizio dell'intestazione Ethernet in un indirizzo allineato a 2 byte per garantire che l'intestazione IP inizi da un indirizzo allineato a 4 byte.

## <a name="tcpip-offload-driver-guidance"></a>Indicazioni sul driver di offload TCP/IP
Per la funzionalità di offload TCP/IP, è necessaria una funzione driver per ogni interfaccia IP. Ecco un elenco di attività aggiuntive per il driver di rete.

* Per il comando `NX_LINK_INITIALIZE` ,
  * Creare un thread del driver per gestire gli eventi di ricezione dell'offload TCP/IP.
* Per il comando `NX_LINK_INTERFACE_ATTACH` ,
  * Impostare la funzionalità di sull'interfaccia del driver. Vedere il codice di esempio seguente.
``` C
driver_req_ptr -> nx_ip_driver_interface -> nx_interface_capability_flag = NX_INTERFACE_CAPABILITY_TCPIP_OFFLOAD;
```
* Per il comando `NX_LINK_ENABLE` ,
  * Avviare il thread del driver.
  * Impostare la funzione di callback TCP/IP su interfaccia del driver. Vedere il codice di esempio seguente.
``` C
driver_req_ptr -> nx_ip_driver_interface -> nx_interface_tcpip_offload_handler = _nx_driver_tcpip_handler;
```
* Per il comando `NX_LINK_DISABLE` ,
  * Arrestare il thread del driver
  * Cancellare la funzione di callback TCP/IP dell'interfaccia del driver.
* Per il comando `NX_LINK_UNINITIALIZE` ,
  * Eliminare il thread del driver

### <a name="tcpip-offload-driver-thread"></a>TCP/IP Offload Driver Thread
Lo scopo del thread del driver è ricevere pacchetti TCP o UDP in ingresso. Nel thread del driver è in genere presente un ciclo while per verificare se è disponibile un pacchetto TCP o UDP in ingresso o se è stata stabilita una connessione. Quando i dati sono disponibili, passare il pacchetto TCP o UDP a NetX Duo. Lo spazio tra `nx_packet_data_start` e deve essere sufficiente per inserire `nx_packet_prepend_ptr` l'intestazione TCP/IP. Per il socket TCP, allocare il pacchetto con tipo `NX_TCP_PACKET` . Per il socket UDP, allocare il pacchetto con tipo `NX_UDP_PACKET` . Compilare i dati in ingresso da `nx_packet_append_ptr` a `nx_packet_data_end` . I dati in `nx_packet_append_ptr` devono contenere solo payload TCP o UDP. L'intestazione TCP/IP **NON** DEVE essere compilata nel pacchetto. Modificare la lunghezza del pacchetto e impostare l'interfaccia di ricezione, quindi chiamare `_nx_tcp_socket_driver_packet_receive` per il pacchetto TCP e per il pacchetto `_nx_udp_socket_driver_packet_receive` UDP. Se una connessione TCP viene arrestato, chiamare `_nx_tcp_socket_driver_packet_receive` con il pacchetto impostato su NULL. Quando viene stabilita la connessione, chiamare `_nx_tcp_socket_driver_establish` .

### <a name="tcpip-offload-driver-handler"></a>Gestore del driver di offload TCP/IP
I comandi del driver seguenti sono necessari per le interfacce di rete con i servizi TCP/IP. 
* Per l'operazione `NX_TCPIP_OFFLOAD_TCP_CLIENT_SOCKET_CONNECT` ,
  * Allocare la risorsa, se necessario.
  * Eseguire il binding alla porta TCP locale e connettersi al server.
  * Restituzione dell'esito positivo alla connessione stabilita. Quando la connessione è in corso, restituire `NX_IN_PROGRESS` . In caso contrario, restituisce un errore.
* Per l'operazione `NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_LISTEN` ,
  * Verificare prima di tutto l'ascolto duplicato. Può essere chiamato più volte sulla stessa porta. Prima volta da `nx_tcp_server_socket_listen` e quindi `nx_tcp_server_socket_relisten` .
  * Allocare la risorsa, se necessario.
  * Restare in ascolto della porta TCP locale.
* Per l'operazione `NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_ACCEPT` ,
  * Allocare la risorsa, se necessario.
  * Accettare la connessione.
* Per l'operazione `NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_UNLISTEN` ,
  * Trovare il socket TCP in ascolto sulla porta locale.
  * Chiudere il socket di ascolto, se trovato.
* Per l'operazione `NX_TCPIP_OFFLOAD_TCP_SOCKET_DISCONNECT` ,
  * Chiudere la connessione di offload TCP/IP.
  * Disassociare la porta TCP locale.
  * Pulire le risorse create durante la connessione.
* Per l'operazione `NX_TCPIP_OFFLOAD_TCP_SOCKET_SEND` ,
  * Inviare dati tramite offload TCP/IP. Prepararsi a gestire una lunghezza del pacchetto maggiore rispetto a MSS o a una situazione di catena di pacchetti.
* Per l'operazione `NX_TCPIP_OFFLOAD_UDP_SOCKET_BIND` ,
  * Allocare la risorsa, se necessario.
  * Eseguire il binding alla porta UDP locale.
* Per l'operazione `NX_TCPIP_OFFLOAD_UDP_SOCKET_UNBIND` ,
  * Disassociare la porta UDP locale.
  * Pulizia delle risorse create durante l'associazione.
* Per l'operazione `NX_TCPIP_OFFLOAD_UDP_SOCKET_SEND` ,
  * Inviare dati tramite offload TCP/IP. Prepararsi a gestire una lunghezza del pacchetto superiore a MTU o a una situazione di catena di pacchetti.