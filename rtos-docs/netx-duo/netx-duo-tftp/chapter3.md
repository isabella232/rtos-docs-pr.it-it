---
title: Capitolo 3-Descrizione dei servizi TFTP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi TFTP NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 56f0d8edb991fff6ae30b6411e375ace58c544f7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821611"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-tftp-services"></a><span data-ttu-id="d96e5-103">Capitolo 3-Descrizione dei servizi TFTP di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d96e5-103">Chapter 3 - Description of Azure RTOS NetX Duo TFTP services</span></span>

<span data-ttu-id="d96e5-104">Questo capitolo contiene una descrizione di tutti i servizi TFTP NetX Duo (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="d96e5-104">This chapter contains a description of all NetX Duo TFTP services (listed below) in alphabetic order.</span></span> <span data-ttu-id="d96e5-105">Se non diversamente specificato, tutti i servizi supportano le comunicazioni IPv6 e IPv4.</span><span class="sxs-lookup"><span data-stu-id="d96e5-105">Unless otherwise specified, all services support IPv6 and IPv4 communications.</span></span>

<span data-ttu-id="d96e5-106">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="d96e5-106">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="d96e5-107">**nxd_tftp_client_file_open**: *aprire il file del client TFTP*</span><span class="sxs-lookup"><span data-stu-id="d96e5-107">**nxd_tftp_client_file_open**: *Open TFTP client file*</span></span>

- <span data-ttu-id="d96e5-108">**nxd_tftp_client_create**: *creare un'istanza del client TFTP*</span><span class="sxs-lookup"><span data-stu-id="d96e5-108">**nxd_tftp_client_create**: *Create a TFTP client instance*</span></span>

- <span data-ttu-id="d96e5-109">**nxd_tftp_client_delete**: *eliminare un'istanza del client TFTP*</span><span class="sxs-lookup"><span data-stu-id="d96e5-109">**nxd_tftp_client_delete**: *Delete a TFTP client instance*</span></span>

- <span data-ttu-id="d96e5-110">**nxd_tftp_client_error_info_get**: *ottenere informazioni sugli errori del client*</span><span class="sxs-lookup"><span data-stu-id="d96e5-110">**nxd_tftp_client_error_info_get**: *Get client error information*</span></span>

- <span data-ttu-id="d96e5-111">**nxd_tftp_client_file_close**: *chiudere il file client*</span><span class="sxs-lookup"><span data-stu-id="d96e5-111">**nxd_tftp_client_file_close**: *Close client file*</span></span>

- <span data-ttu-id="d96e5-112">**nxd_tftp_client_file_open**: *Apri file client*</span><span class="sxs-lookup"><span data-stu-id="d96e5-112">**nxd_tftp_client_file_open**: *Open client file*</span></span>

- <span data-ttu-id="d96e5-113">**nxd_tftp_client_file_read**: *leggere un blocco dal file client*</span><span class="sxs-lookup"><span data-stu-id="d96e5-113">**nxd_tftp_client_file_read**: *Read a block from client file*</span></span>

- <span data-ttu-id="d96e5-114">**nxd_tftp_client_file_write**: *scrittura del blocco nel file client*</span><span class="sxs-lookup"><span data-stu-id="d96e5-114">**nxd_tftp_client_file_write**: *Write block to client file*</span></span>

- <span data-ttu-id="d96e5-115">**nxd_tftp_client_packet_allocate**: *allocare il pacchetto per la scrittura del file client*</span><span class="sxs-lookup"><span data-stu-id="d96e5-115">**nxd_tftp_client_packet_allocate**: *Allocate packet for client file write*</span></span>

- <span data-ttu-id="d96e5-116">**nxd_tftp_client_set_interface**: *impostare l'interfaccia fisica per le richieste TFTP*</span><span class="sxs-lookup"><span data-stu-id="d96e5-116">**nxd_tftp_client_set_interface**: *Set the physical interface for TFTP requests*</span></span>

- <span data-ttu-id="d96e5-117">**nxd_tftp_server_create**: *creare un server TFTP*</span><span class="sxs-lookup"><span data-stu-id="d96e5-117">**nxd_tftp_server_create**: *Create TFTP server*</span></span>

- <span data-ttu-id="d96e5-118">**nxd_tftp_server_delete**: *eliminare il server TFTP*</span><span class="sxs-lookup"><span data-stu-id="d96e5-118">**nxd_tftp_server_delete**: *Delete TFTP server*</span></span>

- <span data-ttu-id="d96e5-119">**nxd_tftp_server_start**: *avvio del server TFTP*</span><span class="sxs-lookup"><span data-stu-id="d96e5-119">**nxd_tftp_server_start**: *Start TFTP server*</span></span>

- <span data-ttu-id="d96e5-120">**nxd_tftp_server_stop**: *arrestare il server TFTP*</span><span class="sxs-lookup"><span data-stu-id="d96e5-120">**nxd_tftp_server_stop**: *Stop TFTP server*</span></span>

> [!NOTE] 
> <span data-ttu-id="d96e5-121">Gli equivalenti IPv4 di tutti i servizi elencati in precedenza sono disponibili nel client e nel server TFTP NetX Duo, ad esempio *nx_tftp_server_create* e *nx_tftp_client_file_open*.</span><span class="sxs-lookup"><span data-stu-id="d96e5-121">The IPv4 equivalents of all the services listed above are available in NetX Duo TFTP Client and Server e.g. *nx_tftp_server_create* and *nx_tftp_client_file_open*.</span></span> <span data-ttu-id="d96e5-122">Nelle pagine seguenti vengono fornite solo le descrizioni dell'API "Duo", ad esempio i servizi che iniziano con *nxd_*.</span><span class="sxs-lookup"><span data-stu-id="d96e5-122">Only the ‘Duo’ API descriptions, e.g. services beginning with *nxd_*, are provided in the following pages.</span></span> <span data-ttu-id="d96e5-123">Quando \* viene specificato un input di NXD_ADDRESS, l'API equivalente IPv4 chiama per l'input ULONG.</span><span class="sxs-lookup"><span data-stu-id="d96e5-123">Where an NXD_ADDRESS \* input is specified, the IPv4 equivalent API calls for ULONG input.</span></span> <span data-ttu-id="d96e5-124">In caso contrario, non esiste alcuna differenza nell'uso dell'API.</span><span class="sxs-lookup"><span data-stu-id="d96e5-124">Otherwise there is no difference in using the API.</span></span>

## <a name="nxd_tftp_client_create"></a><span data-ttu-id="d96e5-125">nxd_tftp_client_create</span><span class="sxs-lookup"><span data-stu-id="d96e5-125">nxd_tftp_client_create</span></span>

<span data-ttu-id="d96e5-126">Creare un'istanza del client TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-126">Create a TFTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-127">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-127">Prototype</span></span>

```C
UINT nxd_tftp_client_create(NX_TFTP_CLIENT *tftp_client_ptr,  
     CHAR *tftp_client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="d96e5-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-128">Description</span></span>

<span data-ttu-id="d96e5-129">Questo servizio crea un'istanza del client TFTP per l'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-129">This service creates a TFTP Client instance for the previously created IP instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d96e5-130">L'applicazione deve assicurarsi che l'indirizzo IP e il pool di pacchetti specificati siano già stati creati.</span><span class="sxs-lookup"><span data-stu-id="d96e5-130">The application must make certain the supplied IP and packet pool are already created.</span></span> <span data-ttu-id="d96e5-131">Inoltre, è necessario abilitare UDP per l'istanza IP prima di chiamare il servizio.</span><span class="sxs-lookup"><span data-stu-id="d96e5-131">In addition, UDP must be enabled for the IP instance prior to calling this service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-132">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-132">Input Parameters</span></span>

- <span data-ttu-id="d96e5-133">**tftp_client_ptr** Puntatore al blocco di controllo client TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-133">**tftp_client_ptr** Pointer to TFTP Client control block.</span></span>

- <span data-ttu-id="d96e5-134">**tftp_client_name** Nome dell'istanza del client TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-134">**tftp_client_name** Name of this TFTP Client instance</span></span>

- <span data-ttu-id="d96e5-135">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-135">**ip_ptr** Pointer to previously created IP instance.</span></span>

- <span data-ttu-id="d96e5-136">**pool_ptr** Puntatore all'istanza del client TFTP del pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d96e5-136">**pool_ptr** Pointer to packet pool TFTP Client instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-137">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-137">Return Values</span></span>

- <span data-ttu-id="d96e5-138">Creazione TFTP riuscita **NX_SUCCESS**(0x00).</span><span class="sxs-lookup"><span data-stu-id="d96e5-138">**NX_SUCCESS**(0x00) Successful TFTP create.</span></span>

- <span data-ttu-id="d96e5-139">La versione di IP **NX_TFTP_INVALID_IP_VERSION** (0X0C) non è valida o non è supportata</span><span class="sxs-lookup"><span data-stu-id="d96e5-139">**NX_TFTP_INVALID_IP_VERSION** (0x0C) Invalid or unsupported IP version</span></span>

- <span data-ttu-id="d96e5-140">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) indirizzo IP del server non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-140">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Invalid Server IP address received</span></span>

- <span data-ttu-id="d96e5-141">ACK server **NX_TFTP_NO_ACK_RECEIVED** (0x09) non ricevuti</span><span class="sxs-lookup"><span data-stu-id="d96e5-141">**NX_TFTP_NO_ACK_RECEIVED** (0x09) Server ACK not received</span></span>

- <span data-ttu-id="d96e5-142">NX_PTR_ERROR (0x16) un IP, un pool o un puntatore TFTP non valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-142">NX_PTR_ERROR (0x16) Invalid IP, pool, or TFTP pointer.</span></span>

- <span data-ttu-id="d96e5-143">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-143">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

- <span data-ttu-id="d96e5-144">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="d96e5-144">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-145">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-145">Allowed From</span></span>

<span data-ttu-id="d96e5-146">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-146">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-147">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-147">Example</span></span>

```C
/* Create a TFTP Client instance. */
status =  nxd_tftp_client_create(&my_tftp_client, “My TFTP Client”, 
                                                    &my_ip, &pool_ptr);

/* If status is NX_SUCCESS a TFTP Client instance was successfully
   created. */
```

## <a name="nxd_tftp_client_delete"></a><span data-ttu-id="d96e5-148">nxd_tftp_client_delete</span><span class="sxs-lookup"><span data-stu-id="d96e5-148">nxd_tftp_client_delete</span></span>

<span data-ttu-id="d96e5-149">Eliminare un'istanza del client TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-149">Delete a TFTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-150">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-150">Prototype</span></span>

```C
UINT nxd_tftp_client_delete(NX_TFTP_CLIENT *tftp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="d96e5-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-151">Description</span></span>

<span data-ttu-id="d96e5-152">Questo servizio Elimina un'istanza del client TFTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-152">This service deletes a previously created TFTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-153">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-153">Input Parameters</span></span>

- <span data-ttu-id="d96e5-154">**tftp_client_ptr** Puntatore a un'istanza del client TFTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-154">**tftp_client_ptr** Pointer to previously created TFTP client instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-155">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-155">Return Values</span></span>

- <span data-ttu-id="d96e5-156">Eliminazione del client TFTP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="d96e5-156">**NX_SUCCESS** (0x00) Successful TFTP Client delete.</span></span>

- <span data-ttu-id="d96e5-157">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-157">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-158">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="d96e5-158">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-159">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-159">Allowed From</span></span>

<span data-ttu-id="d96e5-160">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-160">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-161">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-161">Example</span></span>

```C
/* Delete a TFTP Client instance. */
status =  nxd_tftp_client_delete(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP Client instance was successfully
   deleted. */
```

## <a name="nxd_tftp_client_error_info_get"></a><span data-ttu-id="d96e5-162">nxd_tftp_client_error_info_get</span><span class="sxs-lookup"><span data-stu-id="d96e5-162">nxd_tftp_client_error_info_get</span></span>

<span data-ttu-id="d96e5-163">Ottenere informazioni sull'errore del client</span><span class="sxs-lookup"><span data-stu-id="d96e5-163">Get client error information</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-164">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-164">Prototype</span></span>

```C
UINT nxd_tftp_client_error_info_get(NX_TFTP_CLIENT *tftp_client_ptr,
                        UINT *error_code, CHAR **error_string);
```

### <a name="description"></a><span data-ttu-id="d96e5-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-165">Description</span></span>

<span data-ttu-id="d96e5-166">Questo servizio restituisce l'ultimo codice di errore ricevuto e imposta il puntatore sulla stringa di errore interna del client.</span><span class="sxs-lookup"><span data-stu-id="d96e5-166">This service returns the last error code received and sets the pointer to the client’s internal error string.</span></span> <span data-ttu-id="d96e5-167">In condizioni di errore, l'utente può visualizzare l'ultimo errore inviato dal server.</span><span class="sxs-lookup"><span data-stu-id="d96e5-167">In error conditions, the user can view the last error sent by the server.</span></span> <span data-ttu-id="d96e5-168">Una stringa di errore null indica che non è presente alcun errore.</span><span class="sxs-lookup"><span data-stu-id="d96e5-168">A null error string indicates no error is present.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-169">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-169">Input Parameters</span></span>

- <span data-ttu-id="d96e5-170">**tftp_client_ptr** Puntatore a un'istanza del client TFTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-170">**tftp_client_ptr** Pointer to previously created TFTP Client instance.</span></span>

- <span data-ttu-id="d96e5-171">**error_code** Puntatore all'area di destinazione per il codice di errore</span><span class="sxs-lookup"><span data-stu-id="d96e5-171">**error_code** Pointer to destination area for error code</span></span>

- <span data-ttu-id="d96e5-172">**ERROR_STRING** Puntatore alla destinazione per la stringa di errore</span><span class="sxs-lookup"><span data-stu-id="d96e5-172">**error_string** Pointer to destination for error string</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-173">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-173">Return Values</span></span>

- <span data-ttu-id="d96e5-174">**NX_SUCCESS** (0x00) informazioni sugli errori TFTP riuscite.</span><span class="sxs-lookup"><span data-stu-id="d96e5-174">**NX_SUCCESS** (0x00) Successful TFTP error info get.</span></span>  

- <span data-ttu-id="d96e5-175">NX_PTR_ERROR (0x16) puntatore client TFTP non valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-175">NX_PTR_ERROR (0x16) Invalid TFTP Client pointer.</span></span>

- <span data-ttu-id="d96e5-176">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="d96e5-176">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-177">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-177">Allowed From</span></span>

<span data-ttu-id="d96e5-178">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-178">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-179">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-179">Example</span></span>

```C
/* Get error information for client. */
status =  nxd_tftp_client_error_info_get(&my_tftp_client, &error_code,
                    &error_string_ptr);

/* If status is NX_SUCCESS the error code and error string are available. */
```

## <a name="nxd_tftp_client_file_close"></a><span data-ttu-id="d96e5-180">nxd_tftp_client_file_close</span><span class="sxs-lookup"><span data-stu-id="d96e5-180">nxd_tftp_client_file_close</span></span>

<span data-ttu-id="d96e5-181">Chiudi file client</span><span class="sxs-lookup"><span data-stu-id="d96e5-181">Close client file</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-182">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-182">Prototype</span></span>

```C
UINT nxd_tftp_client_file_close(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="d96e5-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-183">Description</span></span>

<span data-ttu-id="d96e5-184">Questo servizio chiude il file precedentemente aperto da questa istanza del client TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-184">This service closes the previously opened file by this TFTP Client instance.</span></span> <span data-ttu-id="d96e5-185">A un'istanza del client TFTP può essere aperto un solo file alla volta.</span><span class="sxs-lookup"><span data-stu-id="d96e5-185">A TFTP Client instance is allowed to have only one file open at a time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-186">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-186">Input Parameters</span></span>

- <span data-ttu-id="d96e5-187">**tftp_client_ptr** Puntatore a un'istanza del client TFTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-187">**tftp_client_ptr** Pointer to previously created TFTP Client instance.</span></span>

- <span data-ttu-id="d96e5-188">**ip_type** Indica il protocollo IP da usare.</span><span class="sxs-lookup"><span data-stu-id="d96e5-188">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="d96e5-189">Le opzioni valide sono IPv4 (4) o IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="d96e5-189">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-190">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-190">Return Values</span></span>

- <span data-ttu-id="d96e5-191">Chiusura del file TFTP **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="d96e5-191">**NX_SUCCESS** (0x00) Successful TFTP file close.</span></span>

- <span data-ttu-id="d96e5-192">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-192">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-193">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="d96e5-193">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="d96e5-194">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è un input puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-194">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-195">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-195">Allowed From</span></span>

<span data-ttu-id="d96e5-196">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-196">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-197">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-197">Example</span></span>

```C
/* Close the previously opened file associated with “my_client”. */
status =  nxd_tftp_client_file_close(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP file is closed. */
```

## <a name="nx_tftp_client_file_open"></a><span data-ttu-id="d96e5-198">nx_tftp_client_file_open</span><span class="sxs-lookup"><span data-stu-id="d96e5-198">nx_tftp_client_file_open</span></span>

<span data-ttu-id="d96e5-199">Apri file client TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-199">Open TFTP client file</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-200">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-200">Prototype</span></span>

```C
UINT nx_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr, 
            CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
            open_type, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="d96e5-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-201">Description</span></span>

<span data-ttu-id="d96e5-202">Questo servizio tenta di aprire il file specificato nel server TFTP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="d96e5-202">This service attempts to open the specified file on the TFTP Server at the specified IP address.</span></span> <span data-ttu-id="d96e5-203">Il file verrà aperto per la lettura o la scrittura.</span><span class="sxs-lookup"><span data-stu-id="d96e5-203">The file will be opened for either reading or writing.</span></span> 

> [!NOTE] 
> <span data-ttu-id="d96e5-204">Questo è limitato solo ai pacchetti IPv4 ed è destinato a supportare le applicazioni TFTP NetX.</span><span class="sxs-lookup"><span data-stu-id="d96e5-204">This is limited to IPv4 packets only, and is intended for supporting NetX TFTP applications.</span></span> <span data-ttu-id="d96e5-205">Gli sviluppatori sono invitati a trasferire le proprie applicazioni a utilizzando il servizio "Duo" equivalente *nxd_tftp_client_file_open.*</span><span class="sxs-lookup"><span data-stu-id="d96e5-205">Developers are encouraged to port their applications to using equivalent “duo” service *nxd_tftp_client_file_open.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-206">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-206">Input Parameters</span></span>

- <span data-ttu-id="d96e5-207">**tftp_client_ptr** Puntatore al blocco di controllo TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-207">**tftp_client_ptr** Pointer to TFTP control block.</span></span>

- <span data-ttu-id="d96e5-208">**file_name** Nome file ASCII, con terminazione NULL e con le informazioni sul percorso appropriate.</span><span class="sxs-lookup"><span data-stu-id="d96e5-208">**file_name** ASCII file name, NULL-terminated and with appropriate path information.</span></span>

- <span data-ttu-id="d96e5-209">**server_ip_address** Indirizzo TFTP del server.</span><span class="sxs-lookup"><span data-stu-id="d96e5-209">**server_ip_address** Server TFTP address.</span></span>

- <span data-ttu-id="d96e5-210">**open_type** Tipo di richiesta aperta:</span><span class="sxs-lookup"><span data-stu-id="d96e5-210">**open_type** Type of open request, either:</span></span>

  <span data-ttu-id="d96e5-211">**NX_TFTP_OPEN_FOR_READ** (0x01)</span><span class="sxs-lookup"><span data-stu-id="d96e5-211">**NX_TFTP_OPEN_FOR_READ** (0x01)</span></span>

  <span data-ttu-id="d96e5-212">**NX_TFTP_OPEN_FOR_WRITE** (0x02)</span><span class="sxs-lookup"><span data-stu-id="d96e5-212">**NX_TFTP_OPEN_FOR_WRITE** (0x02)</span></span>

- <span data-ttu-id="d96e5-213">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'apertura del file del client TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-213">**wait_option** Defines how long the service will wait for the TFTP Client file open.</span></span> <span data-ttu-id="d96e5-214">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="d96e5-214">The wait options are defined as follows:</span></span>

  <span data-ttu-id="d96e5-215">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="d96e5-215">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="d96e5-216">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="d96e5-216">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span> 
  
  <span data-ttu-id="d96e5-217">Se si seleziona TX_WAIT_FOREVER, il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server TFTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="d96e5-217">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a TFTP Server responds to the request.</span></span> 
  
  <span data-ttu-id="d96e5-218">La selezione di un valore numerico (1-0xFFFFFFFE) consente di specificare il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-218">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the TFTP server response.</span></span>

- <span data-ttu-id="d96e5-219">**ip_type** Indica il protocollo IP da usare.</span><span class="sxs-lookup"><span data-stu-id="d96e5-219">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="d96e5-220">Le opzioni valide sono IPv4 (4) o IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="d96e5-220">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-221">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-221">Return Values</span></span>

- <span data-ttu-id="d96e5-222">Apertura del file client **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="d96e5-222">**NX_SUCCESS** (0x00) Successful Client file open</span></span>

- <span data-ttu-id="d96e5-223">Il client **NX_TFTP_NOT_CLOSED** (0xC3) ha già aperto il file</span><span class="sxs-lookup"><span data-stu-id="d96e5-223">**NX_TFTP_NOT_CLOSED** (0xC3) Client already has file open</span></span>

- <span data-ttu-id="d96e5-224">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-224">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="d96e5-225">**NX_TFTP_NO_ACK_RECEIVED** (0x09) nessun ACK ricevuto dal server</span><span class="sxs-lookup"><span data-stu-id="d96e5-225">**NX_TFTP_NO_ACK_RECEIVED** (0x09) No ACK received from server</span></span>

- <span data-ttu-id="d96e5-226">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) IP del server non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-226">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Invalid Server IP received</span></span>

- <span data-ttu-id="d96e5-227">Codice di errore ricevuto **NX_TFTP_CODE_ERROR** (0x05)</span><span class="sxs-lookup"><span data-stu-id="d96e5-227">**NX_TFTP_CODE_ERROR** (0x05) Received error code</span></span>

- <span data-ttu-id="d96e5-228">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-228">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-229">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="d96e5-229">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="d96e5-230">NX_IP_ADDRESS_ERROR (0x21) indirizzo IP del server non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-230">NX_IP_ADDRESS_ERROR (0x21) Invalid Server IP address</span></span>

- <span data-ttu-id="d96e5-231">Tipo aperto NX_OPTION_ERROR (0x0A) non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-231">NX_OPTION_ERROR (0x0A) Invalid open type</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-232">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-232">Allowed From</span></span>

<span data-ttu-id="d96e5-233">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-233">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-234">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-234">Example</span></span>

```C
/* Define the TFTP server address. */
NXD_ADDRESS server_ip_address;

server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server _ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server _ip_address.nxd_ip_address.v6[1] = 0xf101;
server _ip_address.nxd_ip_address.v6[2] = 0;
server _ip_address.nxd_ip_address.v6[3] = 0x101;

/* Open file “test.txt” for reading on the TFTP Server. */
status =  nxd_tftp_client_file_open(&my_tftp_client, “test.txt”,
        & server_ip_address, NX_TFTP_OPEN_FOR_READ, 200);

/* If status is NX_SUCCESS the “test.txt” file is now open for reading. */
```

## <a name="nxd_tftp_client_file_open"></a><span data-ttu-id="d96e5-235">nxd_tftp_client_file_open</span><span class="sxs-lookup"><span data-stu-id="d96e5-235">nxd_tftp_client_file_open</span></span>

<span data-ttu-id="d96e5-236">Apri file client TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-236">Open TFTP client file</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-237">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-237">Prototype</span></span>

```C
UINT nxd_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr,
        CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
        open_type, ULONG wait_option, UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="d96e5-238">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-238">Description</span></span>

<span data-ttu-id="d96e5-239">Questo servizio tenta di aprire il file specificato nel server TFTP all'indirizzo IPv6 specificato.</span><span class="sxs-lookup"><span data-stu-id="d96e5-239">This service attempts to open the specified file on the TFTP Server at the specified IPv6 address.</span></span> <span data-ttu-id="d96e5-240">Il file verrà aperto per la lettura o la scrittura.</span><span class="sxs-lookup"><span data-stu-id="d96e5-240">The file will be opened for either reading or writing.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-241">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-241">Input Parameters</span></span>

- <span data-ttu-id="d96e5-242">**tftp_client_ptr** Puntatore al blocco di controllo TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-242">**tftp_client_ptr** Pointer to TFTP control block.</span></span>

- <span data-ttu-id="d96e5-243">**file_name** Nome file ASCII, con terminazione NULL e con le informazioni sul percorso appropriate.</span><span class="sxs-lookup"><span data-stu-id="d96e5-243">**file_name** ASCII file name, NULL-terminated and with appropriate path information.</span></span>

- <span data-ttu-id="d96e5-244">**server_ip_address** Indirizzo TFTP del server.</span><span class="sxs-lookup"><span data-stu-id="d96e5-244">**server_ip_address** Server TFTP address.</span></span>

- <span data-ttu-id="d96e5-245">**open_type** Tipo di richiesta aperta:</span><span class="sxs-lookup"><span data-stu-id="d96e5-245">**open_type** Type of open request, either:</span></span>

  <span data-ttu-id="d96e5-246">**NX_TFTP_OPEN_FOR_READ** (0x01)</span><span class="sxs-lookup"><span data-stu-id="d96e5-246">**NX_TFTP_OPEN_FOR_READ** (0x01)</span></span>

  <span data-ttu-id="d96e5-247">**NX_TFTP_OPEN_FOR_WRITE** (0x02)</span><span class="sxs-lookup"><span data-stu-id="d96e5-247">**NX_TFTP_OPEN_FOR_WRITE** (0x02)</span></span>

- <span data-ttu-id="d96e5-248">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa dell'apertura del file del client TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-248">**wait_option** Defines how long the service will wait for the TFTP Client file open.</span></span> <span data-ttu-id="d96e5-249">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="d96e5-249">The wait options are defined as follows:</span></span>

  <span data-ttu-id="d96e5-250">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="d96e5-250">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="d96e5-251">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="d96e5-251">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

  <span data-ttu-id="d96e5-252">Se si seleziona TX_WAIT_FOREVER, il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server TFTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="d96e5-252">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a TFTP Server responds to the request.</span></span>

  <span data-ttu-id="d96e5-253">La selezione di un valore numerico (1-0xFFFFFFFE) consente di specificare il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risposta del server TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-253">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the TFTP server response.</span></span>

- <span data-ttu-id="d96e5-254">**ip_type** Indica il protocollo IP da usare.</span><span class="sxs-lookup"><span data-stu-id="d96e5-254">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="d96e5-255">Le opzioni valide sono IPv4 (4) o IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="d96e5-255">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-256">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-256">Return Values</span></span>

- <span data-ttu-id="d96e5-257">Apertura del file client **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="d96e5-257">**NX_SUCCESS** (0x00) Successful Client file open</span></span>

- <span data-ttu-id="d96e5-258">Il client **NX_TFTP_NOT_CLOSED** (0xC3) ha già aperto il file</span><span class="sxs-lookup"><span data-stu-id="d96e5-258">**NX_TFTP_NOT_CLOSED** (0xC3) Client already has file open</span></span>

- <span data-ttu-id="d96e5-259">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-259">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="d96e5-260">**NX_TFTP_NO_ACK_RECEIVED** (0x09) nessun ACK ricevuto dal server</span><span class="sxs-lookup"><span data-stu-id="d96e5-260">**NX_TFTP_NO_ACK_RECEIVED** (0x09) No ACK received from server</span></span>

- <span data-ttu-id="d96e5-261">**NX_TFTP_INVALID_IP_VERSION** (0x0C) versione IP non valida</span><span class="sxs-lookup"><span data-stu-id="d96e5-261">**NX_TFTP_INVALID_IP_VERSION** (0x0C) Invalid IP version</span></span>

- <span data-ttu-id="d96e5-262">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) IP del server non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-262">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Invalid Server IP received</span></span>

- <span data-ttu-id="d96e5-263">Codice di errore ricevuto **NX_TFTP_CODE_ERROR** (0x05)</span><span class="sxs-lookup"><span data-stu-id="d96e5-263">**NX_TFTP_CODE_ERROR** (0x05) Received error code</span></span>

- <span data-ttu-id="d96e5-264">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-264">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-265">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="d96e5-265">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="d96e5-266">NX_IP_ADDRESS_ERROR (0x21) indirizzo IP del server non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-266">NX_IP_ADDRESS_ERROR (0x21) Invalid Server IP address</span></span>

- <span data-ttu-id="d96e5-267">Tipo aperto NX_OPTION_ERROR (0x0A) non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-267">NX_OPTION_ERROR (0x0A) Invalid open type</span></span>

- <span data-ttu-id="d96e5-268">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-268">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-269">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-269">Allowed From</span></span>

<span data-ttu-id="d96e5-270">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-270">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-271">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-271">Example</span></span>

```C
/* Define the TFTP server address. */
NXD_ADDRESS server_ip_address;

server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server _ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server _ip_address.nxd_ip_address.v6[1] = 0xf101;
server _ip_address.nxd_ip_address.v6[2] = 0;
server _ip_address.nxd_ip_address.v6[3] = 0x101;

/* Open file “test.txt” for reading on the TFTP Server. */
status =  nxd_tftp_client_file_open(&my_tftp_client, “test.txt”,
                & server_ip_address, NX_TFTP_OPEN_FOR_READ, 200);

/* If status is NX_SUCCESS the “test.txt” file is now open for reading. */
```

## <a name="nxd_tftp_client_file_read"></a><span data-ttu-id="d96e5-272">nxd_tftp_client_file_read</span><span class="sxs-lookup"><span data-stu-id="d96e5-272">nxd_tftp_client_file_read</span></span>

<span data-ttu-id="d96e5-273">Leggi un blocco dal file client</span><span class="sxs-lookup"><span data-stu-id="d96e5-273">Read a block from client file</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-274">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-274">Prototype</span></span>

```C
UINT nxd_tftp_client_file_read(NX_TFTP_CLIENT *tftp_client_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="d96e5-275">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-275">Description</span></span>

<span data-ttu-id="d96e5-276">Questo servizio legge un blocco di 512 byte dal file del client TFTP aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-276">This service reads a 512-byte block from the previously opened TFTP Client file.</span></span> <span data-ttu-id="d96e5-277">Un blocco contenente meno di 512 byte segnala la fine del file.</span><span class="sxs-lookup"><span data-stu-id="d96e5-277">A block containing fewer than 512 bytes signals the end of the file.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-278">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-278">Input Parameters</span></span>

- <span data-ttu-id="d96e5-279">**tftp_client_ptr** Puntatore al blocco di controllo client TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-279">**tftp_client_ptr** Pointer to TFTP Client control block.</span></span>

- <span data-ttu-id="d96e5-280">**packet_ptr** Destinazione per il pacchetto contenente il blocco letto dal file.</span><span class="sxs-lookup"><span data-stu-id="d96e5-280">**packet_ptr** Destination for packet containing the block read from the file.</span></span>

- <span data-ttu-id="d96e5-281">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del completamento dell'operazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="d96e5-281">**wait_option** Defines how long the service will wait for the read to complete.</span></span> <span data-ttu-id="d96e5-282">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="d96e5-282">The wait options are defined as follows:</span></span>

  <span data-ttu-id="d96e5-283">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="d96e5-283">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="d96e5-284">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="d96e5-284">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

  <span data-ttu-id="d96e5-285">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server TFTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="d96e5-285">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the TFTP Server responds to the request.</span></span>

  <span data-ttu-id="d96e5-286">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi mentre è in attesa che il server TFTP invii un blocco del file.</span><span class="sxs-lookup"><span data-stu-id="d96e5-286">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the TFTP server to send a block of the file.</span></span>

- <span data-ttu-id="d96e5-287">**ip_type** Indica il protocollo IP da usare.</span><span class="sxs-lookup"><span data-stu-id="d96e5-287">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="d96e5-288">Le opzioni valide sono IPv4 (4) o IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="d96e5-288">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-289">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-289">Return Values</span></span>

- <span data-ttu-id="d96e5-290">Lettura blocco client riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="d96e5-290">**NX_SUCCESS** (0x00) Successful Client block read</span></span>

- <span data-ttu-id="d96e5-291">Il file client specificato **NX_TFTP_NOT_OPEN** (0xC3) non è aperto per la lettura</span><span class="sxs-lookup"><span data-stu-id="d96e5-291">**NX_TFTP_NOT_OPEN** (0xC3) Specified Client file is not open for reading</span></span>

- <span data-ttu-id="d96e5-292">**NX_NO_PACKET** (0x01) non è stato ricevuto alcun pacchetto dal server.</span><span class="sxs-lookup"><span data-stu-id="d96e5-292">**NX_NO_PACKET** (0x01) No Packet received from Server.</span></span>

- <span data-ttu-id="d96e5-293">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-293">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="d96e5-294">**NX_TFTP_NO_ACK_RECEIVED** (0x09) nessun ACK ricevuto dal server</span><span class="sxs-lookup"><span data-stu-id="d96e5-294">**NX_TFTP_NO_ACK_RECEIVED** (0x09) No ACK received from Server</span></span>

- <span data-ttu-id="d96e5-295">È stata rilevata la fine del file **NX_TFTP_END_OF_FILE** (0XC5) (non un errore).</span><span class="sxs-lookup"><span data-stu-id="d96e5-295">**NX_TFTP_END_OF_FILE** (0xC5) End of file detected (not an error).</span></span>

- <span data-ttu-id="d96e5-296">**NX_TFTP_INVALID_IP_VERSION** (0x0C) versione IP non valida</span><span class="sxs-lookup"><span data-stu-id="d96e5-296">**NX_TFTP_INVALID_IP_VERSION** (0x0C) Invalid IP version</span></span>

- <span data-ttu-id="d96e5-297">Codice di errore ricevuto **NX_TFTP_CODE_ERROR** (0x05)</span><span class="sxs-lookup"><span data-stu-id="d96e5-297">**NX_TFTP_CODE_ERROR** (0x05) Received error code</span></span>

- <span data-ttu-id="d96e5-298">**NX_TFTP_FAILED** (0xC2) codice TFTP sconosciuto ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-298">**NX_TFTP_FAILED** (0xC2) Unknown TFTP code received</span></span>

- <span data-ttu-id="d96e5-299">**NX_TFTP_INVALID_BLOCK_NUMBER** (0x0A) numero di blocco non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-299">**NX_TFTP_INVALID_BLOCK_NUMBER** (0x0A) Invalid block number received</span></span>

- <span data-ttu-id="d96e5-300">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-300">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-301">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="d96e5-301">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="d96e5-302">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-302">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-303">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-303">Allowed From</span></span>

<span data-ttu-id="d96e5-304">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-304">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-305">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-305">Example</span></span>

```C
/* Read a block from a previously opened file of “my_client”. */
status =  nxd_tftp_client_file_read(&my_tftp_client, &return_packet_ptr, 200);

/* If status is NX_SUCCESS a block of the TFTP file is in the payload of
   “return_packet_ptr”. */
```

## <a name="nxd_tftp_client_file_write"></a><span data-ttu-id="d96e5-306">nxd_tftp_client_file_write</span><span class="sxs-lookup"><span data-stu-id="d96e5-306">nxd_tftp_client_file_write</span></span>

<span data-ttu-id="d96e5-307">Scrivere un blocco nel file client</span><span class="sxs-lookup"><span data-stu-id="d96e5-307">Write a block to Client file</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-308">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-308">Prototype</span></span>

```C
UINT nxd_tftp_client_file_write(NX_TFTP_CLIENT *tftp_client_ptr,
            NX_PACKET *packet_ptr, ULONG wait_option, UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="d96e5-309">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-309">Description</span></span>

<span data-ttu-id="d96e5-310">Questo servizio scrive un blocco di 512 byte nel file del client TFTP aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-310">This service writes a 512-byte block to the previously opened TFTP Client file.</span></span> <span data-ttu-id="d96e5-311">Se si specifica un blocco contenente meno di 512 byte, viene segnalata la fine del file.</span><span class="sxs-lookup"><span data-stu-id="d96e5-311">Specifying a block containing fewer than 512 bytes signals the end of the file.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-312">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-312">Input Parameters</span></span>

- <span data-ttu-id="d96e5-313">**tftp_client_ptr** Puntatore al blocco di controllo client TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-313">**tftp_client_ptr** Pointer to TFTP Client control block.</span></span>

- <span data-ttu-id="d96e5-314">**packet_ptr** Pacchetto contenente il blocco da scrivere nel file.</span><span class="sxs-lookup"><span data-stu-id="d96e5-314">**packet_ptr** Packet containing the block to write to the file.</span></span>

- <span data-ttu-id="d96e5-315">**WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa del completamento della scrittura.</span><span class="sxs-lookup"><span data-stu-id="d96e5-315">**wait_option** Defines how long the service will wait for the write to complete.</span></span> <span data-ttu-id="d96e5-316">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="d96e5-316">The wait options are defined as follows:</span></span>

  <span data-ttu-id="d96e5-317">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="d96e5-317">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="d96e5-318">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="d96e5-318">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

  <span data-ttu-id="d96e5-319">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando il server TFTP non risponde alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="d96e5-319">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the TFTP Server responds to the request.</span></span>
 
  <span data-ttu-id="d96e5-320">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi mentre è in attesa che il server TFTP invii un ACK per la richiesta di scrittura.</span><span class="sxs-lookup"><span data-stu-id="d96e5-320">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the TFTP server to send an ACK for the write request.</span></span>

- <span data-ttu-id="d96e5-321">**ip_type** Indica il protocollo IP da usare.</span><span class="sxs-lookup"><span data-stu-id="d96e5-321">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="d96e5-322">Le opzioni valide sono IPv4 (4) o IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="d96e5-322">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-323">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-323">Return Values</span></span>

- <span data-ttu-id="d96e5-324">Scrittura blocco client riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="d96e5-324">**NX_SUCCESS** (0x00) Successful Client block write</span></span>

- <span data-ttu-id="d96e5-325">Il file client specificato **NX_TFTP_NOT_OPEN** (0xC3) non è aperto per la scrittura</span><span class="sxs-lookup"><span data-stu-id="d96e5-325">**NX_TFTP_NOT_OPEN** (0xC3) Specified Client file is not open for writing</span></span>

- <span data-ttu-id="d96e5-326">Timeout **NX_TFTP_TIMEOUT** (0xC1) in attesa di ACK server</span><span class="sxs-lookup"><span data-stu-id="d96e5-326">**NX_TFTP_TIMEOUT** (0xC1) Timeout waiting for Server ACK</span></span>

- <span data-ttu-id="d96e5-327">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-327">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="d96e5-328">**NX_TFTP_NO_ACK_RECEIVED** (0x09) nessun ACK ricevuto dal server</span><span class="sxs-lookup"><span data-stu-id="d96e5-328">**NX_TFTP_NO_ACK_RECEIVED** (0x09) No ACK received from server</span></span>

- <span data-ttu-id="d96e5-329">**NX_TFTP_INVALID_IP_VERSION** (0x0C) versione IP non valida</span><span class="sxs-lookup"><span data-stu-id="d96e5-329">**NX_TFTP_INVALID_IP_VERSION** (0x0C) Invalid IP version</span></span>

- <span data-ttu-id="d96e5-330">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) indirizzo server non valido ricevuto</span><span class="sxs-lookup"><span data-stu-id="d96e5-330">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="d96e5-331">Codice di errore ricevuto **NX_TFTP_CODE_ERROR** (0x05)</span><span class="sxs-lookup"><span data-stu-id="d96e5-331">**NX_TFTP_CODE_ERROR** (0x05) Received error code</span></span>

- <span data-ttu-id="d96e5-332">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-332">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-333">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="d96e5-333">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="d96e5-334">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-334">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-335">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-335">Allowed From</span></span>

<span data-ttu-id="d96e5-336">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-336">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-337">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-337">Example</span></span>

```C
/* Write a block to the previously opened file of “my_client”. */
status =  nxd_tftp_client_file_write(&my_tftp_client, packet_ptr, 200);

/* If status is NX_SUCCESS the block in the payload of “packet_ptr” was 
   written to the TFTP file opened by “my_client”. */
```

## <a name="nxd_tftp_client_packet_allocate"></a><span data-ttu-id="d96e5-338">nxd_tftp_client_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="d96e5-338">nxd_tftp_client_packet_allocate</span></span>

<span data-ttu-id="d96e5-339">Alloca pacchetto per la scrittura di file client</span><span class="sxs-lookup"><span data-stu-id="d96e5-339">Allocate packet for Client file write</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-340">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-340">Prototype</span></span>

```C
UINT nxd_tftp_client_packet_allocate(NX_PACKET_POOL *pool_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="d96e5-341">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-341">Description</span></span>

<span data-ttu-id="d96e5-342">Questo servizio alloca un pacchetto UDP dal pool di pacchetti specificato e crea spazio per l'intestazione TFTP a 4 byte prima che il pacchetto venga restituito al chiamante.</span><span class="sxs-lookup"><span data-stu-id="d96e5-342">This service allocates a UDP packet from the specified packet pool and makes room for the 4-byte TFTP header before the packet is returned to the caller.</span></span> <span data-ttu-id="d96e5-343">Il chiamante può quindi compilare un buffer per la scrittura in un file client.</span><span class="sxs-lookup"><span data-stu-id="d96e5-343">The caller can then build a buffer for writing to a client file.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-344">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-344">Input Parameters</span></span>

- <span data-ttu-id="d96e5-345">**pool_ptr** Puntatore al pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d96e5-345">**pool_ptr** Pointer to packet pool.</span></span>

- <span data-ttu-id="d96e5-346">**packet_ptr** Destinazione per il puntatore al pacchetto allocato.</span><span class="sxs-lookup"><span data-stu-id="d96e5-346">**packet_ptr** Destination for pointer to allocated packet.</span></span>

- <span data-ttu-id="d96e5-347">**WAIT_OPTION** Definisce per quanto tempo il servizio attenderà il completamento dell'allocazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d96e5-347">**wait_option** Defines how long the service will wait for the packet allocate to complete.</span></span> <span data-ttu-id="d96e5-348">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="d96e5-348">The wait options are defined as follows:</span></span>

  <span data-ttu-id="d96e5-349">**valore di timeout** (0x00000001 tramite 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="d96e5-349">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="d96e5-350">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="d96e5-350">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

  <span data-ttu-id="d96e5-351">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino al completamento dell'allocazione.</span><span class="sxs-lookup"><span data-stu-id="d96e5-351">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the allocation completes.</span></span>

  <span data-ttu-id="d96e5-352">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi in attesa dell'allocazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d96e5-352">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the packet allocation.</span></span>

- <span data-ttu-id="d96e5-353">**ip_type** Indica il protocollo IP da usare.</span><span class="sxs-lookup"><span data-stu-id="d96e5-353">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="d96e5-354">Le opzioni valide sono IPv4 (4) o IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="d96e5-354">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-355">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-355">Return Values</span></span>

- <span data-ttu-id="d96e5-356">Allocazione pacchetto riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="d96e5-356">**NX_SUCCESS** (0x00) Successful packet allocate</span></span>

- <span data-ttu-id="d96e5-357">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-357">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-358">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="d96e5-358">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="d96e5-359">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-359">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-360">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-360">Allowed From</span></span>

<span data-ttu-id="d96e5-361">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-361">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-362">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-362">Example</span></span>

```C
/* Allocate a packet for TFTP file write. */
status =  nxd_tftp_client_packet_allocate(&my_pool, &packet_ptr, 200);

/* If status is NX_SUCCESS “packet_ptr” contains the new packet. */
```

## <a name="nxd_tftp_client_set_interface"></a><span data-ttu-id="d96e5-363">nxd_tftp_client_set_interface</span><span class="sxs-lookup"><span data-stu-id="d96e5-363">nxd_tftp_client_set_interface</span></span>

<span data-ttu-id="d96e5-364">Imposta l'interfaccia fisica per le richieste TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-364">Set physical interface for TFTP requests</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-365">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-365">Prototype</span></span>

```C
UINT nxd_tftp_client_set_interface(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT if_index);
```

### <a name="description"></a><span data-ttu-id="d96e5-366">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-366">Description</span></span>

<span data-ttu-id="d96e5-367">Questo servizio usa l'indice dell'interfaccia di input per impostare l'interfaccia fisica per il client TFTP per l'invio e la ricezione di pacchetti TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-367">This service uses the input interface index to set the physical interface for the TFTP Client to send and receive TFTP packets.</span></span> <span data-ttu-id="d96e5-368">Il valore predefinito è zero, per l'interfaccia primaria.</span><span class="sxs-lookup"><span data-stu-id="d96e5-368">The default value is zero, for the primary interface.</span></span>

> [!NOTE]
> <span data-ttu-id="d96e5-369">NetX Duo deve supportare l'indirizzamento multihome (v 5.6 o versione successiva) per usare questo servizio.</span><span class="sxs-lookup"><span data-stu-id="d96e5-369">NetX Duo must support multihome addressing (v5.6 or later) to use this service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-370">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-370">Input Parameters</span></span>

- <span data-ttu-id="d96e5-371">**tftp_client_ptr** Puntatore all'istanza del client TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-371">**tftp_client_ptr** Pointer to TFTP Client instance</span></span>

- <span data-ttu-id="d96e5-372">**if_index** Indice dell'interfaccia fisica da usare</span><span class="sxs-lookup"><span data-stu-id="d96e5-372">**if_index** Index of physical interface to use</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-373">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-373">Return Values</span></span>

- <span data-ttu-id="d96e5-374">L'input dell'interfaccia (0x0B) dell'interfaccia non è valido per il **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="d96e5-374">**NX_SUCCESS** (0x00) Successfully set interface (0x0B) Invalid interface input</span></span>

- <span data-ttu-id="d96e5-375">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-375">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-376">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="d96e5-376">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="d96e5-377">Input dell'interfaccia NX_TFTP_INVALID_INTERFACE (0x0B) non valido</span><span class="sxs-lookup"><span data-stu-id="d96e5-377">NX_TFTP_INVALID_INTERFACE (0x0B) Invalid interface input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-378">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-378">Allowed From</span></span>

<span data-ttu-id="d96e5-379">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-379">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-380">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-380">Example</span></span>

```C
/* Specify the primary interface for TFTP requests. */
status =  nxd_tftp_client_set_interface(&client, 0);

/* If status is NX_SUCCESS the primary interface will be use for TFTP communications. */
```

## <a name="nxd_tftp_server_create"></a><span data-ttu-id="d96e5-381">nxd_tftp_server_create</span><span class="sxs-lookup"><span data-stu-id="d96e5-381">nxd_tftp_server_create</span></span>

<span data-ttu-id="d96e5-382">Crea server TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-382">Create TFTP server</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-383">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-383">Prototype</span></span>

```C
UINT nxd_tftp_server_create(NX_TFTP_SERVER *tftp_server_ptr,
            CHAR *tftp_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr, 
            VOID *stack_ptr, ULONG stack_size,
            NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="d96e5-384">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-384">Description</span></span>

<span data-ttu-id="d96e5-385">Questo servizio crea un server TFTP che risponde alle richieste del client TFTP sulla porta 69.</span><span class="sxs-lookup"><span data-stu-id="d96e5-385">This service creates a TFTP Server that responds to TFTP Client requests on port 69.</span></span> <span data-ttu-id="d96e5-386">Il server deve essere avviato da una chiamata successiva a *nxd_tftp_server_start*.</span><span class="sxs-lookup"><span data-stu-id="d96e5-386">The Server must be started by a subsequent call to *nxd_tftp_server_start*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d96e5-387">L'applicazione deve verificare che siano già state create le istanze IP, il pool di pacchetti e l'istanza del supporto FileX specificati.</span><span class="sxs-lookup"><span data-stu-id="d96e5-387">The application must make certain the supplied IP instance, packet pool, and FileX media instance are already created.</span></span> <span data-ttu-id="d96e5-388">Inoltre, è necessario abilitare UDP per l'istanza IP prima di chiamare il servizio.</span><span class="sxs-lookup"><span data-stu-id="d96e5-388">In addition, UDP must be enabled for the IP instance prior to calling this service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-389">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-389">Input Parameters</span></span>

- <span data-ttu-id="d96e5-390">**tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-390">**tftp_server_ptr** Pointer to TFTP Server control block.</span></span>

- <span data-ttu-id="d96e5-391">**tftp_server_name** Nome dell'istanza del server TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-391">**tftp_server_name** Name of this TFTP Server instance</span></span>

- <span data-ttu-id="d96e5-392">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-392">**ip_ptr** Pointer to previously created IP instance.</span></span>

- <span data-ttu-id="d96e5-393">**media_ptr** Puntatore all'istanza del supporto FileX.</span><span class="sxs-lookup"><span data-stu-id="d96e5-393">**media_ptr** Pointer to FileX media instance.</span></span>

- <span data-ttu-id="d96e5-394">**stack_ptr** Puntatore all'area dello stack del server TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-394">**stack_ptr** Pointer to TFTP Server stack area.</span></span>

- <span data-ttu-id="d96e5-395">**stack_size** Numero di byte nello stack del server TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-395">**stack_size** Number of bytes in the TFTP Server stack.</span></span>

- <span data-ttu-id="d96e5-396">**pool_ptr** Puntatore al pool di pacchetti TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-396">**pool_ptr** Pointer to TFTP packet pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="d96e5-397">Il pool fornito deve avere payload di pacchetti di almeno 580 byte. <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d96e5-397">The supplied pool must have packet payloads at least 580 bytes in size.<sup>1</sup></span></span>

<span data-ttu-id="d96e5-398"><sup>1</sup> la parte relativa ai dati di un pacchetto è esattamente 512 byte, ma le dimensioni del payload del pacchetto devono essere di almeno 572 byte.</span><span class="sxs-lookup"><span data-stu-id="d96e5-398"><sup>1</sup> The data portion of a packet is exactly 512 bytes, but the packet payload size must be at least 572 bytes.</span></span> <span data-ttu-id="d96e5-399">I byte rimanenti vengono usati per le intestazioni UDP, IPv6 e Ethernet e i potenziali byte finali richiesti dal driver per l'allineamento.</span><span class="sxs-lookup"><span data-stu-id="d96e5-399">The remaining bytes are used for the UDP, IPv6, and Ethernet headers and potential trailing bytes required by the driver for alignment.</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-400">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-400">Return Values</span></span>

- <span data-ttu-id="d96e5-401">Creazione di un server **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="d96e5-401">**NX_SUCCESS** (0x00) Successful Server create</span></span>

- <span data-ttu-id="d96e5-402">Il pool di pacchetti **NX_TFTP_POOL_ERROR** (0xc6) ha una dimensione del pacchetto inferiore a 560 byte</span><span class="sxs-lookup"><span data-stu-id="d96e5-402">**NX_TFTP_POOL_ERROR** (0xC6) Packet pool has packet size of less than 560 bytes</span></span>

- <span data-ttu-id="d96e5-403">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-403">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-404">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-404">Allowed From</span></span>

<span data-ttu-id="d96e5-405">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-405">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-406">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-406">Example</span></span>

```C
/* Create a TFTP Server called “my_server”. */
status =  nxd_tftp_server_create(&my_server, “My TFTP Server”, &server_ip, 
                &ram_disk, stack_ptr, 2048, pool_ptr);

/* If status is NX_SUCCESS the TFTP Server is created. */
```

## <a name="nxd_tftp_server_delete"></a><span data-ttu-id="d96e5-407">nxd_tftp_server_delete</span><span class="sxs-lookup"><span data-stu-id="d96e5-407">nxd_tftp_server_delete</span></span>

<span data-ttu-id="d96e5-408">Elimina server TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-408">Delete TFTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-409">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-409">Prototype</span></span>

```C
UINT nxd_tftp_server_delete(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="d96e5-410">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-410">Description</span></span>

<span data-ttu-id="d96e5-411">Questo servizio Elimina un server TFTP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-411">This service deletes a previously created TFTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-412">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-412">Input Parameters</span></span>

- <span data-ttu-id="d96e5-413">**tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-413">**tftp_server_ptr** Pointer to TFTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-414">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-414">Return Values</span></span>

- <span data-ttu-id="d96e5-415">Eliminazione server riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="d96e5-415">**NX_SUCCESS** (0x00) Successful Server delete</span></span>

- <span data-ttu-id="d96e5-416">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-416">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-417">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="d96e5-417">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-418">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-418">Allowed From</span></span>

<span data-ttu-id="d96e5-419">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-419">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-420">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-420">Example</span></span>

```C
/* Delete the TFTP Server called “my_server”. */
status =  nxd_tftp_server_delete(&my_server);

/* If status is NX_SUCCESS the TFTP Server is deleted. */
```

## <a name="nxd_tftp_server_start"></a><span data-ttu-id="d96e5-421">nxd_tftp_server_start</span><span class="sxs-lookup"><span data-stu-id="d96e5-421">nxd_tftp_server_start</span></span>

<span data-ttu-id="d96e5-422">Avvia server TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-422">Start TFTP server</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-423">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-423">Prototype</span></span>

```C
UINT nxd_tftp_server_start(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="d96e5-424">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-424">Description</span></span>

<span data-ttu-id="d96e5-425">Questo servizio avvia il server TFTP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-425">This service starts the previously created TFTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-426">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-426">Input Parameters</span></span>

- <span data-ttu-id="d96e5-427">**tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-427">**tftp_server_ptr** Pointer to TFTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-428">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-428">Return Values</span></span>

- <span data-ttu-id="d96e5-429">Avvio del server **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="d96e5-429">**NX_SUCCESS** (0x00) Successful Server start</span></span>

- <span data-ttu-id="d96e5-430">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-430">NX_PTR_ERROR (0x16) Invalid pointer input .</span></span>
 
### <a name="allowed-from"></a><span data-ttu-id="d96e5-431">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-431">Allowed From</span></span>

<span data-ttu-id="d96e5-432">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-432">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-433">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-433">Example</span></span>

```C
/* Start the TFTP Server called “my_server”. */
status =  nxd_tftp_server_start(&my_server);

/* If status is NX_SUCCESS the TFTP Server is started. */
```

## <a name="nxd_tftp_server_stop"></a><span data-ttu-id="d96e5-434">nxd_tftp_server_stop</span><span class="sxs-lookup"><span data-stu-id="d96e5-434">nxd_tftp_server_stop</span></span>

<span data-ttu-id="d96e5-435">Arresta server TFTP</span><span class="sxs-lookup"><span data-stu-id="d96e5-435">Stop TFTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="d96e5-436">Prototipo</span><span class="sxs-lookup"><span data-stu-id="d96e5-436">Prototype</span></span>

```C
UINT nxd_tftp_server_stop(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="d96e5-437">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d96e5-437">Description</span></span>

<span data-ttu-id="d96e5-438">Questo servizio arresta il server TFTP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d96e5-438">This service stops the previously created TFTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d96e5-439">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="d96e5-439">Input Parameters</span></span>

- <span data-ttu-id="d96e5-440">**tftp_server_ptr** Puntatore al blocco di controllo del server TFTP.</span><span class="sxs-lookup"><span data-stu-id="d96e5-440">**tftp_server_ptr** Pointer to TFTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="d96e5-441">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="d96e5-441">Return Values</span></span>

- <span data-ttu-id="d96e5-442">Arresto server riuscito **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="d96e5-442">**NX_SUCCESS** (0x00) Successful Server stop</span></span>

- <span data-ttu-id="d96e5-443">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="d96e5-443">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="d96e5-444">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="d96e5-444">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="d96e5-445">Consentito da</span><span class="sxs-lookup"><span data-stu-id="d96e5-445">Allowed From</span></span>

<span data-ttu-id="d96e5-446">Thread</span><span class="sxs-lookup"><span data-stu-id="d96e5-446">Threads</span></span>

### <a name="example"></a><span data-ttu-id="d96e5-447">Esempio</span><span class="sxs-lookup"><span data-stu-id="d96e5-447">Example</span></span>

```C
/* Stop the TFTP Server called “my_server”. */
status =  nxd_tftp_server_stop(&my_server);

/* If status is NX_SUCCESS the TFTP Server is stopped. */
```