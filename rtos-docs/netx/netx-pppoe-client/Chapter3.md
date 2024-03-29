---
title: Capitolo 3 - Descrizione dei Azure RTOS client PPPoE NetX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS client NETX PPPoE (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8310006b7c188fa63402c931459ffd84ebb776c207dc520959208449862fe27f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790208"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-client-services"></a>Capitolo 3 - Descrizione dei Azure RTOS client PPPoE NetX

Questo capitolo contiene una descrizione di tutti i Azure RTOS client NETX PPPoE (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_pppoe_client_create** *creare un'istanza del client PPPoE*
- **nx_pppoe_client_delete** *eliminare un'istanza del client PPPoE*
- **nx_pppoe_client_host_uniq_set** *l'host univoco per il client PPPoE*
- **nx_pppoe_client_host_uniq_set_extended** *l'host univoco per il client PPPoE*
- **nx_pppoe_client_service_name_set** *il nome del servizio per il client PPPoE*
- **nx_pppoe_client_service_name_set_extended** *impostare il nome del servizio per il client PPPoE*
- **nx_pppoe_client_session_connect** *Connessione sessione client PPPoE nel server PPPoE*
- **nx_pppoe_client_session_packet_send** *pacchetto di sessione PPPoE*
- **nx_pppoe_client_session_terminate** *terminare la sessione PPPoE*
- **nx_pppoe_client_session_get** *ottenere l'inf della sessione PPPoE specificata*

## <a name="nx_pppoe_client_create"></a>nx_pppoe_client_create

Creare un'istanza del client PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT  nx_pppoe_client_create(NX_PPPOE_CLIENT *pppoe_client_ptr,
                            CHAR *name, NX_IP *ip_ptr,
                            UINT interface_index,
                            NX_PACKET_POOL *pool_ptr,
                            VOID *stack_ptr, ULONG stack_size,
                            UINT priority,
                            VOID (*pppoe_link_driver)
                            (struct NX_IP_DRIVER_STRUCT *)
                            VOID (*pppoe_packet_receive)
                            (NX_PACKET *packet_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client PPPoE con il driver di collegamento fornito dall'utente per l'istanza IP NetX specificata. Se il driver di collegamento non è stato inizializzato e abilitato, il software client PPPoE è responsabile dell'inizializzazione del driver di collegamento.

Inoltre, l'applicazione deve fornire un pool di pacchetti creato in precedenza per l'istanza del client PPPoE da usare per l'allocazione interna dei pacchetti.

> [!NOTE]
> In genere è consigliabile creare il thread IP NetX con una priorità più alta rispetto alla priorità del thread del client PPPoE. Fare riferimento al servizio *nx_ip_create* per altre informazioni su come specificare la priorità del thread IP.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.
 - **name** Nome di questa istanza del client PPPoE.
 - **ip_ptr** Puntatore al blocco di controllo per l'istanza IP.
 - **interface_index** Indice dell'interfaccia.
 - **pool_ptr** Puntatore al pool di pacchetti.
 - **stack_ptr** Puntatore all'inizio dell'area dello stack del thread client PPPoE.
 - **stack_size** Dimensione in byte nello stack del thread.
 - **priorità** Priorità dei thread interni del client PPPoE (1-31).
 - **pppoe_link_driver** Driver di collegamento fornito dall'utente.
 - **pppoe_packet_receive** Funzione di ricezione pacchetti fornita dall'utente.

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Creazione del client PPPoE completata.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Client PPPoE, IP, pool di pacchetti o puntatore dello stack non valido.
 - NX_PPPOE_CLIENT_INVALID_INTERFACE (0xD2) Interfaccia non valida.
 - NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) Dimensioni del payload del pool di pacchetti non valide.
 - NX_PPPOE_CLIENT_MEMORY_SIZE_ERROR (0xD4) Dimensioni della memoria non valide.
 - NX_PPPOE_CLIENT_PRIORITY_ERROR (0xD5) Priorità del thread client PPPoE non valida.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create “my_pppoe_client” for IP instance “my_ip”. */
status =  nx_pppoe_client_create(&my_pppoe_client, “my PPPoE Client”, &my_ip,
0, &my_pool, stack_start, 1024, 2,
link_driver, packet_receive);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully created. */
```

## <a name="nx_pppoe_client_delete"></a>nx_pppoe_client_delete

Eliminare un'istanza del client PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_delete(NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina l'istanza del client PPPoE creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Eliminazione del client PPPoE completata.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Puntatore client PPPoE non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_delete(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully deleted. */
```

## <a name="nx_pppoe_client_host_uniq_set"></a>nx_pppoe_client_host_uniq_set

Impostare l'host client PPPoE univoco

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_host_uniq_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'host client PPPoE univoco. Host-Uniq viene usato da un host per associare in modo univoco un concentratore di accesso a una richiesta host specifica.
Possono essere dati binari di qualsiasi valore e lunghezza che l'host sceglie.

> [!NOTE]
> host unique deve essere una stringa con terminazione Null.

> [!NOTE]
> questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione *a nx_pppoe_client_host_uniq_set_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.
 - **host_uniq** Puntatore a un host univoco. L'host univoco deve essere una stringa con terminazione Null.

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Set univoco host client PPPoE riuscito.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Puntatore client PPPoE non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set(&my_pppoe_client,
“220000000000000041000000”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_host_uniq_set_extended"></a>nx_pppoe_client_host_uniq_set_extended

Impostare l'host client PPPoE univoco

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_host_uniq_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq,UINT host_uniq_length);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'host client PPPoE univoco. Host-Uniq viene usato da un host per associare in modo univoco un concentratore di accesso a una richiesta host specifica.
Possono essere dati binari di qualsiasi valore e lunghezza che l'host sceglie.

> [!NOTE]
> host unique deve essere una stringa con terminazione Null.

> [!NOTE]
> Questo servizio sostituisce *nx_pppoe_client_host_uniq_set()*. Questa versione fornisce informazioni aggiuntive sulla lunghezza al servizio.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.
 - **host_uniq** Puntatore a un host univoco. L'host univoco deve essere una stringa con terminazione Null.
 - **host_uniq_length** Lunghezza del host_uniq

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Set univoco host client PPPoE riuscito.
 - **NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Puntatore client PPPoE non valido.
 - **NX_SIZE_ERROR** (0x09) Controllare host_uniq_length esito negativo

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set_extended(&my_pppoe_client,
“220000000000000041000000”,24);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_service_name_set"></a>nx_pppoe_client_service_name_set

Impostare il nome del servizio client PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_service_name_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *service_name);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il nome del servizio client PPPoE. Valore Service-Name che indica il servizio richiesto dall'host. Se Service-Name non è impostato, l'host accetterà un numero qualsiasi di servizi.

> [!NOTE]
> il nome del servizio deve essere una stringa con terminazione Null

> [!NOTE]
> questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione *a nx_pppoe_client_service_name_set_extended()*.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.
 - **service_name** Puntatore a un nome di servizio. Il nome del servizio deve essere una stringa con terminazione Null.

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Set di nomi di servizio client PPPoE riuscito.
 - **NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Puntatore client PPPoE non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_service_name_set(&my_pppoe_client,
“BRAS”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” service name has set. */
```

## <a name="nx_pppoe_client_service_name_set_extended"></a>nx_pppoe_client_service_name_set_extended

Impostare il nome del servizio client PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_service_name_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *service_name,UINT service_name_length);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il nome del servizio client PPPoE. Valore Service-Name che indica il servizio richiesto dall'host. Se Service-Name non è impostato, l'host accetterà un numero qualsiasi di servizi.

> [!NOTE]
> il nome del servizio deve essere una stringa con terminazione Null.

> [!NOTE]
> Questo servizio sostituisce *nx_pppoe_client_service_name_set()*. Questa versione fornisce informazioni aggiuntive sulla lunghezza del nome del servizio alla funzione.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.
 - **service_name** Puntatore a un nome di servizio. Il nome del servizio deve essere una stringa con terminazione Null.
 - **service_name_length** Lunghezza del service_name

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Set di nomi di servizio client PPPoE riuscito.
 - **NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Puntatore client PPPoE non valido.
 - **NX_SIZE_ERROR** (0x09) Controllare service_name_length esito negativo

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_service_name_set_extended(&my_pppoe_client,
“BRAS”,4);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” service name has set. */
```

## <a name="nx_pppoe_client_session_connect"></a>nx_pppoe_client_session_connect

Connessione Sessione client PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_session_connect(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio crea una connessione di sessione PPPoE usando un client PPPoE creato in precedenza al server PPPoE specificato.

> [!NOTE]
> Questa funzione deve essere chiamata *dopo* nx_pppoe_client_create , *nx_pppoe_client_host_uniq_set* e *nx_pppoe_client_service_name_set*.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.
 - **wait_option** Opzione di attesa durante la connessione.

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Connessione della sessione client PPPoE riuscita.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Puntatore client PPPoE non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Enable PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_connect(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” session connection has connected. */
```

## <a name="nx_pppoe_client_session_packet_send"></a>nx_pppoe_client_session_packet_send

Inviare un pacchetto client PPPoE alla sessione specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_session_packet_send(
                                    NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia il pacchetto PPPoE usando l'ID sessione specificato.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.
 - **packet_ptr** Puntatore al pacchetto PPPoE.

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Invio di pacchetti client PPPoE riuscito.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Puntatore client PPPoE non valido.
 - NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) Pacchetto client PPPoE non valido.
 - NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) la sessione PPPoE non è stata stabilita.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Send PPPoE client packet to specified session, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_packet_send(&my_pppoe_client, packet_ptr);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” packet has sent. */
```

## <a name="nx_pppoe_client_session_terminate"></a>nx_pppoe_client_session_terminate

Terminare la sessione client PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_session_terminate(
                                    NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio termina la sessione PPPoE specificata.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_client_ptr** Puntatore al blocco di controllo client PPPoE.

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Terminazione della sessione client PPPoE completata.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Puntatore client PPPoE non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Terminates the specified PPPoE session, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_terminate(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the session has terminated. */
```

## <a name="nx_pppoe_client_session_get"></a>nx_pppoe_client_session_get

Ottenere le informazioni sulla sessione PPPoE specificate

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_client_session_get(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                ULONG *server_mac_msw,
                                ULONG *server_mac_lsw,
                                ULONG *session_id);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene le informazioni di sessione PPPoE specificate, l'indirizzo fisico del server e l'ID sessione.

### <a name="input-parameters"></a>Parametri di input

 - **pppoe_server_ptr** Puntatore al blocco di controllo client PPPoE.
 - **server_mac_msw** Puntatore MSW dell'indirizzo fisico del server.
 - **server_mac_lsw** Puntatore MSW dell'indirizzo fisico del server.
 - **session_id** Puntatore ID sessione.

### <a name="return-values"></a>Valori restituiti

 - **NX_PPPOE_CLIENT_SUCCESS** (0x00) Riuscita della sessione client PPPoE.
 - NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Puntatore client PPPoE non valido.
 - NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) la sessione PPPoE non è stata stabilita.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Gets the specified PPPoE session information, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_get (&my_pppoe_client, &server_mac_msw, &server_mac_lsw, &session_id);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the server physical address and session id
   of the session has got. */
```
