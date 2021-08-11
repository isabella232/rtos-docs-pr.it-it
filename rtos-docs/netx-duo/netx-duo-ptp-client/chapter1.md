---
title: Capitolo 1 - Introduzione al client Azure RTOS NetX Duo PTP
description: Questo capitolo contiene un'introduzione al client Azure RTOS NetX Duo PTP.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cf7210529121c8e49ff3cabbb7c673288b803f24760096396f32f33d4a9fb7e6
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798045"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-ptp-client"></a>Capitolo 1 - Introduzione al client Azure RTOS NetX Duo PTP

Il Azure RTOS NetX Duo PTP implementa la parte client di Precision Time Protocol (PTP) versione 2, IEEE 1588-2008. Viene usato per sincronizzare gli orologi tra le UNITÀ di gestione nella rete locale comunicando tra loro tramite pacchetti multicast IPv4 o IPv6.

## <a name="netx-duo-ptp-client-setup"></a>Configurazione del client NetX Duo PTP

Per funzionare correttamente, il pacchetto client PTP richiede che sia già stata creata un'istanza IP di NetX Duo.

Per impostazione predefinita, il client PTP aggiunge un gruppo multicast IPv4. Per eseguire il client PTP in una rete IPv6, è necessario definire quando si `NX_ENABLE_IPV6_MULTICAST` compila la libreria NetX Duo.

Quando si crea il client PTP, l'applicazione deve fornire una funzione di callback per gestire i timestamp dei pacchetti in ingresso e in uscita. Per ottenere una risoluzione elevata, è consigliabile che le applicazioni generino timestamp usando un timer ad alta risoluzione. Per eseguire PTP nel simulatore, viene fornita un'implementazione basata `nx_ptp_client_soft_clock_callback` su software.

Il client PTP richiede un pool di pacchetti per la trasmissione di messaggi PTP. Le dimensioni del payload del pool di pacchetti non devono essere inferiori a , ovvero 108 byte per `NX_UDP_PACKET + NX_PTP_CLIENT_PACKET_DATA_SIZE` IPv4 e 128 byte se IPv6 è abilitato.

Dopo aver creato il client PTP, l'applicazione può avviare il client PTP. La sincronizzazione viene eseguita nel thread helper PTP. È possibile specificare una funzione di callback dell'evento. Verrà richiamato quando si verifica uno degli eventi seguenti.
* Viene selezionato un master. 
* L'ora viene calibrata.
* Timeout di un master.

## <a name="netx-duo-ptp-client-messages"></a>Messaggi del client NetX Duo PTP

Il client NetX Duo PTP implementa solo il meccanismo di ritardo richiesta-risposta. Il client PTP apre due porte UDP. *319 per* il **messaggio di** evento e *320 per* il **messaggio** generale. Esistono cinque tipi di messaggio per questo meccanismo.

* **Annunciare**. Si tratta di un messaggio di evento. Viene usato per la selezione dell'orologio master.
* **Sincronizzare**. Si tratta di un messaggio di evento. Viene usato per inviare il timestamp di origine e calcolare il ritardo del percorso dal master al client.
* **Follow_Up**. Si tratta di un messaggio generale. È facoltativo e viene usato per correggere il timestamp di origine nel messaggio sync correlato. Viene inviato solo quando è impostato il bit in due passaggi nel flag Sync.
* **Delay_Req**. Si tratta di un messaggio di evento. Viene inviato dal client PTP per calcolare il ritardo del percorso dal client al master, alla ricezione Delay_Resp.
* **Delay_Resp**. Si tratta di un messaggio di evento. Viene inviato dal master al client per calcolare il ritardo del percorso dal client al master.

*Si noti che l'algoritmo "best master clock" non è implementato. Quando il client PTP è in stato di ascolto, viene accettato solo il primo clock master.*

## <a name="netx-duo-ptp-client-clock-callback"></a>NetX Duo PTP Client Clock Callback
Per sincronizzare l'orologio dal master, il client PTP richiede un orologio locale. Una funzione di callback di clock viene passata al client PTP durante la creazione. Il formato della routine di callback dell'orologio è definito di seguito.
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
* *operation* specifica l'operazione di callback. I valori validi sono definiti come illustrato nell'elenco seguente.
  * **NX_PTP_CLIENT_CLOCK_INIT** Inizializzare l'orologio.
  * **NX_PTP_CLIENT_CLOCK_SET** Imposta il timestamp corrente specificato da `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_GET** Restituisce il timestamp corrente a `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Estrarre il timestamp da `packet_ptr` a `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_ADJUST** Regolare il timestamp corrente minore di *1* secondo.
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Contrassegnare `packet_ptr` l'oggetto che richiede di notificare al client PTP il timestamp quando viene trasmesso.
  * **NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Aggiornare il timer software. Può essere ignorato dall'orologio hardware.
* *time_ptr* punta al timestamp.
* *packet_ptr* punta al pacchetto.
* *callback_data* punta a dati di callback opachi.

Il NX_PTP_TIME di dati è definito come segue.
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

## <a name="netx-duo-ptp-client-event-callback"></a>Callback di eventi del client NetX Duo PTP
La funzione di callback dell'evento può essere impostata per notificare all'applicazione lo stato del client PTP. Il formato della routine di callback dell'evento è definito come illustrato di seguito.
```C
UINT event_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT event, 
    VOID *event_data, 
    VOID *callback_data);
```
I parametri di input sono .
* *client_ptr* punta al client PTP.
* *event* specifica l'evento di callback. I valori validi sono definiti come:
  * **NX_PTP_CLIENT_EVENT_MASTER** Viene selezionato un orologio master.
  * **NX_PTP_CLIENT_EVENT_SYNC** Il client PTP è calibrato.
  * **NX_PTP_CLIENT_EVENT_TIMEOUT** L'orologio master è un timeout.
* *event_data* specifica i dati correlati all'evento. Quando l'evento **NX_PTP_CLIENT_EVENT_MASTER**, event_data punta all'istanza `NX_PTP_CLIENT_MASTER` di . Quando l'evento **viene NX_PTP_CLIENT_EVENT_SYNC**, i dati dell'evento puntano all'istanza `NX_PTP_CLIENT_SYNC` di .

## <a name="netx-duo-ptp-client-communication"></a>Comunicazione client NetX Duo PTP
Come accennato in precedenza, il client NetX Duo PTP supporta solo il meccanismo di richiesta-risposta ritardata. Questo meccanismo misura il ritardo medio del percorso tra il client e l'orologio master come indicato di seguito:
1. Il client riceve *il messaggio di* annuncio dal master e lo seleziona come master migliore.
1. Il client riceve *il messaggio di* sincronizzazione dal master. Il timestamp *t1* è il timestamp di origine in questo messaggio. Il timestamp *t2* viene letto dall'orologio locale quando viene ricevuto questo messaggio.
1. Il client riceve *Follow_Up* messaggio dal master. Questo messaggio è facoltativo e valido solo quando sono impostati due passaggi in Flag *di* sincronizzazione. Il timestamp *t1 viene* quindi aggiornato al timestamp di origine in questo messaggio.
1. Il client *Delay_Req* un messaggio al master. Il timestamp *t3* viene letto dall'orologio locale quando il messaggio viene trasmesso.
1. Il client riceve *Delay_Resp* dal master. Il timestamp *t4* è il timestamp di ricezione in questo messaggio.

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
> *Il campo ***correctionField** _ viene ignorato durante la calculation._