---
title: Capitolo 3-Descrizione funzionale del client LWM2M
description: Questo capitolo contiene una descrizione funzionale del client LWM2M.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 24b7ff66fb4d060075eb6bc81bed45b3479e18dc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821842"
---
# <a name="chapter-3--functional-description-of-lwm2m-client"></a><span data-ttu-id="9409b-103">Descrizione funzionale del capitolo 3 del client LWM2M</span><span class="sxs-lookup"><span data-stu-id="9409b-103">Chapter 3  Functional Description of LWM2M Client</span></span>

> <span data-ttu-id="9409b-104">Questo capitolo contiene una descrizione funzionale del client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-104">This chapter contains a functional description of LWM2M Client.</span></span>

## <a name="lwm2m-client-initialization"></a><span data-ttu-id="9409b-105">Inizializzazione del client LWM2M</span><span class="sxs-lookup"><span data-stu-id="9409b-105">LWM2M Client Initialization</span></span>

<span data-ttu-id="9409b-106">Il client LWM2M viene inizializzato chiamando ***nx_lwm2m_client_create*** servizio.</span><span class="sxs-lookup"><span data-stu-id="9409b-106">The LWM2M Client is initialized by calling ***nx_lwm2m_client_create*** service.</span></span> <span data-ttu-id="9409b-107">Il client LWM2M viene eseguito nel proprio thread e può segnalare alcuni eventi all'applicazione tramite l'uso di callback o chiamando metodi degli oggetti personalizzati implementati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9409b-107">The LWM2M Client runs in its own thread and can report some events to the application through the use of callbacks, or by calling methods of the custom objects implemented by the application.</span></span>

<span data-ttu-id="9409b-108">Inoltre, è necessario creare sessioni client di LWM2M chiamando ***nx_lwm2m_client_session_create*** per abilitare la comunicazione con uno o più server.</span><span class="sxs-lookup"><span data-stu-id="9409b-108">In addition, LWM2M Client Sessions must be created by calling ***nx_lwm2m_client_session_create*** for enabling communication with one or more servers.</span></span> <span data-ttu-id="9409b-109">Una sessione può comunicare con due tipi diversi di server: un server bootstrap o un server LWM2M (gestione dei dispositivi).</span><span class="sxs-lookup"><span data-stu-id="9409b-109">A session can communicate with two different types of servers: a Bootstrap Server or a LWM2M Server (Device Management).</span></span>

### <a name="bootstrap-server-session"></a><span data-ttu-id="9409b-110">Sessione del server bootstrap</span><span class="sxs-lookup"><span data-stu-id="9409b-110">Bootstrap Server Session</span></span>

<span data-ttu-id="9409b-111">Una sessione di comunicazione con un server bootstrap viene utilizzata per eseguire il provisioning di informazioni essenziali nel client di LWM2M per consentire al client di LWM2M di eseguire l'operazione "Register" con uno o più server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-111">A communication session with a Bootstrap Server is used to provision essential information into the LWM2M Client to enable the LWM2M Client to perform the operation “Register” with one or more LWM2M Servers.</span></span> <span data-ttu-id="9409b-112">Questo tipo di server viene utilizzato durante le modalità bootstrap avviate dal client e avviate dal server.</span><span class="sxs-lookup"><span data-stu-id="9409b-112">This type of server is used during the Client Initiated and Server Initiated Bootstrap modes.</span></span>

<span data-ttu-id="9409b-113">L'applicazione può avviare una sessione di bootstrap chiamando ***nx_lwm2m_client_session_bootstrap** _ o _*_nx_lwm2m_client_session_bootstrap_dtls_\*_, deve fornire l'indirizzo IP e il numero di porta del server e l'ID istanza di un oggetto di sicurezza facoltativo.</span><span class="sxs-lookup"><span data-stu-id="9409b-113">The application can start a Bootstrap session by calling ***nx_lwm2m_client_session_bootstrap** _ or _*_nx_lwm2m_client_session_bootstrap_dtls_\*_, it must provide the IP address and port number of the server, and an optional Security Object Instance ID.</span></span> <span data-ttu-id="9409b-114">La funzione _*_nx_lwm2m_client_session_bootstrap_*_ utilizza la comunicazione non protetta, mentre _ *_nx_lwm2m_client_session_bootstrap_dtls_*\* stabilisce una connessione DTLS protetta con il server.</span><span class="sxs-lookup"><span data-stu-id="9409b-114">The _*_nx_lwm2m_client_session_bootstrap_*_ function uses insecure communication, whereas _ *_nx_lwm2m_client_session_bootstrap_dtls_*\* establishes a secure DTLS connection with the server.</span></span>

<span data-ttu-id="9409b-115">Se l'operazione di bootstrap ha esito positivo, il server di bootstrap deve avere creato le istanze degli oggetti di sicurezza per i server bootstrap e LWM2M e le istanze dell'oggetto server per i server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-115">If the Bootstrap operation is successful, the Bootstrap server should have created Security Object Instance(s) for the Bootstrap and LWM2M Servers, and Server Object Instance(s) for the LWM2M Servers.</span></span> <span data-ttu-id="9409b-116">L'applicazione può chiamare ***nx_lwm2m_client_session_register_info_get*** per ottenere informazioni sui server lwm2m e usare queste informazioni per stabilire una sessione con i server lwm2m.</span><span class="sxs-lookup"><span data-stu-id="9409b-116">The application can call ***nx_lwm2m_client_session_register_info_get*** to get LWM2M Server(s) information and use this information for establishing a session with the LWM2M Server(s).</span></span>

<span data-ttu-id="9409b-117">I dati bootstrap devono essere salvati nella memoria non volatile dall'applicazione per configurare il client di LWM2M al riavvio successivo del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9409b-117">The Bootstrap data should be saved to non-volatile memory by the application to configure the LWM2M Client at the next reboot of the device.</span></span>

### <a name="lwm2m-server-session"></a><span data-ttu-id="9409b-118">Sessione del server LWM2M</span><span class="sxs-lookup"><span data-stu-id="9409b-118">LWM2M Server Session</span></span>

<span data-ttu-id="9409b-119">Una sessione di comunicazione con un server LWM2M viene usata per la registrazione, la gestione dei dispositivi e l'abilitazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="9409b-119">A communication session with a LWM2M Server is used for Registration, Device Management and Service Enablement.</span></span>

<span data-ttu-id="9409b-120">L'applicazione può registrare il client LWM2M in un server chiamando ***nx_lwm2m_client_session_register** _ o _*_nx_lwm2m_client_session_register_dtls_\*_, deve fornire l'indirizzo IP e il numero di porta del server e l'ID del server breve che corrisponde a un'istanza dell'oggetto server esistente.</span><span class="sxs-lookup"><span data-stu-id="9409b-120">The application can register the LWM2M Client to a server by calling ***nx_lwm2m_client_session_register** _ or _*_nx_lwm2m_client_session_register_dtls_\*_, it must provide the IP address and port number of the server, and the Short Server ID which corresponds to an existing Server Object Instance.</span></span> <span data-ttu-id="9409b-121">La funzione _*_nx_lwm2m_client_session_register_*_ utilizza la comunicazione non protetta, mentre _ *_nx_lwm2m_client_session_register_dtls_*\* stabilisce una connessione DTLS protetta con il server.</span><span class="sxs-lookup"><span data-stu-id="9409b-121">The _*_nx_lwm2m_client_session_register_*_ function uses insecure communication, whereas  _ *_nx_lwm2m_client_session_register_dtls_*\* establishes a secure DTLS connection with the server.</span></span>

<span data-ttu-id="9409b-122">L'applicazione può annullare la registrazione del client LWM2M chiamando \***nx_lwm2m_client_session_deregister** _ e chiedere al client di inviare un messaggio di aggiornamento chiamando _ *_nx_lwm2m_client_session_update_* \*.</span><span class="sxs-lookup"><span data-stu-id="9409b-122">The application can de-register the LWM2M Client by calling ***nx_lwm2m_client_session_deregister** _, and ask the client to send an ‘Update’ message by calling _*_nx_lwm2m_client_session_update_\*\*.</span></span>

### <a name="session-state-callback"></a><span data-ttu-id="9409b-123">Callback dello stato della sessione</span><span class="sxs-lookup"><span data-stu-id="9409b-123">Session State Callback</span></span>

<span data-ttu-id="9409b-124">L'applicazione registra un callback al momento della creazione di una sessione che viene chiamata quando viene aggiornato lo stato della sessione, la funzione di callback **NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK** dispone del prototipo seguente.</span><span class="sxs-lookup"><span data-stu-id="9409b-124">The application registers a callback at creation of a session which is called when the state of the session is updated, the callback function **NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK** has the following prototype.</span></span>

<span data-ttu-id="9409b-125">typedef VOID ( \* NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK) (NX_LWM2M_CLIENT_SESSION \* session_ptr, stato uint);</span><span class="sxs-lookup"><span data-stu-id="9409b-125">typedef VOID (\*NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK)(NX_LWM2M_CLIENT_SESSION \*session_ptr,UINT state);</span></span>

<span data-ttu-id="9409b-126">Sono definiti gli Stati seguenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-126">The following states are defined.</span></span>

| <span data-ttu-id="9409b-127">&nbsp;Stato sessione</span><span class="sxs-lookup"><span data-stu-id="9409b-127">Session&nbsp;State</span></span> | <span data-ttu-id="9409b-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-129">**NX_LWM2M_CLIENT_SESSION_INIT**</span><span class="sxs-lookup"><span data-stu-id="9409b-129">**NX_LWM2M_CLIENT_SESSION_INIT**</span></span> | <span data-ttu-id="9409b-130">Stato iniziale dopo la creazione della sessione.</span><span class="sxs-lookup"><span data-stu-id="9409b-130">The initial state after session creation.</span></span> |
| <span data-ttu-id="9409b-131">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**</span><span class="sxs-lookup"><span data-stu-id="9409b-131">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**</span></span> | <span data-ttu-id="9409b-132">Il client è in attesa della scadenza del timer ' Mantieni fuori ' o bootstrap avviato dal server.</span><span class="sxs-lookup"><span data-stu-id="9409b-132">The client is waiting for the expiration of the ‘Hold Off’ timer or Server Initiated Bootstrap.</span></span> |
| <span data-ttu-id="9409b-133">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**</span><span class="sxs-lookup"><span data-stu-id="9409b-133">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**</span></span> | <span data-ttu-id="9409b-134">Il client ha inviato un messaggio "Request" al server bootstrap (bootstrap avviato dal client).</span><span class="sxs-lookup"><span data-stu-id="9409b-134">The client has sent a ‘Request’ message to the Bootstrap Server (Client Initiated Bootstrap).</span></span> |
| <span data-ttu-id="9409b-135">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**</span><span class="sxs-lookup"><span data-stu-id="9409b-135">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**</span></span> | <span data-ttu-id="9409b-136">Il client riceve i dati dal server bootstrap.</span><span class="sxs-lookup"><span data-stu-id="9409b-136">The client is receiving data from the Bootstrap Server.</span></span> |
| <span data-ttu-id="9409b-137">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**</span><span class="sxs-lookup"><span data-stu-id="9409b-137">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**</span></span> | <span data-ttu-id="9409b-138">Il server bootstrap ha inviato un messaggio "finito".</span><span class="sxs-lookup"><span data-stu-id="9409b-138">The Bootstrap Server has sent a ‘Finished’ message.</span></span> |
| <span data-ttu-id="9409b-139">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**</span><span class="sxs-lookup"><span data-stu-id="9409b-139">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**</span></span> | <span data-ttu-id="9409b-140">La sessione bootstrap non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="9409b-140">The bootstrap session has failed.</span></span> |
| <span data-ttu-id="9409b-141">**NX_LWM2M_CLIENT_SESSION_REGISTERING**</span><span class="sxs-lookup"><span data-stu-id="9409b-141">**NX_LWM2M_CLIENT_SESSION_REGISTERING**</span></span> | <span data-ttu-id="9409b-142">Il client ha inviato un messaggio di "registro" al server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-142">The client has sent a ‘Register’ message to the LWM2M Server.</span></span> |
| <span data-ttu-id="9409b-143">**NX_LWM2M_CLIENT_SESSION_REGISTERED**</span><span class="sxs-lookup"><span data-stu-id="9409b-143">**NX_LWM2M_CLIENT_SESSION_REGISTERED**</span></span> | <span data-ttu-id="9409b-144">Il client viene registrato nel server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-144">The client is registered to the LWM2M Server.</span></span> |
| <span data-ttu-id="9409b-145">**NX_LWM2M_CLIENT_SESSION_UPDATING**</span><span class="sxs-lookup"><span data-stu-id="9409b-145">**NX_LWM2M_CLIENT_SESSION_UPDATING**</span></span> | <span data-ttu-id="9409b-146">Il client ha inviato un messaggio di aggiornamento al server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-146">The client has sent an ‘Update’ message to the LWM2M Server.</span></span> |
| <span data-ttu-id="9409b-147">**NX_LWM2M_CLIENT_SESSION_DEREGISTERING**</span><span class="sxs-lookup"><span data-stu-id="9409b-147">**NX_LWM2M_CLIENT_SESSION_DEREGISTERING**</span></span> | <span data-ttu-id="9409b-148">Il client ha inviato un messaggio "de-Register" al server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-148">The client has sent an ‘De-register’ message to the LWM2M Server.</span></span> |
| <span data-ttu-id="9409b-149">**NX_LWM2M_CLIENT_SESSION_DEREGISTERED**</span><span class="sxs-lookup"><span data-stu-id="9409b-149">**NX_LWM2M_CLIENT_SESSION_DEREGISTERED**</span></span> | <span data-ttu-id="9409b-150">Il client viene deregistrato dal server LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-150">The client is de-registered from the LWM2M Server.</span></span> |
| <span data-ttu-id="9409b-151">**NX_LWM2M_CLIENT_SESSION_DISABLED**</span><span class="sxs-lookup"><span data-stu-id="9409b-151">**NX_LWM2M_CLIENT_SESSION_DISABLED**</span></span> | <span data-ttu-id="9409b-152">Il server LWM2M è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="9409b-152">The LWM2M Server is disabled.</span></span> <span data-ttu-id="9409b-153">Un'Register ' verrà inviato dopo la scadenza del timer di disabilitazione.</span><span class="sxs-lookup"><span data-stu-id="9409b-153">A ‘Register’ will be sent after the expiration of the disable timer.</span></span> |
| <span data-ttu-id="9409b-154">**NX_LWM2M_CLIENT_SESSION_ERROR**</span><span class="sxs-lookup"><span data-stu-id="9409b-154">**NX_LWM2M_CLIENT_SESSION_ERROR**</span></span> | <span data-ttu-id="9409b-155">L'operazione di registrazione o aggiornamento al server LWM2M non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="9409b-155">The registration or update operation to the LWM2M Server has failed.</span></span> |
| <span data-ttu-id="9409b-156">**NX_LWM2M_CLIENT_SESSION_DELETED**</span><span class="sxs-lookup"><span data-stu-id="9409b-156">**NX_LWM2M_CLIENT_SESSION_DELETED**</span></span> | <span data-ttu-id="9409b-157">L'istanza dell'oggetto server corrispondente al server LWM2M è stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="9409b-157">The Server Object Instance corresponding to the LWM2M Server has been deleted.</span></span> |

<span data-ttu-id="9409b-158">In caso di errore, l'applicazione può recuperare la causa dell'errore chiamando ***nx_lwm2m_client_session_error_get***.</span><span class="sxs-lookup"><span data-stu-id="9409b-158">In case of error the application can retrieve the cause of the error by calling ***nx_lwm2m_client_session_error_get***.</span></span>

## <a name="local-device-management"></a><span data-ttu-id="9409b-159">Gestione dei dispositivi locali</span><span class="sxs-lookup"><span data-stu-id="9409b-159">Local Device Management</span></span>

<span data-ttu-id="9409b-160">L'applicazione può accedere agli oggetti del client LWM2M usando le funzioni di gestione dei dispositivi locali.</span><span class="sxs-lookup"><span data-stu-id="9409b-160">The application can access the Objects of the LWM2M Client by using the local device management functions.</span></span> <span data-ttu-id="9409b-161">Sono disponibili le funzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-161">The following functions are provided.</span></span>

| <span data-ttu-id="9409b-162">&nbsp;Nome funzione</span><span class="sxs-lookup"><span data-stu-id="9409b-162">Function&nbsp;Name</span></span> | <span data-ttu-id="9409b-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-163">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-164">***nx_lwm2m_client_object_read***</span><span class="sxs-lookup"><span data-stu-id="9409b-164">***nx_lwm2m_client_object_read***</span></span> | <span data-ttu-id="9409b-165">Leggere le risorse da un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-165">Read resources from an Object Instance.</span></span> |
| <span data-ttu-id="9409b-166">***nx_lwm2m_client_object_discover***</span><span class="sxs-lookup"><span data-stu-id="9409b-166">***nx_lwm2m_client_object_discover***</span></span> | <span data-ttu-id="9409b-167">Ottiene l'elenco delle risorse di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-167">Get the list of the resources of an Object Instance.</span></span>
| <span data-ttu-id="9409b-168">***nx_lwm2m_client_object_write***</span><span class="sxs-lookup"><span data-stu-id="9409b-168">***nx_lwm2m_client_object_write***</span></span> | <span data-ttu-id="9409b-169">Scrivere le risorse in un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-169">Write resources to an Object Instance.</span></span> |
| <span data-ttu-id="9409b-170">***nx_lwm2m_client_object_execute***</span><span class="sxs-lookup"><span data-stu-id="9409b-170">***nx_lwm2m_client_object_execute***</span></span> | <span data-ttu-id="9409b-171">Eseguire l'operazione Execute su una risorsa di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-171">Perform the Execute operation on a resource of an Object Instance.</span></span> |
| <span data-ttu-id="9409b-172">***nx_lwm2m_client_object_create***</span><span class="sxs-lookup"><span data-stu-id="9409b-172">***nx_lwm2m_client_object_create***</span></span> | <span data-ttu-id="9409b-173">Creare una nuova istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-173">Create a new Object Instance.</span></span> |
| <span data-ttu-id="9409b-174">***nx_lwm2m_client_object_delete***</span><span class="sxs-lookup"><span data-stu-id="9409b-174">***nx_lwm2m_client_object_delete***</span></span> | <span data-ttu-id="9409b-175">Eliminare un'istanza dell'oggetto esistente.</span><span class="sxs-lookup"><span data-stu-id="9409b-175">Delete an existing Object Instance.</span></span> |
| <span data-ttu-id="9409b-176">***nx_lwm2m_client_object_next_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-176">***nx_lwm2m_client_object_next_get***</span></span> | <span data-ttu-id="9409b-177">Ottenere l'ID oggetto successivo dal client LWM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-177">Get the next Object ID by the LWM2M Client.</span></span> |
| <span data-ttu-id="9409b-178">***nx_lwm2m_client_object_instance_next_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-178">***nx_lwm2m_client_object_instance_next_get***</span></span> | <span data-ttu-id="9409b-179">Ottiene l'istanza successiva di un oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-179">Get the next Instance of an Object.</span></span> |

## <a name="resource-information"></a><span data-ttu-id="9409b-180">Informazioni sulle risorse</span><span class="sxs-lookup"><span data-stu-id="9409b-180">Resource Information</span></span>

<span data-ttu-id="9409b-181">Durante la lettura e la scrittura negli oggetti, una risorsa viene rappresentata dalla struttura NX_LWM2M_CLIENT_RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="9409b-181">When reading from and writing to Objects a Resource is represented by the NX_LWM2M_CLIENT_RESOURCE structure.</span></span> <span data-ttu-id="9409b-182">Questa struttura contiene l'ID della risorsa o dell'istanza e il relativo valore.</span><span class="sxs-lookup"><span data-stu-id="9409b-182">This structure contains the ID of the Resource/Instance and its value.</span></span>

<span data-ttu-id="9409b-183">Le funzioni seguenti vengono fornite per impostare le informazioni e il valore della risorsa.</span><span class="sxs-lookup"><span data-stu-id="9409b-183">The following functions are provided for setting resource info and value.</span></span>

| <span data-ttu-id="9409b-184">&nbsp;Nome funzione</span><span class="sxs-lookup"><span data-stu-id="9409b-184">Function&nbsp;Name</span></span> | <span data-ttu-id="9409b-185">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-185">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-186">***nx_lwm2m_client_resource_info_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-186">***nx_lwm2m_client_resource_info_set***</span></span> | <span data-ttu-id="9409b-187">Impostare informazioni sulle risorse: ID risorsa e operazione: lettura, scrittura, ESEGUIbile.</span><span class="sxs-lookup"><span data-stu-id="9409b-187">Set resource info: resource id and operation: READ, WRITE, EXECUTABLE.</span></span> |
| <span data-ttu-id="9409b-188">***nx_lwm2m_client_resource_string_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-188">***nx_lwm2m_client_resource_string_set***</span></span> | <span data-ttu-id="9409b-189">Impostare il valore della risorsa come stringa.</span><span class="sxs-lookup"><span data-stu-id="9409b-189">Set the resource value as string.</span></span> |
| <span data-ttu-id="9409b-190">***nx_lwm2m_client_resource_integer32_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-190">***nx_lwm2m_client_resource_integer32_set***</span></span> | <span data-ttu-id="9409b-191">Impostare il valore della risorsa come intero a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="9409b-191">Set the resource value as 32-Bit integer.</span></span> |
| <span data-ttu-id="9409b-192">***nx_lwm2m_client_resource_integer64_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-192">***nx_lwm2m_client_resource_integer64_set***</span></span> | <span data-ttu-id="9409b-193">Impostare il valore della risorsa come intero a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="9409b-193">Set the resource value as 64-Bit integer.</span></span> |
| <span data-ttu-id="9409b-194">***nx_lwm2m_client_resource_float32_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-194">***nx_lwm2m_client_resource_float32_set***</span></span> | <span data-ttu-id="9409b-195">Impostare il valore della risorsa come float a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="9409b-195">Set the resource value as 32-Bit float.</span></span> |
| <span data-ttu-id="9409b-196">***nx_lwm2m_client_resource_float64_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-196">***nx_lwm2m_client_resource_float64_set***</span></span> | <span data-ttu-id="9409b-197">Impostare il valore della risorsa come float a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="9409b-197">Set the resource value as 64-Bit float.</span></span> |
| <span data-ttu-id="9409b-198">***nx_lwm2m_client_resource_boolean_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-198">***nx_lwm2m_client_resource_boolean_set***</span></span> | <span data-ttu-id="9409b-199">Impostare il valore della risorsa come valore booleano.</span><span class="sxs-lookup"><span data-stu-id="9409b-199">Set the resource value as boolean.</span></span> |
| <span data-ttu-id="9409b-200">***nx_lwm2m_client_resource_objlnk_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-200">***nx_lwm2m_client_resource_objlnk_set***</span></span> | <span data-ttu-id="9409b-201">Impostare il valore della risorsa come collegamento all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-201">Set the resource value as object link.</span></span> |
| <span data-ttu-id="9409b-202">***nx_lwm2m_client_resource_opaque_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-202">***nx_lwm2m_client_resource_opaque_set***</span></span> | <span data-ttu-id="9409b-203">Impostare il valore della risorsa come opaco.</span><span class="sxs-lookup"><span data-stu-id="9409b-203">Set the resource value as opaque.</span></span> |
| <span data-ttu-id="9409b-204">***nx_lwm2m_client_resource_instance_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-204">***nx_lwm2m_client_resource_instance_set***</span></span> | <span data-ttu-id="9409b-205">Impostare il valore della risorsa come istanza di per più risorse.</span><span class="sxs-lookup"><span data-stu-id="9409b-205">Set the resource value as instance for multiple resource.</span></span> |
| <span data-ttu-id="9409b-206">***nx_lwm2m_client_resource_dim_set***</span><span class="sxs-lookup"><span data-stu-id="9409b-206">***nx_lwm2m_client_resource_dim_set***</span></span> | <span data-ttu-id="9409b-207">Impostare la dimensione della risorsa per più risorse per l'individuazione.</span><span class="sxs-lookup"><span data-stu-id="9409b-207">Set the resource dimension for multiple resource for discover.</span></span> |

<span data-ttu-id="9409b-208">Le funzioni seguenti vengono fornite per ottenere informazioni sulle risorse e valore.</span><span class="sxs-lookup"><span data-stu-id="9409b-208">The following functions are provided for getting resource info and value.</span></span>

| <span data-ttu-id="9409b-209">&nbsp;Nome funzione</span><span class="sxs-lookup"><span data-stu-id="9409b-209">Function&nbsp;Name</span></span> | <span data-ttu-id="9409b-210">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-210">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-211">***nx_lwm2m_client_resource_info_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-211">***nx_lwm2m_client_resource_info_get***</span></span> | <span data-ttu-id="9409b-212">Ottenere informazioni sulle risorse: ID risorsa e operazione: lettura, scrittura, ESEGUIbile.</span><span class="sxs-lookup"><span data-stu-id="9409b-212">Get resource info: resource id and operation: READ, WRITE, EXECUTABLE.</span></span> |
| <span data-ttu-id="9409b-213">***nx_lwm2m_client_resource_string_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-213">***nx_lwm2m_client_resource_string_get***</span></span> | <span data-ttu-id="9409b-214">Ottenere il valore di una risorsa di stringa.</span><span class="sxs-lookup"><span data-stu-id="9409b-214">Get the value of a string resource.</span></span> |
| <span data-ttu-id="9409b-215">***nx_lwm2m_client_resource_integer32_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-215">***nx_lwm2m_client_resource_integer32_get***</span></span> | <span data-ttu-id="9409b-216">Ottenere il valore di una risorsa Integer a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="9409b-216">Get the value of a 32-Bit integer resource.</span></span> |
| <span data-ttu-id="9409b-217">***nx_lwm2m_client_resource_integer64_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-217">***nx_lwm2m_client_resource_integer64_get***</span></span> | <span data-ttu-id="9409b-218">Ottenere il valore di una risorsa Integer a bit B4.</span><span class="sxs-lookup"><span data-stu-id="9409b-218">Get the value of a b4-Bit integer resource.</span></span> |
| <span data-ttu-id="9409b-219">***nx_lwm2m_client_resource_float32_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-219">***nx_lwm2m_client_resource_float32_get***</span></span> | <span data-ttu-id="9409b-220">Ottenere il valore di una risorsa float a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="9409b-220">Get the value of a 32-Bit float resource.</span></span> |
| <span data-ttu-id="9409b-221">***nx_lwm2m_client_resource_float64_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-221">***nx_lwm2m_client_resource_float64_get***</span></span> | <span data-ttu-id="9409b-222">Ottenere il valore di una risorsa float a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="9409b-222">Get the value of a 64-Bit float resource.</span></span> |
| <span data-ttu-id="9409b-223">***nx_lwm2m_client_resource_boolean_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-223">***nx_lwm2m_client_resource_boolean_get***</span></span> | <span data-ttu-id="9409b-224">Ottenere il valore di una risorsa booleana.</span><span class="sxs-lookup"><span data-stu-id="9409b-224">Get the value of a Boolean resource.</span></span> |
| <span data-ttu-id="9409b-225">***nx_lwm2m_client_resource_objlnk_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-225">***nx_lwm2m_client_resource_objlnk_get***</span></span> | <span data-ttu-id="9409b-226">Ottenere il valore di una risorsa di collegamento a un oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-226">Get the value of an object link resource.</span></span> |
| <span data-ttu-id="9409b-227">***nx_lwm2m_client_resource_opaque_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-227">***nx_lwm2m_client_resource_opaque_get***</span></span> | <span data-ttu-id="9409b-228">Ottenere il valore di una risorsa opaca.</span><span class="sxs-lookup"><span data-stu-id="9409b-228">Get the value of an opaque resource.</span></span> |
| <span data-ttu-id="9409b-229">***nx_lwm2m_client_resource_instance_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-229">***nx_lwm2m_client_resource_instance_get***</span></span> | <span data-ttu-id="9409b-230">Ottenere l'istanza della risorsa per più risorse.</span><span class="sxs-lookup"><span data-stu-id="9409b-230">Get the resource instance for multiple resource.</span></span> |
| <span data-ttu-id="9409b-231">***nx_lwm2m_client_resource_dim_get***</span><span class="sxs-lookup"><span data-stu-id="9409b-231">***nx_lwm2m_client_resource_dim_get***</span></span> | <span data-ttu-id="9409b-232">Ottenere la dimensione di risorsa per più risorse.</span><span class="sxs-lookup"><span data-stu-id="9409b-232">Get the resource dimension for multiple resource.</span></span> |

## <a name="object-implementation"></a><span data-ttu-id="9409b-233">Implementazione di oggetti</span><span class="sxs-lookup"><span data-stu-id="9409b-233">Object Implementation</span></span>

<span data-ttu-id="9409b-234">Il client LWM2M implementa gli oggetti LWM2M OMA obbligatori: Security (0), server (1), Access Control (2) e Device (3).</span><span class="sxs-lookup"><span data-stu-id="9409b-234">The LWM2M Client implements the mandatory OMA LWM2M Objects: Security (0), Server (1), Access Control (2) and Device (3).</span></span> <span data-ttu-id="9409b-235">Altri oggetti specifici del dispositivo devono essere implementati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9409b-235">Other device specific objects must be implemented by the application.</span></span>

<span data-ttu-id="9409b-236">Per definire un oggetto vengono usate due strutture di dati: la struttura NX_LWM2M_CLIENT_OBJECT definisce l'implementazione dell'oggetto, inclusi l'ID oggetto e i metodi dell'oggetto, e la struttura NX_LWM2M_CLIENT_OBJECT_INSTANCE contiene i dati di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-236">Two data structures are used to define an Object: the NX_LWM2M_CLIENT_OBJECT structure defines the Object implementation, including the Object ID and the object methods, and the NX_LWM2M_CLIENT_OBJECT_INSTANCE structure contains the data of an Object Instance.</span></span>

<span data-ttu-id="9409b-237">Sono disponibili le funzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-237">The following functions are provided.</span></span>

| <span data-ttu-id="9409b-238">&nbsp;Nome funzione</span><span class="sxs-lookup"><span data-stu-id="9409b-238">Function&nbsp;Name</span></span> | <span data-ttu-id="9409b-239">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-240">***nx_lwm2m_client_object_add***</span><span class="sxs-lookup"><span data-stu-id="9409b-240">***nx_lwm2m_client_object_add***</span></span> | <span data-ttu-id="9409b-241">Aggiungere l'implementazione dell'oggetto al client LwM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-241">Add object implementation to the LwM2M Client.</span></span> |
| <span data-ttu-id="9409b-242">***nx_lwm2m_client_object_remove***</span><span class="sxs-lookup"><span data-stu-id="9409b-242">***nx_lwm2m_client_object_remove***</span></span> | <span data-ttu-id="9409b-243">Rimuovere l'implementazione dell'oggetto dal client LwM2M.</span><span class="sxs-lookup"><span data-stu-id="9409b-243">Remove object implementation from the LwM2M Client.</span></span> |
| <span data-ttu-id="9409b-244">***nx_lwm2m_client_object_instance_add***</span><span class="sxs-lookup"><span data-stu-id="9409b-244">***nx_lwm2m_client_object_instance_add***</span></span> | <span data-ttu-id="9409b-245">Aggiungere l'istanza dell'oggetto all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-245">Add object instance to the Object.</span></span> |
| <span data-ttu-id="9409b-246">***nx_lwm2m_client_object_instance_remove***</span><span class="sxs-lookup"><span data-stu-id="9409b-246">***nx_lwm2m_client_object_instance_remove***</span></span> | <span data-ttu-id="9409b-247">Rimuovere l'istanza dell'oggetto dall'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-247">Remove object instance from the Object.</span></span> |

<span data-ttu-id="9409b-248">La funzione di callback del metodo Object presenta la firma riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="9409b-248">The object method callback function has signature shown below.</span></span>

```c
typedef UINT (*NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK)(
    UINT operation, 
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr,
    NX_LWM2M_CLIENT_RESOURCE *resource,
    UINT *resource_count,
    VOID *args_ptr,
    UINT args_length);
```

### <a name="the-read-method"></a><span data-ttu-id="9409b-249">Metodo ' Read '</span><span class="sxs-lookup"><span data-stu-id="9409b-249">The ‘Read’ Method</span></span>

<span data-ttu-id="9409b-250">Il metodo ' Read ' viene usato per leggere i valori delle risorse da un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-250">The ‘Read’ method is used to read Resource values from an Object Instance.</span></span> <span data-ttu-id="9409b-251">I parametri sono definiti nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="9409b-251">The parameters are defined as follows.</span></span>

| <span data-ttu-id="9409b-252">Parametro</span><span class="sxs-lookup"><span data-stu-id="9409b-252">Parameter</span></span> | <span data-ttu-id="9409b-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-253">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-254">**operation**</span><span class="sxs-lookup"><span data-stu-id="9409b-254">**operation**</span></span> | <span data-ttu-id="9409b-255">**NX_LWM2M_CLIENT_OBJECT_READ**</span><span class="sxs-lookup"><span data-stu-id="9409b-255">**NX_LWM2M_CLIENT_OBJECT_READ**</span></span> |
| <span data-ttu-id="9409b-256">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-256">**object_ptr**</span></span> | <span data-ttu-id="9409b-257">Puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-257">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="9409b-258">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-258">**instance_ptr**</span></span> | <span data-ttu-id="9409b-259">Puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-259">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="9409b-260">**risorse**</span><span class="sxs-lookup"><span data-stu-id="9409b-260">**resource**</span></span> | <span data-ttu-id="9409b-261">Puntatore a una matrice di **NX_LWM2M_CLIENT_RESOURCE** contenente gli ID delle risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="9409b-261">Pointer to an array of **NX_LWM2M_CLIENT_RESOURCE** containing the IDs of the resources to read.</span></span> <span data-ttu-id="9409b-262">In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-262">On return the array is filled with corresponding types and values.</span></span> |
| <span data-ttu-id="9409b-263">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="9409b-263">**resource_count**</span></span> | <span data-ttu-id="9409b-264">Puntatore al numero di risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="9409b-264">Pointer to the number of resources to read.</span></span> |
| <span data-ttu-id="9409b-265">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-265">**args_ptr**</span></span> | <span data-ttu-id="9409b-266">Parametro non utilizzato per la lettura.</span><span class="sxs-lookup"><span data-stu-id="9409b-266">Unused parameter for read.</span></span> |
| <span data-ttu-id="9409b-267">**args_length**</span><span class="sxs-lookup"><span data-stu-id="9409b-267">**args_length**</span></span> | <span data-ttu-id="9409b-268">Parametro non utilizzato per la lettura.</span><span class="sxs-lookup"><span data-stu-id="9409b-268">Unused parameter for read.</span></span> |

### <a name="the-discover-method"></a><span data-ttu-id="9409b-269">Metodo ' Discover '</span><span class="sxs-lookup"><span data-stu-id="9409b-269">The ‘Discover’ Method</span></span>

<span data-ttu-id="9409b-270">Il metodo ' Discover ' viene usato per recuperare l'elenco di tutte le risorse implementate da un oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-270">The ‘Discover’ method is used to retrieve the list of all Resources implemented by an Object.</span></span> <span data-ttu-id="9409b-271">I parametri sono definiti nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="9409b-271">The parameters are defined as follows.</span></span>

| <span data-ttu-id="9409b-272">Parametro</span><span class="sxs-lookup"><span data-stu-id="9409b-272">Parameter</span></span> | <span data-ttu-id="9409b-273">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-273">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-274">**operation**</span><span class="sxs-lookup"><span data-stu-id="9409b-274">**operation**</span></span> | <span data-ttu-id="9409b-275">**NX_LWM2M_CLIENT_OBJECT_DISCOVER**</span><span class="sxs-lookup"><span data-stu-id="9409b-275">**NX_LWM2M_CLIENT_OBJECT_DISCOVER**</span></span> |
| <span data-ttu-id="9409b-276">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-276">**object_ptr**</span></span> | <span data-ttu-id="9409b-277">Puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-277">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="9409b-278">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-278">**instance_ptr**</span></span> | <span data-ttu-id="9409b-279">Puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-279">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="9409b-280">**risorse**</span><span class="sxs-lookup"><span data-stu-id="9409b-280">**resource**</span></span> | <span data-ttu-id="9409b-281">Puntatore a una matrice di NX_LWM2M_CLIENT_RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="9409b-281">Pointer to an array of NX_LWM2M_CLIENT_RESOURCE.</span></span> <span data-ttu-id="9409b-282">In restituzione la matrice viene riempita con le informazioni sulle risorse corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-282">On return the array is filled with corresponding resource info.</span></span> |
| <span data-ttu-id="9409b-283">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="9409b-283">**resource_count**</span></span> | <span data-ttu-id="9409b-284">Puntatore al numero di risorse da individuare.</span><span class="sxs-lookup"><span data-stu-id="9409b-284">Pointer to the number of resources to discover.</span></span> <span data-ttu-id="9409b-285">Al momento della restituzione, questo parametro deve essere aggiornato come valore true.</span><span class="sxs-lookup"><span data-stu-id="9409b-285">On return this parameter must be updated as the true value.</span></span> |
| <span data-ttu-id="9409b-286">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-286">**args_ptr**</span></span> | <span data-ttu-id="9409b-287">Parametro non utilizzato per l'individuazione.</span><span class="sxs-lookup"><span data-stu-id="9409b-287">Unused parameter for discover.</span></span> |
| <span data-ttu-id="9409b-288">**args_length**</span><span class="sxs-lookup"><span data-stu-id="9409b-288">**args_length**</span></span> | <span data-ttu-id="9409b-289">Parametro non utilizzato per l'individuazione.</span><span class="sxs-lookup"><span data-stu-id="9409b-289">Unused parameter for discover.</span></span> |

### <a name="the-write-method"></a><span data-ttu-id="9409b-290">Metodo ' Write '</span><span class="sxs-lookup"><span data-stu-id="9409b-290">The ‘Write’ Method</span></span>

<span data-ttu-id="9409b-291">Il metodo ' Write ' viene usato per aggiornare o sostituire le risorse di un'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-291">The ‘Write’ method is used to update or replace resources of an Object Instance.</span></span> <span data-ttu-id="9409b-292">I parametri sono definiti nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="9409b-292">The parameters are defined as follows.</span></span>

| <span data-ttu-id="9409b-293">Parametro</span><span class="sxs-lookup"><span data-stu-id="9409b-293">Parameter</span></span>  | <span data-ttu-id="9409b-294">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-294">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-295">**operation**</span><span class="sxs-lookup"><span data-stu-id="9409b-295">**operation**</span></span> | <span data-ttu-id="9409b-296">**NX_LWM2M_CLIENT_OBJECT_WRITE**</span><span class="sxs-lookup"><span data-stu-id="9409b-296">**NX_LWM2M_CLIENT_OBJECT_WRITE**</span></span> |
| <span data-ttu-id="9409b-297">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-297">**object_ptr**</span></span> | <span data-ttu-id="9409b-298">Puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-298">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="9409b-299">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-299">**instance_ptr**</span></span> | <span data-ttu-id="9409b-300">Puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-300">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="9409b-301">**risorse**</span><span class="sxs-lookup"><span data-stu-id="9409b-301">**resource**</span></span> | <span data-ttu-id="9409b-302">Puntatore a una matrice di **NX_LWM2M_CLIENT_RESOURCE** contenente gli ID delle risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="9409b-302">Pointer to an array of **NX_LWM2M_CLIENT_RESOURCE** containing the IDs of the resources to read.</span></span> <span data-ttu-id="9409b-303">In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-303">On return the array is filled with corresponding types and values.</span></span> |
| <span data-ttu-id="9409b-304">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="9409b-304">**resource_count**</span></span> | <span data-ttu-id="9409b-305">Puntatore al numero di risorse da individuare.</span><span class="sxs-lookup"><span data-stu-id="9409b-305">Pointer to the number of resources to discover.</span></span> |
| <span data-ttu-id="9409b-306">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-306">**args_ptr**</span></span> | <span data-ttu-id="9409b-307">Scrivi flag.</span><span class="sxs-lookup"><span data-stu-id="9409b-307">Write flags.</span></span> |
| <span data-ttu-id="9409b-308">**args_length**</span><span class="sxs-lookup"><span data-stu-id="9409b-308">**args_length**</span></span> | <span data-ttu-id="9409b-309">Lunghezza degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-309">The length of the arguments.</span></span> |

<span data-ttu-id="9409b-310">È possibile specificare le operazioni di scrittura seguenti per il parametro del *flag* .</span><span class="sxs-lookup"><span data-stu-id="9409b-310">The following write operations can be specified to the *flag* parameter.</span></span>

| <span data-ttu-id="9409b-311">Operazione</span><span class="sxs-lookup"><span data-stu-id="9409b-311">Operation</span></span> | <span data-ttu-id="9409b-312">Azione</span><span class="sxs-lookup"><span data-stu-id="9409b-312">Action</span></span> | <span data-ttu-id="9409b-313">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-313">Description</span></span> |
| --- | ---| --- |
| <span data-ttu-id="9409b-314">0</span><span class="sxs-lookup"><span data-stu-id="9409b-314">0</span></span> | <span data-ttu-id="9409b-315">Aggiornamento parziale</span><span class="sxs-lookup"><span data-stu-id="9409b-315">Partial Update</span></span> | <span data-ttu-id="9409b-316">Aggiunge o aggiorna le risorse fornite nel nuovo valore e lascia invariate le altre risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-316">Adds or updates Resources provided in the new value and leaves other existing Resources unchanged.</span></span>
| <span data-ttu-id="9409b-317">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE**</span><span class="sxs-lookup"><span data-stu-id="9409b-317">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE**</span></span> | <span data-ttu-id="9409b-318">Sostituisci istanza</span><span class="sxs-lookup"><span data-stu-id="9409b-318">Replace Instance</span></span> | <span data-ttu-id="9409b-319">Sostituisce l'istanza dell'oggetto con i nuovi valori di risorsa specificati.</span><span class="sxs-lookup"><span data-stu-id="9409b-319">Replaces the Object Instance with the new provided resource values.</span></span>
| <span data-ttu-id="9409b-320">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE**</span><span class="sxs-lookup"><span data-stu-id="9409b-320">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE**</span></span> |  <span data-ttu-id="9409b-321">Sostituisci risorsa</span><span class="sxs-lookup"><span data-stu-id="9409b-321">Replace Resource</span></span> | <span data-ttu-id="9409b-322">Sostituisce le risorse con i nuovi valori di risorsa forniti, usati per sostituire più risorse.</span><span class="sxs-lookup"><span data-stu-id="9409b-322">Replaces the Resources with the new provided resource values (used to replace Multiple Resources).</span></span> |
| <span data-ttu-id="9409b-323">**NX_LWM2M_CLIENT_OBJECT_WRITE_CREATE**</span><span class="sxs-lookup"><span data-stu-id="9409b-323">**NX_LWM2M_CLIENT_OBJECT_WRITE_CREATE**</span></span> | <span data-ttu-id="9409b-324">creare un'istanza</span><span class="sxs-lookup"><span data-stu-id="9409b-324">Create Instance</span></span> | <span data-ttu-id="9409b-325">Inizializza l'istanza dell'oggetto appena creata con i valori di risorsa forniti, chiamati dal metodo **_nx_lwm2m_object_create_** .</span><span class="sxs-lookup"><span data-stu-id="9409b-325">Initializes the newly created Object Instance with the provided resource values (called from the **_nx_lwm2m_object_create_** method).</span></span> |
| <span data-ttu-id="9409b-326">**NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP**</span><span class="sxs-lookup"><span data-stu-id="9409b-326">**NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP**</span></span> | <span data-ttu-id="9409b-327">Scrittura bootstrap</span><span class="sxs-lookup"><span data-stu-id="9409b-327">Bootstrap Write</span></span> | <span data-ttu-id="9409b-328">Chiamato durante la sequenza di bootstrap.</span><span class="sxs-lookup"><span data-stu-id="9409b-328">Called during Bootstrap sequence.</span></span> |

### <a name="the-execute-method"></a><span data-ttu-id="9409b-329">Metodo ' Execute '</span><span class="sxs-lookup"><span data-stu-id="9409b-329">The ‘Execute’ Method</span></span>

<span data-ttu-id="9409b-330">Il metodo ' Execute ' implementa l'esecuzione di una risorsa dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-330">The ‘Execute’ method implements the execution of an Object Resource.</span></span>

<span data-ttu-id="9409b-331">I parametri di input sono definiti nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="9409b-331">The input parameters are defined as follows.</span></span>

| <span data-ttu-id="9409b-332">Parametro</span><span class="sxs-lookup"><span data-stu-id="9409b-332">Parameter</span></span>  | <span data-ttu-id="9409b-333">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-333">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-334">**operation**</span><span class="sxs-lookup"><span data-stu-id="9409b-334">**operation**</span></span> | <span data-ttu-id="9409b-335">NX_LWM2M_CLIENT_OBJECT_EXECUTE</span><span class="sxs-lookup"><span data-stu-id="9409b-335">NX_LWM2M_CLIENT_OBJECT_EXECUTE</span></span> |
| <span data-ttu-id="9409b-336">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-336">**object_ptr**</span></span> | <span data-ttu-id="9409b-337">Puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-337">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="9409b-338">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-338">**instance_ptr**</span></span> | <span data-ttu-id="9409b-339">Puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-339">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="9409b-340">**risorse**</span><span class="sxs-lookup"><span data-stu-id="9409b-340">**resource**</span></span> | <span data-ttu-id="9409b-341">Puntatore a una matrice di **NX_LWM2M_CLIENT_RESOURCE** contenente gli ID delle risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="9409b-341">Pointer to an array of **NX_LWM2M_CLIENT_RESOURCE** containing the IDs of the resources to read.</span></span> <span data-ttu-id="9409b-342">In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-342">On return the array is filled with corresponding types and values.</span></span> |
| <span data-ttu-id="9409b-343">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="9409b-343">**resource_count**</span></span> | <span data-ttu-id="9409b-344">Puntatore al numero di risorse da individuare.</span><span class="sxs-lookup"><span data-stu-id="9409b-344">Pointer to the number of resources to discover.</span></span> |
| <span data-ttu-id="9409b-345">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-345">**args_ptr**</span></span> | <span data-ttu-id="9409b-346">Puntatore agli argomenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-346">Pointer to the arguments.</span></span> |
| <span data-ttu-id="9409b-347">**args_length**</span><span class="sxs-lookup"><span data-stu-id="9409b-347">**args_length**</span></span> | <span data-ttu-id="9409b-348">Lunghezza degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-348">The length of the arguments.</span></span>  |

<span data-ttu-id="9409b-349">La funzione deve restituire **NX_LWM2M_CLIENT_NOT_FOUND** se l'ID risorsa non esiste oppure **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** se non supporta l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9409b-349">The function must return **NX_LWM2M_CLIENT_NOT_FOUND** if the Resource ID doesn’t exist, or **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** if it doesn’t support execution.</span></span>

### <a name="the-create-method"></a><span data-ttu-id="9409b-350">Metodo ' Create '</span><span class="sxs-lookup"><span data-stu-id="9409b-350">The ‘Create’ Method</span></span>

<span data-ttu-id="9409b-351">Il metodo ' Create ' implementa la creazione di una nuova istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-351">The ‘Create’ method implements the creation of a new Object Instance.</span></span>

<span data-ttu-id="9409b-352">I parametri di input sono definiti nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="9409b-352">The input parameters are defined as follows.</span></span>

| <span data-ttu-id="9409b-353">Parametro</span><span class="sxs-lookup"><span data-stu-id="9409b-353">Parameter</span></span>  | <span data-ttu-id="9409b-354">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-355">**operation**</span><span class="sxs-lookup"><span data-stu-id="9409b-355">**operation**</span></span> | <span data-ttu-id="9409b-356">**NX_LWM2M_CLIENT_OBJECT_CREATE**</span><span class="sxs-lookup"><span data-stu-id="9409b-356">**NX_LWM2M_CLIENT_OBJECT_CREATE**</span></span> |
| <span data-ttu-id="9409b-357">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-357">**object_ptr**</span></span> | <span data-ttu-id="9409b-358">Puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-358">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="9409b-359">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-359">**instance_ptr**</span></span> | <span data-ttu-id="9409b-360">Parametro non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9409b-360">Unused parameter.</span></span> |
| <span data-ttu-id="9409b-361">**risorse**</span><span class="sxs-lookup"><span data-stu-id="9409b-361">**resource**</span></span> | <span data-ttu-id="9409b-362">Puntatore a una matrice di **NX_LWM2M_CLIENT_RESOURCE** contenente gli ID delle risorse da leggere.</span><span class="sxs-lookup"><span data-stu-id="9409b-362">Pointer to an array of **NX_LWM2M_CLIENT_RESOURCE** containing the IDs of the resources to read.</span></span> <span data-ttu-id="9409b-363">In restituzione la matrice viene riempita con i tipi e i valori corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-363">On return the array is filled with corresponding types and values.</span></span> |
| <span data-ttu-id="9409b-364">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="9409b-364">**resource_count**</span></span> | <span data-ttu-id="9409b-365">Puntatore al numero di risorse da individuare.</span><span class="sxs-lookup"><span data-stu-id="9409b-365">Pointer to the number of resources to discover.</span></span> |
| <span data-ttu-id="9409b-366">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-366">**args_ptr**</span></span> | <span data-ttu-id="9409b-367">ID istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-367">Object instance id.</span></span> |
| <span data-ttu-id="9409b-368">**args_length**</span><span class="sxs-lookup"><span data-stu-id="9409b-368">**args_length**</span></span> | <span data-ttu-id="9409b-369">Lunghezza degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="9409b-369">The length of the arguments.</span></span> |

### <a name="the-delete-method"></a><span data-ttu-id="9409b-370">Metodo ' Delete '</span><span class="sxs-lookup"><span data-stu-id="9409b-370">The ‘Delete’ Method</span></span>

<span data-ttu-id="9409b-371">Il metodo ' Delete ' implementa l'eliminazione di un'istanza dell'oggetto, i parametri di input vengono definiti come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9409b-371">The ‘Delete’ method implements the deletion of an object instance, the input parameters are defined as follows.</span></span>

| <span data-ttu-id="9409b-372">Parametro</span><span class="sxs-lookup"><span data-stu-id="9409b-372">Parameter</span></span>  | <span data-ttu-id="9409b-373">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9409b-373">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9409b-374">**operation**</span><span class="sxs-lookup"><span data-stu-id="9409b-374">**operation**</span></span> | <span data-ttu-id="9409b-375">NX_LWM2M_CLIENT_OBJECT_DELETE</span><span class="sxs-lookup"><span data-stu-id="9409b-375">NX_LWM2M_CLIENT_OBJECT_DELETE</span></span> |
| <span data-ttu-id="9409b-376">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-376">**object_ptr**</span></span> | <span data-ttu-id="9409b-377">Puntatore all'implementazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-377">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="9409b-378">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-378">**instance_ptr**</span></span> | <span data-ttu-id="9409b-379">Puntatore all'istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9409b-379">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="9409b-380">**risorse**</span><span class="sxs-lookup"><span data-stu-id="9409b-380">**resource**</span></span> | <span data-ttu-id="9409b-381">Parametro non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9409b-381">Unused parameter.</span></span> |
| <span data-ttu-id="9409b-382">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="9409b-382">**resource_count**</span></span> | <span data-ttu-id="9409b-383">Parametro non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9409b-383">Unused parameter.</span></span> |
| <span data-ttu-id="9409b-384">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="9409b-384">**args_ptr**</span></span> | <span data-ttu-id="9409b-385">Parametro non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9409b-385">Unused parameter.</span></span> |
| <span data-ttu-id="9409b-386">**args_length**</span><span class="sxs-lookup"><span data-stu-id="9409b-386">**args_length**</span></span> | <span data-ttu-id="9409b-387">Parametro non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9409b-387">Unused parameter.</span></span> |

<span data-ttu-id="9409b-388">In caso di esito positivo, l'oggetto deve rilasciare i dati dell'istanza dell'oggetto e qualsiasi altra risorsa allocata dall'istanza.</span><span class="sxs-lookup"><span data-stu-id="9409b-388">On success the Object must release the Object Instance data and any other resource allocated by the instance.</span></span>

## <a name="example-of-lwm2m-client-application"></a><span data-ttu-id="9409b-389">Esempio di applicazione client LWM2M</span><span class="sxs-lookup"><span data-stu-id="9409b-389">Example of LWM2M Client Application</span></span>

<span data-ttu-id="9409b-390">Il codice seguente è un esempio di una semplice applicazione client LWM2M che implementa un dispositivo personalizzato costituito da un sensore di temperatura e da un Commuter leggero.</span><span class="sxs-lookup"><span data-stu-id="9409b-390">The following code is an example of a simple LWM2M Client Application which implements a custom device consisting of a temperature sensor and a light switch.</span></span>

<span data-ttu-id="9409b-391">Il dispositivo consente a un server di leggere il valore del sensore di temperatura e lo stato booleano del Commuter e di impostare lo switch di luce su on/off.</span><span class="sxs-lookup"><span data-stu-id="9409b-391">The device allows a server to read the value of the temperature sensor and the boolean state of the light switch, and to set the light switch to on/off.</span></span>

```c
#include "nx_lwm2m_client.h"


/* Custom Object implementation. */

/* Temperature Object ID and resource IDs. */
#define IPSO_TEMPERATURE_OBJECT_ID   3303

#define IPSO_RESOURCE_MIN_VALUE      5601
#define IPSO_RESOURCE_MAX_VALUE      5602
#define IPSO_RESOURCE_RESET_MINMAX   5605
#define IPSO_RESOURCE_VALUE          5700
#define IPSO_RESOURCE_UNITS          5701

/* Actuation Object ID and resource IDs. */
#define IPSO_ACTUATION_OBJECT_ID     3306

#define IPSO_RESOURCE_ONOFF          5850

/* Define the Temperature Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_CLIENT_OBJECT_INSTANCE    object_instance;

    /* Resources Data */
    NX_LWM2M_FLOAT32                   temperature;
    NX_LWM2M_FLOAT32                   min_temperature;
    NX_LWM2M_FLOAT32                   max_temperature;

} IPSO_TEMPERATURE_INSTANCE;

/* Define the Actuation Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_CLIENT_OBJECT_INSTANCE    object_instance;

    /* Resources Data */
    NX_LWM2M_BOOL                      onoff;

} IPSO_ACTUATION_INSTANCE;

/* IPSO Temperature */
/* Define the 'Read' Method */
UINT ipso_temperature_read(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count)
{
IPSO_TEMPERATURE_INSTANCE *temp = ((IPSO_TEMPERATURE_INSTANCE *) instance_ptr);
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_MIN_VALUE:

            /* return the minimum measured temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> min_temperature);
            break;

        case IPSO_RESOURCE_MAX_VALUE:

            /* return the maximum measured temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> max_temperature);
            break;

        case IPSO_RESOURCE_VALUE:

            /* return the temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> temperature);
            break;

        case IPSO_RESOURCE_RESET_MINMAX:

            /* Not readable */
            return(NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED);

        case IPSO_RESOURCE_UNITS:

            /* return the temperature units */
            nx_lwm2m_client_resource_string_set(&resource[i], "Cel", 3);
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}

/* Define the 'Discover' method */
UINT ipso_temperature_discover(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resources, UINT *resource_count)
{
    if (*resource_count < 5)
    {
        return(NX_LWM2M_CLIENT_BUFFER_TOO_SMALL);
    }

    /* return the list of supported resources IDs */
    *resource_count = 5;
    nx_lwm2m_client_resource_info_set(&resources[0], IPSO_RESOURCE_MIN_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[1], IPSO_RESOURCE_MAX_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[2], IPSO_RESOURCE_RESET_MINMAX, NX_LWM2M_CLIENT_RESOURCE_OPERATION_EXECUTABLE);
    nx_lwm2m_client_resource_info_set(&resources[3], IPSO_RESOURCE_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[4], IPSO_RESOURCE_UNITS, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);

    return(NX_SUCCESS);
}

/* Define the 'Execute' method */
UINT ipso_temperature_execute(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, const CHAR *args_ptr, UINT args_length)
{
IPSO_TEMPERATURE_INSTANCE *temp = ((IPSO_TEMPERATURE_INSTANCE *) instance_ptr);
NX_LWM2M_CLIENT_RESOURCE value;
NX_LWM2M_ID resource_id;

    /* Get resource id */
    nx_lwm2m_client_resource_info_get(resource, &resource_id, NX_NULL);

    switch (resource_id)
    {

    case IPSO_RESOURCE_MIN_VALUE:
    case IPSO_RESOURCE_MAX_VALUE:
    case IPSO_RESOURCE_VALUE:
    case IPSO_RESOURCE_UNITS:

        /* read-only resource */
        return(NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED);

    case IPSO_RESOURCE_RESET_MINMAX:

        /* reset min/max values to current temperature */
        nx_lwm2m_client_resource_float32_set(&value, temp -> temperature);
        if (temp -> min_temperature != temp -> temperature)
        {
            temp -> min_temperature = temp -> temperature;
            nx_lwm2m_client_resource_info_set(&value, IPSO_RESOURCE_MIN_VALUE, NX_NULL);
            nx_lwm2m_client_object_resource_changed(object_ptr, instance_ptr, &value);
        }
        if (temp -> max_temperature != temp -> temperature)
        {
            temp -> max_temperature = temp -> temperature;
            nx_lwm2m_client_resource_info_set(&value, IPSO_RESOURCE_MAX_VALUE, NX_NULL);
            nx_lwm2m_client_object_resource_changed(object_ptr, instance_ptr, &value);
        }

        break;

    default:

        /* unknown resource ID */
        return(NX_LWM2M_CLIENT_NOT_FOUND);
    }

    return(NX_SUCCESS);
}

/* Define the operation callback function of Temperature Object */
UINT ipso_temperature_operation(UINT operation, NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT *resource_count, VOID *args_ptr, UINT args_length)
{

    switch (operation)
    {
    case NX_LWM2M_CLIENT_OBJECT_READ:

        /* Call read function */
        return ipso_temperature_read(object_ptr, object_instance_ptr, resource, *resource_count);
    case NX_LWM2M_CLIENT_OBJECT_DISCOVER:

        /* Call discover function */
        return ipso_temperature_discover(object_ptr, object_instance_ptr, resource, resource_count);

    case NX_LWM2M_CLIENT_OBJECT_EXECUTE:

        /* Call execute function */
        return ipso_temperature_execute(object_ptr, object_instance_ptr, resource, args_ptr, args_length);
    default:

        /*Unsupported operation */
        return(NX_LWM2M_CLIENT_NOT_SUPPORTED);
    }
}


/* IPSO Actuation */
/* Define the 'Read' Method */
UINT ipso_actuation_read(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count)
{
IPSO_ACTUATION_INSTANCE *act = ((IPSO_ACTUATION_INSTANCE *) instance_ptr);
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_ONOFF:

            /* return the on/off value */
            nx_lwm2m_client_resource_boolean_set(&resource[i], act -> onoff);
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}


/* Define the 'Discover' method */
UINT ipso_actuation_discover(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resources, UINT *resource_count)
{
    if (*resource_count < 1)
    {
        return(NX_LWM2M_CLIENT_BUFFER_TOO_SMALL);
    }

    /* return the list of supported resources IDs */
    *resource_count = 1;
    nx_lwm2m_client_resource_info_set(&resources[0], IPSO_RESOURCE_ONOFF, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ_WRITE);

    return(NX_SUCCESS);
}

/* Define the 'Write' method */
UINT ipso_actuation_write(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count, UINT flags)
{
IPSO_ACTUATION_INSTANCE *act = ((IPSO_ACTUATION_INSTANCE *) instance_ptr);
UINT ret;
NX_LWM2M_BOOL onoff;
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_ONOFF:

            /* assign on/off boolean value */
            ret = nx_lwm2m_client_resource_boolean_get(&resource[i], &onoff);
            if (ret != NX_SUCCESS)
            {
                /* invalid value type */
                return(ret);
            }
            if (onoff != act->onoff)
            {
                act->onoff = onoff;

                printf("Set actuation switch %s\n", onoff ? "On" : "Off");
            }
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}

/* Define the operation callback function of Actuation Object */
UINT ipso_actuation_operation(UINT operation, NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT *resource_count, VOID *args_ptr, UINT args_length)
{
UINT write_op;

    switch (operation)
    {
    case NX_LWM2M_CLIENT_OBJECT_READ:

        /* Call read function */
        return ipso_actuation_read(object_ptr, object_instance_ptr, resource, *resource_count);
    case NX_LWM2M_CLIENT_OBJECT_DISCOVER:

        /* Call discover function */
        return ipso_actuation_discover(object_ptr, object_instance_ptr, resource, resource_count);
    case NX_LWM2M_CLIENT_OBJECT_WRITE:

        /* Get the type of write operation */
        write_op = *(UINT *)args_ptr;

        /* Call write function */
        return ipso_actuation_write(object_ptr, object_instance_ptr, resource, *resource_count, write_op);
    default:

        /* Unsupported operation */
        return(NX_LWM2M_CLIENT_NOT_SUPPORTED);
    }
}


/* NetX data.  */
NX_IP                   ip_0;
NX_PACKET_POOL          pool_0;

/* LWM2M Client data.  */
NX_LWM2M_CLIENT         client;
ULONG                   client_stack[4096 / sizeof(ULONG)];
NX_LWM2M_CLIENT_SESSION session;

/* Objects and instances.  */
NX_LWM2M_CLIENT_OBJECT      temperature_object;
NX_LWM2M_CLIENT_OBJECT      actuation_object;
IPSO_TEMPERATURE_INSTANCE   temperature_instance;
IPSO_ACTUATION_INSTANCE     actuation_instance;

/* Define the session state callback */
void session_callback(NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state)
{
    printf("LWM2M Callback: -> %d\n", state);

    switch (state)
    {

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING:

        printf("Start client initiated bootstrap\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED:

        printf("Got message from boostrap server\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:

         /* Bootstrap session done, we can register to the LWM2M Server */
        printf( "Boostrap finished.\n");
#ifdef BOOTSTRAP
        tx_semaphore_put(&semaphore_bootstarp_finish);
#endif
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:

        /* Failed to Bootstrap the LWM2M Client. */
        printf( "Failed to boostrap device, error=%02x\n", nx_lwm2m_client_session_error_get(session_ptr));
        break;

    case NX_LWM2M_CLIENT_SESSION_REGISTERED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device registered.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_DISABLED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device disabled.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_DEREGISTERED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device deregistered.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_ERROR:

        /* Failed to register to the LWM2M Client. */
        printf( "Failed to register device, error=%02x\n", nx_lwm2m_client_session_error_get(session_ptr));
        break;
    }
}


/* Application main thread */
void application_thread(ULONG info)
{

UINT status;
NX_LWM2M_ID server_id = 0;
NXD_ADDRESS server_addr;
CHAR *server_uri = NX_NULL;
UINT server_uri_len = 0;
UCHAR security_mode = 0;
   
    /* Create the LWM2M client */
    status = nx_lwm2m_client_create(&client, &ip_0, &pool_0, "nxlwm2mclient", sizeof("nxlwm2mclient") - 1, NX_NULL, 0, NX_LWM2M_CLIENT_BINDING_U, client_stack, sizeof(client_stack), 4);
    if (status)
    {
        return;
    }

    /* Define our custom objects: */
    /* Add Temperature Object */
    status = nx_lwm2m_client_object_add(&client, &temperature_object, IPSO_TEMPERATURE_OBJECT_ID, ipso_temperature_operation);
    if (status)
    {
        return;
    }

    /* Define a single instance */
    temperature_instance.temperature = 22.5f;
    temperature_instance.min_temperature = temperature_instance.temperature;
    temperature_instance.max_temperature = temperature_instance.temperature;
    status = nx_lwm2m_client_object_instance_add(&temperature_object, &temperature_instance.object_instance, NX_NULL);
    if (status)
    {
        return;
    }

    /* Add Actuation Object */
    status = nx_lwm2m_client_object_add(&client, &actuation_object, IPSO_ACTUATION_OBJECT_ID, ipso_actuation_operation);
    if (status)
    {
        return;
    }

    /* Define a single instance */
    actuation_instance.onoff = NX_FALSE;
    status = nx_lwm2m_client_object_instance_add(&actuation_object, &actuation_instance.object_instance, NX_NULL);
    if (status)
    {
        return;
    }

    /* Create a session */
    status = nx_lwm2m_client_session_create(&session, &client, session_callback);
    if (status)
    {
        return;
}

    /* Set bootstrap server address.  */
    server_addr.nxd_ip_version = NX_IP_VERSION_V4;
    server_addr.nxd_ip_address.v4 = IP_ADDRESS(23, 97, 187, 154);

    printf("Start boostraping\r\n");
    status = nx_lwm2m_client_session_bootstrap(&session, 0, &server_addr, 5783);
    if (status)
    {
        return;
    }

    status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_len, &security_mode, NX_NULL, NX_NULL, NX_NULL, NX_NULL, NX_NULL, NX_NULL);
    if (status || (security_mode != NX_LWM2M_CLIENT_SECURITY_MODE_NOSEC))
    {
        return;
    }

printf("Register to LWM2M server\r\n");
status = nx_lwm2m_client_session_register(&session, server_id, &server_addr, 5683);

    if (status)
    {
        return;
    }

    /* Application main loop */
    while (1)
    {

        /* application code... */
        tx_thread_sleep(NX_IP_PERIODIC_RATE);
    }

    /* Terminate the LWM2M Client */
    nx_lwm2m_client_delete(&client);
}

```