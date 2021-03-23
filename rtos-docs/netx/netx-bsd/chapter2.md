---
title: Capitolo 2-installazione e uso di Azure RTO NetX BSD
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente RTO NetX BSD di Azure.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7539565ccd4956c5354be45000efab8318dc606c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822748"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-bsd"></a><span data-ttu-id="35a9e-103">Capitolo 2-installazione e uso di Azure RTO NetX BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-103">Chapter 2 - Installation and Use of Azure RTOS NetX BSD</span></span>

<span data-ttu-id="35a9e-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente RTO NetX BSD di Azure.</span><span class="sxs-lookup"><span data-stu-id="35a9e-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX BSD component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="35a9e-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="35a9e-105">Product Distribution</span></span>

<span data-ttu-id="35a9e-106">È possibile ottenere Azure RTO NetX BSD dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="35a9e-106">Azure RTOS NetX BSD can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="35a9e-107">Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="35a9e-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="35a9e-108">**nx_bsd. h**: file di intestazione per NETX BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-108">**nx_bsd.h**: Header file for NetX BSD</span></span>
- <span data-ttu-id="35a9e-109">**nx_bsd. c**: file di origine c per NETX BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-109">**nx_bsd.c**: C Source file for NetX BSD</span></span>
- <span data-ttu-id="35a9e-110">**nx_bsd.pdf**: manuale dell'utente per NETX BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-110">**nx_bsd.pdf**: User Guide for NetX BSD</span></span>

<span data-ttu-id="35a9e-111">File demo:</span><span class="sxs-lookup"><span data-stu-id="35a9e-111">Demo files:</span></span>
- <span data-ttu-id="35a9e-112">**bsd_demo_tcp. c**</span><span class="sxs-lookup"><span data-stu-id="35a9e-112">**bsd_demo_tcp.c**</span></span>
- <span data-ttu-id="35a9e-113">**bsd_demo_udp. c**</span><span class="sxs-lookup"><span data-stu-id="35a9e-113">**bsd_demo_udp.c**</span></span>

## <a name="netx-bsd-installation"></a><span data-ttu-id="35a9e-114">Installazione di NetX BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-114">NetX BSD Installation</span></span>

<span data-ttu-id="35a9e-115">Per poter usare NetX BSD, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="35a9e-115">In order to use NetX BSD the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="35a9e-116">Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_bsd. h* e *nx_bsd. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="35a9e-116">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_bsd.h* and *nx_bsd.c* files should be copied into this directory.</span></span>

## <a name="building-the-threadx-and-netx-components-of-a-bsd-application"></a><span data-ttu-id="35a9e-117">Compilazione dei componenti ThreadX e NetX di un'applicazione BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-117">Building the ThreadX and NetX components of a BSD Application</span></span>

### <a name="threadx"></a><span data-ttu-id="35a9e-118">ThreadX</span><span class="sxs-lookup"><span data-stu-id="35a9e-118">ThreadX</span></span>

<span data-ttu-id="35a9e-119">La libreria ThreadX deve definire *bsd_errno* nell'archiviazione locale di thread.</span><span class="sxs-lookup"><span data-stu-id="35a9e-119">The ThreadX library must define *bsd_errno* in the thread local storage.</span></span> <span data-ttu-id="35a9e-120">Si consiglia la seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="35a9e-120">We recommend the following procedure:</span></span>

1. <span data-ttu-id="35a9e-121">In *tx_port. h*, impostare una delle macro TX_THREAD_EXTENSION come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="35a9e-121">In *tx_port.h*, set one of the TX_THREAD_EXTENSION macros as follows:</span></span>

  ```c
  #define TX_THREAD_EXTENSION_3     int bsd_errno
  ```

2. <span data-ttu-id="35a9e-122">Ricompilare la libreria ThreadX.</span><span class="sxs-lookup"><span data-stu-id="35a9e-122">Rebuild the ThreadX library.</span></span>

> [!NOTE]
> <span data-ttu-id="35a9e-123">Se TX_THREAD_EXTENSION_3 è già in uso, l'utente è libero di usare una delle altre macro TX_THREAD_EXTENSION.</span><span class="sxs-lookup"><span data-stu-id="35a9e-123">If TX_THREAD_EXTENSION_3 is already used, the user is free to use one of the other TX_THREAD_EXTENSION macros.</span></span>

### <a name="netx"></a><span data-ttu-id="35a9e-124">NetX</span><span class="sxs-lookup"><span data-stu-id="35a9e-124">NetX</span></span>

<span data-ttu-id="35a9e-125">Prima di usare NetX BSD Services, è necessario compilare la libreria NetX con NX_ENABLE_EXTENDED_NOTIFY_SUPPORT definito (ad esempio, in *nx_user. h*).</span><span class="sxs-lookup"><span data-stu-id="35a9e-125">Before using NetX BSD Services, the NetX library must be built with NX_ENABLE_EXTENDED_NOTIFY_SUPPORT defined (e.g. in *nx_user.h*).</span></span> <span data-ttu-id="35a9e-126">Per impostazione predefinita, non è definito.</span><span class="sxs-lookup"><span data-stu-id="35a9e-126">By default it is not defined.</span></span>

## <a name="using-netx-bsd"></a><span data-ttu-id="35a9e-127">Uso di NetX BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-127">Using NetX BSD</span></span>

<span data-ttu-id="35a9e-128">L'uso di BSD per NetX è facile.</span><span class="sxs-lookup"><span data-stu-id="35a9e-128">Using BSD for NetX is easy.</span></span> <span data-ttu-id="35a9e-129">In pratica, il codice dell'applicazione deve includere *nx_bsd. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX.</span><span class="sxs-lookup"><span data-stu-id="35a9e-129">Basically, the application code must include *nx_bsd.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="35a9e-130">Una volta incluso *nx_bsd. h* , il codice dell'applicazione è in grado di usare i servizi BSD specificati più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="35a9e-130">Once *nx_bsd.h* is included, the application code is then able to use the BSD services specified later in this guide.</span></span> <span data-ttu-id="35a9e-131">Nell'applicazione deve inoltre essere incluso *nx_bsd. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="35a9e-131">The application must also include *nx_bsd.c* in the build process.</span></span> <span data-ttu-id="35a9e-132">Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35a9e-132">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="35a9e-133">Questo è tutto ciò che è necessario per usare NetX BSD.</span><span class="sxs-lookup"><span data-stu-id="35a9e-133">This is all that is required to use NetX BSD.</span></span>

<span data-ttu-id="35a9e-134">Per usare i servizi NetX BSD, l'applicazione deve creare un'istanza IP, un pool di pacchetti e inizializzare i servizi BSD chiamando *bsd_initialize.*</span><span class="sxs-lookup"><span data-stu-id="35a9e-134">To utilize NetX BSD services, the application must create an IP instance, a packet pool, and initialize BSD services by calling *bsd_initialize.*</span></span> <span data-ttu-id="35a9e-135">Questa procedura è illustrata nella sezione "piccolo esempio" più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="35a9e-135">This is demonstrated in the "Small Example" section later in this guide.</span></span> <span data-ttu-id="35a9e-136">Il prototipo è illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="35a9e-136">The prototype is shown below:</span></span>

```c
INT bsd_initialize(NX_IP *default_ip, NX_PACKET_POOL *default_pool,
                  CHAR *free_memory_ptr, ULONG bsd_thread_stack_size,
                  UINT bsd_thread_priority);
```

<span data-ttu-id="35a9e-137">Gli ultimi tre parametri vengono utilizzati per la creazione di un thread per eseguire attività periodiche, ad esempio la verifica degli eventi TCP e la definizione dello spazio dello stack dei thread.</span><span class="sxs-lookup"><span data-stu-id="35a9e-137">The last three parameters are used for creating a thread for performing periodic tasks such as checking for TCP events and define the thread stack space.</span></span>

> [!NOTE]
> <span data-ttu-id="35a9e-138">A differenza dei socket BSD, che funzionano nell'ordine di rete bye, NetX funziona nell'ordine dei byte dell'host del processore host.</span><span class="sxs-lookup"><span data-stu-id="35a9e-138">In contrast to BSD sockets, which work in network bye order, NetX works in the host byte order of the host processor.</span></span> <span data-ttu-id="35a9e-139">Per motivi di compatibilità con l'origine, le macro htons (), ntohs (), htonl (), ntohl () sono state definite, ma non modificano l'argomento passato.</span><span class="sxs-lookup"><span data-stu-id="35a9e-139">For source compatibility reasons, the macros htons(), ntohs(), htonl(), ntohl() have been defined, but do not modify the argument passed.</span></span>

## <a name="netx-bsd-limitations"></a><span data-ttu-id="35a9e-140">Limitazioni di NetX BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-140">NetX BSD Limitations</span></span>

<span data-ttu-id="35a9e-141">A causa di problemi relativi alle prestazioni e all'architettura, NetX BSD non supporta tutte le funzionalità socket di BSD 4,3:</span><span class="sxs-lookup"><span data-stu-id="35a9e-141">Due to performance and architecture issues, NetX BSD does not support all the BSD 4.3 socket features:</span></span>

<span data-ttu-id="35a9e-142">I flag INT non sono supportati per le chiamate *Send, ricezione, SendTo* e *recvfrom* .</span><span class="sxs-lookup"><span data-stu-id="35a9e-142">INT flags are not supported for *send, recv, sendto* and *recvfrom* calls.</span></span>

## <a name="netx-bsd-with-dns-support"></a><span data-ttu-id="35a9e-143">NetX BSD con supporto DNS</span><span class="sxs-lookup"><span data-stu-id="35a9e-143">NetX BSD with DNS Support</span></span>

<span data-ttu-id="35a9e-144">Se NX_BSD_ENABLE_DNS è stato definito, NetX BSD può inviare query DNS per ottenere informazioni sul nome host o sull'indirizzo IP dell'host.</span><span class="sxs-lookup"><span data-stu-id="35a9e-144">If NX_BSD_ENABLE_DNS is defined, NetX BSD can send DNS queries to obtain hostname or host IP information.</span></span> <span data-ttu-id="35a9e-145">Questa funzionalità richiede che un client DNS NetX venga creato in precedenza usando il servizio *nx_dns_create* .</span><span class="sxs-lookup"><span data-stu-id="35a9e-145">This feature requires a NetX DNS Client to be previously created using the *nx_dns_create* service.</span></span> <span data-ttu-id="35a9e-146">Uno o più indirizzi IP del server DNS noti devono essere registrati con l'istanza DNS usando il *nx_dns_server_add* per l'aggiunta degli indirizzi del server.</span><span class="sxs-lookup"><span data-stu-id="35a9e-146">One or more known DNS server IP addresses must be registered with the DNS instance using the *nx_dns_server_add* for adding server addresses.</span></span>

<span data-ttu-id="35a9e-147">I servizi DNS e l'allocazione di memoria vengono usati dai servizi *funzione getaddrinfo* e *GetNameInfo* :</span><span class="sxs-lookup"><span data-stu-id="35a9e-147">DNS services and memory allocation are used by *getaddrinfo* and *getnameinfo* services:</span></span>

```c
INT getaddrinfo(const CHAR *node, const CHAR *service,
              const struct addrinfo *hints, struct addrinfo **res)

INT getnameinfo(const struct sockaddr *sa, socklen_t salen,
              char *host, size_t hostlen, char *serv, size_t servlen, int flags)
```

<span data-ttu-id="35a9e-148">Quando l'applicazione BSD chiama *funzione getaddrinfo* con un nome host, NETX BSD chiamerà uno dei servizi seguenti per ottenere l'indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="35a9e-148">When the BSD application calls *getaddrinfo* with a hostname, NetX BSD will call any of the below services to obtain the IP address:</span></span>

- <span data-ttu-id="35a9e-149">nx_dns_ipv4_address_by_name_get</span><span class="sxs-lookup"><span data-stu-id="35a9e-149">nx_dns_ipv4_address_by_name_get</span></span>
- <span data-ttu-id="35a9e-150">nx_dns_cname_get</span><span class="sxs-lookup"><span data-stu-id="35a9e-150">nx_dns_cname_get</span></span>

<span data-ttu-id="35a9e-151">Per *nx_dns_ipv4_address_by_name_get*, NETX BSD usa le aree di memoria ipv4_addr_buffer.</span><span class="sxs-lookup"><span data-stu-id="35a9e-151">For *nx_dns_ipv4_address_by_name_get*, NetX BSD uses the ipv4_addr_buffer memory areas.</span></span> <span data-ttu-id="35a9e-152">Le dimensioni di questi buffer sono definite da ( `NX_BSD_IPV4_ADDR_PER_HOST * 4` ).</span><span class="sxs-lookup"><span data-stu-id="35a9e-152">The size of these buffers are defined by (`NX_BSD_IPV4_ADDR_PER_HOST * 4`).</span></span>

<span data-ttu-id="35a9e-153">Per restituire le informazioni sull'indirizzo da *funzione getaddrinfo*, NETX BSD usa la tabella di memoria a blocchi threadX *nx_bsd_addrinfo_pool_memory*, la cui area di memoria è definita da un altro set di opzioni configurabili, *NX_BSD_IPV4_ADDR_MAX_NUM*.</span><span class="sxs-lookup"><span data-stu-id="35a9e-153">For returning address information from *getaddrinfo*, NetX BSD uses the ThreadX block memory table *nx_bsd_addrinfo_pool_memory*, whose memory area is defined by another set of configurable options, *NX_BSD_IPV4_ADDR_MAX_NUM*.</span></span>

<span data-ttu-id="35a9e-154">Per ulteriori informazioni sulle opzioni di configurazione precedenti, vedere **Opzioni di configurazione** .</span><span class="sxs-lookup"><span data-stu-id="35a9e-154">See **Configuration Options** for more details on the above configuration options.</span></span>

<span data-ttu-id="35a9e-155">Inoltre, se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito e l'input dell'host è un nome canonico, NetX BSD alloca la memoria in modo dinamico da un pool di blocchi creato in precedenza *_nx_bsd_cname_block_pool*</span><span class="sxs-lookup"><span data-stu-id="35a9e-155">Additionally, if NX_DNS_ENABLE_EXTENDED_RR_TYPES is defined, and the host input is a canonical name, NetX BSD will allocate memory dynamically from a previously created block pool *_nx_bsd_cname_block_pool*</span></span>

> [!NOTE]
> <span data-ttu-id="35a9e-156">Dopo la chiamata a *funzione getaddrinfo* , l'applicazione BSD è responsabile del rilascio della memoria a cui fa riferimento l'argomento res alla tabella dei blocchi usando il servizio *FreeAddrInfo* .</span><span class="sxs-lookup"><span data-stu-id="35a9e-156">After calling *getaddrinfo* the BSD application is responsible for releasing the memory pointed to by the res argument back to the block table using the *freeaddrinfo* service.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="35a9e-157">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="35a9e-157">Configuration Options</span></span>

<span data-ttu-id="35a9e-158">Le opzioni configurabili dall'utente in *nx_bsd. h* consentono all'applicazione di ottimizzare i socket NETX BSD per i requisiti specifici.</span><span class="sxs-lookup"><span data-stu-id="35a9e-158">User configurable options in *nx_bsd.h* allow the application to fine tune NetX BSD sockets for its particular requirements.</span></span> <span data-ttu-id="35a9e-159">Di seguito è riportato un elenco di questi parametri:</span><span class="sxs-lookup"><span data-stu-id="35a9e-159">The following is a list of these parameters:</span></span>

- <span data-ttu-id="35a9e-160">**NX_BSD_TCP_WINDOW**: utilizzato nelle chiamate di creazione socket TCP.</span><span class="sxs-lookup"><span data-stu-id="35a9e-160">**NX_BSD_TCP_WINDOW**: Used in TCP socket create calls.</span></span> <span data-ttu-id="35a9e-161">65535 è una tipica dimensione della finestra per Ethernet 100Mb.</span><span class="sxs-lookup"><span data-stu-id="35a9e-161">65535 is a typical window size for 100Mb Ethernet.</span></span> <span data-ttu-id="35a9e-162">Il valore predefinito è 65535.</span><span class="sxs-lookup"><span data-stu-id="35a9e-162">The default value is 65535.</span></span>
- <span data-ttu-id="35a9e-163">**NX_BSD_SOCKFD_START** Si tratta dell'indice logico per il valore iniziale del descrittore del file socket BSD.</span><span class="sxs-lookup"><span data-stu-id="35a9e-163">**NX_BSD_SOCKFD_START** This is the logical index for the BSD socket file descriptor start value.</span></span> <span data-ttu-id="35a9e-164">Per impostazione predefinita, questa opzione è 32.</span><span class="sxs-lookup"><span data-stu-id="35a9e-164">By default this option is 32.</span></span>
- <span data-ttu-id="35a9e-165">**NX_BSD_MAX_SOCKETS** Specifica il numero massimo di socket totali disponibili nel livello BSD e deve essere un multiplo di 32. per impostazione predefinita, il valore è 32.</span><span class="sxs-lookup"><span data-stu-id="35a9e-165">**NX_BSD_MAX_SOCKETS** Specifies the maximum number of total sockets available in the BSD layer and must be a multiple of 32.The value is defaulted to 32.</span></span>
- <span data-ttu-id="35a9e-166">**NX_BSD_SOCKET_QUEUE_MAX** Specifica il numero massimo di pacchetti UDP archiviati nella coda del socket di ricezione.</span><span class="sxs-lookup"><span data-stu-id="35a9e-166">**NX_BSD_SOCKET_QUEUE_MAX** Specifies the maximum number of UDP packets stored on the receive socket queue.</span></span> <span data-ttu-id="35a9e-167">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="35a9e-167">The value is defaulted to 5.</span></span>
- <span data-ttu-id="35a9e-168">**NX_BSD_MAX_LISTEN_BACKLOG** Specifica le dimensioni della coda di ascolto (' backlog ') per i socket TCP BSD.</span><span class="sxs-lookup"><span data-stu-id="35a9e-168">**NX_BSD_MAX_LISTEN_BACKLOG** This specifies the size of the listen queue ('backlog') for BSD TCP sockets.</span></span> <span data-ttu-id="35a9e-169">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="35a9e-169">The default value is 5.</span></span>
- <span data-ttu-id="35a9e-170">**NX_MICROSECOND_PER_CPU_TICK** Specifica il numero di microsecondi per ogni interrupt del timer</span><span class="sxs-lookup"><span data-stu-id="35a9e-170">**NX_MICROSECOND_PER_CPU_TICK** Specifies the number of microseconds per timer interrupt</span></span>
- <span data-ttu-id="35a9e-171">**NX_BSD_TIMEOUT** Specifica il timeout nei cicli del timer per le chiamate interne NetX richieste da BSD.</span><span class="sxs-lookup"><span data-stu-id="35a9e-171">**NX_BSD_TIMEOUT** Specifies the timeout in timer ticks on NetX internal calls required by BSD.</span></span> <span data-ttu-id="35a9e-172">Il valore predefinito è 20 \* NX_IP_PERIODIC_RATE.</span><span class="sxs-lookup"><span data-stu-id="35a9e-172">The default value is 20\*NX_IP_PERIODIC_RATE.</span></span>
- <span data-ttu-id="35a9e-173">**NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: specifica il timeout nei cicli del timer per la chiamata di disconnessione NETX.</span><span class="sxs-lookup"><span data-stu-id="35a9e-173">**NX_BSD_TCP_SOCKET_DISCONNECT_TIMEOUT**: Specifies the timeout in timer ticks on NetX disconnect call.</span></span> <span data-ttu-id="35a9e-174">Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="35a9e-174">The default value is 1.</span></span>
- <span data-ttu-id="35a9e-175">**NX_BSD_PRINT_ERRORS** Se impostato, lo stato di errore restituito da una funzione BSD restituisce un numero di riga e il tipo di errore, ad esempio NX_SOC_ERROR in cui si è verificato l'errore.</span><span class="sxs-lookup"><span data-stu-id="35a9e-175">**NX_BSD_PRINT_ERRORS** If set, the error status return of a BSD function returns a line number and type of error e.g. NX_SOC_ERROR where the error occurs.</span></span> <span data-ttu-id="35a9e-176">A questo scopo, lo sviluppatore dell'applicazione deve definire l'output di debug.</span><span class="sxs-lookup"><span data-stu-id="35a9e-176">This requires the application developer to define the debug output.</span></span> <span data-ttu-id="35a9e-177">L'impostazione predefinita è disabilitata e non è stato specificato alcun output di debug in *nx_bsd. h*</span><span class="sxs-lookup"><span data-stu-id="35a9e-177">The default setting is disabled and no debug output is specified in *nx_bsd.h*</span></span>
- <span data-ttu-id="35a9e-178">**NX_BSD_TIMER_RATE** Intervallo dopo il quale viene eseguita l'attività del timer periodico BSD.</span><span class="sxs-lookup"><span data-stu-id="35a9e-178">**NX_BSD_TIMER_RATE** Interval after which BSD periodic timer task runs.</span></span> <span data-ttu-id="35a9e-179">Il valore predefinito è 1 secondo (1 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="35a9e-179">The default value is 1 second (1 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="35a9e-180">**NX_BSD_TIMEOUT_PROCESS_IN_TIMER** Se impostata, questa opzione consente l'esecuzione del processo di timeout BSD nel contesto del timer di sistema.</span><span class="sxs-lookup"><span data-stu-id="35a9e-180">**NX_BSD_TIMEOUT_PROCESS_IN_TIMER** If set, this option allows the BSD timeout process to execute in the system timer context.</span></span> <span data-ttu-id="35a9e-181">Il comportamento predefinito è Disabled.</span><span class="sxs-lookup"><span data-stu-id="35a9e-181">The default behavior is disabled.</span></span> <span data-ttu-id="35a9e-182">Questa funzionalità è descritta in modo più dettagliato nel capitolo 2 "installazione e uso di NetX BSD".</span><span class="sxs-lookup"><span data-stu-id="35a9e-182">This feature is described in more detail in Chapter 2 "Installation and Use of NetX BSD".</span></span>
- <span data-ttu-id="35a9e-183">**NX_BSD_ENABLE_DNS** Se abilitata, NetX BSD invierà una query DNS per un nome host o un indirizzo IP host.</span><span class="sxs-lookup"><span data-stu-id="35a9e-183">**NX_BSD_ENABLE_DNS** If enabled, NetX BSD will send a DNS query for a hostname or host IP address.</span></span> <span data-ttu-id="35a9e-184">Richiede che un'istanza del client DNS venga creata e avviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="35a9e-184">Requires a DNS Client instance to be previously created and started.</span></span> <span data-ttu-id="35a9e-185">Per impostazione predefinita, non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="35a9e-185">By default it is not enabled.</span></span>
- <span data-ttu-id="35a9e-186">**NX_BSD_IPV4_ADDR_MAX_NUM** Numero massimo di indirizzi IPv4 restituiti da *funzione getaddrinfo*.</span><span class="sxs-lookup"><span data-stu-id="35a9e-186">**NX_BSD_IPV4_ADDR_MAX_NUM** Maximum number of IPv4 addresses returned by *getaddrinfo*.</span></span> <span data-ttu-id="35a9e-187">Questo insieme a NX_BSD_IPV4_ADDR_MAX_NUM definisce le dimensioni del pool di blocchi di NetX BSD nx_bsd_addrinfo_block_pool per l'allocazione dinamica della memoria per l'archiviazione delle informazioni di indirizzo in *funzione getaddrinfo*.</span><span class="sxs-lookup"><span data-stu-id="35a9e-187">This along with NX_BSD_IPV4_ADDR_MAX_NUM defines the size of the NetX BSD block pool nx_bsd_addrinfo_block_pool for dynamically allocating memory to address information storage in *getaddrinfo*.</span></span> <span data-ttu-id="35a9e-188">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="35a9e-188">The default value is 5.</span></span>
- <span data-ttu-id="35a9e-189">**NX_BSD_IPV4_ADDR_PER_HOST**: definisce il numero massimo di indirizzi IPv4 archiviati per ogni query DNS.</span><span class="sxs-lookup"><span data-stu-id="35a9e-189">**NX_BSD_IPV4_ADDR_PER_HOST**: Defines maximum IPv4 addresses stored per DNS query.</span></span> <span data-ttu-id="35a9e-190">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="35a9e-190">The default value is 5.</span></span>

## <a name="bsd-socket-options"></a><span data-ttu-id="35a9e-191">Opzioni socket BSD</span><span class="sxs-lookup"><span data-stu-id="35a9e-191">BSD Socket Options</span></span>

<span data-ttu-id="35a9e-192">Il seguente elenco di opzioni socket NetX BSD può essere abilitato (o disabilitato) in fase di esecuzione in base a ogni socket usando il servizio *setsockopt* :</span><span class="sxs-lookup"><span data-stu-id="35a9e-192">The following list of NetX BSD socket options can be enabled (or disabled) at run time on a per socket basis using the *setsockopt* service:</span></span>

```c
INT setsockopt(INT sockID, INT option_level, INT option_name, const
                void *option_value, INT option_length);
```

<span data-ttu-id="35a9e-193">Esistono due impostazioni diverse per *option_level*.</span><span class="sxs-lookup"><span data-stu-id="35a9e-193">There are two different settings for *option_level*.</span></span>

<span data-ttu-id="35a9e-194">Il primo tipo di opzioni dei socket di runtime è SOL_SOCKET per le opzioni a livello di socket.</span><span class="sxs-lookup"><span data-stu-id="35a9e-194">The first type of run time socket options is SOL_SOCKET for socket level options.</span></span> <span data-ttu-id="35a9e-195">Per abilitare un'opzione a livello di socket, chiamare *setsockopt* con option_level impostato su SOL_SOCKET e option_name impostato sull'opzione specifica, ad esempio SO_BROADCAST.</span><span class="sxs-lookup"><span data-stu-id="35a9e-195">To enable a socket level option, call *setsockopt* with option_level set to SOL_SOCKET and option_name set to the specific option e.g. SO_BROADCAST.</span></span> <span data-ttu-id="35a9e-196">Per recuperare un'impostazione di opzione, chiamare *getsockopt* per la option_name con option_level di nuovo impostato su SOL_SOCKET.</span><span class="sxs-lookup"><span data-stu-id="35a9e-196">To retrieve an option setting, call *getsockopt* for the option_name with option_level again set to SOL_SOCKET.</span></span>

<span data-ttu-id="35a9e-197">Di seguito è riportato l'elenco delle opzioni del livello di socket del runtime.</span><span class="sxs-lookup"><span data-stu-id="35a9e-197">The list of run time socket level options is shown below.</span></span>

- <span data-ttu-id="35a9e-198">**SO_BROADCAST**: se impostato, consente l'invio e la ricezione di pacchetti broadcast da NETX Sockets.</span><span class="sxs-lookup"><span data-stu-id="35a9e-198">**SO_BROADCAST**: If set, this enables sending and receiving broadcast packets from Netx sockets.</span></span> <span data-ttu-id="35a9e-199">Questo è il comportamento predefinito per NetX.</span><span class="sxs-lookup"><span data-stu-id="35a9e-199">This is the default behavior for NetX.</span></span> <span data-ttu-id="35a9e-200">Questa funzionalità è presente in tutti i socket.</span><span class="sxs-lookup"><span data-stu-id="35a9e-200">All sockets have this capability.</span></span>
- <span data-ttu-id="35a9e-201">**SO_ERROR**: usato per ottenere lo stato del socket per l'operazione socket precedente del socket specificato, usando il servizio *getsockopt* .</span><span class="sxs-lookup"><span data-stu-id="35a9e-201">**SO_ERROR**: Used to obtain socket status on the previous socket operation of the specified socket, using the *getsockopt* service.</span></span> <span data-ttu-id="35a9e-202">Questa funzionalità è presente in tutti i socket.</span><span class="sxs-lookup"><span data-stu-id="35a9e-202">All sockets have this capability.</span></span>
- <span data-ttu-id="35a9e-203">**SO_KEEPALIVE**: se impostato, Abilita la funzionalità TCP keep alive.</span><span class="sxs-lookup"><span data-stu-id="35a9e-203">**SO_KEEPALIVE**: If set, this enables the TCP Keep Alive feature.</span></span> <span data-ttu-id="35a9e-204">A tale scopo, è necessario compilare la libreria NetX con NX_TCP_ENABLE_KEEPALIVE definito in *nx_user. h*.</span><span class="sxs-lookup"><span data-stu-id="35a9e-204">This requires the NetX library to be built with NX_TCP_ENABLE_KEEPALIVE defined in *nx_user.h*.</span></span> <span data-ttu-id="35a9e-205">Per impostazione predefinita, questa funzionalità è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="35a9e-205">By default this feature is disabled.</span></span>
- <span data-ttu-id="35a9e-206">**SO_RCVTIMEO**: imposta l'opzione wait in secondi per la ricezione dei pacchetti nei socket NETX BSD.</span><span class="sxs-lookup"><span data-stu-id="35a9e-206">**SO_RCVTIMEO**: This sets the wait option in seconds for receiving packets on NetX BSD sockets.</span></span> <span data-ttu-id="35a9e-207">Il valore predefinito è il NX_WAIT_FOREVER (0xFFFFFFFF) o, se il blocco non è abilitato, NX_NO_WAIT (0x0).</span><span class="sxs-lookup"><span data-stu-id="35a9e-207">The default value is the NX_WAIT_FOREVER (0xFFFFFFFF) or, if non-blocking is enabled, NX_NO_WAIT (0x0).</span></span>
- <span data-ttu-id="35a9e-208">**SO_RCVBUF**: consente di impostare le dimensioni della finestra del socket TCP.</span><span class="sxs-lookup"><span data-stu-id="35a9e-208">**SO_RCVBUF**: This sets the window size of the TCP socket.</span></span> <span data-ttu-id="35a9e-209">Il valore predefinito, NX_BSD_TCP_WINDOW, è impostato su 64K per i socket TCP BSD.</span><span class="sxs-lookup"><span data-stu-id="35a9e-209">The default value, NX_BSD_TCP_WINDOW, is set to 64k for BSD TCP sockets.</span></span> <span data-ttu-id="35a9e-210">Per impostare la dimensione superiore a 65535, è necessario che la libreria NetX venga compilata con il NX_TCP_ENABLE_WINDOW_SCALING essere definito.</span><span class="sxs-lookup"><span data-stu-id="35a9e-210">To set the size over 65535 requires the NetX library to be built with the NX_TCP_ENABLE_WINDOW_SCALING be defined.</span></span>
- <span data-ttu-id="35a9e-211">**SO_REUSEADDR**: se impostato, consente di eseguire il mapping di più socket a una porta.</span><span class="sxs-lookup"><span data-stu-id="35a9e-211">**SO_REUSEADDR**: If set, this enables multiple sockets to be mapped to one port.</span></span> <span data-ttu-id="35a9e-212">L'utilizzo tipico è per il socket del server TCP.</span><span class="sxs-lookup"><span data-stu-id="35a9e-212">The typical usage is for the TCP Server socket.</span></span> <span data-ttu-id="35a9e-213">Si tratta del comportamento predefinito dei socket NetX.</span><span class="sxs-lookup"><span data-stu-id="35a9e-213">This is the default behavior of NetX sockets.</span></span>

<span data-ttu-id="35a9e-214">Il secondo tipo di opzioni del socket di run-time è il livello di opzione IP.</span><span class="sxs-lookup"><span data-stu-id="35a9e-214">The second type of run time socket options is the IP option level.</span></span> <span data-ttu-id="35a9e-215">Per abilitare un'opzione a livello IP, chiamare *setsockopt* con option_level impostato su IP_PROTO e option_name impostato sull'opzione, ad esempio IP_MULTICAST_TTL.</span><span class="sxs-lookup"><span data-stu-id="35a9e-215">To enable an IP level option, call *setsockopt* with option_level set to IP_PROTO and option_name set to the option e.g. IP_MULTICAST_TTL.</span></span> <span data-ttu-id="35a9e-216">Per recuperare un'impostazione di opzione, chiamare *getsockopt* per la option_name con option_level di nuovo impostato su IP_PROTO.</span><span class="sxs-lookup"><span data-stu-id="35a9e-216">To retrieve an option setting, call *getsockopt* for the option_name with option_level again set to IP_PROTO.</span></span>

<span data-ttu-id="35a9e-217">Di seguito è riportato l'elenco delle opzioni di livello IP di run-time.</span><span class="sxs-lookup"><span data-stu-id="35a9e-217">The list of run time IP level options is shown below.</span></span>

- <span data-ttu-id="35a9e-218">**IP_MULTICAST_TTL**: imposta la durata (TTL) per i socket UDP.</span><span class="sxs-lookup"><span data-stu-id="35a9e-218">**IP_MULTICAST_TTL**: This sets the time to live for UDP sockets.</span></span> <span data-ttu-id="35a9e-219">Il valore predefinito è NX_IP_TIME_TO_LIVE (0x80) al momento della creazione del socket.</span><span class="sxs-lookup"><span data-stu-id="35a9e-219">The default value is NX_IP_TIME_TO_LIVE (0x80) when the socket is created.</span></span> <span data-ttu-id="35a9e-220">È possibile eseguire l'override di questo valore chiamando *setsockopt* con questa opzione socket.</span><span class="sxs-lookup"><span data-stu-id="35a9e-220">This value can be overridden by calling *setsockopt* with this socket option.</span></span>
- <span data-ttu-id="35a9e-221">**IP_ADD_MEMBERSHIP**: se impostata, questa opzione Abilita il socket BSD (si applica solo ai socket UDP) per l'aggiunta al gruppo IGMP specificato.</span><span class="sxs-lookup"><span data-stu-id="35a9e-221">**IP_ADD_MEMBERSHIP**: If set, this options enables the BSD socket (applies only to UDP sockets) to join the specified IGMP group.</span></span>
- <span data-ttu-id="35a9e-222">**IP_DROP_MEMBERSHIP**: se impostata, questa opzione Abilita il socket BSD (si applica solo ai socket UDP) per lasciare il gruppo IGMP specificato.</span><span class="sxs-lookup"><span data-stu-id="35a9e-222">**IP_DROP_MEMBERSHIP**: If set, this options enables the BSD socket (applies only to UDP sockets) to leave the specified IGMP group.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="35a9e-223">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="35a9e-223">Small Example System</span></span>

<span data-ttu-id="35a9e-224">Un esempio di come usare NetX BSD è illustrato nella figura 1,0 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="35a9e-224">An example of how to use NetX BSD is shown in Figure 1.0 below.</span></span> <span data-ttu-id="35a9e-225">In questo esempio il file di inclusione *nx_bsd. h* viene introdotto nella riga 7.</span><span class="sxs-lookup"><span data-stu-id="35a9e-225">In this example, the include file *nx_bsd.h* is brought in at line 7.</span></span> <span data-ttu-id="35a9e-226">Successivamente, l'istanza IP *bsd_ip* e *bsd_pool* pool di pacchetti vengono creati come variabili globali alle righe 20 e 21.</span><span class="sxs-lookup"><span data-stu-id="35a9e-226">Next, the IP instance *bsd_ip* and packet pool *bsd_pool* are created as global variables at line 20 and 21.</span></span> <span data-ttu-id="35a9e-227">Si noti che questa demo usa un driver di rete RAM (virtuale) (riga 41).</span><span class="sxs-lookup"><span data-stu-id="35a9e-227">Note that this demo uses a ram (virtual) network driver (line 41).</span></span> <span data-ttu-id="35a9e-228">Il client e il server condividono lo stesso indirizzo IP in una singola istanza IP in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="35a9e-228">The client and server will share the same IP address on single IP instance in this example.</span></span>

<span data-ttu-id="35a9e-229">I thread client e server vengono creati alla riga 303 e 309 in *tx_application_define* che imposta l'applicazione ed è definita nelle righe 293-361.</span><span class="sxs-lookup"><span data-stu-id="35a9e-229">The client and server threads are created on line 303 and 309 in *tx_application_define* which sets up the application and is defined on lines 293-361.</span></span> <span data-ttu-id="35a9e-230">Al termine della creazione dell'istanza IP alla riga 327, l'istanza IP è abilitata per i servizi TCP alla riga 350.</span><span class="sxs-lookup"><span data-stu-id="35a9e-230">After IP instance successful creation on line 327, the IP instance is enabled for TCP services on line 350.</span></span> <span data-ttu-id="35a9e-231">L'ultimo requisito prima che i servizi BSD possano essere usati è chiamare *bsd_initialize* alla riga 360 per configurare tutte le strutture di dati e NETX e le risorse threadX necessarie per BSD.</span><span class="sxs-lookup"><span data-stu-id="35a9e-231">The last requirement before BSD services can be used is to call *bsd_initialize* on line 360 to set up all data structures and NetX, and ThreadX resources needed by BSD.</span></span>

<span data-ttu-id="35a9e-232">Nella funzione entry thread server *thread_1_entry,* definita nella riga 381-397, l'applicazione attende il driver per inizializzare NETX con i parametri di rete.</span><span class="sxs-lookup"><span data-stu-id="35a9e-232">In the server thread entry function, *thread_1_entry,* which is defined on lines 381-397, the application waits for the driver to initialize NetX with network parameters.</span></span> <span data-ttu-id="35a9e-233">Al termine, viene chiamato *tcpServer,* definito sulla riga 146-253, per gestire i dettagli della configurazione del socket del server TCP.</span><span class="sxs-lookup"><span data-stu-id="35a9e-233">Once this is done, it calls *tcpServer,* defined on lines 146-253, to handle the details of setting up the TCP server socket.</span></span>

<span data-ttu-id="35a9e-234">*tcpServer* crea il socket Master chiamando il servizio *socket* alla riga 159 e lo associa al socket di ascolto usando la chiamata *Bind* alla riga 176.</span><span class="sxs-lookup"><span data-stu-id="35a9e-234">*tcpServer* creates the master socket by calling the *socket* service on line 159 and binds it to the listening socket using the *bind* call on line 176.</span></span> <span data-ttu-id="35a9e-235">Viene quindi configurata per l'ascolto delle richieste di connessione alla riga 191.</span><span class="sxs-lookup"><span data-stu-id="35a9e-235">It is then configured for listening for connection requests on line 191.</span></span> <span data-ttu-id="35a9e-236">Si noti che il socket master non accetta una richiesta di connessione.</span><span class="sxs-lookup"><span data-stu-id="35a9e-236">Note that the master socket does not accept a connection request.</span></span> <span data-ttu-id="35a9e-237">Viene eseguito in un ciclo continuo che chiama *Select* ogni volta per rilevare le richieste di connessione.</span><span class="sxs-lookup"><span data-stu-id="35a9e-237">It runs in a continuous loop which calls *select* each time to detect connection requests.</span></span> <span data-ttu-id="35a9e-238">Al socket BSD secondario scelto da una matrice di socket BSD viene assegnata la richiesta di connessione dopo la chiamata al servizio *Accept* alla riga 218.</span><span class="sxs-lookup"><span data-stu-id="35a9e-238">A secondary BSD socket chosen from an array of BSD sockets is assigned the connection request after calling the *accept* service on line 218.</span></span>

<span data-ttu-id="35a9e-239">Sul lato client, la funzione di immissione thread del client *thread_0_entry*, definita nelle righe 366-377, deve attendere anche che NETX venga inizializzato dal driver.</span><span class="sxs-lookup"><span data-stu-id="35a9e-239">On the Client side, the client thread entry function, *thread_0_entry*, defined on lines 366-377, should also wait for NetX to be initialized by the driver.</span></span> <span data-ttu-id="35a9e-240">Qui attendiamo semplicemente il lato server.</span><span class="sxs-lookup"><span data-stu-id="35a9e-240">Here we just wait for the server side to do so.</span></span> <span data-ttu-id="35a9e-241">Chiama quindi *TcpClient* definito alla riga 54-142, per gestire i dettagli della configurazione del socket del client TCP e la richiesta di una connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="35a9e-241">It then calls *tcpClient* defined on line 54-142, to handle the details of setting up the TCP client socket and requesting a TCP connection.</span></span>

<span data-ttu-id="35a9e-242">Il socket client TCP viene creato alla riga 68.</span><span class="sxs-lookup"><span data-stu-id="35a9e-242">The TCP client socket is created on line 68.</span></span> <span data-ttu-id="35a9e-243">Il socket è associato all'indirizzo IP specificato e tenta di connettersi al server TCP chiamando *Connect* alla riga 84.</span><span class="sxs-lookup"><span data-stu-id="35a9e-243">The socket is bound to the specified IP address and attempts to connect to the TCP server by calling *connect* on line 84.</span></span> <span data-ttu-id="35a9e-244">È ora possibile iniziare l'invio e la ricezione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="35a9e-244">It is now ready to begin sending and receiving packets.</span></span>

```c
1 /*  This is a small demo of BSD Wrapper for the high-performance NetX TCP/IP stack.
2     This demo demonstrate TCP connection, disconnection, sending, and receiving using
3     ARP and a simulated Ethernet driver. */
4
5 #include     "tx_api.h"
6 #include     "nx_api.h"
7 #include     "nx_bsd.h"
8 #include     <string.h>
9 #include     <stdlib.h>
10
11 #define         DEMO_STACK_SIZE         (16*1024)
12
13
14 /* Define the ThreadX and NetX object control blocks... */
15
16 TX_THREAD       thread_0;
17 TX_THREAD       thread_1;
18
19
20 NX_PACKET_POOL  bsd_pool;
21 NX_IP           bsd_ip;
22
23
24 /* Define the counters used in the demo application... */
25
26 ULONG           error_counter;
27
28 /* Define fd_set for select call */
29 fd_set          master_list,read_ready,read_ready1;
30
31
32 /* Define thread prototypes. */
33
34 VOID            thread_0_entry(ULONG thread_input);
35 VOID            thread_1_entry(ULONG thread_input);
36
37 VOID            tcpClient(CHAR *msg0);
38 VOID            tcpServer(VOID);
39 INT             HandleClient(INT sock);
40
41 VOID            _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
42
43
44 /* Define main entry point. */
45
46 int main()
47 {
48
49     /* Enter the ThreadX kernel. */
50     tx_kernel_enter();
51 }
52
53
54 VOID tcpClient(CHAR *msg0)
55 {
56
57 INT     status,status1,send_counter;
58 INT     sock_tcp_1,length,length1;
59 struct  sockaddr_in echoServAddr;       /* Echo server address */
60 struct  sockaddr_in localAddr;          /* Local address */
61 struct  sockaddr_in remoteAddr;         /* Remote address */
62
63 UINT    echoServPort; /* Echo Server Port */
64 CHAR    rcvBuffer1[32]
65
66
67     /* Create BSD TCP Socket */
68     sock_tcp_1 = **socket**( PF_INET, SOCK_STREAM, IPPROTO_TCP);
69     if (sock_tcp_1 == -1)
70     {
71         printf("\nError: BSD TCP Client socket create \n");
72         return;
73     }
74
75     printf("\nBSD TCP Client socket created %lu \n", sock_tcp_1);
76     /* Fill destination port and IP address */
77     echoServPort = 12;
78     memset(&echoServAddr, 0, sizeof(echoServAddr));
79     echoServAddr.sin_family = PF_INET;
80     echoServAddr.sin_addr.s_addr = htonl(0x01020304);
81     echoServAddr.sin_port = echoServPort;
82
83     /* Now connect this client the server */
84     status1 = connect(sock_tcp_1, (struct sockaddr *)&echoServAddr, sizeof(echoServAddr));
85     /* Check for error. */
86     if (status1 != OK)
87     {
88         printf("\nError: BSD TCP Client socket Connect, %d \n",sock_tcp_1);
89         status = soc_close(sock_tcp_1);
90         if (status != ERROR)
91             printf("\nConnect ERROR so BSD Client Socket Closed: %d\n",sock_tcp_1);
92         else
93             printf("\nError: BSD Client Socket close %d\n",sock_tcp_1);
94         return;
95     }
96     /* Get and print source and destination information */
97     printf("\nBSD TCP Client socket: %d connected \n", sock_tcp_1);
98
99     status = getsockname(sock_tcp_1, (struct sockaddr *)&localAddr, &length);
100    printf("Client port = %lu , Client = %lu,", 
            localAddr.sin_port, localAddr.sin_addr.s_addr);
101    status = getpeername( sock_tcp_1, (struct sockaddr *) &remoteAddr, &length1);
102    printf("Remote port = %lu, Remote IP = %lu \n", 
            remoteAddr.sin_port remoteAddr.sin_addr.s_addr);
103
104    send_counter = 1;
105
106    /* Now receive the echoed packet from the server */
107    while(1)
108    {
109        tx_thread_sleep(2);
110
111        printf("\nClient sock: %d Sending packet No: %d to
                server\n",sock_tcp_1,send_counter);
112        status = send(sock_tcp_1,msg0, sizeof(msg0), 0);
113        if (status == ERROR)
114            printf("Error: BSD Client Socket send %d\n",sock_tcp_1);
115        else
116        {
117            printf("\nMessage sent: %s\n",msg0);
118            send_counter++;
119        }
120
121        status = recv(sock_tcp_1, (VOID *)rcvBuffer1, 31,0);
122        if (status == 0)
123            break;
124
125        rcvBuffer1[status] = 0;
126
127        if (status != ERROR)
128            printf("\nBSD Client Socket: %d received %lu bytes: %s ", 
                        sock_tcp_1,(ULONG)status,rcvBuffer1);
129        else
130            printf("\nError: BSD Client Socket receive %d \n",sock_tcp_1);
131
132    }
133
134    /* close this client socket */
135    status = soc_close(sock_tcp_1);
136    if (status != ERROR)
137        printf("\nBSD Client Socket Closed %d\n",sock_tcp_1);
138    else
139        printf("\nError: BSD Client Socket close %d \n",sock_tcp_1);
140
141    /* End */
142 }
143
144
145
146 void tcpServer(void)
147 {
148
149 INT         status,status1,sock,sock_tcp_2,i;
150 struct      sockaddr_in echoServAddr; /* Echo server address */
151 struct      sockaddr_in ClientAddr;
152
153 INT         Clientlen;
154 UINT        echoServPort; /* Echo Server Port */
155
156 INT         maxfd;
157
158 /* Create BSD TCP Server Socket */
159     sock_tcp_2 = socket( PF_INET, SOCK_STREAM, IPPROTO_TCP);
160     if (sock_tcp_2 == -1)
161     {
162         printf("Error: BSD TCP Server socket create\n");
163         return;
164     }
165     else
166         printf("BSD TCP Server socket created \n");
167
168     /* Now fill server side information */
169     echoServPort = 12;
170     memset(&echoServAddr, 0, sizeof(echoServAddr));
171     echoServAddr.sin_family = PF_INET;
172     echoServAddr.sin_addr.s_addr = htonl(0x01020304);
173     echoServAddr.sin_port = echoServPort;
174
175     /* Bind this server socket */
176         status = bind(sock_tcp_2, (struct sockaddr *) &echoServAddr, sizeof(echoServAddr));
177     if (status < 0)
178     {
179         printf("Error: BSD TCP Server Socket Bind \n");
180         return;
181     }
182     else
183         printf("BSD TCP Server Socket bound \n");
184
185     FD_ZERO(&master_list);
186     FD_ZERO(&read_ready);
187     FD_SET(sock_tcp_2,&master_list);
188     maxfd = sock_tcp_2;
189
190     /* Now listen for any client connections for this server socket */
191     status = listen(sock_tcp_2,5);
192     if (status < 0)
193     {
194         printf("Error: BSD TCP Server Socket Listen\n");
195         return;
196     }
197     else
198         printf("BSD TCP Server Socket Listen complete, ");
199
200     /* All set to accept client connections */
201     printf("Now accepting client connections\n");
202
203     /* Loop to create and establish server connections. */
204     while(1)
205     {
206
207         read_ready = master_list;
208         tx_thread_sleep(2); /* Allow some time to other threads too */
209         status = select(maxfd+1,&read_ready,0,0,0);
210         if (status == ERROR)
211         {
212             continue;
213         }
214
215         status = FD_ISSET(sock_tcp_2,&read_ready);
216         if(status)
217         {
218             sock = accept(sock_tcp_2,(struct sockaddr*)&ClientAddr, &Clientlen);
219
220             /* Add this new connection to our master list */
221             FD_SET(sock,&master_list);
222             if ( sock \maxfd)
223             {
224                 maxfd = sock;
225             }
226
227             continue;
228         }
229         for (i = 0; i < (maxfd+1); i++)
230         {
231             if (( i != sock_tcp_2) && (FD_ISSET(i,&master_list)) && 
                    (FD_ISSET(i,&read_ready)))
232             {
233                 status1 = HandleClient(i);
234                 if (status1 == 0)
235                 {
236                     status1 = soc_close(i);
237                     if (status1 == OK)
238                     {
239                         FD_CLR(i,&master_list);
240                         printf("\nBSD Server Socket:%d closed\n",i);
241                     }
242                     else
243                         printf("\nError:BSD Server Socket:%d close\n",i);
244                 }
245
246             }
247         }
248
249         /* Loop back to check any next client connection */
250
251     } /* While(1) ends */
252
253 }
254
255 CHAR     rcvBuffer[128];
256
257 INT     HandleClient(INT sock)
258 {
259
260 INT     status;
261
262
263     status = recv(sock, (VOID *)rcvBuffer, 128,0);
264     if (status == ERROR )
265     {
266         printf("\n BSD Server Socket:%d receive \n",sock);
267         return(ERROR);
268     }
269
270     /* a zero return from a recv() call indicates client is terminated! */
271     if (status == 0)
272     {
273         /* Done with this client , close this secondary server socket */
274         return(status);
275     }
276
277     /* print data received from the client */
278     printf("\nBSD Server Socket:%d received %lu bytes: %s \n", sock, (ULONG)status,rcvBuffer);
279
280     /* And echo the same data to the client */
281     status = send(sock,rcvBuffer, status + 1, 0);
282     if (status == ERROR )
283     {
284         printf("\nError: BSD Server Socket:%d send \n",sock);
285         return(ERROR);
286     }
287     return(status);
288 }
289
290
291 /* Define what the initial system looks like. */
292
293 void     tx_application_define(void *first_unused_memory)
294 {
295
296 CHAR     *pointer;
297 UINT     status;
298
299     /* Setup the working pointer. */
300     pointer = (CHAR *) first_unused_memory;
301
302     /* Create a client thread. */
303     tx_thread_create(&thread_0, "Client1", thread_0_entry, 0,
304         pointer, DEMO_STACK_SIZE, 2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
305
306     pointer = pointer + DEMO_STACK_SIZE;
307
308     /* Create a server thread. */
309     tx_thread_create(&thread_1, "Server", thread_1_entry, 0,
310         pointer, DEMO_STACK_SIZE,1,1, TX_NO_TIME_SLICE, TX_AUTO_START);
311
312     pointer = pointer + DEMO_STACK_SIZE;
313
314     /* Initialize the NetX system. */
315     nx_system_initialize();
316
317     /* Create a BSD packet pool. */
318     status = nx_packet_pool_create(&bsd_pool,"NetX BSD Packet Pool", 128
                                        pointer, 16384);
319     pointer = pointer + 16384;
320     if (status)
321     {
322         error_counter++;
323         printf("Error in creating BSD packet pool\n!");
324     }
325
326     /* Create an IP instance for BSD. */
327     status = nx_ip_create(&bsd_ip, "NetX IP Instance 2", IP_ADDRESS(1, 2, 3, 4),
                              0xFFFFFF00UL, &bsd_pool, _nx_ram_network_driver,
                              pointer, 2048, 1);
328
329     pointer = pointer + 2048;
330
331     if (status)
332     {
333         error_counter++;
334         printf("Error creating BSD IP instance\n!");
335     }
336
337     /* Enable ARP and supply ARP cache memory for BSD IP Instance */
338     status = nx_arp_enable(&bsd_ip, (void *) pointer, 1024);
339     pointer = pointer + 1024;
340
341     /* Check ARP enable status. */
342     if (status)
343     {
344         error_counter++;
345         printf("Error in Enable ARP and supply ARP cache memory to BSD IP instance\n");
346     }
347
348     /* Enable TCP processing for BSD IP instances. */
349
350     status = nx_tcp_enable(&bsd_ip);
351
352     /* Check TCP enable status. */
353     if (status)
354     {
355         error_counter++;
356         printf("Error in Enable TCP \n");
357     }
358
359     /* Now initialize BSD Scoket Wrapper */
360     status = bsd_initialize(&bsd_ip, &bsd_pool,pointer, 2048, 1);
361 }
362
363
364 /* Define the test threads. */
365
366 void     thread_0_entry)ULONG thread_input)
367 {
368
369 CHAR     *msg0 = "Client 1:
                     "ABCDEFGHIJKLMNOPQRSTUVWXYZ<>ABCDEFGHIJKLMNOPQRSTUVWXYZ<> \
                     "ABCDEFGHIJKLMNOPQRSTUVWXYZ<>END";
370
371     /* Wait till Server side is all set */
372     tx_thread_sleep(2);
373     while (1)
374     {
375         tcpClient(msg0);
376         tx_thread_sleep(1);
377     }
378 }
379
380 /* Define the server thread entry function. */
381 void     thread_1_entry(ULONG thread_input)
382 {
383
384 UINT     status;
385 ULONG    actual_status;
386
387 /* Ensure the IP instance has been initialized. */
388 status = nx_ip_status_check(&bsd_ip, NX_IP_INITIALIZE_DONE, &actual_status, 100);
389
390 /* Check status... */
391 if (status != NX_SUCCESS)
392 {
393     error_counter++;
394     return;
395 }
396 /* Start a TCP Server */
397 tcpServer();
398 }
399
```
