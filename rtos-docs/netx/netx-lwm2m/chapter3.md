---
title: Capitolo 3-Descrizione funzionale di Azure RTO NetX LWM2M
description: Questo capitolo contiene una descrizione funzionale di Azure RTO NetX LWM2M.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f49a4f5f4c899dfa461a9d57a8b56e4503d6acd4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822583"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-lwm2m"></a><span data-ttu-id="fad74-103">Capitolo 3-Descrizione funzionale di Azure RTO NetX LWM2M</span><span class="sxs-lookup"><span data-stu-id="fad74-103">Chapter 3 - Functional description of Azure RTOS NetX LWM2M</span></span>

<span data-ttu-id="fad74-104">Questo capitolo contiene una descrizione funzionale di Azure RTO NetX LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-104">This chapter contains a functional description of Azure RTOS NetX LWM2M.</span></span>

## <a name="lwm2m-client-initialization"></a><span data-ttu-id="fad74-105">Inizializzazione del client LWM2M</span><span class="sxs-lookup"><span data-stu-id="fad74-105">LWM2M Client Initialization</span></span>

<span data-ttu-id="fad74-106">Il client LWM2M viene inizializzato chiamando ***nx_lwm2m_client_create*** servizio.</span><span class="sxs-lookup"><span data-stu-id="fad74-106">The LWM2M Client is initialized by calling ***nx_lwm2m_client_create*** service.</span></span> <span data-ttu-id="fad74-107">Il client LWM2M viene eseguito nel proprio thread e può segnalare alcuni eventi all'applicazione tramite l'uso di callback o chiamando metodi degli oggetti personalizzati implementati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fad74-107">The LWM2M Client runs in its own thread and can report some events to the application through the use of callbacks, or by calling methods of the custom objects implemented by the application.</span></span>

<span data-ttu-id="fad74-108">Inoltre, è necessario creare sessioni client di LWM2M chiamando ***nx_lwm2m_client_session_create*** per abilitare la comunicazione con uno o più server.</span><span class="sxs-lookup"><span data-stu-id="fad74-108">In addition, LWM2M Client Sessions must be created by calling ***nx_lwm2m_client_session_create*** for enabling communication with one or more servers.</span></span> <span data-ttu-id="fad74-109">Una sessione può comunicare con due tipi diversi di server: un server bootstrap o un server LWM2M (gestione dei dispositivi).</span><span class="sxs-lookup"><span data-stu-id="fad74-109">A session can communicate with two different types of servers: a Bootstrap Server or a LWM2M Server (Device Management).</span></span>

### <a name="bootstrap-server-session"></a><span data-ttu-id="fad74-110">Sessione del server bootstrap</span><span class="sxs-lookup"><span data-stu-id="fad74-110">Bootstrap Server Session</span></span>

<span data-ttu-id="fad74-111">Una sessione di comunicazione con un server bootstrap viene utilizzata per eseguire il provisioning di informazioni essenziali nel client di LWM2M per consentire al client di LWM2M di eseguire l'operazione "Register" con uno o più server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-111">A communication session with a Bootstrap Server is used to provision essential information into the LWM2M Client to enable the LWM2M Client to perform the operation "Register" with one or more LWM2M Servers.</span></span> <span data-ttu-id="fad74-112">Questo tipo di server viene utilizzato durante le modalità bootstrap avviate dal client e avviate dal server.</span><span class="sxs-lookup"><span data-stu-id="fad74-112">This type of server is used during the Client Initiated and Server Initiated Bootstrap modes.</span></span>

<span data-ttu-id="fad74-113">L'applicazione può avviare una sessione di bootstrap chiamando ***nx_lwm2m_client_session_bootstrap** _ o _*_nx_lwm2m_client_session_bootstrap_dtls_\*_, deve fornire l'indirizzo IP e il numero di porta del server e l'ID istanza di un oggetto di sicurezza facoltativo.</span><span class="sxs-lookup"><span data-stu-id="fad74-113">The application can start a Bootstrap session by calling ***nx_lwm2m_client_session_bootstrap** _ or _*_nx_lwm2m_client_session_bootstrap_dtls_\*_, it must provide the IP address and port number of the server, and an optional Security Object Instance ID.</span></span> <span data-ttu-id="fad74-114">La funzione _*_nx_lwm2m_client_session_bootstrap_*_ utilizza la comunicazione non protetta, mentre _ *_nx_lwm2m_client_session_bootstrap_dtls_*\* stabilisce una connessione DTLS protetta con il server.</span><span class="sxs-lookup"><span data-stu-id="fad74-114">The _*_nx_lwm2m_client_session_bootstrap_*_ function uses insecure communication, whereas _ *_nx_lwm2m_client_session_bootstrap_dtls_*\* establishes a secure DTLS connection with the server.</span></span>

<span data-ttu-id="fad74-115">Se l'operazione di bootstrap ha esito positivo, il server di bootstrap deve avere creato le istanze degli oggetti di sicurezza per i server bootstrap e LWM2M e le istanze dell'oggetto server per i server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-115">If the Bootstrap operation is successful, the Bootstrap server should have created Security Object Instance(s) for the Bootstrap and LWM2M Servers, and Server Object Instance(s) for the LWM2M Servers.</span></span> <span data-ttu-id="fad74-116">È necessario che l'applicazione utilizzi queste informazioni per stabilire una sessione con i server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-116">The application must use this information for establishing a session with the LWM2M Server(s).</span></span>

<span data-ttu-id="fad74-117">I dati bootstrap devono essere salvati nella memoria non volatile dall'applicazione per configurare il client di LWM2M al riavvio successivo del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fad74-117">The Bootstrap data should be saved to non-volatile memory by the application in order to configure the LWM2M Client at the next reboot of the device.</span></span>

### <a name="lwm2m-server-session"></a><span data-ttu-id="fad74-118">Sessione del server LWM2M</span><span class="sxs-lookup"><span data-stu-id="fad74-118">LWM2M Server Session</span></span>

<span data-ttu-id="fad74-119">Una sessione di comunicazione con un server LWM2M viene usata per la registrazione, la gestione dei dispositivi e l'abilitazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="fad74-119">A communication session with a LWM2M Server is used for Registration, Device Management and Service Enablement.</span></span>

<span data-ttu-id="fad74-120">L'applicazione può registrare il client LWM2M in un server chiamando ***nx_lwm2m_client_session_register** _ o _*_nx_lwm2m_client_session_register_dtls_\*_, deve fornire l'indirizzo IP e il numero di porta del server e l'ID del server breve che corrisponde a un'istanza dell'oggetto server esistente.</span><span class="sxs-lookup"><span data-stu-id="fad74-120">The application can register the LWM2M Client to a server by calling ***nx_lwm2m_client_session_register** _ or _*_nx_lwm2m_client_session_register_dtls_\*_, it must provide the IP address and port number of the server, and the Short Server ID which corresponds to an existing Server Object Instance.</span></span> <span data-ttu-id="fad74-121">La funzione _*_nx_lwm2m_client_session_register_*_ utilizza la comunicazione non protetta, mentre _ *_nx_lwm2m_client_session_register_dtls_*\* stabilisce una connessione DTLS protetta con il server.</span><span class="sxs-lookup"><span data-stu-id="fad74-121">The _*_nx_lwm2m_client_session_register_*_ function uses insecure communication, whereas _ *_nx_lwm2m_client_session_register_dtls_*\* establishes a secure DTLS connection with the server.</span></span>

<span data-ttu-id="fad74-122">L'applicazione può annullare la registrazione del client LWM2M chiamando \***nx_lwm2m_client_session_deregister** _ e chiedere al client di inviare un messaggio di aggiornamento chiamando _ *_nx_lwm2m_client_session_update_* \*.</span><span class="sxs-lookup"><span data-stu-id="fad74-122">The application can de-register the LWM2M Client by calling ***nx_lwm2m_client_session_deregister** _, and ask the client to send an 'Update' message by calling _*_nx_lwm2m_client_session_update_\*\*.</span></span>

### <a name="session-state-callback"></a><span data-ttu-id="fad74-123">Callback dello stato della sessione</span><span class="sxs-lookup"><span data-stu-id="fad74-123">Session State Callback</span></span>

<span data-ttu-id="fad74-124">L'applicazione registra un callback al momento della creazione di una sessione che viene chiamata quando viene aggiornato lo stato della sessione, la funzione di callback NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK dispone del prototipo seguente:</span><span class="sxs-lookup"><span data-stu-id="fad74-124">The application registers a callback at creation of a session which is called when the state of the session is updated, the callback function NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK has the following prototype:</span></span>

```c
typedef VOID (*NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK)
        (NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state);
```

<span data-ttu-id="fad74-125">Sono definiti gli Stati seguenti:</span><span class="sxs-lookup"><span data-stu-id="fad74-125">The following states are defined :</span></span>

- <span data-ttu-id="fad74-126">**NX_LWM2M_CLIENT_SESSION_INIT**: stato iniziale dopo la creazione della sessione.</span><span class="sxs-lookup"><span data-stu-id="fad74-126">**NX_LWM2M_CLIENT_SESSION_INIT**: The initial state after session creation.</span></span>

- <span data-ttu-id="fad74-127">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**: il client è in attesa della scadenza del timer ' Mantieni fuori ' o bootstrap avviato dal server.</span><span class="sxs-lookup"><span data-stu-id="fad74-127">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**: The client is waiting for the expiration of the 'Hold Off' timer or Server Initiated Bootstrap.</span></span>

- <span data-ttu-id="fad74-128">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**: il client ha inviato un messaggio "Request" al server bootstrap (bootstrap avviato dal client).</span><span class="sxs-lookup"><span data-stu-id="fad74-128">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**: The client has sent a 'Request' message to the Bootstrap Server (Client Initiated Bootstrap).</span></span>

- <span data-ttu-id="fad74-129">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**: il client riceve i dati dal server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="fad74-129">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**: The client is receiving data from the Bootstrap Server.</span></span>

- <span data-ttu-id="fad74-130">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**: il server bootstrap ha inviato un messaggio "finito".</span><span class="sxs-lookup"><span data-stu-id="fad74-130">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**: The Bootstrap Server has sent a 'Finished' message.</span></span>

- <span data-ttu-id="fad74-131">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**: la sessione bootstrap non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="fad74-131">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**: The bootstrap session has failed.</span></span>

- <span data-ttu-id="fad74-132">**NX_LWM2M_CLIENT_SESSION_REGISTERING**: il client ha inviato un messaggio di "registro" al server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-132">**NX_LWM2M_CLIENT_SESSION_REGISTERING**: The client has sent a 'Register' message to the LWM2M Server.</span></span>

- <span data-ttu-id="fad74-133">**NX_LWM2M_CLIENT_SESSION_REGISTERED**: il client viene registrato nel server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-133">**NX_LWM2M_CLIENT_SESSION_REGISTERED**: The client is registered to the LWM2M Server.</span></span>

- <span data-ttu-id="fad74-134">**NX_LWM2M_CLIENT_SESSION_UPDATING**: il client ha inviato un messaggio di aggiornamento al server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-134">**NX_LWM2M_CLIENT_SESSION_UPDATING**: The client has sent an 'Update' message to the LWM2M Server.</span></span>

- <span data-ttu-id="fad74-135">**NX_LWM2M_CLIENT_SESSION_DEREGISTERING**: il client ha inviato un messaggio "de-Register" al server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-135">**NX_LWM2M_CLIENT_SESSION_DEREGISTERING**: The client has sent an 'De-register' message to the LWM2M Server.</span></span>

- <span data-ttu-id="fad74-136">**NX_LWM2M_CLIENT_SESSION_DEREGISTERED**: il client viene deregistrato dal server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="fad74-136">**NX_LWM2M_CLIENT_SESSION_DEREGISTERED**: The client is de-registered from the LWM2M Server.</span></span>

- <span data-ttu-id="fad74-137">**NX_LWM2M_CLIENT_SESSION_DISABLED**: il server LWM2M è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="fad74-137">**NX_LWM2M_CLIENT_SESSION_DISABLED**: The LWM2M Server is disabled.</span></span> <span data-ttu-id="fad74-138">Un'Register ' verrà inviato dopo la scadenza del timer di disabilitazione.</span><span class="sxs-lookup"><span data-stu-id="fad74-138">A 'Register' will be sent after the expiration of the disable timer.</span></span>

- <span data-ttu-id="fad74-139">**NX_LWM2M_CLIENT_SESSION_ERROR**: l'operazione di registrazione o aggiornamento al server LWM2M non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="fad74-139">**NX_LWM2M_CLIENT_SESSION_ERROR**: The registration or update operation to the LWM2M Server has failed.</span></span>

- <span data-ttu-id="fad74-140">**NX_LWM2M_CLIENT_SESSION_DELETED**: l'istanza dell'oggetto server corrispondente al server LWM2M è stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="fad74-140">**NX_LWM2M_CLIENT_SESSION_DELETED**: The Server Object Instance corresponding to the LWM2M Server has been deleted.</span></span> <span data-ttu-id="fad74-141">In caso di errore, l'applicazione può recuperare la causa dell'errore chiamando **_nx_lwm2m_client_session_error_get_**.</span><span class="sxs-lookup"><span data-stu-id="fad74-141">In case of error the application can retrieve the cause of the error by calling **_nx_lwm2m_client_session_error_get_**.</span></span>

## <a name="local-device-management"></a><span data-ttu-id="fad74-142">Gestione dei dispositivi locali</span><span class="sxs-lookup"><span data-stu-id="fad74-142">Local Device Management</span></span>

<span data-ttu-id="fad74-143">L'applicazione può accedere agli oggetti del client LWM2M usando le funzioni di gestione dei dispositivi locali.</span><span class="sxs-lookup"><span data-stu-id="fad74-143">The application can access the Objects of the LWM2M Client by using the local device management functions.</span></span> <span data-ttu-id="fad74-144">Sono disponibili le funzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fad74-144">The following functions are provided:</span></span>

- <span data-ttu-id="fad74-145">***nx_lwm2m_client_object_read***: leggere le risorse da un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-145">***nx_lwm2m_client_object_read***: Read resources from an Object Instance.</span></span>

- <span data-ttu-id="fad74-146">***nx_lwm2m_client_object_discover***: Ottiene l'elenco delle risorse di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-146">***nx_lwm2m_client_object_discover***: Get the list of the resources of an Object Instance.</span></span>

- <span data-ttu-id="fad74-147">***nx_lwm2m_client_object_write***: scrivere le risorse in un'istanza dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="fad74-147">***nx_lwm2m_client_object_write***: Write resources to an Object Instance</span></span>

- <span data-ttu-id="fad74-148">***nx_lwm2m_client_object_execute***: eseguire l'operazione Execute su una risorsa di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-148">***nx_lwm2m_client_object_execute***: Perform the Execute operation on a resource of an Object Instance.</span></span>

- <span data-ttu-id="fad74-149">***nx_lwm2m_client_object_create***: creare una nuova istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-149">***nx_lwm2m_client_object_create***: Create a new Object Instance.</span></span>

- <span data-ttu-id="fad74-150">***nx_lwm2m_client_object_delete***: eliminare un'istanza dell'oggetto esistente.</span><span class="sxs-lookup"><span data-stu-id="fad74-150">***nx_lwm2m_client_object_delete***: Delete an existing Object Instance.</span></span>

- <span data-ttu-id="fad74-151">***nx_lwm2m_client_object_get_next***: ottenere l'ID oggetto successivo implementato dal client lwm2m.</span><span class="sxs-lookup"><span data-stu-id="fad74-151">***nx_lwm2m_client_object_get_next***: Get the next Object ID implemented by the LWM2M Client.</span></span>

- <span data-ttu-id="fad74-152">***nx_lwm2m_client_object_instance_get_next***: Ottiene l'istanza successiva di un oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-152">***nx_lwm2m_client_object_instance_get_next***: Get the next Instance of an Object.</span></span>

## <a name="resource-information"></a><span data-ttu-id="fad74-153">Informazioni sulle risorse</span><span class="sxs-lookup"><span data-stu-id="fad74-153">Resource Information</span></span>

<span data-ttu-id="fad74-154">Durante la lettura e la scrittura negli oggetti, una risorsa viene rappresentata dalla struttura NX_LWM2M_RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="fad74-154">When reading from and writing to Objects a Resource is represented by the NX_LWM2M_RESOURCE structure.</span></span> <span data-ttu-id="fad74-155">Questa struttura contiene l'ID della risorsa o dell'istanza e il relativo valore.</span><span class="sxs-lookup"><span data-stu-id="fad74-155">This structure contains the ID of the Resource/Instance and its value.</span></span> <span data-ttu-id="fad74-156">La codifica del valore dipende dal tipo e dalla relativa origine (applicazione o rete).</span><span class="sxs-lookup"><span data-stu-id="fad74-156">The encoding of the value depends on its type and its origin (application or network).</span></span>

<span data-ttu-id="fad74-157">La struttura NX_LWM2M_RESOURCE presenta la seguente definizione:</span><span class="sxs-lookup"><span data-stu-id="fad74-157">The NX_LWM2M_RESOURCE structure has the following definition:</span></span>

```c
typedef struct NX_LWM2M_RESOURCE_STRUCT
{
    NX_LWM2M_ID     nx_lwm2m_resource_id;
    UCHAR           nx_lwm2m_resource_type;
    union
    {
        struct
        {
            const VOID *     nx_lwm2m_resource_buffer_ptr;
            UINT             nx_lwm2m_resource_buffer_length;
        } nx_lwm2m_resource_bufferdata;
        const CHAR *         nx_lwm2m_resource_stringdata;
        NX_LWM2M_INT32       nx_lwm2m_resource_integer32data;
        NX_LWM2M_INT64       nx_lwm2m_resource_integer64data;
        NX_LWM2M_FLOAT32     nx_lwm2m_resource_float32data;
        NX_LWM2M_FLOAT64     nx_lwm2m_resource_float64data;
        NX_LWM2M_BOOL        nx_lwm2m_resource_booleandata;
        NX_LWM2M_OBJLNK      nx_lwm2m_resource_objlnkdata;
        
        struct
        {
            const VOID *     nx_lwm2m_resource_multiple_ptr;
            UINT             nx_lwm2m_resource_multiple_dim;
        } nx_lwm2m_resource_multipledata;
    } nx_lwm2m_resource_value;
} NX_LWM2M_RESOURCE;
```

- <span data-ttu-id="fad74-158">**nx_lwm2m_resource_id**: ID della risorsa o dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="fad74-158">**nx_lwm2m_resource_id**: The ID of the Resource or the Instance.</span></span>
- <span data-ttu-id="fad74-159">**nx_lwm2m_resource_type**: il tipo di valore, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="fad74-159">**nx_lwm2m_resource_type**: The type of the value, see below.</span></span>
- <span data-ttu-id="fad74-160">**nx_lwm2m_resource_value**: il valore della risorsa dipende dal tipo di valore.</span><span class="sxs-lookup"><span data-stu-id="fad74-160">**nx_lwm2m_resource_value**: The value of the Resource, depends on the type of the value.</span></span>

<span data-ttu-id="fad74-161">Sono definiti i seguenti tipi di valori:</span><span class="sxs-lookup"><span data-stu-id="fad74-161">The following type of values are defined :</span></span>

- <span data-ttu-id="fad74-162">**NX_LWM2M_RESOURCE_NONE**: risorsa vuota.</span><span class="sxs-lookup"><span data-stu-id="fad74-162">**NX_LWM2M_RESOURCE_NONE**: Empty resource.</span></span>

- <span data-ttu-id="fad74-163">**NX_LWM2M_RESOURCE_STRING**: valore stringa UTF-8 con terminazione null archiviato nel *nx_lwm2m_resource_stringdata*.</span><span class="sxs-lookup"><span data-stu-id="fad74-163">**NX_LWM2M_RESOURCE_STRING**: A null-terminated UTF-8 string value stored in *nx_lwm2m_resource_stringdata*.</span></span>

- <span data-ttu-id="fad74-164">**NX_LWM2M_RESOURCE_INTEGER32**: valore Integer a 32 bit archiviato nel *nx_lwm2m_resource_integer32data*.</span><span class="sxs-lookup"><span data-stu-id="fad74-164">**NX_LWM2M_RESOURCE_INTEGER32**: A 32-Bit Integer value stored in *nx_lwm2m_resource_integer32data*.</span></span>

- <span data-ttu-id="fad74-165">**NX_LWM2M_RESOURCE_INTEGER64**: valore Integer a 64 bit archiviato nel *nx_lwm2m_resource_integer64data*.</span><span class="sxs-lookup"><span data-stu-id="fad74-165">**NX_LWM2M_RESOURCE_INTEGER64**: A 64-Bit Integer value stored in *nx_lwm2m_resource_integer64data*.</span></span>

- <span data-ttu-id="fad74-166">**NX_LWM2M_RESOURCE_FLOAT32**: un valore a virgola mobile a 32 bit archiviato nel *nx_lwm2m_resource_float32data*.</span><span class="sxs-lookup"><span data-stu-id="fad74-166">**NX_LWM2M_RESOURCE_FLOAT32**: A 32-Bit Floating Point value stored in *nx_lwm2m_resource_float32data*.</span></span>

- <span data-ttu-id="fad74-167">**NX_LWM2M_RESOURCE_FLOAT64**: un valore a virgola mobile a 64 bit archiviato nel *nx_lwm2m_resource_float64data*.</span><span class="sxs-lookup"><span data-stu-id="fad74-167">**NX_LWM2M_RESOURCE_FLOAT64**: A 64-Bit Floating Point value stored in *nx_lwm2m_resource_float64data*.</span></span>

- <span data-ttu-id="fad74-168">**NX_LWM2M_RESOURCE_BOOLEAN**: valore booleano archiviato nel *nx_lwm2m_resource_booleandata*.</span><span class="sxs-lookup"><span data-stu-id="fad74-168">**NX_LWM2M_RESOURCE_BOOLEAN**: A Boolean value stored in *nx_lwm2m_resource_booleandata*.</span></span>

- <span data-ttu-id="fad74-169">**NX_LWM2M_RESOURCE_OPAQUE**: valore opaco definito da *nx_lwm2m_resource_bufferdata*.</span><span class="sxs-lookup"><span data-stu-id="fad74-169">**NX_LWM2M_RESOURCE_OPAQUE**: An Opaque value defined by *nx_lwm2m_resource_bufferdata*.</span></span>

- <span data-ttu-id="fad74-170">**NX_LWM2M_RESOURCE_OBJLNK**: valore del collegamento a un oggetto archiviato nel *nx_lwm2m_resource_objlnkdata*.</span><span class="sxs-lookup"><span data-stu-id="fad74-170">**NX_LWM2M_RESOURCE_OBJLNK**: An Object Link value stored in *nx_lwm2m_resource_objlnkdata*.</span></span>

- <span data-ttu-id="fad74-171">**NX_LWM2M_RESOURCE_TLV**: valore con codifica TLV definito da *nx_lwm2m_resource_bufferdata*.</span><span class="sxs-lookup"><span data-stu-id="fad74-171">**NX_LWM2M_RESOURCE_TLV**: A TLV encoded value defined by *nx_lwm2m_resource_bufferdata*.</span></span>

- <span data-ttu-id="fad74-172">**NX_LWM2M_RESOURCE_TEXT**: valore codificato Plain-Text definito da *nx_lwm2m_resource_bufferdata*.</span><span class="sxs-lookup"><span data-stu-id="fad74-172">**NX_LWM2M_RESOURCE_TEXT**: A Plain-Text encoded value defined by *nx_lwm2m_resource_bufferdata*.</span></span>

- <span data-ttu-id="fad74-173">**NX_LWM2M_RESOURCE_MULTIPLE**: una risorsa multipla definita da *nx_lwm2m_resource_multipledata*.</span><span class="sxs-lookup"><span data-stu-id="fad74-173">**NX_LWM2M_RESOURCE_MULTIPLE**: A Multiple Resource defined by *nx_lwm2m_resource_multipledata*.</span></span> <span data-ttu-id="fad74-174">*nx_lwm2m_resource_multiple_ptr* è un puntatore a una matrice di **NX_LWM2M_RESOURCE** strutture contenenti informazioni su ogni istanza di risorsa.</span><span class="sxs-lookup"><span data-stu-id="fad74-174">*nx_lwm2m_resource_multiple_ptr* is a pointer to an array of **NX_LWM2M_RESOURCE** structures containing information about each Resource Instances.</span></span>

- <span data-ttu-id="fad74-175">**NX_LWM2M_RESOURCE_MULTIPLE_TLV**: una risorsa multipla definita da *nx_lwm2m_resource_multipledata*.</span><span class="sxs-lookup"><span data-stu-id="fad74-175">**NX_LWM2M_RESOURCE_MULTIPLE_TLV**: A Multiple Resource defined by *nx_lwm2m_resource_multipledata*.</span></span> <span data-ttu-id="fad74-176">*nx_lwm2m_resource_multiple_ptr* è un puntatore a un buffer con codifica TLV.</span><span class="sxs-lookup"><span data-stu-id="fad74-176">*nx_lwm2m_resource_multiple_ptr* is a pointer to a TLV encoded buffer.</span></span>

<span data-ttu-id="fad74-177">Per recuperare il valore e controllarne il tipo, l'applicazione non deve mai accedere direttamente al campo *nx_lwm2m_resource_value* quando si recupera un valore da una struttura di NX_LWM2M_RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="fad74-177">Convenience functions are provided for retrieving the value and checking its type, the application should never directly access the *nx_lwm2m_resource_value* field when getting a value from a NX_LWM2M_RESOURCE structure.</span></span> <span data-ttu-id="fad74-178">Sono definite le funzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fad74-178">The following functions are defined :</span></span>

- <span data-ttu-id="fad74-179">***nx_lwm2m_resource_get_***: ottenere un valore con il tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="fad74-179">***nx_lwm2m_resource_get_***: Get a value with the given type.</span></span>
- <span data-ttu-id="fad74-180">***nx_lwm2m_resource_multiple_get_***: ottenere un valore con il tipo specificato da una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="fad74-180">***nx_lwm2m_resource_multiple_get_***: Get a value with the given type from a Multiple Resource.</span></span>

<span data-ttu-id="fad74-181">La macro **NX_LWM2M_RESOURCE_IS_MULTIPLE**(tipo) può essere usata per verificare se un tipo di risorsa è una risorsa multipla.</span><span class="sxs-lookup"><span data-stu-id="fad74-181">The macro **NX_LWM2M_RESOURCE_IS_MULTIPLE**(type) can be used to check if a resource type is a Multiple Resource.</span></span>

## <a name="object-implementation"></a><span data-ttu-id="fad74-182">Implementazione di oggetti</span><span class="sxs-lookup"><span data-stu-id="fad74-182">Object Implementation</span></span>

<span data-ttu-id="fad74-183">Il client LWM2M implementa gli oggetti LWM2M OMA obbligatori: Security (0), server (1), Access Control (2) e Device (3).</span><span class="sxs-lookup"><span data-stu-id="fad74-183">The LWM2M Client implements the mandatory OMA LWM2M Objects: Security (0), Server (1), Access Control (2) and Device (3).</span></span> <span data-ttu-id="fad74-184">Altri oggetti specifici del dispositivo devono essere implementati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fad74-184">Other device specific objects must be implemented by the application.</span></span>

<span data-ttu-id="fad74-185">Per definire un oggetto vengono usate due strutture di dati: la struttura NX_LWM2M_OBJECT definisce l'implementazione dell'oggetto, inclusi l'ID oggetto e i metodi dell'oggetto, e la struttura NX_LWM2M_OBJECT_INSTANCE contiene i dati di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-185">Two data structures are used to define an Object: the NX_LWM2M_OBJECT structure defines the Object implementation, including the Object ID and the object methods, and the NX_LWM2M_OBJECT_INSTANCE structure contains the data of an Object Instance.</span></span>

<span data-ttu-id="fad74-186">La struttura NX_LWM2M_OBJECT presenta la seguente definizione:</span><span class="sxs-lookup"><span data-stu-id="fad74-186">The NX_LWM2M_OBJECT structure has the following definition:</span></span>

```c
typedef struct NX_LWM2M_OBJECT_STRUCT
{
    NX_LWM2M_OBJECT * nx_lwm2m_object_next;
    NX_LWM2M_ID nx_lwm2m_object_id;
    UINT (*nx_lwm2m_object_read)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
        NX_LWM2M_RESOURCE *values);
    UINT (*nx_lwm2m_object_discover)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT *num_resources,
        NX_LWM2M_RESOURCE_INFO *resources);
    UINT (*nx_lwm2m_object_write)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values, const
        NX_LWM2M_RESOURCE *values, UINT write_op);
    UINT (*nx_lwm2m_object_execute)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
        const CHAR *args_ptr, UINT args_length);
    UINT (*nx_lwm2m_object_create)(NX_LWM2M_OBJECT * object_ptr,
        NX_LWM2M_ID instance_id, UINT num_values, const NX_LWM2M_RESOURCE
        *values, NX_LWM2M_OBJECT_INSTANCE **instance_ptr);
    UINT (*nx_lwm2m_object_delete)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr);
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instances;
} NX_LWM2M_OBJECT;
```

- <span data-ttu-id="fad74-187">**nx_lwm2m_object_next**: oggetto successivo nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="fad74-187">**nx_lwm2m_object_next**: The next object in the list.</span></span>
- <span data-ttu-id="fad74-188">**nx_lwm2m_object_id**: ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-188">**nx_lwm2m_object_id**: The Object ID.</span></span>
- <span data-ttu-id="fad74-189">**nx_lwm2m_object_read**: il metodo ' Read ', vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="fad74-189">**nx_lwm2m_object_read**: The 'Read' method, see below.</span></span>
- <span data-ttu-id="fad74-190">**nx_lwm2m_object_discover**: il metodo ' Discover ', vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="fad74-190">**nx_lwm2m_object_discover**: The 'Discover' method, see below.</span></span>
- <span data-ttu-id="fad74-191">**nx_lwm2m_object_write**: il metodo ' Write ', vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="fad74-191">**nx_lwm2m_object_write**: The 'Write' method, see below.</span></span>
- <span data-ttu-id="fad74-192">**nx_lwm2m_object_execute**: il metodo ' Execute ', vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="fad74-192">**nx_lwm2m_object_execute**: The 'Execute' method, see below.</span></span>
- <span data-ttu-id="fad74-193">**nx_lwm2m_object_create**: il metodo ' Create ', vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="fad74-193">**nx_lwm2m_object_create**: The 'Create' method, see below.</span></span>
- <span data-ttu-id="fad74-194">**nx_lwm2m_object_delete**: il metodo ' Delete ', vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="fad74-194">**nx_lwm2m_object_delete**: The 'Delete' method, see below.</span></span>
- <span data-ttu-id="fad74-195">**nx_lwm2m_object_instances**: elenco con terminazione null di istanze di oggetti.</span><span class="sxs-lookup"><span data-stu-id="fad74-195">**nx_lwm2m_object_instances**: The NULL-terminated list of object instances.</span></span>

<span data-ttu-id="fad74-196">La struttura NX_LWM2M_OBJECT_INSTANCE presenta la seguente definizione:</span><span class="sxs-lookup"><span data-stu-id="fad74-196">The NX_LWM2M_OBJECT_INSTANCE structure has the following definition:</span></span>

```c
typedef struct NX_LWM2M_OBJECT_INSTANCE_STRUCT
{
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instance_next;
    NX_LWM2M_ID nx_lwm2m_object_instance_id;
} NX_LWM2M_OBJECT_INSTANCE;
```

- <span data-ttu-id="fad74-197">**nx_lwm2m_object_instance_next**: istanza successiva nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="fad74-197">**nx_lwm2m_object_instance_next**: The next instance in the list.</span></span>
- <span data-ttu-id="fad74-198">**nx_lwm2m_object_instance_id**: ID dell'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-198">**nx_lwm2m_object_instance_id**: The Object Instance ID.</span></span>

<span data-ttu-id="fad74-199">L'oggetto deve implementare i metodi corrispondenti alle operazioni definite dall'interfaccia di gestione dei dispositivi LWM2M:' Read ',' Discovery ',' Write ',' Execute ',' Create ' ed ' Delete '.</span><span class="sxs-lookup"><span data-stu-id="fad74-199">The Object must implement the methods corresponding to the operations defined by the LWM2M Device Management Interface: 'Read', 'Discover', 'Write', 'Execute', 'Create' and 'Delete'.</span></span> <span data-ttu-id="fad74-200">I metodi ' Create ' è Delete ' possono essere impostati su NULL se l'oggetto non supporta la creazione dinamica di istanze.</span><span class="sxs-lookup"><span data-stu-id="fad74-200">The 'Create' and 'Delete' methods can be set to NULL if the object doesn't support dynamic creation of instances.</span></span>

### <a name="the-read-method"></a><span data-ttu-id="fad74-201">Metodo ' Read '</span><span class="sxs-lookup"><span data-stu-id="fad74-201">The 'Read' Method</span></span>

<span data-ttu-id="fad74-202">Il metodo ' Read ' viene usato per leggere i valori delle risorse da un'istanza dell'oggetto. la funzione presenta la definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="fad74-202">The 'Read' method is used to read Resource values from an Object Instance, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_read(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    NX_LWM2M_RESOURCE *values_ptr);
```

<span data-ttu-id="fad74-203">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="fad74-203">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="fad74-204">**object_ptr**: puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-204">**object_ptr**: Pointer to the Object implementation.</span></span>

- <span data-ttu-id="fad74-205">**instance_ptr**: puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-205">**instance_ptr**: Pointer to the Object Instance.</span></span>

- <span data-ttu-id="fad74-206">**num_values**: numero di risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="fad74-206">**num_values**: The number of resources to read.</span></span>

- <span data-ttu-id="fad74-207">**values_ptr**: puntatore a una matrice di NX_LWM2M_RESOURCE contenente gli ID delle risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="fad74-207">**values_ptr**: Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources to read.</span></span> <span data-ttu-id="fad74-208">In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="fad74-208">On return the array is filled with the corresponding types and values.</span></span>

### <a name="the-discover-method"></a><span data-ttu-id="fad74-209">Metodo ' Discover '</span><span class="sxs-lookup"><span data-stu-id="fad74-209">The 'Discover' Method</span></span>

<span data-ttu-id="fad74-210">Il metodo ' Discover ' viene usato per recuperare l'elenco di tutte le risorse implementate da un oggetto. la funzione presenta la definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="fad74-210">The 'Discover' method is used to retrieve the list of all Resources implemented by an Object, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_discover(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT *num_resources_ptr,
    NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

<span data-ttu-id="fad74-211">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="fad74-211">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="fad74-212">**object_ptr**: puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-212">**object_ptr**: Pointer to the Object implementation.</span></span>

- <span data-ttu-id="fad74-213">**instance_ptr**: puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-213">**instance_ptr**: Pointer to the Object Instance.</span></span>

- <span data-ttu-id="fad74-214">**num_resources_ptr**: in input la dimensione del buffer di destinazione, in output il numero di elementi scritti nel buffer.</span><span class="sxs-lookup"><span data-stu-id="fad74-214">**num_resources_ptr**: On input the size of the destination buffer, on output the number of elements writen to the buffer.</span></span>

- <span data-ttu-id="fad74-215">**resources_ptr**: puntatore al buffer di destinazione.</span><span class="sxs-lookup"><span data-stu-id="fad74-215">**resources_ptr**: Pointer to the destination buffer.</span></span>

<span data-ttu-id="fad74-216">Le informazioni sulle risorse vengono restituite in una struttura di NX_LWM2M_RESOURCE_INFO definita come segue:</span><span class="sxs-lookup"><span data-stu-id="fad74-216">The resource information is returned in a NX_LWM2M_RESOURCE_INFO structure defined as follows:</span></span>

```c
typedef struct NX_LWM2M_RESOURCE_INFO_STRUCT
{
    NX_LWM2M_ID     nx_lwm2m_resource_info_id;
    USHORT          nx_lwm2m_resource_info_flags;
    UINT            nx_lwm2m_resource_info_dim;
} NX_LWM2M_RESOURCE_INFO;
```

- <span data-ttu-id="fad74-217">**nx_lwm2m_resource_info_id**: ID della risorsa.</span><span class="sxs-lookup"><span data-stu-id="fad74-217">**nx_lwm2m_resource_info_id**: The ID of the Resource.</span></span>

- <span data-ttu-id="fad74-218">**nx_lwm2m_resource_info_flags**: vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="fad74-218">**nx_lwm2m_resource_info_flags**: See below.</span></span>

- <span data-ttu-id="fad74-219">**nx_lwm2m_resource_info_dim**: dimensione di più risorse se è impostato il flag NX_LWM2M_RESOURCE_INFO_MULTIPLE.</span><span class="sxs-lookup"><span data-stu-id="fad74-219">**nx_lwm2m_resource_info_dim**: The dimension of Multiple Resource if the flag NX_LWM2M_RESOURCE_INFO_MULTIPLE is set.</span></span>

<span data-ttu-id="fad74-220">Il campo *nx_lwm2m_resource_flags* può avere i seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="fad74-220">The field *nx_lwm2m_resource_flags* can have to the following values:</span></span>

- <span data-ttu-id="fad74-221">0: singola risorsa leggibile.</span><span class="sxs-lookup"><span data-stu-id="fad74-221">0: Single readable resource.</span></span>

- <span data-ttu-id="fad74-222">**NX_LWM2M_RESOURCE_INFO_MULTIPLE**: è necessario definire più risorse *nx_lwm2m_resource_info_dim* .</span><span class="sxs-lookup"><span data-stu-id="fad74-222">**NX_LWM2M_RESOURCE_INFO_MULTIPLE**: Multiple Resource, *nx_lwm2m_resource_info_dim* must be defined.</span></span>

- <span data-ttu-id="fad74-223">**NX_LWM2M_RESOURCE_INFO_EXECUTABLE**: risorsa eseguibile o non leggibile.</span><span class="sxs-lookup"><span data-stu-id="fad74-223">**NX_LWM2M_RESOURCE_INFO_EXECUTABLE**: Executable or Non-Readable Resource.</span></span>

### <a name="the-write-method"></a><span data-ttu-id="fad74-224">Metodo ' Write '</span><span class="sxs-lookup"><span data-stu-id="fad74-224">The 'Write' Method</span></span>

<span data-ttu-id="fad74-225">Il metodo ' Write ' viene usato per aggiornare o sostituire le risorse di un'istanza dell'oggetto. la funzione presenta la definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="fad74-225">The 'Write' method is used to update or replace resources of an Object Instance, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_write(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

<span data-ttu-id="fad74-226">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="fad74-226">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="fad74-227">**object_ptr**: puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-227">**object_ptr**: Pointer to the Object implementation.</span></span>
- <span data-ttu-id="fad74-228">**instance_ptr**: puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-228">**instance_ptr**: Pointer to the Object Instance.</span></span>
- <span data-ttu-id="fad74-229">**num_values**: numero di risorse da scrivere.</span><span class="sxs-lookup"><span data-stu-id="fad74-229">**num_values**: The number of resources to write.</span></span>
- <span data-ttu-id="fad74-230">**values_ptr**: puntatore ai valori delle risorse.</span><span class="sxs-lookup"><span data-stu-id="fad74-230">**values_ptr**: Pointer to the resources values.</span></span>
- <span data-ttu-id="fad74-231">**write_op**: tipo di operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="fad74-231">**write_op**: The type of write operations.</span></span>

<span data-ttu-id="fad74-232">È possibile specificare le operazioni di scrittura seguenti per il parametro *write_op* :</span><span class="sxs-lookup"><span data-stu-id="fad74-232">The following write operations can be specified to the *write_op* parameter :</span></span>

- <span data-ttu-id="fad74-233">0 &mdash; aggiornamento parziale: aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate le altre risorse esistenti,</span><span class="sxs-lookup"><span data-stu-id="fad74-233">0 &mdash; Partial Update: adds or updates Resources provided in the new value and leaves other existing Resources unchanged,</span></span>

- <span data-ttu-id="fad74-234">**NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Sostituisci istanza: sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa specificati.</span><span class="sxs-lookup"><span data-stu-id="fad74-234">**NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Replace Instance: replaces the Object Instance with the new provided resource values.</span></span>

- <span data-ttu-id="fad74-235">**NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Sostituisci risorsa: sostituisce le risorse con i nuovi valori di risorsa forniti, usati per sostituire più risorse.</span><span class="sxs-lookup"><span data-stu-id="fad74-235">**NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Replace Resource: replaces the Resources with the new provided resource values (used to replace Multiple Resources).</span></span>

- <span data-ttu-id="fad74-236">**NX_LWM2M_OBJECT_WRITE_CREATE** &mdash; Create instance: Inizializza l'istanza dell'oggetto appena creata con i valori di risorsa forniti, chiamati dal metodo *nx_lwm2m_object_create* .</span><span class="sxs-lookup"><span data-stu-id="fad74-236">**NX_LWM2M_OBJECT_WRITE_CREATE** &mdash; Create Instance: initializes the newly created Object Instance with the provided resource values (called from the *nx_lwm2m_object_create* method).</span></span>

- <span data-ttu-id="fad74-237">**NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Write: chiamato durante la sequenza di bootstrap.</span><span class="sxs-lookup"><span data-stu-id="fad74-237">**NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Write: called during Bootstrap sequence.</span></span>

### <a name="the-execute-method"></a><span data-ttu-id="fad74-238">Metodo ' Execute '</span><span class="sxs-lookup"><span data-stu-id="fad74-238">The 'Execute' Method</span></span>

<span data-ttu-id="fad74-239">Il metodo ' Execute ' implementa l'esecuzione di una risorsa dell'oggetto, la funzione presenta la definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="fad74-239">The 'Execute' method implements the execution of an Object Resource, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_execute(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr);
```

<span data-ttu-id="fad74-240">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="fad74-240">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="fad74-241">**object_ptr**: puntatore all'implementazione dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="fad74-241">**object_ptr**: Pointer to the Object implementation</span></span>
- <span data-ttu-id="fad74-242">**instance_ptr**: puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-242">**instance_ptr**: Pointer to the Object Instance.</span></span>
- <span data-ttu-id="fad74-243">**resource_id**: ID risorsa.</span><span class="sxs-lookup"><span data-stu-id="fad74-243">**resource_id**: The Resource ID.</span></span>
- <span data-ttu-id="fad74-244">**arguments_ptr**: puntatore agli argomenti dell'operazione di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fad74-244">**arguments_ptr**: Pointer to the arguments of the execute operation.</span></span> <span data-ttu-id="fad74-245">Può essere NULL se *arguments_length* è zero.</span><span class="sxs-lookup"><span data-stu-id="fad74-245">Can be NULL if *arguments_length* is zero.</span></span>
- <span data-ttu-id="fad74-246">**arguments_length**: lunghezza degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="fad74-246">**arguments_length**: The length of the arguments.</span></span>

<span data-ttu-id="fad74-247">La funzione deve restituire NX_LWM2M_NOT_FOUND se l'ID risorsa non esiste oppure NX_LWM2M_METHOD_NOT_ALLOWED se non supporta l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fad74-247">The function must return NX_LWM2M_NOT_FOUND if the Resource ID doesn't exist, or NX_LWM2M_METHOD_NOT_ALLOWED if it doesn't support execution.</span></span>

### <a name="the-create-method"></a><span data-ttu-id="fad74-248">Metodo ' Create '</span><span class="sxs-lookup"><span data-stu-id="fad74-248">The 'Create' Method</span></span>

<span data-ttu-id="fad74-249">Il metodo ' Create ' implementa la creazione di una nuova istanza dell'oggetto, la funzione presenta la definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="fad74-249">The 'Create' method implements the creation of a new Object Instance, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_create(NX_LWM2M_OBJECT * object_ptr,
    NX_LWM2M_ID instance_id, UINT num_values, const NX_LWM2M_RESOURCE *values_ptr,
    NX_LWM2M_OBJECT_INSTANCE **instance_ptr, NX_LWM2M_BOOL bootstrap);
```

<span data-ttu-id="fad74-250">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="fad74-250">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="fad74-251">**object_ptr**: puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-251">**object_ptr**: Pointer to the Object implementation.</span></span>
- <span data-ttu-id="fad74-252">**Instance_Id**: ID della nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="fad74-252">**instance_id**: The ID of the new Instance.</span></span>
- <span data-ttu-id="fad74-253">**num_values**: numero di risorse da inizializzare.</span><span class="sxs-lookup"><span data-stu-id="fad74-253">**num_values**: The number of resources to initialize.</span></span>
- <span data-ttu-id="fad74-254">**values_ptr**: puntatore ai valori delle risorse.</span><span class="sxs-lookup"><span data-stu-id="fad74-254">**values_ptr**: Pointer to the resources values.</span></span>
- <span data-ttu-id="fad74-255">**instance_ptr**: puntatore al puntatore di destinazione dell'istanza creata.</span><span class="sxs-lookup"><span data-stu-id="fad74-255">**instance_ptr**: Pointer to the destination pointer of the created instance.</span></span>
- <span data-ttu-id="fad74-256">**bootstrap**: true se chiamato dalla sequenza di bootstrap.</span><span class="sxs-lookup"><span data-stu-id="fad74-256">**bootstrap**: True if called from bootstrap sequence.</span></span>

<span data-ttu-id="fad74-257">L'oggetto deve allocare e initialiaze una nuova istanza dell'oggetto, usando l'elenco di valori di risorsa fornito.</span><span class="sxs-lookup"><span data-stu-id="fad74-257">The Object must allocate and initialiaze a new Object instance, using the provided list of resource values.</span></span>

### <a name="the-delete-method"></a><span data-ttu-id="fad74-258">Metodo ' Delete '</span><span class="sxs-lookup"><span data-stu-id="fad74-258">The 'Delete' Method</span></span>

<span data-ttu-id="fad74-259">Il metodo ' Delete ' implementa l'eliminazione di un'istanza dell'oggetto, la funzione presenta la definizione seguente:</span><span class="sxs-lookup"><span data-stu-id="fad74-259">The 'Delete' method implements the deletion of an object instance, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_delete(NX_LWM2M_OBJECT *object_ptr,
                NX_LWM2M_OBJECT_INSTANCE *instance_ptr);
```

<span data-ttu-id="fad74-260">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="fad74-260">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="fad74-261">**object_ptr**: puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-261">**object_ptr**: Pointer to the Object implementation.</span></span>
- <span data-ttu-id="fad74-262">**instance_ptr**: puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-262">**instance_ptr**: Pointer to the Object Instance.</span></span>

<span data-ttu-id="fad74-263">In caso di esito positivo, l'oggetto deve rilasciare i dati dell'istanza dell'oggetto e qualsiasi altra risorsa allocata dall'istanza.</span><span class="sxs-lookup"><span data-stu-id="fad74-263">On success the Object must release the Object Instance data and any other resource allocated by the instance.</span></span>

### <a name="adding-object-implementations-and-instances-to-the-lwm2m-client"></a><span data-ttu-id="fad74-264">Aggiunta di implementazioni e istanze di oggetti al client LWM2M</span><span class="sxs-lookup"><span data-stu-id="fad74-264">Adding Object Implementations and Instances to the LWM2M Client</span></span>

<span data-ttu-id="fad74-265">L'applicazione può aggiungere la nuova implementazione di un oggetto al client LWM2M chiamando il servizio ***nx_lwm2m_client_object_add*** .</span><span class="sxs-lookup"><span data-stu-id="fad74-265">The application can add new object implementation to the LWM2M Client by calling the ***nx_lwm2m_client_object_add*** service.</span></span>

<span data-ttu-id="fad74-266">Se l'oggetto non supporta la creazione dinamica di istanze, ad esempio se si tratta di un oggetto a istanza singola, il campo *nx_lwm2m_object_instances* della struttura dell'oggetto deve puntare all'elenco delle strutture delle istanze statiche.</span><span class="sxs-lookup"><span data-stu-id="fad74-266">If the Object doesn't support dynamic creation of Instances, for example if it's a single instance only Object, the *nx_lwm2m_object_instances* field of the object structure should point to the list of the static instances structures.</span></span>

<span data-ttu-id="fad74-267">Se l'oggetto supporta la creazione di istanze dinamiche, *nx_lwm2m_object_instances* deve essere impostato su null e deve essere utilizzato il servizio ***nx_lwm2m_client_object_create*** per chiamare il metodo ' Create ' dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="fad74-267">If the Object supports dynamic instance creation, *nx_lwm2m_object_instances* should be set to NULL and the ***nx_lwm2m_client_object_create*** service should be used instead in order to call the 'Create' method of the object.</span></span>

## <a name="example-of-lwm2m-client-application"></a><span data-ttu-id="fad74-268">Esempio di applicazione client LWM2M</span><span class="sxs-lookup"><span data-stu-id="fad74-268">Example of LWM2M Client Application</span></span>

<span data-ttu-id="fad74-269">Il codice seguente è un esempio di una semplice applicazione client LWM2M che implementa un dispositivo personalizzato costituito da un sensore di temperatura e da un Commuter leggero.</span><span class="sxs-lookup"><span data-stu-id="fad74-269">The following code is an example of a simple LWM2M Client Application which implements a custom device consisting of a temperature sensor and a light switch.</span></span>

<span data-ttu-id="fad74-270">Il dispositivo consente a un server di leggere il valore del sensore di temperatura e lo stato booleano del Commuter e di impostare lo switch di luce su on/off.</span><span class="sxs-lookup"><span data-stu-id="fad74-270">The device allows a server to read the value of the temperature sensor and the boolean state of the light switch, and to set the light switch to on/off.</span></span>

```c
#include "nx_lwm2m_client.h"

/* Custom Object implementation */
/* Define the Custom Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_OBJECT_INSTANCE     lwm2m;

    /* Resources Data */
    NX_LWM2M_FLOAT32             temperature;
    NX_LWM2M_BOOL                light;
} MYOBJECT_INSTANCE;

/* Define the Resources IDs */
#define MYOBJECT_RES_TEMPERATURE     0 /* temperature sensor */
#define MYOBJECT_RES_LIGHT           1 /* light switch */

/* Define the 'Read' Method */
UINT myobject_read(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr,
    UINT num_values, NX_LWM2M_RESOURCE *values)
{
    UINT i;
    for (i=0; i<num_values; i++)
    {
        switch (values[i].nx_lwm2m_resource_id)
        {
        case MYOBJECT_RES_TEMPERATURE:

            /* return the temperature value */
            values[i].nx_lwm2m_resource_type = NX_LWM2M_RESOURCE_FLOAT32;
            values[i].nx_lwm2m_resource_value.nx_lwm2m_resource_float32data =
                ((MYOBJECT_INSTANCE *) instance_ptr)->temperature;
            break;
        case MYOBJECT_RES_LIGHT:

            /* return the state of the light switch */
            values[i].nx_lwm2m_resource_type = NX_LWM2M_RESOURCE_BOOLEAN;
            values[i].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata =
                ((MYOBJECT_INSTANCE *) instance_ptr)->light;
            break;

        default:

            /* unknown resource ID */
            return NX_LWM2M_NOT_FOUND;
        }
    }
    return NX_SUCCESS;
}

/* Define the 'Discover' method */
UINT myobject_discover(NX_LWM2M_OBJECT *object_ptr, NX_LWM2M_OBJECT_INSTANCE *instance_ptr,
                                    UINT *num_resources, NX_LWM2M_RESOURCE_INFO *resources)
{
    if (*num_resources < 2)
    {
        return NX_LWM2M_BUFFER_TOO_SMALL;
    }

    /* return the list of supported resources IDs */
    *num_resources = 2;
    resources[0].nx_lwm2m_resource_info_id        = MYOBJECT_RES_TEMPERATURE;
    resources[0].nx_lwm2m_resource_info_flags     = 0;
    resources[1].nx_lwm2m_resource_info_id        = MYOBJECT_RES_LIGHT;
    resources[1].nx_lwm2m_resource_info_flags     = 0;
    return NX_SUCCESS;
}

/* Define the 'Write' method */
UINT myobject_write(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    const NX_LWM2M_RESOURCE *values, UINT flags)
{
    UINT i;
    for (i=0; i<num_values; i++)
    {
        UINT ret;
        switch (values[i].nx_lwm2m_resource_id)
        {

        case MYOBJECT_RES_TEMPERATURE:

            /* read-only resource */
            return NX_LWM2M_METHOD_NOT_ALLOWED;

        case MYOBJECT_RES_LIGHT:

            /* assign boolean value */

            ret = nx_lwm2m_resource_get_boolean(&values[i],
                &((MYOBJECT_INSTANCE *) instance_ptr)->light);

            if (ret != NX_SUCCESS)
            {

                /* invalid value type */
                return ret;
            }
            break;

        default:

            /* unknown resource ID */
            return NX_LWM2M_NOT_FOUND;
        }
    }
    return NX_SUCCESS;
}

/* Define the 'Execute' method */
UINT myobject_execute(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
    const CHAR *args_ptr, UINT args_length)
{
    switch (resource_id)
    {

    case MYOBJECT_RES_TEMPERATURE:
    case MYOBJECT_RES_LIGHT:

        /* read-only resource */
        return NX_LWM2M_METHOD_NOT_ALLOWED;

    default:

        /* unknown resource ID */
        return NX_LWM2M_NOT_FOUND;

    }
}

/* NetX data */
NX_IP                       ip;
NX_PACKET_POOL              packet_pool;

/* LWM2M Client data */
NX_LWM2M_CLIENT             client;
ULONG                       client_stack[4096 / sizeof(ULONG)];
NX_LWM2M_CLIENT_SESSION     session;

/* Custom Object Data */
NX_LWM2M_OBJECT             myobject;
MYOBJECT_INSTANCE           myinstance;

/* Define the session state callback */
void session_callback(NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state)
{
    switch (state)
    {

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:

        /* Bootstrap session done, we can register to the LWM2M Server */
        {
            NX_LWM2M_ID security_id;

            /* find the Security Object Instance of the LWM2M Server */
            security_id = NX_LWM2M_RESERVED_ID;
            while (nx_lwm2m_client_object_instance_get_next(&client,
                NX_LWM2M_SECURITY_OBJECT_ID, &security_id) == NX_SUCCESS)
            {
                NX_LWM2M_RESOURCE res[3];

                /* retrieve instance data: */
                /* Bootstrap server flag */
                res[0].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_BOOTSTRAP_ID;

                /* URI of server */
                res[1].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_URI_ID;

                /* Short Server ID */
                res[2].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_SHORT_SERVER_ID;

                /* Read Object Instance: */
                nx_lwm2m_client_object_read(&client,
                    NX_LWM2M_SECURITY_OBJECT_ID, security_id, 3, res);

                /* Not a bootstrap server? */
                if (!res[0].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata)
                {
                    ULONG ip_addr;
                    UINT udp_port;

                    /* get IP address and UDP port from server URI */
                    parse_uri(res[1].nx_lwm2m_resource_value.nx_lwm2m_resource_stringdata, &ip_addr, &udp_port);

                    /* Start registration to the LWM2M server */
                    nx_lwm2m_client_session_register(&session,
                        (NX_LWM2M_ID) res[2].nx_lwm2m_resource_value.
                        nx_lwm2m_resource_integer32data,
                        ip_addr, udp_port);
                    break;
                }
            }
        }
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:

        /* Failed to Bootstrap the LWM2M Client. */
        break;

    case NX_LWM2M_CLIENT_SESSION_REGISTERED:

        /* Registration to the LWM2M Client done. */
        break;

    case NX_LWM2M_CLIENT_SESSION_ERROR:

        /* Failed to register to the LWM2M Client. */
        break;
    }
}

/* Application main thread */
void application_thread(ULONG info)
{
    NX_LWM2M_RESOURCE res[4];
    NX_LWM2M_ID security_id;

    /* Create the LWM2M client */
    nx_lwm2m_client_create(&client, &ip, &packet_pool, NX_LWM2M_COAP_PORT,
        "mylwm2mclient", NULL, NX_LWM2M_BINDING_U,
        client_stack, sizeof(client_stack));

    /* Define our custom object */
    myobject.nx_lwm2m_object_id           = 1024;
    myobject.nx_lwm2m_object_read         = myobject_read;
    myobject.nx_lwm2m_object_discover     = myobject_discover;
    myobject.nx_lwm2m_object_write        = myobject_write;
    myobject.nx_lwm2m_object_execute      = myobject_execute;
    myobject.nx_lwm2m_object_create       = NULL;
    myobject.nx_lwm2m_object_delete       = NULL;

    /* Define a single instance */
    myobject.nx_lwm2m_object_instances             = (NX_LWM2M_OBJECT_INSTANCE *) &myinstance;
    myinstance.lwm2m.nx_lwm2m_object_instance_id   = 0;
    myinstance.lwm2m.nx_lwm2m_object_instance_next = NULL;
    myinstance.temperature                         = 22.5f;
    myinstance.light                               = NX_FALSE;

    /* Add the object to the LWM2M Client */
    nx_lwm2m_client_object_add(&client, &myobject);

    /* Create a security entry for the bootstrap server */
    security_id = 0;

    /* set the URI of the server */
    res[0].nx_lwm2m_resource_id                                 = NX_LWM2M_SECURITY_URI_ID;
    res[0].nx_lwm2m_resource_type                               = NX_LWM2M_RESOURCE_STRING;
    res[0].nx_lwm2m_resource_value.nx_lwm2m_resource_stringdata = "coap://1.2.3.4";

    /* set the Bootstrap flag */
    res[1].nx_lwm2m_resource_id                                  = NX_LWM2M_SECURITY_BOOTSTRAP_ID;
    res[1].nx_lwm2m_resource_type                                = NX_LWM2M_RESOURCE_BOOLEAN;
    res[1].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata = NX_TRUE;

    /* set the security mode */
    res[2].nx_lwm2m_resource_id                                    = NX_LWM2M_SECURITY_MODE_ID;
    res[2].nx_lwm2m_resource_type                                  = NX_LWM2M_RESOURCE_INTEGER32;
    res[2].nx_lwm2m_resource_value.nx_lwm2m_resource_integer32data =
    NX_LWM2M_SECURITY_MODE_NOSEC;

    /* set the Hold Off timer */
    res[3].nx_lwm2m_resource_id                                    = NX_LWM2M_SECURITY_HOLD_OFF_ID;
    res[3].nx_lwm2m_resource_type                                  = NX_LWM2M_RESOURCE_INTEGER32;
    res[3].nx_lwm2m_resource_value.nx_lwm2m_resource_integer32data = 10;
    nx_lwm2m_client_object_create(&client, NX_LWM2M_SECURITY_OBJECT_ID,
        &security_id, 4, res);

    /* Create a session */
    nx_lwm2m_client_session_create(&session, &client, session_callback);

    /* start bootstrap session */
    nx_lwm2m_client_session_bootstrap(&session, security_id,
                            IP_ADDRESS(1, 2, 3, 4), 5683);

    /* Application main loop */
    while (1)
    {
        /* ...application code... */
    }

    /* Terminate the LWM2M Client */
    nx_lwm2m_client_delete(&client);
}
```
