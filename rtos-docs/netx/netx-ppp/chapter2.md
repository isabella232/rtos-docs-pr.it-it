---
title: Capitolo 2-installazione e uso di Azure RTO NetX Point-to-Point Protocol (PPP)
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente RTO NetX Point-to-Point Protocol (PPP) di Azure.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 40f09da31f5541208c3b2cc0eeb54850b3d71f7c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822559"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-point-to-point-protocol-ppp"></a><span data-ttu-id="1efa0-103">Capitolo 2-installazione e uso di Azure RTO NetX Point-to-Point Protocol (PPP)</span><span class="sxs-lookup"><span data-stu-id="1efa0-103">Chapter 2 - Installation and use of Azure RTOS NetX Point-to-Point Protocol (PPP)</span></span>

<span data-ttu-id="1efa0-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente RTO NetX Point-to-Point Protocol (PPP) di Azure.</span><span class="sxs-lookup"><span data-stu-id="1efa0-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Point-to-Point Protocol (PPP) component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="1efa0-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="1efa0-105">Product Distribution</span></span>

<span data-ttu-id="1efa0-106">Il pacchetto di Point-to-Point Protocol di Azure RTO NetX (PPP) è disponibile all'indirizzo <https://github.com/azure-rtos/netx> .</span><span class="sxs-lookup"><span data-stu-id="1efa0-106">The Azure RTOS NetX Point-to-Point Protocol (PPP) package is available at <https://github.com/azure-rtos/netx>.</span></span> <span data-ttu-id="1efa0-107">Il pacchetto include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="1efa0-107">The package includes the following files:</span></span>

- <span data-ttu-id="1efa0-108">**nx_ppp. h**: file di intestazione per PPP per NETX</span><span class="sxs-lookup"><span data-stu-id="1efa0-108">**nx_ppp.h**: Header file for PPP for NetX</span></span>
- <span data-ttu-id="1efa0-109">**nx_ppp. c**: file di origine c per PPP per NETX</span><span class="sxs-lookup"><span data-stu-id="1efa0-109">**nx_ppp.c**: C Source file for PPP for NetX</span></span>
- <span data-ttu-id="1efa0-110">**nx_ppp.pdf**: Descrizione PDF di PPP per NETX</span><span class="sxs-lookup"><span data-stu-id="1efa0-110">**nx_ppp.pdf**: PDF description of PPP for NetX</span></span>
- <span data-ttu-id="1efa0-111">dimostrazione di **demo_netx_ppp. c**: NETX PPP</span><span class="sxs-lookup"><span data-stu-id="1efa0-111">**demo_netx_ppp.c**: NetX PPP demonstration</span></span>

## <a name="ppp-installation"></a><span data-ttu-id="1efa0-112">Installazione di PPP</span><span class="sxs-lookup"><span data-stu-id="1efa0-112">PPP Installation</span></span>

<span data-ttu-id="1efa0-113">Per poter usare PPP per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="1efa0-113">In order to use PPP for NetX, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="1efa0-114">Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_ppp. h* e *nx_ppp. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="1efa0-114">For example, if NetX is installed in the directory “*\threadx\arm7\green*” then the *nx_ppp.h* and *nx_ppp.c* files should be copied into this directory.</span></span>

## <a name="using-ppp"></a><span data-ttu-id="1efa0-115">Uso di PPP</span><span class="sxs-lookup"><span data-stu-id="1efa0-115">Using PPP</span></span>

<span data-ttu-id="1efa0-116">L'uso di PPP per NetX è facile.</span><span class="sxs-lookup"><span data-stu-id="1efa0-116">Using PPP for NetX is easy.</span></span> <span data-ttu-id="1efa0-117">In pratica, il codice dell'applicazione deve includere *nx_ppp. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX.</span><span class="sxs-lookup"><span data-stu-id="1efa0-117">Basically, the application code must include *nx_ppp.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="1efa0-118">Una volta incluso *nx_ppp. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione PPP specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="1efa0-118">Once *nx_ppp.h* is included, the application code is then able to make the PPP function calls specified later in this guide.</span></span> <span data-ttu-id="1efa0-119">Nell'applicazione deve inoltre essere incluso *nx_ppp. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-119">The application must also include *nx_ppp.c* in the build process.</span></span> <span data-ttu-id="1efa0-120">Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-120">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="1efa0-121">Questo è tutto ciò che è necessario per usare NetX PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-121">This is all that is required to use NetX PPP.</span></span>

## <a name="using-modems"></a><span data-ttu-id="1efa0-122">Uso di modem</span><span class="sxs-lookup"><span data-stu-id="1efa0-122">Using Modems</span></span>

<span data-ttu-id="1efa0-123">Se è necessario un modem per la connessione a Internet, è necessario tenere presenti alcune considerazioni speciali per poter usare il prodotto NetX PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-123">If a modem is required for connection to the internet, some special considerations are required in order to use the NetX PPP product.</span></span> <span data-ttu-id="1efa0-124">In pratica, l'utilizzo di un modem introduce logica di inizializzazione e logica aggiuntive per la perdita di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-124">Basically, using a modem introduces additional initialization logic and logic for loss of communication.</span></span> <span data-ttu-id="1efa0-125">Inoltre, la maggior parte della logica aggiuntiva del modem viene eseguita al di fuori del contesto di NetX PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-125">In addition, most of the additional modem logic is done outside the context of NetX PPP.</span></span> <span data-ttu-id="1efa0-126">Il flusso di base dell'uso di NetX PPP con un modem è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1efa0-126">The basic flow of using the NetX PPP with a modem goes something like this:</span></span>

1. <span data-ttu-id="1efa0-127">Inizializza modem</span><span class="sxs-lookup"><span data-stu-id="1efa0-127">Initialize Modem</span></span>

1. <span data-ttu-id="1efa0-128">Comporre il provider di servizi Internet (ISP)</span><span class="sxs-lookup"><span data-stu-id="1efa0-128">Dial Internet Service Provider (ISP)</span></span>

1. <span data-ttu-id="1efa0-129">Attendi connessione</span><span class="sxs-lookup"><span data-stu-id="1efa0-129">Wait for Connection</span></span>

1. <span data-ttu-id="1efa0-130">Attendi richiesta UserID</span><span class="sxs-lookup"><span data-stu-id="1efa0-130">Wait for UserID Prompt</span></span>

1. <span data-ttu-id="1efa0-131">Avviare NetX PPP [PPP in Operation]</span><span class="sxs-lookup"><span data-stu-id="1efa0-131">Start NetX PPP [PPP in operation]</span></span>

1. <span data-ttu-id="1efa0-132">Perdita di comunicazione</span><span class="sxs-lookup"><span data-stu-id="1efa0-132">Loss of Communication</span></span>

1. <span data-ttu-id="1efa0-133">Arrestare NetX PPP (o riavviare tramite nx_ppp_restart)</span><span class="sxs-lookup"><span data-stu-id="1efa0-133">Stop NetX PPP (or restart via nx_ppp_restart)</span></span>

### <a name="initialize-modem"></a><span data-ttu-id="1efa0-134">Inizializza modem</span><span class="sxs-lookup"><span data-stu-id="1efa0-134">Initialize Modem</span></span>

<span data-ttu-id="1efa0-135">Utilizzando la routine di output seriale di basso livello dell'applicazione, il modem viene inizializzato tramite una serie di comandi per caratteri ASCII. per ulteriori informazioni, vedere la documentazione del modem.</span><span class="sxs-lookup"><span data-stu-id="1efa0-135">Using the application’s low-level serial output routine, the modem is initialized via a series of ASCII character commands (see modem’s documentation for more details).</span></span>

### <a name="dial-internet-service-provider"></a><span data-ttu-id="1efa0-136">Connessione al provider di servizi Internet</span><span class="sxs-lookup"><span data-stu-id="1efa0-136">Dial Internet Service Provider</span></span>

<span data-ttu-id="1efa0-137">Utilizzando la routine di output seriale di basso livello dell'applicazione, al modem viene richiesto di comporre il provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="1efa0-137">Using the application’s low-level serial output routine, the modem is instructed to dial the ISP.</span></span> <span data-ttu-id="1efa0-138">Il codice seguente, ad esempio, è tipico di una stringa ASCII utilizzata per comporre un ISP al numero 123-4567:</span><span class="sxs-lookup"><span data-stu-id="1efa0-138">For example, the following is typical of an ASCII string used to dial an ISP at the number 123-4567:</span></span>

<span data-ttu-id="1efa0-139">"ATDT123456\r"</span><span class="sxs-lookup"><span data-stu-id="1efa0-139">“ATDT123456\r”</span></span>

### <a name="wait-for-connection"></a><span data-ttu-id="1efa0-140">Attendi connessione</span><span class="sxs-lookup"><span data-stu-id="1efa0-140">Wait for Connection</span></span>

<span data-ttu-id="1efa0-141">A questo punto, l'applicazione attende di ricevere indicazioni dal modem che è stata stabilita una connessione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-141">At this point, the application waits to receive indication from the modem that a connection has been established.</span></span> <span data-ttu-id="1efa0-142">Questa operazione viene eseguita cercando i caratteri della routine di input seriale di basso livello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-142">This is accomplished by looking for characters from the application’s low-level serial input routine.</span></span> <span data-ttu-id="1efa0-143">In genere, i modem restituiscono una stringa ASCII "CONNECT" quando è stata stabilita una connessione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-143">Typically, modems return an ASCII string “CONNECT” when a connection has been established.</span></span>

### <a name="wait-for-user-id-prompt"></a><span data-ttu-id="1efa0-144">Attendi richiesta ID utente</span><span class="sxs-lookup"><span data-stu-id="1efa0-144">Wait for User ID Prompt</span></span>

<span data-ttu-id="1efa0-145">Una volta stabilita la connessione, l'applicazione deve ora attendere una richiesta di accesso iniziale da parte del provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="1efa0-145">Once the connection has been established, the application must now wait for an initial login request from the ISP.</span></span> <span data-ttu-id="1efa0-146">Che in genere assume la forma di una stringa ASCII come "login?"</span><span class="sxs-lookup"><span data-stu-id="1efa0-146">This typically takes the form of an ASCII string like “Login?”</span></span>

### <a name="start-netx-ppp"></a><span data-ttu-id="1efa0-147">Avviare NetX PPP</span><span class="sxs-lookup"><span data-stu-id="1efa0-147">Start NetX PPP</span></span>

<span data-ttu-id="1efa0-148">A questo punto, è possibile avviare NetX PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-148">At this point, the NetX PPP can be started.</span></span> <span data-ttu-id="1efa0-149">Questa operazione viene eseguita chiamando il servizio *nx_ppp_create* seguito dal servizio *nx_ip_create* .</span><span class="sxs-lookup"><span data-stu-id="1efa0-149">This is accomplished by calling the *nx_ppp_create* service followed by the *nx_ip_create* service.</span></span> <span data-ttu-id="1efa0-150">Potrebbero essere richiesti anche servizi aggiuntivi per abilitare PAP e configurare gli indirizzi IP PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-150">Additional services to enable PAP and to setup the PPP IP addresses might also be required.</span></span> <span data-ttu-id="1efa0-151">Per ulteriori informazioni, consultare le sezioni seguenti di questa guida.</span><span class="sxs-lookup"><span data-stu-id="1efa0-151">Please review the following sections of this guide for more information.</span></span>

### <a name="loss-of-communication"></a><span data-ttu-id="1efa0-152">Perdita di comunicazione</span><span class="sxs-lookup"><span data-stu-id="1efa0-152">Loss of Communication</span></span>

<span data-ttu-id="1efa0-153">Dopo l'avvio di PPP, le informazioni non PPP vengono passate alla routine "Gestione pacchetti non valida" specificata dall'applicazione al servizio *nx_ppp_create* .</span><span class="sxs-lookup"><span data-stu-id="1efa0-153">Once PPP is started, any non-PPP information is passed to the “invalid packet handling” routine the application specified to the *nx_ppp_create* service.</span></span> <span data-ttu-id="1efa0-154">In genere, i modem inviano una stringa ASCII, ad esempio "nessun vettore", in caso di perdita della comunicazione con il provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="1efa0-154">Typically, modems send an ASCII string such as “NO CARRIER” when communication is lost with the ISP.</span></span> <span data-ttu-id="1efa0-155">Quando l'applicazione riceve un pacchetto non PPP con tali informazioni, è consigliabile arrestare l'istanza di NetX PPP o riavviare la macchina a stati PPP tramite l'API *nx_ppp_restart* .</span><span class="sxs-lookup"><span data-stu-id="1efa0-155">When the application receives a non-PPP packet with such information, it should proceed to either stop the NetX PPP instance or to restart the PPP state machine via the *nx_ppp_restart* API.</span></span>

### <a name="stop-netx-ppp"></a><span data-ttu-id="1efa0-156">Arrestare NetX PPP</span><span class="sxs-lookup"><span data-stu-id="1efa0-156">Stop NetX PPP</span></span>

<span data-ttu-id="1efa0-157">L'arresto di NetX PPP è piuttosto semplice.</span><span class="sxs-lookup"><span data-stu-id="1efa0-157">Stopping the NetX PPP is fairly straightforward.</span></span> <span data-ttu-id="1efa0-158">In pratica, tutti i socket creati devono essere non associati ed eliminati.</span><span class="sxs-lookup"><span data-stu-id="1efa0-158">Basically, all created sockets must be unbound and deleted.</span></span> <span data-ttu-id="1efa0-159">Eliminare quindi l'istanza IP tramite il servizio *nx_ip_delete* .</span><span class="sxs-lookup"><span data-stu-id="1efa0-159">Next, delete the IP instance via the *nx_ip_delete* service.</span></span> <span data-ttu-id="1efa0-160">Una volta eliminata l'istanza IP, è necessario chiamare il servizio *nx_ppp_delete* per completare il processo di arresto di PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-160">Once the IP instance is deleted, the *nx_ppp_delete* service should be called to finish the process of stopping PPP.</span></span> <span data-ttu-id="1efa0-161">A questo punto, l'applicazione è ora in grado di tentare di ristabilire la comunicazione con il provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="1efa0-161">At this point, the application is now able to attempt to reestablish communication with the ISP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="1efa0-162">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="1efa0-162">Small Example System</span></span>

<span data-ttu-id="1efa0-163">Un esempio che illustra la semplicità di utilizzo di NetX PPP è descritto nella figura 1,1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1efa0-163">An example that illustrates how easy it is to use NetX PPP is described in Figure 1.1 that appears below.</span></span> <span data-ttu-id="1efa0-164">In questo esempio il file di inclusione PPP *nx_ppp. h* viene introdotto nella riga 3.</span><span class="sxs-lookup"><span data-stu-id="1efa0-164">In this example, the PPP include file *nx_ppp.h* is brought in at line 3.</span></span> <span data-ttu-id="1efa0-165">Successivamente, il PPP viene creato in *"tx_application_define*" alla riga 56.</span><span class="sxs-lookup"><span data-stu-id="1efa0-165">Next, PPP is created in *”tx_application_define*” at line 56.</span></span> <span data-ttu-id="1efa0-166">Il blocco di controllo PPP "*my_ppp*" è stato definito come variabile globale alla riga 9 precedente.</span><span class="sxs-lookup"><span data-stu-id="1efa0-166">The PPP control block “*my_ppp*” was defined as a global variable at line 9 previously.</span></span> 

>[!NOTE]
><span data-ttu-id="1efa0-167">Prima di creare l'istanza IP, è necessario creare il PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-167">PPP should be created prior to creating the IP instance.</span></span> <span data-ttu-id="1efa0-168">Al termine della creazione di PPP e IP, il thread "*my_thread*" attende che il collegamento PPP venga attivo alla riga 98.</span><span class="sxs-lookup"><span data-stu-id="1efa0-168">After successful creation of PPP and IP, the thread “*my_thread*” waits for the PPP link to come alive at line 98.</span></span> <span data-ttu-id="1efa0-169">Alla riga 104, PPP e NetX sono completamente operativi.</span><span class="sxs-lookup"><span data-stu-id="1efa0-169">At line 104, both PPP and NetX are fully operational.</span></span>

<span data-ttu-id="1efa0-170">Il primo elemento non illustrato in questo esempio è l'ISR di ricezione di byte seriale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-170">The one item not shown in this example is the application’s serial byte receive ISR.</span></span> <span data-ttu-id="1efa0-171">Sarà necessario chiamare *nx_ppp_byte_receive* con "*my_ppp*" e il byte ricevuto come parametri di input.</span><span class="sxs-lookup"><span data-stu-id="1efa0-171">It will need to call *nx_ppp_byte_receive* with “*my_ppp*” and the byte received as input parameters.</span></span>

```c
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nx_ppp.h"

#define     DEMO_STACK_SIZE         4096
TX_THREAD               my_thread;
NX_PACKET_POOL          my_pool;
NX_IP                   my_ip;
NX_PPP                  my_ppp;

/* Define function prototypes. */

void    my_thread_entry(ULONG thread_input);
void    my_serial_driver_byte_output(UCHAR byte);
void    my_invalid_packet_handler(NX_PACKET *packet_ptr);
 
/* Define main entry point. */
intmain()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
 }


/* Define what the initial system looks like. */

void    tx_application_define(void *first_unused_memory)
{

CHAR    *pointer;
UINT    status;

/* Setup the working pointer. */
pointer =  (CHAR *) first_unused_memory;

/* Create “my_thread”. */
    tx_thread_create(&my_thread, "my thread", my_thread_entry, 0,  
                  pointer, DEMO_STACK_SIZE, 
                  2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status =  nx_packet_pool_create(&my_pool, "NetX Main Packet Pool", 
                                    1024, pointer, 64000);
    pointer = pointer + 64000;

    /* Check for pool creation error. */
    if (status)
        error_counter++;

    /* Create a PPP instance. */
    status = nx_ppp_create(&my_ppp, “My PPP”, &my_ip, pointer, 1024, 2, 
                           &my_pool, my_invalid_packet_handler, my_serial_driver_byte_output);
    pointer =  pointer + 1024;
    /* Check for PPP creation pool. */
    if (status)
        error_counter++;

    /* Create an IP instance with the PPP driver. */
    status = nx_ip_create(&my_ip,"My NetX IP Instance", 
                           IP_ADDRESS(216,2,3,1), 0xFFFFFF00, &my_pool, 
                           nx_ppp_driver, pointer, DEMO_STACK_SIZE, 1);
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check for IP create errors. */
    if (status)
        error_counter++;

    /* Enable ICMP for my IP Instance. */
    status =  nx_icmp_enable(&my_ip);

    /* Check for ICMP enable errors. */
    if (status)
        error_counter++;

    /* Enable UDP. */
    status =  nx_udp_enable(&my_ip);
    if (status)
        error_counter++;
}

/* Define my thread. */
void    my_thread_entry(ULONG thread_input)
{

UINT        status;
ULONG       ip_status;
NX_PACKET   *my_packet;

/* Wait for the PPP link in my_ip to become enabled. */
    status =  nx_ip_status_check(&my_ip,NX_IP_LINK_ENABLED,&ip_status,3000);

    /* Check for IP status error. */
    if (status) 
        return;

    /* Link is fully up and operational. All NetX activities 
    are now available. */

}
```
## <a name="configuration-options"></a><span data-ttu-id="1efa0-172">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="1efa0-172">Configuration Options</span></span>

<span data-ttu-id="1efa0-173">Per la compilazione di PPP per NetX sono disponibili diverse opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-173">There are several configuration options for building PPP for NetX.</span></span> <span data-ttu-id="1efa0-174">L'elenco seguente descrive tutti i dettagli:</span><span class="sxs-lookup"><span data-stu-id="1efa0-174">The following list describes each in detail:</span></span>

- <span data-ttu-id="1efa0-175">**NX_DISABLE_ERROR_CHECKING**: definito, questa opzione rimuove il controllo degli errori PPP di base.</span><span class="sxs-lookup"><span data-stu-id="1efa0-175">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic PPP error checking.</span></span> <span data-ttu-id="1efa0-176">Viene in genere usato dopo il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-176">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="1efa0-177">**NX_PPP_PPPOE_ENABLE**: se definito, PPP è in grado di trasmettere pacchetti tramite Ethernet</span><span class="sxs-lookup"><span data-stu-id="1efa0-177">**NX_PPP_PPPOE_ENABLE**: If defined, PPP can transmit packet over Ethernet</span></span>
- <span data-ttu-id="1efa0-178">**NX_PPP_BASE_TIMEOUT**: definisce la frequenza del periodo (nei cicli del timer) in cui l'attività del thread PPP viene riattivata per verificare la presenza di eventi PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-178">**NX_PPP_BASE_TIMEOUT**: This defines the period rate (in timer ticks) that the PPP thread task is woken to check for PPP events.</span></span> <span data-ttu-id="1efa0-179">Il valore predefinito è 1 \* NX_IP_PERIODIC_RATE (100 cicli).</span><span class="sxs-lookup"><span data-stu-id="1efa0-179">The default value is 1\*NX_IP_PERIODIC_RATE (100 ticks).</span></span>
- <span data-ttu-id="1efa0-180">**NX_PPP_DISABLE_INFO**: se definito, la raccolta di informazioni PPP interna è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="1efa0-180">**NX_PPP_DISABLE_INFO**: If defined, internal PPP information gathering is disabled.</span></span>
- <span data-ttu-id="1efa0-181">**NX_PPP_DEBUG_LOG_ENABLE**: se definito, il log di debug PPP interno è abilitato.</span><span class="sxs-lookup"><span data-stu-id="1efa0-181">**NX_PPP_DEBUG_LOG_ENABLE**: If defined, internal PPP debug log is enabled.</span></span>
- <span data-ttu-id="1efa0-182">**NX_PPP_DEBUG_LOG_PRINT_ENABLE**: se definito, viene abilitato il log di debug di PPP interno *printf* a *stdio* .</span><span class="sxs-lookup"><span data-stu-id="1efa0-182">**NX_PPP_DEBUG_LOG_PRINT_ENABLE**:If defined, internal PPP debug log *printf* to *stdio* is enabled.</span></span> <span data-ttu-id="1efa0-183">Questa operazione è valida solo se è abilitato anche il log di debug.</span><span class="sxs-lookup"><span data-stu-id="1efa0-183">This is only valid if the debug log is also enabled.</span></span>
- <span data-ttu-id="1efa0-184">**NX_PPP_DEBUG_LOG_SIZE**: dimensioni del log di debug (numero di voci nel log di debug).</span><span class="sxs-lookup"><span data-stu-id="1efa0-184">**NX_PPP_DEBUG_LOG_SIZE**: Size of debug log (number of entries in the debug log).</span></span> <span data-ttu-id="1efa0-185">Al raggiungimento dell'ultima voce, l'acquisizione di debug esegue il wrapping sulla prima voce e sovrascrive tutti i dati acquisiti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1efa0-185">On reaching the last entry, the debug capture wraps to the first entry and overwrites any data previously captured.</span></span> <span data-ttu-id="1efa0-186">Il valore predefinito è 50.</span><span class="sxs-lookup"><span data-stu-id="1efa0-186">The default value is 50.</span></span>
- <span data-ttu-id="1efa0-187">**NX_PPP_DEBUG_FRAME_SIZE**: quantità massima di dati acquisiti da un payload del pacchetto ricevuto e salvati nell'output di debug.</span><span class="sxs-lookup"><span data-stu-id="1efa0-187">**NX_PPP_DEBUG_FRAME_SIZE**: Maximum amount of data captured from a received packet payload and saved to debug output.</span></span> <span data-ttu-id="1efa0-188">Il valore predefinito è 50.</span><span class="sxs-lookup"><span data-stu-id="1efa0-188">The default value is 50.</span></span>
- <span data-ttu-id="1efa0-189">**NX_PPP_DISABLE_CHAP**: se definito, viene rimossa la logica CHAP interna di PPP, inclusa la logica digest MD5.</span><span class="sxs-lookup"><span data-stu-id="1efa0-189">**NX_PPP_DISABLE_CHAP**: If defined, internal PPP CHAP logic is removed, including the MD5 digest logic.</span></span>
- <span data-ttu-id="1efa0-190">**NX_PPP_DISABLE_PAP**: se definito, viene rimossa la logica PAP per PPP interna.</span><span class="sxs-lookup"><span data-stu-id="1efa0-190">**NX_PPP_DISABLE_PAP**: If defined, internal PPP PAP logic is removed.</span></span>
- <span data-ttu-id="1efa0-191">**NX_PPP_DNS_OPTION_DISABLE**: se definito, l'opzione DNS è disabilitata nella risposta protocollo IPCP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-191">**NX_PPP_DNS_OPTION_DISABLE**: If defined, DNS Option is disabled in the IPCP response.</span></span>  <span data-ttu-id="1efa0-192">Per impostazione predefinita, questa opzione non è definita (l'opzione DNS è impostata).</span><span class="sxs-lookup"><span data-stu-id="1efa0-192">By default this option is not defined (DNS option is set).</span></span>
- <span data-ttu-id="1efa0-193">**NX_PPP_DNS_ADDRESS_MAX_RETRIES**: specifica il numero di volte in cui l'host PPP richiederà un indirizzo del server DNS dal peer nello stato protocollo IPCP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-193">**NX_PPP_DNS_ADDRESS_MAX_RETRIES**: This specifies how many times the PPP host will request a DNS Server address from the peer in the IPCP state.</span></span> <span data-ttu-id="1efa0-194">Questa operazione non ha alcun effetto se viene definito NX_PPP_DNS_OPTION_DISABLE.</span><span class="sxs-lookup"><span data-stu-id="1efa0-194">This has no effect if NX_PPP_DNS_OPTION_DISABLE is defined.</span></span> <span data-ttu-id="1efa0-195">Il valore predefinito è 2.</span><span class="sxs-lookup"><span data-stu-id="1efa0-195">The default value is 2.</span></span>
- <span data-ttu-id="1efa0-196">**NX_PPP_HASHED_VALUE_SIZE**: specifica le dimensioni delle stringhe "valore hash" usate nell'autenticazione CHAP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-196">**NX_PPP_HASHED_VALUE_SIZE**: Specifies the size of “hashed value” strings used in CHAP authentication.</span></span> <span data-ttu-id="1efa0-197">Il valore predefinito è impostato su 16 byte, ma può essere ridefinito prima dell'inclusione di *nx_ppp. h.*</span><span class="sxs-lookup"><span data-stu-id="1efa0-197">The default value is set to 16 bytes, but can be redefined prior to inclusion of *nx_ppp.h.*</span></span>
- <span data-ttu-id="1efa0-198">**NX_PPP_MAX_LCP_PROTOCOL_RETRIES**: definisce il numero massimo di tentativi se il PPP scade prima di inviare un altro messaggio di richiesta di configurazione LCP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-198">**NX_PPP_MAX_LCP_PROTOCOL_RETRIES**: This defines the max number of retries if the PPP times out before sending another LCP configure request message.</span></span> <span data-ttu-id="1efa0-199">Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento è inattivo.</span><span class="sxs-lookup"><span data-stu-id="1efa0-199">When this number is reached the PPP handshake is aborted and the link status is down.</span></span> <span data-ttu-id="1efa0-200">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="1efa0-200">The default value is 20.</span></span>
- <span data-ttu-id="1efa0-201">**NX_PPP_MAX_PAP_PROTOCOL_RETRIES**: definisce il numero massimo di tentativi se il PPP scade prima di inviare un altro messaggio di richiesta di autenticazione PAP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-201">**NX_PPP_MAX_PAP_PROTOCOL_RETRIES**: This defines the max number of retries if the PPP times out before sending another PAP authentication request message.</span></span> <span data-ttu-id="1efa0-202">Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento è inattivo.</span><span class="sxs-lookup"><span data-stu-id="1efa0-202">When this number is reached the PPP handshake is aborted and the link status is down.</span></span> <span data-ttu-id="1efa0-203">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="1efa0-203">The default value is 20.</span></span>
- <span data-ttu-id="1efa0-204">**NX_PPP_MAX_CHAP_PROTOCOL_RETRIES**: definisce il numero massimo di tentativi se il PPP scade prima di inviare un altro messaggio di verifica CHAP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-204">**NX_PPP_MAX_CHAP_PROTOCOL_RETRIES**: This defines the max number of retries if the PPP times out before sending another CHAP challenge message.</span></span> <span data-ttu-id="1efa0-205">Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento è inattivo.</span><span class="sxs-lookup"><span data-stu-id="1efa0-205">When this number is reached the PPP handshake is aborted and the link status is down.</span></span> <span data-ttu-id="1efa0-206">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="1efa0-206">The default value is 20.</span></span>
- <span data-ttu-id="1efa0-207">**NX_PPP_MAX_IPCP_PROTOCOL_RETRIES**: definisce il numero massimo di tentativi se il PPP scade prima di inviare un altro messaggio di richiesta di configurazione protocollo IPCP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-207">**NX_PPP_MAX_IPCP_PROTOCOL_RETRIES**: This defines the max number of retries if the PPP times out before sending another IPCP configure request message.</span></span> <span data-ttu-id="1efa0-208">Quando viene raggiunto questo numero, l'handshake PPP viene interrotto e lo stato del collegamento è inattivo.</span><span class="sxs-lookup"><span data-stu-id="1efa0-208">When this number is reached the PPP handshake is aborted and the link status is down.</span></span> <span data-ttu-id="1efa0-209">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="1efa0-209">The default value is 20.</span></span>
- <span data-ttu-id="1efa0-210">**NX_PPP_MRU**: specifica l'unità di ricezione massima (MRU) per PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-210">**NX_PPP_MRU**: Specifies the Maximum Receive Unit (MRU) for PPP.</span></span> <span data-ttu-id="1efa0-211">Per impostazione predefinita, questo valore è 1.500 byte (valore minimo).</span><span class="sxs-lookup"><span data-stu-id="1efa0-211">By default, this value is 1,500 bytes (the minimum value).</span></span> <span data-ttu-id="1efa0-212">Questa definizione può essere impostata dall'applicazione prima di includere *nx_ppp. h*.</span><span class="sxs-lookup"><span data-stu-id="1efa0-212">This define can be set by the application prior to inclusion of *nx_ppp.h*.</span></span>
- <span data-ttu-id="1efa0-213">**NX_PPP_MINIMUM_MRU**: specifica la quantità minima di MRU ricevuta in un messaggio di richiesta di configurazione LCP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-213">**NX_PPP_MINIMUM_MRU**: Specifies the minimum MRU received in an LCP configure request message.</span></span> <span data-ttu-id="1efa0-214">Per impostazione predefinita, questo valore è 1.500 byte (valore minimo).</span><span class="sxs-lookup"><span data-stu-id="1efa0-214">By default, this value is 1,500 bytes (the minimum value).</span></span> <span data-ttu-id="1efa0-215">Questa definizione può essere impostata dall'applicazione prima di includere *nx_ppp. h*.</span><span class="sxs-lookup"><span data-stu-id="1efa0-215">This define can be set by the application prior to inclusion of *nx_ppp.h*.</span></span>
- <span data-ttu-id="1efa0-216">**NX_PPP_NAME_SIZE**: specifica le dimensioni delle stringhe "Name" usate per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-216">**NX_PPP_NAME_SIZE**: Specifies the size of “name” strings used in authentication.</span></span> <span data-ttu-id="1efa0-217">Il valore predefinito è impostato su 32bytes, ma può essere ridefinito prima dell'inclusione di \* nx_ppp. h.</span><span class="sxs-lookup"><span data-stu-id="1efa0-217">The default value is set to 32bytes, but can be redefined prior to inclusion of \*nx_ppp.h.</span></span>
- <span data-ttu-id="1efa0-218">**NX_PPP_PASSWORD_SIZE**: specifica le dimensioni delle stringhe "password" usate per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-218">**NX_PPP_PASSWORD_SIZE**: Specifies the size of “password” strings used in authentication.</span></span> <span data-ttu-id="1efa0-219">Il valore predefinito è impostato su 32bytes, ma può essere ridefinito prima dell'inclusione di *nx_ppp. h.*</span><span class="sxs-lookup"><span data-stu-id="1efa0-219">The default value is set to 32bytes, but can be redefined prior to inclusion of *nx_ppp.h.*</span></span>
- <span data-ttu-id="1efa0-220">**NX_PPP_PROTOCOL_TIMEOUT**: definisce l'opzione Wait (in secondi) per l'attività PPP per la ricezione di una risposta a un messaggio di richiesta di protocollo PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-220">**NX_PPP_PROTOCOL_TIMEOUT**: This defines the wait option (in seconds) for the PPP task to receive a response to a PPP protocol request message.</span></span> <span data-ttu-id="1efa0-221">Il valore predefinito è 4 secondi.</span><span class="sxs-lookup"><span data-stu-id="1efa0-221">The default value is 4 seconds.</span></span>
- <span data-ttu-id="1efa0-222">**NX_PPP_RECEIVE_TIMEOUTS**: definisce il numero di volte in cui l'attività del thread PPP scade in attesa di ricevere il carattere successivo in un flusso di messaggi PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-222">**NX_PPP_RECEIVE_TIMEOUTS**: This defines the number of times the PPP thread task times out waiting to receive the next character in a PPP message stream.</span></span> <span data-ttu-id="1efa0-223">Successivamente, PPP rilascia il pacchetto e inizia ad attendere la ricezione del messaggio PPP successivo.</span><span class="sxs-lookup"><span data-stu-id="1efa0-223">Thereafter, PPP releases the packet and begins waiting to receive the next PPP message.</span></span> <span data-ttu-id="1efa0-224">Il valore predefinito è 4.</span><span class="sxs-lookup"><span data-stu-id="1efa0-224">The default value is 4.</span></span>
- <span data-ttu-id="1efa0-225">**NX_PPP_SERIAL_BUFFER_SIZE**: specifica le dimensioni del buffer seriale dei caratteri di ricezione.</span><span class="sxs-lookup"><span data-stu-id="1efa0-225">**NX_PPP_SERIAL_BUFFER_SIZE**: Specifies the size of the receive character serial buffer.</span></span> <span data-ttu-id="1efa0-226">Per impostazione predefinita, questo valore è pari a 3.000 byte.</span><span class="sxs-lookup"><span data-stu-id="1efa0-226">By default, this value is 3,000 bytes.</span></span> <span data-ttu-id="1efa0-227">Questa definizione può essere impostata dall'applicazione prima di includere *nx_ppp. h*.</span><span class="sxs-lookup"><span data-stu-id="1efa0-227">This define can be set by the application prior to inclusion of *nx_ppp.h*.</span></span>
- <span data-ttu-id="1efa0-228">**NX_PPP_TIMEOUT**: definisce l'opzione Wait (nei cicli del timer) per l'allocazione dei pacchetti per la trasmissione di dati e per il buffer dei dati seriali PPP in pacchetti da inviare al livello IP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-228">**NX_PPP_TIMEOUT**: This defines the wait option (in timer ticks) for allocating packets to transmit data as well as buffer PPP serial data into packets to send to the IP layer.</span></span> <span data-ttu-id="1efa0-229">Il valore predefinito è 4 \* NX_IP_PERIODIC_RATE (400 cicli).</span><span class="sxs-lookup"><span data-stu-id="1efa0-229">The default value is 4\*NX_IP_PERIODIC_RATE (400 ticks).</span></span>
- <span data-ttu-id="1efa0-230">**NX_PPP_THREAD_TIME_SLICE**: opzione di sezionamento del tempo per i thread PPP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-230">**NX_PPP_THREAD_TIME_SLICE**: Time-slice option for PPP threads.</span></span> <span data-ttu-id="1efa0-231">Per impostazione predefinita, questo valore è TX_NO_TIME_SLICE.</span><span class="sxs-lookup"><span data-stu-id="1efa0-231">By default, this value is TX_NO_TIME_SLICE.</span></span> <span data-ttu-id="1efa0-232">Questa definizione può essere impostata dall'applicazione prima di includere *nx_ppp. h*.</span><span class="sxs-lookup"><span data-stu-id="1efa0-232">This define can be set by the application prior to inclusion of *nx_ppp.h*.</span></span>
- <span data-ttu-id="1efa0-233">**NX_PPP_VALUE_SIZE**: specifica le dimensioni delle stringhe "value" usate nell'autenticazione CHAP.</span><span class="sxs-lookup"><span data-stu-id="1efa0-233">**NX_PPP_VALUE_SIZE**: Specifies the size of “value” strings used in CHAP authentication.</span></span> <span data-ttu-id="1efa0-234">Il valore predefinito è impostato su 32bytes, ma può essere ridefinito prima dell'inclusione di nx_ppp. h.</span><span class="sxs-lookup"><span data-stu-id="1efa0-234">The default value is set to 32bytes, but can be redefined prior to inclusion of nx_ppp.h.</span></span>
