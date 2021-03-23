---
title: Capitolo 3-Descrizione dei servizi client di Azure RTO NetX Duo SNTP
description: Questo capitolo contiene una descrizione di tutti i servizi client NetX Duo SNTP (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 75b2b878cd084ca1c1cdd1eed4333d303fe32ad6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821650"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-sntp-client-services"></a>Capitolo 3-Descrizione dei servizi client di Azure RTO NetX Duo SNTP

Questo capitolo contiene una descrizione di tutti i servizi client di Azure RTO NetX Duo SNTP (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_sntp_client_create**: *creare il client SNTP*
- **nx_sntp_client_delete**: *eliminare il client SNTP*
- **nx_sntp_client_get_local_time**: *ottenere l'ora locale del client SNTP*
- **nx_sntp_client_get_local_time_extended**: *ottenere l'ora locale del client SNTP*
- **nx_sntp_client_initialize_broadcast**: *inizializzare il client per l'operazione di broadcast IPv4*
- **nxd_sntp_client_initialize_broadcast**: *inizializzare il client per l'operazione di broadcast IPv6 o IPv4*
- **nx_sntp_client_initialize_unicast**: *inizializzare il client per l'operazione unicast IPv4*
- **nxd_sntp_client_initialize_unicast**: *inizializzare il client per l'operazione unicast IPv4 o IPv6*
- **nx_sntp_client_receiving_udpates**: il *client sta attualmente ricevendo aggiornamenti SNTP validi*
- **nx_sntp_client_request_unicast_time**: *inviare una richiesta unicast direttamente al server NTP*
- **nx_sntp_client_run_broadcast**: *eseguire il client in modalità broadcast*
- **nx_sntp_client_run_unicast**: *eseguire il client in modalità unicast*
- **nx_sntp_client_set_local_time**: *impostare l'ora locale iniziale del client SNTP*
- **nx_sntp_client_set_time_update_notify**: *impostare il callback di aggiornamento SNTP*
- **nx_sntp_client_stop**: *arrestare il thread del client SNTP*
- **nx_sntp_client_utility_display_date_and_time**: *Visualizza tempo NTP in secondi*
- **nx_sntp_client_utility_msecs_to_fraction**: *convertire i millisecondi in un componente della frazione NTP*
- **nx_sntp_client_utility_usecs_to_fraction**: *convertire i microsecondi in un componente della frazione NTP*
- **nx_sntp_client_utility_fraction_to_usecs**: *conversione di un componente della frazione NTP in microsecondi*


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

- **ip_ptr** Puntatore a istanza IP client

- **iface_index** Indice per l'interfaccia di rete SNTP

- **packet_pool_ptr** Puntatore al pool di pacchetti client

- **leap_second_handler** Callback per la risposta dell'applicazione al secondo intercalare imminente

- **kiss_of_death_handler** Callback per la risposta dell'applicazione a ricevere il bacio del pacchetto di morte

- **random_number_generator** Callback a servizio Generatore di numeri casuali

### <a name="return-values"></a>Valori restituiti

- Creazione client riuscita **NX_SUCCESS** (0x00)

- **NX_SNTP_INSUFFICIENT_PACKET_PAYLOAD** (0xD2A) non è stato inserito alcun puntatore non valido

- NX_PTR_ERROR (0x07) input puntatore non valido

- L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida

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

Questo servizio Elimina un'istanza del client SNTP.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

### <a name="return-values"></a>Valori restituiti

- Creazione client riuscita **NX_SUCCESS** (0x00)

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido

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

Questo servizio ottiene l'ora locale del client SNTP con un input del puntatore del buffer dell'opzione per ricevere i dati nel formato del messaggio stringa.

questo servizio è deprecato. Gli sviluppatori sono invitati a eseguire la migrazione a *nx_sntp_client_get_local_time_extended*().

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **secondi** Puntatore ai secondi dell'ora locale

- **frazione** di Componente frazione ora locale

- **buffer** Puntatore al buffer per scrivere i dati relativi all'ora

### <a name="return-values"></a>Valori restituiti

- Creazione client riuscita **NX_SUCCESS** (0x00)

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido

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

Questo servizio ottiene l'ora locale del client SNTP esteso con un input del puntatore del buffer dell'opzione per ricevere i dati nel formato del messaggio stringa.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **secondi** Puntatore ai secondi dell'ora locale

- **frazione** di Puntatore a componente frazione

- **buffer** Puntatore al buffer per scrivere i dati relativi all'ora

- **BUFFER_SIZE** Lunghezza del buffer

### <a name="return-values"></a>Valori restituiti

- Creazione client riuscita **NX_SUCCESS** (0x00)

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido

- Controllo NX_SIZE_ERROR (0x09) buffer_size esito negativo

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

Inizializzare il client per l'operazione di broadcast

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                                    ULONG multicast_server_address, 
                                    ULONG broadcast_time_servers);


```

### <a name="description"></a>Descrizione

Questo servizio Inizializza il client per l'operazione di broadcast impostando l'indirizzo IP del server SNTP e inizializzando i parametri di avvio e i timeout di SNTP. Se gli indirizzi multicast e broadcast sono diversi da null, viene selezionato l'indirizzo multicast. Se entrambi gli indirizzi sono null, viene restituito un errore. Si noti che questo supporta solo indirizzi server IPv4.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **multicast_server_address** Indirizzo multicast di SNTP

- **broadcast_time_server** Indirizzo di broadcast del server SNTP

### <a name="return-values"></a>Valori restituiti

- Creazione client riuscita **NX_SUCCESS** (0x00)

- **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido

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

Questo servizio Inizializza il client per l'operazione di broadcast impostando l'indirizzo IP del server SNTP e inizializzando i parametri di avvio e i timeout di SNTP. Se i puntatori di trasmissione e di indirizzo multicast sono diversi da null, viene selezionato l'indirizzo multicast. Se entrambi i puntatori di indirizzo sono null, viene restituito un errore. Sono supportati i tipi di indirizzi sia IPv4 che IPv6. Si noti che IPv6 non supporta la trasmissione, quindi il puntatore all'indirizzo di trasmissione è impostato su IPv6, viene restituito un errore.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **multicast_server_address** Indirizzo multicast del server SNTP

- **broadcast_server_address** Indirizzo di broadcast del server SNTP

### <a name="return-values"></a>Valori restituiti

- Inizializzazione del client **NX_SUCCESS** (0x00) completata

- NX_SNTP_PARAM_ERROR (0xD0D) non è stato inserito alcun puntatore non valido

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido


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

Configurare il client di SNTP per l'esecuzione in unicast

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                        ULONG unicast_time_server);

```
### <a name="description"></a>Descrizione

Questo servizio Inizializza il client per l'operazione unicast impostando l'indirizzo IP del server SNTP e inizializzando i parametri di avvio e i timeout di SNTP. Si noti che questo supporta solo indirizzi server IPv4.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **unicast_time_server** Indirizzo IP del server SNTP

### <a name="return-values"></a>Valori restituiti

- Inizializzazione del client **NX_SUCCESS** (0x00) completata

- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido

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

Configurare il client di SNTP per l'esecuzione in unicast IPv4 o IPv6

### <a name="prototype"></a>Prototipo

```C
UINT nxd_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                  NXD_ADDRESS *unicast_time_server);

```

### <a name="description"></a>Descrizione

Questo servizio Inizializza il client per l'operazione unicast impostando l'indirizzo IP del server SNTP e inizializzando i parametri di avvio e i timeout di SNTP. Sono supportati i tipi di indirizzi sia IPv4 che IPv6.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **unicast_time_server** Indirizzo IP del server SNTP

### <a name="return-values"></a>Valori restituiti

- Inizializzazione del client **NX_SUCCESS** (0x00) completata

- NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido

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

Indica se il client riceve aggiornamenti validi

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_receiving_updates(NX_SNTP_CLIENT *client_ptr, 
                                           UINT *receive_status);

```

### <a name="description"></a>Descrizione

Questo servizio indica se il client riceve aggiornamenti SNTP validi. Se viene superato il lasso di tempo massimo senza un aggiornamento o un limite valido per gli aggiornamenti consecutivi non validi, lo stato di ricezione viene restituito come false. Si noti che il client SNTP è ancora in esecuzione e, se l'applicazione vuole riavviare il client di SNTP con un altro server unicast o broadcast/multicast, deve arrestare il client SNTP usando il servizio *nx_sntp_client_stop* , reinizializzare il client usando uno dei servizi di inizializzazione con un altro server.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP.

- **receive_status** Puntatore a indicatore se il client riceve aggiornamenti validi.

### <a name="return-values"></a>Valori restituiti

- Il client **NX_SUCCESS** (0x00) ha ricevuto correttamente lo stato di aggiornamento

- NX_PTR_ERROR (0x07) input puntatore non valido

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

Questo servizio consente all'applicazione di inviare direttamente una richiesta unicast al server NTP in modo asincrono dall'attività thread del client SNTP. L'opzione wait specifica il tempo di attesa di una risposta. In caso di esito positivo, l'applicazione può usare altri servizi client di SNTP per ottenere l'ora più recente. Per altri dettagli, vedere la sezione relativa alle **richieste unicast asincrone di SNTP** .

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP.

- **Wait_option** Opzione wait per la risposta NTP nei cicli del timer.

### <a name="return-values"></a>Valori restituiti

- Il client **NX_SUCCESS** (0x00) Invia e riceve correttamente l'aggiornamento unicast

- Thread client di **NX_SNTP_CLIENT_NOT_STARTED** (0xD0B) non avviato

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido

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

Eseguire il client in modalità broadcast

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_run_broadcast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio avvia il client in modalità broadcast in cui attenderà la ricezione delle trasmissioni dal server SNTP. Se viene ricevuto un messaggio SNTP broadcast valido, viene reimpostato il timeout del client SNTP per la scadenza massima senza aggiornamento e il numero di messaggi non validi consecutivi ricevuti. Se viene superato uno di questi limiti, il client di SNTP imposta lo stato del server su non valido anche se continuerà ad attendere la ricezione degli aggiornamenti. L'applicazione può eseguire il polling dell'attività client SNTP per lo stato del server e, se non è valido, arrestare il client SNTP e reinizializzarlo con un altro indirizzo di broadcast SNTP. Può anche passare a un server SNTP unicast.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP.

### <a name="return-values"></a>Valori restituiti

- **stato** --------stato di completamento effettivo

- Client **NX_SNTP_CLIENT_ALREADY_STARTED** (0xD0C) già avviato

- Client **NX_SNTP_CLIENT_NOT_INITIALIZED** (0xD01) non inizializzato

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido

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

Questo servizio avvia il client in modalità unicast, in cui invia periodicamente una richiesta unicast al server SNTP per un aggiornamento del tempo. Se viene ricevuto un messaggio SNTP valido, viene reimpostato il timeout del client SNTP per la scadenza massima senza aggiornamento, l'intervallo di polling iniziale e il numero di messaggi non validi consecutivi ricevuti. Se viene superato uno di questi limiti, il client SNTP imposta lo stato del server su non valido anche se eseguirà comunque il polling e attenda la ricezione degli aggiornamenti. L'applicazione può eseguire il polling dell'attività client SNTP per lo stato del server e, se non è valido, arrestare il client SNTP e reinizializzarlo con un altro indirizzo unicast SNTP. Può anche passare a un server SNTP broadcast.

.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha avviato correttamente il client in modalità unicast

- Client **NX_SNTP_CLIENT_ALREADY_STARTED** (0xD0C) già avviato

- Client **NX_SNTP_CLIENT_NOT_INITIALIZED** (0xD01) non inizializzato

- NX_PTR_ERROR (0x07) input puntatore non valido

- NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start the Client in unicast mode. */
status =  nx_sntp_client_run_unicast(client_ptr);

/* If status = NX_SUCCESS, the Client was successfully started.  */

```

## <a name="nx_sntp_client_set_local_time"></a>nx_sntp_client_set_local_time

Imposta l'ora locale del client SNTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_set_local_time(NX_SNTP_CLIENT *client_ptr , 
                                ULONG seconds, ULONG fraction);

```

### <a name="description"></a>Descrizione

Questo servizio imposta l'ora locale del client SNTP con l'ora di input, in formato SNTP, ad esempio secondi e "frazione", che rappresenta il formato per l'inserimento di frazioni di secondo in formato esadecimale. È progettato per l'aggiornamento dell'ora locale del client SNTP da un custode del tempo indipendente, ad esempio un clock in tempo reale. Il protocollo SNTP è concepito per gli aggiornamenti del tempo di SNTP per il tempo di clock locale da "Drifting". Gli aggiornamenti temporali del server SNTP possono essere, ma non sono intesi come input esclusivo per l'ora locale del client SNTP se non è presente alcun detentore del tempo indipendente nel dispositivo applicativo.

Questa API può essere usata anche per concedere al client SNTP un'ora di base prima di avviare il thread del client SNTP. L'ora locale del client SNTP viene confrontata con gli aggiornamenti ricevuti per i dati temporali validi. Per il primo aggiornamento ricevuto, potrebbe essere presente una discrepanza molto grande. È pertanto possibile che il client SNTP ignori la discrepanza al primo aggiornamento. In questo modo, il client SNTP può avviarsi senza un'ora di base. È possibile ottenere tempo di input da epoche note (in genere disponibili su Internet) e calcolate come numero di secondi a partire dal 1 ° gennaio 1900 (fino a 2036 quando viene avviato un nuovo ' Epoch '.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **secondi** Componente relativo ai secondi dell'input temporale

- **frazione** di Componente dei subsecondi nel formato della frazione SNTP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha impostato correttamente l'ora locale

- NX_PTR_ERROR (0x07) input puntatore non valido

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

Imposta callback di aggiornamento SNTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_set_time_update_notify(NX_SNTP_CLIENT *client_ptr, 
                           VOID (time_update_cb)(NX_SNTP_TIME_MESSAGE 
                        *time_update_ptr, NX_SNTP_TIME *local_time)));

```

### <a name="description"></a>Descrizione

Questo servizio imposta callback per notificare all'applicazione quando il client di SNTP riceve un aggiornamento temporale valido. Fornisce il messaggio SNTP effettivo e l'ora locale del client SNTP (in genere lo stesso) in formato NTP. L'applicazione può usare direttamente i dati NTP o chiamare il *servizio nx_sntp_client_utility_display_date_time* per convertire l'ora in formato leggibile.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

- **time_update_cb** Puntatore alla funzione di callback

### <a name="return-values"></a>Valori restituiti

- Il callback **NX_SUCCESS** (0x00) è stato impostato correttamente

- NX_PTR_ERROR (0x07) input puntatore non valido

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

Questo servizio arresta il thread del client SNTP. Le attività dei thread del client SNTP, che vengono eseguite in un ciclo infinito, vengono sospese in ogni iterazione per rilasciare il controllo dello stato del client SNTP e consentono alle applicazioni di effettuare chiamate API sul client SNTP.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr** Puntatore al blocco di controllo client SNTP

### <a name="return-values"></a>Valori restituiti

- Thread client arrestato **NX_SUCCESS** (0x00) riuscito

- **NX_SNTP_CLIENT_NOT_STARTED** (0XDB) SNTP thread del client non avviato

- NX_PTR_ERROR (0x07) input puntatore non valido

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

Converte una stringa di data e ora NTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_utility_display_date_time (NX_SNTP_CLIENT 
                      *client_ptr, CHAR *buffer, UINT length);

```

### <a name="description"></a>Descrizione

Questo servizio converte l'ora locale del client SNTP in un formato di data anno mese e restituisce la data nel buffer fornito. Il NX_SNTP_CURRENT_YEAR deve essere diverso da quello dell'ora del client corrente, ma deve essere definito.

### <a name="input-parameters"></a>Parametri di input

- **Puntatore client_ptr al client SNTP**

- **buffer** Puntatore al buffer per archiviare la data

- **lunghezza** Dimensioni del buffer di input

### <a name="return-values"></a>Valori restituiti

- Conversione **NX_SUCCESS** (0x00) riuscita

- Il **NX_SNTP_ERROR_CONVERTING_DATETIME** (0xD08) non NX_SNTP_CURRENT_YEAR definito o non è stato stabilito alcun tempo client locale

- Lunghezza del buffer insufficiente **NX_SNTP_INVALID_DATETIME_BUFFER** (0xD07)


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

Convertire i millisecondi in un componente della frazione NTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_utility_msecs_to_fraction (ULONG milliseconds,   
                                                 ULONG *fraction);

```

### <a name="description"></a>Descrizione

Questo servizio converte i millisecondi di input nel componente della frazione NTP. È progettato per l'uso con applicazioni che hanno un'ora di base iniziale per il client SNTP, ma non in formato NTP secondi/frazione. Il numero di millisecondi deve essere minore di 1000 per creare una frazione valida.

### <a name="input-parameters"></a>Parametri di input

- **millisecondi per la conversione**

- **frazione** di Puntatore a millisecondi convertiti in frazione

### <a name="return-values"></a>Valori restituiti

- Conversione **NX_SUCCESS** (0x00) riuscita

- Errore di **NX_SNTP_OVERFLOW_ERROR** (0XD32) durante la conversione del tempo in una data

- Input di dati di SNTP NX_SNTP_INVALID_TIME (0xD30) non valido

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

Converte i microsecondi in un componente della frazione NTP

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_utility_usecs_to_fraction (ULONG microseconds,   
                                                 ULONG *fraction);

```
### <a name="description"></a>Descrizione

Questo servizio converte i microsecondi di input nel componente della frazione NTP. È progettato per l'uso con applicazioni che hanno un'ora di base iniziale per il client SNTP, ma non in formato NTP secondi/frazione. Il numero di microsecondi deve essere inferiore a 1 milione per creare una frazione valida.

### <a name="input-parameters"></a>Parametri di input

- **microsecondi** Microsecondi da convertire

- **frazione** di Puntatore a microsecondi convertito in frazione

### <a name="return-values"></a>Valori restituiti

- Conversione **NX_SUCCESS** (0x00) riuscita

- Errore di **NX_SNTP_OVERFLOW_ERROR** (0XD32) durante la conversione del tempo in una data

- Input di dati di SNTP NX_SNTP_INVALID_TIME (0xD30) non valido

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

Converte un componente della frazione NTP in microsecondi

### <a name="prototype"></a>Prototipo

```C
UINT nx_sntp_client_utility_fraction_to_usecs (ULONG fraction,   
                                         ULONG *microseconds);

```

### <a name="description"></a>Descrizione

Questo servizio converte il componente della frazione NTP di input in microsecondi.

### <a name="input-parameters"></a>Parametri di input

- **frazione frazione da convertire**

- **microsecondi** Puntatore alla frazione convertita in microsecondi

### <a name="return-values"></a>Valori restituiti

- Conversione **NX_SUCCESS** (0x00) riuscita

- Input di dati di SNTP NX_SNTP_INVALID_TIME (0xD30) non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```C
/* Convert the fraction to microseconds. */


status =  nx_sntp_client_utility_fraction_to_msecs(fraction, 
                                             &microseconds);

/* If status is NX_SUCCESS, data was successfully converted.  */
```