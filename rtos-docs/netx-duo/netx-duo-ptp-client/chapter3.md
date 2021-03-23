---
title: Capitolo 3-Descrizione dei servizi client PTP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi client PTP NetX Duo in ordine alfabetico.
author: v-condav
ms.author: v-condav
ms.date: 01/27/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b4cdeca81c157934e35a219cd5535ec38f2c0746
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821707"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-ptp-client-services"></a>Capitolo 3-Descrizione dei servizi client PTP di Azure RTO NetX Duo

Questo capitolo contiene una descrizione di tutti i servizi client PTP NetX Duo (elencati di seguito) in ordine alfabetico.

[!NOTE]
> *Nella sezione **valori restituiti** nelle seguenti descrizioni della funzione API, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.*

## <a name="nx_ptp_client_create"></a>nx_ptp_client_create

Creare un'istanza del client PTP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_create(
    NX_PTP_CLIENT *client_ptr, NX_IP *ip_ptr, 
    UINT interface_index,
    NX_PACKET_POOL *packet_pool_ptr, 
    UINT thread_priority, 
    UCHAR *thread_stack, 
    UINT stack_size,
    NX_PTP_CLIENT_CLOCK_CALLBACK clock_callback, 
    VOID *clock_callback_data);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client PTP.

Si noti che l'applicazione deve prima creare un'istanza IP e un pool di pacchetti affinché il client PTP trasmetta i pacchetti. Per il pool di pacchetti, l'applicazione può usare lo stesso pool di pacchetti nell'istanza IP; in alternativa, è possibile creare un pool di pacchetti dedicato per il client PTP.  L'approccio dedicato ai pool di pacchetti ha il vantaggio di usare pacchetti di piccole dimensioni (128 byte pacchetti se viene usato IPv6 o 108 byte solo per IPv4).

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da creare
* **ip_ptr** Puntatore a istanza IP
* **interface_index** Indice dell'interfaccia di rete PTP
* **packet_pool_ptr** Puntatore al pool di pacchetti client
* **THREAD_PRIORITY**  Priorità del thread PTP
* **thread_stack** Puntatore a stack di thread
* **stack_size** Dimensioni dello stack di thread
* **clock_callback** Callback Clock PTP
* **clock_callback_data** Dati per il callback di clock

### <a name="return-values"></a>Valori restituiti
* Creazione del client **NX_SUCCESS** (0x00) completata
* Il payload del pacchetto **NX_PTP_CLIENT_INSUFFICIENT_PACKET_PAYLOAD** (0xD04) è troppo piccolo
* Errore **NX_PTP_CLIENT_CLOCK_CALLBACK_FAILURE** (0xD05) al callback Clock
* **stato** di Stato di completamento delle chiamate al servizio NetX Duo e ThreadX
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido
* Interfaccia NX_INVALID_INTERFACE (0x4C) non valida

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_delete"></a>nx_ptp_client_delete

Elimina un'istanza del client PTP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_delete(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del client PTP.

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da eliminare

### <a name="return-values"></a>Valori restituiti
* Il client **NX_SUCCESS** (0x00) è stato eliminato
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
/* Delete the PTP client instance */
status = nx_ptp_client_delete(&ptp_client);

/* If the client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_master_info_get"></a>nx_ptp_client_master_info_get

Ottenere informazioni sull'orologio Master.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_master_info_get(
    NX_PTP_CLIENT_MASTER *master_ptr, 
    NXD_ADDRESS *address, 
    UCHAR **port_identity, 
    UINT *port_identity_length, 
    UCHAR *priority1, 
    UCHAR *priority2, 
    UCHAR *clock_class, UCHAR *clock_accuracy, 
    USHORT *clock_variance, 
    UCHAR **grandmaster_identity,
    UINT *grandmaster_identity_length, 
    USHORT *steps_removed, 
    UCHAR *time_source);
```

### <a name="description"></a>Descrizione
Questo servizio ottiene informazioni sul clock del master. Il blocco di controllo master viene passato all'applicazione utente tramite la funzione di callback evento.

### <a name="input-parameters"></a>Parametri di input
* **master_ptr** Puntatore al clock master di PTP
* **Indirizzo** Indirizzo del clock master
* **port_identity** Identità e porta master PTP
* **port_identity_length** Lunghezza della porta master e dell'identità PTP
* **priority1** Priority1 di clock master PTP
* **Priority2** Priority2 di clock master PTP
* **clock_class** Classe di clock master PTP
* **clock_accuracy** Accuratezza del clock master PTP
* **clock_variance** Varianza del clock master PTP
* **grandmaster_identity** Identità del clock Grandmaster
* **grandmaster_identity_length** Lunghezza dell'identità del Grandmaster
* **steps_removed** Passaggi rimossi dall'intestazione PTP
* **Time_Source** Origine del timer usato dall'orologio Grandmaster

### <a name="return-values"></a>Valori restituiti
* **NX_SUCCESS** (0x00) ottenere correttamente le informazioni sull'orologio Master
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
NXD_ADDRESS address;
UCHAR *port_identity;
UINT port_identity_length;
UCHAR priority1, priority2;
UCHAR clock_class, clock_accuracy;
USHORT clock_variance;
UCHAR *grandmaster_identity;
UINT grandmaster_identity_length;
USHORT steps_removed;
UCHAR time_source;

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_MASTER:
        {
            status = nx_ptp_client_master_info_get((NX_PTP_CLIENT_MASTER *)event_data, 
                                                   &address, &port_identity,
                                                   &port_identity_length, &priority1, 
                                                   &priority2, &clock_class,
                                                   &clock_accuracy, &clock_variance, 
                                                   &grandmaster_identity,
                                                   &grandmaster_identity_length, 
                                                   &steps_removed, &time_source);

            /* If the master clock information was successfully get, status = NX_SUCCESS. */
            break;
        }

        /* Other event process. */
    }
}
```

## <a name="nx_ptp_client_packet_timestamp_notify"></a>nx_ptp_client_packet_timestamp_notify

Notifica al client PTP il timestamp del pacchetto.

### <a name="prototype"></a>Prototipo

```C
VOID nx_ptp_client_packet_timestamp_notify(
    NX_PTP_CLIENT *client_ptr, 
    NX_PACKET *packet_ptr, 
    NX_PTP_TIME *timestamp_ptr);
```

### <a name="description"></a>Descrizione
Questo servizio informa il client PTP che il pacchetto viene trasmesso con timestamp. Questo servizio è progettato per il driver di rete e viene richiamato quando il pacchetto viene trasmesso. Il timestamp viene in genere generato dall'hardware.

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da creare
* **packet_ptr** Puntatore al pacchetto PTP trasmesso
* **timestamp_ptr** Puntatore al timestamp del pacchetto PTP

### <a name="return-values"></a>Valori restituiti
nessuno

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
/* Call notification callback */
nx_ptp_client_packet_timestamp_notify(client_ptr, packet_ptr, &ts);
```

## <a name="nx_ptp_client_soft_clock_callback"></a>nx_ptp_client_soft_clock_callback

Implementazione del software di un clock di PTP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_soft_clock_callback(
    NX_PTP_CLIENT *client_ptr, 
    UINT operation,
    NX_PTP_TIME *time_ptr, 
    NX_PACKET *packet_ptr,
    VOID *callback_data);
```

### <a name="description"></a>Descrizione
Questa funzione di callback funge da origine di clock a bassa risoluzione simulata per PTP. Questa routine viene fornita come riferimento e non può essere usata per la produzione.

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da creare
* **operazione** di Operazione di callback. i valori validi sono definiti come segue:
  * **NX_PTP_CLIENT_CLOCK_INIT** Inizializza Clock.
  * **NX_PTP_CLIENT_CLOCK_SET** Imposta il timestamp corrente specificato da `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_GET** Restituisce il timestamp corrente a `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_EXTRACT** Estrarre il timestamp da `packet_ptr` a `time_ptr` .
  * **NX_PTP_CLIENT_CLOCK_ADJUST** Imposta il timestamp corrente inferiore a *1* secondo.
  * **NX_PTP_CLIENT_CLOCK_PACKET_TS_PREPARE** Contrassegnare il `packet_ptr` che richiede per notificare al client PTP il timestamp al momento della trasmissione.
  * **NX_PTP_CLIENT_CLOCK_SOFT_TIMER_UPDATE** Aggiornare il timer soft. Può essere ignorato dal clock dell'hardware.
* **time_ptr** Puntatore al timestamp.
* **packet_ptr** Puntatore al pacchetto.
* **callback_data** Puntatore ai dati di callback opachi.

### <a name="return-values"></a>Valori restituiti
* Operazione di **NX_SUCCESS** (0x00) riuscita
* Parametro **NX_PTP_PARAM_ERROR** (0XD03) non valido

### <a name="allowed-from"></a>Consentito da
PTP interno

### <a name="example"></a>Esempio
```C/* Create the PTP client instance */
status = nx_ptp_client_create(&ptp_client, &ip_0, 0, &pool_0, 
                              PTP_THREAD_PRIORITY, (UCHAR *)ptp_stack, sizeof(ptp_stack),
                              nx_ptp_client_soft_clock_callback, NX_NULL);

/* If the client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_start"></a>nx_ptp_client_start

Avviare il client PTP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_start(
    NX_PTP_CLIENT *client_ptr, 
    UCHAR *client_port_identity_ptr, 
    UINT client_port_identity_length,
    UINT domain, 
    UINT transport_specific, 
    NX_PTP_CLIENT_EVENT_CALLBACK event_callback,
    VOID *event_callback_data)
```

### <a name="description"></a>Descrizione
Questo servizio avvia un'istanza del client PTP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da creare
* **client_port_identity_ptr** Puntatore alla porta e all'identità client, può essere NULL
* **client_port_identity_length** Lunghezza della porta e dell'identità del client. Deve essere 0 se client_port_identity_ptr è NULL o NX_PTP_CLOCK_PORT_IDENTITY_SIZE (10)
* **dominio** Dominio orologio PTP
* **transport_specific** 4 bit di trasporto specifico
* **event_callback** Funzione di callback richiamata sull'evento
* **event_callback_data** Dati per il callback di evento

### <a name="return-values"></a>Valori restituiti
* Il client **NX_SUCCESS** (0x00) è stato avviato
* Il client PTP **NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) è già stato avviato
* **stato** di Stato di completamento delle chiamate al servizio NetX Duo e ThreadX
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
status = nx_ptp_client_start(&ptp_client, NX_NULL, 0, 0, 0, ptp_event_callback, NX_NULL);

/* If the client was successfully started, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_stop"></a>nx_ptp_client_stop

Arrestare il client PTP.  Quando il client PTP viene arrestato, non elabora i pacchetti PTP né trasmette i pacchetti PTP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_stop(NX_PTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione
Questo servizio interrompe un'istanza del client PTP creata e avviata in precedenza.

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da arrestare

### <a name="return-values"></a>Valori restituiti
* Il client **NX_SUCCESS** (0x00) è stato arrestato
* Client **NX_PTP_CLIENT_NOT_STARTED** (0xD01) non avviato
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
status = nx_ptp_client_stop(&ptp_client);

/* If the client was successfully stopped, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_sync_info_get"></a>nx_ptp_client_sync_info_get

Ottenere le informazioni di sincronizzazione.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_sync_info_get(
    NX_PTP_CLIENT_SYNC *sync_ptr, 
    USHORT *flags, 
    SHORT *utc_offset);
```

### <a name="description"></a>Descrizione
Questo servizio ottiene informazioni sul messaggio di sincronizzazione. Il blocco di controllo di sincronizzazione viene passato all'applicazione utente tramite la funzione di callback evento.

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da creare
* **flag** Flag nel messaggio di sincronizzazione
* **utc_offset** Offset tra TAI e UTC

### <a name="return-values"></a>Valori restituiti
* **NX_SUCCESS** (0x00) ottenere correttamente le informazioni di sincronizzazione
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
static UINT ptp_event_callback(NX_PTP_CLIENT *ptp_client_ptr, UINT event, VOID *event_data, VOID *callback_data)
{
USHORT utc_offset;

    switch (event)
    {
        case NX_PTP_CLIENT_EVENT_SYNC:
        {
            nx_ptp_client_sync_info_get((NX_PTP_CLIENT_SYNC *)event_data, NX_NULL, &utc_offset);

            /* If the Sync information was successfully get, status = NX_SUCCESS. */
            break;
        }

        /* Other event process. */
    }
}
```

## <a name="nx_ptp_client_time_get"></a>nx_ptp_client_time_get

Ottiene l'ora corrente.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_time_get(
    NX_PTP_CLIENT *client_ptr, 
    NX_PTP_TIME *time_ptr);
```

### <a name="description"></a>Descrizione
Questo servizio ottiene il valore corrente del clock di PTP. È disponibile, indipendentemente dal fatto che il client PTP sia sincronizzato con l'orologio Master.

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da creare
* **time_ptr** Puntatore all'ora di PTP

### <a name="return-values"></a>Valori restituiti
* Creazione del client **NX_SUCCESS** (0x00) completata
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
/* Get the PTP clock */
nx_ptp_client_time_get(&ptp_client, &tm);
```

## <a name="nx_ptp_client_time_set"></a>nx_ptp_client_time_set

Imposta l'ora corrente.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_time_set(
    NX_PTP_CLIENT *client_ptr, 
    NX_PTP_TIME *time_ptr);
```

### <a name="description"></a>Descrizione
Questo servizio imposta il valore corrente del clock di PTP. Deve essere richiamato prima dell'avvio del client PTP.

### <a name="input-parameters"></a>Parametri di input
* **client_ptr** Puntatore al client PTP da creare
* **time_ptr** Puntatore all'ora di PTP

### <a name="return-values"></a>Valori restituiti
* Creazione del client **NX_SUCCESS** (0x00) completata
* Il client PTP **NX_PTP_CLIENT_ALREADY_STARTED** (0xD02) è già stato avviato
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
/* Set current time before PTP client started.  */
status = nx_ptp_client_time_set(&ptp_client, &tm);
```

## <a name="nx_ptp_client_utility_convert_time_to_date"></a>nx_ptp_client_utility_convert_time_to_date

Convertire l'ora del PTP in una data e un'ora UTC.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_utility_convert_time_to_date(
    NX_PTP_TIME *time_ptr, 
    LONG offset, 
    NX_PTP_DATE_TIME *date_time_ptr);
```

### <a name="description"></a>Descrizione
Questo servizio converte l'ora PTP in una data e un'ora UTC.

### <a name="input-parameters"></a>Parametri di input
* **time_ptr** Puntatore all'ora di PTP
* **offset** Offset del secondo con segno per aggiungere l'ora di PTP
* **date_time_ptr** Puntatore alla data risultante

### <a name="return-values"></a>Valori restituiti
* Creazione del client **NX_SUCCESS** (0x00) completata
* **Puntatore alla data risultante** (0xD03) parametro di input non valido
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
/* convert PTP time to UTC date and time */
status = nx_ptp_client_utility_convert_time_to_date(&tm, -ptp_utc_offset, &date);

/* If the time was successfully converted, status = NX_SUCCESS. */
```

## <a name="nx_ptp_client_utility_time_diff"></a>nx_ptp_client_utility_time_diff

Diff due volte PTP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_ptp_client_utility_time_diff(
    NX_PTP_TIME *time1_ptr, 
    NX_PTP_TIME *time2_ptr, 
    NX_PTP_TIME *result_ptr);
```

### <a name="description"></a>Descrizione
Questo servizio calcola la differenza tra due volte PTP.

### <a name="input-parameters"></a>Parametri di input
* **time1_ptr** Puntatore alla prima ora PTP
* **time2_ptr** Puntatore alla seconda ora PTP
* **result_ptr** Puntatore al risultato time1-time2

### <a name="return-values"></a>Valori restituiti
* Creazione del client **NX_SUCCESS** (0x00) completata
* Parametro puntatore di input NX_PTR_ERROR (0x07) non valido

### <a name="allowed-from"></a>Consentito da
Thread

### <a name="example"></a>Esempio
```C
/* Diff time.  */
status = nx_ptp_client_utility_time_diff(&time1, &time2, &result);

/* If the calculation was successfully, status = NX_SUCCESS. */
```