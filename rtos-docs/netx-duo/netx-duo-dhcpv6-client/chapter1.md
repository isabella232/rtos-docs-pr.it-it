---
title: Capitolo 1 - Introduzione a Azure RTOS client NetX Duo DHCPv6
description: Nelle reti IPv6 DHCPv6 sostituisce DHCP per l'assegnazione dinamica degli indirizzi IP globali da un server DHCPv6 e offre la maggior parte delle stesse funzionalità e molti miglioramenti.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f938be404c121f3080cfed1a81aa356f698538c4f557387009d951df40496a6d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791313"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcpv6-client"></a>Capitolo 1 - Introduzione a Azure RTOS client NetX Duo DHCPv6

Nelle reti IPv6 DHCPv6 sostituisce DHCP per l'assegnazione dinamica degli indirizzi IP globali da un server DHCPv6 e offre la maggior parte delle stesse funzionalità e molti miglioramenti. Questo documento illustra in dettaglio come viene usata l Azure RTOS API del client NetX Duo DHCPv6 per ottenere gli indirizzi IPv6.

## <a name="dhcpv6-communication"></a>Comunicazione DHCPv6

Il protocollo DHCPv6 usa UDP. Il client usa la porta 546 e il server usa la porta 547 per scambiare messaggi DHCPv6. Il client usa l'indirizzo locale del collegamento per un indirizzo di origine per avviare le richieste DHCPv6 ai server DHCPv6 disponibili. Quando il client invia messaggi destinati a tutti i server DHCPv6 in rete, usa l'indirizzo *multicast All_DHCP_Relay_Agents_and_Servers* *FF02::01:02*. Si tratta di un indirizzo multicast riservato con ambito collegamento.

## <a name="dhcpv6-process-of-requesting-an-ipv6-address"></a>Processo DHCPv6 di richiesta di un indirizzo IPv6

Per iniziare il processo di richiesta di un'assegnazione di indirizzo IPv6 globale, un client invia prima di tutto un messaggio SOLICIT usando il *nx_dhcpv6_send_solicit* servizio:

**UINT nx_dhcpv6_request_solicit(NX_DHCPV6 \* dhcpv6_ptr)**

Questo messaggio viene inviato a tutti i server usando *l'All_DHCP_Relay_Agents_and_Servers* server. Nella richiesta SOLICIT il client può richiedere l'assegnazione di indirizzi IPv6 specifici come hint al server. Può anche richiedere altre informazioni di configurazione di rete dal server, ad esempio il server DNS, il server NTP e altre opzioni nella richiesta di opzione nel messaggio SOLICIT.

Un server DHCPv6 che può rispondere a una richiesta client risponde con un messaggio ADVERTISE contenente gli indirizzi IPv6 che può assegnare al client, il tempo di lease dell'indirizzo IPv6 ed eventuali informazioni aggiuntive richieste dal client. Il protocollo client DHCPv6 richiede al client di attendere un periodo di tempo per ricevere messaggi ADVERTISE da tutti i server DHCPv6 nella rete. Pre-elabora ogni messaggio ADVERTISE come un messaggio valido e analizza i dati delle opzioni per vari parametri DHCPv6. Controlla anche il valore Preferenza nell'opzione preferenza, se specificato dal server. Se viene ricevuto più di un messaggio ADVERTISE, il client NetX DHCPv6 sceglie il server con il valore di preferenza più alto ricevuto entro la fine del periodo di attesa.

L'eccezione è se il client riceve un messaggio ADVERTISE con un valore di preferenza pari a 255. Accetta immediatamente il messaggio ed elimina tutti i messaggi ADVERTISE successivi.

Il periodo di attesa è definito come il periodo di ritrasmissione che il client DHCPv6 attende prima di inviare un altro messaggio SOLICIT se non ha ricevuto una risposta da alcun server. Il timeout di ritrasmissione iniziale nello stato SOLICIT viene definito da al protocollo DHCPv6 descritto in RFC 3315 come 1 secondo. Gli intervalli di ritrasmissione successivi, se il client DHCPv6 non riceve una risposta server valida, vengono raddoppiati fino a un massimo di 120 secondi.

Dopo aver scelto il server, il client estrae i dati dal messaggio ADVERTISE e invia un messaggio REQUEST al server per accettare le informazioni sull'indirizzo assegnato e i tempi di lease. Il server risponde con un messaggio REPLY per confermare che gli indirizzi IPv6 del client sono registrati con il server come assegnato al client.

Il client DHCPv6 registra gli indirizzi IPv6 assegnati con l'istanza IP ,ad esempio NetX Duo. Se configurato per il protocollo DI RILEVAMENTO DEGLI indirizzi duplicati (ABILITATA per impostazione predefinita), NetX Duo invierà automaticamente messaggi Neighbor Solicit per verificare che gli indirizzi assegnati siano univoci nella rete. In tal caso, invia una notifica al client DHCPv6 quando ogni indirizzo assegnato è stato promosso da TENTATIVE a VALID. Il client DHCPv6 viene promosso allo stato BOUND e il dispositivo può usare tale indirizzo IPv6 per inviare e trasmettere messaggi. Se il protocollo UDP ha esito negativo, NetX Duo invia una notifica al client DHCPv6 e il client DHCPv6 invia un messaggio DECLINE per gli indirizzi IPv6 assegnati al server e reimposta lo stato del client DHCPv6 sullo stato INIT.

### <a name="notification-of-successful-address-assignment-and-validation"></a>Notifica di esito positivo dell'assegnazione e della convalida degli indirizzi

L'applicazione può determinare il risultato della richiesta di indirizzo del client DHCPv6 dalle modifiche dello stato se il client DHCPv6 è configurato con il callback di modifica dello stato nel *servizio* nx_dhcpv6_client_create. Se non riceve alcuna risposta dal server, la modifica dello stato osservata è da SOLICIT a INIT. Se ha ricevuto una risposta dal server ma il server non è in grado di assegnare l'indirizzo, l'applicazione riceverà una notifica dal callback di errore del server client DHCPv6 se configurato con uno (anche in *nx_dhcpv6_client_create).* Se il client ha raggiunto lo stato BOUND ma non ha superato il controllo DELL'operazione, verrà visualizzato un cambiamento di stato da BOUND a INIT. Si noti che un'applicazione abilitata per IL TEMPO DI ESECUZIONE DELLA RICHIESTA deve consentire il controllo DELL'evento DOPO l'avvio del processo di richiesta. In genere si tratta di circa 400-500 tick (4-5 secondi nella maggior parte dei casi).

### <a name="relinquishing-an-ipv6-address"></a>Relinquishing an IPv6 Address

Se e quando il client deve rilasciare un indirizzo IPv6 assegnato, informa il server DHCPv6 chiamando il *nx_dhcpv6_request_release* servizio:

### <a name="uint-nx_dhcpv6_request_releasenx_dhcpv6-dhcpv6_ptr"></a>UINT nx_dhcpv6_request_release(NX_DHCPV6 \* dhcpv6_ptr)

Il client DHCPv6 invia un messaggio RELEASE unicast contenente gli indirizzi assegnati al server che ha assegnato l'indirizzo e attende una risposta che conferma che il server ha ricevuto il messaggio.

Nota: è presente un processo diverso per il client che si sta riavviando ma prevede di continuare a usare gli indirizzi IPv6 assegnati al riavvio. Non invia il messaggio RELEASE all'accensione, a meno che non si prevede di richiedere un nuovo indirizzo di accensione. Per una spiegazione di questa situazione, vedere "Requisiti di memoria non volatile".

### <a name="dhcpv6-lease-timeouts"></a>Timeout lease DHCPv6

Il lease IPv6 assegnato dal server contiene due parametri di timeout, T1 e T2 in ogni blocco Identity Association – Non Temporary Addresses (IANA). Un'interfaccia IANA è descritta altrove in questo Manuale dell'utente. Se il tempo trascorso da quando il client DHCPv6 è stato associato all'indirizzo IPv6 assegnato è uguale a T1, il client DHCPv6 avvia automaticamente il rinnovo dell'indirizzo IPv6 inviando un messaggio RENEW. Se il tempo trascorso è uguale a T2, il client DHCPv6 invia automaticamente un messaggio REBIND se non ha ricevuto risposte alle richieste RENEW.

Altri due parametri di lease IPv6, ovvero la durata preferita e valida, vengono assegnati a ogni blocco Identity Association (IA) contenuto nel blocco IANA. Le durate preferite e valide sono quando l'indirizzo IPv6 assegnato è deprecato o non valido, rispettivamente. T1 deve essere minore della durata preferita. T2 deve essere minore della durata valida.

### <a name="ip-thread-task-requirements"></a>Requisiti delle attività thread IP

Il client NetX Duo DHCPv6 richiede la creazione di un'istanza IP di NetX Duo prima della creazione del client DHCPv6 per l'uso dei servizi client DHCPv6.

UDP, IPv6 e ICMPv6 devono essere abilitati nell'istanza IP prima di usare il client DHCPv6.

  - *nx_udp_enable*

  - *nxd_ipv6_enable*

  - *nxd_icmp_enable*

### <a name="packet-pool-requirements"></a>Requisiti del pool di pacchetti

La creazione del client NetX Duo DHCPv6 richiede un pool di pacchetti creato in precedenza per l'invio di messaggi DHCPv6. Le dimensioni del pool di pacchetti in termini di payload dei pacchetti e numero di pacchetti disponibili sono configurabili dall'utente e dipendono dal volume previsto di messaggi DHCPv6 e altre trasmissioni che verranno inviati dall'applicazione.

Un tipico messaggio DHCPv6 è di circa 200 byte a seconda del numero di indirizzi IA e delle opzioni DHCPv6 richieste dal client.

### <a name="network-requirements"></a>Requisiti di rete

Il client NetX Duo DHCPv6 richiede la creazione di un socket UDP associato alla porta 546. Il socket viene creato quando viene creata l'attività client DHCPv6.

### <a name="non-volatile-memory-requirements"></a>Requisiti di memoria non volatile

Se un client DHCPv6 rilascia il lease IPv6 con il server DHCPv6 all'accensione e richiede nuovi indirizzi IPv6 al riavvio, non è necessaria l'archiviazione di memoria non volatile. Se un client vuole continuare a usare il lease assegnato, deve archiviare determinate informazioni sul client DHCPv6 in memoria non volatile tra un riavvio e l'altro.

I requisiti di memoria non volatile e l'API client DHCPv6 sono illustrati più avanti in **Using the NetX Duo DHCPv6 Client** in Chapter Two (Uso del client NetX Duo DHCPv6 nel capitolo 2).

### <a name="netx-duo-dhcpv6-client-limitations"></a>Limitazioni del client NetX Duo DHCPv6

La versione corrente del client NetX Duo DHCPv6 presenta le limitazioni seguenti:

  - Il client NetX Duo DHCPv6 non supporta l'opzione Server Unicast per l'invio di messaggi DHCPv6 unicast al server DHCPv6, anche se il server indica che questa operazione è consentita.

  - Il client NetX Duo DHCPv6 non supporta la richiesta di riconfigurazione in cui un server avvia le modifiche dell'indirizzo IPv6 ai client nella rete.

  - Il client NetX Duo DHCPv6 non supporta il formato Enterprise per il blocco di controllo identificatore univoco DHCPv6. Supporta solo il formato Livello di collegamento e Livello collegamento più ora.

  - Il client NetX Duo DHCPv6 non supporta le richieste di indirizzi TA (Temporary Association), ma supporta le richieste di opzioni non temporanee (IANA).

## <a name="multihome-and-multiple-address-support"></a>Supporto di più indirizzi e multihome

Il client DHCPv6 supporta più interfacce e più indirizzi per ogni interfaccia. Il servizio client DHCPv6, *nx_dhcpv6_client_set_interface* consente all'applicazione client di impostare l'interfaccia di rete su cui l'applicazione comunichi con il server DHCPv6. Per impostazione predefinita, il client DHCPv6 è l'interfaccia primaria (indice zero).

Per più indirizzi per interfaccia, il client DHCPv6 mantiene un elenco interno di indirizzi a partire dall'indice 0. Si noti che lo stesso indirizzo registrato con il client DHCPv6 potrebbe non trovarsi necessariamente nello stesso indice nella tabella IP degli indirizzi di interfaccia.

Per i servizi client DHCPv6 che recuperano informazioni sul lease dell'indirizzo IPv6 del client, è necessario che sia specificato un indice di indirizzi. Di seguito è riportato un esempio per ottenere la durata preferita e valida:

```C
UINT nx_dhcpv6_get_valid_ip_address_lease_time(NX_DHCPV6 *dhcpv6_ptr, 
                                              UINT address_index, 
                                              NXD_ADDRESS *ip_address,
                                              ULONG preferred_lifetime, 
                                              ULONG *valid_lifetime)
```

L'applicazione client può anche recuperare il numero di indirizzi IPv6 validi assegnati dal *nx_dhcpv6_get_valid_ip_address_count* servizio:

```C
UINT nx_dhcpv6_get_valid_ip_address_count(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT *address_count)
```

I servizi client DHCPv6 legacy creati prima del supporto di più indirizzi in NetX Duo non accettano un indice di indirizzi. Pertanto, con questi servizi, i dati richiesti vengono prelevati dall'indirizzo IA globale primario, indipendentemente dal numero di indirizzi IA assegnati al client. Di seguito è riportato un esempio:

```C
UINT nx_dhcpv6_get_IP_address(NX_DHCPV6 *dhcpv6_ptr, 
                              NXD_ADDRESS *ip_address)
```

## <a name="netx-duo-dhcpv6-client-callback-functions"></a>Funzioni di callback del client NetX Duo DHCPv6

*nx_dhcpv6_state_change_callback*

Quando il client DHCPv6 viene modificato in un nuovo stato DHCPv6 in seguito all'elaborazione di una richiesta DHCPv6, invia una notifica all'applicazione con questa funzione di callback.

*nx_dhcpv6_server_error_handler*

Quando il client DHCPv6 riceve una risposta server contenente un'opzione *Status* con stato diverso da zero (non riuscito), invia una notifica all'applicazione con questo callback che include il codice di stato dell'errore del server.

Nota: poiché queste funzioni di callback vengono chiamate dall'attività thread del client DHCPv6, l'applicazione client NON deve chiamare servizi client NetX Duo DHCPv6 che richiedono il controllo mutex del client DHCPv6, ad esempio *nx_dhcpv6_start, nx_dhcpv6_stop* e qualsiasi API che invia messaggi direttamente dal callback, ad esempio *nx_dhcpv6_request_release*.

## <a name="dhcpv6-rfcs"></a>RFC DHCPv6

NetX Duo DHCP è conforme a RFC3315, RFC3646 e alle RFC correlate.