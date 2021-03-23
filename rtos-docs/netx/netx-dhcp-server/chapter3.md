---
title: Capitolo 3-Descrizione dei servizi server DHCP NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi server DHCP NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d24c69cf6b8c2bb84b7155e49a54e8296ee662f0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822688"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-server-services"></a>Capitolo 3-Descrizione dei servizi server DHCP NetX di Azure RTO

Questo capitolo contiene una descrizione di tutti i servizi server DHCP di NetX.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_dhcp_server_create**: *creare un'istanza del server DHCP*
- **nx_dhcp_set_interface_network_parameters**: *impostare le opzioni del server DHCP per i parametri di rete critici per l'interfaccia specificata*
- **nx_dhcp_create_server_ip_address_list**: *creare un pool di indirizzi IP disponibili da assegnare all'interfaccia dei client DHCP*
- **nx_dhcp_clear_client_record**: *rimuovere il record client nel database del server*
- **nx_dhcp_server_delete**: *eliminare un'istanza di dhcpserver*
- **nx_dhcp_server_start**: *avviare o riprendere l'elaborazione del server DHCP*
- **nx_dhcp_server_stop**: *arrestare l'elaborazione del server DHCP*

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
> L'applicazione deve verificare che il pool di pacchetti creato per il servizio di creazione IP disponga di un payload di byte minimum548, escluso le intestazioni UDP, IP e Ethernet.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo server DHCP.  
- **ip_ptr**: puntatore all'istanza IP del server DHCP.
- **stack_ptr**: posizione dello stack del server DHCP del puntatore.
- **stack_size**: dimensioni dello stack di server DHCP
- **input_address_list**: puntatore all'elenco di indirizzi IP del server
- **name_ptr**: puntatore al nome del server DHCP
- **packet_pool_ptr**: puntatore al pool di pacchetti del server DHCP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la creazione del server DHCP è riuscita.
- **NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD**: (0xA9) payload del pacchetto troppo piccolo errore
- **NX_DHCP_NO_SERVER_OPTION_LIST**: l'elenco di opzioni del server (0x96) è vuoto
- NX_DHCP_PARAMETER_ERROR: (0x92) non è stato inserito alcun puntatore non valido
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.
- NX_PTR_ERROR: (0x16) input puntatore non valido.

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

Questo servizio crea un pool specifico di interfaccia di indirizzi IP disponibili per il server DHCP specificato da assegnare. Gli indirizzi IP di inizio e di fine devono corrispondere all'interfaccia di rete specificata. Il numero effettivo di indirizzi IP aggiunti può essere inferiore al totale degli indirizzi se l'elenco di indirizzi IP non è sufficientemente grande (impostazione configurabile dall'utente *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parametro).

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr** Puntatore al blocco di controllo server DHCP.  
- **iface_index**: indice corrispondente all'interfaccia di rete
- **start_ip_address**: primo indirizzo IP disponibile
- **end_ip_address**: ultimo indirizzo IP disponibile
- **addresses_added**: numero di indirizzi IP aggiunti all'elenco

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la creazione del server DHCP è riuscita.
- **NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: l'indice (0xA1) non corrisponde agli indirizzi
- **NX_DHCP_INVALID_IP_ADDRESS_LIST**: (0x99) input dell'indirizzo non valido
- NX_DHCP_INVALID_IP_ADDRESS: (0x9B) indirizzi di inizio/fine illogici
- NX_PTR_ERROR: (0x16) input puntatore non valido.

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

Rimuovi record client dal database del server

### <a name="prototype"></a>Prototipo

```c
UINT nx_dhcp_clear_client_record (NX_DHCP_SERVER *dhcp_ptr,
                                NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella il record client dal database del server.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo server DHCP.  
- **dhcp_client_ptr**: puntatore al client DHCP da rimuovere

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la creazione del server DHCP è riuscita.
- NX_PTR_ERROR: (0x16) input puntatore non valido.
- NX_CALLER_ERROR: (0x11) chiamante non thread del servizio

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

Questo servizio imposta i valori predefiniti per i parametri critici della rete per l'interfaccia specificata. Il server DHCP includerà queste opzioni nell'offerta e le risposte ACK al client DHCP. Se i parametri dell'interfaccia del set di host in cui è in esecuzione un server DHCP, i parametri vengono impostati come predefiniti come indicato di seguito: il router impostato sul gateway di interfaccia principale per il server DHCP stesso, l'indirizzo del server DNS per il server DHCP stesso e il subnet mask allo stesso modo in cui è configurata l'interfaccia server DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore al blocco di controllo server DHCP.  
- **iface_index**: indice corrispondente all'interfaccia di rete
- **subnet_mask**: subnet mask per la rete client
- **default_gateway_address**: indirizzo IP del router del client
- **dns_server_address**: server DNS per la rete del client

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la creazione del server DHCP è riuscita.
- **NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: l'indice (0xA1) non corrisponde agli indirizzi
- **NX_DHCP_INVALID_NETWORK_PARAMETERS**: (0xA3) parametri di rete non validi
- NX_PTR_ERROR: (0x16) input puntatore non valido.

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

Questo servizio Elimina un'istanza del server DHCP creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore a un'istanza del server DHCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione del server DHCP riuscita.
- NX_PTR_ERROR: (0x16) input puntatore non valido.
- NX_DHCP_PARAMETER_ERROR: (0x92) non è stato inserito alcun puntatore non valido
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.

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

Questo servizio avvia l'elaborazione del server DHCP, che include la creazione di un socket UDP del server, l'associazione della porta DHCP e l'attesa per la ricezione delle richieste DHCP del client.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'avvio del server è riuscito.  
- **NX_DHCP_ALREADY_STARTED**: (0X93) DHCP è già avviato.
- NX_PTR_ERROR: (0x16) input puntatore non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.
- NX_DHCP_PARAMETER_ERROR: (0x92) non è stato inserito alcun puntatore non valido

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

Questo servizio interrompe l'elaborazione del server DHCP, che include la ricezione di richieste client DHCP.

### <a name="input-parameters"></a>Parametri di input

- **dhcp_ptr**: puntatore all'istanza del server DHCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'arresto DHCP è riuscito.
- **NX_DHCP_ALREADY_STARTED**: (0X93) DHCP è già avviato.
- NX_PTR_ERROR: (0x16) input puntatore non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.
- NX_DHCP_PARAMETER_ERROR: (0x92) non è stato inserito alcun puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_stop(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully stopped. */
```
