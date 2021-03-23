---
title: Capitolo 3-Descrizione dei servizi client di Azure RTO NetX Duo MQTT
description: Questo capitolo contiene una descrizione di tutti i servizi client NetX Duo MQTT (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9cbb65946c45bfbc476091f7c604346e839a42fc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821800"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-mqtt-client-services"></a><span data-ttu-id="ea05f-103">Capitolo 3-Descrizione dei servizi client di Azure RTO NetX Duo MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-103">Chapter 3 - Description of Azure RTOS NetX Duo MQTT client services</span></span>

<span data-ttu-id="ea05f-104">Questo capitolo contiene una descrizione di tutti i servizi client di Azure RTO NetX Duo MQTT (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="ea05f-104">This chapter contains a description of all Azure RTOS NetX Duo MQTT client services (listed below) in alphabetical order.</span></span>

<span data-ttu-id="ea05f-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="ea05f-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="ea05f-106">**nxd_mqtt_client_create** *creare un'istanza del client MQTT*</span><span class="sxs-lookup"><span data-stu-id="ea05f-106">**nxd_mqtt_client_create** *Create MQTT client instance*</span></span>
- <span data-ttu-id="ea05f-107">**nxd_mqtt_client_will_message_set** *impostare il messaggio*</span><span class="sxs-lookup"><span data-stu-id="ea05f-107">**nxd_mqtt_client_will_message_set** *Set the will message*</span></span>
- <span data-ttu-id="ea05f-108">**nxd_mqtt_client_client_login_set** *impostare il nome utente e la password di accesso client MQTT*</span><span class="sxs-lookup"><span data-stu-id="ea05f-108">**nxd_mqtt_client_client_login_set** *Set MQTT client login username and password*</span></span>
- <span data-ttu-id="ea05f-109">**nxd_mqtt_client_connect** *connettere il client MQTT al broker*</span><span class="sxs-lookup"><span data-stu-id="ea05f-109">**nxd_mqtt_client_connect** *Connect MQTT Client to the broker*</span></span>
- <span data-ttu-id="ea05f-110">**nxd_mqtt_client_secure_connect** *connettere il client MQTT al broker con sicurezza TLS*</span><span class="sxs-lookup"><span data-stu-id="ea05f-110">**nxd_mqtt_client_secure_connect** *Connect MQTT client to the broker with TLS security*</span></span>
- <span data-ttu-id="ea05f-111">**nxd_mqtt_client_publish** *pubblicare un messaggio tramite Service Broker.*</span><span class="sxs-lookup"><span data-stu-id="ea05f-111">**nxd_mqtt_client_publish** *Publish a message through the broker.*</span></span>
- <span data-ttu-id="ea05f-112">**nxd_mqtt_client_subscribe** *sottoscrivere un argomento*</span><span class="sxs-lookup"><span data-stu-id="ea05f-112">**nxd_mqtt_client_subscribe** *Subscribe to a topic*</span></span>
- <span data-ttu-id="ea05f-113">**nxd_mqtt_client_unsubscribe** *annullare la sottoscrizione a un argomento*</span><span class="sxs-lookup"><span data-stu-id="ea05f-113">**nxd_mqtt_client_unsubscribe** *Unsubscribe from a topic*</span></span>
- <span data-ttu-id="ea05f-114">**nxd_mqtt_client_receive_notify_set** *impostare la funzione di callback di ricezione notifiche messaggio MQTT*</span><span class="sxs-lookup"><span data-stu-id="ea05f-114">**nxd_mqtt_client_receive_notify_set** *Set MQTT message receive notify callback function*</span></span>
- <span data-ttu-id="ea05f-115">**nxd_mqtt_client_message_get** *recuperare un messaggio dal broker*</span><span class="sxs-lookup"><span data-stu-id="ea05f-115">**nxd_mqtt_client_message_get** *Retrieve a message from the broker*</span></span>
- <span data-ttu-id="ea05f-116">**nxd_mqtt_client_disconnect_notify_set** *impostare la funzione di callback Notify DISconnessione messaggio MQTT*</span><span class="sxs-lookup"><span data-stu-id="ea05f-116">**nxd_mqtt_client_disconnect_notify_set** *Set MQTT message disconnect notify callback function*</span></span>
- <span data-ttu-id="ea05f-117">**nxd_mqtt_client_disconnect** *disconnettere il client MQTT dal broker*</span><span class="sxs-lookup"><span data-stu-id="ea05f-117">**nxd_mqtt_client_disconnect** *Disconnect MQTT client from the broker*</span></span>
- <span data-ttu-id="ea05f-118">**nxd_mqtt_client_delete** *eliminare l'istanza del client MQTT*</span><span class="sxs-lookup"><span data-stu-id="ea05f-118">**nxd_mqtt_client_delete** *Delete the MQTT client instance*</span></span>

## <a name="nxd_mqtt_client_create"></a><span data-ttu-id="ea05f-119">nxd_mqtt_client_create</span><span class="sxs-lookup"><span data-stu-id="ea05f-119">nxd_mqtt_client_create</span></span>

<span data-ttu-id="ea05f-120">Creare un'istanza del client MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-120">Create MQTT Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-121">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-121">Prototype</span></span>

```c
UINT nxd_mqtt_client_create(NXD_MQTT_CLIENT *client_ptr,
    CHAR *client_name, CHAR *client_id,
    UINT client_id_length, NX_IP *ip_ptr, NX_PACKET_POOL
    *pool_ptr, VOID *stack_ptr, ULONG stack_size, UINT
    mqtt_thread_priority,
    VOID *memory_ptr, ULONG memory_size);
```

### <a name="description"></a><span data-ttu-id="ea05f-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-122">Description</span></span>

<span data-ttu-id="ea05f-123">Questo servizio crea un'istanza del client MQTT nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="ea05f-123">This service creates an MQTT Client instance on the specified IP instance.</span></span> <span data-ttu-id="ea05f-124">La stringa *client_id* viene passata al server durante la fase di connessione MQTT come *identificatore client (ClientID)*.</span><span class="sxs-lookup"><span data-stu-id="ea05f-124">The *client_id* string is passed to the server during MQTT connection phase as the *Client Identifier (ClientId)*.</span></span> <span data-ttu-id="ea05f-125">Vengono inoltre create le risorse ThreadX necessarie (thread attività del client MQTT, mutex, gruppo di flag di evento e socket TCP).</span><span class="sxs-lookup"><span data-stu-id="ea05f-125">It also creates the necessary ThreadX resources (MQTT Client task thread, mutex, event flag group, and TCP socket).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-126">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-126">Input Parameters</span></span>

- <span data-ttu-id="ea05f-127">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-127">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-128">**client_name** Stringa del nome del client.</span><span class="sxs-lookup"><span data-stu-id="ea05f-128">**client_name** Client name string.</span></span>
- <span data-ttu-id="ea05f-129">**client_id** Stringa ID client utilizzata durante la fase di connessione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-129">**client_id** Client ID string used during connection phase.</span></span> <span data-ttu-id="ea05f-130">MQTT broker Usa questa client_id per identificare in modo univoco un client.</span><span class="sxs-lookup"><span data-stu-id="ea05f-130">MQTT broker uses this client_id to uniquely identify a client.</span></span>
- <span data-ttu-id="ea05f-131">**client_id_length** Lunghezza della stringa dell'ID client, in byte.</span><span class="sxs-lookup"><span data-stu-id="ea05f-131">**client_id_length** Length of the client ID string, in bytes.</span></span>
- <span data-ttu-id="ea05f-132">**ip_ptr** Puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="ea05f-132">**ip_ptr** Pointer to IP instance.</span></span>
- <span data-ttu-id="ea05f-133">**pool_ptr** Puntatore a un pool di pacchetti utilizzato dal client MQTT per il relativo funzionamento.</span><span class="sxs-lookup"><span data-stu-id="ea05f-133">**pool_ptr** Pointer to a packet pool MQTT client uses for its operation.</span></span>
- <span data-ttu-id="ea05f-134">**stack_ptr** Area dello stack per il thread del client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-134">**stack_ptr** Stack area for the MQTT Client thread.</span></span>
- <span data-ttu-id="ea05f-135">**stack_size** Dimensioni dell'area dello stack, in byte.</span><span class="sxs-lookup"><span data-stu-id="ea05f-135">**stack_size** Size of the stack area, in bytes.</span></span>
- <span data-ttu-id="ea05f-136">**mqtt_thread_priority** Priorità del thread MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-136">**mqtt_thread_priority** The priority of the MQTT Thread.</span></span>
- <span data-ttu-id="ea05f-137">**memory_ptr** Deprecato.</span><span class="sxs-lookup"><span data-stu-id="ea05f-137">**memory_ptr** Deprecated.</span></span> <span data-ttu-id="ea05f-138">Non più utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ea05f-138">Not used anymore.</span></span>
- <span data-ttu-id="ea05f-139">**memory_size** Deprecato.</span><span class="sxs-lookup"><span data-stu-id="ea05f-139">**memory_size** Deprecated.</span></span> <span data-ttu-id="ea05f-140">Non più utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ea05f-140">Not used anymore.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-141">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-141">Return Values</span></span>

- <span data-ttu-id="ea05f-142">**NXD_MQTT_SUCCESS** (0x00) ha creato il client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-142">**NXD_MQTT_SUCCESS** (0x00) Successfully created MQTT client.</span></span>
- <span data-ttu-id="ea05f-143">Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)</span><span class="sxs-lookup"><span data-stu-id="ea05f-143">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="ea05f-144">NX_PTR_ERROR (0x07): blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti non validi.</span><span class="sxs-lookup"><span data-stu-id="ea05f-144">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer.</span></span>
- <span data-ttu-id="ea05f-145">NXD_MQTT_INVALID_PARAMETER (0x10009) argomento non valido, will_retrain_flag o will_QoS valore.</span><span class="sxs-lookup"><span data-stu-id="ea05f-145">NXD_MQTT_INVALID_PARAMETER (0x10009) Invalid will topic string, will_retrain_flag, or will_QoS value.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-146">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-146">Allowed From</span></span>

<span data-ttu-id="ea05f-147">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-147">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-148">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-148">Example</span></span>

```c
#define CLIENT_ID_STRING "My Test Client"

#define MQTT_THREAD_PRIORITY 2

NXD_MQTT_CLIENT my_client;
NX_IP ip_0; /* Assume ip_0 is created prior to MQTT client creation. */
NX_PACKET_POOL pool_0;/* Assume pool_0 is created prior to MQTT client creation. */
UCHAR mqtt_thread_stack[STACK_SIZE];

/* Create the MQTT Client instance on "ip_0". */
status = **nxd_mqtt_client_create**(&my_client, "my client",
    CLIENT_ID_STRING, stlren(CLIENT_ID_STRING),
    &ip_0, &pool_0, (VOID*)mqtt_thread_stack, STACK_SIZE,
    MQTT_THREAD_PRIORITY, NX_NULL, 0);

/* If status is NXD_MQTT_SUCCESS an MQTT Client instance was successfully created. */
```

## <a name="nxd_mqtt_client_will_message_set"></a><span data-ttu-id="ea05f-149">nxd_mqtt_client_will_message_set</span><span class="sxs-lookup"><span data-stu-id="ea05f-149">nxd_mqtt_client_will_message_set</span></span>

<span data-ttu-id="ea05f-150">Imposta il messaggio di messaggio</span><span class="sxs-lookup"><span data-stu-id="ea05f-150">Sets the Will message</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-151">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-151">Prototype</span></span>

```c
UINT nxd_mqtt_client_will_message_set(NXD_MQTT_CLIENT
    *client_ptr,
    Const UCHAR *will_topic,
    UINT will_topic_length
    Const UCHAR *will_message,
    UINT will_message_length,
    UINT will_retain_flag,
    UINT will_QoS);
```

### <a name="description"></a><span data-ttu-id="ea05f-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-152">Description</span></span>

<span data-ttu-id="ea05f-153">Questo servizio imposta l'argomento facoltativo di e messaggio prima che il client si connetta al server.</span><span class="sxs-lookup"><span data-stu-id="ea05f-153">This service sets the optional will topic and will message before the client connects to the server.</span></span> <span data-ttu-id="ea05f-154">L'argomento deve essere una stringa con codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ea05f-154">Will topic must be UTF-8 encoded string.</span></span>

<span data-ttu-id="ea05f-155">Il messaggio, se impostato, verrà trasmesso al broker come parte del messaggio CONNECT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-155">The will message, if set, is transmitted to the broker as part of the CONNECT message.</span></span> <span data-ttu-id="ea05f-156">Per questo motivo, l'applicazione che vuole usare il messaggio deve usare questo servizio prima di eseguire la connessione MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-156">Therefore application wishing to use will message must use this service before the MQTT connection is make.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-157">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-157">Input Parameters</span></span>

- <span data-ttu-id="ea05f-158">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-158">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-159">**will_topic** La stringa dell'argomento con codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ea05f-159">**will_topic** UTF-8 encoded will topic string.</span></span> <span data-ttu-id="ea05f-160">È necessario che l'argomento sia presente.</span><span class="sxs-lookup"><span data-stu-id="ea05f-160">Will topic must be present.</span></span> <span data-ttu-id="ea05f-161">Il chiamante deve contenere la stringa will_topic valida fino a quando non viene effettuata la chiamata *nx_mqtt_client_connect* .</span><span class="sxs-lookup"><span data-stu-id="ea05f-161">Caller must keep the will_topic string valid till the *nx_mqtt_client_connect* call is made.</span></span>
- <span data-ttu-id="ea05f-162">**will_topic_length** Numero di byte nella stringa dell'argomento della funzione</span><span class="sxs-lookup"><span data-stu-id="ea05f-162">**will_topic_length** Number of bytes in the will topic string</span></span>
- <span data-ttu-id="ea05f-163">**will_message** Messaggio definito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-163">**will_message** Application defined will message.</span></span> <span data-ttu-id="ea05f-164">Se il messaggio non è necessario, l'applicazione può impostare questo campo su *NX_NULL.*</span><span class="sxs-lookup"><span data-stu-id="ea05f-164">If will message is not required, application can set this field to *NX_NULL.*</span></span>
- <span data-ttu-id="ea05f-165">**will_message_length** Numero di byte nella stringa del messaggio di messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-165">**will_message_length** Number of bytes in the will message string.</span></span> <span data-ttu-id="ea05f-166">Se will_message è impostato su NULL, will_message_length deve essere impostato su 0.</span><span class="sxs-lookup"><span data-stu-id="ea05f-166">If will_message is set to NULL, will_message_length must be set to 0.</span></span>
- <span data-ttu-id="ea05f-167">**will_retain_flag** Indica se il server pubblica il messaggio come messaggio mantenuto.</span><span class="sxs-lookup"><span data-stu-id="ea05f-167">**will_retain_flag** Whether the server publishes the will message as a retained message.</span></span> <span data-ttu-id="ea05f-168">I valori validi sono *NX_TRUE* o *NX_FALSE.*</span><span class="sxs-lookup"><span data-stu-id="ea05f-168">Valid values are *NX_TRUE* or *NX_FALSE.*</span></span>
- <span data-ttu-id="ea05f-169">**will_QoS** Valore QoS utilizzato dal server quando viene inviato un messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-169">**will_QoS** QoS value used by the server when sending will message.</span></span> <span data-ttu-id="ea05f-170">I valori validi sono 0 o 1.</span><span class="sxs-lookup"><span data-stu-id="ea05f-170">Valid values are 0 or 1.</span></span>  

### <a name="return-values"></a><span data-ttu-id="ea05f-171">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-171">Return Values</span></span>

- <span data-ttu-id="ea05f-172">**NXD_MQTT_SUCCESS** (0x00) imposta correttamente il messaggio di messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-172">**NXD_MQTT_SUCCESS** (0x00) Successfully sets the will message.</span></span>
- <span data-ttu-id="ea05f-173">I messaggi QoS di livello 2 **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="ea05f-173">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) QoS level 2 messages are not supported.</span></span>
- <span data-ttu-id="ea05f-174">NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido.</span><span class="sxs-lookup"><span data-stu-id="ea05f-174">NX_PTR_ERROR (0x07) Invalid MQTT control block.</span></span>
- <span data-ttu-id="ea05f-175">NXD_MQTT_INVALID_PARAMETER (0x10009) argomento non valido, will_retrain_flag o will_QoS valore.</span><span class="sxs-lookup"><span data-stu-id="ea05f-175">NXD_MQTT_INVALID_PARAMETER (0x10009) Invalid will topic string, will_retrain_flag, or will_QoS value.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-176">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-176">Allowed From</span></span>

<span data-ttu-id="ea05f-177">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-177">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-178">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-178">Example</span></span>

```c
#define WILL_TOPIC "my_will_topic"

#define WILL_MESSAGE "my will message"

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_will_message_set(&my_client,
    WILL_TOPIC, STRLEN(WILL_TOPIC),
    WILL_MESSAGE, STRLEN(WILL_MESSAGE),
    NX_TRUE, 0);

/* If status is NXD_MQTT_SUCCESS the will message is properly
configured for the session. It will be transmitted to the server
during MQTT connection. */
```

## <a name="nxd_mqtt_client_login_set"></a><span data-ttu-id="ea05f-179">nxd_mqtt_client_login_set</span><span class="sxs-lookup"><span data-stu-id="ea05f-179">nxd_mqtt_client_login_set</span></span>

<span data-ttu-id="ea05f-180">Imposta il nome utente e la password di accesso client MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-180">Sets MQTT client login username and password</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-181">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-181">Prototype</span></span>

```c
UINT nxd_mqtt_client_login_set(NXD_MQTT_CLIENT *client_ptr,
    Const UCHAR *username,
    UINT username_length
    Const UCHAR *password,
    UINT password_length);
```

### <a name="description"></a><span data-ttu-id="ea05f-182">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-182">Description</span></span>

<span data-ttu-id="ea05f-183">Questo servizio imposta il nome utente e la password, che viene usato durante la fase di connessione MQTT per lo scopo di autenticazione log.</span><span class="sxs-lookup"><span data-stu-id="ea05f-183">This service sets the username and password, which is used during MQTT connection phase for log in authentication purpose.</span></span>

<span data-ttu-id="ea05f-184">L'account di accesso del client MQTT con nome utente e password è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ea05f-184">The MQTT client login with username and password is optional.</span></span> <span data-ttu-id="ea05f-185">Nelle situazioni in cui il server richiede un nome utente e una password, il nome utente e la password devono essere impostati prima che venga stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-185">In situations where the server requires a user name and password, the user name and password must be set before the connection is established.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-186">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-186">Input Parameters</span></span>

- <span data-ttu-id="ea05f-187">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-187">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-188">**nome utente** Stringa del nome utente con codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ea05f-188">**username** UTF-8 encoded user name string.</span></span> <span data-ttu-id="ea05f-189">Il chiamante deve lasciare valida la stringa del nome utente fino a quando non viene effettuata la chiamata *nx_mqtt_client_connect* .</span><span class="sxs-lookup"><span data-stu-id="ea05f-189">Caller must keep the username string valid till the *nx_mqtt_client_connect* call is made.</span></span>
- <span data-ttu-id="ea05f-190">**username_length** Numero di byte nella stringa del nome utente</span><span class="sxs-lookup"><span data-stu-id="ea05f-190">**username_length** Number of bytes in the username string</span></span>
- <span data-ttu-id="ea05f-191">**password** di Stringa password.</span><span class="sxs-lookup"><span data-stu-id="ea05f-191">**password** Password string.</span></span> <span data-ttu-id="ea05f-192">Se la password non è obbligatoria, questo campo può essere impostato su NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="ea05f-192">If password is not required, this field may be set to NX_NULL.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-193">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-193">Return Values</span></span>

- <span data-ttu-id="ea05f-194">**NXD_MQTT_SUCCESS** (0x00) imposta correttamente il messaggio di messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-194">**NXD_MQTT_SUCCESS** (0x00) Successfully sets the will message.</span></span>
- <span data-ttu-id="ea05f-195">NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido.</span><span class="sxs-lookup"><span data-stu-id="ea05f-195">NX_PTR_ERROR (0x07) Invalid MQTT control block.</span></span>
- <span data-ttu-id="ea05f-196">NXD_MQTT_INVALID_PARAMETER (0x10009) stringa nome utente non valida o stringa password.</span><span class="sxs-lookup"><span data-stu-id="ea05f-196">NXD_MQTT_INVALID_PARAMETER (0x10009) Invalid username string or the password string.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-197">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-197">Allowed From</span></span>

<span data-ttu-id="ea05f-198">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-198">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-199">Example</span></span>

```c
#define USERNAME "MY_NAME"

#define PASSWORD "MY_LOGIN_SECRET"

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_login_set(&my_client,
    USERNAME, STRLEN(USERNAME),
    PASSWORD, STRLEN(PASSWORD));

/* If status is NXD_MQTT_SUCCESS the username and the password 
are set for the session. This information will be 
transmitted to the server during MQTT connection. */
```

## <a name="nxd_mqtt_client_connect"></a><span data-ttu-id="ea05f-200">nxd_mqtt_client_connect</span><span class="sxs-lookup"><span data-stu-id="ea05f-200">nxd_mqtt_client_connect</span></span>

<span data-ttu-id="ea05f-201">Connettere il client di MQTT al broker</span><span class="sxs-lookup"><span data-stu-id="ea05f-201">Connect MQTT Client to the broker</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-202">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-202">Prototype</span></span>

```c
UINT nxd_mqtt_client_connect(NXD_MQTT_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT keepalive, UINT clean_session, ULONG wait_option));
```

### <a name="description"></a><span data-ttu-id="ea05f-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-203">Description</span></span>

<span data-ttu-id="ea05f-204">Questo servizio avvia una connessione al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-204">This service initiates a connection to the broker.</span></span> <span data-ttu-id="ea05f-205">Innanzitutto associa un socket TCP, quindi crea una connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="ea05f-205">First it binds a TCP socket, then makes a TCP connection.</span></span> <span data-ttu-id="ea05f-206">Supponendo che abbia esito positivo, viene creato un timer se è abilitata la funzionalità MQTT Keep Alive.</span><span class="sxs-lookup"><span data-stu-id="ea05f-206">Assuming that succeeds, it creates a timer if the MQTT keep alive feature is enabled.</span></span> <span data-ttu-id="ea05f-207">Quindi si connette al server MQTT (Broker).</span><span class="sxs-lookup"><span data-stu-id="ea05f-207">Then it connects with the MQTT server (broker).</span></span>

<span data-ttu-id="ea05f-208">Si noti che questo servizio crea una connessione MQTT senza protezione TLS.</span><span class="sxs-lookup"><span data-stu-id="ea05f-208">Note that this service creates an MQTT connection with no TLS protection.</span></span> <span data-ttu-id="ea05f-209">Per creare una connessione MQTT protetta, è necessario che l'applicazione utilizzi il servizio ***nxd_mqtt_client_secure_connect ().***</span><span class="sxs-lookup"><span data-stu-id="ea05f-209">To create a secure MQTT connection, the application shall use the service ***nxd_mqtt_client_secure_connect().***</span></span>

<span data-ttu-id="ea05f-210">Al momento della connessione, se il client imposta il *clean_session* su NX_FALSE, il client ritrasmette tutti i messaggi archiviati che non sono ancora stati riconosciuti.</span><span class="sxs-lookup"><span data-stu-id="ea05f-210">Upon the connection, if the client sets the *clean_session* to NX_FALSE, the client will retransmit any messages stored that have not been acknowledged yet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-211">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-211">Input Parameters</span></span>

- <span data-ttu-id="ea05f-212">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-212">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-213">**server_ip** Indirizzo IP broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-213">**server_ip** Broker IP address.</span></span>
- <span data-ttu-id="ea05f-214">**SERVER_PORT** Numero di porta del broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-214">**server_port** Broker port number.</span></span> <span data-ttu-id="ea05f-215">La porta predefinita per MQTT è definita come **_NXD_MQTT_PORT_** (1883).</span><span class="sxs-lookup"><span data-stu-id="ea05f-215">The default port for MQTT is defined as **_NXD_MQTT_PORT_** (1883).</span></span>
- <span data-ttu-id="ea05f-216">**keep_alive** Valore Keep-Alive, in secondi, da utilizzare durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-216">**keep_alive** The keep alive value, in seconds, to be used during the session.</span></span> <span data-ttu-id="ea05f-217">Il valore indica il tempo massimo tra due messaggi di controllo MQTT inviati al broker prima del timeout del client da parte del broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-217">The value indicates the maximum time between two MQTT control messages being sent to the broker before the broker times out this client.</span></span> <span data-ttu-id="ea05f-218">Il valore 0 disattiva la funzionalità Keep-Alive.</span><span class="sxs-lookup"><span data-stu-id="ea05f-218">The value 0 turns off the keep-alive feature.</span></span>
- <span data-ttu-id="ea05f-219">**clean_session** Indica se il server deve avviare la sessione pulita.</span><span class="sxs-lookup"><span data-stu-id="ea05f-219">**clean_session** Whether the server shall start this session clean.</span></span> <span data-ttu-id="ea05f-220">Le opzioni valide sono **_NX_TRUE_*_ o _*_NX_FALSE._**</span><span class="sxs-lookup"><span data-stu-id="ea05f-220">Valid options are **_NX_TRUE_*_ or _*_NX_FALSE._**</span></span>
- <span data-ttu-id="ea05f-221">**WAIT_OPTION** Tempo di attesa della connessione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-221">**wait_option** Connection wait time.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-222">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-222">Return Values</span></span>

- <span data-ttu-id="ea05f-223">**NXD_MQTT_SUCCESS** (0x00) connessione MQTT riuscita</span><span class="sxs-lookup"><span data-stu-id="ea05f-223">**NXD_MQTT_SUCCESS** (0x00) Successful MQTT connection</span></span>
- <span data-ttu-id="ea05f-224">**NXD_MQTT_ALREADY_CONNECTED** (0X10001) il client è già connesso al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-224">**NXD_MQTT_ALREADY_CONNECTED** (0x10001) The client is already connected to the broker.</span></span>
- <span data-ttu-id="ea05f-225">**NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-225">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex</span></span> 
- <span data-ttu-id="ea05f-226">Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)</span><span class="sxs-lookup"><span data-stu-id="ea05f-226">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="ea05f-227">**NXD_MQTT_CONNECT_FAILURE** (0X10005) non è riuscito a connettersi al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-227">**NXD_MQTT_CONNECT_FAILURE** (0x10005) Failed to connect to the broker.</span></span>
- <span data-ttu-id="ea05f-228">**NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è in grado di inviare messaggi al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-228">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Unable to send messages to the broker.</span></span>
- <span data-ttu-id="ea05f-229">Il server **NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) ha risposto con errore</span><span class="sxs-lookup"><span data-stu-id="ea05f-229">**NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) Server responded with error</span></span>
- <span data-ttu-id="ea05f-230">Codice di risposta del server **NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081)</span><span class="sxs-lookup"><span data-stu-id="ea05f-230">**NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081) Server response code</span></span>
- <span data-ttu-id="ea05f-231">Codice di risposta del server **NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082)</span><span class="sxs-lookup"><span data-stu-id="ea05f-231">**NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082) Server response code</span></span>
- <span data-ttu-id="ea05f-232">Codice di risposta del server **NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083)</span><span class="sxs-lookup"><span data-stu-id="ea05f-232">**NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083) Server response code</span></span>
- <span data-ttu-id="ea05f-233">Codice di risposta del server **NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084)</span><span class="sxs-lookup"><span data-stu-id="ea05f-233">**NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084) Server response code</span></span>
- <span data-ttu-id="ea05f-234">Codice di risposta del server **NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085)</span><span class="sxs-lookup"><span data-stu-id="ea05f-234">**NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085) Server response code</span></span>
- <span data-ttu-id="ea05f-235">NX_PTR_ERROR (0x07) non valido: blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ea05f-235">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-236">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-236">Allowed From</span></span>

<span data-ttu-id="ea05f-237">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-237">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-238">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-238">Example</span></span>

```c
NXD_ADDRESS broker_address;

/* Set up broker IP address */
broker_address.nxd_ip_version = 4;
broker_address.nxd_ip_address.v4 = MQTT_BROKER_ADDRESS;

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_connect(&my_client, &broker_address,
    NXD_MQTT_PORT,
    0, /* Turn off keepalive */
    NX_TRUE, /* Clean session flag set */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS a connection to the broker is successfully established. */
```

## <a name="nxd_mqtt_client_secure_connect"></a><span data-ttu-id="ea05f-239">nxd_mqtt_client_secure_connect</span><span class="sxs-lookup"><span data-stu-id="ea05f-239">nxd_mqtt_client_secure_connect</span></span>

<span data-ttu-id="ea05f-240">Connettere il client di MQTT al broker con sicurezza TLS</span><span class="sxs-lookup"><span data-stu-id="ea05f-240">Connect MQTT client to the broker with TLS security</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-241">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-241">Prototype</span></span>

```c
UINT nxd_mqtt_client_secure_connect(NXD_MQTT_CLIENT
    *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT (*tls_setup)(NXD_MQTT_CLIENT *,
        NX_SECURE_TLS_SESISON *,
        NX_SECURE_TLS_CERTIFICATE *,
        NX_SECURE_TLS_CERTIFICATE *),
    UINT keepalive, UINT connection_flag,
    UINT clean_session, ULONG wait_option));
```

### <a name="description"></a><span data-ttu-id="ea05f-242">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-242">Description</span></span>

<span data-ttu-id="ea05f-243">Questo servizio è identico a ***nxd_mqtt_client_connect*** ad eccezione del fatto che la connessione passa attraverso il livello TLS anziché TCP.</span><span class="sxs-lookup"><span data-stu-id="ea05f-243">This service is identical to ***nxd_mqtt_client_connect*** except that the connection goes through TLS layer instead of TCP.</span></span> <span data-ttu-id="ea05f-244">Pertanto, la comunicazione tra il client e il broker è protetta.</span><span class="sxs-lookup"><span data-stu-id="ea05f-244">Therefore, communication between the client and the broker is secured.</span></span>

<span data-ttu-id="ea05f-245">Il *tls_setup* definito dall'utente è una funzione di callback utilizzata dal client di MQTT prima di eseguire una connessione client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-245">The user-defined *tls_setup* is a callback function that the MQTT client uses prior to making a MQTT client connection.</span></span> <span data-ttu-id="ea05f-246">L'applicazione deve inizializzare NetX Secure TLS, configurare i parametri di sicurezza e caricare i certificati rilevanti da usare durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="ea05f-246">The application shall initialize NetX Secure TLS, configure security parameters, and load relevant certificates to be used during TLS handshake.</span></span> <span data-ttu-id="ea05f-247">L'handshake TLS effettivo si verifica dopo che è stata stabilita una connessione TCP sulla porta TLS MQTT del broker (porta TCP predefinita 8883).</span><span class="sxs-lookup"><span data-stu-id="ea05f-247">The actual TLS handshake happens after a TCP connection is established on the broker's MQTT TLS port (default TCP port 8883).</span></span> <span data-ttu-id="ea05f-248">Una volta che l'handshake TLS ha avuto esito positivo, il pacchetto di controllo MQTT CONNECT viene inviato tramite TLS.</span><span class="sxs-lookup"><span data-stu-id="ea05f-248">Once the TLS handshake is successful, the MQTT CONNECT control packet is sent via TLS.</span></span>

<span data-ttu-id="ea05f-249">Per stabilire connessioni sicure, è necessario che sia disponibile la libreria NetX Secure TLS e che il client NetX Duo MQTT sia compilato con ***NX_SECURE_ENABLE*** definito.</span><span class="sxs-lookup"><span data-stu-id="ea05f-249">To make secure connections, the NetX Secure TLS library must be available, and the NetX Duo MQTT client must be built with ***NX_SECURE_ENABLE*** defined.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-250">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-250">Input Parameters</span></span>

- <span data-ttu-id="ea05f-251">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-251">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-252">**server_ip** Indirizzo IP broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-252">**server_ip** Broker IP address.</span></span>
- <span data-ttu-id="ea05f-253">**SERVER_PORT** Numero di porta del broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-253">**server_port** Broker port number.</span></span> <span data-ttu-id="ea05f-254">La porta predefinita per MQTT è definita come **_NXD_MQTT_TLS_PORT_** (8883).</span><span class="sxs-lookup"><span data-stu-id="ea05f-254">The default port for MQTT isdefined as **_NXD_MQTT_TLS_PORT_** (8883).</span></span>
- <span data-ttu-id="ea05f-255">**tls_setup** Funzione di callback di configurazione TLS fornita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ea05f-255">**tls_setup** User-provided TLS Setup callback function.</span></span> <span data-ttu-id="ea05f-256">Questa funzione di callback viene richiamata per configurare i parametri di connessione del client TLS.</span><span class="sxs-lookup"><span data-stu-id="ea05f-256">This callback function is invoked to set up TLS client connection parameters.</span></span>
- <span data-ttu-id="ea05f-257">**keep_alive** Valore Keep-Alive da utilizzare durante la sessione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-257">**keep_alive** The keep-alive value to be used during the session.</span></span> <span data-ttu-id="ea05f-258">Il valore 0 disattiva la funzionalità Keep-Alive.</span><span class="sxs-lookup"><span data-stu-id="ea05f-258">The value 0 turns off the keep-alive feature.</span></span>
- <span data-ttu-id="ea05f-259">**clean_session** Indica se il server deve avviare la sessione pulita.</span><span class="sxs-lookup"><span data-stu-id="ea05f-259">**clean_session** Whether or not the server shall start this session clean.</span></span> <span data-ttu-id="ea05f-260">Le opzioni valide sono **_NX_TRUE_*_ o _*_NX_FALSE._**</span><span class="sxs-lookup"><span data-stu-id="ea05f-260">Valid options are **_NX_TRUE_*_ or _*_NX_FALSE._**</span></span>
- <span data-ttu-id="ea05f-261">**WAIT_OPTION** Tempo di attesa della connessione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-261">**wait_option** Connection wait time.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-262">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-262">Return Values</span></span>

- <span data-ttu-id="ea05f-263">**NXD_MQTT_SUCCESS** (0x00) connessione client MQTT riuscita stabilita tramite TLS.</span><span class="sxs-lookup"><span data-stu-id="ea05f-263">**NXD_MQTT_SUCCESS** (0x00) Successful MQTT client connection established via TLS.</span></span>
- <span data-ttu-id="ea05f-264">**NXD_MQTT_ALREADY_CONNECTED** (0X10001) il client è già connesso al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-264">**NXD_MQTT_ALREADY_CONNECTED** (0x10001) The client is already connected to the broker.</span></span>
- <span data-ttu-id="ea05f-265">**NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-265">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex</span></span> 
- <span data-ttu-id="ea05f-266">Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)</span><span class="sxs-lookup"><span data-stu-id="ea05f-266">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="ea05f-267">**NXD_MQTT_CONNECT_FAILURE** (0X10005) non è riuscito a connettersi al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-267">**NXD_MQTT_CONNECT_FAILURE** (0x10005) Failed to connect to the broker.</span></span>
- <span data-ttu-id="ea05f-268">**NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è in grado di inviare messaggi al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-268">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Unable to send messages to the broker.</span></span>
- <span data-ttu-id="ea05f-269">Il server **NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) ha risposto con un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="ea05f-269">**NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) Server responded with error message.</span></span>
- <span data-ttu-id="ea05f-270">Codice di risposta del server **NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081)</span><span class="sxs-lookup"><span data-stu-id="ea05f-270">**NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081) Server response code</span></span>
- <span data-ttu-id="ea05f-271">Codice di risposta del server **NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082)</span><span class="sxs-lookup"><span data-stu-id="ea05f-271">**NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082) Server response code</span></span>
- <span data-ttu-id="ea05f-272">Codice di risposta del server **NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083)</span><span class="sxs-lookup"><span data-stu-id="ea05f-272">**NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083) Server response code</span></span>
- <span data-ttu-id="ea05f-273">Codice di risposta del server **NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084)</span><span class="sxs-lookup"><span data-stu-id="ea05f-273">**NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084) Server response code</span></span>
- <span data-ttu-id="ea05f-274">Codice di risposta del server **NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085)</span><span class="sxs-lookup"><span data-stu-id="ea05f-274">**NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085) Server response code</span></span>
- <span data-ttu-id="ea05f-275">NX_PTR_ERROR (0x07) non valido per il blocco di controllo MQTT o la struttura di indirizzi del server.</span><span class="sxs-lookup"><span data-stu-id="ea05f-275">NX_PTR_ERROR (0x07) Invalid MQTT control block or sever address structure.</span></span>
- <span data-ttu-id="ea05f-276">La porta del server NX_INVALID_PORT (0x46) non può essere 0.</span><span class="sxs-lookup"><span data-stu-id="ea05f-276">NX_INVALID_PORT (0x46) Server port cannot be 0.</span></span>
- <span data-ttu-id="ea05f-277">Errore del parametro di input NXD_MQTT_INVALID_PARAMETER (0x10009)</span><span class="sxs-lookup"><span data-stu-id="ea05f-277">NXD_MQTT_INVALID_PARAMETER (0x10009) Input parameter error</span></span>
- <span data-ttu-id="ea05f-278">Il thread MQTT di NXD_MQTT_CLIENT_NOT_RUNNING (0x1000E) non è ancora stato avviato.</span><span class="sxs-lookup"><span data-stu-id="ea05f-278">NXD_MQTT_CLIENT_NOT_RUNNING (0x1000E) MQTT Thread has not started running yet.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-279">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-279">Allowed From</span></span>

<span data-ttu-id="ea05f-280">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-280">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-281">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-281">Example</span></span>

```c
/* TLS setup routine. This function is responsible for setting up TLS parameters.*/
UINT tls_setup_callback(NXD_MQTT_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certificate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_certificate,
    UINT timeout)
{
/* Note this routine is simplified to highlight the
necessary steps to setup a TLS session. Each
application may employ different procedures suitable for
its TLS settings, such as cipher suite, certificates. */

/* Create a TLS session for the MQTT connection, and pass
in various crypto methods this session can use for the
initial TLS handshake. */

/* Load appropriate certificates, or set up session key for Pre-share key operation. */

/* Start the TLS session */

/* Return NX_SUCCESS if the TLS session is established. */
    return(NX_SUCCESS);
}

NXD_ADDRESS broker_address;

/* Set up broker IP address */
broker_address.nxd_ip_version = 4;
broker_address.nxd_ip_address.v4 = MQTT_BROKER_ADDRESS;

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_secure_connect(&my_client,
    &server_address, NXD_MQTT_TLS_PORT, tls_setup_callback,
    0, /* Turn off keepalive */
    NX_TRUE, /* Clean session set */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS the MQTT Client was successfully connected to the broker via TLS. */
```

## <a name="nxd_mqtt_client_publish"></a><span data-ttu-id="ea05f-282">nxd_mqtt_client_publish</span><span class="sxs-lookup"><span data-stu-id="ea05f-282">nxd_mqtt_client_publish</span></span>

<span data-ttu-id="ea05f-283">Pubblicare un messaggio tramite Service Broker</span><span class="sxs-lookup"><span data-stu-id="ea05f-283">Publish a message through the broker</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-284">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-284">Prototype</span></span>

```c
UINT nxd_mqtt_client_publish(NXD_MQTT_CLIENT *client_ptr,
    CHAR *topic_name, UINT topic_name_length, CHAR *message, UINT
    message_length,
    UINT retain, UINT QoS, ULONG timeout);
```

### <a name="description"></a><span data-ttu-id="ea05f-285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-285">Description</span></span>

<span data-ttu-id="ea05f-286">Questo servizio pubblica un messaggio tramite Service Broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-286">This service publishes a message through the broker.</span></span> <span data-ttu-id="ea05f-287">La pubblicazione di messaggi di livello 2 QoS non è ancora supportata.</span><span class="sxs-lookup"><span data-stu-id="ea05f-287">Publishing QoS level 2 messages is not supported yet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-288">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-288">Input Parameters</span></span>

- <span data-ttu-id="ea05f-289">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-289">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-290">**topic_name** Argomento in cui pubblicare.</span><span class="sxs-lookup"><span data-stu-id="ea05f-290">**topic_name** Topic to publish to.</span></span>
- <span data-ttu-id="ea05f-291">**topic_name_length** Lunghezza dell'argomento in byte.</span><span class="sxs-lookup"><span data-stu-id="ea05f-291">**topic_name_length** Length of the topic, in bytes.</span></span>
- <span data-ttu-id="ea05f-292">**messaggio** di Puntatore al buffer dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="ea05f-292">**message** Pointer to the message buffer.</span></span>
- <span data-ttu-id="ea05f-293">**message_length** Dimensioni del messaggio, in byte</span><span class="sxs-lookup"><span data-stu-id="ea05f-293">**message_length** Size of the message, in bytes</span></span>
- <span data-ttu-id="ea05f-294">**Mantieni** Determina se il broker deve conservare il messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-294">**retain** Determines if the broker shall retain the message.</span></span>
- <span data-ttu-id="ea05f-295">**QoS** Valore QoS desiderato: 0 o 1.</span><span class="sxs-lookup"><span data-stu-id="ea05f-295">**QoS** The desired QoS value: 0 or 1.</span></span>
- <span data-ttu-id="ea05f-296">**timeout** Valore di timeout</span><span class="sxs-lookup"><span data-stu-id="ea05f-296">**timeout** Timeout value</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-297">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-297">Return Values</span></span>

- <span data-ttu-id="ea05f-298">Creazione di un client MQTT riuscito **NXD_MQTT_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="ea05f-298">**NXD_MQTT_SUCCESS** (0x00) Successful MQTT Client create</span></span>
- <span data-ttu-id="ea05f-299">Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004).</span><span class="sxs-lookup"><span data-stu-id="ea05f-299">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error.</span></span>
- <span data-ttu-id="ea05f-300">**NXD_MQTT_PACKET_POOL_FAILURE** (0X10006) non è riuscito a ottenere il pacchetto dal pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ea05f-300">**NXD_MQTT_PACKET_POOL_FAILURE** (0x10006) Failed to obtain packet from the packet pool.</span></span>
- <span data-ttu-id="ea05f-301">**NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è riuscito a comunicare con Service Broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-301">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Failed to communication with the broker.</span></span>
- <span data-ttu-id="ea05f-302">I messaggi QoS di livello 2 **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="ea05f-302">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) QoS level 2 messages are not supported.</span></span>
- <span data-ttu-id="ea05f-303">NX_PTR_ERROR (0x07) non valido: blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ea05f-303">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="ea05f-304">Errore del parametro di input NXD_MQTT_INVALID_PARAMETER (0x10009)</span><span class="sxs-lookup"><span data-stu-id="ea05f-304">NXD_MQTT_INVALID_PARAMETER (0x10009) Input parameter error</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-305">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-305">Allowed From</span></span>

<span data-ttu-id="ea05f-306">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-306">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-307">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-307">Example</span></span>

```c
CHAR *topic = "temperature";
CHAR *message = "100";

/* Publish the temperature value. */
status = nxd_mqtt_client_publish(&my_client,
    topic, STRLEN(topic),
    message, STRLEN(message),
    NX_TRUE, /* Server retains message. */);
    0, /* QOS */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS the message has been 
successfully sent to the broker. */
```

## <a name="nxd_mqtt_client_subscribe"></a><span data-ttu-id="ea05f-308">nxd_mqtt_client_subscribe</span><span class="sxs-lookup"><span data-stu-id="ea05f-308">nxd_mqtt_client_subscribe</span></span>

<span data-ttu-id="ea05f-309">Sottoscrivere un argomento</span><span class="sxs-lookup"><span data-stu-id="ea05f-309">Subscribe to a topic</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-310">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-310">Prototype</span></span>

```c
UINT nxd_mqtt_client_subscribe(NXD_MQTT_CLIENT
    *mqtt_client_ptr, CHAR *topic_name,
    UINT topic_name_length, UINT QoS);
```

### <a name="description"></a><span data-ttu-id="ea05f-311">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-311">Description</span></span>

<span data-ttu-id="ea05f-312">Questo servizio sottoscrive un argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="ea05f-312">This service subscribes to a specific topic.</span></span> <span data-ttu-id="ea05f-313">La sottoscrizione a messaggi QoS di livello 2 non è ancora supportata.</span><span class="sxs-lookup"><span data-stu-id="ea05f-313">Subscribing to QoS level 2 messages is not supported yet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-314">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-314">Input Parameters</span></span>

- <span data-ttu-id="ea05f-315">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-315">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-316">**topic_name** Argomento in cui pubblicare.</span><span class="sxs-lookup"><span data-stu-id="ea05f-316">**topic_name** Topic to publish to.</span></span>
- <span data-ttu-id="ea05f-317">**topic_name_length** Lunghezza dell'argomento in byte.</span><span class="sxs-lookup"><span data-stu-id="ea05f-317">**topic_name_length** Length of the topic, in bytes.</span></span>
- <span data-ttu-id="ea05f-318">**QoS il livello QoS desiderato:** 0 o 1.</span><span class="sxs-lookup"><span data-stu-id="ea05f-318">**QoS The desired QoS level:** 0 or 1.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-319">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-319">Return Values</span></span>

- <span data-ttu-id="ea05f-320">**NXD_MQTT_SUCCESS** (0x00) ha eseguito la sottoscrizione all'argomento.</span><span class="sxs-lookup"><span data-stu-id="ea05f-320">**NXD_MQTT_SUCCESS** (0x00) Successfully subscribed to the topic.</span></span>
- <span data-ttu-id="ea05f-321">**NXD_MQTT_NOT_CONNECTED** (0X10002) il client non è connesso al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-321">**NXD_MQTT_NOT_CONNECTED** (0x10002) The client is not connected to the broker.</span></span>
- <span data-ttu-id="ea05f-322">**NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-322">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex</span></span>
- <span data-ttu-id="ea05f-323">Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)</span><span class="sxs-lookup"><span data-stu-id="ea05f-323">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="ea05f-324">**NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è in grado di inviare messaggi al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-324">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Unable to send messages to the broker.</span></span>
- <span data-ttu-id="ea05f-325">Il livello QoS di **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) 2messages non è supportato.</span><span class="sxs-lookup"><span data-stu-id="ea05f-325">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) QoS level 2messages are not supported.</span></span>
- <span data-ttu-id="ea05f-326">NX_PTR_ERROR (0x07) non valido: blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ea05f-326">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="ea05f-327">Il topic_name NXD_MQTT_INVALID_PARAMETER (0x10009) non è impostato oppure topic_name_length è zero oppure il valore QoS è non valido.</span><span class="sxs-lookup"><span data-stu-id="ea05f-327">NXD_MQTT_INVALID_PARAMETER (0x10009) topic_name is not set, or topic_name_length is zero, or QoS is value is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-328">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-328">Allowed From</span></span>

<span data-ttu-id="ea05f-329">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-329">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-330">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-330">Example</span></span>

```c
/* Subscribe to the topic "temperature" with QoS level 0 */
CHAR *topic = "temperature";

status = nxd_mqtt_client_subscribe(&my_client, topic,
    STRLEN(topic), 0);

/* If status is NXD_MQTT_SUCCESS, the client successfully
subscribes to the topic "temperate". At this point the client
is ready for receiving messages from the broker. */
```

## <a name="nxd_mqtt_client_unsubscribe"></a><span data-ttu-id="ea05f-331">nxd_mqtt_client_unsubscribe</span><span class="sxs-lookup"><span data-stu-id="ea05f-331">nxd_mqtt_client_unsubscribe</span></span>

<span data-ttu-id="ea05f-332">Annulla sottoscrizione da un argomento</span><span class="sxs-lookup"><span data-stu-id="ea05f-332">Unsubscribe from a topic</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-333">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-333">Prototype</span></span>

```c
UINT nxd_mqtt_client_unsubscribe(NXD_MQTT_CLIENT
    *mqtt_client_pr,
    CHAR *topic_name,
    UINT topic_name_length);
```

### <a name="description"></a><span data-ttu-id="ea05f-334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-334">Description</span></span>

<span data-ttu-id="ea05f-335">Questo servizio annulla la sottoscrizione da un argomento.</span><span class="sxs-lookup"><span data-stu-id="ea05f-335">This service unsubscribes from a topic.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-336">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-336">Input Parameters</span></span>

- <span data-ttu-id="ea05f-337">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-337">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-338">**topic_name** Argomento da cui annullare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-338">**topic_name** Topic to unsubscribe from.</span></span>
- <span data-ttu-id="ea05f-339">**topic_name_length** Lunghezza dell'argomento in byte.</span><span class="sxs-lookup"><span data-stu-id="ea05f-339">**topic_name_length** Length of the topic, in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-340">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-340">Return Values</span></span>

- <span data-ttu-id="ea05f-341">**NXD_MQTT_SUCCESS** (0x00) ha annullato la sottoscrizione dall'argomento.</span><span class="sxs-lookup"><span data-stu-id="ea05f-341">**NXD_MQTT_SUCCESS** (0x00) Successfully unsubscribed from the topic.</span></span>
- <span data-ttu-id="ea05f-342">**NXD_MQTT_NOT_CONNECTED** (0X10002) il client non è connesso al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-342">**NXD_MQTT_NOT_CONNECTED** (0x10002) The client is not connected to the broker.</span></span>
- <span data-ttu-id="ea05f-343">**NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-343">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex.</span></span>
- <span data-ttu-id="ea05f-344">Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)</span><span class="sxs-lookup"><span data-stu-id="ea05f-344">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="ea05f-345">**NXD_MQTT_COMMUNICATION_FAILURE** (0X10007) non è in grado di inviare messaggi al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-345">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Unable to send messages to the broker.</span></span>
- <span data-ttu-id="ea05f-346">NX_PTR_ERROR (0x07) non valido puntatore a blocco di controllo MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-346">NX_PTR_ERROR (0x07) Invalid MQTT control block pointer</span></span>
- <span data-ttu-id="ea05f-347">Il topic_name NXD_MQTT_INVALID_PARAMETER (0x10009) non è impostato oppure topic_name_length è zero.</span><span class="sxs-lookup"><span data-stu-id="ea05f-347">NXD_MQTT_INVALID_PARAMETER (0x10009) topic_name is not set, or topic_name_length is zero.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-348">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-348">Allowed From</span></span>

<span data-ttu-id="ea05f-349">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-349">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-350">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-350">Example</span></span>

```c
/* Subscribe to the topic "temperature" with QoS level 0 */
CHAR *topic = "temperature";

status = nxd_mqtt_client_unsubscribe(&my_client, topic,
    STRLEN(topic));

/* If status is NXD_MQTT_SUCCESS, the client successfully
unsubscribes the topic "temperate". */
```

## <a name="nxd_mqtt_client_receive_notify_set"></a><span data-ttu-id="ea05f-351">nxd_mqtt_client_receive_notify_set</span><span class="sxs-lookup"><span data-stu-id="ea05f-351">nxd_mqtt_client_receive_notify_set</span></span>

<span data-ttu-id="ea05f-352">Impostare la funzione di callback di ricezione notifiche messaggio MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-352">Set MQTT message receive notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-353">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-353">Prototype</span></span>

```c
UINT nxd_mqtt_client_receive_notify_set(NXD_MQTT_CLIENT
    *client_ptr,
    VOID(*receive_notify)(NXD_MQTT_CLIENT* client_ptr,
    UINT message_count));
```

### <a name="description"></a><span data-ttu-id="ea05f-354">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-354">Description</span></span>

<span data-ttu-id="ea05f-355">Questo servizio registra una funzione di callback con il client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-355">This service registers a callback function with the MQTT client.</span></span> <span data-ttu-id="ea05f-356">Al momento della ricezione di un messaggio pubblicato dal broker, il client MQTT archivia il messaggio nella coda di ricezione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-356">Upon receiving a message published by the broker, MQTT client stores the message in the receive queue.</span></span> <span data-ttu-id="ea05f-357">Se la funzione di callback è impostata, la funzione di callback viene richiamata per notificare all'applicazione che un messaggio è pronto per essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="ea05f-357">If the callback function is set, the callback function is invoked to notify the application that a message is ready to be retrieved.</span></span> <span data-ttu-id="ea05f-358">La funzione receive Notify accetta un puntatore al blocco di controllo client di MQTT e un *message_count* indicante il numero di messaggi disponibili nella coda di ricezione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-358">The receive notify function takes a pointer to the MQTT client control block, and a *message_count* indicating the number of messages available in the receive queue.</span></span> <span data-ttu-id="ea05f-359">Si noti che il numero può variare tra la notifica di ricezione e quando l'applicazione recupera questi messaggi, perché i nuovi messaggi possono essere arrivati nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="ea05f-359">Note that the number may change between the receive notification and when the application retrieves these messages, as new messages may have arrived in the interval.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-360">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-360">Input Parameters</span></span>

- <span data-ttu-id="ea05f-361">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-361">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-362">**receive_notify** Funzione di callback fornita dall'utente da richiamare alla ricezione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-362">**receive_notify** User supplied callback function to be invoked on receiving a message.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-363">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-363">Return Values</span></span>

- <span data-ttu-id="ea05f-364">**NXD_MQTT_SUCCESS** (0x00) ha impostato correttamente la funzione receive Notify.</span><span class="sxs-lookup"><span data-stu-id="ea05f-364">**NXD_MQTT_SUCCESS** (0x00) Successfully set the receive notify function.</span></span>
- <span data-ttu-id="ea05f-365">NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido.</span><span class="sxs-lookup"><span data-stu-id="ea05f-365">NX_PTR_ERROR (0x07) Invalid MQTT control block.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-366">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-366">Allowed From</span></span>

<span data-ttu-id="ea05f-367">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-367">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-368">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-368">Example</span></span>

```c
/* Sample MQTT receive notify function. */

VOID my_notify_func(NXD_MQTT_CLIENT* client_ptr,
    UINT message_count)
{

/* On receiving a message, set an event flag to wake up the
application thread. The message will be received and
processed in the application thread. */
tx_event_flags_set(&mqtt_app_flag,
    MESSAGE_RECEIVED_EVENT, TX_OR);

/* All done. Return to the caller. */
    return;
}

/* Set the receive callback function. */
status = **nxd_mqtt_client_receive_notify_set**(&my_client,
    my_notify_func);

/* If status is NXD_MQTT_SUCCESS the notify function is properly set. */
```

## <a name="nxd_mqtt_client_message_get"></a><span data-ttu-id="ea05f-369">nxd_mqtt_client_message_get</span><span class="sxs-lookup"><span data-stu-id="ea05f-369">nxd_mqtt_client_message_get</span></span>

<span data-ttu-id="ea05f-370">Recuperare un messaggio dal broker</span><span class="sxs-lookup"><span data-stu-id="ea05f-370">Retrieve a message from the broker</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-371">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-371">Prototype</span></span>

```c
UINT nxd_mqtt_client_message_get(NXD_MQTT_CLIENT
    *client_ptr,
    UCHAR *topic_buffer, UINT topic_buffer_size,
    UINT *actual_topic_length, UCHAR *message_buffer,
    UINT message_buffer_size, UINT *actual_message_length);
```

### <a name="description"></a><span data-ttu-id="ea05f-372">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-372">Description</span></span>

<span data-ttu-id="ea05f-373">Questo servizio recupera un messaggio pubblicato dal broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-373">This service retrieves a message published by the broker.</span></span> <span data-ttu-id="ea05f-374">Tutti i messaggi in arrivo vengono archiviati nella coda di ricezione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-374">All incoming messages are stored in the receive queue.</span></span> <span data-ttu-id="ea05f-375">L'applicazione utilizza questo servizio per recuperare questi messaggi.</span><span class="sxs-lookup"><span data-stu-id="ea05f-375">The application uses this service to retrieve these messages.</span></span> <span data-ttu-id="ea05f-376">Questa chiamata non è bloccata.</span><span class="sxs-lookup"><span data-stu-id="ea05f-376">This call is non-blocking.</span></span> <span data-ttu-id="ea05f-377">Se la coda di ricezione è vuota, il servizio restituisce \***NXD_MQTT_NO_MESSAGE** _.</span><span class="sxs-lookup"><span data-stu-id="ea05f-377">If the receive queue is empty, this service returns \***NXD_MQTT_NO_MESSAGE** _.</span></span> <span data-ttu-id="ea05f-378">Un'applicazione che desidera ricevere notifiche del messaggio in arrivo può chiamare il servizio _ *_nxd_mqtt_client_receive_notify_set_*\* per registrare una funzione di callback di ricezione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-378">An application wishing to be notified of incoming message can call the service _ *_nxd_mqtt_client_receive_notify_set_*\* to register a receive callback function.</span></span>

<span data-ttu-id="ea05f-379">Il chiamante deve fornire spazio di memoria per la stringa dell'argomento e il corpo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-379">The caller needs to provide memory space for the topic string and the message body.</span></span> <span data-ttu-id="ea05f-380">Le dimensioni di questi due buffer vengono passate usando *topic_buffer_size* e *message_buffer_size*.</span><span class="sxs-lookup"><span data-stu-id="ea05f-380">The sizes of these two buffers are passed in using *topic_buffer_size* and *message_buffer_size*.</span></span> <span data-ttu-id="ea05f-381">Il numero effettivo di byte nella stringa dell'argomento e il corpo del messaggio vengono restituiti in *actual_topic_length* e *actual_message_length*.</span><span class="sxs-lookup"><span data-stu-id="ea05f-381">The actual number of bytes in the topic string and the message body are returned in *actual_topic_length* and *actual_message_length*.</span></span> <span data-ttu-id="ea05f-382">Se la lunghezza dell'argomento o la lunghezza del massaggio è maggiore dello spazio del buffer specificato, il servizio restituisce il codice di errore *NXD_MQTT_INSUFFICIENT_BUFFER_SIZE*.</span><span class="sxs-lookup"><span data-stu-id="ea05f-382">If topic length or massage length is greater than the buffer space provided, this service returns error code *NXD_MQTT_INSUFFICIENT_BUFFER_SIZE*.</span></span>

<span data-ttu-id="ea05f-383">L'applicazione deve allocare un buffer più grande e riprovare.</span><span class="sxs-lookup"><span data-stu-id="ea05f-383">The application shall allocate a bigger buffer and try again.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-384">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-384">Input Parameters</span></span>

- <span data-ttu-id="ea05f-385">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-385">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-386">**topic_buffer** Puntatore alla posizione di memoria in cui viene copiata la stringa dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="ea05f-386">**topic_buffer** Pointer to the memory location where the topic string is copied into.</span></span>
- <span data-ttu-id="ea05f-387">**topic_buffer_size** Dimensioni del buffer dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="ea05f-387">**topic_buffer_size** Size of the topic buffer.</span></span>
- <span data-ttu-id="ea05f-388">**actual_topic_length** Puntatore alla posizione di memoria in cui viene restituita la lunghezza effettiva dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="ea05f-388">**actual_topic_length** Pointer to the memory location where the actual topic length is returned.</span></span>
- <span data-ttu-id="ea05f-389">**message_buffer** Puntatore alla posizione di memoria in cui viene copiata la stringa del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-389">**message_buffer** Pointer to the memory location where the message string is copied into.</span></span>
- <span data-ttu-id="ea05f-390">**message_buffer_size** Dimensioni del buffer dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="ea05f-390">**message_buffer_size** Size of the message buffer.</span></span>
- <span data-ttu-id="ea05f-391">**actual_message_length** Puntatore alla posizione di memoria in cui viene restituita la lunghezza del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-391">**actual_message_length** Pointer to the memory location where the message length is returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-392">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-392">Return Values</span></span>

- <span data-ttu-id="ea05f-393">**NXD_MQTT_SUCCESS** (0x00) ha recuperato correttamente il messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-393">**NXD_MQTT_SUCCESS** (0x00) Successfully retrieved message.</span></span>
- <span data-ttu-id="ea05f-394">Errore di logica interna **NXD_MQTT_INTERNAL_ERROR** (0x10004)</span><span class="sxs-lookup"><span data-stu-id="ea05f-394">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="ea05f-395">**NXD_MQTT_NO_MESSAGE** (0X1000A) la coda di ricezione è vuota.</span><span class="sxs-lookup"><span data-stu-id="ea05f-395">**NXD_MQTT_NO_MESSAGE** (0x1000A) The receive queue is empty.</span></span>
- <span data-ttu-id="ea05f-396">Il buffer dell'argomento di **NXD_MQTT_INSUFFICIENT_BUFFER_SIZE** (0x1000D) o il buffer dei messaggi è troppo piccolo per l'argomento o per il messaggio.</span><span class="sxs-lookup"><span data-stu-id="ea05f-396">**NXD_MQTT_INSUFFICIENT_BUFFER_SIZE** (0x1000D) Topic buffer or message buffer is too small for the topic or the message.</span></span>
- <span data-ttu-id="ea05f-397">NX_PTR_ERROR (0x07) non valido: blocco di controllo MQTT, ip_ptr o puntatore al pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ea05f-397">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="ea05f-398">NXD_MQTT_INVALID_PARAMETER (0x10009) message_buffer o topic_buffer puntatore è NULL</span><span class="sxs-lookup"><span data-stu-id="ea05f-398">NXD_MQTT_INVALID_PARAMETER (0x10009) message_buffer or topic_buffer pointer is NULL</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-399">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-399">Allowed From</span></span>

<span data-ttu-id="ea05f-400">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-400">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-401">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-401">Example</span></span>

```c
UCHAR topic[MAX_TOPIC_SIZE];
UCHAR message[MAX_TOPIC_SIZE];
UINT topic_length;
UINT message_length;

/* Retrieve a message from MQTT client receive queue. */
status = nxd_mqtt_client_message_get(&my_client, topic,
    sizeof(topic), &topic_length, message, sizeof(message),
    &message_length);

/* Check the return value. */
if(status == NXD_MQTT_SUCCESS)
{
/* A message is received. All done. */
}
else if (status == NXD_MQTT_NO_MESSAGE)
{
/* No more messages in the receive queue. All done. */
}
else
{
/* Receive error. */
}
```

## <a name="nxd_mqtt_client_disconnect_notify_set"></a><span data-ttu-id="ea05f-402">nxd_mqtt_client_disconnect_notify_set</span><span class="sxs-lookup"><span data-stu-id="ea05f-402">nxd_mqtt_client_disconnect_notify_set</span></span>

<span data-ttu-id="ea05f-403">Imposta la funzione di callback di disconnessione del messaggio MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-403">Set MQTT message disconnect notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-404">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-404">Prototype</span></span>

```c
UINT nxd_mqtt_client_disconnect_notify_set(
    NXD_MQTT_CLIENT *client_ptr,
    VOID(*disconnect_notify)(NXD_MQTT_CLIENT* client_ptr));
```

### <a name="description"></a><span data-ttu-id="ea05f-405">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-405">Description</span></span>

<span data-ttu-id="ea05f-406">Questo servizio registra una funzione di callback con il client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-406">This service registers a callback function with the MQTT client.</span></span> <span data-ttu-id="ea05f-407">Quando MQTT rileva che la connessione al Broker viene persa, chiama questa funzione Notify per avvisare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-407">When MQTT detects the connection to the broker is lost, it calls this notify function to alert the application.</span></span> <span data-ttu-id="ea05f-408">Pertanto, l'applicazione può utilizzare questa funzione di callback per rilevare una connessione persa e per poter ristabilire la connessione al broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-408">Therefore, the application can use this callback function to detect a lost connection, and to be able to re-establish connection to the broker.</span></span>

```c
VOID callback_func(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="input-parameters"></a><span data-ttu-id="ea05f-409">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-409">Input Parameters</span></span>

- <span data-ttu-id="ea05f-410">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-410">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="ea05f-411">**disconnect_notify** Funzione di callback fornita dall'utente da richiamare quando MQTT rileva che la connessione al Broker viene persa.</span><span class="sxs-lookup"><span data-stu-id="ea05f-411">**disconnect_notify** User supplied callback function to be invoked when MQTT detects the connection to the broker is lost.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-412">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-412">Return Values</span></span>

- <span data-ttu-id="ea05f-413">**NXD_MQTT_SUCCESS** (0x00) ha impostato correttamente la funzione Disconnetti notifica.</span><span class="sxs-lookup"><span data-stu-id="ea05f-413">**NXD_MQTT_SUCCESS** (0x00) Successfully set the disconnect notify function.</span></span>
- <span data-ttu-id="ea05f-414">NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido.</span><span class="sxs-lookup"><span data-stu-id="ea05f-414">NX_PTR_ERROR (0x07) Invalid MQTT control block.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-415">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-415">Allowed From</span></span>

<span data-ttu-id="ea05f-416">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-416">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-417">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-417">Example</span></span>

```c
VOID disconnect_notify(NXD_MQTT_CLIENT *client_ptr)
{
/* MQTT client is disconnected from the broker. Notify the application so it can re-connect to the broker. */
}

status = nxd_mqtt_client_disconnect_notify_set(client_ptr,
    disconnect_notify);
```

## <a name="nxd_mqtt_client_disconnect"></a><span data-ttu-id="ea05f-418">nxd_mqtt_client_disconnect</span><span class="sxs-lookup"><span data-stu-id="ea05f-418">nxd_mqtt_client_disconnect</span></span>

<span data-ttu-id="ea05f-419">Disconnettere il client di MQTT dal broker</span><span class="sxs-lookup"><span data-stu-id="ea05f-419">Disconnect MQTT client from the broker</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-420">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-420">Prototype</span></span>

```c
UINT nxd_mqtt_client_disconnect(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="ea05f-421">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-421">Description</span></span>

<span data-ttu-id="ea05f-422">Questo servizio disconnette il client dal broker.</span><span class="sxs-lookup"><span data-stu-id="ea05f-422">This service disconnects the client from the broker.</span></span> <span data-ttu-id="ea05f-423">Si noti che i messaggi nella coda di ricezione vengono rilasciati.</span><span class="sxs-lookup"><span data-stu-id="ea05f-423">Note that messages on the receive queue are released.</span></span> <span data-ttu-id="ea05f-424">I messaggi con QoS 1 nella coda di trasmissione non vengono rilasciati.</span><span class="sxs-lookup"><span data-stu-id="ea05f-424">Messages with QoS 1 in the transmit queue are not released.</span></span> <span data-ttu-id="ea05f-425">Quando il client si riconnette al server, i messaggi QoS 1 possono essere elaborati, a meno che il client non si riconnetta al server con *clean_session* flag impostato su ***NX_TRUE***.</span><span class="sxs-lookup"><span data-stu-id="ea05f-425">After the client reconnects to the server, QoS 1 messages can be processed, unless the client reconnects to the server with *clean_session* flag set to ***NX_TRUE***.</span></span>

<span data-ttu-id="ea05f-426">Se la connessione è stata effettuata con la protezione TLS, questo servizio chiuderà la sessione TLS prima di disconnettere la connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="ea05f-426">If the connection was made with TLS security protection, this service will close the TLS session before disconnecting the TCP connection.</span></span>

<span data-ttu-id="ea05f-427">La chiamata di disconnessione socket TCP effettiva ha un'opzione wait definita da NXD_MQTT_SOCKET_TIMEOUT (cicli timer).</span><span class="sxs-lookup"><span data-stu-id="ea05f-427">The actual TCP socket disconnect call has a wait option defined by NXD_MQTT_SOCKET_TIMEOUT (timer ticks).</span></span> <span data-ttu-id="ea05f-428">Il valore predefinito è NX_WAIT_FOREVER.</span><span class="sxs-lookup"><span data-stu-id="ea05f-428">The default value is NX_WAIT_FOREVER.</span></span> <span data-ttu-id="ea05f-429">Per evitare una sospensione illimitata nel caso in cui la connessione di rete venga persa o il server non risponda, impostare questa opzione su un valore finito.</span><span class="sxs-lookup"><span data-stu-id="ea05f-429">To avoid indefinite suspension in the event that the network connection is lost or the server is not responding, set this option to a finite value.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-430">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-430">Input Parameters</span></span>

- <span data-ttu-id="ea05f-431">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-431">**client_ptr** Pointer to MQTT Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-432">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-432">Return Values</span></span>

- <span data-ttu-id="ea05f-433">La disconnessione di **NXD_MQTT_SUCCESS** (0x00) da Service Broker è stata completata</span><span class="sxs-lookup"><span data-stu-id="ea05f-433">**NXD_MQTT_SUCCESS** (0x00) Successfully disconnected from broker</span></span>
- <span data-ttu-id="ea05f-434">**NXD_MQTT_MUTEX_FAILURE** (0X10003) non è riuscito a ottenere il mutex MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-434">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex.</span></span>
- <span data-ttu-id="ea05f-435">NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido</span><span class="sxs-lookup"><span data-stu-id="ea05f-435">NX_PTR_ERROR (0x07) Invalid MQTT control block</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-436">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-436">Allowed From</span></span>

<span data-ttu-id="ea05f-437">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-437">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-438">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-438">Example</span></span>

```c
/* Disconnect from the broker. */
status = nxd_mqtt_client_disconnect(&my_client);

/* If status is NXD_MQTT_SUCCESS the client is successfully
disconnected from the broker. */
```

## <a name="nxd_mqtt_client_delete"></a><span data-ttu-id="ea05f-439">nxd_mqtt_client_delete</span><span class="sxs-lookup"><span data-stu-id="ea05f-439">nxd_mqtt_client_delete</span></span>

<span data-ttu-id="ea05f-440">Eliminare l'istanza del client MQTT</span><span class="sxs-lookup"><span data-stu-id="ea05f-440">Delete the MQTT client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="ea05f-441">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ea05f-441">Prototype</span></span>

```c
UINT nxd_mqtt_client_delete(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="ea05f-442">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ea05f-442">Description</span></span>

<span data-ttu-id="ea05f-443">Questo servizio Elimina l'istanza del client MQTT e rilascia le risorse interne.</span><span class="sxs-lookup"><span data-stu-id="ea05f-443">This service deletes the MQTT client instance and releases internal resources.</span></span> <span data-ttu-id="ea05f-444">Questo servizio disconnette automaticamente il client dal broker se è ancora connesso.</span><span class="sxs-lookup"><span data-stu-id="ea05f-444">This service automatically disconnects the client from the broker if it is still connected.</span></span> <span data-ttu-id="ea05f-445">I messaggi non ancora trasmessi o non riconosciuti vengono rilasciati.</span><span class="sxs-lookup"><span data-stu-id="ea05f-445">Messages not yet transmitted or not been acknowledged are released.</span></span> <span data-ttu-id="ea05f-446">Vengono rilasciati anche i messaggi ricevuti ma non recuperati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea05f-446">Messages received but not retrieved by the application are also released.</span></span>

<span data-ttu-id="ea05f-447">Se la connessione è stata effettuata con la protezione TLS, questo servizio chiude la sessione TLS prima di disconnettere la connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="ea05f-447">If the connection was made with TLS security protection, this service closes the TLS session before disconnecting the TCP connection.</span></span>

<span data-ttu-id="ea05f-448">Dopo che il client è stato eliminato, un'applicazione che vuole usare il servizio MQTT deve creare una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="ea05f-448">After the client is deleted, an application wishing to use MQTT service needs to create a new instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ea05f-449">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ea05f-449">Input Parameters</span></span>

- <span data-ttu-id="ea05f-450">**client_ptr** Puntatore al blocco di controllo client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-450">**client_ptr** Pointer to MQTT Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="ea05f-451">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ea05f-451">Return Values</span></span>

- <span data-ttu-id="ea05f-452">**NXD_MQTT_SUCCESS** (0x00) ha eliminato correttamente il client MQTT.</span><span class="sxs-lookup"><span data-stu-id="ea05f-452">**NXD_MQTT_SUCCESS** (0x00) Successfully deleted MQTT client.</span></span>
- <span data-ttu-id="ea05f-453">NX_PTR_ERROR (0x07) un blocco di controllo MQTT non valido</span><span class="sxs-lookup"><span data-stu-id="ea05f-453">NX_PTR_ERROR (0x07) Invalid MQTT control block</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ea05f-454">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ea05f-454">Allowed From</span></span>

<span data-ttu-id="ea05f-455">Thread</span><span class="sxs-lookup"><span data-stu-id="ea05f-455">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ea05f-456">Esempio</span><span class="sxs-lookup"><span data-stu-id="ea05f-456">Example</span></span>

```c
/* Delete the MQTT client instance. */
status = nxd_mqtt_client_delete(&my_client);

/* If status is NXD_MQTT_SUCCESS the client is successfully
deleted from the system. */
```
