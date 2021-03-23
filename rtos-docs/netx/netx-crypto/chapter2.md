---
title: Capitolo 2-installazione e uso di Azure RTO NetX Crypto
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente di crittografia NetX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1616667c5efd73229ed69bcd4e5de5f80e5826f9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822721"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a>Capitolo 2-installazione e uso di Azure RTO NetX Crypto

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente di crittografia NetX di Azure RTO.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO NetX Crypto è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include i file di origine, i file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_crypto. h**: file di intestazione dell'API public NETX modulo Crypto
- **nx_crypto_ *. c/h**: file di origine c/h per la crittografia NETX
- **nx_crypto_port. h**: file di intestazione C contenente tutte le strutture e le definizioni dei dati specifici dello strumento di sviluppo e di destinazione.
- **NetX_Crypto_User_Guide.pdf**: Descrizione PDF del modulo di crittografia NETX.

## <a name="netx-crypto-installation"></a>Installazione della crittografia NetX

L'intera distribuzione citata in precedenza è disponibile nella directory **crypto_libraries** , presente al livello radice del repository NETX Duo.

Per poter usare la crittografia NetX, l'intera distribuzione indicata in precedenza deve essere copiata nello stesso livello di directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "\threadx\arm7\NetX", il nx_crypto *.* le directory devono essere copiate in "\threadx\arm7\NetXCrypto".

Per usare la crittografia NetX in modalità autonoma, l'intera distribuzione indicata in precedenza deve essere copiata nel progetto di applicazione. Ad esempio, **crypto_libraries** directory deve essere copiata nel progetto di applicazione o un progetto di libreria con **crypto_libraries** directory deve essere creata e collegata al progetto dell'applicazione. 

## <a name="using-netx-crypto"></a>Uso della crittografia NetX

L'uso di NetX Crypto è facile. Fondamentalmente, il codice dell'applicazione deve includere il *nx_crypto. h*.  Una volta incluso *nx_crypto. h* , il codice dell'applicazione è in grado di eseguire le chiamate della funzione di crittografia NETX specificate più avanti in questa guida.

## <a name="configuration-options"></a>Opzioni di configurazione

Per la compilazione di NetX Crypto sono disponibili diverse opzioni di configurazione. Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:

- **NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: definito, questa opzione fornisce il modulo RSA massimo previsto in bit. Il valore predefinito è 4096 per un modulo a 4096 bit. Gli altri valori possono essere 3072, 2048 o 1024 (scelta non consigliata).
- **NX_CRYPTO_FIPS**: definito, questa opzione Abilita le funzionalità di sicurezza aggiuntive necessarie per l'utilizzo FIPS-Compliant. Questa opzione non è abilitata per la compilazione non FIPS.
- **NX_CRYPTO_STANDALONE_ENABLE**: defined Abilita l'uso della crittografia NETX in modalità autonoma (senza Azure RTO). Per impostazione predefinita, questo simbolo non è definito.
