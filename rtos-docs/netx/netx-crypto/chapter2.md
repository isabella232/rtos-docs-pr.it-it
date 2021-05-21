---
title: Capitolo 2 - Installazione e uso di Azure RTOS NetX Crypto
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente NetX Crypto.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cd736cf6bbe15e1f407d1812072a4308435c8007
ms.sourcegitcommit: c2f5da5d6c7b230799f8fbd77885e9940acfbab4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2021
ms.locfileid: "110236153"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a><span data-ttu-id="c1c32-103">Capitolo 2 - Installazione e uso di Azure RTOS NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="c1c32-103">Chapter 2 - Installation and use of Azure RTOS NetX Crypto</span></span>

<span data-ttu-id="c1c32-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS netx crypto.</span><span class="sxs-lookup"><span data-stu-id="c1c32-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Crypto component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="c1c32-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="c1c32-105">Product Distribution</span></span>

<span data-ttu-id="c1c32-106">Azure RTOS NetX Crypto è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="c1c32-106">Azure RTOS NetX Crypto is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="c1c32-107">Il pacchetto include i file di origine, i file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c1c32-107">The package includes source files, include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="c1c32-108">**nx_crypto.h:** File di intestazione API pubblica Modulo NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="c1c32-108">**nx_crypto.h**: Public API header file NetX Crypto module</span></span>
- <span data-ttu-id="c1c32-109">**nx_crypto_\*.c/h:** File di origine C/H per NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="c1c32-109">**nx_crypto_\*.c/h**: C/H Source files for NetX Crypto</span></span>
- <span data-ttu-id="c1c32-110">**nx_crypto_port.h:** file di intestazione C contenente tutte le strutture e le definizioni di dati specifiche dello strumento di sviluppo e della destinazione.</span><span class="sxs-lookup"><span data-stu-id="c1c32-110">**nx_crypto_port.h**: C header file containing all development-tool and target specific data definitions and structures.</span></span>
- <span data-ttu-id="c1c32-111">**NetX_Crypto_User_Guide.pdf:** descrizione PDF del modulo di crittografia NetX.</span><span class="sxs-lookup"><span data-stu-id="c1c32-111">**NetX_Crypto_User_Guide.pdf**: PDF description of NetX Crypto Module.</span></span>

## <a name="netx-crypto-installation"></a><span data-ttu-id="c1c32-112">Installazione di NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="c1c32-112">NetX Crypto Installation</span></span>

<span data-ttu-id="c1c32-113">L'intera distribuzione indicata in precedenza **è disponibile crypto_libraries** directory, presente al livello radice del repository NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="c1c32-113">The entire distribution mentioned previously is available in **crypto_libraries** directory, present at root level of NetX Duo repository.</span></span>

<span data-ttu-id="c1c32-114">Per usare NetX Crypto, l'intera distribuzione indicata in precedenza deve essere copiata nello stesso livello di directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="c1c32-114">In order to use NetX Crypto, the entire distribution mentioned previously should be copied to the same directory level where NetX is installed.</span></span> <span data-ttu-id="c1c32-115">Ad esempio, se NetX è installato nella directory "\threadx\arm7\NetX", il nx_crypto *.*</span><span class="sxs-lookup"><span data-stu-id="c1c32-115">For example, if NetX is installed in the directory "\threadx\arm7\NetX" then the nx_crypto *.*</span></span> <span data-ttu-id="c1c32-116">le directory devono essere copiate in "\threadx\arm7\NetXCrypto".</span><span class="sxs-lookup"><span data-stu-id="c1c32-116">directories should be copied into "\threadx\arm7\NetXCrypto".</span></span>

<span data-ttu-id="c1c32-117">Per l'uso di NetX Crypto in modalità autonoma, l'intera distribuzione indicata in precedenza deve essere copiata nel progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1c32-117">For NetX Crypto to be used in standalone mode, the entire distribution mentioned previously should be copied to the application project.</span></span> <span data-ttu-id="c1c32-118">Ad **esempio crypto_libraries** directory deve essere copiata nel progetto di applicazione o un progetto di libreria con crypto_libraries **directory** deve essere creato e collegato al progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1c32-118">For example **crypto_libraries** directory should be copied to the application project or a library project with **crypto_libraries** directory should be created and linked to the application project.</span></span> 

## <a name="using-netx-crypto"></a><span data-ttu-id="c1c32-119">Uso di NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="c1c32-119">Using NetX Crypto</span></span>

<span data-ttu-id="c1c32-120">Questo capitolo descrive l'installazione, l'installazione e l'utilizzo Azure RTOS componente NetX Crypto.</span><span class="sxs-lookup"><span data-stu-id="c1c32-120">This chapter describes installation, setup, and usage of the Azure RTOS NetX Crypto component.</span></span> <span data-ttu-id="c1c32-121">Fondamentalmente, il codice dell'applicazione deve *includere nx_crypto.h.*</span><span class="sxs-lookup"><span data-stu-id="c1c32-121">Basically, the application code must include the *nx_crypto.h*.</span></span>  <span data-ttu-id="c1c32-122">Dopo *nx_crypto.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione NetX Crypto specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="c1c32-122">Once *nx_crypto.h* is included, the application code is then able to make the NetX Crypto function calls specified later in this guide.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="c1c32-123">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="c1c32-123">Configuration Options</span></span>

<span data-ttu-id="c1c32-124">Esistono diverse opzioni di configurazione per la compilazione di NetX Crypto.</span><span class="sxs-lookup"><span data-stu-id="c1c32-124">There are several configuration options for building NetX Crypto.</span></span> <span data-ttu-id="c1c32-125">Di seguito è riportato un elenco di tutte le opzioni, in cui ognuna è descritta in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="c1c32-125">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="c1c32-126">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: definita, questa opzione fornisce il modulo RSA massimo previsto, in bit.</span><span class="sxs-lookup"><span data-stu-id="c1c32-126">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: Defined, this option gives the maximum RSA modulus expected, in bits.</span></span> <span data-ttu-id="c1c32-127">Il valore predefinito è 4096 per un modulo a 4096 bit.</span><span class="sxs-lookup"><span data-stu-id="c1c32-127">The default value is 4096 for a 4096-bit modulus.</span></span> <span data-ttu-id="c1c32-128">Altri valori possono essere 3072, 2048 o 1024 (scelta non consigliata).</span><span class="sxs-lookup"><span data-stu-id="c1c32-128">Other values can be 3072, 2048, or 1024 (not recommended).</span></span>
- <span data-ttu-id="c1c32-129">**NX_CRYPTO_SELF_TEST**: definito, abilita i test self-test per il modulo NetX Crypto.</span><span class="sxs-lookup"><span data-stu-id="c1c32-129">**NX_CRYPTO_SELF_TEST**: Defined, enables self tests for NetX Crypto module.</span></span> <span data-ttu-id="c1c32-130">**NX_CRYPTO_FIPS** simbolo è ora deprecato e rinominato in **NX_CRYPTO_SELF_TEST**</span><span class="sxs-lookup"><span data-stu-id="c1c32-130">**NX_CRYPTO_FIPS** symbol is now deprecated and renamed to **NX_CRYPTO_SELF_TEST**</span></span>
- <span data-ttu-id="c1c32-131">**NX_CRYPTO_STANDALONE_ENABLE**: Defined consente l'uso di NetX Crypto in modalità autonoma (senza Azure RTOS).</span><span class="sxs-lookup"><span data-stu-id="c1c32-131">**NX_CRYPTO_STANDALONE_ENABLE**: Defined enables NetX Crypto to be used in standalone mode (without Azure RTOS).</span></span> <span data-ttu-id="c1c32-132">Per impostazione predefinita, questo simbolo non è definito.</span><span class="sxs-lookup"><span data-stu-id="c1c32-132">By default this symbol is not defined.</span></span>
