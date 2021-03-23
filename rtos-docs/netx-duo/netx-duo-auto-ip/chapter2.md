---
title: Capitolo 2-installazione e uso di Azure RTO NetX Duo AutoIP
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente AutoIP di Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 42c58a4cdec34a03eda9f42315438e5fbe2ea594
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822073"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-autoip"></a><span data-ttu-id="1742b-103">Capitolo 2-installazione e uso di Azure RTO NetX Duo AutoIP</span><span class="sxs-lookup"><span data-stu-id="1742b-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo AutoIP</span></span>

<span data-ttu-id="1742b-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente AutoIP di Azure RTO NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="1742b-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo AutoIP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="1742b-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="1742b-105">Product Distribution</span></span>

<span data-ttu-id="1742b-106">Azure RTO NetX AutoIP può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="1742b-106">Azure RTOS NetX AutoIP can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="1742b-107">Il pacchetto include tre file di origine, uno di inclusione e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1742b-107">The package includes three source files, one include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="1742b-108">**nx_auto_ip. h**: file di intestazione per NETX AutoIP</span><span class="sxs-lookup"><span data-stu-id="1742b-108">**nx_auto_ip.h**: Header file for NetX AutoIP</span></span>
- <span data-ttu-id="1742b-109">**nx_auto_ip. c**: file di origine c per NETX AutoIP</span><span class="sxs-lookup"><span data-stu-id="1742b-109">**nx_auto_ip.c**: C Source file for NetX AutoIP</span></span>
- <span data-ttu-id="1742b-110">**demo_netx_auto_ip. c**: file di origine c per NETX demo AutoIP</span><span class="sxs-lookup"><span data-stu-id="1742b-110">**demo_netx_auto_ip.c**: C Source file for NetX AutoIP Demo</span></span>
- <span data-ttu-id="1742b-111">**nx_auto_ip.pdf**: Descrizione PDF di NETX AutoIP</span><span class="sxs-lookup"><span data-stu-id="1742b-111">**nx_auto_ip.pdf**: PDF description of NetX AutoIP</span></span>

## <a name="autoip-installation"></a><span data-ttu-id="1742b-112">Installazione di AutoIP</span><span class="sxs-lookup"><span data-stu-id="1742b-112">AutoIP Installation</span></span>

<span data-ttu-id="1742b-113">Per poter usare NetX AutoIP, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="1742b-113">In order to use NetX AutoIP, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="1742b-114">Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_auto_ip. h*, *nx_auto_ip. c* e *demo_netx_auto_ip. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="1742b-114">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_auto_ip.h*, *nx_auto_ip.c*, and *demo_netx_auto_ip.c* files should be copied into this directory.</span></span>

## <a name="using-autoip"></a><span data-ttu-id="1742b-115">Uso di AutoIP</span><span class="sxs-lookup"><span data-stu-id="1742b-115">Using AutoIP</span></span>

<span data-ttu-id="1742b-116">L'uso di NetX AutoIP è facile.</span><span class="sxs-lookup"><span data-stu-id="1742b-116">Using NetX AutoIP is easy.</span></span> <span data-ttu-id="1742b-117">In pratica, il codice dell'applicazione deve includere *nx_auto_ip. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter usare threadX e NETX.</span><span class="sxs-lookup"><span data-stu-id="1742b-117">Basically, the application code must include *nx_auto_ip.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX.</span></span> <span data-ttu-id="1742b-118">Una volta incluso *nx_auto_ip. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione AutoIP specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="1742b-118">Once *nx_auto_ip.h* is included, the application code is then able to make the AutoIP function calls specified later in this guide.</span></span> <span data-ttu-id="1742b-119">Nell'applicazione deve inoltre essere incluso *nx_auto_ip. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="1742b-119">The application must also include *nx_auto_ip.c* in the build process.</span></span> <span data-ttu-id="1742b-120">Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1742b-120">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="1742b-121">Questo è tutto ciò che è necessario per usare NetX AutoIP.</span><span class="sxs-lookup"><span data-stu-id="1742b-121">This is all that is required to use NetX AutoIP.</span></span>

> [!NOTE]
> <span data-ttu-id="1742b-122">Poiché AutoIP usa i servizi ARP NetX, è necessario abilitare ARP con la chiamata *nx_arp_enable* prima di usare AutoIP.</span><span class="sxs-lookup"><span data-stu-id="1742b-122">Since AutoIP utilizes NetX ARP services, ARP must be enabled with the *nx_arp_enable* call prior to using AutoIP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="1742b-123">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="1742b-123">Small Example System</span></span>

<span data-ttu-id="1742b-124">Un esempio di come è facile usare NetX AutoIP è descritto nella figura 1,1, riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1742b-124">An example of how easy it is to use NetX AutoIP is described in Figure 1.1, which appears below.</span></span> <span data-ttu-id="1742b-125">In questo esempio, il file di inclusione AutoIP *nx_auto_ip. h* viene portato alla riga 002.</span><span class="sxs-lookup"><span data-stu-id="1742b-125">In this example, the AutoIP include file *nx_auto_ip.h* is brought in at line 002.</span></span> <span data-ttu-id="1742b-126">Successivamente, viene creata l'istanza di NetX AutoIP in "*tx_application_define*" alla riga 090.</span><span class="sxs-lookup"><span data-stu-id="1742b-126">Next, the NetX AutoIP instance is created in "*tx_application_define*" at line 090.</span></span> <span data-ttu-id="1742b-127">Si noti che il blocco di controllo NetX AutoIP "auto_ip_0" è stato definito in precedenza come variabile globale alla riga 015.</span><span class="sxs-lookup"><span data-stu-id="1742b-127">Note that the NetX AutoIP control block "auto_ip_0" was defined previously as a global variable at line 015.</span></span> <span data-ttu-id="1742b-128">Una volta completata la creazione, viene avviato un AutoIP NetX alla riga 098.</span><span class="sxs-lookup"><span data-stu-id="1742b-128">After successful creation, an NetX AutoIP is started at line 098.</span></span> <span data-ttu-id="1742b-129">L'elaborazione della funzione di callback per la modifica dell'indirizzo IP inizia alla riga 105, che viene usata per gestire i conflitti successivi o la possibile risoluzione degli indirizzi DHCP.</span><span class="sxs-lookup"><span data-stu-id="1742b-129">The IP address change callback function processing starts at line 105, which is used to handle subsequent conflicts or possible DHCP address resolution.</span></span>

> [!NOTE]
> <span data-ttu-id="1742b-130">Nell'esempio seguente si presuppone che il dispositivo host sia un dispositivo a Home singolo.</span><span class="sxs-lookup"><span data-stu-id="1742b-130">The example below assumes the host device is a single-homed device.</span></span> <span data-ttu-id="1742b-131">Per un dispositivo multihomed, l'applicazione host può usare il servizio AutoIP NetX *nx_auto_ip_interface_* impostato per specificare un'interfaccia di rete secondaria per verificare la presenza di un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="1742b-131">For a multihomed device, the host application can use the NetX AutoIP service *nx_auto_ip_interface_* set to specify a secondary network interface to probe for an IP address.</span></span> <span data-ttu-id="1742b-132">Per ulteriori informazioni sulla configurazione di applicazioni multihomed, vedere la [Guida dell'utente di NETX](https://docs.microsoft.com/azure/rtos/netx/about-this-guide) .</span><span class="sxs-lookup"><span data-stu-id="1742b-132">See the [NetX User Guide](https://docs.microsoft.com/azure/rtos/netx/about-this-guide) for more details on setting up multihomed applications.</span></span> <span data-ttu-id="1742b-133">Si noti inoltre che l'applicazione host deve usare l'API NetX *nx_status_ip_interface_check* per verificare che AutoIP abbia ottenuto un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="1742b-133">Note further that the host application should use the NetX API *nx_status_ip_interface_check* to verify AutoIP has obtained an IP address.</span></span>

```c
#include "tx_api.h"
#include "nx_api.h"
#include "nx_auto_ip.h"

#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD              thread_0;
NX_PACKET_POOL         pool_0;
NX_IP                  ip_0;

/* Define the AUTO IP structures for the IP instance. */

NX_AUTO_IP             auto_ip_0;

/* Define the counters used in the demo application... */

ULONG                 thread_0_counter;
ULONG                 address_changes;
ULONG                 error_counter;

/* Define thread prototypes. */
void     thread_0_entry(ULONG thread_input);
void     ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{

CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    16, 16, 1, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 128,
                                    pointer, 4096);
    pointer = pointer + 4096;

    if (status)
        error_counter++;

    /* Create an IP instance. */
    status = nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(0, 0, 0, 0),
                        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                        pointer, 4096, 1);
    pointer = pointer + 4096;

    if (status)
        error_counter++;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
        error_counter++;

    /* Create the AutoIP instance for IP Instance 0. */
    status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);
    pointer = pointer + 4096;

    /* Check AutoIP create status. */
    if (status)
        error_counter++;

    /* Start AutoIP instances. */
    status = **nx_auto_ip_start**(&auto_ip_0, 0 /*IP_ADDRESS(169,254,254,255)*/);

    /* Check AutoIP start status. */
    if (status)
        error_counter++;

    /* Register an IP address change function for IP Instance 0. */
    status = nx_ip_address_change_notify(&ip_0, ip_address_changed,
                                        (void *) &auto_ip_0);

    /* Check IP address change notify status. */
    if (status)
        error_counter++;
}

/* Define the test thread. */

void     thread_0_entry(ULONG thread_input)
{

UINT     status;
ULONG    actual_status;

    /* Wait for IP address to be resolved. */
    do
    {

        /* Call IP status check routine. */
        status = nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED,
            &actual_status, 10000);

    } while (status != NX_SUCCESS);

    /* Since the IP address is resolved at this point, the application can now fully utilize NetX! */

    while(1)
    {

        /* Increment thread 0's counter. */
        thread_0_counter++;

        /* Sleep... */
        tx_thread_sleep(10);
    }
}

void          ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address)
{

ULONG         ip_address;
ULONG         network_mask;
NX_AUTO_IP    *auto_ip_ptr;

    /* Setup pointer to auto IP instance. */
    auto_ip_ptr = (NX_AUTO_IP *) auto_ip_address;

    /* Pickup the current IP address. */
    nx_ip_address_get(ip_ptr, &ip_address, &network_mask);

    /* Determine if the IP address has changed back to zero. If so, make sure the AutoIP instance is started. */
    if (ip_address == 0)
    {

        /* Get the last AutoIP address for this node. */
        nx_auto_ip_get_address(auto_ip_ptr, &ip_address);

        /* Start this AutoIP instance. */
        nx_auto_ip_start(auto_ip_ptr, ip_address);
        }

    /* Determine if IP address has transitioned to a non local IP address. */
    else if ((ip_address & 0xFFFF0000UL) != IP_ADDRESS(169, 254, 0, 0))
    {

        /* Stop the AutoIP processing. */
        nx_auto_ip_stop(auto_ip_ptr);
    }

    /* Increment a counter. */
    address_changes++;
}
```

<span data-ttu-id="1742b-134">Figura 1,1 esempio di uso di AutoIP con NetX</span><span class="sxs-lookup"><span data-stu-id="1742b-134">Figure 1.1 Example of AutoIP use with NetX</span></span>

## <a name="configuration-options"></a><span data-ttu-id="1742b-135">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="1742b-135">Configuration Options</span></span>

<span data-ttu-id="1742b-136">Sono disponibili diverse opzioni di configurazione per la compilazione di NetX AutoIP.</span><span class="sxs-lookup"><span data-stu-id="1742b-136">There are several configuration options for building NetX AutoIP.</span></span> <span data-ttu-id="1742b-137">Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="1742b-137">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="1742b-138">**NX_DISABLE_ERROR_CHECKING**: definito, questa opzione rimuove il controllo degli errori di AutoIP di base.</span><span class="sxs-lookup"><span data-stu-id="1742b-138">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic AutoIP error checking.</span></span> <span data-ttu-id="1742b-139">Viene in genere usato dopo il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1742b-139">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="1742b-140">**NX_AUTO_IP_PROBE_WAIT**: numero di secondi di attesa prima dell'invio del primo Probe.</span><span class="sxs-lookup"><span data-stu-id="1742b-140">**NX_AUTO_IP_PROBE_WAIT**: The number of seconds to wait before sending first probe.</span></span> <span data-ttu-id="1742b-141">Per impostazione predefinita, questo valore è definito come 1.</span><span class="sxs-lookup"><span data-stu-id="1742b-141">By default, this value is defined as 1.</span></span>
- <span data-ttu-id="1742b-142">**NX_AUTO_IP_PROBE_NUM**: numero di probe ARP da inviare.</span><span class="sxs-lookup"><span data-stu-id="1742b-142">**NX_AUTO_IP_PROBE_NUM**: The number of ARP probes to send.</span></span> <span data-ttu-id="1742b-143">Per impostazione predefinita, questo valore è definito come 3.</span><span class="sxs-lookup"><span data-stu-id="1742b-143">By default, this value is defined as 3.</span></span>
- <span data-ttu-id="1742b-144">**NX_AUTO_IP_PROBE_MIN**: numero minimo di secondi di attesa tra l'invio di probe.</span><span class="sxs-lookup"><span data-stu-id="1742b-144">**NX_AUTO_IP_PROBE_MIN**: The minimum number of seconds to wait between sending probes.</span></span> <span data-ttu-id="1742b-145">Per impostazione predefinita, questo valore è definito come 1.</span><span class="sxs-lookup"><span data-stu-id="1742b-145">By default, this value is defined as 1.</span></span>
- <span data-ttu-id="1742b-146">**NX_AUTO_IP_PROBE_MAX**: numero massimo di secondi di attesa tra l'invio di probe.</span><span class="sxs-lookup"><span data-stu-id="1742b-146">**NX_AUTO_IP_PROBE_MAX**: The maximum number of seconds to wait between sending probes.</span></span> <span data-ttu-id="1742b-147">Per impostazione predefinita, questo valore è definito come 2.</span><span class="sxs-lookup"><span data-stu-id="1742b-147">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="1742b-148">**NX_AUTO_IP_MAX_CONFLICTS**: numero di conflitti di AutoIP prima di aumentare i ritardi di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="1742b-148">**NX_AUTO_IP_MAX_CONFLICTS**: The number of AutoIP conflicts before increasing processing delays.</span></span> <span data-ttu-id="1742b-149">Per impostazione predefinita, questo valore è definito come 10.</span><span class="sxs-lookup"><span data-stu-id="1742b-149">By default, this value is defined as 10.</span></span>
- <span data-ttu-id="1742b-150">**NX_AUTO_IP_RATE_LIMIT_INTERVAL**: numero di secondi per l'estensione del periodo di attesa quando viene superato il numero totale di conflitti.</span><span class="sxs-lookup"><span data-stu-id="1742b-150">**NX_AUTO_IP_RATE_LIMIT_INTERVAL**: The number of seconds to extend the wait period when the total number of conflicts is exceeded.</span></span> <span data-ttu-id="1742b-151">Per impostazione predefinita, questo valore è definito come 60.</span><span class="sxs-lookup"><span data-stu-id="1742b-151">By default, this value is defined as 60.</span></span>
- <span data-ttu-id="1742b-152">**NX_AUTO_IP_ANNOUNCE_WAIT**: numero di secondi di attesa prima dell'invio dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1742b-152">**NX_AUTO_IP_ANNOUNCE_WAIT**: The number of seconds to wait before sending announcement.</span></span> <span data-ttu-id="1742b-153">Per impostazione predefinita, questo valore è definito come 2.</span><span class="sxs-lookup"><span data-stu-id="1742b-153">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="1742b-154">**NX_AUTO_IP_ANNOUNCE_NUM**: numero di annunci ARP da inviare.</span><span class="sxs-lookup"><span data-stu-id="1742b-154">**NX_AUTO_IP_ANNOUNCE_NUM**: The number of ARP announces to send.</span></span> <span data-ttu-id="1742b-155">Per impostazione predefinita, questo valore è definito come 2.</span><span class="sxs-lookup"><span data-stu-id="1742b-155">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="1742b-156">**NX_AUTO_IP_ANNOUNCE_INTERVAL**: numero di secondi di attesa tra le annunci di invio.</span><span class="sxs-lookup"><span data-stu-id="1742b-156">**NX_AUTO_IP_ANNOUNCE_INTERVAL**: The number of seconds to wait between sending announces.</span></span> <span data-ttu-id="1742b-157">Per impostazione predefinita, questo valore è definito come 2.</span><span class="sxs-lookup"><span data-stu-id="1742b-157">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="1742b-158">**NX_AUTO_IP_DEFEND_INTERVAL**: numero di secondi di attesa tra le annunci di difesa.</span><span class="sxs-lookup"><span data-stu-id="1742b-158">**NX_AUTO_IP_DEFEND_INTERVAL**: The number of seconds to wait between defense announces.</span></span> <span data-ttu-id="1742b-159">Per impostazione predefinita, questo valore è definito come 10.</span><span class="sxs-lookup"><span data-stu-id="1742b-159">By default, this value is defined as 10.</span></span>
