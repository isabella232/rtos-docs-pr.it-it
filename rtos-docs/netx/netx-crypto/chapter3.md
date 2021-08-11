---
title: Capitolo 3 - Descrizione funzionale di Azure RTOS NetX Crypto
description: Questo capitolo contiene una descrizione funzionale di NetX Crypto.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8aa49c130dc2802e95620ccdd4f4d9398c3fd2e55f5896d004e47baa72829848
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796746"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-crypto"></a>Capitolo 3 - Descrizione funzionale di Azure RTOS NetX Crypto

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Questo capitolo contiene una descrizione funzionale di Azure RTOS NetX Crypto. Esistono due tipi principali di esecuzione del programma in un'applicazione di crittografia NetX: inizializzazione e chiamate all'interfaccia dell'applicazione.

*La crittografia NetX può essere usata come libreria di crittografia autonoma o con ThreadX, NetX e/o NetX Secure.*

## <a name="aes"></a>AES

- **Algoritmo Standard:**: NetX Crypto implementa AES in base a NIST FIPS 197, disponibile in: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf)
- **Lunghezze di chiave supportate:** 128, 192, 256
- **Modalità supportate:**
  - CBC, CTR, (lunghezza chiave 128, 192, 256 bit)
  - XCBC (solo lunghezza della chiave a 128 bit),
  - CCM8 (solo lunghezza della chiave a 128 bit)
- **Requisiti di memoria:** l'applicazione specifica il buffer di input e il buffer di output e una struttura di controllo AES. La struttura di controllo AES mantiene lo stato dell'algoritmo AES tra le chiamate all'API. Il buffer di input contiene dati da crittografare o decrittografare e può avere dimensioni arbitrarie. Il buffer di output viene usato da AES per archiviare i dati elaborati da AES. Le dimensioni del buffer di output non devono essere inferiori alle dimensioni del buffer di input e devono essere un multiplo di 16 byte, la dimensione del blocco AES. I buffer di input e output devono essere di memoria contigua e possono non sovrapporsi, tranne nel caso speciale della crittografia sul posto (usando la stessa memoria per l'input e l'output). Quando si esegue la crittografia sul posto, il buffer di output inizia esattamente nella stessa posizione del buffer di input e non deve essere inferiore al buffer di input. Quando la crittografia AES funziona sul posto, non è necessaria memoria aggiuntiva per i file scratch.

## <a name="3des"></a>3DES

- **Algoritmo Standard:** NetX Crypto implementa Tripple DES(TDES, noto anche come 3DES) in base alla pubblicazione speciale NIST 800-67 rev 2: *"Recommendataion for the Triple Data Encryption Algorithm (TDES) Block Cipher" (Raccomandazione* per la crittografia a blocchi TDES (Triple Data Encryption Algorithm), disponibile all'indirizzo: [https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final](https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final)
- **Lunghezza chiave supportata:** 64 * 3 = 192
- **Memory Requreiment:**: None

In NetX Crypto il termine "3DES" viene usato in modo intercambiabile con "TDES".

## <a name="md5"></a>MD5

- **Algorithm Standard:** NetX Crypto implementa MD5 in base a RFC 1321: *"The MD5 Message-Digest Algorithm"*
- **Requisito di memoria:** l'applicazione deve fornire una struttura del blocco di controllo MD5, usata per mantenere lo stato tra le operazioni MD5.

## <a name="sha1-sha256512"></a>SHA1, SHA256/512

- **Algoritmo Standard:** NetX Crypto implementa SHA1/256/512 in base alla pubblicazione NIST FIPS 180-4: "*Secure Hash Standard",* disponibile all'indirizzo: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)
- **Dimensioni del blocco hash:**:
  - SHA1: valore hash a 160 bit
  - SHA 224: valore hash a 224 bit
  - SHA 256: valore hash a 256 bit
  - SHA 384: valore hash a 384 bit
  - SHA 512: valore hash a 512 bit
  - SHA 512/224: valore hash a 224 bit
  - SHA 512/256: valore hash a 256 bit

  In NetX Crypto le routine SHA256 vengono usate per usare SHA256 e SHA224. Le routine SHA512 vengono usate per la consegna di SHA512, SHA384, SHA512/224 e SHA512/256.
- **Requisito di memoria:** L'applicazione deve fornire una struttura di blocchi di controllo SHA per mantenere lo stato tra le operazioni.

## <a name="rsa"></a>RSA

- **Standard:** NetX Crypto implementa RSA in base allo standard "*PKCS #1 v2.2: RSA Cryptography Standard*", pubblicato come RFC 8017 e disponibile anche in: [https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf](https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura di blocchi di controllo RSA per mantenere lo stato tra le operazioni e fornire lo spazio del buffer "scratch" necessario per i calcoli intermedi.

## <a name="hmac"></a>HMAC

- **Standard:** NetX Crypto implementa HMAC in base a FIPS PUB 198-1: "*The Keyed-Hash Message Authentication Code (HMAC)*", disponibile in: [https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf](https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura del blocco di controllo HMAC per mantenere lo stato tra le operazioni. Il blocco di controllo effettivo fornito dipende dall'operazione hash sottostante desiderata(ad esempio SHA1, MD5).

## <a name="elliptic-curve"></a>Curva ellittica

- **Standard:** NetX Crypto implementa la curva ellittica. Le curve denominate supportate sono (solo campo primo):
  - P-192
  - P-224
  - P-256
  - P-384
  - P-521

   > [!TIP]
   > Il formato non compresso è supportato. Vedere le sezioni 2.3.3 e 2.3.4 di SEC1-v1: [http://www.secg.org/sec1-v2.pdf](http://www.secg.org/sec1-v2.pdf)

- **Requisito di memoria:** Nessuno

## <a name="ecdsa"></a>Ecdsa

- **Standard:** NetX Crypto implementa ECDSA in base a FIPS PUB 186-4: "*Digital Signature Standard (DSS)*", disponibile in: [https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf](https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura di blocchi di controllo ECDSA per mantenere lo stato tra le operazioni.

## <a name="ecdh"></a>ECDH

> [!IMPORTANT]
> In Azure RTOS 6.0, le routine ECDH devono essere usate solo per la crittografia ECDHE, perché ECDH con una chiave privata statica richiede che la convalida del punto di input sia sicura.

- **Standard:** NetX Crypto implementa ECDH in base a FIPS PUB 800-56Ar2: "Recommendation for Pair-Wise Key Establishment Schemes Using Discrete Logarithm Cryptography" (Raccomandazione per gli schemi di definizione delle chiavi di Pair-Wise che usano la crittografia logaritmo discreta), disponibile all'indirizzo: [https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura di blocchi di controllo ECDH per mantenere lo stato tra le operazioni.

## <a name="drbg"></a>DRBG

- **Standard:** NetX Crypto implementa DRBG in base a FIPS PUB 800-90Ar1: "Recommendation for Random Number Generation Using Deterministic Random Bit Generators" (Raccomandazione per la generazione di numeri casuali tramite generatori di bit casuali deterministici), disponibile in: [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura di blocchi di controllo DRBG per mantenere lo stato tra le operazioni.

## <a name="fips-compliant"></a>FIPS-Compliant

NetX Crypto FIPS 140-2