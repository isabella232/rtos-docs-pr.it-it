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
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a><span data-ttu-id="5353c-103">Capitolo 2 - Installazione e uso di Azure RTOS NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="5353c-103">Chapter 2 - Installation and use of Azure RTOS NetX Crypto</span></span>

<span data-ttu-id="5353c-104">Questo capitolo descrive l'installazione, l'installazione e l'uso del Azure RTOS netx crypto.</span><span class="sxs-lookup"><span data-stu-id="5353c-104">This chapter describes installation, setup, and usage of the Azure RTOS NetX Crypto component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="5353c-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="5353c-105">Product Distribution</span></span>

<span data-ttu-id="5353c-106">Azure RTOS Crypto NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="5353c-106">Azure RTOS NetX Crypto is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="5353c-107">Il pacchetto include i file di origine, i file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5353c-107">The package includes source files, include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="5353c-108">**nx_crypto.h:** file di intestazione dell'API pubblica Modulo NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="5353c-108">**nx_crypto.h**: Public API header file NetX Crypto module</span></span>
- <span data-ttu-id="5353c-109">**nx_crypto_\*.c/h:** file di origine C/H per NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="5353c-109">**nx_crypto_\*.c/h**: C/H Source files for NetX Crypto</span></span>
- <span data-ttu-id="5353c-110">**nx_crypto_port.h:** file di intestazione C contenente tutte le strutture e le definizioni di dati specifiche dello strumento di sviluppo e della destinazione.</span><span class="sxs-lookup"><span data-stu-id="5353c-110">**nx_crypto_port.h**: C header file containing all development-tool and target specific data definitions and structures.</span></span>
- <span data-ttu-id="5353c-111">**NetX_Crypto_User_Guide.pdf**: Descrizione PDF del modulo Crypto NetX.</span><span class="sxs-lookup"><span data-stu-id="5353c-111">**NetX_Crypto_User_Guide.pdf**: PDF description of NetX Crypto Module.</span></span>

## <a name="netx-crypto-installation"></a><span data-ttu-id="5353c-112">Installazione di NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="5353c-112">NetX Crypto Installation</span></span>

<span data-ttu-id="5353c-113">L'intera distribuzione indicata in precedenza **è disponibile crypto_libraries** directory, presente al livello radice del repository NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5353c-113">The entire distribution mentioned previously is available in **crypto_libraries** directory, present at root level of NetX Duo repository.</span></span>

<span data-ttu-id="5353c-114">Per usare NetX Crypto, l'intera distribuzione indicata in precedenza deve essere copiata nello stesso livello di directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="5353c-114">In order to use NetX Crypto, the entire distribution mentioned previously should be copied to the same directory level where NetX is installed.</span></span> <span data-ttu-id="5353c-115">Ad esempio, se NetX è installato nella directory "\threadx\arm7\NetX", il nx_crypto *.*</span><span class="sxs-lookup"><span data-stu-id="5353c-115">For example, if NetX is installed in the directory "\threadx\arm7\NetX" then the nx_crypto *.*</span></span> <span data-ttu-id="5353c-116">le directory devono essere copiate in "\threadx\arm7\NetXCrypto".</span><span class="sxs-lookup"><span data-stu-id="5353c-116">directories should be copied into "\threadx\arm7\NetXCrypto".</span></span>

<span data-ttu-id="5353c-117">Per l'uso di NetX Crypto in modalità autonoma, l'intera distribuzione indicata in precedenza deve essere copiata nel progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5353c-117">For NetX Crypto to be used in standalone mode, the entire distribution mentioned previously should be copied to the application project.</span></span> <span data-ttu-id="5353c-118">Ad **esempio crypto_libraries** la directory deve essere copiata nel progetto dell'applicazione o deve essere creato un progetto di libreria con **una** directory crypto_libraries collegata al progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5353c-118">For example **crypto_libraries** directory should be copied to the application project or a library project with **crypto_libraries** directory should be created and linked to the application project.</span></span> 

## <a name="using-netx-crypto"></a><span data-ttu-id="5353c-119">Uso di NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="5353c-119">Using NetX Crypto</span></span>

<span data-ttu-id="5353c-120">Il codice dell'applicazione deve includere *nx_crypto.h.*</span><span class="sxs-lookup"><span data-stu-id="5353c-120">The application code must include the *nx_crypto.h*.</span></span>  <span data-ttu-id="5353c-121">Dopo *nx_crypto.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione NetX Crypto specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="5353c-121">Once *nx_crypto.h* is included, the application code is then able to make the NetX Crypto function calls specified later in this guide.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="5353c-122">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="5353c-122">Configuration Options</span></span>

<span data-ttu-id="5353c-123">Esistono diverse opzioni di configurazione per la compilazione di NetX Crypto.</span><span class="sxs-lookup"><span data-stu-id="5353c-123">There are several configuration options for building NetX Crypto.</span></span> <span data-ttu-id="5353c-124">Di seguito è riportato un elenco di tutte le opzioni, in cui ognuna è descritta in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="5353c-124">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="5353c-125">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: definita, questa opzione fornisce il modulo RSA massimo previsto, in bit.</span><span class="sxs-lookup"><span data-stu-id="5353c-125">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: Defined, this option gives the maximum RSA modulus expected, in bits.</span></span> <span data-ttu-id="5353c-126">Il valore predefinito è 4096 per un modulo a 4096 bit.</span><span class="sxs-lookup"><span data-stu-id="5353c-126">The default value is 4096 for a 4096-bit modulus.</span></span> <span data-ttu-id="5353c-127">Altri valori possono essere 3072, 2048 o 1024 (scelta non consigliata).</span><span class="sxs-lookup"><span data-stu-id="5353c-127">Other values can be 3072, 2048, or 1024 (not recommended).</span></span>
- <span data-ttu-id="5353c-128">**NX_CRYPTO_SELF_TEST**: definito, abilita i test self-test per il modulo NetX Crypto.</span><span class="sxs-lookup"><span data-stu-id="5353c-128">**NX_CRYPTO_SELF_TEST**: Defined, enables self tests for NetX Crypto module.</span></span> <span data-ttu-id="5353c-129">**NX_CRYPTO_FIPS** simbolo è ora deprecato e rinominato **in NX_CRYPTO_SELF_TEST**</span><span class="sxs-lookup"><span data-stu-id="5353c-129">**NX_CRYPTO_FIPS** symbol is now deprecated and renamed to **NX_CRYPTO_SELF_TEST**</span></span>
- <span data-ttu-id="5353c-130">**NX_CRYPTO_STANDALONE_ENABLE**: Defined consente l'uso di NetX Crypto in modalità autonoma (senza Azure RTOS).</span><span class="sxs-lookup"><span data-stu-id="5353c-130">**NX_CRYPTO_STANDALONE_ENABLE**: Defined enables NetX Crypto to be used in standalone mode (without Azure RTOS).</span></span> <span data-ttu-id="5353c-131">Per impostazione predefinita, questo simbolo non è definito.</span><span class="sxs-lookup"><span data-stu-id="5353c-131">By default this symbol is not defined.</span></span>
