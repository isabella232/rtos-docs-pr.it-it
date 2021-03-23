---
title: Capitolo 1-Introduzione al server DHCPv6 di Azure RTO NetX Duo
description: Questo documento illustra in dettaglio il modo in cui il server DHCPv6 NetX Duo assegna gli indirizzi IPv6 ai client DHCPv6.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6cf7baa91b1804876b97b1d75d1872d1120ad028
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821947"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcpv6-server"></a>Capitolo 1-Introduzione al server DHCPv6 di Azure RTO NetX Duo

Nelle reti IPv6 DHCPv6is richiede che i client ottengano gli indirizzi IPv6. Non sostituisce DHCP, che è limitato al protocollo IPv4, che non offre indirizzi IPv4. DHCPv6 presenta funzionalità simili a DHCP, oltre a molti miglioramenti. Un client che non è in grado di utilizzare la configurazione automatica degli indirizzi senza stato IPv6 può utilizzare DHCPv6 per l'assegnazione di un indirizzo IPv6 globale univoco da un server DHCPv6.

NetX Duo è stato sviluppato per supportare applicazioni basate su rete IPv6 e protocolli di rete, ad esempio DHCPv6. Questo documento illustra in dettaglio il modo in cui il server DHCPv6 NetX Duo assegna gli indirizzi IPv6 ai client DHCPv6.

## <a name="dhcpv6-communication"></a>Comunicazione DHCPv6

**Struttura del messaggio DHCPv6**

Il contenuto del messaggio è fondamentalmente un'intestazione del messaggio seguita da uno o più blocchi di opzioni (di solito più). Di seguito è riportata la struttura di base in cui ogni blocco rappresenta un byte:

![Diagramma che mostra la struttura del blocco di messaggi e opzioni di DHCPv6.](media/image2.jpg)

**Figura 1. Struttura del blocco di messaggi e opzioni DHCPv6**

Il campo Msg-Type a 1 byte indica il tipo di messaggio DHCPv6. Il campo Transaction-ID di 3 byte viene impostato dal client. Può essere utilizzata da qualsiasi sequenza di caratteri, ma deve essere univoca per ogni messaggio client al server (conformemente ai messaggi duplicati inviati dal client). Il server utilizza tale ID di transazione per ogni risposta al client per consentire al client di associare i messaggi del server in caso di pacchetti ritardati o eliminati in rete. Dopo il campo Transaction-ID sono disponibili una o più opzioni DHCPv6 per indicare le richieste del client.

La struttura dell'opzione DHCPv6 è costituita da un codice di opzione, un campo di lunghezza delle opzioni, che non include i campi lunghezza o codice, e infine i dati di opzione stessi che corrispondono a uno o più campi di codice opzione a 2 byte per i dati richiesti dal client.

Alcuni blocchi di opzioni hanno opzioni nidificate. Ad esempio, un' *associazione di identità per l'opzione di indirizzo non temporaneo (IANA)* contiene una o più opzioni di *associazione di identità (IA)* per richiedere indirizzi IPv6. L'opzione *IANA* restituita nel messaggio di risposta del server contiene le stesse opzioni *Ia* (s) con l'indirizzo IPv6 e i tempi di lease concessi dal server, oltre a un'opzione di *stato* che indica se si è verificato un errore con la richiesta di indirizzo client.

Nell' **appendice a** è disponibile un elenco di tutti i blocchi di opzioni e la relativa descrizione.

**Tipi di messaggio DHCPv6**

Sebbene DHCPv6 rafforzi significativamente la funzionalità di DHCP, USA lo stesso numero di messaggi di DHCP e supporta le stesse opzioni del fornitore di DHCP. L'elenco dei messaggi DHCPv6 è il seguente:

- SOLICT (1) (inviato dal client)
- ANNUNCIO (2) (inviato dal server)
- REQUEST (3) (inviato dal client)
- Rispondi (7) (inviato dal server)
- CONFERMA (4) (inviato dal client)
- RINNOVO (5) (inviato dal client)
- Riassocia (6) (inviato dal client)
- VERSIONE (8) (inviata dal client)
- RIFIUTARE (9) (inviato dal client)
- INFORM_REQUEST (11) (inviato dal client)
- Riconfigura * (10) (inviato dal server)

* RECONFIGURE non è supportato dal server NetX Duo DHCPv6.

La sequenza di richieste DHCPv6 di base, con il tipo di messaggio estensione DHCPv4 equivalente tra parentesi, è la seguente:

Client ***sollecita** _ (_Discovery *) **annuncio** Server (* offerta *) **richiesta** client*(richiesta *) **risposta** server*(DHCPACK *)

**Risposta** server di **rinnovo**(stessa) del client (*DHCPACK*)

## <a name="dhcpv6-message-validation"></a>Convalida del messaggio DHCPv6

ID transazione: il client deve generare un ID transazione per ogni messaggio inviato al server. Il server DHCPv6 rifiuterà tutti i messaggi provenienti dal client che non corrispondono a questo ID transazione. Il server deve a sua volta utilizzare lo stesso ID transazione nelle risposte al client.

**Identificatori univoci di DHCPv6 (Duid)**

Tutti i messaggi server devono includere anche un identificatore univoco DHCPv6 (DUID) in ogni messaggio oppure il client DHCPv6 non deve accettare il messaggio. Un DUID di collegamento è un blocco di controllo che contiene l'indirizzo MAC client, il tipo di hardware e il tipo DUID. Un DUID LLT (link layer Time) contiene anche un campo temporale che consente di ridurre le probabilità che DUID non sia univoco nella rete host. Per questo motivo, RFC 3315 consiglia LLT Duid over LL Duid. Se l'applicazione host non crea il proprio valore di ora univoco, NetX Duo DHCPv6 ne fornirà uno predefinito. Il terzo tipo di DUID è il DUID Enterprise (Vendor assegnato) che contiene un ID Enterprise registrato, come registrato con IANA, e dati privati variabili nel tipo e nella lunghezza, ad esempio in base alle dimensioni della memoria, al tipo di sistema operativo di altre configurazioni hardware. Vedere l'elenco delle opzioni di configurazione in un altro punto del documento per configurare i valori di ID privati e assegnati del fornitore del server.

Il client deve inoltre includere i relativi DUID nei messaggi al server, ad eccezione di INFORM_REQUEST, oppure il server li rifiuterà.

**Sessioni del server client DHCPv6**

I client e i server DHCPv6 scambiano messaggi tramite UDP. Il client utilizza la porta 546 per inviare e ricevere messaggi DHCPv6 e il server utilizza la porta 547. Inizialmente il client usa l'indirizzo locale del collegamento per la trasmissione e la ricezione di messaggi DHCPv6. Invia tutti i messaggi ai server DHCPv6 usando un indirizzo multicast riservato con ambito collegamento noto come indirizzo multicast *All_DHCP_Relay_Agents_and_Servers* *(FF02:: 01:02)*.

Richieste di assegnazione di indirizzi ForIPv6, il server DHCPv6 è in ascolto dei messaggi di *sollecito* inviati all'indirizzo *All_DHCP_Relay_Agents_and_Servers* . Nella richiesta di *sollecitazione* il client può richiedere l'assegnazione di un indirizzo IPv6 specifico o consentire al server di sceglierne una. Può anche richiedere altre informazioni sulla configurazione di rete dal server.

Se il DHCPv6Server estrae un messaggio di *sollecitazione* valido e può assegnare un indirizzo IPv6 al client, risponde con un messaggio di *annuncio* che contiene l'indirizzo IPv6 che verrà concesso al client, il tempo di lease degli indirizzi IPv6 ed eventuali informazioni aggiuntive richieste dal client. Se il client accetta l'offerta server risponde con un messaggio di *richiesta* che informa il server che l'indirizzo IPv6 verrà accettato. Il server conferma che il client è associato all'indirizzo IPv6 con un messaggio di *risposta* .

Se il messaggio DHCPv6 del client non è valido, il server ignorerà il messaggio automaticamente. Se il server non è in grado di concedere la richiesta, invierà un messaggio di *risposta* con un'indicazione del problema nel campo stato dell'opzione indirizzo IP IANA. Se vengono ricevute richieste client duplicate, il server invia nuovamente la risposta DHCPv6 precedente, supponendo che il client non abbia ricevuto semplicemente il pacchetto.

Il client verifica che l'indirizzo IPv6 assegnato dal server non sia assegnato a un altro host nel sistema utilizzando diversi protocolli IPv6, ad esempio il rilevamento di indirizzi duplicati. Se l'indirizzo non è univoco, il client invierà al server un messaggio di *rifiuto* . Il server aggiorna la tabella di lease IP con queste informazioni, registrando che l'indirizzo è già assegnato. Nel frattempo il client deve riavviare il processo di richiesta DHCPv6 con un altro messaggio di *sollecitazione* .

Oltre a un indirizzo IPv6, è probabile che un client conosca anche il server DNS e possibilmente altre informazioni di rete, ad esempio il nome di dominio di rete. DHCPv6 fornisce i mezzi per richiedere queste informazioni tramite l'utilizzo delle richieste di opzioni nei messaggi *di richiesta e* *richiesta* o separatamente nei messaggi di *richiesta di informazioni* . Le opzioni di DHCPv6 sono illustrate più avanti in questo capitolo.

**Durata lease IPv6**

Quando il server concede un indirizzo IPv6 a un client, assegna anche la durata del lease (Lifetime) nell'opzione IANA per quando consiglia al client di avviare il rinnovo (T1) o il riassociazione (T2) del relativo indirizzo IPv6 usando il *rinnovo* e la *riassociazione dei messaggi* . La differenza tra i due è che il client indirizza il messaggio di *rinnovo* al server includendo il server Duid nella richiesta di *rinnovo* . Tuttavia, non specifica alcun server, quindi non include un server DUID nel messaggio di *riassociazione* all'indirizzo del *All_DHCP_Relay_Agents_and_Servers* . L'opzione IA che contiene l'indirizzo IPv6 effettivo concesso dal server al client contiene anche le durate preferite e valide quando l'indirizzo IPv6 con lease diventa deprecato o obsoleto (non valido), rispettivamente.

Il server DHCPv6 NetX Duo mantiene un timeout di sessione per ogni client per tenere traccia del tempo tra i messaggi del client. Questa operazione è necessaria in caso di perdita della connettività o della rete da parte di un host client. Una volta scaduto il timeout della sessione, si presuppone che il client non sia più interessato o in grado di effettuare richieste DHCPv6 del server. Il server Elimina il record client e restituisce qualsiasi indirizzo IPv6 assegnato provvisoriamente al pool disponibile. L'attesa del timeout della sessione è un'opzione configurabile dall'utente.

Se il client desidera rilasciare l'indirizzo IPv6 o rileva che l'indirizzo IPv6 assegnato dal server DHCPv6 è già in uso, invierà rispettivamente un messaggio di *rilascio* o di *rifiuto* . Nel caso di un messaggio di *rilascio* , il server restituisce lo stato dell'indirizzo IPv6 al pool disponibile. Nel caso del messaggio di *rifiuto* , viene aggiornata la tabella dei lease IP per indicare che l'indirizzo IPv6 non è disponibile (di proprietà di un'altra entità in altre parti della rete).

**Dati di lease e record client IPv6**

Quando il server DHCPv6 inizia ad accettare le richieste client, gestisce un elenco dei client attivi che richiedono o sono stati assegnati indirizzi IPv6. Il server verifica la scadenza del lease IP per mezzo di un timer di lease che aggiorna periodicamente la durata del lease client. Quando la durata supera la durata valida, il server cancella il record client e restituisce il relativo indirizzo IPv6 al pool disponibile. È il client ad avviare il processo di rinnovo/riassociazione prima che questo avvenga.

La tabella di record client del server DHCPv6 NetX Duo contiene informazioni per identificare i client e informazioni sullo stato per la convalida delle richieste del client DHCPv6 e l'assegnazione o la riassegnazione degli indirizzi IPv6. Tali informazioni includono:

- Identificatore univoco del client DHCPv6 (DUID) che definisce in modo univoco ogni host client in una rete. Il client deve sempre usare lo stesso DUID per tutti i relativi messaggi DHCPv6.

- Associazione di identità del client per gli indirizzi non temporanei (IANA) e indirizzo IPv6 dell'associazione di identità (IA) che definiscono i parametri di assegnazione di indirizzi IPv6 del client.

- Richieste di opzioni client (server DNS, nome di dominio e così via).

- L'indirizzo di origine IPv6 del client (se impostato) e l'indirizzo di destinazione (se non multicast) della richiesta DHCPv6 più recente.

- Il tipo di messaggio più recente del client e il "stato" di DHCPv6.

## <a name="netx-duo-dhcpv6-server-requirements-and-constraints"></a>Requisiti e vincoli del server DHCPv6 NetX Duo

Per l'API del server DHCPv6 NetX Duo è necessario ThreadX 5,1 o versione successiva e NetX Duo 5,5 o versione successiva.

**Requisiti**

***Impostazione attività thread IP***

Il server DHCPv6 NetX Duo richiede la creazione di un'istanza IP per l'invio e la ricezione di messaggi su DHCPv6 sul collegamento di rete. Questa operazione viene eseguita utilizzando il servizio *nx_ip_create* . È necessario creare il server NetX Duo DHCPv6. Questa operazione viene eseguita utilizzando il servizio *nx_dhcpv6_server_create* .

DHCPv6 USA NetX Duo, ICMPv6 e UDP. Pertanto, è necessario abilitare IPv6 prima di usare il server DHCPv6 chiamando i servizi NetX Duo seguenti:

- *nx_udp_enable*
- *nxd_ipv6_enable*
- *nxd_icmp_enable*

Inoltre, prima che il server DHCPv6 possa essere avviato, è necessario eseguire alcune attività di configurazione:

- Creare e convalidare il collegamento degli indirizzi globali locali e IPv6. La convalida degli indirizzi viene eseguita automaticamente da NetX Duo utilizzando il rilevamento degli indirizzi duplicati, se abilitato. Per informazioni dettagliate sul collegamento della convalida degli indirizzi IP globali e locali, vedere il *manuale dell'utente di NETX Duo* .

- Impostare l'indice dell'interfaccia di rete per l'interfaccia DHCPv6.

- Creare un intervallo di indirizzi IP per gli indirizzi IPv6 assegnabili. In alternativa, se i dati sono presenti in una sessione DHCPv6 del server precedente, i record della tabella e del client di lease IPv6 da tale sessione devono essere caricati dalla memoria non volatile al server DHCPv6. Nel piccolo sistema di esempio di questo documento vengono illustrati i servizi del server DHCPv6 per l'esecuzione di questo requisito.

- Impostare il server DUID. Se il server ha creato DUID in una sessione precedente, deve usare gli stessi dati per creare lo stesso DUID per i messaggi ai client. Il piccolo sistema di esempio in un altro punto di questo documento illustra il modo in cui viene eseguito questo requisito.

A questo punto il server DHCPv6 è pronto per l'esecuzione. Internamente, il server NetX Duo DHCPv6 creerà un socket UDP associato alla porta 547 e inizierà l'ascolto delle richieste client.

***Requisiti del pool di pacchetti***

Il server NetX Duo DHCPv6 richiede un pool di pacchetti per l'invio di messaggi DHCPv6. Le dimensioni del pool di pacchetti in termini di payload del pacchetto e numero di pacchetti disponibili sono configurabili dall'utente e variano a seconda del volume previsto di messaggi DHCPv6 e di altre trasmissioni che verranno inviate dall'applicazione host.

Un messaggio DHCPv6 tipico è di circa 200-300 byte a seconda del numero di opzioni aggiuntive richieste dal client e delle informazioni disponibili dal server.

***Impostazione dell'interfaccia del server DHCPv6***

Il server DHCPv6 utilizza per impostazione predefinita l'interfaccia di rete primaria come interfaccia su cui accetterà le richieste client. Tuttavia, l'applicazione host deve comunque impostare l'indice dell'indirizzo globale usato per creare l'indirizzo globale del server. L'indice dell'interfaccia DHCPv6 e l'indice globale degli indirizzi vengono impostati utilizzando il servizio *nx_dhcpv6_server_interface_set* . Questa operazione è illustrata anche nel "piccolo esempio" di questo documento.

***Salvataggio di DUID DHCPv6 tra i riavvii del server***

Il protocollo DHCPv6 richiede che il server usi lo stesso DUID tra più riavvii. Tutti i dati utilizzati per creare il DUID devono pertanto essere archiviati e recuperati dalla memoria non volatile per questo requisito. Per gli host che usano il collegamento layer Plus Time DUID che richiede l'accesso a un clock in tempo reale. L'applicazione host DHCPv6 NetX Duo deve includere l'accesso ai dati in tempo reale per generare un valore di ora per la creazione iniziale del server DUID e archiviare tali dati per il riutilizzo nelle sessioni server successive. Il *nx_dhcpv6_set_server_duid* accetta quindi i dati Duid come argomenti, nonché le opzioni di configurazione a seconda del tipo Duid, per produrre (o riprodurre) il proprio Duid.

***Creazione elenco indirizzi IPv6 assegnabile***

Dopo la creazione del server DHCPv6, l'applicazione host server deve creare un intervallo di indirizzi globali IPv6 assegnabili se non sono presenti dati dell'elenco di indirizzi IP archiviati in precedenza. Questa operazione viene eseguita utilizzando il servizio *nx_dhcpv6_create_ip_address_range* che accetta come input un indirizzo IPv6 iniziale e finale.

***Salvataggio di dati del client e degli indirizzi assegnabili di DHCPv6***

Il protocollo DHCPv6 richiede che il server DHCPv6 salvi i dati degli indirizzi client e IPv6 in una risorsa di archiviazione non volatile in caso di riavvio del server. Il server DHCPv6 NetX Duo dispone di diverse API per il caricamento e il download dei dati degli indirizzi client e IPv6 da e verso il server DHCPv6, rispettivamente:

*nx_dhcpv6_add_client_record*

*nx_dhcpv6_add_ip_address_lease*

*nx_dhcpv6_retrieve_client_record*

*nx_dhcpv6_retrieve_ip_address_lease*

Il caricamento dei dati nel server deve essere eseguito prima di riavviare il server. Il download dei dati deve essere eseguito solo dopo l'arresto o la sospensione del server DHCPv6. I servizi per questa operazione sono descritti in dettaglio più avanti in questo documento. Tuttavia, NetX Duo DHCPv6 fornisce non definisce l'accesso a un archivio non volatile. Questa operazione deve essere gestita dall'applicazione host. Nel piccolo esempio viene illustrato il modo in cui l'applicazione host esegue questa operazione.

***Identificatore univoco DHCP del server (DUID)***

Il server DUID definisce in modo univoco l'host del server DHCPv6 sulla rete. Se un server non ha creato in precedenza il relativo DUID, può usare il *nx_dhcpv6_server_set_duid* per crearne uno. In base allo standard RFC 3315, il server DHCPv6 deve salvare questo DUID nella memoria non volatile per poterlo recuperare dopo il riavvio del server. Il server DHCPv6 supporta i tipi DUID a livello di collegamento, ora del livello di collegamento e Enterprise (fornitore assegnato). Si noti che il client deve inviare direttamente il tipo di fornitore DUID. L'opzione per il tipo di fornitore DUID (17) non è supportata direttamente dal server NetX Duo DHPv6.

L'applicazione host del server DHCPv6 dispone di valori predefiniti per l'assegnazione di indirizzi IPv6, incluso il timeout del lease. Per informazioni su come impostare queste opzioni, vedere opzioni configurabili più avanti in questo documento. :

Il blocco di controllo *IANA* contiene i campi T1 e T2. Il blocco *Ia* nel blocco di controllo *IANA* contiene i campi di durata preferiti e validi. Per l'impostazione di queste opzioni, l'applicazione host dispone di opzioni configurabili definite altrove in questo documento. Sono assegnati a tutte le richieste di indirizzi IPv6 del client.

Questi parametri di lease IP DHCPv6 sono definiti di seguito.

T1: tempo in secondi durante il quale il client deve iniziare a rinnovare l'indirizzo IPv6 dal server che lo ha assegnato.

T2: tempo in secondi durante il quale il client deve iniziare a riassociare l'indirizzo IPv6, se il rinnovo non è riuscito, con qualsiasi server nel relativo collegamento.

Durata preferita: tempo in secondi durante il quale l'indirizzo client diventa deprecato se il client non ha rinnovato o riassociato. Il client può comunque utilizzare questo indirizzo.

Durata valida: tempo in secondi durante il quale l'indirizzo IP del client è scaduto e non deve usare questo indirizzo nelle trasmissioni di rete.

La specifica RFC consiglia rispettivamente gli orari T1 e T2, ovvero 0,5 e 0,8, della durata preferita nell'opzione client *IANA* . Se il server non ha alcuna preferenza, impostare queste ore su zero. Se una risposta del server contiene le ore T1 e T2 impostate su zero, consente al client di impostare i relativi orari T1 e T2.

**Vincoli**

Il server DHCPv6 NetX Duo non supporta le opzioni DHCPv6 seguenti:

  - Opzione di commit rapido che consente di ottimizzare il processo di richiesta di indirizzi DHCPv6 solo allo scambio di messaggi di sollecitazione e risposta

  - Riconfigura l'opzione che consente al server di avviare le modifiche allo stato dell'indirizzo IP del client.

  - Opzione unicast; tutti i messaggi client devono essere inviati direttamente al *All_DHCP_Relay_Agents_and_Servers* indirizzo multicast anziché al server DHCPv6.

  - Associazione di identità per l'opzione degli indirizzi temporanei (IA_TA) che è un indirizzo IP temporaneo concesso a un client.

  - Più opzioni IA (indirizzi IPv6) per ogni richiesta client

  - L'host di inoltro tra il client e il server DHCPv6, ad esempio client e server, deve trovarsi nella stessa rete.

  - IPSec e l'autenticazione non sono supportati nella messaggistica DHCPv6. Tuttavia, l'istanza IP può essere abilitata per IPSec a seconda della versione di NetX Duo in uso.

  - Il server DHCPv6 NetX Duo supporta direttamente solo la richiesta di opzione del server DNS. Questo può cambiare nelle versioni future.

  - L'opzione di delega del prefisso non è supportata.

  - Autenticazione dei messaggi DHCPv6 sebbene sia possibile abilitare IPSec nell'ambiente NetX Duo sottostante. Il server DHCPv6 NetX Duo non supporta le connessioni di inoltro ai client. Si presuppone che tutte le richieste client abbiano origine dagli host nella rete del server.

## <a name="netx-duo-dhcpv6-server-callback-functions"></a>Funzioni di callback del server DHCPv6 NetX Duo

*nx_dhcpv6_IP_address_declined_handler*

Quando il client DHCPv6 invia un messaggio di rifiuto, il server DHCPv6 NetX Duo contrassegna l'indirizzo come non disponibile nelle tabelle degli indirizzi IPv6. Per avere la possibilità di personalizzare la gestione del server di questo messaggio, viene fornita la *nx_dhcpv6_IP_address_declined_handler* *.* Questo callback, tuttavia, non è attualmente implementato.

*nx_dhcpv6_server_option_request_handler*

Quando il messaggio del client DHCPv6 contiene i dati di richiesta di opzione, il server DHCPv6 NetX Duo invia ogni codice dell'opzione di richiesta di opzione a questo callback utente, se definito. In questo modo, il server NetX Duo è in grado di consentire al callback definito dall'utente di compilare i dati. Questa funzionalità, tuttavia, non è attualmente implementata.

## <a name="supported-dhcpv6-rfcs"></a>RFC DHCPv6 supportate

NetX Duo DHCPv6 è compatibile con RFC3315, RFC3646 e RFC correlati.