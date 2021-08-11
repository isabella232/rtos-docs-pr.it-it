---
title: Capitolo 5 - Azure RTOS di rete NetX
description: Questo capitolo contiene una descrizione dei driver di rete per Azure RTOS NetX.
author: philmea
ms.author: philmea
ms.date: 09/11/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 0770d6beb8b2715a8e5dddf1bdf187c0cd1d5ffd74e7bea9b7ff9bdf1785d088
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801921"
---
# <a name="chapter-5---netx-network-drivers"></a>Capitolo 5 - Driver di rete NetX

Questo capitolo contiene una descrizione dei driver di rete per NetX. Le informazioni presentate sono progettate per aiutare gli sviluppatori a scrivere driver di rete specifici dell'applicazione per Azure RTOS NetX.

## <a name="driver-introduction"></a>Introduzione ai driver

La NX_IP contiene tutti gli elementi per gestire una singola istanza IP. Sono incluse informazioni generali sul protocollo TCP/IP, nonché la routine di ingresso del driver di rete fisica specifico dell'applicazione. La routine di ingresso del driver viene definita durante il ***nx_ip_create*** servizio. È possibile aggiungere altri dispositivi all'istanza IP tramite ***il nx_ip_interface_attach*** servizio.

La comunicazione tra NetX e il driver di rete dell'applicazione viene eseguita tramite la **NX_IP_DRIVER** della richiesta. Questa struttura viene spesso definita in locale nello stack del chiamante e pertanto viene rilasciata dopo la restituzione del driver e della funzione chiamante. La struttura è definita come segue.

```C
typedef struct NX_IP_DRIVER_STRUCT
{
    UINT nx_ip_driver_command;
    UINT nx_ip_driver_status;
    ULONG nx_ip_driver_physical_address_msw;
    ULONG nx_ip_driver_physical_address_lsw;
    NX_PACKET *nx_ip_driver_packet;
    ULONG *nx_ip_driver_return_ptr;
    NX_IP *nx_ip_driver_ptr;
    NX_INTERFACE *nx_ip_driver_interface;
} NX_IP_DRIVER;
```

## <a name="driver-entry"></a>Voce driver

NetX richiama la funzione di immissione del driver di rete per l'inizializzazione del driver e per l'invio di pacchetti e per varie operazioni di controllo e stato, tra cui l'inizializzazione e l'abilitazione del dispositivo di rete. NetX fornisce comandi al driver di rete impostando il campo ***nx_ip_driver_command** _ nella struttura delle richieste _ *NX_IP_DRIVER**. La funzione di ingresso del driver ha il formato seguente:

```C
VOID my_driver_entry(NX_IP_DRIVER *request);
```

## <a name="driver-requests"></a>Richieste driver

NetX crea la richiesta del driver con un comando specifico e richiama la funzione di ingresso del driver per eseguire il comando. Poiché ogni driver di rete ha una singola funzione di immissione, NetX effettua tutte le richieste tramite la struttura dei dati delle richieste del driver. Il ***nx_ip_driver_command*** della struttura dei dati della richiesta del driver (**NX_IP_DRIVER**) definisce la richiesta. Le informazioni sullo stato vengono segnalate al chiamante nel membro ***nx_ip_driver_status***. Se questo campo **è** NX_SUCCESS , la richiesta del driver è stata completata correttamente.

NetX serializza tutti gli accessi al driver. Pertanto, non è necessario che il driver gestirà più thread chiamando in modo asincrono la funzione entry. Si noti che la funzione del driver di dispositivo viene eseguita con il mutex IP bloccato. Pertanto, la funzione interna del driver di dispositivo non deve bloccarsi.

In genere il driver di dispositivo gestisce anche gli interrupt. Pertanto, tutte le funzioni del driver devono essere sicure per gli interrupt.

### <a name="driver-initialization"></a>Inizializzazione del driver

Anche se l'elaborazione effettiva dell'inizializzazione del driver è specifica dell'applicazione, in genere è costituita dalla struttura dei dati e dall'inizializzazione dell'hardware fisico. Le informazioni richieste da NetX per l'inizializzazione del driver sono l'unità massima di trasmissione IP (MTU), ovvero il numero di byte disponibili per il payload a livello IP, inclusa l'intestazione IP, e se l'interfaccia fisica richiede il mapping da logico a fisico. Esigenze del driver

per configurare l'MTU dell'interfaccia impostando il valore in ***nx_interface_ip_mtu_size** _ nella struttura _ *NX_INTERFACE**.

Il driver di dispositivo deve anche configurare il valore in ***nx_ip_interface_address_mapping_needed*** in

**NX_INTERFACE** per informare NetX se è necessario o meno il mapping degli indirizzi dell'interfaccia. Se è necessario il mapping degli indirizzi, il driver è responsabile della configurazione dell'interfaccia con un indirizzo MAC valido e della specifica dell'indirizzo MAC a NetX.

Quando il driver di rete riceve la richiesta NX_LINK INITIALIZE da NetX, riceve un puntatore al blocco di controllo IP come parte del blocco di controllo NX_IP_DRIVER richiesta illustrato in precedenza.

Dopo che ***l'applicazione nx_ip_create***, il thread helper IP invia una richiesta di driver con il comando impostato su NX_LINK_INITIALIZE al driver per inizializzare l'interfaccia di rete fisica. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di inizializzazione.

| NX_IP_DRIVER membro    | Significato |
|------------------------|-----------------------------------------------|
| nx_ip_driver_command   | NX_LINK_INITIALIZE |
| nx_ip_driver_ptr       | Puntatore all'istanza IP. Questo valore deve essere salvato dal driver in modo che la funzione del driver possa trovare l'istanza IP su cui operare. |
| nx_ip_driver_interface | Puntatore alla struttura dell'interfaccia di rete all'interno dell'istanza IP. Queste informazioni devono essere salvate dal driver. Alla ricezione dei pacchetti, il driver userà le informazioni sulla struttura dell'interfaccia durante l'invio del pacchetto nello stack. |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di inizializzare l'interfaccia specificata nell'istanza IP, restituirà uno stato di errore diverso da zero.                                                                                           |


> [!IMPORTANT]
> *La maggior parte dei comandi del driver viene chiamata dal thread helper IP creato per l'istanza IP. Pertanto, la routine del driver deve evitare di eseguire operazioni di blocco o il thread helper IP potrebbe bloccarsi, causando ritardi illimitati per le applicazioni che si basano sul thread IP.*

### <a name="enable-link"></a>Abilita collegamento  

Successivamente, il thread helper IP abilita la rete fisica impostando il comando del driver su NX_LINK_ENABLE nella richiesta del driver e inviando la richiesta al driver di rete. Ciò si verifica poco dopo che il thread helper IP ha completato la richiesta di inizializzazione. L'abilitazione del collegamento può essere semplice quanto l'impostazione nx_interface_link_up campo nell'istanza dell'interfaccia. Ma può anche comportare la manipolazione dell'hardware fisico. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di collegamento di abilitazione.

| NX_IP_DRIVER membro    | Significato |
|------------------------|------------------------------------------|
| nx_ip_driver_command   | NX_LINK_ENABLE                                                                                                          |
| nx_ip_driver_ptr       | Puntatore all'istanza IP                                                                                                  |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia                                                                                       |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di abilitare l'interfaccia specificata, restituirà uno stato di errore diverso da zero. |



### <a name="disable-link"></a>Disabilita collegamento  

Questa richiesta viene effettuata da NetX durante l'eliminazione di un'istanza IP dal servizio ***nx_ip_delete** _. In alternativa, un'applicazione può eseguire questo comando per disabilitare temporaneamente il collegamento per risparmiare energia. Questo servizio disabilita l'interfaccia di rete fisica nell'istanza IP. L'elaborazione per disabilitare il collegamento può essere semplice come cancellare _il flag nx_interface_link_up* nell'istanza dell'interfaccia. Ma può anche comportare la manipolazione dell'hardware fisico. In genere si tratta di un'operazione inversa **dell'operazione** * Abilita_ collegamento. Dopo aver disabilitato il collegamento, l'applicazione richiede l'operazione _ *_Abilita collegamento_** per abilitare l'interfaccia. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di disabilitazione del collegamento.

| NX_IP_DRIVER membro    | Significato |
|------------------------|--------------------------------------|
| nx_ip_driver_command   | NX_LINK_DISABLE |
| nx_ip_driver_ptr       | Puntatore all'istanza IP |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di disabilitare l'interfaccia specificata nell'istanza IP, restituirà uno stato di errore diverso da zero. |


### <a name="uninitialize-link"></a>Annullare l'inizializzazione del collegamento  

Questa richiesta viene effettuata da NetX durante l'eliminazione di un'istanza IP ***da parte nx_ip_delete*** servizio. Questa richiesta annulla l'inizializzazione dell'interfaccia e rilascia tutte le risorse create durante la fase di inizializzazione. In genere si tratta di un'operazione inversa ***dell'operazione Initialize Link.*** Dopo che l'interfaccia non è stata inizializzata, il dispositivo non può essere usato fino a quando l'interfaccia non viene inizializzata nuovamente.

I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di disabilitazione del collegamento.

| NX_IP_DRIVER membro  | Significato                |
|----------------------|------------------------|
| nx_ip_driver_command | NX_LINK_UNINITIALZE    |
| nx_ip_driver_ptr     | Puntatore all'istanza IP |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di annullare l'inizializzazione dell'interfaccia specificata nell'istanza IP, restituirà uno stato di errore diverso da zero. |


### <a name="packet-send"></a>Invio di pacchetti  

Questa richiesta viene effettuata durante l'elaborazione interna dell'invio IP, l'elaborazione, che tutti i protocolli NetX usano per trasmettere pacchetti (ad eccezione di ARP, RARP). Alla ricezione del comando packet send, il *nx_packet_prepend_ptr* punta all'inizio del pacchetto da inviare, ovvero l'inizio dell'intestazione IP.
*nx_packet_length* indica le dimensioni totali (in byte) dei dati trasmessi. Se *nx_packet_next* valido, il datagramma IP in uscita viene archiviato in più pacchetti, il driver deve seguire il pacchetto concatenato e trasmettere l'intero frame. Si noti che l'area dati valida in ogni pacchetto concatenato viene archiviata *tra* nx_packet_prepend_ptr e *nx_packet_append_ptr*.

Il driver è responsabile della costruzione dell'intestazione fisica. Se è necessario il mapping dell'indirizzo fisico all'indirizzo IP ,ad esempio Ethernet, il livello IP ha già risolto l'indirizzo MAC. L'indirizzo MAC di destinazione viene passato dall'istanza IP, archiviato in nx_ip_driver_physical_address_msw *e nx_ip_driver_physical_address_lsw.*

Dopo aver aggiunto l'intestazione fisica, l'elaborazione dell'invio di pacchetti chiama quindi la funzione di output del driver per trasmettere il pacchetto.

I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di invio di pacchetti.

| NX_IP_DRIVER membro               | Significato |
|-----------------------------------|---------------------------------------------------------------|
| nx_ip_driver_command              | NX_LINK_PACKET_SEND |
| nx_ip_driver_ptr                  | Puntatore all'istanza IP |
| nx_ip_driver_packet               | Puntatore al pacchetto da inviare |
| nx_ip_driver_interface            | Puntatore all'istanza dell'interfaccia.             |
| nx_ip_driver_physical_address_msw | Più significativi 32 bit di indirizzo fisico (solo se è necessario il mapping fisico) |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo fisico (solo se è necessario il mapping fisico)    |
| nx_ip_driver_status               | Stato di completamento. Se il driver non è in grado di inviare il pacchetto, restituirà uno stato di errore diverso da zero.  |

### <a name="packet-broadcast"></a>Trasmissione di pacchetti  
Questa richiesta è quasi identica alla richiesta di invio del pacchetto. L'unica differenza è che i campi dell'indirizzo fisico di destinazione sono impostati sull'indirizzo MAC broadcast Ethernet. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di trasmissione di pacchetti.

| NX_IP_DRIVER membro                | Significato          |
|------------------------------------|--------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_PACKET_BROADCAST |
| nx_ip_driver_ptr                   | Puntatore all'istanza IP  |
| nx_ip_driver_packet                | Puntatore al pacchetto da terminare |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF broadcast) |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF broadcast) |
| nx_ip_driver_interface             | Puntatore all'istanza dell'interfaccia. |
| nx_ip_driver_status                | Stato di completamento. Se il driver non è in grado di inviare il pacchetto, restituirà uno stato di errore diverso da zero. |

### <a name="arp-send"></a>Invio ARP  

Questa richiesta è simile alla richiesta di invio di pacchetti IP.
L'unica differenza è che l'intestazione Ethernet specifica un pacchetto ARP anziché un pacchetto IP e i campi dell'indirizzo fisico di destinazione sono impostati sull'indirizzo di trasmissione MAC. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di invio ARP.

| **NX_IP_DRIVER membro** | **Significato** |
| --- | --- |
| nx_ip_driver_command | NX_LINK_ARP_SEND |
| nx_ip_driver_ptr | Puntatore all'istanza IP. |
| nx_ip_driver_packet | Puntatore al pacchetto da inviare. |
| nx_ip_driver_physical_address_msw | 0x0000FFFF (trasmissione) |
| nx_ip_driver_physical_address_lsw | 0xFFFFFFFF (trasmissione) |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia. |
| nx_ip_driver_status | Stato di completamento. Se il driver non è in grado di inviare il pacchetto ARP, restituirà uno stato di errore diverso da zero. |

*Se il mapping fisico non è necessario, l'implementazione di questa richiesta non è necessaria.*

### <a name="arp-response-send"></a>Invio risposta ARP  

Questa richiesta è quasi identica alla richiesta di pacchetto di invio ARP. L'unica differenza è che i campi dell'indirizzo fisico di destinazione vengono passati dall'istanza IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di invio della risposta ARP.

| NX_IP_DRIVER membro               | Significato |
|-----------------------------------| ------------------------------------|
| nx_ip_driver_command              | NX_LINK_ARP_RESPONSE_SEND |
| nx_ip_driver_ptr                  | Puntatore all'istanza IP |
| nx_ip_driver_packet               | Puntatore al pacchetto da inviare|
| nx_ip_driver_physical_address_msw | 32 bit più significativi di indirizzo fisico |
| nx_ip_driver_physical_address_lsw | Meno significativi a 32 bit di indirizzo fisico                     |
| nx_ip_driver_interface            | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status               | Stato di completamento. Se il driver non è in grado di inviare il pacchetto ARP, restituirà uno stato di errore diverso da zero. |

> [!NOTE]
> *Se il mapping fisico non è necessario, l'implementazione di questa richiesta non è necessaria.*

### <a name="rarp-send"></a>INVIO RARP  

Questa richiesta è quasi identica alla richiesta di pacchetto di invio ARP. Le uniche differenze sono il tipo di intestazione del pacchetto e i campi dell'indirizzo fisico non sono necessari perché la destinazione fisica è sempre un indirizzo broadcast.

I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di invio RARP.

| NX_IP_DRIVER membro               | Significato |
|-----------------------------------|---------------------------------|
| nx_ip_driver_command              |NX_LINK_RARP_SEND |
| nx_ip_driver_ptr                  | Puntatore all'istanza IP |
| nx_ip_driver_packet               | Puntatore al pacchetto da inviare |
| nx_ip_driver_physical_address_msw | 0x0000FFFF (trasmissione) |
| nx_ip_driver_physical_address_lsw | 0xFFFFFFFF (trasmissione) |
| NX_IP_DRIVER membro               | Significato |
| nx_ip_driver_interface            | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status               | Stato di completamento. Se il driver non è in grado di inviare il pacchetto RARP, restituirà uno stato di errore diverso da zero.  |

> [!NOTE]
> *Le applicazioni che richiedono il servizio RARP devono implementare questo comando.*

### <a name="multicast-group-join"></a>Aggiunta a un gruppo multicast  

Questa richiesta viene effettuata con il servizio ***nx_igmp_multicast_interface join.*** Il driver di rete accetta l'indirizzo del gruppo multicast fornito e configura il supporto fisico per accettare i pacchetti in ingresso dall'indirizzo del gruppo multicast. Si noti che per i driver che non supportano il filtro multicast, la logica di ricezione del driver potrebbe essere in modalità promiscua. In questo caso, il driver potrebbe dover filtrare i frame in ingresso in base all'indirizzo MAC di destinazione, riducendo così la quantità di traffico passato nell'istanza IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di aggiunta a gruppi multicast.

| NX_IP_DRIVER membro               | Significato |
|-----------------------------------|-----------------------------------------------------------------------|
| nx_ip_driver_command              | NX_LINK_MULTICAST_JOIN                                                |
| nx_ip_driver_ptr                  | Puntatore all'istanza IP                                                |
| nx_ip_driver_physical_address_msw | 32 bit più significativi di indirizzo multicast fisico                |
| nx_ip_driver_physical_address_lsw | Meno significativi a 32 bit di indirizzo multicast fisico               |
| nx_ip_driver_interface            | Puntatore all'istanza dell'interfaccia                                     |
| nx_ip_driver_status               | Stato di completamento. Se il driver non è in grado di partecipare al gruppo multicast, restituirà uno stato di errore diverso da zero. |


### <a name="multicast-group-leave"></a>Gruppo multicast leave  

Questa richiesta viene richiamata chiamando in modo esplicito ***il nx_igmp_multicast_leave*** servizio. Il driver rimuove l'indirizzo multicast Ethernet fornito dall'elenco multicast. Dopo che un host ha lasciato un gruppo multicast, i pacchetti in rete con questo indirizzo multicast Ethernet non vengono più ricevuti da questa istanza IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di lasciare il gruppo multicast.

| NX_IP_DRIVER membro               | Significato |
|-----------------------------------|-----------------------------------------------------------------|
| nx_ip_driver_command              | NX_LINK_MULTICAST_LEAVE |
| nx_ip_driver_ptr                  | Puntatore all'istanza IP |
| nx_ip_driver_physical_address_msw | 32 bit più significativi di ddress multicast fisici |
| nx_ip_driver_physical_address_lsw | Meno significativi 32 bit di indirizzo multicast fisico |
| nx_ip_driver_interface            | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status               | Stato di completamento. Se il driver non è in grado di uscire dal gruppo multicast, restituirà uno stato di errore diverso da zero. |


### <a name="attach-interface"></a>Interfaccia di collegamento  

Questa richiesta viene richiamata da NetX al driver di dispositivo, consentendo al driver di associare l'istanza del driver all'istanza IP corrispondente e all'istanza dell'interfaccia fisica all'interno dell'indirizzo IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di interfaccia di collegamento.

| NX_IP_DRIVER membro    | Significato |
|------------------------|-------------------------------------------------|
| nx_ip_driver_command   | X_LINK_INTERFACE_ATTACH |
| nx_ip_driver_ptr       | Puntatore all'istanza IP |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia. |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di scollegare l'interfaccia specificata nell'istanza IP, restituirà uno stato di errore diverso da zero.  |


### <a name="detach-interface"></a>Scollegare l'interfaccia  

Questa richiesta viene richiamata da NetX al driver di dispositivo, consentendo al driver di dissociare l'istanza del driver con l'istanza IP corrispondente e l'istanza dell'interfaccia fisica all'interno dell'indirizzo IP. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di interfaccia di collegamento.

| NX_IP_DRIVER membro    | Significato |
|------------------------|---------------------------------------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_DETACH |
| nx_ip_driver_ptr       | Puntatore all'istanza IP |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia. |
| nx_ip_driver_status    | Stato di completamento. Se il driver non è in grado di collegare l'interfaccia specificata all'istanza IP, restituirà uno stato di errore diverso da zero. |

### <a name="get-link-status"></a>Ottenere lo stato del collegamento  

L'applicazione può eseguire query sullo stato del collegamento all'interfaccia di rete usando il servizio NetX  ***nx_ip_interface_status_check*** per qualsiasi interfaccia nell'host. Per altri dettagli su questi servizi, vedere il capitolo 4 "Descrizione dei servizi NetX" a pagina 107.

Lo stato del collegamento è contenuto nel *campo nx_interface_link_up* nella struttura NX_INTERFACE a cui punta *nx_ip_driver_interface* puntatore. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di stato del collegamento.

| NX_IP_DRIVER membro     | Significato                                                                                                      |
|-------------------------|--------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_STATUS                                                                                           |
| nx_ip_driver_ptr        | Puntatore all'istanza IP                                                                                       |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per posizionare lo stato.                                                              |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia                                                                            |
| nx_ip_driver_status     | Stato di completamento. Se il driver non è in grado di ottenere uno stato specifico, restituirà uno stato di errore diverso da zero. |
|                         |                                                                                                              |

> [!NOTE]
> ***nx_ip_status_check** è ancora disponibile per controllare lo stato dell'interfaccia primaria. Tuttavia, gli sviluppatori di applicazioni sono invitati a usare il servizio specifico **dell'interfaccia nx_ip_interface_status_check.***

### <a name="get-link-speed"></a>Ottenere la velocità di collegamento  

Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia la velocità della linea del collegamento nella destinazione fornita. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di velocità della linea di collegamento.

| NX_IP_DRIVER membro     | Significato |
|-------------------------|---------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_SPEED |
| nx_ip_driver_ptr        | Puntatore all'istanza IP |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per posizionare la velocità della linea |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status     | Stato di completamento. Se il driver non è in grado di ottenere informazioni sulla velocità, restituirà uno stato di errore diverso da zero.
 |


> [!NOTE]
> *Questa richiesta non viene usata internamente da NetX, quindi la relativa implementazione è facoltativa.*

### <a name="get-duplex-type"></a>Ottenere il tipo duplex  

Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il tipo duplex del collegamento nella destinazione fornita. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di tipo duplex.

| NX_IP_DRIVER membro     | Significato |
|-------------------------|-----------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_DUPLEX_TYPE |
| nx_ip_driver_ptr        | Puntatore all'istanza IP |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per posizionare il tipo duplex |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia |
| nx_ip_driver_status     | Stato di completamento. Se il driver non è in grado di ottenere informazioni duplex, restituirà uno stato di errore diverso da zero.
 |


> [!NOTE]
> *Questa richiesta non viene usata internamente da NetX, quindi la relativa implementazione è facoltativa.*

### <a name="get-error-count"></a>Ottenere il conteggio degli errori  

Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il numero di errori del collegamento nella destinazione fornita. Per supportare questa funzionalità, il driver deve tenere traccia degli errori dell'operazione. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di conteggio degli errori di collegamento.

| NX_IP_DRIVER membro     | Significato                                                                                                  |
|-------------------------|----------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_ERROR_COUNT                                                                                  |
| nx_ip_driver_ptr        | Puntatore all'istanza IP                                                                                   |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il conteggio degli errori                                                      |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia                                                                        |
| nx_ip_driver_status     | Stato di completamento. Se il driver non è in grado di ottenere il numero di errori, restituirà uno stato di errore diverso da zero. |


> [!NOTE]
> *Questa richiesta non viene usata internamente da NetX, quindi la relativa implementazione è facoltativa.*

### <a name="get-receive-packet-count"></a>Ottenere il numero di pacchetti di ricezione  

Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il numero di pacchetti di ricezione del collegamento nella destinazione fornita. Per supportare questa funzionalità, il driver deve tenere traccia del numero di pacchetti ricevuti. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di conteggio pacchetti di ricezione del collegamento.

| NX_IP_DRIVER membro     | Significato                                                                                                    |
|-------------------------|------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_RX_COUNT                                                                                       |
| nx_ip_driver_ptr        | Puntatore all'istanza IP                                                                                     |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il numero di pacchetti di ricezione                                               |
| nx_ip_driver_interface  | Puntatore all'interfaccia di rete fisica                                                                  |
| nx_ip_driver_status     | Stato di completamento. Se il driver non è in grado di ottenere il numero di ricezione, restituirà uno stato di errore diverso da zero. |


> [!NOTE]
> *Questa richiesta non viene usata internamente da NetX, quindi la relativa implementazione è facoltativa.*

### <a name="get-transmit-packet-count"></a>Ottenere il numero di pacchetti di trasmissione  

Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il numero di pacchetti di trasmissione del collegamento nella destinazione fornita. Per supportare questa funzionalità, il driver deve tenere traccia di ogni pacchetto trasmesso su ogni interfaccia. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di conteggio pacchetti di trasmissione del collegamento.

| NX_IP_DRIVER membro     | Significato                                                                                                     |
|-------------------------|-------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_TX_COUNT                                                                                        |
| nx_ip_driver_ptr        | Puntatore all'istanza IP                                                                                      |
| nx_ip_driver_return_ptr | Puntatore alla destinazione per inserire il numero di pacchetti di trasmissione                                               |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia                                                                           |
| nx_ip_driver_status     | Stato di completamento. Se il driver non è in grado di ottenere il numero di trasmissioni, restituirà uno stato di errore diverso da zero. |


> [!NOTE]
> *Questa richiesta non viene usata internamente da NetX, quindi la relativa implementazione è facoltativa.*

### <a name="get-allocation-errors"></a>Ottenere gli errori di allocazione  

Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver archivia il conteggio degli errori di allocazione del pool di pacchetti del collegamento nella destinazione fornita. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di conteggio degli errori di allocazione dei collegamenti.

| **NX_IP_DRIVER membro** | **Significato** |
| --- | ---|
| nx_ip_driver_command | NX_LINK_GET_ALLOC_ERRORS |
| nx_ip_driver_ptr | Puntatore all'istanza IP |

| NX_IP_DRIVER membro     | Significato                                                                                                        |
|-------------------------|----------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_return_ptr | Puntatore alla destinazione in cui inserire il conteggio degli errori di allocazione                                                 |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia                                                                              |
| nx_ip_driver_status     | Stato di completamento. Se il driver non è in grado di ottenere errori di allocazione, restituirà uno stato di errore diverso da zero. |


*Questa richiesta non viene usata internamente da NetX, quindi la relativa implementazione è facoltativa.*

### <a name="driver-deferred-processing"></a>Elaborazione posticipata dei driver  

Questa richiesta viene effettuata dal thread helper IP in risposta al driver che chiama la routine _ ***nx_ip_driver_deferred_processing*** da un ISR di trasmissione o ricezione. In questo modo l'ISR del driver può rinviare l'elaborazione di ricezione e trasmissione dei pacchetti al thread helper IP, riducendo così la quantità di elaborazione nell'ISR. Il *nx_interface_additional_link_info* nella struttura NX_INTERFACE a cui punta *nx_ip_driver_interface* può essere usato dal driver per archiviare informazioni sull'evento di elaborazione posticipato dal contesto del thread helper IP. I membri NX_IP_DRIVER seguenti vengono utilizzati per l'evento di elaborazione posticipata.

**NX_IP_DRIVER**

| member                 | Significato                           |
|------------------------|-----------------------------------|
| nx_ip_driver_command   | NX_LINK_DEFERRED_PROCESSING       |
| nx_ip_driver_ptr       | Puntatore all'istanza IP            |
| nx_ip_driver_interface | Puntatore all'istanza dell'interfaccia |


### <a name="user-commands"></a>Comandi utente  

Questa richiesta viene effettuata dall'interno ***nx_ip_driver_direct_command*** servizio. Il driver elabora i comandi utente specifici dell'applicazione. I membri NX_IP_DRIVER seguenti vengono usati per la richiesta di comando dell'utente.

| NX_IP_DRIVER membro     | Significato                                                                                                        |
|-------------------------|----------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_USER_COMMAND                                                                                           |
| nx_ip_driver_ptr        | Puntatore all'istanza IP                                                                                         |
| nx_ip_driver_return_ptr | Definita dall'utente                                                                                                   |
| nx_ip_driver_interface  | Puntatore all'istanza dell'interfaccia                                                                              |
| nx_ip_driver_status     | Stato di completamento. Se il driver non è in grado di eseguire i comandi utente, restituirà uno stato di errore diverso da zero. |


*Questa richiesta non viene usata internamente da NetX, quindi la relativa implementazione è facoltativa.*

### <a name="unimplemented-commands"></a>Comandi non implementati  

I comandi non implementati dal driver di rete devono avere il campo stato restituito impostato su NX_UNHANDLED_COMMAND.

## <a name="driver-output"></a>Driver Output  

Tutte le richieste di trasmissione di pacchetti menzionate in precedenza richiedono una funzione di output implementata nel driver. La logica di trasmissione specifica è specifica dell'hardware, ma in genere consiste nel controllare la capacità hardware per inviare immediatamente il pacchetto. Se possibile, il payload del pacchetto (e i payload aggiuntivi nella catena di pacchetti) vengono caricati in uno o più buffer di trasmissione hardware e viene avviata un'operazione di trasmissione. Se il pacchetto non rientra nei buffer di trasmissione disponibili, il pacchetto deve essere accodato e trasmesso quando i buffer di trasmissione diventano disponibili.

La coda di trasmissione consigliata è un elenco collegato in modo indosciente, con puntatori sia head che tail. I nuovi pacchetti vengono aggiunti alla fine della coda, mantenendo il pacchetto meno recente in primo piano. Il *nx_packet_queue_next* viene usato come collegamento successivo del pacchetto nella coda. Il driver definisce i puntatori head e tail della coda di trasmissione.

*Poiché l'accesso a questa coda viene eseguito dal thread e dalle parti di interrupt del driver, la protezione degli interrupt deve essere posizionata intorno alle modifiche della coda.*

La maggior parte delle implementazioni di hardware fisico genera un interrupt al completamento della trasmissione di pacchetti.
Quando il driver riceve un interrupt di questo tipo, in genere rilascia le risorse associate al pacchetto appena trasmesso. Se la logica di trasmissione legge i dati direttamente dal buffer NX_PACKET, il driver deve usare il ***servizio nx_packet_transmit_release*** per rilasciare il pacchetto associato all'interrupt completo di trasmissione al pool di pacchetti disponibile. Successivamente, il driver esamina la coda di trasmissione per i pacchetti aggiuntivi in attesa di essere inviati. Poiché molti dei pacchetti di trasmissione in coda che rientrano nei buffer di trasmissione hardware vengono de-accodati e caricati nei buffer. Questa operazione è seguita dall'avvio di un'altra operazione di invio.

Non appena i dati nel NX_PACKET sono stati spostati nel sistema di trasmissione FIFO (o nel caso in cui un driver supporti l'operazione zerocopy, i dati in NX_PACKET sono stati trasmessi), il driver deve spostare il nx_packet_prepend_ptr all'inizio dell'intestazione IP prima di chiamare ***nx_packet_transmit_release.*** Ricordarsi di modificare *nx_packet_length* campo di conseguenza. Se un frame IP è costituito da più pacchetti, deve essere rilasciato solo l'head della catena di pacchetti.

## <a name="driver-input"></a>Driver Input  

Al momento della ricezione di un interrupt di pacchetto ricevuto, il driver di rete recupera il pacchetto dai buffer di ricezione dell'hardware fisico e compila un pacchetto NetX valido. La creazione di un pacchetto NetX valido comporta la configurazione del campo di lunghezza appropriato e il concatenamento di più pacchetti se le dimensioni del pacchetto in ingresso sono maggiori di un singolo payload di pacchetto. Una volta compilato correttamente, il prepend_ptr viene spostato dopo l'intestazione fisica del livello e il pacchetto di ricezione viene inviato a NetX.

NetX presuppone che le intestazioni IP e ARP siano allineate su un limite ULONG. Il driver NetX deve pertanto garantire questo allineamento. Negli ambienti Ethernet questa operazione viene eseguita avviando l'intestazione Ethernet a due byte dall'inizio del pacchetto. Quando il *nx_packet_prepend_ptr* viene spostato oltre l'intestazione Ethernet, l'intestazione ARP o IP sottostante è allineata a 4byte.

In NetX sono disponibili diverse funzioni per i pacchetti di ricezione. Se il pacchetto ricevuto è un pacchetto ARP, _* **nx_arp_packet_deferred_receive**_ viene chiamato . Se il pacchetto ricevuto è un pacchetto RARP, viene _*_chiamato _ nx_rarp_packet_deferred_receive._*_ Sono disponibili diverse opzioni per la gestione dei pacchetti IP in ingresso. Per la gestione più rapida dei pacchetti IP, viene _*_nx_ip_packet_receive_*_ _ . Questo approccio presenta il minor sovraccarico, ma richiede una maggiore elaborazione nel gestore del servizio di interrupt di ricezione (ISR) del driver. Per l'elaborazione isr minima __ *_nx_ip_packet_deferred_receive_* viene chiamato * .

Dopo la corretta creazione del nuovo pacchetto di ricezione, i buffer di ricezione dell'hardware fisico sono stati configurati per ricevere più dati. Questa operazione potrebbe richiedere l'allocazione di pacchetti NetX e l'inserimento dell'indirizzo del payload nel buffer di ricezione hardware o semplicemente la modifica di un'impostazione nel buffer di ricezione hardware. Per ridurre al minimo le possibilità di sovraccarico, è importante che i buffer di ricezione dell'hardware abbiano buffer disponibili il prima possibile dopo la ricezione di un pacchetto.

*I buffer di ricezione iniziali vengono impostati durante l'inizializzazione del driver.*

### <a name="deferred-receive-packet-handling"></a>Gestione dei pacchetti di ricezione posticipata  

Il driver può rinviare l'elaborazione dei pacchetti di ricezione al thread helper IP NetX. Per alcune applicazioni potrebbe essere necessario ridurre al minimo l'elaborazione isr e i pacchetti eliminati. Per usare la gestione dei pacchetti posticipata, la libreria NetX deve prima essere compilata con ***NX_DRIVER_DEFERRED_PROCESSING** _ definito. In questo modo la logica dei pacchetti posticipata viene aggiunta al thread helper IP NetX. Successivamente, alla ricezione di un pacchetto di dati, il driver deve chiamare __nx_ip_packet_deferred_receive():*

```C
_nx_ip_packet_deferred_receive(ip_ptr, packet_ptr);
```

La funzione di ricezione posticipata inserisce il pacchetto di ricezione rappresentato da *packet_ptr* in un FIFO (elenco collegato) e invia una notifica al thread helper IP. Dopo l'esecuzione, l'helper IP chiama in modo ripetitivo la funzione di gestione posticipata per elaborare ogni pacchetto posticipato. L'elaborazione posticipata del gestore include in genere la rimozione dell'intestazione del livello fisico del pacchetto (in genere Ethernet) e l'invio a una di queste funzioni di ricezione NetX:  

***_nx_ip_packet_deferred_receive***  
***_nx_arp_packet_deferred_receive***  
***_nx_rarp_packet_deferred_receive*** 


## <a name="example-ram-ethernet-network-driver"></a>Driver di rete Ethernet ram di esempio  

Il sistema dimostrativo NetX viene fornito con un piccolo driver di rete basato su RAM, definito nel file ***nx_ram_network_driver.c.***
Questo driver presuppone che le istanze IP siano tutte nella stessa rete e assegna semplicemente indirizzi hardware virtuali (indirizzi MAC) a ogni istanza del dispositivo durante la creazione. Questo file fornisce un buon esempio della struttura di base dei driver di rete fisici NetX. Gli utenti possono sviluppare i propri driver di rete usando il framework di driver presentato in questo esempio.

La funzione entry del driver di rete è ***_nx_ram_network_driver,** _ che viene passata alla chiamata di creazione dell'istanza IP. Le funzioni di ingresso per interfacce di rete aggiuntive possono essere passate _*_al nx_ip_interface_attach_*_ servizio. Dopo l'avvio dell'esecuzione dell'istanza IP, viene richiamata la funzione di ingresso del driver per inizializzare e abilitare il dispositivo (vedere i casi _ *NX_LINK_INITIALIZE** **e NX_LINK_ENABLE**). Dopo aver **NX_LINK_ENABLE** comando, il dispositivo deve essere pronto per trasmettere e ricevere pacchetti. 

L'istanza IP trasmette i pacchetti di rete tramite uno dei comandi seguenti:

| ***NX_LINK_PACKET_SEND***    | È in corso la trasmissione di un pacchetto IP.                             |
| ------------------------------- | -------------------------------------------------------------- |
| ***NX_LINK_ARP_SEND***       | È in corso la trasmissione di una richiesta ARP o di un pacchetto di risposta ARP.    |
| ***NX_LINK_ARP_RARP_SEND*** | È in corso la trasmissione di un pacchetto di richiesta o risposta ARP inverso. |

Durante l'elaborazione di questi comandi, il driver di rete deve anteporre l'intestazione del frame Ethernet appropriata e quindi inviarla all'hardware sottostante per la trasmissione. Durante il processo di trasmissione, il driver di rete ha la proprietà esclusiva dell'area del buffer di pacchetti. Pertanto, una volta trasmessi i dati (o dopo che i dati sono stati copiati nel buffer di trasferimento interno del driver), il driver di rete è responsabile del rilascio del buffer di pacchetti spostando prima il puntatore anteposto oltre l'intestazione Ethernet nell'intestazione IP (e regolando di conseguenza la lunghezza del pacchetto) e quindi chiamando il servizio ***nx_packet_transmit_release*** per rilasciare il pacchetto. Se non si rilascia il pacchetto dopo la trasmissione dei dati, i pacchetti andranno persi.

Il driver di dispositivo di rete è anche responsabile della gestione dei pacchetti di dati in ingresso. Nell'esempio del driver RAM, il pacchetto ricevuto viene elaborato dalla funzione ***_nx_ram_network_driver_receive***.

Quando il dispositivo riceve un frame Ethernet, il driver è responsabile dell'archiviazione dei dati in

NX_PACKET struttura . Si noti che NetX presuppone che l'intestazione IP inizi da un indirizzo allineato a 4 byte. Poiché la lunghezza dell'intestazione Ethernet è di 14 byte, il driver deve archiviare l'inizio dell'intestazione Ethernet in un indirizzo allineato a 2 byte per garantire che l'intestazione IP inizi da un indirizzo allineato a 4 byte.