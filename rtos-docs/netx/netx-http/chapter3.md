---
title: Capitolo 3-Descrizione dei servizi HTTP NetX
description: Questo capitolo contiene una descrizione di tutti i servizi HTTP NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c58d0e3d7eca86816a9d656bf2b92a896ffb96fc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822616"
---
# <a name="chapter-3---description-of-netx-http-services"></a><span data-ttu-id="9b120-103">Capitolo 3-Descrizione dei servizi HTTP NetX</span><span class="sxs-lookup"><span data-stu-id="9b120-103">Chapter 3 - Description of NetX HTTP services</span></span>

<span data-ttu-id="9b120-104">Questo capitolo contiene una descrizione di tutti i servizi HTTP NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="9b120-104">This chapter contains a description of all NetX HTTP services (listed below) in alphabetical order.</span></span>

<span data-ttu-id="9b120-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="9b120-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

<span data-ttu-id="9b120-106">**Servizi client HTTP:**</span><span class="sxs-lookup"><span data-stu-id="9b120-106">**HTTP Client services:**</span></span>

- <span data-ttu-id="9b120-107">nx_http_client_create *creare un'istanza del client http*</span><span class="sxs-lookup"><span data-stu-id="9b120-107">nx_http_client_create *Create an HTTP Client Instance*</span></span>
- <span data-ttu-id="9b120-108">nx_http_client_delete *eliminare un'istanza client http*</span><span class="sxs-lookup"><span data-stu-id="9b120-108">nx_http_client_delete *Delete an HTTP Client instance*</span></span>
- <span data-ttu-id="9b120-109">nx_http_client_get_start *avviare una richiesta HTTP Get*</span><span class="sxs-lookup"><span data-stu-id="9b120-109">nx_http_client_get_start *Start an HTTP GET request*</span></span>
- <span data-ttu-id="9b120-110">nx_http_client_get_start_extended *avviare una richiesta HTTP Get*</span><span class="sxs-lookup"><span data-stu-id="9b120-110">nx_http_client_get_start_extended *Start an HTTP GET request*</span></span>
- <span data-ttu-id="9b120-111">nx_http_client_get_packet *ottenere un pacchetto di dati di risorse successivo*</span><span class="sxs-lookup"><span data-stu-id="9b120-111">nx_http_client_get_packet *Get next resource data packet*</span></span>
- <span data-ttu-id="9b120-112">nx_http_client_put_start *avviare una richiesta HTTP PUT*</span><span class="sxs-lookup"><span data-stu-id="9b120-112">nx_http_client_put_start *Start an HTTP PUT request*</span></span>
- <span data-ttu-id="9b120-113">nx_http_client_put_start_extended *avviare una richiesta HTTP PUT*</span><span class="sxs-lookup"><span data-stu-id="9b120-113">nx_http_client_put_start_extended *Start an HTTP PUT request*</span></span>
- <span data-ttu-id="9b120-114">nx_http_client_put_packet *inviare il pacchetto di dati di risorse successivo*</span><span class="sxs-lookup"><span data-stu-id="9b120-114">nx_http_client_put_packet *Send next resource data packet*</span></span>
- <span data-ttu-id="9b120-115">*nx_http_client_set_connect_port* *modificare la porta per la connessione al server http*</span><span class="sxs-lookup"><span data-stu-id="9b120-115">*nx_http_client_set_connect_port* *Change the port to connect to the HTTP Server*</span></span>

<span data-ttu-id="9b120-116">**Servizi server HTTP:**</span><span class="sxs-lookup"><span data-stu-id="9b120-116">**HTTP Server services:**</span></span>

- <span data-ttu-id="9b120-117">nx_http_server_cache_info_callback_set *impostare il callback per recuperare l'età e la data dell'Ultima modifica dell'URL specificato*</span><span class="sxs-lookup"><span data-stu-id="9b120-117">nx_http_server_cache_info_callback_set *Set callback to retrieve age and last modified date of specified URL*</span></span>
- <span data-ttu-id="9b120-118">nx_http_server_callback_data_send *inviare dati http da una funzione di callback*</span><span class="sxs-lookup"><span data-stu-id="9b120-118">nx_http_server_callback_data_send *Send HTTP data from callback function*</span></span>
- <span data-ttu-id="9b120-119">nx_http_server_callback_generate_response_header *creare l'intestazione della risposta nelle funzioni di callback*</span><span class="sxs-lookup"><span data-stu-id="9b120-119">nx_http_server_callback_generate_response_header *Create response header in callback functions*</span></span>
- <span data-ttu-id="9b120-120">nx_http_server_callback_generate_response_header_extended *creare l'intestazione della risposta nelle funzioni di callback*</span><span class="sxs-lookup"><span data-stu-id="9b120-120">nx_http_server_callback_generate_response_header_extended *Create response header in callback functions*</span></span>
- <span data-ttu-id="9b120-121">nx_http_server_callback_packet_send *inviare un pacchetto http da un callback http*</span><span class="sxs-lookup"><span data-stu-id="9b120-121">nx_http_server_callback_packet_send *Send an HTTP packet from an HTTP callback*</span></span>
- <span data-ttu-id="9b120-122">nx_http_server_callback_response_send *inviare risposta dalla funzione di callback*</span><span class="sxs-lookup"><span data-stu-id="9b120-122">nx_http_server_callback_response_send *Send response from callback function*</span></span>
- <span data-ttu-id="9b120-123">nx_http_server_callback_response_send_extended *inviare risposta dalla funzione di callback*</span><span class="sxs-lookup"><span data-stu-id="9b120-123">nx_http_server_callback_response_send_extended *Send response from callback function*</span></span>
- <span data-ttu-id="9b120-124">nx_http_server_content_get *ottenere contenuto dalla richiesta*</span><span class="sxs-lookup"><span data-stu-id="9b120-124">nx_http_server_content_get *Get content from the request*</span></span>
- <span data-ttu-id="9b120-125">nx_http_server_content_get_extended *ottenere contenuto dalla richiesta; supporta le richieste vuote (lunghezza del contenuto pari a zero)*</span><span class="sxs-lookup"><span data-stu-id="9b120-125">nx_http_server_content_get_extended *Get content from the request; supports empty (zero Content Length) requests*</span></span>
- <span data-ttu-id="9b120-126">nx_http_server_content_length_get *ottenere la lunghezza del contenuto nella richiesta*</span><span class="sxs-lookup"><span data-stu-id="9b120-126">nx_http_server_content_length_get *Get length of content in the request*</span></span>
- <span data-ttu-id="9b120-127">nx_http_server_content_length_get_extended *ottenere la lunghezza del contenuto nella richiesta; supporta le richieste vuote (lunghezza del contenuto pari a zero)*</span><span class="sxs-lookup"><span data-stu-id="9b120-127">nx_http_server_content_length_get_extended *Get length of content in the request; supports empty (zero Content Length) requests*</span></span>
- <span data-ttu-id="9b120-128">nx_http_server_create *creare un'istanza del server http*</span><span class="sxs-lookup"><span data-stu-id="9b120-128">nx_http_server_create *Create an HTTP Server instance*</span></span>
- <span data-ttu-id="9b120-129">nx_http_server_delete *eliminare un'istanza del server http*</span><span class="sxs-lookup"><span data-stu-id="9b120-129">nx_http_server_delete *Delete an HTTP Server instance*</span></span>
- <span data-ttu-id="9b120-130">nx_http_server_get_entity_content *la dimensione e la posizione del contenuto dell'entità nell'URL*</span><span class="sxs-lookup"><span data-stu-id="9b120-130">nx_http_server_get_entity_content *Return size and location of entity content in URL*</span></span>
- <span data-ttu-id="9b120-131">nx_http_server_get_entity_header l' *intestazione dell'entità Extract URL nel buffer specificato*</span><span class="sxs-lookup"><span data-stu-id="9b120-131">nx_http_server_get_entity_header *Extract URL entity header into specified buffer*</span></span>
- <span data-ttu-id="9b120-132">nx_http_server_gmt_callback_set *impostare il callback per recuperare la data e l'ora GMT*</span><span class="sxs-lookup"><span data-stu-id="9b120-132">nx_http_server_gmt_callback_set *Set callback to retrieve GMT date and time*</span></span>
- <span data-ttu-id="9b120-133">nx_http_server_invalid_userpassword_notify_set *impostare il callback quando in una richiesta client non è stato ricevuto un nome utente e una password non validi*</span><span class="sxs-lookup"><span data-stu-id="9b120-133">nx_http_server_invalid_userpassword_notify_set *Set callback for when invalid username and password is received in a Client request*</span></span>
- <span data-ttu-id="9b120-134">nx_http_server_mime_maps_additional_set *definire mappe MIME aggiuntive per HTML*</span><span class="sxs-lookup"><span data-stu-id="9b120-134">nx_http_server_mime_maps_additional_set *Define additional mime maps for HTML*</span></span>
- <span data-ttu-id="9b120-135">nx_http_server_packet_content_find *estrarre la lunghezza del contenuto nell'intestazione HTTP e impostare il puntatore all'inizio dei dati del contenuto*</span><span class="sxs-lookup"><span data-stu-id="9b120-135">nx_http_server_packet_content_find *Extract content length in HTTP header and set pointer to start of content data*</span></span>
- <span data-ttu-id="9b120-136">nx_http_server_packet_get *ricevere direttamente il pacchetto client*</span><span class="sxs-lookup"><span data-stu-id="9b120-136">nx_http_server_packet_get *Receive client packet directly*</span></span>
- <span data-ttu-id="9b120-137">nx_http_server_param_get *ottenere il parametro dalla richiesta*</span><span class="sxs-lookup"><span data-stu-id="9b120-137">nx_http_server_param_get *Get parameter from the request*</span></span>
- <span data-ttu-id="9b120-138">nx_http_server_query_get *ottenere una query dalla richiesta*</span><span class="sxs-lookup"><span data-stu-id="9b120-138">nx_http_server_query_get *Get query from the request*</span></span>
- <span data-ttu-id="9b120-139">nx_http_server_start *avviare il server http*</span><span class="sxs-lookup"><span data-stu-id="9b120-139">nx_http_server_start *Start the HTTP Server*</span></span>
- <span data-ttu-id="9b120-140">nx_http_server_stop *arrestare il server http*</span><span class="sxs-lookup"><span data-stu-id="9b120-140">nx_http_server_stop *Stop the HTTP Server*</span></span>
- <span data-ttu-id="9b120-141">nx_http_server_type_get *estrarre il tipo http, ad esempio text/plain dall'intestazione*</span><span class="sxs-lookup"><span data-stu-id="9b120-141">nx_http_server_type_get *Extract HTTP type e.g. text/plain from header*</span></span>
- <span data-ttu-id="9b120-142">nx_http_server_type_get_extended *estrarre il tipo http, ad esempio text/plain dall'intestazione*</span><span class="sxs-lookup"><span data-stu-id="9b120-142">nx_http_server_type_get_extended *Extract HTTP type e.g. text/plain from header*</span></span>
- <span data-ttu-id="9b120-143">nx_http_server_digest_authenticate_notify_set *impostare la funzione di callback autenticazione digest*</span><span class="sxs-lookup"><span data-stu-id="9b120-143">nx_http_server_digest_authenticate_notify_set *Set digest authenticate callback function*</span></span>
- <span data-ttu-id="9b120-144">nx_http_server_authentication_check_set *impostare la funzione di callback per il controllo dell'autenticazione*</span><span class="sxs-lookup"><span data-stu-id="9b120-144">nx_http_server_authentication_check_set *Set authentication checking callback function*</span></span>

## <a name="nx_http_client_create"></a><span data-ttu-id="9b120-145">nx_http_client_create</span><span class="sxs-lookup"><span data-stu-id="9b120-145">nx_http_client_create</span></span>

### <a name="create-an-http-client-instance"></a><span data-ttu-id="9b120-146">Creare un'istanza del client HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-146">Create an HTTP Client Instance</span></span>

<span data-ttu-id="9b120-147">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-147">**Prototype**</span></span>

```c
UINT nx_http_client_create(NX_HTTP_CLIENT *client_ptr,
                          CHAR *client_name, NX_IP *ip_ptr, 
                          NX_PACKET_POOL *pool_ptr,
                          ULONG window_size);
```

<span data-ttu-id="9b120-148">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-148">**Description**</span></span>

<span data-ttu-id="9b120-149">Questo servizio crea un'istanza del client HTTP nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="9b120-149">This service creates an HTTP Client instance on the specified IP instance.</span></span>

<span data-ttu-id="9b120-150">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-150">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-151">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-151">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="9b120-152">**client_name** Nome dell'istanza del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-152">**client_name** Name of HTTP Client instance.</span></span>
- <span data-ttu-id="9b120-153">**ip_ptr** Puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="9b120-153">**ip_ptr** Pointer to IP instance.</span></span>
- <span data-ttu-id="9b120-154">**pool_ptr** Puntatore al pool di pacchetti predefinito.</span><span class="sxs-lookup"><span data-stu-id="9b120-154">**pool_ptr** Pointer to default packet pool.</span></span> <span data-ttu-id="9b120-155">Si noti che i pacchetti in questo pool devono avere un payload sufficientemente grande per gestire l'intestazione della risposta completa.</span><span class="sxs-lookup"><span data-stu-id="9b120-155">Note that the packets in this pool must have a payload large enough to handle the complete response header.</span></span> <span data-ttu-id="9b120-156">Questa impostazione è definita da NX_HTTP_CLIENT_MIN_PACKET_SIZE in *nx_http_client. h*.</span><span class="sxs-lookup"><span data-stu-id="9b120-156">This is defined by NX_HTTP_CLIENT_MIN_PACKET_SIZE in *nx_http_client.h*.</span></span>
- <span data-ttu-id="9b120-157">**window_size** Dimensioni della finestra di ricezione del socket TCP del client.</span><span class="sxs-lookup"><span data-stu-id="9b120-157">**window_size** Size of the Client’s TCP socket receive window.</span></span>

<span data-ttu-id="9b120-158">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-158">**Return Values**</span></span>

- <span data-ttu-id="9b120-159">Creazione client HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="9b120-159">**NX_SUCCESS** (0x00) Successful HTTP Client create</span></span>
- <span data-ttu-id="9b120-160">NX_PTR_ERROR (0x16) puntatore HTTP, ip_ptr o pool di pacchetti non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-160">NX_PTR_ERROR (0x16) Invalid HTTP, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="9b120-161">Dimensioni del payload NX_HTTP_POOL_ERROR (0xE9) non valide nel pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="9b120-161">NX_HTTP_POOL_ERROR(0xE9) Invalid payload size in packet pool</span></span>

<span data-ttu-id="9b120-162">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-162">**Allowed From**</span></span>

<span data-ttu-id="9b120-163">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="9b120-163">Initialization, Threads</span></span>

<span data-ttu-id="9b120-164">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-164">**Example**</span></span>

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status = nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);
  
/* If status is NX_SUCCESS an HTTP Client instance was successfully  created. */
```

## <a name="nx_http_client_delete"></a><span data-ttu-id="9b120-165">nx_http_client_delete</span><span class="sxs-lookup"><span data-stu-id="9b120-165">nx_http_client_delete</span></span>

### <a name="delete-an-http-client-instance"></a><span data-ttu-id="9b120-166">Eliminare un'istanza client HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-166">Delete an HTTP Client Instance</span></span>

<span data-ttu-id="9b120-167">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-167">**Prototype**</span></span>

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

<span data-ttu-id="9b120-168">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-168">**Description**</span></span>

<span data-ttu-id="9b120-169">Questo servizio Elimina un'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-169">This service deletes a previously created HTTP Client instance.</span></span>

<span data-ttu-id="9b120-170">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-170">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-171">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-171">**client_ptr** Pointer to HTTP Client control block.</span></span>

<span data-ttu-id="9b120-172">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-172">**Return Values**</span></span>

- <span data-ttu-id="9b120-173">Eliminazione client HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="9b120-173">**NX_SUCCESS** (0x00) Successful HTTP Client delete</span></span>
- <span data-ttu-id="9b120-174">NX_PTR_ERROR (0x16) puntatore HTTP non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-174">NX_PTR_ERROR (0x16) Invalid HTTP pointer</span></span>
- <span data-ttu-id="9b120-175">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-175">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-176">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-176">**Allowed From**</span></span>

<span data-ttu-id="9b120-177">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-177">Threads</span></span>

<span data-ttu-id="9b120-178">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-178">**Example**</span></span>

```c
/* Delete the HTTP Client instance “my_client.” */
status = nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully  deleted. */
```

## <a name="nx_http_client_get_start"></a><span data-ttu-id="9b120-179">nx_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="9b120-179">nx_http_client_get_start</span></span>

### <a name="start-an-http-get-request"></a><span data-ttu-id="9b120-180">Avviare una richiesta HTTP GET</span><span class="sxs-lookup"><span data-stu-id="9b120-180">Start an HTTP GET request</span></span>

<span data-ttu-id="9b120-181">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-181">**Prototype**</span></span>

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
                             ULONG ip_address, CHAR *resource, CHAR *input_ptr,
                             UINT input_size, CHAR *username, CHAR *password,
                             ULONG wait_option);
```

<span data-ttu-id="9b120-182">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-182">**Description**</span></span>

<span data-ttu-id="9b120-183">Questo servizio tenta di ottenere la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-183">This service attempts to GET the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="9b120-184">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-184">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="9b120-185">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="9b120-185">Note that the resource string can refer to a local file e.g. “/index.htm” or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="9b120-186">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="9b120-186">This service is deprecated.</span></span> <span data-ttu-id="9b120-187">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_client_get_start_extended ()*</span><span class="sxs-lookup"><span data-stu-id="9b120-187">Developers are encouraged to migrate to *nx_http_client_get_start_extended()*</span></span>

<span data-ttu-id="9b120-188">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-188">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-189">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-189">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="9b120-190">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-190">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="9b120-191">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-191">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="9b120-192">**input_ptr** Puntatore a dati aggiuntivi per la richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="9b120-192">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="9b120-193">Questo indirizzo è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="9b120-193">This is optional.</span></span> <span data-ttu-id="9b120-194">Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="9b120-194">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
- <span data-ttu-id="9b120-195">**input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta input_ptr.</span><span class="sxs-lookup"><span data-stu-id="9b120-195">**input_size** Number of bytes in optional additional input pointed to by input_ptr.</span></span>
- <span data-ttu-id="9b120-196">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-196">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="9b120-197">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-197">**password** Pointer to optional password for authentication.</span></span><span data-ttu-id="9b120-198">
-\*\*WAIT_OPTION*\* Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-198">
-\*\*wait_option*\* Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="9b120-199">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="9b120-199">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9b120-200">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="9b120-200">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="9b120-201">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="9b120-201">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="9b120-202">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-202">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="9b120-203">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-203">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="9b120-204">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-204">**Return Values**</span></span>

- <span data-ttu-id="9b120-205">**NX_SUCCESS** (0x00) ha inviato il messaggio di avvio Get client http</span><span class="sxs-lookup"><span data-stu-id="9b120-205">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="9b120-206">Errore del client HTTP interno **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="9b120-206">**NX_HTTP_ERROR** (0xE0) Internal HTTP Client error</span></span>
- <span data-ttu-id="9b120-207">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="9b120-207">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="9b120-208">**NX_HTTP_FAILED** (0xe2) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="9b120-208">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="9b120-209">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="9b120-209">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or password.</span></span>
- <span data-ttu-id="9b120-210">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-210">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-211">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="9b120-211">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

<span data-ttu-id="9b120-212">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-212">**Allowed From**</span></span>

<span data-ttu-id="9b120-213">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-213">Threads</span></span>

<span data-ttu-id="9b120-214">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-214">**Example**</span></span>

```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                  NX_NULL, 0, “myname”, “mypassword”, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
far successful. The client must now call *nx_http_client_get_packet* multiple
times to retrieve the content associated with TEST.HTM. */

#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                  POST_MESSAGE, sizeof(POST_MESSAGE),
                                  “myname”, “mypassword”, 1000);
 
/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST 
request for TEST.HTM and successfully sent. */
```


## <a name="nx_http_client_get_start_extended"></a><span data-ttu-id="9b120-215">nx_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="9b120-215">nx_http_client_get_start_extended</span></span>

### <a name="start-an-http-get-request"></a><span data-ttu-id="9b120-216">Avviare una richiesta HTTP GET</span><span class="sxs-lookup"><span data-stu-id="9b120-216">Start an HTTP GET request</span></span>

<span data-ttu-id="9b120-217">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-217">**Prototype**</span></span>

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
     ULONG ip_address, CHAR *resource, UINT resource_length,
     CHAR *input_ptr, UINT input_size, CHAR *username,
     UINT username_length, CHAR *password, UINT password_length,
     ULONG wait_option);
```

<span data-ttu-id="9b120-218">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-218">**Description**</span></span>

<span data-ttu-id="9b120-219">Questo servizio tenta di ottenere la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-219">This service attempts to GET the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="9b120-220">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_http_client_get_packet* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-220">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="9b120-221">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="9b120-221">Note that the resource string can refer to a local file e.g. “/index.htm” or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="9b120-222">Questo servizio sostituisce *nx_http_client_get_start ()*.</span><span class="sxs-lookup"><span data-stu-id="9b120-222">This service replaces *nx_http_client_get_start()*.</span></span> <span data-ttu-id="9b120-223">È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="9b120-223">It requires caller to specify the length of the resource, username and password.</span></span>

<span data-ttu-id="9b120-224">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-224">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-225">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-225">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="9b120-226">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-226">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="9b120-227">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-227">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="9b120-228">**resource_length** Lunghezza della stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-228">**resource_length** Length of URL string for requested resource.</span></span>
- <span data-ttu-id="9b120-229">**input_ptr** Puntatore a dati aggiuntivi per la richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="9b120-229">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="9b120-230">Questo indirizzo è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="9b120-230">This is optional.</span></span> <span data-ttu-id="9b120-231">Se è valido, l'input specificato viene inserito nell'area del contenuto del messaggio e viene utilizzato un POST anziché un'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="9b120-231">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
- <span data-ttu-id="9b120-232">**input_size** Numero di byte nell'input aggiuntivo facoltativo a cui punta input_ptr.</span><span class="sxs-lookup"><span data-stu-id="9b120-232">**input_size** Number of bytes in optional additional input pointed to by input_ptr.</span></span>
- <span data-ttu-id="9b120-233">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-233">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="9b120-234">**username_length** Lunghezza del nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-234">**username_length** Length of optional user name for authentication.</span></span>
- <span data-ttu-id="9b120-235">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-235">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="9b120-236">**password_length** Lunghezza della password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-236">**password_length** Length of optional password for authentication.</span></span>
- <span data-ttu-id="9b120-237">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-237">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="9b120-238">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="9b120-238">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9b120-239">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="9b120-239">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="9b120-240">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="9b120-240">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="9b120-241">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-241">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="9b120-242">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-242">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="9b120-243">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-243">**Return Values**</span></span>

- <span data-ttu-id="9b120-244">**NX_SUCCESS** (0x00) ha inviato il messaggio di avvio Get client http</span><span class="sxs-lookup"><span data-stu-id="9b120-244">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="9b120-245">Errore del client HTTP interno **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="9b120-245">**NX_HTTP_ERROR** (0xE0) Internal HTTP Client error</span></span>
- <span data-ttu-id="9b120-246">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="9b120-246">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="9b120-247">**NX_HTTP_FAILED** (0xe2) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="9b120-247">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="9b120-248">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="9b120-248">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or password.</span></span>
- <span data-ttu-id="9b120-249">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-249">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-250">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="9b120-250">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

<span data-ttu-id="9b120-251">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-251">**Allowed From**</span></span>

<span data-ttu-id="9b120-252">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-252">Threads</span></span>

<span data-ttu-id="9b120-253">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-253">**Example**</span></span>
            
```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5),
                                           “/TEST.HTM”,
                                           9, NX_NULL, 0, “myname”, 6,
                                           “mypassword”, 10, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
far successful. The client must now call *nx_http_client_get_packet* multiple
times to retrieve the content associated with TEST.HTM. */

#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5), 
                                           “/TEST.HTM”,
                                           9, POST_MESSAGE, sizeof(POST_MESSAGE),
                                           “myname”, 6, “mypassword”, 10, 1000);

/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST 
request for TEST.HTM and successfully sent. */
```

## <a name="nx_http_client_get_packet"></a><span data-ttu-id="9b120-254">nx_http_client_get_packet</span><span class="sxs-lookup"><span data-stu-id="9b120-254">nx_http_client_get_packet</span></span>

### <a name="get-next-resource-data-packet"></a><span data-ttu-id="9b120-255">Ottenere il pacchetto di dati di risorse successivo</span><span class="sxs-lookup"><span data-stu-id="9b120-255">Get next resource data packet</span></span>

<span data-ttu-id="9b120-256">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-256">**Prototype**</span></span>

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                              NX_PACKET **packet_ptr,
                              ULONG wait_option);
```

<span data-ttu-id="9b120-257">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-257">**Description**</span></span>

<span data-ttu-id="9b120-258">Questo servizio recupera il pacchetto successivo di contenuto della risorsa richiesta dalla chiamata *nx_http_client_get_start* precedente.</span><span class="sxs-lookup"><span data-stu-id="9b120-258">This service retrieves the next packet of content of the resource requested by the previous *nx_http_client_get_start* call.</span></span> <span data-ttu-id="9b120-259">Le chiamate successive a questa routine devono essere apportate fino a quando non viene ricevuto lo stato di restituzione del NX_HTTP_GET_DONE.</span><span class="sxs-lookup"><span data-stu-id="9b120-259">Successive calls to this routine should be made until the return status of NX_HTTP_GET_DONE is received.</span></span>

<span data-ttu-id="9b120-260">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-260">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-261">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-261">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="9b120-262">**packet_ptr** Destinazione per il puntatore del pacchetto che contiene il contenuto parziale delle risorse.</span><span class="sxs-lookup"><span data-stu-id="9b120-262">**packet_ptr** Destination for packet pointer containing partial resource content.</span></span>
- <span data-ttu-id="9b120-263">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del pacchetto HTTP client Get.</span><span class="sxs-lookup"><span data-stu-id="9b120-263">**wait_option** Defines how long the service will wait for the HTTP Client get packet.</span></span> <span data-ttu-id="9b120-264">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="9b120-264">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9b120-265">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="9b120-265">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="9b120-266">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="9b120-266">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="9b120-267">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-267">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="9b120-268">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-268">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="9b120-269">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-269">**Return Values**</span></span>

- <span data-ttu-id="9b120-270">**NX_SUCCESS** (0x00) client http con esito positivo Get Packet.</span><span class="sxs-lookup"><span data-stu-id="9b120-270">**NX_SUCCESS** (0x00) Successful HTTP Client get packet.</span></span>
- <span data-ttu-id="9b120-271">**NX_HTTP_GET_DONE** (0XEC) client HTTP Get packet is done</span><span class="sxs-lookup"><span data-stu-id="9b120-271">**NX_HTTP_GET_DONE** (0xEC) HTTP Client get packet is done</span></span>
- <span data-ttu-id="9b120-272">Il client HTTP **NX_HTTP_NOT_READY** (0xea) non è in modalità Get.</span><span class="sxs-lookup"><span data-stu-id="9b120-272">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not in get mode.</span></span>
- <span data-ttu-id="9b120-273">Lunghezza del pacchetto **NX_HTTP_BAD_PACKET_LENGTH** (0XED) non valida</span><span class="sxs-lookup"><span data-stu-id="9b120-273">**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Invalid packet length</span></span>
- <span data-ttu-id="9b120-274">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-274">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-275">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-275">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-276">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-276">**Allowed From**</span></span>

<span data-ttu-id="9b120-277">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-277">Threads</span></span>

<span data-ttu-id="9b120-278">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-278">**Example**</span></span>

```c
/* Get the next packet of resource content on the HTTP Client “my_client.”
Note that the nx_http_client_get_start routine must have been called
previously. */
status = nx_http_client_get_packet(&my_client, &next_packet, 1000);
 
/* If status is NX_SUCCESS, the next packet of content is pointed to by 
“next_packet”. */
```

## <a name="nx_http_client_put_start"></a><span data-ttu-id="9b120-279">nx_http_client_put_start</span><span class="sxs-lookup"><span data-stu-id="9b120-279">nx_http_client_put_start</span></span>

### <a name="start-an-http-put-request"></a><span data-ttu-id="9b120-280">Avvia una richiesta HTTP PUT</span><span class="sxs-lookup"><span data-stu-id="9b120-280">Start an HTTP PUT request</span></span> 

<span data-ttu-id="9b120-281">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-281">**Prototype**</span></span>

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                             ULONG ip_address, CHAR *resource,
                             CHAR *username, CHAR *password,
                             ULONG total_bytes, ULONG wait_option);
```

<span data-ttu-id="9b120-282">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-282">**Description**</span></span>

<span data-ttu-id="9b120-283">Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="9b120-283">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address.</span></span> <span data-ttu-id="9b120-284">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet* per inviare effettivamente il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="9b120-284">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet* routine to actually send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="9b120-285">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="9b120-285">Note that the resource string can refer to a local file e.g. “/index.htm” or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="9b120-286">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="9b120-286">This service is deprecated.</span></span> <span data-ttu-id="9b120-287">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_client_put_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="9b120-287">Developers are encouraged to migrate to *nx_http_client_put_start_extended()*.</span></span>

<span data-ttu-id="9b120-288">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-288">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-289">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-289">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="9b120-290">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-290">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="9b120-291">**risorsa** di Puntatore alla stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="9b120-291">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="9b120-292">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-292">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="9b120-293">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-293">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="9b120-294">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="9b120-294">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="9b120-295">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="9b120-295">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
- <span data-ttu-id="9b120-296">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-296">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="9b120-297">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="9b120-297">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9b120-298">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="9b120-298">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="9b120-299">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="9b120-299">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="9b120-300">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-300">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="9b120-301">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-301">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="9b120-302">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-302">**Return Values**</span></span>

- <span data-ttu-id="9b120-303">**NX_SUCCESS** (0x00) ha inviato una richiesta PUT</span><span class="sxs-lookup"><span data-stu-id="9b120-303">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="9b120-304">**NX_HTTP_USERNAME_TOO_LONG**</span><span class="sxs-lookup"><span data-stu-id="9b120-304">**NX_HTTP_USERNAME_TOO_LONG**</span></span>
- <span data-ttu-id="9b120-305">**(0xF1) nome utente troppo grande per il buffer**</span><span class="sxs-lookup"><span data-stu-id="9b120-305">**(0xF1) Username too large for buffer**</span></span>
- <span data-ttu-id="9b120-306">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="9b120-306">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="9b120-307">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-307">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-308">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="9b120-308">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="9b120-309">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-309">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-310">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-310">**Allowed From**</span></span>

<span data-ttu-id="9b120-311">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-311">Threads</span></span>

<span data-ttu-id="9b120-312">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-312">**Example**</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP 
Server at IP address 1.2.3.5. */
status = nx_http_client_put_start(&my_client, IP_ADDRESS(1, 2, 3, 5),
                                 “/TEST.HTM”, “myname”, “mypassword”, 20, 
                                 NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully 
been started. */
```

## <a name="nx_http_client_put_start_extended"></a><span data-ttu-id="9b120-313">nx_http_client_put_start_extended</span><span class="sxs-lookup"><span data-stu-id="9b120-313">nx_http_client_put_start_extended</span></span>

### <a name="start-an-http-put-request"></a><span data-ttu-id="9b120-314">Avvia una richiesta HTTP PUT</span><span class="sxs-lookup"><span data-stu-id="9b120-314">Start an HTTP PUT request</span></span>

<span data-ttu-id="9b120-315">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-315">**Prototype**</span></span>

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
     ULONG ip_address, CHAR *resource, UINT resource_length,
     CHAR *username,UINT username_length, CHAR *password,
     UINT password_length, ULONG total_bytes, ULONG wait_option);
```

<span data-ttu-id="9b120-316">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-316">**Description**</span></span>

<span data-ttu-id="9b120-317">Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="9b120-317">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address.</span></span> <span data-ttu-id="9b120-318">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_http_client_put_packet* per inviare effettivamente il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="9b120-318">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet* routine to actually send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="9b120-319">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="9b120-319">Note that the resource string can refer to a local file e.g. “/index.htm” or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="9b120-320">Questo servizio sostituisce *nx_http_client_put_start ()*.</span><span class="sxs-lookup"><span data-stu-id="9b120-320">This service replaces *nx_http_client_put_start()*.</span></span> <span data-ttu-id="9b120-321">È necessario che il chiamante specifichi la lunghezza della risorsa, il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="9b120-321">It requires caller to specify the length of the resource, username and password.</span></span>

<span data-ttu-id="9b120-322">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-322">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-323">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-323">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="9b120-324">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-324">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="9b120-325">**risorsa** di Puntatore alla stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="9b120-325">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="9b120-326">**resource_length** Lunghezza della stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="9b120-326">**resource_length** Length of URL string for resource to send to Server.</span></span>
- <span data-ttu-id="9b120-327">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-327">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="9b120-328">**username_length** Lunghezza del nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-328">**username_length** Length of optional user name for authentication.</span></span>
- <span data-ttu-id="9b120-329">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-329">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="9b120-330">**password_length** Lunghezza della password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-330">**password_length** Length of optional password for authentication.</span></span>
- <span data-ttu-id="9b120-331">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="9b120-331">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="9b120-332">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_http_client_put_packet* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="9b120-332">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
- <span data-ttu-id="9b120-333">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-333">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="9b120-334">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="9b120-334">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9b120-335">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="9b120-335">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="9b120-336">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="9b120-336">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="9b120-337">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-337">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="9b120-338">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-338">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="9b120-339">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-339">**Return Values**</span></span>

- <span data-ttu-id="9b120-340">**NX_SUCCESS** (0x00) ha inviato una richiesta PUT</span><span class="sxs-lookup"><span data-stu-id="9b120-340">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="9b120-341">Nome utente di **NX_HTTP_USERNAME_TOO_LONG** (0xF1) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="9b120-341">**NX_HTTP_USERNAME_TOO_LONG** (0xF1) Username too large for buffer</span></span>
- <span data-ttu-id="9b120-342">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="9b120-342">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="9b120-343">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-343">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-344">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="9b120-344">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="9b120-345">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-345">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-346">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-346">**Allowed From**</span></span>

<span data-ttu-id="9b120-347">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-347">Threads</span></span>

<span data-ttu-id="9b120-348">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-348">**Example**</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP 
Server at IP address 1.2.3.5. */
status = nx_http_client_put_start_extended(&my_client, IP_ADDRESS(1, 2, 3, 5),
                                          “/TEST.HTM”, 9, “myname”, 6, 
                                          “mypassword”, 
                                          10, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully 
been started. */
```

## <a name="nx_http_client_put_packet"></a><span data-ttu-id="9b120-349">nx_http_client_put_packet</span><span class="sxs-lookup"><span data-stu-id="9b120-349">nx_http_client_put_packet</span></span>

### <a name="send-next-resource-data-packet"></a><span data-ttu-id="9b120-350">Invia pacchetto di dati di risorse successivo</span><span class="sxs-lookup"><span data-stu-id="9b120-350">Send next resource data packet</span></span>

<span data-ttu-id="9b120-351">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-351">**Prototype**</span></span>

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                              NX_PACKET *packet_ptr,
                              ULONG wait_option);
```

<span data-ttu-id="9b120-352">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-352">**Description**</span></span>

<span data-ttu-id="9b120-353">Questo servizio tenta di inviare il pacchetto successivo di contenuto di risorse al server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-353">This service attempts to send the next packet of resource content to the HTTP Server.</span></span> <span data-ttu-id="9b120-354">Si noti che questa routine deve essere chiamata ripetutamente fino a quando la lunghezza combinata dei pacchetti inviati è uguale a "total_bytes" specificata nella chiamata *nx_http_client_put_start ()* precedente.</span><span class="sxs-lookup"><span data-stu-id="9b120-354">Note that this routine should be called repetitively until the combined length of the packets sent equals the “total_bytes” specified in the previous *nx_http_client_put_start()* call.</span></span>

<span data-ttu-id="9b120-355">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-355">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-356">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-356">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="9b120-357">**packet_ptr** Puntatore al contenuto successivo della risorsa da inviare al server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-357">**packet_ptr** Pointer to next content of the resource to being sent to the HTTP Server.</span></span>
- <span data-ttu-id="9b120-358">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa internamente per elaborare il pacchetto PUT del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-358">**wait_option** Defines how long the service will wait internally to process the HTTP Client PUT packet.</span></span> <span data-ttu-id="9b120-359">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="9b120-359">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9b120-360">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="9b120-360">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="9b120-361">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="9b120-361">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="9b120-362">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-362">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /> <span data-ttu-id="9b120-363">La selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-363">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="9b120-364">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-364">**Return Values**</span></span>

- <span data-ttu-id="9b120-365">Il pacchetto client HTTP è stato inviato **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="9b120-365">**NX_SUCCESS** (0x00) Successfully sent HTTP Client packet.</span></span>
- <span data-ttu-id="9b120-366">Client HTTP **NX_HTTP_NOT_READY** (0xea) non pronto</span><span class="sxs-lookup"><span data-stu-id="9b120-366">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="9b120-367">**NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0XEE) ha ricevuto il codice di errore del server \* *-\*\*NX_HTTP_BAD_PACKET_LENGTH*\* (0xED) lunghezza del pacchetto non valida</span><span class="sxs-lookup"><span data-stu-id="9b120-367">**NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) Received Server error code\*\* -**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Invalid packet length</span></span>
- <span data-ttu-id="9b120-368">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) nome e/o password non validi</span><span class="sxs-lookup"><span data-stu-id="9b120-368">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or Password</span></span>
- <span data-ttu-id="9b120-369">Il server **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) risponde prima del completamento dell'operazione Put</span><span class="sxs-lookup"><span data-stu-id="9b120-369">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Server responds before PUT Is complete</span></span>
- <span data-ttu-id="9b120-370">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-370">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-371">Pacchetto di NX_INVALID_PACKET (0x12) troppo piccolo per l'intestazione TCP</span><span class="sxs-lookup"><span data-stu-id="9b120-371">NX_INVALID_PACKET (0x12) Packet too small for TCP header</span></span>
- <span data-ttu-id="9b120-372">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-372">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-373">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-373">**Allowed From**</span></span>

<span data-ttu-id="9b120-374">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-374">Threads</span></span>

<span data-ttu-id="9b120-375">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-375">**Example**</span></span>

```c
/* Send a 20-byte packet representing the content of the resource
“/TEST.HTM” to the HTTP Server. */
status = nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                                  NX_PACKET *packet_ptr,
                                  ULONG wait_option);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM
has successfully been sent. */
```

## <a name="nx_http_client_set_connect_port"></a><span data-ttu-id="9b120-376">nx_http_client_set_connect_port</span><span class="sxs-lookup"><span data-stu-id="9b120-376">nx_http_client_set_connect_port</span></span>

### <a name="set-the-connection-port-to-the-server"></a><span data-ttu-id="9b120-377">Impostare la porta di connessione sul server</span><span class="sxs-lookup"><span data-stu-id="9b120-377">Set the connection port to the Server</span></span>

<span data-ttu-id="9b120-378">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-378">**Prototype**</span></span>

```c
UINT nx_http_client_set_connect_port(NX_HTTP_CLIENT *client_ptr,
                                    UINT port);
```

<span data-ttu-id="9b120-379">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-379">**Description**</span></span>

<span data-ttu-id="9b120-380">Questo servizio modifica la porta di connessione per la connessione al server HTTP alla porta specificata in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9b120-380">This service changes the connect port when connecting to the HTTP Server to the specified port at runtime.</span></span> <span data-ttu-id="9b120-381">In caso contrario, il valore predefinito della porta di connessione è 80.</span><span class="sxs-lookup"><span data-stu-id="9b120-381">Otherwise the connect port defaults to 80.</span></span> <span data-ttu-id="9b120-382">Questo metodo deve essere chiamato prima di *nx_http_client_get_start*() e *nx_http_client_put_start*(), ad esempio quando il client HTTP si connette al server.</span><span class="sxs-lookup"><span data-stu-id="9b120-382">This must be called before *nx_http_client_get_start*() and *nx_http_client_put_start*() e.g. when the HTTP Client connects with the Server.</span></span>

<span data-ttu-id="9b120-383">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-383">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-384">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-384">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="9b120-385">**porta** Porta per la connessione al server.</span><span class="sxs-lookup"><span data-stu-id="9b120-385">**port** Port for connecting to the Server.</span></span>

<span data-ttu-id="9b120-386">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-386">**Return Values**</span></span>

- <span data-ttu-id="9b120-387">**NX_SUCCESS** (0x00) ha modificato correttamente la porta di connessione</span><span class="sxs-lookup"><span data-stu-id="9b120-387">**NX_SUCCESS** (0x00) Successfully changed the connect port</span></span>
- <span data-ttu-id="9b120-388">La porta **NX_INVALID_PORT** (0x46) supera il valore massimo (0xFFFF) o è zero.</span><span class="sxs-lookup"><span data-stu-id="9b120-388">**NX_INVALID_PORT** (0x46) Port exceeds the maximum (0xFFFF) or is zero.</span></span>
- <span data-ttu-id="9b120-389">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-389">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-390">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-390">**Allowed From**</span></span>

<span data-ttu-id="9b120-391">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="9b120-391">Threads, Initialization</span></span>

<span data-ttu-id="9b120-392">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-392">**Example**</span></span>

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status = nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a><span data-ttu-id="9b120-393">nx_http_server_cache_info_callback_set</span><span class="sxs-lookup"><span data-stu-id="9b120-393">nx_http_server_cache_info_callback_set</span></span>

### <a name="set-the-callback-to-retrieve-url-max-age-and-date"></a><span data-ttu-id="9b120-394">Impostare il callback per il recupero della validità e della data massima dell'URL</span><span class="sxs-lookup"><span data-stu-id="9b120-394">Set the callback to retrieve URL max age and date</span></span>

<span data-ttu-id="9b120-395">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-395">**Prototype**</span></span>

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                                           UINT (*cache_info_get)(CHAR *resource,
                                           UINT *max_age,
                                           NX_HTTP_SERVER_DATE *date));
```

<span data-ttu-id="9b120-396">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-396">**Description**</span></span>

<span data-ttu-id="9b120-397">Questo servizio imposta il servizio di callback richiamato per ottenere la data di validità massima e dell'Ultima modifica della risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="9b120-397">This service sets the callback service invoked to obtain the maximum age and last modified date of the specified resource.</span></span>

<span data-ttu-id="9b120-398">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-398">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-399">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-399">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-400">**cache_info_get** Puntatore al callback</span><span class="sxs-lookup"><span data-stu-id="9b120-400">**cache_info_get** Pointer to the callback</span></span>
- <span data-ttu-id="9b120-401">**max_age** Puntatore alla durata massima di una risorsa</span><span class="sxs-lookup"><span data-stu-id="9b120-401">**max_age** Pointer to maximum age of a resource</span></span>
- <span data-ttu-id="9b120-402">**dati** di Puntatore alla data dell'Ultima modifica restituita.</span><span class="sxs-lookup"><span data-stu-id="9b120-402">**data** Pointer to last modified date returned.</span></span>

<span data-ttu-id="9b120-403">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-403">**Return Values**</span></span>

- <span data-ttu-id="9b120-404">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="9b120-404">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="9b120-405">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-405">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-406">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-406">**Allowed From**</span></span>

<span data-ttu-id="9b120-407">Inizializzazione</span><span class="sxs-lookup"><span data-stu-id="9b120-407">Initialization</span></span>

<span data-ttu-id="9b120-408">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-408">**Example**</span></span>

```c
NX_HTTP_SERVER my_server;
UINT cache_info_get(CHAR *resource, UINT *max_age,
                   NX_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_http_server_create and before the HTTP
server is set by nx_http_server_start(), set the cache info callback: */
status = nx_http_server_cache_info_callback_set(&my_server, cache_info_get);

/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_http_server_callback_data_send"></a><span data-ttu-id="9b120-409">nx_http_server_callback_data_send</span><span class="sxs-lookup"><span data-stu-id="9b120-409">nx_http_server_callback_data_send</span></span>

### <a name="send-data-from-callback-function"></a><span data-ttu-id="9b120-410">Inviare dati da una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="9b120-410">Send data from callback function</span></span>

<span data-ttu-id="9b120-411">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-411">**Prototype**</span></span>

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                      VOID *data_ptr,
                                      ULONG data_length);
```

<span data-ttu-id="9b120-412">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-412">**Description**</span></span>

<span data-ttu-id="9b120-413">Questo servizio invia i dati nel pacchetto fornito dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-413">This service sends the data in the supplied packet from the application’s callback routine.</span></span> <span data-ttu-id="9b120-414">Questa operazione viene in genere usata per inviare i dati dinamici associati alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="9b120-414">This is typically used to send dynamic data associated with GET/POST requests.</span></span> <span data-ttu-id="9b120-415">Si noti che se si utilizza questa funzione, la routine di callback è responsabile dell'invio dell'intera risposta nel formato corretto.</span><span class="sxs-lookup"><span data-stu-id="9b120-415">Note that if this function is used, the callback routine is responsible for sending the entire response in the proper format.</span></span> <span data-ttu-id="9b120-416">Inoltre, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="9b120-416">In addition, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="9b120-417">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-417">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-418">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-418">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-419">**DATA_PTR** Puntatore ai dati da inviare.</span><span class="sxs-lookup"><span data-stu-id="9b120-419">**data_ptr** Pointer to the data to send.</span></span>
- <span data-ttu-id="9b120-420">**Data_length** Numero di byte da inviare.</span><span class="sxs-lookup"><span data-stu-id="9b120-420">**data_length** Number of bytes to send.</span></span>

<span data-ttu-id="9b120-421">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-421">**Return Values**</span></span>

- <span data-ttu-id="9b120-422">**NX_SUCCESS** (0x00) ha inviato correttamente i dati del server</span><span class="sxs-lookup"><span data-stu-id="9b120-422">**NX_SUCCESS** (0x00) Successfully sent Server data</span></span>
- <span data-ttu-id="9b120-423">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-423">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-424">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-424">**Allowed From**</span></span>

<span data-ttu-id="9b120-425">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-425">Threads</span></span>

<span data-ttu-id="9b120-426">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-426">**Example**</span></span>

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
       (strcmp(resource, "/test.htm") == 0))
    {
        /* Found it, override the GET processing by sending the resource
        contents directly. */

        nx_http_server_callback_data_send(server_ptr,
                                         "HTTP/1.0 200 \r\nContent-Length:
                                         103\r\nContent-Type: text/html\r\n\r\n",
                                         63);
        nx_http_server_callback_data_send(server_ptr, "<HTML>> r\n<HEAD><TITLE>NetX
                                         HTTP Test </TITLE></HEAD>\r\n
                                         <BODY>\r\n<H1>NetX Test Page
                                         </H1>\r\n</BODY>> r\n</HTML>\r\n", 103);
        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }
    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_generate_response_header"></a><span data-ttu-id="9b120-427">nx_http_server_callback_generate_response_header</span><span class="sxs-lookup"><span data-stu-id="9b120-427">nx_http_server_callback_generate_response_header</span></span>

### <a name="create-a-response-header-in-a-callback-function"></a><span data-ttu-id="9b120-428">Creare un'intestazione della risposta in una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="9b120-428">Create a response header in a callback function</span></span>

<span data-ttu-id="9b120-429">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-429">**Prototype**</span></span>

```c
UINT nx_http_server_callback_generate_response_header(NX_HTTP_SERVER *server_ptr,
     NX_PACKET **packet_pptr, CHAR *status_code, UINT content_length,
     CHAR *content_type, CHAR* additional_header);
```

<span data-ttu-id="9b120-430">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-430">**Description**</span></span>

<span data-ttu-id="9b120-431">Questo servizio chiama la funzione interna _ *nx_http_server_generate_response_header* quando il server HTTP risponde alle richieste Get, put e Delete del client.</span><span class="sxs-lookup"><span data-stu-id="9b120-431">This service calls the internal function _ *nx_http_server_generate_response_header* when the HTTP server responds to Client get, put and delete requests.</span></span> <span data-ttu-id="9b120-432">È destinato all'uso nelle funzioni di callback del server HTTP quando l'applicazione server HTTP sta progettando la propria risposta al client.</span><span class="sxs-lookup"><span data-stu-id="9b120-432">It is intended for use in HTTP server callback functions when the HTTP server application is designing its response to the Client.</span></span>

<span data-ttu-id="9b120-433">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="9b120-433">This service is deprecated.</span></span> <span data-ttu-id="9b120-434">Gli sviluppatori sono invitati a eseguire la migrazione a *nxd_http_server_callback_generate_response_header_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="9b120-434">Developers are encouraged to migrate to *nxd_http_server_callback_generate_response_header_extended()*.</span></span>

<span data-ttu-id="9b120-435">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-435">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-436">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-436">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-437">**packet_pptr** Puntatore a un puntatore di pacchetto allocato per il messaggio</span><span class="sxs-lookup"><span data-stu-id="9b120-437">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
- <span data-ttu-id="9b120-438">**status_code** Indicare lo stato della risorsa.</span><span class="sxs-lookup"><span data-stu-id="9b120-438">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="9b120-439">Esempi:</span><span class="sxs-lookup"><span data-stu-id="9b120-439">Examples:</span></span>
- <span data-ttu-id="9b120-440">**NX_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="9b120-440">**NX_HTTP_STATUS_OK**</span></span>
- <span data-ttu-id="9b120-441">**NX_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="9b120-441">**NX_HTTP_STATUS_MODIFIED**</span></span>
- <span data-ttu-id="9b120-442">**NX_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="9b120-442">**NX_HTTP_STATUS_INTERNAL_ERROR**</span></span>
- <span data-ttu-id="9b120-443">**CONTENT_LENGTH** Dimensioni del contenuto in byte</span><span class="sxs-lookup"><span data-stu-id="9b120-443">**content_length** Size of content in bytes</span></span>
- <span data-ttu-id="9b120-444">**content_type** Tipo di HTTP, ad esempio "text/plain"</span><span class="sxs-lookup"><span data-stu-id="9b120-444">**content_type** Type of HTTP e.g. “text/plain”</span></span>
- <span data-ttu-id="9b120-445">**additional_header** Puntatore a testo intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="9b120-445">**additional_header** Pointer to additional header text</span></span>

<span data-ttu-id="9b120-446">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-446">**Return Values**</span></span>

- <span data-ttu-id="9b120-447">**NX_SUCCESS** (0x00) ha creato l'intestazione HTML</span><span class="sxs-lookup"><span data-stu-id="9b120-447">**NX_SUCCESS** (0x00) Successfully created HTML header</span></span>
- <span data-ttu-id="9b120-448">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-448">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-449">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-449">**Allowed From**</span></span>

<span data-ttu-id="9b120-450">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-450">Threads</span></span>

<span data-ttu-id="9b120-451">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-451">**Example**</span></span>

```c
CHAR demotestbuffer[] = “<html>\r\n\r\n<head> r\n\r\n<title>Main                 \
                        Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n  \ 
                        </body>\r\n</html>\r\n";

/* my_request_notify is the application request notify callback registered with
the HTTP server in nx_http_server_create, creates a response to the received
Client request. */

UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET     *sresp_packet_ptr;
    ULONG         string_length;
    CHAR          temp_string[30];
    ULONG         length = 0;

        length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length = (ULONG) nx_http_server_type_get(server_ptr, server_ptr ->
                   nx_http_server_request_resource, temp_string);

/* Null terminate the string. */
   temp_string[temp] = 0;

/* Now build a response header with server status is OK and no additional header info. */
   status = nx_http_server_callback_generate_response_header(http_server_ptr,
            &resp_packet_ptr, NX_HTTP_STATUS_OK,
            length, temp_string, NX_NULL);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
            length, server_ptr >>
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

## <a name="nx_http_server_callback_generate_response_header_extended"></a><span data-ttu-id="9b120-452">nx_http_server_callback_generate_response_header_extended</span><span class="sxs-lookup"><span data-stu-id="9b120-452">nx_http_server_callback_generate_response_header_extended</span></span>

### <a name="create-a-response-header-in-a-callback-function"></a><span data-ttu-id="9b120-453">Creare un'intestazione della risposta in una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="9b120-453">Create a response header in a callback function</span></span>

<span data-ttu-id="9b120-454">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-454">**Prototype**</span></span>

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

<span data-ttu-id="9b120-455">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-455">**Description**</span></span>

<span data-ttu-id="9b120-456">Questo servizio chiama la funzione interna _ *nx_http_server_generate_response_header ()* quando il server HTTP risponde alle richieste Get, put e Delete del client.</span><span class="sxs-lookup"><span data-stu-id="9b120-456">This service calls the internal function _ *nx_http_server_generate_response_header()* when the HTTP server responds to Client get, put and delete requests.</span></span> <span data-ttu-id="9b120-457">È destinato all'uso nelle funzioni di callback del server HTTP quando l'applicazione server HTTP sta progettando la propria risposta al client.</span><span class="sxs-lookup"><span data-stu-id="9b120-457">It is intended for use in HTTP server callback functions when the HTTP server application is designing its response to the Client.</span></span>

<span data-ttu-id="9b120-458">Questo servizio sostituisce *nx_http_server_callback_generate_response_header ()*.</span><span class="sxs-lookup"><span data-stu-id="9b120-458">This service replaces *nx_http_server_callback_generate_response_header()*.</span></span> <span data-ttu-id="9b120-459">Questa versione fornisce informazioni aggiuntive sulla lunghezza della funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="9b120-459">This version supplies additional length information to the callback function.</span></span>

<span data-ttu-id="9b120-460">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-460">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-461">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-461">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-462">**packet_pptr** Puntatore a un puntatore di pacchetto allocato per il messaggio</span><span class="sxs-lookup"><span data-stu-id="9b120-462">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
- <span data-ttu-id="9b120-463">**status_code** Indicare lo stato della risorsa.</span><span class="sxs-lookup"><span data-stu-id="9b120-463">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="9b120-464">Esempi:</span><span class="sxs-lookup"><span data-stu-id="9b120-464">Examples:</span></span>
  - <span data-ttu-id="9b120-465">**NX_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="9b120-465">**NX_HTTP_STATUS_OK**</span></span>
  - <span data-ttu-id="9b120-466">**NX_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="9b120-466">**NX_HTTP_STATUS_MODIFIED**</span></span>
  - <span data-ttu-id="9b120-467">**NX_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="9b120-467">**NX_HTTP_STATUS_INTERNAL_ERROR**</span></span>
- <span data-ttu-id="9b120-468">**status_code** Lunghezza del codice di stato</span><span class="sxs-lookup"><span data-stu-id="9b120-468">**status_code** Length of status code</span></span>
- <span data-ttu-id="9b120-469">**CONTENT_LENGTH** Dimensioni del contenuto in byte</span><span class="sxs-lookup"><span data-stu-id="9b120-469">**content_length** Size of content in bytes</span></span>
- <span data-ttu-id="9b120-470">**content_type** Tipo di HTTP, ad esempio "text/plain"</span><span class="sxs-lookup"><span data-stu-id="9b120-470">**content_type** Type of HTTP e.g. “text/plain”</span></span>
- <span data-ttu-id="9b120-471">**content_type_length** Lunghezza del tipo HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-471">**content_type_length** Length of HTTP type</span></span>
- <span data-ttu-id="9b120-472">**additional_header** Puntatore a testo intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="9b120-472">**additional_header** Pointer to additional header text</span></span>
- <span data-ttu-id="9b120-473">**additional_header_length** Lunghezza del testo dell'intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="9b120-473">**additional_header_length** Length of additional header text</span></span>

<span data-ttu-id="9b120-474">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-474">**Return Values**</span></span>

- <span data-ttu-id="9b120-475">Intestazione creazione **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="9b120-475">**NX_SUCCESS** (0x00) Successfully created header</span></span>
- <span data-ttu-id="9b120-476">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-476">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-477">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-477">**Allowed From**</span></span>

<span data-ttu-id="9b120-478">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-478">Threads</span></span>

<span data-ttu-id="9b120-479">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-479">**Example**</span></span>

```c
  CHAR demotestbuffer[] = “<html>\r\n\r\n<head>\r\n\r\n<title>Main                    \
                          Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n     \
                          </body>\r\n</html>\r\n";

/* my_request_notify is the application request notify callback registered with
   the HTTP server in nx_http_server_create, creates a response to the received
   Client request. */

   UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                         CHAR *resource, NX_PACKET *recv_packet_ptr)
   {
     NX_PACKET *sresp_packet_ptr;
     ULONG string_length;
     CHAR temp_string[30];
     ULONG length = 0;

     length = sizeof(demotestbuffer) - 1;

    /* Derive the client request type from the client request. */
       string_length = (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr >>
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
                length, server_ptr ->
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

## <a name="nx_http_server_callback_packet_send"></a><span data-ttu-id="9b120-480">nx_http_server_callback_packet_send</span><span class="sxs-lookup"><span data-stu-id="9b120-480">nx_http_server_callback_packet_send</span></span>

### <a name="send-an-http-packet-from-callback-function"></a><span data-ttu-id="9b120-481">Inviare un pacchetto HTTP dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="9b120-481">Send an HTTP packet from callback function</span></span>

<span data-ttu-id="9b120-482">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-482">**Prototype**</span></span>

```c
UINT nx_http_server_callback_packet_send(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET *packet_ptr);
```

<span data-ttu-id="9b120-483">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-483">**Description**</span></span>

<span data-ttu-id="9b120-484">Questo servizio invia una risposta server HTTP completa da un callback HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-484">This service sends a complete HTTP server response from an HTTP callback.</span></span> <span data-ttu-id="9b120-485">Il pacchetto viene inviato dal server HTTP al _TIMEOUT_SEND NX_HTTP_SERVER.</span><span class="sxs-lookup"><span data-stu-id="9b120-485">HTTP server will send the packet with the NX_HTTP_SERVER _TIMEOUT_SEND.</span></span> <span data-ttu-id="9b120-486">L'intestazione e i dati HTTP devono essere aggiunti al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b120-486">The HTTP header and data must be appended to the packet.</span></span> <span data-ttu-id="9b120-487">Se lo stato restituito indica un errore, l'applicazione HTTP deve rilasciare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b120-487">If the return status indicates an error, the HTTP application must release the packet.</span></span>

<span data-ttu-id="9b120-488">Il callback deve restituire NX_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="9b120-488">The callback should return NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="9b120-489">Per un esempio più dettagliato, vedere *nx_http_server_callback_generate_response_header ()* .</span><span class="sxs-lookup"><span data-stu-id="9b120-489">See *nx_http_server_callback_generate_response_header()* for a more detailed example.</span></span>

<span data-ttu-id="9b120-490">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-490">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-491">**server_ptr** Puntatore al blocco di controllo server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-491">**server_ptr** Pointer to HTTP Server control block</span></span>
- <span data-ttu-id="9b120-492">**packet_ptr** Puntatore al pacchetto da inviare</span><span class="sxs-lookup"><span data-stu-id="9b120-492">**packet_ptr** Pointer to the packet to send</span></span>

<span data-ttu-id="9b120-493">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-493">**Return Values**</span></span>

- <span data-ttu-id="9b120-494">**NX_SUCCESS** (0x00) ha inviato il pacchetto del server http</span><span class="sxs-lookup"><span data-stu-id="9b120-494">**NX_SUCCESS** (0x00) Successfully sent HTTP Server packet</span></span>
- <span data-ttu-id="9b120-495">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-495">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-496">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-496">**Allowed From**</span></span>

<span data-ttu-id="9b120-497">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-497">Threads</span></span>

<span data-ttu-id="9b120-498">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-498">**Example**</span></span>

```c
/* The packet is appended with HTTP header and data and is ready to send to the
Client directly. */

   status = nx_http_server_callback_response_send**(server_ptr, packet_ptr);
   
   if (status != NX_SUCCESS)
   {
        nx_packet_release(packet_ptr);
   }
    return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_callback_response_send"></a><span data-ttu-id="9b120-499">nx_http_server_callback_response_send</span><span class="sxs-lookup"><span data-stu-id="9b120-499">nx_http_server_callback_response_send</span></span>

### <a name="send-response-from-callback-function"></a><span data-ttu-id="9b120-500">Invia risposta dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="9b120-500">Send response from callback function</span></span>

<span data-ttu-id="9b120-501">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-501">**Prototype**</span></span>

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
     CHAR *header, CHAR *information, CHAR additional_info);
```

<span data-ttu-id="9b120-502">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-502">**Description**</span></span>

<span data-ttu-id="9b120-503">Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-503">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="9b120-504">Questa operazione viene in genere usata per inviare risposte personalizzate associate alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="9b120-504">This is typically used to send custom responses associated with GET/POST requests.</span></span> <span data-ttu-id="9b120-505">Si noti che se si utilizza questa funzione, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="9b120-505">Note that if this function is used, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="9b120-506">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="9b120-506">This service is deprecated.</span></span> <span data-ttu-id="9b120-507">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_server_callback_response_send_extended ().*</span><span class="sxs-lookup"><span data-stu-id="9b120-507">Developers are encouraged to migrate to *nx_http_server_callback_response_send_extended().*</span></span>

<span data-ttu-id="9b120-508">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-508">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-509">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-509">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-510">**intestazione** di Puntatore alla stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="9b120-510">**header** Pointer to the response header string.</span></span>
- <span data-ttu-id="9b120-511">**informazioni** su Puntatore alla stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="9b120-511">**information** Pointer to the information string.</span></span>
- <span data-ttu-id="9b120-512">**additional_info** Puntatore alla stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="9b120-512">**additional_info** Pointer to the additional information string.</span></span>

<span data-ttu-id="9b120-513">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-513">**Return Values**</span></span>

- <span data-ttu-id="9b120-514">**NX_SUCCESS** (0x00) ha inviato correttamente la risposta al server http</span><span class="sxs-lookup"><span data-stu-id="9b120-514">**NX_SUCCESS** (0x00) Successfully sent HTTP Server response</span></span>

<span data-ttu-id="9b120-515">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-515">**Allowed From**</span></span>

<span data-ttu-id="9b120-516">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-516">Threads</span></span>

<span data-ttu-id="9b120-517">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-517">**Example**</span></span>

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
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

## <a name="nx_http_server_callback_response_send_extended"></a><span data-ttu-id="9b120-518">nx_http_server_callback_response_send_extended</span><span class="sxs-lookup"><span data-stu-id="9b120-518">nx_http_server_callback_response_send_extended</span></span>

### <a name="send-response-from-callback-function"></a><span data-ttu-id="9b120-519">Invia risposta dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="9b120-519">Send response from callback function</span></span>

<span data-ttu-id="9b120-520">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-520">**Prototype**</span></span>

```c
UINT nx_http_server_callback_response_send_extended(
     NX_HTTP_SERVER *server_ptr, CHAR *heade
     UINT header_length, CHAR *information,
     UINT information_length, CHAR *additional_info,
     UINT additional_info_length);
```

<span data-ttu-id="9b120-521">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-521">**Description**</span></span>

<span data-ttu-id="9b120-522">Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-522">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="9b120-523">Questa operazione viene in genere usata per inviare risposte personalizzate associate alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="9b120-523">This is typically used to send custom responses associated with GET/POST requests.</span></span> <span data-ttu-id="9b120-524">Si noti che se si utilizza questa funzione, la routine di callback deve restituire lo stato di NX_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="9b120-524">Note that if this function is used, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="9b120-525">Questo servizio sostituisce *nx_http_server_callback_response_send ().*</span><span class="sxs-lookup"><span data-stu-id="9b120-525">This service replaces *nx_http_server_callback_response_send().*</span></span> <span data-ttu-id="9b120-526">Questa versione accetta informazioni di lunghezza come argomento di input.</span><span class="sxs-lookup"><span data-stu-id="9b120-526">This version takes length information as input argument.</span></span>

<span data-ttu-id="9b120-527">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-527">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-528">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-528">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-529">**intestazione** di Puntatore alla stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="9b120-529">**header** Pointer to the response header string.</span></span>
- <span data-ttu-id="9b120-530">**HEADER_LENGTH** Lunghezza della stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="9b120-530">**header_length** Length of the response header string.</span></span>
- <span data-ttu-id="9b120-531">**informazioni** su Puntatore alla stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="9b120-531">**information** Pointer to the information string.</span></span>
- <span data-ttu-id="9b120-532">**information_length** Lunghezza della stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="9b120-532">**information_length** Length of the information string.</span></span>
- <span data-ttu-id="9b120-533">**additional_info** Puntatore alla stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="9b120-533">**additional_info** Pointer to the additional information string.</span></span>
- <span data-ttu-id="9b120-534">**additional_info_length** Lunghezza della stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="9b120-534">**additional_info_length** Length of the additional information string.</span></span>

<span data-ttu-id="9b120-535">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-535">**Return Values**</span></span>

- <span data-ttu-id="9b120-536">**NX_SUCCESS** (0x00) ha inviato una risposta server</span><span class="sxs-lookup"><span data-stu-id="9b120-536">**NX_SUCCESS** (0x00) Successfully sent Server response</span></span>

<span data-ttu-id="9b120-537">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-537">**Allowed From**</span></span>

<span data-ttu-id="9b120-538">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-538">Threads</span></span>

<span data-ttu-id="9b120-539">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-539">**Example**</span></span>

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
       if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
          (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
           a resource not found response. */
           nx_http_server_callback_response_send_extended(server_ptr,
                                                         "HTTP/1.0 404 ", 12,
                                                         "NetX HTTP Server unable to find
                                                         file: ", 38, resource, 9);
        /* Return completion status. */
           return(NX_HTTP_CALLBACK_COMPLETED);
    }
    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_content_get"></a><span data-ttu-id="9b120-540">nx_http_server_content_get</span><span class="sxs-lookup"><span data-stu-id="9b120-540">nx_http_server_content_get</span></span>

### <a name="get-content-from-the-request"></a><span data-ttu-id="9b120-541">Ottenere contenuto dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="9b120-541">Get content from the request</span></span>

<span data-ttu-id="9b120-542">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-542">**Prototype**</span></span>

```c
UINT nx_http_server_content_get(NX_HTTP_SERVER *server_ptr,
                                NX_PACKET *packet_ptr,
                                ULONG byte_offset,
                                CHAR *destination_ptr,
                                UINT destination_size,
                                UINT *actual_size);
```

<span data-ttu-id="9b120-543">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-543">**Description**</span></span>

<span data-ttu-id="9b120-544">Questo servizio tenta di recuperare la quantità specificata di contenuto dalla richiesta client HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="9b120-544">This service attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="9b120-545">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="9b120-545">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="9b120-546">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="9b120-546">This service is deprecated.</span></span> <span data-ttu-id="9b120-547">Gli sviluppatori sono invitati a eseguire la migrazione a nx_http_server_content_get_extended ().</span><span class="sxs-lookup"><span data-stu-id="9b120-547">Developers are encouraged to migrate to nx_http_server_content_get_extended().</span></span>

<span data-ttu-id="9b120-548">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-548">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-549">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-549">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-550">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-550">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="9b120-551">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="9b120-551">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="9b120-552">**byte_offset** Numero di byte da sfalsare nell'area del contenuto.</span><span class="sxs-lookup"><span data-stu-id="9b120-552">**byte_offset** Number of bytes to offset into the content area.</span></span>
- <span data-ttu-id="9b120-553">**destination_ptr** Puntatore all'area di destinazione per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="9b120-553">**destination_ptr** Pointer to the destination area for the content.</span></span>
- <span data-ttu-id="9b120-554">**destination_size** Numero massimo di byte disponibili nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-554">**destination_size** Maximum number of bytes available in the destination area.</span></span>
- <span data-ttu-id="9b120-555">**actual_size** Puntatore alla variabile di destinazione che verrà impostata sulle dimensioni effettive del contenuto copiato.</span><span class="sxs-lookup"><span data-stu-id="9b120-555">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

<span data-ttu-id="9b120-556">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-556">**Return Values**</span></span>

- <span data-ttu-id="9b120-557">**NX_SUCCESS** (0x00) il contenuto del server http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="9b120-557">**NX_SUCCESS** (0x00) Successful HTTP Server content get</span></span>
- <span data-ttu-id="9b120-558">Errore interno del server HTTP **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="9b120-558">**NX_HTTP_ERROR** (0xE0) HTTP Server internal error</span></span>
- <span data-ttu-id="9b120-559">**NX_HTTP_DATA_END** (0xE7) fine del contenuto della richiesta</span><span class="sxs-lookup"><span data-stu-id="9b120-559">**NX_HTTP_DATA_END** (0xE7) End of request content</span></span>
- <span data-ttu-id="9b120-560">TIMEOUT del server HTTP **NX_HTTP_TIMEOUT** (0xE1) per il recupero del pacchetto di contenuto successivo</span><span class="sxs-lookup"><span data-stu-id="9b120-560">**NX_HTTP_TIMEOUT** (0xE1) HTTP Server timeout in getting next packet of content</span></span>
- <span data-ttu-id="9b120-561">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-561">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-562">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-562">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-563">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-563">**Allowed From**</span></span>

<span data-ttu-id="9b120-564">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-564">Threads</span></span>

<span data-ttu-id="9b120-565">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-565">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, retrieve up to 100 bytes of content starting at offset 0. */
status = nx_http_server_content_get(&my_server, packet_ptr,
                                   0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
request content. */
```

## <a name="nx_http_server_content_get_extended"></a><span data-ttu-id="9b120-566">nx_http_server_content_get_extended</span><span class="sxs-lookup"><span data-stu-id="9b120-566">nx_http_server_content_get_extended</span></span>

### <a name="get-content-from-the-requestsupports-zero-length-content-length"></a><span data-ttu-id="9b120-567">Ottieni contenuto dalla richiesta/supporta la lunghezza del contenuto di lunghezza zero</span><span class="sxs-lookup"><span data-stu-id="9b120-567">Get content from the request/supports zero length Content Length</span></span>

<span data-ttu-id="9b120-568">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-568">**Prototype**</span></span>

```c
UINT nx_http_server_content_get_extended(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET *packet_ptr,
                                        ULONG byte_offset,
                                        CHAR *destination_ptr,
                                        UINT destination_size,
                                        UINT *actual_size);
```

<span data-ttu-id="9b120-569">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-569">**Description**</span></span>

<span data-ttu-id="9b120-570">Questo servizio è quasi identico a *nx_http_server_content_get ()*; tenta di recuperare la quantità specificata di contenuto dalla richiesta del client HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="9b120-570">This service is almost identical to *nx_http_server_content_get()*; it attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="9b120-571">Tuttavia, gestisce le richieste con lunghezza del contenuto pari a zero (' Empty request ') come richiesta valida.</span><span class="sxs-lookup"><span data-stu-id="9b120-571">However it handles requests with Content Length of zero value (‘empty request’) as a valid request.</span></span> <span data-ttu-id="9b120-572">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="9b120-572">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="9b120-573">Questo servizio sostituisce *nx_http_server_content_get ().*</span><span class="sxs-lookup"><span data-stu-id="9b120-573">This service replaces *nx_http_server_content_get().*</span></span> <span data-ttu-id="9b120-574">Questa versione richiede che il chiamante fornisca informazioni di lunghezza aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="9b120-574">This version requires caller to supply additional length information.</span></span>

<span data-ttu-id="9b120-575">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-575">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-576">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-576">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-577">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-577">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="9b120-578">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="9b120-578">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="9b120-579">**byte_offset** Numero di byte da sfalsare nell'area del contenuto.</span><span class="sxs-lookup"><span data-stu-id="9b120-579">**byte_offset** Number of bytes to offset into the content area.</span></span>
- <span data-ttu-id="9b120-580">**destination_ptr** Puntatore all'area di destinazione per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="9b120-580">**destination_ptr** Pointer to the destination area for the content.</span></span>
- <span data-ttu-id="9b120-581">**destination_size** Numero massimo di byte disponibili nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-581">**destination_size** Maximum number of bytes available in the destination area.</span></span>
- <span data-ttu-id="9b120-582">**actual_size** Puntatore alla variabile di destinazione che verrà impostata sulle dimensioni effettive del contenuto copiato.</span><span class="sxs-lookup"><span data-stu-id="9b120-582">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

<span data-ttu-id="9b120-583">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-583">**Return Values**</span></span>

- <span data-ttu-id="9b120-584">**NX_SUCCESS** (0x00) contenuto http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="9b120-584">**NX_SUCCESS** (0x00) Successful HTTP content get</span></span>
- <span data-ttu-id="9b120-585">Errore interno del server HTTP **NX_HTTP_ERROR** (0XE0)</span><span class="sxs-lookup"><span data-stu-id="9b120-585">**NX_HTTP_ERROR** (0xE0) HTTP Server internal error</span></span>
- <span data-ttu-id="9b120-586">**NX_HTTP_DATA_END** (0xE7) fine del contenuto della richiesta</span><span class="sxs-lookup"><span data-stu-id="9b120-586">**NX_HTTP_DATA_END** (0xE7) End of request content</span></span>
- <span data-ttu-id="9b120-587">TIMEOUT del server HTTP **NX_HTTP_TIMEOUT** (0xE1) nel recupero del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="9b120-587">**NX_HTTP_TIMEOUT** (0xE1) HTTP Server timeout in getting next packet</span></span>
- <span data-ttu-id="9b120-588">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-588">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-589">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-589">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-590">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-590">**Allowed From**</span></span>

<span data-ttu-id="9b120-591">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-591">Threads</span></span>

<span data-ttu-id="9b120-592">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-592">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, retrieve up to 100 bytes of content starting at offset 0. */
status = nx_http_server_content_get_extended(&my_server, packet_ptr,
                                            0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
request content. */
```

## <a name="nx_http_server_content_length_get"></a><span data-ttu-id="9b120-593">nx_http_server_content_length_get</span><span class="sxs-lookup"><span data-stu-id="9b120-593">nx_http_server_content_length_get</span></span>

### <a name="get-length-of-content-in-the-request"></a><span data-ttu-id="9b120-594">Ottenere la lunghezza del contenuto nella richiesta</span><span class="sxs-lookup"><span data-stu-id="9b120-594">Get length of content in the request</span></span>

<span data-ttu-id="9b120-595">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-595">**Prototype**</span></span>

```c
UINT nx_http_server_content_length_get(NX_PACKET *packet_ptr);
```
<span data-ttu-id="9b120-596">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-596">**Description**</span></span>

<span data-ttu-id="9b120-597">Questo servizio tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="9b120-597">This service attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="9b120-598">Se non è presente alcun contenuto HTTP, questa routine restituisce un valore pari a zero.</span><span class="sxs-lookup"><span data-stu-id="9b120-598">If there is no HTTP content, this routine returns a value of zero.</span></span> <span data-ttu-id="9b120-599">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="9b120-599">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="9b120-600">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="9b120-600">This service is deprecated.</span></span> <span data-ttu-id="9b120-601">Gli sviluppatori sono invitati a eseguire la migrazione a nx_http_server_content_length_get_extended ().</span><span class="sxs-lookup"><span data-stu-id="9b120-601">Developers are encouraged to migrate to nx_http_server_content_length_get_extended().</span></span>

<span data-ttu-id="9b120-602">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-602">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-603">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-603">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="9b120-604">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="9b120-604">Note that this packet must not be released by the request notify callback.</span></span>

<span data-ttu-id="9b120-605">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-605">**Return Values**</span></span>

- <span data-ttu-id="9b120-606">**lunghezza contenuto** In errore, viene restituito un valore pari a zero</span><span class="sxs-lookup"><span data-stu-id="9b120-606">**content length** On error, a value of zero is returned</span></span>

<span data-ttu-id="9b120-607">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-607">**Allowed From**</span></span>

<span data-ttu-id="9b120-608">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-608">Threads</span></span>

<span data-ttu-id="9b120-609">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-609">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, get the content length of the HTTP Client request. */
length = nx_http_server_content_length_get(packet_ptr);

/* The “length” variable now contains the length of the HTTP Client
request content area. */
```

## <a name="nx_http_server_content_length_get_extended"></a><span data-ttu-id="9b120-610">nx_http_server_content_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="9b120-610">nx_http_server_content_length_get_extended</span></span>

### <a name="get-length-of-content-in-the-requestsupports-content-length-of-zero-value"></a><span data-ttu-id="9b120-611">Ottenere la lunghezza del contenuto nella richiesta/supporta la lunghezza del contenuto pari a zero valore</span><span class="sxs-lookup"><span data-stu-id="9b120-611">Get length of content in the request/supports Content Length of zero value</span></span>

<span data-ttu-id="9b120-612">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-612">**Prototype**</span></span>

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                               UINT *content_length);
```

<span data-ttu-id="9b120-613">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-613">**Description**</span></span>

<span data-ttu-id="9b120-614">Questo servizio è simile a *nx_http_server_content_length_get ()*; tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="9b120-614">This service is similar to *nx_http_server_content_length_get()*; attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="9b120-615">Tuttavia, il valore restituito indica lo stato di completamento corretto e il valore di lunghezza effettivo viene restituito nel puntatore di input content_length.</span><span class="sxs-lookup"><span data-stu-id="9b120-615">However, the return value indicates successful completion status, and the actual length value is returned in the input pointer content_length.</span></span> <span data-ttu-id="9b120-616">Se non è presente alcun contenuto HTTP/lunghezza contenuto = 0, questa routine restituisce ancora uno stato di completamento corretto e il puntatore di input content_length punta a una lunghezza valida (zero).</span><span class="sxs-lookup"><span data-stu-id="9b120-616">If there is no HTTP content/Content Length = 0, this routine still returns a successful completion status and the content_length input pointer points to a valid length (zero).</span></span> <span data-ttu-id="9b120-617">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="9b120-617">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="9b120-618">Questo servizio sostituisce *nx_http_server_content_length_get*().</span><span class="sxs-lookup"><span data-stu-id="9b120-618">This service replaces *nx_http_server_content_length_get*().</span></span>

<span data-ttu-id="9b120-619">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-619">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-620">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-620">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="9b120-621">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="9b120-621">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="9b120-622">**CONTENT_LENGTH** Puntatore al valore recuperato dal campo lunghezza contenuto</span><span class="sxs-lookup"><span data-stu-id="9b120-622">**content_length** Pointer to value retrieved from Content Length field</span></span>

<span data-ttu-id="9b120-623">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-623">**Return Values**</span></span>

- <span data-ttu-id="9b120-624">**NX_SUCCESS** (0x00) il contenuto del server http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="9b120-624">**NX_SUCCESS** (0x00) Successful HTTP Server content get</span></span>
- <span data-ttu-id="9b120-625">Formato dell'intestazione HTTP **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) non corretto</span><span class="sxs-lookup"><span data-stu-id="9b120-625">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Improper HTTP header format</span></span>
- <span data-ttu-id="9b120-626">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-626">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-627">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-627">**Allowed From**</span></span>

<span data-ttu-id="9b120-628">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-628">Threads</span></span>

<span data-ttu-id="9b120-629">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-629">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, get the content length of the HTTP Client request. */
ULONG content_length;

status = nx_http_server_content_length_get_extended(packet_ptr, &content_length);

/* If the “status” variable indicates successful completion, the“length” variable
contains the length of the HTTP Client request content area. */
```

## <a name="nx_http_server_create"></a><span data-ttu-id="9b120-630">nx_http_server_create</span><span class="sxs-lookup"><span data-stu-id="9b120-630">nx_http_server_create</span></span>

### <a name="create-an-http-server-instance"></a><span data-ttu-id="9b120-631">Creare un'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-631">Create an HTTP Server instance</span></span>

<span data-ttu-id="9b120-632">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-632">**Prototype**</span></span>

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

<span data-ttu-id="9b120-633">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-633">**Description**</span></span>

<span data-ttu-id="9b120-634">Questo servizio crea un'istanza del server HTTP, che viene eseguita nel contesto del proprio thread ThreadX.</span><span class="sxs-lookup"><span data-stu-id="9b120-634">This service creates an HTTP Server instance, which runs in the context of its own ThreadX thread.</span></span> <span data-ttu-id="9b120-635">Le routine di callback dell'applicazione *authentication_check* e *request_notify* facoltative forniscono al software dell'applicazione il controllo sulle operazioni di base del server http.</span><span class="sxs-lookup"><span data-stu-id="9b120-635">The optional *authentication_check* and *request_notify* application callback routines give the application software control over the basic operations of the HTTP Server.</span></span>

<span data-ttu-id="9b120-636">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-636">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-637">**http_server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-637">**http_server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="9b120-638">**http_server_name** Puntatore al nome del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-638">**http_server_name** Pointer to HTTP Server’s name.</span></span>
- <span data-ttu-id="9b120-639">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-639">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="9b120-640">**media_ptr** Puntatore a un'istanza del supporto FileX creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-640">**media_ptr** Pointer to previously created FileX media instance.</span></span>
- <span data-ttu-id="9b120-641">**stack_ptr** Puntatore all'area dello stack di thread del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-641">**stack_ptr** Pointer to HTTP Server thread stack area.</span></span>
- <span data-ttu-id="9b120-642">**stack_size** Puntatore alla dimensione dello stack del thread del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-642">**stack_size** Pointer to HTTP Server thread stack size.</span></span>
- <span data-ttu-id="9b120-643">**authentication_check** Puntatore a funzione per la routine di controllo dell'autenticazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-643">**authentication_check** Function pointer to application’s authentication checking routine.</span></span> <span data-ttu-id="9b120-644">Se specificato, questa routine viene chiamata per ogni richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-644">If specified, this routine is called for each HTTP Client request.</span></span> <span data-ttu-id="9b120-645">Se questo parametro è NULL, non verrà eseguita alcuna autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-645">If this parameter is NULL no authentication will be performed.</span></span>
- <span data-ttu-id="9b120-646">**request_notify** Puntatore della funzione alla routine di notifica della richiesta dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-646">**request_notify** Function pointer to application’s request notify routine.</span></span> <span data-ttu-id="9b120-647">Se specificato, questa routine viene chiamata prima dell'elaborazione del server HTTP della richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b120-647">If specified, this routine is called prior to the HTTP server processing of the request.</span></span> <span data-ttu-id="9b120-648">Questo consente di reindirizzare il nome della risorsa o i campi all'interno di una risorsa da aggiornare prima di completare la richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-648">This allows the resource name to be redirected or fields within a resource to be updated prior to completing the HTTP Client request.</span></span>

<span data-ttu-id="9b120-649">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-649">**Return Values**</span></span>

- <span data-ttu-id="9b120-650">Creazione del server HTTP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="9b120-650">**NX_SUCCESS** (0x00) Successful HTTP Server create.</span></span>
- <span data-ttu-id="9b120-651">NX_PTR_ERROR (0x07) server HTTP, IP, supporti, stack o puntatore al pool di pacchetti non validi.</span><span class="sxs-lookup"><span data-stu-id="9b120-651">NX_PTR_ERROR (0x07) Invalid HTTP Server, IP, media, stack, or packet pool pointer.</span></span>
- <span data-ttu-id="9b120-652">Il payload del pacchetto di NX_HTTP_POOL_ERROR (0xE9) del pool non è sufficiente per contenere la richiesta HTTP completa.</span><span class="sxs-lookup"><span data-stu-id="9b120-652">NX_HTTP_POOL_ERROR (0xE9) Packet payload of pool is not large enough to contain complete HTTP request.</span></span>

<span data-ttu-id="9b120-653">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-653">**Allowed From**</span></span>

<span data-ttu-id="9b120-654">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="9b120-654">Initialization, Threads</span></span>

<span data-ttu-id="9b120-655">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-655">**Example**</span></span>

```c
/* Create an HTTP Server instance called “my_server.” */
status = nx_http_server_create(&my_server, “my server”, &ip_0, &ram_disk,
                              stack_ptr, stack_size, &pool_0,
                              my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_http_server_delete"></a><span data-ttu-id="9b120-656">nx_http_server_delete</span><span class="sxs-lookup"><span data-stu-id="9b120-656">nx_http_server_delete</span></span>

### <a name="delete-an-http-server-instance"></a><span data-ttu-id="9b120-657">Eliminare un'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-657">Delete an HTTP Server instance</span></span>

<span data-ttu-id="9b120-658">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-658">**Prototype**</span></span>

```c
UINT nx_http_server_delete(NX_HTTP_SERVER *http_server_ptr);
```

<span data-ttu-id="9b120-659">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-659">**Description**</span></span>

<span data-ttu-id="9b120-660">Questo servizio Elimina un'istanza del server HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-660">This service deletes a previously created HTTP Server instance.</span></span>

<span data-ttu-id="9b120-661">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-661">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-662">**http_server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-662">**http_server_ptr** Pointer to HTTP Server control block.</span></span>

<span data-ttu-id="9b120-663">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-663">**Return Values**</span></span>

- <span data-ttu-id="9b120-664">Eliminazione del server HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="9b120-664">**NX_SUCCESS** (0x00) Successful HTTP Server delete</span></span>
- <span data-ttu-id="9b120-665">NX_PTR_ERROR (0x07) puntatore al server HTTP non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-665">NX_PTR_ERROR (0x07) Invalid HTTP Server pointer</span></span>
- <span data-ttu-id="9b120-666">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-666">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-667">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-667">**Allowed From**</span></span>

<span data-ttu-id="9b120-668">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-668">Threads</span></span>

<span data-ttu-id="9b120-669">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-669">**Example**</span></span>

```c
/* Delete the HTTP Server instance called “my_server.” */
status = nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a><span data-ttu-id="9b120-670">nx_http_server_get_entity_content</span><span class="sxs-lookup"><span data-stu-id="9b120-670">nx_http_server_get_entity_content</span></span>

### <a name="retrieve-the-location-and-length-of-entity-data"></a><span data-ttu-id="9b120-671">Recuperare il percorso e la lunghezza dei dati dell'entità</span><span class="sxs-lookup"><span data-stu-id="9b120-671">Retrieve the location and length of entity data</span></span>

<span data-ttu-id="9b120-672">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-672">**Prototype**</span></span>

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      ULONG *available_offset,
                                      ULONG *available_length);
```

<span data-ttu-id="9b120-673">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-673">**Description**</span></span>

<span data-ttu-id="9b120-674">Questo servizio determina la posizione dell'inizio dei dati all'interno dell'entità multiparte corrente nei messaggi client ricevuti e la lunghezza dei dati che non includono la stringa di limite.</span><span class="sxs-lookup"><span data-stu-id="9b120-674">This service determines the location of the start of data within the current multipart entity in the received Client messages, and the length of data not including the boundary string.</span></span> <span data-ttu-id="9b120-675">Il server HTTP interno aggiorna i propri offset in modo che questa funzione possa essere richiamata nello stesso datagramma client per i messaggi con più entità.</span><span class="sxs-lookup"><span data-stu-id="9b120-675">Internally HTTP server updates its own offsets so that this function can be called again on the same Client datagram for messages with multiple entities.</span></span> <span data-ttu-id="9b120-676">Il puntatore al pacchetto viene aggiornato al pacchetto successivo in cui il messaggio del client è un datagramma con più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9b120-676">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

<span data-ttu-id="9b120-677">Si noti che per usare questo servizio NX_HTTP_MULTIPART_ENABLE necessario abilitarlo.</span><span class="sxs-lookup"><span data-stu-id="9b120-677">Note that NX_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span>

<span data-ttu-id="9b120-678">Per ulteriori informazioni, vedere *nx_http_server_get_entity_header* .</span><span class="sxs-lookup"><span data-stu-id="9b120-678">See *nx_http_server_get_entity_header* for more details.</span></span>

<span data-ttu-id="9b120-679">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-679">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-680">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-680">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="9b120-681">**packet_pptr** Puntatore alla posizione del puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b120-681">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="9b120-682">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b120-682">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="9b120-683">**available_offset** Puntatore all'offset dei dati dell'entità dal puntatore a prependi del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9b120-683">**available_offset** Pointer to offset of entity data from the packet prepend pointer</span></span>
- <span data-ttu-id="9b120-684">**available_length** Puntatore alla lunghezza dei dati dell'entità</span><span class="sxs-lookup"><span data-stu-id="9b120-684">**available_length** Pointer to length of entity data</span></span>

<span data-ttu-id="9b120-685">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-685">**Return Values**</span></span>

- <span data-ttu-id="9b120-686">**NX_SUCCESS** (0x00) ha recuperato correttamente le dimensioni e la posizione del contenuto dell'entità</span><span class="sxs-lookup"><span data-stu-id="9b120-686">**NX_SUCCESS** (0x00) Successfully retrieved size and location of entity content</span></span>
- <span data-ttu-id="9b120-687">Il contenuto **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) per i marcatori multipart interni del server http è già stato trovato</span><span class="sxs-lookup"><span data-stu-id="9b120-687">**NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) Content for the HTTP server internal multipart markers is already found</span></span>
- <span data-ttu-id="9b120-688">Errore interno del server HTTP NX_HTTP_ERROR (0xE0)</span><span class="sxs-lookup"><span data-stu-id="9b120-688">NX_HTTP_ERROR (0xE0) HTTP Server internal error</span></span>
- <span data-ttu-id="9b120-689">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-689">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-690">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-690">**Allowed From**</span></span>

<span data-ttu-id="9b120-691">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-691">Threads</span></span>

<span data-ttu-id="9b120-692">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-692">**Example**</span></span>

```c
NX_HTTP_SERVER my_server;

UINT         offset, length;
NX_PACKET    *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
the entity header to determine details about the multipart data. If
successful, it then calls this service to get the location of entity data: */
status = nx_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
                                          &length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
entity data. */
```

## <a name="nx_http_server_get_entity_header"></a><span data-ttu-id="9b120-693">nx_http_server_get_entity_header</span><span class="sxs-lookup"><span data-stu-id="9b120-693">nx_http_server_get_entity_header</span></span>

### <a name="retrieve-the-contents-of-entity-header"></a><span data-ttu-id="9b120-694">Recupera il contenuto dell'intestazione dell'entità</span><span class="sxs-lookup"><span data-stu-id="9b120-694">Retrieve the contents of entity header</span></span>

<span data-ttu-id="9b120-695">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-695">**Prototype**</span></span>

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                     NX_PACKET **packet_pptr,
                                     UCHAR *entity_header_buffer,
                                     ULONG buffer_size);
```

<span data-ttu-id="9b120-696">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-696">**Description**</span></span>

<span data-ttu-id="9b120-697">Questo servizio recupera l'intestazione dell'entità nel buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="9b120-697">This service retrieves the entity header into the specified buffer.</span></span> <span data-ttu-id="9b120-698">Il server HTTP interno aggiorna i propri puntatori per individuare la prossima entità multipart in un datagramma client con più intestazioni di entità.</span><span class="sxs-lookup"><span data-stu-id="9b120-698">Internally HTTP Server updates its own pointers to locate the next multipart entity in a Client datagram with multiple entity headers.</span></span> <span data-ttu-id="9b120-699">Il puntatore al pacchetto viene aggiornato al pacchetto successivo in cui il messaggio del client è un datagramma con più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9b120-699">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

<span data-ttu-id="9b120-700">Si noti che per usare questo servizio NX_HTTP_MULTIPART_ENABLE necessario abilitarlo.</span><span class="sxs-lookup"><span data-stu-id="9b120-700">Note that NX_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span>

<span data-ttu-id="9b120-701">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-701">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-702">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-702">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="9b120-703">**packet_pptr** Puntatore alla posizione del puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b120-703">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="9b120-704">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b120-704">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="9b120-705">**entity_header_buffer** Puntatore alla posizione in cui archiviare l'intestazione dell'entità</span><span class="sxs-lookup"><span data-stu-id="9b120-705">**entity_header_buffer** Pointer to location to store entity header</span></span>
- <span data-ttu-id="9b120-706">**BUFFER_SIZE** Dimensioni del buffer di input</span><span class="sxs-lookup"><span data-stu-id="9b120-706">**buffer_size** Size of input buffer</span></span>

<span data-ttu-id="9b120-707">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-707">**Return Values**</span></span>

- <span data-ttu-id="9b120-708">**NX_SUCCESS** (0x00) ha recuperato correttamente l'intestazione dell'entità</span><span class="sxs-lookup"><span data-stu-id="9b120-708">**NX_SUCCESS** (0x00) Successfully retrieved entity heade</span></span>
- <span data-ttu-id="9b120-709">**NX_HTTP_NOT_FOUND (0xE6)** Campo di intestazione dell'entità non trovato</span><span class="sxs-lookup"><span data-stu-id="9b120-709">**NX_HTTP_NOT_FOUND (0xE6)** Entity header field not found</span></span>
- <span data-ttu-id="9b120-710">**NX_HTTP_TIMEOUT (0xE1)** Tempo scaduto per la ricezione del pacchetto successivo per il messaggio client Multipack</span><span class="sxs-lookup"><span data-stu-id="9b120-710">**NX_HTTP_TIMEOUT (0xE1)** Time expired to receive next packet for multipacket client message</span></span> 
- <span data-ttu-id="9b120-711">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-711">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-712">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-712">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="9b120-713">Errore HTTP interno NX_HTTP_ERROR (0xE0)</span><span class="sxs-lookup"><span data-stu-id="9b120-713">NX_HTTP_ERROR (0xE0) Internal HTTP error</span></span>

<span data-ttu-id="9b120-714">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-714">**Allowed From**</span></span>

<span data-ttu-id="9b120-715">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-715">Threads</span></span>

<span data-ttu-id="9b120-716">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-716">**Example**</span></span>

```c
/* my_request_notify* is the application request notify callback registered with
the HTTP server in *nx_http_server_create,* creates a response to the received
Client request. */

UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

NX_PACKET     *sresp_packet_ptr;
UINT          offset, length;**
NX_PACKET     *response_pkt;
UCHAR         buffer[1440];

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
             "Server: NetX HTTP 5.3\r\n");

    if(status == NX_SUCCESS)
    {
        if(nx_http_server_callback_packet_send(server_ptr, response_pkt) !=
                                              NX_SUCCESS)
        {
            nx_packet_release(response_pkt);
        }
    }
}
Else
{

        /* Indicate we have not processed the response to client yet.*/        
        return(NX_SUCCESS);
}

/* Indicate the response to client is transmitted. */
return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_gmt_callback_set"></a><span data-ttu-id="9b120-717">nx_http_server_gmt_callback_set</span><span class="sxs-lookup"><span data-stu-id="9b120-717">nx_http_server_gmt_callback_set</span></span>

### <a name="set-the-callback-to-obtain-gmt-date-and-time"></a><span data-ttu-id="9b120-718">Impostare il callback per ottenere la data e l'ora GMT</span><span class="sxs-lookup"><span data-stu-id="9b120-718">Set the callback to obtain GMT date and time</span></span>

<span data-ttu-id="9b120-719">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-719">**Prototype**</span></span>

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                                    VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

<span data-ttu-id="9b120-720">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-720">**Description**</span></span>

<span data-ttu-id="9b120-721">Questo servizio imposta il callback per ottenere la data e l'ora GMT con un server HTTP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-721">This service sets the callback to obtain GMT date and time with a previously created HTTP server.</span></span> <span data-ttu-id="9b120-722">Questo servizio viene richiamato con il server HTTP che sta creando un'intestazione nel server HTTP risposte al client.</span><span class="sxs-lookup"><span data-stu-id="9b120-722">This service is invoked with the HTTP server is creating a header in HTTP server responses to the Client.</span></span>

<span data-ttu-id="9b120-723">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-723">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-724">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-724">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="9b120-725">**gmt_get** Puntatore al callback GMT</span><span class="sxs-lookup"><span data-stu-id="9b120-725">**gmt_get** Pointer to GMT callback</span></span>
- <span data-ttu-id="9b120-726">**Data di scadenza** Puntatore alla data recuperata</span><span class="sxs-lookup"><span data-stu-id="9b120-726">**date** Pointer to the date retrieved</span></span>

<span data-ttu-id="9b120-727">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-727">**Return Values**</span></span>

- <span data-ttu-id="9b120-728">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="9b120-728">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="9b120-729">NX_PTR_ERROR (0x07) il puntatore al pacchetto o al parametro non è valido.</span><span class="sxs-lookup"><span data-stu-id="9b120-729">NX_PTR_ERROR (0x07) Invalid packet or parameter pointer.</span></span>

<span data-ttu-id="9b120-730">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-730">**Allowed From**</span></span>

<span data-ttu-id="9b120-731">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-731">Threads</span></span>

<span data-ttu-id="9b120-732">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-732">**Example**</span></span>

```c
NX_HTTP_SERVER my_server;

VOID get_gmt(NX_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_http_server_create, and before
starting HTTP services when nx_http_server_start is called, set the GMT
retrieve callback: */

status = nx_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
response header date. */
```

## <a name="nx_http_server_invalid_userpassword_notify_set"></a><span data-ttu-id="9b120-733">nx_http_server_invalid_userpassword_notify_set</span><span class="sxs-lookup"><span data-stu-id="9b120-733">nx_http_server_invalid_userpassword_notify_set</span></span>

### <a name="set-the-callback-to-to-handle-invalid-userpassword"></a><span data-ttu-id="9b120-734">Impostare il callback su per gestire l'utente o la password non valida</span><span class="sxs-lookup"><span data-stu-id="9b120-734">Set the callback to to handle invalid user/password</span></span>

<span data-ttu-id="9b120-735">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-735">**Prototype**</span></span>

```c
UINT nx_http_server_invalid_userpassword_notify_set(
     NX_HTTP_SERVER *http_server_ptr,
     UINT (*invalid_username_password_callback)
     (CHAR *resource,
     ULONG client_address,
     UINT request_type));
```

<span data-ttu-id="9b120-736">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-736">**Description**</span></span>

<span data-ttu-id="9b120-737">Questo servizio imposta il callback richiamato quando viene ricevuto un nome utente e una password non validi in una richiesta GET, put o Delete del client, mediante l'autenticazione digest o di base.</span><span class="sxs-lookup"><span data-stu-id="9b120-737">This service sets the callback invoked when an invalid username and password is received in a Client get, put or delete request, either by digest or basic authentication.</span></span> <span data-ttu-id="9b120-738">Il server HTTP deve essere creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-738">The HTTP server must be previously created.</span></span>

<span data-ttu-id="9b120-739">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-739">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-740">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-740">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="9b120-741">**invalid_username_password_callback** Puntatore a callback utente/pass non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-741">**invalid_username_password_callback** Pointer to invalid user/pass callback</span></span>
- <span data-ttu-id="9b120-742">**risorsa** di Puntatore alla risorsa specificata dal client</span><span class="sxs-lookup"><span data-stu-id="9b120-742">**resource** Pointer to the resource specified by the client</span></span>
- <span data-ttu-id="9b120-743">**CLIENT_ADDRESS** Indirizzo client</span><span class="sxs-lookup"><span data-stu-id="9b120-743">**client_address** Client address</span></span>
- <span data-ttu-id="9b120-744">**request_type** Indica il tipo di richiesta client.</span><span class="sxs-lookup"><span data-stu-id="9b120-744">**request_type** Indicates client request type.</span></span> <span data-ttu-id="9b120-745">Può essere:</span><span class="sxs-lookup"><span data-stu-id="9b120-745">May be:</span></span>
  - <span data-ttu-id="9b120-746">NX_HTTP_SERVER_GET_REQUEST</span><span class="sxs-lookup"><span data-stu-id="9b120-746">NX_HTTP_SERVER_GET_REQUEST</span></span>
  - <span data-ttu-id="9b120-747">NX_HTTP_SERVER_POST_REQUEST NX_HTTP_SERVER_HEAD_REQUEST</span><span class="sxs-lookup"><span data-stu-id="9b120-747">NX_HTTP_SERVER_POST_REQUEST NX_HTTP_SERVER_HEAD_REQUEST</span></span>
  - <span data-ttu-id="9b120-748">NX_HTTP_SERVER_PUT_REQUEST NX_HTTP_SERVER_DELETE_REQUEST</span><span class="sxs-lookup"><span data-stu-id="9b120-748">NX_HTTP_SERVER_PUT_REQUEST NX_HTTP_SERVER_DELETE_REQUEST</span></span>

<span data-ttu-id="9b120-749">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-749">**Return Values**</span></span>

- <span data-ttu-id="9b120-750">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="9b120-750">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="9b120-751">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-751">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-752">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-752">**Allowed From**</span></span>

<span data-ttu-id="9b120-753">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-753">Threads</span></span>

<span data-ttu-id="9b120-754">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-754">**Example**</span></span>

```c
NX_HTTP_SERVER my_server;
VOID invalid_username_password_callback (NX_ CHAR *resource,
                                        ULONG client_address,
                                        UINT request_type);

/* After the HTTP server is created by calling nx_http_server_create, and before
starting HTTP services when nx_http_server_start is called, set the invalid
username password callback: */

status = nx_http_server_gmt_callback_set(&my_server,
                                        invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_http_server_mime_maps_additional_set"></a><span data-ttu-id="9b120-755">nx_http_server_mime_maps_additional_set</span><span class="sxs-lookup"><span data-stu-id="9b120-755">nx_http_server_mime_maps_additional_set</span></span>

### <a name="set-additional-mime-maps-for-html"></a><span data-ttu-id="9b120-756">Impostare mappe MIME aggiuntive per HTML</span><span class="sxs-lookup"><span data-stu-id="9b120-756">Set additional MIME maps for HTML</span></span> 

<span data-ttu-id="9b120-757">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-757">**Prototype**</span></span>

```c
UINT nx_http_server_mime_maps_additional_set(
     NX_HTTP_SERVER *server_ptr,
     NX_HTTP_SERVER_MIME_MAP *mime_maps,
     UINT mime_maps_num);
```

<span data-ttu-id="9b120-758">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-758">**Description**</span></span>

<span data-ttu-id="9b120-759">Questo servizio consente allo sviluppatore di applicazioni HTTP di aggiungere altri tipi MIME dai tipi MIME predefiniti forniti dal server HTTP NetX (vedere *nx_http_server_get_type* per l'elenco dei tipi definiti).</span><span class="sxs-lookup"><span data-stu-id="9b120-759">This service allows the HTTP application developer to add additional MIME types from the default MIME types supplied by NetX HTTP Server (see *nx_http_server_get_type* for list of defined types).</span></span>

<span data-ttu-id="9b120-760">Quando viene ricevuta una richiesta client, ad esempio una richiesta GET, il server HTTP analizza il tipo di file richiesto dall'intestazione HTTP usando il set di mappe MIME aggiuntivo e, se non viene trovata alcuna corrispondenza, Cerca una corrispondenza nella mappa MIME predefinita del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-760">When a client request is received, e.g. a GET request, HTTP server parses the requested file type from the HTTP header using preferentially the additional MIME map set and if no match if found, it looks for a match in the default MIME map of the HTTP server.</span></span> <span data-ttu-id="9b120-761">Se non viene trovata alcuna corrispondenza, il valore predefinito del tipo MIME è "text/plain".</span><span class="sxs-lookup"><span data-stu-id="9b120-761">If no match is found, the MIME type defaults to “text/plain”.</span></span>

<span data-ttu-id="9b120-762">Se la funzione request Notify è registrata con il server HTTP, il callback della richiesta di notifica può chiamare *nx_http_server_type_get* per analizzare il tipo di file.</span><span class="sxs-lookup"><span data-stu-id="9b120-762">If the request notify function is registered with the HTTP server, the request notify callback can call *nx_http_server_type_get* to parse the file type.</span></span>

<span data-ttu-id="9b120-763">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-763">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-764">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-764">**server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="9b120-765">**mime_maps** Puntatore a una matrice di mappa MIME</span><span class="sxs-lookup"><span data-stu-id="9b120-765">**mime_maps** Pointer to a MIME map array</span></span>
- <span data-ttu-id="9b120-766">**mime_map_num** Numero di mappe MIME nella matrice</span><span class="sxs-lookup"><span data-stu-id="9b120-766">**mime_map_num** Number of MIME maps in array</span></span>

<span data-ttu-id="9b120-767">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-767">**Return Values**</span></span>

- <span data-ttu-id="9b120-768">Set di mappe MIME del server HTTP con **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="9b120-768">**NX_SUCCESS** (0x00) Successful HTTP Server MIME map set</span></span>
- <span data-ttu-id="9b120-769">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-769">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-770">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-770">**Allowed From**</span></span>

<span data-ttu-id="9b120-771">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="9b120-771">Initialization, Threads</span></span>

<span data-ttu-id="9b120-772">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-772">**Example**</span></span>

```c
/* my_server is an NX_HTTP_SERVER previously created. */

NX_HTTP_SERVER_MIME_MAP my_mime_maps [2];

static NX_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc", "yourtype/abc"},
    {"xyz", "mytype/xyz"},
};

status = nx_http_server_mime_maps_additional_set(&my_server,
                                                &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP
server MIME map set.” */
```

## <a name="nx_http_server_packet_content_find"></a><span data-ttu-id="9b120-773">nx_http_server_packet_content_find</span><span class="sxs-lookup"><span data-stu-id="9b120-773">nx_http_server_packet_content_find</span></span>

### <a name="extract-content-length-and-set-pointer-to-start-of-data"></a><span data-ttu-id="9b120-774">Estrarre la lunghezza del contenuto e impostare il puntatore all'inizio dei dati</span><span class="sxs-lookup"><span data-stu-id="9b120-774">Extract content length and set pointer to start of data</span></span>

<span data-ttu-id="9b120-775">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-775">**Prototype**</span></span>

```c
UINT nx_http_server_packet_content_find(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_ptr,
                                       UINT *content_length);
```

<span data-ttu-id="9b120-776">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-776">**Description**</span></span>

<span data-ttu-id="9b120-777">Questo servizio estrae la lunghezza del contenuto dall'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-777">This service extracts the content length from the HTTP header.</span></span> <span data-ttu-id="9b120-778">Aggiorna inoltre il pacchetto fornito come indicato di seguito: il puntatore del pacchetto Prepend (inizio della posizione del buffer dei pacchetti in cui scrivere) viene impostato sul contenuto HTTP (dati) appena passata l'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-778">It also updates the supplied packet as follows: the packet prepend pointer (start of location of packet buffer to write to) is set to the HTTP content (data) just passed the HTTP header.</span></span>

<span data-ttu-id="9b120-779">Se l'inizio del contenuto non viene trovato nel pacchetto corrente, la funzione attende la ricezione del pacchetto successivo utilizzando l'opzione NX_HTTP_SERVER_TIMEOUT_RECEIVE wait.</span><span class="sxs-lookup"><span data-stu-id="9b120-779">If the beginning of content is not found in the current packet, the function waits for the next packet to be received using the NX_HTTP_SERVER_TIMEOUT_RECEIVE wait option.</span></span>

<span data-ttu-id="9b120-780">Si noti che questo metodo non deve essere chiamato prima di chiamare *nx_http_server_get_entity_header ()* perché modifica il puntatore anteposto dopo l'intestazione dell'entità.</span><span class="sxs-lookup"><span data-stu-id="9b120-780">Note this should not be called before calling *nx_http_server_get_entity_header()* because it modifies the prepend pointer past the entity header.</span></span>

<span data-ttu-id="9b120-781">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-781">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-782">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-782">**server_ptr** Pointer to HTTP server instance</span></span>
- <span data-ttu-id="9b120-783">**packet_ptr** Puntatore al puntatore del pacchetto per la restituzione del pacchetto con puntatore anteposto aggiornato</span><span class="sxs-lookup"><span data-stu-id="9b120-783">**packet_ptr** Pointer to packet pointer for returning the packet with updated prepend pointer</span></span>
- <span data-ttu-id="9b120-784">**CONTENT_LENGTH** Puntatore a content_length estratte</span><span class="sxs-lookup"><span data-stu-id="9b120-784">**content_length** Pointer to extracted content_length</span></span>

<span data-ttu-id="9b120-785">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-785">**Return Values**</span></span>

- <span data-ttu-id="9b120-786">È stata trovata la lunghezza del contenuto HTTP **NX_SUCCESS** (0x00) e l'aggiornamento del pacchetto è riuscito</span><span class="sxs-lookup"><span data-stu-id="9b120-786">**NX_SUCCESS** (0x00) HTTP content length found and packet successfully updated</span></span>
- <span data-ttu-id="9b120-787">Tempo di **NX_HTTP_TIMEOUT** (0xE1) scaduto in attesa del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="9b120-787">**NX_HTTP_TIMEOUT** (0xE1) Time expired waiting on next packet</span></span>
- <span data-ttu-id="9b120-788">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-788">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-789">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-789">**Allowed From**</span></span>

<span data-ttu-id="9b120-790">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-790">Threads</span></span>

<span data-ttu-id="9b120-791">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-791">**Example**</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
The server has received a Client request packet, recv_packet_ptr, and the packet
content find service is called from the request notify callback function 
registere with the HTTP server. */

UINT content_length;

status = nx_http_server_packet_content_find(server_ptr, recv_packet_ptr,
                                           &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_http_server_packet_get"></a><span data-ttu-id="9b120-792">nx_http_server_packet_get</span><span class="sxs-lookup"><span data-stu-id="9b120-792">nx_http_server_packet_get</span></span>

### <a name="receive-the-next-http-packet"></a><span data-ttu-id="9b120-793">Ricevere il pacchetto HTTP successivo</span><span class="sxs-lookup"><span data-stu-id="9b120-793">Receive the next HTTP packet</span></span>

<span data-ttu-id="9b120-794">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-794">**Prototype**</span></span>

```c
UINT nx_http_server_packet_get(NX_HTTP_SERVER *server_ptr,
                              NX_PACKET **packet_ptr);
```

<span data-ttu-id="9b120-795">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-795">**Description**</span></span>

<span data-ttu-id="9b120-796">Questo servizio restituisce il pacchetto successivo ricevuto sul socket del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-796">This service returns the next packet received on the HTTP server socket.</span></span> <span data-ttu-id="9b120-797">L'opzione Attendi per la ricezione di un pacchetto è NX_HTTP_SERVER_TIMEOUT_RECEIVE.</span><span class="sxs-lookup"><span data-stu-id="9b120-797">The wait option to receive a packet is NX_HTTP_SERVER_TIMEOUT_RECEIVE.</span></span>

<span data-ttu-id="9b120-798">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-798">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-799">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-799">**server_ptr** Pointer to HTTP server instance</span></span>
- <span data-ttu-id="9b120-800">**packet_ptr** Puntatore al pacchetto ricevuto</span><span class="sxs-lookup"><span data-stu-id="9b120-800">**packet_ptr** Pointer to received packet</span></span>

<span data-ttu-id="9b120-801">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-801">**Return Values**</span></span>

- <span data-ttu-id="9b120-802">**NX_SUCCESS** (0x00) ha ricevuto il pacchetto http successivo</span><span class="sxs-lookup"><span data-stu-id="9b120-802">**NX_SUCCESS** (0x00) Successfully received next HTTP packet</span></span>
- <span data-ttu-id="9b120-803">Tempo di **NX_HTTP_TIMEOUT** (0xE1) scaduto in attesa del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="9b120-803">**NX_HTTP_TIMEOUT** (0xE1) Time expired waiting on next packet</span></span>
- <span data-ttu-id="9b120-804">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-804">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-805">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-805">**Allowed From**</span></span>

<span data-ttu-id="9b120-806">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-806">Threads</span></span>

<span data-ttu-id="9b120-807">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-807">**Example**</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started. */

UINT content_length;
NX_PACKET *recv_packet_ptr;

status = nx_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_http_server_param_get"></a><span data-ttu-id="9b120-808">nx_http_server_param_get</span><span class="sxs-lookup"><span data-stu-id="9b120-808">nx_http_server_param_get</span></span>

### <a name="get-parameter-from-the-request"></a><span data-ttu-id="9b120-809">Ottenere il parametro dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="9b120-809">Get parameter from the request</span></span>

<span data-ttu-id="9b120-810">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-810">**Prototype**</span></span>

```c
UINT nx_http_server_param_get(NX_PACKET *packet_ptr,
                             UINT param_number, CHAR *param_ptr,
                             UINT max_param_size);
```

<span data-ttu-id="9b120-811">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-811">**Description**</span></span>

<span data-ttu-id="9b120-812">Questo servizio tenta di recuperare il parametro URL HTTP specificato nel pacchetto di richiesta fornito.</span><span class="sxs-lookup"><span data-stu-id="9b120-812">This service attempts to retrieve the specified HTTP URL parameter in the supplied request packet.</span></span> <span data-ttu-id="9b120-813">Se il parametro HTTP richiesto non è presente, questa routine restituisce lo stato NX_HTTP_NOT_FOUND.</span><span class="sxs-lookup"><span data-stu-id="9b120-813">If the requested HTTP parameter is not present, this routine returns a status of NX_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="9b120-814">Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="9b120-814">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="9b120-815">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-815">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-816">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-816">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="9b120-817">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b120-817">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="9b120-818">**param_number** Numero logico del parametro a partire da zero, da sinistra a destra nell'elenco dei parametri.</span><span class="sxs-lookup"><span data-stu-id="9b120-818">**param_number** Logical number of the parameter starting at zero, from left to right in the parameter list.</span></span>
- <span data-ttu-id="9b120-819">**param_ptr** Area di destinazione per copiare il parametro.</span><span class="sxs-lookup"><span data-stu-id="9b120-819">**param_ptr** Destination area to copy the parameter.</span></span>
- <span data-ttu-id="9b120-820">**max_param_size** Dimensioni massime dell'area di destinazione del parametro.</span><span class="sxs-lookup"><span data-stu-id="9b120-820">**max_param_size** Maximum size of the parameter destination area.</span></span>

<span data-ttu-id="9b120-821">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-821">**Return Values**</span></span>

- <span data-ttu-id="9b120-822">**NX_SUCCESS** (0x00) parametro Server http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="9b120-822">**NX_SUCCESS** (0x00) Successful HTTP Server parameter get</span></span>
- <span data-ttu-id="9b120-823">Il parametro specificato **NX_HTTP_NOT_FOUND** (0xE6) non è stato trovato</span><span class="sxs-lookup"><span data-stu-id="9b120-823">**NX_HTTP_NOT_FOUND** (0xE6) Specified parameter not found</span></span>
- <span data-ttu-id="9b120-824">Il parametro della richiesta **NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xf3) non è terminato correttamente</span><span class="sxs-lookup"><span data-stu-id="9b120-824">**NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) Request parameter not properly terminated</span></span>
- <span data-ttu-id="9b120-825">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-825">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-826">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-826">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-827">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-827">**Allowed From**</span></span>

<span data-ttu-id="9b120-828">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-828">Threads</span></span>

<span data-ttu-id="9b120-829">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-829">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, get the first parameter of the HTTP Client request. */

status = nx_http_server_param_get(request_packet_ptr, 0, param_destination, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
in “param_destination.” */
```

## <a name="nx_http_server_query_get"></a><span data-ttu-id="9b120-830">nx_http_server_query_get</span><span class="sxs-lookup"><span data-stu-id="9b120-830">nx_http_server_query_get</span></span>

### <a name="get-query-from-the-request"></a><span data-ttu-id="9b120-831">Ottenere una query dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="9b120-831">Get query from the request</span></span>

<span data-ttu-id="9b120-832">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-832">**Prototype**</span></span>

```c
UINT nx_http_server_query_get(NX_PACKET *packet_ptr, UINT query_number,
                             CHAR *query_ptr, UINT max_query_size);
```

<span data-ttu-id="9b120-833">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-833">**Description**</span></span>

<span data-ttu-id="9b120-834">Questo servizio tenta di recuperare la query URL HTTP specificata nel pacchetto di richiesta fornito.</span><span class="sxs-lookup"><span data-stu-id="9b120-834">This service attempts to retrieve the specified HTTP URL query in the supplied request packet.</span></span> <span data-ttu-id="9b120-835">Se la query HTTP richiesta non è presente, questa routine restituisce lo stato NX_HTTP_NOT_FOUND.</span><span class="sxs-lookup"><span data-stu-id="9b120-835">If the requested HTTP query is not present, this routine returns a status of NX_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="9b120-836">Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="9b120-836">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="9b120-837">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-837">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-838">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-838">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="9b120-839">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b120-839">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="9b120-840">**query_number** Numero logico del parametro a partire da zero, da sinistra a destra nell'elenco di query.</span><span class="sxs-lookup"><span data-stu-id="9b120-840">**query_number** Logical number of the parameter starting at zero, from left to right in the query list.</span></span>
- <span data-ttu-id="9b120-841">**query_ptr** Area di destinazione per la copia della query.</span><span class="sxs-lookup"><span data-stu-id="9b120-841">**query_ptr** Destination area to copy the query.</span></span>
- <span data-ttu-id="9b120-842">**max_query_size** Dimensioni massime dell'area di destinazione della query.</span><span class="sxs-lookup"><span data-stu-id="9b120-842">**max_query_size** Maximum size of the query destination area.</span></span>

<span data-ttu-id="9b120-843">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-843">**Return Values**</span></span>

- <span data-ttu-id="9b120-844">**NX_SUCCESS** (0x00) query del server http riuscita Get</span><span class="sxs-lookup"><span data-stu-id="9b120-844">**NX_SUCCESS** (0x00) Successful HTTP Server query get</span></span>
- <span data-ttu-id="9b120-845">Dimensioni della query di **NX_HTTP_FAILED** (0xe2) troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="9b120-845">**NX_HTTP_FAILED** (0xE2) Query size too small.</span></span>
- <span data-ttu-id="9b120-846">Impossibile trovare la query specificata **NX_HTTP_NOT_FOUND** (0xE6)</span><span class="sxs-lookup"><span data-stu-id="9b120-846">**NX_HTTP_NOT_FOUND** (0xE6) Specified query not found</span></span>
- <span data-ttu-id="9b120-847">**NX_HTTP_NO_QUERY_PARSED** (0XF2) nessuna query nella richiesta client</span><span class="sxs-lookup"><span data-stu-id="9b120-847">**NX_HTTP_NO_QUERY_PARSED** (0xF2) No query in Client request</span></span>
- <span data-ttu-id="9b120-848">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-848">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-849">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-849">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-850">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-850">**Allowed From**</span></span>

<span data-ttu-id="9b120-851">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-851">Threads</span></span>

<span data-ttu-id="9b120-852">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-852">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, get the first query of the HTTP Client request. */
status = nx_http_server_query_get(request_packet_ptr, 0, query_destination, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
in “query_destination.” */
```

##   
<span data-ttu-id="9b120-853">nx_http_server_start</span><span class="sxs-lookup"><span data-stu-id="9b120-853">nx_http_server_start</span></span>

### <a name="start-the-http-server"></a><span data-ttu-id="9b120-854">Avviare il server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-854">Start the HTTP Server</span></span>

<span data-ttu-id="9b120-855">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-855">**Prototype**</span></span>

```c
UINT nx_http_server_start(NX_HTTP_SERVER *http_server_ptr);
```

<span data-ttu-id="9b120-856">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-856">**Description**</span></span>

<span data-ttu-id="9b120-857">Questo servizio avvia l'istanza del server HTTP create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-857">This service starts the previously create HTTP Server instance.</span></span>

<span data-ttu-id="9b120-858">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-858">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-859">**http_server_ptr** Puntatore all'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-859">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

<span data-ttu-id="9b120-860">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-860">**Return Values**</span></span>

- <span data-ttu-id="9b120-861">Inizio del server HTTP **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="9b120-861">**NX_SUCCESS** (0x00) Successful HTTP Server start</span></span>
- <span data-ttu-id="9b120-862">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-862">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-863">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-863">**Allowed From**</span></span>

<span data-ttu-id="9b120-864">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="9b120-864">Initialization, Threads</span></span>

<span data-ttu-id="9b120-865">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-865">**Example**</span></span>

```c
/* Start the HTTP Server instance “my_server.” */
status = nx_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_http_server_stop"></a><span data-ttu-id="9b120-866">nx_http_server_stop</span><span class="sxs-lookup"><span data-stu-id="9b120-866">nx_http_server_stop</span></span>

### <a name="stop-the-http-server"></a><span data-ttu-id="9b120-867">Arrestare il server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-867">Stop the HTTP Server</span></span>

<span data-ttu-id="9b120-868">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-868">**Prototype**</span></span>

```c
UINT nx_http_server_stop(NX_HTTP_SERVER *http_server_ptr);
```

<span data-ttu-id="9b120-869">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-869">**Description**</span></span>

<span data-ttu-id="9b120-870">Questo servizio arresta l'istanza del server HTTP create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-870">This service stops the previously create HTTP Server instance.</span></span> <span data-ttu-id="9b120-871">Questa routine deve essere chiamata prima di eliminare un'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-871">This routine should be called prior to deleting an HTTP Server instance.</span></span>

<span data-ttu-id="9b120-872">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-872">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-873">**http_server_ptr** Puntatore all'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b120-873">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

<span data-ttu-id="9b120-874">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-874">**Return Values**</span></span>

- <span data-ttu-id="9b120-875">Interruzione del server HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="9b120-875">**NX_SUCCESS** (0x00) Successful HTTP Server stop</span></span>
- <span data-ttu-id="9b120-876">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-876">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-877">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="9b120-877">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="9b120-878">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-878">**Allowed From**</span></span>

<span data-ttu-id="9b120-879">Thread</span><span class="sxs-lookup"><span data-stu-id="9b120-879">Threads</span></span>

<span data-ttu-id="9b120-880">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-880">**Example**</span></span>

```c
/* Stop the HTTP Server instance “my_server.” */

status = nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a><span data-ttu-id="9b120-881">nx_http_server_type_get</span><span class="sxs-lookup"><span data-stu-id="9b120-881">nx_http_server_type_get</span></span>

### <a name="extract-file-type-from-client-http-request"></a><span data-ttu-id="9b120-882">Estrai il tipo di file dalla richiesta HTTP client</span><span class="sxs-lookup"><span data-stu-id="9b120-882">Extract file type from Client HTTP request</span></span>

<span data-ttu-id="9b120-883">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-883">**Prototype**</span></span>

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                            CHAR *name, CHAR *http_type_string);
```

<span data-ttu-id="9b120-884">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-884">**Description**</span></span>

<span data-ttu-id="9b120-885">Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la sua lunghezza nel valore restituito dal *nome* del buffer di input, in genere l'URL.</span><span class="sxs-lookup"><span data-stu-id="9b120-885">This service extracts the HTTP request type in the buffer *http_type_string* and its length in the return value from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="9b120-886">Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene impostato il tipo "text/plain".</span><span class="sxs-lookup"><span data-stu-id="9b120-886">If no MIME map is found, it defaults to the “text/plain” type.</span></span> <span data-ttu-id="9b120-887">In caso contrario, confronta il tipo Estratto con le mappe MIME predefinite del server HTTP per una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-887">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="9b120-888">Le mappe MIME predefinite nel server HTTP NetX sono:</span><span class="sxs-lookup"><span data-stu-id="9b120-888">The default MIME maps in NetX HTTP Server are:</span></span>

- <span data-ttu-id="9b120-889">testo HTML/HTML</span><span class="sxs-lookup"><span data-stu-id="9b120-889">html text/html</span></span>
- <span data-ttu-id="9b120-890">testo htm/html</span><span class="sxs-lookup"><span data-stu-id="9b120-890">htm text/html</span></span>
- <span data-ttu-id="9b120-891">testo txt/normale</span><span class="sxs-lookup"><span data-stu-id="9b120-891">txt text/plain</span></span>
- <span data-ttu-id="9b120-892">immagine gif/gif</span><span class="sxs-lookup"><span data-stu-id="9b120-892">gif image/gif</span></span>
- <span data-ttu-id="9b120-893">immagine jpg/jpeg</span><span class="sxs-lookup"><span data-stu-id="9b120-893">jpg image/jpeg</span></span>
- <span data-ttu-id="9b120-894">icona immagine ICO/x</span><span class="sxs-lookup"><span data-stu-id="9b120-894">ico image/x-icon</span></span>

<span data-ttu-id="9b120-895">Se specificato, verrà inoltre cercato un set definito dall'utente di mappe MIME aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="9b120-895">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="9b120-896">Per ulteriori informazioni sulle mappe definite dall'utente, vedere *nx_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="9b120-896">See *nx_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="9b120-897">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="9b120-897">This service is deprecated.</span></span> <span data-ttu-id="9b120-898">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_http_server_type_get_extended ().*</span><span class="sxs-lookup"><span data-stu-id="9b120-898">Developers are encouraged to migrate to *nx_http_server_type_get_extended().*</span></span>

<span data-ttu-id="9b120-899">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-899">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-900">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-900">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="9b120-901">**nome** Puntatore al buffer in cui eseguire la ricerca</span><span class="sxs-lookup"><span data-stu-id="9b120-901">**name** Pointer to buffer to search</span></span>
- <span data-ttu-id="9b120-902">**http_type_string** (puntatore al tipo HTML Estratto)</span><span class="sxs-lookup"><span data-stu-id="9b120-902">**http_type_string** (Pointer to extracted HTML type)</span></span>

<span data-ttu-id="9b120-903">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-903">**Return Values**</span></span>

- <span data-ttu-id="9b120-904">**Lunghezza della stringa in byte** Il valore diverso da zero è Success</span><span class="sxs-lookup"><span data-stu-id="9b120-904">**Length of string in bytes** Non zero value is success</span></span>
- <span data-ttu-id="9b120-905">**Zero indica un errore**</span><span class="sxs-lookup"><span data-stu-id="9b120-905">**Zero indicates error**</span></span>

<span data-ttu-id="9b120-906">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-906">**Allowed From**</span></span>

<span data-ttu-id="9b120-907">Applicazione</span><span class="sxs-lookup"><span data-stu-id="9b120-907">Application</span></span>

<span data-ttu-id="9b120-908">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-908">**Example**</span></span>

```c
/* my_server is a previously created HTTP server, which starts accepting 
client requests when *nx_http_server_start* is called*/

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
string_length = nx_http_server_type_get(&my_server_ptr,
                my_server.nx_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
```

<span data-ttu-id="9b120-909">Per un esempio più dettagliato, vedere la descrizione di</span><span class="sxs-lookup"><span data-stu-id="9b120-909">For a more detailed example, see the description for</span></span>

<span data-ttu-id="9b120-910">*nx_http_server_callback_generate_response_header.*</span><span class="sxs-lookup"><span data-stu-id="9b120-910">*nx_http_server_callback_generate_response_header.*</span></span>

## <a name="nx_http_server_type_get_extended"></a><span data-ttu-id="9b120-911">nx_http_server_type_get_extended</span><span class="sxs-lookup"><span data-stu-id="9b120-911">nx_http_server_type_get_extended</span></span>

### <a name="extract-file-type-from-client-http-request"></a><span data-ttu-id="9b120-912">Estrai il tipo di file dalla richiesta HTTP client</span><span class="sxs-lookup"><span data-stu-id="9b120-912">Extract file type from Client HTTP request</span></span>

<span data-ttu-id="9b120-913">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-913">**Prototype**</span></span>

```c
UINT nx_http_server_type_get_extended(
     NX_HTTP_SERVER *http_server_ptr,
     CHAR *name, CHAR *http_type_string,
     UINT http_type_string_max_size);
```

<span data-ttu-id="9b120-914">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-914">**Description**</span></span>

<span data-ttu-id="9b120-915">Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la sua lunghezza nel valore restituito dal *nome* del buffer di input, in genere l'URL.</span><span class="sxs-lookup"><span data-stu-id="9b120-915">This service extracts the HTTP request type in the buffer *http_type_string* and its length in the return value from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="9b120-916">Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene impostato il tipo "text/plain".</span><span class="sxs-lookup"><span data-stu-id="9b120-916">If no MIME map is found, it defaults to the “text/plain” type.</span></span> <span data-ttu-id="9b120-917">In caso contrario, confronta il tipo Estratto con le mappe MIME predefinite del server HTTP per una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="9b120-917">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="9b120-918">Le mappe MIME predefinite nel server HTTP NetX Duo sono:</span><span class="sxs-lookup"><span data-stu-id="9b120-918">The default MIME maps in NetX Duo HTTP Server are:</span></span>

- <span data-ttu-id="9b120-919">testo HTML/HTML</span><span class="sxs-lookup"><span data-stu-id="9b120-919">html text/html</span></span>
- <span data-ttu-id="9b120-920">testo htm/html</span><span class="sxs-lookup"><span data-stu-id="9b120-920">htm text/html</span></span>
- <span data-ttu-id="9b120-921">testo txt/normale</span><span class="sxs-lookup"><span data-stu-id="9b120-921">txt text/plain</span></span>
- <span data-ttu-id="9b120-922">immagine gif/gif</span><span class="sxs-lookup"><span data-stu-id="9b120-922">gif image/gif</span></span>
- <span data-ttu-id="9b120-923">immagine jpg/jpeg</span><span class="sxs-lookup"><span data-stu-id="9b120-923">jpg image/jpeg</span></span>
- <span data-ttu-id="9b120-924">icona immagine ICO/x</span><span class="sxs-lookup"><span data-stu-id="9b120-924">ico image/x-icon</span></span>

<span data-ttu-id="9b120-925">Se specificato, verrà inoltre cercato un set definito dall'utente di mappe MIME aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="9b120-925">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="9b120-926">Per ulteriori informazioni sulle mappe definite dall'utente, vedere *nx_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="9b120-926">See *nx_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="9b120-927">Questo servizio sostituisce *nx_http_server_type_get ().*</span><span class="sxs-lookup"><span data-stu-id="9b120-927">This service replaces *nx_http_server_type_get().*</span></span> <span data-ttu-id="9b120-928">Questa versione fornisce informazioni aggiuntive sulla lunghezza.</span><span class="sxs-lookup"><span data-stu-id="9b120-928">This version supplies additional length information.</span></span>

<span data-ttu-id="9b120-929">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-929">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-930">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-930">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="9b120-931">**nome** Puntatore al buffer in cui eseguire la ricerca</span><span class="sxs-lookup"><span data-stu-id="9b120-931">**name** Pointer to buffer to search</span></span>
- <span data-ttu-id="9b120-932">**name_length** Lunghezza del buffer da cercare</span><span class="sxs-lookup"><span data-stu-id="9b120-932">**name_length** Length of buffer to search</span></span>
- <span data-ttu-id="9b120-933">**http_type_string** (puntatore al tipo HTML Estratto)</span><span class="sxs-lookup"><span data-stu-id="9b120-933">**http_type_string** (Pointer to extracted HTML type)</span></span>
- <span data-ttu-id="9b120-934">**http_type_string_max_size**</span><span class="sxs-lookup"><span data-stu-id="9b120-934">**http_type_string_max_size**</span></span>

<span data-ttu-id="9b120-935">Dimensioni del buffer di *http_type_string*</span><span class="sxs-lookup"><span data-stu-id="9b120-935">Size of the *http_type_string* buffer</span></span>

<span data-ttu-id="9b120-936">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-936">**Return Values**</span></span>

- <span data-ttu-id="9b120-937">**Lunghezza della stringa in byte** Il valore diverso da zero è Success</span><span class="sxs-lookup"><span data-stu-id="9b120-937">**Length of string in bytes** Non zero value is success</span></span><br /><span data-ttu-id="9b120-938">Zero indica un errore</span><span class="sxs-lookup"><span data-stu-id="9b120-938">Zero indicates error</span></span>

<span data-ttu-id="9b120-939">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-939">**Allowed From**</span></span>

<span data-ttu-id="9b120-940">Applicazione</span><span class="sxs-lookup"><span data-stu-id="9b120-940">Application</span></span>

<span data-ttu-id="9b120-941">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-941">**Example**</span></span>

```c
/* my_server is a previously created HTTP server, which starts accepting 
client requests when *nx_http_server_start* is called*/

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
string_length = nx_http_server_type_get_extended(&my_server,
                my_server.nx_http_server_request_resource, resource_length,
                temp_string, sizeof(temp_string));

/* If string_length is non zero, the HTTP string is extracted. */
```

<span data-ttu-id="9b120-942">Per un esempio più dettagliato, vedere la descrizione di</span><span class="sxs-lookup"><span data-stu-id="9b120-942">For a more detailed example, see the description for</span></span>

<span data-ttu-id="9b120-943">*nx_http_server_callback_generate_response_header.*</span><span class="sxs-lookup"><span data-stu-id="9b120-943">*nx_http_server_callback_generate_response_header.*</span></span>

## <a name="nx_http_server_digest_authenticate_notify_set"></a><span data-ttu-id="9b120-944">nx_http_server_digest_authenticate_notify_set</span><span class="sxs-lookup"><span data-stu-id="9b120-944">nx_http_server_digest_authenticate_notify_set</span></span>

### <a name="set-digest-authenticate-callback-function"></a><span data-ttu-id="9b120-945">Imposta funzione di callback autenticazione digest</span><span class="sxs-lookup"><span data-stu-id="9b120-945">Set digest authenticate callback function</span></span>

<span data-ttu-id="9b120-946">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-946">**Prototype**</span></span>

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

<span data-ttu-id="9b120-947">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-947">**Description**</span></span>

<span data-ttu-id="9b120-948">Questo servizio imposta il callback richiamato quando viene eseguita l'autenticazione del digest.</span><span class="sxs-lookup"><span data-stu-id="9b120-948">This service sets the callback invoked when digest authenticate is performed.</span></span>

<span data-ttu-id="9b120-949">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-949">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-950">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-950">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="9b120-951">**digest_authenticate_callback** Puntatore al callback di autenticazione del digest</span><span class="sxs-lookup"><span data-stu-id="9b120-951">**digest_authenticate_callback** Pointer to digest authenticate callback</span></span>

<span data-ttu-id="9b120-952">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-952">**Return Values**</span></span>

- <span data-ttu-id="9b120-953">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="9b120-953">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="9b120-954">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-954">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="9b120-955">Autenticazione del digest NX_NOT_SUPPORTED (0x4B) non abilitata</span><span class="sxs-lookup"><span data-stu-id="9b120-955">NX_NOT_SUPPORTED (0x4B) Digest authenticate not enabled</span></span>

<span data-ttu-id="9b120-956">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-956">**Allowed From**</span></span>

<span data-ttu-id="9b120-957">Applicazione</span><span class="sxs-lookup"><span data-stu-id="9b120-957">Application</span></span>

<span data-ttu-id="9b120-958">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-958">**Example**</span></span>

```c
UINT digest_authenticate_callback(NX_HTTP_SERVER *server_ptr, CHAR *name_ptr,
                                 CHAR *realm_ptr, CHAR *password_ptr,
                                 CHAR *method,CHAR *authorization_uri,
                                 CHAR *authorization_nc,
                                 CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and
before starting HTTP services when nx_http_server_start is called, set the
digest authenticate callback: */

status = nx_http_server_digest_authenticate_notify_set (&my_server,
                                                       digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_http_server_authentication_check_set"></a><span data-ttu-id="9b120-959">nx_http_server_authentication_check_set</span><span class="sxs-lookup"><span data-stu-id="9b120-959">nx_http_server_authentication_check_set</span></span>

### <a name="set-authentication-checking-callback-function"></a><span data-ttu-id="9b120-960">Imposta la funzione di callback per il controllo dell'autenticazione</span><span class="sxs-lookup"><span data-stu-id="9b120-960">Set authentication checking callback function</span></span>

<span data-ttu-id="9b120-961">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="9b120-961">**Prototype**</span></span>

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

<span data-ttu-id="9b120-962">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9b120-962">**Description**</span></span>

<span data-ttu-id="9b120-963">Questo servizio imposta la funzione di callback del controllo dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="9b120-963">This service sets the callback function of authentication checking.</span></span>

<span data-ttu-id="9b120-964">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="9b120-964">**Input Parameters**</span></span>

- <span data-ttu-id="9b120-965">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="9b120-965">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="9b120-966">**authentication_check_extended** Puntatore al controllo di autenticazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9b120-966">**authentication_check_extended** Pointer to application’s authentication checking</span></span>

<span data-ttu-id="9b120-967">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="9b120-967">**Return Values**</span></span>

- <span data-ttu-id="9b120-968">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="9b120-968">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="9b120-969">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9b120-969">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="9b120-970">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="9b120-970">**Allowed From**</span></span>

<span data-ttu-id="9b120-971">Applicazione</span><span class="sxs-lookup"><span data-stu-id="9b120-971">Application</span></span>

<span data-ttu-id="9b120-972">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="9b120-972">**Example**</span></span>

```c
static UINT authentication_check_extended(NX_HTTP_SERVER *server_ptr,
                                         UINT request_type, CHAR *resource,
                                         CHAR **name, UINT *name_length,
                                         CHAR **password, 
                                         UINT *password_length,
                                         CHAR **realm, UINT *realm_length)
{

    /* Just use a simple name, password, and realm for all
    requests and resources. */

    *name = "name";
    *password = "password";
    *realm = "NetX Duo HTTP demo";
    *name_length = 4;
    *password_length = 8;
    *realm_length = 18;

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and
before starting HTTP services when nx_http_server_start is called, set 
the authentication checking callback: */

nx_http_server_authentication_check_set (&my_server,
                                        authentication_check_extended);
```