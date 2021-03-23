---
title: Appendice A-Descrizione della funzionalità di ripristino dello stato per il client DHCPv6 RTO NetX duo di Azure
description: L'NX_DHCPV6_CLIENT_RESTORE_STATE opzione di configurazione client Azure RTO NetX Duo DHDPv6 consente a un sistema di ripristinare un client DHCP creato in precedenza in uno stato associato tra i riavvii del sistema.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3e642af158202bb3b2a4e2a37397b47d707b566e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822004"
---
# <a name="appendix-a---description-of-the-restore-state-feature-for-azure-rtos-netx-duo-dhcpv6-client"></a><span data-ttu-id="f25bd-103">Appendice A-Descrizione della funzionalità di ripristino dello stato per il client DHCPv6 RTO NetX duo di Azure</span><span class="sxs-lookup"><span data-stu-id="f25bd-103">Appendix A - Description of the Restore State Feature for Azure RTOS NetX Duo DHCPv6 Client</span></span>

<span data-ttu-id="f25bd-104">L'NX_DHCPV6_CLIENT_RESTORE_STATE opzione di configurazione client Azure RTO NetX Duo DHDPv6 consente a un sistema di ripristinare un client DHCP creato in precedenza in uno stato associato tra i riavvii del sistema.</span><span class="sxs-lookup"><span data-stu-id="f25bd-104">The Azure RTOS NetX Duo DHDPv6 Client configuration option, NX_DHCPV6_CLIENT_RESTORE_STATE, allows a system to restore a previously created DHCP Client in a Bound state between system reboots.</span></span>

<span data-ttu-id="f25bd-105">Questa opzione consente anche a un'applicazione di sospendere il thread del client DHCPv6 e di riprenderlo, aggiornato con il tempo trascorso tra la sospensione e la ripresa del thread senza spegnimento.</span><span class="sxs-lookup"><span data-stu-id="f25bd-105">This option also allows an application to suspend the DHCPv6 Client thread and resume it, updated with the elapsed time between suspending and resuming the thread without powering down.</span></span>

## <a name="restoring-the-dhcpv6-client-between-reboots"></a><span data-ttu-id="f25bd-106">Ripristino del client DHCPv6 tra i riavvii</span><span class="sxs-lookup"><span data-stu-id="f25bd-106">Restoring the DHCPv6 Client between Reboots</span></span>

<span data-ttu-id="f25bd-107">Per ripristinare un client DHCPv6 tra i riavvii, l'applicazione DHCPv6 crea un'istanza del client DHCPv6, quindi ottiene un lease di indirizzi IP utilizzando il protocollo DHCPv6 normale e chiamando *nx_dhcpv6_start*.</span><span class="sxs-lookup"><span data-stu-id="f25bd-107">To restore a DHCPv6 Client between reboots, the DHCPv6 application creates an instance of the DHCPv6 Client, and then obtains an IP address lease using the normal DHCPv6 protocol and calling *nx_dhcpv6_start*.</span></span> <span data-ttu-id="f25bd-108">L'applicazione DHCPv6 attende quindi il completamento del protocollo.</span><span class="sxs-lookup"><span data-stu-id="f25bd-108">Then the DHCPv6 application waits for the protocol to complete.</span></span> <span data-ttu-id="f25bd-109">Se tutto va bene, il dispositivo raggiunge lo stato associato con un indirizzo IP valido assegnato dal server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="f25bd-109">If all goes well, the device achieves the BOUND state with an assigned valid IP address from its DHCPv6 Server.</span></span> <span data-ttu-id="f25bd-110">Prima che venga disattivato, l'applicazione client DHCPv6 Salva l'istanza corrente del client DHCPv6 in un record client DHCPv6 che viene quindi archiviato nella memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="f25bd-110">Before it powers down, the DHCPv6 Client application saves the current DHCPv6 Client instance to a DHCPv6 Client record which is then stored in non-volatile memory.</span></span> <span data-ttu-id="f25bd-111">Un "Time Keeper" indipendente in un'altra parte del sistema tiene traccia del tempo trascorso durante questo stato spento.</span><span class="sxs-lookup"><span data-stu-id="f25bd-111">An independent ‘time keeper’ elsewhere in the system keeps track of the time elapsed during this powered down state.</span></span> <span data-ttu-id="f25bd-112">Durante l'accensione, l'applicazione crea una nuova istanza del client DHCPv6 e la aggiorna con il record client DHCPv6 creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f25bd-112">On powering up, the application creates a new DHCPv6 Client instance, and then updates it with the previously created DHCPv6 Client record.</span></span> <span data-ttu-id="f25bd-113">Il tempo trascorso viene ottenuto dal "Time Keeper" e quindi applicato al tempo rimanente nel lease Clientv6 DHCP.</span><span class="sxs-lookup"><span data-stu-id="f25bd-113">The elapsed time is obtained from the “time keeper” and then applied to the time remaining on the DHCP Clientv6 lease.</span></span> <span data-ttu-id="f25bd-114">A questo punto, l'applicazione può riprendere il client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="f25bd-114">At this point, the application can resume the DHCPv6 Client.</span></span>

<span data-ttu-id="f25bd-115">Se il tempo trascorso durante il spegnimento imposta lo stato del client DHCPv6 in stato di rinnovo o riassociazione, il client DHCPv6 avvierà automaticamente i messaggi DHCPv6 che richiedono di rinnovare o riassociare il lease dell'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="f25bd-115">If the time elapsed during power down puts the DHCPv6 Client state in either a RENEW or REBIND state, the DHCPv6 Client will automatically initiate DHCPv6 messages requesting to renew or rebind the IP address lease.</span></span> <span data-ttu-id="f25bd-116">Se l'indirizzo IP è scaduto, il client DHCPv6 cancellerà automaticamente l'indirizzo IP nell'istanza IP e avvierà il processo DHCPv6 dallo stato INIT, richiedendo un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="f25bd-116">If the IP address is expired, the DHCPv6 Client will automatically clear the IP address on the IP instance and begin the DHCPv6 process from the INIT state, requesting a new IP address.</span></span>

<span data-ttu-id="f25bd-117">In questo modo il client DHCPv6 può operare tra i riavvii come se non fosse interrotto.</span><span class="sxs-lookup"><span data-stu-id="f25bd-117">In this manner the DHCPv6 Client can operate between reboots as if uninterrupted.</span></span>

<span data-ttu-id="f25bd-118">Di seguito è riportata un'illustrazione di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f25bd-118">Below is an illustration of this feature.</span></span>

```C
/* On the power up, create an IP instance, DHCPv6 Client, enable ICMPv6 and UDP
   and other resources (not shown) for the DHCPv6 Client/application
   in tx_application_define(). */
 
/* Define the DHCPv6 Client application thread. */     
void    thread_dhcpv6_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCPV6_CLIENT_RECORD client_my_record;


    /* No previously saved Client record. Start the DHCPv6 Client in the INIT state. */
    status =  nx_dhcpv6_start(&dhcp_0);

    if (status !=NX_SUCCESS)
        return;

    while(1)    
    {
    
        /* Wait for DHCPv6 Client to get the IP address. */
    }

    /* At some point decide we power down the system. */

    /* Save the Client state data which we will subsequently need to restore the DHCPv6    
       Client. */
    status = nx_dhcpv6_client_get_record(&dhcp_0, &client_my_record);               

    /* Copy this memory to non-volatile memory (not shown). */

    /* Delete the IP and DHCPv6 Client instances before powering down. */
    nx_dhcpv6_client_delete(&dhcp_0);

    nx_ip_delete(&ip_0);

    /* Ready to power down, having released other resources as necessary. */

    /* The application has determined there is a previously saved record. We will 
       restore it to the current DHCPv6 Client instance. */

/* Create the IP and DHCPv6 Client instances, enable ICMPv6 and UDP after powering up. */

/* Calculate the time elapsed during power down */

    /* Get the previous Client state data from non-volatile memory. */

    /* Apply the record to the current Client instance. This will also 
       update the IP instance with IP address, mask etc. */
    status = nx_dhcpv6_client_restore_record(&dhcp_0, &client_my_record, time_elapsed);   

     if (status != NX_SUCCESS)
          return;

     /* We are ready to resume the DHCPv6 Client thread and use the assigned IP address. */
     status = nx_dhcpv6_resume(&dhcp_0);

     if (status != NX_SUCCESS)
          return;

}
```

## <a name="nx_dhcpv6_client_get_record"></a><span data-ttu-id="f25bd-119">nx_dhcpv6_client_get_record</span><span class="sxs-lookup"><span data-stu-id="f25bd-119">nx_dhcpv6_client_get_record</span></span>

<span data-ttu-id="f25bd-120">Creare un record dello stato corrente del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="f25bd-120">Create a record of the current DHCPv6 Client state</span></span>

### <a name="prototype"></a><span data-ttu-id="f25bd-121">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f25bd-121">Prototype</span></span>

```C
ULONG nx_dhcpv6_client_get_record(NX_DHCPV6 *dhcpv6_ptr, 
                                  NX_DHCPV6_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a><span data-ttu-id="f25bd-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f25bd-122">Description</span></span>

<span data-ttu-id="f25bd-123">Questo servizio salva il client DHCPv6 nel record a cui fa riferimento record_ptr.</span><span class="sxs-lookup"><span data-stu-id="f25bd-123">This service saves the DHCPv6 Client to the record pointed to by record_ptr.</span></span> <span data-ttu-id="f25bd-124">Ciò consente all'applicazione client DHCPv6 di ripristinare lo stato del client DHCPv6 dopo, ad esempio, un spegnimento e un riavvio.</span><span class="sxs-lookup"><span data-stu-id="f25bd-124">This allows the DHCPv6 Client application restore its DHCPv6 Client state after, for example, a power down and reboot.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f25bd-125">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="f25bd-125">Input Parameters</span></span>

- <span data-ttu-id="f25bd-126">**dhcpv6_ptr** Puntatore al client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="f25bd-126">**dhcpv6_ptr** Pointer to DHCPv6 Client</span></span>

- <span data-ttu-id="f25bd-127">**record_ptr** Puntatore al record client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="f25bd-127">**record_ptr** Pointer to DHCPv6 Client record</span></span>

### <a name="return-values"></a><span data-ttu-id="f25bd-128">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f25bd-128">Return Values</span></span>

- <span data-ttu-id="f25bd-129">**NX_SUCCESS (0x0)** Record client valido creato</span><span class="sxs-lookup"><span data-stu-id="f25bd-129">**NX_SUCCESS (0x0)** Valid Client record created</span></span>

- <span data-ttu-id="f25bd-130">Il client **NX_DHCPV6_NOT_BOUND** (0xE94) non è in stato associato e pertanto non è stato assegnato un indirizzo IP valido</span><span class="sxs-lookup"><span data-stu-id="f25bd-130">**NX_DHCPV6_NOT_BOUND** (0xE94) Client not in bound state, therefore not assigned valid IP address</span></span>

- <span data-ttu-id="f25bd-131">**NX_PTR_ERROR** (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="f25bd-131">**NX_PTR_ERROR** (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f25bd-132">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f25bd-132">Allowed From</span></span>

<span data-ttu-id="f25bd-133">Thread</span><span class="sxs-lookup"><span data-stu-id="f25bd-133">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f25bd-134">Esempio</span><span class="sxs-lookup"><span data-stu-id="f25bd-134">Example</span></span>

```C
NX_DHCPV6_CLIENT_RECORD dhcpv6_record;


/* Obtain a record of the current client state. */
status=  nx_dhcpv6_client_get_record(&dhcpv6_ptr, &dhcpv6_record);

/* If status is NX_SUCCESS dhcpv6_record contains the current DHCPv6 client record. */
```

### <a name="see-also"></a><span data-ttu-id="f25bd-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f25bd-135">See Also</span></span>

- <span data-ttu-id="f25bd-136">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="f25bd-136">nx_dhcpv6_resume</span></span>
- <span data-ttu-id="f25bd-137">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="f25bd-137">nx_dhcpv6_suspend</span></span>
- <span data-ttu-id="f25bd-138">nx_dhcpv6_client_restore_record</span><span class="sxs-lookup"><span data-stu-id="f25bd-138">nx_dhcpv6_client_restore_record</span></span>

## <a name="nx_dhcpv6_client_restore_record"></a><span data-ttu-id="f25bd-139">nx_dhcpv6_client_restore_record</span><span class="sxs-lookup"><span data-stu-id="f25bd-139">nx_dhcpv6_client_restore_record</span></span>

<span data-ttu-id="f25bd-140">Ripristinare lo stato del client DHCPv6 dal record salvato</span><span class="sxs-lookup"><span data-stu-id="f25bd-140">Restore DHCPv6 Client state from saved record</span></span>

### <a name="prototype"></a><span data-ttu-id="f25bd-141">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f25bd-141">Prototype</span></span>

```C
ULONG nx_dhcpv6_client_restore_record(NX_DHCPV6 *dhcpv6_ptr, 
                                      NX_DHCPV6_CLIENT_RECORD       
                                      *record_ptr, ULONG time_elapsed);
```

### <a name="description"></a><span data-ttu-id="f25bd-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f25bd-142">Description</span></span>

<span data-ttu-id="f25bd-143">Questo servizio consente a un'applicazione DHCPv6 di ricreare lo stato client DHCPv6 da una sessione precedente aggiornando il client DHCPv6 con il record client DHCPv6 a cui punta record_ptr e aggiorna il tempo rimanente per il lease del client DHCPv6 con l'input di time_elapsed.</span><span class="sxs-lookup"><span data-stu-id="f25bd-143">This service enables a DHCPv6 application to recreate its DHCPv6 Client state from a previous session by updating the DHCPv6 Client with the DHCPv6 Client record pointed to by record_ptr, and updates the time remaining on DHCPv6 Client lease with the time_elapsed input.</span></span> <span data-ttu-id="f25bd-144">Ciò consente all'applicazione client DHCPv6 di ricreare il client DHCPv6, ad esempio dopo l'accensione.</span><span class="sxs-lookup"><span data-stu-id="f25bd-144">This allows the DHCPv6 Client application to recreate its DHCPv6 Client, for example, after powering down.</span></span> <span data-ttu-id="f25bd-145">A tale scopo, è necessario che l'applicazione client DHCPv6 abbia creato un record del client DHCPv6 prima dell'accensione e abbia salvato tale record nella memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="f25bd-145">This requires that the DHCPv6 Client application created a record of the DHCPv6 Client before powering down, and saved that record to non-volatile memory.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f25bd-146">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="f25bd-146">Input Parameters</span></span>

- <span data-ttu-id="f25bd-147">**dhcpv6_ptr** Puntatore al client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="f25bd-147">**dhcpv6_ptr** Pointer to DHCPv6 Client</span></span>

- <span data-ttu-id="f25bd-148">**record_ptr** Puntatore al record client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="f25bd-148">**record_ptr** Pointer to DHCPv6 Client record</span></span>

- <span data-ttu-id="f25bd-149">**time_elapsed** Tempo di sottrazione dal tempo di lease rimanente nel record client di input</span><span class="sxs-lookup"><span data-stu-id="f25bd-149">**time_elapsed** Time to subtract from the lease time remaining in the input client record</span></span>

### <a name="return-values"></a><span data-ttu-id="f25bd-150">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f25bd-150">Return Values</span></span>

- <span data-ttu-id="f25bd-151">**NX_SUCCESS (0x0)** Record client ripristinato</span><span class="sxs-lookup"><span data-stu-id="f25bd-151">**NX_SUCCESS (0x0)** Client record restored</span></span>

- <span data-ttu-id="f25bd-152">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="f25bd-152">NX_PTR_ERROR (0x16) Invalid Pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f25bd-153">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f25bd-153">Allowed From</span></span>

<span data-ttu-id="f25bd-154">Thread</span><span class="sxs-lookup"><span data-stu-id="f25bd-154">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f25bd-155">Esempio</span><span class="sxs-lookup"><span data-stu-id="f25bd-155">Example</span></span>

```C
NX_DHCPV6_CLIENT_RECORD dhcpv6_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 

/* Obtain a record of the current client state. */
status=  nx_dhcpv6_client_restore_record(&dhcpv6_ptr, &dhcpv6_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCPv6 Client pointed to by dhcpv6_ptr contains the current client record updated for time elapsed during power down. */
```

### <a name="see-also"></a><span data-ttu-id="f25bd-156">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f25bd-156">See Also</span></span>

- <span data-ttu-id="f25bd-157">nx_dhcpv6_client_get_record</span><span class="sxs-lookup"><span data-stu-id="f25bd-157">nx_dhcpv6_client_get_record</span></span>