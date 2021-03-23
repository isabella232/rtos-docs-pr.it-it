---
title: Capitolo 2-installazione e uso del client DHCP RTO NetX duo di Azure
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client DHCP di Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8c3df64be337b557f492617c1ef20adc7c0f8d6e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822028"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-dhcp-client"></a><span data-ttu-id="5b3d0-103">Capitolo 2-installazione e uso del client DHCP RTO NetX duo di Azure</span><span class="sxs-lookup"><span data-stu-id="5b3d0-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo DHCP Client</span></span>

<span data-ttu-id="5b3d0-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client DHCP di Azure RTO NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo DHCP Client component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="5b3d0-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="5b3d0-105">Product Distribution</span></span>

<span data-ttu-id="5b3d0-106">Azure RTO NetX Duo può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/netxduo> .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-106">Azure RTOS NetX Duo can be obtained from our public source code repository at <https://github.com/azure-rtos/netxduo>.</span></span> <span data-ttu-id="5b3d0-107">Il pacchetto include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="5b3d0-107">The package includes the following files:</span></span>

- <span data-ttu-id="5b3d0-108">**nxd_dhcp_client. h**: file di intestazione per NETX Duo DHCP</span><span class="sxs-lookup"><span data-stu-id="5b3d0-108">**nxd_dhcp_client.h**: Header file for NetX Duo DHCP</span></span>
- <span data-ttu-id="5b3d0-109">**nxd_dhcp_client. c**: file di origine c per DHCP NETX Duo</span><span class="sxs-lookup"><span data-stu-id="5b3d0-109">**nxd_dhcp_client.c**: C Source file for DHCP NetX Duo</span></span>
- <span data-ttu-id="5b3d0-110">**nxd_dhcp_client.pdf**: manuale dell'utente per NETX Duo DHCP</span><span class="sxs-lookup"><span data-stu-id="5b3d0-110">**nxd_dhcp_client.pdf**: User Guide for NetX Duo DHCP</span></span> 
    - <span data-ttu-id="5b3d0-111">**demo_netxduo_dhcp. c**: dimostrazione del client DHCP NETX Duo</span><span class="sxs-lookup"><span data-stu-id="5b3d0-111">**demo_netxduo_dhcp.c**: NetX Duo DHCP Client demonstration</span></span>
    - <span data-ttu-id="5b3d0-112">**demo_netxduo_multihome_dhcp_client. c**: dimostrazione del client DHCP NETX duo di DHCP su più interfacce</span><span class="sxs-lookup"><span data-stu-id="5b3d0-112">**demo_netxduo_multihome_dhcp_client.c**: NetX Duo DHCP Client demonstration of DHCP on multiple interfaces</span></span>

## <a name="dhcp-installation"></a><span data-ttu-id="5b3d0-113">Installazione DHCP</span><span class="sxs-lookup"><span data-stu-id="5b3d0-113">DHCP Installation</span></span>

<span data-ttu-id="5b3d0-114">Per usare il client DHCP NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-114">To use NetX Duo DHCP Client, the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="5b3d0-115">Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_dhcp_client. h* e *nxd_dhcp_client. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-115">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the *nxd_dhcp_client.h* and *nxd_dhcp_client.c* files should be copied into this directory.</span></span>

## <a name="using-dhcp"></a><span data-ttu-id="5b3d0-116">Utilizzo di DHCP</span><span class="sxs-lookup"><span data-stu-id="5b3d0-116">Using DHCP</span></span>

<span data-ttu-id="5b3d0-117">L'uso di DHCP per NetX Duo è facile.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-117">Using DHCP for NetX Duo is easy.</span></span> <span data-ttu-id="5b3d0-118">In pratica, il codice dell'applicazione deve includere *nxd_dhcp_client. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-118">Basically, the application code must include *nxd_dhcp_client.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX Duo, respectively.</span></span> <span data-ttu-id="5b3d0-119">Una volta incluso *nxd_dhcp_client. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione DHCP specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-119">Once *nxd_dhcp_client.h* is included, the application code is then able to make the DHCP function calls specified later in this guide.</span></span> <span data-ttu-id="5b3d0-120">Nell'applicazione deve inoltre essere incluso *nxd_dhcp_client. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-120">The application must also include *nxd_dhcp_client.c* in the build process.</span></span> <span data-ttu-id="5b3d0-121">Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-121">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="5b3d0-122">Questo è tutto ciò che è necessario per usare NetX DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-122">This is all that is required to use NetX DHCP.</span></span>

<span data-ttu-id="5b3d0-123">Si noti che poiché DHCP usa i servizi UDP NetX Duo, è necessario abilitare UDP con la chiamata *nx_udp_enable* prima di usare DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-123">Note that since DHCP utilizes NetX Duo UDP services, UDP must be enabled with the *nx_udp_enable* call prior to using DHCP.</span></span>

<span data-ttu-id="5b3d0-124">Per ottenere un indirizzo IP assegnato in precedenza, il client DHCP può avviare il processo DHCP con il messaggio di richiesta e l'opzione 50 "indirizzo IP richiesto" per il server DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-124">To obtain a previously assigned IP address, the DHCP Client can initiate the DHCP process with the Request message and Option 50 “Requested IP Address” to the DHCP Server.</span></span> <span data-ttu-id="5b3d0-125">Il server DHCP risponderà con un messaggio ACK se l'indirizzo IP viene concesso al client o a un NACK se rifiutato.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-125">The DHCP Server will respond with either an ACK message if it grants the IP address to the Client or a NACK if it refuses.</span></span> <span data-ttu-id="5b3d0-126">Nel secondo caso, il client DHCP riavvia il processo DHCP in stato INIT con un messaggio di individuazione e nessun indirizzo IP richiesto.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-126">In the latter case, the DHCP Client restarts the DHCP process at the Init state with a Discover message and no requested IP address.</span></span> <span data-ttu-id="5b3d0-127">L'applicazione host crea innanzitutto il client DHCP, quindi chiama il servizio API *nx_dhcp_request_client_ip* per impostare l'indirizzo IP richiesto prima di avviare il processo DHCP con *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-127">The host application first creates the DHCP Client, then calls the *nx_dhcp_request_client_ip* API service to set the requested IP address before starting the DHCP process with *nx_dhcp_start*.</span></span> <span data-ttu-id="5b3d0-128">Un esempio di applicazione DHCP è disponibile altrove in questo documento per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-128">An example DHCP application is provided elsewhere in this document for more details.</span></span>

## <a name="in-the-bound-state"></a><span data-ttu-id="5b3d0-129">Nello stato associato</span><span class="sxs-lookup"><span data-stu-id="5b3d0-129">In the Bound State</span></span>

<span data-ttu-id="5b3d0-130">Mentre il client DHCP è nello stato associato, il thread del client DHCP elabora lo stato del client una volta per ogni intervallo (come specificato da NX_DHCP_TIME_INTERVAL) e decrementa il tempo rimanente nel lease IP assegnato al client.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-130">While the DHCP Client is in the bound state, the DHCP Client thread processes the Client state once per interval (as specified by NX_DHCP_TIME_INTERVAL) and decrements the time remaining on the IP lease assigned to the Client.</span></span> <span data-ttu-id="5b3d0-131">Quando il tempo di rinnovo è scaduto, lo stato del client DHCP viene aggiornato allo stato di rinnovo in cui il client richiederà un rinnovo dal server DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-131">When the renewal time has elapsed the DHCP Client state is updated to the RENEW state where the Client will request a renewal from the DHCP Server.</span></span>

## <a name="sending-dhcp-messages-to-the-server"></a><span data-ttu-id="5b3d0-132">Invio di messaggi DHCP al server</span><span class="sxs-lookup"><span data-stu-id="5b3d0-132">Sending DHCP Messages To The Server</span></span>

<span data-ttu-id="5b3d0-133">Il client DHCP dispone di servizi API che consentono all'applicazione host di inviare un messaggio al server DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-133">The DHCP Client has API services that allow the host application to send a message to the DHCP Server.</span></span> <span data-ttu-id="5b3d0-134">Si noti che questi servizi non sono destinati all'applicazione host per eseguire manualmente il protocollo client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-134">Note these services are NOT intended for the host application to manually run the DHCP Client protocol.</span></span>

  - <span data-ttu-id="5b3d0-135">*nx_dhcp_release*: Invia un messaggio di rilascio al server quando l'applicazione host lascia la rete o deve rinunciare all'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-135">*nx_dhcp_release*: this sends a RELEASE message to the Server when the host application is either leaving the network or needs relinquish its IP address.</span></span>
  - <span data-ttu-id="5b3d0-136">*nx_dhcp_decline*: Invia un messaggio di rifiuto al server se l'applicazione host determina indipendentemente dal client DHCP che l'indirizzo IP è già in uso.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-136">*nx_dhcp_decline*: this sends a DECLINE message to the Server if the host application determines independently of the DHCP Client that its IP address is already in use.</span></span>
  - <span data-ttu-id="5b3d0-137">*nx_dhcp_forcerenew*: Invia un messaggio Forcerenew al server</span><span class="sxs-lookup"><span data-stu-id="5b3d0-137">*nx_dhcp_forcerenew*: this sends a FORCERENEW message to the Server</span></span>
  - <span data-ttu-id="5b3d0-138">*nx_dhcp_send_request*: accetta come argomento un tipo di messaggio DHCP, come specificato in *nxd_dhcp_client. h*, e invia il messaggio al server.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-138">*nx_dhcp_send_request*: This takes as an argument a DHCP message type, as specified in *nxd_dhcp_client.h*, and sends the message to the Server.</span></span> <span data-ttu-id="5b3d0-139">Questa operazione viene utilizzata principalmente per l'invio del messaggio di notifica DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-139">This is intended primarily for sending the DHCP INFORM message.</span></span>

<span data-ttu-id="5b3d0-140">Per ulteriori informazioni su questi servizi, vedere la [Descrizione dei servizi DHCP](chapter3.md)</span><span class="sxs-lookup"><span data-stu-id="5b3d0-140">See [Description of DHCP Services](chapter3.md) for more information about these services</span></span> 

## <a name="starting-and-stopping-the-dhcp-client"></a><span data-ttu-id="5b3d0-141">Avvio e arresto del client DHCP</span><span class="sxs-lookup"><span data-stu-id="5b3d0-141">Starting and Stopping the DHCP Client</span></span>

<span data-ttu-id="5b3d0-142">Per arrestare il client DHCP, indipendentemente dal fatto che abbia raggiunto uno stato associato, l'applicazione host chiama *nx_dhcp_stop*.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-142">To stop the DHCP Client, regardless if it has achieved a bound state, the host application calls *nx_dhcp_stop*.</span></span>

<span data-ttu-id="5b3d0-143">Per riavviare un client DHCP, l'applicazione host deve prima arrestare il client DHCP utilizzando il servizio *nx_dhcp_stop* descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-143">To restart a DHCP Client, the host application must first stop the DHCP Client using the *nx_dhcp_stop* service described above.</span></span> <span data-ttu-id="5b3d0-144">L'host può quindi chiamare *nx_dhcp_start* per riprendere il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-144">Then the host can call *nx_dhcp_start* to resume the DHCP Client.</span></span> <span data-ttu-id="5b3d0-145">Se l'applicazione host desidera cancellare un profilo client DHCP precedente, ad esempio uno ottenuto da un server DHCP precedente in un'altra rete, l'applicazione host deve chiamare *nx_dhcp_reinitialize* per eseguire internamente questa attività prima di chiamare *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-145">If the host application wishes to clear a previous DHCP Client profile, for example, one obtained from a previous DHCP Server on another network, the host application should call *nx_dhcp_reinitialize* to perform this task internally before calling *nx_dhcp_start*.</span></span>

<span data-ttu-id="5b3d0-146">Una sequenza tipica potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="5b3d0-146">A typical sequence might be:</span></span>

```c
nx_dhcp_stop(&my_dhcp);
nx_dhcp_reinitialize(&my_dhcp);
nx_dhcp_start(&my_dhcp);
```

<span data-ttu-id="5b3d0-147">Per le applicazioni DHCP in esecuzione su una sola interfaccia DHCP, l'arresto del client DHCP disattiva anche il timer del CLIENT DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-147">For DHCP applications running on only a single DHCP interface, stopping the DHCP Client also inactivates the DHCP CLIENT timer.</span></span> <span data-ttu-id="5b3d0-148">Quindi non tiene più traccia del tempo rimanente nel lease IP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-148">Thus it is no longer keeping track of the time remaining on the IP lease.</span></span> <span data-ttu-id="5b3d0-149">L'arresto del client DHCP su una particolare interfaccia non attiverà il timer del client DHCP, ma arresterà gli aggiornamenti del timer fino al tempo rimanente nel lease IP su tale interfaccia</span><span class="sxs-lookup"><span data-stu-id="5b3d0-149">Stopping DHCP Client on a particular interface will not inactivate the DHCP Client timer but will stop timer updates to the time remaining on the IP lease on that interface</span></span>

<span data-ttu-id="5b3d0-150">Pertanto, non è consigliabile arrestare il client DHCP, a meno che l'applicazione host non richieda il riavvio o il cambio di rete.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-150">Therefore, stopping the DHCP Client is not advised unless the host application requires rebooting or switching networks.</span></span>

## <a name="using-the-dhcp-client-with-auto-ip"></a><span data-ttu-id="5b3d0-151">Uso del client DHCP con IP automatico</span><span class="sxs-lookup"><span data-stu-id="5b3d0-151">Using the DHCP Client with Auto IP</span></span>

<span data-ttu-id="5b3d0-152">Il client DHCP NetX Duo funziona simultaneamente con il protocollo IP automatico nelle applicazioni in cui DHCP e IP automatico garantiscono un indirizzo in cui non è garantito che un server DHCP sia disponibile o non risponde.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-152">The NetX Duo DHCP Client works concurrently with the Auto IP protocol in applications where DHCP and Auto IP guarantee an address where a DHCP Server is not guaranteed to be available or responding.</span></span> <span data-ttu-id="5b3d0-153">Tuttavia, se l'host non è in grado di rilevare un server o di ottenere un indirizzo IP assegnato, può passare al protocollo IP automatico per un indirizzo IP locale.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-153">However, If the host is unable to detect a Server or get an IP address assigned, it can switch to the Auto IP protocol for a local IP address.</span></span> <span data-ttu-id="5b3d0-154">Tuttavia, prima di procedere, è consigliabile arrestare temporaneamente il client DHCP mentre l'IP automatico passa attraverso le fasi "probe" e "Defense".</span><span class="sxs-lookup"><span data-stu-id="5b3d0-154">However before doing so, it is advisable to stop the DHCP Client temporarily while Auto IP goes through the “probe” and “defense” stages.</span></span> <span data-ttu-id="5b3d0-155">Quando un indirizzo IP automatico viene assegnato all'host, il client DHCP può essere riavviato e se un server DHCP diventa disponibile, l'indirizzo IP host può accettare l'indirizzo IP offerto dal server DHCP mentre l'applicazione è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-155">Once an Auto IP address is assigned to the host, the DHCP Client can be restarted and if a DHCP Server does become available, the host IP address can accept the IP address offered by the DHCP Server while the application is running.</span></span>

<span data-ttu-id="5b3d0-156">L'IP automatico di NetX Duo dispone di una notifica di modifica dell'indirizzo per l'host per monitorare le attività in caso di modifica di un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-156">The NetX Duo Auto IP has an address change notification for the host to monitor its activities in the event of an IP address change.</span></span>

## <a name="packet-chaining"></a><span data-ttu-id="5b3d0-157">Concatenamento di pacchetti</span><span class="sxs-lookup"><span data-stu-id="5b3d0-157">Packet Chaining</span></span>

<span data-ttu-id="5b3d0-158">Per un uso più efficiente delle risorse di memoria e pool di pacchetti, il client DHCP è in grado di gestire i pacchetti concatenati in ingresso (datagrammi che superano la MTU del driver) dal driver Ethernet.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-158">For more efficient use of packet pool and memory resources, the DHCP Client can handle incoming chained packets (datagrams exceeding the driver MTU) from the Ethernet driver.</span></span> <span data-ttu-id="5b3d0-159">Se il driver ha questa funzionalità, l'applicazione può impostare il pool di pacchetti per la ricezione di pacchetti al di sotto dei NX_DHCP_PACKET_PAYLOAD byte obbligatori.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-159">If the driver has this capability, the application can set the packet pool for receiving packets to below the mandatory NX_DHCP_PACKET_PAYLOAD bytes.</span></span> <span data-ttu-id="5b3d0-160">NX_DHCP_PACKET_PAYLOAD deve contenere il frame della rete fisica (in genere Ethernet), più 548 byte di dati del messaggio DHCP e IP e UDP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-160">NX_DHCP_PACKET_PAYLOAD should accommodate the physical network (typically Ethernet) frame, plus 548 bytes of DHCP message data, and IP and UDP.</span></span>

<span data-ttu-id="5b3d0-161">Si noti che l'applicazione può ottimizzare il payload del pacchetto e il numero di pacchetti nel pool di pacchetti che fa parte del client DHCP e che viene usato per l'invio di messaggi DHCP. Può ottimizzare le dimensioni in base all'utilizzo previsto e alle dimensioni dei messaggi del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-161">Note that the application can optimize the packet payload and number of packets in the packet pool that is part of the DHCP Client, and which is used for sending DHCP messages out. It can optimize the size based on expected usage and size of the DHCP Client messages.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="5b3d0-162">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="5b3d0-162">Small Example System</span></span>

<span data-ttu-id="5b3d0-163">Un esempio di come usare NetX Duo è illustrato nella figura 1,1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-163">An example of how to use NetX Duo is shown in Figure 1.1 below.</span></span> <span data-ttu-id="5b3d0-164">La funzione di immissione del thread dell'applicazione "*my_thread_entry*" viene creata alla riga 101.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-164">The application thread entry function “*my_thread_entry*” is created at line 101.</span></span> <span data-ttu-id="5b3d0-165">Al termine della creazione, l'elaborazione DHCP viene avviata con la chiamata *nx_dhcp_start* alla riga 108.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-165">After successful creation, DHCP processing is initiated with the *nx_dhcp_start* call at line 108.</span></span> <span data-ttu-id="5b3d0-166">A questo punto, l'attività thread client DHCP tenta di contattare un server DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-166">At this point, the DHCP Client thread task separately attempts to contact a DHCP server.</span></span> <span data-ttu-id="5b3d0-167">Durante questo processo, il codice dell'applicazione attende che un indirizzo IP valido venga registrato con l'istanza IP usando il servizio *nx_ip_status_check* (o *nx_ip_interface_status_check* per un'interfaccia secondaria) alla riga 95.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-167">During this process, the application code waits for a valid IP address to be registered with the IP instance using the *nx_ip_status_check* service (or *nx_ip_interface_status_check* for a secondary interface) on line 95.</span></span> <span data-ttu-id="5b3d0-168">Questa operazione viene in genere eseguita in un ciclo con un'opzione di attesa più breve.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-168">This is more commonly done in a loop with a shorter wait option.</span></span>

<span data-ttu-id="5b3d0-169">Dopo la riga 127, DHCP ha ricevuto un indirizzo IP valido e l'applicazione può continuare, usando i servizi TCP/IP di NetX Duo nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-169">After line 127, DHCP has received a valid IP address and the application can then proceed, utilizing NetX Duo TCP/IP services as desired.</span></span>

```c
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nxd_dhcp_client.h"

#define     DEMO_STACK_SIZE         4096
TX_THREAD               my_thread;
NX_PACKET_POOL          my_pool;
NX_IP                   my_ip;
NX_DHCP                 my_dhcp;

/* Define function prototypes.  */

void    my_thread_entry(ULONG thread_input);
void    my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point.  */
intmain()
{
  /* Enter the ThreadX kernel.  */
  tx_kernel_enter();
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

CHAR    *pointer;
UINT    status;
    
    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;

    /* Create “my_thread”.  */
      tx_thread_create(&my_thread, "my thread", my_thread_entry, 0,  
                        pointer, DEMO_STACK_SIZE, 2, 2, 
                        TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX Duo system.  */
    nx_system_initialize();

    /* Create a packet pool.  */
    status =  nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                                     1024, pointer, 64000);
    pointer = pointer + 64000;

    /* Check for pool creation error.  */
    if (status)
        error_counter++;

    /* Create an IP instance without an IP address. */
    status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
                          0xFFFFFF00, &my_pool, my_netx_driver, pointer, 
                          DEMO_STACK_SIZE, 1);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for IP create errors.  */
    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for my IP Instance.  */
    status =  nx_arp_enable(&my_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors.  */
    if (status)
        error_counter++;

    /* Enable UDP.  */
    status =  nx_udp_enable(&my_ip);
    if (status)
        error_counter++;
 }


 /* Define my thread.  */

 void    my_thread_entry(ULONG thread_input)
 {

 UINT        status;
 ULONG       actual_status;
 NX_PACKET   *my_packet;

    /* Wait for the link to come up.  */
    do
    {
    /* Get the link status.  */
        status =  nx_ip_status_check(&my_ip, NX_IP_LINK_ENABLED, 
                                     &actual_status, 100);
    } while (status != NX_SUCCESS);

    /* Create a DHCP instance.  */
    status =  nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

    /* Check for DHCP create error.  */
    if (status)
        error_counter++;

    /* Start DHCP.  */
    nx_dhcp_start(&my_dhcp);

    /* Check for DHCP start error.  */
    if (status)
        error_counter++;

    /* Wait for IP address to be resolved through DHCP.  */
    nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                       (ULONG *) &status, 100000);

    /* Check to see if we have a valid IP address.  */
    if (status)
    {
      error_counter++;
      return;
    }
    else
    {

  /* Yes, a valid IP address is now on lease…  All NetX Duo
        services are available.
    }
 }

```
## <a name="multi-server-environments"></a><span data-ttu-id="5b3d0-170">Ambienti multiserver</span><span class="sxs-lookup"><span data-stu-id="5b3d0-170">Multi-Server Environments</span></span>

<span data-ttu-id="5b3d0-171">Nelle reti in cui è presente più di un server DHCP, il client DHCP accetta il primo messaggio di offerta server DHCP ricevuto, avanza sullo stato della richiesta e ignora le altre offerte ricevute.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-171">On networks where there is more than one DHCP Server, the DHCP Client accepts the first received DHCP Server Offer message, advances to the Request state, and ignores any other received offers.</span></span>

## <a name="arp-probes"></a><span data-ttu-id="5b3d0-172">Probe ARP</span><span class="sxs-lookup"><span data-stu-id="5b3d0-172">ARP Probes</span></span>

<span data-ttu-id="5b3d0-173">Il client DHCP può essere configurato in modo da inviare uno o più Probe ARP dopo l'assegnazione di indirizzi IP dal server DHCP per verificare che l'indirizzo IP non sia già in uso.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-173">The DHCP Client can be configured to send one or more ARP probes after IP address assignment from the DHCP Server to verify the IP address is not already in use.</span></span> <span data-ttu-id="5b3d0-174">Il passaggio del probe ARP è consigliato da RFC 2131 ed è particolarmente importante in ambienti con più di un server DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-174">The ARP probe step is recommended by RFC 2131 and is particularly important in environments with more than one DHCP Server.</span></span> <span data-ttu-id="5b3d0-175">Se l'applicazione host abilita l'opzione NX_DHCP_CLIENT_SEND_ARP_PROBE (vedere le **Opzioni di configurazione** nel capitolo due per le opzioni aggiuntive del probe ARP), il client DHCP invierà un probe ARP "autoindirizzato" e aspetterà il tempo specificato per una risposta.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-175">If the host application enables the NX_DHCP_CLIENT_SEND_ARP_PROBE option (see **Configuration Options** in Chapter Two for additional ARP probe options), the DHCP Client will send a ‘self addressed’ ARP probe and wait for the specified time for a response.</span></span> <span data-ttu-id="5b3d0-176">Se non viene ricevuto alcun valore, il client DHCP passa allo stato associato.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-176">If none is received, the DHCP Client advances to the Bound state.</span></span> <span data-ttu-id="5b3d0-177">Se viene ricevuta una risposta, il client DHCP presuppone che l'indirizzo sia già in uso.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-177">If a response is received, the DHCP Client assumes the address is already in use.</span></span> <span data-ttu-id="5b3d0-178">Invia automaticamente un messaggio di rifiuto al server e reinizializza il client per riavviare i probe DHCP dallo stato INIT.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-178">It automatically sends a DECLINE message to the Server, and reinitializes the Client to restart the DHCP probes again from the INIT state.</span></span> <span data-ttu-id="5b3d0-179">Viene riavviata la macchina a stati DHCP e il client invia un altro messaggio di individuazione al server.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-179">This restarts the DHCP state machine and the Client sends another DISCOVER message to the Server.</span></span>

## <a name="bootp-protocol"></a><span data-ttu-id="5b3d0-180">Protocollo BOOTP</span><span class="sxs-lookup"><span data-stu-id="5b3d0-180">BOOTP Protocol</span></span>

<span data-ttu-id="5b3d0-181">Il client DHCP supporta anche il protocollo BOOTP e il protocollo DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-181">The DHCP Client also supports the BOOTP protocol as well the DHCP protocol.</span></span> <span data-ttu-id="5b3d0-182">Per abilitare questa opzione e utilizzare BOOTP anziché DHCP, l'applicazione host deve impostare l'opzione di configurazione NX_DHCP_BOOTP_ENABLE.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-182">To enable this option and use BOOTP instead of DHCP, the host application must set the NX_DHCP_BOOTP_ENABLE configuration option.</span></span> <span data-ttu-id="5b3d0-183">L'applicazione host può comunque richiedere indirizzi IP specifici nel protocollo BOOTP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-183">The host application can still request specific IP addresses in the BOOTP protocol.</span></span> <span data-ttu-id="5b3d0-184">Tuttavia, il client DHCP non supporta il caricamento del sistema operativo host, perché a volte viene usato BOOTP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-184">However, the DHCP Client does not support loading the host operating system as BOOTP is sometimes used to do.</span></span>

## <a name="dhcp-on-a-secondary-interface"></a><span data-ttu-id="5b3d0-185">DHCP in un'interfaccia secondaria</span><span class="sxs-lookup"><span data-stu-id="5b3d0-185">DHCP on a Secondary Interface</span></span>

<span data-ttu-id="5b3d0-186">Il client DHCP NetX Duo può essere eseguito su interfacce secondarie anziché sull'interfaccia primaria predefinita.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-186">The NetX Duo DHCP Client can run on secondary interfaces rather than the default primary interface.</span></span>

<span data-ttu-id="5b3d0-187">Per eseguire il client DHCP NetX Duo in un'interfaccia di rete secondaria, l'applicazione host deve impostare l'indice di interfaccia del client DHCP sull'interfaccia secondaria usando il servizio API *nx_dhcp_set_interface_index* .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-187">To run NetX Duo DHCP Client on a secondary network interface, the host application must set the interface index of the DHCP Client to the secondary interface using the *nx_dhcp_set_interface_index* API service.</span></span> <span data-ttu-id="5b3d0-188">L'interfaccia deve essere già collegata all'interfaccia di rete primaria usando il servizio *nx_ip_interface_attach* .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-188">The interface must already be attached to the primary network interface using the *nx_ip_interface_attach* service.</span></span> <span data-ttu-id="5b3d0-189">Per ulteriori informazioni sul fissaggio delle interfacce secondarie, vedere la guida dell'utente di NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-189">See the NetX Duo User Guide for more details on attaching secondary interfaces.</span></span>

<span data-ttu-id="5b3d0-190">Di seguito è riportato un sistema di esempio (Figura 1,2) in cui l'applicazione host si connette al server DHCP sull'interfaccia secondaria.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-190">Below is an example system (Figure 1.2) in which the host application connects to the DHCP server on its secondary interface.</span></span> <span data-ttu-id="5b3d0-191">Alla riga 65, l'interfaccia secondaria è collegata all'attività IP con un indirizzo IP null.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-191">On line 65, the secondary interface is attached to the IP task with a null IP address.</span></span> <span data-ttu-id="5b3d0-192">Alla riga 104, dopo la creazione dell'istanza del client DHCP, l'indice dell'interfaccia client DHCP viene impostato su 1 (ad esempio, l'offset dall'interfaccia principale, ovvero l'indice 0), chiamando *nx_dhcp_set_interface_index*.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-192">On line 104, after the DHCP Client instance is created, the DHCP Client interface index is set to 1 (e.g. the offset from the primary interface which itself is index 0) by calling *nx_dhcp_set_interface_index*.</span></span> <span data-ttu-id="5b3d0-193">Il client DHCP è quindi pronto per l'avvio nella riga 108.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-193">Then the DHCP Client is ready to be started in line 108.</span></span>

```c
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nxd_dhcp_client.h"

#define     DEMO_STACK_SIZE         4096
TX_THREAD               my_thread;
NX_PACKET_POOL          my_pool;
NX_IP                   my_ip;
NX_DHCP                 my_dhcp;

/* Define function prototypes.  */

void    my_thread_entry(ULONG thread_input);
void    my_netx_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point.  */

intmain()
{
  /* Enter the ThreadX kernel.  */
  tx_kernel_enter();
}


/* Define what the initial system looks like.  */

void    tx_application_define(void *first_unused_memory)
{

CHAR    *pointer;
UINT    status;

    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;

    /* Create “my_thread”.  */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0,  
                      pointer, DEMO_STACK_SIZE, 
                      2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX Duo system.  */
    nx_system_initialize();

  /* Create a packet pool.  */
    status =  nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                                     1024, pointer, 64000);
    pointer = pointer + 64000;

    /* Check for pool creation error.  */
    if (status)
        error_counter++;

    /* Create an IP instance without an IP address. */
    status = nx_ip_create(&my_ip, "My NetX IP Instance", IP_ADDRESS(0,0,0,0), 
                           0xFFFFFF00, &my_pool, my_netx_driver, pointer, STACK_SIZE, 1);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for IP create errors.  */
    if (status)
        error_counter++;

    status =  _nx_ip_interface_attach(&ip_0, "port_2", IP_ADDRESS(0, 0, 0,0), 
                                       0xFFFFFF00UL, my_netx_driver);

    /* Enable ARP and supply ARP cache memory for my IP Instance.  */
    status =  nx_arp_enable(&my_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors.  */
    if (status)
        error_counter++;

    /* Enable UDP.  */
    status =  nx_udp_enable(&my_ip);
    if (status)
        error_counter++;
}


void    my_thread_entry(ULONG thread_input)
{

UINT        status;
ULONG       status;
NX_PACKET   *my_packet;

    /* Wait for the link to come up.  */
    do
    {
      /* Get the link status.  */
        status =  nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,& status,100);
    } while (status != NX_SUCCESS);

    /* Create a DHCP instance.  */
    status =  nx_dhcp_create(&my_dhcp, &my_ip, "My DHCP");

    /* Check for DHCP create error.  */
    if (status)
        error_counter++;

    /* Set the DHCP client interface to the secondary interface. */
    status = nx_dhcp_set_interface_index(&my_dhcp, 1);


    /* Start DHCP.  */
    nx_dhcp_start(&my_dhcp);

    /* Check for DHCP start error.  */
    if (status)
        error_counter++;

    /* Wait for IP address to be resolved through DHCP.  */
    nx_ip_status_check(&my_ip, NX_IP_ADDRESS_RESOLVED, 
                       (ULONG *) &status, 100000);

    /* Check to see if we have a valid IP address.  */
    if (status)
    {
        error_counter++;
        return;
    }
    else
    {
    /* Yes, a valid IP address is now on lease…  All NetX Duo
        services are available.*/
    }
}
```

## <a name="dhcp-client-on-multiple-interfaces-simultaneously"></a><span data-ttu-id="5b3d0-194">Client DHCP su più interfacce simultaneamente</span><span class="sxs-lookup"><span data-stu-id="5b3d0-194">DHCP Client on Multiple Interfaces Simultaneously</span></span>

<span data-ttu-id="5b3d0-195">Per eseguire il client DHCP su più interfacce, NX_MAX_PHYSICAL_INTERFACES in *nx_api. h* deve essere impostato sul numero di interfacce fisiche connesse al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-195">To run DHCP Client on multiple interfaces, NX_MAX_PHYSICAL_INTERFACES in *nx_api.h* must be set to the number of physical interfaces connected to the device.</span></span> <span data-ttu-id="5b3d0-196">Per impostazione predefinita, questo valore è 1 (ad esempio, l'interfaccia primaria).</span><span class="sxs-lookup"><span data-stu-id="5b3d0-196">By default, this value is 1 (e.g. the primary interface).</span></span> <span data-ttu-id="5b3d0-197">Per registrare un'interfaccia aggiuntiva per l'istanza IP, usare il servizio *nx_ip_interface_attach* .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-197">To register an additional interface to the IP instance use the *nx_ip_interface_attach* service.</span></span> <span data-ttu-id="5b3d0-198">Per ulteriori informazioni sul fissaggio delle interfacce secondarie, vedere la guida dell'utente di NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-198">See the NetX Duo User Guide for more details on attaching secondary interfaces.</span></span>

<span data-ttu-id="5b3d0-199">Il passaggio successivo consiste nell'impostare il NX_DHCP_CLIENT_MAX_RECORDS in *nxd_dhcp_client. h* sul numero massimo di interfacce previste per l'esecuzione simultanea di DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-199">The next step is to set the NX_DHCP_CLIENT_MAX_RECORDS in *nxd_dhcp_client.h* to the maximum number of interfaces expected to run DHCP simultaneously.</span></span> <span data-ttu-id="5b3d0-200">Si noti che NX_DHCP_CLIENT_MAX_RECORDS non deve necessariamente essere uguale NX_MAX_PHYSICAL_INTERFACES.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-200">Note that NX_DHCP_CLIENT_MAX_RECORDS does not have to equal NX_MAX_PHYSICAL_INTERFACES.</span></span> <span data-ttu-id="5b3d0-201">Ad esempio, NX_MAX_PHYSICAL_INTERFACES può essere 3 e NX_DHCP_CLIENT_MAX_RECORDS uguale a 2.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-201">For example, NX_MAX_PHYSICAL_INTERFACES can be 3 and NX_DHCP_CLIENT_MAX_RECORDS equal to 2.</span></span> <span data-ttu-id="5b3d0-202">In questa configurazione, solo due interfacce (e possono essere due delle tre interfacce fisiche in qualsiasi momento) delle tre interfacce fisiche possono eseguire DHCP in un momento qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-202">In this configuration, only two interfaces (and they can be any two of the three physical interfaces at any time) of the three physical interfaces can run DHCP at any one time.</span></span> <span data-ttu-id="5b3d0-203">I record client DHCP non dispongono di un mapping uno-a-uno alle interfacce di rete, ad esempio il record client 1 non è correlato automaticamente all'indice di interfaccia fisica 1.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-203">DHCP Client Records do not have a one to one mapping to network interfaces e.g. Client Record 1 does not automatically correlate to physical interface index 1.</span></span>

<span data-ttu-id="5b3d0-204">NX_DHCP_CLIENT_MAX_RECORDS possono anche essere impostate su un valore maggiore di NX_MAX_PHYSICAL_INTERFACES, ma ciò creerebbe record client inutilizzati e sarà un uso inefficiente della memoria.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-204">NX_DHCP_CLIENT_MAX_RECORDS can also be set to greater than NX_MAX_PHYSICAL_INTERFACES but this would create unused client records and be an inefficient use of memory.</span></span>

<span data-ttu-id="5b3d0-205">Prima di poter avviare DHCP su qualsiasi interfaccia, l'applicazione deve abilitare tali interfacce chiamando *nx_dhcp_interface_enable*.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-205">Before it can start DHCP on any interface, the application must enable those interfaces by calling *nx_dhcp_interface_enable*.</span></span> <span data-ttu-id="5b3d0-206">Si noti che l'eccezione è l'interfaccia primaria abilitata automaticamente nella chiamata *nx_dhcp_create* (e che può essere disabilitata usando il servizio *nx_dhcp_interface_disable* illustrato di seguito).</span><span class="sxs-lookup"><span data-stu-id="5b3d0-206">Note that the exception is the primary interface which is automatically enabled in the *nx_dhcp_create* call (and which can be disabled using the *nx_dhcp_interface_disable* service discussed below).</span></span>

<span data-ttu-id="5b3d0-207">In qualsiasi momento, un'interfaccia può essere disabilitata per DHCP o DHCP può essere arrestata in tale interfaccia indipendentemente dalle altre interfacce che eseguono DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-207">At any time, an interface can be disabled for DHCP or DHCP can be stopped on that interface independently of other interfaces running DHCP.</span></span>

<span data-ttu-id="5b3d0-208">Come indicato in precedenza, per abilitare un'interfaccia specifica per DHCP, usare il servizio *nx_dhcp_interface_enable* e specificare l'indice dell'interfaccia fisica nell'argomento di input.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-208">As mentioned above, to enable a specific interface for DHCP, use the *nx_dhcp_interface_enable* service and specify the physical interface index in the input argument.</span></span> <span data-ttu-id="5b3d0-209">È possibile abilitare fino a NX_DHCP_CLIENT_MAX_RECORDS interfacce con l'unica limitazione che l'argomento di input dell'indice di interfaccia sia minore di NX_MAX_PHYSICAL_INTERFACES.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-209">Up to NX_DHCP_CLIENT_MAX_RECORDS interfaces can be enabled with the only limitation that the interface index input argument be less than NX_MAX_PHYSICAL_INTERFACES.</span></span>

<span data-ttu-id="5b3d0-210">Per avviare DHCP in un'interfaccia specifica, usare il servizio *nx_dhcp_interface_start* .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-210">To start DHCP on a specific interface, use the *nx_dhcp_interface_start* service.</span></span> <span data-ttu-id="5b3d0-211">Per avviare DHCP in tutte le interfacce abilitate, usare il servizio *nx_dhcp_start* .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-211">To start DHCP on all enabled interfaces, use the *nx_dhcp_start* service.</span></span> <span data-ttu-id="5b3d0-212">(Le interfacce che hanno già avviato DHCP non saranno interessate da *nx_dhcp_start*).</span><span class="sxs-lookup"><span data-stu-id="5b3d0-212">(Interfaces that have already started DHCP will not be affected by *nx_dhcp_start*.)</span></span>

<span data-ttu-id="5b3d0-213">Per arrestare DHCP in un'interfaccia, usare il servizio *nx_dhcp_interface_stop* .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-213">To stop DHCP on an interface, use the *nx_dhcp_interface_stop* service.</span></span> <span data-ttu-id="5b3d0-214">È necessario che DHCP sia già stato avviato su tale interfaccia o che venga restituito uno stato di errore.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-214">DHCP must already have started on that interface or an error status is returned.</span></span> <span data-ttu-id="5b3d0-215">Per arrestare DHCP in tutte le interfacce abilitate, usare il servizio *nx_dhcp_stop* .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-215">To stop DHCP on all enabled interfaces, use the *nx_dhcp_stop* service.</span></span> <span data-ttu-id="5b3d0-216">DHCP può essere arrestato indipendentemente dalle altre interfacce in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-216">DHCP can be stopped independently of other interfaces at any time.</span></span>

<span data-ttu-id="5b3d0-217">La maggior parte dei servizi client DHCP esistenti ha un equivalente ' Interface ', ad esempio *nx_dhcp_interface_release* è l'equivalente specifico dell'interfaccia di *nx_dhcp_release.*</span><span class="sxs-lookup"><span data-stu-id="5b3d0-217">Most of the existing DHCP Client services have an ‘interface’ equivalent e.g. *nx_dhcp_interface_release* is the interface specific equivalent of *nx_dhcp_release.*</span></span> <span data-ttu-id="5b3d0-218">Se il client DHCP è configurato per una singola interfaccia, eseguirà la stessa operazione.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-218">If DHCP Client is configured for a single interface, they perform the same action.</span></span>

<span data-ttu-id="5b3d0-219">Si noti che i servizi client DHCP non specifici dell'interfaccia si applicano in genere a tutte le interfacce, ma non a tutti.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-219">Note that non-interface specific DHCP Client services typically apply to all interfaces but not all.</span></span> <span data-ttu-id="5b3d0-220">Nel secondo caso, il servizio non specifico dell'interfaccia si applica alla prima interfaccia DHCP abilitata disponibile nella ricerca nell'elenco dei record di interfaccia del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-220">In the latter case, the non-interface specific service applies to the first DHCP enabled interface found in searching the DHCP Client list of interface records.</span></span> <span data-ttu-id="5b3d0-221">Vedere la **Descrizione dei servizi** nel capitolo tre per informazioni sul modo in cui viene eseguito un servizio specifico non di interfaccia quando sono abilitate più interfacce per DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-221">See **Description of Services** in Chapter Three for how a non-interface specific service performs when multiple interfaces are enabled for DHCP.</span></span>

<span data-ttu-id="5b3d0-222">Nella sequenza di esempio riportata di seguito, l'istanza IP dispone di due interfacce di rete e viene eseguita prima DHCP sull'interfaccia secondaria.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-222">In the example sequence below, the IP instance has two network interfaces and first runs DHCP on the secondary interface.</span></span> <span data-ttu-id="5b3d0-223">In un secondo momento, avvia DHCP sull'interfaccia principale.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-223">At some time later, it starts DHCP on the primary interface.</span></span> <span data-ttu-id="5b3d0-224">Rilascia quindi l'indirizzo IP sull'interfaccia primaria e riavvia DHCP sull'interfaccia primaria:</span><span class="sxs-lookup"><span data-stu-id="5b3d0-224">Then it releases the IP address on the primary interface and restarts DHCP on the primary interface:</span></span>

```c
nx_dhcp_create(&my_dhcp_client); /* By default this enables primary interface for DHCP. */

nx_dhcp_interface_enable(&my_dhcp_client, 1); /* Secondary interface is enabled. */

nx_dhcp_interface_start(&my_dhcp_client, 1); /* DHCP is started on secondary interface. */

/* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); /* DHCP is started on primary interface. */

nx_dhcp_interface_release(&my_dhcp_client, 0); /* Some time later… */

nx_dhcp_interface_start(&my_dhcp_client, 0); /* DHCP is restarted on primary interface. */
```

<span data-ttu-id="5b3d0-225">Per un elenco completo dei servizi specifici dell'interfaccia, vedere la **Descrizione dei servizi** nel capitolo tre.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-225">For a complete list of interface specific services see **Description of Services** in Chapter Three.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="5b3d0-226">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="5b3d0-226">Configuration Options</span></span>

<span data-ttu-id="5b3d0-227">Le opzioni DHCP configurabili dall'utente in *nxd_dhcp_client. h* consentono all'applicazione host di ottimizzare il client DHCP in base ai requisiti specifici.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-227">User configurable DHCP options in *nxd_dhcp_client.h* allow the host application to fine tune DHCP Client for its particular requirements.</span></span> <span data-ttu-id="5b3d0-228">Di seguito è riportato un elenco di questi parametri:</span><span class="sxs-lookup"><span data-stu-id="5b3d0-228">The following is a list of these parameters:</span></span>  
  
- <span data-ttu-id="5b3d0-229">**NX_DHCP_ENABLE_BOOTP**: definito, questa opzione Abilita il protocollo BOOTP anziché DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-229">**NX_DHCP_ENABLE_BOOTP**: Defined, this option enables the BOOTP protocol instead of DHCP.</span></span> <span data-ttu-id="5b3d0-230">Per impostazione predefinita, questa opzione è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-230">By default this option is disabled.</span></span>
- <span data-ttu-id="5b3d0-231">**NX_DHCP_CLIENT_RESTORE_STATE**: se definito, consente al client DHCP di salvare lo stato corrente della licenza client DHCP, incluso il tempo rimanente nel lease, e ripristinare lo stato tra il riavvio dell'applicazione client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-231">**NX_DHCP_CLIENT_RESTORE_STATE**: If defined, this enables the DHCP Client to save its current DHCP Client license ‘state’ including time remaining on the lease, and restore this state between DHCP Client application reboots.</span></span> <span data-ttu-id="5b3d0-232">Il valore predefinito è Disattivata.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-232">The default value is disabled.</span></span>
- <span data-ttu-id="5b3d0-233">**NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL**: se impostato, il client DHCP non creerà il proprio pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-233">**NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL**: If set, the DHCP Client will not create its own packet pool.</span></span> <span data-ttu-id="5b3d0-234">Per impostare il pool di pacchetti client DHCP, l'applicazione host deve utilizzare il servizio *nx_dhcp_packet_pool_set* .</span><span class="sxs-lookup"><span data-stu-id="5b3d0-234">The host application must use the *nx_dhcp_packet_pool_set* service to set the DHCP Client packet pool.</span></span> <span data-ttu-id="5b3d0-235">Il valore predefinito è Disattivata.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-235">The default value is disabled.</span></span>
- <span data-ttu-id="5b3d0-236">**NX_DHCP_CLIENT_SEND_ARP_PROBE**: definito, consente al client DHCP di inviare un probe ARP dopo l'assegnazione degli indirizzi IP per verificare che l'indirizzo DHCP assegnato non sia di proprietà di un altro host.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-236">**NX_DHCP_CLIENT_SEND_ARP_PROBE**: Defined, this enables the DHCP Client to send an ARP probe after IP address assignment to verify the assigned DHCP address is not owned by another host.</span></span> <span data-ttu-id="5b3d0-237">Questa opzione è disabilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-237">By default, this option is disabled.</span></span>
- <span data-ttu-id="5b3d0-238">**NX_DHCP_ARP_PROBE_WAIT**: definisce l'intervallo di tempo durante il quale il client DHCP attende una risposta dopo l'invio di un probe ARP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-238">**NX_DHCP_ARP_PROBE_WAIT**: Defines the length of time the DHCP Client waits for a response after sending an ARP probe.</span></span> <span data-ttu-id="5b3d0-239">Il valore predefinito è un secondo (1 \* NX_IP_PERIODIC_RATE)</span><span class="sxs-lookup"><span data-stu-id="5b3d0-239">The default value is one second (1 \* NX_IP_PERIODIC_RATE)</span></span>
- <span data-ttu-id="5b3d0-240">**NX_DHCP_ARP_PROBE_MIN**: definisce la variazione minima nell'intervallo tra l'invio di probe ARP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-240">**NX_DHCP_ARP_PROBE_MIN**: Defines the minimum variation in the interval between sending ARP probes.</span></span> <span data-ttu-id="5b3d0-241">Per impostazione predefinita, il valore viene impostato su 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-241">The value is defaulted to 1 second.</span></span>
- <span data-ttu-id="5b3d0-242">**NX_DHCP_ARP_PROBE_MAX**: definisce la variazione massima nell'intervallo tra l'invio di probe ARP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-242">**NX_DHCP_ARP_PROBE_MAX**: Defines the maximum variation in the interval between sending ARP probes.</span></span> <span data-ttu-id="5b3d0-243">Per impostazione predefinita, il valore viene impostato su 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-243">The value is defaulted to 2 seconds.</span></span>
- <span data-ttu-id="5b3d0-244">**NX_DHCP_ARP_PROBE_NUM**: definisce il numero di probe ARP inviati per determinare se l'indirizzo IP assegnato dal server DHCP è già in uso.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-244">**NX_DHCP_ARP_PROBE_NUM**: Defines the number of ARP probes sent for determining if the IP address assigned by the DHCP server is already in use.</span></span> <span data-ttu-id="5b3d0-245">Per impostazione predefinita, il valore viene impostato su 3 Probe.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-245">The value is defaulted to 3 probes.</span></span>
- <span data-ttu-id="5b3d0-246">**NX_DHCP_RESTART_WAIT**: definisce il periodo di attesa del client DHCP per riavviare DHCP se l'indirizzo IP assegnato al client DHCP è già in uso.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-246">**NX_DHCP_RESTART_WAIT**: Defines the length of time the DHCP Client waits to restart DHCP if the IP address assigned to the DHCP Client is already in use.</span></span> <span data-ttu-id="5b3d0-247">Per impostazione predefinita, il valore viene impostato su 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-247">The value is defaulted to 10 seconds.</span></span>
- <span data-ttu-id="5b3d0-248">**NX_DHCP_CLIENT_MAX_RECORDS**: specifica il numero massimo di record di interfaccia da salvare nell'istanza del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-248">**NX_DHCP_CLIENT_MAX_RECORDS**: Specifies the maximum number of interface records to save to the DHCP Client instance.</span></span> <span data-ttu-id="5b3d0-249">Un record di interfaccia client DHCP è un record del client DHCP in esecuzione su un'interfaccia specifica.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-249">A DHCP Client interface record is a record of the DHCP Client running on a specific interface.</span></span> <span data-ttu-id="5b3d0-250">Il valore predefinito è impostato come numero di interfacce fisiche (NX_MAX_PHYSICAL_INTERFACES).</span><span class="sxs-lookup"><span data-stu-id="5b3d0-250">The default value is set as physical interfaces count(NX_MAX_PHYSICAL_INTERFACES).</span></span>
- <span data-ttu-id="5b3d0-251">**NX_DHCP_CLIENT_SEND_MAX_DHCP_MESSAGE_OPTION**: definito, consente al client DHCP di inviare l'opzione dimensioni massime messaggi DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-251">**NX_DHCP_CLIENT_SEND_MAX_DHCP_MESSAGE_OPTION**: Defined, this enables the DHCP Client to send maximum DHCP message size option.</span></span> <span data-ttu-id="5b3d0-252">Questa opzione è disabilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-252">By default, this option is disabled.</span></span>
- <span data-ttu-id="5b3d0-253">**NX_DHCP_CLIENT_ENABLE_HOST_NAME_CHECK**: definito, consente al client DHCP di controllare il nome host di input nella chiamata nx_dhcp_create per la lunghezza o i caratteri non validi.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-253">**NX_DHCP_CLIENT_ENABLE_HOST_NAME_CHECK**: Defined, this enables the DHCP Client to check the input host name in the nx_dhcp_create call for invalid characters or length.</span></span> <span data-ttu-id="5b3d0-254">Questa opzione è disabilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-254">By default, this option is disabled.</span></span>
- <span data-ttu-id="5b3d0-255">**NX_DHCP_THREAD_PRIORITY**: priorità del thread DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-255">**NX_DHCP_THREAD_PRIORITY**: Priority of the DHCP thread.</span></span> <span data-ttu-id="5b3d0-256">Per impostazione predefinita, questo valore specifica che il thread DHCP viene eseguito con priorità 3.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-256">By default, this value specifies that the DHCP thread runs at priority 3.</span></span>
- <span data-ttu-id="5b3d0-257">**NX_DHCP_THREAD_STACK_SIZE**: dimensioni dello stack di thread DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-257">**NX_DHCP_THREAD_STACK_SIZE**: Size of the DHCP thread stack.</span></span> <span data-ttu-id="5b3d0-258">Per impostazione predefinita, le dimensioni sono pari a 2048 byte.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-258">By default, the size is 2048 bytes.</span></span>
- <span data-ttu-id="5b3d0-259">**NX_DHCP_TIME_INTERVAL**: intervallo in secondi durante il quale viene eseguita la funzione di scadenza del timer del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-259">**NX_DHCP_TIME_INTERVAL**: Interval in seconds when the DHCP Client timer expiration function executes.</span></span> <span data-ttu-id="5b3d0-260">Questa funzione Aggiorna tutti i timeout nel processo DHCP, ad esempio se i messaggi devono essere ritrasmessi o lo stato del client DHCP è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-260">This function updates all the timeouts in the DHCP process e.g. if messages should be retransmitted or DHCP Client state changed.</span></span> <span data-ttu-id="5b3d0-261">Per impostazione predefinita, questo valore è di 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-261">By default, this value is 1 second.</span></span>
- <span data-ttu-id="5b3d0-262">**NX_DHCP_OPTIONS_BUFFER_SIZE**: dimensioni del buffer delle opzioni DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-262">**NX_DHCP_OPTIONS_BUFFER_SIZE**: Size of DHCP options buffer.</span></span> <span data-ttu-id="5b3d0-263">Per impostazione predefinita, questo valore è pari a 312 byte.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-263">By default, this value is 312 bytes.</span></span>
- <span data-ttu-id="5b3d0-264">**NX_DHCP_PACKET_PAYLOAD**: specifica la dimensione in byte del payload del pacchetto client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-264">**NX_DHCP_PACKET_PAYLOAD**: Specifies the size in bytes of the DHCP Client packet payload.</span></span> <span data-ttu-id="5b3d0-265">Il valore predefinito è NX_DHCP_MINIMUM_IP_DATAGRAM + dimensioni dell'intestazione fisica.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-265">The default value is NX_DHCP_MINIMUM_IP_DATAGRAM + physical header size.</span></span> <span data-ttu-id="5b3d0-266">Le dimensioni dell'intestazione fisica in una rete wireline sono in genere le dimensioni del frame Ethernet.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-266">The physical header size in a wireline network is usually the Ethernet frame size.</span></span>
- <span data-ttu-id="5b3d0-267">**NX_DHCP_PACKET_POOL_SIZE**: specifica le dimensioni del pool di pacchetti client DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-267">**NX_DHCP_PACKET_POOL_SIZE**: Specifies the size of the DHCP Client packet pool.</span></span> <span data-ttu-id="5b3d0-268">Il valore predefinito è (5 \* NX_DHCP_PACKET_PAYLOAD), che fornirà quattro pacchetti più spazio per l'overhead interno del pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-268">The default value is (5 \*NX_DHCP_PACKET_PAYLOAD) which will provide four packets plus room for internal packet pool overhead.</span></span>
- <span data-ttu-id="5b3d0-269">**NX_DHCP_MIN_RETRANS_TIMEOUT**: specifica l'opzione di attesa minima per la ricezione di una risposta dal server DHCP al messaggio client prima della ritrasmissione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-269">**NX_DHCP_MIN_RETRANS_TIMEOUT**: Specifies the minimum wait option for receiving a DHCP Server reply to client message before retransmitting the message.</span></span> <span data-ttu-id="5b3d0-270">Il valore predefinito è RFC 2131 consigliato 4 secondi.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-270">The default value is the RFC 2131 recommended 4 seconds.</span></span>
- <span data-ttu-id="5b3d0-271">**NX_DHCP_MAX_RETRANS_TIMEOUT**: specifica l'opzione di attesa massima per la ricezione di una risposta del server DHCP al messaggio client prima della ritrasmissione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-271">**NX_DHCP_MAX_RETRANS_TIMEOUT**: Specifies the maximum wait option for receiving a DHCP Server reply to client message before retransmitting the message.</span></span> <span data-ttu-id="5b3d0-272">Il valore predefinito è 64 secondi.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-272">The default value is 64 seconds.</span></span>
- <span data-ttu-id="5b3d0-273">**NX_DHCP_MIN_RENEW_TIMEOUT**: specifica l'opzione di attesa minima per la ricezione di un messaggio server DHCP e l'invio di una richiesta di rinnovo dopo che il client DHCP è associato a un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-273">**NX_DHCP_MIN_RENEW_TIMEOUT**: Specifies minimum wait option for receiving a DHCP Server message and sending a renewal request after the DHCP Client is bound to an IP address.</span></span> <span data-ttu-id="5b3d0-274">Il valore predefinito è 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-274">The default value is 60 seconds.</span></span> <span data-ttu-id="5b3d0-275">Tuttavia, il client DHCP utilizza il rinnovo e la riassociazione dei tempi di scadenza dal messaggio del server DHCP prima che venga impostato il timeout di rinnovo minimo.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-275">However, the DHCP Client uses the Renew and Rebind expiration times from the DHCP server message before defaulting to the minimum renew timeout.</span></span>
- <span data-ttu-id="5b3d0-276">**NX_DHCP_TYPE_OF_SERVICE**: tipo di servizio necessario per le richieste UDP DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-276">**NX_DHCP_TYPE_OF_SERVICE**: Type of service required for the DHCP UDP requests.</span></span> <span data-ttu-id="5b3d0-277">Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-277">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="5b3d0-278">**NX_DHCP_FRAGMENT_OPTION**: abilitazione del frammento per le richieste UDP DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-278">**NX_DHCP_FRAGMENT_OPTION**: Fragment enable for DHCP UDP requests.</span></span> <span data-ttu-id="5b3d0-279">Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione UDP DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-279">By default, this value is NX_DONT_FRAGMENT to disable DHCP UDP fragmenting.</span></span>
- <span data-ttu-id="5b3d0-280">**NX_DHCP_TIME_TO_LIVE**: specifica il numero di router che questo pacchetto può superare prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-280">**NX_DHCP_TIME_TO_LIVE**: Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="5b3d0-281">Il valore predefinito è impostato su 0x80.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-281">The default value is set to 0x80.</span></span>
- <span data-ttu-id="5b3d0-282">**NX_DHCP_QUEUE_DEPTH**: specifica il numero massimo di profondità della coda di ricezione.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-282">**NX_DHCP_QUEUE_DEPTH**: Specifies the number of maximum depth of receive queue.</span></span> <span data-ttu-id="5b3d0-283">Il valore predefinito è impostato su 4.</span><span class="sxs-lookup"><span data-stu-id="5b3d0-283">The default value is set to 4.</span></span>