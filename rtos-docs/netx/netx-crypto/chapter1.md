---
title: Capitolo 1-Introduzione ad Azure RTO NetX Crypto
description: NetX Crypto è un'implementazione in tempo reale a prestazioni elevate degli algoritmi di crittografia progettati per fornire servizi di autenticazione e crittografia dei dati.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 0bde9be472584308894cfd702ccd014578afe753
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821500"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-crypto"></a>Capitolo 1-Introduzione ad Azure RTO NetX Crypto

Azure RTO NetX Crypto è un'implementazione in tempo reale a prestazioni elevate degli algoritmi di crittografia progettati per fornire servizi di autenticazione e crittografia dei dati. NetX Crypto è progettato per essere collegato ai moduli NetX Secure TLS, DTLS e IPsec. Le applicazioni possono anche usare NetX Crypto come modulo autonomo al di fuori della sicurezza di rete.

## <a name="netx-crypto-unique-features"></a>Funzionalità univoche di crittografia NetX

NetX Crypto viene implementato nel linguaggio C standard (C99), compatibile con praticamente tutti i compilatori C/C++. La progettazione modulare consente a un'applicazione di collegarsi solo negli algoritmi di crittografia che devono usare, ottenendo quindi dimensioni minime del codice. L'implementazione è progettata per funzionare con la maggior parte dei microprocessori a 32 bit e usa solo le operazioni matematiche di base (addizione, sottrazione, moltiplicazione, divisione, logica e, o, né e operazioni di spostamento di bit). Tutte queste operazioni vengono usate con le quantità a 32 bit, rendendo NetX Crypto portatile tra i microprocessori a 32 bit. L'implementazione è ottimizzata in modo specifico per l'esecuzione in microprocessori vincolati alle risorse, destinate a applicazioni con Deep embedded.

## <a name="algorithms-supported-by-netx-crypto"></a>Algoritmi supportati da NetX Crypto

NetX Crypto supporta gli algoritmi di crittografia seguenti. NetX Crypto segue tutte le raccomandazioni generali e i requisiti di base all'interno dei vincoli di un sistema operativo in tempo reale e delle piattaforme che richiedono un footprint di memoria ridotto e un'esecuzione efficiente.

| Algoritmo       | Lunghezza chiave (BITS)      |
| --------------- | ---------------------- |
| AES (CBC, CTR)   | 128, 192, 256          |
| AES (XCBC)       | 128                    |
| AES-CCM 8       | 128                    |
| 3DES (CBC)       | 192                    |
| HMAC-SHA1       | Qualsiasi lunghezza             |
| HMAC-SHA224     | Qualsiasi lunghezza             |
| HMAC-SHA256     | Qualsiasi lunghezza             |
| HMAC-SHA384     | Qualsiasi lunghezza             |
| HMAC-SHA512     | Qualsiasi lunghezza             |
| HMAC-SHA512/224 | Qualsiasi lunghezza             |
| HMAC-SHA512/256 | Qualsiasi lunghezza             |
| HMAC-MD5        | Qualsiasi lunghezza             |
| RSA             | 1024, 2048, 3072, 4096 |

| Algoritmo       | Lunghezza digest (BITS) | Dimensioni blocco (BITS) |
| --------------- | -------------------- | ----------------- |
| SHA1            | 160                  | 512               |
| SHA224          | 224                  | 512               |
| SHA256          | 256                  | 512               |
| SHA384          | 384                  | 1024              |
| SHA512          | 512                  | 1024              |
| MD5             | 128                  | 512               |
| HMAC-SHA1       | 160                  | 512               |
| HMAC-SHA224     | 224                  | 512               |
| HMAC-SHA256     | 256                  | 512               |
| HMAC-SHA384     | 384                  | 1024              |
| HMAC-SHA512     | 512                  | 1024              |
| HMAC-SHA512/224 | 224                  | 1024              |
| HMAC-SHA512/256 | 256                  | 1024              |
| HMAC-MD5        | 128                  | 512               |
| Curva ellittica  | P192/224/256/384/521 |                   |

## <a name="netx-crypto-requirements"></a>Requisiti di crittografia NetX

TBD: requisito di memoria. Interruzione/rientranza sicura? Discussione necessaria

## <a name="netx-crypto-constraints"></a>Vincoli di crittografia NetX

Nessuno.
