---
title: Capitolo 3-Descrizione dei servizi di Azure RTO NetX Point-to-Point Protocol (PPP)
description: Questo capitolo contiene una descrizione di tutti i servizi di Azure RTO NetX PPP (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f24d7366d27a8223b069a54ef7b93f6b3e38bf3a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822556"
---
# <a name="chapter-3---description-of-azure-rtos-netx-point-to-point-protocol-ppp-services"></a><span data-ttu-id="47ab4-103">Capitolo 3-Descrizione dei servizi di Azure RTO NetX Point-to-Point Protocol (PPP)</span><span class="sxs-lookup"><span data-stu-id="47ab4-103">Chapter 3 - Description of Azure RTOS NetX Point-to-Point Protocol (PPP) services</span></span>

<span data-ttu-id="47ab4-104">Questo capitolo contiene una descrizione di tutti i servizi di Azure RTO NetX PPP (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="47ab4-104">This chapter contains a description of all Azure RTOS NetX PPP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="47ab4-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="47ab4-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="47ab4-106">**nx_ppp_byte_receive**: *ricezione di un byte da ISR seriale*</span><span class="sxs-lookup"><span data-stu-id="47ab4-106">**nx_ppp_byte_receive**: *Receive a byte from serial ISR*</span></span>
- <span data-ttu-id="47ab4-107">**nx_ppp_chap_challenge**: *genera una richiesta CHAP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-107">**nx_ppp_chap_challenge**: *Generate a CHAP challenge*</span></span>
- <span data-ttu-id="47ab4-108">**nx_ppp_chap_enable**: *abilitare l'autenticazione CHAP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-108">**nx_ppp_chap_enable**: *Enable CHAP authentication*</span></span>
- <span data-ttu-id="47ab4-109">**nx_ppp_create**: *creare un'istanza di PPP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-109">**nx_ppp_create**: *Create a PPP instance*</span></span>
- <span data-ttu-id="47ab4-110">**nx_ppp_delete**: *eliminare un'istanza di PPP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-110">**nx_ppp_delete**: *Delete a PPP instance*</span></span>
- <span data-ttu-id="47ab4-111">**nx_ppp_dns_address_get**: *ottenere l'indirizzo IP DNS*</span><span class="sxs-lookup"><span data-stu-id="47ab4-111">**nx_ppp_dns_address_get**: *Get DNS IP address*</span></span>
- <span data-ttu-id="47ab4-112">**nx_ppp_dns_address_set**:*impostare l'indirizzo IP del server DNS*</span><span class="sxs-lookup"><span data-stu-id="47ab4-112">**nx_ppp_dns_address_set**:*Set DNS Server IP address*</span></span>
- <span data-ttu-id="47ab4-113">**nx_ppp_secondary_dns_address_get**: *ottenere l'indirizzo IP del server DNS secondario*</span><span class="sxs-lookup"><span data-stu-id="47ab4-113">**nx_ppp_secondary_dns_address_get**: *Get Secondary DNS Server IP address*</span></span>
- <span data-ttu-id="47ab4-114">**nx_ppp_secondary_dns_address_set**: *impostare l'indirizzo IP del server Secondary_DNS*</span><span class="sxs-lookup"><span data-stu-id="47ab4-114">**nx_ppp_secondary_dns_address_set**: *Set Secondary_DNS Server IP address*</span></span>
- <span data-ttu-id="47ab4-115">**nx_ppp_interface_index_get**: *ottenere l'indice dell'interfaccia IP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-115">**nx_ppp_interface_index_get**: *Get IP interface index*</span></span>
- <span data-ttu-id="47ab4-116">**nx_ppp_ip_address_assign**: *assegnare gli indirizzi IP per protocollo IPCP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-116">**nx_ppp_ip_address_assign**: *Assign IP addresses for IPCP*</span></span>
- <span data-ttu-id="47ab4-117">**nx_ppp_link_down_notify**: *notifica applicazione al collegamento in basso*</span><span class="sxs-lookup"><span data-stu-id="47ab4-117">**nx_ppp_link_down_notify**: *Notify application on link down*</span></span>
- <span data-ttu-id="47ab4-118">**nx_ppp_link_up_notify**: *notifica applicazione al collegamento*</span><span class="sxs-lookup"><span data-stu-id="47ab4-118">**nx_ppp_link_up_notify**: *Notify application on link up*</span></span>
- <span data-ttu-id="47ab4-119">**nx_ppp_nak_authentication_notify**: *notifica l'applicazione se viene ricevuta l'autenticazione NAK*</span><span class="sxs-lookup"><span data-stu-id="47ab4-119">**nx_ppp_nak_authentication_notify**: *Notify application if authentication NAK is received*</span></span>
- <span data-ttu-id="47ab4-120">**nx_ppp_pap_enable**: *Abilita autenticazione PAP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-120">**nx_ppp_pap_enable**: *Enable PAP authentication*</span></span>
- <span data-ttu-id="47ab4-121">**nx_ppp_ping_request**: *inviare una richiesta echo LCP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-121">**nx_ppp_ping_request**: *Send an LCP echo request*</span></span>
- <span data-ttu-id="47ab4-122">**nx_ppp_raw_string_send**: *Invia stringa non PPP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-122">**nx_ppp_raw_string_send**: *Send non PPP string*</span></span>
- <span data-ttu-id="47ab4-123">**nx_ppp_restart**: *riavvio dell'elaborazione PPP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-123">**nx_ppp_restart**: *Restart PPP processing*</span></span>
- <span data-ttu-id="47ab4-124">**nx_ppp_start**: *avviare l'elaborazione PPP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-124">**nx_ppp_start**: *Start PPP processing*</span></span>
- <span data-ttu-id="47ab4-125">**nx_ppp_status_get**: *ottenere lo stato PPP corrente*</span><span class="sxs-lookup"><span data-stu-id="47ab4-125">**nx_ppp_status_get**: *Get current PPP status*</span></span>
- <span data-ttu-id="47ab4-126">**nx_ppp_stop**: *arrestare l'elaborazione PPP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-126">**nx_ppp_stop**: *Stop PPP processing*</span></span>
- <span data-ttu-id="47ab4-127">**nx_ppp_packet_receive**: *ricevere il pacchetto PPP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-127">**nx_ppp_packet_receive**: *Receive PPP packet*</span></span>
- <span data-ttu-id="47ab4-128">**nx_ppp_packet_send_set**: *impostare la funzione di invio pacchetti PPP*</span><span class="sxs-lookup"><span data-stu-id="47ab4-128">**nx_ppp_packet_send_set**: *Set PPP packet send function*</span></span>

## <a name="nx_ppp_byte_receive"></a><span data-ttu-id="47ab4-129">nx_ppp_byte_receive</span><span class="sxs-lookup"><span data-stu-id="47ab4-129">nx_ppp_byte_receive</span></span>

<span data-ttu-id="47ab4-130">Ricevi un byte da ISR seriale</span><span class="sxs-lookup"><span data-stu-id="47ab4-130">Receive a byte from serial ISR</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-131">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-131">Prototype</span></span>

```c
UINT nx_ppp_byte_receive(NX_PPP *ppp_ptr, UCHAR byte);
```

### <a name="description"></a><span data-ttu-id="47ab4-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-132">Description</span></span>

<span data-ttu-id="47ab4-133">Questo servizio viene in genere chiamato dalla routine ISR (Serial driver interrupt Service) dell'applicazione per trasferire un byte ricevuto a PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-133">This service is typically called from the application’s serial driver Interrupt Service Routine (ISR) to transfer a received byte to PPP.</span></span> <span data-ttu-id="47ab4-134">Quando viene chiamato, questa routine inserisce il byte ricevuto in un buffer di byte circolare e invia una notifica al thread PPP appropriato per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-134">When called, this routine places the received byte into a circular byte buffer and notifies the appropriate PPP thread for processing.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-135">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-135">Input Parameters</span></span>

- <span data-ttu-id="47ab4-136">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-136">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-137">**byte**: byte ricevuti dal dispositivo seriale</span><span class="sxs-lookup"><span data-stu-id="47ab4-137">**byte**: Byte received from serial device</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-138">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-138">Return Values</span></span>

- <span data-ttu-id="47ab4-139">**NX_SUCCESS**: (0x00) ricezione byte PPP riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-139">**NX_SUCCESS**: (0x00) Successful PPP byte receive.</span></span>
- <span data-ttu-id="47ab4-140">**NX_PPP_BUFFER_FULL**: (0xB1) il buffer seriale PPP è già pieno.</span><span class="sxs-lookup"><span data-stu-id="47ab4-140">**NX_PPP_BUFFER_FULL**: (0xB1) PPP serial buffer is already full.</span></span>
- <span data-ttu-id="47ab4-141">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-141">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-142">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-142">Allowed From</span></span>

<span data-ttu-id="47ab4-143">Thread, ISRs</span><span class="sxs-lookup"><span data-stu-id="47ab4-143">Threads, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-144">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-144">Example</span></span>

```c
/* Notify “my_ppp” of a received byte. */
status =  nx_ppp_byte_receive(&my_ppp, new_byte);

/* If status is NX_SUCCESS the received byte was successfully
   buffered. */
```

## <a name="nx_ppp_chap_challenge"></a><span data-ttu-id="47ab4-145">nx_ppp_chap_challenge</span><span class="sxs-lookup"><span data-stu-id="47ab4-145">nx_ppp_chap_challenge</span></span>

<span data-ttu-id="47ab4-146">Genera una richiesta CHAP</span><span class="sxs-lookup"><span data-stu-id="47ab4-146">Generate a CHAP challenge</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-147">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-147">Prototype</span></span>

```c
UINT nx_ppp_chap_challenge(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-148">Description</span></span>

<span data-ttu-id="47ab4-149">Questo servizio avvia una richiesta CHAP dopo che la connessione PPP è già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-149">This service initiates a CHAP challenge after the PPP connection is already up and running.</span></span> <span data-ttu-id="47ab4-150">In questo modo l'applicazione è in grado di verificare l'autenticità della connessione periodicamente.</span><span class="sxs-lookup"><span data-stu-id="47ab4-150">This gives the application the ability to verify the authenticity of the connection on a periodic basis.</span></span> <span data-ttu-id="47ab4-151">Se la verifica ha esito negativo, il collegamento PPP viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="47ab4-151">If the challenge is unsuccessful, the PPP link is closed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-152">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-152">Input Parameters</span></span>

- <span data-ttu-id="47ab4-153">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-153">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-154">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-154">Return Values</span></span>

- <span data-ttu-id="47ab4-155">**NX_SUCCESS**: (0x00) avviata verifica PPP riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-155">**NX_SUCCESS**: (0x00) Successful PPP challenge initiated.</span></span>
- <span data-ttu-id="47ab4-156">**NX_PPP_FAILURE**: (0XB0) la richiesta PPP non è valida. il protocollo CHAP è stato abilitato solo per la risposta.</span><span class="sxs-lookup"><span data-stu-id="47ab4-156">**NX_PPP_FAILURE**: (0xB0) Invalid PPP challenge, CHAP was enabled only for response.</span></span>
- <span data-ttu-id="47ab4-157">**NX_NOT_IMPLEMENTED**: (0x80) la logica CHAP è stata disabilitata tramite NX_PPP_DISABLE_CHAP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-157">**NX_NOT_IMPLEMENTED**: (0x80) CHAP logic was disabled via NX_PPP_DISABLE_CHAP.</span></span>
- <span data-ttu-id="47ab4-158">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-158">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="47ab4-159">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-159">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-160">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-160">Allowed From</span></span>

<span data-ttu-id="47ab4-161">Thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-161">Threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-162">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-162">Example</span></span>

```c
/* Initiate a PPP challenge for instance “my_ppp”. */
status =  nx_ppp_chap_challenge(&my_ppp);

/* If status is NX_SUCCESS a CHAP challenge “my_ppp” was successfully 
initiated. */
```

## <a name="nx_ppp_chap_enable"></a><span data-ttu-id="47ab4-163">nx_ppp_chap_enable</span><span class="sxs-lookup"><span data-stu-id="47ab4-163">nx_ppp_chap_enable</span></span>

<span data-ttu-id="47ab4-164">Abilitare l'autenticazione CHAP</span><span class="sxs-lookup"><span data-stu-id="47ab4-164">Enable CHAP authentication</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-165">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-165">Prototype</span></span>

```c
UINT nx_ppp_chap_enable(NX_PPP *ppp_ptr, 
                        UINT (*get_challenge_values)(CHAR *rand_value,CHAR *id,CHAR *name),
                        UINT (*get_responder_values)(CHAR *system,CHAR *name,CHAR *secret),
                        UINT (*get_verification_values)(CHAR *system,CHAR *name,CHAR *secret)); 
```

### <a name="description"></a><span data-ttu-id="47ab4-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-166">Description</span></span>

<span data-ttu-id="47ab4-167">Questo servizio Abilita il protocollo CHAP (Challenge-Handshake Authentication Protocol) per l'istanza di PPP specificata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-167">This service enables the Challenge-Handshake Authentication Protocol (CHAP) for the specified PPP instance.</span></span>

<span data-ttu-id="47ab4-168">Se vengono specificati i puntatori a funzione "\***get_challenge_values**_" e "_ \* _get_verification_values_\* \*", CHAP è richiesto da questa istanza di PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-168">If the “\***get_challenge_values**_” and “_\*_get_verification_values_\*\*” function pointers are specified, CHAP is required by this PPP instance.</span></span> <span data-ttu-id="47ab4-169">In caso contrario, l'autenticazione CHAP risponde solo alle richieste di verifica del peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-169">Otherwise, CHAP only responds to the peer’s challenge requests.</span></span>

<span data-ttu-id="47ab4-170">Sono presenti diversi elementi di dati a cui viene fatto riferimento nelle funzioni di callback obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="47ab4-170">There are several data items referenced below in the required callback functions.</span></span> <span data-ttu-id="47ab4-171">Si prevede che il *segreto*, il *nome* e il *sistema* degli elementi di dati siano stringhe con terminazione NULL con una dimensione massima di NX_PPP_NAME_SIZE-1.</span><span class="sxs-lookup"><span data-stu-id="47ab4-171">The data items *secret*, *name*, and *system* are expected to be NULL-terminated strings with a maximum size of NX_PPP_NAME_SIZE-1.</span></span> <span data-ttu-id="47ab4-172">È previsto che l'elemento dati *rand_value* sia una stringa con terminazione null con una dimensione massima di NX_PPP_VALUE_SIZE-1.</span><span class="sxs-lookup"><span data-stu-id="47ab4-172">The data item *rand_value* is expected to be a NULL-terminated string with a maximum size of NX_PPP_VALUE_SIZE-1.</span></span> <span data-ttu-id="47ab4-173">L' *ID* dell'elemento dati è un tipo di carattere senza segno semplice.</span><span class="sxs-lookup"><span data-stu-id="47ab4-173">The data item *id* is a simple unsigned character type.</span></span>

>[!NOTE]
> <span data-ttu-id="47ab4-174">Questa funzione deve essere chiamata dopo *nx_ppp_create* ma prima di nx_ip_create o *nx_ip_interface_attach*.</span><span class="sxs-lookup"><span data-stu-id="47ab4-174">This function must be called after *nx_ppp_create* but before nx_ip_create or *nx_ip_interface_attach*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-175">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-175">Input Parameters</span></span>

- <span data-ttu-id="47ab4-176">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-176">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-177">**get_challenge_values**: puntatore alla funzione dell'applicazione per recuperare i valori utilizzati per la richiesta di verifica.</span><span class="sxs-lookup"><span data-stu-id="47ab4-177">**get_challenge_values**: Pointer to application function to retrieve values used for the challenge.</span></span> <span data-ttu-id="47ab4-178">Si noti che i valori *rand_value*, *ID* e *Secret* devono essere copiati nelle destinazioni specificate.</span><span class="sxs-lookup"><span data-stu-id="47ab4-178">Note that the *rand_value*, *id*, and *secret* values must be copied into the supplied destinations.</span></span>
- <span data-ttu-id="47ab4-179">**get_responder_values**: puntatore alla funzione dell'applicazione che recupera i valori utilizzati per rispondere a una richiesta di verifica.</span><span class="sxs-lookup"><span data-stu-id="47ab4-179">**get_responder_values**: Pointer to application function that retrieves values used to respond to a challenge.</span></span> <span data-ttu-id="47ab4-180">Si noti che i valori di *sistema*, *nome* e *segreto* devono essere copiati nelle destinazioni specificate.</span><span class="sxs-lookup"><span data-stu-id="47ab4-180">Note that the *system*, *name*, and *secret* values must be copied into the supplied destinations.</span></span>
- <span data-ttu-id="47ab4-181">**get_verification_values**: puntatore alla funzione dell'applicazione che recupera i valori utilizzati per verificare la risposta alla richiesta di verifica.</span><span class="sxs-lookup"><span data-stu-id="47ab4-181">**get_verification_values**: Pointer to application function that retrieves values used to verify the challenge response.</span></span> <span data-ttu-id="47ab4-182">Si noti che i valori di *sistema*,*nome* e *segreto* devono essere copiati nelle destinazioni specificate.</span><span class="sxs-lookup"><span data-stu-id="47ab4-182">Note that the *system*,*name*, and *secret* values must be copied into the supplied destinations.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-183">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-183">Return Values</span></span>

- <span data-ttu-id="47ab4-184">**NX_SUCCESS**: (0x00) abilitata autenticazione CHAP PPP riuscita</span><span class="sxs-lookup"><span data-stu-id="47ab4-184">**NX_SUCCESS**: (0x00) Successful PPP CHAP enable</span></span>
- <span data-ttu-id="47ab4-185">**NX_NOT_IMPLEMENTED**: (0x80) la logica CHAP è stata disabilitata tramite NX_PPP_DISABLE_CHAP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-185">**NX_NOT_IMPLEMENTED**: (0x80) CHAP logic was disabled via NX_PPP_DISABLE_CHAP.</span></span>
- <span data-ttu-id="47ab4-186">NX_PTR_ERROR: (0x07) puntatore PPP o puntatore alla funzione di callback non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-186">NX_PTR_ERROR: (0x07) Invalid PPP pointer or callback function pointer.</span></span> <span data-ttu-id="47ab4-187">Si noti che se si specifica *get_challenge_values* , è necessario specificare anche la funzione *get_verification_values* .</span><span class="sxs-lookup"><span data-stu-id="47ab4-187">Note that if *get_challenge_values* is specified, then the *get_verification_values* function must also be supplied.</span></span>
- <span data-ttu-id="47ab4-188">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-188">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-189">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-189">Allowed From</span></span>

<span data-ttu-id="47ab4-190">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-190">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-191">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-191">Example</span></span>

```c
CHAR    name_string[] = "username";
CHAR    rand_value_string[] = "123456";
CHAR    system_string[] = "system";
CHAR    secret_string[] = "secret";

/* Enable CHAP in both directions (CHAP challenger and CHAP responder) for 
“my_ppp”. */
status =  nx_ppp_chap_enable(&my_ppp,   get_challenge_values, 
                              get_responder_values,
                              get_verification_values);


/* If status is NX_SUCCESS, “my_ppp” has CHAP enabled. */
/* Define the CHAP enable routines.  */
UINT  get_challenge_values(CHAR *rand_value, CHAR *id, CHAR *name)
{
   UINT    i;
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;
   
   *id =  '1';  /* One byte  */
   for (i = 0; i< (NX_PPP_VALUE_SIZE-1); i++)
   {
      rand_value[i] =  rand_value_string[i];
   }
   rand_value[i] =  0;
   
   return(NX_SUCCESS);  
}


UINT  get_responder_values(CHAR *system, CHAR *name, CHAR *secret)
{
   UINT    i;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;

   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      system[i] =  system_string[i];
   }
   system[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      secret[i] =  secret_string[i];
   }
   secret[i] =  0;
   
   return(NX_SUCCESS);  
}

UINT  get_verification_values(CHAR *system, CHAR *name, CHAR *secret)
{
   UINT    i;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      system[i] =  system_string[i];
   }
   system[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      secret[i] =  secret_string[i];
   }
   secret[i] =  0;
   
   return(NX_SUCCESS);  
}

```
## <a name="nx_ppp_create"></a><span data-ttu-id="47ab4-192">nx_ppp_create</span><span class="sxs-lookup"><span data-stu-id="47ab4-192">nx_ppp_create</span></span>

<span data-ttu-id="47ab4-193">Creare un'istanza di PPP</span><span class="sxs-lookup"><span data-stu-id="47ab4-193">Create a PPP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-194">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-194">Prototype</span></span>

```c
UINT  nx_ppp_create(NX_PPP *ppp_ptr, CHAR *name, NX_IP *ip_ptr, 
                    VOID *stack_memory_ptr, ULONG stack_size, 
                    UINT thread_priority, NX_PACKET_POOL *pool_ptr,
                    void (*ppp_invalid_packet_handler)(NX_PACKET *packet_ptr),
                    void (*ppp_byte_send)(UCHAR byte));
```

### <a name="description"></a><span data-ttu-id="47ab4-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-195">Description</span></span>

<span data-ttu-id="47ab4-196">Questo servizio crea un'istanza di PPP per l'istanza IP di NetX specificata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-196">This service creates a PPP instance for the specified NetX IP instance.</span></span>

>[!NOTE]
> <span data-ttu-id="47ab4-197">È in genere consigliabile creare il thread IP NetX con una priorità più alta rispetto alla priorità del thread PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-197">It is generally a good idea to create the NetX IP thread at a higher priority than the PPP thread priority.</span></span> <span data-ttu-id="47ab4-198">Per ulteriori informazioni su come specificare la priorità del thread IP, fare riferimento al servizio *nx_ip_create* .</span><span class="sxs-lookup"><span data-stu-id="47ab4-198">Please refer to the *nx_ip_create* service for more information on specifying the IP thread priority.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-199">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-199">Input Parameters</span></span>

- <span data-ttu-id="47ab4-200">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-200">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-201">**nome**: nome dell'istanza di PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-201">**name**: Name of this PPP instance.</span></span>
- <span data-ttu-id="47ab4-202">**ip_ptr**: puntatore al blocco di controllo per l'istanza IP non ancora creata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-202">**ip_ptr**: Pointer to control block for not-yet-created IP instance.</span></span>
- <span data-ttu-id="47ab4-203">**stack_memory_ptr**: puntatore all'inizio dell'area dello stack del thread PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-203">**stack_memory_ptr**: Pointer to start of PPP thread’s stack area.</span></span>
- <span data-ttu-id="47ab4-204">**stack_size**: dimensioni in byte nello stack del thread.</span><span class="sxs-lookup"><span data-stu-id="47ab4-204">**stack_size**: Size in bytes in the thread’s stack.</span></span>
- <span data-ttu-id="47ab4-205">**pool_ptr**: puntatore al pool di pacchetti predefinito.</span><span class="sxs-lookup"><span data-stu-id="47ab4-205">**pool_ptr**: Pointer to default packet pool.</span></span>
- <span data-ttu-id="47ab4-206">**THREAD_PRIORITY**: priorità dei thread PPP interni (1-31).</span><span class="sxs-lookup"><span data-stu-id="47ab4-206">**thread_priority**: Priority of internal PPP threads (1-31).</span></span>
- <span data-ttu-id="47ab4-207">**ppp_invalid_packet_handler**: puntatore della funzione al gestore dell'applicazione per tutti i pacchetti non PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-207">**ppp_invalid_packet_handler**: Function pointer to application’s handler for all non-PPP packets.</span></span> <span data-ttu-id="47ab4-208">Il PPP NetX in genere chiama questa routine durante l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-208">The NetX PPP typically calls this routine during initialization.</span></span> <span data-ttu-id="47ab4-209">Questo è il punto in cui l'applicazione può rispondere ai comandi del modem o, nel caso di Windows XP, l'applicazione NetX PPP può avviare PPP rispondendo con "SERVER CLIENT" al "CLIENT" iniziale inviato da Windows XP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-209">This is where the application can respond to modem commands or in the case of Windows XP, the NetX PPP application can initiate PPP by responding with“ CLIENT SERVER” to the initial “CLIENT” sent by Windows XP.</span></span>
- <span data-ttu-id="47ab4-210">**ppp_byte_send**: puntatore a funzione per la routine di output di byte seriale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-210">**ppp_byte_send**: Function pointer to application’s serial byte output routine.</span></span>


### <a name="return-values"></a><span data-ttu-id="47ab4-211">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-211">Return Values</span></span>

- <span data-ttu-id="47ab4-212">**NX_SUCCESS**: (0x00) creazione PPP riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-212">**NX_SUCCESS**: (0x00) Successful PPP create.</span></span>
- <span data-ttu-id="47ab4-213">NX_PTR_ERROR: (0x07) puntatore a funzione di output PPP, IP o byte non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-213">NX_PTR_ERROR: (0x07) Invalid PPP, IP, or byte output function pointer.</span></span>
- <span data-ttu-id="47ab4-214">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-214">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-215">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-215">Allowed From</span></span>

<span data-ttu-id="47ab4-216">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-216">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-217">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-217">Example</span></span>

```c
/* Create “my_ppp” for IP instance “my_ip”. */
status =  nx_ppp_create(&my_ppp, “my PPP”, &my_ip, stack_start, 1024, 2, 
                        &my_pool, my_invalid_packet_handler, my_out_byte);

/* If status is NX_SUCCESS the PPP instance was successfully
   created. */
```

## <a name="nx_ppp_delete"></a><span data-ttu-id="47ab4-218">nx_ppp_delete</span><span class="sxs-lookup"><span data-stu-id="47ab4-218">nx_ppp_delete</span></span>

<span data-ttu-id="47ab4-219">Eliminare un'istanza di PPP</span><span class="sxs-lookup"><span data-stu-id="47ab4-219">Delete a PPP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-220">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-220">Prototype</span></span>

```c
UINT nx_ppp_delete(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-221">Description</span></span>

<span data-ttu-id="47ab4-222">Questo servizio Elimina l'istanza di PPP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="47ab4-222">This service deletes the previously created PPP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-223">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-223">Input Parameters</span></span>

- <span data-ttu-id="47ab4-224">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-224">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-225">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-225">Return Values</span></span>

- <span data-ttu-id="47ab4-226">**NX_SUCCESS**: (0x00) eliminazione PPP riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-226">**NX_SUCCESS**: (0x00) Successful PPP deletion.</span></span>
- <span data-ttu-id="47ab4-227">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-227">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="47ab4-228">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-228">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-229">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-229">Allowed From</span></span>

<span data-ttu-id="47ab4-230">Thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-230">Threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-231">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-231">Example</span></span>

```c
/* Delete PPP instance “my_ppp”. */
status =  nx_ppp_delete(&my_ppp);

/* If status is NX_SUCCESS the “my_ppp” was successfully deleted. */
```

## <a name="nx_ppp_dns_address_get"></a><span data-ttu-id="47ab4-232">nx_ppp_dns_address_get</span><span class="sxs-lookup"><span data-stu-id="47ab4-232">nx_ppp_dns_address_get</span></span>

<span data-ttu-id="47ab4-233">Ottenere l'indirizzo IP DNS</span><span class="sxs-lookup"><span data-stu-id="47ab4-233">Get DNS IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-234">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-234">Prototype</span></span>

```c
UINT nx_ppp_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-235">Description</span></span>

<span data-ttu-id="47ab4-236">Questo servizio recupera l'indirizzo IP DNS fornito dal peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-236">This service retrieves the DNS IP address supplied by the peer.</span></span> <span data-ttu-id="47ab4-237">Se non è stato fornito alcun indirizzo IP dal peer, viene restituito un indirizzo IP 0.</span><span class="sxs-lookup"><span data-stu-id="47ab4-237">If no IP address was supplied by the peer, an IP address of 0 is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-238">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-238">Input Parameters</span></span>

- <span data-ttu-id="47ab4-239">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-239">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-240">**dns_address_ptr**: destinazione per l'indirizzo IP DNS</span><span class="sxs-lookup"><span data-stu-id="47ab4-240">**dns_address_ptr**: Destination for DNS IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-241">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-241">Return Values</span></span>

- <span data-ttu-id="47ab4-242">**NX_SUCCESS**: (0x00) indirizzo PPP riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="47ab4-242">**NX_SUCCESS**: (0x00) Successful PPP address get.</span></span>
- <span data-ttu-id="47ab4-243">**NX_PPP_NOT_ESTABLISHED**: (0XB5) PPP non ha completato la negoziazione con peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-243">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP has not completed negotiation with peer.</span></span>
- <span data-ttu-id="47ab4-244">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-244">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-245">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-245">Allowed From</span></span>

<span data-ttu-id="47ab4-246">Inizializzazione, thread, timer, ISRs</span><span class="sxs-lookup"><span data-stu-id="47ab4-246">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-247">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-247">Example</span></span>

```c

ULONG  my_dns_address;

/* Get IP Server address supplied by peer. */
status =  nx_ppp_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the DNS IP address – 
   if the peer supplied one. */
```

## <a name="nx_ppp_secondary_dns_address_get"></a><span data-ttu-id="47ab4-248">nx_ppp_secondary_dns_address_get</span><span class="sxs-lookup"><span data-stu-id="47ab4-248">nx_ppp_secondary_dns_address_get</span></span>

<span data-ttu-id="47ab4-249">Ottenere l'indirizzo IP del server DNS secondario</span><span class="sxs-lookup"><span data-stu-id="47ab4-249">Get Secondary DNS Server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-250">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-250">Prototype</span></span>

```c
UINT nx_ppp_secondary_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-251">Description</span></span>

<span data-ttu-id="47ab4-252">Questo servizio recupera l'indirizzo IP DNS secondario fornito dal peer nell'handshake protocollo IPCP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-252">This service retrieves the secondary DNS IP address supplied by the peer in the IPCP handshake.</span></span> <span data-ttu-id="47ab4-253">Se non è stato fornito alcun indirizzo IP dal peer, viene restituito un indirizzo IP 0.</span><span class="sxs-lookup"><span data-stu-id="47ab4-253">If no IP address was supplied by the peer, an IP address of 0 is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-254">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-254">Input Parameters</span></span>

- <span data-ttu-id="47ab4-255">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-255">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-256">**dns_address_ptr**: destinazione per l'indirizzo del server DNS secondario</span><span class="sxs-lookup"><span data-stu-id="47ab4-256">**dns_address_ptr**: Destination for Secondary DNS server address</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-257">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-257">Return Values</span></span>

- <span data-ttu-id="47ab4-258">**NX_SUCCESS**: (0x00) indirizzo DNS riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="47ab4-258">**NX_SUCCESS**: (0x00) Successful DNS address get.</span></span>
- <span data-ttu-id="47ab4-259">**NX_PPP_NOT_ESTABLISHED**: (0XB5) PPP non ha completato la negoziazione con peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-259">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP has not completed negotiation with peer.</span></span>
- <span data-ttu-id="47ab4-260">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-260">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-261">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-261">Allowed From</span></span>

<span data-ttu-id="47ab4-262">Inizializzazione, thread, timer, ISRs</span><span class="sxs-lookup"><span data-stu-id="47ab4-262">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-263">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-263">Example</span></span>

```c
ULONG  my_dns_address;

/* Get secondary DNS Server address supplied by peer. */
status =  nx_ppp_secondary_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the secondary DNS Server address – if the peer supplied one. */
```

## <a name="nx_ppp_dns_address_set"></a><span data-ttu-id="47ab4-264">nx_ppp_dns_address_set</span><span class="sxs-lookup"><span data-stu-id="47ab4-264">nx_ppp_dns_address_set</span></span>

<span data-ttu-id="47ab4-265">Impostare l'indirizzo IP del server DNS primario</span><span class="sxs-lookup"><span data-stu-id="47ab4-265">Set primary DNS Server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-266">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-266">Prototype</span></span>

```c
UINT nx_ppp_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a><span data-ttu-id="47ab4-267">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-267">Description</span></span>

<span data-ttu-id="47ab4-268">Questo servizio imposta l'indirizzo IP del server DNS.</span><span class="sxs-lookup"><span data-stu-id="47ab4-268">This service sets the DNS Server IP address.</span></span> <span data-ttu-id="47ab4-269">Se il peer invia una richiesta di opzione del server DNS nello stato protocollo IPCP, questo host fornirà le informazioni.</span><span class="sxs-lookup"><span data-stu-id="47ab4-269">If the peer sends a DNS Server option request in the IPCP state, this host will provide the information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-270">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-270">Input Parameters</span></span>

- <span data-ttu-id="47ab4-271">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-271">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-272">**dns_address**: indirizzo del server DNS</span><span class="sxs-lookup"><span data-stu-id="47ab4-272">**dns_address**: DNS server address</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-273">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-273">Return Values</span></span>

- <span data-ttu-id="47ab4-274">**NX_SUCCESS**: (0x00) il set di indirizzi DNS è riuscito.</span><span class="sxs-lookup"><span data-stu-id="47ab4-274">**NX_SUCCESS**: (0x00) Successful DNS address set.</span></span>
- <span data-ttu-id="47ab4-275">**NX_PPP_NOT_ESTABLISHED**: (0XB5) PPP non ha completato la negoziazione con peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-275">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP has not completed negotiation with peer.</span></span>
- <span data-ttu-id="47ab4-276">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-276">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-277">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-277">Allowed From</span></span>

<span data-ttu-id="47ab4-278">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-278">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-279">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-279">Example</span></span>

```c

ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the DNS Server address provided if the peer requests one. */

```

## <a name="nx_ppp_secondary_dns_address_set"></a><span data-ttu-id="47ab4-280">nx_ppp_secondary_dns_address_set</span><span class="sxs-lookup"><span data-stu-id="47ab4-280">nx_ppp_secondary_dns_address_set</span></span>

<span data-ttu-id="47ab4-281">Impostare l'indirizzo IP del server DNS secondario</span><span class="sxs-lookup"><span data-stu-id="47ab4-281">Set secondary DNS Server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-282">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-282">Prototype</span></span>

```c
UINT nx_ppp_secondary_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a><span data-ttu-id="47ab4-283">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-283">Description</span></span>

<span data-ttu-id="47ab4-284">Questo servizio imposta l'indirizzo IP del server DNS secondario.</span><span class="sxs-lookup"><span data-stu-id="47ab4-284">This service sets the secondary DNS Server IP address.</span></span> <span data-ttu-id="47ab4-285">Se il peer invia una richiesta di opzione del server DNS secondario nello stato protocollo IPCP, questo host fornirà le informazioni.</span><span class="sxs-lookup"><span data-stu-id="47ab4-285">If the peer sends a secondary DNS Server option request in the IPCP state, this host will provide the information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-286">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-286">Input Parameters</span></span>

- <span data-ttu-id="47ab4-287">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-287">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-288">**dns_address**: indirizzo del server DNS secondario</span><span class="sxs-lookup"><span data-stu-id="47ab4-288">**dns_address**: Secondary DNS server address</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-289">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-289">Return Values</span></span>

- <span data-ttu-id="47ab4-290">**NX_SUCCESS**: (0x00) il set di indirizzi DNS è riuscito.</span><span class="sxs-lookup"><span data-stu-id="47ab4-290">**NX_SUCCESS**: (0x00) Successful DNS address set.</span></span> 
- <span data-ttu-id="47ab4-291">**NX_PPP_NOT_ESTABLISHED**: (0XB5) PPP non ha completato la negoziazione con peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-291">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP has not completed negotiation with peer.</span></span>
- <span data-ttu-id="47ab4-292">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-292">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-293">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-293">Allowed From</span></span>

<span data-ttu-id="47ab4-294">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-294">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-295">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-295">Example</span></span>

```c
ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_secondary_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the secondary DNS Server address provided if the peer requests one. */

```
## <a name="nx_ppp_interface_index_get"></a><span data-ttu-id="47ab4-296">nx_ppp_interface_index_get</span><span class="sxs-lookup"><span data-stu-id="47ab4-296">nx_ppp_interface_index_get</span></span>

<span data-ttu-id="47ab4-297">Ottenere l'indice dell'interfaccia IP</span><span class="sxs-lookup"><span data-stu-id="47ab4-297">Get IP interface index</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-298">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-298">Prototype</span></span>

```c
UINT nx_ppp_interface_index_get(NX_PPP *ppp_ptr, UINT *index_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-299">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-299">Description</span></span>

<span data-ttu-id="47ab4-300">Questo servizio recupera l'indice dell'interfaccia IP associato a questa istanza di PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-300">This service retrieves the IP interface index associated with this PPP instance.</span></span> <span data-ttu-id="47ab4-301">Questa operazione è utile solo quando l'istanza di PPP non è l'interfaccia principale di un'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-301">This is only useful when the PPP instance is not the primary interface of an IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-302">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-302">Input Parameters</span></span>

- <span data-ttu-id="47ab4-303">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-303">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-304">**index_ptr**: destinazione per l'indice dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="47ab4-304">**index_ptr**: Destination for interface index</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-305">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-305">Return Values</span></span>

- <span data-ttu-id="47ab4-306">**NX_SUCCESS**: (0x00) ottenere l'indice PPP riuscito.</span><span class="sxs-lookup"><span data-stu-id="47ab4-306">**NX_SUCCESS**: (0x00) Successful PPP index get.</span></span>
- <span data-ttu-id="47ab4-307">**NX_IN_PROGRESS**: (0x37) PPP non ha completato l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-307">**NX_IN_PROGRESS**: (0x37) PPP has not completed initialization.</span></span>
- <span data-ttu-id="47ab4-308">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-308">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-309">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-309">Allowed From</span></span>

<span data-ttu-id="47ab4-310">Inizializzazione, thread, timer, ISRs</span><span class="sxs-lookup"><span data-stu-id="47ab4-310">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-311">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-311">Example</span></span>

```c
ULONG  my_index;

/* Get the interface index for this PPP instance. */
status =  nx_ppp_interface_index_get(&my_ppp, &my_index);

/* If status is NX_SUCCESS the “my_index” contains the IP interface index for
   this PPP instance. */

```
## <a name="nx_ppp_ip_address_assign"></a><span data-ttu-id="47ab4-312">nx_ppp_ip_address_assign</span><span class="sxs-lookup"><span data-stu-id="47ab4-312">nx_ppp_ip_address_assign</span></span>

<span data-ttu-id="47ab4-313">Assegnare indirizzi IP per protocollo IPCP</span><span class="sxs-lookup"><span data-stu-id="47ab4-313">Assign IP addresses for IPCP</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-314">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-314">Prototype</span></span>

```c
UINT nx_ppp_ip_address_assign(NX_PPP *ppp_ptr, ULONG local_ip_address, 
            ULONG peer_ip_address);
```

### <a name="description"></a><span data-ttu-id="47ab4-315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-315">Description</span></span>

<span data-ttu-id="47ab4-316">Questo servizio configura gli indirizzi IP locali e peer per l'utilizzo in Internet Protocol Control Protocol (protocollo IPCP).</span><span class="sxs-lookup"><span data-stu-id="47ab4-316">This service sets up the local and peer IP addresses for use in the Internet Protocol Control Protocol (IPCP).</span></span> <span data-ttu-id="47ab4-317">L'applicazione PPP dovrebbe richiamare questo servizio su un'istanza di PPP con indirizzi IP validi per se stesso e per l'altro peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-317">The PPP application should invoke this service on a PPP instance with valid IP addresses for itself and the other peer.</span></span>  <span data-ttu-id="47ab4-318">Se non è stato registrato alcun indirizzo valido con un'istanza di PPP, deve basarsi sul peer PPP per definirne l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-318">If no valid addresses are registered with a PPP instance, it must rely on the PPP peer to define its IP address.</span></span>


### <a name="input-parameters"></a><span data-ttu-id="47ab4-319">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-319">Input Parameters</span></span>

- <span data-ttu-id="47ab4-320">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-320">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-321">**local_ip_address**: indirizzo IP locale.</span><span class="sxs-lookup"><span data-stu-id="47ab4-321">**local_ip_address**: Local IP address.</span></span>
- <span data-ttu-id="47ab4-322">**peer_ip_address**: indirizzo IP del peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-322">**peer_ip_address**: Peer’s IP address.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-323">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-323">Return Values</span></span>

- <span data-ttu-id="47ab4-324">**NX_SUCCESS**: (0x00) assegnazione di indirizzi PPP riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-324">**NX_SUCCESS**: (0x00) Successful PPP address assignment.</span></span>
- <span data-ttu-id="47ab4-325">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-325">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="47ab4-326">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-326">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-327">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-327">Allowed From</span></span>

<span data-ttu-id="47ab4-328">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-328">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-329">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-329">Example</span></span>

```c
/* Set IP addresses for “my_ppp”. */
status =  nx_ppp_ip_address_assign(&my_ppp, IP_ADDRESS(256,2,2,187), 
IP_ADDRESS(256,2,2,188));


/* If status is NX_SUCCESS the “my_ppp” has the IP addresses. */
```

## <a name="nx_ppp_link_down_notify"></a><span data-ttu-id="47ab4-330">nx_ppp_link_down_notify</span><span class="sxs-lookup"><span data-stu-id="47ab4-330">nx_ppp_link_down_notify</span></span>

<span data-ttu-id="47ab4-331">Invia notifica all'applicazione al collegamento</span><span class="sxs-lookup"><span data-stu-id="47ab4-331">Notify application on link down</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-332">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-332">Prototype</span></span>

```c
UINT nx_ppp_link_down_notify(NX_PPP *ppp_ptr, 
                             VOID (*link_down_callback)(NX_PPP *ppp_ptr));
```

### <a name="description"></a><span data-ttu-id="47ab4-333">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-333">Description</span></span>

<span data-ttu-id="47ab4-334">Questo servizio registra il callback di notifica per il collegamento dell'applicazione con l'istanza di PPP specificata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-334">This service registers the application’s link down notification callback with the specified PPP instance.</span></span> <span data-ttu-id="47ab4-335">Se diverso da NULL, la funzione di callback del collegamento di un'applicazione viene chiamata ogni volta che il collegamento diventa inattivo.</span><span class="sxs-lookup"><span data-stu-id="47ab4-335">If non-NULL, the application’s link down callback function is called whenever the link goes down.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-336">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-336">Input Parameters</span></span>

- <span data-ttu-id="47ab4-337">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-337">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-338">**link_down_callback**: puntatore alla funzione di notifica collegamento all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-338">**link_down_callback**: Application’s link down notification function pointer.</span></span> <span data-ttu-id="47ab4-339">Se è NULL, la notifica del collegamento è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-339">If NULL, link down notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-340">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-340">Return Values</span></span>

- <span data-ttu-id="47ab4-341">**NX_SUCCESS**: (0x00) il collegamento alla registrazione di callback delle notifiche è riuscito.</span><span class="sxs-lookup"><span data-stu-id="47ab4-341">**NX_SUCCESS**: (0x00) Successful link down notification callback registration.</span></span>
- <span data-ttu-id="47ab4-342">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-342">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-343">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-343">Allowed From</span></span>

<span data-ttu-id="47ab4-344">Inizializzazione, thread, timer, ISRs</span><span class="sxs-lookup"><span data-stu-id="47ab4-344">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-345">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-345">Example</span></span>

```c
/* Register “my_link_down_callback” to be called whenever the PPP
   link goes down. */
status =  nx_ppp_link_down_notify(&my_ppp, my_link_down_callback);


/* If status is NX_SUCCESS the function “my_link_down_callback” has been
   registered with this PPP instance. */

VOID my_link_down_callback(NX_PPP *ppp_ptr)
{

/* On link down, simply restart PPP.  */
    nx_ppp_restart(ppp_ptr);
} 
```
## <a name="nx_ppp_link_up_notify"></a><span data-ttu-id="47ab4-346">nx_ppp_link_up_notify</span><span class="sxs-lookup"><span data-stu-id="47ab4-346">nx_ppp_link_up_notify</span></span>

<span data-ttu-id="47ab4-347">Invia notifica all'applicazione al collegamento</span><span class="sxs-lookup"><span data-stu-id="47ab4-347">Notify application on link up</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-348">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-348">Prototype</span></span>

```c
UINT nx_ppp_link_up_notify(NX_PPP *ppp_ptr, 
                           VOID (*link_up_callback)(NX_PPP *ppp_ptr));
```
### <a name="description"></a><span data-ttu-id="47ab4-349">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-349">Description</span></span>

<span data-ttu-id="47ab4-350">Questo servizio registra il callback delle notifiche di collegamento dell'applicazione con l'istanza di PPP specificata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-350">This service registers the application’s link up notification callback with the specified PPP instance.</span></span> <span data-ttu-id="47ab4-351">Se diverso da NULL, la funzione di callback del collegamento dell'applicazione viene chiamata ogni volta che il collegamento viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="47ab4-351">If non-NULL, the application’s link up callback function is called whenever the link comes up.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-352">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-352">Input Parameters</span></span>

- <span data-ttu-id="47ab4-353">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-353">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-354">**link_up_callback**: puntatore alla funzione di notifica collegamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-354">**link_up_callback**: Application’s link up notification function pointer.</span></span> <span data-ttu-id="47ab4-355">Se è NULL, la notifica di collegamento è disabilitata. \* \*</span><span class="sxs-lookup"><span data-stu-id="47ab4-355">If NULL, link up notification is disabled.\*\*</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-356">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-356">Return Values</span></span>

- <span data-ttu-id="47ab4-357">**NX_SUCCESS**: (0x00) collegamento riuscito registrazione di callback di notifica.</span><span class="sxs-lookup"><span data-stu-id="47ab4-357">**NX_SUCCESS**: (0x00) Successful link up notification callback registration.</span></span>
- <span data-ttu-id="47ab4-358">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-358">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-359">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-359">Allowed From</span></span>

<span data-ttu-id="47ab4-360">Inizializzazione, thread, timer, ISRs</span><span class="sxs-lookup"><span data-stu-id="47ab4-360">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-361">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-361">Example</span></span>

```c
/* Register “my_link_up_callback” to be called whenever the PPP
   link comes up. */
status =  nx_ppp_link_up_notify(&my_ppp, my_link_up_callback);


/* If status is NX_SUCCESS the function “my_link_up_callback” has been
   registered with this PPP instance. */

VOID my_link_up_callback(NX_PPP *ppp_ptr)
{
    /* On link up, the application my want to start sending/receiving
       UPD/TCP data.  */
}
```

## <a name="nx_ppp_nak_authentication_notify"></a><span data-ttu-id="47ab4-362">nx_ppp_nak_authentication_notify</span><span class="sxs-lookup"><span data-stu-id="47ab4-362">nx_ppp_nak_authentication_notify</span></span>

<span data-ttu-id="47ab4-363">Invia notifica all'applicazione se è stata ricevuta l'autenticazione NAK</span><span class="sxs-lookup"><span data-stu-id="47ab4-363">Notify application if authentication NAK received</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-364">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-364">Prototype</span></span>

```c
UINT    nx_ppp_nak_authentication_notify(NX_PPP *ppp_ptr, 
                                         void (*nak_authentication_notify)(void));
```

### <a name="description"></a><span data-ttu-id="47ab4-365">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-365">Description</span></span>

<span data-ttu-id="47ab4-366">Questo servizio registra il callback di notifica di autenticazione NAK dell'applicazione con l'istanza di PPP specificata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-366">This service registers the application’s authentication nak notification callback with the specified PPP instance.</span></span> <span data-ttu-id="47ab4-367">Se diverso da NULL, questa funzione di callback viene chiamata ogni volta che l'istanza di PPP riceve un NAK durante authentiaction.</span><span class="sxs-lookup"><span data-stu-id="47ab4-367">If non-NULL, this callback function is called whenever the PPP instance receives a NAK during authentiaction.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-368">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-368">Input Parameters</span></span>

- <span data-ttu-id="47ab4-369">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-369">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-370">**nak_authentication_notify**: puntatore a funzione chiamato quando l'istanza di PPP riceve un NAK di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-370">**nak_authentication_notify**: Pointer to function called when the PPP instance receives an authentication NAK.</span></span> <span data-ttu-id="47ab4-371">Se è NULL, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-371">If NULL, the notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-372">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-372">Return Values</span></span>

- <span data-ttu-id="47ab4-373">**NX_SUCCESS**: (0x00) la registrazione del callback di notifica è riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-373">**NX_SUCCESS**: (0x00) Successful notification callback registration.</span></span>
- <span data-ttu-id="47ab4-374">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-374">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-375">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-375">Allowed From</span></span>

<span data-ttu-id="47ab4-376">Inizializzazione, thread, timer, ISRs</span><span class="sxs-lookup"><span data-stu-id="47ab4-376">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-377">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-377">Example</span></span>

```c
/* Register “my_nak_auth_callback” to be called whenever the PPP
   receives a NAK during authentication. */
status =  nx_ppp_nak_authentication_notify(&my_ppp, my_nak_auth_callback);

/* If status is NX_SUCCESS the function “my_nak_auth_callback” has been
   registered with this PPP instance. */

VOID my_nak_auth_callback(NX_PPP *ppp_ptr)
{
   /* Handle the situation of receiving an authentication NAK */
}

```

## <a name="nx_ppp_pap_enable"></a><span data-ttu-id="47ab4-378">nx_ppp_pap_enable</span><span class="sxs-lookup"><span data-stu-id="47ab4-378">nx_ppp_pap_enable</span></span>

<span data-ttu-id="47ab4-379">Abilita autenticazione PAP</span><span class="sxs-lookup"><span data-stu-id="47ab4-379">Enable PAP Authentication</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-380">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-380">Prototype</span></span>

```c

UINT  nx_ppp_pap_enable(NX_PPP *ppp_ptr, 
                        UINT (*generate_login)(CHAR *name, CHAR *password),
                        UINT (*verify_login)(CHAR *name, CHAR *password));
```

### <a name="description"></a><span data-ttu-id="47ab4-381">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-381">Description</span></span>

<span data-ttu-id="47ab4-382">Questo servizio Abilita il Password Authentication Protocol (PAP) per l'istanza di PPP specificata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-382">This service enables the Password Authentication Protocol (PAP) for the specified PPP instance.</span></span> <span data-ttu-id="47ab4-383">Se viene specificato il puntatore a funzione "***verify_login***", il Pap è richiesto da questa istanza di PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-383">If the “***verify_login***” function pointer is specified, PAP is required by this PPP instance.</span></span> <span data-ttu-id="47ab4-384">In caso contrario, PAP risponde solo ai requisiti PAP del peer, come specificato durante la negoziazione LCP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-384">Otherwise, PAP only responds to the peer’s PAP requirements as specified during LCP negotiation.</span></span>

<span data-ttu-id="47ab4-385">Sono presenti diversi elementi di dati a cui viene fatto riferimento nelle funzioni di callback obbligatorie.</span><span class="sxs-lookup"><span data-stu-id="47ab4-385">There are several data items referenced below in the required callback functions.</span></span> <span data-ttu-id="47ab4-386">È previsto che il *nome* dell'elemento dati sia una stringa con terminazione null con una dimensione massima di NX_PPP_NAME_SIZE-1.</span><span class="sxs-lookup"><span data-stu-id="47ab4-386">The data item *name* is expected to be NULL-terminated string with a maximum size of NX_PPP_NAME_SIZE-1.</span></span> <span data-ttu-id="47ab4-387">Anche la *password* dell'elemento dati deve essere una stringa con terminazione null con una dimensione massima pari a NX_PPP_PASSWORD_SIZE-1.</span><span class="sxs-lookup"><span data-stu-id="47ab4-387">The data item *password* is also expected to be a NULL-terminated string with a maximum size of NX_PPP_PASSWORD_SIZE-1.</span></span>

>[!NOTE]
> <span data-ttu-id="47ab4-388">Questa funzione deve essere chiamata dopo *nx_ppp_create* ma prima di *nx_ip_create* o *nx_ip_interface_attach*.</span><span class="sxs-lookup"><span data-stu-id="47ab4-388">This function must be called after *nx_ppp_create* but before *nx_ip_create* or *nx_ip_interface_attach*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-389">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-389">Input Parameters</span></span>

- <span data-ttu-id="47ab4-390">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-390">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-391">**generate_login**: puntatore alla funzione dell'applicazione che produce un *nome* e una *password* per l'autenticazione da parte del peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-391">**generate_login**: Pointer to application function that produces a *name* and *password* for authentication by the peer.</span></span> <span data-ttu-id="47ab4-392">Si noti che i valori relativi al *nome* e alla *password* devono essere copiati nelle destinazioni specificate.</span><span class="sxs-lookup"><span data-stu-id="47ab4-392">Note that the *name* and *password* values must be copied into the supplied destinations.</span></span>
- <span data-ttu-id="47ab4-393">**verify_login**: puntatore alla funzione dell'applicazione che verifica il *nome* e la *password* forniti dal peer.</span><span class="sxs-lookup"><span data-stu-id="47ab4-393">**verify_login**: Pointer to application function that verifies the *name* and *password* supplied by the peer.</span></span> <span data-ttu-id="47ab4-394">Questa routine deve confrontare il *nome* e la *password* specificati.</span><span class="sxs-lookup"><span data-stu-id="47ab4-394">This routine must compare the supplied *name* and *password*.</span></span> <span data-ttu-id="47ab4-395">Se questa routine restituisce NX_SUCCESS, il nome e la password sono corretti e il PPP può procedere al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="47ab4-395">If this routine returns NX_SUCCESS, the name and password are correct and PPP can proceed to the next step.</span></span> <span data-ttu-id="47ab4-396">In caso contrario, questa routine restituisce NX_PPP_ERROR e PPP è semplicemente in attesa di un altro nome e password.</span><span class="sxs-lookup"><span data-stu-id="47ab4-396">Otherwise, this routine returns NX_PPP_ERROR and PPP simply waits for another name and password.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-397">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-397">Return Values</span></span>

- <span data-ttu-id="47ab4-398">**NX_SUCCESS**: (0x00) l'abilitazione del Pap PPP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-398">**NX_SUCCESS**: (0x00) Successful PPP PAP enable.</span></span>
- <span data-ttu-id="47ab4-399">**NX_NOT_IMPLEMENTED**: (0x80) la logica PAP è stata disabilitata tramite NX_PPP_DISABLE_PAP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-399">**NX_NOT_IMPLEMENTED**: (0x80) PAP logic was disabled via NX_PPP_DISABLE_PAP.</span></span>
- <span data-ttu-id="47ab4-400">NX_PTR_ERROR: (0x07) puntatore PPP o puntatore a funzione dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-400">NX_PTR_ERROR: (0x07) Invalid PPP pointer or application function pointer.</span></span>
- <span data-ttu-id="47ab4-401">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-401">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-402">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-402">Allowed From</span></span>

<span data-ttu-id="47ab4-403">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-403">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-404">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-404">Example</span></span>

```c
CHAR    name_string[] = "username";
CHAR    password_string[] =  "password";

/* Enable PAP for PPP instance “my_ppp”. */
status =  nx_ppp_pap_enable(&my_ppp, my_generate_login, my_verify_login);

/* If status is NX_SUCCESS the “my_ppp” now has PAP enabled. */

/* Define callback routines for PAP enable.  */

UINT  generate_login(CHAR *name, CHAR *password)
{

UINT    i;

for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
name[i] = name_string[i];
name[i] =  0;

for (i = 0; i< (NX_PPP_PASSWORD_SIZE-1); i++)
password[i] = password_string[i];
password_string[i] =  0;

return(NX_SUCCESS);  
}

UINT  verify_login(CHAR *name, CHAR *password)
{

/* Assume name and password are correct. Normally, 
a comparison would be made here!  */
printf("Name: %s, Password: %s\n", name, password);

return(NX_SUCCESS);  
}
```

## <a name="nx_ppp_ping_request"></a><span data-ttu-id="47ab4-405">nx_ppp_ping_request</span><span class="sxs-lookup"><span data-stu-id="47ab4-405">nx_ppp_ping_request</span></span>

<span data-ttu-id="47ab4-406">Invia una richiesta ping LCP</span><span class="sxs-lookup"><span data-stu-id="47ab4-406">Send an LCP ping request</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-407">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-407">Prototype</span></span>

```c
UINT  nx_ppp_ping_request(NX_PPP *ppp_ptr, CHAR *data, 
                          UINT data_size, ULONG wait_opion);
```

### <a name="description"></a><span data-ttu-id="47ab4-408">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-408">Description</span></span>

<span data-ttu-id="47ab4-409">Questo servizio invia una richiesta ping LCP e imposta un flag che il dispositivo PPP è in attesa di una risposta echo.</span><span class="sxs-lookup"><span data-stu-id="47ab4-409">This service sends an LCP ping request and sets a flag that the PPP device is waiting for an echo response.</span></span> <span data-ttu-id="47ab4-410">Il servizio viene restituito non appena viene inviata la richiesta.</span><span class="sxs-lookup"><span data-stu-id="47ab4-410">The service returns as soon as the request is sent.</span></span> <span data-ttu-id="47ab4-411">Non attende una risposta.</span><span class="sxs-lookup"><span data-stu-id="47ab4-411">It does not wait for a response.</span></span> 

<span data-ttu-id="47ab4-412">Quando viene ricevuta una risposta echo corrispondente, l'attività thread PPP cancellerà il flag.</span><span class="sxs-lookup"><span data-stu-id="47ab4-412">When a matching echo response is received, the PPP thread task will clear the flag.</span></span> <span data-ttu-id="47ab4-413">Il dispositivo PPP deve avere completato la parte LCP della negoziazione PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-413">The PPP device must have completed the LCP part of the PPP negotiation.</span></span>

<span data-ttu-id="47ab4-414">Questo servizio è utile per i set di impostazioni PPP in cui il polling dell'hardware per lo stato dei collegamenti potrebbe non essere immediatamente possibile.</span><span class="sxs-lookup"><span data-stu-id="47ab4-414">This service is useful for PPP set ups where polling the hardware for link status may not be readily possible.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-415">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-415">Input Parameters</span></span>

- <span data-ttu-id="47ab4-416">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-416">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-417">**Data**: puntatore ai dati da inviare nella richiesta echo.</span><span class="sxs-lookup"><span data-stu-id="47ab4-417">**data**: Pointer to data to send in echo request.</span></span>
- <span data-ttu-id="47ab4-418">**DATA_SIZE**: dimensioni dei dati da inviare WAIT_OPTION tempo di attesa per l'invio del messaggio echo LCP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-418">**data_size**: Size of data to send wait_option Time to wait to send the LCP echo message.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-419">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-419">Return Values</span></span>

- <span data-ttu-id="47ab4-420">**NX_SUCCESS**: (0x00) la richiesta echo è stata inviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="47ab4-420">**NX_SUCCESS**: (0x00) Successful sent echo request.</span></span>
- <span data-ttu-id="47ab4-421">**NX_PPP_NOT_ESTABLISHED**: (0xB5) connessione PPP non stabilita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-421">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP connection not established.</span></span>
- <span data-ttu-id="47ab4-422">NX_PTR_ERROR: (0x07) puntatore PPP o puntatore a funzione dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-422">NX_PTR_ERROR: (0x07) Invalid PPP pointer or application function pointer.</span></span>
- <span data-ttu-id="47ab4-423">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="47ab4-423">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-424">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-424">Allowed From</span></span>

<span data-ttu-id="47ab4-425">Thread applicazione</span><span class="sxs-lookup"><span data-stu-id="47ab4-425">Application threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-426">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-426">Example</span></span>

```c

CHAR    buffer[] = "username";
UINT    buffer_length =  strlen("username ");

/* Send an LCP ping request”. */
status =  nx_ppp_ping_request(&my_ppp, &buffer[0], buffer_length, 200);

/* If status is NX_SUCCESS the LCP echo request was successfully sent. Now wait to 
   receive a response. */

while(my_ppp.nx_ppp_lcp_echo_reply_id > 0)
{
    tx_thread_sleep(100);
}

/* Got a valid reply! */
```

## <a name="nx_ppp_raw_string_send"></a><span data-ttu-id="47ab4-427">nx_ppp_raw_string_send</span><span class="sxs-lookup"><span data-stu-id="47ab4-427">nx_ppp_raw_string_send</span></span>

<span data-ttu-id="47ab4-428">Invia una stringa ASCII non elaborata</span><span class="sxs-lookup"><span data-stu-id="47ab4-428">Send a raw ASCII string</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-429">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-429">Prototype</span></span>

```c
UINT  nx_ppp_raw_sting_send(NX_PPP *ppp_ptr, CHAR *string_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-430">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-430">Description</span></span>

<span data-ttu-id="47ab4-431">Questo servizio invia una stringa ASCII non PPP direttamente dall'interfaccia PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-431">This service sends a non-PPP ASCII string directly out the PPP interface.</span></span> <span data-ttu-id="47ab4-432">Viene in genere usato dopo che PPP riceve un pacchetto non PPP che contiene le informazioni di controllo del modem.</span><span class="sxs-lookup"><span data-stu-id="47ab4-432">It is typically used after PPP receives a non-PPP packet that contains modem control information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-433">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-433">Input Parameters</span></span>

- <span data-ttu-id="47ab4-434">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-434">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-435">**string_ptr**: puntatore alla stringa da inviare.</span><span class="sxs-lookup"><span data-stu-id="47ab4-435">**string_ptr**: Pointer to string to send.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-436">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-436">Return Values</span></span>

- <span data-ttu-id="47ab4-437">**NX_SUCCESS**: (0x00) l'invio di una stringa non ELABORAta PPP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-437">**NX_SUCCESS**: (0x00) Successful PPP raw string send.</span></span>
- <span data-ttu-id="47ab4-438">NX_PTR_ERROR: (0x07) puntatore PPP o puntatore di stringa non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-438">NX_PTR_ERROR: (0x07) Invalid PPP pointer or string pointer.</span></span>
- <span data-ttu-id="47ab4-439">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-439">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-440">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-440">Allowed From</span></span>

<span data-ttu-id="47ab4-441">Thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-441">Threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-442">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-442">Example</span></span>

```c

/* Send “CLIENTSERVER” to “CLIENT” sent by Windows 98 before PPP is
initiated.  */
status =  nx_ppp_raw_string_send(&my_ppp, “CLIENTSERVER”);

/* If status is NX_SUCCESS the raw string was successfully Sent via PPP. */
```
## <a name="nx_ppp_restart"></a><span data-ttu-id="47ab4-443">nx_ppp_restart</span><span class="sxs-lookup"><span data-stu-id="47ab4-443">nx_ppp_restart</span></span>

<span data-ttu-id="47ab4-444">Riavvia elaborazione PPP</span><span class="sxs-lookup"><span data-stu-id="47ab4-444">Restart PPP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-445">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-445">Prototype</span></span>

```c
UINT  nx_ppp_restart(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-446">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-446">Description</span></span>

<span data-ttu-id="47ab4-447">Questo servizio riavvia l'elaborazione PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-447">This service restarts the PPP processing.</span></span> <span data-ttu-id="47ab4-448">Viene in genere chiamato quando il collegamento deve essere ristabilito da un callback di collegamento disattivato o da un messaggio modem non PPP che indica che la comunicazione è stata persa.</span><span class="sxs-lookup"><span data-stu-id="47ab4-448">It is typically called when the link needs to be re-established either from a link down callback or by a non-PPP modem message indicating communication was lost.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-449">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-449">Input Parameters</span></span>

- <span data-ttu-id="47ab4-450">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-450">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-451">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-451">Return Values</span></span>

- <span data-ttu-id="47ab4-452">**NX_SUCCESS**: (0x00) il riavvio PPP riuscito è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="47ab4-452">**NX_SUCCESS**: (0x00) Successful PPP restart initiated.</span></span>
- <span data-ttu-id="47ab4-453">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-453">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="47ab4-454">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-454">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-455">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-455">Allowed From</span></span>

<span data-ttu-id="47ab4-456">Thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-456">Threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-457">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-457">Example</span></span>

```c
/* Restart the PPP instance “my_ppp”.  */
status =  nx_ppp_restart(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been restarted. */
```

## <a name="nx_ppp_start"></a><span data-ttu-id="47ab4-458">nx_ppp_start</span><span class="sxs-lookup"><span data-stu-id="47ab4-458">nx_ppp_start</span></span>

<span data-ttu-id="47ab4-459">Avviare l'elaborazione PPP</span><span class="sxs-lookup"><span data-stu-id="47ab4-459">Start PPP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-460">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-460">Prototype</span></span>

```c
UINT  nx_ppp_start(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-461">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-461">Description</span></span>

<span data-ttu-id="47ab4-462">Questo servizio avvia l'elaborazione PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-462">This service starts the PPP processing.</span></span> <span data-ttu-id="47ab4-463">Viene in genere chiamato dopo la chiamata di nx_ppp_stop ().</span><span class="sxs-lookup"><span data-stu-id="47ab4-463">It is typically called after nx_ppp_stop() called.</span></span>

>[!NOTE]
> <span data-ttu-id="47ab4-464">PPP avvia automaticamente l'elaborazione PPP quando il collegamento è abilitato.</span><span class="sxs-lookup"><span data-stu-id="47ab4-464">PPP automatically starts the PPP processing when the link is enabled.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-465">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-465">Input Parameters</span></span>

- <span data-ttu-id="47ab4-466">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-466">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-467">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-467">Return Values</span></span>

- <span data-ttu-id="47ab4-468">**NX_SUCCESS**: (0x00) avviata PPP riuscita avviata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-468">**NX_SUCCESS**: (0x00) Successful PPP start initiated.</span></span> 
- <span data-ttu-id="47ab4-469">**NX_PPP_ALREADY_STARTED**: (0XB9) PPP già avviato.</span><span class="sxs-lookup"><span data-stu-id="47ab4-469">**NX_PPP_ALREADY_STARTED**: (0xb9) PPP already started.</span></span>
- <span data-ttu-id="47ab4-470">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-470">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="47ab4-471">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-471">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-472">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-472">Allowed From</span></span>

<span data-ttu-id="47ab4-473">Thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-473">Threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-474">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-474">Example</span></span>

```c
/* Start the PPP instance “my_ppp”.  */
status =  nx_ppp_start(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been started. */
```

## <a name="nx_ppp_status_get"></a><span data-ttu-id="47ab4-475">nx_ppp_status_get</span><span class="sxs-lookup"><span data-stu-id="47ab4-475">nx_ppp_status_get</span></span>

<span data-ttu-id="47ab4-476">Ottieni stato PPP corrente</span><span class="sxs-lookup"><span data-stu-id="47ab4-476">Get current PPP status</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-477">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-477">Prototype</span></span>

```c
UINT  nx_ppp_status_get(NX_PPP *ppp_ptr, UINT *status_ptr);
```
### <a name="description"></a><span data-ttu-id="47ab4-478">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-478">Description</span></span>

<span data-ttu-id="47ab4-479">Questo servizio ottiene lo stato corrente dell'istanza di PPP specificata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-479">This service gets the current status of the specified PPP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-480">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-480">Input Parameters</span></span>

- <span data-ttu-id="47ab4-481">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-481">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-482">**STATUS_PTR**: destinazione per lo stato PPP, di seguito sono riportati i valori di stato possibili:</span><span class="sxs-lookup"><span data-stu-id="47ab4-482">**status_ptr**: Destination for the PPP status, the following are possible status values:</span></span>
    - <span data-ttu-id="47ab4-483">**NX_PPP_STATUS_ESTABLISHED**</span><span class="sxs-lookup"><span data-stu-id="47ab4-483">**NX_PPP_STATUS_ESTABLISHED**</span></span>
    - <span data-ttu-id="47ab4-484">**NX_PPP_STATUS_LCP_IN_PROGRESS**</span><span class="sxs-lookup"><span data-stu-id="47ab4-484">**NX_PPP_STATUS_LCP_IN_PROGRESS**</span></span>
    - <span data-ttu-id="47ab4-485">**NX_PPP_STATUS_LCP_FAILED**</span><span class="sxs-lookup"><span data-stu-id="47ab4-485">**NX_PPP_STATUS_LCP_FAILED**</span></span>
    - <span data-ttu-id="47ab4-486">**NX_PPP_STATUS_PAP_IN_PROGRESS**</span><span class="sxs-lookup"><span data-stu-id="47ab4-486">**NX_PPP_STATUS_PAP_IN_PROGRESS**</span></span>
    - <span data-ttu-id="47ab4-487">**NX_PPP_STATUS_PAP_FAILED**</span><span class="sxs-lookup"><span data-stu-id="47ab4-487">**NX_PPP_STATUS_PAP_FAILED**</span></span>
    - <span data-ttu-id="47ab4-488">**NX_PPP_STATUS_CHAP_IN_PROGRESS**</span><span class="sxs-lookup"><span data-stu-id="47ab4-488">**NX_PPP_STATUS_CHAP_IN_PROGRESS**</span></span>
    - <span data-ttu-id="47ab4-489">**NX_PPP_STATUS_CHAP_FAILED**</span><span class="sxs-lookup"><span data-stu-id="47ab4-489">**NX_PPP_STATUS_CHAP_FAILED**</span></span>
    - <span data-ttu-id="47ab4-490">**NX_PPP_STATUS_IPCP_IN_PROGRESS**</span><span class="sxs-lookup"><span data-stu-id="47ab4-490">**NX_PPP_STATUS_IPCP_IN_PROGRESS**</span></span>
    - <span data-ttu-id="47ab4-491">**NX_PPP_STATUS_IPCP_FAILED**</span><span class="sxs-lookup"><span data-stu-id="47ab4-491">**NX_PPP_STATUS_IPCP_FAILED**</span></span>

>[!NOTE]
> <span data-ttu-id="47ab4-492">Lo stato è valido solo se l'API restituisce NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="47ab4-492">The status is only valid if the API returns NX_SUCCESS.</span></span> <span data-ttu-id="47ab4-493">Inoltre, se viene restituito uno dei valori di stato \* _FAILED, l'elaborazione PPP viene arrestata in modo efficace fino al riavvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="47ab4-493">In addition, if any of the \*_FAILED status values are returned, PPP processing is effectively stopped until it is restarted again by the application.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-494">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-494">Return Values</span></span>

- <span data-ttu-id="47ab4-495">**NX_SUCCESS**: (0x00) richiesta di stato PPP riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-495">**NX_SUCCESS**: (0x00) Successful PPP status request.</span></span>
- <span data-ttu-id="47ab4-496">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-496">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-497">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-497">Allowed From</span></span>

<span data-ttu-id="47ab4-498">Inizializzazione, thread, timer, ISRs</span><span class="sxs-lookup"><span data-stu-id="47ab4-498">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-499">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-499">Example</span></span>

```c
UINT ppp_status;
UINT status;


/* Get the current status of PPP instance “my_ppp”.  */
status =  nx_ppp_status_get(&my_ppp, &ppp_status);

/* If status is NX_SUCCESS the current internal PPP status is contained in
   “ppp_status”. */
```
## <a name="nx_ppp_stop"></a><span data-ttu-id="47ab4-500">nx_ppp_stop</span><span class="sxs-lookup"><span data-stu-id="47ab4-500">nx_ppp_stop</span></span>

<span data-ttu-id="47ab4-501">Avviare l'elaborazione PPP</span><span class="sxs-lookup"><span data-stu-id="47ab4-501">Start PPP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-502">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-502">Prototype</span></span>

```c
UINT  nx_ppp_stop(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="47ab4-503">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-503">Description</span></span>

<span data-ttu-id="47ab4-504">Questo servizio interrompe l'elaborazione PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-504">This service stops the PPP processing.</span></span> <span data-ttu-id="47ab4-505">L'utente può anche chiamare nx_ppp_start () per avviare l'elaborazione PPP, se necessario.</span><span class="sxs-lookup"><span data-stu-id="47ab4-505">User also can calls nx_ppp_start() to start the PPP processing if needed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-506">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-506">Input Parameters</span></span>

- <span data-ttu-id="47ab4-507">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-507">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-508">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-508">Return Values</span></span>

- <span data-ttu-id="47ab4-509">**NX_SUCCESS**: (0x00) avviata PPP riuscita avviata.</span><span class="sxs-lookup"><span data-stu-id="47ab4-509">**NX_SUCCESS**: (0x00) Successful PPP start initiated.</span></span> 
- <span data-ttu-id="47ab4-510">**NX_PPP_ALREADY_STOPPED**: (0XB8) PPP è già stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="47ab4-510">**NX_PPP_ALREADY_STOPPED**: (0xb8) PPP already stopped.</span></span>
- <span data-ttu-id="47ab4-511">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-511">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="47ab4-512">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="47ab4-512">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-513">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-513">Allowed From</span></span>

<span data-ttu-id="47ab4-514">Thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-514">Threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-515">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-515">Example</span></span>

```c
/* Stop the PPP instance “my_ppp”.  */
status =  nx_ppp_stop(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been stopped. */
```
## <a name="nx_ppp_packet_receive"></a><span data-ttu-id="47ab4-516">nx_ppp_packet_receive</span><span class="sxs-lookup"><span data-stu-id="47ab4-516">nx_ppp_packet_receive</span></span>

<span data-ttu-id="47ab4-517">Ricevi pacchetto PPP</span><span class="sxs-lookup"><span data-stu-id="47ab4-517">Receive PPP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-518">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-518">Prototype</span></span>

```c
UINT  nx_ppp_packet_receive(NX_PPP *ppp_ptr, NX_PACKET *packet_ptr);

```

### <a name="description"></a><span data-ttu-id="47ab4-519">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-519">Description</span></span>

<span data-ttu-id="47ab4-520">Questo servizio riceve il pacchetto PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-520">This service receives PPP packet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-521">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-521">Input Parameters</span></span>

- <span data-ttu-id="47ab4-522">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-522">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-523">**packet_ptr**: puntatore al pacchetto PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-523">**packet_ptr**: Pointer to PPP packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-524">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-524">Return Values</span></span>

- <span data-ttu-id="47ab4-525">**NX_SUCCESS**: (0x00) richiesta di stato PPP riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-525">**NX_SUCCESS**: (0x00) Successful PPP status request.</span></span>
- <span data-ttu-id="47ab4-526">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-526">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-527">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-527">Allowed From</span></span>

<span data-ttu-id="47ab4-528">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-528">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-529">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-529">Example</span></span>

```c
/* Receive the PPP packet of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_receive(&my_ppp, packet_ptr);

/* If status is NX_SUCCESS the PPP packet has received. */


```
## <a name="nx_ppp_packet_send_set"></a><span data-ttu-id="47ab4-530">nx_ppp_packet_send_set</span><span class="sxs-lookup"><span data-stu-id="47ab4-530">nx_ppp_packet_send_set</span></span>

<span data-ttu-id="47ab4-531">Impostare la funzione di invio pacchetti PPP</span><span class="sxs-lookup"><span data-stu-id="47ab4-531">Set the PPP packet send function</span></span>

### <a name="prototype"></a><span data-ttu-id="47ab4-532">Prototipo</span><span class="sxs-lookup"><span data-stu-id="47ab4-532">Prototype</span></span>

```c
UINT  nx_ppp_packet_send_set(NX_PPP *ppp_ptr, 
                             VOID (*nx_ppp_packet_send)(NX_PACKET *packet_ptr));

```

### <a name="description"></a><span data-ttu-id="47ab4-533">Descrizione</span><span class="sxs-lookup"><span data-stu-id="47ab4-533">Description</span></span>

<span data-ttu-id="47ab4-534">Questo servizio imposta il funciton di invio del pacchetto PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-534">This service sets the PPP packet send funciton.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="47ab4-535">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="47ab4-535">Input Parameters</span></span>

- <span data-ttu-id="47ab4-536">**ppp_ptr**: puntatore al blocco di controllo PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-536">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="47ab4-537">**nx_ppp_packet_send**: routine per l'invio del pacchetto PPP.</span><span class="sxs-lookup"><span data-stu-id="47ab4-537">**nx_ppp_packet_send**: Routine to send PPP packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="47ab4-538">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="47ab4-538">Return Values</span></span>

- <span data-ttu-id="47ab4-539">**NX_SUCCESS**: (0x00) richiesta di stato PPP riuscita.</span><span class="sxs-lookup"><span data-stu-id="47ab4-539">**NX_SUCCESS**: (0x00) Successful PPP status request.</span></span>
- <span data-ttu-id="47ab4-540">NX_PTR_ERROR: (0x07) puntatore PPP non valido.</span><span class="sxs-lookup"><span data-stu-id="47ab4-540">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="47ab4-541">Consentito da</span><span class="sxs-lookup"><span data-stu-id="47ab4-541">Allowed From</span></span>

<span data-ttu-id="47ab4-542">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="47ab4-542">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="47ab4-543">Esempio</span><span class="sxs-lookup"><span data-stu-id="47ab4-543">Example</span></span>

```c
/* Set the PPP packet send function of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_send_set(&my_ppp, nx_ppp_packet_send);

/* If status is NX_SUCCESS the PPP packet send function has set. */


```