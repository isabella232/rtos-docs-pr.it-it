---
title: Capitolo 3-Descrizione dei servizi FTP
description: Questo capitolo contiene una descrizione di tutti i servizi FTP NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d721d8bd3e08d8cccdc13011807b4c5017c84173
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821884"
---
# <a name="chapter-3---description-of-ftp-services"></a><span data-ttu-id="45cab-103">Capitolo 3-Descrizione dei servizi FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-103">Chapter 3 - Description of FTP services</span></span>

<span data-ttu-id="45cab-104">Questo capitolo contiene una descrizione di tutti i servizi FTP NetX (elencati di seguito) in ordine alfabetico, ad eccezione del caso in cui gli equivalenti IPv4 e IPv6 dello stesso servizio siano abbinati.</span><span class="sxs-lookup"><span data-stu-id="45cab-104">This chapter contains a description of all NetX FTP services (listed below) in alphabetic order (except where IPv4 and IPv6 equivalents of the same service are paired together).</span></span>

> [!NOTE]
> <span data-ttu-id="45cab-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="45cab-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_ftp_client_connect"></a><span data-ttu-id="45cab-106">nx_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="45cab-106">nx_ftp_client_connect</span></span>

<span data-ttu-id="45cab-107">Connettersi a un server FTP tramite IPv4</span><span class="sxs-lookup"><span data-stu-id="45cab-107">Connect to an FTP Server over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-108">Prototype</span></span>

```C
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG server_ip, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-109">Description</span></span>

<span data-ttu-id="45cab-110">Questo servizio connette l'istanza del client FTP NetX creata in precedenza al server FTP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="45cab-110">This service connects the previously created NetX FTP Client instance to the FTP Server at the supplied IP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-111">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-111">Input Parameters</span></span>

- <span data-ttu-id="45cab-112">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-112">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-113">**server_ip** Indirizzo IP del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-113">**server_ip** IP address of FTP Server.</span></span>
- <span data-ttu-id="45cab-114">**nome utente** Nome utente del client per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-114">**username** Client username for authentication.</span></span>
- <span data-ttu-id="45cab-115">**password** di Password client per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-115">**password** Client password for authentication.</span></span>
- <span data-ttu-id="45cab-116">**WAIT_OPTION** Definisce il tempo di attesa del servizio per la connessione client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-116">**wait_option** Defines how long the service will wait for the FTP Client connection.</span></span> <span data-ttu-id="45cab-117">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-117">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-118">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-118">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-119">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-119">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-120">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-120">Return Values</span></span>

- <span data-ttu-id="45cab-121">**NX_SUCCESS** (0x00) connessione FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-121">**NX_SUCCESS** (0x00) Successful FTP connection.</span></span>
- <span data-ttu-id="45cab-122">**NX_TFTP_EXPECTED_22X_CODE** (0xDB) non ha ricevuto una risposta 22x (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-122">**NX_TFTP_EXPECTED_22X_CODE** (0xDB) Did not get a 22X (ok) response</span></span>
- <span data-ttu-id="45cab-123">**NX_FTP_EXPECTED_23X_CODE** (0xdc) non ha ricevuto una risposta 23x (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-123">**NX_FTP_EXPECTED_23X_CODE** (0xDC) Did not get a 23X (ok) response</span></span>
- <span data-ttu-id="45cab-124">**NX_FTP_EXPECTED_33X_CODE** (0xDE) non ha ricevuto una risposta 33x (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-124">**NX_FTP_EXPECTED_33X_CODE** (0xDE) Did not get a 33X (ok) response</span></span>
- <span data-ttu-id="45cab-125">Il client **NX_FTP_NOT_DISCONNECTED** (0xd4) è già connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-125">**NX_FTP_NOT_DISCONNECTED** (0xD4) Client is already connected.</span></span>
- <span data-ttu-id="45cab-126">L'input del puntatore NX_PTR_ERROR (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-126">NX_PTR_ERROR (0x07) Invalid pointer input.</span></span>
- <span data-ttu-id="45cab-127">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-127">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="45cab-128">NX_IP_ADDRESS_ERROR (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-128">NX_IP_ADDRESS_ERROR (0x21) Invalid IP address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-129">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-129">Allowed From</span></span>

<span data-ttu-id="45cab-130">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-130">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-131">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-131">Example</span></span>

```C
/* Connect the FTP Client instance “my_client” to the FTP Server at

IP address 1.2.3.4. */

status = nx_ftp_client_connect(&my_client, IP_ADDRESS(1,2,3,4), NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
    connected to the FTP Server. */
```

### <a name="see-also"></a><span data-ttu-id="45cab-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="45cab-132">See Also</span></span>

<span data-ttu-id="45cab-133">nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nxd_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="45cab-133">nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nxd_ftp_client_connect</span></span>

## <a name="nxd_ftp_client_connect"></a><span data-ttu-id="45cab-134">nxd_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="45cab-134">nxd_ftp_client_connect</span></span>

<span data-ttu-id="45cab-135">Connettersi a un server FTP con supporto IPv6</span><span class="sxs-lookup"><span data-stu-id="45cab-135">Connect to an FTP Server with IPv6 support</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-136">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-136">Prototype</span></span>

```C
UINT nxd_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    NXD_ADDRESS *server_ipduo, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-137">Description</span></span>

<span data-ttu-id="45cab-138">Questo servizio connette l'istanza del client FTP NetX Duo creata in precedenza al server FTP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="45cab-138">This service connects the previously created NetX Duo FTP Client instance to the FTP Server at the supplied IP address.</span></span> <span data-ttu-id="45cab-139">Sono supportate sia reti IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="45cab-139">Both IPv4 and IPv6 networks are supported.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-140">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-140">Input Parameters</span></span>

- <span data-ttu-id="45cab-141">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-141">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-142">**server_ipduo** Indirizzo IP del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-142">**server_ipduo** IP address of the FTP Server.</span></span>
- <span data-ttu-id="45cab-143">**nome utente** Nome utente del client per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-143">**username** Client username for authentication.</span></span>
- <span data-ttu-id="45cab-144">**password** di Password client per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-144">**password** Client password for authentication.</span></span>
- <span data-ttu-id="45cab-145">**WAIT_OPTION** Definisce il tempo di attesa del servizio per la connessione client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-145">**wait_option** Defines how long the service will wait for the FTP Client connection.</span></span> <span data-ttu-id="45cab-146">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-146">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-147">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-147">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-148">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-148">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-149">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-149">Return Values</span></span>

- <span data-ttu-id="45cab-150">**NX_SUCCESS** (0x00) connessione FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-150">**NX_SUCCESS** (0x00) Successful FTP connection.</span></span>
- <span data-ttu-id="45cab-151">**NX_TFTP_EXPECTED_22X_CODE** (0xDB) non ha ricevuto una risposta 22x (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-151">**NX_TFTP_EXPECTED_22X_CODE** (0xDB) Did not get a 22X (ok) response</span></span>
- <span data-ttu-id="45cab-152">**NX_FTP_EXPECTED_23X_CODE** (0xdc) non ha ricevuto una risposta 23x (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-152">**NX_FTP_EXPECTED_23X_CODE** (0xDC) Did not get a 23X (ok) response</span></span>
- <span data-ttu-id="45cab-153">**NX_FTP_EXPECTED_33X_CODE** (0xDE) non ha ricevuto una risposta 33x (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-153">**NX_FTP_EXPECTED_33X_CODE** (0xDE) Did not get a 33X (ok) response</span></span>
- <span data-ttu-id="45cab-154">Il client **NX_FTP_NOT_DISCONNECTED** (0xd4) è già connesso</span><span class="sxs-lookup"><span data-stu-id="45cab-154">**NX_FTP_NOT_DISCONNECTED** (0xD4) Client is already connected</span></span>
- <span data-ttu-id="45cab-155">NX_PTR_ERROR (0x07) puntatore non valido InOut.</span><span class="sxs-lookup"><span data-stu-id="45cab-155">NX_PTR_ERROR (0x07) Invalid pointer inout.</span></span>
- <span data-ttu-id="45cab-156">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-156">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="45cab-157">NX_IP_ADDRESS_ERROR (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-157">NX_IP_ADDRESS_ERROR (0x21) Invalid IP address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-158">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-158">Allowed From</span></span>

<span data-ttu-id="45cab-159">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-159">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-160">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-160">Example</span></span>

```C
/* Connect an FTP Client instance to the FTP Server. */

/* Set up an IPv6 address for the server here.
    Note this could also be an IPv4 address as well*/

server_ip_addr.nxd_ip_address.v6[3] = 0x106;
server_ip_addr.nxd_ip_address.v6[2] = 0x0;
server_ip_addr.nxd_ip_address.v6[1] = 0x0000f101;
server_ip_addr.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V6;

status = nxd_ftp_client_connect(&my_client, server_ip_addr, NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
    connected to the FTP Server. */
```

### <a name="see-also"></a><span data-ttu-id="45cab-161">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="45cab-161">See Also</span></span>

<span data-ttu-id="45cab-162">nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nx_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="45cab-162">nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nx_ftp_client_connect</span></span>

## <a name="nx_ftp_client_create"></a><span data-ttu-id="45cab-163">nx_ftp_client_create</span><span class="sxs-lookup"><span data-stu-id="45cab-163">nx_ftp_client_create</span></span>

<span data-ttu-id="45cab-164">Creare un'istanza del client FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-164">Create an FTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-165">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-165">Prototype</span></span>

```C
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="45cab-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-166">Description</span></span>

<span data-ttu-id="45cab-167">Questo servizio crea un'istanza del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-167">This service creates an FTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-168">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-168">Input Parameters</span></span>

- <span data-ttu-id="45cab-169">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-169">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-170">**ftp_client_name** Nome del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-170">**ftp_client_name** Name of FTP Client.</span></span>
- <span data-ttu-id="45cab-171">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45cab-171">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="45cab-172">**window_size** Dimensioni della finestra annunciata per i socket TCP del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-172">**window_size** Advertised window size for TCP sockets of this FTP Client.</span></span>
- <span data-ttu-id="45cab-173">**pool_ptr** Puntatore al pool di pacchetti predefinito per il client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-173">**pool_ptr** Pointer to the default packet pool for this FTP Client.</span></span> <span data-ttu-id="45cab-174">Si noti che il payload del pacchetto minimo deve essere sufficientemente grande da contenere il percorso completo e il nome del file o della directory.</span><span class="sxs-lookup"><span data-stu-id="45cab-174">Note that the minimum packet payload must be large enough to hold  complete path and the file or directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-175">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-175">Return Values</span></span>

- <span data-ttu-id="45cab-176">**NX_SUCCESS** (0x00) creazione client FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-176">**NX_SUCCESS** (0x00) Successful FTP Client create.</span></span>
- <span data-ttu-id="45cab-177">L'input del puntatore NX_PTR_ERROR (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-177">NX_PTR_ERROR (0x07) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-178">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-178">Allowed From</span></span>

<span data-ttu-id="45cab-179">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="45cab-179">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-180">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-180">Example</span></span>

```C
/* Create the FTP Client instance “my_client.” */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
    2000, &client_pool);
/* If status is NX_SUCCESS the FTP Client instance was successfully created. */
```

## <a name="nx_ftp_client_delete"></a><span data-ttu-id="45cab-181">nx_ftp_client_delete</span><span class="sxs-lookup"><span data-stu-id="45cab-181">nx_ftp_client_delete</span></span>

<span data-ttu-id="45cab-182">Eliminare un'istanza del client FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-182">Delete an FTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-183">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-183">Prototype</span></span>

```C
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="45cab-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-184">Description</span></span>

<span data-ttu-id="45cab-185">Questo servizio Elimina un'istanza del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-185">This service deletes an FTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-186">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-186">Input Parameters</span></span>

- <span data-ttu-id="45cab-187">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-187">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-188">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-188">Return Values</span></span>

- <span data-ttu-id="45cab-189">**NX_SUCCESS** (0x00) eliminazione client FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-189">**NX_SUCCESS** (0x00) Successful FTP Client delete.</span></span>
- <span data-ttu-id="45cab-190">Client FTP **NX_FTP_NOT_DISCONNECTED** (0xd4) non disconnesso</span><span class="sxs-lookup"><span data-stu-id="45cab-190">**NX_FTP_NOT_DISCONNECTED** (0xD4) FTP client not disconnected</span></span>
- <span data-ttu-id="45cab-191">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-191">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-192">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-192">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-193">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-193">Allowed From</span></span>

<span data-ttu-id="45cab-194">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-194">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-195">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-195">Example</span></span>

```C
/* Delete the FTP Client instance “my_client.” */

status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a><span data-ttu-id="45cab-196">nx_ftp_client_directory_create</span><span class="sxs-lookup"><span data-stu-id="45cab-196">nx_ftp_client_directory_create</span></span>

<span data-ttu-id="45cab-197">Creare una directory nel server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-197">Create a directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-198">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-198">Prototype</span></span>

```C
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-199">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-199">Description</span></span>

<span data-ttu-id="45cab-200">Questo servizio crea la directory specificata nel server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="45cab-200">This service creates the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-201">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-201">Input Parameters</span></span>

- <span data-ttu-id="45cab-202">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-202">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-203">**DIRECTORY_NAME** Nome della directory da creare.</span><span class="sxs-lookup"><span data-stu-id="45cab-203">**directory_name** Name of directory to create.</span></span>
- <span data-ttu-id="45cab-204">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della creazione della directory FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-204">**wait_option** Defines how long the service will wait for the FTP directory create.</span></span> <span data-ttu-id="45cab-205">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-205">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-206">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-206">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-207">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-207">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-208">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-208">Return Values</span></span>

- <span data-ttu-id="45cab-209">**NX_SUCCESS** (0x00) Creazione directory FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-209">**NX_SUCCESS** (0x00) Successful FTP directory create.</span></span>
- <span data-ttu-id="45cab-210">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-210">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-211">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-211">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-212">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-212">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-213">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-213">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-214">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-214">Allowed From</span></span>

<span data-ttu-id="45cab-215">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-215">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-216">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-216">Example</span></span>

```C
/* Create the directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_create(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” was successfully created. */
```

## <a name="nx_ftp_client_directory_default_set"></a><span data-ttu-id="45cab-217">nx_ftp_client_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="45cab-217">nx_ftp_client_directory_default_set</span></span>

<span data-ttu-id="45cab-218">Imposta la directory predefinita nel server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-218">Set default directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-219">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-219">Prototype</span></span>

```C
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-220">Description</span></span>

<span data-ttu-id="45cab-221">Questo servizio imposta la directory predefinita sul server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="45cab-221">This service sets the default directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="45cab-222">Questa directory predefinita si applica solo alla connessione del client.</span><span class="sxs-lookup"><span data-stu-id="45cab-222">This default directory applies only to this client’s connection.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-223">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-223">Input Parameters</span></span>

- <span data-ttu-id="45cab-224">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-224">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-225">**directory_path** Nome del percorso della directory da impostare.</span><span class="sxs-lookup"><span data-stu-id="45cab-225">**directory_path** Name of directory path to set.</span></span>
- <span data-ttu-id="45cab-226">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del set di directory predefinito FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-226">**wait_option** Defines how long the service will wait for the FTP default directory set.</span></span> <span data-ttu-id="45cab-227">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-227">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-228">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-228">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-229">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-229">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-230">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-230">Return Values</span></span>

- <span data-ttu-id="45cab-231">**NX_SUCCESS** (0x00) impostazione predefinita FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-231">**NX_SUCCESS** (0x00) Successful FTP default set.</span></span>
- <span data-ttu-id="45cab-232">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-232">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-233">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-233">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-234">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-234">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-235">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-235">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-236">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-236">Allowed From</span></span>

<span data-ttu-id="45cab-237">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-237">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-238">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-238">Example</span></span>

```C
/* Set the default directory to “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_default_set(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a><span data-ttu-id="45cab-239">nx_ftp_client_directory_delete</span><span class="sxs-lookup"><span data-stu-id="45cab-239">nx_ftp_client_directory_delete</span></span>

<span data-ttu-id="45cab-240">Elimina directory nel server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-240">Delete directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-241">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-241">Prototype</span></span>

```C
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-242">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-242">Description</span></span>

<span data-ttu-id="45cab-243">Questo servizio Elimina la directory specificata nel server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="45cab-243">This service deletes the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-244">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-244">Input Parameters</span></span>

- <span data-ttu-id="45cab-245">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-245">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-246">**DIRECTORY_NAME** Nome della directory da eliminare.</span><span class="sxs-lookup"><span data-stu-id="45cab-246">**directory_name** Name of directory to delete.</span></span>
- <span data-ttu-id="45cab-247">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'eliminazione della directory FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-247">**wait_option** Defines how long the service will wait for the FTP directory delete.</span></span> <span data-ttu-id="45cab-248">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-248">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-249">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-249">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-250">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-250">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-251">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-251">Return Values</span></span>

- <span data-ttu-id="45cab-252">**NX_SUCCESS** (0x00) eliminazione directory FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-252">**NX_SUCCESS** (0x00) Successful FTP directory delete.</span></span>
- <span data-ttu-id="45cab-253">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-253">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-254">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-254">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-255">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-255">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-256">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-256">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-257">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-257">Allowed From</span></span>

<span data-ttu-id="45cab-258">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-258">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-259">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-259">Example</span></span>

```C
/* Delete directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_delete(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a><span data-ttu-id="45cab-260">nx_ftp_client_directory_listing_get</span><span class="sxs-lookup"><span data-stu-id="45cab-260">nx_ftp_client_directory_listing_get</span></span>

<span data-ttu-id="45cab-261">Ottenere l'elenco di directory dal server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-261">Get directory listing from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-262">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-262">Prototype</span></span>

```C
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-263">Description</span></span>

<span data-ttu-id="45cab-264">Questo servizio ottiene il contenuto della directory specificata nel server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="45cab-264">This service gets the contents of the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="45cab-265">Il puntatore al pacchetto fornito conterrà una o più voci di directory.</span><span class="sxs-lookup"><span data-stu-id="45cab-265">The supplied packet pointer will contain one or more directory entries.</span></span> <span data-ttu-id="45cab-266">Ogni voce è separata da una \<cr/lf\> combinazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-266">Each entry is separated by a \<cr/lf\> combination.</span></span> <span data-ttu-id="45cab-267">Per completare l'operazione di Get della directory è necessario chiamare il ***nx_ftp_client_directory_listing_continue*** .</span><span class="sxs-lookup"><span data-stu-id="45cab-267">The ***nx_ftp_client_directory_listing_continue*** should be called to complete the directory get operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-268">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-268">Input Parameters</span></span>

- <span data-ttu-id="45cab-269">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-269">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-270">**DIRECTORY_NAME** Nome della directory da cui ottenere il contenuto.</span><span class="sxs-lookup"><span data-stu-id="45cab-270">**directory_name** Name of directory to get contents of.</span></span>
- <span data-ttu-id="45cab-271">**packet_ptr** Puntatore al puntatore del pacchetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-271">**packet_ptr** Pointer to destination packet pointer.</span></span> <span data-ttu-id="45cab-272">In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory.</span><span class="sxs-lookup"><span data-stu-id="45cab-272">If successful, the packet payload will contain one or more directory entries.</span></span>
- <span data-ttu-id="45cab-273">**WAIT_OPTION** Definisce il tempo di attesa del servizio per la visualizzazione della directory FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-273">**wait_option** Defines how long the service will wait for the FTP directory listing.</span></span> <span data-ttu-id="45cab-274">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-274">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-275">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-275">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-276">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-276">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-277">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-277">Return Values</span></span>

- <span data-ttu-id="45cab-278">Elenco di directory FTP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="45cab-278">**NX_SUCCESS** (0x00) Successful FTP directory listing.</span></span>
- <span data-ttu-id="45cab-279">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-279">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-280">Servizio **NX_NOT_ENABLED** (0x14) (IPv6) non abilitato</span><span class="sxs-lookup"><span data-stu-id="45cab-280">**NX_NOT_ENABLED** (0x14) Service (IPv6) not enabled</span></span>
- <span data-ttu-id="45cab-281">**NX_FTP_EXPECTED_1XX_CODE** (0xD9) non ha ricevuto una risposta 1xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-281">**NX_FTP_EXPECTED_1XX_CODE** (0xD9) Did not get a 1XX (ok) response</span></span>
- <span data-ttu-id="45cab-282">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-282">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-283">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-283">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-284">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-284">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-285">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-285">Allowed From</span></span>

<span data-ttu-id="45cab-286">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-286">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-287">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-287">Example</span></span>

```C
/* Get the contents of directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_listing_get(&my_client, “my_dir”, &my_packet,
    200);

/* If status is NX_SUCCESS, one or more entries of the directory “my_dir”
    can be found in “my_packet”. */
```

## <a name="nx_ftp_client_directory_listing_continue"></a><span data-ttu-id="45cab-288">nx_ftp_client_directory_listing_continue</span><span class="sxs-lookup"><span data-stu-id="45cab-288">nx_ftp_client_directory_listing_continue</span></span>

<span data-ttu-id="45cab-289">Continua Inserzione directory dal server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-289">Continue directory listing from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-290">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-290">Prototype</span></span>

```C
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-291">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-291">Description</span></span>

<span data-ttu-id="45cab-292">Questo servizio continua a ottenere il contenuto della directory specificata nel server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="45cab-292">This service continues getting the contents of the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="45cab-293">Dovrebbe essere stato immediatamente preceduto da una chiamata a ***nx_ftp_client_directory_listing_get***.</span><span class="sxs-lookup"><span data-stu-id="45cab-293">It should have been immediately preceded by a call to ***nx_ftp_client_directory_listing_get***.</span></span> <span data-ttu-id="45cab-294">In caso di esito positivo, il puntatore al pacchetto fornito conterrà una o più voci di directory.</span><span class="sxs-lookup"><span data-stu-id="45cab-294">If successful, the supplied packet pointer will contain one or more directory entries.</span></span> <span data-ttu-id="45cab-295">Questa routine deve essere chiamata fino a quando non viene ricevuto uno stato di NX_FTP_END_OF_LISTING.</span><span class="sxs-lookup"><span data-stu-id="45cab-295">This routine should be called until an NX_FTP_END_OF_LISTING status is received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-296">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-296">Input Parameters</span></span>

- <span data-ttu-id="45cab-297">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-297">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-298">**packet_ptr** Puntatore al puntatore del pacchetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-298">**packet_ptr** Pointer to destination packet pointer.</span></span> <span data-ttu-id="45cab-299">In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory, separate da un> di <CR/LF.</span><span class="sxs-lookup"><span data-stu-id="45cab-299">If successful, the packet payload will contain one or more directory entries, separated by a <cr/lf>.</span></span>
- <span data-ttu-id="45cab-300">**WAIT_OPTION** Definisce il tempo di attesa del servizio per la visualizzazione della directory FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-300">**wait_option** Defines how long the service will wait for the FTP directory listing.</span></span> <span data-ttu-id="45cab-301">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-301">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-302">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-302">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-303">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-303">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-304">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-304">Return Values</span></span>

- <span data-ttu-id="45cab-305">Elenco di directory FTP riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="45cab-305">**NX_SUCCESS** (0x00) Successful FTP directory listing.</span></span>
- <span data-ttu-id="45cab-306">**NX_FTP_END_OF_LISTING** (0XD8) non sono presenti altre voci in questa directory.</span><span class="sxs-lookup"><span data-stu-id="45cab-306">**NX_FTP_END_OF_LISTING** (0xD8) No more entries in this directory.</span></span>
- <span data-ttu-id="45cab-307">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-307">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-308">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-308">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-309">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-309">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-310">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-310">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-311">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-311">Allowed From</span></span>

<span data-ttu-id="45cab-312">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-312">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-313">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-313">Example</span></span>

```C
/* Continue getting the contents of directory “my_dir” on the FTP Server
    connected to the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_listing_continue(&my_client, &my_packet,
    200);

/* If status is NX_SUCCESS, one or more entries of the directory “my_dir”
    can be found in “my_packet”. */
```

## <a name="nx_ftp_client_disconnect"></a><span data-ttu-id="45cab-314">nx_ftp_client_disconnect</span><span class="sxs-lookup"><span data-stu-id="45cab-314">nx_ftp_client_disconnect</span></span>

<span data-ttu-id="45cab-315">Disconnetti dal server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-315">Disconnect from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-316">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-316">Prototype</span></span>

```C
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-317">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-317">Description</span></span>

<span data-ttu-id="45cab-318">Questo servizio disconnette una connessione al server FTP stabilita in precedenza con il client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="45cab-318">This service disconnects a previously established FTP Server connection with the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-319">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-319">Input Parameters</span></span>

- <span data-ttu-id="45cab-320">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-320">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-321">**WAIT_OPTION** Definisce per quanto tempo il servizio attenderà la disconnessione del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-321">**wait_option** Defines how long the service will wait for the FTP Client disconnect.</span></span> <span data-ttu-id="45cab-322">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-322">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-323">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-323">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-324">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-324">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-325">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-325">Return Values</span></span>

- <span data-ttu-id="45cab-326">Disconnessione FTP **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-326">**NX_SUCCESS** (0x00) Successful FTP disconnect.</span></span>
- <span data-ttu-id="45cab-327">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-327">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-328">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-328">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-329">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-329">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-330">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-330">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-331">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-331">Allowed From</span></span>

<span data-ttu-id="45cab-332">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-332">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-333">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-333">Example</span></span>

```C
/* Disconnect “my_client” from the FTP Server. */

status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, “my_client” has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a><span data-ttu-id="45cab-334">nx_ftp_client_file_close</span><span class="sxs-lookup"><span data-stu-id="45cab-334">nx_ftp_client_file_close</span></span>

<span data-ttu-id="45cab-335">Chiudi file client</span><span class="sxs-lookup"><span data-stu-id="45cab-335">Close Client file</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-336">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-336">Prototype</span></span>

```C
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-337">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-337">Description</span></span>

<span data-ttu-id="45cab-338">Questo servizio chiude un file aperto in precedenza nel server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-338">This service closes a previously opened file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-339">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-339">Input Parameters</span></span>

- <span data-ttu-id="45cab-340">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-340">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-341">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della chiusura del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-341">**wait_option** Defines how long the service will wait for the FTP Client file close.</span></span> <span data-ttu-id="45cab-342">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-342">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-343">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-343">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-344">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-344">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-345">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-345">Return Values</span></span>

- <span data-ttu-id="45cab-346">Chiusura del file FTP **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="45cab-346">**NX_SUCCESS** (0x00) Successful FTP file close.</span></span>
- <span data-ttu-id="45cab-347">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-347">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-348">**NX_FTP_NOT_OPEN (0xD5)** Il file non è aperto; impossibile chiuderla</span><span class="sxs-lookup"><span data-stu-id="45cab-348">**NX_FTP_NOT_OPEN (0xD5)** File not open; cannot close it</span></span>
- <span data-ttu-id="45cab-349">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-349">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-350">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-350">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-351">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-351">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-352">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-352">Allowed From</span></span>

<span data-ttu-id="45cab-353">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-353">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-354">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-354">Example</span></span>

```C
/* Close previously opened file of client “my_client” on the FTP Server. */

status = nx_ftp_client_file_close(&my_client, 200);

/* If status is NX_SUCCESS, the file opened previously in the “my_client” FTP
    connection has been closed. */
```

## <a name="nx_ftp_client_file_delete"></a><span data-ttu-id="45cab-355">nx_ftp_client_file_delete</span><span class="sxs-lookup"><span data-stu-id="45cab-355">nx_ftp_client_file_delete</span></span>

<span data-ttu-id="45cab-356">Elimina file nel server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-356">Delete file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-357">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-357">Prototype</span></span>

```C
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-358">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-358">Description</span></span>

<span data-ttu-id="45cab-359">Questo servizio Elimina il file specificato sul server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-359">This service deletes the specified file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-360">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-360">Input Parameters</span></span>

- <span data-ttu-id="45cab-361">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-361">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-362">**file_name** Nome del file da eliminare.</span><span class="sxs-lookup"><span data-stu-id="45cab-362">**file_name** Name of file to delete.</span></span>
- <span data-ttu-id="45cab-363">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'eliminazione del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-363">**wait_option** Defines how long the service will wait for the FTP Client file delete.</span></span> <span data-ttu-id="45cab-364">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-364">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-365">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-365">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-366">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-366">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-367">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-367">Return Values</span></span>

- <span data-ttu-id="45cab-368">Eliminazione file FTP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="45cab-368">**NX_SUCCESS** (0x00) Successful FTP file delete.</span></span>
- <span data-ttu-id="45cab-369">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-369">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-370">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-370">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-371">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-371">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-372">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-372">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-373">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-373">Allowed From</span></span>

<span data-ttu-id="45cab-374">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-374">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-375">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-375">Example</span></span>

```C
/* Delete the file “my_file.txt” on the FTP Server using the previously
    connected client “my_client.” */

status = nx_ftp_client_file_delete(&my_client, “my_file.txt”, 200);

/* If status is NX_SUCCESS, the file “my_file.txt” on the FTP Server is
    deleted. */
```

## <a name="nx_ftp_client_file_open"></a><span data-ttu-id="45cab-376">nx_ftp_client_file_open</span><span class="sxs-lookup"><span data-stu-id="45cab-376">nx_ftp_client_file_open</span></span>

<span data-ttu-id="45cab-377">Apre il file nel server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-377">Opens file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-378">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-378">Prototype</span></span>

```C
UINT nx_ftp_client_file_open(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, UINT open_type, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-379">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-379">Description</span></span>

<span data-ttu-id="45cab-380">Questo servizio apre il file specificato, per la lettura o la scrittura, sul server FTP precedentemente connesso all'istanza client specificata.</span><span class="sxs-lookup"><span data-stu-id="45cab-380">This service opens the specified file – for reading or writing – on the FTP Server previously connected to the specified Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-381">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-381">Input Parameters</span></span>

- <span data-ttu-id="45cab-382">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-382">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-383">**file_name** Nome del file da aprire.</span><span class="sxs-lookup"><span data-stu-id="45cab-383">**file_name** Name of file to open.</span></span>
- <span data-ttu-id="45cab-384">**open_type** **NX_FTP_OPEN_FOR_READ** o **NX_FTP_OPEN_FOR_WRITE**.</span><span class="sxs-lookup"><span data-stu-id="45cab-384">**open_type** Either **NX_FTP_OPEN_FOR_READ** or **NX_FTP_OPEN_FOR_WRITE**.</span></span>
- <span data-ttu-id="45cab-385">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'apertura del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-385">**wait_option** Defines how long the service will wait for the FTP Client file open.</span></span> <span data-ttu-id="45cab-386">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-386">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-387">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-387">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-388">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-388">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-389">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-389">Return Values</span></span>

- <span data-ttu-id="45cab-390">Apertura del file FTP **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="45cab-390">**NX_SUCCESS** (0x00) Successful FTP file open.</span></span>
- <span data-ttu-id="45cab-391">Il tipo aperto **NX_OPTION_ERROR** (0X0A) non è valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-391">**NX_OPTION_ERROR** (0x0A) Invalid open type.</span></span>
- <span data-ttu-id="45cab-392">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-392">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-393">Il client FTP **NX_FTP_NOT_CLOSED** (0xD6) è già aperto.</span><span class="sxs-lookup"><span data-stu-id="45cab-393">**NX_FTP_NOT_CLOSED** (0xD6) FTP Client is already opened.</span></span>
- <span data-ttu-id="45cab-394">**NX_NO_FREE_PORTS** (0X45) non sono disponibili porte TCP da assegnare</span><span class="sxs-lookup"><span data-stu-id="45cab-394">**NX_NO_FREE_PORTS** (0x45) No TCP ports available to assign</span></span>
- <span data-ttu-id="45cab-395">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-395">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-396">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-396">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-397">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-397">Allowed From</span></span>

<span data-ttu-id="45cab-398">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-398">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-399">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-399">Example</span></span>

```C
/* Open the file “my_file.txt” for reading on the FTP Server using the previously
    connected client “my_client.” */

status = nx_ftp_client_file_open(&my_client, “my_file.txt”, NX_FTP_OPEN_FOR_READ,
    200);

/* If status is NX_SUCCESS, the file “my_file.txt” on the FTP Server is
    open for reading. */
```

## <a name="nx_ftp_client_file_read"></a><span data-ttu-id="45cab-400">nx_ftp_client_file_read</span><span class="sxs-lookup"><span data-stu-id="45cab-400">nx_ftp_client_file_read</span></span>

<span data-ttu-id="45cab-401">Lettura da file</span><span class="sxs-lookup"><span data-stu-id="45cab-401">Read from file</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-402">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-402">Prototype</span></span>

```C
UINT nx_ftp_client_file_read(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-403">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-403">Description</span></span>

<span data-ttu-id="45cab-404">Questo servizio legge un pacchetto da un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45cab-404">This service reads a packet from a previously opened file.</span></span> <span data-ttu-id="45cab-405">Deve essere chiamato ripetutamente fino a quando non viene ricevuto uno stato di NX_FTP_END_OF_FILE.</span><span class="sxs-lookup"><span data-stu-id="45cab-405">It should be called repetitively until a status of NX_FTP_END_OF_FILE is received.</span></span>

<span data-ttu-id="45cab-406">Si noti che il chiamante non alloca un pacchetto per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-406">Note that the caller does not allocate a packet for this service.</span></span>  <span data-ttu-id="45cab-407">È necessario fornire solo un puntatore a un puntatore di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="45cab-407">It need only supply a pointer to a packet pointer.</span></span> <span data-ttu-id="45cab-408">Questo servizio aggiornerà il puntatore del pacchetto in modo che punti a un pacchetto recuperato dalla coda di ricezione del socket.</span><span class="sxs-lookup"><span data-stu-id="45cab-408">This service will update that packet pointer to point to a packet retrieved from the socket receive queue.</span></span>  <span data-ttu-id="45cab-409">Se viene restituito uno stato di esito positivo, significa che è disponibile un pacchetto ed è responsabilità del chiamante rilasciare il pacchetto quando viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="45cab-409">If a successful status is returned, that means there was a packet available, and it is the caller’s responsibility to release the packet when it is done with it.</span></span>

<span data-ttu-id="45cab-410">Se viene restituito uno stato diverso da zero (stato di errore o NX_FTP_END_OF_FILE), il chiamante non rilascia il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="45cab-410">If a non-zero status (either an error status or NX_FTP_END_OF_FILE) is returned, the caller does not release the packet.</span></span> <span data-ttu-id="45cab-411">In caso contrario, viene generato un errore se il puntatore del pacchetto è NULL.</span><span class="sxs-lookup"><span data-stu-id="45cab-411">Otherwise, an error is generated when if the packet pointer is NULL.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-412">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-412">Input Parameters</span></span>

- <span data-ttu-id="45cab-413">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-413">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-414">**packet_ptr** Puntatore alla destinazione per il puntatore del pacchetto di dati da archiviare.</span><span class="sxs-lookup"><span data-stu-id="45cab-414">**packet_ptr** Pointer to destination for the data packet pointer to be stored.</span></span> <span data-ttu-id="45cab-415">Se l'operazione ha esito positivo, il pacchetto parte o tutto il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="45cab-415">If successful, the packet some or all the contains of the file.</span></span>
- <span data-ttu-id="45cab-416">**WAIT_OPTION** Definisce per quanto tempo il servizio attenderà la lettura del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-416">**wait_option** Defines how long the service will wait for the FTP Client file read.</span></span> <span data-ttu-id="45cab-417">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-417">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-418">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-418">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-419">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-419">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-420">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-420">Return Values</span></span>

- <span data-ttu-id="45cab-421">Lettura del file FTP **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="45cab-421">**NX_SUCCESS** (0x00) Successful FTP file read.</span></span>
- <span data-ttu-id="45cab-422">Il client FTP **NX_FTP_NOT_OPEN** (0xD5) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="45cab-422">**NX_FTP_NOT_OPEN** (0xD5) FTP Client is not opened.</span></span>
- <span data-ttu-id="45cab-423">**NX_FTP_END_OF_FILE** la condizione di fine del file (0xD7).</span><span class="sxs-lookup"><span data-stu-id="45cab-423">**NX_FTP_END_OF_FILE** (0xD7) End of file condition.</span></span>
- <span data-ttu-id="45cab-424">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-424">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-425">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-425">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-426">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-426">Allowed From</span></span>

<span data-ttu-id="45cab-427">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-427">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-428">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-428">Example</span></span>

```C
NX_PACKET   *my_packet;

/* Read a packet of data from the file “my_file.txt” that was previously opened
    from the client “my_client.” */

status = nx_ftp_client_file_read(&my_client, &my_packet, 200);

/* Check status.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else
{
    /* Release packet when done with it. */
    nx_packet_release(my_packet);
}

/* If status is NX_SUCCESS, the packet pointer, “my_packet” points to the packet
    that contains the next bytes from the file. If the file is completely
    downloaded, an NX_FTP_END_OF_FILE status is returned (no packet retrieved). */
```

## <a name="nx_ftp_client_file_rename"></a><span data-ttu-id="45cab-429">nx_ftp_client_file_rename</span><span class="sxs-lookup"><span data-stu-id="45cab-429">nx_ftp_client_file_rename</span></span>

<span data-ttu-id="45cab-430">Rinomina file nel server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-430">Rename file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-431">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-431">Prototype</span></span>

```C
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
    CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-432">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-432">Description</span></span>

<span data-ttu-id="45cab-433">Questo servizio Rinomina un file nel server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-433">This service renames a file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-434">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-434">Input Parameters</span></span>

- <span data-ttu-id="45cab-435">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-435">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-436">**nome file** Nome corrente del file.</span><span class="sxs-lookup"><span data-stu-id="45cab-436">**filename** Current name of file.</span></span>
- <span data-ttu-id="45cab-437">**new_filename** Nuovo nome per il file.</span><span class="sxs-lookup"><span data-stu-id="45cab-437">**new_filename** New name for file.</span></span>
- <span data-ttu-id="45cab-438">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della ridenominazione del file client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-438">**wait_option** Defines how long the service will wait for the FTP Client file rename.</span></span> <span data-ttu-id="45cab-439">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-439">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-440">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-440">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-441">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-441">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-442">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-442">Return Values</span></span>

- <span data-ttu-id="45cab-443">**NX_SUCCESS** (0x00) ridenominazione del file FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-443">**NX_SUCCESS** (0x00) Successful FTP file rename.</span></span>
- <span data-ttu-id="45cab-444">Il client FTP **NX_FTP_NOT_CONNECTED** (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="45cab-444">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="45cab-445">**NX_FTP_EXPECTED_3XX_CODE** (0XDD) non ha ricevuto la risposta 3xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-445">**NX_FTP_EXPECTED_3XX_CODE** (0XDD) Did not receive 3XX (ok) response</span></span>
- <span data-ttu-id="45cab-446">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="45cab-446">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="45cab-447">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-447">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-448">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-448">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-449">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-449">Allowed From</span></span>

<span data-ttu-id="45cab-450">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-450">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-451">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-451">Example</span></span>

```C
/* Rename file “my_file.txt” to “new_file.txt” on the previously connected
    Client instance “my_client.” */

status = nx_ftp_client_file_rename(&my_client, “my_file.txt”, “new_file.txt”,
    200);

/* If status is NX_SUCCESS, the file has been renamed. */
```

## <a name="nx_ftp_client_file_write"></a><span data-ttu-id="45cab-452">nx_ftp_client_file_write</span><span class="sxs-lookup"><span data-stu-id="45cab-452">nx_ftp_client_file_write</span></span>

<span data-ttu-id="45cab-453">Scrivi nel file</span><span class="sxs-lookup"><span data-stu-id="45cab-453">Write to file</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-454">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-454">Prototype</span></span>

```C
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="45cab-455">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-455">Description</span></span>

<span data-ttu-id="45cab-456">Questo servizio scrive un pacchetto di dati nel file precedentemente aperto sul server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-456">This service writes a packet of data to the previously opened file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-457">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-457">Input Parameters</span></span>

- <span data-ttu-id="45cab-458">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-458">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-459">**packet_ptr** Puntatore di pacchetto contenente i dati da scrivere.</span><span class="sxs-lookup"><span data-stu-id="45cab-459">**packet_ptr** Packet pointer containing data to write.</span></span>
- <span data-ttu-id="45cab-460">**WAIT_OPTION** Definisce il tempo di attesa del servizio per la scrittura del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-460">**wait_option** Defines how long the service will wait for the FTP Client file write.</span></span> <span data-ttu-id="45cab-461">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="45cab-461">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="45cab-462">**valore di timeout** (0x00000001 tramite 0xfffffffe) la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-462">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="45cab-463">**TX_WAIT_FOREVER** (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER fa sì che il thread chiamante si sospenda per un tempo illimitato fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="45cab-463">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-464">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-464">Return Values</span></span>

- <span data-ttu-id="45cab-465">**NX_SUCCESS** (0x00) scrittura del file FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-465">**NX_SUCCESS** (0x00) Successful FTP file write.</span></span>
- <span data-ttu-id="45cab-466">Il client FTP **NX_FTP_NOT_OPEN** (0xD5) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="45cab-466">**NX_FTP_NOT_OPEN** (0xD5) FTP Client is not opened.</span></span>
- <span data-ttu-id="45cab-467">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-467">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-468">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-468">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-469">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-469">Allowed From</span></span>

<span data-ttu-id="45cab-470">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-470">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-471">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-471">Example</span></span>

```C
/* Write the data contained in “my_packet” to the previously opened file
    “my_file.txt”. */

status = nx_ftp_client_file_write(&my_client, my_packet, 200);

/* If status is NX_SUCCESS, the file has been written to. */
```

## <a name="nx_ftp_client_passive_mode_set"></a><span data-ttu-id="45cab-472">nx_ftp_client_passive_mode_set</span><span class="sxs-lookup"><span data-stu-id="45cab-472">nx_ftp_client_passive_mode_set</span></span>

<span data-ttu-id="45cab-473">Abilitare o disabilitare la modalità di trasferimento passivo</span><span class="sxs-lookup"><span data-stu-id="45cab-473">Enable or disable passive transfer mode</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-474">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-474">Prototype</span></span>

```C
UINT nx_ftp_client_passive_mode_set(NX_FTP_CLIENT *ftp_client_ptr,
    UINT passive_mode_enabled);
```

### <a name="description"></a><span data-ttu-id="45cab-475">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-475">Description</span></span>

<span data-ttu-id="45cab-476">Questo servizio Abilita la modalità di trasferimento passivo se l'input passive_mode_enabled è impostato su NX_TRUE su un'istanza del client FTP creata in precedenza in modo che le chiamate successive ai file di lettura o scrittura (RETR, STOR) o scaricano un elenco di directory (NLST) vengano eseguite in modalità di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="45cab-476">This service enables passive transfer mode if the passive_mode_enabled input is set to NX_TRUE on a previously created FTP Client instance such that subsequent calls to read or write files (RETR, STOR) or download a directory listing (NLST) are done in transfer mode.</span></span> <span data-ttu-id="45cab-477">Per disabilitare il trasferimento in modalità passiva e tornare al comportamento predefinito della modalità di trasferimento attivo, chiamare questa funzione con il passive_mode_enabled input impostato su NX_FALSE.</span><span class="sxs-lookup"><span data-stu-id="45cab-477">To disable passive mode transfer and return to the default behavior of active transfer mode, call this function with the passive_mode_enabled input set to NX_FALSE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-478">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-478">Input Parameters</span></span>

- <span data-ttu-id="45cab-479">**ftp_client_ptr** Puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-479">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="45cab-480">**passive_mode_enabled** Se è impostato su NX_TRUE, viene abilitata la modalità passiva.</span><span class="sxs-lookup"><span data-stu-id="45cab-480">**passive_mode_enabled** If set to NX_TRUE, passive mode is enabled.</span></span><br /><span data-ttu-id="45cab-481">Se impostato su NX_FALSE, la modalità passiva è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="45cab-481">If set to NX_FALSE, passive mode is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-482">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-482">Return Values</span></span>

- <span data-ttu-id="45cab-483">Impostazione della modalità passiva **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="45cab-483">**NX_SUCCESS** (0x00) Successful passive mode set.</span></span>
- <span data-ttu-id="45cab-484">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-484">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-485">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="45cab-485">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-486">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-486">Allowed From</span></span>

<span data-ttu-id="45cab-487">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-487">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-488">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-488">Example</span></span>

```C
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a><span data-ttu-id="45cab-489">nx_ftp_server_create</span><span class="sxs-lookup"><span data-stu-id="45cab-489">nx_ftp_server_create</span></span>

<span data-ttu-id="45cab-490">Crea server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-490">Create FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-491">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-491">Prototype</span></span>

```C
UINT nx_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
    CHAR *ftp_server_name, NX_IP *ip_ptr,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*ftp_login)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        ULONG client_ip_address,
        UINT client_port, CHAR *name, CHAR *password,
        CHAR *extra_info),
    UINT (*ftp_logout)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        ULONG client_ip_address, UINT client_port,
         CHAR *name, CHAR *password, CHAR *extra_info));
```

### <a name="description"></a><span data-ttu-id="45cab-492">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-492">Description</span></span>

<span data-ttu-id="45cab-493">Questo servizio crea un'istanza del server FTP nell'istanza IP di NetX specificata e creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45cab-493">This service creates an FTP Server instance on the specified and previously created NetX IP instance.</span></span> <span data-ttu-id="45cab-494">Si noti che è necessario avviare il server FTP con una chiamata a ***nx_ftp_server_start*** per avviare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-494">Note the FTP Server needs to be started with a call to ***nx_ftp_server_start*** for it to begin operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-495">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-495">Input Parameters</span></span>

- <span data-ttu-id="45cab-496">**ftp_server_ptr** Puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-496">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>
- <span data-ttu-id="45cab-497">**ftp_server_name** Nome del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-497">**ftp_server_name** Name of FTP Server.</span></span>
- <span data-ttu-id="45cab-498">**ip_ptr** Puntatore all'istanza IP di NetX associata.</span><span class="sxs-lookup"><span data-stu-id="45cab-498">**ip_ptr** Pointer to associated NetX IP instance.</span></span> <span data-ttu-id="45cab-499">Si noti che può essere presente un solo server FTP per un'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="45cab-499">Note there can only be one FTP Server for an IP instance.</span></span>
- <span data-ttu-id="45cab-500">**media_ptr** Puntatore all'istanza del supporto FileX associata.</span><span class="sxs-lookup"><span data-stu-id="45cab-500">**media_ptr** Pointer to associated FileX media instance.</span></span>
- <span data-ttu-id="45cab-501">**stack_ptr** Puntatore alla memoria per l'area dello stack del thread del server FTP interno.</span><span class="sxs-lookup"><span data-stu-id="45cab-501">**stack_ptr** Pointer to memory for the internal FTP Server thread’s stack area.</span></span>
- <span data-ttu-id="45cab-502">**stack_size** Dimensioni dell'area dello stack specificata dal *stack_ptr*.</span><span class="sxs-lookup"><span data-stu-id="45cab-502">**stack_size** Size of stack area specified by *stack_ptr*.</span></span>
- <span data-ttu-id="45cab-503">**pool_ptr** Puntatore al pool di pacchetti NetX predefinito.</span><span class="sxs-lookup"><span data-stu-id="45cab-503">**pool_ptr** Pointer to default NetX packet pool.</span></span> <span data-ttu-id="45cab-504">Si noti che la dimensione del payload dei pacchetti nel pool deve essere sufficientemente grande da contenere il nome file o il percorso più grande.</span><span class="sxs-lookup"><span data-stu-id="45cab-504">Note the payload size of packets in the pool must be large enough to accommodate the largest filename/path.</span></span>
- <span data-ttu-id="45cab-505">**ftp_login** Puntatore alla funzione di accesso dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-505">**ftp_login** Function pointer to application’s login function.</span></span> <span data-ttu-id="45cab-506">Questa funzione fornisce il nome utente e la password del client che richiede una connessione e l'indirizzo client nel tipo di dati ULONG.</span><span class="sxs-lookup"><span data-stu-id="45cab-506">This function is supplied the username and password from the Client requesting a connection, and the Client address in the ULONG data type.</span></span> <span data-ttu-id="45cab-507">Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="45cab-507">If this is valid, the application’s login function should return NX_SUCCESS.</span></span>
- <span data-ttu-id="45cab-508">**ftp_logout** Puntatore a funzione per la funzione di disconnessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-508">**ftp_logout** Function pointer to application’s logout function.</span></span> <span data-ttu-id="45cab-509">Questa funzione fornisce il nome utente e la password del client che richiede una disconnessione e l'indirizzo client nel tipo di dati ULONG.</span><span class="sxs-lookup"><span data-stu-id="45cab-509">This function is supplied the username and password from the Client requesting a disconnection, and the Client address in the ULONG data type.</span></span> <span data-ttu-id="45cab-510">Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="45cab-510">If this is valid, the application’s login function should return NX_SUCCESS.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-511">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-511">Return Values</span></span>

- <span data-ttu-id="45cab-512">Creazione del server FTP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="45cab-512">**NX_SUCCESS** (0x00) Successful FTP Server create.</span></span>
- <span data-ttu-id="45cab-513">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-513">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-514">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-514">Allowed From</span></span>

<span data-ttu-id="45cab-515">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="45cab-515">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-516">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-516">Example</span></span>

```C
/* Create the FTP Server “my_server” on the IP instance “ip_0” using the
    “ram_disk” media. */

status = nx_ftp_server_create(&my_server, “My Server Name”, &ip_0, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_login, my_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nxd_ftp_server_create"></a><span data-ttu-id="45cab-517">nxd_ftp_server_create</span><span class="sxs-lookup"><span data-stu-id="45cab-517">nxd_ftp_server_create</span></span>

<span data-ttu-id="45cab-518">Creazione di un server FTP con supporto IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="45cab-518">Create FTP Server with IPv4 and IPv6 support</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-519">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-519">Prototype</span></span>

```C
UINT nxd_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
    CHAR *ftp_server_name, NX_IP *ip_ptr,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*ftp_login_duo)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        NXD_ADDRESS *client_ip_address, UINT client_port, CHAR *name,
        CHAR *password, CHAR *extra_info),
    UINT (*ftp_logout_duo)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        NXD_ADDRESS *client_ip_address, UINT client_port, CHAR *name,
        CHAR *password, CHAR *extra_info));
```

### <a name="description"></a><span data-ttu-id="45cab-520">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-520">Description</span></span>

<span data-ttu-id="45cab-521">Questo servizio crea un'istanza del server FTP nell'istanza IP di NetX specificata e creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45cab-521">This service creates an FTP Server instance on the specified and previously created NetX IP instance.</span></span> <span data-ttu-id="45cab-522">Si noti che è ancora necessario avviare il server FTP con una chiamata a ***nx_ftp_server_start*** per avviare l'operazione dopo la creazione del server.</span><span class="sxs-lookup"><span data-stu-id="45cab-522">Note the FTP Server still needs to be started with a call to ***nx_ftp_server_start*** for it to begin operation after the Server is created.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-523">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-523">Input Parameters</span></span>

- <span data-ttu-id="45cab-524">**ftp_server_ptr** Puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-524">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>
- <span data-ttu-id="45cab-525">**ftp_server_name** Nome del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-525">**ftp_server_name** Name of FTP Server.</span></span>
- <span data-ttu-id="45cab-526">**ip_ptr** Puntatore all'istanza IP di NetX associata.</span><span class="sxs-lookup"><span data-stu-id="45cab-526">**ip_ptr** Pointer to associated NetX IP instance.</span></span> <span data-ttu-id="45cab-527">Si noti che può essere presente un solo server FTP per un'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="45cab-527">Note there can only be one FTP Server for an IP instance.</span></span>
- <span data-ttu-id="45cab-528">**media_ptr** Puntatore all'istanza del supporto FileX associata.</span><span class="sxs-lookup"><span data-stu-id="45cab-528">**media_ptr** Pointer to associated FileX media instance.</span></span>
- <span data-ttu-id="45cab-529">**stack_ptr** Puntatore alla memoria per l'area dello stack del thread del server FTP interno.</span><span class="sxs-lookup"><span data-stu-id="45cab-529">**stack_ptr** Pointer to memory for the internal FTP Server thread’s stack area.</span></span>
- <span data-ttu-id="45cab-530">**stack_size** Dimensioni dell'area dello stack specificata dal *stack_ptr*.</span><span class="sxs-lookup"><span data-stu-id="45cab-530">**stack_size** Size of stack area specified by *stack_ptr*.</span></span>
- <span data-ttu-id="45cab-531">**pool_ptr** Puntatore al pool di pacchetti NetX predefinito.</span><span class="sxs-lookup"><span data-stu-id="45cab-531">**pool_ptr** Pointer to default NetX packet pool.</span></span> <span data-ttu-id="45cab-532">Si noti che la dimensione del payload dei pacchetti nel pool deve essere sufficientemente grande da contenere il nome file o il percorso più grande.</span><span class="sxs-lookup"><span data-stu-id="45cab-532">Note the payload size of packets in the pool must be large enough to accommodate the largest filename/path.</span></span>
- <span data-ttu-id="45cab-533">**ftp_login_duo** Puntatore alla funzione di accesso dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-533">**ftp_login_duo** Function pointer to application’s login function.</span></span> <span data-ttu-id="45cab-534">Questa funzione fornisce il nome utente e la password del client che richiede una connessione e un puntatore all'indirizzo client nel tipo di dati NXD_ADDRESS.</span><span class="sxs-lookup"><span data-stu-id="45cab-534">This function is supplied the username and password from the Client requesting a connection, and a pointer to the Client address in the NXD_ADDRESS data type.</span></span> <span data-ttu-id="45cab-535">Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="45cab-535">If this is valid, the application’s login function should return NX_SUCCESS.</span></span>
- <span data-ttu-id="45cab-536">**ftp_logout_duo** Puntatore a funzione per la funzione di disconnessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45cab-536">**ftp_logout_duo** Function pointer to application’s logout function.</span></span> <span data-ttu-id="45cab-537">Questa funzione fornisce il nome utente e la password del client che richiede una disconnessione e un puntatore all'indirizzo client nel tipo di dati NXD_ADDRESS.</span><span class="sxs-lookup"><span data-stu-id="45cab-537">This function is supplied the username and password from the Client requesting a disconnection, and a pointer to the Client address in the NXD_ADDRESS data type.</span></span> <span data-ttu-id="45cab-538">Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="45cab-538">If this is valid, the application’s login function should return NX_SUCCESS.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-539">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-539">Return Values</span></span>

- <span data-ttu-id="45cab-540">Creazione del server FTP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="45cab-540">**NX_SUCCESS** (0x00) Successful FTP Server create.</span></span>
- <span data-ttu-id="45cab-541">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-541">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-542">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-542">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-543">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-543">Allowed From</span></span>

<span data-ttu-id="45cab-544">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="45cab-544">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-545">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-545">Example</span></span>

```C
/* Create the FTP Server “my_server” on the IP instance “ip_0” using the
    “ram_disk” media. */

status = nxd_ftp_server_create(&my_server, “My Server Name”, &ip_0, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_duo_login, my_duo_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nx_ftp_server_delete"></a><span data-ttu-id="45cab-546">nx_ftp_server_delete</span><span class="sxs-lookup"><span data-stu-id="45cab-546">nx_ftp_server_delete</span></span>

<span data-ttu-id="45cab-547">Elimina server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-547">Delete FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-548">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-548">Prototype</span></span>

```C
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="45cab-549">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-549">Description</span></span>

<span data-ttu-id="45cab-550">Questo servizio Elimina un'istanza del server FTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45cab-550">This service deletes a previously created FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-551">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-551">Input Parameters</span></span>

- <span data-ttu-id="45cab-552">**ftp_server_ptr** Puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-552">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-553">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-553">Return Values</span></span>

- <span data-ttu-id="45cab-554">Eliminazione del server FTP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="45cab-554">**NX_SUCCESS** (0x00) Successful FTP Server delete.</span></span>
- <span data-ttu-id="45cab-555">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-555">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-556">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-556">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-557">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-557">Allowed From</span></span>

<span data-ttu-id="45cab-558">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-558">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-559">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-559">Example</span></span>

```C
/* Delete the FTP Server “my_server”. */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a><span data-ttu-id="45cab-560">nx_ftp_server_start</span><span class="sxs-lookup"><span data-stu-id="45cab-560">nx_ftp_server_start</span></span>

<span data-ttu-id="45cab-561">Avvia server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-561">Start FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-562">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-562">Prototype</span></span>

```C
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="45cab-563">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-563">Description</span></span>

<span data-ttu-id="45cab-564">Questo servizio avvia un'istanza del server FTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45cab-564">This service starts a previously created FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-565">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-565">Input Parameters</span></span>

- <span data-ttu-id="45cab-566">**ftp_server_ptr** Puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-566">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-567">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-567">Return Values</span></span>

- <span data-ttu-id="45cab-568">Avvio del server FTP **NX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="45cab-568">**NX_SUCCESS** (0x00) Successful FTP Server start.</span></span>
- <span data-ttu-id="45cab-569">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-569">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-570">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-570">Allowed From</span></span>

<span data-ttu-id="45cab-571">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-571">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-572">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-572">Example</span></span>

```C
/* Start the FTP Server “my_server”. */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a><span data-ttu-id="45cab-573">nx_ftp_server_stop</span><span class="sxs-lookup"><span data-stu-id="45cab-573">nx_ftp_server_stop</span></span>

<span data-ttu-id="45cab-574">Arresta server FTP</span><span class="sxs-lookup"><span data-stu-id="45cab-574">Stop FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="45cab-575">Prototipo</span><span class="sxs-lookup"><span data-stu-id="45cab-575">Prototype</span></span>

```C
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="45cab-576">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45cab-576">Description</span></span>

<span data-ttu-id="45cab-577">Questo servizio interrompe un'istanza del server FTP creata e avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45cab-577">This service stops a previously created and started FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="45cab-578">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="45cab-578">Input Parameters</span></span>

- <span data-ttu-id="45cab-579">**ftp_server_ptr** Puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="45cab-579">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="45cab-580">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="45cab-580">Return Values</span></span>

- <span data-ttu-id="45cab-581">L'arresto del server FTP **NX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="45cab-581">**NX_SUCCESS** (0x00) Successful FTP Server stop.</span></span>
- <span data-ttu-id="45cab-582">NX_PTR_ERROR (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="45cab-582">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="45cab-583">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="45cab-583">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="45cab-584">Consentito da</span><span class="sxs-lookup"><span data-stu-id="45cab-584">Allowed From</span></span>

<span data-ttu-id="45cab-585">Thread</span><span class="sxs-lookup"><span data-stu-id="45cab-585">Threads</span></span>

### <a name="example"></a><span data-ttu-id="45cab-586">Esempio</span><span class="sxs-lookup"><span data-stu-id="45cab-586">Example</span></span>

```C
/* Stop the FTP Server “my_server”. */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
