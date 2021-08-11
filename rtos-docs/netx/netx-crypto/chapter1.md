---
title: Capitolo 1 - Introduzione alla crittografia Azure RTOS NetX
description: NetX Crypto è un'implementazione in tempo reale ad alte prestazioni di algoritmi di crittografia progettati per fornire servizi di crittografia e autenticazione dei dati.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1b5ee0336ba9e867a628dc5db4f0c029f68ff45c81d68ceb6299e3469d5e2b49
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796804"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-crypto"></a>Capitolo 1 - Introduzione alla crittografia Azure RTOS NetX

Azure RTOS NetX Crypto è un'implementazione ad alte prestazioni in tempo reale di algoritmi di crittografia progettati per fornire servizi di crittografia e autenticazione dei dati. NetX Crypto è progettato per collegare i moduli NETX Secure TLS, DTLS e IPsec. Le applicazioni possono anche usare NetX Crypto come modulo autonomo esterno alla sicurezza di rete.

## <a name="netx-crypto-unique-features"></a>Funzionalità univoche di NetX Crypto

NetX Crypto viene implementato nel linguaggio C standard (C99), compatibile con praticamente tutti i compilatori C/C++. La progettazione modulare consente a un'applicazione di collegarsi solo agli algoritmi di crittografia che deve usare, ottenendo quindi dimensioni minime del codice. L'implementazione è progettata per funzionare con la maggior parte dei microprocessori a 32 bit e usa solo le operazioni matematiche di base (addizione, sottrazione, moltiplicazione, divisione, AND logico, OR, NOR e operazioni di spostamento in bit). Tutte queste operazioni vengono usate con quantità a 32 bit, rendendo Portabile NetX Crypto nella maggior parte dei microprocessori a 32 bit. L'implementazione è ottimizzata in modo specifico per l'esecuzione su microprocessori con vincoli di risorse, che hanno come destinazione applicazioni con incorporamento approfondito.

## <a name="algorithms-supported-by-netx-crypto"></a>Algoritmi supportati da NetX Crypto

NetX Crypto supporta gli algoritmi di crittografia seguenti. NetX Crypto segue tutte le raccomandazioni generali e i requisiti di base entro i vincoli di un sistema operativo e di piattaforme in tempo reale che richiedono un footprint di memoria ridotto ed esecuzione efficiente.

| Algoritmo       | Lunghezza chiave (bit)      |
| --------------- | ---------------------- |
| AES(CBC, CTR)   | 128, 192, 256          |
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

| Algoritmo       | Lunghezza digest (bit) | Dimensioni blocco (bit) |
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

## <a name="netx-crypto-requirements"></a>Requisiti della crittografia NetX

TBD: requisito di memoria. Interrompi/ricognizione sicura? Discussione sulle esigenze

## <a name="netx-crypto-constraints"></a>Vincoli di crittografia NetX

Nessuno.
