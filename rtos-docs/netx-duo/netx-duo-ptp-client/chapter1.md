---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo PTP client
description: Questo capitolo contiene un'introduzione al client PTP di Azure RTO NetX Duo.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5beec64bd6d74e3bed06be15255d6bd4a940ba64
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821710"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-ptp-client"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo PTP client

Azure RTO NetX Duo PTP implementa la parte client della versione 2, IEEE 1588-2008 del protocollo PTP (Precision Time Protocol). Viene usato per sincronizzare gli orologi tra MCU nella rete locale comunicando tra loro tramite pacchetti multicast IPv4 o IPv6.

## <a name="netx-duo-ptp-client-setup"></a>Installazione del client NetX Duo PTP

Per funzionare correttamente, il pacchetto client PTP richiede che sia già stata creata un'istanza IP di NetX Duo.

Per impostazione predefinita, il client PTP si unisce al gruppo multicast IPv4. Per eseguire il client PTP su una rete IPv6, `NX_ENABLE_IPV6_MULTICAST` è necessario definire quando si compila la libreria NETX Duo.

Quando si crea il client PTP, l'applicazione deve fornire una funzione di callback per gestire i timestamp dei pacchetti in ingresso e in uscita. Per ottenere una risoluzione elevata, è consigliabile che le applicazioni generino timestamp usando un timer ad alta risoluzione. Per eseguire il PTP sul simulatore, viene fornita un'implementazione basata su software `nx_ptp_client_soft_clock_callback` .

Il client PTP richiede un pool di pacchetti per la trasmissione di messaggi PTP. Le dimensioni del payload del pool di pacchetti non devono essere minori di `NX_UDP_PACKET + NX_PTP_CLIENT_PACKET_DATA_SIZE` , ovvero 108 byte per IPv4 e 128 byte se IPv6 è abilitato.

Dopo aver creato il client PTP, l'applicazione può avviare il client PTP. La sincronizzazione viene eseguita nel thread Helper PTP. È possibile specificare una funzione di callback degli eventi. Verrà richiamato quando si verifica uno degli eventi seguenti.
* Un Master è selezionato; 
* L'ora viene calibrata.
* Timeout del master.

## <a name="netx-duo-ptp-client-messages"></a>Messaggi client PTP NetX Duo

Il client PTP NetX Duo implementa solo il meccanismo di richiesta-risposta ritardata. Il client PTP apre due porte UDP. *319* per il messaggio di **evento** e *320* per il messaggio **generale** . Per questo meccanismo sono disponibili cinque tipi di messaggio.

* **Annunciare**. Si tratta di un messaggio di evento. Viene usato per la selezione del clock principale.
* **Sincronizzazione**. Si tratta di un messaggio di evento. Viene usato per inviare il timestamp di origine e calcolare il ritardo del percorso da master a client.
* **Follow_Up**. Si tratta di un messaggio generale. È facoltativo e viene usato per correggere il timestamp di origine nel messaggio di sincronizzazione correlato. Viene inviato solo quando viene impostato il bit a due fasi nel flag di sincronizzazione.
* **Delay_Req**. Si tratta di un messaggio di evento. Viene inviato dal client PTP per calcolare il ritardo del percorso da client a master, alla ricezione Delay_Resp.
* **Delay_Resp**. Si tratta di un messaggio di evento. Viene inviato da master a client per calcolare il ritardo del percorso dal client al database master.

*Si noti che l'algoritmo "Best master clock" non è implementato. Solo il primo clock master viene accettato quando il client PTP è in stato di ascolto.*

## <a name="netx-duo-ptp-client-clock-callback"></a>Callback Clock client PTP NetX Duo
Per sincronizzare clock dal master, il client PTP necessita di un orologio locale. Una funzione di callback clock viene passata nel client PTP durante la creazione. Il formato della routine di callback dell'orologio è definito di seguito.
```C
UINT ptp_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```
I parametri di input sono definiti come segue:
* *client_ptr* punta al client PTP.
* *Operation* specifica l'operazione di callback. i valori validi sono definiti come illustrato nell'elenco seguente.
  * **NX_PTP_CLIENT_CLOCK_INIT** Inizializza Clock.
  * **NX_PTP_CLIENT_CLOCK_SET** Imposta il timestamp corrente specificato da `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_GET** Restituisce il timestamp corrente a `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Estrarre il timestamp da `packet_ptr` a `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_ADJUST** Imposta il timestamp corrente inferiore a *1* secondo.
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Contrassegnare il `packet_ptr` che richiede per notificare al client PTP il timestamp al momento della trasmissione.
  * **NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Aggiornare il timer soft. Può essere ignorato dal clock dell'hardware.
* *time_ptr* punta al timestamp.
* *packet_ptr* punta al pacchetto.
* *callback_data* punta ai dati di callback opachi.

Il tipo di dati NX_PTP_TIME viene definito nel modo seguente.
```C
typedef struct NX_PTP_TIME_STRUCT
{
    /* The MSB of the number of seconds */
    LONG  second_high;

    /* The LSB of the number of seconds */
    ULONG second_low;

    /* The number of nanoseconds */
    LONG  nanosecond;
} NX_PTP_TIME;
```

## <a name="netx-duo-ptp-client-event-callback"></a>Callback evento client NetX Duo PTP
È possibile configurare la funzione di callback degli eventi per notificare all'applicazione lo stato del client PTP. Il formato della routine di callback degli eventi viene definito come illustrato di seguito.
```C
UINT event_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT event, 
    VOID *event_data, 
    VOID *callback_data);
```
I parametri di input sono.
* *client_ptr* punta al client PTP.
* *evento* specifica l'evento di callback. i valori validi sono definiti come segue:
  * **NX_PTP_CLIENT_EVENT_MASTER** È stato selezionato un clock master.
  * **NX_PTP_CLIENT_EVENT_SYNC** Il client PTP è calibrato.
  * **NX_PTP_CLIENT_EVENT_TIMEOUT** Il clock principale è il timeout.
* *event_data* specifica i dati correlati all'evento. Quando l'evento viene **NX_PTP_CLIENT_EVENT_MASTER**, event_data punta all' `NX_PTP_CLIENT_MASTER` istanza di. Quando l'evento viene **NX_PTP_CLIENT_EVENT_SYNC**, i dati dell'evento puntano all' `NX_PTP_CLIENT_SYNC` istanza.

## <a name="netx-duo-ptp-client-communication"></a>Comunicazione client PTP NetX Duo
Come indicato in precedenza, il client PTP NetX Duo supporta solo il meccanismo di richiesta-risposta di ritardo. Questo meccanismo misura il ritardo del percorso medio tra il client e il clock master come riportato di seguito:
1. Il client riceve il messaggio di *annuncio* dal master e lo seleziona come master migliore.
1. Il client riceve il messaggio di *sincronizzazione* dal database master. Il timestamp *T1* è il timestamp di origine in questo messaggio. Il timestamp *T2* viene letto dall'orologio locale quando viene ricevuto questo messaggio.
1. Il client riceve *Follow_Up* messaggio dal master. Questo messaggio è facoltativo e valido solo quando è impostato due passaggi nel flag di *sincronizzazione* . Il timestamp *T1* viene quindi aggiornato al timestamp di origine in questo messaggio.
1. Il client invia *Delay_Req* messaggio al database master. Il timestamp *T3* viene letto dall'orologio locale quando viene trasmesso il messaggio.
1. Il client riceve *Delay_Resp* messaggio dal master. Il timestamp *T4* è il timestamp di ricezione in questo messaggio.

Il ritardo medio del percorso viene calcolato come illustrato di seguito.
```C
<meanPathDelay>=[(t2-t1)+(t4-t3)]/2
```
L'offset dal master viene calcolato come illustrato di seguito.
```C
<offsetFromMaster>=client_clock-master_clock
                  =(t2-t1)-<meanPathDelay>
```

> [!NOTE]
> ***CorrectionField** _ viene ignorato durante la calculation._