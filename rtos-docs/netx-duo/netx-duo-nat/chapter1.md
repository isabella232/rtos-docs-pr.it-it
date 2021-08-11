---
title: 'Capitolo 1: Introduzione a Network Address Translation'
description: NAT (Ip Network Address Translation) è stato originariamente sviluppato per risolvere il problema di un numero limitato di indirizzi IPv4 Internet.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8639b87decd78f58a34fe6b8033a2427b560c872814abfdbbcb6057166412d0d
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797465"
---
# <a name="chapter-1---an-introduction-to-network-address-translation"></a>Capitolo 1: Introduzione a Network Address Translation

## <a name="the-need-for-network-address-translation"></a>Necessità di Network Address Translation

NAT (Ip Network Address Translation) è stato originariamente sviluppato per risolvere il problema di un numero limitato di indirizzi IPv4 Internet. La necessità di NAT si verifica quando più dispositivi devono accedere a Internet, ma un solo indirizzo Internet IPv4 viene assegnato dal provider di servizi Internet (ISP).

L'uso di NAT offre anche altri vantaggi. La topologia di rete esterna al dominio locale può cambiare in molti modi. I clienti possono cambiare provider, i backbone aziendali possono essere riorganizzati o i provider possono essere uniti o divisi. Ogni volta che la topologia esterna viene modificata, anche le assegnazioni di indirizzi per gli host all'interno del dominio locale devono cambiare per riflettere queste modifiche esterne. Le modifiche di questo tipo possono essere nascoste agli utenti all'interno del dominio centralizzando le modifiche apportate a un singolo router di conversione degli indirizzi. NAT abilita l'accesso degli host locali alla rete Internet pubblica e li protegge dall'accesso diretto dall'esterno. Le organizzazioni con una configurazione di rete prevalentemente per uso interno, con la necessità di un accesso esterno occasionale sono candidati buoni per questo schema.

## <a name="basic-nat-and-network-address-port-translation"></a>NAT di base e Network Address Port Translation

Tra la rete pubblica e la rete privata viene installato un router abilitato per NAT. Il ruolo del router abilitato per NAT è la conversione tra gli indirizzi IPv4 privati interni e l'indirizzo IPv4 pubblico assegnato, in modo che tutti i dispositivi nella rete privata siano in grado di condividere lo stesso indirizzo IPv4 pubblico.

Nell'implementazione di base di NAT, il router NAT è proprietario di uno o più indirizzi IP registrati a livello globale diversi dal proprio indirizzo IP. Questi indirizzi globali sono disponibili per l'assegnazione agli host nella rete privata in modo statico o dinamico. NAPT, o Network Address Port Translation, è una variante di NAT di base, in cui network address translation viene esteso per includere un identificatore di "trasporto". In genere si tratta del numero di porta per i pacchetti TCP e UDP e dell'ID query per i pacchetti ICMP.

Le connessioni attraverso il limite NAT vengono in genere avviate dagli host nella rete privata che inviano pacchetti in uscita a un host esterno. A questi host vengono in genere *assegnati indirizzi* IP dinamici (temporanei) a questo scopo. Tuttavia, è anche possibile che le connessioni vengono avviate nella direzione opposta se la rete privata dispone di "server", ad esempio server HTTP o FTP che accetteranno richieste client dalla rete esterna. NAT assegna in genere a questi host locali un *indirizzo* IP statico (permanente): porta.

## <a name="how-network-address-translation-works"></a>Funzionamento di Network Address Translation

Una configurazione di rete tipica con un router abilitato per NAT è illustrata nella figura 1.

![Configurazione di rete tipica con un router abilitato per NAT](media/image2.png)

**Figura 1- Configurazione di rete tipica con un router abilitato per NAT**

Un router abilitato per NAT ha in genere due interfacce di rete. Un'interfaccia è connessa alla rete Internet pubblica. l'altro è connesso alla rete privata. Un router tipico in questa configurazione è responsabile del routing dei datagrammi IP tra la rete privata e la rete pubblica in base all'indirizzo IP di destinazione. Un router abilitato per NAT esegue la conversione degli indirizzi prima del routing di un datagramma IPv4 tra l'interfaccia pubblica e l'interfaccia privata. Viene stabilita una conversione per ogni sessione TCP o UDP, in base all'indirizzo di origine interno, al numero di porta di origine e all'indirizzo di destinazione esterno e al numero di porta di destinazione. Per il datagramma di richiesta e risposta echo ICMP, viene usato l'ID query ICMP anziché il numero di porta.

Per illustrare un'implementazione tipica di Network Address Translation, si consideri una configurazione di rete nella figura 2.

![Implementazione tipica di Network Address Translation](media/image3.png)

**Figura 2 - Implementazione tipica di Network Address Translation**

In questo scenario, il router NAT connette la rete privata a sinistra e la rete pubblica a destra. Si supponga che sul lato della rete pubblica l'indirizzo IP dell'interfaccia del router NAT sia 202.151.25.14. nell'interfaccia di rete privata, il router NAT usa l'indirizzo IP 192.168.1.254. Un nodo nella rete privata avvia una connessione TCP con un server Web su Internet.

La figura 3 mostra una visualizzazione di alto livello del processo Network Address Translation.

![Visualizzazione di alto livello del processo Network Address Translation](media/image4.png)

**Figura 3- Visualizzazione di alto livello del processo Network Address Translation**

1. Il client trasmette un messaggio SYN TCP al server Web. L'indirizzo del mittente è 192.168.1.15, numero di porta 6732; l'indirizzo di destinazione è 128.15.54.3, numero di porta 80.
1. Il pacchetto dal client viene ricevuto nell'interfaccia di rete privata dal router NAT. La regola del traffico in uscita si applica al pacchetto: l'indirizzo del mittente (client) viene convertito nell'indirizzo IP pubblico del router NAT 202.15.25.14 e il numero di porta di origine del mittente (client) viene convertito nel numero di porta TCP 2015 sull'interfaccia pubblica.
1. Il pacchetto viene quindi trasmesso su Internet e infine raggiunge l'host di destinazione 128.15.54.3. Si noti che sul lato ricevente, in base all'indirizzo di origine del livello IP e al numero di porta del livello TCP, il pacchetto sembra avere avuto origine da 202.151.24.14, numero di porta 2015.
   La figura 4 illustra il processo NAT nel percorso restituito.

   ![Processo NAT nel percorso restituito](media/image5.png)

   **Figura 4 - Processo NAT nel percorso restituito**
1. In questo scenario, l'host Internet 128.15.54.3 invia un pacchetto di risposta con l'indirizzo Internet del router NAT come destinazione.
1. Il pacchetto raggiunge il router NAT. Poiché si tratta di un pacchetto in ingresso, si applicano le regole di conversione in ingresso: l'indirizzo di destinazione viene modificato nuovamente nell'indirizzo IP del mittente originale (client): 192.168.1.15, numero di porta di destinazione 6732.
1. Il pacchetto viene quindi inoltrato al client tramite l'interfaccia connessa alla rete interna.

In questo modo l'indirizzo di rete Internet e il numero di porta del mittente non sono esposti ad altri host sulla rete Internet pubblica.

## <a name="netx-duo-nat-features"></a>Funzionalità NAT di NetX Duo

Quando l'istanza NAT viene creata *nx_nat_create* chiamata, viene creata la tabella di conversione NAT.

```C
UINT nx_nat_create(NX_NAT_DEVICE *nat_ptr, NX_IP *ip_ptr,
    UINT global_interface_index,
    VOID *dynamic_cache_memory,
    UINT dynamic_cache_size);
```

Per tenere traccia delle traduzioni degli indirizzi di rete per tutte le connessioni attive tra reti locali ed esterne, il router abilitato per NAT di NetX Duo mantiene una tabella di conversione con informazioni su ogni connessione host privato che include l'indirizzo IP di origine e di destinazione e il numero di porta.

La posizione di questa tabella di conversione ("cache") viene impostata con il puntatore dynamic_cache_memory conversione. Quest'area deve essere uno spazio del buffer allineato a 4 byte. Le dimensioni della tabella (o il numero di voci) vengono determinate dividendo le dimensioni della cache dynamic_cache_size per le dimensioni di una voce di tabella NAT. Le dimensioni della tabella devono essere sufficienti per il numero minimo di voci specificato da **NX_NAT_MIN_ENTRY_COUNT definito in *nx_nat.h.* Il valore predefinito è 3.**

Il timeout per tutte le voci dinamiche nella tabella di conversione NAT di NetX Duo viene inizializzato su NX_NAT_ENTRY_RESPONSE_TIMEOUT definito in *nx_nat.h.* Il valore predefinito è 4 minuti (o 240 tick di sistema per un processore a 100 mHz) come consigliato da RFC 2663. Ogni volta che NetX Duo NAT riceve o invia un pacchetto corrispondente a una voce dinamica nella tabella, reimposta il timeout di tale voce NX_NAT_ENTRY_RESPONSE_TIMEOUT. Quando si esegue una ricerca nella tabella, NetX Duo NAT controlla anche la tabella per verificare la presenza di voci scadute ed eliminarle.

Per creare voci in ingresso come statiche nella tabella, ad esempio per i server nella rete locale, NetX Duo NAT fornisce il *nx_nat_inbound_entry_create* servizio. Se una voce di tabella definisce la connessione host locale come statica, non scade mai.

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr,
    ULONG local_ip_address, USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

Questo servizio è descritto in modo più dettagliato nel [capitolo 4 - Descrizione dei servizi](chapter4.md)

Durante il runtime, se la tabella di conversione è piena e non è possibile aggiungere altre voci, NetX Duo NAT invierà una notifica all'applicazione NAT con un callback completo della cache se ne è registrata una con l'istanza NAT. Questa operazione viene eseguita usando *il nx_nat_cache_notify_set* seguente:

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)(NX_NAT_DEVICE *nat_ptr));
```

Per altri dettagli su questo servizio, vedere capitolo [4 - Descrizione](chapter4.md) dei servizi.

## <a name="nat-packet-processing-in-netx-duo"></a>Elaborazione di pacchetti NAT in NetX Duo

NetX Duo NAT è destinato all'uso in un router IPv4. Per il funzionamento di NAT, è necessario configurare NetX Duo per l'inoltro di pacchetti al server NAT. Per informazioni su come eseguire questa operazione, vedere il capitolo 2 sull'installazione nat di NetX Duo. Il server NAT indica quindi se "consumerà" (tenterà di inoltrare) il pacchetto a un host in una delle reti. Se non utilizza il pacchetto, il pacchetto viene "restituito" a NetX Duo per elaborare il pacchetto come di consueto.

Quando il server NAT riceve un pacchetto da inoltrare da NetX Duo, determina se il pacchetto è in ingresso o in uscita.

Per i pacchetti in uscita, il server NAT controlla la porta e l'indirizzo di origine dell'intestazione IP del pacchetto. Se la tabella di conversione non contiene una voce per un pacchetto inviato in precedenza da questo host per la stessa destinazione, NAT creerà una nuova voce che conterrà un indirizzo IP di origine globale univoco:porta per la connessione e modificherà le intestazioni dei pacchetti con questo nuovo indirizzo IP:porta prima di inviarlo alla rete esterna.

Per i pacchetti in ingresso, il server NAT cerca una voce precedente nella relativa tabella di conversione con un indirizzo IP esterno: porta corrispondente all'indirizzo IP di destinazione del pacchetto: porta. Se non viene trovata alcuna corrispondenza, scarterà il pacchetto a meno che l'indirizzo di destinazione: port sia l'indirizzo esterno per il server nella rete locale. Se trova una corrispondenza, sostituirà l'indirizzo IP di destinazione esterno dell'intestazione del pacchetto: porta con l'indirizzo IP privato: porta e invierà il pacchetto nella rete locale all'host privato previsto.

NetX Duo NAT usa un intervallo di porte di conversione TCP, UDP e ICMP per la creazione di indirizzi locali univoci: connessioni di porta per gli host locali che si connettono a host esterni. Le opzioni configurabili dall'utente seguenti, definite in *nx_nat.h,* definiscono l'intervallo per ogni protocollo:

```C
NX_NAT_START_TCP_PORT

NX_NAT_END_TCP_PORT

NX_NAT_START_UDP_PORT

NX_NAT_END_UDP_PORT

NX_NAT_START_ICMP_QUERY_ID

NX_NAT_END_ICMP_QUERY_ID
```

## <a name="nat-requirements-and-constraints"></a>Requisiti e vincoli NAT

NetX Duo NAT richiede NetX Duo 5.8 o versione successiva. L'applicazione NAT richiede la creazione di una singola istanza IP e di un'interfaccia per la rete fisica interna ed esterna.

Vincoli:

- NetX Duo NAT supporta TCP, UDP e ICMP. IGMP non è supportato.
- NetX Duo NAT non supporta l'indirizzamento IPv6.
- NetX Duo NAT non include servizi DNS o DHCP, anche se NetX Duo NAT può integrare tali servizi con le relative operazioni NAT.

## <a name="rfcs-supported-by-netx-duo-nat"></a>RFC supportate da NetX Duo NAT

L'implementazione nat di NetX Duo si basa sulle informazioni presentate nelle RFC seguenti:

- RFC 2663: Terminologia e considerazioni su NAT (Network Address Translator) IP
- RFC 3022: Indirizzo Netowrk IP tradizionale Translator (NAT tradizionale)
- RFC 4787: Requisiti di comportamento nat (Network Address Translation) per UDP unicast
