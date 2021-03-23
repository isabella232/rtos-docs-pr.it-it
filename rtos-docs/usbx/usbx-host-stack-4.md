---
title: Capitolo 4-Descrizione dei servizi host USBX
description: Informazioni sui servizi host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d730658c07f3cd7cec8c75a47818314bdc63f35a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824359"
---
# <a name="chapter-4---description-of-usbx-host-services"></a>Capitolo 4-Descrizione dei servizi host USBX

## <a name="ux_host_stack_initialize"></a>ux_host_stack_initialize

Inizializzare USBX per l'operazione host.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_initialize(
    UINT (*system_change_function)
    (ULONG, UX_HOST_CLASS *));
```

### <a name="description"></a>Descrizione

Questa funzione Inizializza lo stack host USB. L'area di memoria specificata verrà impostata per l'uso interno di USBX. Se viene restituito UX_SUCCESS, USBX è pronto per il controller host e la registrazione della classe.

### <a name="input-parameter"></a>Parametro di input

- **system_change_function** Puntatore alla routine di callback facoltativa per notificare l'applicazione delle modifiche del dispositivo.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) inizializzazione riuscita.
- **UX_MEMORY_INSUFFICIENT** (0X12) un'allocazione di memoria non riuscita.

### <a name="example"></a>Esempio

```c
UINT status;

/* Initialize USBX for host operation, without notification. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, USBX has been successfully initialized for host operation. */
```

## <a name="ux_host_stack_endpoint_transfer_abort"></a>ux_host_stack_endpoint_transfer_abort

Interrompi tutte le transazioni associate a una richiesta di trasferimento per un endpoint.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_endpoint_transfer_abort(UX_ENDPOINT *endpoint);
```

### <a name="description"></a>Descrizione

Questa funzione cancellerà tutte le transazioni attive o in sospeso per una richiesta di trasferimento specifica collegata a un endpoint. La richiesta di trasferimento ha una funzione di callback collegata, la funzione di callback verrà chiamata con lo stato UX_TRANSACTION_ABORTED.

### <a name="input-parameter"></a>Parametro di input

- **endpoint** di Puntatore a un endpoint.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) non sono presenti errori.
- HANDLE dell'endpoint **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) non valido.

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

Ottenere il puntatore a un contenitore della classe.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_get(
    UCHAR *class_name,
    UX_HOST_CLASS **class);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un puntatore al contenitore della classe. Una classe deve ottenere il relativo contenitore dallo stack USB per cercare le istanze quando una classe o un'applicazione vuole aprire un dispositivo.

> [!NOTE]
> La stringa C di class_name deve essere con terminazione NULL e la lunghezza (senza il carattere di terminazione NULL) non deve essere maggiore di UX_MAX_CLASS_NAME_LENGTH.

### <a name="parameters"></a>Parametri

- **class_name** Puntatore al nome della classe.
- **classe** Puntatore aggiornato dalla chiamata di funzione che contiene il contenitore della classe per il nome della classe.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) nessun errore, al ritorno il campo della classe viene archiviato con il puntatore al contenitore della classe.
- La classe **UX_HOST_CLASS_UNKNOWN** (0x59) è sconosciuta dallo stack.

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

Questa funzione registra una classe USB nello stack USB. La classe deve specificare un punto di ingresso per lo stack USB per inviare comandi come il seguente.

- **UX_HOST_CLASS_COMMAND_QUERY**
- **UX_HOST_CLASS_COMMAND_ACTIVATE**
- **UX_HOST_CLASS_COMMAND_DESTROY**

> [!NOTE]
> La stringa C di *class_name* deve essere con terminazione null e la lunghezza (senza il carattere di terminazione null) non deve essere maggiore di **UX_MAX_CLASS_NAME_LENGTH**.

### <a name="parameters"></a>Parametri

- **class_name** Puntatore al nome della classe, le voci valide si trovano nel file ux_system_initialize. c nelle classi USB di USBX.
- **class_entry_address** Indirizzo della funzione entry della classe.

### <a name="return-values"></a>Valori restituiti

- Classe **UX_SUCCESS** (0x00) installata correttamente.
- **UX_MEMORY_ARRAY_FULL** (0X1a) non è più disponibile memoria per archiviare questa classe.
- La classe host **UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) è già installata.

### <a name="example"></a>Esempio:

```c
UINT status;

/* Register all the classes for this implementation. */
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, class was successfully installed. */
```

## <a name="ux_host_stack_class_instance_create"></a>ux_host_stack_class_instance_create

Creare una nuova istanza della classe per un contenitore della classe.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_instance_create(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a>Descrizione

Questa funzione crea una nuova istanza della classe per un contenitore della classe. L'istanza di una classe non è contenuta nel codice della classe per ridurre la complessità della classe. Ogni istanza di classe è invece collegata al contenitore della classe presente nello stack principale.

### <a name="parameters"></a>Parametri

- **classe** Puntatore al contenitore della classe.
- **class_instance** Puntatore all'istanza della classe da creare.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) l'istanza della classe è stata collegata al contenitore della classe.

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

Eliminare un'istanza della classe per un contenitore di classi.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_instance_destroy(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a>Descrizione

Questa funzione Elimina un'istanza della classe per un contenitore della classe.

### <a name="parameters"></a>Parametri

- **classe** Puntatore al contenitore della classe.
- **class_instance** Puntatore all'istanza da eliminare definitivamente.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) l'istanza della classe è stata eliminata definitivamente.
- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5b) l'istanza della classe non è collegata al contenitore della classe.

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

Ottenere un puntatore a un'istanza di classe per una classe specifica.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_class_instance_get(
    UX_HOST_CLASS *class,
    UINT class_index, 
    VOID **class_instance);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un puntatore all'istanza della classe per una classe specifica. L'istanza di una classe non è contenuta nel codice della classe per ridurre la complessità della classe. Ogni istanza di classe è invece collegata al contenitore della classe. Questa funzione viene usata per cercare le istanze della classe all'interno di un contenitore di classi.

### <a name="parameters"></a>Parametri

- **classe** Puntatore al contenitore della classe.
- **class_index** Indice che deve essere utilizzato dalla chiamata di funzione all'interno dell'elenco di classi associate al contenitore.
- **class_instance** Puntatore all'istanza di che deve essere restituita dalla chiamata di funzione.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) l'istanza della classe è stata trovata.

- **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non sono presenti altre istanze di classe associate al contenitore della classe.

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

- **dispositivo** Puntatore al contenitore di dispositivi proprietario della configurazione richiesta.
- **configuration_index** Indice della configurazione in cui eseguire la ricerca.
- **configurazione** di Indirizzo del puntatore al contenitore di configurazione da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) la configurazione è stata trovata.
- **UX_DEVICE_HANDLE_UNKNOWN** (0X50) il contenitore di dispositivi non esiste.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'handle di configurazione per l'indice non esiste.

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

Questa funzione seleziona una configurazione specifica per un dispositivo. Quando questa configurazione è impostata sul dispositivo, per impostazione predefinita ogni interfaccia del dispositivo e l'impostazione alternativa 0 associata viene attivata sul dispositivo. Se la classe del dispositivo/interfaccia desidera modificare l'impostazione di una particolare interfaccia, è necessario eseguire una chiamata al servizio **ux_host_stack_interface_setting_select** .

### <a name="parameters"></a>Parametri

- **configurazione** di Puntatore al contenitore di configurazione che deve essere abilitato per questo dispositivo.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) la selezione della configurazione è stata completata correttamente.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'handle di configurazione non esiste.
- **UX_OVER_CURRENT_CONDITION** (0x43) è presente una condizione Over Current sul bus per questa configurazione.

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

Questa funzione restituisce un contenitore di dispositivi in base al relativo indice. L'indice del dispositivo inizia con 0. Si noti che l'indice è un ULONG perché potrebbero essere presenti più controller e un indice byte potrebbe non essere sufficiente. L'indice del dispositivo non deve essere confuso con l'indirizzo del dispositivo specifico del bus.

### <a name="parameters"></a>Parametri

- **device_index** Indice del dispositivo.
- **dispositivo** Indirizzo dell'indicatore di misura per il contenitore di dispositivi da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il contenitore di dispositivi esiste e viene restituito
- Dispositivo **UX_DEVICE_HANDLE_UNKNOWN** (0x50) sconosciuto

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

Questa funzione restituisce un contenitore di endpoint basato sull'handle dell'interfaccia e un indice dell'endpoint. Si presuppone che sia stata selezionata l'impostazione alternativa per l'interfaccia o che l'impostazione predefinita venga utilizzata prima degli endpoint di cui viene eseguita la ricerca.

### <a name="parameters"></a>Parametri

- **interfaccia** di Puntatore al contenitore dell'interfaccia che contiene l'endpoint richiesto.
- **endpoint_index** Indice dell'endpoint in questa interfaccia.
- **endpoint** di Indirizzo del contenitore dell'endpoint da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il contenitore dell'endpoint esiste e viene restituito.
- L'interfaccia **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) specificata non esiste.
- L'indice dell'endpoint **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) non esiste.

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

Questa funzione registra un controller USB nello stack USB. Alloca principalmente la memoria utilizzata da questo controller e passa il comando di inizializzazione al controller.

### <a name="parameters"></a>Parametri

- **hcd_name** Nome del controller host
- **hcd_function** Funzione nel controller host responsabile dell'inizializzazione.
- **hcd_param1** Il IO o la risorsa di memoria utilizzata da HCD.
- **hcd_param2** IRQ utilizzato dal controller host.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il controller è stato inizializzato correttamente.
- **UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente per questo controller.
- **UX_PORT_RESET_FAILED** (0X31) la reimpostazione del controller non è riuscita.
- **UX_CONTROLLER_INIT_FAILED** (0x32) non è stato possibile inizializzare correttamente il controller.

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

Ottenere un puntatore del contenitore di interfaccia.

### <a name="prototype"></a>Prototipo

```c
UINT ux_host_stack_configuration_interface_get (
    UX_CONFIGURATION *configuration,
    UINT interface_index, 
    UINT alternate_setting_index, 
    UX_INTERFACE **interface);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce un contenitore di interfaccia basato su un handle di configurazione, un indice dell'interfaccia e un indice di impostazione alternativo.

### <a name="parameters"></a>Parametri

- **configurazione** di Puntatore al contenitore di configurazione che possiede l'interfaccia.
- **interface_index** Indice dell'interfaccia in cui eseguire la ricerca.
- **alternate_setting_index** Impostazione alternativa all'interno dell'interfaccia in cui eseguire la ricerca.
- **interfaccia** di Indirizzo del puntatore del contenitore di interfaccia da restituire.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il contenitore dell'interfaccia per l'indice dell'interfaccia e l'impostazione alternativa è stato trovato e restituito.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) la configurazione non esiste.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0X52) l'interfaccia non esiste.

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

Questa funzione seleziona una specifica impostazione alternativa per un'interfaccia specificata che appartiene alla configurazione selezionata. Questa funzione viene usata per passare dall'impostazione alternativa predefinita a una nuova impostazione o per tornare all'impostazione predefinita alternativa. Quando viene selezionata una nuova impostazione alternativa, le caratteristiche precedenti dell'endpoint non sono valide e devono essere ricaricate.

### <a name="input-parameter"></a>Parametro di input

- **interfaccia** di Puntatore al contenitore dell'interfaccia di cui è necessario selezionare l'impostazione alternativa.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) la selezione dell'impostazione alternativa per questa interfaccia è stata completata.
- **UX_INTERFACE_HANDLE_UNKNOWN** (0X52) l'interfaccia non esiste.

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

Questa funzione interrompe una richiesta di trasferimento in sospeso inviata in precedenza. Questa funzione Annulla solo una richiesta di trasferimento specifica. La chiamata alla funzione avrà lo stato UX_TRANSFER REQUEST_STATUS_ABORT.

### <a name="parameters"></a>Parametri

- **richiesta di trasferimento** Puntatore alla richiesta di trasferimento da interrompere.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il trasferimento USB per la richiesta di trasferimento è stato annullato.

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

Questa funzione esegue una transazione USB. All'immissione della richiesta di trasferimento viene assegnata la pipe dell'endpoint selezionata per la transazione e i parametri associati al trasferimento (payload dei dati, lunghezza della transazione). Per la pipe di controllo, la transazione è bloccata e restituirà solo quando le tre fasi del trasferimento del controllo sono state completate o se si è verificato un errore precedente. Per le altre pipe, lo stack USB pianifica la transazione sull'USB ma non ne attende il completamento. Ogni richiesta di trasferimento per le pipe non bloccanti deve specificare un gestore routine di completamento.

Quando la chiamata di funzione restituisce, lo stato della richiesta di trasferimento deve essere esaminato in quanto contiene il risultato della transazione.

### <a name="input-parameter"></a>Parametro di input

- **transfer_request** Puntatore alla richiesta di trasferimento. La richiesta di trasferimento contiene tutte le informazioni necessarie per il trasferimento.

### <a name="return-values"></a>Valori restituiti

- **UX_SUCCESS** (0x00) il trasferimento USB per la richiesta di trasferimento è stato pianificato correttamente. Il codice di stato della richiesta di trasferimento deve essere esaminato al completamento della richiesta di trasferimento.
- **UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente per allocare le risorse del controller necessarie.
- **UX_TRANSFER_NOT_READY** (0x25) il dispositivo si trova in uno stato non valido. deve essere collegato, risolto o configurato.

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
