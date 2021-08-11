---
title: Capitolo 4 - Descrizione dei servizi host USBX
description: Informazioni sui servizi host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 6cbeff83d8e3812f13aa3f8f66d4013b70490d556911939186b4b43840aac50d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790684"
---
# <a name="chapter-4---description-of-usbx-host-services"></a>Capitolo 4 - Descrizione dei servizi host USBX

## <a name="ux_host_stack_initialize"></a>ux_host_stack_initialize

Inizializzare USBX per l'operazione host.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_initialize(
    UINT (*system_change_function)
    (ULONG, UX_HOST_CLASS *));
```

### <a name="description"></a>Descrizione

Questa funzione inizializza lo stack di host USB. L'area di memoria fornita verrà impostata per l'uso interno di USBX. Se UX_SUCCESS viene restituito , USBX è pronto per la registrazione del controller host e della classe.

### <a name="input-parameter"></a>Parametro di input

- **system_change_function** Puntatore alla routine di callback facoltativa per notificare all'applicazione le modifiche del dispositivo.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) Inizializzazione riuscita.
- **UX_MEMORY_INSUFFICIENT** (0x12) Allocazione di memoria non riuscita.

### <a name="example"></a>Esempio

```c
UINT status;

/* Initialize USBX for host operation, without notification. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, USBX has been successfully initialized for host operation. */
```

## <a name="ux_host_stack_endpoint_transfer_abort"></a>ux_host_stack_endpoint_transfer_abort

Interrompere tutte le transazioni collegate a una richiesta di trasferimento per un endpoint.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_endpoint_transfer_abort(UX_ENDPOINT *endpoint);
```

### <a name="description"></a>Descrizione

Questa funzione annullerà tutte le transazioni attive o in sospeso per una richiesta di trasferimento specifica collegata a un endpoint. La richiesta di trasferimento ha una funzione di callback collegata, la funzione di callback verrà chiamata con lo UX_TRANSACTION_ABORTED stato.

### <a name="input-parameter"></a>Parametro di input

- **endpoint** Puntatore a un endpoint.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Nessun errore.
- **UX_ENDPOINT_HANDLE_UNKNOWN(0x53)** Endpoint non valido.

### <a name="example"></a>Esempio

```c
UX_HOST_CLASS_PRINTER *printer;
UINT status;

/* Get the instance for this class. */
printer = (UX_HOST_CLASS_PRINTER *) command ->
    ux_host_class_command_instance;

/* The printer is being shut down. */

printer -> printer_state = UX_HOST_CLASS_INSTANCE_SHUTDOWN;

/* We need to abort transactions on the bulk out pipe. */
status = ux_host_stack_endpoint_transfer_abort
    (printer -> printer_bulk_out_endpoint);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_get"></a>ux_host_stack_class_get

Ottenere il puntatore a un contenitore di classi.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_get(
    UCHAR *class_name,
    UX_HOST_CLASS **class);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un puntatore al contenitore di classi. Una classe deve ottenere il relativo contenitore dallo stack USB per cercare le istanze quando una classe o un'applicazione vuole aprire un dispositivo.

> [!NOTE]
> La stringa C di class_name deve avere terminazione NULL e la lunghezza (senza il carattere di terminazione NULL stesso) non deve essere maggiore di UX_MAX_CLASS_NAME_LENGTH.

### <a name="parameters"></a>Parametri

- **class_name** Puntatore al nome della classe.
- **classe** Puntatore aggiornato dalla chiamata di funzione che contiene il contenitore di classi per il nome della classe.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Nessun errore, al ritorno il campo della classe viene indicato con il puntatore al contenitore di classi.
- **UX_HOST_CLASS_UNKNOWN** classe (0x59) è sconosciuta dallo stack.

### <a name="example"></a>Esempio

```c
UX_HOST_CLASS *printer_container;
UINT status;

/* Get the container for this class. */
status = ux_host_stack_class_get("ux_host_class_printer", &printer_container);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_register"></a>ux_host_stack_class_register

Registrare una classe USB nello stack USB.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

### <a name="description"></a>Descrizione

Questa funzione registra una classe USB nello stack USB. La classe deve specificare un punto di ingresso per lo stack USB per inviare comandi come i seguenti.

- **UX_HOST_CLASS_COMMAND_QUERY**
- **UX_HOST_CLASS_COMMAND_ACTIVATE**
- **UX_HOST_CLASS_COMMAND_DESTROY**

> [!NOTE]
> La stringa C *di class_name* deve avere terminazione NULL e la sua lunghezza (senza il carattere di terminazione NULL stesso) non deve essere maggiore **di UX_MAX_CLASS_NAME_LENGTH**.

### <a name="parameters"></a>Parametri

- **class_name** Puntatore al nome della classe. Le voci valide si trovano nel file ux_system_initialize.c nelle classi USB di USBX.
- **class_entry_address** Indirizzo della funzione di immissione della classe.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) è stato installato correttamente.
- **UX_MEMORY_ARRAY_FULL** (0x1a) Memoria insufficiente per archiviare questa classe.
- **UX_HOST_CLASS_ALREADY_INSTALLED** classe host (0x58) già installata.

### <a name="example"></a>Esempio:

```c
UINT status;

/* Register all the classes for this implementation. */
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, class was successfully installed. */
```

## <a name="ux_host_stack_class_instance_create"></a>ux_host_stack_class_instance_create

Creare una nuova istanza della classe per un contenitore di classi.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_instance_create(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a>Descrizione

Questa funzione crea una nuova istanza della classe per un contenitore di classi. L'istanza di una classe non è contenuta nel codice della classe per ridurre la complessità della classe. Ogni istanza della classe è invece collegata al contenitore di classi che si trova nello stack principale.

### <a name="parameters"></a>Parametri

- **classe** Puntatore al contenitore di classi.
- **class_instance** Puntatore all'istanza della classe da creare.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'istanza della classe è stata associata al contenitore di classi.

### <a name="example"></a>Esempio

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* Obtain memory for this class instance. */

printer = ux_memory_allocate(UX_NO_ALIGN, sizeof(UX_HOST_CLASS_PRINTER));

if (printer == UX_NULL)
    return(UX_MEMORY_INSUFFICIENT);

/* Store the class container into this instance. */
printer -> printer_class = command -> ux_host_class;

/* Create this class instance. */
status = ux_host_stack_class_instance_create(printer -> printer_class, (VOID *)printer);

/* If status equals UX_SUCCESS, the class instance was successfully created and attached to the class container. */
```

## <a name="ux_host_stack_class_instance_destroy"></a>ux_host_stack_class_instance_destroy

Eliminare un'istanza di classe per un contenitore di classi.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_instance_destroy(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a>Descrizione

Questa funzione elimina un'istanza di classe per un contenitore di classi.

### <a name="parameters"></a>Parametri

- **classe** Puntatore al contenitore di classi.
- **class_instance** Puntatore all'istanza di da eliminare.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) L'istanza della classe è stata distrutta.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) L'istanza della classe non è associata al contenitore di classi.

### <a name="example"></a>Esempio

```c
UINT status;
UX_HOST_CLASS_PRINTER *printer;

/* Get the instance for this class. */
printer = (UX_HOST_CLASS_PRINTER *) command -> ux_host_class_command_instance;

/* The printer is being shut down. */
printer -> printer_state = UX_HOST_CLASS_INSTANCE_SHUTDOWN;

/* Destroy the instance. */
status = ux_host_stack_class_instance_destroy(printer -> printer_class, (VOID *) printer);

/* If status equals UX_SUCCESS, the class instance was successfully destroyed. */
```

## <a name="ux_host_stack_class_instance_get"></a>ux_host_stack_class_instance_get

Ottiene un puntatore all'istanza di classe per una classe specifica.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_instance_get(
    UX_HOST_CLASS *class,
    UINT class_index, 
    VOID **class_instance);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un puntatore di istanza di classe per una classe specifica. L'istanza di una classe non è contenuta nel codice della classe per ridurre la complessità della classe. Ogni istanza della classe è invece associata al contenitore di classi. Questa funzione viene usata per cercare istanze di classe all'interno di un contenitore di classi.

### <a name="parameters"></a>Parametri

- **classe** Puntatore al contenitore di classi.
- **class_index** Indice che deve essere usato dalla chiamata di funzione all'interno dell'elenco di classi associate al contenitore.
- **class_instance** Puntatore all'istanza di che deve essere restituita dalla chiamata di funzione.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) È stata trovata l'istanza della classe.

- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) Non sono presenti altre istanze di classe associate al contenitore di classi.

### <a name="example"></a>Esempio

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* Obtain memory for this class instance. */
printer = ux_memory_allocate(UX_NO_ALIGN, sizeof(UX_HOST_CLASS_PRINTER));

if (printer == UX_NULL) return(UX_MEMORY_INSUFFICIENT);

/* Search for instance index 2. */
status = ux_host_stack_class_instance_get(class, 2, (VOID *) printer);

/* If status equals UX_SUCCESS, the class instance was found. */
```

## <a name="ux_host_stack_device_configuration_get"></a>ux_host_stack_device_configuration_get

Ottenere un puntatore a un contenitore di configurazione.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_device_configuration_get(
    UX_DEVICE *device,
    UINT configuration_index, 
    UX_CONFIGURATION *configuration);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un contenitore di configurazione basato su un handle di dispositivo e un indice di configurazione.

### <a name="parameters"></a>Parametri

- **dispositivo** Puntatore al contenitore del dispositivo proprietario della configurazione richiesta.
- **configuration_index** Indice della configurazione in cui eseguire la ricerca.
- **configurazione** Indirizzo del puntatore al contenitore di configurazione da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) La configurazione è stata trovata.
- **UX_DEVICE_HANDLE_UNKNOWN** (0x50) Il contenitore del dispositivo non esiste.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'handle di configurazione per l'indice non esiste.

### <a name="example"></a>Esempio

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* If the device has been configured already, we don't need to do it
again. */

if (printer -> printer_device -> ux_device_state == UX_DEVICE_CONFIGURED)
    return(UX_SUCCESS);

/* A printer normally has one configuration, retrieve 1st configuration only. */

status = ux_host_stack_device_configuration_get(printer -> printer_device,
    0, configuration);

/* If status equals UX_SUCCESS, the configuration was found. */
```

## <a name="ux_host_stack_device_configuration_select"></a>ux_host_stack_device_configuration_select

Selezionare una configurazione specifica per un dispositivo.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_device_configuration_select (UX_CONFIGURATION *configuration);
```

### <a name="description"></a>Descrizione

Questa funzione seleziona una configurazione specifica per un dispositivo. Quando questa configurazione è impostata sul dispositivo, per impostazione predefinita, ogni interfaccia del dispositivo e l'impostazione alternativa associata 0 vengono attivate nel dispositivo. Se la classe dispositivo/interfaccia vuole modificare l'impostazione di una particolare interfaccia, deve eseguire una chiamata ux_host_stack_interface_setting_select **servizio.**

### <a name="parameters"></a>Parametri

- **configurazione** Puntatore al contenitore di configurazione che deve essere abilitato per questo dispositivo.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) La selezione della configurazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'handle di configurazione non esiste.
- **UX_OVER_CURRENT_CONDITION** (0x43) Una condizione over current esiste nel bus per questa configurazione.

### <a name="example"></a>Esempio

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* If the device has been configured already, we don't need to do it again. */
if (printer -> printer_device -> ux_device_state == UX_DEVICE_CONFIGURED)
    return(UX_SUCCESS);

/* A printer normally has one configuration - retrieve 1st configuration only. */
status = ux_host_stack_device_configuration_get(printer -> printer_device, 0,configuration);

/* If status equals UX_SUCCESS, the configuration selection was successful. */

/* If valid configuration, ask USBX to set this configuration. */
status = ux_host_stack_device_configuration_select(configuration);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_device_get"></a>ux_host_stack_device_get

Ottenere un puntatore a un contenitore di dispositivi.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_device_get(
    ULONG device_index, 
    UX_DEVICE *device);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un contenitore di dispositivi in base al relativo indice. L'indice del dispositivo inizia con 0. Si noti che l'indice è un ULONG perché potrebbero essere disponibili diversi controller e un indice di byte potrebbe non essere sufficiente. L'indice del dispositivo non deve essere confuso con l'indirizzo del dispositivo specifico del bus.

### <a name="parameters"></a>Parametri

- **device_index** Indice del dispositivo.
- **dispositivo** Indirizzo del puntatore per il contenitore del dispositivo da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il contenitore del dispositivo esiste e viene restituito
- **UX_DEVICE_HANDLE_UNKNOWN** (0x50) Dispositivo sconosciuto

### <a name="example"></a>Esempio

```c
UINT status;

/* Locate the first device in USBX. */
status = ux_host_stack_device_get(0, device);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_endpoint_get"></a>ux_host_stack_interface_endpoint_get

Ottenere un contenitore di endpoint.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_interface_endpoint_get(
    UX_INTERFACE *interface,
    UINT endpoint_index,
    UX_ENDPOINT *endpoint);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un contenitore di endpoint in base all'handle di interfaccia e a un indice dell'endpoint. Si presuppone che sia stata selezionata l'impostazione alternativa per l'interfaccia o che venga usata l'impostazione predefinita prima della ricerca degli endpoint.

### <a name="parameters"></a>Parametri

- **interfaccia** Puntatore al contenitore di interfaccia che contiene l'endpoint richiesto.
- **endpoint_index** Indice dell'endpoint in questa interfaccia.
- **endpoint** Indirizzo del contenitore di endpoint da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il contenitore endpoint esiste e viene restituito.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) L'interfaccia specificata non esiste.
- **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Dell'endpoint non esiste.

### <a name="example"></a>Esempio

```c
UINT status;
UX_HOST_CLASS_PRINTER *printer;

for(endpoint_index = 0;
    endpoint_index < printer -> printer_interface ->
        ux_interface_descriptor.bNumEndpoints;
    endpoint_index++)
{
    status = ux_host_stack_interface_endpoint_get (printer -> printer_interface,
        endpoint_index, &endpoint);

    if (status == UX_SUCCESS)
    {
        /* Check if endpoint is bulk and OUT. */
        if (((endpoint -> ux_endpoint_descriptor.bEndpointAddress &
            UX_ENDPOINT_DIRECTION) == UX_ENDPOINT_OUT) &&
            ((endpoint -> ux_endpoint_descriptor.bmAttributes &
            UX_MASK_ENDPOINT_TYPE) == UX_BULK_ENDPOINT))
        return(UX_SUCCESS);
    }
}
```

## <a name="ux_host_stack_hcd_register"></a>ux_host_stack_hcd_register

Registrare un controller USB nello stack USB.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

### <a name="description"></a>Descrizione

Questa funzione registra un controller USB nello stack USB. Alloca principalmente la memoria usata da questo controller e passa il comando di inizializzazione al controller.

### <a name="parameters"></a>Parametri

- **hcd_name** Nome del controller host
- **hcd_function** Funzione nel controller host responsabile dell'inizializzazione.
- **hcd_param1** Risorsa di I/O o di memoria usata dall'oggetto hcd.
- **hcd_param2** IRQ usato dal controller host.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il controller è stato inizializzato correttamente.
- **UX_MEMORY_INSUFFICIENT** (0x12) Memoria insufficiente per questo controller.
- **UX_PORT_RESET_FAILED** (0x31) La reimpostazione del controller non è riuscita.
- **UX_CONTROLLER_INIT_FAILED** (0x32) Il controller non è stato inizializzato correttamente.

### <a name="example"></a>Esempio

```c
UINT status;

/* Initialize a host controller mapped at address 0xd0000 and using IRQ 10. */

status = ux_host_stack_hcd_register("ux_hcd_controller",
    ux_hcd_controller_initialize, 0xd0000, 0x0a);

/* If status equals UX_SUCCESS, the controller was initialized properly. */

/* Note that the application must also setup a call to the
    interrupt handler for the controller.
    The function for the controller is called _ux_hch_controller_interrupt_handler. */
```

## <a name="ux_host_stack_configuration_interface_get"></a>ux_host_stack_configuration_interface_get

Ottenere un puntatore al contenitore di interfaccia.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_configuration_interface_get (
    UX_CONFIGURATION *configuration,
    UINT interface_index, 
    UINT alternate_setting_index, 
    UX_INTERFACE **interface);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un contenitore di interfaccia basato su un handle di configurazione, un indice di interfaccia e un indice di impostazione alternativo.

### <a name="parameters"></a>Parametri

- **configurazione** Puntatore al contenitore di configurazione proprietario dell'interfaccia.
- **interface_index** Indice dell'interfaccia in cui eseguire la ricerca.
- **alternate_setting_index** Impostazione alternativa all'interno dell'interfaccia in cui eseguire la ricerca.
- **interfaccia** Indirizzo del puntatore al contenitore di interfaccia da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il contenitore di interfaccia per l'indice di interfaccia e l'impostazione alternativa sono stati trovati e restituiti.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) La configurazione non esiste.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) L'interfaccia non esiste.

### <a name="example"></a>Esempio

```c
UINT status;

/* Search for the default alternate setting on the first interface for the printer. */
status = ux_host_stack_configuration_interface_get(configuration, 0, 0,
    &printer -> printer_interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_setting_select"></a>ux_host_stack_interface_setting_select

Selezionare un'impostazione alternativa per un'interfaccia.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_interface_setting_select(UX_INTERFACE *interface);
```

### <a name="description"></a>Descrizione

Questa funzione seleziona un'impostazione alternativa specifica per una determinata interfaccia appartenente alla configurazione selezionata. Questa funzione viene usata per passare dall'impostazione alternativa predefinita a una nuova impostazione o per tornare all'impostazione alternativa predefinita. Quando si seleziona una nuova impostazione alternativa, le caratteristiche dell'endpoint precedente non sono valide e devono essere ricaricate.

### <a name="input-parameter"></a>Parametro di input

- **interfaccia** Puntatore al contenitore dell'interfaccia la cui impostazione alternativa deve essere selezionata.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) L'impostazione alternativa per questa interfaccia è stata selezionata correttamente.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) L'interfaccia non esiste.

### <a name="example"></a>Esempio

```c
UINT status;

/* Select a new alternate setting for this interface. */
status = ux_host_stack_interface_setting_select(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_transfer_request_abort"></a>ux_host_stack_transfer_request_abort

Interrompere una richiesta di trasferimento in sospeso.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_transfer_request_abort(UX_TRANSFER REQUEST *transfer request);
```

### <a name="description"></a>Descrizione

Questa funzione interrompe una richiesta di trasferimento in sospeso inviata in precedenza. Questa funzione annulla solo una richiesta di trasferimento specifica. La chiamata alla funzione avrà lo stato UX_TRANSFER REQUEST_STATUS_ABORT funzione.

### <a name="parameters"></a>Parametri

- **richiesta di trasferimento** Puntatore alla richiesta di trasferimento da interrompere.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il trasferimento USB per questa richiesta di trasferimento è stato annullato.

### <a name="example"></a>Esempio

```c
UINT status;

/* The following example illustrates this service. */
status = ux_host_stack_transfer_request_abort(transfer request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_transfer_request"></a>ux_host_stack_transfer_request

Richiedere un trasferimento USB.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_transfer_request(UX_TRANSFER REQUEST *transfer request);
```

### <a name="description"></a>Descrizione

Questa funzione esegue una transazione USB. All'immissione la richiesta di trasferimento fornisce la pipe dell'endpoint selezionata per questa transazione e i parametri associati al trasferimento (payload dei dati, lunghezza della transazione). Per la pipe di controllo, la transazione viene bloccata e verrà restituita solo quando le tre fasi del trasferimento del controllo sono state completate o se si è verificato un errore precedente. Per altre pipe, lo stack USB pianifica la transazione sull'USB, ma non attende il completamento. Ogni richiesta di trasferimento per le pipe non bloccanti deve specificare un gestore di routine di completamento.

Quando la chiamata di funzione viene restituita, lo stato della richiesta di trasferimento deve essere esaminato perché contiene il risultato della transazione.

### <a name="input-parameter"></a>Parametro di input

- **transfer_request** Puntatore alla richiesta di trasferimento. La richiesta di trasferimento contiene tutte le informazioni necessarie necessarie per il trasferimento.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) Il trasferimento USB per questa richiesta di trasferimento è stato pianificato correttamente. Il codice di stato della richiesta di trasferimento deve essere esaminato al termine della richiesta di trasferimento.
- **UX_MEMORY_INSUFFICIENT** (0x12) Memoria insufficiente per allocare le risorse del controller necessarie.
- **UX_TRANSFER_NOT_READY** (0x25) Lo stato del dispositivo non è valido. Deve essere COLLEGATO, INDIRIZZATO o CONFIGURATO.

### <a name="example"></a>Esempio:

```c
UINT status;

/* Create a transfer request for the SET_CONFIGURATION request. No data for this request. */
transfer_request -> ux_transfer_request_requested_length = 0;
transfer_request -> ux_transfer_request_function = UX_SET_CONFIGURATION;
transfer_request -> ux_transfer_request_type =
    UX_REQUEST_OUT |
    UX_REQUEST_TYPE_STANDARD |
    UX_REQUEST_TARGET_DEVICE;

transfer_request -> ux_transfer_request_value = (USHORT)
    configuration -> ux_configuration_descriptor.bConfigurationValue;
transfer_request -> ux_transfer_request_index = 0;

/* Send request to HCD layer. */
status = ux_host_stack_transfer_request(transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```
