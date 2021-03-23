---
title: Capitolo 3-Descrizione dei servizi FTP NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi FTP NetX di Azure RTO (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b05d03c45607c45acf32474cf8e40861532c5fae
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822625"
---
# <a name="chapter-3---description-of-azure-rtos-netx-ftp-services"></a><span data-ttu-id="e1d0f-103">Capitolo 3-Descrizione dei servizi FTP NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e1d0f-103">Chapter 3 - Description of Azure RTOS NetX FTP services</span></span>

<span data-ttu-id="e1d0f-104">Questo capitolo contiene una descrizione di tutti i servizi FTP NetX di Azure RTO (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-104">This chapter contains a description of all Azure RTOS NetX FTP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="e1d0f-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="e1d0f-106">**nx_ftp_client_connect**: *connettersi al server FTP*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-106">**nx_ftp_client_connect**: *Connect to FTP Server*</span></span>
- <span data-ttu-id="e1d0f-107">**nx_ftp_client_create**: *creare un'istanza del client FTP*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-107">**nx_ftp_client_create**: *Create an FTP Client instance*</span></span>
- <span data-ttu-id="e1d0f-108">**nx_ftp_client_delete**: *eliminare un'istanza del client FTP*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-108">**nx_ftp_client_delete**: *Delete an FTP Client instance*</span></span>
- <span data-ttu-id="e1d0f-109">**nx_ftp_client_directory_create**: *creare una directory nel server*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-109">**nx_ftp_client_directory_create**: *Create a directory on Server*</span></span>
- <span data-ttu-id="e1d0f-110">**nx_ftp_client_directory_default_set**: *impostare la directory predefinita nel server*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-110">**nx_ftp_client_directory_default_set**: *Set default directory on Server*</span></span>
- <span data-ttu-id="e1d0f-111">**nx_ftp_client_directory_delete**: *eliminare una directory nel server*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-111">**nx_ftp_client_directory_delete**: *Delete a directory on Server*</span></span>
- <span data-ttu-id="e1d0f-112">**nx_ftp_client_directory_listing_get**: *ottenere un elenco di directory dal server*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-112">**nx_ftp_client_directory_listing_get**: *Get directory listing from Server*</span></span>
- <span data-ttu-id="e1d0f-113">**nx_ftp_client_directory_listing_continue**: *continua la visualizzazione della directory dal server*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-113">**nx_ftp_client_directory_listing_continue**: *Continue directory listing from Server*</span></span>
- <span data-ttu-id="e1d0f-114">**nx_ftp_client_disconnect**: *disconnettersi dal server FTP*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-114">**nx_ftp_client_disconnect**: *Disconnect from FTP Server*</span></span>
- <span data-ttu-id="e1d0f-115">**nx_ftp_client_file_close**: *chiudere il file client*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-115">**nx_ftp_client_file_close**: *Close Client file*</span></span>
- <span data-ttu-id="e1d0f-116">**nx_ftp_client_file_delete**: *eliminare un file nel server*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-116">**nx_ftp_client_file_delete**: *Delete file on Server*</span></span>
- <span data-ttu-id="e1d0f-117">**nx_ftp_client_file_open**: *Apri file client*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-117">**nx_ftp_client_file_open**: *Open Client file*</span></span>
- <span data-ttu-id="e1d0f-118">**nx_ftp_client_file_read**: *lettura da file*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-118">**nx_ftp_client_file_read**: *Read from file*</span></span>
- <span data-ttu-id="e1d0f-119">**nx_ftp_client_file_rename**: *rinominare il file nel server*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-119">**nx_ftp_client_file_rename**: *Rename file on Server*</span></span>
- <span data-ttu-id="e1d0f-120">**nx_ftp_client_file_write**: *scrittura nel file*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-120">**nx_ftp_client_file_write**: *Write to file*</span></span>
- <span data-ttu-id="e1d0f-121">**nx_ftp_server_create**: *creare un server FTP*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-121">**nx_ftp_server_create**: *Create FTP Server*</span></span>
- <span data-ttu-id="e1d0f-122">**nx_ftp_server_delete**: *eliminare il server FTP*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-122">**nx_ftp_server_delete**: *Delete FTP Server*</span></span>
- <span data-ttu-id="e1d0f-123">**nx_ftp_server_start**: *avviare il server FTP*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-123">**nx_ftp_server_start**: *Start FTP Server*</span></span>
- <span data-ttu-id="e1d0f-124">**nx_ftp_server_stop**: *arrestare il server FTP*</span><span class="sxs-lookup"><span data-stu-id="e1d0f-124">**nx_ftp_server_stop**: *Stop FTP Server*</span></span>

## <a name="nx_ftp_client_connect"></a><span data-ttu-id="e1d0f-125">nx_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="e1d0f-125">nx_ftp_client_connect</span></span>

<span data-ttu-id="e1d0f-126">Connettersi a un server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-126">Connect to an FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-127">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-127">Prototype</span></span>

```c
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
        ULONG server_ip, CHAR *username, CHAR *password,
        ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-128">Description</span></span>

<span data-ttu-id="e1d0f-129">Questo servizio connette l'istanza del client FTP precedentemente creata al server FTP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-129">This service connects the previously created FTP Client instance to the FTP Server at the supplied IP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-130">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-130">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-131">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-131">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-132">**server_ip**: indirizzo IP del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-132">**server_ip**: IP address of FTP Server.</span></span>
- <span data-ttu-id="e1d0f-133">**username**: nome utente del client per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-133">**username**: Client username for authentication.</span></span>
- <span data-ttu-id="e1d0f-134">**password**: password client per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-134">**password**: Client password for authentication.</span></span>
- <span data-ttu-id="e1d0f-135">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la connessione client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-135">**wait_option**: Defines how long the service will wait for the FTP Client connection.</span></span> <span data-ttu-id="e1d0f-136">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-136">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-137">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-137">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-138">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-138">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-139">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-139">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-140">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-140">Return Values</span></span>

- <span data-ttu-id="e1d0f-141">**NX_SUCCESS**: (0x00) connessione FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-141">**NX_SUCCESS**: (0x00) Successful FTP connection.</span></span>
- <span data-ttu-id="e1d0f-142">**NX_TFTP_EXPECTED_22X_CODE**: (0xDB) non ha ricevuto una risposta 22x (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-142">**NX_TFTP_EXPECTED_22X_CODE**: (0xDB) Did not get a 22X (ok) response</span></span>
- <span data-ttu-id="e1d0f-143">**NX_FTP_EXPECTED_23X_CODE**: (0xdc) non ha ricevuto una risposta 23x (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-143">**NX_FTP_EXPECTED_23X_CODE**: (0xDC) Did not get a 23X (ok) response</span></span>
- <span data-ttu-id="e1d0f-144">**NX_FTP_EXPECTED_33X_CODE**: (0xDE) non ha ricevuto una risposta 33x (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-144">**NX_FTP_EXPECTED_33X_CODE**: (0xDE) Did not get a 33X (ok) response</span></span>
- <span data-ttu-id="e1d0f-145">**NX_FTP_NOT_DISCONNECTED**: il client (0xd4) è già connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-145">**NX_FTP_NOT_DISCONNECTED**: (0xD4) Client is already connected.</span></span>
- <span data-ttu-id="e1d0f-146">NX_PTR_ERROR: (0x07) puntatore non valido InOut.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-146">NX_PTR_ERROR: (0x07) Invalid pointer inout.</span></span>
- <span data-ttu-id="e1d0f-147">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-147">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="e1d0f-148">NX_IP_ADDRESS_ERROR: (0x21) indirizzo IP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-148">NX_IP_ADDRESS_ERROR: (0x21) Invalid IP address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-149">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-149">Allowed From</span></span>

<span data-ttu-id="e1d0f-150">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-150">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-151">Example</span></span>

```c
/* Connect the FTP Client instance "my_client" to the FTP Server at
    IP address 1.2.3.4. */
status = nx_ftp_client_connect(&my_client, IP_ADDRESS(1,2,3,4), NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
connected to the FTP Server. */
```

## <a name="nx_ftp_client_create"></a><span data-ttu-id="e1d0f-152">nx_ftp_client_create</span><span class="sxs-lookup"><span data-stu-id="e1d0f-152">nx_ftp_client_create</span></span>

<span data-ttu-id="e1d0f-153">Creare un'istanza del client FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-153">Create an FTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-154">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-154">Prototype</span></span>

```c
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="e1d0f-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-155">Description</span></span>

<span data-ttu-id="e1d0f-156">Questo servizio crea un'istanza del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-156">This service creates an FTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-157">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-157">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-158">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-158">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-159">**ftp_client_name**: nome del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-159">**ftp_client_name**: Name of FTP Client.</span></span>
- <span data-ttu-id="e1d0f-160">**ip_ptr**: puntatore all'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-160">**ip_ptr**: Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="e1d0f-161">**window_size**: dimensioni della finestra annunciata per il socket TCP del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-161">**window_size**: Advertised window size for TCP socket of this FTP Client.</span></span>
- <span data-ttu-id="e1d0f-162">**pool_ptr**: puntatore al pool di pacchetti predefinito per il client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-162">**pool_ptr**: Pointer to the default packet pool for this FTP Client.</span></span> <span data-ttu-id="e1d0f-163">Si noti che il payload del pacchetto minimo deve essere sufficientemente grande da contenere il percorso completo e il nome del file o della directory.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-163">Note that the minimum packet payload must be large enough to hold complete path and the file or directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-164">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-164">Return Values</span></span>

- <span data-ttu-id="e1d0f-165">**NX_SUCCESS**: (0x00) creazione client FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-165">**NX_SUCCESS**: (0x00) Successful FTP Client create.</span></span>
- <span data-ttu-id="e1d0f-166">NX_PTR_ERROR: (0x16) protocollo FTP, puntatore IP o puntatore al pool di pacchetti non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-166">NX_PTR_ERROR: (0x16) Invalid FTP, IP pointer, or packet pool pointer.</span></span> <span data-ttu-id="e1d0f-167">puntatore alla password.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-167">password pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-168">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-168">Allowed From</span></span>

<span data-ttu-id="e1d0f-169">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-169">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-170">Example</span></span>

```c
/* Create the FTP Client instance "my_client." */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
                                2000, &client_pool);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
created. */
```

## <a name="nx_ftp_client_delete"></a><span data-ttu-id="e1d0f-171">nx_ftp_client_delete</span><span class="sxs-lookup"><span data-stu-id="e1d0f-171">nx_ftp_client_delete</span></span>

<span data-ttu-id="e1d0f-172">Eliminare un'istanza del client FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-172">Delete an FTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-173">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-173">Prototype</span></span>

```c
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="e1d0f-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-174">Description</span></span>

<span data-ttu-id="e1d0f-175">Questo servizio Elimina un'istanza del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-175">This service deletes an FTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-176">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-176">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-177">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-177">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-178">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-178">Return Values</span></span>

- <span data-ttu-id="e1d0f-179">**NX_SUCCESS**: (0x00) eliminazione client FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-179">**NX_SUCCESS**: (0x00) Successful FTP Client delete.</span></span>
- <span data-ttu-id="e1d0f-180">**NX_FTP_NOT_DISCONNECTED**: (0xd4) errore di eliminazione del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-180">**NX_FTP_NOT_DISCONNECTED**: (0xD4) FTP Client delete error.</span></span>
- <span data-ttu-id="e1d0f-181">NX_PTR_ERROR: (0x16) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-181">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-182">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-182">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-183">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-183">Allowed From</span></span>

<span data-ttu-id="e1d0f-184">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-184">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-185">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-185">Example</span></span>

```c
/* Delete the FTP Client instance "my_client." */
status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a><span data-ttu-id="e1d0f-186">nx_ftp_client_directory_create</span><span class="sxs-lookup"><span data-stu-id="e1d0f-186">nx_ftp_client_directory_create</span></span>

<span data-ttu-id="e1d0f-187">Creare una directory nel server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-187">Create a directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-188">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-188">Prototype</span></span>

```c
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-189">Description</span></span>

<span data-ttu-id="e1d0f-190">Questo servizio crea la directory specificata nel server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-190">This service creates the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-191">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-191">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-192">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-192">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-193">**DIRECTORY_NAME**: nome della directory da creare.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-193">**directory_name**: Name of directory to create.</span></span>
- <span data-ttu-id="e1d0f-194">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la creazione della directory FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-194">**wait_option**: Defines how long the service will wait for the FTP directory create.</span></span> <span data-ttu-id="e1d0f-195">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-195">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-196">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-196">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-197">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-197">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-198">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-198">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-199">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-199">Return Values</span></span>

- <span data-ttu-id="e1d0f-200">**NX_SUCCESS**: (0x00) la creazione della directory FTP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-200">**NX_SUCCESS**: (0x00) Successful FTP directory create.</span></span>
- <span data-ttu-id="e1d0f-201">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-201">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-202">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-202">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span> 
- <span data-ttu-id="e1d0f-203">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-203">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span> 
- <span data-ttu-id="e1d0f-204">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-204">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-205">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-205">Allowed From</span></span>

<span data-ttu-id="e1d0f-206">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-206">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-207">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-207">Example</span></span>

```c
/* Create the directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_create(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" was successfully  
    created. */
```

## <a name="nx_ftp_client_directory_default_set"></a><span data-ttu-id="e1d0f-208">nx_ftp_client_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="e1d0f-208">nx_ftp_client_directory_default_set</span></span>

<span data-ttu-id="e1d0f-209">Imposta la directory predefinita nel server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-209">Set default directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-210">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-210">Prototype</span></span>

```c
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
                                CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-211">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-211">Description</span></span>

<span data-ttu-id="e1d0f-212">Questo servizio imposta la directory predefinita sul server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-212">This service sets the default directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="e1d0f-213">Questa directory predefinita si applica solo alla connessione del client.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-213">This default directory applies only to this client's connection.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-214">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-214">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-215">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-215">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-216">**directory_path**: nome del percorso della directory da impostare.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-216">**directory_path**: Name of directory path to set.</span></span>
- <span data-ttu-id="e1d0f-217">**WAIT_OPTION**: definisce per quanto tempo il servizio resterà in attesa del set di directory predefinito FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-217">**wait_option**: Defines how long the service will wait for the FTP default directory set.</span></span> <span data-ttu-id="e1d0f-218">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-218">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-219">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-219">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-220">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-220">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-221">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-221">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-222">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-222">Return Values</span></span>

- <span data-ttu-id="e1d0f-223">**NX_SUCCESS**: (0x00) il set predefinito di FTP è riuscito.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-223">**NX_SUCCESS**: (0x00) Successful FTP default set.</span></span>
- <span data-ttu-id="e1d0f-224">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-224">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-225">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-225">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span> 
- <span data-ttu-id="e1d0f-226">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-226">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span> 
- <span data-ttu-id="e1d0f-227">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-227">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-228">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-228">Allowed From</span></span>

<span data-ttu-id="e1d0f-229">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-229">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-230">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-230">Example</span></span>

```c
/* Set the default directory to "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_default_set(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a><span data-ttu-id="e1d0f-231">nx_ftp_client_directory_delete</span><span class="sxs-lookup"><span data-stu-id="e1d0f-231">nx_ftp_client_directory_delete</span></span>

<span data-ttu-id="e1d0f-232">Elimina directory nel server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-232">Delete directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-233">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-233">Prototype</span></span>

```c
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-234">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-234">Description</span></span>

<span data-ttu-id="e1d0f-235">Questo servizio Elimina la directory specificata nel server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-235">This service deletes the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-236">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-236">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-237">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-237">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-238">**DIRECTORY_NAME**: nome della directory da eliminare.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-238">**directory_name**: Name of directory to delete.</span></span>
- <span data-ttu-id="e1d0f-239">**WAIT_OPTION**: definisce per quanto tempo il servizio resterà in attesa dell'eliminazione della directory FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-239">**wait_option**: Defines how long the service will wait for the FTP directory delete.</span></span> <span data-ttu-id="e1d0f-240">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-240">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-241">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-241">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-242">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-242">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-243">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-243">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-244">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-244">Return Values</span></span>

- <span data-ttu-id="e1d0f-245">**NX_SUCCESS**: (0x00) eliminazione directory FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-245">**NX_SUCCESS**: (0x00) Successful FTP directory delete.</span></span>
- <span data-ttu-id="e1d0f-246">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-246">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-247">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-247">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span> 
- <span data-ttu-id="e1d0f-248">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-248">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span> 
- <span data-ttu-id="e1d0f-249">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-249">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-250">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-250">Allowed From</span></span>

<span data-ttu-id="e1d0f-251">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-251">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-252">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-252">Example</span></span>

```c
/* Delete directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_delete(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a><span data-ttu-id="e1d0f-253">nx_ftp_client_directory_listing_get</span><span class="sxs-lookup"><span data-stu-id="e1d0f-253">nx_ftp_client_directory_listing_get</span></span>

<span data-ttu-id="e1d0f-254">Ottenere l'elenco di directory dal server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-254">Get directory listing from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-255">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-255">Prototype</span></span>

```c
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
                            CHAR *directory_name, NX_PACKET **packet_ptr,
                            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-256">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-256">Description</span></span>

<span data-ttu-id="e1d0f-257">Questo servizio ottiene il contenuto della directory specificata nel server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-257">This service gets the contents of the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="e1d0f-258">Il puntatore al pacchetto fornito conterrà una o più voci di directory.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-258">The supplied packet pointer will contain one or more directory entries.</span></span> <span data-ttu-id="e1d0f-259">Ogni voce è separata da una &lt; combinazione CR/LF \.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-259">Each entry is separated by a &lt;cr/lf\combination.</span></span> <span data-ttu-id="e1d0f-260">Per completare l'operazione di Get della directory è necessario chiamare il ***nx_ftp_client_directory_listing_continue***:.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-260">The ***nx_ftp_client_directory_listing_continue***: should be called to complete the directory get operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-261">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-261">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-262">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-262">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-263">**DIRECTORY_NAME**: nome della directory da cui ottenere il contenuto.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-263">**directory_name**: Name of directory to get contents of.</span></span>
- <span data-ttu-id="e1d0f-264">**packet_ptr**: puntatore al puntatore del pacchetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-264">**packet_ptr**: Pointer to destination packet pointer.</span></span> <span data-ttu-id="e1d0f-265">In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-265">If successful, the packet payload will contain one or more directory entries.</span></span>
- <span data-ttu-id="e1d0f-266">**WAIT_OPTION**: definisce il tempo di attesa del servizio per l'elenco di directory FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-266">**wait_option**: Defines how long the service will wait for the FTP directory listing.</span></span> <span data-ttu-id="e1d0f-267">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-267">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-268">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-268">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-269">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-269">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-270">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-270">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-271">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-271">Return Values</span></span>

- <span data-ttu-id="e1d0f-272">**NX_SUCCESS**: (0x00) elenco di directory FTP riuscite.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-272">**NX_SUCCESS**: (0x00) Successful FTP directory listing.</span></span>
- <span data-ttu-id="e1d0f-273">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-273">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-274">**NX_NOT_ENABLED**: (0X14) servizio (IPv6) non abilitato</span><span class="sxs-lookup"><span data-stu-id="e1d0f-274">**NX_NOT_ENABLED**: (0x14) Service (IPv6) not enabled</span></span>
- <span data-ttu-id="e1d0f-275">**NX_FTP_EXPECTED_1XX_CODE**: (0xD9) non ha ricevuto una risposta 1xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-275">**NX_FTP_EXPECTED_1XX_CODE**: (0xD9) Did not get a 1XX (ok) response</span></span>
- <span data-ttu-id="e1d0f-276">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-276">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="e1d0f-277">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-277">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-278">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-278">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-279">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-279">Allowed From</span></span>

<span data-ttu-id="e1d0f-280">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-280">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-281">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-281">Example</span></span>

```c
/* Get the contents of directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_listing_get(&my_client, "my_dir", &my_packet,
                                            200);

/* If status is NX_SUCCESS, one or more entries of the directory "my_dir"
    can be found in "my_packet". */
```

## <a name="nx_ftp_client_directory_listing_continue"></a><span data-ttu-id="e1d0f-282">nx_ftp_client_directory_listing_continue</span><span class="sxs-lookup"><span data-stu-id="e1d0f-282">nx_ftp_client_directory_listing_continue</span></span>

<span data-ttu-id="e1d0f-283">Continua Inserzione directory dal server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-283">Continue directory listing from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-284">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-284">Prototype</span></span>

```c
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT
                    *ftp_client_ptr, NX_PACKET **packet_ptr,
                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-285">Description</span></span>

<span data-ttu-id="e1d0f-286">Questo servizio continua a ottenere il contenuto della directory specificata nel server FTP connesso al client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-286">This service continues getting the contents of the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="e1d0f-287">Dovrebbe essere stato immediatamente preceduto da una chiamata a ***nx_ftp_client_directory_listing_get***.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-287">It should have been immediately preceded by a call to ***nx_ftp_client_directory_listing_get***.</span></span> <span data-ttu-id="e1d0f-288">In caso di esito positivo, il puntatore al pacchetto fornito conterrà una o più voci di directory.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-288">If successful, the supplied packet pointer will contain one or more directory entries.</span></span> <span data-ttu-id="e1d0f-289">Questa routine deve essere chiamata fino a quando non viene ricevuto uno stato di NX_FTP_END_OF_LISTING.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-289">This routine should be called until an NX_FTP_END_OF_LISTING status is received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-290">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-290">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-291">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-291">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-292">**packet_ptr**: puntatore al puntatore del pacchetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-292">**packet_ptr**: Pointer to destination packet pointer.</span></span> <span data-ttu-id="e1d0f-293">In caso di esito positivo, il payload del pacchetto conterrà una o più voci di directory, separate da &lt; CR/LF &gt; .</span><span class="sxs-lookup"><span data-stu-id="e1d0f-293">If successful, the packet payload will contain one or more directory entries, separated by a &lt;cr/lf&gt;.</span></span>
- <span data-ttu-id="e1d0f-294">**WAIT_OPTION**: definisce il tempo di attesa del servizio per l'elenco di directory FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-294">**wait_option**: Defines how long the service will wait for the FTP directory listing.</span></span> <span data-ttu-id="e1d0f-295">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-295">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-296">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-296">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-297">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-297">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-298">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-298">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-299">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-299">Return Values</span></span>

- <span data-ttu-id="e1d0f-300">**NX_SUCCESS**: (0x00) elenco di directory FTP riuscite.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-300">**NX_SUCCESS**: (0x00) Successful FTP directory listing.</span></span>
- <span data-ttu-id="e1d0f-301">**NX_FTP_END_OF_LISTING**: (0XD8) non sono presenti altre voci in questa directory.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-301">**NX_FTP_END_OF_LISTING**: (0xD8) No more entries in this directory.</span></span>
- <span data-ttu-id="e1d0f-302">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-302">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-303">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-303">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="e1d0f-304">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-304">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-305">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-305">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-306">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-306">Allowed From</span></span>

<span data-ttu-id="e1d0f-307">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-307">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-308">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-308">Example</span></span>

```c
/* Continue getting the contents of directory "my_dir" on the FTP Server
    connected to the FTP Client instance "my_client." */
status = nx_ftp_client_directory_listing_continue(&my_client, &my_packet,
                                                200);

/* If status is NX_SUCCESS, one or more entries of the directory "my_dir"
    can be found in "my_packet". */
```

## <a name="nx_ftp_client_disconnect"></a><span data-ttu-id="e1d0f-309">nx_ftp_client_disconnect</span><span class="sxs-lookup"><span data-stu-id="e1d0f-309">nx_ftp_client_disconnect</span></span>

<span data-ttu-id="e1d0f-310">Disconnetti dal server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-310">Disconnect from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-311">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-311">Prototype</span></span>

```c
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-312">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-312">Description</span></span>

<span data-ttu-id="e1d0f-313">Questo servizio disconnette una connessione al server FTP stabilita in precedenza con il client FTP specificato.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-313">This service disconnects a previously established FTP Server connection with the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-314">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-314">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-315">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-315">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-316">**WAIT_OPTION**: definisce per quanto tempo il servizio attenderà la disconnessione del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-316">**wait_option**: Defines how long the service will wait for the FTP Client disconnect.</span></span> <span data-ttu-id="e1d0f-317">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-317">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-318">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-318">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-319">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-319">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-320">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-320">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-321">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-321">Return Values</span></span>

- <span data-ttu-id="e1d0f-322">**NX_SUCCESS**: (0x00) la DISconnessione FTP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-322">**NX_SUCCESS**: (0x00) Successful FTP disconnect.</span></span>
- <span data-ttu-id="e1d0f-323">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-323">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-324">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-324">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="e1d0f-325">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-325">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-326">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-326">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-327">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-327">Allowed From</span></span>

<span data-ttu-id="e1d0f-328">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-328">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-329">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-329">Example</span></span>

```c
/* Disconnect "my_client" from the FTP Server. */
status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, "my_client" has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a><span data-ttu-id="e1d0f-330">nx_ftp_client_file_close</span><span class="sxs-lookup"><span data-stu-id="e1d0f-330">nx_ftp_client_file_close</span></span>

<span data-ttu-id="e1d0f-331">Chiudi file client</span><span class="sxs-lookup"><span data-stu-id="e1d0f-331">Close Client file</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-332">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-332">Prototype</span></span>

```c
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-333">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-333">Description</span></span>

<span data-ttu-id="e1d0f-334">Questo servizio chiude un file aperto in precedenza nel server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-334">This service closes a previously opened file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-335">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-335">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-336">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-336">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-337">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la chiusura del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-337">**wait_option**: Defines how long the service will wait for the FTP Client file close.</span></span> <span data-ttu-id="e1d0f-338">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-338">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-339">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-339">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-340">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-340">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-341">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-341">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-342">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-342">Return Values</span></span>

- <span data-ttu-id="e1d0f-343">**NX_SUCCESS**: (0x00) chiusura file FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-343">**NX_SUCCESS**: (0x00) Successful FTP file close.</span></span>
- <span data-ttu-id="e1d0f-344">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-344">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-345">**NX_FTP_NOT_OPEN (0xD5)**: file non aperto; impossibile chiuderla</span><span class="sxs-lookup"><span data-stu-id="e1d0f-345">**NX_FTP_NOT_OPEN (0xD5)**: File not open; cannot close it</span></span>
- <span data-ttu-id="e1d0f-346">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-346">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="e1d0f-347">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-347">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-348">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-348">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-349">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-349">Allowed From</span></span>

<span data-ttu-id="e1d0f-350">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-350">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-351">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-351">Example</span></span>

```c
/* Close previously opened file of client "my_client" on the FTP Server. */
status = nx_ftp_client_file_close(&my_client, 200);

/* If status is NX_SUCCESS, the file opened previously in the "my_client" FTP
    connection has been closed. */
```

## <a name="nx_ftp_client_file_delete"></a><span data-ttu-id="e1d0f-352">nx_ftp_client_file_delete</span><span class="sxs-lookup"><span data-stu-id="e1d0f-352">nx_ftp_client_file_delete</span></span>

<span data-ttu-id="e1d0f-353">Elimina file nel server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-353">Delete file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-354">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-354">Prototype</span></span>

```c
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-355">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-355">Description</span></span>

<span data-ttu-id="e1d0f-356">Questo servizio Elimina il file specificato sul server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-356">This service deletes the specified file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-357">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-357">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-358">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-358">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-359">**file_name**: nome del file da eliminare.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-359">**file_name**: Name of file to delete.</span></span>
- <span data-ttu-id="e1d0f-360">**WAIT_OPTION**: definisce per quanto tempo il servizio resterà in attesa dell'eliminazione del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-360">**wait_option**: Defines how long the service will wait for the FTP Client file delete.</span></span> <span data-ttu-id="e1d0f-361">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-361">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-362">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-362">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-363">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-363">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-364">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-364">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-365">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-365">Return Values</span></span>

- <span data-ttu-id="e1d0f-366">**NX_SUCCESS**: (0x00) eliminazione file FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-366">**NX_SUCCESS**: (0x00) Successful FTP file delete.</span></span>
- <span data-ttu-id="e1d0f-367">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-367">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-368">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-368">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="e1d0f-369">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-369">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-370">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-370">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-371">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-371">Allowed From</span></span>

<span data-ttu-id="e1d0f-372">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-372">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-373">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-373">Example</span></span>

```c
/* Delete the file "my_file.txt" on the FTP Server using the previously
    connected client "my_client." */
status = nx_ftp_client_file_delete(&my_client, "my_file.txt", 200);

/* If status is NX_SUCCESS, the file "my_file.txt" on the FTP Server is
    deleted. */
```

## <a name="nx_ftp_client_file_open"></a><span data-ttu-id="e1d0f-374">nx_ftp_client_file_open</span><span class="sxs-lookup"><span data-stu-id="e1d0f-374">nx_ftp_client_file_open</span></span>

<span data-ttu-id="e1d0f-375">Apre il file nel server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-375">Opens file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-376">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-376">Prototype</span></span>

```c
UINT nx_ftp_client_file_open(NX_FTP_CLIENT *ftp_client_ptr,
        CHAR *file_name, UINT open_type, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-377">Description</span></span>

<span data-ttu-id="e1d0f-378">Questo servizio apre il file specificato, per la lettura o la scrittura, sul server FTP precedentemente connesso all'istanza client specificata.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-378">This service opens the specified file – for reading or writing – on the FTP Server previously connected to the specified Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-379">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-379">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-380">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-380">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-381">**file_name**: nome del file da aprire.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-381">**file_name**: Name of file to open.</span></span>
- <span data-ttu-id="e1d0f-382">**open_type**: **NX_FTP_OPEN_FOR_READ** o **NX_FTP_OPEN_FOR_WRITE**.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-382">**open_type**: Either **NX_FTP_OPEN_FOR_READ** or **NX_FTP_OPEN_FOR_WRITE**.</span></span>
- <span data-ttu-id="e1d0f-383">**WAIT_OPTION**: definisce il tempo di attesa del servizio per l'apertura del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-383">**wait_option**: Defines how long the service will wait for the FTP Client file open.</span></span> <span data-ttu-id="e1d0f-384">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-384">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-385">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-385">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-386">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-386">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-387">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-387">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-388">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-388">Return Values</span></span>

- <span data-ttu-id="e1d0f-389">**NX_SUCCESS**: (0x00) l'apertura del file FTP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-389">**NX_SUCCESS**: (0x00) Successful FTP file open.</span></span>
- <span data-ttu-id="e1d0f-390">**NX_OPTION_ERROR**: (0x0A) tipo aperto non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-390">**NX_OPTION_ERROR**: (0x0A) Invalid open type.</span></span>
- <span data-ttu-id="e1d0f-391">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-391">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-392">**NX_FTP_NOT_CLOSED**: il client FTP (0xD6) è già aperto.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-392">**NX_FTP_NOT_CLOSED**: (0xD6) FTP Client is already opened.</span></span>
- <span data-ttu-id="e1d0f-393">**NX_NO_FREE_PORTS**: (0X45) non sono disponibili porte TCP da assegnare</span><span class="sxs-lookup"><span data-stu-id="e1d0f-393">**NX_NO_FREE_PORTS**: (0x45) No TCP ports available to assign</span></span>
- <span data-ttu-id="e1d0f-394">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-394">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-395">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-395">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-396">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-396">Allowed From</span></span>

<span data-ttu-id="e1d0f-397">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-397">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-398">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-398">Example</span></span>

```c
/* Open the file "my_file.txt" for reading on the FTP Server using the previously
    connected client "my_client." */
status = nx_ftp_client_file_open(&my_client, "my_file.txt", NX_FTP_OPEN_FOR_READ,
                                200);

/* If status is NX_SUCCESS, the file "my_file.txt" on the FTP Server is
    open for reading. */
```

## <a name="nx_ftp_client_file_read"></a><span data-ttu-id="e1d0f-399">nx_ftp_client_file_read</span><span class="sxs-lookup"><span data-stu-id="e1d0f-399">nx_ftp_client_file_read</span></span>

<span data-ttu-id="e1d0f-400">Lettura da file</span><span class="sxs-lookup"><span data-stu-id="e1d0f-400">Read from file</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-401">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-401">Prototype</span></span>

```c
UINT nx_ftp_client_file_read(NX_FTP_CLIENT *ftp_client_ptr,
                NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-402">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-402">Description</span></span>

<span data-ttu-id="e1d0f-403">Questo servizio legge un pacchetto da un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-403">This service reads a packet from a previously opened file.</span></span> <span data-ttu-id="e1d0f-404">Deve essere chiamato ripetutamente fino a quando non viene ricevuto uno stato di NX_FTP_END_OF_FILE.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-404">It should be called repetitively until a status of NX_FTP_END_OF_FILE is received.</span></span>

<span data-ttu-id="e1d0f-405">Si noti che il chiamante non alloca un pacchetto per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-405">Note that the caller does not allocate a packet for this service.</span></span>  <span data-ttu-id="e1d0f-406">È necessario fornire solo un puntatore a un puntatore di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-406">It need only supply a pointer to a packet pointer.</span></span> <span data-ttu-id="e1d0f-407">Questo servizio aggiornerà il puntatore del pacchetto in modo che punti a un pacchetto recuperato dalla coda di ricezione del socket.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-407">This service will update that packet pointer to point to a packet retrieved from the socket receive queue.</span></span>  <span data-ttu-id="e1d0f-408">Se viene restituito uno stato di esito positivo, significa che è disponibile un pacchetto ed è responsabilità del chiamante rilasciare il pacchetto quando viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-408">If a successful status is returned, that means there was a packet available, and it is the caller's responsibility to release the packet when it is done with it.</span></span>

<span data-ttu-id="e1d0f-409">Se viene restituito uno stato diverso da zero (stato di errore o NX_FTP_END_OF_FILE), il chiamante non rilascia il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-409">If a non-zero status (either an error status or NX_FTP_END_OF_FILE) is returned, the caller does not release the packet.</span></span> <span data-ttu-id="e1d0f-410">In caso contrario, viene generato un errore se il puntatore del pacchetto è NULL.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-410">Otherwise, an error is generated when if the packet pointer is NULL.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-411">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-411">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-412">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-412">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-413">**packet_ptr**: puntatore alla destinazione per il puntatore al pacchetto di dati recuperato dalla coda.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-413">**packet_ptr**: Pointer to destination for the data packet pointer retrieved from the queue.</span></span> <span data-ttu-id="e1d0f-414">In caso di esito positivo, i dati del pacchetto contengono parte o tutto il file.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-414">If successful, the packet data contains some or all of the file.</span></span>
- <span data-ttu-id="e1d0f-415">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la lettura del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-415">**wait_option**: Defines how long the service will wait for the FTP Client file read.</span></span> <span data-ttu-id="e1d0f-416">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-416">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-417">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-417">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-418">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-418">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-419">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-419">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-420">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-420">Return Values</span></span>

- <span data-ttu-id="e1d0f-421">**NX_SUCCESS**: (0x00) la lettura del file FTP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-421">**NX_SUCCESS**: (0x00) Successful FTP file read.</span></span>
- <span data-ttu-id="e1d0f-422">**NX_FTP_NOT_OPEN**: il client FTP (0xD5) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-422">**NX_FTP_NOT_OPEN**: (0xD5) FTP Client is not opened.</span></span>
- <span data-ttu-id="e1d0f-423">**NX_FTP_END_OF_FILE**: (0xD7) la condizione di fine del file.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-423">**NX_FTP_END_OF_FILE**: (0xD7) End of file condition.</span></span>
- <span data-ttu-id="e1d0f-424">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-424">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-425">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-425">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-426">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-426">Allowed From</span></span>

<span data-ttu-id="e1d0f-427">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-427">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-428">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-428">Example</span></span>

```c
       NX_PACKET   *my_packet;

/* Read a packet of data from the file "my_file.txt" that was previously opened
    from the client "my_client." */

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

/* If status is NX_SUCCESS, the packet pointer, "my_packet" points to the packet
that contains the next bytes from the file. If the file is completely
downloaded, an NX_FTP_END_OF_FILE status is returned (no packet retrieved). */
```

## <a name="nx_ftp_client_file_rename"></a><span data-ttu-id="e1d0f-429">nx_ftp_client_file_rename</span><span class="sxs-lookup"><span data-stu-id="e1d0f-429">nx_ftp_client_file_rename</span></span>

<span data-ttu-id="e1d0f-430">Rinomina file nel server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-430">Rename file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-431">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-431">Prototype</span></span>

```c
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
                                CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-432">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-432">Description</span></span>

<span data-ttu-id="e1d0f-433">Questo servizio Rinomina un file nel server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-433">This service renames a file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-434">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-434">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-435">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-435">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-436">**filename**: nome corrente del file.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-436">**filename**: Current name of file.</span></span>
- <span data-ttu-id="e1d0f-437">**new_filename**: nuovo nome per il file.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-437">**new_filename**: New name for file.</span></span>
- <span data-ttu-id="e1d0f-438">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la ridenominazione del file client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-438">**wait_option**: Defines how long the service will wait for the FTP Client file rename.</span></span> <span data-ttu-id="e1d0f-439">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-439">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-440">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-440">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-441">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-441">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-442">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-442">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-443">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-443">Return Values</span></span>

- <span data-ttu-id="e1d0f-444">**NX_SUCCESS**: (0x00) la ridenominazione del file FTP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-444">**NX_SUCCESS**: (0x00) Successful FTP file rename.</span></span>
- <span data-ttu-id="e1d0f-445">**NX_FTP_NOT_CONNECTED**: il client FTP (0xD3) non è connesso.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-445">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="e1d0f-446">**NX_FTP_EXPECTED_3XX_CODE**: (0XDD) non ha ricevuto la risposta 3xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-446">**NX_FTP_EXPECTED_3XX_CODE**: (0XDD) Did not receive 3XX (ok) response</span></span>
- <span data-ttu-id="e1d0f-447">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) non ha ricevuto una risposta 2xx (OK)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-447">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="e1d0f-448">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-448">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-449">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-449">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-450">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-450">Allowed From</span></span>

<span data-ttu-id="e1d0f-451">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-451">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-452">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-452">Example</span></span>

```c
/* Rename file "my_file.txt" to "new_file.txt" on the previously connected
    Client instance "my_client." */

status = nx_ftp_client_file_rename(&my_client, "my_file.txt", "new_file.txt",
                                    200);

/* If status is NX_SUCCESS, the file has been renamed. */
```

## <a name="nx_ftp_client_file_write"></a><span data-ttu-id="e1d0f-453">nx_ftp_client_file_write</span><span class="sxs-lookup"><span data-stu-id="e1d0f-453">nx_ftp_client_file_write</span></span>

<span data-ttu-id="e1d0f-454">Scrivi nel file</span><span class="sxs-lookup"><span data-stu-id="e1d0f-454">Write to file</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-455">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-455">Prototype</span></span>

```c
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
                    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="e1d0f-456">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-456">Description</span></span>

<span data-ttu-id="e1d0f-457">Questo servizio scrive un pacchetto di dati nel file precedentemente aperto sul server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-457">This service writes a packet of data to the previously opened file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-458">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-458">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-459">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-459">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-460">**packet_ptr**: puntatore al pacchetto contenente i dati da scrivere.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-460">**packet_ptr**: Packet pointer containing data to write.</span></span>
- <span data-ttu-id="e1d0f-461">**WAIT_OPTION**: definisce il tempo di attesa del servizio per la scrittura del file del client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-461">**wait_option**: Defines how long the service will wait for the FTP Client file write.</span></span> <span data-ttu-id="e1d0f-462">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-462">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="e1d0f-463">**valore di timeout**: (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="e1d0f-463">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="e1d0f-464">**TX_WAIT_FOREVER**: (0xFFFFFFFF) la selezione di TX_WAIT_FOREVER determina la sospensione illimitata del thread chiamante fino a quando un server FTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-464">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="e1d0f-465">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-465">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-466">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-466">Return Values</span></span>

- <span data-ttu-id="e1d0f-467">**NX_SUCCESS**: (0x00) scrittura del file FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-467">**NX_SUCCESS**: (0x00) Successful FTP file write.</span></span>
- <span data-ttu-id="e1d0f-468">**NX_FTP_NOT_OPEN**: il client FTP (0xD5) non è aperto.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-468">**NX_FTP_NOT_OPEN**: (0xD5) FTP Client is not opened.</span></span>
- <span data-ttu-id="e1d0f-469">NX_PTR_ERROR: (0x07) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-469">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-470">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-470">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-471">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-471">Allowed From</span></span>

<span data-ttu-id="e1d0f-472">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-472">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-473">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-473">Example</span></span>

```c
/* Write the data contained in "my_packet" to the previously opened file
    "my_file.txt". */

status = nx_ftp_client_file_write(&my_client, my_packet, 200);

/* If status is NX_SUCCESS, the file has been written to. */
```

## <a name="nx_ftp_client_passive_mode_set"></a><span data-ttu-id="e1d0f-474">nx_ftp_client_passive_mode_set</span><span class="sxs-lookup"><span data-stu-id="e1d0f-474">nx_ftp_client_passive_mode_set</span></span>

<span data-ttu-id="e1d0f-475">Abilitare o disabilitare la modalità di trasferimento passivo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-475">Enable or disable passive transfer mode</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-476">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-476">Prototype</span></span>

```c
UINT nx_ftp_client_passive_mode_set(NX_FTP_CLIENT *ftp_client_ptr,
                                    UINT passive_mode_enabled);
```

### <a name="description"></a><span data-ttu-id="e1d0f-477">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-477">Description</span></span>

<span data-ttu-id="e1d0f-478">Questo servizio Abilita la modalità di trasferimento passivo se l'input passive_mode_enabled è impostato su NX_TRUE su un'istanza del client FTP creata in precedenza in modo che le chiamate successive ai file di lettura o scrittura (RETR, STOR) o scaricano un elenco di directory (NLST) vengano eseguite in modalità di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-478">This service enables passive transfer mode if the passive_mode_enabled input is set to NX_TRUE on a previously created FTP Client instance such that subsequent calls to read or write files (RETR, STOR) or download a directory listing (NLST) are done in transfer mode.</span></span> <span data-ttu-id="e1d0f-479">Per disabilitare il trasferimento in modalità passiva e tornare al comportamento predefinito della modalità di trasferimento attivo, chiamare questa funzione con il passive_mode_enabled input impostato su NX_FALSE.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-479">To disable passive mode transfer and return to the default behavior of active transfer mode, call this function with the passive_mode_enabled input set to NX_FALSE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-480">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-480">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-481">**ftp_client_ptr**: puntatore al blocco di controllo client FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-481">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="e1d0f-482">**passive_mode_enabled**:</span><span class="sxs-lookup"><span data-stu-id="e1d0f-482">**passive_mode_enabled**:</span></span>
  - <span data-ttu-id="e1d0f-483">Se è impostato su NX_TRUE, viene abilitata la modalità passiva.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-483">If set to NX_TRUE, passive mode is enabled.</span></span>
  - <span data-ttu-id="e1d0f-484">Se impostato su NX_FALSE, la modalità passiva è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-484">If set to NX_FALSE, passive mode is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-485">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-485">Return Values</span></span>

- <span data-ttu-id="e1d0f-486">**NX_SUCCESS**: (0x00) impostato in modalità passiva riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-486">**NX_SUCCESS**: (0x00) Successful passive mode set.</span></span>
- <span data-ttu-id="e1d0f-487">NX_PTR_ERROR: (0x16) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-487">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-488">NX_INVALID_PARAMETERS: (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="e1d0f-488">NX_INVALID_PARAMETERS: (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-489">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-489">Allowed From</span></span>

<span data-ttu-id="e1d0f-490">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-490">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-491">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-491">Example</span></span>

```c
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a><span data-ttu-id="e1d0f-492">nx_ftp_server_create</span><span class="sxs-lookup"><span data-stu-id="e1d0f-492">nx_ftp_server_create</span></span>

<span data-ttu-id="e1d0f-493">Crea server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-493">Create FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-494">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-494">Prototype</span></span>

```c
UINT nx_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
        CHAR *ftp_server_name, NX_IP *ip_ptr,
        FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
        NX_PACKET_POOL *pool_ptr,
        UINT (*ftp_login)(struct NX_FTP_SERVER_STRUCT
                *ftp_server_ptr, ULONG client_ip_address,
                UINT client_port, CHAR *name, CHAR *password,
                CHAR *extra_info),
        UINT (*ftp_logout)(struct NX_FTP_SERVER_STRUCT
                *ftp_server_ptr, ULONG client_ip_address,
                UINT client_port, CHAR *name, CHAR *password,
                CHAR *extra_info));
```

### <a name="description"></a><span data-ttu-id="e1d0f-495">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-495">Description</span></span>

<span data-ttu-id="e1d0f-496">Questo servizio crea un'istanza del server FTP nell'istanza IP di NetX specificata e creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-496">This service creates an FTP Server instance on the specified and previously created NetX IP instance.</span></span> <span data-ttu-id="e1d0f-497">Si noti che è necessario avviare il server FTP con una chiamata a ***nx_ftp_server_start*** per avviare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-497">Note the FTP Server needs to be started with a call to ***nx_ftp_server_start*** for it to begin operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-498">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-498">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-499">**ftp_server_ptr**: puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-499">**ftp_server_ptr**: Pointer to FTP Server control block.</span></span>
- <span data-ttu-id="e1d0f-500">**ftp_server_name**: nome del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-500">**ftp_server_name**: Name of FTP Server.</span></span>
- <span data-ttu-id="e1d0f-501">**ip_ptr**: puntatore all'istanza IP NETX associata.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-501">**ip_ptr**: Pointer to associated NetX IP instance.</span></span> <span data-ttu-id="e1d0f-502">Si noti che può essere presente un solo server FTP per un'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-502">Note there can only be one FTP Server for an IP instance.</span></span>
- <span data-ttu-id="e1d0f-503">**media_ptr**: puntatore all'istanza del supporto FILEX associata.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-503">**media_ptr**: Pointer to associated FileX media instance.</span></span>
- <span data-ttu-id="e1d0f-504">**stack_ptr**: puntatore alla memoria per l'area dello stack del thread del server FTP interno.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-504">**stack_ptr**: Pointer to memory for the internal FTP Server thread's stack area.</span></span>
- <span data-ttu-id="e1d0f-505">**stack_size**: dimensioni dell'area dello stack specificata da *stack_ptr*.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-505">**stack_size**: Size of stack area specified by *stack_ptr*.</span></span>
- <span data-ttu-id="e1d0f-506">**pool_ptr**: puntatore al pool di pacchetti NETX predefinito.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-506">**pool_ptr**: Pointer to default NetX packet pool.</span></span> <span data-ttu-id="e1d0f-507">Si noti che la dimensione del payload dei pacchetti nel pool deve essere sufficientemente grande da contenere il nome file o il percorso più grande.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-507">Note the payload size of packets in the pool must be large enough to accommodate the largest filename/path.</span></span>
- <span data-ttu-id="e1d0f-508">**ftp_login**: puntatore a funzione per la funzione di accesso dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-508">**ftp_login**: Function pointer to application's login function.</span></span> <span data-ttu-id="e1d0f-509">Questa funzione fornisce il nome utente e la password del client che richiede una connessione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-509">This function is supplied the username and password from the Client requesting a connection.</span></span> <span data-ttu-id="e1d0f-510">Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-510">If this is valid, the application's login function should return NX_SUCCESS.</span></span>
- <span data-ttu-id="e1d0f-511">**ftp_logout**: puntatore a funzione per la funzione di disconnessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-511">**ftp_logout**: Function pointer to application's logout function.</span></span> <span data-ttu-id="e1d0f-512">Questa funzione fornisce il nome utente e la password del client che richiede una disconnessione.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-512">This function is supplied the username and password from the Client requesting a disconnection.</span></span> <span data-ttu-id="e1d0f-513">Se è valido, la funzione di accesso dell'applicazione deve restituire NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-513">If this is valid, the application's login function should return NX_SUCCESS.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-514">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-514">Return Values</span></span>

- <span data-ttu-id="e1d0f-515">**NX_SUCCESS**: (0x00) la creazione del server FTP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-515">**NX_SUCCESS**: (0x00) Successful FTP Server create.</span></span>
- <span data-ttu-id="e1d0f-516">NX_PTR_ERROR: (0x16) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-516">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-517">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-517">Allowed From</span></span>

<span data-ttu-id="e1d0f-518">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-518">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-519">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-519">Example</span></span>

```c
/* Create the FTP Server "my_server" on the IP instance "ip_0" using the
    "ram_disk" media. */

status = nx_ftp_server_create(&my_server, "My Server Name", &ip_0, &ram_disk,
                                stack_ptr, stack_size, &pool_0,
                                my_login, my_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nx_ftp_server_delete"></a><span data-ttu-id="e1d0f-520">nx_ftp_server_delete</span><span class="sxs-lookup"><span data-stu-id="e1d0f-520">nx_ftp_server_delete</span></span>

<span data-ttu-id="e1d0f-521">Elimina server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-521">Delete FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-522">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-522">Prototype</span></span>

```c
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="e1d0f-523">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-523">Description</span></span>

<span data-ttu-id="e1d0f-524">Questo servizio Elimina un'istanza del server FTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-524">This service deletes a previously created FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-525">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-525">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-526">**ftp_server_ptr**: puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-526">**ftp_server_ptr**: Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-527">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-527">Return Values</span></span>

- <span data-ttu-id="e1d0f-528">**NX_SUCCESS**: (0x00) eliminazione del server FTP riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-528">**NX_SUCCESS**: (0x00) Successful FTP Server delete.</span></span>
- <span data-ttu-id="e1d0f-529">NX_PTR_ERROR: (0x16) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-529">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-530">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-530">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-531">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-531">Allowed From</span></span>

<span data-ttu-id="e1d0f-532">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-532">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-533">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-533">Example</span></span>

```c
/* Delete the FTP Server "my_server". */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a><span data-ttu-id="e1d0f-534">nx_ftp_server_start</span><span class="sxs-lookup"><span data-stu-id="e1d0f-534">nx_ftp_server_start</span></span>

<span data-ttu-id="e1d0f-535">Avvia server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-535">Start FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-536">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-536">Prototype</span></span>

```c
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="e1d0f-537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-537">Description</span></span>

<span data-ttu-id="e1d0f-538">Questo servizio avvia un'istanza del server FTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-538">This service starts a previously created FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-539">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-539">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-540">**ftp_server_ptr**: puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-540">**ftp_server_ptr**: Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-541">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-541">Return Values</span></span>

- <span data-ttu-id="e1d0f-542">**NX_SUCCESS**: (0x00) avvio del server FTP riuscito.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-542">**NX_SUCCESS**: (0x00) Successful FTP Server start.</span></span>
- <span data-ttu-id="e1d0f-543">NX_PTR_ERROR: (0x16) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-543">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-544">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-544">Allowed From</span></span>

<span data-ttu-id="e1d0f-545">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-545">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-546">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-546">Example</span></span>

```c
/* Start the FTP Server "my_server". */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a><span data-ttu-id="e1d0f-547">nx_ftp_server_stop</span><span class="sxs-lookup"><span data-stu-id="e1d0f-547">nx_ftp_server_stop</span></span>

<span data-ttu-id="e1d0f-548">Arresta server FTP</span><span class="sxs-lookup"><span data-stu-id="e1d0f-548">Stop FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="e1d0f-549">Prototipo</span><span class="sxs-lookup"><span data-stu-id="e1d0f-549">Prototype</span></span>

```c
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="e1d0f-550">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1d0f-550">Description</span></span>

<span data-ttu-id="e1d0f-551">Questo servizio interrompe un'istanza del server FTP creata e avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-551">This service stops a previously created and started FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e1d0f-552">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="e1d0f-552">Input Parameters</span></span>

- <span data-ttu-id="e1d0f-553">**ftp_server_ptr**: puntatore al blocco di controllo del server FTP.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-553">**ftp_server_ptr**: Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="e1d0f-554">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="e1d0f-554">Return Values</span></span>

- <span data-ttu-id="e1d0f-555">**NX_SUCCESS**: (0x00) l'arresto del server FTP è riuscito.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-555">**NX_SUCCESS**: (0x00) Successful FTP Server stop.</span></span>
- <span data-ttu-id="e1d0f-556">NX_PTR_ERROR: (0x16) puntatore FTP non valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-556">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>
- <span data-ttu-id="e1d0f-557">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="e1d0f-557">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e1d0f-558">Consentito da</span><span class="sxs-lookup"><span data-stu-id="e1d0f-558">Allowed From</span></span>

<span data-ttu-id="e1d0f-559">Thread</span><span class="sxs-lookup"><span data-stu-id="e1d0f-559">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e1d0f-560">Esempio</span><span class="sxs-lookup"><span data-stu-id="e1d0f-560">Example</span></span>

```c
/* Stop the FTP Server "my_server". */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
