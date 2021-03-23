---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo Telnet
description: Azure RTO NetX Duo Telnet è un protocollo progettato per il trasferimento di comandi e risposte tra due nodi in Internet.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d25f5ca4a7bf1ecf4c3d0c68ef6c8aeda7800098
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821638"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-telnet"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo Telnet

Azure RTO NetX Duo Telnet è un protocollo progettato per il trasferimento di comandi e risposte tra due nodi in Internet. Telnet è un protocollo semplice che utilizza i servizi di Transmission Control Protocol affidabili (TCP) per eseguire la relativa funzione di trasferimento. Per questo motivo, Telnet è un protocollo di trasferimento altamente affidabile. Telnet è anche uno dei protocolli applicativi più usati.

## <a name="telnet-requirements"></a>Requisiti di Telnet

Per funzionare correttamente, il pacchetto telnet NetX Duo richiede che sia già stata creata un'istanza IP di NetX. Inoltre, è necessario abilitare TCP nella stessa istanza di IP. La parte client Telnet del pacchetto telnet NetX Duo non ha altri requisiti.

Il server Telnet parte del pacchetto telnet NetX Duo presenta un requisito aggiuntivo. Richiede l'accesso completo alla *porta 23 TCP nota* per la gestione di tutte le richieste Telnet del client.

## <a name="telnet-constraints"></a>Vincoli Telnet 

Il protocollo Telnet NetX Duo implementa lo standard Telnet. Tuttavia, l'interpretazione e la risposta dei comandi Telnet, indicati da un byte con valore 255, sono responsabili dell'applicazione. I vari comandi e parametri del comando Telnet sono definiti nei file *nxd_telnet_client. h e nxd_telnet_server. h* .

## <a name="telnet-communication"></a>Comunicazione Telnet

Come indicato in precedenza, il server Telnet utilizza la *Nota porta TCP 23* per il campo richieste client. I client Telnet possono usare qualsiasi porta TCP disponibile.

## <a name="telnet-authentication"></a>Autenticazione Telnet

L'autenticazione Telnet è responsabilità della funzione di callback del server Telnet dell'applicazione. Il callback del server Telnet "nuova connessione" dell'applicazione richiede in genere al client il nome e/o la password. Il client sarà quindi responsabile di fornire le informazioni. Il server elaborerà quindi le informazioni nel callback "Receive Data". Questo è il punto in cui il codice del server applicazioni deve autenticare le informazioni e decidere se è valido o meno.

## <a name="telnet-new-connection-callback"></a>Callback nuova connessione Telnet

Il server Telnet NetX Duo chiama la funzione di callback specificata dall'applicazione ogni volta che viene ricevuta una nuova richiesta del client Telnet. L'applicazione specifica la funzione di callback quando il server Telnet viene creato tramite la funzione ***nx_telnet_server_create*** . Le azioni tipiche del callback "nuova connessione" includono l'invio di un banner o una richiesta al client. Questa operazione potrebbe includere una richiesta di informazioni di accesso.

### <a name="prototype"></a>Prototipo

```c
void  telnet_new_connection(NX_TELNET_SERVER *server_ptr, 
                            UINT logical_connection);
```

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al server Telnet chiamante.
- **logical_connection**: la connessione logica interna per il server Telnet. Questo può essere utilizzato dall'applicazione come indice in buffer e/o strutture di dati specifiche per ogni connessione client. Il valore è compreso tra 0 e NX_TELNET_MAX_CLIENTS-1.

## <a name="telnet-receive-data-callback"></a>Callback dei dati di ricezione Telnet

Il server Telnet NetX Duo chiama la funzione di callback specificata dall'applicazione ogni volta che vengono ricevuti nuovi dati del client Telnet. L'applicazione specifica la funzione di callback quando il server Telnet viene creato tramite la funzione ***nx_telnet_server_create*** . Le azioni tipiche del callback "nuova connessione" includono l'eco dei dati e/o l'analisi dei dati e la fornitura di dati come risultato dell'interpretazione di un comando dal client.

Si noti che questa routine di callback deve rilasciare anche il pacchetto fornito.

### <a name="prototype"></a>Prototipo

```c
void  telnet_receive_data(NX_TELNET_SERVER *server_ptr, 
                          UINT logical_connection, NX_PACKET *packet_ptr);
```
### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al server Telnet chiamante.
- **logical_connection**: la connessione logica interna per il server Telnet. Questo può essere utilizzato dall'applicazione come indice in buffer e/o strutture di dati specifiche per ogni connessione client. Il valore è compreso tra 0 e NX_TELNET_MAX_CLIENTS-1.
- **packet_ptr**: puntatore al pacchetto contenente i dati dal client.

## <a name="telnet-end-connection-callback"></a>Callback di connessione finale Telnet

Il server Telnet NetX Duo chiama la funzione di callback specificata dall'applicazione ogni volta che un client telnet termina la connessione. L'applicazione specifica la funzione di callback quando il server Telnet viene creato tramite la funzione ***nx_telnet_server_create*** . Le azioni tipiche del callback "End Connection" includono la pulizia delle strutture di dati specifiche del client associate alla connessione logica.

### <a name="prototype"></a>Prototipo
```c
void  telnet_end_connection(NX_TELNET_SERVER *server_ptr, 
                            UINT logical_connection);
```

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al server Telnet chiamante.
- **logical_connection** Connessione logica interna per il server Telnet. Questo può essere utilizzato dall'applicazione come indice in buffer e/o strutture di dati specifiche per ogni connessione client. Il valore è compreso tra 0 e NX_TELNET_MAX_CLIENTS-1.

## <a name="telnet-option-negotiation"></a>Negoziazione di opzioni Telnet

Il server Telnet NetX Duo supporta un set limitato di opzioni Telnet, ad ECHO e a non visualizzare più avanti.

Per abilitare questa funzionalità, il NX_TELNET_SERVER_OPTION_DISABLE non deve essere definito. Per impostazione predefinita, non è definito. Il server Telnet crea un pool di pacchetti nel servizio *nx_telnet_server_create* da cui alloca i pacchetti per l'invio di richieste di opzioni Telnet al client. Vedere "opzioni di configurazione" per impostare il payload del pacchetto (NX_TELNET_SERVER_PACKET_PAYLOAD) e le dimensioni del pool di pacchetti (NX_TELNET_SERVER_PACKET_POOL_SIZE) per questo pool di pacchetti. Questo pool di pacchetti verrà eliminato quando viene chiamato il servizio *nx_telnet_server_delete* .

Quando si effettua una connessione con il client Telnet, questo set di opzioni Telnet verrà inviato al client se non sono state ricevute richieste di opzioni dal client:

- Echo
- non Echo
- SGA

Quando riceve dati Telnet dal client, il server Telnet controlla se il primo byte è il codice "IAC". In tal caso, vengono elaborate tutte le opzioni nel pacchetto client. Le opzioni non presenti nell'elenco precedente vengono ignorate.

Per impostazione predefinita, il server Telnet crea il proprio pool di pacchetti interno se NX_TELNET_SERVER_OPTION_DISABLE non è definito ed è necessario trasmettere i comandi delle opzioni Telnet. Il pool di pacchetti del server Telnet è definito da NX_TELNET_SERVER_PACKET_PAYLOAD e NX_TELNET_SERVER_PACKET_POOLSIZE. Se, tuttavia, NX_TELNET_SERVER_USER_CREATE_PACKET_POOL è definito, l'applicazione deve creare il pool di pacchetti del server Telnet e impostarlo come pool di pacchetti del server Telnet chiamando *_nx_telnet_server_packet_pool_set*. Per altri dettagli su questa funzione, vedere il capitolo 3 "Descrizione dei servizi Telnet".

Diversamente dal server Telnet NetX Duo, il thread attività client Telnet NetX Duo non invia e risponde automaticamente alle opzioni ricevute dal server Telnet. Questa operazione deve essere eseguita dall'applicazione client Telnet.

## <a name="telnet-multi-thread-support"></a>Supporto multithreading Telnet

I servizi client Telnet NetX Duo possono essere chiamati da più thread contemporaneamente. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client Telnet devono essere eseguite in sequenza dallo stesso thread.

## <a name="telnet-rfcs"></a>RFC per Telnet

NetX Duo Telnet è conforme a RFC854 e alle RFC correlate.
