---
title: Capitolo 1 - Introduzione a Azure RTOS NetX Secure
description: Questo capitolo contiene un'introduzione Azure RTOS NetX Secure e una descrizione delle applicazioni e dei vantaggi.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1d6b0f23d7353626f340fe0ab93ee1e04800edaaa1f00da49afd83f84339df86
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791602"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-secure"></a>Capitolo 1 - Introduzione a Azure RTOS NetX Secure

Azure RTOS NetX Secure è un'implementazione in tempo reale ad alte prestazioni degli standard di sicurezza di rete crittografici, tra cui TLS/SSL progettato esclusivamente per le applicazioni incorporate basate su ThreadX. Questo capitolo contiene un'introduzione a NetX Secure e una descrizione delle applicazioni e dei vantaggi.

## <a name="netx-secure-unique-features"></a>Funzionalità univoche sicure di NetX

A differenza della maggior parte delle altre implementazioni TLS, NetX Secure è stato progettato da zero per supportare un'ampia gamma di piattaforme hardware incorporate e si ridimensiona facilmente dalle piccole applicazioni micro-controller ai processori incorporati più potenti disponibili. Il codice viene scritto in base alle risorse limitate dei sistemi incorporati e offre una serie di opzioni di configurazione per ridurre il footprint di memoria necessario per fornire comunicazioni di rete sicure su TLS.

## <a name="rfcs-supported-by-netx-secure"></a>RFC supportate da NetX Secure 

NetX Secure supporta i protocolli seguenti correlati a TLS. L'elenco non è necessariamente completo perché sono presenti numerose RFC relative a TLS e alla crittografia. NetX Secure segue tutte le raccomandazioni generali e i requisiti di base entro i vincoli di un sistema operativo in tempo reale con footprint di memoria ridotto ed esecuzione efficiente.

| RFC      | Descrizione                                                                                                 | Pagina |
|----------|-------------------------------------------------------------------------------------------------------------|------|
| RFC 2104 | HMAC: Keyed-Hashing per l'autenticazione dei messaggi                                                              | 33   |
| RFC 2246 | Protocollo TLS versione 1.0                                                                                | 19   |
| RFC 3268 | Advanced Encryption Standard (AES) per Transport Layer Security (TLS)                          | 31   |
| RFC 3447 | Public-Key Cryptography Standards (PKCS) #1: Specifiche di crittografia RSA versione 2.1                    | 32   |
| RFC 4279 | Ciphersuit della chiave precondi condivisi per TLS                                                                         | 39   |
| RFC 4346 | Protocollo Transport Layer Security (TLS) versione 1.1                                                     | 19   |
| RFC 5246 | Protocollo Transport Layer Security (TLS) versione 1.2                                                     | 19   |
| RFC 5280 | Certificati X.509 PKI (v3)                                                                                 | 41   |
| RFC 5746 | estensione dell'indicazione di rinegoziazione Transport Layer Security (TLS)                                           |      |
| RFC 5869 | Funzione di derivazione delle chiavi di estrazione ed espansione basata su HMAC (HKDF)                                                | 19   |
| RFC 6066<sup>1</sup> | Transport Layer Security (TLS): definizioni di estensione                                            | 19   |
| RFC 6234 | Algoritmi hash sicuri degli Stati Uniti (HMAC e HKDF basati su SHA e SHA)                                                 | 33   |
| RFC 8443 | Pacchetti di crittografia ECC (Elliptic Curve Cryptography) per Transport Layer Security (TLS) 1.2 e versioni precedenti |      |
| RFC 8446 | Protocollo Transport Layer Security (TLS) versione 1.3                                                     | 19   |

1. A partire dalla versione 6.0 è completamente supportata solo l'estensione Indicazione nome server (SNI) da RFC 6066.

## <a name="netx-secure-requirements"></a>Requisiti di sicurezza di NetX

Per funzionare correttamente, la libreria di runtime NetX Secure richiede che sia già stata creata un'istanza IP NetX. Inoltre, e a seconda dell'applicazione, saranno necessari uno o più certificati digitali X.509 con codifica DER, per identificare un'istanza TLS o per verificare i certificati provenienti da un host remoto. Il pacchetto NetX Secure non ha altri requisiti.

## <a name="netx-secure-constraints"></a>Vincoli di sicurezza NetX

Il protocollo NetX Secure implementa i requisiti degli standard RFC 5246 per TLS 1.2 e RFC 8446 per TLS 1.3, oltre a fornire la compatibilità facoltativa (disabilitata per impostazione predefinita) con le RFC 4346 (TLS 1.1) e 2246 (TLS 1.0). Esistono tuttavia i vincoli seguenti:

- Solo i ciphersuit che usano SHA-256 sono supportati per TLS 1.2 e TLS 1.3. Nelle versioni precedenti a TLS 1.2, l'handshake TLS usa una routine hash fissa per verificare che i messaggi di handshake TLS non siano manomissioni. A partire dalla versione 1.2, l'handshake usa la routine hash fornita con ciphersuite. TLS non sa in anticipo quale routine hash verrà usata e deve memorizzare nella cache i messaggi di handshake. Correggendo l'hash in SHA-256, NetX Secure TLS può funzionare con un footprint di RAM inferiore rispetto ad altre implementazioni TLS. Questa limitazione verrà rimossa in una versione futura quando sarà possibile risolvere correttamente l'utilizzo della memoria. *NOTA IMPORTANTE: questa limitazione si **applica solo** alla scelta di ciphersuite. Le firme di certificato X.509 non sono soggette alla stessa limitazione ed è possibile usare una delle routine hash supportate.
- A causa della natura dei dispositivi incorporati, alcune applicazioni potrebbero non avere le risorse necessarie per supportare le dimensioni massime dei record TLS di 16 KB. NetX Secure può gestire record da 16 KB nei dispositivi con risorse sufficienti. Il buffer di riassemblaggio TLS (vedere le informazioni di riferimento sulle API per nx_secure_tls_session_packet_buffer_set *)* può essere impostato su una dimensione inferiore a 16 KB a rischio di problemi di interoperabilità.  Se viene ricevuto un record TLS valido maggiore del buffer di riassemblaggio, NetX Secure TLS interromperà la sessione TLS con un errore. In generale, il buffer deve essere sempre impostato su almeno 18 KB (dimensioni del record TLS di 16 KB + 2 KB per il riempimento della crittografia) e ridotte solo nelle impostazioni controllate (ad esempio, l'host remoto garantisce una dimensione massima dei record TLS).
  > [!NOTE]
  > In generale, il buffer di riassemblaggio dei pacchetti non deve mai essere inferiore alle dimensioni massime del record TLS. Tuttavia, se le caratteristiche dell'host remoto sono note ,ad esempio in un sistema completamente chiuso, le dimensioni possono essere ridotte per recuperare spazio ram.
- Verifica minima del certificato. NetX Secure eseguirà la verifica della catena X.509 di base su un certificato per garantire che il certificato sia valido e firmato da un'autorità di certificazione attendibile e possa fornire il nome comune del certificato per l'applicazione da confrontare con il nome di dominio Top-Level dell'host remoto. Se è disponibile un orologio in tempo reale, può essere usato per verificare la data di scadenza del certificato (vedere Api nx_secure_tls_session_time_function_set). Tuttavia, la verifica delle estensioni del certificato e di altri dati è responsabilità dell'implementatore dell'applicazione.
- La crittografia basata su software richiede un utilizzo intensivo del processore. Le routine crittografiche basate su software NetX Secure sono state ottimizzate per le prestazioni, ma a seconda della potenza del processore di destinazione, queste prestazioni possono comportare operazioni molto lunghe. Quando la crittografia basata su hardware è disponibile, deve essere usata per ottenere prestazioni ottimali di NetX Secure TLS.
- Frammentazione del record di handshake TLS non supportata. Se alcuni messaggi di record di handshake TLS sono troppo grandi, possono essere suddivisi tra più record TLS. NetX Secure TLS lo considera attualmente un errore. I requisiti di memoria per i sistemi incorporati significano che è probabile che il messaggio del record di handshake più grande non possa essere gestito comunque, ma la limitazione potrebbe causare errori durante la comunicazione con determinati host TLS che usano catene di certificati eccessivamente grandi.
- Il server TLS non supporta la selezione dinamica dei certificati quando sono presenti più certificati nell'archivio locale. 
- L'errore X509 Certificate KeyUsage non viene osservato. 
- I cipheruit basati su ECDH non sono supportati. In alternativa, usare ECDHE.
