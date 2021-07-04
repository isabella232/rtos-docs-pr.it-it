---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX Crypto
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente NetX Crypto.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3323af5eaf31ac9c167966522df6477c82e99fdc
ms.sourcegitcommit: c98e5360c9cedbe773af5a44f5163f563c85b570
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/24/2021
ms.locfileid: "110337007"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a>Capitolo 2 - Installazione e uso di Azure RTOS NetX Crypto

Questo capitolo descrive l'installazione, l'installazione e l'uso del Azure RTOS netx crypto.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS Crypto NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include i file di origine, i file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_crypto.h:** file di intestazione dell'API pubblica Modulo NetX Crypto
- **nx_crypto_*.c/h:** file di origine C/H per NetX Crypto
- **nx_crypto_port.h:** file di intestazione C contenente tutte le strutture e le definizioni di dati specifiche dello strumento di sviluppo e della destinazione.
- **NetX_Crypto_User_Guide.pdf**: Descrizione PDF del modulo Crypto NetX.

## <a name="netx-crypto-installation"></a>Installazione di NetX Crypto

L'intera distribuzione indicata in precedenza **è disponibile crypto_libraries** directory, presente al livello radice del repository NetX Duo.

Per usare NetX Crypto, l'intera distribuzione indicata in precedenza deve essere copiata nello stesso livello di directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "\threadx\arm7\NetX", il nx_crypto *.* le directory devono essere copiate in "\threadx\arm7\NetXCrypto".

Per l'uso di NetX Crypto in modalità autonoma, l'intera distribuzione indicata in precedenza deve essere copiata nel progetto dell'applicazione. Ad **esempio crypto_libraries** la directory deve essere copiata nel progetto dell'applicazione o deve essere creato un progetto di libreria con **una** directory crypto_libraries collegata al progetto dell'applicazione. 

## <a name="using-netx-crypto"></a>Uso di NetX Crypto

Il codice dell'applicazione deve includere *nx_crypto.h.*  Dopo *nx_crypto.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione NetX Crypto specificate più avanti in questa guida.

## <a name="configuration-options"></a>Opzioni di configurazione

Esistono diverse opzioni di configurazione per la compilazione di NetX Crypto. Di seguito è riportato un elenco di tutte le opzioni, in cui ognuna è descritta in dettaglio:

- **NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: definita, questa opzione fornisce il modulo RSA massimo previsto, in bit. Il valore predefinito è 4096 per un modulo a 4096 bit. Altri valori possono essere 3072, 2048 o 1024 (scelta non consigliata).
- **NX_CRYPTO_SELF_TEST**: definito, abilita i test self-test per il modulo NetX Crypto. **NX_CRYPTO_FIPS** simbolo è ora deprecato e rinominato **in NX_CRYPTO_SELF_TEST**
- **NX_CRYPTO_STANDALONE_ENABLE**: Defined consente l'uso di NetX Crypto in modalità autonoma (senza Azure RTOS). Per impostazione predefinita, questo simbolo non è definito.
