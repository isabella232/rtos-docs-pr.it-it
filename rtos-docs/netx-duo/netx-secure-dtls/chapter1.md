---
title: Capitolo 1-Introduzione ad Azure RTO NetX Secure DTLS
description: Azure RTO NetX Secure DTLS è un'implementazione in tempo reale di datagramma Transport Layer Security protocollo progettato per le applicazioni incorporate basate su ThreadX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: dbd81082524f50787765dfacf494248dda740fd6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822880"
---
# <a name="chapter-1-introduction-to-azure-rtos-netx-secure-dtls"></a>Capitolo 1: introduzione ad Azure RTO NetX Secure DTLS

Azure RTO NetX Secure DTLS è un'implementazione in tempo reale a prestazioni elevate di di datagramma Transport Layer Security protocollo progettato esclusivamente per le applicazioni basate su ThreadX embedded. Questo capitolo contiene un'introduzione a NetX Secure DTLS e una descrizione delle relative applicazioni e vantaggi.

## <a name="netx-secure-unique-features"></a>Funzionalità univoche sicure di NetX

A differenza della maggior parte delle altre implementazioni di TLS/DTLS, NetX Secure è stato progettato da zero per supportare un'ampia gamma di piattaforme hardware incorporate e consente di ridimensionare facilmente da piccole applicazioni micro-controller ai processori embedded più potenti disponibili. Il codice viene scritto con le limitate risorse dei sistemi incorporati e fornisce una serie di opzioni di configurazione per ridurre il footprint di memoria necessario per fornire comunicazioni di rete sicure su TLS o DTLS.

## <a name="rfcs-supported-by-netx-secure"></a>RFC supportate da NetX Secure

NetX Secure supporta i protocolli seguenti correlati a TLS e DTLS. L'elenco non è necessariamente completo perché sono presenti numerose RFC relative a TLS/DTLS e alla crittografia. NetX Secure segue tutte le raccomandazioni generali e i requisiti di base entro i vincoli di un sistema operativo in tempo reale con un footprint di memoria ridotto e un'esecuzione efficiente.


| RFC | Descrizione |
| --- | ----------- |
| RFC 6347 | Datagramma Transport Layer Security versione 1,2. |
| RFC 2246 | Il protocollo TLS versione 1,0|
| RFC 4346 | Il protocollo Transport Layer Security (TLS) versione 1,1 |
| RFC 5246 | Il protocollo Transport Layer Security (TLS) versione 1,2 |
| RFC 5280 | Certificati PKI X. 509 (v3) |
| RFC 3268 | Advanced Encryption Standard (AES) ciphersuites per Transport Layer Security (TLS) |
| RFC 3447 | Public-Key Cryptography Standards (PKCS) #1: RSA Cryptography Specifications versione 2,1 |
| RFC 2104 | HMAC: Keyed-Hashing per l'autenticazione dei messaggi |
| RFC 6234 | Algoritmi hash sicuri per gli Stati Uniti (hash e HKDF basati su SHA e SHA) |
| RFC 4279 | Ciphersuites chiave pre-condivisa per TLS |

## <a name="netx-secure-dtls-requirements"></a>NetX Secure DTLS requirements

Per funzionare correttamente, la libreria di runtime protetta NetX richiede che sia già stata creata un'istanza IP di NetX. Inoltre, a seconda dell'applicazione, saranno necessari uno o più certificati digitali X. 509 con codifica DER, per identificare un'istanza TLS/DTLS o per verificare i certificati provenienti da un host remoto. Il pacchetto sicuro NetX non ha altri requisiti.

## <a name="netx-secure-dtls-constraints"></a>Vincoli DTLS protetti NetX

Il protocollo NetX Secure DTLS implementa i requisiti dello standard RFC 6347 per DTLS 1,2. Esistono tuttavia i vincoli seguenti:

1. A causa della natura dei dispositivi incorporati, alcune applicazioni potrebbero non avere le risorse necessarie per supportare le dimensioni massime dei record TLS/DTLS di 16KB. NetX Secure è in grado di gestire i record 16KB nei dispositivi con risorse sufficienti.
2. Verifica minima del certificato. NetX Secure eseguirà la verifica della catena X. 509 di base su un certificato per garantire che il certificato sia valido e firmato da un'autorità di certificazione attendibile e possa fornire il nome comune del certificato per l'applicazione da confrontare con il nome di dominio Top-Level dell'host remoto. Tuttavia, la verifica delle estensioni del certificato e di altri dati è responsabilità dell'implementatore dell'applicazione.
3. La crittografia basata su software richiede un utilizzo intensivo del processore. Le routine di crittografia basate su software sicuro NetX sono state ottimizzate per le prestazioni, ma a seconda della potenza del processore di destinazione, le prestazioni possono comportare operazioni molto lunghe. Quando la crittografia basata su hardware è disponibile, è consigliabile usarla per ottenere prestazioni ottimali per NetX Secure DTLS.
