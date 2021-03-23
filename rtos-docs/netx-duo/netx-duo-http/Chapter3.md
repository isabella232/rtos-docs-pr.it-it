---
title: Capitolo 3-Descrizione dei servizi HTTP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi HTTP RTO NetX duo di Azure (elencati di seguito) in ordine alfabetico, ad eccezione dell'equivalente ' NetX ' (solo IPv4) dello stesso servizio.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 703071cd5a1d0677a3e995fccfe35d8b1dbbd9f3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821872"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-http-services"></a><span data-ttu-id="6cf9c-103">Capitolo 3-Descrizione dei servizi HTTP di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-103">Chapter 3 - Description of Azure RTOS NetX Duo HTTP Services</span></span>

<span data-ttu-id="6cf9c-104">Questo capitolo contiene una descrizione di tutti i servizi HTTP RTO NetX duo di Azure (elencati di seguito) in ordine alfabetico, ad eccezione dell'equivalente ' NetX ' (solo IPv4) dello stesso servizio.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-104">This chapter contains a description of all Azure RTOS NetX Duo HTTP services (listed below) in alphabetical order except for the ‘NetX’ (IPv4 only) equivalent of the same service are paired together).</span></span>

<span data-ttu-id="6cf9c-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in GRASSetto non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-105">In the “Return Values” section in the following API descriptions, values in BOLD are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

<span data-ttu-id="6cf9c-106">**Servizi client HTTP:**</span><span class="sxs-lookup"><span data-stu-id="6cf9c-106">**HTTP Client services:**</span></span>

- <span data-ttu-id="6cf9c-107">**nx_http_client_create** *creare un'istanza del client http*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-107">**nx_http_client_create** *Create an HTTP Client Instance*</span></span>
- <span data-ttu-id="6cf9c-108">**nx_http_client_delete** *eliminare un'istanza client http*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-108">**nx_http_client_delete** *Delete an HTTP Client instance*</span></span>
- <span data-ttu-id="6cf9c-109">**nx_http_client_get_start** *avviare una richiesta HTTP Get (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-109">**nx_http_client_get_start** *Start an HTTP GET request (IPv4 only)*</span></span>
- <span data-ttu-id="6cf9c-110">**nx_http_client_get_start_extended** *avviare una richiesta HTTP Get (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-110">**nx_http_client_get_start_extended** *Start an HTTP GET request (IPv4 only)*</span></span>
- <span data-ttu-id="6cf9c-111">**nxd_http_client_get_start** *avviare una richiesta HTTP Get (IPv4 o IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-111">**nxd_http_client_get_start** *Start an HTTP GET request (IPv4 or IPv6)*</span></span>
- <span data-ttu-id="6cf9c-112">**nxd_http_client_get_start_extended** *avviare una richiesta HTTP Get (IPv4 o IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-112">**nxd_http_client_get_start_extended** *Start an HTTP GET request (IPv4 or IPv6)*</span></span>
- <span data-ttu-id="6cf9c-113">**nx_http_client_get_packet** *ottenere un pacchetto di dati di risorse successivo*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-113">**nx_http_client_get_packet** *Get next resource data packet*</span></span>
- <span data-ttu-id="6cf9c-114">**nx_http_client_put_start** *avviare una richiesta HTTP PUT (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-114">**nx_http_client_put_start** *Start an HTTP PUT request (IPv4 only)*</span></span>
- <span data-ttu-id="6cf9c-115">**nx_http_client_put_start_extended** *avviare una richiesta HTTP PUT (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-115">**nx_http_client_put_start_extended** *Start an HTTP PUT request (IPv4 only)*</span></span>
- <span data-ttu-id="6cf9c-116">**nxd_http_client_put_start** *avviare una richiesta HTTP PUT (IPv4 o IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-116">**nxd_http_client_put_start** *Start an HTTP PUT request (IPv4 or IPv6)*</span></span>
- <span data-ttu-id="6cf9c-117">**nxd_http_client_put_start_extended** *avviare una richiesta HTTP PUT (IPv4 o IPv6)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-117">**nxd_http_client_put_start_extended** *Start an HTTP PUT request (IPv4 or IPv6)*</span></span>
- <span data-ttu-id="6cf9c-118">**nx_http_client_put_packet** *inviare il pacchetto di dati di risorse successivo*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-118">**nx_http_client_put_packet** *Send next resource data packet*</span></span>
- <span data-ttu-id="6cf9c-119">**nx_http_client_set_connect_port** *modificare la porta per la connessione al server http*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-119">**nx_http_client_set_connect_port** *Change the port to connect to the HTTP Server*</span></span>

<span data-ttu-id="6cf9c-120">**Servizi server HTTP:**</span><span class="sxs-lookup"><span data-stu-id="6cf9c-120">**HTTP server services:**</span></span>

- <span data-ttu-id="6cf9c-121">**nx_http_server_cache_info_callback_set** *impostare il callback per recuperare l'età e la data dell'Ultima modifica dell'URL specificato*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-121">**nx_http_server_cache_info_callback_set** *Set callback to retrieve age and last modified date of specified URL*</span></span>
- <span data-ttu-id="6cf9c-122">**nx_http_server_callback_data_send** *inviare dati http da una funzione di callback*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-122">**nx_http_server_callback_data_send** *Send HTTP data from callback function*</span></span>
- <span data-ttu-id="6cf9c-123">**nx_http_server_callback_generate_response_header** *creare l'intestazione della risposta nelle funzioni di callback*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-123">**nx_http_server_callback_generate_response_header** *Create response header in callback functions*</span></span>
- <span data-ttu-id="6cf9c-124">**nx_http_server_callback_generate_response_header_extended** *creare l'intestazione della risposta nelle funzioni di callback*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-124">**nx_http_server_callback_generate_response_header_extended** *Create response header in callback functions*</span></span>
- <span data-ttu-id="6cf9c-125">**nx_http_server_callback_packet_send** *inviare un pacchetto http da un callback http*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-125">**nx_http_server_callback_packet_send** *Send an HTTP packet from an HTTP callback*</span></span>
- <span data-ttu-id="6cf9c-126">**nx_http_server_callback_response_send** *inviare risposta dalla funzione di callback*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-126">**nx_http_server_callback_response_send** *Send response from callback function*</span></span>
- <span data-ttu-id="6cf9c-127">**nx_http_server_callback_response_send_extended** *inviare risposta dalla funzione di callback*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-127">**nx_http_server_callback_response_send_extended** *Send response from callback function*</span></span>
- <span data-ttu-id="6cf9c-128">**nx_http_server_content_get** *ottenere contenuto dalla richiesta*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-128">**nx_http_server_content_get** *Get content from the request*</span></span>
- <span data-ttu-id="6cf9c-129">**nx_http_server_content_get_extended** *ottenere contenuto dalla richiesta; supporta le richieste vuote (lunghezza del contenuto pari a zero)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-129">**nx_http_server_content_get_extended** *Get content from the request; supports empty (zero Content Length) requests*</span></span>
- <span data-ttu-id="6cf9c-130">**nx_http_server_content_length_get** *ottenere la lunghezza del contenuto nella richiesta*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-130">**nx_http_server_content_length_get** *Get length of content in the request*</span></span>
- <span data-ttu-id="6cf9c-131">**nx_http_server_content_length_get_extended** *ottenere la lunghezza del contenuto nella richiesta; supporta le richieste vuote (lunghezza del contenuto pari a zero)*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-131">**nx_http_server_content_length_get_extended** *Get length of content in the request; supports empty (zero Content Length) requests*</span></span>
- <span data-ttu-id="6cf9c-132">**nx_http_server_create** *creare un'istanza del server http*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-132">**nx_http_server_create** *Create an HTTP Server instance*</span></span>
- <span data-ttu-id="6cf9c-133">**nx_http_server_delete** \* eliminare un'istanza del server http \*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-133">**nx_http_server_delete** \* Delete an HTTP Server instance\*</span></span>
- <span data-ttu-id="6cf9c-134">**nx_http_server_get_entity_content** *la dimensione e la posizione del contenuto dell'entità nell'URL*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-134">**nx_http_server_get_entity_content** *Return size and location of entity content in URL*</span></span>
- <span data-ttu-id="6cf9c-135">**nx_http_server_get_entity_header** l' *intestazione dell'entità Extract URL nel buffer specificato*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-135">**nx_http_server_get_entity_header** *Extract URL entity header into specified buffer*</span></span>
- <span data-ttu-id="6cf9c-136">**nx_http_server_gmt_callback_set** *impostare il callback per recuperare la data e l'ora GMT*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-136">**nx_http_server_gmt_callback_set** *Set callback to retrieve GMT date and time*</span></span>
- <span data-ttu-id="6cf9c-137">**nx_http_server_invalid_userpassword_notify_set** *impostare il callback quando in una richiesta client non è stato ricevuto un nome utente e una password non validi*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-137">**nx_http_server_invalid_userpassword_notify_set** *Set callback for when invalid username and password is received in a Client request*</span></span>
- <span data-ttu-id="6cf9c-138">**nx_http_server_mime_maps_additional_set** *definire mappe MIME aggiuntive per HTML*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-138">**nx_http_server_mime_maps_additional_set** *Define additional mime maps for HTML*</span></span>
- <span data-ttu-id="6cf9c-139">**nx_http_server_packet_content_find** *estrarre la lunghezza del contenuto nell'intestazione HTTP e impostare il puntatore all'inizio dei dati del contenuto*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-139">**nx_http_server_packet_content_find** *Extract content length in HTTP header and set pointer to start of content data*</span></span>
- <span data-ttu-id="6cf9c-140">**nx_http_server_packet_get** *ricevere direttamente il pacchetto client*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-140">**nx_http_server_packet_get** *Receive client packet directly*</span></span>
- <span data-ttu-id="6cf9c-141">**nx_http_server_param_get** *ottenere il parametro dalla richiesta*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-141">**nx_http_server_param_get** *Get parameter from the request*</span></span>
- <span data-ttu-id="6cf9c-142">**nx_http_server_query_get** *ottenere una query dalla richiesta*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-142">**nx_http_server_query_get** *Get query from the request*</span></span>
- <span data-ttu-id="6cf9c-143">**nx_http_server_start** *avviare il server http*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-143">**nx_http_server_start** *Start the HTTP Server*</span></span>
- <span data-ttu-id="6cf9c-144">**nx_http_server_stop** *arrestare il server http*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-144">**nx_http_server_stop** *Stop the HTTP Server*</span></span>
- <span data-ttu-id="6cf9c-145">**nx_http_server_type_get (obsoleto)** *estrarre il tipo http, ad esempio text/plain dall'intestazione*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-145">**nx_http_server_type_get (deprecated)** *Extract HTTP type e.g. text/plain from header*</span></span>
- <span data-ttu-id="6cf9c-146">**nx_http_server_type_get_extended** *estrarre il tipo http, ad esempio text/plain dall'intestazione*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-146">**nx_http_server_type_get_extended** *Extract HTTP type e.g. text/plain from header*</span></span>
- <span data-ttu-id="6cf9c-147">**nx_http_server_digest_authenticate_notify_set** *impostare la funzione di callback autenticazione digest*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-147">**nx_http_server_digest_authenticate_notify_set** *Set digest authenticate callback function*</span></span>
- <span data-ttu-id="6cf9c-148">**nx_http_server_authentication_check_set** *impostare la funzione di callback per il controllo dell'autenticazione*</span><span class="sxs-lookup"><span data-stu-id="6cf9c-148">**nx_http_server_authentication_check_set** *Set authentication checking callback function*</span></span>

## <a name="nx_http_client_create"></a><span data-ttu-id="6cf9c-149">nx_http_client_create</span><span class="sxs-lookup"><span data-stu-id="6cf9c-149">nx_http_client_create</span></span>

<span data-ttu-id="6cf9c-150">Creare un'istanza del client PPPoE</span><span class="sxs-lookup"><span data-stu-id="6cf9c-150">Create a PPPoE Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-151">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-151">Prototype</span></span>

```c
UINT nx_http_client_create(NX_HTTP_CLIENT *client_ptr,
            CHAR *client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr,
            ULONG window_size);
```

### <a name="description"></a><span data-ttu-id="6cf9c-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-152">Description</span></span>

<span data-ttu-id="6cf9c-153">Questo servizio crea un'istanza del client HTTP nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-153">This service creates an HTTP Client instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-154">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-154">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-155">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-155">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-156">**client_name** Nome dell'istanza del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-156">**client_name** Name of HTTP Client instance.</span></span>
 - <span data-ttu-id="6cf9c-157">**ip_ptr** Puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-157">**ip_ptr** Pointer to IP instance.</span></span>
 - <span data-ttu-id="6cf9c-158">**pool_ptr** Puntatore al pool di pacchetti predefinito.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-158">**pool_ptr** Pointer to default packet pool.</span></span> <span data-ttu-id="6cf9c-159">Si noti che i pacchetti in questo pool devono avere un payload sufficientemente grande per gestire l'intestazione della risposta completa.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-159">Note that the packets in this pool must have a payload large enough to handle the complete response header.</span></span> <span data-ttu-id="6cf9c-160">Questa impostazione è definita da NX_HTTP_CLIENT_MIN_PACKET_SIZE in *nx_http. h*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-160">This is defined by NX_HTTP_CLIENT_MIN_PACKET_SIZE in *nx_http.h*.</span></span>
 - <span data-ttu-id="6cf9c-161">**window_size** Dimensioni della finestra di ricezione del socket TCP del client.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-161">**window_size** Size of the Client’s TCP socket receive window.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-162">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-162">Return Values</span></span>

 - <span data-ttu-id="6cf9c-163">Creazione client HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-163">**NX_SUCCESS** (0x00) Successful HTTP Client create</span></span>
 - <span data-ttu-id="6cf9c-164">NX_PTR_ERROR (0x07) puntatore HTTP, ip_ptr o pool di pacchetti non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-164">NX_PTR_ERROR (0x07) Invalid HTTP, ip_ptr, or packet pool pointer</span></span>
 - <span data-ttu-id="6cf9c-165">Dimensioni del payload NX_HTTP_POOL_ERROR (0xE9) non valide nel pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-165">NX_HTTP_POOL_ERROR (0xE9) Invalid payload size in packet pool</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-166">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-166">Allowed From</span></span>

<span data-ttu-id="6cf9c-167">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-167">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-168">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-168">Example</span></span>

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status =  nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);

/* If status is NX_SUCCESS an HTTP Client instance was successfully created. */
```

## <a name="nx_http_client_delete"></a><span data-ttu-id="6cf9c-169">nx_http_client_delete</span><span class="sxs-lookup"><span data-stu-id="6cf9c-169">nx_http_client_delete</span></span>

<span data-ttu-id="6cf9c-170">Eliminare un'istanza client HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-170">Delete an HTTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-171">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-171">Prototype</span></span>

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="6cf9c-172">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-172">Description</span></span>

<span data-ttu-id="6cf9c-173">Questo servizio Elimina un'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-173">This service deletes a previously created HTTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-174">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-174">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-175">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-175">**client_ptr** Pointer to HTTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-176">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-176">Return Values</span></span>

 - <span data-ttu-id="6cf9c-177">Eliminazione client HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-177">**NX_SUCCESS** (0x00) Successful HTTP Client delete</span></span>
 - <span data-ttu-id="6cf9c-178">NX_PTR_ERROR (0x07) puntatore HTTP non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-178">NX_PTR_ERROR (0x07) Invalid HTTP pointer</span></span>
 - <span data-ttu-id="6cf9c-179">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-179">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-180">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-180">Allowed From</span></span>

<span data-ttu-id="6cf9c-181">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-181">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-182">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-182">Example</span></span>

```c
/* Delete the HTTP Client instance “my_client.”  */
status =  nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully deleted. */
```

## <a name="nx_http_client_get_start"></a><span data-ttu-id="6cf9c-183">nx_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="6cf9c-183">nx_http_client_get_start</span></span>

<span data-ttu-id="6cf9c-184">Avvia una richiesta HTTP GET su IPv4</span><span class="sxs-lookup"><span data-stu-id="6cf9c-184">Start an HTTP GET request over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-185">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-185">Prototype</span></span>

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, CHAR *input_ptr,
            UINT input_size, CHAR *username, CHAR *password,
            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-186">Description</span></span>

<span data-ttu-id="6cf9c-187">Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-187">This service attempts to create and send a GET request with the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="6cf9c-188">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-188">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-189">La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il rinvio delle richieste Get.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-189">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="6cf9c-190">Questo servizio funziona solo sulla rete IPv4.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-190">This service works only over IPv4 network.</span></span> <span data-ttu-id="6cf9c-191">Per le applicazioni che devono connettersi alla rete IPv6, è necessario usare *nxd_http_client_get_start_extended ()* .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-191">For applications that need to connect to IPv6 network, *nxd_http_client_get_start_extended()* should be used.</span></span>

<span data-ttu-id="6cf9c-192">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-192">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-193">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_client_get_start_extended ()* o *nxd_http_client_get_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-193">Developers are encouraged to migrate to *nx_http_client_get_start_extended()* or *nxd_http_client_get_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-194">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-194">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-195">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-195">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-196">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-196">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-197">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-197">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-198">**input_ptr** Puntatore a dati aggiuntivi per la richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-198">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="6cf9c-199">Questo indirizzo è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-199">This is optional.</span></span> <span data-ttu-id="6cf9c-200">Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-200">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
 - <span data-ttu-id="6cf9c-201">**input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-201">**input_size** Number of bytes in optional additional input pointed to by ```input_ptr```.</span></span>
 - <span data-ttu-id="6cf9c-202">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-202">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-203">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-203">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-204">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-204">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="6cf9c-205">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-205">The wait options are defined as follows:</span></span>

    - <span data-ttu-id="6cf9c-206">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-206">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-207">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-207">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-208">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-208">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-209">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-209">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-210">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-210">Return Values</span></span>

 - <span data-ttu-id="6cf9c-211">Il client HTTP è stato inviato **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-211">**NX_SUCCESS** (0x00) Successfully sent HTTP Client.</span></span> <span data-ttu-id="6cf9c-212">OTTENERE il messaggio di avvio.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-212">GET start message.</span></span>
 - <span data-ttu-id="6cf9c-213">Errore del client HTTP interno **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-213">**NX_HTTP_ERROR** (0xE0) Internal HTTP Client error</span></span>
 - <span data-ttu-id="6cf9c-214">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-214">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-215">**NX_HTTP_FAILED** (0xe2) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-215">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-216">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-216">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or password.</span></span>
 - <span data-ttu-id="6cf9c-217">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-217">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-218">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-218">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-219">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-219">Allowed From</span></span>

<span data-ttu-id="6cf9c-220">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-220">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-221">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-221">Example</span></span>

```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                           NX_NULL, 0, “myname”, “mypassword”, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */


#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                            POST_MESSAGE, sizeof(POST_MESSAGE),
                            “myname”, “mypassword”, 1000);


/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST request
   for TEST.HTM and successfully sent. */
```

## <a name="nx_http_client_get_start_extended"></a><span data-ttu-id="6cf9c-222">nx_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-222">nx_http_client_get_start_extended</span></span>

<span data-ttu-id="6cf9c-223">Avvia una richiesta HTTP GET su IPv4</span><span class="sxs-lookup"><span data-stu-id="6cf9c-223">Start an HTTP GET request over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-224">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-224">Prototype</span></span>

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, UINT resource_length,
            CHAR *input_ptr, UINT input_size, CHAR *username,
            UINT username_length, CHAR *password, UINT password_length,
            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-225">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-225">Description</span></span>

<span data-ttu-id="6cf9c-226">Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-226">This service attempts to create and send a GET request with the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="6cf9c-227">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-227">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-228">La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il rinvio delle richieste Get.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-228">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="6cf9c-229">Questo servizio funziona solo sulla rete IPv4.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-229">This service works only over IPv4 network.</span></span> <span data-ttu-id="6cf9c-230">Per le applicazioni che devono connettersi alla rete IPv6, è necessario usare *nxd_http_client_get_start_extended ()* .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-230">For applications that need to connect to IPv6 network, *nxd_http_client_get_start_extended()* should be used.</span></span>

<span data-ttu-id="6cf9c-231">Questo servizio sostituisce *nx_http_client_get_start ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-231">This service replaces *nx_http_client_get_start()*.</span></span> <span data-ttu-id="6cf9c-232">È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-232">It requires caller to specify the length of the resource, username and password.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-233">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-233">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-234">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-234">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-235">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-235">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-236">**puntatore di risorsa** alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-236">**resource Pointer** to URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-237">**resource_length** Lunghezza della stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-237">**resource_length** Length of URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-238">**input_ptr** Puntatore a dati aggiuntivi per la richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-238">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="6cf9c-239">Questo indirizzo è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-239">This is optional.</span></span> <span data-ttu-id="6cf9c-240">Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-240">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
 - <span data-ttu-id="6cf9c-241">**input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-241">**input_size** Number of bytes in optional additional input pointed to by ```input_ptr```.</span></span>
 - <span data-ttu-id="6cf9c-242">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-242">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-243">**username_length** Lunghezza del nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-243">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-244">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-244">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-245">**password_length** Lunghezza della password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-245">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-246">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-246">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="6cf9c-247">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-247">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-248">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-248">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-249">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-249">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-250">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-250">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-251">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-251">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-252">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-252">Return Values</span></span>

 - <span data-ttu-id="6cf9c-253">Il client HTTP è stato inviato **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-253">**NX_SUCCESS** (0x00) Successfully sent HTTP Client.</span></span> <span data-ttu-id="6cf9c-254">OTTENERE il messaggio di avvio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-254">GET start message</span></span>
 - <span data-ttu-id="6cf9c-255">Errore del client HTTP interno **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-255">**NX_HTTP_ERROR** (0xE0) Internal HTTP Client error</span></span>
 - <span data-ttu-id="6cf9c-256">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-256">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-257">**NX_HTTP_FAILED** (0xe2) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-257">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-258">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-258">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or password.</span></span>
 - <span data-ttu-id="6cf9c-259">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-259">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-260">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-260">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-261">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-261">Allowed From</span></span>

<span data-ttu-id="6cf9c-262">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-262">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-263">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-263">Example</span></span>

```c
/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */


#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                     9, POST_MESSAGE, sizeof(POST_MESSAGE),
                                     “myname”, 6, “mypassword”, 10, 1000);


/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST request
   for TEST.HTM and successfully sent. */
```

## <a name="nxd_http_client_get_start"></a><span data-ttu-id="6cf9c-264">nxd_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="6cf9c-264">nxd_http_client_get_start</span></span>

<span data-ttu-id="6cf9c-265">Inviare una richiesta HTTP GET (IPv4 o IPv6)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-265">Send an HTTP GET request (IPv4 or IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-266">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-266">Prototype</span></span>

```c
UINT nxd_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
                NXD_ADDRESS *server_ip, CHAR *resource,
                CHAR *input_ptr, UINT input_size, CHAR *username, CHAR *password, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-267">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-267">Description</span></span>

<span data-ttu-id="6cf9c-268">Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-268">This service attempts to create and send a GET request with the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="6cf9c-269">Può essere usato per connettersi a una rete IPv4 o IPv6.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-269">It can be used to connect to IPv4 or IPv6 network.</span></span> <span data-ttu-id="6cf9c-270">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-270">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

> [!NOTE]
><span data-ttu-id="6cf9c-271">La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il rinvio delle richieste Get.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-271">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="6cf9c-272">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-272">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-273">Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_client_get_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-273">Developers are encouraged to migrate to *nxd_http_client_get_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-274">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-274">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-275">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-275">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-276">**Server_ip** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-276">**Server_ip** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-277">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-277">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-278">**input_ptr** Puntatore a dati aggiuntivi per la richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-278">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="6cf9c-279">Questo indirizzo è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-279">This is optional.</span></span> <span data-ttu-id="6cf9c-280">Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-280">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
 - <span data-ttu-id="6cf9c-281">**input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-281">**input_size** Number of bytes in optional additional input pointed to by ```input_ptr```.</span></span>
 - <span data-ttu-id="6cf9c-282">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-282">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-283">**username_length** Lunghezza del nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-283">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-284">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-284">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-285">**password_length** Lunghezza della password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-285">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-286">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-286">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="6cf9c-287">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-287">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-288">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-288">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-289">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-289">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-290">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-290">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-291">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-291">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-292">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-292">Return Values</span></span>

 - <span data-ttu-id="6cf9c-293">**NX_SUCCESS** (0x00) ha inviato la richiesta Get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-293">**NX_SUCCESS** (0x00) Successfully sent GET request</span></span>
 - <span data-ttu-id="6cf9c-294">La password di **NX_HTTP_PASSWORD_TOO_LONG** (0xF0) supera la dimensione del buffer</span><span class="sxs-lookup"><span data-stu-id="6cf9c-294">**NX_HTTP_PASSWORD_TOO_LONG** (0xF0) Password exceeds buffer size</span></span>
 - <span data-ttu-id="6cf9c-295">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-295">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-296">I parametri del pacchetto **NX_HTTP_FAILED** (0XE2) non sono validi.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-296">**NX_HTTP_FAILED** (0xE2) Invalid packet parameters.</span></span>
 - <span data-ttu-id="6cf9c-297">Il nome o la password di **NX_HTTP_AUTHENTICATION_ERROR** (0XEB) non è valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-297">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name or password</span></span>
 - <span data-ttu-id="6cf9c-298">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-298">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-299">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-299">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-300">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-300">Allowed From</span></span>

<span data-ttu-id="6cf9c-301">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-301">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-302">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-302">Example</span></span>

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;


/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nxd_http_client_get_start(&my_client, server_ip_address, “/TEST.HTM”,
NX_NULL, 0, “myname”, “mypassword”, 1000);


/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */
```

## <a name="nxd_http_client_get_start_extended"></a><span data-ttu-id="6cf9c-303">nxd_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-303">nxd_http_client_get_start_extended</span></span>

<span data-ttu-id="6cf9c-304">Inviare una richiesta HTTP GET (IPv4 o IPv6)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-304">Send an HTTP GET request (IPv4 or IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-305">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-305">Prototype</span></span>

```c
UINT nxd_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
                NXD_ADDRESS *server_ip, CHAR *resource,
                UINT resource_length, CHAR *input_ptr,
                UINT input_size, CHAR *username, UINT
                username_length, CHAR *password, UINT
                password_length, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-306">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-306">Description</span></span>

<span data-ttu-id="6cf9c-307">Questo servizio tenta di creare e inviare una richiesta GET con la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-307">This service attempts to create and send a GET request with the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="6cf9c-308">Può essere usato per connettersi a una rete IPv4 o IPv6.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-308">It can be used to connect to IPv4 or IPv6 network.</span></span> <span data-ttu-id="6cf9c-309">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-309">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-310">La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il rinvio delle richieste Get.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-310">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="6cf9c-311">Questo servizio sostituisce *nxd_http_client_get_start ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-311">This service replaces *nxd_http_client_get_start()*.</span></span> <span data-ttu-id="6cf9c-312">È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-312">It requires caller to specify the length of the resource, username and password.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-313">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-313">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-314">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-314">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-315">**Server_ip** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-315">**Server_ip** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-316">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-316">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-317">**resource_length** Lunghezza della stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-317">**resource_length** Length of URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-318">**input_ptr** Puntatore a dati aggiuntivi per la richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-318">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="6cf9c-319">Questo indirizzo è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-319">This is optional.</span></span> <span data-ttu-id="6cf9c-320">Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-320">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
 - <span data-ttu-id="6cf9c-321">**input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta ```input_ptr``` .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-321">**input_size** Number of bytes in optional additional input pointed to by ```input_ptr```.</span></span>
 - <span data-ttu-id="6cf9c-322">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-322">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-323">**username_length** Lunghezza del nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-323">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-324">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-324">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-325">**password_length** Lunghezza della password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-325">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-326">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa internamente per elaborare il client HTTP Get Start.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-326">**wait_option** Defines how long the service will wait internally to process the HTTP Client get start.</span></span> <span data-ttu-id="6cf9c-327">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-327">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-328">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-328">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-329">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-329">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-330">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-330">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-331">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-331">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-332">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-332">Return Values</span></span>

 - <span data-ttu-id="6cf9c-333">**NX_SUCCESS** (0x00) ha inviato la richiesta Get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-333">**NX_SUCCESS** (0x00) Successfully sent GET request</span></span>
 - <span data-ttu-id="6cf9c-334">La password di **NX_HTTP_PASSWORD_TOO_LONG** (0xF0) supera la dimensione del buffer</span><span class="sxs-lookup"><span data-stu-id="6cf9c-334">**NX_HTTP_PASSWORD_TOO_LONG** (0xF0) Password exceeds buffer size</span></span>
 - <span data-ttu-id="6cf9c-335">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-335">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-336">I parametri del pacchetto **NX_HTTP_FAILED** (0XE2) non sono validi.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-336">**NX_HTTP_FAILED** (0xE2) Invalid packet parameters.</span></span>
 - <span data-ttu-id="6cf9c-337">Il nome o la password di **NX_HTTP_AUTHENTICATION_ERROR** (0XEB) non è valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-337">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name or password</span></span>
 - <span data-ttu-id="6cf9c-338">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-338">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-339">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-339">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-340">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-340">Allowed From</span></span>

<span data-ttu-id="6cf9c-341">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-341">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-342">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-342">Example</span></span>

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;


/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nxd_http_client_get_start_extended(&my_client, server_ip_address,
                                             “/TEST.HTM”, 9, NX_NULL, 0, “myname”,
        6, “mypassword”, 10, 1000);


/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_http_client_get_packet"></a><span data-ttu-id="6cf9c-343">nx_http_client_get_packet</span><span class="sxs-lookup"><span data-stu-id="6cf9c-343">nx_http_client_get_packet</span></span>

<span data-ttu-id="6cf9c-344">Ottenere il pacchetto di dati di risorse successivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-344">Get next resource data packet</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-345">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-345">Prototype</span></span>

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET **packet_ptr, ULONG
                               wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-346">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-346">Description</span></span>

<span data-ttu-id="6cf9c-347">Questo servizio recupera il pacchetto successivo di contenuto della risorsa richiesta dalla chiamata *nx_http_client_get_start* precedente.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-347">This service retrieves the next packet of content of the resource requested by the previous *nx_http_client_get_start* call.</span></span> <span data-ttu-id="6cf9c-348">Le chiamate successive a questa routine devono essere apportate fino a quando non viene ricevuto lo stato di restituzione del NX_HTTP_GET_DONE.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-348">Successive calls to this routine should be made until the return status of NX_HTTP_GET_DONE is received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-349">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-349">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-350">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-350">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-351">**packet_ptr** Destinazione per il puntatore del pacchetto che contiene il contenuto parziale delle risorse.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-351">**packet_ptr** Destination for packet pointer containing partial resource content.</span></span>
 - <span data-ttu-id="6cf9c-352">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del pacchetto HTTP client Get.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-352">**wait_option** Defines how long the service will wait for the HTTP Client get packet.</span></span> <span data-ttu-id="6cf9c-353">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-353">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-354">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-354">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-355">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-355">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-356">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-356">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-357">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-357">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-358">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-358">Return Values</span></span>

 - <span data-ttu-id="6cf9c-359">**NX_SUCCESS** (0x00) client http con esito positivo Get Packet.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-359">**NX_SUCCESS** (0x00) Successful HTTP Client get packet.</span></span>
 - <span data-ttu-id="6cf9c-360">**NX_HTTP_GET_DONE** (0XEC) client HTTP Get packet is done</span><span class="sxs-lookup"><span data-stu-id="6cf9c-360">**NX_HTTP_GET_DONE** (0xEC) HTTP Client get packet is done</span></span>
 - <span data-ttu-id="6cf9c-361">Il client HTTP **NX_HTTP_NOT_READY** (0xea) non è in modalità Get.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-361">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not in get mode.</span></span>
 - <span data-ttu-id="6cf9c-362">Lunghezza del pacchetto **NX_HTTP_BAD_PACKET_LENGTH** (0XED) non valida</span><span class="sxs-lookup"><span data-stu-id="6cf9c-362">**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Invalid packet length</span></span>
 - <span data-ttu-id="6cf9c-363">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-363">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-364">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-364">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-365">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-365">Allowed From</span></span>

<span data-ttu-id="6cf9c-366">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-366">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-367">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-367">Example</span></span>

```c
/* Get the next packet of resource content on the HTTP Client “my_client.”
   Note that the nx_http_client_get_start routine must have been called
   previously. */
status =  nx_http_client_get_packet(&my_client, &next_packet, 1000);


/* If status is NX_SUCCESS, the next packet of content is pointed to
   by “next_packet”. */
```

## <a name="nx_http_client_put_start"></a><span data-ttu-id="6cf9c-368">nx_http_client_put_start</span><span class="sxs-lookup"><span data-stu-id="6cf9c-368">nx_http_client_put_start</span></span>

<span data-ttu-id="6cf9c-369">Avvia una richiesta HTTP PUT su IPv4</span><span class="sxs-lookup"><span data-stu-id="6cf9c-369">Start an HTTP PUT request over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-370">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-370">Prototype</span></span>

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               ULONG ip_address, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-371">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-371">Description</span></span>

<span data-ttu-id="6cf9c-372">Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-372">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address.</span></span> <span data-ttu-id="6cf9c-373">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet ()* per inviare effettivamente il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-373">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet()* routine to actually send the resource contents to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-374">La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il riferimento a richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-374">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="6cf9c-375">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-375">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-376">Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_client_put_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-376">Developers are encouraged to migrate to *nxd_http_client_put_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-377">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-377">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-378">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-378">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-379">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-379">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-380">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-380">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-381">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-381">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-382">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-382">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-383">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-383">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="6cf9c-384">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-384">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
 - <span data-ttu-id="6cf9c-385">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-385">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="6cf9c-386">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-386">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-387">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-387">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-388">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-388">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-389">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-389">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-390">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-390">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-391">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-391">Return Values</span></span>

 - <span data-ttu-id="6cf9c-392">**NX_SUCCESS** (0x00) ha inviato una richiesta PUT</span><span class="sxs-lookup"><span data-stu-id="6cf9c-392">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
 - <span data-ttu-id="6cf9c-393">Nome utente di **NX_HTTP_USERNAME_TOO_LONG** (0xF1) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="6cf9c-393">**NX_HTTP_USERNAME_TOO_LONG** (0xF1) Username too large for buffer</span></span>
 - <span data-ttu-id="6cf9c-394">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-394">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-395">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-395">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-396">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="6cf9c-396">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
 - <span data-ttu-id="6cf9c-397">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-397">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-398">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-398">Allowed From</span></span>

<span data-ttu-id="6cf9c-399">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-400">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-400">Example</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP Server
   at IP address 1.2.3.5. */
status =  nx_http_client_put_start(&my_client, IP_ADDRESS(1, 2, 3, 5),
“/TEST.HTM”, “myname”, “mypassword”, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
   started. */
```

## <a name="nx_http_client_put_start_extended"></a><span data-ttu-id="6cf9c-401">nx_http_client_put_start_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-401">nx_http_client_put_start_extended</span></span>

<span data-ttu-id="6cf9c-402">Avvia una richiesta HTTP PUT su IPv4</span><span class="sxs-lookup"><span data-stu-id="6cf9c-402">Start an HTTP PUT request over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-403">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-403">Prototype</span></span>

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
           ULONG ip_address, CHAR *resource, UINT resource_length,
           CHAR *username,UINT username_length, CHAR *password,
           UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-404">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-404">Description</span></span>

<span data-ttu-id="6cf9c-405">Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-405">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address.</span></span> <span data-ttu-id="6cf9c-406">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet ()* per inviare effettivamente il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-406">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet()* routine to actually send the resource contents to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-407">La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il riferimento a richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-407">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="6cf9c-408">Questo servizio sostituisce *nx_http_client_put_start ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-408">This service replaces *nx_http_client_put_start()*.</span></span> <span data-ttu-id="6cf9c-409">È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-409">It requires caller to specify the length of the resource, username and password.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-410">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-410">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-411">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-411">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-412">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-412">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-413">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-413">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-414">**resource_length** Lunghezza della stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-414">**resource_length** Length of URL string for resource to send to Server.</span></span>
 - <span data-ttu-id="6cf9c-415">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-415">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-416">**username_length** Lunghezza del nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-416">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-417">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-417">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-418">**password_length** Lunghezza della password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-418">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-419">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-419">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="6cf9c-420">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-420">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
 - <span data-ttu-id="6cf9c-421">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-421">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="6cf9c-422">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-422">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-423">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-423">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-424">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-424">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-425">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-425">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-426">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-426">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-427">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-427">Return Values</span></span>

 - <span data-ttu-id="6cf9c-428">**NX_SUCCESS** (0x00) ha inviato una richiesta PUT</span><span class="sxs-lookup"><span data-stu-id="6cf9c-428">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
 - <span data-ttu-id="6cf9c-429">Nome utente di **NX_HTTP_USERNAME_TOO_LONG** (0xF1) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="6cf9c-429">**NX_HTTP_USERNAME_TOO_LONG** (0xF1) Username too large for buffer</span></span>
 - <span data-ttu-id="6cf9c-430">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-430">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-431">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-431">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-432">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="6cf9c-432">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
 - <span data-ttu-id="6cf9c-433">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-433">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-434">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-434">Allowed From</span></span>

<span data-ttu-id="6cf9c-435">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-435">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-436">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-436">Example</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP Server
   at IP address 1.2.3.5. */
status =  nx_http_client_put_start_extended(&my_client, IP_ADDRESS(1, 2, 3, 5),
“/TEST.HTM”, 9, “myname”, 6, “mypassword”, 10, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
   started. */
```

## <a name="nxd_http_client_put_start"></a><span data-ttu-id="6cf9c-437">nxd_http_client_put_start</span><span class="sxs-lookup"><span data-stu-id="6cf9c-437">nxd_http_client_put_start</span></span>

<span data-ttu-id="6cf9c-438">Avviare una richiesta HTTP PUT (IPv4 o IPv6)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-438">Start an HTTP PUT request (IPv4 or IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-439">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-439">Prototype</span></span>

```c
UINT nxd_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               NXD_ADDRESS *server_ip, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-440">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-440">Description</span></span>

<span data-ttu-id="6cf9c-441">Questo servizio tenta di inserire (inviare) la risorsa specificata sul server HTTP nell'indirizzo IP fornito su IPv6.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-441">This service attempts to PUT (send) the specified resource on the HTTP Server at the supplied IP address over IPv6.</span></span> <span data-ttu-id="6cf9c-442">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet ()* per inviare effettivamente il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-442">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet()* routine to actually send the resource contents to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-443">La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il riferimento a richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-443">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="6cf9c-444">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-444">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-445">Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_client_put_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-445">Developers are encouraged to migrate to *nxd_http_client_put_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-446">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-446">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-447">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-447">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-448">**server_ip** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-448">**server_ip** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-449">**risorsa** di Puntatore alla stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-449">**resource** Pointer to URL string for resource to send to Server.</span></span>
 - <span data-ttu-id="6cf9c-450">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-450">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-451">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-451">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-452">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-452">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="6cf9c-453">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-453">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
 - <span data-ttu-id="6cf9c-454">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-454">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="6cf9c-455">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-455">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-456">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-456">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-457">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-457">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-458">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-458">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-459">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-459">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-460">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-460">Return Values</span></span>

 - <span data-ttu-id="6cf9c-461">**NX_SUCCESS** (0x00) ha inviato la richiesta PUT del client http</span><span class="sxs-lookup"><span data-stu-id="6cf9c-461">**NX_SUCCESS** (0x00) Successfully sent HTTP Client PUT request</span></span>
 - <span data-ttu-id="6cf9c-462">Errore interno del client HTTP **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-462">**NX_HTTP_ERROR** (0xE0) HTTP Client internal error</span></span>
 - <span data-ttu-id="6cf9c-463">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-463">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-464">Errore del client HTTP di **NX_HTTP_FAILED** (0xe2) che comunica con il server http</span><span class="sxs-lookup"><span data-stu-id="6cf9c-464">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server</span></span>
 - <span data-ttu-id="6cf9c-465">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-465">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-466">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="6cf9c-466">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
 - <span data-ttu-id="6cf9c-467">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-467">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-468">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-468">Allowed From</span></span>

<span data-ttu-id="6cf9c-469">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-469">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-470">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-470">Example</span></span>

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;

/* Start an HTTP PUT to place the 20-byte resource Client_test.HTM” on the HTTPv6  
   Server. */
status =  nxd_http_client_put_start(&my_client, &server_ip_address,
                                    "/client_test.htm", "name", "password", 103, 50);

/* If status is NX_SUCCESS, the PUT operation for Client_test.HTM has successfully
   been started. */
```

## <a name="nxd_http_client_put_start_extended"></a><span data-ttu-id="6cf9c-471">nxd_http_client_put_start_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-471">nxd_http_client_put_start_extended</span></span>

<span data-ttu-id="6cf9c-472">Avviare una richiesta HTTP PUT (IPv4 o IPv6)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-472">Start an HTTP PUT request (IPv4 or IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-473">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-473">Prototype</span></span>

```c
UINT nxd_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
          NXD_ADDRESS *server_ip, CHAR *resource, UINT resource_length,
          CHAR *username, UINT username_length, CHAR *password,
          UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-474">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-474">Description</span></span>

<span data-ttu-id="6cf9c-475">Questo servizio tenta di inserire (inviare) la risorsa specificata sul server HTTP nell'indirizzo IP fornito su IPv6.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-475">This service attempts to PUT (send) the specified resource on the HTTP Server at the supplied IP address over IPv6.</span></span> <span data-ttu-id="6cf9c-476">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet ()* per inviare effettivamente il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-476">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet()* routine to actually send the resource contents to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-477">La stringa di risorsa può fare riferimento a un file locale, ad esempio ``` “/index.htm” ``` , oppure può fare riferimento a un altro URL, ad esempio ```http://abc.website.com/index.htm``` se il server HTTP indica che supporta il riferimento a richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-477">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="6cf9c-478">Questo servizio sostituisce *nxd_http_client_put_start ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-478">This service replaces *nxd_http_client_put_start()*.</span></span> <span data-ttu-id="6cf9c-479">È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-479">It requires caller to specify the length of the resource, username and password.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-480">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-480">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-481">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-481">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-482">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-482">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-483">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-483">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="6cf9c-484">**resource_length** Lunghezza della stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-484">**resource_length** Length of URL string for resource to send to Server.</span></span>
 - <span data-ttu-id="6cf9c-485">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-485">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-486">**username_length** Lunghezza del nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-486">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="6cf9c-487">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-487">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-488">**password_length** Lunghezza della password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-488">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="6cf9c-489">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-489">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="6cf9c-490">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-490">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
 - <span data-ttu-id="6cf9c-491">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-491">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="6cf9c-492">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-492">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-493">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-493">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-494">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-494">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-495">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-495">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-496">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-496">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-497">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-497">Return Values</span></span>

 - <span data-ttu-id="6cf9c-498">**NX_SUCCESS** (0x00) ha inviato la richiesta PUT del client http</span><span class="sxs-lookup"><span data-stu-id="6cf9c-498">**NX_SUCCESS** (0x00) Successfully sent HTTP Client PUT request</span></span>
 - <span data-ttu-id="6cf9c-499">Errore interno del client HTTP **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-499">**NX_HTTP_ERROR** (0xE0) HTTP Client internal error</span></span>
 - <span data-ttu-id="6cf9c-500">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-500">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-501">Errore del client HTTP di NX_HTTP_FAILED (0xE2) che comunica con il server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-501">NX_HTTP_FAILED (0xE2) HTTP Client error communicating with the HTTP Server</span></span>
 - <span data-ttu-id="6cf9c-502">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-502">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-503">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="6cf9c-503">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
 - <span data-ttu-id="6cf9c-504">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-504">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-505">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-505">Allowed From</span></span>

<span data-ttu-id="6cf9c-506">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-506">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-507">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-507">Example</span></span>

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;

/* Start an HTTP PUT to place the 20-byte resource Client_test.HTM” on the HTTPv6  
   Server. */
status =  nxd_http_client_put_start_extended(&my_client, &server_ip_address,
                                            "/client_test.htm", 16, "name", 4, "password", 8, 103, 50);

/* If status is NX_SUCCESS, the PUT operation for Client_test.HTM has successfully
   been started. */
```

## <a name="nx_http_client_put_packet"></a><span data-ttu-id="6cf9c-508">nx_http_client_put_packet</span><span class="sxs-lookup"><span data-stu-id="6cf9c-508">nx_http_client_put_packet</span></span>

<span data-ttu-id="6cf9c-509">Invia pacchetto di dati di risorse successivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-509">Send next resource data packet</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-510">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-510">Prototype</span></span>

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET *packet_ptr,
                               ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="6cf9c-511">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-511">Description</span></span>

<span data-ttu-id="6cf9c-512">Questo servizio tenta di inviare il pacchetto successivo di contenuto di risorse al server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-512">This service attempts to send the next packet of resource content to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-513">Questa routine deve essere chiamata ripetutamente fino a quando la lunghezza combinata dei pacchetti inviati è uguale alla "total_bytes" specificata nella chiamata *nx_http_client_put_start* precedente.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-513">This routine should be called repetitively until the combined length of the packets sent equals the “total_bytes” specified in the previous *nx_http_client_put_start* call.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-514">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-514">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-515">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-515">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-516">**packet_ptr** Puntatore al contenuto successivo della risorsa da inviare al server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-516">**packet_ptr** Pointer to next content of the resource to being sent to the HTTP Server.</span></span>
 - <span data-ttu-id="6cf9c-517">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa internamente per elaborare il pacchetto PUT del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-517">**wait_option** Defines how long the service will wait internally to process the HTTP Client PUT packet.</span></span> <span data-ttu-id="6cf9c-518">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-518">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="6cf9c-519">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-519">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="6cf9c-520">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-520">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="6cf9c-521">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-521">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="6cf9c-522">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-522">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-523">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-523">Return Values</span></span>

 - <span data-ttu-id="6cf9c-524">Il pacchetto client HTTP è stato inviato **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-524">**NX_SUCCESS** (0x00) Successfully sent HTTP Client packet.</span></span>
 - <span data-ttu-id="6cf9c-525">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-525">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="6cf9c-526">**NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0XEE) ha ricevuto il codice di errore del server</span><span class="sxs-lookup"><span data-stu-id="6cf9c-526">**NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) Received Server error code</span></span>
 - <span data-ttu-id="6cf9c-527">Lunghezza del pacchetto **NX_HTTP_BAD_PACKET_LENGTH** (0XED) non valida</span><span class="sxs-lookup"><span data-stu-id="6cf9c-527">**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Invalid packet length</span></span>
 - <span data-ttu-id="6cf9c-528">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi</span><span class="sxs-lookup"><span data-stu-id="6cf9c-528">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or Password</span></span>
 - <span data-ttu-id="6cf9c-529">Il server **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) risponde prima del completamento dell'operazione Put</span><span class="sxs-lookup"><span data-stu-id="6cf9c-529">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Server responds before PUT Is complete</span></span>
 - <span data-ttu-id="6cf9c-530">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-530">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-531">Pacchetto di NX_INVALID_PACKET (0x12) troppo piccolo per l'intestazione TCP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-531">NX_INVALID_PACKET (0x12) Packet too small for TCP header</span></span>
 - <span data-ttu-id="6cf9c-532">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-532">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-533">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-533">Allowed From</span></span>

<span data-ttu-id="6cf9c-534">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-534">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-535">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-535">Example</span></span>

```c
/* Send a 20-byte packet representing the content of the resource
   “/TEST.HTM” to the HTTP Server. */
status =  nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr, NX_PACKET *packet_ptr, ULONG wait_option);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM has
   successfully been sent. */
```

## <a name="nx_http_client_set_connect_port"></a><span data-ttu-id="6cf9c-536">nx_http_client_set_connect_port</span><span class="sxs-lookup"><span data-stu-id="6cf9c-536">nx_http_client_set_connect_port</span></span>

<span data-ttu-id="6cf9c-537">Impostare la porta di connessione sul server</span><span class="sxs-lookup"><span data-stu-id="6cf9c-537">Set the connection port to the Server</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-538">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-538">Prototype</span></span>

```c
UINT nx_http_client_set_connect_port(NX_HTTP_CLIENT *client_ptr,
                                      UINT port);
```

### <a name="description"></a><span data-ttu-id="6cf9c-539">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-539">Description</span></span>

<span data-ttu-id="6cf9c-540">Questo servizio modifica la porta di connessione per la connessione al server HTTP alla porta specificata in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-540">This service changes the connect port when connecting to the HTTP Server to the specified port at runtime.</span></span> <span data-ttu-id="6cf9c-541">In caso contrario, il valore predefinito della porta di connessione è 80.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-541">Otherwise the connect port defaults to 80.</span></span> <span data-ttu-id="6cf9c-542">Questo metodo deve essere chiamato prima di *nx_http_client_get_start ()* e *nx_http_client_put_start ()* , ad esempio quando il client HTTP si connette al server.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-542">This must be called before *nx_http_client_get_start()* and *nx_http_client_put_start()* e.g. when the HTTP Client connects with the Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-543">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-543">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-544">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-544">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="6cf9c-545">**porta** Porta per la connessione al server.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-545">**port** Port for connecting to the Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-546">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-546">Return Values</span></span>

 - <span data-ttu-id="6cf9c-547">**NX_SUCCESS** (0x00) modifica la porta</span><span class="sxs-lookup"><span data-stu-id="6cf9c-547">**NX_SUCCESS** (0x00) Successfully change port</span></span>
 - <span data-ttu-id="6cf9c-548">La porta NX_INVALID_PORT (0x46) supera il valore massimo (0xFFFF) o è zero</span><span class="sxs-lookup"><span data-stu-id="6cf9c-548">NX_INVALID_PORT (0x46) Port exceeds the maximum (0xFFFF) or is zero</span></span>
 - <span data-ttu-id="6cf9c-549">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-549">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-550">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-550">Allowed From</span></span>

<span data-ttu-id="6cf9c-551">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-551">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-552">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-552">Example</span></span>

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status =  nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a><span data-ttu-id="6cf9c-553">nx_http_server_cache_info_callback_set</span><span class="sxs-lookup"><span data-stu-id="6cf9c-553">nx_http_server_cache_info_callback_set</span></span>

<span data-ttu-id="6cf9c-554">Impostare il callback per il recupero della validità e della data massima dell'URL</span><span class="sxs-lookup"><span data-stu-id="6cf9c-554">Set the callback to retrieve URL max age and date</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-555">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-555">Prototype</span></span>

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                         UINT (*cache_info_get)(CHAR *resource,
                                                 UINT *max_age,
                                                 NX_HTTP_SERVER_DATE
                                                      *date));
```

### <a name="description"></a><span data-ttu-id="6cf9c-556">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-556">Description</span></span>

<span data-ttu-id="6cf9c-557">Questo servizio imposta il servizio di callback richiamato per ottenere la data di validità massima e dell'Ultima modifica della risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-557">This service sets the callback service invoked to obtain the maximum age and last modified date of the specified resource.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-558">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-558">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-559">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-559">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-560">**cache_info_get** Puntatore al callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-560">**cache_info_get** Pointer to the callback</span></span>
 - <span data-ttu-id="6cf9c-561">**max_age** Puntatore alla durata massima di una risorsa</span><span class="sxs-lookup"><span data-stu-id="6cf9c-561">**max_age** Pointer to maximum age of a resource</span></span>
 - <span data-ttu-id="6cf9c-562">**dati** di Puntatore alla data dell'Ultima modifica restituita.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-562">**data** Pointer to last modified date returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-563">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-563">Return Values</span></span>

 - <span data-ttu-id="6cf9c-564">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-564">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="6cf9c-565">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-565">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-566">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-566">Allowed From</span></span>

<span data-ttu-id="6cf9c-567">Inizializzazione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-567">Initialization</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-568">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-568">Example</span></span>

```c
NX_HTTP_SERVER my_server;

UINT cache_info_get(CHAR *resource, UINT *max_age,
                           NX_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_http_server_create and before the HTTP  
   server is set by nx_http_server_start(), set the cache info callback: */

status = nx_http_server_cache_info_callback_set(&my_server, cache_info_get);


/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_http_server_callback_data_send"></a><span data-ttu-id="6cf9c-569">nx_http_server_callback_data_send</span><span class="sxs-lookup"><span data-stu-id="6cf9c-569">nx_http_server_callback_data_send</span></span>

<span data-ttu-id="6cf9c-570">Inviare dati da una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-570">Send data from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-571">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-571">Prototype</span></span>

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                       VOID *data_ptr,
                                       ULONG data_length);
```

### <a name="description"></a><span data-ttu-id="6cf9c-572">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-572">Description</span></span>

<span data-ttu-id="6cf9c-573">Questo servizio invia i dati nel pacchetto fornito dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-573">This service sends the data in the supplied packet from the application’s callback routine.</span></span> <span data-ttu-id="6cf9c-574">Questa operazione viene in genere usata per inviare i dati dinamici associati alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-574">This is typically used to send dynamic data associated with GET/POST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-575">Se viene utilizzata questa funzione, la routine di callback è responsabile dell'invio dell'intera risposta nel formato corretto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-575">If this function is used, the callback routine is responsible for sending the entire response in the proper format.</span></span> <span data-ttu-id="6cf9c-576">Inoltre, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-576">In addition, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-577">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-577">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-578">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-578">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-579">**DATA_PTR** Puntatore ai dati da inviare.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-579">**data_ptr** Pointer to the data to send.</span></span>
 - <span data-ttu-id="6cf9c-580">**Data_length**  Numero di byte da inviare.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-580">**data_length**  Number of bytes to send.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-581">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-581">Return Values</span></span>

 - <span data-ttu-id="6cf9c-582">**NX_SUCCESS** (0x00) ha inviato correttamente i dati del server</span><span class="sxs-lookup"><span data-stu-id="6cf9c-582">**NX_SUCCESS** (0x00) Successfully sent Server data</span></span>
 - <span data-ttu-id="6cf9c-583">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-583">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-584">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-584">Allowed From</span></span>

<span data-ttu-id="6cf9c-585">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-585">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-586">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-586">Example</span></span>

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
  CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
                (strcmp(resource, "/test.htm") == 0))
    {

        /* Found it, override the GET processing by sending the resource
    contents directly. */

        nx_http_server_callback_data_send(server_ptr,
    "HTTP/1.0 200 \r\nContent-Length:
    103\r\nContent-Type: text/html\r\n\r\n",
    63);

        nx_http_server_callback_data_send(server_ptr, "<HTML>\r\n<HEAD><TITLE>NetX
    HTTP Test </TITLE></HEAD>\r\n
    <BODY>\r\n<H1>NetX Test Page
    </H1>\r\n</BODY>\r\n</HTML>\r\n", 103);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_generate_response_header"></a><span data-ttu-id="6cf9c-587">nx_http_server_callback_generate_response_header</span><span class="sxs-lookup"><span data-stu-id="6cf9c-587">nx_http_server_callback_generate_response_header</span></span>

<span data-ttu-id="6cf9c-588">Creare un'intestazione della risposta in una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-588">Create a response header in a callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-589">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-589">Prototype</span></span>

```c
UINT nx_http_server_callback_generate_response_header(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT content_length,
                        CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a><span data-ttu-id="6cf9c-590">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-590">Description</span></span>

<span data-ttu-id="6cf9c-591">Questo servizio chiama la funzione interna *_nx_http_server_generate_response_header* quando il server HTTP risponde alle richieste Get, put e Delete del client.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-591">This service calls the internal function *_nx_http_server_generate_response_header* when the HTTP server responds to Client get, put and delete requests.</span></span> <span data-ttu-id="6cf9c-592">È destinato all'uso nelle funzioni di callback del server HTTP quando l'applicazione server HTTP sta progettando la propria risposta al client.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-592">It is intended for use in HTTP server callback functions when the HTTP server application is designing its response to the Client.</span></span>

<span data-ttu-id="6cf9c-593">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-593">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-594">Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_server_callback_generate_response_header_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-594">Developers are encouraged to migrate to *nxd_http_server_callback_generate_response_header_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-595">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-595">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-596">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-596">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-597">**packet_pptr** Puntatore a un puntatore di pacchetto allocato per il messaggio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-597">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
 - <span data-ttu-id="6cf9c-598">**status_code** Indicare lo stato della risorsa.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-598">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="6cf9c-599">Esempi:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-599">Examples:</span></span>
    - <span data-ttu-id="6cf9c-600">**NX_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="6cf9c-600">**NX_HTTP_STATUS_OK**</span></span>
    - <span data-ttu-id="6cf9c-601">**NX_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="6cf9c-601">**NX_HTTP_STATUS_MODIFIED**</span></span>
    - <span data-ttu-id="6cf9c-602">**NX_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="6cf9c-602">**NX_HTTP_STATUS_INTERNAL_ERROR**</span></span>
 - <span data-ttu-id="6cf9c-603">**CONTENT_LENGTH** Dimensioni del contenuto in byte</span><span class="sxs-lookup"><span data-stu-id="6cf9c-603">**content_length** Size of content in bytes</span></span>
 - <span data-ttu-id="6cf9c-604">**content_type** Tipo di HTTP, ad esempio "text/plain"</span><span class="sxs-lookup"><span data-stu-id="6cf9c-604">**content_type** Type of HTTP e.g. “text/plain”</span></span>
 - <span data-ttu-id="6cf9c-605">**additional_header** Puntatore a testo intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-605">**additional_header** Pointer to additional header text</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-606">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-606">Return Values</span></span>

 - <span data-ttu-id="6cf9c-607">Intestazione creazione **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="6cf9c-607">**NX_SUCCESS** (0x00) Successfully created header</span></span>
 - <span data-ttu-id="6cf9c-608">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-608">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-609">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-609">Allowed From</span></span>

<span data-ttu-id="6cf9c-610">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-610">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-611">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-611">Example</span></span>

```c
CHAR demotestbuffer[] = "<html>\r\n\r\n<head>\r\n\r\n<title>Main   \
            Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n   \  </body>\r\n</html>\r\n";

     /* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
 CHAR *resource, NX_PACKET *recv_packet_ptr)
      {

NX_PACKET   *sresp_packet_ptr;
ULONG       string_length;
CHAR        temp_string[30];
ULONG       length = 0;


   length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length =  (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr ->
nx_http_server_request_resource, temp_string,
sizeof(temp_string));

       /* Null terminate the string. */
   temp_string[temp] = 0;

       /* Now build a response header with server status is OK and no additional header  
          info. */
   status = nx_http_server_callback_generate_response_header(http_server_ptr,
                  &resp_packet_ptr, NX_HTTP_STATUS_OK,
                  length, temp_string, NX_NULL);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                 length,  server_ptr ->
                 nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
       nx_packet_release(resp_packet_ptr);
       return status;
   }



/* Now send the packet! */
           status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                      resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
      nx_packet_release(resp_packet_ptr);

      return status;
   }

/* Let HTTP server know the response has been sent. */
  return NX_HTTP_CALLBACK_COMPLETED;

     }
```

## <a name="nx_http_server_callback_generate_response_header_extended"></a><span data-ttu-id="6cf9c-612">nx_http_server_callback_generate_response_header_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-612">nx_http_server_callback_generate_response_header_extended</span></span>

<span data-ttu-id="6cf9c-613">Creare un'intestazione della risposta in una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-613">Create a response header in a callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-614">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-614">Prototype</span></span>

```c
UINT nx_http_server_callback_generate_response_header_extended(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT status_code_length,
                        UINT content_length,
                        CHAR *content_type, UINT content_type_length,
                        CHAR *additional_header,
                        UINT additional_header_length);
```

### <a name="description"></a><span data-ttu-id="6cf9c-615">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-615">Description</span></span>

<span data-ttu-id="6cf9c-616">Questo servizio chiama la funzione interna *_nx_http_server_generate_response_header ()* quando il server HTTP risponde alle richieste Get, put e Delete del client.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-616">This service calls the internal function *_nx_http_server_generate_response_header()* when the HTTP server responds to Client get, put and delete requests.</span></span> <span data-ttu-id="6cf9c-617">È destinato all'uso nelle funzioni di callback del server HTTP quando l'applicazione server HTTP sta progettando la propria risposta al client.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-617">It is intended for use in HTTP server callback functions when the HTTP server application is designing its response to the Client.</span></span>

<span data-ttu-id="6cf9c-618">Questo servizio sostituisce *nx_http_server_callback_generate_response_header ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-618">This service replaces *nx_http_server_callback_generate_response_header()*.</span></span> <span data-ttu-id="6cf9c-619">Questa versione fornisce informazioni aggiuntive sulla lunghezza della funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-619">This version supplies additional length information to the callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-620">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-620">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-621">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-621">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-622">**packet_pptr** Puntatore a un puntatore di pacchetto allocato per il messaggio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-622">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
 - <span data-ttu-id="6cf9c-623">**status_code** Indicare lo stato della risorsa.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-623">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="6cf9c-624">Esempi:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-624">Examples:</span></span>
    - <span data-ttu-id="6cf9c-625">**NX_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="6cf9c-625">**NX_HTTP_STATUS_OK**</span></span>
    - <span data-ttu-id="6cf9c-626">**NX_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="6cf9c-626">**NX_HTTP_STATUS_MODIFIED**</span></span>
    - <span data-ttu-id="6cf9c-627">**NX_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="6cf9c-627">**NX_HTTP_STATUS_INTERNAL_ERROR**</span></span>
 - <span data-ttu-id="6cf9c-628">**status_code** Lunghezza del codice di stato</span><span class="sxs-lookup"><span data-stu-id="6cf9c-628">**status_code** Length of status code</span></span>
 - <span data-ttu-id="6cf9c-629">**CONTENT_LENGTH** Dimensioni del contenuto in byte</span><span class="sxs-lookup"><span data-stu-id="6cf9c-629">**content_length** Size of content in bytes</span></span>
 - <span data-ttu-id="6cf9c-630">**content_type** Tipo di HTTP, ad esempio "text/plain"</span><span class="sxs-lookup"><span data-stu-id="6cf9c-630">**content_type** Type of HTTP e.g. “text/plain”</span></span>
 - <span data-ttu-id="6cf9c-631">**content_type_length** Lunghezza del tipo HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-631">**content_type_length** Length of HTTP type</span></span>
 - <span data-ttu-id="6cf9c-632">**additional_header** Puntatore a testo intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-632">**additional_header** Pointer to additional header text</span></span>
 - <span data-ttu-id="6cf9c-633">**additional_header_length** Lunghezza del testo dell'intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-633">**additional_header_length** Length of additional header text</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-634">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-634">Return Values</span></span>

 - <span data-ttu-id="6cf9c-635">Intestazione creazione **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="6cf9c-635">**NX_SUCCESS** (0x00) Successfully created header</span></span>
 - <span data-ttu-id="6cf9c-636">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-636">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-637">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-637">Allowed From</span></span>

<span data-ttu-id="6cf9c-638">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-638">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-639">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-639">Example</span></span>

```c
CHAR demotestbuffer[] = "<html>\r\n\r\n<head>\r\n\r\n<title>Main   \
     Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n   \  </body>\r\n</html>\r\n";

     /* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
 CHAR *resource, NX_PACKET *recv_packet_ptr)
      {

NX_PACKET   *sresp_packet_ptr;
ULONG       string_length;
CHAR        temp_string[30];
ULONG       length = 0;


   length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length =  (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr ->
nx_http_server_request_resource, temp_string,
sizeof(temp_string));

       /* Null terminate the string. */
   temp_string[temp] = 0;

       /* Now build a response header with server status is OK and no additional header  
          info. */
   status = nx_http_server_callback_generate_response_header_extended(
                             http_server_ptr, &resp_packet_ptr, NX_HTTP_STATUS_OK,
              sizeof(NX_HTTP_STATUS_OK) - 1, length,
              temp_string, string_length, NX_NULL, 0);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                 length,  server_ptr ->
                 nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
       nx_packet_release(resp_packet_ptr);
       return status;
   }



/* Now send the packet! */
           status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                      resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
      nx_packet_release(resp_packet_ptr);

      return status;
   }

/* Let HTTP server know the response has been sent. */
  return NX_HTTP_CALLBACK_COMPLETED;

     }
```

## <a name="nx_http_server_callback_packet_send"></a><span data-ttu-id="6cf9c-640">nx_http_server_callback_packet_send</span><span class="sxs-lookup"><span data-stu-id="6cf9c-640">nx_http_server_callback_packet_send</span></span>

<span data-ttu-id="6cf9c-641">Inviare un pacchetto HTTP dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-641">Send an HTTP packet from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-642">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-642">Prototype</span></span>

```c
UINT nx_http_server_callback_packet_send(NX_HTTP_SERVER *server_ptr,
                                         NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="6cf9c-643">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-643">Description</span></span>

<span data-ttu-id="6cf9c-644">Questo servizio invia una risposta server HTTP completa da un callback HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-644">This service sends a complete HTTP server response from an HTTP callback.</span></span> <span data-ttu-id="6cf9c-645">Il pacchetto viene inviato dal server HTTP al _TIMEOUT_SEND NX_HTTP_SERVER.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-645">HTTP server will send the packet with the NX_HTTP_SERVER _TIMEOUT_SEND.</span></span> <span data-ttu-id="6cf9c-646">L'intestazione e i dati HTTP devono essere aggiunti al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-646">The HTTP header and data must be appended to the packet.</span></span> <span data-ttu-id="6cf9c-647">Se lo stato restituito indica un errore, l'applicazione HTTP deve rilasciare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-647">If the return status indicates an error, the HTTP application must release the packet.</span></span>

<span data-ttu-id="6cf9c-648">Il callback deve restituire NX_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-648">The callback should return NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="6cf9c-649">Per un esempio più dettagliato, vedere *nx_http_server_callback_generate_response_header ()* .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-649">See *nx_http_server_callback_generate_response_header()* for a more detailed example.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-650">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-650">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-651">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-651">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-652">**packet_ptr** Puntatore al pacchetto da inviare</span><span class="sxs-lookup"><span data-stu-id="6cf9c-652">**packet_ptr** Pointer to the packet to send</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-653">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-653">Return Values</span></span>

 - <span data-ttu-id="6cf9c-654">Il pacchetto server è stato inviato **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-654">**NX_SUCCESS** (0x00) Successfully sent Server packet</span></span>
 - <span data-ttu-id="6cf9c-655">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-655">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-656">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-656">Allowed From</span></span>

<span data-ttu-id="6cf9c-657">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-657">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-658">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-658">Example</span></span>

```c
/* The packet is appended with HTTP header and data and is ready to send to the
   Client directly. */

   status = nx_http_server_callback_response_send(server_ptr, packet_ptr);

   if (status != NX_SUCCESS)
   {

    nx_packet_release(packet_ptr);
   }

    return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_callback_response_send"></a><span data-ttu-id="6cf9c-659">nx_http_server_callback_response_send</span><span class="sxs-lookup"><span data-stu-id="6cf9c-659">nx_http_server_callback_response_send</span></span>

<span data-ttu-id="6cf9c-660">Invia risposta dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-660">Send response from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-661">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-661">Prototype</span></span>

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
                                           CHAR *header,
                                           CHAR *information,
                                           CHAR additional_info);
```

### <a name="description"></a><span data-ttu-id="6cf9c-662">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-662">Description</span></span>

<span data-ttu-id="6cf9c-663">Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-663">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="6cf9c-664">Questa operazione viene in genere usata per inviare risposte personalizzate associate alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-664">This is typically used to send custom responses associated with GET/POST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-665">Se viene utilizzata questa funzione, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-665">If this function is used, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="6cf9c-666">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-666">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-667">Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_server_callback_response_send_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-667">Developers are encouraged to migrate to *nxd_http_server_callback_response_send_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-668">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-668">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-669">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-669">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-670">**intestazione** di Puntatore alla stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-670">**header** Pointer to the response header string.</span></span>
 - <span data-ttu-id="6cf9c-671">**informazioni** su Puntatore alla stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-671">**information** Pointer to the information string.</span></span>
 - <span data-ttu-id="6cf9c-672">**additional_info** Puntatore alla stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-672">**additional_info** Pointer to the additional information string.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-673">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-673">Return Values</span></span>

 - <span data-ttu-id="6cf9c-674">**NX_SUCCESS** (0x00) ha inviato una risposta server</span><span class="sxs-lookup"><span data-stu-id="6cf9c-674">**NX_SUCCESS** (0x00) Successfully sent Server response</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-675">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-675">Allowed From</span></span>

<span data-ttu-id="6cf9c-676">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-676">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-677">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-677">Example</span></span>

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                        CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
               (strcmp(resource, "/test.htm") == 0))
    {

        /* In this example, we will complete the GET processing with
           a resource not found response. */
     nx_http_server_callback_response_send(server_ptr,
                      "HTTP/1.0 404 ",
                      "NetX HTTP Server unable to find  
                       file: ", resource);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_response_send_extended"></a><span data-ttu-id="6cf9c-678">nx_http_server_callback_response_send_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-678">nx_http_server_callback_response_send_extended</span></span>

<span data-ttu-id="6cf9c-679">Invia risposta dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-679">Send response from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-680">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-680">Prototype</span></span>

```c
UINT nx_http_server_callback_response_send_extended(
                                          NX_HTTP_SERVER *server_ptr,
                                          CHAR *header,
                                          UINT header_length,
                                          CHAR *information,
                                          UINT information_length,
                                          CHAR *additional_info,
                                          UINT additional_info_length);
```

### <a name="description"></a><span data-ttu-id="6cf9c-681">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-681">Description</span></span>

<span data-ttu-id="6cf9c-682">Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-682">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="6cf9c-683">Questa operazione viene in genere usata per inviare risposte personalizzate associate alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-683">This is typically used to send custom responses associated with GET/POST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-684">Se viene utilizzata questa funzione, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-684">If this function is used, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="6cf9c-685">Questo servizio sostituisce *nx_http_server_callback_response_send ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-685">This service replaces *nx_http_server_callback_response_send()*.</span></span> <span data-ttu-id="6cf9c-686">Questa versione accetta informazioni di lunghezza aggiuntive come argomenti.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-686">This version takes additional length information as arguments.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-687">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-687">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-688">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-688">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-689">**intestazione** di Puntatore alla stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-689">**header** Pointer to the response header string.</span></span>
 - <span data-ttu-id="6cf9c-690">**HEADER_LENGTH** Lunghezza della stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-690">**header_length** Length of the response header string.</span></span>
 - <span data-ttu-id="6cf9c-691">**informazioni** su Puntatore alla stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-691">**information** Pointer to the information string.</span></span>
 - <span data-ttu-id="6cf9c-692">**information_length** Lunghezza della stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-692">**information_length** Length of the information string.</span></span>
 - <span data-ttu-id="6cf9c-693">**additional_info** Puntatore alla stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-693">**additional_info** Pointer to the additional information string.</span></span>
 - <span data-ttu-id="6cf9c-694">**additional_info_length** Lunghezza della stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-694">**additional_info_length** Length of the additional information string.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-695">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-695">Return Values</span></span>

 - <span data-ttu-id="6cf9c-696">**NX_SUCCESS** (0x00) ha inviato una risposta server</span><span class="sxs-lookup"><span data-stu-id="6cf9c-696">**NX_SUCCESS** (0x00) Successfully sent Server response</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-697">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-697">Allowed From</span></span>

<span data-ttu-id="6cf9c-698">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-698">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-699">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-699">Example</span></span>

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                        CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
               (strcmp(resource, "/test.htm") == 0))
    {

        /* In this example, we will complete the GET processing with
           a resource not found response. */
     nx_http_server_callback_response_send_extended(
                                             server_ptr,
                      "HTTP/1.0 404 ", 12,
                      "NetX HTTP Server unable to find  
                       file: ", 38, resource, 9);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_content_get"></a><span data-ttu-id="6cf9c-700">nx_http_server_content_get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-700">nx_http_server_content_get</span></span>

<span data-ttu-id="6cf9c-701">Ottenere contenuto dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="6cf9c-701">Get content from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-702">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-702">Prototype</span></span>

```c
UINT nx_http_server_content_get(NX_HTTP_SERVER *server_ptr,
                                NX_PACKET *packet_ptr,
                                ULONG byte_offset,
                                CHAR *destination_ptr,
                                UINT destination_size,
                                UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="6cf9c-703">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-703">Description</span></span>

<span data-ttu-id="6cf9c-704">Questo servizio tenta di recuperare la quantità specificata di contenuto dalla richiesta client HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-704">This service attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="6cf9c-705">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-705">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create*).</span></span>

<span data-ttu-id="6cf9c-706">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-706">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-707">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_server_content_get_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-707">Developers are encouraged to migrate to *nx_http_server_content_get_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-708">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-708">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-709">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-709">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-710">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-710">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="6cf9c-711">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-711">Note that this packet must not be released by the request notify callback.</span></span>
 - <span data-ttu-id="6cf9c-712">**byte_offset** Numero di byte da sfalsare nell'area del contenuto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-712">**byte_offset** Number of bytes to offset into the content area.</span></span>
 - <span data-ttu-id="6cf9c-713">**destination_ptr** Puntatore all'area di destinazione per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-713">**destination_ptr** Pointer to the destination area for the content.</span></span>
 - <span data-ttu-id="6cf9c-714">**destination_size** Numero massimo di byte disponibili nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-714">**destination_size** Maximum number of bytes available in the destination area.</span></span>
 - <span data-ttu-id="6cf9c-715">**actual_size** Puntatore alla variabile di destinazione che verrà impostata sulle dimensioni effettive del contenuto copiato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-715">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-716">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-716">Return Values</span></span>

 - <span data-ttu-id="6cf9c-717">**NX_SUCCESS** (0x00) il contenuto del server http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-717">**NX_SUCCESS** (0x00) Successful HTTP Server content get</span></span>
 - <span data-ttu-id="6cf9c-718">Errore interno del server HTTP **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-718">**NX_HTTP_ERROR** (0xE0) HTTP Server internal error</span></span>
 - <span data-ttu-id="6cf9c-719">**NX_HTTP_DATA_END** (0xE7) fine del contenuto della richiesta</span><span class="sxs-lookup"><span data-stu-id="6cf9c-719">**NX_HTTP_DATA_END** (0xE7) End of request content</span></span>
 - <span data-ttu-id="6cf9c-720">TIMEOUT del server HTTP **NX_HTTP_TIMEOUT** (0xE1) per il recupero del pacchetto di contenuto successivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-720">**NX_HTTP_TIMEOUT** (0xE1) HTTP Server timeout in getting next packet of content</span></span>
 - <span data-ttu-id="6cf9c-721">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-721">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-722">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-722">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-723">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-723">Allowed From</span></span>

<span data-ttu-id="6cf9c-724">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-724">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-725">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-725">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, retrieve up to 100 bytes of content starting at offset
   0. */
status =  nx_http_server_content_get(&my_server, packet_ptr,
                      0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
   request content. */
```

## <a name="nx_http_server_content_get_extended"></a><span data-ttu-id="6cf9c-726">nx_http_server_content_get_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-726">nx_http_server_content_get_extended</span></span>

<span data-ttu-id="6cf9c-727">Ottieni contenuto dalla richiesta/supporta la lunghezza del contenuto di lunghezza zero</span><span class="sxs-lookup"><span data-stu-id="6cf9c-727">Get content from the request/supports zero length Content Length</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-728">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-728">Prototype</span></span>

```c
UINT nx_http_server_content_get_extended(NX_HTTP_SERVER *server_ptr,
                                         NX_PACKET *packet_ptr,
                                         ULONG byte_offset,
                                         CHAR *destination_ptr,
                                         UINT destination_size,
                                         UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="6cf9c-729">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-729">Description</span></span>

<span data-ttu-id="6cf9c-730">Questo servizio è quasi identico a *nx_http_server_content_get ()* . tenta di recuperare la quantità specificata di contenuto dalla richiesta del client HTTP post o put.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-730">This service is almost identical to *nx_http_server_content_get();* it attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="6cf9c-731">Tuttavia, gestisce le richieste con lunghezza del contenuto pari a zero (' Empty request ') come richiesta valida.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-731">However it handles requests with Content Length of zero value (‘empty request’) as a valid request.</span></span> <span data-ttu-id="6cf9c-732">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-732">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="6cf9c-733">Questo servizio sostituisce *nx_http_server_content_get ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-733">This service replaces *nx_http_server_content_get()*.</span></span> <span data-ttu-id="6cf9c-734">Questa versione richiede che il chiamante fornisca informazioni di lunghezza aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-734">This version requires caller to supply additional length information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-735">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-735">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-736">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-736">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-737">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-737">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="6cf9c-738">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-738">Note that this packet must not be released by the request notify callback.</span></span>
 - <span data-ttu-id="6cf9c-739">**byte_offset** Numero di byte da sfalsare nell'area del contenuto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-739">**byte_offset** Number of bytes to offset into the content area.</span></span>
 - <span data-ttu-id="6cf9c-740">**destination_ptr** Puntatore all'area di destinazione per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-740">**destination_ptr** Pointer to the destination area for the content.</span></span>
 - <span data-ttu-id="6cf9c-741">**destination_size** Numero massimo di byte disponibili nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-741">**destination_size** Maximum number of bytes available in the destination area.</span></span>
 - <span data-ttu-id="6cf9c-742">**actual_size** Puntatore alla variabile di destinazione che verrà impostata sulle dimensioni effettive del contenuto copiato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-742">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-743">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-743">Return Values</span></span>

 - <span data-ttu-id="6cf9c-744">**NX_SUCCESS** (0x00) contenuto http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-744">**NX_SUCCESS** (0x00) Successful HTTP content get</span></span>
 - <span data-ttu-id="6cf9c-745">Errore interno del server HTTP **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-745">**NX_HTTP_ERROR** (0xE0) HTTP Server internal error</span></span>
 - <span data-ttu-id="6cf9c-746">**NX_HTTP_DATA_END** (0xE7) fine del contenuto della richiesta</span><span class="sxs-lookup"><span data-stu-id="6cf9c-746">**NX_HTTP_DATA_END** (0xE7) End of request content</span></span>
 - <span data-ttu-id="6cf9c-747">TIMEOUT del server HTTP **NX_HTTP_TIMEOUT** (0xE1) nel recupero del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-747">**NX_HTTP_TIMEOUT** (0xE1) HTTP Server timeout in getting next packet</span></span>
 - <span data-ttu-id="6cf9c-748">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-748">NX_PTR_ERROR (0x07) Invalid  pointer input</span></span>
 - <span data-ttu-id="6cf9c-749">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-749">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-750">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-750">Allowed From</span></span>

<span data-ttu-id="6cf9c-751">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-751">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-752">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-752">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, retrieve up to 100 bytes of content starting at offset
   0. */
status =  nx_http_server_content_get_extended(&my_server, packet_ptr,
                               0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
   request content. */
```

## <a name="nx_http_server_content_length_get"></a><span data-ttu-id="6cf9c-753">nx_http_server_content_length_get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-753">nx_http_server_content_length_get</span></span>

<span data-ttu-id="6cf9c-754">Ottenere la lunghezza del contenuto nella richiesta</span><span class="sxs-lookup"><span data-stu-id="6cf9c-754">Get length of content in the request</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-755">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-755">Prototype</span></span>

```c
UINT nx_http_server_content_length_get(NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="6cf9c-756">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-756">Description</span></span>

<span data-ttu-id="6cf9c-757">Questo servizio tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-757">This service attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="6cf9c-758">Se non è presente alcun contenuto HTTP, questa routine restituisce un valore pari a zero.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-758">If there is no HTTP content, this routine returns a value of zero.</span></span> <span data-ttu-id="6cf9c-759">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-759">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="6cf9c-760">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-760">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-761">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_server_content_length_get_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-761">Developers are encouraged to migrate to *nx_http_server_content_length_get_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-762">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-762">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-763">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-763">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="6cf9c-764">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-764">Note that this packet must not be released by the request notify callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-765">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-765">Return Values</span></span>

 - <span data-ttu-id="6cf9c-766">**lunghezza contenuto** In errore, viene restituito un valore pari a zero</span><span class="sxs-lookup"><span data-stu-id="6cf9c-766">**content length** On error, a value of zero is returned</span></span>  

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-767">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-767">Allowed From</span></span>

<span data-ttu-id="6cf9c-768">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-768">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-769">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-769">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, get the content length of the HTTP Client request. */
length =  nx_http_server_content_length_get(packet_ptr);

/* The “length” variable now contains the length of the HTTP Client
   request content area. */
```

## <a name="nx_http_server_content_length_get_extended"></a><span data-ttu-id="6cf9c-770">nx_http_server_content_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-770">nx_http_server_content_length_get_extended</span></span>

<span data-ttu-id="6cf9c-771">Ottenere la lunghezza del contenuto nella richiesta/supporta la lunghezza del contenuto pari a zero valore</span><span class="sxs-lookup"><span data-stu-id="6cf9c-771">Get length of content in the request/supports Content Length of zero value</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-772">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-772">Prototype</span></span>

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                                UINT *content_length);
```

### <a name="description"></a><span data-ttu-id="6cf9c-773">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-773">Description</span></span>

<span data-ttu-id="6cf9c-774">Questo servizio è simile a *nx_http_server_content_length_get;* tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-774">This service is similar to *nx_http_server_content_length_get;* attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="6cf9c-775">Tuttavia, il valore restituito indica lo stato di completamento corretto e il valore di lunghezza effettivo viene restituito nel puntatore di input ```content_length``` .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-775">However, the return value indicates successful completion status, and the actual length value is returned in the input pointer ```content_length```.</span></span> <span data-ttu-id="6cf9c-776">Se non è presente alcun contenuto HTTP/lunghezza contenuto = 0, questa routine restituisce ancora uno stato di completamento corretto e il puntatore di input content_length punta a una lunghezza valida (zero).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-776">If there is no HTTP content/Content Length = 0, this routine still returns a successful completion status and the content_length input pointer points to a valid length (zero).</span></span> <span data-ttu-id="6cf9c-777">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-777">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create*).</span></span>

<span data-ttu-id="6cf9c-778">Questo servizio sostituisce *nx_http_server_content_length_get ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-778">This service replaces *nx_http_server_content_length_get()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-779">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-779">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-780">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-780">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="6cf9c-781">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-781">Note that this packet must not be released by the request notify callback.</span></span>
 - <span data-ttu-id="6cf9c-782">**CONTENT_LENGTH** Puntatore al valore recuperato dal campo lunghezza contenuto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-782">**content_length** Pointer to value retrieved from Content Length field</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-783">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-783">Return Values</span></span>

 - <span data-ttu-id="6cf9c-784">**NX_SUCCESS** (0x00) contenuto server riuscito Get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-784">**NX_SUCCESS** (0x00) Successful Server content get</span></span>
 - <span data-ttu-id="6cf9c-785">Formato dell'intestazione HTTP **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) non corretto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-785">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Improper HTTP header format</span></span>
 - <span data-ttu-id="6cf9c-786">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-786">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-787">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-787">Allowed From</span></span>

<span data-ttu-id="6cf9c-788">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-788">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-789">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-789">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, get the content length of the HTTP Client request. */
ULONG content_length;

status =  nx_http_server_content_length_get_extended(packet_ptr, &content_length);

/* If the “status” variable indicates successful completion, the“length” variable
   contains the length of the HTTP Client request content area. */
```

## <a name="nx_http_server_create"></a><span data-ttu-id="6cf9c-790">nx_http_server_create</span><span class="sxs-lookup"><span data-stu-id="6cf9c-790">nx_http_server_create</span></span>

<span data-ttu-id="6cf9c-791">Creare un'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-791">Create an HTTP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-792">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-792">Prototype</span></span>

```c
UINT nx_http_server_create(NX_HTTP_SERVER *http_server_ptr,
      CHAR *http_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr,
      VOID *stack_ptr, ULONG stack_size, NX_PACKET_POOL *pool_ptr,
      UINT (*authentication_check)(NX_HTTP_SERVER *server_ptr,
            UINT request_type, CHAR *resource, CHAR **name,
            CHAR **password, CHAR **realm),
      UINT (*request_notify)(NX_HTTP_SERVER *server_ptr,
            UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

### <a name="description"></a><span data-ttu-id="6cf9c-793">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-793">Description</span></span>

<span data-ttu-id="6cf9c-794">Questo servizio crea un'istanza del server HTTP, che viene eseguita nel contesto del proprio thread ThreadX.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-794">This service creates an HTTP Server instance, which runs in the context of its own ThreadX thread.</span></span> <span data-ttu-id="6cf9c-795">Le routine di callback dell'applicazione *authentication_check* e request_notify facoltative forniscono al software dell'applicazione il controllo sulle operazioni di base del server http.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-795">The optional *authentication_check* and request_notify application callback routines give the application software control over the basic operations of the HTTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-796">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-796">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-797">**http_server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-797">**http_server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="6cf9c-798">**http_server_name** Puntatore al nome del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-798">**http_server_name** Pointer to HTTP Server’s name.</span></span>
 - <span data-ttu-id="6cf9c-799">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-799">**ip_ptr** Pointer to previously created IP instance.</span></span>
 - <span data-ttu-id="6cf9c-800">**media_ptr** Puntatore a un'istanza del supporto FileX creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-800">**media_ptr** Pointer to previously created FileX media instance.</span></span>
 - <span data-ttu-id="6cf9c-801">**stack_ptr** Puntatore all'area dello stack di thread del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-801">**stack_ptr** Pointer to HTTP Server thread stack area.</span></span>
 - <span data-ttu-id="6cf9c-802">**stack_size** Puntatore alla dimensione dello stack del thread del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-802">**stack_size** Pointer to HTTP Server thread stack size.</span></span>
 - <span data-ttu-id="6cf9c-803">**authentication_check** Puntatore a funzione per la routine di controllo dell'autenticazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-803">**authentication_check** Function pointer to application’s authentication checking routine.</span></span> <span data-ttu-id="6cf9c-804">Se specificato, questa routine viene chiamata per ogni richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-804">If specified, this routine is called for each HTTP Client request.</span></span> <span data-ttu-id="6cf9c-805">Se questo parametro è NULL, non verrà eseguita alcuna autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-805">If this parameter is NULL, no authentication will be performed.</span></span>
 - <span data-ttu-id="6cf9c-806">**request_notify** Puntatore della funzione alla routine di notifica della richiesta dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-806">**request_notify** Function pointer to application’s request notify routine.</span></span> <span data-ttu-id="6cf9c-807">Se specificato, questa routine viene chiamata prima dell'elaborazione del server HTTP della richiesta.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-807">If specified, this routine is called prior to the HTTP server processing of the request.</span></span> <span data-ttu-id="6cf9c-808">Questo consente di reindirizzare il nome della risorsa o i campi all'interno di una risorsa da aggiornare prima di completare la richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-808">This allows the resource name to be redirected or fields within a resource to be updated prior to completing the HTTP Client request.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-809">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-809">Return Values</span></span>

 - <span data-ttu-id="6cf9c-810">Creazione del server HTTP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-810">**NX_SUCCESS** (0x00) Successful HTTP Server create.</span></span>
 - <span data-ttu-id="6cf9c-811">NX_PTR_ERROR (0x07) server HTTP, IP, supporti, stack o puntatore al pool di pacchetti non validi.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-811">NX_PTR_ERROR (0x07) Invalid HTTP Server, IP, media, stack, or packet pool pointer.</span></span>
 - <span data-ttu-id="6cf9c-812">Il payload del pacchetto di NX_HTTP_POOL_ERROR (0xE9) del pool non è sufficiente per contenere la richiesta HTTP completa.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-812">NX_HTTP_POOL_ERROR (0xE9) Packet payload of pool is not large enough to contain complete HTTP request.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-813">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-813">Allowed From</span></span>

<span data-ttu-id="6cf9c-814">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-814">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-815">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-815">Example</span></span>

```c
/* Create an HTTP Server instance called “my_server.”  */
status =  nx_http_server_create(&my_server, “my server”, &ip_0, &ram_disk,
              stack_ptr, stack_size, &pool_0,
              my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_http_server_delete"></a><span data-ttu-id="6cf9c-816">nx_http_server_delete</span><span class="sxs-lookup"><span data-stu-id="6cf9c-816">nx_http_server_delete</span></span>

<span data-ttu-id="6cf9c-817">Eliminare un'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-817">Delete an HTTP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-818">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-818">Prototype</span></span>

```c
UINT nx_http_server_delete(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="6cf9c-819">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-819">Description</span></span>

<span data-ttu-id="6cf9c-820">Questo servizio Elimina un'istanza del server HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-820">This service deletes a previously created HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-821">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-821">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-822">**http_server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-822">**http_server_ptr** Pointer to HTTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-823">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-823">Return Values</span></span>

 - <span data-ttu-id="6cf9c-824">Eliminazione del server HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-824">**NX_SUCCESS** (0x00) Successful HTTP Server delete</span></span>
 - <span data-ttu-id="6cf9c-825">NX_PTR_ERROR (0x07) puntatore al server HTTP non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-825">NX_PTR_ERROR (0x07) Invalid HTTP Server pointer</span></span>
 - <span data-ttu-id="6cf9c-826">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-826">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-827">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-827">Allowed From</span></span>

<span data-ttu-id="6cf9c-828">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-828">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-829">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-829">Example</span></span>

```c
/* Delete the HTTP Server instance called “my_server.”  */
status =  nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a><span data-ttu-id="6cf9c-830">nx_http_server_get_entity_content</span><span class="sxs-lookup"><span data-stu-id="6cf9c-830">nx_http_server_get_entity_content</span></span>

<span data-ttu-id="6cf9c-831">Recuperare il percorso e la lunghezza dei dati dell'entità</span><span class="sxs-lookup"><span data-stu-id="6cf9c-831">Retrieve the location and length of entity data</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-832">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-832">Prototype</span></span>

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_pptr,
                                       ULONG *available_offset,
                                       ULONG *available_length);
```

### <a name="description"></a><span data-ttu-id="6cf9c-833">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-833">Description</span></span>

<span data-ttu-id="6cf9c-834">Questo servizio determina la posizione dell'inizio dei dati all'interno dell'entità multiparte corrente nei messaggi client ricevuti e la lunghezza dei dati che non includono la stringa di limite.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-834">This service determines the location of the start of data within the current multipart entity in the received Client messages, and the length of data not including the boundary string.</span></span> <span data-ttu-id="6cf9c-835">Il server HTTP interno aggiorna i propri offset in modo che questa funzione possa essere richiamata nello stesso datagramma client per i messaggi con più entità.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-835">Internally HTTP server updates its own offsets so that this function can be called again on the same Client datagram for messages with multiple entities.</span></span> <span data-ttu-id="6cf9c-836">Il puntatore al pacchetto viene aggiornato al pacchetto successivo in cui il messaggio del client è un datagramma con più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-836">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-837">Per usare questo servizio NX_HTTP_MULTIPART_ENABLE necessario abilitarlo.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-837">NX_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span>

<span data-ttu-id="6cf9c-838">Per ulteriori informazioni, vedere [*nx_http_server_get_entity_header*](#nx_http_server_get_entity_header) .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-838">See [*nx_http_server_get_entity_header*](#nx_http_server_get_entity_header) for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-839">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-839">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-840">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-840">**server_ptr** Pointer to HTTP Server</span></span>
 - <span data-ttu-id="6cf9c-841">**packet_pptr** Puntatore alla posizione del puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-841">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="6cf9c-842">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-842">Note that the application should not release this packet.</span></span>
 - <span data-ttu-id="6cf9c-843">**available_offset** Puntatore all'offset dei dati dell'entità dal puntatore a prependi del pacchetto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-843">**available_offset** Pointer to offset of entity data from the packet prepend pointer</span></span>
 - <span data-ttu-id="6cf9c-844">**available_length** Puntatore alla lunghezza dei dati dell'entità</span><span class="sxs-lookup"><span data-stu-id="6cf9c-844">**available_length** Pointer to length of entity data</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-845">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-845">Return Values</span></span>

 - <span data-ttu-id="6cf9c-846">**NX_SUCCESS** (0x00) ha recuperato correttamente le dimensioni e la posizione del contenuto dell'entità</span><span class="sxs-lookup"><span data-stu-id="6cf9c-846">**NX_SUCCESS** (0x00) Successfully retrieved size and location of entity content</span></span>
 - <span data-ttu-id="6cf9c-847">Il contenuto **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) per i marcatori multipart interni del server http è già stato trovato</span><span class="sxs-lookup"><span data-stu-id="6cf9c-847">**NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) Content for the HTTP server  internal multipart markers is already found</span></span>
 - <span data-ttu-id="6cf9c-848">Errore HTTP interno NX_HTTP_ERROR (0xE0)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-848">NX_HTTP_ERROR (0xE0) Internal HTTP error</span></span>
 - <span data-ttu-id="6cf9c-849">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-849">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-850">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-850">Allowed From</span></span>

<span data-ttu-id="6cf9c-851">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-851">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-852">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-852">Example</span></span>

```c
NX_HTTP_SERVER my_server;

UINT        offset, length;
NX_PACKET  *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
   the entity header to determine details about the multipart data. If
   successful, it then calls this service to get the location of entity data: */

status =  nx_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
&length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
   entity data. */
```

## <a name="nx_http_server_get_entity_header"></a><span data-ttu-id="6cf9c-853">nx_http_server_get_entity_header</span><span class="sxs-lookup"><span data-stu-id="6cf9c-853">nx_http_server_get_entity_header</span></span>

<span data-ttu-id="6cf9c-854">Recupera il contenuto dell'intestazione dell'entità</span><span class="sxs-lookup"><span data-stu-id="6cf9c-854">Retrieve the contents of entity header</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-855">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-855">Prototype</span></span>

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      UCHAR *entity_header_buffer,
                                      ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="6cf9c-856">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-856">Description</span></span>

<span data-ttu-id="6cf9c-857">Questo servizio recupera l'intestazione dell'entità nel buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-857">This service retrieves the entity header into the specified buffer.</span></span> <span data-ttu-id="6cf9c-858">Il server HTTP interno aggiorna i propri puntatori per individuare la prossima entità multipart in un datagramma client con più intestazioni di entità.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-858">Internally HTTP Server updates its own pointers to locate the next multipart entity in a Client datagram with multiple entity headers.</span></span> <span data-ttu-id="6cf9c-859">Il puntatore al pacchetto viene aggiornato al pacchetto successivo in cui il messaggio del client è un datagramma con più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-859">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-860">Per usare questo servizio NX_HTTP_MULTIPART_ENABLE necessario abilitarlo.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-860">NX_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-861">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-861">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-862">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-862">**server_ptr** Pointer to HTTP Server</span></span>
 - <span data-ttu-id="6cf9c-863">**packet_pptr** Puntatore alla posizione del puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-863">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="6cf9c-864">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-864">Note that the application should not release this packet.</span></span>
 - <span data-ttu-id="6cf9c-865">**entity_header_buffer** Puntatore alla posizione in cui archiviare l'intestazione dell'entità</span><span class="sxs-lookup"><span data-stu-id="6cf9c-865">**entity_header_buffer** Pointer to location to store entity header</span></span>
 - <span data-ttu-id="6cf9c-866">**BUFFER_SIZE** Dimensioni del buffer di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-866">**buffer_size** Size of input buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-867">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-867">Return Values</span></span>

 - <span data-ttu-id="6cf9c-868">**NX_SUCCESS** (0x00) ha recuperato correttamente l'intestazione dell'entità</span><span class="sxs-lookup"><span data-stu-id="6cf9c-868">**NX_SUCCESS** (0x00) Successfully retrieved entity heade</span></span>
 - <span data-ttu-id="6cf9c-869">Campo di intestazione dell'entità **NX_HTTP_NOT_FOUND** **(0xE6)** non trovato</span><span class="sxs-lookup"><span data-stu-id="6cf9c-869">**NX_HTTP_NOT_FOUND** **(0xE6)** Entity header field not found</span></span>
 - <span data-ttu-id="6cf9c-870">Tempo di **NX_HTTP_TIMEOUT** **(0xE1)** scaduto per la ricezione del pacchetto successivo per il messaggio client Multipack</span><span class="sxs-lookup"><span data-stu-id="6cf9c-870">**NX_HTTP_TIMEOUT** **(0xE1)** Time expired to receive next packet for multipacket client message</span></span>
 - <span data-ttu-id="6cf9c-871">Errore HTTP interno NX_HTTP_ERROR (0xE0)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-871">NX_HTTP_ERROR (0xE0) Internal HTTP error</span></span>
 - <span data-ttu-id="6cf9c-872">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-872">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-873">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-873">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-874">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-874">Allowed From</span></span>

<span data-ttu-id="6cf9c-875">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-875">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-876">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-876">Example</span></span>

```c
/* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                              CHAR *resource, NX_PACKET *packet_ptr)
      {

        NX_PACKET   *sresp_packet_ptr;
        UINT        offset, length;
        NX_PACKET   *response_pkt;
        UCHAR       buffer[1440];

        /* Process multipart data. */
        if(request_type == NX_HTTP_SERVER_POST_REQUEST)
        {

       /* Get the content header. */
       while(nx_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
                                         sizeof(buffer)) == NX_SUCCESS)
   {

      /* Header obtained successfully. Get the content data location. */
      while(nx_http_server_get_entity_content(server_ptr, &packet_ptr, &offset,
                                              &length) == NX_SUCCESS)
      {
           /* Write content data to buffer. */
           nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                                         &length);
           buffer[length] = 0;
      }

    }

    /* Generate HTTP header. */
    status = nx_http_server_callback_generate_response_header(server_ptr,
                         &response_pkt, NX_HTTP_STATUS_OK, 800, "text/html",
                         "Server: NetXDuo HTTP 5.3\r\n");

    if(status == NX_SUCCESS)
    {
        if(nx_http_server_callback_packet_send(server_ptr, response_pkt) !=
  NX_SUCCESS)
 {
                nx_packet_release(response_pkt);
     }
    }


}
else
{
    /* Indicate we have not processed the response to client yet.*/
    return(NX_SUCCESS);
}

/* Indicate the response to client is transmitted. */
return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_gmt_callback_set"></a><span data-ttu-id="6cf9c-877">nx_http_server_gmt_callback_set</span><span class="sxs-lookup"><span data-stu-id="6cf9c-877">nx_http_server_gmt_callback_set</span></span>

<span data-ttu-id="6cf9c-878">Impostare il callback per ottenere la data e l'ora GMT</span><span class="sxs-lookup"><span data-stu-id="6cf9c-878">Set the callback to obtain GMT date and time</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-879">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-879">Prototype</span></span>

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

### <a name="description"></a><span data-ttu-id="6cf9c-880">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-880">Description</span></span>

<span data-ttu-id="6cf9c-881">Questo servizio imposta il callback per ottenere la data e l'ora GMT con un server HTTP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-881">This service sets the callback to obtain GMT date and time with a previously created HTTP server.</span></span> <span data-ttu-id="6cf9c-882">Questo servizio viene richiamato con il server HTTP che sta creando un'intestazione nel server HTTP risposte al client.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-882">This service is invoked with the HTTP server is creating a header in HTTP server responses to the Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-883">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-883">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-884">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-884">**server_ptr** Pointer to HTTP Server</span></span>
 - <span data-ttu-id="6cf9c-885">**gmt_getv** Puntatore al callback GMT</span><span class="sxs-lookup"><span data-stu-id="6cf9c-885">**gmt_getv** Pointer to GMT callback</span></span>
 - <span data-ttu-id="6cf9c-886">**DATEV** Puntatore alla data recuperata</span><span class="sxs-lookup"><span data-stu-id="6cf9c-886">**datev** Pointer to the date retrieved</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-887">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-887">Return Values</span></span>

 - <span data-ttu-id="6cf9c-888">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-888">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="6cf9c-889">NX_PTR_ERROR (0x07) il puntatore al pacchetto o al parametro non è valido.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-889">NX_PTR_ERROR (0x07)  Invalid packet or parameter pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-890">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-890">Allowed From</span></span>

<span data-ttu-id="6cf9c-891">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-891">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-892">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-892">Example</span></span>

```c
NX_HTTP_SERVER my_server;

VOID get_gmt(NX_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the GMT
   retrieve callback: */

status =  nx_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
   response header date. */
```

## <a name="nx_http_server_invalid_userpassword_notify_set"></a><span data-ttu-id="6cf9c-893">nx_http_server_invalid_userpassword_notify_set</span><span class="sxs-lookup"><span data-stu-id="6cf9c-893">nx_http_server_invalid_userpassword_notify_set</span></span>

<span data-ttu-id="6cf9c-894">Impostare il callback su per gestire l'utente o la password non valida</span><span class="sxs-lookup"><span data-stu-id="6cf9c-894">Set the callback to to handle invalid user/password</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-895">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-895">Prototype</span></span>

```c
UINT nx_http_server_invalid_userpassword_notify_set(
            NX_HTTP_SERVER *http_server_ptr,
            UINT (*invalid_username_password_callback)
                        (CHAR *resource,
                        NXD_ADDRESS *client_address,
                        UINT request_type));
```

### <a name="description"></a><span data-ttu-id="6cf9c-896">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-896">Description</span></span>

<span data-ttu-id="6cf9c-897">Questo servizio imposta il callback richiamato quando viene ricevuto un nome utente e una password non validi in una richiesta GET, put o Delete del client, mediante l'autenticazione digest o di base.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-897">This service sets the callback invoked when an invalid username and password is received in a Client get, put or delete request, either by digest or basic authentication.</span></span> <span data-ttu-id="6cf9c-898">Il server HTTP deve essere creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-898">The HTTP server must be previously created.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-899">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-899">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-900">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-900">**server_ptr** Pointer to HTTP Server</span></span>
 - <span data-ttu-id="6cf9c-901">**invalid_username_password_callback** Puntatore a callback utente/pass non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-901">**invalid_username_password_callback** Pointer to invalid user/pass callback</span></span>
 - <span data-ttu-id="6cf9c-902">**risorsa** di Puntatore alla risorsa specificata dal client</span><span class="sxs-lookup"><span data-stu-id="6cf9c-902">**resource** Pointer to the resource specified by the client</span></span>
 - <span data-ttu-id="6cf9c-903">**CLIENT_ADDRESS** Puntatore all'indirizzo client.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-903">**client_address** Pointer to client address.</span></span> <span data-ttu-id="6cf9c-904">Può essere IPv4 o IPv6</span><span class="sxs-lookup"><span data-stu-id="6cf9c-904">Can be IPv4 or IPv6</span></span>
 - <span data-ttu-id="6cf9c-905">**request_type** Indica il tipo di richiesta client.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-905">**request_type** Indicates client request type.</span></span> <span data-ttu-id="6cf9c-906">Può essere:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-906">May be:</span></span>
    - <span data-ttu-id="6cf9c-907">NX_HTTP_SERVER_GET_REQUEST</span><span class="sxs-lookup"><span data-stu-id="6cf9c-907">NX_HTTP_SERVER_GET_REQUEST</span></span>
    - <span data-ttu-id="6cf9c-908">NX_HTTP_SERVER_POST_REQUEST</span><span class="sxs-lookup"><span data-stu-id="6cf9c-908">NX_HTTP_SERVER_POST_REQUEST</span></span>
    - <span data-ttu-id="6cf9c-909">NX_HTTP_SERVER_HEAD_REQUEST</span><span class="sxs-lookup"><span data-stu-id="6cf9c-909">NX_HTTP_SERVER_HEAD_REQUEST</span></span>
    - <span data-ttu-id="6cf9c-910">NX_HTTP_SERVER_PUT_REQUEST</span><span class="sxs-lookup"><span data-stu-id="6cf9c-910">NX_HTTP_SERVER_PUT_REQUEST</span></span>
    - <span data-ttu-id="6cf9c-911">NX_HTTP_SERVER_DELETE_REQUEST</span><span class="sxs-lookup"><span data-stu-id="6cf9c-911">NX_HTTP_SERVER_DELETE_REQUEST</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-912">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-912">Return Values</span></span>

 - <span data-ttu-id="6cf9c-913">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-913">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="6cf9c-914">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-914">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-915">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-915">Allowed From</span></span>

<span data-ttu-id="6cf9c-916">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-916">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-917">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-917">Example</span></span>

```c
NX_HTTP_SERVER my_server;
VOID invalid_username_password_callback (NX_ CHAR *resource,
                                         NXD_ADDRESS *client_address,
                                         UINT   request_type);

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the invalid
   username password callback: */

status =  nx_http_server_gmt_callback_set(&my_server,
                                          invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
   will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_http_server_mime_maps_additional_set"></a><span data-ttu-id="6cf9c-918">nx_http_server_mime_maps_additional_set</span><span class="sxs-lookup"><span data-stu-id="6cf9c-918">nx_http_server_mime_maps_additional_set</span></span>

<span data-ttu-id="6cf9c-919">Impostare mappe MIME aggiuntive per HTML</span><span class="sxs-lookup"><span data-stu-id="6cf9c-919">Set additional MIME maps for HTML</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-920">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-920">Prototype</span></span>

```c
UINT nx_http_server_mime_maps_additional_set(
                        NX_HTTP_SERVER *server_ptr,
                        NX_HTTP_SERVER_MIME_MAP *mime_maps,
                        UINT mime_maps_num);
```

### <a name="description"></a><span data-ttu-id="6cf9c-921">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-921">Description</span></span>

<span data-ttu-id="6cf9c-922">Questo servizio consente allo sviluppatore di applicazioni HTTP di aggiungere altri tipi MIME dai tipi MIME predefiniti forniti dal server HTTP NetX Duo (vedere *nx_http_server_get_type* per l'elenco dei tipi definiti).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-922">This service allows the HTTP application developer to add additional MIME types from the default MIME types supplied by NetX Duo HTTP Server (see *nx_http_server_get_type* for list of defined types).</span></span>

<span data-ttu-id="6cf9c-923">Quando viene ricevuta una richiesta client, ad esempio una richiesta GET, il server HTTP analizza il tipo di file richiesto dall'intestazione HTTP usando il set di mappe MIME aggiuntivo e, se non viene trovata alcuna corrispondenza, Cerca una corrispondenza nella mappa MIME predefinita del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-923">When a client request is received, e.g. a GET request, HTTP server parses the requested file type from the HTTP header using preferentially the additional MIME map set and if no match if found, it looks for a match in the default MIME map of the HTTP server.</span></span> <span data-ttu-id="6cf9c-924">Se non viene trovata alcuna corrispondenza, il valore predefinito del tipo MIME è "text/plain".</span><span class="sxs-lookup"><span data-stu-id="6cf9c-924">If no match is found, the MIME type defaults to “text/plain”.</span></span>

<span data-ttu-id="6cf9c-925">Se la funzione request Notify è registrata con il server HTTP, il callback della richiesta di notifica può chiamare *nx_http_server_type_retrieve ()* per analizzare il tipo di file.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-925">If the request notify function is registered with the HTTP server, the request notify callback can call *nx_http_server_type_retrieve()* to parse the file type.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-926">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-926">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-927">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-927">**server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="6cf9c-928">**mime_maps** Puntatore a una matrice di mappa MIME</span><span class="sxs-lookup"><span data-stu-id="6cf9c-928">**mime_maps** Pointer to a MIME map array</span></span>
 - <span data-ttu-id="6cf9c-929">**mime_map_num** Numero di mappe MIME nella matrice</span><span class="sxs-lookup"><span data-stu-id="6cf9c-929">**mime_map_num** Number of MIME maps in array</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-930">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-930">Return Values</span></span>

 - <span data-ttu-id="6cf9c-931">Set di mappe MIME del server HTTP con **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="6cf9c-931">**NX_SUCCESS** (0x00) Successful HTTP Server MIME map set</span></span>
 - <span data-ttu-id="6cf9c-932">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-932">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-933">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-933">Allowed From</span></span>

<span data-ttu-id="6cf9c-934">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-934">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-935">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-935">Example</span></span>

```c
/* my_server is an NX_HTTP_SERVER previously created. */

NX_HTTP_SERVER_MIME_MAP my_mime_maps [2];

static NX_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc",      "yourtype/abc"},
    {"xyz",      "mytype/xyz"},
};

status =  nx_http_server_mime_maps_additional_set(&my_server,
                                                  &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP  
  server MIME map set.” */
```

## <a name="nx_http_server_packet_content_find"></a><span data-ttu-id="6cf9c-936">nx_http_server_packet_content_find</span><span class="sxs-lookup"><span data-stu-id="6cf9c-936">nx_http_server_packet_content_find</span></span>

<span data-ttu-id="6cf9c-937">Estrarre la lunghezza del contenuto e impostare il puntatore all'inizio dei dati</span><span class="sxs-lookup"><span data-stu-id="6cf9c-937">Extract content length and set pointer to start of data</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-938">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-938">Prototype</span></span>

```c
UINT nx_http_server_packet_content_find(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET **packet_ptr,
                                        UINT *content_length);
```

### <a name="description"></a><span data-ttu-id="6cf9c-939">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-939">Description</span></span>

<span data-ttu-id="6cf9c-940">Questo servizio estrae la lunghezza del contenuto dall'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-940">This service extracts the content length from the HTTP header.</span></span> <span data-ttu-id="6cf9c-941">Aggiorna inoltre il pacchetto fornito come indicato di seguito: il puntatore del pacchetto Prepend (inizio della posizione del buffer dei pacchetti in cui scrivere) viene impostato sul contenuto HTTP (dati) appena passata l'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-941">It also  updates the supplied packet as follows: the packet prepend pointer (start of location of packet buffer to write to) is set to the HTTP content (data) just passed the HTTP header.</span></span>

<span data-ttu-id="6cf9c-942">Se l'inizio del contenuto non viene trovato nel pacchetto corrente, la funzione attende la ricezione del pacchetto successivo utilizzando l'opzione NX_HTTP_SERVER_TIMEOUT_RECEIVE wait.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-942">If the beginning of content is not found in the current packet, the function waits for the next packet to be received using the NX_HTTP_SERVER_TIMEOUT_RECEIVE wait option.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-943">Questo metodo non deve essere chiamato prima di chiamare *nx_http_server_get_entity_header* perché modifica il puntatore anteposto dopo l'intestazione dell'entità.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-943">This should not be called before calling *nx_http_server_get_entity_header* because it modifies the prepend pointer past the entity header.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-944">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-944">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-945">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-945">**server_ptr** Pointer to HTTP server instance</span></span>
 - <span data-ttu-id="6cf9c-946">**packet_ptr** Puntatore al puntatore del pacchetto per la restituzione del pacchetto con puntatore anteposto aggiornato</span><span class="sxs-lookup"><span data-stu-id="6cf9c-946">**packet_ptr** Pointer to packet pointer for returning the packet with updated prepend pointer</span></span>
 - <span data-ttu-id="6cf9c-947">**CONTENT_LENGTH** Puntatore a Estratto ```content_length```</span><span class="sxs-lookup"><span data-stu-id="6cf9c-947">**content_length** Pointer to extracted ```content_length```</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-948">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-948">Return Values</span></span>

 - <span data-ttu-id="6cf9c-949">È stata trovata la lunghezza del contenuto HTTP **NX_SUCCESS** (0x00) e l'aggiornamento del pacchetto è riuscito</span><span class="sxs-lookup"><span data-stu-id="6cf9c-949">**NX_SUCCESS** (0x00) HTTP content length found and packet successfully updated</span></span>
 - <span data-ttu-id="6cf9c-950">Tempo di **NX_HTTP_TIMEOUT** (0xE1) scaduto in attesa del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-950">**NX_HTTP_TIMEOUT** (0xE1) Time expired waiting on next packet</span></span>
 - <span data-ttu-id="6cf9c-951">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-951">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-952">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-952">Allowed From</span></span>

<span data-ttu-id="6cf9c-953">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-953">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-954">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-954">Example</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
The server has received a Client request packet, recv_packet_ptr, and the packet
content find service is called from the request notify callback function
registered with the HTTP server. */

UINT content_length;

status =  nx_http_server_packet_content_find(server_ptr, recv_packet_ptr,
                                             &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
   and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_http_server_packet_get"></a><span data-ttu-id="6cf9c-955">nx_http_server_packet_get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-955">nx_http_server_packet_get</span></span>

<span data-ttu-id="6cf9c-956">Ricevere il pacchetto HTTP successivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-956">Receive the next HTTP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-957">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-957">Prototype</span></span>

```c
UINT nx_http_server_packet_get(NX_HTTP_SERVER *server_ptr,
                              NX_PACKET **packet_ptr);
```

### <a name="description"></a><span data-ttu-id="6cf9c-958">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-958">Description</span></span>

<span data-ttu-id="6cf9c-959">Questo servizio restituisce il pacchetto successivo ricevuto sul socket del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-959">This service returns the next packet received on the HTTP server socket.</span></span> <span data-ttu-id="6cf9c-960">L'opzione Attendi per la ricezione di un pacchetto è NX_HTTP_SERVER_TIMEOUT_RECEIVE.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-960">The wait option to receive a packet is NX_HTTP_SERVER_TIMEOUT_RECEIVE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-961">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-961">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-962">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-962">**server_ptr** Pointer to HTTP server instance</span></span>
 - <span data-ttu-id="6cf9c-963">**packet_ptr** Puntatore al pacchetto ricevuto</span><span class="sxs-lookup"><span data-stu-id="6cf9c-963">**packet_ptr** Pointer to received packet</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-964">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-964">Return Values</span></span>

 - <span data-ttu-id="6cf9c-965">**NX_SUCCESS** (0x00) ha ricevuto il pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-965">**NX_SUCCESS** (0x00) Successfully received next packet</span></span>
 - <span data-ttu-id="6cf9c-966">Tempo di **NX_HTTP_TIMEOUT** (0xE1) scaduto in attesa del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-966">**NX_HTTP_TIMEOUT** (0xE1) Time expired waiting on next packet</span></span>
 - <span data-ttu-id="6cf9c-967">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-967">NX_PTR_ERROR (0x07)  Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-968">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-968">Allowed From</span></span>

<span data-ttu-id="6cf9c-969">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-969">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-970">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-970">Example</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started. */

UINT content_length;
NX_PACKET *recv_packet_ptr;

status =  nx_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_http_server_param_get"></a><span data-ttu-id="6cf9c-971">nx_http_server_param_get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-971">nx_http_server_param_get</span></span>

<span data-ttu-id="6cf9c-972">Ottenere il parametro dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="6cf9c-972">Get parameter from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-973">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-973">Prototype</span></span>

```c
UINT nx_http_server_param_get(NX_PACKET *packet_ptr,
                              UINT param_number, CHAR *param_ptr,
                              UINT max_param_size);
```

### <a name="description"></a><span data-ttu-id="6cf9c-974">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-974">Description</span></span>

<span data-ttu-id="6cf9c-975">Questo servizio tenta di recuperare il parametro URL HTTP specificato nel pacchetto di richiesta fornito.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-975">This service attempts to retrieve the specified HTTP URL parameter in the supplied request packet.</span></span> <span data-ttu-id="6cf9c-976">Se il parametro HTTP richiesto non è presente, questa routine restituisce lo stato NX_HTTP_NOT_FOUND.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-976">If the requested HTTP parameter is not present,  this routine returns a status of NX_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="6cf9c-977">Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-977">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-978">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-978">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-979">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-979">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="6cf9c-980">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-980">Note that the application should not release this packet.</span></span>
 - <span data-ttu-id="6cf9c-981">**param_number** Numero logico del parametro a partire da zero, da sinistra a destra nell'elenco dei parametri.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-981">**param_number** Logical number of the parameter starting at zero, from left to right in the parameter list.</span></span>
 - <span data-ttu-id="6cf9c-982">**param_ptr** Area di destinazione per copiare il parametro.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-982">**param_ptr** Destination area to copy the parameter.</span></span>
 - <span data-ttu-id="6cf9c-983">**max_param_size** Dimensioni massime dell'area di destinazione del parametro.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-983">**max_param_size** Maximum size of the parameter destination area.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-984">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-984">Return Values</span></span>

 - <span data-ttu-id="6cf9c-985">**NX_SUCCESS** (0x00) parametro Server http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-985">**NX_SUCCESS** (0x00) Successful HTTP Server parameter get</span></span>
 - <span data-ttu-id="6cf9c-986">Il parametro specificato **NX_HTTP_NOT_FOUND** (0xE6) non è stato trovato</span><span class="sxs-lookup"><span data-stu-id="6cf9c-986">**NX_HTTP_NOT_FOUND** (0xE6) Specified parameter not found</span></span>
 - <span data-ttu-id="6cf9c-987">Il parametro della richiesta **NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xf3) non è terminato correttamente</span><span class="sxs-lookup"><span data-stu-id="6cf9c-987">**NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) Request parameter not properly terminated</span></span>
 - <span data-ttu-id="6cf9c-988">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-988">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-989">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-989">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-990">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-990">Allowed From</span></span>

<span data-ttu-id="6cf9c-991">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-991">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-992">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-992">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, get the first parameter of the HTTP Client request. */

status =  nx_http_server_param_get(request_packet_ptr, 0, param_destination,
               30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
   in “param_destination.” */
```

## <a name="nx_http_server_query_get"></a><span data-ttu-id="6cf9c-993">nx_http_server_query_get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-993">nx_http_server_query_get</span></span>

<span data-ttu-id="6cf9c-994">Ottenere una query dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="6cf9c-994">Get query from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-995">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-995">Prototype</span></span>

```c
UINT nx_http_server_query_get(NX_PACKET *packet_ptr, UINT query_number,
                   CHAR *query_ptr, UINT max_query_size);
```

### <a name="description"></a><span data-ttu-id="6cf9c-996">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-996">Description</span></span>

<span data-ttu-id="6cf9c-997">Questo servizio tenta di recuperare la query URL HTTP specificata nel pacchetto di richiesta fornito.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-997">This service attempts to retrieve the specified HTTP URL query in the supplied request packet.</span></span> <span data-ttu-id="6cf9c-998">Se la query HTTP richiesta non è presente, questa routine restituisce lo stato NX_HTTP_NOT_FOUND.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-998">If the requested HTTP query is not present,  this routine returns a status of NX_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="6cf9c-999">Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create*).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-999">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-1000">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1000">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-1001">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1001">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="6cf9c-1002">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1002">Note that the application should not release this packet.</span></span>
 - <span data-ttu-id="6cf9c-1003">**query_number** Numero logico del parametro a partire da zero, da sinistra a destra nell'elenco di query.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1003">**query_number** Logical number of the parameter starting at zero, from left to right in the query list.</span></span>
 - <span data-ttu-id="6cf9c-1004">**query_ptr** Area di destinazione per la copia della query.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1004">**query_ptr** Destination area to copy the query.</span></span>
 - <span data-ttu-id="6cf9c-1005">**max_query_size** Dimensioni massime dell'area di destinazione della query.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1005">**max_query_size** Maximum size of the query destination area.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-1006">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1006">Return Values</span></span>

 - <span data-ttu-id="6cf9c-1007">**NX_SUCCESS** (0x00) query del server http riuscita Get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1007">**NX_SUCCESS** (0x00) Successful HTTP Server query get</span></span>
 - <span data-ttu-id="6cf9c-1008">Dimensioni della query di **NX_HTTP_FAILED** (0xe2) troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1008">**NX_HTTP_FAILED** (0xE2) Query size too small.</span></span>
 - <span data-ttu-id="6cf9c-1009">Impossibile trovare la query specificata **NX_HTTP_NOT_FOUND** (0xE6)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1009">**NX_HTTP_NOT_FOUND** (0xE6) Specified query not found</span></span>
 - <span data-ttu-id="6cf9c-1010">**NX_HTTP_NO_QUERY_PARSED** (0XF2) nessuna query nella richiesta client</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1010">**NX_HTTP_NO_QUERY_PARSED** (0xF2) No query in Client request</span></span>
 - <span data-ttu-id="6cf9c-1011">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1011">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-1012">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1012">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-1013">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1013">Allowed From</span></span>

<span data-ttu-id="6cf9c-1014">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1014">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-1015">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1015">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, get the first query of the HTTP Client request. */
status =  nx_http_server_query_get(request_packet_ptr, 0, query_destination,
                30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
   in “query_destination.” */
```

## <a name="nx_http_server_start"></a><span data-ttu-id="6cf9c-1016">nx_http_server_start</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1016">nx_http_server_start</span></span>

<span data-ttu-id="6cf9c-1017">Avviare il server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1017">Start the HTTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-1018">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1018">Prototype</span></span>

```c
UINT nx_http_server_start(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="6cf9c-1019">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1019">Description</span></span>

<span data-ttu-id="6cf9c-1020">Questo servizio avvia l'istanza del server HTTP create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1020">This service starts the previously create HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-1021">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1021">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-1022">**http_server_ptr** Puntatore all'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1022">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-1023">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1023">Return Values</span></span>

 - <span data-ttu-id="6cf9c-1024">Avvio del server **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1024">**NX_SUCCESS** (0x00) Successful Server start</span></span>
 - <span data-ttu-id="6cf9c-1025">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1025">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-1026">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1026">Allowed From</span></span>

<span data-ttu-id="6cf9c-1027">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1027">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-1028">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1028">Example</span></span>

```c
/* Start the HTTP Server instance “my_server.”  */
status =  nx_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_http_server_stop"></a><span data-ttu-id="6cf9c-1029">nx_http_server_stop</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1029">nx_http_server_stop</span></span>

<span data-ttu-id="6cf9c-1030">Arrestare il server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1030">Stop the HTTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-1031">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1031">Prototype</span></span>

```c
UINT nx_http_server_stop(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="6cf9c-1032">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1032">Description</span></span>

<span data-ttu-id="6cf9c-1033">Questo servizio arresta l'istanza del server HTTP create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1033">This service stops the previously create HTTP Server instance.</span></span> <span data-ttu-id="6cf9c-1034">Questa routine deve essere chiamata prima di eliminare un'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1034">This routine should be called prior to deleting an HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-1035">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1035">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-1036">**http_server_ptr** Puntatore all'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1036">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-1037">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1037">Return Values</span></span>

 - <span data-ttu-id="6cf9c-1038">Arresto server riuscito **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1038">**NX_SUCCESS** (0x00) Successful Server stop</span></span>
 - <span data-ttu-id="6cf9c-1039">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1039">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-1040">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1040">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-1041">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1041">Allowed From</span></span>

<span data-ttu-id="6cf9c-1042">Thread</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1042">Threads</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-1043">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1043">Example</span></span>

```c
/* Stop the HTTP Server instance “my_server.”  */
status =  nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a><span data-ttu-id="6cf9c-1044">nx_http_server_type_get</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1044">nx_http_server_type_get</span></span>

<span data-ttu-id="6cf9c-1045">Estrai il tipo di file dalla richiesta HTTP client</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1045">Extract file type from Client HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-1046">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1046">Prototype</span></span>

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                             CHAR *name, CHAR *http_type_string);
```

### <a name="description"></a><span data-ttu-id="6cf9c-1047">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1047">Description</span></span>

> [!NOTE]
> <span data-ttu-id="6cf9c-1048">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1048">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-1049">Gli utenti sono invitati a usare il servizio *nx_http_server_type_retrieve ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1049">Users are encouraged to use the service *nx_http_server_type_retrieve()*.</span></span>

<span data-ttu-id="6cf9c-1050">Questo servizio estrae il tipo di richiesta HTTP nel buffer http_type_string e la sua lunghezza nel valore restituito dal nome del buffer di input, in genere l'URL.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1050">This service extracts the HTTP request type in the buffer http_type_string and its length in the return value from the input buffer name, usually the URL.</span></span> <span data-ttu-id="6cf9c-1051">Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene impostato il tipo "text/plain".</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1051">If no MIME map is found, it defaults to the “text/plain” type.</span></span> <span data-ttu-id="6cf9c-1052">In caso contrario, confronta il tipo Estratto con le mappe MIME predefinite del server HTTP per una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1052">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="6cf9c-1053">Le mappe MIME predefinite nel server HTTP NetX Duo sono:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1053">The default MIME maps in NetX Duo HTTP Server are:</span></span>

 - <span data-ttu-id="6cf9c-1054">testo **HTML** /HTML</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1054">**html** text/html</span></span>
 - <span data-ttu-id="6cf9c-1055">testo **htm** /HTML</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1055">**htm** text/html</span></span>
 - <span data-ttu-id="6cf9c-1056">testo **txt** /normale</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1056">**txt** text/plain</span></span>
 - <span data-ttu-id="6cf9c-1057">immagine **gif** /gif</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1057">**gif** image/gif</span></span>
 - <span data-ttu-id="6cf9c-1058">immagine **jpg** /JPEG</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1058">**jpg** image/jpeg</span></span>
 - <span data-ttu-id="6cf9c-1059">icona immagine **ico** /x</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1059">**ico** image/x-icon</span></span>

<span data-ttu-id="6cf9c-1060">Se specificato, verrà inoltre cercato un set definito dall'utente di mappe MIME aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1060">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="6cf9c-1061">Per ulteriori informazioni sulle mappe definite dall'utente, vedere *nx_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1061">See *nx_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="6cf9c-1062">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1062">This service is deprecated.</span></span> <span data-ttu-id="6cf9c-1063">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_server_type_get_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1063">Developers are encouraged to migrate to *nx_http_server_type_get_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-1064">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1064">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-1065">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1065">**http_server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="6cf9c-1066">**puntatore al nome** del buffer da cercare</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1066">**name Pointer** to buffer to search</span></span>
 - <span data-ttu-id="6cf9c-1067">**http_type_string** (puntatore al tipo HTML Estratto)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1067">**http_type_string** (Pointer to extracted HTML type)</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-1068">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1068">Return Values</span></span>

 - <span data-ttu-id="6cf9c-1069">**Lunghezza della stringa in byte** Il valore diverso da zero è success.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1069">**Length of string in bytes** Non zero value is success.</span></span> <span data-ttu-id="6cf9c-1070">Zero indica un errore.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1070">Zero indicates error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-1071">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1071">Allowed From</span></span>

<span data-ttu-id="6cf9c-1072">Applicazione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1072">Application</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-1073">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1073">Example</span></span>

```c
/* my_server is a previously created HTTP server, which starts accepting client
   requests when nx_http_server_start is called*/

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
    string_length =  nx_http_server_type_get(&my_server_ptr,
                my_server.nx_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
```

## <a name="nx_http_server_type_get_extended"></a><span data-ttu-id="6cf9c-1074">nx_http_server_type_get_extended</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1074">nx_http_server_type_get_extended</span></span>

<span data-ttu-id="6cf9c-1075">Estrai il tipo di file dalla richiesta HTTP client</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1075">Extract file type from Client HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-1076">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1076">Prototype</span></span>

```c
UINT nx_http_server_type_get_extended(
                                    NX_HTTP_SERVER *http_server_ptr,
                                    CHAR *name, CHAR *http_type_string,
                                    UINT http_type_string_max_size);
```

### <a name="description"></a><span data-ttu-id="6cf9c-1077">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1077">Description</span></span>

<span data-ttu-id="6cf9c-1078">Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la sua lunghezza nel valore restituito dal *nome* del buffer di input, in genere l'URL.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1078">This service extracts the HTTP request type in the buffer *http_type_string* and its length in the return value from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="6cf9c-1079">Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene impostato il tipo "text/plain".</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1079">If no MIME map is found, it defaults to the “text/plain” type.</span></span> <span data-ttu-id="6cf9c-1080">In caso contrario, confronta il tipo Estratto con le mappe MIME predefinite del server HTTP per una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1080">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="6cf9c-1081">Le mappe MIME predefinite nel server HTTP NetX Duo sono:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1081">The default MIME maps in NetX Duo HTTP Server are:</span></span>

 - <span data-ttu-id="6cf9c-1082">testo **HTML** /HTML</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1082">**html** text/html</span></span>
 - <span data-ttu-id="6cf9c-1083">testo **htm** /HTML</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1083">**htm** text/html</span></span>
 - <span data-ttu-id="6cf9c-1084">testo **txt** /normale</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1084">**txt** text/plain</span></span>
 - <span data-ttu-id="6cf9c-1085">immagine **gif** /gif</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1085">**gif** image/gif</span></span>
 - <span data-ttu-id="6cf9c-1086">immagine **jpg** /JPEG</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1086">**jpg** image/jpeg</span></span>
 - <span data-ttu-id="6cf9c-1087">icona immagine **ico** /x</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1087">**ico** image/x-icon</span></span>

<span data-ttu-id="6cf9c-1088">Se specificato, verrà inoltre cercato un set definito dall'utente di mappe MIME aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1088">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="6cf9c-1089">Per ulteriori informazioni sulle mappe definite dall'utente, vedere *nx_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1089">See *nx_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="6cf9c-1090">Questo servizio sostituisce *nx_http_server_type_get ()*.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1090">This service replaces *nx_http_server_type_get()*.</span></span> <span data-ttu-id="6cf9c-1091">Questa versione fornisce informazioni aggiuntive sulla lunghezza.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1091">This version supplies additional length information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-1092">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1092">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-1093">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1093">**http_server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="6cf9c-1094">**nome** Puntatore al buffer in cui eseguire la ricerca</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1094">**name** Pointer to buffer to search</span></span>
 - <span data-ttu-id="6cf9c-1095">**name_length** Lunghezza del buffer da cercare</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1095">**name_length** Length of buffer to search</span></span>
 - <span data-ttu-id="6cf9c-1096">**http_type_string** (puntatore al tipo HTML Estratto)</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1096">**http_type_string** (Pointer to extracted HTML type)</span></span>
 - <span data-ttu-id="6cf9c-1097">**http_type_string_max_size** Dimensioni del buffer di http_type_string</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1097">**http_type_string_max_size** Size of the http_type_string buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-1098">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1098">Return Values</span></span>

 - <span data-ttu-id="6cf9c-1099">**Lunghezza della stringa in byte** Il valore diverso da zero è success.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1099">**Length of string in bytes** Non zero value is success.</span></span> <span data-ttu-id="6cf9c-1100">Zero indica un errore.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1100">Zero indicates error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-1101">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1101">Allowed From</span></span>

<span data-ttu-id="6cf9c-1102">Applicazione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1102">Application</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-1103">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1103">Example</span></span>

```c
/* my_server is a previously created HTTP server, which starts accepting client
   requests when nx_http_server_start is called*/

CHAR temp_string[20];
UINT string_length;

/* Get the length of request resource. */
    if (_nx_utility_string_length_check(
                    my_server.nx_http_server_request_resource, &resource_length,
                    sizeof(my_server.nx_http_server_request_resource) - 1))
           {
               return;
           }

/* Extract the HTTP type. */
    string_length =  nx_http_server_type_get_extended(&my_server,
               my_server.nx_http_server_request_resource, resource_length,
               temp_string, sizeof(temp_string));

/* If string_length is non zero, the HTTP string is extracted. */
```

<span data-ttu-id="6cf9c-1104">Per un esempio più dettagliato, vedere la descrizione per [*nx_http_server_callback_generate_response_header*](#nx_http_server_callback_generate_response_header).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1104">For a more detailed example, see the description for [*nx_http_server_callback_generate_response_header*](#nx_http_server_callback_generate_response_header).</span></span>

## <a name="nx_http_server_digest_authenticate_notify_set"></a><span data-ttu-id="6cf9c-1105">nx_http_server_digest_authenticate_notify_set</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1105">nx_http_server_digest_authenticate_notify_set</span></span>

<span data-ttu-id="6cf9c-1106">Imposta funzione di callback autenticazione digest</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1106">Set digest authenticate callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-1107">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1107">Prototype</span></span>

```c
UINT nx_http_server_digest_authenticate_notify_set(
       NX_HTTP_SERVER *http_server_ptr,
       UINT (*digest_authenticate_callback)(NX_HTTP_SERVER *server_ptr,
                                            CHAR *name_ptr,
                                            CHAR *realm_ptr,
                                            CHAR *password_ptr,
                                            CHAR *method,
                                            CHAR *authorization_uri,
                                            CHAR *authorization_nc,
                                            CHAR *authorization_cnonce
                                           ));
```

### <a name="description"></a><span data-ttu-id="6cf9c-1108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1108">Description</span></span>

<span data-ttu-id="6cf9c-1109">Questo servizio imposta il callback richiamato quando viene eseguita l'autenticazione del digest.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1109">This service sets the callback invoked when digest authenticate is performed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-1110">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1110">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-1111">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1111">**http_server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="6cf9c-1112">**digest_authenticate_callback** Puntatore al callback di autenticazione del digest</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1112">**digest_authenticate_callback** Pointer to digest authenticate callback</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-1113">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1113">Return Values</span></span>

 - <span data-ttu-id="6cf9c-1114">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1114">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="6cf9c-1115">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1115">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="6cf9c-1116">Autenticazione del digest NX_NOT_SUPPORTED (0x4B) non abilitata</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1116">NX_NOT_SUPPORTED (0x4B) Digest authenticate not enabled</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-1117">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1117">Allowed From</span></span>

<span data-ttu-id="6cf9c-1118">Applicazione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1118">Application</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-1119">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1119">Example</span></span>

```c
UINT digest_authenticate_callback(NX_HTTP_SERVER *server_ptr, CHAR *name_ptr,
                                  CHAR *realm_ptr, CHAR *password_ptr, CHAR *method,
                                  CHAR *authorization_uri, CHAR *authorization_nc,
                                  CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the digest authenticate callback: */

status =  nx_http_server_digest_authenticate_notify_set (&my_server,
    digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
   will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_http_server_authentication_check_set"></a><span data-ttu-id="6cf9c-1120">nx_http_server_authentication_check_set</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1120">nx_http_server_authentication_check_set</span></span>

<span data-ttu-id="6cf9c-1121">Imposta la funzione di callback per il controllo dell'autenticazione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1121">Set authentication checking callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="6cf9c-1122">Prototipo</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1122">Prototype</span></span>

```c
UINT nx_http_server_authentication_check_set(
       NX_HTTP_SERVER *http_server_ptr,
       UINT (*authentication_check_extended)(
                                            NX_HTTP_SERVER *server_ptr,
                                            UINT request_type,
                                            CHAR *resource,
                                            CHAR **name,
                                            UINT *name_length,
                                            CHAR **password,
                                            UINT *password_length,
                                            CHAR **realm,
                                            UINT *realm_length
                                            ));
```

### <a name="description"></a><span data-ttu-id="6cf9c-1123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1123">Description</span></span>

<span data-ttu-id="6cf9c-1124">Questo servizio imposta la funzione di callback del controllo dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1124">This service sets the callback function of authentication checking.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="6cf9c-1125">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1125">Input Parameters</span></span>

 - <span data-ttu-id="6cf9c-1126">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1126">**http_server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="6cf9c-1127">**authentication_check_extended** Puntatore al controllo di autenticazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1127">**authentication_check_extended** Pointer to application’s authentication checking</span></span>

### <a name="return-values"></a><span data-ttu-id="6cf9c-1128">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1128">Return Values</span></span>

 - <span data-ttu-id="6cf9c-1129">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1129">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="6cf9c-1130">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1130">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="6cf9c-1131">Consentito da</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1131">Allowed From</span></span>

<span data-ttu-id="6cf9c-1132">Applicazione</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1132">Application</span></span>

### <a name="example"></a><span data-ttu-id="6cf9c-1133">Esempio</span><span class="sxs-lookup"><span data-stu-id="6cf9c-1133">Example</span></span>

```c
static UINT  authentication_check_extended(NX_HTTP_SERVER *server_ptr,
                                           UINT request_type, CHAR *resource,
                                           CHAR **name, UINT *name_length,
                                           CHAR **password, UINT *password_length,
                                           CHAR **realm, UINT *realm_length)
{

    /* Just use a simple name, password, and realm for all
       requests and resources. */
    *name =     "name";
    *password = "password";
    *realm =    "NetX Duo HTTP demo";
    *name_length = 4;
    *password_length = 8;
    *realm_length = 18;

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the
   authentication checking callback: */

nx_http_server_authentication_check_set (&my_server,
                                         authentication_check_extended);
```
