---
title: Appendice A-Descrizione della funzionalità di stato di ripristino
description: L'NX_DHCP_CLIENT_RESTORE_STATE opzione di configurazione del client Azure RTO NetX DHDP consente a un sistema di ripristinare un record client DHCP creato in precedenza in uno stato associato tra i riavvii del sistema.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be8b5dc4885951bee3dba38af6fe5e21b81aa767
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822712"
---
# <a name="appendix-a---description-of-the-restore-state-feature"></a><span data-ttu-id="5663b-103">Appendice A-Descrizione della funzionalità di stato di ripristino</span><span class="sxs-lookup"><span data-stu-id="5663b-103">Appendix A - Description of the Restore State Feature</span></span>

<span data-ttu-id="5663b-104">L'NX_DHCP_CLIENT_RESTORE_STATE opzione di configurazione del client Azure RTO NetX DHDP consente a un sistema di ripristinare un record client DHCP creato in precedenza in uno stato associato tra i riavvii del sistema.</span><span class="sxs-lookup"><span data-stu-id="5663b-104">The Azure RTOS NetX DHDP Client configuration option, NX_DHCP_CLIENT_RESTORE_STATE, allows a system to restore a previously created DHCP Client Record in a Bound state between system reboots.</span></span>

<span data-ttu-id="5663b-105">Quando questa opzione è abilitata, l'applicazione può sospendere e riprendere il thread del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-105">When this option is enabled, the application can suspend and resume the DHCP Client thread.</span></span> <span data-ttu-id="5663b-106">È inoltre disponibile un servizio per aggiornare il client DHCP con il tempo trascorso tra la sospensione e la ripresa del thread.</span><span class="sxs-lookup"><span data-stu-id="5663b-106">There is also a service to update the DHCP Client with the elapsed time between suspending and resuming the thread.</span></span>

## <a name="restoring-the-dhcp-client-between-reboots"></a><span data-ttu-id="5663b-107">Ripristino del client DHCP tra i riavvii</span><span class="sxs-lookup"><span data-stu-id="5663b-107">Restoring the DHCP Client between Reboots</span></span>

<span data-ttu-id="5663b-108">Prima di ripristinare un client DHCP dopo il riavvio, un client DHCP creato in precedenza che deve raggiungere lo stato associato e a cui viene assegnato un indirizzo IP dal server DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-108">Before restoring a DHCP Client after rebooting, a previously created DHCP Client that must reach the Bound state and be is assigned an IP address from the DHCP server.</span></span> <span data-ttu-id="5663b-109">Prima che venga disattivato, l'applicazione DHCP deve quindi salvare il record client DHCP corrente nella memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="5663b-109">Before it powers down, the DHCP application must then save the current DHCP Client record to non-volatile memory.</span></span> <span data-ttu-id="5663b-110">Per tenere traccia del tempo trascorso durante questo stato di spegnimento, è inoltre necessario che sia presente un "Time Keeper" indipendente.</span><span class="sxs-lookup"><span data-stu-id="5663b-110">There must also be an independent ‘time keeper’ elsewhere in the system to keep track of the time elapsed during this powered down state.</span></span> <span data-ttu-id="5663b-111">Durante l'accensione, l'applicazione crea una nuova istanza del client DHCP, quindi la aggiorna con il record client DHCP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5663b-111">On powering up, the application creates a new DHCP Client instance, and then updates it with the previously created DHCP Client record.</span></span> <span data-ttu-id="5663b-112">Il tempo trascorso viene ottenuto dal "Time Keeper" e quindi applicato al tempo rimanente per il lease del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-112">The elapsed time is obtained from the “time keeper” and then applied to the time remaining on the DHCP Client lease.</span></span> <span data-ttu-id="5663b-113">Si noti che questo può causare la modifica degli Stati da parte del client DHCP, ad esempio dal limite al rinnovo.</span><span class="sxs-lookup"><span data-stu-id="5663b-113">Note that this may cause the DHCP Client to change states e.g. from BOUND to RENEWING.</span></span> <span data-ttu-id="5663b-114">A questo punto, l'applicazione può riprendere il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-114">At this point, the application can resume the DHCP Client.</span></span>

<span data-ttu-id="5663b-115">Se il tempo trascorso durante il spegnimento imposta lo stato del client DHCP in uno stato di rinnovo o riassociazione, il client DHCP avvierà automaticamente i messaggi DHCP che richiedono il rinnovo o il riassociazione del lease di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="5663b-115">If the time elapsed during power down puts the DHCP Client state in either a RENEW or REBIND state, the DHCP Client will automatically initiate DHCP messages requesting to renew or rebind the IP address lease.</span></span> <span data-ttu-id="5663b-116">Se l'indirizzo IP è scaduto, il client DHCP cancellerà automaticamente l'indirizzo IP nell'istanza IP e avvierà il processo DHCP dallo stato INIT, richiedendo un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="5663b-116">If the IP address is expired, the DHCP Client will automatically clear the IP address on the IP instance and begin the DHCP process from the INIT state, requesting a new IP address.</span></span>

<span data-ttu-id="5663b-117">In questo modo il client DHCP può operare tra i riavvii come se non fosse interrotto.</span><span class="sxs-lookup"><span data-stu-id="5663b-117">In this manner the DHCP Client can operate between reboots as if uninterrupted.</span></span>

<span data-ttu-id="5663b-118">Di seguito è riportata un'illustrazione di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5663b-118">Below is an illustration of this feature.</span></span> <span data-ttu-id="5663b-119">Si presuppone che il client DHCP sia in esecuzione solo sull'interfaccia primaria.</span><span class="sxs-lookup"><span data-stu-id="5663b-119">This assumes DHCP Client is running only on the primary interface.</span></span>

```C
/* On the power up, create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) for the DHCP Client/application
   in tx_application_define(). */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

UINT        status;
UINT        time_elapsed = 0;
NX_DHCP_CLIENT_RECORD client_nv_record;


if (/* The application checks if there is a previously saved DHCP Client record. */)
{


  /* No previously saved Client record. Start the DHCP Client in the INIT state. */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  do
  {
  
    /* Wait for DHCP to assign the IP address. */
  } while (status != NX_SUCCESS);

  /* We have a valid IP address. */

  /* At some point decide we power down the system. */

  /* Save the Client state data which we will subsequently need to restore the DHCP  
     Client. */
  status = nx_dhcp_client_get_record(&dhcp_0, &client_nv_record);         

  /* Copy this memory to non-volatile memory (not shown). */

  /* Delete the IP and DHCP Client instances before powering down. */
  nx_dhcp_delete(&dhcp_0);

  nx_ip_delete(&ip_0);

  /* Ready to power down, having released other resources as necessary. */

}
else
{

  /* The application has determined there is a previously saved record. We will 
     restore it to the current DHCP Client instance. */

  /* Get the previous Client state data from non-volatile memory. */

  /* Apply the record to the current Client instance. This will also 
     update the IP instance with IP address, mask etc. */
  status = nx_dhcp_client_restore_record(&dhcp_0, &client_nv_record, time_elapsed);   

     if (status != NX_SUCCESS)
      return;

     /* We are ready to resume the DHCP Client thread and use the assigned IP address. */
     status = nx_dhcp_resume(&dhcp_0);

     if (status != NX_SUCCESS)
      return;

}
```

## <a name="resuming-the-dhcp-client-thread-after-suspension"></a><span data-ttu-id="5663b-120">Ripresa del thread client DHCP dopo la sospensione</span><span class="sxs-lookup"><span data-stu-id="5663b-120">Resuming the DHCP Client Thread after Suspension</span></span> 

<span data-ttu-id="5663b-121">Per sospendere un thread client DHCP senza spegnere, l'applicazione chiama *nx_dhcp_suspend* su un client DHCP che ha raggiunto lo stato associato e che ha un indirizzo IP valido.</span><span class="sxs-lookup"><span data-stu-id="5663b-121">To suspend a DHCP Client thread without powering down, the application calls *nx_dhcp_suspend* on a DHCP Client which has achieved the BOUND state and which has a valid IP address.</span></span> <span data-ttu-id="5663b-122">Quando è pronto per riprendere il client DHCP, chiama prima di tutto *nx_dhcp_client_update_time_remaining* per aggiornare il tempo rimanente nel lease di indirizzi DHCP (ottenendo il tempo trascorso da un custode del tempo indipendente).</span><span class="sxs-lookup"><span data-stu-id="5663b-122">When it is ready to resume the DHCP Client it first calls *nx_dhcp_client_update_time_remaining* to update the time remaining on the DHCP address lease (obtaining the time elapsed from an independent time keeper).</span></span> <span data-ttu-id="5663b-123">Chiama quindi il *nx_dhcp_resume* per riprendere il thread del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-123">Then it calls the *nx_dhcp_resume* to resume the DHCP Client thread.</span></span>

<span data-ttu-id="5663b-124">Se il tempo trascorso imposta lo stato del client DHCP in uno stato di rinnovo o riassociazione, il client DHCP avvierà automaticamente i messaggi DHCP che richiedono il rinnovo o il riassociazione del lease di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="5663b-124">If the time elapsed puts the DHCP Client state in either a RENEW or REBIND state, the DHCP Client will automatically initiate DHCP messages requesting to renew or rebind the IP address lease.</span></span> <span data-ttu-id="5663b-125">Se l'indirizzo IP è scaduto, il client DHCP cancellerà automaticamente l'indirizzo IP e inizierà il processo DHCP dallo stato INIT, richiedendo un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="5663b-125">If the IP address is expired, the DHCP Client will automatically clear the IP address and begin the DHCP process from the INIT state, requesting a new IP address.</span></span>

<span data-ttu-id="5663b-126">Di seguito viene illustrato l'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5663b-126">Below is an illustration of using this feature.</span></span>

```C
/* Create an IP instance, DHCP Client, enable ICMP and UDP
   and other resources (not shown) typically in tx_application_define(). */
 
/* Define the DHCP application thread. */     
void    thread_dhcp_client_entry(ULONG thread_input)
{

  /* Start the DHCP Client. */
  status =  nx_dhcp_start(&dhcp_0);

  if (status !=NX_SUCCESS)
    return;

  while(1)
  {
   
    /* Wait for DHCP to obtain an IP address. */
  }

  /* Do tasks with the IP address e.g. send pings to another host on the 
     network... */
  status =  nx_icmp_ping(…);

  if (status !=NX_SUCCESS)
          printf("Failed %d byte Ping!\n", length);

  /* At some later time, suspend the DHCP Client e.g. the device is going to low 
   power mode (sleep) so we do not want any threads to wake it up. */

  nx_dhcp_suspend(&dhcp_0);  

  /* During this suspended state, an independent timer is keeping track of the
     elapsed time. */


  /* At some point, we are ready to resume the DHCP Client thread. */

  /* Update the DHCP Client lease time remaining with the time elapsed. */
  status = nx_dhcp_client_update_time_remaining(&dhcp_0, time_elapsed);   

  if (status != NX_SUCCESS)
       return;

  /* We now can resume the DHCP Client thread. */
  status = nx_dhcp_resume(&dhcp_0);

  if (status != NX_SUCCESS)
       return;

  /* Resume tasks e.g. ping another host. */
  status =  nx_icmp_ping(…);

}
```

<span data-ttu-id="5663b-127">Di seguito è riportato un elenco di servizi per il ripristino dello stato di un client DHCP dalla memoria e per la sospensione e la ripresa del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-127">Below is a list of services for restoring a DHCP Client state from memory and for suspending and resuming the DHCP Client.</span></span>

## <a name="nx_dhcp_client_get_record"></a><span data-ttu-id="5663b-128">nx_dhcp_client_get_record</span><span class="sxs-lookup"><span data-stu-id="5663b-128">nx_dhcp_client_get_record</span></span>

<span data-ttu-id="5663b-129">Creare un record dello stato corrente del client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-129">Create a record of the current DHCP Client state</span></span>

### <a name="prototype"></a><span data-ttu-id="5663b-130">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5663b-130">Prototype</span></span>

```C
ULONG nx_dhcp_ client_get_record(NX_DHCP *dhcp_ptr, 
                                 NX_DHCP_CLIENT_RECORD *record_ptr);
```

### <a name="description"></a><span data-ttu-id="5663b-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5663b-131">Description</span></span>

<span data-ttu-id="5663b-132">Questo servizio salva il client DHCP in esecuzione nella prima interfaccia abilitata per DHCP trovato nell'istanza del client DHCP al record a cui fa riferimento record_ptr.</span><span class="sxs-lookup"><span data-stu-id="5663b-132">This service saves the DHCP Client running on the first interface enabled for DHCP found on the DHCP Client instance to the record pointed to by record_ptr.</span></span> <span data-ttu-id="5663b-133">Ciò consente all'applicazione client DHCP di ripristinare lo stato del client DHCP dopo, ad esempio, un spegnimento e un riavvio.</span><span class="sxs-lookup"><span data-stu-id="5663b-133">This allows the DHCP Client application restore its DHCP Client state after, for example, a power down and reboot.</span></span>

<span data-ttu-id="5663b-134">Per salvare un record client DHCP in un'interfaccia specifica se è abilitata più di un'interfaccia per DHCP, usare il servizio *nx_dhcp_interface_client_get_record* .</span><span class="sxs-lookup"><span data-stu-id="5663b-134">To save a DHCP Client record on a specific interface if more than one interface is enabled for DHCP, use the *nx_dhcp_interface_client_get_record* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5663b-135">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5663b-135">Input Parameters</span></span>

- <span data-ttu-id="5663b-136">**dhcp_ptr** Puntatore al client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-136">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="5663b-137">**record_ptr** Puntatore al record client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-137">**record_ptr** Pointer to DHCP Client record</span></span>

### <a name="return-values"></a><span data-ttu-id="5663b-138">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5663b-138">Return Values</span></span>

- <span data-ttu-id="5663b-139">Record client di **NX_SUCCESS** (0x0) creato</span><span class="sxs-lookup"><span data-stu-id="5663b-139">**NX_SUCCESS** (0x0) Client record created</span></span>

- <span data-ttu-id="5663b-140">Client di **NX_DHCP_NOT_BOUND** (0x94) non in stato associato</span><span class="sxs-lookup"><span data-stu-id="5663b-140">**NX_DHCP_NOT_BOUND** (0x94) Client not in Bound state</span></span>

- <span data-ttu-id="5663b-141">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) non sono abilitate interfacce per DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-141">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces enabled for DHCP</span></span>

- <span data-ttu-id="5663b-142">**NX_PTR_ERROR** (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5663b-142">**NX_PTR_ERROR** (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5663b-143">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5663b-143">Allowed From</span></span>

<span data-ttu-id="5663b-144">Thread</span><span class="sxs-lookup"><span data-stu-id="5663b-144">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5663b-145">Esempio</span><span class="sxs-lookup"><span data-stu-id="5663b-145">Example</span></span>

```C
NX_DHCP_CLIENT_RECORD dhcp_record;


/* Obtain a record of the current client state. */
status=  nx_dhcp_client_get_record(dhcp_ptr, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_interface_client_get_record"></a><span data-ttu-id="5663b-146">nx_dhcp_interface_client_get_record</span><span class="sxs-lookup"><span data-stu-id="5663b-146">nx_dhcp_interface_client_get_record</span></span>

<span data-ttu-id="5663b-147">Crea un record dello stato del client DHCP corrente sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="5663b-147">Create a record of the current DHCP Client state on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="5663b-148">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5663b-148">Prototype</span></span>

```C
ULONG nx_dhcp_interface_client_get_record(NX_DHCP *dhcp_ptr, 
                                 UINT interface_index,
                                 NX_DHCP_CLIENT_RECORD *record_ptr);
```
### <a name="description"></a><span data-ttu-id="5663b-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5663b-149">Description</span></span>

<span data-ttu-id="5663b-150">Questo servizio salva il client DHCP in esecuzione nell'interfaccia specificata nel record a cui punta record_ptr.</span><span class="sxs-lookup"><span data-stu-id="5663b-150">This service saves the DHCP Client running on the specified interface to the record pointed to by record_ptr.</span></span> <span data-ttu-id="5663b-151">Ciò consente all'applicazione client DHCP di ripristinare lo stato del client DHCP dopo, ad esempio, un spegnimento e un riavvio.</span><span class="sxs-lookup"><span data-stu-id="5663b-151">This allows the DHCP Client application restore its DHCP Client state after, for example, a power down and reboot.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5663b-152">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5663b-152">Input Parameters</span></span>

- <span data-ttu-id="5663b-153">**dhcp_ptr** Puntatore al client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-153">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="5663b-154">**interface_index** Indice in corrispondenza del quale ottenere il record</span><span class="sxs-lookup"><span data-stu-id="5663b-154">**interface_index** Index on which to get record</span></span>

- <span data-ttu-id="5663b-155">**record_ptr** Puntatore al record client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-155">**record_ptr** Pointer to DHCP Client record</span></span>

### <a name="return-values"></a><span data-ttu-id="5663b-156">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5663b-156">Return Values</span></span>

- <span data-ttu-id="5663b-157">Record client di **NX_SUCCESS** (0x0) creato</span><span class="sxs-lookup"><span data-stu-id="5663b-157">**NX_SUCCESS** (0x0) Client record created</span></span>

- <span data-ttu-id="5663b-158">Client di **NX_DHCP_NOT_BOUND** (0x94) non in stato associato</span><span class="sxs-lookup"><span data-stu-id="5663b-158">**NX_DHCP_NOT_BOUND** (0x94) Client not in Bound state</span></span>

- <span data-ttu-id="5663b-159">Indice di interfaccia **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0X9A) non valido</span><span class="sxs-lookup"><span data-stu-id="5663b-159">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) Invalid interface index</span></span>

- <span data-ttu-id="5663b-160">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="5663b-160">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="5663b-161">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="5663b-161">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5663b-162">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5663b-162">Allowed From</span></span>

<span data-ttu-id="5663b-163">Thread</span><span class="sxs-lookup"><span data-stu-id="5663b-163">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5663b-164">Esempio</span><span class="sxs-lookup"><span data-stu-id="5663b-164">Example</span></span>

```C
NX_DHCP_CLIENT_RECORD dhcp_record;


/* Obtain a record of the current client state on interface 1. */
status=  nx_dhcp_interface_client_get_record(dhcp_ptr, 1, &dhcp_record);

/* If status is NX_SUCCESS dhcp_record contains the current DHCP client record. */
```

## <a name="nx_dhcp_-client_restore_record"></a><span data-ttu-id="5663b-165">nx_dhcp_ client_restore_record</span><span class="sxs-lookup"><span data-stu-id="5663b-165">nx_dhcp_ client_restore_record</span></span>

<span data-ttu-id="5663b-166">Ripristinare il client DHCP da un record salvato in precedenza</span><span class="sxs-lookup"><span data-stu-id="5663b-166">Restore DHCP Client from a previously saved record</span></span>

### <a name="prototype"></a><span data-ttu-id="5663b-167">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5663b-167">Prototype</span></span>

```C
ULONG nx_dhcp_client_restore_record(NX_DHCP *dhcp_ptr, 
                                    NX_DHCP_CLIENT_RECORD       
                                    *record_ptr, ULONG time_elapsed);
```
### <a name="description"></a><span data-ttu-id="5663b-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5663b-168">Description</span></span>

<span data-ttu-id="5663b-169">Questo servizio consente a un'applicazione di ripristinare il client DHCP da una sessione precedente utilizzando il record client DHCP a cui punta record_ptr.</span><span class="sxs-lookup"><span data-stu-id="5663b-169">This service enables an application to restore its DHCP Client from a previous session using the DHCP Client record pointed to by record_ptr.</span></span> <span data-ttu-id="5663b-170">L'input time_elapsed viene applicato al tempo rimanente per il lease del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-170">The time_elapsed input is applied to the time remaining on DHCP Client lease.</span></span>

<span data-ttu-id="5663b-171">A tale scopo, è necessario che l'applicazione client DHCP abbia creato un record del client DHCP prima dell'accensione e abbia salvato tale record nella memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="5663b-171">This requires that the DHCP Client application created a record of the DHCP Client before powering down, and saved that record to nonvolatile memory.</span></span>

<span data-ttu-id="5663b-172">Se è abilitata più di un'interfaccia per il client DHCP, questo servizio viene applicato alla prima interfaccia valida presente nell'istanza del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-172">If more than one interface is enabled for DHCP Client, this service is applied to the first valid interface found in the DHCP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5663b-173">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5663b-173">Input Parameters</span></span>

- <span data-ttu-id="5663b-174">**dhcp_ptr** Puntatore al client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-174">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="5663b-175">**record_ptr** Puntatore al record client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-175">**record_ptr** Pointer to DHCP Client record</span></span>

- <span data-ttu-id="5663b-176">**time_elapsed** Tempo di sottrazione dal tempo di lease rimanente nel record client di input</span><span class="sxs-lookup"><span data-stu-id="5663b-176">**time_elapsed** Time to subtract from the lease time remaining in the input client record</span></span>

### <a name="return-values"></a><span data-ttu-id="5663b-177">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5663b-177">Return Values</span></span>

- <span data-ttu-id="5663b-178">Record client di **NX_SUCCESS** (0x0) ripristinato</span><span class="sxs-lookup"><span data-stu-id="5663b-178">**NX_SUCCESS** (0x0) Client record restored</span></span>

- <span data-ttu-id="5663b-179">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) nessuna interfaccia che esegue DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-179">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces running DHCP</span></span>

- <span data-ttu-id="5663b-180">**NX_PTR_ERROR** (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5663b-180">**NX_PTR_ERROR** (0x16) Invalid pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5663b-181">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5663b-181">Allowed From</span></span>

<span data-ttu-id="5663b-182">Thread</span><span class="sxs-lookup"><span data-stu-id="5663b-182">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5663b-183">Esempio</span><span class="sxs-lookup"><span data-stu-id="5663b-183">Example</span></span>
```C
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state. */
status=  nx_dhcp_client_restore_record(client_ptr, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr
   contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_interace_client_restore_record"></a><span data-ttu-id="5663b-184">nx_dhcp_interace_client_restore_record</span><span class="sxs-lookup"><span data-stu-id="5663b-184">nx_dhcp_interace_client_restore_record</span></span>

<span data-ttu-id="5663b-185">Ripristina il client DHCP da un record salvato in precedenza nell'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="5663b-185">Restore DHCP Client from a previously saved record on specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="5663b-186">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5663b-186">Prototype</span></span>

```C
ULONG nx_dhcp_interface_client_restore_record(NX_DHCP *dhcp_ptr, 
                                              NX_DHCP_CLIENT_RECORD       
                                              *record_ptr, ULONG time_elapsed);
```
### <a name="description"></a><span data-ttu-id="5663b-187">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5663b-187">Description</span></span>

<span data-ttu-id="5663b-188">Questo servizio consente a un'applicazione di ripristinare il client DHCP sull'interfaccia specificata utilizzando il record client DHCP a cui punta record_ptr.</span><span class="sxs-lookup"><span data-stu-id="5663b-188">This service enables an application to restore its DHCP Client on the specified interface using the DHCP Client record pointed to by record_ptr.</span></span> <span data-ttu-id="5663b-189">L'input time_elapsed viene applicato al tempo rimanente per il lease del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-189">The time_elapsed input is applied to the time remaining on DHCP Client lease.</span></span>

<span data-ttu-id="5663b-190">A tale scopo, è necessario che l'applicazione client DHCP abbia creato un record del client DHCP prima dell'accensione e abbia salvato tale record nella memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="5663b-190">This requires that the DHCP Client application created a record of the DHCP Client before powering down, and saved that record to nonvolatile memory.</span></span>

<span data-ttu-id="5663b-191">Se è abilitata più di un'interfaccia per il client DHCP, questo servizio viene applicato alla prima interfaccia valida presente nell'istanza del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-191">If more than one interface is enabled for DHCP Client, this service is applied to the first valid interface found in the DHCP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5663b-192">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5663b-192">Input Parameters</span></span>

- <span data-ttu-id="5663b-193">**dhcp_ptr** Puntatore al client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-193">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="5663b-194">**record_ptr** Puntatore al record client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-194">**record_ptr** Pointer to DHCP Client record</span></span>

- <span data-ttu-id="5663b-195">**time_elapsed** Tempo di sottrazione dal tempo di lease rimanente nel record client di input</span><span class="sxs-lookup"><span data-stu-id="5663b-195">**time_elapsed** Time to subtract from the lease time remaining in the input client record</span></span>

### <a name="return-values"></a><span data-ttu-id="5663b-196">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5663b-196">Return Values</span></span>

- <span data-ttu-id="5663b-197">Record client di **NX_SUCCESS** (0x0) ripristinato</span><span class="sxs-lookup"><span data-stu-id="5663b-197">**NX_SUCCESS** (0x0) Client record restored</span></span>

- <span data-ttu-id="5663b-198">Client di **NX_DHCP_NOT_BOUND** (0x94) non associato all'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="5663b-198">**NX_DHCP_NOT_BOUND** (0x94) Client not bound to IP address</span></span>

- <span data-ttu-id="5663b-199">Indice di interfaccia **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0X9A) non valido</span><span class="sxs-lookup"><span data-stu-id="5663b-199">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) Invalid interface index</span></span>

- <span data-ttu-id="5663b-200">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="5663b-200">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="5663b-201">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="5663b-201">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5663b-202">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5663b-202">Allowed From</span></span>

<span data-ttu-id="5663b-203">Thread</span><span class="sxs-lookup"><span data-stu-id="5663b-203">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5663b-204">Esempio</span><span class="sxs-lookup"><span data-stu-id="5663b-204">Example</span></span>

```C
NX_DHCP_CLIENT_RECORD dhcp_record;
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
Time_elapsed = /* to be determined by application */ 1000; 


/* Obtain a record of the current client state on the primary interface. */
status=  nx_dhcp_interface_client_restore_record(client_ptr, 0, &dhcp_record, time_elapsed);

/* If status is NX_SUCCESS the current DHCP Client pointed to by dhcp_ptr  
   contains the current client record updated for time elapsed during power down. */
```

## <a name="nx_dhcp_-client_update_time_remaining"></a><span data-ttu-id="5663b-205">nx_dhcp_ client_update_time_remaining</span><span class="sxs-lookup"><span data-stu-id="5663b-205">nx_dhcp_ client_update_time_remaining</span></span>

<span data-ttu-id="5663b-206">Aggiornare il tempo rimanente per il lease del client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-206">Update the time remaining on DHCP Client lease</span></span>

### <a name="prototype"></a><span data-ttu-id="5663b-207">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5663b-207">Prototype</span></span>

```C
ULONG nx_dhcp_client_update_time_remaining(NX_DHCP *dhcp_ptr
                                           ULONG time_elapsed);
```
### <a name="description"></a><span data-ttu-id="5663b-208">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5663b-208">Description</span></span>

<span data-ttu-id="5663b-209">Questo servizio aggiorna il tempo rimanente per il lease dell'indirizzo IP del client DHCP con l'input time_elapsed sulla prima interfaccia abilitata per DHCP trovato nell'istanza del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-209">This service updates the time remaining on the DHCP Client IP address lease with the time_elapsed input on the first interface enabled for DHCP found on the DHCP Client instance.</span></span> <span data-ttu-id="5663b-210">L'applicazione deve sospendere il thread del client DHCP prima di utilizzare il servizio utilizzando *nx_dhcp_suspend*.</span><span class="sxs-lookup"><span data-stu-id="5663b-210">The application must suspend the DHCP Client thread before using this service using *nx_dhcp_suspend*.</span></span> <span data-ttu-id="5663b-211">Dopo la chiamata a questo servizio, l'applicazione può riprendere il thread del client DHCP chiamando *nx_dhcp_resume*.</span><span class="sxs-lookup"><span data-stu-id="5663b-211">After calling this service, the application can resume the DHCP Client thread by calling *nx_dhcp_resume*.</span></span>

<span data-ttu-id="5663b-212">Questa operazione è destinata alle applicazioni client DHCP che devono sospendere il thread del client DHCP per un determinato periodo di tempo, quindi aggiornare il tempo di lease degli indirizzi IP rimanente.</span><span class="sxs-lookup"><span data-stu-id="5663b-212">This is intended for DHCP Client applications that need to suspend the DHCP Client thread for a period of time, and then update the IP address lease time remaining.</span></span>

> [!NOTE]
> <span data-ttu-id="5663b-213">Questo servizio non deve essere utilizzato con *nx_dhcp_client_get_record* e *nx_dhcp_client_restore_record* descritto in precedenza).</span><span class="sxs-lookup"><span data-stu-id="5663b-213">This service is not intended to be used with *nx_dhcp_client_get_record* and *nx_dhcp_client_restore_record* described previously).</span></span> <span data-ttu-id="5663b-214">Questi servizi sono descritti in precedenza in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="5663b-214">These services are previously described in this section.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5663b-215">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5663b-215">Input Parameters</span></span>

- <span data-ttu-id="5663b-216">**dhcp_ptr** Puntatore al client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-216">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="5663b-217">**time_elapsed** Tempo per la sottrazione dal tempo rimanente per il lease dell'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="5663b-217">**time_elapsed** Time to subtract from the time remaining on the IP address lease</span></span>

### <a name="return-values"></a><span data-ttu-id="5663b-218">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5663b-218">Return Values</span></span>

- <span data-ttu-id="5663b-219">Lease IP client **NX_SUCCESS** (0x0) aggiornato</span><span class="sxs-lookup"><span data-stu-id="5663b-219">**NX_SUCCESS** (0x0) Client IP lease updated</span></span>

- <span data-ttu-id="5663b-220">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) non sono abilitate interfacce per DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-220">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces enabled for DHCP</span></span>

- <span data-ttu-id="5663b-221">**NX_PTR_ERROR** (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5663b-221">**NX_PTR_ERROR** (0x16) Invalid Pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5663b-222">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5663b-222">Allowed From</span></span>

<span data-ttu-id="5663b-223">Thread</span><span class="sxs-lookup"><span data-stu-id="5663b-223">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5663b-224">Esempio</span><span class="sxs-lookup"><span data-stu-id="5663b-224">Example</span></span>

```C
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease. */
status=  nx_dhcp_client_update_time_remaining(client_ptr, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */
```


## <a name="nx_dhcp_interface_client_update_time_remaining"></a><span data-ttu-id="5663b-225">nx_dhcp_interface_client_update_time_remaining</span><span class="sxs-lookup"><span data-stu-id="5663b-225">nx_dhcp_interface_client_update_time_remaining</span></span>

<span data-ttu-id="5663b-226">Aggiornare il tempo rimanente per il lease del client DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="5663b-226">Update the time remaining on DHCP Client lease on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="5663b-227">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5663b-227">Prototype</span></span>

```C
ULONG nx_dhcp_interface_client_update_time_remaining(NX_DHCP *dhcp_ptr,
                                                     UINT interface_index,
                                                     ULONG time_elapsed);
```
### <a name="description"></a><span data-ttu-id="5663b-228">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5663b-228">Description</span></span>

<span data-ttu-id="5663b-229">Questo servizio aggiorna l'ora rimanente del lease di indirizzi IP del client DHCP con l'input time_elapsed sull'interfaccia specificata se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-229">This service updates the time remaining on the DHCP Client IP address lease with the time_elapsed input on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="5663b-230">L'applicazione deve sospendere il thread del client DHCP prima di utilizzare il servizio utilizzando *nx_dhcp_suspend*.</span><span class="sxs-lookup"><span data-stu-id="5663b-230">The application must suspend the DHCP Client thread before using this service using *nx_dhcp_suspend*.</span></span> <span data-ttu-id="5663b-231">Dopo la chiamata a questo servizio, l'applicazione può riprendere il thread del client DHCP chiamando *nx_dhcp_resume*.</span><span class="sxs-lookup"><span data-stu-id="5663b-231">After calling this service, the application can resume the DHCP Client thread by calling *nx_dhcp_resume*.</span></span> <span data-ttu-id="5663b-232">Nota sospendere e riprendere il thread del client DHCP si applica a tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-232">Note suspending and resuming the DHCP Client thread applies to all interfaces enabled for DHCP.</span></span>

<span data-ttu-id="5663b-233">Questa operazione è destinata alle applicazioni client DHCP che devono sospendere il thread del client DHCP per un determinato periodo di tempo, quindi aggiornare il tempo di lease degli indirizzi IP rimanente.</span><span class="sxs-lookup"><span data-stu-id="5663b-233">This is intended for DHCP Client applications that need to suspend the DHCP Client thread for a period of time, and then update the IP address lease time remaining.</span></span>

> [!NOTE] 
> <span data-ttu-id="5663b-234">Questo servizio non deve essere utilizzato con *nx_dhcp_client_get_record* e *nx_dhcp_client_restore_record* descritto in precedenza).</span><span class="sxs-lookup"><span data-stu-id="5663b-234">This service is not intended to be used with *nx_dhcp_client_get_record* and *nx_dhcp_client_restore_record* described previously).</span></span> <span data-ttu-id="5663b-235">Questi servizi sono descritti in precedenza in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="5663b-235">These services are previously described in this section.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5663b-236">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5663b-236">Input Parameters</span></span>

- <span data-ttu-id="5663b-237">**dhcp_ptr** Puntatore al client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-237">**dhcp_ptr** Pointer to DHCP Client</span></span>

- <span data-ttu-id="5663b-238">**interface_index** Indice dell'interfaccia per cui applicare il tempo trascorso</span><span class="sxs-lookup"><span data-stu-id="5663b-238">**interface_index** Index to interface to apply elapsed time to</span></span>

- <span data-ttu-id="5663b-239">**time_elapsed** Tempo per la sottrazione dal tempo rimanente per il lease dell'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="5663b-239">**time_elapsed** Time to subtract from the time remaining on the IP address lease</span></span>

### <a name="return-values"></a><span data-ttu-id="5663b-240">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5663b-240">Return Values</span></span>

- <span data-ttu-id="5663b-241">Lease IP client **NX_SUCCESS** (0x0) aggiornato</span><span class="sxs-lookup"><span data-stu-id="5663b-241">**NX_SUCCESS** (0x0) Client IP lease updated</span></span>

- <span data-ttu-id="5663b-242">Indice di interfaccia **NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0X9A) non valido</span><span class="sxs-lookup"><span data-stu-id="5663b-242">**NX_DHCP_BAD_INTERFACE_INDEX_ERROR** (0x9A) Invalid interface index</span></span>

- <span data-ttu-id="5663b-243">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="5663b-243">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="5663b-244">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="5663b-244">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5663b-245">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5663b-245">Allowed From</span></span>

<span data-ttu-id="5663b-246">Thread</span><span class="sxs-lookup"><span data-stu-id="5663b-246">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5663b-247">Esempio</span><span class="sxs-lookup"><span data-stu-id="5663b-247">Example</span></span>

```C
ULONG       time_elapsed;

/* Obtain time (timer ticks) elapsed from independent time keeper. */
time_elapsed = /* to be determined by application */ 1000; 


/* Apply the elapsed time to the DHCP Client address lease on interface 1. */
status=  nx_dhcp_interface_client_update_time_remaining(client_ptr, 1, time_elapsed);

/* If status is NX_SUCCESS the DHCP Client is updated for time elapsed. */
```


## <a name="nx_dhcp_suspend"></a><span data-ttu-id="5663b-248">nx_dhcp_suspend</span><span class="sxs-lookup"><span data-stu-id="5663b-248">nx_dhcp_suspend</span></span>

<span data-ttu-id="5663b-249">Sospendere il thread del client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-249">Suspend the DHCP Client thread</span></span>

### <a name="prototype"></a><span data-ttu-id="5663b-250">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5663b-250">Prototype</span></span>

```C
ULONG nx_dhcp_suspend(NX_DHCP *dhcp_ptr);
```
### <a name="description"></a><span data-ttu-id="5663b-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5663b-251">Description</span></span>

<span data-ttu-id="5663b-252">Questo servizio sospende il thread del client DHCP corrente.</span><span class="sxs-lookup"><span data-stu-id="5663b-252">This service suspends the current DHCP Client thread.</span></span> <span data-ttu-id="5663b-253">Si noti che, a differenza di *nx_dhcp_stop*, non viene apportata alcuna modifica allo stato del client DHCP quando viene chiamato questo servizio.</span><span class="sxs-lookup"><span data-stu-id="5663b-253">Note that unlike *nx_dhcp_stop*, there is no change to the DHCP Client state when this service is called.</span></span>

<span data-ttu-id="5663b-254">Questo servizio sospende DHCP in esecuzione su tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-254">This service suspends DHCP running on all interfaces enabled for DHCP.</span></span>

<span data-ttu-id="5663b-255">Per aggiornare lo stato del client DHCP con il tempo trascorso mentre il client DHCP è sospeso, vedere la *nx_dhcp_client_update_time_remaining* descritta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5663b-255">To update the DHCP Client state with elapsed time while the DHCP Client is suspended, see the *nx_dhcp_client_update_time_remaining* described previously.</span></span> <span data-ttu-id="5663b-256">Per riprendere un thread client DHCP sospeso, l'applicazione deve chiamare *nx_dhcp_resume*.</span><span class="sxs-lookup"><span data-stu-id="5663b-256">To resume a suspended DHCP Client thread, the application should call *nx_dhcp_resume*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5663b-257">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5663b-257">Input Parameters</span></span>

- <span data-ttu-id="5663b-258">**dhcp_ptr** Puntatore al client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-258">**dhcp_ptr** Pointer to DHCP Client</span></span>

### <a name="return-values"></a><span data-ttu-id="5663b-259">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5663b-259">Return Values</span></span>

- <span data-ttu-id="5663b-260">Thread client di **NX_SUCCESS** (0x0) sospeso</span><span class="sxs-lookup"><span data-stu-id="5663b-260">**NX_SUCCESS** (0x0) Client thread is suspended</span></span>

- <span data-ttu-id="5663b-261">**NX_PTR_ERROR** (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5663b-261">**NX_PTR_ERROR** (0x16) Invalid pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5663b-262">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5663b-262">Allowed From</span></span>

<span data-ttu-id="5663b-263">Thread</span><span class="sxs-lookup"><span data-stu-id="5663b-263">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5663b-264">Esempio</span><span class="sxs-lookup"><span data-stu-id="5663b-264">Example</span></span>

```C
/* Pause the DHCP client thread. */
status=  nx_dhcp_suspend(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is paused. */
```


## <a name="nx_dhcp_resume"></a><span data-ttu-id="5663b-265">nx_dhcp_resume</span><span class="sxs-lookup"><span data-stu-id="5663b-265">nx_dhcp_resume</span></span>

<span data-ttu-id="5663b-266">Riprendere un thread client DHCP sospeso</span><span class="sxs-lookup"><span data-stu-id="5663b-266">Resume a suspended DHCP Client thread</span></span>

### <a name="prototype"></a><span data-ttu-id="5663b-267">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5663b-267">Prototype</span></span>

```C
ULONG nx_dhcp_resume(NX_DHCP *dhcp_ptr);
```
### <a name="description"></a><span data-ttu-id="5663b-268">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5663b-268">Description</span></span>

<span data-ttu-id="5663b-269">Questo servizio riprende un thread client DHCP sospeso.</span><span class="sxs-lookup"><span data-stu-id="5663b-269">This service resumes a suspended DHCP Client thread.</span></span> <span data-ttu-id="5663b-270">Si noti che non viene apportata alcuna modifica allo stato del client DHCP effettivo dopo la ripresa del thread del client.</span><span class="sxs-lookup"><span data-stu-id="5663b-270">Note that there is no change to the actual DHCP Client state after resuming the Client thread.</span></span> <span data-ttu-id="5663b-271">Per aggiornare il tempo rimanente per il lease dell'indirizzo IP del client DHCP con il tempo trascorso prima di chiamare *nx_dhcp_resume*, vedere la *nx_dhcp_client_update_time_remaining* descritta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5663b-271">To update the time remaining on the DHCP Client IP address lease with elapsed time before calling *nx_dhcp_resume*, see the *nx_dhcp_client_update_time_remaining* described previously.</span></span>

<span data-ttu-id="5663b-272">Questo servizio riprende DHCP in esecuzione su tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="5663b-272">This service resumes DHCP running on all interfaces enabled for DHCP.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5663b-273">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5663b-273">Input Parameters</span></span>

- <span data-ttu-id="5663b-274">**dhcp_ptr** Puntatore al client DHCP</span><span class="sxs-lookup"><span data-stu-id="5663b-274">**dhcp_ptr** Pointer to DHCP Client</span></span>

### <a name="return-values"></a><span data-ttu-id="5663b-275">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5663b-275">Return Values</span></span>

- <span data-ttu-id="5663b-276">Il thread client di **NX_SUCCESS** (0x0) viene ripreso</span><span class="sxs-lookup"><span data-stu-id="5663b-276">**NX_SUCCESS** (0x0) Client thread is resumed</span></span>

- <span data-ttu-id="5663b-277">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5663b-277">NX_PTR_ERROR (0x16) Invalid pointer Input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5663b-278">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5663b-278">Allowed From</span></span>

<span data-ttu-id="5663b-279">Thread</span><span class="sxs-lookup"><span data-stu-id="5663b-279">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5663b-280">Esempio</span><span class="sxs-lookup"><span data-stu-id="5663b-280">Example</span></span>

```C
/* Resume the DHCP client thread. */
status=  nx_dhcp_resume(client_ptr);

/* If status is NX_SUCCESS the current DHCP Client thread is resumed. */
```