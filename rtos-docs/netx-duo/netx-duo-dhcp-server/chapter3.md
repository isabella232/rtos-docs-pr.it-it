---
title: Capitolo 3-Descrizione dei servizi server DHCP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi server DHCP di NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 33eb0b4bd98f808124b9a6a1f01950639243d612
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822010"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dhcp-server-services"></a>Capitolo 3-Descrizione dei servizi server DHCP di Azure RTO NetX Duo

Questo capitolo contiene una descrizione di tutti i servizi server DHCP di NetX Duo (elencati di seguito) in ordine alfabetico.

> [!NOTE]
> Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="nx_dhcp_server-create"></a>creazione nx_dhcp_server

Creare un'istanza del server DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_server_create(NX_DHCP_SERVER *dhcp_ptr, NX_IP *ip_ptr,
    VOID *stack_ptr, ULONG stack_size,
    CHAR *input_address_list, CHAR *name_ptr, NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server DHCP con un'istanza IP creata in precedenza.

> [!IMPORTANT]
> L'applicazione deve verificare che il pool di pacchetti creato per il servizio di creazione IP disponga di un payload di 548 byte minimo, esclusi le intestazioni UDP, IP e Ethernet.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo server DHCP.
- **ip_ptr** Puntatore all'istanza IP del server DHCP.
- **stack_ptr** Posizione dello stack del server DHCP del puntatore.
- **Stack_size dimensioni dello stack server DHCP** input_address_list puntatore all'elenco di indirizzi IP del server
- puntatore **name_ptr al nome del server dhcp** packet_pool_ptr puntatore al pool di pacchetti del server DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il server DHCP è stato creato correttamente.
- Errore del payload del pacchetto **NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD** (0xA9) troppo piccolo
- L'elenco di opzioni del server **NX_DHCP_NO_SERVER_OPTION_LIST** (0x96) è vuoto
- NX_DHCP_PARAMETER_ERROR (0x92) non è stato inserito alcun puntatore non valido
- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.
- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```C
/* Create a DHCP Server instance. */

status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
    DEMO_SERVER_STACK_SIZE, SERVER_IP_ADDRESS_LIST, "DHCP server", &server_pool);

/* If status is NX_SUCCESS a DHCP Server instance was successfully created. */
```

## <a name="nx_dhcp_create_server_ip_address_list"></a>nx_dhcp_create_server_ip_address_list

Creare un pool di indirizzi IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_create_server_ip_address_list(NX_DHCP_SERVER *dhcp_ptr,
    UINT iface_index, ULONG start_ip_address,
    ULONG end_ip_address, UINT *addresses_added);
```

### <a name="description"></a>Descrizione

Questo servizio crea un pool specifico dell'interfaccia di rete di indirizzi IP disponibili per il server DHCP specificato da assegnare. Gli indirizzi IP di inizio e di fine devono corrispondere all'interfaccia di rete specificata. Il numero effettivo di indirizzi IP aggiunti può essere inferiore al totale degli indirizzi se l'elenco di indirizzi IP non è sufficientemente grande (impostazione configurabile dall'utente *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parametro).

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo server DHCP.
- **iface_index** Indice corrispondente all'interfaccia di rete
- **start_ip_address** Primo indirizzo IP disponibile
- **end_ip_address** Ultimo indirizzo IP disponibile
- **addresses_added** Numero di indirizzi IP aggiunti all'elenco

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il server DHCP è stato creato correttamente.
- L'indice **NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) non corrisponde agli indirizzi
- Input dell'indirizzo di **NX_DHCP_INVALID_IP_ADDRESS_LIST** (0X99) non valido
- Indirizzi di inizio/fine illogici NX_DHCP_INVALID_IP_ADDRESS (0x9B)
- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```C
/* Create a pool of available IP addresses to assign. */

status = nx_dhcp_create_server_ip_list(&dhcp_server, iface_index,
    START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);

/* If status is NX_SUCCESS a IP address list was successfully created.
    addresses_added indicates how many IP addresses were actually added to the
    list. */
```

## <a name="nx_dhcp_clear_client_record"></a>nx_dhcp_clear_client_record

Rimuovi record client dal database del server

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_clear_client_record(NX_DHCP_SERVER *dhcp_ptr,
    NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella il record client dal database del server.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo server DHCP.
- **dhcp_client_ptr puntatore al client DHCP da rimuovere**

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il server DHCP è stato creato correttamente.
- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.
- NX_CALLER_ERROR (0x11) chiamante non thread del servizio

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```C
/* Remove Client record from the server database. */
status = nx_dhcp_clear_client_record(&dhcp_server, &dhcp_client_ptr);

/* If status is NX_SUCCESS the specified Client was removed from the database. */
```

## <a name="nx_dhcp_set_interface_network_parameters"></a>nx_dhcp_set_interface_network_parameters

Impostare i parametri di rete per le opzioni DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_set_interface_network_parameters(NX_DHCP_SERVER *dhcp_ptr,
    UINT iface_index, ULONG subnet_mask,
    ULONG default_gateway_address,
    ULONG dns_server_address);
```

### <a name="description"></a>Descrizione

Questo servizio imposta i valori predefiniti per i parametri critici della rete per l'interfaccia specificata. Il server DHCP includerà queste opzioni nell'offerta e le risposte ACK al client DHCP. Se i parametri dell'interfaccia del set di host in cui è in esecuzione un server DHCP, i parametri vengono impostati come predefiniti come indicato di seguito: il router impostato sul gateway di interfaccia principale per il server DHCP stesso, l'indirizzo del server DNS per il server DHCP stesso e il subnet mask allo stesso modo in cui è configurata l'interfaccia server DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo server DHCP.
- **iface_index** Indice corrispondente all'interfaccia di rete
- **subnet_mask** Subnet mask per rete client
- **default_gateway_address** Indirizzo IP del router del client
- **dns_server_address** Server DNS per la rete del client

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il server DHCP è stato creato correttamente.
- L'indice **NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) non corrisponde agli indirizzi
- Parametri di rete non validi per **NX_DHCP_INVALID_NETWORK_PARAMETERS** (0xA3)
- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```C
/* Set network parameters for a specific interface. */

status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
    NX_DHCP_SUBNET_MASK, NX_DHCP_DEFAULT_GATEWAY,
    NX_DHCP_DNS_SERVER);

/* If status is NX_SUCCESS network parameters were successfully set. */
```

## <a name="nx_dhcp_server_delete"></a>nx_dhcp_server_delete

Eliminare un'istanza del server DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_server_delete(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del server DHCP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore a un'istanza del server DHCP.

### <a name="return-values"></a>Valori restituiti

- Eliminazione del server DHCP riuscita **NX_SUCCESS** (0x00).
- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.
- NX_DHCP_PARAMETER_ERROR (0x92) non è stato inserito alcun puntatore non valido
- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete a DHCP Server instance. */

status = nx_dhcp_server_delete(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server instance was successfully deleted. */
```

## <a name="nx_dhcp_server_start"></a>nx_dhcp_server_start

Avviare l'elaborazione del server DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_server_start(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'elaborazione del server DHCP, che include la creazione di un socket UDP del server, l'associazione della porta DHCP e l'attesa per la ricezione delle richieste DHCP del client.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Inizio del server **NX_SUCCESS** (0x00) riuscito.
- **NX_DHCP_ALREADY_STARTED** DHCP (0x93) già avviato.
- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.
- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.
- NX_DHCP_PARAMETER_ERROR (0x92) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start the DHCP Server processing for this IP instance. */

status = nx_dhcp_server_start(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server was successfully started. */
```

## <a name="nx_dhcp_server_stop"></a>nx_dhcp_server_stop

Arresta l'elaborazione del server DHCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcp_server_stop(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio interrompe l'elaborazione del server DHCP, che include la ricezione di richieste client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore all'istanza del server DHCP.

### <a name="return-values"></a>Valori restituiti

- Arresto DHCP **NX_SUCCESS** (0x00) riuscito.
- **NX_DHCP_ALREADY_STARTED** DHCP (0x93) già avviato.
- L'input del puntatore NX_PTR_ERROR (0x16) non è valido.
- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.
- NX_DHCP_PARAMETER_ERROR (0x92) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop the DHCP Server processing for this IP instance. */

status = nx_dhcp_server_stop(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server was successfully stopped. */
```
