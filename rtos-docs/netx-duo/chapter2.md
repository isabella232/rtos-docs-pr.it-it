---
title: Capitolo 2-installazione e uso di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello stack di rete ad alte prestazioni Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8ee9d16c71d6c207de2098d688d49e6482c8b780
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550151"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo"></a>Capitolo 2-installazione e uso di Azure RTO NetX Duo

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello stack di rete ad alte prestazioni Azure RTO NetX Duo, inclusi i seguenti: 

## <a name="host-considerations"></a>Considerazioni sull'host

Lo sviluppo incorporato viene in genere eseguito nei computer host Windows o Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e il file eseguibile viene generato nell'host, viene scaricato nell'hardware di destinazione per l'esecuzione.

Il download di destinazione viene in genere eseguito dal debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile di fornire il controllo di esecuzione di destinazione (go, Halt, breakpoint e così via), nonché di accedere ai registri della memoria e del processore.

La maggior parte dei debugger dello strumento di sviluppo comunica con l'hardware di destinazione tramite connessioni di debug (OCD) on-chip come JTAG (IEEE 1149,1) e la modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite connessioni di In-Circuit emulazione (ICE). Le connessioni OCD e ICE forniscono soluzioni affidabili con intrusione minima sul software residente di destinazione.

Per quanto riguarda le risorse usate nell'host, il codice sorgente per NetX Duo viene distribuito in formato ASCII e richiede circa 1 MB di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

NetX Duo richiede tra 5 Kbyte e 45 kByte di memoria Read-Only (ROM) nella destinazione. È necessario un altro 5KBytes della memoria ad accesso casuale (RAM) della destinazione per lo stack di thread NetX Duo e altre strutture di dati globali.

Inoltre, NetX Duo richiede l'uso di due oggetti timer ThreadX e di un oggetto mutex ThreadX. Queste funzionalità vengono usate per le esigenze di elaborazione periodica e la protezione dei thread all'interno dello stack del protocollo NetX Duo.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO NetX Duo può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/netxduo/> .

Di seguito è riportato un elenco di diversi file importanti nel repository:

**nx_api. h**  
File di intestazione C contenente tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.

**nx_port. h** File di intestazione C contenente tutte le strutture e le definizioni dei dati dello strumento di sviluppo e del targetspecific. 

**demo_netx. c** File C contenente una piccola applicazione demo.

**NX. a (o NX. lib)**  
Versione binaria della libreria NetX C distribuita con il pacchetto standard.

## <a name="netx-duo-installation"></a>Installazione di NetX Duo

NetX Duo viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository NetX Duo nel PC:

```c
    git clone https://github.com/azure-rtos/netxduo
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.

Sono inoltre disponibili istruzioni per la compilazione della libreria NetX Duo nella pagina iniziale del repository online.

> [!IMPORTANT]
> *Il software applicativo deve accedere al file di libreria NetX Duo (in genere **NX. a** o **NX. lib**) e i file di inclusione C **nx_api. h e nx_port. h**. Questa operazione può essere eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.*

## <a name="using-netx-duo"></a>Uso di NetX Duo

L'uso di NetX Duo è facile. In pratica, il codice dell'applicazione deve includere ***nx_api. h** _ durante la compilazione e il collegamento con la libreria NETX Duo _*_NX. a_*_ (o _ *_NX. lib_*) *.

Di seguito sono riportati i quattro semplici passaggi necessari per creare un'applicazione NetX Duo:

[!div class="mx-tdCol2BreakAll"]

| Passaggio  | Descrizione  |
|---|---|
|Passaggio &nbsp; 1: |Includere il file ***nx_api. h*** in tutti i file dell'applicazione che usano i servizi o le strutture di dati di NETX Duo.|
|Passaggio &nbsp; 2: |Inizializzare il sistema NetX Duo chiamando ***nx_system_initialize** _ dalla funzione _ *_tx_application_define_** o da un thread dell'applicazione.|
|Passaggio &nbsp; 3: |Creare un'istanza IP, abilitare il protocollo ARP (Address Resolution Protocol), se necessario, e i socket dopo la chiamata di ***nx_system_initialize*** .|
|Passaggio &nbsp; 4: |Compilare l'origine e il collegamento dell'applicazione con la libreria di runtime NetX Duo ***NX. a** _ (o _ *_NX. lib_* *). L'immagine risultante può essere scaricata nella destinazione ed eseguita.|

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta NetX Duo viene fornita con una o più dimostrazioni eseguite in una rete effettiva o tramite un driver di rete simulato. È sempre consigliabile che il sistema dimostrativo venga eseguito per primo.

Se il sistema dimostrativo non viene eseguito correttamente, eseguire le operazioni seguenti per restringere il problema:

1. Determinare la quantità della dimostrazione in esecuzione.
2. Aumentare le dimensioni dello stack in qualsiasi nuovo thread dell'applicazione.
3. Ricompilare la libreria NetX Duo con le opzioni di debug appropriate elencate nella sezione opzione di configurazione.
4. Esaminare la struttura NX_IP per verificare se i pacchetti vengono inviati o ricevuti.
5. Esaminare il pool di pacchetti predefinito per verificare se sono presenti pacchetti disponibili.
6. Verificare che il driver di rete fornisca i pacchetti ARP e IP con le relative intestazioni su limiti di 4 byte per le applicazioni che richiedono la connettività IPv4 o IPv6.
7. Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o è stato modificato. Tali informazioni dovrebbero risultare utili per i tecnici del supporto tecnico Microsoft.

Seguire le procedure descritte nella pagina 12 della pagina 12 per inviare le informazioni raccolte dalla procedura di risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione quando si compila la libreria NetX Duo e l'applicazione usando NetX Duo. Le opzioni di configurazione possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file di inclusione ***nx_user. h*** , salvo diversa indicazione.

> [!NOTE]
> *Le opzioni definite in **nx_user. h** vengono applicate solo se l'applicazione e la libreria NETX Duo sono compilate con* **NX_INCLUDE_USER_DEFINE_FILE** definito. *

Nelle sezioni seguenti sono elencate le opzioni di configurazione disponibili in NetX Duo. Le opzioni generali applicabili sia a IPv4 sia a IPv6 sono elencate per prime, seguite dalle opzioni specifiche di IPv6.

### <a name="system-configuration-options"></a>Opzioni di configurazione del sistema

| Opzione  | Descrizione  |
|---|---|
| NX_ASSERT_FAIL    | Simbolo che definisce l'istruzione di debug da utilizzare in caso di esito negativo di un'asserzione.                               |
| NX_DEBUG           | Definito, Abilita le informazioni di debug di stampa facoltative disponibili dal driver di rete Ethernet RAM. |
| NX_DEBUG_PACKET   | Definito, Abilita il dump del pacchetto di debug facoltativo disponibile nel driver di rete Ethernet RAM.      |
| NX_DISABLE_ASSERT | Definito, Disabilita i controlli ASSERT nel codice sorgente. Per impostazione predefinita, questa opzione non è definita.            |
|NX_DISABLE_ERROR_CHECKING | Definito, rimuove l'API di base per il controllo degli errori di NetX Duo e migliora le prestazioni. I codici restituiti dell'API non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella definizione dell'API. Questa definizione viene in genere utilizzata dopo che l'applicazione è stata sottoposta a debug sufficiente e il suo utilizzo migliora le prestazioni e riduce le dimensioni del codice.|
|NX_DRIVER_DEFERRED_PROCESSING | Definito, Abilita la gestione dei pacchetti del driver di rete posticipata. In questo modo, il driver di rete può inserire un pacchetto nell'istanza IP e fare in modo che la routine di elaborazione reale venga chiamata dal thread di supporto IP interno di NetX Duo.|
|NX_DUAL_PACKET_POOL_ENABLE | Rinominato in ***NX_ENABLE_DUAL_PACKET_POOL** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ENABLE_DUAL_PACKET_POOL_* *.|
|NX_ENABLE_DUAL_PACKET_POOL | Definito consente allo stack di usare due pool di pacchetti, uno con dimensioni del payload elevate e uno con dimensioni del payload inferiori. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_EXTENDED_NOTIFY_SUPPORT| Definito, Abilita più hook di callback nello stack. Queste funzioni di callback vengono usate dal livello wrapper BSD. Per impostazione predefinita, questa opzione non è definita.|
|NX_ENABLE_INTERFACE_CAPABILITY| Definito, consente al driver di dispositivo di interfaccia di specificare informazioni aggiuntive sulla capacità, ad esempio il caricamento di checksum. Per impostazione predefinita, questa opzione non è definita.|
|NX_ENABLE_SOURCE_ADDRESS_CHECK| Definito, consente di controllare l'indirizzo di origine del pacchetto in ingresso. Per impostazione predefinita, questa opzione è disabilitata.|
| NX_IPSEC_ENABLE  | Definito, Abilita la libreria NetX Duo per supportare le operazioni IPsec. Questa funzionalità richiede il modulo facoltativo NetX Duo IPsec. Per impostazione predefinita, questa funzionalità non è abilitata.            |
| NX_LITTLE_ENDIAN | Definito, esegue lo scambio di byte necessario negli ambienti little endian per assicurarsi che le intestazioni di protocollo siano nel formato big endian appropriato. Si noti che il valore predefinito è in genere configurato in ***nx_port. h***.|
|NX_MAX_PHYSICAL_INTERFACES | Specifica il numero totale di interfacce di rete fisiche nel dispositivo. Il valore predefinito è 1 ed è definito in ***nx_api. h***; un dispositivo deve avere almeno un'interfaccia fisica. Si noti che non include l'interfaccia di loopback.|
| NX_NAT_ENABLE | Definito, NetX Duo è compilato con il processo NAT. Per impostazione predefinita, questa opzione non è definita.|
| NX_PHYSICAL_HEADER  | Specifica la dimensione in byte dell'intestazione fisica del frame. Il valore predefinito è 16 (basato su un tipico frame Ethernet a 14 byte allineato al limite di 32 bit) ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima di includere _*_nx_api. h_*_ , ad esempio in _ *_nx_user. h_*. * |
| NX_PHYSICAL_TRAILER | Specifica la dimensione in byte del trailer del pacchetto fisico e viene in genere usata per riservare spazio di archiviazione per elementi come CRC Ethernet e così via. Il valore predefinito è 4 ed è definito in ***nx_api. h***.|

### <a name="arp-configuration-options"></a>Opzioni di configurazione ARP

| Opzione  | Descrizione  |
|---|---|
|NX_ARP_DEFEND_BY_REPLY | Definito, consente a NetX duo di difendere il proprio indirizzo IP inviando una risposta ARP.|
|NX_ARP_DEFEND_INTERVAL| Definisce l'intervallo in secondi durante il quale il modulo ARP invia il successivo pacchetto di difesa in risposta a un messaggio ARP in arrivo che indica un indirizzo in conflitto.|
|NX_ARP_DISABLE_AUTO_ARP_ENTRY|  Rinominato in ***NX_DISABLE_ARP_AUTO_ENTRY** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_ARP_AUTO_ENTRY_* *.|
|NX_ARP_EXPIRATION_RATE| Specifica il numero di secondi per cui le voci ARP restano valide. Il valore predefinito zero disabilita la scadenza o l'invecchiamento delle voci ARP ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_ARP_MAC_CHANGE_NOTIFICATION_ENABLE | Rinominato in ***NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION_* *.|
|NX_ARP_MAX_QUEUE_DEPTH | Specifica il numero massimo di pacchetti che possono essere accodati in attesa di una risposta ARP. Il valore predefinito è 4 ed è definito in ***nx_api. h***.|
|NX_ARP_MAXIMUM_RETRIES | Specifica il numero massimo di tentativi ARP eseguiti senza una risposta ARP. Il valore predefinito è 18 ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_ARP_UPDATE_RATE | Specifica il numero di secondi tra i tentativi ARP. Il valore predefinito è 10, che rappresenta 10 secondi, ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_DISABLE_ARP_AUTO_ENTRY | Definito, Disabilita l'immissione delle informazioni sulla richiesta ARP nella cache ARP.|
|NX_DISABLE_ARP_INFO | Definito, Disabilita la raccolta di informazioni ARP.|
|NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION| Definito, consente a ARP di richiamare una funzione di notifica di callback al rilevamento dell'indirizzo MAC aggiornato.|

### <a name="icmp-configuration-options"></a>Opzioni di configurazione ICMP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_ICMP_INFO| Definito, Disabilita la raccolta di informazioni ICMP.|
|NX_DISABLE_ICMP_RX_CHECKSUM| Definito, Disabilita sia il calcolo di checksum ICMPv4 che ICMPv6 sui pacchetti ICMP ricevuti. Questa opzione è utile quando il driver dell'interfaccia di rete è in grado di verificare il checksum ICMPv4 e ICMPv6 e l'applicazione non usa la funzionalità di frammentazione IP o la funzionalità IPsec. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMP_TX_CHECKSUM | Definito, Disabilita sia il calcolo di checksum ICMPv4 che ICMPv6 sui pacchetti ICMP trasmessi. Questa opzione è utile quando il driver dell'interfaccia di rete è in grado di calcolare il checksum ICMPv4 e ICMPv6,
e l'applicazione non utilizza la funzionalità di frammentazione IP o la funzionalità IPsec. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMPV4_ERROR_MESSAGE | Definito, NetX Duo non invia messaggi di errore ICMPv4 in risposta a condizioni di errore, ad esempio un'intestazione IPv4 formattata in modo errato. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMPV4_RX_CHECKSUM | Definito, Disabilita il calcolo del checksum ICMPv4 nei pacchetti ICMP ricevuti. Questa opzione viene definita automaticamente se ***NX_DISABLE_ICMP_RX_CHECKSUM*** è definito. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMPv4_RX_CHECKSUM | Rinominato in ***NX_DISABLE_ICMPV4_RX_CHECKSUM** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_ICMPV4_RX_CHECKSUM_* *.|
|NX_DISABLE_ICMPV4_TX_CHECKSUM | Definito, Disabilita il calcolo del checksum ICMPv4 sui pacchetti ICMP trasmessi. Questa opzione viene definita automaticamente se ***NX_DISABLE_ICMP_TX_CHECKSUM*** è definito. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMPv4_TX_CHECKSUM | Rinominato in ***NX_DISABLE_ICMPV4_TX_CHECKSUM** _.</br>Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_ICMPV4_TX_CHECKSUM_* *.|
|NX_ENABLE_ICMP_ADDRESS_CHECK | Definito, l'indirizzo di destinazione del pacchetto ICMP è selezionato. L'impostazione predefinita è disabilitata. Una richiesta echo ICMP destinata a un indirizzo IP broadcast o multicast IP verrà ignorata automaticamente.|

### <a name="igmp-configuration-options"></a>Opzioni di configurazione IGMP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_IGMP_INFO | Definito, Disabilita la raccolta di informazioni IGMP.|
|NX_DISABLE_IGMPV2 | Definisce, Disabilita il supporto IGMPv2 e NetX Duo supporta solo IGMPv1. Per impostazione predefinita, questa opzione non è impostata ed è definita in ***nx_api. h***.|
|NX_MAX_MULTICAST_GROUPS | Specifica il numero massimo di gruppi multicast che è possibile unire in join. Il valore predefinito è 7 ed è definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|

### <a name="ip-configuration-options"></a>Opzioni di configurazione IP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_FRAGMENTATION | Definito, Disabilita sia la frammentazione sia IPv4 che IPv6 e la logica di riassemblaggio.|
| NX_DISABLE_IPV4     | Definito, Disabilita la funzionalità IPv4. Questa opzione può essere usata per compilare solo NetX Duo in suupport IPv6. Per impostazione predefinita, questa opzione non è definita. |
| NX_DISABLE_IP_INFO | Definito, Disabilita la raccolta di informazioni IP.|
|NX_DISABLE_IP_RX_CHECKSUM | Definito, Disabilita la logica di checksum nei pacchetti IPv4 ricevuti. Questa operazione è utile se il dispositivo di rete è in grado di verificare il checksum IPv4 e l'applicazione non prevede l'utilizzo della frammentazione IP o IPsec.|
|NX_DISABLE_IP_TX_CHECKSUM | Definito, Disabilita la logica di checksum sui pacchetti IPv4 inviati. Questa operazione è utile nelle situazioni in cui il dispositivo di rete sottostante è in grado di generare il checksum dell'intestazione IPv4 e l'applicazione non prevede di utilizzare la frammentazione IP o IPsec.|
|NX_DISABLE_LOOPBACK_INTERFACE | Definito, Disabilita il supporto di NetX Duo per l'interfaccia di loopback.|
|NX_DISABLE_RX_SIZE_CHECKING | Definito, Disabilita il controllo delle dimensioni sui pacchetti ricevuti.|
|NX_ENABLE_IP_RAW_PACKET_FILTER | Definito, Abilita la funzionalità di filtro di ricezione di pacchetti non elaborati IP. Le applicazioni che richiedono un maggiore controllo sul tipo di pacchetti IP non elaborati da ricevere possono usare questa funzionalità. La funzionalità di filtro dei pacchetti non elaborati IP supporta anche l'operazione socket non elaborata nel livello di compatibilità BSD. Per impostazione predefinita, questa opzione non è definita.|
|NX_ENABLE_IP_STATIC_ROUTING | Definito, Abilita il routing statico IPv4 in cui a un indirizzo di destinazione può essere assegnato un indirizzo hop successivo specifico. Per impostazione predefinita, il routing statico IPv4 è disabilitato.|
|NX_FRAGMENT_IMMEDIATE_ASSEMBLY | Definito consente di eseguire immediatamente la logica di riassemblaggio IPv4 e IPv6 dopo la ricezione di un frammento IP. Per impostazione predefinita, questa opzione non è definita.|
|NX_IP_MAX_REASSEMBLY_TIME | Simbolo che controlla il tempo massimo consentito per riassemblare il frammento IPv4 e il frammento IPv6. Si noti che il valore definito qui sovrascrive sia ***NX_IPV4_MAX_REASSEMBLY_TIME** _ che _ *_NX_IPV6_MAX_REASSEMBLY_TIME_* *.|
|NX_IP_PERIODIC_RATE | Definito, specifica il numero di cicli del timer ThreadX in un secondo. Il valore predefinito è derivato dal simbolo ThreadX ***TX_TIMER_TICKS_PER_SECOND, _,** che per impostazione predefinita è impostato su 100 (timer 10 ms). Le applicazioni devono prestare attenzione quando si modifica questo valore, poiché il resto dei moduli NetX Duo derivano le informazioni sulla temporizzazione da _ *_NX_IP_PERIODIC_RATE_.**|
|NX_IP_RAW_MAX_QUEUE_DEPTH | Il simbolo che controlla il numero di pacchetti IP non elaborati può essere accodato nella coda di ricezione pacchetti non elaborati. Per impostazione predefinita, il valore è impostato su 20.| 
|NX_IP_ROUTING_TABLE_SIZE | Definito, imposta il numero massimo di voci nella tabella di routing statica IPv4, ovvero un elenco di un'interfaccia in uscita e gli indirizzi hop successivi per un indirizzo di destinazione specificato. Il valore predefinito è 8 ed è definito in ***nx_api. h.** _ Questo simbolo viene utilizzato solo se _ *_NX_ENABLE_IP_STATIC_ROUTING_** è definito.|
|NX_IPV4_MAX_REASSEMBLY_TIME | Simbolo che controlla il tempo massimo consentito per riassemblare il frammento IPv4. Si noti che il valore definito in NX_IP_MAX_REASSEMBLY_TIME sovrascrive questo valore.|

### <a name="packet-configuration-options"></a>Opzioni di configurazione pacchetti

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_PACKET_CHAIN | Definito, Disabilita la logica della catena di pacchetti. Per impostazione predefinita, questo valore non è definito.|
|NX_DISABLE_PACKET_INFO | Definito, Disabilita la raccolta di informazioni sul pool di pacchetti.|
|NX_ENABLE_LOW_WATERMARK | Definito, Abilita la funzionalità limite minimo del pool di pacchetti NetX Duo. L'applicazione imposta un valore limite minimo. Alla ricezione di pacchetti TCP, se viene raggiunto il limite minimo per il pool di pacchetti, NetX Duo Elimina automaticamente il pacchetto, rilasciandolo, impedendo la scadenza del pool di pacchetti. Per impostazione predefinita, questa funzionalità non è abilitata.|
|NX_ENABLE_PACKET_DEBUG_INFO | Definito, registra le informazioni di debug del pacchetto.|
|NX_PACKET_ALIGNMENT | Definito, specifica il requisito di allineamento, in byte, per l'indirizzo iniziale dell'area del payload del pacchetto. Questa opzione depreca ***NX_PACKET_HEADER_PAD** _ e _ *_NX_PACKET_HEADER_PAD_SIZE_* *. Per impostazione predefinita, questa opzione è definita come 4, rendendo allineato l'indirizzo iniziale dell'area di payload a 4 byte.|
|NX_PACKET_HEADER_PAD | Definito, Abilita la spaziatura interna verso la fine del blocco di controllo NX_PACKET. Il numero di parole ULONG da riempire è definito da ***NX_PACKET_HEADER_PAD_SIZE** _. Nota Questa opzione è stata ammortizzata da _ *_NX_PACKET_ALIGNMENT_* *.|
|NX_PACKET_HEADER_PAD_SIZE | Imposta il numero di parole ULONG da riempire alla struttura NX_PACKET, consentendo all'area del payload del pacchetto di iniziare dall'allineamento desiderato. Questa funzionalità è utile quando i descrittori del buffer di ricezione puntano direttamente all'area del payload NX_PACKET e la logica di ricezione dell'interfaccia di rete o la logica dell'operazione della cache prevede che l'indirizzo iniziale del buffer soddisfi determinati requisiti di allineamento. Questo valore diventa valido solo quando ***NX_PACKET_HEADER_PAD** _ è definito. Nota Questa opzione è deprecata da _ *_NX_PACKET_ALIGNMENT_* *.|

### <a name="rarp-configuration-options"></a>Opzioni di configurazione di RARP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_RARP_INFO | Definito, Disabilita la raccolta di informazioni di RARP.|

### <a name="tcp-configuration-options"></a>Opzioni di configurazione TCP

| Opzione | Descrizione |
|---|---|
|NX_DISABLE_RESET_DISCONNECT | Definito, Disabilita l'elaborazione della reimpostazione durante la disconnessione quando il valore di timeout specificato viene specificato come ***NX_NO_WAIT***.|
|NX_DISABLE_TCP_INFO | Definito, Disabilita la raccolta di informazioni TCP.|
|NX_DISABLE_TCP_RX_CHECKSUM | Definito, Disabilita la logica di checksum nei pacchetti TCP ricevuti. Questa operazione è utile solo nelle situazioni in cui il livello di collegamento presenta un'elaborazione affidabile di checksum o CRC oppure il driver di interfaccia è in grado di verificare il checksum TCP nell'hardware e l'applicazione non utilizza IPsec.|
|NX_DISABLE_TCP_TX_CHECKSUM | Definito, Disabilita la logica di checksum per l'invio di pacchetti TCP. Questa operazione è utile solo nelle situazioni in cui il nodo di rete ricevente ha ricevuto la logica di checksum TCP disabilitata o se il driver di rete sottostante è in grado di generare il checksum TCP e l'applicazione non usa IPsec.|
|NX_ENABLE_TCP_KEEPALIVE | Definito, Abilita il timer TCP keepalive facoltativo. Le impostazioni predefinite non sono abilitate.|
|NX_ENABLE_TCP_MSS_CHECK | Definito, Abilita la verifica del peer MSS minimo prima di accettare una connessione TCP. Per usare questa funzionalità, è necessario definire il simbolo ***NX_ENABLE_TCP_MSS_MINIMUM*** . Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY| Definito, consente all'applicazione di installare una funzione di callback che viene richiamata quando la profondità della coda di trasmissione TCP non è più al valore massimo. Questo callback funge da indicazione che il socket TCP è pronto per la trasmissione di più dati. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_TCP_WINDOW_SCALING | Abilita l'opzione di scalabilità della finestra per le applicazioni TCP. Se definito, l'opzione di scalabilità della finestra viene negoziata durante la fase di connessione TCP e l'applicazione è in grado di specificare una dimensione della finestra maggiore di 64K. L'impostazione predefinita non è abilitata (non definita).|
|NX_MAX_LISTEN_REQUESTS | Specifica il numero massimo di richieste di ascolto del server. Il valore predefinito è 10 e viene definito in ***nx_api. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_ACK_EVERY_N_PACKETS | Specifica il numero di pacchetti TCP da ricevere prima di inviare un ACK. Nota Se ***NX_TCP_IMMEDIATE_ACK** _ è abilitato ma _ *_NX_TCP_ACK_EVERY_N_PACKETS_** non è, questo valore viene impostato automaticamente su 1 per la compatibilità con le versioni precedenti.|
|NX_TCP_ACK_TIMER_RATE | Specifica il modo in cui il numero di cicli di sistema (NX_IP_PERIODIC_RATE) viene diviso per calcolare la frequenza del timer per l'elaborazione ACK ritardata TCP. Il valore predefinito è 5, che rappresenta 200ms, ed è definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_ENABLE_KEEPALIVE | Rinominato in ***NX_ENABLE_TCP_KEEPALIVE** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ENABLE_TCP_KEEPALIVE_* *.|
|NX_TCP_ENABLE_MSS_CHECK | Rinominato in ***NX_ENABLE_TCP_MSS_CHECK** _. Anche se è ancora supportata, è consigliabile usare _ NX_ENABLE_TCP_MSS_CHECK per i nuovi progetti *_._**|
|NX_TCP_ENABLE_WINDOW_SCALING | Rinominato in ***NX_ENABLE_TCP_WINDOW_SCALING** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ENABLE_TCP_WINDOW_SCALING_* *.|
|NX_TCP_FAST_TIMER_RATE | Specifica il modo in cui viene diviso il numero di cicli interni di NetX Duo (NX_IP_PERIODIC_RATE) per calcolare la velocità del timer TCP veloce. Il timer TCP veloce viene usato per guidare i vari timer TCP, incluso il timer ACK ritardato. Il valore predefinito è 10, che rappresenta 100 MS presumendo che il timer ThreadX sia in esecuzione in 10 ms. Questo valore è definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_IMMEDIATE_ACK| Definito, Abilita l'elaborazione facoltativa della risposta ACK immediata TCP. La definizione di questo simbolo equivale alla definizione di  ***NX_TCP_ACK_EVERY_N_PACKETS*** come 1.|
|NX_TCP_KEEPALIVE_INITIAL | Specifica il numero di secondi di inattività prima dell'attivazione del timer KeepAlive. Il valore predefinito è 7200, che rappresenta 2 ore, ed è definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_KEEPALIVE_RETRIES | Specifica il numero di tentativi KeepAlive consentiti prima che la connessione venga considerata interruppe. Il valore predefinito è 10, che rappresenta 10 tentativi e viene definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_KEEPALIVE_RETRY | Specifica il numero di secondi tra i tentativi del timer KeepAlive, presumendo che l'altro lato della connessione non stia rispondendo. Il valore predefinito è 75, che rappresenta 75 secondi tra i tentativi e viene definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_MAX_OUT_OF_ORDER_PACKETS | Simbolo che definisce il numero massimo di pacchetti TCP non ordinati che è possibile mantenere nella coda di ricezione socket TCP. Questo simbolo può essere utilizzato per limitare il numero di pacchetti accodati nel socket di ricezione TCP, evitando che il pool di pacchetti venga esaurito. Per impostazione predefinita, questo simbolo non è definito, pertanto non esiste alcun limite al numero di pacchetti non ordinati accodati nel socket TCP.|
|NX_TCP_MAXIMUM_RETRIES | Specifica il numero di tentativi di trasmissione dati consentiti prima che la connessione venga considerata interruppe. Il valore predefinito è 10, che rappresenta 10 tentativi e viene definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_MAXIMUM_RX_QUEUE | Simbolo che definisce la coda di ricezione massima per i socket TCP. Questa funzionalità è abilitata dal ***NX_ENABLE_LOW_WATERMARK***.|
|NX_TCP_MAXIMUM_TX_QUEUE | Specifica la profondità massima della coda di trasmissione TCP prima della sospensione o del rifiuto delle richieste di invio TCP. Il valore predefinito è 20, il che significa che un massimo di 20 pacchetti può trovarsi nella coda di trasmissione in un determinato momento. Si noti che i pacchetti vengono mantenuti nella coda di trasmissione fino a quando non viene ricevuto un ACK che copre alcuni o tutti i dati del pacchetto dall'altro lato della connessione. Questa costante è definita in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_MSS_MINIMUM | Simbolo che definisce il valore minimo MSS del modulo NetX Duo TCP accettato. Questa funzionalità è abilitata dal ***NX_ENABLE_TCP_MSS_CHECK***.|
|NX_TCP_QUEUE_DEPTH_UPDATE_NOTIFY_ENABLE | Rinominato in ***NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY_* *.|
|NX_TCP_RETRY_SHIFT | Specifica la modalità di modifica del periodo di timeout di ritrasmissione tra i tentativi. Se questo valore è 0, il timeout di ritrasmissione iniziale è uguale a quello dei successivi timeout di ritrasmissione. Se questo valore è 1, ogni ritrasmissione successiva è due volte più lungo. Se questo valore è 2, ogni timeout di ritrasmissione successivo è quattro volte più lungo. Il valore predefinito è 0 ed è definito in ***nx_tcp. h** _. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|
|NX_TCP_TRANSMIT_TIMER_RATE | Specifica il modo in cui il numero di cicli di sistema (***NX_IP_PERIODIC_RATE** _) viene diviso per calcolare la frequenza del timer per l'elaborazione dei tentativi di trasmissione TCP. Il valore predefinito è 1, che rappresenta 1 secondo, ed è definito in _*_nx_tcp. h_*_. L'applicazione può eseguire l'override dell'impostazione predefinita definendo il valore prima dell'inclusione di _ *_nx_api. h_**.|

### <a name="udp-configuration-options"></a>Opzioni di configurazione UDP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_UDP_INFO | Definito, Disabilita la raccolta di informazioni UDP.|
|NX_DISABLE_UDP_RX_CHECKSUM | Definito, Disabilita il calcolo del checksum UDP sui pacchetti UDP in ingresso. Questa operazione è utile se il driver dell'interfaccia di rete è in grado di verificare il checksum dell'intestazione UDP nell'hardware e l'applicazione non Abilita la logica di frammentazione IPsec o IP.|
|NX_DISABLE_UDP_TX_CHECKSUM | Definito, Disabilita il calcolo del checksum UDP nei pacchetti UDP in uscita. Questa operazione è utile se il driver dell'interfaccia di rete è in grado di calcolare il checksum dell'intestazione UDP e di inserire il valore nell'intestazione IP prima di trasmettere i dati e l'applicazione non Abilita la logica di frammentazione IP o IPsec.|

### <a name="ipv6-options"></a>Opzioni IPv6  

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_IPV6 | Disabilita la funzionalità IPv6 quando viene compilata la libreria NetX Duo. Per le applicazioni che non necessitano di IPv6, in questo modo si evita il pull del codice e lo spazio di archiviazione aggiuntivo necessario per supportare IPv6.|
|NX_DISABLE_IPV6_PATH_MTU_DISCOVERY | Definito, Disabilita il percorso MTU Discovery, che viene usato per determinare la MTU massima nel percorso di una destinazione nella tabella di destinazione dell'host NetX Duo. Questo consente all'host NetX duo di inviare il pacchetto più grande possibile che non richiede la frammentazione. Per impostazione predefinita, questa opzione è definita (il percorso MTU è disabilitato).|
|NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY | Definito, consente di richiamare una funzione di callback quando viene modificato l'indirizzo IPv6. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_IPV6_MULTICAST | Definito, Abilita la funzione di join/uscita multicast IPv6. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_IPV6_PATH_MTU_DISCOVERY | Definito, Abilita la funzionalità di individuazione MTU del percorso IPv6. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_IPV6_ADDRESS_CHANGE_NOTIFY_ENABLE | Rinominato in ***NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY_* *.|
|NX_IPV6_DEFAULT_ROUTER_TABLE_SIZE | Specifica il numero di voci nella tabella di routing IPv6. Per il router predefinito è necessaria almeno la voce onS. Definito in ***nx_api. h***, il valore predefinito è 8.|
|NX_IPV6_DESTINATION_TABLE_SIZE | Specifica il numero di voci nella tabella di destinazione IPv6. Archivia le informazioni sugli indirizzi hop successivi per gli indirizzi IPv6. Definito in ***nx_api. h***, il valore predefinito è 8.|
|NX_IPV6_MAX_REASSEMBLY_TIME | Simbolo che controlla il tempo massimo consentito per riassemblare il frammento IPv6.|
|NX_IPV6_MULTICAST_ENABLE | Rinominato in ***NX_ENABLE_IPV6_MULTICAST** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ENABLE_IPV6_MULTICAST_* *.|
|NX_IPV6_PREFIX_LIST_TABLE_SIZE | Specifica le dimensioni della tabella dei prefissi. Le informazioni sul prefisso vengono ottenute dagli annunci router e fanno parte della configurazione degli indirizzi IPv6. Definito in ***nx_api. h***, il valore predefinito è 8.|
|NX_IPV6_STATELESS_AUTOCONFIG_CONTROL | Definito consente a NetX duo di disabilitare la funzionalità di configurazione automatica degli indirizzi senza stato. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_MAX_IPV6_ADDRESSES | Specifica il numero di voci nel pool di indirizzi IPv6. Durante la configurazione dell'interfaccia, NetX Duo usa le voci IPv6 del pool. Il valore predefinito è (NX_MAX_PHYSICAL_INTERFACES \* 3) per consentire a ogni interfaccia di avere almeno un indirizzo locale collegamento e due indirizzi globali. Si noti che tutte le interfacce condividono il pool di indirizzi IPv6.|
|NX_PATH_MTU_INCREASE_WAIT_INTERVAL | Specifica l'intervallo di attesa nei cicli del timer per reimpostare il valore MTU del percorso per una destinazione specifica nella tabella di destinazione. Se ***NX_DISABLE_IPV6_PATH_MTU_DISCOVERY*** è definito, la definizione di questo simbolo non ha alcun effetto.|
|NX_PATH_MTU_INCREASE_WAIT_INTERVAL | Simbolo che specifica l'intervallo di attesa (in secondi) per la reimpostazione del valore MTU del percorso per una voce della tabella di destinazione. È valido solo se viene definito ***NX_ENABLE_IPV6_PATH_MTU_DISCOVERY*** . Per impostazione predefinita, questo valore è impostato su 600 (secondi).|

### <a name="neighbor-cache-configuration-options"></a>Opzioni di configurazione della cache Neighbor

| Opzione  | Descrizione  |
|---|---|
|NX_DELAY_FIRST_PROBE_TIME | Specifica il ritardo in secondi prima che la prima richiesta venga inviata per una voce della cache nello stato non aggiornato. Definito in ***nx_nd_cache. h***, il valore predefinito è 5.|
|NX_DISABLE_IPV6_DAD | Definita, questa opzione Disabilita il rilevamento degli indirizzi duplicati (DAD) durante l'assegnazione degli indirizzi IPv6. Gli indirizzi vengono impostati mediante configurazione manuale o tramite la configurazione automatica degli indirizzi senza stato.|
|NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES | Definita, questa opzione impedisce a NetX duo di rimuovere le voci della tabella della cache meno recenti prima della scadenza del timeout per creare spazio per le nuove voci quando la tabella è piena. Le voci statiche e del router non vengono mai eliminate.|
|NX_IPV6_DAD_TRANSMITS | Specifica il numero di messaggi di richiesta adiacenti da inviare prima che NetX Duo contrassegni un indirizzo di interfaccia come valido. Se ***NX_DISABLE_IPV6_DAD** _ è definito (il padre è disabilitato), l'impostazione di questa opzione non ha alcun effetto. In alternativa, un valore pari a zero (0) disattiva il padre ma lascia la funzionalità DAD in NetX Duo. Definito in _ *_nx_api. h_* *, il valore predefinito è 3.|
|NX_IPV6_DISABLE_PURGE_UNUSED_CACHE_ENTRIES | Rinominato in ***NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES_* *.|
|NX_IPV6_NEIGHBOR_CACHE_SIZE | Specifica il numero di voci nella tabella della cache del router adiacente IPv6. Definito in ***nx_nd_cache. h***, il valore predefinito è 16.|
|NX_MAX_MULTICAST_SOLICIT | Specifica il numero di messaggi di richiesta adiacenti che NetX duo trasmette come parte del protocollo di individuazione router adiacenti IPv6 quando è richiesto il mapping tra l'indirizzo IPv6 e l'indirizzo MAC. Definito in ***nx_nd_cache. h***, il valore predefinito è 3.|
|NX_MAX_UNICAST_SOLICIT | Specifica il numero di messaggi di richiesta adiacenti che NetX duo trasmette per determinare la raggiungibilità di un router adiacente specifico. Definito in ***nx_nd_cache. h***, il valore predefinito è 3.|
|NX_ND_MAX_QUEUE_DEPTH | Simbolo che definisce il numero massimo di pacchetti accodati per la cache ND da risolvere. Per impostazione predefinita, questo simbolo è impostato su 4.|
|NX_REACHABLE_TIME | Specifica il timeout in secondi per l'esistenza di una voce della cache nello stato raggiungibile senza pacchetti ricevuti dall'indirizzo IPv6 della destinazione della cache. Definito in ***nx_nd_cache. h***, il valore predefinito è 30.|
|NX_RETRANS_TIMER  | Specifica in millisecondi la lunghezza di ritardo tra i pacchetti di richiesta inviati da NetX Duo. Definito in ***nx_nd_cache. h***, il valore predefinito è 1000.|
| NXDUO_DISABLE_DAD | Rinominato in ***NX_DISABLE_IPV6_DAD** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_IPV6_DAD_* *.|
|NXDUO_DUP_ADDR_DETECT_TRANSMITS | Rinominato in ***NX_IPV6_DAD_TRANSMITS** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_IPV6_DAD_TRANSMITS_* *.|

### <a name="miscellaneous-icmpv6-configuration-options"></a>Opzioni di configurazione ICMPv6 varie

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_ICMPV6_ERROR_MESSAGE | Definito, Disabilita NetX Duo dall'invio di un messaggio di errore ICMPv6 in risposta a un pacchetto di problema (ad esempio, l'intestazione formattata in modo errato o il tipo di intestazione del pacchetto è deprecato) ricevuto da un altro host.|
|NX_DISABLE_ICMPV6_REDIRECT_PROCESS | Definito, Disabilita l'elaborazione dei pacchetti di reindirizzamento ICMPv6. NetX Duo, per impostazione predefinita, elabora i messaggi di reindirizzamento e aggiorna la tabella di destinazione con le informazioni sull'indirizzo IP dell'hop successivo.|
|NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS | Definito, Disabilita NetX Duo dalle informazioni di elaborazione ricevute nei pacchetti di annunci router IPv6.|
|NX_DISABLE_ICMPV6_ROUTER_SOLICITATION | Definito, Disabilita NetX Duo dall'invio di messaggi di richiesta router IPv6 a intervalli regolari al router.|
|NX_DISABLE_ICMPV6_RX_CHECKSUM | Definito, Disabilita il calcolo del checksum ICMPv6 nei pacchetti ICMP ricevuti.|
|NX_DISABLE_ICMPv6_RX_CHECKSUM | Rinominato in ***NX_DISABLE_ICMPV6_RX_CHECKSUM** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_CMPV6_RX_CHECKSUM_* *.|
|NX_DISABLE_ICMPV6_TX_CHECKSUM | Definito, Disabilita e calcolo di checksum ICMPv6 sui pacchetti ICMP trasmessi.|
|NX_DISABLE_ICMPV6_TX_CHECKSUM | Rinominato in ***NX_DISABLE_ICMPV6_TX_CHECKSUM** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_ICMPV6_TX_CHECKSUM_* *.|
|NX_ICMPV6_MAX_RTR_SOLICITATIONS | Definire il numero massimo di richieste router inviate da un host fino a quando non viene ricevuta una risposta router. Se non viene ricevuta alcuna risposta, l'host conclude che non è presente alcun router. Il valore predefinito è 3.|
|NX_ICMPV6_RTR_SOLICITATION_DELAY | Specifica il ritardo massimo in secondi per la richiesta del router iniziale.|
|NX_ICMPV6_RTR_SOLICITATION_INTERVAL | Specifica l'intervallo tra due messaggi di richiesta router. Il valore predefinito è 4.|
|NXDUO_DESTINATION_TABLE_SIZE | Rinominato in ***NX_IPV6_DESTINATION_TABLE_SIZE** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_IPV6_DESTINATION_TABLE_SIZE_* *.|
|NXDUO_DISABLE_ICMPV6_ERROR_MESSAGE | Rinominato in ***NX_DISABLE_ICMPV6_ERROR_MESSAGE** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_ICMPV6_ERROR_MESSAGE_* *.|
|NXDUO_DISABLE_ICMPV6_REDIRECT_PROCESS | Rinominato in ***NX_DISABLE_ICMPV6_REDIRECT_PROCESS** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_ICMPV6_REDIRECT_PROCESS_**|  
|NXDUO_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS| Rinominato in ***NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS_* *.|
|NXDUO_DISABLE_ICMPV6_ROUTER_SOLICITATION | Rinominato in ***NX_DISABLE_ICMPV6_ROUTER_SOLICITATION** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_DISABLE_ICMPV6_ROUTER_SOLICITATION_* *.|
|NXDUO_ICMPV6_MAX_RTR_SOLICITATIONS | Rinominato in ***NX_ICMPV6_MAX_RTR_SOLICITATIONS** _. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ICMPV6_MAX_RTR_SOLICITATIONS_* *.|
|NXDUO_ICMPV6_RTR_SOLICITATION_INTERVAL | Rinominato in ***NX_ICMPV6_RTR_SOLICITATION_INTERVAL** _. Questo simbolo viene ammortizzato. Sebbene sia ancora supportato, è consigliabile usare i nuovi progetti _ *_NX_ICMPV6_RTR_SOLICITATION_INTERVAL_**|

## <a name="netx-duo-version-id"></a>ID versione di NetX Duo

La versione corrente di NetX Duo è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. È possibile ottenere la versione di NetX Duo dall'esame del file **nx_port. h** . Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di NETX Duo esaminando la stringa globale _* *_nx_version_id_*_ in _ *_nx_port. h_* *.

Il software applicativo può inoltre ottenere informazioni sulla versione dalle costanti indicate di seguito definite in ***nx_api. h***.

Queste costanti identificano la versione corrente del prodotto in base al nome e alla versione principale e secondaria del prodotto.

\#definire EL_PRODUCT_NETXDUO  
\#definire NETXDUO_MAJOR_VERSION  
\#definire NETXDUO_MINOR_VERSION