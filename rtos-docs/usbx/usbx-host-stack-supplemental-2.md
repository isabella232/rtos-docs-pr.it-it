---
title: API delle classi host USBX
description: In questo capitolo vengono illustrate tutte le API esposte delle classi host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 39f3a71c28dd14e0093f72d1a3b1ff6837c6f1f7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824017"
---
# <a name="chapter-2-usbx-host-classes-api"></a>Capitolo 2: API delle classi host USBX

In questo capitolo vengono illustrate tutte le API esposte delle classi host USBX. Le API seguenti per ogni classe sono descritte in dettaglio.

- Classe Printer
- Classe audio
- Classe ASIX
- Classe Pima/PTP
- Classe Prolific
- Classe seriale generica

## <a name="ux_host_class_printer_read"></a>ux_host_class_printer_read

Leggere dall'interfaccia stampante.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_printer_read(
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Descrizione

Questa funzione legge dall'interfaccia stampante. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo. Una lettura è consentita solo su stampanti bidirezionali.

### <a name="parameters"></a>Parametri

- **Printer**: puntatore all'istanza della classe Printer.
- **data_pointer**: puntatore all'indirizzo del buffer del payload di dati.
- **requested_length**: lunghezza da ricevere.
- **actual_length**: lunghezza effettivamente ricevuta.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- La funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non è supportata perché la stampante non è bidirezionale.
- **UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, lettura incompleta.

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_read(printer, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_write"></a>ux_host_class_printer_write

Scrivere nell'interfaccia stampante.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_printer_write(
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *data_pointer,  
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Descrizione

Questa funzione scrive nell'interfaccia stampante. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.

### <a name="parameters"></a>Parametri

- **Printer**: puntatore all'istanza della classe Printer.
- **data_pointer**: puntatore all'indirizzo del buffer del payload di dati.
- **requested_length**: lunghezza da inviare.
- **actual_length**: lunghezza effettivamente inviata.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, scrittura incompleta.

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_write(printer, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_soft_reset"></a>ux_host_class_printer_soft_reset

Eseguire un ripristino soft alla stampante.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_printer_soft_reset(UX_HOST_CLASS_PRINTER *printer)
```

### <a name="description"></a>Descrizione

Questa funzione esegue un ripristino soft alla stampante.

### <a name="input-parameter"></a>Parametro di input

- **Printer**: puntatore all'istanza della classe Printer.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) la reimpostazione è stata completata.
- **UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, reimpostazione non completata.

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_soft_reset(printer);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_status_get"></a>ux_host_class_printer_status_get

Ottenere lo stato della stampante

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_printer_status_get( 
    UX_HOST_CLASS_PRINTER *printer,
    ULONG *printer_status)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene lo stato della stampante. Lo stato della stampante è simile allo stato di LPT (1284 standard).

### <a name="parameters"></a>Parametri

- **Printer**: puntatore all'istanza della classe Printer.
- **printer_status**: indirizzo dello stato da restituire.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00): la reimpostazione è stata completata.
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per eseguire l'operazione.
- **UX_TRANSFER_TIMEOUT**: (0x5c) Timeout trasferimento, reimpostazione non completata

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_status_get(printer, printer_status);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_device_id_get"></a>ux_host_class_printer_device_id_get

Ottenere l'ID del dispositivo stampante.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_printer_device_id_get( 
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *descriptor_buffer, 
    ULONG length)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene la stringa dell'ID dispositivo IEEE 1284 (inclusa la lunghezza nei primi due byte nel formato big endian).

### <a name="parameters"></a>Parametri

- **Printer**: puntatore all'istanza della classe Printer.
- **descriptor_buffer**: puntatore a un buffer per riempire la stringa dell'ID dispositivo IEEE 1284 (inclusa la lunghezza nei primi due byte nel formato) 
- **length**: lunghezza del buffer in byte.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00): l'operazione è stata completata.
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per eseguire l'operazione.
- **UX_TRANSFER_TIMEOUT**: (0x5c) Timeout trasferimento, richiesta non completata
- **UX_TRANSFER_NOT_READY**: (0x25) il dispositivo si trova in uno stato non valido. deve essere collegato, risolto o configurato.
- **UX_TRANSFER_STALL**: (0x21) il trasferimento è bloccato.
- La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.
- **TX_SEMAPHORE_ERROR** (0x0C) puntatore del semaforo di conteggio non valido.
- **TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_device_id_get(printer, descriptor_buffer, length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_read"></a>ux_host_class_audio_read

Leggere dall'interfaccia audio.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_audio_read(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_TRANSFER_REQUEST
    *audio_transfer_request)
```

### <a name="description"></a>Descrizione

Questa funzione legge dall'interfaccia audio. La chiamata non è bloccata. L'applicazione deve verificare che sia stata selezionata l'impostazione alternativa appropriata per l'interfaccia di streaming audio.

### <a name="parameters"></a>Parametri

- **audio**: puntatore all'istanza della classe audio.
- **audio_transfer_request**: puntatore alla struttura di trasferimento audio.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato
- Funzione **UX_FUNCTION_NOT_SUPPORTED**"(0x54) non supportata

### <a name="example"></a>Esempio

```C
/* The following example reads from the audio interface. */

audio_transfer_request.ux_host_class_audio_transfer_request_completion_function = tx_audio_transfer_completion_function;
audio_transfer_request.ux_host_class_audio_transfer_request_class_instance = audio;
audio_transfer_request.ux_host_class_audio_transfer_request_next_audio_audio_transfer_request = UX_NULL;
audio_transfer_request.ux_host_class_audio_transfer_request_data_pointer = audio_buffer;
audio_transfer_request.ux_host_class_audio_transfer_request_requested_length = requested_length;
audio_transfer_request.ux_host_class_audio_transfer_request_packet_length = AUDIO_FRAME_LENGTH;

status = ux_host_class_audio_read(audio, audio_transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_write"></a>ux_host_class_audio_write

Scrivere nell'interfaccia audio.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_audio_write(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_TRANSFER_REQUEST *audio_transfer_request)
```

### <a name="description"></a>Descrizione

Questa funzione scrive nell'interfaccia audio. La chiamata non è bloccata. L'applicazione deve verificare che sia stata selezionata l'impostazione alternativa appropriata per l'interfaccia di streaming audio.

### <a name="parameters"></a>Parametri

- **audio**: puntatore all'istanza della classe audio
- **audio_transfer_request**: puntatore alla struttura di trasferimento audio

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata.
- Interfaccia **ux_host_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta.

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example writes to the audio interface */

audio_transfer_request.ux_host_class_audio_transfer_request_completion_function = tx_audio_transfer_completion_function;
audio_transfer_request.ux_host_class_audio_transfer_request_class_instance = audio;
audio_transfer_request.ux_host_class_audio_transfer_request_next_audio_audio_transfer_request = UX_NULL;
audio_transfer_request.ux_host_class_audio_transfer_request_data_pointer = audio_buffer;
audio_transfer_request.ux_host_class_audio_transfer_request_requested_length = requested_length;
audio_transfer_request.ux_host_class_audio_transfer_request_packet_length = AUDIO_FRAME_LENGTH;
status = ux_host_class_audio_write(audio, audio_transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_control_get"></a>ux_host_class_audio_control_get

Ottenere un controllo specifico dall'interfaccia del controllo audio.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_audio_control_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

### <a name="description"></a>Descrizione

Questa funzione legge un controllo specifico dall'interfaccia del controllo audio.

### <a name="parameters"></a>Parametri

- **audio**: puntatore all'istanza della classe audio
- **audio_control**: puntatore alla struttura del controllo audio

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato
- Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata
- Interfaccia **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example reads the volume control from a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_CONTROL audio_control;

audio_control.ux_host_class_audio_control_channel = 1;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;

status = ux_host_class_audio_control_get(audio, &audio_control);

/* If status equals UX_SUCCESS, the operation was successful. */

audio_control.ux_host_class_audio_control_channel = 2;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;

status = ux_host_class_audio_control_get(audio, &audio_control);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_control_value_set"></a>ux_host_class_audio_control_value_set

Impostare un controllo specifico sull'interfaccia del controllo audio.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_audio_control_value_set(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

* * Descrizione * *

Questa funzione imposta un controllo specifico sull'interfaccia del controllo audio.

### <a name="parameters"></a>Parametri

- **audio**: puntatore all'istanza della classe audio
- **audio_control**: puntatore alla struttura del controllo audio

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato
- Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata
- Interfaccia **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta

### <a name="example"></a>Esempio

```C
/* The following example sets the volume control of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_CONTROL audio_control;

UINT status;

audio_control.ux_host_class_audio_control_channel = 1;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
audio_control.ux_host_class_audio_control_cur = 0xf000;

status = ux_host_class_audio_control_value_set(audio, &audio_control);
/* If status equals UX_SUCCESS, the operation was successful. */

current_volume = audio_control.audio_control_cur;
audio_control.ux_host_class_audio_control_channel = 2;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
audio_control.ux_host_class_audio_control_cur = 0xf000;

status = ux_host_class_audio_control_value_set(audio, &audio_control);
/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_streaming_sampling_set"></a>ux_host_class_audio_streaming_sampling_set

Impostare un'interfaccia di impostazione alternativa dell'interfaccia di streaming audio.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_audio_streaming_sampling_set
    (UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING *audio_sampling)
```

### <a name="description"></a>Descrizione

Questa funzione imposta l'interfaccia di impostazione alternativa appropriata dell'interfaccia di streaming audio in base a una struttura di campionamento specifica.

### <a name="parameters"></a>Parametri

- **audio**: puntatore all'istanza della classe audio.
- **audio_sampling**: puntatore alla struttura di campionamento audio.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato
- Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata
- Interfaccia **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta
- **UX_NO_ALTERNATE_SETTING**: (0X5e) nessuna impostazione alternativa per i valori di campionamento

### <a name="example"></a>Esempio

```C
/* The following example sets the alternate setting interface of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_SAMPLING audio_sampling;

UINT status;

sampling.ux_host_class_audio_sampling_channels = 2;
sampling.ux_host_class_audio_sampling_frequency = AUDIO_FREQUENCY;
sampling. ux_host_class_audio_sampling_resolution = 16;

status = ux_host_class_audio_streaming_sampling_set(audio, &sampling);
/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_streaming_sampling_get"></a>ux_host_class_audio_streaming_sampling_get

Ottenere le possibili impostazioni di campionamento dell'interfaccia di streaming audio.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_audio_streaming_sampling_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING_CHARACTERISTICS *audio_sampling)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene, una alla volta, tutte le possibili impostazioni di campionamento disponibili in ognuna delle impostazioni alternative dell'interfaccia di streaming audio. La prima volta che si usa la funzione, è necessario reimpostare tutti i campi nel puntatore della struttura chiamante. La funzione restituirà un set specifico di valori di flusso alla restituzione, a meno che non sia stata raggiunta la fine delle impostazioni alternative. Quando questa funzione viene riutilizzata, per individuare i valori di campionamento successivi verranno utilizzati i valori di campionamento precedenti.

### <a name="parameters"></a>Parametri

- **audio**: puntatore all'istanza della classe audio.
- **audio_sampling**: puntatore alla struttura di campionamento audio.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato
- Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata
- Interfaccia **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta
- **UX_NO_ALTERNATE_SETTING**: (0X5e) nessuna impostazione alternativa per i valori di campionamento

### <a name="example"></a>Esempio

```C
/* The following example gets the sampling values for the first alternate setting interface of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_SAMPLING_CHARACTERISTICS audio_sampling;

UINT status;

sampling.ux_host_class_audio_sampling_channels=0;
sampling.ux_host_class_audio_sampling_frequency_low=0;
sampling.ux_host_class_audio_sampling_frequency_high=0;
sampling.ux_host_class_audio_sampling_resolution=0;

status = ux_host_class_audio_streaming_sampling_get(audio, &sampling);

/* If status equals UX_SUCCESS, the operation was successful and information could be displayed as follows:

printf("Number of channels %d, Resolution %d bits, frequency range %d-%d\n",
    sampling.audio_channels, sampling.audio_resolution,
    sampling.audio_frequency_low, sampling.audio_frequency_high);

*/
```

## <a name="ux_host_class_asix_read"></a>ux_host_class_asix_read

Leggere dall'interfaccia ASIX.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_asix_read(
    UX_HOST_CLASS_ASIX *asix,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Descrizione

Questa funzione legge dall'interfaccia ASIX. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.

### <a name="parameters"></a>Parametri

- **ASIX**: puntatore all'istanza della classe ASIX.
- **data_pointer**: puntatore all'indirizzo del buffer del payload di dati.
- **requested_length**: lunghezza da ricevere.
- **actual_length**: lunghezza effettivamente ricevuta.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, lettura incompleta.

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_read(asix, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_asix_write"></a>ux_host_class_asix_write

Scrivere nell'interfaccia ASIX.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_asix_write(
    VOID *asix_class,
    NX_PACKET *packet)
```

### <a name="description"></a>Descrizione

Questa funzione scrive nell'interfaccia ASIX. La chiamata non è bloccata.

### <a name="parameters"></a>Parametri

- **ASIX**: puntatore all'istanza della classe ASIX.
- **pacchetto: pacchetto** di dati NETX

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- Non è stato possibile richiedere il trasferimento **UX_ERROR**: (0xFF).

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_write(asix, packet);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_pima_session_open"></a>ux_host_class_pima_session_open

Apre una sessione tra l'iniziatore e il risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_session_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a>Descrizione

Questa funzione apre una sessione tra un iniziatore PIMA e un risponditore PIMA. Una volta aperta correttamente una sessione, è possibile eseguire la maggior parte dei comandi PIMA.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_sessio**: puntatore alla sessione Pima<

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** sessione: (0x00) aperta correttamente
- **UX_HOST_CLASS_PIMA_RC_SESSION_ALREADY_OPENED**: (0X201E) sessione già aperta

### <a name="example"></a>Esempio

```C
/* Open a pima session. */

status = ux_host_class_pima_session_open(pima, pima_session);

if (status != UX_SUCCESS)
    return(UX_PICTBRIDGE_ERROR_SESSION_NOT_OPEN);
```

## <a name="ux_host_class_pima_session_close"></a>ux_host_class_pima_session_close

Chiude una sessione tra l'iniziatore e il risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_session_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a>Descrizione

Questa funzione chiude una sessione precedentemente aperta tra un iniziatore PIMA e un risponditore PIMA. Dopo la chiusura di una sessione, la maggior parte dei comandi PIMA non può più essere eseguita.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) la sessione è stata chiusa.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: la sessione (0x2003) non è aperta.

### <a name="example"></a>Esempio

```C
/* Close the pima session. */

status = ux_host_class_pima_session_close(pima, pima_session);
```

## <a name="ux_host_class_pima_storage_ids_get"></a>ux_host_class_pima_storage_ids_get

Ottenere la matrice di ID di archiviazione dal risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_storage_ids_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG *storage_ids_array,
    ULONG storage_id_length)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene la matrice di ID di archiviazione dal risponditore.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima
- **storage_ids_array**: matrice in cui verranno restituiti gli ID di archiviazione
- **storage_id_length**: lunghezza dell'array di archiviazione

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) la matrice di ID archiviazione è stata popolata
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* Get the number of storage IDs. */
status = ux_host_class_pima_storage_ids_get(pima, pima_session,
    pictbridge ->ux_pictbridge_storage_ids, 64);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);

    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_storage_info_get"></a>ux_host_class_pima_storage_info_get

Ottenere le informazioni di archiviazione dal risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_storage_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    UX_HOST_CLASS_PIMA_STORAGE *storage)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene le informazioni di archiviazione per un contenitore di archiviazione di valore *storage_id*.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima
- **storage_id**: ID del contenitore di archiviazione
- **archiviazione**: puntatore al contenitore di informazioni di archiviazione

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) sono state recuperate le informazioni di archiviazione
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* Get the first storage ID info container. */
status = ux_host_class_pima_storage_info_get(pima, pima_session,
    pictbridge ->ux_pictbridge_storage_ids[0],
    (UX_HOST_CLASS_PIMA_STORAGE *)pictbridge ->ux_pictbridge_storage);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pictbridge ->
        ux_pictbridge_pima, pima_session);
    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_num_objects_get"></a>ux_host_class_pima_num_objects_get

Ottenere il numero di oggetti in un contenitore di archiviazione dal risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_num_objects_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG object_format_code)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene il numero di oggetti archiviati in un contenitore di archiviazione specifico di value storage_id corrispondente a un codice di formato specifico. Il numero di oggetti viene restituito nel campo: ux_host_class_pima_session_nb_objects della struttura di pima_session.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima
- **storage_id**: ID del contenitore di archiviazione
- **object_format_code**: filtro del codice del formato degli oggetti.

I codici di formato dell'oggetto possono avere uno dei valori seguenti.

| Codice del formato dell'oggetto               | Descrizione   |     Codice USBX                          |
|----------------------------------|---------------|------------------------------------------|
| 0x3000                           | Oggetto non definito non definito | UX_HOST_CLASS_PIMA_OFC_UNDEFINED   |
| 0x3001                           | Associazione di associazione (ad esempio, cartella) | UX_HOST_CLASS_PIMA_OFC_ASSOCIATION |
| 0x3002                           | Script del dispositivo-script specifico del modello | UX_HOST_CLASS_PIMA_OFC_SCRIPT      |
| 0x3003                           | Eseguibile binario specifico del modello di dispositivo eseguibile | UX_HOST_CLASS_PIMA_OFC_EXECUTABLE  |
| 0x3004                           | File di testo di testo  |   UX_HOST_CLASS_PIMA_OFC_TEXT        |
| 0x3005                           | File HTML HyperText Markup Language (testo) | UX_HOST_CLASS_PIMA_OFC_HTML        |
| 0x3006                           | File di formato dell'ordine di stampa digitale DPOF (testo) | UX_HOST_CLASS_PIMA_OFC_DPOF        |
| 0x3007                           | Clip audio AIFF  |  UX_HOST_CLASS_PIMA_OFC_AIFF        |
| 0x3008                           | Clip audio WAV   |  UX_HOST_CLASS_PIMA_OFC_WAV         |
| 0x3009                           | Clip audio MP3   |  UX_HOST_CLASS_PIMA_OFC_MP3         |
| 0x300A                           | Clip video AVI   |  UX_HOST_CLASS_PIMA_OFC_AVI         |
| 0x300B                           | Clip video MPEG  |  UX_HOST_CLASS_PIMA_OFC_MPEG        |
| 0x300C                           | Formato ASF Microsoft Advanced Streaming (video) | UX_HOST_CLASS_PIMA_OFC_ASF         |
| 0x3800                           | Oggetto immagine sconosciuto non definito | UX_HOST_CLASS_PIMA_OFC_QT          |
| 0x3801                           | Formato di file con scambio di formato EXIF/JPEG, JEIDA standard | UX_HOST_CLASS_PIMA_OFC_EXIF_JPEG   |
| 0x3802                           | Formato file di immagine Tag TIFF/EP per la fotografia elettronica | UX_HOST_CLASS_PIMA_OFC_TIFF_EP     |
| 0x3803                           | Formato dell'immagine di archiviazione strutturata FlashPix | UX_HOST_CLASS_PIMA_OFC_FLASHPIX    |
| 0x3804                           | File bitmap Microsoft Windows BMP | UX_HOST_CLASS_PIMA_OFC_BMP         |
| 0x3805                           | Formato file di immagine della fotocamera Canon CIFF | UX_HOST_CLASS_PIMA_OFC_CIFF        |
| 0x3806                           | Riservato non definito |  |
| 0x3807                           | Graphics Interchange Format GIF | UX_HOST_CLASS_PIMA_OFC_GIF         |
| 0x3808                           | Formato di interscambio file JPEG JFIF | UX_HOST_CLASS_PIMA_OFC_JFIF        |
| 0x3809                           | Immagine PAC PhotoCD PCD | UX_HOST_CLASS_PIMA_OFC_PCD         |
| 0x380A                           | Formato immagine rinvio PICT | UX_HOST_CLASS_PIMA_OFC_PICT        |
| 0x380B                           | Portable Network Graphics PNG | UX_HOST_CLASS_PIMA_OFC_PNG         |
| 0x380C                           | Riservato non definito |   |
| 0x380D                           | Formato file immagine Tag TIFF | UX_HOST_CLASS_PIMA_OFC_TIFF        |
| 0x380E                           | Formato file di immagine Tag TIFF/IT per Information Technology (Graphic Arts) | UX_HOST_CLASS_PIMA_OFC_TIFF_IT     |
| 0x380F                           | Formato file baseline JPEG2000 JP2 | UX_HOST_CLASS_PIMA_OFC_JP2         |
| 0x3810                           | Formato file esteso JPX JPEG2000 | UX_HOST_CLASS_PIMA_OFC_JPX         |
| Tutti gli altri codici con MSN di 0011 | Qualsiasi riservato non definito per usi futuri |                                    |
| Tutti gli altri codici con MSN di 1011 | Qualsiasi tipo definito dal fornitore definito dal fornitore: immagine |                                    |

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* Get the number of objects on all containers matching a SCRIPT object. */
status = ux_host_class_pima_num_objects_get(pima, pima_session,
    UX_PICTBRIDGE_ALL_CONTAINERS, UX_PICTBRIDGE_OBJECT_SCRIPT);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_**host_class_pima_session_close(pima, pima_session);

    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
} else
    /* The number of objects is returned in the field: pima_session -> ux_host_class_pima_session_nb_objects */
```

## <a name="ux_host_class_pima_object_handles_get"></a>ux_host_class_pima_object_handles_get

Ottenere handle di oggetto dal risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_object_handles_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG *object_handles_array,
    ULONG object_handles_length,
    ULONG storage_id,
    ULONG object_format_code,
    ULONG object_handle_association)
```

### <a name="description"></a>Descrizione

Restituisce una matrice di handle di oggetto presenti nel contenitore di archiviazione indicato dal parametro storage_id. Se si desidera un elenco aggregato in tutti i punti vendita, questo valore deve essere impostato su 0xFFFFFFFF.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima
- **object_handes_array**: matrice in cui vengono restituiti gli handle
- **object_handles_length**: lunghezza della matrice
- **storage_id**: ID del contenitore di archiviazione
- **object_format_code**: formattare il codice per l'oggetto (vedere la tabella per la funzione ux_host_class_pima_num_objects_get)
- **object_handle_association**: valore facoltativo dell'associazione di oggetti

L'associazione dell'handle di oggetto può essere uno dei valori della tabella seguente:

| AssociationCode                        | AssociationType      | Interpretazione       |
|----------------------------------------|----------------------|----------------------|
| 0x0000                                 | Non definito            | Non definito            |
| 0x0001                                 | GenericFolder        | Non utilizzato               |
| 0x0002                                 | Album                | Riservato             |
| 0x0003                                 | TimeSequence         | DefaultPlaybackDelta |
| 0x0004                                 | HorizontalPanoramic  | Non utilizzato               |
| 0x0005                                 | VerticalPanoramic    | Non utilizzato               |
| 0x0006                                 | 2DPanoramic          | ImagesPerRow         |
| 0x0007                                 | AncillaryData        | Non definito            |
| Tutti gli altri valori con bit 15 impostati su 0  | Riservato             | Non definito            |
| Tutti i valori con bit 15 impostati su 1        | Definito dal fornitore       | Definito dal fornitore       |

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* Get the array of objects handles on the container. */
status = ux_**host_class_pima_object_handles_get(pima, pima_session,
    pictbridge ->ux_pictbridge_object_handles_array,
    4 * pima_session ->ux_host_class_pima_session_nb_objects,
    UX_PICTBRIDGE_ALL_CONTAINERS,
    UX_PICTBRIDGE_OBJECT_SCRIPT, 0);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);
    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_object_info_get"></a>ux_host_class_pima_object_info_get

Ottenere le informazioni sull'oggetto dal risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_object_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene le informazioni sull'oggetto per un handle di oggetto.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima
- **object_handle**: handle dell'oggetto
- **oggetto**: puntatore al contenitore di informazioni sugli oggetti

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* We search for an object that is a picture or a script. */
object_index = 0;

while (object_index < pima_session -> ux_host_class_pima_session_nb_objects)
{
    /* Get the object info structure. */
    status = ux_**host_class_pima_object_info_get(pima, pima_session,
        pictbridge -> ux_pictbridge_object_handles_array[object_index], 
        pima_object);

    if (status != UX_SUCCESS)
    {
        /* Close the pima session. */
        status = ux_host_class_pima_session_close(pima, pima_session);

        return(UX_PICTBRIDGE_ERROR_INVALID_OBJECT_HANDLE );
    }
}
```

## <a name="ux_host_class_pima_object_info_send"></a>ux_host_class_pima_object_info_send

Invia le informazioni sull'oggetto al risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_object_info_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG parent_object_id,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Descrizione

Questa funzione Invia le informazioni di archiviazione per un contenitore di archiviazione di valore storage_id. L'initiator deve usare questo comando prima di inviare un oggetto al risponditore.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima.
- **storage_id**: ID archiviazione di destinazione.
- **parent_object_id**: ObjectHandle padre sul risponditore in cui deve essere inserito l'oggetto.
- **oggetto**: puntatore al contenitore di informazioni sugli oggetti.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* Send a script info. */
status = ux_host_class_pima_object_info_send(pima, pima_session,
    0, 0, pima_object);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);

    return(UX_ERROR);
}
```

## <a name="ux_host_class_pima_object_open"></a>ux_host_class_pima_object_open

Apre un oggetto archiviato nel risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_object_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Descrizione

Questa funzione apre un oggetto nel risponditore prima della lettura o della scrittura.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima.
- **object_handle**: handle dell'oggetto.
- **oggetto**: puntatore al contenitore di informazioni sugli oggetti.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_HOST_CLASS_PIMA_RC_OBJECT_ALREADY_OPENED**: l'oggetto (0x2021) è già aperto.
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* Open the object. */

status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_get"></a>ux_host_class_pima_object_get

Ottiene un oggetto archiviato nel risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_object_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *object_buffer,
    ULONG object_buffer_length,
    ULONG *object_actual_length)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene un oggetto nel risponditore.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima
- **object_handle**: handle dell'oggetto
- **oggetto**: puntatore al contenitore di informazioni sugli oggetti
- **object_buffer**: indirizzo dei dati oggetto
- **object_buffer_length**: lunghezza richiesta dell'oggetto
- **object_actual_length**: lunghezza dell'oggetto restituito

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) l'oggetto è stato trasferito
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) oggetto non aperto.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0X200f) accesso negato all'oggetto
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: il trasferimento (0x2007) è incompleto
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.
- **UX_TRANSFER_ERROR**: (0x23) errore di trasferimento durante la lettura dell'oggetto

### <a name="example"></a>Esempio

```C
/* Open the object. */

status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);

/* Set the object buffer pointer. */
object_buffer = pima_object ->ux_host_class_pima_object_buffer;

/* Obtain all the object data. */
while(object_length != 0)
{
    /* Calculate what length to request. */
    if (object_length > UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER)
        /* Request maximum length. */
        requested_length = UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER;
    else
        /* Request remaining length. */
        requested_length = object_length;

    /* Get the object data. */
    status = ux_host_class_pima_object_get(pima, pima_session,
        object_handle, pima_object, object_buffer,
        requested_length, &actual_length);

    if (status != UX_SUCCESS)
    {
        /* We had a problem, abort the transfer. */
        ux_host_class_pima_object_transfer_abort(pima, pima_session,
            object_handle, pima_object);

        /* And close the object. */
        ux_host_class_pima_object_close(pima, pima_session,
            object_handle, pima_object, object);

        return(status);

    }

    /* We have received some data, update the length remaining. */
    object_length -= actual_length;

    /* Update the buffer address. */
    object_buffer += actual_length;

}

/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session,
    object_handle, pima_object, object);
```

## <a name="ux_host_class_pima_object_send"></a>ux_host_class_pima_object_send

Invia un oggetto archiviato nel risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_object_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *object_buffer, ULONG object_buffer_length)
```

### <a name="description"></a>Descrizione

Questa funzione Invia un oggetto al risponditore.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_sessio**: puntatore alla sessione Pima
- **object_handle**: handle dell'oggetto
- **oggetto**: puntatore al contenitore di informazioni sugli oggetti
- **object_buffer**: indirizzo dei dati oggetto
- **object_buffer_length**: lunghezza richiesta dell'oggetto

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) oggetto non aperto.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0X200f) accesso negato all'oggetto
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: il trasferimento (0x2007) è incompleto
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.
- **UX_TRANSFER_ERROR**: (0x23) errore di trasferimento durante la scrittura dell'oggetto

### <a name="example"></a>Esempio

```C
/* Open the object. */
status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Get the object length. */
object_length = pima_object ->ux_host_class_pima_object_compressed_size;

/* Recall the object buffer address. */
pima_object_buffer = pima_object ->ux_host_class_pima_object_buffer;

/* Send all the object data. */
while(object_length != 0)
{
    /* Calculate what length to request. */
    if (object_length > UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER)
        /* Request maximum length. */
        requested_length = UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER;
    else
        /* Request remaining length. */
        requested_length = object_length;

    /* Send the object data. */
    status = ux_host_class_pima_object_send(pima,
        pima_session, pima_object,
        pima_object_buffer, requested_length);

    if (status != UX_SUCCESS)
    {
        /* Abort the transfer. */
        ux_host_class_pima_object_transfer_abort(pima, pima_session,
            object_handle, pima_object);

        /* Return status. */
        return(status);
    }

    /* We have sent some data, update the length remaining. */
    object_length -= requested_length;
}

/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session, object_handle,
    pima_object, object);
```

## <a name="ux_host_class_pima_thumb_get"></a>ux_host_class_pima_thumb_get

Ottiene un oggetto Thumb archiviato nel risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_thumb_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *thumb_buffer, ULONG thumb_buffer_length,
    ULONG *thumb_actual_length)
```

### <a name="description"></a>Descrizione

Questa funzione ottiene un oggetto Thumb sul risponditore.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima.
- **object_handle**: handle dell'oggetto.
- **oggetto**: puntatore al contenitore di informazioni sugli oggetti.
- **thumb_buffer**: indirizzo dei dati dell'oggetto Thumb.
- **thumb_buffer_length**: lunghezza richiesta dell'oggetto Thumb.
- **thumb_actual_length**: viene restituita la lunghezza dell'oggetto Thumb.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: la sessione (0x2003) non è aperta.
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) oggetto non aperto.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0X200f) accesso negato all'oggetto.
- **UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: il trasferimento (0x2007) è incompleto.
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.
- **UX_TRANSFER_ERROR**: (0x23) errore di trasferimento durante la lettura dell'oggetto.

### <a name="example"></a>Esempio

```C
/* Get the thumb object data. */

status = ux_host_class_pima_thumb_get(pima, pima_session,
    object_handle, pima_object, object_buffer,
    requested_length, &actual_length);

if (status != UX_SUCCESS)
{
    /* And close the object. */
    ux_host_class_pima_object_close(pima, pima_session, object_handle, pima_object, object);

    return(status);
}
```

## <a name="ux_host_class_pima_object_delete"></a>ux_host_class_pima_object_delete

Elimina un oggetto archiviato nel risponditore.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_object_delete(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle)
```

### <a name="description"></a>Descrizione

Questa funzione Elimina un oggetto nel risponditore

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima
- **object_handle**: handle dell'oggetto

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) l'oggetto è stato eliminato.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: la sessione (0x2003) non è aperta.
- **UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0X200f) non è possibile eliminare l'oggetto.
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* Delete the object. */
status = ux_host_class_pima_object_delete(pima, pima_session, object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_close"></a>ux_host_class_pima_object_close

Chiude un oggetto archiviato nel risponditore

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_pima_object_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle, UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a>Descrizione

Questa funzione chiude un oggetto nel risponditore.

### <a name="parameters"></a>Parametri

- **Pima**: puntatore all'istanza della classe Pima.
- **pima_session**: puntatore alla sessione Pima.
- **object_handle**: handle dell'oggetto.
- **oggetto**: puntatore all'oggetto.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) l'oggetto è stato chiuso.
- **UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: la sessione (0x2003) non è aperta.
- **UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) oggetto non aperto.
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.

### <a name="example"></a>Esempio

```C
/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session, object_handle, object);
```

## <a name="ux_host_class_gser_read"></a>ux_host_class_gser_read

Leggere dall'interfaccia seriale generica.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_gser_read(
    UX_HOST_CLASS_GSER *gser,
    ULONG interface_index,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Descrizione

Questa funzione legge dall'interfaccia seriale generica. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.

### <a name="parameters"></a>Parametri

- **gser**: puntatore all'istanza della classe gser.
- **interface_index**: Indice dell'interfaccia da cui leggere.
- **data_pointer**: puntatore all'indirizzo del buffer del payload di dati.
- **requested_length**: lunghezza da ricevere.
- **actual_length**: lunghezza effettivamente ricevuta.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, lettura incompleta.

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_gser_read(cdc_acm, interface_index,data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_write"></a>ux_host_class_gser_write

Scrivere nell'interfaccia seriale generica.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_gser_write(
    UX_HOST_CLASS_GSER *gser,
    ULONG interface_index,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a>Descrizione

Questa funzione scrive nell'interfaccia seriale generica. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.

### <a name="parameters"></a>Parametri

- **gser**: puntatore all'istanza della classe gser.
- **interface_index**: interfaccia in cui scrivere.
- **data_pointer**: puntatore all'indirizzo del buffer del payload di dati.
- **requested_length**: lunghezza da inviare.
- **actual_length**: lunghezza effettivamente inviata.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, scrittura incompleta.

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_cdc_acm_write(gser, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_ioctl"></a>ux_host_class_gser_ioctl

Eseguire una funzione IOCTL nell'interfaccia seriale generica.

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_gser_ioctl(
    UX_HOST_CLASS_GSER *gser,
    ULONG ioctl_function,
    VOID *parameter)
```

### <a name="description"></a>Descrizione

Questa funzione esegue una specifica funzione IOCTL per l'interfaccia gser. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il comando viene completato.

### <a name="parameters"></a>Parametri

- **gser**: puntatore all'istanza della classe gser.
- **ioctl_function**: funzione IOCTL da eseguire. Vedere la tabella seguente per una delle funzioni IOCTL consentite.
- **parametro**: Pointerto un parametro specifico per IOCTL

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.
- **UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente.
- **UX_HOST_CLASS_UNKNOWN**: (0x59) istanza di classe errata
- **UX_FUNCTION_NOT_SUPPORTED**: (0x54) funzione IOCTL sconosciuta.

### <a name="ioctl-functions"></a>Funzioni IOCTL

- UX_HOST_CLASS_GSER_IOCTL_SET_LINE_CODING
- UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING
- UX_HOST_CLASS_GSER_IOCTL_SET_LINE_STATE
- UX_HOST_CLASS_GSER_IOCTL_SEND_BREAK
- UX_HOST_CLASS_GSER_IOCTL_ABORT_IN_PIPE
- UX_HOST_CLASS_GSER_IOCTL_ABORT_OUT_PIPE
- UX_HOST_CLASS_GSER_IOCTL_NOTIFICATION_CALLBACK
- UX_HOST_CLASS_GSER_IOCTL_GET_DEVICE_STATUS

### <a name="example"></a>Esempio

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_gser_ioctl(gser,
    UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING,
    (VOID *)&line_coding);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_reception_start"></a>ux_host_class_gser_reception_start

Avviare la ricezione sull'interfaccia seriale generica

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_gser_reception_start(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a>Descrizione

Questa funzione avvia la ricezione sull'interfaccia della classe seriale generica. Questa funzione consente la ricezione senza blocco. Quando viene ricevuto un buffer, viene richiamato un callback nell'applicazione.

### <a name="parameters"></a>Parametri

- **gser** Puntatore all'istanza della classe gser.
- **gser_reception** Struttura che contiene i parametri di ricezione

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.
- Istanza di classe non corretta **UX_HOST_CLASS_UNKNOWN** (0x59)
- Errore **UX_ERROR** (0x01)

### <a name="example"></a>Esempio

```C
/* Start the reception for gser. AT commands are on interface 2. */
gser_reception.ux_host_class_gser_reception_interface_index =
    UX_DEMO_GSER_AT_INTERFACE;
gser_reception.ux_host_class_gser_reception_block_size =
    UX_DEMO_RECEPTION_BLOCK_SIZE;
gser_reception.ux_host_class_gser_reception_data_buffer =
    gser_reception_buffer;
gser_reception.ux_host_class_gser_reception_data_buffer_size =
    UX_DEMO_RECEPTION_BUFFER_SIZE;
gser_reception.ux_host_class_gser_reception_callback =
    tx_demo_thread_callback;

ux_host_class_gser_reception_start(gser, &gser_reception);
```

## <a name="ux_host_class_gser_reception_stop"></a>ux_host_class_gser_reception_stop

Arrestare la ricezione sull'interfaccia seriale generica

### <a name="prototype"></a>Prototipo

```C
UINT ux_host_class_gser_reception_stop(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a>Descrizione

Questa funzione arresta la ricezione sull'interfaccia della classe seriale generica.

### <a name="parameters"></a>Parametri

- **gser** Puntatore all'istanza della classe gser.
- **gser_reception** Struttura che contiene i parametri di ricezione

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.
- Istanza di classe non corretta **UX_HOST_CLASS_UNKNOWN** (0x59)
- Errore **UX_ERROR** (0x01)

### <a name="example"></a>Esempio

```C
/* Stops the reception for gser. */
ux_host_class_gser_reception_stop(gser, &gser_reception);
```
