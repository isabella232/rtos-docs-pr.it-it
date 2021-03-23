---
title: Capitolo 2-installazione e uso di Azure RTO NetX LWM2M
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente LWM2M NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8c13d3b092d3a5b59bd0369f6ffc162509d02590
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822604"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-lwm2m"></a><span data-ttu-id="790ae-103">Capitolo 2-installazione e uso di Azure RTO NetX LWM2M</span><span class="sxs-lookup"><span data-stu-id="790ae-103">Chapter 2 - Installation and use of Azure RTOS NetX LWM2M</span></span>

<span data-ttu-id="790ae-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente LWM2M NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="790ae-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX LWM2M component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="790ae-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="790ae-105">Product Distribution</span></span>

<span data-ttu-id="790ae-106">NetX LWM2M è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="790ae-106">NetX LWM2M is available at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span> <span data-ttu-id="790ae-107">Il pacchetto include tre file di origine, uno di inclusione e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="790ae-107">The package includes three source files, one include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="790ae-108">**nx_lwm2m_client. h**: file di intestazione per il client Lwm2m di NETX</span><span class="sxs-lookup"><span data-stu-id="790ae-108">**nx_lwm2m_client.h**: Header file for the NetX LWM2M Client</span></span>

- <span data-ttu-id="790ae-109">\*\*nx_lwm2m_ \*. c/h\*\*: file di origine c/h per NETX lwm2m</span><span class="sxs-lookup"><span data-stu-id="790ae-109">**nx_lwm2m_\*.c/h**: C/H Source files for NetX LWM2M</span></span>

- <span data-ttu-id="790ae-110">**demo_netx_lwm2m_client. c**: file di origine c per NETX demo client lwm2m</span><span class="sxs-lookup"><span data-stu-id="790ae-110">**demo_netx_lwm2m_client.c**: C Source file for NetX LWM2M Client Demo</span></span>

- <span data-ttu-id="790ae-111">**NetX_LWM2M_User_Guide.pdf**: Descrizione PDF del prodotto NETX LWM2M</span><span class="sxs-lookup"><span data-stu-id="790ae-111">**NetX_LWM2M_User_Guide.pdf**: PDF description of NetX LWM2M product</span></span>

## <a name="netx-lwm2m-installation"></a><span data-ttu-id="790ae-112">Installazione di NetX LWM2M</span><span class="sxs-lookup"><span data-stu-id="790ae-112">NetX LWM2M Installation</span></span>

<span data-ttu-id="790ae-113">Per poter usare NetX LWM2M, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="790ae-113">In order to use NetX LWM2M, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="790ae-114">Ad esempio, se NetX è installato nella directory "*\\ threadX \\ ARM7 \\ green*", il *nx_lwm2m&#42;. &#42;* i file devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="790ae-114">For example, if NetX is installed in the directory "*\\threadx\\arm7\\green*" then the *nx_lwm2m&#42;.&#42;* files should be copied into this directory.</span></span>

## <a name="using-netx-lwm2m"></a><span data-ttu-id="790ae-115">Uso di NetX LWM2M</span><span class="sxs-lookup"><span data-stu-id="790ae-115">Using NetX LWM2M</span></span>

<span data-ttu-id="790ae-116">L'uso di NetX LWM2M è facile.</span><span class="sxs-lookup"><span data-stu-id="790ae-116">Using NetX LWM2M is easy.</span></span> <span data-ttu-id="790ae-117">In pratica, il codice dell'applicazione deve includere *nx_lwm2m_client. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter usare threadX e NETX.</span><span class="sxs-lookup"><span data-stu-id="790ae-117">Basically, the application code must include *nx_lwm2m_client.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX.</span></span> <span data-ttu-id="790ae-118">Una volta incluso *nx_lwm2m_client. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione lwm2m NETX specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="790ae-118">Once *nx_lwm2m_client.h* is included, the application code is then able to make the NetX LWM2M function calls specified later in this guide.</span></span> <span data-ttu-id="790ae-119">L'applicazione deve inoltre importare i file di *nx_lwm2m&#42;. &#42;* nella libreria NETX.</span><span class="sxs-lookup"><span data-stu-id="790ae-119">The application must also import the *nx_lwm2m&#42;.&#42;* files into the NetX library.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="790ae-120">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="790ae-120">Configuration Options</span></span>

<span data-ttu-id="790ae-121">Sono disponibili diverse opzioni di configurazione quando si compila la libreria client di LWM2M e l'applicazione usando il client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="790ae-121">There are several configuration options when building the LWM2M Client library and the application using the LWM2M Client.</span></span> <span data-ttu-id="790ae-122">Le opzioni di configurazione possono essere definite nell'origine dell'applicazione, nella riga di comando, se non diversamente specificato.</span><span class="sxs-lookup"><span data-stu-id="790ae-122">The configuration options can be defined in the application source, on the command line, unless otherwise specified.</span></span>

### <a name="nx_lwm2m_client_disable_error_checking"></a><span data-ttu-id="790ae-123">NX_LWM2M_CLIENT_DISABLE_ERROR_CHECKING</span><span class="sxs-lookup"><span data-stu-id="790ae-123">NX_LWM2M_CLIENT_DISABLE_ERROR_CHECKING</span></span>

<span data-ttu-id="790ae-124">Definito, rimuove l'API di base per il controllo degli errori del client LWM2M e migliora le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="790ae-124">Defined, removes the basic LWM2M Client error checking API and improves performance.</span></span> <span data-ttu-id="790ae-125">I codici restituiti dell'API non interessati dalla disabilitazione del controllo degli errori sono elencati in grassetto nella definizione dell'API.</span><span class="sxs-lookup"><span data-stu-id="790ae-125">API return codes not affected by disabling error checking are listed in bold typeface in the API definition.</span></span>

### <a name="nx_lwm2m_client_disable_float"></a><span data-ttu-id="790ae-126">NX_LWM2M_CLIENT_DISABLE_FLOAT</span><span class="sxs-lookup"><span data-stu-id="790ae-126">NX_LWM2M_CLIENT_DISABLE_FLOAT</span></span>

<span data-ttu-id="790ae-127">Definito, rimuove il supporto dei valori numerici a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="790ae-127">Defined, removes the support of floating point numbers values.</span></span> <span data-ttu-id="790ae-128">Se disabilitato, il client LWM2M non è in grado di supportare risorse con tipo di dati float.</span><span class="sxs-lookup"><span data-stu-id="790ae-128">When disabled the LWM2M Client cannot support Resources with Float data type.</span></span>

### <a name="nx_lwm2m_client_disable_float64"></a><span data-ttu-id="790ae-129">NX_LWM2M_CLIENT_DISABLE_FLOAT64</span><span class="sxs-lookup"><span data-stu-id="790ae-129">NX_LWM2M_CLIENT_DISABLE_FLOAT64</span></span>

<span data-ttu-id="790ae-130">Definito, rimuove il supporto dei valori numerici a virgola mobile a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="790ae-130">Defined, removes the support of 64-bit floating point numbers values.</span></span> <span data-ttu-id="790ae-131">Il client LWM2M può comunque ricevere messaggi TLV contenenti numeri a virgola mobile a 64 bit, ma i valori vengono convertiti in virgola mobile a 32 bit per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="790ae-131">The LWM2M Client can still receive TLV messages containing 64-bit floating numbers, but the values are converted to 32-bit floating point for processing.</span></span>

### <a name="nx_lwm2m_client_priority"></a><span data-ttu-id="790ae-132">NX_LWM2M_CLIENT_PRIORITY</span><span class="sxs-lookup"><span data-stu-id="790ae-132">NX_LWM2M_CLIENT_PRIORITY</span></span>

<span data-ttu-id="790ae-133">Specifica la priorità del thread del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="790ae-133">Specifies the priority of the LWM2M Client thread.</span></span> <span data-ttu-id="790ae-134">Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.</span><span class="sxs-lookup"><span data-stu-id="790ae-134">By default, this value is defined as 16 to specify priority 16.</span></span>

### <a name="nx_lwm2m_client_max_device_errors"></a><span data-ttu-id="790ae-135">NX_LWM2M_CLIENT_MAX_DEVICE_ERRORS</span><span class="sxs-lookup"><span data-stu-id="790ae-135">NX_LWM2M_CLIENT_MAX_DEVICE_ERRORS</span></span>

<span data-ttu-id="790ae-136">Specifica il numero massimo di codici di errore archiviati dall'oggetto dispositivo.</span><span class="sxs-lookup"><span data-stu-id="790ae-136">Specifies the maximum number of error codes stored by the Device Object.</span></span> <span data-ttu-id="790ae-137">Il valore predefinito è 8.</span><span class="sxs-lookup"><span data-stu-id="790ae-137">The default value is 8.</span></span>

### <a name="nx_lwm2m_client_max_security_instances"></a><span data-ttu-id="790ae-138">NX_LWM2M_CLIENT_MAX_SECURITY_INSTANCES</span><span class="sxs-lookup"><span data-stu-id="790ae-138">NX_LWM2M_CLIENT_MAX_SECURITY_INSTANCES</span></span>

<span data-ttu-id="790ae-139">Specifica il numero massimo di istanze di oggetti di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="790ae-139">Specifies the maximum number of Security Object Instances.</span></span> <span data-ttu-id="790ae-140">Il valore predefinito è 2 per supportare un server bootstrap e un server standard.</span><span class="sxs-lookup"><span data-stu-id="790ae-140">The default value is 2 for supporting a Bootstrap Server and a standard Server.</span></span>

### <a name="nx_lwm2m_client_max_server_instances"></a><span data-ttu-id="790ae-141">NX_LWM2M_CLIENT_MAX_SERVER_INSTANCES</span><span class="sxs-lookup"><span data-stu-id="790ae-141">NX_LWM2M_CLIENT_MAX_SERVER_INSTANCES</span></span>

<span data-ttu-id="790ae-142">Specifica il numero massimo di istanze di oggetti server.</span><span class="sxs-lookup"><span data-stu-id="790ae-142">Specifies the maximum number of Server Object Instances.</span></span> <span data-ttu-id="790ae-143">Il valore predefinito è 1 per il supporto di un singolo server standard.</span><span class="sxs-lookup"><span data-stu-id="790ae-143">The default value is 1 for supporting a single standard Server.</span></span>

### <a name="nx_lwm2m_client_max_server_uri"></a><span data-ttu-id="790ae-144">NX_LWM2M_CLIENT_MAX_SERVER_URI</span><span class="sxs-lookup"><span data-stu-id="790ae-144">NX_LWM2M_CLIENT_MAX_SERVER_URI</span></span>

<span data-ttu-id="790ae-145">Specifica la lunghezza massima di un URI del server, incluso il carattere null di terminazione.</span><span class="sxs-lookup"><span data-stu-id="790ae-145">Specifies the maximum length of a server URI, including terminating nil character.</span></span> <span data-ttu-id="790ae-146">Il valore predefinito è 128.</span><span class="sxs-lookup"><span data-stu-id="790ae-146">The default value is 128.</span></span>

### <a name="nx_lwm2m_client_max_access_control_instances"></a><span data-ttu-id="790ae-147">NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_INSTANCES</span><span class="sxs-lookup"><span data-stu-id="790ae-147">NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_INSTANCES</span></span>

<span data-ttu-id="790ae-148">Specifica il numero massimo di istanze del controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="790ae-148">Specifies the maximum number of Access Control Instances.</span></span> <span data-ttu-id="790ae-149">Il valore predefinito è 0, che disabilita il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="790ae-149">The default value is 0, which disables access control.</span></span> <span data-ttu-id="790ae-150">Se l'applicazione supporta più di un server LWM2M, il numero massimo di istanze del controllo di accesso deve essere impostato sul numero massimo di istanze di oggetti che il client LWM2M supporterà, perché è necessario creare un'istanza del controllo di accesso per ogni istanza dell'oggetto, ad eccezione delle istanze degli oggetti di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="790ae-150">If the application supports more than one LWM2M Server, the maximum number of Access Control Instances must be set to the maximum number of Object Instances that the LWM2M Client will support, as one Access Control Instance must be created for each Object Instance (except for the Security Object Instances).</span></span>

### <a name="nx_lwm2m_client_max_access_control_acls"></a><span data-ttu-id="790ae-151">NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_ACLS</span><span class="sxs-lookup"><span data-stu-id="790ae-151">NX_LWM2M_CLIENT_MAX_ACCESS_CONTROL_ACLS</span></span>

<span data-ttu-id="790ae-152">Specifica il numero massimo di risorse ACL per ogni istanza del controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="790ae-152">Specifies the maximum number of ACL resources per Access Control Instance.</span></span> <span data-ttu-id="790ae-153">Il valore predefinito è 4.</span><span class="sxs-lookup"><span data-stu-id="790ae-153">The default value is 4.</span></span>

### <a name="nx_lwm2m_client_max_notifications"></a><span data-ttu-id="790ae-154">NX_LWM2M_CLIENT_MAX_NOTIFICATIONS</span><span class="sxs-lookup"><span data-stu-id="790ae-154">NX_LWM2M_CLIENT_MAX_NOTIFICATIONS</span></span>

<span data-ttu-id="790ae-155">Specifica il numero massimo di notifiche che il client LWM2M supporterà.</span><span class="sxs-lookup"><span data-stu-id="790ae-155">Specifies the maximum number of notifications that the LWM2M Client will support.</span></span> <span data-ttu-id="790ae-156">Un server LWM2M può impostare notifiche su oggetti, istanze di oggetti e risorse.</span><span class="sxs-lookup"><span data-stu-id="790ae-156">A LWM2M Server can set notifications on Objects, Object Instances, and Resources.</span></span> <span data-ttu-id="790ae-157">Il valore predefinito è 8.</span><span class="sxs-lookup"><span data-stu-id="790ae-157">The default value is 8.</span></span>

### <a name="nx_lwm2m_client_max_resources"></a><span data-ttu-id="790ae-158">NX_LWM2M_CLIENT_MAX_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="790ae-158">NX_LWM2M_CLIENT_MAX_RESOURCES</span></span>

<span data-ttu-id="790ae-159">Specifica il numero massimo di risorse per oggetto.</span><span class="sxs-lookup"><span data-stu-id="790ae-159">Specifies the maximum number of Resources per Object.</span></span> <span data-ttu-id="790ae-160">Il valore predefinito è (32).</span><span class="sxs-lookup"><span data-stu-id="790ae-160">The default value is 32.</span></span>

### <a name="nx_lwm2m_client_bootstrap_idle_timer"></a><span data-ttu-id="790ae-161">NX_LWM2M_CLIENT_BOOTSTRAP_IDLE_TIMER</span><span class="sxs-lookup"><span data-stu-id="790ae-161">NX_LWM2M_CLIENT_BOOTSTRAP_IDLE_TIMER</span></span>

<span data-ttu-id="790ae-162">Specifica il tempo massimo di attesa per le richieste del server di bootstrap quando viene avviata la sessione bootstrap prima di interrompere la sessione.</span><span class="sxs-lookup"><span data-stu-id="790ae-162">Specifies the maximum time to wait for bootstrap server requests when the bootstrap session is initiated before aborting the session.</span></span> <span data-ttu-id="790ae-163">Il valore predefinito è 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="790ae-163">The default value is 60 seconds.</span></span>

### <a name="nx_lwm2m_client_dtls_start_timeout"></a><span data-ttu-id="790ae-164">NX_LWM2M_CLIENT_DTLS_START_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="790ae-164">NX_LWM2M_CLIENT_DTLS_START_TIMEOUT</span></span>

<span data-ttu-id="790ae-165">Specifica il tempo massimo di attesa per il completamento dell'handshake DTLS.</span><span class="sxs-lookup"><span data-stu-id="790ae-165">Specifies the maximum time to wait for DTLS handshake completion.</span></span> <span data-ttu-id="790ae-166">Il valore predefinito è 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="790ae-166">The default value is 30 seconds.</span></span>

### <a name="nx_lwm2m_client_dtls_end_timeout"></a><span data-ttu-id="790ae-167">NX_LWM2M_CLIENT_DTLS_END_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="790ae-167">NX_LWM2M_CLIENT_DTLS_END_TIMEOUT</span></span>

<span data-ttu-id="790ae-168">Specifica il tempo massimo di attesa per il completamento dell'arresto del DTLS.</span><span class="sxs-lookup"><span data-stu-id="790ae-168">Specifies the maximum time to wait for DTLS shutdown completion.</span></span> <span data-ttu-id="790ae-169">Il valore predefinito è 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="790ae-169">The default value is 5 seconds.</span></span>
