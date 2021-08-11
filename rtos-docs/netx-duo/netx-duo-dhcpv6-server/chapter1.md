---
title: Capitolo 1 - Introduzione all'Azure RTOS server NetX Duo DHCPv6
description: Questo documento illustra in dettaglio come il server NetX Duo DHCPv6 assegna indirizzi IPv6 ai client DHCPv6.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 14a9d76731d949e3556a019756caf38b4ef440abfa4cfb927c47607e5712d9ac
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783654"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcpv6-server"></a>Capitolo 1 - Introduzione all'Azure RTOS server NetX Duo DHCPv6

Nelle reti IPv6, DHCPv6 è necessario per i client per ottenere gli indirizzi IPv6. Non sostituisce DHCP, che è limitato a IPv4in che non offre indirizzi IPv4. DHCPv6 offre funzionalità simili a DHCP e molti miglioramenti. Un client che non usa o non può usare la configurazione automatica degli indirizzi senza stato IPv6 può usare DHCPv6 per l'assegnazione di un indirizzo IPv6 globale univoco da un server DHCPv6.

NetX Duo è stato sviluppato per supportare applicazioni basate su rete IPv6 e protocolli di rete come DHCPv6. Questo documento illustra in dettaglio come il server NetX Duo DHCPv6 assegna indirizzi IPv6 ai client DHCPv6.

## <a name="dhcpv6-communication"></a>Comunicazione DHCPv6

**Struttura dei messaggi DHCPv6**

Il contenuto del messaggio è fondamentalmente un'intestazione del messaggio seguita da uno o più blocchi di opzioni (in genere più). Di seguito è riportata la struttura di base in cui ogni blocco rappresenta un byte:

![Diagramma che mostra la struttura del messaggio DHCPv6 e del blocco di opzioni.](media/image2.jpg)

**Figura 1. Struttura del blocco di opzioni e messaggi DHCPv6**

Il campo a 1 byte Msg-Type indica il tipo di messaggio DHCPv6. Il campo TRANSACTION-ID a 3 byte viene impostato dal client. Può essere utilizzato da qualsiasi sequenza di caratteri, ma deve essere univoco per ogni messaggio client inviato al server (conservato tra messaggi duplicati inviati dal client). Il server usa tale ID transazione per ogni risposta al client per consentire al client di associare i messaggi del server in caso di pacchetti ritardati o eliminati nella rete. Dopo il campo ID transazione, sono disponibili una o più opzioni DHCPv6 usate per indicare ciò che il client richiede.

La struttura delle opzioni DHCPv6 è costituita da un codice di opzione, un campo di lunghezza dell'opzione, che non include i campi di lunghezza o di codice, e infine i dati dell'opzione stessa, ovvero uno o più campi di codice di opzione a 2 byte per i dati che il client richiede.

Alcuni blocchi di opzioni hanno opzioni annidate. Ad esempio, *un'opzione Identity Association for Non Temporary Address (IANA)* contiene una o più opzioni *identity association (IA)* per richiedere indirizzi IPv6. L'opzione *IANA* restituita nel messaggio di risposta del server contiene le stesse opzioni *IA* con l'indirizzo IPv6 e i tempi di lease concessi dal server, nonché un'opzione Status che indica se si è verificato un errore con la richiesta dell'indirizzo client. 

Un elenco di tutti i blocchi di opzioni e la relativa descrizione è disponibile **nell'Appendice A.**

**Tipi di messaggi DHCPv6**

Anche se DHCPv6 migliora notevolmente le funzionalità di DHCP, usa lo stesso numero di messaggi di DHCP e supporta le stesse opzioni del fornitore di DHCP. L'elenco dei messaggi DHCPv6 è il seguente:

- SOLICT (1) (inviato dal client)
- ADVERTISE (2) (inviato dal server)
- REQUEST (3) (inviato dal client)
- REPLY (7) (inviato dal server)
- CONFIRM (4) (inviato dal client)
- RENEW (5) (inviato dal client)
- REBIND (6) (inviato dal client)
- RELEASE (8) (inviato dal client)
- DECLINE (9) (inviato dal client)
- INFORM_REQUEST (11) (inviato dal client)
- RECONFIGURE* (10) (inviato dal server)

*RECONFIGURE non è supportato dal server NetX Duo DHCPv6.

La sequenza di richieste DHCPv6 di base, con il tipo di messaggio DHCPv4 equivalente tra parentesi, è la seguente:

Client ***Solicit** _ (_Discovery *) Server **Advertisement** (* Offer *) Client **Request** (* Request *) Server **Reply** (* DHCPAck*)

Client **Renew**(same) Server **Reply** (*DHCPAck*)

## <a name="dhcpv6-message-validation"></a>Convalida dei messaggi DHCPv6

ID transazione: il client deve generare un ID transazione per ogni messaggio inviato al server. Il server DHCPv6 rifiuterà qualsiasi messaggio dal client che non corrisponde a questo ID transazione. Il server a sua volta deve usare lo stesso ID transazione nelle risposte al client.

**Identificatori univoci (DUID) DHCPv6**

Tutti i messaggi del server devono includere anche un identificatore univoco DHCPv6 (DUID) in ogni messaggio, in caso il client DHCPv6 non deve accettare il messaggio. Un DUID del livello di collegamento (LL) è un blocco di controllo contenente l'indirizzo MAC del client, il tipo di hardware e il tipo DUID. Un DUID LLT (Link Layer Time) contiene anche un campo ora che riduce le probabilità che il DUID non sia univoco nella rete host. Per questo motivo RFC 3315 consiglia i DUID LLT rispetto ai DUID LL. Se l'applicazione host non crea un valore di ora univoco, NetX Duo DHCPv6 ne fornirà uno predefinito. Il terzo tipo di DUID è il DUID Enterprise (assegnato dal fornitore) che contiene un ID Enterprise registrato (come in registrato con IANA) e dati privati di tipo e lunghezza variabili, ad esempio in base alle dimensioni della memoria, al tipo di sistema operativo di un'altra configurazione hardware. Vedere l'elenco delle opzioni di configurazione altrove in questo documento per configurare i valori di ID privati e assegnati dal fornitore del server.

Il client deve anche includere il relativo DUID nei messaggi al server, ad eccezione INFORM_REQUEST, in caso contrario il server li rifiuterà.

**Sessioni del server client DHCPv6**

I client e i server DHCPv6 scambiano messaggi tramite UDP. Il client usa la porta 546 per inviare e ricevere messaggi DHCPv6 e il server usa la porta 547. Il client usa inizialmente l'indirizzo locale del collegamento per la trasmissione e la ricezione di messaggi DHCPv6. Invia tutti i messaggi ai server DHCPv6 usando un indirizzo multicast riservato con ambito collegamento noto come indirizzo multicast *di All_DHCP_Relay_Agents_and_Servers* *(FF02::01:02).*

Per le richieste di assegnazione di indirizzi IPv6, il server DHCPv6 è in ascolto dei *messaggi Solicit* inviati all'All_DHCP_Relay_Agents_and_Servers richiesta.  Nella richiesta *Solicit il* client può richiedere l'assegnazione di un indirizzo IPv6 specifico o consentire al server di sceglierne uno. Può anche richiedere altre informazioni di configurazione di rete dal server.

Se DHCPv6Server estrae un messaggio *di* richiesta valido e può assegnare un indirizzo IPv6 al client, risponde con un messaggio *Advertise* contenente l'indirizzo IPv6 che concederà al client, il tempo di lease dell'indirizzo IPv6 ed eventuali informazioni aggiuntive richieste dal client. Se il client accetta l'offerta server, risponde con un messaggio *di* richiesta che informa il server che accetterà l'indirizzo IPv6. Il server conferma che il client è associato all'indirizzo IPv6 con un *messaggio di* risposta.

Se il messaggio client DHCPv6 non è valido, il server lo scarterà automaticamente. Se il server non è in grado di concedere la richiesta, invierà un messaggio *di* risposta con un'indicazione del problema nel campo stato dell'opzione IANA dell'indirizzo IP. Se vengono ricevute richieste client duplicate, il server invia nuovamente la risposta DHCPv6 precedente, presupponendo che il client semplicemente non abbia ricevuto il pacchetto.

È il Client a verificare che l'indirizzo IPv6 assegnato dal server non sia assegnato a un altro host nel sistema usando vari protocolli IPv6, ad esempio il rilevamento degli indirizzi duplicati. Se l'indirizzo non è univoco, il client invierà al server un *messaggio di rifiuto.* Il server aggiorna la tabella dei lease IP con queste informazioni, registrando che l'indirizzo è già assegnato. Nel frattempo, il client deve riavviare il processo di richiesta DHCPv6 con un *altro messaggio di richiesta.*

Oltre a un indirizzo IPv6, un client dovrà probabilmente conoscere anche il server DNS e probabilmente altre informazioni di rete, ad esempio il nome di dominio di rete. DHCPv6 fornisce i mezzi per richiedere queste informazioni utilizzando l'uso di Option Requests nei messaggi *Solicit* e *Request* o separatamente nei *messaggi di richiesta di* informazioni. Le opzioni DHCPv6 sono illustrate più avanti in questo capitolo.

**Durata lease IPv6**

Quando il server concede un indirizzo IPv6 a un client, assegna anche la durata del lease (durata) nell'opzione IANA per quando consiglia al client di avviare il rinnovo (T1) o di riassociare (T2) il proprio indirizzo IPv6 usando i messaggi *Renew* e *Rebind.* La differenza tra i due è che il client indirizza il messaggio *di* rinnovo al server includendo il DUID del server nella *richiesta di* rinnovo. Tuttavia, non specifica alcun server e pertanto non include un DUID del server, nel messaggio *Riassociato* *all'indirizzo All_DHCP_Relay_Agents_and_Servers* destinazione. L'opzione IA che contiene l'indirizzo IPv6 effettivo che il server concede al client contiene anche la durata preferita e valida quando l'indirizzo IPv6 con lease diventa deprecato o obsoleto (non valido), rispettivamente.

Il server NetX Duo DHCPv6 mantiene un timeout di sessione per ogni client per tenere traccia del tempo tra i messaggi client. Ciò è necessario in caso di perdita di connettività o in caso di insodit della rete da parte di un host client. Quando il timeout della sessione scade, si presuppone che il client non sia più interessato o in grado di effettuare richieste DHCPv6 del server. Il server elimina il record Client e restituisce qualsiasi indirizzo IPv6 assegnato provvisoriamente al pool disponibile. L'attesa del timeout della sessione è un'opzione configurabile dall'utente.

Se il client vuole rilasciare il proprio indirizzo IPv6 o rileva che l'indirizzo IPv6 assegnato dal server  DHCPv6 è già in uso, invia rispettivamente un messaggio di rilascio o rifiuto.  Nel caso di un messaggio *di* rilascio, il server restituisce lo stato dell'indirizzo IPv6 al pool disponibile. Nel caso del messaggio *Rifiuta,* aggiorna la tabella del lease IP per indicare che questo indirizzo IPv6 non è disponibile (di proprietà di un'altra entità in un'altra posizione nella rete).

**Dati di lease e record client IPv6**

Quando il server DHCPv6 inizia ad accettare le richieste client, mantiene un elenco di client attivi che richiedono o a cui sono stati assegnati indirizzi IPv6. Il server verifica la scadenza del lease IP tramite un timer di lease che aggiorna periodicamente la durata del lease del client. Quando la durata supera la durata valida, il server cancella il record Client e restituisce il relativo indirizzo IPv6 al pool disponibile. È il client ad avviare il processo di rinnovo/riassociazione prima di eseguire questa operazione.

La tabella dei record del client del server NetX Duo DHCPv6 contiene informazioni per identificare i client e informazioni sullo stato per convalidare le richieste client DHCPv6 e assegnare o rias assegnare indirizzi IPv6. Tali informazioni includono:

- Identificatore univoco (DUID) del client DHCPv6 che definisce in modo univoco ogni host client in una rete. Il client deve sempre usare lo stesso DUID per tutti i messaggi DHCPv6.

- L'associazione di identità client per gli indirizzi non temporanei (IANA) e l'indirizzo IPv6 dell'associazione di identità (IA) in modo cumulativo che definiscono i parametri di assegnazione degli indirizzi IPv6 del client.

- Richieste di opzioni client (server DNS, nome di dominio e così via).

- Indirizzo di origine IPv6 client (se impostato) e indirizzo di destinazione (se non multicast) della richiesta DHCPv6 più recente.

- Tipo di messaggio più recente del client e "stato" DHCPv6.

## <a name="netx-duo-dhcpv6-server-requirements-and-constraints"></a>Requisiti e vincoli del server NetX Duo DHCPv6

L'API del server NetX Duo DHCPv6 richiede ThreadX 5.1 o versione successiva e NetX Duo 5.5 o versione successiva.

**Requisiti**

***Configurazione dell'attività Thread IP***

Il server NetX Duo DHCPv6 richiede la creazione di un'istanza IP per l'invio e la ricezione di messaggi a DHCPv6 nel collegamento di rete. Questa operazione viene eseguita usando il *nx_ip_create* servizio. È necessario creare il server NetX Duo DHCPv6 stesso. Questa operazione viene eseguita usando il *nx_dhcpv6_server_create* servizio.

DHCPv6 usa NetX Duo, ICMPv6 e UDP. IPv6 deve quindi essere abilitato prima di usare il server DHCPv6 chiamando i servizi NetX Duo seguenti:

- *nx_udp_enable*
- *nxd_ipv6_enable*
- *nxd_icmp_enable*

Inoltre, prima di poter iniziare il server DHCPv6, è necessario configurare alcune attività da eseguire:

- Creare e convalidare gli indirizzi locali e globali IPv6 del collegamento. La convalida degli indirizzi viene eseguita automaticamente da NetX Duo usando il rilevamento degli indirizzi duplicati, se abilitato. Per informazioni dettagliate sulla convalida degli indirizzi IP locali e globali dei collegamenti, vedere il manuale dell'utente di *NetX Duo.*

- Impostare l'indice dell'interfaccia di rete per l'interfaccia DHCPv6.

- Creare un intervallo di indirizzi IP per gli indirizzi IPv6 assegnabili. In caso contrario, se esistono dati di una sessione DHCPv6 del server precedente, la tabella di lease IPv6 e i record client di tale sessione devono essere caricati dalla memoria non volatile nel server DHCPv6. Il piccolo sistema di esempio altrove in questo documento illustra i servizi del server DHCPv6 per l'esecuzione di questo requisito.

- Impostare il DUID del server. Se il server ha creato il proprio DUID in una sessione precedente, deve usare gli stessi dati per creare lo stesso DUID per i messaggi ai client. Il piccolo sistema di esempio altrove in questo documento illustra come viene raggiunto questo requisito.

A questo punto il server DHCPv6 è pronto per l'esecuzione. Internamente il server NetX Duo DHCPv6 creerà un socket UDP associato alla porta 547 e inizierà l'ascolto delle richieste client.

***Requisiti del pool di pacchetti***

Il server NetX Duo DHCPv6 richiede un pool di pacchetti per l'invio di messaggi DHCPv6. Le dimensioni del pool di pacchetti in termini di payload del pacchetto e numero di pacchetti disponibili sono configurabili dall'utente e dipendono dal volume previsto di messaggi DHCPv6 e altre trasmissioni che verranno inviati dall'applicazione host.

Un tipico messaggio DHCPv6 è di circa 200-300 byte a seconda del numero di opzioni aggiuntive richieste dal client e delle informazioni disponibili dal server.

***Impostazione dell'interfaccia del server DHCPv6***

Per impostazione predefinita, il server DHCPv6 è l'interfaccia di rete primaria in quanto l'interfaccia su cui accetterà le richieste client. Tuttavia, l'applicazione host deve comunque impostare l'indice indirizzi globale usato per creare l'indirizzo globale del server. L'indice dell'interfaccia DHCPv6 e l'indice degli indirizzi globali vengono impostati usando il *nx_dhcpv6_server_interface_set* servizio. Questo è illustrato anche nel "piccolo esempio" in questo documento.

***Salvataggio di DHCPv6 DUID tra riavvii del server***

Il protocollo DHCPv6 richiede al server di usare lo stesso DUID in più riavvii. Tutti i dati usati per creare il DUID devono quindi essere archiviati e recuperati dalla memoria non volatile per questo requisito. Per gli host che usano il DUID Link Layer Plus Time che richiede l'accesso a un orologio in tempo reale. L'applicazione host NetX Duo DHCPv6 deve includere l'accesso ai dati in tempo reale per la generazione di un valore temporale per la creazione iniziale di SERVER DUID e archiviare i dati per il riutilizzo nelle sessioni server successive. Il *nx_dhcpv6_set_server_duid* quindi accetta i dati DUID come argomenti, nonché le opzioni di configurazione a seconda del tipo DUID, per produrre (o riprodurre) il proprio DUID.

***Creazione dell'elenco indirizzi IPv6 assegnabile***

Dopo la creazione del server DHCPv6, l'applicazione host server deve creare un intervallo di indirizzi globali IPv6 assegnabili se non sono presenti dati dell'elenco indirizzi IP archiviati in precedenza. Questa operazione viene eseguita usando il *nx_dhcpv6_create_ip_address_range* che accetta come input un indirizzo IPv6 iniziale e finale.

***Salvataggio dei dati del client e dell'indirizzo assegnabile DHCPv6***

Il protocollo DHCPv6 richiede che il server DHCPv6 salvi i dati degli indirizzi Client e IPv6 nell'archiviazione non volatile in caso di riavvio del server. Il server NetX Duo DHCPv6 include diverse API per il caricamento e il download dei dati degli indirizzi Client e IPv6 da e verso il server DHCPv6, rispettivamente:

*nx_dhcpv6_add_client_record*

*nx_dhcpv6_add_ip_address_lease*

*nx_dhcpv6_retrieve_client_record*

*nx_dhcpv6_retrieve_ip_address_lease*

Il caricamento dei dati nel server deve essere eseguito prima di riavviare il server. Il download dei dati deve essere eseguito solo dopo l'arresto (o la sospensione) del server DHCPv6. I servizi per questa operazione sono descritti in dettaglio più avanti in questo documento. NetX Duo DHCPv6, tuttavia, non definisce un accesso all'archiviazione non volatile. Deve essere gestito dall'applicazione host. Il piccolo esempio illustra come l'applicazione host esegue questa operazione.

***Server DHCP Unique Identifier (DUID)***

Il DUID del server definisce in modo univoco l'host del server DHCPv6 nella rete. Se un server non ha creato in precedenza il duid, può usare il nx_dhcpv6_server_set_duid *per* crearne uno. Come da RFC 3315, il server DHCPv6 deve salvare questo DUID in memoria non volatile per poterlo recuperare dopo il riavvio del server. Il server DHCPv6 supporta i tipi DUID Livello di collegamento, Tempo livello di collegamento e Enterprise (assegnato dal fornitore). Si noti che il client deve inviare direttamente il tipo di fornitore DUID. L'opzione per i DUID di tipo fornitore (17) non è supportata direttamente dal server NetX Duo DHPv6.

L'applicazione host del server DHCPv6 ha valori predefiniti per l'assegnazione di indirizzi IPv6, incluso il timeout di lease. Per informazioni su come impostare queste opzioni, vedere Opzioni configurabili più avanti in questo documento. :

Il blocco di controllo *IANA* contiene i campi T1 e T2. Il *blocco IA* nel blocco *di controllo IANA* contiene i campi di durata preferiti e validi. L'applicazione host dispone di opzioni configurabili definite altrove in questo documento per l'impostazione di queste opzioni. Vengono assegnati a tutte le richieste di indirizzi IPv6 client.

Questi parametri di lease IP DHCPv6 sono definiti di seguito.

T1: tempo in secondi in cui il client deve iniziare a rinnovare l'indirizzo IPv6 dal server che lo ha assegnato.

T2: tempo in secondi in cui il client deve iniziare a riassociare l'indirizzo IPv6, se il rinnovo non è riuscito, con qualsiasi server nel collegamento.

Durata preferita: tempo in secondi in cui l'indirizzo client diventa deprecato se il client non lo ha rinnovato o riassato. Il client può comunque usare questo indirizzo.

Durata valida: tempo in secondi in cui l'indirizzo IP del client è scaduto e NON DEVE usare questo indirizzo nelle trasmissioni di rete.

La RFC consiglia T1 e T2 volte rispettivamente 0,5 e 0,8 della durata preferita nell'opzione *Client IANA.* Se il server non ha preferenze, deve impostare questi orari su zero. Se una risposta del server contiene T1 e T2 volte impostate su zero, il client imposta le proprie ore T1 e T2.

**Vincoli**

Il server NetX Duo DHCPv6 non supporta le opzioni DHCPv6 seguenti:

  - Opzione di commit rapido che ottimizza il processo di richiesta di indirizzi DHCPv6 solo per lo scambio di messaggi Solicit e Reply

  - Opzione di riconfigurazione che consente al server di avviare le modifiche allo stato dell'indirizzo IP del client.

  - Opzione Unicast; tutti i messaggi client devono essere inviati *all'All_DHCP_Relay_Agents_and_Servers* multicast anziché direttamente al server DHCPv6.

  - Associazione di identità per l'opzione Indirizzi temporanei (IA_TA) che è un indirizzo IP temporaneo concesso a un client.

  - Più opzioni IA (indirizzi IPv6) per ogni richiesta client

  - L'host di inoltro tra client e server DHCPv6, ad esempio client e server, deve essere nella stessa rete.

  - IPSec e Autenticazione non sono supportati nella messaggistica DHCPv6. Tuttavia, l'istanza IP può essere abilitata per IPSec a seconda della versione di NetX Duo in uso.

  - Il server NetX Duo DHCPv6 supporta direttamente solo la richiesta di opzione del server DNS. Questo potrebbe cambiare nelle versioni future.

  - L'opzione Delega del prefisso non è supportata.

  - Autenticazione dei messaggi DHCPv6 anche se IPSec può essere abilitato nell'ambiente NetX Duo sottostante. Né il server NetX Duo DHCPv6 supporta le connessioni di inoltro ai client. Si presuppone che tutte le richieste client provenino da host nella rete server.

## <a name="netx-duo-dhcpv6-server-callback-functions"></a>Funzioni di callback del server NetX Duo DHCPv6

*nx_dhcpv6_IP_address_declined_handler*

Quando il client DHCPv6 invia un messaggio di rifiuto, il server NetX Duo DHCPv6 contrassegna l'indirizzo come non disponibile nelle tabelle degli indirizzi IPv6. Per poter personalizzare la gestione del server di questo messaggio, viene nx_dhcpv6_IP_address_declined_handler *viene* fornito *.* Tuttavia, questo callback non è attualmente implementato.

*nx_dhcpv6_server_option_request_handler*

Quando il messaggio del client DHCPv6 contiene dati di richiesta dell'opzione, il server NetX Duo DHCPv6 inoltra ogni codice di opzione di richiesta di opzione a questo callback utente, se definito. In questo modo NetX Duo Server può consentire al callback definito dall'utente di compilare i dati. Tuttavia, questa funzionalità non è attualmente implementata.

## <a name="supported-dhcpv6-rfcs"></a>RFC DHCPv6 supportate

NetX Duo DHCPv6 è conforme a RFC3315, RFC3646 e alle RFC correlate.