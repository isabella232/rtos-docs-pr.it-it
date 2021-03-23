---
title: Capitolo 3-Descrizione dei servizi Telnet di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi Telnet di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 991ec53aaba052b4f42da6e5a541151953121e76
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821617"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-telnet-services"></a>Capitolo 3-Descrizione dei servizi Telnet di Azure RTO NetX Duo

Questo capitolo contiene una descrizione di tutti i servizi Telnet di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_telnet_client_connect**: *connettere un client Telnet con indirizzo IPv4*
- **nxd_telnet_client_connect**: *connettere un client Telnet IPv6 con indirizzo IPv6*
- **nx_telnet_client_create**: *creare un client Telnet*
- **nx_telnet_client_delete**: *eliminare un client Telnet*
- **nx_telnet_client_disconnect**: *disconnettere un client Telnet*
- **nx_telnet_client_packet_receive**: *ricevere il pacchetto tramite il client Telnet*
- **nx_telnet_client_packet_send**: *inviare il pacchetto tramite il client Telnet*
- **nx_telnet_server_create**: *creare un server Telnet*
- **nx_telnet_server_delete**: *eliminare un server Telnet*
- **nx_telnet_server_disconnect**: *disconnettere un client Telnet*
- **nx_telnet_server_get_open_connection_count**: *recuperare il numero di connessioni aperte*
- **nx_telnet_server_packet_send**: *inviare il pacchetto tramite la connessione client*
- **nx_telnet_server_packet_pool_set**: *impostare pool di pacchetti come pool di pacchetti del server Telnet*
- **nx_telnet_server_start**: *avviare un server Telnet*
- **nx_telnet_server_stop**: *arrestare un server Telnet*

## <a name="nx_telnet_client_connect"></a>nx_telnet_client_connect

Connettere un client Telnet con indirizzo IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                              ULONG server_ip, UINT server_port, 
                              ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di connettere l'istanza del client Telnet creata in precedenza al server sull'IP e sulla porta specificati usando un indirizzo IPv4 per il server Telnet. Questo servizio inserisce effettivamente l'indirizzo IP del server ULONG in un blocco di controllo NXD_ADDRESS e imposta la versione IP su 4 prima di chiamare il servizio *nxd_telnet_client_connect* descritto di seguito.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al blocco di controllo client Telnet.
- **server_ip**: indirizzo IPv4 del server Telnet.
- **SERVER_PORT**: porta TCP del server (il server Telnet è la porta 23).
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la connessione del client Telnet. Le opzioni di attesa sono definite come segue:

    - **valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) connessione client riuscita.
- **NX_TELNET_NOT_DISCONNECTED**: (0XF4) client già connesso.
- NX_PTR_ERROR: (0x07) puntatore client non valido.
- NX_IP_ADDRESS_ERROR: (0x21) indirizzo IP non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Connect the Telnet Client instance “my_client” to the Server at 
   IP address 1.2.3.4 and port 23.  */
status =  nx_telnet_client_connect(&my_client, IP_ADDRESS(1,2,3,4), 23, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   connected to the Telnet Server.  */
```

## <a name="nxd_telnet_client_connect"></a>nxd_telnet_client_connect

Connettere un client Telnet con indirizzo IPv6 o IPv4

### <a name="prototype"></a>Prototipo

```c
UINT nxd_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                               NXD_ADDRESS *server_ip_address, 
                               UINT server_port, 
                               ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di connettere l'istanza del client Telnet creata in precedenza al server con l'indirizzo IP e la porta specificati utilizzando l'indirizzo IPv6 del server Telnet. Questo servizio può assumere un indirizzo IPv4 o IPv6, ma deve essere contenuto nella variabile NXD_ADDRESS *server_ip_address.*

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al blocco di controllo client Telnet.
- **server_ip_address**: indirizzo IP del server.
- **SERVER_PORT**: porta TCP del server (il server Telnet è la porta 23).
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la connessione del client Telnet. Le opzioni di attesa sono definite come segue:

    - **valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) connessione client riuscita.
- **NX_TELNET_ERROR**: (0xF0) errore di connessione del client.
- **NX_TELNET_NOT_DISCONNECTED**: (0XF4) client già connesso.
- NX_PTR_ERROR: (0x07) puntatore client non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.
- NX_TELNET_INVALID_PARAMETER: (0xF5) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Connect the Telnet Client instance “my_client” to the Server at 
   IPv6 address 20010db1:0:f101::101 and port 23.  */
status =  nxd_telnet_client_connect(&my_client, &server_ip_address, 23, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   connected to the Telnet Server.  */
```

## <a name="nx_telnet_client_create"></a>nx_telnet_client_create

Creazione di un client Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_client_create(NX_TELNET_CLIENT *client_ptr, 
                             CHAR *client_name, NX_IP *ip_ptr, 
                             ULONG window_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client Telnet.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al blocco di controllo client Telnet.
- **client_name**: nome dell'istanza del client.
- **ip_ptr**: puntatore all'istanza IP.
- **window_size**: dimensioni della finestra di ricezione TCP per il client.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) creazione client riuscita.
- **NX_TELNET_ERROR**: (0xF0) socket crea errore.
- NX_PTR_ERROR: (0x07) il puntatore IP o il client non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create the Telnet Client instance “my_client” on the IP instance “ip_0”.  */
status =  nx_telnet_client_create(&my_client, “My Telnet Client”, &ip_0, 2048);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   created.  */
```
## <a name="nx_telnet_client_delete"></a>nx_telnet_client_delete

Eliminare un client Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_client_delete(NX_TELNET_CLIENT *client_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del client Telnet creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al blocco di controllo client Telnet.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione client riuscita.
- **NX_TELNET_NOT_DISCONNECTED**: (0xF4) il client è ancora connesso.
- NX_PTR_ERROR: (0x07) puntatore client non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_delete(&my_client);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   deleted.  */
```

## <a name="nx_telnet_client_disconnect"></a>nx_telnet_client_disconnect

Disconnettere un client Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_client_disconnect(NX_TELNET_CLIENT *client_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio disconnette un'istanza del client Telnet connessa in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al blocco di controllo client Telnet.
- **WAIT_OPTION**: definisce per quanto tempo il servizio attenderà la disconnessione del client Telnet. Le opzioni di attesa sono definite come segue:

    - **valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la disconnessione del client è riuscita.
- **NX_TELNET_NOT_CONNECTED**: (0XF3) client non connesso.
- NX_PTR_ERROR: (0x07) puntatore client non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.


### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

/* Disconnect the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_disconnect(&my_client, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   disconnected.  */
```

## <a name="nx_telnet_client_packet_receive"></a>nx_telnet_client_packet_receive

Ricevi pacchetto tramite client Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_client_packet_receive(NX_TELNET_CLIENT *client_ptr, 
                                     NX_PACKET **packet_ptr, 
                                     ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio riceve un pacchetto dall'istanza del client Telnet connessa in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al blocco di controllo client Telnet.
- **packet_ptr**: puntatore alla destinazione per il pacchetto ricevuto.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per la ricezione del pacchetto client Telnet. Le opzioni di attesa sono definite come segue:
    - **valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la ricezione di pacchetti client è riuscita.
- NX_PTR_ERROR: (0x07) input puntatore non valido
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

/* Receive a packet from the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 100);

/* If status is NX_SUCCESS the “my_packet” pointer contains data received from
   the Telnet Client connection.  */
```
## <a name="nx_telnet_client_packet_send"></a>nx_telnet_client_packet_send

Invia pacchetto tramite client Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_client_packet_send(NX_TELNET_CLIENT *client_ptr, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto tramite l'istanza del client Telnet connessa in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **client_ptr**: puntatore al blocco di controllo client Telnet.
- **packet_ptr**: puntatore al pacchetto da inviare.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per l'invio del pacchetto del client Telnet. Le opzioni di attesa sono definite come segue:
    - **valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la trasmissione di pacchetti client è riuscita.
- **NX_TELNET_ERROR**: (0xF0) Impossibile inviare il pacchetto. il chiamante è responsabile del rilascio del pacchetto.
- NX_PTR_ERROR: (0x07) input puntatore non valido
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Send a packet via the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_send(&my_client, my_packet, 100);
/* If status is NX_SUCCESS the packet was successfully sent.  */

```

## <a name="nx_telnet_server_create"></a>nx_telnet_server_create

Creazione di un server Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_server_create(NX_TELNET_SERVER *server_ptr, CHAR *server_name, NX_IP *ip_ptr, 
                             VOID *stack_ptr, ULONG stack_size, 
                             void (*new_connection)(struct NX_TELNET_SERVER_STRUCT*telnet_server_ptr, 
                                                    UINT logical_connection), 
                             void (*receive_data)(struct NX_TELNET_SERVER_STRUCT *telnet_server_ptr, 
                                                  UINT logical_connection, NX_PACKET *packet_ptr), 
                             void (*connection_end)(struct NX_TELNET_SERVER_STRUCT *telnet_server_ptr, 
                                                    UINT logical_connection));

```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del server Telnet nell'istanza IP specificata.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al blocco di controllo del server Telnet.
- **server_name**: nome dell'istanza del server Telnet.
- **ip_ptr**: puntatore all'istanza IP associata.
- **stack_ptr**: puntatore allo stack per il thread del server interno.
- **sack_size**: dimensioni in byte dello stack.
- **new_connection**: puntatore alla funzione di routine di callback dell'applicazione. Questa routine viene chiamata ogni volta che il server rileva una nuova richiesta di connessione del client Telnet.
- **receive_data**: puntatore alla funzione di routine di callback dell'applicazione. Questa routine viene chiamata ogni volta che nella connessione sono presenti nuovi dati del client Telnet. Questa routine è responsabile del rilascio del pacchetto.
- **end_connection**: puntatore alla funzione di routine di callback dell'applicazione. Questa routine viene chiamata ogni volta che una connessione client Telnet viene disconnessa dal client o si verifica il timeout della connessione del client (scade il "timeout attività"). Il server può disconnettersi anche tramite il servizio *nx_telnet_server_disconnect* descritto di seguito.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la creazione del server è riuscita.
- NX_PTR_ERROR: (0x07) i puntatori a server, IP, stack o callback dell'applicazione non validi.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Create a Telnet Server instance “my_server”.  */
status =  nx_telnet_server_create(&my_server, "Telnet Server", &ip_0, 
                                   pointer, 2048, telnet_new_connection, 
                                   telnet_receive_data, telnet_connection_end);


/* If status is NX_SUCCESS the Telnet Server was successfully created.  */
```
## <a name="nx_telnet_server_delete"></a>nx_telnet_server_delete

Eliminare un server Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_server_delete(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del server Telnet creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al blocco di controllo del server Telnet.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) eliminazione server riuscita.
- NX_PTR_ERROR: (0x07) puntatore server non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_delete(&my_server);

/* If status is NX_SUCCESS the Telnet Server was successfully deleted.  */
```

## <a name="nx_telnet_server_disconnect"></a>nx_telnet_server_disconnect

Disconnettere un client Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_server_disconnect(NX_TELNET_SERVER *server_ptr, UINT logical_connection);
```

### <a name="description"></a>Descrizione

Questo servizio disconnette un client precedentemente connesso in questa istanza del server Telnet. Questa routine viene in genere chiamata dalla funzione di callback dei dati di ricezione dell'applicazione in risposta a una condizione rilevata nei dati ricevuti.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al blocco di controllo del server Telnet.
- **logical_connection**: connessione logica corrispondente alla connessione client in questo server. Il valore valido è compreso tra 0 e NX_TELENET_MAX_CLIENTS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) la disconnessione del server è riuscita.
- **NX_TELNET_ERROR**: la disconnessione del server (0xF0) non è riuscita.
- NX_OPTION_ERROR: (0x0A) connessione logica non valida.
- NX_PTR_ERROR: (0x07) puntatore server non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

/* Disconnect the Telnet Client associated with logical connection 2 on 
   the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_disconnect(&my_server, 2);

/* If status is NX_SUCCESS the Client on logical connection 2 was 
   disconnected.  */
```

## <a name="nx_telnet_server_get_open_connection_count"></a>nx_telnet_server_get_open_connection_count

Restituisce il numero di connessioni attualmente aperte

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_server_get_open_connection_count(NX_TELNET_SERVER *server_ptr, UINT *connection_count);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il numero di client Telnet attualmente connessi.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al blocco di controllo del server Telnet.
- **Connection_count**: puntatore alla memoria per archiviare il conteggio delle connessioni

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) completato correttamente.
- NX_PTR_ERROR: (0x07) puntatore server non valido.
- NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Get the number of Telnet Clients connected to the Server. */

status =  nx_telnet_server_get_open_connection_count(&my_server, &conn_count);

/* If status is NX_SUCCESS the conn_count holds the number of open connections.  */

```

## <a name="nx_telnet_server_packet_send"></a>nx_telnet_server_packet_send

Invia pacchetto tramite connessione client

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_server_packet_send(NX_TELNET_SERVER *server_ptr, 
                                  UINT logical_connection, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto alla connessione client in questa istanza del server Telnet. Questa routine viene in genere chiamata dalla funzione di callback dei dati di ricezione dell'applicazione in risposta a una condizione rilevata nei dati ricevuti.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al blocco di controllo del server Telnet.
- **logical_connection**: connessione logica corrispondente alla connessione client in questo server. Il valore valido è compreso tra 0 e NX_TELENET_MAX_CLIENTS.
- **packet_ptr**: puntatore al pacchetto ricevuto.
- **WAIT_OPTION**: definisce il tempo di attesa del servizio per l'invio di pacchetti del server Telnet. Le opzioni di attesa sono definite come segue:
    - **valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta. 

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) l'invio di pacchetti è riuscito.
- **NX_TELNET_FAILED**: (0xF2) trasmissione socket TCP non riuscita.
- NX_OPTION_ERROR: (0x0A) connessione logica non valida.
- NX_PTR_ERROR: (0x07) puntatore server non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Send a packet to the Telnet Client associated with logical connection 2 on 
   the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_packet_send(&my_server, 2, my_packet, 100);

/* If status is NX_SUCCESS the packet was sent to the Client on logical 
   connection 2.  */
```

## <a name="nx_telnet_server_packet_pool_set"></a>nx_telnet_server_packet_pool_set

Imposta pool di pacchetti creato in precedenza come pool di server Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_server_packet_pool_set(NX_TELNET_SERVER *server_ptr, NX_PACKET_POOL *packet_pool_ptr);

```

### <a name="description"></a>Descrizione

Questo servizio imposta un pool di pacchetti creato in precedenza come pool di pacchetti del server Telnet se è stato definito NX_TELNET_SERVER_USER_CREATE_PACKET_POOL. Richiede inoltre che NX_TELNET_SERVER_OPTION_DISABLE non sia definito in modo che il server Telnet necessiti di un pool di pacchetti per trasmettere le opzioni Telnet ai client Telnet.

Ciò consente alle applicazioni di creare il pool di pacchetti in memoria diversa, ad esempio senza memoria cache, rispetto allo stack del server Telnet. Si noti che se questa funzione non controlla se il pool di pacchetti del server Telnet è già impostato. Se viene chiamato su un puntatore al pool di pacchetti del server Telnet non null, lo sovrascriverà e sostituirà il pool di pacchetti esistente con il pool di pacchetti a cui punta il puntatore di input.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al blocco di controllo server Telnet
- **packet_pool_ptr**: puntatore al pool di pacchetti creato in precedenza

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) ha impostato correttamente il pool.
- NX_PTR_ERROR: (0x07) puntatore server non valido.

### <a name="allowed-from"></a>Consentito da

Init, thread

### <a name="example"></a>Esempio

```c
status =  nx_packet_pool_create(&telnet_server_packet_pool, 
                                "Telnet Server Packet Pool", 
                                telnet_server_pool_area, 600*10);

/* Set the packet pool as the Telnet Server packet pool.   */
status =  nx_telnet_server_packet_pool_set(&my_server, &telnet_server_packet_pool);

/* If status is NX_SUCCESS the packet pool is set as Telnet Server pool.  */
```
## <a name="nx_telnet_server_start"></a>nx_telnet_server_start

Avviare un server Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_server_start(NX_TELNET_SERVER *server_ptr);

```

### <a name="description"></a>Descrizione

Questo servizio avvia un'istanza del server Telnet creata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al blocco di controllo del server Telnet.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) avviata correttamente.
- **NX_TELNET_NO_PACKET_POOL**: (0XF6) non è stato impostato alcun pool di pacchetti
- NX_PTR_ERROR: (0x07) puntatore server non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="example"></a>Esempio

```c
/* Start the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_start(&my_server);

/* If status is NX_SUCCESS the Server was started.  */
```

## <a name="nx_telnet_server_stop"></a>nx_telnet_server_stop

Arrestare un server Telnet

### <a name="prototype"></a>Prototipo

```c
UINT nx_telnet_server_stop(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio interrompe un'istanza del server Telnet creata e avviata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al blocco di controllo del server Telnet.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) arrestato correttamente
- NX_PTR_ERROR: (0x07) puntatore server non valido.
- NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Stop the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_stop(&my_server);

/* If status is NX_SUCCESS the Server was stopped.  */
```