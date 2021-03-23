---
title: Capitolo 3-Descrizione dei servizi client POP3
description: Questo capitolo contiene una descrizione di tutti i servizi client POP3 di NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1f7681c8f3fe161db8a37a82574ab7d5e9bf348e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821746"
---
# <a name="chapter-3---description-of-pop3-client-services"></a><span data-ttu-id="5c83d-103">Capitolo 3-Descrizione dei servizi client POP3</span><span class="sxs-lookup"><span data-stu-id="5c83d-103">Chapter 3 - Description of POP3 Client Services</span></span>

<span data-ttu-id="5c83d-104">Questo capitolo contiene una descrizione di tutti i servizi client POP3 di NetX Duo (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="5c83d-104">This chapter contains a description of all NetX Duo POP3 Client services (listed below) in alphabetical order.</span></span>

> [!NOTE]
> <span data-ttu-id="5c83d-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="5c83d-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_pop3_client_create"></a><span data-ttu-id="5c83d-106">nx_pop3_client_create</span><span class="sxs-lookup"><span data-stu-id="5c83d-106">nx_pop3_client_create</span></span>

<span data-ttu-id="5c83d-107">Creare un'istanza del client POP3 per IPv4</span><span class="sxs-lookup"><span data-stu-id="5c83d-107">Create a POP3 Client instance for IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="5c83d-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5c83d-108">Prototype</span></span>

```C
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    ULONG server_ip_address, ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a><span data-ttu-id="5c83d-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c83d-109">Description</span></span>

<span data-ttu-id="5c83d-110">Questo servizio crea un'istanza del client POP3.</span><span class="sxs-lookup"><span data-stu-id="5c83d-110">This service creates an instance of the POP3 Client.</span></span> <span data-ttu-id="5c83d-111">Supporta solo indirizzi server POP3 IPv4.</span><span class="sxs-lookup"><span data-stu-id="5c83d-111">It supports only IPv4 POP3 server addresses.</span></span>

<span data-ttu-id="5c83d-112">Si noti che l'applicazione del dispositivo deve prima creare un'istanza IP e un pool di pacchetti affinché il client POP3 trasmetta i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5c83d-112">Note that the device application must first create an IP instance and a packet pool for the POP3 Client to transmit packets.</span></span> <span data-ttu-id="5c83d-113">Questo pool di pacchetti creato per essere utilizzato esclusivamente dall'attività client POP3 o dallo stesso pool di pacchetti utilizzato nella creazione dell'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="5c83d-113">This packet pool created for use exclusively by the POP3 Client task or the same packet pool used in the IP instance creation.</span></span> <span data-ttu-id="5c83d-114">Il pool di pacchetti può anche essere condiviso con il pool di pacchetti di driver Ethernet, ma ciò presenta lo svantaggio di usare pool di pacchetti di grandi dimensioni il cui payload è destinato alla ricezione di un payload di pacchetti potenzialmente grande per il client POP3 per inviare pacchetti di messaggi POP3 relativamente piccoli al server.</span><span class="sxs-lookup"><span data-stu-id="5c83d-114">The packet pool may also be shared with the Ethernet driver packet pool but this has the disadvantage of using large packet pools whose payload is intended for receiving potentially large packets payload for the POP3 Client to send relatively small POP3 message packets to the server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5c83d-115">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5c83d-115">Input Parameters</span></span>

- <span data-ttu-id="5c83d-116">**client_ptr** Puntatore al client da creare</span><span class="sxs-lookup"><span data-stu-id="5c83d-116">**client_ptr** Pointer to Client to create</span></span>
- <span data-ttu-id="5c83d-117">**APOP_authentication** Abilitare l'autenticazione APOP</span><span class="sxs-lookup"><span data-stu-id="5c83d-117">**APOP_authentication** Enable APOP authentication</span></span>
- <span data-ttu-id="5c83d-118">**puntatore ip_ptr** all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="5c83d-118">**ip_ptr Pointer** to IP instance</span></span>
- <span data-ttu-id="5c83d-119">**packet_pool_ptr** Puntatore al pool di pacchetti client</span><span class="sxs-lookup"><span data-stu-id="5c83d-119">**packet_pool_ptr** Pointer to Client packet pool</span></span>
- <span data-ttu-id="5c83d-120">**server_ip_address** Indirizzo IPv4 del server POP3</span><span class="sxs-lookup"><span data-stu-id="5c83d-120">**server_ip_address** POP3 server IPv4 address</span></span>
- <span data-ttu-id="5c83d-121">**SERVER_PORT** Porta server POP3</span><span class="sxs-lookup"><span data-stu-id="5c83d-121">**server_port** POP3 server port</span></span>
- <span data-ttu-id="5c83d-122">**client_name** Puntatore al nome client</span><span class="sxs-lookup"><span data-stu-id="5c83d-122">**client_name** Pointer to Client name</span></span>
- <span data-ttu-id="5c83d-123">**client_password** Puntatore alla password client</span><span class="sxs-lookup"><span data-stu-id="5c83d-123">**client_password** Pointer to Client password</span></span>

### <a name="return-values"></a><span data-ttu-id="5c83d-124">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5c83d-124">Return Values</span></span>

- <span data-ttu-id="5c83d-125">Creazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="5c83d-125">**NX_SUCCESS** (0x00) Client successfully created</span></span>
- <span data-ttu-id="5c83d-126">**stato** di Stato di completamento delle chiamate al servizio NetX Duo e ThreadX</span><span class="sxs-lookup"><span data-stu-id="5c83d-126">**status** Status completion of NetX Duo and ThreadX service calls</span></span>
- <span data-ttu-id="5c83d-127">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-127">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="5c83d-128">NX_POP3_PARAM_ERROR (0xB1) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-128">NX_POP3_PARAM_ERROR (0xB1) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5c83d-129">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5c83d-129">Allowed From</span></span>

<span data-ttu-id="5c83d-130">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5c83d-130">Application code</span></span>

### <a name="example"></a><span data-ttu-id="5c83d-131">Esempio</span><span class="sxs-lookup"><span data-stu-id="5c83d-131">Example</span></span>

```C
/* Create the POP3 Client. Note that the Client uses its password for its APOP shared
    secret. */

/* Set up user defined callback services. */
/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD "pass"
#define POP3_SERVER_ADDRESS IP_ADDRESS(192,2,2,92)
#define POP3_SERVER_PORT 110

/* Create a NetX POP3 Client instance. */
status = nx_pop3_client_create(&demo_client,
    NX_FALSE /* disable APOP authentication */,
    &client_ip, &client_packet_pool,
    POP3_SERVER_ADDRESS, POP3_SERVER_PORT,
    LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nxd_pop3_client_create"></a><span data-ttu-id="5c83d-132">nxd_pop3_client_create</span><span class="sxs-lookup"><span data-stu-id="5c83d-132">nxd_pop3_client_create</span></span>

<span data-ttu-id="5c83d-133">Creare un'istanza del client POP3 per IPv4 o IPv6</span><span class="sxs-lookup"><span data-stu-id="5c83d-133">Create a POP3 Client instance for IPv4 or IPv6</span></span>

### <a name="prototype"></a><span data-ttu-id="5c83d-134">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5c83d-134">Prototype</span></span>

```C
UINT nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    NXD_ADDRESS *server_ip_address,
    ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a><span data-ttu-id="5c83d-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c83d-135">Description</span></span>

<span data-ttu-id="5c83d-136">Questo servizio crea un'istanza del client POP3.</span><span class="sxs-lookup"><span data-stu-id="5c83d-136">This service creates an instance of the POP3 Client.</span></span> <span data-ttu-id="5c83d-137">Supporta indirizzi server POP3 sia IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="5c83d-137">It supports both IPv4 and IPv6 POP3 server addresses.</span></span> <span data-ttu-id="5c83d-138">Per ulteriori informazioni sul processo di creazione del client POP3, vedere il servizio *nx_pop3_client_create* descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5c83d-138">See the previously described *nx_pop3_client_create* service for more details on POP3 Client create process.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5c83d-139">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5c83d-139">Input Parameters</span></span>

- <span data-ttu-id="5c83d-140">**client_ptr** Puntatore al client da creare</span><span class="sxs-lookup"><span data-stu-id="5c83d-140">**client_ptr** Pointer to Client to create</span></span>
- <span data-ttu-id="5c83d-141">**APOP_authentication** Abilitare l'autenticazione APOP</span><span class="sxs-lookup"><span data-stu-id="5c83d-141">**APOP_authentication** Enable APOP authentication</span></span>
- <span data-ttu-id="5c83d-142">**ip_ptr** Puntatore a istanza IP</span><span class="sxs-lookup"><span data-stu-id="5c83d-142">**ip_ptr** Pointer to IP instance</span></span>
- <span data-ttu-id="5c83d-143">**packet_pool_ptr** Puntatore al pool di pacchetti client</span><span class="sxs-lookup"><span data-stu-id="5c83d-143">**packet_pool_ptr** Pointer to Client packet pool</span></span>
- <span data-ttu-id="5c83d-144">**server_ip_address** Indirizzo IPv4 o IPv6 del server POP3</span><span class="sxs-lookup"><span data-stu-id="5c83d-144">**server_ip_address** POP3 server IPv6 or IPv4 address</span></span>
- <span data-ttu-id="5c83d-145">**SERVER_PORT** Porta server POP3</span><span class="sxs-lookup"><span data-stu-id="5c83d-145">**server_port** POP3 server port</span></span>
- <span data-ttu-id="5c83d-146">**client_name**  Puntatore al nome client</span><span class="sxs-lookup"><span data-stu-id="5c83d-146">**client_name**  Pointer to Client name</span></span>
- <span data-ttu-id="5c83d-147">**client_password** Puntatore alla password client</span><span class="sxs-lookup"><span data-stu-id="5c83d-147">**client_password** Pointer to Client password</span></span>

### <a name="return-values"></a><span data-ttu-id="5c83d-148">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5c83d-148">Return Values</span></span>

- <span data-ttu-id="5c83d-149">Creazione del client **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="5c83d-149">**NX_SUCCESS** (0x00) Client successfully created</span></span>
- <span data-ttu-id="5c83d-150">**stato** di Stato di completamento delle chiamate al servizio NetX Duo e ThreadX</span><span class="sxs-lookup"><span data-stu-id="5c83d-150">**status** Status completion of NetX Duo and ThreadX service calls</span></span>
- <span data-ttu-id="5c83d-151">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-151">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="5c83d-152">NX_POP3_PARAM_ERROR (0xB1) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-152">NX_POP3_PARAM_ERROR (0xB1) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5c83d-153">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5c83d-153">Allowed From</span></span>

<span data-ttu-id="5c83d-154">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5c83d-154">Application code</span></span>

### <a name="example"></a><span data-ttu-id="5c83d-155">Esempio</span><span class="sxs-lookup"><span data-stu-id="5c83d-155">Example</span></span>

```C
/* Create the POP3 Client. */

/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD "pass"
#define POP3_SERVER_PORT 110

/* Create a NetX POP3 Client instance. Also note the details of IPv6 address validation
    and enabling IPv6 and ICMPv6 services on the IP task are not shown here. See the
    NetX Duo User Guide for more details on this process.
*/
NXD_ADDRESS server_ip_address;

/* Set client IP interface address. */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0xf101;
server_ip_address.nxd_ip_address.v6[2] = 0;
server_ip_address.nxd_ip_address.v6[3] = 0x101;
status = nxd_pop3_client_create(&demo_client,
    NX_FALSE /* disable APOP authentication */,
    &client_ip, &client_packet_pool,
    &server_ip_address, POP3_SERVER_PORT,
    LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_delete"></a><span data-ttu-id="5c83d-156">nx_pop3_client_delete</span><span class="sxs-lookup"><span data-stu-id="5c83d-156">nx_pop3_client_delete</span></span>

<span data-ttu-id="5c83d-157">Eliminare un'istanza del client POP3</span><span class="sxs-lookup"><span data-stu-id="5c83d-157">Delete a POP3 Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="5c83d-158">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5c83d-158">Prototype</span></span>

```C
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="5c83d-159">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c83d-159">Description</span></span>

<span data-ttu-id="5c83d-160">Questo servizio Elimina un client POP3 creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5c83d-160">This service deletes a previously created POP3 Client.</span></span> <span data-ttu-id="5c83d-161">Il servizio non elimina il pool di pacchetti client POP3.</span><span class="sxs-lookup"><span data-stu-id="5c83d-161">Not that this service does not delete the POP3 Client packet pool.</span></span> <span data-ttu-id="5c83d-162">L'applicazione del dispositivo deve eliminare questa risorsa separatamente se non è più usata per il pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5c83d-162">The device application must delete this resource separately if it no longer has use for the packet pool.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5c83d-163">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5c83d-163">Input Parameters</span></span>

- <span data-ttu-id="5c83d-164">**client_ptr** Puntatore al client da eliminare</span><span class="sxs-lookup"><span data-stu-id="5c83d-164">**client_ptr** Pointer to Client to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="5c83d-165">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5c83d-165">Return Values</span></span>

- <span data-ttu-id="5c83d-166">Il client **NX_SUCCESS** (0x00) è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="5c83d-166">**NX_SUCCESS** (0x00) Client successfully deleted</span></span>
- <span data-ttu-id="5c83d-167">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-167">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5c83d-168">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5c83d-168">Allowed From</span></span>

<span data-ttu-id="5c83d-169">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5c83d-169">Application code</span></span>

### <a name="example"></a><span data-ttu-id="5c83d-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="5c83d-170">Example</span></span>

```C
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a><span data-ttu-id="5c83d-171">nx_pop3_client_mail_item_delete</span><span class="sxs-lookup"><span data-stu-id="5c83d-171">nx_pop3_client_mail_item_delete</span></span>

<span data-ttu-id="5c83d-172">Elimina un elemento di posta specificato dal client alla maildrop.</span><span class="sxs-lookup"><span data-stu-id="5c83d-172">Delete a specified mail item from the Client maildrop</span></span>

### <a name="prototype"></a><span data-ttu-id="5c83d-173">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5c83d-173">Prototype</span></span>

```C
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
    UINT mail_index);
```

### <a name="description"></a><span data-ttu-id="5c83d-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c83d-174">Description</span></span>

<span data-ttu-id="5c83d-175">Questo servizio Elimina l'elemento di posta specificato dal client alla maildrop..</span><span class="sxs-lookup"><span data-stu-id="5c83d-175">This service deletes the specified mail item from the Client maildrop.</span></span> <span data-ttu-id="5c83d-176">È destinato a dopo il download dell'elemento di posta elettronica, anche se alcuni server POP3 possono eliminare automaticamente gli elementi di posta dopo essere stati richiesti dal client.</span><span class="sxs-lookup"><span data-stu-id="5c83d-176">It is intended for after downloading the mail item, although some POP3 servers may automatically delete mail items after being requested by the Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5c83d-177">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5c83d-177">Input Parameters</span></span>

- <span data-ttu-id="5c83d-178">**client_ptr** Puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="5c83d-178">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="5c83d-179">**mail_index** Indicizza in alla maildrop. client</span><span class="sxs-lookup"><span data-stu-id="5c83d-179">**mail_index** Index into Client maildrop</span></span>

### <a name="return-values"></a><span data-ttu-id="5c83d-180">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5c83d-180">Return Values</span></span>

- <span data-ttu-id="5c83d-181">Richiesta di eliminazione **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="5c83d-181">**NX_SUCCESS** (0x00) Delete request successful</span></span>
- <span data-ttu-id="5c83d-182">**NX_POP3_INVALID_MAIL_ITEM**(0xB2) indice elemento di posta elettronica non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-182">**NX_POP3_INVALID_MAIL_ITEM**(0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="5c83d-183">Il payload del pacchetto client **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**(0xB6) è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="5c83d-183">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**(0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="5c83d-184">Il server **NX_POP3_SERVER_ERROR_STATUS**(0xB4) risponde con lo stato di errore</span><span class="sxs-lookup"><span data-stu-id="5c83d-184">**NX_POP3_SERVER_ERROR_STATUS**(0xB4) Server replies with error status</span></span>
- <span data-ttu-id="5c83d-185">NX_POP3_CLIENT_INVALID_INDEX (0xB8) input dell'indice di posta non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-185">NX_POP3_CLIENT_INVALID_INDEX(0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="5c83d-186">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-186">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5c83d-187">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5c83d-187">Allowed From</span></span>

<span data-ttu-id="5c83d-188">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5c83d-188">Application code</span></span>

### <a name="example"></a><span data-ttu-id="5c83d-189">Esempio</span><span class="sxs-lookup"><span data-stu-id="5c83d-189">Example</span></span>

```C
ULONG item_index;

/* Delete the POP3 Client mail item. */
status = nx_pop3_client_mail_item_delete(&demo_client, item_index);

/* If the server accepts the DELE request (and deletes the mail item), status =
    NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_get"></a><span data-ttu-id="5c83d-190">nx_pop3_client_mail_item_get</span><span class="sxs-lookup"><span data-stu-id="5c83d-190">nx_pop3_client_mail_item_get</span></span>

<span data-ttu-id="5c83d-191">Recupera un elemento di posta elettronica specificato</span><span class="sxs-lookup"><span data-stu-id="5c83d-191">Retrieve a specified mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="5c83d-192">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5c83d-192">Prototype</span></span>

```C
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *item_size);
```

### <a name="description"></a><span data-ttu-id="5c83d-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c83d-193">Description</span></span>

<span data-ttu-id="5c83d-194">Questo servizio esegue una richiesta RETR per recuperare un elemento di posta dal client alla maildrop. specificato dall'indice mail_item.</span><span class="sxs-lookup"><span data-stu-id="5c83d-194">This service makes a RETR request to retrieve a mail item from the Client maildrop specified by the index mail_item.</span></span> <span data-ttu-id="5c83d-195">Dopo aver eseguito una richiesta RETR e aver ricevuto una risposta positiva dal server, il client può avviare il download del messaggio di posta elettronica usando il servizio *nx_pop3_client_mail_item_message_get* .</span><span class="sxs-lookup"><span data-stu-id="5c83d-195">After making a RETR request, and receiving a positive response from the Server, the Client can start downloading the mail message using the *nx_pop3_client_mail_item_message_get* service.</span></span> <span data-ttu-id="5c83d-196">Si noti che il servizio fornisce anche la dimensione dell'elemento di posta elettronica richiesto estratto dalla risposta del server.</span><span class="sxs-lookup"><span data-stu-id="5c83d-196">Note that the service also supplies the size of the requested mail item extracted from the Server reply.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5c83d-197">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5c83d-197">Input Parameters</span></span>

- <span data-ttu-id="5c83d-198">**client_ptr** Puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="5c83d-198">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="5c83d-199">**mail_item** Indicizza in alla maildrop. client</span><span class="sxs-lookup"><span data-stu-id="5c83d-199">**mail_item** Index into Client maildrop</span></span>
- <span data-ttu-id="5c83d-200">**item_size** Puntatore alla dimensione del messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="5c83d-200">**item_size** Pointer to size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="5c83d-201">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5c83d-201">Return Values</span></span>

- <span data-ttu-id="5c83d-202">Elemento di posta **NX_SUCCESS** (0x00) recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="5c83d-202">**NX_SUCCESS** (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="5c83d-203">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) indice elemento di posta elettronica non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-203">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="5c83d-204">Il payload del pacchetto client **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="5c83d-204">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="5c83d-205">Il server **NX_POP3_SERVER_ERROR_STATUS** (0xB4) risponde con lo stato di errore</span><span class="sxs-lookup"><span data-stu-id="5c83d-205">**NX_POP3_SERVER_ERROR_STATUS** (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="5c83d-206">NX_POP3_CLIENT_INVALID_INDEX (0xB8) input dell'indice di posta non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-206">NX_POP3_CLIENT_INVALID_INDEX (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="5c83d-207">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-207">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5c83d-208">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5c83d-208">Allowed From</span></span>

<span data-ttu-id="5c83d-209">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5c83d-209">Application code</span></span>

### <a name="example"></a><span data-ttu-id="5c83d-210">Esempio</span><span class="sxs-lookup"><span data-stu-id="5c83d-210">Example</span></span>

```C
ULONG item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a><span data-ttu-id="5c83d-211">nx_pop3_client_mail_items_get</span><span class="sxs-lookup"><span data-stu-id="5c83d-211">nx_pop3_client_mail_items_get</span></span>

<span data-ttu-id="5c83d-212">Recuperare il numero di elementi di posta elettronica in alla maildrop.</span><span class="sxs-lookup"><span data-stu-id="5c83d-212">Retrieve the number of mail items in maildrop</span></span>

### <a name="prototype"></a><span data-ttu-id="5c83d-213">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5c83d-213">Prototype</span></span>

```C
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
    UINT *number_mail_items,
    ULONG *maildrop_total_size);
```

### <a name="description"></a><span data-ttu-id="5c83d-214">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c83d-214">Description</span></span>

<span data-ttu-id="5c83d-215">Questo servizio esegue una richiesta STAT per recuperare il numero di elementi di posta e le dimensioni totali dei dati del messaggio di posta elettronica dal client alla maildrop..</span><span class="sxs-lookup"><span data-stu-id="5c83d-215">This service makes a STAT request to retrieve the number of mail items and total size of mail message data from the Client maildrop.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5c83d-216">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5c83d-216">Input Parameters</span></span>

- <span data-ttu-id="5c83d-217">**client_ptr** Puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="5c83d-217">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="5c83d-218">**number_mail_item** Numero di messaggi nella alla maildrop. client</span><span class="sxs-lookup"><span data-stu-id="5c83d-218">**number_mail_item** Number of mail in Client maildrop</span></span>
- <span data-ttu-id="5c83d-219">**maildrop_total_size** Puntatore alla dimensione di tutti i messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="5c83d-219">**maildrop_total_size** Pointer to size of all mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="5c83d-220">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5c83d-220">Return Values</span></span>

- <span data-ttu-id="5c83d-221">Elemento di posta **NX_SUCCESS** (0x00) recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="5c83d-221">**NX_SUCCESS** (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="5c83d-222">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) indice elemento di posta elettronica non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-222">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="5c83d-223">Il payload del pacchetto client **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="5c83d-223">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="5c83d-224">Il server **NX_POP3_SERVER_ERROR_STATUS** (0xB4) risponde con lo stato di errore</span><span class="sxs-lookup"><span data-stu-id="5c83d-224">**NX_POP3_SERVER_ERROR_STATUS** (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="5c83d-225">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-225">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5c83d-226">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5c83d-226">Allowed From</span></span>

<span data-ttu-id="5c83d-227">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5c83d-227">Application code</span></span>

### <a name="example"></a><span data-ttu-id="5c83d-228">Esempio</span><span class="sxs-lookup"><span data-stu-id="5c83d-228">Example</span></span>

```C
UINT number_mail_items;

ULONG maildrop_total_size;

/* Retrieve the size and number of items in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_get (&demo_client, 1, &number_mail_items,
    &maildrop_total_size);

/* If the maildrop data was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_message_get"></a><span data-ttu-id="5c83d-229">nx_pop3_client_mail_item_message_get</span><span class="sxs-lookup"><span data-stu-id="5c83d-229">nx_pop3_client_mail_item_message_get</span></span>

<span data-ttu-id="5c83d-230">Recupera il messaggio di elemento di posta specificato</span><span class="sxs-lookup"><span data-stu-id="5c83d-230">Retrieve the specified mail item message</span></span>

### <a name="prototype"></a><span data-ttu-id="5c83d-231">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5c83d-231">Prototype</span></span>

```C
UINT nx_pop3_client_mail_item_message_get(
    NX_POP3_CLIENT *client_ptr,
    NX_PACKET **recv_packet_ptr,
    ULONG *bytes_retrieved,
    UINT *final_packet);
```

### <a name="description"></a><span data-ttu-id="5c83d-232">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c83d-232">Description</span></span>

<span data-ttu-id="5c83d-233">Questo servizio recupera il messaggio dell'elemento di posta, le dimensioni del messaggio di posta elettronica e se è l'ultimo pacchetto del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5c83d-233">This service retrieves the mail item message, size of the mail message, and if it is the last packet in the mail message.</span></span> <span data-ttu-id="5c83d-234">Se final_packet è NX_TRUE il pacchetto a cui punta recv_packet_ptr è il pacchetto finale nel messaggio dell'elemento di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="5c83d-234">If final_packet is NX_TRUE the packet pointed to by recv_packet_ptr is the final packet in the mail item message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5c83d-235">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5c83d-235">Input Parameters</span></span>

- <span data-ttu-id="5c83d-236">**client_ptr** Puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="5c83d-236">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="5c83d-237">**recv_packet_ptr** È stato ricevuto il pacchetto dei dati del messaggio</span><span class="sxs-lookup"><span data-stu-id="5c83d-237">**recv_packet_ptr** Received packet of message data</span></span>
- <span data-ttu-id="5c83d-238">**number_mail_item** Numero di messaggi nella alla maildrop. client</span><span class="sxs-lookup"><span data-stu-id="5c83d-238">**number_mail_item** Number of mail in Client maildrop</span></span>
- <span data-ttu-id="5c83d-239">**maildrop_total_size** Puntatore alla dimensione di tutti i messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="5c83d-239">**maildrop_total_size** Pointer to size of all mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="5c83d-240">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5c83d-240">Return Values</span></span>

- <span data-ttu-id="5c83d-241">Elemento di posta **NX_SUCCESS** (0x00) recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="5c83d-241">**NX_SUCCESS** (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="5c83d-242">Il payload del pacchetto client **NX_POP3_CLIENT_INVALID_STATE** (0xB7) è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="5c83d-242">**NX_POP3_CLIENT_INVALID_STATE** (0xB7) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="5c83d-243">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-243">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5c83d-244">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5c83d-244">Allowed From</span></span>

<span data-ttu-id="5c83d-245">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5c83d-245">Application code</span></span>

### <a name="example"></a><span data-ttu-id="5c83d-246">Esempio</span><span class="sxs-lookup"><span data-stu-id="5c83d-246">Example</span></span>

```C
NX_PACKET *recv_packet_ptr;

ULONG bytes_retrieved;

UINT final_packet;

/* Retrieve the size and number of items in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_message_get (&demo_client, &recv_packet_ptr,
    bytes_retrieved, final_packet);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_size_get"></a><span data-ttu-id="5c83d-247">nx_pop3_client_mail_item_size_get</span><span class="sxs-lookup"><span data-stu-id="5c83d-247">nx_pop3_client_mail_item_size_get</span></span>

<span data-ttu-id="5c83d-248">Recupera la dimensione dell'elemento di posta elettronica specificato</span><span class="sxs-lookup"><span data-stu-id="5c83d-248">Retrieve the size of the specified mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="5c83d-249">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5c83d-249">Prototype</span></span>

```C
UINT nx_pop3_client_mail_item_size_get(
    NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *size);
```

### <a name="description"></a><span data-ttu-id="5c83d-250">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c83d-250">Description</span></span>

<span data-ttu-id="5c83d-251">Questo servizio esegue una richiesta di elenco per ottenere la dimensione dell'elemento di posta elettronica specificato.</span><span class="sxs-lookup"><span data-stu-id="5c83d-251">This service makes a LIST request to obtain the size of the specified mail item.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5c83d-252">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5c83d-252">Input Parameters</span></span>

- <span data-ttu-id="5c83d-253">**client_ptr** Puntatore all'istanza del client</span><span class="sxs-lookup"><span data-stu-id="5c83d-253">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="5c83d-254">**mail_item** Indicizza in alla maildrop. client</span><span class="sxs-lookup"><span data-stu-id="5c83d-254">**mail_item** Index into Client maildrop</span></span>
- <span data-ttu-id="5c83d-255">**dimensioni** Puntatore alla dimensione del messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="5c83d-255">**size** Pointer to size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="5c83d-256">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5c83d-256">Return Values</span></span>

- <span data-ttu-id="5c83d-257">Elemento di posta **NX_SUCCESS** (0x00) recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="5c83d-257">**NX_SUCCESS** (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="5c83d-258">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) indice elemento di posta elettronica non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-258">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="5c83d-259">Il payload del pacchetto client **NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) è troppo piccolo per la richiesta POP3.</span><span class="sxs-lookup"><span data-stu-id="5c83d-259">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="5c83d-260">Il server **NX_POP3_SERVER_ERROR_STATUS** (0xB4) risponde con lo stato di errore</span><span class="sxs-lookup"><span data-stu-id="5c83d-260">**NX_POP3_SERVER_ERROR_STATUS** (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="5c83d-261">NX_POP3_CLIENT_INVALID_INDEX (0xB8) input dell'indice di posta non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-261">NX_POP3_CLIENT_INVALID_INDEX (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="5c83d-262">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="5c83d-262">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5c83d-263">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5c83d-263">Allowed From</span></span>

<span data-ttu-id="5c83d-264">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5c83d-264">Application code</span></span>

### <a name="example"></a><span data-ttu-id="5c83d-265">Esempio</span><span class="sxs-lookup"><span data-stu-id="5c83d-265">Example</span></span>

```C
ULONG size;

UINT mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
