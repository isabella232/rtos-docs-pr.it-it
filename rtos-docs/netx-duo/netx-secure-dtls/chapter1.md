---
title: Capitolo 1 - Introduzione all'Azure RTOS DTLS sicuro netx
description: Azure RTOS NetX Secure DTLS è un'implementazione in tempo reale del protocollo Datagram Transport Layer Security progettato per applicazioni incorporate basate su ThreadX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a7fe51fd1e141c0c525a98986ca3058732b61843f8bd79bf24fc5ac986147501
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797042"
---
# <a name="chapter-1-introduction-to-azure-rtos-netx-secure-dtls"></a>Capitolo 1: Introduzione all'Azure RTOS DTLS sicuro netx

Azure RTOS NetX Secure DTLS è un'implementazione in tempo reale ad alte prestazioni del protocollo Datagram Transport Layer Security progettato esclusivamente per le applicazioni incorporate basate su ThreadX. Questo capitolo contiene un'introduzione a NetX Secure DTLS e una descrizione delle applicazioni e dei vantaggi.

## <a name="netx-secure-unique-features"></a>Funzionalità univoche sicure di NetX

A differenza della maggior parte delle altre implementazioni TLS/DTLS, NetX Secure è stato progettato da zero per supportare un'ampia gamma di piattaforme hardware incorporate e si ridimensiona facilmente dalle piccole applicazioni micro-controller ai processori incorporati più potenti disponibili. Il codice viene scritto in base alle risorse limitate dei sistemi incorporati e offre una serie di opzioni di configurazione per ridurre il footprint di memoria necessario per fornire comunicazioni di rete sicure su TLS o DTLS.

## <a name="rfcs-supported-by-netx-secure"></a>RFC supportate da NetX Secure

NetX Secure supporta i protocolli seguenti correlati a TLS e DTLS. L'elenco non è necessariamente completo perché sono disponibili numerose RFC relative a TLS/DTLS e alla crittografia. NetX Secure segue tutte le raccomandazioni generali e i requisiti di base entro i vincoli di un sistema operativo in tempo reale con footprint di memoria ridotto ed esecuzione efficiente.


| RFC | Descrizione |
| --- | ----------- |
| RFC 6347 | Datagramma Transport Layer Security versione 1.2. |
| RFC 2246 | Protocollo TLS versione 1.0|
| RFC 4346 | Protocollo Transport Layer Security (TLS) versione 1.1 |
| RFC 5246 | Protocollo Transport Layer Security (TLS) versione 1.2 |
| RFC 5280 | Certificati X.509 PKI (v3) |
| RFC 3268 | Advanced Encryption Standard (AES) per Transport Layer Security (TLS) |
| RFC 3447 | Public-Key Cryptography Standards (PKCS) #1: Specifiche di crittografia RSA versione 2.1 |
| RFC 2104 | HMAC: Keyed-Hashing per l'autenticazione dei messaggi |
| RFC 6234 | Algoritmi hash sicuri degli Stati Uniti (HMAC e HKDF basati su SHA e SHA) |
| RFC 4279 | Ciphersuit con chiave precondi condivisa per TLS |

## <a name="netx-secure-dtls-requirements"></a>Requisiti di NetX Secure DTLS

Per funzionare correttamente, la libreria di runtime NetX Secure richiede che sia già stata creata un'istanza IP NetX. Inoltre, e a seconda dell'applicazione, saranno necessari uno o più certificati digitali X.509 con codifica DER, per identificare un'istanza TLS/DTLS o per verificare i certificati provenienti da un host remoto. Il pacchetto NetX Secure non ha altri requisiti.

## <a name="netx-secure-dtls-constraints"></a>Vincoli DTLS sicuri netx

Il protocollo NetX Secure DTLS implementa i requisiti dello standard RFC 6347 per DTLS 1.2. Esistono tuttavia i vincoli seguenti:

1. A causa della natura dei dispositivi incorporati, alcune applicazioni potrebbero non avere le risorse necessarie per supportare le dimensioni massime dei record TLS/DTLS di 16 KB. NetX Secure può gestire record da 16 KB nei dispositivi con risorse sufficienti.
2. Verifica minima del certificato. NetX Secure eseguirà la verifica della catena X.509 di base su un certificato per garantire che il certificato sia valido e firmato da un'autorità di certificazione attendibile e possa fornire il nome comune del certificato per l'applicazione da confrontare con il nome di dominio Top-Level dell'host remoto. Tuttavia, la verifica delle estensioni del certificato e di altri dati è responsabilità dell'implementatore dell'applicazione.
3. La crittografia basata su software richiede un utilizzo intensivo del processore. Le routine crittografiche basate su software NetX Secure sono state ottimizzate per le prestazioni, ma a seconda della potenza del processore di destinazione, queste prestazioni possono comportare operazioni molto lunghe. Quando la crittografia basata su hardware è disponibile, deve essere usata per ottenere prestazioni ottimali di NetX Secure DTLS.
