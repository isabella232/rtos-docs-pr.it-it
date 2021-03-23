---
title: Capitolo 1-Introduzione a Network Address Translation
description: IP Network Address Translation (NAT) è stato sviluppato originariamente per risolvere il problema di un numero limitato di indirizzi IPv4 Internet.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3d01aa6f68e21ea82f65a59a19c4f5c7958a6b92
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821773"
---
# <a name="chapter-1---an-introduction-to-network-address-translation"></a>Capitolo 1-Introduzione a Network Address Translation

## <a name="the-need-for-network-address-translation"></a>Necessità della traduzione degli indirizzi di rete

IP Network Address Translation (NAT) è stato sviluppato originariamente per risolvere il problema di un numero limitato di indirizzi IPv4 Internet. La necessità di NAT si verifica quando più dispositivi devono accedere a Internet, ma solo un indirizzo Internet IPv4 viene assegnato dal provider di servizi Internet (ISP).

Esistono anche altri vantaggi dell'uso di NAT. La topologia di rete all'esterno del dominio locale può variare in molti modi. I clienti possono modificare i provider, i backbone aziendali possono essere riorganizzati oppure i provider possono essere Uniti o divisi. Ogni volta che la topologia esterna viene modificata, è necessario modificare anche le assegnazioni di indirizzi per gli host all'interno del dominio locale in modo da riflettere queste modifiche esterne. Le modifiche di questo tipo possono essere nascoste dagli utenti all'interno del dominio centralizzando le modifiche a un singolo router di traduzione degli indirizzi. NAT consente l'accesso per gli host locali alla rete Internet pubblica e li protegge dall'accesso diretto dall'esterno. Le organizzazioni con una configurazione di rete prevalentemente per uso interno, con la necessità di un accesso esterno occasionale sono ottimi candidati per questo schema.

## <a name="basic-nat-and-network-address-port-translation"></a>Traduzione di base NAT e porta indirizzo di rete

Un router abilitato per NAT viene installato tra la rete pubblica e la rete privata. Il ruolo del router abilitato per NAT è la conversione tra gli indirizzi IPv4 privati interni e l'indirizzo IPv4 pubblico assegnato, in modo che tutti i dispositivi nella rete privata possano condividere lo stesso indirizzo IPv4 pubblico.

Nell'implementazione di base di NAT, il router NAT ' è proprietario ' di uno o più indirizzi IP registrati a livello globale diverso dal proprio indirizzo IP. Questi indirizzi globali sono disponibili per l'assegnazione a host nella propria rete privata in modo statico o dinamico. NAPT, o la conversione di porta dell'indirizzo di rete, è una variante di NAT di base, in cui Network Address Translation viene esteso in modo da includere un identificatore di "trasporto". Generalmente questo è il numero di porta per i pacchetti TCP e UDP e l'ID di query per i pacchetti ICMP.

Le connessioni tra i confini NAT vengono in genere avviate dagli host nella rete privata che inviano pacchetti in uscita a un host esterno. A questi host vengono in genere assegnati indirizzi IP *dinamici* (temporanei) a questo scopo. Tuttavia, è anche possibile che le connessioni siano avviate nella direzione opposta se la rete privata ha "Server", ad esempio server HTTP o FTP che accetteranno le richieste client dalla rete esterna. NAT assegna in genere questi host locali a un indirizzo IP *statico* (permanente): porta.

## <a name="how-network-address-translation-works"></a>Funzionamento della traduzione degli indirizzi di rete

Una configurazione di rete tipica con un router abilitato per NAT è illustrata nella figura 1.

![Una configurazione di rete tipica con un router abilitato per NAT](media/image2.png)

**Figura 1: configurazione di rete tipica con un router abilitato per NAT**

Un router abilitato per NAT ha in genere due interfacce di rete. Un'interfaccia è connessa alla rete Internet pubblica; l'altra è connessa alla rete privata. Un tipico router in questa configurazione è responsabile del routing di datagrammi IP tra la rete privata e la rete pubblica in base all'indirizzo IP di destinazione. Un router abilitato per NAT esegue la conversione degli indirizzi prima di instradare un datagramma IPv4 tra l'interfaccia pubblica e quella privata. Viene stabilita una traduzione per ogni sessione TCP o UDP, in base all'indirizzo di origine interno, al numero di porta di origine e all'indirizzo di destinazione esterno e al numero di porta di destinazione. Per il datagramma di richiesta e risposta echo ICMP, viene usato l'ID di query ICMP anziché il numero di porta.

Per illustrare un'implementazione tipica della traduzione degli indirizzi di rete, si consideri una configurazione di rete nella figura 2.

![Un'implementazione tipica della traduzione degli indirizzi di rete](media/image3.png)

**Figura 2: implementazione tipica della traduzione degli indirizzi di rete**

In questo scenario, il router NAT connette la rete privata a sinistra e la rete pubblica a destra. Si supponga sul lato rete pubblica, l'indirizzo IP dell'interfaccia del router NAT è 202.151.25.14; nell'interfaccia di rete privata, il router NAT usa l'indirizzo IP 192.168.1.254. Un nodo nella rete privata avvia una connessione TCP con un server Web su Internet.

Nella figura 3 viene illustrata una visualizzazione di alto livello del processo di conversione degli indirizzi di rete.

![Una visualizzazione di alto livello del processo di traduzione degli indirizzi di rete](media/image4.png)

**Figura 3: Panoramica generale del processo di conversione degli indirizzi di rete**

1. Il client trasmette un messaggio TCP SYN al server Web. L'indirizzo del mittente è 192.168.1.15, numero di porta 6732; l'indirizzo di destinazione è 128.15.54.3, numero di porta 80.
1. Il pacchetto dal client viene ricevuto sull'interfaccia di rete privata dal router NAT. La regola del traffico in uscita si applica al pacchetto: l'indirizzo del mittente (client) viene convertito nell'indirizzo IP pubblico del router NAT 202.15.25.14 e il numero di porta di origine del mittente (client) viene convertito nel numero di porta TCP 2015 sull'interfaccia pubblica.
1. Il pacchetto viene quindi trasmesso su Internet e infine raggiunge l'host di destinazione 128.15.54.3. Si noti che sul lato ricevente, in base all'indirizzo di origine del livello IP e al numero di porta del livello TCP, il pacchetto sembra avere origine da 202.151.24.14, numero di porta 2015.
   Nella figura 4 viene illustrato il processo NAT sul percorso di ritorno.

   ![Processo NAT nel percorso di ritorno](media/image5.png)

   **Figura 4-processo NAT sul percorso di ritorno**
1. In questo scenario, l'host Internet 128.15.54.3 Invia un pacchetto di risposta con l'indirizzo Internet del router NAT come destinazione.
1. Il pacchetto raggiunge il router NAT. Poiché si tratta di un pacchetto in-bound, vengono applicate le regole di conversione in ingresso: l'indirizzo di destinazione viene modificato di nuovo nell'indirizzo IP del mittente originale (client): 192.168.1.15, porta di destinazione numero 6732.
1. Il pacchetto viene quindi inviato al client tramite l'interfaccia connessa alla rete interna.

In questo modo l'indirizzo di rete Internet e il numero di porta del mittente non vengono esposti ad altri host nella rete Internet pubblica.

## <a name="netx-duo-nat-features"></a>Funzionalità NAT di NetX Duo

Quando l'istanza NAT viene creata utilizzando *nx_nat_create* chiamata, viene creata la tabella di conversione NAT.

```C
UINT nx_nat_create(NX_NAT_DEVICE *nat_ptr, NX_IP *ip_ptr,
    UINT global_interface_index,
    VOID *dynamic_cache_memory,
    UINT dynamic_cache_size);
```

Per tenere traccia delle traduzioni degli indirizzi di rete per tutte le connessioni attive tra reti locali ed esterne, il router NetX Duo abilitato NAT gestisce una tabella di traduzione con informazioni su ogni connessione host privata che include l'indirizzo IP di origine e di destinazione e il numero di porta.

Il percorso della tabella di conversione ("cache") viene impostato con il puntatore dynamic_cache_memory. Quest'area deve essere uno spazio del buffer allineato a 4 byte. La dimensione della tabella (o numero di voci) viene determinata dividendo la dimensione della cache dynamic_cache_size per la dimensione di una voce della tabella NAT. La tabella deve essere sufficientemente grande per il numero minimo di voci specificato da **NX_NAT_MIN_ENTRY_COUNT definito in *nx_nat. h*. Il valore predefinito è 3.**

Il timeout per tutte le voci dinamiche nella tabella di conversione NAT NetX Duo viene inizializzato in NX_NAT_ENTRY_RESPONSE_TIMEOUT definito in *nx_nat. h*. Il valore predefinito è 4 minuti (o 240 cicli di sistema per un processore a 100 mHz) come consigliato da RFC 2663. Ogni volta che NetX Duo NAT riceve o Invia un pacchetto corrispondente a una voce dinamica nella tabella, reimposta il timeout della voce per NX_NAT_ENTRY_RESPONSE_TIMEOUT. Quando si esegue una ricerca nella tabella, NetX Duo NAT controllerà anche la tabella per le voci scadute ed eliminarle.

Per creare voci in ingresso come statiche nella tabella, ad esempio per i server della rete locale, NetX Duo NAT fornisce il servizio *nx_nat_inbound_entry_create* . Se una voce della tabella definisce la connessione host locale come statica, non scade mai.

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr,
    ULONG local_ip_address, USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

Questo servizio è descritto più dettagliatamente nel [capitolo 4-Descrizione dei servizi](chapter4.md)

In fase di esecuzione, se la tabella di traduzione è piena e non è possibile aggiungere altre voci, NetX Duo NAT invierà una notifica all'applicazione NAT con un callback completo della cache se ne è stata registrata una con l'istanza NAT. Questa operazione viene eseguita usando il servizio *nx_nat_cache_notify_set* :

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)(NX_NAT_DEVICE *nat_ptr));
```

Per ulteriori informazioni su questo servizio, vedere il [capitolo 4-Descrizione dei servizi](chapter4.md) .

## <a name="nat-packet-processing-in-netx-duo"></a>Elaborazione di pacchetti NAT in NetX Duo

NetX Duo NAT è progettato per l'uso in un router IPv4. Per il funzionamento di NAT, è necessario configurare NetX Duo per inoltrare i pacchetti al server NAT. Per informazioni su come eseguire questa operazione, vedere il capitolo 2 sull'installazione di NetX Duo NAT. Il server NAT indica quindi se verrà usato (tenta di inviare) il pacchetto a un host in una delle sue reti. Se non utilizzerà il pacchetto, il pacchetto viene restituito a NetX Duo per elaborare il pacchetto come normalmente.

Quando il server NAT riceve un pacchetto da inoltrare da NetX Duo, determina se il pacchetto è in ingresso o in uscita.

Per i pacchetti in uscita, il server NAT controlla la porta e l'indirizzo di origine dell'intestazione IP del pacchetto. Se la tabella di conversione non contiene una voce per un pacchetto inviato in precedenza da questo host per la stessa destinazione, NAT creerà una nuova voce che conterrà un indirizzo IP di origine globale univoco: porta per la connessione e modificherà le intestazioni dei pacchetti con il nuovo indirizzo IP: porta prima di inviarlo alla rete esterna.

Per i pacchetti in ingresso, il server NAT cerca una voce precedente nella relativa tabella di conversione con un indirizzo IP esterno: porta corrispondente all'indirizzo IP di destinazione del pacchetto: porta. Se non viene trovata alcuna corrispondenza, il pacchetto verrà scartato a meno che l'indirizzo di destinazione: porta non sia l'indirizzo esterno per il server nella rete locale. Se trova una corrispondenza, sostituisce l'indirizzo IP di destinazione esterno dell'intestazione del pacchetto: porta con indirizzo IP privato: porta e invia il pacchetto nella rete locale all'host privato previsto.

NetX Duo NAT utilizza un intervallo di porte di conversione TCP, UDP e ICMP per la creazione di indirizzi locali univoci: connessioni porta per gli host locali che si connettono agli host esterni. Le opzioni configurabili dall'utente seguenti, definite in *nx_nat. h,* definiscono l'intervallo per ogni protocollo:

```C
NX_NAT_START_TCP_PORT

NX_NAT_END_TCP_PORT

NX_NAT_START_UDP_PORT

NX_NAT_END_UDP_PORT

NX_NAT_START_ICMP_QUERY_ID

NX_NAT_END_ICMP_QUERY_ID
```

## <a name="nat-requirements-and-constraints"></a>Requisiti e vincoli NAT

NetX Duo NAT richiede NetX Duo 5,8 o versione successiva. Per l'applicazione NAT è richiesta la creazione di una singola istanza IP e di un'interfaccia per la rete fisica interna ed esterna.

Vincoli

- NetX Duo NAT supporta TCP, UDP e ICMP. IGMP non è supportato.
- NetX Duo NAT non supporta l'indirizzamento IPv6.
- NetX Duo NAT non include servizi DNS o DHCP, sebbene NetX Duo NAT possa integrare tali servizi con le relative operazioni NAT.

## <a name="rfcs-supported-by-netx-duo-nat"></a>RFC supportate da NetX Duo NAT

L'implementazione NAT di NetX duo si basa sulle informazioni presentate nei seguenti RFC:

- RFC 2663: terminologia e considerazioni su IP Network Address Translator (NAT)
- RFC 3022: tradizionale indirizzo IP netowrk Translator (NAT tradizionale)
- RFC 4787: requisiti di comportamento NAT (Network Address Translation) per UDP unicast
