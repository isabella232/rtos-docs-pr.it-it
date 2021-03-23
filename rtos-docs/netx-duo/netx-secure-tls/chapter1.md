---
title: Capitolo 1-Introduzione ad Azure RTO NetX Secure
description: Questo capitolo contiene un'introduzione ad Azure RTO NetX Secure e una descrizione delle relative applicazioni e vantaggi.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8f4c7a97564cd2f702f9887181b36297b42fa492
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821587"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-secure"></a>Capitolo 1-Introduzione ad Azure RTO NetX Secure

Azure RTO NetX Secure è un'implementazione in tempo reale a prestazioni elevate degli standard di sicurezza della rete di crittografia, tra cui TLS/SSL progettato esclusivamente per applicazioni incorporate basate su ThreadX. Questo capitolo contiene un'introduzione a NetX Secure e una descrizione delle relative applicazioni e vantaggi.

## <a name="netx-secure-unique-features"></a>Funzionalità univoche sicure di NetX

A differenza della maggior parte delle altre implementazioni TLS, NetX Secure è stato progettato da zero per supportare un'ampia gamma di piattaforme hardware incorporate e consente di ridimensionare facilmente le piccole applicazioni micro-controller ai processori embedded più potenti disponibili. Il codice viene scritto con le limitate risorse dei sistemi incorporati e fornisce una serie di opzioni di configurazione per ridurre il footprint di memoria necessario per fornire comunicazioni di rete sicure su TLS.

## <a name="rfcs-supported-by-netx-secure"></a>RFC supportate da NetX Secure 

NetX Secure supporta i protocolli seguenti correlati a TLS. L'elenco non è necessariamente completo perché sono presenti numerose RFC relative a TLS e crittografia. NetX Secure segue tutte le raccomandazioni generali e i requisiti di base entro i vincoli di un sistema operativo in tempo reale con un footprint di memoria ridotto e un'esecuzione efficiente.

| RFC      | Descrizione                                                                                                 | Pagina |
|----------|-------------------------------------------------------------------------------------------------------------|------|
| RFC 2104 | HMAC: Keyed-Hashing per l'autenticazione dei messaggi                                                              | 33   |
| RFC 2246 | Il protocollo TLS versione 1,0                                                                                | 19   |
| RFC 3268 | Advanced Encryption Standard (AES) ciphersuites per Transport Layer Security (TLS)                          | 31   |
| RFC 3447 | Public-Key Cryptography Standards (PKCS) #1: RSA Cryptography Specifications versione 2,1                    | 32   |
| RFC 4279 | Ciphersuites chiave pre-condivisa per TLS                                                                         | 39   |
| RFC 4346 | Il protocollo Transport Layer Security (TLS) versione 1,1                                                     | 19   |
| RFC 5246 | Il protocollo Transport Layer Security (TLS) versione 1,2                                                     | 19   |
| RFC 5280 | Certificati PKI X. 509 (v3)                                                                                 | 41   |
| RFC 5746 | Estensione per l'indicazione di rinegoziazione Transport Layer Security (TLS)                                           |      |
| RFC 5869 | Funzione di derivazione della chiave Extract-and-expand basata su HMAC (HKDF)                                                | 19   |
| RFC 6066<sup>1</sup> | Estensioni Transport Layer Security (TLS): definizioni di estensione                                            | 19   |
| RFC 6234 | Algoritmi hash sicuri per gli Stati Uniti (hash e HKDF basati su SHA e SHA)                                                 | 33   |
| RFC 8443 | Pacchetti di crittografia a curva ellittica (ECC) per le versioni Transport Layer Security (TLS) 1,2 e versioni precedenti |      |
| RFC 8446 | Il protocollo Transport Layer Security (TLS) versione 1,3                                                     | 19   |

1. A partire dalla versione 6,0 solo l'estensione Indicazione nome server (SNI) di RFC 6066 è completamente supportata.

## <a name="netx-secure-requirements"></a>Requisiti di sicurezza NetX

Per funzionare correttamente, la libreria di runtime protetta NetX richiede che sia già stata creata un'istanza IP di NetX. Inoltre, e a seconda dell'applicazione, saranno necessari uno o più certificati digitali X. 509 con codifica DER, per identificare un'istanza di TLS o per verificare i certificati provenienti da un host remoto. Il pacchetto sicuro NetX non ha altri requisiti.

## <a name="netx-secure-constraints"></a>Vincoli di sicurezza NetX

Il protocollo NetX Secure implementa i requisiti dello standard RFC 5246 per TLS 1,2 e RFC 8446 per TLS 1,3, oltre a fornire la compatibilità (disabilitata per impostazione predefinita) con le RFC 4346 (TLS 1,1) e 2246 (TLS 1,0). Esistono tuttavia i vincoli seguenti:

- Per TLS 1,2 e TLS 1,3 sono supportati solo ciphersuites con SHA-256. Nelle versioni precedenti alla TLS 1,2, l'handshake TLS usa una routine di hashing fisso per verificare che i messaggi di handshake TLS non vengano manomessi. A partire dalla versione 1,2, l'handshake usa la routine hash fornita con ciphersuite. TLS non sa in anticipo quale routine hash verrà usata e deve memorizzare nella cache i messaggi di handshake. Correggendo l'hash in SHA-256, NetX Secure TLS può funzionare con un footprint di RAM inferiore rispetto ad altre implementazioni TLS. Questa limitazione verrà rimossa in una versione futura una volta che l'utilizzo della memoria può essere risolto correttamente. * Nota importante: questa limitazione si applica **solo** alla scelta di ciphersuite. Le firme del certificato X. 509 non sono soggette alla stessa limitazione ed è possibile utilizzare una qualsiasi delle routine hash supportate.
- A causa della natura dei dispositivi incorporati, alcune applicazioni potrebbero non avere le risorse necessarie per supportare le dimensioni massime dei record TLS di 16KB. NetX Secure è in grado di gestire i record 16KB nei dispositivi con risorse sufficienti. Il buffer del riassemblatore TLS (vedere informazioni di riferimento sulle API per *nx_secure_tls_session_packet_buffer_set*) **può** essere impostato su una dimensione inferiore a 16KB a rischio di problemi di interoperabilità. Se viene ricevuto un record TLS valido che è più grande del buffer di riassemblaggio, NetX Secure TLS interrompe la sessione TLS con un errore. In generale, il buffer deve essere sempre impostato su almeno 18KB (dimensione del record TLS 16KB + 2 KB per la spaziatura interna della crittografia) e ridotto solo nelle impostazioni controllate (ad esempio, l'host remoto garantisce una dimensione massima del record TLS).
  > [!NOTE]
  > In generale, il buffer del riassemblaggio del pacchetto non deve mai essere inferiore alle dimensioni massime dei record TLS. Tuttavia, se le caratteristiche dell'host remoto sono note, ad esempio in un sistema completamente chiuso, le dimensioni possono essere ridotte in modo da ottenere un ulteriore spazio di RAM.
- Verifica minima del certificato. NetX Secure eseguirà la verifica della catena X. 509 di base su un certificato per garantire che il certificato sia valido e firmato da un'autorità di certificazione attendibile e possa fornire il nome comune del certificato per l'applicazione da confrontare con il nome di dominio Top-Level dell'host remoto. Se è disponibile un clock in tempo reale, è possibile usarlo per verificare la data di scadenza del certificato (vedere API nx_secure_tls_session_time_function_set). Tuttavia, la verifica delle estensioni del certificato e di altri dati è responsabilità dell'implementatore dell'applicazione.
- La crittografia basata su software richiede un utilizzo intensivo del processore. Le routine di crittografia basate su software sicuro NetX sono state ottimizzate per le prestazioni, ma a seconda della potenza del processore di destinazione, le prestazioni possono comportare operazioni molto lunghe. Quando la crittografia basata su hardware è disponibile, è consigliabile usarla per ottenere prestazioni ottimali di TLS sicuro NetX.
- La frammentazione del record di handshake TLS non è supportata. Se alcuni messaggi di record di handshake TLS sono troppo grandi, possono essere suddivisi in più record TLS. NetX Secure TLS attualmente lo considera come un errore. I requisiti di memoria per i sistemi incorporati indicano che è probabile che il messaggio del record di handshake più grande non possa essere gestito comunque, ma la limitazione potrebbe causare errori durante la comunicazione con determinati host TLS che utilizzano catene di certificati di dimensioni eccessive.
- Il server TLS non supporta la selezione di certificati dinamici quando sono presenti più certificati nell'archivio locale. 
- L'utilizzo della sintassi del certificato X509 non è stato osservato. 
- Ciphersuites basati su ECDH non sono supportati. In alternativa, usare ECDHE.
