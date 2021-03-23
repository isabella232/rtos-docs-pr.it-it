---
title: Capitolo 3-Descrizione client dei servizi client SMTP
description: Questo capitolo contiene una descrizione di tutti i servizi client SMTP NetX Duo (elencati di seguito) in ordine di utilizzo in una tipica applicazione client SMTP.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f590ba5a4c020b4a0aec6628a89c0e5f0f8579d9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821692"
---
# <a name="chapter-3---client-description-of-smtp-client-services"></a><span data-ttu-id="4a9c4-103">Capitolo 3-Descrizione client dei servizi client SMTP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-103">Chapter 3 - Client description of SMTP Client services</span></span>

<span data-ttu-id="4a9c4-104">Questo capitolo contiene una descrizione di tutti i servizi client SMTP NetX Duo (elencati di seguito) in ordine di utilizzo in una tipica applicazione client SMTP.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-104">This chapter contains a description of all NetX Duo SMTP Client services (listed below) in order of usage in a typical SMTP Client application.</span></span>

> [!NOTE]
> <span data-ttu-id="4a9c4-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **_NX_DISABLE_ERROR_CHECKING_** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **_NX_DISABLE_ERROR_CHECKING_** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nxd_smtp_client_create"></a><span data-ttu-id="4a9c4-106">nxd_smtp_client_create</span><span class="sxs-lookup"><span data-stu-id="4a9c4-106">nxd_smtp_client_create</span></span>

<span data-ttu-id="4a9c4-107">Creare un'istanza del client SMTP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-107">Create an SMTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="4a9c4-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="4a9c4-108">Prototype</span></span>

```C
UINT nxd_smtp_client_create(NX_SMTP_CLIENT *client_ptr,
    NX_IP *ip_ptr, NX_PACKET_POOL
    *client_packet_pool_ptr,
    CHAR *username, CHAR *password,
    CHAR *from_address,
    CHAR *client_domain,
    UINT authentication_type, NXD_ADDRESS *server_address,
    UINT port);
```

### <a name="description"></a><span data-ttu-id="4a9c4-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a9c4-109">Description</span></span>

<span data-ttu-id="4a9c4-110">Questo servizio crea un'istanza del client SMTP nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-110">This service creates an SMTP Client instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="4a9c4-111">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="4a9c4-111">Input Parameters</span></span>

- <span data-ttu-id="4a9c4-112">**client_ptr** Puntatore al blocco di controllo client SMTP;</span><span class="sxs-lookup"><span data-stu-id="4a9c4-112">**client_ptr** Pointer to SMTP Client control block;</span></span>
- <span data-ttu-id="4a9c4-113">**ip_ptr** Puntatore all'istanza IP;</span><span class="sxs-lookup"><span data-stu-id="4a9c4-113">**ip_ptr** Pointer to IP instance;</span></span>
- <span data-ttu-id="4a9c4-114">**packet_pool_ptr** Puntatore al pool di pacchetti client;</span><span class="sxs-lookup"><span data-stu-id="4a9c4-114">**packet_pool_ptr** Pointer to Client packet pool;</span></span>
- <span data-ttu-id="4a9c4-115">**nome utente** Nome utente \* \* con terminazione NULL per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="4a9c4-115">**username** NULL-terminated\*\* Username for authentication</span></span>
- <span data-ttu-id="4a9c4-116">**password** di Password con terminazione NULL per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="4a9c4-116">**password** NULL-terminated password for authentication</span></span>
- <span data-ttu-id="4a9c4-117">**from_address** Indirizzo del mittente con terminazione NULL</span><span class="sxs-lookup"><span data-stu-id="4a9c4-117">**from_address** NULL-terminated sender’s address</span></span>
- <span data-ttu-id="4a9c4-118">**client_domain** Nome di dominio con terminazione NULL</span><span class="sxs-lookup"><span data-stu-id="4a9c4-118">**client_domain** NULL-terminated domain name</span></span>
- <span data-ttu-id="4a9c4-119">**authentication_type** Tipo di autenticazione client.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-119">**authentication_type** Client authentication type.</span></span> <span data-ttu-id="4a9c4-120">I tipi supportati sono:</span><span class="sxs-lookup"><span data-stu-id="4a9c4-120">Supported types are:</span></span>
  - <span data-ttu-id="4a9c4-121">NX_SMTP_CLIENT_AUTH_LOGIN</span><span class="sxs-lookup"><span data-stu-id="4a9c4-121">NX_SMTP_CLIENT_AUTH_LOGIN</span></span>
  - <span data-ttu-id="4a9c4-122">NX_SMTP_CLIENT_AUTH_PLAIN</span><span class="sxs-lookup"><span data-stu-id="4a9c4-122">NX_SMTP_CLIENT_AUTH_PLAIN</span></span>
  - <span data-ttu-id="4a9c4-123">NX_SMTP_CLIENT_AUTH_NONE</span><span class="sxs-lookup"><span data-stu-id="4a9c4-123">NX_SMTP_CLIENT_AUTH_NONE</span></span>
- <span data-ttu-id="4a9c4-124">**server_address** Puntatore all'indirizzo IP del server SMTP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-124">**server_address** Pointer to SMTP Server IP address</span></span>
- <span data-ttu-id="4a9c4-125">**SERVER_PORT** Porta TCP del server SMTP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-125">**server_port** SMTP Server TCP port</span></span>

### <a name="return-values"></a><span data-ttu-id="4a9c4-126">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="4a9c4-126">Return Values</span></span>

- <span data-ttu-id="4a9c4-127">Creazione del client SMTP **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-127">**NX_SUCCESS** (0x00) SMTP Client successfully created.</span></span> <span data-ttu-id="4a9c4-128">Stato di creazione socket TCP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-128">TCP socket creation status</span></span>
- <span data-ttu-id="4a9c4-129">NX_SMTP_INVALID_PARAM (0xA5) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="4a9c4-129">NX_SMTP_INVALID_PARAM (0xA5) Invalid non pointer input</span></span>
- <span data-ttu-id="4a9c4-130">Tipo di indirizzo IP NX_IP_ADDRESS_ERROR (0x21) non valido</span><span class="sxs-lookup"><span data-stu-id="4a9c4-130">NX_IP_ADDRESS_ERROR (0x21) Invalid IP address type</span></span>
- <span data-ttu-id="4a9c4-131">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="4a9c4-131">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="4a9c4-132">Consentito da</span><span class="sxs-lookup"><span data-stu-id="4a9c4-132">Allowed From</span></span>

<span data-ttu-id="4a9c4-133">codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4a9c4-133">Application Code</span></span>

### <a name="example"></a><span data-ttu-id="4a9c4-134">Esempio</span><span class="sxs-lookup"><span data-stu-id="4a9c4-134">Example</span></span>

```C
/* Create the SMTP Client instance. */
NX_PACKET_POOL client_packet_pool;
NX_IP client_ip;
NX_SMTP_CLIENT demo_client;

#define USERNAME “myusername”
#define PASSWORD “mypassword”
#define FROM_ADDRESS “<myname@mycompany.com>”
#define LOCAL_DOMAIN “mycompany.com”
#define SERVER_PORT 25

/* Define client authentication type as LOGIN. 
    If not specified or unknown the SMTP Client will set it to PLAIN. */
#define CLIENT_AUTHENTICATION_TYPE NX_SMTP_CLIENT_AUTH_LOGIN

NXD_ADDRESS server_ip_address;

#ifdef USE_IPV6
    /* Set up the Server IPv6 address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    server_ip_address.nxd_ip_address.v6[1] = 0xf101;
    server_ip_address.nxd_ip_address.v6[2] = 0;
    server_ip_address.nxd_ip_address.v6[3] = 0x106;
#else
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_IP_ADDRESS;
#endif

status = nxd_smtp_client_create(&demo_client, &client_ip, &client_packet_pool,
    USERNAME, PASSWORD, FROM_ADDRESS,
    LOCAL_DOMAIN, CLIENT_AUTHENTICATION_TYPE,
    &server_ip_address, SERVER_PORT);

/* If an SMTP Client instance was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_smtp_client_delete"></a><span data-ttu-id="4a9c4-135">nx_smtp_client_delete</span><span class="sxs-lookup"><span data-stu-id="4a9c4-135">nx_smtp_client_delete</span></span>

<span data-ttu-id="4a9c4-136">Eliminare un'istanza del client SMTP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-136">Delete an SMTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="4a9c4-137">Prototipo</span><span class="sxs-lookup"><span data-stu-id="4a9c4-137">Prototype</span></span>

```C
UINT nx_smtp_client_delete(NX_SMTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="4a9c4-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a9c4-138">Description</span></span>

<span data-ttu-id="4a9c4-139">Questo servizio Elimina un'istanza del client SMTP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-139">This service deletes a previously created SMTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="4a9c4-140">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="4a9c4-140">Input Parameters</span></span>

- <span data-ttu-id="4a9c4-141">**client_ptr** Puntatore all'istanza del client SMTP.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-141">**client_ptr** Pointer to SMTP Client instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="4a9c4-142">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="4a9c4-142">Return Values</span></span>

- <span data-ttu-id="4a9c4-143">Il client **NX_SUCCESS** (0x00) è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="4a9c4-143">**NX_SUCCESS** (0x00) Client successfully deleted</span></span>
- <span data-ttu-id="4a9c4-144">Parametro puntatore di input NX_PTR_ERROR (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="4a9c4-144">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="4a9c4-145">Consentito da</span><span class="sxs-lookup"><span data-stu-id="4a9c4-145">Allowed From</span></span>

<span data-ttu-id="4a9c4-146">Thread</span><span class="sxs-lookup"><span data-stu-id="4a9c4-146">Threads</span></span>

### <a name="example"></a><span data-ttu-id="4a9c4-147">Esempio</span><span class="sxs-lookup"><span data-stu-id="4a9c4-147">Example</span></span>

```C
/* Delete the SMTP Client instance “my_client.” */

NX_SMTP_CLIENT demo_client;

status = nx_smtp_client_delete(&demo_client);

/* If an SMTP Client instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_smtp_mail_send"></a><span data-ttu-id="4a9c4-148">nx_smtp_mail_send</span><span class="sxs-lookup"><span data-stu-id="4a9c4-148">nx_smtp_mail_send</span></span>

<span data-ttu-id="4a9c4-149">Creare e inviare un elemento di posta SMTP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-149">Create and send an SMTP mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="4a9c4-150">Prototipo</span><span class="sxs-lookup"><span data-stu-id="4a9c4-150">Prototype</span></span>

```C
UINT nx_smtp_mail_send(NX_SMTP_CLIENT *client_ptr,
    CHAR *recipient_address,
    UINT priority, CHAR *subject,
    CHAR *mail_body,
    UINT mail_body_length);
```

### <a name="description"></a><span data-ttu-id="4a9c4-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a9c4-151">Description</span></span>

<span data-ttu-id="4a9c4-152">Questo servizio crea e invia un elemento di posta SMTP.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-152">This service creates and sends an SMTP mail item.</span></span> <span data-ttu-id="4a9c4-153">Il client SMTP stabilisce una connessione TCP con il server SMTP e invia una serie di comandi SMTP.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-153">The SMTP Client establishes a TCP connection with the SMTP Server and sends a series of SMTP commands.</span></span> <span data-ttu-id="4a9c4-154">Se non viene rilevato alcun errore, il messaggio di posta elettronica verrà trasmesso al server.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-154">If no errors are encountered, it will transmit the mail message to the Server.</span></span> <span data-ttu-id="4a9c4-155">Indipendentemente dal fatto che il messaggio venga inviato correttamente, la connessione TCP verrà terminata e verrà restituito uno stato che indica il risultato della trasmissione della posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-155">Regardless if the mail is sent successfully it will terminate the TCP connection and return a status indicating outcome of the mail transmission.</span></span> <span data-ttu-id="4a9c4-156">L'applicazione può chiamare questo servizio per tutti i messaggi di posta elettronica necessari per l'invio senza limiti.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-156">The application may call this service for as many mail messages as it needs to send without limit.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="4a9c4-157">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="4a9c4-157">Input Parameters</span></span>

- <span data-ttu-id="4a9c4-158">**client_ptr** Puntatore al client SMTP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-158">**client_ptr** Pointer to SMTP Client</span></span>
- <span data-ttu-id="4a9c4-159">**recipient_address** Indirizzo destinatario con terminazione NULL.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-159">**recipient_address** NULL-terminated recipient address.</span></span>
- <span data-ttu-id="4a9c4-160">**oggetto** Testo della riga dell'oggetto con terminazione NULL;.</span><span class="sxs-lookup"><span data-stu-id="4a9c4-160">**subject** NULL-terminated subject line text;.</span></span>
- <span data-ttu-id="4a9c4-161">**priorità** di Livello di priorità a cui viene recapitato il messaggio</span><span class="sxs-lookup"><span data-stu-id="4a9c4-161">**priority** Priority level at which mail is delivered</span></span>
- <span data-ttu-id="4a9c4-162">**mail_body** Puntatore al messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="4a9c4-162">**mail_body** Pointer to mail message</span></span>
- <span data-ttu-id="4a9c4-163">**mail_body_length** Dimensioni del messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="4a9c4-163">**mail_body_length** Size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="4a9c4-164">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="4a9c4-164">Return Values</span></span>

- <span data-ttu-id="4a9c4-165">Messaggio **NX_SUCCESS** (0x00) inviato correttamente</span><span class="sxs-lookup"><span data-stu-id="4a9c4-165">**NX_SUCCESS** (0x00) Mail successfully sent</span></span>
- <span data-ttu-id="4a9c4-166">Istanza del client SMTP **NX_SMTP_CLIENT_NOT_INITIALIZED** (0xB2) non inizializzata per il risultato dello stato della sessione SMTP della sessione SMTP</span><span class="sxs-lookup"><span data-stu-id="4a9c4-166">**NX_SMTP_CLIENT_NOT_INITIALIZED** (0xB2) SMTP Client instance not initialized for SMTP session status Outcome of SMTP session</span></span>
- <span data-ttu-id="4a9c4-167">Parametro puntatore non valido NX_PTR_ERROR (0x07)</span><span class="sxs-lookup"><span data-stu-id="4a9c4-167">NX_PTR_ERROR (0x07) Invalid pointer parameter</span></span>
- <span data-ttu-id="4a9c4-168">NX_SMTP_INVALID_PARAM (0xA5) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="4a9c4-168">NX_SMTP_INVALID_PARAM (0xA5) Invalid non pointer input</span></span>
- <span data-ttu-id="4a9c4-169">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="4a9c4-169">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="4a9c4-170">Consentito da</span><span class="sxs-lookup"><span data-stu-id="4a9c4-170">Allowed From</span></span>

<span data-ttu-id="4a9c4-171">Thread</span><span class="sxs-lookup"><span data-stu-id="4a9c4-171">Threads</span></span>

### <a name="example"></a><span data-ttu-id="4a9c4-172">Esempio</span><span class="sxs-lookup"><span data-stu-id="4a9c4-172">Example</span></span>

```C
/* Create and send a Client mail item. */

#define RECIPIENT_ADDRESS “<your@yourcompany.com>”
#define SUBJECT “NetX Duo SMTP Client Demo”
#define MAIL_BODY "NetX Duo SMTP client is an SMTP client ” \
    “implementation for embedded devices \r\n” \
    "to send email to SMTP servers.\r\n"

status = nx_smtp_mail_send(&demo_client, RECIPIENT_ADDRESS,
    NX_SMTP_MAIL_PRIORITY_NORMAL,
    SUBJECT_LINE, MAIL_BODY,
    sizeof(MAIL_BODY) - 1);

/* Return status being NX_SUCCESS indicates the mail has been
    successfully sent. */
```
