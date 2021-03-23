---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo SNMP
description: L'implementazione SNMP di NetX Duo è quella di un agente SNMP. Un agente è responsabile della risposta ai comandi del gestore SNMP e dell'invio di trap basati su eventi.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5760e35fdbe8d7b27e2ccc82abac37b1f6fb5118
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821686"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-snmp"></a><span data-ttu-id="a0279-104">Capitolo 1-Introduzione ad Azure RTO NetX Duo SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-104">Chapter 1 - Introduction to Azure RTOS NetX Duo SNMP</span></span>

<span data-ttu-id="a0279-105">Il Simple Network Management Protocol (SNMP) è un protocollo progettato per gestire i dispositivi su Internet.</span><span class="sxs-lookup"><span data-stu-id="a0279-105">The Simple Network Management Protocol (SNMP) is a protocol designed for managing devices on the internet.</span></span> <span data-ttu-id="a0279-106">SNMP è un protocollo che utilizza i servizi UDP (User Datagram Protocol) senza connessione per eseguire la relativa funzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="a0279-106">SNMP is a protocol that utilizes the connectionless User Datagram Protocol (UDP) services to perform its management function.</span></span> <span data-ttu-id="a0279-107">L'implementazione SNMP di Azure RTO NetX Duo è quella di un agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-107">The Azure RTOS NetX Duo SNMP implementation is that of an SNMP Agent.</span></span> <span data-ttu-id="a0279-108">Un agente è responsabile della risposta ai comandi del gestore SNMP e dell'invio di trap basati su eventi.</span><span class="sxs-lookup"><span data-stu-id="a0279-108">An agent is responsible for responding to SNMP Manager’s commands and sending event driven traps.</span></span> 

<span data-ttu-id="a0279-109">NetX Duo SNMP supporta la comunicazione sia IPv4 che IPv6 con i gestori SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-109">NetX Duo SNMP supports both IPv4 and IPv6 communication with SNMP Managers.</span></span> <span data-ttu-id="a0279-110">Le applicazioni SNMP NetX devono essere compilate ed eseguite in NetX Duo SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-110">NetX SNMP applications should compile and run in NetX Duo SNMP.</span></span> <span data-ttu-id="a0279-111">Tuttavia, lo sviluppatore è incoraggiato a trasferire le applicazioni SNMP esistenti usando i servizi "Duo" equivalenti.</span><span class="sxs-lookup"><span data-stu-id="a0279-111">However, the developer is encouraged to port existing SNMP applications to using the equivalent “duo” services.</span></span> <span data-ttu-id="a0279-112">Quando si inviano messaggi trap SNMP, ad esempio, i seguenti servizi "Duo" devono sostituire il relativo equivalente NetX:</span><span class="sxs-lookup"><span data-stu-id="a0279-112">For example, when sending SNMP trap messages, the following ‘duo’ services should replace their NetX equivalent:</span></span>

<span data-ttu-id="a0279-113">*nxd_snmp_object_trap_send*</span><span class="sxs-lookup"><span data-stu-id="a0279-113">*nxd_snmp_object_trap_send*</span></span>

<span data-ttu-id="a0279-114">*nxd_snmp_object_trapv2_send*</span><span class="sxs-lookup"><span data-stu-id="a0279-114">*nxd_snmp_object_trapv2_send*</span></span>

<span data-ttu-id="a0279-115">*nxd_snmp_object_trapv3_send*</span><span class="sxs-lookup"><span data-stu-id="a0279-115">*nxd_snmp_object_trapv3_send*</span></span>

<span data-ttu-id="a0279-116">Per ulteriori informazioni, vedere la **Descrizione dei servizi SNMP Agent** in altre parti di questo manuale dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a0279-116">For more details, see **Description of SNMP Agent Services** elsewhere in this User Guide for more details.</span></span>

## <a name="netx-duo-snmp-agent-requirements"></a><span data-ttu-id="a0279-117">Requisiti dell'agente SNMP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-117">NetX Duo SNMP Agent Requirements</span></span>

<span data-ttu-id="a0279-118">Per il pacchetto SNMP NetX Duo è necessario che sia già stata creata un'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="a0279-118">The NetX Duo SNMP package requires that an IP instance has already been created.</span></span> <span data-ttu-id="a0279-119">Inoltre, è necessario abilitare UDP nella stessa istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="a0279-119">In addition, UDP must be enabled on that same IP instance.</span></span>

<span data-ttu-id="a0279-120">L'agente SNMP NetX Duo presenta diversi requisiti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="a0279-120">The NetX Duo SNMP Agent has several additional requirements.</span></span> <span data-ttu-id="a0279-121">Per prima cosa, è necessario l'accesso alla porta 161 per la gestione di tutte le richieste di gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-121">First, it requires access to port 161 for handling all SNMP manager requests.</span></span> <span data-ttu-id="a0279-122">Richiede inoltre l'accesso alla porta 162 per l'invio di messaggi trap al responsabile.</span><span class="sxs-lookup"><span data-stu-id="a0279-122">It also requires access to port 162 for sending trap messages to the Manager.</span></span>

<span data-ttu-id="a0279-123">Per usare l'agente SNMP NetX Duo con su IPv6 e per ottenere gli oggetti IPv6, è necessario abilitare IPv6 in NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="a0279-123">To use NetX Duo SNMP Agent with over IPv6 and to obtain IPv6 objects, IPv6 must be enabled in NetX Duo.</span></span> <span data-ttu-id="a0279-124">Per informazioni dettagliate sull'abilitazione dell'istanza IP per i servizi IPv6, vedere la ***Guida dell'utente di NETX Duo*** .</span><span class="sxs-lookup"><span data-stu-id="a0279-124">See the ***NetX Duo User Guide*** for details on enabling the IP instance for IPv6 services.</span></span>

## <a name="netx-duo-snmp-constraints"></a><span data-ttu-id="a0279-125">Vincoli SNMP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-125">NetX Duo SNMP Constraints</span></span>

<span data-ttu-id="a0279-126">Il protocollo SNMP NetX Duo implementa SNMP versione 1, 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="a0279-126">The NetX Duo SNMP protocol implements SNMP Version 1, 2, and 3.</span></span> <span data-ttu-id="a0279-127">L'implementazione di SNMPv3 supporta l'autenticazione MD5 e SHA e la crittografia DES.</span><span class="sxs-lookup"><span data-stu-id="a0279-127">The SNMPv3 implementation supports MD5 and SHA authentication, and DES encryption.</span></span> <span data-ttu-id="a0279-128">Questa versione dell'agente SNMP NetX Duo presenta i vincoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0279-128">This version of the NetX Duo SNMP Agent has the following constraints:</span></span>

1. <span data-ttu-id="a0279-129">Un agente SNMP per ogni istanza IP di NetX</span><span class="sxs-lookup"><span data-stu-id="a0279-129">One SNMP Agent per NetX IP Instance</span></span>
2. <span data-ttu-id="a0279-130">Nessun supporto per RMON</span><span class="sxs-lookup"><span data-stu-id="a0279-130">No support for RMON</span></span>
3. <span data-ttu-id="a0279-131">Il protocollo SNMP v3 informa che i messaggi non sono supportati</span><span class="sxs-lookup"><span data-stu-id="a0279-131">SNMP v3 Inform messages are not supported</span></span>
4. <span data-ttu-id="a0279-132">I tipi di dati OPAQUE e NSAP non sono supportati</span><span class="sxs-lookup"><span data-stu-id="a0279-132">OPAQUE and NSAP data types are not supported</span></span>
5. <span data-ttu-id="a0279-133">Gli indirizzi IPv6 sono definiti come stringhe ottetto e il controllo del formato viene lasciato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0279-133">IPv6 addresses are defined as octet strings, and format checking is left to the application.</span></span>

## <a name="snmp-object-names"></a><span data-ttu-id="a0279-134">Nomi degli oggetti SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-134">SNMP Object Names</span></span>

<span data-ttu-id="a0279-135">Il protocollo SNMP è progettato per gestire i dispositivi su Internet.</span><span class="sxs-lookup"><span data-stu-id="a0279-135">The SNMP protocol is designed to manage devices on the internet.</span></span> <span data-ttu-id="a0279-136">A tale scopo, ogni dispositivo gestito SNMP dispone di un set di oggetti definiti dalla struttura delle informazioni di gestione (SMI) in base a quanto definito da RFC 1155.</span><span class="sxs-lookup"><span data-stu-id="a0279-136">To accomplish this, each SNMP managed device has a set of objects that are defined by the Structure of Management Information (SMI) as defined by RFC 1155.</span></span> <span data-ttu-id="a0279-137">La struttura è un tipo di struttura ad albero gerarchico simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a0279-137">The structure is a hierarchical tree type of structure that looks like the following:</span></span>

![Diagramma della struttura delle informazioni di gestione.](media/image3.png)

<span data-ttu-id="a0279-139">Ogni nodo dell'albero è un oggetto.</span><span class="sxs-lookup"><span data-stu-id="a0279-139">Each node in the tree is an object.</span></span> <span data-ttu-id="a0279-140">L'oggetto "DOD" nell'albero è identificato dalla notazione 1.3.6, mentre l'oggetto "Internet" nella struttura ad albero è identificato dalla notazione 1.3.6.1.</span><span class="sxs-lookup"><span data-stu-id="a0279-140">The “dod” object in the tree is identified by the notation 1.3.6, while the “internet” object in the tree is identified by the notation 1.3.6.1.</span></span> <span data-ttu-id="a0279-141">Tutti i nomi degli oggetti SNMP iniziano con la notazione 1.3.6.</span><span class="sxs-lookup"><span data-stu-id="a0279-141">All SNMP object names begin with the notation 1.3.6.</span></span>

<span data-ttu-id="a0279-142">Un gestore SNMP utilizza questa notazione dell'oggetto per specificare l'oggetto nel dispositivo che si desidera ottenere o impostare.</span><span class="sxs-lookup"><span data-stu-id="a0279-142">An SNMP Manager uses this object notation to specify what object in the device it wishes to get or set.</span></span> <span data-ttu-id="a0279-143">L'agente SNMP NetX Duo interpreta tali richieste di gestione e fornisce meccanismi che consentono all'applicazione di eseguire l'operazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="a0279-143">The NetX Duo SNMP Agent interprets such manager requests and provides mechanisms for the application to perform the requested operation.</span></span>

## <a name="snmp-manager-requests"></a><span data-ttu-id="a0279-144">Richieste di gestione SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-144">SNMP Manager Requests</span></span>

<span data-ttu-id="a0279-145">SNMP dispone di un meccanismo semplice per la gestione dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a0279-145">The SNMP has a simple mechanism for managing devices.</span></span> <span data-ttu-id="a0279-146">È disponibile un set di comandi SNMP standard rilasciati da gestione SNMP al dispositivo SNMP sulla *porta 161*.</span><span class="sxs-lookup"><span data-stu-id="a0279-146">There is a set of standard SNMP commands that are issued by the SNMP Manager to the SNMP device on *port 161*.</span></span> <span data-ttu-id="a0279-147">Di seguito sono riportati alcuni dei comandi di base di SNMP Manager:</span><span class="sxs-lookup"><span data-stu-id="a0279-147">The following shows some of the basic SNMP Manager commands:</span></span>

| <span data-ttu-id="a0279-148">Comando SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-148">SNMP Command</span></span> | <span data-ttu-id="a0279-149">Significato</span><span class="sxs-lookup"><span data-stu-id="a0279-149">Meaning</span></span>                                                        |
|--------------|----------------------------------------------------------------|
| <span data-ttu-id="a0279-150">GET</span><span class="sxs-lookup"><span data-stu-id="a0279-150">GET</span></span>          | <span data-ttu-id="a0279-151">*Ottenere l'oggetto specificato*</span><span class="sxs-lookup"><span data-stu-id="a0279-151">*Get the specified object*</span></span>                                       |
| <span data-ttu-id="a0279-152">GETNEXT</span><span class="sxs-lookup"><span data-stu-id="a0279-152">GETNEXT</span></span>      | <span data-ttu-id="a0279-153">*Ottiene l'oggetto logico successivo dopo l'ID oggetto specificato*</span><span class="sxs-lookup"><span data-stu-id="a0279-153">*Get the next logical object after the specified object ID*</span></span>      |
| <span data-ttu-id="a0279-154">GETBULK</span><span class="sxs-lookup"><span data-stu-id="a0279-154">GETBULK</span></span>      | <span data-ttu-id="a0279-155">*Ottenere più oggetti logici dopo l'ID oggetto specificato*</span><span class="sxs-lookup"><span data-stu-id="a0279-155">*Get the multiple logical objects after the specified object ID*</span></span> |
| <span data-ttu-id="a0279-156">SET</span><span class="sxs-lookup"><span data-stu-id="a0279-156">SET</span></span>          | <span data-ttu-id="a0279-157">*Imposta l'oggetto specificato*</span><span class="sxs-lookup"><span data-stu-id="a0279-157">*Set the specified object*</span></span>                                       |

<span data-ttu-id="a0279-158">Questi comandi sono codificati in formato ASN. 1 (Abstract Syntax Notation One) e si trovano nel payload del pacchetto UDP inviato da gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-158">These commands are encoded in the Abstract Syntax Notation One (ASN.1) format and reside in the payload of the UDP packet sent by the SNMP Manager.</span></span> <span data-ttu-id="a0279-159">L'agente SNMP NetX Duo elabora la richiesta e quindi chiama la corrispondente routine di gestione specificata nella chiamata ***nx_snmp_agent_create*** .</span><span class="sxs-lookup"><span data-stu-id="a0279-159">The NetX Duo SNMP Agent processes the request and then calls the corresponding handling routine specified in the ***nx_snmp_agent_create*** call.</span></span>

## <a name="netx-duo-snmp-agent-traps"></a><span data-ttu-id="a0279-160">Trap agente SNMP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-160">NetX Duo SNMP Agent Traps</span></span>

<span data-ttu-id="a0279-161">L'agente SNMP NetX Duo consente inoltre di avvisare un gestore SNMP di eventi in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="a0279-161">The NetX Duo SNMP Agent provides the ability to also alert an SNMP Manager of events asynchronously.</span></span> <span data-ttu-id="a0279-162">Questa operazione viene eseguita tramite un comando trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-162">This is done via an SNMP trap command.</span></span> <span data-ttu-id="a0279-163">È disponibile un'API univoca per ogni versione di SNMP per l'invio di trap a un gestore SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-163">There is a unique API for each version of SNMP for sending traps to an SNMP Manager.</span></span> <span data-ttu-id="a0279-164">Per impostazione predefinita, i trap vengono inviati al gestore SNMP sulla porta 162.</span><span class="sxs-lookup"><span data-stu-id="a0279-164">By default, the traps are sent to the SNMP Manager on port 162.</span></span>

<span data-ttu-id="a0279-165">L'agente SNMP NetX Duo fornisce chiavi di sicurezza separate per i messaggi trap SNMPv3.</span><span class="sxs-lookup"><span data-stu-id="a0279-165">The NetX Duo SNMP Agent provides separate security keys for SNMPv3 trap messages.</span></span> <span data-ttu-id="a0279-166">A tale scopo, l'applicazione SNMP deve creare un set separato di chiavi da quelle applicate alle risposte alle richieste di gestione.</span><span class="sxs-lookup"><span data-stu-id="a0279-166">To do so, the SNMP application must create a separate set of keys from those applied to responses to Manager requests.</span></span> <span data-ttu-id="a0279-167">Trap Security consente all'agente SNMP di usare le stesse password o password diverse per l'autenticazione e la privacy.</span><span class="sxs-lookup"><span data-stu-id="a0279-167">Trap security enables the SNMP Agent to use the same or different passwords for authentication and privacy.</span></span> <span data-ttu-id="a0279-168">Per ulteriori informazioni sulla creazione di chiavi di sicurezza, vedere **autenticazione e crittografia SNMP di NETX Duo** nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="a0279-168">For more information on creating security keys, see **NetX Duo SNMP Authentication and Encryption** in the next section.</span></span>

<span data-ttu-id="a0279-169">Un elenco di variabili trap SNMP standard è enumerato nella parte superiore di *nxd_snmp. h:*</span><span class="sxs-lookup"><span data-stu-id="a0279-169">A list of standard SNMP trap variables is enumerated at the top of *nxd_snmp.h:*</span></span>

| <span data-ttu-id="a0279-170">Variabili</span><span class="sxs-lookup"><span data-stu-id="a0279-170">Variables</span></span>                                 | <span data-ttu-id="a0279-171">Valore</span><span class="sxs-lookup"><span data-stu-id="a0279-171">Value</span></span>  |
|-------------------------------------------|---|
| <span data-ttu-id="a0279-172">#define NX_SNMP_TRAP_COLDSTART</span><span class="sxs-lookup"><span data-stu-id="a0279-172">#define NX_SNMP_TRAP_COLDSTART</span></span>            | <span data-ttu-id="a0279-173">0</span><span class="sxs-lookup"><span data-stu-id="a0279-173">0</span></span> |
| <span data-ttu-id="a0279-174">#define NX_SNMP_TRAP_WARMSTART</span><span class="sxs-lookup"><span data-stu-id="a0279-174">#define NX_SNMP_TRAP_WARMSTART</span></span>            | <span data-ttu-id="a0279-175">1</span><span class="sxs-lookup"><span data-stu-id="a0279-175">1</span></span> |
| <span data-ttu-id="a0279-176">#define NX_SNMP_TRAP_LINKDOWN</span><span class="sxs-lookup"><span data-stu-id="a0279-176">#define NX_SNMP_TRAP_LINKDOWN</span></span>             | <span data-ttu-id="a0279-177">2</span><span class="sxs-lookup"><span data-stu-id="a0279-177">2</span></span> |
| <span data-ttu-id="a0279-178">#define NX_SNMP_TRAP_LINKUP</span><span class="sxs-lookup"><span data-stu-id="a0279-178">#define NX_SNMP_TRAP_LINKUP</span></span>               | <span data-ttu-id="a0279-179">3</span><span class="sxs-lookup"><span data-stu-id="a0279-179">3</span></span> |
| <span data-ttu-id="a0279-180">#define NX_SNMP_TRAP_AUTHENTICATE_FAILURE</span><span class="sxs-lookup"><span data-stu-id="a0279-180">#define NX_SNMP_TRAP_AUTHENTICATE_FAILURE</span></span> | <span data-ttu-id="a0279-181">4</span><span class="sxs-lookup"><span data-stu-id="a0279-181">4</span></span> |
| <span data-ttu-id="a0279-182">#define NX_SNMP_TRAP_EGPNEIGHBORLOSS</span><span class="sxs-lookup"><span data-stu-id="a0279-182">#define NX_SNMP_TRAP_EGPNEIGHBORLOSS</span></span>      | <span data-ttu-id="a0279-183">5</span><span class="sxs-lookup"><span data-stu-id="a0279-183">5</span></span> |
| <span data-ttu-id="a0279-184">#define NX_SNMP_TRAP_ENTERPRISESPECIFIC</span><span class="sxs-lookup"><span data-stu-id="a0279-184">#define NX_SNMP_TRAP_ENTERPRISESPECIFIC</span></span>   | <span data-ttu-id="a0279-185">6</span><span class="sxs-lookup"><span data-stu-id="a0279-185">6</span></span> |

<span data-ttu-id="a0279-186">Per includere queste variabili nel messaggio trap, l'argomento di input trap_type in *nx_snmp_agent_trapv2_send* (SNMPv2) o *nx_snmp_agent_trapv3_send* (SNMPv3) viene impostato sul valore enumerato di queste variabili.</span><span class="sxs-lookup"><span data-stu-id="a0279-186">To include these variables in the trap message, the trap_type input argument in *nx_snmp_agent_trapv2_send* (SNMPv2) or *nx_snmp_agent_trapv3_send* (SNMPv3) is set to the enumerated value of these variables.</span></span> <span data-ttu-id="a0279-187">Di seguito è riportato un esempio per SNMPv2 per notificare al gestore SNMP un evento di avvio a freddo:</span><span class="sxs-lookup"><span data-stu-id="a0279-187">An example is shown below for SNMPv2 to notify the SNMP Manager of a cold start event:</span></span>

```c
UINT trap_type = NX_SNMP_TRAP_COLDSTART;

status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                  (UCHAR *)"public", trap_type,
                                  tx_time_get(), NX_NULL);

```

<span data-ttu-id="a0279-188">Per includere variabili proprietarie nel messaggio trap, l'argomento di input trap_type è impostato su NX_SNMP_TRAP_CUSTOM e l'argomento di input trap List contiene i dati proprietari.</span><span class="sxs-lookup"><span data-stu-id="a0279-188">To include proprietary variables in the trap message, the trap_type input argument is set to NX_SNMP_TRAP_CUSTOM and the trap list input argument contains the proprietary data.</span></span> <span data-ttu-id="a0279-189">Si noti che il messaggio trap conterrà come ora di sistema (1.3.6.1.6.3.1.1.4.1.0).</span><span class="sxs-lookup"><span data-stu-id="a0279-189">Note that the trap message will contain as the system up time (1.3.6.1.6.3.1.1.4.1.0).</span></span> <span data-ttu-id="a0279-190">Di seguito viene illustrato un esempio per SNMPv2:</span><span class="sxs-lookup"><span data-stu-id="a0279-190">An example is shown below for SNMPv2:</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[3];
NX_SNMP_OBJECT_DATA trap_data0;

    /* Load the data into the OBJECT. */
    nx_snmp_object_id_get((void*)"1.3.6.1.4.1.7428.1.3.2.0", &trap_data0);

    /* Update the Trap Object with the object and OID. */
    trap_list[0].nx_snmp_object_string_ptr = (UCHAR *)"1.3.6.1.6.3.1.1.4.0";
    trap_list[0].nx_snmp_object_data  = &trap_data0;

    /* Null terminate the trap list. */
    trap_list[1].nx_snmp_object_string_ptr = NX_NULL;

    status = nx_snmp_agent_trapv2_send(&my_agent, MIB_IP_ADDRESS,
                                      (UCHAR *)"trapduo",
                                      NX_SNMP_TRAP_CUSTOM,
                                      tx_time_get(), trap_list);
```

## <a name="netx-duo-snmp-authentication-and-encryption"></a><span data-ttu-id="a0279-191">Autenticazione e crittografia SNMP di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-191">NetX Duo SNMP Authentication and Encryption</span></span>

<span data-ttu-id="a0279-192">Esistono due tipi di autenticazione, ovvero *Basic* e *digest*.</span><span class="sxs-lookup"><span data-stu-id="a0279-192">There are two flavors of authentication, namely *basic* and *digest*.</span></span> <span data-ttu-id="a0279-193">L'autenticazione di base equivale a una semplice autenticazione del *nome utente* in testo normale trovata in molti protocolli.</span><span class="sxs-lookup"><span data-stu-id="a0279-193">Basic authentication is equivalent to a simple plain text *username* authentication found in many protocols.</span></span> <span data-ttu-id="a0279-194">Nell'autenticazione SNMP di base l'utente verifica semplicemente che il nome utente fornito sia valido per l'esecuzione di operazioni SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-194">In SNMP basic authentication, the user simply verifies that the supplied username is valid for performing SNMP operations.</span></span> <span data-ttu-id="a0279-195">L'autenticazione di base è l'unica opzione per SNMP versioni 1 e 2.</span><span class="sxs-lookup"><span data-stu-id="a0279-195">Basic authentication is the only option for SNMP versions 1 and 2.</span></span>

<span data-ttu-id="a0279-196">Lo svantaggio principale dell'autenticazione di base è che il nome utente viene trasmesso in testo normale.</span><span class="sxs-lookup"><span data-stu-id="a0279-196">The main disadvantage of basic authentication is the username is transmitted in plain text.</span></span> <span data-ttu-id="a0279-197">L'autenticazione del digest SNMPv3 risolve questo problema senza trasmettere mai il nome utente in testo normale.</span><span class="sxs-lookup"><span data-stu-id="a0279-197">The SNMPv3 digest authentication addresses this problem by never transmitting the username in plain text.</span></span> <span data-ttu-id="a0279-198">Viene invece usato un algoritmo per derivare un'digest ' a 96 bit dal nome utente, dal motore di contesto e da altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="a0279-198">Instead, an algorithm is used to derive a 96-bit ‘digest’ from the username, context engine, and other information.</span></span> <span data-ttu-id="a0279-199">L'agente SNMP NetX Duo supporta sia gli algoritmi MD5 che quelli del digest SHA.</span><span class="sxs-lookup"><span data-stu-id="a0279-199">The NetX Duo SNMP Agent supports both MD5 and SHA digest algorithms.</span></span>

<span data-ttu-id="a0279-200">Per abilitare l'autenticazione, l'agente SNMP deve impostare l'ID del motore di contesto utilizzando il servizio *nx_snmp_agent_context_engine_set* .</span><span class="sxs-lookup"><span data-stu-id="a0279-200">To enable authentication, the SNMP Agent must set its Context Engine ID using the *nx_snmp_agent_context_engine_set* service.</span></span> <span data-ttu-id="a0279-201">L'ID del motore di contesto viene usato nella creazione della chiave di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a0279-201">The Context Engine ID is used in the creation of the authentication key.</span></span>

<span data-ttu-id="a0279-202">La crittografia dei dati di SNMPv3 è disponibile tramite l'algoritmo DES.</span><span class="sxs-lookup"><span data-stu-id="a0279-202">Encryption of SNMPv3 data is available using the DES algorithm.</span></span> <span data-ttu-id="a0279-203">Per la crittografia è necessaria l'abilitazione dell'autenticazione (non è possibile crittografare i dati senza impostare i parametri di autenticazione).</span><span class="sxs-lookup"><span data-stu-id="a0279-203">Encryption requires that authentication be enabled (one cannot encrypt data without setting the authentication parameters).</span></span>

<span data-ttu-id="a0279-204">Per creare le chiavi di autenticazione e privacy, vengono usate le API seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0279-204">To create authentication and privacy keys, the following API are used:</span></span>

```c
UINT  _nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)

UINT  _nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *password, NX_SNMP_SECURITY_KEY
                                   *destination_key)
```

<span data-ttu-id="a0279-205">Successivamente, è necessario configurare l'agente SNMP per l'utilizzo di queste chiavi.</span><span class="sxs-lookup"><span data-stu-id="a0279-205">Next, the SNMP agent must be configured to use these keys.</span></span> <span data-ttu-id="a0279-206">Per registrare una chiave con l'agente SNMP, vengono usate le API seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0279-206">To register a key with the SNMP agent, the following API are used:</span></span>

```c
UINT  _nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr,
                                          NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr,
                                    NX_SNMP_SECURITY_KEY *key)
```

<span data-ttu-id="a0279-207">È possibile creare chiavi separate per i messaggi trap.</span><span class="sxs-lookup"><span data-stu-id="a0279-207">Separate keys can be created for trap messages.</span></span> <span data-ttu-id="a0279-208">Per applicare le chiavi per i messaggi trap, sono disponibili le API seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0279-208">To apply keys for trap messages the following API are available:</span></span>

```c
UINT  _nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)

UINT  _nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr,
                                       NX_SNMP_SECURITY_KEY *key)
```

<span data-ttu-id="a0279-209">Per disabilitare l'autenticazione o la crittografia per i messaggi di risposta e i trap di invio, usare questi servizi con l'input del puntatore alla chiave impostato su NULL.</span><span class="sxs-lookup"><span data-stu-id="a0279-209">To disable authentication or encryption for response messages and sending traps, use these services with the key pointer input set to NULL.</span></span>

## <a name="netx-duo-snmp-community-strings"></a><span data-ttu-id="a0279-210">Stringhe della community SNMP di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-210">NetX Duo SNMP Community Strings</span></span>

<span data-ttu-id="a0279-211">L'agente SNMP NetX Duo supporta sia le stringhe di community pubbliche che private.</span><span class="sxs-lookup"><span data-stu-id="a0279-211">The NetX Duo SNMP Agent supports both public and private community strings.</span></span> <span data-ttu-id="a0279-212">La stringa pubblica viene impostata con il servizio *nx_snmp_agent _public_string_set* .</span><span class="sxs-lookup"><span data-stu-id="a0279-212">The public string is set with the *nx_snmp_agent _public_string_set* service.</span></span> <span data-ttu-id="a0279-213">La stringa privata dell'agente SNMP NetX Duo viene impostata tramite il servizio *nx_snmp_agent_private_string_set* .</span><span class="sxs-lookup"><span data-stu-id="a0279-213">The NetX Duo SNMP Agent private string is set using the *nx_snmp_agent_private_string_set* service.</span></span>

## <a name="netx-duo-snmp-username-callback"></a><span data-ttu-id="a0279-214">Callback nome utente SNMP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-214">NetX Duo SNMP Username Callback</span></span>

<span data-ttu-id="a0279-215">Il pacchetto dell'agente SNMP NetX Duo consente all'applicazione di specificare (tramite la chiamata ***nx_snmp_agent_create*** ) un callback del nome utente che viene chiamato all'inizio della gestione di ogni richiesta del client SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-215">The NetX Duo SNMP Agent package allows the application to specify (via the ***nx_snmp_agent_create*** call) a username callback  that is called at the beginning of handling each SNMP Client request.</span></span>

<span data-ttu-id="a0279-216">La routine di callback fornisce l'agente SNMP NetX Duo con il nome utente.</span><span class="sxs-lookup"><span data-stu-id="a0279-216">The callback routine provides the NetX Duo SNMP Agent with the username.</span></span> <span data-ttu-id="a0279-217">Se il nome utente specificato è valido o se non è necessario un controllo nome utente per la risposta alla richiesta, il callback del nome utente deve restituire il valore di **NX_SUCCESS**.</span><span class="sxs-lookup"><span data-stu-id="a0279-217">If the supplied username is valid or if no username check is necessary for the responding to the request, the username callback should return the value of **NX_SUCCESS**.</span></span> <span data-ttu-id="a0279-218">In caso contrario, la routine deve restituire **NX_SNMP_ERROR** per indicare che il nome utente specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="a0279-218">Otherwise, the routine should return **NX_SNMP_ERROR** to indicate the specified username is invalid.</span></span>

<span data-ttu-id="a0279-219">Il formato della routine di callback del nome utente dell'applicazione è definito di seguito:</span><span class="sxs-lookup"><span data-stu-id="a0279-219">The format of the application username callback routine is defined below:</span></span>

```c
UINT nx_snmp_agent_username_process(NX_SNMP_AGENT *agent_ptr,
                                    UCHAR *username);
```

<span data-ttu-id="a0279-220">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="a0279-220">The input parameters are defined as follows:</span></span>

| <span data-ttu-id="a0279-221">Parametro</span><span class="sxs-lookup"><span data-stu-id="a0279-221">Parameter</span></span> | <span data-ttu-id="a0279-222">Significato</span><span class="sxs-lookup"><span data-stu-id="a0279-222">Meaning</span></span>                                              |
|-----------|------------------------------------------------------|
| <span data-ttu-id="a0279-223">*agent_ptr*</span><span class="sxs-lookup"><span data-stu-id="a0279-223">*agent_ptr*</span></span> | <span data-ttu-id="a0279-224">Puntatore alla chiamata dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-224">Pointer to calling SNMP agent</span></span>                        |
| <span data-ttu-id="a0279-225">username</span><span class="sxs-lookup"><span data-stu-id="a0279-225">username</span></span>  | <span data-ttu-id="a0279-226">Destinazione per il puntatore al nome utente richiesto</span><span class="sxs-lookup"><span data-stu-id="a0279-226">Destination for the pointer to the required username</span></span> |

<span data-ttu-id="a0279-227">Per le sessioni SNMPv1 e SNMPv2/v2C, l'applicazione vuole esaminare la stringa della community in una richiesta SNMP in ingresso per determinare se la richiesta SNMP ha una stringa community valida.</span><span class="sxs-lookup"><span data-stu-id="a0279-227">For SNMPv1 and SNMPv2/v2C sessions, the application will want to examine the community string on an incoming SNMP request to determine if the SNMP request has a valid community string.</span></span> <span data-ttu-id="a0279-228">Sono disponibili diversi servizi per l'applicazione SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-228">There are several services for the SNMP application to do this.</span></span>

<span data-ttu-id="a0279-229">L'applicazione SNMP può verificare se la richiesta corrente di gestione SNMP è GET, ad esempio GET, GetNext o GetBulk, oppure impostare il tipo di richiesta utilizzando questo servizio:</span><span class="sxs-lookup"><span data-stu-id="a0279-229">The SNMP application can inquire if the current SNMP Manager request is a GET (e.g. GET, GETNEXT, or GETBULK) or SET type of request using this service:</span></span>

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

<span data-ttu-id="a0279-230">Se la richiesta è un tipo GET, l'applicazione dovrà confrontare la stringa della community di input con la stringa pubblica dell'agente SNMP:</span><span class="sxs-lookup"><span data-stu-id="a0279-230">If the request is a GET type, the application will want to compare the input community string to the SNMP Agent’s public string:</span></span>

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr,
                                      UCHAR *username,
                                      UINT *is_public);
```

<span data-ttu-id="a0279-231">Analogamente, se la richiesta è un tipo SET, l'applicazione dovrà confrontare la stringa della community di input con la stringa privata dell'agente SNMP:</span><span class="sxs-lookup"><span data-stu-id="a0279-231">Similarly if the request is a SET type, the application will want to compare the input community string to the SNMP Agent’s private string:</span></span>

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr,
                                       UCHAR *username,
                                       UINT *is_private);
```

<span data-ttu-id="a0279-232">I valori restituiti is_public e is_private indicano rispettivamente se la stringa della community di input è una stringa community pubblica o privata valida.</span><span class="sxs-lookup"><span data-stu-id="a0279-232">The is_public and is_private return values indicate respectively if the input community string is a valid public or private community string.</span></span>

<span data-ttu-id="a0279-233">Il valore restituito dalla routine di callback username indica se il nome utente è valido.</span><span class="sxs-lookup"><span data-stu-id="a0279-233">The return value of the username callback routine indicates if the username is valid.</span></span> <span data-ttu-id="a0279-234">Il valore **NX_SUCCESS** viene restituito se il nome utente è valido oppure **NX_SNMP_ERROR** se il nome utente non è valido.</span><span class="sxs-lookup"><span data-stu-id="a0279-234">The value **NX_SUCCESS** is returned if the username is valid, or **NX_SNMP_ERROR** if the username is invalid.</span></span>

## <a name="netx-duo-snmp-agent-get-callback"></a><span data-ttu-id="a0279-235">Callback di GET dell'agente SNMP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-235">NetX Duo SNMP Agent GET Callback</span></span>

<span data-ttu-id="a0279-236">L'applicazione deve impostare una routine di callback per la gestione delle richieste di oggetti GET da gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-236">The application must set a callback routine for handling GET object requests from the SNMP Manager.</span></span> <span data-ttu-id="a0279-237">Il callback recupera il valore dell'oggetto specificato nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="a0279-237">The callback retrieves the value of the object specified in the request.</span></span>

<span data-ttu-id="a0279-238">La routine di callback di richiesta GET dell'applicazione è definita di seguito:</span><span class="sxs-lookup"><span data-stu-id="a0279-238">The application GET request callback routine is defined below:</span></span>

```c
UINT nx_snmp_agent_get_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

<span data-ttu-id="a0279-239">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="a0279-239">The input parameters are defined as follows:</span></span>

| <span data-ttu-id="a0279-240">Parametro</span><span class="sxs-lookup"><span data-stu-id="a0279-240">Parameter</span></span>        | <span data-ttu-id="a0279-241">Significato</span><span class="sxs-lookup"><span data-stu-id="a0279-241">Meaning</span></span> |
|------------------|----------------------------------|
| <span data-ttu-id="a0279-242">*agent_ptr*</span><span class="sxs-lookup"><span data-stu-id="a0279-242">*agent_ptr*</span></span>        | <span data-ttu-id="a0279-243">Puntatore alla chiamata dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-243">Pointer to calling SNMP agent</span></span> |
| <span data-ttu-id="a0279-244">object_requested</span><span class="sxs-lookup"><span data-stu-id="a0279-244">object_requested</span></span> | <span data-ttu-id="a0279-245">Stringa ASCII che rappresenta l'ID oggetto a cui è destinata l'operazione GET.</span><span class="sxs-lookup"><span data-stu-id="a0279-245">ASCII string representing the object ID the GET operation is for.</span></span> |
| <span data-ttu-id="a0279-246">object_data</span><span class="sxs-lookup"><span data-stu-id="a0279-246">object_data</span></span>      | <span data-ttu-id="a0279-247">Struttura dei dati per conservare il valore recuperato dal callback.</span><span class="sxs-lookup"><span data-stu-id="a0279-247">Data structure to hold the value retrieved by the callback.</span></span> <span data-ttu-id="a0279-248">Questa impostazione può essere configurata con una serie di API SNMP NetX Duo descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="a0279-248">This can be set with a series of NetX Duo SNMP API’s described below.</span></span> |

> [!NOTE]
> <span data-ttu-id="a0279-249">*Per le stringhe di ottetti, all'oggetto deve essere assegnata la lunghezza in modo che la funzione interna sappia quanto tempo la lunghezza è perché il callback stesso non ha un argomento length:*</span><span class="sxs-lookup"><span data-stu-id="a0279-249">*For octet strings, the object must be assigned the length so that the internal function knows how long the length is since the callback itself does not have a length argument:*</span></span>

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

<span data-ttu-id="a0279-250">Poiché il tipo di dati non è noto al callback GET, non è necessario controllare il tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="a0279-250">Since the type of data is not known to the GET callback, there is no need to check the data type.</span></span> <span data-ttu-id="a0279-251">La lunghezza non avrà alcun effetto sui tipi numerici o sulle stringhe delimitate da valori null.</span><span class="sxs-lookup"><span data-stu-id="a0279-251">Length will not have any effect on numeric types or strings which are null delimited.</span></span>

<span data-ttu-id="a0279-252">Chiamare quindi la funzione interna:</span><span class="sxs-lookup"><span data-stu-id="a0279-252">Then call the internal function:</span></span>

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

<span data-ttu-id="a0279-253">Se la funzione di callback non riesce a trovare l'oggetto richiesto, viene restituito il codice di errore **NX_SNMP_ERROR_NOSUCHNAME** .</span><span class="sxs-lookup"><span data-stu-id="a0279-253">If the callback function cannot find the requested object, the **NX_SNMP_ERROR_NOSUCHNAME** error code should be returned.</span></span> <span data-ttu-id="a0279-254">Se viene rilevato un altro errore, è necessario che venga restituito il **NX_SNMP_ERROR** .</span><span class="sxs-lookup"><span data-stu-id="a0279-254">If any other error is detected, the **NX_SNMP_ERROR** should be returned.</span></span>

## <a name="netx-duo-snmp-agent-getnext-callback"></a><span data-ttu-id="a0279-255">Callback GetNext Agent NetX Duo SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-255">NetX Duo SNMP Agent GETNEXT Callback</span></span>

<span data-ttu-id="a0279-256">L'applicazione deve inoltre impostare la routine di callback per le richieste di oggetti GetNext da gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-256">The application must also set the callback routine for GETNEXT object requests from the SNMP Manager.</span></span> <span data-ttu-id="a0279-257">Il callback GetNext Recupera il valore dell'oggetto successivo specificato dalla richiesta.</span><span class="sxs-lookup"><span data-stu-id="a0279-257">The GETNEXT callback retrieves the value of the next object specified by the request.</span></span>

<span data-ttu-id="a0279-258">La routine di callback di richiesta GetNext dell'applicazione è definita di seguito:</span><span class="sxs-lookup"><span data-stu-id="a0279-258">The application GETNEXT request callback routine is defined below:</span></span>

```c
UINT nx_snmp_agent_getnext_process(NX_SNMP_AGENT *agent_ptr,
                                   UCHAR *object_requested,
                                   NX_SNMP_OBJECT_DATA *object_data);
```

<span data-ttu-id="a0279-259">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="a0279-259">The input parameters are defined as follows:</span></span>

| <span data-ttu-id="a0279-260">Parametro</span><span class="sxs-lookup"><span data-stu-id="a0279-260">Parameter</span></span>        | <span data-ttu-id="a0279-261">Significato</span><span class="sxs-lookup"><span data-stu-id="a0279-261">Meaning</span></span> |
|------------------|-------------------------------------------|
| <span data-ttu-id="a0279-262">*agent_ptr*</span><span class="sxs-lookup"><span data-stu-id="a0279-262">*agent_ptr*</span></span>        | <span data-ttu-id="a0279-263">Puntatore alla chiamata dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-263">Pointer to calling SNMP agent</span></span> |
| <span data-ttu-id="a0279-264">object_requested</span><span class="sxs-lookup"><span data-stu-id="a0279-264">object_requested</span></span> | <span data-ttu-id="a0279-265">Stringa ASCII che rappresenta l'ID oggetto a cui è destinata l'operazione GetNext.</span><span class="sxs-lookup"><span data-stu-id="a0279-265">ASCII string representing the object ID the GETNEXT operation is for.</span></span> |
| <span data-ttu-id="a0279-266">object_data</span><span class="sxs-lookup"><span data-stu-id="a0279-266">object_data</span></span>      | <span data-ttu-id="a0279-267">Struttura dei dati per conservare il valore recuperato dal callback.</span><span class="sxs-lookup"><span data-stu-id="a0279-267">Data structure to hold the value retrieved by the callback.</span></span> <span data-ttu-id="a0279-268">Questa impostazione può essere configurata con una serie di API SNMP NetX Duo descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="a0279-268">This can be set with a series of NetX Duo SNMP API’s described below.</span></span> |

<span data-ttu-id="a0279-269">Analogamente a quanto avviene per i callback GET, è necessario assegnare a oggetti con dati stringa ottetto la lunghezza, in modo che la funzione interna sappia quanto tempo la lunghezza è perché il callback stesso non ha un argomento length:</span><span class="sxs-lookup"><span data-stu-id="a0279-269">Same as is true for GET callbacks, objects with octet string data must be assigned the length so that the internal function knows how long the length is since the callback itself does not have a length argument:</span></span>

```c
object_data -> nx_snmp_object_octet_string_size = mib2_mib[i].length;
```

<span data-ttu-id="a0279-270">Poiché il tipo di dati non è noto al callback GET, non è necessario controllare il tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="a0279-270">Since the type of data is not known to the GET callback, there is no need to check the data type.</span></span> <span data-ttu-id="a0279-271">La lunghezza non avrà alcun effetto sui tipi numerici o sulle stringhe delimitate da valori null.</span><span class="sxs-lookup"><span data-stu-id="a0279-271">Length will not have any effect on numeric types or strings which are null delimited.</span></span>

<span data-ttu-id="a0279-272">Chiamare quindi la funzione interna:</span><span class="sxs-lookup"><span data-stu-id="a0279-272">Then call the internal function:</span></span>

```c
status = mib2_mib[i].object_get_callback)
                   (mib2_mib[i].object_value_ptr, object_data);
```

<span data-ttu-id="a0279-273">Se la funzione di callback non riesce a trovare l'oggetto richiesto, viene restituito il codice di errore **NX_SNMP_ERROR_NOSUCHNAME** .</span><span class="sxs-lookup"><span data-stu-id="a0279-273">If the callback function cannot find the requested object, the **NX_SNMP_ERROR_NOSUCHNAME** error code should be returned.</span></span> <span data-ttu-id="a0279-274">Se viene rilevato un altro errore, è necessario che venga restituito il **NX_SNMP_ERROR** .</span><span class="sxs-lookup"><span data-stu-id="a0279-274">If any other error is detected, the **NX_SNMP_ERROR** should be returned.</span></span>

## <a name="netx-duo-snmp-agent-set-callback"></a><span data-ttu-id="a0279-275">Callback SET agenti SNMP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-275">NetX Duo SNMP Agent SET Callback</span></span>

<span data-ttu-id="a0279-276">L'applicazione deve impostare la routine di callback per la gestione delle richieste di oggetti SET da gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-276">The application should set the callback routine for handling SET object requests from the SNMP Manager.</span></span> <span data-ttu-id="a0279-277">Il callback SET imposta il valore dell'oggetto specificato dalla richiesta.</span><span class="sxs-lookup"><span data-stu-id="a0279-277">The SET callback sets the value of the object specified by the request.</span></span>

<span data-ttu-id="a0279-278">La routine di callback della richiesta del SET di applicazioni è definita di seguito:</span><span class="sxs-lookup"><span data-stu-id="a0279-278">The application SET request callback routine is defined below:</span></span>

```c
UINT nx_snmp_agent_set_process(NX_SNMP_AGENT *agent_ptr,
                               UCHAR *object_requested,
                               NX_SNMP_OBJECT_DATA *object_data);
```

<span data-ttu-id="a0279-279">I parametri di input sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="a0279-279">The input parameters are defined as follows:</span></span>

| <span data-ttu-id="a0279-280">Parametro</span><span class="sxs-lookup"><span data-stu-id="a0279-280">Parameter</span></span>        | <span data-ttu-id="a0279-281">Significato</span><span class="sxs-lookup"><span data-stu-id="a0279-281">Meaning</span></span> |
|------------------|-------- |
| <span data-ttu-id="a0279-282">*agent_ptr*</span><span class="sxs-lookup"><span data-stu-id="a0279-282">*agent_ptr*</span></span>      | <span data-ttu-id="a0279-283">Puntatore alla chiamata dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="a0279-283">Pointer to calling SNMP agent</span></span> |
| <span data-ttu-id="a0279-284">object_requested</span><span class="sxs-lookup"><span data-stu-id="a0279-284">object_requested</span></span> | <span data-ttu-id="a0279-285">Stringa ASCII che rappresenta l'ID oggetto a cui è destinata l'operazione di impostazione.</span><span class="sxs-lookup"><span data-stu-id="a0279-285">ASCII string representing the object ID the SET operation is for.</span></span> |
| <span data-ttu-id="a0279-286">object_data</span><span class="sxs-lookup"><span data-stu-id="a0279-286">object_data</span></span>      | <span data-ttu-id="a0279-287">Struttura di dati che contiene il nuovo valore per l'oggetto specificato.</span><span class="sxs-lookup"><span data-stu-id="a0279-287">Data structure that contains the new value for the specified object.</span></span> <span data-ttu-id="a0279-288">L'operazione effettiva può essere eseguita usando l'API SNMP NetX Duo descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="a0279-288">The actual operation can be done using the NetX Duo SNMP API’s described below.</span></span> |

<span data-ttu-id="a0279-289">Si noti che per le stringhe ottetto, il callback SET deve aggiornare la tabella MIB con la lunghezza dei dati, perché l'agente SNMP ha analizzato i dati e conosce il tipo e la lunghezza:</span><span class="sxs-lookup"><span data-stu-id="a0279-289">Note that for octet strings, the SET callback should update the MIB table with the length of the data since the SNMP Agent has parsed the data and knows the type and length:</span></span>

```c
if (object_data -> nx_snmp_object_data_type ==
                           NX_SNMP_ANS1_OCTET_STRING)
{
    mib2_mib[i].length =
        object_data -> nx_snmp_object_octet_string_size;
}

object_data -> nx_snmp_object_octet_string_size =
                                 mib2_mib[i].length;
```

<span data-ttu-id="a0279-290">Se la funzione di callback non riesce a trovare l'oggetto richiesto, viene restituito il codice di errore **NX_SNMP_ERROR_NOSUCHNAME** .</span><span class="sxs-lookup"><span data-stu-id="a0279-290">If the callback function cannot find the requested object, the **NX_SNMP_ERROR_NOSUCHNAME** error code should be returned.</span></span>

<span data-ttu-id="a0279-291">Se l'host SNMP NetX duo ha creato stringhe di community private e il mittente SNMP della richiesta SET non ha la stringa privata corrispondente, può restituire un errore **NX_SNMP_ERROR_NOACCESS** .</span><span class="sxs-lookup"><span data-stu-id="a0279-291">If the NetX Duo SNMP host has created private community strings, and the SNMP sender of the SET request does not have the matching private string, it may return an **NX_SNMP_ERROR_NOACCESS** error.</span></span> <span data-ttu-id="a0279-292">Se viene rilevato un altro errore, è necessario che venga restituito il **NX_SNMP_ERROR** .</span><span class="sxs-lookup"><span data-stu-id="a0279-292">If any other error is detected, the **NX_SNMP_ERROR** should be returned.</span></span>

> [!NOTE]
> <span data-ttu-id="a0279-293">*Sebbene l'agente SNMP di NetX Duo fornisca un database MIB SNMP con la distribuzione, è principalmente a scopo di test e sviluppo. È probabile che lo sviluppatore richieda un database MIB proprietario per un'applicazione SNMP professionale.*</span><span class="sxs-lookup"><span data-stu-id="a0279-293">*Although NetX Duo SNMP Agent supplies an SNMP MIB database with the distribution, it is primarily for testing and development purposes. The developer will likely require a proprietary MIB database for a professional SNMP application.*</span></span>

## <a name="changing-snmp-version-at-run-time"></a><span data-ttu-id="a0279-294">Modifica della versione di SNMP in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="a0279-294">Changing SNMP Version at Run Time</span></span>

<span data-ttu-id="a0279-295">L'host agente SNMP può modificare la versione SNMP per ognuna delle tre versioni in fase di esecuzione utilizzando il servizio *nx_snmp_agent_set_version* .</span><span class="sxs-lookup"><span data-stu-id="a0279-295">The SNMP Agent host can change SNMP version for each of the three versions at run time using the *nx_snmp_agent_set_version* service.</span></span> <span data-ttu-id="a0279-296">Per impostazione predefinita, l'agente SNMP è abilitato per tutte e tre le versioni quando viene creato l'agente SNMP in *nx_snmp_agent_create*.</span><span class="sxs-lookup"><span data-stu-id="a0279-296">The SNMP Agent is by default enabled for all three versions when the SNMP Agent is created in *nx_snmp_agent_create*.</span></span> <span data-ttu-id="a0279-297">Tuttavia, l'applicazione può limitarla a un subset di tutte le versioni.</span><span class="sxs-lookup"><span data-stu-id="a0279-297">However, the application can limit that to a subset of all versions.</span></span>

> [!NOTE]
> <span data-ttu-id="a0279-298">*Se le opzioni di configurazione NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 e/o NX_SNMP_DISABLE_V3 sono definite, questa funzione non avrà alcun effetto sull'abilitazione delle versioni effettive.*</span><span class="sxs-lookup"><span data-stu-id="a0279-298">*If the configuration options NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 and/or NX_SNMP_DISABLE_V3 are defined, this function will have no effect enabling the effected versions.*</span></span>

<span data-ttu-id="a0279-299">L'agente SNMP può recuperare la versione SNMP del pacchetto SNMP più recente ricevuto tramite il servizio *nx_snmp_agent_get_current_version* .</span><span class="sxs-lookup"><span data-stu-id="a0279-299">The SNMP Agent can retrieve the SNMP version of the latest SNMP packet received using the *nx_snmp_agent_get_current_version* service.</span></span>

## <a name="snmpv3-discovery"></a><span data-ttu-id="a0279-300">Individuazione SNMPv3</span><span class="sxs-lookup"><span data-stu-id="a0279-300">SNMPv3 Discovery</span></span>

<span data-ttu-id="a0279-301">L'agente SNMP, se abilitato per SNMPv3, risponderà alle richieste di individuazione da gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="a0279-301">The SNMP Agent, if enabled for SNMPv3, will respond to discovery requests from the SNMP Manager.</span></span> <span data-ttu-id="a0279-302">Tale richiesta contiene i dati dei parametri di sicurezza con valori null per l'ID del motore autorevole, il nome utente, il numero di avvio e l'ora di avvio.</span><span class="sxs-lookup"><span data-stu-id="a0279-302">Such a request contains security parameter data with null values for Authoritative Engine ID, user name, boot count and boot time.</span></span> <span data-ttu-id="a0279-303">I parametri di autenticazione non vengono applicati al messaggio di individuazione.</span><span class="sxs-lookup"><span data-stu-id="a0279-303">Authentication parameters are not applied to the DISCOVERY message.</span></span> <span data-ttu-id="a0279-304">L'elenco di associazioni variabili nella richiesta è vuoto (contiene zero elementi).</span><span class="sxs-lookup"><span data-stu-id="a0279-304">The variable binding list in the request is empty (contains zero items).</span></span> <span data-ttu-id="a0279-305">L'agente SNMP risponde con un'ora di avvio e un conteggio pari a zero e l'elenco di associazioni di variabili contenente 1 elemento, *usmStatsUnknownEngineIDs*, che corrisponde al numero di richieste ricevute con un ID di motore sconosciuto (null).</span><span class="sxs-lookup"><span data-stu-id="a0279-305">The SNMP agent responds with a zero boot time and count, and the variable binding list containing 1 item, *usmStatsUnknownEngineIDs*, which is the count of requests received with an unknown (null) engine ID.</span></span> <span data-ttu-id="a0279-306">Alla successiva richiesta GetNext dal browser o dal gestore, i dati di avvio e i parametri di sicurezza vengono compilati solo se è abilitata la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a0279-306">On the subsequent GETNEXT request from the Browser/Manager, the boot data and security parameters are filled in only if security is enabled.</span></span> <span data-ttu-id="a0279-307">In tal caso, verrà inviato anche un aggiornamento dei dati di NotInTime in PDU.</span><span class="sxs-lookup"><span data-stu-id="a0279-307">If so it will also send a NotInTime data update in the PDU.</span></span> <span data-ttu-id="a0279-308">I parametri di sicurezza, ad esempio l'autenticazione, dimostrano l'identità dell'agente al responsabile.</span><span class="sxs-lookup"><span data-stu-id="a0279-308">The security parameters, e.g. authentication prove the identity of the Agent to the Manager.</span></span>

<span data-ttu-id="a0279-309">Informazioni più dettagliate sull'autenticazione SNMPv3 sono disponibili in RFC 3414 "user-based Security Model (USM) per la versione 3 del Simple Network Management Protocol (SNMPv3)".</span><span class="sxs-lookup"><span data-stu-id="a0279-309">More detailed information on SNMPv3 authentication is available in RFC 3414 “User-based Security Model (USM) for version 3 of the Simple Network Management Protocol (SNMPv3)”.</span></span>

## <a name="netx-duo-snmp-rfcs"></a><span data-ttu-id="a0279-310">RFC SNMP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="a0279-310">NetX Duo SNMP RFCs</span></span>

<span data-ttu-id="a0279-311">NetX Duo SNMP è conforme a RFC1155, RFC1157, RFC1215, RFC1901, RFC1905, RFC1906, RFC1907, RFC1908, RFC2571, RFC2572, RFC2574, RFC2575, RFC 3414 e RFC correlate.</span><span class="sxs-lookup"><span data-stu-id="a0279-311">NetX Duo SNMP is compliant with RFC1155, RFC1157, RFC1215, RFC1901, RFC1905, RFC1906, RFC1907, RFC1908, RFC2571, RFC2572, RFC2574, RFC2575, RFC 3414 and related RFCs.</span></span>
