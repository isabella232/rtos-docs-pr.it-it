---
title: Capitolo 3-Descrizione dei servizi client POP3 di Azure RTO NetX
description: Questo capitolo contiene una descrizione di tutti i servizi client POP3 di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1a0ab96a454bea9f56ced0d7aa8de5d481b284e9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822565"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pop3-client-services"></a><span data-ttu-id="ab71d-103">Capitolo 3-Descrizione dei servizi client POP3 di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="ab71d-103">Chapter 3 - Description of Azure RTOS NetX POP3 Client services</span></span>

<span data-ttu-id="ab71d-104">Questo capitolo contiene una descrizione di tutti i servizi client POP3 di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="ab71d-104">This chapter contains a description of all Azure RTOS NetX POP3 Client services (listed below) in alphabetical order.</span></span>

<span data-ttu-id="ab71d-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="ab71d-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="ab71d-106">nx_pop3_client_create: *creare un'istanza del client POP3*</span><span class="sxs-lookup"><span data-stu-id="ab71d-106">nx_pop3_client_create: *Create a POP3 Client Instance*</span></span>
- <span data-ttu-id="ab71d-107">nx_pop3_client_delete: *eliminare un'istanza del client POP3*</span><span class="sxs-lookup"><span data-stu-id="ab71d-107">nx_pop3_client_delete: *Delete a POP3 Client instance*</span></span>
- <span data-ttu-id="ab71d-108">nx_pop3_client_ mail_item_get: *eliminare un elemento di posta elettronica client dal server alla maildrop.*</span><span class="sxs-lookup"><span data-stu-id="ab71d-108">nx_pop3_client_ mail_item_get: *Delete a Client mail item from Server maildrop*</span></span>
- <span data-ttu-id="ab71d-109">nx_pop3_client_mail_item_get: *recuperare una dimensione del messaggio di posta elettronica specifica*</span><span class="sxs-lookup"><span data-stu-id="ab71d-109">nx_pop3_client_mail_item_get: *Retrieve a specific mail message size*</span></span>
- <span data-ttu-id="ab71d-110">nx_pop3_client_mail_items_get: *ottenere il numero di elementi di posta elettronica in alla maildrop.*</span><span class="sxs-lookup"><span data-stu-id="ab71d-110">nx_pop3_client_mail_items_get: *Obtain the number of mail items in maildrop*</span></span>
- <span data-ttu-id="ab71d-111">nx_pop3_client_mail_item_message _get: *scaricare un messaggio di posta elettronica specifico*</span><span class="sxs-lookup"><span data-stu-id="ab71d-111">nx_pop3_client_mail_item_message _get: *Download a specific mail message*</span></span>
- <span data-ttu-id="ab71d-112">nx_pop3_client_mail_item_size_get: *ottenere le dimensioni di un elemento di posta elettronica specifico*</span><span class="sxs-lookup"><span data-stu-id="ab71d-112">nx_pop3_client_mail_item_size_get: *Obtain the size of a specific mail item*</span></span>

## <a name="nx_pop3_client_create"></a><span data-ttu-id="ab71d-113">nx_pop3_client_create</span><span class="sxs-lookup"><span data-stu-id="ab71d-113">nx_pop3_client_create</span></span>

<span data-ttu-id="ab71d-114">Creare un'istanza del client POP3</span><span class="sxs-lookup"><span data-stu-id="ab71d-114">Create a POP3 Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="ab71d-115">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ab71d-115">Prototype</span></span>

```c
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
                        UINT APOP_authentication, NX_IP *ip_ptr,
                        NX_PACKET_POOL *packet_pool_ptr,
                        ULONG server_ip_address,
                        ULONG server_port,
                        CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a><span data-ttu-id="ab71d-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab71d-116">Description</span></span>

<span data-ttu-id="ab71d-117">Questo servizio crea un'istanza del client POP3 e ne configura la configurazione con i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="ab71d-117">This service creates an instance of the POP3 Client and sets up its configuration with the input parameters.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab71d-118">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ab71d-118">Input Parameters</span></span>

- <span data-ttu-id="ab71d-119">**client_ptr**: puntatore al client da creare</span><span class="sxs-lookup"><span data-stu-id="ab71d-119">**client_ptr**: Pointer to Client to create</span></span>
- <span data-ttu-id="ab71d-120">**APOP_authentication**: abilitare l'autenticazione APOP</span><span class="sxs-lookup"><span data-stu-id="ab71d-120">**APOP_authentication**: Enable APOP authentication</span></span>
- <span data-ttu-id="ab71d-121">**ip_ptr**: puntatore a istanza IP</span><span class="sxs-lookup"><span data-stu-id="ab71d-121">**ip_ptr**: Pointer to IP instance</span></span>
- <span data-ttu-id="ab71d-122">**packet_pool_ptr**: puntatore al pool di pacchetti client</span><span class="sxs-lookup"><span data-stu-id="ab71d-122">**packet_pool_ptr**: Pointer to Client packet pool</span></span>
- <span data-ttu-id="ab71d-123">**server_ip_address**: indirizzo del server POP3</span><span class="sxs-lookup"><span data-stu-id="ab71d-123">**server_ip_address**: POP3 server address</span></span>
- <span data-ttu-id="ab71d-124">**SERVER_PORT**: porta server POP3</span><span class="sxs-lookup"><span data-stu-id="ab71d-124">**server_port**: POP3 server port</span></span>
- <span data-ttu-id="ab71d-125">**client_name**: puntatore al nome client</span><span class="sxs-lookup"><span data-stu-id="ab71d-125">**client_name**: Pointer to Client name</span></span>
- <span data-ttu-id="ab71d-126">**client_password**: puntatore alla password client</span><span class="sxs-lookup"><span data-stu-id="ab71d-126">**client_password**: Pointer to Client password</span></span>

### <a name="return-values"></a><span data-ttu-id="ab71d-127">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ab71d-127">Return Values</span></span>

- <span data-ttu-id="ab71d-128">**NX_SUCCESS**: (0x00) client creato correttamente</span><span class="sxs-lookup"><span data-stu-id="ab71d-128">**NX_SUCCESS**: (0x00) Client successfully created</span></span>
- <span data-ttu-id="ab71d-129">**stato**: completamento dello stato delle chiamate al servizio NETX e threadX</span><span class="sxs-lookup"><span data-stu-id="ab71d-129">**status**: Status completion of NetX and ThreadX service calls</span></span>
- <span data-ttu-id="ab71d-130">NX_PTR_ERROR: (0x07) parametro puntatore di input non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-130">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="ab71d-131">NX_POP3_PARAM_ERROR: (0xB1) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-131">NX_POP3_PARAM_ERROR: (0xB1) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab71d-132">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ab71d-132">Allowed From</span></span>

<span data-ttu-id="ab71d-133">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ab71d-133">Application code</span></span>

### <a name="example"></a><span data-ttu-id="ab71d-134">Esempio</span><span class="sxs-lookup"><span data-stu-id="ab71d-134">Example</span></span>

```c
/* Create the POP3 Client. */

/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST                   "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD          "pass"
#define POP3_SERVER_ADDRESS         IP_ADDRESS(192,2,2,92
#define POP3_SERVER_PORT            110

/* Create a NetX POP3 Client instance. */
ULONG server_ip_address = IP_ADDRESS(1,2,3,4);
status = nx_pop3_client_create(&demo_client,
        NX_FALSE /* disable APOP authentication */,
        &client_ip, &client_packet_pool,
        server_ip_address, POP3_SERVER_PORT,
        LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_delete"></a><span data-ttu-id="ab71d-135">nx_pop3_client_delete</span><span class="sxs-lookup"><span data-stu-id="ab71d-135">nx_pop3_client_delete</span></span>

<span data-ttu-id="ab71d-136">Eliminare un'istanza del client POP3</span><span class="sxs-lookup"><span data-stu-id="ab71d-136">Delete a POP3 Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="ab71d-137">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ab71d-137">Prototype</span></span>

```c
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr)
```

### <a name="description"></a><span data-ttu-id="ab71d-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab71d-138">Description</span></span>

<span data-ttu-id="ab71d-139">Questo servizio Elimina un client POP3 creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ab71d-139">This service deletes a previously created POP3 Client.</span></span> <span data-ttu-id="ab71d-140">Il servizio non elimina il pool di pacchetti client POP3.</span><span class="sxs-lookup"><span data-stu-id="ab71d-140">Not that this service does not delete the POP3 Client packet pool.</span></span> <span data-ttu-id="ab71d-141">L'applicazione del dispositivo deve eliminare questa risorsa separatamente se non è più usata per il pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ab71d-141">The device application must delete this resource separately if it no longer has use for the packet pool.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab71d-142">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ab71d-142">Input Parameters</span></span>

- <span data-ttu-id="ab71d-143">**client_ptr**: puntatore al client da eliminare</span><span class="sxs-lookup"><span data-stu-id="ab71d-143">**client_ptr**: Pointer to Client to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="ab71d-144">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ab71d-144">Return Values</span></span>

- <span data-ttu-id="ab71d-145">**NX_SUCCESS**: (0x00) client eliminato correttamente</span><span class="sxs-lookup"><span data-stu-id="ab71d-145">**NX_SUCCESS**: (0x00) Client successfully deleted</span></span>
- <span data-ttu-id="ab71d-146">NX_PTR_ERROR: (0x07) parametro puntatore di input non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-146">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab71d-147">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ab71d-147">Allowed From</span></span>

<span data-ttu-id="ab71d-148">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ab71d-148">Application code</span></span>

### <a name="example"></a><span data-ttu-id="ab71d-149">Esempio</span><span class="sxs-lookup"><span data-stu-id="ab71d-149">Example</span></span>

```c
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a><span data-ttu-id="ab71d-150">nx_pop3_client_mail_item_delete</span><span class="sxs-lookup"><span data-stu-id="ab71d-150">nx_pop3_client_mail_item_delete</span></span>

<span data-ttu-id="ab71d-151">Elimina un elemento di posta specificato dal client alla maildrop.</span><span class="sxs-lookup"><span data-stu-id="ab71d-151">Delete a specified mail item from the Client maildrop</span></span>

### <a name="prototype"></a><span data-ttu-id="ab71d-152">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ab71d-152">Prototype</span></span>

```c
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
                                    UINT mail_index)
```

### <a name="description"></a><span data-ttu-id="ab71d-153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab71d-153">Description</span></span>

<span data-ttu-id="ab71d-154">Questo servizio Elimina l'elemento di posta specificato dal client alla maildrop..</span><span class="sxs-lookup"><span data-stu-id="ab71d-154">This service deletes the specified mail item from the Client maildrop.</span></span> <span data-ttu-id="ab71d-155">È destinato a dopo il download dell'elemento di posta elettronica, anche se alcuni server POP3 possono eliminare automaticamente gli elementi di posta dopo essere stati richiesti dal client.</span><span class="sxs-lookup"><span data-stu-id="ab71d-155">It is intended for after downloading the mail item, although some POP3 servers may automatically delete mail items after being requested by the Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab71d-156">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ab71d-156">Input Parameters</span></span>

- <span data-ttu-id="ab71d-157">**client_ptr**: puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="ab71d-157">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="ab71d-158">**mail_index**: indicizzare in alla maildrop. client</span><span class="sxs-lookup"><span data-stu-id="ab71d-158">**mail_index**: Index into Client maildrop</span></span>

### <a name="return-values"></a><span data-ttu-id="ab71d-159">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ab71d-159">Return Values</span></span>

- <span data-ttu-id="ab71d-160">**NX_SUCCESS**: (0x00) la richiesta di eliminazione è riuscita</span><span class="sxs-lookup"><span data-stu-id="ab71d-160">**NX_SUCCESS**: (0x00) Delete request successful</span></span>
- <span data-ttu-id="ab71d-161">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) indice elemento di posta elettronica non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-161">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="ab71d-162">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) il payload del pacchetto client è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="ab71d-162">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="ab71d-163">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) il server risponde con lo stato di errore</span><span class="sxs-lookup"><span data-stu-id="ab71d-163">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="ab71d-164">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) input dell'indice di posta non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-164">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="ab71d-165">NX_PTR_ERROR: (0x07) parametro puntatore di input non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-165">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab71d-166">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ab71d-166">Allowed From</span></span>

<span data-ttu-id="ab71d-167">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ab71d-167">Application code</span></span>

### <a name="example"></a><span data-ttu-id="ab71d-168">Esempio</span><span class="sxs-lookup"><span data-stu-id="ab71d-168">Example</span></span>

```c
ULONG     item_index;

/* Delete the POP3 Client mail item. */
status = nx_pop3_client_mail_item_delete(&demo_client, item_index);

/* If the server accepts the DELE request (and deletes the mail item), status = 
   NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_get"></a><span data-ttu-id="ab71d-169">nx_pop3_client_mail_item_get</span><span class="sxs-lookup"><span data-stu-id="ab71d-169">nx_pop3_client_mail_item_get</span></span>

<span data-ttu-id="ab71d-170">Recupera un elemento di posta elettronica specificato</span><span class="sxs-lookup"><span data-stu-id="ab71d-170">Retrieve a specified mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="ab71d-171">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ab71d-171">Prototype</span></span>

```c
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
                                UINT mail_item, ULONG *item_size)
```

### <a name="description"></a><span data-ttu-id="ab71d-172">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab71d-172">Description</span></span>

<span data-ttu-id="ab71d-173">Questo servizio esegue una richiesta RETR per recuperare un elemento di posta dal client alla maildrop. specificato dall'indice mail_item.</span><span class="sxs-lookup"><span data-stu-id="ab71d-173">This service makes a RETR request to retrieve a mail item from the Client maildrop specified by the index mail_item.</span></span> <span data-ttu-id="ab71d-174">Dopo aver eseguito una richiesta RETR e aver ricevuto una risposta positiva dal server, il client può avviare il download del messaggio di posta elettronica usando il servizio *nx_pop3_client_mail_item_message_get* .</span><span class="sxs-lookup"><span data-stu-id="ab71d-174">After making a RETR request, and receiving a positive response from the Server, the Client can start downloading the mail message using the *nx_pop3_client_mail_item_message_get* service.</span></span> <span data-ttu-id="ab71d-175">Si noti che il servizio fornisce anche la dimensione dell'elemento di posta elettronica richiesto estratto dalla risposta del server.</span><span class="sxs-lookup"><span data-stu-id="ab71d-175">Note that the service also supplies the size of the requested mail item extracted from the Server reply.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab71d-176">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ab71d-176">Input Parameters</span></span>

- <span data-ttu-id="ab71d-177">**client_ptr**: puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="ab71d-177">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="ab71d-178">**mail_item**: indicizzare in alla maildrop. client</span><span class="sxs-lookup"><span data-stu-id="ab71d-178">**mail_item**: Index into Client maildrop</span></span>
- <span data-ttu-id="ab71d-179">**item_size**: puntatore alla dimensione del messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="ab71d-179">**item_size**: Pointer to size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="ab71d-180">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ab71d-180">Return Values</span></span>

- <span data-ttu-id="ab71d-181">**NX_SUCCESS**: (0x00) elemento di posta recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="ab71d-181">**NX_SUCCESS**: (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="ab71d-182">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) indice elemento di posta elettronica non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-182">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="ab71d-183">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) il payload del pacchetto client è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="ab71d-183">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="ab71d-184">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) il server risponde con lo stato di errore</span><span class="sxs-lookup"><span data-stu-id="ab71d-184">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="ab71d-185">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) input dell'indice di posta non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-185">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="ab71d-186">NX_PTR_ERROR: (0x07) parametro puntatore di input non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-186">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab71d-187">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ab71d-187">Allowed From</span></span>

<span data-ttu-id="ab71d-188">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ab71d-188">Application code</span></span>

### <a name="example"></a><span data-ttu-id="ab71d-189">Esempio</span><span class="sxs-lookup"><span data-stu-id="ab71d-189">Example</span></span>

```c
ULONG     item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a><span data-ttu-id="ab71d-190">nx_pop3_client_mail_items_get</span><span class="sxs-lookup"><span data-stu-id="ab71d-190">nx_pop3_client_mail_items_get</span></span>

<span data-ttu-id="ab71d-191">Recuperare il numero di elementi di posta elettronica in alla maildrop.</span><span class="sxs-lookup"><span data-stu-id="ab71d-191">Retrieve the number of mail items in maildrop</span></span>

### <a name="prototype"></a><span data-ttu-id="ab71d-192">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ab71d-192">Prototype</span></span>

```c
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
                                UINT *number_mail_items,
                                ULONG *maildrop_total_size)
```

### <a name="description"></a><span data-ttu-id="ab71d-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab71d-193">Description</span></span>

<span data-ttu-id="ab71d-194">Questo servizio esegue una richiesta STAT per recuperare il numero di elementi di posta e le dimensioni totali dei dati del messaggio di posta elettronica dal client alla maildrop..</span><span class="sxs-lookup"><span data-stu-id="ab71d-194">This service makes a STAT request to retrieve the number of mail items and total size of mail message data from the Client maildrop.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab71d-195">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ab71d-195">Input Parameters</span></span>

- <span data-ttu-id="ab71d-196">**client_ptr**: puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="ab71d-196">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="ab71d-197">**number_mail_item**: numero di messaggi di posta elettronica nel client alla maildrop.</span><span class="sxs-lookup"><span data-stu-id="ab71d-197">**number_mail_item**: Number of mail in Client maildrop</span></span>
- <span data-ttu-id="ab71d-198">**maildrop_total_size**: puntatore alla dimensione di tutti i messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="ab71d-198">**maildrop_total_size**: Pointer to size of all mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="ab71d-199">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ab71d-199">Return Values</span></span>

- <span data-ttu-id="ab71d-200">**NX_SUCCESS**: (0x00) elemento di posta recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="ab71d-200">**NX_SUCCESS**: (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="ab71d-201">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) indice elemento di posta elettronica non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-201">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="ab71d-202">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) il payload del pacchetto client è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="ab71d-202">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="ab71d-203">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) il server risponde con lo stato di errore</span><span class="sxs-lookup"><span data-stu-id="ab71d-203">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) Server replies with error status</span></span> 
- <span data-ttu-id="ab71d-204">NX_PTR_ERROR: (0x07) parametro puntatore di input non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-204">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab71d-205">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ab71d-205">Allowed From</span></span>

<span data-ttu-id="ab71d-206">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ab71d-206">Application code</span></span>

### <a name="example"></a><span data-ttu-id="ab71d-207">Esempio</span><span class="sxs-lookup"><span data-stu-id="ab71d-207">Example</span></span>

```c
UINT      number_mail_items;
ULONG     maildrop_total_size;

/* Retrieve the size and number of items in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &number_mail_items,
                                        &maildrop_total_size);

/* If the maildrop data was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_message_get"></a><span data-ttu-id="ab71d-208">nx_pop3_client_mail_item_message_get</span><span class="sxs-lookup"><span data-stu-id="ab71d-208">nx_pop3_client_mail_item_message_get</span></span>

<span data-ttu-id="ab71d-209">Recupera il messaggio di elemento di posta specificato</span><span class="sxs-lookup"><span data-stu-id="ab71d-209">Retrieve the specified mail item message</span></span>

### <a name="prototype"></a><span data-ttu-id="ab71d-210">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ab71d-210">Prototype</span></span>

```c
UINT nx_pop3_client_mail_item_message_get(
                NX_POP3_CLIENT *client_ptr,
                NX_PACKET **recv_packet_ptr,
                ULONG *bytes_retrieved,
                UINT *final_packet)
```

### <a name="description"></a><span data-ttu-id="ab71d-211">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab71d-211">Description</span></span>

<span data-ttu-id="ab71d-212">Questo servizio recupera il messaggio dell'elemento di posta, le dimensioni del messaggio di posta elettronica e se è l'ultimo pacchetto del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="ab71d-212">This service retrieves the mail item message, size of the mail message, and if it is the last packet in the mail message.</span></span> <span data-ttu-id="ab71d-213">Se `final_packet` è NX_TRUE il pacchetto a cui punta `recv_packet_ptr` è il pacchetto finale nel messaggio dell'elemento di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="ab71d-213">If `final_packet` is NX_TRUE the packet pointed to by `recv_packet_ptr` is the final packet in the mail item message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab71d-214">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ab71d-214">Input Parameters</span></span>

- <span data-ttu-id="ab71d-215">**client_ptr**: puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="ab71d-215">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="ab71d-216">**recv_packet_ptr**: ricevuto pacchetto di dati del messaggio</span><span class="sxs-lookup"><span data-stu-id="ab71d-216">**recv_packet_ptr**: Received packet of message data</span></span>
- <span data-ttu-id="ab71d-217">**number_mail_item**: numero di messaggi di posta elettronica nel client alla maildrop.</span><span class="sxs-lookup"><span data-stu-id="ab71d-217">**number_mail_item**: Number of mail in Client maildrop</span></span>
- <span data-ttu-id="ab71d-218">**maildrop_total_size**: puntatore alla dimensione di tutti i messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="ab71d-218">**maildrop_total_size**: Pointer to size of all mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="ab71d-219">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ab71d-219">Return Values</span></span>

- <span data-ttu-id="ab71d-220">**NX_SUCCESS**: (0x00) elemento di posta recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="ab71d-220">**NX_SUCCESS**: (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="ab71d-221">**NX_POP3_CLIENT_INVALID_STATE**: (0xB7) il payload del pacchetto client è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="ab71d-221">**NX_POP3_CLIENT_INVALID_STATE**: (0xB7) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="ab71d-222">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-222">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab71d-223">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ab71d-223">Allowed From</span></span>

<span data-ttu-id="ab71d-224">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ab71d-224">Application code</span></span>

### <a name="example"></a><span data-ttu-id="ab71d-225">Esempio</span><span class="sxs-lookup"><span data-stu-id="ab71d-225">Example</span></span>

```c
NX_PACKET     *recv_packet_ptr;
ULONG         bytes_retrieved;
UINT          final_packet;

/* Retrieve the size and number of items in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_message_get (&demo_client, &recv_packet_ptr,
                                                bytes_retrieved, final_packet);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_size_get"></a><span data-ttu-id="ab71d-226">nx_pop3_client_mail_item_size_get</span><span class="sxs-lookup"><span data-stu-id="ab71d-226">nx_pop3_client_mail_item_size_get</span></span>

<span data-ttu-id="ab71d-227">Recupera la dimensione dell'elemento di posta elettronica specificato</span><span class="sxs-lookup"><span data-stu-id="ab71d-227">Retrieve the size of the specified mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="ab71d-228">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ab71d-228">Prototype</span></span>

```c
UINT nx_pop3_client_mail_item_size_get(
                NX_POP3_CLIENT *client_ptr,
                UINT mail_item, ULONG *size)
```

### <a name="description"></a><span data-ttu-id="ab71d-229">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ab71d-229">Description</span></span>

<span data-ttu-id="ab71d-230">Questo servizio esegue una richiesta di elenco per ottenere la dimensione dell'elemento di posta elettronica specificato.</span><span class="sxs-lookup"><span data-stu-id="ab71d-230">This service makes a LIST request to obtain the size of the specified mail item.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab71d-231">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ab71d-231">Input Parameters</span></span>

- <span data-ttu-id="ab71d-232">**client_ptr**: puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="ab71d-232">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="ab71d-233">**mail_item**: indicizzare in alla maildrop. client</span><span class="sxs-lookup"><span data-stu-id="ab71d-233">**mail_item**: Index into Client maildrop</span></span>
- <span data-ttu-id="ab71d-234">**dimensioni**: puntatore alla dimensione del messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="ab71d-234">**size**: Pointer to size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="ab71d-235">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ab71d-235">Return Values</span></span>

- <span data-ttu-id="ab71d-236">**NX_SUCCESS**: (0x00) elemento di posta recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="ab71d-236">**NX_SUCCESS**: (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="ab71d-237">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) indice elemento di posta elettronica non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-237">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="ab71d-238">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) il payload del pacchetto client è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="ab71d-238">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="ab71d-239">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) il server risponde con lo stato di errore</span><span class="sxs-lookup"><span data-stu-id="ab71d-239">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="ab71d-240">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) input dell'indice di posta non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-240">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="ab71d-241">NX_PTR_ERROR: (0x07) parametro puntatore di input non valido</span><span class="sxs-lookup"><span data-stu-id="ab71d-241">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab71d-242">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ab71d-242">Allowed From</span></span>

<span data-ttu-id="ab71d-243">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ab71d-243">Application code</span></span>

### <a name="example"></a><span data-ttu-id="ab71d-244">Esempio</span><span class="sxs-lookup"><span data-stu-id="ab71d-244">Example</span></span>

```c
ULONG     size;
UINT      mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
