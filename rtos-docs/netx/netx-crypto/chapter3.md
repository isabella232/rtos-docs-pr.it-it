---
title: Capitolo 3-Descrizione funzionale di Azure RTO NetX Crypto
description: Questo capitolo contiene una descrizione funzionale della crittografia NetX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4ecdbfe99daa000d109908f834b139dcaf321491
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821497"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-crypto"></a>Capitolo 3-Descrizione funzionale di Azure RTO NetX Crypto

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Questo capitolo contiene una descrizione funzionale della crittografia NetX di Azure RTO. Esistono due tipi principali di esecuzione del programma in un'applicazione NetX Crypto: inizializzazione e chiamate dell'interfaccia dell'applicazione.

*La crittografia NetX può essere usata come libreria di crittografia autonoma oppure può essere usata con ThreadX, NetX e/o NetX Secure.*

## <a name="aes"></a>AES

- **Algoritmo standard:**: NETX Crypto implementa AES in base al NIST FIPS 197, disponibile all'indirizzo: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197.pdf)
- **Lunghezze di chiave supportate**: 128, 192, 256
- **Modalità supportate**:
  - CBC, CTR, (lunghezza della chiave 128-, 192-, 256-bit)
  - XCBC (solo lunghezza della chiave 128 bit),
  - CCM8 (solo lunghezza chiave 128 bit)
- **Requisiti di memoria**: l'applicazione specifica il buffer di input e il buffer di output e una struttura di controllo AES. La struttura di controllo AES mantiene lo stato dell'algoritmo AES tra le chiamate all'API. Il buffer di input contiene i dati da crittografare o decrittografare e può essere di dimensioni arbitrarie. Il buffer di output viene usato da AES per archiviare i dati elaborati da AES. La dimensione del buffer di output non deve essere inferiore alla dimensione del buffer di input e deve essere un multiplo di 16 byte, ovvero la dimensione del blocco AES. I buffer di input e di output devono essere di memoria contigua e non possono sovrapporsi, tranne nel caso speciale di crittografia sul posto (usando la stessa memoria per l'input e l'output). Quando si esegue la crittografia sul posto, il buffer di output inizia esattamente nella stessa posizione del buffer di input e non deve essere inferiore al buffer di input. Quando la crittografia AES opera sul posto, non è necessaria alcuna memoria aggiuntiva.

## <a name="3des"></a>3DES

- **Algoritmo standard**: NETX Crypto implementa tripla des (TDES, noto anche come 3DES) in base alla pubblicazione speciale NIST 800-67 Rev 2: *"Recommendataion per Triple Data Encryption Algorithm (TDES) Block Cipher"*, disponibile in: [https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final](https://csrc.nist.gov/publications/detail/sp/800-67/rev-2/final)
- **Lunghezza della chiave supportata**: 64 * 3 = 192
- **Memoria Requreiment:**: None

In NetX Crypto il termine "3DES" viene usato in modo interscambiabile con "TDES".

## <a name="md5"></a>MD5

- **Algoritmo standard**: NETX Crypto implementa MD5 in base a RFC 1321: *"algoritmo MD5 Message-Digest"*
- **Requisito di memoria**: l'applicazione deve fornire una struttura del blocco di controllo MD5, usata per mantenere lo stato tra le operazioni MD5.

## <a name="sha1-sha256512"></a>SHA1, SHA256/512

- **Standard algoritmo:** NetX Crypto implementa SHA1/256/512 in base alla pubblicazione FIPS del NIST 180-4: "*Secure hash standard*", disponibile in: [http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)
- **Dimensioni blocco hash:**:
  - SHA1: valore hash bits 160
  - SHA 224: valore hash bits 224
  - SHA 256: valore hash bits 256
  - SHA 384: valore hash bits 384
  - SHA 512: valore hash bits 512
  - Valore hash SHA 512/224:224 BITS
  - Valore hash SHA 512/256:256 bits

  In NetX Crypto le routine SHA256 vengono usate per hadn SHA256 e SHA224. Le routine SHA512 vengono usate per passare SHA512, SHA384, SHA512/224 e SHA512/256.
- **Requisito di memoria:** L'applicazione deve fornire una struttura del blocco di controllo SHA per mantenere lo stato tra le operazioni.

## <a name="rsa"></a>RSA

- **Standard:** NetX Crypto implementa RSA in base allo standard "*PKCS #1 v 2.2: RSA Cryptography Standard*", pubblicato come RFC 8017 ed è disponibile anche in: [https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf](https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura del blocco di controllo RSA per mantenere lo stato tra le operazioni e fornire lo spazio del buffer "Scratch" necessario per i calcoli intermedi.

## <a name="hmac"></a>HMAC

- **Standard:** NetX Crypto implementa HMAC in base a FIPS PUB 198-1: "*The Keyed-Hash Message Authentication Code (HMAC)*", disponibile all'indirizzo: [https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf](https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura del blocco di controllo HMAC per mantenere lo stato tra le operazioni. Il blocco di controllo effettivo fornito dipende dall'operazione hash sottostante desiderata (ad esempio, SHA1, MD5).

## <a name="elliptic-curve"></a>Curva ellittica

- **Standard:** NetX Crypto implementa la curva ellittica. Le curve denominate supportate sono (solo campo primo):
  - P-192
  - P-224
  - P-256
  - P-384
  - P-521

   > [!TIP]
   > Il formato non compresso è supportato. Vedere la sezione 2.3.3 e 2.3.4 di SEC1-V1: [http://www.secg.org/sec1-v2.pdf](http://www.secg.org/sec1-v2.pdf)

- **Requisito di memoria:** Nessuno

## <a name="ecdsa"></a>ECDSA

- **Standard:** NetX Crypto implementa ECDSA in base a FIPS PUB 186-4: "*Digital Signature Standard (DSS)*", disponibile all'indirizzo: [https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf](https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.186-4.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura del blocco di controllo ECDSA per la gestione dello stato tra le operazioni.

## <a name="ecdh"></a>ECDH

> [!IMPORTANT]
> In Azure RTO 6,0, le routine ECDH devono essere usate solo per la crittografia ECDHE perché ECDH con una chiave privata statica richiede la sicurezza della convalida dei punti di input.

- **Standard:** NetX Crypto implementa ECDH in base a FIPS PUB 800-56Ar2: "Recommendation for Pair-Wise Key establishing schemes using discrete logaritmo Cryptography", disponibile in: [https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-56ar2.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura del blocco di controllo ECDH per la gestione dello stato tra le operazioni.

## <a name="drbg"></a>DRBG

- **Standard:** NetX Crypto implementa DRBG in base a FIPS PUB 800-90Ar1: "raccomandazione per la generazione di numeri casuali tramite generatori di bit casuali deterministici", disponibile in: [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf)
- **Requisito di memoria:** L'applicazione deve fornire una struttura del blocco di controllo DRBG per la gestione dello stato tra le operazioni.

## <a name="fips-compliant"></a>FIPS-Compliant

Crittografia FIPS 140-2 di NetX