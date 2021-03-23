---
title: Capitolo 5-API delle classi host USBX
description: Informazioni sulle API delle classi host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: bf5876042e08a59979adcd429917bfc3fbfdbc20
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824524"
---
# <a name="chapter-5---usbx-host-classes-api"></a>Capitolo 5-API delle classi host USBX

In questo capitolo vengono illustrate tutte le API esposte delle classi host USBX. Le API seguenti per ogni classe sono descritte in dettaglio.

- Classe HID
- CDC-ACM (classe)
- Classe CDC-ECM
- Classe di archiviazione

## <a name="ux_host_class_hid_client_register"></a>ux_host_class_hid_client_register

Registrare un client nascosto nella classe HID.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_client_register(
    UCHAR *hid_client_name,
    UINT (*hid_client_handler)
    (struct UX_HOST_CLASS_HID_CLIENT_COMMAND_STRUCT *));
```

### <a name="description"></a>Descrizione

Questa funzione viene utilizzata per registrare un client nascosto nella classe HID. La classe HID deve trovare una corrispondenza tra un dispositivo HID e un client nascosto prima di richiedere i dati da questo dispositivo.

> [!NOTE]
> La stringa C di hid_client_name deve essere con terminazione NULL e la lunghezza (senza il carattere di terminazione NULL) non deve essere maggiore di **UX_HOST_CLASS_HID_MAX_CLIENT_NAME_LENGTH**.

### <a name="parameters"></a>Parametri

- **hid_client_name** Puntatore al nome del client HID.
- **hid_client_handler** Puntatore al gestore client nascosto.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato
- L'allocazione di memoria **UX_MEMORY_INSUFFICIENT** (0x12) per il client non è riuscita.
- Il numero massimo di client **UX_MEMORY_ARRAY_FULL** (0x1A) è già registrato.
- **UX_HOST_CLASS_ALREADY_INSTALLED** (0X58) questa classe esiste già

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates how to register a HID client, in
this case a USB mouse, to the HID class. */

status = ux_host_class_hid_client_register("ux_host_class_hid_client_mouse",
    ux_host_class_hid_mouse_entry);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_callback_register"></a>ux_host_class_hid_report_callback_register

Registrare un callback dalla classe HID.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_report_callback_register(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_REPORT_CALLBACK *call_back);
```

### <a name="description"></a>Descrizione

Questa funzione viene utilizzata per registrare un callback dalla classe HID al client HID quando viene ricevuto un report.

### <a name="parameters"></a>Parametri

- **nascosto** Puntatore all'istanza della classe HID
- **call_back** Puntatore alla struttura call_back

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) istanza HID non valida.
- Errore **UX_HOST_CLASS_HID_REPORT_ERROR** (0x79) nella registrazione del callback del report.

### <a name="example"></a>Esempio

```c
UINT status;

/* This example illustrates how to register a HID client, in this case a USB mouse, to the HID class. In this case, the HID client is asking the HID class to call the client for each usage received in the HID report. */

call_back.ux_host_class_hid_report_callback_id = 0;
call_back.ux_host_class_hid_report_callback_function = ux_host_class_hid_mouse_callback;

call_back.ux_host_class_hid_report_callback_buffer = UX_NULL;
call_back.ux_host_class_hid_report_callback_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

call_back.ux_host_class_hid_report_callback_length = 0;

status = ux_host_class_hid_report_callback_register(hid, &call_back);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_periodic_report_start"></a>ux_host_class_hid_periodic_report_start

Avviare l'endpoint periodico per un'istanza della classe HID.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_periodic_report_start(UX_HOST_CLASS_HID *hid);
```

### <a name="description"></a>Descrizione

Questa funzione viene utilizzata per avviare l'endpoint periodico (interrupt) per l'istanza della classe HID associata a questo client nascosto. La classe HID non può avviare l'endpoint periodico finché il client HID non viene attivato e pertanto viene lasciato al client HID per avviare l'endpoint per la ricezione dei report.

### <a name="input-parameter"></a>Parametro di input

- **nascosto** Puntatore all'istanza della classe HID.

### <a name="return-values"></a>Valori restituiti

- Creazione di report periodici **UX_SUCCESS** (0x00) avviata correttamente.
- Errore **ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) nel rapporto periodico.
- L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates how to start the periodic
endpoint. */

status = ux_host_class_hid_periodic_report_start(hid);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_periodic_report_stop"></a>ux_host_class_hid_periodic_report_stop

Arrestare l'endpoint periodico per un'istanza della classe HID.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_periodic_report_stop(UX_HOST_CLASS_HID *hid);
```

### <a name="description"></a>Descrizione

Questa funzione viene utilizzata per arrestare l'endpoint periodico (interrupt) per l'istanza della classe HID associata a questo client nascosto. La classe HID non può arrestare l'endpoint periodico finché il client HID non viene disattivato, tutte le relative risorse vengono liberate e pertanto viene lasciato al client nascosto per arrestare l'endpoint.

### <a name="input-parameter"></a>Parametro di input

- **nascosto** Puntatore all'istanza della classe HID.

### <a name="return-values"></a>Valori restituiti

- Report periodici di **UX_SUCCESS** (0x00) arrestato correttamente.
- Errore **ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) nel rapporto periodico.
- L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates how to stop the periodic endpoint. */

status = ux_host_class_hid_periodic_report_stop(hid);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_get"></a>ux_host_class_hid_report_get

Ottenere un report da un'istanza della classe HID.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_report_get(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_CLIENT_REPORT *client_report);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata per ricevere un report direttamente dal dispositivo senza basarsi sull'endpoint periodico. Questo report è proveniente dall'endpoint di controllo, ma il suo trattamento è identico a quello che era in arrivo nell'endpoint periodico.

### <a name="parameters"></a>Parametri

- **nascosto** Puntatore all'istanza della classe HID.
- **client_report** Puntatore al report client nascosto.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il report è stato ricevuto correttamente.
- **UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) il report del client non è valido o si è verificato un errore durante il trasferimento.
- L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.
- **UX_BUFFER_OVERFLOW** (0X5d) il buffer fornito non è sufficientemente grande da contenere il report non compresso.

### <a name="example"></a>Esempio

```c
UX_HOST_CLASS_HID_CLIENT_REPORT input_report;

UINT status;

/* The following example illustrates how to get a report. */

input_report.ux_host_class_hid_client_report = hid_report;
input_report.ux_host_class_hid_client_report_buffer = buffer;
input_report.ux_host_class_hid_client_report_length = length;
input_report.ux_host_class_hid_client_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

status = ux_host_class_hid_report_get(hid, &input_report);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_set"></a>ux_host_class_hid_report_set

Inviare un report

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_report_set(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_CLIENT_REPORT *client_report);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata per inviare un report direttamente al dispositivo.

### <a name="parameters"></a>Parametri

- **nascosto** Puntatore all'istanza della classe HID.
- **client_report** Puntatore al report client nascosto.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il report è stato inviato correttamente.
- **UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) il report del client non è valido o si è verificato un errore durante il trasferimento.
- L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.
- **UX_HOST_CLASS_HID_REPORT_OVERFLOW** (0X5d) il buffer fornito non è sufficientemente grande da contenere il report non compresso.

### <a name="example"></a>Esempio

```c
/* The following example illustrates how to send a report. */

UX_HOST_CLASS_HID_CLIENT_REPORT input_report;

input_report.ux_host_class_hid_client_report = hid_report;
input_report.ux_host_class_hid_client_report_buffer = buffer;
input_report.ux_host_class_hid_client_report_length = length;
input_report.ux_host_class_hid_client_report_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

status = ux_host_class_hid_report_set(hid, &input_report);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_mouse_buttons_get"></a>ux_host_class_hid_mouse_buttons_get

Ottenere i pulsanti del mouse.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_mouse_buttons_get(
    UX_HOST_CLASS_HID_MOUSE *mouse_instance,
    ULONG *mouse_buttons);
```

### <a name="description"></a>Descrizione

Questa funzione viene utilizzata per ottenere i pulsanti del mouse

### <a name="parameters"></a>Parametri

- **mouse_instance** Puntatore all'istanza del mouse HID.
- **mouse_buttons** Puntatore ai pulsanti restituiti.

### <a name="return-values"></a>Valori restituiti

- Il pulsante del mouse **UX_SUCCESS** (0x00) è stato recuperato.
- L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.

### <a name="example"></a>Esempio

```c
/* The following example illustrates how to obtain mouse buttons. */

UX_HOST_CLASS_HID_MOUSE *mouse_instance;

ULONG mouse_buttons;

status = ux_host_class_hid_mouse_button_get(mouse_instance, &mouse_buttons);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_mouse_position_get"></a>ux_host_class_hid_mouse_position_get

Ottiene la posizione del mouse.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_mouse_position_get(
    UX_HOST_CLASS_HID_MOUSE *mouse_instance,
    SLONG *mouse_x_position, 
    SLONG *mouse_y_position);
```

### <a name="description"></a>Descrizione

Questa funzione viene utilizzata per ottenere la posizione del mouse in coordinate x & y.

### <a name="parameters"></a>Parametri

- **mouse_instance** Puntatore all'istanza del mouse HID.
- **mouse_x_position** Puntatore alla coordinata x.
- **mouse_y_position** Puntatore alla coordinata y.

### <a name="return-values"></a>Valori restituiti

- Sono state recuperate le coordinate di **UX_SUCCESS** (0x00) X &amp; Y.
- L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.

### <a name="example"></a>Esempio

```c
/* The following example illustrates how to obtain mouse coordinates. */

UX_HOST_CLASS_HID_MOUSE *mouse_instance;

SLONG mouse_x_position;
SLONG mouse_y_position;

status = ux_host_class_hid_mouse_position_get(mouse_instance,
    &mouse_x_position, &mouse_y_position);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_keyboard_key_get"></a>ux_host_class_hid_keyboard_key_get

Ottenere la chiave e lo stato della tastiera.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_keyboard_key_get(
    UX_HOST_CLASS_HID_KEYBOARD *keyboard_instance,
    ULONG *keyboard_key, 
    ULONG *keyboard_state);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata per ottenere il tasto e lo stato della tastiera.

### <a name="parameters"></a>Parametri

- **keyboard_instance** Puntatore all'istanza della tastiera HID.
- **keyboard_key** Puntatore al contenitore di tasti della tastiera.
- **keyboard_state** Puntatore al contenitore dello stato della tastiera.

### <a name="return-values"></a>Valori restituiti

- La chiave e lo stato di **UX_SUCCESS** (0x00) sono stati recuperati correttamente.
- **UX_ERROR** (0Xff) nulla da segnalare.
- L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.

Lo stato della tastiera può includere i valori seguenti.

- **UX_HID_KEYBOARD_STATE_KEY_UP** 0x10000
- **UX_HID_KEYBOARD_STATE_NUM_LOCK** 0x0001
- **UX_HID_KEYBOARD_STATE_CAPS_LOCK** 0x0002
- **UX_HID_KEYBOARD_STATE_SCROLL_LOCK** 0x0004
- **UX_HID_KEYBOARD_STATE_MASK_LOCK** 0x0007
- **UX_HID_KEYBOARD_STATE_LEFT_SHIFT** 0x0100
- **UX_HID_KEYBOARD_STATE_RIGHT_SHIFT** 0x0200
- **UX_HID_KEYBOARD_STATE_SHIFT** 0x0300
- **UX_HID_KEYBOARD_STATE_LEFT_ALT** 0x0400
- **UX_HID_KEYBOARD_STATE_RIGHT_ALT** 0x0800
- **UX_HID_KEYBOARD_STATE_ALT** 0x0A00
- **UX_HID_KEYBOARD_STATE_LEFT_CTRL** 0x1000
- **UX_HID_KEYBOARD_STATE_RIGHT_CTRL** 0x2000
- **UX_HID_KEYBOARD_STATE_CTRL** 0x3000
- **UX_HID_KEYBOARD_STATE_LEFT_GUI** 0x4000
- **UX_HID_KEYBOARD_STATE_RIGHT_GUI** 0x8000
- **UX_HID_KEYBOARD_STATE_GUI** 0xA000

### <a name="example"></a>Esempio

```c
while (1)
{

    /* Get a key/state from the keyboard. */
    status = ux_host_class_hid_keyboard_key_get(keyboard,
        &keyboard_char, &keyboard_state);

    /* Check if there is something. */
    if (status == UX_SUCCESS)
    {

        #ifdef UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE
            if (keyboard_state & UX_HID_KEYBOARD_STATE_KEY_UP)
            {
                /* The key was released. */
            } else
            {
                /* The key was pressed. */
            }
        #endif

        /* We have a character in the queue. */
        keyboard_queue[keyboard_queue_index] = (UCHAR) keyboard_char;

        /* Can we accept more ? */
        if(keyboard_queue_index < 1024)
            keyboard_queue_index++;
    }

    tx_thread_sleep(10);

}
```

## <a name="ux_host_class_hid_keyboard_ioctl"></a>ux_host_class_hid_keyboard_ioctl

Eseguire una funzione IOCTL sulla tastiera HID.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_keyboard_ioctl(
    UX_HOST_CLASS_HID_KEYBOARD *keyboard_instance,
    ULONG ioctl_function, VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione esegue una specifica funzione IOCTL sulla tastiera HID. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il comando viene completato.

### <a name="parameters"></a>Parametri

- **keyboard_instance** Puntatore all'istanza della tastiera HID.
- **ioctl_function** funzione IOCTL da eseguire. Vedere la tabella seguente per una delle funzioni IOCTL consentite.
- **parametro** di Puntatore a un parametro specifico del comando IOCTL.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) la funzione IOCTL è stata completata correttamente.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) funzione IOCTL sconosciuta

### <a name="ioctl-functions"></a>Funzioni IOCTL

- UX_HID_KEYBOARD_IOCTL_SET_LAYOUT
- UX_HID_KEYBOARD_IOCTL_KEY_DECODING_ENABLE
- UX_HID_KEYBOARD_IOCTL_KEY_DECODING_DISABLE

### <a name="example--change-keyboard-layout"></a>Esempio: modificare il layout della tastiera

```c
UINT status;

/* This example shows usage of the SET_LAYOUT IOCTL function.
    USBX receives raw key values from the device (these raw values
    are defined in the HID usage table specification) and optionally
    decodes them for application usage. The decoding is performed
    based on a set of arrays that act as maps – which array is used
    depends on the raw key value (i.e. keypad and non-keypad) and
    the current state of the keyboard (i.e. shift, caps lock, etc.). */

/* When the shift condition is not present and the raw key value
    is not within the keypad value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_unshifted_map[] =
{
    0,0,0,0,
    'a','b','c','d','e','f','g',
    'h','i','j','k','l','m','n',
    'o','p','q','r','s','t',
    'u','v','w','x','y','z',
    '1','2','3','4','5','6','7','8','9','0',
    0x0d,0x1b,0x08,0x07,0x20,'-','=','[',']',
    '\\','#',';',0x27,'`',',','.','/',0xf0,
    0xbb,0xbc,0xbd,0xbe,0xbf,0xc0,0xc1,0xc2,0xc3,0xc4,0xc5,0xc6,
    0x00,0xf1,0x00,0xd2,0xc7,0xc9,0xd3,0xcf,0xd1,0xcd,0xcd,0xd0,0xc8,0xf2,
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
    0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
};

/* When the shift condition is present and the raw key value
    is not within the keypad value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_shifted_map[] =
{
    0,0,0,0,
    'A','B','C','D','E','F','G',
    'H','I','J','K','L','M','N',
    'O','P','Q','R','S','T',
    'U','V','W','X','Y','Z',
    '!','@','#','$','%','^','&','*','(',')',
    0x0d,0x1b,0x08,0x07,0x20,'_','+','{','}',
    '|','~',':','"','~','<','>','?',0xf0,
    0xbb,0xbc,0xbd,0xbe,0xbf,0xc0,0xc1,0xc2,0xc3,0xc4,0xc5,0xc6,
    0x00,0xf1,0x00,0xd2,0xc7,0xc9,0xd3,0xcf,0xd1,0xcd,0xcd,0xd0,0xc8,0xf2,
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
    0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
};

/* When numlock is on and the raw key value is within the keypad
    value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_numlock_on_map[] =
{
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
};

/* When numlock is off and the raw key value is within the keypad value
    range, this array will be used to decode the raw key value. */
static UCHAR keyboard_layout_raw_to_numlock_off_map[] =
{
    '/','*','-','+',
    0x0d,0xcf,0xd0,0xd1,0xcb,'5',0xcd,0xc7,0xc8,0xc9,0xd2,0xd3,'\\',0x00,0x
    00,'=',
};

/* Specify the keyboard layout for USBX usage. */
static UX_HOST_CLASS_HID_KEYBOARD_LAYOUT keyboard_layout =
{
    keyboard_layout_raw_to_shifted_map,
    keyboard_layout_raw_to_unshifted_map,
    keyboard_layout_raw_to_numlock_on_map,
    keyboard_layout_raw_to_numlock_off_map,
    /* The maximum raw key value. Values larger than this are discarded. */
    UX_HID_KEYBOARD_KEYS_UPPER_RANGE,
    /* The raw key value for the letter 'a'. */
    UX_HID_KEYBOARD_KEY_LETTER_A,
    /* The raw key value for the letter 'z'. */
    UX_HID_KEYBOARD_KEY_LETTER_Z,
    /* The lower range raw key value for keypad keys - inclusive. */
    UX_HID_KEYBOARD_KEYS_KEYPAD_LOWER_RANGE,
    /* The upper range raw key value for keypad keys. */
    UX_HID_KEYBOARD_KEYS_KEYPAD_UPPER_RANGE
};

/* Call the IOCTL function to change the keyboard layout. */
status = ux_host_class_hid_keyboard_ioctl(keyboard,
    UX_HID_KEYBOARD_IOCTL_SET_LAYOUT, (VOID *)&keyboard_layout);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="example--disable-keyboard-key-decode"></a>Esempio: disabilitare la decodifica del tasto tastiera

```c
UINT status;

/* The following example illustrates IOCTL function of Disable key decode from keyboard layout. */
status = ux_host_class_hid_keyboard_ioctl(keyboard,
    UX_HID_KEYBOARD_IOCTL_DISABLE_KEYS_DECODE, UX_NULL);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_remote_control_usage_get"></a>ux_host_class_hid_remote_control_usage_get

Ottenere l'utilizzo del controllo remoto

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_hid_remote_control_usage_get(
    UX_HOST_CLASS_HID_REMOTE_CONTROL *remote_control_instance,
    LONG *usage, 
    ULONG *value);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata per ottenere gli utilizzi del controllo remoto.

### <a name="parameters"></a>Parametri

- **remote_control_instance** Puntatore all'istanza di controllo remoto HID.
- **utilizzo** di Puntatore all'utilizzo.
- **valore** di Puntatore al valore per l'utilizzo.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.
- **UX_ERROR** (0Xff) nulla da segnalare.
- L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.

L'elenco di tutti gli utilizzi possibili è troppo lungo per questo manuale dell'utente. Per una descrizione completa, il ux_host_class_hid. h include l'intero set di valori possibili.

### <a name="example"></a>Esempio

```c
/* Read usages and values as the user changes the vol/bass/treble buttons on the speaker */

while (remote_control != UX_NULL)
{
    status = ux_host_class_hid_remote_control_usage_get(remote_control, &usage, &value);
    if (status == UX_SUCCESS)
    {
        /* We have something coming from the HID remote control,
        we filter the usage here and only allow the
        volume usage which can be VOLUME, VOLUME_INCREMENT or VOLUME_DECREMENT */
        switch(usage)
        {
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME :
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME_INCREMENT :
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME_DECREMENT :

            if (value<0x80)
            {
                if (current_volume + audio_control.ux_host_class_audio_control_res < 0xffff)
                    current_volume = current_volume + audio_control.ux_host_class_audio_control_res;
                } else {
                if (current_volume > audio_control.ux_host_class_audio_control_res)
                    current_volume = current_volumeaudio_control.ux_host_class_audio_control_res;
            }

            audio_control.ux_host_class_audio_control_channel = 1;
            audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
            audio_control.ux_host_class_audio_control_cur = current_volume;
            status = ux_host_class_audio_control_value_set(audio, &audio_control);
            audio_control.ux_host_class_audio_control_channel = 2;
            audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
            audio_control.ux_host_class_audio_control_cur = current_volume;
            status = ux_host_class_audio_control_value_set(audio, &audio_control);
            break;

        }
    }
    tx_thread_sleep(10);

}
```

### <a name="ux_host_class_cdc_acm_read"></a>ux_host_class_cdc_acm_read

Leggere dall'interfaccia cdc_acm.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_cdc_acm_read(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length);
```

### <a name="description"></a>Descrizione

Questa funzione legge dall'interfaccia cdc_acm. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.

### <a name="parameters"></a>Parametri

- **cdc_acm** Puntatore all'istanza della classe cdc_acm.
- **data_pointer** Puntatore all'indirizzo del buffer del payload di dati.
- **requested_length** Lunghezza da ricevere.
- **actual_length** Lunghezza effettivamente ricevuta.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5b) l'istanza di cdc_acm non è valida.
- TIMEOUT di trasferimento **UX_TRANSFER_TIMEOUT** (0x5c), lettura incompleta.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_read(cdc_acm, data_pointer,
    requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_write"></a>ux_host_class_cdc_acm_write

Scrivere nell'interfaccia cdc_acm

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_cdc_acm_write(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UCHAR *data_pointer, 
    ULONG requested_length, 
    ULONG *actual_length);
```

### <a name="description"></a>Descrizione

Questa funzione scrive nell'interfaccia cdc_acm. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.

### <a name="parameters"></a>Parametri

- **cdc_acm** Puntatore all'istanza della classe cdc_acm.
- **data_pointer** Puntatore all'indirizzo del buffer del payload di dati.
- **requested_length** Lunghezza da inviare.
- **actual_length** Lunghezza effettivamente inviata.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5b) l'istanza di cdc_acm non è valida.
- TIMEOUT di trasferimento **UX_TRANSFER_TIMEOUT** (0x5c), scrittura incompleta.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_write(cdc_acm, data_pointer,
    requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_ioctl"></a>ux_host_class_cdc_acm_ioctl

Eseguire una funzione IOCTL nell'interfaccia cdc_acm.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_cdc_acm_ioctl(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function, 
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione esegue una specifica funzione IOCTL nell'interfaccia cdc_acm. La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il comando viene completato.

### <a name="parameters"></a>Parametri

- **cdc_acm** Puntatore all'istanza della classe cdc_acm.
- **ioctl_function** funzione IOCTL da eseguire. Vedere la tabella seguente per una delle funzioni IOCTL consentite.
- **parametro** di Puntatore a un parametro specifico di IOCTL

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.
- **UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente.
- L'istanza di **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) CDC-ACM è in uno stato non valido.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) funzione IOCTL sconosciuta.

### <a name="ioctl-functions"></a>Funzioni IOCTL:

- UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING
- UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING
- UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE
- UX_HOST_CLASS_CDC_ACM_IOCTL_SEND_BREAK
- UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_IN_PIPE
- UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_OUT_PIPE
- UX_HOST_CLASS_CDC_ACM_IOCTL_NOTIFICATION_CALLBACK
- UX_HOST_CLASS_CDC_ACM_IOCTL_GET_DEVICE_STATUS

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_ioctl(cdc_acm,
    UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING, (VOID *)&line_coding);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_reception_start"></a>ux_host_class_cdc_acm_reception_start

Inizia la ricezione in background dei dati dal dispositivo.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_cdc_acm_reception_start(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UX_HOST_CLASS_CDC_ACM_RECEPTION *cdc_acm_reception);
```

### <a name="description"></a>Descrizione

Questa funzione fa in modo che USBX legga continuamente i dati dal dispositivo in background. Al completamento di ogni transazione, viene richiamato il callback specificato in **cdc_acm_reception** , in modo che l'applicazione possa eseguire un'ulteriore elaborazione dei dati della transazione.

> [!NOTE]
> non è necessario usare **ux_host_class_cdc_acm_read** mentre è in uso la ricezione in background.

### <a name="parameters"></a>Parametri

- **cdc_acm** Puntatore all'istanza della classe cdc_acm.
- **cdc_acm_reception** Puntatore al parametro che contiene i valori che definiscono il comportamento della ricezione in background. Il layout di questo parametro è il seguente:

```c
typedef struct UX_HOST_CLASS_CDC_ACM_RECEPTION_STRUCT
{
    ULONG ux_host_class_cdc_acm_reception_state;
    ULONG ux_host_class_cdc_acm_reception_block_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_buffer;
    ULONG ux_host_class_cdc_acm_reception_data_buffer_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_head;
    UCHAR *ux_host_class_cdc_acm_reception_data_tail;
    VOID (*ux_host_class_cdc_acm_reception_callback)(struct UX_HOST_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, UCHAR *reception_buffer, ULONG reception_size);
} UX_HOST_CLASS_CDC_ACM_RECEPTION;
```

### <a name="return-value"></a>Valore restituito

- Ricezione in background **UX_SUCCESS** (0x00) avviata correttamente.
- Istanza di classe non corretta **UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b).

```c
UINT status;
UX_HOST_CLASS_CDC_ACM_RECEPTION cdc_acm_reception;

/* Setup the background reception parameter. */

/* Set the desired max read size for each transaction.
    For example, if this value is 64, then the maximum amount of
    data received from the device in a single transaction is 64.
    If the amount of data received from the device is less than this value,
    the callback will still be invoked with the actual amount of data received. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_block_size = block_size;

/* Set the buffer where the data from the device is read to. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_data_buffer = cdc_acm_reception_buffer;

/* Set the size of the data reception buffer.
    Note that this should be at least as large as ux_host_class_cdc_acm_reception_block_size. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_data_buffer_size = cdc_acm_reception_buffer_size;

/* Set the callback that is to be invoked upon each reception transfer completion. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_callback = reception_callback;

/* Start background reception using the values we defined in the reception parameter. */
status = ux_host_class_cdc_acm_reception_start(cdc_acm_host_data, &cdc_acm_reception);

/* If status equals UX_SUCCESS, background reception has successfully started. */
```

## <a name="ux_host_class_cdc_acm_reception_stop"></a>ux_host_class_cdc_acm_reception_stop

Arresta la ricezione dei pacchetti in background.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_class_cdc_acm_reception_stop(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UX_HOST_CLASS_CDC_ACM_RECEPTION *cdc_acm_reception);
```

### <a name="description"></a>Descrizione

Questa funzione fa in modo che USBX arresti la ricezione in background avviata in precedenza da **ux_host_class_cdc_acm_reception_start**.

### <a name="parameters"></a>Parametri

- **cdc_acm** Puntatore all'istanza della classe cdc_acm.
- **cdc_acm_reception** Puntatore allo stesso parametro utilizzato per avviare la ricezione in background. Il layout di questo parametro è il seguente:

```c
typedef struct UX_HOST_CLASS_CDC_ACM_RECEPTION_STRUCT
{
    ULONG ux_host_class_cdc_acm_reception_state;
    ULONG ux_host_class_cdc_acm_reception_block_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_buffer;
    ULONG ux_host_class_cdc_acm_reception_data_buffer_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_head;
    UCHAR *ux_host_class_cdc_acm_reception_data_tail;
    VOID (*ux_host_class_cdc_acm_reception_callback)(
            struct UX_HOST_CLASS_CDC_ACM_STRUCT *cdc_acm, UINT status,
            UCHAR *reception_buffer, ULONG reception_size);
} UX_HOST_CLASS_CDC_ACM_RECEPTION;
```

### <a name="return-value"></a>Valore restituito

- La ricezione in background **UX_SUCCESS** (0x00) è stata arrestata.
- Istanza di classe non corretta **UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b).

```c
UINT status;
UX_HOST_CLASS_CDC_ACM_RECEPTION cdc_acm_reception;

/* Stop background reception. The reception parameter should be the same
    that was passed to ux_host_class_cdc_acm_reception_start. */
status = ux_host_class_cdc_acm_reception_stop(cdc_acm, &cdc_acm_reception);

/* If status equals UX_SUCCESS, background reception has successfully stopped. */
```
