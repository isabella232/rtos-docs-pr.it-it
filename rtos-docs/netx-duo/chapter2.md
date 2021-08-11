---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX Duo
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello stack di rete ad alte prestazioni Azure RTOS NetX Duo.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 32a9efaac3c85d415316fba2e9536cc40939f1f6debcbe3e2fa588de613a694d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788831"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo"></a>Capitolo 2 - Installazione e uso di Azure RTOS NetX Duo

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso dello stack di rete ad alte prestazioni Azure RTOS NetX Duo, inclusi i seguenti: 

## <a name="host-considerations"></a>Considerazioni sull'host

Lo sviluppo incorporato viene in genere eseguito in Windows o nei computer host Linux (Unix). Dopo la compilazione, il collegamento e la generazione dell'eseguibile nell'host, l'applicazione viene scaricata nell'hardware di destinazione per l'esecuzione.

In genere il download di destinazione viene eseguito dall'interno del debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile di fornire il controllo dell'esecuzione di destinazione (go, halt, breakpoint e così via), nonché l'accesso ai registri della memoria e del processore.

La maggior parte dei debugger degli strumenti di sviluppo comunica con l'hardware di destinazione tramite connessioni OCD (On-Chip Debug), ad esempio JTAG (IEEE 1149.1) e BDM (Background Debug Mode). I debugger comunicano anche con l'hardware di destinazione In-Circuit connessioni ICE (In-Circuit Emulation). Entrambe le connessioni OCD e ICE offrono soluzioni affidabili con intrusioni minime nel software residente di destinazione.

Come per le risorse usate nell'host, il codice sorgente per NetX Duo viene fornito in formato ASCII e richiede circa 1 Mbyte di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

NetX Duo richiede da 5 kByte a 45 KByte di memoria Read-Only memoria (ROM) nella destinazione. Sono necessari altri 1-5 KB di memoria ad accesso casuale (RAM) della destinazione per lo stack di thread di NetX Duo e altre strutture di dati globali.

NetX Duo richiede anche l'uso di due oggetti timer ThreadX e di un oggetto mutex ThreadX. Queste funzionalità vengono usate per esigenze di elaborazione periodiche e per la protezione dei thread all'interno dello stack del protocollo NetX Duo.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS NetX Duo può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/netxduo/> .

Di seguito è riportato un elenco di diversi file importanti nel repository:

**nx_api.h**  
File di intestazione C contenente tutti gli elementi di sistema, le strutture di dati e i prototipi di servizio.

**nx_port.h** File di intestazione C contenente tutte le strutture e le definizioni di dati specifiche dello strumento di sviluppo e della destinazione. 

**demo_netx.c** File C contenente una piccola applicazione demo.

**nx.a (o nx.lib)**  
Versione binaria della libreria NetX C distribuita con il pacchetto standard.

## <a name="netx-duo-installation"></a>Installazione di NetX Duo

NetX Duo viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository NetX Duo nel PC:

```c
    git clone https://github.com/azure-rtos/netxduo
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante di download nella GitHub pagina principale.

Le istruzioni per la creazione della libreria NetX Duo sono disponibili anche nella prima pagina del repository online.

> [!IMPORTANT]
> *Il software applicativo deve accedere al file della libreria NetX Duo (in genere **nx.a** o **nx.lib)** e ai file di inclusione C **nx_api.h e nx_port.h**. Questa operazione viene eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.*

## <a name="using-netx-duo"></a>Uso di NetX Duo

L'uso di NetX Duo è semplice. Fondamentalmente, il codice dell'applicazione deve includere ***nx_api.h** _ durante la compilazione e collegarsi alla libreria NetX Duo _*_nx.a_*_ (o _ *_nx.lib_*)*.

Di seguito sono riportati i quattro semplici passaggi necessari per compilare un'applicazione NetX Duo:

| Passaggio  | Descrizione  |
|---|---|
|Passaggio &nbsp; 1: |Includere il file ***nx_api.h*** in tutti i file dell'applicazione che usano i servizi o le strutture di dati di NetX Duo.|
|Passaggio &nbsp; 2: |Inizializzare il sistema NetX Duo chiamando ***nx_system_initialize** _ dalla funzione _ *_tx_application_define_** o da un thread dell'applicazione.|
|Passaggio &nbsp; 3: |Creare un'istanza IP, abilitare il protocollo ARP (Address Resolution Protocol), se necessario, ed eventuali socket dopo ***nx_system_initialize*** viene chiamato .|
|Passaggio &nbsp; 4: |Compilare l'origine dell'applicazione e collegarsi alla libreria di runtime NetX Duo ***nx.a** _ (o _*_nx.lib_**). L'immagine risultante può essere scaricata nella destinazione ed eseguita.|

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta di NetX Duo viene recapitata con una o più dimostrazioni eseguite in una rete effettiva o tramite un driver di rete simulato. È sempre una buona idea fare in modo che il sistema dimostrativo sia in esecuzione per primo.

Se il sistema dimostrativo non viene eseguito correttamente, eseguire le operazioni seguenti per limitare il problema:

1. Determinare la parte della dimostrazione in esecuzione.
2. Aumentare le dimensioni dello stack in tutti i nuovi thread dell'applicazione.
3. Ricompilare la libreria NetX Duo con le opzioni di debug appropriate elencate nella sezione delle opzioni di configurazione.
4. Esaminare la NX_IP per verificare se i pacchetti vengono inviati o ricevuti.
5. Esaminare il pool di pacchetti predefinito per verificare se sono disponibili pacchetti.
6. Assicurarsi che il driver di rete fornissi pacchetti ARP e IP con le intestazioni su limiti a 4 byte per le applicazioni che richiedono connettività IPv4 o IPv6.
7. Ignorare temporaneamente eventuali modifiche recenti per verificare se il problema scompare o cambia. Tali informazioni dovrebbero risultare utili ai tecnici del supporto tecnico Microsoft.

Seguire le procedure descritte in "What We Need From You" a pagina 12 per inviare le informazioni raccolte dai passaggi per la risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compila la libreria NetX Duo e l'applicazione usando NetX Duo, sono disponibili diverse opzioni di configurazione. Le opzioni di configurazione possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file di inclusione ***nx_user.h,*** se non diversamente specificato.

> [!NOTE]
> *Le opzioni definite in **nx_user.h*** vengono applicate solo se l'applicazione e la libreria NetX Duo vengono compilate NX_INCLUDE_USER_DEFINE_FILE definite.* 

Le sezioni seguenti elencano le opzioni di configurazione disponibili in NetX Duo. Le opzioni generali applicabili sia a IPv4 che a IPv6 sono elencate per prime, seguite dalle opzioni specifiche di IPv6.

### <a name="system-configuration-options"></a>Opzioni di configurazione del sistema

| Opzione  | Descrizione  |
|---|---|
| NX_ASSERT_FAIL    | Simbolo che definisce l'istruzione di debug da utilizzare quando un'asserzione ha esito negativo.                               |
| NX_DEBUG           | Definito, abilita le informazioni di debug di stampa facoltative disponibili dal driver di rete RAM Ethernet. |
| NX_DEBUG_PACKET   | Definito, abilita il dump dei pacchetti di debug facoltativo disponibile nel driver di rete RAM Ethernet.      |
| NX_DISABLE_ASSERT | Definito, disabilita i controlli ASSERT nel codice sorgente. Per impostazione predefinita, questa opzione non è definita.            |
|NX_DISABLE_ERROR_CHECKING | Definito, rimuove l'API di controllo degli errori di base di NetX Duo e migliora le prestazioni. I codici restituiti dell'API non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella definizione dell'API. Questa definizione viene in genere usata dopo che il debug dell'applicazione è stato sufficientemente adeguato e il relativo utilizzo migliora le prestazioni e riduce le dimensioni del codice.|
|NX_DRIVER_DEFERRED_PROCESSING | Definito, abilita la gestione posticipata dei pacchetti dei driver di rete. In questo modo il driver di rete può inserire un pacchetto nell'istanza IP e fare in modo che la routine di elaborazione reale sia chiamata dal thread helper IP interno di NetX Duo.|
|NX_DUAL_PACKET_POOL_ENABLE | Rinominato in ***NX_ENABLE_DUAL_PACKET_POOL** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_ENABLE_DUAL_PACKET_POOL_**.|
|NX_ENABLE_DUAL_PACKET_POOL | Definito, consente all'stack di usare due pool di pacchetti, uno con dimensioni di payload di grandi dimensioni e uno con dimensioni del payload inferiori. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_EXTENDED_NOTIFY_SUPPORT| Definito, abilita più hook di callback nello stack. Queste funzioni di callback vengono usate dal livello wrapper BSD. Per impostazione predefinita, questa opzione non è definita.|
|NX_ENABLE_INTERFACE_CAPABILITY| Definito, consente al driver di dispositivo dell'interfaccia di specificare informazioni aggiuntive sulle funzionalità, ad esempio l'off-loading del checksum. Per impostazione predefinita, questa opzione non è definita.|
|NX_ENABLE_SOURCE_ADDRESS_CHECK| Definito, consente di controllare l'indirizzo di origine del pacchetto in ingresso. Per impostazione predefinita, questa opzione è disabilitata.|
| NX_IPSEC_ENABLE  | Definito, consente alla libreria NetX Duo di supportare le operazioni IPsec. Questa funzionalità richiede il modulo IPsec NetX Duo facoltativo. Per impostazione predefinita, questa funzionalità non è abilitata.            |
| NX_LITTLE_ENDIAN | Definito, esegue lo scambio di byte necessario negli ambienti little endian per garantire che le intestazioni del protocollo siano nel formato big endian corretto. Si noti che il valore predefinito è in ***genere nx_port.h***.|
|NX_MAX_PHYSICAL_INTERFACES | Specifica il numero totale di interfacce di rete fisiche nel dispositivo. Il valore predefinito è 1 ed è definito in ***nx_api.h***; un dispositivo deve avere almeno un'interfaccia fisica. Si noti che non include l'interfaccia di loopback.|
| NX_NAT_ENABLE | Definito, NetX Duo è compilato con il processo NAT. Per impostazione predefinita, questa opzione non è definita.|
| NX_PHYSICAL_HEADER  | Specifica le dimensioni in byte dell'intestazione fisica del frame. Il valore predefinito è 16 (basato su un frame Ethernet tipico a 14 byte allineato al limite a 32 bit) ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima che _*_nx_api.h_*_ sia incluso, ad esempio in _ *_nx_user.h_*.* |
| NX_PHYSICAL_TRAILER | Specifica le dimensioni in byte del trailer di pacchetti fisici e viene in genere usato per riservare spazio di archiviazione per elementi come CRC Ethernet e così via. Il valore predefinito è 4 ed è definito in ***nx_api.h.***|

### <a name="arp-configuration-options"></a>Opzioni di configurazione ARP

| Opzione  | Descrizione  |
|---|---|
|NX_ARP_DEFEND_BY_REPLY | Definito, consente a NetX Duo di proteggere il proprio indirizzo IP inviando una risposta ARP.|
|NX_ARP_DEFEND_INTERVAL| Definisce l'intervallo, espresso in secondi, il modulo ARP invia il pacchetto di difesa successivo in risposta a un messaggio ARP in ingresso che indica un indirizzo in conflitto.|
|NX_ARP_DISABLE_AUTO_ARP_ENTRY|  Rinominato in ***NX_DISABLE_ARP_AUTO_ENTRY** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_ARP_AUTO_ENTRY_**.|
|NX_ARP_EXPIRATION_RATE| Specifica il numero di secondi di validità delle voci ARP. Il valore predefinito zero disabilita la scadenza o l'aging delle voci ARP ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_ARP_MAC_CHANGE_NOTIFICATION_ENABLE | Rinominato in ***NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION_**.|
|NX_ARP_MAX_QUEUE_DEPTH | Specifica il numero massimo di pacchetti che possono essere accodati durante l'attesa di una risposta ARP. Il valore predefinito è 4 ed è definito in ***nx_api.h.***|
|NX_ARP_MAXIMUM_RETRIES | Specifica il numero massimo di tentativi ARP evasi senza una risposta ARP. Il valore predefinito è 18 ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_ARP_UPDATE_RATE | Specifica il numero di secondi tra i tentativi ARP. Il valore predefinito è 10, che rappresenta 10 secondi ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_DISABLE_ARP_AUTO_ENTRY | Definito, disabilita l'immissione di informazioni sulla richiesta ARP nella cache ARP.|
|NX_DISABLE_ARP_INFO | Definito, disabilita la raccolta di informazioni ARP.|
|NX_ENABLE_ARP_MAC_CHANGE_NOTIFICATION| Definito, consente a ARP di richiamare una funzione di notifica di callback al rilevamento dell'aggiornamento dell'indirizzo MAC.|

### <a name="icmp-configuration-options"></a>Opzioni di configurazione ICMP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_ICMP_INFO| Definito, disabilita la raccolta di informazioni ICMP.|
|NX_DISABLE_ICMP_RX_CHECKSUM| Definito, disabilita il calcolo del checksum ICMPv4 e ICMPv6 sui pacchetti ICMP ricevuti. Questa opzione è utile quando il driver dell'interfaccia di rete è in grado di verificare il checksum ICMPv4 e ICMPv6 e l'applicazione non usa la funzionalità di frammentazione IP o IPsec. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMP_TX_CHECKSUM | Definito, disabilita il calcolo del checksum ICMPv4 e ICMPv6 sui pacchetti ICMP trasmessi. Questa opzione è utile quando il driver dell'interfaccia di rete è in grado di calcolare il checksum ICMPv4 e ICMPv6,
e l'applicazione non usa la funzionalità di frammentazione IP o IPsec. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMPV4_ERROR_MESSAGE | Definito, NetX Duo non invia messaggi di errore ICMPv4 in risposta a condizioni di errore, ad esempio un'intestazione IPv4 formattata in modo non corretto. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMPV4_RX_CHECKSUM | Definito, disabilita il calcolo del checksum ICMPv4 sui pacchetti ICMP ricevuti. Questa opzione viene definita automaticamente se ***NX_DISABLE_ICMP_RX_CHECKSUM*** definita. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMPv4_RX_CHECKSUM | Rinominato in ***NX_DISABLE_ICMPV4_RX_CHECKSUM** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_ICMPV4_RX_CHECKSUM_**.|
|NX_DISABLE_ICMPV4_TX_CHECKSUM | Definito, disabilita il calcolo del checksum ICMPv4 sui pacchetti ICMP trasmessi. Questa opzione viene definita automaticamente se ***NX_DISABLE_ICMP_TX_CHECKSUM*** definita. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_ICMPv4_TX_CHECKSUM | Rinominato in ***NX_DISABLE_ICMPV4_TX_CHECKSUM** _.</br>Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_ICMPV4_TX_CHECKSUM_**.|
|NX_ENABLE_ICMP_ADDRESS_CHECK | Definito, viene controllato l'indirizzo di destinazione del pacchetto ICMP. L'impostazione predefinita è disabilitata. Una richiesta Echo ICMP destinata a una trasmissione IP o a un indirizzo multicast IP verrà ignorata automaticamente.|

### <a name="igmp-configuration-options"></a>Opzioni di configurazione IGMP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_IGMP_INFO | Definito, disabilita la raccolta di informazioni IGMP.|
|NX_DISABLE_IGMPV2 | Definito, disabilita il supporto IGMPv2 e NetX Duo supporta solo IGMPv1. Per impostazione predefinita, questa opzione non è impostata ed è definita in ***nx_api.h***.|
|NX_MAX_MULTICAST_GROUPS | Specifica il numero massimo di gruppi multicast che possono essere aggiunti. Il valore predefinito è 7 ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|

### <a name="ip-configuration-options"></a>Opzioni di configurazione IP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_FRAGMENTATION | Definito, disabilita la logica di frammentazione e riassemblaggio IPv4 e IPv6.|
| NX_DISABLE_IPV4     | Definito, disabilita la funzionalità IPv4. Questa opzione può essere usata per compilare NetX Duo per il supporto solo di IPv6. Per impostazione predefinita, questa opzione non è definita. |
| NX_DISABLE_IP_INFO | Definito, disabilita la raccolta di informazioni IP.|
|NX_DISABLE_IP_RX_CHECKSUM | Definito, disabilita la logica di checksum sui pacchetti IPv4 ricevuti. Ciò è utile se il dispositivo di rete è in grado di verificare il checksum IPv4 e l'applicazione non prevede di usare la frammentazione IP o IPsec.|
|NX_DISABLE_IP_TX_CHECKSUM | Definito, disabilita la logica di checksum nei pacchetti IPv4 inviati. Ciò è utile in situazioni in cui il dispositivo di rete sottostante è in grado di generare il checksum dell'intestazione IPv4 e l'applicazione non prevede di usare la frammentazione IP o IPsec.|
|NX_DISABLE_LOOPBACK_INTERFACE | Definito, disabilita il supporto di NetX Duo per l'interfaccia di loopback.|
|NX_DISABLE_RX_SIZE_CHECKING | Definito, disabilita il controllo delle dimensioni sui pacchetti ricevuti.|
|NX_ENABLE_IP_RAW_PACKET_FILTER | Definito, abilita la funzionalità del filtro di ricezione pacchetti non elaborati IP. Le applicazioni che richiedono un maggiore controllo sul tipo di pacchetti IP non elaborati da ricevere possono usare questa funzionalità. La funzionalità filtro pacchetti non elaborati IP supporta anche l'operazione socket non elaborata nel livello di compatibilità BSD. Per impostazione predefinita, questa opzione non è definita.|
|NX_ENABLE_IP_STATIC_ROUTING | Definito, abilita il routing statico IPv4 in cui a un indirizzo di destinazione può essere assegnato un indirizzo hop successivo specifico. Per impostazione predefinita, il routing statico IPv4 è disabilitato.|
|NX_FRAGMENT_IMMEDIATE_ASSEMBLY | Definito, consente l'esecuzione della logica di riassemblaggio IPv4 e IPv6 subito dopo la ricezione di un frammento IP. Per impostazione predefinita, questa opzione non è definita.|
|NX_IP_MAX_REASSEMBLY_TIME | Simbolo che controlla il tempo massimo consentito per riassemblare il frammento IPv4 e il frammento IPv6. Si noti che il valore qui definito sovrascrive sia ***NX_IPV4_MAX_REASSEMBLY_TIME** _ che _*_NX_IPV6_MAX_REASSEMBLY_TIME_**.|
|NX_IP_PERIODIC_RATE | Definito, specifica il numero di tick del timer ThreadX in un secondo. Il valore predefinito deriva dal simbolo ThreadX ***TX_TIMER_TICKS_PER_SECOND,** _ che per impostazione predefinita è impostato su 100 (timer di 10 ms). Le applicazioni devono prestare attenzione quando modificano questo valore, poiché gli altri moduli NetX Duo derivano le informazioni di temporizzazione da _ *_NX_IP_PERIODIC_RATE_.**|
|NX_IP_RAW_MAX_QUEUE_DEPTH | Simbolo che controlla il numero di pacchetti IP non elaborati che possono essere accodati nella coda di ricezione di pacchetti non elaborati. Per impostazione predefinita, il valore è impostato su 20.| 
|NX_IP_ROUTING_TABLE_SIZE | Definito, imposta il numero massimo di voci nella tabella di routing statico IPv4, ovvero un elenco di un'interfaccia in uscita e degli indirizzi hop successivi per un determinato indirizzo di destinazione. Il valore predefinito è 8 ed è definito in ***nx_api.h.** _ Questo simbolo viene usato solo se è definito _ *_NX_ENABLE_IP_STATIC_ROUTING_** .|
|NX_IPV4_MAX_REASSEMBLY_TIME | Simbolo che controlla il tempo massimo consentito per riassemblare il frammento IPv4. Si noti che il valore definito in NX_IP_MAX_REASSEMBLY_TIME sovrascrive questo valore.|

### <a name="packet-configuration-options"></a>Opzioni di configurazione dei pacchetti

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_PACKET_CHAIN | Definito, disabilita la logica della catena di pacchetti. Per impostazione predefinita, questa opzione non è definita.|
|NX_DISABLE_PACKET_INFO | Definito, disabilita la raccolta di informazioni sul pool di pacchetti.|
|NX_ENABLE_LOW_WATERMARK | Definito, abilita la funzionalità limite basso del pool di pacchetti NetX Duo. L'applicazione imposta un valore limite basso. Quando si ricevono pacchetti TCP, se viene raggiunto il limite minimo del pool di pacchetti, NetX Duo rimuove automaticamente il pacchetto rilasciandolo, impedendo la carestia del pool di pacchetti. Per impostazione predefinita, questa funzionalità non è abilitata.|
|NX_ENABLE_PACKET_DEBUG_INFO | Definito, registra le informazioni di debug dei pacchetti.|
|NX_PACKET_ALIGNMENT | Definito, specifica il requisito di allineamento, in byte, per l'indirizzo iniziale dell'area del payload del pacchetto. Questa opzione deprecazione *** NX_PACKET_HEADER_PAD** _ e __*_ NX_PACKET_HEADER_PAD_SIZE **. Per impostazione predefinita, questa opzione è definita come 4, rendendo l'indirizzo iniziale dell'area del payload allineato a 4 byte.|
|NX_PACKET_HEADER_PAD | Definito, abilita la spaziatura interna verso la fine del blocco NX_PACKET di controllo. Il numero di parole ULONG da riempire è definito da ***NX_PACKET_HEADER_PAD_SIZE** _. Si noti che questa opzione viene ammortizzata da _*_NX_PACKET_ALIGNMENT_**.|
|NX_PACKET_HEADER_PAD_SIZE | Imposta il numero di parole ULONG da aggiungere alla struttura NX_PACKET, consentendo all'area del payload del pacchetto di iniziare in corrispondenza dell'allineamento desiderato. Questa funzionalità è utile quando i descrittori del buffer di ricezione puntano direttamente NX_PACKET un'area payload e l'interfaccia di rete riceve la logica o la logica di operazione della cache prevede che l'indirizzo iniziale del buffer soddisfi determinati requisiti di allineamento. Questo valore diventa valido solo quando è **definito * NX_PACKET_HEADER_PAD** _ . Si noti che questa opzione è deprecata da _*_NX_PACKET_ALIGNMENT_**.|

### <a name="rarp-configuration-options"></a>Opzioni di configurazione RARP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_RARP_INFO | Definito, disabilita la raccolta di informazioni RARP.|

### <a name="tcp-configuration-options"></a>Opzioni di configurazione TCP

| Opzione | Descrizione |
|---|---|
|NX_DISABLE_RESET_DISCONNECT | Definito, disabilita l'elaborazione della reimpostazione durante la disconnessione quando il valore di timeout specificato viene specificato ***come NX_NO_WAIT***.|
|NX_DISABLE_TCP_INFO | Definito, disabilita la raccolta di informazioni TCP.|
|NX_DISABLE_TCP_RX_CHECKSUM | Definito, disabilita la logica di checksum nei pacchetti TCP ricevuti. Ciò è utile solo in situazioni in cui il livello di collegamento dispone di un checksum affidabile o di elaborazione CRC oppure il driver di interfaccia è in grado di verificare il checksum TCP nell'hardware e l'applicazione non usa IPsec.|
|NX_DISABLE_TCP_TX_CHECKSUM | Definito, disabilita la logica di checksum per l'invio di pacchetti TCP. Ciò è utile solo in situazioni in cui il nodo di rete ricevente ha ricevuto la logica di checksum TCP disabilitata o il driver di rete sottostante è in grado di generare il checksum TCP e l'applicazione non usa IPsec.|
|NX_ENABLE_TCP_KEEPALIVE | Definito, abilita il timer keepalive TCP facoltativo. Le impostazioni predefinite non sono abilitate.|
|NX_ENABLE_TCP_MSS_CHECK | Definito, abilita la verifica del numero minimo di mss peer prima di accettare una connessione TCP. Per usare questa funzionalità, è necessario ***NX_ENABLE_TCP_MSS_MINIMUM*** il simbolo. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY| Definito, consente all'applicazione di installare una funzione di callback che viene richiamata quando la profondità della coda di trasmissione TCP non è più al valore massimo. Questo callback funge da indicazione che il socket TCP è pronto per trasmettere più dati. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_TCP_WINDOW_SCALING | Abilita l'opzione di ridimensionamento della finestra per le applicazioni TCP. Se definita, l'opzione di ridimensionamento della finestra viene negoziata durante la fase di connessione TCP e l'applicazione è in grado di specificare dimensioni della finestra maggiori di 64.000. L'impostazione predefinita non è abilitata (non definita).|
|NX_MAX_LISTEN_REQUESTS | Specifica il numero massimo di richieste di ascolto del server. Il valore predefinito è 10 ed è definito in ***nx_api.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_ACK_EVERY_N_PACKETS | Specifica il numero di pacchetti TCP da ricevere prima di inviare un ACK. Si noti che **se * NX_TCP_IMMEDIATE_ACK** _ è abilitato ma _ *_NX_TCP_ACK_EVERY_N_PACKETS_** non lo è, questo valore viene impostato automaticamente su 1 per compatibilità con le versioni precedenti.|
|NX_TCP_ACK_TIMER_RATE | Specifica il modo in cui il numero di tick di sistema (NX_IP_PERIODIC_RATE) viene diviso per calcolare la velocità del timer per l'elaborazione ACK con ritardo TCP. Il valore predefinito è 5, che rappresenta 200 ms, ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_ENABLE_KEEPALIVE | Rinominato in ***NX_ENABLE_TCP_KEEPALIVE** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare __*_ NX_ENABLE_TCP_KEEPALIVE **.|
|NX_TCP_ENABLE_MSS_CHECK | Rinominato in ***NX_ENABLE_TCP_MSS_CHECK** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _ *_NX_ENABLE_TCP_MSS_CHECK._**|
|NX_TCP_ENABLE_WINDOW_SCALING | Rinominato in ***NX_ENABLE_TCP_WINDOW_SCALING** _. Anche se è ancora supportato, le nuove progettazioni sono invitate a usare _*_NX_ENABLE_TCP_WINDOW_SCALING_**.|
|NX_TCP_FAST_TIMER_RATE | Specifica il modo in cui il numero di tick interni netx duo (NX_IP_PERIODIC_RATE) viene diviso per calcolare la velocità del timer TCP veloce. Il timer TCP rapido viene usato per guidare i vari timer TCP, incluso il timer ACK ritardato. Il valore predefinito è 10, che rappresenta 100 ms presupponendo che il timer ThreadX sia in esecuzione a 10 ms. Questo valore è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_IMMEDIATE_ACK| Definito, abilita l'elaborazione facoltativa della risposta ACK immediata TCP. La definizione di questo simbolo equivale a definire  ***NX_TCP_ACK_EVERY_N_PACKETS*** deve essere 1.|
|NX_TCP_KEEPALIVE_INITIAL | Specifica il numero di secondi di inattività prima dell'attivazione del timer keepalive. Il valore predefinito è 7200, che rappresenta 2 ore, ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_KEEPALIVE_RETRIES | Specifica il numero di tentativi keepalive consentiti prima che la connessione venga considerata interrotta. Il valore predefinito è 10, che rappresenta 10 tentativi, ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_KEEPALIVE_RETRY | Specifica il numero di secondi tra i tentativi del timer keepalive presupponendo che l'altro lato della connessione non risponda. Il valore predefinito è 75, che rappresenta 75 secondi tra i tentativi e viene definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_MAX_OUT_OF_ORDER_PACKETS | Simbolo che definisce il numero massimo di pacchetti TCP non in ordine che possono essere mantenuti nella coda di ricezione del socket TCP. Questo simbolo può essere usato per limitare il numero di pacchetti accodati nel socket di ricezione TCP, impedendo che il pool di pacchetti venga affamato. Per impostazione predefinita, questo simbolo non è definito, quindi non esiste alcun limite al numero di pacchetti non in ordine in coda nel socket TCP.|
|NX_TCP_MAXIMUM_RETRIES | Specifica il numero di tentativi di trasmissione dati consentiti prima che la connessione venga considerata interrotta. Il valore predefinito è 10, che rappresenta 10 tentativi, ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_MAXIMUM_RX_QUEUE | Simbolo che definisce la coda di ricezione massima per i socket TCP. Questa funzionalità è abilitata da ***NX_ENABLE_LOW_WATERMARK***.|
|NX_TCP_MAXIMUM_TX_QUEUE | Specifica la profondità massima della coda di trasmissione TCP prima che le richieste di invio TCP siano sospese o rifiutate. Il valore predefinito è 20, il che significa che un massimo di 20 pacchetti può essere presente nella coda di trasmissione in qualsiasi momento. Si noti che i pacchetti rimangono nella coda di trasmissione fino a quando un ACK che copre alcuni o tutti i dati del pacchetto non viene ricevuto dall'altro lato della connessione. Questa costante è definita in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_MSS_MINIMUM | Simbolo che definisce il valore MSS minimo accettato dal modulo TCP NetX Duo. Questa funzionalità è abilitata da ***NX_ENABLE_TCP_MSS_CHECK***.|
|NX_TCP_QUEUE_DEPTH_UPDATE_NOTIFY_ENABLE | Rinominato in ***NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY** _. Anche se è ancora supportato, le nuove progettazioni sono invitate a usare _*_NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY_**.|
|NX_TCP_RETRY_SHIFT | Specifica il modo in cui il periodo di timeout di ritrasmissione cambia tra i tentativi. Se questo valore è 0, il timeout di ritrasmissione iniziale è lo stesso dei timeout di ritrasmissione successivi. Se questo valore è 1, ogni ritrasmissione successiva è due volte più lunga. Se questo valore è 2, ogni timeout di ritrasmissione successivo è quattro volte più lungo. Il valore predefinito è 0 ed è definito in ***nx_tcp.h** _. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|
|NX_TCP_TRANSMIT_TIMER_RATE | Specifica il modo in cui il numero di tick di sistema (***NX_IP_PERIODIC_RATE** _) viene diviso per calcolare la frequenza del timer per l'elaborazione dei tentativi di trasmissione TCP. Il valore predefinito è 1, che rappresenta 1 secondo, ed è definito in _*_nx_tcp.h_*_. L'applicazione può eseguire l'override del valore predefinito definendo il valore prima *_dell'nx_api.h_**.|

### <a name="udp-configuration-options"></a>Opzioni di configurazione UDP

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_UDP_INFO | Definito, disabilita la raccolta di informazioni UDP.|
|NX_DISABLE_UDP_RX_CHECKSUM | Definito, disabilita il calcolo del checksum UDP sui pacchetti UDP in ingresso. Ciò è utile se il driver dell'interfaccia di rete è in grado di verificare il checksum dell'intestazione UDP nell'hardware e l'applicazione non abilita la logica di frammentazione IP o IPsec.|
|NX_DISABLE_UDP_TX_CHECKSUM | Definito, disabilita il calcolo del checksum UDP sui pacchetti UDP in uscita. Ciò è utile se il driver dell'interfaccia di rete è in grado di calcolare il checksum dell'intestazione UDP e inserire il valore nell'intestazione IP prima di trasmettere i dati e l'applicazione non abilita la logica di frammentazione IP o IPsec.|

### <a name="ipv6-options"></a>Opzioni IPv6  

| Opzione  | Descrizione  |
|---|---|
| NX_DISABLE_IPV6 | Disabilita la funzionalità IPv6 quando viene compilata la libreria NetX Duo. Per le applicazioni che non necessitano di IPv6, si evita di eseguire il pull del codice e dello spazio di archiviazione aggiuntivo necessario per supportare IPv6.|
|NX_DISABLE_IPV6_PATH_MTU_DISCOVERY | Definito, disabilita l'individuazione MTU del percorso, che viene usata per determinare il numero massimo di MTU nel percorso di una destinazione nella tabella di destinazione dell'host NetX Duo. In questo modo l'host di NetX Duo può inviare il pacchetto più grande possibile che non richiederà la frammentazione. Per impostazione predefinita, questa opzione è definita (il percorso MTU è disabilitato).|
|NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY | Definito, consente di richiamare una funzione di callback quando viene modificato l'indirizzo IPv6. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_IPV6_MULTICAST | Definito, abilita la funzione di join/leave multicast IPv6. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_ENABLE_IPV6_PATH_MTU_DISCOVERY | Definito, abilita la funzionalità di individuazione MTU del percorso IPv6. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_IPV6_ADDRESS_CHANGE_NOTIFY_ENABLE | Rinominato in ***NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY_**.|
|NX_IPV6_DEFAULT_ROUTER_TABLE_SIZE | Specifica il numero di voci nella tabella di routing IPv6. Almeno la voce OnS è necessaria per il router predefinito. Definito in ***nx_api.h***, il valore predefinito è 8.|
|NX_IPV6_DESTINATION_TABLE_SIZE | Specifica il numero di voci nella tabella di destinazione IPv6. In questo modo vengono archiviate le informazioni sugli indirizzi hop successivi per gli indirizzi IPv6. Definito in ***nx_api.h***, il valore predefinito è 8.|
|NX_IPV6_MAX_REASSEMBLY_TIME | Simbolo che controlla il tempo massimo consentito per riassemblare il frammento IPv6.|
|NX_IPV6_MULTICAST_ENABLE | Rinominato in ***NX_ENABLE_IPV6_MULTICAST** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_ENABLE_IPV6_MULTICAST_**.|
|NX_IPV6_PREFIX_LIST_TABLE_SIZE | Specifica le dimensioni della tabella dei prefissi. Le informazioni sul prefisso vengono ottenute dagli annunci router e fanno parte della configurazione degli indirizzi IPv6. Definito in ***nx_api.h***, il valore predefinito è 8.|
|NX_IPV6_STATELESS_AUTOCONFIG_CONTROL | Definito, consente a NetX Duo di disabilitare la funzionalità di configurazione automatica degli indirizzi senza stato. Per impostazione predefinita, questa opzione non è abilitata.|
|NX_MAX_IPV6_ADDRESSES | Specifica il numero di voci nel pool di indirizzi IPv6. Durante la configurazione dell'interfaccia, NetX Duo usa le voci IPv6 del pool. Il valore predefinito è (NX_MAX_PHYSICAL_INTERFACES 3) per consentire a ogni interfaccia di avere almeno un indirizzo locale del collegamento e \* due indirizzi globali. Si noti che tutte le interfacce condividono il pool di indirizzi IPv6.|
|NX_PATH_MTU_INCREASE_WAIT_INTERVAL | Specifica l'intervallo di attesa in tick del timer per reimpostare il percorso MTU per una destinazione specifica nella tabella di destinazione. Se ***NX_DISABLE_IPV6_PATH_MTU_DISCOVERY*** definito, la definizione di questo simbolo non ha alcun effetto.|
|NX_PATH_MTU_INCREASE_WAIT_INTERVAL | Simbolo che specifica l'intervallo di attesa (in secondi) per reimpostare il valore MTU del percorso per una voce della tabella di destinazione. È valido solo se ***NX_ENABLE_IPV6_PATH_MTU_DISCOVERY*** è definito . Per impostazione predefinita, questo valore è impostato su 600 (secondi).|

### <a name="neighbor-cache-configuration-options"></a>Opzioni di configurazione della cache adiacente

| Opzione  | Descrizione  |
|---|---|
|NX_DELAY_FIRST_PROBE_TIME | Specifica il ritardo in secondi prima che venga inviata la prima richiesta per una voce della cache nello stato NON DISPONIBILE. Definito in ***nx_nd_cache.h***, il valore predefinito è 5.|
|NX_DISABLE_IPV6_DAD | Definita, questa opzione disabilita il rilevamento degli indirizzi duplicati (DUPLICATE Address Detection) durante l'assegnazione di indirizzi IPv6. Gli indirizzi vengono impostati tramite la configurazione manuale o la configurazione automatica degli indirizzi senza stato.|
|NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES | Definita, questa opzione impedisce a NetX Duo di rimuovere le voci precedenti della tabella della cache prima della scadenza del timeout per fare spazio alle nuove voci quando la tabella è piena. Le voci statiche e router non vengono mai eliminate.|
|NX_IPV6_DAD_TRANSMITS | Specifica il numero di messaggi Neighbor Solicitation da inviare prima che NetX Duo contrassegni un indirizzo di interfaccia come valido. Se ***NX_DISABLE_IPV6_DAD** _ è definito (LA FUNZIONE È disabilitata), l'impostazione di questa opzione non ha alcun effetto. In alternativa, un valore pari a zero (0) disattiva l'opzione DUO, ma lascia la funzionalità DISA in NetX Duo. Definito in _*_nx_api.h_**, il valore predefinito è 3.|
|NX_IPV6_DISABLE_PURGE_UNUSED_CACHE_ENTRIES | Rinominato in ***NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_IPV6_PURGE_UNUSED_CACHE_ENTRIES_**.|
|NX_IPV6_NEIGHBOR_CACHE_SIZE | Specifica il numero di voci nella tabella IPv6 Neighbor Cache. Definito in ***nx_nd_cache.h***, il valore predefinito è 16.|
|NX_MAX_MULTICAST_SOLICIT | Specifica il numero di messaggi Neighbor Solicitation trasmessi da NetX Duo come parte del protocollo di individuazione router adiacenti IPv6 quando è necessario eseguire il mapping tra l'indirizzo IPv6 e l'indirizzo MAC. Definito in ***nx_nd_cache.h***, il valore predefinito è 3.|
|NX_MAX_UNICAST_SOLICIT | Specifica il numero di messaggi Neighbor Solicitation trasmessi da NetX Duo per determinare la raggiungibilità di un vicino specifico. Definito in ***nx_nd_cache.h***, il valore predefinito è 3.|
|NX_ND_MAX_QUEUE_DEPTH | Simbolo che definisce il numero massimo di pacchetti in coda per la risoluzione della cache ND. Per impostazione predefinita, questo simbolo è impostato su 4.|
|NX_REACHABLE_TIME | Specifica il timeout in secondi per la esistenza di una voce della cache nello stato REACHABLE senza pacchetti ricevuti dall'indirizzo IPv6 di destinazione della cache. Definito in ***nx_nd_cache.h,*** il valore predefinito è 30.|
|NX_RETRANS_TIMER  | Specifica in millisecondi la durata del ritardo tra i pacchetti di richiesta inviati da NetX Duo. Definito in ***nx_nd_cache.h***, il valore predefinito è 1000.|
| NXDUO_DISABLE_DAD | Rinominato in ***NX_DISABLE_IPV6_DAD** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_IPV6_DAD_**.|
|NXDUO_DUP_ADDR_DETECT_TRANSMITS | Rinominato in ***NX_IPV6_DAD_TRANSMITS** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_IPV6_DAD_TRANSMITS_**.|

### <a name="miscellaneous-icmpv6-configuration-options"></a>Varie opzioni di configurazione di ICMPv6

| Opzione  | Descrizione  |
|---|---|
|NX_DISABLE_ICMPV6_ERROR_MESSAGE | Definito, disabilita NetX Duo dall'invio di un messaggio di errore ICMPv6 in risposta a un pacchetto problematico (ad esempio, un'intestazione formattata in modo non corretto o il tipo di intestazione del pacchetto è deprecato) ricevuto da un altro host.|
|NX_DISABLE_ICMPV6_REDIRECT_PROCESS | Definito, disabilita l'elaborazione dei pacchetti di reindirizzamento ICMPv6. NetX Duo elabora per impostazione predefinita i messaggi di reindirizzamento e aggiorna la tabella di destinazione con le informazioni sull'indirizzo IP dell'hop successivo.|
|NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS | Definito, disabilita NetX Duo dall'elaborazione delle informazioni ricevute nei pacchetti di annunci router IPv6.|
|NX_DISABLE_ICMPV6_ROUTER_SOLICITATION | Definito, disabilita NetX Duo dall'invio di messaggi di richiesta router IPv6 a intervalli regolari al router.|
|NX_DISABLE_ICMPV6_RX_CHECKSUM | Definito, disabilita il calcolo del checksum ICMPv6 sui pacchetti ICMP ricevuti.|
|NX_DISABLE_ICMPv6_RX_CHECKSUM | Rinominato in ***NX_DISABLE_ICMPV6_RX_CHECKSUM** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_CMPV6_RX_CHECKSUM_**.|
|NX_DISABLE_ICMPV6_TX_CHECKSUM | Definito, disabilita e il calcolo del checksum ICMPv6 sui pacchetti ICMP trasmessi.|
|NX_DISABLE_ICMPV6_TX_CHECKSUM | Rinominato in ***NX_DISABLE_ICMPV6_TX_CHECKSUM** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_ICMPV6_TX_CHECKSUM_**.|
|NX_ICMPV6_MAX_RTR_SOLICITATIONS | Definire il numero massimo di richieste di router inviate da un host fino alla ricezione di una risposta del router. Se non viene ricevuta alcuna risposta, l'host conclude che non è presente alcun router. Il valore predefinito è 3.|
|NX_ICMPV6_RTR_SOLICITATION_DELAY | Specifica il ritardo massimo in secondi per la richiesta iniziale del router.|
|NX_ICMPV6_RTR_SOLICITATION_INTERVAL | Specifica l'intervallo tra due messaggi di richiesta router. Il valore predefinito è 4.|
|NXDUO_DESTINATION_TABLE_SIZE | Rinominato in ***NX_IPV6_DESTINATION_TABLE_SIZE** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_IPV6_DESTINATION_TABLE_SIZE_**.|
|NXDUO_DISABLE_ICMPV6_ERROR_MESSAGE | Rinominato in ***NX_DISABLE_ICMPV6_ERROR_MESSAGE** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_ICMPV6_ERROR_MESSAGE_**.|
|NXDUO_DISABLE_ICMPV6_REDIRECT_PROCESS | Rinominato in ***NX_DISABLE_ICMPV6_REDIRECT_PROCESS** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _ *_NX_DISABLE_ICMPV6_REDIRECT_PROCESS_**|  
|NXDUO_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS| Rinominato in ***NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_ICMPV6_ROUTER_ADVERTISEMENT_PROCESS_**.|
|NXDUO_DISABLE_ICMPV6_ROUTER_SOLICITATION | Rinominato in ***NX_DISABLE_ICMPV6_ROUTER_SOLICITATION** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_DISABLE_ICMPV6_ROUTER_SOLICITATION_**.|
|NXDUO_ICMPV6_MAX_RTR_SOLICITATIONS | Rinominato in ***NX_ICMPV6_MAX_RTR_SOLICITATIONS** _. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _*_NX_ICMPV6_MAX_RTR_SOLICITATIONS_**.|
|NXDUO_ICMPV6_RTR_SOLICITATION_INTERVAL | Rinominato in ***NX_ICMPV6_RTR_SOLICITATION_INTERVAL** _. Questo simbolo è in fase di depreciazione. Anche se è ancora supportata, le nuove progettazioni sono invitate a usare _ *_NX_ICMPV6_RTR_SOLICITATION_INTERVAL_**|

## <a name="netx-duo-version-id"></a>ID versione di NetX Duo

La versione corrente di NetX Duo è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. È possibile ottenere la versione di NetX Duo dall'esame del file **nx_port.h.** Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di NetX Duo esaminando la stringa _* *_globale_*_ nx_version_id in _*_nx_port.h_**.

Il software applicativo può anche ottenere informazioni sulla versione dalle costanti indicate di seguito definite in ***nx_api.h.***

Queste costanti identificano la versione corrente del prodotto in base al nome e alla versione principale e secondaria del prodotto.

\#Definire EL_PRODUCT_NETXDUO  
\#Definire NETXDUO_MAJOR_VERSION  
\#Definire NETXDUO_MINOR_VERSION