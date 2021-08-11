---
title: Capitolo 3 - Descrizione dei Azure RTOS server DHCP NetX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS server DHCP NetX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 702499184b12484fa5862ba83ff3fadb8fccea31089b6bf8b71daf267e8c84a3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799524"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-server-services"></a>Capitolo 3 - Descrizione dei Azure RTOS server DHCP NetX

Questo capitolo contiene una descrizione di tutti i servizi Server DHCP NetX.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **grassetto** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_dhcp_server_create**: *Creare un'istanza del server DHCP*
- **nx_dhcp_set_interface_network_parameters:** impostare *le opzioni del server DHCP per i parametri di rete critici per l'interfaccia specificata*
- **nx_dhcp_create_server_ip_address_list:** creare *un pool di indirizzi IP disponibili da assegnare all'interfaccia client DHCP*
- **nx_dhcp_clear_client_record:** Rimuovere *il record client nel database del server*
- **nx_dhcp_server_delete:** Eliminare *un'istanza di DHCPServer*
- **nx_dhcp_server_start:** Avviare *o riprendere l'elaborazione del server DHCP*
- **nx_dhcp_server_stop:** *Arrestare l'elaborazione del server DHCP*

## <a name="nx_dhcp_server_create"></a>nx_dhcp_server_create

Creare un'istanza del server DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_server_create(NX_DHCP_SERVER *dhcp_ptr, NX_IP *ip_ptr,
                        VOID *stack_ptr, ULONG stack_size,
                        CHAR *input_address_list, CHAR *name_ptr,
                        NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server DHCP con un'istanza IP creata in precedenza.

> [!IMPORTANT]
> L'applicazione deve assicurarsi che il pool di pacchetti creato per il servizio di creazione ip abbia un payload minimo di 548 byte, senza includere le intestazioni UDP, IP ed Ethernet.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** puntatore al blocco di controllo server DHCP.  
- **ip_ptr:** puntatore all'istanza IP del server DHCP.
- **stack_ptr:** percorso dello stack del server DHCP puntatore.
- **stack_size**: Dimensioni dello stack del server DHCP
- **input_address_list:** Puntatore all'elenco di indirizzi IP del server
- **name_ptr:** Puntatore al nome del server DHCP
- **packet_pool_ptr:** Puntatore al pool di pacchetti del server DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione del server DHCP riuscita.
- **NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD:**(0xA9) Errore payload pacchetto troppo piccolo
- **NX_DHCP_NO_SERVER_OPTION_LIST:**(0x96) Elenco di opzioni del server vuoto
- NX_DHCP_PARAMETER_ERROR: (0x92) Input non puntatore non valido
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.
- NX_PTR_ERROR: (0x16) Input del puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```c
/* Create a DHCP Server instance. */
status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                    DEMO_SERVER_STACK_SIZE, SERVER_IP_ADDRESS_LIST,
                    "DHCP server", &server_pool);

/* If status is NX_SUCCESS a DHCP Server instance was successfully created. */
```

## <a name="nx_dhcp_create_server_ip_address_list"></a>nx_dhcp_create_server_ip_address_list

Creare un pool di indirizzi IP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_create_server_ip_address_list(NX_DHCP_SERVER *dhcp_ptr,
                            UINT iface_index, ULONG start_ip_address,
                            ULONG end_ip_address, UINT *addresses_added);
```

### <a name="description"></a>Descrizione

Questo servizio crea un pool specifico networkinterface di indirizzi IP disponibili per il server DHCP specificato da assegnare. Gli indirizzi IP iniziale e finale devono corrispondere all'interfaccia di rete specificata. Il numero effettivo di indirizzi IP aggiunti può essere inferiore al totale degli indirizzi se l'elenco di indirizzi IP non è sufficientemente grande (impostato nel parametro configurabile NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE *utente).*

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo server DHCP.  
- **iface_index:** indice corrispondente all'interfaccia di rete
- **start_ip_address:** primo indirizzo IP disponibile
- **end_ip_address:** Ultimo indirizzo IP disponibile
- **addresses_added:** Numero di indirizzi IP aggiunti all'elenco

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione del server DHCP riuscita.
- **NX_DHCP_SERVER_BAD_INTERFACE_INDEX:** l'indice (0xA1) non corrisponde agli indirizzi
- **NX_DHCP_INVALID_IP_ADDRESS_LIST:**(0x99) Input indirizzo non valido
- NX_DHCP_INVALID_IP_ADDRESS: (0x9B) Indirizzi di inizio/fine illogici
- NX_PTR_ERROR: (0x16) Input del puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```c
/* Create a pool of available IP addresses to assign. */
status = nx_dhcp_create_server_ip_list (&dhcp_server, iface_index,
                START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);

/* If status is NX_SUCCESS aIP address list was successfully created. 
addresses_added indicates how many IP addresses were actually added to the list. */
```

## <a name="nx_dhcp_clear_client_record"></a>nx_dhcp_clear_client_record

Rimuovere il record client dal database del server

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_clear_client_record (NX_DHCP_SERVER *dhcp_ptr,
                                NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cancella il record Client dal database server.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** puntatore al blocco di controllo server DHCP.  
- **dhcp_client_ptr:** Puntatore al client DHCP da rimuovere

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione del server DHCP riuscita.
- NX_PTR_ERROR: (0x16) Input del puntatore non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non thread del servizio

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```c
/* Remove Client record from the server database. */
status = nx_dhcp_clear_client_record (&dhcp_server, &dhcp_client_ptr);

/* If status is NX_SUCCESS the specified Client was removed from the database. */
```

## <a name="nx_dhcp_set_interface_network_parameters"></a>nx_dhcp_set_interface_network_parameters

Impostare i parametri di rete per le opzioni DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_set_interface_network_parameters(NX_DHCP_SERVER *dhcp_ptr,
                                    UINT iface_index, ULONG subnet_mask,
                                    ULONG default_gateway_address,
                                    ULONG dns_server_address);
```

### <a name="description"></a>Descrizione

Questo servizio imposta i valori predefiniti per i parametri critici di rete per l'interfaccia specificata. Il server DHCP includerà queste opzioni nelle risposte OFFER e ACK al client DHCP. Se l'host imposta i parametri di interfaccia in cui è in esecuzione un server DHCP, i parametri verranno impostati per impostazione predefinita come segue: il router impostato sul gateway di interfaccia primaria per il server DHCP stesso, l'indirizzo del server DNS per il server DHCP stesso e il subnet mask allo stesso come l'interfaccia del server DHCP è configurato con.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** puntatore al blocco di controllo server DHCP.  
- **iface_index:** indice corrispondente all'interfaccia di rete
- **subnet_mask:** Subnet mask per la rete client
- **default_gateway_address:** indirizzo IP del router del client
- **dns_server_address:** Server DNS per la rete del client

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Creazione del server DHCP riuscita.
- **NX_DHCP_SERVER_BAD_INTERFACE_INDEX:** l'indice (0xA1) non corrisponde agli indirizzi
- **NX_DHCP_INVALID_NETWORK_PARAMETERS:**(0xA3) Parametri di rete non validi
- NX_PTR_ERROR: (0x16) Input del puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Applicazione

### <a name="example"></a>Esempio

```c
/* Set network parameters for a specific interface. */
status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                                    NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                                    IP_ADDRESS(10,0,0,1));

/* If status is NX_SUCCESS network parameters were successfully set. */
```

## <a name="nx_dhcp_server_delete"></a>nx_dhcp_server_delete

Eliminare un'istanza del server DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_server_delete(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del server DHCP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore a un'istanza del server DHCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Eliminazione del server DHCP riuscita.
- NX_PTR_ERROR: (0x16) Input del puntatore non valido.
- NX_DHCP_PARAMETER_ERROR: (0x92) Input non puntatore non valido
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete a DHCP Server instance. */
status = nx_dhcp_server_delete(&dhcp_server);  
  
/* If status is NX_SUCCESS the DHCP Server instance was successfully deleted. */
```

## <a name="nx_dhcp_server_start"></a>nx_dhcp_server_start

Avviare l'elaborazione del server DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_server_start(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'elaborazione del server DHCP, che include la creazione di un socket UDP del server, l'associazione della porta DHCP e l'attesa della ricezione delle richieste DHCP client.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore a un'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Avvio del server riuscito.  
- **NX_DHCP_ALREADY_STARTED**: DHCP (0x93) già avviato.
- NX_PTR_ERROR: (0x16) Input del puntatore non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.
- NX_DHCP_PARAMETER_ERROR: (0x92) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Start the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_start(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully started. */
```

### <a name="see-also"></a>Vedere anche

nx_dhcp_create, nx_dhcp_delete, nx_dhcp_release, nx_dhcp_state_change_notify, nx_dhcp_stop, nx_dhcp_user_option_retrieve, nx_dhcp_user_option_convert

## <a name="nx_dhcp_server_stop"></a>nx_dhcp_server_stop

Arresta l'elaborazione del server DHCP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_server_stop(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta l'elaborazione del server DHCP, che include la ricezione di richieste client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr:** puntatore all'istanza del server DHCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Arresto DHCP riuscito.
- **NX_DHCP_ALREADY_STARTED**: DHCP (0x93) già avviato.
- NX_PTR_ERROR: (0x16) Input del puntatore non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.
- NX_DHCP_PARAMETER_ERROR: (0x92) Input non puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_stop(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully stopped. */
```
