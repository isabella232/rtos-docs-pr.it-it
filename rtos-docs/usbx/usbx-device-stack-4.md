---
title: Capitolo 4 - Descrizione di Servizi dispositivo USBX
description: Informazioni su USBX Device Services.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9d88d9bd177a251a00fec6757fc1f1494b56bab9655a55f973481f273f0683ee
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797552"
---
# <a name="description-of-usbx-device-services"></a>Descrizione di Servizi dispositivo USBX

### <a name="ux_device_stack_alternate_setting_get"></a>ux_device_stack_alternate_setting_get

Ottenere l'impostazione alternativa corrente per un valore di interfaccia

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_alternate_setting_get(ULONG interface_value);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata dall'host USB per ottenere l'impostazione alternativa corrente per un valore di interfaccia specifico. Viene chiamato dal driver del controller quando viene **ricevuta GET_INTERFACE** richiesta.

### <a name="input-parameter"></a>Parametro di input

- **Interface_value** Valore dell'interfaccia per cui viene eseguita una query sull'impostazione alternativa corrente

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il trasferimento dei dati è stato completato.
- **UX_ERROR** (0xFF) Valore di interfaccia errato.

### <a name="example"></a>Esempio

```c
ULONG interface_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_alternate_setting_set"></a>ux_device_stack_alternate_setting_set

Impostare l'impostazione alternativa corrente per un valore di interfaccia

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_alternate_setting_set(
    ULONG interface_value, 
    ULONG alternate_setting_value);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata dall'host USB per impostare l'impostazione alternativa corrente per un valore di interfaccia specifico. Viene chiamato dal driver del controller quando viene **ricevuta SET_INTERFACE** richiesta. Quando la **SET_INTERFACE** viene completata, i valori delle impostazioni alternative vengono applicati alla classe .

Lo stack di dispositivi emettere **un UX_SLAVE_CLASS_COMMAND_CHANGE** alla classe proprietaria di questa interfaccia per riflettere la modifica dell'impostazione alternativa.

### <a name="parameters"></a>Parametri

- **interface_value:** valore dell'interfaccia per cui è impostata l'impostazione alternativa corrente.
- **alternate_setting_value**: nuovo valore dell'impostazione alternativa.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il trasferimento dei dati è stato completato.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) Nessuna interfaccia collegata.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) non è configurato.
- **UX_ERROR** (0xFF) Valore di interfaccia errato.

### <a name="example"></a>Esempio

```c
ULONG interface_value;

ULONG alternate_setting_value;

/* The following example illustrates this service. */
status = ux_device_stack_alternate_setting_set(interface_value, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_class_register"></a>ux_device_stack_class_register

Registrare una nuova classe di dispositivi USB

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT *),
    ULONG configuration_number, 
    ULONG interface_number,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata dall'applicazione per registrare una nuova classe di dispositivi USB. Questa registrazione avvia un contenitore di classi e non un'istanza della classe . Una classe deve avere un thread attivo ed essere collegata a un'interfaccia specifica.

Alcune classi prevedono un elenco di parametri o parametri. Ad esempio, la classe di archiviazione del dispositivo si aspetta la geometria del dispositivo di archiviazione che sta tentando di emulare. Il campo del parametro dipende quindi dal requisito della classe e può essere un valore o un puntatore a una struttura riempita con i valori della classe.

> [!NOTE]
> La stringa C di class_name deve avere terminazione NULL e la sua lunghezza (senza il carattere di terminazione NULL stesso) non deve essere maggiore **di UX_MAX_CLASS_NAME_LENGTH**.

### <a name="parameters"></a>Parametri

- **class_name** Nome classe
- **class_entry_function** Funzione entry della classe.
- **configuration_number** Numero di configurazione a cui è collegata questa classe.
- **interface_number** Numero di interfaccia a cui è collegata questa classe.
- **parametro** Puntatore a un elenco di parametri specifico della classe.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) La classe è stata registrata
- **UX_MEMORY_INSUFFICIENT** (0x12) Nella tabella di classi non è stata lasciata alcuna voce.
- **UX_THREAD_ERROR** (0x16) Impossibile creare un thread di classe.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */

/* Initialize the device storage class. The class is connected with interface 1 */
status = ux_device_stack_class_register(_ux_system_slave_class_storage_name ux_device_class_storage_entry,
    1, 1, (VOID *)&parameter);
```

### <a name="ux_device_stack_class_unregister"></a>ux_device_stack_class_unregister

Annullare la registrazione di una classe di dispositivi USB

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_class_unregister(
    UCHAR *class_name,
    UINT (*class_entry_function)(struct UX_SLAVE_CLASS_COMMAND_STRUCT*));
```

### <a name="description"></a>Descrizione

Questa funzione viene usata dall'applicazione per annullare la registrazione di una classe di dispositivo USB.

> [!NOTE]
> La stringa C di class_name deve avere terminazione NULL e la sua lunghezza (senza il carattere di terminazione NULL stesso) non deve essere maggiore **di UX_MAX_CLASS_NAME_LENGTH**.

### <a name="parameters"></a>Parametri

- **class_name**: Nome classe
- **class_entry_function**: funzione entry della classe .

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) La registrazione della classe è stata annullata.
- **UX_NO_CLASS_MATCH** (0x57) La classe non è registrata.

### <a name="example"></a>Esempio

```c
/* The following example illustrates this service. */

/* Unitialize the device storage class. */
status = ux_device_stack_class_unregister(_ux_system_slave_class_storage_name, ux_device_class_storage_entry);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_get"></a>ux_device_stack_configuration_get

Ottenere la configurazione corrente

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_configuration_get(VOID);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata dall'host per ottenere la configurazione corrente in esecuzione nel dispositivo.

### <a name="input-parameter"></a>Parametro di input

Nessuno

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) Il trasferimento dei dati è stato completato.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_get();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_configuration_set"></a>ux_device_stack_configuration_set

Impostare la configurazione corrente

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_configuration_set(ULONG configuration_value);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata dall'host per impostare la configurazione corrente in esecuzione nel dispositivo. Al momento della ricezione di questo comando, lo stack di dispositivi USB attiverà l'impostazione alternativa 0 di ogni interfaccia connessa a questa configurazione.

### <a name="input-parameter"></a>Parametro di input

- **configuration_value** Valore di configurazione selezionato dall'host.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) La configurazione è stata impostata correttamente.

### <a name="example"></a>Esempio

```c
ULONG configuration_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_configuration_set(configuration_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_descriptor_send"></a>ux_device_stack_descriptor_send

Inviare un descrittore all'host

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_descriptor_send(
    ULONG descriptor_type, 
    ULONG request_index, 
    ULONG host_length);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata dal lato dispositivo per restituire un descrittore all'host. Questo descrittore può essere un descrittore di dispositivo, un descrittore di configurazione o un descrittore di stringa.

### <a name="parameters"></a>Parametri

- **descriptor_type:** tipo del descrittore. Deve essere uno dei valori seguenti.
  - **UX_DEVICE_DESCRIPTOR_ITEM**
  - **UX_CONFIGURATION_DESCRIPTOR_ITEM**
  - **UX_STRING_DESCRIPTOR_ITEM**
  - **UX_DEVICE_QUALIFIER_DESCRIPTOR_ITEM**
  - **UX_OTHER_SPEED_DESCRIPTOR_ITEM**
- **request_index**: indice del descrittore.
- **host_length**: lunghezza richiesta dall'host.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il trasferimento dei dati è stato completato.
- **UX_ERROR** (0xFF) Il trasferimento non è stato completato.

### <a name="example"></a>Esempio

```c
ULONG descriptor_type;
ULONG request_index;
ULONG host_length;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_descriptor_send(descriptor_type, request_index, host_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_disconnect"></a>ux_device_stack_disconnect

Disconnettere lo stack di dispositivi

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_disconnect(VOID);
```

### <a name="description"></a>Descrizione

Il gestore VBUS chiama questa funzione quando è presente una disconnessione del dispositivo. Lo stack di dispositivi informerà tutte le classi registrate nel dispositivo e successivamente rilascerà tutte le risorse del dispositivo.

### <a name="input-parameter"></a>Parametro di input

Nessuno

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) Il dispositivo è stato disconnesso.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_disconnect();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_endpoint_stall"></a>ux_device_stack_endpoint_stall

Condizione di stallo dell'endpoint di richiesta

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_endpoint_stall(UX_SLAVE_ENDPOINT*endpoint);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata dalla classe di dispositivo USB quando un endpoint deve restituire una condizione Stall all'host.

### <a name="input-parameter"></a>Parametro di input

- **endpoint** Endpoint in cui è richiesta la condizione Stall.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** (0xFF) Lo stato del dispositivo non è valido.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_endpoint_stall(endpoint);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_host_wakeup"></a>ux_device_stack_host_wakeup

Riattivare l'host

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_host_wakeup(VOID);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando il dispositivo vuole riattivare l'host. Questo comando è valido solo quando il dispositivo è in modalità di sospensione. L'applicazione del dispositivo deve decidere quando riattivare l'host USB. Ad esempio, un modem USB può riattivare un host quando rileva un segnale RING sulla linea telefonica.

### <a name="input-parameter"></a>Parametro di input

Nessuno

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) La chiamata ha avuto esito positivo.
- **UX_FUNCTION_NOT_SUPPORTED** (0x54) La chiamata non è riuscita (il dispositivo probabilmente non era in modalità sospesa).

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_host_wakeup();

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_initialize"></a>ux_device_stack_initialize

Inizializzare lo stack di dispositivi USB

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_initialize(
    UCHAR *device_framework_high_speed,
    ULONG device_framework_length_high_speed,
    UCHAR *device_framework_full_speed,
    ULONG device_framework_length_full_speed,
    UCHAR *string_framework,
    ULONG string_framework_length,
    UCHAR *language_id_framework,
    ULONG language_id_framework_length),
    UINT (*ux_system_slave_change_function)(ULONG)));
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata dall'applicazione per inizializzare lo stack di dispositivi USB. Non inizializza classi o controller. Questa operazione deve essere eseguita con chiamate di funzione separate. Questa chiamata fornisce principalmente lo stack con il framework del dispositivo per la funzione USB. Supporta velocità sia elevate che complete con la possibilità di avere un framework di dispositivi completamente separato per ogni velocità. Sono supportati il framework di stringhe e più linguaggi.

### <a name="parameters"></a>Parametri

- **device_framework_high_speed:** puntatore al framework ad alta velocità.
- **device_framework_length_high_speed**: lunghezza del framework ad alta velocità.
- **device_framework_full_speed:** puntatore al framework a velocità completa.
- **device_framework_length_full_speed:** lunghezza del framework di velocità completa.
- **string_framework:** puntatore al framework di stringhe.
- **string_framework_length:** lunghezza del framework di stringhe.
- **language_id_framework:** puntatore al framework del linguaggio di stringa.
- **language_id_framework_length**: lunghezza del framework del linguaggio di stringhe.
- **ux_system_slave_change_function:** funzione da chiamare quando cambia lo stato del dispositivo.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_MEMORY_INSUFFICIENT** (0x12) Memoria insufficiente per inizializzare lo stack.
- **UX_DESCRIPTOR_CORRUPTED** (0x42) Il descrittore non è valido.

### <a name="example"></a>Esempio

```c
/* Example of a device framework */

#define DEVICE_FRAMEWORK_LENGTH_FULL_SPEED 50

UCHAR device_framework_full_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x08,
    0xec, 0x08, 0x10, 0x00, 0x00, 0x00, 0x00, 0x00,
    0x00, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50,
    0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x40, 0x00, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x40, 0x00, 0x00
};

#define DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED 60

UCHAR device_framework_high_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40,
    0x0a, 0x07, 0x25, 0x40, 0x01, 0x00, 0x01, 0x02,
    0x03, 0x01,

    /* Device qualifier descriptor */
    0x0a, 0x06, 0x00, 0x02, 0x00, 0x00, 0x00, 0x40,
    0x01, 0x00,

    /* Configuration descriptor */
    0x09, 0x02, 0x20, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x02, 0x08, 0x06, 0x50,
    0x00,

    /* Endpoint descriptor (Bulk Out) */
    0x07, 0x05, 0x01, 0x02, 0x00, 0x02, 0x00,

    /* Endpoint descriptor (Bulk In) */
    0x07, 0x05, 0x82, 0x02, 0x00, 0x02, 0x00
};

/* String Device Framework:
    Byte 0 and 1: Word containing the language ID: 0x0904 for US
    Byte 2 : Byte containing the index of the descriptor
    Byte 3 : Byte containing the length of the descriptor string */

#define STRING_FRAMEWORK_LENGTH 38 UCHAR string_framework[] = {
    /* Manufacturer string descriptor: Index 1 */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72,0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,

    /* Product string descriptor: Index 2 */
    0x09, 0x04, 0x02, 0x0c,
    0x4D, 0x4C, 0x36, 0x39, 0x36, 0x35, 0x30, 0x30,
    0x20, 0x53, 0x44, 0x4B,

    /* Serial Number string descriptor: Index 3 */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31
};

/* Multiple languages are supported on the device, to add a language besides English, 
  the Unicode language code must be appended to the language_id_framework array 
  and the length adjusted accordingly. */

#define LANGUAGE_ID_FRAMEWORK_LENGTH 2

UCHAR language_id_framework[] = {
    /* English. */
    0x09, 0x04
};
```

L'applicazione può richiedere una chiamata quando il controller ne modifica lo stato. I due stati principali per il controller sono:

- **UX_DEVICE_SUSPENDED**
- **UX_DEVICE_RESUMED**

Se l'applicazione non richiede segnali Sospendi/Riprendi, fornisce una UX_NULL funzione.

```c
UINT status;

/* The code below is required for installing the device portion of USBX. 
    There is no call back for device status change in this example. */
status = ux_device_stack_initialize(&device_framework_high_speed,
    DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED, &device_framework_full_speed,
    DEVICE_FRAMEWORK_LENGTH_FULL_SPEED, &string_framework,
    STRING_FRAMEWORK_LENGTH, &language_id_framework,
    LANGUAGE_ID_FRAMEWORK_LENGTH, UX_NULL);

/* If status equals UX_SUCCESS, initialization was successful. */
```

### <a name="ux_device_stack_interface_delete"></a>ux_device_stack_interface_delete

Eliminare un'interfaccia dello stack

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_interface_delete(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'interfaccia deve essere rimossa. Un'interfaccia viene rimossa quando un dispositivo viene estratto o dopo una reimpostazione del bus o quando è presente una nuova impostazione alternativa.

### <a name="input-parameter"></a>Parametro di input

- **interface:** puntatore all'interfaccia da rimuovere.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_delete(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_get"></a>ux_device_stack_interface_get

Ottenere il valore dell'interfaccia corrente

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_interface_get(UINT interface_value);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando l'host esegue una query sull'interfaccia corrente. Il dispositivo restituisce il valore dell'interfaccia corrente.

> [!NOTE]
> Questa funzione è deprecata. È disponibile per il software legacy, ma il nuovo software deve usare ***ux_device_stack_alternate_setting_get*** funzione.

### <a name="input-parameter"></a>Parametro di input

- **interface_value** Valore dell'interfaccia da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** (0xFF) Non esiste alcuna interfaccia.

### <a name="example"></a>Esempio

```c
ULONG interface_value;

UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_get(interface_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_set"></a>ux_device_stack_interface_set

Modificare l'impostazione alternativa dell'interfaccia

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_interface_set(
    UCHAR *device_framework,
    ULONG device_framework_length, 
    ULONG alternate_setting_value);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando l'host richiede una modifica dell'impostazione alternativa per l'interfaccia.

### <a name="parameters"></a>Parametri

- **device_framework**: indirizzo del framework di dispositivi per questa interfaccia.
- **device_framework_length**: lunghezza del framework di dispositivi.
- **alternate_setting_value**: valore di impostazione alternativo che deve essere usato da questa interfaccia.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** (0xFF) Non esiste alcuna interfaccia.

### <a name="example"></a>Esempio

```c
UCHAR * device_framework
ULONG device_framework_length;
ULONG alternate_setting_value;
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_set(device_framework,
    device_framework_length, alternate_setting_value);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_interface_start"></a>ux_device_stack_interface_start

Avviare la ricerca di una classe proprietaria di un'istanza di interfaccia

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_interface_start(UX_SLAVE_INTERFACE*interface);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'interfaccia è stata selezionata dall'host e lo stack di dispositivi deve cercare una classe di dispositivo proprietaria di questa istanza dell'interfaccia.

### <a name="input-parameter"></a>Parametro di input

- **interface:** puntatore all'interfaccia creata.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_NO_CLASS_MATCH** (0x57) Non esiste alcuna classe per questa interfaccia.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */
status = ux_device_stack_interface_start(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_transfer_request"></a>ux_device_stack_transfer_request

Richiesta di trasferimento dei dati all'host

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_transfer_request(
    UX_SLAVE_TRANSFER *transfer_request,
    ULONG slave_length, 
    ULONG host_length);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando una classe o lo stack vuole trasferire i dati all'host. L'host esegue sempre il polling del dispositivo, ma il dispositivo può preparare i dati in anticipo.

### <a name="parameters"></a>Parametri

- **transfer_request**: puntatore alla richiesta di trasferimento.
- **slave_length:** lunghezza che il dispositivo vuole restituire.
- **host_length:** lunghezza richiesta dall'host.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_TRANSFER_NOT_READY** (0x25) Il dispositivo si trova in uno stato non valido. deve essere **ATTACHED,** **CONFIGURED** o **ADDRESSED.**
- **UX_ERROR** (0xFF) Transport .

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates how to transfer more data than an application requests. */
while(total_length) {
    /* How much can we send in this transfer? */
    if (total_length > UX_SLAVE_CLASS_STORAGE_BUFFER_SIZE)
        transfer_length = UX_SLAVE_CLASS_STORAGE_BUFFER_SIZE;
    else
        transfer_length = total_length;

   /* Copy the Storage Buffer into the transfer request memory. */
   ux_utility_memory_copy(transfer_request ->  ux_slave_transfer_request_data_pointer,
       media_memory, transfer_length);

   /* Send the data payload back to the caller. */
   status = ux_device_transfer_request(transfer_request,
       transfer_length, transfer_length);

   /* If status equals UX_SUCCESS, the operation was successful. */

   /* Update the buffer address.  */
    media_memory += transfer_length;

   /* Update the length to remain. */
    total_length -= transfer_length;
}
```

### <a name="ux_device_stack_transfer_abort"></a>ux_device_stack_transfer_abort

Annullare una richiesta di trasferimento

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_transfer_abort(
    UX_SLAVE_TRANSFER *transfer_request, 
    ULONG completion_code);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve annullare una richiesta di trasferimento o quando lo stack deve interrompere una richiesta di trasferimento associata a un endpoint.

### <a name="parameters"></a>Parametri

- **transfer_request**: puntatore alla richiesta di trasferimento.
- **completion_code**: codice di errore da restituire alla classe in attesa del completamento della richiesta di trasferimento.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates how to abort a transfer when a
    bus reset has been detected on the bus. */
status = ux_device_stack_transfer_abort(transfer_request, UX_TRANSFER_BUS_RESET);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_stack_uninitialize"></a>ux_device_stack_uninitialize

Stack Unitialize

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_stack_uninitialize();
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve unitàalizzare lo stack di dispositivi USBX: tutte le risorse dello stack di dispositivi vengono liberate. Questa operazione deve essere chiamata dopo l'annullamento della registrazione di tutte le classi tramite ux_device_stack_class_unregister.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-value"></a>Valore restituito

**UX_SUCCESS** (0x00) L'operazione è riuscita.
