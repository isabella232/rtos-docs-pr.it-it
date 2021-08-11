---
title: Capitolo 1 - Introduzione alla Azure RTOS NetX Duo Telnet
description: Il Azure RTOS NetX Duo Telnet è un protocollo progettato per il trasferimento di comandi e risposte tra due nodi su Internet.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 50a2c4d8726863f4e609debadd9ddf2455cfd540219a476970756d3d250ec562
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799031"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-telnet"></a>Capitolo 1 - Introduzione alla Azure RTOS NetX Duo Telnet

Il Azure RTOS NetX Duo Telnet è un protocollo progettato per il trasferimento di comandi e risposte tra due nodi su Internet. Telnet è un protocollo semplice che usa i servizi Reliable Transmission Control Protocol (TCP) per eseguire la funzione di trasferimento. Per questo, Telnet è un protocollo di trasferimento altamente affidabile. Telnet è anche uno dei protocolli applicativi più usati.

## <a name="telnet-requirements"></a>Requisiti di Telnet

Per funzionare correttamente, il pacchetto Telnet di NetX Duo richiede che sia già stata creata un'istanza IP NetX. È inoltre necessario che TCP sia abilitato nella stessa istanza IP. La parte Telnet Client del pacchetto Telnet di NetX Duo non ha altri requisiti.

La parte Relativa al server Telnet del pacchetto Telnet di NetX Duo presenta un requisito aggiuntivo. Richiede l'accesso completo alla porta TCP *nota 23 per* la gestione di tutte le richieste Telnet client.

## <a name="telnet-constraints"></a>Vincoli Telnet 

Il protocollo Telnet di NetX Duo implementa lo standard Telnet. Tuttavia, l'interpretazione e la risposta dei comandi Telnet, indicata da un byte con valore 255, è responsabilità dell'applicazione. I vari comandi Telnet e i relativi parametri sono definiti nei *file nxd_telnet_client.h e nxd_telnet_server.h.*

## <a name="telnet-communication"></a>Telnet Communication

Come accennato in precedenza, il server Telnet usa la *porta TCP 23* nota per il campo Richieste client. I client Telnet possono usare qualsiasi porta TCP disponibile.

## <a name="telnet-authentication"></a>Autenticazione Telnet

L'autenticazione Telnet è responsabilità della funzione di callback del server Telnet dell'applicazione. Il callback "nuova connessione" del server Telnet dell'applicazione richiede in genere al client il nome e/o la password. Il client sarà quindi responsabile della fornitura delle informazioni. Il server elabora quindi le informazioni nel callback di "ricezione dati". Qui il codice del server applicazioni deve autenticare le informazioni e decidere se sono valide o meno.

## <a name="telnet-new-connection-callback"></a>Callback della nuova connessione Telnet

Il server Telnet di NetX Duo chiama la funzione di callback specificata dall'applicazione ogni volta che viene ricevuta una nuova richiesta client Telnet. L'applicazione specifica la funzione di callback quando il server Telnet viene creato tramite ***nx_telnet_server_create*** funzione. Le azioni tipiche del callback di "nuova connessione" includono l'invio di un banner o di una richiesta al client. Questo potrebbe includere una richiesta di informazioni di accesso.

### <a name="prototype"></a>Prototipo

```c
void  telnet_new_connection(NX_TELNET_SERVER *server_ptr, 
                            UINT logical_connection);
```

### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al server Telnet chiamante.
- **logical_connection**: connessione logica interna per il server Telnet. Può essere usato dall'applicazione come indice in buffer e/o strutture di dati specifiche per ogni connessione client. Il valore è compreso tra 0 e NX_TELNET_MAX_CLIENTS - 1.

## <a name="telnet-receive-data-callback"></a>Callback di ricezione dati Telnet

Il server Telnet di NetX Duo chiama la funzione di callback specificata dall'applicazione ogni volta che vengono ricevuti nuovi dati del client Telnet. L'applicazione specifica la funzione di callback quando il server Telnet viene creato tramite ***nx_telnet_server_create*** funzione. Le azioni tipiche del callback di "nuova connessione" includono l'eco dei dati e/o l'analisi dei dati e la fornitura di dati come risultato dell'interpretazione di un comando dal client.

Si noti che questa routine di callback deve rilasciare anche il pacchetto fornito.

### <a name="prototype"></a>Prototipo

```c
void  telnet_receive_data(NX_TELNET_SERVER *server_ptr, 
                          UINT logical_connection, NX_PACKET *packet_ptr);
```
### <a name="input-parameters"></a>Parametri di input

- **server_ptr**: puntatore al server Telnet chiamante.
- **logical_connection**: connessione logica interna per il server Telnet. Può essere usato dall'applicazione come indice in buffer e/o strutture di dati specifiche per ogni connessione client. Il valore è compreso tra 0 e NX_TELNET_MAX_CLIENTS - 1.
- **packet_ptr:** puntatore al pacchetto contenente i dati dal client.

## <a name="telnet-end-connection-callback"></a>Callback di fine connessione Telnet

Il server Telnet di NetX Duo chiama la funzione di callback specificata dall'applicazione ogni volta che un client Telnet termina la connessione. L'applicazione specifica la funzione di callback quando il server Telnet viene creato tramite ***nx_telnet_server_create*** funzione. Le azioni tipiche del callback di "fine connessione" includono la pulizia di tutte le strutture di dati specifiche del client associate alla connessione logica.

### <a name="prototype"></a>Prototipo
```c
void  telnet_end_connection(NX_TELNET_SERVER *server_ptr, 
                            UINT logical_connection);
```

### <a name="input-parameters"></a>Parametri di input

- **server_ptr** Puntatore al server Telnet chiamante.
- **logical_connection** Connessione logica interna per il server Telnet. Può essere usato dall'applicazione come indice in buffer e/o strutture di dati specifiche per ogni connessione client. Il valore è compreso tra 0 e NX_TELNET_MAX_CLIENTS - 1.

## <a name="telnet-option-negotiation"></a>Negoziazione dell'opzione Telnet

NetX Duo Telnet Server supporta un set limitato di opzioni Telnet, Echo e Suppress Go Ahead.

Per abilitare questa funzionalità, NX_TELNET_SERVER_OPTION_DISABLE non deve essere definito. Per impostazione predefinita, non è definito. Il server Telnet crea un pool di pacchetti nel *servizio nx_telnet_server_create* da cui alloca i pacchetti per l'invio di richieste di opzioni telnet al client. Vedere "Opzioni di configurazione" per impostare il payload dei pacchetti (NX_TELNET_SERVER_PACKET_PAYLOAD) e le dimensioni del pool di pacchetti (NX_TELNET_SERVER_PACKET_POOL_SIZE) per questo pool di pacchetti. Questo pool di pacchetti verrà eliminato quando viene *chiamato nx_telnet_server_delete* servizio.

Una volta stabilita una connessione con il client Telnet, invierà questo set di opzioni telnet al client se non ha ricevuto richieste di opzioni dal client:

- riecherà
- don't echo
- will sga

Quando riceve i dati Telnet dal client, il server Telnet controlla se il primo byte è il codice "IAC". In questo caso, verranno elaborate tutte le opzioni nel pacchetto client. Le opzioni non presenti nell'elenco precedente vengono ignorate.

Per impostazione predefinita, il server Telnet crea il proprio pool di pacchetti interno se NX_TELNET_SERVER_OPTION_DISABLE non è definito ed è necessario trasmettere i comandi dell'opzione Telnet. Il pool di pacchetti del server Telnet è definito NX_TELNET_SERVER_PACKET_PAYLOAD e NX_TELNET_SERVER_PACKET_POOLSIZE. Se, tuttavia, NX_TELNET_SERVER_USER_CREATE_PACKET_POOL è definito, l'applicazione deve creare il pool di pacchetti del server Telnet e impostarlo come pool di pacchetti del server Telnet *chiamando _nx_telnet_server_packet_pool_set*. Per altri dettagli su questa funzione, vedere il capitolo 3 "Descrizione dei servizi Telnet".

A differenza di NetX Duo Telnet Server, il thread dell'attività Client Telnet di NetX Duo non invia e risponde automaticamente alle opzioni ricevute dal server Telnet. Questa operazione deve essere eseguita dall'applicazione client Telnet.

## <a name="telnet-multi-thread-support"></a>Supporto multi-thread Telnet

I servizi client Telnet di NetX Duo possono essere chiamati contemporaneamente da più thread. Tuttavia, le richieste di lettura o scrittura per una particolare istanza del client Telnet devono essere eseguite in sequenza dallo stesso thread.

## <a name="telnet-rfcs"></a>RFC Telnet

NetX Duo Telnet è conforme a RFC854 e alle RFC correlate.
