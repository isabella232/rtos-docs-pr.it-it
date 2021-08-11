---
title: Capitolo 3 - Descrizione dei Azure RTOS server PPPoE NetX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX PPPoE Server (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d184fc3c5e6ed74ef25045561b1613e280672f77385fbb13b8e84bccf051b301
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782812"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-server-services"></a>Capitolo 3 - Descrizione dei Azure RTOS server PPPoE NetX

Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX PPPoE Server (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **grassetto** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_pppoe_server_create**: *Creare un'istanza del server PPPoE*

- **nx_pppoe_server_ac_name_set:** Impostare *il nome del concentratore di accesso*

- **nx_pppoe_server_delete:** Eliminare *un'istanza del server PPPoE*

- **nx_pppoe_server_enable:** Abilitare *i servizi del server PPPoE*

- **nx_pppoe_server_disable:** *Disabilitare i servizi del server PPPoE*

- **nx_pppoe_server_callback_notify_set:** Impostare le funzioni di notifica di callback del *server PPPoE*

- **nx_pppoe_server_service_name_set:** impostare *il nome del servizio del server PPPoE*

- **nx_pppoe_server_session_send:** *Inviare i dati del server PPPoE alla sessione specificata*

- **nx_pppoe_server_session_packet_send:** *Inviare il pacchetto del server PPPoE alla sessione specificata*

- **nx_pppoe_server_session_terminate**: *termina la sessione PPPoE specificata*

- **nx_pppoe_server_session_get:** ottenere *le informazioni sulla sessione specificata*

## <a name="nx_pppoe_server_create"></a>nx_pppoe_server_create

Creare un'istanza del server PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_create(NX_PPPOE_SERVER *pppoe_server_ptr,
                            CHAR *name, NX_IP *ip_ptr,
                            UINT interface_index,
                            VOID (*pppoe_link_driver)
                            (struct NX_IP_DRIVER_STRUCT *)
                            NX_PACKET_POOL *pool_ptr,
                            VOID *stack_ptr, ULONG stack_size,
                            UINT priority);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza di PPPoE Server con il driver di collegamento fornito dall'utente per l'istanza IP NetX specificata. Se il driver di collegamento non è stato inizializzato e abilitato, il software del server PPPoE è responsabile dell'inizializzazione del driver di collegamento.

Inoltre, l'applicazione deve fornire un pool di pacchetti creato in precedenza per l'istanza del server PPPoE da usare per l'allocazione interna dei pacchetti.

Si noti che in genere è consigliabile creare il thread IP NetX con una priorità più alta rispetto alla priorità del thread del server PPPoE. Per altre informazioni su come specificare la priorità del thread *IP,* vedere il servizio di nx_ip_create ip.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.
- **name:** nome dell'istanza del server PPPoE.
- **ip_ptr:** puntatore al blocco di controllo per l'istanza IP.
- **interface_index:** indice di interfaccia.
- **pppoe_link_driver:** driver di collegamento fornito dall'utente.
- **pool_ptr:** puntatore al pool di pacchetti.
- **stack_ptr:** puntatore all'inizio dell'area dello stack del thread del server PPPoE.
- **stack_size**: dimensioni in byte nello stack del thread.
- **priority:** priorità dei thread interni del server PPPoE (1-31).

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Creazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Server PPPoE, IP, pool di pacchetti o puntatore dello stack non valido.
- NX_PPPOE_SERVER_INVALID_INTERFACE: (0xC2) Interfaccia non valida.
- NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) Dimensioni del payload del pool di pacchetti non valide.
- NX_PPPOE_SERVER_MEMORY_SIZE_ERROR: (0xC4) Dimensioni della memoria non valide.
- NX_PPPOE_SERVER_PRIORITY_ERROR: (0xC5) Priorità del thread del server PPPoE non valida.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create "my_pppoe_server" for IP instance "my_ip". */
status = nx_pppoe_server_create(&my_pppoe_server, "my PPPoE Server", &my_ip,
                                &my_pool, stack_start, 1024, 2);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully created. */
```

## <a name="nx_pppoe_server_delete"></a>nx_pppoe_server_delete

Eliminare un'istanza del server PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_delete(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina l'istanza del server PPPoE creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore PPPoE Server non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_delete(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully deleted. */
```

## <a name="nx_pppoe_server_enable"></a>nx_pppoe_server_enable

Abilitare il servizio PPPoE Server

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_enable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita i servizi PPPoE Server.

> [!NOTE]
> Questa funzione deve essere chiamata dopo *nx_pppoe_server_create* e *nx_pppoe_server_callback_notify_set*.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore PPPoE Server non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Enable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_enable(&my_pppoe_server);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has enabled. */
```

## <a name="nx_pppoe_server_disable"></a>nx_pppoe_server_disable

Disabilitare il servizio PPPoE Server

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_disable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita i servizi PPPoE Server.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore PPPoE Server non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Disable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_disable(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has disabled. */
```

## <a name="nx_pppoe_server_callback_notify_set"></a>nx_pppoe_server_callback_notify_set

Impostare le funzioni di notifica di callback del server PPPoE 

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_callback_notify_set(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        VOID (* pppoe_discover_initiation_notify)(UINT session_index,
                ULONG length, UCHAR *data),
        VOID (* pppoe_discover_request_notify)(UINT session_index),
        VOID (* pppoe_discover_terminate_notify)(UINT session_index),
        VOID (* pppoe_discover_terminate_confirm)(UINT session_index),
        VOID (* pppoe_data_receive_notify)(UINT session_index,
                ULONG length, UCHAR *data, UINT packet_id),
        VOID (* pppoe_discover_notify)(UINT session_index, UCHAR *data))
```

### <a name="description"></a>Descrizione

Questo servizio imposta le funzioni di notifica di callback del server PPPoE.

> [!NOTE]
> Questa funzione deve essere chiamata *prima nx_pppoe_server_enabl e il* puntatore pppoe_data_receive_notify deve essere impostato. In caso contrario, nx_pppoe_server_enable errore. 

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.
- **pppoe_discover_initiation_notify:** funzione dell'applicazione che viene chiamata ogni volta che viene ricevuto il messaggio di avvio di individuazione PPPoE. Se questo valore è NULL, la funzione di callback di individuazione dell'avvio è disabilitata.
- **pppoe_discover_request_notify:** funzione dell'applicazione che viene chiamata ogni volta che viene ricevuto un messaggio di richiesta di individuazione PPPoE. Se questo valore è NULL, la funzione di callback della richiesta di individuazione è disabilitata.
- **pppoe_discover_terminate_notify:** funzione dell'applicazione che viene chiamata ogni volta che viene ricevuto il messaggio di terminazione di individuazione PPPoE. Se questo valore è NULL, la funzione di callback discover terminate è disabilitata.
- **pppoe_discover_terminate_confirm:** funzione dell'applicazione che viene chiamata ogni volta che viene inviato il messaggio di terminazione di individuazione PPPoE. Se questo valore è NULL, la funzione di callback discover terminate è disabilitata.
- **pppoe_data_receive_notify:** funzione dell'applicazione che viene chiamata ogni volta che viene ricevuto un messaggio di dati PPPoE. Questo valore non deve essere zero.
- **pppoe_data_send_notify:** funzione dell'applicazione che viene chiamata ogni volta che viene inviato un messaggio di dati PPPoE. Se questo valore è NULL, la funzione di callback di invio dati è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore al server PPPoE o puntatore a funzione non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set PPPoE Server callback notify functions, PPPoE Server instance "my_pppoe_server". */

status = nx_pppoe_server_disable(&my_pppoe_server,
                pppoe_discovery_initiation_notify,
                pppoe_discovery_request_notify,
                pppoe_discovery_terminate_notify,
                pppoe_discovery_terminate_confirm,
                pppoe_data_receive_notify,
                pppoe_data_send_notify);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the callback notify functions for "my_pppoe_server" service has set. */
```

## <a name="nx_pppoe_server_ac_name_set"></a>nx_pppoe_server_ac_name_set

Impostare il nome del concentratore di accesso

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_ac_name_set(
    NX_PPPOE_SERVER *pppoe_server_ptr,
    CHAR *ac_name, UINT ac_name_length,
);
```

### <a name="description"></a>Descrizione

Questo set di funzioni consente di accedere al nome del concentrar e di chiamare la funzione.

> [!NOTE]
> La stringa di ac_name deve avere terminazione NULL e la lunghezza di ac_name corrisponde alla lunghezza specificata nell'elenco di argomenti.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.
- **ac_name:** accedere al nome di Concentrar.
- **ac_name_length**: lunghezza del ac_ame.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Set di server PPPoE riuscito.
- **NX_PPPOE_SERVER_PTR_ERROR**: (0xC1) Server PPPoE, IP, pool di pacchetti o puntatore dello stack non valido.
- **NX_SIZE_ERROR:**(0x09) Controllare name_length esito negativo.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Set "my PPPoE ac name" for Server instance "my_pppoe_server". */
status = nx_pppoe_server_ac_name_set(&my_pppoe_server, "my PPPoE ac name",16);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my PPPoE ac name" was successfully set. */
```

## <a name="nx_pppoe_server_service_name_set"></a>nx_pppoe_server_service_name_set

Impostare il nome del servizio del server PPPoE

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_service_name_set(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UCHAR **service_name, UINT service_name_count);
```

### <a name="description"></a>Descrizione

Questo servizio imposta il nome del servizio del server PPPoE.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore PPPoE Server non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
CHAR *nx_pppoe_service_name[] =
{
    "XBB",
    "PRINTER",
    NX_NULL
};

/* Set service name for PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_service_namet_set(&my_pppoe_server,
                                    nx_pppoe_service_name, 2);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service name has set. */
```

## <a name="nx_pppoe_server_session_send"></a>nx_pppoe_server_session_send

Inviare i dati del server PPPoE alla sessione specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_session_send (NX_PPPOE_SERVER *pppoe_server_ptr,
                UINT session_index, UCHAR *data_ptr, UINT data_length);
```

### <a name="description"></a>Descrizione

Questo servizio invia un frame PPPoE usando l'ID sessione specificato.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.
- **session_index:** indice della sessione.
- **data_ptr:** puntatore all'inizio del frame di dati del server PPPoE.
- **data_length:** lunghezza del frame di dati del server PPPoE.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore PPPoE Server non valido.
- NX_PPPOE_SERVER_NOT_ENABLED: il servizio PPPoE Server (0xC6) non è abilitato.
- NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Indice di sessione PPPoE non valido.
- NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: la sessione PPPoE (0xC8) non è stata stabilita.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Send PPPoE Server data to specified session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_send(&my_pppoe_server, 0, my_data_ptr, 1400);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" data has sent. */
```

## <a name="nx_pppoe_server_session_packet_send"></a>nx_pppoe_server_session_packet_send

Invia pacchetto pppoe server alla sessione specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_session_packet_send (
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UINT session_index, NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invia il pacchetto PPPoE usando l'ID sessione specificato.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.
- **session_index:** indice della sessione.
- **packet_ptr:** puntatore al pacchetto PPPoE.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore PPPoE Server non valido.
- NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) Pacchetto del server PPPoE non valido.
- NX_PPPOE_SERVER_NOT_ENABLED: il servizio PPPoE Server (0xC6) non è abilitato.
- NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Indice di sessione PPPoE non valido.
- NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: la sessione PPPoE (0xC8) non è stata stabilita.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Send PPPoE Server data to specified session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_packet_send(&my_pppoe_server, 0, packet_ptr);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" packet has sent. */
```

## <a name="nx_pppoe_server_session_terminate"></a>nx_pppoe_server_session_terminate

Termina la sessione PPPoE specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_session_terminate(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UINT session_index);
```

### <a name="description"></a>Descrizione

Questo servizio termina la sessione PPPoE specificata.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.
- **session_index:** indice della sessione.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore PPPoE Server non valido.
- NX_PPPOE_SERVER_NOT_ENABLED: il servizio PPPoE Server (0xC6) non è abilitato.
- NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Indice di sessione PPPoE non valido.
- NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: la sessione PPPoE (0xC8) non è stata stabilita.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Terminates the specified PPPoE session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_send(&my_pppoe_server, 0);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the session indexed with 0 has terminated. */
```

## <a name="nx_pppoe_server_session_get"></a>nx_pppoe_server_session_get

Ottiene le informazioni sulla sessione PPPoE specificata

### <a name="prototype"></a>Prototipo

```c
UINT nx_pppoe_server_session_get(NX_PPPOE_SERVER *pppoe_server_ptr,
                                UINT session_index
                                ULONG *client_mac_msw,
                                ULONG *client_mac_lsw,
                                ULONG *session_id);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene le informazioni di sessione PPPoE specificate, l'indirizzo fisico del client e l'ID sessione.

### <a name="input-parameters"></a>Parametri di input

- **pppoe_server_ptr:** puntatore al blocco di controllo del server PPPoE.
- **session_index:** indice della sessione.
- **client_mac_msw:** puntatore MSW indirizzo fisico client.
- **client_mac_lsw:** puntatore MSW dell'indirizzo fisico client.
- **session_id:** puntatore ID sessione.

### <a name="return-values"></a>Valori restituiti

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Eliminazione del server PPPoE completata.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Puntatore del server PPPoE non valido.
- NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Indice di sessione PPPoE non valido.
- NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: la sessione PPPoE (0xC8) non è stata stabilita.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Gets the specified PPPoE session information, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_get (&my_pppoe_server, 0, &client_mac_msw, &client_mac_lsw, &session_id);

/* If status is NX_PPPOE_SERVER_SUCCESS, the client physical address and session id of the session indexed with 0 has got. */
```

## <a name="pppinitind"></a>PppInitInd

Configurare il nome del servizio predefinito

### <a name="prototype"></a>Prototipo

```c
VOID PppInitnd(UINT length, UCHAR *aData);
```

### <a name="description"></a>Descrizione

Il software PPPoE esporrà questa funzione per consentire al software TTP di configurare il "nome del servizio predefinito" che PPPoE deve usare per filtrare le richieste PADI in ingresso. Il software PPPoE deve ricordare queste informazioni e, se viene ricevuto un pacchetto PADI contenente un nome di servizio corrispondente, deve chiamare PppDiscoverReq.

### <a name="input-parameters"></a>Parametri di input

- **length**: lunghezza del nome del servizio predefinito.
- **aData:** nome del servizio predefinito.

### <a name="return-values"></a>Valori restituiti

**Nessuno**

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Configure the default Service Name. */
PppInitInd (3, "XBB");
```

## <a name="pppdiscovercnf"></a>PppDiscoverCnf

Definire il campo Service Name (Nome servizio) del pacchetto PADO

### <a name="prototype"></a>Prototipo

```c
VOID PppDiscoverCnf (UINT length, UCHAR *aData, UINT interfaceHandle);
```

### <a name="description"></a>Descrizione

Il software PPPoE esporrà questa funzione per consentire al software TTP di definire il campo Nome servizio del pacchetto PADO. Il software PPPoE non deve inviare PADO fino a quando non viene chiamato PppDiscoverCnf.

Il pacchetto PADO deve contenere un nome concentratore di accesso (usando l'ID tag 0x0102 come definito in RFC2516), definito all'inizializzazione del software PPPoE.

È possibile passare più nomi di servizio in aData, con ogni nome che deve essere null terminato.

Il carattere Null viene usato come separatore per offrire la massima flessibilità nel caso in cui altri comandi devono essere passati come parte del nome del servizio.

### <a name="input-parameters"></a>Parametri di input

- **length**: lunghezza del nome del servizio predefinito.
- **aData:** nome del servizio predefinito.
- **interfaceHandle:** handle di interfaccia.

### <a name="return-values"></a>Valori restituiti

**Nessuno**

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Define the Service Name field of the PADO packet. */
PppDiscoverCnf (3, "XBB", 0);
```

## <a name="pppopencnf"></a>PppOpenCnf

Accettare o rifiutare la sessione PPPoE

### <a name="prototype"></a>Prototipo

```c
VOID PppOpenCnf (UCHAR accept, UINT interfaceHandle);
```

### <a name="description"></a>Descrizione

Il software PPPoE esporrà questa funzione per consentire al software TTP di accettare o rifiutare la sessione PPPoE.  In risposta a questo, lo stack PPPoE deve accettare la connessione e assegnare un numero Session_ID PPPoE univoco associato a interfaceHandle.

### <a name="input-parameters"></a>Parametri di input

- **accept**: NX_TRUE se la connessione deve essere accettata.
- **interfaceHandle:** handle di interfaccia.

### <a name="return-values"></a>Valori restituiti

**Nessuno**

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Accept the connection. */
PppOpenCnf(NX_TRUE, 0);
```

## <a name="pppcloseind"></a>PppCloseInd

Chiudere una sessione PPPoE

### <a name="prototype"></a>Prototipo

```c
VOID PppCloseInd (UINT interfaceHandle, UCHAR *causeCode);
```

### <a name="description"></a>Descrizione

Il software PPPoE esporrà questa funzione per consentire al software TTP di chiudere una sessione PPPoE.

Il software PPPoE indicherà la stringa del codice di causa nel tag Generic-Error (0x0203) nel messaggio PADT

### <a name="input-parameters"></a>Parametri di input

- **interfaceHandle:** handle di interfaccia.
- **causeCode:** stringa con terminazione Null per l'invio di informazioni sul motivo della chiusura della connessione dal server PPPoE.

### <a name="return-values"></a>Valori restituiti

**Nessuno**

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Close a PPPoE session. */
PppCloseInd(0, NX_NULL);
```

## <a name="pppclosecnf"></a>PppCloseCnf

Verificare che l'handle sia stato liberato

### <a name="prototype"></a>Prototipo

```c
VOID PppCloseCnf (UINT interfaceHandle);
```

### <a name="description"></a>Descrizione

Il software PPPoE esporrà questa funzione per consentire al software TTP di confermare che l'handle è stato liberato.

### <a name="input-parameters"></a>Parametri di input

- **interfaceHandle:** handle di interfaccia.

### <a name="return-values"></a>Valori restituiti

**Nessuno**

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Confirm that the handle has been freed. */
PppCloseCnf(0);
```

## <a name="ppptransmitdatacnf"></a>PppTransmitDataCnf

Consentire l'riconoscimento di dati PPP precedenti

### <a name="prototype"></a>Prototipo

```c
VOID PppTransmitDataCnf (UINT interfaceHandle, UCHAR *aData,
                        UINT packet_id);
```

### <a name="description"></a>Descrizione

Il software PPPoE esporrà questa funzione per consentire il riconoscimento di un PppTransmitDataReq precedente.  Implica che il software TTP è pronto per un nuovo frame PPP da PPPoE.

### <a name="input-parameters"></a>Parametri di input

- **interfaceHandle:** handle di interfaccia.
- **aData:** puntatore al buffer di dati PPP accettato.
- **Packet_id**: identificatore di pacchetto.

### <a name="return-values"></a>Valori restituiti

**Nessuno**

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
UINT packet_id = 0x20015429

/* Allow a preceding PPP data to be acknowledged, let PPPoE Server release the packet with same packet identifier. */
PppTransmitDataCnf(0, NX_NULL, packet_id);
```

## <a name="pppreceivedataind"></a>PppReceiveDataInd

Ricevere dati dalla trasmissione tramite Ethernet

### <a name="prototype"></a>Prototipo

```c
VOID PppReceiveDataInd(UINT interfaceHandle, UINT length, UCHAR *aData);
```

### <a name="description"></a>Descrizione

Il software PPPoE esporrà questa funzione per ricevere dati per la trasmissione tramite Ethernet

### <a name="input-parameters"></a>Parametri di input

- **interfaceHandle:** handle di interfaccia.
- **length**: numero di byte in aData.
- **aData:** buffer di dati contenente il frame di dati PPP.

### <a name="return-values"></a>Valori restituiti

**Nessuno**

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Receive data from transmission over Ethernet, data start pointer is aData.
The number of bytes in aData is 1480. */
PppReceiveDataInd (0, 1480, aData);
```