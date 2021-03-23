---
title: Capitolo 2-installazione e uso di Azure RTO NetX Duo BSD
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente BSD di Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 582661bc66c51341fc098de9ff7b6fa2a7d746de
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822058"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-bsd"></a><span data-ttu-id="5d977-103">Capitolo 2-installazione e uso di Azure RTO NetX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo BSD</span></span>

<span data-ttu-id="5d977-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente BSD di Azure RTO NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5d977-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo BSD component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="5d977-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="5d977-105">Product Distribution</span></span>

<span data-ttu-id="5d977-106">È possibile ottenere Azure RTO NetX Duo BSD dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="5d977-106">Azure RTOS NetX Duo BSD can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="5d977-107">Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d977-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="5d977-108">**nxd_bsd. h**: file di intestazione per NETX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-108">**nxd_bsd.h**: Header file for NetX Duo BSD</span></span>
- <span data-ttu-id="5d977-109">**nxd_bsd. c**: file di origine c per NETX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-109">**nxd_bsd.c**: C Source file for NetX Duo BSD</span></span>
- <span data-ttu-id="5d977-110">**nxd_bsd.pdf**: manuale dell'utente per NETX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-110">**nxd_bsd.pdf**: User Guide for NetX Duo BSD</span></span>

<span data-ttu-id="5d977-111">File demo:</span><span class="sxs-lookup"><span data-stu-id="5d977-111">Demo files:</span></span>

- <span data-ttu-id="5d977-112">**bsd_demo_udp. c**</span><span class="sxs-lookup"><span data-stu-id="5d977-112">**bsd_demo_udp.c**</span></span>
- <span data-ttu-id="5d977-113">**bsd_demo_tcp. c**</span><span class="sxs-lookup"><span data-stu-id="5d977-113">**bsd_demo_tcp.c**</span></span>
- <span data-ttu-id="5d977-114">**bsd_demo_raw. c**</span><span class="sxs-lookup"><span data-stu-id="5d977-114">**bsd_demo_raw.c**</span></span>

## <a name="netx-duo-bsd-installation"></a><span data-ttu-id="5d977-115">Installazione di NetX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-115">NetX Duo BSD Installation</span></span>

<span data-ttu-id="5d977-116">Per usare NetX Duo BSD, l'intera distribuzione citata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5d977-116">In order to use NetX Duo BSD the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="5d977-117">Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_bsd. h* e *nxd_bsd. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="5d977-117">For example, if NetX Duo is installed in the directory "*\threadx\arm7\green*" then the *nxd_bsd.h* and *nxd_bsd.c* files should be copied into this directory.</span></span>

## <a name="building-the-threadx-and-netx-duo-components-of-a-bsd-application"></a><span data-ttu-id="5d977-118">Compilazione dei componenti ThreadX e NetX duo di un'applicazione BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-118">Building the ThreadX and NetX Duo components of a BSD Application</span></span>

### <a name="threadx"></a><span data-ttu-id="5d977-119">ThreadX</span><span class="sxs-lookup"><span data-stu-id="5d977-119">ThreadX</span></span>

<span data-ttu-id="5d977-120">La libreria ThreadX deve definire `bsd_errno` nell'archiviazione locale di thread.</span><span class="sxs-lookup"><span data-stu-id="5d977-120">The ThreadX library must define `bsd_errno` in the thread local storage.</span></span> <span data-ttu-id="5d977-121">Si consiglia la seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="5d977-121">We recommend the following procedure:</span></span>

1. <span data-ttu-id="5d977-122">In *tx_port. h*, impostare una delle macro TX_THREAD_EXTENSION come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d977-122">In *tx_port.h*, set one of the TX_THREAD_EXTENSION macros as follows:</span></span>
   - `#define TX_THREAD_EXTENSION_3     int bsd_errno`

1. <span data-ttu-id="5d977-123">Ricompilare la libreria ThreadX.</span><span class="sxs-lookup"><span data-stu-id="5d977-123">Rebuild the ThreadX library.</span></span>

> [!NOTE]
> <span data-ttu-id="5d977-124">Se TX_THREAD_EXTENSION_3 è già in uso, l'utente è libero di usare una delle altre macro TX_THREAD_EXTENSION.</span><span class="sxs-lookup"><span data-stu-id="5d977-124">If TX_THREAD_EXTENSION_3 is already used, the user is free to use one of the other TX_THREAD_EXTENSION macros.</span></span>

### <a name="netx-duo"></a><span data-ttu-id="5d977-125">NetX Duo</span><span class="sxs-lookup"><span data-stu-id="5d977-125">NetX Duo</span></span>

<span data-ttu-id="5d977-126">Prima di usare NetX Duo BSD Services, è necessario compilare la libreria NetX Duo con NX_ENABLE_EXTENDED_NOTIFY_SUPPORT definito.</span><span class="sxs-lookup"><span data-stu-id="5d977-126">Before using NetX Duo BSD Services, the NetX Duo library must be built with NX_ENABLE_EXTENDED_NOTIFY_SUPPORT defined.</span></span> <span data-ttu-id="5d977-127">Per impostazione predefinita, non è definito.</span><span class="sxs-lookup"><span data-stu-id="5d977-127">By default it is not defined.</span></span> <span data-ttu-id="5d977-128">Se è necessario usare i socket raw BSD, è necessario compilare la libreria NetX Duo con NX_ENABLE_IP_RAW_PACKET_FILTER definito.</span><span class="sxs-lookup"><span data-stu-id="5d977-128">If the BSD raw sockets are to be used, the NetX Duo library must be built with NX_ENABLE_IP_RAW_PACKET_FILTER defined.</span></span>

## <a name="using-netx-duo-bsd"></a><span data-ttu-id="5d977-129">Uso di NetX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-129">Using NetX Duo BSD</span></span>

<span data-ttu-id="5d977-130">Un progetto di applicazione NetX Duo BSD deve includere *nxd_bsd. h* dopo aver incluso *tx_api. h* e *nx_api. h* per poter usare i servizi BSD specificati più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="5d977-130">A NetX Duo BSD application project must include *nxd_bsd.h* after it includes *tx_api.h* and *nx_api.h* to be able to use BSD services specified later in this guide.</span></span> <span data-ttu-id="5d977-131">Nell'applicazione deve inoltre essere incluso *nxd_bsd. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="5d977-131">The application must also include *nxd_bsd.c* in the build process.</span></span> <span data-ttu-id="5d977-132">Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d977-132">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="5d977-133">Questo è tutto ciò che è necessario per usare NetX Duo BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-133">This is all that is required to use NetX Duo BSD.</span></span>

<span data-ttu-id="5d977-134">Per usare i servizi BSD di NetX Duo, l'applicazione deve creare un'istanza IP, creare un pool di pacchetti per il livello BSD da cui allocare i pacchetti, allocare spazio di memoria per lo stack dei thread BSD interno e specificare la priorità del thread BSD interno.</span><span class="sxs-lookup"><span data-stu-id="5d977-134">To utilize NetX Duo BSD services, the application must create an IP instance, create a packet pool for the BSD layer to allocate packets from, allocate memory space for the internal BSD thread stack, and specify the priority of the internal BSD thread.</span></span> <span data-ttu-id="5d977-135">Il livello BSD viene inizializzato chiamando *bsd_initialize* e passando i parametri.</span><span class="sxs-lookup"><span data-stu-id="5d977-135">The BSD layer is initialized by calling *bsd_initialize* and passing in the parameters.</span></span> <span data-ttu-id="5d977-136">Questa procedura è illustrata in "piccoli esempi" più avanti in questo documento, ma il prototipo è illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d977-136">This is demonstrated in the "Small Examples" later in this document but the prototype is shown below:</span></span>

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                    *CHAR *bsd_thread_stack_area,
                    *ULONG bsd_thread_stack_size,
                    *UINT bsd_thread_priority*);
```

<span data-ttu-id="5d977-137">Il default_ip è l'istanza IP su cui opera il livello BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-137">The default_ip is the IP instance the BSD layer operates on.</span></span> <span data-ttu-id="5d977-138">Il default_pool viene usato dai servizi BSD per allocare pacchetti da.</span><span class="sxs-lookup"><span data-stu-id="5d977-138">The default_pool is used by the BSD services to allocate packets from.</span></span> <span data-ttu-id="5d977-139">I due parametri successivi: bsd_thread_stack_area, bsd_thread_stack_size definisce l'area dello stack utilizzata dal thread BSD interno e l'ultimo parametro, bsd_thread_priority, imposta la priorità del thread.</span><span class="sxs-lookup"><span data-stu-id="5d977-139">The next two parameters: bsd_thread_stack_area, bsd_thread_stack_size defines the stack area used by the internal BSD thread, and the last parameter, bsd_thread_priority, sets the priority of the thread.</span></span>

## <a name="netx-duo-bsd-raw-socket-support"></a><span data-ttu-id="5d977-140">Supporto di socket raw NetX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-140">NetX Duo BSD Raw Socket Support</span></span>

<span data-ttu-id="5d977-141">NetX Duo BSD supporta anche i socket non elaborati.</span><span class="sxs-lookup"><span data-stu-id="5d977-141">NetX Duo BSD also supports raw sockets.</span></span> <span data-ttu-id="5d977-142">Per usare i socket non elaborati in NetX Duo BSD, è necessario compilare la libreria NetX Duo con NX_ENABLE_IP_RAW_PACKET_FILTER definito.</span><span class="sxs-lookup"><span data-stu-id="5d977-142">To use raw sockets in NetX Duo BSD, the NetX Duo library must be compiled with NX_ENABLE_IP_RAW_PACKET_FILTER defined.</span></span> <span data-ttu-id="5d977-143">Per impostazione predefinita, non è definito.</span><span class="sxs-lookup"><span data-stu-id="5d977-143">By default it is not defined.</span></span> <span data-ttu-id="5d977-144">L'applicazione deve quindi abilitare l'elaborazione socket non elaborata per un'istanza di IP creata in precedenza chiamando *nx_ip_raw_packet_enable.*</span><span class="sxs-lookup"><span data-stu-id="5d977-144">The application must then enable raw socket processing for a previously created IP instance by calling *nx_ip_raw_packet_enable.*</span></span>

<span data-ttu-id="5d977-145">Per creare un socket non elaborato in NetX Duo BSD, l'applicazione usa il *socket* di creazione del servizio socket e specifica la famiglia di protocolli, il tipo di socket e il protocollo:</span><span class="sxs-lookup"><span data-stu-id="5d977-145">To create a raw socket in NetX Duo BSD, the application uses the socket create service *socket* and specifies the protocol family, socket type and protocol:</span></span>

```c
sock_1 = socket(INT protocolFamily, INT socket_type, INT protocol)
```

<span data-ttu-id="5d977-146">protocolFamily è AF_INET per i socket IPv4 o AF_INET6 per i socket IPv6, supponendo che IPv6 sia abilitato nell'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="5d977-146">protocolFamily is AF_INET for IPv4 sockets, or AF_INET6 for IPv6 sockets, assuming IPv6 is enabled on the IP instance.</span></span> <span data-ttu-id="5d977-147">Il socket_type deve essere impostato su SOCK_RAW.</span><span class="sxs-lookup"><span data-stu-id="5d977-147">The socket_type must be set to SOCK_RAW.</span></span> <span data-ttu-id="5d977-148">il protocollo è specifico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d977-148">protocol is application specific.</span></span>

<span data-ttu-id="5d977-149">Per inviare e ricevere pacchetti non elaborati, nonché chiudere un socket non elaborato, l'applicazione usa in genere gli stessi servizi BSD di UDP, ad esempio *SendTo, recvfrom, Select* e *soc_close*.</span><span class="sxs-lookup"><span data-stu-id="5d977-149">To send and receive raw packets as well as close a raw socket, the application typically uses the same BSD services as for UDP e.g. *sendto, recvfrom, select* and *soc_close*.</span></span> <span data-ttu-id="5d977-150">I socket non elaborati non supportano i servizi BSD *Accept* o *Listen* .</span><span class="sxs-lookup"><span data-stu-id="5d977-150">Raw sockets do not support either *accept* or *listen* BSD services.</span></span>

- <span data-ttu-id="5d977-151">Per impostazione predefinita, i dati non elaborati IPv4 ricevuti includono l'intestazione IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d977-151">By default, received IPv4 raw data includes the IPv4 header.</span></span>  <span data-ttu-id="5d977-152">Viceversa, i dati non elaborati IPv6 ricevuti non includono l'intestazione IPv6.</span><span class="sxs-lookup"><span data-stu-id="5d977-152">Conversely, received IPv6 raw data does not include the IPv6 header.</span></span>

- <span data-ttu-id="5d977-153">Per impostazione predefinita, quando si inviano pacchetti IPv6 o IPv4 non elaborati, il livello wrapper BSD aggiunge l'intestazione IPv6 o IPv4 prima di inviare i dati.</span><span class="sxs-lookup"><span data-stu-id="5d977-153">By default, when sending either raw IPv6 or IPv4 packets, the BSD wrapper layer adds the IPv6 or IPv4 header before sending the data.</span></span>

<span data-ttu-id="5d977-154">NetX Duo BSD supporta opzioni di socket non elaborate aggiuntive, tra cui IP_RAW_RX_NO_HEADER, IP_HDRINCL e IP_RAW_IPV6_HDRINCL.</span><span class="sxs-lookup"><span data-stu-id="5d977-154">NetX Duo BSD supports additional raw socket options, including IP_RAW_RX_NO_HEADER, IP_HDRINCL and IP_RAW_IPV6_HDRINCL.</span></span>

<span data-ttu-id="5d977-155">Se IP_RAW_RX_NO_HEADER è impostato, l'intestazione IPv4 viene rimossa in modo che i dati ricevuti non contengano l'intestazione IPv4 e la lunghezza del messaggio segnalata non includa l'intestazione IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d977-155">If IP_RAW_RX_NO_HEADER is set, the IPv4 header is removed so that the received data does not contain the IPv4 header, and the reported message length does not include the IPv4 header.</span></span>  <span data-ttu-id="5d977-156">Per i socket IPv6, per impostazione predefinita la ricezione del socket non elaborato non include l'intestazione IPv6, equivalente al set di opzioni IP_RAW_RX_NO_HEADER.</span><span class="sxs-lookup"><span data-stu-id="5d977-156">For IPv6 sockets, by default the raw socket receive does not include IPv6 header, equivalent to having the IP_RAW_RX_NO_HEADER option set.</span></span> <span data-ttu-id="5d977-157">È possibile che l'applicazione utilizzi il servizio *setsockopt* per deselezionare l'opzione IP_RAW_RX_NO_HEADER, una volta deselezionata l'opzione IP_RAW_RX_NO_HEADER, i dati non elaborati IPv6 ricevuti includono l'intestazione IPv6 e la lunghezza del messaggio segnalata include l'intestazione IPv6.</span><span class="sxs-lookup"><span data-stu-id="5d977-157">Application may use the *setsockopt* service to clear the IP_RAW_RX_NO_HEADER option, Once the IP_RAW_RX_NO_HEADER option is cleared, the received IPv6 raw data would include the IPv6 header, and the reported message length includes the IPv6 header.</span></span>

<span data-ttu-id="5d977-158">Questa opzione non ha alcun effetto sui dati trasmessi IPv4 o IPv6.</span><span class="sxs-lookup"><span data-stu-id="5d977-158">This option has no effect on IPv4 or IPv6 transmitted data.</span></span>

<span data-ttu-id="5d977-159">Se IP_HDRINCL è impostato, l'applicazione include l'intestazione IPv4 quando si inviano i dati.</span><span class="sxs-lookup"><span data-stu-id="5d977-159">If IP_HDRINCL is set, the application includes the IPv4 header when sending data.</span></span>  <span data-ttu-id="5d977-160">Questa opzione non ha alcun effetto sulla trasmissione IPv6 e non è definita per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5d977-160">This option has no effect on IPv6 transmission and is not defined by default.</span></span> <span data-ttu-id="5d977-161">Se IP_RAW_IPV6_HDRINCL è impostato, l'applicazione include l'intestazione IPv6 quando si inviano i dati.</span><span class="sxs-lookup"><span data-stu-id="5d977-161">If IP_RAW_IPV6_HDRINCL is set, the application includes the IPv6 header when sending data.</span></span>  <span data-ttu-id="5d977-162">Questa opzione non ha alcun effetto sulla trasmissione IPv4 e non è definita per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5d977-162">This option has no effect on IPv4 transmission and is not defined by default.</span></span>

<span data-ttu-id="5d977-163">IP_HDRINCL e IP_RAW_IPV6_HDRINCL non hanno alcun effetto sulla ricezione IPv4 o IPv6.</span><span class="sxs-lookup"><span data-stu-id="5d977-163">IP_HDRINCL and IP_RAW_IPV6_HDRINCL have no effect on IPv4 or IPv6 reception.</span></span>

> [!NOTE]
> <span data-ttu-id="5d977-164">La specifica del socket BSD 4,3 specifica che il kernel deve copiare il pacchetto non elaborato in ogni buffer di ricezione del socket.</span><span class="sxs-lookup"><span data-stu-id="5d977-164">The BSD 4.3 Socket specification specifies that the kernel must copy the raw packet to each socket receive buffer.</span></span> <span data-ttu-id="5d977-165">Tuttavia, in NetX Duo BSD, se vengono creati più socket che condividono lo stesso protocollo, il comportamento non è definito.</span><span class="sxs-lookup"><span data-stu-id="5d977-165">However in NetX Duo BSD, if multiple sockets are created sharing the same protocol, the behavior is undefined.</span></span>

## <a name="netx-duo-bsd-raw-packet-support"></a><span data-ttu-id="5d977-166">Supporto per pacchetti RAW NetX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-166">NetX Duo BSD Raw Packet Support</span></span>

<span data-ttu-id="5d977-167">Per abilitare il supporto dei pacchetti non elaborati per PPPoE, è necessario compilare il wrapper NetX Duo BSD con NX_BSD_RAW_PPPOE_SUPPORT abilitato.</span><span class="sxs-lookup"><span data-stu-id="5d977-167">To enable the raw packet support for PPPoE, NetX Duo BSD wrapper needs to be built with NX_BSD_RAW_PPPOE_SUPPORT enabled.</span></span>

<span data-ttu-id="5d977-168">Il comando seguente crea un socket BSD per gestire i pacchetti non elaborati PPPoE:</span><span class="sxs-lookup"><span data-stu-id="5d977-168">The following command creates a BSD socket to handle PPPoE raw packets:</span></span>

```c
Sockfd = socket(AF_PACKET, SOCK_RAW, protocol);
```

<span data-ttu-id="5d977-169">L'implementazione corrente di BSD supporta solo due tipi di protocollo nella famiglia di AF_PACKET</span><span class="sxs-lookup"><span data-stu-id="5d977-169">The current BSD implementation only supports two protocol types in AF_PACKET family</span></span>

- <span data-ttu-id="5d977-170">`ETHERTYPE_PPPOE_DISC`: Pacchetti di individuazione PPPoE.</span><span class="sxs-lookup"><span data-stu-id="5d977-170">`ETHERTYPE_PPPOE_DISC`: PPPoE Discovery packets.</span></span> <span data-ttu-id="5d977-171">Nel frame di dati MAC, i pacchetti di individuazione hanno il tipo di frame Ethernet 0x8863.</span><span class="sxs-lookup"><span data-stu-id="5d977-171">In the MAC data frame, the Discovery packets have the Ethernet frame type 0x8863.</span></span>

- <span data-ttu-id="5d977-172">`ETHERTYPE_PPPOE_SESS`: Pacchetti della sessione PPP.</span><span class="sxs-lookup"><span data-stu-id="5d977-172">`ETHERTYPE_PPPOE_SESS`: PPP Session packets.</span></span> <span data-ttu-id="5d977-173">Nel frame di dati MAC, i pacchetti di sessione hanno il tipo di frame Ethernet 0x8864.</span><span class="sxs-lookup"><span data-stu-id="5d977-173">In the MAC data frame, the Session packets have the Ethernet frame type 0x8864.</span></span>

<span data-ttu-id="5d977-174">La struttura `sockaddr_ll` viene utilizzata per specificare i parametri durante l'invio o la ricezione di frame PPPoE.</span><span class="sxs-lookup"><span data-stu-id="5d977-174">The structure `sockaddr_ll` is used to specify parameters when sending or receiving PPPoE frames.</span></span>

<span data-ttu-id="5d977-175">`struct sockaddr_ll` viene dichiarata come:</span><span class="sxs-lookup"><span data-stu-id="5d977-175">`struct sockaddr_ll` is declared as:</span></span>

```c
struct sockaddr_ll
{
    USHORT  sll_family;     /* Must be AF_PACKET */
    USHORT  sll_protocol;   /* LL frame type */
    INT     sll_ifindex;    /* Interface Index. */
    USHORT  sll_hatype;     /* Header type */
    UCHAR   sll_pkttype;    /* Packet type */
    UCHAR   sll_halen;      /* Length of address */
    UCHAR   sll_addr[8];    /* Physical layer address */
};
```

> [!NOTE]
> <span data-ttu-id="5d977-176">Non tutti i campi della struttura vengono utilizzati da `sendto()` o `recvfrom()` .</span><span class="sxs-lookup"><span data-stu-id="5d977-176">Not every field in the structure is used by `sendto()` or `recvfrom()`.</span></span> <span data-ttu-id="5d977-177">Vedere la descrizione seguente per informazioni su come configurare `sockaddr_ll` per l'invio e la ricezione di pacchetti PPPoE.</span><span class="sxs-lookup"><span data-stu-id="5d977-177">See the description below on how to set up the `sockaddr_ll` for sending and receiving PPPoE packets.</span></span>

<span data-ttu-id="5d977-178">Il socket creato nella famiglia di AF_PACKET può essere usato per inviare pacchetti di individuazione PPPoE o pacchetti di sessioni PPP, indipendentemente dal protocollo specificato.</span><span class="sxs-lookup"><span data-stu-id="5d977-178">Socket created in the AF_PACKET family can be used to send either PPPoE Discovery packets or PPP session packets, regardless of the protocol specified.</span></span> <span data-ttu-id="5d977-179">Quando si trasmette un pacchetto PPPoE, l'applicazione deve preparare il buffer che include il frame PPPoE correttamente formattato, incluse le intestazioni MAC (indirizzo MAC di destinazione, indirizzo MAC di origine e tipo di frame). La dimensione del buffer include l'intestazione Ethernet a 14 byte.</span><span class="sxs-lookup"><span data-stu-id="5d977-179">When transmitting a PPPoE packet, application must prepare the buffer that includes properly formatted PPPoE frame, including the MAC headers (Destination MAC address, source MAC address, and frame type.) The size of the buffer includes the 14-byte Ethernet header.</span></span>

<span data-ttu-id="5d977-180">Lo `sockaddr_ll` struct `sll_ifindex` viene usato per indicare l'interfaccia fisica da usare per l'invio del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5d977-180">The `sockaddr_ll` struct, the `sll_ifindex` is used to indicate the physical interface to be used for sending this packet.</span></span> <span data-ttu-id="5d977-181">Il resto dei campi nella struttura non viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5d977-181">The rest of the fields in the structure are not used.</span></span> <span data-ttu-id="5d977-182">I valori impostati sui campi non usati vengono ignorati dal processo interno di BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-182">Values set to the unused fields are ignored by the BSD internal process.</span></span>

<span data-ttu-id="5d977-183">Il blocco di codice seguente illustra come trasmettere un pacchetto PPPoE:</span><span class="sxs-lookup"><span data-stu-id="5d977-183">The following code block illustrates how to transmit a PPPoE packet:</span></span>

```c
struct sockaddr_ll peer_addr;

/* Transmit a PPPoE frame using the primary network interface. */
peer_addr.sll_ifindex = 0;
n = sendto(sockfd, frame, frame_size, 0, (struct
        sockaddr*)&peer_addr, sizeof(peer_addr));
```

<span data-ttu-id="5d977-184">Il valore restituito indica il numero di byte trasmessi.</span><span class="sxs-lookup"><span data-stu-id="5d977-184">The return value indicates the number of bytes transmitted.</span></span> <span data-ttu-id="5d977-185">Poiché i pacchetti PPPoE sono basati su messaggi, in una trasmissione corretta, il numero di byte inviati corrisponde alla dimensione del pacchetto, inclusa l'intestazione Ethernet a 14 byte.</span><span class="sxs-lookup"><span data-stu-id="5d977-185">Since PPPoE packets are message-based, on a successful transmission, the number of bytes sent matches the size of the packet, including the 14-byte Ethernet header.</span></span>

<span data-ttu-id="5d977-186">I pacchetti PPPoE possono essere ricevuti tramite `recvfrom()` .</span><span class="sxs-lookup"><span data-stu-id="5d977-186">PPPoE packets can be received using `recvfrom()`.</span></span> <span data-ttu-id="5d977-187">Il buffer di ricezione deve essere sufficientemente grande da contenere il messaggio di dimensioni MTU Ethernet.</span><span class="sxs-lookup"><span data-stu-id="5d977-187">The receive buffer must be big enough to accommodate message of Ethernet MTU size.</span></span> <span data-ttu-id="5d977-188">Il pacchetto PPPoE ricevuto include l'intestazione Ethernet a 14 byte.</span><span class="sxs-lookup"><span data-stu-id="5d977-188">The received PPPoE packet includes 14-byte Ethernet header.</span></span> <span data-ttu-id="5d977-189">Alla ricezione di pacchetti PPPoE, i pacchetti di individuazione PPPoE possono essere ricevuti solo dal socket creato con il protocollo `ETHERTYPE_PPPOE_DISC` .</span><span class="sxs-lookup"><span data-stu-id="5d977-189">On receiving PPPoE packets, PPPoE Discovery packets can only be received by socket created with protocol `ETHERTYPE_PPPOE_DISC`.</span></span> <span data-ttu-id="5d977-190">Analogamente, i pacchetti di sessione PPP possono essere ricevuti solo dal socket creato con il protocollo `ETHERTYPE_PPPOE_SESS` .</span><span class="sxs-lookup"><span data-stu-id="5d977-190">Similarly, PPP session packets can only be received by socket created with protocol `ETHERTYPE_PPPOE_SESS`.</span></span> <span data-ttu-id="5d977-191">Se vengono creati più socket per lo stesso tipo di protocollo, i pacchetti PPPoE in arrivo vengono inoltrati al socket creato per primo.</span><span class="sxs-lookup"><span data-stu-id="5d977-191">If multiple sockets are created for the same protocol type, arriving PPPoE packets are forwarded to the socket created first.</span></span> <span data-ttu-id="5d977-192">Se il primo socket creato per il protocollo viene chiuso, il socket successivo nell'ordine di creazione viene usato per la ricezione di questi pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5d977-192">If the first socket created for the protocol is closed, the next socket in the order of creation is used for receiving these packets.</span></span>

<span data-ttu-id="5d977-193">Dopo la ricezione di un pacchetto PPPoE, i campi seguenti nello `sockaddr_ll` struct sono validi:</span><span class="sxs-lookup"><span data-stu-id="5d977-193">After a PPPoE packet is received, the following fields in the `sockaddr_ll` struct are valid:</span></span>
- <span data-ttu-id="5d977-194">**sll_family**: impostato dall'interno BSD da AF_PACKET</span><span class="sxs-lookup"><span data-stu-id="5d977-194">**sll_family**: Set by the BSD internal to be AF_PACKET</span></span>
- <span data-ttu-id="5d977-195">**sll_ifindex**: indica l'interfaccia da cui viene ricevuto il pacchetto</span><span class="sxs-lookup"><span data-stu-id="5d977-195">**sll_ifindex**: Indicates the interface from which the packet is received</span></span>
- <span data-ttu-id="5d977-196">**sll_protocol**: impostare sul tipo di pacchetto ricevuto: `ETHERTYPE_PPPOE_DISC` o `ETHERTYPE_PPPOE_SESS`</span><span class="sxs-lookup"><span data-stu-id="5d977-196">**sll_protocol**: Set to the type of packet received: `ETHERTYPE_PPPOE_DISC` or `ETHERTYPE_PPPOE_SESS`</span></span>

## <a name="eliminating-internal-bsd-thread"></a><span data-ttu-id="5d977-197">Eliminazione del thread BSD interno</span><span class="sxs-lookup"><span data-stu-id="5d977-197">Eliminating Internal BSD Thread</span></span>

<span data-ttu-id="5d977-198">Per impostazione predefinita, BSD utilizza un thread interno per eseguire parte dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5d977-198">By default, BSD utilizes an internal thread to perform some of its processing.</span></span> <span data-ttu-id="5d977-199">Nei sistemi con vincoli di memoria limitati, BSD può essere compilato con NX_BSD_TIMEOUT_PROCESS_IN_TIMER definito, che elimina il thread BSD interno e usa invece un timer interno per eseguire la stessa elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5d977-199">In systems with tight memory constraints, BSD can be built with NX_BSD_TIMEOUT_PROCESS_IN_TIMER defined, which eliminates the internal BSD thread and instead uses an internal timer to perform the same processing.</span></span> <span data-ttu-id="5d977-200">In questo modo si elimina la memoria necessaria per il blocco e lo stack di controllo dei thread BSD interni.</span><span class="sxs-lookup"><span data-stu-id="5d977-200">This eliminates the memory required for the internal BSD thread control block and stack.</span></span> <span data-ttu-id="5d977-201">Tuttavia, l'elaborazione del timer complessiva è significativamente aumentata e anche l'elaborazione BSD può essere eseguita con una priorità più alta del necessario.</span><span class="sxs-lookup"><span data-stu-id="5d977-201">However, overall timer processing is significantly increased and the BSD processing may also execute at a higher priority than needed.</span></span>

<span data-ttu-id="5d977-202">Per configurare i socket BSD per l'esecuzione nel contesto del timer ThreadX, definire NX_BSD_TIMEOUT_PROCESS_IN_TIMER in *nxd_bsd. h*.</span><span class="sxs-lookup"><span data-stu-id="5d977-202">To configure BSD sockets to run in the ThreadX timer context, define NX_BSD_TIMEOUT_PROCESS_IN_TIMER in *nxd_bsd.h*.</span></span> <span data-ttu-id="5d977-203">Se il livello BSD è configurato per eseguire le attività BSD nel contesto del timer, nella chiamata a *bsd_initialize* i tre parametri seguenti vengono ignorati e devono essere impostati su null:</span><span class="sxs-lookup"><span data-stu-id="5d977-203">If the BSD layer is configured to execute the BSD tasks in the timer context, in the call to *bsd_initialize*, the following three parameters are ignored, and should be set to NULL:</span></span>

- <span data-ttu-id="5d977-204">**bsd_thread_stack_area**</span><span class="sxs-lookup"><span data-stu-id="5d977-204">**bsd_thread_stack_area**</span></span>
- <span data-ttu-id="5d977-205">**bsd_thread_stack_size**</span><span class="sxs-lookup"><span data-stu-id="5d977-205">**bsd_thread_stack_size**</span></span>
- <span data-ttu-id="5d977-206">**bsd_thread_priority**</span><span class="sxs-lookup"><span data-stu-id="5d977-206">**bsd_thread_priority**</span></span>

## <a name="netx-duo-bsd-with-dns-support"></a><span data-ttu-id="5d977-207">NetX Duo BSD con supporto DNS</span><span class="sxs-lookup"><span data-stu-id="5d977-207">NetX Duo BSD with DNS Support</span></span>

<span data-ttu-id="5d977-208">Se NX_BSD_ENABLE_DNS è stato definito, NetX Duo BSD può inviare query DNS per ottenere informazioni sul nome host o sull'indirizzo IP dell'host.</span><span class="sxs-lookup"><span data-stu-id="5d977-208">If NX_BSD_ENABLE_DNS is defined, NetX Duo BSD can send DNS queries to obtain hostname or host IP information.</span></span> <span data-ttu-id="5d977-209">Questa funzionalità richiede che un client DNS NetX venga creato in precedenza usando il servizio *nx_dns_create* .</span><span class="sxs-lookup"><span data-stu-id="5d977-209">This feature requires a NetX DNS Client to be previously created using the *nx_dns_create* service.</span></span> <span data-ttu-id="5d977-210">Uno o più indirizzi IP del server DNS noti devono essere registrati con l'istanza DNS utilizzando il servizio *nx_dns_server_add* per aggiungere indirizzi server IPv4 o utilizzando il servizio *nxd_dns_server_add* per aggiungere indirizzi server IPv4 o IPv6.</span><span class="sxs-lookup"><span data-stu-id="5d977-210">One or more known DNS server IP addresses must be registered with the DNS instance using the *nx_dns_server_add* service for adding IPv4 server addresses, or using the *nxd_dns_server_add* service for adding either IPv4 or IPv6 server addresses.</span></span>

<span data-ttu-id="5d977-211">I servizi DNS e l'allocazione di memoria vengono usati dai servizi *funzione getaddrinfo* e *GetNameInfo* :</span><span class="sxs-lookup"><span data-stu-id="5d977-211">DNS services and memory allocation are used by *getaddrinfo* and *getnameinfo* services:</span></span>

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
        const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
        char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

<span data-ttu-id="5d977-212">Quando l'applicazione BSD chiama *funzione getaddrinfo* con un nome host, NETX BSD chiamerà uno dei servizi seguenti per ottenere l'indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="5d977-212">When the BSD application calls *getaddrinfo* with a hostname, NetX BSD will call any of the below services to obtain the IP address:</span></span>

- <span data-ttu-id="5d977-213">**nx_dns_ipv4_address_by_name_get**</span><span class="sxs-lookup"><span data-stu-id="5d977-213">**nx_dns_ipv4_address_by_name_get**</span></span>
- <span data-ttu-id="5d977-214">**nxd_dns_ipv6_address_by_name_get**</span><span class="sxs-lookup"><span data-stu-id="5d977-214">**nxd_dns_ipv6_address_by_name_get**</span></span>
- <span data-ttu-id="5d977-215">**nx_dns_cname_get**</span><span class="sxs-lookup"><span data-stu-id="5d977-215">**nx_dns_cname_get**</span></span>

<span data-ttu-id="5d977-216">Per *nx_dns_ipv4_address_by_name_get* e *NXD_DNS_IPV6_ADDRESS_BY_NAME_GET*, NETX BSD USA rispettivamente le aree di memoria ipv4_addr_buffer e ipv6_addr_buffer.</span><span class="sxs-lookup"><span data-stu-id="5d977-216">For *nx_dns_ipv4_address_by_name_get* and *nxd_dns_ipv6_address_by_name_get*, NetX BSD uses the ipv4_addr_buffer and ipv6_addr_buffer memory areas respectively.</span></span> <span data-ttu-id="5d977-217">Le dimensioni di questi buffer sono definite rispettivamente da (NX_BSD_IPV4_ADDR_PER_HOST \* 4) e (NX_BSD_IPV6_ADDR_PER_HOST \* 16).</span><span class="sxs-lookup"><span data-stu-id="5d977-217">The size of these buffers are defined by (NX_BSD_IPV4_ADDR_PER_HOST \* 4) and (NX_BSD_IPV6_ADDR_PER_HOST \* 16) respectively.</span></span>

<span data-ttu-id="5d977-218">Per restituire le informazioni sull'indirizzo da *funzione getaddrinfo*, NETX BSD usa la tabella di memoria a blocchi threadX nx_bsd_addrinfo_pool_memory, la cui area di memoria è definita da un altro set di opzioni configurabili, NX_BSD_IPV4_ADDR_MAX_NUM e NX_BSD_IPV6_ADDR_MAX_NUM.</span><span class="sxs-lookup"><span data-stu-id="5d977-218">For returning address information from *getaddrinfo*, NetX BSD uses the ThreadX block memory table nx_bsd_addrinfo_pool_memory, whose memory area is defined by another set of configurable options, NX_BSD_IPV4_ADDR_MAX_NUM and NX_BSD_IPV6_ADDR_MAX_NUM.</span></span>

<span data-ttu-id="5d977-219">Per ulteriori informazioni sulle opzioni di configurazione precedenti, vedere **Opzioni di configurazione generali** .</span><span class="sxs-lookup"><span data-stu-id="5d977-219">See **General Configuration Options** for more details on the above configuration options.</span></span>

<span data-ttu-id="5d977-220">Inoltre, se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito e l'input dell'host è un nome canonico, NetX Duo BSD allocherà la memoria dinamicamente da un pool di blocchi creato in precedenza ' _nx_bsd_cname_block_pool</span><span class="sxs-lookup"><span data-stu-id="5d977-220">Additionally, if NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, and the host input is a canonical name, NetX Duo BSD will allocate memory dynamically from a previously created block pool \`_nx_bsd_cname_block_pool</span></span>

> [!NOTE]
> <span data-ttu-id="5d977-221">Dopo la chiamata a *funzione getaddrinfo* , l'applicazione BSD è responsabile del rilascio della memoria a cui fa riferimento l'argomento res alla tabella dei blocchi usando il servizio *FreeAddrInfo* .</span><span class="sxs-lookup"><span data-stu-id="5d977-221">After calling *getaddrinfo* the BSD application is responsible for releasing the memory pointed to by the res argument back to the block table using the *freeaddrinfo* service.</span></span>

## <a name="netx-duo-bsd-limitations"></a><span data-ttu-id="5d977-222">Limitazioni di NetX Duo BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-222">NetX Duo BSD Limitations</span></span>

<span data-ttu-id="5d977-223">A causa di problemi relativi alle prestazioni e all'architettura, NetX Duo BSD non supporta tutte le funzionalità socket di BSD 4,3:</span><span class="sxs-lookup"><span data-stu-id="5d977-223">Due to performance and architecture issues, NetX Duo BSD does not support all the BSD 4.3 socket features:</span></span>

<span data-ttu-id="5d977-224">I flag INT non sono supportati per le chiamate *Send, ricezione, SendTo* e *recvfrom* .</span><span class="sxs-lookup"><span data-stu-id="5d977-224">INT flags are not supported for *send, recv, sendto* and *recvfrom* calls.</span></span>

## <a name="general-configuration-options"></a><span data-ttu-id="5d977-225">Opzioni di configurazione generali</span><span class="sxs-lookup"><span data-stu-id="5d977-225">General Configuration Options</span></span>

<span data-ttu-id="5d977-226">Le opzioni configurabili dall'utente in *nxd_bsd. h* consentono all'applicazione di ottimizzare i socket NETX Duo BSD per i requisiti specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d977-226">User configurable options in *nxd_bsd.h* allow the application to fine tune NetX Duo BSD sockets for its particular application requirements.</span></span>

<span data-ttu-id="5d977-227">Di seguito è riportato l'elenco delle opzioni configurabili impostate in fase di compilazione:</span><span class="sxs-lookup"><span data-stu-id="5d977-227">The following is the list of configurable options that are set at compile time:</span></span>

- <span data-ttu-id="5d977-228">**NX_BSD_TCP_WINDOW**: utilizzato nelle chiamate di creazione socket TCP.</span><span class="sxs-lookup"><span data-stu-id="5d977-228">**NX_BSD_TCP_WINDOW**: Used in TCP socket create calls.</span></span> <span data-ttu-id="5d977-229">64K è la tipica dimensione della finestra per Ethernet 100Mb.</span><span class="sxs-lookup"><span data-stu-id="5d977-229">64k is typical window size for 100Mb Ethernet.</span></span> <span data-ttu-id="5d977-230">Il valore predefinito è 65535.</span><span class="sxs-lookup"><span data-stu-id="5d977-230">The default value is 65535.</span></span>

- <span data-ttu-id="5d977-231">**NX_BSD_SOCKFD_START**: si tratta dell'indice logico per il valore iniziale del descrittore del file socket BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-231">**NX_BSD_SOCKFD_START**: This is the logical index for the BSD socket file descriptor start value.</span></span> <span data-ttu-id="5d977-232">Per impostazione predefinita, questa opzione è 32.</span><span class="sxs-lookup"><span data-stu-id="5d977-232">By default this option is 32.</span></span>

- <span data-ttu-id="5d977-233">**NX_BSD_MAX_SOCKETS**: specifica il numero massimo di socket totali disponibili nel livello BSD e deve essere un multiplo di 32.</span><span class="sxs-lookup"><span data-stu-id="5d977-233">**NX_BSD_MAX_SOCKETS**: Specifies the maximum number of total sockets available in the BSD layer and must be a multiple of 32.</span></span> <span data-ttu-id="5d977-234">Per impostazione predefinita, il valore è 32.</span><span class="sxs-lookup"><span data-stu-id="5d977-234">The value is defaulted to 32.</span></span>

- <span data-ttu-id="5d977-235">**NX_BSD_SOCKET_QUEUE_MAX**: specifica il numero massimo di pacchetti UDP archiviati nella coda del socket di ricezione.</span><span class="sxs-lookup"><span data-stu-id="5d977-235">**NX_BSD_SOCKET_QUEUE_MAX**: Specifies the maximum number of UDP packets stored on the receive socket queue.</span></span> <span data-ttu-id="5d977-236">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="5d977-236">The value is defaulted to 5.</span></span>

- <span data-ttu-id="5d977-237">**NX_BSD_MAX_LISTEN_BACKLOG**: specifica le dimensioni della coda di ascolto (' backlog ') per i socket TCP BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-237">**NX_BSD_MAX_LISTEN_BACKLOG**: This specifies the size of the listen queue ('backlog') for BSD TCP sockets.</span></span> <span data-ttu-id="5d977-238">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="5d977-238">The default value is 5.</span></span>

- <span data-ttu-id="5d977-239">**NX_MICROSECOND_PER_CPU_TICK**: specifica il numero di microsecondi per ogni segno di timer dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="5d977-239">**NX_MICROSECOND_PER_CPU_TICK**: Specifies the number of microseconds per scheduler timer tick.</span></span>

- <span data-ttu-id="5d977-240">**NX_BSD_TIMEOUT**: specifica il timeout nei cicli del timer per le chiamate interne NETX Duo richieste da BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-240">**NX_BSD_TIMEOUT**: Specifies the timeout in timer ticks on NetX Duo internal calls required by BSD.</span></span> <span data-ttu-id="5d977-241">Il valore predefinito è (20 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="5d977-241">The default value is (20 \* NX_IP_PERIODIC_RATE).</span></span>

- <span data-ttu-id="5d977-242">**NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: specifica il timeout nei cicli del timer per la chiamata di disconnessione NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="5d977-242">**NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: Specifies the timeout in timer ticks on NetX Duo disconnect call.</span></span> <span data-ttu-id="5d977-243">Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="5d977-243">The default value is 1.</span></span>

- <span data-ttu-id="5d977-244">**NX_BSD_PRINT_ERRORS**: se impostato, lo stato di errore restituito da una funzione BSD restituisce un numero di riga e il tipo di errore, ad esempio NX_SOC_ERROR in cui si è verificato l'errore.</span><span class="sxs-lookup"><span data-stu-id="5d977-244">**NX_BSD_PRINT_ERRORS**: If set, the error status return of a BSD function returns a line number and type of error e.g. NX_SOC_ERROR where the error occurs.</span></span> <span data-ttu-id="5d977-245">A questo scopo, lo sviluppatore dell'applicazione deve definire l'output di debug.</span><span class="sxs-lookup"><span data-stu-id="5d977-245">This requires the application developer to define the debug output.</span></span> <span data-ttu-id="5d977-246">L'impostazione predefinita è disabilitata e non è stato specificato alcun output di debug in *nxd_bsd. h*.</span><span class="sxs-lookup"><span data-stu-id="5d977-246">The default setting is disabled and no debug output is specified in *nxd_bsd.h*.</span></span>

- <span data-ttu-id="5d977-247">**NX_BSD_TIMER_RATE**: intervallo dopo il quale viene eseguita l'attività del timer periodico BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-247">**NX_BSD_TIMER_RATE**: Interval after which BSD periodic timer task runs.</span></span> <span data-ttu-id="5d977-248">Il valore predefinito è 1 secondo (1 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="5d977-248">The default value is 1 second (1 \* NX_IP_PERIODIC_RATE).</span></span>

- <span data-ttu-id="5d977-249">**NX_BSD_TIMEOUT_PROCESS_IN_TIMER**: se impostata, questa opzione consente l'esecuzione del processo di timeout di BSD nel contesto del timer di sistema.</span><span class="sxs-lookup"><span data-stu-id="5d977-249">**NX_BSD_TIMEOUT_PROCESS_IN_TIMER**: If set, this option allows the BSD timeout process to execute in the system timer context.</span></span> <span data-ttu-id="5d977-250">Il comportamento predefinito è Disabled.</span><span class="sxs-lookup"><span data-stu-id="5d977-250">The default behavior is disabled.</span></span> <span data-ttu-id="5d977-251">Questa funzionalità è descritta in modo più dettagliato nel capitolo 2 "installazione e uso di NetX Duo BSD".</span><span class="sxs-lookup"><span data-stu-id="5d977-251">This feature is described in more detail in Chapter 2 "Installation and Use of NetX Duo BSD".</span></span>

- <span data-ttu-id="5d977-252">**NX_BSD_RAW_PPPOE_SUPPORT**: Abilita supporto per i pacchetti PPPoE non elaborati.</span><span class="sxs-lookup"><span data-stu-id="5d977-252">**NX_BSD_RAW_PPPOE_SUPPORT**: Enable PPPoE raw packet support.</span></span> <span data-ttu-id="5d977-253">Per impostazione predefinita, questa opzione non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="5d977-253">By default this option is not enabled.</span></span>

- <span data-ttu-id="5d977-254">**NX_BSD_ENABLE_DNS**: se abilitata, NETX Duo BSD invierà una query DNS per un nome host o un indirizzo IP host.</span><span class="sxs-lookup"><span data-stu-id="5d977-254">**NX_BSD_ENABLE_DNS**: If enabled, NetX Duo BSD will send a DNS query for a hostname or host IP address.</span></span> <span data-ttu-id="5d977-255">Richiede che un'istanza del client DNS venga creata e avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5d977-255">Requires a DNS Client instance to be previously created and started.</span></span> <span data-ttu-id="5d977-256">Per impostazione predefinita, non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="5d977-256">By default it is not enabled.</span></span>

- <span data-ttu-id="5d977-257">**NX_BSD_SOCKET_RAW_PROTOCOL_TABLE_SIZE**: definisce la dimensione della tabella di socket non elaborata.</span><span class="sxs-lookup"><span data-stu-id="5d977-257">**NX_BSD_SOCKET_RAW_PROTOCOL_TABLE_SIZE**: Defines the size of the raw socket table.</span></span> <span data-ttu-id="5d977-258">Il valore deve essere una potenza di due.</span><span class="sxs-lookup"><span data-stu-id="5d977-258">The value must be a power of two.</span></span> <span data-ttu-id="5d977-259">NetX BSD crea una matrice di socket di tipo NX_BSD_SOCKETS per l'invio e la ricezione di pacchetti non elaborati.</span><span class="sxs-lookup"><span data-stu-id="5d977-259">NetX BSD creates an array of sockets of type NX_BSD_SOCKETS for sending and receiving raw packets.</span></span> <span data-ttu-id="5d977-260">NX_ENABLE_IP_RAW_PACKET_FILTER deve essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="5d977-260">NX_ENABLE_IP_RAW_PACKET_FILTER must be enabled.</span></span> <span data-ttu-id="5d977-261">Per impostazione predefinita, è 32.</span><span class="sxs-lookup"><span data-stu-id="5d977-261">By default it is 32.</span></span>

- <span data-ttu-id="5d977-262">**NX_BSD_IPV4_ADDR_MAX_NUM**: numero massimo di indirizzi IPv4 restituiti da *funzione getaddrinfo*.</span><span class="sxs-lookup"><span data-stu-id="5d977-262">**NX_BSD_IPV4_ADDR_MAX_NUM**: Maximum number of IPv4 addresses returned by *getaddrinfo*.</span></span> <span data-ttu-id="5d977-263">Questo insieme a NX_BSD_IPV6_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi di NetX BSD nx_bsd_addrinfo_block_pool per l'allocazione dinamica della memoria per l'archiviazione delle informazioni di indirizzo in *funzione getaddrinfo*.</span><span class="sxs-lookup"><span data-stu-id="5d977-263">This along with NX_BSD_IPV6_ADDR_MAX_NUM defines the size of the NetX BSD block pool nx_bsd_addrinfo_block_pool for dynamically allocating memory to address information storage in *getaddrinfo*.</span></span> <span data-ttu-id="5d977-264">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="5d977-264">The default value is 5.</span></span>

- <span data-ttu-id="5d977-265">**NX_BSD_IPV6_ADDR_MAX_NUM**: numero massimo di indirizzi IPv6 restituiti da *funzione getaddrinfo*.</span><span class="sxs-lookup"><span data-stu-id="5d977-265">**NX_BSD_IPV6_ADDR_MAX_NUM**: Maximum number of IPv6 addresses returned by *getaddrinfo*.</span></span> <span data-ttu-id="5d977-266">Questo insieme a NX_BSD_IPV4_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi di NetX BSD nx_bsd_addrinfo_block_pool per l'allocazione dinamica della memoria per l'archiviazione delle informazioni di indirizzo in *funzione getaddrinfo*.</span><span class="sxs-lookup"><span data-stu-id="5d977-266">This along with NX_BSD_IPV4_ADDR_MAX_NUM defines the size of the NetX BSD block pool nx_bsd_addrinfo_block_pool for dynamically allocating memory to address information storage in *getaddrinfo*.</span></span>

- <span data-ttu-id="5d977-267">**NX_BSD_IPV4_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv4 archiviati per ogni query DNS.</span><span class="sxs-lookup"><span data-stu-id="5d977-267">**NX_BSD_IPV4_ADDR_PER_HOST**: Defines maximum IPv4 addresses stored per DNS query.</span></span> <span data-ttu-id="5d977-268">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="5d977-268">The default value is 5.</span></span>

- <span data-ttu-id="5d977-269">**NX_BSD_IPV6_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv6 archiviati per ogni query DNS.</span><span class="sxs-lookup"><span data-stu-id="5d977-269">**NX_BSD_IPV6_ADDR_PER_HOST**: Defines maximum IPv6 addresses stored per DNS query.</span></span> <span data-ttu-id="5d977-270">Il valore predefinito è 2.</span><span class="sxs-lookup"><span data-stu-id="5d977-270">The default value is 2.</span></span>

## <a name="bsd-socket-options"></a><span data-ttu-id="5d977-271">Opzioni socket BSD</span><span class="sxs-lookup"><span data-stu-id="5d977-271">BSD Socket Options</span></span>

<span data-ttu-id="5d977-272">Il seguente elenco di opzioni socket NetX Duo BSD può essere abilitato (o disabilitato) in fase di esecuzione in base a ogni socket usando il servizio *setsockopt* :</span><span class="sxs-lookup"><span data-stu-id="5d977-272">The following list of NetX Duo BSD socket options can be enabled (or disabled) at run time on a per socket basis using the *setsockopt* service:</span></span>

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, 
                const void *option_value, INT option_length);
```

<span data-ttu-id="5d977-273">Esistono due impostazioni diverse per option_level.</span><span class="sxs-lookup"><span data-stu-id="5d977-273">There are two different settings for option_level.</span></span>

<span data-ttu-id="5d977-274">Il primo tipo di opzioni dei socket di runtime è SOL_SOCKET per le opzioni a livello di socket.</span><span class="sxs-lookup"><span data-stu-id="5d977-274">The first type of run time socket options is SOL_SOCKET for socket level options.</span></span> <span data-ttu-id="5d977-275">Per abilitare un'opzione a livello di socket, chiamare *setsockopt* con option_level impostato su SOL_SOCKET e option_name impostato sull'opzione specifica, ad esempio SO_BROADCAST *.*</span><span class="sxs-lookup"><span data-stu-id="5d977-275">To enable a socket level option, call *setsockopt* with option_level set to SOL_SOCKET and option_name set to the specific option e.g. SO_BROADCAST *.*</span></span> <span data-ttu-id="5d977-276">Per recuperare un'impostazione di opzione, chiamare *getsockopt* per la option_name con option_level di nuovo impostato su SOL_SOCKET.</span><span class="sxs-lookup"><span data-stu-id="5d977-276">To retrieve an option setting, call *getsockopt* for the option_name with option_level again set to SOL_SOCKET.</span></span>

<span data-ttu-id="5d977-277">Di seguito è riportato l'elenco delle opzioni del livello di socket del runtime.</span><span class="sxs-lookup"><span data-stu-id="5d977-277">The list of run time socket level options is shown below.</span></span>

- <span data-ttu-id="5d977-278">**SO_BROADCAST**: se impostato, consente l'invio e la ricezione di pacchetti broadcast da NETX Sockets.</span><span class="sxs-lookup"><span data-stu-id="5d977-278">**SO_BROADCAST**:  If set, this enables sending and receiving broadcast packets from Netx sockets.</span></span> <span data-ttu-id="5d977-279">Questo è il comportamento predefinito per NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5d977-279">This is the default behavior for NetX Duo.</span></span> <span data-ttu-id="5d977-280">Questa funzionalità è presente in tutti i socket.</span><span class="sxs-lookup"><span data-stu-id="5d977-280">All sockets have this capability.</span></span>

- <span data-ttu-id="5d977-281">**SO_ERROR**: usato per ottenere lo stato del socket per l'operazione socket precedente del socket specificato, usando il servizio *getsockopt* .</span><span class="sxs-lookup"><span data-stu-id="5d977-281">**SO_ERROR**:  Used to obtain socket status on the previous socket operation of the specified socket, using the *getsockopt* service.</span></span> <span data-ttu-id="5d977-282">Questa funzionalità è presente in tutti i socket.</span><span class="sxs-lookup"><span data-stu-id="5d977-282">All sockets have this capability.</span></span>

- <span data-ttu-id="5d977-283">**SO_KEEPALIVE**: se impostato, Abilita la funzionalità TCP keep alive.</span><span class="sxs-lookup"><span data-stu-id="5d977-283">**SO_KEEPALIVE**:  If set, this enables the TCP Keep Alive feature.</span></span> <span data-ttu-id="5d977-284">Questa operazione richiede che la libreria NetX Duo venga compilata con NX_TCP_ENABLE_KEEPALIVE definito in *nx_user. h*.</span><span class="sxs-lookup"><span data-stu-id="5d977-284">This requires the NetX Duo library to be built with NX_TCP_ENABLE_KEEPALIVE defined in *nx_user.h*.</span></span> <span data-ttu-id="5d977-285">Per impostazione predefinita, questa funzionalità è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="5d977-285">By default this feature is disabled.</span></span>

- <span data-ttu-id="5d977-286">**SO_RCVTIMEO**: imposta l'opzione wait in secondi per la ricezione dei pacchetti nei socket BSD NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="5d977-286">**SO_RCVTIMEO**:  This sets the wait option in seconds for receiving packets on NetX Duo BSD sockets.</span></span> <span data-ttu-id="5d977-287">Il valore predefinito è il NX_WAIT_FOREVER (0xFFFFFFFF) o, se il blocco non è abilitato, NX_NO_WAIT (0x0).</span><span class="sxs-lookup"><span data-stu-id="5d977-287">The default value is the NX_WAIT_FOREVER (0xFFFFFFFF) or, if non-blocking is enabled, NX_NO_WAIT (0x0).</span></span>

- <span data-ttu-id="5d977-288">**SO_RCVBUF**: consente di impostare le dimensioni della finestra del socket TCP.</span><span class="sxs-lookup"><span data-stu-id="5d977-288">**SO_RCVBUF**:  This sets the window size of the TCP socket.</span></span> <span data-ttu-id="5d977-289">Il valore predefinito, NX_BSD_TCP_WINDOW, è impostato su 64K per i socket TCP BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-289">The default value, NX_BSD_TCP_WINDOW, is set to 64k for BSD TCP sockets.</span></span> <span data-ttu-id="5d977-290">Per impostare la dimensione superiore a 65535, è necessario che la libreria NetX Duo venga compilata con il NX_TCP_ENABLE_WINDOW_SCALING essere definito.</span><span class="sxs-lookup"><span data-stu-id="5d977-290">To set the size over 65535 requires the NetX Duo library to be built with the NX_TCP_ENABLE_WINDOW_SCALING be defined.</span></span>

- <span data-ttu-id="5d977-291">**SO_REUSEADDR**: se impostato, consente di eseguire il mapping di più socket a una porta.</span><span class="sxs-lookup"><span data-stu-id="5d977-291">**SO_REUSEADDR**:  If set, this enables multiple sockets to be mapped to one port.</span></span> <span data-ttu-id="5d977-292">L'utilizzo tipico è per il socket del server TCP.</span><span class="sxs-lookup"><span data-stu-id="5d977-292">The typical usage is for the TCP Server socket.</span></span> <span data-ttu-id="5d977-293">Si tratta del comportamento predefinito dei socket NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="5d977-293">This is the default behavior of NetX Duo sockets.</span></span>

<span data-ttu-id="5d977-294">Il secondo tipo di opzioni del socket di run-time è il livello di opzione IP.</span><span class="sxs-lookup"><span data-stu-id="5d977-294">The second type of run time socket options is the IP option level.</span></span> <span data-ttu-id="5d977-295">Per abilitare un'opzione a livello IP, chiamare *setsockopt* con option_level impostato su IP_PROTO e option_name impostato sull'opzione, ad esempio IP_MULTICAST_TTL *.*</span><span class="sxs-lookup"><span data-stu-id="5d977-295">To enable an IP level option, call *setsockopt* with option_level set to IP_PROTO and option_name set to the option e.g. IP_MULTICAST_TTL *.*</span></span> <span data-ttu-id="5d977-296">Per recuperare un'impostazione di opzione, chiamare *getsockopt* per la option_name con option_level di nuovo impostato su IP_PROTO.</span><span class="sxs-lookup"><span data-stu-id="5d977-296">To retrieve an option setting, call *getsockopt* for the option_name with option_level again set to IP_PROTO.</span></span>

<span data-ttu-id="5d977-297">Di seguito è riportato l'elenco delle opzioni di livello IP di run-time.</span><span class="sxs-lookup"><span data-stu-id="5d977-297">The list of run time IP level options is shown below.</span></span>

- <span data-ttu-id="5d977-298">**IP_MULTICAST_TTL**: imposta la durata (TTL) per i socket UDP.</span><span class="sxs-lookup"><span data-stu-id="5d977-298">**IP_MULTICAST_TTL**:  This sets the time to live for UDP sockets.</span></span> <span data-ttu-id="5d977-299">Il valore predefinito è NX_IP_TIME_TO_LIVE (0x80) al momento della creazione del socket.</span><span class="sxs-lookup"><span data-stu-id="5d977-299">The default value is NX_IP_TIME_TO_LIVE (0x80) when the socket is created.</span></span> <span data-ttu-id="5d977-300">È possibile eseguire l'override di questo valore chiamando *setsockopt* con questa opzione socket.</span><span class="sxs-lookup"><span data-stu-id="5d977-300">This value can be overridden by calling *setsockopt* with this socket option.</span></span>

- <span data-ttu-id="5d977-301">**IP_RAW_IPV6_HDRINCL**: se questa opzione è impostata, l'applicazione chiamante deve aggiungere un'intestazione IPv6 e, facoltativamente, le intestazioni dell'applicazione ai dati trasmessi su socket IPv6 non elaborati creati da BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-301">**IP_RAW_IPV6_HDRINCL**:  If this option is set, the calling application must append an IPv6 header and optionally application headers to data being transmitted on raw IPv6 sockets created by BSD.</span></span> <span data-ttu-id="5d977-302">Per usare questa opzione, è necessario abilitare l'elaborazione di socket non elaborati nell'attività IP.</span><span class="sxs-lookup"><span data-stu-id="5d977-302">To use this option, raw socket processing must be enabled on the IP task.</span></span>

- <span data-ttu-id="5d977-303">**IP_ADD_MEMBERSHIP**: se impostata, questa opzione Abilita il socket BSD (si applica solo ai socket UDP) per l'aggiunta al gruppo IGMP specificato.</span><span class="sxs-lookup"><span data-stu-id="5d977-303">**IP_ADD_MEMBERSHIP**:  If set, this options enables the BSD socket (applies only to UDP sockets) to join the specified IGMP group.</span></span>

- <span data-ttu-id="5d977-304">**IP_DROP_MEMBERSHIP**: se impostata, questa opzione Abilita il socket BSD (si applica solo ai socket UDP) per lasciare il gruppo IGMP specificato.</span><span class="sxs-lookup"><span data-stu-id="5d977-304">**IP_DROP_MEMBERSHIP**:  If set, this options enables the BSD socket (applies only to UDP sockets) to leave the specified IGMP group.</span></span>

- <span data-ttu-id="5d977-305">**IP_HDRINCL**: se questa opzione è impostata, l'applicazione chiamante deve aggiungere l'intestazione IP e, facoltativamente, le intestazioni dell'applicazione ai dati trasmessi in socket IPv4 non elaborati creati in BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-305">**IP_HDRINCL**:  If this option is set, the calling application must append the IP header and optionally application headers to data being transmitted on raw IPv4 sockets created in BSD.</span></span> <span data-ttu-id="5d977-306">Per usare questa opzione, è necessario abilitare l'elaborazione di socket non elaborati nell'attività IP.</span><span class="sxs-lookup"><span data-stu-id="5d977-306">To use this option, raw socket processing must be enabled on the IP task.</span></span>

- <span data-ttu-id="5d977-307">**IP_RAW_RX_NO_HEADER**: Se deselezionata, l'intestazione IPv6 viene inclusa con i dati ricevuti per i socket IPv6 non elaborati creati in BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-307">**IP_RAW_RX_NO_HEADER**:  If cleared, the IPv6 header is included with the received data for raw IPv6 sockets created in BSD.</span></span> <span data-ttu-id="5d977-308">Le intestazioni IPv6 vengono rimosse per impostazione predefinita nei socket IPv6 non elaborati BSD e la lunghezza del pacchetto non include l'intestazione IPv6.</span><span class="sxs-lookup"><span data-stu-id="5d977-308">IPv6 headers are removed by default in BSD raw IPv6 sockets, and the packet length does not include the IPv6 header.</span></span>

<span data-ttu-id="5d977-309">Se impostato, l'intestazione IPv4 viene rimossa dai dati ricevuti su socket raw BSD di tipo IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d977-309">If set, the IPv4 header is removed from received data on BSD raw sockets of type IPv4.</span></span> <span data-ttu-id="5d977-310">Le intestazioni IPv4 sono incluse per impostazione predefinita nei socket IPv4 non elaborati BSD e la lunghezza dei pacchetti include l'intestazione IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d977-310">IPv4 headers are included by default in BSD raw IPv4 sockets and packet length includes the IPv4 header.</span></span>

<span data-ttu-id="5d977-311">Questa opzione non ha alcun effetto sui dati di trasmissione IPv4 o IPv6.</span><span class="sxs-lookup"><span data-stu-id="5d977-311">This option has no effect on either IPv4 or IPv6 transmission data.</span></span>

## <a name="small-ipv4-example"></a><span data-ttu-id="5d977-312">Piccolo esempio IPv4</span><span class="sxs-lookup"><span data-stu-id="5d977-312">Small IPv4 Example</span></span>

<span data-ttu-id="5d977-313">Di seguito è riportato un esempio di come usare i servizi NetX Duo BSD per le reti IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d977-313">An example of how to use NetX Duo BSD services for IPv4 networks is described below.</span></span> <span data-ttu-id="5d977-314">In questo esempio il file di inclusione *nxd_bsd. h* viene introdotto nella riga 8.</span><span class="sxs-lookup"><span data-stu-id="5d977-314">In this example, the include file *nxd_bsd.h* is brought in at line 8.</span></span> <span data-ttu-id="5d977-315">Successivamente, l'istanza IP *bsd_ip* e *bsd_pool* pool di pacchetti vengono creati come variabili globali alle righe 20 e 21.</span><span class="sxs-lookup"><span data-stu-id="5d977-315">Next, the IP instance *bsd_ip* and packet pool *bsd_pool* are created as global variables at line 20 and 21.</span></span> <span data-ttu-id="5d977-316">Si noti che questa demo usa un driver di rete RAM (virtuale)*, _nx_ram_network_driver*.</span><span class="sxs-lookup"><span data-stu-id="5d977-316">Note that this demo uses a ram (virtual) network driver *, _nx_ram_network_driver*.</span></span> <span data-ttu-id="5d977-317">Il client e il server condividono lo stesso indirizzo IP in una singola istanza IP in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="5d977-317">The client and server will share the same IP address on single IP instance in this example.</span></span>

<span data-ttu-id="5d977-318">I thread client e server vengono creati nelle righe 62 e 68.</span><span class="sxs-lookup"><span data-stu-id="5d977-318">The client and server threads are created on lines 62 and 68.</span></span> <span data-ttu-id="5d977-319">Il pool di pacchetti BSD per la trasmissione di pacchetti viene creato alla riga 78 e usato nella creazione dell'istanza IP alla riga 87.</span><span class="sxs-lookup"><span data-stu-id="5d977-319">The BSD packet pool for transmitting packets is created on line 78 and used in the IP instance creation on line 87.</span></span> <span data-ttu-id="5d977-320">Si noti che all'attività thread IP viene assegnata la priorità 1 nella chiamata *nx_ip_create* .</span><span class="sxs-lookup"><span data-stu-id="5d977-320">Note that the IP thread task is given priority 1 in the *nx_ip_create* call.</span></span> <span data-ttu-id="5d977-321">Questo thread deve essere l'attività con priorità più elevata definita nel programma per ottimizzare le prestazioni di NetX.</span><span class="sxs-lookup"><span data-stu-id="5d977-321">This thread should be the highest priority task defined in the program for optimal NetX performance.</span></span>

<span data-ttu-id="5d977-322">L'istanza IP è abilitata per i servizi ARP e TCP rispettivamente sulle righe 88 e 110.</span><span class="sxs-lookup"><span data-stu-id="5d977-322">The IP instance is enabled for ARP and TCP services on lines 88 and 110 respectively.</span></span> <span data-ttu-id="5d977-323">L'ultimo requisito prima che i servizi BSD possano essere usati è chiamare *bsd_initialize* alla riga 120 per configurare tutte le strutture di dati e le risorse NETX e threadX necessarie per BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-323">The last requirement before BSD services can be used is to call *bsd_initialize* on line 120 to set up all data structures and NetX and ThreadX resources needed by BSD.</span></span>

<span data-ttu-id="5d977-324">La funzione entry thread server è definita successivamente.</span><span class="sxs-lookup"><span data-stu-id="5d977-324">The server thread entry function is defined next.</span></span> <span data-ttu-id="5d977-325">Il socket TCP BSD viene creato alla riga 149.</span><span class="sxs-lookup"><span data-stu-id="5d977-325">The BSD TCP socket is created on line 149.</span></span> <span data-ttu-id="5d977-326">La porta e l'indirizzo IP del server sono impostati sulle righe 160-163.</span><span class="sxs-lookup"><span data-stu-id="5d977-326">The server IP address and port are set on lines 160-163.</span></span> <span data-ttu-id="5d977-327">Si noti l'uso delle macro dell'ordine dei byte da host a rete *htonl* e *htons* applicati alla porta e all'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="5d977-327">Note the use of host to network byte order macros *htonl* and *htons* applied to the IP address and port.</span></span> <span data-ttu-id="5d977-328">Questo è conforme alla specifica del socket BSD che i dati in più byte vengono inviati ai servizi BSD nell'ordine dei byte di rete.</span><span class="sxs-lookup"><span data-stu-id="5d977-328">This is in compliance with BSD socket specification that multi byte data is submitted to the BSD services in network byte order.</span></span>

<span data-ttu-id="5d977-329">Successivamente, il socket del server master viene associato alla porta usando il servizio *Bind* alla riga 166.</span><span class="sxs-lookup"><span data-stu-id="5d977-329">Next, the master server socket is bound to the port using the *bind* service on line 166.</span></span> <span data-ttu-id="5d977-330">Questo è il socket in ascolto per le richieste di connessione TCP tramite il servizio *Listen* sulla riga 180.</span><span class="sxs-lookup"><span data-stu-id="5d977-330">This is the listening socket for TCP connection requests using the *listen* service on line 180.</span></span> <span data-ttu-id="5d977-331">Da qui la funzione thread del server, *thread_server_entry*, esegue cicli per verificare la presenza di eventi di ricezione tramite la chiamata *select* alla riga 202.</span><span class="sxs-lookup"><span data-stu-id="5d977-331">From here the server thread function, *thread_server_entry*, loops to check for receive events using the *select* call on line 202.</span></span> <span data-ttu-id="5d977-332">Se un evento Receive è una richiesta di connessione, che viene determinata confrontando l'elenco Read Ready, viene chiamato *Accept* sulla riga 213.</span><span class="sxs-lookup"><span data-stu-id="5d977-332">If a receive event is a connection request, which is determined by comparing the read ready list, it calls *accept* on line 213.</span></span> <span data-ttu-id="5d977-333">Un socket del server figlio viene assegnato per gestire la richiesta di connessione e aggiunto all'elenco principale dei socket del server TCP connessi a un client alla riga 223.</span><span class="sxs-lookup"><span data-stu-id="5d977-333">A child server socket is assigned to handle the connection request and added to the master list of TCP server sockets connected to a Client on line 223.</span></span> <span data-ttu-id="5d977-334">Se non sono presenti nuove richieste di connessione, il thread del server verificherà tutti i socket attualmente connessi per gli eventi di ricezione nel ciclo for a partire dalla riga 236.</span><span class="sxs-lookup"><span data-stu-id="5d977-334">If there are no new connection requests, the server thread then checks all the currently connected sockets for receive events in the for loop starting on line 236.</span></span> <span data-ttu-id="5d977-335">Quando viene rilevato un evento di ricezione in attesa, chiama *Send* e *ricezione* su tale socket fino a quando non vengono ricevuti dati (connessione chiusa sull'altro lato) e il socket viene chiuso utilizzando il servizio *soc_close* alla riga 277.</span><span class="sxs-lookup"><span data-stu-id="5d977-335">When a receive event waiting is detected, it calls *send* and *recv* on that socket until no data is received (connection closed on the other side) and the socket is closed using the *soc_close* service on line 277.</span></span>

<span data-ttu-id="5d977-336">Al termine dell'impostazione del thread del server, la funzione di immissione thread del client *thread_client_entry,* crea un socket alla riga 326 e si connette con il socket del server TCP utilizzando la chiamata di *connessione* alla riga 337.</span><span class="sxs-lookup"><span data-stu-id="5d977-336">After the server thread sets up, the Client thread entry function, *thread_client_entry,* creates a socket on line 326 and connects with the TCP server socket using the *connect* call on line 337.</span></span> <span data-ttu-id="5d977-337">Esegue quindi il ciclo per inviare e ricevere pacchetti usando rispettivamente i servizi *Send* e *ricezione* .</span><span class="sxs-lookup"><span data-stu-id="5d977-337">It then loops to send and receive packets using the *send* and *recv* services respectively.</span></span> <span data-ttu-id="5d977-338">Quando non vengono ricevuti altri dati, il socket viene chiuso alla riga 398 usando il servizio *soc_close* .</span><span class="sxs-lookup"><span data-stu-id="5d977-338">When no more data is received, it closes the socket on line 398 using the *soc_close* service.</span></span> <span data-ttu-id="5d977-339">Dopo la disconnessione, la funzione di immissione thread del client crea un nuovo socket TCP ed effettua un'altra richiesta di connessione nel ciclo while avviato alla riga 321.</span><span class="sxs-lookup"><span data-stu-id="5d977-339">After disconnection, the client thread entry function creates a new TCP socket and makes another connection request in the while loop started on line 321.</span></span>

```c
/* This is a small demo of BSD Wrapper for the high-performance NetX Duo
TCP/IP stack which uses standard BSD services for TCP connection, sending,
and receiving using a simulated Ethernet driver. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nxd_bsd.h"
#include     <string.h>
#include     <stdlib.h>

#define     DEMO_STACK_SIZE     (16*1024)
#define     SERVER_PORT         87
#define     CLIENT_PORT         77

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_server;
TX_THREAD         thread_client;
NX_PACKET_POOL    bsd_pool;
NX_IP             bsd_ip;

/* Define some global data. */
CHAR     *msg0 = "Client 1:
    ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQR
    STUVWXYZ<>END";

INT     maxfd;

/* Define the counters used in the demo application... */

ULONG     error_counter;

/* Define fd_sets for the BSD server socket. */
fd_set     master_list, read_ready;

/* Define thread prototypes. */

VOID     thread_server_entry(ULONG thread_input);
VOID     thread_client_entry(ULONG thread_input);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */
int     main()
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

    /* Create a server thread. */
    tx_thread_create(&thread_server, "Server", thread_server_entry, 0,
                    pointer, DEMO_STACK_SIZE, 8, 8, TX_NO_TIME_SLICE,
                    TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Create a Client thread. */
    tx_thread_create(&thread_client, "Client", thread_client_entry, 0,
                    pointer, DEMO_STACK_SIZE, 16, 16, TX_NO_TIME_SLICE,
                    TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a BSD packet pool. */
    status = nx_packet_pool_create(&bsd_pool, "NetX BSD Packet Pool", 128,
                                pointer, 16384);

    pointer = pointer + 16384;
    if (status)
    {
        error_counter++;
        printf("Error in creating BSD packet pool\n!");
    }

    /* Create an IP instance for BSD. */
    status = nx_ip_create(&bsd_ip, "BSD IP Instance", IP_ADDRESS(1,2,3,4),
                    0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                    pointer, 2048, 1);
                    pointer = pointer + 2048;

    if (status)
    {
        error_counter++;
        printf("Error creating BSD IP instance\n!");
    }

    /* Enable ARP and supply ARP cache memory for BSD IP Instance */
    status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable ARP \n");
    }

    /* Enable TCP processing for BSD IP instances. */
    status = nx_tcp_enable(&bsd_ip);

    /* Check TCP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable TCP \n");
    }

    /* Now initialize BSD Scoket Wrapper */
    status = bsd_initialize (&bsd_ip, &bsd_pool,pointer, 2048, 2);
}

/* Define the Server thread. */
CHAR     Server_Rcv_Buffer[100];

VOID     thread_server_entry(ULONG thread_input)
{

INT       status, sock, sock_tcp_server;
ULONG     actual_status;
INT       Clientlen;
INT       i;
UINT      is_set = NX_FALSE;
struct    sockaddr_in serverAddr;
struct    sockaddr_in ClientAddr;

    tx_thread_sleep(100);

    status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE,
        &actual_status, 100);

    /* Check status... */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Create BSD TCP Socket */
    sock_tcp_server = socket(AF_INET, SOCK_STREAM, 0);

    if (sock_tcp_server == -1)
    {
        printf("Error on Server socket %d create \n", sock_tcp_server);
        return;
    }

    printf("Server socket %d created\n", sock_tcp_server);

    /* Set the server port and IP address */
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    serverAddr.sin_port = htons(SERVER_PORT);

    /* Bind this server socket */
    status = bind (sock_tcp_server, (struct sockaddr *) &serverAddr,
                sizeof(serverAddr));

    if (status < 0)
    {
        printf("Error on Server Socket %d Bind \n", sock_tcp_server);
        return;
    }

    FD_ZERO(&master_list);
    FD_ZERO(&read_ready);
    FD_SET(sock_tcp_server,&master_list);
    maxfd = sock_tcp_server;

    /* Now listen for any client connections for this server socket */
    status = listen (sock_tcp_server, 5);
    if (status < 0)
    {
        printf("Error on Server Socket %d Listen\n", sock_tcp_server);
        return;
    }
    else
        printf("Server socket %d listen complete\n", sock_tcp_server);

    /* All set to accept client connections */

    /* Loop to create and establish server connections. */
    while(1)
    {

        printf("\n");

        read_ready = master_list;

        tx_thread_sleep(20); /* Allow some time to other threads too */

        /* Let the underlying TCP stack determine the timeout. */
        status = select(maxfd + 1, &read_ready, 0, 0, 0);

        if ((status == 0xFFFFFFFF) || (status == 0))
        {

            printf("Error with select. Status 0x%x\n", status);

            continue;
        }

        /* Check for a connection request. */
        is_set = FD_ISSET(sock_tcp_server, &read_ready);

        if(is_set)
        {

            Clientlen = sizeof(ClientAddr);

            sock = accept(sock_tcp_server,(struct sockaddr*)&ClientAddr,
                        &Clientlen);

            /* Add this new connection to our master list */
            FD_SET(sock, &master_list);

            if ( sock \maxfd)
            {

                maxfd = sock;
            }

            continue;
        }

        /* Check the set of 'ready' sockets, e.g connected to remote host and
        waiting for notice of packets received. */
        for (i = NX_BSD_SOCKFD_START; i < (maxfd+1+NX_BSD_SOCKFD_START); i++)
        {

            if ((i != sock_tcp_server) &&
                (FD_ISSET(i , &master_list)) &&
                (FD_ISSET(i , &read_ready)))
            {

                while(1)
                {

                    status = recv(i, (VOID *)Server_Rcv_Buffer, 100, 0);

                    if (status == 0)
                    {
                        printf("(Server received no data from Client on
                            socket %d)\n", i);
                        break;
                    }
                    else if (status == NX_SOC_ERROR)
                    {
                        printf("Error on Server receiving data from Client on
                            socket %d\n", i);
                        break;
                    }
                    if(status == SERVER_RCV_BUFFER_SIZE) status--;
                    Server_Rcv_Buffer[status] = 0;
                    printf("Server socket %d received %d bytes: %s\n ",
                            i, (ULONG)status, Server_Rcv_Buffer);

                    status = send(i, "Hello\n", sizeof("Hello\n"), 0);

                    if (status == NX_SOC_ERROR)
                    {
                        printf("Error on Server socket %d sending data to
                        Client\n", i);
                    }
                    else
                    {
                        printf("Server socket %d message sent to Client:
                        Hello\n", i);
                    }
                }

                /* Close this socket */
                status = soc_close(i);

                if (status != NX_SOC_ERROR)
                {
                    printf("Server socket %d closed \n", i);
                }
                else
                {
                    printf("Error on closing Server socket %d \n", i);
                }
            }
        }

    /* Loop back to check any next client connection */
    }
}

CHAR     Client_Rcv_Buffer[100];

VOID     thread_client_entry(ULONG thread_input)
{

INT        status;
INT        sock_tcp_client, length;
struct     sockaddr_in echoServAddr;
struct     sockaddr_in localAddr; /

    /* Let the server side get set up. */
    tx_thread_sleep(200);

    /* Set local port for displaying IP address and port. */
    memset(&localAddr, 0, sizeof(localAddr));
    localAddr.sin_family = AF_INET;
    localAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    localAddr.sin_port = htons(CLIENT_PORT);

    /* Set server port and IP address which we need to connect. */
    memset(&echoServAddr, 0, sizeof(echoServAddr));
    echoServAddr.sin_family = AF_INET;
    echoServAddr.sin_addr.s_addr = htonl(IP_ADDRESS(1,2,3,4));
    echoServAddr.sin_port = htons(SERVER_PORT);

    /* Now make client connections with the server. */
    while (1)
    {

        printf("\n");

        /* Create BSD TCP Socket */
        sock_tcp_client = socket( AF_INET, SOCK_STREAM, 0);

        if (sock_tcp_client == -1)
        {
            printf("Error on Client socket %d create \n", sock_tcp_client);
            return;
        }

        printf("Client socket %d created\n", sock_tcp_client);

        /* Now connect this client to the server */
        status = connect(sock_tcp_client, (struct sockaddr *)&echoServAddr,
                        sizeof(echoServAddr));

        /* Check for error. */
        if (status != OK)
        {
            printf("Error on Client socket %d connect\n", sock_tcp_client);
                    soc_close(sock_tcp_client);
            return;
        }

        /* Get and print source and destination information */
        printf("Client socket %d connected \n", sock_tcp_client);

        status = getsockname(sock_tcp_client, (struct sockaddr *)&localAddr,
                            &length);

        printf("Client port = %lu , Client = 0x%x,",
            htonl(localAddr.sin_port), htonl(localAddr.sin_addr.s_addr));

        length = sizeof(struct sockaddr_in);

        status = getpeername( sock_tcp_client, (struct sockaddr *)
                            &echoServAddr, &length);

        printf("Remote port = %lu, Remote IP = 0x%x \n",
                htonl(echoServAddr.sin_port),
                htonl(echoServAddr.sin_addr.s_addr));

        /* Now receive the echoed packet from the server */
        while(1)
        {

            printf("Client sock %d sending packet to server\n",
            sock_tcp_client);

            status = send(sock_tcp_client, "Hello", (sizeof("Hello")), 0);

            if (status == ERROR)
            {
                printf("Error: Client Socket (%d) send \n", sock_tcp_client);
            }
            else
            {
                printf("Client socket %d sent message Hello\n",
                        sock_tcp_client);
            }

            status = recv(sock_tcp_client, (VOID *)Client_Rcv_Buffer,100,0);

            if (status <= 0)
            {

                if (status < 0)
                {
                    380 printf("Error on Client receiving on socket %d \n",
                            sock_tcp_client);
                }
                else
                {
                    printf("Nothing received by Client on socket %d\n",
                            sock_tcp_client);
                }

                break;
            }
            else
            {
                printf("Client socket %d received %d bytes: %s\n",
                        sock_tcp_client,
                        status, Client_Rcv_Buffer);
            }

        }

        /* close this client socket */
        status = soc_close(sock_tcp_client);

        if (status != ERROR)
        {
            printf("Client Socket %d closed\n", sock_tcp_client);
        }
        else
        {
            printf("Error on Client Socket %d on close \n", sock_tcp_client);
        }

        /* Make another Client connection...*/

    }
}
```

## <a name="small-ipv6-example-system"></a><span data-ttu-id="5d977-340">Sistema di esempio IPv6 piccolo</span><span class="sxs-lookup"><span data-stu-id="5d977-340">Small IPv6 Example System</span></span>

<span data-ttu-id="5d977-341">Un esempio di come usare i servizi NetX Duo BSD per le reti IPv6 è descritto nel programma riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="5d977-341">An example of how to use NetX Duo BSD services for IPv6 networks is described in the program below.</span></span> <span data-ttu-id="5d977-342">Questo esempio è molto simile al programma demo IPv4 descritto in precedenza con alcune importanti differenze.</span><span class="sxs-lookup"><span data-stu-id="5d977-342">This example is very similar to the IPv4 demo program previously described with a few important differences.</span></span>

<span data-ttu-id="5d977-343">I thread client e server, il pool di pacchetti BSD, l'istanza IP e l'inizializzazione BSD si verificano come per i socket BSD IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d977-343">The client and server threads, BSD packet pool, IP instance and BSD initialization happens as it does for IPv4 BSD sockets.</span></span>

<span data-ttu-id="5d977-344">Nella funzione entry thread server *thread_server_entry*, definisce un paio di variabili IPv6 usando *sockaddr_in6* e *NXD_ADDRESS* tipi di dati sulle righe 145-148.</span><span class="sxs-lookup"><span data-stu-id="5d977-344">In the server thread entry function, *thread_server_entry*, defines a couple IPv6 variables using *sockaddr_in6* and *NXD_ADDRESS* data types on lines 145-148.</span></span> <span data-ttu-id="5d977-345">Il tipo di dati NXD_ADDRESS può archiviare i tipi di indirizzi sia IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="5d977-345">The NXD_ADDRESS data type can actually store both IPv4 and IPv6 address types.</span></span>

<span data-ttu-id="5d977-346">Successivamente, il thread del server Abilita IPv6 e ICMPv6 nell'istanza IP usando rispettivamente il servizio *nxd_ipv6_enable* e *nxd_icmpv6_enable* alla riga 161 e 169.</span><span class="sxs-lookup"><span data-stu-id="5d977-346">Next, the server thread enables IPv6 and ICMPv6 on the IP instance using the *nxd_ipv6_enable* and *nxd_icmpv6_enable* service respectively on line 161 and 169.</span></span> <span data-ttu-id="5d977-347">Successivamente, il collegamento indirizzi IP globali e locali viene registrato con l'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="5d977-347">Next, the link local and global IP addresses are registered with the IP instance.</span></span> <span data-ttu-id="5d977-348">Questa operazione viene eseguita usando il servizio *nxd_ipv6_address_set* sulle righe 180 e 195.</span><span class="sxs-lookup"><span data-stu-id="5d977-348">This is done using the *nxd_ipv6_address_set* service on lines 180 and 195.</span></span> <span data-ttu-id="5d977-349">Quindi dorme abbastanza a lungo affinché l'attività del thread IP completi il protocollo di rilevamento degli indirizzi duplicati e registri questi indirizzi come indirizzi validi nella chiamata *tx_thread_sleep* alla riga 201.</span><span class="sxs-lookup"><span data-stu-id="5d977-349">It then sleeps long enough for the IP thread task to complete the Duplicate Address Detection protocol and register these addresses as valid addresses on the *tx_thread_sleep* call on line 201.</span></span>

<span data-ttu-id="5d977-350">Successivamente, il socket del server TCP viene creato con l'argomento di input del tipo di AF_INET6 socket alla riga 204.</span><span class="sxs-lookup"><span data-stu-id="5d977-350">Next, the TCP server socket is created with the AF_INET6 socket type input argument on line 204.</span></span> <span data-ttu-id="5d977-351">La porta e l'indirizzo IPv6 del socket sono impostati sulle righe 216-221, di nuovo l'uso delle macro *htonl* e *htons* per inserire i dati nell'ordine dei byte di rete per i servizi socket BSD.</span><span class="sxs-lookup"><span data-stu-id="5d977-351">The socket IPv6 address and port are set on lines 216-221, again noting the use of *htonl* and *htons* macros to put data in network byte order for BSD socket services.</span></span> <span data-ttu-id="5d977-352">Da questo punto in poi, la funzione entry thread server è praticamente identica all'esempio IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d977-352">From here on, the server thread entry function is virtually identical to the IPv4 example.</span></span>

<span data-ttu-id="5d977-353">La funzione di immissione thread del client, *thread_client_entry*, viene definita successivamente.</span><span class="sxs-lookup"><span data-stu-id="5d977-353">The client thread entry function, *thread_client_entry*, is defined next.</span></span> <span data-ttu-id="5d977-354">Si noti che poiché il client TCP in questo esempio condivide la stessa istanza IP e l'indirizzo IPv6 del server TCP, non è necessario abilitare nuovamente i servizi IPv6 o ICMPv6 nell'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="5d977-354">Note that because the TCP client in this example shares the same IP instance and IPv6 address as the TCP server, we do not need to enable IPv6 or ICMPv6 services on the IP instance again.</span></span> <span data-ttu-id="5d977-355">Inoltre, l'indirizzo IPv6 è già registrato con l'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="5d977-355">Further, the IPv6 address is also already registered with the IP instance.</span></span> <span data-ttu-id="5d977-356">Al contrario, la funzione di immissione thread del client attende semplicemente la riga 368 per la configurazione del server.</span><span class="sxs-lookup"><span data-stu-id="5d977-356">Instead, the client thread entry function simply waits on line 368 for the server to set up.</span></span> <span data-ttu-id="5d977-357">L'indirizzo del server e la porta sono impostati, usando le macro dell'ordine dei byte dell'host alla rete nelle righe 387-392, quindi il client può connettersi al server TCP alla riga 412.</span><span class="sxs-lookup"><span data-stu-id="5d977-357">The server address and port are set, using the host to network byte order macros on lines 387-392, and then the Client can connect with the TCP server on line 412.</span></span> <span data-ttu-id="5d977-358">Si noti che i tipi di dati degli indirizzi IP locali nelle righe 378-383 vengono usati solo per illustrare rispettivamente i servizi *getsockname* e *getpeername* sulle righe 425 e 434.</span><span class="sxs-lookup"><span data-stu-id="5d977-358">Note that the local IP address data types in lines 378-383 are used only to demonstrate the *getsockname* and *getpeername* services on lines 425 and 434 respectively.</span></span> <span data-ttu-id="5d977-359">Poiché i dati provengono dalla rete, la rete deve ospitare le macro dell'ordine dei byte, come usato nelle righe 378-383.</span><span class="sxs-lookup"><span data-stu-id="5d977-359">Because the data is coming from the network, the network to host byte order macros as used in lines 378-383.</span></span>

<span data-ttu-id="5d977-360">Successivamente la funzione di immissione thread del client entra in un ciclo in cui viene creato un socket TCP, effettua una connessione TCP e invia e riceve i dati con il server TCP fino a quando non vengono ricevuti più dati praticamente identici a quelli dell'esempio IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d977-360">Next the client thread entry function enters a loop in which it creates a TCP socket, makes a TCP connection and sends and receives data with the TCP server until no more data is received virtually the same as the IPv4 example.</span></span> <span data-ttu-id="5d977-361">Il socket viene quindi chiuso alla riga 483, viene sospesa brevemente e viene creato un altro socket TCP e viene richiesta una connessione al server TCP.</span><span class="sxs-lookup"><span data-stu-id="5d977-361">It then closes the socket on line 483, pauses briefly and creates another TCP socket and requests a TCP server connection.</span></span>

<span data-ttu-id="5d977-362">Una differenza importante con l'esempio IPv4 è che le chiamate *socket* specificano un socket IPv6 usando l'argomento di input AF_INET6.</span><span class="sxs-lookup"><span data-stu-id="5d977-362">One important difference with the IPv4 example is the *socket* calls specify an IPv6 socket using the AF_INET6 input argument.</span></span> <span data-ttu-id="5d977-363">Un'altra differenza importante è che la chiamata di *connessione* del client TCP accetta un tipo di dati *sockaddr_in6* e un argomento length impostato sulla dimensione del tipo di dati *sockaddr_in6* .</span><span class="sxs-lookup"><span data-stu-id="5d977-363">Another important difference is that the TCP Client *connect* call takes an *sockaddr_in6* data type and a length argument set to the size of the *sockaddr_in6* data type.</span></span>

```c
/* This is a small demo of BSD Wrapper for the high-performance NetX Duo
TCP/IP stack which uses standard BSD services for TCP connection,
disconnection, sending, and receiving using a simulated Ethernet driver. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nxd_bsd.h"
#include     <string.h>
#include     <stdlib.h>

#define     DEMO_STACK_SIZE     (16*1024)
#define     SERVER_PORT         87
#define     CLIENT_PORT         77

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_server;
TX_THREAD         thread_client;
NX_PACKET_POOL    bsd_pool;
NX_IP             bsd_ip;

/* Define some global data. */
CHAR     *msg0 = "Client 1:
    ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<>END";

INT     maxfd;

/* Define the counters used in the demo application... */
ULONG     error_counter;

/* Define fd_sets for the BSD server socket. */
fd_set     master_list, read_ready;

/* Define thread prototypes. */
VOID     thread_server_entry(ULONG thread_input);
VOID     thread_client_entry(ULONG thread_input);
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

int     main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void tx_application_define(void *first_unused_memory)
{
CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create a server thread. */
    tx_thread_create(&thread_server, "Server", thread_server_entry, 0,
                    pointer, DEMO_STACK_SIZE, 8, 8,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Create a Client thread. */
    tx_thread_create(&thread_client, "Client", thread_client_entry, 0,
                    pointer, DEMO_STACK_SIZE, 16, 16,
                    TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a BSD packet pool. */
    status = nx_packet_pool_create(&bsd_pool, "NetX BSD Packet Pool",
    128, pointer, 16384);

    pointer = pointer + 16384;

    if (status)
    {
        error_counter++;
        printf("Error in creating BSD packet pool\n!");
    }

    /* Create an IP instance for BSD. */
    status = nx_ip_create(&bsd_ip, "BSD IP Instance", IP_ADDRESS(1,2,3,4),
                        0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                        pointer, 2048, 1);
                        pointer = pointer + 2048;

    if (status)
    {
        error_counter++;
        printf("Error creating BSD IP instance\n!");
    }

    /* Enable ARP and supply ARP cache memory for BSD IP Instance */
    status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check ARP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in enable ARP on BSD IP instance\n");
    }

    /* Enable TCP processing for BSD IP instances. */
    status = nx_tcp_enable(&bsd_ip);

    /* Check TCP enable status. */
    if (status)
    {
        error_counter++;
        printf("Error in Enable TCP \n");
    }

    /* Now initialize BSD Scoket Wrapper */
    status = bsd_initialize(&bsd_ip, &bsd_pool,pointer, 2048, 2);

    /* Check BSD initialize status. */
    if (status)
    {
        error_counter++;
        printf("Error in BSD initialize \n");
    }

    pointer = pointer + 2048;
}

/* Define the Server thread. */
CHAR     Server_Rcv_Buffer[100];

VOID     thread_server_entry(ULONG thread_input)
{

INT             status, sock, sock_tcp_server;
ULONG           actual_status;
INT             Clientlen;
INT             i;
UINT            is_set = NX_FALSE;
NXD_ADDRESS     ip_address;
struct          sockaddr_in6 serverAddr;
struct          sockaddr_in6 ClientAddr;
UINT            iface_index, address_index;

    status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE,
            &actual_status, 100);

    /* Check status... */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable IPv6 */
    status = nxd_ipv6_enable(&bsd_ip);
    if((status != NX_SUCCESS) && (status != NX_ALREADY_ENABLED))
    {
        printf("Error with IPv6 enable 0x%x\n", status);
        return;
    }

    /* Enable ICMPv6 */
    status = nxd_icmp_enable(&bsd_ip);

    if(status)
    {
        printf("Error with ECMPv6 enable 0x%x\n", status);
        return;
    }

    /* Set the primary interface for our DNS IPv6 addresses. */
    iface_index = 0;

    /* This assumes we are using the primary network interface (index 0). */
    status = nxd_ipv6_address_set(&bsd_ip, iface_index, NX_NULL, 10,
                                &address_index);

    if (status)
        return;

    /* Set ip_0 interface address. */
    ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    ip_address.nxd_ip_address.v6[0] = htonl(0x20010db8);
    ip_address.nxd_ip_address.v6[1] = htonl(0x0000f101);
    ip_address.nxd_ip_address.v6[2] = 0;
    ip_address.nxd_ip_address.v6[3] = htonl(0x101);

    /* Set the host global IP address. We are assuming a 64
    bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&bsd_ip, iface_index, &ip_address, 64,
                                &address_index);

    if (status)
        return;

    /* Wait for IPv6 stack to finish DAD process. */
    tx_thread_sleep(400);

    /* Create BSD TCP Socket */
    sock_tcp_server = socket(AF_INET6, SOCK_STREAM, 0);

    if (sock_tcp_server == -1)
    {
        printf("\nError: BSD TCP Server socket create \n");
        return;
    }

    printf("\nBSD TCP Server socket created %lu \n", sock_tcp_server);

    /* Set the server port and IP address */
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    serverAddr.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    serverAddr.sin6_addr._S6_un._S6_u32[2] = 0x0;
    serverAddr.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    serverAddr.sin6_port = htons(SERVER_PORT);
    serverAddr.sin6_family = AF_INET6;

    /* Bind this server socket */
    status = bind(sock_tcp_server, (struct sockaddr *) &serverAddr,
                    sizeof(serverAddr));

    if (status < 0)
    {
        printf("Error: Server Socket Bind \n");
        return;
    }

    FD_ZERO(&master_list);
    FD_ZERO(&read_ready);
    FD_SET(sock_tcp_server,&master_list);
    maxfd = sock_tcp_server;

    /* Now listen for any client connections for this server socket */
    status = listen(sock_tcp_server, 5);
    if (status < 0)
    {
        printf("Error: Server Socket Listen\n");
        return;
    }
    else
        printf("Server Listen complete\n");

    /* All set to accept client connections */
    printf("Now accepting client connections\n");

    /* Loop to create and establish server connections. */
    while(1)
    {

        printf("\n");

        read_ready = master_list;

        tx_thread_sleep(20); /* Allow some time to other threads too */

        /* Let the underlying TCP stack determine the timeout. */
        status = select(maxfd + 1, &read_ready, 0, 0, 0);

        if ( (status == 0xFFFFFFFF) || (status == 0) )
        {
            printf("Error with select? Status 0x%x. Try again\n", status);

            continue;
        }

        /* Detected a connection request. */
        is_set = FD_ISSET(sock_tcp_server,&read_ready);

        if(is_set)
        {

            Clientlen = sizeof(ClientAddr);

            sock = accept(sock_tcp_server,
            (struct sockaddr*)&ClientAddr,
            &Clientlen);

            /* Add this new connection to our master list */
            FD_SET(sock, &master_list);

            if ( sock \maxfd)
            {
                printf("New connection %d\n", sock);

                maxfd = sock;
            }

            continue;
        }

        /* Check the set of 'ready' sockets, e.g connected to remote host and
        waiting for notice of packets received. */
        for (i = NX_BSD_SOCKFD_START; i < (maxfd+1+NX_BSD_SOCKFD_START); i++)
        {

            if ((i != sock_tcp_server) &&
                (FD_ISSET(i, &master_list)) &&
                (FD_ISSET(i, &read_ready)))
            {

                while(1)
                {

                    status = recv(i, (VOID *)Server_Rcv_Buffer, 100, 0);

                    if (status == 0)
                    {
                        printf("(Server socket %d received no data from
                                Client)\n", i);

                        break;
                    }
                    else if (status == 0xFFFFFFFF)
                    {
                        printf("Error on Server socket %d receiving data from
                                Client\n", i);

                        break;
                    }

                    printf("Server socket %d received from Client %lu bytes:
                            %s\n ", i, (ULONG)status,
                            Server_Rcv_Buffer);

                    status = send(i, "Hello\n", sizeof("Hello\n"), 0);

                    if (status == ERROR)
                    {
                        printf("Error on Server socket %d sending data to
                                Client \n", i);
                    }
                    else
                    {
                        printf("Server socket %d message sent to Client:
                                Hello\n", i);
                    }
                }

                /* Close this socket */
                status = soc_close(i);

                if (status != ERROR)
                {
                    printf("Server socket %d closing\n", i);
                }
                else
                {

                    printf("Error on Server socket %d closing\n", i);
                }
            }
        }

        /* Loop back to check any next client connection */
    }
}

#define     CLIENT_BUFFER_SIZE 100
CHAR        Client_Rcv_Buffer[CLIENT_BUFFER_SIZE];

VOID        thread_client_entry(ULONG thread_input)
{

INT         status;
INT         sock_tcp_client, length;
struct      sockaddr_in6 echoServAddr6;
struct      sockaddr_in6 localAddr6; address */

    /* Wait for the server side to get set up, including the DAD process. */
    tx_thread_sleep(500);

    /* ICMPv6 and IPv6 should already be enabled on the IP instance
    by the server thread entry function. */

    /* Further the IPv6 address is already established with the IP instance.
    so no need to wait for DAD completion. */

    /* Set local port and IP address (used only for getsockname call). */
    memset(&localAddr6, 0, sizeof(localAddr6));
    localAddr6.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    localAddr6.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    localAddr6.sin6_addr._S6_un._S6_u32[2] = 0x0;
    localAddr6.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    localAddr6.sin6_port = htons(CLIENT_PORT);
    localAddr6.sin6_family = AF_INET6;

    /* Set Server port and IP address to connect to the TCP server. */
    memset(&echoServAddr6, 0, sizeof(echoServAddr6));
    echoServAddr6.sin6_addr._S6_un._S6_u32[0] = htonl(0x20010db8);
    echoServAddr6.sin6_addr._S6_un._S6_u32[1] = htonl(0xf101);
    echoServAddr6.sin6_addr._S6_un._S6_u32[2] = 0x0;
    echoServAddr6.sin6_addr._S6_un._S6_u32[3] = htonl(0x0101);
    echoServAddr6.sin6_port = htons(SERVER_PORT);
    echoServAddr6.sin6_family = AF_INET6;

    /* Now make client connections with the server. */
    while (1)
    {
        printf("\n");

        /* Create BSD TCP Socket */

        sock_tcp_client = socket(AF_INET6, SOCK_STREAM, 0);

        if (sock_tcp_client == -1)
        {
            printf("Error on Client socket %d create \n");
            return;
        }

        printf("Client socket %d created \n", sock_tcp_client);

        /* Now connect this client to the server */
        status = connect(sock_tcp_client, (struct sockaddr *)&echoServAddr6,
                sizeof(echoServAddr6));

        /* Check for error. */
        if (status != NX_SOC_OK)
        {
            printf("Error on Client socket %d connect\n");
            soc_close(sock_tcp_client);
            return;

        }

        /* Get and print source and destination information */
        printf("Client socket %d connected \n", sock_tcp_client);

        status = getsockname(sock_tcp_client, (struct sockaddr *)&localAddr6,
        &length);

        printf("Client port = %lu , Client = 0x%x 0x%x 0x%x 0x%x,",
                ntohs(localAddr6.sin6_port),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[0]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[1]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[2]),
                ntohl(localAddr6.sin6_addr._S6_un._S6_u32[3]));

        length = sizeof(struct sockaddr_in6);

        status = getpeername(sock_tcp_client, (struct sockaddr *)
                            &echoServAddr6, &length);

        printf("Remote port = %lu, Remote IP = 0x%x 0x%x 0x%x 0x%x \n",
                ntohs(echoServAddr6.sin6_port),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[0]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[1]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[2]),
                ntohl(echoServAddr6.sin6_addr._S6_un._S6_u32[3]));

        /* Now receive the echoed packet from the server */
        while(1)
        {

            printf("Client sock %d sending packet to server\n",
                sock_tcp_client);

            status = send(sock_tcp_client, "Hello", sizeof("Hello"), 0);

            if (status == NX_SOC_ERROR)
            {
                printf("Error on Client Socket (%d) send \n",
                        sock_tcp_client);
            }
            else
            {
                printf("Client socket %d sent message: Hello\n",
                        sock_tcp_client);
            }

            status = recv(sock_tcp_client, (VOID *)Client_Rcv_Buffer,
                        CLIENT_BUFFER_SIZE, 0);

            if (status <= 0)
            {

                if (status < 0)
                {
                    printf("Error on Client receiving on socket %d \n",
                            sock_tcp_client);
                }
                else
                {
                    printf("Client received no data on socket %d\n",
                            sock_tcp_client);
                }

            break;
            }
            else
            {
                printf("Client socket %d received %d bytes and this message:
                        %s\n", sock_tcp_client, status,
                        Client_Rcv_Buffer);
            }

        }

        /* close this client socket */
        status = oc_close(sock_tcp_client);

        if (status != NX_SOC_ERROR)
        {
            printf("Client Socket %d closed\n", sock_tcp_client);
        }
        else
        {
            printf("Error on Client Socket %d on close \n", sock_tcp_client);
        }

        /* Make another Client connection...*/

    }
}
```
