---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo DHCPv6 client
description: Nelle reti IPv6, DHCPv6 sostituisce DHCP per l'assegnazione di indirizzi IP globali dinamici da un server DHCPv6 e offre la maggior parte delle stesse funzionalità, oltre a molti miglioramenti.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3bf3b52c53bb26e2c9c2c736ae35817eb967f609
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822001"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcpv6-client"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo DHCPv6 client

Nelle reti IPv6, DHCPv6 sostituisce DHCP per l'assegnazione di indirizzi IP globali dinamici da un server DHCPv6 e offre la maggior parte delle stesse funzionalità, oltre a molti miglioramenti. Questo documento illustra in dettaglio in che modo viene usata l'API client DHCPv6 di Azure RTO NetX Duo per ottenere gli indirizzi IPv6.

## <a name="dhcpv6-communication"></a>Comunicazione DHCPv6

Il protocollo DHCPv6 utilizza UDP. Il client utilizza la porta 546 e il server utilizza la porta 547 per scambiare messaggi DHCPv6. Il client usa l'indirizzo locale del collegamento per un indirizzo di origine per avviare le richieste DHCPv6 ai server DHCPv6 disponibili. Quando il client invia messaggi destinati a tutti i server DHCPv6 sulla rete, usa l'  indirizzo multicast All_DHCP_Relay_Agents_and_Servers *FF02:: 01:02*. Si tratta di un indirizzo multicast riservato con ambito collegamento.

## <a name="dhcpv6-process-of-requesting-an-ipv6-address"></a>Processo DHCPv6 di richiesta di un indirizzo IPv6

Per iniziare il processo di richiesta di un'assegnazione di indirizzi IPv6 globale, un client invia un messaggio di SOLLECITAzione tramite il servizio *nx_dhcpv6_send_solicit* :

**UINT nx_dhcpv6_request_solicit (NX_DHCPV6 \* dhcpv6_ptr)**

Questo messaggio viene inviato a tutti i server che usano l'indirizzo *All_DHCP_Relay_Agents_and_Servers* . Nella richiesta di SOLLECITAzione il client può richiedere l'assegnazione di indirizzi IPv6 specifici come hint al server. Può anche richiedere altre informazioni di configurazione di rete dal server, ad esempio server DNS, server NTP e altre opzioni nella richiesta di opzione nel messaggio di SOLLECITAzione.

Un server DHCPv6 che può soddisfare una richiesta client risponde con un messaggio di annuncio contenente gli indirizzi IPv6 che può assegnare al client, il tempo di lease degli indirizzi IPv6 e tutte le informazioni aggiuntive richieste dal client. Il protocollo client DHCPv6 richiede che il client attenda un periodo di tempo per la ricezione dei messaggi di annuncio da tutti i server DHCPv6 sulla rete. Pre-elabora ogni messaggio di annuncio come un messaggio valido e analizza i dati delle opzioni per i vari parametri DHCPv6. Verifica anche il valore preferenza nell'opzione preferenza, se fornita dal server. Se viene ricevuto più di un messaggio di annuncio, il client DHCPv6 NetX sceglie il server con il valore di preferenza più elevato ricevuto entro la fine del periodo di attesa.

L'eccezione si verifica se il client riceve un messaggio di annuncio con un valore di preferenza pari a 255. Accetta immediatamente il messaggio e ignora tutti i messaggi di annuncio successivi.

Il periodo di attesa viene definito come periodo di ritrasmissione che il client DHCPv6 attende prima di inviare un altro messaggio di SOLLECITAzione se non ha ricevuto una risposta da alcun server. Il timeout di ritrasmissione iniziale nello stato SOLLECITAzione viene definito da al protocollo DHCPv6 descritto in RFC 3315 come 1 secondo. Gli intervalli di ritrasmissione successivi, se il client DHCPv6 non riesce a ricevere una risposta server valida, sono raddoppiati fino a un massimo di 120 secondi.

Dopo aver scelto il server, il client estrae i dati dal messaggio di annuncio e invia un messaggio di richiesta al server per accettare le informazioni relative all'indirizzo e i tempi di lease assegnati. Il server risponde con un messaggio di risposta per verificare che gli indirizzi IPv6 del client siano registrati con il server come assegnati al client.

Il client DHCPv6 registra gli indirizzi IPv6 assegnati con l'istanza IP, ad esempio NetX Duo. Se è stato configurato per il protocollo di rilevamento degli indirizzi duplicati (DAD) (abilitato per impostazione predefinita), NetX Duo invierà automaticamente i messaggi di sollecito adiacenti per verificare che gli indirizzi assegnati siano univoci nella rete. In tal caso, viene inviata una notifica al client DHCPv6 quando ogni indirizzo assegnato è stato promosso da PROVVISORIo a valido. Il client DHCPv6 viene promosso allo stato associato e il dispositivo può utilizzare tale indirizzo IPv6 per inviare e trasmettere messaggi. Se il protocollo DAD ha esito negativo, NetX Duo invia una notifica al client DHCPv6 e il client DHCPv6 invia un messaggio di rifiuto per gli indirizzi IPv6 assegnati di nuovo al server e Reimposta lo stato del client DHCPv6 sullo stato INIT.

### <a name="notification-of-successful-address-assignment-and-validation"></a>Notifica dell'assegnazione e della convalida degli indirizzi riuscita

L'applicazione può determinare il risultato della richiesta di indirizzo del client DHCPv6 dalle modifiche di stato se il client DHCPv6 è configurato con il callback di modifica dello stato nel servizio *nx_dhcpv6_client_create* . Se non riceve alcuna risposta dal server, la modifica dello stato osservato è da SOLLECITAzione a INIT. Se è stata ricevuta una risposta dal server, ma il server non è in grado di assegnare l'indirizzo, l'applicazione riceverà una notifica dal callback di errore del server client DHCPv6 se configurata con una (anche in *nx_dhcpv6_client_create).* Se il client ha eseguito lo stato associato ma non ha superato il controllo padre, visualizzerà una modifica dello stato da BOUND a INIT. Si noti che un'applicazione abilitata per papà deve attendere il controllo del padre dopo l'avvio del processo di richiesta. Si tratta in genere di circa 400-500 di cicli (4-5 secondi nella maggior parte dei casi).

### <a name="relinquishing-an-ipv6-address"></a>Cessione di un indirizzo IPv6

Se e quando il client deve rilasciare un indirizzo IPv6 assegnato, informa il server DHCPv6 chiamando il servizio *nx_dhcpv6_request_release* :

### <a name="uint-nx_dhcpv6_request_releasenx_dhcpv6-dhcpv6_ptr"></a>UINT nx_dhcpv6_request_release (NX_DHCPV6 \* dhcpv6_ptr)

Il client DHCPv6 invia un messaggio di rilascio unicast contenente gli indirizzi assegnati al server che ha assegnato l'indirizzo e attende una risposta confermando che il server ha ricevuto il messaggio.

Nota: è disponibile un processo diverso per il client che si accende ma prevede di continuare a usare gli indirizzi IPv6 assegnati al riavvio. Non invia il messaggio di rilascio per l'accensione, a meno che non si preveda di richiedere un nuovo indirizzo all'accensione. Per una spiegazione di questa situazione, vedere "requisiti di memoria non volatile".

### <a name="dhcpv6-lease-timeouts"></a>Timeout lease DHCPv6

Il lease IPv6 assegnato dal server contiene due parametri di timeout, T1 e T2 in ogni blocco IANA (associazione di identità). Una IANA è descritta in un'altra parte di questo manuale dell'utente. Se il tempo trascorso dal momento in cui il client DHCPv6 è stato associato all'indirizzo IPv6 assegnato è uguale a T1, il client DHCPv6 inizia automaticamente a rinnovare l'indirizzo IPv6 inviando un messaggio di rinnovo. Se il tempo trascorso è uguale a T2, il client DHCPv6 invia automaticamente un messaggio di riassociazione se non riceve risposte alle richieste di rinnovo.

Altri due parametri di lease IPv6, la durata preferita e valida, vengono assegnati a ogni blocco di associazione di identità (IA) contenuto nel blocco IANA. Le durate preferite e valide si verificano quando l'indirizzo IPv6 assegnato è deprecato o non valido, rispettivamente. T1 deve essere inferiore alla durata preferita. T2 deve essere inferiore alla durata valida.

### <a name="ip-thread-task-requirements"></a>Requisiti per le attività dei thread IP

Il client DHCPv6 NetX Duo richiede la creazione di un'istanza IP di NetX Duo precedente alla creazione del client DHCPv6 per l'uso dei servizi client DHCPv6.

È necessario abilitare UDP, IPv6 e ICMPv6 nell'istanza IP prima di utilizzando il client DHCPv6.

  - *nx_udp_enable*

  - *nxd_ipv6_enable*

  - *nxd_icmp_enable*

### <a name="packet-pool-requirements"></a>Requisiti del pool di pacchetti

Per la creazione del client NetX Duo DHCPv6 è necessario un pool di pacchetti creato in precedenza per l'invio di messaggi DHCPv6. Le dimensioni del pool di pacchetti in termini di payload del pacchetto e numero di pacchetti disponibili sono configurabili dall'utente e dipendono dal volume previsto di messaggi DHCPv6 e da altre trasmissioni che l'applicazione invierà.

Un messaggio DHCPv6 tipico è di circa 200 byte, a seconda del numero di indirizzi IA e delle opzioni DHCPv6 richiesti dal client.

### <a name="network-requirements"></a>Requisiti di rete

Il client DHCPv6 NetX Duo richiede la creazione del socket UDP associato alla porta 546. Il socket viene creato quando viene creata l'attività client DHCPv6.

### <a name="non-volatile-memory-requirements"></a>Requisiti di memoria non volatili

Se un client DHCPv6 rilascia il lease IPv6 con il server DHCPv6 quando si accende e richiede nuovi indirizzi IPv6 al riavvio, non è necessaria alcuna archiviazione di memoria non volatile. Se un client desidera continuare a utilizzare il lease assegnato, deve archiviare determinate informazioni sul client DHCPv6 sulla memoria non volatile tra i riavvii.

I requisiti di memoria non volatili e l'API client DHCPv6 vengono descritti ulteriormente in **utilizzo del client Dhcpv6 NETX Duo** nel capitolo due.

### <a name="netx-duo-dhcpv6-client-limitations"></a>Limitazioni client di NetX Duo DHCPv6

La versione corrente del client NetX Duo DHCPv6 presenta le limitazioni seguenti:

  - Il client NetX Duo DHCPv6 non supporta l'opzione unicast del server per l'invio di messaggi DHCPv6 unicast al server DHCPv6 anche se il server indica che questa operazione è consentita.

  - Il client NetX Duo DHCPv6 non supporta la richiesta di riconfigurazione in cui un server avvia le modifiche degli indirizzi IPv6 nei client della rete.

  - Il client NetX Duo DHCPv6 non supporta il formato Enterprise per il blocco di controllo univoco dell'identificatore DHCPv6. Supporta solo il livello di collegamento e il formato di collegamento più tempo.

  - Il client NetX Duo DHCPv6 non supporta le richieste di indirizzi di associazione temporanea (TA), ma supporta le richieste di opzioni non temporanee (IANA).

## <a name="multihome-and-multiple-address-support"></a>Supporto multihome e indirizzi multipli

Il client DHCPv6 supporta più interfacce e più indirizzi per interfaccia. Il servizio client DHCPv6, *nx_dhcpv6_client_set_interface* consente all'applicazione client di impostare l'interfaccia di rete in cui l'applicazione comunicherà con il server DHCPv6. Il client DHCPv6 imposta come valore predefinito l'interfaccia primaria (indice zero).

Per più indirizzi per interfaccia, il client DHCPv6 mantiene un elenco interno di indirizzi a partire dall'indice 0. Si noti che lo stesso indirizzo registrato con il client DHCPv6 potrebbe non trovarsi necessariamente nello stesso indice nella tabella IP degli indirizzi di interfaccia.

Per i servizi client DHCPv6 che recuperano informazioni sul lease di indirizzi IPv6 client, alcuni richiedono che venga specificato un indice di indirizzo. Di seguito è riportato un esempio per ottenere la durata preferita e valida:

```C
UINT nx_dhcpv6_get_valid_ip_address_lease_time(NX_DHCPV6 *dhcpv6_ptr, 
                                              UINT address_index, 
                                              NXD_ADDRESS *ip_address,
                                              ULONG preferred_lifetime, 
                                              ULONG *valid_lifetime)
```

L'applicazione client può anche recuperare il numero di indirizzi IPv6 validi assegnati dal servizio *nx_dhcpv6_get_valid_ip_address_count* :

```C
UINT nx_dhcpv6_get_valid_ip_address_count(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT *address_count)
```

I servizi client DHCPv6 legacy creati prima del supporto di più indirizzi in NetX Duo non accettano un indice di indirizzo. Con questi servizi, quindi, i dati richiesti vengono ricavati dall'indirizzo globale IA primario, indipendentemente dal numero di indirizzi IA assegnati al client. Di seguito è riportato un esempio:

```C
UINT nx_dhcpv6_get_IP_address(NX_DHCPV6 *dhcpv6_ptr, 
                              NXD_ADDRESS *ip_address)
```

## <a name="netx-duo-dhcpv6-client-callback-functions"></a>Funzioni di callback del client DHCPv6 NetX Duo

*nx_dhcpv6_state_change_callback*

Quando il client DHCPv6 passa a un nuovo stato DHCPv6 come risultato dell'elaborazione di una richiesta DHCPv6, invia una notifica all'applicazione con questa funzione di callback.

*nx_dhcpv6_server_error_handler*

Quando il client DHCPv6 riceve una risposta del server contenente un'opzione di *stato* con uno stato diverso da zero (non riuscito), invia una notifica all'applicazione con questo callback che include il codice di stato di errore del server.

Nota: poiché queste funzioni di callback vengono chiamate dall'attività thread del client DHCPv6, l'applicazione client non deve chiamare alcun servizio client DHCPv6 NetX duo che richiede il controllo mutex del client DHCPv6, ad esempio *nx_dhcpv6_start, nx_dhcpv6_stop* e qualsiasi API che invii messaggi direttamente dal callback, ad esempio *nx_dhcpv6_request_release*.

## <a name="dhcpv6-rfcs"></a>RFC DHCPv6

Il protocollo DHCP di NetX Duo è compatibile con RFC3315, RFC3646 e RFC correlati.