---
title: Capitolo 3 - Descrizione dei Azure RTOS agente SNMP di NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi di NetX Duo SNMP Agent (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b24776c2eb25a53195ea4eb452497b23b933e4ab3f9f0a379ea64d8469c1c971
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790123"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-snmp-agent-services"></a>Capitolo 3 - Descrizione dei Azure RTOS agente SNMP di NetX Duo

Questo capitolo contiene una descrizione di tutti i Azure RTOS agente SNMP di NetX Duo (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- [nx_snmp_agent_auth_trap_key_use](#nx_snmp_agent_auth_trap_key_use)
   - *Specificare la chiave di autenticazione (solo SNMP v3) per i messaggi trap*
- [nx_snmp_agent_authenticate_key_use](#nx_snmp_agent_authenticate_key_use)
   - *Specificare la chiave di autenticazione (solo SNMP v3) per i messaggi di risposta*
- [nx_snmp_agent_community_get](#nx_snmp_agent_community_get)
   - *Recuperare il nome della community*
- [nx_snmp_agent_context_engine_set](#nx_snmp_agent_context_engine_set)
   - *Impostare il motore di contesto (solo SNMP v3)*
- [nx_snmp_agent_context_name_set](#nx_snmp_agent_context_name_set)
   - *Impostare il nome del contesto (solo SNMP v3)*
- [nx_snmp_agent_create](#nx_snmp_agent_create)
   - *Creare l'agente SNMP*
- [nx_snmp_agent_current_version_get](#nx_snmp_agent_current_version_get)
   - *Ottenere la versione SNMP del pacchetto ricevuto*
- [nx_snmp_agent_request_get_type_test](#nx_snmp_agent_request_get_type_test)
   - *Indicare se l'ultima richiesta SNMP è di tipo GET o SET*
- [nx_snmp_agent_private_string_test](#nx_snmp_agent_private_string_test)
   - *Determinare se la stringa corrisponde alla stringa privata dell'agente*
- [nx_snmp_agent_public_string_test](#nx_snmp_agent_public_string_test)
   - *Determinare se la stringa corrisponde alla stringa pubblica dell'agente*
- [nx_snmp_agent_set_interface](#nx_snmp_agent_set_interface)
   - *Impostare l'interfaccia di rete per la messaggistica SNMP*
- [nx_snmp_agent_private_string_set](#nx_snmp_agent_private_string_set)
   - *Impostare la stringa della community privata dell'agente SNMP*
- [nx_snmp_agent_public_string_set](#nx_snmp_agent_public_string_set)
   - *Impostare la stringa della community pubblica dell'agente SNMP*
- [nx_snmp_agent_version_set](#nx_snmp_agent_version_set)
   - *Impostare lo stato dell'agente SNMP per tutte le versioni di SNMP*
- [nx_snmp_agent_delete](#nx_snmp_agent_delete)
   - *Eliminare l'agente SNMP*
- [nx_snmp_agent_md5_key_create](#nx_snmp_agent_md5_key_create)
   - *Creare una chiave md5 (solo SNMP v3)*
- [nx_snmp_agent_md5_key_create_extended](#nx_snmp_agent_md5_key_create_extended)
   - *Creare una chiave md5 (solo SNMP v3)*
- [nx_snmp_agent_priv_trap_key_use](#nx_snmp_agent_priv_trap_key_use)
   - *Specificare la chiave di crittografia (solo SNMP v3) per i messaggi trap*
- [nx_snmp_agent_privacy_key_use](#nx_snmp_agent_privacy_key_use)
   - *Specificare la chiave di crittografia (solo SNMP v3) per i messaggi di risposta*
- [nx_snmp_agent_sha_key_create](#nx_snmp_agent_sha_key_create)
   - *Creare una chiave sha (solo SNMP v3)*
- [nx_snmp_agent_sha_key_create_extended](#nx_snmp_agent_sha_key_create_extended)
   - *Creare una chiave sha (solo SNMP v3)*
- [nx_snmp_agent_start](#nx_snmp_agent_start)
   - *Avviare l'agente SNMP*
- [nx_snmp_agent_stop](#nx_snmp_agent_stop)
   - *Arrestare l'agente SNMP*
- [nx_snmp_agent_trap_send](#nx_snmp_agent_trap_send)
   - *Inviare trap SNMP v1 (solo IPv4)*
- [nx_snmp_agent_trapv2_send](#nx_snmp_agent_trapv2_send)
   - *Inviare trap SNMP v2 (solo IPv4)*
- [nx_snmp_agent_trapv2_oid_send](#nx_snmp_agent_trapv2_oid_send)
   - *Inviare trap SNMP v2 (solo IPv4) specificando l'OID*
- [nx_snmp_agent_trapv3_send](#nx_snmp_agent_trapv3_send)
   - *Invia trap SNMP v3 (solo IPv4)*
- [nx_snmp_agent_trapv3_oid_send](#nx_snmp_agent_trapv3_oid_send)
   - *Inviare trap SNMP v2 (solo IPv4) specificando l'OID*
- [nxd_snmp_agent_trap_send](#nxd_snmp_agent_trap_send)
   - *Inviare trap SNMP v1 (IPv4 e IPv6)*
- [nxd_snmp_agent_trapv2_send](#nxd_snmp_agent_trapv2_send)
   - *Inviare trap SNMP v2 (IPv4 e IPv6)*
- [nxd_snmp_agent_trapv2_oid_send](#nxd_snmp_agent_trapv2_oid_send)
   - *Inviare trap SNMP v2 (IPv4/IPv6) specificando l'OID*
- [nxd_snmp_agent_trapv3_send](#nxd_snmp_agent_trapv3_send)
   - *Inviare trap SNMP v3 (IPv4 e IPv6)*
- [nxd_snmp_agent_trapv3_oid_send](#nxd_snmp_agent_trapv3_oid_send)
   - *Inviare trap SNMP v2 (IPv4/IPv6) specificando l'OID*
- [nx_snmp_agent_v3_context_boots_set](#nx_snmp_agent_v3_context_boots_set)
   - *Impostare il numero di riavvii*
- [nx_snmp_object_compare](#nx_snmp_object_compare)
   - *Confrontare due oggetti*
- [nx_snmp_object_compare_extended](#nx_snmp_object_compare_extended)
   - *Confrontare due oggetti*
- [nx_snmp_object_copy](#nx_snmp_object_copy)
   - *Copiare un oggetto*
- [nx_snmp_object_copy_extended](#nx_snmp_object_copy_extended)
   - *Copiare un oggetto*
- [nx_snmp_object_counter_get](#nx_snmp_object_counter_get)
   - *Ottenere l'oggetto contatore*
- [nx_snmp_object_counter_set](#nx_snmp_object_counter_set)
   - *Impostare l'oggetto contatore*
- [nx_snmp_object_counter64_get](#nx_snmp_object_counter64_get)
   - *Ottenere l'oggetto contatore a 64 bit*
- [nx_snmp_object_counter64_set](#nx_snmp_object_counter64_set)
   - *Impostare un oggetto contatore a 64 bit*
- [nx_snmp_object_end_of_mib](#nx_snmp_object_end_of_mib)
   - *Impostare il valore di fine mib*
- [nx_snmp_object_gauge_get](#nx_snmp_object_gauge_get)
   - *Ottenere l'oggetto misuratore*
- [nx_snmp_object_gauge_set](#nx_snmp_object_gauge_set)
   - *Impostare l'oggetto misuratore*
- [nx_snmp_object_id_get](#nx_snmp_object_id_get)
   - *Ottenere l'ID oggetto*
- [nx_snmp_object_id_set](#nx_snmp_object_id_set)
   - *Impostare l'ID oggetto*
- [nx_snmp_object_integer_get](#nx_snmp_object_integer_get)
   - *Ottenere l'oggetto integer*
- [nx_snmp_object_integer_set](#nx_snmp_object_integer_set)
   - *Impostare l'oggetto integer*
- [nx_snmp_object_ip_address_get](#nx_snmp_object_ip_address_get)
   - *Ottenere l'oggetto indirizzo IP (solo IPv4)*
- [nx_snmp_object_ip_address_set](#nx_snmp_object_ip_address_set)
   - *Impostare l'oggetto indirizzo IP (solo IPv4)*
- [nx_snmp_object_ipv6_address_get](#nx_snmp_object_ipv6_address_get)
   - *Ottenere l'oggetto indirizzo IP (solo IPv6)*
- [nx_snmp_object_ipv6_address_set](#nx_snmp_object_ipv6_address_set)
   - *Impostare l'oggetto indirizzo IP (solo IPv6)*
- [nx_snmp_object_no_instance](#nx_snmp_object_no_instance)
   - *Impostare il valore no-instance*
- [nx_snmp_object_not_found](#nx_snmp_object_not_found)
   - *Impostare il valore non trovato*
- [nx_snmp_object_octet_string_get](#nx_snmp_object_octet_string_get)
   - *Ottenere l'oggetto stringa ottetto*
- [nx_snmp_object_octet_string_set](#nx_snmp_object_octet_string_set)
   - *Impostare l'oggetto stringa ottetto*
- [nx_snmp_object_string_get](#nx_snmp_object_string_get)
   - *Ottenere un oggetto stringa ASCII*
- [nx_snmp_object_string_set](#nx_snmp_object_string_set)
   - *Impostare un oggetto stringa ASCII*
- [nx_snmp_object_timetics_get](#nx_snmp_object_timetics_get)
   - *Ottenere l'oggetto timetics*
- [nx_snmp_object_timetics_set](#nx_snmp_object_timetics_set)
   - *Impostare l'oggetto timetics*

## <a name="nx_snmp_agent_auth_trap_key_use"></a>nx_snmp_agent_auth_trap_key_use
Specificare la chiave di autenticazione per i messaggi trap

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr, 
                                     NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a>Descrizione

Questo servizio specifica la chiave da usare per impostare i parametri di autenticazione nell'intestazione di sicurezza SNMPv3 nei messaggi trap. Se si specifica un NX_NULL per la chiave, l'autenticazione viene disabilitata.

> [!NOTE]
> La chiave deve essere creata in precedenza. Vedere nx_snmp_agent_md5_key_create o nx_snmp_agent_sha_key_create.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **chiave** Puntatore a una chiave MD5 o SHA creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Set di chiavi di autenticazione riuscito.
- **NX_NOT_ENABLED** (0x14) SNMP disabilitata 
- **NX_PTR_ERROR** (0x07) Puntatore dell'agente SNMP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Use previously created “my_key” for SNMPv3 trap message authentication.  */
status =  nx_snmp_agent_auth_trap_key_use(&my_agent, &my_key);


/* If status is NX_SUCCESS the SNMP Agent will use “my_key” for
   for authentication parameters in trap messages.  */
```

## <a name="nx_snmp_agent_authenticate_key_use"></a>nx_snmp_agent_authenticate_key_use
Specificare la chiave di autenticazione per i messaggi di risposta

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr, 
                                        NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a>Descrizione

Questo servizio specifica la chiave da usare per i parametri di autenticazione nel parametro di sicurezza SNMPv3 per tutte le richieste effettuate dopo l'impostazione. Se si specifica un NX_NULL per la chiave, l'autenticazione viene disabilitata.

> [!NOTE]
> La chiave deve essere creata in precedenza. Vedere nx_snmp_agent_md5_key_create o nx_snmp_agent_sha_key_create.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **chiave** Puntatore a una chiave MD5 o SHA creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) set di chiavi SNMP riuscito.
- **NX_NOT_ENABLED** (0x14) SNMP disabilitata
- **NX_PTR_ERROR** (0x07) Puntatore dell'agente SNMP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Use previously created “my_key” for SNMPv3 authentication.  */
status =  nx_snmp_agent_authenticate_key_use(&my_agent, &my_key);


/* If status is NX_SUCCESS the SNMP Agent will use “my_key” for
   for setting the authentication parameters of SNMPv3 requests.  */
```

## <a name="nx_snmp_agent_community_get"></a>nx_snmp_agent_community_get
Recuperare il nome della community

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_community_get(NX_SNMP_AGENT *agent_ptr, 
                                 UCHAR **community_string_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il nome della community dalla richiesta SNMP più recente ricevuta dall'agente SNMP.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **community_string_ptr** Puntatore a un puntatore di stringa per restituire la stringa della community dell'agente SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La community SNMP ha avuto esito positivo.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
UCHAR *string_ptr;

/* Pickup the community string pointer for my_agent.  */
status =  nx_snmp_agent_community_get(&my_agent, &string_ptr);


/* If status is NX_SUCCESS the pointer “string_ptr” points to the
   last community name supplied to the SNMP agent.  */
```

## <a name="nx_snmp_agent_request_get_type_test"></a>nx_snmp_agent_request_get_type_test
Indicare se l'ultima richiesta SNMP è di tipo GET o SET

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

### <a name="description"></a>Descrizione

Questo servizio indica se la richiesta più recente da Gestione SNMP è di tipo GET (GET, GETNEXT o GETBULK) o SET. È destinato all'uso con il callback del nome utente in cui l'applicazione SNMPv1 o SNMPv2 dovrà confrontare la stringa community ricevuta con la stringa pubblica dell'agente SNMP se la richiesta è di tipo GET o con la stringa privata dell'agente SNMP se la richiesta è di tipo SET.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **is_get_type** Puntatore allo stato del tipo di richiesta:  
NX_TRUE se il tipo GET  
NX_FALSE se il tipo SET

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Tipo restituito correttamente
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
UINT is_get_type;

/* Determine if the current SNMP request is a GET or SET type.  */
status =  nx_snmp_agent_request_get_type_test(&my_agent, &is_get_type);


/* If status is NX_SUCCESS, is_get_type will indicate the request type.  */
```

## <a name="nx_snmp_agent_context_engine_set"></a>nx_snmp_agent_context_engine_set
Impostare il motore di contesto (solo SNMP v3)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_context_engine_set(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *context_engine, 
                                      UINT context_engine_size);
```
### <a name="description"></a>Descrizione

Questo servizio imposta il motore di contesto dell'agente SNMP. È applicabile solo per l'elaborazione SNMPv3. Questa operazione deve essere chiamata prima di creare chiavi di sicurezza se l'applicazione usa l'autenticazione e la crittografia, poiché l'ID del motore di contesto viene usato nel processo di creazione della chiave. In caso contrario, NetX Duo SNMP fornisce un ID del motore di contesto predefinito nella parte superiore *di nxd_snmp.c:*

```c
UCHAR _nx_snmp_default_context_engine[NX_SNMP_MAX_CONTEXT_STRING] =  
                {0x80, 0x00, 0x03, 0x10, 0x01, 0xc0, 0xa8, 0x64, 0xaf};

```

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **context_engine** Puntatore alla stringa del motore di contesto.
- **context_engine_size** Dimensioni della stringa del motore di contesto. Si noti che il numero massimo di byte in un motore di contesto è definito da NX_SNMP_MAX_CONTEXT_STRING.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Set del motore di contesto SNMP riuscito.
- **NX_NOT_ENABLED** (0x14) SNMPv3 non è abilitato
- **NX_SNMP_ERROR** (0x100) Errore di dimensione del motore del contesto.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
UCHAR my_engine[] = {0x80, 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07};

/* Set the context engine for my_agent.  */
status =  nx_snmp_agent_context_engine_set(&my_agent, my_engine, 9);


/* If status is NX_SUCCESS the context engine has been set.  */
```
## <a name="nx_snmp_agent_context_name_set"></a>nx_snmp_agent_context_name_set
Impostare il nome del contesto (solo SNMP v3)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_context_name_set(NX_SNMP_AGENT *agent_ptr, 
                                    UCHAR *context_name, 
                                    UINT context_name_size);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il nome del contesto dell'agente SNMP. È applicabile solo per l'elaborazione SNMPv3. Se non viene chiamato, NetX Duo SNMP Agent lascia vuoto il nome del contesto.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **context_name** Puntatore alla stringa del nome del contesto.
- **context_name_size** Dimensione della stringa del nome del contesto. Si noti che il numero massimo di byte in un nome di contesto è definito da NX_SNMP_MAX_CONTEXT_STRING.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Set di nomi di contesto SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore di dimensione del nome del contesto.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the context name for my_agent.  */
status =  nx_snmp_agent_context_name_set(&my_agent, “my_context_name”, 15);


/* If status is NX_SUCCESS the context name has been set.  */
```

## <a name="nx_snmp_agent_create"></a>nx_snmp_agent_create
Creare l'agente SNMP

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_create(NX_SNMP_AGENT *agent_ptr, 
      CHAR *snmp_agent_name, NX_IP *ip_ptr, VOID *stack_ptr, 
      ULONG stack_size, NX_PACKET_POOL *pool_ptr,
      UINT (*snmp_agent_username_process)(struct NX_SNMP_AGENT_STRUCT 
                                    *agent_ptr, UCHAR *username),
      UINT (*snmp_agent_get_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data),
      UINT (*snmp_agent_getnext_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data),
      UINT (*snmp_agent_set_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data));
```
### <a name="description"></a>Descrizione

Questo servizio crea un agente SNMP nell'istanza IP specificata.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **snmp_agent_name** Puntatore alla stringa del nome dell'agente SNMP.
- **ip_ptr** Puntatore all'istanza IP.
- **stack_ptr** Puntatore al puntatore dello stack di thread dell'agente SNMP.
- **stack_size** Dimensioni dello stack in byte.
- **pool_ptr** Puntatore al pool di pacchetti predefinito per questo agente SNMP.
- **snmp_agent_username_process** Puntatore a funzione alla routine di gestione del nome utente dell'applicazione.
- **snmp_agent_get_process** Puntatore a funzione alla routine di gestione delle richieste GET dell'applicazione.
- **snmp_agent_getnext_process** Puntatore a funzione alla routine di gestione delle richieste GETNEXT dell'applicazione.
- **snmp_agent_set_process** Puntatore a funzione alla routine di gestione delle richieste SET dell'applicazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione dell'agente SNMP completata.
- **NX_SNMP_ERROR** (0x100) errore di creazione dell'agente SNMP.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
NX_SNMP_AGENT my_agent;

/* Create the SNMP Agent “my_agent.”  */
status =  nx_snmp_agent_create(&my_agent, "My SNMP Agent", &ip_0, stack_start_ptr,
                4096, &pool_0, my_username_processing, my_get_processing, 
                my_getnext_processing, my_set_processing);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been created.  */
```

## <a name="nx_snmp_agent_current_version_get"></a>nx_snmp_agent_current_version_get
Ottenere la versione del pacchetto SNMP

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_current_version_get(NX_SNMP_AGENT *agent_ptr, 
                                       UINT *version);
```

### <a name="description"></a>Descrizione

Questo servizio recupera la versione SNMP analizzata dal pacchetto SNMP più recente ricevuto.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **versione** Puntatore alla versione SNMP analizzata dal pacchetto SNMP ricevuto

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Riuscita della versione SNMP get
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT          snmp_version;
NX_SNMP_AGENT my_agent;

/* Get the version of the last received SNMP packet. */
status =  nx_snmp_agent_current_version_get (&my_agent, &snmp_version);


/* If status is NX_SUCCESS, snmp_version contains 
   the received packet SNMP version.  */
```

## <a name="nx_snmp_agent_private_string_test"></a>nx_snmp_agent_private_string_test
Verificare che la stringa privata corrisponda alla stringa privata dell'agente

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr, 
                                       UCHAR *community_string,          
                                       UINT *is_private);
```

### <a name="description"></a>Descrizione

Questo servizio confronta la stringa della community di input con terminazione Null con la stringa privata dell'agente SNMP e indica se corrispondono.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **community_string** Puntatore a stringa da confrontare
- **is_private** Puntatore al risultato del confronto  
NX_TRUE - corrispondenze di stringhe  
NX_FALSE: la stringa non corrisponde

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Confronto riuscito
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT        is_private;
UCHAR       *community_string_ptr;
NX_SNMP_AGENT   my_agent;

/* Determine if the community string matches the agent private string */
status =  nx_snmp_agent_private_string_test(&my_agent, community_string_ptr,  
                                            &is_private);


/* If status is NX_SUCCESS, is_private will indicate if there is a match. 
   If is_private is NX_TRUE, they match.  */
```

## <a name="nx_snmp_agent_public_string_test"></a>nx_snmp_agent_public_string_test
Verificare che la stringa pubblica ricevuta corrisponda alla stringa pubblica dell'agente

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *community_string,          
                                      UINT *is_public);
```
### <a name="description"></a>Descrizione

Questo servizio confronta una stringa della community di input con terminazione Null con la stringa pubblica dell'agente SNMP e indica se corrispondono.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **community_string** Puntatore a stringa da confrontare
- **is_public** Puntatore al risultato del confronto  
NX_TRUE - corrispondenze di stringhe  
NX_FALSE: la stringa non corrisponde

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Confronto riuscito
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT        is_public;
UCHAR       *community_string_ptr;
NX_SNMP_AGENT   my_agent;


/* Determine if the community string matches the agent public string */
status =  nx_snmp_agent_public_string_test(&my_agent, community_string_ptr,  
                                           &is_public);


/* If status is NX_SUCCESS, is_public will indicate if there is a match. 
   If is_public is true they match.  */
```

## <a name="nx_snmp_agent_version_set"></a>nx_snmp_agent_version_set
Impostare lo stato dell'agente SNMP per ogni versione SNMP

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_version_set(NX_SNMP_AGENT *agent_ptr, 
                               UINT enabled_v1, UINT enable_v2, 
                               UINT enable_v3);
```

### <a name="description"></a>Descrizione

Questo servizio imposta lo stato (abilitato/disabilitato) per ognuna delle versioni SNMP, V1, V2 e V3 nell'agente SNMP. Si noti che le opzioni configurabili dall'utente, NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 e NX_SNMP_DISABLE_V3, eseguiranno l'override di queste impostazioni in fase di esecuzione. Per impostazione predefinita, l'agente SNMP è abilitato per tutte e tre le versioni.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **enabled_v1** Imposta lo stato abilitato per SNMP V1 su On/Off.
- **enabled_v2** Imposta lo stato abilitato per SNMP V2 su On/Off.
- **enabled_v3** Imposta lo stato abilitato per SNMP V3 su On/Off.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Set di versioni SNMP riuscito
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT          v1_on = NX_TRUE;
UINT          v2_on = NX_TRUE;
UINT          v3_on = NX_FALSE;

NX_SNMP_AGENT my_agent;

/* Enable/Disable each SNMP protocol (version) for the SNMP Agent) */
status =  nx_snmp_agent_version_set(&my_agent, v1_on, v2_on, v3_on);


/* If status is NX_SUCCESS, my_agent is enabled only for V1 and V2 assuming 
   NX_SNMP_DISABLE_V1 and NX_SNMP_DISABLE_V2 are not defined. */
```

## <a name="nx_snmp_agent_private_string_set"></a>nx_snmp_agent_private_string_set
Impostare la stringa privata dell'agente SNMP

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_private_string_set(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *community_string);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la stringa della community privata dell'agente SNMP con la stringa con terminazione Null di input. Il valore predefinito è NULL (nessuna stringa privata impostata), in modo che qualsiasi pacchetto SNMP ricevuto con una stringa community "privata" non verrà accettato dall'agente SNMP per l'accesso in lettura/scrittura. La stringa di input deve essere minore o uguale alla dimensione configurabile dall'utente NX_SNMP_MAX_USER_NAME-1 (per consentire spazio per la terminazione Null).

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **community_string** Puntatore alla stringa privata da assegnare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente la stringa privata
- **NX_SNMP_ERROR_TOOBIG** (0x01) Dimensioni della stringa troppo grandi 
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_AGENT my_agent;

/* Set the SNMP agent’s private community string */
status =  nx_snmp_agent_private_string_set(&my_agent, “private”));


/* If status is NX_SUCCESS, the SNMP agent private string is set.  */
```

## <a name="nx_snmp_agent_public_string_set"></a>nx_snmp_agent_public_string_set
Impostare la stringa pubblica dell'agente SNMP

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_public_string_set(NX_SNMP_AGENT *agent_ptr, 
                                     UCHAR *community_string);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la stringa della community pubblica dell'agente SNMP con la stringa di terminazione Null di input. La stringa della community deve essere minore o uguale alla dimensione configurabile dall'utente NX_SNMP_MAX_USER_NAME-1 (per consentire spazio per la terminazione Null).

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **community_string** Puntatore alla stringa pubblica da assegnare

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente la stringa pubblica
- **NX_SNMP_ERROR_TOOBIG** (0x01) Dimensioni della stringa troppo grandi
- **NX_PTR_ERROR** (0x07) Input puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_AGENT my_agent;

/* Set the SNMP agent’s public string. */
nx_snmp_agent_public_string_set(&my_agent, “my_public”));


/* If status is NX_SUCCESS, the SNMP agent public string is set.  */
```

## <a name="nx_snmp_agent_delete"></a>nx_snmp_agent_delete
Eliminare l'agente SNMP

### <a name="prototype"></a>Prototipo

```C
UINT nx_snmp_agent_delete(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina un agente SNMP creato in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione dell'agente SNMP completata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Delete the SNMP Agent “my_agent.”  */
status =  nx_snmp_agent_delete(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been deleted.  */
```

## <a name="nx_snmp_agent_set_interface"></a>nx_snmp_agent_set_interface
Impostare l'interfaccia di rete dell'agente SNMP

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_set_interface(NX_SNMP_AGENT *agent_ptr,  
                                 UINT if_index);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'interfaccia di rete SNMP per l'agente SNMP come specificato dall'indice dell'interfaccia di input. Ciò è utile solo per le applicazioni host SNMP con NetX Duo 5.6 o versione successiva che supportano più interfacce di rete. Il valore predefinito, se non specificato dall'host, è zero, per l'interfaccia primaria.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **If_index** Indice che specifica l'interfaccia SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Set di interfacce SNMP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the SNMP Agent “my_agent” to the secondary interface.  */
if_index = 1;
status =  nx_snmp_agent_set_interface(&my_agent, if_index);


/* If status is NX_SUCCESS the SNMP agent interface is set.  */
```

## <a name="nx_snmp_agent_md5_key_create"></a>nx_snmp_agent_md5_key_create
Creare una chiave md5 (solo SNMP v3)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr, 
                                  UCHAR *password, 
                                  NX_SNMP_SECURITY_KEY 
                                       *destination_key);
```
### <a name="description"></a>Descrizione

Questo servizio crea una chiave MD5 che può essere usata per l'autenticazione e la crittografia.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione *a nx_snmp_agent_md5_key_create_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **password** Puntatore alla stringa della password.
- **destination_key** Puntatore alla struttura dei dati della chiave SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione chiave riuscita.
- **NX_NOT_ENABLED** (0x14) Sicurezza non abilitata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the MD5 key for “my_agent.”   */
status =  nx_snmp_agent_md5_key_create(&my_agent, “authpw”, &my_key);


/* If status is NX_SUCCESS an MD5 key has been created.  */
```

## <a name="nx_snmp_agent_md5_key_create_extended"></a>nx_snmp_agent_md5_key_create_extended
Creare la chiave md5 (solo SNMP v3)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_md5_key_create_extended(NX_SNMP_AGENT *agent_ptr, 
                                           UCHAR *password, 
                                           UINT password_length,
                                           NX_SNMP_SECURITY_KEY 
                                           *destination_key);
```
### <a name="description"></a>Descrizione

Questo servizio crea una chiave MD5 che può essere utilizzata per l'autenticazione e la crittografia.

Questo servizio sostituisce *nx_snmp_agent_md5_key_create().* Questa versione richiede al chiamante di specificare la lunghezza della password.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **password** Puntatore alla stringa della password.
- **password_length** Lunghezza della stringa della password.
- **destination_key** Puntatore alla struttura dei dati della chiave SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione chiave riuscita.
- **NX_NOT_ENABLED** (0x14) Sicurezza non abilitata.
- **NX_SNMP_FAILED** (0x102) SNMP non riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the MD5 key for “my_agent.”   */
status =  nx_snmp_agent_md5_key_create_extended(&my_agent, “authpw”, 6, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_priv_trap_key_use"></a>nx_snmp_agent_priv_trap_key_use
Specificare la chiave di crittografia per i messaggi trap

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr, 
                                     NX_SNMP_SECURITY_KEY *key);
```

### <a name="description"></a>Descrizione

Questo servizio specifica che una chiave di privacy creata in precedenza deve essere usata per la crittografia e la decrittografia dei messaggi trap SNMPv3.

> [!NOTE]
> *Una chiave di autenticazione deve essere creata in precedenza. La privacy (crittografia) SNMP v3 richiede l'autenticazione. Vedere nx_snmp_agent_auth_trap_key_use per informazioni dettagliate.*

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **chiave** Puntatore alla chiave creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'impostazione della chiave di privacy è riuscita.
- **NX_NOT_ENABLED** (0x14) Sicurezza non abilitata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Use the “my_privacy_key” for the SNMP Agent “my_agent” trap messages.   */
status =  nx_snmp_agent_priv_trap_key_use(&my_agent, &my_privacy_key);


/* If status is NX_SUCCESS the privacy key is registered with the SNMP agent.  */
```

## <a name="nx_snmp_agent_privacy_key_use"></a>nx_snmp_agent_privacy_key_use
Specificare la chiave di crittografia per i messaggi di risposta

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr, 
                                   NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a>Descrizione

Questo servizio specifica che la chiave creata in precedenza deve essere usata per la crittografia e la decrittografia dei messaggi di risposta SNMPv3.

> [!NOTE]
> *Una chiave di autenticazione deve essere stata specificata in precedenza. La crittografia SNMP v3 richiede anche la creazione di una chiave di autenticazione. Vedere nx_snmp_agent_authentiation_key_use per informazioni dettagliate.*

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **chiave** Puntatore alla chiave creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'impostazione della chiave di privacy è riuscita.
- **NX_NOT_ENABLED** (0x14) Sicurezza non abilitata.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Use the “my_privacy_key” for the SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_privacy_key_use(&my_agent, &my_privacy_key);


/* If status is NX_SUCCESS the privacy key is registered with the SNMP agent.  */
```

## <a name="nx_snmp_agent_sha_key_create"></a>nx_snmp_agent_sha_key_create
Creare una chiave SHA (solo SNMP v3)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr, 
                                  UCHAR *password, 
                                  NX_SNMP_SECURITY_KEY  
                                  *destination_key);
```
### <a name="description"></a>Descrizione

Questo servizio crea una chiave SHA che può essere usata per l'autenticazione e la crittografia.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la *migrazione nx_snmp_agent_sha_key_create_extended()*.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **password** Puntatore alla stringa della password.
- **destination_key** Puntatore alla struttura dei dati della chiave SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione chiave riuscita.
- **NX_SNMP_ERROR** (0x100) Errore di creazione della chiave.
- **NX_PTR_ERROR** (0x07) Agente SNMP o puntatore a chiave non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the SHA key for “my_agent.”   */
status =  nx_snmp_agent_sha_key_create(&my_agent, “authpw”, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_sha_key_create_extended"></a>nx_snmp_agent_sha_key_create_extended
Creare una chiave SHA (solo SNMP v3)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_sha_key_create_extended(NX_SNMP_AGENT *agent_ptr, 
                                           UCHAR *password, 
                                           UINT password_length,
                                           NX_SNMP_SECURITY_KEY  
                                           *destination_key);
```
### <a name="description"></a>Descrizione

Questo servizio crea una chiave SHA che può essere usata per l'autenticazione e la crittografia.

Questo servizio sostituisce *nx_snmp_agent_sha_key_create().* Questa versione richiede al chiamante di specificare la lunghezza della password.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **password** Puntatore alla stringa della password.
- **password_length** Lunghezza della stringa della password.
- **destination_key** Puntatore alla struttura dei dati della chiave SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione chiave riuscita.
- **NX_SNMP_ERROR** (0x100) Errore di creazione della chiave.
- **NX_SNMP_FAILED** (0x102) creazione della chiave non riuscita.
- **NX_PTR_ERROR** (0x07) Agente SNMP o puntatore a chiave non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the SHA key for “my_agent.”   */
status =  nx_snmp_agent_sha_key_create_extended(&my_agent, “authpw”, 6, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_start"></a>nx_snmp_agent_start
Avviare l'agente SNMP 

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_start(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio associa il socket UDP alla porta SNMP 161 e avvia l'attività thread dell'agente SNMP.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Avvio riuscito dell'agente SNMP.
- **NX_SNMP_ERROR** (0x100) dell'agente SNMP.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Start the previously created SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_start(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been started.  */
```
## <a name="nx_snmp_agent_stop"></a>nx_snmp_agent_stop
Arrestare l'agente SNMP 

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_stop(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio arresta l'attività del thread dell'agente SNMP e disassocia il socket UDP alla porta SNMP.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Arresto riuscito dell'agente SNMP.
- **NX_PTR_ERROR** (0x07) Puntatore dell'agente SNMP non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the previously created and started SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_stop(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been stopped.  */
```
## <a name="nx_snmp_agent_trap_send"></a>nx_snmp_agent_trap_send
Invia trap SNMPv1 *(solo IPv4)*

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_trap_send(NX_SNMP_AGENT *agent_ptr, 
                             ULONG ip_address, UCHAR *enterprise, 
                             UINT trap_type, UINT trap_code, 
                             ULONG elapsed_time, 
                             NX_SNMP_TRAP_OBJECT *object_list_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia una trap SNMP a Gestione SNMP all'indirizzo IPv4 specificato. Il metodo preferito per l'invio di una trap SNMP in NetX Duo è l'uso del *nxd_snmp_agent_trap_send* servizio. *nx_snmp_agent_trap_send* è incluso in NetX Duo per supportare le applicazioni NetX SNMP Agent esistenti.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IPv4 di Gestione SNMP.
- **enterprise** Enterprise object ID string (sysObectID).
- **trap_type** Tipo di trap richiesto, come indicato di seguito:  
   - NX_SNMP_TRAP_COLDSTART (0)  
   - NX_SNMP_TRAP_WARMSTART (1)  
   - NX_SNMP_TRAP_LINKDOWN (2)  
   - NX_SNMP_TRAP_LINKUP (3)  
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)  
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)  

- **trap_code** Codice trap specifico.
- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_NOT_ENABLED** (0x14) SNMPv1 non abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

ULONG dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build list of objects to supply in the trap.  */
trap_list[0].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.2.2.1.1.0";
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_INTEGER;
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_msw =   counter;
trap_list[1].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.1.3.0";
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_TIME_TICS;
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_msw =   tx_time_get();
trap_list[2].nx_snmp_object_string_ptr =  NX_NULL; /* Terminate list!  */

/* Send trap to SNMP manager at 193.2.2.61.  */
status =  nx_snmp_agent_trap_send(&my_agent,dest_ip_address,
                                   "1.3.6.7.7.7", NX_SNMP_TRAP_LINKUP, counter++, 
                                  tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nxd_snmp_agent_trap_send"></a>nxd_snmp_agent_trap_send
Inviare trap SNMPv1 *(IPv4 e IPv6)*

### <a name="prototype"></a>Prototipo

```c
UINT nxd_snmp_agent_trap_send(NX_SNMP_AGENT *agent_ptr, 
            ULONG ip_address, UCHAR *enterprise, UINT trap_type, 
            UINT trap_code, ULONG elapsed_time, 
            NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invia una trap SNMP a Gestione SNMP all'indirizzo IP specificato. Il metodo equivalente per l'invio di una trap SNMP in NetX è *nxd_snmp_agent_trap_send* servizio.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IPv4 o IPv6 di Gestione SNMP.
- **enterprise** Enterprise object ID string (sysObectID).
- **trap_type** Tipo di trap richiesto, come indicato di seguito:  
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)

- **trap_code** Codice trap specifico.
- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_NOT_ENABLED** (0x14) SNMPv1 non abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build list of objects to supply in the trap.  */
trap_list[0].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.2.2.1.1.0";
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_INTEGER;
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_msw =   counter;
trap_list[1].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.1.3.0";
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_TIME_TICS;
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_msw =   tx_time_get();
trap_list[2].nx_snmp_object_string_ptr =  NX_NULL; /* Terminate list!  */

/* Send trap to SNMP manager at 193.2.2.61.  */
status =  nxd_snmp_agent_trap_send(&my_agent,&dest_ip_address,
                 "1.3.6.7.7.7", NX_SNMP_TRAP_LINKUP, counter++, tx_time_get(), 
               trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv2_send"></a>nx_snmp_agent_trapv2_send
Invia trap SNMPv2 (solo IPv4)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_trapv2_send(NX_SNMP_AGENT *agent_ptr, 
            NXD_ADDRESS *ip_address, UCHAR *community, UINT trap_type, 
            ULONG elapsed_time, NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invia una trap SNMPv2 a Gestione SNMP all'indirizzo IPv4 specificato. Il metodo preferito per l'invio di una trap SNMP in NetX Duo è l'uso *del nxd_snmp_agent_trapv2_send* servizio. *nx_snmp_agent_trapv2_send* è incluso in NetX Duo per supportare le applicazioni NetX SNMP Agent esistenti.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IPv4 di Gestione SNMP.
- **nome** Community community (nome utente).
- **trap_type**  
   Tipo di trap richiesto. Gli eventi standard sono:  
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)

   Per i dati proprietari:  
   - NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (definito in *nxd_snmp.h*)
   
- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_NOT_ENABLED** (0x14) SNMPv2 non abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
ULONG  dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv2_send(&my_agent,dest_ip_address, "public",
               NX_SNMP_TRAP_COLDSTART, tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv2_oid_send"></a>nx_snmp_agent_trapv2_oid_send
Invia trap SNMPv2 specificando direttamente L'OID 

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_trapv2_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                   ULONG ip_address, UCHAR *community,        
                                   UCHAR *oid, ULONG elapsed_time,   
                                   NX_SNMP_TRAP_OBJECT 
                                            *object_list_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invia una trap SNMPv2 a Gestione SNMP all'indirizzo IP specificato (solo IPv4) e consente al chiamante di specificare direttamente l'OID. Il metodo preferito per inviare una trap SNMP con L'OID specificato in NetX Duo è usare il *nxd_snmp_agent_trapv2_oid_send* servizio. *nx_snmp_agent_trapv2_oid_ send è* incluso in NetX Duo per supportare le applicazioni NetX SNMP Agent esistenti.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IP di Gestione SNMP.
- **nome** Community community (nome utente).
- **oid** Puntatore al buffer contenente L'OID.
- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_PTR_ERROR** (0x16) Agente SNMP o puntatore al parametro non valido.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP di destinazione non valido.
- **NX_OPTION_ERROR** (0x0a) Parametro non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv2_oid_send(&my_agent, IP_ADDRESS(193,2,2,61), 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv2_send"></a>nxd_snmp_agent_trapv2_send
Inviare trap SNMPv2 (IPv4 e IPv6)

### <a name="prototype"></a>Prototipo

```c
UINT nxd_snmp_agent_trapv2_send(NX_SNMP_AGENT *agent_ptr, 
                                NXD_ADDRESS *ip_address, 
                                UCHAR *community, UINT trap_type, 
                                ULONG elapsed_time, 
                                NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invia un trap SNMP V2 a Gestione SNMP all'indirizzo IP specificato.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IP (IPv4 o IPv6) di Gestione SNMP.
- **nome** Community community (nome utente).
- **trap_type**  
   Tipo di trap richiesto. Gli eventi standard sono:  
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)

   Per i dati proprietari:

   - NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (definito in *nxd_snmp.h*)

- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_NOT_ENABLED** (0x14) SNMPv2 non abilitato.
- **NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) Versione IP non supportata
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send a standard event trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv2_send(&my_agent,&dest_ip_address, "public",
                                    NX_SNMP_TRAP_COLDSTART, tx_time_get(),  
                                    trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv2_oid_send"></a>nxd_snmp_agent_trapv2_oid_send
Invia trap SNMPv2 specificando direttamente L'OID 

### <a name="prototype"></a>Prototipo

```c
UINT nxd_snmp_agent_trapv2_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                    NXD_ADDRESS *ip_address, 
                                    UCHAR *community,        
                                    UCHAR *oid, ULONG elapsed_time,   
                                    NX_SNMP_TRAP_OBJECT 
                                    *object_list_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invia una trap SNMP v2 a Gestione SNMP all'indirizzo IP specificato (IPv4/IPv6) e consente al chiamante di specificare direttamente l'OID.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IP di Gestione SNMP (IPv4/IPv6).
- **nome** Community community (nome utente).
- **oid** Puntatore al buffer contenente L'OID.
- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_PTR_ERROR** (0x16) Agente SNMP o puntatore al parametro non valido.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP di destinazione non valido.
- **NX_OPTION_ERROR** (0x0a) Parametro non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS         address;


/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

address.nxd_ip_version = NX_IP_VERSION_V4;
address.nxd_ip_address.v4 = IP_ADDRESS(193,2,2,61)

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv2_oid_send(&my_agent, &address, 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nx_snmp_agent_trapv3_send"></a>nx_snmp_agent_trapv3_send
Invia trap SNMPv3 (solo IPv4)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_trapv3_send(NX_SNMP_AGENT *agent_ptr, 
            ULONG ip_address, UCHAR *username, UINT trap_type, 
            ULONG elapsed_time, NX_SNMP_TRAP_OBJECT *object_list_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia una trap SNMPv3 a Gestione SNMP all'indirizzo IPv4 specificato. Il metodo preferito per l'invio di una trap SNMP in NetX Duo è l'uso del *nxd_snmp_agent_trapv3_send* servizio. *nx_snmp_agent_trapv3_send* è incluso in NetX Duo per supportare le applicazioni NetX SNMP Agent esistenti.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IPv4 di Gestione SNMP.
- **username** Community name (username).
- **trap_type**  
   Tipo di trap richiesto. Gli eventi standard sono:  
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)

   Per i dati proprietari:
   - NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (definito in *nxd_snmp.h*)

- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_NOT_ENABLED** (0x14) SNMPv3 non abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
ULONG dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv3_send(&my_agent, dest_ip_address, "public",
               NX_SNMP_TRAP_COLDSTART, tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv3_oid_send"></a>nx_snmp_agent_trapv3_oid_send
Inviare il trap SNMPv3 specificando direttamente L'OID 

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_trapv3_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                   ULONG ip_address, UCHAR *username,        
                                   UCHAR *oid, ULONG elapsed_time,   
                                   NX_SNMP_TRAP_OBJECT 
                                   *object_list_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invia un trap SNMPv3 a Gestione SNMP all'indirizzo IP specificato (solo IPv4) e consente al chiamante di specificare direttamente l'OID. Il metodo preferito per l'invio di una trap SNMP con L'OID specificato in NetX Duo è l'uso del *nxd_snmp_agent_trapv3_oid_send* servizio. *nx_snmp_agent_trapv3_oid_ send è* incluso in NetX Duo per supportare le applicazioni NetX SNMP Agent esistenti.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IP di Gestione SNMP.
- **username** Community name (username).
- **oid** Puntatore al buffer contenente L'OID.
- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_PTR_ERROR** (0x16) Agente SNMP o puntatore al parametro non valido.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP di destinazione non valido.
- **NX_OPTION_ERROR** (0x0a) Parametro non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv3_oid_send(&my_agent, IP_ADDRESS(193,2,2,61), 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nxd_snmp_agent_trapv3_send"></a>nxd_snmp_agent_trapv3_send
Inviare trap SNMPv3 (IPv4 e IPv6)

### <a name="prototype"></a>Prototipo

```c
UINT nxd_snmp_agent_trapv3_send(NX_SNMP_AGENT *agent_ptr, 
                                NXD_ADDRESS *ip_address, 
                                UCHAR *username, UINT trap_type, 
                                ULONG elapsed_time, 
                                NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invia una trap SNMP a Gestione SNMP all'indirizzo IP specificato. Questa trap è fondamentalmente uguale alla trap SNMP v2, ad eccezione del fatto che il formato del messaggio trap è contenuto nella PDU SNMP v3.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Indirizzo IP (IPv4 o IPv6) di Gestione SNMP.
- **username** Community name (username).
- **trap_type**  
   Tipo di trap richiesto. Gli eventi standard sono:
   - NX_SNMP_TRAP_COLDSTART (0)
   - NX_SNMP_TRAP_WARMSTART (1)
   - NX_SNMP_TRAP_LINKDOWN (2)
   - NX_SNMP_TRAP_LINKUP (3)
   - NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)
   - NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)  
   Per i dati proprietari:
   - NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (definito in *nxd_snmp.h*)

- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_NOT_ENABLED** (0x14) SNMPv3 non abilitato.
- **NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) Versione IP non supportata
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv3_send(&my_agent, &dest_ip_address, "public",
                                    NX_SNMP_TRAP_COLDSTART, tx_time_get(),  
                                    trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv3_oid_send"></a>nxd_snmp_agent_trapv3_oid_send
Inviare il trap SNMPv3 specificando direttamente L'OID 

### <a name="prototype"></a>Prototipo

```c
UINT nxd_snmp_agent_trapv3_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                    NXD_ADDRESS *ip_address, 
                                    UCHAR *username,        
                                    UCHAR *oid, ULONG elapsed_time,   
                                    NX_SNMP_TRAP_OBJECT 
                                            *object_list_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invia una trap SNMPv3 a Gestione SNMP all'indirizzo IP specificato (IPv4/IPv6) e consente al chiamante di specificare direttamente l'OID.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.
- **ip_address** Puntatore all'indirizzo IP di Gestione SNMP.
- **nome utente** Nome utente (nome community).
- **oid** Puntatore al buffer contenente L'OID.
- **elapsed_time** Il sistema di tempo è stato operativo (sysUpTime).
- **object_list_ptr** Matrice di oggetti e dei relativi valori associati da includere nel trap SNMP. L'elenco NX_NULL terminato.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio trap SNMP riuscito.
- **NX_SNMP_ERROR** (0x100) Errore durante l'invio della trap SNMP.
- **NX_PTR_ERROR** (0x16) Agente SNMP o puntatore al parametro non valido.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP di destinazione non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
NXD_ADDRESS         ip_address;
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

ip_address.nxd_ip_version = NX_IP_VERSION_V4;
ip_address.nxd_ip_address.v4 = IP_ADDRESS(193,2,2,61);

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv3_oid_send(&my_agent, &ip_address, 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nx_snmp_agent_v3_context_boots_set"></a>nx_snmp_agent_v3_context_boots_set
Impostare il numero di riavvii (se SNMPv3 è abilitato)

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_agent_v3_context_boots_set(NX_SNMP_AGENT *agent_ptr, 
                                        UINT boots);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il numero di riavvii registrati dall'agente SNMP. Questo servizio è disponibile solo se SNMPv3 è abilitato per l'agente SNMP perché il conteggio di avvio viene usato solo nel protocollo SNMPv3.

### <a name="input-parameters"></a>Parametri di input

- **agent_ptr** Puntatore al blocco di controllo dell'agente SNMP
- **boots** Valore su cui impostare il conteggio di avvio dell'agente SNMP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Successfully set boot count
- **NX_SNMP_ERROR** (0x100) Numero di avvio dell'impostazione degli errori
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
UINT my_boots = 4;

if (my_agent.nx_snmp_agent_v3_enabled == NX_TRUE)
{
   status = nx_snmp_agent_v3_context_boots_set(&my_agent, my_boots);
}


/* If status is NX_SUCCESS the SNMP boot count is set.  */
```

## <a name="nx_snmp_object_compare"></a>nx_snmp_object_compare
Confrontare due oggetti 

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_object_compare(UCHAR *object, UCHAR *reference_object);
```

### <a name="description"></a>Descrizione

Questo servizio confronta l'ID oggetto fornito con l'ID oggetto di riferimento. Entrambi gli ID oggetto sono nella notazione SMI ASCII, ad esempio entrambi gli oggetti devono iniziare con la stringa ASCII "1.3.6".

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la *migrazione nx_snmp_object_compare_extended().*

### <a name="input-parameters"></a>Parametri di input

- **oggetto** Puntatore all'ID oggetto.
- **reference_object** Puntatore all'ID dell'oggetto di riferimento.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto corrisponde all'oggetto di riferimento.
- **NX_SNMP_NEXT_ENTRY** (0x101) L'oggetto è minore dell'oggetto di riferimento.
- **NX_SNMP_ERROR** (0x100) L'oggetto è maggiore dell'oggetto di riferimento.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Compare “requested_object” with the sysDescr object ID of 
   "1.3.6.1.2.1.1.1.0".  */
Status =  nx_snmp_object_compare(requested_object, "1.3.6.1.2.1.1.1.0");

/* If status is NX_SUCCESS, requested_object is the sysDescr object. 
   Otherwise, if status is NX_SNMP_NEXT_ENTRY, the requested object is
   less than the sysDescr. If status is NX_SNMP_ERROR, the object is 
   greater than sysDescr. */
```

## <a name="nx_snmp_object_compare_extended"></a>nx_snmp_object_compare_extended
Confrontare due oggetti 

### <a name="prototype"></a>Prototipo

```c
UINT nx_snmp_object_compare_extended(UCHAR *request_object, 
                                     UINT requested_object_length,
                                     UCHAR *reference_object
                                     UINT reference_object_length);
```
### <a name="description"></a>Descrizione

Questo servizio confronta l'ID oggetto fornito con l'ID oggetto di riferimento. Entrambi gli ID oggetto sono nella notazione SMI ASCII, ad esempio entrambi gli oggetti devono iniziare con la stringa ASCII "1.3.6".

Questo servizio sostituisce *nx_snmp_object_compare().* Questa versione richiede che i chiamanti fornino informazioni sulla lunghezza.

### <a name="input-parameters"></a>Parametri di input

- **request_object** Puntatore all'ID oggetto della richiesta.
- **request_object_length** Lunghezza dell'ID oggetto della richiesta.
- **reference_object** Puntatore all'ID dell'oggetto di riferimento.
- **reference_object_length** Lunghezza dell'ID oggetto di riferimento.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto corrisponde all'oggetto di riferimento.
- **NX_SNMP_NEXT_ENTRY** (0x101) L'oggetto è minore dell'oggetto di riferimento.
- **NX_SNMP_ERROR** (0x100) L'oggetto è maggiore dell'oggetto di riferimento.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Compare “requested_object” with the sysDescr object ID of 
   "1.3.6.1.2.1.1.1.0".  */
Status =  nx_snmp_object_compare_extended(requested_object, 17,
                                          "1.3.6.1.2.1.1.1.0", 17);

/* If status is NX_SUCCESS, requested_object is the sysDescr object. 
   Otherwise, if status is NX_SNMP_NEXT_ENTRY, the requested object is
   less than the sysDescr. If status is NX_SNMP_ERROR, the object is 
   greater than sysDescr. */
```

## <a name="nx_snmp_object_copy"></a>nx_snmp_object_copy
Copiare un oggetto 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_copy(UCHAR *source_object_name, 
                          UCHAR *destination_object_name);
```
### <a name="description"></a>Descrizione

Questo servizio copia l'oggetto di origine in notazione SIM ASCII nell'oggetto di destinazione.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione *a nx_snmp_object_copy_extended().*

### <a name="input-parameters"></a>Parametri di input

- **source_object_name** Puntatore all'ID oggetto di origine.
- **destination_object_name** Puntatore all'ID dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **size** Numero di byte copiati nel nome di destinazione. Se si verifica un errore, viene restituito zero.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Copy “my_object” to “my_new_object”.  */
size =  nx_snmp_object_copy(my_object, my_new_object);

/* Size contains the number of bytes copied. */
```

## <a name="nx_snmp_object_copy_extended"></a>nx_snmp_object_copy_extended
Copiare un oggetto 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_copy_extended(UCHAR *source_object_name, 
                             UINT source_object_name_length,
                             UCHAR *destination_object_name_buffer,
                             UINT destination_object_name_buffer_size);
```

### <a name="description"></a>Descrizione

Questo servizio copia l'oggetto di origine in notazione SIM ASCII nell'oggetto di destinazione.

Questo servizio sostituisce *nx_snmp_object_copy().* Questa versione richiede che i chiamanti fornino informazioni sulla lunghezza.

### <a name="input-parameters"></a>Parametri di input

- **source_object_name** Puntatore all'ID oggetto di origine.
- **source_object_name_length** Lunghezza dell'ID oggetto di origine.
- **destination_object_name_buffer** Puntatore al buffer dell'oggetto di destinazione.
- **destination_object_name_buffer_size** Dimensione del buffer dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **size** Numero di byte copiati nel nome di destinazione. Se si verifica un errore, viene restituito zero.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
UCHAR   my_object = "1.3.6.1.2.1.1.1.0";
UCHAR   my_new_object[32];


/* Copy “my_object” to “my_new_object”.  */
size =  nx_snmp_object_copy(my_object, 17, my_new_object, sizeof(my_new_object));

/* Size contains the number of bytes copied. */
```

## <a name="nx_snmp_object_counter_get"></a>nx_snmp_object_counter_get
Ottenere l'oggetto contatore 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_counter_get(VOID *source_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```
### <a name="description"></a>Descrizione

Questo servizio recupera l'oggetto contatore in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine del contatore.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto contatore è stato recuperato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the ifInOctets (1.3.6.1.2.1.2.2.1.10.0) MIB-2 object.  */
status =  nx_snmp_object_counter_get(&ifInOctets, my_object);

/* If status is NX_SUCCESS, the ifInOctets object has been 
   retrieved and is ready to be returned. */
```

## <a name="nx_snmp_object_counter_set"></a>nx_snmp_object_counter_set
Impostare l'oggetto contatore 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_counter_set(VOID *destination_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il contatore in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con il valore del contatore nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore alla destinazione del contatore.
- **object_data** Puntatore alla struttura dell'oggetto di origine del contatore.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto contatore è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the ifInOctets (1.3.6.1.2.1.2.2.1.10.0) MIB-2 object with
   the counter object value contained in my_object.  */
status =  nx_snmp_object_counter_set(&ifInOctets, my_object);

/* If status is NX_SUCCESS, the ifInOctets object has been 
   set. */
```

## <a name="nx_snmp_object_counter64_get"></a>nx_snmp_object_counter64_get
Ottenere l'oggetto contatore a 64 bit 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_counter64_get(VOID *source_ptr, 
                                   NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'oggetto contatore a 64 bit in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine del contatore.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto contatore è stato recuperato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of my_64_bit_counter and place it into my_object
   for return.  */
status =  nx_snmp_object_counter64_get(&my_64_bit_counter, my_object);

/* If status is NX_SUCCESS, the my_64_bit_counter object has been 
   retrieved and is ready to be returned. */
```

## <a name="nx_snmp_object_counter64_set"></a>nx_snmp_object_counter64_set
Impostare l'oggetto contatore a 64 bit 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_counter64_set(VOID *destination_ptr, 
                                   NX_SNMP_OBJECT_DATA *object_data);
```
### <a name="description"></a>Descrizione

Questo servizio imposta il contatore a 64 bit in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con il valore del contatore nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore alla destinazione del contatore.
- **object_data** Puntatore alla struttura dell'oggetto di origine del contatore.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto contatore è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the value of my_64_bit_counter with the value in my_object.  */
status =  nx_snmp_object_counter64_set(&my_64_bit_counter, my_object);

/* If status is NX_SUCCESS, the my_64_bit_counter object has been 
   set. */
```

## <a name="nx_snmp_object_end_of_mib"></a>nx_snmp_object_end_of_mib
Impostare il valore di fine mib 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_end_of_mib(VOID *not_used_ptr, 
                              NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio crea un oggetto che segnala la fine del MIB e viene in genere chiamato dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **not_used_ptr** Puntatore non usato: deve essere NX_NULL.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto di fine mib è stato compilato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Place an end-of-mib value in my_object.  */
status =  nx_snmp_object_end_of_mib(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now an end-of-mib object. */
```

## <a name="nx_snmp_object_gauge_get"></a>nx_snmp_object_gauge_get
Ottenere l'oggetto misuratore 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_gauge_get(VOID *source_ptr, 
                               NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'oggetto misuratore in corrispondenza dell'indirizzo specificato dall'indicatore di misura di origine e lo inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine del misuratore.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto misuratore è stato recuperato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of ifSpeed (1.3.6.1.2.1.2.2.1.5.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_gauge_get(&ifSpeed, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ifSpeed gauge value. */
```

## <a name="nx_snmp_object_gauge_set"></a>nx_snmp_object_gauge_set
Impostare l'oggetto misuratore 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_gauge_set(VOID *destination_ptr,
                                     NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il misuratore in corrispondenza dell'indirizzo specificato dall'indicatore di misura di destinazione con il valore del misuratore nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore alla destinazione del misuratore.
- **object_data** Puntatore alla struttura dell'oggetto di origine del misuratore.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto misuratore è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the value of “my_gauge” from the gauge value in my_object.  */
status =  nx_snmp_object_gauge_set(&my_gauge, my_object);

/* If status is NX_SUCCESS, the my_gauge now contains the new gauge value. */
```

## <a name="nx_snmp_object_id_get"></a>nx_snmp_object_id_get
Ottenere l'ID oggetto 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_id_get(VOID *source_ptr, 
                            NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'ID oggetto (in notazione SIM ASCII) in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine ID oggetto.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'ID oggetto è stato recuperato correttamente.
- **NX_SNMP_ERROR** (0x100) Lunghezza dell'oggetto non valida
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of sysObjectID(1.3.6.1.2.1.1.2.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_id_get(&sysObjectID, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysObjectID value. */
```

## <a name="nx_snmp_object_id_set"></a>nx_snmp_object_id_set
Impostare l'ID oggetto 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_id_set(VOID *destination_ptr, 
                             NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'ID oggetto (in notazione SIM ASCII) in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con l'ID oggetto nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore alla destinazione dell'ID oggetto.
- **object_data** Puntatore alla struttura dell'oggetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'ID oggetto è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the string “my_object_id” with the object ID value contained 
   in my_object.  */
status =  nx_snmp_object_id_set(my_object_id, my_object);

/* If status is NX_SUCCESS, the my_object_id now contains the object ID value. */
```

## <a name="nx_snmp_object_integer_get"></a>nx_snmp_object_integer_get
Ottenere l'oggetto integer 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_integer_get(VOID *source_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'oggetto integer in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine integer.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto Integer è stato recuperato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of sysServices (1.3.6.1.2.1.1.7.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_integer_get(&sysServices, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysServices value. */
```

## <a name="nx_snmp_object_integer_set"></a>nx_snmp_object_integer_set
Impostare un oggetto integer 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_integer_set(VOID *destination_ptr,
                                      NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'intero in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con il valore intero nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore alla destinazione integer.
- **object_data** Puntatore alla struttura dell'oggetto di origine integer.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto Integer è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the value of ifAdminStatus from the integer value in my_object.  */
status =  nx_snmp_object_integer_set(&ifAdminStatus, my_object);

/* If status is NX_SUCCESS, ifAdnminStatus now contains the new integer value. */
```

## <a name="nx_snmp_object_ip_address_get"></a>nx_snmp_object_ip_address_get
Ottenere l'oggetto indirizzo IP (solo IPv4)

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_ip_address_get(VOID *source_ptr,
                                          NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'oggetto indirizzo IP in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine dell'indirizzo IPv4.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto indirizzo IP è stato recuperato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of ipAdEntAddr (1.3.6.1.2.1.4.20.1.1.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_ip_address_get(&ipAdEntAddr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ipAdEntAddr value. */
```

## <a name="nx_snmp_object_ipv6_address_get"></a>nx_snmp_object_ipv6_address_get
Ottenere l'oggetto indirizzo IP (solo IPv6)

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_ipv6_address_get(VOID *source_ptr,
                                          NX_SNMP_OBJECT_DATA 
                                      *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'oggetto indirizzo IPv6 in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.
Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine dell'indirizzo IPv6.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto indirizzo IP è stato recuperato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Codice oggetto SNMP di input non corretto
- **NX_NOT_ENABLED** (0x14) IPv6 non abilitato
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of ipAdEntAddr (1.3.6.1.2.1.4.20.1.1.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_ipv6_address_get(&ipAdEntAddr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ipAdEntAddr value. */
```

## <a name="nx_snmp_object_ip_address_set"></a>nx_snmp_object_ip_address_set
Impostare l'oggetto indirizzo IPv4 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_ip_address_set(VOID *destination_ptr, 
                                    NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IPv4 in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con l'indirizzo IP nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore all'indirizzo IP da impostare.
- **object_data** Puntatore alla struttura dell'oggetto indirizzo IP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto indirizzo IP è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the value of atNetworkAddress to the IP address in my_object.  */
status =  nx_snmp_object_ip_address_set(&atNetworkAddress, my_object);

/* If status is NX_SUCCESS, atNetWorkAddress now contains the new IP address. */
```

## <a name="nx_snmp_object_ipv6_address_set"></a>nx_snmp_object_ipv6_address_set
Impostare l'oggetto indirizzo IPv6 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_ipv6_address_set(VOID *destination_ptr, 
                                      NX_SNMP_OBJECT_DATA  
                                      *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IPv6 in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con l'indirizzo IP nella struttura di dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore all'indirizzo IP da impostare.
- **object_data** Puntatore alla struttura dell'oggetto indirizzo IP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo IPv6 è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_NOT_ENABLED** (0x14) IPv6 non abilitato
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the value of atNetworkAddress to the IP address in my_object.  */
status =  nx_snmp_object_ipv6_address_set(&atNetworkAddress, my_object);

/* If status is NX_SUCCESS, atNetWorkAddress now contains the new IP address. */
```

## <a name="nx_snmp_object_no_instance"></a>nx_snmp_object_no_instance
Impostare un oggetto senza istanza 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_no_instance(VOID *not_used_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio crea un oggetto che segnala che non è presente alcuna istanza dell'oggetto specificato e viene in genere chiamato dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **not_used_ptr** Puntatore non usato: deve essere NX_NULL.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto senza istanza è stato compilato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Place no-instance value in my_object.  */
status =  nx_snmp_object_no_instance(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now a no-instance object. */
```

## <a name="nx_snmp_object_not_found"></a>nx_snmp_object_not_found
Impostare l'oggetto non trovato 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_not_found(VOID *not_used_ptr, 
                               NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio crea un oggetto che segnala che l'oggetto non è stato trovato e viene in genere chiamato dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **not_used_ptr** Puntatore non usato: deve essere NX_NULL.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto non trovato è stato compilato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Place not-found value in my_object.  */
status =  nx_snmp_object_not_found(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now a not-found object. */
```

## <a name="nx_snmp_object_octet_string_get"></a>nx_snmp_object_octet_string_get
Ottenere l'oggetto stringa dell'ottetto 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_octet_string_get(VOID *source_ptr,
                                            NX_SNMP_OBJECT_DATA *object_data, 
                                      UINT length);
```
### <a name="description"></a>Descrizione

Questo servizio recupera la stringa dell'ottetto in corrispondenza dell'indirizzo specificato dal puntatore di origine e la inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine della stringa dell'ottetto.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.
- **lunghezza** Numero di byte nella stringa dell'ottetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto stringa ottetto è stato recuperato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of the 6-byte ifPhysAddress (1.3.6.1.2.1.2.2.1.6.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_octet_string_get(ifPhysAddress, my_object, 6);

/* If status is NX_SUCCESS, the my_object now contains the ifPhysAddress value. */
```

## <a name="nx_snmp_object_octet_string_set"></a>nx_snmp_object_octet_string_set
Impostare l'oggetto stringa dell'ottetto 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_octet_string_set(VOID *destination_ptr, 
                                      NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la stringa dell'ottetto in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con la stringa dell'ottetto nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore alla destinazione della stringa dell'ottetto.
- **object_data** Puntatore alla struttura dell'oggetto di origine della stringa dell'ottetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto stringa ottetto è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the value of sysContact (1.3.6.1.2.1.1.4.0) from the 
   octet string in my_object.  */
status =  nx_snmp_object_octet_string_set(sysContact, my_object);

/* If status is NX_SUCCESS, sysContact now contains the new octet string. */
```

## <a name="nx_snmp_object_string_get"></a>nx_snmp_object_string_get
Ottenere l'oggetto stringa ASCII 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_string_get(VOID *source_ptr, 
                                NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio recupera la stringa ASCII in corrispondenza dell'indirizzo specificato dal puntatore di origine e la inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine stringa ASCII.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto stringa ASCII è stato recuperato correttamente.
- **NX_SNMP_ERROR** (0x100) La stringa è troppo grande  
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of the sysDescr (1.3.6.1.2.1.1.1.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_string_get(sysDescr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysDescr string. */
```

## <a name="nx_snmp_object_string_set"></a>nx_snmp_object_string_set
Impostare l'oggetto stringa ASCII 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_string_set(VOID *destination_ptr, 
                                NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la stringa ASCII in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con la stringa ASCII nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore alla destinazione della stringa ASCII.
- **object_data** Puntatore alla struttura dell'oggetto di origine della stringa ASCII.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto stringa ASCII è stato impostato correttamente.
- **NX_SNMP_ERROR** (0x100) Stringa troppo grande.
- **NX_SNMP_ERROR_BADVALUE** (0x03) Carattere non valido nella stringa
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the value of sysContact (1.3.6.1.2.1.1.4.0) from the 
   ASCII string in my_object.  */
status =  nx_snmp_object_string_set(sysContact, my_object);

/* If status is NX_SUCCESS, sysContact now contains the new ASCII string. */
```

## <a name="nx_snmp_object_timetics_get"></a>nx_snmp_object_timetics_get
Ottenere l'oggetto timetics 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_timetics_get(VOID *source_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio recupera i tempi in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX. Questa routine viene in genere chiamata dalla routine di callback dell'applicazione GET o GETNEXT.

### <a name="input-parameters"></a>Parametri di input

- **source_ptr** Puntatore all'origine temporale.
- **object_data** Puntatore alla struttura dell'oggetto di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto timetics è stato recuperato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Get the value of the sysUpTime (1.3.6.1.2.1.1.3.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_timetics_get(sysUpTime, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysUpTime value. */
```

## <a name="nx_snmp_object_timetics_set"></a>nx_snmp_object_timetics_set
Impostare l'oggetto timetics 

### <a name="prototype"></a>Prototipo

```c
UINT  nx_snmp_object_timetics_set(VOID *destination_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la variabile timetics in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con i valori temportici nella struttura dei dati dell'oggetto NetX.
Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.

### <a name="input-parameters"></a>Parametri di input

- **destination_ptr** Puntatore alla destinazione timetics.
- **object_data** Puntatore alla struttura dell'oggetto di origine timetics.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'oggetto timetics è stato impostato correttamente.
- **NX_SNMP_ERROR_WRONGTYPE** (0x07) Tipo di oggetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di input non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set the value of “my_time” from the timetics value in my_object.  */
status =  nx_snmp_object_timetics_set(&my_time, my_object);

/* If status is NX_SUCCESS, my_time now contains the new timetics. */
```