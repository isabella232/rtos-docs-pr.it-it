---
title: Capitolo 3-Descrizione dei servizi HTTP
description: Questo capitolo contiene una descrizione di tutti i servizi HTTP Web NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 30168ad5a564b0f4c0a8c999046c5103385f4f90
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822889"
---
# <a name="chapter-3---description-of-http-services"></a><span data-ttu-id="c8c9b-103">Capitolo 3-Descrizione dei servizi HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-103">Chapter 3 - Description of HTTP services</span></span>

<span data-ttu-id="c8c9b-104">Questo capitolo contiene una descrizione di tutti i servizi HTTP Web NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-104">This chapter contains a description of all NetX Web HTTP services (listed below) in alphabetical order.</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="http-and-https-client-api"></a><span data-ttu-id="c8c9b-106">API client HTTP e HTTPS</span><span class="sxs-lookup"><span data-stu-id="c8c9b-106">HTTP and HTTPS Client API</span></span>

## <a name="nx_web_http_client_connect"></a><span data-ttu-id="c8c9b-107">nx_web_http_client_connect</span><span class="sxs-lookup"><span data-stu-id="c8c9b-107">nx_web_http_client_connect</span></span>

<span data-ttu-id="c8c9b-108">Aprire un socket di testo non crittografato in un server HTTP per le richieste personalizzate</span><span class="sxs-lookup"><span data-stu-id="c8c9b-108">Open a plaintext socket to an HTTP server for custom requests</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-109">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-109">Prototype</span></span>

```C
UINT nx_web_http_client_connect(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip,
    UINT server_port, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-110">Description</span></span>

<span data-ttu-id="c8c9b-111">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-111">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-112">Questo servizio apre un socket TCP non crittografato a un server HTTP, ma non invia alcuna richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-112">This service opens a plaintext TCP socket to an HTTP server but does not send any requests.</span></span> <span data-ttu-id="c8c9b-113">Le richieste vengono create con n *x_web_http_client_request_initialize ()* e inviate utilizzando *nx_web_http_client_request_send ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-113">Requests are created with n *x_web_http_client_request_initialize()* and sent using *nx_web_http_client_request_send()*.</span></span> <span data-ttu-id="c8c9b-114">È possibile aggiungere intestazioni HTTP personalizzate alla richiesta utilizzando *nx_web_http_client_request_header_add ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-114">Custom HTTP headers may be added to the request using *nx_web_http_client_request_header_add()*.</span></span>

<span data-ttu-id="c8c9b-115">L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-115">Use of this service enables an application to add any number of custom headers to the request.</span></span> <span data-ttu-id="c8c9b-116">**Questo consente richieste HTTP personalizzate destinate ad applicazioni specifiche.**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-116">**This allows for customized HTTP requests intended for specific applications.**</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-117">I metodi nx_web_http_client_ \* _start sono forniti per praticità (ad esempio, *nx_web_http_client_get_start*()) e gestiscono la generazione di richieste e la connessione socket.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-117">The nx_web_http_client_\*_start methods are provided for convenience (e.g. *nx_web_http_client_get_start*()) and handle the request generation and socket connection.</span></span> <span data-ttu-id="c8c9b-118">È possibile usare tali servizi invece di *nx_web_http_client_connect ()* e le routine correlate se non sono necessarie intestazioni HTTP personalizzate nelle richieste.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-118">You can use those services instead of *nx_web_http_client_connect()* and the related routines if you do not need custom HTTP headers in your requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-119">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-119">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-120">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-120">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-121">**server_ip** Indirizzo IP del server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-121">**server_ip** IP address of remote HTTP server.</span></span>
- <span data-ttu-id="c8c9b-122">**SERVER_PORT** Porta sul server HTTP remoto, ad esempio 80 per HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-122">**server_port** Port on remote HTTP server (e.g. 80 for HTTP).</span></span>
- <span data-ttu-id="c8c9b-123">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa delle operazioni di rete sottostanti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-123">**wait_option** Defines how long the service will wait for underlying network operations.</span></span> <span data-ttu-id="c8c9b-124">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-124">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-125">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-125">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-126">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-126">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-127">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-127">Return Values</span></span>

- <span data-ttu-id="c8c9b-128">**NX_SUCCESS** (0x00) connessione riuscita del socket TCP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-128">**NX_SUCCESS** (0x00) Successful connection of TCP socket.</span></span>
- <span data-ttu-id="c8c9b-129">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-129">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-130">NX_WEB_HTTP_NOT_READY (0x3000A) è già in corso un'altra richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-130">NX_WEB_HTTP_NOT_READY (0x3000A) Another request is already in progress.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-131">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-131">Allowed From</span></span>

<span data-ttu-id="c8c9b-132">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-132">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-133">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-133">Example</span></span>

```C
NXD_ADDRESS server_ip_addr;

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

nx_web_http_client_connect(&my_client, &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get* until the entire response is retrieved. *./

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);
    /* Process response packets… */
}
```

## <a name="nx_web_http_client_create"></a><span data-ttu-id="c8c9b-134">nx_web_http_client_create</span><span class="sxs-lookup"><span data-stu-id="c8c9b-134">nx_web_http_client_create</span></span>

<span data-ttu-id="c8c9b-135">Creare un'istanza del client HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-135">Create an HTTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-136">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-136">Prototype</span></span>

```C
UINT nx_web_http_client_create(NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr,
    ULONG window_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-137">Description</span></span>

<span data-ttu-id="c8c9b-138">Questo servizio crea un'istanza del client HTTP nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-138">This service creates an HTTP Client instance on the specified IP instance.</span></span> <span data-ttu-id="c8c9b-139">L'istanza del client può essere utilizzata sia per HTTP che per HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-139">The Client instance can be used for either HTTP or HTTPS.</span></span> <span data-ttu-id="c8c9b-140">Per ulteriori informazioni sull'avvio di un'istanza HTTP o HTTPS, vedere i servizi *nx_web_http_client_connect ()* e *nx_web_http_client_secure_connect ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-140">See the services *nx_web_http_client_connect()* and *nx_web_http_client_secure_connect()* for more information on starting an HTTP or HTTPS instance.</span></span> <span data-ttu-id="c8c9b-141">Vedere anche l'API per \* nx_web_http_client_get_ \* \*, \*nx_web_http_client_put_ \* *, *nx_web_http_client_post_** per le chiamate semplici di metodi get, put e post.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-141">Also refer to the API for \*nx_web_http_client_get_\*\*, *nx_web_http_client_put_\*\*, *nx_web_http_client_post_** for simple invocations of GET, PUT, and POST methods.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-142">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-142">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-143">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-143">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-144">**client_name** Nome dell'istanza del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-144">**client_name** Name of HTTP Client instance.</span></span>
- <span data-ttu-id="c8c9b-145">**ip_ptr** Puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-145">**ip_ptr** Pointer to IP instance.</span></span>
- <span data-ttu-id="c8c9b-146">**pool_ptr** Puntatore al pool di pacchetti predefinito.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-146">**pool_ptr** Pointer to default packet pool.</span></span> <span data-ttu-id="c8c9b-147">Si noti che i pacchetti in questo pool devono avere un payload sufficientemente grande per gestire l'intestazione della risposta completa.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-147">Note that the packets in this pool must have a payload large enough to handle the complete response header.</span></span> <span data-ttu-id="c8c9b-148">Questa impostazione è definita da *NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE* in *nx_web_http_client. h*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-148">This is defined by *NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE* in *nx_web_http_client.h*.</span></span>
- <span data-ttu-id="c8c9b-149">**window_size** Dimensioni della finestra di ricezione del socket TCP del client.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-149">**window_size** Size of the Client’s TCP socket receive window.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-150">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-150">Return Values</span></span>

- <span data-ttu-id="c8c9b-151">Creazione client HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-151">**NX_SUCCESS** (0x00) Successful HTTP Client create</span></span>
- <span data-ttu-id="c8c9b-152">NX_PTR_ERROR (0x16) puntatore HTTP, ip_ptr o pool di pacchetti non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-152">NX_PTR_ERROR (0x16) Invalid HTTP, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="c8c9b-153">Dimensioni del payload NX_WEB_HTTP_POOL_ERROR (0x30009) non valide nel pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-153">NX_WEB_HTTP_POOL_ERROR (0x30009) Invalid payload size in packet pool</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-154">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-154">Allowed From</span></span>

<span data-ttu-id="c8c9b-155">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-155">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-156">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-156">Example</span></span>

```C
/* Create the HTTP Client instance "my_client" on "ip_0". */
status = nx_web_http_client_create(&my_client, "my client", &ip_0, &pool_0, 8192);

/* If status is NX_SUCCESS an HTTP Client instance was successfully
    created. */
```

## <a name="nx_web_http_client_delete"></a><span data-ttu-id="c8c9b-157">nx_web_http_client_delete</span><span class="sxs-lookup"><span data-stu-id="c8c9b-157">nx_web_http_client_delete</span></span>

<span data-ttu-id="c8c9b-158">Eliminare un'istanza client HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-158">Delete an HTTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-159">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-159">Prototype</span></span>

```C
UINT nx_web_http_client_delete(NX_WEB_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="c8c9b-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-160">Description</span></span>

<span data-ttu-id="c8c9b-161">Questo servizio Elimina un'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-161">This service deletes a previously created HTTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-162">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-162">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-163">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-163">**client_ptr** Pointer to HTTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-164">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-164">Return Values</span></span>

- <span data-ttu-id="c8c9b-165">Eliminazione client HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-165">**NX_SUCCESS** (0x00) Successful HTTP Client delete</span></span>
- <span data-ttu-id="c8c9b-166">NX_PTR_ERROR (0x16) puntatore HTTP non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-166">NX_PTR_ERROR (0x16) Invalid HTTP pointer</span></span>
- <span data-ttu-id="c8c9b-167">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-167">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-168">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-168">Allowed From</span></span>

<span data-ttu-id="c8c9b-169">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-169">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-170">Example</span></span>

```C
/* Delete the HTTP Client instance "my_client." */
status = nx_web_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully
    deleted. */
```

## <a name="nx_web_http_client_delete_start"></a><span data-ttu-id="c8c9b-171">nx_web_http_client_delete_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-171">nx_web_http_client_delete_start</span></span>

<span data-ttu-id="c8c9b-172">Avvia una richiesta di eliminazione HTTP non crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-172">Start a plaintext HTTP DELETE request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-173">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-173">Prototype</span></span>

```C
UINT nx_web_http_client_delete_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-174">Description</span></span>

<span data-ttu-id="c8c9b-175">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-175">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-176">Questo servizio tenta di inviare una richiesta DELETE per la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-176">This service attempts to send a DELETE request for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-177">Se questa routine restituisce NX_SUCCESS, l'applicazione può chiamare *nx_web_http_client_response_body_get ()* per recuperare la risposta del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-177">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response.</span></span>

<span data-ttu-id="c8c9b-178">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-178">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-179">Questa API è deprecata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-179">This API is deprecated.</span></span> <span data-ttu-id="c8c9b-180">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_delete_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-180">Developers are encouraged to use *nx_web_http_client_delete_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-181">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-181">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-182">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-182">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-183">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-183">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-184">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-184">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-185">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-185">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-186">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-186">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-187">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-187">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-188">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-188">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-189">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-189">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-190">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-190">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-191">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-191">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-192">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-192">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-193">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-193">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-194">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-194">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-195">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-195">Return Values</span></span>

- <span data-ttu-id="c8c9b-196">**NX_SUCCESS** (0x00) ha inviato un messaggio di richiesta di eliminazione client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-196">**NX_SUCCESS** (0x00) Successfully sent HTTP Client DELETE request message</span></span>
- <span data-ttu-id="c8c9b-197">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-197">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-198">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-198">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-199">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-199">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-200">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-200">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-201">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-201">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-202">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-202">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-203">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-203">Allowed From</span></span>

<span data-ttu-id="c8c9b-204">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-204">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-205">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-205">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_start(&my_client, &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_delete_start_extended"></a><span data-ttu-id="c8c9b-206">nx_web_http_client_delete_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-206">nx_web_http_client_delete_start_extended</span></span>

<span data-ttu-id="c8c9b-207">Avvia una richiesta di eliminazione HTTP non crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-207">Start a plaintext HTTP DELETE request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-208">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-208">Prototype</span></span>

```C
UINT nx_web_http_client_delete_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-209">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-209">Description</span></span>

<span data-ttu-id="c8c9b-210">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-210">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-211">Questo servizio tenta di inviare una richiesta DELETE per la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-211">This service attempts to send a DELETE request for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-212">Se questa routine restituisce NX_SUCCESS, l'applicazione può chiamare *nx_web_http_client_response_body_get ()* per recuperare la risposta del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-212">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response.</span></span>

<span data-ttu-id="c8c9b-213">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-213">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-214">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-214">The strings of resource, host, username and password must be NULL-terminated, and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-215">Questo servizio sostituisce *nx_web_http_client_delete_start* ().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-215">This service replaces *nx_web_http_client_delete_start* ().</span></span> <span data-ttu-id="c8c9b-216">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-216">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-217">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-217">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-218">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-218">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-219">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-219">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-220">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-220">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-221">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-221">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-222">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-222">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-223">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-223">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-224">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-224">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-225">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-225">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-226">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-226">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-227">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-227">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-228">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-228">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-229">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-229">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-230">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-230">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-231">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-231">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-232">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-232">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-233">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-233">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-234">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-234">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-235">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-235">Return Values</span></span>

- <span data-ttu-id="c8c9b-236">**NX_SUCCESS** (0x00) ha inviato un messaggio di richiesta di eliminazione client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-236">**NX_SUCCESS** (0x00) Successfully sent HTTP Client DELETE request message</span></span>
- <span data-ttu-id="c8c9b-237">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-237">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-238">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-238">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-239">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-239">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-240">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-240">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-241">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-241">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-242">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-242">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-243">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-243">Allowed From</span></span>

<span data-ttu-id="c8c9b-244">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-244">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-245">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-245">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_start_extended(&my_client,
    &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_delete_secure_start"></a><span data-ttu-id="c8c9b-246">nx_web_http_client_delete_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-246">nx_web_http_client_delete_secure_start</span></span>

<span data-ttu-id="c8c9b-247">Avviare una richiesta di eliminazione HTTPS crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-247">Start an encrypted HTTPS DELETE request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-248">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-248">Prototype</span></span>

```C
UINT nx_web_http_client_delete_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-249">Description</span></span>

<span data-ttu-id="c8c9b-250">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-250">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-251">Questo servizio tenta di inviare una richiesta DELETE per la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-251">This service attempts to send a DELETE request for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-252">Se questa routine restituisce NX_SUCCESS, l'applicazione può chiamare *nx_web_http_client_response_body_get ()* per recuperare la risposta del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-252">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response.</span></span>

<span data-ttu-id="c8c9b-253">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-253">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-254">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-254">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-255">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_delete_secure_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-255">Developers are encouraged to use *nx_web_http_client_delete_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-256">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-256">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-257">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-257">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-258">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-258">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-259">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-259">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-260">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-260">**resource** Pointer to URL string for requested resource.</span></span> <span data-ttu-id="c8c9b-261">la risorsa deve essere con terminazione NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-261">resource must be NULL-terminated.</span></span>
- <span data-ttu-id="c8c9b-262">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-262">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-263">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-263">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-264">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-264">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-265">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-265">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-266">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-266">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-267">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-267">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-268">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-268">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-269">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-269">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-270">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-270">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-271">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-271">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-272">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-272">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-273">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-273">Return Values</span></span>

- <span data-ttu-id="c8c9b-274">**NX_SUCCESS** (0x00) ha inviato un messaggio di richiesta di eliminazione client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-274">**NX_SUCCESS** (0x00) Successfully sent HTTP Client DELETE request message</span></span>
- <span data-ttu-id="c8c9b-275">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-275">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-276">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-276">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-277">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-277">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-278">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-278">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-279">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-279">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-280">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-280">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-281">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-281">Allowed From</span></span>

<span data-ttu-id="c8c9b-282">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-282">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-283">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-283">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_delete_secure_start_extended"></a><span data-ttu-id="c8c9b-284">nx_web_http_client_delete_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-284">nx_web_http_client_delete_secure_start_extended</span></span>

<span data-ttu-id="c8c9b-285">Avviare una richiesta di eliminazione HTTPS crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-285">Start an encrypted HTTPS DELETE request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-286">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-286">Prototype</span></span>

```C
UINT nx_web_http_client_delete_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-287">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-287">Description</span></span>

<span data-ttu-id="c8c9b-288">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-288">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-289">Questo servizio tenta di inviare una richiesta DELETE per la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-289">This service attempts to send a DELETE request for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-290">Se questa routine restituisce NX_SUCCESS, l'applicazione può chiamare *nx_web_http_client_response_body_get ()* per recuperare la risposta del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-290">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response.</span></span>

<span data-ttu-id="c8c9b-291">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-291">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-292">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-292">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-293">Questo servizio sostituisce *nx_web_http_client_delete_secure_start*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-293">This service replaces *nx_web_http_client_delete_secure_start*().</span></span> <span data-ttu-id="c8c9b-294">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-294">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-295">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-295">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-296">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-296">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-297">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-297">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-298">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-298">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-299">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-299">**resource** Pointer to URL string for requested resource.</span></span> <span data-ttu-id="c8c9b-300">la risorsa deve essere con terminazione NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-300">resource must be NULL-terminated.</span></span>
- <span data-ttu-id="c8c9b-301">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-301">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-302">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-302">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-303">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-303">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-304">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-304">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-305">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-305">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-306">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-306">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-307">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-307">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-308">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-308">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-309">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-309">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-310">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-310">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-311">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-311">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-312">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-312">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-313">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-313">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-314">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-314">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-315">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-315">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-316">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-316">Return Values</span></span>

- <span data-ttu-id="c8c9b-317">**NX_SUCCESS** (0x00) ha inviato un messaggio di richiesta di eliminazione client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-317">**NX_SUCCESS** (0x00) Successfully sent HTTP Client DELETE request message</span></span>
- <span data-ttu-id="c8c9b-318">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-318">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-319">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-319">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-320">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-320">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-321">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-321">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-322">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-322">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-323">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-323">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="c8c9b-324">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-324">Allowed From</span></span>

<span data-ttu-id="c8c9b-325">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-325">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-326">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-326">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_secure_start_extended(&my_client,
    &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_get_start"></a><span data-ttu-id="c8c9b-327">nx_web_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-327">nx_web_http_client_get_start</span></span>

<span data-ttu-id="c8c9b-328">Avvia una richiesta HTTP GET non crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-328">Start a plaintext HTTP GET request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-329">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-329">Prototype</span></span>

```C
UINT nx_web_http_client_get_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-330">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-330">Description</span></span>

<span data-ttu-id="c8c9b-331">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-331">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-332">Questo servizio tenta di ottenere la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-332">This service attempts to GET the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-333">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_web_http_client_response_body_get ()* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-333">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_web_http_client_response_body_get()* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8c9b-334">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-334">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-335">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-335">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-336">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_get_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-336">Developers are encouraged to use *nx_web_http_client_get_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-337">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-337">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-338">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-338">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-339">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-339">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-340">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-340">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-341">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-341">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-342">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-342">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-343">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-343">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-344">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-344">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-345">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-345">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-346">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-346">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-347">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-347">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-348">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-348">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-349">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-349">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-350">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-350">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-351">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-351">Return Values</span></span>

- <span data-ttu-id="c8c9b-352">**NX_SUCCESS** (0x00) ha inviato il messaggio di avvio Get client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-352">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="c8c9b-353">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-353">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-354">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-354">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-355">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-355">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-356">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-356">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-357">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-357">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-358">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-358">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-359">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-359">Allowed From</span></span>

<span data-ttu-id="c8c9b-360">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-360">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-361">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-361">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    multiple times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_start_extended"></a><span data-ttu-id="c8c9b-362">nx_web_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-362">nx_web_http_client_get_start_extended</span></span>

<span data-ttu-id="c8c9b-363">Avvia una richiesta HTTP GET non crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-363">Start a plaintext HTTP GET request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-364">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-364">Prototype</span></span>

```C
UINT nx_web_http_client_get_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-365">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-365">Description</span></span>

<span data-ttu-id="c8c9b-366">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-366">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-367">Questo servizio tenta di ottenere la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-367">This service attempts to GET the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-368">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_web_http_client_response_body_get ()* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-368">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_web_http_client_response_body_get()* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8c9b-369">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-369">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-370">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-370">The strings of resource, host, username and password must be NULL-terminated, and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-371">Questo servizio sostituisce *nx_web_http_client_get_start*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-371">This service replaces *nx_web_http_client_get_start*().</span></span> <span data-ttu-id="c8c9b-372">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-372">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-373">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-373">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-374">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-374">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-375">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-375">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-376">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-376">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-377">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-377">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-378">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-378">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-379">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-379">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-380">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-380">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-381">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-381">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-382">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-382">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-383">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-383">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-384">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-384">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-385">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-385">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-386">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-386">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-387">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-387">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-388">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-388">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-389">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-389">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-390">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-390">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-391">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-391">Return Values</span></span>

- <span data-ttu-id="c8c9b-392">**NX_SUCCESS** (0x00) ha inviato il messaggio di avvio Get client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-392">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="c8c9b-393">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-393">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-394">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-394">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-395">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-395">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-396">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-396">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-397">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-397">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-398">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-398">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-399">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-399">Allowed From</span></span>

<span data-ttu-id="c8c9b-400">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-400">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-401">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-401">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_start_extended(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    multiple times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_secure_start"></a><span data-ttu-id="c8c9b-402">nx_web_http_client_get_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-402">nx_web_http_client_get_secure_start</span></span>

<span data-ttu-id="c8c9b-403">Avviare una richiesta HTTPS GET crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-403">Start an encrypted HTTPS GET request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-404">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-404">Prototype</span></span>

```C
UINT nx_web_http_client_get_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
        NX_SECURE_TLS_SESSION *tls_session),
        ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-405">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-405">Description</span></span>

<span data-ttu-id="c8c9b-406">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-406">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-407">Questo servizio tenta di ottenere la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-407">This service attempts to GET the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-408">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_web_http_client_response_body_get ()* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-408">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_web_http_client_response_body_get()* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8c9b-409">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-409">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-410">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-410">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-411">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_get_secure_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-411">Developers are encouraged to use *nx_web_http_client_get_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-412">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-412">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-413">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-413">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-414">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-414">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-415">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-415">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-416">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-416">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-417">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-417">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-418">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-418">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-419">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-419">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-420">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-420">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-421">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-421">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-422">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-422">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-423">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-423">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-424">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-424">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-425">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-425">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-426">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-426">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-427">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-427">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-428">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-428">Return Values</span></span>

- <span data-ttu-id="c8c9b-429">**NX_SUCCESS** (0x00) ha inviato il messaggio di avvio Get client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-429">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="c8c9b-430">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-430">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-431">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-431">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-432">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-432">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-433">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-433">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-434">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-434">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-435">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-435">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-436">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-436">Allowed From</span></span>

<span data-ttu-id="c8c9b-437">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-437">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-438">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-438">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started
    and is so far successful. The client must now call
    *nx_web_http_client_response_body_get()* multiple times to
    retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_secure_start_extended"></a><span data-ttu-id="c8c9b-439">nx_web_http_client_get_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-439">nx_web_http_client_get_secure_start_extended</span></span>

<span data-ttu-id="c8c9b-440">Avviare una richiesta HTTPS GET crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-440">Start an encrypted HTTPS GET request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-441">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-441">Prototype</span></span>

```C
UINT nx_web_http_client_get_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-442">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-442">Description</span></span>

<span data-ttu-id="c8c9b-443">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-443">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-444">Questo servizio tenta di ottenere la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-444">This service attempts to GET the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-445">Se questa routine restituisce NX_SUCCESS, l'applicazione può effettuare più chiamate a *nx_web_http_client_response_body_get ()* per recuperare i pacchetti di dati corrispondenti al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-445">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_web_http_client_response_body_get()* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8c9b-446">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-446">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-447">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-447">The strings of resource, host, username and password must be NULL-terminated, and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-448">Questo servizio sostituisce *nx_web_http_client_secure_start*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-448">This service replaces *nx_web_http_client_secure_start*().</span></span> <span data-ttu-id="c8c9b-449">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-449">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-450">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-450">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-451">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-451">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-452">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-452">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-453">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-453">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-454">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-454">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-455">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-455">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-456">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-456">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-457">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-457">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-458">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-458">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-459">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-459">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-460">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-460">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-461">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-461">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-462">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-462">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-463">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-463">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-464">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-464">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-465">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-465">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-466">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-466">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-467">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-467">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-468">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-468">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-469">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-469">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-470">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-470">Return Values</span></span>

- <span data-ttu-id="c8c9b-471">**NX_SUCCESS** (0x00) ha inviato il messaggio di avvio Get client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-471">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="c8c9b-472">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-472">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-473">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-473">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-474">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-474">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-475">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-475">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-476">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-476">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-477">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-477">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-478">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-478">Allowed From</span></span>

<span data-ttu-id="c8c9b-479">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-479">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-480">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-480">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM
    is started and is so far successful. The client must now call
    *nx_web_http_client_response_body_get()* multiple times to retrieve
    the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_head_start"></a><span data-ttu-id="c8c9b-481">nx_web_http_client_head_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-481">nx_web_http_client_head_start</span></span>

<span data-ttu-id="c8c9b-482">Avvia una richiesta HEAD HTTP non crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-482">Start a plaintext HTTP HEAD request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-483">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-483">Prototype</span></span>

```C
UINT nx_web_http_client_head_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-484">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-484">Description</span></span>

<span data-ttu-id="c8c9b-485">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-485">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-486">Questo servizio tenta di recuperare i metadati HEAD per la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-486">This service attempts to retrieve the HEAD metadata for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-487">Se questa routine restituisce NX_SUCCESS, l'applicazione può chiamare *nx_web_http_client_response_body_get ()* per recuperare la risposta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-487">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the response.</span></span>

<span data-ttu-id="c8c9b-488">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-488">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-489">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-489">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-490">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_head_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-490">Developers are encouraged to use *nx_web_http_client_head_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-491">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-491">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-492">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-492">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-493">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-493">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-494">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-494">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-495">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-495">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-496">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-496">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-497">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-497">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-498">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-498">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-499">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-499">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-500">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-500">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-501">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-501">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-502">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-502">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-503">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-503">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-504">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-504">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-505">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-505">Return Values</span></span>

- <span data-ttu-id="c8c9b-506">**NX_SUCCESS** (0x00) ha inviato un messaggio di richiesta Head client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-506">**NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message</span></span>
- <span data-ttu-id="c8c9b-507">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-507">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-508">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-508">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-509">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-509">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-510">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-510">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-511">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-511">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-512">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-512">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-513">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-513">Allowed From</span></span>

<span data-ttu-id="c8c9b-514">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-514">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-515">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-515">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_head_start_extended"></a><span data-ttu-id="c8c9b-516">nx_web_http_client_head_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-516">nx_web_http_client_head_start_extended</span></span>

<span data-ttu-id="c8c9b-517">Avvia una richiesta HEAD HTTP non crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-517">Start a plaintext HTTP HEAD request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-518">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-518">Prototype</span></span>

```C
UINT nx_web_http_client_head_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-519">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-519">Description</span></span>

<span data-ttu-id="c8c9b-520">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-520">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-521">Questo servizio tenta di recuperare i metadati HEAD per la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-521">This service attempts to retrieve the HEAD metadata for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-522">Se questa routine restituisce NX_SUCCESS, l'applicazione può chiamare *nx_web_http_client_response_body_get ()* per recuperare la risposta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-522">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the response.</span></span>

<span data-ttu-id="c8c9b-523">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-523">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-524">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-524">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-525">Questo servizio sostituisce *nx_web_http_client_head_start*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-525">This service replaces *nx_web_http_client_head_start*().</span></span> <span data-ttu-id="c8c9b-526">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-526">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-527">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-527">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-528">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-528">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-529">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-529">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-530">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-530">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-531">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-531">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-532">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-532">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-533">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-533">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-534">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-534">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-535">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-535">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-536">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-536">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-537">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-537">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-538">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-538">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-539">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-539">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-540">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-540">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-541">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-541">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-542">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-542">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-543">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-543">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-544">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-544">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-545">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-545">Return Values</span></span>

- <span data-ttu-id="c8c9b-546">**NX_SUCCESS** (0x00) ha inviato un messaggio di richiesta Head client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-546">**NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message</span></span>
- <span data-ttu-id="c8c9b-547">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-547">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-548">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-548">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-549">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-549">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-550">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-550">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-551">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-551">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-552">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-552">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-553">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-553">Allowed From</span></span>

<span data-ttu-id="c8c9b-554">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-554">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-555">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-555">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_head_secure_start"></a><span data-ttu-id="c8c9b-556">nx_web_http_client_head_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-556">nx_web_http_client_head_secure_start</span></span>

<span data-ttu-id="c8c9b-557">Avviare una richiesta HEAD HTTPS crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-557">Start an encrypted HTTPS HEAD request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-558">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-558">Prototype</span></span>

```C
UINT nx_web_http_client_head_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-559">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-559">Description</span></span>

<span data-ttu-id="c8c9b-560">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-560">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-561">Questo servizio tenta di recuperare i metadati HEAD per la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-561">This service attempts to retrieve the HEAD metadata for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-562">Se questa routine restituisce NX_SUCCESS, l'applicazione può chiamare *nx_web_http_client_response_body_get ()* per recuperare la risposta del server corrispondente al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-562">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8c9b-563">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-563">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-564">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-564">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-565">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_head_secure_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-565">Developers are encouraged to use *nx_web_http_client_head_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-566">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-566">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-567">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-567">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-568">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-568">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-569">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-569">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-570">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-570">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-571">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-571">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-572">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-572">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-573">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-573">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-574">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-574">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-575">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-575">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-576">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-576">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-577">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-577">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-578">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-578">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-579">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-579">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-580">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-580">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-581">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-581">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-582">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-582">Return Values</span></span>

- <span data-ttu-id="c8c9b-583">**NX_SUCCESS** (0x00) ha inviato un messaggio di richiesta Head client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-583">**NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message</span></span>
- <span data-ttu-id="c8c9b-584">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-584">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-585">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-585">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-586">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-586">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-587">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-587">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-588">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-588">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-589">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-589">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-590">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-590">Allowed From</span></span>

<span data-ttu-id="c8c9b-591">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-591">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-592">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-592">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_head_secure_start_extended"></a><span data-ttu-id="c8c9b-593">nx_web_http_client_head_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-593">nx_web_http_client_head_secure_start_extended</span></span>

<span data-ttu-id="c8c9b-594">Avviare una richiesta HEAD HTTPS crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-594">Start an encrypted HTTPS HEAD request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-595">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-595">Prototype</span></span>

```C
UINT nx_web_http_client_head_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-596">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-596">Description</span></span>

<span data-ttu-id="c8c9b-597">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-597">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-598">Questo servizio tenta di recuperare i metadati HEAD per la risorsa specificata dal puntatore "Resource" nell'istanza del client HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-598">This service attempts to retrieve the HEAD metadata for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-599">Se questa routine restituisce NX_SUCCESS, l'applicazione può chiamare *nx_web_http_client_response_body_get ()* per recuperare la risposta del server corrispondente al contenuto della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-599">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8c9b-600">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio di richieste Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-600">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8c9b-601">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-601">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-602">Questo servizio sostituisce *nx_web_http_client_head_secure_start*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-602">This service replaces *nx_web_http_client_head_secure_start*().</span></span> <span data-ttu-id="c8c9b-603">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-603">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-604">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-604">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-605">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-605">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-606">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-606">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-607">**SERVER_PORT** Porta sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-607">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-608">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-608">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-609">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-609">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-610">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-610">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-611">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-611">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-612">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-612">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-613">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-613">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-614">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-614">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-615">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-615">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-616">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-616">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-617">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-617">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-618">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-618">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-619">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-619">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-620">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-620">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-621">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-621">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-622">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-622">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-623">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-623">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-624">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-624">Return Values</span></span>

- <span data-ttu-id="c8c9b-625">**NX_SUCCESS** (0x00) ha inviato un messaggio di richiesta Head client http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-625">**NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message</span></span>
- <span data-ttu-id="c8c9b-626">Errore del client HTTP interno **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-626">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8c9b-627">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-627">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-628">**NX_WEB_HTTP_FAILED** (0x30002) errore client HTTP che comunica con il server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-628">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-629">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-629">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8c9b-630">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-630">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-631">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-631">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-632">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-632">Allowed From</span></span>

<span data-ttu-id="c8c9b-633">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-633">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-634">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-634">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_request_packet_allocate"></a><span data-ttu-id="c8c9b-635">nx_web_http_client_request_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c8c9b-635">nx_web_http_client_request_packet_allocate</span></span>

<span data-ttu-id="c8c9b-636">Allocare un pacchetto HTTP (S)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-636">Allocate a HTTP(S) packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-637">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-637">Prototype</span></span>

```C
UINT nx_web_http_client_request_packet_allocate(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-638">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-638">Description</span></span>

<span data-ttu-id="c8c9b-639">Questo servizio tenta di allocare un pacchetto per HTTP (S) client.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-639">This service attempts to allocates a packet for Client HTTP(S).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-640">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-640">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-641">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-641">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-642">**packet_ptr** Puntatore al pacchetto allocato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-642">**packet_ptr** Pointer to allocated packet.</span></span>
- <span data-ttu-id="c8c9b-643">**WAIT_OPTION** Definisce il tempo di attesa in cicli se non sono disponibili pacchetti nel pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-643">**wait_option** Defines the wait time in ticks if there are no packets available in the packet pool.</span></span> <span data-ttu-id="c8c9b-644">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-644">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-645">**NX_NO_WAIT** (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-645">**NX_NO_WAIT** (0x00000000)</span></span>
  - <span data-ttu-id="c8c9b-646">**NX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-646">**NX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>
  - <span data-ttu-id="c8c9b-647">**timeout nei cicli (da 0x00000001 a** 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-647">**timeout in ticks** (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-648">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-648">Return Values</span></span>

- <span data-ttu-id="c8c9b-649">Allocazione pacchetto riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-649">**NX_SUCCESS** (0x00) Successful packet allocate</span></span>
- <span data-ttu-id="c8c9b-650">**NX_NO_PACKET** (0x01) non sono disponibili pacchetti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-650">**NX_NO_PACKET** (0x01) No packet available</span></span>
- <span data-ttu-id="c8c9b-651">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al *tx_thread_wait_abort*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-651">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="c8c9b-652">Le dimensioni del pacchetto **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non supportano il protocollo.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-652">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="c8c9b-653">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-653">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-654">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-654">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-655">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-655">Allowed From</span></span>

<span data-ttu-id="c8c9b-656">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-656">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-657">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-657">Example</span></span>

```C
/* Allocate a packet for HTTP(S) Client and suspend for a maximum of 5 timer
    ticks if the pool is empty. */
status = nx_web_http_client_request_packet_allocate(&my_client, &packet_ptr, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
    variable packet_ptr. */
```

## <a name="nx_web_http_client_post_start"></a><span data-ttu-id="c8c9b-658">nx_web_http_client_post_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-658">nx_web_http_client_post_start</span></span>

<span data-ttu-id="c8c9b-659">Avviare una richiesta HTTP POST</span><span class="sxs-lookup"><span data-stu-id="c8c9b-659">Start an HTTP POST request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-660">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-660">Prototype</span></span>

```C
UINT nx_web_http_client_post_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host,
    CHAR *username, CHAR *password,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-661">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-661">Description</span></span>

<span data-ttu-id="c8c9b-662">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-662">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-663">Questo servizio tenta di inviare una richiesta POST con la risorsa specificata al server HTTP nell'indirizzo IP e nella porta specificati.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-663">This service attempts to send a POST request with the specified resource to the HTTP Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8c9b-664">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet* per inviare il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-664">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-665">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-665">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8c9b-666">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-666">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-667">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_post_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-667">Developers are encouraged to use *nx_web_http_client_post_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-668">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-668">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-669">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-669">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-670">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-670">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-671">**SERVER_PORT** Porta TCP sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-671">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-672">**risorsa** di Puntatore alla stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-672">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="c8c9b-673">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-673">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-674">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-674">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-675">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-675">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-676">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-676">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-677">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-677">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-678">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-678">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8c9b-679">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_web_http_client_put_packet ()* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-679">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8c9b-680">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-680">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-681">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-681">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-682">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-682">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-683">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-683">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-684">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-684">Return Values</span></span>

- <span data-ttu-id="c8c9b-685">**NX_SUCCESS** (0x00) ha inviato correttamente la richiesta post</span><span class="sxs-lookup"><span data-stu-id="c8c9b-685">**NX_SUCCESS** (0x00) Successfully sent POST request</span></span>
- <span data-ttu-id="c8c9b-686">Nome utente di **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="c8c9b-686">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8c9b-687">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-687">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-688">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-688">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-689">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-689">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8c9b-690">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-690">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-691">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-691">Allowed From</span></span>

<span data-ttu-id="c8c9b-692">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-692">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-693">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-693">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start an HTTP POST to post the 20-byte resource "/TEST.HTM" to the HTTP Server
    at IP address 1.2.3.5. */
status = nx_web_http_client_post_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_start_extended"></a><span data-ttu-id="c8c9b-694">nx_web_http_client_post_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-694">nx_web_http_client_post_start_extended</span></span>

<span data-ttu-id="c8c9b-695">Avviare una richiesta HTTP POST</span><span class="sxs-lookup"><span data-stu-id="c8c9b-695">Start an HTTP POST request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-696">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-696">Prototype</span></span>

```C
UINT nx_web_http_client_post_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-697">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-697">Description</span></span>

<span data-ttu-id="c8c9b-698">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-698">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-699">Questo servizio tenta di inviare una richiesta POST con la risorsa specificata al server HTTP nell'indirizzo IP e nella porta specificati.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-699">This service attempts to send a POST request with the specified resource to the HTTP Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8c9b-700">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet* per inviare il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-700">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-701">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-701">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8c9b-702">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-702">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-703">Questo servizio sostituisce *nx_web_http_client_post_start* ().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-703">This service replaces *nx_web_http_client_post_start* ().</span></span> <span data-ttu-id="c8c9b-704">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-704">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-705">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-705">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-706">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-706">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-707">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-707">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-708">**SERVER_PORT** Porta TCP sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-708">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-709">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-709">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-710">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-710">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-711">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-711">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-712">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-712">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-713">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-713">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-714">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-714">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-715">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-715">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-716">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-716">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-717">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-717">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-718">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-718">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-719">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-719">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8c9b-720">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_web_http_client_put_packet ()* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-720">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8c9b-721">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-721">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-722">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-722">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-723">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-723">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-724">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-724">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-725">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-725">Return Values</span></span>

- <span data-ttu-id="c8c9b-726">**NX_SUCCESS** (0x00) ha inviato correttamente la richiesta post</span><span class="sxs-lookup"><span data-stu-id="c8c9b-726">**NX_SUCCESS** (0x00) Successfully sent POST request</span></span>
- <span data-ttu-id="c8c9b-727">Nome utente di **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="c8c9b-727">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8c9b-728">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-728">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-729">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-729">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-730">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-730">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8c9b-731">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-731">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-732">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-732">Allowed From</span></span>

<span data-ttu-id="c8c9b-733">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-733">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-734">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-734">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start an HTTP POST to post the 20-byte resource "/TEST.HTM" to the HTTP Server
    at IP address 1.2.3.5. */
status = nx_web_http_client_post_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_secure_start"></a><span data-ttu-id="c8c9b-735">nx_web_http_client_post_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-735">nx_web_http_client_post_secure_start</span></span>

<span data-ttu-id="c8c9b-736">Avvia una richiesta POST HTTPS crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-736">Start an encrypted HTTPS POST request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-737">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-737">Prototype</span></span>

```C
UINT nx_web_http_client_post_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-738">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-738">Description</span></span>

<span data-ttu-id="c8c9b-739">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-739">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-740">Questo servizio tenta di inviare una richiesta POST con la risorsa specificata al server HTTPS nell'indirizzo IP e nella porta specificati.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-740">This service attempts to send a POST request with the specified resource to the HTTPS Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8c9b-741">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet ()* per inviare il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-741">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-742">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-742">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8c9b-743">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-743">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-744">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_post_secure_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-744">Developers are encouraged to use *nx_web_http_client_post_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-745">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-745">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-746">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-746">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-747">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-747">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-748">**SERVER_PORT** Porta TCP sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-748">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-749">**risorsa** di Puntatore alla stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-749">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="c8c9b-750">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-750">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-751">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-751">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-752">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-752">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-753">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-753">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-754">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-754">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-755">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-755">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8c9b-756">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_web_http_client_put_packet ()* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-756">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8c9b-757">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-757">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-758">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-758">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-759">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-759">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-760">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-760">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-761">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-761">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-762">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-762">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-763">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-763">Return Values</span></span>

- <span data-ttu-id="c8c9b-764">**NX_SUCCESS** (0x00) ha inviato correttamente la richiesta post</span><span class="sxs-lookup"><span data-stu-id="c8c9b-764">**NX_SUCCESS** (0x00) Successfully sent POST request</span></span>
- <span data-ttu-id="c8c9b-765">Nome utente di **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="c8c9b-765">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8c9b-766">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-766">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-767">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-767">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-768">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-768">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8c9b-769">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-769">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-770">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-770">Allowed From</span></span>

<span data-ttu-id="c8c9b-771">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-771">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-772">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-772">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_secure_start_extended"></a><span data-ttu-id="c8c9b-773">nx_web_http_client_post_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-773">nx_web_http_client_post_secure_start_extended</span></span>

<span data-ttu-id="c8c9b-774">Avvia una richiesta POST HTTPS crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-774">Start an encrypted HTTPS POST request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-775">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-775">Prototype</span></span>

```C
UINT nx_web_http_client_post_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-776">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-776">Description</span></span>

<span data-ttu-id="c8c9b-777">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-777">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-778">Questo servizio tenta di inviare una richiesta POST con la risorsa specificata al server HTTPS nell'indirizzo IP e nella porta specificati.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-778">This service attempts to send a POST request with the specified resource to the HTTPS Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8c9b-779">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet ()* per inviare il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-779">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-780">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-780">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8c9b-781">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-781">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-782">Questo servizio sostituisce *nx_web_http_client_post_secure_start* ().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-782">This service replaces *nx_web_http_client_post_secure_start* ().</span></span> <span data-ttu-id="c8c9b-783">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-783">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-784">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-784">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-785">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-785">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-786">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-786">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-787">**SERVER_PORT** Porta TCP sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-787">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-788">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-788">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-789">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-789">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-790">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-790">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-791">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-791">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-792">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-792">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-793">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-793">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-794">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-794">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-795">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-795">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-796">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-796">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-797">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-797">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-798">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-798">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8c9b-799">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_web_http_client_put_packet ()* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-799">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8c9b-800">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-800">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-801">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-801">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-802">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-802">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-803">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-803">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-804">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-804">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-805">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-805">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-806">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-806">Return Values</span></span>

- <span data-ttu-id="c8c9b-807">**NX_SUCCESS** (0x00) ha inviato correttamente la richiesta post</span><span class="sxs-lookup"><span data-stu-id="c8c9b-807">**NX_SUCCESS** (0x00) Successfully sent POST request</span></span>
- <span data-ttu-id="c8c9b-808">Nome utente di **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="c8c9b-808">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8c9b-809">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-809">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-810">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-810">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-811">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-811">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8c9b-812">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-812">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-813">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-813">Allowed From</span></span>

<span data-ttu-id="c8c9b-814">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-814">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-815">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-815">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_start"></a><span data-ttu-id="c8c9b-816">nx_web_http_client_put_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-816">nx_web_http_client_put_start</span></span>

<span data-ttu-id="c8c9b-817">Avvia una richiesta HTTP PUT</span><span class="sxs-lookup"><span data-stu-id="c8c9b-817">Start an HTTP PUT request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-818">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-818">Prototype</span></span>

```C
UINT nx_web_http_client_put_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-819">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-819">Description</span></span>

<span data-ttu-id="c8c9b-820">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-820">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-821">Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP in corrispondenza dell'indirizzo IP e della porta forniti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-821">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8c9b-822">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet ()* per inviare il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-822">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-823">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-823">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8c9b-824">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-824">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-825">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_put_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-825">Developers are encouraged to use *nx_web_http_client_put_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-826">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-826">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-827">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-827">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-828">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-828">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-829">**SERVER_PORT** Porta TCP sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-829">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-830">**risorsa** di Puntatore alla stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-830">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="c8c9b-831">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-831">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-832">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-832">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-833">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-833">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-834">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-834">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-835">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-835">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-836">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-836">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8c9b-837">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_web_http_client_put_packet ()* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-837">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8c9b-838">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-838">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-839">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-839">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-840">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-840">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-841">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-841">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-842">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-842">Return Values</span></span>

- <span data-ttu-id="c8c9b-843">**NX_SUCCESS** (0x00) ha inviato una richiesta PUT</span><span class="sxs-lookup"><span data-stu-id="c8c9b-843">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="c8c9b-844">Nome utente di **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="c8c9b-844">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8c9b-845">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-845">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-846">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-846">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-847">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-847">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8c9b-848">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-848">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-849">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-849">Allowed From</span></span>

<span data-ttu-id="c8c9b-850">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-850">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-851">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-851">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTP Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_start_extended"></a><span data-ttu-id="c8c9b-852">nx_web_http_client_put_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-852">nx_web_http_client_put_start_extended</span></span>

<span data-ttu-id="c8c9b-853">Avvia una richiesta HTTP PUT</span><span class="sxs-lookup"><span data-stu-id="c8c9b-853">Start an HTTP PUT request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-854">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-854">Prototype</span></span>

```C
UINT nx_web_http_client_put_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-855">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-855">Description</span></span>

<span data-ttu-id="c8c9b-856">Questo metodo è per http non **crittografato** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-856">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8c9b-857">Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTP in corrispondenza dell'indirizzo IP e della porta forniti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-857">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8c9b-858">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet ()* per inviare il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-858">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-859">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-859">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8c9b-860">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-860">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-861">Questo servizio sostituisce *nx_web_http_client_put_start* ().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-861">This service replaces *nx_web_http_client_put_start* ().</span></span> <span data-ttu-id="c8c9b-862">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-862">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-863">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-863">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-864">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-864">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-865">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-865">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-866">**SERVER_PORT** Porta TCP sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-866">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-867">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-867">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-868">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-868">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-869">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-869">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-870">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-870">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-871">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-871">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-872">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-872">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-873">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-873">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-874">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-874">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-875">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-875">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-876">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-876">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-877">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-877">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8c9b-878">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_web_http_client_put_packet ()* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-878">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8c9b-879">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-879">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-880">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-880">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-881">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-881">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-882">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-882">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-883">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-883">Return Values</span></span>

- <span data-ttu-id="c8c9b-884">**NX_SUCCESS** (0x00) ha inviato una richiesta PUT</span><span class="sxs-lookup"><span data-stu-id="c8c9b-884">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="c8c9b-885">Nome utente di **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="c8c9b-885">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8c9b-886">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-886">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-887">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-887">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-888">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-888">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8c9b-889">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-889">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-890">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-890">Allowed From</span></span>

<span data-ttu-id="c8c9b-891">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-891">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-892">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-892">Example</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTP Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_secure_start"></a><span data-ttu-id="c8c9b-893">nx_web_http_client_put_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-893">nx_web_http_client_put_secure_start</span></span>

<span data-ttu-id="c8c9b-894">Avviare una richiesta PUT HTTPS crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-894">Start an encrypted HTTPS PUT request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-895">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-895">Prototype</span></span>

```C
UINT nx_web_http_client_put_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-896">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-896">Description</span></span>

<span data-ttu-id="c8c9b-897">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-897">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-898">Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTPS nell'indirizzo IP e nella porta specificati.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-898">This service attempts to send a PUT request with the specified resource to the HTTPS Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8c9b-899">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet ()* per inviare il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-899">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-900">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-900">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8c9b-901">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-901">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-902">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_put_secure_start_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-902">Developers are encouraged to use *nx_web_http_client_put_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-903">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-903">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-904">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-904">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-905">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-905">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-906">**SERVER_PORT** Porta TCP sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-906">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-907">**risorsa** di Puntatore alla stringa URL per la risorsa da inviare al server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-907">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="c8c9b-908">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-908">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-909">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-909">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-910">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-910">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-911">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-911">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-912">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-912">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-913">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-913">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8c9b-914">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_web_http_client_put_packet ()* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-914">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8c9b-915">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-915">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-916">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-916">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-917">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-917">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-918">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-918">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-919">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-919">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-920">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-920">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-921">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-921">Return Values</span></span>

- <span data-ttu-id="c8c9b-922">**NX_SUCCESS** (0x00) ha inviato una richiesta PUT</span><span class="sxs-lookup"><span data-stu-id="c8c9b-922">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="c8c9b-923">Nome utente di **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="c8c9b-923">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8c9b-924">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-924">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-925">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-925">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-926">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-926">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8c9b-927">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-927">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-928">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-928">Allowed From</span></span>

<span data-ttu-id="c8c9b-929">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-929">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-930">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-930">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_secure_start_extended"></a><span data-ttu-id="c8c9b-931">nx_web_http_client_put_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-931">nx_web_http_client_put_secure_start_extended</span></span>

<span data-ttu-id="c8c9b-932">Avviare una richiesta PUT HTTPS crittografata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-932">Start an encrypted HTTPS PUT request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-933">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-933">Prototype</span></span>

```C
UINT nx_web_http_client_put_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-934">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-934">Description</span></span>

<span data-ttu-id="c8c9b-935">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-935">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-936">Questo servizio tenta di inviare una richiesta PUT con la risorsa specificata al server HTTPS nell'indirizzo IP e nella porta specificati.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-936">This service attempts to send a PUT request with the specified resource to the HTTPS Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8c9b-937">Se questa routine ha esito positivo, il codice dell'applicazione deve effettuare chiamate successive alla routine *nx_web_http_client_put_packet ()* per inviare il contenuto della risorsa al server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-937">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-938">Si noti che la stringa di risorsa può fare riferimento a un file locale, ad esempio "/index.htm" oppure può fare riferimento a un altro URL, ad esempio `http://abc.website.com/index.htm` se il server HTTP indica che supporta il rinvio delle richieste PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-938">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8c9b-939">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-939">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-940">Questo servizio sostituisce *nx_web_http_client_put_secure_start*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-940">This service replaces *nx_web_http_client_put_secure_start*().</span></span> <span data-ttu-id="c8c9b-941">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-941">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-942">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-942">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-943">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-943">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-944">**ip_address** Indirizzo IP del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-944">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-945">**SERVER_PORT** Porta TCP sul server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-945">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-946">**risorsa** di Puntatore alla stringa URL per la risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-946">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8c9b-947">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-947">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-948">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-948">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-949">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-949">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-950">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-950">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-951">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-951">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-952">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-952">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-953">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-953">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-954">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-954">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-955">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-955">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-956">**total_bytes** Byte totali della risorsa inviata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-956">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8c9b-957">Si noti che la lunghezza combinata di tutti i pacchetti inviati tramite chiamate successive a *nx_web_http_client_put_packet ()* deve essere uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-957">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8c9b-958">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-958">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-959">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-959">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-960">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-960">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-961">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-961">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-962">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-962">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-963">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-963">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-964">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-964">Return Values</span></span>

- <span data-ttu-id="c8c9b-965">**NX_SUCCESS** (0x00) ha inviato una richiesta PUT</span><span class="sxs-lookup"><span data-stu-id="c8c9b-965">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="c8c9b-966">Nome utente di **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) troppo grande per il buffer</span><span class="sxs-lookup"><span data-stu-id="c8c9b-966">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8c9b-967">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-967">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-968">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-968">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-969">NX_SIZE_ERROR (0x09) dimensioni totali non valide della risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-969">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8c9b-970">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-970">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-971">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-971">Allowed From</span></span>

<span data-ttu-id="c8c9b-972">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-972">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-973">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-973">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_packet"></a><span data-ttu-id="c8c9b-974">nx_web_http_client_put_packet</span><span class="sxs-lookup"><span data-stu-id="c8c9b-974">nx_web_http_client_put_packet</span></span>

<span data-ttu-id="c8c9b-975">Invia pacchetto di dati di risorse successivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-975">Send next resource data packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-976">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-976">Prototype</span></span>

```C
UINT nx_web_http_client_put_packet(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-977">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-977">Description</span></span>

<span data-ttu-id="c8c9b-978">Questo servizio tenta di inviare il pacchetto successivo di contenuto di risorse al server HTTP per le operazioni PUT e POST.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-978">This service attempts to send the next packet of resource content to the HTTP Server for both PUT and POST operations.</span></span> <span data-ttu-id="c8c9b-979">Si noti che questa routine deve essere chiamata ripetutamente fino a quando la lunghezza combinata dei pacchetti inviati è uguale alla "total_bytes" specificata nella chiamata *nx_web_http_client_put_start ()* o *nx_web_http_client_post_start ()* precedente (o nelle versioni sicure corrispondenti).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-979">Note that this routine should be called repetitively until the combined length of the packets sent equals the "total_bytes" specified in the previous *nx_web_http_client_put_start()* or *nx_web_http_client_post_start()* call (or their corresponding secure versions).</span></span>

<span data-ttu-id="c8c9b-980">Questo servizio controlla anche la presenza di una risposta dal server nel caso in cui si sia verificato un problema durante il tentativo di stabilire la connessione HTTP (o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-980">This service also checks for a response from the server in case there was a problem establishing the HTTP (or HTTPS) connection.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-981">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-981">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-982">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-982">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-983">**packet_ptr** Puntatore al contenuto successivo della risorsa da inviare al server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-983">**packet_ptr** Pointer to next content of the resource to being sent to the HTTP Server.</span></span>
- <span data-ttu-id="c8c9b-984">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-984">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-985">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-985">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-986">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-986">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-987">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-987">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-988">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-988">Return Values</span></span>

- <span data-ttu-id="c8c9b-989">Il pacchetto client HTTP è stato inviato **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-989">**NX_SUCCESS** (0x00) Successfully sent HTTP Client packet.</span></span>
- <span data-ttu-id="c8c9b-990">Client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non pronto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-990">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8c9b-991">**NX_WEB_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0X3000E) ha ricevuto il codice di errore del server \* \*</span><span class="sxs-lookup"><span data-stu-id="c8c9b-991">**NX_WEB_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0x3000E) Received Server error code\*\*</span></span>
- <span data-ttu-id="c8c9b-992">Lunghezza del pacchetto **NX_WEB_HTTP_BAD_PACKET_LENGTH** (0X3000D) non valida</span><span class="sxs-lookup"><span data-stu-id="c8c9b-992">**NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000D) Invalid packet length</span></span>
- <span data-ttu-id="c8c9b-993">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) nome e/o password non validi</span><span class="sxs-lookup"><span data-stu-id="c8c9b-993">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or Password</span></span>
- <span data-ttu-id="c8c9b-994">Il server **NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) risponde prima del completamento dell'operazione Put</span><span class="sxs-lookup"><span data-stu-id="c8c9b-994">**NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) Server responds before PUT is complete</span></span>
- <span data-ttu-id="c8c9b-995">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-995">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-996">Pacchetto di NX_INVALID_PACKET (0x12) troppo piccolo per l'intestazione TCP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-996">NX_INVALID_PACKET (0x12) Packet too small for TCP header</span></span>
- <span data-ttu-id="c8c9b-997">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-997">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-998">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-998">Allowed From</span></span>

<span data-ttu-id="c8c9b-999">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-999">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1000">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1000">Example</span></span>

```C
/* Send a 20-byte packet representing the content of the resource
    "/TEST.HTM" to the HTTP Server. */

status = nx_web_http_client_put_packet(&client_ptr, packet_ptr, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM has
    successfully been sent. */
```

## <a name="nx_web_http_client_request_chunked_set"></a><span data-ttu-id="c8c9b-1001">nx_web_http_client_request_chunked_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1001">nx_web_http_client_request_chunked_set</span></span>

<span data-ttu-id="c8c9b-1002">Imposta il trasferimento Chunked per la richiesta HTTP (S)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1002">Set chunked transfer for HTTP(S) request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1003">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1003">Prototype</span></span>

```C
UINT nx_web_http_client_request_chunked_set(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT chunk_size, NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1004">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1004">Description</span></span>

<span data-ttu-id="c8c9b-1005">Questo servizio usa la codifica di trasferimento Chunked per inviare una richiesta HTTP (S) personalizzata al server specificato nella chiamata *nx_web_http_client_connect ()* o *nx_web_http_client_secure_connect ()* che ha precedentemente stabilito la connessione socket all'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1005">This service uses chunked transfer coding to send a custom HTTP(S) request to the server specified in the *nx_web_http_client_connect()* or *nx_web_http_client_secure_connect()* call which has previously established the socket connection to the remote host.</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-1006">Se l'applicazione usa la codifica di trasferimento Chunked per inviare un pacchetto di dati di richiesta, deve chiamare questo servizio dopo aver chiamato *nx_web_http_client_request_packet_allocate*() e prima di chiamare *nx_web_http_client_reqeust_packet_send* ().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1006">If the application uses chunked transfer coding to send a request data packet, it must call this service after calling *nx_web_http_client_request_packet_allocate*(), and before call *nx_web_http_client_reqeust_packet_send* ().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1007">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1007">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1008">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1008">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1009">**chunk_size** Dimensione dei blocchi-dati in ottetti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1009">**chunk_size** Size of the chunk-data in octets.</span></span>
- <span data-ttu-id="c8c9b-1010">**packet_ptr** Puntatore ai pacchetti di dati della richiesta HTTP (S).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1010">**packet_ptr** HTTP(S) request data packet pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1011">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1011">Return Values</span></span>

- <span data-ttu-id="c8c9b-1012">**NX_SUCCESS** (0x00) ha impostato la suddivisione in blocchi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1012">**NX_SUCCESS** (0x00) Successfully set chunked.</span></span>
- <span data-ttu-id="c8c9b-1013">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1013">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1014">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1014">Allowed From</span></span>

<span data-ttu-id="c8c9b-1015">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1015">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1016">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1016">Example</span></span>

```C
/* Connect to a remote HTTPS server. */

nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a PUT request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_PUT, "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_TRUE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the PUT operation. */
nx_web_http_client_request_send(&my_client, 1000);

/* Create a new data packet request on the HTTP(S) client instance. */
nx_web_http_client_request_packet_allocate(&my_client,
    &my_packet,
    NX_WAIT_FOREVER);

/* Set the chunked transfer. */
status = nx_web_http_client_request_chunked_set(&my_client, 128, my_packet);

/* At this point, user can fill the data into my_packet. *./
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet request to server. */
nx_web_http_client_request_packet_send(&my_client, my_packet,
    0, NX_WAIT_FOREVER);
```

## <a name="nx_web_http_client_request_header_add"></a><span data-ttu-id="c8c9b-1017">nx_web_http_client_request_header_add</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1017">nx_web_http_client_request_header_add</span></span>

<span data-ttu-id="c8c9b-1018">Aggiungere un'intestazione personalizzata a una richiesta HTTP personalizzata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1018">Add a custom header to a custom HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1019">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1019">Prototype</span></span>

```C
UINT nx_web_http_client_request_header_add(
    NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *field_name, UINT name_length,
    CHAR *field_value, UINT value_length,
    UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1020">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1020">Description</span></span>

<span data-ttu-id="c8c9b-1021">Questo servizio aggiunge un'intestazione personalizzata (sotto forma di nome e valore del campo) a una richiesta HTTP personalizzata creata con n *x_web_http_client_request_initialize ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1021">This service adds a custom header (in the form of a field name and value) to a custom HTTP request created with n *x_web_http_client_request_initialize()*.</span></span>

<span data-ttu-id="c8c9b-1022">L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1022">Use of this service enables an application to add any number of custom headers to the request.</span></span> <span data-ttu-id="c8c9b-1023">**Questo consente richieste HTTP personalizzate destinate ad applicazioni specifiche.**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1023">**This allows for customized HTTP requests intended for specific applications.**</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-1024">I \* metodi di _start nx_web_http_client_ sono forniti per praticità.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1024">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8c9b-1025">Queste funzioni usano tutte questa routine internamente (insieme a *nx_web_http_client_request_initialize ())* per creare e inviare richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1025">These functions all use this routine internally (along with *nx_web_http_client_request_initialize())* to create and send HTTP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1026">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1026">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1027">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1027">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1028">**FIELD_NAME** Stringa del nome del campo (ad esempio "Content-Type").</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1028">**field_name** Field name string (e.g. "Content-Type").</span></span>
- <span data-ttu-id="c8c9b-1029">**name_length** Lunghezza della stringa del nome del campo in byte.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1029">**name_length** Length of field name string in bytes.</span></span>
- <span data-ttu-id="c8c9b-1030">**FIELD_VALUE** Stringa del valore del campo (ad esempio "Application/ottetto-Stream").</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1030">**field_value** Field value string (e.g. "application/octet-stream").</span></span>
- <span data-ttu-id="c8c9b-1031">**value_length** Lunghezza della stringa valore in byte.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1031">**value_length** Length of value string in bytes.</span></span>
- <span data-ttu-id="c8c9b-1032">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1032">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-1033">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1033">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1034">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1034">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-1035">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1035">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1036">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1036">Return Values</span></span>

- <span data-ttu-id="c8c9b-1037">**NX_SUCCESS** (0x00) aggiunta dell'intestazione da richiedere.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1037">**NX_SUCCESS** (0x00) Successful addition of header to request.</span></span>
- <span data-ttu-id="c8c9b-1038">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1038">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1039">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1039">Allowed From</span></span>

<span data-ttu-id="c8c9b-1040">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1040">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1041">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1041">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */

nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server
    by repeatedly calling *nx_web_http_client_response_body_get()*
    until the entire response is retrieved. *./

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_initialize"></a><span data-ttu-id="c8c9b-1042">nx_web_http_client_request_initialize</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1042">nx_web_http_client_request_initialize</span></span>

<span data-ttu-id="c8c9b-1043">Inizializzare una richiesta HTTP personalizzata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1043">Initialize a custom HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1044">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1044">Prototype</span></span>

```C
UINT nx_web_http_client_request_initialize(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT method, CHAR *resource, CHAR *host,
    UINT input_size, UINT transfer_encoding_trunked,
    CHAR *username, CHAR *password, UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1045">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1045">Description</span></span>

<span data-ttu-id="c8c9b-1046">Questo servizio crea una richiesta HTTP personalizzata e la associa all'istanza del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1046">This service creates a custom HTTP request and associates it with the HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-1047">Diversamente dalla nx_web_http_client_get_start più semplice *()* (insieme ai metodi per put, post e le versioni sicure associate di tali API), la richiesta personalizzata non viene inviata finché non viene chiamato il servizio *nx_web_http_client_request_send ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1047">Unlike the simpler *nx_web_http_client_get_start()* (along with the methods for PUT, POST, and the associated secure versions of those API), the custom request is not sent until the *nx_web_http_client_request_send()* service is called.</span></span>

<span data-ttu-id="c8c9b-1048">L'utilizzo di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta utilizzando il servizio ***nx_web_http_client_request_header_add ()*** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1048">Use of this service enables an application to add any number of custom headers to the request using the ***nx_web_http_client_request_header_add()*** service.</span></span> <span data-ttu-id="c8c9b-1049">Questo consente richieste HTTP personalizzate destinate ad applicazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1049">This allows for customized HTTP requests intended for specific applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-1050">I \* metodi di _start nx_web_http_client_ sono forniti per praticità.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1050">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8c9b-1051">Queste funzioni usano tutte questa routine internamente (insieme a *nx_web_http_client_request_send ())* per creare e inviare richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1051">These functions all use this routine internally (along with *nx_web_http_client_request_send())* to create and send HTTP requests.</span></span>

<span data-ttu-id="c8c9b-1052">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1052">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-1053">Gli sviluppatori sono invitati a utilizzare *nx_web_http_client_request_initialize_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1053">Developers are encouraged to use *nx_web_http_client_request_initialize_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1054">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1054">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1055">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1055">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1056">**Metodo** Metodo di richiesta HTTP da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1056">**method** The HTTP request method to use.</span></span> <span data-ttu-id="c8c9b-1057">Le opzioni sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1057">The options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1058">**NX_WEB_HTTP_METHOD_NONE (0x0)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1058">**NX_WEB_HTTP_METHOD_NONE (0x0)**</span></span>
  - <span data-ttu-id="c8c9b-1059">**NX_WEB_HTTP_METHOD_GET (0x1)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1059">**NX_WEB_HTTP_METHOD_GET (0x1)**</span></span>
  - <span data-ttu-id="c8c9b-1060">**NX_WEB_HTTP_METHOD_PUT (0x2)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1060">**NX_WEB_HTTP_METHOD_PUT (0x2)**</span></span>
  - <span data-ttu-id="c8c9b-1061">**NX_WEB_HTTP_METHOD_POST (0x3)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1061">**NX_WEB_HTTP_METHOD_POST (0x3)**</span></span>
  - <span data-ttu-id="c8c9b-1062">**NX_WEB_HTTP_METHOD_DELETE (0x4)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1062">**NX_WEB_HTTP_METHOD_DELETE (0x4)**</span></span>
  - <span data-ttu-id="c8c9b-1063">**NX_WEB_HTTP_METHOD_HEAD (0x5)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1063">**NX_WEB_HTTP_METHOD_HEAD (0x5)**</span></span>
- <span data-ttu-id="c8c9b-1064">**risorsa** di Nome della risorsa da trasferire.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1064">**resource** Name of resource being transferred.</span></span>
- <span data-ttu-id="c8c9b-1065">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1065">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-1066">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1066">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-1067">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1067">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-1068">**input_size** Dimensioni dei dati di input per PUT e POST.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1068">**input_size** Size of input data for PUT and POST.</span></span> <span data-ttu-id="c8c9b-1069">Passaggio 0 per altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1069">Pass 0 for other operations.</span></span>
- <span data-ttu-id="c8c9b-1070">**transfer_encoding_trunked** Parametro riservato per il futuro supporto per trasferimento con trunking.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1070">**transfer_encoding_trunked** Reserved parameter for future trunked transfer support.</span></span>
- <span data-ttu-id="c8c9b-1071">**nome utente** Nome utente per le risorse protette.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1071">**username** Username for protected resources.</span></span>
- <span data-ttu-id="c8c9b-1072">**password** di Password per le risorse protette.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1072">**password** Password for protected resources.</span></span>
- <span data-ttu-id="c8c9b-1073">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1073">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-1074">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1074">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1075">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1075">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-1076">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1076">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1077">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1077">Return Values</span></span>

- <span data-ttu-id="c8c9b-1078">**NX_SUCCESS** (0x00) inizializzazione della richiesta completata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1078">**NX_SUCCESS** (0x00) Successful initialization of request.</span></span>
- <span data-ttu-id="c8c9b-1079">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1079">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1080">NX_WEB_HTTP_METHOD_ERROR (0x30014) mancano alcune informazioni necessarie, ad esempio input_size per PUT o POST.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1080">NX_WEB_HTTP_METHOD_ERROR (0x30014) Some required information was missing (e.g. input_size for PUT or POST).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1081">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1081">Allowed From</span></span>

<span data-ttu-id="c8c9b-1082">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1082">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1083">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1083">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */

status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get()* until the entire response is retrieved. *./
get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_initialize_extended"></a><span data-ttu-id="c8c9b-1084">nx_web_http_client_request_initialize_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1084">nx_web_http_client_request_initialize_extended</span></span>

<span data-ttu-id="c8c9b-1085">Inizializzare una richiesta HTTP personalizzata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1085">Initialize a custom HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1086">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1086">Prototype</span></span>

```C
UINT nx_web_http_client_request_initialize(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT method, CHAR *resource, CHAR *host,
    UINT input_size, UINT transfer_encoding_trunked,
    CHAR *username, CHAR *password, UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1087">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1087">Description</span></span>

<span data-ttu-id="c8c9b-1088">Questo servizio crea una richiesta HTTP personalizzata e la associa all'istanza del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1088">This service creates a custom HTTP request and associates it with the HTTP Client instance.</span></span> <span data-ttu-id="c8c9b-1089">Diversamente dalla nx_web_http_client_get_start più semplice *()* (insieme ai metodi per put, post e le versioni sicure associate di tali API), la richiesta personalizzata non viene inviata finché non viene chiamato il servizio *nx_web_http_client_request_send ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1089">Unlike the simpler *nx_web_http_client_get_start()* (along with the methods for PUT, POST, and the associated secure versions of those API), the custom request is not sent until the *nx_web_http_client_request_send()* service is called.</span></span>

<span data-ttu-id="c8c9b-1090">L'utilizzo di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta utilizzando il servizio ***nx_web_http_client_request_header_add ()*** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1090">Use of this service enables an application to add any number of custom headers to the request using the ***nx_web_http_client_request_header_add()*** service.</span></span> <span data-ttu-id="c8c9b-1091">Questo consente richieste HTTP personalizzate destinate ad applicazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1091">This allows for customized HTTP requests intended for specific applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-1092">I \* metodi di _start nx_web_http_client_ sono forniti per praticità.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1092">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8c9b-1093">Queste funzioni usano tutte questa routine internamente (insieme a *nx_web_http_client_request_send ())* per creare e inviare richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1093">These functions all use this routine internally (along with *nx_web_http_client_request_send())* to create and send HTTP requests.</span></span>

<span data-ttu-id="c8c9b-1094">Le stringhe di risorsa, host, nome utente e password devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1094">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-1095">Questo servizio sostituisce *nx_web_http_client_request_initialize*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1095">This service replaces *nx_web_http_client_request_initialize*().</span></span> <span data-ttu-id="c8c9b-1096">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1096">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1097">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1097">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1098">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1098">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1099">**Metodo** Metodo di richiesta HTTP da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1099">**method** The HTTP request method to use.</span></span> <span data-ttu-id="c8c9b-1100">Le opzioni sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1100">The options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1101">**NX_WEB_HTTP_METHOD_NONE (0x0)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1101">**NX_WEB_HTTP_METHOD_NONE (0x0)**</span></span>
  - <span data-ttu-id="c8c9b-1102">**NX_WEB_HTTP_METHOD_GET (0x1)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1102">**NX_WEB_HTTP_METHOD_GET (0x1)**</span></span>
  - <span data-ttu-id="c8c9b-1103">**NX_WEB_HTTP_METHOD_PUT (0x2)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1103">**NX_WEB_HTTP_METHOD_PUT (0x2)**</span></span>
  - <span data-ttu-id="c8c9b-1104">**NX_WEB_HTTP_METHOD_POST (0x3)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1104">**NX_WEB_HTTP_METHOD_POST (0x3)**</span></span>
  - <span data-ttu-id="c8c9b-1105">**NX_WEB_HTTP_METHOD_DELETE (0x4)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1105">**NX_WEB_HTTP_METHOD_DELETE (0x4)**</span></span>
  - <span data-ttu-id="c8c9b-1106">**NX_WEB_HTTP_METHOD_HEAD (0x5)**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1106">**NX_WEB_HTTP_METHOD_HEAD (0x5)**</span></span>
- <span data-ttu-id="c8c9b-1107">**risorsa** di Nome della risorsa da trasferire.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1107">**resource** Name of resource being transferred.</span></span>
- <span data-ttu-id="c8c9b-1108">**resource_length** Lunghezza della stringa della risorsa richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1108">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8c9b-1109">**host** di Stringa con terminazione null del nome di dominio del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1109">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8c9b-1110">Questa stringa viene trasmessa nel campo dell'intestazione host HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1110">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8c9b-1111">La stringa host non può essere NULL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1111">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8c9b-1112">**host_length** Lunghezza della stringa dell'host.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1112">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8c9b-1113">**input_size** Dimensioni dei dati di input per PUT e POST.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1113">**input_size** Size of input data for PUT and POST.</span></span> <span data-ttu-id="c8c9b-1114">Passaggio 0 per altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1114">Pass 0 for other operations.</span></span>
- <span data-ttu-id="c8c9b-1115">**transfer_encoding_trunked** Parametro riservato per il futuro supporto per trasferimento con trunking.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1115">**transfer_encoding_trunked** Reserved parameter for future trunked transfer support.</span></span>
- <span data-ttu-id="c8c9b-1116">**nome utente** Puntatore al nome utente facoltativo per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1116">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-1117">**username_length** Lunghezza della stringa del nome utente per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1117">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8c9b-1118">**password** di Puntatore alla password facoltativa per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1118">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8c9b-1119">**password_length** Lunghezza della stringa di password per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1119">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8c9b-1120">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1120">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-1121">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1121">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1122">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1122">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-1123">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1123">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1124">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1124">Return Values</span></span>

- <span data-ttu-id="c8c9b-1125">**NX_SUCCESS** (0x00) inizializzazione della richiesta completata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1125">**NX_SUCCESS** (0x00) Successful initialization of request.</span></span>
- <span data-ttu-id="c8c9b-1126">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1126">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1127">NX_WEB_HTTP_METHOD_ERROR (0x30014) mancano alcune informazioni necessarie, ad esempio input_size per PUT o POST.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1127">NX_WEB_HTTP_METHOD_ERROR (0x30014) Some required information was missing (e.g. input_size for PUT or POST).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1128">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1128">Allowed From</span></span>

<span data-ttu-id="c8c9b-1129">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1129">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1130">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1130">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize_extended(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "test.txt ", sizeof("test.txt ") – 1,
    "host.com", sizeof("host.com") – 1,
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    0,
    NX_NULL, /* password */
    0,
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);


/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get()* until the entire response is retrieved. *./
get_status = NX_SUCCESS;
while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_packet_send"></a><span data-ttu-id="c8c9b-1131">nx_web_http_client_request_packet_send</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1131">nx_web_http_client_request_packet_send</span></span>

<span data-ttu-id="c8c9b-1132">Invia pacchetto di dati di richiesta HTTP (S) al server remoto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1132">Send HTTP(S) request data packet to remote server</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1133">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1133">Prototype</span></span>

```C
UINT nx_web_http_client_request_packet_send(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET *packet_ptr, UINT more_date,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1134">Description</span></span>

<span data-ttu-id="c8c9b-1135">Questo servizio invia un pacchetto di dati di richiesta HTTP (S) personalizzato creato con *nx_web_http_client_request_packet_allocate* () al server specificato nella chiamata *nx_web_http_client_connect ()* o *nx_web_http_client_secure_connect (*) che ha precedentemente stabilito la connessione socket all'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1135">This service sends a custom HTTP(S) request data packet created with *nx_web_http_client_request_packet_allocate* () to the server specified in the *nx_web_http_client_connect()* or *nx_web_http_client_secure_connect(*) call which has previously established the socket connection to the remote host.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1136">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1136">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1137">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1137">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1138">**packet_ptr** Puntatore ai pacchetti di dati della richiesta HTTP (S).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1138">**packet_ptr** HTTP(S) request data packet pointer.</span></span>
- <span data-ttu-id="c8c9b-1139">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1139">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-1140">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1140">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1141">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1141">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-1142">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1142">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1143">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1143">Return Values</span></span>

- <span data-ttu-id="c8c9b-1144">**NX_SUCCESS** (0x00) invio del pacchetto di dati della richiesta riuscito.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1144">**NX_SUCCESS** (0x00) Successful send of request data packet.</span></span>
- <span data-ttu-id="c8c9b-1145">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1145">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1146">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1146">Allowed From</span></span>

<span data-ttu-id="c8c9b-1147">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1147">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1148">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1148">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a PUT request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_PUT,
    "https://192.168.1.150/test.txt ",
    128, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the PUT operation. */
nx_web_http_client_request_send(&my_client, 1000);

/* Create a new data packet request on the HTTP(S) client instance. */
nx_web_http_client_request_packet_allocate(&my_client,
    &my_packet,
    NX_WAIT_FOREVER);

/* At this point, user can fill the data into my_packet. *./
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet request to server. */
status = nx_web_http_client_request_packet_send(&my_client,
    my_packet,
    0,
    NX_WAIT_FOREVER);
```

## <a name="nx_web_http_client_request_send"></a><span data-ttu-id="c8c9b-1149">nx_web_http_client_request_send</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1149">nx_web_http_client_request_send</span></span>

<span data-ttu-id="c8c9b-1150">Inviare una richiesta HTTP personalizzata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1150">Send a custom HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1151">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1151">Prototype</span></span>

```C
UINT nx_web_http_client_request_send(NX_WEB_HTTP_CLIENT *client_ptr,
    UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1152">Description</span></span>

<span data-ttu-id="c8c9b-1153">Questo servizio invia una richiesta HTTP personalizzata creata con *nx_web_http_client_request_initialize ()* al server specificato nell' *nx_web_http_client_connect ()* o *nx_web_http_client_secure_connect ()* entrambi i quali hanno stabilito in precedenza la connessione al socket per l'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1153">This service sends a custom HTTP request created with *nx_web_http_client_request_initialize()* to the server specified in the *nx_web_http_client_connect()* or *nx_web_http_client_secure_connect()* both of which have previously established the socket connection to the remote host.</span></span>

<span data-ttu-id="c8c9b-1154">L'utilizzo di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta utilizzando il servizio ***nx_web_http_client_request_header_add ()*** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1154">Use of this service enables an application to add any number of custom headers to the request using the ***nx_web_http_client_request_header_add()*** service.</span></span> <span data-ttu-id="c8c9b-1155">Questo consente richieste HTTP personalizzate destinate ad applicazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1155">This allows for customized HTTP requests intended for specific applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-1156">I \* metodi di _start nx_web_http_client_ sono forniti per praticità.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1156">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8c9b-1157">Queste funzioni usano tutte questa routine internamente (insieme a *nx_web_http_client_request_initialize ())* per creare e inviare richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1157">These functions all use this routine internally (along with *nx_web_http_client_request_initialize())* to create and send HTTP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1158">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1158">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1159">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1159">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1160">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1160">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-1161">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1161">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1162">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1162">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-1163">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1163">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1164">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1164">Return Values</span></span>

- <span data-ttu-id="c8c9b-1165">**NX_SUCCESS** (0x00) invio della richiesta riuscita.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1165">**NX_SUCCESS** (0x00) Successful send of request.</span></span>
- <span data-ttu-id="c8c9b-1166">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1166">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1167">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1167">Allowed From</span></span>

<span data-ttu-id="c8c9b-1168">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1168">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1169">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1169">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by
    repeatedly calling *nx_web_http_client_response_body_get* until
    the entire response is retrieved. *./

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_response_body_get"></a><span data-ttu-id="c8c9b-1170">nx_web_http_client_response_body_get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1170">nx_web_http_client_response_body_get</span></span>

<span data-ttu-id="c8c9b-1171">Ottenere il pacchetto di dati di risorse successivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1171">Get next resource data packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1172">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1172">Prototype</span></span>

```C
UINT nx_web_http_client_response_body_get(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET **packet_ptr, ULONG
    wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1173">Description</span></span>

<span data-ttu-id="c8c9b-1174">Questo servizio recupera il pacchetto successivo di contenuto della risorsa richiesta dalla chiamata precedente a *nx_web_http_client_get_start ()* o *nx_web_http_client_get_secure_start ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1174">This service retrieves the next packet of content of the resource requested by the previous *nx_web_http_client_get_start()* or *nx_web_http_client_get_secure_start()* call.</span></span> <span data-ttu-id="c8c9b-1175">Le chiamate successive a questa routine devono essere apportate fino a quando non viene ricevuto lo stato di restituzione del NX_WEB_HTTP_GET_DONE.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1175">Successive calls to this routine should be made until the return status of NX_WEB_HTTP_GET_DONE is received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1176">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1176">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1177">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1177">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1178">**packet_ptr** Destinazione per il puntatore del pacchetto che contiene il contenuto parziale delle risorse.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1178">**packet_ptr** Destination for packet pointer containing partial resource content.</span></span>
- <span data-ttu-id="c8c9b-1179">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1179">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-1180">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1180">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1181">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1181">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-1182">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1182">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1183">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1183">Return Values</span></span>

- <span data-ttu-id="c8c9b-1184">**NX_SUCCESS** (0x00) ha esito positivo Get del pacchetto client http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1184">**NX_SUCCESS** (0x00) Successful get of HTTP Client packet.</span></span>
- <span data-ttu-id="c8c9b-1185">**NX_WEB_HTTP_GET_DONE** (0X3000C) client HTTP Get packet is done</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1185">**NX_WEB_HTTP_GET_DONE** (0x3000C) HTTP Client get packet is done</span></span>
- <span data-ttu-id="c8c9b-1186">Il client HTTP **NX_WEB_HTTP_NOT_READY** (0x3000A) non è in modalità Get.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1186">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not in get mode.</span></span>
- <span data-ttu-id="c8c9b-1187">Lunghezza del pacchetto **NX_WEB_HTTP_BAD_PACKET_LENGTH** (0X3000D) non valida</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1187">**NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000D) Invalid packet length</span></span>
- <span data-ttu-id="c8c9b-1188">**NX_WEB_HTTP_STATUS_CODE_CONTINUE** (0x3001A) codice di stato HTTP 100 continua</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1188">**NX_WEB_HTTP_STATUS_CODE_CONTINUE** (0x3001A) HTTP status code 100 Continue</span></span>
- <span data-ttu-id="c8c9b-1189">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_SWITCHING_PROTOCOLS** (0x3001B) 101 scambio di protocolli</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1189">**NX_WEB_HTTP_STATUS_CODE_SWITCHING_PROTOCOLS** (0x3001B) HTTP status code 101 Switching Protocols</span></span>
- <span data-ttu-id="c8c9b-1190">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_CREATED** (0x3001C) 201 creato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1190">**NX_WEB_HTTP_STATUS_CODE_CREATED** (0x3001C) HTTP status code 201 Created</span></span>
- <span data-ttu-id="c8c9b-1191">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_ACCEPTED** (0x3001D) 202 accettato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1191">**NX_WEB_HTTP_STATUS_CODE_ACCEPTED** (0x3001D) HTTP status code 202 Accepted</span></span>
- <span data-ttu-id="c8c9b-1192">**NX_WEB_HTTP_STATUS_CODE_NON_AUTH_INFO** (0x3001E) codice di stato HTTP 203 informazioni non autorevoli</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1192">**NX_WEB_HTTP_STATUS_CODE_NON_AUTH_INFO** (0x3001E) HTTP status code 203 Non-Authoritative Information</span></span>
- <span data-ttu-id="c8c9b-1193">**NX_WEB_HTTP_STATUS_CODE_NO_CONTENT** (0x3001F) codice di stato HTTP 204 nessun contenuto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1193">**NX_WEB_HTTP_STATUS_CODE_NO_CONTENT** (0x3001F) HTTP status code 204 No Content</span></span>
- <span data-ttu-id="c8c9b-1194">**NX_WEB_HTTP_STATUS_CODE_RESET_CONTENT** (0x30020) codice di stato HTTP 205 Reimposta contenuto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1194">**NX_WEB_HTTP_STATUS_CODE_RESET_CONTENT** (0x30020) HTTP status code 205 Reset Content</span></span>
- <span data-ttu-id="c8c9b-1195">**NX_WEB_HTTP_STATUS_CODE_PARTIAL_CONTENT** (0x30021) codice di stato HTTP 206 contenuto parziale</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1195">**NX_WEB_HTTP_STATUS_CODE_PARTIAL_CONTENT** (0x30021) HTTP status code 206 Partial Content</span></span>
- <span data-ttu-id="c8c9b-1196">Codice di stato HTTP **NX_WEB_HTTP_STATUS_CODE_MULTIPLE_CHOICES** (0x30022) 300 opzioni multiple</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1196">**NX_WEB_HTTP_STATUS_CODE_MULTIPLE_CHOICES** (0x30022) HTTP status code 300 Multiple Choices</span></span>
- <span data-ttu-id="c8c9b-1197">Il codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_MOVED_PERMANETLY** (0x30023) 301 è stato spostato in modo permanente</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1197">**NX_WEB_HTTP_STATUS_CODE_MOVED_PERMANETLY** (0x30023) HTTP status code 301 Moved Permanently</span></span>
- <span data-ttu-id="c8c9b-1198">Codice di stato HTTP **NX_WEB_HTTP_STATUS_CODE_FOUND** (0x30024) 302 trovato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1198">**NX_WEB_HTTP_STATUS_CODE_FOUND** (0x30024) HTTP status code 302 Found</span></span>
- <span data-ttu-id="c8c9b-1199">**NX_WEB_HTTP_STATUS_CODE_SEE_OTHER** (0x30025) codice di stato HTTP 303 vedere altro</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1199">**NX_WEB_HTTP_STATUS_CODE_SEE_OTHER** (0x30025) HTTP status code 303 See Other</span></span>
- <span data-ttu-id="c8c9b-1200">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_NOT_MODIFIED** (0x30026) 304 non modificato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1200">**NX_WEB_HTTP_STATUS_CODE_NOT_MODIFIED** (0x30026) HTTP status code 304 Not Modified</span></span>
- <span data-ttu-id="c8c9b-1201">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_USE_PROXY** (0x30027) 305 uso del proxy</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1201">**NX_WEB_HTTP_STATUS_CODE_USE_PROXY** (0x30027) HTTP status code 305 Use Proxy</span></span>
- <span data-ttu-id="c8c9b-1202">**NX_WEB_HTTP_STATUS_CODE_TEMPORARY_REDIRECT** (0x30028) codice di stato HTTP 307 Reindirizzamento temporaneo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1202">**NX_WEB_HTTP_STATUS_CODE_TEMPORARY_REDIRECT** (0x30028) HTTP status code 307 Temporary Redirect</span></span>
- <span data-ttu-id="c8c9b-1203">**NX_WEB_HTTP_STATUS_CODE_BAD_REQUEST** (0x30029) codice di stato HTTP 400 richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1203">**NX_WEB_HTTP_STATUS_CODE_BAD_REQUEST** (0x30029) HTTP status code 400 Bad Request</span></span>
- <span data-ttu-id="c8c9b-1204">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_UNAUTHORIZED** (0x3002A) 401 non autorizzato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1204">**NX_WEB_HTTP_STATUS_CODE_UNAUTHORIZED** (0x3002A) HTTP status code 401 Unauthorized</span></span>
- <span data-ttu-id="c8c9b-1205">**NX_WEB_HTTP_STATUS_CODE_PAYMENT_REQUIRED** (0x3002B) codice di stato HTTP 402 pagamento obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1205">**NX_WEB_HTTP_STATUS_CODE_PAYMENT_REQUIRED** (0x3002B) HTTP status code 402 Payment Required</span></span>
- <span data-ttu-id="c8c9b-1206">Codice di stato HTTP **NX_WEB_HTTP_STATUS_CODE_FORBIDDEN** (0x3002C) 403 non consentito</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1206">**NX_WEB_HTTP_STATUS_CODE_FORBIDDEN** (0x3002C) HTTP status code 403 Forbidden</span></span>
- <span data-ttu-id="c8c9b-1207">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_NOT_FOUND** (0x3002D) 404 non trovato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1207">**NX_WEB_HTTP_STATUS_CODE_NOT_FOUND** (0x3002D) HTTP status code 404 Not Found</span></span>
- <span data-ttu-id="c8c9b-1208">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_METHOD_NOT_ALLOWED** (0x3002E) 405 non consentito</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1208">**NX_WEB_HTTP_STATUS_CODE_METHOD_NOT_ALLOWED** (0x3002E) HTTP status code 405 Method Not Allowed</span></span>
- <span data-ttu-id="c8c9b-1209">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_NOT_ACCEPTABLE** (0x3002F) 406 non accettabile</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1209">**NX_WEB_HTTP_STATUS_CODE_NOT_ACCEPTABLE** (0x3002F) HTTP status code 406 Not Acceptable</span></span>
- <span data-ttu-id="c8c9b-1210">**NX_WEB_HTTP_STATUS_CODE_PROXY_AUTH_REQUIRED** (0x30030) codice di stato HTTP 407 Autenticazione proxy necessaria</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1210">**NX_WEB_HTTP_STATUS_CODE_PROXY_AUTH_REQUIRED** (0x30030) HTTP status code 407 Proxy Authentication Required</span></span>
- <span data-ttu-id="c8c9b-1211">**NX_WEB_HTTP_STATUS_CODE_REQUEST_TIMEOUT** (0x30031) codice di stato HTTP 408 Timeout richieste</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1211">**NX_WEB_HTTP_STATUS_CODE_REQUEST_TIMEOUT** (0x30031) HTTP status code 408 Request Time-out</span></span>
- <span data-ttu-id="c8c9b-1212">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_CONFLICT** (0x30032) 409 conflitto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1212">**NX_WEB_HTTP_STATUS_CODE_CONFLICT** (0x30032) HTTP status code 409 Conflict</span></span>
- <span data-ttu-id="c8c9b-1213">Codice di stato HTTP **NX_WEB_HTTP_STATUS_CODE_GONE** (0x30033) 410 andato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1213">**NX_WEB_HTTP_STATUS_CODE_GONE** (0x30033) HTTP status code 410 Gone</span></span>
- <span data-ttu-id="c8c9b-1214">**NX_WEB_HTTP_STATUS_CODE_LENGTH_REQUIRED** (0x30034) codice di stato http 411 lunghezza richiesta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1214">**NX_WEB_HTTP_STATUS_CODE_LENGTH_REQUIRED** (0x30034) HTTP status code 411 Length Required</span></span>
- <span data-ttu-id="c8c9b-1215">**NX_WEB_HTTP_STATUS_CODE_PRECONDITION_FAILED** (0x30035) codice di stato HTTP 412 Precondizione non riuscita</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1215">**NX_WEB_HTTP_STATUS_CODE_PRECONDITION_FAILED** (0x30035) HTTP status code 412 Precondition Failed</span></span>
- <span data-ttu-id="c8c9b-1216">**NX_WEB_HTTP_STATUS_CODE_ENTITY_TOO_LARGE** (0x30036) codice di stato HTTP 413 entità richiesta troppo grande</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1216">**NX_WEB_HTTP_STATUS_CODE_ENTITY_TOO_LARGE** (0x30036) HTTP status code 413 Request Entity Too Large</span></span>
- <span data-ttu-id="c8c9b-1217">**NX_WEB_HTTP_STATUS_CODE_URL_TOO_LARGE** (0x30037) codice di stato HTTP 414 URL richiesta troppo grande</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1217">**NX_WEB_HTTP_STATUS_CODE_URL_TOO_LARGE** (0x30037) HTTP status code 414 Request URL Too Large</span></span>
- <span data-ttu-id="c8c9b-1218">**NX_WEB_HTTP_STATUS_CODE_UNSUPPORTED_MEDIA** (0x30038) codice di stato HTTP 415 tipo di supporto non supportato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1218">**NX_WEB_HTTP_STATUS_CODE_UNSUPPORTED_MEDIA** (0x30038) HTTP status code 415 Unsupported Media Type</span></span>
- <span data-ttu-id="c8c9b-1219">**NX_WEB_HTTP_STATUS_CODE_RANGE_NOT_SATISFY** (0x30039) codice di stato HTTP 416 intervallo richiesto non Impossibile attenersi all'</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1219">**NX_WEB_HTTP_STATUS_CODE_RANGE_NOT_SATISFY** (0x30039) HTTP status code 416 Requested range not satisfiable</span></span>
- <span data-ttu-id="c8c9b-1220">**NX_WEB_HTTP_STATUS_CODE_EXPECTATION_FAILED** (0x3003A) codice di stato HTTP 417 previsione non riuscita</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1220">**NX_WEB_HTTP_STATUS_CODE_EXPECTATION_FAILED** (0x3003A) HTTP status code 417 Expectation Failed</span></span>
- <span data-ttu-id="c8c9b-1221">Codice di stato HTTP **NX_WEB_HTTP_STATUS_CODE_INTERNAL_ERROR** (0x3003B) 500 errore interno del server</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1221">**NX_WEB_HTTP_STATUS_CODE_INTERNAL_ERROR** (0x3003B) HTTP status code 500 Internal Server Error</span></span>
- <span data-ttu-id="c8c9b-1222">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_NOT_IMPLEMENTED** (0x3003C) 501 non implementato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1222">**NX_WEB_HTTP_STATUS_CODE_NOT_IMPLEMENTED** (0x3003C) HTTP status code 501 Not Implemented</span></span>
- <span data-ttu-id="c8c9b-1223">Codice di stato HTTP di **NX_WEB_HTTP_STATUS_CODE_BAD_GATEWAY** (0x3003D) 502 gateway errato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1223">**NX_WEB_HTTP_STATUS_CODE_BAD_GATEWAY** (0x3003D) HTTP status code 502 Bad Gateway</span></span>
- <span data-ttu-id="c8c9b-1224">**NX_WEB_HTTP_STATUS_CODE_SERVICE_UNAVAILABLE** (0x3003E) codice di stato HTTP 503 servizio non disponibile</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1224">**NX_WEB_HTTP_STATUS_CODE_SERVICE_UNAVAILABLE** (0x3003E) HTTP status code 503 Service Unavailable</span></span>
- <span data-ttu-id="c8c9b-1225">**NX_WEB_HTTP_STATUS_CODE_GATEWAY_TIMEOUT** (0x3003F) codice di stato HTTP 504 il timeout del gateway</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1225">**NX_WEB_HTTP_STATUS_CODE_GATEWAY_TIMEOUT** (0x3003F) HTTP status code 504 Gateway Time-out</span></span>
- <span data-ttu-id="c8c9b-1226">**NX_WEB_HTTP_STATUS_CODE_VERSION_ERROR** (0x30040) codice di stato HTTP 505 versione http non supportata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1226">**NX_WEB_HTTP_STATUS_CODE_VERSION_ERROR** (0x30040) HTTP status code 505 HTTP Version not supported</span></span>
- <span data-ttu-id="c8c9b-1227">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1227">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1228">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1228">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1229">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1229">Allowed From</span></span>

<span data-ttu-id="c8c9b-1230">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1230">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1231">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1231">Example</span></span>

```C
/* Get the next packet of resource content on the HTTP Client "my_client."
    Note that the nx_web_http_client_get_start() routine must have been called
    previously. */
status = nx_web_http_client_response_body_get(&my_client, &next_packet, 1000);

/* If status is NX_SUCCESS, the next packet of content is pointed to
    by "next_packet". */
```

## <a name="nx_web_http_client_response_header_callback_set"></a><span data-ttu-id="c8c9b-1232">nx_web_http_client_response_header_callback_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1232">nx_web_http_client_response_header_callback_set</span></span>

<span data-ttu-id="c8c9b-1233">Imposta callback da richiamare durante l'elaborazione di intestazioni HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1233">Set callback to invoke when processing HTTP headers</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1234">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1234">Prototype</span></span>

```C
UINT nx_web_http_client_response_header_callback_set(
    NX_WEB_HTTP_CLIENT *client_ptr,
    VOID (*callback_function)(NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *field_name, UINT field_name_length,
    CHAR *field_value, UINT field_value_length));
```

### <a name="description"></a><span data-ttu-id="c8c9b-1235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1235">Description</span></span>

<span data-ttu-id="c8c9b-1236">Questo servizio assegna un callback che verrà richiamato ogni volta che il client HTTP NetX Web elabora un'intestazione HTTP in una risposta in ingresso da un server HTTP remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1236">This service assigns a callback that will be invoked whenever NetX Web HTTP Client processes an HTTP header in an incoming response from a remote HTTP server.</span></span> <span data-ttu-id="c8c9b-1237">Il callback viene richiamato una volta per ogni intestazione nella risposta mentre viene elaborata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1237">The callback is invoked once for each header in the response as it is processed.</span></span> <span data-ttu-id="c8c9b-1238">Il callback consente a un'applicazione client HTTP di accedere a ciascuna delle intestazioni nella risposta del server HTTP per eseguire qualsiasi azione desiderata oltre l'elaborazione di base che il client HTTP Web di NetX esegue.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1238">The callback allows an HTTP Client application to access each of the headers in the HTTP server response to take any desired actions beyond the basic processing that NetX Web HTTP Client does.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1239">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1239">Input Parameters</span></span>

<span data-ttu-id="c8c9b-1240">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1240">**client_ptr** Pointer to HTTP Client control block.</span></span>

<span data-ttu-id="c8c9b-1241">**callback_function** Callback richiamato durante l'elaborazione dell'intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1241">**callback_function** Callback invoked during response header processing.</span></span> <span data-ttu-id="c8c9b-1242">Il callback viene richiamato con il nome e il valore del campo come stringhe (e le relative lunghezze).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1242">The callback is invoked with the field name and value as strings (and their lengths).</span></span> <span data-ttu-id="c8c9b-1243">Ad esempio, l'intestazione "Content-length: 100" provocherebbe la chiamata della funzione con "Content-Length" per *FIELD_NAME* e la stringa "100" per *FIELD_VALUE*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1243">For example, the header "Content-Length: 100" would cause the function to be invoked with "Content-Length" for *field_name* and the string "100" for *field_value*.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1244">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1244">Return Values</span></span>

- <span data-ttu-id="c8c9b-1245">**NX_SUCCESS** (0x00) assegnazione riuscita del callback.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1245">**NX_SUCCESS** (0x00) Successful assignment of callback.</span></span>
- <span data-ttu-id="c8c9b-1246">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1246">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1247">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1247">Allowed From</span></span>

<span data-ttu-id="c8c9b-1248">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1248">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1249">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1249">Example</span></span>

```C
/* Setup a callback to print out header information as it is processed. */
VOID http_response_callback(NX_WEB_HTTP_CLIENT *client_ptr, CHAR *field_name,
    UINT field_name_length, CHAR *field_value,
    UINT field_value_length)
{
    CHAR name[100];
    CHAR value[100];
    memset(name, 0, sizeof(name));

    memset(value, 0, sizeof(value));

    strncpy(name, field_name, field_name_length);
    strncpy(value, field_value, field_value_length);

    printf("Received header: \n");
    printf("\tField name: %s (%d bytes)\n", name, field_name_length);
    printf("\tValue: %s (%d bytes)\n\n", value, field_value_length);
}

/* Assign the callback to the HTTP client instance. */
nx_web_http_client_response_header_callback_set(&my_client,
    http_response_callback);

/* Start a GET operation to get a response from the HTTP server. */
status = nx_web_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "myname", "mypassword", 1000);

/* When the HTTP server returns a response to the GET request, NetX Web HTTP
    Client will invoke the http_response_callback function for each header
    processed in the HTTP response. */
```

## <a name="nx_web_http_client_secure_connect"></a><span data-ttu-id="c8c9b-1250">nx_web_http_client_secure_connect</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1250">nx_web_http_client_secure_connect</span></span>

<span data-ttu-id="c8c9b-1251">Aprire una sessione TLS in un server HTTPS per le richieste personalizzate</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1251">Open a TLS session to an HTTPS server for custom requests</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1252">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1252">Prototype</span></span>

```C
UINT nx_web_http_client_secure_connect(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1253">Description</span></span>

<span data-ttu-id="c8c9b-1254">Questo metodo è per HTTPS **protetto da TLS** .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1254">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8c9b-1255">Questo servizio apre una sessione TLS protetta in un server HTTPS, ma non invia alcuna richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1255">This service opens a secured TLS session to an HTTPS server but does not send any requests.</span></span> <span data-ttu-id="c8c9b-1256">Le richieste vengono create con n *x_web_http_client_request_initialize ()* e inviate utilizzando *nx_web_http_client_request_send ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1256">Requests are created with n *x_web_http_client_request_initialize()* and sent using *nx_web_http_client_request_send()*.</span></span> <span data-ttu-id="c8c9b-1257">È possibile aggiungere intestazioni HTTP personalizzate alla richiesta utilizzando *nx_web_http_client_request_header_add ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1257">Custom HTTP headers may be added to the request using *nx_web_http_client_request_header_add()*.</span></span>

<span data-ttu-id="c8c9b-1258">L'uso di questo servizio consente a un'applicazione di aggiungere un numero qualsiasi di intestazioni personalizzate alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1258">Use of this service enables an application to add any number of custom headers to the request.</span></span> <span data-ttu-id="c8c9b-1259">**Questo consente richieste HTTP personalizzate destinate ad applicazioni specifiche.**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1259">**This allows for customized HTTP requests intended for specific applications.**</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-1260">I \* metodi di _start nx_web_http_client_ sono forniti per praticità.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1260">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8c9b-1261">Queste funzioni usano tutte questa routine internamente (insieme a *nx_web_http_client_request_initialize ())* per creare e inviare richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1261">These functions all use this routine internally (along with *nx_web_http_client_request_initialize())* to create and send HTTP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1262">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1262">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1263">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1263">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1264">**server_ip** Indirizzo IP del server HTTPS remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1264">**server_ip** IP address of remote HTTPS server.</span></span>
- <span data-ttu-id="c8c9b-1265">**SERVER_PORT** Porta sul server HTTPS remoto, ad esempio 443 per HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1265">**server_port** Port on remote HTTPS server (e.g. 443 for HTTPS).</span></span>
- <span data-ttu-id="c8c9b-1266">**tls_setup** Callback utilizzato per configurare la configurazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1266">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8c9b-1267">L'applicazione definisce questo callback per inizializzare la crittografia TLS e le credenziali (ad esempio certificati).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1267">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8c9b-1268">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della richiesta di avvio del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1268">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8c9b-1269">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1269">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1270">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1270">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8c9b-1271">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1271">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1272">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1272">Return Values</span></span>

- <span data-ttu-id="c8c9b-1273">**NX_SUCCESS** (0x00) connessione riuscita della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1273">**NX_SUCCESS** (0x00) Successful connection of TLS session.</span></span>
- <span data-ttu-id="c8c9b-1274">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1274">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1275">NX_WEB_HTTP_NOT_READY (0x3000A) è già in corso un'altra richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1275">NX_WEB_HTTP_NOT_READY (0x3000A) Another request is already in progress.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1276">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1276">Allowed From</span></span>

<span data-ttu-id="c8c9b-1277">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1277">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1278">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1278">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

nx_web_http_client_secure_connect(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get* until the entire response is retrieved. *./

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);
    /* Process response packets… */
}
```

## <a name="http-and-https-server-api"></a><span data-ttu-id="c8c9b-1279">API server HTTP e HTTPS</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1279">HTTP and HTTPS Server API</span></span>

## <a name="nx_web_http_server_cache_info_callback_set"></a><span data-ttu-id="c8c9b-1280">nx_web_http_server_cache_info_callback_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1280">nx_web_http_server_cache_info_callback_set</span></span>

<span data-ttu-id="c8c9b-1281">Impostare il callback per il recupero della validità e della data massima dell'URL</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1281">Set the callback to retrieve URL max age and date</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1282">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1282">Prototype</span></span>

```C
UINT nx_web_http_server_cache_info_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT (*cache_info_get)(CHAR *resource,
    UINT *max_age,
    NX_WEB_HTTP_SERVER_DATE *date));
```

### <a name="description"></a><span data-ttu-id="c8c9b-1283">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1283">Description</span></span>

<span data-ttu-id="c8c9b-1284">Questo servizio imposta il servizio di callback richiamato per ottenere la data di validità massima e dell'Ultima modifica della risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1284">This service sets the callback service invoked to obtain the maximum age and last modified date of the specified resource.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1285">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1285">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1286">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1286">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1287">**cache_info_get** Puntatore al callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1287">**cache_info_get** Pointer to the callback</span></span>
- <span data-ttu-id="c8c9b-1288">**max_age** Puntatore alla durata massima di una risorsa</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1288">**max_age** Pointer to maximum age of a resource</span></span>
- <span data-ttu-id="c8c9b-1289">**dati** di Puntatore alla data dell'Ultima modifica restituita.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1289">**data** Pointer to last modified date returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1290">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1290">Return Values</span></span>

- <span data-ttu-id="c8c9b-1291">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1291">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8c9b-1292">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1292">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1293">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1293">Allowed From</span></span>

<span data-ttu-id="c8c9b-1294">Inizializzazione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1294">Initialization</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1295">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1295">Example</span></span>

```C
NX_WEB_HTTP_SERVER my_server;

UINT cache_info_get(CHAR *resource, UINT *max_age,
    NX_WEB_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_web_http_server_create and before the HTTP
    server is set by nx_web_http_server_start(), set the cache info callback: */
status = nx_web_http_server_cache_info_callback_set(&my_server, cache_info_get);

/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_web_http_server_callback_data_send"></a><span data-ttu-id="c8c9b-1296">nx_web_http_server_callback_data_send</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1296">nx_web_http_server_callback_data_send</span></span>

<span data-ttu-id="c8c9b-1297">Inviare dati da una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1297">Send data from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1298">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1298">Prototype</span></span>

```C
UINT nx_web_http_server_callback_data_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID *data_ptr, ULONG data_length);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1299">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1299">Description</span></span>

<span data-ttu-id="c8c9b-1300">Questo servizio invia i dati nel pacchetto fornito dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1300">This service sends the data in the supplied packet from the application’s callback routine.</span></span> <span data-ttu-id="c8c9b-1301">Questa operazione viene in genere usata per inviare i dati dinamici associati alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1301">This is typically used to send dynamic data associated with GET/POST requests.</span></span> <span data-ttu-id="c8c9b-1302">Si noti che se si utilizza questa funzione, la routine di callback è responsabile dell'invio dell'intera risposta nel formato corretto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1302">Note that if this function is used, the callback routine is responsible for sending the entire response in the proper format.</span></span> <span data-ttu-id="c8c9b-1303">Inoltre, la routine di callback deve restituire lo stato di NX_WEB_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1303">In addition, the callback routine must return the status of NX_WEB_HTTP_CALLBACK_COMPLETED.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1304">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1304">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1305">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1305">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1306">**DATA_PTR** Puntatore ai dati da inviare.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1306">**data_ptr** Pointer to the data to send.</span></span>
- <span data-ttu-id="c8c9b-1307">**Data_length** Numero di byte da inviare.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1307">**data_length** Number of bytes to send.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1308">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1308">Return Values</span></span>

- <span data-ttu-id="c8c9b-1309">**NX_SUCCESS** (0x00) ha inviato correttamente i dati del server</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1309">**NX_SUCCESS** (0x00) Successfully sent Server data</span></span>
- <span data-ttu-id="c8c9b-1310">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1310">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1311">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1311">Allowed From</span></span>

<span data-ttu-id="c8c9b-1312">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1312">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1313">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1313">Example</span></span>

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* Found it, override the GET processing by sending the resource
            contents directly. */
        nx_web_http_server_callback_data_send(server_ptr,
            "HTTP/1.0 200 \r\nContent-Length:" "103\r\nContent-Type: text/html\r\n\r\n",
            63);

        nx_web_http_server_callback_data_send(server_ptr, "<HTML>\r\n<HEAD><TITLE>NetX"
            "HTTP Test </TITLE></HEAD>\r\n"
            :<BODY>\r\n<H1>NetX Test Page"
            "</H1>\r\n</BODY>\r\n</HTML>\r\n", 103);

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_callback_generate_response_header"></a><span data-ttu-id="c8c9b-1314">nx_web_http_server_callback_generate_response_header</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1314">nx_web_http_server_callback_generate_response_header</span></span>

<span data-ttu-id="c8c9b-1315">Creare un'intestazione della risposta in una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1315">Create a response header in a callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1316">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1316">Prototype</span></span>

```C
UINT nx_web_http_server_callback_generate_response_header(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    CHAR *status_code, UINT content_length,
    CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1317">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1317">Description</span></span>

<span data-ttu-id="c8c9b-1318">Questo servizio viene usato nella routine di callback del server HTTP (S) (definita dall'applicazione) per generare un'intestazione di risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1318">This service is used in the HTTP(S) server callback routine (defined by the application) to generate an HTTP response header.</span></span> <span data-ttu-id="c8c9b-1319">La routine di callback del server viene richiamata quando il server HTTP risponde alle richieste GET, PUT e DELETE del client che richiedono una risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1319">The server callback routine is invoked when the HTTP server responds to Client GET, PUT and DELETE requests which require an HTTP response.</span></span> <span data-ttu-id="c8c9b-1320">Questa funzione accetta le informazioni di risposta dall'applicazione e genera l'intestazione di risposta appropriata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1320">This function takes the response information from the application and generates the appropriate response header.</span></span> <span data-ttu-id="c8c9b-1321">Per ulteriori informazioni sulla routine di callback delle richieste server, vedere il nx_web_http_server_create di servizio *()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1321">See the service *nx_web_http_server_create()* for more information on the server request callback routine.</span></span>

<span data-ttu-id="c8c9b-1322">Questa API è deprecata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1322">This API is deprecated.</span></span> <span data-ttu-id="c8c9b-1323">Gli sviluppatori sono invitati a utilizzare *nx_web_http_server_callback_generate_response_header_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1323">Developers are encouraged to use *nx_web_http_server_callback_generate_response_header_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1324">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1324">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1325">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1325">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1326">**packet_pptr** Puntatore a un puntatore di pacchetto allocato per il messaggio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1326">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
- <span data-ttu-id="c8c9b-1327">**status_code** Indicare lo stato della risorsa.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1327">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="c8c9b-1328">Esempi:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1328">Examples:</span></span>
  - <span data-ttu-id="c8c9b-1329">**NX_WEB_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1329">**NX_WEB_HTTP_STATUS_OK**</span></span>
  - <span data-ttu-id="c8c9b-1330">**NX_WEB_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1330">**NX_WEB_HTTP_STATUS_MODIFIED**</span></span>
  - <span data-ttu-id="c8c9b-1331">**NX_WEB_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1331">**NX_WEB_HTTP_STATUS_INTERNAL_ERROR**</span></span>
- <span data-ttu-id="c8c9b-1332">**CONTENT_LENGTH** Dimensioni del contenuto in byte</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1332">**content_length** Size of content in bytes</span></span>
- <span data-ttu-id="c8c9b-1333">**content_type** Tipo di HTTP, ad esempio "text/plain"</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1333">**content_type** Type of HTTP e.g. "text/plain"</span></span>
- <span data-ttu-id="c8c9b-1334">**additional_header** Puntatore a testo intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1334">**additional_header** Pointer to additional header text</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1335">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1335">Return Values</span></span>

- <span data-ttu-id="c8c9b-1336">**NX_SUCCESS** (0x00) ha creato l'intestazione HTML</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1336">**NX_SUCCESS** (0x00) Successfully created HTML header</span></span>
- <span data-ttu-id="c8c9b-1337">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1337">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1338">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1338">Allowed From</span></span>

<span data-ttu-id="c8c9b-1339">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1339">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1340">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1340">Example</span></span>

```C
CHAR demotestbuffer[] = "<html>> r\n\r\n<head>> r\n\r\n<title>Main \
    Window</title>> r\n</head>> r\n\r\n<body>Test message\r\n \ </body>> r\n</html>> r\n";

/* my_request_notify* is the application request notify callback registered
    with the HTTP server in *nx_web_http_server_create*,
    creates a response to the received Client request. */

UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET *resp_packet_ptr;
    ULONG string_length;
    CHAR temp_string[30];
    ULONG length = 0;
    length = strlen(&demotestbuffer[0]);

    /* Derive the client request type from the client request. */
    nx_web_http_server_type_extract(server_ptr,
        server_ptr -> nx_web_http_server_request_resource,
        temp_string, sizeof(temp_string), &string_length);

    /* Null terminate the string. */
    temp_string[string_length] = 0;

    /* Now build a response header with server status is OK and no additional header info. */
    status = nx_web_http_server_callback_generate_response_header(http_server_ptr,
        &resp_packet_ptr, NX_WEB_HTTP_STATUS_OK,
        length, temp_string, NX_NULL);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
    status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
        strlen(&demotestbuffer[0]), server_ptr >>
        nx_web_http_server_packet_pool_ptr, NX_WAIT_FOREVER);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
    status = nx_web_http_server_callback_packet_send(
        &(server_ptr -> nx_web_http_server_socket),
        resp_packet_ptr);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Let HTTP server know the response has been sent. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);
}
```

## <a name="nx_web_http_server_callback_generate_response_header_extended"></a><span data-ttu-id="c8c9b-1341">nx_web_http_server_callback_generate_response_header_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1341">nx_web_http_server_callback_generate_response_header_extended</span></span>

<span data-ttu-id="c8c9b-1342">Creare un'intestazione della risposta in una funzione di callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1342">Create a response header in a callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1343">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1343">Prototype</span></span>

```C
UINT nx_web_http_server_callback_generate_response_header_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    CHAR *status_code, UINT status_code_length,
    UINT content_length, CHAR *content_type,
    UINT content_type_length,
    CHAR* additional_header,
    UINT additional_header_length);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1344">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1344">Description</span></span>

<span data-ttu-id="c8c9b-1345">Questo servizio viene usato nella routine di callback del server HTTP (S) (definita dall'applicazione) per generare un'intestazione di risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1345">This service is used in the HTTP(S) server callback routine (defined by the application) to generate an HTTP response header.</span></span> <span data-ttu-id="c8c9b-1346">La routine di callback del server viene richiamata quando il server HTTP risponde alle richieste GET, PUT e DELETE del client che richiedono una risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1346">The server callback routine is invoked when the HTTP server responds to Client GET, PUT and DELETE requests which require an HTTP response.</span></span> <span data-ttu-id="c8c9b-1347">Questa funzione accetta le informazioni di risposta dall'applicazione e genera l'intestazione di risposta appropriata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1347">This function takes the response information from the application and generates the appropriate response header.</span></span> <span data-ttu-id="c8c9b-1348">Per ulteriori informazioni sulla routine di callback delle richieste server, vedere il nx_web_http_server_create di servizio *()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1348">See the service *nx_web_http_server_create()* for more information on the server request callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1349">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1349">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1350">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1350">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1351">**packet_pptr** Puntatore a un puntatore di pacchetto allocato per il messaggio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1351">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
- <span data-ttu-id="c8c9b-1352">**status_code** Indicare lo stato della risorsa.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1352">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="c8c9b-1353">Esempi:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1353">Examples:</span></span>
  - <span data-ttu-id="c8c9b-1354">**NX_WEB_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1354">**NX_WEB_HTTP_STATUS_OK**</span></span>
  - <span data-ttu-id="c8c9b-1355">**NX_WEB_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1355">**NX_WEB_HTTP_STATUS_MODIFIED**</span></span>
  - <span data-ttu-id="c8c9b-1356">**NX_WEB_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1356">**NX_WEB_HTTP_STATUS_INTERNAL_ERROR**</span></span>
- <span data-ttu-id="c8c9b-1357">**status_code_length** Lunghezza stringa del codice di stato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1357">**status_code_length** String length of status code</span></span>
- <span data-ttu-id="c8c9b-1358">**CONTENT_LENGTH** Dimensioni del contenuto in byte</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1358">**content_length** Size of content in bytes</span></span>
- <span data-ttu-id="c8c9b-1359">**content_type** Tipo di HTTP, ad esempio "text/plain"</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1359">**content_type** Type of HTTP e.g. "text/plain"</span></span>
- <span data-ttu-id="c8c9b-1360">**content_type_length** Lunghezza stringa del tipo di contenuto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1360">**content_type_length** String length of content type</span></span>
- <span data-ttu-id="c8c9b-1361">**additional_header** Puntatore a testo intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1361">**additional_header** Pointer to additional header text</span></span>
- <span data-ttu-id="c8c9b-1362">**additional_header_length** Lunghezza del testo dell'intestazione aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1362">**additional_header_length** Length of additional header text</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1363">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1363">Return Values</span></span>

- <span data-ttu-id="c8c9b-1364">**NX_SUCCESS** (0x00) ha creato l'intestazione HTML</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1364">**NX_SUCCESS** (0x00) Successfully created HTML header</span></span>
- <span data-ttu-id="c8c9b-1365">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1365">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1366">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1366">Allowed From</span></span>

<span data-ttu-id="c8c9b-1367">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1367">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1368">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1368">Example</span></span>

```C
CHAR demotestbuffer[] = "<html>> r\n\r\n<head>> r\n\r\n<title>Main \
    Window</title>> r\n</head>> r\n\r\n<body>Test message\r\n \ </body>> r\n</html>> r\n";

/* my_request_notify* is the application request notify callback
    registered with the HTTP server in *nx_web_http_server_create*,
    creates a response to the received Client request. */

UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET *resp_packet_ptr;
    ULONG string_length;
    CHAR temp_string[30];
    ULONG length = 0;
    length = strlen(&demotestbuffer[0]);

    /* Derive the client request type from the client request. */
    nx_web_http_server_type_extract(server_ptr,
        server_ptr -> nx_web_http_server_request_resource,
        temp_string, sizeof(temp_string), &string_length);

    /* Null terminate the string. */
    temp_string[string_length] = 0;

    /* Now build a response header with server status is OK and no additional header info. */
    status = nx_web_http_server_callback_generate_response_header_extended(http_server_ptr,
        &resp_packet_ptr, NX_WEB_HTTP_STATUS_OK,
        sizeof(NX_WEB_HTTP_STATUS_OK) – 1,
        length, temp_string, string_length NX_NULL, 0);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
    status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
        strlen(&demotestbuffer[0]), server_ptr >>
        nx_web_http_server_packet_pool_ptr, NX_WAIT_FOREVER);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
    status = nx_web_http_server_callback_packet_send(
        &(server_ptr -> nx_web_http_server_socket),
        resp_packet_ptr);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Let HTTP server know the response has been sent. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);

}
```

## <a name="nx_web_http_server_callback_packet_send"></a><span data-ttu-id="c8c9b-1369">nx_web_http_server_callback_packet_send</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1369">nx_web_http_server_callback_packet_send</span></span>

<span data-ttu-id="c8c9b-1370">Inviare un pacchetto HTTP dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1370">Send an HTTP packet from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1371">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1371">Prototype</span></span>

```C
UINT nx_web_http_server_callback_packet_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1372">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1372">Description</span></span>

<span data-ttu-id="c8c9b-1373">Questo servizio invia una risposta server HTTP completa da un callback HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1373">This service sends a complete HTTP server response from an HTTP callback.</span></span> <span data-ttu-id="c8c9b-1374">Il pacchetto viene inviato dal server HTTP al _TIMEOUT_SEND NX_WEB_HTTP_SERVER.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1374">HTTP server will send the packet with the NX_WEB_HTTP_SERVER _TIMEOUT_SEND.</span></span> <span data-ttu-id="c8c9b-1375">L'intestazione e i dati HTTP devono essere aggiunti al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1375">The HTTP header and data must be appended to the packet.</span></span> <span data-ttu-id="c8c9b-1376">Se lo stato restituito indica un errore, l'applicazione HTTP deve rilasciare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1376">If the return status indicates an error, the HTTP application must release the packet.</span></span>

<span data-ttu-id="c8c9b-1377">Il callback deve restituire NX_WEB_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1377">The callback should return NX_WEB_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="c8c9b-1378">Per un esempio più dettagliato, vedere *nx_web_http_server_callback_generate_response_header ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1378">See *nx_web_http_server_callback_generate_response_header()* for a more detailed example.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1379">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1379">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1380">**server_ptr** Puntatore al blocco di controllo server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1380">**server_ptr** Pointer to HTTP Server control block</span></span>
- <span data-ttu-id="c8c9b-1381">**packet_ptr** Puntatore al pacchetto da inviare</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1381">**packet_ptr** Pointer to the packet to send</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1382">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1382">Return Values</span></span>

- <span data-ttu-id="c8c9b-1383">**NX_SUCCESS** (0x00) ha inviato il pacchetto del server http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1383">**NX_SUCCESS** (0x00) Successfully sent HTTP Server packet</span></span>
- <span data-ttu-id="c8c9b-1384">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1384">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1385">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1385">Allowed From</span></span>

<span data-ttu-id="c8c9b-1386">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1386">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1387">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1387">Example</span></span>

```C
/* The packet is appended with HTTP header and data
    and is ready to send to the Client directly. */
status = nx_web_http_server_callback_packet_send(server_ptr, packet_ptr);

if (status != NX_SUCCESS)
{
    nx_packet_release(packet_ptr);
}

return(NX_WEB_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_web_http_server_callback_response_send"></a><span data-ttu-id="c8c9b-1388">nx_web_http_server_callback_response_send</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1388">nx_web_http_server_callback_response_send</span></span>

<span data-ttu-id="c8c9b-1389">Invia risposta dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1389">Send response from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1390">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1390">Prototype</span></span>

```C
UINT nx_web_http_server_callback_response_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    CHAR *header,
    CHAR *information,
    CHAR additional_info);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1391">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1391">Description</span></span>

<span data-ttu-id="c8c9b-1392">Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1392">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="c8c9b-1393">Questa operazione viene in genere usata per inviare risposte personalizzate associate alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1393">This is typically used to send custom responses associated with GET/POST requests.</span></span> <span data-ttu-id="c8c9b-1394">Si noti che se si utilizza questa funzione, la routine di callback deve restituire lo stato di NX_WEB_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1394">Note that if this function is used, the callback routine must return the status of NX_WEB_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="c8c9b-1395">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1395">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-1396">Gli sviluppatori sono invitati a utilizzare *nx_web_http_server_callback_response_send_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1396">Developers are encouraged to use *nx_web_http_server_callback_response_send_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1397">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1397">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1398">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1398">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1399">**intestazione** di Puntatore alla stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1399">**header** Pointer to the response header string.</span></span>
- <span data-ttu-id="c8c9b-1400">**informazioni** su Puntatore alla stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1400">**information** Pointer to the information string.</span></span>
- <span data-ttu-id="c8c9b-1401">**additional_info** Puntatore alla stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1401">**additional_info** Pointer to the additional information string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1402">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1402">Return Values</span></span>

- <span data-ttu-id="c8c9b-1403">**NX_SUCCESS** (0x00) ha inviato correttamente la risposta al server http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1403">**NX_SUCCESS** (0x00) Successfully sent HTTP Server response</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1404">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1404">Allowed From</span></span>

<span data-ttu-id="c8c9b-1405">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1405">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1406">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1406">Example</span></span>

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
            a resource not found response. */
        nx_web_http_server_callback_response_send(server_ptr,
            "HTTP/1.0 404 ",
            "NetX HTTP Server unable to find file: ",
            resource);

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_callback_response_send_extended"></a><span data-ttu-id="c8c9b-1407">nx_web_http_server_callback_response_send_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1407">nx_web_http_server_callback_response_send_extended</span></span>

<span data-ttu-id="c8c9b-1408">Invia risposta dalla funzione di callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1408">Send response from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1409">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1409">Prototype</span></span>

```C
UINT nx_web_http_server_callback_response_send_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    CHAR *header, UINT header_length,
    CHAR *information,
    UINT information_length,
    CHAR additional_info,
    UINT additional_info_length);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1410">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1410">Description</span></span>

<span data-ttu-id="c8c9b-1411">Questo servizio invia le informazioni di risposta fornite dalla routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1411">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="c8c9b-1412">Questa operazione viene in genere usata per inviare risposte personalizzate associate alle richieste GET/POST.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1412">This is typically used to send custom responses associated with GET/POST requests.</span></span> <span data-ttu-id="c8c9b-1413">Si noti che se si utilizza questa funzione, la routine di callback deve restituire lo stato di NX_WEB_HTTP_CALLBACK_COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1413">Note that if this function is used, the callback routine must return the status of NX_WEB_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="c8c9b-1414">Le stringhe di intestazione, informazioni e additional_info devono essere con terminazione NULL e la lunghezza di ogni stringa corrisponde alla lunghezza specificata nell'elenco di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1414">The strings of header, information and additional_info must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8c9b-1415">Questo servizio sostituisce *nx_web_http_server_callback_response_send*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1415">This service replaces *nx_web_http_server_callback_response_send*().</span></span> <span data-ttu-id="c8c9b-1416">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1416">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1417">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1417">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1418">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1418">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1419">**intestazione** di Puntatore alla stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1419">**header** Pointer to the response header string.</span></span>
- <span data-ttu-id="c8c9b-1420">**HEADER_LENGTH** Lunghezza della stringa di intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1420">**header_length** Length of the response header string.</span></span>
- <span data-ttu-id="c8c9b-1421">**informazioni** su Puntatore alla stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1421">**information** Pointer to the information string.</span></span>
- <span data-ttu-id="c8c9b-1422">**Information_length** Lunghezza della stringa di informazioni.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1422">**Information_length** Length of the information string.</span></span>
- <span data-ttu-id="c8c9b-1423">**additional_info** Puntatore alla stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1423">**additional_info** Pointer to the additional information string.</span></span>
- <span data-ttu-id="c8c9b-1424">**additional_info_length** Lunghezza della stringa di informazioni aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1424">**additional_info_length** Length of the additional information string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1425">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1425">Return Values</span></span>

- <span data-ttu-id="c8c9b-1426">**NX_SUCCESS** (0x00) ha inviato correttamente la risposta al server http</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1426">**NX_SUCCESS** (0x00) Successfully sent HTTP Server response</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1427">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1427">Allowed From</span></span>

<span data-ttu-id="c8c9b-1428">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1428">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1429">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1429">Example</span></span>

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
            a resource not found response. */
        nx_web_http_server_callback_response_send_extended(server_ptr,
            "HTTP/1.0 404 ",
            sizeof("HTTP/1.0 404 ") – 1,
            "NetX HTTP Server unable to find file: ",
            sizeof("NetX HTTP Server unable to find file: ") – 1,
            resource, strlen(resource));

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_content_get"></a><span data-ttu-id="c8c9b-1430">nx_web_http_server_content_get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1430">nx_web_http_server_content_get</span></span>

<span data-ttu-id="c8c9b-1431">Ottenere contenuto dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1431">Get content from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1432">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1432">Prototype</span></span>

```C
UINT nx_web_http_server_content_get(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr,
    ULONG byte_offset,
    CHAR *destination_ptr,
    UINT destination_size,
    UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1433">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1433">Description</span></span>

<span data-ttu-id="c8c9b-1434">Questo servizio tenta di recuperare la quantità specificata di contenuto dalla richiesta client HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1434">This service attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="c8c9b-1435">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1435">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1436">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1436">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1437">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1437">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1438">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1438">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="c8c9b-1439">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1439">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="c8c9b-1440">**byte_offset** Numero di byte da sfalsare nell'area del contenuto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1440">**byte_offset** Number of bytes to offset into the content area.</span></span>
- <span data-ttu-id="c8c9b-1441">**destination_ptr** Puntatore all'area di destinazione per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1441">**destination_ptr** Pointer to the destination area for the content.</span></span>
- <span data-ttu-id="c8c9b-1442">**destination_size** Numero massimo di byte disponibili nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1442">**destination_size** Maximum number of bytes available in the destination area.</span></span>
- <span data-ttu-id="c8c9b-1443">**actual_size** Puntatore alla variabile di destinazione che verrà impostata sulle dimensioni effettive del contenuto copiato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1443">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1444">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1444">Return Values</span></span>

- <span data-ttu-id="c8c9b-1445">**NX_SUCCESS** (0x00) il contenuto del server http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1445">**NX_SUCCESS** (0x00) Successful HTTP Server content Get</span></span>
- <span data-ttu-id="c8c9b-1446">Errore interno del server HTTP **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1446">**NX_WEB_HTTP_ERROR** (0x30000) HTTP Server internal error</span></span>
- <span data-ttu-id="c8c9b-1447">**NX_WEB_HTTP_DATA_END** (0X30007) fine del contenuto della richiesta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1447">**NX_WEB_HTTP_DATA_END** (0x30007) End of request content</span></span>
- <span data-ttu-id="c8c9b-1448">TIMEOUT del server HTTP **NX_WEB_HTTP_TIMEOUT** (0x30001) per il recupero del pacchetto di contenuto successivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1448">**NX_WEB_HTTP_TIMEOUT** (0x30001) HTTP Server timeout in getting next packet of content</span></span>
- <span data-ttu-id="c8c9b-1449">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1449">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1450">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1450">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1451">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1451">Allowed From</span></span>

<span data-ttu-id="c8c9b-1452">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1452">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1453">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1453">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, retrieve up to 100 bytes of content starting at offset
    0. */
status = nx_web_http_server_content_get(&my_server, packet_ptr,
    0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, "my_buffer" contains "actual_size" bytes of
    request content. */
```

## <a name="nx_web_http_server_content_get_extended"></a><span data-ttu-id="c8c9b-1454">nx_web_http_server_content_get_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1454">nx_web_http_server_content_get_extended</span></span>

<span data-ttu-id="c8c9b-1455">Ottieni contenuto dalla richiesta/supporta la lunghezza del contenuto di lunghezza zero</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1455">Get content from the request/supports zero length Content Length</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1456">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1456">Prototype</span></span>

```C
UINT nx_web_http_server_content_get_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr,
    ULONG byte_offset,
    CHAR *destination_ptr,
    UINT destination_size,
    UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1457">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1457">Description</span></span>

<span data-ttu-id="c8c9b-1458">Questo servizio è quasi identico a *nx_web_http_server_content_get ()*; tenta di recuperare la quantità specificata di contenuto dalla richiesta del client HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1458">This service is almost identical to *nx_web_http_server_content_get()*; it attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="c8c9b-1459">Tuttavia, gestisce le richieste con lunghezza del contenuto pari a zero (' Empty request ') come richiesta valida.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1459">However it handles requests with Content Length of zero value (‘empty request’) as a valid request.</span></span> <span data-ttu-id="c8c9b-1460">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1460">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

<span data-ttu-id="c8c9b-1461">Questo servizio sostituisce *nx_web_http_server_content_get*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1461">This service replaces *nx_web_http_server_content_get*().</span></span> <span data-ttu-id="c8c9b-1462">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1462">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1463">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1463">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1464">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1464">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1465">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1465">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="c8c9b-1466">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1466">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="c8c9b-1467">**byte_offset** Numero di byte da sfalsare nell'area del contenuto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1467">**byte_offset** Number of bytes to offset into the content area.</span></span>
- <span data-ttu-id="c8c9b-1468">**destination_ptr** Puntatore all'area di destinazione per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1468">**destination_ptr** Pointer to the destination area for the content.</span></span>
- <span data-ttu-id="c8c9b-1469">**destination_size** Numero massimo di byte disponibili nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1469">**destination_size** Maximum number of bytes available in the destination area.</span></span>
- <span data-ttu-id="c8c9b-1470">**actual_size** Puntatore alla variabile di destinazione che verrà impostata sulle dimensioni effettive del contenuto copiato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1470">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1471">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1471">Return Values</span></span>

- <span data-ttu-id="c8c9b-1472">**NX_SUCCESS** (0x00) contenuto http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1472">**NX_SUCCESS** (0x00) Successful HTTP content get</span></span>
- <span data-ttu-id="c8c9b-1473">Errore interno del server HTTP **NX_WEB_HTTP_ERROR** (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1473">**NX_WEB_HTTP_ERROR** (0x30000) HTTP Server internal error</span></span>
- <span data-ttu-id="c8c9b-1474">**NX_WEB_HTTP_DATA_END** (0X30007) fine del contenuto della richiesta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1474">**NX_WEB_HTTP_DATA_END** (0x30007) End of request content</span></span>
- <span data-ttu-id="c8c9b-1475">TIMEOUT del server HTTP **NX_WEB_HTTP_TIMEOUT** (0x30001) nel recupero del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1475">**NX_WEB_HTTP_TIMEOUT** (0x30001) HTTP Server timeout in getting next packet</span></span>
- <span data-ttu-id="c8c9b-1476">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1476">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1477">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1477">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1478">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1478">Allowed From</span></span>

<span data-ttu-id="c8c9b-1479">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1479">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1480">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1480">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, retrieve up to 100 bytes of content starting at offset
    0. */
status = nx_web_http_server_content_get_extended(&my_server, packet_ptr,
    0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, "my_buffer" contains "actual_size" bytes of
    request content. */
```

## <a name="nx_web_http_server_content_length_get"></a><span data-ttu-id="c8c9b-1481">nx_web_http_server_content_length_get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1481">nx_web_http_server_content_length_get</span></span>

<span data-ttu-id="c8c9b-1482">Ottenere la lunghezza del contenuto nella richiesta/supporta la lunghezza del contenuto pari a zero valore</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1482">Get length of content in the request/supports Content Length of zero value</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1483">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1483">Prototype</span></span>

```C
UINT nx_web_http_server_content_length_get(
    NX_PACKET *packet_ptr,
    UINT *content_length);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1484">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1484">Description</span></span>

<span data-ttu-id="c8c9b-1485">Questo servizio tenta di recuperare la lunghezza del contenuto HTTP nel pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1485">This service attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="c8c9b-1486">Il valore restituito indica lo stato di completamento corretto e il valore di lunghezza effettivo viene restituito nel puntatore di input content_length.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1486">The return value indicates successful completion status and the actual length value is returned in the input pointer content_length.</span></span> <span data-ttu-id="c8c9b-1487">Se non è presente alcun contenuto HTTP/lunghezza contenuto = 0, questa routine restituisce ancora uno stato di completamento corretto e il puntatore di input content_length punta a una lunghezza valida (zero).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1487">If there is no HTTP content/Content Length = 0, this routine still returns a successful completion status and the content_length input pointer points to a valid length (zero).</span></span> <span data-ttu-id="c8c9b-1488">Deve essere chiamato dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1488">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1489">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1489">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1490">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1490">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="c8c9b-1491">Si noti che questo pacchetto non deve essere rilasciato dal callback della richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1491">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="c8c9b-1492">**CONTENT_LENGTH** Puntatore al valore recuperato dal campo lunghezza contenuto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1492">**content_length** Pointer to value retrieved from Content Length field</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1493">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1493">Return Values</span></span>

- <span data-ttu-id="c8c9b-1494">**NX_SUCCESS** (0x00) lunghezza contenuto server http riuscita Get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1494">**NX_SUCCESS** (0x00) Successful HTTP Server Content Length Get</span></span>
- <span data-ttu-id="c8c9b-1495">Formato dell'intestazione HTTP **NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) non corretto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1495">**NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) Improper HTTP header format</span></span>
- <span data-ttu-id="c8c9b-1496">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1496">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1497">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1497">Allowed From</span></span>

<span data-ttu-id="c8c9b-1498">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1498">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1499">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1499">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, get the content length of the HTTP Client request. */

ULONG content_length;
status = nx_web_http_server_content_length_get(packet_ptr, &content_length);

/* If the "status" variable indicates successful completion, the "length"
    Variable contains the length of the HTTP Client request content area. */
```

## <a name="nx_web_http_server_create"></a><span data-ttu-id="c8c9b-1500">nx_web_http_server_create</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1500">nx_web_http_server_create</span></span>

<span data-ttu-id="c8c9b-1501">Creare un'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1501">Create an HTTP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1502">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1502">Prototype</span></span>

```C
UINT nx_web_http_server_create(NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *http_server_name, NX_IP *ip_ptr, UINT server_port,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*authentication_check)(NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type, CHAR *resource, CHAR **name,
        CHAR **password, CHAR **realm),
    UINT (*request_notify)(NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

### <a name="description"></a><span data-ttu-id="c8c9b-1503">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1503">Description</span></span>

<span data-ttu-id="c8c9b-1504">Questo servizio crea un'istanza del server HTTP, che viene eseguita nel contesto del proprio thread ThreadX.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1504">This service creates an HTTP Server instance, which runs in the context of its own ThreadX thread.</span></span> <span data-ttu-id="c8c9b-1505">Le routine di callback dell'applicazione *authentication_check* e *request_notify* facoltative forniscono al software dell'applicazione il controllo sulle operazioni di base del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1505">The optional *authentication_check* and *request_notify* application callback routines give the application software control over the basic operations of the HTTP Server.</span></span>

<span data-ttu-id="c8c9b-1506">Questo servizio viene utilizzato per creare sia server HTTP in testo non crittografato che server HTTPS protetti da TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1506">This service is used to create both plaintext HTTP servers and TLS-secured HTTPS servers.</span></span> <span data-ttu-id="c8c9b-1507">Per abilitare HTTPS usando TLS, vedere il nx_web_http_server_secure_configure di servizio *()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1507">To enable HTTPS using TLS, see the service *nx_web_http_server_secure_configure()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1508">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1508">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1509">**http_server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1509">**http_server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1510">**http_server_name** Puntatore al nome del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1510">**http_server_name** Pointer to HTTP Server’s name.</span></span>
- <span data-ttu-id="c8c9b-1511">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1511">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="c8c9b-1512">**SERVER_PORT** Porta TCP in ascolto per l'istanza del server.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1512">**server_port** TCP listening port for server instance.</span></span>
- <span data-ttu-id="c8c9b-1513">**media_ptr** Puntatore a un'istanza del supporto FileX creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1513">**media_ptr** Pointer to previously created FileX media instance.</span></span>
- <span data-ttu-id="c8c9b-1514">**stack_ptr** Puntatore all'area dello stack di thread del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1514">**stack_ptr** Pointer to HTTP Server thread stack area.</span></span>
- <span data-ttu-id="c8c9b-1515">**stack_size** Puntatore alla dimensione dello stack del thread del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1515">**stack_size** Pointer to HTTP Server thread stack size.</span></span>
- <span data-ttu-id="c8c9b-1516">**authentication_check** Puntatore a funzione per la routine di controllo dell'autenticazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1516">**authentication_check** Function pointer to application’s authentication checking routine.</span></span> <span data-ttu-id="c8c9b-1517">Se specificato, questa routine viene chiamata per ogni richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1517">If specified, this routine is called for each HTTP Client request.</span></span> <span data-ttu-id="c8c9b-1518">Se questo parametro è NULL, non verrà eseguita alcuna autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1518">If this parameter is NULL, no authentication will be performed.</span></span> <span data-ttu-id="c8c9b-1519">Questo parametro è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1519">This parameter is deprecated.</span></span> <span data-ttu-id="c8c9b-1520">Chiamare invece *nx_web_http_server_authenticate_check_set*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1520">Call *nx_web_http_server_authenticate_check_set*() instead.</span></span>
- <span data-ttu-id="c8c9b-1521">**request_notify** Puntatore della funzione alla routine di notifica della richiesta dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1521">**request_notify** Function pointer to application’s request notify routine.</span></span> <span data-ttu-id="c8c9b-1522">Se specificato, questa routine viene chiamata prima dell'elaborazione del server HTTP della richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1522">If specified, this routine is called prior to the HTTP server processing of the request.</span></span> <span data-ttu-id="c8c9b-1523">Questo consente di reindirizzare il nome della risorsa o i campi all'interno di una risorsa da aggiornare prima di completare la richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1523">This allows the resource name to be redirected or fields within a resource to be updated prior to completing the HTTP Client request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1524">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1524">Return Values</span></span>

- <span data-ttu-id="c8c9b-1525">Creazione del server HTTP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1525">**NX_SUCCESS** (0x00) Successful HTTP Server create.</span></span>
- <span data-ttu-id="c8c9b-1526">NX_PTR_ERROR (0x07) server HTTP, IP, supporti, stack o puntatore al pool di pacchetti non validi.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1526">NX_PTR_ERROR (0x07) Invalid HTTP Server, IP, media, stack, or packet pool pointer.</span></span>
- <span data-ttu-id="c8c9b-1527">Il payload del pacchetto di NX_WEB_HTTP_POOL_ERROR (0x30009) del pool non è sufficiente per contenere la richiesta HTTP completa.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1527">NX_WEB_HTTP_POOL_ERROR (0x30009) Packet payload of pool is not large enough to contain complete HTTP request.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1528">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1528">Allowed From</span></span>

<span data-ttu-id="c8c9b-1529">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1529">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1530">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1530">Example</span></span>

```C
/* Create an HTTP Server instance called "my_server." */
status = nx_web_http_server_create(&my_server, "my server", &ip_0,
    NX_WEB_HTTPS_SERVER_PORT, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_web_http_server_delete"></a><span data-ttu-id="c8c9b-1531">nx_web_http_server_delete</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1531">nx_web_http_server_delete</span></span>

<span data-ttu-id="c8c9b-1532">Eliminare un'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1532">Delete an HTTP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1533">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1533">Prototype</span></span>

```C
UINT nx_web_http_server_delete(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1534">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1534">Description</span></span>

<span data-ttu-id="c8c9b-1535">Questo servizio Elimina un'istanza del server HTTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1535">This service deletes a previously created HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1536">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1536">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1537">**http_server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1537">**http_server_ptr** Pointer to HTTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1538">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1538">Return Values</span></span>

- <span data-ttu-id="c8c9b-1539">Eliminazione del server HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1539">**NX_SUCCESS** (0x00) Successful HTTP Server delete</span></span>
- <span data-ttu-id="c8c9b-1540">NX_PTR_ERROR (0x07) puntatore al server HTTP non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1540">NX_PTR_ERROR (0x07) Invalid HTTP Server pointer</span></span>
- <span data-ttu-id="c8c9b-1541">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1541">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1542">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1542">Allowed From</span></span>

<span data-ttu-id="c8c9b-1543">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1543">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1544">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1544">Example</span></span>

```C
/* Delete the HTTP Server instance called "my_server." */
status = nx_web_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_web_http_server_get_entity_content"></a><span data-ttu-id="c8c9b-1545">nx_web_http_server_get_entity_content</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1545">nx_web_http_server_get_entity_content</span></span>

<span data-ttu-id="c8c9b-1546">Recuperare il percorso e la lunghezza dei dati dell'entità</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1546">Retrieve the location and length of entity data</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1547">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1547">Prototype</span></span>

```C
UINT nx_web_http_server_get_entity_content(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    ULONG *available_offset,
    ULONG *available_length);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1548">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1548">Description</span></span>

<span data-ttu-id="c8c9b-1549">Questo servizio determina la posizione dell'inizio dei dati all'interno dell'entità multiparte corrente nei messaggi client ricevuti e la lunghezza dei dati che non includono la stringa di limite.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1549">This service determines the location of the start of data within the current multipart entity in the received Client messages, and the length of data not including the boundary string.</span></span> <span data-ttu-id="c8c9b-1550">Internamente, il server HTTP Aggiorna i propri offset in modo che questa funzione possa essere richiamata nello stesso datagramma client per i messaggi con più entità.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1550">Internally, the HTTP server updates its own offsets so that this function can be called again on the same Client datagram for messages with multiple entities.</span></span> <span data-ttu-id="c8c9b-1551">Il puntatore al pacchetto viene aggiornato al pacchetto successivo in cui il messaggio del client è un datagramma con più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1551">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

<span data-ttu-id="c8c9b-1552">Si noti che per usare questo servizio NX_WEB_HTTP_MULTIPART_ENABLE necessario abilitarlo.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1552">Note that NX_WEB_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span> <span data-ttu-id="c8c9b-1553">Si noti inoltre che l'applicazione non deve rilasciare il pacchetto a cui punta packet_pptr.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1553">Also note that the application should not release the packet pointed to by packet_pptr.</span></span> <span data-ttu-id="c8c9b-1554">Questa operazione viene eseguita internamente dal server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1554">This is done internally by the HTTP server.</span></span>

<span data-ttu-id="c8c9b-1555">Per ulteriori informazioni, vedere *nx_web_http_server_get_entity_header ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1555">See *nx_web_http_server_get_entity_header()* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1556">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1556">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1557">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1557">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="c8c9b-1558">**packet_pptr** Puntatore alla posizione del puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1558">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="c8c9b-1559">Si noti che l'applicazione non deve rilasciare questo pacchetto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1559">Note that the application should not release this packet</span></span>
- <span data-ttu-id="c8c9b-1560">**available_offset** Puntatore all'offset dei dati dell'entità dal puntatore a prependi del pacchetto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1560">**available_offset** Pointer to offset of entity data from the packet prepend pointer</span></span>
- <span data-ttu-id="c8c9b-1561">**available_length** Puntatore alla lunghezza dei dati dell'entità</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1561">**available_length** Pointer to length of entity data</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1562">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1562">Return Values</span></span>

- <span data-ttu-id="c8c9b-1563">**NX_SUCCESS** (0x00) ha recuperato correttamente le dimensioni e la posizione del contenuto dell'entità</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1563">**NX_SUCCESS** (0x00) Successfully retrieved size and location of entity content</span></span>
- <span data-ttu-id="c8c9b-1564">Il contenuto **NX_WEB_HTTP_BOUNDARY_ALREADY_FOUND** (0x30016) per i marcatori multipart interni del server http è già stato trovato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1564">**NX_WEB_HTTP_BOUNDARY_ALREADY_FOUND** (0x30016) Content for the HTTP server internal multipart markers is already found</span></span>
- <span data-ttu-id="c8c9b-1565">Errore interno del server HTTP NX_WEB_HTTP_ERROR (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1565">NX_WEB_HTTP_ERROR (0x30000) HTTP Server internal error</span></span>
- <span data-ttu-id="c8c9b-1566">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1566">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1567">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1567">Allowed From</span></span>

<span data-ttu-id="c8c9b-1568">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1568">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1569">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1569">Example</span></span>

```C
NX_WEB_HTTP_SERVER my_server;
UINT offset, length;
NX_PACKET *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
    the entity header to determine details about the multipart data. If
    successful, it then calls this service to get the location of entity data: */
status = nx_web_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
    &length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
    entity data. */
```

## <a name="nx_web_http_server_get_entity_header"></a><span data-ttu-id="c8c9b-1570">nx_web_http_server_get_entity_header</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1570">nx_web_http_server_get_entity_header</span></span>

<span data-ttu-id="c8c9b-1571">Recupera il contenuto dell'intestazione dell'entità</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1571">Retrieve the contents of entity header</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1572">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1572">Prototype</span></span>

```C
UINT nx_web_http_server_get_entity_header(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    UCHAR *entity_header_buffer,
    ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1573">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1573">Description</span></span>

<span data-ttu-id="c8c9b-1574">Questo servizio recupera l'intestazione dell'entità nel buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1574">This service retrieves the entity header into the specified buffer.</span></span> <span data-ttu-id="c8c9b-1575">Il server HTTP interno aggiorna i propri puntatori per individuare la prossima entità multipart in un datagramma client con più intestazioni di entità.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1575">Internally HTTP Server updates its own pointers to locate the next multipart entity in a Client datagram with multiple entity headers.</span></span> <span data-ttu-id="c8c9b-1576">Il puntatore al pacchetto viene aggiornato al pacchetto successivo in cui il messaggio del client è un datagramma con più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1576">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

<span data-ttu-id="c8c9b-1577">Si noti che per usare questo servizio NX_WEB_HTTP_MULTIPART_ENABLE necessario abilitarlo.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1577">Note that NX_WEB_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span> <span data-ttu-id="c8c9b-1578">Si noti inoltre che l'applicazione non deve rilasciare il pacchetto a cui punta packet_pptr.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1578">Note also that the application should not release the packet pointed to by packet_pptr.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1579">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1579">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1580">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1580">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="c8c9b-1581">**packet_pptr** Puntatore alla posizione del puntatore del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1581">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="c8c9b-1582">Si noti che l'applicazione non deve rilasciare questo pacchetto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1582">Note that the application should not release this packet</span></span>
- <span data-ttu-id="c8c9b-1583">**entity_header_buffer** Puntatore alla posizione in cui archiviare l'intestazione dell'entità</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1583">**entity_header_buffer** Pointer to location to store entity header</span></span>
- <span data-ttu-id="c8c9b-1584">**BUFFER_SIZE** Dimensioni del buffer di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1584">**buffer_size** Size of input buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1585">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1585">Return Values</span></span>

- <span data-ttu-id="c8c9b-1586">L'intestazione dell'entità è stata recuperata **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1586">**NX_SUCCESS** (0x00) Successfully retrieved entity Header</span></span>
- <span data-ttu-id="c8c9b-1587">Campo di intestazione dell'entità **NX_WEB_HTTP_NOT_FOUND** (0x30006) non trovato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1587">**NX_WEB_HTTP_NOT_FOUND** (0x30006) Entity header field not found</span></span>
- <span data-ttu-id="c8c9b-1588">Tempo di **NX_WEB_HTTP_TIMEOUT** (0x30001) scaduto per la ricezione del pacchetto successivo per il messaggio client Multipack</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1588">**NX_WEB_HTTP_TIMEOUT** (0x30001) Time expired to receive next packet for multipacket client message</span></span>
- <span data-ttu-id="c8c9b-1589">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1589">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1590">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1590">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="c8c9b-1591">Errore HTTP interno NX_WEB_HTTP_ERROR (0x30000)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1591">NX_WEB_HTTP_ERROR (0x30000) Internal HTTP error</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1592">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1592">Allowed From</span></span>

<span data-ttu-id="c8c9b-1593">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1593">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1594">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1594">Example</span></span>

```C
/* Buffer to hold data we are extracting from the request. */
UCHAR buffer[1440];

/* *my_request_notify()* is the application request notify callback
    registered with the HTTP server in *nx_web_http_server_create()*,
    creates a response to the received Client request. */
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    UINT offset, length;
    NX_PACKET *response_pkt;

    /* Process multipart data. */
    if(request_type == NX_WEB_HTTP_SERVER_POST_REQUEST)
    {
        /* Get the content header. */
        while(nx_web_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
            sizeof(buffer)) == NX_SUCCESS)
        {
            /* Header obtained successfully. Get the content data location. */
            while(nx_web_http_server_get_entity_content(server_ptr,
                &packet_ptr, &offset, &length) == NX_SUCCESS)
            {
                /* Write content data to buffer. */
                nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                    &length);
                buffer[length] = 0;
            }
        }

        /* Generate HTTP header. */
        status = nx_web_http_server_callback_generate_response_header(server_ptr,
            &response_pkt, NX_WEB_HTTP_STATUS_OK, 800, "text/html",
            "Server: NetX WEB HTTP 5.10\r\n");

        if(status == NX_SUCCESS)
        {
            if(nx_web_http_server_callback_packet_send(server_ptr, response_pkt) !=
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
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);
}

```

## <a name="nx_web_http_server_gmt_callback_set"></a><span data-ttu-id="c8c9b-1595">nx_web_http_server_gmt_callback_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1595">nx_web_http_server_gmt_callback_set</span></span>

<span data-ttu-id="c8c9b-1596">Impostare il callback per ottenere la data e l'ora GMT</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1596">Set the callback to obtain GMT date and time</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1597">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1597">Prototype</span></span>

```C
UINT nx_web_http_server_gmt_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID (*gmt_get)(NX_WEB_HTTP_SERVER_DATE *date);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1598">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1598">Description</span></span>

<span data-ttu-id="c8c9b-1599">Questo servizio imposta il callback per ottenere la data e l'ora GMT con un server HTTP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1599">This service sets the callback to obtain GMT date and time with a previously created HTTP server.</span></span> <span data-ttu-id="c8c9b-1600">Questo servizio viene richiamato con il server HTTP che sta creando un'intestazione nel server HTTP risposte al client.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1600">This service is invoked with the HTTP server is creating a header in HTTP server responses to the Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1601">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1601">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1602">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1602">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="c8c9b-1603">**gmt_get** Puntatore al callback GMT</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1603">**gmt_get** Pointer to GMT callback</span></span>
- <span data-ttu-id="c8c9b-1604">**Data di scadenza** Puntatore alla data recuperata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1604">**date** Pointer to the date retrieved</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1605">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1605">Return Values</span></span>

- <span data-ttu-id="c8c9b-1606">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1606">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8c9b-1607">NX_PTR_ERROR (0x07) il puntatore al pacchetto o al parametro non è valido.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1607">NX_PTR_ERROR (0x07) Invalid packet or parameter pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1608">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1608">Allowed From</span></span>

<span data-ttu-id="c8c9b-1609">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1609">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1610">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1610">Example</span></span>

```C
NX_WEB_HTTP_SERVER my_server;

VOID get_gmt(NX_WEB_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_web_http_server_create(),
    and before starting HTTP services when nx_web_http_server_start() is called,
    set the GMT retrieve callback: */
status = nx_web_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
    response header date. */
```

## <a name="nx_web_http_server_invalid_userpassword_notify_set"></a><span data-ttu-id="c8c9b-1611">nx_web_http_server_invalid_userpassword_notify_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1611">nx_web_http_server_invalid_userpassword_notify_set</span></span>

<span data-ttu-id="c8c9b-1612">Impostare il callback per gestire l'utente o la password non valida</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1612">Set the callback to handle invalid user/password</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1613">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1613">Prototype</span></span>

```C
UINT nx_web_http_server_invalid_userpassword_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*invalid_username_password_callback)
        (CHAR *resource,
        ULONG client_address,
        UINT request_type));
```

### <a name="description"></a><span data-ttu-id="c8c9b-1614">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1614">Description</span></span>

<span data-ttu-id="c8c9b-1615">Questo servizio imposta il callback richiamato quando viene ricevuto un nome utente e una password non validi in una richiesta GET, put o Delete del client, mediante l'autenticazione digest o di base.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1615">This service sets the callback invoked when an invalid username and password is received in a Client get, put or delete request, either by digest or basic authentication.</span></span> <span data-ttu-id="c8c9b-1616">Il server HTTP deve essere creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1616">The HTTP server must be previously created.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1617">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1617">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1618">**server_ptr** Puntatore al server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1618">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="c8c9b-1619">**invalid_username_password_callback** Puntatore a callback utente/pass non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1619">**invalid_username_password_callback** Pointer to invalid user/pass callback</span></span>
- <span data-ttu-id="c8c9b-1620">**risorsa** di Puntatore alla risorsa specificata dal client</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1620">**resource** Pointer to the resource specified by the client</span></span>
- <span data-ttu-id="c8c9b-1621">**CLIENT_ADDRESS** Indirizzo client</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1621">**client_address** Client address</span></span>
- <span data-ttu-id="c8c9b-1622">**request_type** Indica il tipo di richiesta client.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1622">**request_type** Indicates client request type.</span></span> <span data-ttu-id="c8c9b-1623">Può essere:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1623">May be:</span></span>
  - <span data-ttu-id="c8c9b-1624">*NX_WEB_HTTP_SERVER_GET_REQUEST*</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1624">*NX_WEB_HTTP_SERVER_GET_REQUEST*</span></span>
  - <span data-ttu-id="c8c9b-1625">*NX_WEB_HTTP_SERVER_POST_REQUEST NX_WEB_HTTP_SERVER_HEAD_REQUEST*</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1625">*NX_WEB_HTTP_SERVER_POST_REQUEST NX_WEB_HTTP_SERVER_HEAD_REQUEST*</span></span>
  - <span data-ttu-id="c8c9b-1626">*NX_WEB_HTTP_SERVER_PUT_REQUEST NX_WEB_HTTP_SERVER_DELETE_REQUEST*</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1626">*NX_WEB_HTTP_SERVER_PUT_REQUEST NX_WEB_HTTP_SERVER_DELETE_REQUEST*</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1627">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1627">Return Values</span></span>

- <span data-ttu-id="c8c9b-1628">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1628">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8c9b-1629">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1629">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1630">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1630">Allowed From</span></span>

<span data-ttu-id="c8c9b-1631">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1631">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1632">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1632">Example</span></span>

```C
NX_WEB_HTTP_SERVER my_server;

VOID invalid_username_password_callback(NX_CHAR *resource,
    ULONG client_address,
    UINT request_type);

/* After the HTTP server is created by calling nx_web_http_server_create,
    and before starting HTTP services when nx_web_http_server_start() is called,
    set the invalid username password callback: */

status = nx_web_http_server_invalid_userpassword_notify_set( (&my_server,
    invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
    will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_web_http_server_mime_maps_additional_set"></a><span data-ttu-id="c8c9b-1633">nx_web_http_server_mime_maps_additional_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1633">nx_web_http_server_mime_maps_additional_set</span></span>

<span data-ttu-id="c8c9b-1634">Impostare mappe MIME aggiuntive per HTML</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1634">Set additional MIME maps for HTML</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1635">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1635">Prototype</span></span>

```C
UINT nx_web_http_server_mime_maps_additional_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_WEB_HTTP_SERVER_MIME_MAP *mime_maps,
    UINT mime_maps_num);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1636">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1636">Description</span></span>

<span data-ttu-id="c8c9b-1637">Questo servizio consente allo sviluppatore di applicazioni HTTP di aggiungere altri tipi MIME dai tipi MIME predefiniti forniti dal server HTTP Web NetX.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1637">This service allows the HTTP application developer to add additional MIME types from the default MIME types supplied by the NetX Web HTTP Server.</span></span> <span data-ttu-id="c8c9b-1638">Per un elenco dei tipi definiti, vedere *nx_web_http_server_get_type ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1638">See *nx_web_http_server_get_type()* for list of defined types.</span></span>

<span data-ttu-id="c8c9b-1639">Quando viene ricevuta una richiesta client, ad esempio una richiesta GET, il server HTTP analizza il tipo di file richiesto dall'intestazione HTTP usando il set di mappe MIME aggiuntivo e, se non viene trovata alcuna corrispondenza, Cerca una corrispondenza nella mappa MIME predefinita del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1639">When a client request is received, e.g. a GET request, HTTP server parses the requested file type from the HTTP header using preferentially the additional MIME map set and if no match if found, it looks for a match in the default MIME map of the HTTP server.</span></span> <span data-ttu-id="c8c9b-1640">Se non viene trovata alcuna corrispondenza, il valore predefinito del tipo MIME è "text/plain".</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1640">If no match is found, the MIME type defaults to "text/plain".</span></span>

<span data-ttu-id="c8c9b-1641">Se la funzione request Notify è registrata con il server HTTP, il callback della richiesta di notifica può chiamare *nx_web_http_server_type_get_extended ()* per analizzare il tipo di file.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1641">If the request notify function is registered with the HTTP server, the request notify callback can call *nx_web_http_server_type_get_extended()* to parse the file type.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1642">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1642">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1643">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1643">**server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8c9b-1644">**mime_maps** Puntatore a una matrice di mappa MIME</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1644">**mime_maps** Pointer to a MIME map array</span></span>
- <span data-ttu-id="c8c9b-1645">**mime_map_num** Numero di mappe MIME nella matrice</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1645">**mime_map_num** Number of MIME maps in array</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1646">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1646">Return Values</span></span>

- <span data-ttu-id="c8c9b-1647">Set di mappe MIME del server HTTP con **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1647">**NX_SUCCESS** (0x00) Successful HTTP Server MIME map set</span></span>
- <span data-ttu-id="c8c9b-1648">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1648">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1649">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1649">Allowed From</span></span>

<span data-ttu-id="c8c9b-1650">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1650">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1651">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1651">Example</span></span>

```C
/* my_server is an NX_WEB_HTTP_SERVER previously created. */
static NX_WEB_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc", "yourtype/abc"},
    {"xyz", "mytype/xyz"},
};

status = nx_web_http_server_mime_maps_additional_set(&my_server,
    &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP
    server MIME map set." */
```

## <a name="nx_web_http_server_response_packet_allocate"></a><span data-ttu-id="c8c9b-1652">nx_web_http_server_response_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1652">nx_web_http_server_response_packet_allocate</span></span>

<span data-ttu-id="c8c9b-1653">Allocare un pacchetto HTTP (S)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1653">Allocate an HTTP(S) packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1654">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1654">Prototype</span></span>

```C
UINT nx_web_http_server_response_packet_allocate(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1655">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1655">Description</span></span>

<span data-ttu-id="c8c9b-1656">Questo servizio tenta di allocare un pacchetto per il server HTTP (S).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1656">This service attempts to allocates a packet for the HTTP(S) server.</span></span>

<span data-ttu-id="c8c9b-1657">Si noti che se un'API NetX o HTTP Server successiva che usa questo pacchetto come input ha **esito negativo**, ad esempio nx_packet_data_append o \* \* nx_web_http_server_callback_packet_send, l'applicazione è responsabile del rilascio del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1657">Note that if a subsequent NetX or HTTP Server API using this packet as input **fails**, such as nx_packet_data_append or \*\*nx_web_http_server_callback_packet_send, the application is responsible for releasing the packet.</span></span> **

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1658">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1658">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1659">**server_ptr** Puntatore al blocco di controllo server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1659">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8c9b-1660">**packet_ptr** Puntatore al pacchetto allocato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1660">**packet_ptr** Pointer to allocated packet.</span></span>
- <span data-ttu-id="c8c9b-1661">**WAIT_OPTION** Definisce il tempo di attesa in cicli se non sono disponibili pacchetti nel pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1661">**wait_option** Defines the wait time in ticks if there are no packets available in the packet pool.</span></span> <span data-ttu-id="c8c9b-1662">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1662">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8c9b-1663">**NX_NO_WAIT** (0x00000000) se si seleziona NX_NO_WAIT, il thread chiamante restituirà immediatamente se la richiesta non può essere soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1663">**NX_NO_WAIT** (0x00000000) Selecting NX_NO_WAIT causes the calling thread to return immediately if the request cannot be fulfilled.</span></span>
  - <span data-ttu-id="c8c9b-1664">**NX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di NX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server HTTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1664">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>
  - <span data-ttu-id="c8c9b-1665">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (0x1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server http.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1665">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1666">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1666">Return Values</span></span>

- <span data-ttu-id="c8c9b-1667">Allocazione pacchetto riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1667">**NX_SUCCESS** (0x00) Successful packet allocate</span></span>
- <span data-ttu-id="c8c9b-1668">**NX_NO_PACKET** (0x01) non sono disponibili pacchetti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1668">**NX_NO_PACKET** (0x01) No packet available</span></span>
- <span data-ttu-id="c8c9b-1669">La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al *tx_thread_wait_abort*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1669">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="c8c9b-1670">Le dimensioni del pacchetto **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non supportano il protocollo.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1670">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="c8c9b-1671">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1671">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1672">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1672">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1673">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1673">Allowed From</span></span>

<span data-ttu-id="c8c9b-1674">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1674">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1675">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1675">Example</span></span>

```C
/* Allocate a packet for HTTP(S) Server and suspend for a maximum of 5 timer
    ticks if the pool is empty. */
status = nx_web_http_server_response_packet_allocate(&my_client, &packet_ptr, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
    variable packet_ptr. */
```

## <a name="nx_web_http_server_packet_content_find"></a><span data-ttu-id="c8c9b-1676">nx_web_http_server_packet_content_find</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1676">nx_web_http_server_packet_content_find</span></span>

<span data-ttu-id="c8c9b-1677">Estrarre la lunghezza del contenuto e impostare il puntatore all'inizio dei dati</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1677">Extract content length and set pointer to start of data</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1678">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1678">Prototype</span></span>

```C
UINT nx_web_http_server_packet_content_find(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr,
    UINT *content_length);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1679">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1679">Description</span></span>

<span data-ttu-id="c8c9b-1680">Questo servizio estrae la lunghezza del contenuto dall'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1680">This service extracts the content length from the HTTP header.</span></span> <span data-ttu-id="c8c9b-1681">Aggiorna inoltre il pacchetto fornito come indicato di seguito: il puntatore del pacchetto Prepend (inizio della posizione del buffer dei pacchetti in cui scrivere) viene impostato sul contenuto HTTP (dati) appena passata l'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1681">It also updates the supplied packet as follows: the packet prepend pointer (start of location of packet buffer to write to) is set to the HTTP content (data) just passed the HTTP header.</span></span>

<span data-ttu-id="c8c9b-1682">Se l'inizio del contenuto non viene trovato nel pacchetto corrente, la funzione attende la ricezione del pacchetto successivo utilizzando l'opzione NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE wait.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1682">If the beginning of content is not found in the current packet, the function waits for the next packet to be received using the NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE wait option.</span></span>

<span data-ttu-id="c8c9b-1683">Si noti che questo metodo non deve essere chiamato prima di chiamare *nx_web_http_server_get_entity_header ()* perché modifica il puntatore anteposto del pacchetto oltre l'intestazione dell'entità.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1683">Note this should not be called before calling *nx_web_http_server_get_entity_header()* because it modifies the packet prepend pointer past the entity header.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1684">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1684">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1685">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1685">**server_ptr** Pointer to HTTP server instance</span></span>
- <span data-ttu-id="c8c9b-1686">**packet_ptr** Puntatore al puntatore del pacchetto per la restituzione del pacchetto con puntatore anteposto aggiornato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1686">**packet_ptr** Pointer to packet pointer for returning the packet with updated prepend pointer</span></span>
- <span data-ttu-id="c8c9b-1687">**CONTENT_LENGTH** Puntatore a content_length estratte</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1687">**content_length** Pointer to extracted content_length</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1688">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1688">Return Values</span></span>

- <span data-ttu-id="c8c9b-1689">È stata trovata la lunghezza del contenuto HTTP **NX_SUCCESS** (0x00) e l'aggiornamento del pacchetto è riuscito</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1689">**NX_SUCCESS** (0x00) HTTP content length found and packet successfully updated</span></span>
- <span data-ttu-id="c8c9b-1690">Tempo di **NX_WEB_HTTP_TIMEOUT** (0x30001) scaduto in attesa del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1690">**NX_WEB_HTTP_TIMEOUT** (0x30001) Time expired waiting on next Packet</span></span>
- <span data-ttu-id="c8c9b-1691">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1691">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1692">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1692">Allowed From</span></span>

<span data-ttu-id="c8c9b-1693">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1693">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1694">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1694">Example</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
    The server has received a Client request packet, recv_packet_ptr,
    and the packet content find service is called from the request notify callback
    function registered with the HTTP server. */

UINT content_length;

status = nx_web_http_server_packet_content_find(server_ptr, recv_packet_ptr,
    &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
    and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_web_http_server_packet_get"></a><span data-ttu-id="c8c9b-1695">nx_web_http_server_packet_get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1695">nx_web_http_server_packet_get</span></span>

<span data-ttu-id="c8c9b-1696">Ricevere il pacchetto HTTP successivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1696">Receive the next HTTP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1697">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1697">Prototype</span></span>

```C
UINT nx_web_http_server_packet_get(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1698">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1698">Description</span></span>

<span data-ttu-id="c8c9b-1699">Questo servizio restituisce il pacchetto successivo ricevuto sul socket del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1699">This service returns the next packet received on the HTTP server socket.</span></span> <span data-ttu-id="c8c9b-1700">L'opzione Attendi per la ricezione di un pacchetto è NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1700">The wait option to receive a packet is NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE.</span></span>

<span data-ttu-id="c8c9b-1701">Si noti che, in caso di esito positivo, l'applicazione è responsabile del rilascio del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1701">Note that if successful the application is responsible for releasing the packet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1702">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1702">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1703">**server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1703">**server_ptr** Pointer to HTTP server instance</span></span>
- <span data-ttu-id="c8c9b-1704">**packet_ptr** Puntatore al pacchetto ricevuto</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1704">**packet_ptr** Pointer to received packet</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1705">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1705">Return Values</span></span>

- <span data-ttu-id="c8c9b-1706">**NX_SUCCESS** (0x00) ha ricevuto il pacchetto http successivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1706">**NX_SUCCESS** (0x00) Successfully received next HTTP packet</span></span>
- <span data-ttu-id="c8c9b-1707">Tempo di **NX_WEB_HTTP_TIMEOUT** (0x30001) scaduto in attesa del pacchetto successivo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1707">**NX_WEB_HTTP_TIMEOUT** (0x30001) Time expired waiting on next Packet</span></span>
- <span data-ttu-id="c8c9b-1708">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1708">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1709">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1709">Allowed From</span></span>

<span data-ttu-id="c8c9b-1710">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1710">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1711">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1711">Example</span></span>

```C
/* The HTTP server pointed to by server_ptr is previously created and started. */
UINT content_length;
NX_PACKET *recv_packet_ptr;

status = nx_web_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_web_http_server_param_get"></a><span data-ttu-id="c8c9b-1712">nx_web_http_server_param_get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1712">nx_web_http_server_param_get</span></span>

<span data-ttu-id="c8c9b-1713">Ottenere il parametro dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1713">Get parameter from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1714">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1714">Prototype</span></span>

```C
UINT nx_web_http_server_param_get(NX_PACKET *packet_ptr,
    UINT param_number, CHAR *param_ptr,
    UINT *param_size, UINT max_param_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1715">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1715">Description</span></span>

<span data-ttu-id="c8c9b-1716">Questo servizio tenta di recuperare il parametro URL HTTP specificato nel pacchetto di richiesta fornito.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1716">This service attempts to retrieve the specified HTTP URL parameter in the supplied request packet.</span></span> <span data-ttu-id="c8c9b-1717">Se il parametro HTTP richiesto non è presente, questa routine restituisce lo stato NX_WEB_HTTP_NOT_FOUND.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1717">If the requested HTTP parameter is not present, this routine returns a status of NX_WEB_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="c8c9b-1718">Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1718">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1719">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1719">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1720">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1720">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="c8c9b-1721">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1721">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="c8c9b-1722">**param_number** Numero logico del parametro a partire da zero, da sinistra a destra nell'elenco dei parametri.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1722">**param_number** Logical number of the parameter starting at zero, from left to right in the parameter list.</span></span>
- <span data-ttu-id="c8c9b-1723">**param_ptr** Area di destinazione per copiare il parametro.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1723">**param_ptr** Destination area to copy the parameter.</span></span>
- <span data-ttu-id="c8c9b-1724">**param_size** Restituisce la lunghezza totale dei dati del parametro (in byte).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1724">**param_size** Return the total parameter data length (in bytes).</span></span>
- <span data-ttu-id="c8c9b-1725">**max_param_size** Dimensioni massime dell'area di destinazione del parametro.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1725">**max_param_size** Maximum size of the parameter destination area.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1726">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1726">Return Values</span></span>

- <span data-ttu-id="c8c9b-1727">**NX_SUCCESS** (0x00) parametro Server http riuscito Get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1727">**NX_SUCCESS** (0x00) Successful HTTP Server parameter get</span></span>
- <span data-ttu-id="c8c9b-1728">Il parametro specificato **NX_WEB_HTTP_NOT_FOUND** (0x30006) non è stato trovato</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1728">**NX_WEB_HTTP_NOT_FOUND** (0x30006) Specified parameter not found</span></span>
- <span data-ttu-id="c8c9b-1729">Il parametro della richiesta **NX_WEB_HTTP_IMPROPERLY_TERMINATED_PARAM** (0x30015) non è terminato correttamente</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1729">**NX_WEB_HTTP_IMPROPERLY_TERMINATED_PARAM** (0x30015) Request parameter not properly terminated</span></span>
- <span data-ttu-id="c8c9b-1730">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1730">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1731">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1731">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1732">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1732">Allowed From</span></span>

<span data-ttu-id="c8c9b-1733">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1733">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1734">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1734">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, get the first parameter of the HTTP Client request. */

status = nx_web_http_server_param_get(request_packet_ptr, 0, param_destination,
    &param_size, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
    in "param_destination" and the size of that string can be found
    in the variable "param_size." */
```

## <a name="nx_web_http_server_query_get"></a><span data-ttu-id="c8c9b-1735">nx_web_http_server_query_get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1735">nx_web_http_server_query_get</span></span>

<span data-ttu-id="c8c9b-1736">Ottenere una query dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1736">Get query from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1737">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1737">Prototype</span></span>

```C
UINT nx_web_http_server_query_get(NX_PACKET *packet_ptr,
    UINT query_number,
    CHAR *query_ptr,
    CHAR *query_size,
    UINT max_query_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1738">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1738">Description</span></span>

<span data-ttu-id="c8c9b-1739">Questo servizio tenta di recuperare la query URL HTTP specificata nel pacchetto di richiesta fornito.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1739">This service attempts to retrieve the specified HTTP URL query in the supplied request packet.</span></span> <span data-ttu-id="c8c9b-1740">Se la query HTTP richiesta non è presente, questa routine restituisce lo stato NX_WEB_HTTP_NOT_FOUND.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1740">If the requested HTTP query is not present, this routine returns a status of NX_WEB_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="c8c9b-1741">Questa routine deve essere chiamata dal callback di notifica della richiesta dell'applicazione specificato durante la creazione del server HTTP (*nx_web_http_server_create ()*).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1741">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1742">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1742">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1743">**packet_ptr** Puntatore al pacchetto di richiesta del client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1743">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="c8c9b-1744">Si noti che l'applicazione non deve rilasciare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1744">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="c8c9b-1745">**query_number** Numero logico del parametro a partire da zero, da sinistra a destra nell'elenco di query.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1745">**query_number** Logical number of the parameter starting at zero, from left to right in the query list.</span></span>
- <span data-ttu-id="c8c9b-1746">**query_ptr** Area di destinazione per la copia della query.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1746">**query_ptr** Destination area to copy the query.</span></span>
- <span data-ttu-id="c8c9b-1747">**query_size** Restituisce le dimensioni dei dati della query (in byte).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1747">**query_size** Return query data size (in bytes).</span></span>
- <span data-ttu-id="c8c9b-1748">**max_query_size** Dimensione massima della destinazione della query</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1748">**max_query_size** Maximum size of the query destination</span></span>

<span data-ttu-id="c8c9b-1749">quell'area.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1749">area.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1750">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1750">Return Values</span></span>

- <span data-ttu-id="c8c9b-1751">**NX_SUCCESS** (0x00) query del server http riuscita Get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1751">**NX_SUCCESS** (0x00) Successful HTTP Server query get</span></span>
- <span data-ttu-id="c8c9b-1752">Dimensioni della query di **NX_WEB_HTTP_FAILED** (0x30002) troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1752">**NX_WEB_HTTP_FAILED** (0x30002) Query size too small.</span></span>
- <span data-ttu-id="c8c9b-1753">Impossibile trovare la query specificata **NX_WEB_HTTP_NOT_FOUND** (0x30006)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1753">**NX_WEB_HTTP_NOT_FOUND** (0x30006) Specified query not found</span></span>
- <span data-ttu-id="c8c9b-1754">**NX_WEB_HTTP_NO_QUERY_PARSED** (0X30013) nessuna query nella richiesta client</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1754">**NX_WEB_HTTP_NO_QUERY_PARSED** (0x30013) No query in Client request</span></span>
- <span data-ttu-id="c8c9b-1755">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1755">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1756">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1756">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1757">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1757">Allowed From</span></span>

<span data-ttu-id="c8c9b-1758">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1758">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1759">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1759">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, get the first query of the HTTP Client request. */

status = nx_web_http_server_query_get(request_packet_ptr, 0,
    query_destination, &query_size, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
    in "query_destination" and the length of that string can be found in the
    variable "query_size". */
```

## <a name="nx_web_http_server_response_chunked_set"></a><span data-ttu-id="c8c9b-1760">nx_web_http_server_response_chunked_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1760">nx_web_http_server_response_chunked_set</span></span>

<span data-ttu-id="c8c9b-1761">Imposta il trasferimento Chunked per la risposta HTTP (S)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1761">Set chunked transfer for HTTP(S) response</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1762">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1762">Prototype</span></span>

```C
UINT nx_web_http_server_response_chunked_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT chunk_size, NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1763">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1763">Description</span></span>

<span data-ttu-id="c8c9b-1764">Questo servizio usa la codifica di trasferimento Chunked per inviare al client un pacchetto di dati di risposta HTTP (S) personalizzato creato con *nx_web_http_server_response_packet_allocate*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1764">This service uses chunked transfer coding to send a custom HTTP(S) response data packet created with *nx_web_http_server_response_packet_allocate*() to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-1765">Se l'applicazione usa la codifica di trasferimento Chunked per inviare un pacchetto di dati di risposta, deve chiamare questo servizio dopo aver chiamato *nx_web_http_server_response_packet_allocate*() e prima di chiamare *nx_web_http_server_callback_packet_send*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1765">If the application uses chunked transfer coding to send a response data packet, it must call this service after calling *nx_web_http_server_response_packet_allocate*(), and before calling *nx_web_http_server_callback_packet_send*().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1766">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1766">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1767">**client_ptr** Puntatore al blocco di controllo client HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1767">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8c9b-1768">**chunk_size** Dimensione dei blocchi-dati in ottetti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1768">**chunk_size** Size of the chunk-data in octets.</span></span>
- <span data-ttu-id="c8c9b-1769">**packet_ptr** Puntatore ai pacchetti di dati della richiesta HTTP (S).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1769">**packet_ptr** HTTP(S) request data packet pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1770">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1770">Return Values</span></span>

- <span data-ttu-id="c8c9b-1771">**NX_SUCCESS** (0x00) set completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1771">**NX_SUCCESS** (0x00) Successful set chunked.</span></span>
- <span data-ttu-id="c8c9b-1772">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1772">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1773">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1773">Allowed From</span></span>

<span data-ttu-id="c8c9b-1774">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1774">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1775">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1775">Example</span></span>

```C
/* Generate HTTP header. */
nx_web_http_server_callback_generate_response_header(server_ptr,
    &response_pkt, NX_WEB_HTTP_STATUS_OK, 0, "text/html",
    "Transfer-Encoding: chunked\r\n");

/* Create a new data packet response on the HTTP(S) Server instance. */
nx_web_http_server_response_packet_allocate(&my_server, &my_packet, NX_WAIT_FOREVER);

/* Set the chunked transfer. */
status = nx_web_http_server_response_chunked_set(&my_server, 128, my_packet)

/* At this point, user can fill the data into my_packet. *./
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet response to client. */
nx_web_http_server_callback_packet_send(&my_server, my_packet);
```

## <a name="nx_web_http_server_secure_configure"></a><span data-ttu-id="c8c9b-1776">nx_web_http_server_secure_configure</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1776">nx_web_http_server_secure_configure</span></span>

<span data-ttu-id="c8c9b-1777">Configurare un server HTTP per l'uso di TLS per Secure HTTPS</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1777">Configure an HTTP Server to use TLS for secure HTTPS</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1778">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1778">Prototype</span></span>

```C
UINT nx_web_http_server_secure_configure(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    const NX_SECURE_TLS_CRYPTO *crypto_table,
    VOID *metadata_buffer, ULONG metadata_size,
    UCHAR* packet_buffer, UINT packet_buffer_size,
    NX_SECURE_X509_CERT *identity_certificate,
    NX_SECURE_X509_CERT *trusted_certificates[],
    UINT trusted_certs_num,
    NX_SECURE_X509_CERT *remote_certificates[],
    UINT remote_certs_num,
    UCHAR *remote_certificate_buffer,
    UINT remote_cert_buffer_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1779">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1779">Description</span></span>

<span data-ttu-id="c8c9b-1780">Questo servizio configura un'istanza del server HTTP Web NetX creata in precedenza per l'uso di TLS per le comunicazioni HTTPS sicure.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1780">This service configures a previously created NetX Web HTTP server instance to use TLS for secure HTTPS communications.</span></span> <span data-ttu-id="c8c9b-1781">I parametri vengono usati per configurare tutte le sessioni TLS possibili con lo stato identico, in modo che ogni client HTTPS in ingresso verifichi un comportamento coerente.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1781">The parameters are used to configure all the possible TLS sessions with identical state so that each incoming HTTPS Client experiences consistent behavior.</span></span> <span data-ttu-id="c8c9b-1782">Il numero di sessioni TLS viene controllato utilizzando la macro NX_WEB_HTTP_SESSION_MAX.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1782">The number of TLS sessions is controlled using the macro NX_WEB_HTTP_SESSION_MAX.</span></span>

<span data-ttu-id="c8c9b-1783">La tabella di routine di crittografia (tabella ciphersuite) viene condivisa tra tutte le sessioni TLS perché contiene solo i puntatori a funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1783">The cryptographic routine table (ciphersuite table) is shared between all TLS sessions as it just contains function pointers.</span></span>

<span data-ttu-id="c8c9b-1784">I buffer dei metadati e dei riassemblatori dei pacchetti sono divisi equamente tra tutte le sessioni TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1784">The metadata and packet reassembly buffers are each divided equally between all TLS sessions.</span></span> <span data-ttu-id="c8c9b-1785">Se la dimensione del buffer non è divisibile equamente per il numero di sessioni, il resto non verrà usato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1785">If the buffer size is not evenly divisible by the number of sessions the remainder will be unused.</span></span>

<span data-ttu-id="c8c9b-1786">Il certificato di identità passato viene usato da tutte le sessioni.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1786">The passed-in identity certificate is used by all sessions.</span></span> <span data-ttu-id="c8c9b-1787">Durante l'operazione TLS, il certificato di identità server viene letto solo da, quindi le copie non sono necessarie per ogni sessione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1787">During TLS operation the server identity certificate is only read from so copies are not needed for each session.</span></span>

<span data-ttu-id="c8c9b-1788">I certificati attendibili vengono aggiunti a ogni sessione TLS nel server HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1788">The trusted certificates are added to each TLS session in the HTTPS Server.</span></span> <span data-ttu-id="c8c9b-1789">Questi vengono usati per l'autenticazione del certificato client abilitata automaticamente quando viene fornito spazio per i certificati remoti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1789">These are used for Client certificate authentication which is automatically enabled when remote certificate space is provided.</span></span>

<span data-ttu-id="c8c9b-1790">Per impostazione predefinita, la matrice e il buffer del certificato remoto sono condivisi tra tutte le sessioni TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1790">The remote certificate array and buffer is shared by default between all TLS sessions.</span></span> <span data-ttu-id="c8c9b-1791">I certificati remoti vengono usati per l'autenticazione del certificato client, che viene abilitata automaticamente quando il numero di certificati remoti è diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1791">The remote certificates are used for Client certificate authentication which is automatically enabled when the remote certificate count is nonzero.</span></span> <span data-ttu-id="c8c9b-1792">A causa della condivisione del buffer, è possibile che alcune sessioni si blocchino durante la convalida del certificato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1792">Due to the buffer being shared some sessions may block during certificate validation.</span></span>

<span data-ttu-id="c8c9b-1793">Per disabilitare l'autenticazione del certificato client, passare NX_NULL per il parametro remote_certificates e il valore 0 per il parametro remote_certs_num.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1793">To disable client certificate authentication, pass NX_NULL for the remote_certificates parameter and a value of 0 for the remote_certs_num parameter.</span></span>

<span data-ttu-id="c8c9b-1794">I valori restituiti includeranno eventuali codici di errore TLS derivanti da problemi di configurazione delle sessioni TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1794">Return values will include any TLS error codes resulting from issues in the configuration of the TLS sessions.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1795">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1795">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1796">**http_server_ptr** Puntatore all'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1796">**http_server_ptr** Pointer to HTTP Server instance.</span></span>
- <span data-ttu-id="c8c9b-1797">**crypto_table** Puntatore alla tabella TLS ciphersuite.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1797">**crypto_table** Pointer to TLS ciphersuite table.</span></span>
- <span data-ttu-id="c8c9b-1798">**metadata_buffer** Puntatore al buffer dei metadati crittografici.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1798">**metadata_buffer** Pointer to cryptographic metadata buffer.</span></span>
- <span data-ttu-id="c8c9b-1799">**metadata_size** Dimensioni del buffer dei metadati crittografici.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1799">**metadata_size** Size of cryptographic metadata buffer.</span></span>
- <span data-ttu-id="c8c9b-1800">**packet_buffer** Buffer del riassemblaggio dei pacchetti TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1800">**packet_buffer** TLS packet reassembly buffer.</span></span>
- <span data-ttu-id="c8c9b-1801">**packet_buffer** Dimensioni del buffer dei pacchetti TLS: devono essere uguali a (<dimensioni del buffer TLS desiderate \* NX_WEB_HTTP_SESSION_MAX).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1801">**packet_buffer** Size of TLS packet buffer – should be equal to (<desired TLS buffer size\* NX_WEB_HTTP_SESSION_MAX).</span></span>
- <span data-ttu-id="c8c9b-1802">**identity_certificate** Certificato di identità del server TLS: verrà usato per tutte le sessioni del server HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1802">**identity_certificate** TLS server identity certificate – will be used for all HTTPS server sessions.</span></span>
- <span data-ttu-id="c8c9b-1803">**trusted_certificates** Puntatore alla matrice di oggetti NX_SECURE_X509_CERT, utilizzato per convalidare i certificati client in ingresso se l'autenticazione del certificato client viene abilitata passando un valore diverso da zero per il parametro *remote_certs_num* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1803">**trusted_certificates** Pointer to array of NX_SECURE_X509_CERT objects, used to validate incoming client certificates if client certificate authentication is enabled by passing a non-zero value for the *remote_certs_num* parameter.</span></span>
- <span data-ttu-id="c8c9b-1804">**trusted_certs_num** Numero di certificati attendibili nella matrice *trusted_certificates* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1804">**trusted_certs_num** Number of trusted certificates in the *trusted_certificates* array.</span></span>
- <span data-ttu-id="c8c9b-1805">**remote_certificates** Puntatore alla matrice di oggetti NX_SECURE_X509_CERT utilizzati per i certificati client in ingresso.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1805">**remote_certificates** Pointer to array of NX_SECURE_X509_CERT objects, used for incoming client certificates.</span></span>
- <span data-ttu-id="c8c9b-1806">**remote_certs_num** Numero di certificati remoti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1806">**remote_certs_num** Number of remote certificates.</span></span> <span data-ttu-id="c8c9b-1807">Deve corrispondere al numero massimo di certificati previsti dai client.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1807">Should be the maximum number of expected certificates from clients.</span></span> <span data-ttu-id="c8c9b-1808">L'autenticazione del certificato client viene abilitata automaticamente quando è diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1808">Client certificate authentication is enabled automatically when this is non-zero.</span></span>
- <span data-ttu-id="c8c9b-1809">**remote_certificate_buffer** Buffer che contiene i certificati remoti in ingresso dai client se è abilitata l'autenticazione del certificato client.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1809">**remote_certificate_buffer** Buffer to contain incoming remote certificates from clients if client certificate authentication is enabled.</span></span> <span data-ttu-id="c8c9b-1810">remote_cert_buffer_size dimensione del buffer dei certificati remoti.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1810">remote_cert_buffer_size Size of remote certificates buffer.</span></span> <span data-ttu-id="c8c9b-1811">Deve essere uguale a (<dimensioni massime previste del certificato \* remote_certs_num).</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1811">Should be equal to (<maximum expected certificate size \* remote_certs_num).</span></span>


### <a name="return-values"></a><span data-ttu-id="c8c9b-1812">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1812">Return Values</span></span>

- <span data-ttu-id="c8c9b-1813">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1813">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c8c9b-1814">**NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1814">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="c8c9b-1815">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0X102) un tipo di messaggio TLS ricevuto non è corretto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1815">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) A received TLS message type is incorrect.</span></span>
- <span data-ttu-id="c8c9b-1816">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0X106) una crittografia fornita dall'host remoto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1816">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A cipher provided by the remote host is not supported.</span></span>
- <span data-ttu-id="c8c9b-1817">L'elaborazione del messaggio **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) durante l'handshake TLS non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1817">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Message processing during the TLS handshake has failed.</span></span>
- <span data-ttu-id="c8c9b-1818">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0X108) un messaggio in arrivo non ha superato un controllo Mac hash.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1818">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) An incoming message failed a  hash MAC check.</span></span>
- <span data-ttu-id="c8c9b-1819">**NX_SECURE_TLS_TCP_SEND_FAILE** (0x109) non è stato possibile inviare un socket TCP sottostante.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1819">**NX_SECURE_TLS_TCP_SEND_FAILE** (0x109) An underlying TCP socket send failed.</span></span>
- <span data-ttu-id="c8c9b-1820">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0X10A) un messaggio in ingresso ha un campo di lunghezza non valido.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1820">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) An incoming message had an invalid length field.</span></span>
- <span data-ttu-id="c8c9b-1821">**NX_SECURE_TLS_BAD_CIPHERSPE** (0X10B) un messaggio ChangeCipherSpec in ingresso non è corretto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1821">**NX_SECURE_TLS_BAD_CIPHERSPE** (0x10B) An incoming ChangeCipherSpec message was incorrect.</span></span>
- <span data-ttu-id="c8c9b-1822">**NX_SECURE_TLS_INVALID_SERVER_CER** (0X10C) un certificato TLS in ingresso è inutilizzabile per l'identificazione del server TLS remoto.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1822">**NX_SECURE_TLS_INVALID_SERVER_CER** (0x10C) An incoming TLS certificate is unusable for identifying the remote TLS server.</span></span>
- <span data-ttu-id="c8c9b-1823">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0X10D) la crittografia a chiave pubblica fornita dall'host remoto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1823">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) The public-key cipher provided by the remote host is unsupported.</span></span>
- <span data-ttu-id="c8c9b-1824">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0X10E) l'host remoto non ha indicato ciphersuites supportati dallo stack TLS sicuro NETX.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1824">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) The remote host has indicated no ciphersuites that are supported by the NetX Secure TLS stack.</span></span>
- <span data-ttu-id="c8c9b-1825">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) un messaggio TLS ricevuto ha una versione di TLS sconosciuta nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1825">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received TLS message had an unknown TLS version in its header.</span></span>
- <span data-ttu-id="c8c9b-1826">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) un messaggio TLS ricevuto ha una versione di TLS nota ma non supportata nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1826">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) A received TLS message had a known but unsupported TLS version in its header.</span></span>
- <span data-ttu-id="c8c9b-1827">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0X111) l'allocazione di pacchetti TLS interna non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1827">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) An internal TLS packet allocation failed.</span></span>
- <span data-ttu-id="c8c9b-1828">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0X112) l'host remoto ha fornito un certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1828">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) The remote host provided an invalid certificate.</span></span>
- <span data-ttu-id="c8c9b-1829">**NX_SECURE_TLS_ALERT_RECEIVED** (0X114) l'host remoto ha inviato un avviso che indica un errore e termina la sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1829">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) The remote host sent an alert indicating an error and ending the TLS session.</span></span>
- <span data-ttu-id="c8c9b-1830">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1830">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1831">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1831">Allowed From</span></span>

<span data-ttu-id="c8c9b-1832">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1832">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1833">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1833">Example</span></span>

```C
/* Create the HTTPS Server. */

status = nx_web_http_server_create(&my_server, "My HTTP Server",
    &ip_0, &ram_disk, &server_stack, sizeof(server_stack),
    &pool_0, authentication_check, server_request_callback);

/* Initialize device certificate (used for all sessions in HTTPS server). */
nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
    device_cert_der_len, NX_NULL, 0,
    device_cert_key_der, device_cert_key_der_len,
    NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

/* Setup TLS session for the HTTPS server.
    Note that since the remote_certs_num parameter is 0,
    no trusted certificates are needed, and Client certificate authentication is disabled. */
status = nx_web_http_server_secure_configure(&my_server, &nx_crypto_tls_ciphers,
    crypto_metadata,
    sizeof(crypto_metadata),
    tls_packet_buffer, sizeof(tls_packet_buffer),
    &certificate, NX_NULL, 0, NX_NULL, 0, NX_NULL, 0);

/* Start an HTTPS Server with TLS. */
status = nx_web_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_web_http_server_start"></a><span data-ttu-id="c8c9b-1834">nx_web_http_server_start</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1834">nx_web_http_server_start</span></span>

<span data-ttu-id="c8c9b-1835">Avviare il server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1835">Start the HTTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1836">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1836">Prototype</span></span>

```C
UINT nx_web_http_server_start(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1837">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1837">Description</span></span>

<span data-ttu-id="c8c9b-1838">Questo servizio avvia un'istanza del server HTTP o HTTPS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1838">This service starts a previously created HTTP or HTTPS Server instance.</span></span>

<span data-ttu-id="c8c9b-1839">I server HTTPS condividono la stessa API HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1839">HTTPS servers share the same API as HTTP.</span></span> <span data-ttu-id="c8c9b-1840">Per abilitare HTTPS usando TLS in un server HTTP, vedere il nx_web_http_server_secure_configure di servizio *().*</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1840">To enable HTTPS using TLS on an HTTP server, see the service *nx_web_http_server_secure_configure().*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1841">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1841">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1842">**http_server_ptr** Puntatore all'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1842">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1843">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1843">Return Values</span></span>

- <span data-ttu-id="c8c9b-1844">Inizio del server HTTP **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1844">**NX_SUCCESS** (0x00) Successful HTTP Server Start</span></span>
- <span data-ttu-id="c8c9b-1845">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1845">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1846">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1846">Allowed From</span></span>

<span data-ttu-id="c8c9b-1847">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1847">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1848">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1848">Example</span></span>

```C
/* Start the HTTP Server instance "my_server." */
status = nx_web_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_web_http_server_stop"></a><span data-ttu-id="c8c9b-1849">nx_web_http_server_stop</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1849">nx_web_http_server_stop</span></span>

<span data-ttu-id="c8c9b-1850">Arrestare il server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1850">Stop the HTTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1851">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1851">Prototype</span></span>

```C
UINT nx_web_http_server_stop(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1852">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1852">Description</span></span>

<span data-ttu-id="c8c9b-1853">Questo servizio arresta l'istanza del server HTTP create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1853">This service stops the previously create HTTP Server instance.</span></span> <span data-ttu-id="c8c9b-1854">Questa routine deve essere chiamata prima di eliminare un'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1854">This routine should be called prior to deleting an HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1855">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1855">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1856">**http_server_ptr** Puntatore all'istanza del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1856">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1857">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1857">Return Values</span></span>

- <span data-ttu-id="c8c9b-1858">Interruzione del server HTTP riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1858">**NX_SUCCESS** (0x00) Successful HTTP Server Stop</span></span>
- <span data-ttu-id="c8c9b-1859">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1859">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1860">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1860">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1861">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1861">Allowed From</span></span>

<span data-ttu-id="c8c9b-1862">Thread</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1862">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1863">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1863">Example</span></span>

```C
/* Stop the HTTP Server instance "my_server." */
status = nx_web_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_web_http_server_type_get"></a><span data-ttu-id="c8c9b-1864">nx_web_http_server_type_get</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1864">nx_web_http_server_type_get</span></span>

<span data-ttu-id="c8c9b-1865">Estrai il tipo di file dalla richiesta HTTP client</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1865">Extract file type from Client HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1866">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1866">Prototype</span></span>

```C
UINT nx_web_http_server_type_get(NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *name, CHAR *http_type_string,
    UINT *string_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1867">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1867">Description</span></span>

> [!NOTE]
> <span data-ttu-id="c8c9b-1868">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1868">This service is deprecated.</span></span> <span data-ttu-id="c8c9b-1869">Gli utenti sono invitati a usare il servizio *nx_web_http_server_type_get_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1869">Users are encouraged to use the service *nx_web_http_server_type_get_extended()*.</span></span>

<span data-ttu-id="c8c9b-1870">Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la relativa lunghezza in *string_size* dal *nome* del buffer di input, in genere l'URL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1870">This service extracts the HTTP request type in the buffer *http_type_string* and its length in *string_size* from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="c8c9b-1871">Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene impostato il tipo "text/plain".</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1871">If no MIME map is found, it defaults to the "text/plain" type.</span></span> <span data-ttu-id="c8c9b-1872">In caso contrario, confronta il tipo Estratto con le mappe MIME predefinite del server HTTP per una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1872">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="c8c9b-1873">Le mappe MIME predefinite nel server HTTP Web NetX sono:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1873">The default MIME maps in NetX Web HTTP Server are:</span></span>

- <span data-ttu-id="c8c9b-1874">testo HTML/HTML</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1874">html text/html</span></span>
- <span data-ttu-id="c8c9b-1875">testo htm/html</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1875">htm text/html</span></span>
- <span data-ttu-id="c8c9b-1876">testo txt/normale</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1876">txt text/plain</span></span>
- <span data-ttu-id="c8c9b-1877">immagine gif/gif</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1877">gif image/gif</span></span>
- <span data-ttu-id="c8c9b-1878">immagine jpg/jpeg</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1878">jpg image/jpeg</span></span>
- <span data-ttu-id="c8c9b-1879">icona immagine ICO/x</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1879">ico image/x-icon</span></span>

<span data-ttu-id="c8c9b-1880">Se specificato, verrà inoltre cercato un set definito dall'utente di mappe MIME aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1880">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="c8c9b-1881">Per ulteriori informazioni sulle mappe definite dall'utente, vedere *nx_web_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1881">See *nx_web_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1882">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1882">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1883">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1883">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8c9b-1884">**nome** Puntatore al buffer in cui eseguire la ricerca</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1884">**name** Pointer to buffer to search</span></span>
- <span data-ttu-id="c8c9b-1885">**http_type_string** Puntatore alla stringa di tipo HTML estratta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1885">**http_type_string** Pointer to extracted HTML type string</span></span>
- <span data-ttu-id="c8c9b-1886">**string_size** Puntatore per restituire la lunghezza della stringa di tipo HTML estratta.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1886">**string_size** Pointer to return extracted HTML type string length.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1887">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1887">Return Values</span></span>

- <span data-ttu-id="c8c9b-1888">Estrazione del tipo da **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1888">**NX_SUCCESS** (0x00) Successful extraction of type</span></span>
- <span data-ttu-id="c8c9b-1889">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1889">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1890">**NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0X30019) valore predefinito "text/plain" restituito.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1890">**NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) Default "text/plain" returned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1891">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1891">Allowed From</span></span>

<span data-ttu-id="c8c9b-1892">Applicazione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1892">Application</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1893">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1893">Example</span></span>

```C
/* my_server is a previously created HTTP server, which starts accepting client
    requests when *nx_web_http_server_start* is called */

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
string_length = nx_web_http_server_type_get(&my_server_ptr,
    my_server.nx_web_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
    For a more detailed example, see the description for
    *nx_web_http_server_callback_generate_response_header().*
```

## <a name="nx_web_http_server_type_get_extended"></a><span data-ttu-id="c8c9b-1894">nx_web_http_server_type_get_extended</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1894">nx_web_http_server_type_get_extended</span></span>

<span data-ttu-id="c8c9b-1895">Estrai il tipo di file dalla richiesta HTTP client</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1895">Extract file type from Client HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1896">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1896">Prototype</span></span>

```C
UINT nx_web_http_server_type_get_extended(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *name, UINT name_length,
    CHAR *http_type_string,
    UINT http_type_string_max_size,
    UINT *string_size);
```

### <a name="description"></a><span data-ttu-id="c8c9b-1897">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1897">Description</span></span>

<span data-ttu-id="c8c9b-1898">Questo servizio estrae il tipo di richiesta HTTP nel buffer *http_type_string* e la relativa lunghezza in *string_size* dal *nome* del buffer di input, in genere l'URL.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1898">This service extracts the HTTP request type in the buffer *http_type_string* and its length in *string_size* from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="c8c9b-1899">Se non viene trovata alcuna mappa MIME, per impostazione predefinita viene impostato il tipo "text/plain".</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1899">If no MIME map is found, it defaults to the "text/plain" type.</span></span> <span data-ttu-id="c8c9b-1900">In caso contrario, confronta il tipo Estratto con le mappe MIME predefinite del server HTTP per una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1900">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="c8c9b-1901">Le mappe MIME predefinite nel server HTTP Web NetX sono:</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1901">The default MIME maps in NetX Web HTTP Server are:</span></span>

- <span data-ttu-id="c8c9b-1902">testo HTML/HTML</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1902">html text/html</span></span>
- <span data-ttu-id="c8c9b-1903">testo htm/html</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1903">htm text/html</span></span>
- <span data-ttu-id="c8c9b-1904">testo txt/normale</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1904">txt text/plain</span></span>
- <span data-ttu-id="c8c9b-1905">immagine gif/gif</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1905">gif image/gif</span></span>
- <span data-ttu-id="c8c9b-1906">immagine jpg/jpeg</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1906">jpg image/jpeg</span></span>
- <span data-ttu-id="c8c9b-1907">icona immagine ICO/x</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1907">ico image/x-icon</span></span>

<span data-ttu-id="c8c9b-1908">Se specificato, verrà inoltre cercato un set definito dall'utente di mappe MIME aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1908">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="c8c9b-1909">Per ulteriori informazioni sulle mappe definite dall'utente, vedere *nx_web_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1909">See *nx_web_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="c8c9b-1910">Questo servizio sostituisce *nx_web_http_server_type_get*().</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1910">This service replaces *nx_web_http_server_type_get*().</span></span> <span data-ttu-id="c8c9b-1911">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza alla funzione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1911">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1912">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1912">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1913">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1913">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8c9b-1914">**nome** Puntatore al buffer in cui eseguire la ricerca</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1914">**name** Pointer to buffer to search</span></span>
- <span data-ttu-id="c8c9b-1915">**name_length** Lunghezza del nome</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1915">**name_length** Length of name</span></span>
- <span data-ttu-id="c8c9b-1916">**http_type_string** Puntatore alla stringa di tipo HTML estratta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1916">**http_type_string** Pointer to extracted HTML type string</span></span>
- <span data-ttu-id="c8c9b-1917">**http_type_string_max_size** Dimensioni del buffer di http_type_string</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1917">**http_type_string_max_size** Size of the http_type_string buffer size</span></span>
- <span data-ttu-id="c8c9b-1918">**string_size** Puntatore per restituire la stringa di tipo HTML estratta</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1918">**string_size** Pointer to return extracted HTML type string</span></span>

<span data-ttu-id="c8c9b-1919">lunghezza.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1919">length.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1920">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1920">Return Values</span></span>

- <span data-ttu-id="c8c9b-1921">Estrazione del tipo da **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1921">**NX_SUCCESS** (0x00) Successful extraction of type</span></span>
- <span data-ttu-id="c8c9b-1922">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1922">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1923">**NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0X30019) valore predefinito "text/plain" restituito.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1923">**NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) Default "text/plain" returned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1924">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1924">Allowed From</span></span>

<span data-ttu-id="c8c9b-1925">Applicazione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1925">Application</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1926">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1926">Example</span></span>

```C
/* my_server is a previously created HTTP server, which starts accepting client
    requests when *nx_web_http_server_start* is called */

CHAR temp_string[20];
UINT string_length;
UINT ret;

/* Extract the HTTP type. */
ret = nx_web_http_server_type_get_extended(&my_server_ptr,
    my_server.nx_web_http_server_request_resource,
    strlen(my_server.nx_web_http_server_request_resource),
    temp_string,sizeof(temp_string), &string_length);

/* If string_length is non zero, the HTTP string is extracted. */
    For a more detailed example, see the description for
    *nx_web_http_server_callback_generate_response_header().*
```

## <a name="nx_web_http_server_digest_authenticate_notify_set"></a><span data-ttu-id="c8c9b-1927">nx_web_http_server_digest_authenticate_notify_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1927">nx_web_http_server_digest_authenticate_notify_set</span></span>

<span data-ttu-id="c8c9b-1928">Imposta funzione di callback autenticazione digest</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1928">Set digest authenticate callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1929">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1929">Prototype</span></span>

```C
UINT nx_web_http_server_digest_authenticate_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*digest_authenticate_callback)(NX_WEB_HTTP_SERVER *server_ptr,
        CHAR *name_ptr,
        CHAR *realm_ptr,
        CHAR *password_ptr,
        CHAR *method,
        CHAR *authorization_uri,
        CHAR *authorization_nc,
        CHAR *authorization_cnonce));
```

### <a name="description"></a><span data-ttu-id="c8c9b-1930">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1930">Description</span></span>

<span data-ttu-id="c8c9b-1931">Questo servizio imposta il callback richiamato quando viene eseguita l'autenticazione del digest.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1931">This service sets the callback invoked when digest authenticate is performed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1932">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1932">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1933">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1933">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8c9b-1934">**digest_authenticate_callback** Puntatore al callback di autenticazione del digest</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1934">**digest_authenticate_callback** Pointer to digest authenticate callback</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1935">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1935">Return Values</span></span>

- <span data-ttu-id="c8c9b-1936">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1936">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8c9b-1937">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1937">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8c9b-1938">Autenticazione del digest NX_NOT_SUPPORTED (0x4B) non abilitata</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1938">NX_NOT_SUPPORTED (0x4B) Digest authenticate not enabled</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1939">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1939">Allowed From</span></span>

<span data-ttu-id="c8c9b-1940">Applicazione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1940">Application</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1941">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1941">Example</span></span>

```C
UINT digest_authenticate_callback(NX_WEB_HTTP_SERVER *server_ptr, CHAR *name_ptr,
    CHAR *realm_ptr, CHAR *password_ptr, CHAR *method,
    CHAR *authorization_uri, CHAR *authorization_nc,
    CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_WEB_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_web_http_server_create, and
    before starting HTTP services when nx_web_http_server_start is called, set the digest authenticate callback: */
status = nx_web_http_server_digest_authenticate_notify_set(&my_server,
    digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
    will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_web_http_server_authenticate_check_set"></a><span data-ttu-id="c8c9b-1942">nx_web_http_server_authenticate_check_set</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1942">nx_web_http_server_authenticate_check_set</span></span>

<span data-ttu-id="c8c9b-1943">Imposta funzione di callback autenticazione digest</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1943">Set digest authenticate callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8c9b-1944">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1944">Prototype</span></span>

```C
UINT nx_web_http_server_digest_authenticate_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*authentication_check_extended)(
        NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type,
        CHAR *resource,
        CHAR **name,
        UINT *name_length,
        CHAR **password,
        UINT password_length,
        CHAR **realm,
        UINT *realm_length));
```

### <a name="description"></a><span data-ttu-id="c8c9b-1945">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1945">Description</span></span>

<span data-ttu-id="c8c9b-1946">Questo servizio imposta il callback richiamato quando viene eseguito il controllo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1946">This service sets the callback invoked when authenticate check is performed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8c9b-1947">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1947">Input Parameters</span></span>

- <span data-ttu-id="c8c9b-1948">**http_server_ptr** Puntatore all'istanza del server HTTP</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1948">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8c9b-1949">**authenticate_check_externded** Puntatore per autenticare il callback del controllo</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1949">**authenticate_check_externded** Pointer to authenticate check callback</span></span>

### <a name="return-values"></a><span data-ttu-id="c8c9b-1950">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1950">Return Values</span></span>

- <span data-ttu-id="c8c9b-1951">**NX_SUCCESS** (0x00) ha impostato correttamente il callback</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1951">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8c9b-1952">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1952">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8c9b-1953">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1953">Allowed From</span></span>

<span data-ttu-id="c8c9b-1954">Applicazione</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1954">Application</span></span>

### <a name="example"></a><span data-ttu-id="c8c9b-1955">Esempio</span><span class="sxs-lookup"><span data-stu-id="c8c9b-1955">Example</span></span>

```C
UINT authenticate_check_callback(NX_WEB_HTTP_SERVER *server_ptr,
    UINT request_type,
    CHAR *name_ptr, UCHAR *resource, UCHAR **name,
    UINT *name_length, UCHAR **password,
    UINT *password_length, UCHAR **realm,
    UINT *realm_length)
{
    *name = "name";
    *name_length = 4;
    *password = "password";
    *password_length = 8;
    *realm = "realm";
    *realm_length = 5;
    return(NX_SUCCESS);
}

NX_WEB_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_web_http_server_create, and
    before starting HTTP services when nx_web_http_server_start is called, set the authenticate check callback: */

status = nx_web_http_digest_authenticate_check_set (&my_server,
    authenticate_check_callback);

/* If status equals NX_SUCCESS, the authenticate_check_callback function
    will be called when the HTTP server performs authenticate check. */
```
