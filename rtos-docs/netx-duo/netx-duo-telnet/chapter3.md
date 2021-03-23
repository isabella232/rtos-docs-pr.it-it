---
title: Capitolo 3-Descrizione dei servizi Telnet di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi Telnet di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 991ec53aaba052b4f42da6e5a541151953121e76
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821617"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-telnet-services"></a><span data-ttu-id="07270-103">Capitolo 3-Descrizione dei servizi Telnet di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="07270-103">Chapter 3 - Description of Azure RTOS NetX Duo Telnet services</span></span>

<span data-ttu-id="07270-104">Questo capitolo contiene una descrizione di tutti i servizi Telnet di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="07270-104">This chapter contains a description of all Azure RTOS NetX Duo Telnet Services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="07270-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="07270-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="07270-106">**nx_telnet_client_connect**: *connettere un client Telnet con indirizzo IPv4*</span><span class="sxs-lookup"><span data-stu-id="07270-106">**nx_telnet_client_connect**: *Connect a Telnet Client with IPv4 address*</span></span>
- <span data-ttu-id="07270-107">**nxd_telnet_client_connect**: *connettere un client Telnet IPv6 con indirizzo IPv6*</span><span class="sxs-lookup"><span data-stu-id="07270-107">**nxd_telnet_client_connect**: *Connect an IPv6 Telnet Client with IPv6 address*</span></span>
- <span data-ttu-id="07270-108">**nx_telnet_client_create**: *creare un client Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-108">**nx_telnet_client_create**: *Create a Telnet Client*</span></span>
- <span data-ttu-id="07270-109">**nx_telnet_client_delete**: *eliminare un client Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-109">**nx_telnet_client_delete**: *Delete a Telnet Client*</span></span>
- <span data-ttu-id="07270-110">**nx_telnet_client_disconnect**: *disconnettere un client Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-110">**nx_telnet_client_disconnect**: *Disconnect a Telnet Client*</span></span>
- <span data-ttu-id="07270-111">**nx_telnet_client_packet_receive**: *ricevere il pacchetto tramite il client Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-111">**nx_telnet_client_packet_receive**: *Receive packet via Telnet Client*</span></span>
- <span data-ttu-id="07270-112">**nx_telnet_client_packet_send**: *inviare il pacchetto tramite il client Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-112">**nx_telnet_client_packet_send**: *Send packet via Telnet Client*</span></span>
- <span data-ttu-id="07270-113">**nx_telnet_server_create**: *creare un server Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-113">**nx_telnet_server_create**: *Create a Telnet Server*</span></span>
- <span data-ttu-id="07270-114">**nx_telnet_server_delete**: *eliminare un server Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-114">**nx_telnet_server_delete**: *Delete a Telnet Server*</span></span>
- <span data-ttu-id="07270-115">**nx_telnet_server_disconnect**: *disconnettere un client Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-115">**nx_telnet_server_disconnect**: *Disconnect a Telnet Client*</span></span>
- <span data-ttu-id="07270-116">**nx_telnet_server_get_open_connection_count**: *recuperare il numero di connessioni aperte*</span><span class="sxs-lookup"><span data-stu-id="07270-116">**nx_telnet_server_get_open_connection_count**: *Retrieve the number of open connections*</span></span>
- <span data-ttu-id="07270-117">**nx_telnet_server_packet_send**: *inviare il pacchetto tramite la connessione client*</span><span class="sxs-lookup"><span data-stu-id="07270-117">**nx_telnet_server_packet_send**: *Send packet through Client connection*</span></span>
- <span data-ttu-id="07270-118">**nx_telnet_server_packet_pool_set**: *impostare pool di pacchetti come pool di pacchetti del server Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-118">**nx_telnet_server_packet_pool_set**: *Set packet pool as Telnet Server packet pool*</span></span>
- <span data-ttu-id="07270-119">**nx_telnet_server_start**: *avviare un server Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-119">**nx_telnet_server_start**: *Start a Telnet Server*</span></span>
- <span data-ttu-id="07270-120">**nx_telnet_server_stop**: *arrestare un server Telnet*</span><span class="sxs-lookup"><span data-stu-id="07270-120">**nx_telnet_server_stop**: *Stop a Telnet Server*</span></span>

## <a name="nx_telnet_client_connect"></a><span data-ttu-id="07270-121">nx_telnet_client_connect</span><span class="sxs-lookup"><span data-stu-id="07270-121">nx_telnet_client_connect</span></span>

<span data-ttu-id="07270-122">Connettere un client Telnet con indirizzo IPv4</span><span class="sxs-lookup"><span data-stu-id="07270-122">Connect a Telnet Client with IPv4 address</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-123">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-123">Prototype</span></span>

```c
UINT nx_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                              ULONG server_ip, UINT server_port, 
                              ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="07270-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-124">Description</span></span>

<span data-ttu-id="07270-125">Questo servizio tenta di connettere l'istanza del client Telnet creata in precedenza al server sull'IP e sulla porta specificati usando un indirizzo IPv4 per il server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-125">This service attempts to connect the previously created Telnet Client instance to the Server at the specified IP and port using an IPv4 address for the Telnet Server.</span></span> <span data-ttu-id="07270-126">Questo servizio inserisce effettivamente l'indirizzo IP del server ULONG in un blocco di controllo NXD_ADDRESS e imposta la versione IP su 4 prima di chiamare il servizio *nxd_telnet_client_connect* descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="07270-126">This service actually inserts the ULONG server IP address in an NXD_ADDRESS control block and sets the IP version to 4 before calling the *nxd_telnet_client_connect* service described below.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-127">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-127">Input Parameters</span></span>

- <span data-ttu-id="07270-128">**client_ptr**: puntatore al blocco di controllo client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-128">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="07270-129">**server_ip**: indirizzo IPv4 del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-129">**server_ip**: IPv4 Address of the Telnet Server.</span></span>
- <span data-ttu-id="07270-130">**SERVER_PORT**: porta TCP del server (il server Telnet è la porta 23).</span><span class="sxs-lookup"><span data-stu-id="07270-130">**server_port**: TCP Port of Server (Telnet Server is port 23).</span></span>
- <span data-ttu-id="07270-131">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la connessione del client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-131">**wait_option**: Defines how long the service will wait for the Telnet Client connect.</span></span> <span data-ttu-id="07270-132">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="07270-132">The wait options are defined as follows:</span></span>

    - <span data-ttu-id="07270-133">**valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-133">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="07270-134">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="07270-134">**TX_WAIT_FOREVER**: (0xFFFFFFFF)Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-135">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-135">Return Values</span></span>

- <span data-ttu-id="07270-136">**NX_SUCCESS**: (0x00) connessione client riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-136">**NX_SUCCESS**: (0x00) Successful Client connect.</span></span>
- <span data-ttu-id="07270-137">**NX_TELNET_NOT_DISCONNECTED**: (0XF4) client già connesso.</span><span class="sxs-lookup"><span data-stu-id="07270-137">**NX_TELNET_NOT_DISCONNECTED**: (0xF4) Client already connected.</span></span>
- <span data-ttu-id="07270-138">NX_PTR_ERROR: (0x07) puntatore client non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-138">NX_PTR_ERROR: (0x07) Invalid Client pointer.</span></span>
- <span data-ttu-id="07270-139">NX_IP_ADDRESS_ERROR: (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-139">NX_IP_ADDRESS_ERROR: (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="07270-140">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-140">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-141">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-141">Allowed From</span></span>

<span data-ttu-id="07270-142">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-142">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-143">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-143">Example</span></span>

```c
/* Connect the Telnet Client instance “my_client” to the Server at 
   IP address 1.2.3.4 and port 23.  */
status =  nx_telnet_client_connect(&my_client, IP_ADDRESS(1,2,3,4), 23, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   connected to the Telnet Server.  */
```

## <a name="nxd_telnet_client_connect"></a><span data-ttu-id="07270-144">nxd_telnet_client_connect</span><span class="sxs-lookup"><span data-stu-id="07270-144">nxd_telnet_client_connect</span></span>

<span data-ttu-id="07270-145">Connettere un client Telnet con indirizzo IPv6 o IPv4</span><span class="sxs-lookup"><span data-stu-id="07270-145">Connect a Telnet Client with IPv6 or IPv4 address</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-146">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-146">Prototype</span></span>

```c
UINT nxd_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                               NXD_ADDRESS *server_ip_address, 
                               UINT server_port, 
                               ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="07270-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-147">Description</span></span>

<span data-ttu-id="07270-148">Questo servizio tenta di connettere l'istanza del client Telnet creata in precedenza al server con l'indirizzo IP e la porta specificati utilizzando l'indirizzo IPv6 del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-148">This service attempts to connect the previously created Telnet Client instance to the Server at the specified IP and port using the Telnet Server’s IPv6 address.</span></span> <span data-ttu-id="07270-149">Questo servizio può assumere un indirizzo IPv4 o IPv6, ma deve essere contenuto nella variabile NXD_ADDRESS *server_ip_address.*</span><span class="sxs-lookup"><span data-stu-id="07270-149">This service can take an IPv4 or an IPv6 address but must be contained in the NXD_ADDRESS variable *server_ip_address.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-150">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-150">Input Parameters</span></span>

- <span data-ttu-id="07270-151">**client_ptr**: puntatore al blocco di controllo client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-151">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="07270-152">**server_ip_address**: indirizzo IP del server.</span><span class="sxs-lookup"><span data-stu-id="07270-152">**server_ip_address**: IP Address of Server.</span></span>
- <span data-ttu-id="07270-153">**SERVER_PORT**: porta TCP del server (il server Telnet è la porta 23).</span><span class="sxs-lookup"><span data-stu-id="07270-153">**server_port**: TCP Port of Server (Telnet Server is port 23).</span></span>
- <span data-ttu-id="07270-154">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la connessione del client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-154">**wait_option**: Defines how long the service will wait for the Telnet Client connect.</span></span> <span data-ttu-id="07270-155">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="07270-155">The wait options are defined as follows:</span></span>

    - <span data-ttu-id="07270-156">**valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-156">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="07270-157">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="07270-157">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-158">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-158">Return Values</span></span>

- <span data-ttu-id="07270-159">**NX_SUCCESS**: (0x00) connessione client riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-159">**NX_SUCCESS**: (0x00) Successful Client connect.</span></span>
- <span data-ttu-id="07270-160">**NX_TELNET_ERROR**: (0xF0) errore di connessione del client.</span><span class="sxs-lookup"><span data-stu-id="07270-160">**NX_TELNET_ERROR**: (0xF0) Client connect error.</span></span>
- <span data-ttu-id="07270-161">**NX_TELNET_NOT_DISCONNECTED**: (0XF4) client già connesso.</span><span class="sxs-lookup"><span data-stu-id="07270-161">**NX_TELNET_NOT_DISCONNECTED**: (0xF4) Client already connected.</span></span>
- <span data-ttu-id="07270-162">NX_PTR_ERROR: (0x07) puntatore client non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-162">NX_PTR_ERROR: (0x07) Invalid Client pointer.</span></span>
- <span data-ttu-id="07270-163">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-163">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="07270-164">NX_TELNET_INVALID_PARAMETER: (0xF5) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="07270-164">NX_TELNET_INVALID_PARAMETER: (0xF5) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-165">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-165">Allowed From</span></span>

<span data-ttu-id="07270-166">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-166">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-167">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-167">Example</span></span>

```c
/* Connect the Telnet Client instance “my_client” to the Server at 
   IPv6 address 20010db1:0:f101::101 and port 23.  */
status =  nxd_telnet_client_connect(&my_client, &server_ip_address, 23, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   connected to the Telnet Server.  */
```

## <a name="nx_telnet_client_create"></a><span data-ttu-id="07270-168">nx_telnet_client_create</span><span class="sxs-lookup"><span data-stu-id="07270-168">nx_telnet_client_create</span></span>

<span data-ttu-id="07270-169">Creazione di un client Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-169">Create a Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-170">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-170">Prototype</span></span>

```c
UINT nx_telnet_client_create(NX_TELNET_CLIENT *client_ptr, 
                             CHAR *client_name, NX_IP *ip_ptr, 
                             ULONG window_size);
```

### <a name="description"></a><span data-ttu-id="07270-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-171">Description</span></span>

<span data-ttu-id="07270-172">Questo servizio crea un'istanza del client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-172">This service creates a Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-173">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-173">Input Parameters</span></span>

- <span data-ttu-id="07270-174">**client_ptr**: puntatore al blocco di controllo client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-174">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="07270-175">**client_name**: nome dell'istanza del client.</span><span class="sxs-lookup"><span data-stu-id="07270-175">**client_name**: Name of Client instance.</span></span>
- <span data-ttu-id="07270-176">**ip_ptr**: puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="07270-176">**ip_ptr**: Pointer to IP instance.</span></span>
- <span data-ttu-id="07270-177">**window_size**: dimensioni della finestra di ricezione TCP per il client.</span><span class="sxs-lookup"><span data-stu-id="07270-177">**window_size**: Size of TCP receive window for this Client.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-178">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-178">Return Values</span></span>

- <span data-ttu-id="07270-179">**NX_SUCCESS**: (0x00) creazione client riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-179">**NX_SUCCESS**: (0x00) Successful Client create.</span></span>
- <span data-ttu-id="07270-180">**NX_TELNET_ERROR**: (0xF0) socket crea errore.</span><span class="sxs-lookup"><span data-stu-id="07270-180">**NX_TELNET_ERROR**: (0xF0) Socket create error.</span></span>
- <span data-ttu-id="07270-181">NX_PTR_ERROR: (0x07) il puntatore IP o il client non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-181">NX_PTR_ERROR: (0x07) Invalid Client or IP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-182">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-182">Allowed From</span></span>

<span data-ttu-id="07270-183">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="07270-183">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-184">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-184">Example</span></span>

```c
/* Create the Telnet Client instance “my_client” on the IP instance “ip_0”.  */
status =  nx_telnet_client_create(&my_client, “My Telnet Client”, &ip_0, 2048);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   created.  */
```
## <a name="nx_telnet_client_delete"></a><span data-ttu-id="07270-185">nx_telnet_client_delete</span><span class="sxs-lookup"><span data-stu-id="07270-185">nx_telnet_client_delete</span></span>

<span data-ttu-id="07270-186">Eliminare un client Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-186">Delete a Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-187">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-187">Prototype</span></span>

```c
UINT nx_telnet_client_delete(NX_TELNET_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="07270-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-188">Description</span></span>

<span data-ttu-id="07270-189">Questo servizio Elimina un'istanza del client Telnet creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="07270-189">This service deletes a previously created Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-190">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-190">Input Parameters</span></span>

- <span data-ttu-id="07270-191">**client_ptr**: puntatore al blocco di controllo client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-191">**client_ptr**: Pointer to Telnet Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-192">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-192">Return Values</span></span>

- <span data-ttu-id="07270-193">**NX_SUCCESS**: (0x00) eliminazione client riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-193">**NX_SUCCESS**: (0x00) Successful Client delete.</span></span>
- <span data-ttu-id="07270-194">**NX_TELNET_NOT_DISCONNECTED**: (0xF4) il client è ancora connesso.</span><span class="sxs-lookup"><span data-stu-id="07270-194">**NX_TELNET_NOT_DISCONNECTED**: (0xF4) Client still connected.</span></span>
- <span data-ttu-id="07270-195">NX_PTR_ERROR: (0x07) puntatore client non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-195">NX_PTR_ERROR: (0x07) Invalid Client pointer.</span></span>
- <span data-ttu-id="07270-196">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-196">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-197">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-197">Allowed From</span></span>

<span data-ttu-id="07270-198">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-198">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-199">Example</span></span>

```c
/* Delete the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_delete(&my_client);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   deleted.  */
```

## <a name="nx_telnet_client_disconnect"></a><span data-ttu-id="07270-200">nx_telnet_client_disconnect</span><span class="sxs-lookup"><span data-stu-id="07270-200">nx_telnet_client_disconnect</span></span>

<span data-ttu-id="07270-201">Disconnettere un client Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-201">Disconnect a Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-202">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-202">Prototype</span></span>

```c
UINT nx_telnet_client_disconnect(NX_TELNET_CLIENT *client_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="07270-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-203">Description</span></span>

<span data-ttu-id="07270-204">Questo servizio disconnette un'istanza del client Telnet connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="07270-204">This service disconnects a previously connected Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-205">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-205">Input Parameters</span></span>

- <span data-ttu-id="07270-206">**client_ptr**: puntatore al blocco di controllo client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-206">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="07270-207">**WAIT_OPTION**: definisce per quanto tempo il servizio attenderà la disconnessione del client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-207">**wait_option**: Defines how long the service will wait for the Telnet Client disconnect.</span></span> <span data-ttu-id="07270-208">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="07270-208">The wait options are defined as follows:</span></span>

    - <span data-ttu-id="07270-209">**valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-209">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="07270-210">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="07270-210">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-211">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-211">Return Values</span></span>

- <span data-ttu-id="07270-212">**NX_SUCCESS**: (0x00) la disconnessione del client è riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-212">**NX_SUCCESS**: (0x00) Successful Client disconnect.</span></span>
- <span data-ttu-id="07270-213">**NX_TELNET_NOT_CONNECTED**: (0XF3) client non connesso.</span><span class="sxs-lookup"><span data-stu-id="07270-213">**NX_TELNET_NOT_CONNECTED**: (0xF3) Client not connected.</span></span>
- <span data-ttu-id="07270-214">NX_PTR_ERROR: (0x07) puntatore client non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-214">NX_PTR_ERROR: (0x07) Invalid Client pointer.</span></span>
- <span data-ttu-id="07270-215">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-215">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="07270-216">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-216">Allowed From</span></span>

<span data-ttu-id="07270-217">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-217">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-218">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-218">Example</span></span>

```c

/* Disconnect the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_disconnect(&my_client, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   disconnected.  */
```

## <a name="nx_telnet_client_packet_receive"></a><span data-ttu-id="07270-219">nx_telnet_client_packet_receive</span><span class="sxs-lookup"><span data-stu-id="07270-219">nx_telnet_client_packet_receive</span></span>

<span data-ttu-id="07270-220">Ricevi pacchetto tramite client Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-220">Receive packet via Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-221">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-221">Prototype</span></span>

```c
UINT nx_telnet_client_packet_receive(NX_TELNET_CLIENT *client_ptr, 
                                     NX_PACKET **packet_ptr, 
                                     ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="07270-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-222">Description</span></span>

<span data-ttu-id="07270-223">Questo servizio riceve un pacchetto dall'istanza del client Telnet connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="07270-223">This service receives a packet from the previously connected Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-224">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-224">Input Parameters</span></span>

- <span data-ttu-id="07270-225">**client_ptr**: puntatore al blocco di controllo client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-225">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="07270-226">**packet_ptr**: puntatore alla destinazione per il pacchetto ricevuto.</span><span class="sxs-lookup"><span data-stu-id="07270-226">**packet_ptr**: Pointer to the destination for the received packet.</span></span>
- <span data-ttu-id="07270-227">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la ricezione del pacchetto client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-227">**wait_option**: Defines how long the service will wait for the Telnet Client packet receive.</span></span> <span data-ttu-id="07270-228">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="07270-228">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="07270-229">**valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-229">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="07270-230">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="07270-230">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-231">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-231">Return Values</span></span>

- <span data-ttu-id="07270-232">**NX_SUCCESS**: (0x00) la ricezione di pacchetti client è riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-232">**NX_SUCCESS**: (0x00) Successful Client packet receive.</span></span>
- <span data-ttu-id="07270-233">NX_PTR_ERROR: (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="07270-233">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="07270-234">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-234">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-235">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-235">Allowed From</span></span>

<span data-ttu-id="07270-236">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-236">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-237">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-237">Example</span></span>

```c

/* Receive a packet from the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 100);

/* If status is NX_SUCCESS the “my_packet” pointer contains data received from
   the Telnet Client connection.  */
```
## <a name="nx_telnet_client_packet_send"></a><span data-ttu-id="07270-238">nx_telnet_client_packet_send</span><span class="sxs-lookup"><span data-stu-id="07270-238">nx_telnet_client_packet_send</span></span>

<span data-ttu-id="07270-239">Invia pacchetto tramite client Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-239">Send packet via Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-240">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-240">Prototype</span></span>

```c
UINT nx_telnet_client_packet_send(NX_TELNET_CLIENT *client_ptr, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="07270-241">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-241">Description</span></span>

<span data-ttu-id="07270-242">Questo servizio invia un pacchetto tramite l'istanza del client Telnet connessa in precedenza.</span><span class="sxs-lookup"><span data-stu-id="07270-242">This service sends a packet through the previously connected Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-243">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-243">Input Parameters</span></span>

- <span data-ttu-id="07270-244">**client_ptr**: puntatore al blocco di controllo client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-244">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="07270-245">**packet_ptr**: puntatore al pacchetto da inviare.</span><span class="sxs-lookup"><span data-stu-id="07270-245">**packet_ptr**: Pointer to the packet to send.</span></span>
- <span data-ttu-id="07270-246">**WAIT_OPTION**: definisce il tempo di attesa del servizio per l'invio del pacchetto del client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-246">**wait_option**: Defines how long the service will wait for the Telnet Client packet send.</span></span> <span data-ttu-id="07270-247">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="07270-247">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="07270-248">**valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-248">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="07270-249">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="07270-249">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-250">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-250">Return Values</span></span>

- <span data-ttu-id="07270-251">**NX_SUCCESS**: (0x00) la trasmissione di pacchetti client è riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-251">**NX_SUCCESS**: (0x00) Successful Client packet send.</span></span>
- <span data-ttu-id="07270-252">**NX_TELNET_ERROR**: (0xF0) Impossibile inviare il pacchetto. il chiamante è responsabile del rilascio del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="07270-252">**NX_TELNET_ERROR**: (0xF0) Send packet failed – caller is responsible for releasing the packet.</span></span>
- <span data-ttu-id="07270-253">NX_PTR_ERROR: (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="07270-253">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="07270-254">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-254">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-255">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-255">Allowed From</span></span>

<span data-ttu-id="07270-256">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-256">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-257">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-257">Example</span></span>

```c
/* Send a packet via the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_send(&my_client, my_packet, 100);
/* If status is NX_SUCCESS the packet was successfully sent.  */

```

## <a name="nx_telnet_server_create"></a><span data-ttu-id="07270-258">nx_telnet_server_create</span><span class="sxs-lookup"><span data-stu-id="07270-258">nx_telnet_server_create</span></span>

<span data-ttu-id="07270-259">Creazione di un server Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-259">Create a Telnet Server</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-260">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-260">Prototype</span></span>

```c
UINT nx_telnet_server_create(NX_TELNET_SERVER *server_ptr, CHAR *server_name, NX_IP *ip_ptr, 
                             VOID *stack_ptr, ULONG stack_size, 
                             void (*new_connection)(struct NX_TELNET_SERVER_STRUCT*telnet_server_ptr, 
                                                    UINT logical_connection), 
                             void (*receive_data)(struct NX_TELNET_SERVER_STRUCT *telnet_server_ptr, 
                                                  UINT logical_connection, NX_PACKET *packet_ptr), 
                             void (*connection_end)(struct NX_TELNET_SERVER_STRUCT *telnet_server_ptr, 
                                                    UINT logical_connection));

```

### <a name="description"></a><span data-ttu-id="07270-261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-261">Description</span></span>

<span data-ttu-id="07270-262">Questo servizio crea un'istanza del server Telnet nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="07270-262">This service creates a Telnet Server instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-263">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-263">Input Parameters</span></span>

- <span data-ttu-id="07270-264">**server_ptr**: puntatore al blocco di controllo del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-264">**server_ptr**: Pointer to Telnet Server control block.</span></span>
- <span data-ttu-id="07270-265">**server_name**: nome dell'istanza del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-265">**server_name**: Name of Telnet Server instance.</span></span>
- <span data-ttu-id="07270-266">**ip_ptr**: puntatore all'istanza IP associata.</span><span class="sxs-lookup"><span data-stu-id="07270-266">**ip_ptr**: Pointer to associated IP instance.</span></span>
- <span data-ttu-id="07270-267">**stack_ptr**: puntatore allo stack per il thread del server interno.</span><span class="sxs-lookup"><span data-stu-id="07270-267">**stack_ptr**: Pointer to stack for the internal Server thread.</span></span>
- <span data-ttu-id="07270-268">**sack_size**: dimensioni in byte dello stack.</span><span class="sxs-lookup"><span data-stu-id="07270-268">**sack_size**: Size of the stack, in bytes.</span></span>
- <span data-ttu-id="07270-269">**new_connection**: puntatore alla funzione di routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07270-269">**new_connection**: Application callback routine function pointer.</span></span> <span data-ttu-id="07270-270">Questa routine viene chiamata ogni volta che il server rileva una nuova richiesta di connessione del client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-270">This routine is called whenever a new Telnet Client connection request is detected by the Server.</span></span>
- <span data-ttu-id="07270-271">**receive_data**: puntatore alla funzione di routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07270-271">**receive_data**: Application callback routine function pointer.</span></span> <span data-ttu-id="07270-272">Questa routine viene chiamata ogni volta che nella connessione sono presenti nuovi dati del client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-272">This routine is called whenever a new Telnet Client data is present on the connection.</span></span> <span data-ttu-id="07270-273">Questa routine è responsabile del rilascio del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="07270-273">This routine is responsible for releasing the packet.</span></span>
- <span data-ttu-id="07270-274">**end_connection**: puntatore alla funzione di routine di callback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07270-274">**end_connection**: Application callback routine function pointer.</span></span> <span data-ttu-id="07270-275">Questa routine viene chiamata ogni volta che una connessione client Telnet viene disconnessa dal client o si verifica il timeout della connessione del client (scade il "timeout attività").</span><span class="sxs-lookup"><span data-stu-id="07270-275">This routine is called whenever a Telnet Client connection is disconnected by the Client or the Client connection times out (“activity timeout” expires).</span></span> <span data-ttu-id="07270-276">Il server può disconnettersi anche tramite il servizio *nx_telnet_server_disconnect* descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="07270-276">The Server can also disconnect via the *nx_telnet_server_disconnect* service described below.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-277">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-277">Return Values</span></span>

- <span data-ttu-id="07270-278">**NX_SUCCESS**: (0x00) la creazione del server è riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-278">**NX_SUCCESS**: (0x00) Successful Server create.</span></span>
- <span data-ttu-id="07270-279">NX_PTR_ERROR: (0x07) i puntatori a server, IP, stack o callback dell'applicazione non validi.</span><span class="sxs-lookup"><span data-stu-id="07270-279">NX_PTR_ERROR: (0x07) Invalid Server, IP, stack, or application callback pointers.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-280">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-280">Allowed From</span></span>

<span data-ttu-id="07270-281">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="07270-281">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-282">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-282">Example</span></span>

```c
/* Create a Telnet Server instance “my_server”.  */
status =  nx_telnet_server_create(&my_server, "Telnet Server", &ip_0, 
                                   pointer, 2048, telnet_new_connection, 
                                   telnet_receive_data, telnet_connection_end);


/* If status is NX_SUCCESS the Telnet Server was successfully created.  */
```
## <a name="nx_telnet_server_delete"></a><span data-ttu-id="07270-283">nx_telnet_server_delete</span><span class="sxs-lookup"><span data-stu-id="07270-283">nx_telnet_server_delete</span></span>

<span data-ttu-id="07270-284">Eliminare un server Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-284">Delete a Telnet Server</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-285">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-285">Prototype</span></span>

```c
UINT nx_telnet_server_delete(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="07270-286">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-286">Description</span></span>

<span data-ttu-id="07270-287">Questo servizio Elimina un'istanza del server Telnet creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="07270-287">This service deletes a previously created Telnet Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-288">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-288">Input Parameters</span></span>

- <span data-ttu-id="07270-289">**server_ptr**: puntatore al blocco di controllo del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-289">**server_ptr**: Pointer to Telnet Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-290">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-290">Return Values</span></span>

- <span data-ttu-id="07270-291">**NX_SUCCESS**: (0x00) eliminazione server riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-291">**NX_SUCCESS**: (0x00) Successful Server delete.</span></span>
- <span data-ttu-id="07270-292">NX_PTR_ERROR: (0x07) puntatore server non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-292">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="07270-293">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-293">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-294">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-294">Allowed From</span></span>

<span data-ttu-id="07270-295">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-295">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-296">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-296">Example</span></span>

```c
/* Delete the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_delete(&my_server);

/* If status is NX_SUCCESS the Telnet Server was successfully deleted.  */
```

## <a name="nx_telnet_server_disconnect"></a><span data-ttu-id="07270-297">nx_telnet_server_disconnect</span><span class="sxs-lookup"><span data-stu-id="07270-297">nx_telnet_server_disconnect</span></span>

<span data-ttu-id="07270-298">Disconnettere un client Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-298">Disconnect a Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-299">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-299">Prototype</span></span>

```c
UINT nx_telnet_server_disconnect(NX_TELNET_SERVER *server_ptr, UINT logical_connection);
```

### <a name="description"></a><span data-ttu-id="07270-300">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-300">Description</span></span>

<span data-ttu-id="07270-301">Questo servizio disconnette un client precedentemente connesso in questa istanza del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-301">This service disconnects a previously connected Client on this Telnet Server instance.</span></span> <span data-ttu-id="07270-302">Questa routine viene in genere chiamata dalla funzione di callback dei dati di ricezione dell'applicazione in risposta a una condizione rilevata nei dati ricevuti.</span><span class="sxs-lookup"><span data-stu-id="07270-302">This routine is typically called from the application’s receive data callback function in response to a condition detected in the data received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-303">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-303">Input Parameters</span></span>

- <span data-ttu-id="07270-304">**server_ptr**: puntatore al blocco di controllo del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-304">**server_ptr**: Pointer to Telnet Server control block.</span></span>
- <span data-ttu-id="07270-305">**logical_connection**: connessione logica corrispondente alla connessione client in questo server.</span><span class="sxs-lookup"><span data-stu-id="07270-305">**logical_connection**: Logical connection corresponding the Client connection on this Server.</span></span> <span data-ttu-id="07270-306">Il valore valido è compreso tra 0 e NX_TELENET_MAX_CLIENTS.</span><span class="sxs-lookup"><span data-stu-id="07270-306">Valid value range from 0 through NX_TELENET_MAX_CLIENTS.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-307">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-307">Return Values</span></span>

- <span data-ttu-id="07270-308">**NX_SUCCESS**: (0x00) la disconnessione del server è riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-308">**NX_SUCCESS**: (0x00) Successful Server disconnect.</span></span>
- <span data-ttu-id="07270-309">**NX_TELNET_ERROR**: la disconnessione del server (0xF0) non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-309">**NX_TELNET_ERROR**: (0xF0) Server disconnect failed.</span></span>
- <span data-ttu-id="07270-310">NX_OPTION_ERROR: (0x0A) connessione logica non valida.</span><span class="sxs-lookup"><span data-stu-id="07270-310">NX_OPTION_ERROR: (0x0A) Invalid logical connection.</span></span>
- <span data-ttu-id="07270-311">NX_PTR_ERROR: (0x07) puntatore server non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-311">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="07270-312">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-312">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-313">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-313">Allowed From</span></span>

<span data-ttu-id="07270-314">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-314">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-315">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-315">Example</span></span>

```c

/* Disconnect the Telnet Client associated with logical connection 2 on 
   the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_disconnect(&my_server, 2);

/* If status is NX_SUCCESS the Client on logical connection 2 was 
   disconnected.  */
```

## <a name="nx_telnet_server_get_open_connection_count"></a><span data-ttu-id="07270-316">nx_telnet_server_get_open_connection_count</span><span class="sxs-lookup"><span data-stu-id="07270-316">nx_telnet_server_get_open_connection_count</span></span>

<span data-ttu-id="07270-317">Restituisce il numero di connessioni attualmente aperte</span><span class="sxs-lookup"><span data-stu-id="07270-317">Return number of currently open connections</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-318">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-318">Prototype</span></span>

```c
UINT nx_telnet_server_get_open_connection_count(NX_TELNET_SERVER *server_ptr, UINT *connection_count);
```

### <a name="description"></a><span data-ttu-id="07270-319">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-319">Description</span></span>

<span data-ttu-id="07270-320">Questo servizio restituisce il numero di client Telnet attualmente connessi.</span><span class="sxs-lookup"><span data-stu-id="07270-320">This service returns the number of currently connected Telnet Clients.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-321">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-321">Input Parameters</span></span>

- <span data-ttu-id="07270-322">**server_ptr**: puntatore al blocco di controllo del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-322">**server_ptr**: Pointer to Telnet Server control block.</span></span>
- <span data-ttu-id="07270-323">**Connection_count**: puntatore alla memoria per archiviare il conteggio delle connessioni</span><span class="sxs-lookup"><span data-stu-id="07270-323">**Connection_count**: Pointer to memory to store connection count</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-324">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-324">Return Values</span></span>

- <span data-ttu-id="07270-325">**NX_SUCCESS**: (0x00) completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="07270-325">**NX_SUCCESS**: (0x00) Successful completion.</span></span>
- <span data-ttu-id="07270-326">NX_PTR_ERROR: (0x07) puntatore server non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-326">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="07270-327">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-327">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-328">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-328">Allowed From</span></span>

<span data-ttu-id="07270-329">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-329">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-330">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-330">Example</span></span>

```c
/* Get the number of Telnet Clients connected to the Server. */

status =  nx_telnet_server_get_open_connection_count(&my_server, &conn_count);

/* If status is NX_SUCCESS the conn_count holds the number of open connections.  */

```

## <a name="nx_telnet_server_packet_send"></a><span data-ttu-id="07270-331">nx_telnet_server_packet_send</span><span class="sxs-lookup"><span data-stu-id="07270-331">nx_telnet_server_packet_send</span></span>

<span data-ttu-id="07270-332">Invia pacchetto tramite connessione client</span><span class="sxs-lookup"><span data-stu-id="07270-332">Send packet through Client connection</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-333">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-333">Prototype</span></span>

```c
UINT nx_telnet_server_packet_send(NX_TELNET_SERVER *server_ptr, 
                                  UINT logical_connection, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="07270-334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-334">Description</span></span>

<span data-ttu-id="07270-335">Questo servizio invia un pacchetto alla connessione client in questa istanza del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-335">This service sends a packet to the Client connection on this Telnet Server instance.</span></span> <span data-ttu-id="07270-336">Questa routine viene in genere chiamata dalla funzione di callback dei dati di ricezione dell'applicazione in risposta a una condizione rilevata nei dati ricevuti.</span><span class="sxs-lookup"><span data-stu-id="07270-336">This routine is typically called from the application’s receive data callback function in response to a condition detected in the data received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-337">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-337">Input Parameters</span></span>

- <span data-ttu-id="07270-338">**server_ptr**: puntatore al blocco di controllo del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-338">**server_ptr**: Pointer to Telnet Server control block.</span></span>
- <span data-ttu-id="07270-339">**logical_connection**: connessione logica corrispondente alla connessione client in questo server.</span><span class="sxs-lookup"><span data-stu-id="07270-339">**logical_connection**: Logical connection corresponding the Client connection on this Server.</span></span> <span data-ttu-id="07270-340">Il valore valido è compreso tra 0 e NX_TELENET_MAX_CLIENTS.</span><span class="sxs-lookup"><span data-stu-id="07270-340">Valid value range from 0 through NX_TELENET_MAX_CLIENTS.</span></span>
- <span data-ttu-id="07270-341">**packet_ptr**: puntatore al pacchetto ricevuto.</span><span class="sxs-lookup"><span data-stu-id="07270-341">**packet_ptr**: Pointer to the received packet.</span></span>
- <span data-ttu-id="07270-342">**WAIT_OPTION**: definisce il tempo di attesa del servizio per l'invio di pacchetti del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-342">**wait_option**: Defines how long the service will wait for the Telnet Server packet send.</span></span> <span data-ttu-id="07270-343">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="07270-343">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="07270-344">**valore di timeout**: (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-344">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="07270-345">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando il server Telnet non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="07270-345">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span> 

### <a name="return-values"></a><span data-ttu-id="07270-346">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-346">Return Values</span></span>

- <span data-ttu-id="07270-347">**NX_SUCCESS**: (0x00) l'invio di pacchetti è riuscito.</span><span class="sxs-lookup"><span data-stu-id="07270-347">**NX_SUCCESS**: (0x00) Successful packet send.</span></span>
- <span data-ttu-id="07270-348">**NX_TELNET_FAILED**: (0xF2) trasmissione socket TCP non riuscita.</span><span class="sxs-lookup"><span data-stu-id="07270-348">**NX_TELNET_FAILED**: (0xF2) TCP socket send failed.</span></span>
- <span data-ttu-id="07270-349">NX_OPTION_ERROR: (0x0A) connessione logica non valida.</span><span class="sxs-lookup"><span data-stu-id="07270-349">NX_OPTION_ERROR: (0x0A) Invalid logical connection.</span></span>
- <span data-ttu-id="07270-350">NX_PTR_ERROR: (0x07) puntatore server non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-350">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="07270-351">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="07270-351">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-352">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-352">Allowed From</span></span>

<span data-ttu-id="07270-353">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-353">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-354">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-354">Example</span></span>

```c
/* Send a packet to the Telnet Client associated with logical connection 2 on 
   the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_packet_send(&my_server, 2, my_packet, 100);

/* If status is NX_SUCCESS the packet was sent to the Client on logical 
   connection 2.  */
```

## <a name="nx_telnet_server_packet_pool_set"></a><span data-ttu-id="07270-355">nx_telnet_server_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="07270-355">nx_telnet_server_packet_pool_set</span></span>

<span data-ttu-id="07270-356">Imposta pool di pacchetti creato in precedenza come pool di server Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-356">Set previously created packet pool as Telnet Server pool</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-357">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-357">Prototype</span></span>

```c
UINT nx_telnet_server_packet_pool_set(NX_TELNET_SERVER *server_ptr, NX_PACKET_POOL *packet_pool_ptr);

```

### <a name="description"></a><span data-ttu-id="07270-358">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-358">Description</span></span>

<span data-ttu-id="07270-359">Questo servizio imposta un pool di pacchetti creato in precedenza come pool di pacchetti del server Telnet se è stato definito NX_TELNET_SERVER_USER_CREATE_PACKET_POOL.</span><span class="sxs-lookup"><span data-stu-id="07270-359">This service sets a previously created packet pool as the Telnet Server packet pool if NX_TELNET_SERVER_USER_CREATE_PACKET_POOL is defined.</span></span> <span data-ttu-id="07270-360">Richiede inoltre che NX_TELNET_SERVER_OPTION_DISABLE non sia definito in modo che il server Telnet necessiti di un pool di pacchetti per trasmettere le opzioni Telnet ai client Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-360">It also requires that NX_TELNET_SERVER_OPTION_DISABLE not be defined such that the Telnet Server needs a packet pool to transmit Telnet options to Telnet clients.</span></span>

<span data-ttu-id="07270-361">Ciò consente alle applicazioni di creare il pool di pacchetti in memoria diversa, ad esempio senza memoria cache, rispetto allo stack del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-361">This permits applications to create the packet pool in different memory e.g. no cache memory, than the Telnet Server stack.</span></span> <span data-ttu-id="07270-362">Si noti che se questa funzione non controlla se il pool di pacchetti del server Telnet è già impostato.</span><span class="sxs-lookup"><span data-stu-id="07270-362">Note that if this function does not check if the Telnet Server packet pool is already set.</span></span> <span data-ttu-id="07270-363">Se viene chiamato su un puntatore al pool di pacchetti del server Telnet non null, lo sovrascriverà e sostituirà il pool di pacchetti esistente con il pool di pacchetti a cui punta il puntatore di input.</span><span class="sxs-lookup"><span data-stu-id="07270-363">If it is called on a non null Telnet Server packet pool pointer, it will overwrite it and replace the existing packet pool with packet pool pointed to by the input pointer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-364">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-364">Input Parameters</span></span>

- <span data-ttu-id="07270-365">**server_ptr**: puntatore al blocco di controllo server Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-365">**server_ptr**: Pointer to Telnet Server control block</span></span>
- <span data-ttu-id="07270-366">**packet_pool_ptr**: puntatore al pool di pacchetti creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="07270-366">**packet_pool_ptr**: Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-367">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-367">Return Values</span></span>

- <span data-ttu-id="07270-368">**NX_SUCCESS**: (0x00) ha impostato correttamente il pool.</span><span class="sxs-lookup"><span data-stu-id="07270-368">**NX_SUCCESS**: (0x00) Successfully set pool.</span></span>
- <span data-ttu-id="07270-369">NX_PTR_ERROR: (0x07) puntatore server non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-369">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-370">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-370">Allowed From</span></span>

<span data-ttu-id="07270-371">Init, thread</span><span class="sxs-lookup"><span data-stu-id="07270-371">Init, Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-372">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-372">Example</span></span>

```c
status =  nx_packet_pool_create(&telnet_server_packet_pool, 
                                "Telnet Server Packet Pool", 
                                telnet_server_pool_area, 600*10);

/* Set the packet pool as the Telnet Server packet pool.   */
status =  nx_telnet_server_packet_pool_set(&my_server, &telnet_server_packet_pool);

/* If status is NX_SUCCESS the packet pool is set as Telnet Server pool.  */
```
## <a name="nx_telnet_server_start"></a><span data-ttu-id="07270-373">nx_telnet_server_start</span><span class="sxs-lookup"><span data-stu-id="07270-373">nx_telnet_server_start</span></span>

<span data-ttu-id="07270-374">Avviare un server Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-374">Start a Telnet Server</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-375">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-375">Prototype</span></span>

```c
UINT nx_telnet_server_start(NX_TELNET_SERVER *server_ptr);

```

### <a name="description"></a><span data-ttu-id="07270-376">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-376">Description</span></span>

<span data-ttu-id="07270-377">Questo servizio avvia un'istanza del server Telnet creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="07270-377">This service starts a previously created Telnet Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-378">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-378">Input Parameters</span></span>

- <span data-ttu-id="07270-379">**server_ptr**: puntatore al blocco di controllo del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-379">**server_ptr**: Pointer to Telnet Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-380">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-380">Return Values</span></span>

- <span data-ttu-id="07270-381">**NX_SUCCESS**: (0x00) avviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="07270-381">**NX_SUCCESS**: (0x00) Successfully started.</span></span>
- <span data-ttu-id="07270-382">**NX_TELNET_NO_PACKET_POOL**: (0XF6) non è stato impostato alcun pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="07270-382">**NX_TELNET_NO_PACKET_POOL**: (0xF6) No packet pool set</span></span>
- <span data-ttu-id="07270-383">NX_PTR_ERROR: (0x07) puntatore server non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-383">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-384">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-384">Allowed From</span></span>

<span data-ttu-id="07270-385">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="07270-385">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-386">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-386">Example</span></span>

```c
/* Start the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_start(&my_server);

/* If status is NX_SUCCESS the Server was started.  */
```

## <a name="nx_telnet_server_stop"></a><span data-ttu-id="07270-387">nx_telnet_server_stop</span><span class="sxs-lookup"><span data-stu-id="07270-387">nx_telnet_server_stop</span></span>

<span data-ttu-id="07270-388">Arrestare un server Telnet</span><span class="sxs-lookup"><span data-stu-id="07270-388">Stop a Telnet Server</span></span>

### <a name="prototype"></a><span data-ttu-id="07270-389">Prototipo</span><span class="sxs-lookup"><span data-stu-id="07270-389">Prototype</span></span>

```c
UINT nx_telnet_server_stop(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="07270-390">Descrizione</span><span class="sxs-lookup"><span data-stu-id="07270-390">Description</span></span>

<span data-ttu-id="07270-391">Questo servizio interrompe un'istanza del server Telnet creata e avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="07270-391">This service stops a previously created and started Telnet Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="07270-392">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="07270-392">Input Parameters</span></span>

- <span data-ttu-id="07270-393">**server_ptr**: puntatore al blocco di controllo del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="07270-393">**server_ptr**: Pointer to Telnet Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="07270-394">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="07270-394">Return Values</span></span>

- <span data-ttu-id="07270-395">**NX_SUCCESS**: (0x00) arrestato correttamente</span><span class="sxs-lookup"><span data-stu-id="07270-395">**NX_SUCCESS**: (0x00) Successfully stopped</span></span>
- <span data-ttu-id="07270-396">NX_PTR_ERROR: (0x07) puntatore server non valido.</span><span class="sxs-lookup"><span data-stu-id="07270-396">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="07270-397">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="07270-397">NX_CALLER_ERROR: (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="07270-398">Consentito da</span><span class="sxs-lookup"><span data-stu-id="07270-398">Allowed From</span></span>

<span data-ttu-id="07270-399">Thread</span><span class="sxs-lookup"><span data-stu-id="07270-399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="07270-400">Esempio</span><span class="sxs-lookup"><span data-stu-id="07270-400">Example</span></span>

```c
/* Stop the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_stop(&my_server);

/* If status is NX_SUCCESS the Server was stopped.  */
```