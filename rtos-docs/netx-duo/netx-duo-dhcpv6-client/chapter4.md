---
title: Capitolo 4 - Azure RTOS client NetX Duo DHCPv6
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS client NetX Duo DHCPv6 (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6caf943f990f8fe5cbd2cd6139a1253fcaf47dc207141963e31a9e31864ef839
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791738"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-client-services"></a>Capitolo 4 - Azure RTOS client NetX Duo DHCPv6

Questo capitolo contiene una descrizione di tutti i Azure RTOS client NetX Duo DHCPv6 (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_dhcpv6_client_create: Creare** *un'istanza del client DHCPv6* 

- **nx_dhcpv6_client_delete: Eliminare** *un'istanza del client DHCPv6* 

- **nx_dhcpv6_create_ client_duid: Creare** *un DUID client DHCPv6* 

- **nx_dhcpv6 _add_client_ia: Aggiungere** *un indirizzo IA (Client Identity Address) DHCPv6* 

- **nx_dhcpv6 _create_client_ia:** (*Legacy Add a DHCPv6 Client Identity Address (IA))* 

- **nx_dhcpv6_create_client_iana: Creare** *un'associazione di identità client DHCPv6 per indirizzi non temporanei (IANA)* 

- **nx_dhcpv6_get_client_duid_time_id: ottenere** *l'ID ora dal DUID client DHCPv6* 

- **nx_dhcpv6_client_set_interface: impostare** *l'interfaccia di rete client per le comunicazioni con il server DHCPv6* 

- **nx_dhcpv6_get_IP_address: ottenere** *l'indirizzo IPv6 globale assegnato al client DHCPv6* 

- **nx_dhcpv6_get_lease_time_data: ottenere** T1, T2, durate valide e *preferite per l'indirizzo IPv6 globale* del client

- **nx_dhcpv6_get_valid_ip_address_lease_time: Ottenere** T1, T2, durate valide e preferite per *l'indice IPv6 del client DHCPv6* 

- **nx_dhcpv6_get_iana_lease_time: Ottenere** *T1 e T2 nell'associazione di identità (IANA) in lease al client DHCPv6* 

- **nx_dhcpv6_get_other_option_data: ottenere** *i dati dell'opzione specificati, ad* esempio il nome di dominio o il server del fuso orario 

- **nx_dhcpv6_get_DNS_server_address: ottenere l'indirizzo** del server DNS in corrispondenza dell'indice *specificato nell'elenco dei server DNS client DHCPv6* 

- **nx_dhcpv6_get_time_accrued: ottenere** il tempo accumulato dal lease globale degli indirizzi *IPv6 associato al client DHCPv6* 

- **nx_dhcpv6_get_time_server_address: ottenere** *l'indirizzo del server di tempo in corrispondenza dell'indice specificato nell'elenco del server ora client DHCPv6*

- **nx_dhcpv6_get_valid_ip_address_count: ottenere** *il numero di indirizzi IPv6 assegnati al client DHCPv6* 

- **nx_dhcpv6_reinitialize:** *reinizializzare DHCPv6* per riavviare la macchina a stati del client DHCPv6 ed eseguire di nuovo il protocollo DHCPv6 

- **nx_dhcpv6_request_confirm:** *Inviare una richiesta CONFIRM al server* 

- **nx_dhcpv6_request_inform_request:** Terminare *un messaggio INFORM REQUEST al server* 

- **nx_dhcpv6_request_release:** *Inviare una richiesta RELEASE al server* 

- **nx_dhcpv6_request_option_DNS_server: aggiungere** *l'opzione server DNS all'opzione Client per* richiedere i dati nei messaggi di richiesta al server 

- **nx_dhcpv6_request_option_FQDN: aggiungere** *l'opzione FQDN all'opzione Client per* richiedere i dati nei messaggi di richiesta al server 

- **nx_dhcpv6_request_option_domain_name: aggiungere** *l'opzione domain name all'opzione Client request data in request messages to the Server* 

- **nx_dhcpv6_request_option_time_server: aggiungere** *l'opzione del server di tempo all'opzione Client per* richiedere i dati nei messaggi di richiesta al server 

- **nx_dhcpv6_request_option_timezone: aggiungere** *l'opzione fuso orario ai dati di richiesta* dell'opzione Client nei messaggi di richiesta al server 

- **nx_dhcpv6_request_solicit:** *Inviare una richiesta DHCPv6 SOLICIT a qualsiasi server nella rete client (broadcast)* 

- **nx_dhcpv6_request_solicit_rapid: Inviare** *una richiesta DHCPv6 SOLICIT a* qualsiasi server nella rete client (broadcast) con l'opzione Commit rapido impostata 

- **nx_dhcpv6_resume: riprendere** *l'elaborazione del client DHCPv6* 

- **nx_dhcpv6_start: avviare** *l'attività thread client DHCPv6. Si noti che questo non equivale all'avvio della macchina a stati DHCPv6 e non invia una richiesta SOLICIT* 

- **nx_dhcpv6_stop: arrestare** *l'attività del thread del client DHCPv6* 

- **nx_dhcpv6_suspend: Sospendere** *l'attività thread client DHCPv6* 

- **nx_dhcpv6_set_time_accrued: impostare** il tempo accumulato per il lease dell'indirizzo *IPv6* client globale nel record client.

## <a name="nx_dhcpv6_client_create"></a>nx_dhcpv6_client_create

Creare un'istanza del client DHCPv6

### <a name="prototype"></a>Prototipo

```C
UINT  nx_dhcpv6_client_create(NX_DHCPV6 *dhcpv6_ptr, 
                        NX_IP *ip_ptr, CHAR *name_ptr, 
                        NX_PACKET_POOL *packet_pool_ptr, 
                        VOID *stack_ptr, ULONG stack_size,
                        VOID (*dhcpv6_state_change_notify)
                                 (struct NX_DHCPV6_STRUCT *dhcpv6_ptr, 
                                  UINT old_state, UINT new_state), 
                        VOID (*dhcpv6_server_error_handler)
                                 (struct NX_DHCPV6_STRUCT *dhcpv6_ptr, 
                                 UINT op_code, UINT status_code, 
                                 UINT message_type));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client DHCPv6, incluse le funzioni di callback.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore al blocco di controllo DHCPv6  

- **ip_ptr** Puntatore all'istanza IP client  

- **name_ptr** Puntatore al nome per l'istanza di DHCPv6

- **packet_pool_ptr** Puntatore al pool di pacchetti client

- **stack_ptr** Puntatore alla memoria dello stack del client

- **stack_size** Dimensioni della memoria dello stack del client

- **dhcpv6_state_change_notify** Puntatore alla funzione di callback richiamata quando il client avvia una nuova richiesta DHCPv6 al server

- **dhcpv6_server_error_handler** Puntatore alla funzione di callback richiamata quando il client riceve uno stato di errore dal server

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione client riuscita

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_DHCPV6_PARAM_ERROR (0xE93) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Create a DHCPv6 client instance without specifying link local or preferred
   global IP address.  */
status =  nx_dhcpv6_client_create(&dhcp_0, &ip_0, "DHCPv6 Client", &pool_0,
                                  NULL, NULL, pointer, 2048,        
                                  dhcpv6_state_change_notify, 
                                  dhcpv6_server_error_handler);

/* If status is NX_SUCCESS a DHCPv6 client instance was successfully
   created.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_client_delete

## <a name="nx_dhcpv6_client_delete"></a>nx_dhcpv6_client_delete

Eliminare un'istanza del client DHCPv6

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_client_delete(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del client DHCPv6 creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione DHCPv6 riuscita

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_DHCPV6_PARAM_ERROR (0xE93) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete a DHCPv6 client instance.  */
status =  nx_dhcpv6_client_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCPv6 client instance was successfully
   deleted.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_client_create

## <a name="nx_dhcpv6_client_set_interface"></a>nx_dhcpv6_client_set_interface

Imposta l'interfaccia di rete del client per DHCPv6

### <a name="prototype"></a>Prototipo

```C
UINT    nx_dhcpv6_client_set_interface(NX_DHCPV6 *dhcpv6_ptr, 
                                       UINT *interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'interfaccia di rete del client per la comunicazione con i server DHCPv6 sull'indice dell'interfaccia di input specificato.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **interface_index** Indice che indica l'interfaccia di rete

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'interfaccia è stata impostata correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_INVALID_INTERFACE (0x4C) Input dell'indice dell'interfaccia non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the client interface for DHCPv6 communication with the Server to 
   the secondary interface (1). */

UINT index = 1;
status = nx_dhcpv6_client_set_interface(&dhcp_0, index);

/* If status is NX_SUCCESS, the Client successfully set 
   the DHCPv6 network interface.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_client _create
- nx_dhcpv6_start

## <a name="nx_dhcpv6_client_set_destination_address"></a>nx_dhcpv6_client_set_destination_address

Imposta l'indirizzo di destinazione a cui deve essere inviato il messaggio DHCPv6

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_client_set_destination_address(NX_DHCPV6 *dhcpv6_ptr,
                                              NXD_ADDRESS *destination_address);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo di destinazione a cui deve essere inviato il messaggio DHCPv6. Per impostazione predefinita, ALL_DHCP_Relay_Agents_and_Servers(FF02::1:2).

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **destination_address** Indirizzo di destinazione

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'interfaccia è stata impostata correttamente

- NX_PTR_ERROR (0x07) Input puntatore non valido

- NX_DHCPV6_PARAM_ERROR errore di paramento (0xE93)

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the destination address where DHCPv6 message should be sent to. */

NXD_ADDRESS dest_address; /* Set the destination address.  */

status = nx_dhcpv6_client_set_destination_address(&dhcp_0, &dest_address);

/* If status is NX_SUCCESS, the Client successfully set the destination address. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_client _create
- nx_dhcpv6_start

## <a name="nx_dhcpv6_create_client_duid"></a>nx_dhcpv6_create_client_duid

Creare l'oggetto DUID client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_create_client_duid(NX_DHCPV6 *dhcpv6_ptr,
                                  UINT duid_type, UINT hardware_type,
                                  ULONG time);
```

### <a name="description"></a>Descrizione

Questo servizio crea il DUID client con i parametri di input. Se l'input temporale non viene fornito e il tipo duid indica il livello di collegamento con il tempo, questa funzione fornisce un tempo che include un fattore casuale per l'univocità. I tipi duid assegnati dal fornitore (enterprise) non sono supportati.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **duid_type** Tipo di DUID (hardware, aziendale e così via)

- **hardware_type** Hardware di rete, ad esempio IEEE 802

- **time** Valore usato nella creazione di un identificatore univoco

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) DUID client riuscito creato

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_DHCPV6_PARAM_ERROR (0xE93) Input non puntatore non valido

- NX_DHCPV6_UNSUPPORTED_DUID_TYPE (0xE98) TIPO DUID sconosciuto o non supportato 

- NX_DHCPV6_UNSUPPORTED_DUID_HW_TYPE (0xE99) Tipo di hardware DUID sconosciuto o non supportato

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Create the Client DUID from the supplied input.
   The time field is left NULL so the DHCPv6 client will provide one.  */
status = nx_dhcpv6_create_client_duid(&dhcp_0, NX_DHCPV6_DUID_TYPE_LINK_TIME,
                                      NX_DHCPV6_HW_TYPE_IEEE_802, 0)

/* If status is NX_SUCCESS the client DUID was successfully created.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_create_client_ia
- nx_dhcpv6_create_client_iana
- nx_dhcpv6_create_server_duid

## <a name="nx_dhcpv6_create_client_ia"></a>nx_dhcpv6_create_client_ia

Aggiungere un'associazione di identità al client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_create_client_ia(NX_DHCPV6 *dhcpv6_ptr,
                                NXD_ADDRESS *ipv6_address,
                                ULONG preferred_lifetime,
                                ULONG valid_lifetime);
```

### <a name="description"></a>Descrizione

Questo servizio è identico al servizio *nx_dhcpv6_add_client_ia* servizio. Aggiunge un'associazione di identità client compilando il record Client con i parametri forniti. Per richiedere la durata massima preferita e valida, impostare questi parametri su infinito. Per aggiungere più di un IA a un client DHCPv6, impostare il NX_DHCPV6_MAX_IA_ADDRESS su un valore maggiore del valore predefinito 1.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **ipv6_address** Puntatore al blocco di indirizzi IP NetX Duo

- **preferred_lifetime** Periodo di tempo prima che l'indirizzo IP sia deprecato

- **valid_lifetime** Periodo di tempo prima della scadenza dell'indirizzo IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta dell'IA client riuscita

- **NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xEAF) Indirizzo IA duplicato 

- **NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xEAE) IA supera il numero massimo di IA che il client IAs può archiviare

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) Indirizzo IA non valido (ad esempio null) in IA

- NX_DHCPV6_PARAM_ERROR (0xE93) Input non puntatore non valido


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Add an Client IA using the supplied input.   */
status = nx_dhcpv6_create_client_ia(&dhcp_0, &ipv6_address, 
NX_DHCPV6_PREFERRED_LIFETIME, NX_DHCPV6_VALID_LIFETIME);

/* If status is NX_SUCCESS the client IA was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_add_client_duid
- nx_dhcpv6_create_server_duid
- nx_dhcpv6_create_client_iana

## <a name="nx_dhcpv6_create_client_iana"></a>nx_dhcpv6_create_client_iana

Creare un'associazione di identità (non temporanea) per il client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_create_client_iana(NX_DHCPV6 *dhcpv6_ptr, 
                                  UINT IA_ident, ULONG T1, ULONG T2);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'associazione IANA (Client Non Temporary Identity Association) dai parametri forniti. Per impostare le volte T1 e T2 su un valore massimo (infinito) nelle richieste del client DHCPv6, impostare questi parametri su NX_DHCPV6_INFINITE_LEASE. 

> [!NOTE]
> Un client ha un solo IANA.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **IA_ident** Identificatore univoco dell'associazione di identità

- **T1** Quando il client deve avviare il rinnovo dell'indirizzo IPv6

- **T2** Quando il client deve avviare la riassociazione dell'indirizzo IPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'IANA è stata creata correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_DHCPV6_PARAM_ERROR (0xE93) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Create the Client IANA from the supplied input.  */
status = nx_dhcpv6_create_client_iana(&dhcp_0, DHCPV6_IA_ID, DHCPV6_T1,   
                                      DHCPV6_T2);

/* If status is NX_SUCCESS the client IANA was successfully created.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_create_client_duid
- nx_dhcpv6_create_server_duid
- nx_dhcpv6_add_client_ia

## <a name="nx_dhcpv6_add_client_ia"></a>nx_dhcpv6_add_client_ia 

Aggiungere un'associazione di identità al client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_add_client_ia(NX_DHCPV6 *dhcpv6_ptr, 
                             NXD_ADDRESS *ipv6_address, 
                             ULONG preferred_lifetime, 
                             ULONG valid_lifetime);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'associazione di identità client compilando il record Client con i parametri specificati. Per richiedere la durata massima preferita e valida, impostare questi parametri su infinito. Per aggiungere più di un IA a un client DHCPv6, impostare il NX_DHCPV6_MAX_IA_ADDRESS su un valore maggiore del valore predefinito 1.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **ipv6_address** Puntatore al blocco di indirizzi IP NetX Duo

- **preferred_lifetime** Periodo di tempo prima che l'indirizzo IP sia deprecato

- **valid_lifetime** Periodo di tempo prima della scadenza dell'indirizzo IP 

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta di IA client con esito positivo

- **NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xEAF) indirizzo IA duplicato 

- **NX_DHCPV6_REACHED_MAX_IA_ADDRESS** IA (0xEAE) supera il numero massimo di IA che il client IAs può archiviare

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) Indirizzo IA non valido (ad esempio null) in IA

- NX_DHCPV6_PARAM_ERROR (0xE93) Input non puntatore non valido

 
### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Add an Client IA using the supplied input.   */
status = nx_dhcpv6_add_client_ia(&dhcp_0, &ipv6_address, 
                                 NX_DHCPV6_PREFERRED_LIFETIME,
                                 NX_DHCPV6_VALID_LIFETIME);

/* If status is NX_SUCCESS the client IA was successfully added.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_create_client_duid
- nx_dhcpv6_create_server_duid
- nx_dhcpv6_create_client_iana

## <a name="nx_dhcpv6_get_client_duid_time_id"></a>nx_dhcpv6_get_client_duid_time_id

Recupera l'ID ora dal DUID del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_get_client_duid_time_id(NX_DHCPV6 *dhcpv6_ptr, ULONG *time_id);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il campo id ora dal DUID client. Se l'applicazione deve prima *chiamare nx_dhcpv6_create_client_duid*, per compilare il DUID client nell'istanza del client DHCPv6 oppure avrà un valore Null per questo campo. Lo scopo è che l'applicazione salverà questi dati e presenterà lo stesso DUID client al server, incluso il campo dell'ora, tra un riavvio e l'altro.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **time_id** Puntatore al campo ora DUID client

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati di lease IP sono stati recuperati correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Retrieve the time ID from the Client DUID.  */
status = nx_dhcpv6_get_client_duid_time_id(&dhcp_0, &time_ID);

/* If status is NX_SUCCESS the time ID was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_time_lease_data
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_get_ip_address"></a>nx_dhcpv6_get_IP_address

Recupera l'indirizzo IPv6 globale del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_get_IP_address(NX_DHCPV6 *dhcpv6_ptr, 
                              NXD_ADDRESS *ip_address);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IPv6 globale del client. Se il client non ha un indirizzo valido, viene restituito uno stato di errore. Se un client ha più di un indirizzo IPv6 globale, viene restituito l'indirizzo IPv6 primario.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **ip_address** Puntatore all'indirizzo IPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) IPv6 assegnato correttamente

- **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) IPv6 non è valido

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UINT address_status;
UINT address_index;

/* Retrieve the client’s assigned IP address.  */
status = nx_dhcpv6_get_IP_address(&dhcp_0, &ipv6_address);

/* If status is NX_SUCCESS the client IP address was assigned.
   Now register it with NetX Duo on the primary interface (index zero). 
   The address index is returned in the address_index field*/
status = nxd_ipv6_address_set(&ip_0, 0, &ipv6_address, 64, &address_index);
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_client_duid_time_id
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_get_lease_time_data"></a>nx_dhcpv6_get_lease_time_data

Recupera i dati relativi al tempo di lease degli indirizzi IA del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_get_lease_time_data(NX_DHCPV6 *dhcpv6_ptr, ULONG *T1, 
                                   ULONG *T2, ULONG *preferred_lifetime, 
                                   ULONG *valid_lifetime);
```

### <a name="description"></a>Descrizione

Questo servizio recupera i dati relativi all'ora dell'indirizzo IA globale del client. Se lo stato dell'indirizzo IA del client non è valido, i dati sull'ora vengono impostati su zero e viene restituito uno stato di completamento corretto. Se un client ha più di un indirizzo IPv6 globale, vengono restituiti i dati dell'indirizzo IA primario.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **T1** Puntatore all'ora di rinnovo dell'indirizzo IA

- **T2** Puntatore all'ora di riassociata dell'indirizzo IA

- **preferred_lifetime** Puntatore all'ora in cui l'indirizzo IA è deprecato

- **valid_lifetime** Puntatore all'ora in cui l'indirizzo IA è scaduto

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) i dati di lease IA recuperati correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Retrieve the client’s assigned IA lease data.  */
status = nx_dhcpv6_get_lease_time_data(&dhcp_0, &T1, &T2, &preferred_lifetime, 
                                       &valid_lifetime);

/* If status is NX_SUCCESS the client IA address lease data was retrieved.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_client_duid_time_id
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_time_accrued
- nx_dhcpv6_get_iana_lease_time

## <a name="nx_dhcpv6_get_iana-lease_time"></a>nx_dhcpv6_get_iana lease_time

Recuperare i dati relativi al tempo di lease IANA del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_get_iana_lease_time(NX_DHCPV6 *dhcpv6_ptr, ULONG *T1, 
                                    ULONG *T2);
```

### <a name="description"></a>Descrizione

Questo servizio recupera i dati di durata lease IA-NA globali del client (T1 e T2). Se nessuno degli indirizzi IA-NA client ha uno stato di indirizzo valido, i dati relativi all'ora vengono impostati su zero e viene restituito uno stato di completamento corretto. Se un client ha più di un indirizzo IPv6 globale, vengono restituiti i dati dell'indirizzo IA primario.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **T1** Puntatore all'ora per l'avvio del rinnovo del lease

- **T2** Puntatore all'ora per l'avvio del riassociazione del lease

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** dati di lease IANA 0x00 (0x00)

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Retrieve the client’s assigned IANA lease data.  */
status = nx_dhcpv6_get_iana_lease_time(&dhcp_0, &T1, &T2);

/* If status is NX_SUCCESS the client IA address lease data was retrieved.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_client_duid_time_id
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_time_accrued
- nx_dhcpv6_get_lease_time_data

## <a name="nx_dhcpv6_get_valid_ip_address_count"></a>nx_dhcpv6_get_valid_ip_address_count

Recuperare un conteggio degli indirizzi IA validi del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_get_valid_ip_address_count(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT *address_count);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il conteggio degli indirizzi IPv6 validi del client. Un indirizzo IPv6 valido viene associato (assegnato) al client e registrato con l'istanza IP.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **address_count** Puntatore al numero di indirizzi da restituire

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** dati di lease IANA 0x00 (0x00)

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UINT address_count; 

/* Retrieve the count of valid IA-NA addresses.  */
status = nx_dhcpv6_get_valid_ip_address_count(&dhcp_0, &address_count);

/* If status is NX_SUCCESS the client IA address count was retrieved.  */
```

## <a name="nx_dhcpv6_get_valid_ip_address_lease_time"></a>nx_dhcpv6_get_valid_ip_address_lease_time

Recuperare i dati IA client in base all'indice degli indirizzi

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_get_valid_ip_address_lease_time(NX_DHCPV6 *dhcpv6_ptr, 
                                               UINT address_index,
                                               NXD_ADDRESS *ip_address,
                                               ULONG *preferred_lifetime,
                                               ULONG *valid_lifetime);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IA del client e i dati di lease in base all'indice dell'indirizzo. Se viene fornito un indice non valido o l'indirizzo IPv6 in corrispondenza di tale indice non è valido, il servizio restituisce un errore NX_DHCPV6_IA_ADDRESS_NOT_VALID errore.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **address_index** Indice nella tabella IA DHCPv6

- **ip_address** Puntatore all'indirizzo IPv6 da recuperare

- **preferred_lifetime** Puntatore all'ora in cui l'indirizzo IA è deprecato

- **valid_lifetime** Puntatore all'ora in cui l'indirizzo IA è scaduto

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) IANA recuperati correttamente

- **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) Indice non valido o nessun indirizzo IPv6 valido nell'indice specificato 

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UINT address_index = 1; 
NXD_ADDRESS *ip_address;

/* Retrieve the IPv6 address, and valid and preferred lifetime for the IA record
   Saved at index 1 in the DHCPv6 table.  */
status = nx_dhcpv6_get_valid_ip_address_lease_time(&dhcp_0, address_index, 
                                                   &ip_address, 
                                                   &preferred_lifetime,  
                                                   &valid_lifetime);

/* If status is NX_SUCCESS the client IA address and lease data were retrieved.  */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_iana_lease_time
- nx_dhcpv6_get_lease_time_data

## <a name="nx_dhcpv6_get_dns_server_address"></a>nx_dhcpv6_get_DNS_server_address

Recupera l'indirizzo del server DNS 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_get_DNS_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index,
                                      NXD_ADDRESS *server_address);
```

### <a name="description"></a>Descrizione

Questo servizio recupera i dati degli indirizzi IPv6 del server DNS in corrispondenza dell'indice specificato nell'elenco Client. Se l'elenco non contiene un indirizzo del server in corrispondenza dell'indice, viene restituito un errore. L'indice non può superare le dimensioni dell'elenco server DNS specificato dall'opzione configurabile dall'utente NX_DHCPV6_NUM_DNS_SERVERS.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **index** Indice nell'elenco dei server DNS

- **server_address** Puntatore al buffer degli indirizzi del server

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) recuperato correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Retrieve the DNS server at the specified index in the list. */

UINT index = 0;
NXD_ADDRESS server_address;


        status = nx_dhcpv6_get_DNS_server_address(&dhcp_0, index, &server_address);

/* If status == NX_SUCCESS, the DNS server IP address successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_get_other_option_data"></a>nx_dhcpv6_get_other_option_data

Recupera i dati dell'opzione DHCPv6 

### <a name="prototype"></a>Prototipo

```C
UINT  nx_dhcpv6_get_other_option_data(NX_DHCPV6 *dhcpv6_ptr, 
                                      UINT option_code, UCHAR *buffer);
```

### <a name="description"></a>Descrizione

Questo servizio recupera i dati dell'opzione DHCPv6 da un messaggio DHCPv6 per il codice di opzione specificato.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **option** code Codice di opzione per cui recuperare i dati

- **buffer** Puntatore al buffer in cui copiare i dati 

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati dell'opzione sono stati recuperati correttamente

- **NX_DHCPV6_UNKNOWN_OPTION** (0xEAB) Codice opzione sconosciuto/non supportato

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_DHCPV6_PARAM_ERROR (0xE93) Input non puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Retrieve the option data specified by the input option code. */
status = nx_dhcpv6_get_other_option_data(&dhcp_0, option_code, buffer);

/* If status is NX_SUCCESS the option data was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_get_time_accrued"></a>nx_dhcpv6_get_time_accrued

Recupera il tempo accumulato per il lease dell'indirizzo IP del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_get_time_accrued(NX_DHCPV6 *dhcpv6_ptr, ULONG *time_accrued);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il tempo accumulato per il lease dell'indirizzo IPv6 del client. La funzione controlla tutti gli indirizzi IPv6 assegnati al client per il primo indirizzo valido. Se non viene trovato alcun indirizzo valido, viene restituito un valore zero per il tempo accumulato.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **time_accrued** Puntatore al tempo accumulato nel lease IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Tempo accumulato recuperato

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Retrieve time accrued time on the Client address lease. */
status = nx_dhcpv6_get_time_accrued(&dhcp_0, &time_accrued);

/* If status is NX_SUCCESS the time accrued on the client IP address 
   lease was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_set_time_accrued

## <a name="nx_dhcpv6_get_time_server_address"></a>nx_dhcpv6_get_time_server_address

Recupera l'indirizzo del server di tempo 

### <a name="prototype"></a>Prototipo

```C
UINT  nx_dhcpv6_get_time_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index, 
                                        NXD_ADDRESS *server_address);
```

### <a name="description"></a>Descrizione

Questo servizio recupera i dati dell'indirizzo IPv6 del server di tempo in corrispondenza dell'indice specificato nell'elenco Client. Se l'elenco non contiene un indirizzo del server in corrispondenza dell'indice, viene restituito un errore. L'indice non può superare le dimensioni dell'elenco server di tempo specificato dall'opzione configurabile dall'utente NX_DHCPV6_NUM_TIME_SERVERS.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **index** Indice nell'elenco del server di tempo

- **server_address** Puntatore al buffer degli indirizzi del server

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) recuperato correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Retrieve the Time server at the specified index in the list. */

UINT index = 0;
NXD_ADDRESS server_address;


      status = nx_dhcpv6_get_time_server_address(&dhcp_0, index, &server_address);

/* If status == NX_SUCCESS, the Time server IP address successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_time_accrued
- nx_dhcpv6_get_DNS_server_address

## <a name="nx_dhcpv6_reinitialize"></a>nx_dhcpv6_reinitialize

Rimuovere l'indirizzo IP del client dalla tabella IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_reinitialize(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio reinizializza il client per riavviare la macchina a stati DHCPv6 ed eseguire nuovamente il protocollo DHCPv6. Questa operazione non è necessaria se il client non ha avviato in precedenza la macchina a stati DHPCv6 o non è stato assegnato alcun indirizzo IPv6. Gli indirizzi salvati nel client DHCPv6 e registrati con l'istanza IP vengono entrambi cancellati.

> [!NOTE]
> L'applicazione deve comunque avviare il client DHCPv6 usando il *servizio nx_dhcpv6_start* e iniziare la richiesta di assegnazione di indirizzi IPv6 *chiamando nx_dhcpv6_request_solicit*.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rimozione dell'indirizzo

- **NX_DHCPV6_ALREADY_STARTED** client DHCPv6 (0xE91) è già in esecuzione

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Clear the assigned IP address(es) from the Client and the IP instance */
status = nx_dhcpv6_reinitialize(&dhcp_0);

/* If status is NX_SUCCESS the Client IP address was successfully removed. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_stop
- nx_dhcpv6_start

## <a name="nx_dhcpv6_request_confirm"></a>nx_dhcpv6_request_confirm

Elaborare lo stato CONFIRM del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_confirm(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia una richiesta CONFIRM. Se viene ricevuta una risposta dal server, il client DHCPv6 aggiorna i parametri di lease con i dati ricevuti.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) CONFIRM inviato ed elaborato correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send a CONFIRM message to the Server. */
status = nx_dhcpv6_request_confirm(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the CONFIRM message. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_inform_request
- nx_dhcpv6_request_release
- nx_dhcpv6_request_solicit


## <a name="nx_dhcpv6_request_inform_request"></a>nx_dhcpv6_request_inform_request

Elaborare lo stato INFORM REQUEST del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_inform_request(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia un messaggio INFORM REQUEST. Se viene ricevuta una risposta, quando ne viene ricevuta una, la risposta viene elaborata per determinarne la validità e il server ha concesso la richiesta. L'istanza client viene quindi aggiornata con le informazioni sul server in base alle esigenze.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) INFORM REQUEST creato ed elaborato correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send an INFORM REQUEST message to the server. */
status = nx_dhcpv6_request_inform_request(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the INFORM REQUEST 
   message and processed the reply. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_confirm

## <a name="nx_dhcpv6_request_option_dns_server"></a>nx_dhcpv6_request_option_DNS_server

Aggiungere un server DNS alla richiesta dell'opzione DHCPv6

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_option_DNS_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge l'opzione per la richiesta di informazioni sul server DNS alla richiesta dell'opzione DHCPv6. Se la risposta del server include i dati del server DNS, il client archivierà il server DNS se ha spazio a tale scopo. Il numero di server DNS che il client può archiviare è determinato dall'opzione configurabile NX_DHCPV6_NUM_DNS_SERVERS il cui valore predefinito è 2.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS(0x00)** è inclusa l'opzione del server DNS

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the DNS server option in Client requests. */
nx_dhcpv6_request_option_DNS_server(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_option_domain_name
- nx_dhcpv6_request_option_time_server
- nx_dhcpv6_request_option_timezone

## <a name="nx_dhcpv6_request_option_fqdn"></a>nx_dhcpv6_request_option_FQDN

Aggiungere l'opzione Nome di dominio completo all'elenco di richieste di opzioni

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_option_FQDN(NX_DHCPV6 *dhcpv6_ptr, UCHAR *domain_name, 
UINT op);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge l'opzione per aggiungere il nome di dominio completo del client alla richiesta di opzione DHCPv6. Per l'opzione FQDN sono disponibili tre opzioni:

- NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR 0 Aggiornare il mapping degli indirizzi da FQDN a IPv6 per FQDN e indirizzi usati dal client.

- NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE 1 Aggiornare il mapping degli indirizzi da FQDN a IPv6 per FQDN e indirizzi usati dal client al server.

- NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE 2 Richiedere al server di non eseguire aggiornamenti DNS per conto del client.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **domain_name** Stringa contenente il nome di dominio

- **op** Tipo di opzione FQDN da applicare (vedere l'elenco precedente)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS'opzione** FQDN 0x00 (0x00)

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the FQDN option in Client DHCPv6 request. */
nx_dhcpv6_request_option_FQDN(&dhcp_0, “DHCPv6_Client”, 
                              NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE);
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_option_domain_name
- nx_dhcpv6_request_option_time_server
- nx_dhcpv6_request_option_timezone

## <a name="nx_dhcpv6_request_option_domain_name"></a>nx_dhcpv6_request_option_domain_name

Opzione Aggiungi nome di dominio alla richiesta di opzione DHCPv6

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_option_domain_name(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge l'opzione domain name alla richiesta di opzione nei messaggi di richiesta client. Se la risposta del server include i dati del nome di dominio, il client archivierà le informazioni sul nome di dominio se le dimensioni del nome di dominio sono all'interno delle dimensioni del buffer per contenere il nome di dominio. Questa dimensione del buffer è un'opzione configurabile (NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE) con un valore predefinito di 30 byte.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Set di opzioni Nome di dominio

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the domain name option in Client requests. */
nx_dhcpv6_request_option_domain_name(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_option_DNS_server
- nx_dhcpv6_request_option_time_server
- nx_dhcpv6_request_option_timezone

## <a name="nx_dhcpv6_request_option_time_server"></a>nx_dhcpv6_request_option_time_server

Impostare i dati del server di tempo come richiesta facoltativa

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_option_time_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge l'opzione per le informazioni sul server di tempo alla richiesta di opzione dei messaggi di richiesta client. Se la risposta del server include i dati del server tim, il client archivierà il server di tempo se ha spazio a tale scopo. Il numero di server di tempo che il client può archiviare è determinato dall'opzione configurabile

NX_DHCPV6_NUM_TIME _SERVERS il cui valore predefinito è 1.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** aggiunta l'0x00 server di tempo (0x00)

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the time server option in Client request messages. */
nx_dhcpv6_request_option_time_server(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_option_DNS_server
- nx_dhcpv6_request_option_domain_name
- nx_dhcpv6_request_option_timezone

## <a name="nx_dhcpv6_request_option_timezone"></a>nx_dhcpv6_request_option_timezone

Impostare i dati del fuso orario come richiesta facoltativa

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_option_timezone(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge l'opzione per richiedere informazioni sul fuso orario alla richiesta dell'opzione Client. Se la risposta del server include i dati sul fuso orario, il client archivierà le informazioni sul fuso orario se le dimensioni del fuso orario sono all'interno delle dimensioni del buffer per contenere il fuso orario. Questa dimensione del buffer è un'opzione configurabile (NX_DHCPV6_ TIME_ZONE _BUFFER_SIZE) con un valore predefinito di 10 byte.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Fuso orario aggiunto

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set time zone option in Client request messages. */
nx_dhcpv6_request_option_timezone(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_option_DNS_server
- nx_dhcpv6_request_option_domain_name
- nx_dhcpv6_request_option_time_server

## <a name="nx_dhcpv6_request_release"></a>nx_dhcpv6_request_release

Inviare un messaggio DHCPv6 RELEASE

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_release(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia un messaggio RELEASE nella rete client. Se il messaggio viene inviato correttamente, viene restituito uno stato di esito positivo. Un completamento riuscito non significa che il client ha ricevuto una risposta o ha ancora ricevuto un indirizzo IPv6. L'attività thread client DHCPv6 attende una risposta da un server DHCPv6. Se ne riceve una, verifica che la risposta sia valida e archivia i dati nel record client.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) MESSAGGIO RELEASE inviato correttamente

- **NX_DHCPV6_NOT_STARTED** (0xE92) Attività client DHCPv6 non avviata

- **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) Indirizzo non associato al client

- **NX_INVALID_INTERFACE** (0x4C) Non trovato nella tabella degli indirizzi IP

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send an RELEASE message to the Server. */
status = nx_dhcpv6_request_release(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the RELEASE message. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_confirm
- nx_dhcpv6_request_inform_request
- nx_dhcpv6_request_solicit

## <a name="nx_dhcpv6_request_solicit"></a>nx_dhcpv6_request_solicit

Inviare un messaggio SOLICIT

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_solicit(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia un messaggio SOLICIT in rete. Se il messaggio viene inviato correttamente, viene restituito uno stato di esito positivo. Un completamento riuscito non significa che il client ha ricevuto una risposta o ha ancora ricevuto un indirizzo IPv6. L'attività thread client DHCPv6 attende una risposta (un messaggio ADVERTISE) da un server DHCPv6. Se ne riceve uno, verifica che la risposta sia valida, archivia i dati nel record Client e alza di livello il client allo stato REQUEST.

> [!NOTE] 
> Se l'opzione Rapid Commit è impostata, il client DHCPv6 passa direttamente allo stato Bound se riceve un messaggio SERVER ADVERTISE valido. Per altri dettagli, vedere *la descrizione nx_dhcpv6_request_solicit_rapid* servizio.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) SOLICIT inviato correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

## <a name="nx_dhcpv6_request_solicit_rapid"></a>nx_dhcpv6_request_solicit_rapid

Inviare un messaggio SOLICIT con l'opzione Rapid Commit

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_request_solicit_rapid(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia un messaggio SOLICIT in rete con l'opzione Rapid Commit impostata. Se il messaggio viene inviato correttamente, viene restituito uno stato di esito positivo. Un completamento riuscito non significa che il client ha ricevuto una risposta o ha ancora ricevuto un indirizzo IPv6. L'attività thread client DHCPv6 attende una risposta (un messaggio ADVERTISE) da un server DHCPv6. Se ne riceve uno, verifica che la risposta sia valida, archivia i dati nel record Client e alza di livello il client allo stato BOUND.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) SOLICIT inviato correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit_rapid(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_request_solicit
- nx_dhcpv6_request_confirm
- nx_dhcpv6_request_inform_request
- nx_dhcpv6_request_release

## <a name="nx_dhcpv6_resume"></a>nx_dhcpv6_resume

Riprendere l'attività del client DHCPv6 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_resume(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio riprende l'attività del thread del client DHCPv6. Lo stato corrente del client DHCPv6 verrà elaborato (ad esempio Bound, Solicit)

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il client è stato ripreso correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) Deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Resume the DHCPv6 Client task. */
status = nx_dhcpv6_resume(&dhcp_0);

/* If status is NX_SUCCESS the Client thread task successfully resumed. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_start
- nx_dhcpv6_stop
- nx_dhcpv6_suspend

## <a name="nx_dhcpv6_set_-time_accrued"></a>nx_dhcpv6_set_ time_accrued

Imposta l'ora accumulata nel lease dell'indirizzo IP del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_set_time_accrued(NX_DHCPV6 *dhcpv6_ptr,
                                ULONG time_accrued);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il tempo accumulato nell'indirizzo IP globale del client da quando è stato assegnato dal server. Deve essere usato solo se un client è attualmente associato a un indirizzo IPv6 assegnato.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

- **time_accrued** Tempo accumulato nel lease IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il tempo accumulato è stato impostato correttamente

- NX_PTR_ERROR (0x16) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set time accrued since client’s assigned IP address was assigned. */
status = nx_dhcpv6_set_time_accrued(&dhcp_0, time_accrued);

/* If status is NX_SUCCESS the time accrued on the client IP address lease was 
   successfully set. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_start"></a>nx_dhcpv6_start

Avviare l'attività client DHCPv6 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_start(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia l'attività client DHCPv6 e prepara il client per l'esecuzione del protocollo DHCPv6. Verifica che l'istanza del client disponga di informazioni sufficienti, ad esempio un DUID client, crea e associa il socket UDP per l'invio e la ricezione di messaggi DHCPv6 e attiva timer per tenere traccia dell'ora della sessione e della scadenza del lease IPv6 corrente.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client (0x00) avviato correttamente

- **NX_DHCPV6_MISSING_REQUIRED_OPTIONS** (0xEA9) Mancano le opzioni obbligatorie

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start the DHCPv6 Client task. */
status = nx_dhcpv6_start(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully started. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_resume
- nx_dhcpv6_suspend
- nx_dhcpv6_stop
- nx_dhcpv6_reinitialize

## <a name="nx_dhcpv6_stop"></a>nx_dhcpv6_stop

Arrestare l'attività client DHCPv6 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_stop(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta l'attività client DHCPv6 e cancella i conteggi di ritrasmissione, gli intervalli massimi di ritrasmissione, disattiva i timer di scadenza della sessione e del lease e disassocia la porta socket del client DHCPv6. Per riavviare il client, è prima necessario arrestare e facoltativamente reinizializzare il client prima di avviare un'altra sessione con qualsiasi server DHCPv6. Per altri dettagli, vedere la sezione Esempio piccolo.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client (0x00) arrestato correttamente

- **NX_DHCPV6_NOT_STARTED** thread client (0xE92) non avviato

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop the DHCPv6 Client task. */
status = nx_dhcpv6_start(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully stopped. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_resume
- nx_dhcpv6_suspend
- nx_dhcpv6_reinitialize
- nx_dhcpv6_start

## <a name="nx_dhcpv6_suspend"></a>nx_dhcpv6_suspend

Sospendere l'attività client DHCPv6 

### <a name="prototype"></a>Prototipo

```C
UINT nx_dhcpv6_suspend(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio sospende l'attività del client DHCPv6 e qualsiasi richiesta in corso di elaborazione. I timer vengono disattivati e lo stato del client è impostato su non in esecuzione.

### <a name="input-parameters"></a>Parametri di input

- **dhcpv6_ptr** Puntatore all'istanza del client DHCPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client (0x00) sospeso correttamente

- **NX_DHCPV6_NOT_STARTED** client (0XE92) non in esecuzione, quindi non può essere sospeso

- NX_PTR_ERROR (0x16) Input puntatore non valido

- NX_CALLER_ERROR (0x11) deve essere chiamato dal thread

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Suspend the DHCPv6 Client task. */
status = nx_dhcpv6_suspend(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully suspended. */
```

### <a name="see-also"></a>Vedere anche

- nx_dhcpv6_resume
- nx_dhcpv6_start
- nx_dhcpv6_reinitialize
- nx_dhcpv6_stop
