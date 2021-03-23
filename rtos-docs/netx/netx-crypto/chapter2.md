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
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a><span data-ttu-id="e3833-103">Capitolo 2-installazione e uso di Azure RTO NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="e3833-103">Chapter 2 - Installation and use of Azure RTOS NetX Crypto</span></span>

<span data-ttu-id="e3833-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente di crittografia NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="e3833-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Crypto component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="e3833-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="e3833-105">Product Distribution</span></span>

<span data-ttu-id="e3833-106">Azure RTO NetX Crypto è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="e3833-106">Azure RTOS NetX Crypto is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="e3833-107">Il pacchetto include i file di origine, i file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e3833-107">The package includes source files, include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="e3833-108">**nx_crypto. h**: file di intestazione dell'API public NETX modulo Crypto</span><span class="sxs-lookup"><span data-stu-id="e3833-108">**nx_crypto.h**: Public API header file NetX Crypto module</span></span>
- <span data-ttu-id="e3833-109">\*\*nx_crypto_ \*. c/h\*\*: file di origine c/h per la crittografia NETX</span><span class="sxs-lookup"><span data-stu-id="e3833-109">**nx_crypto_\*.c/h**: C/H Source files for NetX Crypto</span></span>
- <span data-ttu-id="e3833-110">**nx_crypto_port. h**: file di intestazione C contenente tutte le strutture e le definizioni dei dati specifici dello strumento di sviluppo e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e3833-110">**nx_crypto_port.h**: C header file containing all development-tool and target specific data definitions and structures.</span></span>
- <span data-ttu-id="e3833-111">**NetX_Crypto_User_Guide.pdf**: Descrizione PDF del modulo di crittografia NETX.</span><span class="sxs-lookup"><span data-stu-id="e3833-111">**NetX_Crypto_User_Guide.pdf**: PDF description of NetX Crypto Module.</span></span>

## <a name="netx-crypto-installation"></a><span data-ttu-id="e3833-112">Installazione della crittografia NetX</span><span class="sxs-lookup"><span data-stu-id="e3833-112">NetX Crypto Installation</span></span>

<span data-ttu-id="e3833-113">L'intera distribuzione citata in precedenza è disponibile nella directory **crypto_libraries** , presente al livello radice del repository NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="e3833-113">The entire distribution mentioned previously is available in **crypto_libraries** directory, present at root level of NetX Duo repository.</span></span>

<span data-ttu-id="e3833-114">Per poter usare la crittografia NetX, l'intera distribuzione indicata in precedenza deve essere copiata nello stesso livello di directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="e3833-114">In order to use NetX Crypto, the entire distribution mentioned previously should be copied to the same directory level where NetX is installed.</span></span> <span data-ttu-id="e3833-115">Ad esempio, se NetX è installato nella directory "\threadx\arm7\NetX", il nx_crypto *.*</span><span class="sxs-lookup"><span data-stu-id="e3833-115">For example, if NetX is installed in the directory "\threadx\arm7\NetX" then the nx_crypto *.*</span></span> <span data-ttu-id="e3833-116">le directory devono essere copiate in "\threadx\arm7\NetXCrypto".</span><span class="sxs-lookup"><span data-stu-id="e3833-116">directories should be copied into "\threadx\arm7\NetXCrypto".</span></span>

<span data-ttu-id="e3833-117">Per usare la crittografia NetX in modalità autonoma, l'intera distribuzione indicata in precedenza deve essere copiata nel progetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3833-117">For NetX Crypto to be used in standalone mode, the entire distribution mentioned previously should be copied to the application project.</span></span> <span data-ttu-id="e3833-118">Ad esempio, **crypto_libraries** directory deve essere copiata nel progetto di applicazione o un progetto di libreria con **crypto_libraries** directory deve essere creata e collegata al progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3833-118">For example **crypto_libraries** directory should be copied to the application project or a library project with **crypto_libraries** directory should be created and linked to the application project.</span></span> 

## <a name="using-netx-crypto"></a><span data-ttu-id="e3833-119">Uso della crittografia NetX</span><span class="sxs-lookup"><span data-stu-id="e3833-119">Using NetX Crypto</span></span>

<span data-ttu-id="e3833-120">L'uso di NetX Crypto è facile.</span><span class="sxs-lookup"><span data-stu-id="e3833-120">Using NetX Crypto is easy.</span></span> <span data-ttu-id="e3833-121">Fondamentalmente, il codice dell'applicazione deve includere il *nx_crypto. h*.</span><span class="sxs-lookup"><span data-stu-id="e3833-121">Basically, the application code must include the *nx_crypto.h*.</span></span>  <span data-ttu-id="e3833-122">Una volta incluso *nx_crypto. h* , il codice dell'applicazione è in grado di eseguire le chiamate della funzione di crittografia NETX specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="e3833-122">Once *nx_crypto.h* is included, the application code is then able to make the NetX Crypto function calls specified later in this guide.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="e3833-123">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="e3833-123">Configuration Options</span></span>

<span data-ttu-id="e3833-124">Per la compilazione di NetX Crypto sono disponibili diverse opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e3833-124">There are several configuration options for building NetX Crypto.</span></span> <span data-ttu-id="e3833-125">Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="e3833-125">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="e3833-126">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: definito, questa opzione fornisce il modulo RSA massimo previsto in bit.</span><span class="sxs-lookup"><span data-stu-id="e3833-126">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: Defined, this option gives the maximum RSA modulus expected, in bits.</span></span> <span data-ttu-id="e3833-127">Il valore predefinito è 4096 per un modulo a 4096 bit.</span><span class="sxs-lookup"><span data-stu-id="e3833-127">The default value is 4096 for a 4096-bit modulus.</span></span> <span data-ttu-id="e3833-128">Gli altri valori possono essere 3072, 2048 o 1024 (scelta non consigliata).</span><span class="sxs-lookup"><span data-stu-id="e3833-128">Other values can be 3072, 2048, or 1024 (not recommended).</span></span>
- <span data-ttu-id="e3833-129">**NX_CRYPTO_FIPS**: definito, questa opzione Abilita le funzionalità di sicurezza aggiuntive necessarie per l'utilizzo FIPS-Compliant.</span><span class="sxs-lookup"><span data-stu-id="e3833-129">**NX_CRYPTO_FIPS**: Defined, this option enables extra security features required for FIPS-Compliant usage.</span></span> <span data-ttu-id="e3833-130">Questa opzione non è abilitata per la compilazione non FIPS.</span><span class="sxs-lookup"><span data-stu-id="e3833-130">This option is not enabled for non-FIPS build.</span></span>
- <span data-ttu-id="e3833-131">**NX_CRYPTO_STANDALONE_ENABLE**: defined Abilita l'uso della crittografia NETX in modalità autonoma (senza Azure RTO).</span><span class="sxs-lookup"><span data-stu-id="e3833-131">**NX_CRYPTO_STANDALONE_ENABLE**: Defined enables NetX Crypto to be used in standalone mode (without Azure RTOS).</span></span> <span data-ttu-id="e3833-132">Per impostazione predefinita, questo simbolo non è definito.</span><span class="sxs-lookup"><span data-stu-id="e3833-132">By default this symbol is not defined.</span></span>
