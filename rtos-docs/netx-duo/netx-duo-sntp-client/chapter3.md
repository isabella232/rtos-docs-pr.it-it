---
title: Capitolo 3 - Descrizione dei Azure RTOS client NetX Duo SNTP
description: Questo capitolo contiene una descrizione di tutti i servizi client NetX Duo SNTP (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7aee18642e480ec61488515164c8a6816753dca86eb8f6d146ea22d4956e037a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791670"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-sntp-client-services"></a>Capitolo 3 - Descrizione dei Azure RTOS client NetX Duo SNTP

Questo capitolo contiene una descrizione di tutti Azure RTOS client NetX Duo SNTP (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **grassetto** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_sntp_client_create**: *Creare il client SNTP*
- **nx_sntp_client_delete**: *Eliminare il client SNTP*
- **nx_sntp_client_get_local_time:** Ottenere *l'ora locale del client SNTP*
- **nx_sntp_client_get_local_time_extended:** Ottenere *l'ora locale del client SNTP*
- **nx_sntp_client_initialize_broadcast:** *Inizializzare il client per l'operazione di trasmissione IPv4*
- **nxd_sntp_client_initialize_broadcast:** *Inizializzare il client per l'operazione di trasmissione IPv6 o IPv4*
- **nx_sntp_client_initialize_unicast:** *Inizializzare il client per l'operazione unicast IPv4*
- **nxd_sntp_client_initialize_unicast:** *Inizializzare il client per l'operazione unicast IPv4 o IPv6*
- **nx_sntp_client_receiving_udpates:** Il *client sta attualmente ricevendo aggiornamenti SNTP validi*
- **nx_sntp_client_request_unicast_time**: *Inviare una richiesta unicast direttamente al server NTP*
- **nx_sntp_client_run_broadcast**: *Eseguire il client in modalità di trasmissione*
- **nx_sntp_client_run_unicast**: *Eseguire il client in modalità unicast*
- **nx_sntp_client_set_local_time:** impostare *l'ora locale iniziale del client SNTP*
- **nx_sntp_client_set_time_update_notify**: *Impostare il callback di aggiornamento SNTP*
- **nx_sntp_client_stop**: *Arrestare il thread del client SNTP*
- **nx_sntp_client_utility_display_date_and_time:** visualizza *l'ora NTP in secondi*
- **nx_sntp_client_utility_msecs_to_fraction**: *converte i millisecondi in un componente frazione NTP*
- **nx_sntp_client_utility_usecs_to_fraction:** Convertire *microsecondi in un componente frazione NTP*
- **nx_sntp_client_utility_fraction_to_usecs**: *Converte un componente frazione NTP in microsecondi*


## <a name="nx_sntp_client_create"></a>nx_sntp_client_create

Creare un client SNTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_create(NX_SNTP_CLIENT *client_ptr, NX_IP *ip_ptr,  
                                     UINT iface_index, 
                                     NX_PACKET_POOL *packet_pool_ptr, 
UINT (*leap_second_handler)(NX_SNTP_CLIENT *client_ptr, 
                                        UINT indicator), 
UINT (*kiss_of_death_handler)(NX_SNTP_CLIENT *client_ptr, 
                               NX_SNTP_TIME_MESSAGE *server_time_msg),
VOID (random_number_generator)(struct NX_SNTP_CLIENT_STRUCT 
                                *client_ptr, ULONG *rand));

```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client SNTP.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **ip_ptr** Puntatore all'istanza IP del client

- **iface_index** Indice nell'interfaccia di rete SNTP

- **packet_pool_ptr** Puntatore al pool di pacchetti client

- **leap_second_handler** Callback per la risposta dell'applicazione al secondo intercalare imminente

- **kiss_of_death_handler** Callback per la risposta dell'applicazione alla ricezione del pacchetto di morte

- **random_number_generator** Callback al servizio generatore di numeri casuali

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione client riuscita

- **NX_SNTP_INSUFFICIENT_PACKET_PAYLOAD** (0xD2A) Input non puntatore non valido

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_INVALID_INTERFACE (0x4C) Interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Create the SNTP Client on the primary interface. */
UINT iface_index = 0;
status =  nx_sntp_client_create(&demo_client, 
                     iface_index, &client_ip, 
&client_packet_pool, leap_second_handler, 
                    kiss_of_death_handler, 
NULL /* no random_number_generator callback */);

/* If status is NX_SUCCESS an SNTP Client instance was successfully
   created.  */

```

## <a name="nx_sntp_client_delete"></a>nx_sntp_client_delete

Eliminare un client SNTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_delete(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del client SNTP.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione client riuscita

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete the SNTP Client. */
status =  nx_sntp_client_delete(&demo_client);

/* If status is NX_SUCCESS an SNTP Client 
   instance was successfully deleted.  */

```

## <a name="nx_sntp_client_get_local_time"></a>nx_sntp_client_get_local_time

Ottenere l'ora locale del client SNTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_get_local_time(NX_SNTP_CLIENT *client_ptr , 
                                                ULONG *seconds, 
                                                ULONG *fraction, 
                                                CHAR *buffer);

```

### <a name="description"></a>Descrizione

Questo servizio ottiene l'ora locale del client SNTP con un'opzione di input del puntatore del buffer per ricevere i dati in formato di messaggio stringa.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione *nx_sntp_client_get_local_time_extended*().

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **seconds** Puntatore ai secondi dell'ora locale

- **fraction** Componente frazione dell'ora locale

- **buffer** Puntatore al buffer per scrivere i dati di ora

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione client riuscita

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Get the SNTP Client local time without the 
   string message option. */

ULONG base_seconds;
ULONG base_fraction;

status =  nx_sntp_client_get_local_time(&demo_client, 
                                       &base_seconds, 
                                       &base_fraction, 
                                       NX_NULL);
/* If status is NX_SUCCESS an SNTP Client time was successfully
   retrieved.  */

```

## <a name="nx_sntp_client_get_local_time_extended"></a>nx_sntp_client_get_local_time_extended

Ottenere l'ora locale del client SNTP esteso

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_get_local_time_extended(
                 NX_SNTP_CLIENT *client_ptr,
                 ULONG *seconds, 
                 ULONG *fraction, 
                 CHAR *buffer
                 UINT buffer_size);

```

### <a name="description"></a>Descrizione

Questo servizio ottiene l'ora locale del client SNTP esteso con un'opzione di input del puntatore del buffer per ricevere i dati in formato di messaggio stringa.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **seconds** Puntatore ai secondi dell'ora locale

- **fraction** Puntatore al componente frazione

- **buffer** Puntatore al buffer per scrivere i dati di ora

- **buffer_size** Lunghezza del buffer

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione client riuscita

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido

- NX_SIZE_ERROR (0x09) Controllare buffer_size esito negativo

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Get the SNTP Client local time without the 
   string message option. */

#define BUFSIZE 50

ULONG seconds;
ULONG fraction;
CHAR  buffer[BUFSIZE];

status =  nx_sntp_client_get_local_time_extended(&demo_client, 
                                                &seconds, 
                                                &fraction, 
                                                buffer, 
                                                BUFSIZE);

/* If status is NX_SUCCESS an SNTP Client 
   time was successfully retrieved.  */

```

## <a name="nx_sntp_client_initialize_broadcast"></a>nx_sntp_client_initialize_broadcast

Inizializzare il client per l'operazione di trasmissione

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                                    ULONG multicast_server_address, 
                                    ULONG broadcast_time_servers);


```

### <a name="description"></a>Descrizione

Questo servizio inizializza il client per l'operazione di trasmissione impostando l'indirizzo IP del server SNTP e inizializzando i parametri e i timeout di avvio SNTP. Se gli indirizzi multicast e broadcast sono diversi da Null, viene selezionato l'indirizzo multicast. Se entrambi gli indirizzi sono Null, viene restituito un errore. Si noti che supporta solo indirizzi server IPv4.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **multicast_server_address** Indirizzo multicast SNTP

- **broadcast_time_server** Indirizzo di trasmissione del server SNTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione client riuscita

- **NX_INVALID_PARAMETERS** (0x4D) Input non puntatore non valido

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Initialize the client for broadcast operation.  */
status =  nx_sntp_client_initialize_broadcast(client_ptr,0x0,
                            NX_NULL, IP_ADDRESS(192,2,2,255);

/* If status is NX_SUCCESS the Client 
   was successfully initialized.  */

```

## <a name="nxd_sntp_client_initialize_broadcast"></a>nxd_sntp_client_initialize_broadcast

Inizializzare il client per l'operazione di trasmissione IPv4 o IPv6

### <a name="prototype"></a>Prototipo

```C
UINT nxd_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                            NXD_ADDRESS *multicast_server_address, 
                            NXD_ADDRESS *broadcast_server_address);

```

### <a name="description"></a>Descrizione

Questo servizio inizializza il client per l'operazione di trasmissione configurando l'indirizzo IP del server SNTP e inizializzando i parametri e i timeout di avvio SNTP. Se sia i puntatori di indirizzo broadcast che multicast sono non Null, viene selezionato l'indirizzo multicast. Se entrambi i puntatori di indirizzo sono Null, viene restituito un errore. Supporta entrambi i tipi di indirizzo IPv4 e IPv6. Si noti che IPv6 non supporta la trasmissione, quindi il puntatore dell'indirizzo broadcast è impostato su IPv6, viene restituito un errore.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **multicast_server_address** Indirizzo multicast del server SNTP

- **broadcast_server_address** Indirizzo di trasmissione del server SNTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client (0x00) correttamente inizializzato

- NX_SNTP_PARAM_ERROR (0xD0D) Input non puntatore non valido

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido


### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Initialize the client for broadcast operation.  */
NXD_ADDRESS broadcast_server;

Broadcast_server.nxd_ip_address = NX_IP_VERSION_V6;
Broadcast_server.nxd_ip_address.v6[0] = 0x20010db1;
Broadcast_server.nxd_ip_address.v6[1] = 0x0f101;
Broadcast_server.nxd_ip_address.v6[2] = 0x0;
Broadcast_server.nxd_ip_address.v6[3] = 0x101;

status =  nxd_sntp_client_initialize_broadcast(client_ptr,0x0,
                                  NX_NULL, &broadcast_server)


/* If status is NX_SUCCESS the Client 
   was successfully initialized.  */

```

## <a name="nx_sntp_client_initialize_unicast"></a>nx_sntp_client_initialize_unicast

Configurare il client SNTP per l'esecuzione in unicast

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                        ULONG unicast_time_server);

```
### <a name="description"></a>Descrizione

Questo servizio inizializza il client per l'operazione unicast impostando l'indirizzo IP del server SNTP e inizializzando i parametri e i timeout di avvio SNTP. Si noti che supporta solo indirizzi server IPv4.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **unicast_time_server** Indirizzo IP del server SNTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client (0x00) correttamente inizializzato

- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Initialize the Client for unicast operation.  */
status =  nx_sntp_client_initialize_unicast(&client_ptr, 
                                 IP_ADDRESS(192,2,2,1));


/* If status is NX_SUCCESS the Client 
   is initialized for unicast operation.  */

```


## <a name="nxd_sntp_client_initialize_unicast"></a>nxd_sntp_client_initialize_unicast

Configurare il client SNTP per l'esecuzione in unicast IPv4 o IPv6

### <a name="prototype"></a>Prototipo

```C
UINT nxd_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                  NXD_ADDRESS *unicast_time_server);

```

### <a name="description"></a>Descrizione

Questo servizio inizializza il client per l'operazione unicast configurando l'indirizzo IP del server SNTP e inizializzando i parametri e i timeout di avvio SNTP. Supporta entrambi i tipi di indirizzo IPv4 e IPv6.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **unicast_time_server** Indirizzo IP del server SNTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client (0x00) correttamente inizializzato

- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Initialize the Client for unicast operation.  */
NXD_ADDRESS unicast_server;

unicast _server.nxd_ip_address = NX_IP_VERSION_V6;
unicast _server.nxd_ip_address.v6[0] = 0x20010db1;
unicast _server.nxd_ip_address.v6[1] = 0x0f101;
unicast _server.nxd_ip_address.v6[2] = 0x0;
unicast _server.nxd_ip_address.v6[3] = 0x101;

status =  nxd_sntp_client_initialize_unicast(&client_ptr, 
                                        *unicast_server); 


/* If status is NX_SUCCESS the Client 
   is initialized for unicast operation.  */

```

## <a name="nx_sntp_client_receiving_updates"></a>nx_sntp_client_receiving_updates

Indicare se il client riceve aggiornamenti validi

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_receiving_updates(NX_SNTP_CLIENT *client_ptr, 
                                           UINT *receive_status);

```

### <a name="description"></a>Descrizione

Questo servizio indica se il client riceve aggiornamenti SNTP validi. Se viene superato il periodo di tempo massimo senza un aggiornamento valido o un limite per gli aggiornamenti consecutivi non validi, lo stato di ricezione viene restituito come false. Si noti che il client SNTP è ancora in esecuzione e, se l'applicazione desidera riavviare il client SNTP con un altro server unicast o broadcast/multicast, è necessario arrestare il client SNTP usando il *servizio nx_sntp_client_stop,* reinizializzare il client usando uno dei servizi di inizializzazione con un altro server.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP.

- **receive_status** Puntatore all'indicatore che indica se il client sta ricevendo aggiornamenti validi.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client (0x00) ha ricevuto correttamente lo stato di aggiornamento

- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Determine if the SNTP Client is receiving valid udpates.  */
UINT receive_status;

status =  nx_sntp_client_receiving_updates(client_ptr, 
                                     &receive_status);

/* If status is NX_SUCCESS and receive_status is NX_TRUE, 
   the client is currently receiving valid updates.  */

```

## <a name="nx_sntp_client_request_unicast_time"></a>nx_sntp_client_request_unicast_time

Inviare una richiesta unicast direttamente al server NTP


### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_request_unicast_time(NX_SNTP_CLIENT *client_ptr, 
                                                  UINT wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio consente all'applicazione di inviare direttamente una richiesta unicast al server NTP in modo asincrono dall'attività thread client SNTP. L'opzione wait specifica il tempo di attesa di una risposta. In caso di esito positivo, l'applicazione può usare altri servizi client SNTP per ottenere l'ora più recente. Per altri dettagli, vedere la sezione Richieste **unicast asincrone SNTP.**

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP.

- **Wait_option** Opzione wait per la risposta NTP nei tick del timer.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** client (0x00) invia e riceve l'aggiornamento unicast

- **NX_SNTP_CLIENT_NOT_STARTED** thread client (0xD0B) non avviato

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Determine if the SNTP Client is receiving valid udpates.  */
UINT receive_status;

status =  nx_sntp_client_request_unicast_time(client_ptr, 400);

/* If status is NX_SUCCESS and receive_status is NX_TRUE, 
   the client is received a valid response to the unicast request.  */

```

## <a name="nx_sntp_client_run_broadcast"></a>nx_sntp_client_run_broadcast

Eseguire il client in modalità di trasmissione

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_run_broadcast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia il client in modalità di trasmissione in cui attenderà di ricevere le trasmissioni dal server SNTP. Se viene ricevuto un messaggio SNTP di trasmissione valido, viene reimpostato il timeout del client SNTP per la scadenza massima senza un aggiornamento e il numero di messaggi consecutivi non validi ricevuti. Se viene superato uno di questi limiti, il client SNTP imposta lo stato del server su non valido, anche se attenderà comunque di ricevere gli aggiornamenti. L'applicazione può eseguire il polling dell'attività client SNTP per verificare lo stato del server e, se non è valida, arrestare il client SNTP e reinizializzare l'attività con un altro indirizzo di trasmissione SNTP. Può anche passare a un server SNTP unicast.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP.

### <a name="return-values"></a>Valori restituiti

- **stato --------** stato di completamento effettivo

- **NX_SNTP_CLIENT_ALREADY_STARTED** client (0xD0C) già avviato

- **NX_SNTP_CLIENT_NOT_INITIALIZED** client (0xD01) non inizializzato

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start Client running in broadcast mode.  */
status =  nx_sntp_client_run_broadcast(client_ptr);

/* If status is NX_SUCCESS, the client is successfully started.  */

```

## <a name="nx_sntp_client_run_unicast"></a>nx_sntp_client_run_unicast

Eseguire il client in modalità unicast

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_run_unicast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia il client in modalità unicast in cui invia periodicamente una richiesta unicast al server SNTP per un aggiornamento temporale. Se viene ricevuto un messaggio SNTP valido, il timeout del client SNTP per la scadenza massima senza un aggiornamento, l'intervallo di polling iniziale e il numero di messaggi consecutivi non validi ricevuti vengono reimpostati. Se viene superato uno di questi limiti, il client SNTP imposta lo stato del server su non valido anche se continuerà a eseguire il polling e ad attendere la ricezione degli aggiornamenti. L'applicazione può eseguire il polling dell'attività client SNTP per verificare lo stato del server e, se non è valida, arrestare il client SNTP e reinizializzare l'attività con un altro indirizzo unicast SNTP. Può anche passare a un server SNTP di trasmissione.

.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Client avviato correttamente in modalità unicast

- **NX_SNTP_CLIENT_ALREADY_STARTED** client (0xD0C) già avviato

- **NX_SNTP_CLIENT_NOT_INITIALIZED** client (0xD01) non inizializzato

- NX_PTR_ERROR (0x07) Input del puntatore non valido

- NX_CALLER_ERROR (0x11) Chiamante del servizio non valido


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start the Client in unicast mode. */
status =  nx_sntp_client_run_unicast(client_ptr);

/* If status = NX_SUCCESS, the Client was successfully started.  */

```

## <a name="nx_sntp_client_set_local_time"></a>nx_sntp_client_set_local_time

Impostare l'ora locale del client SNTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_set_local_time(NX_SNTP_CLIENT *client_ptr , 
                                ULONG seconds, ULONG fraction);

```

### <a name="description"></a>Descrizione

Questo servizio imposta l'ora locale del client SNTP con l'ora di input, in formato SNTP, ad esempio secondi e "frazione", ovvero il formato per l'inserimento delle frazioni di secondo in formato esadecimale. È destinato all'aggiornamento dell'ora locale del client SNTP da un'ora indipendente, ad esempio un orologio in tempo reale. Il protocollo SNTP è destinato agli aggiornamenti dell'ora SNTP per evitare che l'ora dell'orologio locale sia "deviata". Gli aggiornamenti dell'ora del server SNTP possono essere, ma non sono destinati a essere l'unico input per l'ora locale del client SNTP se non esiste un'ora indipendente nel dispositivo dell'applicazione.

Questa API può essere usata anche per assegnare al client SNTP un'ora di base prima di avviare il thread del client SNTP. L'ora locale del client SNTP viene confrontata con gli aggiornamenti ricevuti per i dati di ora validi. Per la prima volta che viene ricevuto l'aggiornamento, potrebbe esserci una discrepanza molto grande. È quindi disponibile un'opzione che consente al client SNTP di ignorare la discrepanza al primo aggiornamento. In questo modo, il client SNTP può essere avviato senza un'ora di base. L'ora di input può essere ottenuta da periodi noti (in genere disponibili su Internet) e viene calcolata come numero di secondi a partire dal 1° gennaio 1900 (fino al 2036, quando verrà avviato un nuovo "periodo".

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **seconds** Componente secondi dell'input dell'ora

- **fraction** Componente Subseconds nel formato frazione SNTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente l'ora locale

- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione

### <a name="example"></a>Esempio

```C
/* Set the SNTP Client local time. */
base_seconds =  0xd2c50b71;
base_fraction = 0xa132db1e;

status =  nx_sntp_client_set_local_time(&demo_client, 
                                        base_seconds, 
                                        base_fraction);

/* If status is NX_SUCCESS an SNTP Client time 
   was successfully set.  */

```

## <a name="nx_sntp_client_set_time_update_notify"></a>nx_sntp_client_set_time_update_notify

Impostare il callback di aggiornamento SNTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_set_time_update_notify(NX_SNTP_CLIENT *client_ptr, 
                           VOID (time_update_cb)(NX_SNTP_TIME_MESSAGE 
                        *time_update_ptr, NX_SNTP_TIME *local_time)));

```

### <a name="description"></a>Descrizione

Questo servizio imposta il callback per notificare all'applicazione quando il client SNTP riceve un aggiornamento dell'ora valido. Fornisce il messaggio SNTP effettivo e l'ora locale del client SNTP (in genere la stessa) in formato NTP. L'applicazione può usare direttamente i dati NTP o chiamare *il nx_sntp_client_utility_display_date_time* per convertire l'ora in formato leggibile.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **time_update_cb** Puntatore alla funzione di callback

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Callback impostato correttamente

- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione

### <a name="example"></a>Esempio

```C
/* Set the SNTP Client time update callback. */
VOID client_time_update_notify(NX_SNTP_TIME_MESSAGE *time_update_ptr, 
                                           NX_SNTP_TIME *local time);

NX_SNTP_CLIENT demo_client;


status = nx_sntp_client_set_time_update_notify(&demo_client, 
                                            time_update_cb);

/* If status is NX_SUCCESS an SNTP Client 
   time update callback was successfully set.  */

```

## <a name="nx_sntp_client_stop"></a>nx_sntp_client_stop

Arrestare il thread del client SNTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_stop(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio arresta il thread del client SNTP. Le attività del thread del client SNTP, eseguite in un ciclo infinito, vengono sospese a ogni iterazione per rilasciare il controllo dello stato del client SNTP e consentire alle applicazioni di effettuare chiamate API sul client SNTP.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Thread client arrestato riuscito

- **NX_SNTP_CLIENT_NOT_STARTED** thread client SNTP (0xDB) non avviato

- NX_PTR_ERROR (0x07) Input del puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Stop the SNTP Client. */
status =  nx_sntp_client_stop(&demo_client);

/* If status is NX_SUCCESS an SNTP 
   Client instance was successfully stopped.  */

```

## <a name="nx_sntp_client_utility_display_date_time"></a>nx_sntp_client_utility_display_date_time

Convertire un'ora NTP in una stringa di data e ora

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_utility_display_date_time (NX_SNTP_CLIENT 
                      *client_ptr, CHAR *buffer, UINT length);

```

### <a name="description"></a>Descrizione

Questo servizio converte l'ora locale del client SNTP nel formato di data del mese dell'anno e restituisce la data nel buffer fornito. Il NX_SNTP_CURRENT_YEAR non deve essere lo stesso anno dell'ora corrente del client, ma deve essere definito.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr puntatore al client SNTP**

- **buffer** Puntatore al buffer per archiviare la data

- **length** Dimensioni del buffer di input

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Conversione riuscita

- **NX_SNTP_ERROR_CONVERTING_DATETIME** (0xD08) NX_SNTP_CURRENT_YEAR definito o non è stata stabilita alcuna ora del client locale

- **NX_SNTP_INVALID_DATETIME_BUFFER** (0xD07) Lunghezza del buffer insufficiente


### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Convert and display the Client’s local time. */

status =  nx_sntp_client_utility_display_date_time(client_ptr , 
                                        buffer, sizeof(buffer));

/* If status is NX_SUCCESS, 
   date was successfully written to buffer.  */

```

## <a name="nx_sntp_client_utility_msecs_to_fraction"></a>nx_sntp_client_utility_msecs_to_fraction

Convertire i millisecondi in un componente frazione NTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_utility_msecs_to_fraction (ULONG milliseconds,   
                                                 ULONG *fraction);

```

### <a name="description"></a>Descrizione

Questo servizio converte i millisecondi di input nel componente frazione NTP. È destinato all'uso con applicazioni che hanno un'ora di base iniziale per il client SNTP ma non nel formato NTP secondi/frazioni. Il numero di millisecondi deve essere minore di 1000 per rendere una frazione valida.

### <a name="input-parameters"></a>Parametri di input

- **millisecondi millisecondi da convertire**

- **fraction** Puntatore ai millisecondi convertiti in frazioni

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Conversione riuscita

- **NX_SNTP_OVERFLOW_ERROR** (0xD32) Errore durante la conversione dell'ora in una data

- NX_SNTP_INVALID_TIME (0xD30) Input di dati SNTP non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Convert the milliseconds to a fraction. */


status =  nx_sntp_client_utility_msecs_to_fraction(milliseconds, 
                                                     &fraction);

/* If status is NX_SUCCESS, 
   data was successfully converted.  */

```

## <a name="nx_sntp_client_utility_usecs_to_fraction"></a>nx_sntp_client_utility_usecs_to_fraction

Convertire microsecondi in un componente frazione NTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_utility_usecs_to_fraction (ULONG microseconds,   
                                                 ULONG *fraction);

```
### <a name="description"></a>Descrizione

Questo servizio converte i microsecondi di input nel componente frazione NTP. È destinato all'uso con applicazioni che hanno un'ora di base iniziale per il client SNTP ma non nel formato NTP secondi/frazioni. Il numero di microsecondi deve essere minore di 1000000 per rendere una frazione valida.

### <a name="input-parameters"></a>Parametri di input

- **microsecondi** Microsecondi da convertire

- **fraction** Puntatore a microsecondi convertiti in frazioni

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Conversione riuscita

- **NX_SNTP_OVERFLOW_ERROR** (0xD32) Errore durante la conversione dell'ora in una data

- NX_SNTP_INVALID_TIME (0xD30) Input di dati SNTP non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Convert the microseconds to a fraction. */


status =  nx_sntp_client_utility_msecs_to_fraction(microseconds, 
                                                     &fraction);

/* If status is NX_SUCCESS, data was successfully converted.  */

```

## <a name="nx_sntp_client_utility_fraction_to_usecs"></a>nx_sntp_client_utility_fraction_to_usecs

Convertire un componente frazione NTP in microsecondi

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_utility_fraction_to_usecs (ULONG fraction,   
                                         ULONG *microseconds);

```

### <a name="description"></a>Descrizione

Questo servizio converte il componente frazione NTP di input in microsecondi.

### <a name="input-parameters"></a>Parametri di input

- **frazione frazione da convertire**

- **microsecondi** Puntatore alla frazione convertita in microsecondi

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Conversione riuscita

- NX_SNTP_INVALID_TIME (0xD30) Input di dati SNTP non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Convert the fraction to microseconds. */


status =  nx_sntp_client_utility_fraction_to_msecs(fraction, 
                                             &microseconds);

/* If status is NX_SUCCESS, data was successfully converted.  */
```